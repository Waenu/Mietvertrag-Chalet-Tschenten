# Mietvertrag Chalet Tschenten

Eingabemaske, die aus den Vertragsdaten ein PDF erzeugt (Vorlage Version 1.8). Läuft komplett im Browser, es werden keine Daten an einen Server gesendet.

## Dateien
- `index.html` – Maske und PDF-Erzeugung
- `einstellungen.json` – Vorgaben (Rabatt, Reinigung, Zeiten) und Vertragstexte; wie beim Tschentomat direkt im Repo änderbar
- `lib/jspdf.umd.min.js` – PDF-Bibliothek jsPDF 2.5.2 (mitgeliefert, kein Internet nötig)

## Rechenregeln
- Anzahl Übernachtungen = Check-out minus Check-in
- Preis nach Rabatt = Preis × (100 − Rabatt %) / 100, auf den Rappen gerundet
- Total = Preis nach Rabatt + Reinigungsgebühr
- Zahlbar bis = Check-in minus 30 Tage (steht im PDF unter dem Zahlungshinweis). Liegt dieses Datum vor dem Ausfülltag (kurzfristige Buchung), erscheint kein Datum; es gilt dann der Vertragssatz «3 Tage nach Vertragsabschluss».

## Belegungsregeln (Vorlage 2.0)
- Drei Gruppen: Gäste ab 6 Jahren (Gästekarte und Kurtaxe), Kinder von 2½ bis 5 Jahren, Kleinkinder bis 2½ Jahre (Kinderbettchen).
- Gäste ab 6 Jahren plus Kinder von 2½ bis 5 Jahren: zusammen höchstens 6 (Erwachsenenbetten). Kleinkinder: höchstens 2, zusätzlich. Die Auswahllisten werden entsprechend begrenzt.
- Mindestens 1 Gast ab 6 Jahren. Der Mieter steht als erster Eintrag in der Gästeliste; sein Geburtsdatum ist Pflicht und wird am Check-in auf mindestens 18 Jahre geprüft.
- Die Geburtsdaten der Gästeliste werden am Check-in mit den gewählten Anzahlen verglichen; bei Abweichung erscheint eine Warnung (sperrt nicht).
- Die Werte stehen in `einstellungen.json` unter `vorgaben` (`maxPersonen`, `maxKleinkinder`, `minAlterMieter`, `grenzeGastJahre`, `grenzeKleinkindMonate`).

## Mindestaufenthalt
Mindestens 4 Nächte (`minNaechte` in `einstellungen.json`). Im Kalender sind Check-out-Tage vor dem Mindestaufenthalt gesperrt; das PDF wird bei weniger Nächten nicht erzeugt.

## Belegung aus Airbnb
- Der Kalender zeigt belegte Nächte schraffiert. Die Daten kommen aus `belegt.json` im Repository Tschentomat (wird dort alle 3 Stunden per GitHub Action aus dem Airbnb-Kalender erzeugt). Adresse: `einstellungen.json` unter `belegung.url`.
- Dieses Projekt enthält keinen Airbnb-Link und keine Secrets.
- Überschneidet sich der gewählte Zeitraum mit belegten Nächten, erscheint eine Warnung. Sie sperrt nichts, weil der Vertrag auch zu einer bereits eingetragenen eigenen Buchung gehören kann.
- Lässt sich die Belegung nicht laden, erscheint ein Hinweis, und die Maske funktioniert trotzdem.

## Dateiname
`JJJJ-MM-TT - JJJJ-MM-TT Mietvertrag Vorname Nachname.pdf`, z. B. `2027-02-18 - 2027-02-25 Mietvertrag Liselotte Freiburghaus.pdf`. Das Jahr steht immer bei beiden Daten.

## Persönliche Daten (nicht im Repo)
Vermieter-Adresse, Mail, Telefonnummern, IBAN, QR-Bild und Unterschrift werden unter «Einstellungen» einmalig eingegeben und nur im Browser des Rechners gespeichert. Mit «Einstellungen sichern» entsteht eine Datei `Mietvertrag Einstellungen PRIVAT.json` als Kopie auf dem PC (nicht ins Repo legen; `.gitignore` schliesst sie aus).

## Hinweis
Die Maske muss über http(s) geöffnet werden (GitHub Pages), nicht per Doppelklick, weil `einstellungen.json` geladen wird.
