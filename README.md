# Projet de Patching Sécurité avec Vagrant et Ansible

Ce dépôt contient la configuration Vagrant pour créer l'environnement de machines virtuelles nécessaire au projet.

## Configuration Vagrant (par Personne 2)

Ce `Vagrantfile` configure une machine virtuelle Ubuntu 22.04 LTS pour les tests.

### Machine(s) virtuelle(s) configurée(s) :

* **server01**
    * **OS :** Ubuntu 22.04 LTS (Jammy Jellyfish)
    * **Adresse IP privée :** 192.168.56.11
    * **Ressources :** 1 CPU, 1 Go RAM

### Comment démarrer l'environnement :

1.  Assurez-vous d'avoir [VirtualBox](https://www.virtualbox.org/wiki/Downloads) et [Vagrant](https://www.vagrantup.com/downloads) installés sur votre machine hôte.
2.  Naviguez dans le dossier `patch_project_vagrant` via votre terminal (PowerShell, CMD, Bash, etc.).
3.  Exécutez la commande suivante pour démarrer la machine virtuelle :
    ```bash
    vagrant up
    ```
    (La première fois, la box sera téléchargée.)
4.  Pour vous connecter en SSH à la VM :
    ```bash
    vagrant ssh server01 # ou simplement vagrant ssh si c'est la seule VM
    ```
5.  Pour arrêter la VM :
    ```bash
    vagrant halt
    ```
6.  Pour détruire (supprimer) la VM :
    ```bash
    vagrant destroy -f
    ```

---

## État du Projet (Jour 1)

* **Environnement Vagrant :** La machine virtuelle `server01` est définie et a été testée avec succès. Elle est prête pour le déploiement Ansible.
* **Collaboration pour Personne 1 :** L'adresse IP de `server01` est `192.168.56.11`.
  Les informations d'accès SSH pour Ansible peuvent être obtenues via `vagrant ssh-config server01` (nécessaire pour l'inventaire Ansible).
* **Prochaine étape :** Mise en place d'une configuration multi-VMs.
