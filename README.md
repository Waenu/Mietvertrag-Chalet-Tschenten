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

## Dateiname
`JJJJ_MM_TT-MM_TT Mietvertrag Vorname Nachname.pdf`, z. B. `2027_02_18-02_25 Mietvertrag Liselotte Freiburghaus.pdf`.
Bei Jahreswechsel mit Jahr beim Austritt: `2027_12_28-2028_01_03 …`.

## Persönliche Daten (nicht im Repo)
Vermieter-Adresse, Mail, Telefonnummern, IBAN, QR-Bild und Unterschrift werden unter «Einstellungen» einmalig eingegeben und nur im Browser des Rechners gespeichert. Mit «Einstellungen sichern» entsteht eine Datei `Mietvertrag Einstellungen PRIVAT.json` als Kopie auf dem PC (nicht ins Repo legen; `.gitignore` schliesst sie aus).

## Hinweis
Die Maske muss über http(s) geöffnet werden (GitHub Pages), nicht per Doppelklick, weil `einstellungen.json` geladen wird.
