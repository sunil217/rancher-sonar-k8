# Deploy SONARQUBE on Kubernetes with Persistent Storage

  On NFS server (rancher-06) Node

    vim /etc/exports
      /sonarqube/mysql *(rw,sync,no_root_squash)
      /sonarqube/data *(rw,sync,no_root_squash)

    sudo mkdir -p /sonarqube/mysql; sudo mkdir -p /sonarqube/data
    sudo mkdir -p /sonarqube/extensions
    sudo chmod -R 755 /sonarqube

    sudo chown nfsnobody:nfsnobody /sonarqube -R

    systemctl restart rpcbind

    systemctl restart nfs-server

    systemctl restart nfs-lock

    systemctl restart nfs-idmap

on Rancher-01 (Node)

  git clone https://github.com/sunil217/rancher-sonar-k8.git

  cd rancher-sonar-k8

  inside sonar-deployment.yaml and sonar-mysql-deployment.yaml

    Replace server: "rancher06-ipaddress"

  kubectl create -f .

  open the browser and hit any ip of worker node on port 30080

      Username: admin
      Password: admin
