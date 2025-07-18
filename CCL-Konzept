# 🧩 CC.License (CC.L) – Matryoshka.cc Lizenzplattform

**CC.License** ist ein öffentlich zugängliches Lizenz- und API-System, entwickelt von [Matryoshka.cc](https://matryoshka.cc). Es erlaubt **Nutzern**, eigene Lizenzen zu erstellen, Keys zu generieren und via API in eigene Projekte einzubinden – kostenlos, simpel, DSGVO-konform.

> 📌 Keine klassischen Softwarelizenzen – sondern **Nutzer-generierte Lizenzsysteme** für persönliche Projekte wie Bots, Scripts, Mods, Tools oder Online-Anwendungen.

---

## 📌 Inhaltsverzeichnis

- [🧠 Konzept](#-konzept)
- [🆔 Was ist eine UIN?](#-was-ist-eine-uin)
- [🧩 Features](#-features)
- [🗂 Projektstruktur](#-projektstruktur)
- [⚙️ Setup & Installation](#️-setup--installation)
- [🧪 Beispiel: Lizenz erstellen & nutzen](#-beispiel-lizenz-erstellen--nutzen)
- [🔌 API-Schnittstellen](#-api-schnittstellen)
- [🤖 Discord-Bot-Kompatibilität](#-discord-bot-kompatibilität)
- [🛡 Sicherheit](#-sicherheit)
- [📄 Logging & Monitoring](#-logging--monitoring)
- [👥 Accounts & Rollen](#-accounts--rollen)
- [📊 Lizenz- und Keylimits](#-lizenz--und-keylimits)
- [📨 E-Mail-System](#-e-mail-system)
- [📂 DSGVO: Datenzugang & Automatisierung](#-dsgvo-datenzugang--automatisierung)
- [📊 Statistik-Dashboard](#-statistik-dashboard)
- [🌟 Nutzerfreundliche Funktionen (QoL)](#-nutzerfreundliche-funktionen-qol)
- [⚖️ Rechtliche Anforderungen](#-rechtliche-anforderungen)
- [💡 Entwickler-Tipps](#-entwickler-tipps)
- [🧱 Technologien](#-technologien)
- [📜 Lizenz](#-lizenz)
---

## 🧠 Konzept

1. Nutzer registrieren sich → erhalten eine eindeutige **UIN (UserIdentificationNode)**  
2. Sie erstellen beliebig viele **Lizenzen** (bis zu 10 pro Useraccount)
3. Innerhalb jeder Lizenz können **bis zu 25 Keys** erzeugt werden
4. Diese Keys können über eine API validiert und verwaltet werden
5. Nutzer können Keys deaktivieren, einschränken oder löschen
6. Admins können Accounts, Lizenzen und Keys zentral überwachen

---

## 🆔 Was ist eine UIN?

Die **UIN (UserIdentificationNode)** ist eine neu entwickelte Benutzer-ID, die die klassische UUID ersetzt.

**Beispiel:**
```
UIN-v7_4X2A-MTKS23-Z8K1
```

**Eigenschaften:**
- Bei Registrierung automatisch generiert
- Vollständig zufällig + Entropie + Zeitstempel
- Kollisionen werden durch Datenbankabfrage ausgeschlossen
- Bleibt dauerhaft mit dem Account verknüpft
- Wird in API-Requests und als User-Identifier verwendet

**Finden der eigenen UIN:**
- Im Dashboard sichtbar
- Automatisch per Mail bei Registrierung und Lizenzaktionen
- Per API: `GET /api/whoami` mit Token

---

## 🧩 Features

| Funktion | Beschreibung |
|---------|--------------|
| 🔐 UIN statt UUID | Eindeutige Identifikation jedes Nutzers |
| 📜 Benutzerdefinierte Lizenzen | Eigene Namen, Regeln, Keys pro Projekt |
| 🔑 Keyverwaltung | Erstellen, Löschen, Limitieren, IP-Bindung |
| 📡 REST-API | Schnittstelle zur externen Key-Prüfung |
| 🤖 Discord-kompatibel | Webhooks und Key-Check für Bots |
| 🧾 Logging | Jede Abfrage wird gespeichert (DSGVO-konform) |
| 👨‍💼 Admin-Panel | Überblick über alle Nutzer, Lizenzen und Aktionen |
| 📉 Limits | 10 Lizenzen pro User, 25 Keys je Lizenz |
| 📧 Mailsystem | Verifikation, Warnungen, Wiederherstellung |
| 📄 Rechtstexte | DSGVO, Impressum, AGB integriert |

---

## 🗂 Projektstruktur

```
📁 /public/       → HTML-Oberfläche, Tailwind-basiert
📁 /api/          → API-Routen
📁 /lib/          → Auth, Mail, Logging, DB
📁 /views/        → Templates (Dashboard, Fehler, Login)
📁 /admin/        → Admin-Oberfläche
📁 /sql/          → Setup-Dumps & Migrationen
📄 .env           → Konfig (DB, SMTP, Token)
```

---

## ⚙️ Setup & Installation

```bash
git clone https://github.com/dein-name/cc-license.git
cd cc-license
cp .env.example .env
nano .env
```

```ini
DB_HOST=localhost
DB_USER=ccuser
DB_PASS=ccpass
DB_NAME=cc_license
MAIL_FROM=info@deinedomain.de
MAIL_SMTP=smtp.deinedomain.de
SITE_URL=https://license.matryoshka.cc
SALT=SICHERER_RANDOM_SALT
```

```bash
mysql -u root -p cc_license < sql/schema.sql
```

> Webserver: Apache2 oder NGINX mit TLS empfohlen. PHP 8.2+, MySQL/MariaDB, TLS via Cloudflare möglich.

---

## 🧪 Beispiel: Lizenz erstellen & nutzen

1. Registrieren: `/register`
2. Lizenz anlegen → Name, Beschreibung
3. Key erzeugen: z.B. `XYZ-123-ALPHA`
4. API nutzen:

```http
GET /api/check?uin=UIN-v7_...&key=XYZ-123-ALPHA
```

**Response:**
```json
{
  "valid": true,
  "license": "Projekt Alpha",
  "status": "ACTIVE"
}
```

---

## 🔌 API-Schnittstellen

| Methode | Route | Beschreibung |
|--------|-------|--------------|
| `GET`  | `/api/check` | Key validieren |
| `POST` | `/api/newkey` | Key erzeugen (mit Auth) |
| `POST` | `/api/block` | Key blockieren |
| `GET`  | `/api/stats` | Lizenznutzung anzeigen |
| `GET`  | `/api/whoami` | Gibt aktuelle UIN zurück (mit Auth) |

---

## 🤖 Discord-Bot-Kompatibilität

Ja, CC.L kann verwendet werden, um z. B. Botzugriffe zu lizensieren:

- Beim Botstart wird `GET /api/check?uin=...&key=...` durchgeführt
- Antwort validiert, ob Bot starten darf
- Webhook-Nutzung möglich für Logs, Statusupdates oder Warnungen

---

## 🛡 Sicherheit

- Argon2id-Hashing für Passwörter
- Sessions mit Secure+HttpOnly+SameSite
- Brute-Force-Protection (Rate-Limit)
- IP-Analyse, HWID-Fingerprinting möglich
- CSP, X-Frame-Deny, Referrer-Policy aktivierbar
- Kein direkter Zugriff auf sensible Nutzerdaten

---

## 📄 Logging & Monitoring

Pro API-Aufruf:
- Timestamp
- Lizenz-ID
- IP
- HWID/Fingerprint
- Statuscode
- Fehlertext

Admins sehen globale Logs, Nutzer nur ihre eigenen.

---

## 👥 Accounts & Rollen

### Normale Nutzer:
- Eigene Lizenzen & Keys verwalten
- Zugriff auf API-Dashboard
- Max. 10 Lizenzen, je 25 Keys

### Admins:
- Übersicht über alle Accounts
- Lizenzen & Keys aller Nutzer einsehbar
- Accounts sperren oder reaktivieren
- Systemweite Logs & Statistiken

---

## 📊 Lizenz- und Keylimits

- Maximal **10 aktive Lizenzen** pro Benutzer
- Pro Lizenz **max. 25 aktive Keys**
- Weitere über Admin-Freischaltung möglich

---

## 📨 E-Mail-System

Verwendet SMTP aus `.env`.  
Eingesetzt für:
- Registrierung (Verifizierung)
- Wiederherstellung (Reset)
- Missbrauchsbenachrichtigungen
- Optional: Webhook-Weiterleitung

---

## 📁 DSGVO, AGB & Impressum

- DSGVO-konform, keine Dauer-IP-Logs
- E-Mail nur für technische Zwecke
- Kein externes Tracking
- Löschanfragen via `/support` möglich

---

## 💡 Entwickler-Tipps

- Für größere Projekte: Lizenzen nach Umgebung aufteilen (z. B. Dev/Test/Prod)
- Verwende UINs als festen Identifier in Webhooks oder Bot-Konfiguration
- Verwende `key_type` in API um bestimmte Keys für Events zu sperren

---

## 🧱 Technologien

- PHP 8.2+
- MySQL / MariaDB
- TailwindCSS (CDN)
- Vanilla JS
- Apache2 oder NGINX
- Cloudflare (empfohlen)

---

## 📜 Lizenz

Dieses Projekt steht unter der MIT-Lizenz.  
Siehe `LICENSE.md` für Details.

## 🧠 Warum wird die UIN in der API benötigt?

Die **UIN (UserIdentificationNode)** ist der zentrale Schlüssel zur Trennung der Datenbankinhalte pro Benutzer. Ohne UIN wäre es nicht möglich zu erkennen, **welchem Nutzer** ein Lizenzschlüssel zugeordnet ist.

Vorteile der UIN im API-Kontext:

- 🔐 Schutz vor fremden Key-Abfragen (Schlüssel allein reicht nicht!)
- 🧩 Mehrfach gleiche Keys in unterschiedlichen Lizenzen möglich, solange die UIN verschieden ist
- 🧠 Logische Isolation im Code: Kein globaler Schlüsselraum nötig
- 📈 Trennung der Nutzungsstatistiken je Nutzer

---

## 🛡 Schutz vor unautorisierten Zugriffen (SQL, API, Keys)

### 1. SQL-Absicherung (Server-seitig)
- ✅ Prepared Statements (SQL Injection unmöglich)
- ✅ Keine Root-Zugänge für Webserver-User
- ✅ MySQL-User mit minimalen Rechten:
  - `SELECT`, `INSERT`, `UPDATE`, `DELETE` nur auf CC.L-Datenbank
- ✅ Zugriff auf SQL nur lokal (`bind-address = 127.0.0.1`)
- ✅ Keine SQL-Debugmeldungen im Frontend

### 2. API-Sicherheit
- 🔑 Jeder API-Aufruf muss UIN enthalten
- 🧪 Optional: HWID / IP / User-Agent zur Abgleichprüfung
- 📦 Rate-Limit: Max. X Anfragen pro Minute
- 🕵️ Fingerprinting + User-Agent Prüfung (Bot-Abwehr)
- 🚫 API-Key rotieren/löschen bei Missbrauch
- 🔐 Nur POST bei sensiblen Endpunkten (z. B. Key-Erzeugung)

---

## 🖥 Interface (Frontend-Konzept)

### Start-Dashboard (nach Login)
- Begrüßung & Benutzerinformationen (inkl. UIN)
- Übersicht: Wie viele Lizenzen erstellt / Limit erreicht?
- Letzte API-Zugriffe & Status

### Lizenz-Übersicht
- Tabelle mit allen eigenen Lizenzen
- Für jede Lizenz:
  - Name, Beschreibung
  - Anzahl aktiver Keys (z. B. 14 / 25)
  - Button „Details“ → Key-Verwaltung

### Key-Verwaltung
- Liste mit allen Keys (pro Lizenz)
  - Status (aktiv, gesperrt, verbraucht)
  - Anzahl API-Zugriffe
  - Button „sperren“, „löschen“, „Details“

---

## 🧰 Nutzer-Settings

| Option | Beschreibung |
|--------|--------------|
| Passwort ändern | Aktuelles & neues Passwort |
| Account löschen | DSGVO-konforme Löschung mit Bestätigung |
| API-Meldungen | Aktivieren/Deaktivieren von Mails bei Key-Zugriff |
| Projektlimits | Anzeige: 10 Lizenzen, 25 Keys je Lizenz |
| E-Mail ändern | Mit Bestätigungslink |

---

## 🔒 Sichere MySQL-Konfiguration

- `skip-name-resolve` aktivieren (Performance)
- `bind-address = 127.0.0.1` → Kein externer Zugriff
- Keine anonymen Nutzer (`DELETE FROM mysql.user WHERE User=''`)
- `root` Login per Socket oder deaktivieren
- `general_log = OFF`, `slow_query_log = ON`
- Firewall (z. B. UFW): Port 3306 nur intern freigeben
- Regelmäßige Dumps mit Verschlüsselung

---

## 🌐 Absicherung der API-Endpunkte

- Nur JSON akzeptieren (`Content-Type: application/json`)
- CSRF für alle mutierenden Aufrufe
- UIN + Lizenz + Key + optional Fingerprint prüfen
- Keine `GET`-Requests für kritische Endpunkte
- Response-Timing normalisieren (Timing-Angriffe verhindern)
- Alle Logs verschlüsselt speichern (optional)

---

Diese zusätzlichen Inhalte helfen dir, sowohl das API-System als auch das Backend gegen typische Angriffe abzusichern und nutzerfreundlich zu halten.

---

## 🧽 Datenschutz- & DSGVO-Automatisierung

### 📬 Benutzerlöschung (Self-Service)
Jeder Benutzer kann sein Konto jederzeit eigenständig löschen:

- In den „Settings“: Button **„Konto und alle Daten löschen“**
- Sicherheitsabfrage + Mail-Bestätigung erforderlich
- Es werden **alle**:
  - Lizenzen
  - Keys
  - Logs
  - Accountdaten
  gelöscht (nicht recoverbar!)

### 🗃 Speicherung & Ordnerstruktur für Logs
Alle API- und Zugriff-Logs werden **außerhalb der Webroot** gespeichert, z. B.:

```
/var/log/cclogs/USER-UIN/YYYY-MM-DD.log
```

- Nur durch Admin einsehbar
- Pro UIN ein Unterordner
- Pro Tag eine Datei (max. 24h)
- Rotationssystem: Ältere Logs nach 30 Tagen gelöscht (cronjob)

### 🔄 Automatisiertes DSGVO-System

| Feature | Beschreibung |
|--------|--------------|
| 📥 Datenauskunft | Per Klick in den Einstellungen oder via Mailanforderung (`/privacy/export`) |
| ⌛ Datenlöschung | Nach 365 Tagen Inaktivität wird Nutzer per Mail gewarnt – danach Auto-Löschung |
| 🧾 Exportformat | JSON-basiert, inklusive Lizenzen, Keys, Zugriffe, Metadaten |
| 🔐 Verschlüsselung | Exporte werden mit AES256 verschlüsselt und für 48h bereitgestellt |
| 🔒 Zugriffskontrolle | Nur der jeweilige Nutzer kann seine Daten exportieren |

---

## 🎨 Interface Design (UX/UI)

Das Interface ist **schlicht, modern, zugänglich** – designed mit TailwindCSS (CDN) und bewusst ohne JS-Frameworks.

### 🔝 Layout-Aufteilung

```
+---------------------------------------+
|              Header (Navbar)          |
| [Logo] | Dashboard | Lizenzen | Logs  |
+---------------------------------------+

+------------------+  +----------------+
| Seitenleiste     |  | Hauptinhalt    |
| - Home           |  | (dynamisch)    |
| - Einstellungen  |  |                |
| - Support        |  |                |
+------------------+  +----------------+

+---------------------------------------+
| Footer: Impressum · Datenschutz · AGB |
+---------------------------------------+
```

### 🎛 Komponentenübersicht

| Komponente         | Funktion |
|--------------------|----------|
| ⚙️ `DashboardCard` | Zeigt Gesamtstatus: #Lizenzen, #Keys, #Anfragen |
| 📊 `LicenseTable`  | Tabelle aller Lizenzen mit Progressbar (Limitanzeige) |
| 🔑 `KeyList`       | Detailansicht mit Verwaltung pro Lizenz |
| 📄 `LogsPanel`     | Zeigt letzte API-Zugriffe (Time, IP, Key) |
| 👤 `UserSettings`  | Passwort, Mail, DSGVO, Export, Löschen |

### 📱 Responsive Verhalten

- Ab <768px → Seitenleiste verschwindet, Hamburger-Menu erscheint
- Alle Tabellen sind scrollbar
- Modal-Fenster für Aktionen (z. B. Key löschen, Lizenz deaktivieren)

---

## 🔧 Empfohlene zusätzliche Funktionen

### 1. 🔔 API-Webhooks für externe Benachrichtigung

Optional können Nutzer Webhooks definieren für:
- Neue Zugriffe auf einen Key
- Blockierungen durch Limitierungen
- Fehlversuche

Payload ist JSON-basiert, sicher signiert mit HMAC.

### 2. 📈 Admin-Dashboard

Für Serverbetreiber:
- Übersicht über Anzahl Nutzer, Lizenzen, tägliche Anfragen
- Missbrauchsmuster erkennen (z. B. Key-Sharing, IP-Rotation)
- Manuelle Sperrung von Accounts, Keys oder IPs

### 3. 🔄 UIN-Rotation (WIP)

Optional: Nutzer können nach vollständiger Datenlöschung eine neue UIN beantragen, wenn sie erneut beitreten möchten.

---

## 📌 Zusammenfassung

> Dieses System ist ein vollständiges, datenschutzfreundliches Lizenzsystem mit Nutzerverwaltung, Key-Prüfung, API-Sicherheit und klarer Trennung zwischen Nutzern.  
Es ist erweiterbar, transparent und bereit für Integration in moderne Tools wie Bots, Webservices, Software oder Projekte.

---

## 📊 Erweiterung: DSGVO-Einblicke & Nutzer-Statistiken

### 📂 DSGVO: Transparente Echtzeitdaten

CC.L implementiert eine **aktive DSGVO-Datenansicht** für jeden Nutzer – direkt im Webinterface:

| Bereich | Beschreibung |
|--------|--------------|
| 👤 Accountdaten | Anzeige von gespeicherter E-Mail, Registrierungsdatum, UIN |
| 🗂 Lizenzen & Keys | Übersicht über alle erstellten Lizenzen, alle Schlüssel & Status |
| 📜 API-Aktivitäten | Letzte 30 API-Abfragen mit IP, Lizenz-ID, Erfolg/Fehlercode |
| 🔒 Datenschutz | Vollständige Darstellung aller gespeicherten Daten – exportierbar |
| 📤 Datenexport | Live-Vorschau + Button zum verschlüsselten JSON-Export |

### 🧮 Nutzer-Statistik-Dashboard

Nutzer erhalten unter dem Menüpunkt **„Statistiken“** eine vollständige Übersicht über ihre Nutzung:

| Kategorie | Beispielinhalt |
|----------|----------------|
| 📅 Zeitbasiert | Anzahl Anfragen pro Tag/Woche/Monat |
| 🔐 Lizenzen | Welche Lizenzen wurden wie oft geprüft |
| 🌍 Geografie (optional) | Länder/IP-Ranges, aus denen Keys genutzt wurden |
| ❌ Fehler | Anzahl geblockter/abgelaufener Keys |
| 📈 Verlauf | Entwicklung der Key-Nutzung im Zeitverlauf |
| ⚠️ Missbrauch | Übersicht über Blockierungen & Limits pro Key |

Optional können Statistiken im CSV- oder PNG-Format exportiert werden.

### 🧠 Warum ist das sinnvoll?

- Erfüllt nicht nur die **gesetzliche Auskunftspflicht** nach DSGVO Art. 15 ff., sondern **bietet Mehrwert**
- Hilft Nutzern, eigene Keys zu analysieren, Missbrauch zu erkennen
- Visualisiert Projektaktivität – besonders für SaaS- oder Discord-Integrationen

---

## 🧭 Empfehlungen für Erweiterungen (optional)

- 📅 **Tägliche Mail-Zusammenfassung**: Optional aktivierbar – z. B. Anzahl Zugriffe, Sperrversuche, neue Keys
- 📘 **ChangeLog System**: Internes Änderungsprotokoll je Lizenz/Key
- 🔔 **Warnlevel-Schwellen**: Bei zu vielen Zugriffen auf einen Key wird Nutzer automatisch informiert
- 📍 **Regionale Nutzungsmuster erkennen**: (z. B. Proxy-Verdacht, Bot-Aktivität)

---

---

## 🛑 Hinweis zu GeoIP & Cloudflare

Da CC.License über **Cloudflare als Reverse Proxy** betrieben wird, sind die vom Webserver erfassten IPs **nicht die echten Besucher-IPs**, sondern die Cloudflare-IPs. GeoIP-basierte Features (z. B. Länderzuordnung) sind daher **nicht zuverlässig**.

> Lösung: X-Forwarded-For Header auswerten, ABER nur mit IP-Whitelist oder lokalem Auth-Check auf echte Cloudflare-IPs.

---

## 🧑‍💼 Admins: Unbegrenzte Ressourcen

Accounts mit Admin-Flag erhalten:

- ❎ Kein Limit auf Lizenzen oder Keys
- 📂 Zugriff auf alle Nutzer-Logs, Lizenz- & Keydaten
- 🔧 Zugriff auf Nutzer-Sperrfunktion, Statistiken, Abuse-Meldungen
- 🔒 Zugriff auf Datenexporte anderer Nutzer (z. B. bei DSGVO-Anfragen)
- 🔁 Möglichkeit, Lizenzen und Keys anderer Nutzer temporär zu übernehmen (zu Debugzwecken)

---

## 🌟 Quality-of-Life (QoL) Funktionen für Nutzer

| Feature | Beschreibung |
|--------|--------------|
| 🔁 Schnell-Key-Klonen | Ein bestehender Key kann 1:1 kopiert & neu erzeugt werden |
| ⏳ API-Nutzungslimits anzeigen | In der Dashboard-Topbar sehen Nutzer, wie viele API-Calls noch verfügbar sind |
| 🎨 Light/Dark Mode | Interface passt sich System oder Nutzerwahl an |
| 📑 Lizenzbeschreibungen mit Markdown | Nutzer können bei Lizenzbeschreibung Markdown verwenden |
| 📬 Kontaktformular (Support) | Einfache DSGVO-konforme Supportanfrage direkt im Interface |
| 🔃 Auto-Refresh auf Logs | Live-Update der API-Zugriffslogs im Log-Panel |
| 🔍 Key-Suchfunktion | Schnelles Auffinden eines Keys über Filterbar |
| 📁 Backup-Funktion | Exporte der eigenen Daten auf Wunsch regelmäßig automatisch senden

---

## ⚖️ Rechtliche Grundlagen: AGB, DSGVO, Impressum

### 📃 Sind AGB notwendig?

Für **privat betriebene, nicht-kommerzielle** Dienste wie CC.L ist **keine Pflicht für AGB** gegeben – es sei denn:

- Monetarisierung (z. B. Spenden mit Gegenleistung)
- Pflichtregistrierung + rechtliche Bindung
- Haftungsausschluss gewünscht

**Empfehlung:** Eine freiwillige AGB-Seite kann dennoch erstellt werden für:

- Ausschluss der Haftung bei Missbrauch
- Definition von Pflichten (kein Abuse, keine Bots, etc.)
- Kündigungsregelung

**Pflichtbestandteile in AGB (wenn genutzt):**
- Betreibername und Kontakt
- Zweck des Systems
- Nutzungsvoraussetzungen (z. B. keine illegalen Inhalte)
- Rechte & Pflichten des Nutzers
- Regeln zur Sperrung und Löschung
- Hinweis auf DSGVO & Datenschutz

---

### 🔐 DSGVO – Was MUSS rein?

| Abschnitt | Inhalt |
|----------|--------|
| Verantwortlicher | Dein vollständiger Name + Kontaktadresse (Mail reicht für private Nutzung) |
| Erhobene Daten | UIN, E-Mail, Lizenzen, Keys, Zugriffsdaten, IP (Cloudflare-gefiltert) |
| Zweck der Erhebung | Systemnutzung, Sicherheit, Logging, Missbrauchsschutz |
| Rechtsgrundlage | Einwilligung bei Registrierung (Art. 6 Abs. 1 lit. a DSGVO) |
| Löschfristen | Sofort bei Nutzerlöschung, auto nach Inaktivität (z. B. 365 Tage) |
| Auskunftsrecht | Jeder Nutzer kann Daten exportieren & löschen lassen |
| Weitergabe | Keine Weitergabe an Dritte |
| Auftragsverarbeiter | Cloudflare, ggf. dein Hostinganbieter (mit Sitz benennen) |

---

### 🧾 Impressum – was ist Pflicht?

Für private Projekte mit Registrierung und Interaktion ist ein Impressum **notwendig**, auch ohne Monetarisierung.

**Pflichtangaben:**
- Vollständiger Name
- Anschrift (bei privatem Projekt genügt oft Stadt + Mailadresse)
- E-Mail-Kontakt
- Haftungshinweis: Keine Verantwortung für Inhalte Dritter
- Hinweis auf Datenschutzseite
- Ggf. Urheberrechtshinweise (z. B. für Tailwind, FontAwesome)

---

## 📌 Zusammenfassung: Was muss in die rechtlichen Seiten?

| Seite | Muss enthalten |
|------|----------------|
| `Impressum` | Betreibername, Ort, Mail, Haftung, Verweise |
| `Datenschutz` | Datenarten, Speicherfristen, Empfänger, Rechte |
| `AGB` (optional) | Nutzung, Pflichten, Sperrgründe, Kündigung, Haftungsausschluss |

---

---

## 🎨 TailwindCSS – Einbindung und Nutzung im Projekt

CC.License verwendet **TailwindCSS** für das vollständige Webinterface – für ein modernes, responsives und leicht wartbares Design.

### 🧾 Warum Tailwind?

- Utility-first CSS → schnelleres Prototyping
- Kein eigenes CSS nötig – alles über Klassen
- Perfekt für strukturierte Panels, Tabellen und Dashboards
- Kompatibel mit Dark/Light Mode, Mobile-First Design
- Einbindung ohne Build-Toolchain per CDN

---

### ⚙️ Einbindung in HTML (CDN)

Am besten bindest du Tailwind über das offizielle CDN direkt im `<head>` deiner HTML-Dateien ein:

```html
<!DOCTYPE html>
<html lang="de">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>CC.License</title>
    <script src="https://cdn.tailwindcss.com"></script>
  </head>
  <body class="bg-gray-900 text-white">
    <!-- Content here -->
  </body>
</html>
```

> 💡 Hinweis: Die CDN-Version enthält **alle Klassen** und ist ideal für schnelle Entwicklung ohne Buildsystem.

---

### 🧩 Wichtige Tailwind-Klassen im CC.L Interface

| Element | Klassen-Beispiel |
|--------|------------------|
| Buttons | `bg-blue-600 hover:bg-blue-700 text-white py-2 px-4 rounded-xl` |
| Karten/Boxes | `bg-gray-800 p-4 rounded-2xl shadow-md` |
| Tabellen | `table-auto w-full text-left text-sm` |
| Eingabefelder | `bg-gray-700 p-2 rounded-md w-full` |
| Status-Badges | `inline-block px-2 py-1 rounded text-xs font-semibold` |
| Navigation | `flex items-center justify-between py-4 px-6 bg-gray-900` |

---

### 🌓 Dark Mode Support

Tailwind unterstützt Dark Mode nativ. Beispiel:

```html
<div class="bg-white text-black dark:bg-gray-900 dark:text-white">
  Lizenzbereich
</div>
```

Mit `darkMode: 'media'` oder `darkMode: 'class'` (im Tailwind-Konfig) kannst du bei eigener Build-Chain noch mehr kontrollieren.

---

### 🧠 Tipps zur Nutzung im Projekt

- Benutze `flex`, `grid`, `space-x-*` und `gap-*` für Layouts statt Margin-Hacks
- Arbeite mit `rounded-2xl`, `shadow-lg`, `backdrop-blur` für modernen Look
- Responsive-Klassen: `sm:`, `md:`, `lg:` z. B. `md:text-lg lg:text-xl`
- Farbschema: Vermeide rein schwarze Hintergründe (`#000`) – lieber `gray-800/900`
- Icons kannst du via [FontAwesome CDN](https://cdnjs.com/libraries/font-awesome) oder Heroicons verwenden

---

### 🛠 Optional: Eigene Styles per @layer

Falls du irgendwann doch eigene Komponenten definieren willst:

```css
@layer components {
  .btn-primary {
    @apply bg-blue-600 hover:bg-blue-700 text-white px-4 py-2 rounded;
  }
}
```

---

## 📦 Was du brauchst, um loszulegen

- Tailwind via `<script src="https://cdn.tailwindcss.com"></script>`
- Optional: `<script>tailwind.config = { theme: { extend: {} } }</script>`
- HTML-Dateien mit klassischer Struktur (`div`, `section`, `form`, etc.)
- Keine eigene CSS-Datei notwendig (es sei denn für Custom Components)

---
