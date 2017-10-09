---
title: "cluster do Azure Kubernetes aaaMonitor - gerenciamento de operações | Microsoft Docs"
description: "Monitoramento do cluster Kubernetes no serviço de contêiner do Azure usando o Microsoft Operations Management Suite"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: 7474ee1571134ffe43ff8e4041cf5a64f5635bb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-microsoft-operations-management-suite-oms"></a>Monitorar um cluster do Serviço de Contêiner do Azure com o Microsoft Operations Management Suite (OMS)

## <a name="prerequisites"></a>Pré-requisitos
Este passo a passo presume que você tenha [criado um cluster Kubernetes usando o Serviço de contêiner do Azure](container-service-kubernetes-walkthrough.md).

Ele também pressupõe que você tenha Olá `az` cli do Azure e `kubectl` ferramentas instaladas.

Você pode testar se você tiver Olá `az` ferramenta instalada executando:

```console
$ az --version
```

Se você não tiver Olá `az` ferramenta instalada, há instruções [aqui](https://github.com/azure/azure-cli#installation).  
Como alternativa, você pode usar [Shell de nuvem do Azure](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), que tem Olá `az` cli do Azure e `kubectl` ferramentas já instaladas para você.  

Você pode testar se você tiver Olá `kubectl` ferramenta instalada executando:

```console
$ kubectl version
```

Se não tem `kubectl` instalado, você pode executar:
```console
$ az acs kubernetes install-cli
```

tootest se você tiver chaves kubernetes instaladas em sua ferramenta kubectl que você pode executar:
```console
$ kubectl get nodes
```

Se hello acima erros de comando out, você precisa chaves do cluster kubernetes tooinstall em sua ferramenta kubectl. Você pode fazer isso com hello comando a seguir:
```console
RESOURCE_GROUP=my-resource-group
CLUSTER_NAME=my-acs-name
az acs kubernetes get-credentials --resource-group=$RESOURCE_GROUP --name=$CLUSTER_NAME
```

## <a name="monitoring-containers-with-operations-management-suite-oms"></a>Contêineres de monitoramentos no Operations Management Suite (OMS)

O OMS (Microsoft Operations Management Suite) é a solução de gerenciamento de TI baseada em nuvem da Microsoft que ajuda você a gerenciar e proteger sua infraestrutura local e em nuvem. Contêiner é uma solução de análise de logs do OMS, que ajuda a exibir o inventário de contêiner hello, desempenho e logs em um único local. Você pode auditar, solucionar problemas de contêineres exibindo Olá logs em um local centralizado e encontrar ruidosas consumindo em excesso contêiner em um host.

![](media/container-service-monitoring-oms/image1.png)

Para obter mais informações sobre solução de contêiner, consulte toothe [análise de logs de solução de contêiner](../../log-analytics/log-analytics-containers.md).

## <a name="installing-oms-on-kubernetes"></a>Instalando o OMS em Kubernetes

### <a name="obtain-your-workspace-id-and-key"></a>Obter sua ID do espaço de trabalho e a chave
Saudação de serviço do OMS agente tootalk toohello necessárias toobe configurado com uma id do espaço de trabalho e uma chave do espaço de trabalho. tooget Olá id e a chave é necessário toocreate um OMS conta em <https://mms.microsoft.com>. Siga etapas de saudação toocreate uma conta. Quando você terminar de criar conta de saudação, você precisa tooobtain sua id e a chave clicando **configurações**, em seguida, **fontes conectadas**e, em seguida, **servidores Linux**, conforme mostrado abaixo.

 ![](media/container-service-monitoring-oms/image5.png)

### <a name="install-hello-oms-agent-using-a-daemonset"></a>Instalar o agente do OMS hello usando um DaemonSet
DaemonSets são usados por Kubernetes toorun uma única instância de um contêiner em cada host no cluster hello.
Eles são perfeitos para a execução de agentes de monitoramento.

Aqui está a saudação [arquivo YAML DaemonSet](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes). Salve-o arquivo tooa chamado `oms-daemonset.yaml` e substitua os valores de espaço reservado de saudação para `WSID` e `KEY` com a id do espaço de trabalho e a chave no arquivo hello.

Depois de adicionar a ID do espaço de trabalho e a chave toohello DaemonSet configuração, você pode instalar o agente do OMS Olá em seu cluster com hello `kubectl` ferramenta de linha de comando:

```console
$ kubectl create -f oms-daemonset.yaml
```

### <a name="installing-hello-oms-agent-using-a-kubernetes-secret"></a>Instalando o agente do OMS hello usando um segredo Kubernetes
tooprotect a ID do espaço de trabalho do OMS e a chave que você pode usar o segredo Kubernetes como parte do arquivo DaemonSet YAML.

 - Copie o script hello, arquivo de modelo de segredo e hello arquivo DaemonSet YAML (de [repositório](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) e certifique-se de que elas estão no hello mesmo diretório. 
      - script de geração de segredo – secret-gen.sh
      - modelo de segredo – secret-template.yaml
   - Arquivo YAML do DaemonSet – omsagent-ds-secrets.yaml
 - Execute o script hello. Olá script pedirá Olá ID do espaço de trabalho do OMS e a chave primária. Insira o que e script hello criará um arquivo yaml segredo para que você pode executá-lo.   
   ```
   #> sudo bash ./secret-gen.sh 
   ```

   - Crie pod de segredos Olá executando Olá seguinte:``` kubectl create -f omsagentsecret.yaml ```
 
   - toocheck, execute Olá seguinte: 

   ``` 
   root@ubuntu16-13db:~# kubectl get secrets
   NAME                  TYPE                                  DATA      AGE
   default-token-gvl91   kubernetes.io/service-account-token   3         50d
   omsagent-secret       Opaque                                2         1d
   root@ubuntu16-13db:~# kubectl describe secrets omsagent-secret
   Name:           omsagent-secret
   Namespace:      default
   Labels:         <none>
   Annotations:    <none>

   Type:   Opaque

   Data
   ====
   WSID:   36 bytes
   KEY:    88 bytes 
   ```
 
  - Criar o omsagent daemon-set executando ``` kubectl create -f omsagent-ds-secrets.yaml ```

### <a name="conclusion"></a>Conclusão
É isso! Após alguns minutos, você deve ser capaz de toosee dados fluindo tooyour painel do OMS.
