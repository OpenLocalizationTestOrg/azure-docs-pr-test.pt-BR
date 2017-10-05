---
title: "Usar um locatário do Office 365 com uma assinatura do Azure | Microsoft Docs"
description: "Saiba como adicionar um diretório do Office 365 (locatário) a uma assinatura do Azure."
services: 
documentationcenter: 
author: JiangChen79
manager: jlian
editor: 
tags: billing,top-support-issue
ms.assetid: cc9c57c6-7bfd-4dea-9027-c75ef3737589
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: cjiang
ms.openlocfilehash: 7affb4a83cdb8ababef60e786a3c824e7477ed68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="associate-an-office-365-tenant-to-an-azure-subscription"></a><span data-ttu-id="76098-103">Associar um locatário do Office 365 a uma assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="76098-103">Associate an Office 365 tenant to an Azure subscription</span></span>
<span data-ttu-id="76098-104">Vincule suas assinaturas do Azure e o Office 365 separadas para que possam acessar o locatário do Office 365 da sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="76098-104">Link your separate Azure and Office 365 subscriptions so that you can access the Office 365 tenant from your Azure subscription.</span></span> <span data-ttu-id="76098-105">Para vincular suas assinaturas, entre no Azure com a conta de administrador de serviços do Azure, adicione um diretório e adicione as contas organizacionais do Office 365 para o locatário do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="76098-105">To link your subscriptions, sign in to Azure with the Azure service administrator account, add a directory, and add the Office 365 organizational accounts to the Azure Active Directory tenant.</span></span>

<span data-ttu-id="76098-106">Se você quiser uma assinatura do Office 365 para usuários na sua instância do Azure Active Directory ou você tiver uma conta do Office 365, mas não uma conta do Azure, consulte [Inscrever-se no Azure com uma conta do Office 365](billing-use-existing-office-365-account-azure-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="76098-106">If you want an Office 365 subscription for users in your Azure Active Directory instance or you have an Office 365 account but not an Azure account, see [Sign up for Azure with Office 365 account](billing-use-existing-office-365-account-azure-subscription.md).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="76098-107">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="76098-107">Before you begin</span></span>
* <span data-ttu-id="76098-108">Você deve ter as credenciais do administrador de serviços de assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="76098-108">You must have the credentials of the Azure subscription service administrator.</span></span> <span data-ttu-id="76098-109">Contas de coadministrador não podem realizar algumas das etapas neste artigo.</span><span class="sxs-lookup"><span data-stu-id="76098-109">Co-administrator accounts can't do some of the steps in this article.</span></span> <span data-ttu-id="76098-110">Para alterar o administrador do serviço, veja [Como adicionar ou alterar funções de administrador do Azure](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).</span><span class="sxs-lookup"><span data-stu-id="76098-110">To change your service administrator, see [How to add or change Azure administrator roles](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).</span></span>
* <span data-ttu-id="76098-111">Você deve ter as credenciais de um administrador global do locatário do Office 365.</span><span class="sxs-lookup"><span data-stu-id="76098-111">You must have the credentials of a global administrator of the Office 365 tenant.</span></span>
* <span data-ttu-id="76098-112">O endereço de email do administrador de serviços não deve estar no locatário do Office 365.</span><span class="sxs-lookup"><span data-stu-id="76098-112">The email address of the service administrator must not be in the Office 365 tenant.</span></span>
* <span data-ttu-id="76098-113">O endereço de email do administrador do serviço não deve ser igual ao do administrador global do locatário do Office 365.</span><span class="sxs-lookup"><span data-stu-id="76098-113">The email address of the service administrator must not match that of any global administrator of the Office 365 tenant.</span></span>
* <span data-ttu-id="76098-114">Se você usar um endereço de email que é uma conta da Microsoft e uma conta organizacional, altere temporariamente o administrador de serviços de sua assinatura do Azure para usar outra conta da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="76098-114">If you use an email address that is both a Microsoft account and an organizational account, temporarily change the service administrator of your Azure subscription to use another Microsoft account.</span></span> <span data-ttu-id="76098-115">Você pode criar uma nova conta da Microsoft na [Página de inscrição de conta da Microsoft](https://signup.live.com/).</span><span class="sxs-lookup"><span data-stu-id="76098-115">You can create a Microsoft account at the [Microsoft account signup page](https://signup.live.com/).</span></span>

## <a name="link-office-365-tenant-to-azure-subscription"></a><span data-ttu-id="76098-116">Vincular o locatário do Office 365 à assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="76098-116">Link Office 365 tenant to Azure subscription</span></span>
<span data-ttu-id="76098-117">Para associar o locatário do Office 365 à assinatura do Azure, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="76098-117">To associate the Office 365 tenant to the Azure subscription, follow these steps:</span></span>

### <a name="step-1-add-office-365-tenant-to-your-azure-subscription"></a><span data-ttu-id="76098-118">Etapa 1: adicionar o locatário do Office 365 à assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="76098-118">Step 1: Add Office 365 tenant to your Azure subscription</span></span>

1. <span data-ttu-id="76098-119">Entre no [Portal clássico do Azure](https://manage.windowsazure.com/) com as credenciais de administrador do serviço.</span><span class="sxs-lookup"><span data-stu-id="76098-119">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) with the service administrator credentials.</span></span>

    ![Captura de tela de entrada do Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)

2. <span data-ttu-id="76098-121">No painel esquerdo, selecione **ACTIVE DIRECTORY**.</span><span class="sxs-lookup"><span data-stu-id="76098-121">In the left pane, select **ACTIVE DIRECTORY**.</span></span> <span data-ttu-id="76098-122">Você não deverá ver o locatário do Office 365.</span><span class="sxs-lookup"><span data-stu-id="76098-122">You shouldn't see the Office 365 tenant.</span></span> <span data-ttu-id="76098-123">Se isso acontecer, pule para a [Etapa 2: Alterar o diretório associado à assinatura do Azure](#Step2).</span><span class="sxs-lookup"><span data-stu-id="76098-123">If you see it, skip to [Step 2: Change the directory associated with the Azure subscription](#Step2).</span></span>
   
   ![Captura de tela da entrada do Active Directory](./media/billing-add-office-365-tenant-to-azure-subscription/s35-classic-portal-active-directory-entry.png)

3. <span data-ttu-id="76098-125">Selecione **NOVO** > **DIRETÓRIO** > **CRIAÇÃO PERSONALIZADA**.</span><span class="sxs-lookup"><span data-stu-id="76098-125">Select **NEW** > **DIRECTORY** > **CUSTOM CREATE**.</span></span>
   
    ![Captura de tela da criação personalizada do Azure Active Directory](./media/billing-add-office-365-tenant-to-azure-subscription/s37-aad-custom-create.png)
   
4. <span data-ttu-id="76098-127">Na página **Adicionar diretório** em **DIRETÓRIO**, selecione **Usar diretório existente**.</span><span class="sxs-lookup"><span data-stu-id="76098-127">On the **Add directory** page, under **DIRECTORY**, select **Use existing directory**.</span></span> <span data-ttu-id="76098-128">Em seguida, selecione **estou pronto para sair agora** e selecione **Concluir** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="76098-128">Then select **I am ready to be signed out now**, and select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>
   
    ![Captura de tela de "Usar diretório existente"](./media/billing-add-office-365-tenant-to-azure-subscription/s39_add-directory-use-existing.png)
   
5. <span data-ttu-id="76098-130">Depois de sair, entre com as credenciais do administrador global do seu locatário do Office 365.</span><span class="sxs-lookup"><span data-stu-id="76098-130">After you are signed out, sign in with the global administrator’s credentials of your Office 365 tenant.</span></span>
   
    ![Captura de tela de entrada no administrador global do Office 365](./media/billing-add-office-365-tenant-to-azure-subscription/s310_sign-in-global-admin-office-365.png)
   
6. <span data-ttu-id="76098-132">Selecione **Continuar**.</span><span class="sxs-lookup"><span data-stu-id="76098-132">Select **Continue**.</span></span>
   
    ![Captura de tela de verificação](./media/billing-add-office-365-tenant-to-azure-subscription/s311_use-contoso-directory-azure-verify.png)
   
7. <span data-ttu-id="76098-134">Selecione **Sair agora**.</span><span class="sxs-lookup"><span data-stu-id="76098-134">Select **Sign out now**.</span></span>
   
    ![Captura de tela de saída](./media/billing-add-office-365-tenant-to-azure-subscription/s312_use-contoso-directory-azure-confirm-and-sign-out.png)
   
8. <span data-ttu-id="76098-136">Entre no [Portal clássico do Azure](https://manage.windowsazure.com/) com as credenciais de administrador do serviço.</span><span class="sxs-lookup"><span data-stu-id="76098-136">Sign in to the [Azure classic portal](https://manage.windowsazure.com/) with the service administrator credentials.</span></span>
   
    ![Captura de tela de entrada do Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)
   
9. <span data-ttu-id="76098-138">Você deverá ver seu locatário do Office 365 no painel de controle.</span><span class="sxs-lookup"><span data-stu-id="76098-138">You should see your Office 365 tenant in the dashboard.</span></span>
   
    ![Captura de tela do painel](./media/billing-add-office-365-tenant-to-azure-subscription/s314_office-365-tenant-appear-in-azure.png)

### <span data-ttu-id="76098-140"><a name="Step2"></a>Etapa 2: alterar o diretório associado à assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="76098-140"><a name="Step2"></a>Step 2: Change the directory associated with the Azure subscription</span></span>
   
1. <span data-ttu-id="76098-141">Escolha a opção **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="76098-141">Select **Settings**.</span></span>
   
    ![Captura de tela do ícone de configurações do Portal Clássico do Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s315_azure-classic-portal-settings-icon.png)
   
2. <span data-ttu-id="76098-143">Selecione sua assinatura do Azure e selecione **EDITAR DIRETÓRIO**.</span><span class="sxs-lookup"><span data-stu-id="76098-143">Select your Azure subscription, and then select **EDIT DIRECTORY**.</span></span>

    ![Captura de tela do diretório de edição de assinatura do Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s316_azure-subscription-edit-directory.png)
   
3. <span data-ttu-id="76098-145">Selecione **Avançar** ![ícone Avançar](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).</span><span class="sxs-lookup"><span data-stu-id="76098-145">Select **Next** ![Next icon](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).</span></span>
   
    ![Captura de tela de "Alterar o diretório associado"](./media/billing-add-office-365-tenant-to-azure-subscription/s318_azure-change-associated-directory.png)
   
4. <span data-ttu-id="76098-147">Examine as contas afetadas.</span><span class="sxs-lookup"><span data-stu-id="76098-147">Review the affected accounts.</span></span> <span data-ttu-id="76098-148">Todos os coadministradores e usuários de [RBAC (Controle de Acesso Baseado em Função)](../active-directory/role-based-access-control-configure.md) com acesso Atribuído nos grupos de recursos existentes são removidos.</span><span class="sxs-lookup"><span data-stu-id="76098-148">All co-administrators and [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) users with assigned access in the existing resource groups are removed.</span></span> <span data-ttu-id="76098-149">O aviso que você recebe menciona apenas a remoção dos coadministradores.</span><span class="sxs-lookup"><span data-stu-id="76098-149">The warning you receive only mentions the removal of co-administrators.</span></span>
      
    ![Captura de tela que mostra as contas de coadministrador a serem removidas.](./media/billing-add-office-365-tenant-to-azure-subscription/s322_azure-confirm-directory-mapping.png)
   
    ![Captura de tela que mostra um exemplo de conta de usuário a ser removida.](./media/billing-add-office-365-tenant-to-azure-subscription/s325_assigned-users-removed-resource-groups.png)
   
5. <span data-ttu-id="76098-152">Selecione **Concluir** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="76098-152">Select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>

### <a name="step-3-add-your-office-365-organizational-accounts-as-co-administrators-to-the-azure-active-directory-tenant"></a><span data-ttu-id="76098-153">Etapa 3: adicionar as contas organizacionais do Office 365 como coadministradores ao locatário do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="76098-153">Step 3: Add your Office 365 organizational accounts as co-administrators to the Azure Active Directory tenant</span></span>
   
1. <span data-ttu-id="76098-154">Selecione a guia **ADMINISTRADORES** e, em seguida, selecione **ADICIONAR**.</span><span class="sxs-lookup"><span data-stu-id="76098-154">Select the **ADMINISTRATORS** tab, and then select **ADD**.</span></span>
   
    ![Captura de tela da guia de administradores de configurações do Portal Clássico do Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s319_azure-classic-portal-settings-administrators.png)
   
2. <span data-ttu-id="76098-156">Insira uma conta organizacional de seu locatário do Office 365, clique para selecionar a assinatura do Azure e, em seguida, clique em **Concluir** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="76098-156">Enter an organizational account of your Office 365 tenant, select the Azure subscription, and then select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>
   
    ![Captura de tela de caixa de diálogo de adicionar coadministrador ao Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s320_azure-add-co-administrator.png)
   
3. <span data-ttu-id="76098-158">Volte para a guia **ADMINISTRADORES**.</span><span class="sxs-lookup"><span data-stu-id="76098-158">Go back to the **ADMINISTRATORS** tab.</span></span> <span data-ttu-id="76098-159">Você deverá ver a conta organizacional exibida como coadministrador.</span><span class="sxs-lookup"><span data-stu-id="76098-159">You should see the organizational account displayed as co-administrator.</span></span>
   
    ![Captura de tela da guia administradores](./media/billing-add-office-365-tenant-to-azure-subscription/s321_azure-co-administrator-added.png)
4.  <span data-ttu-id="76098-161">Teste o acesso ao Azure com a conta de coadministrador.</span><span class="sxs-lookup"><span data-stu-id="76098-161">Test access to Azure with the co-administrator account.</span></span>
   
    <span data-ttu-id="76098-162">a.</span><span class="sxs-lookup"><span data-stu-id="76098-162">a.</span></span> <span data-ttu-id="76098-163">Saia do portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="76098-163">Sign out of the Azure classic portal.</span></span>
   
    <span data-ttu-id="76098-164">b.</span><span class="sxs-lookup"><span data-stu-id="76098-164">b.</span></span> <span data-ttu-id="76098-165">Abra o [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="76098-165">Open the [Azure portal](https://portal.azure.com/).</span></span>
   
    <span data-ttu-id="76098-166">c.</span><span class="sxs-lookup"><span data-stu-id="76098-166">c.</span></span> <span data-ttu-id="76098-167">Insira as credenciais do coadministrador e, em seguida, selecione **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="76098-167">Enter the credentials of the co-administrator, and then select **Sign in**.</span></span>
   
    ![Captura de tela de página de entrada do Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s324_azure-sign-in-with-co-admin.png)

## <a name="need-help-contact-support"></a><span data-ttu-id="76098-169">Precisa de ajuda?</span><span class="sxs-lookup"><span data-stu-id="76098-169">Need help?</span></span> <span data-ttu-id="76098-170">Entre em contato com o suporte.</span><span class="sxs-lookup"><span data-stu-id="76098-170">Contact support.</span></span>
<span data-ttu-id="76098-171">Se ainda tiver dúvidas, [entre em contato com o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) para resolver seu problema rapidamente.</span><span class="sxs-lookup"><span data-stu-id="76098-171">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your issue resolved quickly.</span></span>


