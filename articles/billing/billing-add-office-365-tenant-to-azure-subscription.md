---
title: "locatário aaaUse um Office 365 com uma assinatura do Azure | Microsoft Docs"
description: "Saiba como tooadd um Office 365 (Locatário) do diretório tooan assinatura do Azure."
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
ms.openlocfilehash: e560370417bd074a7e37ceb7c60da45dbbbcf775
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="associate-an-office-365-tenant-tooan-azure-subscription"></a><span data-ttu-id="477cb-103">Associar um tooan de locatário do Office 365 assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="477cb-103">Associate an Office 365 tenant tooan Azure subscription</span></span>
<span data-ttu-id="477cb-104">Vincule suas assinaturas do Azure e o Office 365 separadas para que você pode acessar o locatário Olá Office 365 na sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="477cb-104">Link your separate Azure and Office 365 subscriptions so that you can access hello Office 365 tenant from your Azure subscription.</span></span> <span data-ttu-id="477cb-105">toolink suas assinaturas, entrar tooAzure com hello conta de administrador de serviço do Azure, adicione um diretório e adicionar Olá Office 365 contas organizacionais toohello Active Directory do Azure locatário.</span><span class="sxs-lookup"><span data-stu-id="477cb-105">toolink your subscriptions, sign in tooAzure with hello Azure service administrator account, add a directory, and add hello Office 365 organizational accounts toohello Azure Active Directory tenant.</span></span>

<span data-ttu-id="477cb-106">Se você quiser uma assinatura do Office 365 para usuários na sua instância do Azure Active Directory ou você tiver uma conta do Office 365, mas não uma conta do Azure, consulte [Inscrever-se no Azure com uma conta do Office 365](billing-use-existing-office-365-account-azure-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="477cb-106">If you want an Office 365 subscription for users in your Azure Active Directory instance or you have an Office 365 account but not an Azure account, see [Sign up for Azure with Office 365 account](billing-use-existing-office-365-account-azure-subscription.md).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="477cb-107">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="477cb-107">Before you begin</span></span>
* <span data-ttu-id="477cb-108">Você deve ter credenciais de saudação do administrador de serviço de assinatura do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="477cb-108">You must have hello credentials of hello Azure subscription service administrator.</span></span> <span data-ttu-id="477cb-109">Contas de coadministrador não podem fazer algumas das etapas de saudação neste artigo.</span><span class="sxs-lookup"><span data-stu-id="477cb-109">Co-administrator accounts can't do some of hello steps in this article.</span></span> <span data-ttu-id="477cb-110">toochange o administrador do serviço, consulte [como tooadd ou alterar funções de administrador do Azure](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).</span><span class="sxs-lookup"><span data-stu-id="477cb-110">toochange your service administrator, see [How tooadd or change Azure administrator roles](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).</span></span>
* <span data-ttu-id="477cb-111">Você deve ter credenciais de saudação de um administrador global do locatário do Office 365 hello.</span><span class="sxs-lookup"><span data-stu-id="477cb-111">You must have hello credentials of a global administrator of hello Office 365 tenant.</span></span>
* <span data-ttu-id="477cb-112">endereço de email de saudação do administrador de serviço de saudação não deve ser no locatário do Office 365 hello.</span><span class="sxs-lookup"><span data-stu-id="477cb-112">hello email address of hello service administrator must not be in hello Office 365 tenant.</span></span>
* <span data-ttu-id="477cb-113">endereço de email de saudação do administrador de serviço de saudação não deve corresponder de qualquer administrador global do locatário Olá Office 365.</span><span class="sxs-lookup"><span data-stu-id="477cb-113">hello email address of hello service administrator must not match that of any global administrator of hello Office 365 tenant.</span></span>
* <span data-ttu-id="477cb-114">Se você usar um endereço de email que é uma conta da Microsoft e uma conta organizacional, temporariamente altere Olá administrador de serviços de sua assinatura do Azure toouse outra conta da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="477cb-114">If you use an email address that is both a Microsoft account and an organizational account, temporarily change hello service administrator of your Azure subscription toouse another Microsoft account.</span></span> <span data-ttu-id="477cb-115">Você pode criar uma conta da Microsoft em Olá [página de inscrição de conta Microsoft](https://signup.live.com/).</span><span class="sxs-lookup"><span data-stu-id="477cb-115">You can create a Microsoft account at hello [Microsoft account signup page](https://signup.live.com/).</span></span>

## <a name="link-office-365-tenant-tooazure-subscription"></a><span data-ttu-id="477cb-116">Vincular a assinatura do Office 365 locatário tooAzure</span><span class="sxs-lookup"><span data-stu-id="477cb-116">Link Office 365 tenant tooAzure subscription</span></span>
<span data-ttu-id="477cb-117">tooassociate Olá Office 365 locatário toohello assinatura do Azure, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="477cb-117">tooassociate hello Office 365 tenant toohello Azure subscription, follow these steps:</span></span>

### <a name="step-1-add-office-365-tenant-tooyour-azure-subscription"></a><span data-ttu-id="477cb-118">Etapa 1: Adicionar tooyour de locatário do Office 365 assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="477cb-118">Step 1: Add Office 365 tenant tooyour Azure subscription</span></span>

1. <span data-ttu-id="477cb-119">Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com/) com as credenciais de administrador de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="477cb-119">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) with hello service administrator credentials.</span></span>

    ![Captura de tela de entrada do Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)

2. <span data-ttu-id="477cb-121">No painel esquerdo do hello, selecione **do ACTIVE DIRECTORY**.</span><span class="sxs-lookup"><span data-stu-id="477cb-121">In hello left pane, select **ACTIVE DIRECTORY**.</span></span> <span data-ttu-id="477cb-122">Você não deve ver locatário Olá Office 365.</span><span class="sxs-lookup"><span data-stu-id="477cb-122">You shouldn't see hello Office 365 tenant.</span></span> <span data-ttu-id="477cb-123">Se você vê-lo, ignore muito[etapa 2: altere o diretório Olá associado Olá assinatura do Azure](#Step2).</span><span class="sxs-lookup"><span data-stu-id="477cb-123">If you see it, skip too[Step 2: Change hello directory associated with hello Azure subscription](#Step2).</span></span>
   
   ![Captura de tela da entrada do Active Directory](./media/billing-add-office-365-tenant-to-azure-subscription/s35-classic-portal-active-directory-entry.png)

3. <span data-ttu-id="477cb-125">Selecione **NOVO** > **DIRETÓRIO** > **CRIAÇÃO PERSONALIZADA**.</span><span class="sxs-lookup"><span data-stu-id="477cb-125">Select **NEW** > **DIRECTORY** > **CUSTOM CREATE**.</span></span>
   
    ![Captura de tela da criação personalizada do Azure Active Directory](./media/billing-add-office-365-tenant-to-azure-subscription/s37-aad-custom-create.png)
   
4. <span data-ttu-id="477cb-127">Em Olá **Adicionar diretório** página em **diretório**, selecione **usar diretório existente**.</span><span class="sxs-lookup"><span data-stu-id="477cb-127">On hello **Add directory** page, under **DIRECTORY**, select **Use existing directory**.</span></span> <span data-ttu-id="477cb-128">Em seguida, selecione **estou pronto toobe sair agora**e selecione **concluir** ![ícone concluir](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="477cb-128">Then select **I am ready toobe signed out now**, and select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>
   
    ![Captura de tela de "Usar diretório existente"](./media/billing-add-office-365-tenant-to-azure-subscription/s39_add-directory-use-existing.png)
   
5. <span data-ttu-id="477cb-130">Depois que você está desconectado, entre com credenciais de administrador global saudação do seu locatário do Office 365.</span><span class="sxs-lookup"><span data-stu-id="477cb-130">After you are signed out, sign in with hello global administrator’s credentials of your Office 365 tenant.</span></span>
   
    ![Captura de tela de entrada no administrador global do Office 365](./media/billing-add-office-365-tenant-to-azure-subscription/s310_sign-in-global-admin-office-365.png)
   
6. <span data-ttu-id="477cb-132">Selecione **Continuar**.</span><span class="sxs-lookup"><span data-stu-id="477cb-132">Select **Continue**.</span></span>
   
    ![Captura de tela de verificação](./media/billing-add-office-365-tenant-to-azure-subscription/s311_use-contoso-directory-azure-verify.png)
   
7. <span data-ttu-id="477cb-134">Selecione **Sair agora**.</span><span class="sxs-lookup"><span data-stu-id="477cb-134">Select **Sign out now**.</span></span>
   
    ![Captura de tela de saída](./media/billing-add-office-365-tenant-to-azure-subscription/s312_use-contoso-directory-azure-confirm-and-sign-out.png)
   
8. <span data-ttu-id="477cb-136">Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com/) com as credenciais de administrador de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="477cb-136">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) with hello service administrator credentials.</span></span>
   
    ![Captura de tela de entrada do Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)
   
9. <span data-ttu-id="477cb-138">Você deve ver seu locatário do Office 365 no painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="477cb-138">You should see your Office 365 tenant in hello dashboard.</span></span>
   
    ![Captura de tela do painel](./media/billing-add-office-365-tenant-to-azure-subscription/s314_office-365-tenant-appear-in-azure.png)

### <span data-ttu-id="477cb-140"><a name="Step2"></a>Etapa 2: Altere o diretório Olá associado Olá assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="477cb-140"><a name="Step2"></a>Step 2: Change hello directory associated with hello Azure subscription</span></span>
   
1. <span data-ttu-id="477cb-141">Escolha a opção **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="477cb-141">Select **Settings**.</span></span>
   
    ![Captura de tela do ícone de configurações do Portal Clássico do Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s315_azure-classic-portal-settings-icon.png)
   
2. <span data-ttu-id="477cb-143">Selecione sua assinatura do Azure e selecione **EDITAR DIRETÓRIO**.</span><span class="sxs-lookup"><span data-stu-id="477cb-143">Select your Azure subscription, and then select **EDIT DIRECTORY**.</span></span>

    ![Captura de tela do diretório de edição de assinatura do Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s316_azure-subscription-edit-directory.png)
   
3. <span data-ttu-id="477cb-145">Selecione **Avançar** ![ícone Avançar](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).</span><span class="sxs-lookup"><span data-stu-id="477cb-145">Select **Next** ![Next icon](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).</span></span>
   
    ![Captura de tela de "Hello de alteração de diretório associado"](./media/billing-add-office-365-tenant-to-azure-subscription/s318_azure-change-associated-directory.png)
   
4. <span data-ttu-id="477cb-147">Examine as contas de saudação afetada.</span><span class="sxs-lookup"><span data-stu-id="477cb-147">Review hello affected accounts.</span></span> <span data-ttu-id="477cb-148">Todos os administradores e [controle de acesso baseado em função (RBAC)](../active-directory/role-based-access-control-configure.md) os usuários com acesso atribuído em grupos de recursos existente Olá são removidos.</span><span class="sxs-lookup"><span data-stu-id="477cb-148">All co-administrators and [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) users with assigned access in hello existing resource groups are removed.</span></span> <span data-ttu-id="477cb-149">Aviso de saudação que receber apenas menciona remoção de saudação de administradores.</span><span class="sxs-lookup"><span data-stu-id="477cb-149">hello warning you receive only mentions hello removal of co-administrators.</span></span>
      
    ![Captura de tela que mostra Olá contas de coadministrador toobe removido.](./media/billing-add-office-365-tenant-to-azure-subscription/s322_azure-confirm-directory-mapping.png)
   
    ![Captura de tela que mostra uma toobe de conta de usuário de exemplo é removido.](./media/billing-add-office-365-tenant-to-azure-subscription/s325_assigned-users-removed-resource-groups.png)
   
5. <span data-ttu-id="477cb-152">Selecione **Concluir** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="477cb-152">Select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>

### <a name="step-3-add-your-office-365-organizational-accounts-as-co-administrators-toohello-azure-active-directory-tenant"></a><span data-ttu-id="477cb-153">Etapa 3: Adicionar suas contas organizacionais do Office 365 como o locatário de Active Directory do Azure toohello administradores</span><span class="sxs-lookup"><span data-stu-id="477cb-153">Step 3: Add your Office 365 organizational accounts as co-administrators toohello Azure Active Directory tenant</span></span>
   
1. <span data-ttu-id="477cb-154">Selecione Olá **administradores** guia e, em seguida, selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="477cb-154">Select hello **ADMINISTRATORS** tab, and then select **ADD**.</span></span>
   
    ![Captura de tela da guia de administradores de configurações do Portal Clássico do Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s319_azure-classic-portal-settings-administrators.png)
   
2. <span data-ttu-id="477cb-156">Insira uma conta organizacional do seu locatário do Office 365, selecione Olá assinatura do Azure e, em seguida, selecione **concluir** ![ícone concluir](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span><span class="sxs-lookup"><span data-stu-id="477cb-156">Enter an organizational account of your Office 365 tenant, select hello Azure subscription, and then select **Complete** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).</span></span>
   
    ![Captura de tela de caixa de diálogo de adicionar coadministrador ao Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s320_azure-add-co-administrator.png)
   
3. <span data-ttu-id="477cb-158">Voltar toohello **administradores** guia. Você deve ver a conta organizacional hello, exibida como coadministrador.</span><span class="sxs-lookup"><span data-stu-id="477cb-158">Go back toohello **ADMINISTRATORS** tab. You should see hello organizational account displayed as co-administrator.</span></span>
   
    ![Captura de tela da guia administradores](./media/billing-add-office-365-tenant-to-azure-subscription/s321_azure-co-administrator-added.png)
4.  <span data-ttu-id="477cb-160">Teste tooAzure de acesso à conta de coadministrador hello.</span><span class="sxs-lookup"><span data-stu-id="477cb-160">Test access tooAzure with hello co-administrator account.</span></span>
   
    <span data-ttu-id="477cb-161">a.</span><span class="sxs-lookup"><span data-stu-id="477cb-161">a.</span></span> <span data-ttu-id="477cb-162">Saia do hello portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="477cb-162">Sign out of hello Azure classic portal.</span></span>
   
    <span data-ttu-id="477cb-163">b.</span><span class="sxs-lookup"><span data-stu-id="477cb-163">b.</span></span> <span data-ttu-id="477cb-164">Olá abrir [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="477cb-164">Open hello [Azure portal](https://portal.azure.com/).</span></span>
   
    <span data-ttu-id="477cb-165">c.</span><span class="sxs-lookup"><span data-stu-id="477cb-165">c.</span></span> <span data-ttu-id="477cb-166">Insira as credenciais de saudação de coadministrador hello e, em seguida, selecione **entrar**.</span><span class="sxs-lookup"><span data-stu-id="477cb-166">Enter hello credentials of hello co-administrator, and then select **Sign in**.</span></span>
   
    ![Captura de tela de página de entrada do Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s324_azure-sign-in-with-co-admin.png)

## <a name="need-help-contact-support"></a><span data-ttu-id="477cb-168">Precisa de ajuda?</span><span class="sxs-lookup"><span data-stu-id="477cb-168">Need help?</span></span> <span data-ttu-id="477cb-169">Entre em contato com o suporte.</span><span class="sxs-lookup"><span data-stu-id="477cb-169">Contact support.</span></span>
<span data-ttu-id="477cb-170">Se você ainda precisar de Ajuda, [entre em contato com o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget seu problema resolvido rapidamente.</span><span class="sxs-lookup"><span data-stu-id="477cb-170">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your issue resolved quickly.</span></span>


