---
title: "Service Fabric e implantação de contêineres no Linux| Microsoft Docs"
description: "Service Fabric e o uso de contêineres do Linux para implantar aplicativos de microsserviço. Este artigo descreve os recursos que o Service Fabric fornece para contêineres e como implantar uma imagem de contêiner do Linux em um cluster"
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
ms.openlocfilehash: 9dcec753e5f999a1bac07276373c0c25f89ec58d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-linux-container-to-service-fabric"></a><span data-ttu-id="96550-104">Implantar um contêiner do Linux no Service Fabric</span><span class="sxs-lookup"><span data-stu-id="96550-104">Deploy a Linux container to Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="96550-105">Implantar contêiner do Windows</span><span class="sxs-lookup"><span data-stu-id="96550-105">Deploy Windows Container</span></span>](service-fabric-deploy-container.md)
> * [<span data-ttu-id="96550-106">Implantar contêiner do Linux</span><span class="sxs-lookup"><span data-stu-id="96550-106">Deploy Linux Container</span></span>](service-fabric-deploy-container-linux.md)
>
>

<span data-ttu-id="96550-107">Este artigo orienta a criação de serviços contentorizados em contêineres do Docker no Linux.</span><span class="sxs-lookup"><span data-stu-id="96550-107">This article walks you through building containerized services in Docker containers on Linux.</span></span>

<span data-ttu-id="96550-108">O Service Fabric tem vários recursos de contêiner que ajudam na compilação de aplicativos que são compostos por microsserviços que estão em contêineres.</span><span class="sxs-lookup"><span data-stu-id="96550-108">Service Fabric has several container capabilities that help you with building applications that are composed of microservices that are containerized.</span></span> <span data-ttu-id="96550-109">Esses serviços são chamados de serviços em contêineres.</span><span class="sxs-lookup"><span data-stu-id="96550-109">These services are called containerized services.</span></span>

<span data-ttu-id="96550-110">Os recursos incluem;</span><span class="sxs-lookup"><span data-stu-id="96550-110">The capabilities include;</span></span>

* <span data-ttu-id="96550-111">Implantação e ativação de imagens de contêiner</span><span class="sxs-lookup"><span data-stu-id="96550-111">Container image deployment and activation</span></span>
* <span data-ttu-id="96550-112">Governança de recursos</span><span class="sxs-lookup"><span data-stu-id="96550-112">Resource governance</span></span>
* <span data-ttu-id="96550-113">Autenticação do repositório</span><span class="sxs-lookup"><span data-stu-id="96550-113">Repository authentication</span></span>
* <span data-ttu-id="96550-114">Porta do contêiner para o mapeamento da porta de host</span><span class="sxs-lookup"><span data-stu-id="96550-114">Container port to host port mapping</span></span>
* <span data-ttu-id="96550-115">Descoberta e comunicação de contêiner para contêiner</span><span class="sxs-lookup"><span data-stu-id="96550-115">Container-to-container discovery and communication</span></span>
* <span data-ttu-id="96550-116">Capacidade de configurar e definir as variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="96550-116">Ability to configure and set environment variables</span></span>

## <a name="packaging-a-docker-container-with-yeoman"></a><span data-ttu-id="96550-117">Empacotando um contêiner do Docker com yeoman</span><span class="sxs-lookup"><span data-stu-id="96550-117">Packaging a docker container with yeoman</span></span>
<span data-ttu-id="96550-118">Ao empacotar um contêiner no Linux, você pode optar por usar um modelo yeoman ou por [criar o pacote de aplicativos manualmente](#manually).</span><span class="sxs-lookup"><span data-stu-id="96550-118">When packaging a container on Linux, you can choose either to use a yeoman template or [create the application package manually](#manually).</span></span>

<span data-ttu-id="96550-119">Um aplicativo do Service Fabric pode conter um ou mais contêineres, cada um com uma função específica no fornecimento de funcionalidade do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="96550-119">A Service Fabric application can contain one or more containers, each with a specific role in delivering the application's functionality.</span></span> <span data-ttu-id="96550-120">O SDK do Service Fabric para Linux inclui um gerador [Yeoman](http://yeoman.io/) que facilita a criação de seu aplicativo e a adição de uma imagem de contêiner.</span><span class="sxs-lookup"><span data-stu-id="96550-120">The Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy to create your application and add a container image.</span></span> <span data-ttu-id="96550-121">Vamos usar o Yeoman para criar um aplicativo, com um único contêiner do Docker, chamado de *SimpleContainerApp*.</span><span class="sxs-lookup"><span data-stu-id="96550-121">Let's use Yeoman to create an application with a single Docker container called *SimpleContainerApp*.</span></span> <span data-ttu-id="96550-122">Você pode adicionar mais serviços mais tarde editando os arquivos de manifesto gerados.</span><span class="sxs-lookup"><span data-stu-id="96550-122">You can add more services later by editing the generated manifest files.</span></span>

## <a name="install-docker-on-your-development-box"></a><span data-ttu-id="96550-123">Instalar o Docker em sua caixa de desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="96550-123">Install Docker on your development box</span></span>

<span data-ttu-id="96550-124">Execute os seguintes comandos para instalar o docker em sua caixa de desenvolvimento do Linux (se você estiver usando a imagem vagrant no OSX, o docker já estará instalado):</span><span class="sxs-lookup"><span data-stu-id="96550-124">Run the following commands to install docker on your Linux development box (if you are using the vagrant image on OSX, docker is already installed):</span></span>

```bash
    sudo apt-get install wget
    wget -qO- https://get.docker.io/ | sh
```

## <a name="create-the-application"></a><span data-ttu-id="96550-125">Criar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="96550-125">Create the application</span></span>
1. <span data-ttu-id="96550-126">Em um terminal, digite `yo azuresfcontainer`.</span><span class="sxs-lookup"><span data-stu-id="96550-126">In a terminal, type `yo azuresfcontainer`.</span></span>
2. <span data-ttu-id="96550-127">Dê um nome para o seu aplicativo, por exemplo, mycontainerap</span><span class="sxs-lookup"><span data-stu-id="96550-127">Name your application - for example, mycontainerap</span></span>
3. <span data-ttu-id="96550-128">Forneça a URL da imagem do contêiner de um repositório DockerHub.</span><span class="sxs-lookup"><span data-stu-id="96550-128">Provide the URL for the container image from a DockerHub repo.</span></span> <span data-ttu-id="96550-129">O parâmetro da imagem assume a forma [repositório]/[nome da imagem]</span><span class="sxs-lookup"><span data-stu-id="96550-129">The image parameter takes the form [repo]/[image name]</span></span>
4. <span data-ttu-id="96550-130">Se a imagem não tiver um ponto de entrada de carga de trabalho definido, em seguida, você precisa especificar explicitamente os comandos de entrada com um conjunto delimitado por vírgulas de comandos para serem executados dentro do contêiner, que manterá o contêiner em execução após a inicialização.</span><span class="sxs-lookup"><span data-stu-id="96550-130">If the image does not have a workload entry-point defined, then you need to explicitly specify input commands with a comma-delimited set of commands to run inside the container, which will keep the container running after startup.</span></span>

![Gerador de Yeoman do Service Fabric para contêineres][sf-yeoman]

## <a name="deploy-the-application"></a><span data-ttu-id="96550-132">Implantar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="96550-132">Deploy the application</span></span>

### <a name="using-xplat-cli"></a><span data-ttu-id="96550-133">Usando a CLI XPlat</span><span class="sxs-lookup"><span data-stu-id="96550-133">Using XPlat CLI</span></span>
<span data-ttu-id="96550-134">Após a compilação do aplicativo, você pode implantá-lo no cluster local usando a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="96550-134">Once the application is built, you can deploy it to the local cluster using the Azure CLI.</span></span>

1. <span data-ttu-id="96550-135">Conectar-se ao cluster local do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="96550-135">Connect to the local Service Fabric cluster.</span></span>

    ```bash
    azure servicefabric cluster connect
    ```

2. <span data-ttu-id="96550-136">Use o script de instalação fornecido no modelo para copiar o pacote de aplicativo no repositório de imagens do cluster, registrar o tipo de aplicativo e criar uma instância do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="96550-136">Use the install script provided in the template to copy the application package to the cluster's image store, register the application type, and create an instance of the application.</span></span>

    ```bash
    ./install.sh
    ```

3. <span data-ttu-id="96550-137">Abra um navegador e navegue até o Service Fabric Explorer em http://localhost:19080/Explorer (substitua localhost pelo IP privado da VM se estiver usando Vagrant no Mac OS X).</span><span class="sxs-lookup"><span data-stu-id="96550-137">Open a browser and navigate to Service Fabric Explorer at http://localhost:19080/Explorer (replace localhost with the private IP of the VM if using Vagrant on Mac OS X).</span></span>
4. <span data-ttu-id="96550-138">Expanda o nó Aplicativos e observe que agora há uma entrada para o seu tipo de aplicativo e outra para a primeira instância desse tipo.</span><span class="sxs-lookup"><span data-stu-id="96550-138">Expand the Applications node and note that there is now an entry for your application type and another for the first instance of that type.</span></span>
5. <span data-ttu-id="96550-139">Use o script de desinstalação fornecido com o modelo para excluir a instância do aplicativo e cancelar o registro do tipo de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="96550-139">Use the uninstall script provided in the template to delete the application instance and unregister the application type.</span></span>

    ```bash
    ./uninstall.sh
    ```

### <a name="using-azure-cli-20"></a><span data-ttu-id="96550-140">Usando a CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="96550-140">Using Azure CLI 2.0</span></span>

<span data-ttu-id="96550-141">Confira o documento de referência sobre como gerenciar um [ciclo de vida do aplicativo usando a CLI do Azure 2.0](service-fabric-application-lifecycle-azure-cli-2-0.md).</span><span class="sxs-lookup"><span data-stu-id="96550-141">See the reference doc on managing an [application life cycle using the Azure CLI 2.0](service-fabric-application-lifecycle-azure-cli-2-0.md).</span></span>

<span data-ttu-id="96550-142">Para obter um aplicativo de exemplo, [confira os códigos de exemplo de contêiner do Service Fabric no GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="96550-142">For an example application, [checkout the Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>

## <a name="adding-more-services-to-an-existing-application"></a><span data-ttu-id="96550-143">Adicionando mais serviços a um aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="96550-143">Adding more services to an existing application</span></span>

<span data-ttu-id="96550-144">Para adicionar outro serviço de contêiner a um aplicativo já criado usando `yo`, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="96550-144">To add another container service to an application already created using `yo`, perform the following steps:</span></span>

1. <span data-ttu-id="96550-145">Altere o diretório para a raiz do aplicativo existente.</span><span class="sxs-lookup"><span data-stu-id="96550-145">Change directory to the root of the existing application.</span></span>  <span data-ttu-id="96550-146">Por exemplo, `cd ~/YeomanSamples/MyApplication`, se `MyApplication` é o aplicativo criado pelo Yeoman.</span><span class="sxs-lookup"><span data-stu-id="96550-146">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is the application created by Yeoman.</span></span>
2. <span data-ttu-id="96550-147">Execute o `yo azuresfcontainer:AddService`</span><span class="sxs-lookup"><span data-stu-id="96550-147">Run `yo azuresfcontainer:AddService`</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a><span data-ttu-id="96550-148">Empacotar e implantar manualmente uma imagem de contêiner</span><span class="sxs-lookup"><span data-stu-id="96550-148">Manually package and deploy a container image</span></span>
<span data-ttu-id="96550-149">O processo de empacotamento manual de um serviço em contêiner se baseia nas seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="96550-149">The process of manually packaging a containerized service is based on the following steps:</span></span>

1. <span data-ttu-id="96550-150">Publicar os contêineres em seu repositório.</span><span class="sxs-lookup"><span data-stu-id="96550-150">Publish the containers to your repository.</span></span>
2. <span data-ttu-id="96550-151">Criar a estrutura de diretórios do pacote.</span><span class="sxs-lookup"><span data-stu-id="96550-151">Create the package directory structure.</span></span>
3. <span data-ttu-id="96550-152">Editar o arquivo de manifesto do serviço.</span><span class="sxs-lookup"><span data-stu-id="96550-152">Edit the service manifest file.</span></span>
4. <span data-ttu-id="96550-153">Editar o arquivo de manifesto do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="96550-153">Edit the application manifest file.</span></span>

## <a name="deploy-and-activate-a-container-image"></a><span data-ttu-id="96550-154">Implantar e ativar uma imagem de contêiner</span><span class="sxs-lookup"><span data-stu-id="96550-154">Deploy and activate a container image</span></span>
<span data-ttu-id="96550-155">No [modelo de aplicativo](service-fabric-application-model.md)do Service Fabric, um contêiner representa um host de aplicativo no qual várias réplicas de serviço são colocadas.</span><span class="sxs-lookup"><span data-stu-id="96550-155">In the Service Fabric [application model](service-fabric-application-model.md), a container represents an application host in which multiple service replicas are placed.</span></span> <span data-ttu-id="96550-156">Para implantar e ativar um contêiner, coloque o nome da imagem do contêiner em um elemento `ContainerHost` no manifesto do serviço.</span><span class="sxs-lookup"><span data-stu-id="96550-156">To deploy and activate a container, put the name of the container image into a `ContainerHost` element in the service manifest.</span></span>

<span data-ttu-id="96550-157">No manifesto do serviço, adicione um `ContainerHost` do ponto de entrada.</span><span class="sxs-lookup"><span data-stu-id="96550-157">In the service manifest, add a `ContainerHost` for the entry point.</span></span> <span data-ttu-id="96550-158">Em seguida, defina o `ImageName` para o nome do repositório de contêiner e imagem.</span><span class="sxs-lookup"><span data-stu-id="96550-158">Then set the `ImageName` to be the name of the container repository and image.</span></span> <span data-ttu-id="96550-159">O manifesto parcial a seguir mostra um exemplo de como implantar o contêiner chamado `myimage:v1` de um repositório chamado `myrepo`:</span><span class="sxs-lookup"><span data-stu-id="96550-159">The following partial manifest shows an example of how to deploy the container called `myimage:v1` from a repository called `myrepo`:</span></span>

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

<span data-ttu-id="96550-160">Você pode fornecer comandos de entrada especificando o elemento opcional `Commands` com uma vírgula delimitada por conjunto de comandos a serem executados dentro do contêiner.</span><span class="sxs-lookup"><span data-stu-id="96550-160">You can provide input commands by specifying the optional `Commands` element with a comma-delimited set of commands to run inside the container.</span></span>

> [!NOTE]
> <span data-ttu-id="96550-161">Se a imagem não tiver um ponto de entrada de carga de trabalho definido, em seguida, você precisa especificar explicitamente os comandos de entrada dentro do elemento `Commands` com um conjunto delimitado por vírgulas de comandos para serem executados dentro do contêiner, que manterá o contêiner em execução após a inicialização.</span><span class="sxs-lookup"><span data-stu-id="96550-161">If the image does not have a workload entry-point defined, then you need to explicitly specify input commands inside `Commands` element with a comma-delimited set of commands to run inside the container, which will keep the container running after startup.</span></span>

## <a name="understand-resource-governance"></a><span data-ttu-id="96550-162">Compreender a governança de recursos</span><span class="sxs-lookup"><span data-stu-id="96550-162">Understand resource governance</span></span>
<span data-ttu-id="96550-163">A governança de recursos é uma funcionalidade do contêiner e restringe os recursos que o contêiner pode usar no host.</span><span class="sxs-lookup"><span data-stu-id="96550-163">Resource governance is a capability of the container that restricts the resources that the container can use on the host.</span></span> <span data-ttu-id="96550-164">O `ResourceGovernancePolicy`, especificado no manifesto do aplicativo, é usado para declarar os limites de recurso para um pacote de códigos de serviço.</span><span class="sxs-lookup"><span data-stu-id="96550-164">The `ResourceGovernancePolicy`, which is specified in the application manifest is used to declare resource limits for a service code package.</span></span> <span data-ttu-id="96550-165">Limites de recursos podem ser definidos para os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="96550-165">Resource limits can be set for the following resources:</span></span>

* <span data-ttu-id="96550-166">Memória</span><span class="sxs-lookup"><span data-stu-id="96550-166">Memory</span></span>
* <span data-ttu-id="96550-167">MemorySwap</span><span class="sxs-lookup"><span data-stu-id="96550-167">MemorySwap</span></span>
* <span data-ttu-id="96550-168">CpuShares (peso relativo da CPU)</span><span class="sxs-lookup"><span data-stu-id="96550-168">CpuShares (CPU relative weight)</span></span>
* <span data-ttu-id="96550-169">MemoryReservationInMB</span><span class="sxs-lookup"><span data-stu-id="96550-169">MemoryReservationInMB</span></span>  
* <span data-ttu-id="96550-170">BlkioWeight (peso relativo do BlockIO).</span><span class="sxs-lookup"><span data-stu-id="96550-170">BlkioWeight (BlockIO relative weight).</span></span>

> [!NOTE]
> <span data-ttu-id="96550-171">Em uma versão futura, será incluído suporte para especificar limites de E/S de um bloco específico, como IOPs, leitura/gravação de BPS e outros.</span><span class="sxs-lookup"><span data-stu-id="96550-171">In a future release, support for specifying specific block IO limits such as IOPs, read/write BPS, and others will be included.</span></span>
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

## <a name="authenticate-a-repository"></a><span data-ttu-id="96550-172">Autenticar um repositório</span><span class="sxs-lookup"><span data-stu-id="96550-172">Authenticate a repository</span></span>
<span data-ttu-id="96550-173">Para baixar um contêiner, poderá ser preciso fornecer as credenciais de logon para o repositório do contêiner.</span><span class="sxs-lookup"><span data-stu-id="96550-173">To download a container, you might have to provide sign-in credentials to the container repository.</span></span> <span data-ttu-id="96550-174">As credenciais de logon especificadas no manifesto do aplicativo são usadas para especificar as informações de logon, ou a chave SSH, para baixar a imagem do contêiner do repositório de imagens.</span><span class="sxs-lookup"><span data-stu-id="96550-174">The sign-in credentials, specified in the application manifest, are used to specify the sign-in information, or SSH key, for downloading the container image from the image repository.</span></span> <span data-ttu-id="96550-175">O exemplo a seguir mostra uma conta chamada *TestUser* junto com a senha em texto não criptografado (*não* recomendado):</span><span class="sxs-lookup"><span data-stu-id="96550-175">The following example shows an account called *TestUser* along with the password in clear text (*not* recommended):</span></span>

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

<span data-ttu-id="96550-176">É recomendável que você criptografe a senha usando um certificado implantado no computador.</span><span class="sxs-lookup"><span data-stu-id="96550-176">We recommend that you encrypt the password by using a certificate that's deployed to the machine.</span></span>

<span data-ttu-id="96550-177">O exemplo a seguir mostra uma conta chamada *TestUser*, em que a senha foi criptografada usando um certificado chamado *MyCert*.</span><span class="sxs-lookup"><span data-stu-id="96550-177">The following example shows an account called *TestUser*, where the password was encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="96550-178">Você pode usar o comando `Invoke-ServiceFabricEncryptText` do PowerShell para criar o texto cifrado secreto para a senha.</span><span class="sxs-lookup"><span data-stu-id="96550-178">You can use the `Invoke-ServiceFabricEncryptText` PowerShell command to create the secret cipher text for the password.</span></span> <span data-ttu-id="96550-179">Para obter mais informações, consulte o artigo [Gerenciar segredos em aplicativos do Service Fabric](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="96550-179">For more information, see the article [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md).</span></span>

<span data-ttu-id="96550-180">A chave privada do certificado usada para descriptografar a senha deve ser implantada no computador local em um método fora de banda.</span><span class="sxs-lookup"><span data-stu-id="96550-180">The private key of the certificate that's used to decrypt the password must be deployed to the local machine in an out-of-band method.</span></span> <span data-ttu-id="96550-181">(No Azure, esse método é o Azure Resource Manager.) Em seguida, quando o Service Fabric implanta o pacote de serviço para o computador, ele poderá descriptografar o segredo.</span><span class="sxs-lookup"><span data-stu-id="96550-181">(In Azure, this method is Azure Resource Manager.) Then, when Service Fabric deploys the service package to the machine, it can decrypt the secret.</span></span> <span data-ttu-id="96550-182">Usando o segredo junto com o nome da conta, ele então pode autenticar com o repositório do contêiner.</span><span class="sxs-lookup"><span data-stu-id="96550-182">By using the secret along with the account name, it can then authenticate with the container repository.</span></span>

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

## <a name="configure-container-port-to-host-port-mapping"></a><span data-ttu-id="96550-183">Configurar mapeamento de porta do contêiner para o porta de host</span><span class="sxs-lookup"><span data-stu-id="96550-183">Configure container port-to-host port mapping</span></span>
<span data-ttu-id="96550-184">Você pode configurar uma porta de host usada para se comunicar com o contêiner especificando um `PortBinding` no manifesto do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="96550-184">You can configure a host port used to communicate with the container by specifying a `PortBinding` in the application manifest.</span></span> <span data-ttu-id="96550-185">A associação de porta mapeia a porta que o serviço está escutando dentro do contêiner para uma porta no host.</span><span class="sxs-lookup"><span data-stu-id="96550-185">The port binding maps the port to which the service is listening inside the container to a port on the host.</span></span>

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

## <a name="configure-container-to-container-discovery-and-communication"></a><span data-ttu-id="96550-186">Configurar descoberta e comunicação de contêiner para contêiner</span><span class="sxs-lookup"><span data-stu-id="96550-186">Configure container-to-container discovery and communication</span></span>
<span data-ttu-id="96550-187">Usando a política `PortBinding`, você pode mapear uma porta de contêiner para um `Endpoint` no manifesto do serviço.</span><span class="sxs-lookup"><span data-stu-id="96550-187">By using the `PortBinding` policy, you can map a container port to an `Endpoint` in the service manifest.</span></span> <span data-ttu-id="96550-188">O ponto de extremidade `Endpoint1` pode especificar uma porta fixa (por exemplo, porta 80).</span><span class="sxs-lookup"><span data-stu-id="96550-188">The endpoint `Endpoint1` can specify a fixed port (for example, port 80).</span></span> <span data-ttu-id="96550-189">Também pode especificar nenhuma porta, quando uma porta aleatória no intervalo de portas do aplicativo do cluster será escolhida para você.</span><span class="sxs-lookup"><span data-stu-id="96550-189">It can also specify no port at all, in which case a random port from the cluster's application port range is chosen for you.</span></span>

<span data-ttu-id="96550-190">Se você especificar um ponto de extremidade, usando a marca `Endpoint` no manifesto do serviço de um contêiner de convidado, o Service Fabric poderá publicar automaticamente este ponto de extremidade no serviço de Nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="96550-190">If you specify an endpoint, using the `Endpoint` tag in the service manifest of a guest container, Service Fabric can automatically publish this endpoint to the Naming service.</span></span> <span data-ttu-id="96550-191">Portanto, outros serviços que são executados no cluster podem descobrir esse contêiner usando as consultas REST para resolver.</span><span class="sxs-lookup"><span data-stu-id="96550-191">Other services that are running in the cluster can thus discover this container using the REST queries for resolving.</span></span>

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

<span data-ttu-id="96550-192">Ao se registrar com o serviço de Nomenclatura, você poderá fazer a comunicação de contêiner para contêiner facilmente no código dentro do contêiner usando o [proxy reverso](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="96550-192">By registering with the Naming service, you can easily do container-to-container communication in the code within your container by using the [reverse proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="96550-193">A comunicação é realizada fornecendo a porta de escuta de proxy reverso http e o nome dos serviços com os quais você deseja se comunicar como variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="96550-193">Communication is performed by providing the reverse proxy http listening port and the name of the services that you want to communicate with as environment variables.</span></span> <span data-ttu-id="96550-194">Para obter mais informações, confira a próxima seção.</span><span class="sxs-lookup"><span data-stu-id="96550-194">For more information, see the next section.</span></span>

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="96550-195">Configurar e definir as variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="96550-195">Configure and set environment variables</span></span>
<span data-ttu-id="96550-196">Variáveis de ambiente podem ser especificadas para cada pacote de código no manifesto de serviço, tanto para serviços implantados em contêineres quanto para serviços implantados como processos/executáveis convidados.</span><span class="sxs-lookup"><span data-stu-id="96550-196">Environment variables can be specified for each code package in the service manifest, both for services that are deployed in containers or for services that are deployed as processes/guest executables.</span></span> <span data-ttu-id="96550-197">Esses valores de variável de ambiente podem ser substituídos especialmente no manifesto do aplicativo ou especificados durante a implantação como parâmetros do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="96550-197">These environment variable values can be overridden specifically in the application manifest or specified during deployment as application parameters.</span></span>

<span data-ttu-id="96550-198">O trecho XML do manifesto do serviço a seguir mostra um exemplo de como especificar variáveis de ambiente para um pacote de códigos:</span><span class="sxs-lookup"><span data-stu-id="96550-198">The following service manifest XML snippet shows an example of how to specify environment variables for a code package:</span></span>

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

<span data-ttu-id="96550-199">Essas variáveis de ambiente podem ser substituídas no nível do manifesto do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="96550-199">These environment variables can be overridden at the application manifest level:</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

<span data-ttu-id="96550-200">No exemplo acima, especificamos um valor explícito para a variável de ambiente `HttpGateway` (19000) enquanto definimos o valor do parâmetro `BackendServiceName` é definido por meio do parâmetro de aplicativo `[BackendSvc]`.</span><span class="sxs-lookup"><span data-stu-id="96550-200">In the previous example, we specified an explicit value for the `HttpGateway` environment variable (19000), while we set the value for `BackendServiceName` parameter via the `[BackendSvc]` application parameter.</span></span> <span data-ttu-id="96550-201">Essas configurações permitem especificar o valor para `BackendServiceName`valor quando você implanta o aplicativo e não tem um valor fixo no manifesto.</span><span class="sxs-lookup"><span data-stu-id="96550-201">These settings enable you to specify the value for `BackendServiceName`value when you deploy the application and not have a fixed value in the manifest.</span></span>

## <a name="complete-examples-for-application-and-service-manifest"></a><span data-ttu-id="96550-202">Exemplos completos de aplicativo e manifesto do serviço</span><span class="sxs-lookup"><span data-stu-id="96550-202">Complete examples for application and service manifest</span></span>

<span data-ttu-id="96550-203">Aqui está um exemplo de manifesto de aplicativo:</span><span class="sxs-lookup"><span data-stu-id="96550-203">An example application manifest follows:</span></span>

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

<span data-ttu-id="96550-204">Aqui está um exemplo de manifesto de serviço (especificado no manifesto do aplicativo anterior):</span><span class="sxs-lookup"><span data-stu-id="96550-204">An example service manifest (specified in the preceding application manifest) follows:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="96550-205">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="96550-205">Next steps</span></span>
<span data-ttu-id="96550-206">Agora que você implantou um serviço em contêiner, saiba como gerenciar seu ciclo de vida lendo [ciclo de vida de aplicativos do Service Fabric](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="96550-206">Now that you have deployed a containerized service, learn how to manage its lifecycle by reading [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span></span>

* [<span data-ttu-id="96550-207">Visão geral do Service Fabric e contêineres</span><span class="sxs-lookup"><span data-stu-id="96550-207">Overview of Service Fabric and containers</span></span>](service-fabric-containers-overview.md)
* [<span data-ttu-id="96550-208">Interagindo com clusters do Service Fabric usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="96550-208">Interacting with Service Fabric clusters using the Azure CLI</span></span>](service-fabric-azure-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-deploy-container-linux/sf-container-yeoman1.png

## <a name="related-articles"></a><span data-ttu-id="96550-209">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="96550-209">Related articles</span></span>

* [<span data-ttu-id="96550-210">Introdução ao Service Fabric e a CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="96550-210">Getting started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
* [<span data-ttu-id="96550-211">Introdução à CLI XPlat do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="96550-211">Getting started with Service Fabric XPlat CLI</span></span>](service-fabric-azure-cli.md)
