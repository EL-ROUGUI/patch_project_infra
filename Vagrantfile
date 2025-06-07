# -*- mode: ruby -*-
# vi: set ft=ruby :

# Configuration pour Vagrant. La version "2" est la plus courante.
Vagrant.configure("2") do |config|

  # Définit la "box" Vagrant à utiliser.
  # "ubuntu/jammy64" correspond à Ubuntu 22.04 LTS.
  config.vm.box = "ubuntu/jammy64"

  # Configure le nom d'hôte de la machine virtuelle.
  # Ce nom sera visible à l'intérieur de la VM (ex: dans le prompt du terminal).
  config.vm.hostname = "server01"

  # Configure un réseau privé pour la communication entre votre machine physique (l'hôte) et la VM (le client).
  # L'adresse IP "192.168.56.11" sera l'adresse IP statique de votre VM sur ce réseau privé.
  # Cela permet une communication stable et isolée sans interférer avec votre réseau domestique/entreprise.
  config.vm.network "private_network", ip: "192.168.56.11"

  # Configuration spécifique au fournisseur de virtualisation, ici VirtualBox.
  # Cela permet de personnaliser les ressources matérielles allouées à la VM.
  config.vm.provider "virtualbox" do |vb|
    # Alloue 1024 MB (soit 1 Go) de mémoire RAM à la VM.
    vb.memory = "1024"
    # Alloue 1 cœur de processeur (CPU) à la VM.
    vb.cpus = "1"
    # Optionnel: Pour afficher l'interface graphique de VirtualBox au démarrage de la VM, vous pouvez décommenter la ligne ci-dessous.
    # vb.gui = true
  end

end