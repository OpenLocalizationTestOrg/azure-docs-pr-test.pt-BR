---
title: Substituir o comportamento HTTP usando o mecanismo de regras da CDN do Azure | Microsoft Docs
description: "O mecanismo de regras permite que você personalize a forma como as solicitações HTTP são manipuladas pela CDN do Azure, como o bloqueio da entrega de certos tipos de conteúdo, definição de uma política de cache e modificação dos cabeçalhos HTTP."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 625a912b-91f2-485d-8991-128cc194ee71
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: abfe283476206b181018d187675b47112dc5ad2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="override-http-behavior-using-the-azure-cdn-rules-engine"></a><span data-ttu-id="a3d64-103">Substituir o comportamento HTTP usando o mecanismo de regras da CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="a3d64-103">Override HTTP behavior using the Azure CDN rules engine</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="a3d64-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="a3d64-104">Overview</span></span>
<span data-ttu-id="a3d64-105">O mecanismo de regras permite personalizar a forma como as solicitações HTTP são manipuladas, como o bloqueio de entrega de alguns tipos de conteúdo, definição de uma política de caching e modificação dos cabeçalhos HTTP.</span><span class="sxs-lookup"><span data-stu-id="a3d64-105">The rules engine allows you to customize how HTTP requests are handled, such as blocking the delivery of certain types of content, defining a caching policy, and modifying HTTP headers.</span></span>  <span data-ttu-id="a3d64-106">Este tutorial demonstrará a criação de uma regra que irá alterar o comportamento de caching dos ativos da CDN.</span><span class="sxs-lookup"><span data-stu-id="a3d64-106">This tutorial will demonstrate creating a rule that will change the caching behavior of CDN assets.</span></span>  <span data-ttu-id="a3d64-107">Também há conteúdo de vídeo disponível na seção "[Veja também](#see-also)".</span><span class="sxs-lookup"><span data-stu-id="a3d64-107">There's also video content available in the "[See also](#see-also)" section.</span></span>

   > [!TIP] 
   > <span data-ttu-id="a3d64-108">Para obter uma referência para a sintaxe em detalhes, consulte [Referência do Mecanismo de Regras](cdn-rules-engine-reference.md).</span><span class="sxs-lookup"><span data-stu-id="a3d64-108">For a reference to the syntax in detail, see [Rules Engine Reference](cdn-rules-engine-reference.md).</span></span>
   > 


## <a name="tutorial"></a><span data-ttu-id="a3d64-109">Tutorial</span><span class="sxs-lookup"><span data-stu-id="a3d64-109">Tutorial</span></span>
1. <span data-ttu-id="a3d64-110">Na folha do perfil CDN, clique no botão **Gerenciar** .</span><span class="sxs-lookup"><span data-stu-id="a3d64-110">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![botão gerenciar da folha Perfil CDN](./media/cdn-rules-engine/cdn-manage-btn.png)
   
    <span data-ttu-id="a3d64-112">O portal de gerenciamento da CDN é aberto.</span><span class="sxs-lookup"><span data-stu-id="a3d64-112">The CDN management portal opens.</span></span>
2. <span data-ttu-id="a3d64-113">Clique na guia **HTTP Grande**, seguida do **Mecanismo de Regras**.</span><span class="sxs-lookup"><span data-stu-id="a3d64-113">Click on the **HTTP Large** tab, followed by **Rules Engine**.</span></span>
   
    <span data-ttu-id="a3d64-114">São exibidas opções para uma nova regra.</span><span class="sxs-lookup"><span data-stu-id="a3d64-114">Options for a new rule are displayed.</span></span>
   
    ![Novas opções de regra CDN](./media/cdn-rules-engine/cdn-new-rule.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="a3d64-116">A ordem na qual são listadas várias regras afeta como elas são manipuladas.</span><span class="sxs-lookup"><span data-stu-id="a3d64-116">The order in which multiple rules are listed affects how they are handled.</span></span> <span data-ttu-id="a3d64-117">Uma regra subsequente poderá substituir as ações especificadas por uma regra anterior.</span><span class="sxs-lookup"><span data-stu-id="a3d64-117">A subsequent rule may override the actions specified by a previous rule.</span></span>
   > 
   > 
3. <span data-ttu-id="a3d64-118">Insira um nome na caixa de texto **Nome/Descrição** .</span><span class="sxs-lookup"><span data-stu-id="a3d64-118">Enter a name in the **Name / Description** textbox.</span></span>
4. <span data-ttu-id="a3d64-119">Identifique o tipo de solicitações às quais a regra será aplicada.</span><span class="sxs-lookup"><span data-stu-id="a3d64-119">Identify the type of requests the rule will apply to.</span></span>  <span data-ttu-id="a3d64-120">Por padrão, a condição de correspondência **Sempre** é selecionada.</span><span class="sxs-lookup"><span data-stu-id="a3d64-120">By default, the **Always** match condition is selected.</span></span>  <span data-ttu-id="a3d64-121">Você usará **Sempre** para este tutorial; portanto, deixe essa opção marcada.</span><span class="sxs-lookup"><span data-stu-id="a3d64-121">You'll use **Always** for this tutorial, so leave that selected.</span></span>
   
   ![Condição de correspondência CDN](./media/cdn-rules-engine/cdn-request-type.png)
   
   > [!TIP]
   > <span data-ttu-id="a3d64-123">Há vários tipos de condições de correspondência disponíveis no menu suspenso.</span><span class="sxs-lookup"><span data-stu-id="a3d64-123">There are many types of match conditions available in the dropdown.</span></span>  <span data-ttu-id="a3d64-124">Clicar no ícone de informação azul à esquerda da condição de correspondência explicará a condição atualmente selecionada em detalhes.</span><span class="sxs-lookup"><span data-stu-id="a3d64-124">Clicking on the blue informational icon to the left of the match condition will explain the currently selected condition in detail.</span></span>
   > 
   >  <span data-ttu-id="a3d64-125">Para obter a lista completa de expressões condicionais em detalhes, consulte [Expressões condicionais do Mecanismo de regras](cdn-rules-engine-reference-match-conditions.md).</span><span class="sxs-lookup"><span data-stu-id="a3d64-125">For the full list of conditional expressions in detail, see [Rules Engine Conditional Expressions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   >  
   > <span data-ttu-id="a3d64-126">Para obter a lista completa de condições de correspondência em detalhes, veja [Condições de correspondência do Mecanismo de regras](cdn-rules-engine-reference-match-conditions.md).</span><span class="sxs-lookup"><span data-stu-id="a3d64-126">For the full list of match conditions in detail, see [Rules Engine Match Conditions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   > 
   > 
5. <span data-ttu-id="a3d64-127">Clique no botão **+** próximo aos **Recursos** para adicionar um novo recurso.</span><span class="sxs-lookup"><span data-stu-id="a3d64-127">Click the **+** button next to **Features** to add a new feature.</span></span>  <span data-ttu-id="a3d64-128">Na lista suspensa à esquerda, selecione **Force Internal Max-Age**.</span><span class="sxs-lookup"><span data-stu-id="a3d64-128">In the dropdown on the left, select **Force Internal Max-Age**.</span></span>  <span data-ttu-id="a3d64-129">Na caixa de texto que aparece, digite **300**.</span><span class="sxs-lookup"><span data-stu-id="a3d64-129">In the textbox that appears, enter **300**.</span></span>  <span data-ttu-id="a3d64-130">Mantenha os valores padrão restantes.</span><span class="sxs-lookup"><span data-stu-id="a3d64-130">Leave the remaining default values.</span></span>
   
   ![Recurso CDN](./media/cdn-rules-engine/cdn-new-feature.png)
   
   > [!NOTE]
   > <span data-ttu-id="a3d64-132">Assim como ocorre com condições de correspondência, clicando no ícone de informação azul à esquerda do novo recurso para exibir detalhes sobre esse recurso.</span><span class="sxs-lookup"><span data-stu-id="a3d64-132">As with match conditions, clicking the blue informational icon to the left of the new feature will display details about this feature.</span></span>  <span data-ttu-id="a3d64-133">No caso de **Force Internal Max-Age**, estamos substituindo os cabeçalhos **Cache-Control** e **Expires** do ativo para controlar quando o nó de borda da CDN atualizará o ativo da origem.</span><span class="sxs-lookup"><span data-stu-id="a3d64-133">In the case of **Force Internal Max-Age**, we are overriding the asset's **Cache-Control** and **Expires** headers to control when the CDN edge node will refresh the asset from the origin.</span></span>  <span data-ttu-id="a3d64-134">Nosso exemplo de 300 segundos significa que o nó de borda da CDN armazenará em cache o ativo por 5 minutos antes de atualizar o ativo de sua origem.</span><span class="sxs-lookup"><span data-stu-id="a3d64-134">Our example of 300 seconds means the CDN edge node will cache the asset for 5 minutes before refreshing the asset from its origin.</span></span>
   > 
   > <span data-ttu-id="a3d64-135">Para obter a lista completa de recursos em detalhes, veja [Detalhes de recursos do Mecanismo de regras](cdn-rules-engine-reference-features.md).</span><span class="sxs-lookup"><span data-stu-id="a3d64-135">For the full list of features in detail, see [Rules Engine Feature Details](cdn-rules-engine-reference-features.md).</span></span>
   > 
   > 
6. <span data-ttu-id="a3d64-136">Clique no botão **Adicionar** para salvar a nova regra.</span><span class="sxs-lookup"><span data-stu-id="a3d64-136">Click the **Add** button to save the new rule.</span></span>  <span data-ttu-id="a3d64-137">A nova regra agora está aguardando aprovação.</span><span class="sxs-lookup"><span data-stu-id="a3d64-137">The new rule is now awaiting approval.</span></span> <span data-ttu-id="a3d64-138">Depois de aprovado, o status será alterado de **XML Pendente** para **XML Ativo**.</span><span class="sxs-lookup"><span data-stu-id="a3d64-138">Once it has been approved, the status will change from **Pending XML** to **Active XML**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="a3d64-139">Alterações de regras podem levar até 90 minutos para propagar por meio da CDN.</span><span class="sxs-lookup"><span data-stu-id="a3d64-139">Rules changes may take up to 90 minutes to propagate through the CDN.</span></span>
   > 
   > 

## <a name="see-also"></a><span data-ttu-id="a3d64-140">Consulte também</span><span class="sxs-lookup"><span data-stu-id="a3d64-140">See also</span></span>
* [<span data-ttu-id="a3d64-141">Visão geral da CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="a3d64-141">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="a3d64-142">Referência do Mecanismo de Regras</span><span class="sxs-lookup"><span data-stu-id="a3d64-142">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="a3d64-143">Condições de correspondência do Mecanismo de regras</span><span class="sxs-lookup"><span data-stu-id="a3d64-143">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="a3d64-144">Expressões condicionais do Mecanismo de regras</span><span class="sxs-lookup"><span data-stu-id="a3d64-144">Rules Engine Conditional Expressions</span></span>](cdn-rules-engine-reference-conditional-expressions.md)
* [<span data-ttu-id="a3d64-145">Recursos do Mecanismo de Regras</span><span class="sxs-lookup"><span data-stu-id="a3d64-145">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="a3d64-146">Substituindo o comportamento HTTP padrão usando o mecanismo de regras</span><span class="sxs-lookup"><span data-stu-id="a3d64-146">Overriding default HTTP behavior using the rules engine</span></span>](cdn-rules-engine.md)
* <span data-ttu-id="a3d64-147">[Azure Fridays: novos recursos Premium poderosos do Azure CDN](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (vídeo)</span><span class="sxs-lookup"><span data-stu-id="a3d64-147">[Azure Fridays: Azure CDN's powerful new Premium Features](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (video)</span></span>