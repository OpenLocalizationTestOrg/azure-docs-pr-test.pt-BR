---
title: "Implantação de aplicativos do Azure Service Fabric | Microsoft Docs"
description: Como implantar e remover aplicativos no Service Fabric usando o PowerShell.
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
ms.date: 06/01/2017
ms.author: ryanwi
ms.openlocfilehash: edef23a8cdab7fd0bef54456f0caabb9db273bf9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-and-remove-applications-using-powershell"></a><span data-ttu-id="4ebaa-103">Implantar e remover aplicativos usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="4ebaa-103">Deploy and remove applications using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4ebaa-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4ebaa-104">PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
> * [<span data-ttu-id="4ebaa-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4ebaa-105">Visual Studio</span></span>](service-fabric-publish-app-remote-cluster.md)
> * [<span data-ttu-id="4ebaa-106">APIs de FabricClient</span><span class="sxs-lookup"><span data-stu-id="4ebaa-106">FabricClient APIs</span></span>](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

<span data-ttu-id="4ebaa-107">Assim que um [tipo de aplicativo for empacotado][10], ele está pronto para implantação em um cluster do Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-107">Once an [application type has been packaged][10], it's ready for deployment into an Azure Service Fabric cluster.</span></span> <span data-ttu-id="4ebaa-108">A implantação envolve as três etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ebaa-108">Deployment involves the following three steps:</span></span>

1. <span data-ttu-id="4ebaa-109">Carregar o pacote de aplicativos no repositório de imagens</span><span class="sxs-lookup"><span data-stu-id="4ebaa-109">Upload the application package to the image store</span></span>
2. <span data-ttu-id="4ebaa-110">Registrar o tipo de aplicativo</span><span class="sxs-lookup"><span data-stu-id="4ebaa-110">Register the application type</span></span>
3. <span data-ttu-id="4ebaa-111">Criar a instância do aplicativo</span><span class="sxs-lookup"><span data-stu-id="4ebaa-111">Create the application instance</span></span>

<span data-ttu-id="4ebaa-112">Depois que um aplicativo é implantado e uma instância está em execução no cluster, você pode excluir a instância do aplicativo e o tipo de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-112">After an application is deployed and an instance is running in the cluster, you can delete the application instance and its application type.</span></span> <span data-ttu-id="4ebaa-113">Remover completamente um aplicativo do cluster envolve as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="4ebaa-113">To completely remove an application from the cluster involves the following steps:</span></span>

1. <span data-ttu-id="4ebaa-114">Remover (ou excluir) a execução da instância do aplicativo</span><span class="sxs-lookup"><span data-stu-id="4ebaa-114">Remove (or delete) the running application instance</span></span>
2. <span data-ttu-id="4ebaa-115">Cancelar o registro do tipo de aplicativo se você não precisar mais dele</span><span class="sxs-lookup"><span data-stu-id="4ebaa-115">Unregister the application type if you no longer need it</span></span>
3. <span data-ttu-id="4ebaa-116">Remover o pacote de aplicativos do repositório de imagens</span><span class="sxs-lookup"><span data-stu-id="4ebaa-116">Remove the application package from the image store</span></span>

<span data-ttu-id="4ebaa-117">Se você usar o [Visual Studio para implantar e depurar aplicativos](service-fabric-publish-app-remote-cluster.md) no cluster de desenvolvimento local, todas as etapas anteriores serão tratadas automaticamente por meio de um script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-117">If you use [Visual Studio for deploying and debugging applications](service-fabric-publish-app-remote-cluster.md) on your local development cluster, all the preceding steps are handled automatically through a PowerShell script.</span></span>  <span data-ttu-id="4ebaa-118">Esse script é encontrado na pasta *Scripts* do projeto do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-118">This script is found in the *Scripts* folder of the application project.</span></span> <span data-ttu-id="4ebaa-119">Este artigo fornece informações sobre o que esse script faz para que você possa executar as mesmas operações fora do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-119">This article provides background on what that script is doing so that you can perform the same operations outside of Visual Studio.</span></span> 
 
## <a name="connect-to-the-cluster"></a><span data-ttu-id="4ebaa-120">Conectar-se ao cluster</span><span class="sxs-lookup"><span data-stu-id="4ebaa-120">Connect to the cluster</span></span>
<span data-ttu-id="4ebaa-121">Antes de executar qualquer comando do PowerShell neste artigo, sempre comece usando [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) para se conectar ao cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-121">Before you run any PowerShell commands in this article, always start by using [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) to connect to the Service Fabric cluster.</span></span> <span data-ttu-id="4ebaa-122">Para se conectar ao cluster de desenvolvimento local, execute o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4ebaa-122">To connect to the local development cluster, run the following:</span></span>

```powershell
PS C:\>Connect-ServiceFabricCluster
```

<span data-ttu-id="4ebaa-123">Para obter exemplos de como se conectar a um cluster remoto ou protegido usando o Azure Active Directory, certificados X509 ou Active Directory do Windows, veja [Conectar-se a um cluster seguro](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="4ebaa-123">For examples of connecting to a remote cluster or cluster secured using Azure Active Directory, X509 certificates, or Windows Active Directory see [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

## <a name="upload-the-application-package"></a><span data-ttu-id="4ebaa-124">Carregar o pacote de aplicativos</span><span class="sxs-lookup"><span data-stu-id="4ebaa-124">Upload the application package</span></span>
<span data-ttu-id="4ebaa-125">O carregamento do pacote de aplicativos coloca-o em um local acessível por componentes internos do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-125">Uploading the application package puts it in a location that's accessible by internal Service Fabric components.</span></span>
<span data-ttu-id="4ebaa-126">Se quiser verificar o pacote de aplicativos localmente, use o cmdlet [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="4ebaa-126">If you want to verify the application package locally, use the [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="4ebaa-127">O comando [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) carrega o pacote do aplicativo para o Repositório de Imagens do cluster.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-127">The [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command uploads the application package to the cluster image store.</span></span>
<span data-ttu-id="4ebaa-128">O cmdlet **Get-ImageStoreConnectionStringFromClusterManifest** , que faz parte do módulo do PowerShell do SDK do Service Fabric, é usado para obter a cadeia de conexão do repositório de imagens.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-128">The **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of the Service Fabric SDK PowerShell module, is used to get the image store connection string.</span></span>  <span data-ttu-id="4ebaa-129">Para importar o módulo do SDK, execute:</span><span class="sxs-lookup"><span data-stu-id="4ebaa-129">To import the SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="4ebaa-130">Suponha que você crie e empacote um aplicativo chamado *MyApplication* no Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-130">Suppose you build and package an application named *MyApplication* in Visual Studio 2015.</span></span> <span data-ttu-id="4ebaa-131">Por padrão, o nome do tipo de aplicativo listado no ApplicationManifest.xml é "MyApplicationType".</span><span class="sxs-lookup"><span data-stu-id="4ebaa-131">By default, the application type name listed in the ApplicationManifest.xml is "MyApplicationType".</span></span>  <span data-ttu-id="4ebaa-132">O pacote de aplicativos, que contém o manifesto do aplicativo, os manifestos de serviço e os pacotes de códigos/configurações/dados necessários, está localizado em *C:\Users\\<nome de usuário\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug*.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-132">The application package, which contains the necessary application manifest, service manifests, and code/config/data packages, is located in *C:\Users\<username\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug*.</span></span> 

<span data-ttu-id="4ebaa-133">O comando a seguir lista o conteúdo do pacote de aplicativos:</span><span class="sxs-lookup"><span data-stu-id="4ebaa-133">The following command lists the contents of the application package:</span></span>

```powershell
PS C:\> $path = 'C:\Users\<user\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug'
PS C:\> tree /f $path
Folder PATH listing for volume OSDisk
Volume serial number is 0459-2393
C:\USERS\USER\DOCUMENTS\VISUAL STUDIO 2015\PROJECTS\MYAPPLICATION\MYAPPLICATION\PKG\DEBUG
│   ApplicationManifest.xml
│
└───Stateless1Pkg
    │   ServiceManifest.xml
    │
    ├───Code
    │       Microsoft.ServiceFabric.Data.dll
    │       Microsoft.ServiceFabric.Data.Interfaces.dll
    │       Microsoft.ServiceFabric.Internal.dll
    │       Microsoft.ServiceFabric.Internal.Strings.dll
    │       Microsoft.ServiceFabric.Services.dll
    │       ServiceFabricServiceModel.dll
    │       Stateless1.exe
    │       Stateless1.exe.config
    │       Stateless1.pdb
    │       System.Fabric.dll
    │       System.Fabric.Strings.dll
    │
    └───Config
            Settings.xml
```

<span data-ttu-id="4ebaa-134">Se o pacote de aplicativos for grande e/ou tiver vários arquivos, você poderá [compactá-lo](service-fabric-package-apps.md#compress-a-package).</span><span class="sxs-lookup"><span data-stu-id="4ebaa-134">If the application package is large and/or has many files, you can [compress it](service-fabric-package-apps.md#compress-a-package).</span></span> <span data-ttu-id="4ebaa-135">A compactação reduz o tamanho e o número de arquivos.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-135">The compression reduces the size and the number of files.</span></span>
<span data-ttu-id="4ebaa-136">O efeito colateral é que o registro e o cancelamento do registro do tipo de aplicativo são mais rápidos.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-136">The side effect is that registering and un-registering the application type are faster.</span></span> <span data-ttu-id="4ebaa-137">O tempo de upload poderá ser mais lento atualmente, especialmente se você incluir o tempo usado para compactar o pacote.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-137">Upload time may be slower currently, especially if you include the time to compress the package.</span></span> 

<span data-ttu-id="4ebaa-138">Para compactar um pacote, use o mesmo comando [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="4ebaa-138">To compress a package, use the same [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command.</span></span> <span data-ttu-id="4ebaa-139">A compactação pode ser feita separadamente do upload pelo uso do sinalizador `SkipCopy` ou então junto com a operação de upload.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-139">Compression can be done separate from upload, by using the `SkipCopy` flag, or together with the upload operation.</span></span> <span data-ttu-id="4ebaa-140">Aplicar compactação em um pacote compactado é não operacional.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-140">Applying compression on a compressed package is no-op.</span></span>
<span data-ttu-id="4ebaa-141">Para descompactar um pacote compactado, use o mesmo comando [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) com a opção `UncompressPackage`.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-141">To uncompress a compressed package, use the same [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command with the `UncompressPackage` switch.</span></span>

<span data-ttu-id="4ebaa-142">O cmdlet a seguir compacta o pacote sem copiá-lo para o repositório de imagens.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-142">The following cmdlet compresses the package without copying it to the image store.</span></span> <span data-ttu-id="4ebaa-143">O pacote agora inclui arquivos compactados para os pacotes `Code` e `Config`.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-143">The package now includes zipped files for the `Code` and `Config` packages.</span></span> <span data-ttu-id="4ebaa-144">O aplicativo e os manifestos do serviço não são compactados porque eles são necessários para várias operações internas (como compartilhamento do pacote, extração da versão e nome do tipo de aplicativo para determinadas validações).</span><span class="sxs-lookup"><span data-stu-id="4ebaa-144">The application and the service manifests are not zipped, because they are needed for many internal operations (like package sharing, application type name and version extraction for certain validations).</span></span> <span data-ttu-id="4ebaa-145">Compactar os manifestos tornaria essas operações ineficientes.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-145">Zipping the manifests would make these operations inefficient.</span></span>

```
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -CompressPackage -SkipCopy
PS C:\> tree /f $path
Folder PATH listing for volume OSDisk
Volume serial number is 0459-2393
C:\USERS\USER\DOCUMENTS\VISUAL STUDIO 2015\PROJECTS\MYAPPLICATION\MYAPPLICATION\PKG\DEBUG
|   ApplicationManifest.xml
|
└───Stateless1Pkg
       Code.zip
       Config.zip
       ServiceManifest.xml
```

<span data-ttu-id="4ebaa-146">Para pacotes de aplicativos grandes, a compactação leva tempo.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-146">For large application packages, the compression takes time.</span></span> <span data-ttu-id="4ebaa-147">Para obter melhores resultados, use uma unidade SSD rápida.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-147">For best results, use a fast SSD drive.</span></span> <span data-ttu-id="4ebaa-148">Os tempos de compactação e o tamanho do pacote compactado também diferem com base no conteúdo do pacote.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-148">The compression times and the size of the compressed package also differ based on the package content.</span></span>
<span data-ttu-id="4ebaa-149">Por exemplo, eis aqui as estatísticas de compactação para alguns pacotes, que mostram o tamanho a inicial e o do pacote compactado, com o tempo de compactação.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-149">For example, here is compression statistics for some packages, which show the initial and the compressed package size, with the compression time.</span></span>

|<span data-ttu-id="4ebaa-150">Tamanho inicial (MB)</span><span class="sxs-lookup"><span data-stu-id="4ebaa-150">Initial size (MB)</span></span>|<span data-ttu-id="4ebaa-151">Contagem de arquivos</span><span class="sxs-lookup"><span data-stu-id="4ebaa-151">File count</span></span>|<span data-ttu-id="4ebaa-152">Tempo de compactação</span><span class="sxs-lookup"><span data-stu-id="4ebaa-152">Compression Time</span></span>|<span data-ttu-id="4ebaa-153">Tamanho do pacote compactado (MB)</span><span class="sxs-lookup"><span data-stu-id="4ebaa-153">Compressed package size (MB)</span></span>|
|----------------:|---------:|---------------:|---------------------------:|
|<span data-ttu-id="4ebaa-154">100</span><span class="sxs-lookup"><span data-stu-id="4ebaa-154">100</span></span>|<span data-ttu-id="4ebaa-155">100</span><span class="sxs-lookup"><span data-stu-id="4ebaa-155">100</span></span>|<span data-ttu-id="4ebaa-156">00:00:03.3547592</span><span class="sxs-lookup"><span data-stu-id="4ebaa-156">00:00:03.3547592</span></span>|<span data-ttu-id="4ebaa-157">60</span><span class="sxs-lookup"><span data-stu-id="4ebaa-157">60</span></span>|
|<span data-ttu-id="4ebaa-158">512</span><span class="sxs-lookup"><span data-stu-id="4ebaa-158">512</span></span>|<span data-ttu-id="4ebaa-159">100</span><span class="sxs-lookup"><span data-stu-id="4ebaa-159">100</span></span>|<span data-ttu-id="4ebaa-160">00:00:16.3850303</span><span class="sxs-lookup"><span data-stu-id="4ebaa-160">00:00:16.3850303</span></span>|<span data-ttu-id="4ebaa-161">307</span><span class="sxs-lookup"><span data-stu-id="4ebaa-161">307</span></span>|
|<span data-ttu-id="4ebaa-162">1.024</span><span class="sxs-lookup"><span data-stu-id="4ebaa-162">1024</span></span>|<span data-ttu-id="4ebaa-163">500</span><span class="sxs-lookup"><span data-stu-id="4ebaa-163">500</span></span>|<span data-ttu-id="4ebaa-164">00:00:32.5907950</span><span class="sxs-lookup"><span data-stu-id="4ebaa-164">00:00:32.5907950</span></span>|<span data-ttu-id="4ebaa-165">615</span><span class="sxs-lookup"><span data-stu-id="4ebaa-165">615</span></span>|
|<span data-ttu-id="4ebaa-166">2.048</span><span class="sxs-lookup"><span data-stu-id="4ebaa-166">2048</span></span>|<span data-ttu-id="4ebaa-167">1000</span><span class="sxs-lookup"><span data-stu-id="4ebaa-167">1000</span></span>|<span data-ttu-id="4ebaa-168">00:01:04.3775554</span><span class="sxs-lookup"><span data-stu-id="4ebaa-168">00:01:04.3775554</span></span>|<span data-ttu-id="4ebaa-169">1231</span><span class="sxs-lookup"><span data-stu-id="4ebaa-169">1231</span></span>|
|<span data-ttu-id="4ebaa-170">5012</span><span class="sxs-lookup"><span data-stu-id="4ebaa-170">5012</span></span>|<span data-ttu-id="4ebaa-171">100</span><span class="sxs-lookup"><span data-stu-id="4ebaa-171">100</span></span>|<span data-ttu-id="4ebaa-172">00:02:45.2951288</span><span class="sxs-lookup"><span data-stu-id="4ebaa-172">00:02:45.2951288</span></span>|<span data-ttu-id="4ebaa-173">3074</span><span class="sxs-lookup"><span data-stu-id="4ebaa-173">3074</span></span>|

<span data-ttu-id="4ebaa-174">Depois que um pacote é compactado, ele pode ser carregado para um ou vários clusters do Service Fabric conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-174">Once a package is compressed, it can be uploaded to one or multiple Service Fabric clusters as needed.</span></span> <span data-ttu-id="4ebaa-175">O mecanismo de implantação é o mesmo para pacotes compactados e não compactados.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-175">The deployment mechanism is same for compressed and uncompressed packages.</span></span> <span data-ttu-id="4ebaa-176">Se o pacote for compactado ele será armazenado como tal no repositório de imagens do cluster e será descompactado no nó antes que o aplicativo seja executado.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-176">If the package is compressed, it is stored as such in the cluster image store and it's uncompressed on the node before the application is run.</span></span>


<span data-ttu-id="4ebaa-177">O exemplo a seguir carrega o pacote para o armazenamento de imagens em uma pasta chamada "MyApplicationV1":</span><span class="sxs-lookup"><span data-stu-id="4ebaa-177">The following example uploads the package to the image store, into a folder named "MyApplicationV1":</span></span>

```powershell
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)) -TimeoutSec 1800
```

<span data-ttu-id="4ebaa-178">O cmdlet **Get-ImageStoreConnectionStringFromClusterManifest** , que faz parte do módulo do PowerShell do SDK do Service Fabric, é usado para obter a cadeia de conexão do repositório de imagens.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-178">The **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of the Service Fabric SDK PowerShell module, is used to get the image store connection string.</span></span>  <span data-ttu-id="4ebaa-179">Para importar o módulo do SDK, execute:</span><span class="sxs-lookup"><span data-stu-id="4ebaa-179">To import the SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="4ebaa-180">Se você não especificar o parâmetro *-ApplicationPackagePathInImageStore*, o pacote de aplicativos será copiado para a pasta "Debug" no repositório de imagens.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-180">If you do not specify the *-ApplicationPackagePathInImageStore* parameter, the application package is copied into the "Debug" folder in the image store.</span></span>

<span data-ttu-id="4ebaa-181">O tempo necessário que leva para carregar um pacote difere, dependendo de vários fatores.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-181">The time it takes to upload a package differs depending on multiple factors.</span></span> <span data-ttu-id="4ebaa-182">Alguns desses fatores são o número de arquivos no pacote, o tamanho do pacote e os tamanhos dos arquivos.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-182">Some of these factors are the number of files in the package, the package size, and the file sizes.</span></span> <span data-ttu-id="4ebaa-183">A velocidade da rede entre o computador de origem e o cluster do Service Fabric também afeta o tempo de upload.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-183">The network speed between the source machine and the Service Fabric cluster also impacts the upload time.</span></span> <span data-ttu-id="4ebaa-184">O tempo limite padrão para [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) é de 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-184">The default timeout for [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) is 30 minutes.</span></span>
<span data-ttu-id="4ebaa-185">Dependendo dos fatores descritos, talvez você precise aumentar o tempo limite.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-185">Depending on the described factors, you may have to increase the timeout.</span></span> <span data-ttu-id="4ebaa-186">Se você estiver compactando o pacote na chamada de cópia, você também precisará considerar o tempo de compactação.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-186">If you are compressing the package in the copy call, you need to also consider the compression time.</span></span>

<span data-ttu-id="4ebaa-187">Confira [Noções básicas sobre a configuração ImageStoreConnectionString](service-fabric-image-store-connection-string.md) para obter informações suplementares sobre o repositório de imagens e a cadeia de conexão de armazenamento de imagens.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-187">See [Understand the image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about the image store and image store connection string.</span></span>

## <a name="register-the-application-package"></a><span data-ttu-id="4ebaa-188">Registrar o pacote de aplicativos</span><span class="sxs-lookup"><span data-stu-id="4ebaa-188">Register the application package</span></span>
<span data-ttu-id="4ebaa-189">O tipo e a versão do aplicativo declarados no manifesto do aplicativo tornam-se disponíveis para uso quando o pacote de aplicativos é registrado.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-189">The application type and version declared in the application manifest become available for use when the application package is registered.</span></span> <span data-ttu-id="4ebaa-190">O sistema lê o pacote carregado na etapa anterior, verifica o pacote, processa o conteúdo do pacote e copia o pacote processado em um local interno do sistema.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-190">The system reads the package uploaded in the previous step, verifies the package, processes the package contents, and copies the processed package to an internal system location.</span></span>  

<span data-ttu-id="4ebaa-191">Execute o cmdlet [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) para registrar o tipo de aplicativo no cluster e disponibilizá-lo para implantação:</span><span class="sxs-lookup"><span data-stu-id="4ebaa-191">Run the [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet to register the application type in the cluster and make it available for deployment:</span></span>

```powershell
PS C:\> Register-ServiceFabricApplicationType MyApplicationV1
Register application type succeeded
```

<span data-ttu-id="4ebaa-192">"MyApplicationV1" é a pasta no repositório de imagens em que o pacote de aplicativos se encontra.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-192">"MyApplicationV1" is the folder in the image store where the application package is located.</span></span> <span data-ttu-id="4ebaa-193">O tipo de aplicativo com o nome "MyApplicationType" e a versão "1.0.0" (ambos são encontradas no manifesto do aplicativo) agora é registrado no cluster.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-193">The application type with name "MyApplicationType" and version "1.0.0" (both are found in the application manifest) is now registered in the cluster.</span></span>

<span data-ttu-id="4ebaa-194">O comando [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) retornará somente depois que o sistema tiver registrado com êxito o pacote de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-194">The [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) command returns only after the system has successfully registered the application package.</span></span> <span data-ttu-id="4ebaa-195">O tempo que se leva para o registro depende do tamanho e do conteúdo do pacote de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-195">How long registration takes depends on the size and contents of the application package.</span></span> <span data-ttu-id="4ebaa-196">O parâmetro **-TimeoutSec** pode ser usado para fornecer um tempo limite maior, se necessário (o tempo limite padrão é 60 segundos).</span><span class="sxs-lookup"><span data-stu-id="4ebaa-196">If needed, the **-TimeoutSec** parameter can be used to supply a longer timeout (the default timeout is 60 seconds).</span></span>

<span data-ttu-id="4ebaa-197">Se você tiver um pacote de aplicativos grande ou estiver experienciando tempos limite sendo atingidos, use o parâmetro **-Async**.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-197">If you have a large application package or if you are experiencing timeouts, use the **-Async** parameter.</span></span> <span data-ttu-id="4ebaa-198">O comando retorna quando o cluster aceita o comando de registro e o processamento continua conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-198">The command returns when the cluster accepts the register command, and the processing continues as needed.</span></span>
<span data-ttu-id="4ebaa-199">O comando [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) lista todas as versões do tipo de aplicativo registradas com êxito e seu status de registro.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-199">The [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="4ebaa-200">Você pode usar esse comando para determinar quando o registro é feito.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-200">You can use this command to determine when the registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="create-the-application"></a><span data-ttu-id="4ebaa-201">Criar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="4ebaa-201">Create the application</span></span>
<span data-ttu-id="4ebaa-202">É possível instanciar um aplicativo de qualquer versão do tipo de aplicativo registrada com êxito usando o cmdlet [New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="4ebaa-202">You can instantiate an application from any application type version that has been registered successfully by using the [New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="4ebaa-203">O nome de cada aplicativo deve começar com o esquema *"fabric:"* e ser exclusivo para cada instância do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-203">The name of each application must start with the *"fabric:"* scheme and must be unique for each application instance.</span></span> <span data-ttu-id="4ebaa-204">Quaisquer serviços padrão definidos no manifesto do aplicativo do tipo de aplicativo de destino também são criados.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-204">Any default services defined in the application manifest of the target application type are also created.</span></span>

```powershell
PS C:\> New-ServiceFabricApplication fabric:/MyApp MyApplicationType 1.0.0

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationParameters  : {}
```
<span data-ttu-id="4ebaa-205">Várias instâncias do aplicativo podem ser criadas para qualquer determinada versão de um tipo de aplicativo registrado.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-205">Multiple application instances can be created for any given version of a registered application type.</span></span> <span data-ttu-id="4ebaa-206">Cada instância do aplicativo é executada isoladamente, com seu próprio processo e diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-206">Each application instance runs in isolation, with its own work directory and process.</span></span>

<span data-ttu-id="4ebaa-207">Para ver quais apps e serviços nomeados estão em execução no cluster, execute os cmdlets [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) e [Get-ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps):</span><span class="sxs-lookup"><span data-stu-id="4ebaa-207">To see which named apps and services are running in the cluster, run the [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) and [Get-ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) cmdlets:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplication  

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Ok
ApplicationParameters  : {}

PS C:\> Get-ServiceFabricApplication | Get-ServiceFabricService

ServiceName            : fabric:/MyApp/Stateless1
ServiceKind            : Stateless
ServiceTypeName        : Stateless1Type
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
ServiceStatus          : Active
HealthState            : Ok
```

## <a name="remove-an-application"></a><span data-ttu-id="4ebaa-208">Remover um aplicativo</span><span class="sxs-lookup"><span data-stu-id="4ebaa-208">Remove an application</span></span>
<span data-ttu-id="4ebaa-209">Quando uma instância de aplicativo não é mais necessária, você pode removê-la permanentemente pelo nome usando o cmdlet [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="4ebaa-209">When an application instance is no longer needed, you can permanently remove it by name using the [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="4ebaa-210">[Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) também remove automaticamente todos os serviços que pertencem ao aplicativo, removendo permanentemente todos os estados de serviço.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-210">[Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) automatically removes all services that belong to the application as well, permanently removing all service state.</span></span> 

> [!WARNING]
> <span data-ttu-id="4ebaa-211">Essa operação não pode ser revertida e o estado do aplicativo não pode ser recuperado.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-211">This operation cannot be reversed, and application state cannot be recovered.</span></span>

```powershell
PS C:\> Remove-ServiceFabricApplication fabric:/MyApp

Confirm
Continue with this operation?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):
Remove application instance succeeded

PS C:\> Get-ServiceFabricApplication
```

## <a name="unregister-an-application-type"></a><span data-ttu-id="4ebaa-212">Cancelar o registro de um tipo de aplicativo</span><span class="sxs-lookup"><span data-stu-id="4ebaa-212">Unregister an application type</span></span>
<span data-ttu-id="4ebaa-213">Quando uma versão específica de um tipo de aplicativo não é mais necessária, cancele o registro do tipo de aplicativo usando o cmdlet [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="4ebaa-213">When a particular version of an application type is no longer needed, you should unregister the application type using the [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="4ebaa-214">O cancelamento de registro de tipos de aplicativo não utilizados libera espaço de armazenamento usado pelo repositório de imagens.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-214">Unregistering unused application types releases storage space used by the image store.</span></span> <span data-ttu-id="4ebaa-215">Um tipo de aplicativo pode ter seu registro cancelado, desde que não existam aplicativos instanciados nele e nenhuma atualização de aplicativo pendente que faça referência a ele.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-215">An application type can be unregistered as long as no applications are instantiated against it and no pending application upgrades are referencing it.</span></span>

<span data-ttu-id="4ebaa-216">Execute [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) para ver os tipos de aplicativo registrados no cluster no momento:</span><span class="sxs-lookup"><span data-stu-id="4ebaa-216">Run [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) to see the application types currently registered in the cluster:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

<span data-ttu-id="4ebaa-217">Execute [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) para cancelar o registro de um tipo de aplicativo específico:</span><span class="sxs-lookup"><span data-stu-id="4ebaa-217">Run [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) to unregister a specific application type:</span></span>

```powershell
PS C:\> Unregister-ServiceFabricApplicationType MyApplicationType 1.0.0
```

## <a name="remove-an-application-package-from-the-image-store"></a><span data-ttu-id="4ebaa-218">Remover um pacote de aplicativos do repositório de imagens</span><span class="sxs-lookup"><span data-stu-id="4ebaa-218">Remove an application package from the image store</span></span>
<span data-ttu-id="4ebaa-219">Quando um pacote de aplicativos não for mais necessário, você poderá excluí-lo do repositório de imagens para liberar recursos do sistema.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-219">When an application package is no longer needed, you can delete it from the image store to free up system resources.</span></span>

```powershell
PS C:\>Remove-ServiceFabricApplicationPackage -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest))
```

## <a name="troubleshooting"></a><span data-ttu-id="4ebaa-220">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="4ebaa-220">Troubleshooting</span></span>
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a><span data-ttu-id="4ebaa-221">Copy-ServiceFabricApplicationPackage solicita um ImageStoreConnectionString</span><span class="sxs-lookup"><span data-stu-id="4ebaa-221">Copy-ServiceFabricApplicationPackage asks for an ImageStoreConnectionString</span></span>
<span data-ttu-id="4ebaa-222">O ambiente do SDK da Malha do Serviço já deve ter os padrões corretos configurados.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-222">The Service Fabric SDK environment should already have the correct defaults set up.</span></span> <span data-ttu-id="4ebaa-223">Mas, se necessário, o ImageStoreConnectionString para todos os comandos deve corresponder ao valor que o cluster de Malha do Serviço está usando.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-223">But if needed, the ImageStoreConnectionString for all commands should match the value that the Service Fabric cluster is using.</span></span> <span data-ttu-id="4ebaa-224">Você pode encontrar ImageStoreConnectionString no manifesto do cluster, recuperado usando os comandos [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) e Get-ImageStoreConnectionStringFromClusterManifest:</span><span class="sxs-lookup"><span data-stu-id="4ebaa-224">You can find the ImageStoreConnectionString in the cluster manifest, retrieved using the [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) and Get-ImageStoreConnectionStringFromClusterManifest commands:</span></span>

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

<span data-ttu-id="4ebaa-225">O cmdlet **Get-ImageStoreConnectionStringFromClusterManifest** , que faz parte do módulo do PowerShell do SDK do Service Fabric, é usado para obter a cadeia de conexão do repositório de imagens.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-225">The **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of the Service Fabric SDK PowerShell module, is used to get the image store connection string.</span></span>  <span data-ttu-id="4ebaa-226">Para importar o módulo do SDK, execute:</span><span class="sxs-lookup"><span data-stu-id="4ebaa-226">To import the SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="4ebaa-227">ImageStoreConnectionString é encontrado no manifesto do cluster:</span><span class="sxs-lookup"><span data-stu-id="4ebaa-227">The ImageStoreConnectionString is found in the cluster manifest:</span></span>

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

<span data-ttu-id="4ebaa-228">Confira [Noções básicas sobre a configuração ImageStoreConnectionString](service-fabric-image-store-connection-string.md) para obter informações suplementares sobre o repositório de imagens e a cadeia de conexão de armazenamento de imagens.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-228">See [Understand the image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about the image store and image store connection string.</span></span>

### <a name="deploy-large-application-package"></a><span data-ttu-id="4ebaa-229">Implantar um pacote de aplicativos grande</span><span class="sxs-lookup"><span data-stu-id="4ebaa-229">Deploy large application package</span></span>
<span data-ttu-id="4ebaa-230">Problema: [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) atinge o tempo limite para um pacote de aplicativos grande (na ordem de GB).</span><span class="sxs-lookup"><span data-stu-id="4ebaa-230">Issue: [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) times out for a large application package (order of GB).</span></span>
<span data-ttu-id="4ebaa-231">Experimente:</span><span class="sxs-lookup"><span data-stu-id="4ebaa-231">Try:</span></span>
- <span data-ttu-id="4ebaa-232">Especificar um tempo limite maior para o comando [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) com o parâmetro `TimeoutSec`.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-232">Specify a larger timeout for [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command, with `TimeoutSec` parameter.</span></span> <span data-ttu-id="4ebaa-233">Por padrão, o tempo limite é de 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-233">By default, the timeout is 30 minutes.</span></span>
- <span data-ttu-id="4ebaa-234">Verifique a conexão de rede entre o computador de origem e o cluster.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-234">Check the network connection between your source machine and cluster.</span></span> <span data-ttu-id="4ebaa-235">Se a conexão estiver lenta, considere usar um computador com uma conexão de rede melhor.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-235">If the connection is slow, consider using a machine with a better network connection.</span></span>
<span data-ttu-id="4ebaa-236">Se o computador cliente estiver em uma região diferente do cluster, considere usar um computador cliente em uma região mais próxima ou na mesma que o cluster.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-236">If the client machine is in another region than the cluster, consider using a client machine in a closer or same region as the cluster.</span></span>
- <span data-ttu-id="4ebaa-237">Verifique se você está sofrendo limitação externa.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-237">Check if you are hitting external throttling.</span></span> <span data-ttu-id="4ebaa-238">Por exemplo, quando o repositório de imagens é configurado para usar o Armazenamento do Azure, o upload pode ser limitado.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-238">For example, when the image store is configured to use azure storage, upload may be throttled.</span></span>

<span data-ttu-id="4ebaa-239">Problema: o upload do pacote foi concluído com êxito, mas [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) atingiu o tempo limite.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-239">Issue: Upload package completed successfully, but [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) times out.</span></span>
<span data-ttu-id="4ebaa-240">Experimente:</span><span class="sxs-lookup"><span data-stu-id="4ebaa-240">Try:</span></span>
- <span data-ttu-id="4ebaa-241">[Compactar o pacote](service-fabric-package-apps.md#compress-a-package) antes de copiar para o repositório de imagens.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-241">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store.</span></span>
<span data-ttu-id="4ebaa-242">A compactação reduz o tamanho e o número de arquivos, o que por sua vez reduz a quantidade de tráfego e trabalho que o Service Fabric deve executar.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-242">The compression reduces the size and the number of files, which in turn reduces the amount of traffic and work that Service Fabric must perform.</span></span> <span data-ttu-id="4ebaa-243">A operação de upload pode ser mais lenta (especialmente se você incluir o tempo de compactação), mas as operações de registrar e cancelar o registro do tipo de aplicativo são mais rápidas.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-243">The upload operation may be slower (especially if you include the compression time), but register and un-register the application type are faster.</span></span>
- <span data-ttu-id="4ebaa-244">Especificar um tempo limite maior para o comando [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) com o parâmetro `TimeoutSec`.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-244">Specify a larger timeout for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) with `TimeoutSec` parameter.</span></span>
- <span data-ttu-id="4ebaa-245">Especifique a opção `Async` para [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="4ebaa-245">Specify `Async` switch for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span></span> <span data-ttu-id="4ebaa-246">O comando retorna quando o cluster aceita o comando e o registro do tipo de aplicativo continua de modo assíncrono.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-246">The command returns when the cluster accepts the command and the registration of the application type continues asynchronously.</span></span> <span data-ttu-id="4ebaa-247">Por esse motivo, não é necessário especificar um tempo limite maior nesse caso.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-247">For this reason, there is no need to specify a higher timeout in this case.</span></span> <span data-ttu-id="4ebaa-248">O comando [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) lista todas as versões do tipo de aplicativo registradas com êxito e seu status de registro.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-248">The [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="4ebaa-249">Você pode usar esse comando para determinar quando o registro é feito.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-249">You can use this command to determine when the registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

### <a name="deploy-application-package-with-many-files"></a><span data-ttu-id="4ebaa-250">Implantar pacote de aplicativos com muitos arquivos</span><span class="sxs-lookup"><span data-stu-id="4ebaa-250">Deploy application package with many files</span></span>
<span data-ttu-id="4ebaa-251">Problema: [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) atinge o tempo limite para um pacote de aplicativos com muitos arquivos (na ordem de milhares).</span><span class="sxs-lookup"><span data-stu-id="4ebaa-251">Issue: [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) times out for an application package with many files (order of thousands).</span></span>
<span data-ttu-id="4ebaa-252">Experimente:</span><span class="sxs-lookup"><span data-stu-id="4ebaa-252">Try:</span></span>
- <span data-ttu-id="4ebaa-253">[Compactar o pacote](service-fabric-package-apps.md#compress-a-package) antes de copiar para o repositório de imagens.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-253">[Compress the package](service-fabric-package-apps.md#compress-a-package) before copying to the image store.</span></span> <span data-ttu-id="4ebaa-254">A compactação reduz o número de arquivos.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-254">The compression reduces the number of files.</span></span>
- <span data-ttu-id="4ebaa-255">Especificar um tempo limite maior para o comando [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) com o parâmetro `TimeoutSec`.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-255">Specify a larger timeout for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) with `TimeoutSec` parameter.</span></span>
- <span data-ttu-id="4ebaa-256">Especifique a opção `Async` para [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="4ebaa-256">Specify `Async` switch for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span></span> <span data-ttu-id="4ebaa-257">O comando retorna quando o cluster aceita o comando e o registro do tipo de aplicativo continua de modo assíncrono.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-257">The command returns when the cluster accepts the command and the registration of the application type continues asynchronously.</span></span>
<span data-ttu-id="4ebaa-258">Por esse motivo, não é necessário especificar um tempo limite maior nesse caso.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-258">For this reason, there is no need to specify a higher timeout in this case.</span></span> <span data-ttu-id="4ebaa-259">O comando [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) lista todas as versões do tipo de aplicativo registradas com êxito e seu status de registro.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-259">The [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="4ebaa-260">Você pode usar esse comando para determinar quando o registro é feito.</span><span class="sxs-lookup"><span data-stu-id="4ebaa-260">You can use this command to determine when the registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="next-steps"></a><span data-ttu-id="4ebaa-261">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4ebaa-261">Next steps</span></span>
[<span data-ttu-id="4ebaa-262">Atualização de aplicativos do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4ebaa-262">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="4ebaa-263">Introdução à integridade da Malha do Serviço</span><span class="sxs-lookup"><span data-stu-id="4ebaa-263">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)

[<span data-ttu-id="4ebaa-264">Diagnosticar e solucionar problemas de um serviço da Malha do Serviço</span><span class="sxs-lookup"><span data-stu-id="4ebaa-264">Diagnose and troubleshoot a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="4ebaa-265">Modelar um aplicativo na Malha do Serviço</span><span class="sxs-lookup"><span data-stu-id="4ebaa-265">Model an application in Service Fabric</span></span>](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before the slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
