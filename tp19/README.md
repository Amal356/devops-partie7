# TP19 : GitOps avec Argo CD (synchronisation, self-healing, ApplicationSet, promotion)

> **Cours** : DevOps & Cloud, M. Wahid ([énoncé](https://docs.teknolabs.net/courses/devops-cloud/partie-7-gitops/tp19-gitops-argocd/))
> **Étudiante** : Amal Jemli, Master DevOps
> **Dépôt GitOps** : [github.com/Amal356/tp19-gitops](https://github.com/Amal356/tp19-gitops)
> **Objectif** : l'état désiré du cluster est déclaré dans Git ; Argo CD le compare en permanence au cluster et le réconcilie. On ne déploie plus avec `kubectl apply`, mais avec un commit ou une Pull Request.

## Sommaire
1. [Les 4 principes GitOps](#1-les-4-principes-gitops)
2. [Environnement](#2-environnement)
3. [Partie 1 : installer Argo CD](#3-partie-1--installer-argo-cd)
4. [Partie 2 : première Application](#4-partie-2--première-application)
5. [Partie 3 : synchronisation automatique, prune, self-healing, rollback](#5-partie-3--synchronisation-automatique-prune-self-healing-rollback)
6. [Partie 4 : ApplicationSet](#6-partie-4--applicationset)
7. [Partie 5 : promotion sans reconstruction](#7-partie-5--promotion-sans-reconstruction)
8. [Difficultés rencontrées](#8-difficultés-rencontrées)
9. [Sécurité](#9-sécurité)
10. [Livrables](#10-livrables)

---

## 1. Les 4 principes GitOps

| Principe (OpenGitOps) | Concrètement dans ce TP |
|---|---|
| **Déclaratif** | l'état désiré est décrit en YAML (Kustomize : `base/` + `envs/*`) |
| **Versionné et immuable** | il est stocké dans Git ([tp19-gitops](https://github.com/Amal356/tp19-gitops)) : historique complet, `git revert` possible |
| **Tiré (pull)** | Argo CD, dans le cluster, **tire** le dépôt (toutes les 3 min) : pas de port entrant, pas d'identifiants du cluster dans la CI |
| **Réconcilié en continu** | Argo CD compare Git et le cluster, et corrige les écarts (*self-heal*, *prune*) |

## 2. Environnement

| Élément | Valeur |
|---|---|
| Cluster | K3s v1.34.12+k3s1, mono-nœud sur la VM de lab (9,2 Go de RAM, disque 76 Go) |
| Argo CD | **v3.6.1**, déjà installé par **Helm** (chart `argo-cd` 10.18.0) pour un autre projet de la VM (ApplicationSet `portfolio`) : **réutilisé** pour ce TP, sans toucher aux Applications existantes |
| CLI `argocd` | v3.6.2, empreinte SHA256 vérifiée (`cli_checksums.txt` : OK) |
| Dépôt GitOps | [Amal356/tp19-gitops](https://github.com/Amal356/tp19-gitops) (public, lu par Argo CD en *pull*) |

> 🟡 TP en cours : reprise à la connexion du CLI (`port-forward` + `argocd login`), puis partie 2.

## 3. Partie 1 : installer Argo CD
> ⏳

## 4. Partie 2 : première Application
> ⏳

## 5. Partie 3 : synchronisation automatique, prune, self-healing, rollback
> ⏳

## 6. Partie 4 : ApplicationSet
> ⏳

## 7. Partie 5 : promotion sans reconstruction
> ⏳

## 8. Difficultés rencontrées

| Problème | Cause | Solution |
|---|---|---|
| `kubectl apply -n argocd --server-side -f install.yaml` : nombreux `conflict with "helm"` | Argo CD était **déjà installé par Helm** sur la VM (autre activité) ; l'apply côté serveur refuse de modifier les champs gérés par Helm | Installation existante réutilisée. `helm rollback argocd 1` ; seul `argocd-notifications-controller` (passé en v3.6.2 par l'apply) a été remis en v3.6.1 avec `kubectl set image`, car Helm ne détectait pas l'écart |
| `argocd login` : `connection refused` | `port-forward` non lancé | `kubectl -n argocd port-forward svc/argocd-server 8443:443 &`, puis vérification du log |

## 9. Sécurité
> ⏳

## 10. Livrables

| Capture | Contenu | État |
|---|---|---|
| `captures/argocd-synced.png` | Application `whoami-dev` Synced / Healthy dans l'UI | ⏳ |
| `captures/self-heal.png` | `kubectl scale` annulé par Argo CD | ⏳ |
| `captures/git-revert.png` | Application Degraded puis rétablie après `git revert` | ⏳ |
| `captures/applicationset.png` | Trois Applications générées par l'ApplicationSet | ⏳ |
| `captures/promotion-pr.png` | Pull Request de promotion vers staging | ⏳ |
| `captures/same-digest.png` | Même digest d'image en dev et en staging | ⏳ |

Dépôt GitOps avec son historique de commits : [github.com/Amal356/tp19-gitops/commits/main](https://github.com/Amal356/tp19-gitops/commits/main)
