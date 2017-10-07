---
title: aaaUsing tooSaaS de acesso de toomanage um grupo aplicativos | Microsoft Docs
description: "Como os grupos de toouse no Azure Active Directory Premium ou básica tooassign acessar tooSaaS aplicativos integrados ao Active Directory do Azure."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: ab8dee63-bedc-46ca-8852-234f5c16ae98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.reviewer: piotrci
ms.custom: it-pro;oldportal
ms.openlocfilehash: f45ea4472b3d88e8ea514af3db31b4cc9ea68d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-a-group-toomanage-access-toosaas-applications"></a>Usando um grupo toomanage tooSaaS os aplicativos access
Usando o Azure Active Directory (AD do Azure) com uma licença Azure AD Premium ou Azure AD Basic, você pode usar grupos tooassign acesso tooa aplicativo SaaS que esteja integrado ao AD do Azure. Por exemplo, se você quiser acesso tooassign Olá marketing departamento toouse cinco aplicativos SaaS diferentes, você pode criar um grupo que contém usuários Olá no departamento de marketing Olá e, em seguida, atribuir esse grupo toothese cinco aplicativos SaaS que são necessárias pelo departamento de marketing hello. Dessa forma você pode poupar tempo gerenciando participação Olá Olá marketing departamento em um único local. Em seguida, os usuários recebem toohello aplicativo quando eles são adicionados como membros do grupo marketing hello e sua atribuição é removida do aplicativo hello quando eles são removidos do grupo de marketing de saudação.

> [!IMPORTANT]
> A Microsoft recomenda que você gerencie o AD do Azure usando Olá [Centro de administração do AD do Azure](https://aad.portal.azure.com) em Olá portal do Azure em vez de usar Olá portal clássico do Azure mencionado neste artigo. 

Esse recurso pode ser usado com centenas de aplicativos que você adiciona da Olá Galeria de aplicativos do Azure AD.

**acesso de tooassign para um grupo de tooa aplicativo SaaS**

1. Em Olá [portal clássico do Azure](https://manage.windowsazure.com), selecione **do Active Directory** na barra de navegação Olá Olá esquerda.
2. Selecione Olá **diretório** guia e diretório Olá aberto, em seguida, no qual você deseja acesso de tooassign para um grupo de tooa aplicativo SaaS.
3. Selecione Olá **aplicativos** guia. Selecione um aplicativo que você adicionou da saudação Galeria de aplicativos e, em seguida, clique em Olá **usuários e grupos** guia.
4. Em Olá **usuários e grupos** guia Olá **começando com** , digite o nome da saudação de saudação grupo toowhich você deseja acesso tooassign e, em seguida, selecione Olá marca de seleção no canto superior direito de saudação. Você só precisa tootype Olá primeira parte do nome do grupo.
5. Selecione o grupo de hello, em seguida, em seguida, Olá **atribuir acesso** botão. Selecione **Sim** quando você vir a mensagem de confirmação de saudação. Associações de grupo aninhado não há suporte para a atribuição baseada em grupo tooapplications neste momento.
6. Você também pode ver quais usuários são atribuídos toohello aplicativo, seja diretamente ou por associação em um grupo. toodo, Olá alteração **Mostrar lista suspensa de 'Grupos'** muito**'Todos os usuários'**. lista de saudação mostra usuários no diretório de saudação e se deseja ou não é atribuída a cada usuário toohello aplicativo. lista de saudação também mostra se usuários Olá atribuído são atribuídos diretamente aplicativo toohello (tipo de atribuição mostrado como "Direto"), ou por meio de associação de grupo (tipo de atribuição mostrado como 'Herdado'.)

> [!NOTE]
> Você pode ver hello usuários e guia grupos somente depois que você tiver ativado o Azure AD Premium ou Azure AD Basic.
>
>

### <a name="next-steps"></a>Próximas etapas
Esses artigos fornecem mais informações sobre o Active Directory do Azure.

* [Gerenciando acesso tooresources com grupos do Active Directory do Azure](active-directory-manage-groups.md)
* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](active-directory-apps-index.md)
* [Cmdlets do Azure Active Directory para definir configurações de grupo](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [O que é o Active Directory do Azure?](active-directory-whatis.md)
* [Integração de suas identidades locais com o Active Directory do Azure](active-directory-aadconnect.md)
