---
title: "comportamento de aaaOverride HTTP usando o mecanismo de regras do Azure CDN Olá | Microsoft Docs"
description: "mecanismo de regras de saudação permite toocustomize como solicitações HTTP são manipuladas pelo CDN do Azure, como bloqueio de entrega de saudação de certos tipos de conteúdo, defina uma política de cache e modificar os cabeçalhos HTTP."
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
ms.openlocfilehash: dd7194be9dbda43180c64568d3e1f52c5c513a7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="override-http-behavior-using-hello-azure-cdn-rules-engine"></a><span data-ttu-id="78e42-103">Substituir o comportamento HTTP usando o mecanismo de regras do hello CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="78e42-103">Override HTTP behavior using hello Azure CDN rules engine</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="78e42-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="78e42-104">Overview</span></span>
<span data-ttu-id="78e42-105">mecanismo de regras de saudação permite toocustomize como solicitações HTTP são tratadas como bloqueio de entrega de saudação de certos tipos de conteúdo, definindo uma política de cache e modificar os cabeçalhos HTTP.</span><span class="sxs-lookup"><span data-stu-id="78e42-105">hello rules engine allows you toocustomize how HTTP requests are handled, such as blocking hello delivery of certain types of content, defining a caching policy, and modifying HTTP headers.</span></span>  <span data-ttu-id="78e42-106">Este tutorial demonstrará a criação de uma regra que irá alterar Olá comportamento de ativos CDN do cache.</span><span class="sxs-lookup"><span data-stu-id="78e42-106">This tutorial will demonstrate creating a rule that will change hello caching behavior of CDN assets.</span></span>  <span data-ttu-id="78e42-107">Também há conteúdo de vídeo disponíveis no hello "[Consulte também](#see-also)" seção.</span><span class="sxs-lookup"><span data-stu-id="78e42-107">There's also video content available in hello "[See also](#see-also)" section.</span></span>

   > [!TIP] 
   > <span data-ttu-id="78e42-108">Para obter a sintaxe de toohello uma referência em detalhes, consulte [referência do mecanismo de regras](cdn-rules-engine-reference.md).</span><span class="sxs-lookup"><span data-stu-id="78e42-108">For a reference toohello syntax in detail, see [Rules Engine Reference](cdn-rules-engine-reference.md).</span></span>
   > 


## <a name="tutorial"></a><span data-ttu-id="78e42-109">Tutorial</span><span class="sxs-lookup"><span data-stu-id="78e42-109">Tutorial</span></span>
1. <span data-ttu-id="78e42-110">Na folha de perfil CDN hello, clique em Olá **gerenciar** botão.</span><span class="sxs-lookup"><span data-stu-id="78e42-110">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![botão gerenciar da folha Perfil CDN](./media/cdn-rules-engine/cdn-manage-btn.png)
   
    <span data-ttu-id="78e42-112">portal de gerenciamento de CDN Olá é aberto.</span><span class="sxs-lookup"><span data-stu-id="78e42-112">hello CDN management portal opens.</span></span>
2. <span data-ttu-id="78e42-113">Clique em Olá **HTTP grande** guia, seguida por **mecanismo de regras**.</span><span class="sxs-lookup"><span data-stu-id="78e42-113">Click on hello **HTTP Large** tab, followed by **Rules Engine**.</span></span>
   
    <span data-ttu-id="78e42-114">São exibidas opções para uma nova regra.</span><span class="sxs-lookup"><span data-stu-id="78e42-114">Options for a new rule are displayed.</span></span>
   
    ![Novas opções de regra CDN](./media/cdn-rules-engine/cdn-new-rule.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="78e42-116">ordem de saudação na qual várias regras são listadas afeta como elas são manipuladas.</span><span class="sxs-lookup"><span data-stu-id="78e42-116">hello order in which multiple rules are listed affects how they are handled.</span></span> <span data-ttu-id="78e42-117">Uma regra subsequente pode substituir ações Olá especificadas por uma regra anterior.</span><span class="sxs-lookup"><span data-stu-id="78e42-117">A subsequent rule may override hello actions specified by a previous rule.</span></span>
   > 
   > 
3. <span data-ttu-id="78e42-118">Insira um nome no hello **nome / descrição** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="78e42-118">Enter a name in hello **Name / Description** textbox.</span></span>
4. <span data-ttu-id="78e42-119">Identificar o tipo de saudação de solicitações Olá regra será aplicada.</span><span class="sxs-lookup"><span data-stu-id="78e42-119">Identify hello type of requests hello rule will apply to.</span></span>  <span data-ttu-id="78e42-120">Por padrão, Olá **sempre** condição de correspondência está selecionada.</span><span class="sxs-lookup"><span data-stu-id="78e42-120">By default, hello **Always** match condition is selected.</span></span>  <span data-ttu-id="78e42-121">Você usará **Sempre** para este tutorial; portanto, deixe essa opção marcada.</span><span class="sxs-lookup"><span data-stu-id="78e42-121">You'll use **Always** for this tutorial, so leave that selected.</span></span>
   
   ![Condição de correspondência CDN](./media/cdn-rules-engine/cdn-request-type.png)
   
   > [!TIP]
   > <span data-ttu-id="78e42-123">Há muitos tipos de correspondência de condições disponíveis no menu suspenso de saudação.</span><span class="sxs-lookup"><span data-stu-id="78e42-123">There are many types of match conditions available in hello dropdown.</span></span>  <span data-ttu-id="78e42-124">Clicando em toohello de ícone informativo azul de saudação à esquerda da condição de correspondência Olá explicará condição Olá atualmente selecionado em detalhes.</span><span class="sxs-lookup"><span data-stu-id="78e42-124">Clicking on hello blue informational icon toohello left of hello match condition will explain hello currently selected condition in detail.</span></span>
   > 
   >  <span data-ttu-id="78e42-125">Para a lista completa de saudação de expressões condicionais em detalhes, consulte [expressões condicionais do mecanismo de regras](cdn-rules-engine-reference-match-conditions.md).</span><span class="sxs-lookup"><span data-stu-id="78e42-125">For hello full list of conditional expressions in detail, see [Rules Engine Conditional Expressions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   >  
   > <span data-ttu-id="78e42-126">Para Olá a lista completa das condições de correspondência em detalhes, consulte [corresponder a condições de mecanismo de regras](cdn-rules-engine-reference-match-conditions.md).</span><span class="sxs-lookup"><span data-stu-id="78e42-126">For hello full list of match conditions in detail, see [Rules Engine Match Conditions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   > 
   > 
5. <span data-ttu-id="78e42-127">Clique em Olá  **+**  botão Avançar muito**recursos** tooadd um novo recurso.</span><span class="sxs-lookup"><span data-stu-id="78e42-127">Click hello **+** button next too**Features** tooadd a new feature.</span></span>  <span data-ttu-id="78e42-128">No menu suspenso de Olá Olá esquerda, selecione **Force interno Max-Age**.</span><span class="sxs-lookup"><span data-stu-id="78e42-128">In hello dropdown on hello left, select **Force Internal Max-Age**.</span></span>  <span data-ttu-id="78e42-129">Na saudação de texto que aparece, digite **300**.</span><span class="sxs-lookup"><span data-stu-id="78e42-129">In hello textbox that appears, enter **300**.</span></span>  <span data-ttu-id="78e42-130">Deixe Olá restantes valores padrão.</span><span class="sxs-lookup"><span data-stu-id="78e42-130">Leave hello remaining default values.</span></span>
   
   ![Recurso CDN](./media/cdn-rules-engine/cdn-new-feature.png)
   
   > [!NOTE]
   > <span data-ttu-id="78e42-132">Como com condições de correspondência, clicando em toohello de ícone informativo Olá azul à esquerda do hello novo recurso exibirá detalhes sobre esse recurso.</span><span class="sxs-lookup"><span data-stu-id="78e42-132">As with match conditions, clicking hello blue informational icon toohello left of hello new feature will display details about this feature.</span></span>  <span data-ttu-id="78e42-133">No caso de saudação de **Force interno Max-Age**, substituindo o ativo de saudação **Cache-Control** e **Expires** cabeçalhos toocontrol ao nó de extremidade CDN Olá atualizará Olá ativo de origem hello.</span><span class="sxs-lookup"><span data-stu-id="78e42-133">In hello case of **Force Internal Max-Age**, we are overriding hello asset's **Cache-Control** and **Expires** headers toocontrol when hello CDN edge node will refresh hello asset from hello origin.</span></span>  <span data-ttu-id="78e42-134">Nosso exemplo de 300 segundos significa que o nó de borda do hello CDN armazenará em cache ativo Olá para 5 minutos antes de atualizar um ativo de saudação de sua origem.</span><span class="sxs-lookup"><span data-stu-id="78e42-134">Our example of 300 seconds means hello CDN edge node will cache hello asset for 5 minutes before refreshing hello asset from its origin.</span></span>
   > 
   > <span data-ttu-id="78e42-135">Para Olá a lista completa de recursos em detalhes, consulte [detalhes do recurso de mecanismo de regras](cdn-rules-engine-reference-features.md).</span><span class="sxs-lookup"><span data-stu-id="78e42-135">For hello full list of features in detail, see [Rules Engine Feature Details](cdn-rules-engine-reference-features.md).</span></span>
   > 
   > 
6. <span data-ttu-id="78e42-136">Clique em Olá **adicionar** nova regra de botão toosave hello.</span><span class="sxs-lookup"><span data-stu-id="78e42-136">Click hello **Add** button toosave hello new rule.</span></span>  <span data-ttu-id="78e42-137">nova regra de saudação agora está aguardando aprovação.</span><span class="sxs-lookup"><span data-stu-id="78e42-137">hello new rule is now awaiting approval.</span></span> <span data-ttu-id="78e42-138">Depois que ele tiver sido aprovado, o status de saudação será alterado de **XML pendente** muito**XML Active**.</span><span class="sxs-lookup"><span data-stu-id="78e42-138">Once it has been approved, hello status will change from **Pending XML** too**Active XML**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="78e42-139">Alterações de regras podem levar too90 minutos toopropagate por meio de saudação CDN.</span><span class="sxs-lookup"><span data-stu-id="78e42-139">Rules changes may take up too90 minutes toopropagate through hello CDN.</span></span>
   > 
   > 

## <a name="see-also"></a><span data-ttu-id="78e42-140">Consulte também</span><span class="sxs-lookup"><span data-stu-id="78e42-140">See also</span></span>
* [<span data-ttu-id="78e42-141">Visão geral da CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="78e42-141">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="78e42-142">Referência do Mecanismo de Regras</span><span class="sxs-lookup"><span data-stu-id="78e42-142">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="78e42-143">Condições de correspondência do Mecanismo de regras</span><span class="sxs-lookup"><span data-stu-id="78e42-143">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="78e42-144">Expressões condicionais do Mecanismo de regras</span><span class="sxs-lookup"><span data-stu-id="78e42-144">Rules Engine Conditional Expressions</span></span>](cdn-rules-engine-reference-conditional-expressions.md)
* [<span data-ttu-id="78e42-145">Recursos do Mecanismo de regras</span><span class="sxs-lookup"><span data-stu-id="78e42-145">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="78e42-146">Substituindo o comportamento HTTP padrão usando o mecanismo de regras de saudação</span><span class="sxs-lookup"><span data-stu-id="78e42-146">Overriding default HTTP behavior using hello rules engine</span></span>](cdn-rules-engine.md)
* <span data-ttu-id="78e42-147">[Azure Fridays: novos recursos Premium poderosos do Azure CDN](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (vídeo)</span><span class="sxs-lookup"><span data-stu-id="78e42-147">[Azure Fridays: Azure CDN's powerful new Premium Features](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (video)</span></span>