---
title: aaaProtect sua API com gerenciamento de API do Azure | Microsoft Docs
description: "Saiba como tooprotect sua API com cotas e políticas (limite de taxa) de limitação."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 450dc368-d005-401d-ae64-3e1a2229b12f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 3113fd277d434da0c051b8b90fd629a102bf4867
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-your-api-with-rate-limits-using-azure-api-management"></a>Proteja sua API com limites de taxa usando o Gerenciamento de API do Azure
Este guia mostra como é fácil tooadd proteção para a API de back-end, configurando políticas de cota e de limite de taxa ao gerenciamento de API do Azure.

Neste tutorial, você criará um produto de "Avaliação gratuita" API que permite aos desenvolvedores toomake too10 chamadas por minuto e backup tooa máximo de 200 chamadas por semana tooyour API usando Olá [limitar a taxa de chamada por assinatura](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) e [ Definir a cota de uso por assinatura](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) políticas. Você, em seguida, publicar Olá API e testar a política de limite de taxa de saudação.

Para mais avançados limitação cenários usando Olá [taxa limite por chave](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) e [cota por chave](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) políticas, consulte [solicitação avançada de limitação com gerenciamento de API do Azure](api-management-sample-flexible-throttling.md).

## <a name="create-product"></a>toocreate um produto
Nesta etapa você criará um produto de avaliação gratuita que não requer aprovação de assinatura.

> [!NOTE]
> Se você já tiver um produto configurado e deseja toouse-la para este tutorial, você pode pular muito[configurar políticas de cota e de limite de taxa de chamada] [ Configure call rate limit and quota policies] e siga o tutorial hello a partir daí, usando o produto em vez de produto de avaliação gratuita de saudação.
> 
> 

tooget iniciado, clique em **portal do publicador** em hello Portal do Azure para seu serviço de gerenciamento de API.

![Portal do editor][api-management-management-console]

> Se você ainda não tiver criado uma instância do serviço de gerenciamento de API, consulte [criar uma instância do serviço de gerenciamento de API] [ Create an API Management service instance] em Olá [gerenciar sua primeira API no gerenciamento de API do Azure] [ Manage your first API in Azure API Management] tutorial.
> 
> 

Clique em **produtos** em Olá **gerenciamento de API** menu Olá toodisplay esquerdo Olá **produtos** página.

![Adicionar produto][api-management-add-product]

Clique em **adicionar produto** toodisplay Olá **adicionar novo produto** caixa de diálogo.

![Adicionar novo produto][api-management-new-product-window]

Em Olá **título** , digite **avaliação gratuita**.

Em Olá **descrição** caixa, Olá tipo texto a seguir: **assinantes será capaz de toorun 10 chamadas por minuto backup tooa máximo de 200 chamadas/semana após o qual o acesso é negado.**

Os produtos de Gerenciamento de API podem ser protegidos ou abertos. Produtos protegidos devem ser toobefore inscrito, eles podem ser usados. Os produtos abertos podem ser usados sem uma assinatura. Certifique-se de que **exigir assinatura** é toocreate selecionado um produto protegido que requer uma assinatura. Essa é a configuração de padrão de saudação.

Se você deseja que um administrador tooreview e aceitar ou rejeitar assinatura tentativas toothis produto, selecione **exigirem a aprovação de assinatura**. Se a caixa de seleção de saudação não estiver selecionada, tentativas de assinatura serão aprovadas automaticamente. Neste exemplo, as assinaturas são automaticamente aprovadas, portanto, não marque a caixa de saudação.

contas de desenvolvedor tooallow toosubscribe várias vezes toohello novo produto, selecione Olá **permitir várias inscrições simultâneas** caixa de seleção. Este tópico não utiliza várias inscrições simultâneas, por isso deixe-o desmarcado.

Depois que todos os valores são inseridos, clique em **salvar** toocreate produto de saudação.

![Produto adicionado][api-management-product-added]

Por padrão, novos produtos são visíveis toousers em Olá **administradores** grupo. Vamos Olá tooadd **desenvolvedores** grupo. Clique em **avaliação gratuita**e, em seguida, clique em Olá **visibilidade** guia.

> No gerenciamento de API, os grupos são usados toomanage Olá visibilidade de produtos toodevelopers. Produtos conceder toogroups de visibilidade, e os desenvolvedores podem exibir e assinar toohello produtos que são grupos de toohello visíveis no qual eles pertencem. Para obter mais informações, consulte [como toocreate e use os grupos no gerenciamento de API do Azure][How toocreate and use groups in Azure API Management].
> 
> 

![Adicionar um grupo de desenvolvedores][api-management-add-developers-group]

Selecione Olá **desenvolvedores** caixa de seleção e, em seguida, clique em **salvar**.

## <a name="add-api"></a>tooadd uma API toohello produto
Nesta etapa do tutorial Olá, vamos adicionar Olá Echo toohello nova avaliação gratuita produto da API.

> Cada instância de serviço de gerenciamento de API vem pré-configurada com uma API de eco que podem ser usado tooexperiment com e saiba mais sobre o gerenciamento de API. Para saber mais, confira [Gerenciar sua primeira API no Gerenciamento de API do Azure][Manage your first API in Azure API Management].
> 
> 

Clique em **produtos** de saudação **gerenciamento de API** menu saudação à esquerda e clique **avaliação gratuita** tooconfigure produto de saudação.

![Configurar produto][api-management-configure-product]

Clique em **tooproduct adicionar API**.

![Adicionar tooproduct de API][api-management-add-api]

Selecione a **API de Eco** e clique em **Salvar**.

![Adicionar API de Eco][api-management-add-echo-api]

## <a name="policies"></a>tooconfigure políticas de cota e de limite de taxa de chamada
Cotas e limites de taxa são configuradas no editor de diretiva de saudação. políticas de saudação dois adicionaremos neste tutorial são Olá [limitar a taxa de chamada por assinatura](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) e [definir cota de uso por assinatura](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota) políticas. Essas políticas devem ser aplicadas no escopo do produto hello.

Clique em **políticas** em Olá **gerenciamento de API** menu Olá esquerda. Em Olá **produto** lista, clique em **avaliação gratuita**.

![Política de produtos][api-management-product-policy]

Clique em **adicionar política** tooimport Olá modelo de política e começar a criar políticas de cota e de limite de taxa de saudação.

![Adicionar política][api-management-add-policy]

Políticas de cota e de limite de taxa são políticas de entrada, portanto cursor Olá de posição no elemento de entrada hello.

![Editor de políticas][api-management-policy-editor-inbound]

Role a lista de saudação de políticas e localizar Olá **limitar a taxa de chamada por assinatura** entrada da política.

![Declarações de políticas][api-management-limit-policies]

Após Olá cursor é posicionado na Olá **entrada** elemento de política, clique Olá seta ao lado de **limitar a taxa de chamada por assinatura** tooinsert seu modelo de política.

```xml
<rate-limit calls="number" renewal-period="seconds">
<api name="name" calls="number">
<operation name="name" calls="number" />
</api>
</rate-limit>
```

Como você pode ver do trecho hello, a política de saudação permite que os limites de configuração para as operações e as APIs do produto hello. Neste tutorial, não use esse recurso, exclua Olá **api** e **operação** elementos da saudação **limite de taxa** elemento, de modo que apenas Olá externa **limite de taxa** elemento permanece, conforme mostrado no exemplo a seguir de saudação.

```xml
<rate-limit calls="number" renewal-period="seconds">
</rate-limit>
```

Produto de avaliação gratuita Olá, taxa de chamada permitido máximo de saudação é 10 chamadas por minuto, digite **10** como valor Olá Olá **chamadas** atributo, e **60** para Olá **período de renovação** atributo.

```xml
<rate-limit calls="10" renewal-period="60">
</rate-limit>
```

Olá tooconfigure **definir cota de uso por assinatura** política, posição o cursor imediatamente abaixo Olá recém-adicionado **limite de taxa** elemento dentro do hello **entrada** elemento, localize e clique em Olá seta à esquerda da toohello de **definir cota de uso por assinatura**.

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
<api name="name" calls="number" bandwidth="kilobytes">
<operation name="name" calls="number" bandwidth="kilobytes" />
</api>
</quota>
```

Da mesma forma toohello **definir cota de uso por assinatura** política, **definir cota de uso por assinatura** política permite definir limites para em operações e APIs do produto hello. Neste tutorial, não use esse recurso, exclua Olá **api** e **operação** elementos da saudação **cota** elemento, conforme mostrado no exemplo a seguir de saudação.

```xml
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">
</quota>
```

As cotas podem ser com base no número de saudação de chamadas por intervalo, a largura de banda ou ambos. Neste tutorial, nós não são limitação com base na largura de banda, exclua Olá **largura de banda** atributo.

```xml
<quota calls="number" renewal-period="seconds">
</quota>
```

Produto de avaliação gratuita do hello, a cota de saudação é 200 chamadas por semana. Especifique **200** como valor Olá Olá **chamadas** de atributo e, em seguida, especifique **604800** como valor Olá Olá **período de renovação** atributo.

```xml
<quota calls="200" renewal-period="604800">
</quota>
```

> Os intervalos de política são especificados em segundos. o intervalo de saudação toocalculate por uma semana, você pode multiplicar Olá quantos dias (7) pelo número de saudação de horas em um dia (24) pelo número de saudação de minutos em uma hora (60) por um número de segundos em um minuto (60) hello: 7 * 24 * 60 * 60 = 604800.
> 
> 

Quando terminar de configurar a política de hello, ele deve corresponder Olá exemplo a seguir.

```xml
<policies>
    <inbound>
        <rate-limit calls="10" renewal-period="60">
        </rate-limit>
        <quota calls="200" renewal-period="604800">
        </quota>
        <base />

</inbound>
<outbound>

    <base />

    </outbound>
</policies>
```

Depois de saudação desejado políticas estão configuradas, clique em **salvar**.

![Salvar política][api-management-policy-save]

## <a name="publish-product"></a> produto de saudação toopublish
Agora que hello hello APIs foram adicionadas e Olá políticas estão configuradas, produto Olá deve ser publicado para que ele pode ser usado por desenvolvedores. Clique em **produtos** de saudação **gerenciamento de API** menu saudação à esquerda e clique **avaliação gratuita** tooconfigure produto de saudação.

![Configurar produto][api-management-configure-product]

Clique em **publicar**e, em seguida, clique em **Sim, publicá-lo** tooconfirm.

![Publicar produto][api-management-publish-product]

## <a name="subscribe-account"></a>toosubscribe um produto de toohello de conta de desenvolvedor
Agora esse produto Olá é publicado, é tooand toobe disponível assinado usado por desenvolvedores.

> Os administradores de uma instância de gerenciamento de API são automaticamente inscritos tooevery produto. Nessa etapa do tutorial, vamos assinará um produto de avaliação gratuita do hello desenvolvedor de não-administrador contas toohello. Se sua conta de desenvolvedor fizer parte da função de administradores hello, você pode prosseguir com esta etapa, mesmo que você já se inscreveu.
> 
> 

Clique em **usuários** em Olá **gerenciamento de API** menu Olá à esquerda e, em seguida, clique em nome de saudação da sua conta de desenvolvedor. Neste exemplo, estamos usando Olá **Clayton Gragg** conta de desenvolvedor.

![Configurar desenvolvedor][api-management-configure-developer]

Clique em **Adicionar assinatura**.

![Adicionar assinatura][api-management-add-subscription-menu]

Selecione **Avaliação Gratuita** e clique em **Assinar**.

![Adicionar assinatura][api-management-add-subscription]

> [!NOTE]
> Neste tutorial, várias assinaturas simultâneas não estão habilitadas para o produto de avaliação gratuita de saudação. Se forem, seria tooname solicitadas Olá assinatura, conforme mostrado no exemplo a seguir de saudação.
> 
> 

![Adicionar assinatura][api-management-add-subscription-multiple]

Depois de clicar em **assinar**, produto Olá aparece no hello **assinatura** lista de usuário hello.

![Assinatura adicionada][api-management-subscription-added]

## <a name="test-rate-limit"></a>toocall um limite de taxa de saudação operação e teste
Agora que hello produto de avaliação gratuita está configurado e publicado, podemos chamar algumas operações e testar a política de limite de taxa de saudação.
Portal do desenvolvedor do comutador toohello clicando **portal do desenvolvedor** no menu superior direito de saudação.

![Portal do desenvolvedor][api-management-developer-portal-menu]

Clique em **APIs** Olá menu superior e, em seguida, clique em **Echo API**.

![Portal do desenvolvedor][api-management-developer-portal-api-menu]

Clique em **Recurso GET**, em seguida, clique em **Experimentar**.

![Abrir console][api-management-open-console]

Mantenha o padrão de saudação valores de parâmetro e, em seguida, selecione a chave de assinatura para o produto de avaliação gratuita de saudação.

![Chave de assinatura][api-management-select-key]

> [!NOTE]
> Se você tiver várias assinaturas, ser se tooselect Olá chave **avaliação gratuita**, ou mais políticas de saudação que foram configuradas nas etapas anteriores Olá não terá efeito.
> 
> 

Clique em **enviar**e, em seguida, exibir resposta hello. Saudação de Observação **status da resposta** de **200 Okey**.

![Resultados da operação][api-management-http-get-results]

Clique em **enviar** em uma taxa maior que a política de limite de taxa de saudação de 10 chamadas por minuto. Depois de política de limite de taxa de saudação for excedida, um status de resposta de **429 muito muitas solicitações** é retornado.

![Resultados da operação][api-management-http-get-429]

Olá **conteúdo de resposta** indica Olá restantes intervalo antes de tentativas será bem-sucedida.

Quando a política de limite de taxa de saudação de 10 chamadas por minuto está em vigor, as chamadas subsequentes falharão até que 60 segundos decorridos da saudação primeiro de produto de toohello do hello 10 chamadas com êxito antes que o limite de taxa de saudação foi excedido. Neste exemplo, Olá restantes intervalo é 54 segundos.

## <a name="next-steps"> </a>Próximas etapas
* Assista a uma demonstração de definir as cotas e limites de taxa em Olá vídeo a seguir.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Rate-Limits-and-Quotas/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-product-with-rules/api-management-management-console.png
[api-management-add-product]: ./media/api-management-howto-product-with-rules/api-management-add-product.png
[api-management-new-product-window]: ./media/api-management-howto-product-with-rules/api-management-new-product-window.png
[api-management-product-added]: ./media/api-management-howto-product-with-rules/api-management-product-added.png
[api-management-add-policy]: ./media/api-management-howto-product-with-rules/api-management-add-policy.png
[api-management-policy-editor-inbound]: ./media/api-management-howto-product-with-rules/api-management-policy-editor-inbound.png
[api-management-limit-policies]: ./media/api-management-howto-product-with-rules/api-management-limit-policies.png
[api-management-policy-save]: ./media/api-management-howto-product-with-rules/api-management-policy-save.png
[api-management-configure-product]: ./media/api-management-howto-product-with-rules/api-management-configure-product.png
[api-management-add-api]: ./media/api-management-howto-product-with-rules/api-management-add-api.png
[api-management-add-echo-api]: ./media/api-management-howto-product-with-rules/api-management-add-echo-api.png
[api-management-developer-portal-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-menu.png
[api-management-publish-product]: ./media/api-management-howto-product-with-rules/api-management-publish-product.png
[api-management-configure-developer]: ./media/api-management-howto-product-with-rules/api-management-configure-developer.png
[api-management-add-subscription-menu]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-menu.png
[api-management-add-subscription]: ./media/api-management-howto-product-with-rules/api-management-add-subscription.png
[api-management-developer-portal-api-menu]: ./media/api-management-howto-product-with-rules/api-management-developer-portal-api-menu.png
[api-management-open-console]: ./media/api-management-howto-product-with-rules/api-management-open-console.png
[api-management-http-get]: ./media/api-management-howto-product-with-rules/api-management-http-get.png
[api-management-http-get-results]: ./media/api-management-howto-product-with-rules/api-management-http-get-results.png
[api-management-http-get-429]: ./media/api-management-howto-product-with-rules/api-management-http-get-429.png
[api-management-product-policy]: ./media/api-management-howto-product-with-rules/api-management-product-policy.png
[api-management-add-developers-group]: ./media/api-management-howto-product-with-rules/api-management-add-developers-group.png
[api-management-select-key]: ./media/api-management-howto-product-with-rules/api-management-select-key.png
[api-management-subscription-added]: ./media/api-management-howto-product-with-rules/api-management-subscription-added.png
[api-management-add-subscription-multiple]: ./media/api-management-howto-product-with-rules/api-management-add-subscription-multiple.png

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: ../api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Manage your first API in Azure API Management]: api-management-get-started.md
[How toocreate and use groups in Azure API Management]: api-management-howto-create-groups.md
[View subscribers tooa product]: api-management-howto-add-products.md#view-subscribers
[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[Next steps]: #next-steps

[Create a product]: #create-product
[Configure call rate limit and quota policies]: #policies
[Add an API toohello product]: #add-api
[Publish hello product]: #publish-product
[Subscribe a developer account toohello product]: #subscribe-account
[Call an operation and test hello rate limit]: #test-rate-limit

[Limit call rate]: https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate
[Set usage quota]: https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota
