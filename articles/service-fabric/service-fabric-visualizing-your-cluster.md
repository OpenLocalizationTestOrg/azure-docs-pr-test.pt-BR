---
title: aaaVisualizing o cluster usando o Gerenciador do Service Fabric | Microsoft Docs
description: "O Explorador do Service Fabric é uma ferramenta baseada na Web para inspecionar e gerenciar aplicativos em nuvem e nós em um cluster do Service Fabric do Microsoft Azure."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: c875b993-b4eb-494b-94b5-e02f5eddbd6a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: ryanwi
ms.openlocfilehash: 73adc4fc254cf6b949b4419b02a046cee3f6a83d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-your-cluster-with-service-fabric-explorer"></a>Visualizando o cluster com o Service Fabric Explorer
O Explorador do Service Fabric é uma ferramenta baseada na Web para inspecionar e gerenciar aplicativos e nós em um cluster do Service Fabric do Azure. Gerenciador do Service Fabric está hospedado diretamente no cluster hello, para que ele estará sempre disponível, independentemente de onde o cluster está em execução.

## <a name="video-tutorial"></a>Tutorial em vídeo

toolearn como toouse Service Fabric Explorer, assista Olá vídeo Microsoft Virtual Academy a seguir:

[<center><img src="./media/service-fabric-visualizing-your-cluster/SfxVideo.png" WIDTH="360" HEIGHT="244"></center>](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=bBTFg46yC_9806218965)

## <a name="connect-tooservice-fabric-explorer"></a>Conecte-se tooService Fabric Explorer
Se você seguiu as instruções de saudação muito[preparar seu ambiente de desenvolvimento](service-fabric-get-started.md), você pode iniciar o Gerenciador do Service Fabric no cluster local navegando toohttp://localhost:19080 / Explorer.

## <a name="understand-hello-service-fabric-explorer-layout"></a>Entender o layout do Service Fabric Explorer Olá
Você pode navegar por meio do Gerenciador do Service Fabric usando árvore Olá Olá esquerda. Na raiz de saudação da árvore Olá, painel de cluster de saudação fornece uma visão geral do cluster, incluindo um resumo do aplicativo e a integridade do nó.

![Painel de clusters do Explorador do Service Fabric][sfx-cluster-dashboard]

### <a name="view-hello-clusters-layout"></a>Exibir o layout do cluster Olá
Nós em um cluster do Service Fabric são colocados em uma grade bidimensional de domínios de falha e domínios de atualização. Esse posicionamento garante que os aplicativos permanecem disponíveis na presença de saudação de falhas de hardware e atualizações de aplicativo. Você pode exibir como o cluster atual Olá é distribuído usando o mapa de cluster hello.

![Mapa de clusters do Explorador do Service Fabric][sfx-cluster-map]

### <a name="view-applications-and-services"></a>Exibir aplicativos e serviços
cluster Olá contém duas subárvores: um para aplicativos e outra para nós.

Você pode usar o hello aplicativo exibição toonavigate a hierarquia lógica da malha do serviço: aplicativos, serviços, partições e réplicas.

O exemplo hello abaixo, Olá aplicativo **MyApp** consiste em dois serviços, **MyStatefulService** e **WebService**. Como o **MyStatefulService** tem monitoração de estado, ele inclui uma partição com uma réplica principal e duas secundárias. Por outro lado, o WebSvcService é sem monitoração de estado e contém uma única instância.

![Exibição do aplicativo do Explorador do Service Fabric][sfx-application-tree]

Em cada nível da árvore de hello, painel principal Olá mostra informações pertinentes sobre o item de saudação. Por exemplo, você pode ver o status de integridade de saudação e versão para um serviço específico.

![Painel essencial do Explorador do Service Fabric][sfx-service-essentials]

### <a name="view-hello-clusters-nodes"></a>Visualizar os nós do cluster Olá
exibição do nó de saudação mostra o layout físico de saudação do cluster hello. Para um nó específico, você pode inspecionar quais aplicativos têm código implantado naquele nó. Mais especificamente, você pode ver quais réplicas estão sendo executadas lá atualmente.

## <a name="actions"></a>Ações
Service Fabric Explorer oferece uma maneira rápida de tooinvoke ações em nós, aplicativos e serviços em cluster.

Por exemplo, toodelete uma instância de aplicativo, escolha o aplicativo hello da árvore Olá Olá esquerda e, em seguida, escolha **ações** > **excluir aplicativo**.

![Excluir um aplicativo no Explorador do Service Fabric][sfx-delete-application]

> [!TIP]
> Você pode executar Olá ações clicando Olá reticências próximo tooeach elemento.
>
>

Olá tabela a seguir lista as ações de saudação disponíveis para cada entidade:

| **Entidade** | **Ação** | **Descrição** |
| --- | --- | --- |
| Tipo de aplicativo |Remover o provisionamento de tipo |Remove o pacote de aplicativo de saudação do cluster de saudação repositório de imagens. Requer que todos os aplicativos de que toobe tipo removido primeiro. |
| Aplicativo |Excluir Aplicativo |Exclua aplicativo hello, incluindo todos os seus serviços e seus estados (se houver). |
| O Barramento de |Excluir serviço |Exclua serviço hello e seu estado (se houver). |
| Nó |Ativar |Ative nó hello. |
| Nó | Desativar (pausa) | Pausa no nó Olá em seu estado atual. Serviços continuam toorun mas Service Fabric não proativamente mover tudo para ou dela, a menos que ele é necessário tooprevent uma interrupção ou inconsistência de dados. Esta ação é normalmente usada tooenable depurando serviços em tooensure um nó específico que eles não serão movidos durante a inspeção. | |
| Nó | Desativar (reiniciar) | Mova todos os serviços na memória de um nó com segurança e feche os serviços persistentes. Geralmente usado quando os processos de host hello ou máquina necessidade toobe reiniciado. | |
| Nó | Desativar (remover dados) | Feche com segurança todos os serviços em execução no nó Olá após a criação de réplicas de reposição suficientes. Normalmente usado quando um nó (ou pelo menos seu armazenamento) é desabilitado permanentemente. | |
| Nó | Remover o estado do nó | Remova dados de conhecimento das réplicas de um nó de cluster de saudação. Normalmente usado quando um nó com falha já é considerado irrecuperável. | |
| Nó | Reiniciar | Simule uma falha de nó, reiniciando nó hello. Mais informações podem ser obtidas [aqui](/powershell/module/servicefabric/restart-servicefabricnode?view=azureservicefabricps) | |

Como muitas ações são destrutivas, talvez seja solicitado tooconfirm sua intenção antes da conclusão da ação de saudação.

> [!TIP]
> Todas as ações que podem ser executadas por meio do Gerenciador do Service Fabric também podem ser executadas por meio do PowerShell ou uma API REST, tooenable automação.
>
>

Você também pode usar instâncias de aplicativos do Service Fabric Explorer toocreate para um tipo determinado aplicativo e a versão. Escolha o tipo de aplicativo de Olá Olá na exibição em árvore, clique em Olá **criar instância de aplicativo** versão toohello próximo link no painel direito da saudação.

![Criar uma instância de aplicativo no Service Fabric Explorer][sfx-create-app-instance]

> [!NOTE]
> Instâncias de aplicativos criadas por meio do Service Fabric Explorer no momento não podem ser parametrizadas. Elas são criadas usando os valores de parâmetro padrão.
>
>

## <a name="connect-tooa-remote-service-fabric-cluster"></a>Conecte-se o cluster de malha do serviço remoto tooa
Se você souber o ponto de extremidade do cluster hello e tem permissões suficientes, você pode acessar Service Fabric Explorer em qualquer navegador. Isso ocorre porque o Service Fabric Explorer é apenas outro serviço que é executado no cluster hello.

### <a name="discover-hello-service-fabric-explorer-endpoint-for-a-remote-cluster"></a>Descobrir ponto de extremidade do hello Service Fabric Explorer para um cluster remoto
tooreach Service Fabric Explorer para um determinado cluster, aponte seu navegador para:

http://&lt;your-cluster-endpoint&gt;:19080/Explorer

Para clusters do Azure, Olá a URL completa também está disponível no painel de essentials de cluster de saudação do hello portal do Azure.

### <a name="connect-tooa-secure-cluster"></a>Conecte-se o cluster seguro tooa
Você pode controlar o cliente tooyour Service Fabric cluster de acesso com certificados ou usando o Azure Active Directory (AAD).

Se você tentar tooconnect tooService Fabric Explorer em um cluster seguro, dependendo da configuração do cluster de saudação você vai ser toopresent necessário um certificado de cliente ou faça logon usando o AAD.

## <a name="next-steps"></a>Próximas etapas
* [Visão geral da Possibilidade de Teste](service-fabric-testability-overview.md)
* [Gerenciando aplicativos da Malha do Serviço no Visual Studio](service-fabric-manage-application-in-visual-studio.md)
* [Implantação de aplicativos de Malha do Serviço usando o PowerShell](service-fabric-deploy-remove-applications.md)

<!--Image references-->
[sfx-cluster-dashboard]: ./media/service-fabric-visualizing-your-cluster/SfxClusterDashboard.png
[sfx-cluster-map]: ./media/service-fabric-visualizing-your-cluster/SfxClusterMap.png
[sfx-application-tree]: ./media/service-fabric-visualizing-your-cluster/SfxApplicationTree.png
[sfx-service-essentials]: ./media/service-fabric-visualizing-your-cluster/SfxServiceEssentials.png
[sfx-delete-application]: ./media/service-fabric-visualizing-your-cluster/SfxDeleteApplication.png
[sfx-create-app-instance]: ./media/service-fabric-visualizing-your-cluster/SfxCreateAppInstance.png
