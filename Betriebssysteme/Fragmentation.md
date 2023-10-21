
### external
- unbenutzter Speicher außerhalb des allokierten Speicherblocks
- es werden Speicherfragmente kreiert durch Allokation, die nicht mehr benutzt werden können, da sie zu klein sind
- list-based strategies(first fit, best fit) and buddy system wenn Mergen nicht möglich ist
- Häufiges swapping in-/out(start/termination) von Prozessen bei Segmentierung 
-> Mergen von Löchern im Speicher, Reallokation von Speicher

### internal
- unbenutzter Speicher innerhalb des allokierten Speicherblocks
- Buddy System- immer nächste zweier Potenz, daher oft interne Fragmentierung, 
- Paging, da Blockgröße nicht immer vollständig benutzt werden kann
- schwierig zu entdecken, invalide Pointer in fragmentierten Speicherbereich
-> schwierig zu behandeln: Passe die Beschaffenheit des Speichers dem 
memory Speicherallokationsprinzip an 