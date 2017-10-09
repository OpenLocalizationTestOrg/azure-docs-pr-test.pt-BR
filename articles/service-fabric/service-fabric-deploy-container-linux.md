---
title: "aaaService malha e implantar contêineres do Linux | Microsoft Docs"
description: "Serviço de malha e hello usam contêineres toodeploy microsserviço aplicativos do Linux. Este artigo descreve recursos de saudação do Service Fabric fornece para contêineres e como toodeploy um contêiner de Linux a imagem em um cluster"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 4ba99103-6064-429d-ba17-82861b6ddb11
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: msfussell
ms.openlocfilehash: e28f99a145b0594d871b0ec0566233a7ad235ce8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-linux-container-tooservice-fabric"></a><span data-ttu-id="1e3ee-104">Implantar um contêiner de Linux tooService malha</span><span class="sxs-lookup"><span data-stu-id="1e3ee-104">Deploy a Linux container tooService Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1e3ee-105">Implantar contêiner do Windows</span><span class="sxs-lookup"><span data-stu-id="1e3ee-105">Deploy Windows Container</span></span>](service-fabric-deploy-container.md)
> * [<span data-ttu-id="1e3ee-106">Implantar contêiner do Linux</span><span class="sxs-lookup"><span data-stu-id="1e3ee-106">Deploy Linux Container</span></span>](service-fabric-deploy-container-linux.md)
>
>

<span data-ttu-id="1e3ee-107">Este artigo orienta a criação de serviços contentorizados em contêineres do Docker no Linux.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-107">This article walks you through building containerized services in Docker containers on Linux.</span></span>

<span data-ttu-id="1e3ee-108">O Service Fabric tem vários recursos de contêiner que ajudam na compilação de aplicativos que são compostos por microsserviços que estão em contêineres.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-108">Service Fabric has several container capabilities that help you with building applications that are composed of microservices that are containerized.</span></span> <span data-ttu-id="1e3ee-109">Esses serviços são chamados de serviços em contêineres.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-109">These services are called containerized services.</span></span>

<span data-ttu-id="1e3ee-110">recursos de saudação incluem;</span><span class="sxs-lookup"><span data-stu-id="1e3ee-110">hello capabilities include;</span></span>

* <span data-ttu-id="1e3ee-111">Implantação e ativação de imagens de contêiner</span><span class="sxs-lookup"><span data-stu-id="1e3ee-111">Container image deployment and activation</span></span>
* <span data-ttu-id="1e3ee-112">Governança de recursos</span><span class="sxs-lookup"><span data-stu-id="1e3ee-112">Resource governance</span></span>
* <span data-ttu-id="1e3ee-113">Autenticação do repositório</span><span class="sxs-lookup"><span data-stu-id="1e3ee-113">Repository authentication</span></span>
* <span data-ttu-id="1e3ee-114">Mapeamento de porta de toohost de porta de contêiner</span><span class="sxs-lookup"><span data-stu-id="1e3ee-114">Container port toohost port mapping</span></span>
* <span data-ttu-id="1e3ee-115">Descoberta e comunicação de contêiner para contêiner</span><span class="sxs-lookup"><span data-stu-id="1e3ee-115">Container-to-container discovery and communication</span></span>
* <span data-ttu-id="1e3ee-116">Capacidade tooconfigure e definir variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="1e3ee-116">Ability tooconfigure and set environment variables</span></span>

## <a name="packaging-a-docker-container-with-yeoman"></a><span data-ttu-id="1e3ee-117">Empacotando um contêiner do Docker com yeoman</span><span class="sxs-lookup"><span data-stu-id="1e3ee-117">Packaging a docker container with yeoman</span></span>
<span data-ttu-id="1e3ee-118">Ao empacotar um contêiner no Linux, você pode escolher qualquer toouse um modelo de yeoman ou [criar manualmente o pacote de aplicativo hello](#manually).</span><span class="sxs-lookup"><span data-stu-id="1e3ee-118">When packaging a container on Linux, you can choose either toouse a yeoman template or [create hello application package manually](#manually).</span></span>

<span data-ttu-id="1e3ee-119">Um aplicativo de malha do serviço pode conter um ou mais contêineres, cada um com uma função específica no fornecimento de funcionalidade do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-119">A Service Fabric application can contain one or more containers, each with a specific role in delivering hello application's functionality.</span></span> <span data-ttu-id="1e3ee-120">Olá SDK do Service Fabric para Linux inclui um [Yeoman](http://yeoman.io/) gerador que torna mais fácil toocreate seu aplicativo e adicione uma imagem de contêiner.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-120">hello Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy toocreate your application and add a container image.</span></span> <span data-ttu-id="1e3ee-121">Vamos usar Yeoman toocreate chamado de um aplicativo com um único contêiner de Docker *SimpleContainerApp*.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-121">Let's use Yeoman toocreate an application with a single Docker container called *SimpleContainerApp*.</span></span> <span data-ttu-id="1e3ee-122">Você pode adicionar mais serviços mais tarde editando os arquivos de manifesto Olá gerado.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-122">You can add more services later by editing hello generated manifest files.</span></span>

## <a name="install-docker-on-your-development-box"></a><span data-ttu-id="1e3ee-123">Instalar o Docker em sua caixa de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="1e3ee-123">Install Docker on your development box</span></span>

<span data-ttu-id="1e3ee-124">A seguir Olá execução comandos docker tooinstall na caixa de desenvolvimento do Linux (se você estiver usando a imagem vagrant Olá no OSX, docker já está instalado):</span><span class="sxs-lookup"><span data-stu-id="1e3ee-124">Run hello following commands tooinstall docker on your Linux development box (if you are using hello vagrant image on OSX, docker is already installed):</span></span>

```bash
    sudo apt-get install wget
    wget -qO- https://get.docker.io/ | sh
```

## <a name="create-hello-application"></a><span data-ttu-id="1e3ee-125">Criar um aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="1e3ee-125">Create hello application</span></span>
1. <span data-ttu-id="1e3ee-126">Em um terminal, digite `yo azuresfcontainer`.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-126">In a terminal, type `yo azuresfcontainer`.</span></span>
2. <span data-ttu-id="1e3ee-127">Dê um nome para o seu aplicativo, por exemplo, mycontainerap</span><span class="sxs-lookup"><span data-stu-id="1e3ee-127">Name your application - for example, mycontainerap</span></span>
3. <span data-ttu-id="1e3ee-128">Forneça a URL de saudação para imagem de contêiner de saudação de um repositório DockerHub.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-128">Provide hello URL for hello container image from a DockerHub repo.</span></span> <span data-ttu-id="1e3ee-129">Olá imagem parâmetro usa Olá formulário [repositório] / [nome da imagem]</span><span class="sxs-lookup"><span data-stu-id="1e3ee-129">hello image parameter takes hello form [repo]/[image name]</span></span>
4. <span data-ttu-id="1e3ee-130">Se Olá imagem não tiver um carga de trabalho-ponto de entrada definido, você precisará tooexplicitly especificar comandos de entrada com um conjunto delimitado por vírgulas de comandos toorun Olá contêiner, que manterá o contêiner de saudação em execução após a inicialização.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-130">If hello image does not have a workload entry-point defined, then you need tooexplicitly specify input commands with a comma-delimited set of commands toorun inside hello container, which will keep hello container running after startup.</span></span>

![Gerador de Yeoman do Service Fabric para contêineres][sf-yeoman]

## <a name="deploy-hello-application"></a><span data-ttu-id="1e3ee-132">Implantar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="1e3ee-132">Deploy hello application</span></span>

### <a name="using-xplat-cli"></a><span data-ttu-id="1e3ee-133">Usando a CLI XPlat</span><span class="sxs-lookup"><span data-stu-id="1e3ee-133">Using XPlat CLI</span></span>
<span data-ttu-id="1e3ee-134">Depois que o aplicativo hello é criado, você pode implantar toohello cluster local usando Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-134">Once hello application is built, you can deploy it toohello local cluster using hello Azure CLI.</span></span>

1. <span data-ttu-id="1e3ee-135">Conecte-se toohello cluster de malha do serviço local.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-135">Connect toohello local Service Fabric cluster.</span></span>

    ```bash
    azure servicefabric cluster connect
    ```

2. <span data-ttu-id="1e3ee-136">Olá Use o script de instalação fornecidas no hello modelo toocopy aplicativo hello pacote repositório de imagens do cluster toohello, registrar o tipo de aplicativo hello e criar uma instância do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-136">Use hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

    ```bash
    ./install.sh
    ```

3. <span data-ttu-id="1e3ee-137">Abra um navegador e navegue tooService Fabric Explorer no http://localhost:19080/Explorer (substitua localhost com IP privada Olá Olá VM se usando Vagrant no Mac OS X).</span><span class="sxs-lookup"><span data-stu-id="1e3ee-137">Open a browser and navigate tooService Fabric Explorer at http://localhost:19080/Explorer (replace localhost with hello private IP of hello VM if using Vagrant on Mac OS X).</span></span>
4. <span data-ttu-id="1e3ee-138">Expanda o nó de aplicativos hello e observe que agora há uma entrada para o tipo de aplicativo e outro para Olá primeira instância desse tipo.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-138">Expand hello Applications node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>
5. <span data-ttu-id="1e3ee-139">Usar script de desinstalação Olá fornecido na instância de aplicativo hello modelo toodelete hello e cancelar o registro do tipo de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-139">Use hello uninstall script provided in hello template toodelete hello application instance and unregister hello application type.</span></span>

    ```bash
    ./uninstall.sh
    ```

### <a name="using-azure-cli-20"></a><span data-ttu-id="1e3ee-140">Usando a CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="1e3ee-140">Using Azure CLI 2.0</span></span>

<span data-ttu-id="1e3ee-141">Consulte o documento de referência de saudação sobre como gerenciar uma [ciclo de vida do aplicativo usando hello Azure CLI 2.0](service-fabric-application-lifecycle-azure-cli-2-0.md).</span><span class="sxs-lookup"><span data-stu-id="1e3ee-141">See hello reference doc on managing an [application life cycle using hello Azure CLI 2.0](service-fabric-application-lifecycle-azure-cli-2-0.md).</span></span>

<span data-ttu-id="1e3ee-142">Para um aplicativo de exemplo, [Olá check-out código do contêiner do Service Fabric amostras no GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="1e3ee-142">For an example application, [checkout hello Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>

## <a name="adding-more-services-tooan-existing-application"></a><span data-ttu-id="1e3ee-143">Adicionar mais serviços tooan aplicativo</span><span class="sxs-lookup"><span data-stu-id="1e3ee-143">Adding more services tooan existing application</span></span>

<span data-ttu-id="1e3ee-144">tooadd outro contêiner de serviço tooan aplicativo já criado usando `yo`, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1e3ee-144">tooadd another container service tooan application already created using `yo`, perform hello following steps:</span></span>

1. <span data-ttu-id="1e3ee-145">Alterar o diretório raiz de toohello do aplicativo existente hello.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-145">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="1e3ee-146">Por exemplo, `cd ~/YeomanSamples/MyApplication`, se `MyApplication` é um aplicativo hello criado por Yeoman.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-146">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="1e3ee-147">Execute o `yo azuresfcontainer:AddService`</span><span class="sxs-lookup"><span data-stu-id="1e3ee-147">Run `yo azuresfcontainer:AddService`</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a><span data-ttu-id="1e3ee-148">Empacotar e implantar manualmente uma imagem de contêiner</span><span class="sxs-lookup"><span data-stu-id="1e3ee-148">Manually package and deploy a container image</span></span>
<span data-ttu-id="1e3ee-149">processo de saudação do empacotamento manualmente um serviço em contêineres se baseia na Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1e3ee-149">hello process of manually packaging a containerized service is based on hello following steps:</span></span>

1. <span data-ttu-id="1e3ee-150">Publica Olá contêineres tooyour repositório.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-150">Publish hello containers tooyour repository.</span></span>
2. <span data-ttu-id="1e3ee-151">Crie estrutura de diretório do pacote de saudação.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-151">Create hello package directory structure.</span></span>
3. <span data-ttu-id="1e3ee-152">Edite o arquivo de manifesto de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-152">Edit hello service manifest file.</span></span>
4. <span data-ttu-id="1e3ee-153">Edite o arquivo de manifesto de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-153">Edit hello application manifest file.</span></span>

## <a name="deploy-and-activate-a-container-image"></a><span data-ttu-id="1e3ee-154">Implantar e ativar uma imagem de contêiner</span><span class="sxs-lookup"><span data-stu-id="1e3ee-154">Deploy and activate a container image</span></span>
<span data-ttu-id="1e3ee-155">Em Olá Service Fabric [modelo de aplicativo](service-fabric-application-model.md), um contêiner representa um host de aplicativo no qual o serviço várias réplicas são colocadas.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-155">In hello Service Fabric [application model](service-fabric-application-model.md), a container represents an application host in which multiple service replicas are placed.</span></span> <span data-ttu-id="1e3ee-156">toodeploy e ativar um contêiner, um nome de saudação put da imagem de contêiner de saudação em um `ContainerHost` elemento no manifesto do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-156">toodeploy and activate a container, put hello name of hello container image into a `ContainerHost` element in hello service manifest.</span></span>

<span data-ttu-id="1e3ee-157">No manifesto do serviço hello, adicione um `ContainerHost` para o ponto de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-157">In hello service manifest, add a `ContainerHost` for hello entry point.</span></span> <span data-ttu-id="1e3ee-158">Em seguida, o conjunto de saudação `ImageName` toobe nome de saudação do repositório de contêiner hello e imagem.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-158">Then set hello `ImageName` toobe hello name of hello container repository and image.</span></span> <span data-ttu-id="1e3ee-159">Olá, manifesto parcial a seguir mostra um exemplo de como o contêiner de saudação toodeploy chamado `myimage:v1` de um repositório chamado `myrepo`:</span><span class="sxs-lookup"><span data-stu-id="1e3ee-159">hello following partial manifest shows an example of how toodeploy hello container called `myimage:v1` from a repository called `myrepo`:</span></span>

```xml
    <CodePackage Name="Code" Version="1.0">
        <EntryPoint>
          <ContainerHost>
            <ImageName>myrepo/myimage:v1</ImageName>
            <Commands></Commands>
          </ContainerHost>
        </EntryPoint>
    </CodePackage>
```

<span data-ttu-id="1e3ee-160">Você pode fornecer entrada de comandos, especificando Olá opcional `Commands` elemento com um conjunto delimitado por vírgulas de comandos toorun dentro do contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-160">You can provide input commands by specifying hello optional `Commands` element with a comma-delimited set of commands toorun inside hello container.</span></span>

> [!NOTE]
> <span data-ttu-id="1e3ee-161">Se Olá imagem não tiver um carga de trabalho-ponto de entrada definido, você precisará tooexplicitly especificar entrados comandos dentro `Commands` elemento com um conjunto delimitado por vírgulas de comandos toorun Olá contêiner, que manterá o contêiner de saudação em execução inicialização.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-161">If hello image does not have a workload entry-point defined, then you need tooexplicitly specify input commands inside `Commands` element with a comma-delimited set of commands toorun inside hello container, which will keep hello container running after startup.</span></span>

## <a name="understand-resource-governance"></a><span data-ttu-id="1e3ee-162">Compreender a governança de recursos</span><span class="sxs-lookup"><span data-stu-id="1e3ee-162">Understand resource governance</span></span>
<span data-ttu-id="1e3ee-163">Governança de recursos é um recurso de contêiner de saudação que restringe os recursos de Olá Olá contêiner pode usar no host de saudação.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-163">Resource governance is a capability of hello container that restricts hello resources that hello container can use on hello host.</span></span> <span data-ttu-id="1e3ee-164">Olá `ResourceGovernancePolicy`, que é especificado no manifesto de aplicativo hello é usado toodeclare limites de recurso para um pacote de código de serviço.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-164">hello `ResourceGovernancePolicy`, which is specified in hello application manifest is used toodeclare resource limits for a service code package.</span></span> <span data-ttu-id="1e3ee-165">Limites de recursos podem ser definidos para Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="1e3ee-165">Resource limits can be set for hello following resources:</span></span>

* <span data-ttu-id="1e3ee-166">Memória</span><span class="sxs-lookup"><span data-stu-id="1e3ee-166">Memory</span></span>
* <span data-ttu-id="1e3ee-167">MemorySwap</span><span class="sxs-lookup"><span data-stu-id="1e3ee-167">MemorySwap</span></span>
* <span data-ttu-id="1e3ee-168">CpuShares (peso relativo da CPU)</span><span class="sxs-lookup"><span data-stu-id="1e3ee-168">CpuShares (CPU relative weight)</span></span>
* <span data-ttu-id="1e3ee-169">MemoryReservationInMB</span><span class="sxs-lookup"><span data-stu-id="1e3ee-169">MemoryReservationInMB</span></span>  
* <span data-ttu-id="1e3ee-170">BlkioWeight (peso relativo do BlockIO).</span><span class="sxs-lookup"><span data-stu-id="1e3ee-170">BlkioWeight (BlockIO relative weight).</span></span>

> [!NOTE]
> <span data-ttu-id="1e3ee-171">Em uma versão futura, será incluído suporte para especificar limites de E/S de um bloco específico, como IOPs, leitura/gravação de BPS e outros.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-171">In a future release, support for specifying specific block IO limits such as IOPs, read/write BPS, and others will be included.</span></span>
>
>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ResourceGovernancePolicy CodePackageRef="FrontendService.Code" CpuShares="500"
            MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
        </Policies>
    </ServiceManifestImport>
```

## <a name="authenticate-a-repository"></a><span data-ttu-id="1e3ee-172">Autenticar um repositório</span><span class="sxs-lookup"><span data-stu-id="1e3ee-172">Authenticate a repository</span></span>
<span data-ttu-id="1e3ee-173">toodownload um contêiner, você pode ter um repositório de contêiner de toohello tooprovide credenciais de logon.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-173">toodownload a container, you might have tooprovide sign-in credentials toohello container repository.</span></span> <span data-ttu-id="1e3ee-174">Olá credenciais de logon, especificadas no manifesto de aplicativo hello, são usadas toospecify Olá entrar informações ou uma chave SSH, para baixar a imagem de contêiner de saudação do repositório de imagens de saudação.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-174">hello sign-in credentials, specified in hello application manifest, are used toospecify hello sign-in information, or SSH key, for downloading hello container image from hello image repository.</span></span> <span data-ttu-id="1e3ee-175">Olá, exemplo a seguir mostra uma conta chamada *TestUser* junto com a senha Olá em texto não criptografado (*não* recomendado):</span><span class="sxs-lookup"><span data-stu-id="1e3ee-175">hello following example shows an account called *TestUser* along with hello password in clear text (*not* recommended):</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="12345" PasswordEncrypted="false"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

<span data-ttu-id="1e3ee-176">É recomendável que você criptografe senha hello usando um certificado que tenha implantado toohello máquina.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-176">We recommend that you encrypt hello password by using a certificate that's deployed toohello machine.</span></span>

<span data-ttu-id="1e3ee-177">Olá, exemplo a seguir mostra uma conta chamada *TestUser*, onde a senha de saudação foi criptografada usando um certificado chamado *MyCert*.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-177">hello following example shows an account called *TestUser*, where hello password was encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="1e3ee-178">Você pode usar o hello `Invoke-ServiceFabricEncryptText` PowerShell comando toocreate Olá secreta de criptografia texto para senha hello.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-178">You can use hello `Invoke-ServiceFabricEncryptText` PowerShell command toocreate hello secret cipher text for hello password.</span></span> <span data-ttu-id="1e3ee-179">Para obter mais informações, consulte o artigo Olá [gerenciar segredos em aplicativos do Service Fabric](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="1e3ee-179">For more information, see hello article [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md).</span></span>

<span data-ttu-id="1e3ee-180">chave privada de saudação do certificado de saudação que usou a senha de saudação toodecrypt deve ser implantado toohello o computador local em um método fora de banda.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-180">hello private key of hello certificate that's used toodecrypt hello password must be deployed toohello local machine in an out-of-band method.</span></span> <span data-ttu-id="1e3ee-181">(No Azure, esse método é o Azure Resource Manager.) Em seguida, quando o Service Fabric implanta a máquina de toohello de pacote de serviço Olá, ele pode descriptografar o segredo de hello.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-181">(In Azure, this method is Azure Resource Manager.) Then, when Service Fabric deploys hello service package toohello machine, it can decrypt hello secret.</span></span> <span data-ttu-id="1e3ee-182">Usando o segredo Olá junto com o nome da conta Olá, em seguida, pode autenticar com o repositório de contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-182">By using hello secret along with hello account name, it can then authenticate with hello container repository.</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="[Put encrypted password here using MyCert certificate ]" PasswordEncrypted="true"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <a name="configure-container-port-to-host-port-mapping"></a><span data-ttu-id="1e3ee-183">Configurar mapeamento de porta do contêiner para o porta de host</span><span class="sxs-lookup"><span data-stu-id="1e3ee-183">Configure container port-to-host port mapping</span></span>
<span data-ttu-id="1e3ee-184">Você pode configurar toocommunicate de porta usada um host com o contêiner de saudação especificando um `PortBinding` no manifesto de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-184">You can configure a host port used toocommunicate with hello container by specifying a `PortBinding` in hello application manifest.</span></span> <span data-ttu-id="1e3ee-185">Olá porta associação mapas Olá porta toowhich Olá serviço está escutando em Olá contêiner tooa porta no host de saudação.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-185">hello port binding maps hello port toowhich hello service is listening inside hello container tooa port on hello host.</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <a name="configure-container-to-container-discovery-and-communication"></a><span data-ttu-id="1e3ee-186">Configurar descoberta e comunicação de contêiner para contêiner</span><span class="sxs-lookup"><span data-stu-id="1e3ee-186">Configure container-to-container discovery and communication</span></span>
<span data-ttu-id="1e3ee-187">Usando Olá `PortBinding` política, você pode mapear uma porta de contêiner tooan `Endpoint` no manifesto do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-187">By using hello `PortBinding` policy, you can map a container port tooan `Endpoint` in hello service manifest.</span></span> <span data-ttu-id="1e3ee-188">ponto de extremidade de Olá `Endpoint1` pode especificar uma porta fixa (por exemplo, a porta 80).</span><span class="sxs-lookup"><span data-stu-id="1e3ee-188">hello endpoint `Endpoint1` can specify a fixed port (for example, port 80).</span></span> <span data-ttu-id="1e3ee-189">Ele também não pode especificar nenhuma porta, caso em que uma porta aleatória do intervalo de portas de aplicativo do cluster Olá é escolhida para você.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-189">It can also specify no port at all, in which case a random port from hello cluster's application port range is chosen for you.</span></span>

<span data-ttu-id="1e3ee-190">Se você especificar um ponto de extremidade, usando Olá `Endpoint` marca no manifesto do serviço de saudação de um contêiner de convidado, o Service Fabric pode publicar automaticamente toohello esse ponto de extremidade Naming service.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-190">If you specify an endpoint, using hello `Endpoint` tag in hello service manifest of a guest container, Service Fabric can automatically publish this endpoint toohello Naming service.</span></span> <span data-ttu-id="1e3ee-191">Outros serviços que são executados no cluster hello, portanto, podem descobrir esse contêiner usando consultas REST Olá para resolver.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-191">Other services that are running in hello cluster can thus discover this container using hello REST queries for resolving.</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

<span data-ttu-id="1e3ee-192">Registrando Olá Naming service, você poderá facilmente fazer comunicação de contêiner para contêiner no código hello dentro de seu contêiner usando Olá [proxy reverso](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="1e3ee-192">By registering with hello Naming service, you can easily do container-to-container communication in hello code within your container by using hello [reverse proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="1e3ee-193">A comunicação é executada, fornecendo a porta de escuta Olá proxy reverso http e o nome de saudação do serviços de saudação que você deseja toocommunicate com como variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-193">Communication is performed by providing hello reverse proxy http listening port and hello name of hello services that you want toocommunicate with as environment variables.</span></span> <span data-ttu-id="1e3ee-194">Para obter mais informações, consulte Olá próxima seção.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-194">For more information, see hello next section.</span></span>

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="1e3ee-195">Configurar e definir as variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="1e3ee-195">Configure and set environment variables</span></span>
<span data-ttu-id="1e3ee-196">Variáveis de ambiente podem ser especificadas para cada pacote de códigos no manifesto do serviço hello, tanto para serviços que são implantados em contêineres ou para serviços que são implantados como executáveis processos/convidado.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-196">Environment variables can be specified for each code package in hello service manifest, both for services that are deployed in containers or for services that are deployed as processes/guest executables.</span></span> <span data-ttu-id="1e3ee-197">Esses valores de variáveis de ambiente podem ser substituídas especificamente no manifesto do aplicativo hello ou especificados durante a implantação como parâmetros de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-197">These environment variable values can be overridden specifically in hello application manifest or specified during deployment as application parameters.</span></span>

<span data-ttu-id="1e3ee-198">Olá, serviço manifesto trecho XML a seguir mostra um exemplo de como toospecify variáveis de ambiente para um pacote de código:</span><span class="sxs-lookup"><span data-stu-id="1e3ee-198">hello following service manifest XML snippet shows an example of how toospecify environment variables for a code package:</span></span>

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>a guest executable service in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
    </ServiceManifest>
```

<span data-ttu-id="1e3ee-199">Essas variáveis de ambiente podem ser substituídos no nível de manifesto de aplicativo hello:</span><span class="sxs-lookup"><span data-stu-id="1e3ee-199">These environment variables can be overridden at hello application manifest level:</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

<span data-ttu-id="1e3ee-200">No exemplo anterior de saudação, especificamos um valor explícito para Olá `HttpGateway` (19000), enquanto definimos Olá valor de variável de ambiente `BackendServiceName` parâmetro via Olá `[BackendSvc]` parâmetro de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-200">In hello previous example, we specified an explicit value for hello `HttpGateway` environment variable (19000), while we set hello value for `BackendServiceName` parameter via hello `[BackendSvc]` application parameter.</span></span> <span data-ttu-id="1e3ee-201">Essas configurações permitem que você valor Olá toospecify `BackendServiceName`quando você implanta o aplicativo hello e não tem um valor fixo no manifesto de saudação do valor.</span><span class="sxs-lookup"><span data-stu-id="1e3ee-201">These settings enable you toospecify hello value for `BackendServiceName`value when you deploy hello application and not have a fixed value in hello manifest.</span></span>

## <a name="complete-examples-for-application-and-service-manifest"></a><span data-ttu-id="1e3ee-202">Exemplos completos de aplicativo e manifesto do serviço</span><span class="sxs-lookup"><span data-stu-id="1e3ee-202">Complete examples for application and service manifest</span></span>

<span data-ttu-id="1e3ee-203">Aqui está um exemplo de manifesto de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="1e3ee-203">An example application manifest follows:</span></span>

```xml
    <ApplicationManifest ApplicationTypeName="SimpleContainerApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>A simple service container application</Description>
        <Parameters>
            <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
            <Parameter Name="BackEndSvcName" DefaultValue="bkend"></Parameter>
        </Parameters>
        <ServiceManifestImport>
            <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
            <EnvironmentOverrides CodePackageRef="FrontendService.Code">
                <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvcName]"/>
                <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
            </EnvironmentOverrides>
            <Policies>
                <ResourceGovernancePolicy CodePackageRef="Code" CpuShares="500" MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
                <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                    <RepositoryCredentials AccountName="username" Password="****" PasswordEncrypted="true"/>
                    <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
                </ContainerHostPolicies>
            </Policies>
        </ServiceManifestImport>
    </ApplicationManifest>
```

<span data-ttu-id="1e3ee-204">Um manifesto de serviço de exemplo (especificado na Olá precede o manifesto do aplicativo) a seguir:</span><span class="sxs-lookup"><span data-stu-id="1e3ee-204">An example service manifest (specified in hello preceding application manifest) follows:</span></span>

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description> A service that implements a stateless front end in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
        <ConfigPackage Name="FrontendService.Config" Version="1.0" />
        <DataPackage Name="FrontendService.Data" Version="1.0" />
        <Resources>
            <Endpoints>
                <Endpoint Name="Endpoint1" UriScheme="http" Port="80" Protocol="http"/>
            </Endpoints>
        </Resources>
    </ServiceManifest>
```

## <a name="next-steps"></a><span data-ttu-id="1e3ee-205">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1e3ee-205">Next steps</span></span>
<span data-ttu-id="1e3ee-206">Agora que você implantou um serviço em contêineres, saiba como toomanage seu ciclo de vida lendo [ciclo de vida do aplicativo de malha do serviço](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="1e3ee-206">Now that you have deployed a containerized service, learn how toomanage its lifecycle by reading [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span></span>

* [<span data-ttu-id="1e3ee-207">Visão geral do Service Fabric e contêineres</span><span class="sxs-lookup"><span data-stu-id="1e3ee-207">Overview of Service Fabric and containers</span></span>](service-fabric-containers-overview.md)
* [<span data-ttu-id="1e3ee-208">Interagir com clusters de malha do serviço usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="1e3ee-208">Interacting with Service Fabric clusters using hello Azure CLI</span></span>](service-fabric-azure-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-deploy-container-linux/sf-container-yeoman1.png

## <a name="related-articles"></a><span data-ttu-id="1e3ee-209">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="1e3ee-209">Related articles</span></span>

* [<span data-ttu-id="1e3ee-210">Introdução ao Service Fabric e a CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="1e3ee-210">Getting started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
* [<span data-ttu-id="1e3ee-211">Introdução à CLI XPlat do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1e3ee-211">Getting started with Service Fabric XPlat CLI</span></span>](service-fabric-azure-cli.md)
