---
title: aaaSign para o Office 365 com a conta do Azure | Microsoft Docs
description: Saiba como assinatura toocreate um Office 365 usando uma conta do Azure
services: 
documentationcenter: 
author: JiangChen79
manager: adpick
editor: 
tags: billing,top-support-issue
ms.assetid: 
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: cjiang
ms.openlocfilehash: d19e1c1edff0b9658b639e796a72bbf4e87b9c3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-up-for-an-office-365-subscription-with-your-azure-account"></a>Inscreva-se para obter uma assinatura do Office 365 com sua conta do Azure
Se você for assinante do Azure, você pode usar toosign sua conta do Azure para uma assinatura do Office 365. Se você fizer parte de uma organização que tem uma assinatura do Azure, será possível criar uma assinatura do Office 365 para usuários em seu Azure AD (Azure Active Directory) existente. Inscreva-se tooOffice 365 usando uma conta que tenha permissões de Administrador Global ou administrador de cobrança em seu locatário do Active Directory do Azure. Para obter mais informações, consulte [Check my account permissions in Azure AD (Verificar minhas permissões de conta no Azure AD)](#RoleInAzureAD) e [Atribuindo funções de administrador no Azure Active Directory](../active-directory/active-directory-assign-admin-roles.md).

Se você já tiver uma conta do Office 365 e uma assinatura do Azure, você pode [associar um tooan de locatário do Office 365 assinatura do Azure](billing-add-office-365-tenant-to-azure-subscription.md).

## <a name="get-an-office-365-subscription-by-using-your-azure-account"></a>Obter uma assinatura do Office 365 usando sua conta do Azure

1. Vá toohello [página de produto do Office 365](https://products.office.com/business)e selecione um plano.
2. Clique em **entrar** no canto superior direito de saudação da página de saudação.

    ![captura de tela da página de avaliação do Office 365](./media/billing-use-existing-azure-account-office-365-subscription/12-office-365-trial-page.png)
3. Conecte-se com as credenciais de conta do Azure. Se você estiver criando uma assinatura para sua organização, use uma conta do Azure que é um membro da função de diretório Administrador Global ou administrador de cobrança de saudação em seu locatário do Active Directory do Azure.

    ![captura de tela de conexão do Office 365](./media/billing-use-existing-azure-account-office-365-subscription/13-office-365-sign-in.png)
4. Clique em **Experimentar agora**.

    ![Captura de tela que confirma o pedido do Office 365.](./media/billing-use-existing-azure-account-office-365-subscription/14-office-365-confirm-your-order.png)
5. Na página de confirmação de pedido hello, clique em **continuar**.

    ![Captura de tela de recibo do pedido Olá Office 365](./media/billing-use-existing-azure-account-office-365-subscription/15-office-365-order-receipt.png)

Está tudo pronto para você. Se você criou a assinatura Olá Office 365 para sua organização, use Olá seguindo as etapas toocheck que os usuários do AD do Azure agora estão no Office 365.

1. Abra o Centro de administração do Office 365 de saudação.
2. Expanda **USUÁRIOS** e clique em **Usuários Ativos**.

    ![Captura de tela de usuários do hello Office 365 admin center](./media/billing-use-existing-azure-account-office-365-subscription/16-office-365-admin-center-users.png)

Depois de você se inscrever, Olá assinatura do Office 365 é adicionada toohello mesma instância do Active Directory do Azure que sua assinatura do Azure pertence. Para obter mais informações, consulte [More about Azure and Office 365 subscriptions (Mais sobre as assinaturas do Azure e do Office 365)](billing-use-existing-office-365-account-azure-subscription.md#more-about-subs) e [Como as assinaturas do Azure são associadas ao Azure Active Directory](../active-directory/active-directory-how-subscriptions-associated-directory.md).

## <a id="RoleInAzureAD"></a>Verifique as permissões da minha conta no Azure AD
1. Entrar toohello [portal do Azure](https://portal.azure.com/).
2. Clique em **Mais serviços** e, em seguida, pesquise **Active Directory**.

    ![Captura de tela do Active Directory no hello portal do Azure](./media/billing-use-existing-azure-account-office-365-subscription/billing-more-services-active-directory.png)
3. Clique em **Usuários e grupos** > **Todos os usuários**.
4. Selecione o nome de usuário de saudação. 

    ![Captura de tela que mostra os usuários do Active Directory do Azure Olá](./media/billing-use-existing-azure-account-office-365-subscription/billing-users-groups.png)

5. Clique em **Função do diretório**.
  
    ![Captura de tela que mostra a função de diretório do portal do Azure Olá](./media/billing-use-existing-azure-account-office-365-subscription/billing-user-directory-role.png)
6.  função Hello **Administrador Global** ou **administrador limitado** > **administrador de cobrança** é toocreate necessária uma assinatura do Office 365 para usuários no seu Azure Active Directory existente.

    ![Captura de tela que mostra a função do diretório Administrador de cobrança do portal do Azure](./media/billing-use-existing-azure-account-office-365-subscription/billing-directoryrole-limited.png)

## <a name="need-help-contact-support"></a>Precisa de ajuda? Entre em contato com o suporte.
Se você ainda precisar de Ajuda, [entre em contato com o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget seu problema resolvido rapidamente. 
