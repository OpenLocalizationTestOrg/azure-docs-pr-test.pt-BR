---
title: "Crie seu primeiro aplicativo de microsserviços do Azure no Linux usando C# | Microsoft Docs"
description: Criar e implantar um aplicativo do Service Fabric usando C#
services: service-fabric
documentationcenter: csharp
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 5a96d21d-fa4a-4dc2-abe8-a830a3482fb1
ms.service: service-fabric
ms.devlang: csharp
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/21/2017
ms.author: subramar
ms.openlocfilehash: adcafaa5522fcddc0a01eb1dc8deba04ebfc38f2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-azure-service-fabric-application"></a><span data-ttu-id="3e1d0-103">Criar seu primeiro aplicativo do Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="3e1d0-103">Create your first Azure Service Fabric application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3e1d0-104">C# - Windows</span><span class="sxs-lookup"><span data-stu-id="3e1d0-104">C# - Windows</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
> * [<span data-ttu-id="3e1d0-105">Java - Linux</span><span class="sxs-lookup"><span data-stu-id="3e1d0-105">Java - Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
> * [<span data-ttu-id="3e1d0-106">C# - Linux</span><span class="sxs-lookup"><span data-stu-id="3e1d0-106">C# - Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

<span data-ttu-id="3e1d0-107">O Service Fabric fornece SDKs para compilação de serviços no Linux em .NET Core e Java.</span><span class="sxs-lookup"><span data-stu-id="3e1d0-107">Service Fabric provides SDKs for building services on Linux in both .NET Core and Java.</span></span> <span data-ttu-id="3e1d0-108">Neste tutorial, vamos ver como criar um aplicativo para Linux e compilar um serviço usando C# (.NET Core).</span><span class="sxs-lookup"><span data-stu-id="3e1d0-108">In this tutorial, we look at how to create an application for Linux and build a service using C# (.NET Core).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e1d0-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3e1d0-109">Prerequisites</span></span>
<span data-ttu-id="3e1d0-110">Antes de começar, verifique se você [configurar o ambiente de desenvolvimento Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="3e1d0-110">Before you get started, make sure that you have [set up your Linux development environment](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="3e1d0-111">Se você estiver usando Mac OS X, poderá [configurar um ambiente de uma caixa do Linux em uma máquina virtual usando Vagrant](service-fabric-get-started-mac.md).</span><span class="sxs-lookup"><span data-stu-id="3e1d0-111">If you are using Mac OS X, you can [set up a Linux one-box environment in a virtual machine using Vagrant](service-fabric-get-started-mac.md).</span></span>

<span data-ttu-id="3e1d0-112">Você também desejará instalar a [CLI do Service Fabric](service-fabric-cli.md)</span><span class="sxs-lookup"><span data-stu-id="3e1d0-112">You will also want to install the [Service Fabric CLI](service-fabric-cli.md)</span></span>

### <a name="install-and-set-up-the-generators-for-csharp"></a><span data-ttu-id="3e1d0-113">Instalar e configurar os geradores para CSharp</span><span class="sxs-lookup"><span data-stu-id="3e1d0-113">Install and set up the generators for CSharp</span></span>
<span data-ttu-id="3e1d0-114">O Service Fabric fornece ferramentas de scaffolding que ajudarão a criar um aplicativo em CSharp do Service Fabric no terminal usando gerador de modelos Yeoman.</span><span class="sxs-lookup"><span data-stu-id="3e1d0-114">Service Fabric provides scaffolding tools which will help you create a Service Fabric CSharp application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="3e1d0-115">Execute as etapas abaixo para garantir que você tenha o gerador de modelos yeoman do Service Fabric para CSharp funcionando em seu computador.</span><span class="sxs-lookup"><span data-stu-id="3e1d0-115">Please follow the steps below to ensure you have the Service Fabric yeoman template generator for CSharp working on your machine.</span></span>
1. <span data-ttu-id="3e1d0-116">Instalar o nodejs e o NPM em seu computador</span><span class="sxs-lookup"><span data-stu-id="3e1d0-116">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="3e1d0-117">Instalar o gerador de modelos [Yeoman](http://yeoman.io/) em seu computador a partir do NPM</span><span class="sxs-lookup"><span data-stu-id="3e1d0-117">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="3e1d0-118">Instalar o gerador de aplicativos Java Yeo do Service Fabric a partir do NPM</span><span class="sxs-lookup"><span data-stu-id="3e1d0-118">Install the Service Fabric Yeo Java application generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfcsharp
  ```

## <a name="create-the-application"></a><span data-ttu-id="3e1d0-119">Criar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="3e1d0-119">Create the application</span></span>
<span data-ttu-id="3e1d0-120">Um aplicativo do Service Fabric pode conter um ou mais serviços, cada um com uma função específica no fornecimento de funcionalidade do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3e1d0-120">A Service Fabric application can contain one or more services, each with a specific role in delivering the application's functionality.</span></span> <span data-ttu-id="3e1d0-121">O gerador [Yeoman](http://yeoman.io/) do Service Fabric para CSharp, instalado na última etapa, que facilita a criação de seu primeiro serviço e a adição de mais serviços posteriormente.</span><span class="sxs-lookup"><span data-stu-id="3e1d0-121">The Service Fabric [Yeoman](http://yeoman.io/) generator for CSharp, which you installed in last step, makes it easy to create your first service and to add more later.</span></span> <span data-ttu-id="3e1d0-122">Vamos usar Yeoman para criar um novo aplicativo com um único serviço.</span><span class="sxs-lookup"><span data-stu-id="3e1d0-122">Let's use Yeoman to create an application with a single service.</span></span>

1. <span data-ttu-id="3e1d0-123">Em um terminal, digite o comando a seguir para começar a criar o scaffolding: `yo azuresfcsharp`</span><span class="sxs-lookup"><span data-stu-id="3e1d0-123">In a terminal, type the following command to start building the scaffolding: `yo azuresfcsharp`</span></span>
2. <span data-ttu-id="3e1d0-124">Nome do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3e1d0-124">Name your application.</span></span>
3. <span data-ttu-id="3e1d0-125">Escolha o tipo de seu primeiro serviço e dê um nome para ele.</span><span class="sxs-lookup"><span data-stu-id="3e1d0-125">Choose the type of your first service and name it.</span></span> <span data-ttu-id="3e1d0-126">Para os fins deste tutorial, escolheremos o Serviço Reliable Actor.</span><span class="sxs-lookup"><span data-stu-id="3e1d0-126">For the purposes of this tutorial, we choose a Reliable Actor Service.</span></span>

   ![Gerador de Yeoman do Service Fabric para C#][sf-yeoman]

> [!NOTE]
> <span data-ttu-id="3e1d0-128">Para obter mais informações sobre as opções, confira [Visão geral do modelo de programação do Service Fabric](service-fabric-choose-framework.md).</span><span class="sxs-lookup"><span data-stu-id="3e1d0-128">For more information about the options, see [Service Fabric programming model overview](service-fabric-choose-framework.md).</span></span>
>
>

## <a name="build-the-application"></a><span data-ttu-id="3e1d0-129">Compilar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="3e1d0-129">Build the application</span></span>
<span data-ttu-id="3e1d0-130">Os modelos Yeoman do Service Fabric incluem um script de build para criar o aplicativo por meio do terminal (após navegar até a pasta do terminal).</span><span class="sxs-lookup"><span data-stu-id="3e1d0-130">The Service Fabric Yeoman templates include a build script that you can use to build the app from the terminal (after navigating to the application folder).</span></span>

  ```sh
 cd myapp
 ./build.sh
  ```

## <a name="deploy-the-application"></a><span data-ttu-id="3e1d0-131">Implantar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="3e1d0-131">Deploy the application</span></span>

<span data-ttu-id="3e1d0-132">Após a compilação do aplicativo, você pode implantá-lo no cluster local.</span><span class="sxs-lookup"><span data-stu-id="3e1d0-132">Once the application is built, you can deploy it to the local cluster.</span></span>

1. <span data-ttu-id="3e1d0-133">Conectar-se ao cluster local do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="3e1d0-133">Connect to the local Service Fabric cluster.</span></span>

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. <span data-ttu-id="3e1d0-134">Use o script de instalação fornecido no modelo para copiar o pacote de aplicativo no repositório de imagens do cluster, registre o tipo de aplicativo e crie uma instância do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3e1d0-134">Run the install script provided in the template to copy the application package to the cluster's image store, register the application type, and create an instance of the application.</span></span>

    ```bash
    ./install.sh
    ```

<span data-ttu-id="3e1d0-135">A implantação do aplicativo interno é igual a qualquer outro aplicativo do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="3e1d0-135">Deploying the built application is the same as any other Service Fabric application.</span></span> <span data-ttu-id="3e1d0-136">Consulte a documentação sobre [como gerenciar um aplicativo do Service Fabric com a CLI do Service Fabric](service-fabric-application-lifecycle-sfctl.md) para obter instruções detalhadas.</span><span class="sxs-lookup"><span data-stu-id="3e1d0-136">See the documentation on [managing a Service Fabric application with the Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) for detailed instructions.</span></span>

<span data-ttu-id="3e1d0-137">Os parâmetros para esses comandos podem ser encontrados nos manifestos gerados dentro do pacote de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="3e1d0-137">Parameters to these commands can be found in the generated manifests inside the application package.</span></span>

<span data-ttu-id="3e1d0-138">Depois da implantação do aplicativo, abra um navegador e navegue até [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) em [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="3e1d0-138">Once the application has been deployed, open a browser and navigate to [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) at [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="3e1d0-139">Em seguida, expanda o nó **Aplicativos** e observe que agora há uma entrada para o seu tipo de aplicativo e outra para a primeira instância desse tipo.</span><span class="sxs-lookup"><span data-stu-id="3e1d0-139">Then, expand the **Applications** node and note that there is now an entry for your application type and another for the first instance of that type.</span></span>

## <a name="start-the-test-client-and-perform-a-failover"></a><span data-ttu-id="3e1d0-140">Inicie o cliente de teste e execute um failover</span><span class="sxs-lookup"><span data-stu-id="3e1d0-140">Start the test client and perform a failover</span></span>
<span data-ttu-id="3e1d0-141">Projetos de atores não fazem nada por conta própria.</span><span class="sxs-lookup"><span data-stu-id="3e1d0-141">Actor projects do not do anything on their own.</span></span> <span data-ttu-id="3e1d0-142">Eles exigem outro serviço ou cliente para enviar mensagens a eles.</span><span class="sxs-lookup"><span data-stu-id="3e1d0-142">They require another service or client to send them messages.</span></span> <span data-ttu-id="3e1d0-143">O modelo de ator inclui um script de teste simples que você pode usar para interagir com o serviço de ator.</span><span class="sxs-lookup"><span data-stu-id="3e1d0-143">The actor template includes a simple test script that you can use to interact with the actor service.</span></span>

1. <span data-ttu-id="3e1d0-144">Execute o script usando o utilitário de inspeção para ver a saída do serviço de ator.</span><span class="sxs-lookup"><span data-stu-id="3e1d0-144">Run the script using the watch utility to see the output of the actor service.</span></span>

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```
2. <span data-ttu-id="3e1d0-145">No Service Fabric Explorer, localize o nó que hospeda a réplica primária para o serviço de ator.</span><span class="sxs-lookup"><span data-stu-id="3e1d0-145">In Service Fabric Explorer, locate node hosting the primary replica for the actor service.</span></span> <span data-ttu-id="3e1d0-146">Na captura de tela abaixo, é o nó 3.</span><span class="sxs-lookup"><span data-stu-id="3e1d0-146">In the screenshot below, it is node 3.</span></span>

    ![Localizar a réplica primária no Service Fabric Explorer][sfx-primary]
3. <span data-ttu-id="3e1d0-148">Clique no nó encontrado na etapa anterior e selecione **Desativar (Reiniciar)** no menu Ações.</span><span class="sxs-lookup"><span data-stu-id="3e1d0-148">Click the node you found in the previous step, then select **Deactivate (restart)** from the Actions menu.</span></span> <span data-ttu-id="3e1d0-149">Esta ação reiniciará um nó no cluster local e forçará um failover para uma das réplicas secundárias em execução em outro nó.</span><span class="sxs-lookup"><span data-stu-id="3e1d0-149">This action restarts one node in your local cluster forcing a failover to a secondary replica running on another node.</span></span> <span data-ttu-id="3e1d0-150">Ao fazer isso, preste atenção à saída do cliente de teste e observe que o contador continua a aumentar apesar do failover.</span><span class="sxs-lookup"><span data-stu-id="3e1d0-150">As you perform this action, pay attention to the output from the test client and note that the counter continues to increment despite the failover.</span></span>

## <a name="adding-more-services-to-an-existing-application"></a><span data-ttu-id="3e1d0-151">Adicionando mais serviços a um aplicativo existente</span><span class="sxs-lookup"><span data-stu-id="3e1d0-151">Adding more services to an existing application</span></span>

<span data-ttu-id="3e1d0-152">Para adicionar outro serviço a um aplicativo já criado usando `yo`, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="3e1d0-152">To add another service to an application already created using `yo`, perform the following steps:</span></span>
1. <span data-ttu-id="3e1d0-153">Altere o diretório para a raiz do aplicativo existente.</span><span class="sxs-lookup"><span data-stu-id="3e1d0-153">Change directory to the root of the existing application.</span></span>  <span data-ttu-id="3e1d0-154">Por exemplo, `cd ~/YeomanSamples/MyApplication`, se `MyApplication` é o aplicativo criado pelo Yeoman.</span><span class="sxs-lookup"><span data-stu-id="3e1d0-154">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is the application created by Yeoman.</span></span>
2. <span data-ttu-id="3e1d0-155">Execute o `yo azuresfcsharp:AddService`</span><span class="sxs-lookup"><span data-stu-id="3e1d0-155">Run `yo azuresfcsharp:AddService`</span></span>

## <a name="migrating-from-projectjson-to-csproj"></a><span data-ttu-id="3e1d0-156">Migração do project.json para o .csproj</span><span class="sxs-lookup"><span data-stu-id="3e1d0-156">Migrating from project.json to .csproj</span></span>
1. <span data-ttu-id="3e1d0-157">Executar 'dotnet migrar' no diretório raiz do projeto migrará todos os project.json para o formato csproj.</span><span class="sxs-lookup"><span data-stu-id="3e1d0-157">Running 'dotnet migrate' in project root directory will migrate all the project.json to csproj format.</span></span>
2. <span data-ttu-id="3e1d0-158">Atualize as referências de projeto de acordo com os arquivos csproj em arquivos de projeto.</span><span class="sxs-lookup"><span data-stu-id="3e1d0-158">Update the project references accordingly to csproj files in project files.</span></span>
3. <span data-ttu-id="3e1d0-159">Atualize os nomes de arquivo de projeto para arquivos csproj em build.sh.</span><span class="sxs-lookup"><span data-stu-id="3e1d0-159">Update the project file names to csproj files in build.sh.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e1d0-160">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3e1d0-160">Next steps</span></span>

* [<span data-ttu-id="3e1d0-161">Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="3e1d0-161">Learn more about Reliable Actors</span></span>](service-fabric-reliable-actors-introduction.md)
* [<span data-ttu-id="3e1d0-162">Interação com os clusters do Service Fabric usando a CLI do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="3e1d0-162">Interacting with Service Fabric clusters using the Service Fabric CLI</span></span>](service-fabric-cli.md)
* <span data-ttu-id="3e1d0-163">Saiba mais sobre as [opções de suporte do Service Fabric](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="3e1d0-163">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>
* [<span data-ttu-id="3e1d0-164">Introdução à CLI do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="3e1d0-164">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-csharp/yeoman-csharp.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-csharp/sfx-primary.png
