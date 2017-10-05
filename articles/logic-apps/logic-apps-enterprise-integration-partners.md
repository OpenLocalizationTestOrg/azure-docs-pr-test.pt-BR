---
title: "Criar parceiros para mensagens B2B (entre empresas) — Aplicativos Lógicos do Azure"
description: "Saiba como adicionar parceiros à sua conta de integração com o Enterprise Integration Pack e os Aplicativos Lógicos"
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
ms.openlocfilehash: 950cb449b53f400f0f0f860caf5415bbb5212269
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="add-or-update-partners-in-business-to-business-agreements-in-your-workflow"></a><span data-ttu-id="48c1d-103">Adicionar ou atualizar parceiros em contratos B2B no seu fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="48c1d-103">Add or update partners in business-to-business agreements in your workflow</span></span>

<span data-ttu-id="48c1d-104">Os parceiros são as entidades que participam de mensagens e transações B2B (entre empresas).</span><span class="sxs-lookup"><span data-stu-id="48c1d-104">Partners are entities that participate in business-to-business (B2B) transactions and exchange messages between each other.</span></span> <span data-ttu-id="48c1d-105">Antes de criar os parceiros que representam você e a outra organização nessas transações, é necessário que ambas as partes compartilhem informações que identificam e validam as mensagens enviadas.</span><span class="sxs-lookup"><span data-stu-id="48c1d-105">Before you can create partners that represent you and another organization in these transactions, you must both share information that identifies and validates messages sent by each other.</span></span> <span data-ttu-id="48c1d-106">Após a discussão desses detalhes e o início da relação de negócios, é possível criar parceiros em sua conta de integração para representar as duas partes.</span><span class="sxs-lookup"><span data-stu-id="48c1d-106">After you discuss these details and are ready to start your business relationship, you can create partners in your integration account to represent you both.</span></span>

## <a name="what-roles-do-partners-have-in-your-integration-account"></a><span data-ttu-id="48c1d-107">Quais são as funções dos parceiros na conta de integração?</span><span class="sxs-lookup"><span data-stu-id="48c1d-107">What roles do partners have in your integration account?</span></span>

<span data-ttu-id="48c1d-108">Para definir os detalhes sobre as mensagens trocadas entre parceiros, crie contratos entre tais parceiros.</span><span class="sxs-lookup"><span data-stu-id="48c1d-108">To define details about the messages exchanged between partners, you create agreements between those partners.</span></span> <span data-ttu-id="48c1d-109">No entanto, antes de criar um contrato, é necessário adicionar pelo menos dois parceiros à sua conta de integração.</span><span class="sxs-lookup"><span data-stu-id="48c1d-109">However, before you can create an agreement, you must have added at least two partners to your integration account.</span></span> <span data-ttu-id="48c1d-110">Sua organização deve fazer parte do contrato como **parceiro do host**.</span><span class="sxs-lookup"><span data-stu-id="48c1d-110">Your organization must be part of the agreement as the **host partner**.</span></span> <span data-ttu-id="48c1d-111">O outro parceiro, ou **parceiro convidado**, representa a organização que troca mensagens com a sua empresa.</span><span class="sxs-lookup"><span data-stu-id="48c1d-111">The other partner, or **guest partner** represents the organization that exchanges messages with your organization.</span></span> <span data-ttu-id="48c1d-112">O parceiro convidado pode ser outra empresa ou até mesmo um departamento dentro da sua organização.</span><span class="sxs-lookup"><span data-stu-id="48c1d-112">The guest partner can be another company, or even a department in your own organization.</span></span>

<span data-ttu-id="48c1d-113">Depois de adicionar esses parceiros, você pode criar um contrato.</span><span class="sxs-lookup"><span data-stu-id="48c1d-113">After you add these partners, you can create an agreement.</span></span>

<span data-ttu-id="48c1d-114">As configurações de Recebimento e Envio são orientadas do ponto de vista do Parceiro host.</span><span class="sxs-lookup"><span data-stu-id="48c1d-114">Receive and Send settings are oriented from the point of view of the Hosted Partner.</span></span> <span data-ttu-id="48c1d-115">Por exemplo, as configurações de recebimento em um contrato determinam como o parceiro host recebe as mensagens enviadas de um parceiro convidado.</span><span class="sxs-lookup"><span data-stu-id="48c1d-115">For example, the receive settings in an agreement determine how the hosted partner receives messages sent from a guest partner.</span></span> <span data-ttu-id="48c1d-116">Da mesma forma, as configurações de envio no contrato indicam como o parceiro host envia mensagens ao parceiro convidado.</span><span class="sxs-lookup"><span data-stu-id="48c1d-116">Likewise, the send settings on the agreement indicate how the hosted partner sends messages to the guest partner.</span></span>

## <a name="how-to-create-a-partner"></a><span data-ttu-id="48c1d-117">Como criar um parceiro?</span><span class="sxs-lookup"><span data-stu-id="48c1d-117">How to create a partner?</span></span>

1. <span data-ttu-id="48c1d-118">No portal do Azure, selecione **Procurar**.</span><span class="sxs-lookup"><span data-stu-id="48c1d-118">In the Azure portal, select **Browse**.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="48c1d-119">Insira **integração** na caixa de pesquisa do filtro e, em seguida, selecione **Contas de Integração** na lista de resultados.</span><span class="sxs-lookup"><span data-stu-id="48c1d-119">In the filter search box, enter **integration**, then select **Integration Accounts** in the results list.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="48c1d-120">Escolha a conta de integração à qual você deseja adicionar parceiros.</span><span class="sxs-lookup"><span data-stu-id="48c1d-120">Select the integration account where you want to add your partners.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="48c1d-121">Escolha o bloco **Parceiros** .</span><span class="sxs-lookup"><span data-stu-id="48c1d-121">Select the **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-1.png)

5. <span data-ttu-id="48c1d-122">Na folha Parceiros, escolha **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="48c1d-122">In the Partners blade, choose **Add**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-2.png)

6. <span data-ttu-id="48c1d-123">Insira um nome para seu parceiro e, em seguida, escolha um **Qualificador**.</span><span class="sxs-lookup"><span data-stu-id="48c1d-123">Enter a name for your partner, then select a **Qualifier**.</span></span> <span data-ttu-id="48c1d-124">Por fim, insira um **Valor** para ajudar a identificar os documentos que entram em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="48c1d-124">Finally, enter a **Value** to help identify documents that come into your apps.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-3.png)

7. <span data-ttu-id="48c1d-125">Para ver o progresso do processo de criação do seu parceiro, selecione o ícone de notificação em forma de *sino*.</span><span class="sxs-lookup"><span data-stu-id="48c1d-125">To see the progress for your partner creation process, select the *bell* notification icon.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-4.png)

8. <span data-ttu-id="48c1d-126">Para confirmar que seus novos parceiros foram adicionados com êxito, selecione o bloco **Parceiros**.</span><span class="sxs-lookup"><span data-stu-id="48c1d-126">To confirm that your new partners were successfully added, select the **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-5.png)

    <span data-ttu-id="48c1d-127">Depois de selecionar o bloco Parceiros, você também verá os parceiros recém-adicionados na folha Parceiros.</span><span class="sxs-lookup"><span data-stu-id="48c1d-127">After you select the Partners tile, you'll also see  newly added partners in the Partners blade.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-6.png)

## <a name="how-to-edit-existing-partners-in-your-integration-account"></a><span data-ttu-id="48c1d-128">Como editar os parceiros existentes em sua conta de integração</span><span class="sxs-lookup"><span data-stu-id="48c1d-128">How to edit existing partners in your integration account</span></span>

1. <span data-ttu-id="48c1d-129">Escolha o bloco **Parceiros** .</span><span class="sxs-lookup"><span data-stu-id="48c1d-129">Select the **Partners** tile.</span></span>
2. <span data-ttu-id="48c1d-130">Após a folha Parceiros se abrir, selecione o parceiro que deseja editar.</span><span class="sxs-lookup"><span data-stu-id="48c1d-130">After the Partners blade opens, select the partner you want to edit.</span></span>
3. <span data-ttu-id="48c1d-131">No bloco **Atualizar Parceiro**, faça as alterações.</span><span class="sxs-lookup"><span data-stu-id="48c1d-131">On the **Update Partner** tile, make your changes.</span></span>
4. <span data-ttu-id="48c1d-132">Depois de terminar, escolha **Salvar** ou, para cancelar as alterações, selecione **Descartar**.</span><span class="sxs-lookup"><span data-stu-id="48c1d-132">After you're done, choose **Save**, or to cancel your changes, select **Discard**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/edit-1.png)

## <a name="how-to-delete-a-partner"></a><span data-ttu-id="48c1d-133">Como excluir um parceiro</span><span class="sxs-lookup"><span data-stu-id="48c1d-133">How to delete a partner</span></span>

1. <span data-ttu-id="48c1d-134">Escolha o bloco **Parceiros** .</span><span class="sxs-lookup"><span data-stu-id="48c1d-134">Select the **Partners** tile.</span></span>
2. <span data-ttu-id="48c1d-135">Após a folha Parceiros se abrir, selecione o parceiro que deseja excluir.</span><span class="sxs-lookup"><span data-stu-id="48c1d-135">After the Partner blade opens, select the partner that you want to delete.</span></span>
3. <span data-ttu-id="48c1d-136">Clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="48c1d-136">Choose **Delete**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/delete-1.png)

## <a name="next-steps"></a><span data-ttu-id="48c1d-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="48c1d-137">Next steps</span></span>
* [<span data-ttu-id="48c1d-138">Saiba mais sobre os contratos</span><span class="sxs-lookup"><span data-stu-id="48c1d-138">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Saiba mais sobre os contratos de integração corporativa")  

