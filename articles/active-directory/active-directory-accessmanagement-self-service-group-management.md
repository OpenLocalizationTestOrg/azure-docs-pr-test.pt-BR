---
title: "aaaSetting o Azure Active Directory para o gerenciamento de acesso do aplicativo de serviço de autoatendimento | Microsoft Docs"
description: "Gerenciamento de grupo de autoatendimento permite que usuários toocreate e gerenciar grupos de segurança ou grupos do Office 365 no Active Directory do Azure e o grupo de segurança do ofertas usuários Olá possibilidade toorequest ou associações de grupo do Office 365"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 904d5c70-c34a-46c4-a9a7-d1efecf4821c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/27/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 2a73f4ed2532d41143fe5abe2fef1322d971a5c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-azure-active-directory-for-self-service-group-management"></a>Configuração do Azure Active Directory para gerenciamento de grupo de autoatendimento
Gerenciamento de grupo de autoatendimento permite que usuários toocreate e gerenciar grupos de segurança ou grupos do Office 365 no Azure Active Directory (AD do Azure). Os usuários também podem solicitar o grupo de segurança ou associações de grupo do Office 365, e, em seguida, hello proprietário do grupo de saudação pode aprovar ou negar associação. Dessa forma, controle diário de associação de grupo pode ser delegada toopeople que compreendem o contexto de negócios Olá para essa associação. Os recursos de gerenciamento de grupo de autoatendimento só estão disponíveis para grupos de segurança e para grupos do Office 365, mas não para grupos de segurança habilitados para email ou listas de distribuição.

> [!IMPORTANT]
> A Microsoft recomenda que você gerencie o AD do Azure usando Olá [Centro de administração do AD do Azure](https://aad.portal.azure.com) em Olá portal do Azure em vez de usar Olá portal clássico do Azure mencionado neste artigo.

Atualmente, o gerenciamento de grupo de autoatendimento é composto de dois cenários essenciais:gerenciamento de grupo delegado e gerenciamento de grupo de autoatendimento.

* **Gerenciamento de grupo delegado** um exemplo é um administrador que está gerenciando o aplicativo de SaaS do tooa acesso Olá empresa está usando. O gerenciamento desses direitos de acesso está se tornando um incômodo, portanto, esse administrador solicita Olá business proprietário toocreate um novo grupo. Olá administrador atribui acesso para o novo grupo de saudação aplicativo toohello e adiciona o grupo de toohello todas as pessoas que já acessam o aplicativo toohello. os proprietários de negócios Hello, em seguida, podem adicionar mais usuários e os usuários são automaticamente provisionados toohello aplicativo. os proprietários de negócios Olá não precisam toowait Olá toomanage para acesso de administrador para os usuários. Se Olá administrador concede Olá mesmo Gerenciador de tooa de permissão em um grupo de negócios diferente, em seguida, essa pessoa também pode gerenciar o acesso para seus próprios usuários. Proprietário da empresa hello, nem manager Olá pode exibir ou gerenciar uns dos outros usuários. administrador de saudação ainda pode ver todos os usuários que têm acesso toohello aplicativo e direitos de acesso de bloco, se necessário.
* **Gerenciamento de grupo de autoatendimento** Um exemplo deste cenário consiste em dois usuários que têm sites do SharePoint Online que eles configuram de forma independente. Eles querem toogive cada de outras equipes acesso tootheir sites. tooaccomplish isso, eles podem criar um grupo no AD do Azure e no SharePoint Online cada um deles seleciona o grupo tooprovide acesso tootheir sites. Quando alguém deseja acesso, eles solicitação-lo da saudação painel de acesso e depois de aprovado obtém acesso de sites do SharePoint Online tooboth automaticamente. Posteriormente, um deles decide que todas as pessoas acessam Olá site também devem obter acesso tooa determinado aplicativo SaaS. administrador de saudação do hello aplicativo SaaS pode adicionar direitos de acesso para o site do SharePoint Online de toohello do aplicativo hello. Daí em seguida diante, todas as solicitações tiverem aprovadas dá acesso toohello dois sites SharePoint Online e também toothis aplicativo SaaS.

## <a name="making-a-group-available-for-end-user-self-service"></a>Disponibilização de um grupo para o usuário final de autoatendimento
1. Em Olá [portal clássico do Azure](https://manage.windowsazure.com), abra o diretório do AD do Azure.
2. Em Olá **configurar** guia, defina **gerenciamento de grupo delegado** tooEnabled.
3. Definir **os usuários podem criar grupos de segurança** ou **os usuários podem criar grupos do Office** tooEnabled.

Quando **os usuários podem criar grupos de segurança** é habilitada, todos os usuários em seu diretório são permitidos toocreate novos grupos de segurança e adicionar membros a grupos de toothese. Esses novos grupos também deverão aparecer no hello painel de acesso para todos os outros usuários. Se a configuração de política de saudação no grupo de saudação permitir, outros usuários podem criar solicitações toojoin esses grupos. Se a opção **Os usuários podem criar grupos de segurança** for desabilitada, os usuários não poderão criar grupos nem alterar grupos existentes dos quais são proprietários. No entanto, ainda podem gerenciar associações Olá desses grupos e aprovar solicitações de outros usuários toojoin seus grupos.

Você também pode usar **os usuários que podem usar o autoatendimento para grupos de segurança** tooachieve um controle de acesso mais refinado sobre o gerenciamento de grupo de autoatendimento para seus usuários. Quando **os usuários podem criar grupos** é habilitada, todos os usuários em seu diretório são permitidos toocreate novos grupos e adicionar membros a grupos de toothese. Definindo também **os usuários que podem usar o autoatendimento para grupos de segurança** tooSome, você está restringindo tooonly de gerenciamento de grupo a um grupo limitado de usuários. Quando essa opção é definida tooSome, você deve adicionar o grupo de usuários do toohello SSGMSecurityGroupsUsers antes de criar novos grupos e adicionar membros toothem. Definindo **os usuários que podem usar o autoatendimento para grupos de segurança** tooAll, habilitar todos os usuários em seus novos grupos do diretório toocreate.

Você também pode usar o hello **grupo que pode usar o autoatendimento para grupos de segurança** toospecify um nome personalizado para um grupo cujos membros podem usar o autoatendimento de caixa.

## <a name="next-steps"></a>Próximas etapas
Esses artigos fornecem mais informações sobre o Active Directory do Azure.

* [Gerenciando acesso tooresources com grupos do Active Directory do Azure](active-directory-manage-groups.md)
* [Cmdlets do Azure Active Directory para definir configurações de grupo](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure](active-directory-apps-index.md)
* [O que é o Active Directory do Azure?](active-directory-whatis.md)
* [Integração de suas identidades locais com o Active Directory do Azure](active-directory-aadconnect.md)
