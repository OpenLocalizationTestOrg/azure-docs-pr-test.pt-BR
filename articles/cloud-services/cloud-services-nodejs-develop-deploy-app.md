---
title: "Guia de introdução ao Node.js | Microsoft Docs"
description: "Saiba como criar um aplicativo Web simples do Node.js e implantá-lo em um serviço de nuvem do Azure."
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
ms.openlocfilehash: 980643f35c78bbae7b1b12336331ca15ad4fb89b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="build-and-deploy-a-nodejs-application-to-an-azure-cloud-service"></a><span data-ttu-id="ff468-103">Criar e implantar um aplicativo Node.jc para um Serviço de Nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="ff468-103">Build and deploy a Node.js application to an Azure Cloud Service</span></span>

<span data-ttu-id="ff468-104">Este tutorial mostra como criar um aplicativo simples do Node.js em execução em um Serviço de Nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="ff468-104">This tutorial shows how to create a simple Node.js application running in an Azure Cloud Service.</span></span> <span data-ttu-id="ff468-105">Os Serviços de Nuvem são os blocos de construção de aplicativos de nuvem escalonáveis no Azure.</span><span class="sxs-lookup"><span data-stu-id="ff468-105">Cloud Services are the building blocks of scalable cloud applications in Azure.</span></span> <span data-ttu-id="ff468-106">Eles permitem a separação e o gerenciamento independente e o dimensionamento dos componentes de front-end e back-end de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ff468-106">They allow the separation and independent management and scale-out of front-end and back-end components of your application.</span></span>  <span data-ttu-id="ff468-107">Os serviços de nuvem fornecem uma máquina virtual exclusiva robusta para hospedar cada função confiável.</span><span class="sxs-lookup"><span data-stu-id="ff468-107">Cloud Services provide a robust dedicated virtual machine for hosting each role reliably.</span></span>

<span data-ttu-id="ff468-108">Para saber mais sobre serviços de nuvem e como eles são comparados aos Sites do Azure e máquinas virtuais, consulte [Comparação de Sites do Azure, Serviços de Nuvem e Máquinas virtuais].</span><span class="sxs-lookup"><span data-stu-id="ff468-108">For more information on Cloud Services, and how they compare to Azure Websites and Virtual machines, see [Azure Websites, Cloud Services and Virtual Machines comparison].</span></span>

> [!TIP]
> <span data-ttu-id="ff468-109">Procurando desenvolver um site simples?</span><span class="sxs-lookup"><span data-stu-id="ff468-109">Looking to build a simple website?</span></span> <span data-ttu-id="ff468-110">Se o seu cenário envolve apenas um site de front-end simples, considere [usar um aplicativo Web leve].</span><span class="sxs-lookup"><span data-stu-id="ff468-110">If your scenario involves just a simple website front-end, consider [using a lightweight web app].</span></span> <span data-ttu-id="ff468-111">Você pode atualizar facilmente para um serviço de nuvem conforme o aplicativo Web cresce e suas necessidades mudam.</span><span class="sxs-lookup"><span data-stu-id="ff468-111">You can easily upgrade to a Cloud Service as your web app grows and your requirements change.</span></span>

<span data-ttu-id="ff468-112">Seguindo este tutorial, você irá criar um aplicativo da Web simples hospedado dentro de uma função Web.</span><span class="sxs-lookup"><span data-stu-id="ff468-112">By following this tutorial, you will build a simple web application hosted inside a web role.</span></span> <span data-ttu-id="ff468-113">Você usará o emulador de computação para testar o aplicativo localmente e, em seguida, o implantará usando ferramentas de linha de comando do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ff468-113">You will use the compute emulator to test your application locally, then deploy it using PowerShell command-line tools.</span></span>

<span data-ttu-id="ff468-114">O aplicativo é um aplicativo simples "hello world":</span><span class="sxs-lookup"><span data-stu-id="ff468-114">The application is a simple "hello world" application:</span></span>

![Um navegador exibindo a página da Web Hello World][A web browser displaying the Hello World web page]

## <a name="prerequisites"></a><span data-ttu-id="ff468-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ff468-116">Prerequisites</span></span>
> [!NOTE]
> <span data-ttu-id="ff468-117">Este tutorial usa o PowerShell do Azure, que requer o Windows.</span><span class="sxs-lookup"><span data-stu-id="ff468-117">This tutorial uses Azure PowerShell, which requires Windows.</span></span>

* <span data-ttu-id="ff468-118">Instalar e configurar o [Powershell do Azure].</span><span class="sxs-lookup"><span data-stu-id="ff468-118">Install and configure [Azure Powershell].</span></span>
* <span data-ttu-id="ff468-119">Baixe e instale o [SDK do Azure para .NET 2.7].</span><span class="sxs-lookup"><span data-stu-id="ff468-119">Download and install the [Azure SDK for .NET 2.7].</span></span> <span data-ttu-id="ff468-120">Na configuração da instalação, selecione:</span><span class="sxs-lookup"><span data-stu-id="ff468-120">In the install setup, select:</span></span>
  * <span data-ttu-id="ff468-121">MicrosoftAzureAuthoringTools</span><span class="sxs-lookup"><span data-stu-id="ff468-121">MicrosoftAzureAuthoringTools</span></span>
  * <span data-ttu-id="ff468-122">MicrosoftAzureComputeEmulator</span><span class="sxs-lookup"><span data-stu-id="ff468-122">MicrosoftAzureComputeEmulator</span></span>

## <a name="create-an-azure-cloud-service-project"></a><span data-ttu-id="ff468-123">Criar um projeto de Serviço de Nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="ff468-123">Create an Azure Cloud Service project</span></span>
<span data-ttu-id="ff468-124">Execute as tarefas a seguir para criar um novo projeto do Serviço de Nuvem do Azure, juntamente com a estrutura básica do Node.js:</span><span class="sxs-lookup"><span data-stu-id="ff468-124">Perform the following tasks to create a new Azure Cloud Service project, along with basic Node.js scaffolding:</span></span>

1. <span data-ttu-id="ff468-125">Execute o **Windows PowerShell** como administrador. No **Menu Iniciar** ou na tela **Início**, procure o **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="ff468-125">Run **Windows PowerShell** as Administrator; from the **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span>
2. <span data-ttu-id="ff468-126">[Conecte o PowerShell] à sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="ff468-126">[Connect PowerShell] to your subscription.</span></span>
3. <span data-ttu-id="ff468-127">Insira o seguinte cmdlet do PowerShell para criar o projeto:</span><span class="sxs-lookup"><span data-stu-id="ff468-127">Enter the following PowerShell cmdlet to create to create the project:</span></span>

        New-AzureServiceProject helloworld

    ![O resultado do comando New-AzureService helloworld][The result of the New-AzureService helloworld command]

    <span data-ttu-id="ff468-129">O cmdlet **New-AzureServiceProject** gera uma estrutura básica para publicar um aplicativo do Node.js para um Serviço de Nuvem.</span><span class="sxs-lookup"><span data-stu-id="ff468-129">The **New-AzureServiceProject** cmdlet generates a basic structure for publishing a Node.js application to a Cloud Service.</span></span> <span data-ttu-id="ff468-130">Ele contém arquivos de configuração necessários para publicar no Azure.</span><span class="sxs-lookup"><span data-stu-id="ff468-130">It contains configuration files necessary for publishing to Azure.</span></span> <span data-ttu-id="ff468-131">O cmdlet também altera o diretório de trabalho para o diretório de serviço.</span><span class="sxs-lookup"><span data-stu-id="ff468-131">The cmdlet also changes your working directory to the directory for the service.</span></span>

    <span data-ttu-id="ff468-132">O cmdlet cria os seguintes arquivos:</span><span class="sxs-lookup"><span data-stu-id="ff468-132">The cmdlet creates the following files:</span></span>

   * <span data-ttu-id="ff468-133">**ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** e **ServiceDefinition.csdef**: são arquivos específicos do Azure necessários para publicar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ff468-133">**ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** and **ServiceDefinition.csdef**: Azure-specific files necessary for publishing your application.</span></span> <span data-ttu-id="ff468-134">Para saber mais, consulte [Visão geral da criação de um serviço hospedado para o Azure].</span><span class="sxs-lookup"><span data-stu-id="ff468-134">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
   * <span data-ttu-id="ff468-135">**deploymentSettings.json**: armazena configurações locais que são usadas pelos cmdlets de implantação do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ff468-135">**deploymentSettings.json**: Stores local settings that are used by the Azure PowerShell deployment cmdlets.</span></span>
4. <span data-ttu-id="ff468-136">Digite o seguinte comando para adicionar uma nova função da Web:</span><span class="sxs-lookup"><span data-stu-id="ff468-136">Enter the following command to add a new web role:</span></span>

       Add-AzureNodeWebRole

   ![A saída do comando Add-AzureNodeWebRole.][The output of the Add-AzureNodeWebRole command]

   <span data-ttu-id="ff468-138">O cmdlet **Add-AzureNodeWebRole** cria um aplicativo básico do Node.js.</span><span class="sxs-lookup"><span data-stu-id="ff468-138">The **Add-AzureNodeWebRole** cmdlet creates a basic Node.js application.</span></span> <span data-ttu-id="ff468-139">Ele também modifica os arquivos **.csfg** e **.csdef** para adicionar entradas de configuração para a nova função.</span><span class="sxs-lookup"><span data-stu-id="ff468-139">It also modifies the **.csfg** and **.csdef** files to add configuration entries for the new role.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ff468-140">Se você não especificar um nome de função, um nome padrão será usado.</span><span class="sxs-lookup"><span data-stu-id="ff468-140">If you do not specify a role name, a default name is used.</span></span> <span data-ttu-id="ff468-141">Você pode fornecer um nome como o primeiro parâmetro do cmdlet: `Add-AzureNodeWebRole MyRole`</span><span class="sxs-lookup"><span data-stu-id="ff468-141">You can provide a name as the first cmdlet parameter: `Add-AzureNodeWebRole MyRole`</span></span>

<span data-ttu-id="ff468-142">O aplicativo do Node.js é definido no arquivo **server.js**, localizado no diretório da função Web (**WebRole1**, por padrão).</span><span class="sxs-lookup"><span data-stu-id="ff468-142">The Node.js app is defined in the file **server.js**, located in the directory for the web role (**WebRole1** by default).</span></span> <span data-ttu-id="ff468-143">Eis o código:</span><span class="sxs-lookup"><span data-stu-id="ff468-143">Here is the code:</span></span>

    var http = require('http');
    var port = process.env.port || 1337;
    http.createServer(function (req, res) {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('Hello World\n');
    }).listen(port);

<span data-ttu-id="ff468-144">Esse código é basicamente o mesmo código do exemplo "Hello World" no site [nodejs.org] , com a exceção de que ele usa o número de porta atribuído pelo ambiente de nuvem.</span><span class="sxs-lookup"><span data-stu-id="ff468-144">This code is essentially the same as the "Hello World" sample on the [nodejs.org] website, except it uses the port number assigned by the cloud environment.</span></span>

## <a name="deploy-the-application-to-azure"></a><span data-ttu-id="ff468-145">Implantar o aplicativo no Azure</span><span class="sxs-lookup"><span data-stu-id="ff468-145">Deploy the application to Azure</span></span>

> [!NOTE]
> <span data-ttu-id="ff468-146">Para concluir este tutorial, você precisa de uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="ff468-146">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="ff468-147">Você pode [ativar os benefícios de assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) ou [se inscrever para fazer uma conta gratuita](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).</span><span class="sxs-lookup"><span data-stu-id="ff468-147">You can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) or [sign up for a free account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).</span></span>

### <a name="download-the-azure-publishing-settings"></a><span data-ttu-id="ff468-148">Baixar as configurações de publicação do Azure</span><span class="sxs-lookup"><span data-stu-id="ff468-148">Download the Azure publishing settings</span></span>
<span data-ttu-id="ff468-149">Para implantar seu aplicativo do Azure, você deve primeiro baixar as definições de publicação para sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="ff468-149">To deploy your application to Azure, you must first download the publishing settings for your Azure subscription.</span></span>

1. <span data-ttu-id="ff468-150">Execute o seguinte cmdlet do PowerShell do Azure:</span><span class="sxs-lookup"><span data-stu-id="ff468-150">Run the following Azure PowerShell cmdlet:</span></span>

       Get-AzurePublishSettingsFile

   <span data-ttu-id="ff468-151">Isso irá usar o navegador para navegar para a página de download de configurações de publicação.</span><span class="sxs-lookup"><span data-stu-id="ff468-151">This will use your browser to navigate to the publish settings download page.</span></span> <span data-ttu-id="ff468-152">Você precisará fazer logon com uma conta da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ff468-152">You may be prompted to log in with a Microsoft Account.</span></span> <span data-ttu-id="ff468-153">Se fizer, use a conta associada com sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="ff468-153">If so, use the account associated with your Azure subscription.</span></span>

   <span data-ttu-id="ff468-154">Salve o perfil baixado para um local de arquivo, que você pode acessar facilmente.</span><span class="sxs-lookup"><span data-stu-id="ff468-154">Save the downloaded profile to a file location you can easily access.</span></span>
2. <span data-ttu-id="ff468-155">Execute o seguinte cmdlet para importar o perfil de publicação que você baixou:</span><span class="sxs-lookup"><span data-stu-id="ff468-155">Run following cmdlet to import the publishing profile you downloaded:</span></span>

       Import-AzurePublishSettingsFile [path to file]

    > [!NOTE]
    > <span data-ttu-id="ff468-156">Depois de importar as configurações de publicação, considere a exclusão do arquivo .publishsettings baixado, pois ele contém informações que podem permitir que alguém acesse sua conta.</span><span class="sxs-lookup"><span data-stu-id="ff468-156">After importing the publish settings, consider deleting the downloaded .publishSettings file, because it contains information that could allow someone to access your account.</span></span>

### <a name="publish-the-application"></a><span data-ttu-id="ff468-157">Publicar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="ff468-157">Publish the application</span></span>
<span data-ttu-id="ff468-158">Para publicar, execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="ff468-158">To publish, run the following commands:</span></span>

      $ServiceName = "NodeHelloWorld" + $(Get-Date -Format ('ddhhmm'))
    Publish-AzureServiceProject -ServiceName $ServiceName  -Location "East US" -Launch

* <span data-ttu-id="ff468-159">**-ServiceName** especifica o nome para a implantação.</span><span class="sxs-lookup"><span data-stu-id="ff468-159">**-ServiceName** specifies the name for the deployment.</span></span> <span data-ttu-id="ff468-160">Esse deve ser um nome exclusivo, caso contrário, o processo de publicação falhará.</span><span class="sxs-lookup"><span data-stu-id="ff468-160">This must be a unique name, otherwise the publish process will fail.</span></span> <span data-ttu-id="ff468-161">O comando **Get-Date** usa uma cadeia de caracteres de data/hora que deve tornar o nome exclusivo.</span><span class="sxs-lookup"><span data-stu-id="ff468-161">The **Get-Date** command tacks on a date/time string that should make the name unique.</span></span>
* <span data-ttu-id="ff468-162">**-Location** especifica o datacenter no qual o aplicativo será hospedado.</span><span class="sxs-lookup"><span data-stu-id="ff468-162">**-Location** specifies the datacenter that the application will be hosted in.</span></span> <span data-ttu-id="ff468-163">Para ver uma lista dos centros de dados disponíveis, use o cmdlet **Get-AzureLocation** .</span><span class="sxs-lookup"><span data-stu-id="ff468-163">To see a list of available datacenters, use the **Get-AzureLocation** cmdlet.</span></span>
* <span data-ttu-id="ff468-164">**-Launch** abre uma janela do navegador e navega para o serviço hospedado após a conclusão da implantação.</span><span class="sxs-lookup"><span data-stu-id="ff468-164">**-Launch** opens a browser window and navigates to the hosted service after deployment has completed.</span></span>

<span data-ttu-id="ff468-165">Após a publicação for bem-sucedida, você verá uma resposta semelhante à seguinte:</span><span class="sxs-lookup"><span data-stu-id="ff468-165">After publishing succeeds, you will see a response similar to the following:</span></span>

![A saída do comando Publish-AzureService][The output of the Publish-AzureService command]

> [!NOTE]
> <span data-ttu-id="ff468-167">Pode levar alguns minutos para o aplicativo ser implantado e tornar-se disponível quando for publicado pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="ff468-167">It can take several minutes for the application to deploy and become available when first published.</span></span>

<span data-ttu-id="ff468-168">Depois que a implantação for concluída, uma janela do navegador será aberta e irá navegar para o serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="ff468-168">Once the deployment has completed, a browser window will open and navigate to the cloud service.</span></span>

![Uma janela do navegador exibindo a página hello world; a URL indica que a página está hospedada no Azure.][A browser window displaying the hello world page; the URL indicates the page is hosted on Azure.]

<span data-ttu-id="ff468-170">Seu aplicativo está em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="ff468-170">Your application is now running on Azure.</span></span>

<span data-ttu-id="ff468-171">O cmdlet **Publish-AzureServiceProject** executa as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ff468-171">The **Publish-AzureServiceProject** cmdlet performs the following steps:</span></span>

1. <span data-ttu-id="ff468-172">Cria um pacote a ser implantado.</span><span class="sxs-lookup"><span data-stu-id="ff468-172">Creates a package to deploy.</span></span> <span data-ttu-id="ff468-173">O pacote contém todos os arquivos em sua pasta de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="ff468-173">The package contains all the files in your application folder.</span></span>
2. <span data-ttu-id="ff468-174">Cria uma nova **conta de armazenamento** se não existir.</span><span class="sxs-lookup"><span data-stu-id="ff468-174">Creates a new **storage account** if one does not exist.</span></span> <span data-ttu-id="ff468-175">A conta de armazenamento do Azure é usada para armazenar o pacote de aplicativos durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="ff468-175">The Azure storage account is used to store the application package during deployment.</span></span> <span data-ttu-id="ff468-176">Você pode excluir com segurança a conta de armazenamento após a conclusão da implantação.</span><span class="sxs-lookup"><span data-stu-id="ff468-176">You can safely delete the storage account after deployment is done.</span></span>
3. <span data-ttu-id="ff468-177">Cria um novo **serviço de nuvem** se não existir.</span><span class="sxs-lookup"><span data-stu-id="ff468-177">Creates a new **cloud service** if one does not already exist.</span></span> <span data-ttu-id="ff468-178">Um **serviço de nuvem** é o contêiner no qual seu aplicativo é hospedado quando é implantado no Azure.</span><span class="sxs-lookup"><span data-stu-id="ff468-178">A **cloud service** is the container in which your application is hosted when it is deployed to Azure.</span></span> <span data-ttu-id="ff468-179">Para saber mais, consulte [Visão geral da criação de um serviço hospedado para o Azure].</span><span class="sxs-lookup"><span data-stu-id="ff468-179">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
4. <span data-ttu-id="ff468-180">Publica o pacote de implantação do Azure.</span><span class="sxs-lookup"><span data-stu-id="ff468-180">Publishes the deployment package to Azure.</span></span>

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="ff468-181">Parando e excluindo seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="ff468-181">Stopping and deleting your application</span></span>
<span data-ttu-id="ff468-182">Depois de implantar seu aplicativo, convém desativá-lo para que você possa evitar custos extras.</span><span class="sxs-lookup"><span data-stu-id="ff468-182">After deploying your application, you may want to disable it so you can avoid extra costs.</span></span> <span data-ttu-id="ff468-183">O Azure cobra as instâncias de função web por hora de acordo com o tempo consumido do servidor.</span><span class="sxs-lookup"><span data-stu-id="ff468-183">Azure bills web role instances per hour of server time consumed.</span></span> <span data-ttu-id="ff468-184">O tempo do servidor é consumido quando seu aplicativo é implantado, mesmo se as instâncias não estiverem sendo executadas e estiverem no estado parado.</span><span class="sxs-lookup"><span data-stu-id="ff468-184">Server time is consumed once your application is deployed, even if the instances are not running and are in the stopped state.</span></span>

1. <span data-ttu-id="ff468-185">Na janela do Windows PowerShell, interrompa a implantação do serviço criada na seção anterior com o seguinte cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ff468-185">In the Windows PowerShell window, stop the service deployment created in the previous section with the following cmdlet:</span></span>

       Stop-AzureService

   <span data-ttu-id="ff468-186">Interromper o serviço pode levar alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="ff468-186">Stopping the service may take several minutes.</span></span> <span data-ttu-id="ff468-187">Quando o serviço for interrompido, você recebe uma mensagem indicando que foi interrompido.</span><span class="sxs-lookup"><span data-stu-id="ff468-187">When the service is stopped, you receive a message indicating that it has stopped.</span></span>

   ![O status do comando Stop-AzureService][The status of the Stop-AzureService command]
2. <span data-ttu-id="ff468-189">Para excluir o serviço, chame o seguinte cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ff468-189">To delete the service, call the following cmdlet:</span></span>

       Remove-AzureService

   <span data-ttu-id="ff468-190">Quando solicitado, insira **Y** para excluir o serviço.</span><span class="sxs-lookup"><span data-stu-id="ff468-190">When prompted, enter **Y** to delete the service.</span></span>

   <span data-ttu-id="ff468-191">Excluir o serviço pode levar alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="ff468-191">Deleting the service may take several minutes.</span></span> <span data-ttu-id="ff468-192">Após o serviço ter sido excluído, você recebe uma mensagem indicando que o serviço foi excluído.</span><span class="sxs-lookup"><span data-stu-id="ff468-192">After the service has been deleted you receive a message indicating that the service was deleted.</span></span>

   ![O status do comando Remove-AzureService][The status of the Remove-AzureService command]

   > [!NOTE]
   > <span data-ttu-id="ff468-194">Excluir o serviço não exclui a conta de armazenamento criada quando o serviço foi inicialmente publicado e você continuará a ser cobrado pelo armazenamento usado.</span><span class="sxs-lookup"><span data-stu-id="ff468-194">Deleting the service does not delete the storage account that was created when the service was initially published, and you will continue to be billed for storage used.</span></span> <span data-ttu-id="ff468-195">Se ninguém mais está usando o repositório, convém excluí-lo.</span><span class="sxs-lookup"><span data-stu-id="ff468-195">If nothing else is using the storage, you may want to delete it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff468-196">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ff468-196">Next steps</span></span>
<span data-ttu-id="ff468-197">Para saber mais, confira o [Centro de desenvolvedores do Node.js].</span><span class="sxs-lookup"><span data-stu-id="ff468-197">For more information, see the [Node.js Developer Center].</span></span>

<!-- URL List -->

<span data-ttu-id="ff468-198">[Comparação de Sites do Azure, Serviços de Nuvem e Máquinas virtuais]: ../app-service-web/choose-web-site-cloud-service-vm.md</span><span class="sxs-lookup"><span data-stu-id="ff468-198">[Azure Websites, Cloud Services and Virtual Machines comparison]: ../app-service-web/choose-web-site-cloud-service-vm.md</span></span>
<span data-ttu-id="ff468-199">[usar um aplicativo Web leve]: ../app-service-web/app-service-web-get-started-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="ff468-199">[using a lightweight web app]: ../app-service-web/app-service-web-get-started-nodejs.md</span></span>
<span data-ttu-id="ff468-200">[Powershell do Azure]: /powershell/azureps-cmdlets-docs</span><span class="sxs-lookup"><span data-stu-id="ff468-200">[Azure Powershell]: /powershell/azureps-cmdlets-docs</span></span>
<span data-ttu-id="ff468-201">[SDK do Azure para .NET 2.7]: http://www.microsoft.com/en-us/download/details.aspx?id=48178</span><span class="sxs-lookup"><span data-stu-id="ff468-201">[Azure SDK for .NET 2.7]: http://www.microsoft.com/en-us/download/details.aspx?id=48178</span></span>
<span data-ttu-id="ff468-202">[Conecte o PowerShell]: /powershell/azureps-cmdlets-docs#step-3-connect</span><span class="sxs-lookup"><span data-stu-id="ff468-202">[Connect PowerShell]: /powershell/azureps-cmdlets-docs#step-3-connect</span></span>
<span data-ttu-id="ff468-203">[nodejs.org]: http://nodejs.org/</span><span class="sxs-lookup"><span data-stu-id="ff468-203">[nodejs.org]: http://nodejs.org/</span></span>
<span data-ttu-id="ff468-204">[Visão geral da criação de um serviço hospedado para o Azure]: https://azure.microsoft.com/documentation/services/cloud-services/</span><span class="sxs-lookup"><span data-stu-id="ff468-204">[Overview of Creating a Hosted Service for Azure]: https://azure.microsoft.com/documentation/services/cloud-services/</span></span>
<span data-ttu-id="ff468-205">[Centro de desenvolvedores do Node.js]: https://azure.microsoft.com/develop/nodejs/</span><span class="sxs-lookup"><span data-stu-id="ff468-205">[Node.js Developer Center]: https://azure.microsoft.com/develop/nodejs/</span></span>

<!-- IMG List -->

[The result of the New-AzureService helloworld command]: ./media/cloud-services-nodejs-develop-deploy-app/node9.png
[The output of the Add-AzureNodeWebRole command]: ./media/cloud-services-nodejs-develop-deploy-app/node11.png
[A web browser displaying the Hello World web page]: ./media/cloud-services-nodejs-develop-deploy-app/node14.png
[The output of the Publish-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node19.png
[A browser window displaying the hello world page; the URL indicates the page is hosted on Azure.]: ./media/cloud-services-nodejs-develop-deploy-app/node21.png
[The status of the Stop-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node48.png
[The status of the Remove-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node49.png
