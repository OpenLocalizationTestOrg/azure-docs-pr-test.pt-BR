---
title: "aaaHow tooAssign usuários tooapplications | Microsoft Docs"
description: "Entender como os usuários são atribuídos tooan aplicativo em seu locatário"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4df60c7d723140d0d1bbd6ba8b34aa4e762d1138
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooassign-users-tooapplications"></a>Como tooassign usuários tooapplications

Este artigo ajuda toounderstand como os usuários são atribuídos tooan aplicativo em seu locatário.

## <a name="how-do-users-get-assigned-tooan-application-in-azure-ad"></a>Como os usuários recebem tooan aplicativo no Azure AD?

Para um usuário tooaccess um aplicativo, ele devem ser atribuídos primeiro tooit de alguma forma. Atribuição pode ser executada por um administrador, um representante de negócios ou às vezes, Olá usuário próprios. Abaixo descreve maneiras de saudação podem ser atribuídos a usuários tooapplications:

1.  Um administrador [atribui um usuário](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) toohello aplicativo diretamente

2.  Um administrador [atribui a um grupo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) usuário Olá é um membro do aplicativo toohello, incluindo:

  * Um grupo que foi sincronizado do local

  * Um grupo de segurança estático criado na nuvem Olá

  * Um [o grupo de segurança dinâmica](https://docs.microsoft.com/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal) criadas na nuvem Olá

  * Um grupo do Office 365 criado na nuvem Olá

  * Olá [todos os usuários](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-dedicated-groups) grupo

3.  Um administrador habilita [autoatendimento acesso ao aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow um tooadd de usuário usando um aplicativo hello [painel de acesso do aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Adicionar aplicativo** recurso **sem a aprovação de negócios**

4.  Um administrador habilita [autoatendimento acesso ao aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooallow um tooadd de usuário usando um aplicativo hello [painel de acesso do aplicativo](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) **Adicionar aplicativo** recurso, mas somente w **i aprovação de um conjunto selecionado de aprovadores de negócios**

5.  Um administrador habilita [gerenciamento de grupo de autoatendimento](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow toojoin um usuário um grupo de um aplicativo atribuído muito**sem a aprovação de negócios**

6.  Um administrador habilita [gerenciamento de grupo de autoatendimento](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management) tooallow toojoin um usuário um grupo de um aplicativo atribuído ao, mas apenas **com aprovação de um conjunto selecionado de aprovadores de negócios**

7.  Um administrador atribui um licença tooa usuário diretamente um primeiro aplicativo de terceiros, como [Microsoft Office 365](http://products.office.com/)

8.  Um administrador atribui um grupo de tooa de licença que Olá usuário é um membro do primeiro aplicativo de parte tooa, como [Microsoft Office 365](http://products.office.com/)

9.  Um [consentimento do administrador do aplicativo tooan](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toobe usado por todos os usuários e, em seguida, um usuário entra no aplicativo toohello

10. Um usuário [consentir aplicativos tooan](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) próprios entrando no aplicativo toohello

## <a name="next-steps"></a>Próximas etapas
[Gerenciando aplicativos com o Azure Active Directory](active-directory-enable-sso-scenario.md)
