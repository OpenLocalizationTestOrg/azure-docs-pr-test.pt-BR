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
# <a name="associate-an-office-365-tenant-tooan-azure-subscription"></a>Associar um tooan de locatário do Office 365 assinatura do Azure
Vincule suas assinaturas do Azure e o Office 365 separadas para que você pode acessar o locatário Olá Office 365 na sua assinatura do Azure. toolink suas assinaturas, entrar tooAzure com hello conta de administrador de serviço do Azure, adicione um diretório e adicionar Olá Office 365 contas organizacionais toohello Active Directory do Azure locatário.

Se você quiser uma assinatura do Office 365 para usuários na sua instância do Azure Active Directory ou você tiver uma conta do Office 365, mas não uma conta do Azure, consulte [Inscrever-se no Azure com uma conta do Office 365](billing-use-existing-office-365-account-azure-subscription.md). 

## <a name="before-you-begin"></a>Antes de começar
* Você deve ter credenciais de saudação do administrador de serviço de assinatura do Azure hello. Contas de coadministrador não podem fazer algumas das etapas de saudação neste artigo. toochange o administrador do serviço, consulte [como tooadd ou alterar funções de administrador do Azure](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).
* Você deve ter credenciais de saudação de um administrador global do locatário do Office 365 hello.
* endereço de email de saudação do administrador de serviço de saudação não deve ser no locatário do Office 365 hello.
* endereço de email de saudação do administrador de serviço de saudação não deve corresponder de qualquer administrador global do locatário Olá Office 365.
* Se você usar um endereço de email que é uma conta da Microsoft e uma conta organizacional, temporariamente altere Olá administrador de serviços de sua assinatura do Azure toouse outra conta da Microsoft. Você pode criar uma conta da Microsoft em Olá [página de inscrição de conta Microsoft](https://signup.live.com/).

## <a name="link-office-365-tenant-tooazure-subscription"></a>Vincular a assinatura do Office 365 locatário tooAzure
tooassociate Olá Office 365 locatário toohello assinatura do Azure, siga estas etapas:

### <a name="step-1-add-office-365-tenant-tooyour-azure-subscription"></a>Etapa 1: Adicionar tooyour de locatário do Office 365 assinatura do Azure

1. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com/) com as credenciais de administrador de serviço hello.

    ![Captura de tela de entrada do Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)

2. No painel esquerdo do hello, selecione **do ACTIVE DIRECTORY**. Você não deve ver locatário Olá Office 365. Se você vê-lo, ignore muito[etapa 2: altere o diretório Olá associado Olá assinatura do Azure](#Step2).
   
   ![Captura de tela da entrada do Active Directory](./media/billing-add-office-365-tenant-to-azure-subscription/s35-classic-portal-active-directory-entry.png)

3. Selecione **NOVO** > **DIRETÓRIO** > **CRIAÇÃO PERSONALIZADA**.
   
    ![Captura de tela da criação personalizada do Azure Active Directory](./media/billing-add-office-365-tenant-to-azure-subscription/s37-aad-custom-create.png)
   
4. Em Olá **Adicionar diretório** página em **diretório**, selecione **usar diretório existente**. Em seguida, selecione **estou pronto toobe sair agora**e selecione **concluir** ![ícone concluir](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).
   
    ![Captura de tela de "Usar diretório existente"](./media/billing-add-office-365-tenant-to-azure-subscription/s39_add-directory-use-existing.png)
   
5. Depois que você está desconectado, entre com credenciais de administrador global saudação do seu locatário do Office 365.
   
    ![Captura de tela de entrada no administrador global do Office 365](./media/billing-add-office-365-tenant-to-azure-subscription/s310_sign-in-global-admin-office-365.png)
   
6. Selecione **Continuar**.
   
    ![Captura de tela de verificação](./media/billing-add-office-365-tenant-to-azure-subscription/s311_use-contoso-directory-azure-verify.png)
   
7. Selecione **Sair agora**.
   
    ![Captura de tela de saída](./media/billing-add-office-365-tenant-to-azure-subscription/s312_use-contoso-directory-azure-confirm-and-sign-out.png)
   
8. Entrar toohello [portal clássico do Azure](https://manage.windowsazure.com/) com as credenciais de administrador de serviço hello.
   
    ![Captura de tela de entrada do Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)
   
9. Você deve ver seu locatário do Office 365 no painel de saudação.
   
    ![Captura de tela do painel](./media/billing-add-office-365-tenant-to-azure-subscription/s314_office-365-tenant-appear-in-azure.png)

### <a name="Step2"></a>Etapa 2: Altere o diretório Olá associado Olá assinatura do Azure
   
1. Escolha a opção **Configurações**.
   
    ![Captura de tela do ícone de configurações do Portal Clássico do Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s315_azure-classic-portal-settings-icon.png)
   
2. Selecione sua assinatura do Azure e selecione **EDITAR DIRETÓRIO**.

    ![Captura de tela do diretório de edição de assinatura do Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s316_azure-subscription-edit-directory.png)
   
3. Selecione **Avançar** ![ícone Avançar](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).
   
    ![Captura de tela de "Hello de alteração de diretório associado"](./media/billing-add-office-365-tenant-to-azure-subscription/s318_azure-change-associated-directory.png)
   
4. Examine as contas de saudação afetada. Todos os administradores e [controle de acesso baseado em função (RBAC)](../active-directory/role-based-access-control-configure.md) os usuários com acesso atribuído em grupos de recursos existente Olá são removidos. Aviso de saudação que receber apenas menciona remoção de saudação de administradores.
      
    ![Captura de tela que mostra Olá contas de coadministrador toobe removido.](./media/billing-add-office-365-tenant-to-azure-subscription/s322_azure-confirm-directory-mapping.png)
   
    ![Captura de tela que mostra uma toobe de conta de usuário de exemplo é removido.](./media/billing-add-office-365-tenant-to-azure-subscription/s325_assigned-users-removed-resource-groups.png)
   
5. Selecione **Concluir** ![complete-icon](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).

### <a name="step-3-add-your-office-365-organizational-accounts-as-co-administrators-toohello-azure-active-directory-tenant"></a>Etapa 3: Adicionar suas contas organizacionais do Office 365 como o locatário de Active Directory do Azure toohello administradores
   
1. Selecione Olá **administradores** guia e, em seguida, selecione **adicionar**.
   
    ![Captura de tela da guia de administradores de configurações do Portal Clássico do Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s319_azure-classic-portal-settings-administrators.png)
   
2. Insira uma conta organizacional do seu locatário do Office 365, selecione Olá assinatura do Azure e, em seguida, selecione **concluir** ![ícone concluir](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).
   
    ![Captura de tela de caixa de diálogo de adicionar coadministrador ao Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s320_azure-add-co-administrator.png)
   
3. Voltar toohello **administradores** guia. Você deve ver a conta organizacional hello, exibida como coadministrador.
   
    ![Captura de tela da guia administradores](./media/billing-add-office-365-tenant-to-azure-subscription/s321_azure-co-administrator-added.png)
4.  Teste tooAzure de acesso à conta de coadministrador hello.
   
    a. Saia do hello portal clássico do Azure.
   
    b. Olá abrir [portal do Azure](https://portal.azure.com/).
   
    c. Insira as credenciais de saudação de coadministrador hello e, em seguida, selecione **entrar**.
   
    ![Captura de tela de página de entrada do Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s324_azure-sign-in-with-co-admin.png)

## <a name="need-help-contact-support"></a>Precisa de ajuda? Entre em contato com o suporte.
Se você ainda precisar de Ajuda, [entre em contato com o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget seu problema resolvido rapidamente.


