---
title: "Gerenciar o acesso a cobrança usando funções do Azure | Documentos do Microsoft"
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
ms.openlocfilehash: c70904097f139bc2178feed83f1cf1274f3c738d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-access-to-billing-information-for-azure-using-role-based-access-control"></a><span data-ttu-id="bebf6-102">Gerenciar o acesso a informações de cobrança do Azure usando o controle de acesso baseado em função</span><span class="sxs-lookup"><span data-stu-id="bebf6-102">Manage access to billing information for Azure using role-based access control</span></span>

<span data-ttu-id="bebf6-103">Você pode conceder acesso a informações de cobrança do Azure para membros da equipe atribuindo uma das seguintes funções de usuário para sua assinatura: Conta de Administrador, Administrador de serviço, Coadministrador, Proprietário, Colaborador, Leitor e Leitor de cobrança.</span><span class="sxs-lookup"><span data-stu-id="bebf6-103">You can grant access for Azure billing information to members of your team by assigning one of the following user roles to your subscription: Account Administrator, Service Administrator, Co-administrator, Owner, Contributor, Reader, and Billing Reader.</span></span> <span data-ttu-id="bebf6-104">Elas podem ter acesso a informações de cobrança no [portal do Azure](https://portal.azure.com/), e eles podem usar o [APIs de cobrança](billing-usage-rate-card-overview.md) para obter programaticamente os detalhes de uso e notas fiscais (uma vez decidido).</span><span class="sxs-lookup"><span data-stu-id="bebf6-104">They would have access to billing information in the [Azure portal](https://portal.azure.com/), and they can use the [Billing APIs](billing-usage-rate-card-overview.md) to programmatically get invoices (once opted-in) and usage details.</span></span> <span data-ttu-id="bebf6-105">Para obter mais informações sobre quem pode conceder funções e o que as funções podem fazer, consulte [funções no Azure RBAC](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="bebf6-105">For more information about who can grant roles, and which roles can do what, see [Roles in Azure RBAC](../active-directory/role-based-access-built-in-roles.md).</span></span>

## <span data-ttu-id="bebf6-106"><a name="opt-in"></a>Permitindo que usuários adicionais acessem notas fiscais</span><span class="sxs-lookup"><span data-stu-id="bebf6-106"><a name="opt-in"></a> Allowing additional users to access invoices</span></span>

<span data-ttu-id="bebf6-107">O Administrador da Conta deve aceitar usando o [portal do Azure](https://portal.azure.com/) permitir acesso às notas fiscais para outros usuários e por meio da API.</span><span class="sxs-lookup"><span data-stu-id="bebf6-107">The Account Administrator must opt in using the [Azure portal](https://portal.azure.com/) allow access to invoices for other users and via API.</span></span>

1. <span data-ttu-id="bebf6-108">Como Administrador da Conta, selecione sua assinatura da [folha Assinaturas](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bebf6-108">As the Account Administrator, select your subscription from the [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal.</span></span>

1. <span data-ttu-id="bebf6-109">Selecione **Faturas** e **Acesso às notas fiscais**.</span><span class="sxs-lookup"><span data-stu-id="bebf6-109">Select **Invoices** and then **Access to invoices**.</span></span>

    ![Captura de tela mostrando como delegar acesso a faturas](./media/billing-manage-access/AA-optin.png)

1. <span data-ttu-id="bebf6-111">**Ative** o acesso e, depois, salve as alterações para permitir que os usuários com funções que estão no escopo da assinatura baixem a fatura.</span><span class="sxs-lookup"><span data-stu-id="bebf6-111">Turn **On** the access followed by saving the changes, to allow users in subscription scoped roles to download invoice.</span></span>

    ![Captura de tela mostrando o comando liga/delsiga para delegar acesso a faturas](./media/billing-manage-access/AA-optinAllow.png)

<span data-ttu-id="bebf6-113">Aceitar permite que o Administrador de serviço, coadministrador, proprietário, colaborador, leitor e o leitor de cobrança da assinatura para fazer o download de notas fiscais PDF no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bebf6-113">Opting in allows Service Administrator, Co-administrator, Owner, Contributor, Reader, and Billing Reader on the subscription to download PDF invoices in the Azure portal.</span></span> <span data-ttu-id="bebf6-114">No entanto, faturas anteriores a dezembro de 2016 ficam disponíveis apenas para o Administrador de Conta por enquanto.</span><span class="sxs-lookup"><span data-stu-id="bebf6-114">However, invoices older than December 2016 are available only to the Account Administrator for now.</span></span>

<span data-ttu-id="bebf6-115">O Administrador de Conta também pode configurar para que as faturas sejam enviadas por e-mail.</span><span class="sxs-lookup"><span data-stu-id="bebf6-115">The Account Administrator can also configure to have invoices sent via email.</span></span> <span data-ttu-id="bebf6-116">Para obter mais informações, consulte [Obter sua fatura no e-mail](billing-download-azure-invoice-daily-usage-date.md).</span><span class="sxs-lookup"><span data-stu-id="bebf6-116">To learn more, see [Get your invoice in email](billing-download-azure-invoice-daily-usage-date.md).</span></span>

## <a name="adding-users-to-the-billing-reader-role"></a><span data-ttu-id="bebf6-117">Adicionar usuários à função de Leitor de cobrança</span><span class="sxs-lookup"><span data-stu-id="bebf6-117">Adding users to the Billing Reader role</span></span>

<span data-ttu-id="bebf6-118">A função de Leitor de cobrança tem acesso Somente leitura a informações de cobrança de assinatura no portal do Azure e nenhum acesso a serviços como VMs e contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="bebf6-118">The Billing Reader role has read-only access to subscription billing information in Azure portal, and no access to services such as VMs and storage accounts.</span></span> <span data-ttu-id="bebf6-119">Atribua a função de Leitor de Cobrança para alguém que precisa acessar as informações de cobrança da assinatura, mas não a capacidade de gerenciar os serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="bebf6-119">Assign the Billing Reader role to someone that needs access to the subscription billing information but not the ability to manage Azure services.</span></span> <span data-ttu-id="bebf6-120">Essa função é apropriada para os usuários em uma organização que executam apenas gerenciamento de custos e financeiro de assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="bebf6-120">This role is appropriate for users in an organization who only perform financial and cost management for Azure subscriptions.</span></span>

1. <span data-ttu-id="bebf6-121">Selecione sua assinatura na [folha de Assinaturas](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bebf6-121">Select your subscription from the [Subscriptions blade](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) in Azure portal.</span></span>

1. <span data-ttu-id="bebf6-122">Selecione **Controle de acesso (IAM)** e, em seguida, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="bebf6-122">Select **Access control (IAM)** and then click **Add**.</span></span>

    ![A captura de tela mostra IAM na folha da assinatura](./media/billing-manage-access/select-iam.PNG)

1. <span data-ttu-id="bebf6-124">Escolha **Leitor de cobrança** na página **Selecionar uma função**.</span><span class="sxs-lookup"><span data-stu-id="bebf6-124">Choose **Billing Reader** in the **Select a role** page.</span></span>

    ![A captura de tela mostra a o Leitor de Cobrança no modo de exibição pop-up](./media/billing-manage-access/select-roles.PNG)

1. <span data-ttu-id="bebf6-126">Digite o e-mail para o usuário que deseja convidar e, em seguida, clique em **OK** para enviar o convite.</span><span class="sxs-lookup"><span data-stu-id="bebf6-126">Type the email for the user you want to invite, then click **OK** to send the invitation.</span></span>

    ![A captura de tela que mostra inserir o e-mail para convidar alguém](./media/billing-manage-access/add-user.PNG)

1. <span data-ttu-id="bebf6-128">Siga as instruções no e-mail de convite para fazer logon como um Leitor de Cobrança.</span><span class="sxs-lookup"><span data-stu-id="bebf6-128">Follow instructions in the invite email to log in as a Billing Reader.</span></span>

    ![A captura de tela que mostra o que o Leitor de Cobrança pode ver no portal do Azure](./media/billing-manage-access/billing-reader-view.png)

> [!NOTE]
> <span data-ttu-id="bebf6-130">O recurso de Leitor de Cobrança está na visualização e ainda não da suporte às assinaturas enterprise (EA) ou nuvens não globais.</span><span class="sxs-lookup"><span data-stu-id="bebf6-130">The Billing Reader feature is in preview, and does not yet support enterprise (EA) subscriptions or non-global clouds.</span></span>

## <a name="adding-users-to-other-roles"></a><span data-ttu-id="bebf6-131">Adicionar usuários a outras funções</span><span class="sxs-lookup"><span data-stu-id="bebf6-131">Adding users to other roles</span></span>

<span data-ttu-id="bebf6-132">Outras funções, como o Proprietário ou Colaborador, os usuários podem acessar as informações de cobrança não apenas, mas também os serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="bebf6-132">Users in other roles, such as Owner or Contributor, can access not just billing information, but Azure services as well.</span></span> <span data-ttu-id="bebf6-133">Para gerenciar essas funções, consulte [Adicionar ou alterar as funções de administrador do Azure que gerenciam a assinatura ou serviços](billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="bebf6-133">To manage these roles, see [Add or change Azure administrator roles that manage the subscription or services](billing-add-change-azure-subscription-administrator.md).</span></span>

## <a name="who-can-access-the-account-centerhttpsaccountwindowsazurecom"></a><span data-ttu-id="bebf6-134">Quem pode acessar o [Centro de contas](https://account.windowsazure.com)?</span><span class="sxs-lookup"><span data-stu-id="bebf6-134">Who can access the [Account Center](https://account.windowsazure.com)?</span></span>

<span data-ttu-id="bebf6-135">Somente o Administrador da Conta pode acessar o Centro de Contas do Azure.</span><span class="sxs-lookup"><span data-stu-id="bebf6-135">Only the Account Administrator can log in to the Account center.</span></span> <span data-ttu-id="bebf6-136">O Administrador da conta é o proprietário legal da assinatura.</span><span class="sxs-lookup"><span data-stu-id="bebf6-136">The Account Administrator is the legal owner of the subscription.</span></span> <span data-ttu-id="bebf6-137">Por padrão, a pessoa que assinou ou comprou a assinatura do Azure é o Administrador da Conta, a menos que [a propriedade de assinatura foi transferida](billing-subscription-transfer.md) para outra pessoa.</span><span class="sxs-lookup"><span data-stu-id="bebf6-137">By default, the person who signed up for or bought the Azure subscription is the Account Administrator, unless the [subscription ownership was transferred](billing-subscription-transfer.md) to somebody else.</span></span> <span data-ttu-id="bebf6-138">O Administrador da Conta pode criar assinaturas, cancelar inscrições, alterar o endereço de cobrança para uma assinatura e gerenciar políticas de acesso para a assinatura.</span><span class="sxs-lookup"><span data-stu-id="bebf6-138">The Account Administrator can create subscriptions, cancel subscriptions, change the billing address for a subscription, and manage access policies for the subscription.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="bebf6-139">Precisa de ajuda?</span><span class="sxs-lookup"><span data-stu-id="bebf6-139">Need help?</span></span> <span data-ttu-id="bebf6-140">Entre em contato com o suporte.</span><span class="sxs-lookup"><span data-stu-id="bebf6-140">Contact support.</span></span>

<span data-ttu-id="bebf6-141">Se ainda tiver dúvidas, [entre em contato com o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) para resolver seu problema rapidamente.</span><span class="sxs-lookup"><span data-stu-id="bebf6-141">If you still have further questions, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>
