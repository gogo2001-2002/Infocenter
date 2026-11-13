# Infocenter – technische Dokumentation

## Zweck

Infocenter überwacht Variablen in IP-Symcon anhand konfigurierbarer Bedingungen. Es übernimmt Benachrichtigungswege und Regeloptionen der bestehenden Überwachung und ergänzt pro Regel den Meldungstyp **Info**, **Warnung** oder **Alarm**.

## Meldungsformat

- Erstmeldung: `Info: Meldungstext`, `Warnung: Meldungstext` oder `Alarm: Meldungstext`
- Behobenmeldung: `Behoben Info: Meldungstext`, `Behoben Warnung: Meldungstext` oder `Behoben Alarm: Meldungstext`
- Eskalation: `Eskalation N: Meldungstext`

Eine Eskalation wird immer mit rotem Alarmsymbol dargestellt. Eine Behobenmeldung erhält ein Erfolgssymbol. Für Info wird kein Statussymbol gesetzt; Warnung erhält ein Warnsymbol. Die Push-APIs von WebFront und Tile bieten keinen direkten Farbwert; WebFront erhält den Typ im Kopftext und Tile zusätzlich ein semantisches Symbol.

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
