---
title: aplicativos web de tecnologias de origem aaaOpen perguntas frequentes sobre o Azure | Microsoft Docs
description: "Obtenha respostas toofrequently perguntas frequentes sobre tecnologias de código-fonte aberto no recurso de aplicativos Web de saudação do serviço de aplicativo do Azure."
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 35cff4f322859d25972747cf55aa7c4316381a51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="open-source-technologies-faqs-for-web-apps-in-azure"></a><span data-ttu-id="d27fb-103">Perguntas frequentes sobre tecnologias de código aberto para Aplicativos Web do Azure</span><span class="sxs-lookup"><span data-stu-id="d27fb-103">Open-source technologies FAQs for Web Apps in Azure</span></span>

<span data-ttu-id="d27fb-104">Este artigo possui respostas toofrequently perguntas frequentes (FAQs) sobre os problemas com tecnologias de código-fonte aberto para Olá [recurso de aplicativos Web do serviço de aplicativo do Azure](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="d27fb-104">This article has answers toofrequently asked questions (FAQs) about issues with open-source technologies for hello [Web Apps feature of Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-cleardb-database-is-down-how-do-i-resolve-this"></a><span data-ttu-id="d27fb-105">Meu banco de dados ClearDB está inoperante.</span><span class="sxs-lookup"><span data-stu-id="d27fb-105">My ClearDB database is down.</span></span> <span data-ttu-id="d27fb-106">Como resolver isso?</span><span class="sxs-lookup"><span data-stu-id="d27fb-106">How do I resolve this?</span></span>

<span data-ttu-id="d27fb-107">Para problemas relacionados ao banco de dados, entre em contato com o [Suporte do ClearDB](https://www.cleardb.com/developers/help/support).</span><span class="sxs-lookup"><span data-stu-id="d27fb-107">For database-related issues, contact [ClearDB support](https://www.cleardb.com/developers/help/support).</span></span> 

<span data-ttu-id="d27fb-108">Para respostas toocommon dúvidas ClearDB, consulte [ClearDB perguntas frequentes sobre](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="d27fb-108">For answers toocommon questions about ClearDB, see [ClearDB FAQs](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="why-isnt-my-cleardb-database-listed-in-hello-portal"></a><span data-ttu-id="d27fb-109">Por que meu banco de dados ClearDB não estiver listado no portal de Olá?</span><span class="sxs-lookup"><span data-stu-id="d27fb-109">Why isn't my ClearDB database listed in hello portal?</span></span>

<span data-ttu-id="d27fb-110">Se você criar um banco de dados ClearDB Olá [portal do Azure](http://portal.azure.com/), banco de dados de saudação não aparece na Olá [portal clássico do Azure](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="d27fb-110">If you create a ClearDB database in hello [Azure portal](http://portal.azure.com/), hello database doesn't appear in hello [Azure classic portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="d27fb-111">toowork esse problema, você pode vincular manualmente seu aplicativo de web de toohello do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="d27fb-111">toowork around this, you can manually link your database toohello web app.</span></span>

<span data-ttu-id="d27fb-112">Da mesma forma, se você criar um banco de dados ClearDB Olá [portal clássico do Azure](http://manage.windowsazure.com/), você não verá o banco de dados em Olá [portal do Azure](http://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d27fb-112">Similarly, if you create a ClearDB database in hello [Azure classic portal](http://manage.windowsazure.com/),  you won't see your database in hello [Azure portal](http://portal.azure.com/).</span></span> <span data-ttu-id="d27fb-113">Nesse caso, nenhuma solução alternativa está disponível.</span><span class="sxs-lookup"><span data-stu-id="d27fb-113">In this case, no workaround is available.</span></span> 

<span data-ttu-id="d27fb-114">Para mais informações, consulte [Perguntas frequentes sobre bancos de dados MySql do ClearDB com o Serviço de Aplicativo do Azure](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="d27fb-114">For more information, see [FAQs for ClearDB MySQL databases with Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="why-wasnt-my-cleardb-database-migrated-during-my-subscription-migration"></a><span data-ttu-id="d27fb-115">Por que meu banco de dados ClearDB não migrou durante a migração da minha assinatura?</span><span class="sxs-lookup"><span data-stu-id="d27fb-115">Why wasn't my ClearDB database migrated during my subscription migration?</span></span>

<span data-ttu-id="d27fb-116">Quando você executar recursos de migração entre assinaturas, serão aplicadas algumas limitações.</span><span class="sxs-lookup"><span data-stu-id="d27fb-116">When you perform resource migration across subscriptions, some limitations apply.</span></span> <span data-ttu-id="d27fb-117">O banco de dados MySQL ClearDB é um serviço de terceiros e, portanto, não será migrado durante a migração da assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="d27fb-117">A ClearDB MySQL database is a third-party service and is not migrated during an Azure subscription migration.</span></span>

<span data-ttu-id="d27fb-118">Se você não gerencia a migração de saudação do banco de dados MySQL antes de migrar os recursos do Azure, seu banco de dados ClearDB MySQL pode estar indisponível.</span><span class="sxs-lookup"><span data-stu-id="d27fb-118">If you don't manage hello migration of your MySQL database before you migrate your Azure resources, your ClearDB MySQL database might be unavailable.</span></span> <span data-ttu-id="d27fb-119">tooavoid isso, primeiro, migrar manualmente o banco de dados ClearDB e, em seguida, migrar Olá assinatura do Azure para seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="d27fb-119">tooavoid this, first, manually migrate your ClearDB database, and then migrate hello Azure subscription for your web app.</span></span>

<span data-ttu-id="d27fb-120">Para mais informações, consulte [Perguntas frequentes sobre bancos de dados MySql do ClearDB com o Serviço de Aplicativo do Azure](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="d27fb-120">For more information, see [FAQs for ClearDB MySQL databases with Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="how-do-i-turn-on-php-logging-tootroubleshoot-php-issues"></a><span data-ttu-id="d27fb-121">Como ativar PHP log tootroubleshoot problemas PHP?</span><span class="sxs-lookup"><span data-stu-id="d27fb-121">How do I turn on PHP logging tootroubleshoot PHP issues?</span></span>

<span data-ttu-id="d27fb-122">tooturn registro em log de PHP:</span><span class="sxs-lookup"><span data-stu-id="d27fb-122">tooturn on PHP logging:</span></span>

1. <span data-ttu-id="d27fb-123">Entrar tooyour [site Kudu](https://*yourwebsitename*.scm.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="d27fb-123">Sign in tooyour [Kudu website](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
2. <span data-ttu-id="d27fb-124">No menu superior do hello, selecione **Console depuração** > **CMD**.</span><span class="sxs-lookup"><span data-stu-id="d27fb-124">In hello top menu, select **Debug Console** > **CMD**.</span></span>
3. <span data-ttu-id="d27fb-125">Selecione Olá **Site** pasta.</span><span class="sxs-lookup"><span data-stu-id="d27fb-125">Select hello **Site** folder.</span></span>
4. <span data-ttu-id="d27fb-126">Selecione Olá **wwwroot** pasta.</span><span class="sxs-lookup"><span data-stu-id="d27fb-126">Select hello **wwwroot** folder.</span></span>
5. <span data-ttu-id="d27fb-127">Selecione Olá  **+**  ícone e, em seguida, selecione **novo arquivo**.</span><span class="sxs-lookup"><span data-stu-id="d27fb-127">Select hello **+** icon, and then select **New File**.</span></span>
6. <span data-ttu-id="d27fb-128">Defina o nome do arquivo hello muito**. user.ini**.</span><span class="sxs-lookup"><span data-stu-id="d27fb-128">Set hello file name too**.user.ini**.</span></span>
7. <span data-ttu-id="d27fb-129">Selecione o ícone de lápis Olá Avançar muito**. user.ini**.</span><span class="sxs-lookup"><span data-stu-id="d27fb-129">Select hello pencil icon next too**.user.ini**.</span></span>
8. <span data-ttu-id="d27fb-130">No arquivo hello, adicione este código:`log_errors=on`</span><span class="sxs-lookup"><span data-stu-id="d27fb-130">In hello file, add this code: `log_errors=on`</span></span>
9. <span data-ttu-id="d27fb-131">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="d27fb-131">Select **Save**.</span></span>
10. <span data-ttu-id="d27fb-132">Selecione o ícone de lápis Olá Avançar muito**config.php wp**.</span><span class="sxs-lookup"><span data-stu-id="d27fb-132">Select hello pencil icon next too**wp-config.php**.</span></span>
11. <span data-ttu-id="d27fb-133">Alterar toohello de texto de saudação código a seguir:</span><span class="sxs-lookup"><span data-stu-id="d27fb-133">Change hello text toohello following code:</span></span>
   ```
   //Enable WP_DEBUG modedefine('WP_DEBUG', true);//Enable debug logging too/wp-content/debug.logdefine('WP_DEBUG_LOG', true);
   //Supress errors and warnings tooscreendefine('WP_DEBUG_DISPLAY', false);//Supress PHP errors tooscreenini_set('display_errors', 0);
   ```
12. <span data-ttu-id="d27fb-134">Olá portal do Azure, no menu de aplicativo web hello, reiniciar o seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="d27fb-134">In hello Azure portal, in hello web app menu, restart your web app.</span></span>

<span data-ttu-id="d27fb-135">Para obter mais informações, consulte [Habilitar logs de erros do WordPress](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span><span class="sxs-lookup"><span data-stu-id="d27fb-135">For more information, see [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span></span>

## <a name="how-do-i-log-python-application-errors-in-apps-that-are-hosted-in-app-service"></a><span data-ttu-id="d27fb-136">Como registrar erros do aplicativo Python em aplicativos que são hospedados no Serviço de Aplicativo?</span><span class="sxs-lookup"><span data-stu-id="d27fb-136">How do I log Python application errors in apps that are hosted in App Service?</span></span>

<span data-ttu-id="d27fb-137">erros de aplicativo do Python toocapture:</span><span class="sxs-lookup"><span data-stu-id="d27fb-137">toocapture Python application errors:</span></span>

1. <span data-ttu-id="d27fb-138">No hello portal do Azure, em seu aplicativo web, selecione **configurações**.</span><span class="sxs-lookup"><span data-stu-id="d27fb-138">In hello Azure portal, in your web app, select **Settings**.</span></span>
2. <span data-ttu-id="d27fb-139">Em Olá **configurações** guia, selecione **configurações de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="d27fb-139">On hello **Settings** tab, select **Application settings**.</span></span>
3. <span data-ttu-id="d27fb-140">Em **configurações do aplicativo**, digite Olá par chave/valor a seguir:</span><span class="sxs-lookup"><span data-stu-id="d27fb-140">Under **App settings**, enter hello following key/value pair:</span></span>
    * <span data-ttu-id="d27fb-141">Chave: WSGI_LOG</span><span class="sxs-lookup"><span data-stu-id="d27fb-141">Key : WSGI_LOG</span></span>
    * <span data-ttu-id="d27fb-142">Valor: D:\home\site\wwwroot\logs.txt (Insira o nome de arquivo da sua escolha)</span><span class="sxs-lookup"><span data-stu-id="d27fb-142">Value : D:\home\site\wwwroot\logs.txt (enter your choice of file name)</span></span>

<span data-ttu-id="d27fb-143">Agora você verá erros no arquivo de logs de saudação na pasta wwwroot hello.</span><span class="sxs-lookup"><span data-stu-id="d27fb-143">You should now see errors in hello logs.txt file in hello wwwroot folder.</span></span>

## <a name="how-do-i-change-hello-version-of-hello-nodejs-application-that-is-hosted-in-app-service"></a><span data-ttu-id="d27fb-144">Como alterar a versão de saudação do hello aplicativo Node. js que é hospedado no serviço de aplicativo?</span><span class="sxs-lookup"><span data-stu-id="d27fb-144">How do I change hello version of hello Node.js application that is hosted in App Service?</span></span>

<span data-ttu-id="d27fb-145">toochange Olá versão Olá aplicativo Node. js, você pode usar uma saudação as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="d27fb-145">toochange hello version of hello Node.js application, you can use one of hello following options:</span></span>

*   <span data-ttu-id="d27fb-146">Olá portal do Azure, usar **configurações do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="d27fb-146">In hello Azure portal, use **App settings**.</span></span>
    1. <span data-ttu-id="d27fb-147">No hello portal do Azure, vá tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="d27fb-147">In hello Azure portal, go tooyour web app.</span></span>
    2. <span data-ttu-id="d27fb-148">Em Olá **configurações** folha, selecione **configurações de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="d27fb-148">On hello **Settings** blade, select **Application settings**.</span></span>
    3. <span data-ttu-id="d27fb-149">Em **configurações do aplicativo**, você pode incluir WEBSITE_NODE_DEFAULT_VERSION como chave hello e hello versão do Node. js que desejar como valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="d27fb-149">In **App settings**, you can include WEBSITE_NODE_DEFAULT_VERSION as hello key, and hello version of Node.js you want as hello value.</span></span>
    4. <span data-ttu-id="d27fb-150">Vá tooyour [console Kudu](https://*yourwebsitename*.scm.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="d27fb-150">Go tooyour [Kudu console](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
    5. <span data-ttu-id="d27fb-151">toocheck Olá versão Node. js, digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="d27fb-151">toocheck hello Node.js version, enter hello following command:</span></span>  
   ```
   node -v
   ```
*   <span data-ttu-id="d27fb-152">Modificar o arquivo de iisnode.yml hello.</span><span class="sxs-lookup"><span data-stu-id="d27fb-152">Modify hello iisnode.yml file.</span></span> <span data-ttu-id="d27fb-153">Versão de Node. js Olá alteração no arquivo de iisnode.yml Olá apenas define ambiente de tempo de execução de saudação que iisnode usa.</span><span class="sxs-lookup"><span data-stu-id="d27fb-153">Changing hello Node.js version in hello iisnode.yml file only sets hello runtime environment that iisnode uses.</span></span> <span data-ttu-id="d27fb-154">O cmd Kudu e outros ainda usam a versão de Node. js de saudação que está definida no **configurações do aplicativo** em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d27fb-154">Your Kudu cmd and others still use hello Node.js version that is set in **App settings** in hello Azure portal.</span></span>

    <span data-ttu-id="d27fb-155">tooset Olá iisnode.yml manualmente, crie um arquivo de iisnode.yml na pasta raiz do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d27fb-155">tooset hello iisnode.yml manually, create an iisnode.yml file in your app root folder.</span></span> <span data-ttu-id="d27fb-156">No arquivo hello, incluem hello seguinte linha:</span><span class="sxs-lookup"><span data-stu-id="d27fb-156">In hello file, include hello following line:</span></span>
   ```
   nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
   ```
   
*   <span data-ttu-id="d27fb-157">Olá iisnode.yml arquivo de conjunto usando Package. JSON durante a implantação do controle de origem.</span><span class="sxs-lookup"><span data-stu-id="d27fb-157">Set hello iisnode.yml file by using package.json during source control deployment.</span></span>
    <span data-ttu-id="d27fb-158">Olá processo de implantação de controle do código-fonte do Azure envolve Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d27fb-158">hello Azure source control deployment process involves hello following steps:</span></span>
    1. <span data-ttu-id="d27fb-159">Move o aplicativo web do Azure de toohello conteúdo.</span><span class="sxs-lookup"><span data-stu-id="d27fb-159">Moves content toohello Azure web app.</span></span>
    2. <span data-ttu-id="d27fb-160">Cria um script de implantação padrão, se não houver um (Deploy, arquivos .deployment) na pasta raiz do Olá web app.</span><span class="sxs-lookup"><span data-stu-id="d27fb-160">Creates a default deployment script, if there isn’t one (deploy.cmd, .deployment files) in hello web app root folder.</span></span>
    3. <span data-ttu-id="d27fb-161">Executa um script de implantação em que ele cria um arquivo iisnode.yml se mencionar versão do Node. js Olá no arquivo de Package. JSON hello > mecanismo`"engines": {"node": "5.9.1","npm": "3.7.3"}`</span><span class="sxs-lookup"><span data-stu-id="d27fb-161">Runs a deployment script in which it creates an iisnode.yml file if you mention hello Node.js version in hello package.json file > engine `"engines": {"node": "5.9.1","npm": "3.7.3"}`</span></span>
    4. <span data-ttu-id="d27fb-162">arquivo de iisnode.yml Olá tem Olá a seguinte linha de código:</span><span class="sxs-lookup"><span data-stu-id="d27fb-162">hello iisnode.yml file has hello following line of code:</span></span>
        ```
        nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
        ```

## <a name="i-see-hello-message-error-establishing-a-database-connection-in-my-wordpress-app-thats-hosted-in-app-service-how-do-i-troubleshoot-this"></a><span data-ttu-id="d27fb-163">Vejo a mensagem de saudação "Erro ao estabelecer uma conexão de banco de dados" em meu aplicativo WordPress que é hospedado no serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d27fb-163">I see hello message "Error establishing a database connection" in my WordPress app that's hosted in App Service.</span></span> <span data-ttu-id="d27fb-164">Como solucionar isso?</span><span class="sxs-lookup"><span data-stu-id="d27fb-164">How do I troubleshoot this?</span></span>

<span data-ttu-id="d27fb-165">Se você vir esse erro no aplicativo do Azure WordPress, tooenable php_errors.log e Debug, etapas de saudação completa detalhadas em [logs de erros do WordPress habilitar](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span><span class="sxs-lookup"><span data-stu-id="d27fb-165">If you see this error in your Azure WordPress app, tooenable php_errors.log and debug.log, complete hello steps detailed in [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span></span>

<span data-ttu-id="d27fb-166">Quando Olá logs são habilitados, reproduza o erro Olá e verifique se Olá logs toosee se você estiver executando sem conexões:</span><span class="sxs-lookup"><span data-stu-id="d27fb-166">When hello logs are enabled, reproduce hello error, and then check hello logs toosee if you are running out of connections:</span></span>
```
[09-Oct-2015 00:03:13 UTC] PHP Warning: mysqli_real_connect(): (HY000/1226): User ‘abcdefghijk79' has exceeded hello ‘max_user_connections’ resource (current value: 4) in D:\home\site\wwwroot\wp-includes\wp-db.php on line 1454
```

<span data-ttu-id="d27fb-167">Se você vir esse erro nos arquivos de Debug ou php_errors.log, seu aplicativo é excede o número de saudação de conexões.</span><span class="sxs-lookup"><span data-stu-id="d27fb-167">If you see this error in your debug.log or php_errors.log files, your app is exceeding hello number of connections.</span></span> <span data-ttu-id="d27fb-168">Se você estiver hospedando no ClearDB, verifique o número de saudação de conexões que estão disponíveis no seu [plano de serviço](https://www.cleardb.com/pricing.view).</span><span class="sxs-lookup"><span data-stu-id="d27fb-168">If you’re hosting on ClearDB, verify hello number of connections that are available in your [service plan](https://www.cleardb.com/pricing.view).</span></span>

## <a name="how-do-i-debug-a-nodejs-app-thats-hosted-in-app-service"></a><span data-ttu-id="d27fb-169">Como depurar um aplicativo Node.js que está hospedado no Serviço de Aplicativo?</span><span class="sxs-lookup"><span data-stu-id="d27fb-169">How do I debug a Node.js app that's hosted in App Service?</span></span>

1.  <span data-ttu-id="d27fb-170">Vá tooyour [console Kudu](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).</span><span class="sxs-lookup"><span data-stu-id="d27fb-170">Go tooyour [Kudu console](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).</span></span>
2.  <span data-ttu-id="d27fb-171">Pasta de logs de aplicativo do vá tooyour (D:\home\LogFiles\Application).</span><span class="sxs-lookup"><span data-stu-id="d27fb-171">Go tooyour application logs folder (D:\home\LogFiles\Application).</span></span>
3.  <span data-ttu-id="d27fb-172">No arquivo de logging_errors.txt hello, verifique se há conteúdo.</span><span class="sxs-lookup"><span data-stu-id="d27fb-172">In hello logging_errors.txt file, check for content.</span></span>

## <a name="how-do-i-install-native-python-modules-in-an-app-service-web-app-or-api-app"></a><span data-ttu-id="d27fb-173">Como instalar módulos Python nativos em um aplicativo web do Serviço de Aplicativo ou aplicativo de API?</span><span class="sxs-lookup"><span data-stu-id="d27fb-173">How do I install native Python modules in an App Service web app or API app?</span></span>

<span data-ttu-id="d27fb-174">Alguns pacotes não podem ser instalados usando o pip no Azure.</span><span class="sxs-lookup"><span data-stu-id="d27fb-174">Some packages might not install by using pip in Azure.</span></span> <span data-ttu-id="d27fb-175">pacote de saudação pode não estar disponível em Olá Python pacote índice ou um compilador pode ser necessário (um compilador não está disponível no computador de saudação que está executando o aplicativo web de saudação no serviço de aplicativo).</span><span class="sxs-lookup"><span data-stu-id="d27fb-175">hello package might not be available on hello Python Package Index, or a compiler might be required (a compiler is not available on hello computer that is running hello web app in App Service).</span></span> <span data-ttu-id="d27fb-176">Para obter informações sobre como instalar os módulos nativos em aplicativos web do Serviço de Aplicativo e aplicativos de API, consulte [Instalar módulos Python no Serviço de Aplicativo](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/).</span><span class="sxs-lookup"><span data-stu-id="d27fb-176">For information about installing native modules in App Service web apps and API apps, see [Install Python modules in App Service](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/).</span></span>

## <a name="how-do-i-deploy-a-django-app-tooapp-service-by-using-git-and-hello-new-version-of-python"></a><span data-ttu-id="d27fb-177">Como implantar um aplicativo de Django tooApp serviço usando o Git e Olá a nova versão do Python?</span><span class="sxs-lookup"><span data-stu-id="d27fb-177">How do I deploy a Django app tooApp Service by using Git and hello new version of Python?</span></span>

<span data-ttu-id="d27fb-178">Para obter informações sobre como instalar Django, consulte [Implantando um aplicativo de Django tooApp serviço](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).</span><span class="sxs-lookup"><span data-stu-id="d27fb-178">For information about installing Django, see [Deploying a Django app tooApp Service](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).</span></span>

## <a name="where-are-hello-tomcat-log-files-located"></a><span data-ttu-id="d27fb-179">Onde estão os arquivos de log do Tomcat Olá localizados?</span><span class="sxs-lookup"><span data-stu-id="d27fb-179">Where are hello Tomcat log files located?</span></span>

<span data-ttu-id="d27fb-180">Para o Azure Marketplace e implantações personalizadas:</span><span class="sxs-lookup"><span data-stu-id="d27fb-180">For Azure Marketplace and custom deployments:</span></span>

* <span data-ttu-id="d27fb-181">Local da pasta: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs</span><span class="sxs-lookup"><span data-stu-id="d27fb-181">Folder location: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs</span></span>
* <span data-ttu-id="d27fb-182">Arquivos de interesse:</span><span class="sxs-lookup"><span data-stu-id="d27fb-182">Files of interest:</span></span>
    * <span data-ttu-id="d27fb-183">catalina.*aaaa-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="d27fb-183">catalina.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="d27fb-184">host-manager.*aaaa-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="d27fb-184">host-manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="d27fb-185">localhost.*aaaa-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="d27fb-185">localhost.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="d27fb-186">manager.*aaaa-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="d27fb-186">manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="d27fb-187">site_access_log.*yyyy-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="d27fb-187">site_access_log.*yyyy-mm-dd*.log</span></span>


<span data-ttu-id="d27fb-188">Para implantações de **Configurações do aplicativo** do portal:</span><span class="sxs-lookup"><span data-stu-id="d27fb-188">For portal **App settings** deployments:</span></span>

* <span data-ttu-id="d27fb-189">Local da pasta: D:\home\LogFiles</span><span class="sxs-lookup"><span data-stu-id="d27fb-189">Folder location: D:\home\LogFiles</span></span>
* <span data-ttu-id="d27fb-190">Arquivos de interesse:</span><span class="sxs-lookup"><span data-stu-id="d27fb-190">Files of interest:</span></span>
    * <span data-ttu-id="d27fb-191">catalina.*aaaa-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="d27fb-191">catalina.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="d27fb-192">host-manager.*aaaa-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="d27fb-192">host-manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="d27fb-193">localhost.*aaaa-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="d27fb-193">localhost.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="d27fb-194">manager.*aaaa-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="d27fb-194">manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="d27fb-195">site_access_log.*yyyy-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="d27fb-195">site_access_log.*yyyy-mm-dd*.log</span></span>

## <a name="how-do-i-troubleshoot-jdbc-driver-connection-errors"></a><span data-ttu-id="d27fb-196">Como solucionar problemas de erros de conexão do driver JDBC?</span><span class="sxs-lookup"><span data-stu-id="d27fb-196">How do I troubleshoot JDBC driver connection errors?</span></span>

<span data-ttu-id="d27fb-197">Você poderá ver Olá seguinte mensagem nos logs Tomcat:</span><span class="sxs-lookup"><span data-stu-id="d27fb-197">You might see hello following message in your Tomcat logs:</span></span>

```
hello web application[ROOT] registered hello JDBC driver [com.mysql.jdbc.Driver] but failed toounregister it when hello web application was stopped. tooprevent a memory leak,hello JDBC Driver has been forcibly unregistered
```

<span data-ttu-id="d27fb-198">Erro de saudação tooresolve:</span><span class="sxs-lookup"><span data-stu-id="d27fb-198">tooresolve hello error:</span></span>

1. <span data-ttu-id="d27fb-199">Remova o arquivo de sqljdbc*.jar de saudação da sua pasta de aplicativo/lib.</span><span class="sxs-lookup"><span data-stu-id="d27fb-199">Remove hello sqljdbc*.jar file from your app/lib folder.</span></span>
2. <span data-ttu-id="d27fb-200">Se você estiver usando Olá Tomcat ou o Azure Marketplace Tomcat servidor web personalizado, copie essa pasta lib do. jar arquivo toohello Tomcat.</span><span class="sxs-lookup"><span data-stu-id="d27fb-200">If you are using hello custom Tomcat or Azure Marketplace Tomcat web server, copy this .jar file toohello Tomcat lib folder.</span></span>
3. <span data-ttu-id="d27fb-201">Se você estiver habilitando Java do hello portal do Azure (selecione **Java 1.8** > **servidor Tomcat**), cópia Olá sqljdbc.* jar arquivo hello pasta que é aplicativo tooyour paralela.</span><span class="sxs-lookup"><span data-stu-id="d27fb-201">If you are enabling Java from hello Azure portal (select **Java 1.8** > **Tomcat server**), copy hello sqljdbc.* jar file in hello folder that's parallel tooyour app.</span></span> <span data-ttu-id="d27fb-202">Em seguida, adicione Olá classpath configuração toohello. config a seguir:</span><span class="sxs-lookup"><span data-stu-id="d27fb-202">Then, add hello following classpath setting toohello web.config file:</span></span>

    ```
    <httpPlatform>
    <environmentVariables>
    <environmentVariablename ="JAVA_OPTS" value=" -Djava.net.preferIPv4Stack=true
    -Xms128M -classpath %CLASSPATH%;[Path toohello sqljdbc*.jarfile]" />
    </environmentVariables>
    </httpPlatform>
    ```

## <a name="why-do-i-see-errors-when-i-attempt-toocopy-live-log-files"></a><span data-ttu-id="d27fb-203">Por que vejo erros quando tento toocopy arquivos de log em tempo real?</span><span class="sxs-lookup"><span data-stu-id="d27fb-203">Why do I see errors when I attempt toocopy live log files?</span></span>

<span data-ttu-id="d27fb-204">Se você tentar toocopy arquivos de log em tempo real para um aplicativo Java (por exemplo, Tomcat), você poderá ver esse erro FTP:</span><span class="sxs-lookup"><span data-stu-id="d27fb-204">If you try toocopy live log files for a Java app (for example, Tomcat), you might see this FTP error:</span></span>

```
Error transferring file [filename] Copying files from remote side failed.
    
hello process cannot access hello file because it is being used by another process.
```

<span data-ttu-id="d27fb-205">mensagem de erro de saudação poderão variar, dependendo de cliente Olá FTP.</span><span class="sxs-lookup"><span data-stu-id="d27fb-205">hello error message might vary, depending on hello FTP client.</span></span>

<span data-ttu-id="d27fb-206">Todos os aplicativos Java tem esse problema de bloqueio.</span><span class="sxs-lookup"><span data-stu-id="d27fb-206">All Java apps have this locking issue.</span></span> <span data-ttu-id="d27fb-207">Somente Kudu oferece suporte a baixar este arquivo enquanto o aplicativo hello está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="d27fb-207">Only Kudu supports downloading this file while hello app is running.</span></span>

<span data-ttu-id="d27fb-208">Parando aplicativo de saudação permite acesso FTP toothese de arquivos.</span><span class="sxs-lookup"><span data-stu-id="d27fb-208">Stopping hello app allows FTP access toothese files.</span></span>

<span data-ttu-id="d27fb-209">Outra alternativa é toowrite um trabalho Web que é executado em um agendamento e copia esses diretório diferente de tooa de arquivos.</span><span class="sxs-lookup"><span data-stu-id="d27fb-209">Another workaround is toowrite a WebJob that runs on a schedule and copies these files tooa different directory.</span></span> <span data-ttu-id="d27fb-210">Para um projeto de exemplo, consulte Olá [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob) projeto.</span><span class="sxs-lookup"><span data-stu-id="d27fb-210">For a sample project, see hello [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob) project.</span></span>

## <a name="where-do-i-find-hello-log-files-for-jetty"></a><span data-ttu-id="d27fb-211">Onde encontrar os arquivos de log Olá para Jetty?</span><span class="sxs-lookup"><span data-stu-id="d27fb-211">Where do I find hello log files for Jetty?</span></span>

<span data-ttu-id="d27fb-212">Para o Marketplace e implantações personalizadas, o arquivo de log de saudação está na pasta de D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs hello.</span><span class="sxs-lookup"><span data-stu-id="d27fb-212">For Marketplace and custom deployments, hello log file is in hello D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs folder.</span></span> <span data-ttu-id="d27fb-213">Observe que local da pasta Olá depende da versão de saudação do Jetty que você está usando.</span><span class="sxs-lookup"><span data-stu-id="d27fb-213">Note that hello folder location depends on hello version of Jetty you are using.</span></span> <span data-ttu-id="d27fb-214">Por exemplo, o caminho de saudação fornecidas aqui servem para Jetty 9.1.2.</span><span class="sxs-lookup"><span data-stu-id="d27fb-214">For example, hello path provided here is for Jetty 9.1.2.</span></span> <span data-ttu-id="d27fb-215">Procure jetty_*YYYY_MM_DD*.stderrout.log.</span><span class="sxs-lookup"><span data-stu-id="d27fb-215">Look for jetty_*YYYY_MM_DD*.stderrout.log.</span></span>

<span data-ttu-id="d27fb-216">Para implantações de configuração do aplicativo do portais, o arquivo de log hello está em D:\home\LogFiles.</span><span class="sxs-lookup"><span data-stu-id="d27fb-216">For portal App Setting deployments, hello log file is in D:\home\LogFiles.</span></span> <span data-ttu-id="d27fb-217">Procure jetty_*YYYY_MM_DD*.stderrout.log</span><span class="sxs-lookup"><span data-stu-id="d27fb-217">Look for jetty_*YYYY_MM_DD*.stderrout.log</span></span>

## <a name="can-i-send-email-from-my-azure-web-app"></a><span data-ttu-id="d27fb-218">Posso enviar email de meu aplicativo web do Azure?</span><span class="sxs-lookup"><span data-stu-id="d27fb-218">Can I send email from my Azure web app?</span></span>

<span data-ttu-id="d27fb-219">Serviço de Aplicativo não tem uma funcionalidade de email interno.</span><span class="sxs-lookup"><span data-stu-id="d27fb-219">App Service doesn't have a built-in email feature.</span></span> <span data-ttu-id="d27fb-220">Para algumas boas alternativas para enviar email de seu aplicativo, consulte esta [Discussão de Stack Overflow](http://stackoverflow.com/questions/17666161/sending-email-from-azure).</span><span class="sxs-lookup"><span data-stu-id="d27fb-220">For some good alternatives for sending email from your app, see this [Stack Overflow discussion](http://stackoverflow.com/questions/17666161/sending-email-from-azure).</span></span>

## <a name="why-does-my-wordpress-site-redirect-tooanother-url"></a><span data-ttu-id="d27fb-221">Por que meu site WordPress redirecionar a URL tooanother?</span><span class="sxs-lookup"><span data-stu-id="d27fb-221">Why does my WordPress site redirect tooanother URL?</span></span>

<span data-ttu-id="d27fb-222">Se você tiver migrado recentemente tooAzure, WordPress pode URL de redirecionamento toohello antigo domínio.</span><span class="sxs-lookup"><span data-stu-id="d27fb-222">If you have recently migrated tooAzure, WordPress might redirect toohello old domain URL.</span></span> <span data-ttu-id="d27fb-223">Isso é causado por uma configuração no banco de dados do hello MySQL.</span><span class="sxs-lookup"><span data-stu-id="d27fb-223">This is caused by a setting in hello MySQL database.</span></span>

<span data-ttu-id="d27fb-224">WordPress Buddy + é uma extensão de Site do Azure que você pode usar o URL de redirecionamento de saudação tooupdate diretamente no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="d27fb-224">WordPress Buddy+ is an Azure Site Extension that you can use tooupdate hello redirection URL directly in hello database.</span></span> <span data-ttu-id="d27fb-225">Para obter mais informações sobre como usar o WordPress Buddy +, consulte [Ferramentas WordPress e migração do MySQL com WordPress Buddy +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span><span class="sxs-lookup"><span data-stu-id="d27fb-225">For more information about using WordPress Buddy+, see [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

<span data-ttu-id="d27fb-226">Como alternativa, se você preferir a URL de redirecionamento do toomanually atualização hello usando consultas SQL ou PHPMyAdmin, consulte [WordPress: redirecionamento de URL toowrong](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/).</span><span class="sxs-lookup"><span data-stu-id="d27fb-226">Alternatively, if you prefer toomanually update hello redirection URL by using SQL queries or PHPMyAdmin, see [WordPress: Redirecting toowrong URL](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/).</span></span>

## <a name="how-do-i-change-my-wordpress-sign-in-password"></a><span data-ttu-id="d27fb-227">Como alterar minha senha de logon do WordPress?</span><span class="sxs-lookup"><span data-stu-id="d27fb-227">How do I change my WordPress sign-in password?</span></span>

<span data-ttu-id="d27fb-228">Se você esqueceu sua senha de logon do WordPress, você pode usar o WordPress Buddy + tooupdate-lo.</span><span class="sxs-lookup"><span data-stu-id="d27fb-228">If you have forgotten your WordPress sign-in password, you can use WordPress Buddy+ tooupdate it.</span></span> <span data-ttu-id="d27fb-229">tooreset sua senha, Olá instalar extensão Site WordPress Buddy + do Azure e as etapas de Olá concluída, em seguida, descritas em [WordPress ferramentas e migração do MySQL com WordPress Buddy +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span><span class="sxs-lookup"><span data-stu-id="d27fb-229">tooreset your password, install hello WordPress Buddy+ Azure Site Extension, and then complete hello steps described in [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

## <a name="i-cant-sign-in-toowordpress-how-do-i-resolve-this"></a><span data-ttu-id="d27fb-230">Não consigo entrar tooWordPress.</span><span class="sxs-lookup"><span data-stu-id="d27fb-230">I can't sign in tooWordPress.</span></span> <span data-ttu-id="d27fb-231">Como resolver isso?</span><span class="sxs-lookup"><span data-stu-id="d27fb-231">How do I resolve this?</span></span>

<span data-ttu-id="d27fb-232">Se você estiver o WordPress bloqueado depois de instalar recentemente um plug-in, você pode ter um plug-in com defeito.</span><span class="sxs-lookup"><span data-stu-id="d27fb-232">If you find yourself locked out of WordPress after recently installing a plugin, you might have a faulty plugin.</span></span> <span data-ttu-id="d27fb-233">WordPress Buddy + é uma extensão de Site do Azure que podem ajudá-lo desabilitar plug-ins no WordPress.</span><span class="sxs-lookup"><span data-stu-id="d27fb-233">WordPress Buddy+ is an Azure Site Extension that can help you disable plugins in WordPress.</span></span> <span data-ttu-id="d27fb-234">Para obter mais informações, consulte [Ferramentas WordPress e migração do MySQL com WordPress Buddy +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span><span class="sxs-lookup"><span data-stu-id="d27fb-234">For more information, see [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

## <a name="how-do-i-migrate-my-wordpress-database"></a><span data-ttu-id="d27fb-235">Como migrar meu banco de dados do WordPress?</span><span class="sxs-lookup"><span data-stu-id="d27fb-235">How do I migrate my WordPress database?</span></span>

<span data-ttu-id="d27fb-236">Você tem várias opções de migração Olá MySQL banco de dados conectado tooyour WordPress site:</span><span class="sxs-lookup"><span data-stu-id="d27fb-236">You have multiple options for migrating hello MySQL database that's connected tooyour WordPress website:</span></span>

* <span data-ttu-id="d27fb-237">Desenvolvedores: Saudação de uso [prompt de comando ou PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)</span><span class="sxs-lookup"><span data-stu-id="d27fb-237">Developers: Use hello [command prompt or PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)</span></span>
* <span data-ttu-id="d27fb-238">Não-desenvolvedores: Usar [WordPress Buddy +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)</span><span class="sxs-lookup"><span data-stu-id="d27fb-238">Non-developers: Use [WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)</span></span>

## <a name="how-do-i-help-make-wordpress-more-secure"></a><span data-ttu-id="d27fb-239">Como ajudar a proteger melhor o WordPress?</span><span class="sxs-lookup"><span data-stu-id="d27fb-239">How do I help make WordPress more secure?</span></span>

<span data-ttu-id="d27fb-240">toolearn sobre as práticas recomendadas de segurança para WordPress, consulte [as práticas recomendadas para segurança do WordPress no Azure](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).</span><span class="sxs-lookup"><span data-stu-id="d27fb-240">toolearn about security best practices for WordPress, see [Best practices for WordPress security in Azure](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).</span></span>

## <a name="i-am-trying-toouse-phpmyadmin-and-i-see-hello-message-access-denied-how-do-i-resolve-this"></a><span data-ttu-id="d27fb-241">Estou tentando toouse PHPMyAdmin e posso ver a mensagem "Acesso negado".</span><span class="sxs-lookup"><span data-stu-id="d27fb-241">I am trying toouse PHPMyAdmin, and I see hello message “Access denied.”</span></span> <span data-ttu-id="d27fb-242">Como resolver isso?</span><span class="sxs-lookup"><span data-stu-id="d27fb-242">How do I resolve this?</span></span>

<span data-ttu-id="d27fb-243">Se o recurso de no aplicativo hello MySQL não está em execução ainda nesta instância do serviço de aplicativo, você poderá enfrentar esse problema.</span><span class="sxs-lookup"><span data-stu-id="d27fb-243">You might experience this issue if hello MySQL in-app feature isn't running yet in this App Service instance.</span></span> <span data-ttu-id="d27fb-244">tooresolve Olá problema, tente tooaccess seu site.</span><span class="sxs-lookup"><span data-stu-id="d27fb-244">tooresolve hello issue, try tooaccess your website.</span></span> <span data-ttu-id="d27fb-245">Isso inicia processos Olá necessárias, incluindo processo Olá MySQL no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d27fb-245">This starts hello required processes, including hello MySQL in-app process.</span></span> <span data-ttu-id="d27fb-246">tooverify que MySQL no aplicativo está em execução, no Explorador de processos, certifique-se de que mysqld.exe é listado em processos de saudação.</span><span class="sxs-lookup"><span data-stu-id="d27fb-246">tooverify that MySQL in-app is running, in Process Explorer, ensure that mysqld.exe is listed in hello processes.</span></span>

<span data-ttu-id="d27fb-247">Depois de garantir que o MySQL no aplicativo está em execução, tente toouse PHPMyAdmin.</span><span class="sxs-lookup"><span data-stu-id="d27fb-247">After you ensure that MySQL in-app is running, try toouse PHPMyAdmin.</span></span>

## <a name="i-get-an-http-403-error-when-i-try-tooimport-or-export-my-mysql-in-app-database-by-using-phpmyadmin-how-do-i-resolve-this"></a><span data-ttu-id="d27fb-248">Recebo um erro de HTTP 403 quando tentar tooimport ou exportar meu banco de dados MySQL no aplicativo usando PHPMyadmin.</span><span class="sxs-lookup"><span data-stu-id="d27fb-248">I get an HTTP 403 error when I try tooimport or export my MySQL in-app database by using PHPMyadmin.</span></span> <span data-ttu-id="d27fb-249">Como resolver isso?</span><span class="sxs-lookup"><span data-stu-id="d27fb-249">How do I resolve this?</span></span>

<span data-ttu-id="d27fb-250">Se você estiver usando uma versão mais antiga do Chrome, talvez você esteja tendo um bug conhecido.</span><span class="sxs-lookup"><span data-stu-id="d27fb-250">If you are using an older version of Chrome, you might be experiencing a known bug.</span></span> <span data-ttu-id="d27fb-251">problema de saudação tooresolve, tooa atualizar a versão mais recente do Chrome.</span><span class="sxs-lookup"><span data-stu-id="d27fb-251">tooresolve hello issue, upgrade tooa newer version of Chrome.</span></span> <span data-ttu-id="d27fb-252">Além disso, tente usando um navegador diferente, como o Internet Explorer ou borda, onde Olá problema não ocorre.</span><span class="sxs-lookup"><span data-stu-id="d27fb-252">Also try using a different browser, like Internet Explorer or Edge, where hello issue does not occur.</span></span>
