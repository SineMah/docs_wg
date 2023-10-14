
- [ ] Asset Upload max size, mime check (Request-Klasse)
	- [ ] jpg, png, pdf 5mb
- [ ] Filtererweiterung: OR bei Attributen (Prüfung ob auch Stammdaten aufgenommen werden können)
- [ ] Offene CloneEntries per place anzeigen
+ [x] user federation für produktive partner
- [ ] ldap require bike/ce attribute?
+ [x] Scopes für unterschiedliche JWT-Typen (sso, DE|AT|NL|Default) Passport & Keycloak
+ [x] scopes, soo, roles, scopes prüfen & testen
	+ [x] scopes
	+ [x] roles
	+ [x] sso
	+ [x] pav
	+ [x] kein scope
	+ [x] key cloak token (ssh, pav, kein filter)
	+ [x] sso token (sso filter)
	+ [x] passport token (places pav/sso filter)
	+ [x] prüfen von http request klassen
	+ [x] Datenspiegelung mit sso jwt anpassen
- [ ] Route Check ob FH: Zentrale, übergeordneter FH, Aktivpartner, FH + spiegelbare attribute (PVA, whitelisting, Produktion, Logo)
+ [x] Import der neuen CSV lokal
+ [x] Places Db prod neu exportieren und einspielen lokal
+ [x] Daten von FH zu Zentrale kopieren und spiegeln
+ [x] Db auf Stage aktualisieren
+ [x] Scopes (seeder || command?) anpassen
- [x] dev & stage testen
+ [x] Abgleich der PVAs
+ [x] Config für Attribute erweitern (Helm usw , https://jira.wertgarantie.com/browse/SWDBAPI-2254?focusedId=445285&page=com.atlassian.jira.plugin.system.issuetabpanels%3Acomment-tabpanel#comment-445285)
+ [x] Batch für HTTP
- [ ] Clone HTTP testen
	+ [x] async?
+ [x] Queue für Cloning anpassen
- [ ] Nachfragen wer FHV testet
+ [x] Route Agent is head office, retailer headquarter, place uuids
- [ ] woher stammt die Datei `2022_10_14_10_00_jak.csv` ?
	- [ ] https://jira.wertgarantie.com/browse/SWDBAPI-2255
- [ ] Wer legt die FH in Keycloak an?

[[Services/Places]]