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

# Commands
## MySQL-Export
```bash
cd /tmp
mysqldump -uuser_name -p db_name > 20231012.places_0.sql
tar czvf 20231012.places_0.tgz 20231012.places_0.sql
```

## MySQL-Import (lokal)
```bash
scp stage-1:/tmp/20231012.places_0.tgz ~/Downloads
tar xzvf 20231012.places_0.tgz
mysql -uroot -p < 20231012.places_0.sql
```

# Test-Queries
## GraphQL (Quelle MySQL)
```
{
  place(
    filter: {
      uuid: "91c550eb-7a73-40c1-b58a-272fc1cf6d47"
    }
  ) {
    uuid
    name
    distance
    attributes {
      path
      value {
        radius
        device_class_group
        device_class
        is_available
        service
      }
    }
  }
}

```

## GraphQL (Quelle Opensearch)
```
{
  places(
    filter: {
      uuid: "91c550eb-7a73-40c1-b58a-272fc1cf6d47"
    }, 
    options: {
      pagination: {size: 25 offset: 0}
    })
  
  {
    uuid
    attributes{
	  uuid
      path
      value {
        opening_hours {
          periods {
            open {
              day
              time
            }
            close {
              day
              time
            }
          }
        }
        code
        amount
        uuid
        name
        name_list {
          language
          name
        }
        device_class_group
        service
        is_available
      }
    }
  }
}
```

## MySQL
```sql
select attribute_places.*
from attribute_places ap
inner join places p on p.id = ap.place_id
inner join agents a on a.id = p.agent_id
where a.wg_agent_number = 11114
```