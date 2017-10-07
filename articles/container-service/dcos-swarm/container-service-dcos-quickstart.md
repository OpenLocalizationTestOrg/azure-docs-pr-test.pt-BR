---
title: "aaaAzure início rápido de serviço de contêiner - implantar DC/OS Cluster | Microsoft Docs"
description: "Início rápido do Serviço de Contêiner do Azure – implantar cluster de DC/SO"
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
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b961f15bd73deeafda5a3fc25ab53c839195219b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-dcos-cluster"></a>Implantar um cluster de DC/SO

DC/SO fornece uma plataforma distribuída para executar aplicativos modernos e em contêineres. Com o Serviço de Contêiner do Azure, o provisionamento de um cluster de DC/SO pronto para produção é simples e rápido. Este guia rápido detalhes Olá as etapas básicas necessárias toodeploy um cluster de DC/OS e execução de carga de trabalho básica.

Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.

Este tutorial requer Olá CLI do Azure versão 2.0.4 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooupgrade, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="log-in-tooazure"></a>Faça logon no tooAzure 

Fazer logon no tooyour assinatura do Azure com hello [logon az](/cli/azure/#login) de comando e siga o hello instruções na tela.

```azurecli
az login
```

## <a name="create-a-resource-group"></a>Criar um grupo de recursos

Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando. Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados. 

Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local.

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-dcos-cluster"></a>Criar cluster de DC/SO

Criar um cluster de DC/SO com hello [az acs criar](/cli/azure/acs#create) comando.

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

túnel SSH Olá pode ser testado navegando muito`http://localhost`. Se uma porta outros que 80 foi usada, ajustar Olá local toomatch. 

Se o túnel SSH Olá foi criado com êxito, portal de DC/OS de saudação é retornado.

![INTERFACE DO USUÁRIO DE DC/SO](./media/container-service-dcos-quickstart/dcos-ui.png)

## <a name="install-dcos-cli"></a>Instalar CLI de DC/SO

interface de linha de comando Olá DC/sistema operacional é usada toomanage um cluster de DC/OS de saudação de linha de comando. Instalar a cli do hello DC/OS usando Olá [az acs dcos install-cli](/azure/acs/dcos#install-cli) comando. Se você estiver usando o Azure CloudShell, Olá CLI DC/sistema operacional já está instalado. 

Se você estiver executando Olá CLI do Azure em macOS ou Linux, talvez seja necessário um comando de saudação toorun com sudo.

```azurecli
az acs dcos install-cli
```

Antes de Olá que CLI pode ser usado com cluster hello, deve ser túnel SSH Olá toouse configurado. toodo assim, executar Olá comando a seguir, ajustando porta hello, se necessário.

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a>Executar um aplicativo

padrão de saudação mecanismo para um cluster ACS DC/OS de agendamento é maratona. Maratona é toostart usado um aplicativo e gerenciar o estado de saudação do aplicativo hello no cluster de DC/OS de saudação. tooschedule um aplicativo por meio da maratona, crie um arquivo chamado *app.json maratona*, e Olá cópia seguindo o conteúdo nele. 

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
dcos marathon app add marathon-app.json
```

status da implantação toosee Olá para o aplicativo hello, executar Olá comando a seguir.

```azurecli
dcos marathon app list
```

Olá quando **ESPERANDO** alterna o valor da coluna de *True* muito*False*, implantação do aplicativo foi concluída.

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/1    ---       ---      False      DOCKER   None
```

Obter o endereço IP público de Olá Olá DC/OS de agentes do cluster.

```azurecli
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

Procurando toothis endereço retorna o site NGINX saudação padrão.

![NGINX](./media/container-service-dcos-quickstart/nginx.png)

## <a name="delete-dcos-cluster"></a>Excluir cluster de DC/SO

Quando não é mais necessário, você pode usar o hello [excluir grupo de az](/cli/azure/group#delete) comando tooremove grupo de recursos de hello, cluster de DC/OS e recursos todos relacionados.

```azurecli
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a>Próximas etapas

Esse início rápido, você implantou um cluster de DC/OS e executar um simple contêiner do Docker no cluster de saudação. toolearn mais sobre o serviço de contêiner do Azure, continuar toohello ACS tutoriais.

> [!div class="nextstepaction"]
> [Gerenciar um cluster de DC/SO do ACS](container-service-dcos-manage-tutorial.md)