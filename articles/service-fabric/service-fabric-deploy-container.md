---
title: "Service Fabric e implantação de contêineres | Microsoft Docs"
description: "Service Fabric e o uso de contêineres para implantar aplicativos de microsserviço. Este artigo descreve os recursos que o Service Fabric fornece para contêineres e como implantar uma imagem de contêiner do Windows em um cluster."
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
ms.openlocfilehash: 25d6b056421e71fa70ed20a39589f77dbbc25c69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-windows-container-to-service-fabric"></a><span data-ttu-id="26ac5-104">Implantar um contêiner do Windows no Service Fabric</span><span class="sxs-lookup"><span data-stu-id="26ac5-104">Deploy a Windows container to Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="26ac5-105">Implantar contêiner do Windows</span><span class="sxs-lookup"><span data-stu-id="26ac5-105">Deploy Windows Container</span></span>](service-fabric-deploy-container.md)
> * [<span data-ttu-id="26ac5-106">Implantar contêiner do Docker</span><span class="sxs-lookup"><span data-stu-id="26ac5-106">Deploy Docker Container</span></span>](service-fabric-deploy-container-linux.md)
> 
> 

<span data-ttu-id="26ac5-107">Este artigo o orienta pelo processo de compilação de serviços contidos em contêineres do Windows.</span><span class="sxs-lookup"><span data-stu-id="26ac5-107">This article walks you through the process of building containerized services in Windows containers.</span></span>

<span data-ttu-id="26ac5-108">O Service Fabric tem vários recursos que ajudam na criação de aplicativos compostos de microsserviços em execução em contêineres.</span><span class="sxs-lookup"><span data-stu-id="26ac5-108">Service Fabric has several capabilities that help you with building applications that are composed of microservices running inside containers.</span></span> 

<span data-ttu-id="26ac5-109">As funcionalidade s incluem:</span><span class="sxs-lookup"><span data-stu-id="26ac5-109">The capabilities include:</span></span>

* <span data-ttu-id="26ac5-110">Implantação e ativação de imagens de contêiner</span><span class="sxs-lookup"><span data-stu-id="26ac5-110">Container image deployment and activation</span></span>
* <span data-ttu-id="26ac5-111">Governança de recursos</span><span class="sxs-lookup"><span data-stu-id="26ac5-111">Resource governance</span></span>
* <span data-ttu-id="26ac5-112">Autenticação do repositório</span><span class="sxs-lookup"><span data-stu-id="26ac5-112">Repository authentication</span></span>
* <span data-ttu-id="26ac5-113">Mapeamento de porta de contêiner para porta de host</span><span class="sxs-lookup"><span data-stu-id="26ac5-113">Container port-to-host port mapping</span></span>
* <span data-ttu-id="26ac5-114">Descoberta e comunicação de contêiner para contêiner</span><span class="sxs-lookup"><span data-stu-id="26ac5-114">Container-to-container discovery and communication</span></span>
* <span data-ttu-id="26ac5-115">Capacidade de configurar e definir as variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="26ac5-115">Ability to configure and set environment variables</span></span>

<span data-ttu-id="26ac5-116">Vamos ver como cada um dos recursos funciona quando você está empacotando um serviço em contêiner a ser incluído em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="26ac5-116">Let's look at how each of capabilities works when you're packaging a containerized service to be included in your application.</span></span>

## <a name="package-a-windows-container"></a><span data-ttu-id="26ac5-117">Empacotar um contêiner do Windows</span><span class="sxs-lookup"><span data-stu-id="26ac5-117">Package a Windows container</span></span>
<span data-ttu-id="26ac5-118">Ao empacotar um contêiner, você pode optar por usar um modelo de projeto do Visual Studio ou [criar o pacote de aplicativos manualmente](#manually).</span><span class="sxs-lookup"><span data-stu-id="26ac5-118">When you package a container, you can choose to use either a Visual Studio project template or [create the application package manually](#manually).</span></span>  <span data-ttu-id="26ac5-119">Ao usar o Visual Studio, a estrutura do pacote de aplicativos e os arquivos de manifesto são criados para você pelo modelo Novo Projeto.</span><span class="sxs-lookup"><span data-stu-id="26ac5-119">When you use Visual Studio, the application package structure and manifest files are created by the New Project template for you.</span></span>

> [!TIP]
> <span data-ttu-id="26ac5-120">A maneira mais fácil de empacotar uma imagem de contêiner existente em um serviço é usar o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="26ac5-120">The easiest way to package an existing container image into a service is to use Visual Studio.</span></span>

## <a name="use-visual-studio-to-package-an-existing-container-image"></a><span data-ttu-id="26ac5-121">Usar o Visual Studio para empacotar uma imagem de contêiner existente</span><span class="sxs-lookup"><span data-stu-id="26ac5-121">Use Visual Studio to package an existing container image</span></span>
<span data-ttu-id="26ac5-122">O Visual Studio fornece um modelo de serviço do Service Fabric para ajudar você a implantar um contêiner em um cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="26ac5-122">Visual Studio provides a Service Fabric service template to help you deploy a container to a Service Fabric cluster.</span></span>

1. <span data-ttu-id="26ac5-123">Escolha **Arquivo** > **Novo Projeto** e crie um aplicativo de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="26ac5-123">Choose **File** > **New Project**, and create a Service Fabric application.</span></span>
2. <span data-ttu-id="26ac5-124">Escolha **Contêiner Convidado** como o modelo de serviço.</span><span class="sxs-lookup"><span data-stu-id="26ac5-124">Choose **Guest Container** as the service template.</span></span>
3. <span data-ttu-id="26ac5-125">Escolha **Nome da Imagem** e forneça o caminho da imagem no repositório de contêiner.</span><span class="sxs-lookup"><span data-stu-id="26ac5-125">Choose **Image Name** and provide the path to the image in your container repository.</span></span> <span data-ttu-id="26ac5-126">Por exemplo, `myrepo/myimage:v1` em https://hub.docker.com</span><span class="sxs-lookup"><span data-stu-id="26ac5-126">For example, `myrepo/myimage:v1` in https://hub.docker.com</span></span>
4. <span data-ttu-id="26ac5-127">Dê um nome ao seu serviço e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="26ac5-127">Give your service a name, and click **OK**.</span></span>
5. <span data-ttu-id="26ac5-128">Se seu serviço em contêiner precisar de um ponto de extremidade para comunicação, você poderá adicionar o protocolo, a porta e o tipo ao arquivo ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="26ac5-128">If your containerized service needs an endpoint for communication, you can now add the protocol, port, and type to the ServiceManifest.xml file.</span></span> <span data-ttu-id="26ac5-129">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="26ac5-129">For example:</span></span> 
     
    `<Endpoint Name="MyContainerServiceEndpoint" Protocol="http" Port="80" UriScheme="http" PathSuffix="myapp/" Type="Input" />`
    
    <span data-ttu-id="26ac5-130">Fornecendo o `UriScheme`, o Service Fabric registra automaticamente o ponto de extremidade do contêiner no serviço de Nomenclatura para capacidade de descoberta.</span><span class="sxs-lookup"><span data-stu-id="26ac5-130">By providing the `UriScheme`, Service Fabric automatically registers the container endpoint with the Naming service for discoverability.</span></span> <span data-ttu-id="26ac5-131">A porta pode ser fixa (conforme mostrado no exemplo anterior) ou alocada dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="26ac5-131">The port can either be fixed (as shown in the preceding example) or dynamically allocated.</span></span> <span data-ttu-id="26ac5-132">Se você não especificar uma porta, ela será alocada dinamicamente do intervalo de portas do aplicativo (como acontece com qualquer serviço).</span><span class="sxs-lookup"><span data-stu-id="26ac5-132">If you don't specify a port, it is dynamically allocated from the application port range (as would happen with any service).</span></span>
    <span data-ttu-id="26ac5-133">Você também precisa configurar o contêiner para o mapeamento de porta de host, especificando uma política `PortBinding` no manifesto do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="26ac5-133">You also need to configure the container to host port mapping by specifying a `PortBinding` policy in the application manifest.</span></span> <span data-ttu-id="26ac5-134">Para obter mais informações, confira [Configurar contêiner para hospedar mapeamento de porta](#Portsection).</span><span class="sxs-lookup"><span data-stu-id="26ac5-134">For more information, see [Configure container to host port mapping](#Portsection).</span></span>
6. <span data-ttu-id="26ac5-135">Se seu contêiner precisar de governança de recursos, adicione `ResourceGovernancePolicy`.</span><span class="sxs-lookup"><span data-stu-id="26ac5-135">If your container needs resource governance then add a `ResourceGovernancePolicy`.</span></span>
8. <span data-ttu-id="26ac5-136">Se o seu contêiner precisar autenticar com um repositório privado, adicione `RepositoryCredentials`.</span><span class="sxs-lookup"><span data-stu-id="26ac5-136">If your container needs to authenticate with a private repository, then add `RepositoryCredentials`.</span></span>
7. <span data-ttu-id="26ac5-137">Se estiver realizando a execução em um computador Windows Server 2016 com o suporte de contêiner habilitado, você poderá usar o pacote e a ação de publicação para implantar no cluster local.</span><span class="sxs-lookup"><span data-stu-id="26ac5-137">If you are running on a Windows Server 2016 machine with container support enabled, you can use the package and publish action to deploy to your local cluster.</span></span> 
8. <span data-ttu-id="26ac5-138">Quando estiver pronto, você poderá publicar o aplicativo em um cluster remoto ou fazer check-in da solução para o controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="26ac5-138">When ready, you can publish the application to a remote cluster or check in the solution to source control.</span></span> 

<span data-ttu-id="26ac5-139">Para obter um exemplo, [confira os códigos de exemplo de contêiner do Service Fabric no GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="26ac5-139">For an example, checkout the [Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>

## <a name="creating-a-windows-server-2016-cluster"></a><span data-ttu-id="26ac5-140">Criar um cluster do Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="26ac5-140">Creating a Windows Server 2016 cluster</span></span>
<span data-ttu-id="26ac5-141">Para implantar aplicativos contidos, é necessário criar um cluster que execute o Windows Server 2016 com o suporte para contêineres habilitado.</span><span class="sxs-lookup"><span data-stu-id="26ac5-141">To deploy your containerized application, you need to create a cluster running Windows Server 2016 with container support enabled.</span></span> <span data-ttu-id="26ac5-142">O cluster pode estar em execução localmente ou ser implantado por meio do Azure Resource Manager no Azure.</span><span class="sxs-lookup"><span data-stu-id="26ac5-142">Your cluster may be running locally, or deployed via Azure Resource Manager in Azure.</span></span> 

<span data-ttu-id="26ac5-143">Para implantar um cluster usando o Azure Resource Manager, escolha a opção de imagem **Windows Server 2016 com Contêineres** no Azure.</span><span class="sxs-lookup"><span data-stu-id="26ac5-143">To deploy a cluster using Azure Resource Manager, choose the **Windows Server 2016 with Containers** image option in Azure.</span></span> <span data-ttu-id="26ac5-144">Consulte o artigo [Criar um cluster do Service Fabric usando o Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="26ac5-144">See the article [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="26ac5-145">Use as seguintes configurações do Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="26ac5-145">Ensure that you use the following Azure Resource Manager settings:</span></span>

```xml
"vmImageOffer": { "type": "string","defaultValue": "WindowsServer"     },
"vmImageSku": { "defaultValue": "2016-Datacenter-with-Containers","type": "string"     },
"vmImageVersion": { "defaultValue": "latest","type": "string"     },  
```
<span data-ttu-id="26ac5-146">Você também pode usar o [modelo de cinco nós do Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) para criar um cluster.</span><span class="sxs-lookup"><span data-stu-id="26ac5-146">You can also use the [Five Node Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) to create a cluster.</span></span> <span data-ttu-id="26ac5-147">Como alternativa, leia uma [postagem de blog](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) da comunidade sobre o uso de contêineres do Windows e do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="26ac5-147">Alternatively read a community [blog post](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) on using Service Fabric and Windows containers.</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a><span data-ttu-id="26ac5-148">Empacotar e implantar manualmente uma imagem de contêiner</span><span class="sxs-lookup"><span data-stu-id="26ac5-148">Manually package and deploy a container image</span></span>
<span data-ttu-id="26ac5-149">O processo de empacotamento manual de um serviço em contêiner se baseia nas seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="26ac5-149">The process of manually packaging a containerized service is based on the following steps:</span></span>

1. <span data-ttu-id="26ac5-150">Publicar os contêineres em seu repositório.</span><span class="sxs-lookup"><span data-stu-id="26ac5-150">Publish the containers to your repository.</span></span>
2. <span data-ttu-id="26ac5-151">Criar a estrutura de diretórios do pacote.</span><span class="sxs-lookup"><span data-stu-id="26ac5-151">Create the package directory structure.</span></span>
3. <span data-ttu-id="26ac5-152">Editar o arquivo de manifesto do serviço.</span><span class="sxs-lookup"><span data-stu-id="26ac5-152">Edit the service manifest file.</span></span>
4. <span data-ttu-id="26ac5-153">Editar o arquivo de manifesto do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="26ac5-153">Edit the application manifest file.</span></span>

## <a name="deploy-and-activate-a-container-image"></a><span data-ttu-id="26ac5-154">Implantar e ativar uma imagem de contêiner</span><span class="sxs-lookup"><span data-stu-id="26ac5-154">Deploy and activate a container image</span></span>
<span data-ttu-id="26ac5-155">No [modelo de aplicativo](service-fabric-application-model.md)do Service Fabric, um contêiner representa um host de aplicativo no qual várias réplicas de serviço são colocadas.</span><span class="sxs-lookup"><span data-stu-id="26ac5-155">In the Service Fabric [application model](service-fabric-application-model.md), a container represents an application host in which multiple service replicas are placed.</span></span> <span data-ttu-id="26ac5-156">Para implantar e ativar um contêiner, coloque o nome da imagem do contêiner em um elemento `ContainerHost` no manifesto do serviço.</span><span class="sxs-lookup"><span data-stu-id="26ac5-156">To deploy and activate a container, put the name of the container image into a `ContainerHost` element in the service manifest.</span></span>

<span data-ttu-id="26ac5-157">No manifesto do serviço, adicione um `ContainerHost` do ponto de entrada.</span><span class="sxs-lookup"><span data-stu-id="26ac5-157">In the service manifest, add a `ContainerHost` for the entry point.</span></span> <span data-ttu-id="26ac5-158">Em seguida, defina o `ImageName` para o nome do repositório de contêiner e imagem.</span><span class="sxs-lookup"><span data-stu-id="26ac5-158">Then set the `ImageName` to be the name of the container repository and image.</span></span> <span data-ttu-id="26ac5-159">O manifesto parcial a seguir mostra um exemplo de como implantar o contêiner chamado `myimage:v1` de um repositório chamado `myrepo`:</span><span class="sxs-lookup"><span data-stu-id="26ac5-159">The following partial manifest shows an example of how to deploy the container called `myimage:v1` from a repository called `myrepo`:</span></span>

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

<span data-ttu-id="26ac5-160">Você pode especificar comandos opcionais para serem executados após a inicialização do contêiner sob o elemento `Commands`.</span><span class="sxs-lookup"><span data-stu-id="26ac5-160">You can specify optional commands to run upon starting the container under the `Commands` element.</span></span> <span data-ttu-id="26ac5-161">Para vários comandos, delimite-os com vírgulas.</span><span class="sxs-lookup"><span data-stu-id="26ac5-161">For multiple commands, comma-delimit them.</span></span> 

## <a name="understand-resource-governance"></a><span data-ttu-id="26ac5-162">Compreender a governança de recursos</span><span class="sxs-lookup"><span data-stu-id="26ac5-162">Understand resource governance</span></span>
<span data-ttu-id="26ac5-163">A governança de recursos é uma funcionalidade do contêiner e restringe os recursos que o contêiner pode usar no host.</span><span class="sxs-lookup"><span data-stu-id="26ac5-163">Resource governance is a capability of the container that restricts the resources that the container can use on the host.</span></span> <span data-ttu-id="26ac5-164">O `ResourceGovernancePolicy`, especificado no manifesto do aplicativo, é usado para declarar os limites de recurso para um pacote de códigos de serviço.</span><span class="sxs-lookup"><span data-stu-id="26ac5-164">The `ResourceGovernancePolicy`, which is specified in the application manifest is used to declare resource limits for a service code package.</span></span> <span data-ttu-id="26ac5-165">Limites de recursos podem ser definidos para os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="26ac5-165">Resource limits can be set for the following resources:</span></span>

* <span data-ttu-id="26ac5-166">Memória</span><span class="sxs-lookup"><span data-stu-id="26ac5-166">Memory</span></span>
* <span data-ttu-id="26ac5-167">MemorySwap</span><span class="sxs-lookup"><span data-stu-id="26ac5-167">MemorySwap</span></span>
* <span data-ttu-id="26ac5-168">CpuShares (peso relativo da CPU)</span><span class="sxs-lookup"><span data-stu-id="26ac5-168">CpuShares (CPU relative weight)</span></span>
* <span data-ttu-id="26ac5-169">MemoryReservationInMB</span><span class="sxs-lookup"><span data-stu-id="26ac5-169">MemoryReservationInMB</span></span>  
* <span data-ttu-id="26ac5-170">BlkioWeight (peso relativo do BlockIO).</span><span class="sxs-lookup"><span data-stu-id="26ac5-170">BlkioWeight (BlockIO relative weight).</span></span>

> [!NOTE]
> <span data-ttu-id="26ac5-171">o Suporte para especificar os limites de e/s de bloco específicoS como IOPs, leitura/gravação BPS e outros estão planejados para uma versão futura.</span><span class="sxs-lookup"><span data-stu-id="26ac5-171">Support for specifying specific block IO limits such as IOPs, read/write BPS, and others are planned for a future release.</span></span>
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

## <a name="authenticate-a-repository"></a><span data-ttu-id="26ac5-172">Autenticar um repositório</span><span class="sxs-lookup"><span data-stu-id="26ac5-172">Authenticate a repository</span></span>
<span data-ttu-id="26ac5-173">Para baixar um contêiner, poderá ser preciso fornecer as credenciais de logon para o repositório do contêiner.</span><span class="sxs-lookup"><span data-stu-id="26ac5-173">To download a container, you might have to provide sign-in credentials to the container repository.</span></span> <span data-ttu-id="26ac5-174">As credenciais de logon especificadas no manifesto do aplicativo são usadas para especificar as informações de logon, ou a chave SSH, para baixar a imagem do contêiner do repositório de imagens.</span><span class="sxs-lookup"><span data-stu-id="26ac5-174">The sign-in credentials, specified in the application manifest, are used to specify the sign-in information, or SSH key, for downloading the container image from the image repository.</span></span> <span data-ttu-id="26ac5-175">O exemplo a seguir mostra uma conta chamada *TestUser* junto com a senha em texto não criptografado (*não* recomendado):</span><span class="sxs-lookup"><span data-stu-id="26ac5-175">The following example shows an account called *TestUser* along with the password in clear text (*not* recommended):</span></span>

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

<span data-ttu-id="26ac5-176">É recomendável que você criptografe a senha usando um certificado implantado no computador.</span><span class="sxs-lookup"><span data-stu-id="26ac5-176">We recommend that you encrypt the password by using a certificate that's deployed to the machine.</span></span>

<span data-ttu-id="26ac5-177">O exemplo a seguir mostra uma conta chamada *TestUser*, em que a senha foi criptografada usando um certificado chamado *MyCert*.</span><span class="sxs-lookup"><span data-stu-id="26ac5-177">The following example shows an account called *TestUser*, where the password was encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="26ac5-178">Você pode usar o comando `Invoke-ServiceFabricEncryptText` do PowerShell para criar o texto cifrado secreto para a senha.</span><span class="sxs-lookup"><span data-stu-id="26ac5-178">You can use the `Invoke-ServiceFabricEncryptText` PowerShell command to create the secret cipher text for the password.</span></span> <span data-ttu-id="26ac5-179">Para obter mais informações, consulte o artigo [Gerenciar segredos em aplicativos do Service Fabric](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="26ac5-179">For more information, see the article [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md).</span></span>

<span data-ttu-id="26ac5-180">A chave privada do certificado usada para descriptografar a senha deve ser implantada no computador local em um método fora de banda.</span><span class="sxs-lookup"><span data-stu-id="26ac5-180">The private key of the certificate that's used to decrypt the password must be deployed to the local machine in an out-of-band method.</span></span> <span data-ttu-id="26ac5-181">(No Azure, esse método é o Azure Resource Manager.) Em seguida, quando o Service Fabric implanta o pacote de serviço para o computador, ele poderá descriptografar o segredo.</span><span class="sxs-lookup"><span data-stu-id="26ac5-181">(In Azure, this method is Azure Resource Manager.) Then, when Service Fabric deploys the service package to the machine, it can decrypt the secret.</span></span> <span data-ttu-id="26ac5-182">Usando o segredo junto com o nome da conta, ele então pode autenticar com o repositório do contêiner.</span><span class="sxs-lookup"><span data-stu-id="26ac5-182">By using the secret along with the account name, it can then authenticate with the container repository.</span></span>

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

## <span data-ttu-id="26ac5-183"><a name ="Portsection"></a>Configurar o contêiner para o mapeamento de porta de host</span><span class="sxs-lookup"><span data-stu-id="26ac5-183"><a name ="Portsection"></a> Configure container to host port mapping</span></span>
<span data-ttu-id="26ac5-184">Você pode configurar uma porta de host usada para se comunicar com o contêiner especificando um `PortBinding` no manifesto do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="26ac5-184">You can configure a host port used to communicate with the container by specifying a `PortBinding` in the application manifest.</span></span> <span data-ttu-id="26ac5-185">A associação de porta mapeia a porta que o serviço está escutando dentro do contêiner para uma porta no host.</span><span class="sxs-lookup"><span data-stu-id="26ac5-185">The port binding maps the port to which the service is listening inside the container to a port on the host.</span></span>

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

## <a name="configure-container-to-container-discovery-and-communication"></a><span data-ttu-id="26ac5-186">Configurar descoberta e comunicação de contêiner para contêiner</span><span class="sxs-lookup"><span data-stu-id="26ac5-186">Configure container-to-container discovery and communication</span></span>
<span data-ttu-id="26ac5-187">Você pode usar o elemento `PortBinding` para mapear uma porta de contêiner para um ponto de extremidade no manifesto do serviço.</span><span class="sxs-lookup"><span data-stu-id="26ac5-187">You can use the `PortBinding` element to map a container port to an endpoint in the service manifest.</span></span> <span data-ttu-id="26ac5-188">No exemplo a seguir, o ponto de extremidade `Endpoint1` especifica uma porta fixa, 8905.</span><span class="sxs-lookup"><span data-stu-id="26ac5-188">In the following example, the endpoint `Endpoint1` specifies a fixed port, 8905.</span></span> <span data-ttu-id="26ac5-189">Também pode especificar nenhuma porta, quando uma porta aleatória no intervalo de portas do aplicativo do cluster será escolhida para você.</span><span class="sxs-lookup"><span data-stu-id="26ac5-189">It can also specify no port at all, in which case a random port from the cluster's application port range is chosen for you.</span></span>


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
<span data-ttu-id="26ac5-190">Se você especificar um ponto de extremidade, usando a marca `Endpoint` no manifesto do serviço de um contêiner de convidado, o Service Fabric poderá publicar automaticamente este ponto de extremidade no serviço de Nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="26ac5-190">If you specify an endpoint, using the `Endpoint` tag in the service manifest of a guest container, Service Fabric can automatically publish this endpoint to the Naming service.</span></span> <span data-ttu-id="26ac5-191">Portanto, outros serviços que são executados no cluster podem descobrir esse contêiner usando as consultas REST para resolver.</span><span class="sxs-lookup"><span data-stu-id="26ac5-191">Other services that are running in the cluster can thus discover this container using the REST queries for resolving.</span></span>

<span data-ttu-id="26ac5-192">Registrando-se no serviço de Nomenclatura, você pode executar a comunicação de contêiner para contêiner no contêiner usando o [proxy reverso](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="26ac5-192">By registering with the Naming service, you can perform container-to-container communication within your container by using the [reverse proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="26ac5-193">A comunicação é realizada fornecendo a porta de escuta de proxy reverso http e o nome dos serviços com os quais você deseja se comunicar como variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="26ac5-193">Communication is performed by providing the reverse proxy http listening port and the name of the services that you want to communicate with as environment variables.</span></span> <span data-ttu-id="26ac5-194">Para obter mais informações, confira a próxima seção.</span><span class="sxs-lookup"><span data-stu-id="26ac5-194">For more information, see the next section.</span></span> 

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="26ac5-195">Configurar e definir as variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="26ac5-195">Configure and set environment variables</span></span>
<span data-ttu-id="26ac5-196">Variáveis de ambiente podem ser especificadas para cada pacote de códigos no manifesto do serviço.</span><span class="sxs-lookup"><span data-stu-id="26ac5-196">Environment variables can be specified for each code package in the service manifest.</span></span> <span data-ttu-id="26ac5-197">Esse recurso está disponível para todos os serviços, independentemente de eles serem implantados como contêineres ou processos ou executáveis convidados.</span><span class="sxs-lookup"><span data-stu-id="26ac5-197">This feature is available for all services irrespective of whether they are deployed as containers or processes or guest executables.</span></span> <span data-ttu-id="26ac5-198">Você pode substituir valores de variáveis de ambiente no manifesto do aplicativo ou especificá-los durante a implantação como parâmetros de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="26ac5-198">You can override environment variable values in the application manifest or specify them during deployment as application parameters.</span></span>

<span data-ttu-id="26ac5-199">O trecho XML do manifesto do serviço a seguir mostra um exemplo de como especificar variáveis de ambiente para um pacote de códigos:</span><span class="sxs-lookup"><span data-stu-id="26ac5-199">The following service manifest XML snippet shows an example of how to specify environment variables for a code package:</span></span>

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

<span data-ttu-id="26ac5-200">Essas variáveis de ambiente podem ser substituídas no nível do manifesto do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="26ac5-200">These environment variables can be overridden at the application manifest level:</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

<span data-ttu-id="26ac5-201">No exemplo acima, especificamos um valor explícito para a variável de ambiente `HttpGateway` (19000) enquanto definimos o valor do parâmetro `BackendServiceName` é definido por meio do parâmetro de aplicativo `[BackendSvc]`.</span><span class="sxs-lookup"><span data-stu-id="26ac5-201">In the previous example, we specified an explicit value for the `HttpGateway` environment variable (19000), while we set the value for `BackendServiceName` parameter via the `[BackendSvc]` application parameter.</span></span> <span data-ttu-id="26ac5-202">Essas configurações permitem especificar o valor para `BackendServiceName`valor quando você implanta o aplicativo e não tem um valor fixo no manifesto.</span><span class="sxs-lookup"><span data-stu-id="26ac5-202">These settings enable you to specify the value for `BackendServiceName`value when you deploy the application and not have a fixed value in the manifest.</span></span>

## <a name="configure-isolation-mode"></a><span data-ttu-id="26ac5-203">Configurar o modo de isolamento</span><span class="sxs-lookup"><span data-stu-id="26ac5-203">Configure isolation mode</span></span>

<span data-ttu-id="26ac5-204">L Windows dá suporte a dois modos de isolamento para contêineres: processo e Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="26ac5-204">Windows supports two isolation modes for containers - process and Hyper-V.</span></span>  <span data-ttu-id="26ac5-205">Com o modo de isolamento de processo, todos os contêineres em execução no mesmo computador host compartilham o kernel com o host.</span><span class="sxs-lookup"><span data-stu-id="26ac5-205">With the process isolation mode, all the containers running on the same host machine share the kernel with the host.</span></span> <span data-ttu-id="26ac5-206">Com o modo de isolamento do Hyper-V, os kernels são isolados entre cada contêiner do Hyper-V e o host do contêiner.</span><span class="sxs-lookup"><span data-stu-id="26ac5-206">With the Hyper-V isolation mode, the kernels are isolated between each Hyper-V container and the container host.</span></span> <span data-ttu-id="26ac5-207">O modo de isolamento é especificado na marca `ContainerHostPolicies` no arquivo de manifesto do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="26ac5-207">The isolation mode is specified in the `ContainerHostPolicies` tag in the application manifest file.</span></span>  <span data-ttu-id="26ac5-208">Os modos de isolamento que podem ser especificados são `process`, `hyperv` e `default`.</span><span class="sxs-lookup"><span data-stu-id="26ac5-208">The isolation modes that can be specified are `process`, `hyperv`, and `default`.</span></span> <span data-ttu-id="26ac5-209">O modo de isolamento `default` usa `process` por padrão em hosts do Windows Server e usa `hyperv` por padrão em hosts do Windows 10.</span><span class="sxs-lookup"><span data-stu-id="26ac5-209">The `default` isolation mode defaults to `process` on Windows Server hosts, and defaults to `hyperv` on Windows 10 hosts.</span></span>  <span data-ttu-id="26ac5-210">O trecho a seguir mostra como o modo de isolamento é especificado no arquivo de manifesto do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="26ac5-210">The following snippet shows how the isolation mode is specified in the application manifest file.</span></span>

```xml
   <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv">
```


## <a name="complete-examples-for-application-and-service-manifest"></a><span data-ttu-id="26ac5-211">Exemplos completos de aplicativo e manifesto do serviço</span><span class="sxs-lookup"><span data-stu-id="26ac5-211">Complete examples for application and service manifest</span></span>

<span data-ttu-id="26ac5-212">Aqui está um exemplo de manifesto de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="26ac5-212">An example application manifest follows:</span></span>

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

<span data-ttu-id="26ac5-213">Aqui está um exemplo de manifesto de serviço (especificado no manifesto do aplicativo anterior):</span><span class="sxs-lookup"><span data-stu-id="26ac5-213">An example service manifest (specified in the preceding application manifest) follows:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="26ac5-214">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="26ac5-214">Next steps</span></span>
<span data-ttu-id="26ac5-215">Agora que você implantou um serviço em contêiner, saiba como gerenciar seu ciclo de vida lendo [ciclo de vida de aplicativos do Service Fabric](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="26ac5-215">Now that you have deployed a containerized service, learn how to manage its lifecycle by reading [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span></span>

* [<span data-ttu-id="26ac5-216">Visão geral do Service Fabric e contêineres</span><span class="sxs-lookup"><span data-stu-id="26ac5-216">Overview of Service Fabric and containers</span></span>](service-fabric-containers-overview.md)
* <span data-ttu-id="26ac5-217">Por exemplo, confira [Exemplos de código do contêiner do Service Fabric no GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="26ac5-217">For an example, checkout [Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>
