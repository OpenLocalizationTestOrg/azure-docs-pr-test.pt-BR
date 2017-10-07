---
title: grupos de aaaDedicated no Active Directory do Azure | Microsoft Docs
description: "Visão geral do funcionamento e da criação de grupos dedicados no Active Directory do Azure."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 86158909-083a-41fe-8090-955e96ad1865
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: 8feec6e1a4e6b384470392d3043caeeec2b03dd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="dedicated-groups-in-azure-active-directory"></a>Grupos dedicados no Active Directory do Azure
No Azure Active Directory (AD do Azure), o recurso de grupos dedicados Olá automaticamente cria e preenche a associação de grupos predefinido do AD do Azure. Membros de grupos dedicados não podem ser adicionados ou removido usando hello Azure clássico portal, cmdlets do Windows PowerShell, ou programaticamente.

> [!NOTE]
> Grupos dedicados requerem que uma licença do Azure AD Premium seja atribuída ao
>
> * administrador de saudação que gerencia a regra Olá em um grupo
> * todos os usuários que são selecionados por Olá toobe um membro do grupo de saudação de regra
>
>

**grupos de tooenable dedicado**

1. Em Olá [portal clássico do Azure](https://manage.windowsazure.com), selecione **do Active Directory**e, em seguida, abra o diretório da sua organização.
2. Selecione Olá **grupos** guia e grupo hello, em seguida, abra tooedit desejado.
3. Selecione Olá **configurar** guia e, em seguida, defina **habilitar grupos dedicados** muito**Sim**.

Depois de saudação alternar habilitar grupos dedicados está definida muito**Sim**, você pode habilitar Olá diretório tooautomatically criar grupo dedicado de todos os usuários de saudação por configuração Olá **habilitar "Todos os usuários" grupo** Alternar muito**Sim**. Você pode também editar nome hello desse grupo dedicado digitando-o em hello **nome para exibição para "Todos os usuários" grupo** campo.

grupo de todos os usuários Olá pode ser usado tooassign Olá mesmo permissões tooall Olá os usuários em seu diretório. Por exemplo, você pode conceder a todos os usuários no seu acesso de diretório tooa aplicativo SaaS, atribuindo acesso Olá grupo dedicado de todos os usuários toothis de aplicativo.

grupo de todos os usuários Olá dedicado inclui todos os usuários no diretório hello, inclusive convidados e usuários externos. Se você precisar de um grupo que exclui os usuários externos, você pode fazer isso criando um grupo com uma regra dinâmica baseada em atributo como seguinte Olá:

                (user.userPrincipalName -notContains "#EXT#@")

Para um grupo que exclui todos os convidados, use uma regra, como a seguir hello:

                (user.userType -ne "Guest")

toolearn sobre como toocreate *avançados* regra (regras que podem conter várias comparações) para a associação de grupo dinâmico, consulte [usar atributos toocreate regras avançadas](active-directory-accessmanagement-groups-with-advanced-rules.md).

### <a name="next-steps"></a>Próximas etapas
Esses artigos fornecem mais informações sobre o Active Directory do Azure.

* [Gerenciando acesso tooresources com grupos do Active Directory do Azure](active-directory-manage-groups.md)
* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](active-directory-apps-index.md)
* [O que é o Active Directory do Azure?](active-directory-whatis.md)
* [Integração de suas identidades locais com o Active Directory do Azure](active-directory-aadconnect.md)
