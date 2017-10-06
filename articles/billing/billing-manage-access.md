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
# <a name="manage-access-toobilling-information-for-azure-using-role-based-access-control"></a>Gerenciar informações de toobilling de acesso do Azure usando o controle de acesso baseado em função

Você pode conceder acesso para o Azure toomembers de informações de cobrança da sua equipe, atribuindo uma saudação assinatura de tooyour de funções de usuário a seguir: conta de administrador, administrador de serviço, coadministrador, proprietário, colaborador, leitor e leitor de cobrança. Eles teriam acesso toobilling informações Olá [portal do Azure](https://portal.azure.com/), e eles podem usar o hello [cobrança APIs](billing-usage-rate-card-overview.md) tooprogrammatically obter faturas (uma vez incluído-entrada) e detalhes de uso. Para obter mais informações sobre quem pode conceder funções e o que as funções podem fazer, consulte [funções no Azure RBAC](../active-directory/role-based-access-built-in-roles.md).

## <a name="opt-in"></a>Permitir que usuários adicionais tooaccess faturas

Olá administrador da conta deve aceitar usando Olá [portal do Azure](https://portal.azure.com/) permitir acesso tooinvoices para outros usuários e por meio da API.

1. Olá administrador da conta, selecione sua assinatura do hello [folha assinaturas](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) no portal do Azure.

1. Selecione **faturas** e **acessar tooinvoices**.

    ![Captura de tela mostra como toodelegate acessar tooinvoices](./media/billing-manage-access/AA-optin.png)

1. Ativar **em** acesso Olá seguido por salvar as alterações do hello, tooallow usuários na assinatura funções com escopo toodownload fatura.

    ![Captura de tela mostra-off toodelegate tooinvoice de acesso](./media/billing-manage-access/AA-optinAllow.png)

Aceitar permite administrador de serviço, coadministrador, proprietário, colaborador, leitor e de cobrança leitor Olá assinatura toodownload PDF as notas fiscais em Olá portal do Azure. No entanto, faturas anteriores dezembro de 2016 são toohello disponível somente o administrador da conta agora.

Olá administrador da conta também pode configurar toohave faturas enviadas por email. mais, consulte toolearn [obter sua fatura no email](billing-download-azure-invoice-daily-usage-date.md).

## <a name="adding-users-toohello-billing-reader-role"></a>Adicionando a função de leitor de cobrança de toohello usuários

a função de leitor de cobrança Olá tem informações de cobrança toosubscription acesso somente leitura no portal do Azure e nenhum tooservices de acesso, como máquinas virtuais e contas de armazenamento. Atribuir Olá toosomeone de função de leitor de cobrança que precisa acessar as informações de cobrança de assinatura toohello mas não Olá toomanage de capacidade do Azure services. Essa função é apropriada para os usuários em uma organização que executam apenas gerenciamento de custos e financeiro de assinaturas do Azure.

1. Selecione sua assinatura do hello [folha assinaturas](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) no portal do Azure.

1. Selecione **Controle de acesso (IAM)** e, em seguida, clique em **Adicionar**.

    ![Captura de tela mostra IAM na folha da assinatura de saudação](./media/billing-manage-access/select-iam.PNG)

1. Escolha **cobrança leitor** em Olá **selecionar uma função** página.

    ![Captura de tela mostra o leitor de cobrança no modo de exibição de pop-up Olá](./media/billing-manage-access/select-roles.PNG)

1. Digite o email Olá para usuário Olá você deseja tooinvite e clique **Okey** toosend convite de saudação.

    ![Captura de tela que mostra tooenter email tooinvite alguém](./media/billing-manage-access/add-user.PNG)

1. Siga as instruções em toolog de email de convite de saudação em como um leitor de cobrança.

    ![Captura de tela que mostra o que Olá leitor de cobrança pode ver no portal do Azure](./media/billing-manage-access/billing-reader-view.png)

> [!NOTE]
> recurso de cobrança leitor Hello está em visualização e ainda não suporta as assinaturas do enterprise (EA) ou não global nuvens.

## <a name="adding-users-tooother-roles"></a>Adicionando usuários tooother funções

Outras funções, como o Proprietário ou Colaborador, os usuários podem acessar as informações de cobrança não apenas, mas também os serviços do Azure. Essas funções, consulte o toomanage [adicionar ou alterar funções de administrador do Azure que gerenciam a assinatura de saudação ou serviços](billing-add-change-azure-subscription-administrator.md).

## <a name="who-can-access-hello-account-centerhttpsaccountwindowsazurecom"></a>Quem pode acessar Olá [Centro de contas](https://account.windowsazure.com)?

Olá administrador da conta pode fazer logon no Centro de contas toohello. Olá administrador da conta é proprietário legal Olá assinatura hello. Por padrão, Olá pessoa inscreveu ou comprou Olá assinatura do Azure é Olá administrador da conta, a menos que Olá [a propriedade de assinatura foi transferida](billing-subscription-transfer.md) toosomebody else. Olá administrador da conta pode criar assinaturas, cancelar assinaturas, alterar o endereço para cobrança Olá para uma assinatura e gerenciar políticas de acesso para a assinatura de saudação.

## <a name="need-help-contact-support"></a>Precisa de ajuda? Entre em contato com o suporte.

Se você ainda tiver mais perguntas, [entre em contato com o suporte](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget seu problema resolvido rapidamente.
