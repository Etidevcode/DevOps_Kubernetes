# Minikube

+ Minikube provisionne et gère des clusters Kubernetes locaux optimisés pour les
workflows de développement.

### **Configuration de Minikube pour K8**

#### **1) Configurer Minikube**
+ Ouvrez `PowerShell` en tant qu'administrateur
+ Configuration `Chocolatey`
+ Installer `Minikube` avec `Chocolatey`
   + `choco install minikube kubernetes-cli`
+ Ouvrez `PowerShell` et exécutez
   + `start minikube`

#### **2) Configuration avec Kops (Prérequis)**
+ Domaine pour les enregistrements DNS Kubernetes
   + par exemple groophy.in de `Godaddy`
+ Créer une `VM` Linux et configurer
   + kops, kubectl, clés ssh, awscli.
+ Connectez-vous au compte `AWS` et configurez
   + `seau s3`, `Utilisateur IAM` pour `AWSCli`, `Zone hébergée Route53`

### Documentation

[Installation-Minkube](Materiels/minikube/Minikube-commands.txt)
[Minikube](https://minikube.sigs.k8s.io/docs/start/?arch=%2Fwindows%2Fx86-64%2Fstable%2F.exe+download)