# Infocenter

IP-Symcon-Modul zur Überwachung von Variablen und zum Versand konfigurierbarer Benachrichtigungen. Jede Regel kann einer Meldungsart zugeordnet werden: **Info**, **Warnung** oder **Alarm**.

## Funktionen

- Wertvergleiche sowie „Variable verändert“ und „Variable aktualisiert“
- Verzögerung und Eskalationsintervall pro Regel
- Push an WebFront- und Tile-Visualisierungen
- WebPush, E-Mail, TelefonansageDirekt und EchoRemote
- Erstmeldung, Eskalation und „Behoben melden“ getrennt je Kanal
- Optional eigener Meldungstext für die Behobenmeldung pro Regel (leer = normaler Meldungstext)
- Bis zu vier Push-Visualisierungen und vier EchoRemote-Instanzen pro Regel
- Vergleich mit einem festen Wert oder einer Vergleichsvariable
- Dynamische Auswahl verfügbarer Visualisierungen, Echo-Geräte und WebPush-Ziele

## Meldungstyp und Kopfzeile

Der Typ wird für jede Regel separat als **Info**, **Warnung** oder **Alarm** ausgewählt. Neue Regeln beginnen mit **Alarm**. Übernommene Bestandseinträge werden ebenfalls mit **Alarm** initialisiert.

- Erstmeldung: `Typ: Meldungstext`
- Behoben: `Behoben Typ: Meldungstext`
- Eskalation: `Eskalation 1: Meldungstext` (mit aktueller Nummer)

Für Tile-Push werden passende Symbole gesetzt: Info ohne Symbol, Warnung mit Warnsymbol, Alarm und Eskalation mit Alarmsymbol, Behoben mit Erfolgssymbol. WebFront-Push erhält den Meldungstyp im Kopftext; die WebFront-Push-API bietet keinen separaten Farbparameter.

## Installation

1. Dieses öffentliche Repository in IP-Symcon unter **Module Control** hinzufügen.
2. **Infocenter** über **Instanz hinzufügen** auswählen.
3. SMTP-, TelefonansageDirekt- und Benachrichtigungsziele konfigurieren.
4. Regeln mit Meldungstext, Typ und Überwachungsbedingung anlegen.

## Vergleichswerte

Ist eine Vergleichsvariable ausgewählt, wird ausschließlich deren aktueller Wert verwendet. Andernfalls gilt der feste Vergleichswert. Bei den Operatoren „Variable verändert“ und „Variable aktualisiert“ wird kein Vergleichswert ausgewertet.

## Eskalationen und Entwarnung

Eskalationen werden im konfigurierten Intervall erneut gesendet, solange die Regel aktiv bleibt. Die Nummer wird als `Eskalation N: Meldungstext` ausgegeben. Für Push, WebPush, E-Mail, Anruf und Echo kann „Behoben melden“ jeweils unabhängig aktiviert werden. Unter dem normalen Meldungstext kann pro Regel ein eigener Behoben-Meldungstext hinterlegt werden; bleibt er leer, wird der normale Meldungstext verwendet.

## Übernahme vorhandener Regeln

Die vorhandene Instanz bleibt unverändert. Globale Einstellungen und alle bestehenden Bedingungen werden kopiert. Aktivierte Bedingungen bleiben aktiv und können dadurch parallel auslösen.
