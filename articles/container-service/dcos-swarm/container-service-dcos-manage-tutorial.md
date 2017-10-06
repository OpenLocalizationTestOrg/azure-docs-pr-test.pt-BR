---
title: "tutorial de serviço de contêiner aaaAzure - gerenciar DC/OS | Microsoft Docs"
description: "Tutorial de Serviço de Contêiner do Azure – gerenciar DC/SO"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Contêineres, Microsserviços, Kubernetes, DC/SO, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/17/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b91c433bfd7e48ec405cc62be1486d9d4662839d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-service-tutorial---manage-dcos"></a>Tutorial de Serviço de Contêiner do Azure – gerenciar DC/SO

DC/SO fornece uma plataforma distribuída para executar aplicativos modernos e em contêineres. Com o Serviço de Contêiner do Azure, o provisionamento de um cluster de DC/SO pronto para produção é simples e rápido. Esse início rápido detalhes as etapas básicas necessárias toodeploy um cluster de DC/OS e execução de carga de trabalho básica.

> [!div class="checklist"]
> * Criar um cluster de DC/SO do ACS
> * Conecte-se o cluster toohello
> * Instalar Olá CLI DC/OS
> * Implantar um cluster de toohello do aplicativo
> * Dimensionar um aplicativo no cluster Olá
> * Expandir nós de cluster Olá DC/OS
> * Gerenciamento básico do DC/SO
> * Excluir Olá DC/OS cluster

Este tutorial requer Olá CLI do Azure versão 2.0.4 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooupgrade, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-dcos-cluster"></a>Criar cluster de DC/SO

Primeiro, crie um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando. Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados. 

Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *westeurope* local.

```azurecli
az group create --name myResourceGroup --location westeurope
```

Em seguida, criar um cluster de DC/SO com hello [az acs criar](/cli/azure/acs#create) comando.

Olá, exemplo a seguir cria um cluster de DC/OS denominado *myDCOSCluster* e cria as chaves de SSH se eles ainda não existir. toouse um conjunto específico de chaves, use Olá `--ssh-key-value` opção.  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

Após alguns minutos, o comando de Olá for concluída e retorna informações sobre a implantação de saudação.

## <a name="connect-toodcos-cluster"></a>Conecte-se o cluster tooDC/OS

Quando um cluster de DC/SO tiver sido criado, ele poderá ser acessado por meio de um túnel SSH. Execute Olá comando tooreturn Olá endereço IP público do mestre de controlador de domínio/OS Olá a seguir. Esse endereço IP é armazenado em uma variável e usado na próxima etapa do hello.

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

toocreate Olá túnel SSH, executar Olá comando a seguir e siga o hello instruções na tela. Se a porta 80 já está em uso, Olá falhará. Saudação de atualização encapsulado tooone de porta não está em uso, como `85:localhost:80`. 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

## <a name="install-dcos-cli"></a>Instalar CLI de DC/SO

Instalar a cli do hello DC/OS usando Olá [az acs dcos install-cli](/azure/acs/dcos#install-cli) comando. Se você estiver usando o Azure CloudShell, Olá CLI DC/sistema operacional já está instalado. Se você estiver executando Olá CLI do Azure em macOS ou Linux, talvez seja necessário um comando de saudação toorun com sudo.

```azurecli
az acs dcos install-cli
```

Antes de Olá que CLI pode ser usado com cluster hello, deve ser túnel SSH Olá toouse configurado. toodo assim, executar Olá comando a seguir, ajustando porta hello, se necessário.

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a>Executar um aplicativo

padrão de saudação mecanismo para um cluster ACS DC/OS de agendamento é maratona. Maratona é toostart usado um aplicativo e gerenciar o estado de saudação do aplicativo hello no cluster de DC/OS de saudação. tooschedule um aplicativo por meio da maratona, crie um arquivo chamado **app.json maratona**, e Olá cópia seguindo o conteúdo nele. 

```json
{
  "id": "demo-app-private",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 1,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

Execute Olá após o comando tooschedule Olá aplicativo toorun no cluster de DC/OS de saudação.

```azurecli
dcos marathon app add marathon-app.json
```

status da implantação toosee Olá para o aplicativo hello, executar Olá comando a seguir.

```azurecli
dcos marathon app list
```

Olá quando **tarefas** alterna o valor da coluna de *0/1* muito*1/1*, implantação do aplicativo foi concluída.

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     0/1    ---       ---      False      DOCKER   None
```

## <a name="scale-marathon-application"></a>Dimensionar aplicativo Marathon

No exemplo anterior de saudação, um aplicativo de instância única foi criado. tooupdate essa implantação para que as três instâncias do aplicativo hello estão disponíveis, abra o hello **maratona app.json** de arquivos e atualizar Olá too3 de propriedade de instância.

```json
{
  "id": "demo-app-private",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 3,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

Atualizar o aplicativo hello usando Olá `dcos marathon app update` comando.

```azurecli
dcos marathon app update demo-app-private < marathon-app.json
```

status da implantação toosee Olá para o aplicativo hello, executar Olá comando a seguir.

```azurecli
dcos marathon app list
```

Olá quando **tarefas** alterna o valor da coluna de *1/3* muito*3/1*, implantação do aplicativo foi concluída.

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/3    ---       ---      False      DOCKER   None
```

## <a name="run-internet-accessible-app"></a>Execute o aplicativo acessível pela Internet

Olá ACS DC/OS cluster consiste em dois conjuntos de nó, Olá a um público que pode ser acessado na internet e um particular que não é acessível em Olá da internet. conjunto padrão de saudação é nós particular do hello, que foi usado no exemplo última hello.

toomake um aplicativo acessível na Olá da internet, implantá-los toohello conjunto de nós públicos. toodo portanto, conceder Olá `acceptedResourceRoles` o valor do objeto `slave_public`.

Crie um arquivo chamado **nginx public.json** e Olá cópia seguindo o conteúdo nele.

```json
{
  "id": "demo-app",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 1,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  },
  "acceptedResourceRoles": [
    "slave_public"
  ]
}
```

Execute Olá após o comando tooschedule Olá aplicativo toorun no cluster de DC/OS de saudação.

```azurecli 
dcos marathon app add nginx-public.json
```

Obter o endereço IP público de Olá Olá DC/OS públicos de agentes do cluster.

```azurecli 
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

Procurando toothis endereço retorna o site NGINX saudação padrão.

![NGINX](./media/container-service-dcos-manage-tutorial/nginx.png)

## <a name="scale-dcos-cluster"></a>Cluster de DC/SO de escala

Nos exemplos anteriores do hello, um aplicativo foi dimensionado toomultiple instância. infraestrutura de DC/OS Olá também pode ser dimensionado tooprovide mais ou menos de capacidade de computação. Isso é feito com hello [az acs dimensionar]() comando. 

contagem atual do hello toosee dos agentes de DC/sistema operacional, use Olá [az acs Mostrar](/cli/azure/acs#show) comando.

```azurecli
az acs show --resource-group myResourceGroup --name myDCOSCluster --query "agentPoolProfiles[0].count"
```

tooincrease Olá too5 contagem, use Olá [az acs dimensionar](/cli/azure/acs#scale) comando. 

```azurecli
az acs scale --resource-group myResourceGroup --name myDCOSCluster --new-agent-count 5
```

## <a name="delete-dcos-cluster"></a>Excluir cluster de DC/SO

Quando não é mais necessário, você pode usar o hello [excluir grupo de az](/cli/azure/group#delete) comando tooremove grupo de recursos de hello, cluster de DC/OS e recursos todos relacionados.

```azurecli 
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu sobre tarefas básicas de gerenciamento DC/sistema operacional incluindo Olá seguinte. 

> [!div class="checklist"]
> * Criar um cluster de DC/SO do ACS
> * Conecte-se o cluster toohello
> * Instalar Olá CLI DC/OS
> * Implantar um cluster de toohello do aplicativo
> * Dimensionar um aplicativo no cluster Olá
> * Expandir nós de cluster Olá DC/OS
> * Excluir Olá DC/OS cluster

Toohello antecipada próxima toolearn tutorial sobre como carregar o aplicativo balanceamento no controlador de domínio/sistema operacional no Azure. 

> [!div class="nextstepaction"]
> [Aplicativos de balanceamento de carga](container-service-load-balancing.md)