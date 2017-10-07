---
title: "aaaDeploy um aplicativo .NET em um contêiner de tooAzure Service Fabric | Microsoft Docs"
description: "Ensina como toopackage um aplicativo .NET no Visual Studio em um contêiner do Docker. Esse novo aplicativo de \"contêiner\", em seguida, é implantado cluster do Service Fabric tooa."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: mikhegn
ms.openlocfilehash: 094b0e71d76b2e56ffb9b23638dd8154b3aff5fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-net-application-in-a-windows-container-tooazure-service-fabric"></a><span data-ttu-id="9e12b-104">Implantar um aplicativo .NET em um contêiner de Windows tooAzure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9e12b-104">Deploy a .NET application in a Windows container tooAzure Service Fabric</span></span>

<span data-ttu-id="9e12b-105">Este tutorial mostra como toodeploy um aplicativo ASP.NET existente em um contêiner do Windows no Azure.</span><span class="sxs-lookup"><span data-stu-id="9e12b-105">This tutorial shows you how toodeploy an existing ASP.NET application in a Windows container on Azure.</span></span>

<span data-ttu-id="9e12b-106">Neste tutorial, você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="9e12b-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9e12b-107">Criar um projeto do Docker no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9e12b-107">Create a Docker project in Visual Studio</span></span>
> * <span data-ttu-id="9e12b-108">Colocar um aplicativo existente em um contêiner</span><span class="sxs-lookup"><span data-stu-id="9e12b-108">Containerize an existing application</span></span>
> * <span data-ttu-id="9e12b-109">Configurar a integração contínua com o Visual Studio e o VSTS</span><span class="sxs-lookup"><span data-stu-id="9e12b-109">Setup continuous integration with Visual Studio and VSTS</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e12b-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9e12b-110">Prerequisites</span></span>

1. <span data-ttu-id="9e12b-111">Instalar o [Docker CE para Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description) de forma que você possa executar contêineres no Windows 10.</span><span class="sxs-lookup"><span data-stu-id="9e12b-111">Install [Docker CE for Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description) so that you can run containers on Windows 10.</span></span>
2. <span data-ttu-id="9e12b-112">Familiarize-se com hello [início rápido de contêineres do Windows 10][link-container-quickstart].</span><span class="sxs-lookup"><span data-stu-id="9e12b-112">Familiarize yourself with hello [Windows 10 Containers quickstart][link-container-quickstart].</span></span>
3. <span data-ttu-id="9e12b-113">Baixar Olá [Fabrikam fibra CallCenter] [ link-fabrikam-github] aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="9e12b-113">Download hello [Fabrikam Fiber CallCenter][link-fabrikam-github] sample application.</span></span>
4. <span data-ttu-id="9e12b-114">Instalar o [Azure PowerShell][link-azure-powershell-install]</span><span class="sxs-lookup"><span data-stu-id="9e12b-114">Install [Azure PowerShell][link-azure-powershell-install]</span></span>
5. <span data-ttu-id="9e12b-115">Instalar Olá [extensão de ferramentas de entrega contínua para 2017 do Visual Studio][link-visualstudio-cd-extension]</span><span class="sxs-lookup"><span data-stu-id="9e12b-115">Install hello [Continuous Delivery Tools extension for Visual Studio 2017][link-visualstudio-cd-extension]</span></span>
6. <span data-ttu-id="9e12b-116">Criar uma [assinatura do Azure][link-azure-subscription] e uma [conta do Visual Studio Team Services][link-vsts-account].</span><span class="sxs-lookup"><span data-stu-id="9e12b-116">Create an [Azure subscription][link-azure-subscription] and a [Visual Studio Team Services account][link-vsts-account].</span></span> 
7. [<span data-ttu-id="9e12b-117">Criar um cluster no Azure</span><span class="sxs-lookup"><span data-stu-id="9e12b-117">Create a cluster on Azure</span></span>](service-fabric-tutorial-create-cluster-azure-ps.md)

## <a name="containerize-hello-application"></a><span data-ttu-id="9e12b-118">Coloca o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="9e12b-118">Containerize hello application</span></span>

<span data-ttu-id="9e12b-119">Agora que você tem um [cluster do Service Fabric está em execução no Azure](service-fabric-tutorial-create-cluster-azure-ps.md) são toocreate pronto e implantar um aplicativo em contêineres.</span><span class="sxs-lookup"><span data-stu-id="9e12b-119">Now that you have a [Service Fabric cluster is running in Azure](service-fabric-tutorial-create-cluster-azure-ps.md) you are ready toocreate and deploy a containerized application.</span></span> <span data-ttu-id="9e12b-120">toostart executar o aplicativo em um contêiner, é preciso tooadd **Docker suporte** toohello projeto no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9e12b-120">toostart running our application in a container, we need tooadd **Docker Support** toohello project in Visual Studio.</span></span> <span data-ttu-id="9e12b-121">Quando você adiciona **suporte Docker** toohello aplicativo, duas coisas acontecem.</span><span class="sxs-lookup"><span data-stu-id="9e12b-121">When you add **Docker support** toohello application, two things happen.</span></span> <span data-ttu-id="9e12b-122">Primeiro, um _Dockerfile_ é adicionado toohello projeto.</span><span class="sxs-lookup"><span data-stu-id="9e12b-122">First, a _Dockerfile_ is added toohello project.</span></span> <span data-ttu-id="9e12b-123">Esse novo arquivo descreve como a imagem de contêiner de saudação é toobe criado.</span><span class="sxs-lookup"><span data-stu-id="9e12b-123">This new file describes how hello container image is toobe built.</span></span> <span data-ttu-id="9e12b-124">Em seguida, segundo, um novo _compor docker_ projeto é adicionado toohello solução.</span><span class="sxs-lookup"><span data-stu-id="9e12b-124">Then second, a new _docker-compose_ project is added toohello solution.</span></span> <span data-ttu-id="9e12b-125">Olá, novo projeto contém alguns arquivos de compor docker.</span><span class="sxs-lookup"><span data-stu-id="9e12b-125">hello new project contains a few docker-compose files.</span></span> <span data-ttu-id="9e12b-126">Compor docker arquivos podem ser usado toodescribe como contêiner Olá é executado.</span><span class="sxs-lookup"><span data-stu-id="9e12b-126">Docker-compose files can be used toodescribe how hello container is run.</span></span>

<span data-ttu-id="9e12b-127">Mais informações sobre como trabalhar com as [Ferramentas de Contêiner do Visual Studio][link-visualstudio-container-tools].</span><span class="sxs-lookup"><span data-stu-id="9e12b-127">More info on working with [Visual Studio Container Tools][link-visualstudio-container-tools].</span></span>

>[!NOTE]
><span data-ttu-id="9e12b-128">Se for Olá primeira vez que você está executando a imagens de contêiner do Windows em seu computador, Docker CE deve suspenso imagens de base Olá para os contêineres.</span><span class="sxs-lookup"><span data-stu-id="9e12b-128">If it is hello first time you are running Windows container images on your computer, Docker CE must pull down hello base images for your containers.</span></span> <span data-ttu-id="9e12b-129">imagens de saudação usadas neste tutorial são 14 GB.</span><span class="sxs-lookup"><span data-stu-id="9e12b-129">hello images used in this tutorial are 14 GB.</span></span> <span data-ttu-id="9e12b-130">Vá em frente e execute Olá base imagens do comando terminal toopull Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="9e12b-130">Go ahead and run hello following terminal command toopull hello base images:</span></span>
>```cmd
>docker pull microsoft/mssql-server-windows-developer
>docker pull microsoft/aspnet:4.6.2
>```

### <a name="add-docker-support"></a><span data-ttu-id="9e12b-131">Adicionar suporte ao Docker</span><span class="sxs-lookup"><span data-stu-id="9e12b-131">Add Docker support</span></span>

<span data-ttu-id="9e12b-132">Olá abrir [FabrikamFiber.CallCenter.sln] [ link-fabrikam-github] arquivo no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9e12b-132">Open hello [FabrikamFiber.CallCenter.sln][link-fabrikam-github] file in Visual Studio.</span></span>

<span data-ttu-id="9e12b-133">Saudação de atalho **FabrikamFiber.Web** projeto > **adicionar** > **Docker suporte**.</span><span class="sxs-lookup"><span data-stu-id="9e12b-133">Right-click hello **FabrikamFiber.Web** project > **Add** > **Docker Support**.</span></span>

### <a name="add-support-for-sql"></a><span data-ttu-id="9e12b-134">Adicionar suporte para SQL</span><span class="sxs-lookup"><span data-stu-id="9e12b-134">Add support for SQL</span></span>

<span data-ttu-id="9e12b-135">Este aplicativo usa SQL como provedor de dados Olá, para que um SQL server é necessário toorun Olá aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9e12b-135">This application uses SQL as hello data provider, so a SQL server is required toorun hello application.</span></span> <span data-ttu-id="9e12b-136">Referencie uma imagem de contêiner do SQL Server em nosso arquivo docker-compose.override.yml.</span><span class="sxs-lookup"><span data-stu-id="9e12b-136">Reference a SQL Server container image in our docker-compose.override.yml file.</span></span>

<span data-ttu-id="9e12b-137">No Visual Studio, abra **Gerenciador de soluções**, localizar **compor docker**e o arquivo aberto Olá **compose.override.yml docker**.</span><span class="sxs-lookup"><span data-stu-id="9e12b-137">In Visual Studio, open **Solution Explorer**, find **docker-compose**, and open hello file **docker-compose.override.yml**.</span></span>

<span data-ttu-id="9e12b-138">Navegue toohello `services:` nó, adicionar um nó denominado `db:` que define a entrada do SQL Server Olá para o contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="9e12b-138">Navigate toohello `services:` node, add a node named `db:` that defines hello SQL Server entry for hello container.</span></span>

```yml
  db:
    image: microsoft/mssql-server-windows-developer
    environment:
      sa_password: "Password1"
      ACCEPT_EULA: "Y"
    ports:
      - "1433"
    healthcheck:
      test: [ "CMD", "sqlcmd", "-U", "sa", "-P", "Password1", "-Q", "select 1" ]
      interval: 1s
      retries: 20
```

>[!NOTE]
><span data-ttu-id="9e12b-139">Você pode usar qualquer SQL Server que preferir para a depuração local, desde que ele seja acessível no host.</span><span class="sxs-lookup"><span data-stu-id="9e12b-139">You can use any SQL Server you prefer for local debugging, as long as it is reachable from your host.</span></span> <span data-ttu-id="9e12b-140">No entanto, **localdb** não dá suporte à comunicação `container -> host`.</span><span class="sxs-lookup"><span data-stu-id="9e12b-140">However, **localdb** does not support `container -> host` communication.</span></span>

>[!WARNING]
><span data-ttu-id="9e12b-141">A execução do SQL Server em um contêiner não dá suporte a dados persistentes.</span><span class="sxs-lookup"><span data-stu-id="9e12b-141">Running SQL Server in a container does not support persisting data.</span></span> <span data-ttu-id="9e12b-142">Quando o contêiner de saudação for interrompida, seus dados são apagados.</span><span class="sxs-lookup"><span data-stu-id="9e12b-142">When hello container stops, your data is erased.</span></span> <span data-ttu-id="9e12b-143">Não use essa configuração para produção.</span><span class="sxs-lookup"><span data-stu-id="9e12b-143">Do not use this configuration for production.</span></span>

<span data-ttu-id="9e12b-144">Navegue toohello `fabrikamfiber.web:` nó e adicionar um nó filho denominado `depends_on:`.</span><span class="sxs-lookup"><span data-stu-id="9e12b-144">Navigate toohello `fabrikamfiber.web:` node and add a child node named `depends_on:`.</span></span> <span data-ttu-id="9e12b-145">Isso garante que Olá `db` serviço (contêiner de saudação do SQL Server) é iniciado antes de nosso aplicativo web (fabrikamfiber.web).</span><span class="sxs-lookup"><span data-stu-id="9e12b-145">This ensures that hello `db` service (hello SQL Server container) starts before our web application (fabrikamfiber.web).</span></span>

```yml
  fabrikamfiber.web:
    depends_on:
      - db
```

### <a name="update-hello-web-config"></a><span data-ttu-id="9e12b-146">Atualizar a configuração de web Olá</span><span class="sxs-lookup"><span data-stu-id="9e12b-146">Update hello web config</span></span>

<span data-ttu-id="9e12b-147">Em Olá **FabrikamFiber.Web** projeto, a cadeia de caracteres de conexão Olá de atualização em hello **Web. config** de arquivos toopoint toohello do SQL Server no contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="9e12b-147">Back in hello **FabrikamFiber.Web** project, update hello connection string in hello **web.config** file, toopoint toohello SQL Server in hello container.</span></span>

```xml
<add name="FabrikamFiber-Express" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />

<add name="FabrikamFiber-DataWarehouse" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />
```

>[!NOTE]
><span data-ttu-id="9e12b-148">Se você quiser toouse um SQL Server diferente durante a criação de uma versão de compilação do seu aplicativo web, adicione outro arquivo de web.release.config do tooyour cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="9e12b-148">If you want toouse a different SQL Server when building a release build of your web application, add another connection string tooyour web.release.config file.</span></span>

### <a name="test-your-container"></a><span data-ttu-id="9e12b-149">Testar o contêiner</span><span class="sxs-lookup"><span data-stu-id="9e12b-149">Test your container</span></span>

<span data-ttu-id="9e12b-150">Pressione **F5** toorun e depurar aplicativo hello em seu contêiner.</span><span class="sxs-lookup"><span data-stu-id="9e12b-150">Press **F5** toorun and debug hello application in your container.</span></span>

<span data-ttu-id="9e12b-151">Borda abre a página de inicialização definido do seu aplicativo usando o endereço IP de saudação do contêiner Olá na rede interna de NAT hello (geralmente 172.x.x.x).</span><span class="sxs-lookup"><span data-stu-id="9e12b-151">Edge opens your application's defined launch page using hello IP address of hello container on hello internal NAT network (typically 172.x.x.x).</span></span> <span data-ttu-id="9e12b-152">toolearn mais sobre a depuração de aplicativos em contêineres com o Visual Studio de 2017, consulte [neste artigo][link-debug-container].</span><span class="sxs-lookup"><span data-stu-id="9e12b-152">toolearn more about debugging applications in containers using Visual Studio 2017, see [this article][link-debug-container].</span></span>

![exemplo de fabrikam em um contêiner][image-web-preview]

<span data-ttu-id="9e12b-154">contêiner de saudação agora está pronto toobe criados e empacotados em um aplicativo de malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="9e12b-154">hello container is now ready toobe built and packaged in a Service Fabric application.</span></span> <span data-ttu-id="9e12b-155">Uma vez que a imagem de contêiner Olá criada no seu computador, você pode por push do registro de contêiner tooany e levante-o para baixo tooany toorun de host.</span><span class="sxs-lookup"><span data-stu-id="9e12b-155">Once you have hello container image built on your machine, you can push it tooany container registry and pull it down tooany host toorun.</span></span>

## <a name="get-hello-application-ready-for-hello-cloud"></a><span data-ttu-id="9e12b-156">Preparar o aplicativo hello para nuvem Olá</span><span class="sxs-lookup"><span data-stu-id="9e12b-156">Get hello application ready for hello cloud</span></span>

<span data-ttu-id="9e12b-157">aplicativo de hello tooget pronto para execução na malha do serviço no Azure, é preciso toocomplete duas etapas:</span><span class="sxs-lookup"><span data-stu-id="9e12b-157">tooget hello application ready for running in Service Fabric in Azure, we need toocomplete two steps:</span></span>

1. <span data-ttu-id="9e12b-158">Expor porta Olá onde desejamos tooreach capaz de toobe nosso aplicativo web no cluster do Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="9e12b-158">Expose hello port where we want toobe able tooreach our web application in hello Service Fabric cluster.</span></span>
2. <span data-ttu-id="9e12b-159">Fornecer um banco de dados SQL pronto para produção para nosso aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9e12b-159">Provide a production ready SQL database for our application.</span></span>

### <a name="expose-hello-port-for-hello-app"></a><span data-ttu-id="9e12b-160">Expor porta Olá para o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="9e12b-160">Expose hello port for hello app</span></span>
<span data-ttu-id="9e12b-161">cluster do Service Fabric Olá configuramos, tem porta *80* aberta por padrão no hello balanceador de carga do Azure, que equilibra a entrada cluster toohello de tráfego.</span><span class="sxs-lookup"><span data-stu-id="9e12b-161">hello Service Fabric cluster we have configured, has port *80* open by default in hello Azure Load Balancer, that balances incoming traffic toohello cluster.</span></span> <span data-ttu-id="9e12b-162">É possível expor o contêiner nessa porta por meio do arquivo docker-compose.yml.</span><span class="sxs-lookup"><span data-stu-id="9e12b-162">We can expose our container on this port via our docker-compose.yml file.</span></span>

<span data-ttu-id="9e12b-163">No Visual Studio, abra **Gerenciador de soluções**, localizar **compor docker**e o arquivo aberto Olá **compose.override.yml docker**.</span><span class="sxs-lookup"><span data-stu-id="9e12b-163">In Visual Studio, open **Solution Explorer**, find **docker-compose**, and open hello file **docker-compose.override.yml**.</span></span>

<span data-ttu-id="9e12b-164">Modificar Olá `fabrikamfiber.web:` nó, adicionar um nó filho denominado `ports:`.</span><span class="sxs-lookup"><span data-stu-id="9e12b-164">Modify hello `fabrikamfiber.web:` node, add a child node named `ports:`.</span></span>

<span data-ttu-id="9e12b-165">Adicione uma entrada de cadeia de caracteres `- "80:80"`.</span><span class="sxs-lookup"><span data-stu-id="9e12b-165">Add a string entry `- "80:80"`.</span></span>

```yml
  version: '3'

  services:
    fabrikamfiber.web:
      image: fabrikamfiber.web
      build:
        context: .\FabrikamFiber.Web
        dockerfile: Dockerfile
      ports:
        - "80:80"
```

### <a name="use-a-production-sql-database"></a><span data-ttu-id="9e12b-166">Usar um banco de dados SQL de produção</span><span class="sxs-lookup"><span data-stu-id="9e12b-166">Use a production SQL database</span></span>
<span data-ttu-id="9e12b-167">Ao executar em produção, precisamos que os dados sejam persistidos em nosso banco de dados.</span><span class="sxs-lookup"><span data-stu-id="9e12b-167">When running in production, we need our data persisted in our database.</span></span> <span data-ttu-id="9e12b-168">Atualmente há nenhum dado persistente de tooguarantee de maneira em um contêiner, portanto você não pode armazenar dados de produção no SQL Server em um contêiner.</span><span class="sxs-lookup"><span data-stu-id="9e12b-168">There is currently no way tooguarantee persistent data in a container, therefore you cannot store production data in SQL Server in a container.</span></span>

<span data-ttu-id="9e12b-169">Recomendamos o uso de um Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="9e12b-169">We recommend you utilize an Azure SQL Database.</span></span> <span data-ttu-id="9e12b-170">tooset backup e executar um servidor gerenciado do SQL no Azure, visite Olá [início rápido de banco de dados do SQL Azure] [ link-azure-sql] artigo.</span><span class="sxs-lookup"><span data-stu-id="9e12b-170">tooset up and run a managed SQL Server in Azure, visit hello [Azure SQL Database Quickstarts][link-azure-sql] article.</span></span>

>[!NOTE]
><span data-ttu-id="9e12b-171">Lembre-se de toochange Olá conexão cadeias de caracteres toohello do SQL server no hello **web.release.config** arquivo hello **FabrikamFiber.Web** projeto.</span><span class="sxs-lookup"><span data-stu-id="9e12b-171">Remember toochange hello connection strings toohello SQL server in hello **web.release.config** file in hello **FabrikamFiber.Web** project.</span></span>
>
><span data-ttu-id="9e12b-172">Esse aplicativo falha normalmente se nenhum banco de dados SQL está acessível.</span><span class="sxs-lookup"><span data-stu-id="9e12b-172">This application fails gracefully if no SQL database is reachable.</span></span> <span data-ttu-id="9e12b-173">Você pode escolher toogo em frente e implantar o aplicativo hello com nenhum SQL server.</span><span class="sxs-lookup"><span data-stu-id="9e12b-173">You can choose toogo ahead and deploy hello application with no SQL server.</span></span>

## <a name="deploy-with-visual-studio-team-services"></a><span data-ttu-id="9e12b-174">Implantar com o Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="9e12b-174">Deploy with Visual Studio Team Services</span></span>

<span data-ttu-id="9e12b-175">tooset a implantação usando o Visual Studio Team Services, você precisa Olá tooinstall [extensão de ferramentas de entrega contínua para Visual Studio de 2017][link-visualstudio-cd-extension].</span><span class="sxs-lookup"><span data-stu-id="9e12b-175">tooset up deployment using Visual Studio Team Services, you need tooinstall hello [Continuous Delivery Tools extension for Visual Studio 2017][link-visualstudio-cd-extension].</span></span> <span data-ttu-id="9e12b-176">Essa extensão torna fácil toodeploy tooAzure por meio da configuração do Visual Studio Team Services e obter o cluster do aplicativo implantado tooyour Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9e12b-176">This extension makes it easy toodeploy tooAzure by configuring Visual Studio Team Services and get your app deployed tooyour Service Fabric cluster.</span></span>

<span data-ttu-id="9e12b-177">tooget iniciado, seu código deve ser hospedado no controle de origem.</span><span class="sxs-lookup"><span data-stu-id="9e12b-177">tooget started, your code must be hosted in source control.</span></span> <span data-ttu-id="9e12b-178">assume restante desta seção Olá **git** está sendo usado.</span><span class="sxs-lookup"><span data-stu-id="9e12b-178">hello rest of this section assumes **git** is being used.</span></span>

### <a name="set-up-a-vsts-repo"></a><span data-ttu-id="9e12b-179">Configurar um repositório do VSTS</span><span class="sxs-lookup"><span data-stu-id="9e12b-179">Set up a VSTS repo</span></span>
<span data-ttu-id="9e12b-180">No canto inferior direito de saudação do Visual Studio, clique em **adicionar tooSource controle** > **Git** (ou qualquer opção que você preferir).</span><span class="sxs-lookup"><span data-stu-id="9e12b-180">At hello bottom-right corner of Visual Studio, click **Add tooSource Control** > **Git** (or whichever option you prefer).</span></span>

![Pressione o botão de controle do código-fonte Olá][image-source-control]

<span data-ttu-id="9e12b-182">Em Olá _Team Explorer_ painel, pressione **publicar o repositório do Git**.</span><span class="sxs-lookup"><span data-stu-id="9e12b-182">In hello _Team Explorer_ pane, press **Publish Git Repo**.</span></span>

<span data-ttu-id="9e12b-183">Selecione o nome do repositório VSTS e pressione **Repositório**.</span><span class="sxs-lookup"><span data-stu-id="9e12b-183">Select your VSTS repository name and press **Repository**.</span></span>

![publicar o repositório tooVSTS][image-publish-repo]

<span data-ttu-id="9e12b-185">Agora que seu código está sincronizado com um repositório de origem do VSTS, você pode configurar a integração e a entrega contínuas.</span><span class="sxs-lookup"><span data-stu-id="9e12b-185">Now that your code is synchronized with a VSTS source repository, you can configure continuous integration and continuous delivery.</span></span>

### <a name="setup-continuous-delivery"></a><span data-ttu-id="9e12b-186">Configurar a entrega contínua</span><span class="sxs-lookup"><span data-stu-id="9e12b-186">Setup continuous delivery</span></span>

<span data-ttu-id="9e12b-187">Em _Solution Explorer_, Olá do botão direito do mouse **solução** > **configurar fornecimento contínuo**.</span><span class="sxs-lookup"><span data-stu-id="9e12b-187">In _Solution Explorer_, right-click hello **solution** > **Configure Continuous Delivery**.</span></span>

<span data-ttu-id="9e12b-188">Selecione Olá assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="9e12b-188">Select hello Azure Subscription.</span></span>

<span data-ttu-id="9e12b-189">Definir **tipo de Host** muito**Cluster do Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="9e12b-189">Set **Host Type** too**Service Fabric Cluster**.</span></span>

<span data-ttu-id="9e12b-190">Definir **Host de destino** toohello cluster do service fabric você criou na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="9e12b-190">Set **Target Host** toohello service fabric cluster you created in hello previous section.</span></span>

<span data-ttu-id="9e12b-191">Escolha um **registro de contêiner** toopublish seu recipiente.</span><span class="sxs-lookup"><span data-stu-id="9e12b-191">Choose a **Container Registry** toopublish your container to.</span></span>

>[!TIP]
><span data-ttu-id="9e12b-192">Saudação de uso **editar** botão toocreate um registro de contêiner.</span><span class="sxs-lookup"><span data-stu-id="9e12b-192">Use hello **Edit** button toocreate a container registry.</span></span>

<span data-ttu-id="9e12b-193">Pressione **OK**.</span><span class="sxs-lookup"><span data-stu-id="9e12b-193">Press **OK**.</span></span>

![configurar a integração contínua do service fabric][image-setup-ci]
   
   <span data-ttu-id="9e12b-195">Concluída a configuração Olá, o contêiner é implantado tooService malha.</span><span class="sxs-lookup"><span data-stu-id="9e12b-195">Once hello configuration is completed, your container is deployed tooService Fabric.</span></span> <span data-ttu-id="9e12b-196">Sempre que você enviar por push o repositório de toohello atualizações uma nova compilação e a versão é executado.</span><span class="sxs-lookup"><span data-stu-id="9e12b-196">Whenever you push updates toohello repository a new build and release is executed.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="9e12b-197">Imagens de contêiner de saudação de construção levar aproximadamente 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="9e12b-197">Building hello container images take approximately 15 minutes.</span></span>
   ><span data-ttu-id="9e12b-198">Olá primeiro implantação toohello Service Fabric cluster faz com que Olá base Windows Server Core contêiner imagens toobe baixado.</span><span class="sxs-lookup"><span data-stu-id="9e12b-198">hello first deployment toohello Service Fabric cluster causes hello base Windows Server Core container images toobe downloaded.</span></span> <span data-ttu-id="9e12b-199">download de saudação leva toocomplete mais de 5 a 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="9e12b-199">hello download takes additional 5-10 minutes toocomplete.</span></span>

<span data-ttu-id="9e12b-200">Navegar no aplicativo de Call Center de Fabrikam toohello usando a url de saudação do cluster: por exemplo, *http://mycluster.westeurope.cloudapp.azure.com*</span><span class="sxs-lookup"><span data-stu-id="9e12b-200">Browse toohello Fabrikam Call Center application using hello url of your cluster: for example, *http://mycluster.westeurope.cloudapp.azure.com*</span></span>

<span data-ttu-id="9e12b-201">Agora que você tem em contêineres e implantado Olá Fabrikam Call Center solução, você pode abrir Olá [portal do Azure] [ link-azure-portal] e ver o aplicativo hello em execução no serviço de malha.</span><span class="sxs-lookup"><span data-stu-id="9e12b-201">Now that you have containerized and deployed hello Fabrikam Call Center solution, you can open hello [Azure portal][link-azure-portal] and see hello application running in Service Fabric.</span></span> <span data-ttu-id="9e12b-202">aplicativo de hello tootry, abra um navegador da web e vá toohello URL do cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9e12b-202">tootry hello application, open a web browser and go toohello URL of your Service Fabric cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e12b-203">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9e12b-203">Next steps</span></span>

<span data-ttu-id="9e12b-204">Neste tutorial, você aprendeu a:</span><span class="sxs-lookup"><span data-stu-id="9e12b-204">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9e12b-205">Criar um projeto do Docker no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9e12b-205">Create a Docker project in Visual Studio</span></span>
> * <span data-ttu-id="9e12b-206">Colocar um aplicativo existente em um contêiner</span><span class="sxs-lookup"><span data-stu-id="9e12b-206">Containerize an existing application</span></span>
> * <span data-ttu-id="9e12b-207">Configurar a integração contínua com o Visual Studio e o VSTS</span><span class="sxs-lookup"><span data-stu-id="9e12b-207">Setup continuous integration with Visual Studio and VSTS</span></span>

<!--   NOTE SURE WHAT WE SHOULD DO YET HERE

Advance toohello next tutorial toolearn how toobind a custom SSL certificate tooit.

> [!div class="nextstepaction"]
> [Bind an existing custom SSL certificate tooAzure Web Apps](app-service-web-tutorial-custom-ssl.md)

## Next steps

- [Container Tooling in Visual Studio][link-visualstudio-container-tools]
- [Get started with containers in Service Fabric][link-servicefabric-containers]
- [Creating Service Fabric applications][link-servicefabric-createapp]
-->

[link-debug-container]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-fabrikam-github]: https://aka.ms/fabrikamcontainer
[link-container-quickstart]: /virtualization/windowscontainers/quick-start/quick-start-windows-10
[link-visualstudio-container-tools]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-azure-powershell-install]: /powershell/azure/install-azurerm-ps
[link-servicefabric-create-secure-clusters]: service-fabric-cluster-creation-via-arm.md
[link-visualstudio-cd-extension]: https://aka.ms/cd4vs
[link-servicefabric-containers]: service-fabric-get-started-containers.md
[link-servicefabric-createapp]: service-fabric-create-your-first-application-in-visual-studio.md
[link-azure-portal]: https://portal.azure.com
[link-sf-clustertemplate]: https://aka.ms/securepreviewonelineclustertemplate
[link-azure-pricing-calculator]: https://azure.microsoft.com/en-us/pricing/calculator/
[link-azure-subscription]: https://azure.microsoft.com/en-us/free/
[link-vsts-account]: https://www.visualstudio.com/team-services/pricing/
[link-azure-sql]: /azure/sql-database/

[image-web-preview]: media/service-fabric-host-app-in-a-container/fabrikam-web-sample.png
[image-source-control]: media/service-fabric-host-app-in-a-container/add-to-source-control.png
[image-publish-repo]: media/service-fabric-host-app-in-a-container/publish-repo.png
[image-setup-ci]: media/service-fabric-host-app-in-a-container/configure-continuous-integration.png
