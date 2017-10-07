---
title: aaaDebug seu aplicativo no Visual Studio | Microsoft Docs
description: "Melhore Olá confiabilidade e o desempenho de seus serviços, desenvolver e depurá-los no Visual Studio em um cluster de desenvolvimento local."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: cb888532-bcdb-4e47-95e4-bfbb1f644da4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek;mikhegn
ms.openlocfilehash: 8d08689e82195d09f57b462631ad04fd237bc4fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-service-fabric-application-by-using-visual-studio"></a>Depurar seu aplicativo do Service Fabric usando o Visual Studio
> [!div class="op_single_selector"]
> * [Visual Studio/CSharp](service-fabric-debugging-your-application.md) 
> * [Eclipse/Java](service-fabric-debugging-your-application-java.md)
>


## <a name="debug-a-local-service-fabric-application"></a>Depurar um aplicativo local do Service Fabric
Você pode economizar tempo e dinheiro implantando e depurando seu aplicativo do Service Fabric do Azure no cluster de desenvolvimento de um computador local. Visual Studio 2017 ou Visual Studio 2015 pode implantar aplicativos de saudação toohello cluster local e conectar-se automaticamente instâncias de tooall depurador saudação do seu aplicativo.

1. Iniciar um cluster de desenvolvimento local, seguindo as etapas de saudação em [configurar seu ambiente de desenvolvimento do Service Fabric](service-fabric-get-started.md).
2. Pressione **F5** ou clique em **Depurar** > **Iniciar Depuração**.
   
    ![Iniciar depuração de um aplicativo][startdebugging]
3. Definir pontos de interrupção no seu código e percorrer o aplicativo hello clicando nos comandos no hello **depurar** menu.
   
   > [!NOTE]
   > O Visual Studio anexa tooall instâncias do seu aplicativo. Ao percorrer o código, os pontos de interrupção podem ser atingidos por vários processos, resultando em sessões simultâneas. Tente desabilitar pontos de interrupção Olá depois que eles for atingidos, fazendo cada ponto de interrupção condicional na ID de thread de saudação ou por meio de eventos de diagnóstico.
   > 
   > 
4. Olá **eventos de diagnóstico** janela será aberta automaticamente para que você possa exibir eventos de diagnóstico em tempo real.
   
    ![Exibir eventos de diagnóstico em tempo real][diagnosticevents]
5. Você também pode abrir Olá **eventos de diagnóstico** janela no Pesquisador de objetos de nuvem.  Em **Service Fabric**, clique com o botão direito do mouse em qualquer nó e escolha **Exibir Rastreamentos de Streaming**.
   
    ![Janela de eventos de diagnóstico Olá aberto][viewdiagnosticevents]
   
    Se você quiser toofilter seus rastreamentos tooa serviço ou aplicativo específico, basta habilite streaming rastreamentos em que serviço ou aplicativo específico.
6. eventos de diagnóstico Olá podem ser vistos no hello gerado automaticamente **ServiceEventSource.cs** de arquivos e são chamados de código do aplicativo.
   
    ```csharp
    ServiceEventSource.Current.ServiceMessage(this, "My ServiceMessage with a parameter {0}", result.Value.ToString());
    ```
7. Olá **eventos de diagnóstico** janela oferece suporte à filtragem, pausando e inspecionar os eventos em tempo real.  filtro de saudação é uma pesquisa simples de cadeia de caracteres da mensagem de evento hello, incluindo seu conteúdo.
   
    ![Filtrar, pausar e retomar ou inspecionar eventos em tempo real][diagnosticeventsactions]
8. A depuração de serviços é semelhante à depuração de qualquer outro aplicativo. Normalmente, você define pontos de interrupção por meio do Visual Studio para fácil depuração. Embora as Reliable Collections sejam replicadas em vários nós, elas ainda implementam IEnumerable. Isso significa que você pode usar Olá exibição dos resultados no Visual Studio durante a depuração toosee que é armazenado dentro. Basta definir um ponto de interrupção em qualquer lugar em seu código.
   
    ![Iniciar depuração de um aplicativo][breakpoint]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="debug-a-remote-service-fabric-application"></a>Depurar um aplicativo remoto do Service Fabric
Se seus aplicativos do Service Fabric estiver executando em um cluster do Service Fabric no Azure, você será capaz de tooremotely depurar esses, diretamente do Visual Studio.

> [!NOTE]
> Olá recurso requer [Service Fabric SDK 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) e [SDK do Azure para .NET 2.9](https://azure.microsoft.com/downloads/).    
> 
> 

<!-- -->
> [!WARNING]
> Depuração remota destina-se para cenários de desenvolvimento/teste e não toobe usada em ambientes de produção, devido ao impacto de saudação em Olá aplicativos em execução.
> 
> 

1. Navegue cluster tooyour **Cloud Explorer**, com o botão direito e escolha **Ativar depuração**
   
    ![Habilitar depuração remota][enableremotedebugging]
   
    Isso iniciará o processo de saudação de habilitar Olá extensão em nós do cluster de depuração remota, bem como as configurações de rede necessárias.
2. Nó de cluster de saudação com o botão direito em **Cloud Explorer**e escolha **Anexar depurador**
   
    ![Anexar Depurador][attachdebugger]
3. Em Olá **anexar tooprocess** caixa de diálogo, escolha o processo de saudação desejado toodebug e clique em **anexar**
   
    ![Escolher processo][chooseprocess]
   
    nome de saudação do processo de saudação desejado tooattach para, equals Olá nome do seu nome de assembly do projeto de serviço.
   
    Olá depurador se anexará tooall nós executando o processo de saudação.
   
   * No caso de Olá onde você está depurando um serviço sem monitoração de estado, todas as instâncias do serviço de saudação em todos os nós são parte da sessão de depuração de saudação.
   * Se você estiver depurando um serviço com monitoração de estado, apenas Olá réplica primária de qualquer partição será ativo e, portanto, capturada pelo depurador hello. Se a réplica primária Olá move durante a sessão de depuração Olá, processamento de saudação da réplica ainda farão parte da sessão de depuração de saudação.
   * Em partições relevantes da ordem tooonly catch ou instâncias de um determinado serviço, você pode usar pontos de interrupção condicionais tooonly quebra uma partição específica ou instância.
     
     ![Ponto de interrupção condicional][conditionalbreakpoint]
     
     > [!NOTE]
     > Atualmente não há suporte para depuração de um cluster do Service Fabric com várias instâncias do hello mesmo nome executável do serviço.
     > 
     > 
4. Depois de concluir a depuração do seu aplicativo, você pode desabilitar a extensão de depuração remota Olá clicando com o cluster de saudação em **Cloud Explorer** e escolha **Desabilitar depuração**
   
    ![Desabilitar depuração remota][disableremotedebugging]

## <a name="streaming-traces-from-a-remote-cluster-node"></a>Transmitindo rastreamentos de um nó de cluster remoto
Também é possível toostream rastreamentos diretamente de um nó de cluster remoto tooVisual Studio. Esse recurso permite que você toostream os eventos de rastreamento do ETW, produzidos em um nó de cluster do Service Fabric.

> [!NOTE]
> O recurso requer o [SDK do Service Fabric 2.0](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric-VS2015) e o [SDK do Azure para .NET 2.9](https://azure.microsoft.com/downloads/).
> Esse recurso só oferece suporte a clusters em execução no Azure.
> 
> 

<!-- -->
> [!WARNING]
> Streaming rastreamentos destina-se para cenários de desenvolvimento/teste e não toobe usada em ambientes de produção, devido ao impacto de saudação em Olá aplicativos em execução.
> Em um cenário de produção, você deve confiar nos eventos de encaminhamento usando o Diagnóstico do Azure.
> 
> 

1. Navegue cluster tooyour **Cloud Explorer**, com o botão direito e escolha **habilitar rastreamentos de Streaming**
   
    ![Habilitar transmissão remota de rastreamentos][enablestreamingtraces]
   
    Isso iniciará o processo de saudação de habilitar Olá streaming extensão rastreamentos em nós do cluster, bem como as configurações de rede necessárias.
2. Expanda Olá **nós** elemento **Cloud Explorer**, nó de saudação com o botão direito você deseja toostream rastreamentos do e escolha **rastreamentos de Streaming de exibição**
   
    ![Exibir transmissão remota de rastreamentos][viewremotestreamingtraces]
   
    Repita a etapa 2 para nós quantos desejar toosee rastreamentos do. Cada fluxo de nó será mostrado em uma janela dedicada.
   
    Agora você está toosee capaz de rastreamentos de saudação emitidos pelo serviço de malha e seus serviços. Se você quiser toofilter Olá eventos tooonly mostrar um aplicativo específico, basta digite nome de saudação do aplicativo hello no filtro de saudação.
   
    ![Exibindo transmissão de rastreamentos][viewingstreamingtraces]
3. Depois de terminar de rastreamentos de streaming do cluster, você pode desabilitar remotos rastreamentos de streaming, clicando com o cluster Olá **Cloud Explorer** e escolha **desabilitar rastreamentos de Streaming**
   
    ![Desabilitar transmissão remota de rastreamentos][disablestreamingtraces]

## <a name="next-steps"></a>Próximas etapas
* [Testar um serviço da Malha do Serviço](service-fabric-testability-overview.md).
* [Gerenciar seu aplicativo do Service Fabric no Visual Studio](service-fabric-manage-application-in-visual-studio.md).

<!--Image references-->
[startdebugging]: ./media/service-fabric-debugging-your-application/startdebugging.png
[diagnosticevents]: ./media/service-fabric-debugging-your-application/diagnosticevents.png
[viewdiagnosticevents]: ./media/service-fabric-debugging-your-application/viewdiagnosticevents.png
[diagnosticeventsactions]: ./media/service-fabric-debugging-your-application/diagnosticeventsactions.png
[breakpoint]: ./media/service-fabric-debugging-your-application/breakpoint.png
[enableremotedebugging]: ./media/service-fabric-debugging-your-application/enableremotedebugging.png
[attachdebugger]: ./media/service-fabric-debugging-your-application/attachdebugger.png
[chooseprocess]: ./media/service-fabric-debugging-your-application/chooseprocess.png
[conditionalbreakpoint]: ./media/service-fabric-debugging-your-application/conditionalbreakpoint.png
[disableremotedebugging]: ./media/service-fabric-debugging-your-application/disableremotedebugging.png
[enablestreamingtraces]: ./media/service-fabric-debugging-your-application/enablestreamingtraces.png
[viewingstreamingtraces]: ./media/service-fabric-debugging-your-application/viewingstreamingtraces.png
[viewremotestreamingtraces]: ./media/service-fabric-debugging-your-application/viewremotestreamingtraces.png
[disablestreamingtraces]: ./media/service-fabric-debugging-your-application/disablestreamingtraces.png
