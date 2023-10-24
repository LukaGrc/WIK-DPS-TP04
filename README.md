# MODULE - DevOps : WIK-DPS-TP04

- [Étape 1 : Pod](#étape-1--pod)
    - [🎯 Objectifs](#-objectifs-step-1)
    - [🚶 Étapes à suivre](#-étapes-à-suivre-step-1)
    - [💻 Commandes notables](#-commandes-notables-step-1)
- [Étape 2 : ReplicaSet](#étape-2--replicaset)
    - [🎯 Objectifs](#-objectifs-step-2)
    - [🚶 Étapes à suivre](#-étapes-à-suivre-step-2)
    - [💻 Commandes notables](#-commandes-notables-step-2)
- [Étape 3 : Deployment](#étape-3--deployment)
    - [🎯 Objectifs](#-objectifs-step-3)
    - [🚶 Étapes à suivre](#-étapes-à-suivre-step-3)
- [Étape 4 : Service](#étape-4--service)
    - [🎯 Objectifs](#-objectifs-step-4)
    - [🚶 Étapes à suivre](#-étapes-à-suivre-step-4)
    - [💻 Commandes notables](#-commandes-notables-step-4)

## Étape 1 : Pod

### 🎯 Objectifs (Step 1)

```
Créer un Pod pour déployer l'image registry.cluster.wik.cloud/public/echo (c'est l'image créée lors du TP WIK-DPS-TP02) et le tester sur minikube en local
Pour le tester vous devez faire un port-forwarding entre le port du Pod sur lequel votre API écoute et un port sur votre hôte`
```

### 🚶 Étapes à suivre (Step 1)

**Étape 1 :** Créer un fichier YAML avec le contenu de notre Pod (voir fichier [step-1.yaml](./step-1.yaml))

**Étape 2 :** Appliquer les instructions qui sont données dans notre fichier avec la commande `kubectl apply -f ./step-1.yaml` (Remplacer ./step-1.yaml par le chemin vers votre fichier).

Il est possible de bien voir que notre pod a été crée avec la commande suivante :

```
PS C:\Users\lukabdx> kubectl get pods
NAME           READY   STATUS    RESTARTS   AGE
wik-dps-tp04   1/1     Running   0          52s
```

**Étape 3 :** Il faut maintenant faire du port forwarding pour pouvoir accéder à notre API grâce à la commande `kubectl port-forward pod/wik-dps-tp04 8080:80`

**Notre API est maintenant joignable sur le port 8080 (à l'adresse [http://localhost:8080/ping](http://localhost:8080/ping)) !**

### 💻 Commandes notables (Step 1)

- Création d'objets (Pods/ReplicaSet/...) : `kubectl apply -f [direction vers le fichier].yaml`
- Suppression d'objets (Pods/ReplicaSet/...) : `kubectl delete -f [direction vers le fichier].yaml`
- Pods crées : `kubectl get pods`
- Port forwarding : `kubectl port-forward pod/[nom du pod] [port machine]:[port pod]`

## Étape 2 : ReplicaSet

### 🎯 Objectifs (Step 2)

```
Remplacer le Pod par un ReplicaSet afin de déployer 4 réplicas du Pod créé précédemment
```

### 🚶 Étapes à suivre (Step 2)

**Étape 1 :** Créer un fichier YAML avec le contenu de notre ReplicaSet (voir fichier [step-2.yaml](./step-2.yaml))

**Étape 2 :** Appliquer les instructions qui sont données dans notre fichier avec la commande `kubectl apply -f ./step-2.yaml` (Remplacer ./step-2.yaml par le chemin vers votre fichier).

Il est possible de bien voir que notre ReplicaSet et nos Pods a été crée avec la commande suivante :

```sh
# ReplicaSet
PS C:\Users\lukab\Desktop\YNOV\B3\DevOps\WIK-DPS-TP04> kubectl get rs
NAME             DESIRED   CURRENT   READY   AGE
wik-dps-tp04-2   4         4         4       38s

# Pods
PS C:\Users\lukab\Desktop\YNOV\B3\DevOps\WIK-DPS-TP04> kubectl get pods
NAME                   READY   STATUS    RESTARTS   AGE
wik-dps-tp04-2-2dj6v   1/1     Running   0          52s
wik-dps-tp04-2-7h2gw   1/1     Running   0          52s
wik-dps-tp04-2-bvxmr   1/1     Running   0          52s
wik-dps-tp04-2-rz66t   1/1     Running   0          52s
```

*Il n'est pas possible de faire du port forwarding sur un ReplicaSet, il nous faut un service (étape 4) !*

### 💻 Commandes notables (Step 2)

- ReplicaSet crées : `kubectl get rs`

## Étape 3 : Deployment

### 🎯 Objectifs (Step 3)

```
Remplacer le ReplicaSet par un Deployment afin de pouvoir définir une stratégie d'update en RollingUpdate (50% en maxUnavailable)
```

### 🚶 Étapes à suivre (Step 3)

Les étapes à suivres sont les mêmes que pour le ReplicaSet, l'objectif d'un Deployment est d'assurer une continuité de service, mais a le même fonctionnement que les ReplicaSet (voir fichier [step-3.yaml](./step-3.yaml))

## Étape 4 : Service

### 🎯 Objectifs (Step 4)

```
Créer un Service pour pouvoir communiquer avec les Pod du ReplicaSet créé précédemment

Pour le tester vous devez faire un port-forwarding entre le port du Service sur lequel votre API écoute et un port sur votre hôte
```

### 🚶 Étapes à suivre (Step 4)

**Étape 1 :** Créer un fichier YAML avec le contenu de notre Service (voir fichier [step-4.yaml](./step-4yaml))

**Étape 2 :** Appliquer les instructions qui sont données dans nos fichiers (de deployment et de service) avec les commandes suivantes :
- Deployment :  `kubectl apply -f ./step-3.yaml` (Remplacer ./step-3.yaml par le chemin vers votre fichier).
- Service :  `kubectl apply -f ./step-4.yaml` (Remplacer ./step-4.yaml par le chemin vers votre fichier).

**Étape 3 :** Il faut maintenant faire du port forwarding pour pouvoir accéder à notre API grâce à la commande `kubectl port-forward service/wik-dps-tp04 8080:8080`

**Notre API est maintenant joignable sur le port 8080 (à l'adresse [http://localhost:8080/ping](http://localhost:8080/ping)) !**

### 💻 Commandes notables (Step 4)

- Port forwarding (avec un service) : `kubectl port-forward service/[nom du pod] [port machine]:[port pod]`