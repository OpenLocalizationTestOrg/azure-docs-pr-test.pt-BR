---
title: "Implantar um executável existente ao Service Fabric do Azure | Microsoft Docs"
description: "Instruções passo a passo sobre como empacotar um aplicativo existente como um executável de convidado, para que ele possa ser implantado em um cluster do Service Fabric"
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
ms.openlocfilehash: a1db3dda674ffe43587333d88f3816549af3019c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-guest-executable-to-service-fabric"></a><span data-ttu-id="b83fc-103">Implantar um executável convidado à Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b83fc-103">Deploy a guest executable to Service Fabric</span></span>
<span data-ttu-id="b83fc-104">Você pode executar qualquer tipo de código, como Node.js, Java ou C++ no Service Fabric como um serviço.</span><span class="sxs-lookup"><span data-stu-id="b83fc-104">You can run any type of code, such as Node.js, Java, or C++ in Azure Service Fabric as a service.</span></span> <span data-ttu-id="b83fc-105">O Service Fabric se refere a esses tipos de serviço como executáveis convidados.</span><span class="sxs-lookup"><span data-stu-id="b83fc-105">Service Fabric refers to these types of services as guest executables.</span></span>

<span data-ttu-id="b83fc-106">Os executáveis convidados são tratados pela Service Fabric como serviços sem monitoração de estado.</span><span class="sxs-lookup"><span data-stu-id="b83fc-106">Guest executables are treated by Service Fabric like stateless services.</span></span> <span data-ttu-id="b83fc-107">Como resultado, eles são colocados em nós em um cluster, com base na disponibilidade e em outras métricas.</span><span class="sxs-lookup"><span data-stu-id="b83fc-107">As a result, they are placed on nodes in a cluster, based on availability and other metrics.</span></span> <span data-ttu-id="b83fc-108">Este artigo descreve como empacotar e implantar um executável convidado em um cluster do Service Fabric usando o Visual Studio ou um utilitário de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="b83fc-108">This article describes how to package and deploy a guest executable to a Service Fabric cluster, by using Visual Studio or a command-line utility.</span></span>

<span data-ttu-id="b83fc-109">Neste artigo, abordaremos as etapas para empacotar um convidado executável e implantá-lo no Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b83fc-109">In this article, we cover the steps to package a guest executable and deploy it to Service Fabric.</span></span>  

## <a name="benefits-of-running-a-guest-executable-in-service-fabric"></a><span data-ttu-id="b83fc-110">Benefícios de executar um executável convidado no Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b83fc-110">Benefits of running a guest executable in Service Fabric</span></span>
<span data-ttu-id="b83fc-111">Há várias vantagens de executar um convidado executável em um cluster de Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="b83fc-111">There are several advantages to running a guest executable in a Service Fabric cluster:</span></span>

* <span data-ttu-id="b83fc-112">Alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="b83fc-112">High availability.</span></span> <span data-ttu-id="b83fc-113">Os aplicativos que são executados no Service Fabric estão no modo de alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="b83fc-113">Applications that run in Service Fabric are made highly available.</span></span> <span data-ttu-id="b83fc-114">O Service Fabric garante que as instâncias de um aplicativo estão em execução.</span><span class="sxs-lookup"><span data-stu-id="b83fc-114">Service Fabric ensures that instances of an application are running.</span></span>
* <span data-ttu-id="b83fc-115">Monitoramento de integridade.</span><span class="sxs-lookup"><span data-stu-id="b83fc-115">Health monitoring.</span></span> <span data-ttu-id="b83fc-116">O monitoramento de integridade do Service Fabric detecta se um aplicativo está em execução e fornece informações de diagnóstico se houver uma falha.</span><span class="sxs-lookup"><span data-stu-id="b83fc-116">Service Fabric health monitoring detects if an application is running, and provides diagnostic information if there is a failure.</span></span>   
* <span data-ttu-id="b83fc-117">Gerenciamento do ciclo de vida do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b83fc-117">Application lifecycle management.</span></span> <span data-ttu-id="b83fc-118">Além de oferecer atualizações sem tempo de inatividade, o Service Fabric fornecerá reversão automática da versão anterior, se houver um evento de integridade deficiente durante uma atualização.</span><span class="sxs-lookup"><span data-stu-id="b83fc-118">Besides providing upgrades with no downtime, Service Fabric provides automatic rollback to the previous version if there is a bad health event reported during an upgrade.</span></span>    
* <span data-ttu-id="b83fc-119">Densidade.</span><span class="sxs-lookup"><span data-stu-id="b83fc-119">Density.</span></span> <span data-ttu-id="b83fc-120">Você pode executar vários aplicativos no cluster, o que elimina a necessidade um hardware próprio para a execução de cada aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b83fc-120">You can run multiple applications in a cluster, which eliminates the need for each application to run on its own hardware.</span></span>
* <span data-ttu-id="b83fc-121">Capacidade de descoberta: usando o REST, você pode chamar o serviço Nomenclatura do Service Fabric para localizar outros serviços no cluster.</span><span class="sxs-lookup"><span data-stu-id="b83fc-121">Discoverability: Using REST you can call the Service Fabric Naming service to find other services in the cluster.</span></span> 

## <a name="samples"></a><span data-ttu-id="b83fc-122">Exemplos</span><span class="sxs-lookup"><span data-stu-id="b83fc-122">Samples</span></span>
* [<span data-ttu-id="b83fc-123">Exemplo de empacotamento e implantação de um executável convidado</span><span class="sxs-lookup"><span data-stu-id="b83fc-123">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="b83fc-124">Exemplo de dois executáveis convidados (C# e nodejs) se comunicando por meio do Serviço de nomenclatura usando REST</span><span class="sxs-lookup"><span data-stu-id="b83fc-124">Sample of two guest executables (C# and nodejs) communicating via the Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="overview-of-application-and-service-manifest-files"></a><span data-ttu-id="b83fc-125">Visão geral do aplicativo e dos arquivos de manifesto do serviço</span><span class="sxs-lookup"><span data-stu-id="b83fc-125">Overview of application and service manifest files</span></span>
<span data-ttu-id="b83fc-126">Como parte da implantação de um executável convidado, é útil entender o modelo de implantação e empacotamento do Service Fabric conforme descrito no [modelo de aplicativo](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="b83fc-126">As part of deploying a guest executable, it is useful to understand the Service Fabric packaging and deployment model as described in [application model](service-fabric-application-model.md).</span></span> <span data-ttu-id="b83fc-127">O modelo de empacotamento do Service Fabric depende de dois arquivos XML: o aplicativo e o manifesto do serviço.</span><span class="sxs-lookup"><span data-stu-id="b83fc-127">The Service Fabric packaging model relies on two XML files: the application and service manifests.</span></span> <span data-ttu-id="b83fc-128">A definição de esquema dos arquivos ApplicationManifest.xml e ServiceManifest.xml é instalada com o SDK do Service Fabric em *C:\Arquivos de Programas\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="b83fc-128">The schema definition for the ApplicationManifest.xml and ServiceManifest.xml files is installed with the Service Fabric SDK into *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

* <span data-ttu-id="b83fc-129">**Manifesto do aplicativo** O manifesto do aplicativo é usado para descrever o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b83fc-129">**Application manifest** The application manifest is used to describe the application.</span></span> <span data-ttu-id="b83fc-130">Ele lista os serviços que o compõem e os outros parâmetros usados para definir como um ou mais serviços devem ser implantados, como o número de instâncias.</span><span class="sxs-lookup"><span data-stu-id="b83fc-130">It lists the services that compose it, and other parameters that are used to define how one or more services should be deployed, such as the number of instances.</span></span>

  <span data-ttu-id="b83fc-131">No Service Fabric, um aplicativo é uma unidade de implantação e atualização.</span><span class="sxs-lookup"><span data-stu-id="b83fc-131">In Service Fabric, an application is a unit of deployment and upgrade.</span></span> <span data-ttu-id="b83fc-132">Um aplicativo pode ser atualizado como uma única unidade em que falhas e reversões potencias são gerenciadas.</span><span class="sxs-lookup"><span data-stu-id="b83fc-132">An application can be upgraded as a single unit where potential failures and potential rollbacks are managed.</span></span> <span data-ttu-id="b83fc-133">O Service Fabric garante que o processo de atualização seja completamente bem-sucedido ou, se a atualização falhar, ele não deixará o aplicativo em um estado desconhecido/instável.</span><span class="sxs-lookup"><span data-stu-id="b83fc-133">Service Fabric guarantees that the upgrade process is either successful, or, if the upgrade fails, does not leave the application in an unknown or unstable state.</span></span>
* <span data-ttu-id="b83fc-134">**Manifesto do serviço** O manifesto do serviço descreve os componentes de um serviço.</span><span class="sxs-lookup"><span data-stu-id="b83fc-134">**Service manifest** The service manifest describes the components of a service.</span></span> <span data-ttu-id="b83fc-135">Ele inclui dados como o nome e o tipo do serviço e seu código e configuração.</span><span class="sxs-lookup"><span data-stu-id="b83fc-135">It includes data, such as the name and type of service, and its code and configuration.</span></span> <span data-ttu-id="b83fc-136">O manifesto do serviço também inclui alguns parâmetros adicionais que podem ser usados para configurar o serviço após sua implantação.</span><span class="sxs-lookup"><span data-stu-id="b83fc-136">The service manifest also includes some additional parameters that can be used to configure the service once it is deployed.</span></span>

## <a name="application-package-file-structure"></a><span data-ttu-id="b83fc-137">Estrutura de arquivos do pacote de aplicativos</span><span class="sxs-lookup"><span data-stu-id="b83fc-137">Application package file structure</span></span>
<span data-ttu-id="b83fc-138">Para implantar um aplicativo no Service Fabric, o aplicativo deve seguir uma estrutura de diretórios predefinida.</span><span class="sxs-lookup"><span data-stu-id="b83fc-138">To deploy an application to Service Fabric, the application should follow a predefined directory structure.</span></span> <span data-ttu-id="b83fc-139">A seguir está um exemplo dessa estrutura.</span><span class="sxs-lookup"><span data-stu-id="b83fc-139">The following is an example of that structure.</span></span>

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

<span data-ttu-id="b83fc-140">O ApplicationPackageRoot contém o arquivo ApplicationManifest.xml que define o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b83fc-140">The ApplicationPackageRoot contains the ApplicationManifest.xml file that defines the application.</span></span> <span data-ttu-id="b83fc-141">Um subdiretório para cada serviço incluído no aplicativo é usado para conter todos os artefatos que o serviço requer.</span><span class="sxs-lookup"><span data-stu-id="b83fc-141">A subdirectory for each service included in the application is used to contain all the artifacts that the service requires.</span></span> <span data-ttu-id="b83fc-142">Esses subdiretórios são ServiceManifest.xml e, normalmente, o seguinte:</span><span class="sxs-lookup"><span data-stu-id="b83fc-142">These subdirectories are the ServiceManifest.xml and, typically, the following:</span></span>

* <span data-ttu-id="b83fc-143">*Código*.</span><span class="sxs-lookup"><span data-stu-id="b83fc-143">*Code*.</span></span> <span data-ttu-id="b83fc-144">Esse diretório contém o código de serviço.</span><span class="sxs-lookup"><span data-stu-id="b83fc-144">This directory contains the service code.</span></span>
* <span data-ttu-id="b83fc-145">*Config*.</span><span class="sxs-lookup"><span data-stu-id="b83fc-145">*Config*.</span></span> <span data-ttu-id="b83fc-146">Esse diretório contém o arquivo Settings.xml (e outros arquivos, se necessário) que o serviço pode acessar no tempo de execução para recuperar definições de configuração específicas.</span><span class="sxs-lookup"><span data-stu-id="b83fc-146">This directory contains a Settings.xml file (and other files if necessary) that the service can access at runtime to retrieve specific configuration settings.</span></span>
* <span data-ttu-id="b83fc-147">*Dados*.</span><span class="sxs-lookup"><span data-stu-id="b83fc-147">*Data*.</span></span> <span data-ttu-id="b83fc-148">Esse é um diretório adicional para armazenar dados locais adicionais que podem ser necessário para o serviço.</span><span class="sxs-lookup"><span data-stu-id="b83fc-148">This is an additional directory to store additional local data that the service may need.</span></span> <span data-ttu-id="b83fc-149">Os dados devem ser usados para armazenar somente dados efêmeros.</span><span class="sxs-lookup"><span data-stu-id="b83fc-149">Data should be used to store only ephemeral data.</span></span> <span data-ttu-id="b83fc-150">O Service Fabric não copia nem replica alterações ao diretório de dados se o serviço precisar ser realocado (por exemplo, durante o failover).</span><span class="sxs-lookup"><span data-stu-id="b83fc-150">Service Fabric does not copy or replicate changes to the data directory if the service needs to be relocated (for example, during failover).</span></span>

> [!NOTE]
> <span data-ttu-id="b83fc-151">Você não precisa criar os diretórios `config` e `data` se não precisar deles.</span><span class="sxs-lookup"><span data-stu-id="b83fc-151">You don't have to create the `config` and `data` directories if you don't need them.</span></span>
>
>

## <a name="package-an-existing-executable"></a><span data-ttu-id="b83fc-152">Empacotar um executável existente</span><span class="sxs-lookup"><span data-stu-id="b83fc-152">Package an existing executable</span></span>
<span data-ttu-id="b83fc-153">Ao empacotar um executável convidado, você pode optar por usar um modelo de projeto do Visual Studio ou [criar o pacote de aplicativos manualmente](#manually).</span><span class="sxs-lookup"><span data-stu-id="b83fc-153">When packaging a guest executable, you can choose either to use a Visual Studio project template or to [create the application package manually](#manually).</span></span> <span data-ttu-id="b83fc-154">Usando o Visual Studio, a estrutura do pacote de aplicativos e os arquivos de manifesto são criados pelo novo modelo de projeto para você.</span><span class="sxs-lookup"><span data-stu-id="b83fc-154">Using Visual Studio, the application package structure and manifest files are created by the new project template for you.</span></span>

> [!TIP]
> <span data-ttu-id="b83fc-155">A maneira mais fácil de empacotar um executável existente do Windows em um serviço é usar o Visual Studio e, no Linux, usar o Yeoman</span><span class="sxs-lookup"><span data-stu-id="b83fc-155">The easiest way to package an existing Windows executable into a service is to use Visual Studio and on Linux to use Yeoman</span></span>
>

## <a name="use-visual-studio-to-package-and-deploy-an-existing-executable"></a><span data-ttu-id="b83fc-156">Usar o Visual Studio para empacotar e implantar um executável existente</span><span class="sxs-lookup"><span data-stu-id="b83fc-156">Use Visual Studio to package and deploy an existing executable</span></span>
<span data-ttu-id="b83fc-157">O Visual Studio fornece um modelo de serviço do Service Fabric para ajudar você a implantar um executável convidado em um cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b83fc-157">Visual Studio provides a Service Fabric service template to help you deploy a guest executable to a Service Fabric cluster.</span></span>

1. <span data-ttu-id="b83fc-158">Escolha **Arquivo** > **Novo Projeto** e crie um aplicativo de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b83fc-158">Choose **File** > **New Project**, and create a Service Fabric application.</span></span>
2. <span data-ttu-id="b83fc-159">Escolha **Executável Convidado** como o modelo de serviço.</span><span class="sxs-lookup"><span data-stu-id="b83fc-159">Choose **Guest Executable** as the service template.</span></span>
3. <span data-ttu-id="b83fc-160">Clique em **Procurar** para selecionar a pasta com o executável e preencha o restante dos parâmetros para criar o serviço.</span><span class="sxs-lookup"><span data-stu-id="b83fc-160">Click **Browse** to select the folder with your executable and fill in the rest of the parameters to create the service.</span></span>
   * <span data-ttu-id="b83fc-161">*Comportamento do Pacote de Código*.</span><span class="sxs-lookup"><span data-stu-id="b83fc-161">*Code Package Behavior*.</span></span> <span data-ttu-id="b83fc-162">Pode ser definido para copiar todo o conteúdo da pasta para o Projeto do Visual Studio, o que será útil se o executável não mudar.</span><span class="sxs-lookup"><span data-stu-id="b83fc-162">Can be set to copy all the content of your folder to the Visual Studio Project, which is useful if the executable does not change.</span></span> <span data-ttu-id="b83fc-163">Se você espera que o executável mude e se quiser a capacidade de obter novas compilações dinamicamente, poderá optar por vincular para a pasta.</span><span class="sxs-lookup"><span data-stu-id="b83fc-163">If you expect the executable to change and want the ability to pick up new builds dynamically, you can choose to link to the folder instead.</span></span> <span data-ttu-id="b83fc-164">Você pode usar pastas vinculadas ao criar o projeto de aplicativo no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b83fc-164">You can use linked folders when creating the application project in Visual Studio.</span></span> <span data-ttu-id="b83fc-165">Isso cria um vínculo com o local de origem de dentro do projeto, tornando possível atualizar o executável convidado em seu destino de origem.</span><span class="sxs-lookup"><span data-stu-id="b83fc-165">This links to the source location from within the project, making it possible for you to update the guest executable in its source destination.</span></span> <span data-ttu-id="b83fc-166">Essas atualizações se tornam parte do pacote de aplicativo no build.</span><span class="sxs-lookup"><span data-stu-id="b83fc-166">Those updates become part of the application package on build.</span></span>
   * <span data-ttu-id="b83fc-167">*Programa* especifica o executável que deve ser executado para iniciar o serviço.</span><span class="sxs-lookup"><span data-stu-id="b83fc-167">*Program* specifies the executable that should be run to start the service.</span></span>
   * <span data-ttu-id="b83fc-168">*Argumentos* especificam os argumentos que devem ser passados para o executável.</span><span class="sxs-lookup"><span data-stu-id="b83fc-168">*Arguments* specifies the arguments that should be passed to the executable.</span></span> <span data-ttu-id="b83fc-169">Pode ser uma lista de parâmetros com argumentos.</span><span class="sxs-lookup"><span data-stu-id="b83fc-169">It can be a list of parameters with arguments.</span></span>
   * <span data-ttu-id="b83fc-170">*WorkingFolder* especifica o diretório de trabalho para o processo que será iniciado.</span><span class="sxs-lookup"><span data-stu-id="b83fc-170">*WorkingFolder* specifies the working directory for the process that is going to be started.</span></span> <span data-ttu-id="b83fc-171">Você pode especificar três valores:</span><span class="sxs-lookup"><span data-stu-id="b83fc-171">You can specify three values:</span></span>
     * <span data-ttu-id="b83fc-172">`CodeBase` especifica que o diretório de trabalho será definido no diretório de código no pacote de aplicativos (diretório `Code` mostrado na estrutura de arquivos anterior).</span><span class="sxs-lookup"><span data-stu-id="b83fc-172">`CodeBase` specifies that the working directory is going to be set to the code directory in the application package (`Code` directory shown in the preceding file structure).</span></span>
     * <span data-ttu-id="b83fc-173">`CodePackage` especifica que o diretório de trabalho será definido como a raiz do pacote de aplicativos (`GuestService1Pkg` mostrado na estrutura de arquivos anterior).</span><span class="sxs-lookup"><span data-stu-id="b83fc-173">`CodePackage` specifies that the working directory is going to be set to the root of the application package    (`GuestService1Pkg` shown in the preceding file structure).</span></span>
     * <span data-ttu-id="b83fc-174">`Work` especifica que os arquivos são colocados em um subdiretório chamado trabalho.</span><span class="sxs-lookup"><span data-stu-id="b83fc-174">`Work` specifies that the files are placed in a subdirectory called work.</span></span>
4. <span data-ttu-id="b83fc-175">Dê um nome ao seu serviço e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="b83fc-175">Give your service a name, and click **OK**.</span></span>
5. <span data-ttu-id="b83fc-176">Se seu serviço precisar de um ponto de extremidade para comunicação, você é possível adicionar o protocolo, a porta e o tipo ao arquivo ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="b83fc-176">If your service needs an endpoint for communication, you can now add the protocol, port, and type to the ServiceManifest.xml file.</span></span> <span data-ttu-id="b83fc-177">Por exemplo: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.</span><span class="sxs-lookup"><span data-stu-id="b83fc-177">For example: `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.</span></span>
6. <span data-ttu-id="b83fc-178">Agora você pode usar o pacote e publicar a ação em seu cluster local ao depurar a solução no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b83fc-178">You can now use the package and publish action against your local cluster by debugging the solution in Visual Studio.</span></span> <span data-ttu-id="b83fc-179">Quando estiver pronto, você poderá publicar o aplicativo em um cluster remoto ou fazer check-in da solução para o controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="b83fc-179">When ready, you can publish the application to a remote cluster or check in the solution to source control.</span></span>
7. <span data-ttu-id="b83fc-180">Vá para o final deste artigo para conferir como exibir seu serviço executável de convidado em execução no Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="b83fc-180">Go to the end of this article to see how to view your guest executable service running in Service Fabric Explorer.</span></span>

## <a name="use-yoeman-to-package-and-deploy-an-existing-executable-on-linux"></a><span data-ttu-id="b83fc-181">Usar o Yeoman para empacotar e implantar um executável existente no Linux</span><span class="sxs-lookup"><span data-stu-id="b83fc-181">Use Yoeman to package and deploy an existing executable on Linux</span></span>

<span data-ttu-id="b83fc-182">O procedimento para criar e implantar um executável convidado no Linux é igual à implantação de um aplicativo csharp ou java.</span><span class="sxs-lookup"><span data-stu-id="b83fc-182">The procedure for creating and deploying a guest executable on Linux is the same as deploying a csharp or java application.</span></span>

1. <span data-ttu-id="b83fc-183">Em um terminal, digite `yo azuresfguest`.</span><span class="sxs-lookup"><span data-stu-id="b83fc-183">In a terminal, type `yo azuresfguest`.</span></span>
2. <span data-ttu-id="b83fc-184">Nome do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b83fc-184">Name your application.</span></span>
3. <span data-ttu-id="b83fc-185">Nomeie o serviço e forneça os detalhes, incluindo o caminho do executável e os parâmetros com os quais ele deve ser invocado.</span><span class="sxs-lookup"><span data-stu-id="b83fc-185">Name your service, and provide the details including path of the executable and the parameters it must be invoked with.</span></span>

<span data-ttu-id="b83fc-186">O Yeoman cria um pacote de aplicativos com os devidos arquivos de aplicativo e manifesto juntamente com a instalação e desinstalação dos scripts.</span><span class="sxs-lookup"><span data-stu-id="b83fc-186">Yeoman creates an application package with the appropriate application and manifest files along with install and uninstall scripts.</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-an-existing-executable"></a><span data-ttu-id="b83fc-187">Empacotar e implantar manualmente um executável existente</span><span class="sxs-lookup"><span data-stu-id="b83fc-187">Manually package and deploy an existing executable</span></span>
<span data-ttu-id="b83fc-188">O processo de empacotar manualmente um executável convidado baseia-se nas seguintes etapas gerais:</span><span class="sxs-lookup"><span data-stu-id="b83fc-188">The process of manually packaging a guest executable is based on the following general steps:</span></span>

1. <span data-ttu-id="b83fc-189">Criar a estrutura de diretórios do pacote.</span><span class="sxs-lookup"><span data-stu-id="b83fc-189">Create the package directory structure.</span></span>
2. <span data-ttu-id="b83fc-190">Adicionar os arquivos de configuração e código do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b83fc-190">Add the application's code and configuration files.</span></span>
3. <span data-ttu-id="b83fc-191">Editar o arquivo de manifesto do serviço.</span><span class="sxs-lookup"><span data-stu-id="b83fc-191">Edit the service manifest file.</span></span>
4. <span data-ttu-id="b83fc-192">Editar o arquivo de manifesto do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b83fc-192">Edit the application manifest file.</span></span>

<!--
>[AZURE.NOTE] We do provide a packaging tool that allows you to create the ApplicationPackage automatically. The tool is currently in preview. You can download it from [here](http://aka.ms/servicefabricpacktool).
-->

### <a name="create-the-package-directory-structure"></a><span data-ttu-id="b83fc-193">Criar a estrutura de diretórios do pacote</span><span class="sxs-lookup"><span data-stu-id="b83fc-193">Create the package directory structure</span></span>
<span data-ttu-id="b83fc-194">Você pode iniciar criando a estrutura de diretório, conforme descrito na seção anterior, "Estrutura de arquivo de pacote de aplicativo".</span><span class="sxs-lookup"><span data-stu-id="b83fc-194">You can start by creating the directory structure, as described in the preceding section, "Application package file structure."</span></span>

### <a name="add-the-applications-code-and-configuration-files"></a><span data-ttu-id="b83fc-195">Adicionar os arquivos de configuração e código do aplicativo</span><span class="sxs-lookup"><span data-stu-id="b83fc-195">Add the application's code and configuration files</span></span>
<span data-ttu-id="b83fc-196">Depois de criar a estrutura de diretório, você pode adicionar os arquivos de configuração e código do aplicativo aos diretórios de code e config.</span><span class="sxs-lookup"><span data-stu-id="b83fc-196">After you have created the directory structure, you can add the application's code and configuration files under the code and config directories.</span></span> <span data-ttu-id="b83fc-197">Também é possível criar diretórios adicionais ou subdiretórios nos diretórios code ou config.</span><span class="sxs-lookup"><span data-stu-id="b83fc-197">You can also create additional directories or subdirectories under the code or config directories.</span></span>

<span data-ttu-id="b83fc-198">O Service Fabric faz uma `xcopy` do conteúdo do diretório raiz do aplicativo, portanto, não há estrutura predefinida a usar que não criar dois diretórios principais, código e configurações.</span><span class="sxs-lookup"><span data-stu-id="b83fc-198">Service Fabric does an `xcopy` of the content of the application root directory, so there is no predefined structure to use other than creating two top directories, code and settings.</span></span> <span data-ttu-id="b83fc-199">(Você pode escolher nomes diferentes, se desejar.</span><span class="sxs-lookup"><span data-stu-id="b83fc-199">(You can pick different names if you want.</span></span> <span data-ttu-id="b83fc-200">Mais detalhes estão na próxima seção.)</span><span class="sxs-lookup"><span data-stu-id="b83fc-200">More details are in the next section.)</span></span>

> [!NOTE]
> <span data-ttu-id="b83fc-201">Inclua todos os arquivos e dependências de que o aplicativo precisa.</span><span class="sxs-lookup"><span data-stu-id="b83fc-201">Make sure that you include all the files and dependencies that the application needs.</span></span> <span data-ttu-id="b83fc-202">O Service Fabric copia o conteúdo do pacote de aplicativos em todos os nós do cluster nos quais os serviços do aplicativo serão implantados.</span><span class="sxs-lookup"><span data-stu-id="b83fc-202">Service Fabric copies the content of the application package on all nodes in the cluster where the application's services are going to be deployed.</span></span> <span data-ttu-id="b83fc-203">O pacote deve conter todos os códigos que o aplicativo precisa para ser executado.</span><span class="sxs-lookup"><span data-stu-id="b83fc-203">The package should contain all the code that the application needs to run.</span></span> <span data-ttu-id="b83fc-204">Não presuma que as dependências já estão instaladas.</span><span class="sxs-lookup"><span data-stu-id="b83fc-204">Do not assume that the dependencies are already installed.</span></span>
>
>

### <a name="edit-the-service-manifest-file"></a><span data-ttu-id="b83fc-205">Editar o arquivo de manifesto do serviço</span><span class="sxs-lookup"><span data-stu-id="b83fc-205">Edit the service manifest file</span></span>
<span data-ttu-id="b83fc-206">A próxima etapa é editar o arquivo de manifesto do serviço para incluir as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="b83fc-206">The next step is to edit the service manifest file to include the following information:</span></span>

* <span data-ttu-id="b83fc-207">O nome da fila do tipo de serviço.</span><span class="sxs-lookup"><span data-stu-id="b83fc-207">The name of the service type.</span></span> <span data-ttu-id="b83fc-208">Esse é um ID que o Service Fabric usa para identificar um serviço.</span><span class="sxs-lookup"><span data-stu-id="b83fc-208">This is an ID that Service Fabric uses to identify a service.</span></span>
* <span data-ttu-id="b83fc-209">O comando a ser usado para iniciar o aplicativo (ExeHost).</span><span class="sxs-lookup"><span data-stu-id="b83fc-209">The command to use to launch the application (ExeHost).</span></span>
* <span data-ttu-id="b83fc-210">Qualquer script que precisa ser executado para configurar o aplicativo (SetupEntrypoint).</span><span class="sxs-lookup"><span data-stu-id="b83fc-210">Any script that needs to be run to set up the application (SetupEntrypoint).</span></span>

<span data-ttu-id="b83fc-211">Segue um exemplo de um arquivo `ServiceManifest.xml` :</span><span class="sxs-lookup"><span data-stu-id="b83fc-211">The following is an example of a `ServiceManifest.xml` file:</span></span>

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

<span data-ttu-id="b83fc-212">As seções a seguir repassam as diferente partes do arquivo que você precisa atualizar.</span><span class="sxs-lookup"><span data-stu-id="b83fc-212">The following sections go over the different parts of the file that you need to update.</span></span>

#### <a name="update-servicetypes"></a><span data-ttu-id="b83fc-213">Atualizar ServiceTypes</span><span class="sxs-lookup"><span data-stu-id="b83fc-213">Update ServiceTypes</span></span>
```xml
<ServiceTypes>
  <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true" />
</ServiceTypes>
```

* <span data-ttu-id="b83fc-214">Você pode escolher qualquer nome que desejar para `ServiceTypeName`.</span><span class="sxs-lookup"><span data-stu-id="b83fc-214">You can pick any name that you want for `ServiceTypeName`.</span></span> <span data-ttu-id="b83fc-215">O valor é usado no arquivo `ApplicationManifest.xml` para identificar o serviço.</span><span class="sxs-lookup"><span data-stu-id="b83fc-215">The value is used in the `ApplicationManifest.xml` file to identify the service.</span></span>
* <span data-ttu-id="b83fc-216">Especifique `UseImplicitHost="true"`.</span><span class="sxs-lookup"><span data-stu-id="b83fc-216">Specify `UseImplicitHost="true"`.</span></span> <span data-ttu-id="b83fc-217">Esse atributo informa ao Service Fabric que o serviço se baseia em um aplicativo independente, de modo tudo o que o Service Fabric precisa fazer é iniciá-lo como um processo e monitorar a integridade.</span><span class="sxs-lookup"><span data-stu-id="b83fc-217">This attribute tells Service Fabric that the service is based on a self-contained app, so all Service Fabric needs to do is to launch it as a process and monitor its health.</span></span>

#### <a name="update-codepackage"></a><span data-ttu-id="b83fc-218">Atualizar CodePackage</span><span class="sxs-lookup"><span data-stu-id="b83fc-218">Update CodePackage</span></span>
<span data-ttu-id="b83fc-219">O elemento CodePackage especifica o local (e a versão) do código do serviço.</span><span class="sxs-lookup"><span data-stu-id="b83fc-219">The CodePackage element specifies the location (and version) of the service's code.</span></span>

```xml
<CodePackage Name="Code" Version="1.0.0.0">
```

<span data-ttu-id="b83fc-220">O elemento `Name` é usado para especificar o nome do diretório no pacote de aplicativos que contém o código do serviço.</span><span class="sxs-lookup"><span data-stu-id="b83fc-220">The `Name` element is used to specify the name of the directory in the application package that contains the service's code.</span></span> <span data-ttu-id="b83fc-221">`CodePackage` também tem o atributo `version`.</span><span class="sxs-lookup"><span data-stu-id="b83fc-221">`CodePackage` also has the `version` attribute.</span></span> <span data-ttu-id="b83fc-222">Isso pode ser usado para especificar a versão do código e também pode ser usado para atualizar o código do serviço usando a infraestrutura de gerenciamento de ciclo de vida de aplicativo no Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b83fc-222">This can be used to specify the version of the code, and can also potentially be used to upgrade the service's code by using the application lifecycle management infrastructure in Service Fabric.</span></span>

#### <a name="optional-update-setupentrypoint"></a><span data-ttu-id="b83fc-223">Opcional: atualizar SetupEntrypoint</span><span class="sxs-lookup"><span data-stu-id="b83fc-223">Optional: Update SetupEntrypoint</span></span>
```xml
<SetupEntryPoint>
   <ExeHost>
       <Program>scripts\launchConfig.cmd</Program>
   </ExeHost>
</SetupEntryPoint>
```
<span data-ttu-id="b83fc-224">O elemento SetupEntryPoint é usado para especificar qualquer executável ou arquivo em lotes que precise ser executado antes da inicialização do código do serviço.</span><span class="sxs-lookup"><span data-stu-id="b83fc-224">The SetupEntryPoint element is used to specify any executable or batch file that should be executed before the service's code is launched.</span></span> <span data-ttu-id="b83fc-225">É uma etapa opcional, de modo que não precisa ser incluída se não houver necessidade de inicialização.</span><span class="sxs-lookup"><span data-stu-id="b83fc-225">It is an optional step, so it does not need to be included if there is no initialization required.</span></span> <span data-ttu-id="b83fc-226">O SetupEntrypoint é executado toda vez que o serviço é reiniciado.</span><span class="sxs-lookup"><span data-stu-id="b83fc-226">The SetupEntryPoint is executed every time the service is restarted.</span></span>

<span data-ttu-id="b83fc-227">Há apenas um SetupEntryPoint, de modo que os scripts de instalação precisarão ser agrupados em um único arquivo em lotes se a instalação do aplicativo exigir vários scripts.</span><span class="sxs-lookup"><span data-stu-id="b83fc-227">There is only one SetupEntryPoint, so setup scripts need to be grouped in a single batch file if the application's setup requires multiple scripts.</span></span> <span data-ttu-id="b83fc-228">O SetupEntryPoint pode executar qualquer tipo de arquivo: arquivos executáveis, arquivos em lotes e cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b83fc-228">The SetupEntryPoint can execute any type of file: executable files, batch files, and PowerShell cmdlets.</span></span> <span data-ttu-id="b83fc-229">Para obter mais detalhes, confira [Configure SetupEntryPoint](service-fabric-application-runas-security.md)(Configurar SetupEntryPoint).</span><span class="sxs-lookup"><span data-stu-id="b83fc-229">For more details, see [Configure SetupEntryPoint](service-fabric-application-runas-security.md).</span></span>

<span data-ttu-id="b83fc-230">No exemplo anterior, o SetupEntryPoint executa um arquivo em lote chamado `LaunchConfig.cmd`, que está localizado no subdiretório `scripts` do diretório de código (supondo que o elemento WorkingFolder esteja definido como CodeBase).</span><span class="sxs-lookup"><span data-stu-id="b83fc-230">In the preceding example, the SetupEntryPoint runs a batch file called `LaunchConfig.cmd` that is located in the `scripts` subdirectory of the code directory (assuming the WorkingFolder element is set to CodeBase).</span></span>

#### <a name="update-entrypoint"></a><span data-ttu-id="b83fc-231">Atualizar EntryPoint</span><span class="sxs-lookup"><span data-stu-id="b83fc-231">Update EntryPoint</span></span>
```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
  </ExeHost>
</EntryPoint>
```

<span data-ttu-id="b83fc-232">O elemento `EntryPoint` no arquivo de manifesto do serviço é usado para especificar como iniciar o serviço.</span><span class="sxs-lookup"><span data-stu-id="b83fc-232">The `EntryPoint` element in the service manifest file is used to specify how to launch the service.</span></span> <span data-ttu-id="b83fc-233">O elemento `ExeHost` especifica o executável e os argumentos que devem ser usados para iniciar o serviço.</span><span class="sxs-lookup"><span data-stu-id="b83fc-233">The `ExeHost` element specifies the executable (and arguments) that should be used to launch the service.</span></span>

* <span data-ttu-id="b83fc-234">`Program` especifica o nome do executável que deve iniciar o serviço.</span><span class="sxs-lookup"><span data-stu-id="b83fc-234">`Program` specifies the name of the executable that should start the service.</span></span>
* <span data-ttu-id="b83fc-235">`Arguments` especifica os argumentos que devem ser passados para o executável.</span><span class="sxs-lookup"><span data-stu-id="b83fc-235">`Arguments` specifies the arguments that should be passed to the executable.</span></span> <span data-ttu-id="b83fc-236">Pode ser uma lista de parâmetros com argumentos.</span><span class="sxs-lookup"><span data-stu-id="b83fc-236">It can be a list of parameters with arguments.</span></span>
* <span data-ttu-id="b83fc-237">`WorkingFolder` especifica o diretório de trabalho para o processo que será iniciado.</span><span class="sxs-lookup"><span data-stu-id="b83fc-237">`WorkingFolder` specifies the working directory for the process that is going to be started.</span></span> <span data-ttu-id="b83fc-238">Você pode especificar três valores:</span><span class="sxs-lookup"><span data-stu-id="b83fc-238">You can specify three values:</span></span>
  * <span data-ttu-id="b83fc-239">`CodeBase` especifica que o diretório de trabalho será definido no diretório de código no pacote de aplicativos (diretório `Code` na estrutura de arquivos anterior).</span><span class="sxs-lookup"><span data-stu-id="b83fc-239">`CodeBase` specifies that the working directory is going to be set to the code directory in the application package (`Code` directory in the preceding file structure).</span></span>
  * <span data-ttu-id="b83fc-240">`CodePackage` especifica que o diretório de trabalho será definido como a raiz do pacote de aplicativos (`GuestService1Pkg` na estrutura de arquivos anterior).</span><span class="sxs-lookup"><span data-stu-id="b83fc-240">`CodePackage` specifies that the working directory is going to be set to the root of the application package    (`GuestService1Pkg` in the preceding file structure).</span></span>
    * <span data-ttu-id="b83fc-241">`Work` especifica que os arquivos são colocados em um subdiretório chamado trabalho.</span><span class="sxs-lookup"><span data-stu-id="b83fc-241">`Work` specifies that the files are placed in a subdirectory called work.</span></span>

<span data-ttu-id="b83fc-242">A WorkingFolder é útil para definir o diretório de trabalho correto, de modo que os caminhos relativos possam ser usados pelo aplicativo ou pelos scripts de inicialização.</span><span class="sxs-lookup"><span data-stu-id="b83fc-242">The WorkingFolder is useful to set the correct working directory so that relative paths can be used by either the application or initialization scripts.</span></span>

#### <a name="update-endpoints-and-register-with-naming-service-for-communication"></a><span data-ttu-id="b83fc-243">Atualizar pontos de extremidade e registrar com o Serviço de Nomenclatura para comunicação</span><span class="sxs-lookup"><span data-stu-id="b83fc-243">Update Endpoints and register with Naming Service for communication</span></span>
```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
</Endpoints>

```
<span data-ttu-id="b83fc-244">No exemplo anterior, o elemento `Endpoint` especifica os pontos de extremidade nos quais o aplicativo pode escutar.</span><span class="sxs-lookup"><span data-stu-id="b83fc-244">In the preceding example, the `Endpoint` element specifies the endpoints that the application can listen on.</span></span> <span data-ttu-id="b83fc-245">Neste exemplo, o aplicativo Node.js escuta ao http na porta 3000.</span><span class="sxs-lookup"><span data-stu-id="b83fc-245">In this example, the Node.js application listens on http on port 3000.</span></span>

<span data-ttu-id="b83fc-246">Além disso, você pode solicitar ao Service Fabric para publicar este ponto de extremidade no Serviço de Cadastramento, de modo que outros serviços possam descobrir o endereço do ponto de extremidade deste serviço.</span><span class="sxs-lookup"><span data-stu-id="b83fc-246">Furthermore you can ask Service Fabric to publish this endpoint to the Naming Service so other services can discover the endpoint address to this service.</span></span> <span data-ttu-id="b83fc-247">Isso permite que você se comunique entre os serviços que são executáveis de convidado.</span><span class="sxs-lookup"><span data-stu-id="b83fc-247">This enables you to be able to communicate between services that are guest executables.</span></span>
<span data-ttu-id="b83fc-248">O endereço do ponto de extremidade publicado está no formato `UriScheme://IPAddressOrFQDN:Port/PathSuffix`.</span><span class="sxs-lookup"><span data-stu-id="b83fc-248">The published endpoint address is of the form `UriScheme://IPAddressOrFQDN:Port/PathSuffix`.</span></span> <span data-ttu-id="b83fc-249">`UriScheme` e `PathSuffix` são atributos opcionais.</span><span class="sxs-lookup"><span data-stu-id="b83fc-249">`UriScheme` and `PathSuffix` are optional attributes.</span></span> <span data-ttu-id="b83fc-250">`IPAddressOrFQDN` é o Endereço IP ou o nome de domínio totalmente qualificado do nó em que esse executável é colocado e calculado para você.</span><span class="sxs-lookup"><span data-stu-id="b83fc-250">`IPAddressOrFQDN` is the IP address or fully qualified domain name of the node this executable gets placed on, and it is calculated for you.</span></span>

<span data-ttu-id="b83fc-251">No exemplo a seguir, quando o serviço for implantado no Service Fabric Explorer, você verá um ponto de extremidade semelhante ao `http://10.1.4.92:3000/myapp/` publicado para a instância de serviço.</span><span class="sxs-lookup"><span data-stu-id="b83fc-251">In the following example, once the service is deployed, in Service Fabric Explorer you see an endpoint similar to `http://10.1.4.92:3000/myapp/` published for the service instance.</span></span> <span data-ttu-id="b83fc-252">Se esta for um computador local, você verá `http://localhost:3000/myapp/`.</span><span class="sxs-lookup"><span data-stu-id="b83fc-252">Or if this is a local machine, you see `http://localhost:3000/myapp/`.</span></span>

```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000"  UriScheme="http" PathSuffix="myapp/" Type="Input" />
</Endpoints>
```
<span data-ttu-id="b83fc-253">Você pode usar esses endereços com o [proxy reverso](service-fabric-reverseproxy.md) para se comunicar entre os serviços.</span><span class="sxs-lookup"><span data-stu-id="b83fc-253">You can use these addresses with [reverse proxy](service-fabric-reverseproxy.md) to communicate between services.</span></span>

### <a name="edit-the-application-manifest-file"></a><span data-ttu-id="b83fc-254">Editar o arquivo de manifesto do aplicativo</span><span class="sxs-lookup"><span data-stu-id="b83fc-254">Edit the application manifest file</span></span>
<span data-ttu-id="b83fc-255">Depois de configurar o arquivo `Servicemanifest.xml`, você deve fazer algumas alterações ao arquivo `ApplicationManifest.xml` para garantir o uso do tipo e do nome de serviço corretos.</span><span class="sxs-lookup"><span data-stu-id="b83fc-255">Once you have configured the `Servicemanifest.xml` file, you need to make some changes to the `ApplicationManifest.xml` file to ensure that the correct service type and name are used.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="NodeAppType" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
   </ServiceManifestImport>
</ApplicationManifest>
```

#### <a name="servicemanifestimport"></a><span data-ttu-id="b83fc-256">ServiceManifestImport</span><span class="sxs-lookup"><span data-stu-id="b83fc-256">ServiceManifestImport</span></span>
<span data-ttu-id="b83fc-257">No elemento `ServiceManifestImport` , você pode especificar um ou mais serviços para incluí-los no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b83fc-257">In the `ServiceManifestImport` element, you can specify one or more services that you want to include in the app.</span></span> <span data-ttu-id="b83fc-258">Os serviços são referenciados com `ServiceManifestName`, que especifica o nome do diretório em que o arquivo `ServiceManifest.xml` está localizado.</span><span class="sxs-lookup"><span data-stu-id="b83fc-258">Services are referenced with `ServiceManifestName`, which specifies the name of the directory where the `ServiceManifest.xml` file is located.</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
</ServiceManifestImport>
```

## <a name="set-up-logging"></a><span data-ttu-id="b83fc-259">Configurar registro em log</span><span class="sxs-lookup"><span data-stu-id="b83fc-259">Set up logging</span></span>
<span data-ttu-id="b83fc-260">Para executáveis convidados, é útil poder ver os logs do console para descobrir se o aplicativo e os scripts de configuração mostram algum erro.</span><span class="sxs-lookup"><span data-stu-id="b83fc-260">For guest executables, it is useful to be able to see console logs to find out if the application and configuration scripts show any errors.</span></span>
<span data-ttu-id="b83fc-261">O redirecionamento do console pode ser configurado no arquivo `ServiceManifest.xml` usando o elemento `ConsoleRedirection`.</span><span class="sxs-lookup"><span data-stu-id="b83fc-261">Console redirection can be configured in the `ServiceManifest.xml` file using the `ConsoleRedirection` element.</span></span>

> [!WARNING]
> <span data-ttu-id="b83fc-262">Nunca use a política de redirecionamento de console em um aplicativo implantado na produção, pois isso pode afetar o failover do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b83fc-262">Never use the console redirection policy in an application that is deployed in production because this can affect the application failover.</span></span> <span data-ttu-id="b83fc-263">*Só* use isso para fins de depuração e de desenvolvimento locais.</span><span class="sxs-lookup"><span data-stu-id="b83fc-263">*Only* use this for local development and debugging purposes.</span></span>  
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

<span data-ttu-id="b83fc-264">`ConsoleRedirection` pode ser usado para redirecionar a saída do console (stdout e stderr) para um diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="b83fc-264">`ConsoleRedirection` can be used to redirect console output (both stdout and stderr) to a working directory.</span></span> <span data-ttu-id="b83fc-265">Isso possibilita verificar se não há erros durante a instalação ou execução do aplicativo no cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b83fc-265">This provides the ability to verify that there are no errors during the setup or execution of the application in the Service Fabric cluster.</span></span>

<span data-ttu-id="b83fc-266">O `FileRetentionCount` determina quantos arquivos são salvos no diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="b83fc-266">`FileRetentionCount` determines how many files are saved in the working directory.</span></span> <span data-ttu-id="b83fc-267">Um valor de 5, por exemplo, significa que os arquivos de log das cinco execução anteriores são armazenados no diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="b83fc-267">A value of 5, for example, means that the log files for the previous five executions are stored in the working directory.</span></span>

<span data-ttu-id="b83fc-268">`FileMaxSizeInKb` especifica o tamanho máximo dos arquivos de log.</span><span class="sxs-lookup"><span data-stu-id="b83fc-268">`FileMaxSizeInKb` specifies the maximum size of the log files.</span></span>

<span data-ttu-id="b83fc-269">Arquivos de log são salvos em um dos diretórios de trabalho do serviço.</span><span class="sxs-lookup"><span data-stu-id="b83fc-269">Log files are saved in one of the service's working directories.</span></span> <span data-ttu-id="b83fc-270">Para determinar o local em que os arquivos estão localizados, use o Service Fabric Explorer para determinar em qual nó o serviço está sendo executado e qual diretório de trabalho está sendo usado.</span><span class="sxs-lookup"><span data-stu-id="b83fc-270">To determine where the files are located, use Service Fabric Explorer to determine which node the service is running on, and which working directory is being used.</span></span> <span data-ttu-id="b83fc-271">Esse processo é abordado mais adiante neste artigo.</span><span class="sxs-lookup"><span data-stu-id="b83fc-271">This process is covered later in this article.</span></span>

## <a name="deployment"></a><span data-ttu-id="b83fc-272">Implantação</span><span class="sxs-lookup"><span data-stu-id="b83fc-272">Deployment</span></span>
<span data-ttu-id="b83fc-273">A última etapa será [implantar seu aplicativo](service-fabric-deploy-remove-applications.md).</span><span class="sxs-lookup"><span data-stu-id="b83fc-273">The last step is to [deploy your application](service-fabric-deploy-remove-applications.md).</span></span> <span data-ttu-id="b83fc-274">O script do PowerShell a seguir mostra como implantar seu aplicativo no cluster de desenvolvimento local e iniciar um novo serviço do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b83fc-274">The following PowerShell script shows how to deploy your application to the local development cluster, and start a new Service Fabric service.</span></span>

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
> <span data-ttu-id="b83fc-275">[Compacte o pacote](service-fabric-package-apps.md#compress-a-package) antes de copiar no armazenamento de imagens, se o pacote for grande ou tiver muitos arquivos.</span><span class="sxs-lookup"><span data-stu-id="b83fc-275">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store if the package is large or has many files.</span></span> <span data-ttu-id="b83fc-276">Leia mais [aqui](service-fabric-deploy-remove-applications.md#upload-the-application-package).</span><span class="sxs-lookup"><span data-stu-id="b83fc-276">Read more [here](service-fabric-deploy-remove-applications.md#upload-the-application-package).</span></span>
>

<span data-ttu-id="b83fc-277">Um serviço do Service Fabric pode ser implantado em várias "configurações".</span><span class="sxs-lookup"><span data-stu-id="b83fc-277">A Service Fabric service can be deployed in various "configurations."</span></span> <span data-ttu-id="b83fc-278">Por exemplo, pode ser implantado como uma ou várias instâncias, ou pode ser implantado de forma que haja uma instância do serviço em cada nó do cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b83fc-278">For example, it can be deployed as single or multiple instances, or it can be deployed in such a way that there is one instance of the service on each node of the Service Fabric cluster.</span></span>

<span data-ttu-id="b83fc-279">O parâmetro `InstanceCount` do cmdlet `New-ServiceFabricService` é usado para especificar quantas instâncias do serviço devem ser iniciadas no cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b83fc-279">The `InstanceCount` parameter of the `New-ServiceFabricService` cmdlet is used to specify how many instances of the service should be launched in the Service Fabric cluster.</span></span> <span data-ttu-id="b83fc-280">Você pode definir o valor de `InstanceCount` dependendo do tipo de aplicativo que está implantando.</span><span class="sxs-lookup"><span data-stu-id="b83fc-280">You can set the `InstanceCount` value, depending on the type of application that you are deploying.</span></span> <span data-ttu-id="b83fc-281">Os dois cenários mais comuns são:</span><span class="sxs-lookup"><span data-stu-id="b83fc-281">The two most common scenarios are:</span></span>

* <span data-ttu-id="b83fc-282">`InstanceCount = "1"`.</span><span class="sxs-lookup"><span data-stu-id="b83fc-282">`InstanceCount = "1"`.</span></span> <span data-ttu-id="b83fc-283">Neste caso, somente uma instância do serviço é implantada no cluster.</span><span class="sxs-lookup"><span data-stu-id="b83fc-283">In this case, only one instance of the service is deployed in the cluster.</span></span> <span data-ttu-id="b83fc-284">O agendador do Service Fabric determina em qual nó o serviço será implantado.</span><span class="sxs-lookup"><span data-stu-id="b83fc-284">Service Fabric's scheduler determines which node the service is going to be deployed on.</span></span>
* <span data-ttu-id="b83fc-285">`InstanceCount ="-1"`.</span><span class="sxs-lookup"><span data-stu-id="b83fc-285">`InstanceCount ="-1"`.</span></span> <span data-ttu-id="b83fc-286">Neste caso, uma instância do serviço é implantada em cada nó do cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b83fc-286">In this case, one instance of the service is deployed on every node in the Service Fabric cluster.</span></span> <span data-ttu-id="b83fc-287">O resultado é ter uma (e apenas uma) instância do serviço para cada nó no cluster.</span><span class="sxs-lookup"><span data-stu-id="b83fc-287">The result is having one (and only one) instance of the service for each node in the cluster.</span></span>

<span data-ttu-id="b83fc-288">Essa é uma configuração útil para aplicativos de front-end (por exemplo, um ponto de extremidade REST), pois os aplicativos cliente precisam se “conectar” a qualquer um dos nós do cluster para usar o ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="b83fc-288">This is a useful configuration for front-end applications (for example, a REST endpoint), because client applications need to "connect" to any of the nodes in the cluster to use the endpoint.</span></span> <span data-ttu-id="b83fc-289">Essa configuração também pode ser usada quando, por exemplo, todos os nós do cluster do Service Fabric estiverem conectados a um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="b83fc-289">This configuration can also be used when, for example, all nodes of the Service Fabric cluster are connected to a load balancer.</span></span> <span data-ttu-id="b83fc-290">O tráfego do cliente então pode ser distribuído entre o serviço está em execução em todos os nós no cluster.</span><span class="sxs-lookup"><span data-stu-id="b83fc-290">Client traffic can then be distributed across the service that is running on all nodes in the cluster.</span></span>

## <a name="check-your-running-application"></a><span data-ttu-id="b83fc-291">Verificar seu aplicativo em execução</span><span class="sxs-lookup"><span data-stu-id="b83fc-291">Check your running application</span></span>
<span data-ttu-id="b83fc-292">No Gerenciador do Service Fabric, identifique o nó em que o serviço está em execução.</span><span class="sxs-lookup"><span data-stu-id="b83fc-292">In Service Fabric Explorer, identify the node where the service is running.</span></span> <span data-ttu-id="b83fc-293">Neste exemplo, ele está executando no Node1:</span><span class="sxs-lookup"><span data-stu-id="b83fc-293">In this example, it runs on Node1:</span></span>

![Nó em que o serviço está em execução](./media/service-fabric-deploy-existing-app/nodeappinsfx.png)

<span data-ttu-id="b83fc-295">Se navegar até o nó e procurar o aplicativo, você verá as informações essenciais do nó, incluindo sua localização no disco.</span><span class="sxs-lookup"><span data-stu-id="b83fc-295">If you navigate to the node and browse to the application, you see the essential node information, including its location on disk.</span></span>

![Local no disco](./media/service-fabric-deploy-existing-app/locationondisk2.png)

<span data-ttu-id="b83fc-297">Se navegar até o diretório usando o Gerenciador de Servidores, você poderá localizar o diretório de trabalho e a pasta de log do serviço, como mostra a seguinte captura de tela:</span><span class="sxs-lookup"><span data-stu-id="b83fc-297">If you browse to the directory by using Server Explorer, you can find the working directory and the service's log folder, as shown in the following screenshot:</span></span> 

![Local do log](./media/service-fabric-deploy-existing-app/loglocation.png)

## <a name="next-steps"></a><span data-ttu-id="b83fc-299">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b83fc-299">Next steps</span></span>
<span data-ttu-id="b83fc-300">Neste artigo, você aprendeu como empacotar um executável convidado e implantá-lo à Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b83fc-300">In this article, you have learned how to package a guest executable and deploy it to Service Fabric.</span></span> <span data-ttu-id="b83fc-301">Consulte os seguintes artigos para tarefas e informações relacionadas.</span><span class="sxs-lookup"><span data-stu-id="b83fc-301">See the following articles for related information and tasks.</span></span>

* <span data-ttu-id="b83fc-302">[Amostra de empacotamento e implantação de um executável convidado](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), incluindo um link para o pré-lançamento da ferramenta de empacotamento</span><span class="sxs-lookup"><span data-stu-id="b83fc-302">[Sample for packaging and deploying a guest executable](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), including a link to the prerelease of the packaging tool</span></span>
* [<span data-ttu-id="b83fc-303">Exemplo de dois executáveis convidados (C# e nodejs) se comunicando por meio do Serviço de nomenclatura usando REST</span><span class="sxs-lookup"><span data-stu-id="b83fc-303">Sample of two guest executables (C# and nodejs) communicating via the Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
* [<span data-ttu-id="b83fc-304">Implantar vários executáveis de convidado</span><span class="sxs-lookup"><span data-stu-id="b83fc-304">Deploy multiple guest executables</span></span>](service-fabric-deploy-multiple-apps.md)
* [<span data-ttu-id="b83fc-305">Criar seu primeiro aplicativo do Service Fabric usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b83fc-305">Create your first Service Fabric application using Visual Studio</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
