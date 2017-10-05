---
title: "Configurar aplicativos Web no Serviço de Aplicativo do Azure"
description: "Como configurar um aplicativo Web nos Serviços de Aplicativos do Azure"
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9af8a367-7d39-4399-9941-b80cbc5f39a0
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: cacbcf879555907f81d824dc1069b05579dca010
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-web-apps-in-azure-app-service"></a><span data-ttu-id="75e15-103">Configurar aplicativos Web no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="75e15-103">Configure web apps in Azure App Service</span></span>
<span data-ttu-id="75e15-104">Este tópico explica como configurar um aplicativo Web usando o [Portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="75e15-104">This topic explains how to configure a web app using the [Azure Portal].</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="application-settings"></a><span data-ttu-id="75e15-105">Configurações do aplicativo</span><span class="sxs-lookup"><span data-stu-id="75e15-105">Application settings</span></span>
1. <span data-ttu-id="75e15-106">No [Portal do Azure], abra a folha do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="75e15-106">In the [Azure Portal], open the blade for the web app.</span></span>
2. <span data-ttu-id="75e15-107">Clique em **Todas as Configurações**.</span><span class="sxs-lookup"><span data-stu-id="75e15-107">Click **All Settings**.</span></span>
3. <span data-ttu-id="75e15-108">Clique em **Configurações do Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="75e15-108">Click **Application Settings**.</span></span>

![Configurações do aplicativo][configure01]

<span data-ttu-id="75e15-110">A folha **Configurações do aplicativo** tem configurações agrupadas em várias categorias.</span><span class="sxs-lookup"><span data-stu-id="75e15-110">The **Application settings** blade has settings grouped under several categories.</span></span>

### <a name="general-settings"></a><span data-ttu-id="75e15-111">Configurações gerais</span><span class="sxs-lookup"><span data-stu-id="75e15-111">General settings</span></span>
<span data-ttu-id="75e15-112">**Versão do Framework**.</span><span class="sxs-lookup"><span data-stu-id="75e15-112">**Framework versions**.</span></span> <span data-ttu-id="75e15-113">Configurar essas opções se seu aplicativo usa qualquer um desses frameworks:</span><span class="sxs-lookup"><span data-stu-id="75e15-113">Set these options if your app uses any these frameworks:</span></span> 

* <span data-ttu-id="75e15-114">**.NET Framework**: configure a versão do .NET framework.</span><span class="sxs-lookup"><span data-stu-id="75e15-114">**.NET Framework**: Set the .NET framework version.</span></span> 
* <span data-ttu-id="75e15-115">**PHP**: defina a versão do PHP ou **DESATIVADO** para desabilitar o PHP.</span><span class="sxs-lookup"><span data-stu-id="75e15-115">**PHP**: Set the PHP version, or **OFF** to disable PHP.</span></span> 
* <span data-ttu-id="75e15-116">**Java**: selecione a versão do Java ou **DESATIVADO** para desabilitar o Java.</span><span class="sxs-lookup"><span data-stu-id="75e15-116">**Java**: Select the Java version or **OFF** to disable Java.</span></span> <span data-ttu-id="75e15-117">Use a opção **Contêiner da Web** para escolher entre as versões do Tomcat e Jetty.</span><span class="sxs-lookup"><span data-stu-id="75e15-117">Use the **Web Container** option to choose between Tomcat and Jetty versions.</span></span>
* <span data-ttu-id="75e15-118">**Python**: selecione a versão do Python ou **DESATIVADO** para desabilitar o Python.</span><span class="sxs-lookup"><span data-stu-id="75e15-118">**Python**: Select the Python version, or **OFF** to disable Python.</span></span>

<span data-ttu-id="75e15-119">Por razões técnicas, a habilitação do Java para seu aplicativo desabilita as opções .NET, PHP e Python.</span><span class="sxs-lookup"><span data-stu-id="75e15-119">For technical reasons, enabling Java for your app disables the .NET, PHP, and Python options.</span></span>

<span data-ttu-id="75e15-120"><a name="platform"></a>
**Plataforma**.</span><span class="sxs-lookup"><span data-stu-id="75e15-120"><a name="platform"></a>
**Platform**.</span></span> <span data-ttu-id="75e15-121">Seleciona se o seu aplicativo é executado em ambiente de 32 ou 64 bits.</span><span class="sxs-lookup"><span data-stu-id="75e15-121">Selects whether your web app runs in a 32-bit or 64-bit environment.</span></span> <span data-ttu-id="75e15-122">O ambiente de 64-bit requere o modo Básico ou Padrão.</span><span class="sxs-lookup"><span data-stu-id="75e15-122">The 64-bit environment requires Basic or Standard mode.</span></span> <span data-ttu-id="75e15-123">Modos Livre e Compartilhado são sempre executados em um ambiente de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="75e15-123">Free and Shared modes always run in a 32-bit environment.</span></span>

<span data-ttu-id="75e15-124">**Web Sockets**.</span><span class="sxs-lookup"><span data-stu-id="75e15-124">**Web Sockets**.</span></span> <span data-ttu-id="75e15-125">Defina a opção como **ATIVADO** para habilitar o protocolo WebSocket; por exemplo, se seu aplicativo Web usar [ASP.NET SignalR] ou [socket.io].</span><span class="sxs-lookup"><span data-stu-id="75e15-125">Set **ON** to enable the WebSocket protocol; for example, if your web app uses [ASP.NET SignalR] or [socket.io].</span></span>

<span data-ttu-id="75e15-126"><a name="alwayson"></a>
**Sempre ativado**.</span><span class="sxs-lookup"><span data-stu-id="75e15-126"><a name="alwayson"></a>
**Always On**.</span></span> <span data-ttu-id="75e15-127">Por padrão, os aplicativos Web serão descarregados se estiverem ociosos por um determinado período de tempo.</span><span class="sxs-lookup"><span data-stu-id="75e15-127">By default, web apps are unloaded if they are idle for some period of time.</span></span> <span data-ttu-id="75e15-128">Isso permite ao sistema conservar recursos.</span><span class="sxs-lookup"><span data-stu-id="75e15-128">This lets the system conserve resources.</span></span> <span data-ttu-id="75e15-129">No modo Básico ou Padrão, você pode habilitar a opção **Sempre Ativado** para manter o aplicativo carregado o tempo todo.</span><span class="sxs-lookup"><span data-stu-id="75e15-129">In Basic or Standard mode, you can enable **Always On** to keep the app loaded all the time.</span></span> <span data-ttu-id="75e15-130">Se o aplicativo executar WebJobs contínuos ou executar WebJobs disparados com uma expressão CRON, você deverá habilitar a opção **Sempre ativo** ou os trabalhos Web poderão não ser executados de forma confiável.</span><span class="sxs-lookup"><span data-stu-id="75e15-130">If your app runs continuous WebJobs or runs WebJobs triggered using a CRON expression, you should enable **Always On**, or the web jobs may not run reliably.</span></span>

<span data-ttu-id="75e15-131">**Versão do Pipeline Gerenciado**.</span><span class="sxs-lookup"><span data-stu-id="75e15-131">**Managed Pipeline Version**.</span></span> <span data-ttu-id="75e15-132">Configurar o IIS [modo de pipeline].</span><span class="sxs-lookup"><span data-stu-id="75e15-132">Sets the IIS [pipeline mode].</span></span> <span data-ttu-id="75e15-133">Deixar este conjunto como Integrado (o padrão), a menos que você tenha um aplicativo herdado que exija uma versão anterior do IIS.</span><span class="sxs-lookup"><span data-stu-id="75e15-133">Leave this set to Integrated (the default) unless you have a legacy app that requires an older version of IIS.</span></span>

<span data-ttu-id="75e15-134">**Troca Automática**.</span><span class="sxs-lookup"><span data-stu-id="75e15-134">**Auto Swap**.</span></span> <span data-ttu-id="75e15-135">Se você habilitar a Troca Automática para um slot de implantação, o Serviço de Aplicativo alternará automaticamente o aplicativo Web em produção quando você enviar uma atualização por push para esse slot.</span><span class="sxs-lookup"><span data-stu-id="75e15-135">If you enable Auto Swap for a deployment slot, App Service will automatically swap the web app into production when you push an update to that slot.</span></span> <span data-ttu-id="75e15-136">Para saber mais, consulte [Implantar em slots de preparo para aplicativos Web no Serviço de Aplicativo do Azure](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="75e15-136">For more information, see [Deploy to staging slots for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span>

### <a name="debugging"></a><span data-ttu-id="75e15-137">Depurando</span><span class="sxs-lookup"><span data-stu-id="75e15-137">Debugging</span></span>
<span data-ttu-id="75e15-138">**Depuração Remota**.</span><span class="sxs-lookup"><span data-stu-id="75e15-138">**Remote Debugging**.</span></span> <span data-ttu-id="75e15-139">Habilita a depuração remota.</span><span class="sxs-lookup"><span data-stu-id="75e15-139">Enables remote debugging.</span></span> <span data-ttu-id="75e15-140">Quando habilitado, você pode usar o depurador remoto no Visual Studio para conectar-se diretamente com seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="75e15-140">When enabled, you can use the remote debugger in Visual Studio to connect directly to your web app.</span></span> <span data-ttu-id="75e15-141">A depuração remota permanecerá habilitada por 48 horas.</span><span class="sxs-lookup"><span data-stu-id="75e15-141">Remote debugging will remain enabled for 48 hours.</span></span> 

### <a name="app-settings"></a><span data-ttu-id="75e15-142">Configurações do aplicativo</span><span class="sxs-lookup"><span data-stu-id="75e15-142">App settings</span></span>
<span data-ttu-id="75e15-143">Esta seção contém pares de nome/valor que seu aplicativo Web carregará na inicialização.</span><span class="sxs-lookup"><span data-stu-id="75e15-143">This section contains name/value pairs that you web app will load on start up.</span></span> 

* <span data-ttu-id="75e15-144">Para aplicativos .NET, essas configurações serão injetadas em sua configuração `AppSettings` em tempo de execução, substituindo as configurações existentes.</span><span class="sxs-lookup"><span data-stu-id="75e15-144">For .NET apps, these settings are injected into your .NET configuration `AppSettings` at runtime, overriding existing settings.</span></span> 
* <span data-ttu-id="75e15-145">Os aplicativos PHP, Python, Java e Nó podem acessar essas configurações como variáveis do ambiente em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="75e15-145">PHP, Python, Java and Node applications can access these settings as environment variables at runtime.</span></span> <span data-ttu-id="75e15-146">Para cada configuração do aplicativo, são criadas duas variáveis; uma com o nome especificado pela entrada de configuração do aplicativo, e outra com um prefixo de APPSETTING_.</span><span class="sxs-lookup"><span data-stu-id="75e15-146">For each app setting, two environment variables are created; one with the name specified by the app setting entry, and another with a prefix of APPSETTING_.</span></span> <span data-ttu-id="75e15-147">Ambas contêm o mesmo valor.</span><span class="sxs-lookup"><span data-stu-id="75e15-147">Both contain the same value.</span></span>

### <a name="connection-strings"></a><span data-ttu-id="75e15-148">Cadeias de conexão</span><span class="sxs-lookup"><span data-stu-id="75e15-148">Connection strings</span></span>
<span data-ttu-id="75e15-149">Cadeia de conexão para recursos vinculados.</span><span class="sxs-lookup"><span data-stu-id="75e15-149">Connection strings for linked resources.</span></span> 

<span data-ttu-id="75e15-150">Para aplicativos .NET, essas cadeias de conexão serão injetadas em suas definições do `connectionStrings` das configurações do .NET no tempo de execução, substituindo as entradas existentes cujas chaves são iguais ao nome do banco de dados vinculado.</span><span class="sxs-lookup"><span data-stu-id="75e15-150">For .NET apps, these connection strings are injected into your .NET configuration `connectionStrings` settings at runtime, overriding existing entries where the key equals the linked database name.</span></span> 

<span data-ttu-id="75e15-151">Para aplicativos PHP, Python, Java e Nó essas configurações estarão disponíveis como variáveis de ambiente em tempo de execução, antecedidas com o tipo de conexão.</span><span class="sxs-lookup"><span data-stu-id="75e15-151">For PHP, Python, Java and Node applications, these settings will be available as environment variables at runtime, prefixed with the connection type.</span></span> <span data-ttu-id="75e15-152">Os prefixos das variáveis de ambiente são os seguintes:</span><span class="sxs-lookup"><span data-stu-id="75e15-152">The environment variable prefixes are as follows:</span></span> 

* <span data-ttu-id="75e15-153">SQL Server: `SQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="75e15-153">SQL Server: `SQLCONNSTR_`</span></span>
* <span data-ttu-id="75e15-154">MySQL: `MYSQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="75e15-154">MySQL: `MYSQLCONNSTR_`</span></span>
* <span data-ttu-id="75e15-155">Banco de Dados SQL: `SQLAZURECONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="75e15-155">SQL Database: `SQLAZURECONNSTR_`</span></span>
* <span data-ttu-id="75e15-156">Personalizado: `CUSTOMCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="75e15-156">Custom: `CUSTOMCONNSTR_`</span></span>

<span data-ttu-id="75e15-157">Por exemplo, se uma cadeia de conexão MySql fosse nomeado `connectionstring1`, ela seria acessada pela variável de ambiente `MYSQLCONNSTR_connectionString1`.</span><span class="sxs-lookup"><span data-stu-id="75e15-157">For example, if a MySql connection string were named `connectionstring1`, it would be accessed through the environment variable `MYSQLCONNSTR_connectionString1`.</span></span>

### <a name="default-documents"></a><span data-ttu-id="75e15-158">Documentos padrão</span><span class="sxs-lookup"><span data-stu-id="75e15-158">Default documents</span></span>
<span data-ttu-id="75e15-159">O documento padrão é a página da Web exibida na URL raiz de um site.</span><span class="sxs-lookup"><span data-stu-id="75e15-159">The default document is the web page that is displayed at the root URL for a website.</span></span>  <span data-ttu-id="75e15-160">O primeiro arquivo correspondente na lista é usado.</span><span class="sxs-lookup"><span data-stu-id="75e15-160">The first matching file in the list is used.</span></span> 

<span data-ttu-id="75e15-161">Os aplicativos Web podem utilizar módulos que rotearão na URL, em vez de atender ao conteúdo estático, nesse caso, não há um documento padrão como tal.</span><span class="sxs-lookup"><span data-stu-id="75e15-161">Web apps might use modules that route based on URL, rather than serving static content, in which case there is no default document as such.</span></span>    

### <a name="handler-mappings"></a><span data-ttu-id="75e15-162">Mapeamentos de manipulador</span><span class="sxs-lookup"><span data-stu-id="75e15-162">Handler mappings</span></span>
<span data-ttu-id="75e15-163">Use essa área para adicionar processadores de script personalizados para manipular solicitações de extensões de arquivo específicas.</span><span class="sxs-lookup"><span data-stu-id="75e15-163">Use this area to add custom script processors to handle requests for specific file extensions.</span></span> 

* <span data-ttu-id="75e15-164">**Extensão**.</span><span class="sxs-lookup"><span data-stu-id="75e15-164">**Extension**.</span></span> <span data-ttu-id="75e15-165">A extensão do arquivo a ser manipulada, como *.php ou handler.fcgi.</span><span class="sxs-lookup"><span data-stu-id="75e15-165">The file extension to be handled, such as *.php or handler.fcgi.</span></span> 
* <span data-ttu-id="75e15-166">**Caminho do Processador de script**.</span><span class="sxs-lookup"><span data-stu-id="75e15-166">**Script Processor Path**.</span></span> <span data-ttu-id="75e15-167">O caminho absoluto do processador de script.</span><span class="sxs-lookup"><span data-stu-id="75e15-167">The absolute path of the script processor.</span></span> <span data-ttu-id="75e15-168">As solicitações para arquivos que correspondam a extensão do arquivo serão processadas pelo processador de script.</span><span class="sxs-lookup"><span data-stu-id="75e15-168">Requests to files that match the file extension will be processed by the script processor.</span></span> <span data-ttu-id="75e15-169">Use o caminho `D:\home\site\wwwroot` para se referir ao diretório raiz do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="75e15-169">Use the path `D:\home\site\wwwroot` to refer to your app's root directory.</span></span>
* <span data-ttu-id="75e15-170">**Argumentos adicionais**.</span><span class="sxs-lookup"><span data-stu-id="75e15-170">**Additional Arguments**.</span></span> <span data-ttu-id="75e15-171">Argumentos da linha de comando opcionais para o processador de script</span><span class="sxs-lookup"><span data-stu-id="75e15-171">Optional command-line arguments for the script processor</span></span> 

### <a name="virtual-applications-and-directories"></a><span data-ttu-id="75e15-172">Aplicativos e diretórios virtuais</span><span class="sxs-lookup"><span data-stu-id="75e15-172">Virtual applications and directories</span></span>
<span data-ttu-id="75e15-173">Para configurar diretórios e aplicativos virtuais, especifique cada diretório virtual e seu caminho físico correspondente com relação à raiz do site.</span><span class="sxs-lookup"><span data-stu-id="75e15-173">To configure virtual applications and directories, specify each virtual directory and its corresponding physical path relative to the website root.</span></span> <span data-ttu-id="75e15-174">Opcionalmente, você pode marcar a caixa de seleção **Aplicativo** para marcar um diretório virtual como um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="75e15-174">Optionally, you can select the **Application** checkbox to mark a virtual directory as an application.</span></span>

## <a name="enabling-diagnostic-logs"></a><span data-ttu-id="75e15-175">Habilitar logs de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="75e15-175">Enabling diagnostic logs</span></span>
<span data-ttu-id="75e15-176">Para habilitar logs de diagnóstico:</span><span class="sxs-lookup"><span data-stu-id="75e15-176">To enable diagnostic logs:</span></span>

1. <span data-ttu-id="75e15-177">Na folha do seu aplicativo Web, clique em **Todas as configurações**.</span><span class="sxs-lookup"><span data-stu-id="75e15-177">In the blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="75e15-178">Clique em **Logs de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="75e15-178">Click **Diagnostic logs**.</span></span> 

<span data-ttu-id="75e15-179">Opções para gravar os logs de diagnóstico de um aplicativo web que ofereça suporte ao registro em log:</span><span class="sxs-lookup"><span data-stu-id="75e15-179">Options for writing diagnostic logs from a web application that supports logging:</span></span> 

* <span data-ttu-id="75e15-180">**Registro do Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="75e15-180">**Application Logging**.</span></span> <span data-ttu-id="75e15-181">Grava logs de aplicativos no sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="75e15-181">Writes application logs to the file system.</span></span> <span data-ttu-id="75e15-182">O registro em log dura por 12 horas.</span><span class="sxs-lookup"><span data-stu-id="75e15-182">Logging lasts for a period of 12 hours.</span></span> 

<span data-ttu-id="75e15-183">**Nível**.</span><span class="sxs-lookup"><span data-stu-id="75e15-183">**Level**.</span></span> <span data-ttu-id="75e15-184">Quando o registro de aplicativo em log estiver habilitado, esta opção especifica a quantidade de informações que serão gravadas (Erro, Aviso, Informações ou Detalhado).</span><span class="sxs-lookup"><span data-stu-id="75e15-184">When application logging is enabled, this option specifies the amount of information that will be recorded (Error, Warning, Information, or Verbose).</span></span>

<span data-ttu-id="75e15-185">**Log do servidor Web**.</span><span class="sxs-lookup"><span data-stu-id="75e15-185">**Web server logging**.</span></span> <span data-ttu-id="75e15-186">Os logs são salvos no formato W3C estendido de arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="75e15-186">Logs are saved in the W3C extended log file format.</span></span> 

<span data-ttu-id="75e15-187">**Mensagens de erro detalhadas**.</span><span class="sxs-lookup"><span data-stu-id="75e15-187">**Detailed error messages**.</span></span> <span data-ttu-id="75e15-188">Salva arquivos .htm de mensagens de erro detalhadas.</span><span class="sxs-lookup"><span data-stu-id="75e15-188">Saves detailed error messages .htm files.</span></span> <span data-ttu-id="75e15-189">Os arquivos são salvos em /LogFiles/DetailedErrors.</span><span class="sxs-lookup"><span data-stu-id="75e15-189">The files are saved under /LogFiles/DetailedErrors.</span></span> 

<span data-ttu-id="75e15-190">**Rastreamento de solicitações com falha**.</span><span class="sxs-lookup"><span data-stu-id="75e15-190">**Failed request tracing**.</span></span> <span data-ttu-id="75e15-191">Registra solicitações malsucedidas em arquivos XML.</span><span class="sxs-lookup"><span data-stu-id="75e15-191">Logs failed requests to XML files.</span></span> <span data-ttu-id="75e15-192">Os arquivos são salvos em /LogFiles/W3SVC*xxx*, onde xxx é um identificador único.</span><span class="sxs-lookup"><span data-stu-id="75e15-192">The files are saved under /LogFiles/W3SVC*xxx*, where xxx is a unique identifier.</span></span> <span data-ttu-id="75e15-193">Esta pasta contém um arquivo XSL e um ou mais arquivos XML.</span><span class="sxs-lookup"><span data-stu-id="75e15-193">This folder contains an XSL file and one or more XML files.</span></span> <span data-ttu-id="75e15-194">Certifique-se de baixar o arquivo XSL, porque ele fornece funcionalidade para formatar e filtrar os conteúdos dos arquivos XMl.</span><span class="sxs-lookup"><span data-stu-id="75e15-194">Make sure to download the XSL file, because it provides functionality for formatting and filtering the contents of the XML files.</span></span>

<span data-ttu-id="75e15-195">Para exibir os arquivos de log, você deve criar credenciais FTP da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="75e15-195">To view the log files, you must create FTP credentials, as follows:</span></span>

1. <span data-ttu-id="75e15-196">Na folha do seu aplicativo Web, clique em **Todas as configurações**.</span><span class="sxs-lookup"><span data-stu-id="75e15-196">In the blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="75e15-197">Clique em **Credenciais de implantação**.</span><span class="sxs-lookup"><span data-stu-id="75e15-197">Click **Deployment credentials**.</span></span>
3. <span data-ttu-id="75e15-198">Digite um nome de usuário e uma senha.</span><span class="sxs-lookup"><span data-stu-id="75e15-198">Enter a user name and password.</span></span>
4. <span data-ttu-id="75e15-199">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="75e15-199">Click **Save**.</span></span>

![Definir credenciais de implantação][configure03]

<span data-ttu-id="75e15-201">O nome de usuário completo do FTP é "app\nomedousuário", onde *app* é o nome do seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="75e15-201">The full FTP user name is “app\username” where *app* is the name of your web app.</span></span> <span data-ttu-id="75e15-202">O nome de usuário é listado no aplicativo Web, em **Essentials**.</span><span class="sxs-lookup"><span data-stu-id="75e15-202">The username is listed in the web app blade, under **Essentials**.</span></span>  

![Credenciais de implantação FTP][configure02]

## <a name="other-configuration-tasks"></a><span data-ttu-id="75e15-204">Outras tarefas de configuração</span><span class="sxs-lookup"><span data-stu-id="75e15-204">Other configuration tasks</span></span>
### <a name="ssl"></a><span data-ttu-id="75e15-205">SSL</span><span class="sxs-lookup"><span data-stu-id="75e15-205">SSL</span></span>
<span data-ttu-id="75e15-206">no modo Básico ou Padrão, você pode carregar certificados SSL para domínios personalizados.</span><span class="sxs-lookup"><span data-stu-id="75e15-206">In Basic or Standard mode, you can upload SSL certificates for a custom domain.</span></span> <span data-ttu-id="75e15-207">Para obter mais informações, veja [Habilitar HTTPS para um aplicativo Web].</span><span class="sxs-lookup"><span data-stu-id="75e15-207">For more information, see [Enable HTTPS for a web app].</span></span> 

<span data-ttu-id="75e15-208">Para exibir os certificados carregados, clique em **Todas as Configurações** > **Domínios personalizados e SSL**.</span><span class="sxs-lookup"><span data-stu-id="75e15-208">To view your uploaded certificates, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="domain-names"></a><span data-ttu-id="75e15-209">Nomes de domínio</span><span class="sxs-lookup"><span data-stu-id="75e15-209">Domain names</span></span>
<span data-ttu-id="75e15-210">Adicione nomes de domínio personalizados para seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="75e15-210">Add custom domain names for your web app.</span></span> <span data-ttu-id="75e15-211">Para obter mais informações, veja [Configurar um nome de domínio personalizado para um aplicativo Web no Serviço de Aplicativo do Azure].</span><span class="sxs-lookup"><span data-stu-id="75e15-211">For more information, see [Configure a custom domain name for a web app in Azure App Service].</span></span>

<span data-ttu-id="75e15-212">Para exibir seus nomes de domínio, clique em **Todas as Configurações** > **Domínios personalizados e SSL**.</span><span class="sxs-lookup"><span data-stu-id="75e15-212">To view your domain names, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="deployments"></a><span data-ttu-id="75e15-213">Implantações</span><span class="sxs-lookup"><span data-stu-id="75e15-213">Deployments</span></span>
* <span data-ttu-id="75e15-214">Configure a implantação contínua.</span><span class="sxs-lookup"><span data-stu-id="75e15-214">Set up continuous deployment.</span></span> <span data-ttu-id="75e15-215">Confira [Usando Git para implantar aplicativos Web no Serviço de Aplicativo do Azure](web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="75e15-215">See [Using Git to deploy Web Apps in Azure App Service](web-sites-deploy.md).</span></span>
* <span data-ttu-id="75e15-216">Slots de implantação.</span><span class="sxs-lookup"><span data-stu-id="75e15-216">Deployment slots.</span></span> <span data-ttu-id="75e15-217">Veja [Implantar em ambientes de preparo para aplicativos Web no Serviço de Aplicativo do Azure].</span><span class="sxs-lookup"><span data-stu-id="75e15-217">See [Deploy to Staging Environments for Web Apps in Azure App Service].</span></span>

<span data-ttu-id="75e15-218">Para exibir seus slots de implantação, clique em **Todas as Configurações** > **Slots de implantação**.</span><span class="sxs-lookup"><span data-stu-id="75e15-218">To view your deployment slots, click **All Settings** > **Deployment slots**.</span></span>

### <a name="monitoring"></a><span data-ttu-id="75e15-219">Monitoramento</span><span class="sxs-lookup"><span data-stu-id="75e15-219">Monitoring</span></span>
<span data-ttu-id="75e15-220">No modo Básico ou Standard, você pode testar a disponibilidade dos pontos de extremidade HTTP ou HTTPS, de até três locais geograficamente distribuídos.</span><span class="sxs-lookup"><span data-stu-id="75e15-220">In Basic or Standard mode, you can  test the availability of HTTP or HTTPS endpoints, from up to three geo-distributed locations.</span></span> <span data-ttu-id="75e15-221">Um teste de monitoramento falhará se o código de resposta HTTP for um erro (4xx ou 5xx) ou se a resposta demorar mais de 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="75e15-221">A monitoring test fails if the HTTP response code is an error (4xx or 5xx) or the response takes more than 30 seconds.</span></span> <span data-ttu-id="75e15-222">Um ponto de extremidade será considerado disponível caso os testes de monitoramento tenham êxito a partir de todos os locais especificados.</span><span class="sxs-lookup"><span data-stu-id="75e15-222">An endpoint is considered available if the monitoring tests succeed from all the specified locations.</span></span> 

<span data-ttu-id="75e15-223">Para saber mais, consulte [Como monitorar o status de pontos de extremidade da Web].</span><span class="sxs-lookup"><span data-stu-id="75e15-223">For more information, see [How to: Monitor web endpoint status].</span></span>

> [!NOTE]
> <span data-ttu-id="75e15-224">Se você deseja começar com o Serviço de Aplicativo do Azure antes de se inscrever em uma conta do Azure, acesse [Experimentar o Serviço de Aplicativo], em que você pode criar imediatamente um aplicativo Web inicial de curta duração no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="75e15-224">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="75e15-225">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="75e15-225">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="75e15-226">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="75e15-226">Next steps</span></span>
* <span data-ttu-id="75e15-227">[Configurar um nome de domínio personalizado no Serviço de Aplicativo do Azure]</span><span class="sxs-lookup"><span data-stu-id="75e15-227">[Configure a custom domain name in Azure App Service]</span></span>
* <span data-ttu-id="75e15-228">[Habilitar HTTPS para um aplicativo no Serviço de Aplicativo do Azure]</span><span class="sxs-lookup"><span data-stu-id="75e15-228">[Enable HTTPS for an app in Azure App Service]</span></span>
* <span data-ttu-id="75e15-229">[Dimensionar um aplicativo Web no Serviço de Aplicativo do Azure]</span><span class="sxs-lookup"><span data-stu-id="75e15-229">[Scale a web app in Azure App Service]</span></span>
* <span data-ttu-id="75e15-230">[Conceitos básicos de monitoramento para aplicativos Web no Serviço de Aplicativo do Azure]</span><span class="sxs-lookup"><span data-stu-id="75e15-230">[Monitoring basics for Web Apps in Azure App Service]</span></span>

<!-- URL List -->

<span data-ttu-id="75e15-231">[ASP.NET SignalR]: http://www.asp.net/signalr</span><span class="sxs-lookup"><span data-stu-id="75e15-231">[ASP.NET SignalR]: http://www.asp.net/signalr</span></span>
<span data-ttu-id="75e15-232">[Portal do Azure]: https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="75e15-232">[Azure Portal]: https://portal.azure.com/</span></span>
<span data-ttu-id="75e15-233">[Configurar um nome de domínio personalizado no Serviço de Aplicativo do Azure]: ./app-service-web-tutorial-custom-domain.md</span><span class="sxs-lookup"><span data-stu-id="75e15-233">[Configure a custom domain name in Azure App Service]: ./app-service-web-tutorial-custom-domain.md</span></span>
<span data-ttu-id="75e15-234">[Implantar em ambientes de preparo para aplicativos Web no Serviço de Aplicativo do Azure]: ./web-sites-staged-publishing.md</span><span class="sxs-lookup"><span data-stu-id="75e15-234">[Deploy to Staging Environments for Web Apps in Azure App Service]: ./web-sites-staged-publishing.md</span></span>
<span data-ttu-id="75e15-235">[Habilitar HTTPS para um aplicativo no Serviço de Aplicativo do Azure]: ./app-service-web-tutorial-custom-ssl.md</span><span class="sxs-lookup"><span data-stu-id="75e15-235">[Enable HTTPS for an app in Azure App Service]: ./app-service-web-tutorial-custom-ssl.md</span></span>
<span data-ttu-id="75e15-236">[Como monitorar o status de pontos de extremidade da Web]: http://go.microsoft.com/fwLink/?LinkID=279906</span><span class="sxs-lookup"><span data-stu-id="75e15-236">[How to: Monitor web endpoint status]: http://go.microsoft.com/fwLink/?LinkID=279906</span></span>
<span data-ttu-id="75e15-237">[Conceitos básicos de monitoramento para aplicativos Web no Serviço de Aplicativo do Azure]: ./web-sites-monitor.md</span><span class="sxs-lookup"><span data-stu-id="75e15-237">[Monitoring basics for Web Apps in Azure App Service]: ./web-sites-monitor.md</span></span>
<span data-ttu-id="75e15-238">[modo de pipeline]: http://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture#Application</span><span class="sxs-lookup"><span data-stu-id="75e15-238">[pipeline mode]: http://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture#Application</span></span>
<span data-ttu-id="75e15-239">[Dimensionar um aplicativo Web no Serviço de Aplicativo do Azure]: ./web-sites-scale.md</span><span class="sxs-lookup"><span data-stu-id="75e15-239">[Scale a web app in Azure App Service]: ./web-sites-scale.md</span></span>
<span data-ttu-id="75e15-240">[socket.io]: ./web-sites-nodejs-chat-app-socketio.md</span><span class="sxs-lookup"><span data-stu-id="75e15-240">[socket.io]: ./web-sites-nodejs-chat-app-socketio.md</span></span>
<span data-ttu-id="75e15-241">[Experimentar o Serviço de Aplicativo]: https://azure.microsoft.com/try/app-service/</span><span class="sxs-lookup"><span data-stu-id="75e15-241">[Try App Service]: https://azure.microsoft.com/try/app-service/</span></span>

<!-- IMG List -->

[configure01]: ./media/web-sites-configure/configure01.png
[configure02]: ./media/web-sites-configure/configure02.png
[configure03]: ./media/web-sites-configure/configure03.png
