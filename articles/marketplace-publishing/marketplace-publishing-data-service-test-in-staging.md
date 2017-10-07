---
title: "aaaTesting seu serviço de dados oferecem para Olá Marketplace | Microsoft Docs"
description: "Entenda como tootest seu serviço de dados oferecem para hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e861bd11-f74d-4d77-b4b5-23fb463644ad
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 1b9c7027d8e0818b9bdee5cfca971bab25dd1959
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="testing-your-data-service-offer-in-staging"></a><span data-ttu-id="8ee79-103">Testando sua oferta do Serviço de Dados no preparo</span><span class="sxs-lookup"><span data-stu-id="8ee79-103">Testing your Data Service offer in Staging</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8ee79-104">**Neste momento, não estamos mais realizando a integração de novos editores de Serviço de Dados. Novos serviços de dados não serão ser aprovados para listagem.**</span><span class="sxs-lookup"><span data-stu-id="8ee79-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="8ee79-105">Se você tiver um aplicativo de negócios SaaS você gostaria que toopublish em AppSource, você pode encontrar mais informações [aqui](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="8ee79-105">If you have a SaaS business application you would like toopublish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="8ee79-106">Se você tiver aplicativos de IaaS ou desenvolvedor de serviço seria como toopublish no Azure Marketplace, você pode encontrar mais informações [aqui](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="8ee79-106">If you have an IaaS applications or developer service you would like toopublish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

<span data-ttu-id="8ee79-107">Depois de concluir as duas primeiras etapas saudação do [criação de sua conta do Microsoft Developer](marketplace-publishing-accounts-creation-registration.md) e [criando sua oferta de serviço de dados no Portal de publicação](marketplace-publishing-data-service-creation.md) você está pronto para disponibilizar sua oferta no Olá Marketplace do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ee79-107">After completing hello first two steps of [Creating your Microsoft Developer account](marketplace-publishing-accounts-creation-registration.md) and [Creating your Data Service Offer in Publishing Portal](marketplace-publishing-data-service-creation.md) you’re ready for making your offer available in hello Azure Marketplace.</span></span> <span data-ttu-id="8ee79-108">Este tópico orientará Olá primeiro, intermediário, chamada "preparação" de etapa</span><span class="sxs-lookup"><span data-stu-id="8ee79-108">This topic will walk you through hello first, intermediate, step called “Staging”</span></span>

<span data-ttu-id="8ee79-109">Preparo significa Implantando sua oferta em uma "área restrita" onde você pode testar e verificar sua funcionalidade antes de enviar a ele tooproduction particular.</span><span class="sxs-lookup"><span data-stu-id="8ee79-109">Staging means deploying your offer in a private "sandbox" where you can test and verify its functionality before pushing it tooproduction.</span></span> <span data-ttu-id="8ee79-110">oferta Hello serão exibidos no preparo como faria cliente tooa que implantou a ele.</span><span class="sxs-lookup"><span data-stu-id="8ee79-110">hello offer will appear in staging just as it would tooa customer who has deployed it.</span></span>

## <a name="step-1-pushing-your-offer-toostaging"></a><span data-ttu-id="8ee79-111">Etapa 1.</span><span class="sxs-lookup"><span data-stu-id="8ee79-111">Step 1.</span></span> <span data-ttu-id="8ee79-112">Enviar por push toostaging sua oferta</span><span class="sxs-lookup"><span data-stu-id="8ee79-112">Pushing your offer toostaging</span></span>
<span data-ttu-id="8ee79-113">Enviar por push toostaging sua oferta permite que você tootest oferta de saudação antes de se tornar disponível toofuture assinantes.</span><span class="sxs-lookup"><span data-stu-id="8ee79-113">Pushing your offer toostaging allows you tootest hello offer before it becomes available toofuture subscribers.</span></span>  <span data-ttu-id="8ee79-114">Você pode ver como sua oferta aparecerá e funcione para aqueles que se inscreveram tooyour dados.</span><span class="sxs-lookup"><span data-stu-id="8ee79-114">You can see how your offer will appear and function for those subscribing tooyour data.</span></span>  

  ![desenho](media/marketplace-publishing-data-service-test-in-staging/step-1.1.png)

1. <span data-ttu-id="8ee79-116">Fazer logon no hello [Portal de publicação](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="8ee79-116">Login into hello [Publishing Portal](https://publish.windowsazure.com)</span></span>
2. <span data-ttu-id="8ee79-117">Selecione **Data Services** na janela de navegação à esquerda da saudação</span><span class="sxs-lookup"><span data-stu-id="8ee79-117">Select **Data Services** in hello left navigation window</span></span>
3. <span data-ttu-id="8ee79-118">Selecione a oferta desejada toopush toostaging.</span><span class="sxs-lookup"><span data-stu-id="8ee79-118">Select your offer you want toopush toostaging.</span></span> <span data-ttu-id="8ee79-119">Você verá Olá acima da tela.</span><span class="sxs-lookup"><span data-stu-id="8ee79-119">You will see hello above screen.</span></span>
4. <span data-ttu-id="8ee79-120">Clique em **Push tooStaging** botão.</span><span class="sxs-lookup"><span data-stu-id="8ee79-120">Click **Push tooStaging** button.</span></span>  
5. <span data-ttu-id="8ee79-121">Se houver problemas com hello oferta que necessário toobe concluída toostaging toopushing anterior, você verá uma lista exibida.</span><span class="sxs-lookup"><span data-stu-id="8ee79-121">If there are issues with hello offer that needed toobe completed prior toopushing toostaging, you will see a list displayed.</span></span>  <span data-ttu-id="8ee79-122">Corrija esses itens clicando em cada item na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="8ee79-122">Correct these items by clicking on each item in hello list.</span></span> <span data-ttu-id="8ee79-123">Quando todas as correções feitas, clique em **Push tooStaging** novamente.</span><span class="sxs-lookup"><span data-stu-id="8ee79-123">When all corrections made, click **Push tooStaging** button again.</span></span>

<span data-ttu-id="8ee79-124">Se não houver nenhum problema com sua oferta você verá a janela pop-up de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="8ee79-124">If there are no issues with your offer you will see hello popup window below.</span></span>  

<span data-ttu-id="8ee79-125">Se você não estiver planejando/não aprovado toosurface sua oferta no Portal do Azure (atualmente tem capacidade limitada), e a janela pop-up Olá apenas fechar.</span><span class="sxs-lookup"><span data-stu-id="8ee79-125">If you’re not planning/not approved toosurface your offer in Azure Portal (currently has limited capacity), then just close hello pop-up window.</span></span>

<span data-ttu-id="8ee79-126">tootest seus dados de serviço no Portal do Azure (no portal de DataMarket de toohello adição), você precisará tootest uma ID de assinatura do Azure com.</span><span class="sxs-lookup"><span data-stu-id="8ee79-126">tootest your Data Service in Azure Portal (in addition toohello DataMarket portal), you will need an Azure Subscription ID tootest with.</span></span>  <span data-ttu-id="8ee79-127">Essa ID de assinatura identificará conta Olá que será permitido tootest sua oferta.</span><span class="sxs-lookup"><span data-stu-id="8ee79-127">This Subscription ID will identify hello account that will be allowed tootest your offer.</span></span>  

<span data-ttu-id="8ee79-128">Recorte e cole sua ID de assinatura e clique em Olá toocontinue de marca de seleção.</span><span class="sxs-lookup"><span data-stu-id="8ee79-128">Cut and paste your Subscription ID and click hello checkmark toocontinue.</span></span>

  ![desenho](media/marketplace-publishing-data-service-test-in-staging/step-1.2.png)

> [!NOTE]
> <span data-ttu-id="8ee79-130">Essas identificações de assinaturas do Azure só são necessários para teste e no hello [Portal de gerenciamento](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="8ee79-130">These Azure subscriptions IDs are only required for testing and staging in hello [Azure Management Portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="8ee79-131">Eles não são necessário tootest no Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="8ee79-131">They are not required tootest in Azure Marketplace.</span></span>
> 
> 

<span data-ttu-id="8ee79-132">Olá próxima tela exibida mostra que a publicação está ocorrendo exibindo hello "em andamento" ícone realçado amarelo abaixo.</span><span class="sxs-lookup"><span data-stu-id="8ee79-132">hello next screen that appears shows that publishing is taking place by displaying hello “In progress” icon highlighted yellow below.</span></span> <span data-ttu-id="8ee79-133">Enviar por push toostaging leva de 10 minutos too15.</span><span class="sxs-lookup"><span data-stu-id="8ee79-133">Pushing toostaging takes between 10 too15 minutes.</span></span>  <span data-ttu-id="8ee79-134">Se levar mais tempo, primeiro atualize seu navegador (pressione F5 no IE).</span><span class="sxs-lookup"><span data-stu-id="8ee79-134">If it takes longer, first refresh your browser (press F5 in IE).</span></span>  <span data-ttu-id="8ee79-135">Olá raros casos em que sua oferta é ainda envio por push toostaging após uma hora, clique em contato Olá nos vincular toolet nos saber se há um problema.</span><span class="sxs-lookup"><span data-stu-id="8ee79-135">In hello rare cases where your offer is still pushing toostaging after an hour, click hello contact us link toolet us know that there is an issue.</span></span>

  ![desenho](media/marketplace-publishing-data-service-test-in-staging/step-1.3.png)

<span data-ttu-id="8ee79-137">Quando Olá Push tooStaging conclui hello "em andamento" ícone irá parar mover e Olá status será atualizado muito "preparação".</span><span class="sxs-lookup"><span data-stu-id="8ee79-137">When hello Push tooStaging completes hello “In progress” icon will stop moving and hello status will be updated too“Staged”.</span></span>  <span data-ttu-id="8ee79-138">Você está agora pronto tootest sua oferta.</span><span class="sxs-lookup"><span data-stu-id="8ee79-138">You are now ready tootest your offer.</span></span>  

## <a name="step-2-test-your-staged-offer-in-datamarket"></a><span data-ttu-id="8ee79-139">Etapa 2.</span><span class="sxs-lookup"><span data-stu-id="8ee79-139">Step 2.</span></span> <span data-ttu-id="8ee79-140">Testar sua oferta preparada no DataMarket</span><span class="sxs-lookup"><span data-stu-id="8ee79-140">Test your staged offer in DataMarket</span></span>
<span data-ttu-id="8ee79-141">Clique em link Olá depois do texto de saudação **"ver seu serviço oferecem em...."**</span><span class="sxs-lookup"><span data-stu-id="8ee79-141">Click hello link following hello text **“See Your service offer at…”**</span></span> <span data-ttu-id="8ee79-142">tela hello toodisplay que Olá assinante será exibida quando a sua oferta fica tooproduction e aparecerá no DataMarket.</span><span class="sxs-lookup"><span data-stu-id="8ee79-142">toodisplay hello screen that hello subscriber will see when your offer goes tooproduction and will appear in DataMarket.</span></span>

  ![desenho](media/marketplace-publishing-data-service-test-in-staging/step-2.2.png)

<span data-ttu-id="8ee79-144">Teste ou verifique se cada um dos 12 itens de saudação marcado acima tooensure todos os logotipos, preços/transações, texto, imagens, documentação e links estão corretas e funcionando corretamente.</span><span class="sxs-lookup"><span data-stu-id="8ee79-144">Test or verify each of hello 12 items marked above tooensure all logos, prices/transactions, text, images, documentation, and links are correct and working properly.</span></span>  <span data-ttu-id="8ee79-145">Este é um tooensure bom momento quaisquer valores de teste inseridos durante a criação de sua oferta foram substituídos por valores reais.</span><span class="sxs-lookup"><span data-stu-id="8ee79-145">This is a good time tooensure any test values you entered when creating your offer have been replaced with actual values.</span></span>

1. <span data-ttu-id="8ee79-146">Logotipo da oferta</span><span class="sxs-lookup"><span data-stu-id="8ee79-146">Offer logo</span></span>
2. <span data-ttu-id="8ee79-147">Nome da oferta</span><span class="sxs-lookup"><span data-stu-id="8ee79-147">Offer name</span></span>
3. <span data-ttu-id="8ee79-148">Site da empresa das tooyour de link do nome do publicador</span><span class="sxs-lookup"><span data-stu-id="8ee79-148">Publisher name/link tooyour company's website</span></span>
4. <span data-ttu-id="8ee79-149">Pesquisar categorias para a oferta</span><span class="sxs-lookup"><span data-stu-id="8ee79-149">Search categories for your offer</span></span>
5. <span data-ttu-id="8ee79-150">Assinantes de tooassist de link de suporte da oferta</span><span class="sxs-lookup"><span data-stu-id="8ee79-150">Your offer's support link tooassist subscribers</span></span>
6. <span data-ttu-id="8ee79-151">Descrição contextual da oferta</span><span class="sxs-lookup"><span data-stu-id="8ee79-151">Contextual description for your offer</span></span>
7. <span data-ttu-id="8ee79-152">Plano de oferta que descreve os detalhes de cobrança</span><span class="sxs-lookup"><span data-stu-id="8ee79-152">Offer plan depicting billing details</span></span>
8. <span data-ttu-id="8ee79-153">Código de tooimplementation de link</span><span class="sxs-lookup"><span data-stu-id="8ee79-153">Link tooimplementation code</span></span>
9. <span data-ttu-id="8ee79-154">Imagens de exemplo que ilustram o uso dos dados da oferta</span><span class="sxs-lookup"><span data-stu-id="8ee79-154">Sample images that illustrate use of offer data</span></span>
10. <span data-ttu-id="8ee79-155">Metadados de entrada/saída para cada serviço na oferta de saudação</span><span class="sxs-lookup"><span data-stu-id="8ee79-155">Input/Output metadata for each service within hello offer</span></span>
11. <span data-ttu-id="8ee79-156">Termos de Uso da oferta</span><span class="sxs-lookup"><span data-stu-id="8ee79-156">Offer's Terms of Use</span></span>
12. <span data-ttu-id="8ee79-157">Visualização dos dados da oferta do hello</span><span class="sxs-lookup"><span data-stu-id="8ee79-157">Preview of hello offer's data</span></span>

<span data-ttu-id="8ee79-158">Finalmente, verifique o serviço Olá funcionará por meio de saudação do Datamarket clicando o link hello "Explorar este conjunto de dados".</span><span class="sxs-lookup"><span data-stu-id="8ee79-158">Finally, check hello service will work through hello Datamarket by clicking hello link “EXPLORE THIS DATASET”.</span></span>  <span data-ttu-id="8ee79-159">Uma nova janela será aberta na ferramenta Olá chamamos "Gerenciador de serviços" para que você pode visualizar os resultados de saudação de uma consulta em relação a seu serviço.</span><span class="sxs-lookup"><span data-stu-id="8ee79-159">A new window will open in hello tool we call “Service Explorer” so you can preview hello results of a query against your service.</span></span>  <span data-ttu-id="8ee79-160">Nessa janela, você pode inserir Olá parâmetros necessários e ver os resultados de saudação exibidos a partir de uma consulta em relação a seu serviço.</span><span class="sxs-lookup"><span data-stu-id="8ee79-160">In this window, you can enter hello parameters needed and see hello results displayed from a query against your service.</span></span>   <span data-ttu-id="8ee79-161">Além disso, exibido é Olá URL para a sua consulta.</span><span class="sxs-lookup"><span data-stu-id="8ee79-161">Also, displayed is hello URL for your Query.</span></span>  

> [!NOTE]
> <span data-ttu-id="8ee79-162">Ser se tooreview Olá descrição textual Olá serviço exibida na parte superior da saudação.</span><span class="sxs-lookup"><span data-stu-id="8ee79-162">Be sure tooreview hello textual description of hello service displayed at hello top.</span></span>  <span data-ttu-id="8ee79-163">E se sua oferta consiste em mais de um serviço chamam, clique nas guias de saudação em Olá inferior tooswitch toohello próximo serviço tooreview e teste.</span><span class="sxs-lookup"><span data-stu-id="8ee79-163">And if your offer consists of more than one service call, click hello tabs at hello bottom tooswitch toohello next service tooreview and test.</span></span>
> 
> 

## <a name="next-step"></a><span data-ttu-id="8ee79-164">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="8ee79-164">Next step</span></span>
<span data-ttu-id="8ee79-165">Se você estiver tendo problemas e precisar de ajuda para resolvê-los, entre em contato com o [Suporte do Editor do Azure](http://go.microsoft.com/fwlink/?LinkId=272975).</span><span class="sxs-lookup"><span data-stu-id="8ee79-165">If you are having issues and need help resolving them please contact [Azure Publisher Support](http://go.microsoft.com/fwlink/?LinkId=272975).</span></span>

<span data-ttu-id="8ee79-166">Se você estiver satisfeito e pronto toopublish sua oferta, leia Olá [solicitar aprovação tooPush tooProduction](marketplace-publishing-push-to-production.md) documentação.</span><span class="sxs-lookup"><span data-stu-id="8ee79-166">If you are satisfied and ready toopublish your offer please read hello [Request Approval tooPush tooProduction](marketplace-publishing-push-to-production.md) documentation.</span></span>

## <a name="see-also"></a><span data-ttu-id="8ee79-167">Consulte também</span><span class="sxs-lookup"><span data-stu-id="8ee79-167">See Also</span></span>
* [<span data-ttu-id="8ee79-168">Guia de Introdução: Como toopublish toohello uma oferta do Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="8ee79-168">Getting Started: How toopublish an offer toohello Azure Marketplace</span></span>](marketplace-publishing-getting-started.md)

