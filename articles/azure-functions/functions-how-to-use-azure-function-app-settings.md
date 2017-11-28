---
title: "aaaConfigure configurações de aplicativo de função do Azure | Microsoft Docs"
description: "Saiba como tooconfigure Azure funciona configurações do aplicativo."
services: 
documentationcenter: .net
author: rachelappel
manager: erikre
editor: 
ms.assetid: 81eb04f8-9a27-45bb-bf24-9ab6c30d205c
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 04/23/2017
ms.author: glenga
ms.openlocfilehash: 539e203ac449061ef3ceae5e93df3bdbb326e43b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-a-function-app-in-hello-azure-portal"></a><span data-ttu-id="7497d-103">Como um aplicativo de função no portal do Azure de saudação do toomanage</span><span class="sxs-lookup"><span data-stu-id="7497d-103">How toomanage a function app in hello Azure portal</span></span> 

<span data-ttu-id="7497d-104">Em funções do Azure, um função de aplicativo fornece o contexto de execução de saudação para suas funções individuais.</span><span class="sxs-lookup"><span data-stu-id="7497d-104">In Azure Functions, a function app provides hello execution context for your individual functions.</span></span> <span data-ttu-id="7497d-105">Comportamentos de aplicativo de função se aplicam a funções tooall hospedadas por um aplicativo de determinada função.</span><span class="sxs-lookup"><span data-stu-id="7497d-105">Function app behaviors apply tooall functions hosted by a given function app.</span></span> <span data-ttu-id="7497d-106">Este tópico descreve como tooconfigure e gerenciar seus aplicativos de função no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7497d-106">This topic describes how tooconfigure and manage your function apps in hello Azure portal.</span></span>

<span data-ttu-id="7497d-107">toobegin, vá toohello [portal do Azure](http://portal.azure.com) e entrar tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="7497d-107">toobegin, go toohello [Azure portal](http://portal.azure.com) and sign in tooyour Azure account.</span></span> <span data-ttu-id="7497d-108">Na barra de pesquisa Olá na parte superior de saudação do portal Olá, digite nome de saudação do seu aplicativo de função e selecioná-lo na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="7497d-108">In hello search bar at hello top of hello portal, type hello name of your function app and select it from hello list.</span></span> <span data-ttu-id="7497d-109">Depois de selecionar o aplicativo de função, você verá Olá página a seguir:</span><span class="sxs-lookup"><span data-stu-id="7497d-109">After selecting your function app, you see hello following page:</span></span>

![Visão geral do aplicativo de função no hello portal do Azure](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-main.png)

## <span data-ttu-id="7497d-111"><a name="manage-app-service-settings"></a>Guia Configurações do aplicativo de funções</span><span class="sxs-lookup"><span data-stu-id="7497d-111"><a name="manage-app-service-settings"></a>Function app settings tab</span></span>

![Visão geral de função aplicativo no portal do Azure de saudação.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-settings-tab.png)

<span data-ttu-id="7497d-113">Olá **configurações** guia é onde você pode atualizar a versão de tempo de execução de funções hello usado pelo seu aplicativo de função.</span><span class="sxs-lookup"><span data-stu-id="7497d-113">hello **Settings** tab is where you can update hello Functions runtime version used by your function app.</span></span> <span data-ttu-id="7497d-114">Também é onde você gerencia Olá host chaves usadas toorestrict HTTP acesso tooall funções hospedadas pelo aplicativo de função hello.</span><span class="sxs-lookup"><span data-stu-id="7497d-114">It is also where you manage hello host keys used toorestrict HTTP access tooall functions hosted by hello function app.</span></span>

<span data-ttu-id="7497d-115">O Functions oferece suporte aos planos de hospedagem de Consumo e Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7497d-115">Functions supports both Consumption hosting and App Service hosting plans.</span></span> <span data-ttu-id="7497d-116">Para obter mais informações, consulte [escolha plano de serviço correta Olá para funções do Azure](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="7497d-116">For more information, see [Choose hello correct service plan for Azure Functions](functions-scale.md).</span></span> <span data-ttu-id="7497d-117">Para aprimorar a previsibilidade no plano de consumo hello, funções permite limitar o uso de plataforma, definindo uma cota de uso diário, em gigabytes segundos.</span><span class="sxs-lookup"><span data-stu-id="7497d-117">For better predictability in hello Consumption plan, Functions lets you limit platform usage by setting a daily usage quota, in gigabytes-seconds.</span></span> <span data-ttu-id="7497d-118">Quando a cota de uso diário de saudação é atingida, Olá função aplicativo está parado.</span><span class="sxs-lookup"><span data-stu-id="7497d-118">Once hello daily usage quota is reached, hello function app is stopped.</span></span> <span data-ttu-id="7497d-119">Um aplicativo de função interrompido como resultado de alcançar Olá gastos cota pode ser habilitado novamente de saudação mesmo contexto de estabelecer Olá diariamente gastos cota.</span><span class="sxs-lookup"><span data-stu-id="7497d-119">A function app stopped as a result of reaching hello spending quota can be re-enabled from hello same context as establishing hello daily spending quota.</span></span> <span data-ttu-id="7497d-120">Consulte Olá [funções do Azure página de preços](http://azure.microsoft.com/pricing/details/functions/) para obter detalhes sobre a cobrança.</span><span class="sxs-lookup"><span data-stu-id="7497d-120">See hello [Azure Functions pricing page](http://azure.microsoft.com/pricing/details/functions/) for details on billing.</span></span>   

## <a name="platform-features-tab"></a><span data-ttu-id="7497d-121">Guia Recursos da plataforma</span><span class="sxs-lookup"><span data-stu-id="7497d-121">Platform features tab</span></span>

![Guia Recursos da plataforma do aplicativo de funções.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-features-tab.png)

<span data-ttu-id="7497d-123">Função aplicativos executados no e são mantidos pela plataforma do serviço de aplicativo do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="7497d-123">Function apps run in, and are maintained, by hello Azure App Service platform.</span></span> <span data-ttu-id="7497d-124">Como tal, seus aplicativos de função tem acesso toomost dos recursos de saudação da plataforma de hospedagem na web do Azure núcleo.</span><span class="sxs-lookup"><span data-stu-id="7497d-124">As such, your function apps have access toomost of hello features of Azure's core web hosting platform.</span></span> <span data-ttu-id="7497d-125">Olá **recursos de plataforma** guia é onde você acesso Olá muitos recursos da saudação plataforma de serviço de aplicativo que você pode usar em seus aplicativos de função.</span><span class="sxs-lookup"><span data-stu-id="7497d-125">hello **Platform features** tab is where you access hello many features of hello App Service platform that you can use in your function apps.</span></span> 

> [!NOTE]
> <span data-ttu-id="7497d-126">Nem todos os recursos do serviço de aplicativo estão disponíveis quando um função de aplicativo é executado no plano de hospedagem de consumo de saudação.</span><span class="sxs-lookup"><span data-stu-id="7497d-126">Not all App Service features are available when a function app runs on hello Consumption hosting plan.</span></span>

<span data-ttu-id="7497d-127">rest Olá deste tópico se concentra em Olá seguintes recursos do serviço de aplicativo hello portal do Azure que são úteis para funções:</span><span class="sxs-lookup"><span data-stu-id="7497d-127">hello rest of this topic focuses on hello following App Service features in hello Azure portal that are useful for Functions:</span></span>

+ [<span data-ttu-id="7497d-128">Editor do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="7497d-128">App Service editor</span></span>](#editor)
+ [<span data-ttu-id="7497d-129">Configurações do aplicativo</span><span class="sxs-lookup"><span data-stu-id="7497d-129">Application settings</span></span>](#settings) 
+ [<span data-ttu-id="7497d-130">Console</span><span class="sxs-lookup"><span data-stu-id="7497d-130">Console</span></span>](#console)
+ [<span data-ttu-id="7497d-131">Ferramentas avançadas (Kudu)</span><span class="sxs-lookup"><span data-stu-id="7497d-131">Advanced tools (Kudu)</span></span>](#kudu)
+ [<span data-ttu-id="7497d-132">Opções de implantação</span><span class="sxs-lookup"><span data-stu-id="7497d-132">Deployment options</span></span>](#deployment)
+ [<span data-ttu-id="7497d-133">CORS</span><span class="sxs-lookup"><span data-stu-id="7497d-133">CORS</span></span>](#cors)
+ [<span data-ttu-id="7497d-134">Autenticação</span><span class="sxs-lookup"><span data-stu-id="7497d-134">Authentication</span></span>](#auth)
+ [<span data-ttu-id="7497d-135">Definição da API</span><span class="sxs-lookup"><span data-stu-id="7497d-135">API definition</span></span>](#swagger)

<span data-ttu-id="7497d-136">Para obter mais informações sobre como toowork com configurações de serviço de aplicativo, consulte [definir configurações de serviço de aplicativo do Azure](../app-service-web/web-sites-configure.md).</span><span class="sxs-lookup"><span data-stu-id="7497d-136">For more information about how toowork with App Service settings, see [Configure Azure App Service Settings](../app-service-web/web-sites-configure.md).</span></span>

### <span data-ttu-id="7497d-137"><a name="editor"></a>Editor de Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="7497d-137"><a name="editor"></a>App Service Editor</span></span>

| | |
|-|-|
| ![Editor do Serviço de Aplicativo do aplicativo de funções.](./media/functions-how-to-use-azure-function-app-settings/function-app-appsvc-editor.png)  | <span data-ttu-id="7497d-139">Olá editor de serviço de aplicativo é um editor no portal avançado que você pode usar arquivos de configuração JSON toomodify e arquivos de código semelhantes.</span><span class="sxs-lookup"><span data-stu-id="7497d-139">hello App Service editor is an advanced in-portal editor that you can use toomodify JSON configuration files and code files alike.</span></span> <span data-ttu-id="7497d-140">Escolher essa opção inicia uma nova guia do navegador com um editor básico.</span><span class="sxs-lookup"><span data-stu-id="7497d-140">Choosing this option launches a separate browser tab with a basic editor.</span></span> <span data-ttu-id="7497d-141">Isso permite que você toointegrate com código de repositório, executar e depurar Git hello e modificar configurações de função do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7497d-141">This enables you toointegrate with hello Git repository, run and debug code, and modify function app settings.</span></span> <span data-ttu-id="7497d-142">Esse editor fornece um ambiente de desenvolvimento aprimoradas para funções, em comparação com folha saudação padrão de função do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7497d-142">This editor provides an enhanced development environment for your functions compared with hello default function app blade.</span></span>    |

![Olá editor de serviço de aplicativo](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-appservice-editor.png)

### <span data-ttu-id="7497d-144"><a name="settings"></a>Configurações do aplicativo</span><span class="sxs-lookup"><span data-stu-id="7497d-144"><a name="settings"></a>Application settings</span></span>

| | |
|-|-|
| ![Configurações de aplicativo do aplicativo de funções.](./media/functions-how-to-use-azure-function-app-settings/function-app-application-settings.png) | <span data-ttu-id="7497d-146">saudação do serviço de aplicativo **configurações de aplicativo** folha é onde você pode configura e gerencia versões do framework, depuração remota, as configurações do aplicativo e cadeias de caracteres de conexão.</span><span class="sxs-lookup"><span data-stu-id="7497d-146">hello App Service **Application settings** blade is where you configure and manage framework versions, remote debugging, app settings, and connection strings.</span></span> <span data-ttu-id="7497d-147">Ao integrar seu aplicativo de funções ao Azure e a outros serviços de terceiros, você pode modificar essas configurações aqui.</span><span class="sxs-lookup"><span data-stu-id="7497d-147">When you integrate your function app with other Azure and third-party services, you can modify those settings here.</span></span> |

![Definir as configurações do aplicativo](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-settings.png)

### <span data-ttu-id="7497d-149"><a name="console"></a>Console</span><span class="sxs-lookup"><span data-stu-id="7497d-149"><a name="console"></a>Console</span></span>

| | |
|-|-|
| ![Console do aplicativo de função no hello portal do Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-console.png) | <span data-ttu-id="7497d-151">console de no portal de saudação é uma ferramenta de desenvolvedor ideal quando você prefere toointeract com seu aplicativo de função na linha de comando hello.</span><span class="sxs-lookup"><span data-stu-id="7497d-151">hello in-portal console is an ideal developer tool when you prefer toointeract with your function app from hello command line.</span></span> <span data-ttu-id="7497d-152">Os comandos comuns incluem criação e navegação de diretório e arquivo, bem como execução scripts e arquivos em lote.</span><span class="sxs-lookup"><span data-stu-id="7497d-152">Common commands include directory and file creation and navigation, as well as executing batch files and scripts.</span></span> |

![Console do aplicativo de funções](./media/functions-how-to-use-azure-function-app-settings/configure-function-console.png)

### <span data-ttu-id="7497d-154"><a name="kudu"></a>Ferramentas avançadas (Kudu)</span><span class="sxs-lookup"><span data-stu-id="7497d-154"><a name="kudu"></a>Advanced tools (Kudu)</span></span>

| | |
|-|-|
| ![Função app Kudu Olá portal do Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-advanced-tools.png) | <span data-ttu-id="7497d-156">Olá ferramentas avançadas para o serviço de aplicativo (também conhecido como Kudu) fornecem acesso a recursos administrativos tooadvanced do seu aplicativo de função.</span><span class="sxs-lookup"><span data-stu-id="7497d-156">hello advanced tools for App Service (also known as Kudu) provide access tooadvanced administrative features of your function app.</span></span> <span data-ttu-id="7497d-157">No Kudu, você pode gerenciar informações do sistema, configurações do aplicativo, variáveis de ambiente, extensões do site, cabeçalhos HTTP e variáveis de servidor.</span><span class="sxs-lookup"><span data-stu-id="7497d-157">From Kudu, you manage system information, app settings, environment variables, site extensions, HTTP headers, and server variables.</span></span> <span data-ttu-id="7497d-158">Você também pode iniciar **Kudu** navegando toohello o ponto de extremidade SCM para seu aplicativo de função, como`https://<myfunctionapp>.scm.azurewebsites.net/`</span><span class="sxs-lookup"><span data-stu-id="7497d-158">You can also launch **Kudu** by browsing toohello SCM endpoint for your function app, like `https://<myfunctionapp>.scm.azurewebsites.net/`</span></span> |

![Configurar Kudu](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-kudu.png)


### <a name="a-namedeploymentdeployment-options"></a><span data-ttu-id="7497d-160"><a name="deployment">Opções de implantação</span><span class="sxs-lookup"><span data-stu-id="7497d-160"><a name="deployment">Deployment options</span></span>

| | |
|-|-|
| ![Opções de implantação de aplicativo de função no hello portal do Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-deployment-source.png) | <span data-ttu-id="7497d-162">O Functions permite que você desenvolva o código de sua função em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="7497d-162">Functions lets you develop your function code on your local machine.</span></span> <span data-ttu-id="7497d-163">Em seguida, você pode carregar seu tooAzure de projeto de aplicativo de função local.</span><span class="sxs-lookup"><span data-stu-id="7497d-163">You can then upload your local function app project tooAzure.</span></span> <span data-ttu-id="7497d-164">Além disso tootraditional de carregamento FTP, funções permite que você implante seu aplicativo de função usando soluções de integração contínua populares, como GitHub, VSTS, Dropbox, Bitbucket e outros.</span><span class="sxs-lookup"><span data-stu-id="7497d-164">In addition tootraditional FTP upload, Functions lets you deploy your function app using popular continuous integration solutions, like GitHub, VSTS, Dropbox, Bitbucket, and others.</span></span> <span data-ttu-id="7497d-165">Para saber mais, confira [Implantação contínua do Azure Functions](functions-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="7497d-165">For more information, see [Continuous deployment for Azure Functions](functions-continuous-deployment.md).</span></span> <span data-ttu-id="7497d-166">tooupload manualmente usando FTP ou Git local, você também deve [configurar suas credenciais de implantação](functions-continuous-deployment.md#credentials).</span><span class="sxs-lookup"><span data-stu-id="7497d-166">tooupload manually using FTP or local Git, you also must [configure your deployment credentials](functions-continuous-deployment.md#credentials).</span></span> |


### <span data-ttu-id="7497d-167"><a name="cors"></a>CORS</span><span class="sxs-lookup"><span data-stu-id="7497d-167"><a name="cors"></a>CORS</span></span>

| | |
|-|-|
| ![Função app CORS Olá portal do Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-cors.png) | <span data-ttu-id="7497d-169">execução de código mal-intencionado tooprevent em seus serviços, blocos de serviço de aplicativo chama tooyour função aplicativos de fontes externas.</span><span class="sxs-lookup"><span data-stu-id="7497d-169">tooprevent malicious code execution in your services, App Service blocks calls tooyour function apps from external sources.</span></span> <span data-ttu-id="7497d-170">Funções dá suporte a recursos entre origens (CORS) toolet definir uma "lista branca" de origens das quais funções podem aceitar solicitações remotas de permissão de compartilhamento.</span><span class="sxs-lookup"><span data-stu-id="7497d-170">Functions supports cross-origin resource sharing (CORS) toolet you define a "whitelist" of allowed origins from which your functions can accept remote requests.</span></span>  |

![Configurar CORS do Aplicativo de funções](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-cors.png)

### <span data-ttu-id="7497d-172"><a name="auth"></a>Autenticação</span><span class="sxs-lookup"><span data-stu-id="7497d-172"><a name="auth"></a>Authentication</span></span>

| | |
|-|-|
| ![Autenticação do aplicativo de função no hello portal do Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-authentication.png) | <span data-ttu-id="7497d-174">Quando as funções usam um gatilho HTTP, você pode exigir chamadas toofirst ser autenticada.</span><span class="sxs-lookup"><span data-stu-id="7497d-174">When functions use an HTTP trigger, you can require calls toofirst be authenticated.</span></span> <span data-ttu-id="7497d-175">O Serviço de Aplicativo oferece suporte à autenticação do Azure Active Directory e a entrada com provedores sociais, como Facebook, Microsoft e Twitter.</span><span class="sxs-lookup"><span data-stu-id="7497d-175">App Service supports Azure Active Directory authentication and sign in with social providers, such as Facebook, Microsoft, and Twitter.</span></span> <span data-ttu-id="7497d-176">Para obter detalhes sobre como configurar provedores de autenticação específicos, consulte [Visão geral de autenticação do serviço de aplicativo do Azure](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7497d-176">For details on configuring specific authentication providers, see [Azure App Service authentication overview](../app-service/app-service-authentication-overview.md).</span></span> |

![Configurar a autenticação para um aplicativo de funções](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-authentication.png)


### <span data-ttu-id="7497d-178"><a name="swagger"></a>Definição da API</span><span class="sxs-lookup"><span data-stu-id="7497d-178"><a name="swagger"></a>API definition</span></span>

| | |
|-|-|
| ![API de função de aplicativo swagger de definição em Olá portal do Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-api-definition.png) | <span data-ttu-id="7497d-180">Oferece suporte a funções Swagger tooallow clientes toomore facilmente consumir funções disparado por HTTP.</span><span class="sxs-lookup"><span data-stu-id="7497d-180">Functions supports Swagger tooallow clients toomore easily consume your HTTP-triggered functions.</span></span> <span data-ttu-id="7497d-181">Para obter mais informações sobre como criar definições de API com Swagger, visite [Introdução aos aplicativos de API, ASP.NET e Swagger no Azure](../app-service-api/app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7497d-181">For more information on creating API definitions with Swagger, visit [Get Started with API Apps, ASP.NET, and Swagger in Azure](../app-service-api/app-service-api-dotnet-get-started.md).</span></span> <span data-ttu-id="7497d-182">Você também pode usar funções Proxies toodefine uma única superfície de API para várias funções.</span><span class="sxs-lookup"><span data-stu-id="7497d-182">You can also use Functions Proxies toodefine a single API surface for multiple functions.</span></span> <span data-ttu-id="7497d-183">Para saber mais, veja [Trabalhar com o Proxies do Azure Functions](functions-proxies.md).</span><span class="sxs-lookup"><span data-stu-id="7497d-183">For more information, see [Working with Azure Functions Proxies](functions-proxies.md).</span></span> |

![Configurar API do Aplicativo de funções](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-apidef.png)



## <a name="next-steps"></a><span data-ttu-id="7497d-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7497d-185">Next steps</span></span>

+ [<span data-ttu-id="7497d-186">Definir configurações do Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="7497d-186">Configure Azure App Service Settings</span></span>](../app-service-web/web-sites-configure.md)
+ [<span data-ttu-id="7497d-187">Implantação contínua para Azure Functions</span><span class="sxs-lookup"><span data-stu-id="7497d-187">Continuous deployment for Azure Functions</span></span>](functions-continuous-deployment.md)



