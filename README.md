# Machine learning B3A
### Dauguen Arnaud / Hay Théo / Sella Justin

## Prérequis
* minikube
* [helm](https://helm.sh/docs/intro/install/)

## Démarrage
```
minikube start
```

## 1. Découpage en Namespace
Nous avons choisi un découpage en 4 namespace par client, 2 pour les bases de données (dev et prod) et 2 autres pour le projet (dev et prod)

Nous avons également des namespaces spécifiques à notre usage. On retrouve par exemple `monitoring`, créé durant la partie 5.

* Lancer la génération automatique des namespace
  * (remplacez `<client-name>` par le nom du nouveau client
  * /!\ Ne doit contenir que :
    * lettre miniscules [a-z]
    * '-'
    * '.'
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

## 3. Wordpress

## 4. RBAC

## 5. Monitoring
Note: namespace pour cette partie : `monitoring` ou changer le nom paragraphe 1

### **Bonus**
## 6. OIDC

## 7. Registry + GUI Web