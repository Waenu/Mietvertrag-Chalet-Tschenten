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

## Belegungsregeln (Vorlage 1.9)
- Mindestens 1 Erwachsener (ab 18 Jahren). Der Mieter steht als erster Eintrag in der Gästeliste, sein Geburtsdatum ist Pflicht und wird am Check-in auf mindestens 18 Jahre geprüft.
- Erwachsene + Kinder und Jugendliche von 6 bis 17 Jahren + Kinder von 4 bis 5 Jahren: zusammen höchstens 6 (Erwachsenenbetten). Die Auswahllisten werden entsprechend begrenzt.
- Kleinkinder bis 3 Jahre: höchstens 2, zusätzlich zu den 6.
- Die Werte stehen in `einstellungen.json` unter `vorgaben` (`maxPersonen`, `maxKleinkinder`, `minAlterMieter`).

## Dateiname
`JJJJ-MM-TT - JJJJ-MM-TT Mietvertrag Vorname Nachname.pdf`, z. B. `2027-02-18 - 2027-02-25 Mietvertrag Liselotte Freiburghaus.pdf`. Das Jahr steht immer bei beiden Daten.

## Persönliche Daten (nicht im Repo)
Vermieter-Adresse, Mail, Telefonnummern, IBAN, QR-Bild und Unterschrift werden unter «Einstellungen» einmalig eingegeben und nur im Browser des Rechners gespeichert. Mit «Einstellungen sichern» entsteht eine Datei `Mietvertrag Einstellungen PRIVAT.json` als Kopie auf dem PC (nicht ins Repo legen; `.gitignore` schliesst sie aus).

## Hinweis
Die Maske muss über http(s) geöffnet werden (GitHub Pages), nicht per Doppelklick, weil `einstellungen.json` geladen wird.
