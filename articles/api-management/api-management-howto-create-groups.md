---
title: contas de desenvolvedor aaaManage usando grupos no gerenciamento de API do Azure | Microsoft Docs
description: Saiba como desenvolvedor toomanage contas usando grupos no gerenciamento de API do Azure
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 33660b45-442f-44be-9a4a-1899d7f699b0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: c46e010e41d9705ae161dcd60d734a76d19c9e93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-use-groups-toomanage-developer-accounts-in-azure-api-management"></a>Como desenvolvedor de toomanage grupos toocreate e usar contas no gerenciamento de API do Azure
No gerenciamento de API, os grupos são usados toomanage Olá visibilidade de produtos toodevelopers. Os produtos são primeiro toogroups visíveis feitas e, em seguida, os desenvolvedores desses grupos podem exibir e assinar toohello produtos que estão associados a grupos de saudação. 

Gerenciamento de API tem Olá seguintes grupos de sistema imutável.

* **Administradores** - os administradores de assinatura do Azure são membros desse grupo. Os administradores gerenciar instâncias do serviço de gerenciamento de API, criando Olá APIs, operações e produtos que são usados pelos desenvolvedores.
* **Desenvolvedores** - usuários autenticados do portal do desenvolvedor se enquadram nesse grupo. Os desenvolvedores são clientes Olá que desenvolvem aplicativos utilizando suas APIs. Os desenvolvedores recebem o portal do desenvolvedor do access toohello e criarem aplicativos que chamar operações de saudação de uma API.
* **Convidados** -usuários portal do desenvolvedor, como clientes potenciais visitando o portal do desenvolvedor de saudação de uma queda de instância de gerenciamento de API para este grupo não autenticados. Eles podem ser concedidos determinado acesso somente leitura, como Olá capacidade tooview APIs, mas não chamá-los.

Em grupos de sistema de toothese de adição, os administradores podem criar grupos personalizados ou [aproveitar grupos externos nos locatários do Active Directory do Azure associados][leverage external groups in associated Azure Active Directory tenants]. Grupos externos e personalizados podem ser usados juntamente com grupos de sistema ao dar visibilidade a desenvolvedores e acessar tooAPI produtos. Por exemplo, você pode criar um grupo personalizado para desenvolvedores associados a uma determinada organização do parceiro e permitem acesso toohello APIs de um produto que contém apenas as APIs relevantes. Um usuário pode ser um membro de mais de um grupo.

Este guia mostra como administradores de uma instância do Gerenciamento de API podem adicionar novos grupos e associá-los a produtos e desenvolvedores.

> [!NOTE]
> Além disso toocreating e gerenciar grupos no portal do publicador hello, você pode criar e gerenciar seus grupos usando Olá API de REST de gerenciamento de API [grupo](https://msdn.microsoft.com/library/azure/dn776329.aspx) entidade.
> 
> 

## <a name="create-group"> </a>Criar um grupo
toocreate um novo grupo, clique em **portal do publicador** em hello Portal do Azure para seu serviço de gerenciamento de API. Isso leva toohello portal do publicador de gerenciamento de API.

![Portal do editor][api-management-management-console]

> Se você ainda não tiver criado uma instância do serviço de gerenciamento de API, consulte [criar uma instância do serviço de gerenciamento de API] [ Create an API Management service instance] em Olá [Introdução ao gerenciamento de API do Azure] [ Get started with Azure API Management] tutorial.
> 
> 

Clique em **grupos** de saudação **gerenciamento de API** menu saudação à esquerda e clique **adicionar grupo**.

![Adicione o novo grupo][api-management-add-group]

Insira um nome exclusivo para o grupo de saudação e uma descrição opcional e clique em **salvar**.

![Adicione o novo grupo][api-management-add-group-window]

Olá novo grupo é exibido na saudação do hello grupos na guia tooedit **nome** ou **descrição** do grupo Olá, clique o nome de saudação do grupo de saudação na lista de saudação. grupo de saudação toodelete, clique em **excluir**.

![Grupo adicionado][api-management-new-group]

Agora que hello grupo é criado, ele pode ser associado com produtos e desenvolvedores.

## <a name="associate-group-product"> </a>Associar um grupo a um produto
tooassociate um grupo com um produto, clique em **produtos** de saudação **gerenciamento de API** menu saudação à esquerda e clique em nome de saudação do produto desejado hello.

![Configurar visibilidade][api-management-add-group-to-product]

Selecione Olá **visibilidade** guia tooadd e remover grupos e tooview Olá atual de grupos de produto hello. tooadd ou remover grupos, marque ou desmarque as caixas de seleção de saudação para Olá desejado grupos e clique em **salvar**.

![Configurar visibilidade][api-management-add-group-to-product-visibility]

> [!NOTE]
> tooadd grupos do Active Directory do Azure, consulte [como desenvolvedor tooauthorize contas usando Active Directory do Azure no gerenciamento de API do Azure](api-management-howto-aad.md).
> 
> grupos de tooconfigure de saudação **visibilidade** para um produto, clique em **gerenciar grupos**.
> 
> 

Quando um produto está associado um grupo, os desenvolvedores nesse grupo podem exibir e assinar toohello produto.

## <a name="associate-group-developer"> </a>Associar grupos a desenvolvedores
grupos de tooassociate com os desenvolvedores, clique em **usuários** de saudação **gerenciamento de API** menu saudação à esquerda e, em seguida, caixa Olá de seleção ao lado de desenvolvedores Olá desejar tooassociate com um grupo.

![Adicionar toogroup de desenvolvedor][api-management-add-group-to-developer]

Depois de saudação desejado desenvolvedores são verificados, clique em grupo desejado de saudação em hello **adicionar tooGroup** lista suspensa. Os desenvolvedores podem ser removidos dos grupos usando Olá **remover do grupo** lista suspensa. 

![Desenvolvedores][api-management-add-group-to-developer-saved]

Depois que a associação Olá é adicionada entre desenvolvedor hello e grupo hello, você pode exibi-lo no hello **usuários** guia.

## <a name="next-steps"> </a>Próximas etapas
* Depois que um desenvolvedor é adicionado tooa grupo, eles podem exibir e assinar toohello produtos associados ao grupo. Para obter mais informações, consulte [Como criar e publicar um produto no Gerenciamento de API do Azure][How create and publish a product in Azure API Management],
* Além disso toocreating e gerenciar grupos no portal do publicador hello, você pode criar e gerenciar seus grupos usando Olá API de REST de gerenciamento de API [grupo](https://msdn.microsoft.com/library/azure/dn776329.aspx) entidade.

[api-management-management-console]: ./media/api-management-howto-create-groups/api-management-management-console.png
[api-management-add-group]: ./media/api-management-howto-create-groups/api-management-add-group.png
[api-management-add-group-window]: ./media/api-management-howto-create-groups/api-management-add-group-window.png
[api-management-new-group]: ./media/api-management-howto-create-groups/api-management-new-group.png
[api-management-add-group-to-product]: ./media/api-management-howto-create-groups/api-management-add-group-to-product.png
[api-management-add-group-to-product-visibility]: ./media/api-management-howto-create-groups/api-management-add-group-to-product-visibility.png
[api-management-add-group-to-developer]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer.png
[api-management-add-group-to-developer-saved]: ./media/api-management-howto-create-groups/api-management-add-group-to-developer-saved.png

[api-management-]: ./media/api-management-howto-create-groups/api-management-.png

[Create a group]: #create-group
[Associate a group with a product]: #associate-group-product
[Associate groups with developers]: #associate-group-developer
[Next steps]: #next-steps

[How create and publish a product in Azure API Management]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[leverage external groups in associated Azure Active Directory tenants]: api-management-howto-aad.md#how-to-add-an-external-azure-active-directory-group
