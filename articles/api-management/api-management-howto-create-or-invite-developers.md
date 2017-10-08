---
title: "aaaHow gerenciar contas de usuário no gerenciamento de API do Azure | Microsoft Docs"
description: "Saiba como toocreate ou convidar usuários no gerenciamento de API do Azure"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 078abfa5-1e4f-4c9d-b9c7-a172bd19c1a2
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 3966f4454e29621d7c615beefee352ec91b48b2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-user-accounts-in-azure-api-management"></a>Como contas de usuário toomanage no gerenciamento de API do Azure
No gerenciamento de API, os desenvolvedores são usuários Olá Olá APIs que você expõe usando gerenciamento de API. Este guia mostra toohow toocreate e convidar os desenvolvedores toouse hello APIs e produtos que você faça toothem disponível com sua instância de gerenciamento de API. Para obter informações sobre como gerenciar contas de usuário por meio de programação, consulte Olá [entidade usuário](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentação Olá [API REST de gerenciamento](https://msdn.microsoft.com/library/azure/dn776326.aspx) referência.

## <a name="create-developer"> </a>Criar um novo desenvolvedor
toocreate um desenvolvedor de novo, clique em **portal do publicador** em hello Portal do Azure para seu serviço de gerenciamento de API. Isso leva toohello portal do publicador de gerenciamento de API. Se você ainda não tiver criado uma instância do serviço de gerenciamento de API, consulte [criar uma instância do serviço de gerenciamento de API] [ Create an API Management service instance] em Olá [Introdução ao gerenciamento de API do Azure] [ Get started with Azure API Management] tutorial.

![Portal do editor][api-management-management-console]

Clique em **usuários** de saudação **gerenciamento de API** menu saudação à esquerda e clique **adicionar usuário**.

![Criar desenvolvedor][api-management-create-developer]

Digite hello **Email**, **senha**, e **nome** para desenvolvedor novo hello e clique em **salvar**.

![Criar desenvolvedor][api-management-add-new-user]

Por padrão, são contas de desenvolvedor recém-criado **Active**e associado Olá **desenvolvedores** grupo.

![Novo desenvolvedor][api-management-new-developer]

Contas de desenvolvedor que estão em um **active** estado pode ser usado tooaccess todos os APIs Olá para os quais têm assinaturas. desenvolvedor de saudação recém-criado tooassociate grupos adicionais, consulte [como os grupos de tooassociate com os desenvolvedores][How tooassociate groups with developers].

## <a name="invite-developer"> </a>Convidar um desenvolvedor
tooinvite um desenvolvedor, clique em **usuários** de saudação **gerenciamento de API** menu saudação à esquerda e clique **convidar usuário**.

![Convidar desenvolvedor][api-management-invite-developer]

Digite hello nome e endereço de email do desenvolvedor Olá e clique em **convidar**.

![Convidar desenvolvedor][api-management-invite-developer-window]

Será exibida uma mensagem de confirmação, mas o desenvolvedor Olá recentemente convidado não aparecem na lista de saudação até depois de aceitar o convite de saudação. 

![Confirmação de convite][api-management-invite-developer-confirmation]

Quando um desenvolvedor é convidado, é enviado um email toohello developer. O email é gerado utilizando um modelo e pode ser personalizado. Para obter mais informações, consulte [Configurar modelos de email][Configure email templates].

Quando Olá convite é aceito, conta Olá fica ativa.

## <a name="block-developer"> </a> Desativar ou reativar uma conta de desenvolvedor
Por padrão, as contas de desenvolvedor criadas ou convidadas recentemente têm o estado **Ativa**. Clique em toodeactivate uma conta de desenvolvedor, **bloco**. tooreactivate uma conta de desenvolvedor bloqueado, clique em **ativar**. Uma conta de desenvolvedor bloqueados não pode acessar o portal do desenvolvedor hello ou chamar quaisquer APIs. toodelete uma conta de usuário, clique em **excluir**.

![Bloquear desenvolvedor][api-management-new-developer]

## <a name="reset-a-user-password"></a>Redefinir a senha de um usuário
senha de saudação tooreset para uma conta de usuário, clique o nome de saudação da conta de saudação.

![Redefinir senha][api-management-view-developer]

Clique em **Redefinir senha** toosend um tooreset de usuário do link toohello sua senha.

![Redefinir senha][api-management-reset-password]

trabalho tooprogrammatically com contas de usuário, consulte Olá [entidade usuário](https://msdn.microsoft.com/library/azure/dn776330.aspx) documentação Olá [API REST de gerenciamento](https://msdn.microsoft.com/library/azure/dn776326.aspx) referência. tooreset um valor específico do usuário conta senha tooa, você pode usar o hello [atualizar um usuário](https://msdn.microsoft.com/library/azure/dn776330.aspx#UpdateUser) operação e especifique a senha desejada hello.

## <a name="pending-verification"></a>Verificação pendente
![Verificação pendente][api-management-pending-verification]

## <a name="next-steps"> </a>Próximas etapas
Depois de criar uma conta de desenvolvedor, você pode associá-lo com as funções e inscrevê-lo tooproducts e APIs. Para obter mais informações, consulte [como toocreate e use grupos][How toocreate and use groups].

[api-management-management-console]: ./media/api-management-howto-create-or-invite-developers/api-management-management-console.png
[api-management-add-new-user]: ./media/api-management-howto-create-or-invite-developers/api-management-add-new-user.png
[api-management-create-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-create-developer.png
[api-management-invite-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer.png
[api-management-new-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-new-developer.png
[api-management-invite-developer-window]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer-window.png
[api-management-invite-developer-confirmation]: ./media/api-management-howto-create-or-invite-developers/api-management-invite-developer-confirmation.png
[api-management-pending-verification]: ./media/api-management-howto-create-or-invite-developers/api-management-pending-verification.png
[api-management-view-developer]: ./media/api-management-howto-create-or-invite-developers/api-management-view-developer.png
[api-management-reset-password]: ./media/api-management-howto-create-or-invite-developers/api-management-reset-password.png


[Create a new developer]: #create-developer
[Invite a developer]: #invite-developer
[Deactivate or reactivate a developer account]: #block-developer
[Next steps]: #next-steps
[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Configure email templates]: api-management-howto-configure-notifications.md#email-templates
