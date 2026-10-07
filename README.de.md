<div align="center">

# AutoPin-CS

[English](README.md) · [中文](README.zh.md) · [Español](README.es.md) · Deutsch · [Français](README.fr.md)

[GitHub @frommmmmg](https://github.com/frommmmmg)

</div>

> **Dieses Repository ist ein Schaufenster, keine Quellcode-Veröffentlichung.** AutoPin-CS ist nicht quelloffen, deshalb gibt es hier keinen Code, nur was es kann, wie es gebaut ist und wie es aussieht. Wenn du darüber sprechen möchtest, melde dich über mein [GitHub-Profil](https://github.com/frommmmmg).

**Ein Planer und eine Flottenverwaltung für Social-Media-Content-Betrieb im großen Maßstab.** Ein zentraler Server verteilt Aufgaben an eine Flotte von Windows-Clients, und eine KI-Agenten-Schicht lässt Betreiber das gesamte System in normaler Sprache steuern.

Eine große Flotte unbeaufsichtigter Desktop-Clients zu betreiben ist vor allem ein Betriebsproblem. Wie spielt man eine neue Version ein, ohne die Flotte lahmzulegen? Wie nimmt man eine frische Maschine jedes Mal auf dieselbe Weise in Betrieb? Wie findet man die eine Maschine, die still ausfällt? AutoPin-CS ist das System, das um diese Fragen gebaut wurde, und der größte Teil seines Codes sorgt dafür, dass die Antworten wiederholbar, prüfbar und wiederherstellbar sind.

![Architektur](assets/autopin-architecture.svg)

| | |
|---|---|
| **Meine Rolle** | Alleiniger Entwickler und Betreuer von Server, Client, Desktop-Steuerung, Deployment-Werkzeugen und Dokumentation |
| **Status** | Im Produktivbetrieb. Ein privates kommerzielles System, daher keine öffentliche Seite |
| **Umfang** | Etwa 1.300 Python-Dateien, etwa 620 Testdateien, über 400 Architekturentscheidungen und etwa 290 Fehler-Nachbetrachtungen |
| **Technik** | Python · Flask · uWSGI · MySQL · Windows-Dienste · Browser-Automatisierung · FFmpeg |

### Was es kann

**Server**
- **Zentrale Planung und Verwaltung.** Ein Flask/uWSGI-Dienst mit MySQL verwaltet Aufgaben, Aufträge, die Client-Registrierung, Aufgaben-Logs und -Ergebnisse, Sicherungen und Auswertungen.
- **Verträge und Schema-Disziplin.** Das Schema jeder Tabelle ist versioniert und gehört einem Modul, und die Bereitschaftsprüfung hält die Planer zurück, bis die Datenbank im erwarteten Zustand ist.

**Client-Flotte**
- **Python-Daemons mit mehreren Betriebsmodi**, die Browser-Automatisierungsabläufe ausführen: ein dauerhaft laufender Worker, ein vom Server gesteuerter Einzelaufgaben-Modus und weitere Aufgabentypen.
- **Ein Desktop-Agent, der die Windows-Sitzungsisolierung durchdringt.** Er kann den echten Benutzer-Desktop sehen und steuern, sodass die Ferndiagnose Screenshots und Prozesssteuerung statt Vermutungen aus Logs umfasst.
- **Videoaufbereitung.** Ein geprüfter Stapelablauf normalisiert Videos auf ein konservatives H.264/AAC-Profil, das auch alte Windows-und-Browser-Kombinationen akzeptieren.

**Release-Technik**
- **Eine Release-Schranke, die nie nachgibt.** Jedes Client-Update wird als vollständiges Paket gebaut, inaktiv registriert, **auf einer echten Canary-Maschine verifiziert** und erst dann aktiviert, mit bereitem Rollback. Ein grüner Build, ein entpackbares Paket oder ein einzelner Heartbeat zählen nicht als Erfolg.

**Eine KI-Agenten-Schicht**
- **Betrieb als Agenten-Skills.** Eine neue Maschine in Betrieb nehmen, einen entfernten Client diagnostizieren, die Planer prüfen, auffällige Konten sichten und ein Release bauen sind als Skills geschrieben, die ein KI-Agent ausführen kann. Jeder Skill ist eine feste Schrittfolge mit Prüfschranken und Belegauslesung, gestartet durch einen Satz des Betreibers.

## Screenshots

*Screenshots fehlen absichtlich: Die Admin-Konsole zeigt Client- und Kontodaten.*

## So funktioniert es

![Ein Release wird erst aktiviert, wenn eine echte Canary-Maschine alle Schranken besteht.](assets/autopin-release-gate.svg)
*Ein Release wird erst aktiviert, wenn eine echte Canary-Maschine alle Schranken besteht.*

![Der Betreiber spricht normal; der Agent führt ein festes Runbook aus und liest die Belege zurück.](assets/autopin-agent-loop.svg)
*Der Betreiber spricht normal; der Agent führt ein festes Runbook aus und liest die Belege zurück.*

<!--notes-->
## Technische Notizen

- **Entscheidungen sind aufgeschrieben, und es sind viele.** Über 400 Architekturentscheidungen halten fest, warum die Dinge so sind, wie sie sind, viele davon zu Versionierung und Zuständigkeit von Datenbankschemata, damit Start und Migrationen vorhersehbar bleiben.
- **Fehler bekommen eine Nachbetrachtung und eine Suche nach Geschwistern.** Rund 290 Fehlerprotokolle nennen jeweils Ursache, Regressionstest und die Suche nach demselben Defekt an anderer Stelle. Ein Fehler wird erst geschlossen, wenn diese Suche erledigt ist.
- **Belege statt Hoffnung.** Ein Release gilt nur mit Nachweisen von einer echten Maschine als funktionierend: stabiler Prozessbaum, Desktop-Sitzung, gespeicherter Erfolg, kein neuerer Fehler oder Rollback. Paketprüfungen umfassen Mitgliederlisten, ZIP-Prüfsummen, Länge, SHA-256 und Kompatibilität mit dem ältesten Interpreter der Flotte.
- **Wiederherstellung wird entworfen, bevor man sie braucht.** Rollback-Wege, ein geprüfter Wiederherstellungsweg für die Canary-Maschine und ein Wiederherstellungs-Playbook mit vollständigem Installer sind aufgeschrieben, und die ursprünglichen Fehlerprotokolle bleiben erhalten, statt überschrieben zu werden.
- **Geheimnisse bleiben aus Code und Kommandozeile heraus.** Zugangsdaten liegen im Schlüsselbund des Betriebssystems und werden den Werkzeugen erst im Moment der Nutzung übergeben.
- **Agenten folgen denselben Regeln wie Menschen.** Die Agenten-Skills sind im Repository versioniert, tragen dieselben Sicherheitsregeln (den Canary nie überspringen, nicht raten, von welchem Einstiegspunkt ein Log stammt) und müssen mit der Bestätigung enden, dass die Änderung gepusht wurde.

**Weitere Projekte:** [AffProof](https://github.com/frommmmmg/AffProof-showcase) · [Tonu.app](https://github.com/frommmmmg/Tonu.app-showcase) · [AffiliateScraper](https://github.com/frommmmmg/AffiliateScraper-showcase)

---

<div align="center">

<sub>Screenshots verwenden nur Beispiel- oder öffentliche Daten. © Alle Rechte vorbehalten. Beschreibungen dürfen mit Quellenangabe zitiert werden; die Software selbst darf nicht weitergegeben werden.</sub>

</div>
