# LLB-LoRa Mesh v6.0

## User Story

Als Entwickler, Betreiber oder Nutzer eines robusten Funk-Mesh-Netzes möchte ich ein LoRa-basiertes System verwenden, das ohne zentrale Instanz funktioniert, damit Geräte auch unter schwierigen Bedingungen direkt miteinander kommunizieren, Daten weiterleiten und Sessions aufbauen können, ohne von Gateways, festen Rollen oder einer ständig verfügbaren Infrastruktur abhängig zu sein.

Ich möchte, dass jeder Peer grundsätzlich gleichwertig ist und nur über klar definierte Fähigkeiten verfügt, statt über starre Hierarchien. Das Netz soll kleine, physikalisch realistische Funkframes verwenden, große Nachrichten sauber fragmentieren und pro Hop adaptiv entscheiden, wie viel Zuverlässigkeit wirklich nötig ist. Dadurch soll das System ressourcenschonend, nachvollziehbar und real auf ESP32-S3- und SX1262-basierter Hardware umsetzbar sein.

Ich möchte außerdem, dass Sicherheit nicht „irgendwie“ passiert, sondern strikt definiert ist: Ende-zu-Ende geschützte Nutzdaten, klare Trennung zwischen veränderbaren Forwarding-Feldern und geschütztem Inner Payload, Replay-Schutz, Session-Frische und eine lokale Vertrauenswurzel. Kritische Root- oder Admin-Änderungen dürfen niemals über LoRa ausgelöst werden, sondern nur lokal über physisch kontrollierte Wege wie USB oder eine lokale CLI.

## Kurzbeschreibung

LLB-LoRa Mesh v6.0 ist ein deterministisches, roleless Peer-to-Peer-Mesh-Protokoll für kleine LoRa-Geräte. Es ersetzt ältere, widersprüchliche Ansätze mit Rollenmodellen, Monolith-Frames und implizitem Verhalten durch eine klar strukturierte Architektur mit logischen Schichten für Radio, MAC, Routing, Session, Reassembly, PhoneBook und Local Admin.

Der Fokus liegt auf realistisch umsetzbarer Funkkommunikation: kein On-Air-Frame darf größer als 255 Bytes sein, große Nutzdaten müssen fragmentiert werden, kleine Control-Frames bleiben kompakt, und Zuverlässigkeit wird hop-lokal über Link-Profile angepasst. Das Protokoll kennt keine Pflichtrollen wie Gateway oder Router-Master; stattdessen gibt es Capability-Flags wie Relay, Store-and-Forward, BLE-Config oder USB-Admin.

## Ziel des Projekts

Dieses Projekt soll eine sauber implementierbare Grundlage schaffen für:

- dezentrale LoRa-Mesh-Kommunikation ohne zentrale Koordination
- sichere Ende-zu-Ende-Datenübertragung mit klarer Outer/Inner-Trennung
- deterministische Routing-, Session- und Retry-Entscheidungen
- lokale Administration mit strenger Sicherheitsgrenze
- testbare Firmware mit Golden Vectors, Parser-Checks und klaren Modulgrenzen. 

## Warum dieses Projekt existiert

Viele Mesh-Ideen scheitern daran, dass sie zu viel versprechen und zu wenig auf Funkrealität achten. LLB v6.0 soll genau das vermeiden: keine magischen Annahmen, keine übergroßen Frames, keine unsauberen Sicherheitsgrenzen, keine impliziten Sonderrollen. Stattdessen setzt das Design auf Determinismus, kleine Frames, eindeutige Regeln und lokal kontrollierte Vertrauensanker.

## Nutzen für den Anwender

Der Anwender erhält ein Mesh-System, das:

- ohne zentrale Instanz arbeiten kann
- auch mit mehreren Hops strukturiert und nachvollziehbar bleibt
- Daten Ende-zu-Ende schützt
- kritische Admin-Funktionen niemals unkontrolliert über Funk freigibt
- auf Embedded-Hardware realistisch implementierbar ist
- durch klare Tests und Golden Vectors reproduzierbar entwickelt werden kann.

## Technische Leitidee

LLB v6.0 trennt strikt zwischen:

- **Outer Header** für Routing, Hop-Verhalten und mutable Weiterleitungsinformationen
- **Inner Payload** für stabile, Ende-zu-Ende geschützte Inhalte

Dadurch dürfen Weiterleiter notwendige Felder wie Hop-Zähler, Route-Hinweise oder Link-Profile ändern, ohne die eigentliche Ende-zu-Ende-Sicherheit zu brechen. Genau diese Trennung ist eine der zentralen Designregeln des Systems.

## Sicherheitsversprechen

LLB v6.0 basiert auf folgenden Sicherheitsannahmen:

- lokale Vertrauenswurzel
- keine Root-Änderung über Funk
- Session-Frische und Replay-Schutz
- klare Trennung von mutable und immutable Feldern
- selektive Offenlegung bei PhoneBook-Sync
- keine stillen Root-Operationen über BLE.

## Entwicklungsziel

Die Spezifikation ist so gedacht, dass sie direkt durch Codex oder Firmware-Entwicklung umgesetzt werden kann. Die empfohlene Struktur trennt Radio, MAC, Routing, Session, Security, Framing, Reassembly, PhoneBook, CLI und BLE. Ergänzt wird das Ganze durch deterministische Golden Vectors und Integrationstests, damit Verhalten nicht geraten, sondern reproduzierbar geprüft wird.

## Fazit

LLB-LoRa Mesh v6.0 ist die Grundlage für ein ehrliches, sicheres und deterministisches Funk-Mesh. Es ist kein LoRaWAN-Klon, kein zentral verwaltetes TDMA-System und kein monolithischer Funkblock, sondern ein praktisches Embedded-Protokoll für direkte Peer-to-Peer-Kommunikation mit klaren Grenzen und klarer Architektur.
