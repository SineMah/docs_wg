Payments (Backend)
- [ ] Stabilität muss gewährleistet sein (bedenken wegen IT)
- [ ] Datenspeichern bevor erste Verarbeitung stattfindet (Webhook, AS)
	- [ ] am liebsten dokumentenbasierte Db (Mongo, CouchDb, …) um einfach wegzuspeichern oder MySQL JSON Field
	- [ ] Redis ungeeignet, flush ist zu unsicher
- [ ] [Events | Novalnet Docs](https://developer.novalnet.de/asynchronousnotification/events)
- [ ] [Redirection | Novalnet Docs](https://developer.novalnet.de/onlinepayments/redirection#step1)
- [ ] [Direct API | Novalnet Docs](https://developer.novalnet.de/onlinepayments/api)
- [ ] [Authentication - websockets 10.3 documentation](https://websockets.readthedocs.io/en/stable/topics/authentication.html)
- [ ] [Testing | Novalnet Docs](https://developer.novalnet.de/testing)
- [ ] Per Event-Type weiter pushen, abspeichern
	- [ ] BE muss fähig sein Daten an FE bspw bei Abbruch/Ausstieg zu pushen, insofern Event vorliegt
+ [x] Bekommt FE von Landing Page Daten oder muss BE immer Pushen?
- [ ] Dokumentation der Events muss für uns lückenlos sein
- [ ] Müssen wir Datensätze noch einer gewissen Zeit löschen? Betrifft nur Payment-Service
- [ ] Contracts-Erweiterung mit TID (novalnet Transaktion-ID)
- [ ] FE muss Abbrüche, Erfolgreiche Abschlüsse an BE senden
- [ ] Link für Novalnet Landing Page generieren
- [ ] Storno
- [ ] BE REST, Websockets (Node) - Kommunikation über Worker 
	- [ ] redis pub/sub oder redis listen als Queues
	+ [x] alternativ RabbitMQ/MQTT
	- [ ] für Websockets sollten wir ein eigenes “Protokoll” im Vorfeld definieren
	- [ ] Auth für Websockets
	- [ ] WSS
- [ ] eventuell Abgleich mit Novalnet CSV-Export, falls Service nicht erreichbar war (Wartung, Infrastruktur, Updates etc)
- [ ] Ich hätte auch Lust TypeSense oder OpenSearch lose einzubinden, um Daten schnell zu finden ;p

Datendurchsatz und Reaktionszeit muss passen

[[Insurance]]