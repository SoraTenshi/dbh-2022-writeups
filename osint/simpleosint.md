# simpleosint

Diese challenge war relativ interessant (meiner Meinung nach).
In der "Beschreibung" der challenge findet man `XaenoMorph63` welches mich im Glauben gelassen hat, dass es sich hierbei um einen nickname handelt.

So hab ich nun also erstmal meine Suchmaschine der Wahl angeworfen um nach dem Namen zu suchen.

Der erste Treffer ist ein Github link, welchen ich folgte.
3 Repositories, wovon 2 forks sind.
So hab ich also `my-first-project` inspiziert, ein einfaches Python script, welches eine mail mail mit den dort konfigurierten werden schickt:

```json
{
    "to": "xaenomorph63@gmail.com",
    "subject": "W1R-MOEG3N-K34S",
    "content": "einmal den schluessel zum mitnehmen bitte. nicht im menu"
}
```
Also:
Absender: `xaenomorph63@gmail.com`
Betreff: `W1R-MOEG3N-K34S`
und mit dem E-Mail body: `einmal den schluessel zum mitnehmen bitte. nicht im menu`

Nun hab ich das also ebenfalls gemacht, die E-Mail genau so geschrieben und abgeschickt.
Anschliessend wirkte das Format auf mich sehr nach base64, so hab ich also versucht den inhalt zu dekodieren.
Das war erfolgreich und da war dann auch schon meine Flagge: `DBH{d5287d25-b421-4240-aea8-b8aabbc9deba}`
