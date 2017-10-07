---
title: "aaaGet de Introdução ao Azure AD Privileged Identity Management | Microsoft Docs"
description: Saiba como toomanage privilegiado identidades de aplicativo do Azure Active Directory Privileged Identity Management hello no portal do Azure.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2299db7d-bee7-40d0-b3c6-8d628ac61071
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: a89205023a8dbcc3649fa732735ca927e64736ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="start-using-azure-ad-privileged-identity-management"></a>Começar a usar o Azure AD Privileged Identity Management
Com o Privileged Identity Management do Azure Active Directory (AD), você pode gerenciar, controlar e monitorar o acesso em sua organização. Esse escopo inclui tooresources de acesso no AD do Azure e outros Microsoft online services como Office 365 ou Microsoft Intune.

Este artigo mostra como tooadd Olá tooyour de aplicativo do Azure AD PIM painel do portal do Azure.

## <a name="add-hello-privileged-identity-management-application"></a>Adicionar aplicativo do hello Privileged Identity Management
Antes de usar o Azure AD Privileged Identity Management, você precisa tooadd Olá aplicativo tooyour painel do portal do Azure.

1. Entrar toohello [portal do Azure](https://portal.azure.com/) como um administrador global do seu diretório.
2. Se sua organização tiver mais de um diretório, selecione seu nome de usuário no canto superior direito de saudação do hello portal do Azure. Selecione o diretório de saudação onde você deseja toouse PIM.
3. Selecione **mais serviços** e usar Olá toosearch de caixa de texto de filtro para **do Azure AD Privileged Identity Management**.
4. Verificar **Pin toodashboard** e, em seguida, clique em **criar**. Olá aplicativo Privileged Identity Management é aberto.

Se você estiver hello primeira pessoa toouse Azure AD Privileged Identity Management em seu diretório, são atribuídos automaticamente Olá **administrador de segurança** e **administrador com privilégios de função** funções no diretório de saudação. Somente os administradores com privilégios de função podem gerenciar atribuições de função de usuários. Além disso, você pode escolher Olá toorun [Assistente de segurança.](active-directory-privileged-identity-management-security-wizard.md) que orienta você na experiência inicial de detecção e atribuição de saudação.

## <a name="navigate-tooyour-tasks"></a>Navegue tooyour tarefas
Depois de configurar o Azure AD Privileged Identity Management, você verá blade de navegação Olá sempre que você abrir o aplicativo hello. Use esta folha tooaccomplish suas tarefas de gerenciamento de identidade.

![Tarefas de nível superior para o PIM - captura de tela](./media/active-directory-privileged-identity-management-getting-started/PIM_Tasks_New.png)

* **Meu funções** leva você tooa lista de funções atribuídas tooyou. Essa seção é onde você ativará as funções para as quais está qualificado.
* **Aprovar Solicitações (Versão prévia)** exibe uma lista de solicitações de ativação de usuários pendentes no seu diretório. [Saiba mais.](./privileged-identity-management/azure-ad-pim-approval-workflow.md)
* **(Visualização) de solicitações pendentes** exibe qualquer tooactivate de toohave feita solicitações atuais.
* **Analise o acesso** leva você tooany pendentes acesso analisa o que você precisa toocomplete, se você revisar o acesso para você ou outra pessoa.
* **Funções de diretório do AD do Azure** localizado sob Olá seção 'Gerenciar' é o painel de saudação do atribuições de função com privilégios de função administradores toomanage, alterar as configurações de ativação de função, análises de acesso de início e muito mais. Opções de saudação nesse painel são desabilitadas para qualquer pessoa que não for um administrador com privilégios de função.

## <a name="next-steps"></a>Próximas etapas
Olá [visão geral do Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md) inclui mais detalhes sobre como você pode gerenciar o acesso administrativo em sua organização.

[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
