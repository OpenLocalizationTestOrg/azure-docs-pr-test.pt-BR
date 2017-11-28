---
title: "aaaGuide toocreating um serviço de dados para Olá Marketplace | Microsoft Docs"
description: "Instruções detalhadas de como toocreate, certificar e implantar um serviço de dados para compra em hello Azure Marketplace."
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
ms.openlocfilehash: 0220d357ae0ec89e7d4f6399605850e57c646f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="data-service-publishing-guide-for-hello-azure-marketplace"></a><span data-ttu-id="97988-103">Guia de publicação de serviço de dados para hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="97988-103">Data Service Publishing Guide for hello Azure Marketplace</span></span>
> [!IMPORTANT]
> <span data-ttu-id="97988-104">**Neste momento, não estamos mais realizando a integração de novos editores de Serviço de Dados. Novos serviços de dados não serão ser aprovados para listagem.**</span><span class="sxs-lookup"><span data-stu-id="97988-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="97988-105">Se você tiver um aplicativo de negócios SaaS você gostaria que toopublish em AppSource, você pode encontrar mais informações [aqui](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="97988-105">If you have a SaaS business application you would like toopublish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="97988-106">Se você tiver aplicativos de IaaS ou desenvolvedor de serviço seria como toopublish no Azure Marketplace, você pode encontrar mais informações [aqui](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="97988-106">If you have an IaaS applications or developer service you would like toopublish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="97988-107">Depois de concluir a etapa de saudação 1, [criação da conta e o registro](marketplace-publishing-accounts-creation-registration.md), que você é orientado pelos Olá [geral não técnico](marketplace-publishing-pre-requisites.md) e [requisitos técnicos](marketplace-publishing-data-service-creation-prerequisites.md) de um serviço de dados oferta no Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="97988-107">After completing hello step 1, [Account Creation and Registration](marketplace-publishing-accounts-creation-registration.md), we guided you through hello [General Non-Technical](marketplace-publishing-pre-requisites.md) and [Technical Requirements](marketplace-publishing-data-service-creation-prerequisites.md) of a Data Service offer on Azure Marketplace.</span></span> <span data-ttu-id="97988-108">Agora podemos irá orientá-lo pelas etapas de saudação para criar uma oferta de serviço de dados em Olá [Portal de publicação] [ link-pubportal] para hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="97988-108">Now we will walk you through hello steps for creating a Data Service offer on hello [Publishing Portal][link-pubportal] for hello Azure Marketplace.</span></span>

## <a name="1----login-toohello-publishing-portal"></a><span data-ttu-id="97988-109">1.    Logon toohello Portal de publicação.</span><span class="sxs-lookup"><span data-stu-id="97988-109">1.    Login toohello Publishing Portal.</span></span>
<span data-ttu-id="97988-110">Vá muito[https://publish.windowsazure.com](https://publish.windowsazure.com.)</span><span class="sxs-lookup"><span data-stu-id="97988-110">Go too[https://publish.windowsazure.com](https://publish.windowsazure.com.)</span></span>

<span data-ttu-id="97988-111">**Para a primeira hora logon tooPublishing Portal, use Olá a mesma conta com a qual o vendedor da sua empresa perfil foi registrada no Centro de desenvolvedores.**</span><span class="sxs-lookup"><span data-stu-id="97988-111">**For first time login tooPublishing Portal, use hello same account with which your company’s Seller Profile was registered in Developer Center.**</span></span>  <span data-ttu-id="97988-112">(Mais tarde você pode adicionar qualquer funcionário da sua empresa como um coadministrador no Portal de publicação de saudação).</span><span class="sxs-lookup"><span data-stu-id="97988-112">(Later you can add any employee of your company as a co-admin in hello Publishing Portal).</span></span>

<span data-ttu-id="97988-113">Clique em Olá **publicar uma Data Services** se esse for o primeiro o logon no portal de publicação Olá Olá lado a lado.</span><span class="sxs-lookup"><span data-stu-id="97988-113">Click on hello **Publish a Data Services** tile if this is hello first login into hello publishing portal.</span></span>

## <a name="2----choose-data-services-in-hello-navigation-menu-on-hello-left-side"></a><span data-ttu-id="97988-114">2.    Escolha **Data Services** no menu de navegação Olá no lado esquerdo de saudação.</span><span class="sxs-lookup"><span data-stu-id="97988-114">2.    Choose **Data Services** in hello navigation menu on hello left side.</span></span>
  ![desenho](media/marketplace-publishing-data-service-creation/pubportal-main-nav.png)

## <a name="3----create-a-new-data-service"></a><span data-ttu-id="97988-116">3.    Crie um novo Serviço de Dados</span><span class="sxs-lookup"><span data-stu-id="97988-116">3.    Create a New Data Service</span></span>
<span data-ttu-id="97988-117">Preencha título Olá para sua nova oferta de serviço de dados e clique em "+" na saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="97988-117">Fill in hello title for your new Data Service Offer and click on “+” on hello right.</span></span>

  ![desenho](media/marketplace-publishing-data-service-creation/step-3.png)

## <a name="4----review-hello-sub-menu-under-hello-newly-created-data-service-in-hello-navigation-menu"></a><span data-ttu-id="97988-119">4.    Revisão Olá submenu em Olá recém-criados serviço de dados no menu de navegação hello.</span><span class="sxs-lookup"><span data-stu-id="97988-119">4.    Review hello sub-menu under hello newly created Data Service in hello navigation menu.</span></span>
<span data-ttu-id="97988-120">Clique em Olá **passo a passo** guia e examinar todas as etapas necessárias necessário toopublish corretamente Olá serviço de dados em hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="97988-120">Click on hello **Walkthrough** tab and review all necessary steps needed toopublish properly hello Data Service on hello Azure Marketplace.</span></span>

> [!TIP]
> <span data-ttu-id="97988-121">Você sempre pode clique nos links de saudação na página de "Passo a passo" hello ou usar guias no submenu da oferta de serviço de dados Olá no lado esquerdo da saudação.</span><span class="sxs-lookup"><span data-stu-id="97988-121">You always can click on hello links in hello “Walkthrough” page or use tabs on hello Data Service offer’s sub-menu on hello left side.</span></span>
> 
> 

## <a name="5----create-a-new-plan"></a><span data-ttu-id="97988-122">5.    Crie um novo Plano.</span><span class="sxs-lookup"><span data-stu-id="97988-122">5.    Create a new Plan.</span></span>
### <a name="offers-plans-transactions"></a><span data-ttu-id="97988-123">Ofertas, planos, transações.</span><span class="sxs-lookup"><span data-stu-id="97988-123">Offers, Plans, transactions.</span></span>
<span data-ttu-id="97988-124">Cada oferta pode ter vários planos, mas a quantidade mínima de planos é 1 (um).</span><span class="sxs-lookup"><span data-stu-id="97988-124">Each Offer can have multiple Plans, but must have at least one (1) Plan.</span></span> <span data-ttu-id="97988-125">Quando os usuários finais se inscreve tooyour oferta eles se inscrever para uma plano do oferta de saudação.</span><span class="sxs-lookup"><span data-stu-id="97988-125">When end-users subscribe tooyour offer they subscribe for one of hello offer’s Plan.</span></span> <span data-ttu-id="97988-126">Cada plano define como os usuários finais vai ser capaz de toouse seu serviço.</span><span class="sxs-lookup"><span data-stu-id="97988-126">Each plan defines how end-users will be able toouse your service.</span></span>

<span data-ttu-id="97988-127">No momento Azure Marketplace oferece suporte a apenas mensal assinatura transação modelo com base em serviços de dados, ou seja, os usuários finais pagará taxa mensal de acordo com o preço de toohello de plano específico hello, eles inscrito tooand será capaz de tooconsume cada número de mês de transação definida pelo plano de saudação.</span><span class="sxs-lookup"><span data-stu-id="97988-127">Currently Azure Marketplace support only Monthly Subscription Transaction Based model for Data Services, i.e. end-users will pay monthly fee according toohello price of hello specific plan they subscribed tooand will be able tooconsume each month number of transaction defined by hello plan.</span></span>

<span data-ttu-id="97988-128">Cada transação geralmente definida como o número de registros que o serviço de dados retornará com base em consulta Olá toohello serviço.</span><span class="sxs-lookup"><span data-stu-id="97988-128">Each Transaction usually defined as number of records your Data Service will return based on hello query sent toohello Service.</span></span> <span data-ttu-id="97988-129">saudação padrão é 100.</span><span class="sxs-lookup"><span data-stu-id="97988-129">hello default is 100.</span></span> <span data-ttu-id="97988-130">Número de transações retornado tooeach consulta será dividido por 100 de número de registros e arredondado até o inteiro mais próximo toohello.</span><span class="sxs-lookup"><span data-stu-id="97988-130">Number of transactions returned tooeach query will be number of records divided by 100 and rounded up toohello closest integer.</span></span>

<span data-ttu-id="97988-131">É o Azure Marketplace serviço camada responsabilidade toomonitor (medidor) o número de transações consumida por cada consulta.</span><span class="sxs-lookup"><span data-stu-id="97988-131">It’s Azure Marketplace Service layer responsibility toomonitor (meter) number of transactions consumed by each query.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="97988-132">Os usuários finais que atingiu o limite de transação Olá durante o mês de saudação serão impedidos de continuar o serviço de saudação do toouse até o final de seu ciclo de assinatura mensal.</span><span class="sxs-lookup"><span data-stu-id="97988-132">End-Users which reached hello transaction limit during hello month will be blocked from continuing toouse hello service until end of their monthly subscription cycle.</span></span>
> 
> <span data-ttu-id="97988-133">Olá plano ou um dos planos de saudação pode (mas não deve) incluem um número ilimitado de transações.</span><span class="sxs-lookup"><span data-stu-id="97988-133">hello plan or one of hello plans can (but not must) include unlimited number of transactions.</span></span>
> 
> 

### <a name="create-a-plan"></a><span data-ttu-id="97988-134">Crie um plano.</span><span class="sxs-lookup"><span data-stu-id="97988-134">Create a plan.</span></span>
1. <span data-ttu-id="97988-135">Clique em **"+"** toohello próximo "adicionar um novo plano".</span><span class="sxs-lookup"><span data-stu-id="97988-135">Click on **“+”** next toohello “Add a new plan”.</span></span>
2. <span data-ttu-id="97988-136">Escolha uma das opções de saudação: **Unlimited** ou **limitado** uso para este plano.</span><span class="sxs-lookup"><span data-stu-id="97988-136">Choose one of hello options: **Unlimited** or **Limited** usage for this plan.</span></span>  <span data-ttu-id="97988-137">Se limitado, em seguida, forneça o número de saudação do plano de saudação transação permitirá tooconsume em um mês.</span><span class="sxs-lookup"><span data-stu-id="97988-137">If Limited then provide hello number of transaction hello plan will allow tooconsume in a month.</span></span>
   
    ![desenho](media/marketplace-publishing-data-service-creation/step-5.1.png)  
   
    <span data-ttu-id="97988-139">Portal de publicação também sugere "Identificador de plano", que será usado toocommunicate toohello os usuários finais Olá nome do plano Olá Olá da interface do usuário e também usada pela Olá tooidentify de serviço do mercado Olá plano.</span><span class="sxs-lookup"><span data-stu-id="97988-139">Publishing Portal will also suggest “Plan Identifier”, which will be used toocommunicate toohello end-users hello name of hello plan in hello UI and also used by hello Market Place Service tooidentify hello Plan.</span></span> <span data-ttu-id="97988-140">Se desejar, você pode alterar hello "Identificador de plano".</span><span class="sxs-lookup"><span data-stu-id="97988-140">You can change hello “Plan Identifier” if you want.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="97988-141">Olá "Identificador de plano" deve ser exclusivo no escopo de saudação de cada oferta.</span><span class="sxs-lookup"><span data-stu-id="97988-141">hello “Plan Identifier” must be unique within hello scope of each offer.</span></span> <span data-ttu-id="97988-142">Como muitos outros identificadores usado no hello planejar publicação de Portal identificador será bloqueado após hello tooproduction publicação primeiro e você não será capaz de toochange esse identificador.</span><span class="sxs-lookup"><span data-stu-id="97988-142">As many other Identifiers used in hello Publishing Portal Plan identifier will be locked after hello first publishing tooproduction and you will not be able toochange this identifier.</span></span>
   > 
   > 
3. <span data-ttu-id="97988-143">Clique em tooaccept sua escolha.</span><span class="sxs-lookup"><span data-stu-id="97988-143">Click tooaccept your choice.</span></span>
4. <span data-ttu-id="97988-144">Em seguida, você deve responder a algumas perguntas adicionais sobre seu plano recém-criado.</span><span class="sxs-lookup"><span data-stu-id="97988-144">Then you will be asked few additional questions regarding your newly created Plan.</span></span>
   
    ![desenho](media/marketplace-publishing-data-service-creation/step-5.2.png)

| <span data-ttu-id="97988-146">Pergunta</span><span class="sxs-lookup"><span data-stu-id="97988-146">Question</span></span> | <span data-ttu-id="97988-147">Significado</span><span class="sxs-lookup"><span data-stu-id="97988-147">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="97988-148">**Este Plano é gratuito e está disponível em todo o mundo?**</span><span class="sxs-lookup"><span data-stu-id="97988-148">**This Plan is free and available world-wide?**</span></span> |<span data-ttu-id="97988-149">Você pode criar um plano totalmente gratuito.</span><span class="sxs-lookup"><span data-stu-id="97988-149">You can create a completely free-of-charge plan.</span></span> <span data-ttu-id="97988-150">Se seu Olá apenas plano para essa oferta – isso significa que você está publicando "Oferecem livre" em Olá Marketplace.</span><span class="sxs-lookup"><span data-stu-id="97988-150">If it’s hello only plan for this offer – it means that you are publishing “Free Offer” in hello Marketplace.</span></span> <span data-ttu-id="97988-151">Se for somente para um (de alguns) plano, Olá lhe toolearn de usuários finais de toooffer uma opção mais sobre o serviço com um número relativamente pequeno de transações por mês.</span><span class="sxs-lookup"><span data-stu-id="97988-151">If it’s only for one (of few) Plan, hello it gives you an option toooffer end-users toolearn more about your service with a relatively small number of transactions per month.</span></span>  <span data-ttu-id="97988-152">Se a resposta de saudação é "Sim", serão solicitadas sem mais perguntas.</span><span class="sxs-lookup"><span data-stu-id="97988-152">If hello answer is "Yes," then no further questions will be asked.</span></span> |

> [!NOTE]
> <span data-ttu-id="97988-153">Os usuários finais podem sempre atualize toohello paga planos.</span><span class="sxs-lookup"><span data-stu-id="97988-153">End users can always upgrade toohello paid plans.</span></span>
> 
> 

| <span data-ttu-id="97988-154">Pergunta</span><span class="sxs-lookup"><span data-stu-id="97988-154">Question</span></span> | <span data-ttu-id="97988-155">Significado</span><span class="sxs-lookup"><span data-stu-id="97988-155">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="97988-156">**Existe uma avaliação gratuita disponível?**</span><span class="sxs-lookup"><span data-stu-id="97988-156">**Is free trial available?**</span></span> |<span data-ttu-id="97988-157">Você pode escolher entre "Sem avaliação" em todos os ou oferecem uma opção toouse seu plano para "Um mês".</span><span class="sxs-lookup"><span data-stu-id="97988-157">You can choose between “No Trial” at all or give an option toouse your Plan for “One Month”.</span></span> <span data-ttu-id="97988-158">Editores como toouse esse opção tooprovide os usuários finais Olá possibilidade toounderstand Olá benefícios Olá oferecem gratuitamente por um mês.</span><span class="sxs-lookup"><span data-stu-id="97988-158">Publishers like toouse this option tooprovide end-users hello possibility toounderstand hello benefits of hello offer for free for one month.</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="97988-159">Os usuários finais só será capaz de toopurchase uma avaliação gratuita se estabelecerem instrumento de pagamento, por exemplo, cartão de crédito, contrato enterprise.</span><span class="sxs-lookup"><span data-stu-id="97988-159">End-users will only be able toopurchase a free trial if they have established payment instrument e.g. credit card, enterprise agreement.</span></span>
> 
> <span data-ttu-id="97988-160">Depois de um mês de avaliação gratuita hello, Azure Marketplace será iniciado Carregando clientes preço Olá data Olá da assinatura hello, a menos que o cliente Olá iniciou o cancelamento de assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="97988-160">After one month of hello free trial, Azure Marketplace will start charging customers hello price as of hello date of hello subscription, unless hello customer initiated hello subscription cancellation.</span></span> <span data-ttu-id="97988-161">Nenhuma notificação especial será fornecida toohello os usuários finais.</span><span class="sxs-lookup"><span data-stu-id="97988-161">No special notification will be provided toohello end-users.</span></span>
> 
> 

| <span data-ttu-id="97988-162">Pergunta</span><span class="sxs-lookup"><span data-stu-id="97988-162">Question</span></span> | <span data-ttu-id="97988-163">Significado</span><span class="sxs-lookup"><span data-stu-id="97988-163">Significance</span></span> |
| --- | --- |
| <span data-ttu-id="97988-164">**Este plano requer um toopurchase de código de promoção?**</span><span class="sxs-lookup"><span data-stu-id="97988-164">**This plan requires a promotion code toopurchase?**</span></span> |<span data-ttu-id="97988-165">Editores têm uma opção toolimit acesso tootheir que planos de serviço, fornecendo um código especial, chamado "A Promocode" toospecific clientes.</span><span class="sxs-lookup"><span data-stu-id="97988-165">Publishers have an option toolimit access tootheir Service Plans by providing a special code, called “A Promocode” toospecific customers.</span></span> <span data-ttu-id="97988-166">Somente os usuários finais que terão esse Promocode será capaz de toosubscribe toohello plano.</span><span class="sxs-lookup"><span data-stu-id="97988-166">Only end-users which will have this Promocode will be able toosubscribe toohello Plan.</span></span> <span data-ttu-id="97988-167">Se você escolher "Não", você concorda que todos da região Olá onde Olá oferecem estão disponível (consulte [guia de conteúdo de Marketing do Marketplace](marketplace-publishing-push-to-staging.md) para obter mais detalhes) será capaz de toosubscribe toothis plano.</span><span class="sxs-lookup"><span data-stu-id="97988-167">If you choose “No”, then you agree that everyone from hello region where hello offer is available (See [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) for more details) will be able toosubscribe toothis plan.</span></span> <span data-ttu-id="97988-168">Não será feita nenhuma outra pergunta.</span><span class="sxs-lookup"><span data-stu-id="97988-168">No further questions will be asked.</span></span> |
| <span data-ttu-id="97988-169">**Ocultar esse plano de qualquer pessoa que não tenha um código de promoção válido?**</span><span class="sxs-lookup"><span data-stu-id="97988-169">**Also hide this plan from anyone who doesn’t have a valid promotion code?**</span></span> |<span data-ttu-id="97988-170">Se a pergunta do hello resposta toohello anterior é "Sim" hello publicador tem toocompletely uma opção remover esse plano apareçam nos Olá interface de usuário do Marketplace de saudação.</span><span class="sxs-lookup"><span data-stu-id="97988-170">If hello answer toohello previous question is “Yes” hello Publisher has an option toocompletely remove this plan from appearing in hello UI of hello Marketplace.</span></span> <span data-ttu-id="97988-171">Isso significa que, os clientes não verão este plano na página de detalhes da oferta do hello.</span><span class="sxs-lookup"><span data-stu-id="97988-171">It means, customers will not see this plan in hello Offer’s details page.</span></span> <span data-ttu-id="97988-172">Os usuários finais que irá receber um toopurchase promocode, será capaz de toosubscribe tooit usando este promocode.</span><span class="sxs-lookup"><span data-stu-id="97988-172">End-users which will receive a promocode toopurchase it, will be able toosubscribe tooit using this promocode.</span></span> |

## <a name="6----create-your-marketplace-marketing-content"></a><span data-ttu-id="97988-173">6.    Criar conteúdo de marketing do Marketplace</span><span class="sxs-lookup"><span data-stu-id="97988-173">6.    Create your Marketplace marketing content</span></span>
<span data-ttu-id="97988-174">Para como tooprovide informações necessárias, na **Marketing, preços, suporte e categorias** guias, visite [guia de conteúdo de Marketing do Marketplace](marketplace-publishing-push-to-staging.md) que é comum artefatos tooall publicados em Olá Marketplace do Azure.</span><span class="sxs-lookup"><span data-stu-id="97988-174">For How tooprovide information required in **Marketing, Pricing, Support and Categories** tabs please visit [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) which is common tooall artifacts published in hello Azure Marketplace.</span></span>  

## <a name="7----connect-your-offer-tooyour-service-sql-azure-based-or-web-service-based"></a><span data-ttu-id="97988-175">7.    Conecte-se tooyour sua oferta de serviço (SQL Azure com base ou serviço da Web com base).</span><span class="sxs-lookup"><span data-stu-id="97988-175">7.    Connect your offer tooyour Service (SQL Azure based or Web Service based).</span></span>
<span data-ttu-id="97988-176">Clique em Olá **Data Services** submenu.</span><span class="sxs-lookup"><span data-stu-id="97988-176">Click on hello **Data Services** sub-menu.</span></span>

<span data-ttu-id="97988-177">Na metade superior do hello da página Olá deverá da oferta do hello tooprovide **Namespace**.</span><span class="sxs-lookup"><span data-stu-id="97988-177">On hello upper half of hello page you’ll be asked tooprovide hello offer’s **Namespace**.</span></span>  

  ![desenho](media/marketplace-publishing-data-service-creation/step-7.png)

<span data-ttu-id="97988-179">Olá abaixo pergunta definirá como Olá publicador será tooexpose recém-criado oferta tooAzure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="97988-179">hello below question will define how hello Publisher is going tooexpose newly created offer tooAzure Marketplace.</span></span> <span data-ttu-id="97988-180">(Para obter mais detalhes, consulte Olá [guia pré-requisito técnico de serviços de dados](marketplace-publishing-data-service-creation-prerequisites.md)).</span><span class="sxs-lookup"><span data-stu-id="97988-180">(For more details see hello [Data Services Technical Prerequisite Guide](marketplace-publishing-data-service-creation-prerequisites.md)).</span></span>

  ![desenho](media/marketplace-publishing-data-service-creation/step-7.2.png)

<span data-ttu-id="97988-182">**Publicando Olá banco de dados com base em serviço**</span><span class="sxs-lookup"><span data-stu-id="97988-182">**Publishing hello Database based service**</span></span>

<span data-ttu-id="97988-183">Clique em **Banco de Dados**.</span><span class="sxs-lookup"><span data-stu-id="97988-183">Click on **Database**.</span></span> <span data-ttu-id="97988-184">saudação de página a seguir será exibida:</span><span class="sxs-lookup"><span data-stu-id="97988-184">hello following page will appear:</span></span>

  ![desenho](media/marketplace-publishing-data-service-creation/step-7.3.png)

<span data-ttu-id="97988-186">toocreate um mapeamento de CSDL para Olá conjunto de dados com base em Olá banco de dados do SQL Azure:</span><span class="sxs-lookup"><span data-stu-id="97988-186">toocreate a CSDL mapping for hello Dataset based on hello SQL Azure DB:</span></span>

  ![desenho](media/marketplace-publishing-data-service-creation/step-7.4.png)

<span data-ttu-id="97988-188">E para cada tabela</span><span class="sxs-lookup"><span data-stu-id="97988-188">And then for each table</span></span>

  ![desenho](media/marketplace-publishing-data-service-creation/step-7.5.png)

  ![desenho](media/marketplace-publishing-data-service-creation/step-7.6.png)

<span data-ttu-id="97988-191">Se for serviço Web</span><span class="sxs-lookup"><span data-stu-id="97988-191">If Web Service</span></span>

  ![desenho](media/marketplace-publishing-data-service-creation/step-7.7.png)

> [!IMPORTANT]
> <span data-ttu-id="97988-193">Leitura [mapeamento existente web tooOData de serviço por meio de CSDL](marketplace-publishing-data-service-creation-odata-mapping.md) para obter instruções detalhadas e exemplos para a criação de um serviço Web de CSDL.</span><span class="sxs-lookup"><span data-stu-id="97988-193">Read [Mapping an existing web service tooOData through CSDL](marketplace-publishing-data-service-creation-odata-mapping.md) for detailed instructions and examples for creating a CSDL Web Service.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="97988-194">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="97988-194">Next Steps</span></span>
<span data-ttu-id="97988-195">Agora que você criou sua oferta de serviço de dados, certifique-se de que você conclua instruções Olá Olá [guia de conteúdo de Marketing do Marketplace](marketplace-publishing-push-to-staging.md) antes de você Avançar muito[Testando seu serviço de dados de preparo](marketplace-publishing-data-service-test-in-staging.md).</span><span class="sxs-lookup"><span data-stu-id="97988-195">Now that you've created your Data Service offer, please ensure that you complete hello instructions in hello [Marketplace Marketing Content Guide](marketplace-publishing-push-to-staging.md) before you move forward too[Testing your Data Service in Staging](marketplace-publishing-data-service-test-in-staging.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="97988-196">Consulte também</span><span class="sxs-lookup"><span data-stu-id="97988-196">See Also</span></span>
* [<span data-ttu-id="97988-197">Guia de Introdução: Como toopublish toohello uma oferta do Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="97988-197">Getting Started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)
* <span data-ttu-id="97988-198">Se você estiver interessado em entender Olá processo geral de mapeamento de OData e a finalidade, leia este artigo [dados serviço OData mapeamento](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview definições, estruturas e instruções.</span><span class="sxs-lookup"><span data-stu-id="97988-198">If you are interested in understanding hello overall OData mapping process and purpose, read this article [Data Service OData Mapping](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview definitions, structures, and instructions.</span></span>
* <span data-ttu-id="97988-199">Se você estiver interessado em aprendizado e nós específicos de saudação de compreensão e seus parâmetros, leia este artigo [dados serviço OData mapeamento nós](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) para definições e explicações, exemplos e contexto de casos de uso.</span><span class="sxs-lookup"><span data-stu-id="97988-199">If you are interested in learning and understanding hello specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="97988-200">Se você estiver interessado em examinar os exemplos, leia este artigo [dados serviço OData mapeamento exemplos](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee código de exemplo e entender a sintaxe de código e o contexto.</span><span class="sxs-lookup"><span data-stu-id="97988-200">If you are interested in reviewing examples, read this article [Data Service OData Mapping Examples](marketplace-publishing-data-service-creation-odata-mapping-examples.md) toosee sample code and understand code syntax and context.</span></span>

[link-pubportal]:https://publish.windowsazure.com
