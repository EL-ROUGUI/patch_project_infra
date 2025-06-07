# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  (1..3).each do |i|
    config.vm.define "server0#{i}" do |server|
      server.vm.box = "ubuntu/jammy64"
      server.vm.hostname = "server0#{i}"
      server.vm.network "private_network", ip: "192.168.56.1#{i}"

      server.vm.provider "virtualbox" do |vb|
        vb.memory = "1024"
        vb.cpus = "1"
      end

      # --- DEBUT DE LA NOUVELLE SECTION POUR PROVISIONNEMENT ---
      # Provisionnement pour installer Node Exporter (si Personne 3 utilise Prometheus)
      server.vm.provision "shell", inline: <<-SHELL
        # Mise à jour des paquets et installation des dépendances
        sudo apt update -y
        sudo apt install -y curl

        # Télécharger Node Exporter (vérifier la dernière version sur GitHub releases)
        # Remplacez la version si une plus récente est disponible sur https://github.com/prometheus/node_exporter/releases
        NODE_EXPORTER_VERSION="1.8.1" # ou la dernière version stable
        wget https://github.com/prometheus/node_exporter/releases/download/v${NODE_EXPORTER_VERSION}/node_exporter-${NODE_EXPORTER_VERSION}.linux-amd64.tar.gz -O /tmp/node_exporter.tar.gz

        # Décompresser l'archive
        tar -xvf /tmp/node_exporter.tar.gz -C /tmp/

        # Déplacer le binaire et nettoyer
        sudo mv /tmp/node_exporter-${NODE_EXPORTER_VERSION}.linux-amd64/node_exporter /usr/local/bin/
        rm -rf /tmp/node_exporter*

        # Créer l'utilisateur node_exporter (si n'existe pas)
        sudo useradd -rs /bin/false node_exporter || true

        # Créer le répertoire pour textfile_collector (pour les métriques personnalisées par Ansible)
        sudo mkdir -p /var/lib/node_exporter/textfile_collector
        sudo chown node_exporter:node_exporter /var/lib/node_exporter/textfile_collector

        # Créer le fichier de service systemd pour Node Exporter
        sudo bash -c 'cat << EOF > /etc/systemd/system/node_exporter.service
        [Unit]
        Description=Node Exporter
        Wants=network-online.target
        After=network-online.target

        [Service]
        User=node_exporter
        Group=node_exporter
        Type=simple
        ExecStart=/usr/local/bin/node_exporter --web.listen-address="0.0.0.0:9100" --collector.textfile.directory=/var/lib/node_exporter/textfile_collector

        [Install]
        WantedBy=multi-user.target
        EOF'

        # Recharger systemd, démarrer et activer Node Exporter
        sudo systemctl daemon-reload
        sudo systemctl enable node_exporter
        sudo systemctl start node_exporter
        sudo systemctl status node_exporter --no-pager
      SHELL
      # --- FIN DE LA NOUVELLE SECTION POUR PROVISIONNEMENT ---

    end
  end
end