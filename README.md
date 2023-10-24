# MODULE - DevOps : WIK-DPS-TP04

- [Étape 1](#étape-1)
    - [🎯 Objectifs](#-objectifs-step-1)
    - [🚶 Étapes à suivre](#-étapes-à-suivre-step-1)
    - [💻 Commandes notables](#-commandes-notables-step-1)
- [Étape 2](#étape-2)
    - [🎯 Objectifs](#-objectifs-step-2)

## Étape 1

### 🎯 Objectifs (Step 1)

```
Créer un Pod pour déployer l'image registry.cluster.wik.cloud/public/echo (c'est l'image créée lors du TP WIK-DPS-TP02) et le tester sur minikube en local
Pour le tester vous devez faire un port-forwarding entre le port du Pod sur lequel votre API écoute et un port sur votre hôte`
```

### 🚶 Étapes à suivre (Step 1)

**Étape 1 :** Créer un fichier YAML avec le contenu de notre Pod (voir fichier [step-one.yaml](./step-one.yaml))

**Étape 2 :** Appliquer les instructions qui sont données dans notre fichier avec la commande `kubectl apply -f ./step-one.yaml` (Remplacer ./step-one.yaml par le chemin vers votre fichier).

Il est possible de bien voir que notre pod a été crée avec la commande suivante :

```
PS C:\Users\lukabdx> kubectl get pods
NAME           READY   STATUS    RESTARTS   AGE
wik-dps-tp04   1/1     Running   0          52s
```

**Étape 3 :** Il faut maintenant faire du port forwarding pour pouvoir accéder à notre API grâce à la commande `kubectl port-forward pod/wik-dps-tp04 8080:80`

**Notre API est maintenant joignable sur le port 8080 (à l'adresse [http://localhost:8080/ping](http://localhost:8080/ping)) !**

### 💻 Commandes notables (Step 1)

- Création de pod : `kubectl apply -f [direction vers le fichier].yaml`
- Suppression de pod : `kubectl delete -f [direction vers le fichier].yaml`
- Pods crées : `kubectl get pods`
- Port forwarding : `kubectl port-forward pod/[nom du pod] [port machine]:[port pod]`

## Étape 2

### 🎯 Objectifs (Step 2)

```
Remplacer le Pod par un ReplicaSet afin de déployer 4 réplicas du Pod créé précédemment
```

