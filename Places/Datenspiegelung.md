# Wie Debuggen?
```
Wissenschaftliches Arbeiten beschreibt ein methodisch-systematisches Vorgehen, bei dem die Ergebnisse der Arbeit für jeden objektiv nachvollziehbar oder wiederholbar sind.
```
[Wikipedia](https://de.wikipedia.org/wiki/Wissenschaftliche_Arbeit#Wissenschaftliches_Arbeiten)

-> Reproduzierbarkeit

# Wie erreichen wir Reproduzierbarkeit?
* Vor dem Test Status-Quo (Ist-Zustand) sichern (Datenbankexport)
* Test-Case, Test-Scope festlegen und niederschreiben
	* Fachhändler
	* Attribute
	* Vorgehensweise dokumentieren (evtl. Screenrecord), HTTP-Payloads, usw ...
* Daten spiegeln
* Datenbankexport
* Daten in einem System überprüfen, die die Daten nicht verändern (nicht FHV)
	* GraphQL: Place
	* Datenbank
	* Admin-Oberfläche
* Ist Soll-Zustand erreicht?
	* Wenn nein, Delta feststellen; Überprüfen, ob keine gewünschten Nebeneffekte Spiegelung verhinderten
	* Wenn ja, neuen Soll-Zustand als Ist-Zustand festlegen -> ggfs Test-Case, Test-Scope festlegen
* Ergebnis dokumentieren

Zum optimalem Vergleich den alten Ist-Zustand lokal in MySQL importieren und beide Datenbankiterationen vergleichen.