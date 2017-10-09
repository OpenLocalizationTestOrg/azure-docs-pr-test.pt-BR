---
title: "tooAzure de serviço web Marketplace de aprendizado de máquina de publicação de AAA(deprecated) | Microsoft Docs"
description: "(preterido) Como toopublish toohello seu serviço de Web de aprendizado de máquina do Azure Marketplace do Azure"
services: machine-learning
documentationcenter: 
author: BharathS
manager: jhubbard
editor: cgronlun
ms.assetid: 68e908be-3a99-4cd7-9517-e2b5f2f341b8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: machine-learning-gallery-experiments
redirect_document_id: True
ms.openlocfilehash: 149abc3df9b79c1b37d233d5e85e803592ff1020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-publish-azure-machine-learning-web-service-toohello-azure-marketplace"></a><span data-ttu-id="eb5ff-103">(preterido) Publicar o serviço de Web de aprendizado de máquina do Azure toohello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="eb5ff-103">(deprecated) Publish Azure Machine Learning Web Service toohello Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="eb5ff-104">O DataMarket e os Serviços de Dados estão sendo desativados e as assinaturas existentes serão desativadas e canceladas a partir de 31/3/2017.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-104">DataMarket and Data Services are being retired, and existing subscriptions will be retired and cancelled starting 3/31/2017.</span></span> <span data-ttu-id="eb5ff-105">Como resultado, este artigo está sendo preterido.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-105">As a result, this article is being deprecated.</span></span> 
> 
> <span data-ttu-id="eb5ff-106">Como alternativa, você pode publicar seu toohello experiências de aprendizado de máquina [Cortana Intelligence galeria](https://gallery.cortanaintelligence.com/) para o benefício de saudação da comunidade de ciência de dados hello.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-106">As an alternative, you can publish your Machine Learning experiments toohello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) for hello benefit of hello data science community.</span></span> <span data-ttu-id="eb5ff-107">Para obter mais informações, consulte [compartilhamento e descobrir recursos na Olá Cortana Intelligence galeria](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span><span class="sxs-lookup"><span data-stu-id="eb5ff-107">For more information, see [Share and discover resources in hello Cortana Intelligence Gallery](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).</span></span>

<span data-ttu-id="eb5ff-108">Olá Marketplace do Azure fornece a capacidade de saudação toopublish dos serviços web de aprendizado de máquina do Azure como paga ou libere serviços para consumo por clientes externos.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-108">hello Azure Marketplace provides hello ability toopublish Azure Machine Learning web services as paid or free services for consumption by external customers.</span></span> <span data-ttu-id="eb5ff-109">Este artigo fornece uma visão geral do processo com links tooguidelines tooget que é iniciado.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-109">This article provides an overview of that process with links tooguidelines tooget you started.</span></span> <span data-ttu-id="eb5ff-110">Usando esse processo, você pode tornar seus serviços web disponíveis para outros desenvolvedores tooconsume em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-110">By using this process, you can make your web services available for other developers tooconsume in their applications.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview-of-hello-publishing-process"></a><span data-ttu-id="eb5ff-111">Visão geral do processo de publicação de saudação</span><span class="sxs-lookup"><span data-stu-id="eb5ff-111">Overview of hello publishing process</span></span>
<span data-ttu-id="eb5ff-112">Olá seguem etapas Olá para publicar um tooAzure de serviço web do aprendizado de máquina do Azure Marketplace:</span><span class="sxs-lookup"><span data-stu-id="eb5ff-112">hello following are hello steps for publishing an Azure Machine Learning web service tooAzure Marketplace:</span></span>

1. <span data-ttu-id="eb5ff-113">Criar e publicar um RRS (serviço de Solicitação-Resposta) do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="eb5ff-113">Create and publish a Machine Learning Request-Response service (RRS)</span></span>
2. <span data-ttu-id="eb5ff-114">Implantar Olá tooproduction de serviço e obter Olá informações de ponto de extremidade OData e chave de API.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-114">Deploy hello service tooproduction, and obtain hello API Key and OData endpoint information.</span></span>
3. <span data-ttu-id="eb5ff-115">URL de saudação de uso de saudação publicada toopublish de serviço web muito[Azure Marketplace (Data Market)](https://publish.windowsazure.com/workspace/)</span><span class="sxs-lookup"><span data-stu-id="eb5ff-115">Use hello URL of hello published web service toopublish too[Azure Marketplace (Data Market)](https://publish.windowsazure.com/workspace/)</span></span> 
4. <span data-ttu-id="eb5ff-116">Quando enviado, a sua oferta é analisada e precisa toobe aprovada antes dos clientes pode começar a compra-lo.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-116">Once submitted, your offer is reviewed and needs toobe approved before your customers can start purchasing it.</span></span> <span data-ttu-id="eb5ff-117">o processo de publicação Olá pode levar alguns dias.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-117">hello publishing process can take a few business days.</span></span> 

## <a name="walk-through"></a><span data-ttu-id="eb5ff-118">Passo a passo</span><span class="sxs-lookup"><span data-stu-id="eb5ff-118">Walk through</span></span>
### <a name="step-1-create-and-publish-a-machine-learning-request-response-service-rrs"></a><span data-ttu-id="eb5ff-119">Etapa 1: criar e publicar um RRS (serviço de Solicitação-Resposta) do Machine Learning</span><span class="sxs-lookup"><span data-stu-id="eb5ff-119">Step 1: Create and publish a Machine Learning Request-Response service (RRS)</span></span>
 <span data-ttu-id="eb5ff-120">Se você ainda não fez isso, consulte o [passo a passo](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="eb5ff-120">If you have not done this already, please take a look at this [walk through](machine-learning-walkthrough-5-publish-web-service.md).</span></span>

### <a name="step-2-deploy-hello-service-tooproduction-and-obtain-hello-api-key-and-odata-endpoint-information"></a><span data-ttu-id="eb5ff-121">Etapa 2: Implantar Olá tooproduction de serviço e obter Olá informações de ponto de extremidade OData e chave de API</span><span class="sxs-lookup"><span data-stu-id="eb5ff-121">Step 2: Deploy hello service tooproduction, and obtain hello API Key and OData endpoint information</span></span>
1. <span data-ttu-id="eb5ff-122">De saudação [Portal clássico do Azure](http://manage.windowsazure.com), selecione Olá **APRENDIZADO de máquina** opção da barra de navegação à esquerda do hello e selecione seu espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-122">From hello [Azure Classic Portal](http://manage.windowsazure.com), select hello **MACHINE LEARNING** option from hello left navigation bar, and select your workspace.</span></span> 
2. <span data-ttu-id="eb5ff-123">Clique em Olá **serviços WEB** guia e selecione Olá web serviço toopublish toohello marketplace.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-123">Click on hello **WEB SERVICES** tab, and select hello web service you would like toopublish toohello marketplace.</span></span>
   
    ![Azure Marketplace][workspace]
3. <span data-ttu-id="eb5ff-125">Selecione o ponto de extremidade de saudação você como toohave Olá marketplace consumiria.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-125">Select hello endpoint you would like toohave hello marketplace consume.</span></span> <span data-ttu-id="eb5ff-126">Se você não criou nenhum ponto de extremidade adicionais, você pode selecionar Olá **padrão** ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-126">If you have not created any additional endpoints, you can select hello **Default** endpoint.</span></span>
4. <span data-ttu-id="eb5ff-127">Depois de clicar no ponto de extremidade hello, será capaz de toosee Olá **chave API**.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-127">Once you have clicked on hello endpoint, you will be able toosee hello **API KEY**.</span></span> <span data-ttu-id="eb5ff-128">Você precisará dessa informação posteriormente na Etapa 3, então, faça uma cópia dela.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-128">You will need this piece of information later on in Step 3, so make a copy of it.</span></span>
   
    ![Azure Marketplace][apikey]
5. <span data-ttu-id="eb5ff-130">Clique em Olá **solicitação/resposta** toohello marketplace de serviços do método, neste momento, não há suporte para execução de lote de publicação.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-130">Click on hello **REQUEST/RESPONSE** method, at this point we do not support publishing batch execution services toohello marketplace.</span></span> <span data-ttu-id="eb5ff-131">Isso o levará toohello API a página de ajuda para o método de solicitação/resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-131">That will take you toohello API help page for hello Request/Response method.</span></span>
6. <span data-ttu-id="eb5ff-132">Saudação de cópia **endereço de ponto de extremidade OData**, você precisará dessas informações posteriormente na etapa 3.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-132">Copy hello **OData Endpoint Address**, you will need this information later on in Step 3.</span></span>
   
    ![Azure Marketplace][odata]

<span data-ttu-id="eb5ff-134">Implante o serviço de saudação em produção.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-134">deploy hello service into production.</span></span>

### <a name="step-3-use-hello-url-of-hello-published-web-service-toopublish-tooazure-marketplace-datamarket"></a><span data-ttu-id="eb5ff-135">Etapa 3: Use URL Olá Olá publicado web serviço toopublish tooAzure Marketplace (DataMarket)</span><span class="sxs-lookup"><span data-stu-id="eb5ff-135">Step 3: Use hello URL of hello published web service toopublish tooAzure Marketplace (DataMarket)</span></span>
1. <span data-ttu-id="eb5ff-136">Navegue muito[Azure Marketplace (Data Market)](http://datamarket.azure.com/home)</span><span class="sxs-lookup"><span data-stu-id="eb5ff-136">Navigate too[Azure Marketplace (Data Market)](http://datamarket.azure.com/home)</span></span> 
2. <span data-ttu-id="eb5ff-137">Clique em Olá **publicar** link na parte superior de saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-137">Click on hello **Publish** link at hello top of hello page.</span></span> <span data-ttu-id="eb5ff-138">Isso o levará toohello [Portal de publicação do Microsoft Azure](https://publish.windowsazure.com)</span><span class="sxs-lookup"><span data-stu-id="eb5ff-138">This will take you toohello [Microsoft Azure Publishing Portal](https://publish.windowsazure.com)</span></span>
3. <span data-ttu-id="eb5ff-139">Clique em Olá **editores** tooregister seção como um publicador.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-139">Click on hello **publishers** section tooregister as a publisher.</span></span>
4. <span data-ttu-id="eb5ff-140">Quando criar uma nova oferta, selecione **Serviços de Dados**, em seguida, clique em **Criar um novo serviço de dados**.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-140">When creating a new offer, select **Data Services**, then click **Create a New Data Service**.</span></span> 
   
   ![Azure Marketplace][image1]
   
   <br />
5. <span data-ttu-id="eb5ff-142">Em **Planos** , forneça informações sobre sua oferta, incluindo um plano de preços.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-142">Under **Plans** provide information on your offering, including a pricing plan.</span></span> <span data-ttu-id="eb5ff-143">Decida se você oferecerá um serviço gratuito ou pago.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-143">Decide if you will offer a free or paid service.</span></span> <span data-ttu-id="eb5ff-144">tooget pago, fornecer informações de pagamento, como as informações do banco e imposto.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-144">tooget paid, provide payment information such as your bank and tax information.</span></span>
6. <span data-ttu-id="eb5ff-145">Em **Marketing** fornecem informações sobre sua oferta, como título hello e uma descrição para sua oferta.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-145">Under **Marketing** provide information about your offer, such as hello title and description for your offer.</span></span>
7. <span data-ttu-id="eb5ff-146">Em **preços** você pode definir preços Olá para seus planos para países específicos ou permitir que o sistema hello "autoprice" sua oferta.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-146">Under **Pricing** you can set hello price for your plans for specific countries, or let hello system "autoprice" your offer.</span></span>
8. <span data-ttu-id="eb5ff-147">Em Olá **serviço de dados** , clique em **Web Service** como Olá **fonte de dados**.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-147">On hello **Data Service** tab, click **Web Service** as hello **Data Source**.</span></span>
   
    ![Azure Marketplace][image2]
9. <span data-ttu-id="eb5ff-149">Obter chave de API e a URL de serviço de web do hello de saudação Portal clássico do Azure, conforme explicado na etapa 2 acima.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-149">Get hello web service URL and API key from hello Azure Classic Portal, as explained in step 2 above.</span></span>
10. <span data-ttu-id="eb5ff-150">Na caixa de diálogo Instalação do serviço de dados do Marketplace hello, cole endereço de ponto de extremidade OData Olá Olá **URL do serviço** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-150">In hello Marketplace Data Service setup dialog box, paste hello OData endpoint address into hello **Service URL** text box.</span></span>
11. <span data-ttu-id="eb5ff-151">Para **autenticação**, escolha **cabeçalho** como Olá **esquema de autenticação**.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-151">For **Authentication**, choose **Header** as hello **Authentication Scheme**.</span></span>
    
    * <span data-ttu-id="eb5ff-152">Digite "Autorização" hello **nome de cabeçalho**.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-152">Enter "Authorization" for hello **Header Name**.</span></span>
    * <span data-ttu-id="eb5ff-153">Para Olá **o valor do cabeçalho**, digite "Portador" (sem aspas Olá), clique em Olá **espaço** barra e, em seguida, cole a chave de API de saudação.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-153">For hello **Header Value**, enter "Bearer" (without hello quotation marks), click hello **Space** bar, and then paste hello API key.</span></span>
    * <span data-ttu-id="eb5ff-154">Selecione Olá **este serviço é OData** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-154">Select hello **This Service is OData** check box.</span></span>
    * <span data-ttu-id="eb5ff-155">Clique em **Conexão de teste** tootest conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-155">Click **Test Connection** tootest hello connection.</span></span>
12. <span data-ttu-id="eb5ff-156">Em **Categorias**, verifique se **Machine Learning** está selecionado.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-156">Under **Categories**, ensure **Machine Learning** is selected.</span></span>
13. <span data-ttu-id="eb5ff-157">Quando você terminar de inserir todas Olá metadados sobre sua oferta, clique em **publicar**e, em seguida, **Push tooStaging**.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-157">When you are done entering all hello metadata about your offer, click on **Publish**, and then **Push tooStaging**.</span></span> <span data-ttu-id="eb5ff-158">Neste ponto, você será notificado de outros problemas que você precisa toofix.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-158">At this point, you will be notified of any remaining issues that you need toofix.</span></span>
14. <span data-ttu-id="eb5ff-159">Após ter assegurado conclusão de todos os problemas pendentes de saudação, clique em **solicitar aprovação toopush tooProduction**.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-159">After you have ensured completion of all hello outstanding issues, click on **Request approval toopush tooProduction**.</span></span> <span data-ttu-id="eb5ff-160">o processo de publicação Olá pode levar alguns dias.</span><span class="sxs-lookup"><span data-stu-id="eb5ff-160">hello publishing process can take a few business days.</span></span> 

[image1]:./media/machine-learning-publish-web-service-to-azure-marketplace/image1.png
[image2]:./media/machine-learning-publish-web-service-to-azure-marketplace/image2.png
[workspace]:./media/machine-learning-publish-web-service-to-azure-marketplace/selectworkspace.png
[apikey]:./media/machine-learning-publish-web-service-to-azure-marketplace/apikey.png
[odata]:./media/machine-learning-publish-web-service-to-azure-marketplace/odata.png

