# WebVisu-Integration

Die WebPush-Ausgabe des Infocenters liefert Kopfzeile und Meldungstext getrennt:

- `message.title`: `Info`, `Warnung`, `Alarm`, `Eskalation N Warnung` oder `Behoben Alarm`
- erste Zeile von `message.body`: ausschließlich der in der Bedingung konfigurierte Meldungstext
- `message.alarmState`: `initial`, `escalation` oder `resolved`

Der bestehende Renderer der WebVisu liest bislang vor allem `message.text` und zeichnet für Erstmeldungen einen gelben Punkt. Er muss die Anzeige für Infocenter-Einträge wie folgt aufbauen:

1. Kopfzeile aus `message.title` anzeigen.
2. Erste Zeile aus `message.body` direkt darunter als Meldungstext anzeigen.
3. Den Typ aus dem Ende von `message.title` lesen: `Info`, `Warnung` oder `Alarm`.
4. Den Rahmen neutral für Info, gelb für Warnung und rot für Alarm setzen.
5. Den Punkt anhand von `message.alarmState` färben: farblos für `initial`, rot für `escalation`, grün für `resolved`.

Als Erkennung neuer Infocenter-Kopfzeilen kann der Renderer diesen Ausdruck verwenden:

```js
const isInfocenterHeader = /^(?:(?:Eskalation\s+\d+|Behoben)\s+)?(?:Info|Warnung|Alarm)$/u.test(String(message.title || '').trim());
const typeMatch = String(message.title || '').trim().match(/(?:^|\s)(Info|Warnung|Alarm)$/u);
const messageType = typeMatch ? typeMatch[1] : '';
const messageLine = String(message.body || '').split(/\r?\n/, 1)[0].trim();
const borderClass = messageType === 'Warnung' ? 'border-amber-500'
  : messageType === 'Alarm' ? 'border-rose-600'
  : 'border-cardborder';
const dotStyle = message.alarmState === 'escalation' ? 'background-color:#ad3945;border-color:#92303a;'
  : message.alarmState === 'resolved' ? 'background-color:#32836f;border-color:#286e5d;'
  : 'background-color:transparent;border-color:transparent;';
```

Nur wenn `isInfocenterHeader` wahr ist, werden die getrennten Felder für die zwei sichtbaren Zeilen benutzt. Für andere WebPush-Nachrichten kann die bisherige Darstellung erhalten bleiben. Den Titel nicht aus `message.text` ableiten: Der WebPush-Helper ergänzt dort weiterhin Betreff und Detailzeilen.

## Zuständigkeit

Der Renderer liegt in der bestehenden Dashboard-WebHook-Datei (Symcon-Skript 58558), nicht im Infocenter-Modul. Diese Datei ist nicht Bestandteil dieses Repositorys. Die Moduländerung stellt die passenden Daten bereit; für die tatsächliche Rahmen- und Punktdarstellung muss die Renderfunktion separat aktualisiert werden.
