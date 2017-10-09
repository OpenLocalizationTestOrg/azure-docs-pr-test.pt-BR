---
title: "cluster do Azure DC/OS aaaMonitor - gerenciamento de operações | Microsoft Docs"
description: "Monitorar um cluster DC/OS do Serviço de Contêiner do Azure com o Microsoft Operations Management Suite."
services: container-service
documentationcenter: 
author: keikhara
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 11/17/2016
ms.author: keikhara
ms.custom: mvc
ms.openlocfilehash: 0ebfa3ba3cef8f0205b15731b0e91f5b304bc8fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-operations-management-suite"></a>Monitorar um cluster DC/OS do Serviço de Contêiner do Azure com o Operations Management Suite

O OMS (Microsoft Operations Management Suite) é a solução de gerenciamento de TI baseada em nuvem da Microsoft que ajuda a gerenciar e proteger sua infraestrutura local e de nuvem. Contêiner é uma solução de análise de logs do OMS, que ajuda a exibir o inventário de contêiner hello, desempenho e logs em um único local. Você pode auditar, solucionar problemas de contêineres exibindo Olá logs em um local centralizado e encontrar ruidosas consumindo em excesso contêiner em um host.

![](media/container-service-monitoring-oms/image1.png)

Para obter mais informações sobre solução de contêiner, consulte toothe [análise de logs de solução de contêiner](../../log-analytics/log-analytics-containers.md).

## <a name="setting-up-oms-from-hello-dcos-universe"></a>Configurar o OMS do universo de DC/OS Olá


Este artigo pressupõe que você tiver configurado um controlador de domínio/sistema operacional e implantar aplicativos de contêiner da web simples no cluster hello.

### <a name="pre-requisite"></a>Pré-requisito
- [Assinatura do Microsoft Azure](https://azure.microsoft.com/free/) - você pode obter uma gratuitamente.  
- Configuração do espaço de trabalho do Microsoft OMS - consulte a "Etapa 3" abaixo
- [CLI do DC/OS](https://dcos.io/docs/1.8/usage/cli/install/) instalada.

1. No painel de DC/OS hello, clique no universo e procure 'OMS', conforme mostrado abaixo.

![](media/container-service-monitoring-oms/image2.png)

2. Clique em **Instalar**. Você verá um pop backup com informações de versão do OMS hello e um **instalar pacote** ou **instalação avançada** botão. Quando você clica em **instalação avançada**, o que leva toohello **propriedades de configuração específicas do OMS** página.

![](media/container-service-monitoring-oms/image3.png)

![](media/container-service-monitoring-oms/image4.png)

3. Aqui, você deverá Olá tooenter `wsid` (Olá ID do espaço de trabalho do OMS) e `wskey` (Olá OMS chave primária para a id do espaço de trabalho de saudação). ambos os tooget `wsid` e `wskey` você precisa de uma conta do OMS no toocreate <https://mms.microsoft.com>. Siga etapas de saudação toocreate uma conta. Depois de terminar de criar conta de Olá, é necessário tooobtain seu `wsid` e `wskey` clicando **configurações**, em seguida, **fontes conectadas**e, em seguida, **servidores Linux** , conforme mostrado abaixo.

 ![](media/container-service-monitoring-oms/image5.png)

4. Selecione Olá número você OMS instâncias que você deseja e clique botão de 'Examine e instale' hello. Normalmente, você desejará toohave número de saudação de OMS instâncias toohello igual quantos você tem em seu cluster de agente da VM. Agente do OMS para Linux é instalado como contêineres individuais em cada VM que deseja toocollect informações para o monitoramento e as informações de log.

## <a name="setting-up-a-simple-oms-dashboard"></a>Configuração de um painel OMS simples

Depois que você instalou Olá agente do OMS para Linux em VMs hello, a próxima etapa é tooset o painel do OMS hello. Há dois toodo de maneiras isso: Portal do OMS ou no Portal do Azure.

### <a name="oms-portal"></a>Portal do OMS 

Faça logon no portal do OMS toohello (<https://mms.microsoft.com>) e vá toohello **Galeria de soluções**.

![](media/container-service-monitoring-oms/image6.png)

Quando estiver no hello **Galeria de soluções**, selecione **contêineres**.

![](media/container-service-monitoring-oms/image7.png)

Depois de selecionar Olá solução de contêiner, você verá Olá lado a lado na página do painel de visão geral do OMS hello. Quando os dados do contêiner Olá incluído são indexados, você verá bloco Olá populado com informações sobre os blocos de exibição de solução.

![](media/container-service-monitoring-oms/image8.png)

### <a name="azure-portal"></a>Portal do Azure 

Portal de tooAzure de logon em <https://portal.microsoft.com/>. Acesse **Marketplace**, selecione **Monitoramento + gerenciamento** e clique em **Ver Tudo**. Em seguida, digite `containers` na pesquisa. Você verá nos resultados da pesquisa hello "contêineres". Selecione **Contêineres** e clique em **Criar**.

![](media/container-service-monitoring-oms/image9.png)

Depois de clicar em **Criar**, ele solicitará seu espaço de trabalho. Selecione seu espaço de trabalho ou, se você não tiver um, crie um novo.

![](media/container-service-monitoring-oms/image10.PNG)

Depois de selecionar o espaço de trabalho, clique em **Criar**.

![](media/container-service-monitoring-oms/image11.png)

Para obter mais informações sobre Olá solução de contêiner do OMS, consulte toothe [análise de logs de solução de contêiner](../../log-analytics/log-analytics-containers.md).

### <a name="how-tooscale-oms-agent-with-acs-dcos"></a>Como tooscale agente do OMS com o ACS DC/OS 

No caso de precisar toohave instalado o agente do OMS com pouca contagem do nó real hello ou estão chegando VMSS adicionando mais VM, você pode fazer isso, dimensionando Olá `msoms` serviço.

Você pode ir de guia de serviços de interface do usuário de DC/OS tooMarathon ou hello e dimensionar sua contagem de nó.

![](media/container-service-monitoring-oms/image12.PNG)

Isso implantará nós tooother que ainda não tem implantado o agente do OMS hello.

## <a name="uninstall-ms-oms"></a>Desinstalar o MS OMS

toouninstall MS OMS digite Olá comando a seguir:

```bash
$ dcos package uninstall msoms
```

## <a name="let-us-know"></a>Fale conosco!!!
O que funciona? O que falta? O que mais você precisa para esta toobe útil para você? Fale conosco em <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.

## <a name="next-steps"></a>Próximas etapas

 Agora que você tiver configurado o OMS toomonitor seus contêineres,[ver seu painel de contêiner](../../log-analytics/log-analytics-containers.md).
