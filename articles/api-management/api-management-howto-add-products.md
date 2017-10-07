---
title: aaaHow toocreate e publicar um produto no gerenciamento de API do Azure
description: Saiba como toocreate e publicar produtos no gerenciamento de API do Azure.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 31de55cb-9384-490b-a2f2-6dfcf83da764
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: f0a37f08b4e29ca68be9caec4c7604e3b4b6aaa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-publish-a-product-in-azure-api-management"></a>Como toocreate e publicar um produto no gerenciamento de API do Azure
No gerenciamento de API do Azure, um produto contém um ou mais APIs, bem como em termos de cota e hello de uso de uso. Depois que um produto é publicado, os desenvolvedores podem assinar toohello produto e começar a APIs do produto do toouse hello. tópico de Olá fornece um guia toocreating um produto, a adição de uma API e publicá-la para desenvolvedores.

## <a name="create-product"> </a>Criar um produto
As operações são adicionadas e configurados tooan API no portal do publicador Olá. tooaccess Olá clique portal, publisher **portal do publicador** em hello Portal do Azure para seu serviço de gerenciamento de API.

![Portal do editor][api-management-management-console]

> Se você ainda não tiver criado uma instância do serviço de gerenciamento de API, consulte [criar uma instância do serviço de gerenciamento de API] [ Create an API Management service instance] em Olá [Introdução ao gerenciamento de API do Azure] [ Get started with Azure API Management] tutorial.
> 
> 

Clique em **produtos** na menu Olá Olá toodisplay esquerdo Olá **produtos** página e, em seguida, clique em **adicionar produto**.

![Produtos][api-management-products]

![Novo produto][api-management-add-new-product]

Insira um nome descritivo para o produto de saudação em Olá **nome** campo e uma descrição de produto Olá Olá **descrição** campo.

Produtos de Gerenciamento de API podem ser **Livres** ou **Protegidos**. Produtos protegidos devem ser assinado toobefore, eles podem ser usados, ao abrir produtos podem ser usados sem uma assinatura. Verificar **exigir assinatura** toocreate um produto protegido que requer uma assinatura. Essa é a configuração de padrão de saudação.

Verificar **exigirem a aprovação de assinatura** se você deseja que um administrador tooreview e aceitar ou rejeitar assinatura tentativas toothis produto. Se Olá caixa está desmarcada, tentativas de assinatura serão aprovadas automaticamente. Para obter mais informações sobre assinaturas, consulte [produto do modo de exibição assinantes tooa][View subscribers tooa product].

toosubscribe contas de desenvolvedor tooallow produto de toohello várias vezes, verifique Olá **permitir várias assinaturas** caixa de seleção. Se essa caixa não estiver marcada, cada conta de desenvolvedor pode inscrever-se apenas um produto de toohello única vez.

![Várias assinaturas ilimitadas][api-management-unlimited-multiple-subscriptions]

Contagem de saudação toolimit de várias assinaturas simultâneas, verifique Olá **limitar o número de assinaturas simultâneas para** caixa de seleção e insira o limite de assinatura de saudação. Em Olá exemplo a seguir, assinaturas simultâneas são toofour limitado por conta de desenvolvedor.

![Quatro assinaturas][api-management-four-multiple-subscriptions]

Depois que todas as novas opções de produto são configuradas, clique em **salvar** novo produto do toocreate hello.

![Produtos][api-management-products-page]

> Por padrão novos produtos são não publicados e são visível toohello somente **administradores** grupo.
> 
> 

tooconfigure um produto, clique no nome do produto de saudação em Olá **produtos** guia.

## <a name="add-apis"></a>Produto de tooa adicionar APIs
Olá **produtos** página contém quatro links para a configuração: **resumo**, **configurações**, **visibilidade**, e  **Os assinantes**. Olá **resumo** guia é onde você pode adicionar APIs e publicar ou cancelar a publicação de um produto.

![Resumo][api-management-new-product-summary]

Antes de publicar seu produto é necessário tooadd uma ou mais APIs. toodo, clique **tooproduct adicionar API**.

![Adicionar APIs][api-management-add-apis-to-product]

Selecione Olá desejado APIs e clique em **salvar**.

## <a name="add-description"></a>Produto do adicionar informações descritivas tooa
Olá **configurações** guia permite que você tooprovide informações detalhadas sobre o produto hello como sua finalidade, Olá APIs que fornece acesso a e outras informações úteis. conteúdo de saudação é destinado a desenvolvedores Olá que serão chamado hello API e podem ser gravados em texto sem formatação ou marcação HTML.

![Configurações do produto][api-management-product-settings]

Verificar **exigir assinatura** toocreate um produto protegido que requer um toobe de assinatura usado ou desmarque Olá toocreate da caixa de seleção um produto aberto que pode ser chamado sem uma assinatura.

Selecione **exigirem a aprovação de assinatura** se você quiser toomanually aprovar todas as solicitações de assinatura de produto. Por padrão, todas as assinaturas de produto são aprovadas automaticamente.

toosubscribe contas de desenvolvedor tooallow produto de toohello várias vezes, verifique Olá **permitir várias assinaturas** caixa de seleção e, opcionalmente, especificar um limite. Se essa caixa não estiver marcada, cada conta de desenvolvedor pode inscrever-se apenas um produto de toohello única vez.

Opcionalmente, preencha Olá **termos de uso** campo que descreve os termos de saudação de uso de produto de saudação que os assinantes devem aceitar no produto de saudação do pedido toouse.

## <a name="publish-product"> </a>Publicar um produto
Antes de saudação APIs em um produto pode ser chamada, produto Olá deve ser publicado. Em Olá **resumo** produto hello, clique em **publicar**e, em seguida, clique em **Sim, publicá-lo** tooconfirm. toomake privado um produto publicada anteriormente, clique em **Cancelar publicação**.

![Publicar produto][api-management-publish-product]

## <a name="make-visible"></a>Fazer um toodevelopers visível do produto
Olá **visibilidade** guia permite que você toochoose quais funções são capazes de toosee Olá produto no portal do desenvolvedor hello e assinar toohello produto.

![Visibilidade do produto][api-management-product-visiblity]

tooenable ou desativar visibilidade de um produto para desenvolvedores de saudação em um grupo, marque ou desmarque Olá a caixa de seleção ao lado do grupo de saudação e, em seguida, clique em **salvar**.

> Para obter mais informações, consulte [como desenvolvedor de toomanage grupos toocreate e usar contas no gerenciamento de API do Azure][How toocreate and use groups toomanage developer accounts in Azure API Management].
> 
> 

## <a name="view-subscribers"></a>Produto de tooa de assinantes do modo de exibição
Olá **assinantes** guia lista os desenvolvedores de saudação que assinaram toohello produto. Olá detalhes e as configurações para cada desenvolvedor podem ser exibidas clicando no nome do desenvolvedor hello. Neste exemplo não desenvolvedores inscreveu ainda toohello produto.

![Desenvolvedores][api-management-developer-list]

## <a name="next-steps"> </a>Próximas etapas
Uma vez Olá desejado APIs foram adicionadas e produto Olá publicado, os desenvolvedores podem assinar toohello produto e começar a saudação toocall APIs. Para ver um tutorial que demonstra esses itens, bem como a configuração avançada do produto, consulte [Como criar e definir configurações avançadas no Gerenciamento de API do Azure][How create and configure advanced product settings in Azure API Management].

Para obter mais informações sobre como trabalhar com produtos, consulte Olá vídeo a seguir.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

[Create a product]: #create-product
[Add APIs tooa product]: #add-apis
[Add descriptive information tooa product]: #add-description
[Publish a product]: #publish-product
[Make a product visible toodevelopers]: #make-visible
[View subscribers tooa product]: #view-subscribers
[Next steps]: #next-steps

[api-management-management-console]: ./media/api-management-howto-add-products/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-add-products/api-management-add-product.png
[api-management-add-new-product]: ./media/api-management-howto-add-products/api-management-add-new-product.png
[api-management-unlimited-multiple-subscriptions]: ./media/api-management-howto-add-products/api-management-unlimited-multiple-subscriptions.png
[api-management-four-multiple-subscriptions]: ./media/api-management-howto-add-products/api-management-four-multiple-subscriptions.png
[api-management-products-page]: ./media/api-management-howto-add-products/api-management-products-page.png
[api-management-new-product-summary]: ./media/api-management-howto-add-products/api-management-new-product-summary.png
[api-management-add-apis-to-product]: ./media/api-management-howto-add-products/api-management-add-apis-to-product.png
[api-management-product-settings]: ./media/api-management-howto-add-products/api-management-product-settings.png
[api-management-publish-product]: ./media/api-management-howto-add-products/api-management-publish-product.png
[api-management-product-visiblity]: ./media/api-management-howto-add-products/api-management-product-visibility.png
[api-management-developer-list]: ./media/api-management-howto-add-products/api-management-developer-list.png



[api-management-products]: ./media/api-management-howto-add-products/api-management-products.png
[api-management-]: ./media/api-management-howto-add-products/
[api-management-]: ./media/api-management-howto-add-products/


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps
[How toocreate and use groups toomanage developer accounts in Azure API Management]: api-management-howto-create-groups.md
[How create and configure advanced product settings in Azure API Management]: api-management-howto-product-with-rules.md 
