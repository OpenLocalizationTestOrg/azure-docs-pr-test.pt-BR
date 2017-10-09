---
title: "contêineres de saldo de aaaLoad no cluster do Azure DC/sistema operacional | Microsoft Docs"
description: "Balancear a carga entre vários contêineres em um cluster do Serviço de Contêiner do Azure DC/OS."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Contêineres, Microsserviços, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 2249cb06880cdb7e9a3aa94c0750c6a27316d349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-an-azure-container-service-dcos-cluster"></a>Balancear a carga de contêineres em um cluster do Serviço de Contêiner do Azure DC/OS
Neste artigo, vamos explorar como toocreate um balanceador de carga interno em um controlador de domínio/sistema operacional gerenciado usando maratona balanceamento de carga de serviço de contêiner do Azure. Essa configuração permite a você tooscale seus aplicativos horizontalmente. Ele também permite tootake vantagem de clusters de agente públicas e privadas de saudação colocando seu balanceadores de carga no cluster público hello e seus contêineres de aplicativos em cluster privada hello. Neste tutorial, você:

> [!div class="checklist"]
> * Configurar um balanceador de carga do Marathon
> * Implantar um aplicativo usando Olá balanceador de carga
> * Configurar um Azure Load Balancer

Você precisa de um controlador de domínio/SO ACS saudação do cluster toocomplete as etapas neste tutorial. Se necessário, [este exemplo de script](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) pode criar um para você.

Este tutorial requer Olá CLI do Azure versão 2.0.4 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooupgrade, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="load-balancing-overview"></a>Visão geral do balanceamento de carga

Há duas camadas de balanceamento de carga em um cluster de DC/SO do Serviço de Contêiner do Azure: 

**O balanceador de carga do Azure** fornece pontos de entrada pública (Olá aqueles que os usuários finais acessar). Um balanceamento de carga do Azure é fornecido automaticamente pelo serviço de contêiner do Azure e é, por padrão, a porta configurada tooexpose 80, 443 e 8080.

**Olá maratona balanceador de carga (lb maratona)** rotas instâncias de toocontainer solicitações que atendem a essas solicitações de entrada. Como podemos dimensionar contêineres Olá fornecendo nosso serviço web, Olá maratona lb se adapta dinamicamente. Esse balanceador de carga não é fornecida por padrão em seu serviço de contêiner, mas é fácil tooinstall.

## <a name="configure-marathon-load-balancer"></a>Configurar Balanceador de Carga Marathon

Balanceador de carga maratona reconfigura dinamicamente com base em contêineres de saudação que você implantou. Também é toohello resiliente perda de um contêiner ou um agente - se isso ocorrer, Apache Mesos reinicia o contêiner de saudação em outro lugar e se adapta maratona balanceamento de carga.

Execute Olá seguindo o balanceador de carga do comando tooinstall Olá maratona no cluster do agente do hello pública.

```azurecli-interactive
dcos package install marathon-lb
```

## <a name="deploy-load-balanced-application"></a>Implantar aplicativo com balanceamento de carga

Agora que temos o pacote de balanceamento de carga maratona hello, podemos implantar um contêiner de aplicativo que desejamos que o saldo de tooload. 

Primeiro, obtenha Olá FQDN de agentes Olá exposto publicamente.

```azurecli-interactive
az acs list --resource-group myResourceGroup --query "[0].agentPoolProfiles[0].fqdn" --output tsv
```

Em seguida, crie um arquivo chamado *web.json Olá* e cópia em Olá conteúdo a seguir. Olá `HAPROXY_0_VHOST` toobe atualizado com hello FQDN de agentes do controlador de domínio/OS Olá precisa de rótulo. 

```json
{
  "id": "web",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "yeasy/simple-web",
      "network": "BRIDGE",
      "portMappings": [
        { "hostPort": 0, "containerPort": 80, "servicePort": 10000 }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "labels":{
    "HAPROXY_GROUP":"external",
    "HAPROXY_0_VHOST":"YOUR FQDN",
    "HAPROXY_0_MODE":"http"
  }
}
```

Use Olá CLI DC/OS toorun Olá aplicativo. Por padrão, maratona implanta Olá Olá aplicativo toohello privada de cluster. Isso significa que Olá acima implantação somente é acessível por meio do balanceador de carga, que geralmente é o comportamento de saudação desejado.

```azurecli-interactive
dcos marathon app add hello-web.json
```

Quando o aplicativo hello tiver sido implantado, procure toohello FQDN do aplicativo com balanceamento de carga do hello agente cluster tooview.

![Imagem do aplicativo com balanceamento de carga](./media/container-service-load-balancing/lb-app.png)

## <a name="configure-azure-load-balancer"></a>Configurar o Azure Load Balancer

Por padrão, o Azure Load Balancer expõe as portas 80, 8080 e 443. Se você estiver usando um destes três portas (como fazemos em Olá exemplo acima) e nada que é necessário toodo. Você deve ser capaz de toohit FQDN do balanceador de carga do seu agente, e cada vez que você atualizar, você encontrará um de seus servidores três web em um modo de rodízio. 

Se você usar uma porta diferente, você precisa tooadd round robin regra e uma investigação do balanceador de carga Olá para porta Olá que você usou. Você pode fazer isso de saudação [CLI do Azure](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), com comandos Olá `azure network lb rule create` e `azure network lb probe create`.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu sobre balanceamento de carga no ACS com hello maratona e carga do Azure balanceadores incluindo Olá ações a seguir:

> [!div class="checklist"]
> * Configurar um balanceador de carga do Marathon
> * Implantar um aplicativo usando Olá balanceador de carga
> * Configurar um Azure Load Balancer

Avançar toohello toolearn próximo de tutorial sobre como integrar o armazenamento do Azure com o controlador de domínio/sistema operacional no Azure.

> [!div class="nextstepaction"]
> [Montar o compartilhamento de arquivos do Azure no cluster de DC/SO](container-service-dcos-fileshare.md)