---
title: "Testando sua oferta de modelo de solução para o Marketplace | Microsoft Docs"
description: "Saiba como testar a oferta do modelo de solução para o Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: ef8f9b5e-b98c-49f3-913f-cdf772c14c12
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/04/2015
ms.author: hascipio; v-divte
ms.openlocfilehash: da1fc4713fd1d832c7ba91226f72cbef63b241bc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="test-your-solution-template-offer-in-staging"></a><span data-ttu-id="1dfdb-103">Testar a oferta de modelo de solução em preparo</span><span class="sxs-lookup"><span data-stu-id="1dfdb-103">Test your solution template offer in staging</span></span>
<span data-ttu-id="1dfdb-104">Preparo significa implantar a sua oferta em uma "área restrita" privada, em que você poderá testar e verificar sua funcionalidade antes de publicá-la para produção.</span><span class="sxs-lookup"><span data-stu-id="1dfdb-104">Staging means deploying your offer in a private "sandbox" where you can test and verify its functionality before pushing it to production.</span></span> <span data-ttu-id="1dfdb-105">A oferta aparece em preparo como apareceria para um cliente que a tivesse implantado.</span><span class="sxs-lookup"><span data-stu-id="1dfdb-105">The offer appears in staging just as it would to a customer who has deployed it.</span></span> <span data-ttu-id="1dfdb-106">Sua oferta deve estar certificada para ser enviada por push para preparação.</span><span class="sxs-lookup"><span data-stu-id="1dfdb-106">Your offer must be certified to be pushed to staging.</span></span>

<span data-ttu-id="1dfdb-107">Depois que a oferta for preparada, você poderá exibir e testar a oferta no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1dfdb-107">After the offer is staged, you can view and test the offer in the [Azure Portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="1dfdb-108">Siga as etapas abaixo para enviar por push sua oferta de preparo e testá-la no [Portal do Azure](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="1dfdb-108">Follow the steps below to push your offer to staging and test it in the [Azure Portal](https://portal.azure.com/):</span></span>

1. <span data-ttu-id="1dfdb-109">Acesse o [Portal de Publicação](https://publish.windowsazure.com) > **guia Modelos de Solução** > sua oferta > **Publicar** > **Enviar por Push para Preparação**.</span><span class="sxs-lookup"><span data-stu-id="1dfdb-109">Go to the [Publishing Portal](https://publish.windowsazure.com) > **Solution Templates** tab > your offer > **Publish** > **Push to Staging**.</span></span>
2. <span data-ttu-id="1dfdb-110">Forneça a lista de assinaturas do Azure que você usará para visualizar e testar sua oferta.</span><span class="sxs-lookup"><span data-stu-id="1dfdb-110">Provide the list of Azure subscriptions that you will use to preview and test your offer.</span></span>
3. <span data-ttu-id="1dfdb-111">Entre no portal de visualização do Azure usando uma dos IDs de assinatura do Azure que você usou na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="1dfdb-111">Sign in to the Azure preview portal by using the subscription ID that you used in the previous step.</span></span>
4. <span data-ttu-id="1dfdb-112">Execute pelo menos uma rodada de testes no portal de visualização do Azure nos pontos mencionados a seguir:</span><span class="sxs-lookup"><span data-stu-id="1dfdb-112">Carry out at least one round of testing in the Azure preview portal on the points mentioned below:</span></span>
   * <span data-ttu-id="1dfdb-113">Certifique-se de que o conteúdo de marketing seja mostrado corretamente no Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="1dfdb-113">Make sure that marketing content shows up correctly in the Azure Marketplace.</span></span>
   * <span data-ttu-id="1dfdb-114">Implantação ponta a ponta da topologia.</span><span class="sxs-lookup"><span data-stu-id="1dfdb-114">End-to-end deployment of the topology.</span></span>
   * <span data-ttu-id="1dfdb-115">Execute testes de desempenho e testes de estresse.</span><span class="sxs-lookup"><span data-stu-id="1dfdb-115">Perform performance testing and stress testing.</span></span>
   * <span data-ttu-id="1dfdb-116">Certifique-se de que a sua topologia segue as práticas recomendadas.</span><span class="sxs-lookup"><span data-stu-id="1dfdb-116">Ensure that your topology adheres to the best practices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1dfdb-117">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1dfdb-117">Next steps</span></span>
<span data-ttu-id="1dfdb-118">Se você estiver satisfeito com os resultados, poderá prosseguir para a fase de publicação de oferta final, **Etapa 4**: [Implantando sua oferta no Marketplace](marketplace-publishing-push-to-production.md).</span><span class="sxs-lookup"><span data-stu-id="1dfdb-118">If you are satisfied with the results, then you can proceed to the final offer publishing phase, **Step 4**:  [Deploying your offer to the Marketplace](marketplace-publishing-push-to-production.md).</span></span> <span data-ttu-id="1dfdb-119">Caso contrário, faça alterações na oferta e solicite a certificação novamente.</span><span class="sxs-lookup"><span data-stu-id="1dfdb-119">Otherwise, make changes in your offer and request certification again.</span></span>

> [!NOTE]
> <span data-ttu-id="1dfdb-120">A certificação não é necessária para mudanças de conteúdo de marketing.</span><span class="sxs-lookup"><span data-stu-id="1dfdb-120">For marketing content changes, certification is not required.</span></span>
> 
> 

<span data-ttu-id="1dfdb-121">Confira [Introdução: como publicar uma oferta no Azure Marketplace](marketplace-publishing-getting-started.md) para obter um guia para todas as tarefas de editor.</span><span class="sxs-lookup"><span data-stu-id="1dfdb-121">See [Getting started: How to publish an offer to the Azure Marketplace](marketplace-publishing-getting-started.md) for a guide to all publisher tasks.</span></span>

