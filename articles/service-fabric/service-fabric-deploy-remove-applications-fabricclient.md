---
title: "aaaAzure implantação de aplicativos do Service Fabric | Microsoft Docs"
description: "Use Olá toodeploy FabricClient APIs e remover aplicativos na malha do serviço."
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
ms.openlocfilehash: b2986b71c461f3e785ba16ec1b827fe47ad852fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-fabricclient"></a><span data-ttu-id="9efe8-103">Implantar e remover aplicativos usando FabricClient</span><span class="sxs-lookup"><span data-stu-id="9efe8-103">Deploy and remove applications using FabricClient</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9efe8-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9efe8-104">PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
> * [<span data-ttu-id="9efe8-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9efe8-105">Visual Studio</span></span>](service-fabric-publish-app-remote-cluster.md)
> * [<span data-ttu-id="9efe8-106">APIs de FabricClient</span><span class="sxs-lookup"><span data-stu-id="9efe8-106">FabricClient APIs</span></span>](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

<span data-ttu-id="9efe8-107">Assim que um [tipo de aplicativo for empacotado][10], ele está pronto para implantação em um cluster do Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9efe8-107">Once an [application type has been packaged][10], it's ready for deployment into an Azure Service Fabric cluster.</span></span> <span data-ttu-id="9efe8-108">Implantação envolve Olá três etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9efe8-108">Deployment involves hello following three steps:</span></span>

1. <span data-ttu-id="9efe8-109">Carregar o repositório de imagens toohello do pacote de aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="9efe8-109">Upload hello application package toohello image store</span></span>
2. <span data-ttu-id="9efe8-110">Registrar o tipo de aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="9efe8-110">Register hello application type</span></span>
3. <span data-ttu-id="9efe8-111">Criar instância de aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="9efe8-111">Create hello application instance</span></span>

<span data-ttu-id="9efe8-112">Depois que um aplicativo é implantado e uma instância está em execução no cluster hello, você pode excluir a instância do aplicativo hello e seu tipo de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9efe8-112">After an application is deployed and an instance is running in hello cluster, you can delete hello application instance and its application type.</span></span> <span data-ttu-id="9efe8-113">toocompletely remover um aplicativo de cluster Olá envolve Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9efe8-113">toocompletely remove an application from hello cluster involves hello following steps:</span></span>

1. <span data-ttu-id="9efe8-114">Remover (ou excluir) Olá executando a instância do aplicativo</span><span class="sxs-lookup"><span data-stu-id="9efe8-114">Remove (or delete) hello running application instance</span></span>
2. <span data-ttu-id="9efe8-115">Cancelar o registro do tipo de aplicativo hello se você não precisar mais dela</span><span class="sxs-lookup"><span data-stu-id="9efe8-115">Unregister hello application type if you no longer need it</span></span>
3. <span data-ttu-id="9efe8-116">Remover o pacote de aplicativo hello saudação do repositório de imagens</span><span class="sxs-lookup"><span data-stu-id="9efe8-116">Remove hello application package from hello image store</span></span>

<span data-ttu-id="9efe8-117">Se você usar [Visual Studio para implantar e depurar aplicativos](service-fabric-publish-app-remote-cluster.md) no cluster de desenvolvimento local, todos os Olá etapas anteriores são tratadas automaticamente por meio de um script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9efe8-117">If you use [Visual Studio for deploying and debugging applications](service-fabric-publish-app-remote-cluster.md) on your local development cluster, all hello preceding steps are handled automatically through a PowerShell script.</span></span>  <span data-ttu-id="9efe8-118">Esse script é encontrado no hello *Scripts* pasta do projeto de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="9efe8-118">This script is found in hello *Scripts* folder of hello application project.</span></span> <span data-ttu-id="9efe8-119">Este artigo fornece informações detalhadas sobre o que esse script está fazendo para que você possa executar Olá mesmas operações fora do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9efe8-119">This article provides background on what that script is doing so that you can perform hello same operations outside of Visual Studio.</span></span> 
 
## <a name="connect-toohello-cluster"></a><span data-ttu-id="9efe8-120">Conecte-se o cluster toohello</span><span class="sxs-lookup"><span data-stu-id="9efe8-120">Connect toohello cluster</span></span>
<span data-ttu-id="9efe8-121">Conecte-se o cluster toohello criando um [FabricClient](/dotnet/api/system.fabric.fabricclient) instância antes de executar qualquer uma das Olá exemplos de código neste artigo.</span><span class="sxs-lookup"><span data-stu-id="9efe8-121">Connect toohello cluster by creating a [FabricClient](/dotnet/api/system.fabric.fabricclient) instance before you run any of hello code examples in this article.</span></span> <span data-ttu-id="9efe8-122">Para obter exemplos de cluster de desenvolvimento local tooa conexão ou um cluster remoto ou o cluster protegido usando o Active Directory do Azure, X509 certificados ou consulte Active Directory do Windows [conectar tooa segura cluster](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis).</span><span class="sxs-lookup"><span data-stu-id="9efe8-122">For examples of connecting tooa local development cluster or a remote cluster or cluster secured using Azure Active Directory, X509 certificates, or Windows Active Directory see [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md#connect-to-a-cluster-using-the-fabricclient-apis).</span></span> <span data-ttu-id="9efe8-123">cluster de desenvolvimento local em toohello tooconnect, execute Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="9efe8-123">tooconnect toohello local development cluster, run hello following:</span></span>

```csharp
// Connect toohello local cluster.
FabricClient fabricClient = new FabricClient();
```

## <a name="upload-hello-application-package"></a><span data-ttu-id="9efe8-124">Carregar pacote de aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="9efe8-124">Upload hello application package</span></span>
<span data-ttu-id="9efe8-125">Suponha que você crie e empacote um aplicativo chamado *MyApplication* no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9efe8-125">Suppose you build and package an application named *MyApplication* in Visual Studio.</span></span> <span data-ttu-id="9efe8-126">Por padrão, o nome do tipo de aplicativo hello listado no hello ApplicationManifest.xml é "MyApplicationType".</span><span class="sxs-lookup"><span data-stu-id="9efe8-126">By default, hello application type name listed in hello ApplicationManifest.xml is "MyApplicationType".</span></span>  <span data-ttu-id="9efe8-127">Olá pacote de aplicativo, que contém o manifesto de aplicativo necessário hello, manifestos do serviço e pacotes de dados/de configuração de código, está localizado em *C:\Users\&lt; nome de usuário&gt;\Documents\Visual 2017\Projects\ Studio MyApplication\MyApplication\pkg\Debug*.</span><span class="sxs-lookup"><span data-stu-id="9efe8-127">hello application package, which contains hello necessary application manifest, service manifests, and code/config/data packages, is located in *C:\Users\&lt;username&gt;\Documents\Visual Studio 2017\Projects\MyApplication\MyApplication\pkg\Debug*.</span></span>

<span data-ttu-id="9efe8-128">Carregar pacote de aplicativo hello coloca em um local que seja acessível pelos componentes do hello internos do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9efe8-128">Uploading hello application package puts it in a location that's accessible by hello internal Service Fabric components.</span></span> <span data-ttu-id="9efe8-129">Serviço de malha verifica o pacote de aplicativo hello durante o registro de saudação do pacote de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="9efe8-129">Service Fabric verifies hello application package during hello registration of hello application package.</span></span> <span data-ttu-id="9efe8-130">No entanto, se você quiser tooverify Olá pacote do aplicativo localmente (ou seja, antes de carregar), use Olá [ServiceFabricApplicationPackage teste](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9efe8-130">However, if you want tooverify hello application package locally (i.e., before uploading), use hello [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="9efe8-131">Olá [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API carrega o repositório de imagens do hello aplicativo pacote toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="9efe8-131">hello [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API uploads hello application package toohello cluster image store.</span></span> 

<span data-ttu-id="9efe8-132">Se o pacote de aplicativo hello é grande e/ou tem muitos arquivos, você pode [compactá-los](service-fabric-package-apps.md#compress-a-package) e copie-o repositório de imagens toohello usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9efe8-132">If hello application package is large and/or has many files, you can [compress it](service-fabric-package-apps.md#compress-a-package) and copy it toohello image store using PowerShell.</span></span> <span data-ttu-id="9efe8-133">compactação de saudação reduz o tamanho de saudação e número de saudação de arquivos.</span><span class="sxs-lookup"><span data-stu-id="9efe8-133">hello compression reduces hello size and hello number of files.</span></span>

<span data-ttu-id="9efe8-134">Consulte [entender a cadeia de conexão de repositório de imagens Olá](service-fabric-image-store-connection-string.md) para obter mais informações sobre repositório de imagens hello e imagem armazenam a cadeia de caracteres de conexão.</span><span class="sxs-lookup"><span data-stu-id="9efe8-134">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

## <a name="register-hello-application-package"></a><span data-ttu-id="9efe8-135">Registrar pacote de aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="9efe8-135">Register hello application package</span></span>
<span data-ttu-id="9efe8-136">tipo de aplicativo Hello e versão declarados no manifesto de aplicativo hello ficam disponível para uso quando o pacote de aplicativo hello está registrado.</span><span class="sxs-lookup"><span data-stu-id="9efe8-136">hello application type and version declared in hello application manifest become available for use when hello application package is registered.</span></span> <span data-ttu-id="9efe8-137">sistema Olá lê o pacote de saudação carregado na etapa anterior Olá, verifica o pacote de saudação, processa o conteúdo do pacote hello e copia o local do hello processado pacote tooan interno do sistema.</span><span class="sxs-lookup"><span data-stu-id="9efe8-137">hello system reads hello package uploaded in hello previous step, verifies hello package, processes hello package contents, and copies hello processed package tooan internal system location.</span></span>  

<span data-ttu-id="9efe8-138">Olá [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API registra Olá tipo de aplicativo no cluster hello e disponibilizá-lo para implantação.</span><span class="sxs-lookup"><span data-stu-id="9efe8-138">hello [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API registers hello application type in hello cluster and make it available for deployment.</span></span>

<span data-ttu-id="9efe8-139">Olá [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) API fornece informações sobre todos os tipos de aplicativo registrado com êxito.</span><span class="sxs-lookup"><span data-stu-id="9efe8-139">hello [GetApplicationTypeListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationtypelistasync) API provides information about all successfully registered application types.</span></span> <span data-ttu-id="9efe8-140">Você pode usar essa API toodetermine quando é feito registro hello.</span><span class="sxs-lookup"><span data-stu-id="9efe8-140">You can use this API toodetermine when hello registration is done.</span></span>

## <a name="create-an-application-instance"></a><span data-ttu-id="9efe8-141">Criar uma instância do aplicativo</span><span class="sxs-lookup"><span data-stu-id="9efe8-141">Create an application instance</span></span>
<span data-ttu-id="9efe8-142">Você pode instanciar um aplicativo de qualquer tipo de aplicativo que foi registrado com êxito usando Olá [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) API.</span><span class="sxs-lookup"><span data-stu-id="9efe8-142">You can instantiate an application from any application type that has been registered successfully by using hello [CreateApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.createapplicationasync) API.</span></span> <span data-ttu-id="9efe8-143">nome de saudação de cada aplicativo deve começar com hello *"fabric:"* esquema e deve ser exclusivo para cada instância do aplicativo (dentro de um cluster).</span><span class="sxs-lookup"><span data-stu-id="9efe8-143">hello name of each application must start with hello *"fabric:"* scheme and must be unique for each application instance (within a cluster).</span></span> <span data-ttu-id="9efe8-144">Todos os serviços padrão definidos no manifesto de aplicativo de saudação do tipo de aplicativo de destino Olá também são criados.</span><span class="sxs-lookup"><span data-stu-id="9efe8-144">Any default services defined in hello application manifest of hello target application type are also created.</span></span>

<span data-ttu-id="9efe8-145">Várias instâncias do aplicativo podem ser criadas para qualquer determinada versão de um tipo de aplicativo registrado.</span><span class="sxs-lookup"><span data-stu-id="9efe8-145">Multiple application instances can be created for any given version of a registered application type.</span></span> <span data-ttu-id="9efe8-146">Cada instância do aplicativo é executada isoladamente, com seu próprio diretório de trabalho e conjunto de processos.</span><span class="sxs-lookup"><span data-stu-id="9efe8-146">Each application instance runs in isolation, with its own working directory and set of processes.</span></span>

<span data-ttu-id="9efe8-147">toosee chamado aplicativos e serviços estão em execução no cluster hello, executar Olá [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) e [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) APIs.</span><span class="sxs-lookup"><span data-stu-id="9efe8-147">toosee which named applications and services are running in hello cluster, run hello [GetApplicationListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync) and [GetServiceListAsync](/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync) APIs.</span></span>

## <a name="create-a-service-instance"></a><span data-ttu-id="9efe8-148">Crie uma instância de serviço</span><span class="sxs-lookup"><span data-stu-id="9efe8-148">Create a service instance</span></span>
<span data-ttu-id="9efe8-149">Você pode instanciar um serviço de um tipo de serviço usando Olá [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API.</span><span class="sxs-lookup"><span data-stu-id="9efe8-149">You can instantiate a service from a service type using hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API.</span></span>  <span data-ttu-id="9efe8-150">Se o serviço de saudação é declarado como um serviço padrão no manifesto de aplicativo hello, serviço Olá é instanciado quando o aplicativo hello é instanciado.</span><span class="sxs-lookup"><span data-stu-id="9efe8-150">If hello service is declared as a default service in hello application manifest, hello service is instantiated when hello application is instantiated.</span></span>  <span data-ttu-id="9efe8-151">Olá chamada [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API para um serviço que já é instanciado retornará uma exceção do tipo FabricException que contém um código de erro com um valor de FabricErrorCode.ServiceAlreadyExists.</span><span class="sxs-lookup"><span data-stu-id="9efe8-151">Calling hello [CreateServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) API for a service that is already instantiated will return an exception of type FabricException containing an error code with a value of FabricErrorCode.ServiceAlreadyExists.</span></span>

## <a name="remove-a-service-instance"></a><span data-ttu-id="9efe8-152">Remover uma instância de serviço</span><span class="sxs-lookup"><span data-stu-id="9efe8-152">Remove a service instance</span></span>
<span data-ttu-id="9efe8-153">Quando uma instância de serviço não for mais necessário, você poderá removê-lo da saudação executando a instância do aplicativo por chamada hello [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) API.</span><span class="sxs-lookup"><span data-stu-id="9efe8-153">When a service instance is no longer needed, you can remove it from hello running application instance by calling hello [DeleteServiceAsync](/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync) API.</span></span>  

> [!WARNING]
> <span data-ttu-id="9efe8-154">Essa operação não pode ser revertida e o estado do serviço não pode ser recuperado.</span><span class="sxs-lookup"><span data-stu-id="9efe8-154">This operation cannot be reversed, and service state cannot be recovered.</span></span>

## <a name="remove-an-application-instance"></a><span data-ttu-id="9efe8-155">Remover uma instância do aplicativo</span><span class="sxs-lookup"><span data-stu-id="9efe8-155">Remove an application instance</span></span>
<span data-ttu-id="9efe8-156">Quando uma instância de aplicativo não for mais necessário, você poderá removê-lo permanentemente por nome usando Olá [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) API.</span><span class="sxs-lookup"><span data-stu-id="9efe8-156">When an application instance is no longer needed, you can permanently remove it by name using hello [DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) API.</span></span> <span data-ttu-id="9efe8-157">[DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) remove automaticamente todos os serviços que pertencem a aplicativo toohello bem, permanentemente, removendo todos os estados de serviço.</span><span class="sxs-lookup"><span data-stu-id="9efe8-157">[DeleteApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.deleteapplicationasync) automatically removes all services that belong toohello application as well, permanently removing all service state.</span></span>

> [!WARNING]
> <span data-ttu-id="9efe8-158">Essa operação não pode ser revertida e o estado do aplicativo não pode ser recuperado.</span><span class="sxs-lookup"><span data-stu-id="9efe8-158">This operation cannot be reversed, and application state cannot be recovered.</span></span>

## <a name="unregister-an-application-type"></a><span data-ttu-id="9efe8-159">Cancelar o registro de um tipo de aplicativo</span><span class="sxs-lookup"><span data-stu-id="9efe8-159">Unregister an application type</span></span>
<span data-ttu-id="9efe8-160">Quando uma versão específica de um tipo de aplicativo não for mais necessário, você deve cancelar o registro dessa versão específica do tipo de aplicativo hello usando Olá [Unregister-ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) API.</span><span class="sxs-lookup"><span data-stu-id="9efe8-160">When a particular version of an application type is no longer needed, you should unregister that particular version of hello application type using hello [Unregister-ServiceFabricApplicationType](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.unprovisionapplicationasync) API.</span></span> <span data-ttu-id="9efe8-161">Versões não utilizadas ao cancelar o registro aplicativo tipos versões de espaço de armazenamento usado pelo repositório de imagens de saudação.</span><span class="sxs-lookup"><span data-stu-id="9efe8-161">Unregistering unused versions of application types releases storage space used by hello image store.</span></span> <span data-ttu-id="9efe8-162">Uma versão de um tipo de aplicativo pode ser cancelada, desde que nenhum aplicativo é instanciado em relação a essa versão do tipo de aplicativo hello e nenhuma atualização de aplicativo está fazendo referência a essa versão do tipo de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="9efe8-162">A version of an application type can be unregistered as long as no applications are instantiated against that version of hello application type and no pending application upgrades are referencing that version of hello application type.</span></span>

## <a name="remove-an-application-package-from-hello-image-store"></a><span data-ttu-id="9efe8-163">Remover um pacote de aplicativo hello do repositório de imagens</span><span class="sxs-lookup"><span data-stu-id="9efe8-163">Remove an application package from hello image store</span></span>
<span data-ttu-id="9efe8-164">Quando um pacote de aplicativo não for mais necessário, você poderá excluí-la da saudação imagem repositório toofree recursos do sistema usando Olá [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) API.</span><span class="sxs-lookup"><span data-stu-id="9efe8-164">When an application package is no longer needed, you can delete it from hello image store toofree up system resources using hello [RemoveApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.removeapplicationpackage) API.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="9efe8-165">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="9efe8-165">Troubleshooting</span></span>
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a><span data-ttu-id="9efe8-166">Copy-ServiceFabricApplicationPackage solicita um ImageStoreConnectionString</span><span class="sxs-lookup"><span data-stu-id="9efe8-166">Copy-ServiceFabricApplicationPackage asks for an ImageStoreConnectionString</span></span>
<span data-ttu-id="9efe8-167">ambiente de SDK do Service Fabric Olá já deve ter Olá correto padrões configurar.</span><span class="sxs-lookup"><span data-stu-id="9efe8-167">hello Service Fabric SDK environment should already have hello correct defaults set up.</span></span> <span data-ttu-id="9efe8-168">Mas se necessário, Olá ImageStoreConnectionString para todos os comandos deve coincidir valor Olá que Olá malha do serviço de cluster está usando.</span><span class="sxs-lookup"><span data-stu-id="9efe8-168">But if needed, hello ImageStoreConnectionString for all commands should match hello value that hello Service Fabric cluster is using.</span></span> <span data-ttu-id="9efe8-169">Você pode encontrar hello ImageStoreConnectionString no manifesto do cluster hello, recuperadas usando Olá [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) e comandos Get-ImageStoreConnectionStringFromClusterManifest:</span><span class="sxs-lookup"><span data-stu-id="9efe8-169">You can find hello ImageStoreConnectionString in hello cluster manifest, retrieved using hello [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) and Get-ImageStoreConnectionStringFromClusterManifest commands:</span></span>

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

<span data-ttu-id="9efe8-170">Olá **ImageStoreConnectionStringFromClusterManifest Get** cmdlet, que é parte do módulo do PowerShell do SDK do Service Fabric Olá, é a imagem de saudação do tooget usado armazenar a cadeia de caracteres de conexão.</span><span class="sxs-lookup"><span data-stu-id="9efe8-170">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="9efe8-171">módulo SDK em Olá tooimport, execute:</span><span class="sxs-lookup"><span data-stu-id="9efe8-171">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```


<span data-ttu-id="9efe8-172">Olá ImageStoreConnectionString foi encontrado no manifesto do cluster hello:</span><span class="sxs-lookup"><span data-stu-id="9efe8-172">hello ImageStoreConnectionString is found in hello cluster manifest:</span></span>

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

<span data-ttu-id="9efe8-173">Consulte [entender a cadeia de conexão de repositório de imagens Olá](service-fabric-image-store-connection-string.md) para obter mais informações sobre repositório de imagens hello e imagem armazenam a cadeia de caracteres de conexão.</span><span class="sxs-lookup"><span data-stu-id="9efe8-173">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

### <a name="deploy-large-application-package"></a><span data-ttu-id="9efe8-174">Implantar um pacote de aplicativos grande</span><span class="sxs-lookup"><span data-stu-id="9efe8-174">Deploy large application package</span></span>
<span data-ttu-id="9efe8-175">Problema: a API [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) atinge o tempo limite para um pacote de aplicativos grande (na ordem de GB).</span><span class="sxs-lookup"><span data-stu-id="9efe8-175">Issue: [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) API times out for a large application package (order of GB).</span></span>
<span data-ttu-id="9efe8-176">Experimente:</span><span class="sxs-lookup"><span data-stu-id="9efe8-176">Try:</span></span>
- <span data-ttu-id="9efe8-177">Especificar um tempo limite maior para o método [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) com o parâmetro `timeout`.</span><span class="sxs-lookup"><span data-stu-id="9efe8-177">Specify a larger timeout for [CopyApplicationPackage](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.copyapplicationpackage) method, with `timeout` parameter.</span></span> <span data-ttu-id="9efe8-178">Por padrão, o tempo limite de saudação é 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="9efe8-178">By default, hello timeout is 30 minutes.</span></span>
- <span data-ttu-id="9efe8-179">Verifique a conexão de rede de saudação entre o computador de origem e o cluster.</span><span class="sxs-lookup"><span data-stu-id="9efe8-179">Check hello network connection between your source machine and cluster.</span></span> <span data-ttu-id="9efe8-180">Se a conexão de saudação estiver lenta, considere o uso de uma máquina com uma conexão de rede melhor.</span><span class="sxs-lookup"><span data-stu-id="9efe8-180">If hello connection is slow, consider using a machine with a better network connection.</span></span>
<span data-ttu-id="9efe8-181">Se máquina do cliente Olá for em outra região de cluster hello, considere usando um computador cliente em uma região mais próxima ou mesmo como cluster hello.</span><span class="sxs-lookup"><span data-stu-id="9efe8-181">If hello client machine is in another region than hello cluster, consider using a client machine in a closer or same region as hello cluster.</span></span>
- <span data-ttu-id="9efe8-182">Verifique se você está sofrendo limitação externa.</span><span class="sxs-lookup"><span data-stu-id="9efe8-182">Check if you are hitting external throttling.</span></span> <span data-ttu-id="9efe8-183">Por exemplo, quando o repositório de imagens Olá é armazenamento toouse configurada do azure, carregamento pode ser limitado.</span><span class="sxs-lookup"><span data-stu-id="9efe8-183">For example, when hello image store is configured toouse azure storage, upload may be throttled.</span></span>

<span data-ttu-id="9efe8-184">Problema: o upload do pacote foi concluído com êxito, mas a API [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) atinge o tempo limite. Experimente:</span><span class="sxs-lookup"><span data-stu-id="9efe8-184">Issue: Upload package completed successfully, but [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API times out. Try:</span></span>
- <span data-ttu-id="9efe8-185">[Compactar pacote hello](service-fabric-package-apps.md#compress-a-package) antes de copiar toohello repositório de imagens.</span><span class="sxs-lookup"><span data-stu-id="9efe8-185">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span>
<span data-ttu-id="9efe8-186">compactação Olá reduz o tamanho do hello e Olá vários arquivos, que por sua vez reduz a quantidade de saudação do tráfego e funciona malha esse serviço devem executar.</span><span class="sxs-lookup"><span data-stu-id="9efe8-186">hello compression reduces hello size and hello number of files, which in turn reduces hello amount of traffic and work that Service Fabric must perform.</span></span> <span data-ttu-id="9efe8-187">operação de carregamento de saudação pode ser mais lenta (especialmente se você incluir o tempo de compactação de saudação), mas o tipo de aplicativo hello registrar e cancelar o registro são mais rápidos.</span><span class="sxs-lookup"><span data-stu-id="9efe8-187">hello upload operation may be slower (especially if you include hello compression time), but register and un-register hello application type are faster.</span></span>
- <span data-ttu-id="9efe8-188">Especifique um tempo limite maior para a API [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) com o parâmetro `timeout`.</span><span class="sxs-lookup"><span data-stu-id="9efe8-188">Specify a larger timeout for [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) API with `timeout` parameter.</span></span>

### <a name="deploy-application-package-with-many-files"></a><span data-ttu-id="9efe8-189">Implantar pacote de aplicativos com muitos arquivos</span><span class="sxs-lookup"><span data-stu-id="9efe8-189">Deploy application package with many files</span></span>
<span data-ttu-id="9efe8-190">Problema: [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) atinge o tempo limite para um pacote de aplicativos com muitos arquivos (na ordem de milhares).</span><span class="sxs-lookup"><span data-stu-id="9efe8-190">Issue: [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) times out for an application package with many files (order of thousands).</span></span>
<span data-ttu-id="9efe8-191">Experimente:</span><span class="sxs-lookup"><span data-stu-id="9efe8-191">Try:</span></span>
- <span data-ttu-id="9efe8-192">[Compactar pacote hello](service-fabric-package-apps.md#compress-a-package) antes de copiar toohello repositório de imagens.</span><span class="sxs-lookup"><span data-stu-id="9efe8-192">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span> <span data-ttu-id="9efe8-193">compactação de saudação reduz o número de saudação de arquivos.</span><span class="sxs-lookup"><span data-stu-id="9efe8-193">hello compression reduces hello number of files.</span></span>
- <span data-ttu-id="9efe8-194">Especifique um tempo limite maior para [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) com o parâmetro `timeout`.</span><span class="sxs-lookup"><span data-stu-id="9efe8-194">Specify a larger timeout for [ProvisionApplicationAsync](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient.provisionapplicationasync) with `timeout` parameter.</span></span>

## <a name="code-example"></a><span data-ttu-id="9efe8-195">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="9efe8-195">Code example</span></span>
<span data-ttu-id="9efe8-196">Olá exemplo a seguir copia um repositório de imagens de toohello de pacote de aplicativo, provisiona o tipo de aplicativo hello, cria uma instância de aplicativo, cria uma instância de serviço, remove a instância do aplicativo de hello, cancelar provisiona tipo de aplicativo hello, e Exclui o pacote de aplicativo Olá Olá do repositório de imagens.</span><span class="sxs-lookup"><span data-stu-id="9efe8-196">hello following example copies an application package toohello image store, provisions hello application type, creates an application instance, creates a service instance, removes hello application instance, un-provisions hello application type, and deletes hello application package from hello image store.</span></span>

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

    // Connect toohello cluster.
    FabricClient fabricClient = new FabricClient(clusterConnection);

    // Copy hello application package tooa location in hello image store
    try
    {
        fabricClient.ApplicationManager.CopyApplicationPackage(imageStoreConnectionString, packagePath, packagePathInImageStore);
        Console.WriteLine("Application package copied too{0}", packagePathInImageStore);
    }
    catch (AggregateException ae)
    {
        Console.WriteLine("Application package copy tooImage Store failed: ");
        foreach (Exception ex in ae.InnerExceptions)
        {
            Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
        }
    }

    // Provision hello application.  "MyApplicationV1" is hello folder in hello image store where hello application package is located. 
    // hello application type with name "MyApplicationType" and version "1.0.0" (both are found in hello application manifest) 
    // is now registered in hello cluster.            
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

    //  Create hello application instance.
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

    // Create hello stateless service description.  For stateful services, use a StatefulServiceDescription object.
    StatelessServiceDescription serviceDescription = new StatelessServiceDescription();
    serviceDescription.ApplicationName = new Uri(appName);
    serviceDescription.InstanceCount = 1;
    serviceDescription.PartitionSchemeDescription = new SingletonPartitionSchemeDescription();
    serviceDescription.ServiceName = new Uri(serviceName);
    serviceDescription.ServiceTypeName = serviceType;

    // Create hello service instance.  If hello service is declared as a default service in hello ApplicationManifest.xml,
    // hello service instance is already running and this call will fail.
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

    // Delete an application instance from hello application type.
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

    // Un-provision hello application type.
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

    // Delete hello application package from a location in hello image store.
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

## <a name="next-steps"></a><span data-ttu-id="9efe8-197">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9efe8-197">Next steps</span></span>
[<span data-ttu-id="9efe8-198">Atualização de aplicativos do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9efe8-198">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="9efe8-199">Introdução à integridade da Malha do Serviço</span><span class="sxs-lookup"><span data-stu-id="9efe8-199">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)

[<span data-ttu-id="9efe8-200">Diagnosticar e solucionar problemas de um serviço da Malha do Serviço</span><span class="sxs-lookup"><span data-stu-id="9efe8-200">Diagnose and troubleshoot a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="9efe8-201">Modelar um aplicativo na Malha do Serviço</span><span class="sxs-lookup"><span data-stu-id="9efe8-201">Model an application in Service Fabric</span></span>](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
