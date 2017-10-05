---
title: Empacotar um aplicativo do Azure Service Fabric | Microsoft Docs
description: Como empacotar um aplicativo do Service Fabric antes de implantar em um cluster.
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
ms.openlocfilehash: 486a27d7ca576c8fe1552c02eb24ece6b8bb2ba8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="package-an-application"></a><span data-ttu-id="3cc08-103">Preparar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="3cc08-103">Package an application</span></span>
<span data-ttu-id="3cc08-104">Este artigo descreve como empacotar um aplicativo do Service Fabric e deixá-lo pronto para implantação.</span><span class="sxs-lookup"><span data-stu-id="3cc08-104">This article describes how to package a Service Fabric application and make it ready for deployment.</span></span>

## <a name="package-layout"></a><span data-ttu-id="3cc08-105">Layout do pacote</span><span class="sxs-lookup"><span data-stu-id="3cc08-105">Package layout</span></span>
<span data-ttu-id="3cc08-106">O manifesto do aplicativo, um ou mais manifestos do serviço e outros arquivos de pacote necessários devem ser organizados em um layout específico para implantação em um cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="3cc08-106">The application manifest, one or more service manifests, and other necessary package files must be organized in a specific layout for deployment into a Service Fabric cluster.</span></span> <span data-ttu-id="3cc08-107">Os manifestos de exemplo neste artigo precisariam estar organizados na seguinte estrutura de diretórios:</span><span class="sxs-lookup"><span data-stu-id="3cc08-107">The example manifests in this article would need to be organized in the following directory structure:</span></span>

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

<span data-ttu-id="3cc08-108">As pastas são nomeadas para corresponder a atributos **Name** de cada elemento correspondente.</span><span class="sxs-lookup"><span data-stu-id="3cc08-108">The folders are named to match the **Name** attributes of each corresponding element.</span></span> <span data-ttu-id="3cc08-109">Por exemplo, se o manifesto do serviço contiver dois pacotes de códigos com os nomes **MyCodeA** e **MyCodeB**, então, duas pastas com os mesmos nomes conteriam os binários necessários para cada pacote de códigos.</span><span class="sxs-lookup"><span data-stu-id="3cc08-109">For example, if the service manifest contained two code packages with the names **MyCodeA** and **MyCodeB**, then two folders with the same names would contain the necessary binaries for each code package.</span></span>

## <a name="use-setupentrypoint"></a><span data-ttu-id="3cc08-110">Use o SetupEntryPoint</span><span class="sxs-lookup"><span data-stu-id="3cc08-110">Use SetupEntryPoint</span></span>
<span data-ttu-id="3cc08-111">Cenários típicos de uso do **SetupEntryPoint** quando você precisa executar um executável antes do início do serviço ou você precisa executar uma operação com privilégios elevados.</span><span class="sxs-lookup"><span data-stu-id="3cc08-111">Typical scenarios for using **SetupEntryPoint** are when you need to run an executable before the service starts or you need to perform an operation with elevated privileges.</span></span> <span data-ttu-id="3cc08-112">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="3cc08-112">For example:</span></span>

* <span data-ttu-id="3cc08-113">Configurar e inicializar as variáveis de ambiente que o serviço executável precisa.</span><span class="sxs-lookup"><span data-stu-id="3cc08-113">Setting up and initializing environment variables that the service executable needs.</span></span> <span data-ttu-id="3cc08-114">Isso não é limitado apenas a executáveis gravados por meio de modelos de programação do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="3cc08-114">It is not limited to only executables written via the Service Fabric programming models.</span></span> <span data-ttu-id="3cc08-115">Por exemplo, npm.exe precisa de algumas variáveis de ambiente configurados para implantar um aplicativo node.js.</span><span class="sxs-lookup"><span data-stu-id="3cc08-115">For example, npm.exe needs some environment variables configured for deploying a node.js application.</span></span>
* <span data-ttu-id="3cc08-116">Configurando o controle de acesso, instalando certificados de segurança.</span><span class="sxs-lookup"><span data-stu-id="3cc08-116">Setting up access control by installing security certificates.</span></span>

<span data-ttu-id="3cc08-117">Para obter mais informações sobre como configurar o **SetupEntryPoint**, consulte [Configurar a política para um ponto de entrada de instalação do serviço](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="3cc08-117">For more information on how to configure the **SetupEntryPoint**, see [Configure the policy for a service setup entry point](service-fabric-application-runas-security.md)</span></span>

<a id="Package-App"></a>
## <a name="configure"></a><span data-ttu-id="3cc08-118">Configurar</span><span class="sxs-lookup"><span data-stu-id="3cc08-118">Configure</span></span>
### <a name="build-a-package-by-using-visual-studio"></a><span data-ttu-id="3cc08-119">Compilar um pacote usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3cc08-119">Build a package by using Visual Studio</span></span>
<span data-ttu-id="3cc08-120">Se você usar o Visual Studio 2015 para criar o seu aplicativo, pode usar o comando Package para criar automaticamente um pacote que corresponda ao layout descrito acima.</span><span class="sxs-lookup"><span data-stu-id="3cc08-120">If you use Visual Studio 2015 to create your application, you can use the Package command to automatically create a package that matches the layout described above.</span></span>

<span data-ttu-id="3cc08-121">Para criar um pacote, clique com o botão direito do mouse no projeto de aplicativo no Gerenciador de Soluções e escolha o comando de Pacote, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="3cc08-121">To create a package, right-click the application project in Solution Explorer and choose the Package command, as shown below:</span></span>

![Empacotando um aplicativo no Visual Studio][vs-package-command]

<span data-ttu-id="3cc08-123">Quando o empacotamento estiver concluído, você poderá encontrar o local do pacote na janela **Saída**.</span><span class="sxs-lookup"><span data-stu-id="3cc08-123">When packaging is complete, you can find the location of the package in the **Output** window.</span></span> <span data-ttu-id="3cc08-124">A etapa de empacotamento ocorre automaticamente quando você implanta ou depura seu aplicativo no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3cc08-124">The packaging step occurs automatically when you deploy or debug your application in Visual Studio.</span></span>

### <a name="build-a-package-by-command-line"></a><span data-ttu-id="3cc08-125">Criar um pacote pela linha de comando</span><span class="sxs-lookup"><span data-stu-id="3cc08-125">Build a package by command line</span></span>
<span data-ttu-id="3cc08-126">Também é possível empacote seu aplicativo de modo programático usando `msbuild.exe`.</span><span class="sxs-lookup"><span data-stu-id="3cc08-126">It is also possible to programmatically package up your application using `msbuild.exe`.</span></span> <span data-ttu-id="3cc08-127">Nos bastidores, o Visual Studio está sendo executado, de forma que o resultado é o mesmo.</span><span class="sxs-lookup"><span data-stu-id="3cc08-127">Under the hood, Visual Studio is running it so the output is same.</span></span>

```shell
D:\Temp> msbuild HelloWorld.sfproj /t:Package
```

## <a name="test-the-package"></a><span data-ttu-id="3cc08-128">Teste o pacote</span><span class="sxs-lookup"><span data-stu-id="3cc08-128">Test the package</span></span>
<span data-ttu-id="3cc08-129">Você pode verificar a estrutura do pacote localmente por meio do PowerShell usando o comando [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) .</span><span class="sxs-lookup"><span data-stu-id="3cc08-129">You can verify the package structure locally through PowerShell by using the [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) command.</span></span>
<span data-ttu-id="3cc08-130">Esse comando verifica se há problemas de análise de manifesto e também todas as referências.</span><span class="sxs-lookup"><span data-stu-id="3cc08-130">This command checks for manifest parsing issues and verify all references.</span></span> <span data-ttu-id="3cc08-131">Observe que esse comando só verifica a correção estrutural de diretórios e arquivos no pacote.</span><span class="sxs-lookup"><span data-stu-id="3cc08-131">This command only verifies the structural correctness of the directories and files in the package.</span></span>
<span data-ttu-id="3cc08-132">Ele não verificará nenhum código ou conteúdo do pacote de dados além de verificar se todos os arquivos necessários estão presentes.</span><span class="sxs-lookup"><span data-stu-id="3cc08-132">It doesn't verify any of the code or data package contents beyond checking that all necessary files are present.</span></span>

```
PS D:\temp> Test-ServiceFabricApplicationPackage .\MyApplicationType
False
Test-ServiceFabricApplicationPackage : The EntryPoint MySetup.bat is not found.
FileName: C:\Users\servicefabric\AppData\Local\Temp\TestApplicationPackage_7195781181\nrri205a.e2h\MyApplicationType\MyServiceManifest\ServiceManifest.xml
```

<span data-ttu-id="3cc08-133">Esse erro mostra que o arquivo *MySetup.bat* referenciado no manifesto do serviço **SetupEntryPoint** está ausente do pacote de código.</span><span class="sxs-lookup"><span data-stu-id="3cc08-133">This error shows that the *MySetup.bat* file referenced in the service manifest **SetupEntryPoint** is missing from the code package.</span></span> <span data-ttu-id="3cc08-134">Depois de adicionar o arquivo que está faltando, a verificação do aplicativo é aprovada:</span><span class="sxs-lookup"><span data-stu-id="3cc08-134">After the missing file is added, the application verification passes:</span></span>

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

<span data-ttu-id="3cc08-135">Se seu aplicativo tiver [parâmetros do aplicativo](service-fabric-manage-multiple-environment-app-configuration.md) definidos, você poderá passá-los em [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) para a validação correta.</span><span class="sxs-lookup"><span data-stu-id="3cc08-135">If your application has [application parameters](service-fabric-manage-multiple-environment-app-configuration.md) defined, you can pass them in [Test-ServiceFabricApplicationPackage](/powershell/module/servicefabric/test-servicefabricapplicationpackage?view=azureservicefabricps) for proper validation.</span></span>

<span data-ttu-id="3cc08-136">Se você souber o cluster em que o aplicativo será implantado, é recomendado passar o parâmetro `ImageStoreConnectionString`.</span><span class="sxs-lookup"><span data-stu-id="3cc08-136">If you know the cluster where the application will be deployed, it is recommended you pass in the `ImageStoreConnectionString` parameter.</span></span> <span data-ttu-id="3cc08-137">Nesse caso, o pacote também é validado para as versões anteriores do aplicativo que já estão em execução no cluster.</span><span class="sxs-lookup"><span data-stu-id="3cc08-137">In this case, the package is also validated against previous versions of the application that are already running in the cluster.</span></span> <span data-ttu-id="3cc08-138">Por exemplo, a validação pode detectar se um pacote com a mesma versão mas conteúdo diferente já foi implantado.</span><span class="sxs-lookup"><span data-stu-id="3cc08-138">For example, the validation can detect whether a package with the same version but different content was already deployed.</span></span>  

<span data-ttu-id="3cc08-139">Depois que o aplicativo for empacotado corretamente for validado com êxito, avalie com base no tamanho e no número de arquivos se há necessidade de compactação.</span><span class="sxs-lookup"><span data-stu-id="3cc08-139">Once the application is packaged correctly and passes validation, evaluate based on the size and the number of files if compression is needed.</span></span>

## <a name="compress-a-package"></a><span data-ttu-id="3cc08-140">Compactar um pacote</span><span class="sxs-lookup"><span data-stu-id="3cc08-140">Compress a package</span></span>
<span data-ttu-id="3cc08-141">Quando um pacote é grande ou tem vários arquivos, você pode compactá-lo para uma implantação mais rápida.</span><span class="sxs-lookup"><span data-stu-id="3cc08-141">When a package is large or has many files, you can compress it for faster deployment.</span></span> <span data-ttu-id="3cc08-142">A compactação reduz o número de arquivos e o tamanho do pacote.</span><span class="sxs-lookup"><span data-stu-id="3cc08-142">Compression reduces the number of files and the package size.</span></span>
<span data-ttu-id="3cc08-143">Para um pacote de aplicativos compactado, [carregar o pacote de aplicativos](service-fabric-deploy-remove-applications.md#upload-the-application-package) pode levar mais tempo comparado a carregar o pacote não compactado (especialmente se o tempo de compactação for levado em conta), mas [registrar](service-fabric-deploy-remove-applications.md#register-the-application-package) e [cancelar o registro do tipo de aplicativo](service-fabric-deploy-remove-applications.md#unregister-an-application-type) é mais rápido para um pacote de aplicativos compactado.</span><span class="sxs-lookup"><span data-stu-id="3cc08-143">For a compressed application package, [Uploading the application package](service-fabric-deploy-remove-applications.md#upload-the-application-package) may take longer compared to uploading the uncompressed package (specially if compression time is factored in), but [registering](service-fabric-deploy-remove-applications.md#register-the-application-package) and [un-registering the application type](service-fabric-deploy-remove-applications.md#unregister-an-application-type) are faster for a compressed application package.</span></span>

<span data-ttu-id="3cc08-144">O mecanismo de implantação é o mesmo para pacotes compactados e não compactados.</span><span class="sxs-lookup"><span data-stu-id="3cc08-144">The deployment mechanism is same for compressed and uncompressed packages.</span></span> <span data-ttu-id="3cc08-145">Se o pacote for compactado ele será armazenado como tal no repositório de imagens do cluster e será descompactado no nó antes que o aplicativo seja executado.</span><span class="sxs-lookup"><span data-stu-id="3cc08-145">If the package is compressed, it is stored as such in the cluster image store and it's uncompressed on the node before the application is run.</span></span>
<span data-ttu-id="3cc08-146">A compactação substitui o pacote do Service Fabric válido pela versão compactada.</span><span class="sxs-lookup"><span data-stu-id="3cc08-146">The compression replaces the valid Service Fabric package with the compressed version.</span></span> <span data-ttu-id="3cc08-147">A pasta deve aceitar permissões de gravação.</span><span class="sxs-lookup"><span data-stu-id="3cc08-147">The folder must allow write permissions.</span></span> <span data-ttu-id="3cc08-148">A execução da compactação em um pacote já compactado não produz nenhuma alteração.</span><span class="sxs-lookup"><span data-stu-id="3cc08-148">Running compression on an already compressed package yields no changes.</span></span>

<span data-ttu-id="3cc08-149">Você pode compactar um pacote executando o comando do PowerShell [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) com a opção `CompressPackage`.</span><span class="sxs-lookup"><span data-stu-id="3cc08-149">You can compress a package by running the Powershell command [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) with `CompressPackage` switch.</span></span> <span data-ttu-id="3cc08-150">Você pode descompactar o pacote com o mesmo comando, usando a opção `UncompressPackage`.</span><span class="sxs-lookup"><span data-stu-id="3cc08-150">You can uncompress the package with the same command, using `UncompressPackage` switch.</span></span>

<span data-ttu-id="3cc08-151">O comando a seguir compacta o pacote sem copiá-lo para o repositório de imagens.</span><span class="sxs-lookup"><span data-stu-id="3cc08-151">The following command compresses the package without copying it to the image store.</span></span> <span data-ttu-id="3cc08-152">Você pode copiar um pacote compactado para um ou mais clusters do Service Fabric, conforme necessário, usando [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) sem o sinalizador `SkipCopy`.</span><span class="sxs-lookup"><span data-stu-id="3cc08-152">You can copy a compressed package to one or more Service Fabric clusters, as needed, using [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) without the `SkipCopy` flag.</span></span>
<span data-ttu-id="3cc08-153">O pacote agora inclui arquivos compactados para os pacotes `code`, `config` e `data`.</span><span class="sxs-lookup"><span data-stu-id="3cc08-153">The package now includes zipped files for the `code`, `config`, and `data` packages.</span></span> <span data-ttu-id="3cc08-154">O manifesto do aplicativo e os manifestos do serviço não são compactados porque eles são necessários para várias operações internas (como compartilhamento do pacote, extração da versão e nome do tipo de aplicativo para determinadas validações).</span><span class="sxs-lookup"><span data-stu-id="3cc08-154">The application manifest and the service manifests are not zipped, because they are needed for many internal operations (like package sharing, application type name and version extraction for certain validations).</span></span>
<span data-ttu-id="3cc08-155">Compactar os manifestos tornaria essas operações ineficientes.</span><span class="sxs-lookup"><span data-stu-id="3cc08-155">Zipping the manifests would make these operations inefficient.</span></span>

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

<span data-ttu-id="3cc08-156">Como alternativa, você pode compactar e copiar o pacote com [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) em uma única etapa.</span><span class="sxs-lookup"><span data-stu-id="3cc08-156">Alternatively, you can compress and copy the package with [Copy-ServiceFabricApplicationPackage](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) in one step.</span></span>
<span data-ttu-id="3cc08-157">Se o pacote for grande, forneça um tempo limite suficientemente longo para que haja tempo tanto para a compactação do pacote quanto para o upload para o cluster.</span><span class="sxs-lookup"><span data-stu-id="3cc08-157">If the package is large, provide a high enough timeout to allow time for both the package compression and the upload to the cluster.</span></span>
```
PS D:\temp> Copy-ServiceFabricApplicationPackage -ApplicationPackagePath .\MyApplicationType -ApplicationPackagePathInImageStore MyApplicationType -ImageStoreConnectionString fabric:ImageStore -CompressPackage -TimeoutSec 5400
```

<span data-ttu-id="3cc08-158">Internamente, o Service Fabric computa somas de verificação para os pacotes de aplicativos para validação.</span><span class="sxs-lookup"><span data-stu-id="3cc08-158">Internally, Service Fabric computes checksums for the application packages for validation.</span></span> <span data-ttu-id="3cc08-159">Ao usar a compactação, as somas de verificação são calculadas nas versões compactadas de cada pacote.</span><span class="sxs-lookup"><span data-stu-id="3cc08-159">When using compression, the checksums are computed on the zipped versions of each package.</span></span>
<span data-ttu-id="3cc08-160">Se você copiou uma versão não compactada de seu pacote de aplicativos e deseja usar a compactação para o mesmo pacote, deverá alterar as versões dos pacotes `code`, `config` e `data` para evitar a incompatibilidade de soma de verificação.</span><span class="sxs-lookup"><span data-stu-id="3cc08-160">If you copied an uncompressed version of your application package, and you want to use compression for the same package, you must change the versions of the `code`, `config`, and `data` packages to avoid checksum mismatch.</span></span> <span data-ttu-id="3cc08-161">Se os pacotes não forem alterados, em vez de alterar a versão, você poderá usar o [provisionamento de comparação](service-fabric-application-upgrade-advanced.md).</span><span class="sxs-lookup"><span data-stu-id="3cc08-161">If the packages are unchanged, instead of changing the version, you can use [diff provisioning](service-fabric-application-upgrade-advanced.md).</span></span> <span data-ttu-id="3cc08-162">Com essa opção, não inclua o pacote inalterado, mas apenas referencie-o no manifesto do serviço.</span><span class="sxs-lookup"><span data-stu-id="3cc08-162">With this option, do not include the unchanged package instead reference it from the service manifest.</span></span>

<span data-ttu-id="3cc08-163">Da mesma forma, se você carregou uma versão compactada do pacote e deseja usar um pacote descompactado, é necessário atualizar as versões para evitar a incompatibilidade da soma de verificação.</span><span class="sxs-lookup"><span data-stu-id="3cc08-163">Similarly, if you uploaded a compressed version of the package and you want to use an uncompressed package, you must update the versions to avoid the checksum mismatch.</span></span>

<span data-ttu-id="3cc08-164">O pacote agora é empacotado corretamente, validado e compactado (se necessário), para que esteja pronto para [implantação](service-fabric-deploy-remove-applications.md) em um ou mais clusters do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="3cc08-164">The package is now packaged correctly, validated, and compressed (if needed), so it is ready for [deployment](service-fabric-deploy-remove-applications.md) to one or more Service Fabric clusters.</span></span>

### <a name="compress-packages-when-deploying-using-visual-studio"></a><span data-ttu-id="3cc08-165">Compactar pacotes durante a implantação usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3cc08-165">Compress packages when deploying using Visual Studio</span></span>
<span data-ttu-id="3cc08-166">Você pode instruir o Visual Studio para compactar os pacotes em implantação, adicionando o elemento `CopyPackageParameters` em seu perfil de publicação e definir o atributo `CompressPackage` como `true`.</span><span class="sxs-lookup"><span data-stu-id="3cc08-166">You can instruct Visual Studio to compress packages on deployment, by adding the `CopyPackageParameters` element to your publish profile, and set the `CompressPackage` attribute to `true`.</span></span>

``` xml
    <PublishProfile xmlns="http://schemas.microsoft.com/2015/05/fabrictools">
        <ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com" />
        <ApplicationParameterFile Path="..\ApplicationParameters\Cloud.xml" />
        <CopyPackageParameters CompressPackage="true"/>
    </PublishProfile>
```

## <a name="next-steps"></a><span data-ttu-id="3cc08-167">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3cc08-167">Next steps</span></span>
<span data-ttu-id="3cc08-168">[Implantar e remover aplicativos][10] descreve como usar o PowerShell para gerenciar instâncias do aplicativo</span><span class="sxs-lookup"><span data-stu-id="3cc08-168">[Deploy and remove applications][10] describes how to use PowerShell to manage application instances</span></span>

<span data-ttu-id="3cc08-169">[Gerenciamento de parâmetros do aplicativo para vários ambientes][11] descreve como configurar os parâmetros e variáveis de ambiente para diferentes instâncias do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3cc08-169">[Managing application parameters for multiple environments][11] describes how to configure parameters and environment variables for different application instances.</span></span>

<span data-ttu-id="3cc08-170">[Configurar políticas de segurança para seu aplicativo][12] descreve como executar serviços sob políticas de segurança para restringir o acesso.</span><span class="sxs-lookup"><span data-stu-id="3cc08-170">[Configure security policies for your application][12] describes how to run services under security policies to restrict access.</span></span>

<!--Image references-->
[vs-package-command]: ./media/service-fabric-package-apps/vs-package-command.png

<!--Link references--In actual articles, you only need a single period before the slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
