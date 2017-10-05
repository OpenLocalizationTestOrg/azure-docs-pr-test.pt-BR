---
title: Usar um grupo para gerenciar o acesso a aplicativos SaaS| Microsoft Docs
description: "Como usar grupos no Azure Active Directory Premium ou Basic para atribuir acesso a aplicativos SaaS que estão integrados ao Azure Active Directory."
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
ms.openlocfilehash: d350011ee9fc5ced9ddb16993f68d3c840a645a5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="using-a-group-to-manage-access-to-saas-applications"></a>Usar um grupo para gerenciar o acesso a aplicativos SaaS
Usando o Azure AD (Azure Active Directory) com a licença do Azure AD Premium ou do Azure AD Basic, você pode usar grupos para atribuir acesso a um aplicativo SaaS que esteja integrado ao Azure AD. Por exemplo, se você quiser atribuir acesso ao departamento de marketing usar cinco aplicativos SaaS diferentes, você pode criar um grupo que contém os usuários no departamento de marketing e atribuir esse grupo a esses cinco aplicativos SaaS que são necessários para o departamento de marketing. Dessa forma, você pode poupar tempo gerenciando a associação no departamento de marketing em um único lugar. Os usuários são atribuídos ao aplicativo quando eles são adicionados como membros do grupo de marketing, e sua atribuição é removida do aplicativo quando eles são removidos do grupo de marketing.

> [!IMPORTANT]
> A Microsoft recomenda que você gerencie o Azure AD usando o [Centro de administração do AD do Azure](https://aad.portal.azure.com) no portal do Azure em vez de usar o portal clássico do Azure mencionado neste artigo. 

Esse recurso pode ser usado com centenas de aplicativos que você adiciona na Galeria de aplicativos do Azure AD.

**Para atribuir acesso de um grupo a um aplicativo SaaS**

1. No [portal clássico do Azure](https://manage.windowsazure.com), selecione **Active Directory** na barra de navegação à esquerda.
2. Selecione a guia **Diretório** e abra o diretório no qual você deseja atribuir o acesso de um grupo a um aplicativo SaaS.
3. Selecione a guia **Aplicativos** . Selecione um aplicativo que você adicionou da Galeria de Aplicativos e clique na guia **Usuários e Grupos**.
4. Na guia **Usuários e Grupos**, no campo **Iniciando com**, insira o nome do grupo ao qual você deseja atribuir acesso e escolha a de seleção no canto superior direito. Você só precisa digitar a primeira parte do nome do grupo.
5. Selecione o grupo e selecione o botão **Atribuir Acesso** . Selecione **Sim** quando visualizar a mensagem de confirmação. No momento, as associações de grupo aninhadas não têm suporte para atribuição com base em grupo de aplicativos.
6. Você também pode ver quais usuários são atribuídos ao aplicativo, diretamente ou por associação em um grupo. Para fazer isso, altere **Mostrar lista suspensa de “Grupos”** para **“Todos os Usuários”**. A lista mostra usuários no diretório e se cada usuário está ou não atribuído ao aplicativo. A lista também mostra se os usuários atribuídos estão atribuídos diretamente ao aplicativo (tipo de atribuição mostrado como "Direto"), ou por meio de associação de grupo (tipo de atribuição mostrado como "Herdado".)

> [!NOTE]
> Você pode ver a guia Usuários e Grupos somente depois que tiver habilitado Azure AD Premium e Azure AD Basic.
>
>

### <a name="next-steps"></a>Próximas etapas
Esses artigos fornecem mais informações sobre o Active Directory do Azure.

* [Gerenciamento de acesso a recursos com grupos do Active Directory do Azure](active-directory-manage-groups.md)
* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](active-directory-apps-index.md)
* [Cmdlets do Azure Active Directory para definir configurações de grupo](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [O que é o Active Directory do Azure?](active-directory-whatis.md)
* [Integração de suas identidades locais com o Active Directory do Azure](active-directory-aadconnect.md)
