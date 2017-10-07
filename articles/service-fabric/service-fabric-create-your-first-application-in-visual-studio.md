---
title: "aaaCreate um serviço confiável do Azure Service Fabric com c#"
description: Crie, implante e depure um aplicativo Reliable Service baseado no Azure Service Fabric com o Visual Studio.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: vturecek
ms.assetid: c3655b7b-de78-4eac-99eb-012f8e042109
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/28/2017
ms.author: ryanwi
ms.openlocfilehash: 740c866da6e639219b529fe92ed63cbeaa702a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-c-service-fabric-stateful-reliable-services-application"></a>Criar seu primeiro aplicativo Reliable Services com estado do Service Fabric em C#

Saiba como toodeploy seu primeiro aplicativo do Service Fabric para .NET no Windows em apenas alguns minutos. Quando você terminar, terá um cluster local com um aplicativo de serviço confiável.

## <a name="prerequisites"></a>Pré-requisitos

Antes de começar, verifique se você [configurou o ambiente de desenvolvimento](service-fabric-get-started.md). Isso inclui a instalação Olá SDK do Service Fabric e 2017 do Visual Studio ou 2015.

## <a name="create-hello-application"></a>Criar um aplicativo hello

Inicie o Visual Studio como um **administrador**.

Criar um projeto com `CTRL`+`SHIFT`+`N`

Em Olá **novo projeto** caixa de diálogo, escolha **nuvem > aplicativo de malha do serviço**.

Nome do aplicativo hello **MyApplication** e pressione **Okey**.

   
![Caixa de diálogo Novo projeto no Visual Studio][1]

Você pode criar qualquer tipo de aplicativo de malha do serviço na próxima caixa de diálogo de saudação. Para este guia de início rápido, escolha **Serviço com Estado**.

Nome do serviço de saudação **MyStatefulService** e pressione **Okey**.

![Caixa de diálogo Novo serviço no Visual Studio][2]


Visual Studio cria o projeto de aplicativo hello e projeto de serviço com monitoração de estado hello e exibe-os no Gerenciador de soluções.

![Gerenciador de Soluções seguindo a criação de aplicativo com serviço com estado][3]

projeto de aplicativo Hello (**MyApplication**) não contém qualquer código diretamente. Em vez disso, ele faz referência a um conjunto de projetos de serviço. Além disso, ele contém três outros tipos de conteúdo:

* **Perfis de publicação**  
Perfis para a implantação de ambientes de toodifferent.

* **Scripts**  
Script do PowerShell para a implantação/atualização de seu aplicativo.

* **Definição de aplicativo**  
Inclui o arquivo applicationmanifest. XML de saudação em *ApplicationPackageRoot* que descreve a composição do aplicativo. Arquivos de parâmetro de aplicativo associados estão sob *ApplicationParameters*, que pode ser usado toospecify parâmetros específicos do ambiente. Perfil de publicação do Visual seleciona Studio associado de um arquivo de parâmetro de aplicativo que é especificado no hello durante o ambiente específico de tooa de implantação.
    
Para obter uma visão geral do conteúdo de saudação do projeto de serviço hello, consulte [Introdução aos serviços confiável](service-fabric-reliable-services-quick-start.md).

## <a name="deploy-and-debug-hello-application"></a>Implantar e depurar o aplicativo hello

Agora que você tem um aplicativo, execute-o.

No Visual Studio, pressione `F5` toodeploy aplicativo de saudação para depuração.

>[!NOTE]
>Olá a primeira vez que você executar e implanta o aplicativo hello localmente, o Visual Studio cria um cluster local para depuração. Isso pode levar algum tempo. status de criação de cluster Olá é exibido na janela de saída do Visual Studio hello.

Quando o cluster Olá estiver pronto, você obtém uma notificação de aplicativo hello cluster local system bandeja manager acompanha Olá SDK.
   
![Notificação de bandeja do sistema de cluster local][4]

Uma vez iniciado do aplicativo hello, Visual Studio fornece automaticamente Olá **Visualizador de eventos de diagnóstico**, onde você pode ver a saída de rastreamento de seus serviços.
   
![Visualizador de eventos de diagnóstico][5]

Olá modelo de serviço com monitoração de estado que usamos simplesmente mostra um incremento de valor de contador em Olá `RunAsync` método **MyStatefulService.cs**.

Expanda uma saudação eventos toosee obter mais detalhes, incluindo Olá nó onde o código hello está sendo executado. Nesse caso, é o \_Node\_2, que pode ser diferente em seu computador.
   
![Detalhe do visualizador de eventos de diagnóstico][6]

o cluster local Olá contém cinco nós hospedado em um único computador. Em um ambiente de produção, cada nó está hospedado em uma máquina virtual ou física distinta. depurador de perda de saudação toosimulate de uma máquina ao exercer Olá Visual Studio em hello mesmo tempo, vamos dar um de nós de saudação no cluster local hello.

Em Olá **Solution Explorer** janela, abra **MyStatefulService.cs**. 

Localize Olá `RunAsync` método e defina um ponto de interrupção na primeira linha de saudação do método hello.

![Ponto de interrupção no método RunAsync de serviço com estado][7]

Iniciar Olá **Service Fabric Explorer** ferramenta clicando em Olá **Gerenciador de Cluster Local** aplicativo de bandeja do sistema e escolha **gerenciar o Cluster Local**.

![Inicie o Gerenciador do Service Fabric Olá Gerenciador de Cluster Local][systray-launch-sfx]

O [**Service Fabric Explorer** ](service-fabric-visualizing-your-cluster.md) oferece uma representação visual de um cluster. Ele inclui o conjunto de saudação de tooit aplicativos implantados e conjunto Olá nós físicos que compõem-lo.

No painel esquerdo do hello, expanda **Cluster > nós** e localizar Olá nó onde seu código está sendo executado.

Clique em **ações > desativar (reinicialização)** toosimulate uma reinicialização do computador.

![Parar um nó no Service Fabric Explorer][sfx-stop-node]

Temporariamente, você deve ver o ponto de interrupção que você estava fazendo diretamente em um nó de computação de saudação failover tooanother de ocorrências no Visual Studio.


Em seguida, retornar toohello Visualizador de eventos de diagnóstico e observar as mensagens de saudação. contador de saudação continua aumentando, mesmo que eventos de saudação realmente são provenientes de um nó diferente.

![Visualizador de eventos de diagnóstico após o failover][diagnostic-events-viewer-detail-post-failover]

## <a name="cleaning-up-hello-local-cluster-optional"></a>Limpando o cluster local da saudação (opcional)

Lembre-se de que esse cluster local é real. Parar o depurador Olá remove a instância do aplicativo e cancela o registro de tipo de aplicativo hello. No entanto, o cluster de saudação continua toorun no plano de fundo de saudação. Quando você estiver cluster local do toostop pronto hello, há duas opções.

### <a name="keep-application-and-trace-data"></a>Manter os dados de aplicativo e rastreamento

Desligue o cluster de saudação clicando em Olá **Gerenciador de Cluster Local** aplicativo de bandeja do sistema e, em seguida, escolha **parar Cluster Local**.

### <a name="delete-hello-cluster-and-all-data"></a>Excluir o cluster hello e todos os dados

Remover cluster Olá clicando em Olá **Gerenciador de Cluster Local** aplicativo de bandeja do sistema e, em seguida, escolha **remover Cluster Local**. 

Se você escolher essa opção, o Visual Studio será reimplantar Olá Olá de cluster próxima vez Olá a execução do aplicativo. Escolha esta opção se você não pretende cluster local do toouse Olá por algum tempo ou se você precisar de recursos de tooreclaim.

## <a name="next-steps"></a>Próximas etapas
Leia mais sobre [Reliable Services](service-fabric-reliable-services-introduction.md).
<!-- Image References -->

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog.png
[2]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png
[3]: ./media/service-fabric-create-your-first-application-in-visual-studio/solution-explorer-stateful-service-template.png
[4]: ./media/service-fabric-create-your-first-application-in-visual-studio/local-cluster-manager-notification.png
[5]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer.png
[6]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail.png
[7]: ./media/service-fabric-create-your-first-application-in-visual-studio/runasync-breakpoint.png
[sfx-stop-node]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-deactivate-node.png
[systray-launch-sfx]: ./media/service-fabric-create-your-first-application-in-visual-studio/launch-sfx.png
[diagnostic-events-viewer-detail-post-failover]: ./media/service-fabric-create-your-first-application-in-visual-studio/diagnostic-events-viewer-detail-post-failover.png
[sfe-delete-application]: ./media/service-fabric-create-your-first-application-in-visual-studio/sfe-delete-application.png
[switch-cluster-mode]: ./media/service-fabric-create-your-first-application-in-visual-studio/switch-cluster-mode.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
