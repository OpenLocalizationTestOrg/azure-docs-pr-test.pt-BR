---
title: "Visão geral detalhada de planos de aaaAzure do serviço de aplicativo | Microsoft Docs"
description: "Saiba como os planos do Serviço de Aplicativo para o Serviço de Aplicativo do Azure funcionam e como eles beneficiam sua experiência de gerenciamento."
keywords: "serviço de aplicativo, serviço de aplicativo do azure, escala, escalonável, plano de serviço de aplicativo, custo de serviço de aplicativo"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: dea3f41e-cf35-481b-a6bc-33d7fc9d01b1
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: byvinyal
ms.openlocfilehash: b384790d9e69b234ca69ac591164c48a4b6ed210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-plans-in-depth-overview"></a><span data-ttu-id="8e84f-104">Visão geral detalhada de planos de serviço de aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="8e84f-104">Azure App Service plans in-depth overview</span></span>

<span data-ttu-id="8e84f-105">Planos de serviço de aplicativo representam a coleção de saudação de recursos físicos usados toohost seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="8e84f-105">App Service plans represent hello collection of physical resources used toohost your apps.</span></span>

<span data-ttu-id="8e84f-106">Os Planos do Serviço de Aplicativo definem:</span><span class="sxs-lookup"><span data-stu-id="8e84f-106">App Service plans define:</span></span>

- <span data-ttu-id="8e84f-107">Região (Oeste dos EUA, Leste dos EUA, etc.)</span><span class="sxs-lookup"><span data-stu-id="8e84f-107">Region (West US, East US, etc.)</span></span>
- <span data-ttu-id="8e84f-108">Contagem da escala (uma, duas, três instâncias, etc.)</span><span class="sxs-lookup"><span data-stu-id="8e84f-108">Scale count (one, two, three instances, etc.)</span></span>
- <span data-ttu-id="8e84f-109">Tamanha da instância (Pequena, Média, Grande)</span><span class="sxs-lookup"><span data-stu-id="8e84f-109">Instance size (Small, Medium, Large)</span></span>
- <span data-ttu-id="8e84f-110">SKU (Gratuito, Compartilhado, Básico, Standard, Premium)</span><span class="sxs-lookup"><span data-stu-id="8e84f-110">SKU (Free, Shared, Basic, Standard, Premium)</span></span>

<span data-ttu-id="8e84f-111">Aplicativos Web, Aplicativos Móveis, Aplicativos de API, Aplicativos de Funções (ou Funções) no [Serviço de Aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) todos executados em um plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8e84f-111">Web Apps, Mobile Apps, API Apps, Function Apps (or Functions), in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) all run in an App Service plan.</span></span>  <span data-ttu-id="8e84f-112">Aplicativos em Olá mesma assinatura e região podem compartilhar um plano de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8e84f-112">Apps in hello same subscription, and region can share an App Service plan.</span></span> 

<span data-ttu-id="8e84f-113">Todos os aplicativos atribuídos tooan **plano de serviço de aplicativo** compartilham recursos Olá definidos por ela.</span><span class="sxs-lookup"><span data-stu-id="8e84f-113">All applications assigned tooan **App Service plan** share hello resources defined by it.</span></span> <span data-ttu-id="8e84f-114">Esse compartilhamento economiza dinheiro ao hospedar vários aplicativos em um único plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8e84f-114">This sharing saves money when hosting multiple apps in a single App Service plan.</span></span>

<span data-ttu-id="8e84f-115">O **plano de serviço de aplicativo** pode ser dimensionada de **livre** e **compartilhado** SKUs muito**básica**, **padrão**, e **Premium** SKUs dando a você acessam os recursos de toomore e recursos ao longo de saudação maneira.</span><span class="sxs-lookup"><span data-stu-id="8e84f-115">Your **App Service plan** can scale from **Free** and **Shared** SKUs too**Basic**, **Standard**, and **Premium** SKUs giving you access toomore resources and features along hello way.</span></span>

<span data-ttu-id="8e84f-116">Se seu plano de serviço de aplicativo está definido muito**básica** SKU ou superior, em seguida, você pode controlar Olá **tamanho** e dimensionar a contagem de saudação VMs.</span><span class="sxs-lookup"><span data-stu-id="8e84f-116">If your App Service plan is set too**Basic** SKU or higher, then you can control hello **size** and scale count of hello VMs.</span></span>

<span data-ttu-id="8e84f-117">Por exemplo, se seu plano é configurado toouse duas instâncias de "pequeno" na camada de serviço standard Olá, todos os aplicativos que estão associados esse plano é executado em ambas as instâncias.</span><span class="sxs-lookup"><span data-stu-id="8e84f-117">For example, if your plan is configured toouse two "small" instances in hello standard service tier, all apps that are associated with that plan run on both instances.</span></span> <span data-ttu-id="8e84f-118">Os aplicativos também têm características do nível de serviço padrão do acesso toohello.</span><span class="sxs-lookup"><span data-stu-id="8e84f-118">Apps also have access toohello standard service tier features.</span></span> <span data-ttu-id="8e84f-119">Instâncias do plano nas quais aplicativos estão em execução são totalmente gerenciadas e altamente disponíveis.</span><span class="sxs-lookup"><span data-stu-id="8e84f-119">Plan instances on which apps are running are fully managed and highly available.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e84f-120">Olá **SKU** e **escala** de saudação do serviço de aplicativo plano determina o número de custo e não hello de saudação de aplicativos hospedados nele.</span><span class="sxs-lookup"><span data-stu-id="8e84f-120">hello **SKU** and **Scale** of hello App Service plan determines hello cost and not hello number of apps hosted in it.</span></span>

<span data-ttu-id="8e84f-121">Este artigo explora Olá principais características, como camada e escala de um plano de serviço de aplicativo e como eles entram em ação ao gerenciar seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="8e84f-121">This article explores hello key characteristics, such as tier and scale, of an App Service plan and how they come into play while managing your apps.</span></span>

## <a name="apps-and-app-service-plans"></a><span data-ttu-id="8e84f-122">Aplicativos e planos do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="8e84f-122">Apps and App Service plans</span></span>

<span data-ttu-id="8e84f-123">Um aplicativo no Serviço de Aplicativo pode ser associado a apenas um plano de Serviço de Aplicativo de cada vez.</span><span class="sxs-lookup"><span data-stu-id="8e84f-123">An app in App Service can be associated with only one App Service plan at any given time.</span></span>

<span data-ttu-id="8e84f-124">Os aplicativos e os planos estão contidos em **grupo de recursos**.</span><span class="sxs-lookup"><span data-stu-id="8e84f-124">Both apps and plans are contained in a **resource group**.</span></span> <span data-ttu-id="8e84f-125">Um grupo de recursos serve como o limite de ciclo de vida de Olá para cada recurso que está dentro dele.</span><span class="sxs-lookup"><span data-stu-id="8e84f-125">A resource group serves as hello lifecycle boundary for every resource that's within it.</span></span> <span data-ttu-id="8e84f-126">Você pode usar toomanage de grupos de recursos todas as partes de saudação de um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8e84f-126">You can use resource groups toomanage all hello pieces of an application together.</span></span>

<span data-ttu-id="8e84f-127">Como um único grupo de recursos pode ter vários planos de serviço de aplicativo, você pode alocar aplicativos diferentes recursos físicos toodifferent.</span><span class="sxs-lookup"><span data-stu-id="8e84f-127">Because a single resource group can have multiple App Service plans, you can allocate different apps toodifferent physical resources.</span></span>

<span data-ttu-id="8e84f-128">Por exemplo, você pode dividir os recursos entre ambientes de desenvolvimento, teste e produção.</span><span class="sxs-lookup"><span data-stu-id="8e84f-128">For example, you can separate resources among dev, test, and production environments.</span></span> <span data-ttu-id="8e84f-129">Ter ambientes separados para desenvolvimento/teste e produção permite isolar recursos.</span><span class="sxs-lookup"><span data-stu-id="8e84f-129">Having separate environments for production and dev/test lets you isolate resources.</span></span> <span data-ttu-id="8e84f-130">Dessa forma, em relação a uma nova versão de seus aplicativos de teste de carga não compete para Olá mesmo recursos como seus aplicativos de produção, o que estão atendendo clientes reais.</span><span class="sxs-lookup"><span data-stu-id="8e84f-130">In this way, load testing against a new version of your apps does not compete for hello same resources as your production apps, which are serving real customers.</span></span>

<span data-ttu-id="8e84f-131">Quando você tem vários planos em um único grupo de recursos, também pode definir um aplicativo que abrange várias regiões geográficas.</span><span class="sxs-lookup"><span data-stu-id="8e84f-131">When you have multiple plans in a single resource group, you can also define an application that spans geographical regions.</span></span>

<span data-ttu-id="8e84f-132">Por exemplo, um aplicativo altamente disponível executando em duas regiões incluirá pelo menos dois planos, um para cada região e um aplicativo associado com cada plano.</span><span class="sxs-lookup"><span data-stu-id="8e84f-132">For example, a highly available app running in two regions includes at least two plans, one for each region, and one app associated with each plan.</span></span> <span data-ttu-id="8e84f-133">Em tal situação, todas as cópias de saudação do aplicativo hello, em seguida, estão contidas em um único grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8e84f-133">In such a situation, all hello copies of hello app are then contained in a single resource group.</span></span> <span data-ttu-id="8e84f-134">Ter um grupo de recursos com vários planos e vários aplicativos torna fácil toomanage, controle e exibir a integridade de saudação do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="8e84f-134">Having a resource group with multiple plans and multiple apps makes it easy toomanage, control, and view hello health of hello application.</span></span>

## <a name="create-an-app-service-plan-or-use-existing-one"></a><span data-ttu-id="8e84f-135">Criar um Plano do Serviço de Aplicativo ou usar um existente</span><span class="sxs-lookup"><span data-stu-id="8e84f-135">Create an App Service plan or use existing one</span></span>

<span data-ttu-id="8e84f-136">Ao criar um aplicativo, você deverá considerar a criação de um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8e84f-136">When you create an app, you should consider creating a resource group.</span></span> <span data-ttu-id="8e84f-137">Em Olá outro lado, se este aplicativo é um componente para um aplicativo maior, criá-lo no grupo de recursos de saudação que é alocado para o aplicativo maior.</span><span class="sxs-lookup"><span data-stu-id="8e84f-137">On hello other hand, if this app is a component for a larger application, create it within hello resource group that's allocated for that larger application.</span></span>

<span data-ttu-id="8e84f-138">Se o aplicativo hello é um aplicativo totalmente novo ou parte de uma maior, você pode escolher toouse um toohost plano existente-lo ou criar um novo.</span><span class="sxs-lookup"><span data-stu-id="8e84f-138">Whether hello app is an altogether new application or part of a larger one, you can choose toouse an existing plan toohost it or create a new one.</span></span> <span data-ttu-id="8e84f-139">Essa decisão é mais uma questão de capacidade e carga esperada.</span><span class="sxs-lookup"><span data-stu-id="8e84f-139">This decision is more a question of capacity and expected load.</span></span>

<span data-ttu-id="8e84f-140">É recomendável isolar seu aplicativo em um novo Plano do Serviço de Aplicativo quando:</span><span class="sxs-lookup"><span data-stu-id="8e84f-140">We recommend isolating your app into a new App Service plan when:</span></span>

- <span data-ttu-id="8e84f-141">O aplicativo faz uso intensivo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8e84f-141">App is resource-intensive.</span></span>
- <span data-ttu-id="8e84f-142">Aplicativo tem diferente fatores de dimensionamento de saudação outros aplicativos hospedados em um plano existente.</span><span class="sxs-lookup"><span data-stu-id="8e84f-142">App has different scaling factors from hello other apps hosted in an existing plan.</span></span>
- <span data-ttu-id="8e84f-143">O aplicativo precisa de recursos em uma região geográfica diferente.</span><span class="sxs-lookup"><span data-stu-id="8e84f-143">App needs resource in a different geographical region.</span></span>

<span data-ttu-id="8e84f-144">Dessa forma, você pode alocar um novo conjunto de recursos para seu aplicativo e ter mais controle sobre seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="8e84f-144">This way you can allocate a new set of resources for your app and gain greater control of your apps.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="8e84f-145">Criar um plano de Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="8e84f-145">Create an App Service plan</span></span>

> [!TIP]
> <span data-ttu-id="8e84f-146">Se você tiver um ambiente de serviço de aplicativo, você pode examinar Olá documentação específica tooApp ambientes de serviço aqui: [criar um plano de serviço de aplicativo em um ambiente de serviço de aplicativo](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)</span><span class="sxs-lookup"><span data-stu-id="8e84f-146">If you have an App Service Environment, you can review hello documentation specific tooApp Service Environments here: [Create an App Service plan in an App Service Environment](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)</span></span>

<span data-ttu-id="8e84f-147">Você pode criar um plano de serviço de aplicativo vazio de saudação experiência de navegação do plano de serviço de aplicativo ou como parte da criação do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8e84f-147">You can create an empty App Service plan from hello App Service plan browse experience or as part of app creation.</span></span>

<span data-ttu-id="8e84f-148">Em Olá [portal do Azure](https://portal.azure.com), clique em **novo** > **Web + móvel**e, em seguida, selecione **aplicativo Web** ou outro tipo de aplicativo de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8e84f-148">In hello [Azure portal](https://portal.azure.com), click **New** > **Web + mobile**, and then select **Web App** or other App Service app kind.</span></span>

![Crie um aplicativo em Olá portal do Azure.][createWebApp]

<span data-ttu-id="8e84f-150">Em seguida, você pode selecionar ou criar hello plano de serviço de aplicativo para o novo aplicativo de saudação.</span><span class="sxs-lookup"><span data-stu-id="8e84f-150">You can then select or create hello App Service plan for hello new app.</span></span>

 ![Crie um plano do Serviço de Aplicativo.][createASP]

<span data-ttu-id="8e84f-152">toocreate um plano de serviço de aplicativo, clique em **[+] criar novos**, Olá tipo **plano de serviço de aplicativo** nome e, em seguida, selecione adequados **local**.</span><span class="sxs-lookup"><span data-stu-id="8e84f-152">toocreate an App Service plan, click **[+] Create New**, type hello **App Service plan** name, and then select an appropriate **Location**.</span></span> <span data-ttu-id="8e84f-153">Clique em **preço**e, em seguida, selecione uma camada de preços apropriada para o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="8e84f-153">Click **Pricing tier**, and then select an appropriate pricing tier for hello service.</span></span> <span data-ttu-id="8e84f-154">Selecione **exibir todos os** tooview preços mais opções, como **livre** e **compartilhado**.</span><span class="sxs-lookup"><span data-stu-id="8e84f-154">Select **View all** tooview more pricing options, such as **Free** and **Shared**.</span></span> <span data-ttu-id="8e84f-155">Depois que você selecionou Olá preço, clique em Olá **selecione** botão.</span><span class="sxs-lookup"><span data-stu-id="8e84f-155">After you have selected hello pricing tier, click hello **Select** button.</span></span>

## <a name="move-an-app-tooa-different-app-service-plan"></a><span data-ttu-id="8e84f-156">Mover um plano de serviço de aplicativo diferente do aplicativo tooa</span><span class="sxs-lookup"><span data-stu-id="8e84f-156">Move an app tooa different App Service plan</span></span>

<span data-ttu-id="8e84f-157">Você pode mover um plano de serviço de aplicativo diferente do aplicativo tooa Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8e84f-157">You can move an app tooa different App Service plan in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="8e84f-158">Você pode mover aplicativos entre planos como planos de saudação estão no hello mesmo grupo de recursos e a região geográfica.</span><span class="sxs-lookup"><span data-stu-id="8e84f-158">You can move apps between plans as long as hello plans are in hello same resource group and geographical region.</span></span>

<span data-ttu-id="8e84f-159">toomove um plano de tooanother do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="8e84f-159">toomove an app tooanother plan:</span></span>

- <span data-ttu-id="8e84f-160">Navegue toohello aplicativo que você deseja toomove.</span><span class="sxs-lookup"><span data-stu-id="8e84f-160">Navigate toohello app that you want toomove.</span></span>
- <span data-ttu-id="8e84f-161">Em Olá **Menu**, procure Olá **plano do serviço de aplicativo** seção.</span><span class="sxs-lookup"><span data-stu-id="8e84f-161">In hello **Menu**, look for hello **App Service Plan** section.</span></span>
- <span data-ttu-id="8e84f-162">Selecione **plano de serviço de aplicativo de alteração** toostart processo de saudação.</span><span class="sxs-lookup"><span data-stu-id="8e84f-162">Select **Change App Service plan** toostart hello process.</span></span>

<span data-ttu-id="8e84f-163">**Plano de serviço de aplicativo de alteração** abre Olá **plano de serviço de aplicativo** seletor.</span><span class="sxs-lookup"><span data-stu-id="8e84f-163">**Change App Service plan** opens hello **App Service plan** selector.</span></span> <span data-ttu-id="8e84f-164">Neste ponto, você pode escolher um toomove plano existente este aplicativo em.</span><span class="sxs-lookup"><span data-stu-id="8e84f-164">At this point, you can pick an existing plan toomove this app into.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e84f-165">plano de serviço de aplicativo Hello select da interface do usuário é filtrado por Olá critérios a seguir:</span><span class="sxs-lookup"><span data-stu-id="8e84f-165">hello select App Service plan UI is filtered by hello following criteria:</span></span>
> - <span data-ttu-id="8e84f-166">Encontra Olá mesmo grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="8e84f-166">Exists within hello same Resource Group</span></span>
> - <span data-ttu-id="8e84f-167">Existe no hello mesma região geográfica</span><span class="sxs-lookup"><span data-stu-id="8e84f-167">Exists in hello same Geographical Region</span></span>
> - <span data-ttu-id="8e84f-168">Encontra Olá mesmo espaço na Web</span><span class="sxs-lookup"><span data-stu-id="8e84f-168">Exists within hello same Webspace</span></span>
>
> <span data-ttu-id="8e84f-169">Um espaço Web é uma construção lógica dentro do Serviço de Aplicativo que define um agrupamento de recursos do servidor.</span><span class="sxs-lookup"><span data-stu-id="8e84f-169">A Webspace is a logical construct within App Service which defines a grouping of server resources.</span></span> <span data-ttu-id="8e84f-170">Uma região geográfica (por exemplo, oeste dos EUA) contém muitos espaços na Web em clientes de tooallocate ordem usando o serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8e84f-170">A Geographical region (such as West US) contains many Webspaces in order tooallocate customers using App Service.</span></span> <span data-ttu-id="8e84f-171">Atualmente, recursos de serviço de aplicativo não capaz de toobe movido entre espaços na Web.</span><span class="sxs-lookup"><span data-stu-id="8e84f-171">Currently, App Service resources aren’t able toobe moved between Webspaces.</span></span>
>

![Seletor de plano do Serviço de Aplicativo.][change]

<span data-ttu-id="8e84f-173">Cada plano tem seu próprio tipo de preço.</span><span class="sxs-lookup"><span data-stu-id="8e84f-173">Each plan has its own pricing tier.</span></span> <span data-ttu-id="8e84f-174">Por exemplo, a movimentação de um site de uma camada de padrão de tooa camada gratuita, permite que todos os aplicativos atribuídos tooit toouse Olá recursos e da camada de saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="8e84f-174">For example, moving a site from a Free tier tooa Standard tier, enables all apps assigned tooit toouse hello features and resources of hello Standard tier.</span></span>

## <a name="clone-an-app-tooa-different-app-service-plan"></a><span data-ttu-id="8e84f-175">Clonar um plano de serviço de aplicativo diferente do aplicativo tooa</span><span class="sxs-lookup"><span data-stu-id="8e84f-175">Clone an app tooa different App Service plan</span></span>

<span data-ttu-id="8e84f-176">Se você quiser toomove Olá aplicativo tooa uma região diferente, uma alternativa é aplicativo clonagem.</span><span class="sxs-lookup"><span data-stu-id="8e84f-176">If you want toomove hello app tooa different region, one alternative is app cloning.</span></span> <span data-ttu-id="8e84f-177">A clonagem faz uma cópia do seu aplicativo em um novo plano do Serviço de Aplicativo existente em qualquer região.</span><span class="sxs-lookup"><span data-stu-id="8e84f-177">Cloning makes a copy of your app in a new or existing App Service plan in any region.</span></span>

<span data-ttu-id="8e84f-178">Você pode encontrar **aplicativo Clone** em Olá **ferramentas de desenvolvimento** seção do menu hello.</span><span class="sxs-lookup"><span data-stu-id="8e84f-178">You can find **Clone App** in hello **Development Tools** section of hello menu.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e84f-179">A clonagem tem algumas limitações que você pode ler a respeito em [Clonagem de aplicativo do Serviço de Aplicativo do Azure usando o portal do Azure](../app-service-web/app-service-web-app-cloning-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8e84f-179">Cloning has some limitations that you can read about at [Azure App Service App cloning using Azure portal](../app-service-web/app-service-web-app-cloning-portal.md).</span></span>

## <a name="scale-an-app-service-plan"></a><span data-ttu-id="8e84f-180">Dimensionar um plano de Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="8e84f-180">Scale an App Service plan</span></span>

<span data-ttu-id="8e84f-181">Há três tooscale de maneiras de um plano:</span><span class="sxs-lookup"><span data-stu-id="8e84f-181">There are three ways tooscale a plan:</span></span>

- <span data-ttu-id="8e84f-182">**Alterar plano de saudação do preço**.</span><span class="sxs-lookup"><span data-stu-id="8e84f-182">**Change hello plan’s pricing tier**.</span></span> <span data-ttu-id="8e84f-183">Um plano na camada básica Olá pode ser convertido tooStandard e todos os aplicativos atribuídos tooit toouse recursos de saudação da camada de saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="8e84f-183">A plan in hello Basic tier can be converted tooStandard, and all apps assigned tooit toouse hello features of hello Standard tier.</span></span>
- <span data-ttu-id="8e84f-184">**Alterar o tamanho da instância do plano Olá**.</span><span class="sxs-lookup"><span data-stu-id="8e84f-184">**Change hello plan’s instance size**.</span></span> <span data-ttu-id="8e84f-185">Por exemplo, um plano na camada básica de saudação que usa pequenas instâncias pode ser alterado toouse grandes instâncias.</span><span class="sxs-lookup"><span data-stu-id="8e84f-185">As an example, a plan in hello Basic tier that uses small instances can be changed toouse large instances.</span></span> <span data-ttu-id="8e84f-186">Todos os aplicativos que estão associados esse plano agora podem usar memória adicional hello e recursos da CPU que Olá oferece maior de tamanho de instância.</span><span class="sxs-lookup"><span data-stu-id="8e84f-186">All apps that are associated with that plan now can use hello additional memory and CPU resources that hello larger instance size offers.</span></span>
- <span data-ttu-id="8e84f-187">**Alterar a contagem de instâncias do plano Olá**.</span><span class="sxs-lookup"><span data-stu-id="8e84f-187">**Change hello plan’s instance count**.</span></span> <span data-ttu-id="8e84f-188">Por exemplo, um plano padrão que é expandido toothree instâncias pode ser dimensionado too10 instâncias.</span><span class="sxs-lookup"><span data-stu-id="8e84f-188">For example, a Standard plan that's scaled out toothree instances can be scaled too10 instances.</span></span> <span data-ttu-id="8e84f-189">Um plano Premium pode ser expandido too20 instâncias (assunto tooavailability).</span><span class="sxs-lookup"><span data-stu-id="8e84f-189">A Premium plan can be scaled out too20 instances (subject tooavailability).</span></span> <span data-ttu-id="8e84f-190">Todos os aplicativos que estão associados esse plano agora podem usar memória adicional hello e recursos da CPU que Olá oferece maior de contagem de instância.</span><span class="sxs-lookup"><span data-stu-id="8e84f-190">All apps that are associated with that plan now can use hello additional memory and CPU resources that hello larger instance count offers.</span></span>

<span data-ttu-id="8e84f-191">Você pode alterar Olá tamanho de instância e de camada de preços clicando Olá **aumentar** item em configurações para o aplicativo hello ou Olá plano de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8e84f-191">You can change hello pricing tier and instance size by clicking hello **Scale Up** item under settings for either hello app or hello App Service plan.</span></span> <span data-ttu-id="8e84f-192">As alterações aplicam toohello plano de serviço de aplicativo e afetam todos os aplicativos que ele hospeda.</span><span class="sxs-lookup"><span data-stu-id="8e84f-192">Changes apply toohello App Service plan and affect all apps that it hosts.</span></span>

 ![Tooscale de valores do conjunto de backup de um aplicativo.][pricingtier]

## <a name="app-service-plan-cleanup"></a><span data-ttu-id="8e84f-194">Limpeza do Plano do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="8e84f-194">App Service plan cleanup</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e84f-195">**Planos de serviço de aplicativo** com nenhuma toothem aplicativos associados ainda incorrendo em encargos, pois eles continuam a capacidade de computação tooreserve hello.</span><span class="sxs-lookup"><span data-stu-id="8e84f-195">**App Service plans** that have no apps associated toothem still incur charges since they continue tooreserve hello compute capacity.</span></span>

<span data-ttu-id="8e84f-196">tooavoid inesperados encargos, quando o aplicativo do último Olá hospedado em um plano de serviço de aplicativo for excluído, Olá vazio resultante plano de serviço de aplicativo também será excluído.</span><span class="sxs-lookup"><span data-stu-id="8e84f-196">tooavoid unexpected charges, when hello last app hosted in an App Service plan is deleted, hello resulting empty App Service plan is also deleted.</span></span>

## <a name="summary"></a><span data-ttu-id="8e84f-197">Resumo</span><span class="sxs-lookup"><span data-stu-id="8e84f-197">Summary</span></span>

<span data-ttu-id="8e84f-198">Os planos de Serviço de Aplicativo representam um conjunto de recursos e capacidades que pode ser compartilhado entre seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="8e84f-198">App Service plans represent a set of features and capacity that you can share across your apps.</span></span> <span data-ttu-id="8e84f-199">Planos de serviço de aplicativo dê Olá conjunto de tooa do flexibilidade tooallocate aplicativos específicos de recursos e otimizar ainda mais a utilização de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="8e84f-199">App Service plans give you hello flexibility tooallocate specific apps tooa set of resources and further optimize your Azure resource utilization.</span></span> <span data-ttu-id="8e84f-200">Dessa forma, se você quiser toosave dinheiro em seu ambiente de teste, você pode compartilhar um plano entre vários aplicativos.</span><span class="sxs-lookup"><span data-stu-id="8e84f-200">This way, if you want toosave money on your testing environment, you can share a plan across multiple apps.</span></span> <span data-ttu-id="8e84f-201">Você também pode maximizar a produtividade para seu ambiente de produção dimensionando-o em várias regiões e planos.</span><span class="sxs-lookup"><span data-stu-id="8e84f-201">You can also maximize throughput for your production environment by scaling it across multiple regions and plans.</span></span>

## <a name="whats-changed"></a><span data-ttu-id="8e84f-202">O que mudou</span><span class="sxs-lookup"><span data-stu-id="8e84f-202">What's changed</span></span>

- <span data-ttu-id="8e84f-203">Uma alteração de toohello do guia de sites tooApp serviço, consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="8e84f-203">For a guide toohello change from Websites tooApp Service, see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[pricingtier]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/appserviceplan-pricingtier.png
[assign]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/assing-appserviceplan.png
[change]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/change-appserviceplan.png
[createASP]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-appserviceplan.png
[createWebApp]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-web-app.png
