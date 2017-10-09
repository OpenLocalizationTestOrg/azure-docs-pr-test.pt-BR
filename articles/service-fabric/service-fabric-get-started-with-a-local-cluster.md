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
# <a name="get-started-with-deploying-and-upgrading-applications-on-your-local-cluster"></a><span data-ttu-id="f2cca-103">Introdução à implantação e à atualização de aplicativos em seu cluster local</span><span class="sxs-lookup"><span data-stu-id="f2cca-103">Get started with deploying and upgrading applications on your local cluster</span></span>
<span data-ttu-id="f2cca-104">Olá SDK do Azure Service Fabric inclui um ambiente de desenvolvimento completo local que você pode usar tooquickly começar a implantar e gerenciar aplicativos em um cluster local.</span><span class="sxs-lookup"><span data-stu-id="f2cca-104">hello Azure Service Fabric SDK includes a full local development environment that you can use tooquickly get started with deploying and managing applications on a local cluster.</span></span> <span data-ttu-id="f2cca-105">Neste artigo, criar um cluster local, implante um tooit de aplicativo existente e, em seguida, atualizar o aplicativo tooa nova versão, tudo a partir do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f2cca-105">In this article, you create a local cluster, deploy an existing application tooit, and then upgrade that application tooa new version, all from Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="f2cca-106">Este artigo pressupõe que você já tenha [configurado seu ambiente de desenvolvimento](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f2cca-106">This article assumes that you already [set up your development environment](service-fabric-get-started.md).</span></span>
> 
> 

## <a name="create-a-local-cluster"></a><span data-ttu-id="f2cca-107">Criar um cluster local</span><span class="sxs-lookup"><span data-stu-id="f2cca-107">Create a local cluster</span></span>
<span data-ttu-id="f2cca-108">Um cluster do Service Fabric representa um conjunto de recursos de hardware em que você pode implantar aplicativos.</span><span class="sxs-lookup"><span data-stu-id="f2cca-108">A Service Fabric cluster represents a set of hardware resources that you can deploy applications to.</span></span> <span data-ttu-id="f2cca-109">Normalmente, um cluster consiste em qualquer lugar de cinco toomany milhares de máquinas.</span><span class="sxs-lookup"><span data-stu-id="f2cca-109">Typically, a cluster is made up of anywhere from five toomany thousands of machines.</span></span> <span data-ttu-id="f2cca-110">No entanto, a saudação SDK do Service Fabric inclui uma configuração de cluster que pode ser executados em um único computador.</span><span class="sxs-lookup"><span data-stu-id="f2cca-110">However, hello Service Fabric SDK includes a cluster configuration that can run on a single machine.</span></span>

<span data-ttu-id="f2cca-111">É importante toounderstand que Olá cluster local do serviço de malha não é um simulador ou emulador.</span><span class="sxs-lookup"><span data-stu-id="f2cca-111">It is important toounderstand that hello Service Fabric local cluster is not an emulator or simulator.</span></span> <span data-ttu-id="f2cca-112">Ele é executado Olá mesmo código de plataforma que é encontrado em clusters com vários computadores.</span><span class="sxs-lookup"><span data-stu-id="f2cca-112">It runs hello same platform code that is found on multi-machine clusters.</span></span> <span data-ttu-id="f2cca-113">Olá única diferença é que ele seja executado processos de plataforma de saudação que normalmente estão espalhados em cinco máquinas em um computador.</span><span class="sxs-lookup"><span data-stu-id="f2cca-113">hello only difference is that it runs hello platform processes that are normally spread across five machines on one machine.</span></span>

<span data-ttu-id="f2cca-114">Olá SDK fornece dois tooset maneiras um cluster local: do Windows PowerShell script e hello Gerenciador de Cluster Local system bandeja aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f2cca-114">hello SDK provides two ways tooset up a local cluster: a Windows PowerShell script and hello Local Cluster Manager system tray app.</span></span> <span data-ttu-id="f2cca-115">Neste tutorial, usamos o script do PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="f2cca-115">In this tutorial, we use hello PowerShell script.</span></span>

> [!NOTE]
> <span data-ttu-id="f2cca-116">Se você já tiver criado um cluster local ao implantar um aplicativo do Visual Studio, poderá ignorar esta seção.</span><span class="sxs-lookup"><span data-stu-id="f2cca-116">If you have already created a local cluster by deploying an application from Visual Studio, you can skip this section.</span></span>
> 
> 

1. <span data-ttu-id="f2cca-117">Inicie uma nova janela do PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="f2cca-117">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="f2cca-118">Execute o script de instalação de cluster de saudação da pasta de saudação do SDK:</span><span class="sxs-lookup"><span data-stu-id="f2cca-118">Run hello cluster setup script from hello SDK folder:</span></span>
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"
    ```
   
    <span data-ttu-id="f2cca-119">A instalação do cluster leva alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="f2cca-119">Cluster setup takes a few moments.</span></span> <span data-ttu-id="f2cca-120">Após a conclusão da instalação, você verá uma saída como esta:</span><span class="sxs-lookup"><span data-stu-id="f2cca-120">After setup is finished, you should see output similar to:</span></span>
   
    ![Saída da instalação do cluster][cluster-setup-success]
   
    <span data-ttu-id="f2cca-122">Agora você está pronto tootry Implantando um cluster de tooyour do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f2cca-122">You are now ready tootry deploying an application tooyour cluster.</span></span>

## <a name="deploy-an-application"></a><span data-ttu-id="f2cca-123">Implantar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="f2cca-123">Deploy an application</span></span>
<span data-ttu-id="f2cca-124">Olá SDK do Service Fabric inclui um conjunto avançado de estruturas e ferramentas para criar aplicativos de desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="f2cca-124">hello Service Fabric SDK includes a rich set of frameworks and developer tooling for creating applications.</span></span> <span data-ttu-id="f2cca-125">Se você estiver interessado em saber mais sobre como toocreate aplicativos no Visual Studio, consulte [criar seu primeiro aplicativo de malha do serviço no Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="f2cca-125">If you are interested in learning how toocreate applications in Visual Studio, see [Create your first Service Fabric application in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span></span>

<span data-ttu-id="f2cca-126">Neste tutorial, você usar um aplicativo de exemplo existente (chamado WordCount) para que você possa se concentrar em aspectos do gerenciamento de saudação da plataforma Olá: implantação, monitoramento e atualização.</span><span class="sxs-lookup"><span data-stu-id="f2cca-126">In this tutorial, you use an existing sample application (called WordCount) so that you can focus on hello management aspects of hello platform: deployment, monitoring, and upgrade.</span></span>

1. <span data-ttu-id="f2cca-127">Inicie uma nova janela do PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="f2cca-127">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="f2cca-128">Importar o módulo do PowerShell do SDK do Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="f2cca-128">Import hello Service Fabric SDK PowerShell module.</span></span>
   
    ```powershell
    Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
    ```
3. <span data-ttu-id="f2cca-129">Crie um aplicativo hello toostore de diretório que você baixar e implanta, como C:\ServiceFabric.</span><span class="sxs-lookup"><span data-stu-id="f2cca-129">Create a directory toostore hello application that you download and deploy, such as C:\ServiceFabric.</span></span>
   
    ```powershell
    mkdir c:\ServiceFabric\
    cd c:\ServiceFabric\
    ```
4. <span data-ttu-id="f2cca-130">[Baixe o aplicativo de WordCount hello](http://aka.ms/servicefabric-wordcountapp) toohello local criado por você.</span><span class="sxs-lookup"><span data-stu-id="f2cca-130">[Download hello WordCount application](http://aka.ms/servicefabric-wordcountapp) toohello location you created.</span></span>  <span data-ttu-id="f2cca-131">Observação: o navegador Microsoft Edge de saudação salva o arquivo de saudação com um *. zip* extensão.</span><span class="sxs-lookup"><span data-stu-id="f2cca-131">Note: hello Microsoft Edge browser saves hello file with a *.zip* extension.</span></span>  <span data-ttu-id="f2cca-132">Alterar a extensão de arquivo hello muito*.sfpkg*.</span><span class="sxs-lookup"><span data-stu-id="f2cca-132">Change hello file extension too*.sfpkg*.</span></span>
5. <span data-ttu-id="f2cca-133">Conecte o cluster local toohello:</span><span class="sxs-lookup"><span data-stu-id="f2cca-133">Connect toohello local cluster:</span></span>
   
    ```powershell
    Connect-ServiceFabricCluster localhost:19000
    ```
6. <span data-ttu-id="f2cca-134">Crie um novo aplicativo usando o comando de implantação de saudação do SDK com um nome e um pacote de aplicativo de toohello de caminho.</span><span class="sxs-lookup"><span data-stu-id="f2cca-134">Create a new application using hello SDK's deployment command with a name and a path toohello application package.</span></span>
   
    ```powershell  
   Publish-NewServiceFabricApplication -ApplicationPackagePath c:\ServiceFabric\WordCountV1.sfpkg -ApplicationName "fabric:/WordCount"
    ```
   
    <span data-ttu-id="f2cca-135">Se tudo correr bem, você deverá ver Olá saída a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2cca-135">If all goes well, you should see hello following output:</span></span>
   
    ![Implantar um cluster local do aplicativo toohello][deploy-app-to-local-cluster]
7. <span data-ttu-id="f2cca-137">aplicativo de hello toosee em ação, inicie o navegador hello e navegue muito[http://localhost:8081/wordcount/index.html](http://localhost:8081/wordcount/index.html).</span><span class="sxs-lookup"><span data-stu-id="f2cca-137">toosee hello application in action, launch hello browser and navigate too[http://localhost:8081/wordcount/index.html](http://localhost:8081/wordcount/index.html).</span></span> <span data-ttu-id="f2cca-138">Você deverá ver:</span><span class="sxs-lookup"><span data-stu-id="f2cca-138">You should see:</span></span>
   
    ![IU do aplicativo implantado][deployed-app-ui]
   
    <span data-ttu-id="f2cca-140">Olá aplicativo WordCount é simple.</span><span class="sxs-lookup"><span data-stu-id="f2cca-140">hello WordCount application is simple.</span></span> <span data-ttu-id="f2cca-141">Ele inclui o cliente JavaScript código toogenerate aleatória cinco caracteres "palavras", que são retransmitidas toohello aplicativo por meio da API Web do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="f2cca-141">It includes client-side JavaScript code toogenerate random five-character "words", which are then relayed toohello application via ASP.NET Web API.</span></span> <span data-ttu-id="f2cca-142">Um serviço com monitoração de estado rastreia o número de saudação de palavras contados.</span><span class="sxs-lookup"><span data-stu-id="f2cca-142">A stateful service tracks hello number of words counted.</span></span> <span data-ttu-id="f2cca-143">Eles serão particionados com base no primeiro o caractere de palavra Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="f2cca-143">They are partitioned based on hello first character of hello word.</span></span> <span data-ttu-id="f2cca-144">Você pode encontrar o código-fonte Olá para o aplicativo WordCount Olá Olá [clássico Introdução exemplos](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).</span><span class="sxs-lookup"><span data-stu-id="f2cca-144">You can find hello source code for hello WordCount app in hello [classic getting started samples](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount).</span></span>
   
    <span data-ttu-id="f2cca-145">aplicativo de Hello implantamos contém quatro partições.</span><span class="sxs-lookup"><span data-stu-id="f2cca-145">hello application that we deployed contains four partitions.</span></span> <span data-ttu-id="f2cca-146">Portanto palavras que começam com À G são armazenadas na primeira partição do hello, palavras que começam com H até N são armazenadas na segunda partição de saudação e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="f2cca-146">So words beginning with A through G are stored in hello first partition, words beginning with H through N are stored in hello second partition, and so on.</span></span>

## <a name="view-application-details-and-status"></a><span data-ttu-id="f2cca-147">Exibir detalhes e o status do aplicativo</span><span class="sxs-lookup"><span data-stu-id="f2cca-147">View application details and status</span></span>
<span data-ttu-id="f2cca-148">Agora que estamos implantou o aplicativo hello, vamos examinar alguns dos detalhes do aplicativo hello no PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f2cca-148">Now that we have deployed hello application, let's look at some of hello app details in PowerShell.</span></span>

1. <span data-ttu-id="f2cca-149">Consulta implantados todos os aplicativos em cluster hello:</span><span class="sxs-lookup"><span data-stu-id="f2cca-149">Query all deployed applications on hello cluster:</span></span>
   
    ```powershell
    Get-ServiceFabricApplication
    ```
   
    <span data-ttu-id="f2cca-150">Supondo que você implantou apenas Olá WordCount aplicativo, você verá algo semelhante a:</span><span class="sxs-lookup"><span data-stu-id="f2cca-150">Assuming that you have only deployed hello WordCount app, you see something similar to:</span></span>
   
    ![Consultar todos os aplicativos implantados no PowerShell][ps-getsfapp]
2. <span data-ttu-id="f2cca-152">Vá toohello próximo nível consultando o conjunto de saudação de serviços que são incluídos no aplicativo de WordCount hello.</span><span class="sxs-lookup"><span data-stu-id="f2cca-152">Go toohello next level by querying hello set of services that are included in hello WordCount application.</span></span>
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Lista de serviços para o aplicativo hello no PowerShell][ps-getsfsvc]
   
    <span data-ttu-id="f2cca-154">aplicativo Hello é composto de dois serviços, Olá web front-end e serviço de monitoração de estado de saudação que gerencia palavras Olá.</span><span class="sxs-lookup"><span data-stu-id="f2cca-154">hello application is made up of two services, hello web front end, and hello stateful service that manages hello words.</span></span>
3. <span data-ttu-id="f2cca-155">Por fim, examine a lista Olá de partições para WordCountService:</span><span class="sxs-lookup"><span data-stu-id="f2cca-155">Finally, look at hello list of partitions for WordCountService:</span></span>
   
    ```powershell
    Get-ServiceFabricPartition 'fabric:/WordCount/WordCountService'
    ```
   
    ![Exibir hello serviço partições no PowerShell][ps-getsfpartitions]
   
    <span data-ttu-id="f2cca-157">Olá conjunto de comandos que você usou, como todos os comandos do PowerShell de malha do serviço, estão disponíveis para qualquer cluster que você pode se conectar ao local ou remoto.</span><span class="sxs-lookup"><span data-stu-id="f2cca-157">hello set of commands that you used, like all Service Fabric PowerShell commands, are available for any cluster that you might connect to, local or remote.</span></span>
   
    <span data-ttu-id="f2cca-158">Para um toointeract de maneira mais visual com cluster hello, você pode usar Olá web Service Fabric Explorer ferramenta navegando muito[http://localhost:19080/Explorer](http://localhost:19080/Explorer) no navegador de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2cca-158">For a more visual way toointeract with hello cluster, you can use hello web-based Service Fabric Explorer tool by navigating too[http://localhost:19080/Explorer](http://localhost:19080/Explorer) in hello browser.</span></span>
   
    ![Exibir detalhes do aplicativo no Service Fabric Explorer][sfx-service-overview]
   
   > [!NOTE]
   > <span data-ttu-id="f2cca-160">toolearn mais sobre o Service Fabric Explorer, consulte [visualizar seu cluster com o Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="f2cca-160">toolearn more about Service Fabric Explorer, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
   > 
   > 

## <a name="upgrade-an-application"></a><span data-ttu-id="f2cca-161">Atualizar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="f2cca-161">Upgrade an application</span></span>
<span data-ttu-id="f2cca-162">Service Fabric fornece atualizações nenhum tempo de inatividade, monitorando a integridade de saudação do aplicativo hello conforme ele lança cluster hello.</span><span class="sxs-lookup"><span data-stu-id="f2cca-162">Service Fabric provides no-downtime upgrades by monitoring hello health of hello application as it rolls out across hello cluster.</span></span> <span data-ttu-id="f2cca-163">Execute uma atualização do aplicativo WordCount do hello.</span><span class="sxs-lookup"><span data-stu-id="f2cca-163">Perform an upgrade of hello WordCount application.</span></span>

<span data-ttu-id="f2cca-164">nova versão de saudação do aplicativo hello agora conta apenas as palavras que começam com uma vogal.</span><span class="sxs-lookup"><span data-stu-id="f2cca-164">hello new version of hello application now counts only words that begin with a vowel.</span></span> <span data-ttu-id="f2cca-165">Atualização de saudação distribui, vemos duas alterações no comportamento do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="f2cca-165">As hello upgrade rolls out, we see two changes in hello application's behavior.</span></span> <span data-ttu-id="f2cca-166">Primeiro, taxa de saudação em que a contagem de saudação cresce deve lenta, já que menos palavras são contadas.</span><span class="sxs-lookup"><span data-stu-id="f2cca-166">First, hello rate at which hello count grows should slow, since fewer words are being counted.</span></span> <span data-ttu-id="f2cca-167">Em segundo lugar, como partição primeiro Olá tem dois vogais (A e E) e todas as outras partições contêm somente um, sua contagem deve eventualmente iniciar toooutpace Olá outras pessoas.</span><span class="sxs-lookup"><span data-stu-id="f2cca-167">Second, since hello first partition has two vowels (A and E) and all other partitions contain only one each, its count should eventually start toooutpace hello others.</span></span>

1. <span data-ttu-id="f2cca-168">[Baixe o pacote da versão 2 do hello WordCount](http://aka.ms/servicefabric-wordcountappv2) toohello mesmo local onde você baixou o pacote de versão 1 hello.</span><span class="sxs-lookup"><span data-stu-id="f2cca-168">[Download hello WordCount version 2 package](http://aka.ms/servicefabric-wordcountappv2) toohello same location where you downloaded hello version 1 package.</span></span>
2. <span data-ttu-id="f2cca-169">Retornar tooyour janela do PowerShell e use o comando upgrade de saudação do SDK tooregister Olá nova versão em cluster hello.</span><span class="sxs-lookup"><span data-stu-id="f2cca-169">Return tooyour PowerShell window and use hello SDK's upgrade command tooregister hello new version in hello cluster.</span></span> <span data-ttu-id="f2cca-170">Começar a atualizar malha Olá: / aplicativo WordCount.</span><span class="sxs-lookup"><span data-stu-id="f2cca-170">Then begin upgrading hello fabric:/WordCount application.</span></span>
   
    ```powershell
    Publish-UpgradedServiceFabricApplication -ApplicationPackagePath C:\ServiceFabric\WordCountV2.sfpkg -ApplicationName "fabric:/WordCount" -UpgradeParameters @{"FailureAction"="Rollback"; "UpgradeReplicaSetCheckTimeout"=1; "Monitored"=$true; "Force"=$true}
    ```
   
    <span data-ttu-id="f2cca-171">Você deve ver a saída no PowerShell Olá atualização a seguir Olá começa.</span><span class="sxs-lookup"><span data-stu-id="f2cca-171">You should see hello following output in PowerShell as hello upgrade begins.</span></span>
   
    ![Andamento da atualização no PowerShell][ps-appupgradeprogress]
3. <span data-ttu-id="f2cca-173">Enquanto a atualização Olá é continuar, talvez seja mais fácil toomonitor o status do Gerenciador do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f2cca-173">While hello upgrade is proceeding, you may find it easier toomonitor its status from Service Fabric Explorer.</span></span> <span data-ttu-id="f2cca-174">Inicie uma janela do navegador e navegue muito[http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="f2cca-174">Launch a browser window and navigate too[http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="f2cca-175">Expanda **aplicativos** na árvore de Olá Olá esquerda, escolha **WordCount**e, finalmente, **fabric: / WordCount**.</span><span class="sxs-lookup"><span data-stu-id="f2cca-175">Expand **Applications** in hello tree on hello left, then choose **WordCount**, and finally **fabric:/WordCount**.</span></span> <span data-ttu-id="f2cca-176">Na guia do essentials Olá, você deve ver um status de saudação da atualização de saudação conforme ele passa os domínios de atualização do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="f2cca-176">In hello essentials tab, you see hello status of hello upgrade as it proceeds through hello cluster's upgrade domains.</span></span>
   
    ![Andamento da atualização no Service Fabric Explorer][sfx-upgradeprogress]
   
    <span data-ttu-id="f2cca-178">Como atualização Olá continua por meio de cada domínio, verificações de integridade são realizada tooensure que o aplicativo hello está se comportando corretamente.</span><span class="sxs-lookup"><span data-stu-id="f2cca-178">As hello upgrade proceeds through each domain, health checks are performed tooensure that hello application is behaving properly.</span></span>
4. <span data-ttu-id="f2cca-179">Se você executar novamente a saudação anterior de consulta para conjunto de saudação de serviços na malha Olá: / aplicativo WordCount, observe que Olá WordCountService versão alterada mas Olá WordCountWebService versão não:</span><span class="sxs-lookup"><span data-stu-id="f2cca-179">If you rerun hello earlier query for hello set of services in hello fabric:/WordCount application, notice that hello WordCountService version changed but hello WordCountWebService version did not:</span></span>
   
    ```powershell
    Get-ServiceFabricService -ApplicationName 'fabric:/WordCount'
    ```
   
    ![Consultar serviços de aplicativos após a atualização][ps-getsfsvc-postupgrade]
   
    <span data-ttu-id="f2cca-181">Este exemplo destaca como o Service Fabric gerencia atualizações de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f2cca-181">This example highlights how Service Fabric manages application upgrades.</span></span> <span data-ttu-id="f2cca-182">Ele envolve apenas Olá conjunto de serviços (ou pacotes de código/configuração nesses serviços) que foram alterados, que torna o processo de saudação de atualização mais rápida e confiável.</span><span class="sxs-lookup"><span data-stu-id="f2cca-182">It touches only hello set of services (or code/configuration packages within those services) that have changed, which makes hello process of upgrading faster and more reliable.</span></span>
5. <span data-ttu-id="f2cca-183">Finalmente, retorne o comportamento da saudação tooobserve toohello navegador da nova versão do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="f2cca-183">Finally, return toohello browser tooobserve hello behavior of hello new application version.</span></span> <span data-ttu-id="f2cca-184">Conforme o esperado, Olá contagem progride mais lentamente e Olá primeira partição acaba com um pouco mais de volume hello.</span><span class="sxs-lookup"><span data-stu-id="f2cca-184">As expected, hello count progresses more slowly, and hello first partition ends up with slightly more of hello volume.</span></span>
   
    ![Exibição Olá nova versão do aplicativo hello no navegador Olá][deployed-app-ui-v2]

## <a name="cleaning-up"></a><span data-ttu-id="f2cca-186">Limpando</span><span class="sxs-lookup"><span data-stu-id="f2cca-186">Cleaning up</span></span>
<span data-ttu-id="f2cca-187">Antes de encapsular o, é importante tooremember que Olá cluster local é real.</span><span class="sxs-lookup"><span data-stu-id="f2cca-187">Before wrapping up, it's important tooremember that hello local cluster is real.</span></span> <span data-ttu-id="f2cca-188">Aplicativos continuam toorun no plano de fundo Olá até você removê-los.</span><span class="sxs-lookup"><span data-stu-id="f2cca-188">Applications continue toorun in hello background until you remove them.</span></span>  <span data-ttu-id="f2cca-189">Dependendo da natureza da saudação de seus aplicativos, um aplicativo em execução pode consomem recursos significativos em seu computador.</span><span class="sxs-lookup"><span data-stu-id="f2cca-189">Depending on hello nature of your apps, a running app can take up significant resources on your machine.</span></span> <span data-ttu-id="f2cca-190">Você tem vários aplicativos de toomanage de opções e cluster hello:</span><span class="sxs-lookup"><span data-stu-id="f2cca-190">You have several options toomanage applications and hello cluster:</span></span>

1. <span data-ttu-id="f2cca-191">tooremove um aplicativo individual e todos os-lo da dados, execute o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="f2cca-191">tooremove an individual application and all it's data, run hello following command:</span></span>
   
    ```powershell
    Unpublish-ServiceFabricApplication -ApplicationName "fabric:/WordCount"
    ```
   
    <span data-ttu-id="f2cca-192">Ou exclua o aplicativo hello do hello Service Fabric Explorer **ações** menu ou menu de contexto de saudação na exibição de lista do aplicativo esquerdo hello.</span><span class="sxs-lookup"><span data-stu-id="f2cca-192">Or, delete hello application from hello Service Fabric Explorer **ACTIONS** menu or hello context menu in hello left-hand application list view.</span></span>
   
    ![Excluir um aplicativo no Service Fabric Explorer][sfe-delete-application]
2. <span data-ttu-id="f2cca-194">Depois de excluir o aplicativo hello do cluster hello, cancele o registro versões 1.0.0 e 2.0.0 de saudação WordCount tipo de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f2cca-194">After deleting hello application from hello cluster, unregister versions 1.0.0 and 2.0.0 of hello WordCount application type.</span></span> <span data-ttu-id="f2cca-195">A exclusão remove os pacotes de aplicativos hello, incluindo código hello e configuração do cluster de saudação repositório de imagens.</span><span class="sxs-lookup"><span data-stu-id="f2cca-195">Deletion removes hello application packages, including hello code and configuration, from hello cluster's image store.</span></span>
   
    ```powershell
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 2.0.0
    Remove-ServiceFabricApplicationType -ApplicationTypeName WordCount -ApplicationTypeVersion 1.0.0
    ```
   
    <span data-ttu-id="f2cca-196">Ou, no Gerenciador do Service Fabric, escolha **desconfiguração tipo** para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="f2cca-196">Or, in Service Fabric Explorer, choose **Unprovision Type** for hello application.</span></span>
3. <span data-ttu-id="f2cca-197">tooshut cluster hello, mas manter os dados aplicativo hello e rastreamentos, clique em **parar Cluster Local** no aplicativo de bandeja do sistema hello.</span><span class="sxs-lookup"><span data-stu-id="f2cca-197">tooshut down hello cluster but keep hello application data and traces, click **Stop Local Cluster** in hello system tray app.</span></span>
4. <span data-ttu-id="f2cca-198">cluster de saudação toodelete totalmente, clique em **remover Cluster Local** no aplicativo de bandeja do sistema hello.</span><span class="sxs-lookup"><span data-stu-id="f2cca-198">toodelete hello cluster entirely, click **Remove Local Cluster** in hello system tray app.</span></span> <span data-ttu-id="f2cca-199">Essa opção resultará em outro Olá de implantação lenta próxima vez que você pressionar F5 no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f2cca-199">This option will result in another slow deployment hello next time you press F5 in Visual Studio.</span></span> <span data-ttu-id="f2cca-200">Remova cluster local Olá somente se você não pretende toouse-lo por algum tempo ou se você precisa de recursos de tooreclaim.</span><span class="sxs-lookup"><span data-stu-id="f2cca-200">Remove hello local cluster only if you don't intend toouse it for some time or if you need tooreclaim resources.</span></span>

## <a name="one-node-and-five-node-cluster-mode"></a><span data-ttu-id="f2cca-201">Modo de um nó e de cinco nós do cluster</span><span class="sxs-lookup"><span data-stu-id="f2cca-201">One-node and five-node cluster mode</span></span>
<span data-ttu-id="f2cca-202">Ao desenvolver aplicativos, você geralmente acaba fazendo iterações rápidas entre a produção do código, depuração, alteração do código e depuração.</span><span class="sxs-lookup"><span data-stu-id="f2cca-202">When developing applications, you often find yourself doing quick iterations of writing code, debugging, changing code, and debugging.</span></span> <span data-ttu-id="f2cca-203">toohelp otimizar esse processo, o cluster local Olá pode ser executado em dois modos: um nó ou cinco nós.</span><span class="sxs-lookup"><span data-stu-id="f2cca-203">toohelp optimize this process, hello local cluster can run in two modes: one-node or five-node.</span></span> <span data-ttu-id="f2cca-204">Os dois modos de cluster têm seus benefícios.</span><span class="sxs-lookup"><span data-stu-id="f2cca-204">Both cluster modes have their benefits.</span></span> <span data-ttu-id="f2cca-205">Modo de cinco nós de cluster permite que você toowork com um cluster real.</span><span class="sxs-lookup"><span data-stu-id="f2cca-205">Five-node cluster mode enables you toowork with a real cluster.</span></span> <span data-ttu-id="f2cca-206">Você pode testar os cenários de failover, trabalhar com mais instâncias e réplicas de seus serviços.</span><span class="sxs-lookup"><span data-stu-id="f2cca-206">You can test failover scenarios, work with more instances and replicas of your services.</span></span> <span data-ttu-id="f2cca-207">Modo de cluster de um nó é otimizada toodo rápida implantação e o registro de serviços, toohelp você valida o código usando o tempo de execução do Service Fabric Olá rapidamente.</span><span class="sxs-lookup"><span data-stu-id="f2cca-207">One-node cluster mode is optimized toodo quick deployment and registration of services, toohelp you quickly validate code using hello Service Fabric runtime.</span></span>

<span data-ttu-id="f2cca-208">Tanto o modo de um nó como o de cinco nós do cluster não são um emulador ou simulador.</span><span class="sxs-lookup"><span data-stu-id="f2cca-208">Neither one-node cluster or five-node cluster modes are an emulator or simulator.</span></span> <span data-ttu-id="f2cca-209">cluster de desenvolvimento local Olá executa Olá mesmo código de plataforma que é encontrado em clusters com vários computadores.</span><span class="sxs-lookup"><span data-stu-id="f2cca-209">hello local development cluster runs hello same platform code that is found on multi-machine clusters.</span></span>

> [!WARNING]
> <span data-ttu-id="f2cca-210">Quando você altera o modo de saudação do cluster, o cluster atual Olá é removido do seu sistema e um novo cluster é criado.</span><span class="sxs-lookup"><span data-stu-id="f2cca-210">When you change hello cluster mode, hello current cluster is removed from your system and a new cluster is created.</span></span> <span data-ttu-id="f2cca-211">dados de saudação armazenados em cluster Olá são excluídos quando você altera o modo de cluster.</span><span class="sxs-lookup"><span data-stu-id="f2cca-211">hello data stored in hello cluster is deleted when you change cluster mode.</span></span>
> 
> 

<span data-ttu-id="f2cca-212">toochange Olá modo tooone cluster de nó, selecione **alterne o modo de Cluster** no hello Gerenciador de Cluster de Local do serviço de malha.</span><span class="sxs-lookup"><span data-stu-id="f2cca-212">toochange hello mode tooone-node cluster, select **Switch Cluster Mode** in hello Service Fabric Local Cluster Manager.</span></span>

![Alternar o modo de cluster][switch-cluster-mode]

<span data-ttu-id="f2cca-214">Ou então, alterar o modo de saudação do cluster usando o PowerShell:</span><span class="sxs-lookup"><span data-stu-id="f2cca-214">Or, change hello cluster mode using PowerShell:</span></span>

1. <span data-ttu-id="f2cca-215">Inicie uma nova janela do PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="f2cca-215">Launch a new PowerShell window as an administrator.</span></span>
2. <span data-ttu-id="f2cca-216">Execute o script de instalação de cluster de saudação da pasta de saudação do SDK:</span><span class="sxs-lookup"><span data-stu-id="f2cca-216">Run hello cluster setup script from hello SDK folder:</span></span>
   
    ```powershell
    & "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1" -CreateOneNodeCluster
    ```
   
    <span data-ttu-id="f2cca-217">A instalação do cluster leva alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="f2cca-217">Cluster setup takes a few moments.</span></span> <span data-ttu-id="f2cca-218">Após a conclusão da instalação, você verá uma saída como esta:</span><span class="sxs-lookup"><span data-stu-id="f2cca-218">After setup is finished, you should see output similar to:</span></span>
   
    ![Saída da instalação do cluster][cluster-setup-success-1-node]

## <a name="next-steps"></a><span data-ttu-id="f2cca-220">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f2cca-220">Next steps</span></span>
* <span data-ttu-id="f2cca-221">Agora que você implantou e atualizou alguns aplicativos pré-compilados, poderá [tentar compilar seu próprio aplicativo no Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="f2cca-221">Now that you have deployed and upgraded some pre-built applications, you can [try building your own in Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md).</span></span>
* <span data-ttu-id="f2cca-222">Todas as ações de saudação executadas no cluster local do hello neste artigo podem ser executadas em um [cluster do Azure](service-fabric-cluster-creation-via-portal.md) também.</span><span class="sxs-lookup"><span data-stu-id="f2cca-222">All hello actions performed on hello local cluster in this article can be performed on an [Azure cluster](service-fabric-cluster-creation-via-portal.md) as well.</span></span>
* <span data-ttu-id="f2cca-223">atualização de saudação que realizamos neste artigo foi básico.</span><span class="sxs-lookup"><span data-stu-id="f2cca-223">hello upgrade that we performed in this article was basic.</span></span> <span data-ttu-id="f2cca-224">Consulte Olá [documentação de atualização](service-fabric-application-upgrade.md) toolearn mais sobre o power hello e flexibilidade de atualizações de malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="f2cca-224">See hello [upgrade documentation](service-fabric-application-upgrade.md) toolearn more about hello power and flexibility of Service Fabric upgrades.</span></span>

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
