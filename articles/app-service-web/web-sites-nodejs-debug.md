---
title: "aaaHow toodebug um aplicativo da web Node. js no serviço de aplicativo do Azure"
description: "Saiba como toodebug um Node. js web app no serviço de aplicativo do Azure."
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
ms.openlocfilehash: 888ec5c3f92cfc3aeea4ea86005b9b6a0d1306ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodebug-a-nodejs-web-app-in-azure-app-service"></a><span data-ttu-id="9c180-103">Como toodebug um Node. js web app no serviço de aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="9c180-103">How toodebug a Node.js web app in Azure App Service</span></span>
<span data-ttu-id="9c180-104">O Azure fornece tooassist diagnóstico interno com depuração Node. js aplicativos hospedados em [do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="9c180-104">Azure provides built-in diagnostics tooassist with debugging Node.js applications hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="9c180-105">Neste artigo, você aprenderá como log tooenable de stdout e stderr, exibir informações de erro no navegador hello e como toodownload e exibir arquivos de log.</span><span class="sxs-lookup"><span data-stu-id="9c180-105">In this article, you will learn how tooenable logging of stdout and stderr, display error information in hello browser, and how toodownload and view log files.</span></span>

<span data-ttu-id="9c180-106">O diagnóstico para aplicativos do Node.js hospedados no Azure é fornecido por [IISNode].</span><span class="sxs-lookup"><span data-stu-id="9c180-106">Diagnostics for Node.js applications hosted on Azure is provided by [IISNode].</span></span> <span data-ttu-id="9c180-107">Embora este artigo aborda as configurações mais comuns de saudação para reunir informações de diagnóstico, ele não fornece uma referência completa para trabalhar com IISNode.</span><span class="sxs-lookup"><span data-stu-id="9c180-107">While this article discusses hello most common settings for gathering diagnostics information, it does not provide a complete reference for working with IISNode.</span></span> <span data-ttu-id="9c180-108">Para obter mais informações sobre como trabalhar com IISNode, consulte Olá [IISNode Readme] no GitHub.</span><span class="sxs-lookup"><span data-stu-id="9c180-108">For more information on working with IISNode, see hello [IISNode Readme] on GitHub.</span></span>

<a id="enablelogging"></a>

## <a name="enable-logging"></a><span data-ttu-id="9c180-109">Habilitar o registro em log</span><span class="sxs-lookup"><span data-stu-id="9c180-109">Enable logging</span></span>
<span data-ttu-id="9c180-110">Por padrão, um aplicativo Web do Serviço de Aplicativo captura somente informações de diagnóstico sobre implantações, como quando você implanta um aplicativo Web usando Git.</span><span class="sxs-lookup"><span data-stu-id="9c180-110">By default, an App Service web app only captures diagnostic information about deployments, such as when you deploy a web app using Git.</span></span> <span data-ttu-id="9c180-111">Essas informações são úteis se você estiver tendo problemas durante a implantação, como uma falha durante a instalação de um módulo referenciado na **package.json**, ou se você estiver usando um script de implantação personalizada.</span><span class="sxs-lookup"><span data-stu-id="9c180-111">This information is useful if you are having problems during deployment, such as a failure when installing a module referenced in **package.json**, or if you are using a custom deployment script.</span></span>

<span data-ttu-id="9c180-112">Olá tooenable log de fluxos stdout e stderr, você deve criar um **IISNode.yml** arquivo na raiz de saudação do seu aplicativo Node. js e adicione o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="9c180-112">tooenable hello logging of stdout and stderr streams, you must create an **IISNode.yml** file at hello root of your Node.js application and add hello following:</span></span>

    loggingEnabled: true

<span data-ttu-id="9c180-113">Isso habilita o log de saudação do stderr e stdout do seu aplicativo Node. js.</span><span class="sxs-lookup"><span data-stu-id="9c180-113">This enables hello logging of stderr and stdout from your Node.js application.</span></span>

<span data-ttu-id="9c180-114">Olá **IISNode.yml** arquivo também pode ser usado toocontrol se erros amigáveis ou desenvolvedor são retornados toohello navegador quando ocorre uma falha.</span><span class="sxs-lookup"><span data-stu-id="9c180-114">hello **IISNode.yml** file can also be used toocontrol whether friendly errors or developer errors are returned toohello browser when a failure occurs.</span></span> <span data-ttu-id="9c180-115">erros de desenvolvedor tooenable, adicionar Olá toohello linha a seguir **IISNode.yml** arquivo:</span><span class="sxs-lookup"><span data-stu-id="9c180-115">tooenable developer errors, add hello following line toohello **IISNode.yml** file:</span></span>

    devErrorsEnabled: true

<span data-ttu-id="9c180-116">Quando essa opção é habilitada, IISNode retornará Olá última 64K de informações enviadas toostderr em vez de um erro amigável, como "Ocorreu um erro interno do servidor".</span><span class="sxs-lookup"><span data-stu-id="9c180-116">Once this option is enabled, IISNode will return hello last 64K of information sent toostderr instead of a friendly error such as "an internal server error occurred".</span></span>

> [!NOTE]
> <span data-ttu-id="9c180-117">Enquanto devErrorsEnabled é útil para diagnosticar problemas durante o desenvolvimento, habilitá-la em um ambiente de produção pode resultar em erros de desenvolvimento que está sendo enviados tooend usuários.</span><span class="sxs-lookup"><span data-stu-id="9c180-117">While devErrorsEnabled is useful when diagnosing problems during development, enabling it in a production environment may result in development errors being sent tooend users.</span></span>
> 
> 

<span data-ttu-id="9c180-118">Se hello **IISNode.yml** arquivo ainda não existia no seu aplicativo, você deve reiniciar seu aplicativo web depois de publicar o aplicativo hello atualizado.</span><span class="sxs-lookup"><span data-stu-id="9c180-118">If hello **IISNode.yml** file did not already exist within your application, you must restart your web app after publishing hello updated application.</span></span> <span data-ttu-id="9c180-119">Se você estiver simplesmente alterando as configurações em um arquivo **IISNode.yml** arquivo que tenha sido publicado anteriormente, não é necessário reiniciar.</span><span class="sxs-lookup"><span data-stu-id="9c180-119">If you are simply changing settings in an existing **IISNode.yml** file that has previously been published, no restart is required.</span></span>

> [!NOTE]
> <span data-ttu-id="9c180-120">Se seu aplicativo web foi criado usando as ferramentas de linha de comando do Azure hello ou Cmdlets do PowerShell do Azure, um padrão **IISNode.yml** arquivo será criado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="9c180-120">If your web app was created using hello Azure Command-Line Tools or Azure PowerShell Cmdlets, a default **IISNode.yml** file is automatically created.</span></span>
> 
> 

<span data-ttu-id="9c180-121">aplicativo web do hello toorestart, aplicativo web de select Olá Olá [Portal do Azure](https://portal.azure.com)e, em seguida, clique em **reiniciar** botão:</span><span class="sxs-lookup"><span data-stu-id="9c180-121">toorestart hello web app, select hello web app in hello [Azure Portal](https://portal.azure.com), and then click **RESTART** button:</span></span>

![botão de reinicialização][restart-button]

<span data-ttu-id="9c180-123">Se Olá ferramentas de linha de comando do Azure estão instaladas em seu ambiente de desenvolvimento, você pode usar Olá comando toorestart Olá web aplicativo a seguir:</span><span class="sxs-lookup"><span data-stu-id="9c180-123">If hello Azure Command-Line Tools are installed in your development environment, you can use hello following command toorestart hello web app:</span></span>

    azure site restart [sitename]

> [!NOTE]
> <span data-ttu-id="9c180-124">Enquanto loggingEnabled e devErrorsEnabled são opções de configuração de IISNode.yml hello mais comumente usado para capturar informações de diagnóstico, IISNode.yml pode ser usado tooconfigure uma variedade de opções para o seu ambiente de hospedagem.</span><span class="sxs-lookup"><span data-stu-id="9c180-124">While loggingEnabled and devErrorsEnabled are hello most commonly used IISNode.yml configuration options for capturing diagnostic information, IISNode.yml can be used tooconfigure a variety of options for your hosting environment.</span></span> <span data-ttu-id="9c180-125">Para obter uma lista completa das opções de configuração de hello, consulte Olá [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) arquivo.</span><span class="sxs-lookup"><span data-stu-id="9c180-125">For a full list of hello configuration options, see hello [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) file.</span></span>
> 
> 

<a id="viewlogs"></a>

## <a name="accessing-logs"></a><span data-ttu-id="9c180-126">Acessando os logs</span><span class="sxs-lookup"><span data-stu-id="9c180-126">Accessing logs</span></span>
<span data-ttu-id="9c180-127">Logs de diagnóstico que podem ser acessados de três maneiras; Usando Olá protocolo FTP (File Transfer), baixar um arquivo Zip, ou como um dinâmica atualizado o fluxo de log da saudação (também conhecido como a parte final).</span><span class="sxs-lookup"><span data-stu-id="9c180-127">Diagnostic logs can be accessed in three ways; Using hello File Transfer Protocol (FTP), downloading a Zip archive, or as a live updated stream of hello log (also known as a tail).</span></span> <span data-ttu-id="9c180-128">Baixando o arquivo Zip Olá Olá dos arquivos de log ou exibindo o fluxo ao vivo Olá exigem Olá ferramentas de linha de comando do Azure.</span><span class="sxs-lookup"><span data-stu-id="9c180-128">Downloading hello Zip archive of hello log files or viewing hello live stream require hello Azure Command-Line Tools.</span></span> <span data-ttu-id="9c180-129">Elas podem ser instaladas usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="9c180-129">These can be installed by using hello following command:</span></span>

    npm install azure-cli -g

<span data-ttu-id="9c180-130">Uma vez instalado, ferramentas de saudação podem ser acessadas usando o comando Olá 'do azure'.</span><span class="sxs-lookup"><span data-stu-id="9c180-130">Once installed, hello tools can be accessed using hello 'azure' command.</span></span> <span data-ttu-id="9c180-131">Olá ferramentas de linha de comando deve ser configurado toouse sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="9c180-131">hello command-line tools must first be configured toouse your Azure subscription.</span></span> <span data-ttu-id="9c180-132">Para obter informações sobre como tooaccomplish essa tarefa, consulte Olá **como toodownload e importar configurações de publicação** seção Olá [como tooUse Olá ferramentas de linha de comando do Azure](../xplat-cli-connect.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="9c180-132">For information on how tooaccomplish this task, see hello **How toodownload and import publish settings** section of hello [How tooUse hello Azure Command-Line Tools](../xplat-cli-connect.md) article.</span></span>

### <a name="ftp"></a><span data-ttu-id="9c180-133">FTP</span><span class="sxs-lookup"><span data-stu-id="9c180-133">FTP</span></span>
<span data-ttu-id="9c180-134">informações de diagnóstico Olá tooaccess por meio de FTP, visite Olá [Portal do Azure](https://portal.azure.com), selecione seu aplicativo web e, em seguida, selecione Olá **painel**.</span><span class="sxs-lookup"><span data-stu-id="9c180-134">tooaccess hello diagnostic information through FTP, visit hello [Azure Portal](https://portal.azure.com), select your web app, and then select hello **DASHBOARD**.</span></span> <span data-ttu-id="9c180-135">Em Olá **links rápidos** seção, hello **LOGS de diagnóstico de FTP** e **LOGS de diagnóstico de FTPS** links fornecem acesso toohello logs usando o protocolo de saudação FTP.</span><span class="sxs-lookup"><span data-stu-id="9c180-135">In hello **quick links** section, hello **FTP DIAGNOSTIC LOGS** and **FTPS DIAGNOSTIC LOGS** links provide access toohello logs using hello FTP protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="9c180-136">Se você não tiver configurado anteriormente o nome de usuário e senha de FTP ou implantação, você pode fazer isso de saudação **Quickstart** página de gerenciamento selecionando **configurar credenciais de implantação**.</span><span class="sxs-lookup"><span data-stu-id="9c180-136">If you have not previously configured user name and password for FTP or deployment, you can do so from hello **Quickstart** management page by selecting **Set up deployment credentials**.</span></span>
> 
> 

<span data-ttu-id="9c180-137">Hello FTP URL retornada no painel de saudação é de saudação **LogFiles** diretório, que irá conter Olá subdiretórios a seguir:</span><span class="sxs-lookup"><span data-stu-id="9c180-137">hello FTP URL returned in hello dashboard is for hello **LogFiles** directory, which will contain hello following sub-directories:</span></span>

* <span data-ttu-id="9c180-138">[Método de implantação](web-sites-deploy.md) -se você usar um método de implantação, como o Git, um diretório de saudação mesmo nome será criado e conterá informações relacionadas toodeployments.</span><span class="sxs-lookup"><span data-stu-id="9c180-138">[Deployment Method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of hello same name will be created and will contain information related toodeployments.</span></span>
* <span data-ttu-id="9c180-139">nodejs - Stdout e stderr informações capturadas de todas as instâncias do seu aplicativo (quando loggingEnabled for true.)</span><span class="sxs-lookup"><span data-stu-id="9c180-139">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="zip-archive"></a><span data-ttu-id="9c180-140">Arquivo Zip</span><span class="sxs-lookup"><span data-stu-id="9c180-140">Zip archive</span></span>
<span data-ttu-id="9c180-141">toodownload um arquivo Zip dos logs de diagnóstico hello, Olá uso a seguir de comando de ferramentas de linha de comando do hello Azure:</span><span class="sxs-lookup"><span data-stu-id="9c180-141">toodownload a Zip archive of hello diagnostic logs, use hello following command from hello Azure Command-Line Tools:</span></span>

    azure site log download [sitename]

<span data-ttu-id="9c180-142">Isso baixará uma **diagnostics.zip** no diretório atual hello.</span><span class="sxs-lookup"><span data-stu-id="9c180-142">This will download a **diagnostics.zip** in hello current directory.</span></span> <span data-ttu-id="9c180-143">Este arquivo contém Olá estrutura de diretórios a seguir:</span><span class="sxs-lookup"><span data-stu-id="9c180-143">This archive contains hello following directory structure:</span></span>

* <span data-ttu-id="9c180-144">implantações - de um log de informações sobre a implantação do seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="9c180-144">deployments - A log of information about deployments of your application</span></span>
* <span data-ttu-id="9c180-145">arquivos de log</span><span class="sxs-lookup"><span data-stu-id="9c180-145">LogFiles</span></span>
  
  * <span data-ttu-id="9c180-146">[Método de implantação](web-sites-deploy.md) -se você usar um método de implantação, como o Git, um diretório de saudação mesmo nome será criado e conterá informações relacionadas toodeployments.</span><span class="sxs-lookup"><span data-stu-id="9c180-146">[Deployment method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of hello same name will be created and will contain information related toodeployments.</span></span>
  * <span data-ttu-id="9c180-147">nodejs - Stdout e stderr informações capturadas de todas as instâncias do seu aplicativo (quando loggingEnabled for true.)</span><span class="sxs-lookup"><span data-stu-id="9c180-147">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="live-stream-tail"></a><span data-ttu-id="9c180-148">Fluxo ao vivo (final)</span><span class="sxs-lookup"><span data-stu-id="9c180-148">Live stream (tail)</span></span>
<span data-ttu-id="9c180-149">tooview uma transmissão ao vivo de informações de log de diagnóstico, Olá uso a seguir de comando de ferramentas de linha de comando do hello Azure:</span><span class="sxs-lookup"><span data-stu-id="9c180-149">tooview a live stream of diagnostic log information, use hello following command from hello Azure Command-Line Tools:</span></span>

    azure site log tail [sitename]

<span data-ttu-id="9c180-150">Isso retorna um fluxo de eventos de log que são atualizadas à medida que ocorrem no servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="9c180-150">This will return a stream of log events that are updated as they occur on hello server.</span></span> <span data-ttu-id="9c180-151">Este fluxo irá retornar informações sobre a implantação, bem como informações de stdout e stderr (quando loggingEnabled for true.)</span><span class="sxs-lookup"><span data-stu-id="9c180-151">This stream will return deployment information as well as stdout and stderr information (when loggingEnabled is true.)</span></span>

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="9c180-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9c180-152">Next Steps</span></span>
<span data-ttu-id="9c180-153">Neste artigo, você aprendeu como tooenable e acessar as informações de diagnóstico do Azure.</span><span class="sxs-lookup"><span data-stu-id="9c180-153">In this article you learned how tooenable and access diagnostics information for Azure.</span></span> <span data-ttu-id="9c180-154">Enquanto essas informações são úteis em Noções básicas sobre problemas ocorridos com seu aplicativo, ele pode apontar tooa problema com um módulo que você está usando ou versão saudação do Node. js usado pelo serviço de aplicativo Web de aplicativos é diferente de saudação usado na sua implantação ambiente.</span><span class="sxs-lookup"><span data-stu-id="9c180-154">While this information is useful in understanding problems that occur with your application, it may point tooa problem with a module you are using or that hello version of Node.js used by App Service Web Apps is different than hello one used in your deployment environment.</span></span>

<span data-ttu-id="9c180-155">Para obter informações no trabalho com módulos no Azure, consulte [usando o Node. js módulos com aplicativos do Azure](../nodejs-use-node-modules-azure-apps.md)</span><span class="sxs-lookup"><span data-stu-id="9c180-155">For information in working with modules on Azure, see [Using Node.js Modules with Azure Applications](../nodejs-use-node-modules-azure-apps.md).</span></span>

<span data-ttu-id="9c180-156">Para obter informações sobre como especificar uma versão do Node.js para seu aplicativo, consulte [Especificar uma versão do Node.js em um aplicativo do Azure].</span><span class="sxs-lookup"><span data-stu-id="9c180-156">For information on specifying a Node.js version for your application, see [Specifying a Node.js version in an Azure application].</span></span>

<span data-ttu-id="9c180-157">Para obter mais informações, consulte também Olá [Node. js Developer Center](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="9c180-157">For more information, see also hello [Node.js Developer Center](/develop/nodejs/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="9c180-158">O que mudou</span><span class="sxs-lookup"><span data-stu-id="9c180-158">What's changed</span></span>
* <span data-ttu-id="9c180-159">Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="9c180-159">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="9c180-160">Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9c180-160">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="9c180-161">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="9c180-161">No credit cards required; no commitments.</span></span>
> 
> 

[IISNode]: https://github.com/tjanczuk/iisnode
[IISNode Readme]: https://github.com/tjanczuk/iisnode#readme
[How tooUse hello Azure Command-Line Interface]:../cli-install-nodejs.md
[Using Node.js Modules with Azure Applications]: ../nodejs-use-node-modules-azure-apps.md
[Especificar uma versão do Node.js em um aplicativo do Azure]: ../nodejs-specify-node-version-azure-apps.md

[restart-button]: ./media/web-sites-nodejs-debug/restartbutton.png

