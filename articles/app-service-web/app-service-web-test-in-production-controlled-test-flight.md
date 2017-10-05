---
title: "Implantação flighting (teste beta) no Serviço de Aplicativo do Azure"
description: "Saiba como realizar a implantação flighting de novos recursos em seu aplicativo ou realizar teste beta em suas atualizações neste tutorial completo. Ele reúne os recursos do Serviço de Aplicativo como publicação contínua, slots, roteamento de tráfego e integração do Application Insights."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 17953c51-38f8-442d-bb0b-f69c1542f0e9
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/02/2016
ms.author: cephalin
ms.openlocfilehash: 83e3247310461ac148fff3c4ade3aa7216478537
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="flighting-deployment-beta-testing-in-azure-app-service"></a><span data-ttu-id="ce0d4-104">Implantação flighting (teste beta) no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="ce0d4-104">Flighting deployment (beta testing) in Azure App Service</span></span>
<span data-ttu-id="ce0d4-105">Este tutorial mostra como realizar *implantações de liberação de versões de pré-lançamento* integrando os vários recursos do [Serviço de Aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) e do [Azure Application Insights](/services/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="ce0d4-105">This tutorial shows you how to do *flighting deployments* by integrating the various capabilities of [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) and [Azure Application Insights](/services/application-insights/).</span></span>

<span data-ttu-id="ce0d4-106">*Flighting* é um processo de implantação que valida um novo recurso ou alteração com um número limitado de clientes reais, e é um teste importante no cenário de produção.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-106">*Flighting* is a deployment process that validates a new feature or change with a limited number of real customers, and is a major testing in production scenario.</span></span> <span data-ttu-id="ce0d4-107">É semelhante ao teste beta e às vezes é conhecido como “voo de teste controlado”.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-107">It is akin to beta testing and is sometimes known as "controlled test flight".</span></span> <span data-ttu-id="ce0d4-108">Muitas grandes empresas com uma presença na Web usam essa abordagem para obter validação antecipada sobre suas atualizações de aplicativo em sua prática de [desenvolvimento ágil](https://en.wikipedia.org/wiki/Agile_software_development).</span><span class="sxs-lookup"><span data-stu-id="ce0d4-108">Many large enterprises with a web presence use this approach to get early validation on their app updates in their practice of [agile development](https://en.wikipedia.org/wiki/Agile_software_development).</span></span> <span data-ttu-id="ce0d4-109">O Serviço de Aplicativo do Azure permite a integração de teste em produção com a publicação contínua e o Application Insights para implementar o mesmo cenário de DevOps.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-109">Azure App Service enables you to integrate test in production with continous publishing and Application Insights to implement the same DevOps scenario.</span></span> <span data-ttu-id="ce0d4-110">Entre os benefícios dessa abordagem estão:</span><span class="sxs-lookup"><span data-stu-id="ce0d4-110">Benefits of this approach include:</span></span>

* <span data-ttu-id="ce0d4-111">**Obtenha comentários reais *antes* que as atualizações sejam lançadas na produção** - a única coisa melhor do que obter comentários após o lançamento é obter comentários antes dele.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-111">**Gain real feedback *before* updates are released to production** - The only thing better than gaining feedback as soon as you release is gaining feedback before you release.</span></span> <span data-ttu-id="ce0d4-112">Você pode testar atualizações com o tráfego e comportamentos de usuário real em qualquer etapa desejada do ciclo de vida do produto.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-112">You can test updates with real user traffic and behaviors as early as you desire in the product life cycle.</span></span>
* <span data-ttu-id="ce0d4-113">**Aprimore o [CTDD (desenvolvimento contínuo controlado por testes)](https://en.wikipedia.org/wiki/Continuous_test-driven_development)** - ao integrar o teste em produção com a integração e instrumentação contínuas com o Application Insights, a validação do usuário ocorre automaticamente e desde o início do ciclo de vida do produto.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-113">**Enhance [continuous test-driven development (CTDD)](https://en.wikipedia.org/wiki/Continuous_test-driven_development)** - By integrating test in production with continuous integration and instrumentation with Application Insights, user validation happens early and automatically in your product life cycle.</span></span> <span data-ttu-id="ce0d4-114">Isso ajuda a reduzir os investimentos em tempo na execução de teste manual.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-114">This helps reduce time investments in manual test execution.</span></span>
* <span data-ttu-id="ce0d4-115">**Otimizar o fluxo de trabalho de teste** - ao automatizar o teste em produção com a instrumentação de monitoramento contínuo, é possível potencialmente atingir os objetivos de vários tipos de testes em um único processo, como [integração](https://en.wikipedia.org/wiki/Integration_testing), [regressão](https://en.wikipedia.org/wiki/Regression_testing), [usabilidade](https://en.wikipedia.org/wiki/Usability_testing), acessibilidade, localização, [desempenho](https://en.wikipedia.org/wiki/Software_performance_testing), [segurança](https://en.wikipedia.org/wiki/Security_testing) e[ aceitação](https://en.wikipedia.org/wiki/Acceptance_testing).</span><span class="sxs-lookup"><span data-stu-id="ce0d4-115">**Optimize test workflow** - By automating test in production with continuous monitoring instrumentation, you can potentially accomplish the goals of various kinds of tests in a single process, such as [integration](https://en.wikipedia.org/wiki/Integration_testing), [regression](https://en.wikipedia.org/wiki/Regression_testing), [usability](https://en.wikipedia.org/wiki/Usability_testing), accessibility, localization, [performance](https://en.wikipedia.org/wiki/Software_performance_testing), [security](https://en.wikipedia.org/wiki/Security_testing), and [acceptance](https://en.wikipedia.org/wiki/Acceptance_testing).</span></span>

<span data-ttu-id="ce0d4-116">Uma implantação flighting não se trata apenas do roteamento de tráfego em tempo real.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-116">A flighting deployment is not just about routing live traffic.</span></span> <span data-ttu-id="ce0d4-117">Nesse tipo de implantação, você deseja obter informações o mais rápido possível, seja um bug inesperado, degradação de desempenho ou problemas de experiência do usuário.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-117">In such a deployment you want to gain insight as quickly as possible, whether it be an unexpected bug, performance degradation, user experience issues.</span></span> <span data-ttu-id="ce0d4-118">Lembre-se de que você está lidando com clientes reais.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-118">Remember, you are dealing with real customers.</span></span> <span data-ttu-id="ce0d4-119">Portanto, para fazer isso da maneira certa, certifique-se de que você configurou sua implantação flighting para coletar todos os dados necessários para tomar uma decisão informada para a próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-119">So to do it right, you must make sure that you have set up your flighting deployment to gather all the data you need in order to make an informed decision for your next step.</span></span> <span data-ttu-id="ce0d4-120">Este tutorial mostra como coletar dados com o Application Insights, mas você pode usar o New Relic ou outras tecnologias que se adaptem ao seu cenário.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-120">This tutorial shows you how to collect data with Application Insights, but you can use New Relic or other technologies that suits your scenario.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="ce0d4-121">O que você fará</span><span class="sxs-lookup"><span data-stu-id="ce0d4-121">What you will do</span></span>
<span data-ttu-id="ce0d4-122">Neste tutorial, você aprenderá a reunir os seguintes cenários para testar seu aplicativo do Serviço de Aplicativo em produção:</span><span class="sxs-lookup"><span data-stu-id="ce0d4-122">In this tutorial, you will learn how to bring the following scenarios together to test your App Service app in production:</span></span>

* <span data-ttu-id="ce0d4-123">[Encaminhar o tráfego de produção](app-service-web-test-in-production-get-start.md) para o seu aplicativo beta</span><span class="sxs-lookup"><span data-stu-id="ce0d4-123">[Route production traffic](app-service-web-test-in-production-get-start.md) to your beta app</span></span>
* <span data-ttu-id="ce0d4-124">[Instrumentar seu aplicativo](../application-insights/app-insights-web-track-usage.md) para obter métricas úteis</span><span class="sxs-lookup"><span data-stu-id="ce0d4-124">[Instrument your app](../application-insights/app-insights-web-track-usage.md) to obtain useful metrics</span></span>
* <span data-ttu-id="ce0d4-125">Implantar continuamente seu aplicativo beta e rastrear métricas de aplicativo em tempo real</span><span class="sxs-lookup"><span data-stu-id="ce0d4-125">Continuously deploy your beta app and track live app metrics</span></span>
* <span data-ttu-id="ce0d4-126">Compare as métricas entre o aplicativo de produção e o aplicativo de beta para ver como as alterações de código são convertidas para resultados</span><span class="sxs-lookup"><span data-stu-id="ce0d4-126">Compare metrics between the production app and the beta app to see how code changes translate to results</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="ce0d4-127">O que será necessário</span><span class="sxs-lookup"><span data-stu-id="ce0d4-127">What you will need</span></span>
* <span data-ttu-id="ce0d4-128">Uma conta do Azure</span><span class="sxs-lookup"><span data-stu-id="ce0d4-128">An Azure account</span></span>
* <span data-ttu-id="ce0d4-129">Uma conta do [GitHub](https://github.com/)</span><span class="sxs-lookup"><span data-stu-id="ce0d4-129">A [GitHub](https://github.com/) account</span></span>
* <span data-ttu-id="ce0d4-130">Visual Studio 2015 - você pode baixar a [Community edition](https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="ce0d4-130">Visual Studio 2015 - you can download the [Community edition](https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx).</span></span>
* <span data-ttu-id="ce0d4-131">Git Shell (instalado com o [GitHub para Windows](https://windows.github.com/)) – isso permite que você execute comandos do Git e do PowerShell na mesma sessão</span><span class="sxs-lookup"><span data-stu-id="ce0d4-131">Git Shell (installed with [GitHub for Windows](https://windows.github.com/)) - this enables you to run both the Git and PowerShell commands in the same session</span></span>
* <span data-ttu-id="ce0d4-132">Bits do [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi) mais recentes</span><span class="sxs-lookup"><span data-stu-id="ce0d4-132">Latest [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi) bits</span></span>
* <span data-ttu-id="ce0d4-133">Noções básicas sobre:</span><span class="sxs-lookup"><span data-stu-id="ce0d4-133">Basic understanding of the following:</span></span>
  * <span data-ttu-id="ce0d4-134">Implantação do modelo do [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) (veja [Implantar um aplicativo complexo de modo previsível no Azure](app-service-deploy-complex-application-predictably.md))</span><span class="sxs-lookup"><span data-stu-id="ce0d4-134">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) template deployment (see [Deploy a complex application predictably in Azure](app-service-deploy-complex-application-predictably.md))</span></span>
  * [<span data-ttu-id="ce0d4-135">Git</span><span class="sxs-lookup"><span data-stu-id="ce0d4-135">Git</span></span>](http://git-scm.com/documentation)
  * [<span data-ttu-id="ce0d4-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ce0d4-136">PowerShell</span></span>](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> <span data-ttu-id="ce0d4-137">Você de uma conta do Azure para concluir este tutorial:</span><span class="sxs-lookup"><span data-stu-id="ce0d4-137">You need an Azure account to complete this tutorial:</span></span>
>
> * <span data-ttu-id="ce0d4-138">É possível [abrir uma conta do Azure gratuitamente](https://azure.microsoft.com/pricing/free-trial/) – você obtém créditos que podem ser usados para experimentar serviços pagos do Azure e, mesmo após eles serem utilizados, é possível manter a conta e utilizar os serviços gratuitos do Azure, como Aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-138">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services, such as Web Apps.</span></span>
> * <span data-ttu-id="ce0d4-139">É possível [ativar os benefícios para assinantes do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) – todos os meses, sua assinatura do Visual Studio concede créditos que podem ser usados para experimentar serviços pagos do Azure.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-139">You can [activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) - Your Visual Studio subscription gives you credits every month that you can use for paid Azure services.</span></span>
>
> <span data-ttu-id="ce0d4-140">Se você deseja começar com o Serviço de Aplicativo do Azure antes de se inscrever em uma conta do Azure, vá até [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/), em que você pode criar imediatamente um aplicativo Web inicial de curta duração no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-140">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="ce0d4-141">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-141">No credit cards required; no commitments.</span></span>
>
>

## <a name="set-up-your-production-web-app"></a><span data-ttu-id="ce0d4-142">Configurar seu aplicativo Web de produção</span><span class="sxs-lookup"><span data-stu-id="ce0d4-142">Set up your production web app</span></span>
> [!NOTE]
> <span data-ttu-id="ce0d4-143">O script usado neste tutorial configurará automaticamente a publicação contínua de seu repositório GitHub.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-143">The script used in this tutorial will automatically configure continuous publishing from your GitHub repository.</span></span> <span data-ttu-id="ce0d4-144">Isso requer que as credenciais do GitHub já estejam armazenadas no Azure; caso contrário, a implantação de scripts falhará ao tentar definir configurações de controle de origem para aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-144">This requires that your GitHub credentials are already stored in Azure, otherwise the scripted deployment will fail when attempting to configure source control settings for the web apps.</span></span>
>
> <span data-ttu-id="ce0d4-145">Para armazenar suas credenciais do GitHub no Azure, crie um aplicativo Web no [Portal do Azure](https://portal.azure.com/) e [configure a implantação do GitHub](app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="ce0d4-145">To store your GitHub credentials in Azure, create a web app in the [Azure Portal](https://portal.azure.com/) and [configure GitHub deployment](app-service-continuous-deployment.md).</span></span> <span data-ttu-id="ce0d4-146">Você só precisa fazer isso uma vez.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-146">You only need to do this once.</span></span>
>
>

<span data-ttu-id="ce0d4-147">Em um cenário típico de DevOps, você tem um aplicativo que está em execução em tempo real no Azure e deseja fazer alterações nele por meio de publicação contínua.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-147">In a typical DevOps scenario, you have an application that’s running live in Azure, and you want to make changes to it through continuous publishing.</span></span> <span data-ttu-id="ce0d4-148">Neste cenário, você implantará na produção um modelo que você desenvolveu e testou.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-148">In this scenario, you will deploy to production a template that you have developed and tested.</span></span>

1. <span data-ttu-id="ce0d4-149">Crie sua própria bifurcação do repositório do [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) .</span><span class="sxs-lookup"><span data-stu-id="ce0d4-149">Create your own fork of the [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) repository.</span></span> <span data-ttu-id="ce0d4-150">Para obter informações sobre como criar a bifurcação, consulte [Bifurcar um repositório](https://help.github.com/articles/fork-a-repo/).</span><span class="sxs-lookup"><span data-stu-id="ce0d4-150">For information on creating your fork, see [Fork a Repo](https://help.github.com/articles/fork-a-repo/).</span></span> <span data-ttu-id="ce0d4-151">Depois que a bifurcação é criada, você pode vê-la no navegador.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-151">Once your fork is created, you can see it in your browser.</span></span>

   ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. <span data-ttu-id="ce0d4-152">Abra uma sessão do Git Shell.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-152">Open a Git Shell session.</span></span> <span data-ttu-id="ce0d4-153">Se ainda não tiver o Git Shell, instale o [GitHub para Windows](https://windows.github.com/) agora.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-153">If you don't have Git Shell yet, install [GitHub for Windows](https://windows.github.com/) now.</span></span>
3. <span data-ttu-id="ce0d4-154">Crie um clone local de seu bifurcação executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="ce0d4-154">Create a local clone of your fork by executing the following command:</span></span>

     <span data-ttu-id="ce0d4-155">git clone https://github.com/<your_fork>/ToDoApp.git</span><span class="sxs-lookup"><span data-stu-id="ce0d4-155">git clone https://github.com/<your_fork>/ToDoApp.git</span></span>
4. <span data-ttu-id="ce0d4-156">Depois que tiver seu clone local, navegue até a *&lt;raiz_do_repositório>*\ARMTemplates e execute o script deploy.ps1 com um sufixo exclusivo, como mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="ce0d4-156">Once you have your local clone, navigate to *&lt;repository_root>*\ARMTemplates, and run the deploy.ps1 script with a unique suffix, as shown below:</span></span>

     <span data-ttu-id="ce0d4-157">.\deploy.ps1 –RepoUrl https://github.com/<your_fork>/todoapp.git -ResourceGroupSuffix <your_suffix></span><span class="sxs-lookup"><span data-stu-id="ce0d4-157">.\deploy.ps1 –RepoUrl https://github.com/<your_fork>/todoapp.git -ResourceGroupSuffix <your_suffix></span></span>
5. <span data-ttu-id="ce0d4-158">Quando solicitado, digite o nome de usuário desejado e a senha para acesso ao banco de dados.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-158">When prompted, type in the desired username and password for database access.</span></span> <span data-ttu-id="ce0d4-159">Lembre-se de suas credenciais do banco de dados, porque você precisará especificá-las novamente ao atualizar o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-159">Remember your database credentials because you will need to specify them again when updating the resource group.</span></span>

   <span data-ttu-id="ce0d4-160">Você deverá ver o progresso de provisionamento de vários recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-160">You should see the provisioning progress of various Azure resources.</span></span> <span data-ttu-id="ce0d4-161">Quando a implantação for concluída, o script iniciará o aplicativo no navegador e emitirá um aviso sonoro.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-161">When deployment completes, the script will launch the application in the browser and give you a friendly beep.</span></span>
   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.1-app-in-browser.png)
6. <span data-ttu-id="ce0d4-162">De volta à sessão do Git Shell, execute:</span><span class="sxs-lookup"><span data-stu-id="ce0d4-162">Back in your Git Shell session, run:</span></span>

     <span data-ttu-id="ce0d4-163">.\swap –Name ToDoApp<your_suffix></span><span class="sxs-lookup"><span data-stu-id="ce0d4-163">.\swap –Name ToDoApp<your_suffix></span></span>

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.2-swap-to-production.png)
7. <span data-ttu-id="ce0d4-164">Quando o script for concluído, volte para navegar até endereço do front-end (http://ToDoApp*&lt;seu_sufixo>*.azurewebsites.net/) para ver o aplicativo em execução na produção.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-164">When the script finishes, go back to browse to the frontend’s address (http://ToDoApp*&lt;your_suffix>*.azurewebsites.net/) to see the application running in production.</span></span>
8. <span data-ttu-id="ce0d4-165">Faça logon no [Portal do Azure](https://portal.azure.com/) e veja o que foi criado.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-165">Log into the [Azure Portal](https://portal.azure.com/) and take a look at what’s created.</span></span>

   <span data-ttu-id="ce0d4-166">Você deverá ver dois aplicativos Web no mesmo grupo de recursos, um com o sufixo `Api` no nome.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-166">You should be able to see two web apps in the same resource group, one with the `Api` suffix in the name.</span></span> <span data-ttu-id="ce0d4-167">Se examinar o modo de exibição do grupo de recursos, você também verá o banco de dados SQL e o servidor, o plano do Serviço de Aplicativo e os slots de preparo dos aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-167">If you look at the resource group view, you will also see the SQL Database and server, the App Service plan, and the staging slots for the web apps.</span></span> <span data-ttu-id="ce0d4-168">Navegue pelos diferentes recursos e compare-os com *&lt;raiz_do_repositório>*\ARMTemplates\ProdAndStage.json para ver como eles são configurados no modelo.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-168">Browse through the different resources and compare them with *&lt;repository_root>*\ARMTemplates\ProdAndStage.json to see how they are configured in the template.</span></span>

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.3-resource-group-view.png)

<span data-ttu-id="ce0d4-169">Você configurou o aplicativo de produção.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-169">You have set up the production app.</span></span>  <span data-ttu-id="ce0d4-170">Agora, vamos imaginar que você receba comentários de que a usabilidade é insatisfatória para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-170">Now, let's imagine that you receive feedback that usability is poor for the app.</span></span> <span data-ttu-id="ce0d4-171">Portanto, você decide investigar.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-171">So you decide to investigate.</span></span> <span data-ttu-id="ce0d4-172">Você instrumentará seu aplicativo para que ele forneça comentários.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-172">You're going to instrument your app to give you feedback.</span></span>

## <a name="investigate-instrument-your-client-app-for-monitoringmetrics"></a><span data-ttu-id="ce0d4-173">Investigue: instrumentar o aplicativo cliente para monitoramento/métricas</span><span class="sxs-lookup"><span data-stu-id="ce0d4-173">Investigate: Instrument your client app for monitoring/metrics</span></span>
1. <span data-ttu-id="ce0d4-174">Abra *&lt;raiz_do-repositório>*\src\MultiChannelToDo.sln in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-174">Open *&lt;repository_root>*\src\MultiChannelToDo.sln in Visual Studio.</span></span>
2. <span data-ttu-id="ce0d4-175">Restaure todos os pacotes NuGet clicando com o botão direito do mouse na solução > **Gerenciar Pacotes NuGet da Solução** > **Restaurar**.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-175">Restore all Nuget packages by right-clicking solution > **Manage NuGet Packages for Solution** > **Restore**.</span></span>
3. <span data-ttu-id="ce0d4-176">Clique com o botão direito do mouse em **MultiChannelToDo.Web** > **Adicionar Application Insights Telemetry** > **Definir Configurações** > Alterar grupo de recursos para ToDoApp*&lt;seu_sufixo>* > **Adicionar Application Insights ao Projeto**.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-176">Right-click **MultiChannelToDo.Web** > **Add Application Insights Telemetry** > **Configure Settings** > Change resource group to ToDoApp*&lt;your_suffix>* > **Add Application Insights to Project**.</span></span>
4. <span data-ttu-id="ce0d4-177">No Portal do Azure, abra a folha do recurso **MultiChannelToDo.Web** do Application Insight.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-177">In the Azure Portal, open the blade for the **MultiChannelToDo.Web** Application Insight resource.</span></span> <span data-ttu-id="ce0d4-178">Em seguida, na seção **Integridade do aplicativo**, clique em **Saiba como coletar dados de carregamento da página do navegador** > copiar código.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-178">Then in the **Application health** part, click **Learn how to collect browser page load data** > copy code.</span></span>
5. <span data-ttu-id="ce0d4-179">Adicione o código de instrumentação JS copiado à *&lt;raiz_repositório>*\src\MultiChannelToDo.Web\app\Index.cshtml, logo antes da marca `<heading>` de fechamento.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-179">Add the copied JS instrumentation code to *&lt;repository_root>*\src\MultiChannelToDo.Web\app\Index.cshtml, just before the closing `<heading>` tag.</span></span> <span data-ttu-id="ce0d4-180">Ele deve conter a chave exclusiva de instrumentação do recurso do Application Insight.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-180">It should contain the unique instrumentation key of your Application Insight resource.</span></span>

        <script type="text/javascript">
        var appInsights=window.appInsights||function(config){
            function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
        }({
            instrumentationKey:"<your_unique_instrumentation_key>"
        });

        window.appInsights=appInsights;
        appInsights.trackPageView();
        </script>
6. <span data-ttu-id="ce0d4-181">Envie eventos personalizados para o Application Insights para cliques do mouse adicionando o seguinte código à parte inferior do corpo:</span><span class="sxs-lookup"><span data-stu-id="ce0d4-181">Send custom events to Application Insights for mouse clicks by adding the following code to the bottom of body:</span></span>

       <script>
           $(document.body).find("*").click(function(event) {

               appInsights.trackEvent(event.target.tagName + ": " + event.target.className);
           });
       </script>

   <span data-ttu-id="ce0d4-182">Este trecho de código em JavaScript envia um evento personalizado para o Application Insights sempre que um usuário clica em algum lugar no aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-182">This JavaScript snippet sends a custom event to Application Insights every time a user clicks anywhere in the web app.</span></span>
7. <span data-ttu-id="ce0d4-183">No Git Shell, confirme e envie por push as alterações à bifurcação no GitHub.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-183">In Git Shell, commit and push your changes to your fork in GitHub.</span></span> <span data-ttu-id="ce0d4-184">Em seguida, aguarde até que os clientes atualizem o navegador.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-184">Then, wait for clients to refresh browser.</span></span>

       git add -A :/
       git commit -m "add AI configuration for client app"
       git push origin master
8. <span data-ttu-id="ce0d4-185">Alterne as alterações do aplicativo implantado para a produção:</span><span class="sxs-lookup"><span data-stu-id="ce0d4-185">Swap the deployed app changes to production:</span></span>

     <span data-ttu-id="ce0d4-186">.\swap –Name ToDoApp<your_suffix></span><span class="sxs-lookup"><span data-stu-id="ce0d4-186">.\swap –Name ToDoApp<your_suffix></span></span>
9. <span data-ttu-id="ce0d4-187">Navegue até o recurso do Application Insights que você configurou.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-187">Browse to the Application Insights resource that you configured.</span></span> <span data-ttu-id="ce0d4-188">Clique em Eventos personalizados.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-188">Click Custom events.</span></span>

   ![](./media/app-service-web-test-in-production-controlled-test-flight/01-custom-events.png)

   <span data-ttu-id="ce0d4-189">Se você não vir as métricas para eventos personalizados, aguarde alguns minutos e clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-189">If you don't see metrics for custom events, wait a few minutes and click **Refresh**.</span></span>

<span data-ttu-id="ce0d4-190">Suponha que você veja um gráfico como o mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="ce0d4-190">Suppose you see a chart like below:</span></span>

![](./media/app-service-web-test-in-production-controlled-test-flight/02-custom-events-chart-view.png)

<span data-ttu-id="ce0d4-191">E a grade de eventos abaixo dele:</span><span class="sxs-lookup"><span data-stu-id="ce0d4-191">And the event grid below it:</span></span>

![](./media/app-service-web-test-in-production-controlled-test-flight/03-custom-event-grid-view.png)

<span data-ttu-id="ce0d4-192">De acordo com o código do aplicativo ToDoApp, o evento **BUTTON** corresponde ao botão Enviar e o evento **INPUT** corresponde à caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-192">According to your ToDoApp application code, the **BUTTON** event corresponds to the submit button, and the **INPUT** event corresponds to the textbox.</span></span> <span data-ttu-id="ce0d4-193">Até agora, as coisas fazem sentido.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-193">So far, things make sense.</span></span> <span data-ttu-id="ce0d4-194">No entanto, parece que há uma boa quantidade de cliques e muito poucos cliques nos itens de tarefas pendentes (os eventos **LI** ).</span><span class="sxs-lookup"><span data-stu-id="ce0d4-194">However, it looks like there's a good amount of clicks and very few clicks on the to-do items (the **LI** events).</span></span>

<span data-ttu-id="ce0d4-195">Com base nisso, você forma a hipótese de que alguns usuários estão confusos sobre qual parte da interface do usuário é clicável, e isso ocorre porque o cursor tem o estilo de seleção de texto quando ele é passado sobre os itens da lista e seus ícones.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-195">Based on this, you form your hypothesis that some users are confused which part of the UI is clickable and it is because the cursor is styled for text selection when it hovers on the list items and their icons.</span></span>

![](./media/app-service-web-test-in-production-controlled-test-flight/04-to-do-list-item-ui.png)

<span data-ttu-id="ce0d4-196">Isso pode ser um exemplo forçado.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-196">This might be a contrived example.</span></span> <span data-ttu-id="ce0d4-197">No entanto, você fará uma melhoria em seu aplicativo e realizará uma implantação flighting para obter comentários de usabilidade dos clientes em tempo real.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-197">Nevertheless, you're going to make an improvement to your app, and then perform a flighting deployment to get usability feedback from live customers.</span></span>

### <a name="instrument-your-server-app-for-monitoringmetrics"></a><span data-ttu-id="ce0d4-198">Instrumentar seu aplicativo de servidor para monitoramento/métricas</span><span class="sxs-lookup"><span data-stu-id="ce0d4-198">Instrument your server app for monitoring/metrics</span></span>
<span data-ttu-id="ce0d4-199">Essa é uma tangente, pois o cenário demonstrado neste tutorial lida apenas com o aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-199">This is a tangent since the scenario demonstrated in this tutorial only deals with the client app.</span></span> <span data-ttu-id="ce0d4-200">No entanto, para fins de integridade, você configurará o aplicativo do lado do servidor.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-200">However, for completeness you will set up the server-side app.</span></span>

1. <span data-ttu-id="ce0d4-201">Clique com o botão direito do mouse em **MultiChannelToDo** > **Adicionar Application Insights Telemetry** > **Definir Configurações** > Alterar grupo de recursos para ToDoApp*&lt;seu_sufixo>* > **Adicionar Application Insights ao Projeto**.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-201">Right-click **MultiChannelToDo** > **Add Application Insights Telemetry** > **Configure Settings** > Change resource group to ToDoApp*&lt;your_suffix>* > **Add Application Insights to Project**.</span></span>
2. <span data-ttu-id="ce0d4-202">No Git Shell, confirme e envie por push as alterações à bifurcação no GitHub.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-202">In Git Shell, commit and push your changes to your fork in GitHub.</span></span> <span data-ttu-id="ce0d4-203">Em seguida, aguarde até que os clientes atualizem o navegador.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-203">Then, wait for clients to refresh browser.</span></span>

       git add -A :/
       git commit -m "add AI configuration for server app"
       git push origin master
3. <span data-ttu-id="ce0d4-204">Alterne as alterações do aplicativo implantado para a produção:</span><span class="sxs-lookup"><span data-stu-id="ce0d4-204">Swap the deployed app changes to production:</span></span>

     <span data-ttu-id="ce0d4-205">.\swap –Name ToDoApp<your_suffix></span><span class="sxs-lookup"><span data-stu-id="ce0d4-205">.\swap –Name ToDoApp<your_suffix></span></span>

<span data-ttu-id="ce0d4-206">É isso!</span><span class="sxs-lookup"><span data-stu-id="ce0d4-206">That's it!</span></span>

## <a name="investigate-add-slot-specific-tags-to-your-client-app-metrics"></a><span data-ttu-id="ce0d4-207">Investigue: adicionar marcas específicas do slot às métricas do aplicativo cliente</span><span class="sxs-lookup"><span data-stu-id="ce0d4-207">Investigate: Add slot-specific tags to your client app metrics</span></span>
<span data-ttu-id="ce0d4-208">Nesta seção, você configurará os diferentes slots de implantação para enviar telemetria específica do slot para o mesmo recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-208">In this section, you will configure the different deployment slots to send slot-specific telemetry to the same Application Insights resource.</span></span> <span data-ttu-id="ce0d4-209">Dessa forma, você pode comparar os dados de telemetria entre o tráfego de slots diferentes (ambientes de implantação) para ver o efeito das alterações de seu aplicativo com facilidade.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-209">This way, you can compare telemetry data between traffic from different slots (deployment environments) to easily see the effect of your app changes.</span></span> <span data-ttu-id="ce0d4-210">Ao mesmo tempo, você pode separar o tráfego de produção do restante, para que você possa continuar a monitorar seu aplicativo de produção, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-210">At the same time, you can separate the production traffic from the rest so you can continue to monitor your production app as needed.</span></span>

<span data-ttu-id="ce0d4-211">Já que você está reunindo dados sobre o comportamento do cliente, você poderá [adicionar um inicializador de telemetria ao seu código do JavaScript](../application-insights/app-insights-api-filtering-sampling.md) em index.cshtml.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-211">Since you're gathering data on client behavior, you will [add a telemetry initializer to your JavaScript code](../application-insights/app-insights-api-filtering-sampling.md) in index.cshtml.</span></span> <span data-ttu-id="ce0d4-212">Se desejar testar o desempenho do lado do servidor, por exemplo, também é possível realizar o mesmo em seu código do servidor (veja [API do Application Insights para métricas e eventos personalizados](../application-insights/app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="ce0d4-212">If you want to test server-side performance, for example, you can also do similarly in your server code (see [Application Insights API for custom events and metrics](../application-insights/app-insights-api-custom-events-metrics.md).</span></span>

1. <span data-ttu-id="ce0d4-213">Primeiro, adicione o código entre os dois comentários `//` abaixo no bloco de JavaScript adicionado à marca `<heading>` anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-213">First, add the code bewteen the two `//` comments below in the JavaScript block that you added to the `<heading>` tag earlier.</span></span>

        window.appInsights = appInsights;

        // Begin new code
        appInsights.queue.push(function () {
            appInsights.context.addTelemetryInitializer(function (envelope) {
                var telemetryItem = envelope.data.baseData;
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["Environment"] = "@System.Configuration.ConfigurationManager.AppSettings["environment"]";
            });
        });
        // End new code

        appInsights.trackPageView();

    <span data-ttu-id="ce0d4-214">Esse código do inicializador faz com que o objeto `appInsights` adicione uma propriedade personalizada chamada `Environment` a cada item de telemetria enviado.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-214">This initializer code causes the `appInsights` object to add the a custom property called `Environment` to every piece of telemetry it sends.</span></span>
2. <span data-ttu-id="ce0d4-215">Em seguida, adicione essa propriedade personalizada como uma [configuração do slot](web-sites-staged-publishing.md#AboutConfiguration) de seu aplicativo Web no Azure.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-215">Next, add this custom property as a [slot setting](web-sites-staged-publishing.md#AboutConfiguration) for your web app in Azure.</span></span> <span data-ttu-id="ce0d4-216">Para fazer isso, execute os comandos a seguir em sua sessão do Git Shell.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-216">To do this, run the following commands in your Git Shell session.</span></span>

        $app = Get-AzureWebsite -Name todoapp<your_suffix> -Slot production
        $app.AppSettings.Add("environment", "Production")
        $app.SlotStickyAppSettingNames.Add("environment")
        $app | Set-AzureWebsite -Name todoapp<your_suffix> -Slot production

    <span data-ttu-id="ce0d4-217">O Web.config em seu projeto já define a configuração `environment` do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-217">The Web.config in your project already defines the `environment` app setting.</span></span> <span data-ttu-id="ce0d4-218">Com essa configuração, quando você testar o aplicativo localmente, suas métricas serão marcadas com `VS Debugger`.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-218">With this setting, when you test the app locally, your metrics will be tagged with `VS Debugger`.</span></span> <span data-ttu-id="ce0d4-219">No entanto, quando você enviar por push suas alterações para o Azure, o Azure encontrará e usará a configuração do aplicativo `environment` na configuração do aplicativo Web e suas métricas serão marcadas com `Production`.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-219">However, when you push your changes to Azure, Azure will find and use the `environment` app setting in the web app's configuration instead, and your metrics will be tagged with `Production`.</span></span>
3. <span data-ttu-id="ce0d4-220">Confirme e envie por push as alterações de código à bifurcação no GitHub e aguarde até que os usuários usem o novo aplicativo (é necessário atualizar o navegador).</span><span class="sxs-lookup"><span data-stu-id="ce0d4-220">Commit and push your code changes to your fork on GitHub, and then wait for your users to use the new app (need to refresh the browser).</span></span> <span data-ttu-id="ce0d4-221">Demora cerca de 15 minutos para que a nova propriedade apareça em seu recurso `MultiChannelToDo.Web` do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-221">It takes about 15 minutes for the new property to show up in your Application Insights `MultiChannelToDo.Web` resource.</span></span>

        git add -A :/
        git commit -m "add environment property to AI events for client app"
        git push origin master
4. <span data-ttu-id="ce0d4-222">Agora, vá novamente para a folha **Eventos personalizados** e filtre as métricas em `Environment=Production`.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-222">Now, go to the **Custom events** blade again and filter the metrics on `Environment=Production`.</span></span> <span data-ttu-id="ce0d4-223">Agora, você deverá ver todos os novos eventos personalizados no slot de produção com este filtro.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-223">You should now be able to see all the new custom events in the production slot with this filter.</span></span>

    ![](./media/app-service-web-test-in-production-controlled-test-flight/05-filter-on-production-environment.png)
5. <span data-ttu-id="ce0d4-224">Clique no botão **Favoritos** para salvar as configurações atuais do Metrics Explorer como algo como **Eventos personalizados: Produção**.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-224">Click the **Favorites** button to save the current Metrics Explorer settings to something like **Custom events: Production**.</span></span> <span data-ttu-id="ce0d4-225">Você pode alternar facilmente entre esta exibição e uma exibição de slot de implantação posteriormente.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-225">You can easily switch between this view and a deployment slot view later.</span></span>

   > [!TIP]
   > <span data-ttu-id="ce0d4-226">Para uma análise ainda mais eficiente, considere [integrar seu recurso do Application Insights com o Power BI](../application-insights/app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="ce0d4-226">For even more powerful analytics, consider [integrating your Application Insights resource with Power BI](../application-insights/app-insights-export-power-bi.md).</span></span>
   >
   >

### <a name="add-slot-specific-tags-to-your-server-app-metrics"></a><span data-ttu-id="ce0d4-227">Adicionar marcas específicas do slot às suas métricas de aplicativo de servidor</span><span class="sxs-lookup"><span data-stu-id="ce0d4-227">Add slot-specific tags to your server app metrics</span></span>
<span data-ttu-id="ce0d4-228">Novamente, para fins de exatidão, você configurará o aplicativo do lado do servidor.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-228">Again, for completeness you will set up the server-side app.</span></span> <span data-ttu-id="ce0d4-229">Ao contrário do aplicativo cliente que é instrumentado em JavaScript, as marcas específicas do slot para o aplicativo de servidor são instrumentadas com o código do .NET.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-229">Unlike the client app which is instrumented in JavaScript, slot-specific tags for the server app is instrumented with .NET code.</span></span>

1. <span data-ttu-id="ce0d4-230">Abra *&lt;raiz_do_repositório>*\src\MultiChannelToDo\Global.asax.cs.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-230">Open *&lt;repository_root>*\src\MultiChannelToDo\Global.asax.cs.</span></span> <span data-ttu-id="ce0d4-231">Adicione o bloco de código abaixo, logo antes da chave do namespace de fechamento.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-231">Add the code block below, just before the closing namespace curly brace.</span></span>

        namespace MultiChannelToDo
        {
                ...

                // Begin new code
            public class ConfigInitializer
            : ITelemetryInitializer
            {
                void ITelemetryInitializer.Initialize(ITelemetry telemetry)
                {
                    telemetry.Context.Properties["Environment"] = System.Configuration.ConfigurationManager.AppSettings["environment"];
                }
            }
                // End new code
        }
2. <span data-ttu-id="ce0d4-232">Corrija os erros de resolução de nomes adicionando as instruções `using` abaixo ao início do arquivo:</span><span class="sxs-lookup"><span data-stu-id="ce0d4-232">Correct the name resolution errors by adding the `using` statements below to the beginning of the file:</span></span>

        using Microsoft.ApplicationInsights.Channel;
        using Microsoft.ApplicationInsights.Extensibility;
3. <span data-ttu-id="ce0d4-233">Adicione o código abaixo ao início do método `Application_Start()` :</span><span class="sxs-lookup"><span data-stu-id="ce0d4-233">Add the code below to the beginning of the `Application_Start()` method:</span></span>

        TelemetryConfiguration.Active.TelemetryInitializers.Add(new ConfigInitializer());
4. <span data-ttu-id="ce0d4-234">Confirme e envie por push as alterações de código à bifurcação no GitHub e aguarde até que os usuários usem o novo aplicativo (é necessário atualizar o navegador).</span><span class="sxs-lookup"><span data-stu-id="ce0d4-234">Commit and push your code changes to your fork on GitHub, and then wait for your users to use the new app (need to refresh the browser).</span></span> <span data-ttu-id="ce0d4-235">Demora cerca de 15 minutos para que a nova propriedade apareça em seu recurso `MultiChannelToDo` do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-235">It takes about 15 minutes for the new property to show up in your Application Insights `MultiChannelToDo` resource.</span></span>

        git add -A :/
        git commit -m "add environment property to AI events for server app"
        git push origin master

## <a name="update-set-up-your-beta-branch"></a><span data-ttu-id="ce0d4-236">Atualização: configurar sua ramificação beta</span><span class="sxs-lookup"><span data-stu-id="ce0d4-236">Update: Set up your beta branch</span></span>
1. <span data-ttu-id="ce0d4-237">Abra *&lt;raiz_do_repositório>*\ARMTemplates\ProdAndStagetest.json e encontre os recursos do `appsettings` (procure `"name": "appsettings"`).</span><span class="sxs-lookup"><span data-stu-id="ce0d4-237">Open *&lt;repository_root>*\ARMTemplates\ProdAndStagetest.json and find the `appsettings` resources (search for `"name": "appsettings"`).</span></span> <span data-ttu-id="ce0d4-238">Há quatro deles, um para cada slot.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-238">There are 4 of them, one for each slot.</span></span>
2. <span data-ttu-id="ce0d4-239">Para cada recurso do `appsettings`, adicione uma configuração do aplicativo `"environment": "[parameters('slotName')]"` ao final da matriz `properties`.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-239">For each `appsettings` resource, add an  `"environment": "[parameters('slotName')]"` app setting to the end of the `properties` array.</span></span> <span data-ttu-id="ce0d4-240">Não se esqueça de terminar a linha anterior com uma vírgula.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-240">Don't forget to end the previous line with a comma.</span></span>

    ![](./media/app-service-web-test-in-production-controlled-test-flight/06-arm-app-setting-with-slot-name.png)

    <span data-ttu-id="ce0d4-241">Você acabou de adicionar a configuração de aplicativo `environment` a todos os slots no modelo.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-241">You have just added the `environment` app setting to all the slots in the template.</span></span>
3. <span data-ttu-id="ce0d4-242">No mesmo arquivo, encontre os recursos do `slotconfignames` (procure `"name": "slotconfignames"`).</span><span class="sxs-lookup"><span data-stu-id="ce0d4-242">In the same file, find the `slotconfignames` resources (search for `"name": "slotconfignames"`).</span></span> <span data-ttu-id="ce0d4-243">Há dois deles, um para cada aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-243">There are 2 of them, one for each app.</span></span>
4. <span data-ttu-id="ce0d4-244">Para cada recurso do `slotconfignames`, adicione `"environment"` ao final da matriz `appSettingNames`.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-244">For each `slotconfignames` resource, add `"environment"` to the end of the `appSettingNames` array.</span></span> <span data-ttu-id="ce0d4-245">Não se esqueça de terminar a linha anterior com uma vírgula.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-245">Don't forget to end the previous line with a comma.</span></span>

    <span data-ttu-id="ce0d4-246">Você acabou de fixar a configuração de aplicativo `environment` em seu respectivo slot de implantação para os dois aplicativos.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-246">You have just made the `environment` app setting stick to its respective deployment slot for both apps.</span></span>  
5. <span data-ttu-id="ce0d4-247">Em sua sessão do Git Shell, execute os comandos a seguir com o mesmo sufixo do grupo de recursos que você usou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-247">In your Git Shell session, run the following commands with the same resource group suffix that you used before.</span></span>

        git checkout -b beta
        git push origin beta
        .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch beta
6. <span data-ttu-id="ce0d4-248">Quando solicitado, especifique as mesmas credenciais do banco de dados SQL que anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-248">When prompted, specify the same SQL database credentials as before.</span></span> <span data-ttu-id="ce0d4-249">Em seguida, quando solicitado a atualizar o grupo de recursos, digite `Y` e `ENTER`.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-249">Then, when asked to update the resource group, type `Y`, then `ENTER`.</span></span>

    <span data-ttu-id="ce0d4-250">Depois que o script for concluído, todos os seus recursos no grupo de recursos original serão mantidos, mas um novo slot chamado “beta” será criado nele com a mesma configuração que o slot de “Preparação” que foi criado no início.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-250">Once the script finishes, all your resources in the original resource group are retained, but a new slot named "beta" is created in it with the same configuration as the "Staging" slot that was created in the beginning.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ce0d4-251">Esse método de criação de diferentes ambientes de implantação é diferente do método no [Desenvolvimento de software Agile com o Serviço de Aplicativo do Azure](app-service-agile-software-development.md).</span><span class="sxs-lookup"><span data-stu-id="ce0d4-251">This method of creating different deployment environments is different from the method in [Agile software development with Azure App Service](app-service-agile-software-development.md).</span></span> <span data-ttu-id="ce0d4-252">Aqui, você cria ambientes de implantação com slots de implantação, enquanto que lá você cria ambientes de implantação com grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-252">Here, you create deployment environments with deployment slots, where as there you create deployment environments with resource groups.</span></span> <span data-ttu-id="ce0d4-253">O gerenciamento de ambientes de implantação com grupos de recursos permite que você mantenha o ambiente de produção fora dos limites para os desenvolvedores; porém, não é fácil realizar testes em produção, o que pode ser feito facilmente com slots.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-253">Managing deployment environments with resource groups enables you to keep the production environment off-limits to developers, but it's not easy to do testing in production, which you can do easily with slots.</span></span>
   >
   >

<span data-ttu-id="ce0d4-254">Se desejar, você também pode criar um aplicativo alfa executando</span><span class="sxs-lookup"><span data-stu-id="ce0d4-254">If you wish, you can also create an alpha app by running</span></span>

    git checkout -b alpha
    git push origin alpha
    .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch alpha

<span data-ttu-id="ce0d4-255">Para este tutorial, você continuará usando seu aplicativo beta.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-255">For this tutorial, you will just keep using your beta app.</span></span>

## <a name="update-push-your-updates-to-the-beta-app"></a><span data-ttu-id="ce0d4-256">Atualização: enviar por push as atualizações para o aplicativo beta</span><span class="sxs-lookup"><span data-stu-id="ce0d4-256">Update: Push your updates to the beta app</span></span>
<span data-ttu-id="ce0d4-257">Volte ao aplicativo que você deseja melhorar.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-257">Back to your app that you want to improve.</span></span>

1. <span data-ttu-id="ce0d4-258">Verifique se você está agora em sua ramificação beta</span><span class="sxs-lookup"><span data-stu-id="ce0d4-258">Make sure you're now in your beta branch</span></span>

        git checkout beta
2. <span data-ttu-id="ce0d4-259">Em *&lt;raiz_repositório>*\src\MultiChannelToDo.Web\app\Index.cshtml, encontre a marca `<li>` e adicione o atributo `style="cursor:pointer"`, como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-259">In *&lt;repository_root>*\src\MultiChannelToDo.Web\app\Index.cshtml, find the `<li>` tag and add the `style="cursor:pointer"` attribute, as shown below.</span></span>

    ![](./media/app-service-web-test-in-production-controlled-test-flight/07-change-cursor-style-on-li.png)
3. <span data-ttu-id="ce0d4-260">confirme e envie por push para o Azure.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-260">commit and push to Azure.</span></span>
4. <span data-ttu-id="ce0d4-261">Verifique se a alteração é agora refletida no slot beta navegando até http://todoapp*&lt;seu_sufixo>*-beta.azurewebsites.net/.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-261">Verify that the change is now reflected in the beta slot by navigating to http://todoapp*&lt;your_suffix>*-beta.azurewebsites.net/.</span></span> <span data-ttu-id="ce0d4-262">Se você ainda não vir a alteração, atualize o navegador para obter o novo código JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-262">If you don't see the change yet, refresh your browser to get the new javascript code.</span></span>

    ![](./media/app-service-web-test-in-production-controlled-test-flight/08-verify-change-in-beta-site.png)

<span data-ttu-id="ce0d4-263">Agora que a alteração está em execução no slot beta, você está pronto para realizar uma implantação flighting.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-263">Now that you have your change running in the beta slot, you are ready to perform a flighting deployment.</span></span>

## <a name="validate-route-traffic-to-the-beta-app"></a><span data-ttu-id="ce0d4-264">Validar: encaminhar o tráfego para o aplicativo beta</span><span class="sxs-lookup"><span data-stu-id="ce0d4-264">Validate: Route traffic to the beta app</span></span>
<span data-ttu-id="ce0d4-265">Nesta seção, você encaminhará o tráfego para o aplicativo beta.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-265">In this section, you will route traffic to the beta app.</span></span> <span data-ttu-id="ce0d4-266">Para fins de clareza de demonstração, vamos encaminhar uma parte significativa do tráfego de usuário para ele.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-266">For sake of clarity of demonstration, you're going to route a significant portion of the user traffic to it.</span></span> <span data-ttu-id="ce0d4-267">Na realidade, a quantidade de tráfego que você deseja encaminhar dependerá de sua situação específica.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-267">In reality, the amount of traffic you want to route will depend on your specific situation.</span></span> <span data-ttu-id="ce0d4-268">Por exemplo, se o seu site estiver na escala do microsoft.com, talvez seja necessário menos de 1% do tráfego total para obter dados úteis.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-268">For example, if your site is at the scale of microsoft.com, then you may need less than one percent of your total traffic in order to gain useful data.</span></span>

1. <span data-ttu-id="ce0d4-269">Em sua sessão do Git Shell, execute os seguintes comandos para encaminhar metade do tráfego de produção para o slot beta:</span><span class="sxs-lookup"><span data-stu-id="ce0d4-269">In your Git Shell session, run the following commands to route half of the production traffic to the beta slot:</span></span>

        $siteName = "ToDoApp<your suffix>"
        $rule = New-Object Microsoft.WindowsAzure.Commands.Utilities.Websites.Services.WebEntities.RampUpRule
        $rule.ActionHostName = "$siteName-beta.azurewebsites.net"
        $rule.ReroutePercentage = 50
        $rule.Name = "beta"
        Set-AzureWebsite $siteName -Slot Production -RoutingRules $rule

   <span data-ttu-id="ce0d4-270">A propriedade `ReroutePercentage=50` especifica que 50% do tráfego de produção será encaminhado para a URL do aplicativo beta (especificado pela propriedade `ActionHostName`).</span><span class="sxs-lookup"><span data-stu-id="ce0d4-270">The `ReroutePercentage=50` property specifies that 50% of the production traffic will be routed to the beta app's URL (specified by the `ActionHostName` property).</span></span>
2. <span data-ttu-id="ce0d4-271">Agora, navegue até http://ToDoApp*&lt;seu_sufixo>*.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-271">Now navigate to http://ToDoApp*&lt;your_suffix>*.azurewebsites.net.</span></span> <span data-ttu-id="ce0d4-272">50% do tráfego agora deve ser redirecionado para o slot beta.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-272">50% of the traffic should now be redirected to the beta slot.</span></span>
3. <span data-ttu-id="ce0d4-273">Em seu recurso do Application Insights, filtre as métricas pelo ambiente = “beta”.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-273">In your Application Insights resource, filter the metrics by environment="beta".</span></span>

   > [!NOTE]
   > <span data-ttu-id="ce0d4-274">Se você salvar esta exibição filtrada como outro favorito, você poderá inverter facilmente as exibições do Metric Explorer entre as exibições de produção e beta.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-274">If you save this filtered view as another favorite, then you can easily flip the metric explorer views between production and beta views.</span></span>
   >
   >

<span data-ttu-id="ce0d4-275">Suponha que no Application Insights você veja algo semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="ce0d4-275">Suppose in Application Insights you see something similar to the following:</span></span>

![](./media/app-service-web-test-in-production-controlled-test-flight/09-test-beta-site-in-production.png)

<span data-ttu-id="ce0d4-276">Isso não só mostra que há muito mais cliques nas marcas `<li>`, mas também que parece haver um aumento de cliques nas marcas `<li>`.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-276">Not only is this showing that there are many more clicks on the `<li>` tags, but there seems to be a surge of clicks on `<li>` tags.</span></span> <span data-ttu-id="ce0d4-277">Em seguida, você pode concluir que as pessoas descobriram que as novas marcas `<li>` são clicáveis e agora estão limpando todas as suas tarefas concluídas anteriormente no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-277">You can then conclude that people have discovered the new `<li>` tags are clickable and are now clearing all their previously-completed tasks in the app.</span></span>

<span data-ttu-id="ce0d4-278">Com base nos dados de sua implantação flighting, você decide que a nova interface do usuário está pronta para produção.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-278">Based on the data of your flighting deployment, you decide that your new UI is ready for production.</span></span>

## <a name="go-live-move-your-new-code-into-production"></a><span data-ttu-id="ce0d4-279">Ativação: mover seu novo código para a produção</span><span class="sxs-lookup"><span data-stu-id="ce0d4-279">Go live: Move your new code into production</span></span>
<span data-ttu-id="ce0d4-280">Agora você está pronto para mover a atualização para a produção.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-280">You're now ready to move your update to production.</span></span> <span data-ttu-id="ce0d4-281">A boa notícia é que agora você sabe que a atualização já foi validada *antes* de ser enviada para a produção.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-281">What's great is that now you know that your update has already been validated *before* it is pushed to production.</span></span> <span data-ttu-id="ce0d4-282">Agora você pode implantá-la com confiança.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-282">So now you can confidently deploy it.</span></span> <span data-ttu-id="ce0d4-283">Já que você fez uma atualização ao aplicativo de cliente AngularJS, você apenas validou o código do lado do cliente.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-283">Since you made an update to the AngularJS client app, you only validated the client-side code.</span></span> <span data-ttu-id="ce0d4-284">Se você fosse fazer alterações no aplicativo de API da Web de back-end, você poderia validar as alterações da mesma forma e com facilidade.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-284">If you were to make changes to the back-end Web API app, you could validate your changes similarly and easily.</span></span>

1. <span data-ttu-id="ce0d4-285">No Git Shell, remova a regra de roteamento de tráfego executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="ce0d4-285">In Git Shell, remove the traffic routing rule by running the following command:</span></span>

        Set-AzureWebsite $siteName -Slot Production -RoutingRules @()
2. <span data-ttu-id="ce0d4-286">Execute os comandos do Git:</span><span class="sxs-lookup"><span data-stu-id="ce0d4-286">Run the Git commands:</span></span>

        git checkout master
        git pull origin master
        git merge beta
        git push origin master
3. <span data-ttu-id="ce0d4-287">Aguarde alguns minutos até que o novo código seja implantado no slot de preparo e inicie http://ToDoApp*&lt;seu_sufixo>*-staging.azurewebsites.net para verificar se a nova atualização está pronta no slot de preparo.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-287">Wait for a few minutes for the new code to be deployed to the staging slot, then launch http://ToDoApp*&lt;your_suffix>*-staging.azurewebsites.net to verify that the new update is warmed up in the staging slot.</span></span> <span data-ttu-id="ce0d4-288">Lembre-se de que a ramificação mestre da bifurcação está vinculada ao slot de preparo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-288">Remember that the your fork's master branch is linked to the staging slot of your app.</span></span>
4. <span data-ttu-id="ce0d4-289">Agora, permute o slot de preparo para a produção</span><span class="sxs-lookup"><span data-stu-id="ce0d4-289">Now, swap the staging slot into production</span></span>

        cd <ROOT>\ToDoApp\ARMTemplates
        .\swap.ps1 -Name todoapp<your_suffix>

## <a name="summary"></a><span data-ttu-id="ce0d4-290">Resumo</span><span class="sxs-lookup"><span data-stu-id="ce0d4-290">Summary</span></span>
<span data-ttu-id="ce0d4-291">O Serviço de Aplicativo do Azure facilita para as empresas de pequeno a médio porte testar seus aplicativos voltados para o cliente em produção, algo que tradicionalmente era feito em grandes empresas.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-291">Azure App Service makes it easy for small- to medium-sized businesses to test their customer-facing apps in production, something that has been traditionally done in big enterprises.</span></span> <span data-ttu-id="ce0d4-292">Espero que este tutorial tenha fornecido o conhecimento necessário para reunir o Serviço de Aplicativo e o Application Insights e possibilitar a implantação flighting, e até mesmo outros cenários de teste na produção, em seu mundo DevOps.</span><span class="sxs-lookup"><span data-stu-id="ce0d4-292">Hopefully, this tutorial has given you the knowledge you need to bring together App Service and Application Insights to make possible flighting deployment, and even other test-in-production scenarios, in your DevOps world.</span></span>

## <a name="more-resources"></a><span data-ttu-id="ce0d4-293">Mais recursos</span><span class="sxs-lookup"><span data-stu-id="ce0d4-293">More resources</span></span>
* [<span data-ttu-id="ce0d4-294">Desenvolvimento de software Agile com o Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="ce0d4-294">Agile software development with Azure App Service</span></span>](app-service-agile-software-development.md)
* [<span data-ttu-id="ce0d4-295">Configurar ambientes de preparo para aplicativos Web no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="ce0d4-295">Set up staging environments for web apps in Azure App Service</span></span>](web-sites-staged-publishing.md)
* [<span data-ttu-id="ce0d4-296">Implantar um aplicativo complexo de modo previsível no Azure</span><span class="sxs-lookup"><span data-stu-id="ce0d4-296">Deploy a complex application predictably in Azure</span></span>](app-service-deploy-complex-application-predictably.md)
* [<span data-ttu-id="ce0d4-297">Criando modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ce0d4-297">Authoring Azure Resource Manager Templates</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)
* [<span data-ttu-id="ce0d4-298">JSONLint - o validador JSON</span><span class="sxs-lookup"><span data-stu-id="ce0d4-298">JSONLint - The JSON Validator</span></span>](http://jsonlint.com/)
* [<span data-ttu-id="ce0d4-299">Ramificação Git – Conceitos básicos de ramificação e mesclagem</span><span class="sxs-lookup"><span data-stu-id="ce0d4-299">Git Branching – Basic Branching and Merging</span></span>](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [<span data-ttu-id="ce0d4-300">PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="ce0d4-300">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="ce0d4-301">Projeto Kudu Wiki</span><span class="sxs-lookup"><span data-stu-id="ce0d4-301">Project Kudu Wiki</span></span>](https://github.com/projectkudu/kudu/wiki)
