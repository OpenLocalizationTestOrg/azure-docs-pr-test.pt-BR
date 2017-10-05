---
title: "Implantação de aplicativos do Azure Service Fabric | Microsoft Docs"
description: Use as APIs de FabricClient para implantar e remover aplicativos no Service Fabric.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: b120ffbf-f1e3-4b26-a492-347c29f8f66b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/07/2017
ms.author: ryanwi
ms.openlocfilehash: 2e4ca1069b4e8e473b26b790e81770b41e25ff50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-and-remove-applications-using-fabricclient"></a><span data-ttu-id="89a57-103">Implantar e remover aplicativos usando FabricClient</span><span class="sxs-lookup"><span data-stu-id="89a57-103">Deploy and remove applications using FabricClient</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="89a57-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="89a57-104">PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
> * [<span data-ttu-id="89a57-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="89a57-105">Visual Studio</span></span>](service-fabric-publish-app-remote-cluster.md)
> * [<span data-ttu-id="89a57-106">APIs de FabricClient</span><span class="sxs-lookup"><span data-stu-id="89a57-106">FabricClient APIs</span></span>](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

<span data-ttu-id="89a57-107">Assim que um [tipo de aplicativo for empacotado][10], ele está pronto para implantação em um cluster do Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="89a57-107">Once an [application type has been packaged][10], it's ready for deployment into an Azure Service Fabric cluster.</span></span> <span data-ttu-id="89a57-108">A implantação envolve as três etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="89a57-108">Deployment involves the following three steps:</span></span>

1. <span data-ttu-id="89a57-109">Carregar o pacote de aplicativos no repositório de imagens</span><span class="sxs-lookup"><span data-stu-id="89a57-109">Upload the application package to the image store</span></span>
2. <span data-ttu-id="89a57-110">Registrar o tipo de aplicativo</span><span class="sxs-lookup"><span data-stu-id="89a57-110">Register the application type</span></span>
3. <span data-ttu-id="89a57-111">Criar a instância do aplicativo</span><span class="sxs-lookup"><span data-stu-id="89a57-111">Create the application instance</span></span>

<span data-ttu-id="89a57-112">Depois que um aplicativo é implantado e uma instância está em execução no cluster, você pode excluir a instância do aplicativo e o tipo de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="89a57-112">After an application is deployed and an instance is running in the cluster, you can delete the application instance and its application type.</span></span> <span data-ttu-id="89a57-113">Remover completamente um aplicativo do cluster envolve as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="89a57-113">To completely remove an application from the cluster involves the following steps:</span></span>

1. <span data-ttu-id="89a57-114">Remover (ou excluir) a execução da instância do aplicativo</span><span class="sxs-lookup"><span data-stu-id="89a57-114">Remove (or delete) the running application instance</span></span>
2. <span data-ttu-id="89a57-115">Cancelar o registro do tipo de aplicativo se você não precisar mais dele</span><span class="sxs-lookup"><span data-stu-id="89a57-115">Unregister the application type if you no longer need it</span></span>
3. <span data-ttu-id="89a57-116">Remover o pacote de aplicativos do repositório de imagens</span><span class="sxs-lookup"><span data-stu-id="89a57-116">Remove the application package from the image store</span></span>

<span data-ttu-id="89a57-117">Se você usar o [Visual Studio para implantar e depurar aplicativos](service-fabric-publish-app-remote-cluster.md) no cluster de desenvolvimento local, todas as etapas anteriores serão tratadas automaticamente por meio de um script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="89a57-117">If you use [Visual Studio for deploying and debugging applications](service-fabric-publish-app-remote-cluster.md) on your local development cluster, all the preceding steps are handled automatically through a PowerShell script.</span></span>  <span data-ttu-id="89a57-118">Esse script é encontrado na pasta *Scripts* do projeto do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="89a57-118">This script is found in the *Scripts* folder of the application project.</span></span> <span data-ttu-id="89a57-119">Este artigo fornece informações sobre o que esse script faz para que você possa executar as mesmas operações fora do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="89a57-119">This article provides background on what that script is doing so that you can perform the same operations outside of Visual Studio.</span></span> 
 
## <a name="connect-to-the-cluster"></a><span data-ttu-id="89a57-120">Conectar-se ao cluster</span><span class="sxs-lookup"><span data-stu-id="89a57-120">Connect to the cluster</span></span>
<span data-ttu-id="89a57-121">Conecte-se ao cluster criando uma instância [FabricClient](/dotnet/api/system.fabric.fabricclient) antes de executar qualquer um dos exemplos de código neste artigo.</span><span class="sxs-lookup"><span data-stu-id="89a57-121">Connect to the cluster by creating a [FabricClient](/dotnet/api/system.fabric.fabricclient) instance before you run any of the code examples in this article.</span></span> <span data-ttu-id="89a57-122">Para obter exemplos de como se conectar a um cluster de desenvolvimento local ou a um cluster remoto ou protegido usando o Azure Active Directory, certificados X509 ou o Microsoft Active Directory, consulte [Conectar a um cluster seguro](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis).</span><span class="sxs-lookup"><span data-stu-id="89a57-122">For examples of connecting to a local development cluster or a remote cluster or cluster secured using Azure Active Directory, X509 certificates, or Windows Active Directory see [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis).</span></span> <span data-ttu-id="89a57-123">Para se conectar ao cluster de desenvolvimento local, execute o seguinte:</span><span class="sxs-lookup"><span data-stu-id="89a57-123">To connect to the local development cluster, run the following:</span></span>

```csharp
// Connect to the local cluster.
FabricClient fabricClient = new FabricClient();
```

## <a name="upload-the-application-package"></a><span data-ttu-id="89a57-124">Carregar o pacote de aplicativos</span><span class="sxs-lookup"><span data-stu-id="89a57-124">Upload the application package</span></span>
<span data-ttu-id="89a57-125">Suponha que você crie e empacote um aplicativo chamado *MyApplication* no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="89a57-125">Suppose you build and package an application named *MyApplication* in Visual Studio.</span></span> <span data-ttu-id="89a57-126">Por padrão, o nome do tipo de aplicativo listado no ApplicationManifest.xml é "MyApplicationType".</span><span class="sxs-lookup"><span data-stu-id="89a57-126">By default, the application type name listed in the ApplicationManifest.xml is "MyApplicationType".</span></span>  <span data-ttu-id="89a57-127">O pacote de aplicativos, que contém o manifesto do aplicativo, os manifestos do serviço e os pacotes de códigos/configurações/dados necessários, está localizado em *C:\Users\&lt;nome de usuário&gt;\Documents\Visual Studio 2017\Projects\MyApplication\MyApplication\pkg\Debug*.</span><span class="sxs-lookup"><span data-stu-id="89a57-127">The application package, which contains the necessary application manifest, service manifests, and code/config/data packages, is located in *C:\Users\&lt;username&gt;\Documents\Visual Studio 2017\Projects\MyApplication\MyApplication\pkg\Debug*.</span></span>

<span data-ttu-id="89a57-128">O carregamento do pacote de aplicativos coloca-o em um local acessível pelos componentes internos do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="89a57-128">Uploading the application package puts it in a location that's accessible by the internal Service Fabric components.</span></span> <span data-ttu-id="89a57-129">O Service Fabric verifica o pacote de aplicativos durante o registro do pacote de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="89a57-129">Service Fabric verifies the application package during the registration of the application package.</span></span> <span data-ttu-id="89a57-130">No entanto, se você quiser verificar o pacote de aplicativos localmente (ou seja, antes de carregá-lo), use o cmdlet [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="89a57-130">However, if you want to verify the application package locally (i.e., before uploading), use the [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="89a57-131">A API [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) carrega o pacote de aplicativos para o repositório de imagens do cluster.</span><span class="sxs-lookup"><span data-stu-id="89a57-131">The [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API uploads the application package to the cluster image store.</span></span> 

<span data-ttu-id="89a57-132">Se o pacote de aplicativos for grande e/ou tiver vários arquivos, será possível [compactá-lo](service-fabric-package-apps.md#compress-a-package) e copiá-lo para o repositório de imagens usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="89a57-132">If the application package is large and/or has many files, you can [compress it](service-fabric-package-apps.md#compress-a-package) and copy it to the image store using PowerShell.</span></span> <span data-ttu-id="89a57-133">A compactação reduz o tamanho e o número de arquivos.</span><span class="sxs-lookup"><span data-stu-id="89a57-133">The compression reduces the size and the number of files.</span></span>

<span data-ttu-id="89a57-134">Confira [Noções básicas sobre a configuração ImageStoreConnectionString](service-fabric-image-store-connection-string.md) para obter informações suplementares sobre o repositório de imagens e a cadeia de conexão de armazenamento de imagens.</span><span class="sxs-lookup"><span data-stu-id="89a57-134">See [Understand the image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about the image store and image store connection string.</span></span>

## <a name="register-the-application-package"></a><span data-ttu-id="89a57-135">Registrar o pacote de aplicativos</span><span class="sxs-lookup"><span data-stu-id="89a57-135">Register the application package</span></span>
<span data-ttu-id="89a57-136">O tipo e a versão do aplicativo declarados no manifesto do aplicativo tornam-se disponíveis para uso quando o pacote de aplicativos é registrado.</span><span class="sxs-lookup"><span data-stu-id="89a57-136">The application type and version declared in the application manifest become available for use when the application package is registered.</span></span> <span data-ttu-id="89a57-137">O sistema lê o pacote carregado na etapa anterior, verifica o pacote, processa o conteúdo do pacote e copia o pacote processado em um local interno do sistema.</span><span class="sxs-lookup"><span data-stu-id="89a57-137">The system reads the package uploaded in the previous step, verifies the package, processes the package contents, and copies the processed package to an internal system location.</span></span>  

<span data-ttu-id="89a57-138">A API [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) registra o tipo de aplicativo no cluster e o disponibiliza para implantação.</span><span class="sxs-lookup"><span data-stu-id="89a57-138">The [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API registers the application type in the cluster and make it available for deployment.</span></span>

<span data-ttu-id="89a57-139">A API [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) fornece informações sobre todos os tipos de aplicativo registrados com êxito.</span><span class="sxs-lookup"><span data-stu-id="89a57-139">The [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) API provides information about all successfully registered application types.</span></span> <span data-ttu-id="89a57-140">Você pode usar essa API para determinar quando o registro é feito.</span><span class="sxs-lookup"><span data-stu-id="89a57-140">You can use this API to determine when the registration is done.</span></span>

## <a name="create-an-application-instance"></a><span data-ttu-id="89a57-141">Criar uma instância do aplicativo</span><span class="sxs-lookup"><span data-stu-id="89a57-141">Create an application instance</span></span>
<span data-ttu-id="89a57-142">É possível criar uma instância de um aplicativo de qualquer tipo de aplicativo registrada com êxito usando a API [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync).</span><span class="sxs-lookup"><span data-stu-id="89a57-142">You can instantiate an application from any application type that has been registered successfully by using the [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) API.</span></span> <span data-ttu-id="89a57-143">O nome de cada aplicativo deve começar com o esquema *"fabric:"* e ser exclusivo para cada instância do aplicativo (dentro de um cluster).</span><span class="sxs-lookup"><span data-stu-id="89a57-143">The name of each application must start with the *"fabric:"* scheme and must be unique for each application instance (within a cluster).</span></span> <span data-ttu-id="89a57-144">Quaisquer serviços padrão definidos no manifesto do aplicativo do tipo de aplicativo de destino também são criados.</span><span class="sxs-lookup"><span data-stu-id="89a57-144">Any default services defined in the application manifest of the target application type are also created.</span></span>

<span data-ttu-id="89a57-145">Várias instâncias do aplicativo podem ser criadas para qualquer determinada versão de um tipo de aplicativo registrado.</span><span class="sxs-lookup"><span data-stu-id="89a57-145">Multiple application instances can be created for any given version of a registered application type.</span></span> <span data-ttu-id="89a57-146">Cada instância do aplicativo é executada isoladamente, com seu próprio diretório de trabalho e conjunto de processos.</span><span class="sxs-lookup"><span data-stu-id="89a57-146">Each application instance runs in isolation, with its own working directory and set of processes.</span></span>

<span data-ttu-id="89a57-147">Para ver quais aplicativos e serviços nomeados estão em execução no cluster, execute as APIs [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) e [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync).</span><span class="sxs-lookup"><span data-stu-id="89a57-147">To see which named applications and services are running in the cluster, run the [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) and [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) APIs.</span></span>

## <a name="create-a-service-instance"></a><span data-ttu-id="89a57-148">Crie uma instância de serviço</span><span class="sxs-lookup"><span data-stu-id="89a57-148">Create a service instance</span></span>
<span data-ttu-id="89a57-149">É possível criar uma instância de um serviço com base em um tipo de serviço de que usa a API [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync).</span><span class="sxs-lookup"><span data-stu-id="89a57-149">You can instantiate a service from a service type using the [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API.</span></span>  <span data-ttu-id="89a57-150">Se o serviço for declarado como um serviço padrão no manifesto do aplicativo, a instância desse serviço será criada com a criação da instância do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="89a57-150">If the service is declared as a default service in the application manifest, the service is instantiated when the application is instantiated.</span></span>  <span data-ttu-id="89a57-151">Chamar a API [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) para um serviço que já é instanciado retornará uma exceção do tipo FabricException, contendo um código de erro com um valor de FabricErrorCode.ServiceAlreadyExists.</span><span class="sxs-lookup"><span data-stu-id="89a57-151">Calling the [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API for a service that is already instantiated will return an exception of type FabricException containing an error code with a value of FabricErrorCode.ServiceAlreadyExists.</span></span>

## <a name="remove-a-service-instance"></a><span data-ttu-id="89a57-152">Remover uma instância de serviço</span><span class="sxs-lookup"><span data-stu-id="89a57-152">Remove a service instance</span></span>
<span data-ttu-id="89a57-153">Quando uma instância de serviço não for mais necessária, será possível removê-la da instância do aplicativo em execução chamando a API [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync).</span><span class="sxs-lookup"><span data-stu-id="89a57-153">When a service instance is no longer needed, you can remove it from the running application instance by calling the [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) API.</span></span>  

> [!WARNING]
> <span data-ttu-id="89a57-154">Essa operação não pode ser revertida e o estado do serviço não pode ser recuperado.</span><span class="sxs-lookup"><span data-stu-id="89a57-154">This operation cannot be reversed, and service state cannot be recovered.</span></span>

## <a name="remove-an-application-instance"></a><span data-ttu-id="89a57-155">Remover uma instância do aplicativo</span><span class="sxs-lookup"><span data-stu-id="89a57-155">Remove an application instance</span></span>
<span data-ttu-id="89a57-156">Quando a instância de um aplicativo não for mais necessária, será possível removê-la permanentemente pelo nome que usa a API [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync).</span><span class="sxs-lookup"><span data-stu-id="89a57-156">When an application instance is no longer needed, you can permanently remove it by name using the [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) API.</span></span> <span data-ttu-id="89a57-157">[DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) também remove automaticamente todos os serviços que pertencem ao aplicativo, removendo permanentemente todos os estados de serviço.</span><span class="sxs-lookup"><span data-stu-id="89a57-157">[DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) automatically removes all services that belong to the application as well, permanently removing all service state.</span></span>

> [!WARNING]
> <span data-ttu-id="89a57-158">Essa operação não pode ser revertida e o estado do aplicativo não pode ser recuperado.</span><span class="sxs-lookup"><span data-stu-id="89a57-158">This operation cannot be reversed, and application state cannot be recovered.</span></span>

## <a name="unregister-an-application-type"></a><span data-ttu-id="89a57-159">Cancelar o registro de um tipo de aplicativo</span><span class="sxs-lookup"><span data-stu-id="89a57-159">Unregister an application type</span></span>
<span data-ttu-id="89a57-160">Quando uma versão específica de um tipo de aplicativo não for mais necessária, você deve cancelar o registro dessa versão específica do tipo de aplicativo usando a API [Unregister-ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync).</span><span class="sxs-lookup"><span data-stu-id="89a57-160">When a particular version of an application type is no longer needed, you should unregister that particular version of the application type using the [Unregister-ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) API.</span></span> <span data-ttu-id="89a57-161">O cancelamento de registro de versões não utilizadas de tipos de aplicativo libera espaço de armazenamento usado pelo repositório de imagens.</span><span class="sxs-lookup"><span data-stu-id="89a57-161">Unregistering unused versions of application types releases storage space used by the image store.</span></span> <span data-ttu-id="89a57-162">Uma versão de um tipo de aplicativo pode ter seu registro cancelado, desde que não existam aplicativos instanciados nela nem nenhuma atualização de aplicativo pendente que faça referência a ela.</span><span class="sxs-lookup"><span data-stu-id="89a57-162">A version of an application type can be unregistered as long as no applications are instantiated against that version of the application type and no pending application upgrades are referencing that version of the application type.</span></span>

## <a name="remove-an-application-package-from-the-image-store"></a><span data-ttu-id="89a57-163">Remover um pacote de aplicativos do repositório de imagens</span><span class="sxs-lookup"><span data-stu-id="89a57-163">Remove an application package from the image store</span></span>
<span data-ttu-id="89a57-164">Quando um pacote de aplicativos não for mais necessário, será possível excluí-lo do repositório de imagens para liberar recursos do sistema usando a API [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage).</span><span class="sxs-lookup"><span data-stu-id="89a57-164">When an application package is no longer needed, you can delete it from the image store to free up system resources using the [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) API.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="89a57-165">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="89a57-165">Troubleshooting</span></span>
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a><span data-ttu-id="89a57-166">Copy-ServiceFabricApplicationPackage solicita um ImageStoreConnectionString</span><span class="sxs-lookup"><span data-stu-id="89a57-166">Copy-ServiceFabricApplicationPackage asks for an ImageStoreConnectionString</span></span>
<span data-ttu-id="89a57-167">O ambiente do SDK da Malha do Serviço já deve ter os padrões corretos configurados.</span><span class="sxs-lookup"><span data-stu-id="89a57-167">The Service Fabric SDK environment should already have the correct defaults set up.</span></span> <span data-ttu-id="89a57-168">Mas, se necessário, o ImageStoreConnectionString para todos os comandos deve corresponder ao valor que o cluster de Malha do Serviço está usando.</span><span class="sxs-lookup"><span data-stu-id="89a57-168">But if needed, the ImageStoreConnectionString for all commands should match the value that the Service Fabric cluster is using.</span></span> <span data-ttu-id="89a57-169">Você pode encontrar ImageStoreConnectionString no manifesto do cluster, recuperado usando os comandos [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) e Get-ImageStoreConnectionStringFromClusterManifest:</span><span class="sxs-lookup"><span data-stu-id="89a57-169">You can find the ImageStoreConnectionString in the cluster manifest, retrieved using the [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) and Get-ImageStoreConnectionStringFromClusterManifest commands:</span></span>

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

<span data-ttu-id="89a57-170">O cmdlet **Get-ImageStoreConnectionStringFromClusterManifest** , que faz parte do módulo do PowerShell do SDK do Service Fabric, é usado para obter a cadeia de conexão do repositório de imagens.</span><span class="sxs-lookup"><span data-stu-id="89a57-170">The **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of the Service Fabric SDK PowerShell module, is used to get the image store connection string.</span></span>  <span data-ttu-id="89a57-171">Para importar o módulo do SDK, execute:</span><span class="sxs-lookup"><span data-stu-id="89a57-171">To import the SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```


<span data-ttu-id="89a57-172">ImageStoreConnectionString é encontrado no manifesto do cluster:</span><span class="sxs-lookup"><span data-stu-id="89a57-172">The ImageStoreConnectionString is found in the cluster manifest:</span></span>

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

<span data-ttu-id="89a57-173">Confira [Noções básicas sobre a configuração ImageStoreConnectionString](service-fabric-image-store-connection-string.md) para obter informações suplementares sobre o repositório de imagens e a cadeia de conexão de armazenamento de imagens.</span><span class="sxs-lookup"><span data-stu-id="89a57-173">See [Understand the image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about the image store and image store connection string.</span></span>

### <a name="deploy-large-application-package"></a><span data-ttu-id="89a57-174">Implantar um pacote de aplicativos grande</span><span class="sxs-lookup"><span data-stu-id="89a57-174">Deploy large application package</span></span>
<span data-ttu-id="89a57-175">Problema: a API [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) atinge o tempo limite para um pacote de aplicativos grande (na ordem de GB).</span><span class="sxs-lookup"><span data-stu-id="89a57-175">Issue: [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API times out for a large application package (order of GB).</span></span>
<span data-ttu-id="89a57-176">Experimente:</span><span class="sxs-lookup"><span data-stu-id="89a57-176">Try:</span></span>
- <span data-ttu-id="89a57-177">Especificar um tempo limite maior para o método [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) com o parâmetro `timeout`.</span><span class="sxs-lookup"><span data-stu-id="89a57-177">Specify a larger timeout for [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) method, with `timeout` parameter.</span></span> <span data-ttu-id="89a57-178">Por padrão, o tempo limite é de 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="89a57-178">By default, the timeout is 30 minutes.</span></span>
- <span data-ttu-id="89a57-179">Verifique a conexão de rede entre o computador de origem e o cluster.</span><span class="sxs-lookup"><span data-stu-id="89a57-179">Check the network connection between your source machine and cluster.</span></span> <span data-ttu-id="89a57-180">Se a conexão estiver lenta, considere usar um computador com uma conexão de rede melhor.</span><span class="sxs-lookup"><span data-stu-id="89a57-180">If the connection is slow, consider using a machine with a better network connection.</span></span>
<span data-ttu-id="89a57-181">Se o computador cliente estiver em uma região diferente do cluster, considere usar um computador cliente em uma região mais próxima ou na mesma que o cluster.</span><span class="sxs-lookup"><span data-stu-id="89a57-181">If the client machine is in another region than the cluster, consider using a client machine in a closer or same region as the cluster.</span></span>
- <span data-ttu-id="89a57-182">Verifique se você está sofrendo limitação externa.</span><span class="sxs-lookup"><span data-stu-id="89a57-182">Check if you are hitting external throttling.</span></span> <span data-ttu-id="89a57-183">Por exemplo, quando o repositório de imagens é configurado para usar o Armazenamento do Azure, o upload pode ser limitado.</span><span class="sxs-lookup"><span data-stu-id="89a57-183">For example, when the image store is configured to use azure storage, upload may be throttled.</span></span>

<span data-ttu-id="89a57-184">Problema: o upload do pacote foi concluído com êxito, mas a API [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) atinge o tempo limite.</span><span class="sxs-lookup"><span data-stu-id="89a57-184">Issue: Upload package completed successfully, but [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API times out.</span></span>
<span data-ttu-id="89a57-185">Experimente:</span><span class="sxs-lookup"><span data-stu-id="89a57-185">Try:</span></span>
- <span data-ttu-id="89a57-186">[Compactar o pacote](service-fabric-package-apps.md#compress-a-package) antes de copiar para o repositório de imagens.</span><span class="sxs-lookup"><span data-stu-id="89a57-186">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store.</span></span>
<span data-ttu-id="89a57-187">A compactação reduz o tamanho e o número de arquivos, o que por sua vez reduz a quantidade de tráfego e trabalho que o Service Fabric deve executar.</span><span class="sxs-lookup"><span data-stu-id="89a57-187">The compression reduces the size and the number of files, which in turn reduces the amount of traffic and work that Service Fabric must perform.</span></span> <span data-ttu-id="89a57-188">A operação de upload pode ser mais lenta (especialmente se você incluir o tempo de compactação), mas as operações de registrar e cancelar o registro do tipo de aplicativo são mais rápidas.</span><span class="sxs-lookup"><span data-stu-id="89a57-188">The upload operation may be slower (especially if you include the compression time), but register and un-register the application type are faster.</span></span>
- <span data-ttu-id="89a57-189">Especifique um tempo limite maior para a API [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) com o parâmetro `timeout`.</span><span class="sxs-lookup"><span data-stu-id="89a57-189">Specify a larger timeout for [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API with `timeout` parameter.</span></span>

### <a name="deploy-application-package-with-many-files"></a><span data-ttu-id="89a57-190">Implantar pacote de aplicativos com muitos arquivos</span><span class="sxs-lookup"><span data-stu-id="89a57-190">Deploy application package with many files</span></span>
<span data-ttu-id="89a57-191">Problema: [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) atinge o tempo limite para um pacote de aplicativos com muitos arquivos (na ordem de milhares).</span><span class="sxs-lookup"><span data-stu-id="89a57-191">Issue: [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) times out for an application package with many files (order of thousands).</span></span>
<span data-ttu-id="89a57-192">Experimente:</span><span class="sxs-lookup"><span data-stu-id="89a57-192">Try:</span></span>
- <span data-ttu-id="89a57-193">[Compactar o pacote](service-fabric-package-apps.md#compress-a-package) antes de copiar para o repositório de imagens.</span><span class="sxs-lookup"><span data-stu-id="89a57-193">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store.</span></span> <span data-ttu-id="89a57-194">A compactação reduz o número de arquivos.</span><span class="sxs-lookup"><span data-stu-id="89a57-194">The compression reduces the number of files.</span></span>
- <span data-ttu-id="89a57-195">Especifique um tempo limite maior para [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) com o parâmetro `timeout`.</span><span class="sxs-lookup"><span data-stu-id="89a57-195">Specify a larger timeout for [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) with `timeout` parameter.</span></span>

## <a name="code-example"></a><span data-ttu-id="89a57-196">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="89a57-196">Code example</span></span>
<span data-ttu-id="89a57-197">O exemplo a seguir copia um pacote de aplicativos para o repositório de imagens, provisiona o tipo de aplicativo, cria uma instância do aplicativo, cria uma instância de serviço, remove a instância do aplicativo, cancela o provisionamento do tipo de aplicativo e exclui o pacote de aplicativos do repositório de imagens.</span><span class="sxs-lookup"><span data-stu-id="89a57-197">The following example copies an application package to the image store, provisions the application type, creates an application instance, creates a service instance, removes the application instance, un-provisions the application type, and deletes the application package from the image store.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Reflection;
using System.Threading.Tasks;

using System.Fabric;
using System.Fabric.Description;
using System.Threading;

namespace ServiceFabricAppLifecycle
{
class Program
{
static void Main(string[] args)
{

    string clusterConnection = "localhost:19000";
    string appName = "fabric:/MyApplication";
    string appType = "MyApplicationType";
    string appVersion = "1.0.0";
    string serviceName = "fabric:/MyApplication/Stateless1";
    string imageStoreConnectionString = "file:C:\\SfDevCluster\\Data\\ImageStoreShare";
    string packagePathInImageStore = "MyApplication";
    string packagePath = "C:\\Users\\username\\Documents\\Visual Studio 2017\\Projects\\MyApplication\\MyApplication\\pkg\\Debug";
    string serviceType = "Stateless1Type";

    // Connect to the cluster.
    FabricClient fabricClient = new FabricClient(clusterConnection);

    // Copy the application package to a location in the image store
    try
    {
        fabricClient.ApplicationManager.CopyApplicationPackage(imageStoreConnectionString, packagePath, packagePathInImageStore);
        Console.WriteLine("Application package copied to {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package copy to Image Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Provision the application.  "MyApplicationV1" is the folder in the image store where the application package is located. 
    // The application type with name "MyApplicationType" and version "1.0.0" (both are found in the application manifest) 
    // is now registered in the cluster.            
    try
    {
        fabricClient.ApplicationManager.ProvisionApplicationAsync(packagePathInImageStore).Wait();

        Console.WriteLine("Provisioned application type {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Provision Application Type failed:");

        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    //  Create the application instance.
    try
    {
        ApplicationDescription appDesc = new ApplicationDescription(new Uri(appName), appType, appVersion);
        fabricClient.ApplicationManager.CreateApplicationAsync(appDesc).Wait();
        Console.WriteLine("Created application instance of type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Create the stateless service description.  For stateful services, use a StatefulServiceDescription object.
    StatelessServiceDescription serviceDescription = new StatelessServiceDescription();
    serviceDescription.ApplicationName = new Uri(appName);
    serviceDescription.InstanceCount = 1;
    serviceDescription.PartitionSchemeDescription = new SingletonPartitionSchemeDescription();
    serviceDescription.ServiceName = new Uri(serviceName);
    serviceDescription.ServiceTypeName = serviceType;

    // Create the service instance.  If the service is declared as a default service in the ApplicationManifest.xml,
    // the service instance is already running and this call will fail.
    try
    {
        fabricClient.ServiceManager.CreateServiceAsync(serviceDescription).Wait();
        Console.WriteLine("Created service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("CreateService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete a service instance.
    try
    {
        DeleteServiceDescription deleteServiceDescription = new DeleteServiceDescription(new Uri(serviceName));

        fabricClient.ServiceManager.DeleteServiceAsync(deleteServiceDescription);
        Console.WriteLine("Deleted service instance {0}", serviceName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteService failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete an application instance from the application type.
    try
    {
        DeleteApplicationDescription deleteApplicationDescription = new DeleteApplicationDescription(new Uri(appName));

        fabricClient.ApplicationManager.DeleteApplicationAsync(deleteApplicationDescription).Wait();
        Console.WriteLine("Deleted application instance {0}", appName);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("DeleteApplication failed.");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Un-provision the application type.
    try
    {
        fabricClient.ApplicationManager.UnprovisionApplicationAsync(appType, appVersion).Wait();
        Console.WriteLine("Un-provisioned application type {0}, version {1}", appType, appVersion);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Un-provision application type failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Delete the application package from a location in the image store.
    try
    {
        fabricClient.ApplicationManager.RemoveApplicationPackage(imageStoreConnectionString, packagePathInImageStore);
        Console.WriteLine("Application package removed from {0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package removal from Image Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    Console.WriteLine("Hit enter...");
    Console.Read();
}        
}
}

```

## <a name="next-steps"></a><span data-ttu-id="89a57-198">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="89a57-198">Next steps</span></span>
[<span data-ttu-id="89a57-199">Atualização de aplicativos do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="89a57-199">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="89a57-200">Introdução à integridade da Malha do Serviço</span><span class="sxs-lookup"><span data-stu-id="89a57-200">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)

[<span data-ttu-id="89a57-201">Diagnosticar e solucionar problemas de um serviço da Malha do Serviço</span><span class="sxs-lookup"><span data-stu-id="89a57-201">Diagnose and troubleshoot a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="89a57-202">Modelar um aplicativo na Malha do Serviço</span><span class="sxs-lookup"><span data-stu-id="89a57-202">Model an application in Service Fabric</span></span>](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before the slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
