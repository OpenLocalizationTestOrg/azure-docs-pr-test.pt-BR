---
title: "aaaCreate um cluster do Azure Service Fabric autônomo | Microsoft Docs"
description: "Crie um cluster do Azure Service Fabric em qualquer computador (físico ou virtual) executando o Windows Server, seja ele local ou em qualquer nuvem."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 31349169-de19-4be6-8742-ca20ac41eb9e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/10/2017
ms.author: chackdan;maburlik;dekapur
ms.openlocfilehash: 444970816290a0448d88a8b2082c75eb7a64cb44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-standalone-cluster-running-on-windows-server"></a><span data-ttu-id="ee150-103">Criar um cluster autônomo em execução no Windows Server</span><span class="sxs-lookup"><span data-stu-id="ee150-103">Create a standalone cluster running on Windows Server</span></span>
<span data-ttu-id="ee150-104">Você pode usar clusters de malha do serviço do Azure Service Fabric toocreate em quaisquer máquinas virtuais ou computadores que executam o Windows Server.</span><span class="sxs-lookup"><span data-stu-id="ee150-104">You can use Azure Service Fabric toocreate Service Fabric clusters on any virtual machines or computers running Windows Server.</span></span> <span data-ttu-id="ee150-105">Isso significa que você pode implantar e executar os aplicativos do Service Fabric em qualquer ambiente que tenha um conjunto de computadores com o Windows Server interconectados, seja localmente ou em qualquer provedor de nuvem.</span><span class="sxs-lookup"><span data-stu-id="ee150-105">This means you can deploy and run Service Fabric applications in any environment that contains a set of interconnected Windows Server computers, be it on premises or with any cloud provider.</span></span> <span data-ttu-id="ee150-106">Serviço de malha fornece um toocreate de pacote de instalação que do Service Fabric clusters chamado de pacote do hello autônomo do Windows Server.</span><span class="sxs-lookup"><span data-stu-id="ee150-106">Service Fabric provides a setup package toocreate Service Fabric clusters called hello standalone Windows Server package.</span></span>

<span data-ttu-id="ee150-107">Este artigo o orienta pelas etapas de saudação para a criação de um cluster do Service Fabric autônomo.</span><span class="sxs-lookup"><span data-stu-id="ee150-107">This article walks you through hello steps for creating a Service Fabric standalone cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="ee150-108">Este pacote autônomo do Windows Server está disponível para venda e pode ser usado para implantações de produção.</span><span class="sxs-lookup"><span data-stu-id="ee150-108">This standalone Windows Server package is commercially available and may be used for production deployments.</span></span> <span data-ttu-id="ee150-109">Este pacote pode conter novos recursos do Service Fabric que estão em “Visualização”.</span><span class="sxs-lookup"><span data-stu-id="ee150-109">This package may contain new Service Fabric features that are in "Preview".</span></span> <span data-ttu-id="ee150-110">Role para baixo demais"[incluídos neste pacote de recursos de visualização](#previewfeatures_anchor)."</span><span class="sxs-lookup"><span data-stu-id="ee150-110">Scroll down too"[Preview features included in this package](#previewfeatures_anchor)."</span></span> <span data-ttu-id="ee150-111">seção para obter lista de saudação de recursos de visualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="ee150-111">section for hello list of hello preview features.</span></span> <span data-ttu-id="ee150-112">Você pode [baixar uma cópia do EULA da saudação](http://go.microsoft.com/fwlink/?LinkID=733084) agora.</span><span class="sxs-lookup"><span data-stu-id="ee150-112">You can [download a copy of hello EULA](http://go.microsoft.com/fwlink/?LinkID=733084) now.</span></span>
> 
> 

<a id="getsupport"></a>

## <a name="get-support-for-hello-service-fabric-for-windows-server-package"></a><span data-ttu-id="ee150-113">Obter suporte para o pacote de malha do serviço para o Windows Server Olá</span><span class="sxs-lookup"><span data-stu-id="ee150-113">Get support for hello Service Fabric for Windows Server package</span></span>
* <span data-ttu-id="ee150-114">Perguntar comunidade Olá pacote do hello Service Fabric autônomo para o Windows Server em Olá [Fórum do Azure Service Fabric](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).</span><span class="sxs-lookup"><span data-stu-id="ee150-114">Ask hello community about hello Service Fabric standalone package for Windows Server in hello [Azure Service Fabric forum](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).</span></span>
* <span data-ttu-id="ee150-115">Abra um tíquete de [Suporte Profissional para o Service Fabric](http://support.microsoft.com/oas/default.aspx?prid=16146).</span><span class="sxs-lookup"><span data-stu-id="ee150-115">Open a ticket for [Professional Support for Service Fabric](http://support.microsoft.com/oas/default.aspx?prid=16146).</span></span>  <span data-ttu-id="ee150-116">Saiba mais sobre o Suporte Profissional da Microsoft [aqui](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).</span><span class="sxs-lookup"><span data-stu-id="ee150-116">Learn more about Professional Support from Microsoft [here](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).</span></span>
* <span data-ttu-id="ee150-117">Você também pode obter suporte para este pacote como parte do [Suporte Premier da Microsoft](https://support.microsoft.com/en-us/premier).</span><span class="sxs-lookup"><span data-stu-id="ee150-117">You can also get support for this package as a part of [Microsoft Premier Support](https://support.microsoft.com/en-us/premier).</span></span>
* <span data-ttu-id="ee150-118">Para obter mais detalhes, consulte as [Opções de suporte do Azure Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).</span><span class="sxs-lookup"><span data-stu-id="ee150-118">For more details, please see [Azure Service Fabric support options](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).</span></span>
* <span data-ttu-id="ee150-119">logs de toocollect para fins de suporte, executados Olá [coletor de Log do serviço do Fabric autônomo](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="ee150-119">toocollect logs for support purposes, run hello [Service Fabric Standalone Log collector](service-fabric-cluster-standalone-package-contents.md).</span></span>

<a id="downloadpackage"></a>

## <a name="download-hello-service-fabric-for-windows-server-package"></a><span data-ttu-id="ee150-120">Baixar pacote de malha do serviço para o Windows Server Olá</span><span class="sxs-lookup"><span data-stu-id="ee150-120">Download hello Service Fabric for Windows Server package</span></span>
<span data-ttu-id="ee150-121">cluster de Olá toocreate, use o pacote de malha do serviço para o Windows Server hello (Windows Server 2012 R2 e mais recente) encontradas aqui:</span><span class="sxs-lookup"><span data-stu-id="ee150-121">toocreate hello cluster, use hello Service Fabric for Windows Server package (Windows Server 2012 R2 and newer) found here:</span></span> <br><span data-ttu-id="ee150-122">
[Link de Download – pacote autônomo do Service Fabric – Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)</span><span class="sxs-lookup"><span data-stu-id="ee150-122">
[Download Link - Service Fabric Standalone Package - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)</span></span>

<span data-ttu-id="ee150-123">Encontrar detalhes sobre o conteúdo do pacote de saudação [aqui](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="ee150-123">Find details on contents of hello package [here](service-fabric-cluster-standalone-package-contents.md).</span></span>

<span data-ttu-id="ee150-124">pacote de tempo de execução do Service Fabric Olá é baixado automaticamente no momento da criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="ee150-124">hello Service Fabric runtime package is automatically downloaded at time of cluster creation.</span></span> <span data-ttu-id="ee150-125">Se a implantação de um computador não conectado toohello internet, baixe o pacote de tempo de execução de saudação fora da banda em aqui:</span><span class="sxs-lookup"><span data-stu-id="ee150-125">If deploying from a machine not connected toohello internet, please download hello runtime package out of band from here:</span></span> <br><span data-ttu-id="ee150-126">
[Link de Download – Tempo de Execução do Service Fabric – Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)</span><span class="sxs-lookup"><span data-stu-id="ee150-126">
[Download Link - Service Fabric Runtime - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)</span></span>

<span data-ttu-id="ee150-127">Encontre amostras de configuração de cluster autônomo em:</span><span class="sxs-lookup"><span data-stu-id="ee150-127">Find Standalone Cluster Configuration samples at:</span></span> <br><span data-ttu-id="ee150-128">
[Amostras de configuração de cluster autônomo](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span><span class="sxs-lookup"><span data-stu-id="ee150-128">
[Standalone Cluster Configuration Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span></span>

<a id="createcluster"></a>

## <a name="create-hello-cluster"></a><span data-ttu-id="ee150-129">Criar cluster Olá</span><span class="sxs-lookup"><span data-stu-id="ee150-129">Create hello cluster</span></span>
<span data-ttu-id="ee150-130">Malha do serviço pode ser implantado tooa cluster de desenvolvimento de um computador usando Olá *ClusterConfig.Unsecure.DevCluster.json* arquivo incluído no [exemplos](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="ee150-130">Service Fabric can be deployed tooa one-machine development cluster by using hello *ClusterConfig.Unsecure.DevCluster.json* file included in [Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).</span></span>

<span data-ttu-id="ee150-131">Desempacotar máquina do hello autônoma pacote tooyour, cópia Olá exemplo config arquivo toohello máquina local e execução Olá *CreateServiceFabricCluster.ps1* script por meio de uma sessão do PowerShell de administrador, do hello autônomo pasta do pacote:</span><span class="sxs-lookup"><span data-stu-id="ee150-131">Unpack hello standalone package tooyour machine, copy hello sample config file toohello local machine, then run hello *CreateServiceFabricCluster.ps1* script through an administrator PowerShell session, from hello standalone package folder:</span></span>
### <a name="step-1a-create-an-unsecured-local-development-cluster"></a><span data-ttu-id="ee150-132">Etapa 1A: criar um cluster de desenvolvimento local desprotegido</span><span class="sxs-lookup"><span data-stu-id="ee150-132">Step 1A: Create an unsecured local development cluster</span></span>
```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

<span data-ttu-id="ee150-133">Consulte Olá a seção de configuração do ambiente no [planejar e preparar a implantação de cluster](service-fabric-cluster-standalone-deployment-preparation.md) para obter detalhes de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="ee150-133">See hello Environment Setup section at [Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md) for troubleshooting details.</span></span>

<span data-ttu-id="ee150-134">Se você concluiu os cenários de desenvolvimento em execução, você pode remover o cluster do Service Fabric Olá da máquina Olá referindo toosteps na seção "[remover um cluster](#removecluster_anchor)".</span><span class="sxs-lookup"><span data-stu-id="ee150-134">If you're finished running development scenarios, you can remove hello Service Fabric cluster from hello machine by referring toosteps in section "[Remove a cluster](#removecluster_anchor)".</span></span> 

### <a name="step-1b-create-a-multi-machine-cluster"></a><span data-ttu-id="ee150-135">Etapa 1B: criar um cluster com vários computadores</span><span class="sxs-lookup"><span data-stu-id="ee150-135">Step 1B: Create a multi-machine cluster</span></span>
<span data-ttu-id="ee150-136">Depois de você ter feito Olá planejamento e etapas de preparação detalhadas em Olá abaixo do link, você está pronto toocreate seu cluster de produção usando o arquivo de configuração do cluster.</span><span class="sxs-lookup"><span data-stu-id="ee150-136">After you have gone through hello planning and preparation steps detailed at hello below link, you are ready toocreate your production cluster using your cluster configuration file.</span></span> <br><span data-ttu-id="ee150-137">
[Planejar e preparar a implantação do cluster](service-fabric-cluster-standalone-deployment-preparation.md)</span><span class="sxs-lookup"><span data-stu-id="ee150-137">
[Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md)</span></span>

1. <span data-ttu-id="ee150-138">Validar o arquivo de configuração Olá escrevê executando Olá *TestConfiguration.ps1* script hello autônomo da pasta do pacote:</span><span class="sxs-lookup"><span data-stu-id="ee150-138">Validate hello configuration file you have written by running hello *TestConfiguration.ps1* script from hello standalone package folder:</span></span>  

    ```powershell
    .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.json
    ```

    <span data-ttu-id="ee150-139">Você deverá ver uma saída como a abaixo.</span><span class="sxs-lookup"><span data-stu-id="ee150-139">You should see output like below.</span></span> <span data-ttu-id="ee150-140">Se o campo de último hello "Aprovado" é retornado como "True", verificações de integridade tiveram passado e cluster Olá parece com base na configuração de entrada hello toobe implantável.</span><span class="sxs-lookup"><span data-stu-id="ee150-140">If hello bottom field "Passed" is returned as "True", sanity checks have passed and hello cluster looks toobe deployable based on hello input configuration.</span></span>

    ```
    Trace folder already exists. Traces will be written tooexisting trace folder: C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer\DeploymentTraces
    Running Best Practices Analyzer...
    Best Practices Analyzer completed successfully.
    
    LocalAdminPrivilege        : True
    IsJsonValid                : True
    IsCabValid                 : True
    RequiredPortsOpen          : True
    RemoteRegistryAvailable    : True
    FirewallAvailable          : True
    RpcCheckPassed             : True
    NoConflictingInstallations : True
    FabricInstallable          : True
    Passed                     : True
    ```

2. <span data-ttu-id="ee150-141">Criar cluster Olá: executar Olá *CreateServiceFabricCluster.ps1* cluster do script toodeploy saudação do Service Fabric em cada computador na configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="ee150-141">Create hello cluster:  Run hello *CreateServiceFabricCluster.ps1* script toodeploy hello Service Fabric cluster across each machine in hello configuration.</span></span> 
    ```powershell
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -AcceptEULA
    ```

> [!NOTE]
> <span data-ttu-id="ee150-142">Os rastreamentos de implantação são gravados toohello VM/máquina em que você executou o script do PowerShell CreateServiceFabricCluster.ps1 hello.</span><span class="sxs-lookup"><span data-stu-id="ee150-142">Deployment traces are written toohello VM/machine on which you ran hello CreateServiceFabricCluster.ps1 PowerShell script.</span></span> <span data-ttu-id="ee150-143">Eles podem ser encontrados na subpasta Olá DeploymentTraces, com base no diretório de saudação do qual Olá script foi executado.</span><span class="sxs-lookup"><span data-stu-id="ee150-143">These can be found in hello subfolder DeploymentTraces, based in hello directory from which hello script was run.</span></span> <span data-ttu-id="ee150-144">toosee se a malha do serviço foi implantado corretamente tooa máquina, localizar arquivos de Olá instalado no diretório de FabricDataRoot hello, conforme detalhado no arquivo de configuração de cluster Olá FabricSettings seção (por padrão c:\ProgramData\SF).</span><span class="sxs-lookup"><span data-stu-id="ee150-144">toosee if Service Fabric was deployed correctly tooa machine, find hello installed files in hello FabricDataRoot directory, as detailed in hello cluster configuration file FabricSettings section (by default c:\ProgramData\SF).</span></span> <span data-ttu-id="ee150-145">Além disso, processos FabricHost.exe e Fabric.exe podem ser vistos em execução no Gerenciador de Tarefas.</span><span class="sxs-lookup"><span data-stu-id="ee150-145">As well, FabricHost.exe and Fabric.exe processes can be seen running in Task Manager.</span></span>
> 
> 

### <a name="step-1c-create-an-offline-internet-disconnected-cluster"></a><span data-ttu-id="ee150-146">Etapa 1C: Criar um cluster offline (desconectado da Internet)</span><span class="sxs-lookup"><span data-stu-id="ee150-146">Step 1C: Create an offline (internet-disconnected) cluster</span></span>
<span data-ttu-id="ee150-147">pacote de tempo de execução do Service Fabric Olá é baixado automaticamente na criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="ee150-147">hello Service Fabric runtime package is automatically downloaded at cluster creation.</span></span> <span data-ttu-id="ee150-148">Ao implantar um cluster toomachines não conectado toohello internet, você precisará Olá toodownload Service Fabric runtime separadamente do pacote e fornecer Olá caminho tooit na criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="ee150-148">When deploying a cluster toomachines not connected toohello internet, you will need toodownload hello Service Fabric runtime package separately, and provide hello path tooit at cluster creation.</span></span>
<span data-ttu-id="ee150-149">Olá pacote de tempo de execução pode ser baixado separadamente, de outro computador conectado toohello internet, em [o Link de Download - tempo de execução do serviço de malha - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).</span><span class="sxs-lookup"><span data-stu-id="ee150-149">hello runtime package can be downloaded separately, from another machine connected toohello internet, at [Download Link - Service Fabric Runtime - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).</span></span> <span data-ttu-id="ee150-150">Copiar Olá toowhere de pacote em tempo de execução você está implantando o cluster offline de saudação do e cria cluster Olá executando `CreateServiceFabricCluster.ps1` com hello `-FabricRuntimePackagePath` parâmetro incluído, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="ee150-150">Copy hello runtime package toowhere you are deploying hello offline cluster from, and create hello cluster by running `CreateServiceFabricCluster.ps1` with hello `-FabricRuntimePackagePath` parameter included, as shown below:</span></span> 

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -FabricRuntimePackagePath .\MicrosoftAzureServiceFabric.cab
```
<span data-ttu-id="ee150-151">onde `.\ClusterConfig.json` e `.\MicrosoftAzureServiceFabric.cab` são configuração de cluster Olá caminhos toohello e CAB de tempo de execução-Olá, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="ee150-151">where `.\ClusterConfig.json` and `.\MicrosoftAzureServiceFabric.cab` are hello paths toohello cluster configuration and hello runtime .cab file respectively.</span></span>


### <a name="step-2-connect-toohello-cluster"></a><span data-ttu-id="ee150-152">Etapa 2: Conectar toohello cluster</span><span class="sxs-lookup"><span data-stu-id="ee150-152">Step 2: Connect toohello cluster</span></span>
<span data-ttu-id="ee150-153">tooconnect tooa o cluster seguro, consulte [do Service fabric se conectar a cluster toosecure](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="ee150-153">tooconnect tooa secure cluster, see [Service fabric connect toosecure cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

<span data-ttu-id="ee150-154">tooconnect tooan não segura cluster, execute Olá comando PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="ee150-154">tooconnect tooan unsecure cluster, run hello following PowerShell command:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <*IPAddressofaMachine*>:<Client connection end point port>
```
<span data-ttu-id="ee150-155">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="ee150-155">Example:</span></span>
```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint 192.13.123.2345:19000
```
### <a name="step-3-bring-up-service-fabric-explorer"></a><span data-ttu-id="ee150-156">Etapa 3: abrir o Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="ee150-156">Step 3: Bring up Service Fabric Explorer</span></span>
<span data-ttu-id="ee150-157">Agora você pode se conectar toohello cluster Service Fabric Explorer diretamente de uma das máquinas Olá http://localhost:19080/Explorer/index.html ou remotamente com http://<;*IPAddressofaMachine*>: 19080 / Explorer/index.HTML.</span><span class="sxs-lookup"><span data-stu-id="ee150-157">Now you can connect toohello cluster with Service Fabric Explorer either directly from one of hello machines with http://localhost:19080/Explorer/index.html or remotely with http://<*IPAddressofaMachine*>:19080/Explorer/index.html.</span></span>

## <a name="add-and-remove-nodes"></a><span data-ttu-id="ee150-158">Adicionar e remover nós</span><span class="sxs-lookup"><span data-stu-id="ee150-158">Add and remove nodes</span></span>
<span data-ttu-id="ee150-159">Você pode adicionar ou remover o cluster do Service Fabric de nós tooyour autônomo conforme suas necessidades comerciais mudarem.</span><span class="sxs-lookup"><span data-stu-id="ee150-159">You can add or remove nodes tooyour standalone Service Fabric cluster as your business needs change.</span></span> <span data-ttu-id="ee150-160">Consulte [adicionar ou remover nós tooa Service Fabric autônomo cluster](service-fabric-cluster-windows-server-add-remove-nodes.md) para obter etapas detalhadas.</span><span class="sxs-lookup"><span data-stu-id="ee150-160">See [Add or Remove nodes tooa Service Fabric standalone cluster](service-fabric-cluster-windows-server-add-remove-nodes.md) for detailed steps.</span></span>

<a id="removecluster" name="removecluster_anchor"></a>
## <a name="remove-a-cluster"></a><span data-ttu-id="ee150-161">Remover um cluster</span><span class="sxs-lookup"><span data-stu-id="ee150-161">Remove a cluster</span></span>
<span data-ttu-id="ee150-162">tooremove um cluster, execute Olá *RemoveServiceFabricCluster.ps1* script do PowerShell na pasta de pacote de saudação e passe o arquivo de configuração do hello caminho toohello JSON.</span><span class="sxs-lookup"><span data-stu-id="ee150-162">tooremove a cluster, run hello *RemoveServiceFabricCluster.ps1* PowerShell script from hello package folder and pass in hello path toohello JSON configuration file.</span></span> <span data-ttu-id="ee150-163">Opcionalmente, você pode especificar um local para o log de saudação de exclusão de saudação.</span><span class="sxs-lookup"><span data-stu-id="ee150-163">You can optionally specify a location for hello log of hello deletion.</span></span>

<span data-ttu-id="ee150-164">Esse script pode ser executado em qualquer computador que tenha acesso tooall Olá máquinas de administrador são listadas como nós em um arquivo de configuração de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="ee150-164">This script can be run on any machine that has administrator access tooall hello machines that are listed as nodes in hello cluster configuration file.</span></span> <span data-ttu-id="ee150-165">máquina de saudação que esse script é executado no não tem toobe parte do cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="ee150-165">hello machine that this script is run on does not have toobe part of hello cluster.</span></span>

```
# Removes Service Fabric from each machine in hello configuration
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -Force
```

```
# Removes Service Fabric from hello current machine
.\CleanFabric.ps1
```

<a id="telemetry"></a>

## <a name="telemetry-data-collected-and-how-tooopt-out-of-it"></a><span data-ttu-id="ee150-166">Dados de telemetria coletados e como tooopt fora dele</span><span class="sxs-lookup"><span data-stu-id="ee150-166">Telemetry data collected and how tooopt out of it</span></span>
<span data-ttu-id="ee150-167">Por padrão, produto Olá coleta a telemetria no hello Service Fabric uso tooimprove Olá de produto.</span><span class="sxs-lookup"><span data-stu-id="ee150-167">As a default, hello product collects telemetry on hello Service Fabric usage tooimprove hello product.</span></span> <span data-ttu-id="ee150-168">Olá analisador de práticas recomendadas que é executado como parte da instalação Olá verifica a conectividade muito[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1).</span><span class="sxs-lookup"><span data-stu-id="ee150-168">hello Best Practice Analyzer that runs as a part of hello setup checks for connectivity too[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1).</span></span> <span data-ttu-id="ee150-169">Se não estiver acessível, a instalação de saudação falhará a menos que você recusar a telemetria.</span><span class="sxs-lookup"><span data-stu-id="ee150-169">If it is not reachable, hello setup fails unless you opt out of telemetry.</span></span>

1. <span data-ttu-id="ee150-170">pipeline de telemetria Hello tenta Olá tooupload seguintes dados muito[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) uma vez por dia.</span><span class="sxs-lookup"><span data-stu-id="ee150-170">hello telemetry pipeline tries tooupload hello following data too[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) once every day.</span></span> <span data-ttu-id="ee150-171">Ele é um carregamento de melhor esforço e não tem nenhum impacto sobre a funcionalidade do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="ee150-171">It is a best-effort upload and has no impact on hello cluster functionality.</span></span> <span data-ttu-id="ee150-172">Telemetria de saudação é enviada apenas do nó Olá executa Olá principal do Gerenciador de failover.</span><span class="sxs-lookup"><span data-stu-id="ee150-172">hello telemetry is only sent from hello node that runs hello failover manager primary.</span></span> <span data-ttu-id="ee150-173">Nenhum outro nó envia telemetria.</span><span class="sxs-lookup"><span data-stu-id="ee150-173">No other nodes send out telemetry.</span></span>
2. <span data-ttu-id="ee150-174">Telemetria Olá consiste em seguir hello:</span><span class="sxs-lookup"><span data-stu-id="ee150-174">hello telemetry consists of hello following:</span></span>

* <span data-ttu-id="ee150-175">Número de serviços</span><span class="sxs-lookup"><span data-stu-id="ee150-175">Number of services</span></span>
* <span data-ttu-id="ee150-176">Número de ServiceTypes</span><span class="sxs-lookup"><span data-stu-id="ee150-176">Number of ServiceTypes</span></span>
* <span data-ttu-id="ee150-177">Número de Aplicativos</span><span class="sxs-lookup"><span data-stu-id="ee150-177">Number of Applications</span></span>
* <span data-ttu-id="ee150-178">Número de ApplicationUpgrades</span><span class="sxs-lookup"><span data-stu-id="ee150-178">Number of ApplicationUpgrades</span></span>
* <span data-ttu-id="ee150-179">Número de FailoverUnits</span><span class="sxs-lookup"><span data-stu-id="ee150-179">Number of FailoverUnits</span></span>
* <span data-ttu-id="ee150-180">Número de InBuildFailoverUnits</span><span class="sxs-lookup"><span data-stu-id="ee150-180">Number of InBuildFailoverUnits</span></span>
* <span data-ttu-id="ee150-181">Número de UnhealthyFailoverUnits</span><span class="sxs-lookup"><span data-stu-id="ee150-181">Number of UnhealthyFailoverUnits</span></span>
* <span data-ttu-id="ee150-182">Número de Réplicas</span><span class="sxs-lookup"><span data-stu-id="ee150-182">Number of Replicas</span></span>
* <span data-ttu-id="ee150-183">Número de InBuildReplicas</span><span class="sxs-lookup"><span data-stu-id="ee150-183">Number of InBuildReplicas</span></span>
* <span data-ttu-id="ee150-184">Número de StandByReplicas</span><span class="sxs-lookup"><span data-stu-id="ee150-184">Number of StandByReplicas</span></span>
* <span data-ttu-id="ee150-185">Número de OfflineReplicas</span><span class="sxs-lookup"><span data-stu-id="ee150-185">Number of OfflineReplicas</span></span>
* <span data-ttu-id="ee150-186">CommonQueueLength</span><span class="sxs-lookup"><span data-stu-id="ee150-186">CommonQueueLength</span></span>
* <span data-ttu-id="ee150-187">QueryQueueLength</span><span class="sxs-lookup"><span data-stu-id="ee150-187">QueryQueueLength</span></span>
* <span data-ttu-id="ee150-188">FailoverUnitQueueLength</span><span class="sxs-lookup"><span data-stu-id="ee150-188">FailoverUnitQueueLength</span></span>
* <span data-ttu-id="ee150-189">CommitQueueLength</span><span class="sxs-lookup"><span data-stu-id="ee150-189">CommitQueueLength</span></span>
* <span data-ttu-id="ee150-190">Número de Nós</span><span class="sxs-lookup"><span data-stu-id="ee150-190">Number of Nodes</span></span>
* <span data-ttu-id="ee150-191">IsContextComplete: True/False</span><span class="sxs-lookup"><span data-stu-id="ee150-191">IsContextComplete: True/False</span></span>
* <span data-ttu-id="ee150-192">ClusterId: esse é um GUID gerado aleatoriamente para cada cluster</span><span class="sxs-lookup"><span data-stu-id="ee150-192">ClusterId: This is a GUID randomly generated for each cluster</span></span>
* <span data-ttu-id="ee150-193">ServiceFabricVersion</span><span class="sxs-lookup"><span data-stu-id="ee150-193">ServiceFabricVersion</span></span>
* <span data-ttu-id="ee150-194">Endereço IP da máquina virtual de saudação ou máquina na qual Olá telemetria é carregada</span><span class="sxs-lookup"><span data-stu-id="ee150-194">IP address of hello virtual machine or machine from which hello telemetry is uploaded</span></span>

<span data-ttu-id="ee150-195">Telemetria toodisable, adicionar Olá seguir muito*propriedades* na sua configuração de cluster: *enableTelemetry: false*.</span><span class="sxs-lookup"><span data-stu-id="ee150-195">toodisable telemetry, add hello following too*properties* in your cluster config: *enableTelemetry: false*.</span></span>

<a id="previewfeatures" name="previewfeatures_anchor"></a>

## <a name="preview-features-included-in-this-package"></a><span data-ttu-id="ee150-196">Recursos de preview incluídos neste pacote</span><span class="sxs-lookup"><span data-stu-id="ee150-196">Preview features included in this package</span></span>
<span data-ttu-id="ee150-197">Nenhuma.</span><span class="sxs-lookup"><span data-stu-id="ee150-197">None.</span></span>


> [!NOTE]
> <span data-ttu-id="ee150-198">Começando com hello novo [versão GA do cluster do hello autônomo para o Windows Server (versão 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), você pode atualizar versões toofuture cluster, manual ou automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ee150-198">Starting with hello new [GA version of hello standalone cluster for Windows Server (version 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), you can upgrade your cluster toofuture releases, manually or automatically.</span></span> <span data-ttu-id="ee150-199">Consulte também[atualizar uma versão de cluster do Service Fabric autônomo](service-fabric-cluster-upgrade-windows-server.md) documento para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="ee150-199">Refer too[Upgrade a standalone Service Fabric cluster version](service-fabric-cluster-upgrade-windows-server.md) document for details.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ee150-200">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ee150-200">Next steps</span></span>
* [<span data-ttu-id="ee150-201">Implantar e remover aplicativos usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="ee150-201">Deploy and remove applications using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="ee150-202">Definições de configuração para o cluster autônomo no Windows</span><span class="sxs-lookup"><span data-stu-id="ee150-202">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="ee150-203">Adicionar ou remover nós tooa autônomo do Service Fabric cluster</span><span class="sxs-lookup"><span data-stu-id="ee150-203">Add or remove nodes tooa standalone Service Fabric cluster</span></span>](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [<span data-ttu-id="ee150-204">Atualizar uma versão autônoma de cluster do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ee150-204">Upgrade a standalone Service Fabric cluster version</span></span>](service-fabric-cluster-upgrade-windows-server.md)
* [<span data-ttu-id="ee150-205">Criar um cluster do Service Fabric autônomo com VMs do Azure executando o Windows</span><span class="sxs-lookup"><span data-stu-id="ee150-205">Create a standalone Service Fabric cluster with Azure VMs running Windows</span></span>](service-fabric-cluster-creation-with-windows-azure-vms.md)
* [<span data-ttu-id="ee150-206">Proteger um cluster autônomo no Windows usando a segurança</span><span class="sxs-lookup"><span data-stu-id="ee150-206">Secure a standalone cluster on Windows using Windows security</span></span>](service-fabric-windows-cluster-windows-security.md)
* [<span data-ttu-id="ee150-207">Proteger um cluster autônomo no Windows usando os certificados X509</span><span class="sxs-lookup"><span data-stu-id="ee150-207">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)

<!--Image references-->
[Trusted Zone]: ./media/service-fabric-cluster-creation-for-windows-server/TrustedZone.png
