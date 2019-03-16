
# Fahrplan Hands On Lab (BID 2019)

### 1. Hälfte - Herantasten an Forschungsdaten (9:15 Uhr - 10:00 Uhr)
 
- Vorstellung Forschungsfrage
- Forschungsdatenmanagement mit RDMO
- Analyse Datenquellen
- rechtliche Fragestellungen

### 2. Hälfte - Arbeiten mit Forschungsdaten (10:15 Uhr - 11:00 Uhr)
- Erstellung Rohdatenset mit pyg
- Daten-Provenienz mit provit
- Datenexploration mit Kibana
- Ausblick

### 3. Abschluss (11:00 Uhr - 11:30 Uhr)
- Diskussion


---

# 1. Hälfte - Herantasten an Forschungsdaten

## Research Data Management Organiser (RDMO)

Der Research Data Management Organiser (RDMO) unterstützt Institutionen und Forschende bei der Erfassung und Pflege von Datenmanagamentplänen. Mithilfe eines Fragenkatalogs werden strukturiert Informationen u.a. zur Forschungsfrage, zu den Forschungsdaten und deren Verwendung im Forschungsprozess erfasst.

Abschnitte des RDMO Fragekatalogs:
* Allgemein
* Inhaltliche Einordnung
* Technische Einordnung
* Rechtliche und ethische Fragen
* Datennutzung
* Datenorganisation
* Metadaten und Referenzierung
* Langzeitarchivierung

Für den Workshop wurde der Fragenkatalog angepasst und gekürzt.

Weiterführende Informationen unter: https://rdmorganiser.github.io/

> **BID Programmhinweis**
> "Aktives Datenmanagement mit RDMO"
> Hands On Lab digital, Seminarraum 6/7
> 20.03.2019, 14:00 – 15:30 

## Quellenauswahl

### Quellen

Es gibt eine Vielzahl von Quellen welche die zur Beantwortung der Forschungsfrage benötigte Daten beinhalten. Nicht alle Quellen beinhalten alle benötigten Daten oder stellen diese im benötigten Umfang kostenlos zur Verfügung.

#### Twitter

* Zugang über API begrenzt
* Diskussionen (Threads) über API nicht verfügbar

#### Facebook

* Daten zu “Freunde” und Diskussionen etc. nur mit expliziter Genehmigung der jeweiligen User verfügbar
* Cambridge Analytica

#### Patreon

* Keine offizielle Daten-API (inoffizielle, interne API vorhanden)
* Geringe Datenmenge (manuelle Auswertung möglich)
* Teil der Inhalte exklusiv für “Patrons” (Förderer) verfügbar

#### YouTube

* Google Data API mit großzügigem Datenlimit
* (Meta-)Daten zu Videos, Playlists, Kommentaren
* Keine Daten zu Subscriber von den Kanälen

### API Beispiel

Eine Website besteht aus zwei wichtigen Bestandteilen, den Daten (also Inhalten) und der Präsentation. Die gleichen Daten können den NutzerInnen auf verschiedene Weisen präsentiert werden, z.B. als klassische Website und als App fürs Smartphone. 

Eine API (Advanced Programmers Interface) ist dabei die Schnittstelle zu den Daten und befindet sich gewissermaßen hinter der Präsentationsebene. Einige Internetangebote stellen auch Endnutzern Zugang zu diesen Datenschnittstellen bereit. Dies ermöglicht den einfacheren Zugriff auf die Daten, wenn man nur an den Inhalten aber nicht an der Präsentation interessiert ist, also z.B. wenn man eine Statistik über einen Youtube-Kanal erstellen möchte.

Die Metadaten der Videos von [PythonSelkanHDs](https://www.youtube.com/user/pythonselkanHD) "Latest Videos" Playlist kann man über die YouTube Data-API besorgen.

***Browser***

Es gibt nun verschiendene Varianten auf diese APIs zuzugreifen. Im einfachsten Fall nimmt man einfach einen Browser. Die folgenden Befehlen holen die Liste der Videos in der Playlist:

*Tipp: Um die komplette Zeile zu markieren dreimal schnell in das Feld klicken.*
``` 
https://www.googleapis.com/youtube/v3/playlistItems?part=snippet%2CcontentDetails&maxResults=10&playlistId=PLA565E1205E032A46&key=<YOUTUBE_API_KEY>
```

Hier sieht man nun die reine Daten-Ebene von Youtube, also ohne die Präsenationsebene (Video, Bilder, Formatierung, ...). 

***Terminal (CURL request)***

*Tipp: Zum Einfügen im Terminal entweder Strg+Umschalt(Shift)+V oder die mittlere Maustaste drücken. Alternativ kann auch im "Bearbeiten"-Menü auf "Einfügen" geklickt werden.*
```
curl -i -G -d "part=snippet%2CcontentDetails&maxResults=10&playlistId=PLA565E1205E032A46&key=<YOUTUBE_API_KEY>" https://www.googleapis.com/youtube/v3/playlistItems
````

Aus dem Ergebnis kann man die Video-IDs der zuletzt in dem Channel veröffentlichten Videos herauslesen. Damit kann man mittels des folgenden Befehls die jeweiligen Video-Metadaten holen:

***Browser***

*Hinweis: Hier muss an der Stelle <VIDEO_ID> eine video ID aus dem vorigen Request eingefügt werden*

```
https://www.googleapis.com/youtube/v3/videos?part=snippet&key=<YOUTUBE_API_KEY>&id=<VIDEO_ID>
```

***Terminal (CURL request)***

*Hinweis: Hier muss an der Stelle <VIDEO_ID> eine video ID aus dem vorigen Request eingefügt werden*

```
curl -i -G -d "part=snippet&key=<YOUTUBE_API_KEY>&id=<VIDEO_ID>" https://www.googleapis.com/youtube/v3/videos
````

## Rechtliche Fragen

### Datenschutz:

Social Media Kommentare sind "personenbezogene Daten" (DSGVO), weil sie den Rückbezug zu natürlichen Personen ermöglichen.

Was darf veröffentlicht werden?
- aggregierte Daten
- Topic Models & Sentiment Lexika keine personenbezogenen Daten

### Urheberrecht

Social Media Kommentare sind urheberrechtlich geschützte "Mikropublikationen"

- Zitation aus YT unbedenklich
- Zitation aus Forschungsdaten kontrovers
- Forschungsdatensatz ist kein eigenständiges Sprachwerk

### Weiterführende Links:

- Handreichungen:
    - https://verwaltung.uni-koeln.de/stabsstelle02.3/content/forschungsdatenschutz/index_ger.html
    - https://www.internetrecht-nuernberg.de/internetrecht/datenschutzrecht.html

- Rechtstexte:
    - https://dsgvo-gesetz.de/
    - https://www.revosax.sachsen.de/vorschrift/17647

- Forschung:
    - https://tu-dresden.de/gsw/jura/igetem/jfbimd13/forschung/forschungsprojekt-datajus

- Förderung:
    - https://www.dfg.de/foerderung/programme/nfdi/index.html


---

# 2. Hälfte - Arbeiten mit Forschungsdaten

## Erstellung des Rohdatensets mit PYG 

Das Programm [PYG](https://github.com/diggr/pyg) (Passable Youtube Grabber) ist ein Werkzeug mit welchem die Youtube-API einfach abgefragt werden kann. Dabei können z.B. alle Kommentare unter den Videos eines Youtube-Kanals heruntergeladen werden, und anschließend in verschiedene Formate exportiert werden. PYG wurde vom diggr-Team entwickelt und befindet sich noch in einem frühen Entwicklungsstand; Es können also noch sporadisch Fehlfunktionen auftreten, aber prinzipiell stehen die wichtigsten Funktionen bereits zur Verfügung.

Das Programm hat keine grafische Benutzeroberfläche, sondern lediglich ein Command Line Interface (CLI). Das ist aber selbst für weniger erfahrene NutzerInnen insofern unproblematisch, als dass sich die Konfiguration durch das Editieren von Textdateien durchführen lässt, und lediglich das Starten des Programms von der Kommandozeile aus erfolgte. 

Die Software ist auf github zu finden und für alle kostenlos herunterzuladen, zu benutzen und zu modifizieren: https://github.com/diggr/pyg.

Mit **PYG** werden wir nun  über die YouTube Data-API alle zu einem Kanal verfügbaren Daten (Videometadaten und Captions, Kommentare, und Playlists) herunterladen und Archiv im Format .ZIP abspeichern.

### Vollständige Anleitung für ein neues Projekt

*Hinweis: Im Workshop benutzen wir aus Zeitgründen ein bereits bestehendes Projekt, die notwendigen Schritte zur Erstellung eines neuen Projekts seien hier der Vollständigkeit halber erwähnt. **Wir springen also direkt zu Schritt 6.***

1. Erstelle ein Verzeichnis für das Projekt

    Kann man ganz klassisch über den Filebrowser (unter Windows: Explorer) erledigen oder über die Kommandozeile:
    ```
    $ mkdir pygproject
    ```

2. Initialisiere das Verzeichnis als PYG-Projektverzeichnis (dies erstellt YAML-Konfigurationsdateien für das Projekt)

    ```
    $ cd pygproject
    ```
    ```
    $ pyg init
    ```

3. Füge YouTube-API Key in config.yml ein

    ```
    elasticsearch:
      prefix: bid_
      url: 'http://user:pwd@localhost:9200'
    network:
      proxy: ''
    project:
      dir: data
      name: bid
    youtube:
      api-key: '<YOUR-YOUTUBE-API-KEY>'
    ```

4. Füge den *slug* des YouTube Kanals in channels.yml ein

    ```
    main:
    - 'user/pythonselkanHD'
    ```

5. Führe PYG *fetch* Befehl aus um das Datenset zu erstellen. Das Datenset wird unter `data/channels/main/<CHANNEL-TITLE>.zip` abgeleget.

    ```
    $ pyg fetch channels
    ```

**WORKSHOP-START**

6. Um später eine Update File zu holen, führe PYG *update* Befehl aus

    ```
    $ cd bid_raw_data
    ```
    ```
    $ pyg update channels
    ```

7. Daten in Kibana laden

    ```
    $ pyg elasticsearch channels
    ```

## Provit 

Um die Herkunft von Daten und deren Bearbeitung besser im Blick zu behalten, bietet es sich an ein Logbuch dafür anzulegen. Mit Hilfe des Programms [Provit](https://github.com/diggr/provit) kann dies einfach erfolgen. 

**PYG** erstellt nämlich zu jedem Datensatz bereits ein Logbuch, welches durch die NutzerInnen dann weitergenutzt werden kann, um einerseits bisher erfolgte Bearbeitungsschritte nachzuvollziehen oder neue hinzuzufügen. 

Ein Logbuch ist natürlich immer nur so gut, wie die Person die es führt. Mangelnde Konsequenz im Eintragen der Bearbeitungsschritte rächt sich, nicht sofort, aber spätestens wenn man nach 2 Monaten versucht nachzuvollziehen, wie der Datensatz, den man gerade vorliegen hat zustande kam. 

Provit bietet eine grafische Benutzeroberfläche die mit den meisten gängigen Browser zu benutzen sein sollte. Dazu muss der Provit Server in der Kommandozeile gestartet werden. 

```
$ provit browser
```

Nun kann man http://localhost:5555 aufrufen um die Benutzeroberfläche zu öffnen.

## Kibana/ElasticSearch 

[Kibana](https://www.elastic.co/products/kibana)  ist eine browserbasierte grafische Benutzeroberfläche mit der Daten welche in einem Elasticsearch gespeichert sind, angezeigt, untersucht und für die weitere Bearbeitung exportiert werden können. Kibana gehört neben Elasticsearch und Logstash zum sogenannten ELK-Stack, und ist in Datengetriebenen Umgebungen ein gern genutztes Tool, um Daten, deren Struktur, und Zusammenhänge zu untersuchen. 

1. Index einrichten

    * Klick auf "Discover" (linke Menüleiste)
    * Nun in das Eingabefeld *bid_yt_comments* als Index-Pattern eintragen
    * Klick auf "Next Step"
    * Nun "timestamp" als Time-Pattern aus wählen
    * Klick auf "Finish"
   
2. Suchen vorbereiten

    * Klick auf "Discover" (oben links)
    * Klick auf "time picker" (oben rechts) > "Relative" 
    * unter "From" "15" eingeben und Zeiteinheit "Years ago" auswählen

3. Datenexploration 1:

    * Volltextsuche: "Kojima" (*Existiert dieser Term im Korpus?*)
  
4. Datenexploration 2 -- Filter:
    * Klick: "Add a filter"
    * Filter 1 - *Videotitel mit "Kojima"*: 
        * unter "Filter" "video_title" auswählen
        * unter "Operator" "is" auswählen
        * unter "Value" "Kojima" eintragen
        * "Save" klicken
    * Filter 2 - *Kommentare mit "Kojima"*:
        * unter "Filter" "text" auswählen
        * unter "Operator" "is" auswählen
        * unter "Value" "Kojima" eintragen
        * "Save" klicken
5. Exportieren
    * Tabelle für Export zusammenstellen
        * *hover* über Features: "Add"
        * folgende Features auswählen (="Add" klicken):
           * "channel"
           * "video_title"
           * "video_id"
           * "user"
           * "user_id"
           * "text"
           * "timestamp"
        * auf "Share" klicken
        * anschließend auf "CSV Report" klicken
    * Textprompt erscheint: Klick zum Herunterladen des CSV Reports