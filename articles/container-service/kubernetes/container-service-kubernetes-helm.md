---
title: "contêineres de aaaDeploy com o comando no Azure Kubernetes | Microsoft Docs"
description: "Use contêineres de toodeploy Olá comando empacotamento ferramenta em um cluster de Kubernetes no serviço de contêiner do Azure"
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/10/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: c7bd780afe00084ebe4e3a14873e1e340a29d144
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-helm-toodeploy-containers-on-a-kubernetes-cluster"></a>Usar contêineres de toodeploy de comando em um cluster de Kubernetes 

[Comando](https://github.com/kubernetes/helm/) é uma ferramenta de empacotamento do código-fonte aberto que ajuda a instalar e gerenciar o ciclo de vida de saudação do Kubernetes aplicativos. Gerenciadores de pacotes de tooLinux semelhantes, como get Apt e Yum, comando é usado toomanage Kubernetes gráficos que são pacotes de recursos de Kubernetes pré-configurado. Este artigo mostra como toowork com o comando em um cluster Kubernetes implantados no serviço de contêiner do Azure.

O Helm tem dois componentes: 
* Olá **comando CLI** é um cliente que é executado em seu computador, localmente ou na nuvem Olá  

* **Tiller** é um servidor que é executado no cluster de Kubernetes hello e gerencia o ciclo de vida de saudação de seus aplicativos Kubernetes 
 
## <a name="prerequisites"></a>Pré-requisitos

* [Implantar um cluster Kubernetes](container-service-kubernetes-walkthrough.md) no Serviço de Contêiner do Azure

* [Instalar e configurar o `kubectl`](../container-service-connect.md) em um computador local

* [Instalar o Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md) em um computador local

## <a name="helm-basics"></a>Noções básicas do Helm 

informações de tooview sobre Olá Kubernetes cluster que você está instalando Tiller e implantar seus aplicativos, digite hello comando a seguir:

```bash
kubectl cluster-info 
```
![informações do cluster kubectl](./media/container-service-kubernetes-helm/clusterinfo.png)
 
Depois que você instalou o comando, instale Tiller em seu cluster Kubernetes digitando o comando a seguir de saudação:

```bash
helm init --upgrade
```
Quando ele for concluído com êxito, você verá a saída como Olá seguinte:

![Instalação do Tiller](./media/container-service-kubernetes-helm/tiller-install.png)
 
 
 
 
tooview todos os Olá comando gráficos disponíveis no repositório de hello, Olá tipo a seguir de comando:

```bash 
helm search 
```

Você verá a saída como Olá seguinte:

![Pesquisa do Helm](./media/container-service-kubernetes-helm/helm-search.png)
 
tooupdate Olá gráficos tooget Olá versões mais recentes, digite:

```bash 
helm repo update 
```
## <a name="deploy-an-nginx-ingress-controller-chart"></a>Implantar um gráfico de controlador de entrada do Nginx 
 
toodeploy um gráfico de controlador de entrada Nginx, digite um único comando:

```bash
helm install stable/nginx-ingress 
```
![Implantar o controlador de entrada](./media/container-service-kubernetes-helm/nginx-ingress.png)

Se você digitar `kubectl get svc` tooview todos os serviços que estão em execução no cluster hello, verá que um endereço IP seja atribuído toohello controlador de entrada. (Enquanto atribuição hello está em andamento, você verá `<pending>`. Leva alguns minutos toocomplete.) 

Depois que o endereço IP de saudação é atribuído, navegue toohello valor Olá externo IP endereço toosee Olá Nginx back-end em execução. 
 
![Endereço IP de entrada](./media/container-service-kubernetes-helm/ingress-ip-address.png)


toosee uma lista de gráficos instalado no seu cluster, tipo:

```bash
helm list 
```

Você pode abreviar o comando Olá muito`helm ls`.
 
 
 
 
## <a name="deploy-a-mariadb-chart-and-client"></a>Implantar um cliente e um gráfico MariaDB

Agora, implante um gráfico de MariaDB e um banco de dados do MariaDB cliente tooconnect toohello.

gráfico do MariaDB toodeploy hello, Olá tipo comando a seguir:

```bash
helm install --name v1 stable/mariadb
```

em que `--name` é uma marcação usada para lançamentos.

> [!TIP]
> Se a implantação Olá falhar, execute `helm repo update` e tente novamente.
>
 
 
tooview todos os gráficos de saudação implantadas no cluster, tipo:

```bash 
helm list
```
 
tooview todas as implantações em execução no seu cluster, digite:

```bash
kubectl get deployments 
``` 
 
 
Por fim, toorun um cliente de saudação do pod tooaccess, digite:

```bash
kubectl run v1-mariadb-client --rm --tty -i --image bitnami/mariadb --command -- bash  
``` 
 
 
cliente de toohello tooconnect, Olá tipo comando a seguir, substituindo `v1-mariadb` com o nome de saudação da implantação:

```bash
sudo mysql –h v1-mariadb
```
 
 
Agora você pode usar o padrão SQL comandos toocreate os bancos de dados, tabelas, etc. Por exemplo, `Create DATABASE testdb1;` cria um banco de dados vazio. 
 
 
 
## <a name="next-steps"></a>Próximas etapas

* Para obter mais informações sobre como gerenciar Kubernetes gráficos, consulte Olá [comando documentação](https://github.com/kubernetes/helm/blob/master/docs/index.md). 

