---
title: "aaaConfigure os aplicativos web no serviço de aplicativo do Azure"
description: "Como tooconfigure um aplicativo web de serviços de aplicativo do Azure"
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
ms.openlocfilehash: 8697ab6f21cfeb470e11f0d82c68692d43142fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-apps-in-azure-app-service"></a><span data-ttu-id="4b493-103">Configurar aplicativos Web no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="4b493-103">Configure web apps in Azure App Service</span></span>
<span data-ttu-id="4b493-104">Este tópico explica como tooconfigure um aplicativo web usando Olá [Portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="4b493-104">This topic explains how tooconfigure a web app using hello [Azure Portal].</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="application-settings"></a><span data-ttu-id="4b493-105">Configurações do aplicativo</span><span class="sxs-lookup"><span data-stu-id="4b493-105">Application settings</span></span>
1. <span data-ttu-id="4b493-106">Em Olá [Portal do Azure], abra folha Olá para o aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="4b493-106">In hello [Azure Portal], open hello blade for hello web app.</span></span>
2. <span data-ttu-id="4b493-107">Clique em **Todas as Configurações**.</span><span class="sxs-lookup"><span data-stu-id="4b493-107">Click **All Settings**.</span></span>
3. <span data-ttu-id="4b493-108">Clique em **Configurações do Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="4b493-108">Click **Application Settings**.</span></span>

![Configurações do aplicativo][configure01]

<span data-ttu-id="4b493-110">Olá **configurações de aplicativo** folha tem configurações agrupadas em várias categorias.</span><span class="sxs-lookup"><span data-stu-id="4b493-110">hello **Application settings** blade has settings grouped under several categories.</span></span>

### <a name="general-settings"></a><span data-ttu-id="4b493-111">Configurações gerais</span><span class="sxs-lookup"><span data-stu-id="4b493-111">General settings</span></span>
<span data-ttu-id="4b493-112">**Versão do Framework**.</span><span class="sxs-lookup"><span data-stu-id="4b493-112">**Framework versions**.</span></span> <span data-ttu-id="4b493-113">Configurar essas opções se seu aplicativo usa qualquer um desses frameworks:</span><span class="sxs-lookup"><span data-stu-id="4b493-113">Set these options if your app uses any these frameworks:</span></span> 

* <span data-ttu-id="4b493-114">**.NET framework**: conjunto Olá a versão do .NET framework.</span><span class="sxs-lookup"><span data-stu-id="4b493-114">**.NET Framework**: Set hello .NET framework version.</span></span> 
* <span data-ttu-id="4b493-115">**PHP**: versão do conjunto de PHP hello, ou **OFF** toodisable PHP.</span><span class="sxs-lookup"><span data-stu-id="4b493-115">**PHP**: Set hello PHP version, or **OFF** toodisable PHP.</span></span> 
* <span data-ttu-id="4b493-116">**Java**: versão do Java Olá Select ou **OFF** toodisable Java.</span><span class="sxs-lookup"><span data-stu-id="4b493-116">**Java**: Select hello Java version or **OFF** toodisable Java.</span></span> <span data-ttu-id="4b493-117">Saudação de uso **contêiner da Web** toochoose opção entre versões Tomcat e Jetty.</span><span class="sxs-lookup"><span data-stu-id="4b493-117">Use hello **Web Container** option toochoose between Tomcat and Jetty versions.</span></span>
* <span data-ttu-id="4b493-118">**Python**: versão do Python selecione hello, ou **OFF** toodisable Python.</span><span class="sxs-lookup"><span data-stu-id="4b493-118">**Python**: Select hello Python version, or **OFF** toodisable Python.</span></span>

<span data-ttu-id="4b493-119">Por motivos técnicos, habilitar o Java para seu aplicativo desativa opções de saudação .NET, PHP e Python.</span><span class="sxs-lookup"><span data-stu-id="4b493-119">For technical reasons, enabling Java for your app disables hello .NET, PHP, and Python options.</span></span>

<span data-ttu-id="4b493-120"><a name="platform"></a>
**Plataforma**.</span><span class="sxs-lookup"><span data-stu-id="4b493-120"><a name="platform"></a>
**Platform**.</span></span> <span data-ttu-id="4b493-121">Seleciona se o seu aplicativo é executado em ambiente de 32 ou 64 bits.</span><span class="sxs-lookup"><span data-stu-id="4b493-121">Selects whether your web app runs in a 32-bit or 64-bit environment.</span></span> <span data-ttu-id="4b493-122">ambiente de 64 bits Olá requer modo básico ou padrão.</span><span class="sxs-lookup"><span data-stu-id="4b493-122">hello 64-bit environment requires Basic or Standard mode.</span></span> <span data-ttu-id="4b493-123">Modos Livre e Compartilhado são sempre executados em um ambiente de 32 bits.</span><span class="sxs-lookup"><span data-stu-id="4b493-123">Free and Shared modes always run in a 32-bit environment.</span></span>

<span data-ttu-id="4b493-124">**Web Sockets**.</span><span class="sxs-lookup"><span data-stu-id="4b493-124">**Web Sockets**.</span></span> <span data-ttu-id="4b493-125">Definir **ON** tooenable Olá protocolo WebSocket; por exemplo, se seu aplicativo web usa [ASP.NET SignalR] ou [socket.io].</span><span class="sxs-lookup"><span data-stu-id="4b493-125">Set **ON** tooenable hello WebSocket protocol; for example, if your web app uses [ASP.NET SignalR] or [socket.io].</span></span>

<span data-ttu-id="4b493-126"><a name="alwayson"></a>
**Sempre ativado**.</span><span class="sxs-lookup"><span data-stu-id="4b493-126"><a name="alwayson"></a>
**Always On**.</span></span> <span data-ttu-id="4b493-127">Por padrão, os aplicativos Web serão descarregados se estiverem ociosos por um determinado período de tempo.</span><span class="sxs-lookup"><span data-stu-id="4b493-127">By default, web apps are unloaded if they are idle for some period of time.</span></span> <span data-ttu-id="4b493-128">Isso permite que o sistema Olá conservar recursos.</span><span class="sxs-lookup"><span data-stu-id="4b493-128">This lets hello system conserve resources.</span></span> <span data-ttu-id="4b493-129">No modo básico ou padrão, você pode habilitar **AlwaysOn** tookeep Olá aplicativo carregado todo o tempo de saudação.</span><span class="sxs-lookup"><span data-stu-id="4b493-129">In Basic or Standard mode, you can enable **Always On** tookeep hello app loaded all hello time.</span></span> <span data-ttu-id="4b493-130">Se seu aplicativo executa trabalhos Web contínuos ou execuções de trabalhos Web disparado usando uma expressão CRON, você deve habilitar **AlwaysOn**, ou trabalhos de web hello podem não ser executado com confiança.</span><span class="sxs-lookup"><span data-stu-id="4b493-130">If your app runs continuous WebJobs or runs WebJobs triggered using a CRON expression, you should enable **Always On**, or hello web jobs may not run reliably.</span></span>

<span data-ttu-id="4b493-131">**Versão do Pipeline Gerenciado**.</span><span class="sxs-lookup"><span data-stu-id="4b493-131">**Managed Pipeline Version**.</span></span> <span data-ttu-id="4b493-132">Conjuntos de Olá IIS [modo pipeline].</span><span class="sxs-lookup"><span data-stu-id="4b493-132">Sets hello IIS [pipeline mode].</span></span> <span data-ttu-id="4b493-133">Deixe este definido tooIntegrated (padrão de saudação), a menos que você tenha um aplicativo herdado que requer uma versão mais antiga do IIS.</span><span class="sxs-lookup"><span data-stu-id="4b493-133">Leave this set tooIntegrated (hello default) unless you have a legacy app that requires an older version of IIS.</span></span>

<span data-ttu-id="4b493-134">**Troca Automática**.</span><span class="sxs-lookup"><span data-stu-id="4b493-134">**Auto Swap**.</span></span> <span data-ttu-id="4b493-135">Se você habilitar a troca automática para um slot de implantação, do serviço de aplicativo automaticamente alternará Olá web aplicativo em produção quando você enviar por push um slot de toothat de atualização.</span><span class="sxs-lookup"><span data-stu-id="4b493-135">If you enable Auto Swap for a deployment slot, App Service will automatically swap hello web app into production when you push an update toothat slot.</span></span> <span data-ttu-id="4b493-136">Para obter mais informações, consulte [implantar toostaging slots para aplicativos web no serviço de aplicativo do Azure](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="4b493-136">For more information, see [Deploy toostaging slots for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span>

### <a name="debugging"></a><span data-ttu-id="4b493-137">Depurando</span><span class="sxs-lookup"><span data-stu-id="4b493-137">Debugging</span></span>
<span data-ttu-id="4b493-138">**Depuração Remota**.</span><span class="sxs-lookup"><span data-stu-id="4b493-138">**Remote Debugging**.</span></span> <span data-ttu-id="4b493-139">Habilita a depuração remota.</span><span class="sxs-lookup"><span data-stu-id="4b493-139">Enables remote debugging.</span></span> <span data-ttu-id="4b493-140">Quando habilitado, você pode usar o depurador remoto Olá no Visual Studio tooconnect diretamente tooyour de aplicativo da web.</span><span class="sxs-lookup"><span data-stu-id="4b493-140">When enabled, you can use hello remote debugger in Visual Studio tooconnect directly tooyour web app.</span></span> <span data-ttu-id="4b493-141">A depuração remota permanecerá habilitada por 48 horas.</span><span class="sxs-lookup"><span data-stu-id="4b493-141">Remote debugging will remain enabled for 48 hours.</span></span> 

### <a name="app-settings"></a><span data-ttu-id="4b493-142">Configurações do aplicativo</span><span class="sxs-lookup"><span data-stu-id="4b493-142">App settings</span></span>
<span data-ttu-id="4b493-143">Esta seção contém pares de nome/valor que seu aplicativo Web carregará na inicialização.</span><span class="sxs-lookup"><span data-stu-id="4b493-143">This section contains name/value pairs that you web app will load on start up.</span></span> 

* <span data-ttu-id="4b493-144">Para aplicativos .NET, essas configurações serão injetadas em sua configuração `AppSettings` em tempo de execução, substituindo as configurações existentes.</span><span class="sxs-lookup"><span data-stu-id="4b493-144">For .NET apps, these settings are injected into your .NET configuration `AppSettings` at runtime, overriding existing settings.</span></span> 
* <span data-ttu-id="4b493-145">Os aplicativos PHP, Python, Java e Nó podem acessar essas configurações como variáveis do ambiente em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="4b493-145">PHP, Python, Java and Node applications can access these settings as environment variables at runtime.</span></span> <span data-ttu-id="4b493-146">Para cada configuração de aplicativo, as duas variáveis de ambiente são criadas; um com o nome de saudação especificado pela entrada de configuração de aplicativo hello e outra com um prefixo de APPSETTING_.</span><span class="sxs-lookup"><span data-stu-id="4b493-146">For each app setting, two environment variables are created; one with hello name specified by hello app setting entry, and another with a prefix of APPSETTING_.</span></span> <span data-ttu-id="4b493-147">Ambos contêm Olá mesmo valor.</span><span class="sxs-lookup"><span data-stu-id="4b493-147">Both contain hello same value.</span></span>

### <a name="connection-strings"></a><span data-ttu-id="4b493-148">Cadeias de conexão</span><span class="sxs-lookup"><span data-stu-id="4b493-148">Connection strings</span></span>
<span data-ttu-id="4b493-149">Cadeia de conexão para recursos vinculados.</span><span class="sxs-lookup"><span data-stu-id="4b493-149">Connection strings for linked resources.</span></span> 

<span data-ttu-id="4b493-150">Para aplicativos .NET, essas cadeias de caracteres de conexão serão injetadas nas configuração do .NET `connectionStrings` configurações em tempo de execução, substituindo as entradas existentes onde é igual a chave Olá Olá nome do banco de dados vinculado.</span><span class="sxs-lookup"><span data-stu-id="4b493-150">For .NET apps, these connection strings are injected into your .NET configuration `connectionStrings` settings at runtime, overriding existing entries where hello key equals hello linked database name.</span></span> 

<span data-ttu-id="4b493-151">Para aplicativos PHP, Python, Java e nó, essas configurações estarão disponíveis como variáveis de ambiente em tempo de execução, prefixado com o tipo de conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="4b493-151">For PHP, Python, Java and Node applications, these settings will be available as environment variables at runtime, prefixed with hello connection type.</span></span> <span data-ttu-id="4b493-152">prefixos de variável de ambiente Olá são da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="4b493-152">hello environment variable prefixes are as follows:</span></span> 

* <span data-ttu-id="4b493-153">SQL Server: `SQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="4b493-153">SQL Server: `SQLCONNSTR_`</span></span>
* <span data-ttu-id="4b493-154">MySQL: `MYSQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="4b493-154">MySQL: `MYSQLCONNSTR_`</span></span>
* <span data-ttu-id="4b493-155">Banco de Dados SQL: `SQLAZURECONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="4b493-155">SQL Database: `SQLAZURECONNSTR_`</span></span>
* <span data-ttu-id="4b493-156">Personalizado: `CUSTOMCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="4b493-156">Custom: `CUSTOMCONNSTR_`</span></span>

<span data-ttu-id="4b493-157">Por exemplo, se uma cadeia de caracteres de conexão MySql foram nomeada `connectionstring1`, ele seria acessado por meio da variável de ambiente Olá `MYSQLCONNSTR_connectionString1`.</span><span class="sxs-lookup"><span data-stu-id="4b493-157">For example, if a MySql connection string were named `connectionstring1`, it would be accessed through hello environment variable `MYSQLCONNSTR_connectionString1`.</span></span>

### <a name="default-documents"></a><span data-ttu-id="4b493-158">Documentos padrão</span><span class="sxs-lookup"><span data-stu-id="4b493-158">Default documents</span></span>
<span data-ttu-id="4b493-159">o documento padrão Olá é Olá web página é exibido na URL da raiz de saudação para um site.</span><span class="sxs-lookup"><span data-stu-id="4b493-159">hello default document is hello web page that is displayed at hello root URL for a website.</span></span>  <span data-ttu-id="4b493-160">Olá primeira correspondência na lista de saudação é usado.</span><span class="sxs-lookup"><span data-stu-id="4b493-160">hello first matching file in hello list is used.</span></span> 

<span data-ttu-id="4b493-161">Os aplicativos Web podem utilizar módulos que rotearão na URL, em vez de atender ao conteúdo estático, nesse caso, não há um documento padrão como tal.</span><span class="sxs-lookup"><span data-stu-id="4b493-161">Web apps might use modules that route based on URL, rather than serving static content, in which case there is no default document as such.</span></span>    

### <a name="handler-mappings"></a><span data-ttu-id="4b493-162">Mapeamentos de manipulador</span><span class="sxs-lookup"><span data-stu-id="4b493-162">Handler mappings</span></span>
<span data-ttu-id="4b493-163">Use solicitações de toohandle de processadores de script personalizado para tooadd essa área para extensões de arquivo específico.</span><span class="sxs-lookup"><span data-stu-id="4b493-163">Use this area tooadd custom script processors toohandle requests for specific file extensions.</span></span> 

* <span data-ttu-id="4b493-164">**Extensão**.</span><span class="sxs-lookup"><span data-stu-id="4b493-164">**Extension**.</span></span> <span data-ttu-id="4b493-165">Olá toobe de extensão de arquivo é tratado como *.php ou fcgi.</span><span class="sxs-lookup"><span data-stu-id="4b493-165">hello file extension toobe handled, such as *.php or handler.fcgi.</span></span> 
* <span data-ttu-id="4b493-166">**Caminho do Processador de script**.</span><span class="sxs-lookup"><span data-stu-id="4b493-166">**Script Processor Path**.</span></span> <span data-ttu-id="4b493-167">caminho absoluto de saudação do processador de script hello.</span><span class="sxs-lookup"><span data-stu-id="4b493-167">hello absolute path of hello script processor.</span></span> <span data-ttu-id="4b493-168">Toofiles de solicitações que correspondam a extensão de arquivo hello serão processados pelo processador de script hello.</span><span class="sxs-lookup"><span data-stu-id="4b493-168">Requests toofiles that match hello file extension will be processed by hello script processor.</span></span> <span data-ttu-id="4b493-169">Use o caminho de saudação `D:\home\site\wwwroot` diretório de raiz do aplicativo de tooyour toorefer.</span><span class="sxs-lookup"><span data-stu-id="4b493-169">Use hello path `D:\home\site\wwwroot` toorefer tooyour app's root directory.</span></span>
* <span data-ttu-id="4b493-170">**Argumentos adicionais**.</span><span class="sxs-lookup"><span data-stu-id="4b493-170">**Additional Arguments**.</span></span> <span data-ttu-id="4b493-171">Argumentos de linha de comando opcionais para o processador de script hello</span><span class="sxs-lookup"><span data-stu-id="4b493-171">Optional command-line arguments for hello script processor</span></span> 

### <a name="virtual-applications-and-directories"></a><span data-ttu-id="4b493-172">Aplicativos e diretórios virtuais</span><span class="sxs-lookup"><span data-stu-id="4b493-172">Virtual applications and directories</span></span>
<span data-ttu-id="4b493-173">aplicativos virtuais tooconfigure e diretórios, especifique cada diretório virtual e sua raiz do site correspondente no caminho físico relativo toohello.</span><span class="sxs-lookup"><span data-stu-id="4b493-173">tooconfigure virtual applications and directories, specify each virtual directory and its corresponding physical path relative toohello website root.</span></span> <span data-ttu-id="4b493-174">Opcionalmente, você pode selecionar Olá **aplicativo** caixa de seleção toomark um diretório virtual como um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4b493-174">Optionally, you can select hello **Application** checkbox toomark a virtual directory as an application.</span></span>

## <a name="enabling-diagnostic-logs"></a><span data-ttu-id="4b493-175">Habilitar logs de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="4b493-175">Enabling diagnostic logs</span></span>
<span data-ttu-id="4b493-176">logs de diagnóstico tooenable:</span><span class="sxs-lookup"><span data-stu-id="4b493-176">tooenable diagnostic logs:</span></span>

1. <span data-ttu-id="4b493-177">Na folha de saudação para seu aplicativo web, clique em **todas as configurações**.</span><span class="sxs-lookup"><span data-stu-id="4b493-177">In hello blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="4b493-178">Clique em **Logs de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="4b493-178">Click **Diagnostic logs**.</span></span> 

<span data-ttu-id="4b493-179">Opções para gravar os logs de diagnóstico de um aplicativo web que ofereça suporte ao registro em log:</span><span class="sxs-lookup"><span data-stu-id="4b493-179">Options for writing diagnostic logs from a web application that supports logging:</span></span> 

* <span data-ttu-id="4b493-180">**Registro do Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="4b493-180">**Application Logging**.</span></span> <span data-ttu-id="4b493-181">Grava logs de aplicativo toohello sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="4b493-181">Writes application logs toohello file system.</span></span> <span data-ttu-id="4b493-182">O registro em log dura por 12 horas.</span><span class="sxs-lookup"><span data-stu-id="4b493-182">Logging lasts for a period of 12 hours.</span></span> 

<span data-ttu-id="4b493-183">**Nível**.</span><span class="sxs-lookup"><span data-stu-id="4b493-183">**Level**.</span></span> <span data-ttu-id="4b493-184">Quando o log de aplicativo é habilitado, essa opção especifica Olá de informações que serão gravado (erro, aviso, informações ou detalhado).</span><span class="sxs-lookup"><span data-stu-id="4b493-184">When application logging is enabled, this option specifies hello amount of information that will be recorded (Error, Warning, Information, or Verbose).</span></span>

<span data-ttu-id="4b493-185">**Log do servidor Web**.</span><span class="sxs-lookup"><span data-stu-id="4b493-185">**Web server logging**.</span></span> <span data-ttu-id="4b493-186">Logs são salvos no formato de arquivo de log estendido do hello W3C.</span><span class="sxs-lookup"><span data-stu-id="4b493-186">Logs are saved in hello W3C extended log file format.</span></span> 

<span data-ttu-id="4b493-187">**Mensagens de erro detalhadas**.</span><span class="sxs-lookup"><span data-stu-id="4b493-187">**Detailed error messages**.</span></span> <span data-ttu-id="4b493-188">Salva arquivos .htm de mensagens de erro detalhadas.</span><span class="sxs-lookup"><span data-stu-id="4b493-188">Saves detailed error messages .htm files.</span></span> <span data-ttu-id="4b493-189">Olá arquivos são salvos em /LogFiles/DetailedErrors.</span><span class="sxs-lookup"><span data-stu-id="4b493-189">hello files are saved under /LogFiles/DetailedErrors.</span></span> 

<span data-ttu-id="4b493-190">**Rastreamento de solicitações com falha**.</span><span class="sxs-lookup"><span data-stu-id="4b493-190">**Failed request tracing**.</span></span> <span data-ttu-id="4b493-191">Logs de falha solicitações tooXML arquivos.</span><span class="sxs-lookup"><span data-stu-id="4b493-191">Logs failed requests tooXML files.</span></span> <span data-ttu-id="4b493-192">Olá arquivos são salvos em arquivos de log/W3SVC*xxx*, onde xxx é um identificador exclusivo.</span><span class="sxs-lookup"><span data-stu-id="4b493-192">hello files are saved under /LogFiles/W3SVC*xxx*, where xxx is a unique identifier.</span></span> <span data-ttu-id="4b493-193">Esta pasta contém um arquivo XSL e um ou mais arquivos XML.</span><span class="sxs-lookup"><span data-stu-id="4b493-193">This folder contains an XSL file and one or more XML files.</span></span> <span data-ttu-id="4b493-194">Verifique a saudação de toodownload-se de que o arquivo XSL, porque ele fornece a funcionalidade para formatar e filtragem de conteúdo Olá Olá dos arquivos de XML.</span><span class="sxs-lookup"><span data-stu-id="4b493-194">Make sure toodownload hello XSL file, because it provides functionality for formatting and filtering hello contents of hello XML files.</span></span>

<span data-ttu-id="4b493-195">arquivos de log do tooview hello, você deve criar as credenciais FTP, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="4b493-195">tooview hello log files, you must create FTP credentials, as follows:</span></span>

1. <span data-ttu-id="4b493-196">Na folha de saudação para seu aplicativo web, clique em **todas as configurações**.</span><span class="sxs-lookup"><span data-stu-id="4b493-196">In hello blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="4b493-197">Clique em **Credenciais de implantação**.</span><span class="sxs-lookup"><span data-stu-id="4b493-197">Click **Deployment credentials**.</span></span>
3. <span data-ttu-id="4b493-198">Digite um nome de usuário e uma senha.</span><span class="sxs-lookup"><span data-stu-id="4b493-198">Enter a user name and password.</span></span>
4. <span data-ttu-id="4b493-199">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="4b493-199">Click **Save**.</span></span>

![Definir credenciais de implantação][configure03]

<span data-ttu-id="4b493-201">nome de usuário FTP completo Olá é "app\username" onde *aplicativo* é o nome de saudação do seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="4b493-201">hello full FTP user name is “app\username” where *app* is hello name of your web app.</span></span> <span data-ttu-id="4b493-202">Olá nome de usuário está listado na folha de saudação do aplicativo web, em **Essentials**.</span><span class="sxs-lookup"><span data-stu-id="4b493-202">hello username is listed in hello web app blade, under **Essentials**.</span></span>  

![Credenciais de implantação FTP][configure02]

## <a name="other-configuration-tasks"></a><span data-ttu-id="4b493-204">Outras tarefas de configuração</span><span class="sxs-lookup"><span data-stu-id="4b493-204">Other configuration tasks</span></span>
### <a name="ssl"></a><span data-ttu-id="4b493-205">SSL</span><span class="sxs-lookup"><span data-stu-id="4b493-205">SSL</span></span>
<span data-ttu-id="4b493-206">no modo Básico ou Padrão, você pode carregar certificados SSL para domínios personalizados.</span><span class="sxs-lookup"><span data-stu-id="4b493-206">In Basic or Standard mode, you can upload SSL certificates for a custom domain.</span></span> <span data-ttu-id="4b493-207">Para obter mais informações, veja [Habilitar HTTPS para um aplicativo Web].</span><span class="sxs-lookup"><span data-stu-id="4b493-207">For more information, see [Enable HTTPS for a web app].</span></span> 

<span data-ttu-id="4b493-208">tooview os certificados carregados, clique **todas as configurações** > **domínios personalizados e SSL**.</span><span class="sxs-lookup"><span data-stu-id="4b493-208">tooview your uploaded certificates, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="domain-names"></a><span data-ttu-id="4b493-209">Nomes de domínio</span><span class="sxs-lookup"><span data-stu-id="4b493-209">Domain names</span></span>
<span data-ttu-id="4b493-210">Adicione nomes de domínio personalizados para seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="4b493-210">Add custom domain names for your web app.</span></span> <span data-ttu-id="4b493-211">Para obter mais informações, veja [Configurar um nome de domínio personalizado para um aplicativo Web no Serviço de Aplicativo do Azure].</span><span class="sxs-lookup"><span data-stu-id="4b493-211">For more information, see [Configure a custom domain name for a web app in Azure App Service].</span></span>

<span data-ttu-id="4b493-212">tooview seus nomes de domínio, clique **todas as configurações** > **domínios personalizados e SSL**.</span><span class="sxs-lookup"><span data-stu-id="4b493-212">tooview your domain names, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="deployments"></a><span data-ttu-id="4b493-213">Implantações</span><span class="sxs-lookup"><span data-stu-id="4b493-213">Deployments</span></span>
* <span data-ttu-id="4b493-214">Configure a implantação contínua.</span><span class="sxs-lookup"><span data-stu-id="4b493-214">Set up continuous deployment.</span></span> <span data-ttu-id="4b493-215">Consulte [toodeploy Git usando aplicativos Web no serviço de aplicativo do Azure](web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="4b493-215">See [Using Git toodeploy Web Apps in Azure App Service](web-sites-deploy.md).</span></span>
* <span data-ttu-id="4b493-216">Slots de implantação.</span><span class="sxs-lookup"><span data-stu-id="4b493-216">Deployment slots.</span></span> <span data-ttu-id="4b493-217">Consulte [implantar ambientes tooStaging para aplicativos Web no serviço de aplicativo do Azure].</span><span class="sxs-lookup"><span data-stu-id="4b493-217">See [Deploy tooStaging Environments for Web Apps in Azure App Service].</span></span>

<span data-ttu-id="4b493-218">tooview seus slots de implantação, clique **todas as configurações** > **slots de implantação**.</span><span class="sxs-lookup"><span data-stu-id="4b493-218">tooview your deployment slots, click **All Settings** > **Deployment slots**.</span></span>

### <a name="monitoring"></a><span data-ttu-id="4b493-219">Monitoramento</span><span class="sxs-lookup"><span data-stu-id="4b493-219">Monitoring</span></span>
<span data-ttu-id="4b493-220">No modo básico ou padrão, você pode testar disponibilidade Olá de pontos de extremidade HTTP ou HTTPS, de locais distribuídos geograficamente de toothree.</span><span class="sxs-lookup"><span data-stu-id="4b493-220">In Basic or Standard mode, you can  test hello availability of HTTP or HTTPS endpoints, from up toothree geo-distributed locations.</span></span> <span data-ttu-id="4b493-221">Teste de monitoramento falhará se Olá código de resposta HTTP é um erro (4xx ou 5xx) ou resposta Olá leva mais de 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="4b493-221">A monitoring test fails if hello HTTP response code is an error (4xx or 5xx) or hello response takes more than 30 seconds.</span></span> <span data-ttu-id="4b493-222">Um ponto de extremidade é considerado disponível se os testes de monitoramento Olá bem-sucedida de todos os Olá especificou locais.</span><span class="sxs-lookup"><span data-stu-id="4b493-222">An endpoint is considered available if hello monitoring tests succeed from all hello specified locations.</span></span> 

<span data-ttu-id="4b493-223">Para saber mais, consulte [Como monitorar o status de pontos de extremidade da Web].</span><span class="sxs-lookup"><span data-stu-id="4b493-223">For more information, see [How to: Monitor web endpoint status].</span></span>

> [!NOTE]
> <span data-ttu-id="4b493-224">Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo], onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4b493-224">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="4b493-225">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="4b493-225">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="4b493-226">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4b493-226">Next steps</span></span>
* <span data-ttu-id="4b493-227">[Configurar um nome de domínio personalizado no Serviço de Aplicativo do Azure]</span><span class="sxs-lookup"><span data-stu-id="4b493-227">[Configure a custom domain name in Azure App Service]</span></span>
* <span data-ttu-id="4b493-228">[Habilitar HTTPS para um aplicativo no Serviço de Aplicativo do Azure]</span><span class="sxs-lookup"><span data-stu-id="4b493-228">[Enable HTTPS for an app in Azure App Service]</span></span>
* <span data-ttu-id="4b493-229">[Dimensionar um aplicativo Web no Serviço de Aplicativo do Azure]</span><span class="sxs-lookup"><span data-stu-id="4b493-229">[Scale a web app in Azure App Service]</span></span>
* <span data-ttu-id="4b493-230">[Conceitos básicos de monitoramento para aplicativos Web no Serviço de Aplicativo do Azure]</span><span class="sxs-lookup"><span data-stu-id="4b493-230">[Monitoring basics for Web Apps in Azure App Service]</span></span>

<!-- URL List -->

[ASP.NET SignalR]: http://www.asp.net/signalr
[Portal do Azure]: https://portal.azure.com/
[Configurar um nome de domínio personalizado no Serviço de Aplicativo do Azure]: ./app-service-web-tutorial-custom-domain.md
[implantar ambientes tooStaging para aplicativos Web no serviço de aplicativo do Azure]: ./web-sites-staged-publishing.md
[Habilitar HTTPS para um aplicativo no Serviço de Aplicativo do Azure]: ./app-service-web-tutorial-custom-ssl.md
[Como monitorar o status de pontos de extremidade da Web]: http://go.microsoft.com/fwLink/?LinkID=279906
[Conceitos básicos de monitoramento para aplicativos Web no Serviço de Aplicativo do Azure]: ./web-sites-monitor.md
[modo pipeline]: http://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture#Application
[Dimensionar um aplicativo Web no Serviço de Aplicativo do Azure]: ./web-sites-scale.md
[socket.io]: ./web-sites-nodejs-chat-app-socketio.md
[tente do serviço de aplicativo]: https://azure.microsoft.com/try/app-service/

<!-- IMG List -->

[configure01]: ./media/web-sites-configure/configure01.png
[configure02]: ./media/web-sites-configure/configure02.png
[configure03]: ./media/web-sites-configure/configure03.png
