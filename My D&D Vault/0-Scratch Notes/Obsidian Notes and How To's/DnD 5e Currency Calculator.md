This calculator can be used to calculate the conversion of currencies commonly used in the Forgotten Realms.

##### Required Plugins

[Meta Bind](obsidian://show-plugin?id=obsidian-meta-bind-plugin) The calculator is coded with Meta Bind and relies on this to function.

#### Instructions

1. Create a new note and call it whatever you like.
2. Copy the template below into the new note ensuring that there are no blank lines above the top of the template. The `---` must be at the top of the note.

```
---
CoinsCopper: 2000
CoinsSiler: 1
CoinsElectrum: 20
CoinsGold: 1
CoinsPlatinum: 100
PartySize: 2
---

# Amount
 
 | Type     | Input                         | Copper                       | Silver                      | Electrum                   | Gold                       | Platinum                   |
 | -------- | ----------------------------- | ---------------------------- | --------------------------- | -------------------------- | -------------------------- | -------------------------- |
 | Copper   | `INPUT[number:CoinsCopper]`   | `VIEW[{CoinsCopper}]`        | `VIEW[{CoinsCopper}/10]`    | `VIEW[{CoinsCopper}/50]`   | `VIEW[{CoinsCopper}/100]`  | `VIEW[{CoinsCopper}/1000]` |
 | Silver   | `INPUT[number:CoinsSiler]`    | `VIEW[{CoinsSiler}*10]`      | `VIEW[{CoinsSiler}]`        | `VIEW[{CoinsSiler}/5]`     | `VIEW[{CoinsSiler}/10]`    | `VIEW[{CoinsSiler}/100]`   |
 | Electrum | `INPUT[number:CoinsElectrum]` | `VIEW[{CoinsElectrum}*50]`   | `VIEW[{CoinsElectrum}*5]`   | `VIEW[{CoinsElectrum}]`    | `VIEW[{CoinsElectrum}/2]`  | `VIEW[{CoinsElectrum}/20]` |
 | Gold     | `INPUT[number:CoinsGold]`     | `VIEW[{CoinsGold}*100]`      | `VIEW[{CoinsGold}*10]`      | `VIEW[{CoinsGold}*2]`      | `VIEW[{CoinsGold}]`        | `VIEW[{CoinsGold}/10]`     |
 | Platinum | `INPUT[number:CoinsPlatinum]` | `VIEW[{CoinsPlatinum}*1000]` | `VIEW[{CoinsPlatinum}*100]` | `VIEW[{CoinsPlatinum}*20]` | `VIEW[{CoinsPlatinum}*10]` | `VIEW[{CoinsPlatinum}]`    | 
 
 ## Total Converted Value
 
 Party Size: `INPUT[number:PartySize]`  
 
 | Type     | Total                                                                                                          | Total Per Player                                                                                                    |
 | -------- | -------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
 | Copper   | `VIEW[{CoinsCopper}+({CoinsSiler}*10)+({CoinsElectrum}*50)+({CoinsGold}*100)+({CoinsPlatinum}*1000)]`          | `VIEW[({CoinsCopper}+({CoinsSiler}*10)+({CoinsElectrum}*50)+({CoinsGold}*100)+({CoinsPlatinum}*1000))/{PartySize}]` | 
 | Silver   | `VIEW[(({CoinsCopper}+({CoinsSiler}*10)+({CoinsElectrum}*50)+({CoinsGold}*100)+({CoinsPlatinum}*1000))/10)]`   | `VIEW[(({CoinsCopper}+({CoinsSiler}*10)+({CoinsElectrum}*50)+({CoinsGold}*100)+({CoinsPlatinum}*1000))/10)/{PartySize}]`                                                                                                                    |
 | Electrum | `VIEW[(({CoinsCopper}+({CoinsSiler}*10)+({CoinsElectrum}*50)+({CoinsGold}*100)+({CoinsPlatinum}*1000))/50)]`   | `VIEW[(({CoinsCopper}+({CoinsSiler}*10)+({CoinsElectrum}*50)+({CoinsGold}*100)+({CoinsPlatinum}*1000))/50)/{PartySize}]`                                                                                                                    |
 | Gold     | `VIEW[(({CoinsCopper}+({CoinsSiler}*10)+({CoinsElectrum}*50)+({CoinsGold}*100)+({CoinsPlatinum}*1000))/100)]`  | `VIEW[(({CoinsCopper}+({CoinsSiler}*10)+({CoinsElectrum}*50)+({CoinsGold}*100)+({CoinsPlatinum}*1000))/100)/{PartySize}]`                                                                                                                    |
 | Platinum | `VIEW[(({CoinsCopper}+({CoinsSiler}*10)+({CoinsElectrum}*50)+({CoinsGold}*100)+({CoinsPlatinum}*1000))/1000)]` | `VIEW[(({CoinsCopper}+({CoinsSiler}*10)+({CoinsElectrum}*50)+({CoinsGold}*100)+({CoinsPlatinum}*1000))/1000)/{PartySize}]`       


```