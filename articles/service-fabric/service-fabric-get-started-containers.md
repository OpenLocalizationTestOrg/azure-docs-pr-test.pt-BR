---
title: "aaaCreate um aplicativo de contêiner do Azure Service Fabric | Microsoft Docs"
description: "Crie seu primeiro aplicativo de contêiner do Windows no Azure Service Fabric.  Montar uma imagem do Docker com um aplicativo de Python, enviar por push o registro de contêiner Olá imagem tooa, criar e implantar um aplicativo de contêiner do Service Fabric."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: vturecek
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/18/2017
ms.author: ryanwi
ms.openlocfilehash: b79d3a41eb2da5f7791266588fe9ea7becb0e58f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-container-application-on-windows"></a><span data-ttu-id="cca01-104">Como criar seu primeiro aplicativo de contêiner do Service Fabric no Windows</span><span class="sxs-lookup"><span data-stu-id="cca01-104">Create your first Service Fabric container application on Windows</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cca01-105">Windows</span><span class="sxs-lookup"><span data-stu-id="cca01-105">Windows</span></span>](service-fabric-get-started-containers.md)
> * [<span data-ttu-id="cca01-106">Linux</span><span class="sxs-lookup"><span data-stu-id="cca01-106">Linux</span></span>](service-fabric-get-started-containers-linux.md)

<span data-ttu-id="cca01-107">Executando um aplicativo existente em um contêiner do Windows em um cluster do Service Fabric não requer qualquer aplicativo tooyour de alterações.</span><span class="sxs-lookup"><span data-stu-id="cca01-107">Running an existing application in a Windows container on a Service Fabric cluster doesn't require any changes tooyour application.</span></span> <span data-ttu-id="cca01-108">Este artigo orienta a criação de uma imagem do Docker que contém um Python [bulbo](http://flask.pocoo.org/) aplicativo e implantá-la tooa cluster de malha do serviço web.</span><span class="sxs-lookup"><span data-stu-id="cca01-108">This article walks you through creating a Docker image containing a Python [Flask](http://flask.pocoo.org/) web application and deploying it tooa Service Fabric cluster.</span></span>  <span data-ttu-id="cca01-109">Você também compartilhará seu aplicativo em contêineres pelo [Registro de Contêiner do Azure](/azure/container-registry/).</span><span class="sxs-lookup"><span data-stu-id="cca01-109">You will also share your containerized application through [Azure Container Registry](/azure/container-registry/).</span></span>  <span data-ttu-id="cca01-110">Este artigo pressupõe uma compreensão básica sobre o Docker.</span><span class="sxs-lookup"><span data-stu-id="cca01-110">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="cca01-111">Você pode aprender sobre o Docker ao ler Olá [visão geral de Docker](https://docs.docker.com/engine/understanding-docker/).</span><span class="sxs-lookup"><span data-stu-id="cca01-111">You can learn about Docker by reading hello [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cca01-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cca01-112">Prerequisites</span></span>
<span data-ttu-id="cca01-113">Um computador de desenvolvimento executando:</span><span class="sxs-lookup"><span data-stu-id="cca01-113">A development computer running:</span></span>
* <span data-ttu-id="cca01-114">Visual Studio 2015 ou Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="cca01-114">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="cca01-115">[Ferramentas e SDK do Service Fabric](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="cca01-115">[Service Fabric SDK and tools](service-fabric-get-started.md).</span></span>
*  <span data-ttu-id="cca01-116">Docker para Windows.</span><span class="sxs-lookup"><span data-stu-id="cca01-116">Docker for Windows.</span></span>  <span data-ttu-id="cca01-117">[Obter Docker CE para o Windows (estável)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description).</span><span class="sxs-lookup"><span data-stu-id="cca01-117">[Get Docker CE for Windows (stable)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description).</span></span> <span data-ttu-id="cca01-118">Depois de instalar e iniciar o Docker, com o botão direito no ícone de bandeja hello e selecione **alternar contêineres tooWindows**.</span><span class="sxs-lookup"><span data-stu-id="cca01-118">After installing and starting Docker, right-click on hello tray icon and select **Switch tooWindows containers**.</span></span> <span data-ttu-id="cca01-119">Isso é necessário toorun imagens do Docker com base no Windows.</span><span class="sxs-lookup"><span data-stu-id="cca01-119">This is required toorun Docker images based on Windows.</span></span>

<span data-ttu-id="cca01-120">Um cluster do Windows com três ou mais nós em execução no Windows Server 2016 com contêineres - [Criar um cluster](service-fabric-cluster-creation-via-portal.md) ou [experimente o Service Fabric gratuitamente](https://aka.ms/tryservicefabric).</span><span class="sxs-lookup"><span data-stu-id="cca01-120">A Windows cluster with three or more nodes running on Windows Server 2016 with Containers- [Create a cluster](service-fabric-cluster-creation-via-portal.md) or [try Service Fabric for free](https://aka.ms/tryservicefabric).</span></span>

<span data-ttu-id="cca01-121">Um registro no Registro de Contêiner do Azure - [Crie um registro de contêiner](../container-registry/container-registry-get-started-portal.md) em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="cca01-121">A registry in Azure Container Registry - [Create a container registry](../container-registry/container-registry-get-started-portal.md) in your Azure subscription.</span></span>

## <a name="define-hello-docker-container"></a><span data-ttu-id="cca01-122">Definir o contêiner do Docker Olá</span><span class="sxs-lookup"><span data-stu-id="cca01-122">Define hello Docker container</span></span>
<span data-ttu-id="cca01-123">Criar uma imagem com base em Olá [imagem Python](https://hub.docker.com/_/python/) localizado no Hub do Docker.</span><span class="sxs-lookup"><span data-stu-id="cca01-123">Build an image based on hello [Python image](https://hub.docker.com/_/python/) located on Docker Hub.</span></span>

<span data-ttu-id="cca01-124">Defina o contêiner do Docker em um Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="cca01-124">Define your Docker container in a Dockerfile.</span></span> <span data-ttu-id="cca01-125">Olá Dockerfile contém instruções para a configuração de ambiente hello dentro de seu contêiner, carregar o aplicativo hello deseja toorun e mapear portas.</span><span class="sxs-lookup"><span data-stu-id="cca01-125">hello Dockerfile contains instructions for setting up hello environment inside your container, loading hello application you want toorun, and mapping ports.</span></span> <span data-ttu-id="cca01-126">Olá Dockerfile é toohello de entrada hello `docker build` comando, que cria a imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="cca01-126">hello Dockerfile is hello input toohello `docker build` command, which creates hello image.</span></span>

<span data-ttu-id="cca01-127">Criar um diretório vazio e criar o arquivo hello *Dockerfile* (com nenhuma extensão de arquivo).</span><span class="sxs-lookup"><span data-stu-id="cca01-127">Create an empty directory and create hello file *Dockerfile* (with no file extension).</span></span> <span data-ttu-id="cca01-128">Adicionar Olá seguir muito*Dockerfile* e salve as alterações:</span><span class="sxs-lookup"><span data-stu-id="cca01-128">Add hello following too*Dockerfile* and save your changes:</span></span>

```
# Use an official Python runtime as a base image
FROM python:2.7-windowsservercore

# Set hello working directory too/app
WORKDIR /app

# Copy hello current directory contents into hello container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available toohello world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when hello container launches
CMD ["python", "app.py"]
```

<span data-ttu-id="cca01-129">Saudação de leitura [referência do Dockerfile](https://docs.docker.com/engine/reference/builder/) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="cca01-129">Read hello [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for more information.</span></span>

## <a name="create-a-simple-web-application"></a><span data-ttu-id="cca01-130">Criar um aplicativo Web simples</span><span class="sxs-lookup"><span data-stu-id="cca01-130">Create a simple web application</span></span>
<span data-ttu-id="cca01-131">Crie um aplicativo Web Flask que escuta a porta 80 retornar "Olá, Mundo!".</span><span class="sxs-lookup"><span data-stu-id="cca01-131">Create a Flask web application listening on port 80 that returns "Hello World!".</span></span>  <span data-ttu-id="cca01-132">Em Olá mesmo diretório, crie o arquivo hello *requirements.txt*.</span><span class="sxs-lookup"><span data-stu-id="cca01-132">In hello same directory, create hello file *requirements.txt*.</span></span>  <span data-ttu-id="cca01-133">Adicione o seguinte de saudação e salve as alterações:</span><span class="sxs-lookup"><span data-stu-id="cca01-133">Add hello following and save your changes:</span></span>
```
Flask
```

<span data-ttu-id="cca01-134">Também criar hello *app.py* de arquivo e adicione Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="cca01-134">Also create hello *app.py* file and add hello following:</span></span>

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():

    return 'Hello World!'

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

<a id="Build-Containers"></a>
## <a name="build-hello-image"></a><span data-ttu-id="cca01-135">Criar imagem Olá</span><span class="sxs-lookup"><span data-stu-id="cca01-135">Build hello image</span></span>
<span data-ttu-id="cca01-136">Executar Olá `docker build` imagem de saudação do comando toocreate que executa o aplicativo da web.</span><span class="sxs-lookup"><span data-stu-id="cca01-136">Run hello `docker build` command toocreate hello image that runs your web application.</span></span> <span data-ttu-id="cca01-137">Abra uma janela do PowerShell e navegue toohello diretório contendo Olá Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="cca01-137">Open a PowerShell window and navigate toohello directory containing hello Dockerfile.</span></span> <span data-ttu-id="cca01-138">Execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="cca01-138">Run hello following command:</span></span>

```
docker build -t helloworldapp .
```

<span data-ttu-id="cca01-139">Este comando compilações Olá nova imagem usando as instruções de saudação em seu Dockerfile, nomear (-t marcação) imagem hello "helloworldapp".</span><span class="sxs-lookup"><span data-stu-id="cca01-139">This command builds hello new image using hello instructions in your Dockerfile, naming (-t tagging) hello image "helloworldapp".</span></span> <span data-ttu-id="cca01-140">Criando uma imagem extrai imagem base Olá para baixo do Hub do Docker e cria uma nova imagem que adiciona o seu aplicativo na parte superior da imagem base hello.</span><span class="sxs-lookup"><span data-stu-id="cca01-140">Building an image pulls hello base image down from Docker Hub and creates a new image that adds your application on top of hello base image.</span></span>  

<span data-ttu-id="cca01-141">Após a conclusão do comando de compilação hello, executar Olá `docker images` informações toosee na nova imagem de saudação do comando:</span><span class="sxs-lookup"><span data-stu-id="cca01-141">Once hello build command completes, run hello `docker images` command toosee information on hello new image:</span></span>

```
$ docker images

REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              8ce25f5d6a79        2 minutes ago       10.4 GB
```

## <a name="run-hello-application-locally"></a><span data-ttu-id="cca01-142">Executar o aplicativo hello localmente</span><span class="sxs-lookup"><span data-stu-id="cca01-142">Run hello application locally</span></span>
<span data-ttu-id="cca01-143">Verifique se sua imagem localmente antes de enviar por push-registro de contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="cca01-143">Verify your image locally before pushing it hello container registry.</span></span>  

<span data-ttu-id="cca01-144">Execute o aplicativo hello:</span><span class="sxs-lookup"><span data-stu-id="cca01-144">Run hello application:</span></span>

```
docker run -d --name my-web-site helloworldapp
```

<span data-ttu-id="cca01-145">*nome* oferece um toohello nome executando contêiner (em vez de ID de contêiner de saudação).</span><span class="sxs-lookup"><span data-stu-id="cca01-145">*name* gives a name toohello running container (instead of hello container ID).</span></span>

<span data-ttu-id="cca01-146">Depois de iniciada a contêiner hello, localize seu endereço IP para que você possa conectar tooyour executando o contêiner de um navegador:</span><span class="sxs-lookup"><span data-stu-id="cca01-146">Once hello container starts, find its IP address so that you can connect tooyour running container from a browser:</span></span>
```
docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" my-web-site
```

<span data-ttu-id="cca01-147">Conecte-se toohello executando o contêiner.</span><span class="sxs-lookup"><span data-stu-id="cca01-147">Connect toohello running container.</span></span>  <span data-ttu-id="cca01-148">Abra um navegador da web apontando o endereço IP de toohello retornado, por exemplo "http://172.31.194.61".</span><span class="sxs-lookup"><span data-stu-id="cca01-148">Open a web browser pointing toohello IP address returned, for example "http://172.31.194.61".</span></span> <span data-ttu-id="cca01-149">Você deve ver Olá título "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="cca01-149">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="cca01-150">Exibir no navegador de saudação.</span><span class="sxs-lookup"><span data-stu-id="cca01-150">display in hello browser.</span></span>

<span data-ttu-id="cca01-151">toostop seu contêiner, execute:</span><span class="sxs-lookup"><span data-stu-id="cca01-151">toostop your container, run:</span></span>

```
docker stop my-web-site
```

<span data-ttu-id="cca01-152">Exclua contêiner de saudação do seu computador de desenvolvimento:</span><span class="sxs-lookup"><span data-stu-id="cca01-152">Delete hello container from your development machine:</span></span>

```
docker rm my-web-site
```

<a id="Push-Containers"></a>
## <a name="push-hello-image-toohello-container-registry"></a><span data-ttu-id="cca01-153">Registro de contêiner do push Olá imagem toohello</span><span class="sxs-lookup"><span data-stu-id="cca01-153">Push hello image toohello container registry</span></span>
<span data-ttu-id="cca01-154">Depois de verificar o que contêiner Olá é executado no computador de desenvolvimento, enviar por push do registro do hello imagem tooyour no registro de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="cca01-154">After you verify that hello container runs on your development machine, push hello image tooyour registry in Azure Container Registry.</span></span>

<span data-ttu-id="cca01-155">Executar ``docker login`` toolog tooyour registro de contêiner com o [credenciais de registro](../container-registry/container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="cca01-155">Run ``docker login`` toolog in tooyour container registry with your [registry credentials](../container-registry/container-registry-authentication.md).</span></span>

<span data-ttu-id="cca01-156">Olá exemplo a seguir passa Olá ID e a senha de um Active Directory do Azure [entidade de serviço](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="cca01-156">hello following example passes hello ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="cca01-157">Por exemplo, você pode ter atribuído um registro de tooyour principal do serviço para um cenário de automação.</span><span class="sxs-lookup"><span data-stu-id="cca01-157">For example, you might have assigned a service principal tooyour registry for an automation scenario.</span></span> <span data-ttu-id="cca01-158">Ou pode fazer logon usando o nome de usuário e a senha do registro.</span><span class="sxs-lookup"><span data-stu-id="cca01-158">Or, you could login using your registry username and password.</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="cca01-159">Olá comando a seguir cria uma marca, ou alias, da imagem hello, com um registro de tooyour caminho totalmente qualificado.</span><span class="sxs-lookup"><span data-stu-id="cca01-159">hello following command creates a tag, or alias, of hello image, with a fully qualified path tooyour registry.</span></span> <span data-ttu-id="cca01-160">Este exemplo casas Olá imagem no hello ```samples``` namespace tooavoid desordem na raiz de saudação do registro hello.</span><span class="sxs-lookup"><span data-stu-id="cca01-160">This example places hello image in hello ```samples``` namespace tooavoid clutter in hello root of hello registry.</span></span>

```
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

<span data-ttu-id="cca01-161">Registro de push Olá imagem tooyour contêiner:</span><span class="sxs-lookup"><span data-stu-id="cca01-161">Push hello image tooyour container registry:</span></span>

```
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="create-hello-containerized-service-in-visual-studio"></a><span data-ttu-id="cca01-162">Criar serviço Olá em contêineres no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cca01-162">Create hello containerized service in Visual Studio</span></span>
<span data-ttu-id="cca01-163">Olá SDK do Service Fabric e ferramentas fornecem um toohelp de modelo de serviço é criar um aplicativo em contêineres.</span><span class="sxs-lookup"><span data-stu-id="cca01-163">hello Service Fabric SDK and tools provide a service template toohelp you create a containerized application.</span></span>

1. <span data-ttu-id="cca01-164">Inicie o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cca01-164">Start Visual Studio.</span></span>  <span data-ttu-id="cca01-165">Selecione **Arquivo** > **Novo** > **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="cca01-165">Select **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="cca01-166">Selecione **Aplicativo do Service Fabric**, nomeie-o como "MyFirstContainer" e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="cca01-166">Select **Service Fabric application**, name it "MyFirstContainer", and click **OK**.</span></span>
3. <span data-ttu-id="cca01-167">Selecione **convidado contêiner** na lista de saudação do **modelos de serviço**.</span><span class="sxs-lookup"><span data-stu-id="cca01-167">Select **Guest Container** from hello list of **service templates**.</span></span>
4. <span data-ttu-id="cca01-168">Em **nome da imagem** insira "myregistry.azurecr.io/samples/helloworldapp," imagem Olá enviada por push tooyour repositório de contêiner.</span><span class="sxs-lookup"><span data-stu-id="cca01-168">In **Image Name** enter "myregistry.azurecr.io/samples/helloworldapp", hello image you pushed tooyour container repository.</span></span>
5. <span data-ttu-id="cca01-169">Dê um nome ao seu serviço e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="cca01-169">Give your service a name, and click **OK**.</span></span>

## <a name="configure-communication"></a><span data-ttu-id="cca01-170">Configurar a comunicação</span><span class="sxs-lookup"><span data-stu-id="cca01-170">Configure communication</span></span>
<span data-ttu-id="cca01-171">serviço de saudação em contêineres precisa de um ponto de extremidade de comunicação.</span><span class="sxs-lookup"><span data-stu-id="cca01-171">hello containerized service needs an endpoint for communication.</span></span> <span data-ttu-id="cca01-172">Adicionar um `Endpoint` elemento com o arquivo do tipo toohello ServiceManifest.xml, porta e protocolo de saudação.</span><span class="sxs-lookup"><span data-stu-id="cca01-172">Add an `Endpoint` element with hello protocol, port, and type toohello ServiceManifest.xml file.</span></span> <span data-ttu-id="cca01-173">Neste artigo, o serviço de saudação em contêineres escuta na porta 8081.</span><span class="sxs-lookup"><span data-stu-id="cca01-173">For this article, hello containerized service listens on port 8081.</span></span>  <span data-ttu-id="cca01-174">Neste exemplo, uma porta fixa 8081 é usada.</span><span class="sxs-lookup"><span data-stu-id="cca01-174">In this example, a fixed port 8081 is used.</span></span>  <span data-ttu-id="cca01-175">Se nenhuma porta for especificada, uma porta aleatória do intervalo de portas de aplicativo hello é escolhida.</span><span class="sxs-lookup"><span data-stu-id="cca01-175">If no port is specified, a random port from hello application port range is chosen.</span></span>  

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
  </Endpoints>
</Resources>
```

<span data-ttu-id="cca01-176">Definindo um ponto de extremidade, o Service Fabric publica toohello de ponto de extremidade Olá Naming service.</span><span class="sxs-lookup"><span data-stu-id="cca01-176">By defining an endpoint, Service Fabric publishes hello endpoint toohello Naming service.</span></span>  <span data-ttu-id="cca01-177">Outros serviços em execução no cluster Olá podem resolver este contêiner.</span><span class="sxs-lookup"><span data-stu-id="cca01-177">Other services running in hello cluster can resolve this container.</span></span>  <span data-ttu-id="cca01-178">Você também pode executar a comunicação de contêiner para contêiner usando Olá [proxy reverso](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="cca01-178">You can also perform container-to-container communication using hello [reverse proxy](service-fabric-reverseproxy.md).</span></span>  <span data-ttu-id="cca01-179">A comunicação é executada, fornecendo a porta de escuta de proxy reverso HTTP de saudação e o nome de saudação do serviços de saudação que você deseja toocommunicate com como variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="cca01-179">Communication is performed by providing hello reverse proxy HTTP listening port and hello name of hello services that you want toocommunicate with as environment variables.</span></span>

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="cca01-180">Configurar e definir as variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="cca01-180">Configure and set environment variables</span></span>
<span data-ttu-id="cca01-181">Variáveis de ambiente podem ser especificadas para cada pacote de código no manifesto do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="cca01-181">Environment variables can be specified for each code package in hello service manifest.</span></span> <span data-ttu-id="cca01-182">Esse recurso está disponível para todos os serviços, independentemente de eles serem implantados como contêineres ou processos ou executáveis convidados.</span><span class="sxs-lookup"><span data-stu-id="cca01-182">This feature is available for all services irrespective of whether they are deployed as containers or processes or guest executables.</span></span> <span data-ttu-id="cca01-183">Você pode substituir a variável de ambiente valores no aplicativo hello manifesto ou especificá-las durante a implantação como parâmetros de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cca01-183">You can override environment variable values in hello application manifest or specify them during deployment as application parameters.</span></span>

<span data-ttu-id="cca01-184">Olá, serviço manifesto trecho XML a seguir mostra um exemplo de como toospecify variáveis de ambiente para um pacote de código:</span><span class="sxs-lookup"><span data-stu-id="cca01-184">hello following service manifest XML snippet shows an example of how toospecify environment variables for a code package:</span></span>
```xml
<CodePackage Name="Code" Version="1.0.0">
  ...
  <EnvironmentVariables>
    <EnvironmentVariable Name="HttpGatewayPort" Value=""/>    
  </EnvironmentVariables>
</CodePackage>
```

<span data-ttu-id="cca01-185">Essas variáveis de ambiente podem ser substituídos no manifesto de aplicativo hello:</span><span class="sxs-lookup"><span data-stu-id="cca01-185">These environment variables can be overridden in hello application manifest:</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
  </EnvironmentOverrides>
  ...
</ServiceManifestImport>
```

## <a name="configure-container-port-to-host-port-mapping-and-container-to-container-discovery"></a><span data-ttu-id="cca01-186">Configurar mapeamento de porta para host e descoberta de contêiner para contêiner</span><span class="sxs-lookup"><span data-stu-id="cca01-186">Configure container port-to-host port mapping and container-to-container discovery</span></span>
<span data-ttu-id="cca01-187">Configure toocommunicate de porta usada um host com o contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="cca01-187">Configure a host port used toocommunicate  with hello container.</span></span> <span data-ttu-id="cca01-188">associação de porta Olá mapeia a porta de saudação em qual Olá serviço está escutando em Olá contêiner tooa porta no host de saudação.</span><span class="sxs-lookup"><span data-stu-id="cca01-188">hello port binding maps hello port on which hello service is listening inside hello container tooa port on hello host.</span></span> <span data-ttu-id="cca01-189">Adicionar um `PortBinding` elemento `ContainerHostPolicies` elemento do arquivo de ApplicationManifest.xml hello.</span><span class="sxs-lookup"><span data-stu-id="cca01-189">Add a `PortBinding` element in `ContainerHostPolicies` element of hello ApplicationManifest.xml file.</span></span>  <span data-ttu-id="cca01-190">Neste artigo, `ContainerPort` é 80 (contêiner Olá expõe a porta 80, Olá especificado no Dockerfile) e `EndpointRef` é "Guest1TypeEndpoint" (Olá definido anteriormente no manifesto do serviço de saudação do ponto de extremidade).</span><span class="sxs-lookup"><span data-stu-id="cca01-190">For this article, `ContainerPort` is 80 (hello container exposes port 80, as specified in hello Dockerfile) and `EndpointRef` is "Guest1TypeEndpoint" (hello endpoint previously defined in hello service manifest).</span></span>  <span data-ttu-id="cca01-191">Solicitações de entrada toohello na porta 8081 são mapeados tooport 80 no contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="cca01-191">Incoming requests toohello service on port 8081 are mapped tooport 80 on hello container.</span></span>

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-container-registry-authentication"></a><span data-ttu-id="cca01-192">Definir autenticação do registro de contêiner</span><span class="sxs-lookup"><span data-stu-id="cca01-192">Configure container registry authentication</span></span>
<span data-ttu-id="cca01-193">Configurar a autenticação de registro de contêiner adicionando `RepositoryCredentials` muito`ContainerHostPolicies` do arquivo applicationmanifest. XML de saudação.</span><span class="sxs-lookup"><span data-stu-id="cca01-193">Configure container registry authentication by adding `RepositoryCredentials` too`ContainerHostPolicies` of hello ApplicationManifest.xml file.</span></span> <span data-ttu-id="cca01-194">Adicione Olá conta e senha Olá myregistry.azurecr.io contêiner do registro, que permite que a imagem de contêiner de Olá Olá serviço toodownload do repositório de saudação.</span><span class="sxs-lookup"><span data-stu-id="cca01-194">Add hello account and password for hello myregistry.azurecr.io container registry, which allows hello service toodownload hello container image from hello repository.</span></span>

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

<span data-ttu-id="cca01-195">É recomendável que você criptografe a senha do repositório hello usando um certificado de codificação que implantou tooall nós de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="cca01-195">We recommend that you encrypt hello repository password by using an encipherment certificate that's deployed tooall nodes of hello cluster.</span></span> <span data-ttu-id="cca01-196">Quando o Service Fabric implanta Olá serviço pacote toohello, certificado de codificação de saudação é toodecrypt usado Olá codificação texto.</span><span class="sxs-lookup"><span data-stu-id="cca01-196">When Service Fabric deploys hello service package toohello cluster, hello encipherment certificate is used toodecrypt hello cipher text.</span></span>  <span data-ttu-id="cca01-197">Olá Invoke-ServiceFabricEncryptText cmdlet é usado toocreate Olá codificação texto senha hello, que é adicionado toohello ApplicationManifest.xml arquivo.</span><span class="sxs-lookup"><span data-stu-id="cca01-197">hello Invoke-ServiceFabricEncryptText cmdlet is used toocreate hello cipher text for hello password, which is added toohello ApplicationManifest.xml file.</span></span>

<span data-ttu-id="cca01-198">Olá script a seguir cria um novo certificado autoassinado e exporta-o arquivo PFX de tooa.</span><span class="sxs-lookup"><span data-stu-id="cca01-198">hello following script creates a new self-signed certificate and exports it tooa PFX file.</span></span>  <span data-ttu-id="cca01-199">certificado de saudação é importado para um cofre de chave existente e, em seguida, implantados cluster do Service Fabric toohello.</span><span class="sxs-lookup"><span data-stu-id="cca01-199">hello certificate is imported into an existing key vault and then deployed toohello Service Fabric cluster.</span></span>

```powershell
# Variables.
$certpwd = ConvertTo-SecureString -String "Pa$$word321!" -Force -AsPlainText
$filepath = "C:\MyCertificates\dataenciphermentcert.pfx"
$subjectname = "dataencipherment"
$vaultname = "mykeyvault"
$certificateName = "dataenciphermentcert"
$groupname="myclustergroup"
$clustername = "mycluster"

$subscriptionId = "subscription ID"

Login-AzureRmAccount

Select-AzureRmSubscription -SubscriptionId $subscriptionId

# Create a self signed cert, export tooPFX file.
New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject $subjectname -Provider 'Microsoft Enhanced Cryptographic Provider v1.0' `
| Export-PfxCertificate -FilePath $filepath -Password $certpwd

# Import hello certificate tooan existing key vault.  hello key vault must be enabled for deployment.
$cer = Import-AzureKeyVaultCertificate -VaultName $vaultName -Name $certificateName -FilePath $filepath -Password $certpwd

Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $groupname -EnabledForDeployment

# Add hello certificate tooall hello VMs in hello cluster.
Add-AzureRmServiceFabricApplicationCertificate -ResourceGroupName $groupname -Name $clustername -SecretIdentifier $cer.SecretId
```
<span data-ttu-id="cca01-200">Criptografar a senha hello usando Olá [ServiceFabricEncryptText Invoke](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="cca01-200">Encrypt hello password using hello [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet.</span></span>

```powershell
$text = "=P==/==/=8=/=+u4lyOB=+=nWzEeRfF="
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint $cer.Thumbprint -Text $text -StoreLocation Local -StoreName My
```

<span data-ttu-id="cca01-201">Substitua a senha de saudação com texto cifrado de saudação retornado por Olá [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet e defina `PasswordEncrypted` muito "true".</span><span class="sxs-lookup"><span data-stu-id="cca01-201">Replace hello password with hello cipher text returned by hello [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet and set `PasswordEncrypted` too"true".</span></span>

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <RepositoryCredentials AccountName="myregistry" Password="MIIB6QYJKoZIhvcNAQcDoIIB2jCCAdYCAQAxggFRMIIBTQIBADA1MCExHzAdBgNVBAMMFnJ5YW53aWRhdGFlbmNpcGhlcm1lbnQCEFfyjOX/17S6RIoSjA6UZ1QwDQYJKoZIhvcNAQEHMAAEg
gEAS7oqxvoz8i6+8zULhDzFpBpOTLU+c2mhBdqXpkLwVfcmWUNA82rEWG57Vl1jZXe7J9BkW9ly4xhU8BbARkZHLEuKqg0saTrTHsMBQ6KMQDotSdU8m8Y2BR5Y100wRjvVx3y5+iNYuy/JmM
gSrNyyMQ/45HfMuVb5B4rwnuP8PAkXNT9VLbPeqAfxsMkYg+vGCDEtd8m+bX/7Xgp/kfwxymOuUCrq/YmSwe9QTG3pBri7Hq1K3zEpX4FH/7W2Zb4o3fBAQ+FuxH4nFjFNoYG29inL0bKEcTX
yNZNKrvhdM3n1Uk/8W2Hr62FQ33HgeFR1yxQjLsUu800PrYcR5tLfyTB8BgkqhkiG9w0BBwEwHQYJYIZIAWUDBAEqBBBybgM5NUV8BeetUbMR8mJhgFBrVSUsnp9B8RyebmtgU36dZiSObDsI
NtTvlzhk11LIlae/5kjPv95r3lw6DHmV4kXLwiCNlcWPYIWBGIuspwyG+28EWSrHmN7Dt2WqEWqeNQ==" PasswordEncrypted="true"/>
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-isolation-mode"></a><span data-ttu-id="cca01-202">Configurar o modo de isolamento</span><span class="sxs-lookup"><span data-stu-id="cca01-202">Configure isolation mode</span></span>
<span data-ttu-id="cca01-203">O Windows dá suporte a dois modos de isolamento para contêineres: processo e Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="cca01-203">Windows supports two isolation modes for containers: process and Hyper-V.</span></span> <span data-ttu-id="cca01-204">Com o modo de isolamento do processo de hello, todos os contêineres de saudação em execução no hello mesmo host máquina compartilhamento saudação do kernel com o host de saudação.</span><span class="sxs-lookup"><span data-stu-id="cca01-204">With hello process isolation mode, all hello containers running on hello same host machine share hello kernel with hello host.</span></span> <span data-ttu-id="cca01-205">Com o modo de isolamento Olá Hyper-V, kernels Olá são isolados entre cada contêiner do Hyper-V e o host do contêiner hello.</span><span class="sxs-lookup"><span data-stu-id="cca01-205">With hello Hyper-V isolation mode, hello kernels are isolated between each Hyper-V container and hello container host.</span></span> <span data-ttu-id="cca01-206">modo de isolamento de saudação é especificado em Olá `ContainerHostPolicies` elemento no arquivo de manifesto de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="cca01-206">hello isolation mode is specified in hello `ContainerHostPolicies` element in hello application manifest file.</span></span> <span data-ttu-id="cca01-207">modos de isolamento de saudação que podem ser especificados são `process`, `hyperv`, e `default`.</span><span class="sxs-lookup"><span data-stu-id="cca01-207">hello isolation modes that can be specified are `process`, `hyperv`, and `default`.</span></span> <span data-ttu-id="cca01-208">modo de isolamento padrão Olá padrões muito`process` no Windows Server hospeda e os padrões muito`hyperv` em hosts do Windows 10.</span><span class="sxs-lookup"><span data-stu-id="cca01-208">hello default isolation mode defaults too`process` on Windows Server hosts, and defaults too`hyperv` on Windows 10 hosts.</span></span> <span data-ttu-id="cca01-209">Olá trecho a seguir mostra como o modo de isolamento de saudação é especificado no arquivo de manifesto de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="cca01-209">hello following snippet shows how hello isolation mode is specified in hello application manifest file.</span></span>

```xml
<ContainerHostPolicies CodePackageRef="Code" Isolation="hyperv">
```

## <a name="configure-resource-governance"></a><span data-ttu-id="cca01-210">Configurar governança de recursos</span><span class="sxs-lookup"><span data-stu-id="cca01-210">Configure resource governance</span></span>
<span data-ttu-id="cca01-211">[Governança de recursos](service-fabric-resource-governance.md) restringe Olá podem usar recursos que Olá contêiner no host de saudação.</span><span class="sxs-lookup"><span data-stu-id="cca01-211">[Resource governance](service-fabric-resource-governance.md) restricts hello resources that hello container can use on hello host.</span></span> <span data-ttu-id="cca01-212">Olá `ResourceGovernancePolicy` elemento, que é especificado no manifesto de aplicativo hello, é usado toodeclare limites de recurso para um pacote de código de serviço.</span><span class="sxs-lookup"><span data-stu-id="cca01-212">hello `ResourceGovernancePolicy` element, which is specified in hello application manifest, is used toodeclare resource limits for a service code package.</span></span> <span data-ttu-id="cca01-213">Limites de recurso podem ser definidos para Olá recursos a seguir: memória, MemorySwap, CpuShares (peso relativo da CPU), MemoryReservationInMB, BlkioWeight (BlockIO peso relativo).</span><span class="sxs-lookup"><span data-stu-id="cca01-213">Resource limits can be set for hello following resources: Memory, MemorySwap, CpuShares (CPU relative weight), MemoryReservationInMB, BlkioWeight (BlockIO relative weight).</span></span>  <span data-ttu-id="cca01-214">Neste exemplo, o pacote de serviço Guest1Pkg obtém um núcleo em nós de cluster Olá onde ele é colocado.</span><span class="sxs-lookup"><span data-stu-id="cca01-214">In this example, service package Guest1Pkg gets one core on hello cluster nodes where it is placed.</span></span>  <span data-ttu-id="cca01-215">Limites de memória são absolutos, para o pacote de códigos Olá seja limitado too1024 MB de memória (e uma reserva de garantia de software de Olá mesmo).</span><span class="sxs-lookup"><span data-stu-id="cca01-215">Memory limits are absolute, so hello code package is limited too1024 MB of memory (and a soft-guarantee reservation of hello same).</span></span> <span data-ttu-id="cca01-216">Pacotes de código (contêineres ou processos) não são tooallocate capaz de mais memória do que esse limite e tentar toodo pode resultar em uma exceção de falta de memória.</span><span class="sxs-lookup"><span data-stu-id="cca01-216">Code packages (containers or processes) are not able tooallocate more memory than this limit, and attempting toodo so results in an out-of-memory exception.</span></span> <span data-ttu-id="cca01-217">Para toowork de imposição de limite de recursos, todos os pacotes de código dentro de um pacote de serviço devem ter limites de memória especificados.</span><span class="sxs-lookup"><span data-stu-id="cca01-217">For resource limit enforcement toowork, all code packages within a service package should have memory limits specified.</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
  <Policies>
    <ServicePackageResourceGovernancePolicy CpuCores="1"/>
    <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
  </Policies>
</ServiceManifestImport>
```

## <a name="deploy-hello-container-application"></a><span data-ttu-id="cca01-218">Implantar o aplicativo de contêiner hello</span><span class="sxs-lookup"><span data-stu-id="cca01-218">Deploy hello container application</span></span>
<span data-ttu-id="cca01-219">Salvar todas as suas alterações e compile o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="cca01-219">Save all your changes and build hello application.</span></span> <span data-ttu-id="cca01-220">toopublish seu aplicativo, o botão direito do mouse em **MyFirstContainer** no Gerenciador de soluções e selecione **publicar**.</span><span class="sxs-lookup"><span data-stu-id="cca01-220">toopublish your application, right-click on **MyFirstContainer** in Solution Explorer and select **Publish**.</span></span>

<span data-ttu-id="cca01-221">Em **ponto de extremidade de Conexão**, insira o ponto de extremidade de gerenciamento Olá para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="cca01-221">In **Connection Endpoint**, enter hello management endpoint for hello cluster.</span></span>  <span data-ttu-id="cca01-222">Por exemplo, "containercluster.westus2.cloudapp.azure.com:19000".</span><span class="sxs-lookup"><span data-stu-id="cca01-222">For example, "containercluster.westus2.cloudapp.azure.com:19000".</span></span> <span data-ttu-id="cca01-223">Você pode encontrar a conexão de cliente Olá ponto de extremidade na folha de visão geral de saudação para seu cluster em Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cca01-223">You can find hello client connection endpoint in hello Overview blade for your cluster in hello [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="cca01-224">Clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="cca01-224">Click **Publish**.</span></span>

<span data-ttu-id="cca01-225">O [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) é uma ferramenta baseada na Web para inspecionar e gerenciar aplicativos e nós em um cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="cca01-225">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a web-based tool for inspecting and managing applications and nodes in a Service Fabric cluster.</span></span> <span data-ttu-id="cca01-226">Abra um navegador e navegue toohttp://containercluster.westus2.cloudapp.azure.com:19080 Explorer/e siga a implantação do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="cca01-226">Open a browser and navigate toohttp://containercluster.westus2.cloudapp.azure.com:19080/Explorer/ and follow hello application deployment.</span></span>  <span data-ttu-id="cca01-227">aplicativo Hello implanta, mas está em estado de erro até Olá imagem é baixada em nós de cluster de saudação (que podem levar algum tempo, dependendo do tamanho da imagem Olá): ![erro][1]</span><span class="sxs-lookup"><span data-stu-id="cca01-227">hello application deploys but is in an error state until hello image is downloaded on hello cluster nodes (which can take some time, depending on hello image size): ![Error][1]</span></span>

<span data-ttu-id="cca01-228">aplicativo Hello está pronto quando ele está em ```Ready``` estado: ![pronto][2]</span><span class="sxs-lookup"><span data-stu-id="cca01-228">hello application is ready when it's in ```Ready``` state: ![Ready][2]</span></span>

<span data-ttu-id="cca01-229">Abra um navegador e navegue toohttp://containercluster.westus2.cloudapp.azure.com:8081.</span><span class="sxs-lookup"><span data-stu-id="cca01-229">Open a browser and navigate toohttp://containercluster.westus2.cloudapp.azure.com:8081.</span></span> <span data-ttu-id="cca01-230">Você deve ver Olá título "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="cca01-230">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="cca01-231">Exibir no navegador de saudação.</span><span class="sxs-lookup"><span data-stu-id="cca01-231">display in hello browser.</span></span>

## <a name="clean-up"></a><span data-ttu-id="cca01-232">Limpar</span><span class="sxs-lookup"><span data-stu-id="cca01-232">Clean up</span></span>
<span data-ttu-id="cca01-233">Continue tooincur encargos enquanto Olá cluster está em execução, considere [excluindo o cluster](service-fabric-get-started-azure-cluster.md#remove-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="cca01-233">You continue tooincur charges while hello cluster is running, consider [deleting your cluster](service-fabric-get-started-azure-cluster.md#remove-the-cluster).</span></span>  <span data-ttu-id="cca01-234">[Clusters de terceiros](http://tryazureservicefabric.westus.cloudapp.azure.com/) são excluídos automaticamente após algumas horas.</span><span class="sxs-lookup"><span data-stu-id="cca01-234">[Party clusters](http://tryazureservicefabric.westus.cloudapp.azure.com/) are automatically deleted after a few hours.</span></span>

<span data-ttu-id="cca01-235">Depois que você enviar por push o registro de contêiner de toohello Olá imagem, você pode excluir imagem local saudação do seu computador de desenvolvimento:</span><span class="sxs-lookup"><span data-stu-id="cca01-235">After you push hello image toohello container registry you can delete hello local image from your development computer:</span></span>

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a><span data-ttu-id="cca01-236">Exemplo completo de manifestos de serviço e aplicativo do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="cca01-236">Complete example Service Fabric application and service manifests</span></span>
<span data-ttu-id="cca01-237">Aqui estão os manifestos de aplicativo usados neste artigo e serviço completo hello.</span><span class="sxs-lookup"><span data-stu-id="cca01-237">Here are hello complete service and application manifests used in this article.</span></span>

### <a name="servicemanifestxml"></a><span data-ttu-id="cca01-238">ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="cca01-238">ServiceManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="Guest1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         hello UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="Guest1Type" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers tooService Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables tooyour container: -->    
    <EnvironmentVariables>
      <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
      <EnvironmentVariable Name="BackendServiceName" Value=""/>
    </EnvironmentVariables>

  </CodePackage>

  <!-- Config package is hello contents of hello Config directoy under PackageRoot that contains an
       independently-updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which to
           listen. Please note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a><span data-ttu-id="cca01-239">ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="cca01-239">ApplicationManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="MyFirstContainerType"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Parameters>
    <Parameter Name="Guest1_InstanceCount" DefaultValue="-1" />
  </Parameters>
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion
       should match hello Name and Version attributes of hello ServiceManifest element defined in the
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="FrontendService.Code">
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentOverrides>
    <ConfigOverrides />
    <Policies>
      <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="MIIB6QYJKoZIhvcNAQcDoIIB2jCCAdYCAQAxggFRMIIBTQIBADA1MCExHzAdBgNVBAMMFnJ5YW53aWRhdGFlbmNpcGhlcm1lbnQCEFfyjOX/17S6RIoSjA6UZ1QwDQYJKoZIhvcNAQEHMAAEg
gEAS7oqxvoz8i6+8zULhDzFpBpOTLU+c2mhBdqXpkLwVfcmWUNA82rEWG57Vl1jZXe7J9BkW9ly4xhU8BbARkZHLEuKqg0saTrTHsMBQ6KMQDotSdU8m8Y2BR5Y100wRjvVx3y5+iNYuy/JmM
gSrNyyMQ/45HfMuVb5B4rwnuP8PAkXNT9VLbPeqAfxsMkYg+vGCDEtd8m+bX/7Xgp/kfwxymOuUCrq/YmSwe9QTG3pBri7Hq1K3zEpX4FH/7W2Zb4o3fBAQ+FuxH4nFjFNoYG29inL0bKEcTX
yNZNKrvhdM3n1Uk/8W2Hr62FQ33HgeFR1yxQjLsUu800PrYcR5tLfyTB8BgkqhkiG9w0BBwEwHQYJYIZIAWUDBAEqBBBybgM5NUV8BeetUbMR8mJhgFBrVSUsnp9B8RyebmtgU36dZiSObDsI
NtTvlzhk11LIlae/5kjPv95r3lw6DHmV4kXLwiCNlcWPYIWBGIuspwyG+28EWSrHmN7Dt2WqEWqeNQ==" PasswordEncrypted="true"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
      </ContainerHostPolicies>
      <ServicePackageResourceGovernancePolicy CpuCores="1"/>
      <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types, when an instance of this
         application type is created. You can also create one or more instances of service type using the
         ServiceFabric PowerShell module.

         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="Guest1">
      <StatelessService ServiceTypeName="Guest1Type" InstanceCount="[Guest1_InstanceCount]">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```

## <a name="configure-time-interval-before-container-is-force-terminated"></a><span data-ttu-id="cca01-240">Configurar o intervalo de tempo antes do contêiner ser forçado a terminar</span><span class="sxs-lookup"><span data-stu-id="cca01-240">Configure time interval before container is force terminated</span></span>

<span data-ttu-id="cca01-241">Você pode configurar um intervalo de tempo para Olá toowait de tempo de execução antes de contêiner de saudação é removida depois hello exclusão de serviço (ou um nó de tooanother mover) foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="cca01-241">You can configure a time interval for hello runtime toowait before hello container is removed after hello service deletion (or a move tooanother node) has started.</span></span> <span data-ttu-id="cca01-242">Configurando intervalo de tempo de saudação envia Olá `docker stop <time in seconds>` contêiner de toohello de comando.</span><span class="sxs-lookup"><span data-stu-id="cca01-242">Configuring hello time interval sends hello `docker stop <time in seconds>` command toohello container.</span></span>   <span data-ttu-id="cca01-243">Para obter mais detalhes, consulte [parar docker](https://docs.docker.com/engine/reference/commandline/stop/).</span><span class="sxs-lookup"><span data-stu-id="cca01-243">For more detail, see [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span></span> <span data-ttu-id="cca01-244">Olá toowait de intervalo de tempo especificado em Olá `Hosting` seção.</span><span class="sxs-lookup"><span data-stu-id="cca01-244">hello time interval toowait is specified under hello `Hosting` section.</span></span> <span data-ttu-id="cca01-245">Olá trecho do manifesto de cluster a seguir mostra como o intervalo de espera tooset hello:</span><span class="sxs-lookup"><span data-stu-id="cca01-245">hello following cluster manifest snippet shows how tooset hello wait interval:</span></span>

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
<span data-ttu-id="cca01-246">Olá intervalo de tempo padrão é definido too10 segundos.</span><span class="sxs-lookup"><span data-stu-id="cca01-246">hello default time interval is set too10 seconds.</span></span> <span data-ttu-id="cca01-247">Como essa configuração é dinâmica, uma configuração só atualizar no tempo limite de saudação de atualizações de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="cca01-247">Since this configuration is dynamic, a config only upgrade on hello cluster updates hello timeout.</span></span> 


## <a name="configure-hello-runtime-tooremove-unused-container-images"></a><span data-ttu-id="cca01-248">Configurar Olá runtime tooremove imagens de contêiner não utilizado</span><span class="sxs-lookup"><span data-stu-id="cca01-248">Configure hello runtime tooremove unused container images</span></span>

<span data-ttu-id="cca01-249">Você pode configurar Olá Service Fabric cluster tooremove imagens de contêiner não utilizados do nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="cca01-249">You can configure hello Service Fabric cluster tooremove unused container images from hello node.</span></span> <span data-ttu-id="cca01-250">Essa configuração permite toobe de espaço em disco retomou se houver muitas imagens de contêiner no nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="cca01-250">This configuration allows disk space toobe recaptured if too many container images are present on hello node.</span></span>  <span data-ttu-id="cca01-251">tooenable deste recurso, a atualização Olá `Hosting` seção no manifesto do cluster hello, conforme mostrado no hello trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="cca01-251">tooenable this feature, update hello `Hosting` section in hello cluster manifest as shown in hello following snippet:</span></span> 


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

<span data-ttu-id="cca01-252">Para as imagens que não devem ser excluídas, você poderá especificá-los em Olá `ContainerImagesToSkip` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="cca01-252">For images that should not be deleted, you can specify them under hello `ContainerImagesToSkip` parameter.</span></span> 



## <a name="next-steps"></a><span data-ttu-id="cca01-253">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cca01-253">Next steps</span></span>
* <span data-ttu-id="cca01-254">Saiba mais sobre como executar [contêineres no Service Fabric](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cca01-254">Learn more about running [containers on Service Fabric](service-fabric-containers-overview.md).</span></span>
* <span data-ttu-id="cca01-255">Saudação de leitura [implantar um aplicativo .NET em um contêiner](service-fabric-host-app-in-a-container.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="cca01-255">Read hello [Deploy a .NET application in a container](service-fabric-host-app-in-a-container.md) tutorial.</span></span>
* <span data-ttu-id="cca01-256">Saiba mais sobre Olá Service Fabric [ciclo de vida do aplicativo](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="cca01-256">Learn about hello Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
* <span data-ttu-id="cca01-257">Saudação de check-out [exemplos de código do contêiner do Service Fabric](https://github.com/Azure-Samples/service-fabric-dotnet-containers) no GitHub.</span><span class="sxs-lookup"><span data-stu-id="cca01-257">Checkout hello [Service Fabric container code samples](https://github.com/Azure-Samples/service-fabric-dotnet-containers) on GitHub.</span></span>

[1]: ./media/service-fabric-get-started-containers/MyFirstContainerError.png
[2]: ./media/service-fabric-get-started-containers/MyFirstContainerReady.png
