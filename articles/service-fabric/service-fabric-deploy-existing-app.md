---
title: "aaaDeploy um tooAzure executável existente do Service Fabric | Microsoft Docs"
description: "Passo a passo sobre como toopackage um aplicativo existente como um executável de convidado, para que ele possa ser implantado cluster do Service Fabric tooa"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: d799c1c6-75eb-4b8a-9f94-bf4f3dadf4c3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 07/02/2017
ms.author: mfussell;mikhegn
ms.openlocfilehash: 5599802bdb6bda2407a138d77e12148ccb64f437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-guest-executable-tooservice-fabric"></a><span data-ttu-id="132be-103">Implantar um tooService executável de convidado malha</span><span class="sxs-lookup"><span data-stu-id="132be-103">Deploy a guest executable tooService Fabric</span></span>
<span data-ttu-id="132be-104">Você pode executar qualquer tipo de código, como Node.js, Java ou C++ no Service Fabric como um serviço.</span><span class="sxs-lookup"><span data-stu-id="132be-104">You can run any type of code, such as Node.js, Java, or C++ in Azure Service Fabric as a service.</span></span> <span data-ttu-id="132be-105">Service Fabric se refere a tipos de toothese de serviços como convidado executáveis.</span><span class="sxs-lookup"><span data-stu-id="132be-105">Service Fabric refers toothese types of services as guest executables.</span></span>

<span data-ttu-id="132be-106">Os executáveis convidados são tratados pela Service Fabric como serviços sem monitoração de estado.</span><span class="sxs-lookup"><span data-stu-id="132be-106">Guest executables are treated by Service Fabric like stateless services.</span></span> <span data-ttu-id="132be-107">Como resultado, eles são colocados em nós em um cluster, com base na disponibilidade e em outras métricas.</span><span class="sxs-lookup"><span data-stu-id="132be-107">As a result, they are placed on nodes in a cluster, based on availability and other metrics.</span></span> <span data-ttu-id="132be-108">Este artigo descreve como toopackage e implantar um cluster de malha do serviço de tooa executável de convidado, usando o Visual Studio ou um utilitário de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="132be-108">This article describes how toopackage and deploy a guest executable tooa Service Fabric cluster, by using Visual Studio or a command-line utility.</span></span>

<span data-ttu-id="132be-109">Neste artigo, vamos abranger Olá etapas toopackage um executável de convidado e implantá-lo tooService malha.</span><span class="sxs-lookup"><span data-stu-id="132be-109">In this article, we cover hello steps toopackage a guest executable and deploy it tooService Fabric.</span></span>  

## <a name="benefits-of-running-a-guest-executable-in-service-fabric"></a><span data-ttu-id="132be-110">Benefícios de executar um executável convidado no Service Fabric</span><span class="sxs-lookup"><span data-stu-id="132be-110">Benefits of running a guest executable in Service Fabric</span></span>
<span data-ttu-id="132be-111">Há várias toorunning de vantagens convidado executável em um cluster do Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="132be-111">There are several advantages toorunning a guest executable in a Service Fabric cluster:</span></span>

* <span data-ttu-id="132be-112">Alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="132be-112">High availability.</span></span> <span data-ttu-id="132be-113">Os aplicativos que são executados no Service Fabric estão no modo de alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="132be-113">Applications that run in Service Fabric are made highly available.</span></span> <span data-ttu-id="132be-114">O Service Fabric garante que as instâncias de um aplicativo estão em execução.</span><span class="sxs-lookup"><span data-stu-id="132be-114">Service Fabric ensures that instances of an application are running.</span></span>
* <span data-ttu-id="132be-115">Monitoramento de integridade.</span><span class="sxs-lookup"><span data-stu-id="132be-115">Health monitoring.</span></span> <span data-ttu-id="132be-116">O monitoramento de integridade do Service Fabric detecta se um aplicativo está em execução e fornece informações de diagnóstico se houver uma falha.</span><span class="sxs-lookup"><span data-stu-id="132be-116">Service Fabric health monitoring detects if an application is running, and provides diagnostic information if there is a failure.</span></span>   
* <span data-ttu-id="132be-117">Gerenciamento do ciclo de vida do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="132be-117">Application lifecycle management.</span></span> <span data-ttu-id="132be-118">Além de fornecer atualizações sem tempo de inatividade, o Service Fabric fornece versão anterior do toohello de reversão automática se houver um evento de integridade inválido relatado durante uma atualização.</span><span class="sxs-lookup"><span data-stu-id="132be-118">Besides providing upgrades with no downtime, Service Fabric provides automatic rollback toohello previous version if there is a bad health event reported during an upgrade.</span></span>    
* <span data-ttu-id="132be-119">Densidade.</span><span class="sxs-lookup"><span data-stu-id="132be-119">Density.</span></span> <span data-ttu-id="132be-120">Você pode executar vários aplicativos em um cluster, o que elimina a necessidade de saudação de toorun cada aplicativo em seu próprio hardware.</span><span class="sxs-lookup"><span data-stu-id="132be-120">You can run multiple applications in a cluster, which eliminates hello need for each application toorun on its own hardware.</span></span>
* <span data-ttu-id="132be-121">Descoberta: Usando REST você pode chamar toofind de serviço de nomeação de malha do serviço Olá outros serviços em cluster hello.</span><span class="sxs-lookup"><span data-stu-id="132be-121">Discoverability: Using REST you can call hello Service Fabric Naming service toofind other services in hello cluster.</span></span> 

## <a name="samples"></a><span data-ttu-id="132be-122">Exemplos</span><span class="sxs-lookup"><span data-stu-id="132be-122">Samples</span></span>
* [<span data-ttu-id="132be-123">Exemplo de empacotamento e implantação de um executável convidado</span><span class="sxs-lookup"><span data-stu-id="132be-123">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="132be-124">Exemplo de dois convidado executáveis (c# e nodejs) se comunicar por meio do serviço de nomenclatura hello usando REST</span><span class="sxs-lookup"><span data-stu-id="132be-124">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="overview-of-application-and-service-manifest-files"></a><span data-ttu-id="132be-125">Visão geral do aplicativo e dos arquivos de manifesto do serviço</span><span class="sxs-lookup"><span data-stu-id="132be-125">Overview of application and service manifest files</span></span>
<span data-ttu-id="132be-126">Como parte da implantação de um executável de convidado, é útil toounderstand Olá Service Fabric modelo de pacotes e implantação conforme descrito em [modelo de aplicativo](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="132be-126">As part of deploying a guest executable, it is useful toounderstand hello Service Fabric packaging and deployment model as described in [application model](service-fabric-application-model.md).</span></span> <span data-ttu-id="132be-127">modelo de empacotamento do Service Fabric Olá se baseia em dois arquivos XML: Olá manifestos de aplicativo e serviço.</span><span class="sxs-lookup"><span data-stu-id="132be-127">hello Service Fabric packaging model relies on two XML files: hello application and service manifests.</span></span> <span data-ttu-id="132be-128">Olá definição de esquema para hello arquivos ApplicationManifest.xml e ServiceManifest.xml é instalado com hello no SDK do Service Fabric *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="132be-128">hello schema definition for hello ApplicationManifest.xml and ServiceManifest.xml files is installed with hello Service Fabric SDK into *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

* <span data-ttu-id="132be-129">**O manifesto do aplicativo** o manifesto do aplicativo hello é usado toodescribe Olá aplicativo.</span><span class="sxs-lookup"><span data-stu-id="132be-129">**Application manifest** hello application manifest is used toodescribe hello application.</span></span> <span data-ttu-id="132be-130">Lista serviços Olá que compõem a ele e outros parâmetros que são usado toodefine devem ser implantados como um ou mais serviços, como número de saudação de instâncias.</span><span class="sxs-lookup"><span data-stu-id="132be-130">It lists hello services that compose it, and other parameters that are used toodefine how one or more services should be deployed, such as hello number of instances.</span></span>

  <span data-ttu-id="132be-131">No Service Fabric, um aplicativo é uma unidade de implantação e atualização.</span><span class="sxs-lookup"><span data-stu-id="132be-131">In Service Fabric, an application is a unit of deployment and upgrade.</span></span> <span data-ttu-id="132be-132">Um aplicativo pode ser atualizado como uma única unidade em que falhas e reversões potencias são gerenciadas.</span><span class="sxs-lookup"><span data-stu-id="132be-132">An application can be upgraded as a single unit where potential failures and potential rollbacks are managed.</span></span> <span data-ttu-id="132be-133">Service Fabric garante que o processo de atualização Olá seja bem-sucedida, ou se Olá atualização falhar, não deixe aplicativo hello em um estado instável ou desconhecido.</span><span class="sxs-lookup"><span data-stu-id="132be-133">Service Fabric guarantees that hello upgrade process is either successful, or, if hello upgrade fails, does not leave hello application in an unknown or unstable state.</span></span>
* <span data-ttu-id="132be-134">**Manifesto do serviço** manifesto do serviço Olá descreve os componentes de saudação de um serviço.</span><span class="sxs-lookup"><span data-stu-id="132be-134">**Service manifest** hello service manifest describes hello components of a service.</span></span> <span data-ttu-id="132be-135">Ele inclui dados, como nome de saudação e tipo de serviço e seu código e configuração.</span><span class="sxs-lookup"><span data-stu-id="132be-135">It includes data, such as hello name and type of service, and its code and configuration.</span></span> <span data-ttu-id="132be-136">Olá manifesto de serviço também inclui alguns parâmetros adicionais que podem ser usados tooconfigure serviço de saudação quando ele é implantado.</span><span class="sxs-lookup"><span data-stu-id="132be-136">hello service manifest also includes some additional parameters that can be used tooconfigure hello service once it is deployed.</span></span>

## <a name="application-package-file-structure"></a><span data-ttu-id="132be-137">Estrutura de arquivos do pacote de aplicativos</span><span class="sxs-lookup"><span data-stu-id="132be-137">Application package file structure</span></span>
<span data-ttu-id="132be-138">toodeploy tooService um aplicativo do Fabric, aplicativo hello deve seguir uma estrutura de diretório predefinidos.</span><span class="sxs-lookup"><span data-stu-id="132be-138">toodeploy an application tooService Fabric, hello application should follow a predefined directory structure.</span></span> <span data-ttu-id="132be-139">a seguir Olá é um exemplo de estrutura.</span><span class="sxs-lookup"><span data-stu-id="132be-139">hello following is an example of that structure.</span></span>

```
|-- ApplicationPackageRoot
    |-- GuestService1Pkg
        |-- Code
            |-- existingapp.exe
        |-- Config
            |-- Settings.xml
        |-- Data
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```

<span data-ttu-id="132be-140">Olá ApplicationPackageRoot contém arquivo applicationmanifest. XML Olá que define o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="132be-140">hello ApplicationPackageRoot contains hello ApplicationManifest.xml file that defines hello application.</span></span> <span data-ttu-id="132be-141">Um subdiretório para cada serviço incluído no aplicativo hello é usado toocontain todos Olá artefatos de serviço Olá requer.</span><span class="sxs-lookup"><span data-stu-id="132be-141">A subdirectory for each service included in hello application is used toocontain all hello artifacts that hello service requires.</span></span> <span data-ttu-id="132be-142">Esses subdiretórios são Olá ServiceManifest.xml e, geralmente, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="132be-142">These subdirectories are hello ServiceManifest.xml and, typically, hello following:</span></span>

* <span data-ttu-id="132be-143">*Código*.</span><span class="sxs-lookup"><span data-stu-id="132be-143">*Code*.</span></span> <span data-ttu-id="132be-144">Este diretório contém código de saudação do serviço.</span><span class="sxs-lookup"><span data-stu-id="132be-144">This directory contains hello service code.</span></span>
* <span data-ttu-id="132be-145">*Config*. Este diretório contém um arquivo Settings.xml (e outros arquivos, se necessário) que o serviço de saudação pode acessar no tempo de execução tooretrieve configurações específicas.</span><span class="sxs-lookup"><span data-stu-id="132be-145">*Config*. This directory contains a Settings.xml file (and other files if necessary) that hello service can access at runtime tooretrieve specific configuration settings.</span></span>
* <span data-ttu-id="132be-146">*Dados*.</span><span class="sxs-lookup"><span data-stu-id="132be-146">*Data*.</span></span> <span data-ttu-id="132be-147">Este é um diretório adicional toostore local dados adicionais que talvez seja necessário serviço hello.</span><span class="sxs-lookup"><span data-stu-id="132be-147">This is an additional directory toostore additional local data that hello service may need.</span></span> <span data-ttu-id="132be-148">Dados devem ser dados apenas efêmera toostore usado.</span><span class="sxs-lookup"><span data-stu-id="132be-148">Data should be used toostore only ephemeral data.</span></span> <span data-ttu-id="132be-149">Malha do serviço faz não copiar ou replicar o diretório de dados do alterações toohello se precisar de serviço Olá toobe realocado (por exemplo, durante o failover).</span><span class="sxs-lookup"><span data-stu-id="132be-149">Service Fabric does not copy or replicate changes toohello data directory if hello service needs toobe relocated (for example, during failover).</span></span>

> [!NOTE]
> <span data-ttu-id="132be-150">Você não tem toocreate Olá `config` e `data` diretórios se você não precisar deles.</span><span class="sxs-lookup"><span data-stu-id="132be-150">You don't have toocreate hello `config` and `data` directories if you don't need them.</span></span>
>
>

## <a name="package-an-existing-executable"></a><span data-ttu-id="132be-151">Empacotar um executável existente</span><span class="sxs-lookup"><span data-stu-id="132be-151">Package an existing executable</span></span>
<span data-ttu-id="132be-152">Ao empacotar um executável de convidado, você pode escolher qualquer toouse um modelo de projeto do Visual Studio ou muito[criar manualmente o pacote de aplicativo hello](#manually).</span><span class="sxs-lookup"><span data-stu-id="132be-152">When packaging a guest executable, you can choose either toouse a Visual Studio project template or too[create hello application package manually](#manually).</span></span> <span data-ttu-id="132be-153">Usando o Visual Studio, Olá a estrutura do pacote de aplicativos e arquivos de manifesto são criados pelo novo modelo de projeto Olá para você.</span><span class="sxs-lookup"><span data-stu-id="132be-153">Using Visual Studio, hello application package structure and manifest files are created by hello new project template for you.</span></span>

> [!TIP]
> <span data-ttu-id="132be-154">toopackage de maneira mais fácil de saudação um executável em um serviço existente do Windows é toouse Visual Studio e no Linux toouse Yeoman</span><span class="sxs-lookup"><span data-stu-id="132be-154">hello easiest way toopackage an existing Windows executable into a service is toouse Visual Studio and on Linux toouse Yeoman</span></span>
>

## <a name="use-visual-studio-toopackage-and-deploy-an-existing-executable"></a><span data-ttu-id="132be-155">Use o Visual Studio toopackage e implantar um arquivo executável existente</span><span class="sxs-lookup"><span data-stu-id="132be-155">Use Visual Studio toopackage and deploy an existing executable</span></span>
<span data-ttu-id="132be-156">O Visual Studio fornece uma estrutura de serviço toohelp de modelo de serviço é implantar um cluster do convidado tooa executável do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="132be-156">Visual Studio provides a Service Fabric service template toohelp you deploy a guest executable tooa Service Fabric cluster.</span></span>

1. <span data-ttu-id="132be-157">Escolha **Arquivo** > **Novo Projeto** e crie um aplicativo de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="132be-157">Choose **File** > **New Project**, and create a Service Fabric application.</span></span>
2. <span data-ttu-id="132be-158">Escolha **executável de convidado** como modelo de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="132be-158">Choose **Guest Executable** as hello service template.</span></span>
3. <span data-ttu-id="132be-159">Clique em **procurar** tooselect pasta de saudação com o executável e preencha o restante de saudação do serviço de Olá Olá parâmetros toocreate.</span><span class="sxs-lookup"><span data-stu-id="132be-159">Click **Browse** tooselect hello folder with your executable and fill in hello rest of hello parameters toocreate hello service.</span></span>
   * <span data-ttu-id="132be-160">*Comportamento do Pacote de Código*.</span><span class="sxs-lookup"><span data-stu-id="132be-160">*Code Package Behavior*.</span></span> <span data-ttu-id="132be-161">Pode ser conjunto toocopy todo o conteúdo de saudação do toohello sua pasta projeto do Visual Studio, que é útil se Olá executável não for alterada.</span><span class="sxs-lookup"><span data-stu-id="132be-161">Can be set toocopy all hello content of your folder toohello Visual Studio Project, which is useful if hello executable does not change.</span></span> <span data-ttu-id="132be-162">Se você espera toochange executável hello e desejar Olá capacidade toopick backup novas compilações dinamicamente, você pode escolher toolink toohello pasta em vez disso.</span><span class="sxs-lookup"><span data-stu-id="132be-162">If you expect hello executable toochange and want hello ability toopick up new builds dynamically, you can choose toolink toohello folder instead.</span></span> <span data-ttu-id="132be-163">Você pode usar pastas vinculadas ao criar o projeto de aplicativo hello no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="132be-163">You can use linked folders when creating hello application project in Visual Studio.</span></span> <span data-ttu-id="132be-164">Isso vincula o local de origem toohello do projeto Olá, possibilitando que os convidados Olá tooupdate executável em seu destino de origem.</span><span class="sxs-lookup"><span data-stu-id="132be-164">This links toohello source location from within hello project, making it possible for you tooupdate hello guest executable in its source destination.</span></span> <span data-ttu-id="132be-165">Essas atualizações se tornam parte do pacote de aplicativo hello na compilação.</span><span class="sxs-lookup"><span data-stu-id="132be-165">Those updates become part of hello application package on build.</span></span>
   * <span data-ttu-id="132be-166">*Programa* Especifica Olá executável que deve ser executado o serviço de saudação toostart.</span><span class="sxs-lookup"><span data-stu-id="132be-166">*Program* specifies hello executable that should be run toostart hello service.</span></span>
   * <span data-ttu-id="132be-167">*Argumentos* Especifica argumentos de saudação que devem ser passados toohello executável.</span><span class="sxs-lookup"><span data-stu-id="132be-167">*Arguments* specifies hello arguments that should be passed toohello executable.</span></span> <span data-ttu-id="132be-168">Pode ser uma lista de parâmetros com argumentos.</span><span class="sxs-lookup"><span data-stu-id="132be-168">It can be a list of parameters with arguments.</span></span>
   * <span data-ttu-id="132be-169">*Pasta de trabalho* Especifica Olá a pasta de trabalho para processo de saudação que será toobe iniciado.</span><span class="sxs-lookup"><span data-stu-id="132be-169">*WorkingFolder* specifies hello working directory for hello process that is going toobe started.</span></span> <span data-ttu-id="132be-170">Você pode especificar três valores:</span><span class="sxs-lookup"><span data-stu-id="132be-170">You can specify three values:</span></span>
     * <span data-ttu-id="132be-171">`CodeBase`Especifica esse diretório de trabalho Olá vai toobe definir diretório de código toohello no pacote de aplicativo hello (`Code` directory mostrada a saudação anterior a estrutura de arquivos).</span><span class="sxs-lookup"><span data-stu-id="132be-171">`CodeBase` specifies that hello working directory is going toobe set toohello code directory in hello application package (`Code` directory shown in hello preceding file structure).</span></span>
     * <span data-ttu-id="132be-172">`CodePackage`Especifica esse diretório de trabalho Olá vai toobe definir toohello raiz do pacote de aplicativo hello (`GuestService1Pkg` mostra a saudação anterior a estrutura de arquivos).</span><span class="sxs-lookup"><span data-stu-id="132be-172">`CodePackage` specifies that hello working directory is going toobe set toohello root of hello application package    (`GuestService1Pkg` shown in hello preceding file structure).</span></span>
     * <span data-ttu-id="132be-173">`Work`Especifica que os arquivos de saudação são colocados em uma subpasta chamada de trabalho.</span><span class="sxs-lookup"><span data-stu-id="132be-173">`Work` specifies that hello files are placed in a subdirectory called work.</span></span>
4. <span data-ttu-id="132be-174">Dê um nome ao seu serviço e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="132be-174">Give your service a name, and click **OK**.</span></span>
5. <span data-ttu-id="132be-175">Se seu serviço precisa de um ponto de extremidade de comunicação, agora você pode adicionar arquivos do tipo toohello ServiceManifest.xml, porta e protocolo de saudação.</span><span class="sxs-lookup"><span data-stu-id="132be-175">If your service needs an endpoint for communication, you can now add hello protocol, port, and type toohello ServiceManifest.xml file.</span></span> <span data-ttu-id="132be-176">Por exemplo: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.</span><span class="sxs-lookup"><span data-stu-id="132be-176">For example: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.</span></span>
6. <span data-ttu-id="132be-177">Agora você pode usar o pacote de saudação e publicar ação contra o cluster local, depuração Olá solução no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="132be-177">You can now use hello package and publish action against your local cluster by debugging hello solution in Visual Studio.</span></span> <span data-ttu-id="132be-178">Quando estiver pronto, você pode publicar cluster remoto da saudação aplicativo tooa ou check-in de controle de toosource Olá solução.</span><span class="sxs-lookup"><span data-stu-id="132be-178">When ready, you can publish hello application tooa remote cluster or check in hello solution toosource control.</span></span>
7. <span data-ttu-id="132be-179">Ir para o fim de toohello de toosee este artigo como tooview seu serviço executável de convidado em execução no Gerenciador do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="132be-179">Go toohello end of this article toosee how tooview your guest executable service running in Service Fabric Explorer.</span></span>

## <a name="use-yoeman-toopackage-and-deploy-an-existing-executable-on-linux"></a><span data-ttu-id="132be-180">Use Yoeman toopackage e implantar um executável existente no Linux</span><span class="sxs-lookup"><span data-stu-id="132be-180">Use Yoeman toopackage and deploy an existing executable on Linux</span></span>

<span data-ttu-id="132be-181">procedimento de saudação para criar e implantar um convidado executável no Linux é Olá igual ao implantar um aplicativo de java csharp.</span><span class="sxs-lookup"><span data-stu-id="132be-181">hello procedure for creating and deploying a guest executable on Linux is hello same as deploying a csharp or java application.</span></span>

1. <span data-ttu-id="132be-182">Em um terminal, digite `yo azuresfguest`.</span><span class="sxs-lookup"><span data-stu-id="132be-182">In a terminal, type `yo azuresfguest`.</span></span>
2. <span data-ttu-id="132be-183">Nome do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="132be-183">Name your application.</span></span>
3. <span data-ttu-id="132be-184">Nome do seu serviço e fornecer detalhes de saudação incluindo caminho do executável do hello e parâmetros de saudação com que precisa ser chamada.</span><span class="sxs-lookup"><span data-stu-id="132be-184">Name your service, and provide hello details including path of hello executable and hello parameters it must be invoked with.</span></span>

<span data-ttu-id="132be-185">Yeoman cria um pacote de aplicativos com o aplicativo apropriado hello e arquivos de manifesto juntamente com instalar e desinstalar scripts.</span><span class="sxs-lookup"><span data-stu-id="132be-185">Yeoman creates an application package with hello appropriate application and manifest files along with install and uninstall scripts.</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-an-existing-executable"></a><span data-ttu-id="132be-186">Empacotar e implantar manualmente um executável existente</span><span class="sxs-lookup"><span data-stu-id="132be-186">Manually package and deploy an existing executable</span></span>
<span data-ttu-id="132be-187">processo de saudação do empacotamento manualmente um executável de convidado se baseia na Olá etapas gerais a seguir:</span><span class="sxs-lookup"><span data-stu-id="132be-187">hello process of manually packaging a guest executable is based on hello following general steps:</span></span>

1. <span data-ttu-id="132be-188">Crie estrutura de diretório do pacote de saudação.</span><span class="sxs-lookup"><span data-stu-id="132be-188">Create hello package directory structure.</span></span>
2. <span data-ttu-id="132be-189">Adicione arquivos de código e configuração do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="132be-189">Add hello application's code and configuration files.</span></span>
3. <span data-ttu-id="132be-190">Edite o arquivo de manifesto de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="132be-190">Edit hello service manifest file.</span></span>
4. <span data-ttu-id="132be-191">Edite o arquivo de manifesto de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="132be-191">Edit hello application manifest file.</span></span>

<!--
>[AZURE.NOTE] We do provide a packaging tool that allows you toocreate hello ApplicationPackage automatically. hello tool is currently in preview. You can download it from [here](http://aka.ms/servicefabricpacktool).
-->

### <a name="create-hello-package-directory-structure"></a><span data-ttu-id="132be-192">Criar estrutura de diretório do pacote de saudação</span><span class="sxs-lookup"><span data-stu-id="132be-192">Create hello package directory structure</span></span>
<span data-ttu-id="132be-193">Você pode iniciar, criando a estrutura de diretórios hello, conforme descrito em Olá anterior seção, "Estrutura de arquivo de pacote de aplicativos".</span><span class="sxs-lookup"><span data-stu-id="132be-193">You can start by creating hello directory structure, as described in hello preceding section, "Application package file structure."</span></span>

### <a name="add-hello-applications-code-and-configuration-files"></a><span data-ttu-id="132be-194">Adicionar arquivos de código e configuração do aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="132be-194">Add hello application's code and configuration files</span></span>
<span data-ttu-id="132be-195">Depois que você criou a estrutura de diretórios hello, você pode adicionar arquivos de código e configuração do aplicativo hello em diretórios de código e configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="132be-195">After you have created hello directory structure, you can add hello application's code and configuration files under hello code and config directories.</span></span> <span data-ttu-id="132be-196">Você também pode criar diretórios adicionais ou subpastas em pastas de código ou configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="132be-196">You can also create additional directories or subdirectories under hello code or config directories.</span></span>

<span data-ttu-id="132be-197">Service Fabric um `xcopy` conteúdo de saudação do hello diretório raiz do aplicativo, portanto, não há nenhum toouse estrutura predefinida diferente de criar dois diretórios principais, código e configurações.</span><span class="sxs-lookup"><span data-stu-id="132be-197">Service Fabric does an `xcopy` of hello content of hello application root directory, so there is no predefined structure toouse other than creating two top directories, code and settings.</span></span> <span data-ttu-id="132be-198">(Você pode escolher nomes diferentes, se desejar.</span><span class="sxs-lookup"><span data-stu-id="132be-198">(You can pick different names if you want.</span></span> <span data-ttu-id="132be-199">Mais detalhes estão na próxima seção, hello.)</span><span class="sxs-lookup"><span data-stu-id="132be-199">More details are in hello next section.)</span></span>

> [!NOTE]
> <span data-ttu-id="132be-200">Certifique-se de incluir todos os arquivos de saudação e as dependências de Olá necessidades do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="132be-200">Make sure that you include all hello files and dependencies that hello application needs.</span></span> <span data-ttu-id="132be-201">Service Fabric copia Olá conteúdo do pacote de aplicativo hello em todos os nós no cluster Olá onde os serviços do aplicativo hello são toobe será implantado.</span><span class="sxs-lookup"><span data-stu-id="132be-201">Service Fabric copies hello content of hello application package on all nodes in hello cluster where hello application's services are going toobe deployed.</span></span> <span data-ttu-id="132be-202">pacote de saudação deve conter todo o código Olá aplicativo hello precisa toorun.</span><span class="sxs-lookup"><span data-stu-id="132be-202">hello package should contain all hello code that hello application needs toorun.</span></span> <span data-ttu-id="132be-203">Não suponha que as dependências de saudação já estão instaladas.</span><span class="sxs-lookup"><span data-stu-id="132be-203">Do not assume that hello dependencies are already installed.</span></span>
>
>

### <a name="edit-hello-service-manifest-file"></a><span data-ttu-id="132be-204">Editar o arquivo de manifesto de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="132be-204">Edit hello service manifest file</span></span>
<span data-ttu-id="132be-205">Olá próxima etapa é Olá tooedit Olá serviço arquivo de manifesto tooinclude informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="132be-205">hello next step is tooedit hello service manifest file tooinclude hello following information:</span></span>

* <span data-ttu-id="132be-206">nome de Olá Olá do tipo de serviço.</span><span class="sxs-lookup"><span data-stu-id="132be-206">hello name of hello service type.</span></span> <span data-ttu-id="132be-207">Essa é uma ID do Service Fabric usa tooidentify um serviço.</span><span class="sxs-lookup"><span data-stu-id="132be-207">This is an ID that Service Fabric uses tooidentify a service.</span></span>
* <span data-ttu-id="132be-208">comando toouse toolaunch Olá aplicativo Hello (ExeHost).</span><span class="sxs-lookup"><span data-stu-id="132be-208">hello command toouse toolaunch hello application (ExeHost).</span></span>
* <span data-ttu-id="132be-209">Qualquer script que precisa tooset toobe executar o aplicativo hello (SetupEntrypoint).</span><span class="sxs-lookup"><span data-stu-id="132be-209">Any script that needs toobe run tooset up hello application (SetupEntrypoint).</span></span>

<span data-ttu-id="132be-210">Olá, a seguir é um exemplo de um `ServiceManifest.xml` arquivo:</span><span class="sxs-lookup"><span data-stu-id="132be-210">hello following is an example of a `ServiceManifest.xml` file:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="NodeApp" Version="1.0.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceTypes>
      <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true"/>
   </ServiceTypes>
   <CodePackage Name="code" Version="1.0.0.0">
      <SetupEntryPoint>
         <ExeHost>
             <Program>scripts\launchConfig.cmd</Program>
         </ExeHost>
      </SetupEntryPoint>
      <EntryPoint>
         <ExeHost>
            <Program>node.exe</Program>
            <Arguments>bin/www</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
         </ExeHost>
      </EntryPoint>
   </CodePackage>
   <Resources>
      <Endpoints>
         <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
   </Resources>
</ServiceManifest>
```

<span data-ttu-id="132be-211">Olá seções a seguir passa pelo partes diferentes de saudação do arquivo de saudação que você precisa tooupdate.</span><span class="sxs-lookup"><span data-stu-id="132be-211">hello following sections go over hello different parts of hello file that you need tooupdate.</span></span>

#### <a name="update-servicetypes"></a><span data-ttu-id="132be-212">Atualizar ServiceTypes</span><span class="sxs-lookup"><span data-stu-id="132be-212">Update ServiceTypes</span></span>
```xml
<ServiceTypes>
  <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true" />
</ServiceTypes>
```

* <span data-ttu-id="132be-213">Você pode escolher qualquer nome que desejar para `ServiceTypeName`.</span><span class="sxs-lookup"><span data-stu-id="132be-213">You can pick any name that you want for `ServiceTypeName`.</span></span> <span data-ttu-id="132be-214">Olá valor é usado em Olá `ApplicationManifest.xml` tooidentify Olá serviço de arquivo.</span><span class="sxs-lookup"><span data-stu-id="132be-214">hello value is used in hello `ApplicationManifest.xml` file tooidentify hello service.</span></span>
* <span data-ttu-id="132be-215">Especifique `UseImplicitHost="true"`.</span><span class="sxs-lookup"><span data-stu-id="132be-215">Specify `UseImplicitHost="true"`.</span></span> <span data-ttu-id="132be-216">Esse atributo diz Service Fabric que serviço Olá baseia-se em um aplicativo independente, para todos os Service Fabric precisa toodo toolaunch-lo como um processo e monitorar sua integridade.</span><span class="sxs-lookup"><span data-stu-id="132be-216">This attribute tells Service Fabric that hello service is based on a self-contained app, so all Service Fabric needs toodo is toolaunch it as a process and monitor its health.</span></span>

#### <a name="update-codepackage"></a><span data-ttu-id="132be-217">Atualizar CodePackage</span><span class="sxs-lookup"><span data-stu-id="132be-217">Update CodePackage</span></span>
<span data-ttu-id="132be-218">elemento de CodePackage Olá Especifica o local de saudação (e versão) do código de saudação do serviço.</span><span class="sxs-lookup"><span data-stu-id="132be-218">hello CodePackage element specifies hello location (and version) of hello service's code.</span></span>

```xml
<CodePackage Name="Code" Version="1.0.0.0">
```

<span data-ttu-id="132be-219">Olá `Name` elemento é usado toospecify Olá nome do diretório Olá no pacote de aplicativo hello que contém o código do serviço hello.</span><span class="sxs-lookup"><span data-stu-id="132be-219">hello `Name` element is used toospecify hello name of hello directory in hello application package that contains hello service's code.</span></span> <span data-ttu-id="132be-220">`CodePackage`também tem Olá `version` atributo.</span><span class="sxs-lookup"><span data-stu-id="132be-220">`CodePackage` also has hello `version` attribute.</span></span> <span data-ttu-id="132be-221">Isso pode ser usado toospecify versão de saudação do código-Olá e pode também ser usado código do serviço de saudação tooupgrade usando a infraestrutura de gerenciamento de ciclo de vida do aplicativo hello na malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="132be-221">This can be used toospecify hello version of hello code, and can also potentially be used tooupgrade hello service's code by using hello application lifecycle management infrastructure in Service Fabric.</span></span>

#### <a name="optional-update-setupentrypoint"></a><span data-ttu-id="132be-222">Opcional: atualizar SetupEntrypoint</span><span class="sxs-lookup"><span data-stu-id="132be-222">Optional: Update SetupEntrypoint</span></span>
```xml
<SetupEntryPoint>
   <ExeHost>
       <Program>scripts\launchConfig.cmd</Program>
   </ExeHost>
</SetupEntryPoint>
```
<span data-ttu-id="132be-223">elemento do Hello SetupEntryPoint é usado toospecify qualquer arquivo executável ou em lotes que deve ser executado antes que o código de saudação do serviço é iniciado.</span><span class="sxs-lookup"><span data-stu-id="132be-223">hello SetupEntryPoint element is used toospecify any executable or batch file that should be executed before hello service's code is launched.</span></span> <span data-ttu-id="132be-224">É uma etapa opcional, portanto não precisa toobe incluído se não houver nenhum inicialização necessária.</span><span class="sxs-lookup"><span data-stu-id="132be-224">It is an optional step, so it does not need toobe included if there is no initialization required.</span></span> <span data-ttu-id="132be-225">Olá SetupEntryPoint é executado sempre que o serviço Olá for reiniciado.</span><span class="sxs-lookup"><span data-stu-id="132be-225">hello SetupEntryPoint is executed every time hello service is restarted.</span></span>

<span data-ttu-id="132be-226">Como há apenas um SetupEntryPoint, scripts de instalação necessário toobe agrupado em um arquivo único lote, se a instalação do aplicativo hello requer vários scripts.</span><span class="sxs-lookup"><span data-stu-id="132be-226">There is only one SetupEntryPoint, so setup scripts need toobe grouped in a single batch file if hello application's setup requires multiple scripts.</span></span> <span data-ttu-id="132be-227">Olá SetupEntryPoint pode executar qualquer tipo de arquivo: arquivos executáveis, arquivos em lotes e cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="132be-227">hello SetupEntryPoint can execute any type of file: executable files, batch files, and PowerShell cmdlets.</span></span> <span data-ttu-id="132be-228">Para obter mais detalhes, confira [Configure SetupEntryPoint](service-fabric-application-runas-security.md)(Configurar SetupEntryPoint).</span><span class="sxs-lookup"><span data-stu-id="132be-228">For more details, see [Configure SetupEntryPoint](service-fabric-application-runas-security.md).</span></span>

<span data-ttu-id="132be-229">Em Olá anterior de exemplo, Olá SetupEntryPoint executa um arquivo em lotes chamado `LaunchConfig.cmd` que é localizado na Olá `scripts` subdiretório do diretório de código hello (supondo que o elemento de pasta de trabalho de saudação é definido tooCodeBase).</span><span class="sxs-lookup"><span data-stu-id="132be-229">In hello preceding example, hello SetupEntryPoint runs a batch file called `LaunchConfig.cmd` that is located in hello `scripts` subdirectory of hello code directory (assuming hello WorkingFolder element is set tooCodeBase).</span></span>

#### <a name="update-entrypoint"></a><span data-ttu-id="132be-230">Atualizar EntryPoint</span><span class="sxs-lookup"><span data-stu-id="132be-230">Update EntryPoint</span></span>
```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
  </ExeHost>
</EntryPoint>
```

<span data-ttu-id="132be-231">Olá `EntryPoint` elemento no arquivo de manifesto de serviço Olá é usado toospecify como serviço de saudação toolaunch.</span><span class="sxs-lookup"><span data-stu-id="132be-231">hello `EntryPoint` element in hello service manifest file is used toospecify how toolaunch hello service.</span></span> <span data-ttu-id="132be-232">Olá `ExeHost` elemento Especifica hello executável (e argumentos) que deve ser usado toolaunch Olá serviço.</span><span class="sxs-lookup"><span data-stu-id="132be-232">hello `ExeHost` element specifies hello executable (and arguments) that should be used toolaunch hello service.</span></span>

* <span data-ttu-id="132be-233">`Program`Especifica o nome de saudação do executável de saudação que deve iniciar o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="132be-233">`Program` specifies hello name of hello executable that should start hello service.</span></span>
* <span data-ttu-id="132be-234">`Arguments`Especifica argumentos de saudação que devem ser passados toohello executável.</span><span class="sxs-lookup"><span data-stu-id="132be-234">`Arguments` specifies hello arguments that should be passed toohello executable.</span></span> <span data-ttu-id="132be-235">Pode ser uma lista de parâmetros com argumentos.</span><span class="sxs-lookup"><span data-stu-id="132be-235">It can be a list of parameters with arguments.</span></span>
* <span data-ttu-id="132be-236">`WorkingFolder`Especifica o diretório de trabalho de saudação do processo Olá vai toobe iniciado.</span><span class="sxs-lookup"><span data-stu-id="132be-236">`WorkingFolder` specifies hello working directory for hello process that is going toobe started.</span></span> <span data-ttu-id="132be-237">Você pode especificar três valores:</span><span class="sxs-lookup"><span data-stu-id="132be-237">You can specify three values:</span></span>
  * <span data-ttu-id="132be-238">`CodeBase`Especifica esse diretório de trabalho Olá vai toobe definir diretório de código toohello no pacote de aplicativo hello (`Code` diretório no hello anterior a estrutura de arquivos).</span><span class="sxs-lookup"><span data-stu-id="132be-238">`CodeBase` specifies that hello working directory is going toobe set toohello code directory in hello application package (`Code` directory in hello preceding file structure).</span></span>
  * <span data-ttu-id="132be-239">`CodePackage`Especifica esse diretório de trabalho Olá vai toobe definir toohello raiz do pacote de aplicativo hello (`GuestService1Pkg` no hello anterior a estrutura de arquivos).</span><span class="sxs-lookup"><span data-stu-id="132be-239">`CodePackage` specifies that hello working directory is going toobe set toohello root of hello application package    (`GuestService1Pkg` in hello preceding file structure).</span></span>
    * <span data-ttu-id="132be-240">`Work`Especifica que os arquivos de saudação são colocados em uma subpasta chamada de trabalho.</span><span class="sxs-lookup"><span data-stu-id="132be-240">`Work` specifies that hello files are placed in a subdirectory called work.</span></span>

<span data-ttu-id="132be-241">Olá pasta de trabalho é diretório de trabalho útil tooset Olá correto para que os caminhos relativos podem ser usados por qualquer um dos scripts de inicialização ou o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="132be-241">hello WorkingFolder is useful tooset hello correct working directory so that relative paths can be used by either hello application or initialization scripts.</span></span>

#### <a name="update-endpoints-and-register-with-naming-service-for-communication"></a><span data-ttu-id="132be-242">Atualizar pontos de extremidade e registrar com o Serviço de Nomenclatura para comunicação</span><span class="sxs-lookup"><span data-stu-id="132be-242">Update Endpoints and register with Naming Service for communication</span></span>
```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
</Endpoints>

```
<span data-ttu-id="132be-243">Em Olá anterior de exemplo, Olá `Endpoint` elemento Especifica os pontos de extremidade de saudação que aplicativo hello pode escutar em.</span><span class="sxs-lookup"><span data-stu-id="132be-243">In hello preceding example, hello `Endpoint` element specifies hello endpoints that hello application can listen on.</span></span> <span data-ttu-id="132be-244">Neste exemplo, Olá aplicativo Node. js escuta http na porta 3000.</span><span class="sxs-lookup"><span data-stu-id="132be-244">In this example, hello Node.js application listens on http on port 3000.</span></span>

<span data-ttu-id="132be-245">Além disso você pode pedir Service Fabric toopublish toohello esse ponto de extremidade Naming Service para que outros serviços podem descobrir o serviço de toothis de endereço de ponto de extremidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="132be-245">Furthermore you can ask Service Fabric toopublish this endpoint toohello Naming Service so other services can discover hello endpoint address toothis service.</span></span> <span data-ttu-id="132be-246">Isso permite que você toocommunicate capaz de toobe entre os serviços que são executáveis de convidado.</span><span class="sxs-lookup"><span data-stu-id="132be-246">This enables you toobe able toocommunicate between services that are guest executables.</span></span>
<span data-ttu-id="132be-247">Hello endereço de ponto de extremidade publicados tem Olá forma `UriScheme://IPAddressOrFQDN:Port/PathSuffix`.</span><span class="sxs-lookup"><span data-stu-id="132be-247">hello published endpoint address is of hello form `UriScheme://IPAddressOrFQDN:Port/PathSuffix`.</span></span> <span data-ttu-id="132be-248">`UriScheme` e `PathSuffix` são atributos opcionais.</span><span class="sxs-lookup"><span data-stu-id="132be-248">`UriScheme` and `PathSuffix` are optional attributes.</span></span> <span data-ttu-id="132be-249">`IPAddressOrFQDN`é Olá endereço IP ou nome de domínio totalmente qualificado do nó Olá este executável é colocada no e ele é calculado para você.</span><span class="sxs-lookup"><span data-stu-id="132be-249">`IPAddressOrFQDN` is hello IP address or fully qualified domain name of hello node this executable gets placed on, and it is calculated for you.</span></span>

<span data-ttu-id="132be-250">No hello exemplo a seguir, uma vez o serviço Olá é implantado, no Gerenciador do Service Fabric você ver um ponto de extremidade semelhante muito`http://10.1.4.92:3000/myapp/` publicado Olá instância de serviço.</span><span class="sxs-lookup"><span data-stu-id="132be-250">In hello following example, once hello service is deployed, in Service Fabric Explorer you see an endpoint similar too`http://10.1.4.92:3000/myapp/` published for hello service instance.</span></span> <span data-ttu-id="132be-251">Se esta for um computador local, você verá `http://localhost:3000/myapp/`.</span><span class="sxs-lookup"><span data-stu-id="132be-251">Or if this is a local machine, you see `http://localhost:3000/myapp/`.</span></span>

```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000"  UriScheme="http" PathSuffix="myapp/" Type="Input" />
</Endpoints>
```
<span data-ttu-id="132be-252">Você pode usar esses endereços com [proxy reverso](service-fabric-reverseproxy.md) toocommunicate entre serviços.</span><span class="sxs-lookup"><span data-stu-id="132be-252">You can use these addresses with [reverse proxy](service-fabric-reverseproxy.md) toocommunicate between services.</span></span>

### <a name="edit-hello-application-manifest-file"></a><span data-ttu-id="132be-253">Editar o arquivo de manifesto de aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="132be-253">Edit hello application manifest file</span></span>
<span data-ttu-id="132be-254">Depois que você configurou Olá `Servicemanifest.xml` arquivo, você precisa toomake toohello algumas alterações `ApplicationManifest.xml` tooensure Olá de arquivo correto para o tipo de serviço e o nome são usados.</span><span class="sxs-lookup"><span data-stu-id="132be-254">Once you have configured hello `Servicemanifest.xml` file, you need toomake some changes toohello `ApplicationManifest.xml` file tooensure that hello correct service type and name are used.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="NodeAppType" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
   </ServiceManifestImport>
</ApplicationManifest>
```

#### <a name="servicemanifestimport"></a><span data-ttu-id="132be-255">ServiceManifestImport</span><span class="sxs-lookup"><span data-stu-id="132be-255">ServiceManifestImport</span></span>
<span data-ttu-id="132be-256">Em Olá `ServiceManifestImport` elemento, você pode especificar um ou mais serviços que você deseja tooinclude no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="132be-256">In hello `ServiceManifestImport` element, you can specify one or more services that you want tooinclude in hello app.</span></span> <span data-ttu-id="132be-257">Os serviços são referenciados com `ServiceManifestName`, que especifica o nome de saudação do diretório de saudação onde hello `ServiceManifest.xml` arquivo está localizado.</span><span class="sxs-lookup"><span data-stu-id="132be-257">Services are referenced with `ServiceManifestName`, which specifies hello name of hello directory where hello `ServiceManifest.xml` file is located.</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
</ServiceManifestImport>
```

## <a name="set-up-logging"></a><span data-ttu-id="132be-258">Configurar registro em log</span><span class="sxs-lookup"><span data-stu-id="132be-258">Set up logging</span></span>
<span data-ttu-id="132be-259">Para executáveis de convidado, é útil toobe toosee capaz de console logs toofind out se os scripts de configuração de aplicativo e Olá mostram erros.</span><span class="sxs-lookup"><span data-stu-id="132be-259">For guest executables, it is useful toobe able toosee console logs toofind out if hello application and configuration scripts show any errors.</span></span>
<span data-ttu-id="132be-260">Redirecionamento de console pode ser configurado no hello `ServiceManifest.xml` arquivo usando Olá `ConsoleRedirection` elemento.</span><span class="sxs-lookup"><span data-stu-id="132be-260">Console redirection can be configured in hello `ServiceManifest.xml` file using hello `ConsoleRedirection` element.</span></span>

> [!WARNING]
> <span data-ttu-id="132be-261">Nunca use a política de redirecionamento do console de saudação em um aplicativo que é implantado na produção, pois isso pode afetar o failover de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="132be-261">Never use hello console redirection policy in an application that is deployed in production because this can affect hello application failover.</span></span> <span data-ttu-id="132be-262">*Só* use isso para fins de depuração e de desenvolvimento locais.</span><span class="sxs-lookup"><span data-stu-id="132be-262">*Only* use this for local development and debugging purposes.</span></span>  
>
>

```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="5" FileMaxSizeInKb="2048"/>
  </ExeHost>
</EntryPoint>
```

<span data-ttu-id="132be-263">`ConsoleRedirection`pode ser um diretório de trabalho usado tooredirect console saída (stdout e stderr) tooa.</span><span class="sxs-lookup"><span data-stu-id="132be-263">`ConsoleRedirection` can be used tooredirect console output (both stdout and stderr) tooa working directory.</span></span> <span data-ttu-id="132be-264">Isso fornece Olá capacidade tooverify que não existem erros durante a instalação de saudação ou execução do aplicativo hello no cluster do Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="132be-264">This provides hello ability tooverify that there are no errors during hello setup or execution of hello application in hello Service Fabric cluster.</span></span>

<span data-ttu-id="132be-265">`FileRetentionCount`Determina quantos arquivos são salvos no diretório de trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="132be-265">`FileRetentionCount` determines how many files are saved in hello working directory.</span></span> <span data-ttu-id="132be-266">Um valor de 5, por exemplo, significa que os arquivos de log Olá para execuções de cinco anterior Olá são armazenados no diretório de trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="132be-266">A value of 5, for example, means that hello log files for hello previous five executions are stored in hello working directory.</span></span>

<span data-ttu-id="132be-267">`FileMaxSizeInKb`Especifica o tamanho máximo de Olá Olá dos arquivos de log.</span><span class="sxs-lookup"><span data-stu-id="132be-267">`FileMaxSizeInKb` specifies hello maximum size of hello log files.</span></span>

<span data-ttu-id="132be-268">Arquivos de log são salvos em um dos diretórios de trabalho do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="132be-268">Log files are saved in one of hello service's working directories.</span></span> <span data-ttu-id="132be-269">toodetermine onde Olá arquivos estão localizados, use o Service Fabric Explorer toodetermine qual serviço de saudação do nó está em execução e o diretório de trabalho está sendo usado.</span><span class="sxs-lookup"><span data-stu-id="132be-269">toodetermine where hello files are located, use Service Fabric Explorer toodetermine which node hello service is running on, and which working directory is being used.</span></span> <span data-ttu-id="132be-270">Esse processo é abordado mais adiante neste artigo.</span><span class="sxs-lookup"><span data-stu-id="132be-270">This process is covered later in this article.</span></span>

## <a name="deployment"></a><span data-ttu-id="132be-271">Implantação</span><span class="sxs-lookup"><span data-stu-id="132be-271">Deployment</span></span>
<span data-ttu-id="132be-272">Olá última etapa é muito[implantar seu aplicativo](service-fabric-deploy-remove-applications.md).</span><span class="sxs-lookup"><span data-stu-id="132be-272">hello last step is too[deploy your application](service-fabric-deploy-remove-applications.md).</span></span> <span data-ttu-id="132be-273">Olá mostra de script do PowerShell a seguir como toodeploy seu cluster de desenvolvimento local do aplicativo toohello e iniciar um novo serviço de malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="132be-273">hello following PowerShell script shows how toodeploy your application toohello local development cluster, and start a new Service Fabric service.</span></span>

```PowerShell

Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath 'C:\Dev\MultipleApplications' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'nodeapp'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'nodeapp'

New-ServiceFabricApplication -ApplicationName 'fabric:/nodeapp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0

New-ServiceFabricService -ApplicationName 'fabric:/nodeapp' -ServiceName 'fabric:/nodeapp/nodeappservice' -ServiceTypeName 'NodeApp' -Stateless -PartitionSchemeSingleton -InstanceCount 1

```

>[!TIP]
> <span data-ttu-id="132be-274">[Compactar pacote hello](service-fabric-package-apps.md#compress-a-package) antes de copiar o repositório de imagens toohello se o pacote de saudação é grande ou tem muitos arquivos.</span><span class="sxs-lookup"><span data-stu-id="132be-274">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store if hello package is large or has many files.</span></span> <span data-ttu-id="132be-275">Leia mais [aqui](service-fabric-deploy-remove-applications.md#upload-the-application-package).</span><span class="sxs-lookup"><span data-stu-id="132be-275">Read more [here](service-fabric-deploy-remove-applications.md#upload-the-application-package).</span></span>
>

<span data-ttu-id="132be-276">Um serviço do Service Fabric pode ser implantado em várias "configurações".</span><span class="sxs-lookup"><span data-stu-id="132be-276">A Service Fabric service can be deployed in various "configurations."</span></span> <span data-ttu-id="132be-277">Por exemplo, ele pode ser implantado como uma ou várias instâncias, ou pode ser implantado de forma que há uma instância do serviço de saudação em cada nó do cluster do Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="132be-277">For example, it can be deployed as single or multiple instances, or it can be deployed in such a way that there is one instance of hello service on each node of hello Service Fabric cluster.</span></span>

<span data-ttu-id="132be-278">Olá `InstanceCount` parâmetro hello `New-ServiceFabricService` cmdlet é usado toospecify quantas instâncias do serviço de saudação devem ser iniciadas no cluster do Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="132be-278">hello `InstanceCount` parameter of hello `New-ServiceFabricService` cmdlet is used toospecify how many instances of hello service should be launched in hello Service Fabric cluster.</span></span> <span data-ttu-id="132be-279">Você pode definir Olá `InstanceCount` valor, dependendo do tipo de saudação do aplicativo que você está implantando.</span><span class="sxs-lookup"><span data-stu-id="132be-279">You can set hello `InstanceCount` value, depending on hello type of application that you are deploying.</span></span> <span data-ttu-id="132be-280">Olá dois os cenários mais comuns são:</span><span class="sxs-lookup"><span data-stu-id="132be-280">hello two most common scenarios are:</span></span>

* <span data-ttu-id="132be-281">`InstanceCount = "1"`.</span><span class="sxs-lookup"><span data-stu-id="132be-281">`InstanceCount = "1"`.</span></span> <span data-ttu-id="132be-282">Nesse caso, apenas uma instância do serviço de saudação é implantada no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="132be-282">In this case, only one instance of hello service is deployed in hello cluster.</span></span> <span data-ttu-id="132be-283">Agendador do Service Fabric determina qual serviço de saudação do nó será toobe implantado em.</span><span class="sxs-lookup"><span data-stu-id="132be-283">Service Fabric's scheduler determines which node hello service is going toobe deployed on.</span></span>
* <span data-ttu-id="132be-284">`InstanceCount ="-1"`.</span><span class="sxs-lookup"><span data-stu-id="132be-284">`InstanceCount ="-1"`.</span></span> <span data-ttu-id="132be-285">Nesse caso, uma instância do serviço de saudação é implantada em cada nó no cluster do Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="132be-285">In this case, one instance of hello service is deployed on every node in hello Service Fabric cluster.</span></span> <span data-ttu-id="132be-286">resultado Hello está tendo um (e apenas um) instância do serviço de saudação para cada nó de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="132be-286">hello result is having one (and only one) instance of hello service for each node in hello cluster.</span></span>

<span data-ttu-id="132be-287">Essa é uma configuração útil para aplicativos front-end (por exemplo, um ponto de extremidade REST), porque aplicativos cliente precisam muito "conectar" tooany de nós de Olá no ponto de extremidade da saudação toouse Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="132be-287">This is a useful configuration for front-end applications (for example, a REST endpoint), because client applications need too"connect" tooany of hello nodes in hello cluster toouse hello endpoint.</span></span> <span data-ttu-id="132be-288">Essa configuração também pode ser usada quando, por exemplo, todos os nós do cluster do Service Fabric Olá são conectados tooa balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="132be-288">This configuration can also be used when, for example, all nodes of hello Service Fabric cluster are connected tooa load balancer.</span></span> <span data-ttu-id="132be-289">O tráfego do cliente, em seguida, pode ser distribuído em serviço Olá que está em execução em todos os nós no cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="132be-289">Client traffic can then be distributed across hello service that is running on all nodes in hello cluster.</span></span>

## <a name="check-your-running-application"></a><span data-ttu-id="132be-290">Verificar seu aplicativo em execução</span><span class="sxs-lookup"><span data-stu-id="132be-290">Check your running application</span></span>
<span data-ttu-id="132be-291">No Gerenciador do Service Fabric, identifica o nó de saudação onde o serviço hello está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="132be-291">In Service Fabric Explorer, identify hello node where hello service is running.</span></span> <span data-ttu-id="132be-292">Neste exemplo, ele está executando no Node1:</span><span class="sxs-lookup"><span data-stu-id="132be-292">In this example, it runs on Node1:</span></span>

![Nó em que o serviço está em execução](./media/service-fabric-deploy-existing-app/nodeappinsfx.png)

<span data-ttu-id="132be-294">Se você navegar nó toohello e procurar toohello aplicativo, você verá informações de nó essencial hello, incluindo sua localização no disco.</span><span class="sxs-lookup"><span data-stu-id="132be-294">If you navigate toohello node and browse toohello application, you see hello essential node information, including its location on disk.</span></span>

![Local no disco](./media/service-fabric-deploy-existing-app/locationondisk2.png)

<span data-ttu-id="132be-296">Se você procurar o diretório toohello usando o Gerenciador de servidores, você pode encontrar o diretório de trabalho hello e pasta de log do serviço hello, conforme mostrado no hello captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="132be-296">If you browse toohello directory by using Server Explorer, you can find hello working directory and hello service's log folder, as shown in hello following screenshot:</span></span> 

![Local do log](./media/service-fabric-deploy-existing-app/loglocation.png)

## <a name="next-steps"></a><span data-ttu-id="132be-298">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="132be-298">Next steps</span></span>
<span data-ttu-id="132be-299">Neste artigo, você aprendeu como toopackage um executável de convidado e implantá-lo tooService malha.</span><span class="sxs-lookup"><span data-stu-id="132be-299">In this article, you have learned how toopackage a guest executable and deploy it tooService Fabric.</span></span> <span data-ttu-id="132be-300">Consulte Olá artigos para tarefas e informações relacionadas a seguir.</span><span class="sxs-lookup"><span data-stu-id="132be-300">See hello following articles for related information and tasks.</span></span>

* <span data-ttu-id="132be-301">[Exemplo para empacotar e implantar um executável de convidado](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), incluindo uma versão de pré-lançamento do toohello de link da ferramenta de empacotamento Olá</span><span class="sxs-lookup"><span data-stu-id="132be-301">[Sample for packaging and deploying a guest executable](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), including a link toohello prerelease of hello packaging tool</span></span>
* [<span data-ttu-id="132be-302">Exemplo de dois convidado executáveis (c# e nodejs) se comunicar por meio do serviço de nomenclatura hello usando REST</span><span class="sxs-lookup"><span data-stu-id="132be-302">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
* [<span data-ttu-id="132be-303">Implantar vários executáveis de convidado</span><span class="sxs-lookup"><span data-stu-id="132be-303">Deploy multiple guest executables</span></span>](service-fabric-deploy-multiple-apps.md)
* [<span data-ttu-id="132be-304">Criar seu primeiro aplicativo do Service Fabric usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="132be-304">Create your first Service Fabric application using Visual Studio</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
