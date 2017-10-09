---
title: aaaDeploy e atualizar localmente microservices do Azure | Microsoft Docs
description: Saiba como tooset um cluster do Service Fabric local, implante um tooit de aplicativo existente e, em seguida, atualizar o aplicativo.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 60a1f6a5-5478-46c0-80a8-18fe62da17a8
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/13/2017
ms.author: ryanwi;mikhegn
ms.openlocfilehash: e5f5adc9edb71433b2a7635e9d661ff92a4b18ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-deploying-and-upgrading-applications-on-your-local-cluster"></a>Introdução à implantação e à atualização de aplicativos em seu cluster local
Olá SDK do Azure Service Fabric inclui um ambiente de desenvolvimento completo local que você pode usar tooquickly começar a implantar e gerenciar aplicativos em um cluster local. Neste artigo, criar um cluster local, implante um tooit de aplicativo existente e, em seguida, atualizar o aplicativo tooa nova versão, tudo a partir do Windows PowerShell.

> [!NOTE]
> Este artigo pressupõe que você já tenha [configurado seu ambiente de desenvolvimento](service-fabric-get-started.md).
> 
> 

## <a name="create-a-local-cluster"></a>Criar um cluster local
Um cluster do Service Fabric representa um conjunto de recursos de hardware em que você pode implantar aplicativos. Normalmente, um cluster consiste em qualquer lugar de cinco toomany milhares de máquinas. No entanto, a saudação SDK do Service Fabric inclui uma configuração de cluster que pode ser executados em um único computador.

É importante toounderstand que Olá cluster local do serviço de malha não é um simulador ou emulador. Ele é executado Olá mesmo código de plataforma que é encontrado em clusters com vários computadores. Olá única diferença é que ele seja executado processos de plataforma de saudação que normalmente estão espalhados em cinco máquinas em um computador.

Olá SDK fornece dois tooset maneiras um cluster local: do Windows PowerShell script e hello Gerenciador de Cluster Local system bandeja aplicativo. Neste tutorial, usamos o script do PowerShell hello.

> [!NOTE]
> Se você já tiver criado um cluster local ao implantar um aplicativo do Visual Studio, poderá ignorar esta seção.
> 
> 

1. Inicie uma nova janela do PowerShell como administrador.
2. Execute o script de instalação de cluster de saudação da pasta de saudação do SDK:
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"
    ```
   
    A instalação do cluster leva alguns minutos. Após a conclusão da instalação, você verá uma saída como esta:
   
    ![Saída da instalação do cluster][cluster-setup-success]
   
    Agora você está pronto tootry Implantando um cluster de tooyour do aplicativo.

## <a name="deploy-an-application"></a>Implantar um aplicativo
Olá SDK do Service Fabric inclui um conjunto avançado de estruturas e ferramentas para criar aplicativos de desenvolvedor. Se você estiver interessado em saber mais sobre como toocreate aplicativos no Visual Studio, consulte [criar seu primeiro aplicativo de malha do serviço no Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).

Neste tutorial, você usar um aplicativo de exemplo existente (chamado WordCount) para que você possa se concentrar em aspectos do gerenciamento de saudação da plataforma Olá: implantação, monitoramento e atualização.

1. Inicie uma nova janela do PowerShell como administrador.
2. Importar o módulo do PowerShell do SDK do Service Fabric hello.
   
    ```powershell
    Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
    ```
3. Crie um aplicativo hello toostore de diretório que você baixar e implanta, como C:\ServiceFabric.
   
    ```powershell
    mkdir c:\ServiceFabric\
    cd c:\ServiceFabric\
    ```
4. [Baixe o aplicativo de WordCount hello](http://aka.ms/servicefabric-wordcountapp) toohello local criado por você.  Observação: o navegador Microsoft Edge de saudação salva o arquivo de saudação com um *. zip* extensão.  Alterar a extensão de arquivo hello muito*.sfpkg*.
5. Conecte o cluster local toohello:
   
    ```powershell
    Connect-ServiceFabricCluster localhost:19000
    ```
6. Crie um novo aplicativo usando o comando de implantação de saudação do SDK com um nome e um pacote de aplicativo de toohello de caminho.
   
    ```powershell  
   Publish-NewServiceFabricApplication -ApplicationPackagePath c:\ServiceFabric\WordCountV1.sfpkg -ApplicationName "fabric:/WordCount"
    ```
   
    Se tudo correr bem, você deverá ver Olá saída a seguir:
   
    ![Implantar um cluster local do aplicativo toohello][deploy-app-to-local-cluster]
7. aplicativo de hello toosee em ação, inicie o navegador hello e navegue muito[http://localhost:8081/wordcount/index.html](http://localhost:8081/wordcount/index.html). Você deverá ver:
   
    ![IU do aplicativo implantado][deployed-app-ui]
   
    Olá aplicativo WordCount é simple. Ele inclui o cliente JavaScript código toogenerate aleatória cinco caracteres "palavras", que são retransmitidas toohello aplicativo por meio da API Web do ASP.NET. Um serviço com monitoração de estado rastreia o número de saudação de palavras contados. Eles serão particionados com base no primeiro o caractere de palavra Olá Olá. Você pode encontrar o código-fonte Olá para o aplicativo WordCount Olá Olá [clássico Introdução exemplos](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).
   
    aplicativo de Hello implantamos contém quatro partições. Portanto palavras que começam com À G são armazenadas na primeira partição do hello, palavras que começam com H até N são armazenadas na segunda partição de saudação e assim por diante.

## <a name="view-application-details-and-status"></a>Exibir detalhes e o status do aplicativo
Agora que estamos implantou o aplicativo hello, vamos examinar alguns dos detalhes do aplicativo hello no PowerShell.

1. Consulta implantados todos os aplicativos em cluster hello:
   
    ```powershell
    Get-ServiceFabricApplication
    ```
   
    Supondo que você implantou apenas Olá WordCount aplicativo, você verá algo semelhante a:
   
    ![Consultar todos os aplicativos implantados no PowerShell][ps-getsfapp]
2. Vá toohello próximo nível consultando o conjunto de saudação de serviços que são incluídos no aplicativo de WordCount hello.
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Lista de serviços para o aplicativo hello no PowerShell][ps-getsfsvc]
   
    aplicativo Hello é composto de dois serviços, Olá web front-end e serviço de monitoração de estado de saudação que gerencia palavras Olá.
3. Por fim, examine a lista Olá de partições para WordCountService:
   
    ```powershell
    Get-ServiceFabricPartition 'fabric:/WordCount/WordCountService'
    ```
   
    ![Exibir hello serviço partições no PowerShell][ps-getsfpartitions]
   
    Olá conjunto de comandos que você usou, como todos os comandos do PowerShell de malha do serviço, estão disponíveis para qualquer cluster que você pode se conectar ao local ou remoto.
   
    Para um toointeract de maneira mais visual com cluster hello, você pode usar Olá web Service Fabric Explorer ferramenta navegando muito[http://localhost:19080/Explorer](http://localhost:19080/Explorer) no navegador de saudação.
   
    ![Exibir detalhes do aplicativo no Service Fabric Explorer][sfx-service-overview]
   
   > [!NOTE]
   > toolearn mais sobre o Service Fabric Explorer, consulte [visualizar seu cluster com o Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).
   > 
   > 

## <a name="upgrade-an-application"></a>Atualizar um aplicativo
Service Fabric fornece atualizações nenhum tempo de inatividade, monitorando a integridade de saudação do aplicativo hello conforme ele lança cluster hello. Execute uma atualização do aplicativo WordCount do hello.

nova versão de saudação do aplicativo hello agora conta apenas as palavras que começam com uma vogal. Atualização de saudação distribui, vemos duas alterações no comportamento do aplicativo hello. Primeiro, taxa de saudação em que a contagem de saudação cresce deve lenta, já que menos palavras são contadas. Em segundo lugar, como partição primeiro Olá tem dois vogais (A e E) e todas as outras partições contêm somente um, sua contagem deve eventualmente iniciar toooutpace Olá outras pessoas.

1. [Baixe o pacote da versão 2 do hello WordCount](http://aka.ms/servicefabric-wordcountappv2) toohello mesmo local onde você baixou o pacote de versão 1 hello.
2. Retornar tooyour janela do PowerShell e use o comando upgrade de saudação do SDK tooregister Olá nova versão em cluster hello. Começar a atualizar malha Olá: / aplicativo WordCount.
   
    ```powershell
    Publish-UpgradedServiceFabricApplication -ApplicationPackagePath C:\ServiceFabric\WordCountV2.sfpkg -ApplicationName "fabric:/WordCount" -UpgradeParameters @{"FailureAction"="Rollback"; "UpgradeReplicaSetCheckTimeout"=1; "Monitored"=$true; "Force"=$true}
    ```
   
    Você deve ver a saída no PowerShell Olá atualização a seguir Olá começa.
   
    ![Andamento da atualização no PowerShell][ps-appupgradeprogress]
3. Enquanto a atualização Olá é continuar, talvez seja mais fácil toomonitor o status do Gerenciador do Service Fabric. Inicie uma janela do navegador e navegue muito[http://localhost:19080/Explorer](http://localhost:19080/Explorer). Expanda **aplicativos** na árvore de Olá Olá esquerda, escolha **WordCount**e, finalmente, **fabric: / WordCount**. Na guia do essentials Olá, você deve ver um status de saudação da atualização de saudação conforme ele passa os domínios de atualização do cluster hello.
   
    ![Andamento da atualização no Service Fabric Explorer][sfx-upgradeprogress]
   
    Como atualização Olá continua por meio de cada domínio, verificações de integridade são realizada tooensure que o aplicativo hello está se comportando corretamente.
4. Se você executar novamente a saudação anterior de consulta para conjunto de saudação de serviços na malha Olá: / aplicativo WordCount, observe que Olá WordCountService versão alterada mas Olá WordCountWebService versão não:
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Consultar serviços de aplicativos após a atualização][ps-getsfsvc-postupgrade]
   
    Este exemplo destaca como o Service Fabric gerencia atualizações de aplicativo. Ele envolve apenas Olá conjunto de serviços (ou pacotes de código/configuração nesses serviços) que foram alterados, que torna o processo de saudação de atualização mais rápida e confiável.
5. Finalmente, retorne o comportamento da saudação tooobserve toohello navegador da nova versão do aplicativo hello. Conforme o esperado, Olá contagem progride mais lentamente e Olá primeira partição acaba com um pouco mais de volume hello.
   
    ![Exibição Olá nova versão do aplicativo hello no navegador Olá][deployed-app-ui-v2]

## <a name="cleaning-up"></a>Limpando
Antes de encapsular o, é importante tooremember que Olá cluster local é real. Aplicativos continuam toorun no plano de fundo Olá até você removê-los.  Dependendo da natureza da saudação de seus aplicativos, um aplicativo em execução pode consomem recursos significativos em seu computador. Você tem vários aplicativos de toomanage de opções e cluster hello:

1. tooremove um aplicativo individual e todos os-lo da dados, execute o comando a seguir de saudação:
   
    ```powershell
    Unpublish-ServiceFabricApplication -ApplicationName "fabric:/WordCount"
    ```
   
    Ou exclua o aplicativo hello do hello Service Fabric Explorer **ações** menu ou menu de contexto de saudação na exibição de lista do aplicativo esquerdo hello.
   
    ![Excluir um aplicativo no Service Fabric Explorer][sfe-delete-application]
2. Depois de excluir o aplicativo hello do cluster hello, cancele o registro versões 1.0.0 e 2.0.0 de saudação WordCount tipo de aplicativo. A exclusão remove os pacotes de aplicativos hello, incluindo código hello e configuração do cluster de saudação repositório de imagens.
   
    ```powershell
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 2.0.0
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 1.0.0
    ```
   
    Ou, no Gerenciador do Service Fabric, escolha **desconfiguração tipo** para o aplicativo hello.
3. tooshut cluster hello, mas manter os dados aplicativo hello e rastreamentos, clique em **parar Cluster Local** no aplicativo de bandeja do sistema hello.
4. cluster de saudação toodelete totalmente, clique em **remover Cluster Local** no aplicativo de bandeja do sistema hello. Essa opção resultará em outro Olá de implantação lenta próxima vez que você pressionar F5 no Visual Studio. Remova cluster local Olá somente se você não pretende toouse-lo por algum tempo ou se você precisa de recursos de tooreclaim.

## <a name="one-node-and-five-node-cluster-mode"></a>Modo de um nó e de cinco nós do cluster
Ao desenvolver aplicativos, você geralmente acaba fazendo iterações rápidas entre a produção do código, depuração, alteração do código e depuração. toohelp otimizar esse processo, o cluster local Olá pode ser executado em dois modos: um nó ou cinco nós. Os dois modos de cluster têm seus benefícios. Modo de cinco nós de cluster permite que você toowork com um cluster real. Você pode testar os cenários de failover, trabalhar com mais instâncias e réplicas de seus serviços. Modo de cluster de um nó é otimizada toodo rápida implantação e o registro de serviços, toohelp você valida o código usando o tempo de execução do Service Fabric Olá rapidamente.

Tanto o modo de um nó como o de cinco nós do cluster não são um emulador ou simulador. cluster de desenvolvimento local Olá executa Olá mesmo código de plataforma que é encontrado em clusters com vários computadores.

> [!WARNING]
> Quando você altera o modo de saudação do cluster, o cluster atual Olá é removido do seu sistema e um novo cluster é criado. dados de saudação armazenados em cluster Olá são excluídos quando você altera o modo de cluster.
> 
> 

toochange Olá modo tooone cluster de nó, selecione **alterne o modo de Cluster** no hello Gerenciador de Cluster de Local do serviço de malha.

![Alternar o modo de cluster][switch-cluster-mode]

Ou então, alterar o modo de saudação do cluster usando o PowerShell:

1. Inicie uma nova janela do PowerShell como administrador.
2. Execute o script de instalação de cluster de saudação da pasta de saudação do SDK:
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1" -CreateOneNodeCluster
    ```
   
    A instalação do cluster leva alguns minutos. Após a conclusão da instalação, você verá uma saída como esta:
   
    ![Saída da instalação do cluster][cluster-setup-success-1-node]

## <a name="next-steps"></a>Próximas etapas
* Agora que você implantou e atualizou alguns aplicativos pré-compilados, poderá [tentar compilar seu próprio aplicativo no Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).
* Todas as ações de saudação executadas no cluster local do hello neste artigo podem ser executadas em um [cluster do Azure](service-fabric-cluster-creation-via-portal.md) também.
* atualização de saudação que realizamos neste artigo foi básico. Consulte Olá [documentação de atualização](service-fabric-application-upgrade.md) toolearn mais sobre o power hello e flexibilidade de atualizações de malha do serviço.

<!-- Images -->

[cluster-setup-success]: ./media/service-fabric-get-started-with-a-local-cluster/LocalClusterSetup.png
[extracted-app-package]: ./media/service-fabric-get-started-with-a-local-cluster/ExtractedAppPackage.png
[deploy-app-to-local-cluster]: ./media/service-fabric-get-started-with-a-local-cluster/DeployAppToLocalCluster.png
[deployed-app-ui]: ./media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-v1.png
[deployed-app-ui-v2]: ./media/service-fabric-get-started-with-a-local-cluster/DeployedAppUI-PostUpgrade.png
[sfx-app-instance]: ./media/service-fabric-get-started-with-a-local-cluster/SfxAppInstance.png
[sfx-two-app-instances-different-partitions]: ./media/service-fabric-get-started-with-a-local-cluster/SfxTwoAppInstances-DifferentPartitionCount.png
[ps-getsfapp]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFApp.png
[ps-getsfsvc]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc.png
[ps-getsfpartitions]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFPartitions.png
[ps-appupgradeprogress]: ./media/service-fabric-get-started-with-a-local-cluster/PS-AppUpgradeProgress.png
[ps-getsfsvc-postupgrade]: ./media/service-fabric-get-started-with-a-local-cluster/PS-GetSFSvc-PostUpgrade.png
[sfx-upgradeprogress]: ./media/service-fabric-get-started-with-a-local-cluster/SfxUpgradeOverview.png
[sfx-service-overview]: ./media/service-fabric-get-started-with-a-local-cluster/sfx-service-overview.png
[sfe-delete-application]: ./media/service-fabric-get-started-with-a-local-cluster/sfe-delete-application.png
[cluster-setup-success-1-node]: ./media/service-fabric-get-started-with-a-local-cluster/cluster-setup-success-1-node.png
[switch-cluster-mode]: ./media/service-fabric-get-started-with-a-local-cluster/switch-cluster-mode.png
