---
title: "Definir configurações de Aplicativo de funções do Azure | Microsoft Docs"
description: "Saiba como definir configurações de aplicativos do Azure Functions."
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
ms.openlocfilehash: 3b23011f66592151d517d61bf806da8743f38e03
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-manage-a-function-app-in-the-azure-portal"></a><span data-ttu-id="cfc14-103">Como gerenciar um aplicativo de funções no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="cfc14-103">How to manage a function app in the Azure portal</span></span> 

<span data-ttu-id="cfc14-104">No Azure Functions, um aplicativo de funções fornece o contexto de execução para suas funções individuais.</span><span class="sxs-lookup"><span data-stu-id="cfc14-104">In Azure Functions, a function app provides the execution context for your individual functions.</span></span> <span data-ttu-id="cfc14-105">Os comportamentos do aplicativo de funções se aplicam a todas as funções hospedadas por um aplicativo função de determinada.</span><span class="sxs-lookup"><span data-stu-id="cfc14-105">Function app behaviors apply to all functions hosted by a given function app.</span></span> <span data-ttu-id="cfc14-106">Este tópico descreve como configurar e gerenciar seus aplicativos de funções no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="cfc14-106">This topic describes how to configure and manage your function apps in the Azure portal.</span></span>

<span data-ttu-id="cfc14-107">Acesse o [portal do Azure](http://portal.azure.com) e entre usando sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="cfc14-107">To begin, go to the [Azure portal](http://portal.azure.com) and sign in to your Azure account.</span></span> <span data-ttu-id="cfc14-108">Na barra de pesquisa na parte superior do portal, digite o nome de seu aplicativo de funções e selecione-o na lista.</span><span class="sxs-lookup"><span data-stu-id="cfc14-108">In the search bar at the top of the portal, type the name of your function app and select it from the list.</span></span> <span data-ttu-id="cfc14-109">Depois de selecionar o aplicativo de funções, você deverá ver esta página:</span><span class="sxs-lookup"><span data-stu-id="cfc14-109">After selecting your function app, you see the following page:</span></span>

![Visão geral do aplicativo de funções no portal do Azure](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-main.png)

## <span data-ttu-id="cfc14-111"><a name="manage-app-service-settings"></a>Guia Configurações do aplicativo de funções</span><span class="sxs-lookup"><span data-stu-id="cfc14-111"><a name="manage-app-service-settings"></a>Function app settings tab</span></span>

![Visão geral do aplicativo de funções no portal do Azure.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-settings-tab.png)

<span data-ttu-id="cfc14-113">É na guia **Configurações** que você pode atualizar a versão de tempo de execução do Functions usada por seu aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="cfc14-113">The **Settings** tab is where you can update the Functions runtime version used by your function app.</span></span> <span data-ttu-id="cfc14-114">Também é onde você pode gerenciar as chaves de host usadas para restringir o acesso HTTP para todas as funções hospedadas pelo aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="cfc14-114">It is also where you manage the host keys used to restrict HTTP access to all functions hosted by the function app.</span></span>

<span data-ttu-id="cfc14-115">O Functions oferece suporte aos planos de hospedagem de Consumo e Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cfc14-115">Functions supports both Consumption hosting and App Service hosting plans.</span></span> <span data-ttu-id="cfc14-116">Para saber mais, confira [Escolher o plano de serviço correto para o Azure Functions](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="cfc14-116">For more information, see [Choose the correct service plan for Azure Functions](functions-scale.md).</span></span> <span data-ttu-id="cfc14-117">Para aprimorar a previsibilidade no plano de Consumo, o Functions permite a limitação do uso da plataforma por meio da definição de uma cota de uso diário, em gigabytes/segundo.</span><span class="sxs-lookup"><span data-stu-id="cfc14-117">For better predictability in the Consumption plan, Functions lets you limit platform usage by setting a daily usage quota, in gigabytes-seconds.</span></span> <span data-ttu-id="cfc14-118">Assim que a cota diária de uso é atingida, o aplicativo de funções é interrompido.</span><span class="sxs-lookup"><span data-stu-id="cfc14-118">Once the daily usage quota is reached, the function app is stopped.</span></span> <span data-ttu-id="cfc14-119">O aplicativo de funções interrompido como resultado do alcance da cota de gasto pode ser reabilitado no mesmo contexto na definição da cota diária de gasto.</span><span class="sxs-lookup"><span data-stu-id="cfc14-119">A function app stopped as a result of reaching the spending quota can be re-enabled from the same context as establishing the daily spending quota.</span></span> <span data-ttu-id="cfc14-120">Consulte a [página de preços do Azure Functions](http://azure.microsoft.com/pricing/details/functions/) para obter detalhes sobre a cobrança.</span><span class="sxs-lookup"><span data-stu-id="cfc14-120">See the [Azure Functions pricing page](http://azure.microsoft.com/pricing/details/functions/) for details on billing.</span></span>   

## <a name="platform-features-tab"></a><span data-ttu-id="cfc14-121">Guia Recursos da plataforma</span><span class="sxs-lookup"><span data-stu-id="cfc14-121">Platform features tab</span></span>

![Guia Recursos da plataforma do aplicativo de funções.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-features-tab.png)

<span data-ttu-id="cfc14-123">Aplicativos de funções executados e mantidos pela plataforma de Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="cfc14-123">Function apps run in, and are maintained, by the Azure App Service platform.</span></span> <span data-ttu-id="cfc14-124">Dessa forma, seus aplicativos de funções têm acesso à maioria dos recursos da principal plataforma de hospedagem na Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="cfc14-124">As such, your function apps have access to most of the features of Azure's core web hosting platform.</span></span> <span data-ttu-id="cfc14-125">Na guia **Recursos da plataforma** você acessa vários recursos da plataforma de Serviço de Aplicativo para uso em seus aplicativos de funções.</span><span class="sxs-lookup"><span data-stu-id="cfc14-125">The **Platform features** tab is where you access the many features of the App Service platform that you can use in your function apps.</span></span> 

> [!NOTE]
> <span data-ttu-id="cfc14-126">Nem todos os recursos do Serviço de Aplicativo estão disponíveis quando um aplicativo de funções é executado no plano de hospedagem de Consumo.</span><span class="sxs-lookup"><span data-stu-id="cfc14-126">Not all App Service features are available when a function app runs on the Consumption hosting plan.</span></span>

<span data-ttu-id="cfc14-127">O restante deste tópico se concentra nos seguintes recursos de Serviço de Aplicativo do portal do Azure que são úteis para o Functions:</span><span class="sxs-lookup"><span data-stu-id="cfc14-127">The rest of this topic focuses on the following App Service features in the Azure portal that are useful for Functions:</span></span>

+ [<span data-ttu-id="cfc14-128">Editor do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="cfc14-128">App Service editor</span></span>](#editor)
+ [<span data-ttu-id="cfc14-129">Configurações do aplicativo</span><span class="sxs-lookup"><span data-stu-id="cfc14-129">Application settings</span></span>](#settings) 
+ [<span data-ttu-id="cfc14-130">Console</span><span class="sxs-lookup"><span data-stu-id="cfc14-130">Console</span></span>](#console)
+ [<span data-ttu-id="cfc14-131">Ferramentas avançadas (Kudu)</span><span class="sxs-lookup"><span data-stu-id="cfc14-131">Advanced tools (Kudu)</span></span>](#kudu)
+ [<span data-ttu-id="cfc14-132">Opções de implantação</span><span class="sxs-lookup"><span data-stu-id="cfc14-132">Deployment options</span></span>](#deployment)
+ [<span data-ttu-id="cfc14-133">CORS</span><span class="sxs-lookup"><span data-stu-id="cfc14-133">CORS</span></span>](#cors)
+ [<span data-ttu-id="cfc14-134">Autenticação</span><span class="sxs-lookup"><span data-stu-id="cfc14-134">Authentication</span></span>](#auth)
+ [<span data-ttu-id="cfc14-135">Definição da API</span><span class="sxs-lookup"><span data-stu-id="cfc14-135">API definition</span></span>](#swagger)

<span data-ttu-id="cfc14-136">Para saber mais sobre como trabalhar com configurações da Serviço de Aplicativo, confira [Definir configurações do Serviço de Aplicativo do Azure](../app-service-web/web-sites-configure.md).</span><span class="sxs-lookup"><span data-stu-id="cfc14-136">For more information about how to work with App Service settings, see [Configure Azure App Service Settings](../app-service-web/web-sites-configure.md).</span></span>

### <span data-ttu-id="cfc14-137"><a name="editor"></a>Editor de Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="cfc14-137"><a name="editor"></a>App Service Editor</span></span>

| | |
|-|-|
| ![Editor do Serviço de Aplicativo do aplicativo de funções.](./media/functions-how-to-use-azure-function-app-settings/function-app-appsvc-editor.png)  | <span data-ttu-id="cfc14-139">O Editor do Serviço de Aplicativo é um editor avançado dentro do portal que você pode usar para modificar arquivos de configuração JSON e arquivos de código.</span><span class="sxs-lookup"><span data-stu-id="cfc14-139">The App Service editor is an advanced in-portal editor that you can use to modify JSON configuration files and code files alike.</span></span> <span data-ttu-id="cfc14-140">Escolher essa opção inicia uma nova guia do navegador com um editor básico.</span><span class="sxs-lookup"><span data-stu-id="cfc14-140">Choosing this option launches a separate browser tab with a basic editor.</span></span> <span data-ttu-id="cfc14-141">Isso permite que você se integre ao repositório do Git, execute e depure código, além de modificar as configurações do aplicativos de funções.</span><span class="sxs-lookup"><span data-stu-id="cfc14-141">This enables you to integrate with the Git repository, run and debug code, and modify function app settings.</span></span> <span data-ttu-id="cfc14-142">Esse editor fornece um ambiente de desenvolvimento avançado para suas funções em comparação com a folha do aplicativo de funções padrão.</span><span class="sxs-lookup"><span data-stu-id="cfc14-142">This editor provides an enhanced development environment for your functions compared with the default function app blade.</span></span>    |

![O Editor de Serviço de Aplicativo](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-appservice-editor.png)

### <span data-ttu-id="cfc14-144"><a name="settings"></a>Configurações do aplicativo</span><span class="sxs-lookup"><span data-stu-id="cfc14-144"><a name="settings"></a>Application settings</span></span>

| | |
|-|-|
| ![Configurações de aplicativo do aplicativo de funções.](./media/functions-how-to-use-azure-function-app-settings/function-app-application-settings.png) | <span data-ttu-id="cfc14-146">A folha **Configurações do aplicativo** do Serviço de Aplicativo é onde você pode configurar e gerencia versões do framework, a depuração remota, as configurações do aplicativo e cadeias de conexão.</span><span class="sxs-lookup"><span data-stu-id="cfc14-146">The App Service **Application settings** blade is where you configure and manage framework versions, remote debugging, app settings, and connection strings.</span></span> <span data-ttu-id="cfc14-147">Ao integrar seu aplicativo de funções ao Azure e a outros serviços de terceiros, você pode modificar essas configurações aqui.</span><span class="sxs-lookup"><span data-stu-id="cfc14-147">When you integrate your function app with other Azure and third-party services, you can modify those settings here.</span></span> |

![Definir as configurações do aplicativo](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-settings.png)

### <span data-ttu-id="cfc14-149"><a name="console"></a>Console</span><span class="sxs-lookup"><span data-stu-id="cfc14-149"><a name="console"></a>Console</span></span>

| | |
|-|-|
| ![Console do aplicativo de funções no portal do Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-console.png) | <span data-ttu-id="cfc14-151">O console no portal é uma ferramenta ideal de desenvolvimento quando você preferir interagir com seu aplicativo de funções na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="cfc14-151">The in-portal console is an ideal developer tool when you prefer to interact with your function app from the command line.</span></span> <span data-ttu-id="cfc14-152">Os comandos comuns incluem criação e navegação de diretório e arquivo, bem como execução scripts e arquivos em lote.</span><span class="sxs-lookup"><span data-stu-id="cfc14-152">Common commands include directory and file creation and navigation, as well as executing batch files and scripts.</span></span> |

![Console do aplicativo de funções](./media/functions-how-to-use-azure-function-app-settings/configure-function-console.png)

### <span data-ttu-id="cfc14-154"><a name="kudu"></a>Ferramentas avançadas (Kudu)</span><span class="sxs-lookup"><span data-stu-id="cfc14-154"><a name="kudu"></a>Advanced tools (Kudu)</span></span>

| | |
|-|-|
| ![Kudu do aplicativo de funções no portal do Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-advanced-tools.png) | <span data-ttu-id="cfc14-156">As ferramentas avançadas para o Serviço de Aplicativo (também conhecidas como Kudu) fornecem acesso a recursos administrativos avançados de seu aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="cfc14-156">The advanced tools for App Service (also known as Kudu) provide access to advanced administrative features of your function app.</span></span> <span data-ttu-id="cfc14-157">No Kudu, você pode gerenciar informações do sistema, configurações do aplicativo, variáveis de ambiente, extensões do site, cabeçalhos HTTP e variáveis de servidor.</span><span class="sxs-lookup"><span data-stu-id="cfc14-157">From Kudu, you manage system information, app settings, environment variables, site extensions, HTTP headers, and server variables.</span></span> <span data-ttu-id="cfc14-158">Você também pode iniciar o **Kudu** navegando até o ponto de extremidade SCM de seu aplicativo de funções, como`https://<myfunctionapp>.scm.azurewebsites.net/`</span><span class="sxs-lookup"><span data-stu-id="cfc14-158">You can also launch **Kudu** by browsing to the SCM endpoint for your function app, like `https://<myfunctionapp>.scm.azurewebsites.net/`</span></span> |

![Configurar Kudu](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-kudu.png)


### <a name="a-namedeploymentdeployment-options"></a><span data-ttu-id="cfc14-160"><a name="deployment">Opções de implantação</span><span class="sxs-lookup"><span data-stu-id="cfc14-160"><a name="deployment">Deployment options</span></span>

| | |
|-|-|
| ![Opções de implantação do aplicativo de funções no portal do Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-deployment-source.png) | <span data-ttu-id="cfc14-162">O Functions permite que você desenvolva o código de sua função em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="cfc14-162">Functions lets you develop your function code on your local machine.</span></span> <span data-ttu-id="cfc14-163">Depois, você pode carregar seu projeto de aplicativo de funções local no Azure.</span><span class="sxs-lookup"><span data-stu-id="cfc14-163">You can then upload your local function app project to Azure.</span></span> <span data-ttu-id="cfc14-164">Além do carregamento FTP tradicional, o Functions permite que você implante seu aplicativo de funções usando soluções de integração contínua populares, como GitHub, VSTS, Dropbox, Bitbucket e outros.</span><span class="sxs-lookup"><span data-stu-id="cfc14-164">In addition to traditional FTP upload, Functions lets you deploy your function app using popular continuous integration solutions, like GitHub, VSTS, Dropbox, Bitbucket, and others.</span></span> <span data-ttu-id="cfc14-165">Para saber mais, confira [Implantação contínua do Azure Functions](functions-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="cfc14-165">For more information, see [Continuous deployment for Azure Functions](functions-continuous-deployment.md).</span></span> <span data-ttu-id="cfc14-166">Para carregar manualmente usando FTP ou Git local, você deve também [configurar suas credenciais de implantação](functions-continuous-deployment.md#credentials).</span><span class="sxs-lookup"><span data-stu-id="cfc14-166">To upload manually using FTP or local Git, you also must [configure your deployment credentials](functions-continuous-deployment.md#credentials).</span></span> |


### <span data-ttu-id="cfc14-167"><a name="cors"></a>CORS</span><span class="sxs-lookup"><span data-stu-id="cfc14-167"><a name="cors"></a>CORS</span></span>

| | |
|-|-|
| ![CORS do aplicativo de funções no portal do Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-cors.png) | <span data-ttu-id="cfc14-169">Para impedir a execução de código mal-intencionado em seus serviços, o Serviço de Aplicativo bloqueia chamadas para seus aplicativos de funções de fontes externas.</span><span class="sxs-lookup"><span data-stu-id="cfc14-169">To prevent malicious code execution in your services, App Service blocks calls to your function apps from external sources.</span></span> <span data-ttu-id="cfc14-170">O Functions oferece suporte a CORS (compartilhamento de recursos entre origens) para permitir que você defina uma "lista de permissão" com as origens permitidas das quais suas funções podem aceitar solicitações remotas.</span><span class="sxs-lookup"><span data-stu-id="cfc14-170">Functions supports cross-origin resource sharing (CORS) to let you define a "whitelist" of allowed origins from which your functions can accept remote requests.</span></span>  |

![Configurar CORS do Aplicativo de funções](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-cors.png)

### <span data-ttu-id="cfc14-172"><a name="auth"></a>Autenticação</span><span class="sxs-lookup"><span data-stu-id="cfc14-172"><a name="auth"></a>Authentication</span></span>

| | |
|-|-|
| ![Autenticação do aplicativo de funções no portal do Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-authentication.png) | <span data-ttu-id="cfc14-174">Quando as funções usam um gatilho HTTP, você pode exigir que as chamadas sejam autenticadas primeiro.</span><span class="sxs-lookup"><span data-stu-id="cfc14-174">When functions use an HTTP trigger, you can require calls to first be authenticated.</span></span> <span data-ttu-id="cfc14-175">O Serviço de Aplicativo oferece suporte à autenticação do Azure Active Directory e a entrada com provedores sociais, como Facebook, Microsoft e Twitter.</span><span class="sxs-lookup"><span data-stu-id="cfc14-175">App Service supports Azure Active Directory authentication and sign in with social providers, such as Facebook, Microsoft, and Twitter.</span></span> <span data-ttu-id="cfc14-176">Para obter detalhes sobre como configurar provedores de autenticação específicos, consulte [Visão geral de autenticação do serviço de aplicativo do Azure](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cfc14-176">For details on configuring specific authentication providers, see [Azure App Service authentication overview](../app-service/app-service-authentication-overview.md).</span></span> |

![Configurar a autenticação para um aplicativo de funções](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-authentication.png)


### <span data-ttu-id="cfc14-178"><a name="swagger"></a>Definição da API</span><span class="sxs-lookup"><span data-stu-id="cfc14-178"><a name="swagger"></a>API definition</span></span>

| | |
|-|-|
| ![Definição de swagger da API do aplicativo de funções no portal do Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-api-definition.png) | <span data-ttu-id="cfc14-180">O Functions oferece suporte ao Swagger para permitir que os clientes consumam mais facilmente suas funções disparadas por HTTP.</span><span class="sxs-lookup"><span data-stu-id="cfc14-180">Functions supports Swagger to allow clients to more easily consume your HTTP-triggered functions.</span></span> <span data-ttu-id="cfc14-181">Para obter mais informações sobre como criar definições de API com Swagger, visite [Introdução aos aplicativos de API, ASP.NET e Swagger no Azure](../app-service-api/app-service-api-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="cfc14-181">For more information on creating API definitions with Swagger, visit [Get Started with API Apps, ASP.NET, and Swagger in Azure](../app-service-api/app-service-api-dotnet-get-started.md).</span></span> <span data-ttu-id="cfc14-182">Você também pode usar os Proxies do Functions para definir uma única superfície de API para várias funções.</span><span class="sxs-lookup"><span data-stu-id="cfc14-182">You can also use Functions Proxies to define a single API surface for multiple functions.</span></span> <span data-ttu-id="cfc14-183">Para saber mais, veja [Trabalhar com o Proxies do Azure Functions](functions-proxies.md).</span><span class="sxs-lookup"><span data-stu-id="cfc14-183">For more information, see [Working with Azure Functions Proxies](functions-proxies.md).</span></span> |

![Configurar API do Aplicativo de funções](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-apidef.png)



## <a name="next-steps"></a><span data-ttu-id="cfc14-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cfc14-185">Next steps</span></span>

+ [<span data-ttu-id="cfc14-186">Definir configurações do Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="cfc14-186">Configure Azure App Service Settings</span></span>](../app-service-web/web-sites-configure.md)
+ [<span data-ttu-id="cfc14-187">Implantação contínua para Azure Functions</span><span class="sxs-lookup"><span data-stu-id="cfc14-187">Continuous deployment for Azure Functions</span></span>](functions-continuous-deployment.md)



