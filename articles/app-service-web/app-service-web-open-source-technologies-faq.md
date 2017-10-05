---
title: "Perguntas frequentes sobre tecnologias de código aberto para aplicativos web do Azure | Microsoft Docs"
description: "Obtenha respostas para perguntas frequentes sobre tecnologias de código aberto na funcionalidade Aplicativos Web do Serviço de Aplicativo do Azure."
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
ms.openlocfilehash: d37b53242c0b231d83425a59ecbe50216216a95b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="open-source-technologies-faqs-for-web-apps-in-azure"></a><span data-ttu-id="e52ba-103">Perguntas frequentes sobre tecnologias de código aberto para Aplicativos Web do Azure</span><span class="sxs-lookup"><span data-stu-id="e52ba-103">Open-source technologies FAQs for Web Apps in Azure</span></span>

<span data-ttu-id="e52ba-104">Este artigo apresenta perguntas frequentes (FAQs) sobre problemas com tecnologias de código aberto para a [funcionalidade do Aplicativos Web do Serviço de Aplicativo do Azure](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="e52ba-104">This article has answers to frequently asked questions (FAQs) about issues with open-source technologies for the [Web Apps feature of Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-cleardb-database-is-down-how-do-i-resolve-this"></a><span data-ttu-id="e52ba-105">Meu banco de dados ClearDB está inoperante.</span><span class="sxs-lookup"><span data-stu-id="e52ba-105">My ClearDB database is down.</span></span> <span data-ttu-id="e52ba-106">Como resolver isso?</span><span class="sxs-lookup"><span data-stu-id="e52ba-106">How do I resolve this?</span></span>

<span data-ttu-id="e52ba-107">Para problemas relacionados ao banco de dados, entre em contato com o [Suporte do ClearDB](https://www.cleardb.com/developers/help/support).</span><span class="sxs-lookup"><span data-stu-id="e52ba-107">For database-related issues, contact [ClearDB support](https://www.cleardb.com/developers/help/support).</span></span> 

<span data-ttu-id="e52ba-108">Para obter respostas a perguntas comuns sobre ClearDB, consulte [perguntas frequentes sobre ClearDB](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="e52ba-108">For answers to common questions about ClearDB, see [ClearDB FAQs](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="why-isnt-my-cleardb-database-listed-in-the-portal"></a><span data-ttu-id="e52ba-109">Por que meu banco de dados ClearDB não está listado no portal?</span><span class="sxs-lookup"><span data-stu-id="e52ba-109">Why isn't my ClearDB database listed in the portal?</span></span>

<span data-ttu-id="e52ba-110">Se você criar um banco de dados ClearDB no [portal do Azure](http://portal.azure.com/), o banco de dados não aparecerá no [portal clássico do Azure](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="e52ba-110">If you create a ClearDB database in the [Azure portal](http://portal.azure.com/), the database doesn't appear in the [Azure classic portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="e52ba-111">Para resolver esse problema, você pode vincular o banco de dados manualmente ao aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="e52ba-111">To work around this, you can manually link your database to the web app.</span></span>

<span data-ttu-id="e52ba-112">Da mesma forma, se você criar um banco de dados ClearDB no [portal clássico do Azure](http://manage.windowsazure.com/), você não verá o banco de dados no [portal do Azure](http://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e52ba-112">Similarly, if you create a ClearDB database in the [Azure classic portal](http://manage.windowsazure.com/),  you won't see your database in the [Azure portal](http://portal.azure.com/).</span></span> <span data-ttu-id="e52ba-113">Nesse caso, nenhuma solução alternativa está disponível.</span><span class="sxs-lookup"><span data-stu-id="e52ba-113">In this case, no workaround is available.</span></span> 

<span data-ttu-id="e52ba-114">Para mais informações, consulte [Perguntas frequentes sobre bancos de dados MySql do ClearDB com o Serviço de Aplicativo do Azure](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="e52ba-114">For more information, see [FAQs for ClearDB MySQL databases with Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="why-wasnt-my-cleardb-database-migrated-during-my-subscription-migration"></a><span data-ttu-id="e52ba-115">Por que meu banco de dados ClearDB não migrou durante a migração da minha assinatura?</span><span class="sxs-lookup"><span data-stu-id="e52ba-115">Why wasn't my ClearDB database migrated during my subscription migration?</span></span>

<span data-ttu-id="e52ba-116">Quando você executar recursos de migração entre assinaturas, serão aplicadas algumas limitações.</span><span class="sxs-lookup"><span data-stu-id="e52ba-116">When you perform resource migration across subscriptions, some limitations apply.</span></span> <span data-ttu-id="e52ba-117">O banco de dados MySQL ClearDB é um serviço de terceiros e, portanto, não será migrado durante a migração da assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="e52ba-117">A ClearDB MySQL database is a third-party service and is not migrated during an Azure subscription migration.</span></span>

<span data-ttu-id="e52ba-118">Se você não gerenciar a migração do banco de dados MySQL antes da migração de recursos do Azure, seus bancos de dados MySQL ClearDB poderão não estar disponíveis.</span><span class="sxs-lookup"><span data-stu-id="e52ba-118">If you don't manage the migration of your MySQL database before you migrate your Azure resources, your ClearDB MySQL database might be unavailable.</span></span> <span data-ttu-id="e52ba-119">Para evitar isso, primeiro, migre manualmente seu banco de dados ClearDB e, em seguida, migre a assinatura do Azure para seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="e52ba-119">To avoid this, first, manually migrate your ClearDB database, and then migrate the Azure subscription for your web app.</span></span>

<span data-ttu-id="e52ba-120">Para mais informações, consulte [Perguntas frequentes sobre bancos de dados MySql do ClearDB com o Serviço de Aplicativo do Azure](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="e52ba-120">For more information, see [FAQs for ClearDB MySQL databases with Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="how-do-i-turn-on-php-logging-to-troubleshoot-php-issues"></a><span data-ttu-id="e52ba-121">Como ativar registro em log PHP para solucionar problemas de PHP?</span><span class="sxs-lookup"><span data-stu-id="e52ba-121">How do I turn on PHP logging to troubleshoot PHP issues?</span></span>

<span data-ttu-id="e52ba-122">Para ativar o registro em log de PHP:</span><span class="sxs-lookup"><span data-stu-id="e52ba-122">To turn on PHP logging:</span></span>

1. <span data-ttu-id="e52ba-123">Entre no seu [site Kudu](https://*yourwebsitename*.scm.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="e52ba-123">Sign in to your [Kudu website](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
2. <span data-ttu-id="e52ba-124">No menu superior, selecione **Console de Depuração** > **CMD**.</span><span class="sxs-lookup"><span data-stu-id="e52ba-124">In the top menu, select **Debug Console** > **CMD**.</span></span>
3. <span data-ttu-id="e52ba-125">Selecione a pasta **Site**.</span><span class="sxs-lookup"><span data-stu-id="e52ba-125">Select the **Site** folder.</span></span>
4. <span data-ttu-id="e52ba-126">Selecione a pasta **wwwroot**.</span><span class="sxs-lookup"><span data-stu-id="e52ba-126">Select the **wwwroot** folder.</span></span>
5. <span data-ttu-id="e52ba-127">Selecione o  **+**  ícone e, em seguida, selecione **Novo arquivo**.</span><span class="sxs-lookup"><span data-stu-id="e52ba-127">Select the **+** icon, and then select **New File**.</span></span>
6. <span data-ttu-id="e52ba-128">Defina o nome de arquivo para **.user.ini**.</span><span class="sxs-lookup"><span data-stu-id="e52ba-128">Set the file name to **.user.ini**.</span></span>
7. <span data-ttu-id="e52ba-129">Selecione o ícone de lápis ao lado de **.user.ini**.</span><span class="sxs-lookup"><span data-stu-id="e52ba-129">Select the pencil icon next to **.user.ini**.</span></span>
8. <span data-ttu-id="e52ba-130">No arquivo, adicione este código:`log_errors=on`</span><span class="sxs-lookup"><span data-stu-id="e52ba-130">In the file, add this code: `log_errors=on`</span></span>
9. <span data-ttu-id="e52ba-131">Selecione **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="e52ba-131">Select **Save**.</span></span>
10. <span data-ttu-id="e52ba-132">Selecione o ícone de lápis ao lado de **wp-config.php**.</span><span class="sxs-lookup"><span data-stu-id="e52ba-132">Select the pencil icon next to **wp-config.php**.</span></span>
11. <span data-ttu-id="e52ba-133">Adicione o texto para o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="e52ba-133">Change the text to the following code:</span></span>
   ```
   //Enable WP_DEBUG modedefine('WP_DEBUG', true);//Enable debug logging to /wp-content/debug.logdefine('WP_DEBUG_LOG', true);
   //Supress errors and warnings to screendefine('WP_DEBUG_DISPLAY', false);//Supress PHP errors to screenini_set('display_errors', 0);
   ```
12. <span data-ttu-id="e52ba-134">No portal do Azure, no menu do aplicativo web, reinicie o aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="e52ba-134">In the Azure portal, in the web app menu, restart your web app.</span></span>

<span data-ttu-id="e52ba-135">Para obter mais informações, consulte [Habilitar logs de erros do WordPress](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span><span class="sxs-lookup"><span data-stu-id="e52ba-135">For more information, see [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span></span>

## <a name="how-do-i-log-python-application-errors-in-apps-that-are-hosted-in-app-service"></a><span data-ttu-id="e52ba-136">Como registrar erros do aplicativo Python em aplicativos que são hospedados no Serviço de Aplicativo?</span><span class="sxs-lookup"><span data-stu-id="e52ba-136">How do I log Python application errors in apps that are hosted in App Service?</span></span>

<span data-ttu-id="e52ba-137">Para capturar erros de aplicativo Python:</span><span class="sxs-lookup"><span data-stu-id="e52ba-137">To capture Python application errors:</span></span>

1. <span data-ttu-id="e52ba-138">No Portal do Azure, no seu aplicativo Web, selecione **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="e52ba-138">In the Azure portal, in your web app, select **Settings**.</span></span>
2. <span data-ttu-id="e52ba-139">Na guia **Configurações**, selecione **Configurações do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="e52ba-139">On the **Settings** tab, select **Application settings**.</span></span>
3. <span data-ttu-id="e52ba-140">Em **Configurações do aplicativo**, digite o seguinte par de chave/valor:</span><span class="sxs-lookup"><span data-stu-id="e52ba-140">Under **App settings**, enter the following key/value pair:</span></span>
    * <span data-ttu-id="e52ba-141">Chave: WSGI_LOG</span><span class="sxs-lookup"><span data-stu-id="e52ba-141">Key : WSGI_LOG</span></span>
    * <span data-ttu-id="e52ba-142">Valor: D:\home\site\wwwroot\logs.txt (Insira o nome de arquivo da sua escolha)</span><span class="sxs-lookup"><span data-stu-id="e52ba-142">Value : D:\home\site\wwwroot\logs.txt (enter your choice of file name)</span></span>

<span data-ttu-id="e52ba-143">Agora você verá erros no arquivo logs.txt na pasta wwwroot.</span><span class="sxs-lookup"><span data-stu-id="e52ba-143">You should now see errors in the logs.txt file in the wwwroot folder.</span></span>

## <a name="how-do-i-change-the-version-of-the-nodejs-application-that-is-hosted-in-app-service"></a><span data-ttu-id="e52ba-144">Como alterar a versão do aplicativo Node.js que está hospedado no Serviço de Aplicativo?</span><span class="sxs-lookup"><span data-stu-id="e52ba-144">How do I change the version of the Node.js application that is hosted in App Service?</span></span>

<span data-ttu-id="e52ba-145">Para alterar a versão do aplicativo Node.js, você pode usar uma das seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="e52ba-145">To change the version of the Node.js application, you can use one of the following options:</span></span>

*   <span data-ttu-id="e52ba-146">No portal do Azure, use **Configurações do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="e52ba-146">In the Azure portal, use **App settings**.</span></span>
    1. <span data-ttu-id="e52ba-147">No portal do Azure, vá para seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="e52ba-147">In the Azure portal, go to your web app.</span></span>
    2. <span data-ttu-id="e52ba-148">Na folha **Configurações**, selecione **Configurações do aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="e52ba-148">On the **Settings** blade, select **Application settings**.</span></span>
    3. <span data-ttu-id="e52ba-149">Em **Configurações do aplicativo**, você pode incluir WEBSITE_NODE_DEFAULT_VERSION como a chave e a versão do Node.js que desejar como o valor.</span><span class="sxs-lookup"><span data-stu-id="e52ba-149">In **App settings**, you can include WEBSITE_NODE_DEFAULT_VERSION as the key, and the version of Node.js you want as the value.</span></span>
    4. <span data-ttu-id="e52ba-150">Vá para o [console Kudu](https://*yourwebsitename*.scm.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="e52ba-150">Go to your [Kudu console](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
    5. <span data-ttu-id="e52ba-151">Para verificar a versão do Node.js, digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="e52ba-151">To check the Node.js version, enter the following command:</span></span>  
   ```
   node -v
   ```
*   <span data-ttu-id="e52ba-152">Modificar o arquivo iisnode.yml.</span><span class="sxs-lookup"><span data-stu-id="e52ba-152">Modify the iisnode.yml file.</span></span> <span data-ttu-id="e52ba-153">Alterar a versão do Node.js no arquivo iisnode.yml apenas define o ambiente de tempo de execução que iisnode usa.</span><span class="sxs-lookup"><span data-stu-id="e52ba-153">Changing the Node.js version in the iisnode.yml file only sets the runtime environment that iisnode uses.</span></span> <span data-ttu-id="e52ba-154">O Kudu cmd e outros ainda usam a versão de Node.js que está definida em **Configurações do aplicativo** no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e52ba-154">Your Kudu cmd and others still use the Node.js version that is set in **App settings** in the Azure portal.</span></span>

    <span data-ttu-id="e52ba-155">Para definir o iisnode.yml manualmente, crie um arquivo de iisnode.yml na pasta raiz do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e52ba-155">To set the iisnode.yml manually, create an iisnode.yml file in your app root folder.</span></span> <span data-ttu-id="e52ba-156">No arquivo, inclua a seguinte linha:</span><span class="sxs-lookup"><span data-stu-id="e52ba-156">In the file, include the following line:</span></span>
   ```
   nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
   ```
   
*   <span data-ttu-id="e52ba-157">Defina o arquivo de iisnode.yml usando package.json durante a implantação do controle do código fonte.</span><span class="sxs-lookup"><span data-stu-id="e52ba-157">Set the iisnode.yml file by using package.json during source control deployment.</span></span>
    <span data-ttu-id="e52ba-158">O processo de implantação de controle do código-fonte do Azure envolve as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="e52ba-158">The Azure source control deployment process involves the following steps:</span></span>
    1. <span data-ttu-id="e52ba-159">Mova o conteúdo do aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="e52ba-159">Moves content to the Azure web app.</span></span>
    2. <span data-ttu-id="e52ba-160">Crie um script de implantação padrão, se não houver um (arquivos deploy.cmd, .deployment) na pasta raiz de aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="e52ba-160">Creates a default deployment script, if there isn’t one (deploy.cmd, .deployment files) in the web app root folder.</span></span>
    3. <span data-ttu-id="e52ba-161">Execute um script de implantação em que ele cria um arquivo iisnode.yml se mencionar a versão do Node.js no arquivo package.json > mecanismo`"engines": {"node": "5.9.1","npm": "3.7.3"}`</span><span class="sxs-lookup"><span data-stu-id="e52ba-161">Runs a deployment script in which it creates an iisnode.yml file if you mention the Node.js version in the package.json file > engine `"engines": {"node": "5.9.1","npm": "3.7.3"}`</span></span>
    4. <span data-ttu-id="e52ba-162">O arquivo iisnode.yml tem a seguinte linha de código:</span><span class="sxs-lookup"><span data-stu-id="e52ba-162">The iisnode.yml file has the following line of code:</span></span>
        ```
        nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
        ```

## <a name="i-see-the-message-error-establishing-a-database-connection-in-my-wordpress-app-thats-hosted-in-app-service-how-do-i-troubleshoot-this"></a><span data-ttu-id="e52ba-163">É exibida a mensagem "Erro ao estabelecer uma conexão de banco de dados" em meu aplicativo de WordPress que está hospedado no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e52ba-163">I see the message "Error establishing a database connection" in my WordPress app that's hosted in App Service.</span></span> <span data-ttu-id="e52ba-164">Como solucionar isso?</span><span class="sxs-lookup"><span data-stu-id="e52ba-164">How do I troubleshoot this?</span></span>

<span data-ttu-id="e52ba-165">Se você vir esse erro em seu aplicativo WordPress do Azure, para permitir php_errors.log e debug.log, conclua as etapas detalhadas em [Habilitar logs de erros do WordPress](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span><span class="sxs-lookup"><span data-stu-id="e52ba-165">If you see this error in your Azure WordPress app, to enable php_errors.log and debug.log, complete the steps detailed in [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span></span>

<span data-ttu-id="e52ba-166">Quando os logs estão habilitados, reproduza o erro e, em seguida, verifique os logs para ver se você está executando sem conexões:</span><span class="sxs-lookup"><span data-stu-id="e52ba-166">When the logs are enabled, reproduce the error, and then check the logs to see if you are running out of connections:</span></span>
```
[09-Oct-2015 00:03:13 UTC] PHP Warning: mysqli_real_connect(): (HY000/1226): User ‘abcdefghijk79' has exceeded the ‘max_user_connections’ resource (current value: 4) in D:\home\site\wwwroot\wp-includes\wp-db.php on line 1454
```

<span data-ttu-id="e52ba-167">Se você vir esse erro nos arquivos de debug.log ou php_errors.log, seu aplicativo está excedendo o número de conexões.</span><span class="sxs-lookup"><span data-stu-id="e52ba-167">If you see this error in your debug.log or php_errors.log files, your app is exceeding the number of connections.</span></span> <span data-ttu-id="e52ba-168">Se você estiver hospedando no ClearDB, verifique o número de conexões que estão disponíveis no seu [plano de serviço](https://www.cleardb.com/pricing.view).</span><span class="sxs-lookup"><span data-stu-id="e52ba-168">If you’re hosting on ClearDB, verify the number of connections that are available in your [service plan](https://www.cleardb.com/pricing.view).</span></span>

## <a name="how-do-i-debug-a-nodejs-app-thats-hosted-in-app-service"></a><span data-ttu-id="e52ba-169">Como depurar um aplicativo Node.js que está hospedado no Serviço de Aplicativo?</span><span class="sxs-lookup"><span data-stu-id="e52ba-169">How do I debug a Node.js app that's hosted in App Service?</span></span>

1.  <span data-ttu-id="e52ba-170">Vá para o [console Kudu](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).</span><span class="sxs-lookup"><span data-stu-id="e52ba-170">Go to your [Kudu console](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).</span></span>
2.  <span data-ttu-id="e52ba-171">Vá para a pasta de logs de aplicativo (D:\home\LogFiles\Application).</span><span class="sxs-lookup"><span data-stu-id="e52ba-171">Go to your application logs folder (D:\home\LogFiles\Application).</span></span>
3.  <span data-ttu-id="e52ba-172">No arquivo logging_errors.txt, verifique se há conteúdo.</span><span class="sxs-lookup"><span data-stu-id="e52ba-172">In the logging_errors.txt file, check for content.</span></span>

## <a name="how-do-i-install-native-python-modules-in-an-app-service-web-app-or-api-app"></a><span data-ttu-id="e52ba-173">Como instalar módulos Python nativos em um aplicativo web do Serviço de Aplicativo ou aplicativo de API?</span><span class="sxs-lookup"><span data-stu-id="e52ba-173">How do I install native Python modules in an App Service web app or API app?</span></span>

<span data-ttu-id="e52ba-174">Alguns pacotes não podem ser instalados usando o pip no Azure.</span><span class="sxs-lookup"><span data-stu-id="e52ba-174">Some packages might not install by using pip in Azure.</span></span> <span data-ttu-id="e52ba-175">O pacote não pode estar disponível no índice de pacote do Python ou um compilador pode ser necessário (um compilador não está disponível no computador que está executando o aplicativo web no Serviço de Aplicativo).</span><span class="sxs-lookup"><span data-stu-id="e52ba-175">The package might not be available on the Python Package Index, or a compiler might be required (a compiler is not available on the computer that is running the web app in App Service).</span></span> <span data-ttu-id="e52ba-176">Para obter informações sobre como instalar os módulos nativos em aplicativos web do Serviço de Aplicativo e aplicativos de API, consulte [Instalar módulos Python no Serviço de Aplicativo](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/).</span><span class="sxs-lookup"><span data-stu-id="e52ba-176">For information about installing native modules in App Service web apps and API apps, see [Install Python modules in App Service](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/).</span></span>

## <a name="how-do-i-deploy-a-django-app-to-app-service-by-using-git-and-the-new-version-of-python"></a><span data-ttu-id="e52ba-177">Como implantar um aplicativo de Django para o Serviço de Aplicativo usando o Git e a nova versão do Python?</span><span class="sxs-lookup"><span data-stu-id="e52ba-177">How do I deploy a Django app to App Service by using Git and the new version of Python?</span></span>

<span data-ttu-id="e52ba-178">Para obter informações sobre como instalar Django, consulte [Implantando um aplicativo Django para o Serviço de Aplicativo](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).</span><span class="sxs-lookup"><span data-stu-id="e52ba-178">For information about installing Django, see [Deploying a Django app to App Service](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).</span></span>

## <a name="where-are-the-tomcat-log-files-located"></a><span data-ttu-id="e52ba-179">Onde estão localizados os arquivos de log do Tomcat?</span><span class="sxs-lookup"><span data-stu-id="e52ba-179">Where are the Tomcat log files located?</span></span>

<span data-ttu-id="e52ba-180">Para o Azure Marketplace e implantações personalizadas:</span><span class="sxs-lookup"><span data-stu-id="e52ba-180">For Azure Marketplace and custom deployments:</span></span>

* <span data-ttu-id="e52ba-181">Local da pasta: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs</span><span class="sxs-lookup"><span data-stu-id="e52ba-181">Folder location: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs</span></span>
* <span data-ttu-id="e52ba-182">Arquivos de interesse:</span><span class="sxs-lookup"><span data-stu-id="e52ba-182">Files of interest:</span></span>
    * <span data-ttu-id="e52ba-183">catalina.*aaaa-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="e52ba-183">catalina.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="e52ba-184">host-manager.*aaaa-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="e52ba-184">host-manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="e52ba-185">localhost.*aaaa-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="e52ba-185">localhost.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="e52ba-186">manager.*aaaa-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="e52ba-186">manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="e52ba-187">site_access_log.*yyyy-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="e52ba-187">site_access_log.*yyyy-mm-dd*.log</span></span>


<span data-ttu-id="e52ba-188">Para implantações de **Configurações do aplicativo** do portal:</span><span class="sxs-lookup"><span data-stu-id="e52ba-188">For portal **App settings** deployments:</span></span>

* <span data-ttu-id="e52ba-189">Local da pasta: D:\home\LogFiles</span><span class="sxs-lookup"><span data-stu-id="e52ba-189">Folder location: D:\home\LogFiles</span></span>
* <span data-ttu-id="e52ba-190">Arquivos de interesse:</span><span class="sxs-lookup"><span data-stu-id="e52ba-190">Files of interest:</span></span>
    * <span data-ttu-id="e52ba-191">catalina.*aaaa-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="e52ba-191">catalina.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="e52ba-192">host-manager.*aaaa-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="e52ba-192">host-manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="e52ba-193">localhost.*aaaa-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="e52ba-193">localhost.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="e52ba-194">manager.*aaaa-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="e52ba-194">manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="e52ba-195">site_access_log.*yyyy-mm-dd*.log</span><span class="sxs-lookup"><span data-stu-id="e52ba-195">site_access_log.*yyyy-mm-dd*.log</span></span>

## <a name="how-do-i-troubleshoot-jdbc-driver-connection-errors"></a><span data-ttu-id="e52ba-196">Como solucionar problemas de erros de conexão do driver JDBC?</span><span class="sxs-lookup"><span data-stu-id="e52ba-196">How do I troubleshoot JDBC driver connection errors?</span></span>

<span data-ttu-id="e52ba-197">Você verá a seguinte mensagem nos seus logs Tomcat:</span><span class="sxs-lookup"><span data-stu-id="e52ba-197">You might see the following message in your Tomcat logs:</span></span>

```
The web application[ROOT] registered the JDBC driver [com.mysql.jdbc.Driver] but failed to unregister it when the web application was stopped. To prevent a memory leak,the JDBC Driver has been forcibly unregistered
```

<span data-ttu-id="e52ba-198">Para resolver o erro:</span><span class="sxs-lookup"><span data-stu-id="e52ba-198">To resolve the error:</span></span>

1. <span data-ttu-id="e52ba-199">Remova o arquivo sqljdbc*.jar da pasta do app/lib.</span><span class="sxs-lookup"><span data-stu-id="e52ba-199">Remove the sqljdbc*.jar file from your app/lib folder.</span></span>
2. <span data-ttu-id="e52ba-200">Se você estiver usando o servidor web Tomcat personalizado ou o Azure Marketplace Tomcat, copie esse arquivo. jar para a pasta lib Tomcat.</span><span class="sxs-lookup"><span data-stu-id="e52ba-200">If you are using the custom Tomcat or Azure Marketplace Tomcat web server, copy this .jar file to the Tomcat lib folder.</span></span>
3. <span data-ttu-id="e52ba-201">Se você estiver habilitando Java do portal do Azure (selecione **Java 1.8** > **servidor Tomcat**), copie o arquivo jar sqljdbc.* na pasta que é paralela ao seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e52ba-201">If you are enabling Java from the Azure portal (select **Java 1.8** > **Tomcat server**), copy the sqljdbc.* jar file in the folder that's parallel to your app.</span></span> <span data-ttu-id="e52ba-202">Em seguida, adicione a seguinte configuração de classpath para o arquivo web.config:</span><span class="sxs-lookup"><span data-stu-id="e52ba-202">Then, add the following classpath setting to the web.config file:</span></span>

    ```
    <httpPlatform>
    <environmentVariables>
    <environmentVariablename ="JAVA_OPTS" value=" -Djava.net.preferIPv4Stack=true
    -Xms128M -classpath %CLASSPATH%;[Path to the sqljdbc*.jarfile]" />
    </environmentVariables>
    </httpPlatform>
    ```

## <a name="why-do-i-see-errors-when-i-attempt-to-copy-live-log-files"></a><span data-ttu-id="e52ba-203">Por que vejo erros ao tentar copiar os arquivos de log em tempo real?</span><span class="sxs-lookup"><span data-stu-id="e52ba-203">Why do I see errors when I attempt to copy live log files?</span></span>

<span data-ttu-id="e52ba-204">Se você tentar copiar arquivos de log em tempo real para um aplicativo Java (por exemplo, Tomcat), você poderá ver esse erro FTP:</span><span class="sxs-lookup"><span data-stu-id="e52ba-204">If you try to copy live log files for a Java app (for example, Tomcat), you might see this FTP error:</span></span>

```
Error transferring file [filename] Copying files from remote side failed.
    
The process cannot access the file because it is being used by another process.
```

<span data-ttu-id="e52ba-205">A mensagem de erro pode variar, dependendo do cliente FTP.</span><span class="sxs-lookup"><span data-stu-id="e52ba-205">The error message might vary, depending on the FTP client.</span></span>

<span data-ttu-id="e52ba-206">Todos os aplicativos Java tem esse problema de bloqueio.</span><span class="sxs-lookup"><span data-stu-id="e52ba-206">All Java apps have this locking issue.</span></span> <span data-ttu-id="e52ba-207">Apenas o Kudu oferece suporte para baixar este arquivo enquanto o aplicativo está em execução.</span><span class="sxs-lookup"><span data-stu-id="e52ba-207">Only Kudu supports downloading this file while the app is running.</span></span>

<span data-ttu-id="e52ba-208">Parar o aplicativo permite o acesso ao FTP para esses arquivos.</span><span class="sxs-lookup"><span data-stu-id="e52ba-208">Stopping the app allows FTP access to these files.</span></span>

<span data-ttu-id="e52ba-209">Outra solução alternativa é gravar um WebJob que é executado em um agendamento e copiá-los para um diretório diferente.</span><span class="sxs-lookup"><span data-stu-id="e52ba-209">Another workaround is to write a WebJob that runs on a schedule and copies these files to a different directory.</span></span> <span data-ttu-id="e52ba-210">Para um projeto de exemplo, consulte o projeto [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob).</span><span class="sxs-lookup"><span data-stu-id="e52ba-210">For a sample project, see the [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob) project.</span></span>

## <a name="where-do-i-find-the-log-files-for-jetty"></a><span data-ttu-id="e52ba-211">Onde encontrar os arquivos de log para Jetty?</span><span class="sxs-lookup"><span data-stu-id="e52ba-211">Where do I find the log files for Jetty?</span></span>

<span data-ttu-id="e52ba-212">Para o Marketplace e implantações personalizadas, o arquivo de log está na pasta D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs.</span><span class="sxs-lookup"><span data-stu-id="e52ba-212">For Marketplace and custom deployments, the log file is in the D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs folder.</span></span> <span data-ttu-id="e52ba-213">Observe que o local da pasta depende da versão do Jetty que você está usando.</span><span class="sxs-lookup"><span data-stu-id="e52ba-213">Note that the folder location depends on the version of Jetty you are using.</span></span> <span data-ttu-id="e52ba-214">Por exemplo, o caminho fornecido aqui é para Jetty 9.1.2.</span><span class="sxs-lookup"><span data-stu-id="e52ba-214">For example, the path provided here is for Jetty 9.1.2.</span></span> <span data-ttu-id="e52ba-215">Procure jetty_*YYYY_MM_DD*.stderrout.log.</span><span class="sxs-lookup"><span data-stu-id="e52ba-215">Look for jetty_*YYYY_MM_DD*.stderrout.log.</span></span>

<span data-ttu-id="e52ba-216">Para implantações de Configuração do aplicativo do portal, o arquivo de log está em D:\home\LogFiles.</span><span class="sxs-lookup"><span data-stu-id="e52ba-216">For portal App Setting deployments, the log file is in D:\home\LogFiles.</span></span> <span data-ttu-id="e52ba-217">Procure jetty_*YYYY_MM_DD*.stderrout.log</span><span class="sxs-lookup"><span data-stu-id="e52ba-217">Look for jetty_*YYYY_MM_DD*.stderrout.log</span></span>

## <a name="can-i-send-email-from-my-azure-web-app"></a><span data-ttu-id="e52ba-218">Posso enviar email de meu aplicativo web do Azure?</span><span class="sxs-lookup"><span data-stu-id="e52ba-218">Can I send email from my Azure web app?</span></span>

<span data-ttu-id="e52ba-219">Serviço de Aplicativo não tem uma funcionalidade de email interno.</span><span class="sxs-lookup"><span data-stu-id="e52ba-219">App Service doesn't have a built-in email feature.</span></span> <span data-ttu-id="e52ba-220">Para algumas boas alternativas para enviar email de seu aplicativo, consulte esta [Discussão de Stack Overflow](http://stackoverflow.com/questions/17666161/sending-email-from-azure).</span><span class="sxs-lookup"><span data-stu-id="e52ba-220">For some good alternatives for sending email from your app, see this [Stack Overflow discussion](http://stackoverflow.com/questions/17666161/sending-email-from-azure).</span></span>

## <a name="why-does-my-wordpress-site-redirect-to-another-url"></a><span data-ttu-id="e52ba-221">Por que meu site WordPress redireciona para outra URL?</span><span class="sxs-lookup"><span data-stu-id="e52ba-221">Why does my WordPress site redirect to another URL?</span></span>

<span data-ttu-id="e52ba-222">Se você ter migrado recentemente no Azure, WordPress pode redirecionar para a URL do domínio antigo.</span><span class="sxs-lookup"><span data-stu-id="e52ba-222">If you have recently migrated to Azure, WordPress might redirect to the old domain URL.</span></span> <span data-ttu-id="e52ba-223">Isso é causado por uma configuração no banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="e52ba-223">This is caused by a setting in the MySQL database.</span></span>

<span data-ttu-id="e52ba-224">WordPress Buddy + é uma extensão de Site do Azure que você pode usar para atualizar a URL de redirecionamento diretamente no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e52ba-224">WordPress Buddy+ is an Azure Site Extension that you can use to update the redirection URL directly in the database.</span></span> <span data-ttu-id="e52ba-225">Para obter mais informações sobre como usar o WordPress Buddy +, consulte [Ferramentas WordPress e migração do MySQL com WordPress Buddy +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span><span class="sxs-lookup"><span data-stu-id="e52ba-225">For more information about using WordPress Buddy+, see [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

<span data-ttu-id="e52ba-226">Como alternativa, se você preferir atualizar manualmente o redirecionamento de URL usando consultas SQL ou PHPMyAdmin, consulte [WordPress: Redirecionamento de URL errado](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/).</span><span class="sxs-lookup"><span data-stu-id="e52ba-226">Alternatively, if you prefer to manually update the redirection URL by using SQL queries or PHPMyAdmin, see [WordPress: Redirecting to wrong URL](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/).</span></span>

## <a name="how-do-i-change-my-wordpress-sign-in-password"></a><span data-ttu-id="e52ba-227">Como alterar minha senha de logon do WordPress?</span><span class="sxs-lookup"><span data-stu-id="e52ba-227">How do I change my WordPress sign-in password?</span></span>

<span data-ttu-id="e52ba-228">Se você esqueceu sua senha de logon do WordPress, você pode usar WordPress Buddy + para atualizá-la.</span><span class="sxs-lookup"><span data-stu-id="e52ba-228">If you have forgotten your WordPress sign-in password, you can use WordPress Buddy+ to update it.</span></span> <span data-ttu-id="e52ba-229">Para redefinir sua senha, instale a extensão do Azure Site WordPress Buddy + e, em seguida, conclua as etapas descritas em [Ferramentas WordPress e migração do MySQL com WordPress Buddy +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span><span class="sxs-lookup"><span data-stu-id="e52ba-229">To reset your password, install the WordPress Buddy+ Azure Site Extension, and then complete the steps described in [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

## <a name="i-cant-sign-in-to-wordpress-how-do-i-resolve-this"></a><span data-ttu-id="e52ba-230">Não consigo entrar WordPress.</span><span class="sxs-lookup"><span data-stu-id="e52ba-230">I can't sign in to WordPress.</span></span> <span data-ttu-id="e52ba-231">Como resolver isso?</span><span class="sxs-lookup"><span data-stu-id="e52ba-231">How do I resolve this?</span></span>

<span data-ttu-id="e52ba-232">Se você estiver o WordPress bloqueado depois de instalar recentemente um plug-in, você pode ter um plug-in com defeito.</span><span class="sxs-lookup"><span data-stu-id="e52ba-232">If you find yourself locked out of WordPress after recently installing a plugin, you might have a faulty plugin.</span></span> <span data-ttu-id="e52ba-233">WordPress Buddy + é uma extensão de Site do Azure que podem ajudá-lo desabilitar plug-ins no WordPress.</span><span class="sxs-lookup"><span data-stu-id="e52ba-233">WordPress Buddy+ is an Azure Site Extension that can help you disable plugins in WordPress.</span></span> <span data-ttu-id="e52ba-234">Para obter mais informações, consulte [Ferramentas WordPress e migração do MySQL com WordPress Buddy +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span><span class="sxs-lookup"><span data-stu-id="e52ba-234">For more information, see [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

## <a name="how-do-i-migrate-my-wordpress-database"></a><span data-ttu-id="e52ba-235">Como migrar meu banco de dados do WordPress?</span><span class="sxs-lookup"><span data-stu-id="e52ba-235">How do I migrate my WordPress database?</span></span>

<span data-ttu-id="e52ba-236">Você tem várias opções para migrar o banco de dados MySQL que está conectado ao seu site de WordPress:</span><span class="sxs-lookup"><span data-stu-id="e52ba-236">You have multiple options for migrating the MySQL database that's connected to your WordPress website:</span></span>

* <span data-ttu-id="e52ba-237">Desenvolvedores: Usar o [prompt de comando ou PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)</span><span class="sxs-lookup"><span data-stu-id="e52ba-237">Developers: Use the [command prompt or PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)</span></span>
* <span data-ttu-id="e52ba-238">Não-desenvolvedores: Usar [WordPress Buddy +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)</span><span class="sxs-lookup"><span data-stu-id="e52ba-238">Non-developers: Use [WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)</span></span>

## <a name="how-do-i-help-make-wordpress-more-secure"></a><span data-ttu-id="e52ba-239">Como ajudar a proteger melhor o WordPress?</span><span class="sxs-lookup"><span data-stu-id="e52ba-239">How do I help make WordPress more secure?</span></span>

<span data-ttu-id="e52ba-240">Para saber mais sobre práticas recomendadas de segurança para WordPress, consulte [Práticas recomendadas para segurança do WordPress no Azure](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).</span><span class="sxs-lookup"><span data-stu-id="e52ba-240">To learn about security best practices for WordPress, see [Best practices for WordPress security in Azure](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).</span></span>

## <a name="i-am-trying-to-use-phpmyadmin-and-i-see-the-message-access-denied-how-do-i-resolve-this"></a><span data-ttu-id="e52ba-241">Estou tentando usar PHPMyAdmin e é exibida a mensagem "Acesso negado."</span><span class="sxs-lookup"><span data-stu-id="e52ba-241">I am trying to use PHPMyAdmin, and I see the message “Access denied.”</span></span> <span data-ttu-id="e52ba-242">Como resolver isso?</span><span class="sxs-lookup"><span data-stu-id="e52ba-242">How do I resolve this?</span></span>

<span data-ttu-id="e52ba-243">Se a funcionalidade do MySQL no aplicativo não estiver em execução ainda nesta instância do Serviço de Aplicativo, você poderá enfrentar esse problema.</span><span class="sxs-lookup"><span data-stu-id="e52ba-243">You might experience this issue if the MySQL in-app feature isn't running yet in this App Service instance.</span></span> <span data-ttu-id="e52ba-244">Para resolver o problema, tente acessar o site.</span><span class="sxs-lookup"><span data-stu-id="e52ba-244">To resolve the issue, try to access your website.</span></span> <span data-ttu-id="e52ba-245">Isso inicia os processos necessários, incluindo o processo do MySQL no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e52ba-245">This starts the required processes, including the MySQL in-app process.</span></span> <span data-ttu-id="e52ba-246">Para verificar se MySQL no aplicativo está em execução, no Process Explorer, certifique-se de que mysqld.exe está listado nos processos.</span><span class="sxs-lookup"><span data-stu-id="e52ba-246">To verify that MySQL in-app is running, in Process Explorer, ensure that mysqld.exe is listed in the processes.</span></span>

<span data-ttu-id="e52ba-247">Depois de garantir que MySQL no aplicativo está em execução, tente usar PHPMyAdmin.</span><span class="sxs-lookup"><span data-stu-id="e52ba-247">After you ensure that MySQL in-app is running, try to use PHPMyAdmin.</span></span>

## <a name="i-get-an-http-403-error-when-i-try-to-import-or-export-my-mysql-in-app-database-by-using-phpmyadmin-how-do-i-resolve-this"></a><span data-ttu-id="e52ba-248">Recebo um erro de HTTP 403 ao tentar importar ou exportar meu banco de dados MySQL no aplicativo usando PHPMyadmin.</span><span class="sxs-lookup"><span data-stu-id="e52ba-248">I get an HTTP 403 error when I try to import or export my MySQL in-app database by using PHPMyadmin.</span></span> <span data-ttu-id="e52ba-249">Como resolver isso?</span><span class="sxs-lookup"><span data-stu-id="e52ba-249">How do I resolve this?</span></span>

<span data-ttu-id="e52ba-250">Se você estiver usando uma versão mais antiga do Chrome, talvez você esteja tendo um bug conhecido.</span><span class="sxs-lookup"><span data-stu-id="e52ba-250">If you are using an older version of Chrome, you might be experiencing a known bug.</span></span> <span data-ttu-id="e52ba-251">Para resolver o problema, atualize para uma versão mais recente do Chrome.</span><span class="sxs-lookup"><span data-stu-id="e52ba-251">To resolve the issue, upgrade to a newer version of Chrome.</span></span> <span data-ttu-id="e52ba-252">Além disso, tente usar um navegador diferente, como o Internet Explorer ou Edge, onde o problema não ocorre.</span><span class="sxs-lookup"><span data-stu-id="e52ba-252">Also try using a different browser, like Internet Explorer or Edge, where the issue does not occur.</span></span>
