---
title: "aaaCreate um aplicativo de contêiner do Azure Service Fabric no Linux | Microsoft Docs"
description: "Crie seu primeiro aplicativo de contêiner do Linux no Azure Service Fabric.  Montar uma imagem do Docker com o seu aplicativo, enviar por push o registro de contêiner Olá imagem tooa, criar e implantar um aplicativo de contêiner do Service Fabric."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/28/2017
ms.author: ryanwi
ms.openlocfilehash: 348dbcbaa1a534fb2808450e4c2d5f9acc7c7b35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-container-application-on-linux"></a><span data-ttu-id="848b4-104">Criar seu primeiro aplicativo de contêiner do Service Fabric no Linux</span><span class="sxs-lookup"><span data-stu-id="848b4-104">Create your first Service Fabric container application on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="848b4-105">Windows</span><span class="sxs-lookup"><span data-stu-id="848b4-105">Windows</span></span>](service-fabric-get-started-containers.md)
> * [<span data-ttu-id="848b4-106">Linux</span><span class="sxs-lookup"><span data-stu-id="848b4-106">Linux</span></span>](service-fabric-get-started-containers-linux.md)

<span data-ttu-id="848b4-107">Executar um aplicativo existente em um contêiner do Linux em um cluster do Service Fabric não requer qualquer aplicativo tooyour de alterações.</span><span class="sxs-lookup"><span data-stu-id="848b4-107">Running an existing application in a Linux container on a Service Fabric cluster doesn't require any changes tooyour application.</span></span> <span data-ttu-id="848b4-108">Este artigo orienta a criação de uma imagem do Docker que contém um Python [bulbo](http://flask.pocoo.org/) aplicativo e implantá-la tooa cluster de malha do serviço web.</span><span class="sxs-lookup"><span data-stu-id="848b4-108">This article walks you through creating a Docker image containing a Python [Flask](http://flask.pocoo.org/) web application and deploying it tooa Service Fabric cluster.</span></span>  <span data-ttu-id="848b4-109">Você também compartilhará seu aplicativo em contêineres pelo [Registro de Contêiner do Azure](/azure/container-registry/).</span><span class="sxs-lookup"><span data-stu-id="848b4-109">You will also share your containerized application through [Azure Container Registry](/azure/container-registry/).</span></span>  <span data-ttu-id="848b4-110">Este artigo pressupõe uma compreensão básica sobre o Docker.</span><span class="sxs-lookup"><span data-stu-id="848b4-110">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="848b4-111">Você pode aprender sobre o Docker ao ler Olá [visão geral de Docker](https://docs.docker.com/engine/understanding-docker/).</span><span class="sxs-lookup"><span data-stu-id="848b4-111">You can learn about Docker by reading hello [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="848b4-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="848b4-112">Prerequisites</span></span>
* <span data-ttu-id="848b4-113">Um computador de desenvolvimento executando:</span><span class="sxs-lookup"><span data-stu-id="848b4-113">A development computer running:</span></span>
  * <span data-ttu-id="848b4-114">[Ferramentas e SDK do Service Fabric](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="848b4-114">[Service Fabric SDK and tools](service-fabric-get-started-linux.md).</span></span>
  * <span data-ttu-id="848b4-115">[Docker CE para Linux](https://docs.docker.com/engine/installation/#prior-releases).</span><span class="sxs-lookup"><span data-stu-id="848b4-115">[Docker CE for Linux](https://docs.docker.com/engine/installation/#prior-releases).</span></span> 
  * [<span data-ttu-id="848b4-116">CLI do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="848b4-116">Service Fabric CLI</span></span>](service-fabric-cli.md)

* <span data-ttu-id="848b4-117">Um registro no Registro de Contêiner do Azure - [Crie um registro de contêiner](../container-registry/container-registry-get-started-portal.md) em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="848b4-117">A registry in Azure Container Registry - [Create a container registry](../container-registry/container-registry-get-started-portal.md) in your Azure subscription.</span></span> 

## <a name="define-hello-docker-container"></a><span data-ttu-id="848b4-118">Definir o contêiner do Docker Olá</span><span class="sxs-lookup"><span data-stu-id="848b4-118">Define hello Docker container</span></span>
<span data-ttu-id="848b4-119">Criar uma imagem com base em Olá [imagem Python](https://hub.docker.com/_/python/) localizado no Hub do Docker.</span><span class="sxs-lookup"><span data-stu-id="848b4-119">Build an image based on hello [Python image](https://hub.docker.com/_/python/) located on Docker Hub.</span></span> 

<span data-ttu-id="848b4-120">Defina o contêiner do Docker em um Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="848b4-120">Define your Docker container in a Dockerfile.</span></span> <span data-ttu-id="848b4-121">Olá Dockerfile contém instruções para a configuração de ambiente hello dentro de seu contêiner, carregar o aplicativo hello deseja toorun e mapear portas.</span><span class="sxs-lookup"><span data-stu-id="848b4-121">hello Dockerfile contains instructions for setting up hello environment inside your container, loading hello application you want toorun, and mapping ports.</span></span> <span data-ttu-id="848b4-122">Olá Dockerfile é toohello de entrada hello `docker build` comando, que cria a imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="848b4-122">hello Dockerfile is hello input toohello `docker build` command, which creates hello image.</span></span> 

<span data-ttu-id="848b4-123">Criar um diretório vazio e criar o arquivo hello *Dockerfile* (com nenhuma extensão de arquivo).</span><span class="sxs-lookup"><span data-stu-id="848b4-123">Create an empty directory and create hello file *Dockerfile* (with no file extension).</span></span> <span data-ttu-id="848b4-124">Adicionar Olá seguir muito*Dockerfile* e salve as alterações:</span><span class="sxs-lookup"><span data-stu-id="848b4-124">Add hello following too*Dockerfile* and save your changes:</span></span>

```
# Use an official Python runtime as a base image
FROM python:2.7-slim

# Set hello working directory too/app
WORKDIR /app

# Copy hello current directory contents into hello container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when hello container launches
CMD ["python", "app.py"]
```

<span data-ttu-id="848b4-125">Saudação de leitura [referência do Dockerfile](https://docs.docker.com/engine/reference/builder/) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="848b4-125">Read hello [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for more information.</span></span>

## <a name="create-a-simple-web-application"></a><span data-ttu-id="848b4-126">Criar um aplicativo Web simples</span><span class="sxs-lookup"><span data-stu-id="848b4-126">Create a simple web application</span></span>
<span data-ttu-id="848b4-127">Crie um aplicativo Web Flask que escuta a porta 80 retornar "Olá, Mundo!".</span><span class="sxs-lookup"><span data-stu-id="848b4-127">Create a Flask web application listening on port 80 that returns "Hello World!".</span></span>  <span data-ttu-id="848b4-128">Em Olá mesmo diretório, crie o arquivo hello *requirements.txt*.</span><span class="sxs-lookup"><span data-stu-id="848b4-128">In hello same directory, create hello file *requirements.txt*.</span></span>  <span data-ttu-id="848b4-129">Adicione o seguinte de saudação e salve as alterações:</span><span class="sxs-lookup"><span data-stu-id="848b4-129">Add hello following and save your changes:</span></span>
```
Flask
```

<span data-ttu-id="848b4-130">Também criar hello *app.py* de arquivo e adicione Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="848b4-130">Also create hello *app.py* file and add hello following:</span></span>

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():
    
    return 'Hello World!'

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

## <a name="build-hello-image"></a><span data-ttu-id="848b4-131">Criar imagem Olá</span><span class="sxs-lookup"><span data-stu-id="848b4-131">Build hello image</span></span>
<span data-ttu-id="848b4-132">Executar Olá `docker build` imagem de saudação do comando toocreate que executa o aplicativo da web.</span><span class="sxs-lookup"><span data-stu-id="848b4-132">Run hello `docker build` command toocreate hello image that runs your web application.</span></span> <span data-ttu-id="848b4-133">Abra uma janela do PowerShell e navegue muito*c:\temp\helloworldapp*.</span><span class="sxs-lookup"><span data-stu-id="848b4-133">Open a PowerShell window and navigate too*c:\temp\helloworldapp*.</span></span> <span data-ttu-id="848b4-134">Execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="848b4-134">Run hello following command:</span></span>

```bash
docker build -t helloworldapp .
```

<span data-ttu-id="848b4-135">Este comando compilações Olá nova imagem usando as instruções de saudação em seu Dockerfile, nomear (-t marcação) imagem hello "helloworldapp".</span><span class="sxs-lookup"><span data-stu-id="848b4-135">This command builds hello new image using hello instructions in your Dockerfile, naming (-t tagging) hello image "helloworldapp".</span></span> <span data-ttu-id="848b4-136">Criando uma imagem extrai imagem base Olá para baixo do Hub do Docker e cria uma nova imagem que adiciona o seu aplicativo na parte superior da imagem base hello.</span><span class="sxs-lookup"><span data-stu-id="848b4-136">Building an image pulls hello base image down from Docker Hub and creates a new image that adds your application on top of hello base image.</span></span>  

<span data-ttu-id="848b4-137">Após a conclusão do comando de compilação hello, executar Olá `docker images` informações toosee na nova imagem de saudação do comando:</span><span class="sxs-lookup"><span data-stu-id="848b4-137">Once hello build command completes, run hello `docker images` command toosee information on hello new image:</span></span>

```bash
$ docker images
    
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              86838648aab6        2 minutes ago       194 MB
```

## <a name="run-hello-application-locally"></a><span data-ttu-id="848b4-138">Executar o aplicativo hello localmente</span><span class="sxs-lookup"><span data-stu-id="848b4-138">Run hello application locally</span></span>
<span data-ttu-id="848b4-139">Verifique se que seu aplicativo em contêineres é executado localmente antes de enviar por push-registro de contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="848b4-139">Verify that your containerized application runs locally before pushing it hello container registry.</span></span>  

<span data-ttu-id="848b4-140">Executar o aplicativo hello, mapeamento do contêiner do seu computador porta 4000 toohello expostos a porta 80:</span><span class="sxs-lookup"><span data-stu-id="848b4-140">Run hello application, mapping your computer's port 4000 toohello container's exposed port 80:</span></span>

```bash
docker run -d -p 4000:80 --name my-web-site helloworldapp
```

<span data-ttu-id="848b4-141">*nome* oferece um toohello nome executando contêiner (em vez de ID de contêiner de saudação).</span><span class="sxs-lookup"><span data-stu-id="848b4-141">*name* gives a name toohello running container (instead of hello container ID).</span></span>

<span data-ttu-id="848b4-142">Conecte-se toohello executando o contêiner.</span><span class="sxs-lookup"><span data-stu-id="848b4-142">Connect toohello running container.</span></span>  <span data-ttu-id="848b4-143">Abra um navegador da web apontando toohello endereço IP retornado na porta 4000, por exemplo "http://localhost:4000".</span><span class="sxs-lookup"><span data-stu-id="848b4-143">Open a web browser pointing toohello IP address returned on port 4000, for example "http://localhost:4000".</span></span> <span data-ttu-id="848b4-144">Você deve ver Olá título "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="848b4-144">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="848b4-145">Exibir no navegador de saudação.</span><span class="sxs-lookup"><span data-stu-id="848b4-145">display in hello browser.</span></span>

![Olá, Mundo!][hello-world]

<span data-ttu-id="848b4-147">toostop seu contêiner, execute:</span><span class="sxs-lookup"><span data-stu-id="848b4-147">toostop your container, run:</span></span>

```bash
docker stop my-web-site
```

<span data-ttu-id="848b4-148">Exclua contêiner de saudação do seu computador de desenvolvimento:</span><span class="sxs-lookup"><span data-stu-id="848b4-148">Delete hello container from your development machine:</span></span>

```bash
docker rm my-web-site
```

## <a name="push-hello-image-toohello-container-registry"></a><span data-ttu-id="848b4-149">Registro de contêiner do push Olá imagem toohello</span><span class="sxs-lookup"><span data-stu-id="848b4-149">Push hello image toohello container registry</span></span>
<span data-ttu-id="848b4-150">Depois de verificar que o aplicativo hello é executado no Docker, enviar por push do registro do hello imagem tooyour no registro de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="848b4-150">After you verify that hello application runs in Docker, push hello image tooyour registry in Azure Container Registry.</span></span>

<span data-ttu-id="848b4-151">Executar `docker login` toolog tooyour registro de contêiner com o [credenciais de registro](../container-registry/container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="848b4-151">Run `docker login` toolog in tooyour container registry with your [registry credentials](../container-registry/container-registry-authentication.md).</span></span>

<span data-ttu-id="848b4-152">Olá exemplo a seguir passa Olá ID e a senha de um Active Directory do Azure [entidade de serviço](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="848b4-152">hello following example passes hello ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="848b4-153">Por exemplo, você pode ter atribuído um registro de tooyour principal do serviço para um cenário de automação.</span><span class="sxs-lookup"><span data-stu-id="848b4-153">For example, you might have assigned a service principal tooyour registry for an automation scenario.</span></span>  <span data-ttu-id="848b4-154">Ou pode fazer logon usando o nome de usuário e a senha do registro.</span><span class="sxs-lookup"><span data-stu-id="848b4-154">Or, you could login using your registry username and password.</span></span>

```bash
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="848b4-155">Olá comando a seguir cria uma marca, ou alias, da imagem hello, com um registro de tooyour caminho totalmente qualificado.</span><span class="sxs-lookup"><span data-stu-id="848b4-155">hello following command creates a tag, or alias, of hello image, with a fully qualified path tooyour registry.</span></span> <span data-ttu-id="848b4-156">Este exemplo casas Olá imagem no hello `samples` namespace tooavoid desordem na raiz de saudação do registro hello.</span><span class="sxs-lookup"><span data-stu-id="848b4-156">This example places hello image in hello `samples` namespace tooavoid clutter in hello root of hello registry.</span></span>

```bash
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

<span data-ttu-id="848b4-157">Registro de push Olá imagem tooyour contêiner:</span><span class="sxs-lookup"><span data-stu-id="848b4-157">Push hello image tooyour container registry:</span></span>

```bash
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="package-hello-docker-image-with-yeoman"></a><span data-ttu-id="848b4-158">Imagem de Docker de saudação do pacote com Yeoman</span><span class="sxs-lookup"><span data-stu-id="848b4-158">Package hello Docker image with Yeoman</span></span>
<span data-ttu-id="848b4-159">Olá SDK do Service Fabric para Linux inclui um [Yeoman](http://yeoman.io/) gerador que torna mais fácil toocreate seu aplicativo e adicione uma imagem de contêiner.</span><span class="sxs-lookup"><span data-stu-id="848b4-159">hello Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy toocreate your application and add a container image.</span></span> <span data-ttu-id="848b4-160">Vamos usar Yeoman toocreate chamado de um aplicativo com um único contêiner de Docker *SimpleContainerApp*.</span><span class="sxs-lookup"><span data-stu-id="848b4-160">Let's use Yeoman toocreate an application with a single Docker container called *SimpleContainerApp*.</span></span>

<span data-ttu-id="848b4-161">toocreate um aplicativo de contêiner de serviço de malha, abra uma janela do terminal e execute `yo azuresfcontainer`.</span><span class="sxs-lookup"><span data-stu-id="848b4-161">toocreate a Service Fabric container application, open a terminal window and run `yo azuresfcontainer`.</span></span>  

<span data-ttu-id="848b4-162">Dê um nome para o seu aplicativo (por exemplo, “mycontainer”).</span><span class="sxs-lookup"><span data-stu-id="848b4-162">Name your application (for example, "mycontainer").</span></span> 

<span data-ttu-id="848b4-163">Forneça a URL de saudação para imagem de contêiner de saudação em um registro de contêiner (por exemplo, "").</span><span class="sxs-lookup"><span data-stu-id="848b4-163">Provide hello URL for hello container image in a container registry (for example, "").</span></span> 

<span data-ttu-id="848b4-164">Esta imagem tem uma carga de trabalho-ponto de entrada definido, portanto precisa tooexplicitly especificar comandos de entrada (comandos executados dentro do contêiner Olá que manterá o contêiner de saudação em execução após a inicialização).</span><span class="sxs-lookup"><span data-stu-id="848b4-164">This image has a workload entry-point defined, so need tooexplicitly specify input commands (commands run inside hello container, which will keep hello container running after startup).</span></span> 

<span data-ttu-id="848b4-165">Especifique a contagem de instâncias como "1".</span><span class="sxs-lookup"><span data-stu-id="848b4-165">Specify an instance count of "1".</span></span>

![Gerador de Yeoman do Service Fabric para contêineres][sf-yeoman]

## <a name="configure-port-mapping-and-container-repository-authentication"></a><span data-ttu-id="848b4-167">Configurar a autenticação de repositório de contêiner e o mapeamento de porta</span><span class="sxs-lookup"><span data-stu-id="848b4-167">Configure port mapping and container repository authentication</span></span>
<span data-ttu-id="848b4-168">O serviço em contêineres precisa de um ponto de extremidade para comunicação.</span><span class="sxs-lookup"><span data-stu-id="848b4-168">Your containerized service needs an endpoint for communication.</span></span>  <span data-ttu-id="848b4-169">Agora adicione Olá protocolo, porta e tipo tooan `Endpoint` no arquivo ServiceManifest.xml de saudação.</span><span class="sxs-lookup"><span data-stu-id="848b4-169">Now add hello protocol, port, and type tooan `Endpoint` in hello ServiceManifest.xml file.</span></span> <span data-ttu-id="848b4-170">Neste artigo, o serviço de saudação em contêineres escuta na porta 4000:</span><span class="sxs-lookup"><span data-stu-id="848b4-170">For this article, hello containerized service listens on port 4000:</span></span> 

```xml
<Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
```
<span data-ttu-id="848b4-171">Fornecendo Olá `UriScheme` automaticamente registra Olá ponto de extremidade de contêiner com hello serviço de nomeação de malha do serviço de descoberta.</span><span class="sxs-lookup"><span data-stu-id="848b4-171">Providing hello `UriScheme` automatically registers hello container endpoint with hello Service Fabric Naming service for discoverability.</span></span> <span data-ttu-id="848b4-172">Um arquivo de exemplo ServiceManifest.xml completo é fornecido no final deste artigo hello.</span><span class="sxs-lookup"><span data-stu-id="848b4-172">A full ServiceManifest.xml example file is provided at hello end of this article.</span></span> 

<span data-ttu-id="848b4-173">Configurar o mapeamento de porta de host de contêiner porta Olá especificando um `PortBinding` política no `ContainerHostPolicies` do arquivo applicationmanifest. XML de saudação.</span><span class="sxs-lookup"><span data-stu-id="848b4-173">Configure hello container port-to-host port mapping by specifying a `PortBinding` policy in `ContainerHostPolicies` of hello ApplicationManifest.xml file.</span></span>  <span data-ttu-id="848b4-174">Neste artigo, `ContainerPort` é 80 (contêiner Olá expõe a porta 80, Olá especificado no Dockerfile) e `EndpointRef` é "myserviceTypeEndpoint" (ponto de extremidade Olá definido no manifesto do serviço de saudação).</span><span class="sxs-lookup"><span data-stu-id="848b4-174">For this article, `ContainerPort` is 80 (hello container exposes port 80, as specified in hello Dockerfile) and `EndpointRef` is "myserviceTypeEndpoint" (hello endpoint defined in hello service manifest).</span></span>  <span data-ttu-id="848b4-175">Solicitações de entrada toohello na porta 4000 são mapeados tooport 80 no contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="848b4-175">Incoming requests toohello service on port 4000 are mapped tooport 80 on hello container.</span></span>  <span data-ttu-id="848b4-176">Se o contêiner deve tooauthenticate com um repositório privado, em seguida, adicione `RepositoryCredentials`.</span><span class="sxs-lookup"><span data-stu-id="848b4-176">If your container needs tooauthenticate with a private repository, then add `RepositoryCredentials`.</span></span>  <span data-ttu-id="848b4-177">Neste artigo, adicione Olá nome e a senha para o registro de contêiner myregistry.azurecr.io hello.</span><span class="sxs-lookup"><span data-stu-id="848b4-177">For this article, add hello account name and password for hello myregistry.azurecr.io container registry.</span></span> 

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

## <a name="build-and-package-hello-service-fabric-application"></a><span data-ttu-id="848b4-178">Compilação e o pacote de aplicativo do Service Fabric hello</span><span class="sxs-lookup"><span data-stu-id="848b4-178">Build and package hello Service Fabric application</span></span>
<span data-ttu-id="848b4-179">modelos de serviço do Fabric Yeoman Olá incluem um script de compilação para [Gradle](https://gradle.org/), que você pode usar o aplicativo hello toobuild Olá terminal.</span><span class="sxs-lookup"><span data-stu-id="848b4-179">hello Service Fabric Yeoman templates include a build script for [Gradle](https://gradle.org/), which you can use toobuild hello application from hello terminal.</span></span> <span data-ttu-id="848b4-180">toobuild e pacote de aplicativo hello, execute Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="848b4-180">toobuild and package hello application, run hello following:</span></span>

```bash
cd mycontainer
gradle
```

## <a name="deploy-hello-application"></a><span data-ttu-id="848b4-181">Implantar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="848b4-181">Deploy hello application</span></span>
<span data-ttu-id="848b4-182">Depois que o aplicativo hello é criado, você pode implantá-lo usando Olá CLI de malha do serviço de cluster local do toohello.</span><span class="sxs-lookup"><span data-stu-id="848b4-182">Once hello application is built, you can deploy it toohello local cluster using hello Service Fabric CLI.</span></span>

<span data-ttu-id="848b4-183">Conecte-se toohello cluster de malha do serviço local.</span><span class="sxs-lookup"><span data-stu-id="848b4-183">Connect toohello local Service Fabric cluster.</span></span>

```bash
sfctl cluster select --endpoint http://localhost:19080
```

<span data-ttu-id="848b4-184">Olá Use o script de instalação fornecidas no hello modelo toocopy aplicativo hello pacote repositório de imagens do cluster toohello, registrar o tipo de aplicativo hello e criar uma instância do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="848b4-184">Use hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

```bash
./install.sh
```

<span data-ttu-id="848b4-185">Abra um navegador e navegue tooService Fabric Explorer no http://localhost:19080/Explorer (substitua localhost com IP privada Olá Olá VM se usando Vagrant no Mac OS X).</span><span class="sxs-lookup"><span data-stu-id="848b4-185">Open a browser and navigate tooService Fabric Explorer at http://localhost:19080/Explorer (replace localhost with hello private IP of hello VM if using Vagrant on Mac OS X).</span></span> <span data-ttu-id="848b4-186">Expanda o nó de aplicativos hello e observe que agora há uma entrada para o tipo de aplicativo e outro para Olá primeira instância desse tipo.</span><span class="sxs-lookup"><span data-stu-id="848b4-186">Expand hello Applications node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>

<span data-ttu-id="848b4-187">Conecte-se toohello executando o contêiner.</span><span class="sxs-lookup"><span data-stu-id="848b4-187">Connect toohello running container.</span></span>  <span data-ttu-id="848b4-188">Abra um navegador da web apontando toohello endereço IP retornado na porta 4000, por exemplo "http://localhost:4000".</span><span class="sxs-lookup"><span data-stu-id="848b4-188">Open a web browser pointing toohello IP address returned on port 4000, for example "http://localhost:4000".</span></span> <span data-ttu-id="848b4-189">Você deve ver Olá título "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="848b4-189">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="848b4-190">Exibir no navegador de saudação.</span><span class="sxs-lookup"><span data-stu-id="848b4-190">display in hello browser.</span></span>

![Olá, Mundo!][hello-world]

## <a name="clean-up"></a><span data-ttu-id="848b4-192">Limpar</span><span class="sxs-lookup"><span data-stu-id="848b4-192">Clean up</span></span>
<span data-ttu-id="848b4-193">Usar script de desinstalação Olá fornecido na instância do aplicativo hello modelo toodelete saudação do cluster de desenvolvimento local hello e cancelar o registro do tipo de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="848b4-193">Use hello uninstall script provided in hello template toodelete hello application instance from hello local development cluster and unregister hello application type.</span></span>

```bash
./uninstall.sh
```

<span data-ttu-id="848b4-194">Depois que você enviar por push o registro de contêiner de toohello Olá imagem, você pode excluir imagem local saudação do seu computador de desenvolvimento:</span><span class="sxs-lookup"><span data-stu-id="848b4-194">After you push hello image toohello container registry you can delete hello local image from your development computer:</span></span>

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a><span data-ttu-id="848b4-195">Exemplo completo de manifestos de serviço e aplicativo do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="848b4-195">Complete example Service Fabric application and service manifests</span></span>
<span data-ttu-id="848b4-196">Aqui estão os manifestos de aplicativo usados neste artigo e serviço completo hello.</span><span class="sxs-lookup"><span data-stu-id="848b4-196">Here are hello complete service and application manifests used in this article.</span></span>

### <a name="servicemanifestxml"></a><span data-ttu-id="848b4-197">ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="848b4-197">ServiceManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="myservicePkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         hello UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="myserviceType" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers 
      tooService Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
        <Commands></Commands>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables tooyour container: -->
    
    <EnvironmentVariables>
      <!--
      <EnvironmentVariable Name="VariableName" Value="VariableValue"/>
      -->
    </EnvironmentVariables>
    
  </CodePackage>

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a><span data-ttu-id="848b4-198">ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="848b4-198">ApplicationManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="mycontainerType"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion 
       should match hello Name and Version attributes of hello ServiceManifest element defined in hello 
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="myservicePkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <Policies>
      <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
      </ContainerHostPolicies>
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types, when an instance of this 
         application type is created. You can also create one or more instances of service type using hello 
         ServiceFabric PowerShell module.
         
         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="myservice">
      <!-- On a local development cluster, set InstanceCount too1.  On a multi-node production 
      cluster, set InstanceCount too-1 for hello container service toorun on every node in 
      hello cluster.
      -->
      <StatelessService ServiceTypeName="myserviceType" InstanceCount="1">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```
## <a name="adding-more-services-tooan-existing-application"></a><span data-ttu-id="848b4-199">Adicionar mais serviços tooan aplicativo</span><span class="sxs-lookup"><span data-stu-id="848b4-199">Adding more services tooan existing application</span></span>

<span data-ttu-id="848b4-200">outro aplicativo de contêiner serviço tooan já criado usando yeoman, executar a tooadd Olá seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="848b4-200">tooadd another container service tooan application already created using yeoman, perform hello following steps:</span></span>

1. <span data-ttu-id="848b4-201">Alterar o diretório raiz de toohello do aplicativo existente hello.</span><span class="sxs-lookup"><span data-stu-id="848b4-201">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="848b4-202">Por exemplo, `cd ~/YeomanSamples/MyApplication`, se `MyApplication` é um aplicativo hello criado por Yeoman.</span><span class="sxs-lookup"><span data-stu-id="848b4-202">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="848b4-203">Execute o `yo azuresfcontainer:AddService`</span><span class="sxs-lookup"><span data-stu-id="848b4-203">Run `yo azuresfcontainer:AddService`</span></span>

<a id="manually"></a>


## <a name="configure-time-interval-before-container-is-force-terminated"></a><span data-ttu-id="848b4-204">Configurar o intervalo de tempo antes do contêiner ser forçado a terminar</span><span class="sxs-lookup"><span data-stu-id="848b4-204">Configure time interval before container is force terminated</span></span>

<span data-ttu-id="848b4-205">Você pode configurar um intervalo de tempo para Olá toowait de tempo de execução antes de contêiner de saudação é removida depois hello exclusão de serviço (ou um nó de tooanother mover) foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="848b4-205">You can configure a time interval for hello runtime toowait before hello container is removed after hello service deletion (or a move tooanother node) has started.</span></span> <span data-ttu-id="848b4-206">Configurando intervalo de tempo de saudação envia Olá `docker stop <time in seconds>` contêiner de toohello de comando.</span><span class="sxs-lookup"><span data-stu-id="848b4-206">Configuring hello time interval sends hello `docker stop <time in seconds>` command toohello container.</span></span>   <span data-ttu-id="848b4-207">Para obter mais detalhes, consulte [parar docker](https://docs.docker.com/engine/reference/commandline/stop/).</span><span class="sxs-lookup"><span data-stu-id="848b4-207">For more detail, see [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span></span> <span data-ttu-id="848b4-208">Olá toowait de intervalo de tempo especificado em Olá `Hosting` seção.</span><span class="sxs-lookup"><span data-stu-id="848b4-208">hello time interval toowait is specified under hello `Hosting` section.</span></span> <span data-ttu-id="848b4-209">Olá trecho do manifesto de cluster a seguir mostra como o intervalo de espera tooset hello:</span><span class="sxs-lookup"><span data-stu-id="848b4-209">hello following cluster manifest snippet shows how tooset hello wait interval:</span></span>

```xml
{
        "name": "Hosting",
        "parameters": [
          {
            "ContainerDeactivationTimeout": "10",
          ...
          }
        ]
}
```
<span data-ttu-id="848b4-210">Olá intervalo de tempo padrão é definido too10 segundos.</span><span class="sxs-lookup"><span data-stu-id="848b4-210">hello default time interval is set too10 seconds.</span></span> <span data-ttu-id="848b4-211">Como essa configuração é dinâmica, uma configuração só atualizar no tempo limite de saudação de atualizações de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="848b4-211">Since this configuration is dynamic, a config only upgrade on hello cluster updates hello timeout.</span></span> 


## <a name="configure-hello-runtime-tooremove-unused-container-images"></a><span data-ttu-id="848b4-212">Configurar Olá runtime tooremove imagens de contêiner não utilizado</span><span class="sxs-lookup"><span data-stu-id="848b4-212">Configure hello runtime tooremove unused container images</span></span>

<span data-ttu-id="848b4-213">Você pode configurar Olá Service Fabric cluster tooremove imagens de contêiner não utilizados do nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="848b4-213">You can configure hello Service Fabric cluster tooremove unused container images from hello node.</span></span> <span data-ttu-id="848b4-214">Essa configuração permite toobe de espaço em disco retomou se houver muitas imagens de contêiner no nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="848b4-214">This configuration allows disk space toobe recaptured if too many container images are present on hello node.</span></span>  <span data-ttu-id="848b4-215">tooenable deste recurso, a atualização Olá `Hosting` seção no manifesto do cluster hello, conforme mostrado no hello trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="848b4-215">tooenable this feature, update hello `Hosting` section in hello cluster manifest as shown in hello following snippet:</span></span> 


```xml
{
        "name": "Hosting",
        "parameters": [
          {
            "PruneContainerImages": “True”,
            "ContainerImagesToSkip": "microsoft/windowsservercore|microsoft/nanoserver|…",
          ...
          }
        ]
} 
```

<span data-ttu-id="848b4-216">Para as imagens que não devem ser excluídas, você poderá especificá-los em Olá `ContainerImagesToSkip` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="848b4-216">For images that should not be deleted, you can specify them under hello `ContainerImagesToSkip` parameter.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="848b4-217">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="848b4-217">Next steps</span></span>
* <span data-ttu-id="848b4-218">Saiba mais sobre como executar [contêineres no Service Fabric](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="848b4-218">Learn more about running [containers on Service Fabric](service-fabric-containers-overview.md).</span></span>
* <span data-ttu-id="848b4-219">Saudação de leitura [implantar um aplicativo .NET em um contêiner](service-fabric-host-app-in-a-container.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="848b4-219">Read hello [Deploy a .NET application in a container](service-fabric-host-app-in-a-container.md) tutorial.</span></span>
* <span data-ttu-id="848b4-220">Saiba mais sobre Olá Service Fabric [ciclo de vida do aplicativo](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="848b4-220">Learn about hello Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
* <span data-ttu-id="848b4-221">Saudação de check-out [exemplos de código do contêiner do Service Fabric](https://github.com/Azure-Samples/service-fabric-dotnet-containers) no GitHub.</span><span class="sxs-lookup"><span data-stu-id="848b4-221">Checkout hello [Service Fabric container code samples](https://github.com/Azure-Samples/service-fabric-dotnet-containers) on GitHub.</span></span>

[hello-world]: ./media/service-fabric-get-started-containers-linux/HelloWorld.png
[sf-yeoman]: ./media/service-fabric-get-started-containers-linux/YoSF.png
