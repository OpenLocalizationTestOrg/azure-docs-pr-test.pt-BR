---
title: aaaDeploy um aplicativo Node. js que usa o MongoDB | Microsoft Docs
description: "Instruções passo a passo sobre como toopackage vários cluster convidado do executáveis toodeploy tooan Azure Service Fabric"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: b76bb756-c1ba-49f9-9666-e9807cf8f92f
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: msfussell;mikhegn
ms.openlocfilehash: 2775080f0d9d42d6ba15cca911e23067106be26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-multiple-guest-executables"></a><span data-ttu-id="70c0f-103">Implantar vários executáveis de convidado</span><span class="sxs-lookup"><span data-stu-id="70c0f-103">Deploy multiple guest executables</span></span>
<span data-ttu-id="70c0f-104">Este artigo mostra como toopackage e implantar várias tooAzure de executáveis de convidado do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="70c0f-104">This article shows how toopackage and deploy multiple guest executables tooAzure Service Fabric.</span></span> <span data-ttu-id="70c0f-105">Para criar e implantar um único pacote de malha do serviço, leia como muito[implantar um tooService executável de convidado malha](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="70c0f-105">For building and deploying a single Service Fabric package read how too[deploy a guest executable tooService Fabric](service-fabric-deploy-existing-app.md).</span></span>

<span data-ttu-id="70c0f-106">Embora este passo a passo mostra como toodeploy um aplicativo com um front-end de Node. js que usa o MongoDB como repositório de dados hello, você pode aplicar tooany aplicativo hello etapas tem dependências em outro aplicativo.</span><span class="sxs-lookup"><span data-stu-id="70c0f-106">While this walkthrough shows how toodeploy an application with a Node.js front end that uses MongoDB as hello data store, you can apply hello steps tooany application that has dependencies on another application.</span></span>   

<span data-ttu-id="70c0f-107">Você pode usar o Visual Studio tooproduce Olá pacote de aplicativo que contém vários executáveis de convidado.</span><span class="sxs-lookup"><span data-stu-id="70c0f-107">You can use Visual Studio tooproduce hello application package that contains multiple guest executables.</span></span> <span data-ttu-id="70c0f-108">Consulte [toopackage com o Visual Studio um aplicativo existente](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="70c0f-108">See [Using Visual Studio toopackage an existing application](service-fabric-deploy-existing-app.md).</span></span> <span data-ttu-id="70c0f-109">Após ter adicionado o executável de convidado primeiro hello, clique com botão direito no projeto de aplicativo hello e selecione Olá **Adicionar -> serviço de malha do novo serviço** tooadd Olá segunda convidado projeto executável toohello solução.</span><span class="sxs-lookup"><span data-stu-id="70c0f-109">After you have added hello first guest executable, right click on hello application project and select hello **Add->New Service Fabric service** tooadd hello second guest executable project toohello solution.</span></span> <span data-ttu-id="70c0f-110">Observação: Se você escolher a fonte de saudação toolink em Olá projeto do Visual Studio, criação de solução do Visual Studio Olá, garantirá que seu pacote de aplicativo é o toodate com alterações feitas na fonte de saudação.</span><span class="sxs-lookup"><span data-stu-id="70c0f-110">Note: If you choose toolink hello source in hello Visual Studio project, building hello Visual Studio solution, will make sure that your application package is up toodate with changes in hello source.</span></span> 

## <a name="samples"></a><span data-ttu-id="70c0f-111">Exemplos</span><span class="sxs-lookup"><span data-stu-id="70c0f-111">Samples</span></span>
* [<span data-ttu-id="70c0f-112">Exemplo de empacotamento e implantação de um executável convidado</span><span class="sxs-lookup"><span data-stu-id="70c0f-112">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="70c0f-113">Exemplo de dois convidado executáveis (c# e nodejs) se comunicar por meio do serviço de nomenclatura hello usando REST</span><span class="sxs-lookup"><span data-stu-id="70c0f-113">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="manually-package-hello-multiple-guest-executable-application"></a><span data-ttu-id="70c0f-114">Manualmente o pacote hello vários aplicativo executável de convidado</span><span class="sxs-lookup"><span data-stu-id="70c0f-114">Manually package hello multiple guest executable application</span></span>
<span data-ttu-id="70c0f-115">Como alternativa, você pode empacotar manualmente executável de convidado hello.</span><span class="sxs-lookup"><span data-stu-id="70c0f-115">Alternatively you can manually package hello guest executable.</span></span> <span data-ttu-id="70c0f-116">Para empacotamento manual de hello, este artigo usa a ferramenta de empacotamento do Service Fabric hello, está disponível em [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).</span><span class="sxs-lookup"><span data-stu-id="70c0f-116">For hello manual packaging, this article uses hello Service Fabric packaging tool, which is available at [http://aka.ms/servicefabricpacktool](http://aka.ms/servicefabricpacktool).</span></span>

### <a name="packaging-hello-nodejs-application"></a><span data-ttu-id="70c0f-117">Saudação de empacotamento aplicativo Node. js</span><span class="sxs-lookup"><span data-stu-id="70c0f-117">Packaging hello Node.js application</span></span>
<span data-ttu-id="70c0f-118">Este artigo pressupõe que o Node. js não está instalado em nós de Olá no cluster do Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="70c0f-118">This article assumes that Node.js is not installed on hello nodes in hello Service Fabric cluster.</span></span> <span data-ttu-id="70c0f-119">Como consequência, você precisa tooadd Node.exe toohello diretório de raiz do seu aplicativo de nó antes do empacotamento.</span><span class="sxs-lookup"><span data-stu-id="70c0f-119">As a consequence, you need tooadd Node.exe toohello root directory of your node application before packaging.</span></span> <span data-ttu-id="70c0f-120">estrutura de diretório de saudação do aplicativo do Node. js hello (usando a estrutura do web Express e o mecanismo de modelo Jade) deve ser semelhante toohello um abaixo:</span><span class="sxs-lookup"><span data-stu-id="70c0f-120">hello directory structure of hello Node.js application (using Express web framework and Jade template engine) should look similar toohello one below:</span></span>

```
|-- NodeApplication
    |-- bin
        |-- www
    |-- node_modules
        |-- .bin
        |-- express
        |-- jade
        |-- etc.
    |-- public
        |-- images
        |-- etc.
    |-- routes
        |-- index.js
        |-- users.js
    |-- views
        |-- index.jade
        |-- etc.
    |-- app.js
    |-- package.json
    |-- node.exe
```

<span data-ttu-id="70c0f-121">Como uma próxima etapa, você cria um pacote de aplicativo hello aplicativo Node. js.</span><span class="sxs-lookup"><span data-stu-id="70c0f-121">As a next step, you create an application package for hello Node.js application.</span></span> <span data-ttu-id="70c0f-122">código de saudação abaixo cria um pacote de aplicativo de malha do serviço que contém o aplicativo do hello Node. js.</span><span class="sxs-lookup"><span data-stu-id="70c0f-122">hello code below creates a Service Fabric application package that contains hello Node.js application.</span></span>

```
.\ServiceFabricAppPackageUtil.exe /source:'[yourdirectory]\MyNodeApplication' /target:'[yourtargetdirectory] /appname:NodeService /exe:'node.exe' /ma:'bin/www' /AppType:NodeAppType
```

<span data-ttu-id="70c0f-123">Abaixo está uma descrição dos parâmetros de saudação que estão sendo usadas:</span><span class="sxs-lookup"><span data-stu-id="70c0f-123">Below is a description of hello parameters that are being used:</span></span>

* <span data-ttu-id="70c0f-124">**/Source** pontos toohello diretório de aplicativo hello que deve ser empacotado.</span><span class="sxs-lookup"><span data-stu-id="70c0f-124">**/source** points toohello directory of hello application that should be packaged.</span></span>
* <span data-ttu-id="70c0f-125">**/Target** define Olá diretório no qual Olá pacote deve ser criado.</span><span class="sxs-lookup"><span data-stu-id="70c0f-125">**/target** defines hello directory in which hello package should be created.</span></span> <span data-ttu-id="70c0f-126">Este diretório tem toobe diferente saudação do diretório de origem.</span><span class="sxs-lookup"><span data-stu-id="70c0f-126">This directory has toobe different from hello source directory.</span></span>
* <span data-ttu-id="70c0f-127">**/appname** define o nome do aplicativo de saudação do aplicativo existente hello.</span><span class="sxs-lookup"><span data-stu-id="70c0f-127">**/appname** defines hello application name of hello existing application.</span></span> <span data-ttu-id="70c0f-128">É importante toounderstand que isso se traduz toohello nome do serviço no manifesto de saudação e não toohello nome do aplicativo de malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="70c0f-128">It's important toounderstand that this translates toohello service name in hello manifest, and not toohello Service Fabric application name.</span></span>
* <span data-ttu-id="70c0f-129">**/exe** define Olá executável que Service Fabric deve toolaunch, neste caso `node.exe`.</span><span class="sxs-lookup"><span data-stu-id="70c0f-129">**/exe** defines hello executable that Service Fabric is supposed toolaunch, in this case `node.exe`.</span></span>
* <span data-ttu-id="70c0f-130">**/ma** define o argumento de saudação que está sendo usado toolaunch Olá executável.</span><span class="sxs-lookup"><span data-stu-id="70c0f-130">**/ma** defines hello argument that is being used toolaunch hello executable.</span></span> <span data-ttu-id="70c0f-131">Como o Node. js não estiver instalado, do Service Fabric precisa de servidor de web toolaunch Olá Node. js executando `node.exe bin/www`.</span><span class="sxs-lookup"><span data-stu-id="70c0f-131">As Node.js is not installed, Service Fabric needs toolaunch hello Node.js web server by executing `node.exe bin/www`.</span></span>  <span data-ttu-id="70c0f-132">`/ma:'bin/www'`informa Olá empacotamento ferramenta toouse `bin/ma` como argumento de saudação para node.exe.</span><span class="sxs-lookup"><span data-stu-id="70c0f-132">`/ma:'bin/www'` tells hello packaging tool toouse `bin/ma` as hello argument for node.exe.</span></span>
* <span data-ttu-id="70c0f-133">**/ O tipo de aplicativo** define o nome do tipo de aplicativo hello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="70c0f-133">**/AppType** defines hello Service Fabric application type name.</span></span>

<span data-ttu-id="70c0f-134">Se você procurar o diretório toohello que foi especificado no parâmetro de /target hello, você pode ver que essa ferramenta Olá criou um pacote de malha do serviço totalmente funcional conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="70c0f-134">If you browse toohello directory that was specified in hello /target parameter, you can see that hello tool has created a fully functioning Service Fabric package as shown below:</span></span>

```
|--[yourtargetdirectory]
    |-- NodeApplication
        |-- C
              |-- bin
              |-- data
              |-- node_modules
              |-- public
              |-- routes
              |-- views
              |-- app.js
              |-- package.json
              |-- node.exe
        |-- config
              |--Settings.xml
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```
<span data-ttu-id="70c0f-135">Olá ServiceManifest.xml gerado agora tem uma seção que descreve como o servidor de web Node.js Olá deve ser iniciada, conforme mostrado no trecho de código Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="70c0f-135">hello generated ServiceManifest.xml now has a section that describes how hello Node.js web server should be launched, as shown in hello code snippet below:</span></span>

```xml
<CodePackage Name="C" Version="1.0">
    <EntryPoint>
        <ExeHost>
            <Program>node.exe</Program>
            <Arguments>'bin/www'</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
        </ExeHost>
    </EntryPoint>
</CodePackage>
```
<span data-ttu-id="70c0f-136">Neste exemplo, o servidor de web de Node. js Olá escuta tooport 3000, portanto, você precisa de informações de ponto de extremidade Olá tooupdate no arquivo ServiceManifest.xml de saudação conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="70c0f-136">In this sample, hello Node.js web server listens tooport 3000, so you need tooupdate hello endpoint information in hello ServiceManifest.xml file as shown below.</span></span>   

```xml
<Resources>
      <Endpoints>
         <Endpoint Name="NodeServiceEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
</Resources>
```
### <a name="packaging-hello-mongodb-application"></a><span data-ttu-id="70c0f-137">Saudação de empacotamento MongoDB aplicativo</span><span class="sxs-lookup"><span data-stu-id="70c0f-137">Packaging hello MongoDB application</span></span>
<span data-ttu-id="70c0f-138">Agora que você empacotar aplicativo do Node. js hello, você pode vá em frente e MongoDB do pacote.</span><span class="sxs-lookup"><span data-stu-id="70c0f-138">Now that you have packaged hello Node.js application, you can go ahead and package MongoDB.</span></span> <span data-ttu-id="70c0f-139">Como mencionado anteriormente, Olá etapas que você percorrer agora não são tooNode.js específico e MongoDB.</span><span class="sxs-lookup"><span data-stu-id="70c0f-139">As mentioned before, hello steps that you go through now are not specific tooNode.js and MongoDB.</span></span> <span data-ttu-id="70c0f-140">Na verdade, se aplicam a aplicativos tooall devem toobe reunido como um aplicativo de malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="70c0f-140">In fact, they apply tooall applications that are meant toobe packaged together as one Service Fabric application.</span></span>  

<span data-ttu-id="70c0f-141">toopackage MongoDB, você deseja toomake-se de que você empacotar Mongod.exe e Mongo.exe.</span><span class="sxs-lookup"><span data-stu-id="70c0f-141">toopackage MongoDB, you want toomake sure you package Mongod.exe and Mongo.exe.</span></span> <span data-ttu-id="70c0f-142">Ambos os binários estão localizados em Olá `bin` diretório de seu diretório de instalação do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="70c0f-142">Both binaries are located in hello `bin` directory of your MongoDB installation directory.</span></span> <span data-ttu-id="70c0f-143">estrutura de diretórios Olá parece semelhante toohello um abaixo.</span><span class="sxs-lookup"><span data-stu-id="70c0f-143">hello directory structure looks similar toohello one below.</span></span>

```
|-- MongoDB
    |-- bin
        |-- mongod.exe
        |-- mongo.exe
        |-- anybinary.exe
```
<span data-ttu-id="70c0f-144">Service Fabric precisa toostart MongoDB com um toohello semelhante do comando um abaixo, para que você precise Olá toouse `/ma` parâmetro ao empacotar o MongoDB.</span><span class="sxs-lookup"><span data-stu-id="70c0f-144">Service Fabric needs toostart MongoDB with a command similar toohello one below, so you need toouse hello `/ma` parameter when packaging MongoDB.</span></span>

```
mongod.exe --dbpath [path toodata]
```
> [!NOTE]
> <span data-ttu-id="70c0f-145">dados de Olá não estão sendo preservados no caso de saudação de uma falha de nó se você colocar o diretório de dados do MongoDB Olá no diretório local de saudação do nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="70c0f-145">hello data is not being preserved in hello case of a node failure if you put hello MongoDB data directory on hello local directory of hello node.</span></span> <span data-ttu-id="70c0f-146">Você deve usar o armazenamento durável ou implementar um conjunto ordem tooprevent perda de dados de réplicas do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="70c0f-146">You should either use durable storage or implement a MongoDB replica set in order tooprevent data loss.</span></span>  
>
>

<span data-ttu-id="70c0f-147">No shell de comando do PowerShell ou hello, podemos executar a ferramenta de empacotamento de Olá com hello parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="70c0f-147">In PowerShell or hello command shell, we run hello packaging tool with hello following parameters:</span></span>

```
.\ServiceFabricAppPackageUtil.exe /source: [yourdirectory]\MongoDB' /target:'[yourtargetdirectory]' /appname:MongoDB /exe:'bin\mongod.exe' /ma:'--dbpath [path toodata]' /AppType:NodeAppType
```

<span data-ttu-id="70c0f-148">No pacote de aplicativo do Service Fabric tooyour do pedido tooadd MongoDB, você precisa toomake-se de que o parâmetro hello /target pontos toohello mesmo diretório que já contém o manifesto do aplicativo hello junto com o aplicativo do hello Node. js.</span><span class="sxs-lookup"><span data-stu-id="70c0f-148">In order tooadd MongoDB tooyour Service Fabric application package, you need toomake sure that hello /target parameter points toohello same directory that already contains hello application manifest along with hello Node.js application.</span></span> <span data-ttu-id="70c0f-149">Você também precisa toomake-se de que você está usando Olá mesmo nome ApplicationType.</span><span class="sxs-lookup"><span data-stu-id="70c0f-149">You also need toomake sure that you are using hello same ApplicationType name.</span></span>

<span data-ttu-id="70c0f-150">Vamos procurar o diretório toohello e examinar qual ferramenta Olá criou.</span><span class="sxs-lookup"><span data-stu-id="70c0f-150">Let's browse toohello directory and examine what hello tool has created.</span></span>

```
|--[yourtargetdirectory]
    |-- MyNodeApplication
    |-- MongoDB
        |-- C
            |--bin
                |-- mongod.exe
                |-- mongo.exe
                |-- etc.
        |-- config
            |--Settings.xml
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```
<span data-ttu-id="70c0f-151">Como você pode ver, ferramenta Olá adicionado um novo diretório de toohello de pasta, MongoDB, que contém os binários do MongoDB hello.</span><span class="sxs-lookup"><span data-stu-id="70c0f-151">As you can see, hello tool added a new folder, MongoDB, toohello directory that contains hello MongoDB binaries.</span></span> <span data-ttu-id="70c0f-152">Se você abrir Olá `ApplicationManifest.xml` arquivo, você pode ver que o pacote hello agora contém o aplicativo de Node. js hello e MongoDB.</span><span class="sxs-lookup"><span data-stu-id="70c0f-152">If you open hello `ApplicationManifest.xml` file, you can see that hello package now contains both hello Node.js application and MongoDB.</span></span> <span data-ttu-id="70c0f-153">Olá código a seguir mostra o hello conteúdo saudação do manifesto do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="70c0f-153">hello code below shows hello content of hello application manifest.</span></span>

```xml
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyNodeApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MongoDB" ServiceManifestVersion="1.0" />
   </ServiceManifestImport>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeService" ServiceManifestVersion="1.0" />
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="MongoDBService">
         <StatelessService ServiceTypeName="MongoDB">
            <SingletonPartition />
         </StatelessService>
      </Service>
      <Service Name="NodeServiceService">
         <StatelessService ServiceTypeName="NodeService">
            <SingletonPartition />
         </StatelessService>
      </Service>
   </DefaultServices>
</ApplicationManifest>  
```

### <a name="publishing-hello-application"></a><span data-ttu-id="70c0f-154">Aplicativo de publicação hello</span><span class="sxs-lookup"><span data-stu-id="70c0f-154">Publishing hello application</span></span>
<span data-ttu-id="70c0f-155">Olá última etapa é toopublish Olá aplicativo toohello Service Fabric cluster local usando scripts do PowerShell Olá abaixo:</span><span class="sxs-lookup"><span data-stu-id="70c0f-155">hello last step is toopublish hello application toohello local Service Fabric cluster by using hello PowerShell scripts below:</span></span>

```
Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath '[yourtargetdirectory]' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'NodeAppType'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'NodeAppType'

New-ServiceFabricApplication -ApplicationName 'fabric:/NodeApp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0  
```

<span data-ttu-id="70c0f-156">Após o aplicativo hello cluster local toohello publicado com êxito, é possível acessar o aplicativo de Node. js de saudação na porta de saudação que é inserido no manifesto do serviço de saudação do aplicativo de Node. js hello – por exemplo, http://localhost:3000.</span><span class="sxs-lookup"><span data-stu-id="70c0f-156">Once hello application is successfully published toohello local cluster, you can access hello Node.js application on hello port that we have entered in hello service manifest of hello Node.js application--for example http://localhost:3000.</span></span>

<span data-ttu-id="70c0f-157">Neste tutorial, você viu como tooeasily pacote dois aplicativos existentes como um aplicativo de malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="70c0f-157">In this tutorial, you have seen how tooeasily package two existing applications as one Service Fabric application.</span></span> <span data-ttu-id="70c0f-158">Você também aprendeu como toodeploy-tooService malha para que ele pode se beneficiar Olá de alguns recursos de malha do serviço, como integração alta disponibilidade e integridade do sistema.</span><span class="sxs-lookup"><span data-stu-id="70c0f-158">You have also learned how toodeploy it tooService Fabric so that it can benefit from some of hello Service Fabric features, such as high availability and health system integration.</span></span>


## <a name="adding-more-guest-executables-tooan-existing-application-using-yeoman-on-linux"></a><span data-ttu-id="70c0f-159">Adicionando mais convidado executáveis tooan aplicativo existente usando Yeoman no Linux</span><span class="sxs-lookup"><span data-stu-id="70c0f-159">Adding more guest executables tooan existing application using Yeoman on Linux</span></span>

<span data-ttu-id="70c0f-160">tooadd outro tooan aplicativo de serviço já criado usando `yo`, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="70c0f-160">tooadd another service tooan application already created using `yo`, perform hello following steps:</span></span> 
1. <span data-ttu-id="70c0f-161">Alterar o diretório raiz de toohello do aplicativo existente hello.</span><span class="sxs-lookup"><span data-stu-id="70c0f-161">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="70c0f-162">Por exemplo, `cd ~/YeomanSamples/MyApplication`, se `MyApplication` é um aplicativo hello criado por Yeoman.</span><span class="sxs-lookup"><span data-stu-id="70c0f-162">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="70c0f-163">Execute `yo azuresfguest:AddService` e fornecer detalhes necessários hello.</span><span class="sxs-lookup"><span data-stu-id="70c0f-163">Run `yo azuresfguest:AddService` and provide hello necessary details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70c0f-164">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="70c0f-164">Next steps</span></span>
* <span data-ttu-id="70c0f-165">Saiba mais sobre como implantar contêineres com a [Visão geral de contêineres e do Service Fabric](service-fabric-containers-overview.md)</span><span class="sxs-lookup"><span data-stu-id="70c0f-165">Learn about deploying containers with [Service Fabric and containers overview](service-fabric-containers-overview.md)</span></span>
* [<span data-ttu-id="70c0f-166">Exemplo de empacotamento e implantação de um executável convidado</span><span class="sxs-lookup"><span data-stu-id="70c0f-166">Sample for packaging and deploying a guest executable</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="70c0f-167">Exemplo de dois convidado executáveis (c# e nodejs) se comunicar por meio do serviço de nomenclatura hello usando REST</span><span class="sxs-lookup"><span data-stu-id="70c0f-167">Sample of two guest executables (C# and nodejs) communicating via hello Naming service using REST</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
