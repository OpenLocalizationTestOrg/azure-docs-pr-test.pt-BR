---
title: "aaaService malha e implantar contêineres | Microsoft Docs"
description: "Service Fabric e hello o uso de aplicativos de microsserviço toodeploy contêineres. Este artigo descreve os recursos de saudação do Service Fabric fornece para contêineres e como toodeploy um contêiner do Windows da imagem em um cluster."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 799cc9ad-32fd-486e-a6b6-efff6b13622d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/16/2017
ms.author: msfussell
ms.openlocfilehash: 8b6540579641474f21b8712b56049c7d177bec26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-windows-container-tooservice-fabric"></a><span data-ttu-id="49650-104">Implantar um tooService de contêiner do Windows Fabric</span><span class="sxs-lookup"><span data-stu-id="49650-104">Deploy a Windows container tooService Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="49650-105">Implantar contêiner do Windows</span><span class="sxs-lookup"><span data-stu-id="49650-105">Deploy Windows Container</span></span>](service-fabric-deploy-container.md)
> * [<span data-ttu-id="49650-106">Implantar contêiner do Docker</span><span class="sxs-lookup"><span data-stu-id="49650-106">Deploy Docker Container</span></span>](service-fabric-deploy-container-linux.md)
> 
> 

<span data-ttu-id="49650-107">Este artigo orienta você pelo processo de saudação da criação de serviços em contêineres em contêineres do Windows.</span><span class="sxs-lookup"><span data-stu-id="49650-107">This article walks you through hello process of building containerized services in Windows containers.</span></span>

<span data-ttu-id="49650-108">O Service Fabric tem vários recursos que ajudam na criação de aplicativos compostos de microsserviços em execução em contêineres.</span><span class="sxs-lookup"><span data-stu-id="49650-108">Service Fabric has several capabilities that help you with building applications that are composed of microservices running inside containers.</span></span> 

<span data-ttu-id="49650-109">Olá recursos incluem:</span><span class="sxs-lookup"><span data-stu-id="49650-109">hello capabilities include:</span></span>

* <span data-ttu-id="49650-110">Implantação e ativação de imagens de contêiner</span><span class="sxs-lookup"><span data-stu-id="49650-110">Container image deployment and activation</span></span>
* <span data-ttu-id="49650-111">Governança de recursos</span><span class="sxs-lookup"><span data-stu-id="49650-111">Resource governance</span></span>
* <span data-ttu-id="49650-112">Autenticação do repositório</span><span class="sxs-lookup"><span data-stu-id="49650-112">Repository authentication</span></span>
* <span data-ttu-id="49650-113">Mapeamento de porta de contêiner para porta de host</span><span class="sxs-lookup"><span data-stu-id="49650-113">Container port-to-host port mapping</span></span>
* <span data-ttu-id="49650-114">Descoberta e comunicação de contêiner para contêiner</span><span class="sxs-lookup"><span data-stu-id="49650-114">Container-to-container discovery and communication</span></span>
* <span data-ttu-id="49650-115">Capacidade tooconfigure e definir variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="49650-115">Ability tooconfigure and set environment variables</span></span>

<span data-ttu-id="49650-116">Vamos ver como cada um dos recursos funciona quando você estiver Empacotando uma toobe de serviço em contêineres incluído em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="49650-116">Let's look at how each of capabilities works when you're packaging a containerized service toobe included in your application.</span></span>

## <a name="package-a-windows-container"></a><span data-ttu-id="49650-117">Empacotar um contêiner do Windows</span><span class="sxs-lookup"><span data-stu-id="49650-117">Package a Windows container</span></span>
<span data-ttu-id="49650-118">Ao empacotar um contêiner, você pode escolher toouse um modelo de projeto Visual Studio ou [criar manualmente o pacote de aplicativo hello](#manually).</span><span class="sxs-lookup"><span data-stu-id="49650-118">When you package a container, you can choose toouse either a Visual Studio project template or [create hello application package manually](#manually).</span></span>  <span data-ttu-id="49650-119">Quando você usa o Visual Studio, a estrutura do pacote de aplicativo hello e arquivos de manifesto são criados pelo modelo de projeto novo Olá para você.</span><span class="sxs-lookup"><span data-stu-id="49650-119">When you use Visual Studio, hello application package structure and manifest files are created by hello New Project template for you.</span></span>

> [!TIP]
> <span data-ttu-id="49650-120">toopackage de maneira mais fácil de saudação uma imagem de contêiner existente em um serviço é toouse Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="49650-120">hello easiest way toopackage an existing container image into a service is toouse Visual Studio.</span></span>

## <a name="use-visual-studio-toopackage-an-existing-container-image"></a><span data-ttu-id="49650-121">Use o Visual Studio toopackage uma imagem de contêiner existente</span><span class="sxs-lookup"><span data-stu-id="49650-121">Use Visual Studio toopackage an existing container image</span></span>
<span data-ttu-id="49650-122">O Visual Studio fornece uma estrutura de serviço toohelp de modelo de serviço é implantar um cluster do contêiner tooa Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="49650-122">Visual Studio provides a Service Fabric service template toohelp you deploy a container tooa Service Fabric cluster.</span></span>

1. <span data-ttu-id="49650-123">Escolha **Arquivo** > **Novo Projeto** e crie um aplicativo de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="49650-123">Choose **File** > **New Project**, and create a Service Fabric application.</span></span>
2. <span data-ttu-id="49650-124">Escolha **convidado contêiner** como modelo de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="49650-124">Choose **Guest Container** as hello service template.</span></span>
3. <span data-ttu-id="49650-125">Escolha **nome da imagem** e fornecer Olá caminho toohello imagem no repositório de contêiner.</span><span class="sxs-lookup"><span data-stu-id="49650-125">Choose **Image Name** and provide hello path toohello image in your container repository.</span></span> <span data-ttu-id="49650-126">Por exemplo, `myrepo/myimage:v1` em https://hub.docker.com</span><span class="sxs-lookup"><span data-stu-id="49650-126">For example, `myrepo/myimage:v1` in https://hub.docker.com</span></span>
4. <span data-ttu-id="49650-127">Dê um nome ao seu serviço e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="49650-127">Give your service a name, and click **OK**.</span></span>
5. <span data-ttu-id="49650-128">Se seu serviço em contêineres precisa de um ponto de extremidade de comunicação, agora você pode adicionar arquivos do tipo toohello ServiceManifest.xml, porta e protocolo de saudação.</span><span class="sxs-lookup"><span data-stu-id="49650-128">If your containerized service needs an endpoint for communication, you can now add hello protocol, port, and type toohello ServiceManifest.xml file.</span></span> <span data-ttu-id="49650-129">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="49650-129">For example:</span></span> 
     
    `<Endpoint Name="MyContainerServiceEndpoint" Protocol="http" Port="80" UriScheme="http" PathSuffix="myapp/" Type="Input" />`
    
    <span data-ttu-id="49650-130">Fornecendo Olá `UriScheme`, Service Fabric registra automaticamente o ponto de extremidade de contêiner de saudação com hello Naming Service, serviço de descoberta.</span><span class="sxs-lookup"><span data-stu-id="49650-130">By providing hello `UriScheme`, Service Fabric automatically registers hello container endpoint with hello Naming service for discoverability.</span></span> <span data-ttu-id="49650-131">porta Olá pode ser fixa (conforme mostrado no hello anterior exemplo) ou alocada dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="49650-131">hello port can either be fixed (as shown in hello preceding example) or dynamically allocated.</span></span> <span data-ttu-id="49650-132">Se você não especificar uma porta, ela é alocada dinamicamente do intervalo de portas de aplicativo hello (como acontece com qualquer serviço).</span><span class="sxs-lookup"><span data-stu-id="49650-132">If you don't specify a port, it is dynamically allocated from hello application port range (as would happen with any service).</span></span>
    <span data-ttu-id="49650-133">Você também precisa de mapeamento de porta tooconfigure Olá contêiner toohost especificando um `PortBinding` política no manifesto de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="49650-133">You also need tooconfigure hello container toohost port mapping by specifying a `PortBinding` policy in hello application manifest.</span></span> <span data-ttu-id="49650-134">Para obter mais informações, consulte [Configurar mapeamento de porta do contêiner toohost](#Portsection).</span><span class="sxs-lookup"><span data-stu-id="49650-134">For more information, see [Configure container toohost port mapping](#Portsection).</span></span>
6. <span data-ttu-id="49650-135">Se seu contêiner precisar de governança de recursos, adicione `ResourceGovernancePolicy`.</span><span class="sxs-lookup"><span data-stu-id="49650-135">If your container needs resource governance then add a `ResourceGovernancePolicy`.</span></span>
8. <span data-ttu-id="49650-136">Se o contêiner deve tooauthenticate com um repositório privado, em seguida, adicione `RepositoryCredentials`.</span><span class="sxs-lookup"><span data-stu-id="49650-136">If your container needs tooauthenticate with a private repository, then add `RepositoryCredentials`.</span></span>
7. <span data-ttu-id="49650-137">Se você estiver executando em um computador Windows Server 2016 com suporte de contêiner habilitado, você pode usar pacote de hello e publicar o cluster local da ação toodeploy tooyour.</span><span class="sxs-lookup"><span data-stu-id="49650-137">If you are running on a Windows Server 2016 machine with container support enabled, you can use hello package and publish action toodeploy tooyour local cluster.</span></span> 
8. <span data-ttu-id="49650-138">Quando estiver pronto, você pode publicar cluster remoto da saudação aplicativo tooa ou check-in de controle de toosource Olá solução.</span><span class="sxs-lookup"><span data-stu-id="49650-138">When ready, you can publish hello application tooa remote cluster or check in hello solution toosource control.</span></span> 

<span data-ttu-id="49650-139">Para obter um exemplo, a saudação de check-out [exemplos de código do contêiner do Service Fabric no GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="49650-139">For an example, checkout hello [Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>

## <a name="creating-a-windows-server-2016-cluster"></a><span data-ttu-id="49650-140">Criar um cluster do Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="49650-140">Creating a Windows Server 2016 cluster</span></span>
<span data-ttu-id="49650-141">toodeploy seu aplicativo em contêineres, você precisa toocreate habilitado de um cluster executando o Windows Server 2016 com suporte do contêiner.</span><span class="sxs-lookup"><span data-stu-id="49650-141">toodeploy your containerized application, you need toocreate a cluster running Windows Server 2016 with container support enabled.</span></span> <span data-ttu-id="49650-142">O cluster pode estar em execução localmente ou ser implantado por meio do Azure Resource Manager no Azure.</span><span class="sxs-lookup"><span data-stu-id="49650-142">Your cluster may be running locally, or deployed via Azure Resource Manager in Azure.</span></span> 

<span data-ttu-id="49650-143">toodeploy um cluster usando o Gerenciador de recursos do Azure, escolha Olá **Windows Server 2016 com contêineres** imagem opção no Azure.</span><span class="sxs-lookup"><span data-stu-id="49650-143">toodeploy a cluster using Azure Resource Manager, choose hello **Windows Server 2016 with Containers** image option in Azure.</span></span> <span data-ttu-id="49650-144">Consulte o artigo Olá [criar um cluster do Service Fabric usando o Gerenciador de recursos do Azure](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="49650-144">See hello article [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="49650-145">Certifique-se de que você use hello Azure Resource Manager configurações a seguir:</span><span class="sxs-lookup"><span data-stu-id="49650-145">Ensure that you use hello following Azure Resource Manager settings:</span></span>

```xml
"vmImageOffer": { "type": "string","defaultValue": "WindowsServer"     },
"vmImageSku": { "defaultValue": "2016-Datacenter-with-Containers","type": "string"     },
"vmImageVersion": { "defaultValue": "latest","type": "string"     },  
```
<span data-ttu-id="49650-146">Você também pode usar o hello [modelo de cinco nós do Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) toocreate um cluster.</span><span class="sxs-lookup"><span data-stu-id="49650-146">You can also use hello [Five Node Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) toocreate a cluster.</span></span> <span data-ttu-id="49650-147">Como alternativa, leia uma [postagem de blog](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) da comunidade sobre o uso de contêineres do Windows e do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="49650-147">Alternatively read a community [blog post](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) on using Service Fabric and Windows containers.</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a><span data-ttu-id="49650-148">Empacotar e implantar manualmente uma imagem de contêiner</span><span class="sxs-lookup"><span data-stu-id="49650-148">Manually package and deploy a container image</span></span>
<span data-ttu-id="49650-149">processo de saudação do empacotamento manualmente um serviço em contêineres se baseia na Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="49650-149">hello process of manually packaging a containerized service is based on hello following steps:</span></span>

1. <span data-ttu-id="49650-150">Publica Olá contêineres tooyour repositório.</span><span class="sxs-lookup"><span data-stu-id="49650-150">Publish hello containers tooyour repository.</span></span>
2. <span data-ttu-id="49650-151">Crie estrutura de diretório do pacote de saudação.</span><span class="sxs-lookup"><span data-stu-id="49650-151">Create hello package directory structure.</span></span>
3. <span data-ttu-id="49650-152">Edite o arquivo de manifesto de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="49650-152">Edit hello service manifest file.</span></span>
4. <span data-ttu-id="49650-153">Edite o arquivo de manifesto de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="49650-153">Edit hello application manifest file.</span></span>

## <a name="deploy-and-activate-a-container-image"></a><span data-ttu-id="49650-154">Implantar e ativar uma imagem de contêiner</span><span class="sxs-lookup"><span data-stu-id="49650-154">Deploy and activate a container image</span></span>
<span data-ttu-id="49650-155">Em Olá Service Fabric [modelo de aplicativo](service-fabric-application-model.md), um contêiner representa um host de aplicativo no qual o serviço várias réplicas são colocadas.</span><span class="sxs-lookup"><span data-stu-id="49650-155">In hello Service Fabric [application model](service-fabric-application-model.md), a container represents an application host in which multiple service replicas are placed.</span></span> <span data-ttu-id="49650-156">toodeploy e ativar um contêiner, um nome de saudação put da imagem de contêiner de saudação em um `ContainerHost` elemento no manifesto do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="49650-156">toodeploy and activate a container, put hello name of hello container image into a `ContainerHost` element in hello service manifest.</span></span>

<span data-ttu-id="49650-157">No manifesto do serviço hello, adicione um `ContainerHost` para o ponto de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="49650-157">In hello service manifest, add a `ContainerHost` for hello entry point.</span></span> <span data-ttu-id="49650-158">Em seguida, o conjunto de saudação `ImageName` toobe nome de saudação do repositório de contêiner hello e imagem.</span><span class="sxs-lookup"><span data-stu-id="49650-158">Then set hello `ImageName` toobe hello name of hello container repository and image.</span></span> <span data-ttu-id="49650-159">Olá, manifesto parcial a seguir mostra um exemplo de como o contêiner de saudação toodeploy chamado `myimage:v1` de um repositório chamado `myrepo`:</span><span class="sxs-lookup"><span data-stu-id="49650-159">hello following partial manifest shows an example of how toodeploy hello container called `myimage:v1` from a repository called `myrepo`:</span></span>

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

<span data-ttu-id="49650-160">Você pode especificar comandos opcionais toorun durante a inicialização do contêiner de saudação em Olá `Commands` elemento.</span><span class="sxs-lookup"><span data-stu-id="49650-160">You can specify optional commands toorun upon starting hello container under hello `Commands` element.</span></span> <span data-ttu-id="49650-161">Para vários comandos, delimite-os com vírgulas.</span><span class="sxs-lookup"><span data-stu-id="49650-161">For multiple commands, comma-delimit them.</span></span> 

## <a name="understand-resource-governance"></a><span data-ttu-id="49650-162">Compreender a governança de recursos</span><span class="sxs-lookup"><span data-stu-id="49650-162">Understand resource governance</span></span>
<span data-ttu-id="49650-163">Governança de recursos é um recurso de contêiner de saudação que restringe os recursos de Olá Olá contêiner pode usar no host de saudação.</span><span class="sxs-lookup"><span data-stu-id="49650-163">Resource governance is a capability of hello container that restricts hello resources that hello container can use on hello host.</span></span> <span data-ttu-id="49650-164">Olá `ResourceGovernancePolicy`, que é especificado no manifesto de aplicativo hello é usado toodeclare limites de recurso para um pacote de código de serviço.</span><span class="sxs-lookup"><span data-stu-id="49650-164">hello `ResourceGovernancePolicy`, which is specified in hello application manifest is used toodeclare resource limits for a service code package.</span></span> <span data-ttu-id="49650-165">Limites de recursos podem ser definidos para Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="49650-165">Resource limits can be set for hello following resources:</span></span>

* <span data-ttu-id="49650-166">Memória</span><span class="sxs-lookup"><span data-stu-id="49650-166">Memory</span></span>
* <span data-ttu-id="49650-167">MemorySwap</span><span class="sxs-lookup"><span data-stu-id="49650-167">MemorySwap</span></span>
* <span data-ttu-id="49650-168">CpuShares (peso relativo da CPU)</span><span class="sxs-lookup"><span data-stu-id="49650-168">CpuShares (CPU relative weight)</span></span>
* <span data-ttu-id="49650-169">MemoryReservationInMB</span><span class="sxs-lookup"><span data-stu-id="49650-169">MemoryReservationInMB</span></span>  
* <span data-ttu-id="49650-170">BlkioWeight (peso relativo do BlockIO).</span><span class="sxs-lookup"><span data-stu-id="49650-170">BlkioWeight (BlockIO relative weight).</span></span>

> [!NOTE]
> <span data-ttu-id="49650-171">o Suporte para especificar os limites de e/s de bloco específicoS como IOPs, leitura/gravação BPS e outros estão planejados para uma versão futura.</span><span class="sxs-lookup"><span data-stu-id="49650-171">Support for specifying specific block IO limits such as IOPs, read/write BPS, and others are planned for a future release.</span></span>
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

## <a name="authenticate-a-repository"></a><span data-ttu-id="49650-172">Autenticar um repositório</span><span class="sxs-lookup"><span data-stu-id="49650-172">Authenticate a repository</span></span>
<span data-ttu-id="49650-173">toodownload um contêiner, você pode ter um repositório de contêiner de toohello tooprovide credenciais de logon.</span><span class="sxs-lookup"><span data-stu-id="49650-173">toodownload a container, you might have tooprovide sign-in credentials toohello container repository.</span></span> <span data-ttu-id="49650-174">Olá credenciais de logon, especificadas no manifesto de aplicativo hello, são usadas toospecify Olá entrar informações ou uma chave SSH, para baixar a imagem de contêiner de saudação do repositório de imagens de saudação.</span><span class="sxs-lookup"><span data-stu-id="49650-174">hello sign-in credentials, specified in hello application manifest, are used toospecify hello sign-in information, or SSH key, for downloading hello container image from hello image repository.</span></span> <span data-ttu-id="49650-175">Olá, exemplo a seguir mostra uma conta chamada *TestUser* junto com a senha Olá em texto não criptografado (*não* recomendado):</span><span class="sxs-lookup"><span data-stu-id="49650-175">hello following example shows an account called *TestUser* along with hello password in clear text (*not* recommended):</span></span>

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

<span data-ttu-id="49650-176">É recomendável que você criptografe senha hello usando um certificado que tenha implantado toohello máquina.</span><span class="sxs-lookup"><span data-stu-id="49650-176">We recommend that you encrypt hello password by using a certificate that's deployed toohello machine.</span></span>

<span data-ttu-id="49650-177">Olá, exemplo a seguir mostra uma conta chamada *TestUser*, onde a senha de saudação foi criptografada usando um certificado chamado *MyCert*.</span><span class="sxs-lookup"><span data-stu-id="49650-177">hello following example shows an account called *TestUser*, where hello password was encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="49650-178">Você pode usar o hello `Invoke-ServiceFabricEncryptText` PowerShell comando toocreate Olá secreta de criptografia texto para senha hello.</span><span class="sxs-lookup"><span data-stu-id="49650-178">You can use hello `Invoke-ServiceFabricEncryptText` PowerShell command toocreate hello secret cipher text for hello password.</span></span> <span data-ttu-id="49650-179">Para obter mais informações, consulte o artigo Olá [gerenciar segredos em aplicativos do Service Fabric](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="49650-179">For more information, see hello article [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md).</span></span>

<span data-ttu-id="49650-180">chave privada de saudação do certificado de saudação que usou a senha de saudação toodecrypt deve ser implantado toohello o computador local em um método fora de banda.</span><span class="sxs-lookup"><span data-stu-id="49650-180">hello private key of hello certificate that's used toodecrypt hello password must be deployed toohello local machine in an out-of-band method.</span></span> <span data-ttu-id="49650-181">(No Azure, esse método é o Azure Resource Manager.) Em seguida, quando o Service Fabric implanta a máquina de toohello de pacote de serviço Olá, ele pode descriptografar o segredo de hello.</span><span class="sxs-lookup"><span data-stu-id="49650-181">(In Azure, this method is Azure Resource Manager.) Then, when Service Fabric deploys hello service package toohello machine, it can decrypt hello secret.</span></span> <span data-ttu-id="49650-182">Usando o segredo Olá junto com o nome da conta Olá, em seguida, pode autenticar com o repositório de contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="49650-182">By using hello secret along with hello account name, it can then authenticate with hello container repository.</span></span>

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

## <span data-ttu-id="49650-183"><a name ="Portsection"></a>Configurar o mapeamento de porta do contêiner toohost</span><span class="sxs-lookup"><span data-stu-id="49650-183"><a name ="Portsection"></a> Configure container toohost port mapping</span></span>
<span data-ttu-id="49650-184">Você pode configurar toocommunicate de porta usada um host com o contêiner de saudação especificando um `PortBinding` no manifesto de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="49650-184">You can configure a host port used toocommunicate with hello container by specifying a `PortBinding` in hello application manifest.</span></span> <span data-ttu-id="49650-185">Olá porta associação mapas Olá porta toowhich Olá serviço está escutando em Olá contêiner tooa porta no host de saudação.</span><span class="sxs-lookup"><span data-stu-id="49650-185">hello port binding maps hello port toowhich hello service is listening inside hello container tooa port on hello host.</span></span>

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

## <a name="configure-container-to-container-discovery-and-communication"></a><span data-ttu-id="49650-186">Configurar descoberta e comunicação de contêiner para contêiner</span><span class="sxs-lookup"><span data-stu-id="49650-186">Configure container-to-container discovery and communication</span></span>
<span data-ttu-id="49650-187">Você pode usar o hello `PortBinding` elemento toomap um ponto de extremidade de tooan de porta de contêiner no manifesto do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="49650-187">You can use hello `PortBinding` element toomap a container port tooan endpoint in hello service manifest.</span></span> <span data-ttu-id="49650-188">Em Olá exemplo a seguir, Olá ponto de extremidade `Endpoint1` Especifica uma porta fixa, 8905.</span><span class="sxs-lookup"><span data-stu-id="49650-188">In hello following example, hello endpoint `Endpoint1` specifies a fixed port, 8905.</span></span> <span data-ttu-id="49650-189">Ele também não pode especificar nenhuma porta, caso em que uma porta aleatória do intervalo de portas de aplicativo do cluster Olá é escolhida para você.</span><span class="sxs-lookup"><span data-stu-id="49650-189">It can also specify no port at all, in which case a random port from hello cluster's application port range is chosen for you.</span></span>


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
<span data-ttu-id="49650-190">Se você especificar um ponto de extremidade, usando Olá `Endpoint` marca no manifesto do serviço de saudação de um contêiner de convidado, o Service Fabric pode publicar automaticamente toohello esse ponto de extremidade Naming service.</span><span class="sxs-lookup"><span data-stu-id="49650-190">If you specify an endpoint, using hello `Endpoint` tag in hello service manifest of a guest container, Service Fabric can automatically publish this endpoint toohello Naming service.</span></span> <span data-ttu-id="49650-191">Outros serviços que são executados no cluster hello, portanto, podem descobrir esse contêiner usando consultas REST Olá para resolver.</span><span class="sxs-lookup"><span data-stu-id="49650-191">Other services that are running in hello cluster can thus discover this container using hello REST queries for resolving.</span></span>

<span data-ttu-id="49650-192">Registrando Olá Naming service, você pode executar o contêiner para contêiner comunicação dentro de seu contêiner usando Olá [proxy reverso](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="49650-192">By registering with hello Naming service, you can perform container-to-container communication within your container by using hello [reverse proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="49650-193">A comunicação é executada, fornecendo a porta de escuta Olá proxy reverso http e o nome de saudação do serviços de saudação que você deseja toocommunicate com como variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="49650-193">Communication is performed by providing hello reverse proxy http listening port and hello name of hello services that you want toocommunicate with as environment variables.</span></span> <span data-ttu-id="49650-194">Para obter mais informações, consulte Olá próxima seção.</span><span class="sxs-lookup"><span data-stu-id="49650-194">For more information, see hello next section.</span></span> 

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="49650-195">Configurar e definir as variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="49650-195">Configure and set environment variables</span></span>
<span data-ttu-id="49650-196">Variáveis de ambiente podem ser especificadas para cada pacote de código no manifesto do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="49650-196">Environment variables can be specified for each code package in hello service manifest.</span></span> <span data-ttu-id="49650-197">Esse recurso está disponível para todos os serviços, independentemente de eles serem implantados como contêineres ou processos ou executáveis convidados.</span><span class="sxs-lookup"><span data-stu-id="49650-197">This feature is available for all services irrespective of whether they are deployed as containers or processes or guest executables.</span></span> <span data-ttu-id="49650-198">Você pode substituir a variável de ambiente valores no aplicativo hello manifesto ou especificá-las durante a implantação como parâmetros de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="49650-198">You can override environment variable values in hello application manifest or specify them during deployment as application parameters.</span></span>

<span data-ttu-id="49650-199">Olá, serviço manifesto trecho XML a seguir mostra um exemplo de como toospecify variáveis de ambiente para um pacote de código:</span><span class="sxs-lookup"><span data-stu-id="49650-199">hello following service manifest XML snippet shows an example of how toospecify environment variables for a code package:</span></span>

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

<span data-ttu-id="49650-200">Essas variáveis de ambiente podem ser substituídos no nível de manifesto de aplicativo hello:</span><span class="sxs-lookup"><span data-stu-id="49650-200">These environment variables can be overridden at hello application manifest level:</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

<span data-ttu-id="49650-201">No exemplo anterior de saudação, especificamos um valor explícito para Olá `HttpGateway` (19000), enquanto definimos Olá valor de variável de ambiente `BackendServiceName` parâmetro via Olá `[BackendSvc]` parâmetro de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="49650-201">In hello previous example, we specified an explicit value for hello `HttpGateway` environment variable (19000), while we set hello value for `BackendServiceName` parameter via hello `[BackendSvc]` application parameter.</span></span> <span data-ttu-id="49650-202">Essas configurações permitem que você valor Olá toospecify `BackendServiceName`quando você implanta o aplicativo hello e não tem um valor fixo no manifesto de saudação do valor.</span><span class="sxs-lookup"><span data-stu-id="49650-202">These settings enable you toospecify hello value for `BackendServiceName`value when you deploy hello application and not have a fixed value in hello manifest.</span></span>

## <a name="configure-isolation-mode"></a><span data-ttu-id="49650-203">Configurar o modo de isolamento</span><span class="sxs-lookup"><span data-stu-id="49650-203">Configure isolation mode</span></span>

<span data-ttu-id="49650-204">L Windows dá suporte a dois modos de isolamento para contêineres: processo e Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="49650-204">Windows supports two isolation modes for containers - process and Hyper-V.</span></span>  <span data-ttu-id="49650-205">Com o modo de isolamento do processo de hello, todos os contêineres de saudação em execução no hello mesmo host máquina compartilhamento saudação do kernel com o host de saudação.</span><span class="sxs-lookup"><span data-stu-id="49650-205">With hello process isolation mode, all hello containers running on hello same host machine share hello kernel with hello host.</span></span> <span data-ttu-id="49650-206">Com o modo de isolamento Olá Hyper-V, kernels Olá são isolados entre cada contêiner do Hyper-V e o host do contêiner hello.</span><span class="sxs-lookup"><span data-stu-id="49650-206">With hello Hyper-V isolation mode, hello kernels are isolated between each Hyper-V container and hello container host.</span></span> <span data-ttu-id="49650-207">modo de isolamento de saudação é especificado em Olá `ContainerHostPolicies` marca no arquivo de manifesto de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="49650-207">hello isolation mode is specified in hello `ContainerHostPolicies` tag in hello application manifest file.</span></span>  <span data-ttu-id="49650-208">modos de isolamento de saudação que podem ser especificados são `process`, `hyperv`, e `default`.</span><span class="sxs-lookup"><span data-stu-id="49650-208">hello isolation modes that can be specified are `process`, `hyperv`, and `default`.</span></span> <span data-ttu-id="49650-209">Olá `default` modo de isolamento padrão é muito`process` no Windows Server hospeda e os padrões muito`hyperv` em hosts do Windows 10.</span><span class="sxs-lookup"><span data-stu-id="49650-209">hello `default` isolation mode defaults too`process` on Windows Server hosts, and defaults too`hyperv` on Windows 10 hosts.</span></span>  <span data-ttu-id="49650-210">Olá trecho a seguir mostra como o modo de isolamento de saudação é especificado no arquivo de manifesto de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="49650-210">hello following snippet shows how hello isolation mode is specified in hello application manifest file.</span></span>

```xml
   <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv">
```


## <a name="complete-examples-for-application-and-service-manifest"></a><span data-ttu-id="49650-211">Exemplos completos de aplicativo e manifesto do serviço</span><span class="sxs-lookup"><span data-stu-id="49650-211">Complete examples for application and service manifest</span></span>

<span data-ttu-id="49650-212">Aqui está um exemplo de manifesto de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="49650-212">An example application manifest follows:</span></span>

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

<span data-ttu-id="49650-213">Um manifesto de serviço de exemplo (especificado na Olá precede o manifesto do aplicativo) a seguir:</span><span class="sxs-lookup"><span data-stu-id="49650-213">An example service manifest (specified in hello preceding application manifest) follows:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="49650-214">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="49650-214">Next steps</span></span>
<span data-ttu-id="49650-215">Agora que você implantou um serviço em contêineres, saiba como toomanage seu ciclo de vida lendo [ciclo de vida do aplicativo de malha do serviço](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="49650-215">Now that you have deployed a containerized service, learn how toomanage its lifecycle by reading [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span></span>

* [<span data-ttu-id="49650-216">Visão geral do Service Fabric e contêineres</span><span class="sxs-lookup"><span data-stu-id="49650-216">Overview of Service Fabric and containers</span></span>](service-fabric-containers-overview.md)
* <span data-ttu-id="49650-217">Por exemplo, confira [Exemplos de código do contêiner do Service Fabric no GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="49650-217">For an example, checkout [Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>
