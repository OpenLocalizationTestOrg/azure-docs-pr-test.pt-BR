---
title: "aaaAssign um aplicativo de enterprise tooan usuário ou grupo no Active Directory do Azure | Microsoft Docs"
description: "Como tooselect um aplicativo de enterprise tooassign um tooit de usuário ou grupo no Active Directory do Azure"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 5817ad48-d916-492b-a8d0-2ade8c50a224
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 86c11f19892b9c947a5331677c17759178ed2806
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-user-or-group-tooan-enterprise-app-in-azure-active-directory"></a>Atribuir um aplicativo de enterprise tooan usuário ou grupo no Active Directory do Azure
É fácil tooassign um usuário ou um aplicativo do grupo tooyour enterprise no Azure Active Directory (AD do Azure). Você deve ter Olá permissões apropriadas toomanage Olá enterprise aplicativo e deve ser o administrador global para o diretório de saudação.

## <a name="how-do-i-assign-user-access-tooan-enterprise-app"></a>Como atribuir acesso de usuário tooan enterprise aplicativo?
1. Entrar toohello [portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global para o diretório de saudação.
2. Selecione **mais serviços**, insira o Active Directory do Azure na caixa de texto de saudação e, em seguida, selecione **Enter**.
3. Em Olá **do Active Directory do Azure - *directoryname***  folha (ou seja, Olá AD do Azure folha para diretório de saudação que você está gerenciando), selecione **aplicativos empresariais**.

    ![Abrir aplicativos empresariais](./media/active-directory-coreapps-assign-user-azure-portal/open-enterprise-apps.png)
4. Em Olá **aplicativos empresariais** folha, selecione **todos os aplicativos**. Você verá uma lista de aplicativos de saudação, que você pode gerenciar.
5. Em Olá **aplicativos corporativos - todos os aplicativos** folha, selecione um aplicativo.
6. Em Olá ***appname*** folha (ou seja, Olá folha com nome Olá Olá o aplicativo selecionado no título de saudação), selecione **usuários e grupos**.

    ![Selecionando Olá comando de todos os aplicativos](./media/active-directory-coreapps-assign-user-azure-portal/select-app-users.png)
7. Em Olá ***appname*** **-atribuição de grupo de & usuário** folha, selecione Olá **adicionar** comando.
8. Em Olá **Adicionar atribuição** folha, selecione **usuários e grupos**.

    ![Atribuir um aplicativo de usuário ou grupo toohello](./media/active-directory-coreapps-assign-user-azure-portal/assign-users.png)
9. Em Olá **usuários e grupos** folha, selecione um ou mais usuários ou grupos de saudação e, em seguida, selecione Olá **selecione** botão na parte inferior da saudação da folha de saudação.
10. Em Olá **Adicionar atribuição** folha, selecione **função**. Em seguida, na Olá **Selecionar função** folha, selecione um toohello de tooapply função usuários ou grupos selecionados e, em seguida, selecione Olá **Okey** botão na parte inferior da saudação da folha de saudação.
11. Em Olá **Adicionar atribuição** folha, selecione Olá **atribuir** botão na parte inferior da saudação da folha de saudação. Olá atribuída a usuários ou grupos terão permissões de saudação definidas pela função selecionada de saudação para esse aplicativo corporativo.

## <a name="next-steps"></a>Próximas etapas
* [Ver todos os meus grupos](active-directory-groups-view-azure-portal.md)
* [Remover uma atribuição de usuário ou de grupo de um aplicativo empresarial](active-directory-coreapps-remove-assignment-azure-portal.md)
* [Desabilitar as entradas de usuário em um aplicativo empresarial](active-directory-coreapps-disable-app-azure-portal.md)
* [Alterar nome de saudação ou logotipo de um aplicativo corporativo](active-directory-coreapps-change-app-logo-user-azure-portal.md)
