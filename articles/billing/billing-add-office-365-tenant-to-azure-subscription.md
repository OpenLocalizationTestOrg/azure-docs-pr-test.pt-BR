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
# <a name="associate-an-office-365-tenant-to-an-azure-subscription"></a>Associar um locatário do Office 365 a uma assinatura do Azure
Vincule suas assinaturas do Azure e o Office 365 separadas para que possam acessar o locatário do Office 365 da sua assinatura do Azure. Para vincular suas assinaturas, entre no Azure com a conta de administrador de serviços do Azure, adicione um diretório e adicione as contas organizacionais do Office 365 para o locatário do Azure Active Directory.

Se você quiser uma assinatura do Office 365 para usuários na sua instância do Azure Active Directory ou você tiver uma conta do Office 365, mas não uma conta do Azure, consulte [Inscrever-se no Azure com uma conta do Office 365](billing-use-existing-office-365-account-azure-subscription.md). 

## <a name="before-you-begin"></a>Antes de começar
* Você deve ter as credenciais do administrador de serviços de assinatura do Azure. Contas de coadministrador não podem realizar algumas das etapas neste artigo. Para alterar o administrador do serviço, veja [Como adicionar ou alterar funções de administrador do Azure](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).
* Você deve ter as credenciais de um administrador global do locatário do Office 365.
* O endereço de email do administrador de serviços não deve estar no locatário do Office 365.
* O endereço de email do administrador do serviço não deve ser igual ao do administrador global do locatário do Office 365.
* Se você usar um endereço de email que é uma conta da Microsoft e uma conta organizacional, altere temporariamente o administrador de serviços de sua assinatura do Azure para usar outra conta da Microsoft. Você pode criar uma nova conta da Microsoft na [Página de inscrição de conta da Microsoft](https://signup.live.com/).

## <a name="link-office-365-tenant-to-azure-subscription"></a>Vincular o locatário do Office 365 à assinatura do Azure
Para associar o locatário do Office 365 à assinatura do Azure, siga estas etapas:

### <a name="step-1-add-office-365-tenant-to-your-azure-subscription"></a>Etapa 1: adicionar o locatário do Office 365 à assinatura do Azure

1. Entre no [Portal clássico do Azure](https://manage.windowsazure.com/) com as credenciais de administrador do serviço.

    ![Captura de tela de entrada do Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)

2. No painel esquerdo, selecione **ACTIVE DIRECTORY**. Você não deverá ver o locatário do Office 365. Se isso acontecer, pule para a [Etapa 2: Alterar o diretório associado à assinatura do Azure](#Step2).
   
   ![Captura de tela da entrada do Active Directory](./media/billing-add-office-365-tenant-to-azure-subscription/s35-classic-portal-active-directory-entry.png)

3. Selecione **NOVO** > **DIRETÓRIO** > **CRIAÇÃO PERSONALIZADA**.
   
    ![Captura de tela da criação personalizada do Azure Active Directory](./media/billing-add-office-365-tenant-to-azure-subscription/s37-aad-custom-create.png)
   
4. Na página **Adicionar diretório** em **DIRETÓRIO**, selecione **Usar diretório existente**. Em seguida, selecione **estou pronto para sair agora** e selecione **Concluir** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).
   
    ![Captura de tela de "Usar diretório existente"](./media/billing-add-office-365-tenant-to-azure-subscription/s39_add-directory-use-existing.png)
   
5. Depois de sair, entre com as credenciais do administrador global do seu locatário do Office 365.
   
    ![Captura de tela de entrada no administrador global do Office 365](./media/billing-add-office-365-tenant-to-azure-subscription/s310_sign-in-global-admin-office-365.png)
   
6. Selecione **Continuar**.
   
    ![Captura de tela de verificação](./media/billing-add-office-365-tenant-to-azure-subscription/s311_use-contoso-directory-azure-verify.png)
   
7. Selecione **Sair agora**.
   
    ![Captura de tela de saída](./media/billing-add-office-365-tenant-to-azure-subscription/s312_use-contoso-directory-azure-confirm-and-sign-out.png)
   
8. Entre no [Portal clássico do Azure](https://manage.windowsazure.com/) com as credenciais de administrador do serviço.
   
    ![Captura de tela de entrada do Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)
   
9. Você deverá ver seu locatário do Office 365 no painel de controle.
   
    ![Captura de tela do painel](./media/billing-add-office-365-tenant-to-azure-subscription/s314_office-365-tenant-appear-in-azure.png)

### <a name="Step2"></a>Etapa 2: alterar o diretório associado à assinatura do Azure
   
1. Escolha a opção **Configurações**.
   
    ![Captura de tela do ícone de configurações do Portal Clássico do Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s315_azure-classic-portal-settings-icon.png)
   
2. Selecione sua assinatura do Azure e selecione **EDITAR DIRETÓRIO**.

    ![Captura de tela do diretório de edição de assinatura do Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s316_azure-subscription-edit-directory.png)
   
3. Selecione **Avançar** ![ícone Avançar](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).
   
    ![Captura de tela de "Alterar o diretório associado"](./media/billing-add-office-365-tenant-to-azure-subscription/s318_azure-change-associated-directory.png)
   
4. Examine as contas afetadas. Todos os coadministradores e usuários de [RBAC (Controle de Acesso Baseado em Função)](../active-directory/role-based-access-control-configure.md) com acesso Atribuído nos grupos de recursos existentes são removidos. O aviso que você recebe menciona apenas a remoção dos coadministradores.
      
    ![Captura de tela que mostra as contas de coadministrador a serem removidas.](./media/billing-add-office-365-tenant-to-azure-subscription/s322_azure-confirm-directory-mapping.png)
   
    ![Captura de tela que mostra um exemplo de conta de usuário a ser removida.](./media/billing-add-office-365-tenant-to-azure-subscription/s325_assigned-users-removed-resource-groups.png)
   
5. Selecione **Concluir** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).

### <a name="step-3-add-your-office-365-organizational-accounts-as-co-administrators-to-the-azure-active-directory-tenant"></a>Etapa 3: adicionar as contas organizacionais do Office 365 como coadministradores ao locatário do Azure Active Directory
   
1. Selecione a guia **ADMINISTRADORES** e, em seguida, selecione **ADICIONAR**.
   
    ![Captura de tela da guia de administradores de configurações do Portal Clássico do Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s319_azure-classic-portal-settings-administrators.png)
   
2. Insira uma conta organizacional de seu locatário do Office 365, clique para selecionar a assinatura do Azure e, em seguida, clique em **Concluir** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).
   
    ![Captura de tela de caixa de diálogo de adicionar coadministrador ao Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s320_azure-add-co-administrator.png)
   
3. Volte para a guia **ADMINISTRADORES**. Você deverá ver a conta organizacional exibida como coadministrador.
   
    ![Captura de tela da guia administradores](./media/billing-add-office-365-tenant-to-azure-subscription/s321_azure-co-administrator-added.png)
4.  Teste o acesso ao Azure com a conta de coadministrador.
   
    a. Saia do portal clássico do Azure.
   
    b. Abra o [Portal do Azure](https://portal.azure.com/).
   
    c. Insira as credenciais do coadministrador e, em seguida, selecione **Entrar**.
   
    ![Captura de tela de página de entrada do Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s324_azure-sign-in-with-co-admin.png)

## <a name="need-help-contact-support"></a>Precisa de ajuda? Entre em contato com o suporte.
Se ainda tiver dúvidas, [entre em contato com o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) para resolver seu problema rapidamente.


