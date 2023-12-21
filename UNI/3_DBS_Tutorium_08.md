--- DBS Aufgabe 8-1 ---

--- ( a ) ---

SELECT DISTINCT v.vorlNr, v.titel, ROUND(avg(pruef.note), 3) as 'avgNote'
    FROM Vorlesungen v, Pruefungen pruef
        WHERE v.vorlNr = pruef.vorlNr
            GROUP BY v.vorlNr;


--- ( b ) ---

SELECT DISTINCT prof.persNr, prof.name, count(v.vorlNr) as myCount
    FROM Professoren prof LEFT OUTER JOIN Vorlesungen v
        ON prof.persNr = v.gelesenVon
            GROUP BY prof.persNr, prof.name
                ORDER BY myCount DESC;


--- ( c ) ---

select s1.matrNr, s1.name, count(distinct h2.matrNr)
from hoeren h1, hoeren h2, Studenten s1, Studenten s2
where s1.semester < s2.semester and h1.vorlNr = h2.vorlNr and h1.matrNr = s1.matrNr and h2.matrNr = s2.matrNr
group by s1.matrNr, s1.name
having count(distinct h2.matrNr) >= 3;


--- ( d ) ---

select persNr, name
from Professoren p join 
(
select gelesenVon, matrNr from hoeren natural join Vorlesungen
group by gelesenVon, matrNr
having count(*) >= 3
) 
profStud on p.persNr = profStud.gelesenVon
group by persNr, name
having count(*) >=2;


--- ( e ) ---

--- Wir suchen die Vorlesungen, die mind. eine Vorlesung als Voraussetzung haben.
create view VorlesungenMitVoraussetzung as (
select distinct vorlNr, titel
from Vorlesungen v join Voraussetzungen vorausg on v.vorlNr = vorausg.vorlesung
);

--- Wir bringen solche Vorlesungen, die mind. eine Voraussetzung haben, mit ihren Zuhörern (Studenten) zusammen. 
--- Wir gruppieren nach den jeweiligen Vorlesungen und selektieren nur solche, die von Studenten aus mind. zwei verschiedenen (daher distinct) Semestern gehört werden.
--- Wir erhalten Gruppen (jeweils eine Vorlesung mit mehreren Studenten). Wir zählen die Anzahl der Studenten (myCount). 
--- myCount werden wir später als Nenner zur Berechnung des Prozentsatzes benötigen.
create view GruppierungNachVorlesung as (
select vorlNr, titel, count(*) as myCount
from VorlesungenMitVoraussetzung natural join hoeren natural join Studenten
group by vorlNr, titel
having count(distinct semester) >= 2
);

--- Wir bringen die Vorlesungen aus GruppierungNachVorlesung wieder mit den Zuhörern zusammen. Wir gruppieren diesmal zusätzlich nach Vorlesung und Semester. 
--- Per count(*) in der "select"-Klausel zählen wir, wie viele Studenten aus dem jeweiligen Semester die jeweilige Vorlesung hören.
--- Wir berechnen den Anteil per (Studenten aus dem jeweiligen Semester) geteilt durch (Studenten in der Vorlesung insgesamt). Über *100 erhalten wir den Prozentsatz.
select vorlNr, titel, semester, round(count(*) / myCount * 100, 2) as Prozentsatz
from GruppierungNachVorlesung natural join hoeren natural join Studenten
group by vorlNr, titel, semester 
order by titel asc, Prozentsatz desc, semester asc;



--- DBS Aufgabe 8-2 ---

--- ( a ) ---

select art_nr, art_bez, lagerort, lagerbest
from Inventar
where lagerort in ('Hamburg', 'Muenchen');


--- ( b ) ---

select auftr_nr, i.art_nr, menge, lagerbest, lagerort
from Auftragsposten a , Inventar i
where a.art_nr = i.art_nr and i.art_nr = 203333 and a.menge <= i.lagerbest;


--- ( c ) ---

--- Funktioniert nicht in der Schnittstelle.
select k.kund_nr
from Kunde k
except (select v.kund_nr from Verkauf v);

--- Funktioniert in der Schnittstelle.
select k.kund_nr
from Kunde k
where kund_nr not in (select v.kund_nr from Verkauf v);


--- ( d ) ---

select distinct lagerort 
from Inventar
where lagerbest >= 8;


--- ( e ) ---

select distinct vorname, nachname 
from Personal p
where exists (
   select * from Verkauf v natural join Kunde k where p.pers_nr = v.pers_nr and k.ort = 'Stuttgart'
);


--- ( f ) ---

select distinct nachname, vorname, einsatz, gehalt
from Personal
order by einsatz asc, gehalt desc;


--- ( g ) ---

select pers_nr, gehalt
from Personal 
where gehalt = (select min(gehalt) from Personal)
        or gehalt = (select max(gehalt) from Personal);


--- ( h ) ---

select einsatz, count(*)
from Personal
group by (einsatz);


--- ( i ) ---

select avg(abc.myCount)
from  (
   select einsatz, count(*) as myCount
   from Personal
   group by (einsatz)
) abc;


--- ( j ) ---

select art_nr, sum(lagerbest)
from Inventar
group by art_nr
having sum(lagerbest) > 10;
