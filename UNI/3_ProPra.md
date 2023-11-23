# Info Talk
- Feedback Runden verpflichtend, Zuteilung erfolgt nächste Woche
- Über GitLab abgeben (JAR mit src code) wöchentlich aber Feedback nur jede zweite

# Discord
## Tickets
- Eröffnen mit /open im Chat

# Deadlines
- 07.12.23



# Backupcode
``java
    @Override
    public GameStatus gameStatus(){
        ArrayList<HashSet<Integer>> winConds = new ArrayList<>();

        // check all rows
        for (int i = 0; i < gameSize; i++) {
            HashSet<Integer> row = new HashSet<>();
            for (int j = 0; j < gameSize; j++) {
                int currField = getBoard()[i][j];
                if(currField != 0) {
                    row.add(getBoard()[i][j]);
                }
            }
                winConds.add(row);
        }


        // check all cols
        for (int i = 0; i < gameSize; i++) {
            HashSet<Integer> col = new HashSet<>();
            for (int j = 0; j < gameSize; j++) {
                int currField = getBoard()[i][j];
                if(currField != 0) {
                    col.add(getBoard()[j][i]);
                }
            }
            winConds.add(col);
        }

        // check all Diags
        for (int i = 0; i < gameSize; i++) {
            HashSet<Integer> diag1 = new HashSet<>();
            HashSet<Integer> diag2 = new HashSet<>();

            int currField1 = getBoard()[i][i];
            int currField2 = getBoard()[gameSize-1-i][gameSize-1-i];

            if(currField1 != 0) {
                diag1.add(currField1);
            }

            if(currField2 != 0) {
                diag2.add(currField2);
            }

            winConds.add(diag1);
            winConds.add(diag2);
        }

        // check draw
        if(getRoundCounter() == gameSize*gameSize){
            return GameStatus.DRAW;
        }
        // now checking win conditions
        for (HashSet<Integer> conds : winConds){
           if (conds.size() == 1){
               if(conds.contains(1)){
                   return GameStatus.PLAYER_1_WON;
               }
               return GameStatus.PLAYER_2_WON;
           }
        }

        return GameStatus.RUNNING;
    }
```
