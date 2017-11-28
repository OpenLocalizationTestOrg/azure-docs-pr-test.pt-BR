---
title: "aaaPreview Office 365 grupos de expiração no Active Directory do Azure | Microsoft Docs"
description: "Como os grupos de tooset a expiração para o Office 365 no Active Directory do Azure (visualização)"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: it-pro
ms.openlocfilehash: a8c99961cff3aad3f4d8b0cc1b2eb8e8a4c9ba95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-office-365-groups-expiration-preview"></a><span data-ttu-id="cd185-103">Como configurar o vencimento de grupos do Office 365 (visualização)</span><span class="sxs-lookup"><span data-stu-id="cd185-103">Configure Office 365 groups expiration (preview)</span></span>

<span data-ttu-id="cd185-104">Agora você pode gerenciar o ciclo de vida de saudação de grupos do Office 365, definindo a validade de todos os grupos Office 365 que você selecionar.</span><span class="sxs-lookup"><span data-stu-id="cd185-104">You can now manage hello lifecycle of Office 365 groups by setting expiration for any Office 365 groups that you select.</span></span> <span data-ttu-id="cd185-105">Quando este expiração estiver definida, os proprietários desses grupos são frequentes toorenew seus grupos se eles ainda terão que grupos de saudação.</span><span class="sxs-lookup"><span data-stu-id="cd185-105">Once this expiration is set, owners of those groups are asked toorenew their groups if they still need hello groups.</span></span> <span data-ttu-id="cd185-106">Os grupos do Office 365 que não forem renovados, serão excluídos.</span><span class="sxs-lookup"><span data-stu-id="cd185-106">Any Office 365 group that is not renewed will be deleted.</span></span> <span data-ttu-id="cd185-107">Qualquer grupo que foi excluído do Office 365 pode ser restaurado dentro de 30 dias por proprietários do grupo de saudação ou administrador hello.</span><span class="sxs-lookup"><span data-stu-id="cd185-107">Any Office 365 group that was deleted can be restored within 30 days by hello group owners or hello administrator.</span></span>  


> [!NOTE]
> <span data-ttu-id="cd185-108">Você pode definir o vencimento de grupos somente do Office 365.</span><span class="sxs-lookup"><span data-stu-id="cd185-108">You can set expiration for only Office 365 groups.</span></span>
>
> <span data-ttu-id="cd185-109">Atribuir um vencimento para grupos do O365 requer que uma licença Premium do Azure AD esteja atribuída para:</span><span class="sxs-lookup"><span data-stu-id="cd185-109">Setting expiration for O365 groups requires that an Azure AD Premium license is assigned to</span></span>
>   - <span data-ttu-id="cd185-110">administrador de saudação que configura as configurações de expiração de saudação do locatário Olá</span><span class="sxs-lookup"><span data-stu-id="cd185-110">hello administrator who configures hello expiration settings for hello tenant</span></span>
>   - <span data-ttu-id="cd185-111">Todos os membros de grupos de saudação selecionados para esta configuração</span><span class="sxs-lookup"><span data-stu-id="cd185-111">All members of hello groups selected for this setting</span></span>

## <a name="set-office-365-groups-expiration"></a><span data-ttu-id="cd185-112">Como configurar o vencimento de grupos do Office 365</span><span class="sxs-lookup"><span data-stu-id="cd185-112">Set Office 365 groups expiration</span></span>

1. <span data-ttu-id="cd185-113">Olá abrir [Centro de administração do AD do Azure](https://aad.portal.azure.com) com uma conta que seja um administrador global no seu locatário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="cd185-113">Open hello [Azure AD admin center](https://aad.portal.azure.com) with an account that is a global administrator in your Azure AD tenant.</span></span>

2. <span data-ttu-id="cd185-114">Abra o Azure AD e selecione **Usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="cd185-114">Open Azure AD, select **Users and groups**.</span></span>

3. <span data-ttu-id="cd185-115">Selecione **configurações de grupo** e, em seguida, selecione **validade** tooopen as configurações de expiração de saudação.</span><span class="sxs-lookup"><span data-stu-id="cd185-115">Select **Group settings** and then select **Expiration** tooopen hello expiration settings.</span></span>
  
  ![Folha Vencimento](./media/active-directory-groups-lifecycle-azure-portal/expiration-settings.png)

4. <span data-ttu-id="cd185-117">Em Olá **validade** folha, você pode:</span><span class="sxs-lookup"><span data-stu-id="cd185-117">On hello **Expiration** blade, you can:</span></span>

  * <span data-ttu-id="cd185-118">Definir o tempo de vida de grupo Olá em dias.</span><span class="sxs-lookup"><span data-stu-id="cd185-118">Set hello group lifetime in days.</span></span> <span data-ttu-id="cd185-119">Você pode selecionar um dos Olá predefinição valores ou um valor personalizado (deve ser 31 dias ou mais).</span><span class="sxs-lookup"><span data-stu-id="cd185-119">You could select one of hello preset values, or a custom value (should be 31 days or more).</span></span> 
  * <span data-ttu-id="cd185-120">Especifique um endereço de email onde as notificações de expiração e renovação Olá devem ser enviadas quando um grupo não tem nenhum proprietário.</span><span class="sxs-lookup"><span data-stu-id="cd185-120">Specify an email address where hello renewal and expiration notifications should be sent when a group has no owner.</span></span> 
  * <span data-ttu-id="cd185-121">Selecione quais grupos do Office 365 expirarão.</span><span class="sxs-lookup"><span data-stu-id="cd185-121">Select which Office 365 groups expire.</span></span> <span data-ttu-id="cd185-122">Você pode habilitar a expiração para **todos os** grupos do Office 365, você pode selecionar entre grupos de saudação Office 365 ou selecionar **nenhum** para desabilitar a validade de todos os grupos.</span><span class="sxs-lookup"><span data-stu-id="cd185-122">You can enable expiration for **All** Office 365 groups, you can select from among hello Office 365 groups, or you select **None** to disable expiration for all groups.</span></span>
  * <span data-ttu-id="cd185-123">Salve as configurações quando terminar selecionando **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="cd185-123">Save your settings when you're done by selecting **Save**.</span></span>

<span data-ttu-id="cd185-124">Para obter instruções sobre como toodownload e instale Olá expiração de tooconfigure de módulo do Microsoft PowerShell para grupos do Office 365 por meio do PowerShell, consulte [Azure V2 PowerShell módulo do Active Directory - versão de visualização pública 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137).</span><span class="sxs-lookup"><span data-stu-id="cd185-124">For instructions on how toodownload and install hello Microsoft PowerShell module tooconfigure expiration for Office 365 groups via PowerShell, see [Azure Active Directory V2 PowerShell Module - Public Preview Release 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137).</span></span>

<span data-ttu-id="cd185-125">Notificações de email como esta são enviadas proprietários de grupo toohello Office 365 30 dias, 15 dias e tooexpiration anteriores de 1 dia do grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="cd185-125">Email notifications such as this one are sent toohello Office 365 group owners 30 days, 15 days, and 1 day prior tooexpiration of hello group.</span></span>

![Notificação de email de vencimento](./media/active-directory-groups-lifecycle-azure-portal/expiration-notification.png)

<span data-ttu-id="cd185-127">o proprietário do grupo Hello, em seguida, pode selecionar **renovar grupo** toorenew Olá grupo do Office 365, ou pode selecionar **vá toogroup** toosee membros de saudação e outros detalhes sobre Olá grupo.</span><span class="sxs-lookup"><span data-stu-id="cd185-127">hello group owner can then select **Renew group** toorenew hello Office 365 group, or can select **Go toogroup** toosee hello members and other details about hello group.</span></span>

<span data-ttu-id="cd185-128">Quando um grupo de expira, o grupo de saudação é excluído um dia após a data de expiração de saudação.</span><span class="sxs-lookup"><span data-stu-id="cd185-128">When a group expires, hello group is deleted one day after hello expiration date.</span></span> <span data-ttu-id="cd185-129">Uma notificação por email, como este é enviada proprietários do grupo toohello Office 365 informando sobre expiração hello e exclusão subsequente de seus grupos do Office 365.</span><span class="sxs-lookup"><span data-stu-id="cd185-129">An email notification such as this one is sent toohello Office 365 group owners informing them about hello expiration and subsequent deletion of their Office 365 group.</span></span>

![Notificação de email de exclusão do grupo](./media/active-directory-groups-lifecycle-azure-portal/deletion-notification.png)

<span data-ttu-id="cd185-131">Olá grupo pode ser restaurado selecionando **restauração grupo** ou usando cmdlets do PowerShell, conforme descrito em [restauração um Office 365 excluído o grupo no Active Directory do Azure] (https://docs.microsoft.com/azure/active-directory/ Active-Directory-Groups-Restore-Azure-portal).</span><span class="sxs-lookup"><span data-stu-id="cd185-131">hello group can be restored by selecting **Restore group** or by using PowerShell cmdlets, as described in [Restore a deleted Office 365 group in Azure Active Directory] (https://docs.microsoft.com/azure/active-directory/active-directory-groups-restore-azure-portal).</span></span>
    
<span data-ttu-id="cd185-132">Se você estiver restaurando de grupo de saudação contiver documentos, sites do SharePoint ou outros objetos persistentes, pode levar até too24 horas toofully restauração Olá grupo e seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="cd185-132">If hello group you're restoring contains documents, SharePoint sites, or other persistent objects, it might take up too24 hours toofully restore hello group and its contents.</span></span>

> [!NOTE]
> * <span data-ttu-id="cd185-133">Ao implantar as configurações de expiração hello, pode haver alguns grupos que são mais antigos que a janela de expiração de saudação.</span><span class="sxs-lookup"><span data-stu-id="cd185-133">When deploying hello expiration settings, there might be some groups that are older than hello expiration window.</span></span> <span data-ttu-id="cd185-134">Esses grupos não são ser imediatamente excluídos, mas são definir too30 dias até a expiração.</span><span class="sxs-lookup"><span data-stu-id="cd185-134">These groups are not be immediately deleted, but are set too30 days until expiration.</span></span> <span data-ttu-id="cd185-135">email de notificação de renovação primeiro Olá é enviado dentro de um dia.</span><span class="sxs-lookup"><span data-stu-id="cd185-135">hello first renewal notification email is sent out within a day.</span></span> <span data-ttu-id="cd185-136">Por exemplo, um grupo foi criado 400 dias atrás e intervalo de expiração de saudação é definido too180 dias.</span><span class="sxs-lookup"><span data-stu-id="cd185-136">For example, Group A was created 400 days ago, and hello expiration interval is set too180 days.</span></span> <span data-ttu-id="cd185-137">Quando você aplica as configurações de expiração, um grupo tem 30 dias antes de ser excluído, a menos que renova o proprietário de saudação.</span><span class="sxs-lookup"><span data-stu-id="cd185-137">When you apply expiration settings, Group A has 30 days before it is deleted, unless hello owner renews it.</span></span>
> * <span data-ttu-id="cd185-138">Quando um grupo dinâmico é excluído e restaurado, ele é visto como um novo grupo e regra de toohello acordo populado novamente.</span><span class="sxs-lookup"><span data-stu-id="cd185-138">When a dynamic group is deleted and restored, it is seen as a new group and re-populated according toohello rule.</span></span> <span data-ttu-id="cd185-139">Esse processo pode levar até too24 horas.</span><span class="sxs-lookup"><span data-stu-id="cd185-139">This process might take up too24 hours.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd185-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cd185-140">Next steps</span></span>
<span data-ttu-id="cd185-141">Esses artigos fornecem mais informações sobre os grupos do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cd185-141">These articles provide additional information on Azure AD groups.</span></span>

* [<span data-ttu-id="cd185-142">Consultar grupos existentes</span><span class="sxs-lookup"><span data-stu-id="cd185-142">See existing groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="cd185-143">Gerenciar configurações de um grupo</span><span class="sxs-lookup"><span data-stu-id="cd185-143">Manage settings of a group</span></span>](active-directory-groups-settings-azure-portal.md)
* [<span data-ttu-id="cd185-144">Gerenciar membros de um grupo</span><span class="sxs-lookup"><span data-stu-id="cd185-144">Manage members of a group</span></span>](active-directory-groups-members-azure-portal.md)
* [<span data-ttu-id="cd185-145">Gerenciar associações de um grupo</span><span class="sxs-lookup"><span data-stu-id="cd185-145">Manage memberships of a group</span></span>](active-directory-groups-membership-azure-portal.md)
* [<span data-ttu-id="cd185-146">Gerenciar regras dinâmicas para usuários em um grupo</span><span class="sxs-lookup"><span data-stu-id="cd185-146">Manage dynamic rules for users in a group</span></span>](active-directory-groups-dynamic-membership-azure-portal.md)
