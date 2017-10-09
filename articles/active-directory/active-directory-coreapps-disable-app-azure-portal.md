---
title: "aaaDisable entradas do usuário para um aplicativo de empresa no Active Directory do Azure | Microsoft Docs"
description: "Como toodisable um aplicativo corporativo para que nenhum usuário pode entrar tooit no Active Directory do Azure"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a27562f9-18dc-42e8-9fee-5419566f8fd7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 4c560b59359d433b0852a7606cc2cc0204866234
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="disable-user-sign-ins-for-an-enterprise-app-in-azure-active-directory"></a>Desabilitar entradas de usuário em um aplicativo empresarial no Azure Active Directory
É fácil toodisable um aplicativo corporativo para que nenhum usuário pode entrar tooit no Azure Active Directory (AD do Azure). Você deve ter Olá permissões apropriadas toomanage Olá enterprise aplicativo e deve ser o administrador global para o diretório de saudação.

## <a name="how-do-i-disable-user-sign-ins"></a>Como desabilitar entradas de usuário?
1. Entrar toohello [portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global para o diretório de saudação.
2. Selecione **mais serviços**, digite **Active Directory do Azure** Olá caixa de texto e, em seguida, selecione **Enter**.
3. Em Olá **Active Directory do Azure** -  ***directoryname*** folha (ou seja, Olá AD do Azure folha para diretório de saudação que você está gerenciando), selecione **aplicativos empresariais**.

    ![Abrir aplicativos empresariais](./media/active-directory-coreapps-disable-app-azure-portal/open-enterprise-apps.png)
4. Em Olá **aplicativos empresariais** folha, selecione **todos os aplicativos**. Você ver uma lista de aplicativos de saudação, que você pode gerenciar.
5. Em Olá **aplicativos corporativos - todos os aplicativos** folha, selecione um aplicativo.
6. Em Olá ***appname*** folha (ou seja, Olá folha com nome Olá Olá o aplicativo selecionado no título de saudação), selecione **propriedades**.

    ![Selecionando Olá comando de todos os aplicativos](./media/active-directory-coreapps-disable-app-azure-portal/select-app.png)
7. Em Olá ***appname*** - **propriedades** folha, selecione **não** para **habilitada para usuários em toosign?**.
8. Selecione Olá **salvar** comando.

## <a name="next-steps"></a>Próximas etapas
* [Ver todos os meus grupos](active-directory-groups-view-azure-portal.md)
* [Atribuir um aplicativo de enterprise tooan usuário ou grupo](active-directory-coreapps-assign-user-azure-portal.md)
* [Remover uma atribuição de usuário ou de grupo de um aplicativo empresarial](active-directory-coreapps-remove-assignment-azure-portal.md)
* [Alterar nome de saudação ou logotipo de um aplicativo corporativo](active-directory-coreapps-change-app-logo-user-azure-portal.md)
