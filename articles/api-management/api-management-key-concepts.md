---
title: "conceitos de visão geral e a chave de gerenciamento de API aaaAzure | Microsoft Docs"
description: "Saiba mais sobre APIs, produtos, funções, grupos e outros conceitos principais do Gerenciamento de API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: e71da405-835a-48f3-956f-45c1a85698d7
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: a77b24b4632d868afa15bd6cf88060982046cb38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-api-management"></a>O que é Gerenciamento de API?
Gerenciamento de API ajuda as organizações a publicar APIs tooexternal, parceiros e desenvolvedores internos toounlock Olá potencial seus dados e serviços. Empresas everywhere estão procurando tooextend suas operações, como uma plataforma digital, criando novos canais, encontrando novos clientes e orienta a relação mais sólida com os existentes. Gerenciamento de API fornece Olá core competências tooensure um programa de API com êxito pelo contrato de desenvolvedor, ideias de negócios, análises, segurança e proteção.

Veja Olá seguinte vídeo para obter uma visão geral do gerenciamento de API do Azure e aprenda como tooadd de gerenciamento de API toouse muitos recursos tooyour API, inclusive o controle de acesso, taxa de limitação, monitoramento, o log de eventos e o cache de resposta, com um mínimo de trabalho de sua parte.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-API-Management-Overview/player]
> 
> 

toouse gerenciamento de API, os administradores criam APIs. Cada API consiste em uma ou mais operações e pode ser adicionado a cada API tooone ou mais produtos. toouse uma API, os desenvolvedores assinam tooa produto que contenha essa API e, em seguida, ele podem chamar a operação de saudação da API, assunto tooany as políticas de uso pode estar em vigor.

Esse tópico fornece uma visão geral dos principais conceitos de Gerenciamento de API.

> [!NOTE]
> Para obter mais informações, consulte Olá [baseado em nuvem de gerenciamento de API: utilizando Olá APIs do Power](http://j.mp/ms-apim-whitepaper) white paper do PDF. Este white paper introdutório sobre o Gerenciamento de API, feito pelo CITO Research, abrange: 
> 
> * Desafios e requisitos comuns de API
> * Dissociação de APIs e apresentação de fachadas
> * Como ajudar os desenvolvedores a trabalhar de modo rápido e fácil
> * Proteção de acesso
> * Métricas e análise
> * Obtenção de controle e ideias com uma plataforma de Gerenciamento de API
> * Usar a nuvem vs. soluções locais
> * Gerenciamento de API do Azure
> 
> 

## <a name="apis"> </a>APIs e operações
APIs são a base de saudação de uma instância do serviço de gerenciamento de API. Cada API representa um conjunto de toodevelopers de operações disponíveis. Cada API contém um serviço de back-end de toohello de referência que implementa a API de saudação e suas operações mapeiam operações toohello implementadas pelo serviço de back-end de saudação. As operações no Gerenciamento de API são altamente configuráveis, com controle sobre o mapeamento de URL, parâmetros de consulta e caminho, conteúdo de solicitação e resposta e caching de resposta de operação. O limite de taxa, cotas e políticas de restrição de IP também podem ser implementadas no nível de operação individual ou Olá API.

Para obter mais informações, consulte [como toocreate APIs] [ How toocreate APIs] e [como tooadd operações tooan API][How tooadd operations tooan API].

## <a name="products"> </a> Produtos
Os produtos são como os APIs são toodevelopers da superfície. Os produtos no Gerenciamento de API têm uma ou mais APIs e são configurados com título, descrição e termos de uso. Produtos podem ser **Abertos** ou **Protegidos**. Produtos protegidos devem ser assinado toobefore, eles podem ser usados, ao abrir produtos podem ser usados sem uma assinatura. Quando um produto fica pronto para uso pelo desenvolvedor ele pode ser publicado. Depois que ele é publicado, ela pode ser exibida (e no hello caso de produtos protegidos assinado) por desenvolvedores. Aprovação da assinatura é configurada no nível do produto hello e pode exigir aprovação do administrador ou ser aprovada automaticamente.

Os grupos são usados toomanage Olá visibilidade de produtos toodevelopers. Produtos conceder toogroups de visibilidade, e os desenvolvedores podem exibir e assinar toohello produtos que são grupos de toohello visíveis no qual eles pertencem. 

Para obter mais informações, consulte [como toocreate e publicar um produto] [ How toocreate and publish a product] e Olá vídeo a seguir.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Using-Products/player]
> 
> 

## <a name="groups"> </a> Grupos
Os grupos são usados toomanage Olá visibilidade de produtos toodevelopers. Gerenciamento de API tem Olá seguintes grupos de sistema imutável.

* **Administradores** - os administradores de assinatura do Azure são membros desse grupo. Os administradores gerenciar instâncias do serviço de gerenciamento de API, criando Olá APIs, operações e produtos que são usados pelos desenvolvedores.
* **Desenvolvedores** - usuários autenticados do portal do desenvolvedor se enquadram nesse grupo. Os desenvolvedores são clientes Olá que desenvolvem aplicativos utilizando suas APIs. Os desenvolvedores recebem o portal do desenvolvedor do access toohello e criarem aplicativos que chamar operações de saudação de uma API.
* **Convidados** -usuários portal do desenvolvedor, como clientes potenciais visitando o portal do desenvolvedor de saudação de uma queda de instância de gerenciamento de API para este grupo não autenticados. Eles podem ser concedidos determinado acesso somente leitura, como Olá capacidade tooview APIs, mas não chamá-los.

Em grupos de sistema de toothese de adição, os administradores podem criar grupos personalizados ou [aproveitar grupos externos nos locatários do Active Directory do Azure associados](api-management-howto-aad.md#how-to-add-an-external-azure-active-directory-group). Grupos externos e personalizados podem ser usados juntamente com grupos de sistema ao dar visibilidade a desenvolvedores e acessar tooAPI produtos. Por exemplo, você pode criar um grupo personalizado para desenvolvedores associados a uma determinada organização do parceiro e permitem acesso toohello APIs de um produto que contém apenas as APIs relevantes. Um usuário pode ser um membro de mais de um grupo.

Para obter mais informações, consulte [como toocreate e use grupos][How toocreate and use groups].

## <a name="developers"> </a> Desenvolvedores
Os desenvolvedores representam contas de usuário de saudação em uma instância do serviço de gerenciamento de API. Os desenvolvedores podem ser criados ou convidado toojoin por administradores, ou pode inscrever da saudação [portal do desenvolvedor][Developer portal]. Cada desenvolvedor é um membro de um ou mais grupos e é possível assinar toohello produtos que conceder visibilidade toothose grupos.

Quando os desenvolvedores assinam tooa produto eles recebem a chave primária e secundária Olá Olá produto. Essa chave é usada ao fazer chamadas para APIs do produto hello.

Para obter mais informações, consulte [como toocreate ou convite desenvolvedores] [ How toocreate or invite developers] e [como os grupos de tooassociate com os desenvolvedores][How tooassociate groups with developers].

## <a name="policies"> </a> Políticas
As políticas são um recurso poderoso do gerenciamento de API que permitem que o publicador Olá toochange comportamento de saudação do hello API por meio da configuração. As políticas são um conjunto de instruções que são executadas sequencialmente na solicitação de saudação ou resposta de uma API. As instruções populares incluem conversão de formato de XML tooJSON e chamada taxa limitando toorestrict Olá quantidade de chamadas de entrada de um desenvolvedor e muitas outras políticas estão disponíveis.

Expressões de política podem ser usadas como valores de atributo ou texto em qualquer uma das políticas de gerenciamento de API hello, a menos que Olá política especifique o contrário. Algumas políticas, como Olá [fluxo de controle](https://msdn.microsoft.com/library/azure/dn894085.aspx#choose) e [Set variable](https://msdn.microsoft.com/library/azure/dn894085.aspx#set-variable) políticas se baseiam em expressões de política. Para obter mais informações, consulte [políticas avançadas](https://msdn.microsoft.com/library/azure/dn894085.aspx#AdvancedPolicies), [expressões de política](https://msdn.microsoft.com/library/azure/dn910913.aspx), e Olá inspecionar vídeo a seguir.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

Para obter uma lista completa de políticas de Gerenciamento de API, confira [Referência de política][Policy reference]. Para obter mais informações sobre como usar e configurar políticas, confira [Políticas de Gerenciamento de API][API Management policies]. Para obter um tutorial sobre como criar um produto com políticas de cota e limite de taxa, confira [Como criar e definir configurações avançadas de produto][How create and configure advanced product settings]. Para ver uma demonstração, consulte Olá vídeo a seguir.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Rate-Limits-and-Quotas/player]
> 
> 

## <a name="developer-portal"> </a> Portal do desenvolvedor
portal do desenvolvedor Olá é onde os desenvolvedores podem aprender sobre as operações de APIs, exibição e chamada e inscrever-se tooproducts. Clientes potenciais podem visitar o portal do desenvolvedor hello, exibir APIs e operações e inscrever-se. saudação URL para o portal do desenvolvedor está localizado no painel de saudação do hello Portal clássico do Azure para sua instância de serviço de gerenciamento de API.

Você pode personalizar Olá aparência de seu portal do desenvolvedor adicionar conteúdo personalizado, personalizar estilos e adicionando a sua identidade visual.

## <a name="api-management-and-hello-api-economy"></a>Economia de API de gerenciamento de API e hello
toolearn mais sobre o gerenciamento de API, Olá Observação a seguir de apresentação de conferência Olá Microsoft Ignite 2015.

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3708/player]
> 
> 

[APIs and operations]: #apis
[Products]: #products
[Groups]: #groups
[Developers]: #developers
[Policies]: #policies
[Developer portal]: #developer-portal

[How toocreate APIs]: api-management-howto-create-apis.md
[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocreate and use groups]: api-management-howto-create-groups.md
[How tooassociate groups with developers]: api-management-howto-create-groups.md#associate-group-developer
[How create and configure advanced product settings]: api-management-howto-product-with-rules.md
[How toocreate or invite developers]: api-management-howto-create-or-invite-developers.md
[Policy reference]: api-management-policy-reference.md
[API Management policies]: api-management-howto-policies.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance




