---
title: "Guia de Introdução ao aaaNode.js | Microsoft Docs"
description: "Saiba como toocreate Node.js um simples aplicativo web e implantá-lo tooan serviço de nuvem do Azure."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 50951a87-fed4-48e0-bcfa-453b9e50452e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 22945bfcc1b0e5da2a2d37dc5cc86be013cc0b5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-a-nodejs-application-tooan-azure-cloud-service"></a><span data-ttu-id="c6d48-103">Criar e implantar um aplicativo de Node. js tooan serviço de nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="c6d48-103">Build and deploy a Node.js application tooan Azure Cloud Service</span></span>

<span data-ttu-id="c6d48-104">Este tutorial mostra como toocreate Node.js um simples aplicativo em execução em um serviço de nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6d48-104">This tutorial shows how toocreate a simple Node.js application running in an Azure Cloud Service.</span></span> <span data-ttu-id="c6d48-105">Serviços de nuvem são blocos de construção de saudação de aplicativos de nuvem escalonáveis no Azure.</span><span class="sxs-lookup"><span data-stu-id="c6d48-105">Cloud Services are hello building blocks of scalable cloud applications in Azure.</span></span> <span data-ttu-id="c6d48-106">Eles permitem a separação de saudação e gerenciamento independente e expansão dos componentes front-end e back-end do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c6d48-106">They allow hello separation and independent management and scale-out of front-end and back-end components of your application.</span></span>  <span data-ttu-id="c6d48-107">Os serviços de nuvem fornecem uma máquina virtual exclusiva robusta para hospedar cada função confiável.</span><span class="sxs-lookup"><span data-stu-id="c6d48-107">Cloud Services provide a robust dedicated virtual machine for hosting each role reliably.</span></span>

<span data-ttu-id="c6d48-108">Para obter mais informações sobre serviços de nuvem e como eles se comparam tooAzure sites e máquinas virtuais, consulte [comparação de sites do Azure, serviços de nuvem e máquinas virtuais].</span><span class="sxs-lookup"><span data-stu-id="c6d48-108">For more information on Cloud Services, and how they compare tooAzure Websites and Virtual machines, see [Azure Websites, Cloud Services and Virtual Machines comparison].</span></span>

> [!TIP]
> <span data-ttu-id="c6d48-109">Procurando toobuild um site simples?</span><span class="sxs-lookup"><span data-stu-id="c6d48-109">Looking toobuild a simple website?</span></span> <span data-ttu-id="c6d48-110">Se o seu cenário envolve apenas um site de front-end simples, considere [usar um aplicativo Web leve].</span><span class="sxs-lookup"><span data-stu-id="c6d48-110">If your scenario involves just a simple website front-end, consider [using a lightweight web app].</span></span> <span data-ttu-id="c6d48-111">É possível atualizar facilmente tooa serviço de nuvem que seu aplicativo web cresce e suas necessidades mudam.</span><span class="sxs-lookup"><span data-stu-id="c6d48-111">You can easily upgrade tooa Cloud Service as your web app grows and your requirements change.</span></span>

<span data-ttu-id="c6d48-112">Seguindo este tutorial, você irá criar um aplicativo da Web simples hospedado dentro de uma função Web.</span><span class="sxs-lookup"><span data-stu-id="c6d48-112">By following this tutorial, you will build a simple web application hosted inside a web role.</span></span> <span data-ttu-id="c6d48-113">Você usará tootest de emulador de computação Olá seu aplicativo localmente e implantá-lo usando ferramentas de linha de comando do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c6d48-113">You will use hello compute emulator tootest your application locally, then deploy it using PowerShell command-line tools.</span></span>

<span data-ttu-id="c6d48-114">aplicativo Hello é um aplicativo simples "hello world":</span><span class="sxs-lookup"><span data-stu-id="c6d48-114">hello application is a simple "hello world" application:</span></span>

![Um navegador da web exibindo a página de web do Olá Olá, mundo][A web browser displaying hello Hello World web page]

## <a name="prerequisites"></a><span data-ttu-id="c6d48-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c6d48-116">Prerequisites</span></span>
> [!NOTE]
> <span data-ttu-id="c6d48-117">Este tutorial usa o PowerShell do Azure, que requer o Windows.</span><span class="sxs-lookup"><span data-stu-id="c6d48-117">This tutorial uses Azure PowerShell, which requires Windows.</span></span>

* <span data-ttu-id="c6d48-118">Instalar e configurar o [Powershell do Azure].</span><span class="sxs-lookup"><span data-stu-id="c6d48-118">Install and configure [Azure Powershell].</span></span>
* <span data-ttu-id="c6d48-119">Baixe e instale Olá [SDK do Azure para .NET 2.7].</span><span class="sxs-lookup"><span data-stu-id="c6d48-119">Download and install hello [Azure SDK for .NET 2.7].</span></span> <span data-ttu-id="c6d48-120">Olá instalar o programa de instalação, selecione:</span><span class="sxs-lookup"><span data-stu-id="c6d48-120">In hello install setup, select:</span></span>
  * <span data-ttu-id="c6d48-121">MicrosoftAzureAuthoringTools</span><span class="sxs-lookup"><span data-stu-id="c6d48-121">MicrosoftAzureAuthoringTools</span></span>
  * <span data-ttu-id="c6d48-122">MicrosoftAzureComputeEmulator</span><span class="sxs-lookup"><span data-stu-id="c6d48-122">MicrosoftAzureComputeEmulator</span></span>

## <a name="create-an-azure-cloud-service-project"></a><span data-ttu-id="c6d48-123">Criar um projeto de Serviço de Nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="c6d48-123">Create an Azure Cloud Service project</span></span>
<span data-ttu-id="c6d48-124">Execute Olá tarefas toocreate um novo projeto de serviço de nuvem do Azure, juntamente com a estrutura básica do Node. js a seguir:</span><span class="sxs-lookup"><span data-stu-id="c6d48-124">Perform hello following tasks toocreate a new Azure Cloud Service project, along with basic Node.js scaffolding:</span></span>

1. <span data-ttu-id="c6d48-125">Executar **do Windows PowerShell** como administrador; da saudação **Menu Iniciar** ou **tela inicial**, procure **do Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="c6d48-125">Run **Windows PowerShell** as Administrator; from hello **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span>
2. <span data-ttu-id="c6d48-126">[Conectar o PowerShell] tooyour assinatura.</span><span class="sxs-lookup"><span data-stu-id="c6d48-126">[Connect PowerShell] tooyour subscription.</span></span>
3. <span data-ttu-id="c6d48-127">Digite hello projeto saudação do PowerShell cmdlet toocreate toocreate a seguir:</span><span class="sxs-lookup"><span data-stu-id="c6d48-127">Enter hello following PowerShell cmdlet toocreate toocreate hello project:</span></span>

        New-AzureServiceProject helloworld

    ![resultado de saudação do comando de helloworld Olá New-AzureService][hello result of hello New-AzureService helloworld command]

    <span data-ttu-id="c6d48-129">Olá **AzureServiceProject novo** cmdlet gera uma estrutura básica para publicar um aplicativo de Node. js tooa serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="c6d48-129">hello **New-AzureServiceProject** cmdlet generates a basic structure for publishing a Node.js application tooa Cloud Service.</span></span> <span data-ttu-id="c6d48-130">Ele contém arquivos de configuração necessários para a publicação tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c6d48-130">It contains configuration files necessary for publishing tooAzure.</span></span> <span data-ttu-id="c6d48-131">Olá cmdlet também altera o diretório de serviço Olá toohello de diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="c6d48-131">hello cmdlet also changes your working directory toohello directory for hello service.</span></span>

    <span data-ttu-id="c6d48-132">Olá cria Olá seguintes arquivos:</span><span class="sxs-lookup"><span data-stu-id="c6d48-132">hello cmdlet creates hello following files:</span></span>

   * <span data-ttu-id="c6d48-133">**ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** e **ServiceDefinition.csdef**: são arquivos específicos do Azure necessários para publicar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c6d48-133">**ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** and **ServiceDefinition.csdef**: Azure-specific files necessary for publishing your application.</span></span> <span data-ttu-id="c6d48-134">Para saber mais, consulte [Visão geral da criação de um serviço hospedado para o Azure].</span><span class="sxs-lookup"><span data-stu-id="c6d48-134">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
   * <span data-ttu-id="c6d48-135">**Deploymentsettings**: armazena as configurações locais que são usadas por Olá cmdlets de implantação do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c6d48-135">**deploymentSettings.json**: Stores local settings that are used by hello Azure PowerShell deployment cmdlets.</span></span>
4. <span data-ttu-id="c6d48-136">Digite hello comando tooadd uma nova função web a seguir:</span><span class="sxs-lookup"><span data-stu-id="c6d48-136">Enter hello following command tooadd a new web role:</span></span>

       Add-AzureNodeWebRole

   ![saída de saudação do hello comando Add-AzureNodeWebRole][hello output of hello Add-AzureNodeWebRole command]

   <span data-ttu-id="c6d48-138">Olá **Add-AzureNodeWebRole** cmdlet cria um aplicativo básico do Node. js.</span><span class="sxs-lookup"><span data-stu-id="c6d48-138">hello **Add-AzureNodeWebRole** cmdlet creates a basic Node.js application.</span></span> <span data-ttu-id="c6d48-139">Ele também modifica Olá **. csfg** e **. csdef** arquivos tooadd entradas de configuração para a nova função de saudação.</span><span class="sxs-lookup"><span data-stu-id="c6d48-139">It also modifies hello **.csfg** and **.csdef** files tooadd configuration entries for hello new role.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c6d48-140">Se você não especificar um nome de função, um nome padrão será usado.</span><span class="sxs-lookup"><span data-stu-id="c6d48-140">If you do not specify a role name, a default name is used.</span></span> <span data-ttu-id="c6d48-141">Você pode fornecer um nome como primeiro parâmetro de cmdlet hello:`Add-AzureNodeWebRole MyRole`</span><span class="sxs-lookup"><span data-stu-id="c6d48-141">You can provide a name as hello first cmdlet parameter: `Add-AzureNodeWebRole MyRole`</span></span>

<span data-ttu-id="c6d48-142">Olá Node. js aplicativo é definido no arquivo hello **server.js**, localizado no diretório Olá para função de web hello (**WebRole1** por padrão).</span><span class="sxs-lookup"><span data-stu-id="c6d48-142">hello Node.js app is defined in hello file **server.js**, located in hello directory for hello web role (**WebRole1** by default).</span></span> <span data-ttu-id="c6d48-143">Aqui está o código de saudação:</span><span class="sxs-lookup"><span data-stu-id="c6d48-143">Here is hello code:</span></span>

    var http = require('http');
    var port = process.env.port || 1337;
    http.createServer(function (req, res) {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('Hello World\n');
    }).listen(port);

<span data-ttu-id="c6d48-144">Esse código é essencialmente Olá mesmo hello "Hello World" de exemplo no hello [nodejs.org] site, exceto que ele usa o número da porta Olá atribuído pelo ambiente de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="c6d48-144">This code is essentially hello same as hello "Hello World" sample on hello [nodejs.org] website, except it uses hello port number assigned by hello cloud environment.</span></span>

## <a name="deploy-hello-application-tooazure"></a><span data-ttu-id="c6d48-145">Implantar Olá aplicativo tooAzure</span><span class="sxs-lookup"><span data-stu-id="c6d48-145">Deploy hello application tooAzure</span></span>

> [!NOTE]
> <span data-ttu-id="c6d48-146">toocomplete neste tutorial, você precisa de uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6d48-146">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="c6d48-147">Você pode [ativar os benefícios de assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) ou [se inscrever para fazer uma conta gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).</span><span class="sxs-lookup"><span data-stu-id="c6d48-147">You can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) or [sign up for a free account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).</span></span>

### <a name="download-hello-azure-publishing-settings"></a><span data-ttu-id="c6d48-148">Baixar hello Azure configurações de publicação</span><span class="sxs-lookup"><span data-stu-id="c6d48-148">Download hello Azure publishing settings</span></span>
<span data-ttu-id="c6d48-149">toodeploy tooAzure seu aplicativo, você deve primeiro baixar Olá publicar configurações para sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6d48-149">toodeploy your application tooAzure, you must first download hello publishing settings for your Azure subscription.</span></span>

1. <span data-ttu-id="c6d48-150">Execute hello Azure PowerShell cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="c6d48-150">Run hello following Azure PowerShell cmdlet:</span></span>

       Get-AzurePublishSettingsFile

   <span data-ttu-id="c6d48-151">Isso usará seu navegador toonavigate toohello página de download de configurações de publicação.</span><span class="sxs-lookup"><span data-stu-id="c6d48-151">This will use your browser toonavigate toohello publish settings download page.</span></span> <span data-ttu-id="c6d48-152">Você pode ser solicitado toolog com um Account da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c6d48-152">You may be prompted toolog in with a Microsoft Account.</span></span> <span data-ttu-id="c6d48-153">Nesse caso, use conta Olá associada à sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6d48-153">If so, use hello account associated with your Azure subscription.</span></span>

   <span data-ttu-id="c6d48-154">Salve o local do arquivo hello baixado perfil tooa você pode acessar facilmente.</span><span class="sxs-lookup"><span data-stu-id="c6d48-154">Save hello downloaded profile tooa file location you can easily access.</span></span>
2. <span data-ttu-id="c6d48-155">Execute o seguinte cmdlet tooimport Olá baixado do perfil de publicação:</span><span class="sxs-lookup"><span data-stu-id="c6d48-155">Run following cmdlet tooimport hello publishing profile you downloaded:</span></span>

       Import-AzurePublishSettingsFile [path toofile]

    > [!NOTE]
    > <span data-ttu-id="c6d48-156">Depois de importar Olá configurações de publicação, considere excluir Olá baixou o arquivo. publishsettings, porque ele contém informações que podem permitir que alguém tooaccess sua conta.</span><span class="sxs-lookup"><span data-stu-id="c6d48-156">After importing hello publish settings, consider deleting hello downloaded .publishSettings file, because it contains information that could allow someone tooaccess your account.</span></span>

### <a name="publish-hello-application"></a><span data-ttu-id="c6d48-157">Publicar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="c6d48-157">Publish hello application</span></span>
<span data-ttu-id="c6d48-158">toopublish, execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="c6d48-158">toopublish, run hello following commands:</span></span>

      $ServiceName = "NodeHelloWorld" + $(Get-Date -Format ('ddhhmm'))
    Publish-AzureServiceProject -ServiceName $ServiceName  -Location "East US" -Launch

* <span data-ttu-id="c6d48-159">**-ServiceName** especifica nome Olá para implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="c6d48-159">**-ServiceName** specifies hello name for hello deployment.</span></span> <span data-ttu-id="c6d48-160">Isso deve ser um nome exclusivo, caso contrário, o processo de publicação Olá falhará.</span><span class="sxs-lookup"><span data-stu-id="c6d48-160">This must be a unique name, otherwise hello publish process will fail.</span></span> <span data-ttu-id="c6d48-161">Olá **Get-Date** comando move em uma cadeia de caracteres de data/hora deve tornar o nome de saudação exclusivo.</span><span class="sxs-lookup"><span data-stu-id="c6d48-161">hello **Get-Date** command tacks on a date/time string that should make hello name unique.</span></span>
* <span data-ttu-id="c6d48-162">**-Local** Especifica Olá datacenter que será hospedado no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="c6d48-162">**-Location** specifies hello datacenter that hello application will be hosted in.</span></span> <span data-ttu-id="c6d48-163">toosee uma lista de centros de dados disponíveis, use Olá **AzureLocation Get** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c6d48-163">toosee a list of available datacenters, use hello **Get-AzureLocation** cmdlet.</span></span>
* <span data-ttu-id="c6d48-164">**-Inicie** abre uma janela do navegador e navega toohello hospedado serviço após a implantação.</span><span class="sxs-lookup"><span data-stu-id="c6d48-164">**-Launch** opens a browser window and navigates toohello hosted service after deployment has completed.</span></span>

<span data-ttu-id="c6d48-165">Após a publicação será bem-sucedida, você verá uma resposta semelhante toohello a seguir:</span><span class="sxs-lookup"><span data-stu-id="c6d48-165">After publishing succeeds, you will see a response similar toohello following:</span></span>

![saída de saudação do hello comando Publish-AzureService][hello output of hello Publish-AzureService command]

> [!NOTE]
> <span data-ttu-id="c6d48-167">Ele pode levar vários minutos para toodeploy de aplicativo hello e ficam disponível quando publicado pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="c6d48-167">It can take several minutes for hello application toodeploy and become available when first published.</span></span>

<span data-ttu-id="c6d48-168">Depois de saudação implantação for concluída, uma janela do navegador será aberto e navegue toohello serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="c6d48-168">Once hello deployment has completed, a browser window will open and navigate toohello cloud service.</span></span>

![Uma janela do navegador exibindo Olá Olá mundo página; Olá URL indica a página Olá é hospedada no Azure.][A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]

<span data-ttu-id="c6d48-170">Seu aplicativo está em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="c6d48-170">Your application is now running on Azure.</span></span>

<span data-ttu-id="c6d48-171">Olá **AzureServiceProject publicar** cmdlet executa Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c6d48-171">hello **Publish-AzureServiceProject** cmdlet performs hello following steps:</span></span>

1. <span data-ttu-id="c6d48-172">Cria um pacote toodeploy.</span><span class="sxs-lookup"><span data-stu-id="c6d48-172">Creates a package toodeploy.</span></span> <span data-ttu-id="c6d48-173">pacote de saudação contém todos os arquivos de saudação na pasta de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c6d48-173">hello package contains all hello files in your application folder.</span></span>
2. <span data-ttu-id="c6d48-174">Cria uma nova **conta de armazenamento** se não existir.</span><span class="sxs-lookup"><span data-stu-id="c6d48-174">Creates a new **storage account** if one does not exist.</span></span> <span data-ttu-id="c6d48-175">Olá conta de armazenamento do Azure é o pacote de aplicativo hello toostore usado durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="c6d48-175">hello Azure storage account is used toostore hello application package during deployment.</span></span> <span data-ttu-id="c6d48-176">Você pode excluir com segurança conta de armazenamento Olá após a conclusão da implantação.</span><span class="sxs-lookup"><span data-stu-id="c6d48-176">You can safely delete hello storage account after deployment is done.</span></span>
3. <span data-ttu-id="c6d48-177">Cria um novo **serviço de nuvem** se não existir.</span><span class="sxs-lookup"><span data-stu-id="c6d48-177">Creates a new **cloud service** if one does not already exist.</span></span> <span data-ttu-id="c6d48-178">Um **serviço de nuvem** é Olá contêiner no qual o aplicativo está hospedado quando ele é implantado tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c6d48-178">A **cloud service** is hello container in which your application is hosted when it is deployed tooAzure.</span></span> <span data-ttu-id="c6d48-179">Para saber mais, consulte [Visão geral da criação de um serviço hospedado para o Azure].</span><span class="sxs-lookup"><span data-stu-id="c6d48-179">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
4. <span data-ttu-id="c6d48-180">Publica Olá tooAzure de pacote de implantação.</span><span class="sxs-lookup"><span data-stu-id="c6d48-180">Publishes hello deployment package tooAzure.</span></span>

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="c6d48-181">Parando e excluindo seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="c6d48-181">Stopping and deleting your application</span></span>
<span data-ttu-id="c6d48-182">Depois de implantar seu aplicativo, convém toodisable isso, você pode evitar custos extras.</span><span class="sxs-lookup"><span data-stu-id="c6d48-182">After deploying your application, you may want toodisable it so you can avoid extra costs.</span></span> <span data-ttu-id="c6d48-183">O Azure cobra as instâncias de função web por hora de acordo com o tempo consumido do servidor.</span><span class="sxs-lookup"><span data-stu-id="c6d48-183">Azure bills web role instances per hour of server time consumed.</span></span> <span data-ttu-id="c6d48-184">Hora do servidor é consumida quando seu aplicativo é implantado, mesmo se as instâncias de saudação não estão em execução e estão em estado de parado de saudação.</span><span class="sxs-lookup"><span data-stu-id="c6d48-184">Server time is consumed once your application is deployed, even if hello instances are not running and are in hello stopped state.</span></span>

1. <span data-ttu-id="c6d48-185">Na janela do Windows PowerShell hello, interrompa a implantação do serviço Olá criada na seção anterior Olá com hello cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="c6d48-185">In hello Windows PowerShell window, stop hello service deployment created in hello previous section with hello following cmdlet:</span></span>

       Stop-AzureService

   <span data-ttu-id="c6d48-186">Parar serviço Olá pode levar vários minutos.</span><span class="sxs-lookup"><span data-stu-id="c6d48-186">Stopping hello service may take several minutes.</span></span> <span data-ttu-id="c6d48-187">Quando a saudação serviço for interrompido, você recebe uma mensagem indicando que ele foi interrompido.</span><span class="sxs-lookup"><span data-stu-id="c6d48-187">When hello service is stopped, you receive a message indicating that it has stopped.</span></span>

   ![status de saudação do comando Olá Stop-AzureService][hello status of hello Stop-AzureService command]
2. <span data-ttu-id="c6d48-189">serviço de saudação toodelete, chamada hello cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="c6d48-189">toodelete hello service, call hello following cmdlet:</span></span>

       Remove-AzureService

   <span data-ttu-id="c6d48-190">Quando solicitado, insira **Y** toodelete serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="c6d48-190">When prompted, enter **Y** toodelete hello service.</span></span>

   <span data-ttu-id="c6d48-191">Excluindo serviço Olá pode levar vários minutos.</span><span class="sxs-lookup"><span data-stu-id="c6d48-191">Deleting hello service may take several minutes.</span></span> <span data-ttu-id="c6d48-192">Após a exclusão de serviço Olá você receberá uma mensagem indicando que o serviço de saudação foi excluído.</span><span class="sxs-lookup"><span data-stu-id="c6d48-192">After hello service has been deleted you receive a message indicating that hello service was deleted.</span></span>

   ![status de saudação do comando Olá Remove-AzureService][hello status of hello Remove-AzureService command]

   > [!NOTE]
   > <span data-ttu-id="c6d48-194">Excluindo serviço Olá não excluir conta de armazenamento de saudação que foi criada quando o serviço de saudação foi inicialmente publicado e você continuará toobe cobrado pelo armazenamento usado.</span><span class="sxs-lookup"><span data-stu-id="c6d48-194">Deleting hello service does not delete hello storage account that was created when hello service was initially published, and you will continue toobe billed for storage used.</span></span> <span data-ttu-id="c6d48-195">Se nada mais é usar o armazenamento de saudação, talvez você queira toodelete-lo.</span><span class="sxs-lookup"><span data-stu-id="c6d48-195">If nothing else is using hello storage, you may want toodelete it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6d48-196">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c6d48-196">Next steps</span></span>
<span data-ttu-id="c6d48-197">Para obter mais informações, consulte Olá [Node. js Developer Center].</span><span class="sxs-lookup"><span data-stu-id="c6d48-197">For more information, see hello [Node.js Developer Center].</span></span>

<!-- URL List -->

[comparação de sites do Azure, serviços de nuvem e máquinas virtuais]: ../app-service-web/choose-web-site-cloud-service-vm.md
[usar um aplicativo Web leve]: ../app-service-web/app-service-web-get-started-nodejs.md
[Powershell do Azure]: /powershell/azureps-cmdlets-docs
[SDK do Azure para .NET 2.7]: http://www.microsoft.com/en-us/download/details.aspx?id=48178
[Conectar o PowerShell]: /powershell/azureps-cmdlets-docs#step-3-connect
[nodejs.org]: http://nodejs.org/
[Visão geral da criação de um serviço hospedado para o Azure]: https://azure.microsoft.com/documentation/services/cloud-services/
[Node. js Developer Center]: https://azure.microsoft.com/develop/nodejs/

<!-- IMG List -->

[hello result of hello New-AzureService helloworld command]: ./media/cloud-services-nodejs-develop-deploy-app/node9.png
[hello output of hello Add-AzureNodeWebRole command]: ./media/cloud-services-nodejs-develop-deploy-app/node11.png
[A web browser displaying hello Hello World web page]: ./media/cloud-services-nodejs-develop-deploy-app/node14.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node19.png
[A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]: ./media/cloud-services-nodejs-develop-deploy-app/node21.png
[hello status of hello Stop-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node48.png
[hello status of hello Remove-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node49.png
