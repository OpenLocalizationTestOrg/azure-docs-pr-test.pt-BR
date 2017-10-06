---
title: "alertas de segurança tooconfigure aaaHow | Microsoft Docs"
description: "Saiba como segurança tooconfigure alertas para a extensão do Privileged Identity Management do Azure."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 4e0c911a-36c6-42a0-8f79-a01c03d2d04f
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 1b3c4a7d36fa3f81bb3fe2574d675fdf0ab34909
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-security-alerts-in-azure-ad-privileged-identity-management"></a>Como a segurança tooconfigure alertas no Azure AD Privileged Identity Management
## <a name="security-alerts"></a>Alertas de segurança
O Azure PIM (Privileged Identity Management) gera alertas quando há atividade suspeita ou não segura em seu ambiente. Quando um alerta é disparado, ele é exibido no painel PIM hello. Selecione Olá alerta toosee um relatório que lista Olá usuários ou funções que disparou o alerta de saudação.

![Alertas de segurança do painel PIM – captura de tela][1]

| Alerta | Gatilho | Recomendações |
| --- | --- | --- |
| **As funções estão sendo atribuídas fora do PIM** |Um administrador permanentemente foi atribuído a função tooa, fora da interface PIM hello. |Examine a nova atribuição de função hello. Como outros serviços só podem atribuir administradores permanentes, altere atribuição qualificados tooan se necessário. |
| **As funções estão sendo ativadas com muita frequência** |Havia muitos reativações de hello a mesma função no tempo de saudação permitida nas configurações de saudação. |Entre em contato com hello usuário toosee por que eles ativou a função hello muitas vezes. Talvez o tempo de saudação que limite é muito curto para eles toocomplete suas tarefas, ou talvez elas estiver usando scripts tooautomatically ativar uma função. |
| **Roles don't require multi-factor authentication for activation (As funções não exigem o multi-factor authentication para ativação)** |Há funções sem MFA habilitada nas configurações de saudação. |Exigir MFA para funções hello mais altamente privilegiado, mas recomendamos que você habilitar a MFA para ativação de todas as funções. |
| **Administrators aren't using their privileged roles (Os administradores não estão utilizando suas funções privilegiadas)** |Existem administradores qualificados que não ativaram suas funções recentemente. |Inicie um acesso revisão toodetermine Olá os usuários que não precisam mais de acesso. |
| **Há muitos administradores globais** |Existem mais administradores globais do que o recomendado. |Caso você tenha um grande número de administradores globais, é provável que os usuários estejam obtendo mais permissões do que eles precisam. Mover os usuários tooless privilegiado funções ou fazer algumas delas qualificados para a função hello em vez de atribuídos permanentemente. |

## <a name="configure-security-alert-settings"></a>Definir configurações de alerta de segurança
Você pode personalizar alguns dos alertas de segurança Olá no PIM toowork com seu ambiente e os objetivos de segurança. Siga a folha de configurações essas etapas tooreach hello:

1. Entrar toohello [portal do Azure](https://portal.azure.com/) e selecione hello **do Azure AD Privileged Identity Management** lado a lado do painel de saudação.
2. Selecione **Managed privileged roles (Funções com privilégios gerenciadas)** > **Configurações** > **Configurações de alertas**.
   
    ![Navegue toosecurity configurações de alertas][2]

### <a name="roles-are-being-activated-too-frequently-alert"></a>Alerta “As funções estão sendo ativadas com muita frequência”
Esse alerta se um usuário ativa os gatilhos Olá a mesma função com privilégios várias vezes em um período especificado. Você pode configurar ambos Olá tempo período e hello de número de ativações.

* **Período de renovação da ativação**: especificar em dias, horas, minutos, e pela segunda vez Olá período desejar toouse tootrack suspeitas renovações.
* **Número de renovações de ativação de**: especificar Olá número de ativações de too100 2, que você considerar valioso de alerta, dentro do período de saudação escolhido. Você pode alterar essa configuração pelo controle deslizante de saudação movimentação ou digitando um número na caixa de texto de saudação.

### <a name="there-are-too-many-global-administrators-alert"></a>Alerta “Há muitos administradores globais”
O PIM disparará esse alerta se dois critérios diferentes forem atendidos, e você poderá configurar ambos. Primeiro, é necessário tooreach um certo limite de administradores globais. Em segundo lugar, um determinado percentual do seu total de atribuições de função deve ser de administradores globais. Se você atender apenas uma dessas medidas, o alerta de saudação não aparecer.  

* **Número mínimo de administradores globais**: especificar Olá número de administradores globais, de too100 2, que você considere um valor de unsafe.
* **Percentual de administradores globais**: especificar Olá percentual de administradores que são administradores globais, de 0% too100%, que não é segura em seu ambiente.

### <a name="administrators-arent-using-their-privileged-roles-alert"></a>Alerta “Administrators aren't using their privileged roles” (Os administradores não estão utilizando suas funções privilegiadas)
Esse alerta será disparado se um usuário passar um determinado período sem ativar uma função.

* **Número de dias**: especificar Olá número de dias, too100 0, o que um usuário pode prosseguir sem ativar uma função.

## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-configure-security-alerts/PIM_security_dash.png
[2]: ./media/active-directory-privileged-identity-management-how-to-configure-security-alerts/PIM_security_settings.png
