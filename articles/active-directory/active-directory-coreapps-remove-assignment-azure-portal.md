---
title: "aaaRemove uma atribuição de usuário ou grupo de um aplicativo de empresa no Active Directory do Azure | Microsoft Docs"
description: "Como tooremove Olá acessar atribuição de um usuário ou grupo de um aplicativo de empresa no Active Directory do Azure"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7b2d365b-ae92-477f-9702-353cc6acc5ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: c067ecf59b4dedfe8f848357ca8bd545bdc610eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="remove-a-user-or-group-assignment-from-an-enterprise-app-in-azure-active-directory"></a>Remover a atribuição de um usuário ou grupo de um aplicativo empresarial no Azure Active Directory
É fácil tooremove um usuário ou um grupo sejam atribuídos acesso tooone de seus aplicativos de empresa no Active Directory do Azure (AD do Azure). Você deve ter Olá permissões apropriadas toomanage Olá enterprise aplicativo e deve ser o administrador global para o diretório de saudação.

## <a name="how-do-i-remove-a-user-or-group-assignment"></a>Como removo a atribuição de um usuário ou grupo?
1. Entrar toohello [portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global para o diretório de saudação.
2. Selecione **mais serviços**, digite **Active Directory do Azure** Olá caixa de texto e, em seguida, selecione **Enter**.
3. Em Olá **do Active Directory do Azure - *directoryname***  folha (ou seja, Olá AD do Azure folha para diretório de saudação que você está gerenciando), selecione **aplicativos empresariais**.

    ![Abrir aplicativos empresariais](./media/active-directory-coreapps-remove-assignment-user-azure-portal/open-enterprise-apps.png)
4. Em Olá **aplicativos empresariais** folha, selecione **todos os aplicativos**. Você verá uma lista de aplicativos de saudação, que você pode gerenciar.
5. Em Olá **aplicativos corporativos - todos os aplicativos** folha, selecione um aplicativo.
6. Em Olá ***appname*** folha (ou seja, Olá folha com nome Olá Olá o aplicativo selecionado no título de saudação), selecione **usuários e grupos**.

    ![Seleção de usuários ou de grupos](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-app-users.png)
7. Em Olá ***appname*** **-atribuição de grupo de & usuário** folha, selecione uma das mais usuários ou grupos e, em seguida, selecione Olá **remover** comando. Confirme sua decisão no prompt de saudação.

    ![Selecionando o comando de Remove Olá](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-users.png)

## <a name="next-steps"></a>Próximas etapas
* [Ver todos os meus grupos](active-directory-groups-view-azure-portal.md)
* [Atribuir um aplicativo de enterprise tooan usuário ou grupo](active-directory-coreapps-assign-user-azure-portal.md)
* [Desabilitar as entradas de usuário em um aplicativo empresarial](active-directory-coreapps-disable-app-azure-portal.md)
* [Alterar nome de saudação ou logotipo de um aplicativo corporativo](active-directory-coreapps-change-app-logo-user-azure-portal.md)
