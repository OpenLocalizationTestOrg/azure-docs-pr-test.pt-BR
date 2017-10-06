---
title: "aaaManage tooAzure de acesso usando funções de cobrança | Microsoft Docs"
description: 
services: 
documentationcenter: 
author: vikramdesai01
manager: vikdesai
editor: 
tags: billing
ms.assetid: e4c4d136-2826-4938-868f-a7e67ff6b025
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: vikdesai
ms.openlocfilehash: 5937fac5ffa5ca204eb03a1dcbc5e800b3d5eb74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-access-toobilling-information-for-azure-using-role-based-access-control"></a><span data-ttu-id="4d76e-102">Gerenciar informações de toobilling de acesso do Azure usando o controle de acesso baseado em função</span><span class="sxs-lookup"><span data-stu-id="4d76e-102">Manage access toobilling information for Azure using role-based access control</span></span>

<span data-ttu-id="4d76e-103">Você pode conceder acesso para o Azure toomembers de informações de cobrança da sua equipe, atribuindo uma saudação assinatura de tooyour de funções de usuário a seguir: conta de administrador, administrador de serviço, coadministrador, proprietário, colaborador, leitor e leitor de cobrança.</span><span class="sxs-lookup"><span data-stu-id="4d76e-103">You can grant access for Azure billing information toomembers of your team by assigning one of hello following user roles tooyour subscription: Account Administrator, Service Administrator, Co-administrator, Owner, Contributor, Reader, and Billing Reader.</span></span> <span data-ttu-id="4d76e-104">Eles teriam acesso toobilling informações Olá [portal do Azure](https://portal.azure.com/), e eles podem usar o hello [cobrança APIs](billing-usage-rate-card-overview.md) tooprogrammatically obter faturas (uma vez incluído-entrada) e detalhes de uso.</span><span class="sxs-lookup"><span data-stu-id="4d76e-104">They would have access toobilling information in hello [Azure portal](https://portal.azure.com/), and they can use hello [Billing APIs](billing-usage-rate-card-overview.md) tooprogrammatically get invoices (once opted-in) and usage details.</span></span> <span data-ttu-id="4d76e-105">Para obter mais informações sobre quem pode conceder funções e o que as funções podem fazer, consulte [funções no Azure RBAC](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="4d76e-105">For more information about who can grant roles, and which roles can do what, see [Roles in Azure RBAC](../active-directory/role-based-access-built-in-roles.md).</span></span>

## <span data-ttu-id="4d76e-106"><a name="opt-in"></a>Permitir que usuários adicionais tooaccess faturas</span><span class="sxs-lookup"><span data-stu-id="4d76e-106"><a name="opt-in"></a> Allowing additional users tooaccess invoices</span></span>

<span data-ttu-id="4d76e-107">Olá administrador da conta deve aceitar usando Olá [portal do Azure](https://portal.azure.com/) permitir acesso tooinvoices para outros usuários e por meio da API.</span><span class="sxs-lookup"><span data-stu-id="4d76e-107">hello Account Administrator must opt in using hello [Azure portal](https://portal.azure.com/) allow access tooinvoices for other users and via API.</span></span>

1. <span data-ttu-id="4d76e-108">Olá administrador da conta, selecione sua assinatura do hello [folha assinaturas](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4d76e-108">As hello Account Administrator, select your subscription from hello [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal.</span></span>

1. <span data-ttu-id="4d76e-109">Selecione **faturas** e **acessar tooinvoices**.</span><span class="sxs-lookup"><span data-stu-id="4d76e-109">Select **Invoices** and then **Access tooinvoices**.</span></span>

    ![Captura de tela mostra como toodelegate acessar tooinvoices](./media/billing-manage-access/AA-optin.png)

1. <span data-ttu-id="4d76e-111">Ativar **em** acesso Olá seguido por salvar as alterações do hello, tooallow usuários na assinatura funções com escopo toodownload fatura.</span><span class="sxs-lookup"><span data-stu-id="4d76e-111">Turn **On** hello access followed by saving hello changes, tooallow users in subscription scoped roles toodownload invoice.</span></span>

    ![Captura de tela mostra-off toodelegate tooinvoice de acesso](./media/billing-manage-access/AA-optinAllow.png)

<span data-ttu-id="4d76e-113">Aceitar permite administrador de serviço, coadministrador, proprietário, colaborador, leitor e de cobrança leitor Olá assinatura toodownload PDF as notas fiscais em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4d76e-113">Opting in allows Service Administrator, Co-administrator, Owner, Contributor, Reader, and Billing Reader on hello subscription toodownload PDF invoices in hello Azure portal.</span></span> <span data-ttu-id="4d76e-114">No entanto, faturas anteriores dezembro de 2016 são toohello disponível somente o administrador da conta agora.</span><span class="sxs-lookup"><span data-stu-id="4d76e-114">However, invoices older than December 2016 are available only toohello Account Administrator for now.</span></span>

<span data-ttu-id="4d76e-115">Olá administrador da conta também pode configurar toohave faturas enviadas por email.</span><span class="sxs-lookup"><span data-stu-id="4d76e-115">hello Account Administrator can also configure toohave invoices sent via email.</span></span> <span data-ttu-id="4d76e-116">mais, consulte toolearn [obter sua fatura no email](billing-download-azure-invoice-daily-usage-date.md).</span><span class="sxs-lookup"><span data-stu-id="4d76e-116">toolearn more, see [Get your invoice in email](billing-download-azure-invoice-daily-usage-date.md).</span></span>

## <a name="adding-users-toohello-billing-reader-role"></a><span data-ttu-id="4d76e-117">Adicionando a função de leitor de cobrança de toohello usuários</span><span class="sxs-lookup"><span data-stu-id="4d76e-117">Adding users toohello Billing Reader role</span></span>

<span data-ttu-id="4d76e-118">a função de leitor de cobrança Olá tem informações de cobrança toosubscription acesso somente leitura no portal do Azure e nenhum tooservices de acesso, como máquinas virtuais e contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="4d76e-118">hello Billing Reader role has read-only access toosubscription billing information in Azure portal, and no access tooservices such as VMs and storage accounts.</span></span> <span data-ttu-id="4d76e-119">Atribuir Olá toosomeone de função de leitor de cobrança que precisa acessar as informações de cobrança de assinatura toohello mas não Olá toomanage de capacidade do Azure services.</span><span class="sxs-lookup"><span data-stu-id="4d76e-119">Assign hello Billing Reader role toosomeone that needs access toohello subscription billing information but not hello ability toomanage Azure services.</span></span> <span data-ttu-id="4d76e-120">Essa função é apropriada para os usuários em uma organização que executam apenas gerenciamento de custos e financeiro de assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="4d76e-120">This role is appropriate for users in an organization who only perform financial and cost management for Azure subscriptions.</span></span>

1. <span data-ttu-id="4d76e-121">Selecione sua assinatura do hello [folha assinaturas](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4d76e-121">Select your subscription from hello [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal.</span></span>

1. <span data-ttu-id="4d76e-122">Selecione **Controle de acesso (IAM)** e, em seguida, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4d76e-122">Select **Access control (IAM)** and then click **Add**.</span></span>

    ![Captura de tela mostra IAM na folha da assinatura de saudação](./media/billing-manage-access/select-iam.PNG)

1. <span data-ttu-id="4d76e-124">Escolha **cobrança leitor** em Olá **selecionar uma função** página.</span><span class="sxs-lookup"><span data-stu-id="4d76e-124">Choose **Billing Reader** in hello **Select a role** page.</span></span>

    ![Captura de tela mostra o leitor de cobrança no modo de exibição de pop-up Olá](./media/billing-manage-access/select-roles.PNG)

1. <span data-ttu-id="4d76e-126">Digite o email Olá para usuário Olá você deseja tooinvite e clique **Okey** toosend convite de saudação.</span><span class="sxs-lookup"><span data-stu-id="4d76e-126">Type hello email for hello user you want tooinvite, then click **OK** toosend hello invitation.</span></span>

    ![Captura de tela que mostra tooenter email tooinvite alguém](./media/billing-manage-access/add-user.PNG)

1. <span data-ttu-id="4d76e-128">Siga as instruções em toolog de email de convite de saudação em como um leitor de cobrança.</span><span class="sxs-lookup"><span data-stu-id="4d76e-128">Follow instructions in hello invite email toolog in as a Billing Reader.</span></span>

    ![Captura de tela que mostra o que Olá leitor de cobrança pode ver no portal do Azure](./media/billing-manage-access/billing-reader-view.png)

> [!NOTE]
> <span data-ttu-id="4d76e-130">recurso de cobrança leitor Hello está em visualização e ainda não suporta as assinaturas do enterprise (EA) ou não global nuvens.</span><span class="sxs-lookup"><span data-stu-id="4d76e-130">hello Billing Reader feature is in preview, and does not yet support enterprise (EA) subscriptions or non-global clouds.</span></span>

## <a name="adding-users-tooother-roles"></a><span data-ttu-id="4d76e-131">Adicionando usuários tooother funções</span><span class="sxs-lookup"><span data-stu-id="4d76e-131">Adding users tooother roles</span></span>

<span data-ttu-id="4d76e-132">Outras funções, como o Proprietário ou Colaborador, os usuários podem acessar as informações de cobrança não apenas, mas também os serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="4d76e-132">Users in other roles, such as Owner or Contributor, can access not just billing information, but Azure services as well.</span></span> <span data-ttu-id="4d76e-133">Essas funções, consulte o toomanage [adicionar ou alterar funções de administrador do Azure que gerenciam a assinatura de saudação ou serviços](billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="4d76e-133">toomanage these roles, see [Add or change Azure administrator roles that manage hello subscription or services](billing-add-change-azure-subscription-administrator.md).</span></span>

## <a name="who-can-access-hello-account-centerhttpsaccountwindowsazurecom"></a><span data-ttu-id="4d76e-134">Quem pode acessar Olá [Centro de contas](https://account.windowsazure.com)?</span><span class="sxs-lookup"><span data-stu-id="4d76e-134">Who can access hello [Account Center](https://account.windowsazure.com)?</span></span>

<span data-ttu-id="4d76e-135">Olá administrador da conta pode fazer logon no Centro de contas toohello.</span><span class="sxs-lookup"><span data-stu-id="4d76e-135">Only hello Account Administrator can log in toohello Account center.</span></span> <span data-ttu-id="4d76e-136">Olá administrador da conta é proprietário legal Olá assinatura hello.</span><span class="sxs-lookup"><span data-stu-id="4d76e-136">hello Account Administrator is hello legal owner of hello subscription.</span></span> <span data-ttu-id="4d76e-137">Por padrão, Olá pessoa inscreveu ou comprou Olá assinatura do Azure é Olá administrador da conta, a menos que Olá [a propriedade de assinatura foi transferida](billing-subscription-transfer.md) toosomebody else.</span><span class="sxs-lookup"><span data-stu-id="4d76e-137">By default, hello person who signed up for or bought hello Azure subscription is hello Account Administrator, unless hello [subscription ownership was transferred](billing-subscription-transfer.md) toosomebody else.</span></span> <span data-ttu-id="4d76e-138">Olá administrador da conta pode criar assinaturas, cancelar assinaturas, alterar o endereço para cobrança Olá para uma assinatura e gerenciar políticas de acesso para a assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="4d76e-138">hello Account Administrator can create subscriptions, cancel subscriptions, change hello billing address for a subscription, and manage access policies for hello subscription.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="4d76e-139">Precisa de ajuda?</span><span class="sxs-lookup"><span data-stu-id="4d76e-139">Need help?</span></span> <span data-ttu-id="4d76e-140">Entre em contato com o suporte.</span><span class="sxs-lookup"><span data-stu-id="4d76e-140">Contact support.</span></span>

<span data-ttu-id="4d76e-141">Se você ainda tiver mais perguntas, [entre em contato com o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget seu problema resolvido rapidamente.</span><span class="sxs-lookup"><span data-stu-id="4d76e-141">If you still have further questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>
