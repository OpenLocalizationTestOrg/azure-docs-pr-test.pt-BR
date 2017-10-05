---
title: "Como depurar um aplicativo Web Node.js no Serviço de Aplicativo do Azure"
description: "Saiba como depurar um aplicativo Web Node.js no Serviço de Aplicativo do Azure"
tags: azure-portal
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: a48f906c-1a3e-43bc-ae84-7d2dde175b15
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 5e302a4c58a171d40e43a22c34c724e868019ec8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-debug-a-nodejs-web-app-in-azure-app-service"></a><span data-ttu-id="b7d23-103">Como depurar um aplicativo Web Node.js no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="b7d23-103">How to debug a Node.js web app in Azure App Service</span></span>
<span data-ttu-id="b7d23-104">O Azure fornece diagnóstico interno para ajudar na depuração de aplicativos Node.js hospedados em Aplicativos Web do [Serviço de Aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) .</span><span class="sxs-lookup"><span data-stu-id="b7d23-104">Azure provides built-in diagnostics to assist with debugging Node.js applications hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="b7d23-105">Neste artigo, você aprenderá como habilitar o log de stdout e stderr, exibir informações de erro no navegador e como baixar e exibir arquivos de log.</span><span class="sxs-lookup"><span data-stu-id="b7d23-105">In this article, you will learn how to enable logging of stdout and stderr, display error information in the browser, and how to download and view log files.</span></span>

<span data-ttu-id="b7d23-106">O diagnóstico para aplicativos do Node.js hospedados no Azure é fornecido por [IISNode].</span><span class="sxs-lookup"><span data-stu-id="b7d23-106">Diagnostics for Node.js applications hosted on Azure is provided by [IISNode].</span></span> <span data-ttu-id="b7d23-107">Embora este artigo descreve as configurações mais comuns para coletar informações de diagnóstico, ele não fornece uma referência completa para trabalhar com IISNode.</span><span class="sxs-lookup"><span data-stu-id="b7d23-107">While this article discusses the most common settings for gathering diagnostics information, it does not provide a complete reference for working with IISNode.</span></span> <span data-ttu-id="b7d23-108">Para obter mais informações sobre como trabalhar com IISNode, consulte o [IISNode Readme] no GitHub.</span><span class="sxs-lookup"><span data-stu-id="b7d23-108">For more information on working with IISNode, see the [IISNode Readme] on GitHub.</span></span>

<a id="enablelogging"></a>

## <a name="enable-logging"></a><span data-ttu-id="b7d23-109">Habilitar o registro em log</span><span class="sxs-lookup"><span data-stu-id="b7d23-109">Enable logging</span></span>
<span data-ttu-id="b7d23-110">Por padrão, um aplicativo Web do Serviço de Aplicativo captura somente informações de diagnóstico sobre implantações, como quando você implanta um aplicativo Web usando Git.</span><span class="sxs-lookup"><span data-stu-id="b7d23-110">By default, an App Service web app only captures diagnostic information about deployments, such as when you deploy a web app using Git.</span></span> <span data-ttu-id="b7d23-111">Essas informações são úteis se você estiver tendo problemas durante a implantação, como uma falha durante a instalação de um módulo referenciado na **package.json**, ou se você estiver usando um script de implantação personalizada.</span><span class="sxs-lookup"><span data-stu-id="b7d23-111">This information is useful if you are having problems during deployment, such as a failure when installing a module referenced in **package.json**, or if you are using a custom deployment script.</span></span>

<span data-ttu-id="b7d23-112">Para habilitar o registro em log de fluxos stdout e stderr, você deve criar um arquivo **IISNode.yml** na raiz do seu aplicativo do Node.js e adicionar o seguinte:</span><span class="sxs-lookup"><span data-stu-id="b7d23-112">To enable the logging of stdout and stderr streams, you must create an **IISNode.yml** file at the root of your Node.js application and add the following:</span></span>

    loggingEnabled: true

<span data-ttu-id="b7d23-113">Isso permite que o log de stderr e stdout do seu aplicativo do Node. js.</span><span class="sxs-lookup"><span data-stu-id="b7d23-113">This enables the logging of stderr and stdout from your Node.js application.</span></span>

<span data-ttu-id="b7d23-114">O **IISNode.yml** arquivo também pode ser usado para controlar se erros amigáveis ou desenvolvedor são retornados ao navegador quando ocorre uma falha.</span><span class="sxs-lookup"><span data-stu-id="b7d23-114">The **IISNode.yml** file can also be used to control whether friendly errors or developer errors are returned to the browser when a failure occurs.</span></span> <span data-ttu-id="b7d23-115">Para permitir que erros de desenvolvedor, adicione a seguinte linha para o **IISNode.yml** arquivo:</span><span class="sxs-lookup"><span data-stu-id="b7d23-115">To enable developer errors, add the following line to the **IISNode.yml** file:</span></span>

    devErrorsEnabled: true

<span data-ttu-id="b7d23-116">Quando essa opção estiver habilitada, IISNode retornará a última 64K de informações enviadas para stderr em vez de um erro amigáveis, como "Ocorreu um erro interno do servidor".</span><span class="sxs-lookup"><span data-stu-id="b7d23-116">Once this option is enabled, IISNode will return the last 64K of information sent to stderr instead of a friendly error such as "an internal server error occurred".</span></span>

> [!NOTE]
> <span data-ttu-id="b7d23-117">Enquanto devErrorsEnabled é útil para diagnosticar problemas durante o desenvolvimento, ativá-lo em um ambiente de produção pode resultar em erros de desenvolvimento sendo enviados para usuários finais.</span><span class="sxs-lookup"><span data-stu-id="b7d23-117">While devErrorsEnabled is useful when diagnosing problems during development, enabling it in a production environment may result in development errors being sent to end users.</span></span>
> 
> 

<span data-ttu-id="b7d23-118">Se o arquivo **iisnode. yml** ainda não existir dentro de seu aplicativo, você deverá reiniciar o aplicativo Web depois de publicar o aplicativo atualizado.</span><span class="sxs-lookup"><span data-stu-id="b7d23-118">If the **IISNode.yml** file did not already exist within your application, you must restart your web app after publishing the updated application.</span></span> <span data-ttu-id="b7d23-119">Se você estiver simplesmente alterando as configurações em um arquivo **IISNode.yml** arquivo que tenha sido publicado anteriormente, não é necessário reiniciar.</span><span class="sxs-lookup"><span data-stu-id="b7d23-119">If you are simply changing settings in an existing **IISNode.yml** file that has previously been published, no restart is required.</span></span>

> [!NOTE]
> <span data-ttu-id="b7d23-120">Se seu aplicativo Web foi criado usando os Cmdlets do PowerShell do Azure ou as ferramentas de linha de comando do Azure, um arquivo **IISNode.yml** padrão é criado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b7d23-120">If your web app was created using the Azure Command-Line Tools or Azure PowerShell Cmdlets, a default **IISNode.yml** file is automatically created.</span></span>
> 
> 

<span data-ttu-id="b7d23-121">Para reiniciar o aplicativo Web, selecione-o no [Portal do Azure](https://portal.azure.com)e clique no botão **REINICIAR** :</span><span class="sxs-lookup"><span data-stu-id="b7d23-121">To restart the web app, select the web app in the [Azure Portal](https://portal.azure.com), and then click **RESTART** button:</span></span>

![botão de reinicialização][restart-button]

<span data-ttu-id="b7d23-123">Se as ferramentas de linha de comando do Azure estiverem instaladas em seu ambiente de desenvolvimento, você poderá usar o seguinte comando para reiniciar o aplicativo Web:</span><span class="sxs-lookup"><span data-stu-id="b7d23-123">If the Azure Command-Line Tools are installed in your development environment, you can use the following command to restart the web app:</span></span>

    azure site restart [sitename]

> [!NOTE]
> <span data-ttu-id="b7d23-124">Enquanto loggingEnabled e devErrorsEnabled são os mais usados IISNode.yml opções de configuração para a captura de informações de diagnóstico, IISNode.yml pode ser usado para configurar uma variedade de opções para seu ambiente de hospedagem.</span><span class="sxs-lookup"><span data-stu-id="b7d23-124">While loggingEnabled and devErrorsEnabled are the most commonly used IISNode.yml configuration options for capturing diagnostic information, IISNode.yml can be used to configure a variety of options for your hosting environment.</span></span> <span data-ttu-id="b7d23-125">Para obter uma lista completa das opções de configuração, consulte o arquivo [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml).</span><span class="sxs-lookup"><span data-stu-id="b7d23-125">For a full list of the configuration options, see the [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) file.</span></span>
> 
> 

<a id="viewlogs"></a>

## <a name="accessing-logs"></a><span data-ttu-id="b7d23-126">Acessando os logs</span><span class="sxs-lookup"><span data-stu-id="b7d23-126">Accessing logs</span></span>
<span data-ttu-id="b7d23-127">Logs de diagnóstico podem ser acessado de três maneiras; Usando o protocolo FTP (File Transfer), fazer o download de um arquivo Zip, ou como um live atualizado fluxo do log (também conhecido como um laço).</span><span class="sxs-lookup"><span data-stu-id="b7d23-127">Diagnostic logs can be accessed in three ways; Using the File Transfer Protocol (FTP), downloading a Zip archive, or as a live updated stream of the log (also known as a tail).</span></span> <span data-ttu-id="b7d23-128">Fazer o download do arquivo Zip dos arquivos de log ou exibição do fluxo ao vivo exigem o Azure Command-line Tools.</span><span class="sxs-lookup"><span data-stu-id="b7d23-128">Downloading the Zip archive of the log files or viewing the live stream require the Azure Command-Line Tools.</span></span> <span data-ttu-id="b7d23-129">Elas podem ser instaladas usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="b7d23-129">These can be installed by using the following command:</span></span>

    npm install azure-cli -g

<span data-ttu-id="b7d23-130">Uma vez instalado, as ferramentas podem ser acessadas usando o comando 'azure'.</span><span class="sxs-lookup"><span data-stu-id="b7d23-130">Once installed, the tools can be accessed using the 'azure' command.</span></span> <span data-ttu-id="b7d23-131">As ferramentas de linha de comando devem primeiro ser configuradas para usar sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="b7d23-131">The command-line tools must first be configured to use your Azure subscription.</span></span> <span data-ttu-id="b7d23-132">Para obter informações sobre como realizar essa tarefa, consulte o **como fazer o download e importar as configurações de publicação** seção a [como uso o Azure Command-line Tools](../xplat-cli-connect.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="b7d23-132">For information on how to accomplish this task, see the **How to download and import publish settings** section of the [How to Use The Azure Command-Line Tools](../xplat-cli-connect.md) article.</span></span>

### <a name="ftp"></a><span data-ttu-id="b7d23-133">FTP</span><span class="sxs-lookup"><span data-stu-id="b7d23-133">FTP</span></span>
<span data-ttu-id="b7d23-134">Para acessar as informações de diagnóstico por FTP, visite o [Portal do Azure](https://portal.azure.com), selecione o seu aplicativo Web e selecione **PAINEL**.</span><span class="sxs-lookup"><span data-stu-id="b7d23-134">To access the diagnostic information through FTP, visit the [Azure Portal](https://portal.azure.com), select your web app, and then select the **DASHBOARD**.</span></span> <span data-ttu-id="b7d23-135">Na seção **links rápidos**, os links **LOGS DE DIAGNÓSTICO FTP** e **LOGS DE DIAGNÓSTICO FTPS** fornecem acesso aos logs usando o protocolo FTP.</span><span class="sxs-lookup"><span data-stu-id="b7d23-135">In the **quick links** section, the **FTP DIAGNOSTIC LOGS** and **FTPS DIAGNOSTIC LOGS** links provide access to the logs using the FTP protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="b7d23-136">Se ainda não tiver configurado o nome de usuário e a senha para FTP ou para implantação, você poderá fazer isso da página de gerenciamento **Início rápido** selecionando **Configurar credenciais de implantação**.</span><span class="sxs-lookup"><span data-stu-id="b7d23-136">If you have not previously configured user name and password for FTP or deployment, you can do so from the **Quickstart** management page by selecting **Set up deployment credentials**.</span></span>
> 
> 

<span data-ttu-id="b7d23-137">É a URL FTP retornado no painel de controle para o **arquivos de log** diretório, que irá conter as seguintes subpastas:</span><span class="sxs-lookup"><span data-stu-id="b7d23-137">The FTP URL returned in the dashboard is for the **LogFiles** directory, which will contain the following sub-directories:</span></span>

* <span data-ttu-id="b7d23-138">[Método de implantação](web-sites-deploy.md) - se você usar um método de implantação como git, uma pasta com o mesmo nome será criada e conterá informações relacionadas às implantações.</span><span class="sxs-lookup"><span data-stu-id="b7d23-138">[Deployment Method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of the same name will be created and will contain information related to deployments.</span></span>
* <span data-ttu-id="b7d23-139">nodejs - Stdout e stderr informações capturadas de todas as instâncias do seu aplicativo (quando loggingEnabled for true.)</span><span class="sxs-lookup"><span data-stu-id="b7d23-139">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="zip-archive"></a><span data-ttu-id="b7d23-140">Arquivo Zip</span><span class="sxs-lookup"><span data-stu-id="b7d23-140">Zip archive</span></span>
<span data-ttu-id="b7d23-141">Para fazer o download de um arquivo Zip dos logs de diagnóstico, use o seguinte comando das ferramentas de linha de comando do Azure:</span><span class="sxs-lookup"><span data-stu-id="b7d23-141">To download a Zip archive of the diagnostic logs, use the following command from the Azure Command-Line Tools:</span></span>

    azure site log download [sitename]

<span data-ttu-id="b7d23-142">Isso fará o download uma **diagnostics.zip** no diretório atual.</span><span class="sxs-lookup"><span data-stu-id="b7d23-142">This will download a **diagnostics.zip** in the current directory.</span></span> <span data-ttu-id="b7d23-143">Este arquivo contém a seguinte estrutura de diretórios:</span><span class="sxs-lookup"><span data-stu-id="b7d23-143">This archive contains the following directory structure:</span></span>

* <span data-ttu-id="b7d23-144">implantações - de um log de informações sobre a implantação do seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="b7d23-144">deployments - A log of information about deployments of your application</span></span>
* <span data-ttu-id="b7d23-145">arquivos de log</span><span class="sxs-lookup"><span data-stu-id="b7d23-145">LogFiles</span></span>
  
  * <span data-ttu-id="b7d23-146">[Método de implantação](web-sites-deploy.md) - se você usar um método de implantação como Git, uma pasta com o mesmo nome será criada e conterá informações relacionadas às implantações.</span><span class="sxs-lookup"><span data-stu-id="b7d23-146">[Deployment method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of the same name will be created and will contain information related to deployments.</span></span>
  * <span data-ttu-id="b7d23-147">nodejs - Stdout e stderr informações capturadas de todas as instâncias do seu aplicativo (quando loggingEnabled for true.)</span><span class="sxs-lookup"><span data-stu-id="b7d23-147">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="live-stream-tail"></a><span data-ttu-id="b7d23-148">Fluxo ao vivo (final)</span><span class="sxs-lookup"><span data-stu-id="b7d23-148">Live stream (tail)</span></span>
<span data-ttu-id="b7d23-149">Para visualizar um fluxo ao vivo da informações de log de diagnóstico, use o seguinte comando das ferramentas de linha de comando do Azure:</span><span class="sxs-lookup"><span data-stu-id="b7d23-149">To view a live stream of diagnostic log information, use the following command from the Azure Command-Line Tools:</span></span>

    azure site log tail [sitename]

<span data-ttu-id="b7d23-150">Isso retornará uma cadeia de eventos de log que são atualizados à medida que ocorrem no servidor.</span><span class="sxs-lookup"><span data-stu-id="b7d23-150">This will return a stream of log events that are updated as they occur on the server.</span></span> <span data-ttu-id="b7d23-151">Este fluxo irá retornar informações sobre a implantação, bem como informações de stdout e stderr (quando loggingEnabled for true.)</span><span class="sxs-lookup"><span data-stu-id="b7d23-151">This stream will return deployment information as well as stdout and stderr information (when loggingEnabled is true.)</span></span>

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="b7d23-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b7d23-152">Next Steps</span></span>
<span data-ttu-id="b7d23-153">Neste artigo, você aprendeu como ativar e acessar as informações de diagnóstico do Azure.</span><span class="sxs-lookup"><span data-stu-id="b7d23-153">In this article you learned how to enable and access diagnostics information for Azure.</span></span> <span data-ttu-id="b7d23-154">Embora essas informações sejam úteis em problemas de compreensão que ocorrem em seu aplicativo, podem indicar um problema com um módulo que você esteja usando ou indicar que a versão de Node.js usada pelos Aplicativos Web do Serviço de Aplicativo é diferente daquela usada no seu ambiente de implantação.</span><span class="sxs-lookup"><span data-stu-id="b7d23-154">While this information is useful in understanding problems that occur with your application, it may point to a problem with a module you are using or that the version of Node.js used by App Service Web Apps is different than the one used in your deployment environment.</span></span>

<span data-ttu-id="b7d23-155">Para obter informações no trabalho com módulos no Azure, consulte [usando o Node. js módulos com aplicativos do Azure](../nodejs-use-node-modules-azure-apps.md)</span><span class="sxs-lookup"><span data-stu-id="b7d23-155">For information in working with modules on Azure, see [Using Node.js Modules with Azure Applications](../nodejs-use-node-modules-azure-apps.md).</span></span>

<span data-ttu-id="b7d23-156">Para obter informações sobre como especificar uma versão do Node.js para seu aplicativo, consulte [Especificar uma versão do Node.js em um aplicativo do Azure].</span><span class="sxs-lookup"><span data-stu-id="b7d23-156">For information on specifying a Node.js version for your application, see [Specifying a Node.js version in an Azure application].</span></span>

<span data-ttu-id="b7d23-157">Para obter mais informações, consulte também o [Centro de desenvolvedores do Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="b7d23-157">For more information, see also the [Node.js Developer Center](/develop/nodejs/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="b7d23-158">O que mudou</span><span class="sxs-lookup"><span data-stu-id="b7d23-158">What's changed</span></span>
* <span data-ttu-id="b7d23-159">Para obter um guia sobre a alteração de Sites para o Serviço de Aplicativo, confira: [Serviço de Aplicativo do Azure e seu impacto sobre os serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="b7d23-159">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="b7d23-160">Se desejar começar a usar o Serviço de Aplicativo do Azure antes de inscrever-se em uma conta do Azure, vá para [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo Web inicial de curta duração no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b7d23-160">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="b7d23-161">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="b7d23-161">No credit cards required; no commitments.</span></span>
> 
> 

<span data-ttu-id="b7d23-162">[IISNode]: https://github.com/tjanczuk/iisnode</span><span class="sxs-lookup"><span data-stu-id="b7d23-162">[IISNode]: https://github.com/tjanczuk/iisnode</span></span>
<span data-ttu-id="b7d23-163">[IISNode Readme]: https://github.com/tjanczuk/iisnode#readme</span><span class="sxs-lookup"><span data-stu-id="b7d23-163">[IISNode Readme]: https://github.com/tjanczuk/iisnode#readme</span></span>
[How to Use The Azure Command-Line Interface]:../cli-install-nodejs.md
[Using Node.js Modules with Azure Applications]: ../nodejs-use-node-modules-azure-apps.md
<span data-ttu-id="b7d23-164">[Especificar uma versão do Node.js em um aplicativo do Azure]: ../nodejs-specify-node-version-azure-apps.md</span><span class="sxs-lookup"><span data-stu-id="b7d23-164">[Specifying a Node.js version in an Azure application]: ../nodejs-specify-node-version-azure-apps.md</span></span>

[restart-button]: ./media/web-sites-nodejs-debug/restartbutton.png

