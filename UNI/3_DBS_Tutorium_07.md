-- DBS Aufgabe 7-1

--- ( a ) ---

--- mit Join-Operation: ---

SELECT DISTINCT i.art_nr, i.art_bez
    FROM Inventar i, Personal p
        WHERE ((p.nachname = 'Winter' AND p.vorname = 'Margot' AND p.gehalt = i.preis)
            OR (p.nachname = 'Hartinger' AND p.vorname = 'Roswita' AND p.gehalt = i.preis));


--- mit Unterabfragen: ---

SELECT DISTINCT i.art_nr, i.art_bez
    FROM Inventar i
        WHERE EXISTS (
            SELECT * FROM Personal p WHERE ((p.nachname = 'Winter' AND p.vorname = 'Margot' AND p.gehalt = i.preis) 
                OR (p.nachname = 'Hartinger' AND p.vorname = 'Roswita' AND p.gehalt = i.preis))
        );


--- Alternativ ist die Unterabfrage auch via IN ... SELECT möglich: ---

SELECT DISTINCT i.art_nr, i.art_bez
    FROM Inventar i
        WHERE i.preis IN (
		    SELECT p.gehalt FROM Personal p
			    WHERE (p.nachname = 'Winter' AND p.vorname = 'Margot') 
                OR (p.nachname = 'Hartinger' AND p.vorname = 'Roswita')
	    );



--- ( b ) ---

--- mit Join-Operation: ---

SELECT DISTINCT k.kund_name
    FROM Kunde k, Personal p, Verkauf v
        WHERE (k.kund_nr = v.kund_nr AND p.pers_nr = v.pers_nr AND v.bestelldatum = '2023-07-24' AND p.einsatz = 'Hamburg');


--- mit Unterabfragen: ---

SELECT DISTINCT k.kund_name
    FROM Kunde k
        WHERE EXISTS (
            SELECT * FROM Verkauf v WHERE (
                v.bestelldatum = '2023-07-24' AND v.kund_nr = k.kund_nr AND EXISTS(
                    SELECT * FROM Personal p 
                        WHERE (p.pers_nr = v.pers_nr AND p.einsatz = 'Hamburg')
                )
            )
        );



--- ( c ) ---

SELECT vorname, nachname, gehalt
    FROM Personal
        ORDER BY gehalt DESC, nachname ASC, vorname ASC;



--- ( d ) ---

SELECT DISTINCT art_nr, art_bez, preis 
    FROM Inventar i1
        WHERE NOT EXISTS (SELECT * FROM Inventar i2 WHERE i2.preis < i1.preis);



--- ( e ) ---

SELECT a.art_nr
    FROM Auftragsposten a NATURAL JOIN Verkauf v NATURAL JOIN Kunde k 
        WHERE k.ort = 'Stuttgart'
        GROUP BY a.art_nr
        HAVING count(DISTINCT kund_nr) >= 2;


--- Möglichkeit mit sehr basic Syntak: Iteriere über alle Tupel Auftragsposten, Verkauf, Kunde und schaue, ob jeweils ein anderer Stuttgarter Kunde existiert, der denselben Artikel gekauft hat.

SELECT DISTINCT auftr.art_nr
    FROM Auftragsposten auftr, Verkauf v, Kunde k1
        WHERE (
            auftr.auftr_nr = v.auftr_nr
            AND v.kund_nr = k1.kund_nr
            AND k1.ort = 'Stuttgart'  
            AND EXISTS(
                SELECT * FROM Kunde k2 WHERE(
                    k1.kund_nr <> k2.kund_nr
                    AND k2.ort = 'Stuttgart'
                    AND EXISTS(
                        SELECT * FROM Auftragsposten auftr2, Verkauf v2 WHERE(
                            auftr2.auftr_nr = v2.auftr_nr 
                            AND v2.kund_nr = k2.kund_nr 
                            AND auftr2.art_nr = auftr.art_nr
                        )
                    )
                )
            )
        );




-- DBS Aufgabe 7-2

--- ( a ) ---

SELECT k.kund_nr, k.Kund_name
    FROM Kunde k 
        WHERE NOT EXISTS (SELECT * 
            FROM Verkauf v 
                WHERE k.kund_nr = v.kund_nr);

            
--- ( b ) ---

SELECT p.pers_nr, p.nachname
    FROM Personal p
        WHERE NOT EXISTS (SELECT *
            FROM Kunde k 
                WHERE k.ort = 'Landshut' AND NOT EXISTS (SELECT *
                    FROM Verkauf v
                        WHERE v.kund_nr = k.kund_nr AND v.pers_nr = p.pers_nr) 
        )
