<div align="center">

# AutoPin-CS

[English](README.md) · [中文](README.zh.md) · [Español](README.es.md) · [Deutsch](README.de.md) · Français

</div>

> **Ce dépôt est une vitrine, pas une publication de code source.** AutoPin-CS est un projet privé : il n'y a donc pas de code ici, seulement ce qu'il fait, comment il est construit et à quoi il ressemble. Pour en discuter, contactez-moi via mon [profil GitHub](https://github.com/frommmmmg).

**Un planificateur et gestionnaire de flotte pour l'exploitation de contenu sur les réseaux sociaux à grande échelle.** Un serveur central distribue le travail à une flotte de clients Windows, et une couche d'agents IA permet à un opérateur de piloter tout le système en langage courant.

![Architecture d'AutoPin-CS](assets/autopin-architecture.svg)

**Points forts**

- **Planification et administration centrales.** Un service Flask/uWSGI adossé à MySQL gère les tâches, les clients, les commandes et les statistiques.
- **Une flotte de clients à base de démons Python** qui exécutent des flux d'automatisation du navigateur, avec plusieurs modes de fonctionnement selon le type de tâche.
- **Des mises en production sûres.** Chaque mise à jour client est construite en paquet complet, enregistrée, **vérifiée sur une vraie machine canari** puis seulement activée, avec retour arrière prêt. Le déploiement général sans canari est interdit par conception.
- **L'exploitation sous forme de compétences d'agent.** Mettre en service une nouvelle machine, diagnostiquer un client distant, contrôler les planificateurs et préparer une version sont écrits comme des compétences qu'un agent IA exécute sur une instruction d'une ligne.
- **Une discipline d'ingénierie écrite.** ADR, contrats système, guides d'exploitation et un processus de suivi des bogues qui cherche les défauts jumeaux avant de clore.
- **Une échelle réelle.** Des milliers de fichiers entre serveur, client, contrôle du bureau, déploiement et tests.

**Technologies :** Python · Flask · uWSGI · MySQL · services Windows · automatisation du navigateur de type Playwright · FFmpeg

## Captures d'écran

*Pas de captures d'écran, volontairement : la console d'administration affiche des données de clients et de comptes.*

## Comment ça marche

![Une version n'est activée qu'après qu'une vraie machine canari a franchi tous les contrôles.](assets/autopin-release-gate.svg)
*Une version n'est activée qu'après qu'une vraie machine canari a franchi tous les contrôles.*

![L'opérateur parle simplement ; l'agent exécute un guide fixe et relit les preuves.](assets/autopin-agent-loop.svg)
*L'opérateur parle simplement ; l'agent exécute un guide fixe et relit les preuves.*

---

<div align="center">

<sub>Les captures n'utilisent que des données d'exemple ou publiques. © Tous droits réservés. Les descriptions peuvent être citées avec attribution ; le logiciel lui-même ne peut pas être redistribué.</sub>

</div>
