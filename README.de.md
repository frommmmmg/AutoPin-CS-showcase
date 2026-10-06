<div align="center">

# AutoPin-CS

[English](README.md) · [中文](README.zh.md) · [Español](README.es.md) · Deutsch · [Français](README.fr.md)

</div>

> **Dieses Repository ist ein Schaufenster, keine Quellcode-Veröffentlichung.** AutoPin-CS ist ein privates Projekt, deshalb gibt es hier keinen Code, nur was es kann, wie es gebaut ist und wie es aussieht. Wenn du darüber sprechen möchtest, melde dich über mein [GitHub-Profil](https://github.com/frommmmmg).

**Ein Planer und eine Flottenverwaltung für Social-Media-Content-Betrieb im großen Maßstab.** Ein zentraler Server verteilt Aufgaben an eine Flotte von Windows-Clients, und eine KI-Agenten-Schicht lässt Betreiber das gesamte System in normaler Sprache steuern.

![AutoPin-CS-Architektur](assets/autopin-architecture.svg)

**Highlights**

- **Zentrale Planung und Verwaltung.** Ein Flask/uWSGI-Dienst mit MySQL verwaltet Aufgaben, Clients, Aufträge und Auswertungen.
- **Eine Client-Flotte aus Python-Daemons**, die Browser-Automatisierungsabläufe ausführen, mit mehreren Betriebsmodi je nach Aufgabentyp.
- **Sichere Releases.** Jedes Client-Update wird als vollständiges Paket gebaut, registriert, **auf einer echten Canary-Maschine verifiziert** und erst dann aktiviert, mit bereitem Rollback. Ein vollständiger Rollout ohne Canary ist konstruktionsbedingt verboten.
- **Betrieb als Agenten-Skills.** Eine neue Maschine in Betrieb nehmen, einen entfernten Client diagnostizieren, die Planer prüfen und ein Release bauen sind als Skills geschrieben, die ein KI-Agent mit einer einzeiligen Anweisung ausführen kann.
- **Schriftlich festgehaltene Ingenieursdisziplin.** ADRs, Systemverträge, Runbooks und ein Fehlerprozess, der vor dem Schließen nach Geschwisterdefekten sucht.
- **Umfang.** Tausende Dateien aus Server-, Client-, Desktop-Steuerungs-, Deployment- und Testcode.

**Technik:** Python · Flask · uWSGI · MySQL · Windows-Dienste · Playwright-artige Browser-Automatisierung · FFmpeg

## Screenshots

*Screenshots fehlen absichtlich: Die Admin-Konsole zeigt Client- und Kontodaten.*

## So funktioniert es

![Ein Release wird erst aktiviert, wenn eine echte Canary-Maschine alle Schranken besteht.](assets/autopin-release-gate.svg)
*Ein Release wird erst aktiviert, wenn eine echte Canary-Maschine alle Schranken besteht.*

![Der Betreiber spricht normal; der Agent führt ein festes Runbook aus und liest die Belege zurück.](assets/autopin-agent-loop.svg)
*Der Betreiber spricht normal; der Agent führt ein festes Runbook aus und liest die Belege zurück.*

---

<div align="center">

<sub>Screenshots verwenden nur Beispiel- oder öffentliche Daten. © Alle Rechte vorbehalten. Beschreibungen dürfen mit Quellenangabe zitiert werden; die Software selbst darf nicht weitergegeben werden.</sub>

</div>
