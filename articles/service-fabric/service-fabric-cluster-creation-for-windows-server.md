---
title: "Criar um cluster autônomo do Azure Service Fabric | Microsoft Docs"
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
ms.openlocfilehash: 6aa2905a97ec6b8c125f2ab9572a8e40bf525b27
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-standalone-cluster-running-on-windows-server"></a><span data-ttu-id="f5b83-103">Criar um cluster autônomo em execução no Windows Server</span><span class="sxs-lookup"><span data-stu-id="f5b83-103">Create a standalone cluster running on Windows Server</span></span>
<span data-ttu-id="f5b83-104">Você pode usar o Azure Service Fabric para criar clusters do Service Fabric em qualquer máquina virtual ou computador que estiver executando o Windows Server.</span><span class="sxs-lookup"><span data-stu-id="f5b83-104">You can use Azure Service Fabric to create Service Fabric clusters on any virtual machines or computers running Windows Server.</span></span> <span data-ttu-id="f5b83-105">Isso significa que você pode implantar e executar os aplicativos do Service Fabric em qualquer ambiente que tenha um conjunto de computadores com o Windows Server interconectados, seja localmente ou em qualquer provedor de nuvem.</span><span class="sxs-lookup"><span data-stu-id="f5b83-105">This means you can deploy and run Service Fabric applications in any environment that contains a set of interconnected Windows Server computers, be it on premises or with any cloud provider.</span></span> <span data-ttu-id="f5b83-106">O Service Fabric fornece um pacote de instalação para criar os clusters do Service Fabric denominado pacote do Windows Server autônomo.</span><span class="sxs-lookup"><span data-stu-id="f5b83-106">Service Fabric provides a setup package to create Service Fabric clusters called the standalone Windows Server package.</span></span>

<span data-ttu-id="f5b83-107">Este artigo guia você pelas etapas para criação de um cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f5b83-107">This article walks you through the steps for creating a Service Fabric standalone cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="f5b83-108">Este pacote autônomo do Windows Server está disponível para venda e pode ser usado para implantações de produção.</span><span class="sxs-lookup"><span data-stu-id="f5b83-108">This standalone Windows Server package is commercially available and may be used for production deployments.</span></span> <span data-ttu-id="f5b83-109">Este pacote pode conter novos recursos do Service Fabric que estão em “Visualização”.</span><span class="sxs-lookup"><span data-stu-id="f5b83-109">This package may contain new Service Fabric features that are in "Preview".</span></span> <span data-ttu-id="f5b83-110">Role para baixo até “[Recursos de visualização incluídos neste pacote](#previewfeatures_anchor)”.</span><span class="sxs-lookup"><span data-stu-id="f5b83-110">Scroll down to "[Preview features included in this package](#previewfeatures_anchor)."</span></span> <span data-ttu-id="f5b83-111">para obter uma lista dos recursos da visualização.</span><span class="sxs-lookup"><span data-stu-id="f5b83-111">section for the list of the preview features.</span></span> <span data-ttu-id="f5b83-112">Você pode [baixar uma cópia do EULA](http://go.microsoft.com/fwlink/?LinkID=733084) agora.</span><span class="sxs-lookup"><span data-stu-id="f5b83-112">You can [download a copy of the EULA](http://go.microsoft.com/fwlink/?LinkID=733084) now.</span></span>
> 
> 

<a id="getsupport"></a>

## <a name="get-support-for-the-service-fabric-for-windows-server-package"></a><span data-ttu-id="f5b83-113">Obter suporte para o pacote do Service Fabric para Windows Server</span><span class="sxs-lookup"><span data-stu-id="f5b83-113">Get support for the Service Fabric for Windows Server package</span></span>
* <span data-ttu-id="f5b83-114">Pergunte à comunidade sobre o pacote autônomo do Service Fabric para Windows Server no [Fórum do Service Fabric do Azure](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).</span><span class="sxs-lookup"><span data-stu-id="f5b83-114">Ask the community about the Service Fabric standalone package for Windows Server in the [Azure Service Fabric forum](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).</span></span>
* <span data-ttu-id="f5b83-115">Abra um tíquete de [Suporte Profissional para o Service Fabric](http://support.microsoft.com/oas/default.aspx?prid=16146).</span><span class="sxs-lookup"><span data-stu-id="f5b83-115">Open a ticket for [Professional Support for Service Fabric](http://support.microsoft.com/oas/default.aspx?prid=16146).</span></span>  <span data-ttu-id="f5b83-116">Saiba mais sobre o Suporte Profissional da Microsoft [aqui](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).</span><span class="sxs-lookup"><span data-stu-id="f5b83-116">Learn more about Professional Support from Microsoft [here](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).</span></span>
* <span data-ttu-id="f5b83-117">Você também pode obter suporte para este pacote como parte do [Suporte Premier da Microsoft](https://support.microsoft.com/en-us/premier).</span><span class="sxs-lookup"><span data-stu-id="f5b83-117">You can also get support for this package as a part of [Microsoft Premier Support](https://support.microsoft.com/en-us/premier).</span></span>
* <span data-ttu-id="f5b83-118">Para obter mais detalhes, consulte as [Opções de suporte do Azure Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).</span><span class="sxs-lookup"><span data-stu-id="f5b83-118">For more details, please see [Azure Service Fabric support options](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).</span></span>
* <span data-ttu-id="f5b83-119">Para coletar logs para fins de suporte, execute o [Coletor de logs Autônomo do Service Fabric](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="f5b83-119">To collect logs for support purposes, run the [Service Fabric Standalone Log collector](service-fabric-cluster-standalone-package-contents.md).</span></span>

<a id="downloadpackage"></a>

## <a name="download-the-service-fabric-for-windows-server-package"></a><span data-ttu-id="f5b83-120">Baixar o pacote do Service Fabric para Windows Server</span><span class="sxs-lookup"><span data-stu-id="f5b83-120">Download the Service Fabric for Windows Server package</span></span>
<span data-ttu-id="f5b83-121">Para criar o cluster, use o pacote do Service Fabric para Windows Server (Windows Server 2012 R2 e mais recente) encontrado aqui:</span><span class="sxs-lookup"><span data-stu-id="f5b83-121">To create the cluster, use the Service Fabric for Windows Server package (Windows Server 2012 R2 and newer) found here:</span></span> <br><span data-ttu-id="f5b83-122">
[Link de Download – pacote autônomo do Service Fabric – Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)</span><span class="sxs-lookup"><span data-stu-id="f5b83-122">
[Download Link - Service Fabric Standalone Package - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)</span></span>

<span data-ttu-id="f5b83-123">Encontre detalhes sobre o conteúdo do pacote [aqui](service-fabric-cluster-standalone-package-contents.md).</span><span class="sxs-lookup"><span data-stu-id="f5b83-123">Find details on contents of the package [here](service-fabric-cluster-standalone-package-contents.md).</span></span>

<span data-ttu-id="f5b83-124">O pacote de tempo de execução do Service Fabric é baixado automaticamente no momento da criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="f5b83-124">The Service Fabric runtime package is automatically downloaded at time of cluster creation.</span></span> <span data-ttu-id="f5b83-125">Se for implantar de um computador não conectado à Internet, baixe o pacote de tempo de execução fora de banda aqui:</span><span class="sxs-lookup"><span data-stu-id="f5b83-125">If deploying from a machine not connected to the internet, please download the runtime package out of band from here:</span></span> <br><span data-ttu-id="f5b83-126">
[Link de Download – Tempo de Execução do Service Fabric – Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)</span><span class="sxs-lookup"><span data-stu-id="f5b83-126">
[Download Link - Service Fabric Runtime - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)</span></span>

<span data-ttu-id="f5b83-127">Encontre amostras de configuração de cluster autônomo em:</span><span class="sxs-lookup"><span data-stu-id="f5b83-127">Find Standalone Cluster Configuration samples at:</span></span> <br><span data-ttu-id="f5b83-128">
[Amostras de configuração de cluster autônomo](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span><span class="sxs-lookup"><span data-stu-id="f5b83-128">
[Standalone Cluster Configuration Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span></span>

<a id="createcluster"></a>

## <a name="create-the-cluster"></a><span data-ttu-id="f5b83-129">Criar o cluster</span><span class="sxs-lookup"><span data-stu-id="f5b83-129">Create the cluster</span></span>
<span data-ttu-id="f5b83-130">O Service Fabric pode ser implantado em um cluster de desenvolvimento de um computador usando o arquivo *ClusterConfig.Unsecure.DevCluster.json* incluído em [Amostras](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="f5b83-130">Service Fabric can be deployed to a one-machine development cluster by using the *ClusterConfig.Unsecure.DevCluster.json* file included in [Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).</span></span>

<span data-ttu-id="f5b83-131">Descompacte o pacote autônomo no seu computador, copie o arquivo de configuração de exemplo para o computador local, execute o script *CreateServiceFabricCluster.ps1* por meio de uma sessão do PowerShell do administrador, da pasta de pacote autônomo:</span><span class="sxs-lookup"><span data-stu-id="f5b83-131">Unpack the standalone package to your machine, copy the sample config file to the local machine, then run the *CreateServiceFabricCluster.ps1* script through an administrator PowerShell session, from the standalone package folder:</span></span>
### <a name="step-1a-create-an-unsecured-local-development-cluster"></a><span data-ttu-id="f5b83-132">Etapa 1A: criar um cluster de desenvolvimento local desprotegido</span><span class="sxs-lookup"><span data-stu-id="f5b83-132">Step 1A: Create an unsecured local development cluster</span></span>
```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

<span data-ttu-id="f5b83-133">Consulte a seção Configuração do ambiente em [Planejar e preparar a implantação do cluster](service-fabric-cluster-standalone-deployment-preparation.md) para obter detalhes de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="f5b83-133">See the Environment Setup section at [Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md) for troubleshooting details.</span></span>

<span data-ttu-id="f5b83-134">Se você concluiu a execução de cenários de desenvolvimento, poderá remover o cluster do Service Fabric do computador consultando as etapas na seção “[Remover um cluster](#removecluster_anchor)”.</span><span class="sxs-lookup"><span data-stu-id="f5b83-134">If you're finished running development scenarios, you can remove the Service Fabric cluster from the machine by referring to steps in section "[Remove a cluster](#removecluster_anchor)".</span></span> 

### <a name="step-1b-create-a-multi-machine-cluster"></a><span data-ttu-id="f5b83-135">Etapa 1B: criar um cluster com vários computadores</span><span class="sxs-lookup"><span data-stu-id="f5b83-135">Step 1B: Create a multi-machine cluster</span></span>
<span data-ttu-id="f5b83-136">Depois que tiver verificado o planejamento e etapas de preparação detalhadas no link abaixo, você estará pronto para criar seu cluster de produção usando o arquivo de configuração do cluster.</span><span class="sxs-lookup"><span data-stu-id="f5b83-136">After you have gone through the planning and preparation steps detailed at the below link, you are ready to create your production cluster using your cluster configuration file.</span></span> <br><span data-ttu-id="f5b83-137">
[Planejar e preparar a implantação do cluster](service-fabric-cluster-standalone-deployment-preparation.md)</span><span class="sxs-lookup"><span data-stu-id="f5b83-137">
[Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md)</span></span>

1. <span data-ttu-id="f5b83-138">Valide o arquivo de configuração que você gravou escrito executando o script *TestConfiguration.ps1* da pasta do pacote autônomo:</span><span class="sxs-lookup"><span data-stu-id="f5b83-138">Validate the configuration file you have written by running the *TestConfiguration.ps1* script from the standalone package folder:</span></span>  

    ```powershell
    .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.json
    ```

    <span data-ttu-id="f5b83-139">Você deverá ver uma saída como a abaixo.</span><span class="sxs-lookup"><span data-stu-id="f5b83-139">You should see output like below.</span></span> <span data-ttu-id="f5b83-140">Se o campo inferior "Passed" é retornado como "True", as verificações de integridade são aprovadas e o cluster parece estar pronto para implantação com base na configuração de entrada.</span><span class="sxs-lookup"><span data-stu-id="f5b83-140">If the bottom field "Passed" is returned as "True", sanity checks have passed and the cluster looks to be deployable based on the input configuration.</span></span>

    ```
    Trace folder already exists. Traces will be written to existing trace folder: C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer\DeploymentTraces
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

2. <span data-ttu-id="f5b83-141">Criar o cluster: execute o script *CreateServiceFabricCluster.ps1* para implantar o cluster do Service Fabric em cada computador na configuração.</span><span class="sxs-lookup"><span data-stu-id="f5b83-141">Create the cluster:  Run the *CreateServiceFabricCluster.ps1* script to deploy the Service Fabric cluster across each machine in the configuration.</span></span> 
    ```powershell
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -AcceptEULA
    ```

> [!NOTE]
> <span data-ttu-id="f5b83-142">Rastreamentos de implantação são gravados na VM/computador em que você executou o script do PowerShell CreateServiceFabricCluster.ps1.</span><span class="sxs-lookup"><span data-stu-id="f5b83-142">Deployment traces are written to the VM/machine on which you ran the CreateServiceFabricCluster.ps1 PowerShell script.</span></span> <span data-ttu-id="f5b83-143">Eles podem ser encontrados na subpasta DeploymentTraces, com base no diretório do qual o script foi executado.</span><span class="sxs-lookup"><span data-stu-id="f5b83-143">These can be found in the subfolder DeploymentTraces, based in the directory from which the script was run.</span></span> <span data-ttu-id="f5b83-144">Para ver se o Service Fabric foi implantado corretamente em um computador, localize os arquivos instalados no diretório FabricDataRoot, conforme detalhado na seção FabricSettings do arquivo de configuração de cluster (por padrão, c:\ProgramData\SF).</span><span class="sxs-lookup"><span data-stu-id="f5b83-144">To see if Service Fabric was deployed correctly to a machine, find the installed files in the FabricDataRoot directory, as detailed in the cluster configuration file FabricSettings section (by default c:\ProgramData\SF).</span></span> <span data-ttu-id="f5b83-145">Além disso, processos FabricHost.exe e Fabric.exe podem ser vistos em execução no Gerenciador de Tarefas.</span><span class="sxs-lookup"><span data-stu-id="f5b83-145">As well, FabricHost.exe and Fabric.exe processes can be seen running in Task Manager.</span></span>
> 
> 

### <a name="step-1c-create-an-offline-internet-disconnected-cluster"></a><span data-ttu-id="f5b83-146">Etapa 1C: Criar um cluster offline (desconectado da Internet)</span><span class="sxs-lookup"><span data-stu-id="f5b83-146">Step 1C: Create an offline (internet-disconnected) cluster</span></span>
<span data-ttu-id="f5b83-147">O pacote de tempo de execução do Service Fabric é baixado automaticamente durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="f5b83-147">The Service Fabric runtime package is automatically downloaded at cluster creation.</span></span> <span data-ttu-id="f5b83-148">Ao implantar um cluster em computadores que não estão conectados à Internet, você precisará baixar o pacote de tempo de execução do Service Fabric separadamente e fornecer o caminho para ele durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="f5b83-148">When deploying a cluster to machines not connected to the internet, you will need to download the Service Fabric runtime package separately, and provide the path to it at cluster creation.</span></span>
<span data-ttu-id="f5b83-149">O pacote de tempo de execução pode ser baixado separadamente, em outro computador conectado à Internet, em [Link de Download – Tempo de Execução do Service Fabric – Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).</span><span class="sxs-lookup"><span data-stu-id="f5b83-149">The runtime package can be downloaded separately, from another machine connected to the internet, at [Download Link - Service Fabric Runtime - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).</span></span> <span data-ttu-id="f5b83-150">Copie o pacote de tempo de execução para o local de origem da implantação do cluster offline e crie o cluster executando `CreateServiceFabricCluster.ps1` com o parâmetro `-FabricRuntimePackagePath` incluído, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="f5b83-150">Copy the runtime package to where you are deploying the offline cluster from, and create the cluster by running `CreateServiceFabricCluster.ps1` with the `-FabricRuntimePackagePath` parameter included, as shown below:</span></span> 

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -FabricRuntimePackagePath .\MicrosoftAzureServiceFabric.cab
```
<span data-ttu-id="f5b83-151">em que `.\ClusterConfig.json` e `.\MicrosoftAzureServiceFabric.cab` são os caminhos para a configuração do cluster e o arquivo .cab de tempo de execução, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="f5b83-151">where `.\ClusterConfig.json` and `.\MicrosoftAzureServiceFabric.cab` are the paths to the cluster configuration and the runtime .cab file respectively.</span></span>


### <a name="step-2-connect-to-the-cluster"></a><span data-ttu-id="f5b83-152">Etapa 2: conectar-se ao cluster</span><span class="sxs-lookup"><span data-stu-id="f5b83-152">Step 2: Connect to the cluster</span></span>
<span data-ttu-id="f5b83-153">Para se conectar a um cluster seguro, confira [Service fabric connect to secure cluster](service-fabric-connect-to-secure-cluster.md) (Conexão do Service Fabric com um cluster seguro).</span><span class="sxs-lookup"><span data-stu-id="f5b83-153">To connect to a secure cluster, see [Service fabric connect to secure cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

<span data-ttu-id="f5b83-154">Para se conectar a um cluster não seguro, execute o seguinte comando do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="f5b83-154">To connect to an unsecure cluster, run the following PowerShell command:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <*IPAddressofaMachine*>:<Client connection end point port>
```
<span data-ttu-id="f5b83-155">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="f5b83-155">Example:</span></span>
```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint 192.13.123.2345:19000
```
### <a name="step-3-bring-up-service-fabric-explorer"></a><span data-ttu-id="f5b83-156">Etapa 3: abrir o Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="f5b83-156">Step 3: Bring up Service Fabric Explorer</span></span>
<span data-ttu-id="f5b83-157">Agora, você pode conectar o cluster com o Service Fabric Explorer diretamente de um dos computadores com http://localhost:19080/Explorer/index.html ou remotamente com http://<*IPAddressofaMachine*>:19080/Explorer/index.html.</span><span class="sxs-lookup"><span data-stu-id="f5b83-157">Now you can connect to the cluster with Service Fabric Explorer either directly from one of the machines with http://localhost:19080/Explorer/index.html or remotely with http://<*IPAddressofaMachine*>:19080/Explorer/index.html.</span></span>

## <a name="add-and-remove-nodes"></a><span data-ttu-id="f5b83-158">Adicionar e remover nós</span><span class="sxs-lookup"><span data-stu-id="f5b83-158">Add and remove nodes</span></span>
<span data-ttu-id="f5b83-159">Você pode adicionar ou remover os nós do cluster do Service Fabric autônomo quando seu negócio precisa mudar.</span><span class="sxs-lookup"><span data-stu-id="f5b83-159">You can add or remove nodes to your standalone Service Fabric cluster as your business needs change.</span></span> <span data-ttu-id="f5b83-160">Confira [Adicionar ou remover nós de um cluster do Service Fabric autônomo](service-fabric-cluster-windows-server-add-remove-nodes.md) para ver as etapas detalhadas.</span><span class="sxs-lookup"><span data-stu-id="f5b83-160">See [Add or Remove nodes to a Service Fabric standalone cluster](service-fabric-cluster-windows-server-add-remove-nodes.md) for detailed steps.</span></span>

<a id="removecluster" name="removecluster_anchor"></a>
## <a name="remove-a-cluster"></a><span data-ttu-id="f5b83-161">Remover um cluster</span><span class="sxs-lookup"><span data-stu-id="f5b83-161">Remove a cluster</span></span>
<span data-ttu-id="f5b83-162">Para remover um cluster, execute o script do PowerShell *RemoveServiceFabricCluster.ps1* da pasta do pacote e transmita o caminho para o arquivo de configuração JSON.</span><span class="sxs-lookup"><span data-stu-id="f5b83-162">To remove a cluster, run the *RemoveServiceFabricCluster.ps1* PowerShell script from the package folder and pass in the path to the JSON configuration file.</span></span> <span data-ttu-id="f5b83-163">Como alternativa, você pode especificar um local para o log de exclusão.</span><span class="sxs-lookup"><span data-stu-id="f5b83-163">You can optionally specify a location for the log of the deletion.</span></span>

<span data-ttu-id="f5b83-164">Esse script pode ser executado em qualquer computador que tenha o acesso de administrador para todos os computadores listados como nós no arquivo de configuração do cluster.</span><span class="sxs-lookup"><span data-stu-id="f5b83-164">This script can be run on any machine that has administrator access to all the machines that are listed as nodes in the cluster configuration file.</span></span> <span data-ttu-id="f5b83-165">O computador no qual este script é executado não precisa fazer parte do cluster.</span><span class="sxs-lookup"><span data-stu-id="f5b83-165">The machine that this script is run on does not have to be part of the cluster.</span></span>

```
# Removes Service Fabric from each machine in the configuration
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -Force
```

```
# Removes Service Fabric from the current machine
.\CleanFabric.ps1
```

<a id="telemetry"></a>

## <a name="telemetry-data-collected-and-how-to-opt-out-of-it"></a><span data-ttu-id="f5b83-166">Dados de telemetria coletados e como recusá-los</span><span class="sxs-lookup"><span data-stu-id="f5b83-166">Telemetry data collected and how to opt out of it</span></span>
<span data-ttu-id="f5b83-167">Por padrão, o produto coleta a telemetria sobre o uso do Service Fabric para aprimorar o produto.</span><span class="sxs-lookup"><span data-stu-id="f5b83-167">As a default, the product collects telemetry on the Service Fabric usage to improve the product.</span></span> <span data-ttu-id="f5b83-168">O Analisador de Práticas Recomendadas executado como parte da instalação verifica a conectividade para [https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1).</span><span class="sxs-lookup"><span data-stu-id="f5b83-168">The Best Practice Analyzer that runs as a part of the setup checks for connectivity to [https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1).</span></span> <span data-ttu-id="f5b83-169">Se ele não estiver acessível, a instalação falhará, a menos que você recuse a telemetria.</span><span class="sxs-lookup"><span data-stu-id="f5b83-169">If it is not reachable, the setup fails unless you opt out of telemetry.</span></span>

1. <span data-ttu-id="f5b83-170">O pipeline de telemetria tenta carregar os dados a seguir para [https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) uma vez por dia.</span><span class="sxs-lookup"><span data-stu-id="f5b83-170">The telemetry pipeline tries to upload the following data to [https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) once every day.</span></span> <span data-ttu-id="f5b83-171">É um upload de melhor esforço e não causa nenhum impacto sobre a funcionalidade do cluster.</span><span class="sxs-lookup"><span data-stu-id="f5b83-171">It is a best-effort upload and has no impact on the cluster functionality.</span></span> <span data-ttu-id="f5b83-172">A telemetria é enviada somente do nó que executa o gerenciador de failover primário.</span><span class="sxs-lookup"><span data-stu-id="f5b83-172">The telemetry is only sent from the node that runs the failover manager primary.</span></span> <span data-ttu-id="f5b83-173">Nenhum outro nó envia telemetria.</span><span class="sxs-lookup"><span data-stu-id="f5b83-173">No other nodes send out telemetry.</span></span>
2. <span data-ttu-id="f5b83-174">A Telemetria consiste no seguinte:</span><span class="sxs-lookup"><span data-stu-id="f5b83-174">The telemetry consists of the following:</span></span>

* <span data-ttu-id="f5b83-175">Número de serviços</span><span class="sxs-lookup"><span data-stu-id="f5b83-175">Number of services</span></span>
* <span data-ttu-id="f5b83-176">Número de ServiceTypes</span><span class="sxs-lookup"><span data-stu-id="f5b83-176">Number of ServiceTypes</span></span>
* <span data-ttu-id="f5b83-177">Número de Aplicativos</span><span class="sxs-lookup"><span data-stu-id="f5b83-177">Number of Applications</span></span>
* <span data-ttu-id="f5b83-178">Número de ApplicationUpgrades</span><span class="sxs-lookup"><span data-stu-id="f5b83-178">Number of ApplicationUpgrades</span></span>
* <span data-ttu-id="f5b83-179">Número de FailoverUnits</span><span class="sxs-lookup"><span data-stu-id="f5b83-179">Number of FailoverUnits</span></span>
* <span data-ttu-id="f5b83-180">Número de InBuildFailoverUnits</span><span class="sxs-lookup"><span data-stu-id="f5b83-180">Number of InBuildFailoverUnits</span></span>
* <span data-ttu-id="f5b83-181">Número de UnhealthyFailoverUnits</span><span class="sxs-lookup"><span data-stu-id="f5b83-181">Number of UnhealthyFailoverUnits</span></span>
* <span data-ttu-id="f5b83-182">Número de Réplicas</span><span class="sxs-lookup"><span data-stu-id="f5b83-182">Number of Replicas</span></span>
* <span data-ttu-id="f5b83-183">Número de InBuildReplicas</span><span class="sxs-lookup"><span data-stu-id="f5b83-183">Number of InBuildReplicas</span></span>
* <span data-ttu-id="f5b83-184">Número de StandByReplicas</span><span class="sxs-lookup"><span data-stu-id="f5b83-184">Number of StandByReplicas</span></span>
* <span data-ttu-id="f5b83-185">Número de OfflineReplicas</span><span class="sxs-lookup"><span data-stu-id="f5b83-185">Number of OfflineReplicas</span></span>
* <span data-ttu-id="f5b83-186">CommonQueueLength</span><span class="sxs-lookup"><span data-stu-id="f5b83-186">CommonQueueLength</span></span>
* <span data-ttu-id="f5b83-187">QueryQueueLength</span><span class="sxs-lookup"><span data-stu-id="f5b83-187">QueryQueueLength</span></span>
* <span data-ttu-id="f5b83-188">FailoverUnitQueueLength</span><span class="sxs-lookup"><span data-stu-id="f5b83-188">FailoverUnitQueueLength</span></span>
* <span data-ttu-id="f5b83-189">CommitQueueLength</span><span class="sxs-lookup"><span data-stu-id="f5b83-189">CommitQueueLength</span></span>
* <span data-ttu-id="f5b83-190">Número de Nós</span><span class="sxs-lookup"><span data-stu-id="f5b83-190">Number of Nodes</span></span>
* <span data-ttu-id="f5b83-191">IsContextComplete: True/False</span><span class="sxs-lookup"><span data-stu-id="f5b83-191">IsContextComplete: True/False</span></span>
* <span data-ttu-id="f5b83-192">ClusterId: esse é um GUID gerado aleatoriamente para cada cluster</span><span class="sxs-lookup"><span data-stu-id="f5b83-192">ClusterId: This is a GUID randomly generated for each cluster</span></span>
* <span data-ttu-id="f5b83-193">ServiceFabricVersion</span><span class="sxs-lookup"><span data-stu-id="f5b83-193">ServiceFabricVersion</span></span>
* <span data-ttu-id="f5b83-194">Endereço IP da máquina virtual ou computador por meio do qual a telemetria é carregada</span><span class="sxs-lookup"><span data-stu-id="f5b83-194">IP address of the virtual machine or machine from which the telemetry is uploaded</span></span>

<span data-ttu-id="f5b83-195">Para desabilitar a telemetria, adicione o seguinte ao elemento *propriedades* em sua configuração de cluster: *enableTelemetry: false*.</span><span class="sxs-lookup"><span data-stu-id="f5b83-195">To disable telemetry, add the following to *properties* in your cluster config: *enableTelemetry: false*.</span></span>

<a id="previewfeatures" name="previewfeatures_anchor"></a>

## <a name="preview-features-included-in-this-package"></a><span data-ttu-id="f5b83-196">Recursos de preview incluídos neste pacote</span><span class="sxs-lookup"><span data-stu-id="f5b83-196">Preview features included in this package</span></span>
<span data-ttu-id="f5b83-197">Nenhuma.</span><span class="sxs-lookup"><span data-stu-id="f5b83-197">None.</span></span>


> [!NOTE]
> <span data-ttu-id="f5b83-198">A partir da nova [versão GA do cluster autônomo para Windows Server (versão 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), você pode atualizar seu cluster para versões futuras, de modo manual ou automático.</span><span class="sxs-lookup"><span data-stu-id="f5b83-198">Starting with the new [GA version of the standalone cluster for Windows Server (version 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), you can upgrade your cluster to future releases, manually or automatically.</span></span> <span data-ttu-id="f5b83-199">Consulte o documento [Atualizar uma versão autônoma do cluster do Service Fabric](service-fabric-cluster-upgrade-windows-server.md) para ver mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="f5b83-199">Refer to [Upgrade a standalone Service Fabric cluster version](service-fabric-cluster-upgrade-windows-server.md) document for details.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="f5b83-200">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f5b83-200">Next steps</span></span>
* [<span data-ttu-id="f5b83-201">Implantar e remover aplicativos usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5b83-201">Deploy and remove applications using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="f5b83-202">Definições de configuração para o cluster autônomo no Windows</span><span class="sxs-lookup"><span data-stu-id="f5b83-202">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="f5b83-203">Adicionar ou remover nós de um cluster do Service Fabric autônomo</span><span class="sxs-lookup"><span data-stu-id="f5b83-203">Add or remove nodes to a standalone Service Fabric cluster</span></span>](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [<span data-ttu-id="f5b83-204">Atualizar uma versão autônoma de cluster do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f5b83-204">Upgrade a standalone Service Fabric cluster version</span></span>](service-fabric-cluster-upgrade-windows-server.md)
* [<span data-ttu-id="f5b83-205">Criar um cluster do Service Fabric autônomo com VMs do Azure executando o Windows</span><span class="sxs-lookup"><span data-stu-id="f5b83-205">Create a standalone Service Fabric cluster with Azure VMs running Windows</span></span>](service-fabric-cluster-creation-with-windows-azure-vms.md)
* [<span data-ttu-id="f5b83-206">Proteger um cluster autônomo no Windows usando a segurança</span><span class="sxs-lookup"><span data-stu-id="f5b83-206">Secure a standalone cluster on Windows using Windows security</span></span>](service-fabric-windows-cluster-windows-security.md)
* [<span data-ttu-id="f5b83-207">Proteger um cluster autônomo no Windows usando os certificados X509</span><span class="sxs-lookup"><span data-stu-id="f5b83-207">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)

<!--Image references-->
[Trusted Zone]: ./media/service-fabric-cluster-creation-for-windows-server/TrustedZone.png
