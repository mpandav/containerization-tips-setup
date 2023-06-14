# How to install minikube on Ubuntu?

Follow steps documented here for your os flavour and architecure</br>
https://minikube.sigs.k8s.io/docs/start/

## Prerequisite steps
1. Update and upgrade packages (if its new system)

          sudo apt update || sudo apt upgrade

2. Install docker on the system from docker.io or you can choose to install from snap
          
          sudo apt install docker.io

3. Verify docker setup if its working. 
Most likely, you wiill see below error if you run any cmd without sudo (root) user permissions. 
Ex.

          ubuntu@ip-172-31-44-6:~$ docker ps
          Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get "http://%2Fvar%2Frun%2Fdocker.sock/v1.24/containers/json": dial unix /var/run/docker.sock: connect: permission denied

To solve this problem, provde permissions to current user on /var/run/* .
Ex. 

          ubuntu@ip-172-31-44-6:~$ sudo chmod 777 /var/run/

Now, you will be able to run any command without needing root previledges. 

          ubuntu@ip-172-31-44-6:~$ docker ps
          CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

## Minikube installation
You can follow below outlined steps to install minikube on ubuntu/any server.

### Install kubectl
1. Download and Install kubectl to manage your k8s cluster.

          ubuntu@ip-172-31-44-6:~$ curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl
            % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                           Dload  Upload   Total   Spent    Left  Speed
          100 46.9M  100 46.9M    0     0  21.0M      0  0:00:02  0:00:02 --:--:-- 21.0M

2. Copy and configure kubectl in system path

          ubuntu@ip-172-31-44-6:~$ chmod +x ./kubectl

          ubuntu@ip-172-31-44-6:~$ sudo mv ./kubectl /usr/local/bin/kubectl

          ubuntu@ip-172-31-44-6:~$ kubectl version
          WARNING: This version information is deprecated and will be replaced with the output from kubectl version --short.  Use --output=yaml|json to get the full version.
          Client Version: version.Info{Major:"1", Minor:"27", GitVersion:"v1.27.1", GitCommit:"4c9411232e10168d7b050c49a1b59f6df9d7ea4b", GitTreeState:"clean", BuildDate:"2023-04-14T13:21:19Z", GoVersion:"go1.20.3", Compiler:"gc", Platform:"linux/amd64"}
          Kustomize Version: v5.0.1
          The connection to the server localhost:8080 was refused - did you specify the right host or port?

### Install minikube

1. Download the correct version of minikube installer

          ubuntu@ip-172-31-44-6:~$ curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
            % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                           Dload  Upload   Total   Spent    Left  Speed
          100 80.0M  100 80.0M    0     0  24.6M      0  0:00:03  0:00:03 --:--:-- 24.6M
          ubuntu@ip-172-31-44-6:~$ 

2. Install minikube on your system

          ubuntu@ip-172-31-44-6:~$ sudo install minikube-linux-amd64 /usr/local/bin/minikube
          ubuntu@ip-172-31-44-6:~$ 

3. Start the minikube server

          ubuntu@ip-172-31-44-6:~$ minikube start
          😄  minikube v1.30.1 on Ubuntu 22.04 (xen/amd64)
          ✨  Automatically selected the docker driver. Other choices: none, ssh
          📌  Using Docker driver with root privileges
          👍  Starting control plane node minikube in cluster minikube
          🚜  Pulling base image ...
          💾  Downloading Kubernetes v1.26.3 preload ...
              > preloaded-images-k8s-v18-v1...:  397.02 MiB / 397.02 MiB  100.00% 29.42 M
              > gcr.io/k8s-minikube/kicbase...:  373.53 MiB / 373.53 MiB  100.00% 15.76 M
          🔥  Creating docker container (CPUs=2, Memory=8000MB) ...
          🐳  Preparing Kubernetes v1.26.3 on Docker 23.0.2 ...
              ▪ Generating certificates and keys ...
              ▪ Booting up control plane ...
              ▪ Configuring RBAC rules ...
          🔗  Configuring bridge CNI (Container Networking Interface) ...
              ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
          🔎  Verifying Kubernetes components...
          🌟  Enabled addons: storage-provisioner, default-storageclass
          🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default

4. Verify the setup if its running by checking the status

          ubuntu@ip-172-31-44-6:~$ minikube status
          minikube
          type: Control Plane
          host: Running
          kubelet: Running
          apiserver: Running
          kubeconfig: Configured

Good Luck!!!
