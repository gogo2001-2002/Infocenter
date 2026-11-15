# Infocenter – technische Dokumentation

## Zweck

Infocenter überwacht Variablen in IP-Symcon anhand konfigurierbarer Bedingungen. Es übernimmt Benachrichtigungswege und Regeloptionen der bestehenden Überwachung und ergänzt pro Regel den Meldungstyp **Info**, **Warnung** oder **Alarm**.

## Meldungsformat

- Erstmeldung: `Info: Meldungstext`, `Warnung: Meldungstext` oder `Alarm: Meldungstext`
- Behobenmeldung: `Behoben Info: Meldungstext`, `Behoben Warnung: Meldungstext` oder `Behoben Alarm: Meldungstext`
- Eskalation: `Eskalation N Info: Meldungstext`, `Eskalation N Warnung: Meldungstext` oder `Eskalation N Alarm: Meldungstext`

Eine Eskalation enthält ebenfalls den Meldungstyp. Für jede Regel kann unter dem Meldungstext ein eigener **Behoben-Meldungstext** angegeben werden. Ist dieses Feld leer, wird weiterhin der normale Meldungstext verwendet. Die Vorgabe gilt für Push, WebPush, E-Mail, Anruf und Echo. Die WebPush-Daten für die Visu trennen Kopfzeile und phasenabhängigen Meldungstext, damit beide in eigenen Zeilen erscheinen können.

## WebVisu

Für die Darstellung in der bestehenden WebVisu gilt: Rahmenfarbe nach Meldungstyp (Info neutral, Warnung gelb, Alarm rot), Punktfarbe nach Phase (Erstmeldung farblos, Eskalation rot, Behoben grün). Die erste Zeile enthält Phase und Meldungstyp, die zweite Zeile ausschließlich den konfigurierten Meldungstext. Die erforderliche Anpassung des WebVisu-Renderers ist in [WEBVISU-INTEGRATION.md](WEBVISU-INTEGRATION.md) beschrieben.

## Meldungstyp

Jede Bedingung enthält die Auswahl **Meldungstyp** mit den gültigen Werten Info, Warnung und Alarm. Neue Regeln und übernommene Bestandsregeln erhalten den Startwert Alarm. Ungültige oder fehlende Werte werden bei der Migration auf Alarm gesetzt.

## Benachrichtigungskanäle

Erstmeldung, Eskalation und Behobenmeldung sind getrennt für Push, WebPush, E-Mail, Anruf und Echo einstellbar. Pro Bedingung können bis zu vier Push-Visualisierungen und vier EchoRemote-Ziele genutzt werden. WebPush-Ziele werden automatisch ermittelt oder können manuell ausgewählt werden.

## Bedingungen und Laufzeit

Unterstützte Operatoren: `==`, `!=`, `>=`, `>`, `<`, `<=`, `CHANGED` und `UPDATED`. Eine Regel kann einen festen Vergleichswert oder eine Vergleichsvariable verwenden. Bei `CHANGED` und `UPDATED` wird kein Vergleichswert ausgewertet.

Verzögerung und Eskalationsintervall sind pro Regel konfigurierbar. Die Eskalationsnummer wird je Regel als Integer-Variable geführt und bei Behebung zurückgesetzt.

## Kopie der bestehenden Konfiguration

Die neue Instanz wird parallel zur vorhandenen Instanz angelegt. Globale Eigenschaften und alle vorhandenen Regeln werden mit ihren Kanaleinstellungen kopiert. Der Meldungstyp wird für jede kopierte Regel auf Alarm gesetzt. Aktivierte Bedingungen bleiben aktiv; beide Instanzen können daher parallel dieselben Benachrichtigungen auslösen.

## Installation

Repository `https://github.com/gogo2001-2002/Infocenter` in IP-Symcon unter **Module Control** hinzufügen und danach die Instanz **Infocenter** anlegen. SMTP-, TelefonansageDirekt-, EchoRemote- und Visualisierungsinstanzen müssen auf dem System vorhanden sein.
