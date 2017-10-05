---
title: "Criar um aplicativo de contêiner do Azure Service Fabric no Linux | Microsoft Docs"
description: "Crie seu primeiro aplicativo de contêiner do Linux no Azure Service Fabric.  Crie uma imagem do Docker com o seu aplicativo, envie a imagem para um registro de contêiner por push, crie e implante um aplicativo de contêiner do Service Fabric."
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
ms.openlocfilehash: 8355478cb2fff3a63bc4a9b359ec8e2b132c80f6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-service-fabric-container-application-on-linux"></a><span data-ttu-id="8ca14-104">Criar seu primeiro aplicativo de contêiner do Service Fabric no Linux</span><span class="sxs-lookup"><span data-stu-id="8ca14-104">Create your first Service Fabric container application on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8ca14-105">Windows</span><span class="sxs-lookup"><span data-stu-id="8ca14-105">Windows</span></span>](service-fabric-get-started-containers.md)
> * [<span data-ttu-id="8ca14-106">Linux</span><span class="sxs-lookup"><span data-stu-id="8ca14-106">Linux</span></span>](service-fabric-get-started-containers-linux.md)

<span data-ttu-id="8ca14-107">A execução de um aplicativo existente em um contêiner do Linux em um cluster do Service Fabric não requer alterações no seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8ca14-107">Running an existing application in a Linux container on a Service Fabric cluster doesn't require any changes to your application.</span></span> <span data-ttu-id="8ca14-108">Este artigo mostra como criar uma imagem do Docker que contém um aplicativo de web Python [Flask](http://flask.pocoo.org/) e a implantá-lo em um cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8ca14-108">This article walks you through creating a Docker image containing a Python [Flask](http://flask.pocoo.org/) web application and deploying it to a Service Fabric cluster.</span></span>  <span data-ttu-id="8ca14-109">Você também compartilhará seu aplicativo em contêineres pelo [Registro de Contêiner do Azure](/azure/container-registry/).</span><span class="sxs-lookup"><span data-stu-id="8ca14-109">You will also share your containerized application through [Azure Container Registry](/azure/container-registry/).</span></span>  <span data-ttu-id="8ca14-110">Este artigo pressupõe uma compreensão básica sobre o Docker.</span><span class="sxs-lookup"><span data-stu-id="8ca14-110">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="8ca14-111">Saiba mais sobre o Docker lendo a [Visão geral de Docker](https://docs.docker.com/engine/understanding-docker/).</span><span class="sxs-lookup"><span data-stu-id="8ca14-111">You can learn about Docker by reading the [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ca14-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8ca14-112">Prerequisites</span></span>
* <span data-ttu-id="8ca14-113">Um computador de desenvolvimento executando:</span><span class="sxs-lookup"><span data-stu-id="8ca14-113">A development computer running:</span></span>
  * <span data-ttu-id="8ca14-114">[Ferramentas e SDK do Service Fabric](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="8ca14-114">[Service Fabric SDK and tools](service-fabric-get-started-linux.md).</span></span>
  * <span data-ttu-id="8ca14-115">[Docker CE para Linux](https://docs.docker.com/engine/installation/#prior-releases).</span><span class="sxs-lookup"><span data-stu-id="8ca14-115">[Docker CE for Linux](https://docs.docker.com/engine/installation/#prior-releases).</span></span> 
  * [<span data-ttu-id="8ca14-116">CLI do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8ca14-116">Service Fabric CLI</span></span>](service-fabric-cli.md)

* <span data-ttu-id="8ca14-117">Um registro no Registro de Contêiner do Azure - [Crie um registro de contêiner](../container-registry/container-registry-get-started-portal.md) em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ca14-117">A registry in Azure Container Registry - [Create a container registry](../container-registry/container-registry-get-started-portal.md) in your Azure subscription.</span></span> 

## <a name="define-the-docker-container"></a><span data-ttu-id="8ca14-118">Defina o contêiner Docker</span><span class="sxs-lookup"><span data-stu-id="8ca14-118">Define the Docker container</span></span>
<span data-ttu-id="8ca14-119">Crie uma imagem com base na [imagem do Python](https://hub.docker.com/_/python/) localizada no Hub do Docker.</span><span class="sxs-lookup"><span data-stu-id="8ca14-119">Build an image based on the [Python image](https://hub.docker.com/_/python/) located on Docker Hub.</span></span> 

<span data-ttu-id="8ca14-120">Defina o contêiner do Docker em um Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="8ca14-120">Define your Docker container in a Dockerfile.</span></span> <span data-ttu-id="8ca14-121">O Dockerfile contém instruções para configurar o ambiente do seu contêiner, carregar o aplicativo que você deseja executar e mapear portas.</span><span class="sxs-lookup"><span data-stu-id="8ca14-121">The Dockerfile contains instructions for setting up the environment inside your container, loading the application you want to run, and mapping ports.</span></span> <span data-ttu-id="8ca14-122">O Dockerfile é a entrada para o comando `docker build`, que cria a imagem.</span><span class="sxs-lookup"><span data-stu-id="8ca14-122">The Dockerfile is the input to the `docker build` command, which creates the image.</span></span> 

<span data-ttu-id="8ca14-123">Crie um diretório vazio e crie o arquivo *Dockerfile* (sem extensão de arquivo).</span><span class="sxs-lookup"><span data-stu-id="8ca14-123">Create an empty directory and create the file *Dockerfile* (with no file extension).</span></span> <span data-ttu-id="8ca14-124">Adicione o seguinte ao *Dockerfile* e salve as alterações:</span><span class="sxs-lookup"><span data-stu-id="8ca14-124">Add the following to *Dockerfile* and save your changes:</span></span>

```
# Use an official Python runtime as a base image
FROM python:2.7-slim

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "app.py"]
```

<span data-ttu-id="8ca14-125">Leia a [referência do Dockerfile](https://docs.docker.com/engine/reference/builder/) para saber mais informações.</span><span class="sxs-lookup"><span data-stu-id="8ca14-125">Read the [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for more information.</span></span>

## <a name="create-a-simple-web-application"></a><span data-ttu-id="8ca14-126">Criar um aplicativo Web simples</span><span class="sxs-lookup"><span data-stu-id="8ca14-126">Create a simple web application</span></span>
<span data-ttu-id="8ca14-127">Crie um aplicativo Web Flask que escuta a porta 80 retornar "Olá, Mundo!".</span><span class="sxs-lookup"><span data-stu-id="8ca14-127">Create a Flask web application listening on port 80 that returns "Hello World!".</span></span>  <span data-ttu-id="8ca14-128">No mesmo diretório, crie o arquivo *requirements.txt*.</span><span class="sxs-lookup"><span data-stu-id="8ca14-128">In the same directory, create the file *requirements.txt*.</span></span>  <span data-ttu-id="8ca14-129">Adicione o seguinte e salve as alterações:</span><span class="sxs-lookup"><span data-stu-id="8ca14-129">Add the following and save your changes:</span></span>
```
Flask
```

<span data-ttu-id="8ca14-130">Crie também o arquivo *app.py* e adicione o seguinte:</span><span class="sxs-lookup"><span data-stu-id="8ca14-130">Also create the *app.py* file and add the following:</span></span>

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():
    
    return 'Hello World!'

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

## <a name="build-the-image"></a><span data-ttu-id="8ca14-131">Criar a imagem</span><span class="sxs-lookup"><span data-stu-id="8ca14-131">Build the image</span></span>
<span data-ttu-id="8ca14-132">Execute o comando `docker build` para criar a imagem que executa o seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="8ca14-132">Run the `docker build` command to create the image that runs your web application.</span></span> <span data-ttu-id="8ca14-133">Abra uma janela do PowerShell e navegue até *c:\temp\helloworldapp*.</span><span class="sxs-lookup"><span data-stu-id="8ca14-133">Open a PowerShell window and navigate to *c:\temp\helloworldapp*.</span></span> <span data-ttu-id="8ca14-134">Execute o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="8ca14-134">Run the following command:</span></span>

```bash
docker build -t helloworldapp .
```

<span data-ttu-id="8ca14-135">Esse comando cria a nova imagem usando as instruções no seu Dockerfile de nomeando (-t marcação) a imagem "helloworldapp".</span><span class="sxs-lookup"><span data-stu-id="8ca14-135">This command builds the new image using the instructions in your Dockerfile, naming (-t tagging) the image "helloworldapp".</span></span> <span data-ttu-id="8ca14-136">A criação de uma imagem puxa a imagem base do Hub do Docker e cria uma nova imagem que adiciona seu aplicativo sobre a imagem base.</span><span class="sxs-lookup"><span data-stu-id="8ca14-136">Building an image pulls the base image down from Docker Hub and creates a new image that adds your application on top of the base image.</span></span>  

<span data-ttu-id="8ca14-137">Depois de concluir o comando de compilação, execute o comando `docker images` para ver informações sobre a nova imagem:</span><span class="sxs-lookup"><span data-stu-id="8ca14-137">Once the build command completes, run the `docker images` command to see information on the new image:</span></span>

```bash
$ docker images
    
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              86838648aab6        2 minutes ago       194 MB
```

## <a name="run-the-application-locally"></a><span data-ttu-id="8ca14-138">Executar o aplicativo localmente</span><span class="sxs-lookup"><span data-stu-id="8ca14-138">Run the application locally</span></span>
<span data-ttu-id="8ca14-139">Verifique se seu aplicativo em contêineres está sendo executado localmente antes de enviar a ele o registro de contêiner.</span><span class="sxs-lookup"><span data-stu-id="8ca14-139">Verify that your containerized application runs locally before pushing it the container registry.</span></span>  

<span data-ttu-id="8ca14-140">Execute o aplicativo, mapeando a porta 4000 do computador para a porta 80 exposta do contêiner:</span><span class="sxs-lookup"><span data-stu-id="8ca14-140">Run the application, mapping your computer's port 4000 to the container's exposed port 80:</span></span>

```bash
docker run -d -p 4000:80 --name my-web-site helloworldapp
```

<span data-ttu-id="8ca14-141">*name* fornece um nome para o contêiner em execução (em vez da ID do contêiner).</span><span class="sxs-lookup"><span data-stu-id="8ca14-141">*name* gives a name to the running container (instead of the container ID).</span></span>

<span data-ttu-id="8ca14-142">Conectar-se ao contêiner em execução.</span><span class="sxs-lookup"><span data-stu-id="8ca14-142">Connect to the running container.</span></span>  <span data-ttu-id="8ca14-143">Abra um navegador da Web apontando para o endereço IP retornado na porta 4000, por exemplo "http://localhost:4000".</span><span class="sxs-lookup"><span data-stu-id="8ca14-143">Open a web browser pointing to the IP address returned on port 4000, for example "http://localhost:4000".</span></span> <span data-ttu-id="8ca14-144">Você deve ver o cabeçalho "Olá, Mundo!"</span><span class="sxs-lookup"><span data-stu-id="8ca14-144">You should see the heading "Hello World!"</span></span> <span data-ttu-id="8ca14-145">ser exibido no navegador.</span><span class="sxs-lookup"><span data-stu-id="8ca14-145">display in the browser.</span></span>

![Olá, Mundo!][hello-world]

<span data-ttu-id="8ca14-147">Para interromper o contêiner, execute:</span><span class="sxs-lookup"><span data-stu-id="8ca14-147">To stop your container, run:</span></span>

```bash
docker stop my-web-site
```

<span data-ttu-id="8ca14-148">Exclua o contêiner do seu computador de desenvolvimento:</span><span class="sxs-lookup"><span data-stu-id="8ca14-148">Delete the container from your development machine:</span></span>

```bash
docker rm my-web-site
```

## <a name="push-the-image-to-the-container-registry"></a><span data-ttu-id="8ca14-149">Enviar a imagem para o registro de contêiner</span><span class="sxs-lookup"><span data-stu-id="8ca14-149">Push the image to the container registry</span></span>
<span data-ttu-id="8ca14-150">Depois de verificar que o aplicativo é executado no Docker, envie a imagem por push para o registro no Registro de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ca14-150">After you verify that the application runs in Docker, push the image to your registry in Azure Container Registry.</span></span>

<span data-ttu-id="8ca14-151">Execute `docker login` para fazer logon em seu registro de contêiner as [credenciais de registro](../container-registry/container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="8ca14-151">Run `docker login` to log in to your container registry with your [registry credentials](../container-registry/container-registry-authentication.md).</span></span>

<span data-ttu-id="8ca14-152">O seguinte exemplo passa a ID e senha de uma [entidade de serviço](../active-directory/active-directory-application-objects.md) do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8ca14-152">The following example passes the ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="8ca14-153">Por exemplo, você pode atribuir uma entidade de serviço ao registro para um cenário de automação.</span><span class="sxs-lookup"><span data-stu-id="8ca14-153">For example, you might have assigned a service principal to your registry for an automation scenario.</span></span>  <span data-ttu-id="8ca14-154">Ou pode fazer logon usando o nome de usuário e a senha do registro.</span><span class="sxs-lookup"><span data-stu-id="8ca14-154">Or, you could login using your registry username and password.</span></span>

```bash
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="8ca14-155">O comando a seguir cria uma marca ou alias imagem, com um caminho totalmente qualificado para o registro.</span><span class="sxs-lookup"><span data-stu-id="8ca14-155">The following command creates a tag, or alias, of the image, with a fully qualified path to your registry.</span></span> <span data-ttu-id="8ca14-156">Este exemplo coloca a imagem no namespace `samples` para evitar confusão na raiz do registro.</span><span class="sxs-lookup"><span data-stu-id="8ca14-156">This example places the image in the `samples` namespace to avoid clutter in the root of the registry.</span></span>

```bash
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

<span data-ttu-id="8ca14-157">Enviar a imagem para o eu registro de contêiner:</span><span class="sxs-lookup"><span data-stu-id="8ca14-157">Push the image to your container registry:</span></span>

```bash
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="package-the-docker-image-with-yeoman"></a><span data-ttu-id="8ca14-158">Empacotar a imagem do Docker com o Yeoman</span><span class="sxs-lookup"><span data-stu-id="8ca14-158">Package the Docker image with Yeoman</span></span>
<span data-ttu-id="8ca14-159">O SDK do Service Fabric para Linux inclui um gerador [Yeoman](http://yeoman.io/) que facilita a criação de seu aplicativo e a adição de uma imagem de contêiner.</span><span class="sxs-lookup"><span data-stu-id="8ca14-159">The Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy to create your application and add a container image.</span></span> <span data-ttu-id="8ca14-160">Vamos usar o Yeoman para criar um aplicativo, com um único contêiner do Docker, chamado de *SimpleContainerApp*.</span><span class="sxs-lookup"><span data-stu-id="8ca14-160">Let's use Yeoman to create an application with a single Docker container called *SimpleContainerApp*.</span></span>

<span data-ttu-id="8ca14-161">Para criar um aplicativo de contêiner do Service Fabric, abra uma janela do terminal e execute `yo azuresfcontainer`.</span><span class="sxs-lookup"><span data-stu-id="8ca14-161">To create a Service Fabric container application, open a terminal window and run `yo azuresfcontainer`.</span></span>  

<span data-ttu-id="8ca14-162">Dê um nome para o seu aplicativo (por exemplo, “mycontainer”).</span><span class="sxs-lookup"><span data-stu-id="8ca14-162">Name your application (for example, "mycontainer").</span></span> 

<span data-ttu-id="8ca14-163">Forneça a URL da imagem de contêiner em um registro de contêiner (por exemplo, "").</span><span class="sxs-lookup"><span data-stu-id="8ca14-163">Provide the URL for the container image in a container registry (for example, "").</span></span> 

<span data-ttu-id="8ca14-164">Essa imagem tem um ponto de entrada de carga de trabalho-ponto definido e, portanto, precisa especificar explicitamente os comandos de entrada (comandos executados dentro do contêiner, o que manterá o contêiner em execução depois da inicialização).</span><span class="sxs-lookup"><span data-stu-id="8ca14-164">This image has a workload entry-point defined, so need to explicitly specify input commands (commands run inside the container, which will keep the container running after startup).</span></span> 

<span data-ttu-id="8ca14-165">Especifique a contagem de instâncias como "1".</span><span class="sxs-lookup"><span data-stu-id="8ca14-165">Specify an instance count of "1".</span></span>

![Gerador de Yeoman do Service Fabric para contêineres][sf-yeoman]

## <a name="configure-port-mapping-and-container-repository-authentication"></a><span data-ttu-id="8ca14-167">Configurar a autenticação de repositório de contêiner e o mapeamento de porta</span><span class="sxs-lookup"><span data-stu-id="8ca14-167">Configure port mapping and container repository authentication</span></span>
<span data-ttu-id="8ca14-168">O serviço em contêineres precisa de um ponto de extremidade para comunicação.</span><span class="sxs-lookup"><span data-stu-id="8ca14-168">Your containerized service needs an endpoint for communication.</span></span>  <span data-ttu-id="8ca14-169">Agora, adicione o protocolo, a porta e o tipo a um `Endpoint` no arquivo ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="8ca14-169">Now add the protocol, port, and type to an `Endpoint` in the ServiceManifest.xml file.</span></span> <span data-ttu-id="8ca14-170">Para este artigo, o serviço em contêineres escuta na porta 4000:</span><span class="sxs-lookup"><span data-stu-id="8ca14-170">For this article, the containerized service listens on port 4000:</span></span> 

```xml
<Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
```
<span data-ttu-id="8ca14-171">Ao fornecer `UriScheme`, o ponto de extremidade do contêiner é registrado automaticamente no serviço de Nomenclatura do Service Fabric para capacidade de descoberta.</span><span class="sxs-lookup"><span data-stu-id="8ca14-171">Providing the `UriScheme` automatically registers the container endpoint with the Service Fabric Naming service for discoverability.</span></span> <span data-ttu-id="8ca14-172">Um arquivo de exemplo servicemanifest. XML completo é fornecido no final deste artigo.</span><span class="sxs-lookup"><span data-stu-id="8ca14-172">A full ServiceManifest.xml example file is provided at the end of this article.</span></span> 

<span data-ttu-id="8ca14-173">Configure o mapeamento de porta, da porta para o host, do contêiner especificando uma política `PortBinding` no `ContainerHostPolicies` do arquivo ApplicationManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="8ca14-173">Configure the container port-to-host port mapping by specifying a `PortBinding` policy in `ContainerHostPolicies` of the ApplicationManifest.xml file.</span></span>  <span data-ttu-id="8ca14-174">Para este artigo, `ContainerPort` é 80 (o contêiner expõe a porta 80, conforme especificado no Dockerfile) e `EndpointRef` é "myserviceTypeEndpoint" (o ponto de extremidade definido no manifesto do serviço).</span><span class="sxs-lookup"><span data-stu-id="8ca14-174">For this article, `ContainerPort` is 80 (the container exposes port 80, as specified in the Dockerfile) and `EndpointRef` is "myserviceTypeEndpoint" (the endpoint defined in the service manifest).</span></span>  <span data-ttu-id="8ca14-175">As solicitações de entrada para o serviço na porta 4000 são mapeadas para a porta 80 no contêiner.</span><span class="sxs-lookup"><span data-stu-id="8ca14-175">Incoming requests to the service on port 4000 are mapped to port 80 on the container.</span></span>  <span data-ttu-id="8ca14-176">Se o seu contêiner precisar autenticar com um repositório privado, adicione `RepositoryCredentials`.</span><span class="sxs-lookup"><span data-stu-id="8ca14-176">If your container needs to authenticate with a private repository, then add `RepositoryCredentials`.</span></span>  <span data-ttu-id="8ca14-177">Para este artigo, adicione o nome da conta e a senha para o registro de contêiner de myregistry.azurecr.io.</span><span class="sxs-lookup"><span data-stu-id="8ca14-177">For this article, add the account name and password for the myregistry.azurecr.io container registry.</span></span> 

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

## <a name="build-and-package-the-service-fabric-application"></a><span data-ttu-id="8ca14-178">Compilar e empacotar o aplicativo do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8ca14-178">Build and package the Service Fabric application</span></span>
<span data-ttu-id="8ca14-179">Os modelos Yeoman do Service Fabric incluem um script de compilação para [Gradle](https://gradle.org/), que pode ser usado para compilar o aplicativo no terminal.</span><span class="sxs-lookup"><span data-stu-id="8ca14-179">The Service Fabric Yeoman templates include a build script for [Gradle](https://gradle.org/), which you can use to build the application from the terminal.</span></span> <span data-ttu-id="8ca14-180">Para compilar e empacotar o aplicativo, execute o seguinte:</span><span class="sxs-lookup"><span data-stu-id="8ca14-180">To build and package the application, run the following:</span></span>

```bash
cd mycontainer
gradle
```

## <a name="deploy-the-application"></a><span data-ttu-id="8ca14-181">Implantar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="8ca14-181">Deploy the application</span></span>
<span data-ttu-id="8ca14-182">Após a compilação do aplicativo, você pode implantá-lo no cluster local usando a CLI do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8ca14-182">Once the application is built, you can deploy it to the local cluster using the Service Fabric CLI.</span></span>

<span data-ttu-id="8ca14-183">Conectar-se ao cluster local do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8ca14-183">Connect to the local Service Fabric cluster.</span></span>

```bash
sfctl cluster select --endpoint http://localhost:19080
```

<span data-ttu-id="8ca14-184">Use o script de instalação fornecido no modelo para copiar o pacote de aplicativo no repositório de imagens do cluster, registrar o tipo de aplicativo e criar uma instância do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8ca14-184">Use the install script provided in the template to copy the application package to the cluster's image store, register the application type, and create an instance of the application.</span></span>

```bash
./install.sh
```

<span data-ttu-id="8ca14-185">Abra um navegador e navegue até o Service Fabric Explorer em http://localhost:19080/Explorer (substitua localhost pelo IP privado da VM se estiver usando Vagrant no Mac OS X).</span><span class="sxs-lookup"><span data-stu-id="8ca14-185">Open a browser and navigate to Service Fabric Explorer at http://localhost:19080/Explorer (replace localhost with the private IP of the VM if using Vagrant on Mac OS X).</span></span> <span data-ttu-id="8ca14-186">Expanda o nó Aplicativos e observe que agora há uma entrada para o seu tipo de aplicativo e outra para a primeira instância desse tipo.</span><span class="sxs-lookup"><span data-stu-id="8ca14-186">Expand the Applications node and note that there is now an entry for your application type and another for the first instance of that type.</span></span>

<span data-ttu-id="8ca14-187">Conectar-se ao contêiner em execução.</span><span class="sxs-lookup"><span data-stu-id="8ca14-187">Connect to the running container.</span></span>  <span data-ttu-id="8ca14-188">Abra um navegador da Web apontando para o endereço IP retornado na porta 4000, por exemplo "http://localhost:4000".</span><span class="sxs-lookup"><span data-stu-id="8ca14-188">Open a web browser pointing to the IP address returned on port 4000, for example "http://localhost:4000".</span></span> <span data-ttu-id="8ca14-189">Você deve ver o cabeçalho "Olá, Mundo!"</span><span class="sxs-lookup"><span data-stu-id="8ca14-189">You should see the heading "Hello World!"</span></span> <span data-ttu-id="8ca14-190">ser exibido no navegador.</span><span class="sxs-lookup"><span data-stu-id="8ca14-190">display in the browser.</span></span>

![Olá, Mundo!][hello-world]

## <a name="clean-up"></a><span data-ttu-id="8ca14-192">Limpar</span><span class="sxs-lookup"><span data-stu-id="8ca14-192">Clean up</span></span>
<span data-ttu-id="8ca14-193">Use o script de desinstalação fornecido com o modelo para excluir a instância do aplicativo no cluster de desenvolvimento local e cancelar o registro do tipo de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8ca14-193">Use the uninstall script provided in the template to delete the application instance from the local development cluster and unregister the application type.</span></span>

```bash
./uninstall.sh
```

<span data-ttu-id="8ca14-194">Depois que você enviar a imagem para o registro de contêiner, você pode excluir a imagem local do seu computador de desenvolvimento:</span><span class="sxs-lookup"><span data-stu-id="8ca14-194">After you push the image to the container registry you can delete the local image from your development computer:</span></span>

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a><span data-ttu-id="8ca14-195">Exemplo completo de manifestos de serviço e aplicativo do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="8ca14-195">Complete example Service Fabric application and service manifests</span></span>
<span data-ttu-id="8ca14-196">Aqui estão os manifestos de aplicativo e serviço completos usados neste artigo.</span><span class="sxs-lookup"><span data-stu-id="8ca14-196">Here are the complete service and application manifests used in this article.</span></span>

### <a name="servicemanifestxml"></a><span data-ttu-id="8ca14-197">ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="8ca14-197">ServiceManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="myservicePkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is the name of your ServiceType.
         The UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="myserviceType" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers 
      to Service Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
        <Commands></Commands>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables to your container: -->
    
    <EnvironmentVariables>
      <!--
      <EnvironmentVariable Name="VariableName" Value="VariableValue"/>
      -->
    </EnvironmentVariables>
    
  </CodePackage>

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by the communication listener to obtain the port on which to 
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a><span data-ttu-id="8ca14-198">ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="8ca14-198">ApplicationManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="mycontainerType"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <!-- Import the ServiceManifest from the ServicePackage. The ServiceManifestName and ServiceManifestVersion 
       should match the Name and Version attributes of the ServiceManifest element defined in the 
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
    <!-- The section below creates instances of service types, when an instance of this 
         application type is created. You can also create one or more instances of service type using the 
         ServiceFabric PowerShell module.
         
         The attribute ServiceTypeName below must match the name defined in the imported ServiceManifest.xml file. -->
    <Service Name="myservice">
      <!-- On a local development cluster, set InstanceCount to 1.  On a multi-node production 
      cluster, set InstanceCount to -1 for the container service to run on every node in 
      the cluster.
      -->
      <StatelessService ServiceTypeName="myserviceType" InstanceCount="1">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```
## <a name="adding-more-services-to-an-existing-application"></a><span data-ttu-id="8ca14-199">Adicionando mais serviços a um aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="8ca14-199">Adding more services to an existing application</span></span>

<span data-ttu-id="8ca14-200">Para adicionar outro serviço de contêiner a um aplicativo já criado usando o yeoman, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="8ca14-200">To add another container service to an application already created using yeoman, perform the following steps:</span></span>

1. <span data-ttu-id="8ca14-201">Altere o diretório para a raiz do aplicativo existente.</span><span class="sxs-lookup"><span data-stu-id="8ca14-201">Change directory to the root of the existing application.</span></span>  <span data-ttu-id="8ca14-202">Por exemplo, `cd ~/YeomanSamples/MyApplication`, se `MyApplication` é o aplicativo criado pelo Yeoman.</span><span class="sxs-lookup"><span data-stu-id="8ca14-202">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is the application created by Yeoman.</span></span>
2. <span data-ttu-id="8ca14-203">Execute o `yo azuresfcontainer:AddService`</span><span class="sxs-lookup"><span data-stu-id="8ca14-203">Run `yo azuresfcontainer:AddService`</span></span>

<a id="manually"></a>


## <a name="configure-time-interval-before-container-is-force-terminated"></a><span data-ttu-id="8ca14-204">Configurar o intervalo de tempo antes do contêiner ser forçado a terminar</span><span class="sxs-lookup"><span data-stu-id="8ca14-204">Configure time interval before container is force terminated</span></span>

<span data-ttu-id="8ca14-205">Você pode configurar um intervalo de tempo para a execução aguardar antes do contêiner ser removido após a exclusão do serviço (ou um movimento para outro nó) ter iniciado.</span><span class="sxs-lookup"><span data-stu-id="8ca14-205">You can configure a time interval for the runtime to wait before the container is removed after the service deletion (or a move to another node) has started.</span></span> <span data-ttu-id="8ca14-206">Configurar o intervalo de tempo envia o comando `docker stop <time in seconds>` para o contêiner.</span><span class="sxs-lookup"><span data-stu-id="8ca14-206">Configuring the time interval sends the `docker stop <time in seconds>` command to the container.</span></span>   <span data-ttu-id="8ca14-207">Para obter mais detalhes, consulte [parar docker](https://docs.docker.com/engine/reference/commandline/stop/).</span><span class="sxs-lookup"><span data-stu-id="8ca14-207">For more detail, see [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span></span> <span data-ttu-id="8ca14-208">O intervalo de tempo de espera é especificado na seção `Hosting`.</span><span class="sxs-lookup"><span data-stu-id="8ca14-208">The time interval to wait is specified under the `Hosting` section.</span></span> <span data-ttu-id="8ca14-209">O trecho de manifesto do cluster a seguir mostra como definir o intervalo de espera:</span><span class="sxs-lookup"><span data-stu-id="8ca14-209">The following cluster manifest snippet shows how to set the wait interval:</span></span>

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
<span data-ttu-id="8ca14-210">O intervalo de tempo padrão é definido para 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="8ca14-210">The default time interval is set to 10 seconds.</span></span> <span data-ttu-id="8ca14-211">Como essa configuração é dinâmica, uma configuração somente atualiza no cluster que atualiza no tempo limite.</span><span class="sxs-lookup"><span data-stu-id="8ca14-211">Since this configuration is dynamic, a config only upgrade on the cluster updates the timeout.</span></span> 


## <a name="configure-the-runtime-to-remove-unused-container-images"></a><span data-ttu-id="8ca14-212">Configurar a execução para remover as imagens de contêiner não utilizadas</span><span class="sxs-lookup"><span data-stu-id="8ca14-212">Configure the runtime to remove unused container images</span></span>

<span data-ttu-id="8ca14-213">Você pode configurar o cluster do Service Fabric para remover as imagens de contêiner não utilizadas do nó.</span><span class="sxs-lookup"><span data-stu-id="8ca14-213">You can configure the Service Fabric cluster to remove unused container images from the node.</span></span> <span data-ttu-id="8ca14-214">Essa configuração permite que o espaço em disco seja recapturado se houver imagens de contêiner demais no nó.</span><span class="sxs-lookup"><span data-stu-id="8ca14-214">This configuration allows disk space to be recaptured if too many container images are present on the node.</span></span>  <span data-ttu-id="8ca14-215">Para habilitar esse recurso, atualize a `Hosting` seção no manifesto do cluster, conforme mostrado no trecho a seguir:</span><span class="sxs-lookup"><span data-stu-id="8ca14-215">To enable this feature, update the `Hosting` section in the cluster manifest as shown in the following snippet:</span></span> 


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

<span data-ttu-id="8ca14-216">Para as imagens que não devem ser excluídas, você pode especificá-las no parâmetro `ContainerImagesToSkip`.</span><span class="sxs-lookup"><span data-stu-id="8ca14-216">For images that should not be deleted, you can specify them under the `ContainerImagesToSkip` parameter.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="8ca14-217">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8ca14-217">Next steps</span></span>
* <span data-ttu-id="8ca14-218">Saiba mais sobre como executar [contêineres no Service Fabric](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8ca14-218">Learn more about running [containers on Service Fabric](service-fabric-containers-overview.md).</span></span>
* <span data-ttu-id="8ca14-219">Leia o tutorial [Como implantar um aplicativo .NET em um contêiner](service-fabric-host-app-in-a-container.md).</span><span class="sxs-lookup"><span data-stu-id="8ca14-219">Read the [Deploy a .NET application in a container](service-fabric-host-app-in-a-container.md) tutorial.</span></span>
* <span data-ttu-id="8ca14-220">Leia mais sobre o [ciclo de vida do aplicativo](service-fabric-application-lifecycle.md) do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="8ca14-220">Learn about the Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
* <span data-ttu-id="8ca14-221">Confira os [exemplos de código do Service Fabric](https://github.com/Azure-Samples/service-fabric-dotnet-containers) no GitHub.</span><span class="sxs-lookup"><span data-stu-id="8ca14-221">Checkout the [Service Fabric container code samples](https://github.com/Azure-Samples/service-fabric-dotnet-containers) on GitHub.</span></span>

[hello-world]: ./media/service-fabric-get-started-containers-linux/HelloWorld.png
[sf-yeoman]: ./media/service-fabric-get-started-containers-linux/YoSF.png
