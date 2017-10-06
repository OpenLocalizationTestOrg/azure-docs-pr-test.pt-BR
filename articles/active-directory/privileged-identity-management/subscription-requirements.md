---
title: assinaturas de gerenciamento de identidade aaaPrivileged - Azure | Microsoft Docs
description: "Explica a assinatura hello e requisitos de licenciamento para gerenciar e usar o Azure AD Privileged Identity Management em seu locatário"
services: active-directory
documentationcenter: 
author: barclayn
manager: mbaldwin
editor: mwahl
ms.assetid: 34367721-8b42-4fab-a443-a2e55cdbf33d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: barclayn
ms.custom: pim
ms.openlocfilehash: 2639d13c250a582fdcf0b277c9bab37fdfcabcb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-privileged-identity-management-subscription-requirements"></a>Requisitos de assinatura do Azure Active Directory Privileged Identity Management

Azure AD Privileged Identity Management está disponível como parte da edição Premium P2 de saudação do AD do Azure. Para obter mais informações sobre Olá outros recursos de P2 e como ele se compara tooPremium P1, consulte [edições do Active Directory do Azure](../active-directory-editions.md).

>[!NOTE]
Quando Privileged Identity Management do Azure Active Directory (AD do Azure) estava no modo de visualização, não havia nenhuma verificação de licença para um serviço de saudação do locatário tootry.  Agora que o Azure AD Privileged Identity Management alcança disponibilidade geral, uma assinatura de avaliação ou paga deve estar presente para Olá locatário toocontinue usando Privileged Identity Management após dezembro de 2016.
  

## <a name="confirm-your-trial-or-paid-subscription"></a>Confirmar sua assinatura de avaliação ou paga

Se você não tiver certeza se sua organização tem uma versão de avaliação ou comprou a assinatura, você pode verificar se há uma assinatura em seu locatário usando comandos Olá incluídos no Azure Active Directory módulo para Windows PowerShell V1. 
1. Abra uma janela do PowerShell.
2. Digite `Connect-MsolService` tooauthenticate como um usuário em seu locatário.
3. Digite `Get-MsolSubscription | ft SkuPartNumber,IsTrial,Status`.

Esse comando recupera uma lista de assinaturas de saudação em seu locatário. Se não houver que nenhuma linha retornada, que você precisará de avaliação tooobtain um Azure AD Premium P2, compre uma assinatura do Azure AD Premium P2 ou EMS E5 toouse de assinatura do Azure AD Privileged Identity Management.  tooget uma versão de avaliação e começar a usar o Azure AD Privileged Identity Management, leia [Introdução ao Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md).

Se esse comando retorna uma linha na qual SkuPartNumber é "AAD_PREMIUM_P2" ou "EMSPREMIUM" e IsTrial for "True", isso indica que uma versão de avaliação do Azure AD Premium P2 está presente no locatário hello.  Se o status da assinatura Olá não está habilitado e você não tiver uma compra de assinatura do Azure AD Premium P2 ou EMS E5, você deve comprar uma assinatura do Azure AD Premium P2 ou EMS E5 toocontinue de assinatura usando o Azure AD Privileged Identity Management.

Azure AD Premium P2 está disponível por meio de um [Microsoft Enterprise Agreement](https://www.microsoft.com/en-us/licensing/licensing-programs/enterprise.aspx), Olá [programa de licença de Volume aberto](https://www.microsoft.com/en-us/licensing/licensing-programs/open-license.aspx)e hello [programa de fornecedores de soluções de nuvem](https://partner.microsoft.com/en-US/cloud-solution-provider). Os assinantes do Azure e do Office 365 também podem adquirir o Azure AD Premium P2 online.  Para obter mais informações sobre preços do Azure AD Premium e como tooorder online pode ser encontrada em [preços do Azure Active Directory](https://azure.microsoft.com/en-us/pricing/details/active-directory/).

## <a name="azure-ad-privileged-identity-management-is-not-available-in-tenant"></a>O Azure AD Privileged Identity Management não está disponível no locatário

O Azure AD Privileged Identity Management não estará mais disponível em seu locatário se:
- Sua organização usou o Azure AD Privileged Identity Management quando ele estava no modo de visualização e não comprou a assinatura Premium P2 do Azure AD ou EMS E5.
- Sua organização tinha uma avaliação do Premium P2 do Azure AD ou EMS E5 que expirou.
- Sua organização comprou uma assinatura que expirou.

Quando uma assinatura Premium P2 do Azure AD ou EMS E5 expira, ou uma organização que estava usando o Azure AD Privileged Identity Management no modo visualização não compra a assinatura Premium P2 do Azure AD ou EMS E5:

- Funções de tooAzure AD de atribuições de função permanente não serão afetadas.
- Olá extensão do Azure AD Privileged Identity Management em Olá portal do Azure, bem como cmdlets de API do Graph hello e interfaces do PowerShell do Azure AD Privileged Identity Management, não será esteja disponível para usuários com privilégios de tooactivate funções, gerenciar acesso privilegiado, ou executar análises de acesso de funções privilegiadas.
- Atribuições de função qualificado de funções do AD do Azure serão removidas, como os usuários não será capaz de tooactivate privilegiado funções.
- Quaisquer revisões de acesso contínuo de funções do Azure AD serão encerradas, e definições de configuração do Azure AD Privileged Identity Management serão removidas.
- O Azure AD Privileged Identity Management não enviará emails sobre alterações de atribuição de função.

## <a name="next-steps"></a>Próximas etapas

- [Introdução ao Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md)
- [Funções no Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-roles.md)
