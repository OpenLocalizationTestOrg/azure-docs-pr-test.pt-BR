---
title: "aaaAzure implantação de aplicativos do Service Fabric | Microsoft Docs"
description: "Como toodeploy e remova os aplicativos na malha do serviço usando o PowerShell."
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
ms.openlocfilehash: 3de9c6a937ee7b29bf9ec86d6e9e631487797507
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-remove-applications-using-powershell"></a><span data-ttu-id="01835-103">Implantar e remover aplicativos usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="01835-103">Deploy and remove applications using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="01835-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="01835-104">PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
> * [<span data-ttu-id="01835-105">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="01835-105">Visual Studio</span></span>](service-fabric-publish-app-remote-cluster.md)
> * [<span data-ttu-id="01835-106">APIs de FabricClient</span><span class="sxs-lookup"><span data-stu-id="01835-106">FabricClient APIs</span></span>](service-fabric-deploy-remove-applications-fabricclient.md)
> 
> 

<br/>

<span data-ttu-id="01835-107">Assim que um [tipo de aplicativo for empacotado][10], ele está pronto para implantação em um cluster do Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="01835-107">Once an [application type has been packaged][10], it's ready for deployment into an Azure Service Fabric cluster.</span></span> <span data-ttu-id="01835-108">Implantação envolve Olá três etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="01835-108">Deployment involves hello following three steps:</span></span>

1. <span data-ttu-id="01835-109">Carregar o repositório de imagens toohello do pacote de aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="01835-109">Upload hello application package toohello image store</span></span>
2. <span data-ttu-id="01835-110">Registrar o tipo de aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="01835-110">Register hello application type</span></span>
3. <span data-ttu-id="01835-111">Criar instância de aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="01835-111">Create hello application instance</span></span>

<span data-ttu-id="01835-112">Depois que um aplicativo é implantado e uma instância está em execução no cluster hello, você pode excluir a instância do aplicativo hello e seu tipo de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="01835-112">After an application is deployed and an instance is running in hello cluster, you can delete hello application instance and its application type.</span></span> <span data-ttu-id="01835-113">toocompletely remover um aplicativo de cluster Olá envolve Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="01835-113">toocompletely remove an application from hello cluster involves hello following steps:</span></span>

1. <span data-ttu-id="01835-114">Remover (ou excluir) Olá executando a instância do aplicativo</span><span class="sxs-lookup"><span data-stu-id="01835-114">Remove (or delete) hello running application instance</span></span>
2. <span data-ttu-id="01835-115">Cancelar o registro do tipo de aplicativo hello se você não precisar mais dela</span><span class="sxs-lookup"><span data-stu-id="01835-115">Unregister hello application type if you no longer need it</span></span>
3. <span data-ttu-id="01835-116">Remover o pacote de aplicativo hello saudação do repositório de imagens</span><span class="sxs-lookup"><span data-stu-id="01835-116">Remove hello application package from hello image store</span></span>

<span data-ttu-id="01835-117">Se você usar [Visual Studio para implantar e depurar aplicativos](service-fabric-publish-app-remote-cluster.md) no cluster de desenvolvimento local, todos os Olá etapas anteriores são tratadas automaticamente por meio de um script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="01835-117">If you use [Visual Studio for deploying and debugging applications](service-fabric-publish-app-remote-cluster.md) on your local development cluster, all hello preceding steps are handled automatically through a PowerShell script.</span></span>  <span data-ttu-id="01835-118">Esse script é encontrado no hello *Scripts* pasta do projeto de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="01835-118">This script is found in hello *Scripts* folder of hello application project.</span></span> <span data-ttu-id="01835-119">Este artigo fornece informações detalhadas sobre o que esse script está fazendo para que você possa executar Olá mesmas operações fora do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="01835-119">This article provides background on what that script is doing so that you can perform hello same operations outside of Visual Studio.</span></span> 
 
## <a name="connect-toohello-cluster"></a><span data-ttu-id="01835-120">Conecte-se o cluster toohello</span><span class="sxs-lookup"><span data-stu-id="01835-120">Connect toohello cluster</span></span>
<span data-ttu-id="01835-121">Antes de executar quaisquer comandos do PowerShell neste artigo, sempre iniciar usando [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cluster do tooconnect toohello do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="01835-121">Before you run any PowerShell commands in this article, always start by using [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) tooconnect toohello Service Fabric cluster.</span></span> <span data-ttu-id="01835-122">cluster de desenvolvimento local em toohello tooconnect, execute Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="01835-122">tooconnect toohello local development cluster, run hello following:</span></span>

```powershell
PS C:\>Connect-ServiceFabricCluster
```

<span data-ttu-id="01835-123">Para obter exemplos de conexão tooa remoto cluster ou protegido usando o Active Directory do Azure, X509 certificados ou consulte Active Directory do Windows [conectar tooa segura cluster](service-fabric-connect-to-secure-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="01835-123">For examples of connecting tooa remote cluster or cluster secured using Azure Active Directory, X509 certificates, or Windows Active Directory see [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

## <a name="upload-hello-application-package"></a><span data-ttu-id="01835-124">Carregar pacote de aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="01835-124">Upload hello application package</span></span>
<span data-ttu-id="01835-125">Carregar pacote de aplicativo hello coloca em um local que seja acessível pelos componentes internos do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="01835-125">Uploading hello application package puts it in a location that's accessible by internal Service Fabric components.</span></span>
<span data-ttu-id="01835-126">Se quiser que o pacote de aplicativo de saudação tooverify localmente, use Olá [ServiceFabricApplicationPackage teste](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="01835-126">If you want tooverify hello application package locally, use hello [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="01835-127">Olá [ServiceFabricApplicationPackage cópia](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) comando carregamentos Olá repositório de imagem do aplicativo pacotes toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="01835-127">hello [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command uploads hello application package toohello cluster image store.</span></span>
<span data-ttu-id="01835-128">Olá **ImageStoreConnectionStringFromClusterManifest Get** cmdlet, que é parte do módulo do PowerShell do SDK do Service Fabric Olá, é a imagem de saudação do tooget usado armazenar a cadeia de caracteres de conexão.</span><span class="sxs-lookup"><span data-stu-id="01835-128">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="01835-129">módulo SDK em Olá tooimport, execute:</span><span class="sxs-lookup"><span data-stu-id="01835-129">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="01835-130">Suponha que você crie e empacote um aplicativo chamado *MyApplication* no Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="01835-130">Suppose you build and package an application named *MyApplication* in Visual Studio 2015.</span></span> <span data-ttu-id="01835-131">Por padrão, o nome do tipo de aplicativo hello listado no hello ApplicationManifest.xml é "MyApplicationType".</span><span class="sxs-lookup"><span data-stu-id="01835-131">By default, hello application type name listed in hello ApplicationManifest.xml is "MyApplicationType".</span></span>  <span data-ttu-id="01835-132">Olá pacote de aplicativo, que contém o manifesto de aplicativo necessário hello, manifestos do serviço e pacotes de dados/de configuração de código, está localizado em *C:\Users\<username\>\Documents\Visual 2015\Projects\ Studio MyApplication\MyApplication\pkg\Debug*.</span><span class="sxs-lookup"><span data-stu-id="01835-132">hello application package, which contains hello necessary application manifest, service manifests, and code/config/data packages, is located in *C:\Users\<username\>\Documents\Visual Studio 2015\Projects\MyApplication\MyApplication\pkg\Debug*.</span></span> 

<span data-ttu-id="01835-133">Olá comando a seguir lista os conteúdos de Olá Olá do pacote de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="01835-133">hello following command lists hello contents of hello application package:</span></span>

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

<span data-ttu-id="01835-134">Se o pacote de aplicativo hello é grande e/ou tem muitos arquivos, você pode [compactá-los](service-fabric-package-apps.md#compress-a-package).</span><span class="sxs-lookup"><span data-stu-id="01835-134">If hello application package is large and/or has many files, you can [compress it](service-fabric-package-apps.md#compress-a-package).</span></span> <span data-ttu-id="01835-135">compactação de saudação reduz o tamanho de saudação e número de saudação de arquivos.</span><span class="sxs-lookup"><span data-stu-id="01835-135">hello compression reduces hello size and hello number of files.</span></span>
<span data-ttu-id="01835-136">Olá, efeito colateral é que hello cancelamento do registro e registrar o tipo de aplicativo são mais rápidos.</span><span class="sxs-lookup"><span data-stu-id="01835-136">hello side effect is that registering and un-registering hello application type are faster.</span></span> <span data-ttu-id="01835-137">Tempo de carregamento pode ser mais lento no momento, especialmente se você incluir o pacote de saudação do hello tempo toocompress.</span><span class="sxs-lookup"><span data-stu-id="01835-137">Upload time may be slower currently, especially if you include hello time toocompress hello package.</span></span> 

<span data-ttu-id="01835-138">toocompress um pacote, use Olá mesmo [ServiceFabricApplicationPackage cópia](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) comando.</span><span class="sxs-lookup"><span data-stu-id="01835-138">toocompress a package, use hello same [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command.</span></span> <span data-ttu-id="01835-139">A compactação pode ser feita separado de carregamento, usando Olá `SkipCopy` sinalizador ou junto com hello operação de carregamento.</span><span class="sxs-lookup"><span data-stu-id="01835-139">Compression can be done separate from upload, by using hello `SkipCopy` flag, or together with hello upload operation.</span></span> <span data-ttu-id="01835-140">Aplicar compactação em um pacote compactado é não operacional.</span><span class="sxs-lookup"><span data-stu-id="01835-140">Applying compression on a compressed package is no-op.</span></span>
<span data-ttu-id="01835-141">um pacote compactado, o uso de toouncompress Olá mesmo [cópia ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) com hello `UncompressPackage` alternar.</span><span class="sxs-lookup"><span data-stu-id="01835-141">toouncompress a compressed package, use hello same [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command with hello `UncompressPackage` switch.</span></span>

<span data-ttu-id="01835-142">Olá cmdlet a seguir compacta pacote hello sem copiá-lo toohello repositório de imagens.</span><span class="sxs-lookup"><span data-stu-id="01835-142">hello following cmdlet compresses hello package without copying it toohello image store.</span></span> <span data-ttu-id="01835-143">pacote de saudação agora inclui os arquivos compactados para Olá `Code` e `Config` pacotes.</span><span class="sxs-lookup"><span data-stu-id="01835-143">hello package now includes zipped files for hello `Code` and `Config` packages.</span></span> <span data-ttu-id="01835-144">Olá manifestos de aplicativo e Olá service não estão compactados, porque eles são necessários para várias operações internas (como compartilhamento de extração de versão e o nome de tipo de aplicativo para determinados validações de pacote).</span><span class="sxs-lookup"><span data-stu-id="01835-144">hello application and hello service manifests are not zipped, because they are needed for many internal operations (like package sharing, application type name and version extraction for certain validations).</span></span> <span data-ttu-id="01835-145">Manifestos de compactação Olá tornaria essas operações ineficiente.</span><span class="sxs-lookup"><span data-stu-id="01835-145">Zipping hello manifests would make these operations inefficient.</span></span>

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

<span data-ttu-id="01835-146">Para pacotes de aplicativo grande, a compactação Olá leva tempo.</span><span class="sxs-lookup"><span data-stu-id="01835-146">For large application packages, hello compression takes time.</span></span> <span data-ttu-id="01835-147">Para obter melhores resultados, use uma unidade SSD rápida.</span><span class="sxs-lookup"><span data-stu-id="01835-147">For best results, use a fast SSD drive.</span></span> <span data-ttu-id="01835-148">tempos de compactação de Hello e tamanho de saudação do pacote compactado Olá também variam com base no conteúdo do pacote de saudação.</span><span class="sxs-lookup"><span data-stu-id="01835-148">hello compression times and hello size of hello compressed package also differ based on hello package content.</span></span>
<span data-ttu-id="01835-149">Por exemplo, aqui está o estatísticas de compactação para alguns pacotes, que mostram a saudação inicial e Olá tamanho de pacote compactado, com tempo de compactação de saudação.</span><span class="sxs-lookup"><span data-stu-id="01835-149">For example, here is compression statistics for some packages, which show hello initial and hello compressed package size, with hello compression time.</span></span>

|<span data-ttu-id="01835-150">Tamanho inicial (MB)</span><span class="sxs-lookup"><span data-stu-id="01835-150">Initial size (MB)</span></span>|<span data-ttu-id="01835-151">Contagem de arquivos</span><span class="sxs-lookup"><span data-stu-id="01835-151">File count</span></span>|<span data-ttu-id="01835-152">Tempo de compactação</span><span class="sxs-lookup"><span data-stu-id="01835-152">Compression Time</span></span>|<span data-ttu-id="01835-153">Tamanho do pacote compactado (MB)</span><span class="sxs-lookup"><span data-stu-id="01835-153">Compressed package size (MB)</span></span>|
|----------------:|---------:|---------------:|---------------------------:|
|<span data-ttu-id="01835-154">100</span><span class="sxs-lookup"><span data-stu-id="01835-154">100</span></span>|<span data-ttu-id="01835-155">100</span><span class="sxs-lookup"><span data-stu-id="01835-155">100</span></span>|<span data-ttu-id="01835-156">00:00:03.3547592</span><span class="sxs-lookup"><span data-stu-id="01835-156">00:00:03.3547592</span></span>|<span data-ttu-id="01835-157">60</span><span class="sxs-lookup"><span data-stu-id="01835-157">60</span></span>|
|<span data-ttu-id="01835-158">512</span><span class="sxs-lookup"><span data-stu-id="01835-158">512</span></span>|<span data-ttu-id="01835-159">100</span><span class="sxs-lookup"><span data-stu-id="01835-159">100</span></span>|<span data-ttu-id="01835-160">00:00:16.3850303</span><span class="sxs-lookup"><span data-stu-id="01835-160">00:00:16.3850303</span></span>|<span data-ttu-id="01835-161">307</span><span class="sxs-lookup"><span data-stu-id="01835-161">307</span></span>|
|<span data-ttu-id="01835-162">1.024</span><span class="sxs-lookup"><span data-stu-id="01835-162">1024</span></span>|<span data-ttu-id="01835-163">500</span><span class="sxs-lookup"><span data-stu-id="01835-163">500</span></span>|<span data-ttu-id="01835-164">00:00:32.5907950</span><span class="sxs-lookup"><span data-stu-id="01835-164">00:00:32.5907950</span></span>|<span data-ttu-id="01835-165">615</span><span class="sxs-lookup"><span data-stu-id="01835-165">615</span></span>|
|<span data-ttu-id="01835-166">2.048</span><span class="sxs-lookup"><span data-stu-id="01835-166">2048</span></span>|<span data-ttu-id="01835-167">1000</span><span class="sxs-lookup"><span data-stu-id="01835-167">1000</span></span>|<span data-ttu-id="01835-168">00:01:04.3775554</span><span class="sxs-lookup"><span data-stu-id="01835-168">00:01:04.3775554</span></span>|<span data-ttu-id="01835-169">1231</span><span class="sxs-lookup"><span data-stu-id="01835-169">1231</span></span>|
|<span data-ttu-id="01835-170">5012</span><span class="sxs-lookup"><span data-stu-id="01835-170">5012</span></span>|<span data-ttu-id="01835-171">100</span><span class="sxs-lookup"><span data-stu-id="01835-171">100</span></span>|<span data-ttu-id="01835-172">00:02:45.2951288</span><span class="sxs-lookup"><span data-stu-id="01835-172">00:02:45.2951288</span></span>|<span data-ttu-id="01835-173">3074</span><span class="sxs-lookup"><span data-stu-id="01835-173">3074</span></span>|

<span data-ttu-id="01835-174">Depois que um pacote é compactado, pode ser carregado tooone ou clusters de vários Service Fabric conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="01835-174">Once a package is compressed, it can be uploaded tooone or multiple Service Fabric clusters as needed.</span></span> <span data-ttu-id="01835-175">mecanismo de implantação de saudação é o mesmo para os pacotes compactados e não compactados.</span><span class="sxs-lookup"><span data-stu-id="01835-175">hello deployment mechanism is same for compressed and uncompressed packages.</span></span> <span data-ttu-id="01835-176">Se o pacote de saudação for compactado, ela é armazenada como tal no repositório de imagens de cluster hello e é descompactado no nó de saudação antes que o aplicativo hello é executado.</span><span class="sxs-lookup"><span data-stu-id="01835-176">If hello package is compressed, it is stored as such in hello cluster image store and it's uncompressed on hello node before hello application is run.</span></span>


<span data-ttu-id="01835-177">Olá exemplo a seguir carrega repositório de imagens toohello do pacote hello, em uma pasta chamada "MyApplicationV1":</span><span class="sxs-lookup"><span data-stu-id="01835-177">hello following example uploads hello package toohello image store, into a folder named "MyApplicationV1":</span></span>

```powershell
PS C:\> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $path -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)) -TimeoutSec 1800
```

<span data-ttu-id="01835-178">Olá **ImageStoreConnectionStringFromClusterManifest Get** cmdlet, que é parte do módulo do PowerShell do SDK do Service Fabric Olá, é a imagem de saudação do tooget usado armazenar a cadeia de caracteres de conexão.</span><span class="sxs-lookup"><span data-stu-id="01835-178">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="01835-179">módulo SDK em Olá tooimport, execute:</span><span class="sxs-lookup"><span data-stu-id="01835-179">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="01835-180">Se você não especificar Olá *- ApplicationPackagePathInImageStore* parâmetro, pacote de aplicativo hello é copiado para hello "Depuração" no repositório de imagens de saudação.</span><span class="sxs-lookup"><span data-stu-id="01835-180">If you do not specify hello *-ApplicationPackagePathInImageStore* parameter, hello application package is copied into hello "Debug" folder in hello image store.</span></span>

<span data-ttu-id="01835-181">Olá tempo tooupload um pacote difere dependendo de vários fatores.</span><span class="sxs-lookup"><span data-stu-id="01835-181">hello time it takes tooupload a package differs depending on multiple factors.</span></span> <span data-ttu-id="01835-182">Alguns desses fatores são o número de saudação de arquivos no pacote de saudação, tamanho do pacote hello e tamanhos de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="01835-182">Some of these factors are hello number of files in hello package, hello package size, and hello file sizes.</span></span> <span data-ttu-id="01835-183">a velocidade da rede Olá entre máquina de origem hello e cluster do Service Fabric Olá também afeta o tempo de carregamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="01835-183">hello network speed between hello source machine and hello Service Fabric cluster also impacts hello upload time.</span></span> <span data-ttu-id="01835-184">Olá tempo limite padrão de [ServiceFabricApplicationPackage cópia](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) é de 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="01835-184">hello default timeout for [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) is 30 minutes.</span></span>
<span data-ttu-id="01835-185">Dependendo Olá fatores descritos, você pode ter o tempo limite de saudação tooincrease.</span><span class="sxs-lookup"><span data-stu-id="01835-185">Depending on hello described factors, you may have tooincrease hello timeout.</span></span> <span data-ttu-id="01835-186">Se você estiver compactando pacote hello na chamada de cópia hello, será necessário tooalso considerar o tempo de compactação de saudação.</span><span class="sxs-lookup"><span data-stu-id="01835-186">If you are compressing hello package in hello copy call, you need tooalso consider hello compression time.</span></span>

<span data-ttu-id="01835-187">Consulte [entender a cadeia de conexão de repositório de imagens Olá](service-fabric-image-store-connection-string.md) para obter mais informações sobre repositório de imagens hello e imagem armazenam a cadeia de caracteres de conexão.</span><span class="sxs-lookup"><span data-stu-id="01835-187">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

## <a name="register-hello-application-package"></a><span data-ttu-id="01835-188">Registrar pacote de aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="01835-188">Register hello application package</span></span>
<span data-ttu-id="01835-189">tipo de aplicativo Hello e versão declarados no manifesto de aplicativo hello ficam disponível para uso quando o pacote de aplicativo hello está registrado.</span><span class="sxs-lookup"><span data-stu-id="01835-189">hello application type and version declared in hello application manifest become available for use when hello application package is registered.</span></span> <span data-ttu-id="01835-190">sistema Olá lê o pacote de saudação carregado na etapa anterior Olá, verifica o pacote de saudação, processa o conteúdo do pacote hello e copia o local do hello processado pacote tooan interno do sistema.</span><span class="sxs-lookup"><span data-stu-id="01835-190">hello system reads hello package uploaded in hello previous step, verifies hello package, processes hello package contents, and copies hello processed package tooan internal system location.</span></span>  

<span data-ttu-id="01835-191">Executar Olá [ServiceFabricApplicationType registro](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) tooregister cmdlet Olá tipo de aplicativo no cluster hello e disponibilizá-lo para implantação:</span><span class="sxs-lookup"><span data-stu-id="01835-191">Run hello [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) cmdlet tooregister hello application type in hello cluster and make it available for deployment:</span></span>

```powershell
PS C:\> Register-ServiceFabricApplicationType MyApplicationV1
Register application type succeeded
```

<span data-ttu-id="01835-192">"MyApplicationV1" é a pasta de saudação no repositório de imagem Olá onde o pacote de aplicativo hello está localizado.</span><span class="sxs-lookup"><span data-stu-id="01835-192">"MyApplicationV1" is hello folder in hello image store where hello application package is located.</span></span> <span data-ttu-id="01835-193">saudação de tipo de aplicativo com o nome "MyApplicationType" e a versão "1.0.0" (ambos são encontradas no manifesto do aplicativo hello) agora é registrado no cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="01835-193">hello application type with name "MyApplicationType" and version "1.0.0" (both are found in hello application manifest) is now registered in hello cluster.</span></span>

<span data-ttu-id="01835-194">Olá [ServiceFabricApplicationType registro](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) comando retorna somente depois que o sistema de saudação tem o pacote de aplicativo hello registrado com êxito.</span><span class="sxs-lookup"><span data-stu-id="01835-194">hello [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) command returns only after hello system has successfully registered hello application package.</span></span> <span data-ttu-id="01835-195">Quanto tempo leva de registro depende tamanho hello e o conteúdo do pacote de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="01835-195">How long registration takes depends on hello size and contents of hello application package.</span></span> <span data-ttu-id="01835-196">Se necessário, Olá **- TimeoutSec** parâmetro pode ser usado toosupply um tempo limite maior (tempo limite da saudação padrão é 60 segundos).</span><span class="sxs-lookup"><span data-stu-id="01835-196">If needed, hello **-TimeoutSec** parameter can be used toosupply a longer timeout (hello default timeout is 60 seconds).</span></span>

<span data-ttu-id="01835-197">Se você tiver um aplicativo grande pacote ou se você estiver enfrentando tempos limite, use Olá **- Async** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="01835-197">If you have a large application package or if you are experiencing timeouts, use hello **-Async** parameter.</span></span> <span data-ttu-id="01835-198">comando Olá retorna ao cluster Olá aceita o comando ' register ' hello, e o processamento de saudação continua conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="01835-198">hello command returns when hello cluster accepts hello register command, and hello processing continues as needed.</span></span>
<span data-ttu-id="01835-199">Olá [ServiceFabricApplicationType Get](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) comando lista todas as versões do tipo de aplicativo registrado com êxito e seu status de registro.</span><span class="sxs-lookup"><span data-stu-id="01835-199">hello [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="01835-200">Você pode usar esse comando toodetermine ao Olá registro está pronto.</span><span class="sxs-lookup"><span data-stu-id="01835-200">You can use this command toodetermine when hello registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="create-hello-application"></a><span data-ttu-id="01835-201">Criar um aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="01835-201">Create hello application</span></span>
<span data-ttu-id="01835-202">Você pode instanciar um aplicativo de qualquer versão do tipo de aplicativo que foi registrado com êxito usando Olá [ServiceFabricApplication novo](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="01835-202">You can instantiate an application from any application type version that has been registered successfully by using hello [New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="01835-203">nome de saudação de cada aplicativo deve começar com hello *"fabric:"* esquema e deve ser exclusivo para cada instância do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="01835-203">hello name of each application must start with hello *"fabric:"* scheme and must be unique for each application instance.</span></span> <span data-ttu-id="01835-204">Todos os serviços padrão definidos no manifesto de aplicativo de saudação do tipo de aplicativo de destino Olá também são criados.</span><span class="sxs-lookup"><span data-stu-id="01835-204">Any default services defined in hello application manifest of hello target application type are also created.</span></span>

```powershell
PS C:\> New-ServiceFabricApplication fabric:/MyApp MyApplicationType 1.0.0

ApplicationName        : fabric:/MyApp
ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
ApplicationParameters  : {}
```
<span data-ttu-id="01835-205">Várias instâncias do aplicativo podem ser criadas para qualquer determinada versão de um tipo de aplicativo registrado.</span><span class="sxs-lookup"><span data-stu-id="01835-205">Multiple application instances can be created for any given version of a registered application type.</span></span> <span data-ttu-id="01835-206">Cada instância do aplicativo é executada isoladamente, com seu próprio processo e diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="01835-206">Each application instance runs in isolation, with its own work directory and process.</span></span>

<span data-ttu-id="01835-207">toosee chamado aplicativos e serviços estão em execução no cluster hello, executar Olá [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) e [ServiceFabricService Get](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) cmdlets:</span><span class="sxs-lookup"><span data-stu-id="01835-207">toosee which named apps and services are running in hello cluster, run hello [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) and [Get-ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) cmdlets:</span></span>

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

## <a name="remove-an-application"></a><span data-ttu-id="01835-208">Remover um aplicativo</span><span class="sxs-lookup"><span data-stu-id="01835-208">Remove an application</span></span>
<span data-ttu-id="01835-209">Quando uma instância de aplicativo não for mais necessário, você poderá removê-lo permanentemente por nome usando Olá [ServiceFabricApplication remover](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="01835-209">When an application instance is no longer needed, you can permanently remove it by name using hello [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="01835-210">[Remover ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) remove automaticamente todos os serviços que pertencem a aplicativo toohello bem, permanentemente, removendo todos os estados de serviço.</span><span class="sxs-lookup"><span data-stu-id="01835-210">[Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) automatically removes all services that belong toohello application as well, permanently removing all service state.</span></span> 

> [!WARNING]
> <span data-ttu-id="01835-211">Essa operação não pode ser revertida e o estado do aplicativo não pode ser recuperado.</span><span class="sxs-lookup"><span data-stu-id="01835-211">This operation cannot be reversed, and application state cannot be recovered.</span></span>

```powershell
PS C:\> Remove-ServiceFabricApplication fabric:/MyApp

Confirm
Continue with this operation?
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):
Remove application instance succeeded

PS C:\> Get-ServiceFabricApplication
```

## <a name="unregister-an-application-type"></a><span data-ttu-id="01835-212">Cancelar o registro de um tipo de aplicativo</span><span class="sxs-lookup"><span data-stu-id="01835-212">Unregister an application type</span></span>
<span data-ttu-id="01835-213">Quando uma versão específica de um tipo de aplicativo não for mais necessário, você deve cancelar o registro do tipo de aplicativo hello usando Olá [ServiceFabricApplicationType Unregister](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="01835-213">When a particular version of an application type is no longer needed, you should unregister hello application type using hello [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="01835-214">Cancelando o registro não usadas de aplicativo tipos versões espaço de armazenamento usado pelo repositório de imagem hello.</span><span class="sxs-lookup"><span data-stu-id="01835-214">Unregistering unused application types releases storage space used by hello image store.</span></span> <span data-ttu-id="01835-215">Um tipo de aplicativo pode ter seu registro cancelado, desde que não existam aplicativos instanciados nele e nenhuma atualização de aplicativo pendente que faça referência a ele.</span><span class="sxs-lookup"><span data-stu-id="01835-215">An application type can be unregistered as long as no applications are instantiated against it and no pending application upgrades are referencing it.</span></span>

<span data-ttu-id="01835-216">Executar [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) toosee Olá aplicativo atualmente registrados no cluster hello:</span><span class="sxs-lookup"><span data-stu-id="01835-216">Run [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) toosee hello application types currently registered in hello cluster:</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

<span data-ttu-id="01835-217">Executar [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) toounregister um tipo de aplicativo específico:</span><span class="sxs-lookup"><span data-stu-id="01835-217">Run [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) toounregister a specific application type:</span></span>

```powershell
PS C:\> Unregister-ServiceFabricApplicationType MyApplicationType 1.0.0
```

## <a name="remove-an-application-package-from-hello-image-store"></a><span data-ttu-id="01835-218">Remover um pacote de aplicativo hello do repositório de imagens</span><span class="sxs-lookup"><span data-stu-id="01835-218">Remove an application package from hello image store</span></span>
<span data-ttu-id="01835-219">Quando um pacote de aplicativo não for mais necessário, você poderá excluí-la da saudação imagem repositório toofree recursos do sistema.</span><span class="sxs-lookup"><span data-stu-id="01835-219">When an application package is no longer needed, you can delete it from hello image store toofree up system resources.</span></span>

```powershell
PS C:\>Remove-ServiceFabricApplicationPackage -ApplicationPackagePathInImageStore MyApplicationV1 -ImageStoreConnectionString (Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest))
```

## <a name="troubleshooting"></a><span data-ttu-id="01835-220">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="01835-220">Troubleshooting</span></span>
### <a name="copy-servicefabricapplicationpackage-asks-for-an-imagestoreconnectionstring"></a><span data-ttu-id="01835-221">Copy-ServiceFabricApplicationPackage solicita um ImageStoreConnectionString</span><span class="sxs-lookup"><span data-stu-id="01835-221">Copy-ServiceFabricApplicationPackage asks for an ImageStoreConnectionString</span></span>
<span data-ttu-id="01835-222">ambiente de SDK do Service Fabric Olá já deve ter Olá correto padrões configurar.</span><span class="sxs-lookup"><span data-stu-id="01835-222">hello Service Fabric SDK environment should already have hello correct defaults set up.</span></span> <span data-ttu-id="01835-223">Mas se necessário, Olá ImageStoreConnectionString para todos os comandos deve coincidir valor Olá que Olá malha do serviço de cluster está usando.</span><span class="sxs-lookup"><span data-stu-id="01835-223">But if needed, hello ImageStoreConnectionString for all commands should match hello value that hello Service Fabric cluster is using.</span></span> <span data-ttu-id="01835-224">Você pode encontrar hello ImageStoreConnectionString no manifesto do cluster hello, recuperadas usando Olá [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) e comandos Get-ImageStoreConnectionStringFromClusterManifest:</span><span class="sxs-lookup"><span data-stu-id="01835-224">You can find hello ImageStoreConnectionString in hello cluster manifest, retrieved using hello [Get-ServiceFabricClusterManifest](/powershell/module/servicefabric/get-servicefabricclustermanifest?view=azureservicefabricps) and Get-ImageStoreConnectionStringFromClusterManifest commands:</span></span>

```powershell
PS C:\> Get-ImageStoreConnectionStringFromClusterManifest(Get-ServiceFabricClusterManifest)
```

<span data-ttu-id="01835-225">Olá **ImageStoreConnectionStringFromClusterManifest Get** cmdlet, que é parte do módulo do PowerShell do SDK do Service Fabric Olá, é a imagem de saudação do tooget usado armazenar a cadeia de caracteres de conexão.</span><span class="sxs-lookup"><span data-stu-id="01835-225">hello **Get-ImageStoreConnectionStringFromClusterManifest** cmdlet, which is part of hello Service Fabric SDK PowerShell module, is used tooget hello image store connection string.</span></span>  <span data-ttu-id="01835-226">módulo SDK em Olá tooimport, execute:</span><span class="sxs-lookup"><span data-stu-id="01835-226">tooimport hello SDK module, run:</span></span>

```powershell
Import-Module "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\Tools\PSModule\ServiceFabricSDK\ServiceFabricSDK.psm1"
```

<span data-ttu-id="01835-227">Olá ImageStoreConnectionString foi encontrado no manifesto do cluster hello:</span><span class="sxs-lookup"><span data-stu-id="01835-227">hello ImageStoreConnectionString is found in hello cluster manifest:</span></span>

```xml
<ClusterManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="Server-Default-SingleNode" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

    [...]

    <Section Name="Management">
      <Parameter Name="ImageStoreConnectionString" Value="file:D:\ServiceFabric\Data\ImageStore" />
    </Section>

    [...]
```

<span data-ttu-id="01835-228">Consulte [entender a cadeia de conexão de repositório de imagens Olá](service-fabric-image-store-connection-string.md) para obter mais informações sobre repositório de imagens hello e imagem armazenam a cadeia de caracteres de conexão.</span><span class="sxs-lookup"><span data-stu-id="01835-228">See [Understand hello image store connection string](service-fabric-image-store-connection-string.md) for supplementary information about hello image store and image store connection string.</span></span>

### <a name="deploy-large-application-package"></a><span data-ttu-id="01835-229">Implantar um pacote de aplicativos grande</span><span class="sxs-lookup"><span data-stu-id="01835-229">Deploy large application package</span></span>
<span data-ttu-id="01835-230">Problema: [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) atinge o tempo limite para um pacote de aplicativos grande (na ordem de GB).</span><span class="sxs-lookup"><span data-stu-id="01835-230">Issue: [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) times out for a large application package (order of GB).</span></span>
<span data-ttu-id="01835-231">Experimente:</span><span class="sxs-lookup"><span data-stu-id="01835-231">Try:</span></span>
- <span data-ttu-id="01835-232">Especificar um tempo limite maior para o comando [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) com o parâmetro `TimeoutSec`.</span><span class="sxs-lookup"><span data-stu-id="01835-232">Specify a larger timeout for [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) command, with `TimeoutSec` parameter.</span></span> <span data-ttu-id="01835-233">Por padrão, o tempo limite de saudação é 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="01835-233">By default, hello timeout is 30 minutes.</span></span>
- <span data-ttu-id="01835-234">Verifique a conexão de rede de saudação entre o computador de origem e o cluster.</span><span class="sxs-lookup"><span data-stu-id="01835-234">Check hello network connection between your source machine and cluster.</span></span> <span data-ttu-id="01835-235">Se a conexão de saudação estiver lenta, considere o uso de uma máquina com uma conexão de rede melhor.</span><span class="sxs-lookup"><span data-stu-id="01835-235">If hello connection is slow, consider using a machine with a better network connection.</span></span>
<span data-ttu-id="01835-236">Se máquina do cliente Olá for em outra região de cluster hello, considere usando um computador cliente em uma região mais próxima ou mesmo como cluster hello.</span><span class="sxs-lookup"><span data-stu-id="01835-236">If hello client machine is in another region than hello cluster, consider using a client machine in a closer or same region as hello cluster.</span></span>
- <span data-ttu-id="01835-237">Verifique se você está sofrendo limitação externa.</span><span class="sxs-lookup"><span data-stu-id="01835-237">Check if you are hitting external throttling.</span></span> <span data-ttu-id="01835-238">Por exemplo, quando o repositório de imagens Olá é armazenamento toouse configurada do azure, carregamento pode ser limitado.</span><span class="sxs-lookup"><span data-stu-id="01835-238">For example, when hello image store is configured toouse azure storage, upload may be throttled.</span></span>

<span data-ttu-id="01835-239">Problema: o upload do pacote foi concluído com êxito, mas [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) atingiu o tempo limite. Experimente:</span><span class="sxs-lookup"><span data-stu-id="01835-239">Issue: Upload package completed successfully, but [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) times out. Try:</span></span>
- <span data-ttu-id="01835-240">[Compactar pacote hello](service-fabric-package-apps.md#compress-a-package) antes de copiar toohello repositório de imagens.</span><span class="sxs-lookup"><span data-stu-id="01835-240">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span>
<span data-ttu-id="01835-241">compactação Olá reduz o tamanho do hello e Olá vários arquivos, que por sua vez reduz a quantidade de saudação do tráfego e funciona malha esse serviço devem executar.</span><span class="sxs-lookup"><span data-stu-id="01835-241">hello compression reduces hello size and hello number of files, which in turn reduces hello amount of traffic and work that Service Fabric must perform.</span></span> <span data-ttu-id="01835-242">operação de carregamento de saudação pode ser mais lenta (especialmente se você incluir o tempo de compactação de saudação), mas o tipo de aplicativo hello registrar e cancelar o registro são mais rápidos.</span><span class="sxs-lookup"><span data-stu-id="01835-242">hello upload operation may be slower (especially if you include hello compression time), but register and un-register hello application type are faster.</span></span>
- <span data-ttu-id="01835-243">Especificar um tempo limite maior para o comando [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) com o parâmetro `TimeoutSec`.</span><span class="sxs-lookup"><span data-stu-id="01835-243">Specify a larger timeout for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) with `TimeoutSec` parameter.</span></span>
- <span data-ttu-id="01835-244">Especifique a opção `Async` para [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="01835-244">Specify `Async` switch for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span></span> <span data-ttu-id="01835-245">comando Olá retorna quando o cluster Olá aceita o comando hello e registro de saudação do tipo de aplicativo hello continua assincronamente.</span><span class="sxs-lookup"><span data-stu-id="01835-245">hello command returns when hello cluster accepts hello command and hello registration of hello application type continues asynchronously.</span></span> <span data-ttu-id="01835-246">Por esse motivo, há toospecify sem necessidade de um tempo limite maior nesse caso.</span><span class="sxs-lookup"><span data-stu-id="01835-246">For this reason, there is no need toospecify a higher timeout in this case.</span></span> <span data-ttu-id="01835-247">Olá [ServiceFabricApplicationType Get](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) comando lista todas as versões do tipo de aplicativo registrado com êxito e seu status de registro.</span><span class="sxs-lookup"><span data-stu-id="01835-247">hello [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="01835-248">Você pode usar esse comando toodetermine ao Olá registro está pronto.</span><span class="sxs-lookup"><span data-stu-id="01835-248">You can use this command toodetermine when hello registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

### <a name="deploy-application-package-with-many-files"></a><span data-ttu-id="01835-249">Implantar pacote de aplicativos com muitos arquivos</span><span class="sxs-lookup"><span data-stu-id="01835-249">Deploy application package with many files</span></span>
<span data-ttu-id="01835-250">Problema: [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) atinge o tempo limite para um pacote de aplicativos com muitos arquivos (na ordem de milhares).</span><span class="sxs-lookup"><span data-stu-id="01835-250">Issue: [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) times out for an application package with many files (order of thousands).</span></span>
<span data-ttu-id="01835-251">Experimente:</span><span class="sxs-lookup"><span data-stu-id="01835-251">Try:</span></span>
- <span data-ttu-id="01835-252">[Compactar pacote hello](service-fabric-package-apps.md#compress-a-package) antes de copiar toohello repositório de imagens.</span><span class="sxs-lookup"><span data-stu-id="01835-252">[Compress hello package](service-fabric-package-apps.md#compress-a-package) before copying toohello image store.</span></span> <span data-ttu-id="01835-253">compactação de saudação reduz o número de saudação de arquivos.</span><span class="sxs-lookup"><span data-stu-id="01835-253">hello compression reduces hello number of files.</span></span>
- <span data-ttu-id="01835-254">Especificar um tempo limite maior para o comando [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) com o parâmetro `TimeoutSec`.</span><span class="sxs-lookup"><span data-stu-id="01835-254">Specify a larger timeout for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) with `TimeoutSec` parameter.</span></span>
- <span data-ttu-id="01835-255">Especifique a opção `Async` para [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="01835-255">Specify `Async` switch for [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps).</span></span> <span data-ttu-id="01835-256">comando Olá retorna quando o cluster Olá aceita o comando hello e registro de saudação do tipo de aplicativo hello continua assincronamente.</span><span class="sxs-lookup"><span data-stu-id="01835-256">hello command returns when hello cluster accepts hello command and hello registration of hello application type continues asynchronously.</span></span>
<span data-ttu-id="01835-257">Por esse motivo, há toospecify sem necessidade de um tempo limite maior nesse caso.</span><span class="sxs-lookup"><span data-stu-id="01835-257">For this reason, there is no need toospecify a higher timeout in this case.</span></span> <span data-ttu-id="01835-258">Olá [ServiceFabricApplicationType Get](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) comando lista todas as versões do tipo de aplicativo registrado com êxito e seu status de registro.</span><span class="sxs-lookup"><span data-stu-id="01835-258">hello [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) command lists all successfully registered application type versions and their registration status.</span></span> <span data-ttu-id="01835-259">Você pode usar esse comando toodetermine ao Olá registro está pronto.</span><span class="sxs-lookup"><span data-stu-id="01835-259">You can use this command toodetermine when hello registration is done.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationType

ApplicationTypeName    : MyApplicationType
ApplicationTypeVersion : 1.0.0
Status                 : Available
DefaultParameters      : { "Stateless1_InstanceCount" = "-1" }
```

## <a name="next-steps"></a><span data-ttu-id="01835-260">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="01835-260">Next steps</span></span>
[<span data-ttu-id="01835-261">Atualização de aplicativos do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="01835-261">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="01835-262">Introdução à integridade da Malha do Serviço</span><span class="sxs-lookup"><span data-stu-id="01835-262">Service Fabric health introduction</span></span>](service-fabric-health-introduction.md)

[<span data-ttu-id="01835-263">Diagnosticar e solucionar problemas de um serviço da Malha do Serviço</span><span class="sxs-lookup"><span data-stu-id="01835-263">Diagnose and troubleshoot a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="01835-264">Modelar um aplicativo na Malha do Serviço</span><span class="sxs-lookup"><span data-stu-id="01835-264">Model an application in Service Fabric</span></span>](service-fabric-application-model.md)

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-application-model.md
[11]: service-fabric-application-upgrade.md
