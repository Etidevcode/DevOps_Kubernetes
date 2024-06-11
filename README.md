## **Kubernetes**

|PLAN|
|-----------|
|Présentation|
|Configuration de Minikube pour K8|
|Kops pour la configuration des K8|
|Objets et documentation|
|Configuration Kube|
|Espace de noms|
|Pods|
|Différents niveaux de journalisation|
|Service|
|Ensemble de répliques|
|Déploiement|
|Commandement et arguments|
|Volumes|
|Carte de configuration|
|Secret|
|Entrée|
|Kubectl CLI et Cheasheet|
|Suppléments|
|Lens|


# Présentation

#### **1) Introduction**
+ Kubernetes : exécuter des conteneurs pour la production
+ Noeud exécutant Docker.
+ Clustering: Le noeud maitre donnera des instructions aux noeuds docker sur les conteneurs à executer. Il va distribuer des conteneurs sur vos noeuds docker.
+ En cas de defaillance de l'un des noeuds docker, vous pourriez executer des conteneurs sur les moteurs Docker en direct.
+ L'orchestration des conteneurs  est le fait de disposer d'un côté un noeud maitre que l'on appelle orchestrateur et d'un autre côté un cluster de noeuds docker ou noeuds de travail où l'orchestrateur distribuera le conteneur.

#### **2) Orchestration Tools**

+ Docker Swarm
+ Kubernetes
+ Mesosphere marathon
+ AWS ECS & EKS
+ Azure Container Service
+ Google Container Engine
+ CoreOS Fleet
+ OpenShift

#### **3) Historique de Kubernetes**
+ Créé par `Google` pour gérer leurs conteneurs `AKA Borg`
+ `Mi-2014` : Google a présenté Kubernetes comme une version open source de Borg
+ `21 juillet 2015` : [Kubernetes v1.0](#) est publié. [Avec la publication](#), Google s'est associé à Linux Formation pour former la [Cloud Native Computing Foundation (CNCF)](#)
+ `2016` : Kubernetes se généralise !
     + Kops, Minikube, Kubeadm, etc.
     + 29 septembre : [Pokemon GO ! Publication de l'étude de cas Kubernetes !](#)

+ `2017` : Adoption par les entreprises
     + Google et IBM annoncent [Istio](#)
     + Github fonctionne sur Kubernetes
     + [Oracle rejoint](#) la Cloud Native Computing Foundation

#### **4) Fournit Kubernetes**
+ Découverte de service et équilibrage de charge
+ Orchestration du stockage
+ Déploiements et restaurations automatisés
+ Emballage automatique des bacs
+ Auto-guérison
+ Gestion des secrets et de la configuration

  + https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/

#### **5) Kubernetes Architecture**

+ Il existe donc de nombreux services en jeu qui donnent l'architecture Kubernetes complète ou le cluster.

+ Deux composants principaux, le nœud maître et le nœud travailleur. Les nœuds de travail sont ceux où le moteur docker est en cours d'exécution. Le nœud maître est celui qui gère ces nœuds de travail.

+ Vous ne vous connectez même pas au nœud maître. Vous vous connectez en utilisant un client. Vous donnez des informations au nœud maître qui lance tellement de conteneurs. Et ça va prendre l'action en fonction de l'exigence.

+ Vous avez donc dans le nœud maître qui est aussi appelé plan de contrôle. Le nœud maître est également appelé plan de contrôle.

+ Vous avez un service ici, un service de serveur API, deuxième l' ordonnanceur, troisième le gestionnaire de contrôleur, quatrième etc. Ce sont quatre services de base. Ensuite, vous pouvez ajouter quelques services supplémentaires. Il y a aussi des add-ons. Mais ce sont quatre services principaux dans le maître Kubernetes ou le plan de contrôle. Le nœud de travail aura un proxy, kublet, le moteur docker. Ces trois services importants s'exécutent sur le nœud de travail.

#### **6) Maître : Serveur d'API Kube**
+ Héros principal ! Gère toutes les demandes et permet la communication entre les services de la pile.
+ Composant sur le maître qui expose l'API Kubernets.
+ C'est le frontal du plan de contrôle Kubernetes.
+ Les administrateurs s'y connectent à l'aide de `Kubectl CLI`
+ Le tableau de bord Web peut être intégré à cette API.
+ et bien d'autres intégrations...

#### **7) Maître : serveur ETCD**
+ Stocke toutes les informations
+ Magasin de valeur clé cohérent et hautement disponible utilisé comme magasin de sauvegarde kubernetes pour toutes les données du cluster.
+ Les magasins d'API Kube y récupèrent.
+ Doit être sauvegardé régulièrement.
+ Stocke l'état actuel de tout dans le cluster.

#### **8) Maître : planificateur Kube**
+ Surveille les pods nouvellement créés auxquels aucun nœud n'est attribué et sélectionne un nœud sur lequel ils doivent s'exécuter
+ Les facteurs pris en compte pour les décisions de planification incluent
   + besoins en ressources individuelles et collectives
   + contraintes matérielles/logicielles/politiques,
   + spécifications d'affinité et d'anti-affinité
   + localité des données
   + interférences inter-charges et délais

#### **9) Maître : Gestionnaire de contrôleurs**
+ Logiquement, chaque contrôleur est un processus séparé,
+ Pour réduire la complexité, ils sont tous compilés en un seul binaire et exécutés en un seul processus.

+ Ces contrôleurs incluent :
   + `Node Controller` : Responsable de remarquer et de répondre lorsque les nœuds tombent en panne.
   + `Replication Controller` : responsable du maintien du nombre correct de pods pour chaque objet contrôleur de réplication dans le système.
   + `Endpoints Controller` : remplit l'objet Endpoints (c'est-à-dire, rejoint les services et les pods).
   + `Service Account & Token Controllers` : créez des comptes par défaut et des jetons d'accès à l'API pour le nouvel espace de noms.

#### **10) Composants de nœud**
+ `Kubelet`
   + Un agent qui s'exécute sur chacun dans le cluster. Il s'assure que les conteneurs s'exécutent dans un pod.

+ `Proxy Kube`
   + Proxy réseau qui s'exécute sur chaque nœud de votre cluster.
   + Règle de réseau
     + les règles autorisent la communication réseau avec vos pods à l'intérieur ou à l'extérieur de votre cluster.

+ `Container Runtime` : kubernetes prend en charge plusieurs runtime de conteneur
   + Docker
   + conteneur
   + cri-o, rktlet
   + Kubernetes CRI (interface d'exécution de conteneur)

#### **11) Addons**
+ DNS
+ Web UI
+ Container Ressource Monitoring
+ Cluster Level Logging


#### **12) Outils de configuration de Kubernetes**
+ Difficile : configuration manuelle
+ `Minikube` :
   + Un cluster Kubernetes Node sur votre ordinateur
+ `Kubeadm` :
   + Cluster Kuberenetes multi-nœuds
   + Peut être créé sur n'importe quelle plate-forme vm, ec2, machines physiques, etc.
+ `Kops` :
   + Cluster Kubernetes multi-nœuds sur AWS.

