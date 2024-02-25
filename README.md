# Testes com ScyllaDB

Este guia o ajudará a implantar o ScyllaDB, um banco de dados NoSQL altamente escalável, em um cluster Kubernetes.

## Pré-requisitos
- Um cluster Kubernetes ([caso não tenha, veja este guia](https://raissonsouto.notion.site/Guia-para-instala-o-do-Kubernetes-6fc8a731f39a4ede8b946393e4492a96))


## Instalar o ScyllaDB

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
