# Projet de Patching Sécurité avec Vagrant et Ansible

Ce dépôt contient la configuration Vagrant pour créer l'environnement de machines virtuelles nécessaire au projet.

## Configuration Vagrant (par Personne 2)

Ce `Vagrantfile` configure un ensemble de machines virtuelles Ubuntu 22.04 LTS pour les tests.

### Machine(s) virtuelle(s) configurée(s) :

* **server01**
    * **OS :** Ubuntu 22.04 LTS (Jammy Jellyfish)
    * **Adresse IP privée :** 192.168.56.11
    * **Ressources :** 1 CPU, 1 Go RAM
* **server02**
    * **OS :** Ubuntu 22.04 LTS (Jammy Jellyfish)
    * **Adresse IP privée :** 192.168.56.12
    * **Ressources :** 1 CPU, 1 Go RAM
* **server03**
    * **OS :** Ubuntu 22.04 LTS (Jammy Jellyfish)
    * **Adresse IP privée :** 192.168.56.13
    * **Ressources :** 1 CPU, 1 Go RAM

### Comment démarrer l'environnement :

1.  Assurez-vous d'avoir [VirtualBox](https://www.virtualbox.org/wiki/Downloads) et [Vagrant](https://www.vagrantup.com/downloads) installés sur votre machine hôte.
2.  Naviguez dans le dossier `patch_project_vagrant` via votre terminal (PowerShell, CMD, Bash, etc.).
3.  Exécutez la commande suivante pour démarrer les machines virtuelles :
    ```bash
    vagrant up
    ```
    (La première fois pour une box, le téléchargement peut prendre du temps.)
4.  Pour vous connecter en SSH à une VM spécifique (remplacez X par 1, 2 ou 3) :
    ```bash
    vagrant ssh server0X
    ```
5.  Pour arrêter toutes les VMs :
    ```bash
    vagrant halt
    ```
6.  Pour détruire (supprimer) toutes les VMs de VirtualBox :
    ```bash
    vagrant destroy -f
    ```

---

## État du Projet (Jour 2 - Avancement actuel)

### Tâches accomplies par Personne 2 :

* **Environnement Vagrant Multi-VMs :** Le `Vagrantfile` est configuré pour 3 machines virtuelles (`server01`, `server02`, `server03`). Toutes les VMs ont été créées et la connectivité SSH a été testée avec succès. L'environnement est prêt pour les déploiements Ansible.
* **Robustesse de l'environnement :** Des cycles de `vagrant destroy -f` et `vagrant up` ont été effectués pour s'assurer de la reproductibilité et de la stabilité de l'environnement.
* **Monitoring (Node Exporter) :** `node_exporter` est automatiquement installé et configuré sur chaque machine virtuelle (`server01`, `server02`, `server03`) via le provisionnement Vagrant, écoutant sur le port 9100. Un répertoire `/var/lib/node_exporter/textfile_collector` est également créé pour les métriques personnalisées (supposant l'option B de Grafana).

### Informations pour la Collaboration (à l'attention de Personne 1 - Spécialiste Ansible) :

* Les adresses IP des VMs sont :
    * `server01`: `192.168.56.11`
    * `server02`: `192.168.56.12`
    * `server03`: `192.168.56.13`
* Les informations d'accès SSH pour Ansible peuvent être obtenues via `vagrant ssh-config server0X` (où X est 1, 2 ou 3) pour chaque machine virtuelle.

### Prochaines étapes et responsabilités continues pour Personne 2 :

* **Support & Stabilité Environnement :** Être disponible pour le support et le débogage de l'environnement (redémarrage/recréation des VMs, problèmes de connectivité) pendant les tests des playbooks Ansible par Personne 1.
* **Finalisation Documentation Vagrant :** Continuer à affiner et à enrichir ce `README.md` ou d'autres documents liés à la configuration Vagrant.
* **(Optionnel/Bonus) Exploration Inventaire Dynamique :** Si le temps le permet, explorer la possibilité de générer un inventaire Ansible dynamique à partir de Vagrant.