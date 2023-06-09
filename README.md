# Testes com ScyllaDB

Este guia o ajudará a implantar o ScyllaDB, um banco de dados NoSQL altamente escalável, em um cluster Kubernetes. Abordaremos a instalação do Docker e do Kubernetes, a configuração de um plugin de rede (Calico), a conexão dos nós ao cluster e, por fim, a instalação do ScyllaDB.

## Pré-requisitos

- Ambiente baseado em Linux (Ubuntu, CentOS, etc.)
- Acesso root ou privilégios administrativos
- Um cluster Kubernetes com nós de trabalho

## Instalação

### Passo 1: Instalar o Docker

1. Atualize a lista de pacotes em seu sistema:

```
sudo apt update
```

2. Instale o Docker usando o script de instalação:

```
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

3. Adicione seu usuário ao grupo "docker" para executar comandos Docker sem usar "sudo":

```
sudo usermod -aG docker $USER
```

4. Faça logout e login novamente para aplicar as alterações no grupo.

### Passo 2: Instalar o Kubernetes

1. Instale os pacotes necessários:

```
sudo apt update
sudo apt install -y apt-transport-https ca-certificates curl
```

2. Baixe e adicione a chave de assinatura do Kubernetes:

```
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
```

3. Adicione o repositório do Kubernetes:

```
echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
```

4. Atualize novamente a lista de pacotes:

```
sudo apt update
```

5. Instale os componentes do Kubernetes:

```
sudo apt install -y kubelet kubeadm kubectl
```

6. Inicialize o cluster do Kubernetes (no nó mestre):

```
sudo kubeadm init
```

7. Siga as instruções fornecidas pelo comando kubeadm init para configurar o kubeconfig do seu usuário.

8. Configure o plugin de rede. Neste guia, usaremos o Calico:

```
kubectl apply -f https://docs.projectcalico.org/v3.20/manifests/calico.yaml
```

### Passo 3: Conectar os Nós ao Cluster

### Passo 4: Instalar o ScyllaDB

1. Crie um arquivo ConfigMap (scylla-config.yaml) com a configuração do ScyllaDB.

2. Aplique o ConfigMap no cluster:

```
kubectl apply -f scylla-config.yaml
```

3. Crie um arquivo DaemonSet (scylla-daemonset.yaml) para implantar instâncias do ScyllaDB em cada nó de trabalho. Consulte o exemplo anterior para criar um DaemonSet.

4. Aplique o DaemonSet no cluster:

```
kubectl apply -f scylla-daemonset.yaml
```

5. Verifique se os pods do ScyllaDB estão em execução:

```
kubectl get pods
```
