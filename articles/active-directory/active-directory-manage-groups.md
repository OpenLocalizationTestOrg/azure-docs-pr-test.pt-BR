---
title: grupos de aaaUse toomanage tooresources de acesso no Active Directory do Azure | Microsoft Docs
description: "Como toouse grupos de usuário do Active Directory do Azure toomanage acessam recursos e aplicativos de nuvem e tooon local."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 714120d0-cdf9-465d-afee-39bef591c6b3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 876a356c8095505432e9346721f35c7943819e9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-access-tooresources-with-azure-active-directory-groups"></a>Gerenciar acesso tooresources com grupos do Active Directory do Azure
Azure Active Directory (AD do Azure) é uma solução de gerenciamento abrangente para acesso e identidade que fornece um conjunto robusto de recursos, incluindo serviços online da Microsoft como o Office 365 e aplicativos de nuvem e recursos toomanage tooon acesso local e um mundo de aplicativos SaaS de Microsoft. Este artigo fornece uma visão geral, mas se você quiser toostart usando o Azure AD de grupos no momento, siga as instruções de saudação em [Gerenciando grupos de segurança no AD do Azure](active-directory-accessmanagement-manage-groups.md). Se você quiser toosee como você pode usar o PowerShell toomanage grupos no Azure Active directory, você pode ler mais em [cmdlets do Active Directory do Azure para gerenciamento de grupo](active-directory-accessmanagement-groups-settings-v2-cmdlets.md).

> [!NOTE]
> toouse Active Directory do Azure, você precisa de uma conta do Azure. Se você ainda não tem uma conta, você pode [inscrever-se para uma conta gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
>
>

No AD do Azure, um dos principais recursos de saudação é Olá capacidade toomanage acesso tooresources. Esses recursos podem fazer parte do diretório hello, como no caso de saudação de objetos de toomanage permissões por meio de funções no diretório de hello, ou recursos de diretório toohello externo, como aplicativos SaaS, os serviços do Azure e sites do SharePoint ou no local recursos. Há quatro maneiras que um usuário pode receber recursos de tooa de direitos de acesso:

1. Atribuição direta

    Os usuários podem ser atribuídos diretamente tooa recurso pelo proprietário de saudação do recurso.
2. Associação de grupo

    Um grupo pode ser atribuído tooa recurso pelo proprietário do recurso de saudação e por isso, concedendo membros de saudação do recurso grupo acesso toohello. Associação de grupo hello, em seguida, pode ser gerenciada pelo proprietário de saudação do grupo de saudação. Efetivamente, delegados de proprietário do recurso Olá Olá permissão tooassign usuários tootheir toohello proprietário do recurso de grupo de saudação.
3. Com base em regra

    proprietário do recurso Olá pode usar um tooexpress regra quais usuários devem receber acesso tooa recursos. resultado de saudação da regra Olá depende Olá atributos usados na regra e seus valores para usuários específicos e fazendo isso, o proprietário do recurso de saudação delega efetivamente Olá toomanage direito acesso tootheir recurso toohello origem autoritativa de saudação atributos que são usados na regra de saudação. proprietário do recurso Olá ainda gerencia regra Olá em si e determina quais atributos e valores de fornecem acesso tootheir recursos.
4. Autoridade externa

    recurso de tooa acesso Olá é derivado de uma fonte externa; Por exemplo, um grupo que é sincronizado por meio de uma fonte autoritativa como um diretório local ou um aplicativo SaaS, como o dia de trabalho. proprietário do recurso Olá atribui o recurso de toohello Olá grupo tooprovide acesso e a origem externa Olá gerencia membros de saudação do grupo de saudação.

   ![Visão geral do diagrama de gerenciamento de acesso](./media/active-directory-access-management-groups/access-management-overview.png)

## <a name="watch-a-video-that-explains-access-management"></a>Assista a um vídeo que explica o gerenciamento de acesso
Você pode assistir a um breve vídeo que explica mais sobre isso:

**AD do Azure: Associação de toodynamic introdução para grupos**

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-AD--Introduction-to-Dynamic-Memberships-for-Groups/player]
>
>

## <a name="how-does-access-management-in-azure-active-directory-work"></a>Como funciona o gerenciamento de acesso no Azure Active Directory?
Em Olá Centro de saudação solução de gerenciamento de acesso do AD do Azure é o grupo de segurança hello. Usar um tooresources de acesso de toomanage de grupo de segurança é um paradigma conhecido, que permite que um recurso de tooa maneira flexível e fácil de entender tooprovide acesso de grupo Olá pretendido de usuários. proprietário do recurso de saudação (ou o administrador de saudação do diretório Olá) pode atribuir tooprovide um grupo um determinados recursos de toohello direito acesso que eles possuem. membros de saudação do grupo de saudação terão acesso hello e proprietário do recurso Olá pode delegar a lista de membros de Olá Olá toomanage à direita de uma pessoa, como um gerente de departamento ou um administrador de assistência técnica de toosomeone de grupo.

![Diagrama de gerenciamento de acesso do Active Directory do Azure](./media/active-directory-access-management-groups/active-directory-access-management-works.png)

proprietário de saudação de um grupo também pode disponibilizar esse grupo para solicitações de autoatendimento. Dessa forma, um usuário final pode procurar e localizar o grupo de saudação e fazer uma solicitação toojoin, efetivamente procurando recursos de saudação do permissão tooaccess que são gerenciados pelo grupo de saudação. proprietário de saudação do grupo de saudação pode configurar grupo de saudação para que as solicitações de associação são aprovadas automaticamente ou exigem aprovação por proprietário de saudação do grupo de saudação. Quando um usuário faz uma solicitação toojoin um grupo, a solicitação de junção de saudação é encaminhada toohello proprietários do grupo de saudação. Se um dos proprietários Olá Aprovar solicitação de hello, notificará o usuário solicitante hello e usuário Olá é toohello ingressado no grupo. Se um dos proprietários Olá Negar solicitação hello, usuário solicitante Olá é notificado, mas não ingressados no grupo toohello.

## <a name="getting-started-with-access-management"></a>Introdução ao gerenciamento de acesso
Pronto tooget iniciado? Tente algumas das tarefas básicas hello, que você pode fazer com grupos do AD do Azure. Use esses recursos tooprovide especializado acessar toodifferent grupos de pessoas diferentes recursos em sua organização. Uma lista das primeiras etapas básicas é exibida abaixo.

* [Criar uma regra simples tooconfigure da associação dinâmica de um grupo](active-directory-accessmanagement-manage-groups.md#how-can-i-manage-the-membership-of-a-group-dynamically)
* [Usando um grupo toomanage tooSaaS os aplicativos access](active-directory-accessmanagement-group-saasapps.md)
* [Disponibilização de um grupo para autoatendimento do usuário final](active-directory-accessmanagement-self-service-group-management.md)
* [Sincronizando um tooAzure de grupo local usando o Azure AD Connect](active-directory-aadconnect.md)
* [Gerenciando proprietários de um grupo](active-directory-accessmanagement-managing-group-owners.md)

## <a name="next-steps"></a>Próximas etapas
Agora que você entendeu Noções básicas de saudação do gerenciamento de acesso aqui estão alguns recursos avançados adicionais disponíveis no Azure Active Directory para gerenciar o acesso tooyour aplicativos e recursos.

* [Usando atributos toocreate regras avançadas](active-directory-accessmanagement-groups-with-advanced-rules.md)
* [Gerenciamento de grupos de segurança no Azure AD](active-directory-accessmanagement-manage-groups.md)
* [Configuração de grupos dedicados no Azure AD](active-directory-accessmanagement-dedicated-groups.md)
* [Referência de API do Graph para grupos](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/groups-operations#GroupFunctions)
* [Cmdlets do Azure Active Directory para definir configurações de grupo](active-directory-accessmanagement-groups-settings-cmdlets.md)
