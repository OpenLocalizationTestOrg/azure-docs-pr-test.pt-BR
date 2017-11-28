---
title: "parceiros de aaaCreate para mensagens entre empresas (B2B) - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Saiba como a integração de tooyour parceiros tooadd conta com hello pacote de integração de empresa e aplicativos lógicos"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: b179325c-a511-4c1b-9796-f7484b4f6873
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8dc70a8f441fcf228ed178029dcdbac940d794b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-update-partners-in-business-to-business-agreements-in-your-workflow"></a><span data-ttu-id="09f74-103">Adicionar ou atualizar parceiros em contratos B2B no seu fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="09f74-103">Add or update partners in business-to-business agreements in your workflow</span></span>

<span data-ttu-id="09f74-104">Os parceiros são as entidades que participam de mensagens e transações B2B (entre empresas).</span><span class="sxs-lookup"><span data-stu-id="09f74-104">Partners are entities that participate in business-to-business (B2B) transactions and exchange messages between each other.</span></span> <span data-ttu-id="09f74-105">Antes de criar os parceiros que representam você e a outra organização nessas transações, é necessário que ambas as partes compartilhem informações que identificam e validam as mensagens enviadas.</span><span class="sxs-lookup"><span data-stu-id="09f74-105">Before you can create partners that represent you and another organization in these transactions, you must both share information that identifies and validates messages sent by each other.</span></span> <span data-ttu-id="09f74-106">Depois de abordar esses detalhes e são toostart pronto sua relação de negócios, você pode criar parceiros em sua toorepresent de conta de integração que ambos.</span><span class="sxs-lookup"><span data-stu-id="09f74-106">After you discuss these details and are ready toostart your business relationship, you can create partners in your integration account toorepresent you both.</span></span>

## <a name="what-roles-do-partners-have-in-your-integration-account"></a><span data-ttu-id="09f74-107">Quais são as funções dos parceiros na conta de integração?</span><span class="sxs-lookup"><span data-stu-id="09f74-107">What roles do partners have in your integration account?</span></span>

<span data-ttu-id="09f74-108">toodefine detalhes sobre mensagens de saudação trocadas entre os parceiros, você cria acordos entre parceiros.</span><span class="sxs-lookup"><span data-stu-id="09f74-108">toodefine details about hello messages exchanged between partners, you create agreements between those partners.</span></span> <span data-ttu-id="09f74-109">No entanto, antes de criar um contrato, você deve ter adicionado contas de integração de tooyour pelo menos dois parceiros.</span><span class="sxs-lookup"><span data-stu-id="09f74-109">However, before you can create an agreement, you must have added at least two partners tooyour integration account.</span></span> <span data-ttu-id="09f74-110">Sua organização deve fazer parte do contrato de Olá Olá **parceiro host**.</span><span class="sxs-lookup"><span data-stu-id="09f74-110">Your organization must be part of hello agreement as hello **host partner**.</span></span> <span data-ttu-id="09f74-111">Olá outro parceiro ou **parceiro convidado** representa Olá organização que troca mensagens com sua organização.</span><span class="sxs-lookup"><span data-stu-id="09f74-111">hello other partner, or **guest partner** represents hello organization that exchanges messages with your organization.</span></span> <span data-ttu-id="09f74-112">parceiro de convidado Olá pode ser outra empresa, ou até mesmo um departamento em sua própria organização.</span><span class="sxs-lookup"><span data-stu-id="09f74-112">hello guest partner can be another company, or even a department in your own organization.</span></span>

<span data-ttu-id="09f74-113">Depois de adicionar esses parceiros, você pode criar um contrato.</span><span class="sxs-lookup"><span data-stu-id="09f74-113">After you add these partners, you can create an agreement.</span></span>

<span data-ttu-id="09f74-114">Receber e enviar as configurações são orientadas do hello ponto de vista do hello parceiro hospedado.</span><span class="sxs-lookup"><span data-stu-id="09f74-114">Receive and Send settings are oriented from hello point of view of hello Hosted Partner.</span></span> <span data-ttu-id="09f74-115">Por exemplo, Olá receber as configurações de um contrato de determinar como o parceiro Olá hospedado recebe as mensagens enviadas de um parceiro convidado.</span><span class="sxs-lookup"><span data-stu-id="09f74-115">For example, hello receive settings in an agreement determine how hello hosted partner receives messages sent from a guest partner.</span></span> <span data-ttu-id="09f74-116">Da mesma forma, as configurações de envio de saudação no contrato de saudação indicam como parceiro Olá hospedado envia o parceiro de convidado de toohello de mensagens.</span><span class="sxs-lookup"><span data-stu-id="09f74-116">Likewise, hello send settings on hello agreement indicate how hello hosted partner sends messages toohello guest partner.</span></span>

## <a name="how-toocreate-a-partner"></a><span data-ttu-id="09f74-117">Como um parceiro de toocreate?</span><span class="sxs-lookup"><span data-stu-id="09f74-117">How toocreate a partner?</span></span>

1. <span data-ttu-id="09f74-118">No portal do Azure de Olá, selecione **procurar**.</span><span class="sxs-lookup"><span data-stu-id="09f74-118">In hello Azure portal, select **Browse**.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="09f74-119">Na caixa de pesquisa do filtro hello, digite **integração**, em seguida, selecione **contas de integração** na lista de resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="09f74-119">In hello filter search box, enter **integration**, then select **Integration Accounts** in hello results list.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="09f74-120">Selecione onde você deseja tooadd seus parceiros de conta do hello integration.</span><span class="sxs-lookup"><span data-stu-id="09f74-120">Select hello integration account where you want tooadd your partners.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="09f74-121">Selecione Olá **parceiros** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="09f74-121">Select hello **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-1.png)

5. <span data-ttu-id="09f74-122">Na folha de parceiros hello, escolha **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="09f74-122">In hello Partners blade, choose **Add**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-2.png)

6. <span data-ttu-id="09f74-123">Insira um nome para seu parceiro e, em seguida, escolha um **Qualificador**.</span><span class="sxs-lookup"><span data-stu-id="09f74-123">Enter a name for your partner, then select a **Qualifier**.</span></span> <span data-ttu-id="09f74-124">Finalmente, insira um **valor** toohelp identificar documentos que entram em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="09f74-124">Finally, enter a **Value** toohelp identify documents that come into your apps.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-3.png)

7. <span data-ttu-id="09f74-125">progresso de saudação toosee para o processo de criação de parceiro, selecione Olá *bell* ícone de notificação.</span><span class="sxs-lookup"><span data-stu-id="09f74-125">toosee hello progress for your partner creation process, select hello *bell* notification icon.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-4.png)

8. <span data-ttu-id="09f74-126">tooconfirm seus parceiros novos foram com êxito adicionado, selecione Olá **parceiros** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="09f74-126">tooconfirm that your new partners were successfully added, select hello **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-5.png)

    <span data-ttu-id="09f74-127">Depois de selecionar o bloco de parceiros hello, você também verá parceiros recém-adicionado na folha de parceiros de saudação.</span><span class="sxs-lookup"><span data-stu-id="09f74-127">After you select hello Partners tile, you'll also see  newly added partners in hello Partners blade.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-6.png)

## <a name="how-tooedit-existing-partners-in-your-integration-account"></a><span data-ttu-id="09f74-128">Como parceiros de tooedit existente em sua conta de integração</span><span class="sxs-lookup"><span data-stu-id="09f74-128">How tooedit existing partners in your integration account</span></span>

1. <span data-ttu-id="09f74-129">Selecione Olá **parceiros** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="09f74-129">Select hello **Partners** tile.</span></span>
2. <span data-ttu-id="09f74-130">Depois de abre a folha de parceiros hello, selecione o parceiro de saudação deseja tooedit.</span><span class="sxs-lookup"><span data-stu-id="09f74-130">After hello Partners blade opens, select hello partner you want tooedit.</span></span>
3. <span data-ttu-id="09f74-131">Em Olá **atualização parceiro** lado a lado, faça as alterações.</span><span class="sxs-lookup"><span data-stu-id="09f74-131">On hello **Update Partner** tile, make your changes.</span></span>
4. <span data-ttu-id="09f74-132">Depois de terminar, escolha **salvar**, ou toocancel as alterações, selecione **descartar**.</span><span class="sxs-lookup"><span data-stu-id="09f74-132">After you're done, choose **Save**, or toocancel your changes, select **Discard**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/edit-1.png)

## <a name="how-toodelete-a-partner"></a><span data-ttu-id="09f74-133">Como toodelete um parceiro</span><span class="sxs-lookup"><span data-stu-id="09f74-133">How toodelete a partner</span></span>

1. <span data-ttu-id="09f74-134">Selecione Olá **parceiros** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="09f74-134">Select hello **Partners** tile.</span></span>
2. <span data-ttu-id="09f74-135">Depois de abre a folha de parceiro hello, selecione o parceiro de saudação que você deseja toodelete.</span><span class="sxs-lookup"><span data-stu-id="09f74-135">After hello Partner blade opens, select hello partner that you want toodelete.</span></span>
3. <span data-ttu-id="09f74-136">Clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="09f74-136">Choose **Delete**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/delete-1.png)

## <a name="next-steps"></a><span data-ttu-id="09f74-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="09f74-137">Next steps</span></span>
* [<span data-ttu-id="09f74-138">Saiba mais sobre os contratos</span><span class="sxs-lookup"><span data-stu-id="09f74-138">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Saiba mais sobre os contratos de integração corporativa")  

