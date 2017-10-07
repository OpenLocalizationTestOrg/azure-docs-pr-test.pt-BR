---
title: "integração com o System Center Operations Manager com o mapa de aaaService | Microsoft Docs"
description: "Mapa de serviço é uma solução Operations Management Suite que detecta automaticamente os componentes do aplicativo no Windows e mapas e sistemas Linux Olá comunicação entre serviços. Este artigo discute o uso do mapa de serviço tooautomatically criar diagramas de aplicativo distribuído no Operations Manager."
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: e8614a5a-9cf8-4c81-8931-896d358ad2cb
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: bwren;dairwin
ms.openlocfilehash: cff9cce2559448ec3a5fd14087b867f314716560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-map-integration-with-system-center-operations-manager"></a>Integração do Mapa do Serviço com o System Center Operations Manager
  > [!NOTE]
  > Esse recurso está em uma versão prévia.
  > 
  
Mapa de serviço do Operations Management Suite detecta os componentes de aplicativos em sistemas Windows e Linux e mapeia a comunicação entre serviços Olá automaticamente. Mapa de serviço permite que você tooview caminho Olá servidores pensar neles, como sistemas interconectados que fornecem serviços essenciais. Mapa de serviço mostra conexões entre servidores, processos e portas em qualquer arquitetura conectado por TCP, sem nenhuma configuração necessária além de instalação de saudação de um agente. Para obter mais informações, consulte Olá [documentação de mapa de serviço](operations-management-suite-service-map.md).

Com essa integração entre o mapa de serviço e o System Center Operations Manager, você pode criar automaticamente diagramas de aplicativo distribuído no Operations Manager que se baseiam em mapas de dependência dinâmica de saudação no mapa de serviço.

## <a name="prerequisites"></a>Pré-requisitos
* Um grupo de gerenciamento do Operations Manager que gerencia um conjunto de servidores.
* Um espaço de trabalho do Operations Management Suite com hello solução Mapa de serviço habilitada.
* Um conjunto de servidores (pelo menos um) que estão sendo gerenciados pelo Operations Manager e enviar dados tooService mapa. Há suporte para servidores Windows e Linux.
* Uma entidade de serviço com acesso toohello assinatura do Azure que está associada com o espaço de trabalho do hello Operations Management Suite. Para obter mais informações, vá muito[criar uma entidade de serviço](#creating-a-service-principal).

## <a name="install-hello-service-map-management-pack"></a>Instalar pacote de gerenciamento de mapa de serviço Olá
Você habilitar a integração de saudação entre o Operations Manager e o mapa de serviço, importando Olá Microsoft.SystemCenter.ServiceMap pacote de gerenciamento (Microsoft.SystemCenter.ServiceMap.mpb). pacote de saudação contém Olá pacotes de gerenciamento a seguir:
* Exibições de Aplicativo do Mapa do Serviço da Microsoft
* Mapa do Serviço Interno do Microsoft System Center
* Substituições do Mapa do Serviço do Microsoft System Center
* Mapa do Serviço do Microsoft System Center

## <a name="configure-hello-service-map-integration"></a>Configurar a integração do mapa de serviço Olá
Depois de instalar o pacote de gerenciamento de mapa de serviço hello, um novo nó, **mapa de serviço**, é exibido em **Operations Management Suite** em Olá **administração** painel. 

tooconfigure integração com o mapa de serviço, Olá a seguir:

1. Assistente de configuração de saudação do tooopen, do hello **visão geral do mapa de serviço** painel, clique em **adicionar espaço de trabalho**.  

    ![Painel Visão Geral do Mapa do Serviço](media/oms-service-map/scom-configuration.png)

2. Em Olá **configuração de Conexão** janela, digite o nome do locatário hello ou ID, ID de aplicativo (também conhecido como nome de usuário de saudação ou clientID) e senha da entidade de serviço hello e, em seguida, clique em **próximo**. Para obter mais informações, vá muito[criar uma entidade de serviço](#creating-a-service-principal).

    ![janela de configuração de Conexão de saudação](media/oms-service-map/scom-config-spn.png)

3. Em Olá **assinatura seleção** janela, selecione Olá assinatura do Azure, o grupo de recursos do Azure (Olá que contém o espaço de trabalho do hello Operations Management Suite) e o espaço de trabalho do Operations Management Suite e, em seguida, clique em **Próximo**.

    ![Olá espaço de trabalho de configuração do Operations Manager](media/oms-service-map/scom-config-workspace.png)

4. Em Olá **seleção de grupo do computador** janela, que você escolha quais grupos de computadores do mapa de serviço você deseja toosync tooOperations Manager. Clique em **adicionar ou remover grupos de computadores**, escolha grupos na lista de saudação do **grupos de computadores disponíveis**e clique em **adicionar**.  Quando você terminar de selecionar os grupos, clique em **Okey** toofinish.
    
    ![Olá grupos de máquina de configuração do Operations Manager](media/oms-service-map/scom-config-machine-groups.png)
    
5. Em Olá **seleção de servidor** janela, que você configurar Olá grupo de servidores de mapa de serviço com servidores Olá que você deseja toosync entre o Operations Manager e o mapa de serviço. Clique em **Adicionar/Remover Servidores**.   
    
    Para Olá integração toobuild um diagrama de aplicativo distribuído para um servidor, o servidor de saudação deve ser:

    * Gerenciado pelo Operations Manager
    * Gerenciado pelo Mapa do Serviço
    * Listado em Olá grupo de servidores de mapa de serviço

    ![saudação de grupo de configuração do Operations Manager](media/oms-service-map/scom-config-group.png)

6. Opcional: Selecione toocommunicate de pool de recursos Olá servidor de gerenciamento com o Operations Management Suite e, em seguida, clique em **adicionar espaço de trabalho**.

    ![saudação de Pool de recursos de configuração do Operations Manager](media/oms-service-map/scom-config-pool.png)

    Ele pode levar um minuto tooconfigure e registrar o espaço de trabalho do hello Operations Management Suite. Depois de configurado, Operations Manager inicia a primeira sincronização de mapa de serviço saudação do Operations Management Suite.

    ![saudação de Pool de recursos de configuração do Operations Manager](media/oms-service-map/scom-config-success.png)


## <a name="monitor-service-map"></a>Monitorar o Mapa do Serviço
Depois que o espaço de trabalho do hello Operations Management Suite está conectado, uma nova pasta, o mapa de serviço, é exibida no hello **monitoramento** painel do console do Operations Manager hello.

![Painel de monitoramento do Operations Manager Olá](media/oms-service-map/scom-monitoring.png)

pasta de mapa de serviço Olá tem quatro nós:
* **Alertas ativos**: lista todos os alertas ativos do hello sobre comunicação Olá entre o Operations Manager e o mapa de serviço.  Observe que esses alertas não estão sendo sincronizados tooOperations Gerenciador de alertas de Operations Management Suite. 

* **Servidores**: listas Olá monitorado servidores configurados toosync do mapa de serviço.

    ![Painel de monitoramento de servidores do Operations Manager Olá](media/oms-service-map/scom-monitoring-servers.png)

* **Exibições de dependência de grupo do computador**: lista todos os grupos de computadores que foram sincronizados de mapa de serviço. Você pode clicar tooview qualquer grupo seu diagrama de aplicativo distribuído.

    ![diagrama de aplicativo distribuído do Operations Manager Olá](media/oms-service-map/scom-group-dad.png)

* **Exibições de Dependência de Servidor**: lista todos os servidores sincronizados por meio do Mapa do Serviço. Você pode clicar tooview qualquer servidor em seu diagrama de aplicativo distribuído.

    ![diagrama de aplicativo distribuído do Operations Manager Olá](media/oms-service-map/scom-dad.png)

## <a name="edit-or-delete-hello-workspace"></a>Editar ou excluir o espaço de trabalho de saudação
Você pode editar ou excluir espaço de trabalho de saudação configurado por meio de saudação **visão geral do mapa de serviço** painel (**administração** painel > **Operations Management Suite**  >  **Mapa de serviço**). No momento, é possível configurar apenas um espaço de trabalho do Operations Management Suite.

![Painel de espaço de trabalho do Operations Manager Editar Olá](media/oms-service-map/scom-edit-workspace.png)

## <a name="configure-rules-and-overrides"></a>Configurar regras e substituições
Uma regra, _Microsoft.SystemCenter.ServiceMapImport.Rule_, é criado tooperiodically informações de busca de mapa de serviço. intervalos de sincronização de toochange, você pode configurar substituições de regra da saudação (**criação** painel > **regras** > **Microsoft.SystemCenter.ServiceMapImport.Rule**).

![janela de propriedades de substituições do Operations Manager Olá](media/oms-service-map/scom-overrides.png)

* **Enabled**: habilite ou desabilite atualizações automáticas. 
* **IntervalMinutes**: redefinir o tempo de saudação entre as atualizações. intervalo padrão de saudação é de uma hora. Se você quiser toosync server mapas com mais frequência, você pode alterar o valor de saudação.
* **TimeoutSeconds**: redefinir o comprimento de saudação de tempo antes de solicitação de saudação expira. 
* **TimeWindowMinutes**: janela de tempo de saudação de redefinição para consultar dados. O padrão é uma janela de 60 minutos. valor máximo de saudação permitido pelo mapa de serviço é 60 minutos.

## <a name="known-issues-and-limitations"></a>Problemas e limitações conhecidos

design atual Hello apresenta seguinte Olá limitações e problemas:
* Você só pode se conectar tooa único espaço de trabalho de Operations Management Suite.
* Embora seja possível adicionar servidores toohello grupo de servidores de mapa de serviço manualmente por meio de saudação **criação** painel, Olá mapas para os servidores não são sincronizadas imediatamente.  Eles serão sincronizados do mapa de serviço durante a saudação próximo ciclo de sincronização.
* Se você fizer alterações toohello distribuídas diagramas de aplicativos criados pelo pacote de gerenciamento hello, essas alterações provavelmente serão substituídas na próxima sincronização Olá com mapa de serviço.

## <a name="create-a-service-principal"></a>Criar uma entidade de serviço
Para obter a documentação oficial do Azure sobre como criar uma entidade de serviço, consulte:
* [Criar uma entidade de serviço usando o PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [Criar uma entidade de serviço usando a CLI do Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)
* [Criar uma entidade de serviço usando Olá portal do Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal)

### <a name="feedback"></a>Comentários
Você tem algum comentário sobre o Mapa de Serviço ou sobre esta documentação? Visite nossa [página do User Voice](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), na qual você pode sugerir recursos ou votar em sugestões existentes.
