---
title: aaaPackage um aplicativo do Azure Service Fabric | Microsoft Docs
description: "Como toopackage um aplicativo de malha do serviço antes de implantar o cluster tooa."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: mani-ramaswamy
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: ryanwi
ms.openlocfilehash: b3918e1e25e532acdc9440855213e1fa364ea000
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="package-an-application"></a><span data-ttu-id="86c6e-103">Preparar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="86c6e-103">Package an application</span></span>
<span data-ttu-id="86c6e-104">Este artigo descreve como toopackage um aplicativo de serviço de malha e torná-lo pronto para a implantação.</span><span class="sxs-lookup"><span data-stu-id="86c6e-104">This article describes how toopackage a Service Fabric application and make it ready for deployment.</span></span>

## <a name="package-layout"></a><span data-ttu-id="86c6e-105">Layout do pacote</span><span class="sxs-lookup"><span data-stu-id="86c6e-105">Package layout</span></span>
<span data-ttu-id="86c6e-106">manifesto do aplicativo Hello, um ou mais manifestos de serviço e outros pacotes necessários arquivos devem ser organizados em um layout específico para implantação em um cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="86c6e-106">hello application manifest, one or more service manifests, and other necessary package files must be organized in a specific layout for deployment into a Service Fabric cluster.</span></span> <span data-ttu-id="86c6e-107">manifestos de exemplo Hello neste artigo precisaria toobe organizado em Olá estrutura de diretórios a seguir:</span><span class="sxs-lookup"><span data-stu-id="86c6e-107">hello example manifests in this article would need toobe organized in hello following directory structure:</span></span>

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat
```

<span data-ttu-id="86c6e-108">pastas de saudação são nomeadas toomatch Olá **nome** atributos de cada elemento correspondente.</span><span class="sxs-lookup"><span data-stu-id="86c6e-108">hello folders are named toomatch hello **Name** attributes of each corresponding element.</span></span> <span data-ttu-id="86c6e-109">Por exemplo, se hello o manifesto de serviço contidos dois pacotes de código com nomes de saudação **MyCodeA** e **MyCodeB**, em seguida, duas pastas com hello mesmos nomes conteria Olá binários necessários para cada código pacote.</span><span class="sxs-lookup"><span data-stu-id="86c6e-109">For example, if hello service manifest contained two code packages with hello names **MyCodeA** and **MyCodeB**, then two folders with hello same names would contain hello necessary binaries for each code package.</span></span>

## <a name="use-setupentrypoint"></a><span data-ttu-id="86c6e-110">Use o SetupEntryPoint</span><span class="sxs-lookup"><span data-stu-id="86c6e-110">Use SetupEntryPoint</span></span>
<span data-ttu-id="86c6e-111">Cenários típicos de uso **SetupEntryPoint** são quando precisar de um executável antes do início do serviço de saudação do toorun ou precisar tooperform uma operação com privilégios elevados.</span><span class="sxs-lookup"><span data-stu-id="86c6e-111">Typical scenarios for using **SetupEntryPoint** are when you need toorun an executable before hello service starts or you need tooperform an operation with elevated privileges.</span></span> <span data-ttu-id="86c6e-112">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="86c6e-112">For example:</span></span>

* <span data-ttu-id="86c6e-113">Configurando e inicializar variáveis de ambiente que Olá necessidades executável do serviço.</span><span class="sxs-lookup"><span data-stu-id="86c6e-113">Setting up and initializing environment variables that hello service executable needs.</span></span> <span data-ttu-id="86c6e-114">Não é limitado tooonly executáveis gravados por meio de modelos de programação de malha do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="86c6e-114">It is not limited tooonly executables written via hello Service Fabric programming models.</span></span> <span data-ttu-id="86c6e-115">Por exemplo, npm.exe precisa de algumas variáveis de ambiente configurados para implantar um aplicativo node.js.</span><span class="sxs-lookup"><span data-stu-id="86c6e-115">For example, npm.exe needs some environment variables configured for deploying a node.js application.</span></span>
* <span data-ttu-id="86c6e-116">Configurando o controle de acesso, instalando certificados de segurança.</span><span class="sxs-lookup"><span data-stu-id="86c6e-116">Setting up access control by installing security certificates.</span></span>

<span data-ttu-id="86c6e-117">Para obter mais informações sobre como Olá tooconfigure **SetupEntryPoint**, consulte [configurar política de saudação para um ponto de entrada de configuração de serviço](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="86c6e-117">For more information on how tooconfigure hello **SetupEntryPoint**, see [Configure hello policy for a service setup entry point](service-fabric-application-runas-security.md)</span></span>

<a id="Package-App"></a>
## <a name="configure"></a><span data-ttu-id="86c6e-118">Configurar</span><span class="sxs-lookup"><span data-stu-id="86c6e-118">Configure</span></span>
### <a name="build-a-package-by-using-visual-studio"></a><span data-ttu-id="86c6e-119">Compilar um pacote usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="86c6e-119">Build a package by using Visual Studio</span></span>
<span data-ttu-id="86c6e-120">Se você usar o Visual Studio 2015 toocreate seu aplicativo, você pode usar o hello pacote tooautomatically comando cria um pacote que corresponda layout Olá descrito acima.</span><span class="sxs-lookup"><span data-stu-id="86c6e-120">If you use Visual Studio 2015 toocreate your application, you can use hello Package command tooautomatically create a package that matches hello layout described above.</span></span>

<span data-ttu-id="86c6e-121">toocreate um pacote, clique em projeto de aplicativo hello no Gerenciador de soluções e escolha o comando de pacote hello, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="86c6e-121">toocreate a package, right-click hello application project in Solution Explorer and choose hello Package command, as shown below:</span></span>

![Empacotando um aplicativo no Visual Studio][vs-package-command]

<span data-ttu-id="86c6e-123">Quando a compactação estiver concluída, você pode encontrar o local de saudação do pacote de saudação no hello **saída** janela.</span><span class="sxs-lookup"><span data-stu-id="86c6e-123">When packaging is complete, you can find hello location of hello package in hello **Output** window.</span></span> <span data-ttu-id="86c6e-124">Olá empacotamento ocorrerá automaticamente quando você implantar ou depura seu aplicativo no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="86c6e-124">hello packaging step occurs automatically when you deploy or debug your application in Visual Studio.</span></span>

### <a name="build-a-package-by-command-line"></a><span data-ttu-id="86c6e-125">Criar um pacote pela linha de comando</span><span class="sxs-lookup"><span data-stu-id="86c6e-125">Build a package by command line</span></span>
<span data-ttu-id="86c6e-126">Também é possível tooprogrammatically pacote usando o aplicativo `msbuild.exe`.</span><span class="sxs-lookup"><span data-stu-id="86c6e-126">It is also possible tooprogrammatically package up your application using `msbuild.exe`.</span></span> <span data-ttu-id="86c6e-127">Bastidores hello, Visual Studio é executá-lo para a saída de hello é o mesma.</span><span class="sxs-lookup"><span data-stu-id="86c6e-127">Under hello hood, Visual Studio is running it so hello output is same.</span></span>

```shell
D:\Temp> msbuild HelloWorld.sfproj /t:Package
```

## <a name="test-hello-package"></a><span data-ttu-id="86c6e-128">Pacote de saudação do teste</span><span class="sxs-lookup"><span data-stu-id="86c6e-128">Test hello package</span></span>
<span data-ttu-id="86c6e-129">Você pode verificar a estrutura do pacote hello localmente por meio do PowerShell usando Olá [ServiceFabricApplicationPackage teste](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) comando.</span><span class="sxs-lookup"><span data-stu-id="86c6e-129">You can verify hello package structure locally through PowerShell by using hello [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) command.</span></span>
<span data-ttu-id="86c6e-130">Esse comando verifica se há problemas de análise de manifesto e também todas as referências.</span><span class="sxs-lookup"><span data-stu-id="86c6e-130">This command checks for manifest parsing issues and verify all references.</span></span> <span data-ttu-id="86c6e-131">Esse comando verifica apenas a exatidão estrutural Olá de diretórios de saudação e arquivos no pacote de saudação.</span><span class="sxs-lookup"><span data-stu-id="86c6e-131">This command only verifies hello structural correctness of hello directories and files in hello package.</span></span>
<span data-ttu-id="86c6e-132">Ele não verifica qualquer conteúdo do pacote de códigos ou dados do hello além de verificar se todos os arquivos necessários estão presentes.</span><span class="sxs-lookup"><span data-stu-id="86c6e-132">It doesn't verify any of hello code or data package contents beyond checking that all necessary files are present.</span></span>

```
PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
False
Test-ServiceFabricApplicationPackage : hello EntryPoint MySetup.bat is not found.
FileName: C:\Users\servicefabric\AppData\Local\Temp\TestApplicationPackage_7195781181\nrri205a.e2h\MyApplicationType\MyServiceManifest\ServiceManifest.xml
```

<span data-ttu-id="86c6e-133">Este erro mostra que Olá *MySetup.bat* arquivo referenciado no manifesto do serviço Olá **SetupEntryPoint** está ausente no pacote de código hello.</span><span class="sxs-lookup"><span data-stu-id="86c6e-133">This error shows that hello *MySetup.bat* file referenced in hello service manifest **SetupEntryPoint** is missing from hello code package.</span></span> <span data-ttu-id="86c6e-134">Depois que o arquivo ausente Olá é adicionado, passa a verificação do aplicativo hello:</span><span class="sxs-lookup"><span data-stu-id="86c6e-134">After hello missing file is added, hello application verification passes:</span></span>

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │       MySetup.bat
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat

PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
True
PS D:\temp>
```

<span data-ttu-id="86c6e-135">Se seu aplicativo tiver [parâmetros do aplicativo](service-fabric-manage-multiple-environment-app-configuration.md) definidos, você poderá passá-los em [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) para a validação correta.</span><span class="sxs-lookup"><span data-stu-id="86c6e-135">If your application has [application parameters](service-fabric-manage-multiple-environment-app-configuration.md) defined, you can pass them in [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) for proper validation.</span></span>

<span data-ttu-id="86c6e-136">Se você souber cluster Olá onde o aplicativo hello será implantado, é recomendável passar no hello `ImageStoreConnectionString` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="86c6e-136">If you know hello cluster where hello application will be deployed, it is recommended you pass in hello `ImageStoreConnectionString` parameter.</span></span> <span data-ttu-id="86c6e-137">Nesse caso, o pacote de Olá também é validado em relação a versões anteriores do aplicativo hello que já estão em execução no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="86c6e-137">In this case, hello package is also validated against previous versions of hello application that are already running in hello cluster.</span></span> <span data-ttu-id="86c6e-138">Por exemplo, a validação de saudação pode detectar se um pacote com hello mesma versão, mas conteúdo diferente já foi implantada.</span><span class="sxs-lookup"><span data-stu-id="86c6e-138">For example, hello validation can detect whether a package with hello same version but different content was already deployed.</span></span>  

<span data-ttu-id="86c6e-139">Depois que o aplicativo hello é empacotado corretamente e passa a validação, avalie com base no tamanho hello e número de saudação de arquivos se a compactação é necessária.</span><span class="sxs-lookup"><span data-stu-id="86c6e-139">Once hello application is packaged correctly and passes validation, evaluate based on hello size and hello number of files if compression is needed.</span></span>

## <a name="compress-a-package"></a><span data-ttu-id="86c6e-140">Compactar um pacote</span><span class="sxs-lookup"><span data-stu-id="86c6e-140">Compress a package</span></span>
<span data-ttu-id="86c6e-141">Quando um pacote é grande ou tem vários arquivos, você pode compactá-lo para uma implantação mais rápida.</span><span class="sxs-lookup"><span data-stu-id="86c6e-141">When a package is large or has many files, you can compress it for faster deployment.</span></span> <span data-ttu-id="86c6e-142">A compactação reduz o número de saudação de arquivos e o tamanho de pacote de saudação.</span><span class="sxs-lookup"><span data-stu-id="86c6e-142">Compression reduces hello number of files and hello package size.</span></span>
<span data-ttu-id="86c6e-143">Para um pacote de aplicativos compactados, [pacote de aplicativo hello Carregando](service-fabric-deploy-remove-applications.md#upload-the-application-package) pode levar mais comparados toouploading Olá descompactados pacote (especialmente se o tempo de compactação é acrescentado), mas [registrando](service-fabric-deploy-remove-applications.md#register-the-application-package) e [tipo de cancelamento do registro do aplicativo hello](service-fabric-deploy-remove-applications.md#unregister-an-application-type) são mais rápidos para um pacote de aplicativos compactados.</span><span class="sxs-lookup"><span data-stu-id="86c6e-143">For a compressed application package, [Uploading hello application package](service-fabric-deploy-remove-applications.md#upload-the-application-package) may take longer compared toouploading hello uncompressed package (specially if compression time is factored in), but [registering](service-fabric-deploy-remove-applications.md#register-the-application-package) and [un-registering hello application type](service-fabric-deploy-remove-applications.md#unregister-an-application-type) are faster for a compressed application package.</span></span>

<span data-ttu-id="86c6e-144">mecanismo de implantação de saudação é o mesmo para os pacotes compactados e não compactados.</span><span class="sxs-lookup"><span data-stu-id="86c6e-144">hello deployment mechanism is same for compressed and uncompressed packages.</span></span> <span data-ttu-id="86c6e-145">Se o pacote de saudação for compactado, ela é armazenada como tal no repositório de imagens de cluster hello e é descompactado no nó de saudação antes que o aplicativo hello é executado.</span><span class="sxs-lookup"><span data-stu-id="86c6e-145">If hello package is compressed, it is stored as such in hello cluster image store and it's uncompressed on hello node before hello application is run.</span></span>
<span data-ttu-id="86c6e-146">compactação de saudação substitui o pacote de Service Fabric válido de saudação com versão compactada Olá.</span><span class="sxs-lookup"><span data-stu-id="86c6e-146">hello compression replaces hello valid Service Fabric package with hello compressed version.</span></span> <span data-ttu-id="86c6e-147">pasta Olá deverá conceder permissões de gravação.</span><span class="sxs-lookup"><span data-stu-id="86c6e-147">hello folder must allow write permissions.</span></span> <span data-ttu-id="86c6e-148">A execução da compactação em um pacote já compactado não produz nenhuma alteração.</span><span class="sxs-lookup"><span data-stu-id="86c6e-148">Running compression on an already compressed package yields no changes.</span></span>

<span data-ttu-id="86c6e-149">É possível compactar um pacote executando o comando do Powershell Olá [cópia ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) com `CompressPackage` alternar.</span><span class="sxs-lookup"><span data-stu-id="86c6e-149">You can compress a package by running hello Powershell command [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) with `CompressPackage` switch.</span></span> <span data-ttu-id="86c6e-150">Olá descompactar pacote com hello mesmo comando, usando `UncompressPackage` alternar.</span><span class="sxs-lookup"><span data-stu-id="86c6e-150">You can uncompress hello package with hello same command, using `UncompressPackage` switch.</span></span>

<span data-ttu-id="86c6e-151">Olá comando a seguir compacta pacote hello sem copiá-lo toohello repositório de imagens.</span><span class="sxs-lookup"><span data-stu-id="86c6e-151">hello following command compresses hello package without copying it toohello image store.</span></span> <span data-ttu-id="86c6e-152">Você pode copiar um pacote compactado tooone ou mais clusters de malha do serviço, conforme necessário, usando [cópia ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) sem Olá `SkipCopy` sinalizador.</span><span class="sxs-lookup"><span data-stu-id="86c6e-152">You can copy a compressed package tooone or more Service Fabric clusters, as needed, using [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) without hello `SkipCopy` flag.</span></span>
<span data-ttu-id="86c6e-153">pacote de saudação agora inclui os arquivos compactados para Olá `code`, `config`, e `data` pacotes.</span><span class="sxs-lookup"><span data-stu-id="86c6e-153">hello package now includes zipped files for hello `code`, `config`, and `data` packages.</span></span> <span data-ttu-id="86c6e-154">o manifesto do aplicativo Hello e Olá manifestos do serviço não estão compactados, porque eles são necessários para várias operações internas (como compartilhamento de extração de versão e o nome de tipo de aplicativo para determinados validações de pacote).</span><span class="sxs-lookup"><span data-stu-id="86c6e-154">hello application manifest and hello service manifests are not zipped, because they are needed for many internal operations (like package sharing, application type name and version extraction for certain validations).</span></span>
<span data-ttu-id="86c6e-155">Manifestos de compactação Olá tornaria essas operações ineficiente.</span><span class="sxs-lookup"><span data-stu-id="86c6e-155">Zipping hello manifests would make these operations inefficient.</span></span>

```
PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
    │   ServiceManifest.xml
    │
    ├───MyCode
    │       MyServiceHost.exe
    │       MySetup.bat
    │
    ├───MyConfig
    │       Settings.xml
    │
    └───MyData
            init.dat
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -CompressPackage -SkipCopy

PS D:\temp> tree /f .\MyApplicationType

D:\TEMP\MYAPPLICATIONTYPE
│   ApplicationManifest.xml
│
└───MyServiceManifest
       ServiceManifest.xml
       MyCode.zip
       MyConfig.zip
       MyData.zip

```

<span data-ttu-id="86c6e-156">Como alternativa, você pode compactar e copiar o pacote de saudação com [ServiceFabricApplicationPackage cópia](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) em uma única etapa.</span><span class="sxs-lookup"><span data-stu-id="86c6e-156">Alternatively, you can compress and copy hello package with [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) in one step.</span></span>
<span data-ttu-id="86c6e-157">Se o pacote de saudação for grande, forneça uma hora de tooallow de tempo limite alto o suficiente para compactação de pacote hello e o cluster de toohello de carregamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="86c6e-157">If hello package is large, provide a high enough timeout tooallow time for both hello package compression and hello upload toohello cluster.</span></span>
```
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -ApplicationPackagePathInImageStore MyApplicationType -ImageStoreConnectionString fabric:ImageStore -CompressPackage -TimeoutSec 5400
```

<span data-ttu-id="86c6e-158">Internamente, o Service Fabric calcula somas de verificação para pacotes de aplicativos Olá para validação.</span><span class="sxs-lookup"><span data-stu-id="86c6e-158">Internally, Service Fabric computes checksums for hello application packages for validation.</span></span> <span data-ttu-id="86c6e-159">Ao usar a compactação, Olá somas de verificação são computadas em Olá compactado versões de cada pacote.</span><span class="sxs-lookup"><span data-stu-id="86c6e-159">When using compression, hello checksums are computed on hello zipped versions of each package.</span></span>
<span data-ttu-id="86c6e-160">Se você copiou uma versão descompactada do seu pacote de aplicativo, e você desejar toouse compactação Olá mesmo pacote, você deve alterar as versões de saudação do hello `code`, `config`, e `data` incompatibilidade de soma de verificação de tooavoid de pacotes.</span><span class="sxs-lookup"><span data-stu-id="86c6e-160">If you copied an uncompressed version of your application package, and you want toouse compression for hello same package, you must change hello versions of hello `code`, `config`, and `data` packages tooavoid checksum mismatch.</span></span> <span data-ttu-id="86c6e-161">Se os pacotes de saudação forem alterados, em vez de alterar a versão de hello, você pode usar [comparação provisionamento](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="86c6e-161">If hello packages are unchanged, instead of changing hello version, you can use [diff provisioning](service-fabric-application-upgrade-advanced.md).</span></span> <span data-ttu-id="86c6e-162">Com essa opção, não inclua pacote inalterado Olá em vez disso, referenciá-lo no manifesto do serviço hello.</span><span class="sxs-lookup"><span data-stu-id="86c6e-162">With this option, do not include hello unchanged package instead reference it from hello service manifest.</span></span>

<span data-ttu-id="86c6e-163">Da mesma forma, se você carregou uma versão compactada do pacote de saudação e você desejar toouse um pacote não compactado, você deve atualizar a incompatibilidade de soma de verificação Olá versões tooavoid hello.</span><span class="sxs-lookup"><span data-stu-id="86c6e-163">Similarly, if you uploaded a compressed version of hello package and you want toouse an uncompressed package, you must update hello versions tooavoid hello checksum mismatch.</span></span>

<span data-ttu-id="86c6e-164">Olá pacote é agora empacotado corretamente, validado e compactado (se necessário), para que esteja pronta para [implantação](service-fabric-deploy-remove-applications.md) tooone ou uma malha de serviço mais clusters.</span><span class="sxs-lookup"><span data-stu-id="86c6e-164">hello package is now packaged correctly, validated, and compressed (if needed), so it is ready for [deployment](service-fabric-deploy-remove-applications.md) tooone or more Service Fabric clusters.</span></span>

### <a name="compress-packages-when-deploying-using-visual-studio"></a><span data-ttu-id="86c6e-165">Compactar pacotes durante a implantação usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="86c6e-165">Compress packages when deploying using Visual Studio</span></span>
<span data-ttu-id="86c6e-166">Você pode instruir pacotes toocompress do Visual Studio na implantação, adicionando Olá `CopyPackageParameters` tooyour elemento perfil de publicação e definir Olá `CompressPackage` atributo muito`true`.</span><span class="sxs-lookup"><span data-stu-id="86c6e-166">You can instruct Visual Studio toocompress packages on deployment, by adding hello `CopyPackageParameters` element tooyour publish profile, and set hello `CompressPackage` attribute too`true`.</span></span>

``` xml
    <PublishProfile xmlns="http://schemas.microsoft.com/2015/05/fabrictools">
        <ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com" />
        <ApplicationParameterFile Path="..\ApplicationParameters\Cloud.xml" />
        <CopyPackageParameters CompressPackage="true"/>
    </PublishProfile>
```

## <a name="next-steps"></a><span data-ttu-id="86c6e-167">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="86c6e-167">Next steps</span></span>
<span data-ttu-id="86c6e-168">[Implantar e remover aplicativos] [ 10] descreve como instâncias do aplicativo toouse PowerShell toomanage</span><span class="sxs-lookup"><span data-stu-id="86c6e-168">[Deploy and remove applications][10] describes how toouse PowerShell toomanage application instances</span></span>

<span data-ttu-id="86c6e-169">[Gerenciando parâmetros do aplicativo para vários ambientes] [ 11] descreve como tooconfigure parâmetros e variáveis de ambiente para instâncias de aplicativo diferente.</span><span class="sxs-lookup"><span data-stu-id="86c6e-169">[Managing application parameters for multiple environments][11] describes how tooconfigure parameters and environment variables for different application instances.</span></span>

<span data-ttu-id="86c6e-170">[Configurar políticas de segurança para seu aplicativo] [ 12] descreve como os serviços de toorun em acesso de toorestrict de políticas de segurança.</span><span class="sxs-lookup"><span data-stu-id="86c6e-170">[Configure security policies for your application][12] describes how toorun services under security policies toorestrict access.</span></span>

<!--Image references-->
[vs-package-command]: ./media/service-fabric-package-apps/vs-package-command.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
