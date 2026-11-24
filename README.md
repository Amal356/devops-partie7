# DevOps & Cloud – Partie 7 : GitOps

> **Étudiante** : Amal Jemli, Master DevOps
> **Cours** : [Teknolabs – DevOps & Cloud, M. Wahid](https://docs.teknolabs.net/courses/devops-cloud/partie-7-gitops/)
> Suite de [devops-partie5](https://github.com/Amal356/devops-partie5) et [devops-partie6](https://github.com/Amal356/devops-partie6).

Objectif de la partie : déployer depuis Git avec Argo CD puis Flux CD, et promouvoir la même version d'un environnement à l'autre.

| TP | Sujet | Dossier | Dépôt GitOps | État |
|---|---|---|---|---|
| TP19 | GitOps avec Argo CD : synchronisation, prune, self-healing, ApplicationSet, promotion | [tp19/](tp19/README.md) | [tp19-gitops](https://github.com/Amal356/tp19-gitops) | ✅ 6/6 captures (+3 complémentaires) |
| TP20 | GitOps avec Flux : bootstrap, Kustomization, HelmRelease, comparaison | tp20/ | — | ⏳ |

## Fil rouge sécurité
- Git est la **source de vérité** : chaque changement est relu (Pull Request), tracé et réversible (`git revert`).
- Modèle **pull** : l'agent GitOps tire les changements depuis GitHub ; aucun port entrant ni identifiant du cluster dans la CI.
- Branche `main` protégée (PR obligatoire, 1 approbation).
- Aucun secret dans Git (mot de passe admin Argo CD jamais affiché ni commité).
