# Kubernetes B3A
### Dauguen Arnaud / Hay Théo / Sella Justin

## Prérequis
* minikube
* [helm](https://helm.sh/docs/intro/install/)
* kubedb
    ```
    helm repo add appscode https://charts.appscode.com/stable/
    helm repo update
    helm search repo appscode/kubedb
    helm install kubedb-operator appscode/kubedb --version 0.9.0 --namespace kube-system

    helm install kubedb-catalog appscode/kubedb-catalog --version 0.9.0 --namespace kube-system
    ```

## Démarrage
* on va supprimer l'ancienne VM et en créer une nouvelle avec plus de CPU de de mémoire que celle de base
```
minikube delete
minikube start --cpus 4 --memory 8192
```

## 1. Découpage en Namespace
Nous avons choisi un découpage en 4 namespace par client, 2 pour les bases de données (dev et prod) et 2 autres pour le projet (dev et prod)
* Les namespaces client1-app-dev et client1-app-prod contiendront l'application du client
* Les namespaces client1-bdd-dev et client1-bdd-prod contiendront uniquement les bases de données

Nous avons également des namespaces spécifiques à notre usage. On retrouve par exemple `monitoring`, créé durant la partie 5.

* Lancer la génération automatique des namespace
  * (remplacez `<client-name>` par le nom du nouveau client
  * /!\ Ne doit contenir que :
    * des lettre miniscules [a-z]
    * des '-'
    * des '.'
  * doit commencer et terminer par une lettre miniscule [a-z]
  ```
  helm install --generate-name ./namespace --set projectName=<client-name>
  ```
* Lister les nameSpaces maintenant créés
    ```
    kubectl get namespace
    ```
* Lister les resourceQuotas inclus dans les nameSpaces (/!\ listera tout les resourcesQuotas existants /!\ )
    ```
    kubectl get resourcequotas -A
    ```

## 2. KubeDB
*Fichiers de configuration dans ./namespace/templates*

## 3. Wordpress

## 4. RBAC (Role Based Access Control)
```
minikube start --extra-config=apiserver.Authorization.Mode=RBAC
```
Cette commande est censé démarrer un cluster en mode RBAC

Rôles prévus :
* Administrateur de cluster
  * Acces à tous les namespace administratifs
  * Acces aux namespaces clients en lecture uniquement
* Sysops (chez le client)
  * Acces à tous les namespaces du client
* Developpeur (chez le client)
  * Acces à tous les namespaces du client
* Client
  * Acces aux namespaces prod du client, en lecture uniquement



## 5. Monitoring
Note: namespace pour cette partie : `monitoring` ou changer le nom paragraphe 1

### **Bonus**
## 6. OIDC

## 7. Registry + GUI Web