---
title: "Guia para a criação de um Serviço de Dados para o Marketplace | Microsoft Docs"
description: "Instruções detalhadas sobre como criar, certificar e implantar um Serviço de Dados para compra no Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 96194198-6991-43b4-918e-ee337e250339
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: c0c9362f1c2e15c947aaaf7187f3383ad243140f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="data-service-publishing-guide-for-the-azure-marketplace"></a><span data-ttu-id="665c9-103">Guia de publicação do Serviço de Dados para o Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="665c9-103">Data Service Publishing Guide for the Azure Marketplace</span></span>
> [!IMPORTANT]
> <span data-ttu-id="665c9-104">**Neste momento, não estamos mais realizando a integração de novos editores de Serviço de Dados. Novos serviços de dados não serão ser aprovados para listagem.**</span><span class="sxs-lookup"><span data-stu-id="665c9-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="665c9-105">Se você tiver um aplicativo de negócios de SaaS que quer publicar no AppSource, encontre mais informações [aqui](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="665c9-105">If you have a SaaS business application you would like to publish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="665c9-106">Se você tiver aplicativos de IaaS ou serviços de desenvolvedor para publicar no Azure Marketplace, saiba mais [aqui](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="665c9-106">If you have an IaaS applications or developer service you would like to publish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="665c9-107">Após concluir a etapa 1, [Criação e registro de conta](marketplace-publishing-accounts-creation-registration.md), orientamos você pelos [Requisitos gerais não técnicos](marketplace-publishing-pre-requisites.md) e [técnicos](marketplace-publishing-data-service-creation-prerequisites.md) de uma oferta de Serviço de Dados no Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="665c9-107">After completing the step 1, [Account Creation and Registration](marketplace-publishing-accounts-creation-registration.md), we guided you through the [General Non-Technical](marketplace-publishing-pre-requisites.md) and [Technical Requirements](marketplace-publishing-data-service-creation-prerequisites.md) of a Data Service offer on Azure Marketplace.</span></span> <span data-ttu-id="665c9-108">Agora, orientaremos você pelas etapas de criação de uma oferta de Serviço de Dados no [Portal de Publicação][link-pubportal] do Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="665c9-108">Now we will walk you through the steps for creating a Data Service offer on the [Publishing Portal][link-pubportal] for the Azure Marketplace.</span></span>

## <a name="1----login-to-the-publishing-portal"></a><span data-ttu-id="665c9-109">1.    Faça logon no Portal de Publicação.</span><span class="sxs-lookup"><span data-stu-id="665c9-109">1.    Login to the Publishing Portal.</span></span>
<span data-ttu-id="665c9-110">Vá para [https://publish.windowsazure.com](https://publish.windowsazure.com.)</span><span class="sxs-lookup"><span data-stu-id="665c9-110">Go to [https://publish.windowsazure.com](https://publish.windowsazure.com.)</span></span>

<span data-ttu-id="665c9-111">**Ao fazer logon pela primeira vez no Portal de Publicação, use a mesma conta utilizada para o registro de Perfil de Vendedor de sua empresa na Central de desenvolvedores.**</span><span class="sxs-lookup"><span data-stu-id="665c9-111">**For first time login to Publishing Portal, use the same account with which your company’s Seller Profile was registered in Developer Center.**</span></span>  <span data-ttu-id="665c9-112">(Posteriormente, você poderá adicionar qualquer funcionário de sua empresa como um coadministrador no Portal de Publicação).</span><span class="sxs-lookup"><span data-stu-id="665c9-112">(Later you can add any employee of your company as a co-admin in the Publishing Portal).</span></span>

<span data-ttu-id="665c9-113">Clique no bloco **Publicar Serviços de Dados** se esse for o primeiro logon no portal de publicação.</span><span class="sxs-lookup"><span data-stu-id="665c9-113">Click on the **Publish a Data Services** tile if this is the first login into the publishing portal.</span></span>

## <a name="2----choose-data-services-in-the-navigation-menu-on-the-left-side"></a><span data-ttu-id="665c9-114">2.    Escolha **Serviços de Dados** no menu de navegação à esquerda.</span><span class="sxs-lookup"><span data-stu-id="665c9-114">2.    Choose **Data Services** in the navigation menu on the left side.</span></span>
  ![desenho](media/marketplace-publishing-data-service-creation/pubportal-main-nav.png)

## <a name="3----create-a-new-data-service"></a><span data-ttu-id="665c9-116">3.    Crie um novo Serviço de Dados</span><span class="sxs-lookup"><span data-stu-id="665c9-116">3.    Create a New Data Service</span></span>
<span data-ttu-id="665c9-117">Preencha o título da nova Oferta de Serviço de Dados e clique em "+" à direita.</span><span class="sxs-lookup"><span data-stu-id="665c9-117">Fill in the title for your new Data Service Offer and click on “+” on the right.</span></span>

  ![desenho](media/marketplace-publishing-data-service-creation/step-3.png)

## <a name="4----review-the-sub-menu-under-the-newly-created-data-service-in-the-navigation-menu"></a><span data-ttu-id="665c9-119">4.    Examine o submenu do Serviço de Dados recém-criado no menu de navegação.</span><span class="sxs-lookup"><span data-stu-id="665c9-119">4.    Review the sub-menu under the newly created Data Service in the navigation menu.</span></span>
<span data-ttu-id="665c9-120">Clique na guia **Passo a passo** e examine todas as etapas necessárias para publicar corretamente o Serviço de Dados no Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="665c9-120">Click on the **Walkthrough** tab and review all necessary steps needed to publish properly the Data Service on the Azure Marketplace.</span></span>

> [!TIP]
> <span data-ttu-id="665c9-121">Você sempre pode clicar nos links na página "Passo a passo" ou usar guias no submenu da oferta de Serviço de Dados no lado esquerdo.</span><span class="sxs-lookup"><span data-stu-id="665c9-121">You always can click on the links in the “Walkthrough” page or use tabs on the Data Service offer’s sub-menu on the left side.</span></span>
> 
> 

## <a name="5----create-a-new-plan"></a><span data-ttu-id="665c9-122">5.    Crie um novo Plano.</span><span class="sxs-lookup"><span data-stu-id="665c9-122">5.    Create a new Plan.</span></span>
### <a name="offers-plans-transactions"></a><span data-ttu-id="665c9-123">Ofertas, planos, transações.</span><span class="sxs-lookup"><span data-stu-id="665c9-123">Offers, Plans, transactions.</span></span>
<span data-ttu-id="665c9-124">Cada oferta pode ter vários planos, mas a quantidade mínima de planos é 1 (um).</span><span class="sxs-lookup"><span data-stu-id="665c9-124">Each Offer can have multiple Plans, but must have at least one (1) Plan.</span></span> <span data-ttu-id="665c9-125">Quando os usuários finais se inscrevem em sua oferta, eles se inscrevem em um dos planos da oferta.</span><span class="sxs-lookup"><span data-stu-id="665c9-125">When end-users subscribe to your offer they subscribe for one of the offer’s Plan.</span></span> <span data-ttu-id="665c9-126">Cada plano define como os usuários finais poderão usar o serviço.</span><span class="sxs-lookup"><span data-stu-id="665c9-126">Each plan defines how end-users will be able to use your service.</span></span>

<span data-ttu-id="665c9-127">Atualmente, o Azure Marketplace dá suporte somente ao modelo baseado em transações da assinatura mensal para Serviços de Dados, ou seja, os usuários finais pagarão uma taxa mensal de acordo com os preços dos planos específicos que assinaram e poderão a cada mês consumir a quantidade de transações definidas pelo plano.</span><span class="sxs-lookup"><span data-stu-id="665c9-127">Currently Azure Marketplace support only Monthly Subscription Transaction Based model for Data Services, i.e. end-users will pay monthly fee according to the price of the specific plan they subscribed to and will be able to consume each month number of transaction defined by the plan.</span></span>

<span data-ttu-id="665c9-128">Cada transação é normalmente definida como o número de registros que o Serviço de Dados retornará com base na consulta enviada ao serviço.</span><span class="sxs-lookup"><span data-stu-id="665c9-128">Each Transaction usually defined as number of records your Data Service will return based on the query sent to the Service.</span></span> <span data-ttu-id="665c9-129">O padrão é 100.</span><span class="sxs-lookup"><span data-stu-id="665c9-129">The default is 100.</span></span> <span data-ttu-id="665c9-130">O número de transações retornadas para cada consulta é o número de registros dividido por 100 e arredondado para cima até o inteiro mais próximo.</span><span class="sxs-lookup"><span data-stu-id="665c9-130">Number of transactions returned to each query will be number of records divided by 100 and rounded up to the closest integer.</span></span>

<span data-ttu-id="665c9-131">É responsabilidade da camada de serviço do Azure Marketplace monitorar (medir) o número de transações consumidas por cada consulta.</span><span class="sxs-lookup"><span data-stu-id="665c9-131">It’s Azure Marketplace Service layer responsibility to monitor (meter) number of transactions consumed by each query.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="665c9-132">Os usuários finais que atingirem o limite de transação durante o mês serão impedidos de continuar a usar o serviço até o final do ciclo de assinatura mensal.</span><span class="sxs-lookup"><span data-stu-id="665c9-132">End-Users which reached the transaction limit during the month will be blocked from continuing to use the service until end of their monthly subscription cycle.</span></span>
> 
> <span data-ttu-id="665c9-133">O plano ou um dos planos pode (mas não é obrigatório) incluir um número ilimitado de transações.</span><span class="sxs-lookup"><span data-stu-id="665c9-133">The plan or one of the plans can (but not must) include unlimited number of transactions.</span></span>
> 
> 

### <a name="create-a-plan"></a><span data-ttu-id="665c9-134">Crie um plano.</span><span class="sxs-lookup"><span data-stu-id="665c9-134">Create a plan.</span></span>
1. <span data-ttu-id="665c9-135">Clique em **"+"** ao lado de "Adicionar um novo plano".</span><span class="sxs-lookup"><span data-stu-id="665c9-135">Click on **“+”** next to the “Add a new plan”.</span></span>
2. <span data-ttu-id="665c9-136">Escolha uma das opções: uso **Ilimitado** ou **Limitado** para esse plano.</span><span class="sxs-lookup"><span data-stu-id="665c9-136">Choose one of the options: **Unlimited** or **Limited** usage for this plan.</span></span>  <span data-ttu-id="665c9-137">Se Limitado, forneça o número de transações mensais permitido pelo plano.</span><span class="sxs-lookup"><span data-stu-id="665c9-137">If Limited then provide the number of transaction the plan will allow to consume in a month.</span></span>
   
    ![desenho](media/marketplace-publishing-data-service-creation/step-5.1.png)  
   
    <span data-ttu-id="665c9-139">O Portal de Publicação também sugere um "Identificador de Plano", que é usado para se comunicar com os usuários finais, é usado como nome do plano na interface do usuário e também é usado pelo Serviço Marketplace para identificar o Plano.</span><span class="sxs-lookup"><span data-stu-id="665c9-139">Publishing Portal will also suggest “Plan Identifier”, which will be used to communicate to the end-users the name of the plan in the UI and also used by the Market Place Service to identify the Plan.</span></span> <span data-ttu-id="665c9-140">Se desejar, você pode alterar o "Identificador de Plano".</span><span class="sxs-lookup"><span data-stu-id="665c9-140">You can change the “Plan Identifier” if you want.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="665c9-141">O "Identificador de Plano" deve ser exclusivo dentro do escopo de cada oferta.</span><span class="sxs-lookup"><span data-stu-id="665c9-141">The “Plan Identifier” must be unique within the scope of each offer.</span></span> <span data-ttu-id="665c9-142">Como muitos outros identificadores usados no Portal de Publicação, ele será bloqueado após a primeira publicação para produção e você não poderá alterá-lo.</span><span class="sxs-lookup"><span data-stu-id="665c9-142">As many other Identifiers used in the Publishing Portal Plan identifier will be locked after the first publishing to production and you will not be able to change this identifier.</span></span>
   > 
   > 
3. <span data-ttu-id="665c9-143">Clique para aceitar sua escolha.</span><span class="sxs-lookup"><span data-stu-id="665c9-143">Click to accept your choice.</span></span>
4. <span data-ttu-id="665c9-144">Em seguida, você deve responder a algumas perguntas adicionais sobre seu plano recém-criado.</span><span class="sxs-lookup"><span data-stu-id="665c9-144">Then you will be asked few additional questions regarding your newly created Plan.</span></span>
   
    ![desenho](media/marketplace-publishing-data-service-creation/step-5.2.png)

| <span data-ttu-id="665c9-146">Pergunta</span><span class="sxs-lookup"><span data-stu-id="665c9-146">Question</span></span> | <span data-ttu-id="665c9-147">Significado</span><span class="sxs-lookup"><span data-stu-id="665c9-147">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="665c9-148">**Este Plano é gratuito e está disponível em todo o mundo?**</span><span class="sxs-lookup"><span data-stu-id="665c9-148">**This Plan is free and available world-wide?**</span></span> |<span data-ttu-id="665c9-149">Você pode criar um plano totalmente gratuito.</span><span class="sxs-lookup"><span data-stu-id="665c9-149">You can create a completely free-of-charge plan.</span></span> <span data-ttu-id="665c9-150">Se é o único plano para essa oferta, significa que você está publicando uma "Oferta Gratuita" no Marketplace.</span><span class="sxs-lookup"><span data-stu-id="665c9-150">If it’s the only plan for this offer – it means that you are publishing “Free Offer” in the Marketplace.</span></span> <span data-ttu-id="665c9-151">Se é apenas para um plano (ou alguns), ele dá a opção de permitir que os usuários finais saibam mais sobre seu serviço com um número relativamente pequeno de transações por mês.</span><span class="sxs-lookup"><span data-stu-id="665c9-151">If it’s only for one (of few) Plan, the it gives you an option to offer end-users to learn more about your service with a relatively small number of transactions per month.</span></span>  <span data-ttu-id="665c9-152">Se a resposta for "Sim", nenhuma outra pergunta será feita.</span><span class="sxs-lookup"><span data-stu-id="665c9-152">If the answer is "Yes," then no further questions will be asked.</span></span> |

> [!NOTE]
> <span data-ttu-id="665c9-153">Os usuários finais sempre poderão atualizar para os planos pagos.</span><span class="sxs-lookup"><span data-stu-id="665c9-153">End users can always upgrade to the paid plans.</span></span>
> 
> 

| <span data-ttu-id="665c9-154">Pergunta</span><span class="sxs-lookup"><span data-stu-id="665c9-154">Question</span></span> | <span data-ttu-id="665c9-155">Significado</span><span class="sxs-lookup"><span data-stu-id="665c9-155">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="665c9-156">**Existe uma avaliação gratuita disponível?**</span><span class="sxs-lookup"><span data-stu-id="665c9-156">**Is free trial available?**</span></span> |<span data-ttu-id="665c9-157">Você pode escolher entre "Sem avaliação" ou uma opção para usar seu plano por "Um mês".</span><span class="sxs-lookup"><span data-stu-id="665c9-157">You can choose between “No Trial” at all or give an option to use your Plan for “One Month”.</span></span> <span data-ttu-id="665c9-158">Os editores gostam de usar essa opção para permitir aos usuários finais compreender os benefícios da oferta gratuitamente por um mês.</span><span class="sxs-lookup"><span data-stu-id="665c9-158">Publishers like to use this option to provide end-users the possibility to understand the benefits of the offer for free for one month.</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="665c9-159">Os usuários finais só poderão adquirir uma avaliação gratuita se inserirem um instrumento de pagamento, por exemplo, cartão de crédito, contrato empresarial.</span><span class="sxs-lookup"><span data-stu-id="665c9-159">End-users will only be able to purchase a free trial if they have established payment instrument e.g. credit card, enterprise agreement.</span></span>
> 
> <span data-ttu-id="665c9-160">Depois de um mês de avaliação gratuita, o Azure Marketplace começará a cobrar o preço dos clientes a partir da data da assinatura, a menos que o cliente tenha iniciado seu cancelamento.</span><span class="sxs-lookup"><span data-stu-id="665c9-160">After one month of the free trial, Azure Marketplace will start charging customers the price as of the date of the subscription, unless the customer initiated the subscription cancellation.</span></span> <span data-ttu-id="665c9-161">Nenhuma notificação especial será feita para os usuários finais.</span><span class="sxs-lookup"><span data-stu-id="665c9-161">No special notification will be provided to the end-users.</span></span>
> 
> 

| <span data-ttu-id="665c9-162">Pergunta</span><span class="sxs-lookup"><span data-stu-id="665c9-162">Question</span></span> | <span data-ttu-id="665c9-163">Significado</span><span class="sxs-lookup"><span data-stu-id="665c9-163">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="665c9-164">**O plano requer um código promocional de compra?**</span><span class="sxs-lookup"><span data-stu-id="665c9-164">**This plan requires a promotion code to purchase?**</span></span> |<span data-ttu-id="665c9-165">Os editores têm a opção de limitar o acesso a seus planos de serviço fornecendo um código especial, chamado "Código promocional A", para clientes específicos.</span><span class="sxs-lookup"><span data-stu-id="665c9-165">Publishers have an option to limit access to their Service Plans by providing a special code, called “A Promocode” to specific customers.</span></span> <span data-ttu-id="665c9-166">Somente os usuários finais com esse código promocional poderão assinar o plano.</span><span class="sxs-lookup"><span data-stu-id="665c9-166">Only end-users which will have this Promocode will be able to subscribe to the Plan.</span></span> <span data-ttu-id="665c9-167">Se você escolher "Não", concorda que todos da região onde a oferta está disponível (confira o [Guia de conteúdo de marketing do Marketplace](marketplace-publishing-push-to-staging.md) para obter mais detalhes) poderão assinar esse plano.</span><span class="sxs-lookup"><span data-stu-id="665c9-167">If you choose “No”, then you agree that everyone from the region where the offer is available (See [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) for more details) will be able to subscribe to this plan.</span></span> <span data-ttu-id="665c9-168">Não será feita nenhuma outra pergunta.</span><span class="sxs-lookup"><span data-stu-id="665c9-168">No further questions will be asked.</span></span> |
| <span data-ttu-id="665c9-169">**Ocultar esse plano de qualquer pessoa que não tenha um código de promoção válido?**</span><span class="sxs-lookup"><span data-stu-id="665c9-169">**Also hide this plan from anyone who doesn’t have a valid promotion code?**</span></span> |<span data-ttu-id="665c9-170">Se a resposta à pergunta anterior for "Sim", o editor terá a opção de remover completamente a exibição desse plano da interface do usuário no Marketplace.</span><span class="sxs-lookup"><span data-stu-id="665c9-170">If the answer to the previous question is “Yes” the Publisher has an option to completely remove this plan from appearing in the UI of the Marketplace.</span></span> <span data-ttu-id="665c9-171">Isso significa que os clientes não verão esse plano na página de detalhes da Oferta.</span><span class="sxs-lookup"><span data-stu-id="665c9-171">It means, customers will not see this plan in the Offer’s details page.</span></span> <span data-ttu-id="665c9-172">Os usuários finais que receberem um código promocional para comprá-la poderão se inscrever na oferta usado o código </span><span class="sxs-lookup"><span data-stu-id="665c9-172">End-users which will receive a promocode to purchase it, will be able to subscribe to it using this promocode.</span></span> |

## <a name="6----create-your-marketplace-marketing-content"></a><span data-ttu-id="665c9-173">6.    Criar conteúdo de marketing do Marketplace</span><span class="sxs-lookup"><span data-stu-id="665c9-173">6.    Create your Marketplace marketing content</span></span>
<span data-ttu-id="665c9-174">Para saber como fornecer as informações necessárias nas guias **Marketing, Preço, Suporte e Categorias** , visite [Guia de conteúdo de marketing do Marketplace](marketplace-publishing-push-to-staging.md) , que é comum a todos os artefatos publicados no Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="665c9-174">For How to provide information required in **Marketing, Pricing, Support and Categories** tabs please visit [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) which is common to all artifacts published in the Azure Marketplace.</span></span>  

## <a name="7----connect-your-offer-to-your-service-sql-azure-based-or-web-service-based"></a><span data-ttu-id="665c9-175">7.    Conecte a oferta ao seu Serviço (baseado no SQL Azure ou em serviço Web).</span><span class="sxs-lookup"><span data-stu-id="665c9-175">7.    Connect your offer to your Service (SQL Azure based or Web Service based).</span></span>
<span data-ttu-id="665c9-176">Clique no submenu **Serviços de Dados** .</span><span class="sxs-lookup"><span data-stu-id="665c9-176">Click on the **Data Services** sub-menu.</span></span>

<span data-ttu-id="665c9-177">Na metade superior da página, insira o **Namespace**da oferta.</span><span class="sxs-lookup"><span data-stu-id="665c9-177">On the upper half of the page you’ll be asked to provide the offer’s **Namespace**.</span></span>  

  ![desenho](media/marketplace-publishing-data-service-creation/step-7.png)

<span data-ttu-id="665c9-179">A pergunta a seguir define como editor vai expor a oferta recém-criada no Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="665c9-179">The below question will define how the Publisher is going to expose newly created offer to Azure Marketplace.</span></span> <span data-ttu-id="665c9-180">(Para obter mais detalhes, confira o [Guia de pré-requisito técnico de Serviços de Dados](marketplace-publishing-data-service-creation-prerequisites.md)).</span><span class="sxs-lookup"><span data-stu-id="665c9-180">(For more details see the [Data Services Technical Prerequisite Guide](marketplace-publishing-data-service-creation-prerequisites.md)).</span></span>

  ![desenho](media/marketplace-publishing-data-service-creation/step-7.2.png)

<span data-ttu-id="665c9-182">**Publicando o serviço baseado em Banco de Dados**</span><span class="sxs-lookup"><span data-stu-id="665c9-182">**Publishing the Database based service**</span></span>

<span data-ttu-id="665c9-183">Clique em **Banco de Dados**.</span><span class="sxs-lookup"><span data-stu-id="665c9-183">Click on **Database**.</span></span> <span data-ttu-id="665c9-184">A página abaixo será exibida:</span><span class="sxs-lookup"><span data-stu-id="665c9-184">The following page will appear:</span></span>

  ![desenho](media/marketplace-publishing-data-service-creation/step-7.3.png)

<span data-ttu-id="665c9-186">Para criar um mapeamento CSDL para o conjunto de dados baseado no Banco de Dados SQL Azure:</span><span class="sxs-lookup"><span data-stu-id="665c9-186">To create a CSDL mapping for the Dataset based on the SQL Azure DB:</span></span>

  ![desenho](media/marketplace-publishing-data-service-creation/step-7.4.png)

<span data-ttu-id="665c9-188">E para cada tabela</span><span class="sxs-lookup"><span data-stu-id="665c9-188">And then for each table</span></span>

  ![desenho](media/marketplace-publishing-data-service-creation/step-7.5.png)

  ![desenho](media/marketplace-publishing-data-service-creation/step-7.6.png)

<span data-ttu-id="665c9-191">Se for serviço Web</span><span class="sxs-lookup"><span data-stu-id="665c9-191">If Web Service</span></span>

  ![desenho](media/marketplace-publishing-data-service-creation/step-7.7.png)

> [!IMPORTANT]
> <span data-ttu-id="665c9-193">Leia [Mapeando um serviço Web existente para OData por meio de CSDL](marketplace-publishing-data-service-creation-odata-mapping.md) para obter instruções detalhadas e exemplos de como criar um serviço Web CSDL.</span><span class="sxs-lookup"><span data-stu-id="665c9-193">Read [Mapping an existing web service to OData through CSDL](marketplace-publishing-data-service-creation-odata-mapping.md) for detailed instructions and examples for creating a CSDL Web Service.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="665c9-194">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="665c9-194">Next Steps</span></span>
<span data-ttu-id="665c9-195">Agora que você criou sua oferta de Serviço de Dados, não deixe de concluir as instruções no [Guia de conteúdo de marketing do Marketplace](marketplace-publishing-push-to-staging.md) antes de avançar para [Testando seu Serviço de Dados em preparação](marketplace-publishing-data-service-test-in-staging.md).</span><span class="sxs-lookup"><span data-stu-id="665c9-195">Now that you've created your Data Service offer, please ensure that you complete the instructions in the [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) before you move forward to [Testing your Data Service in Staging](marketplace-publishing-data-service-test-in-staging.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="665c9-196">Consulte também</span><span class="sxs-lookup"><span data-stu-id="665c9-196">See Also</span></span>
* [<span data-ttu-id="665c9-197">Introdução: como publicar uma oferta no Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="665c9-197">Getting Started: How to publish an offer to the Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* <span data-ttu-id="665c9-198">Se estiver interessado em entender o processo e a finalidade geral do mapeamento de OData, leia este artigo [Mapeamento OData de Serviço de Dados](marketplace-publishing-data-service-creation-odata-mapping.md) para examinar as definições, as estruturas e as instruções.</span><span class="sxs-lookup"><span data-stu-id="665c9-198">If you are interested in understanding the overall OData mapping process and purpose, read this article [Data Service OData Mapping](marketplace-publishing-data-service-creation-odata-mapping.md) to review definitions, structures, and instructions.</span></span>
* <span data-ttu-id="665c9-199">Se estiver interessado em aprender e em compreender os nós específicos e seus parâmetros, leia este artigo [Nós do mapeamento OData de Serviço de Dados](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) para obter definições, explicações, exemplos e contexto de casos de uso.</span><span class="sxs-lookup"><span data-stu-id="665c9-199">If you are interested in learning and understanding the specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="665c9-200">Se estiver interessado em examinar exemplos, leia este artigo [Exemplos de mapeamento OData de Serviço de Dados](marketplace-publishing-data-service-creation-odata-mapping-examples.md) para ver um código de exemplo e compreender a sintaxe do código e o contexto.</span><span class="sxs-lookup"><span data-stu-id="665c9-200">If you are interested in reviewing examples, read this article [Data Service OData Mapping Examples](marketplace-publishing-data-service-creation-odata-mapping-examples.md) to see sample code and understand code syntax and context.</span></span>

[link-pubportal]:https://publish.windowsazure.com
