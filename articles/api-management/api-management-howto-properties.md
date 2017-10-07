---
title: "Propriedades de toouse aaaHow nas políticas de gerenciamento de API do Azure"
description: "Saiba como propriedades toouse nas políticas de gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 6f39b00f-cf6e-4cef-9bf2-1f89202c0bc0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 1ff096deeb97543b48dcf1f40be9dbfcbcd09542
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-properties-in-azure-api-management-policies"></a>Como propriedades toouse nas políticas de gerenciamento de API do Azure
Políticas de gerenciamento de API são um recurso poderoso do sistema Olá que permitem que o publicador Olá toochange comportamento de saudação do hello API por meio da configuração. As políticas são um conjunto de instruções que são executadas sequencialmente na solicitação de saudação ou resposta de uma API. É possível construir declarações de política usando valores de texto literais, expressões de política e propriedades. 

Cada instância de serviço de gerenciamento de API tem uma coleção de propriedades de pares chave/valor que são globais toohello instância de serviço. Essas propriedades podem ser valores de cadeia de caracteres constante toomanage usado em todas as políticas e configurações de API. Cada propriedade tem Olá atributos a seguir.

| Atributo | Tipo | Descrição |
| --- | --- | --- |
| Name |string |nome de saudação da propriedade de saudação. Ele pode conter apenas letras, dígitos, ponto, traço e caracteres de sublinhado. |
| Valor |string |valor de saudação da propriedade de saudação. Ele não pode ficar vazio ou conter apenas espaços em branco. |
| Segredo |Booliano |Determina se o valor de saudação é um segredo e deve ser criptografado ou não. |
| Marcas |matriz de cadeias de caracteres |Opcional marcas que, quando fornecido pode ser usado toofilter Olá propriedade lista. |

Propriedades são configuradas no portal do publicador de saudação em Olá **propriedades** guia. Saudação de exemplo a seguir, três propriedades são configuradas.

![Propriedades][api-management-properties]

Os valores de propriedade podem conter cadeias de caracteres literais e [expressões de política](https://msdn.microsoft.com/library/azure/dn910913.aspx). Olá tabela a seguir mostra Olá anterior exemplo três propriedades e seus atributos. Olá valor `ExpressionProperty` é uma expressão de diretiva que retorna uma cadeia de caracteres que contém Olá data e hora atuais. Olá propriedade `ContosoHeaderValue` está marcado como um segredo, portanto, seu valor não é exibido.

| Nome | Valor | Segredo | Marcas |
| --- | --- | --- | --- |
| ContosoHeader |TrackingId |Falso |Contoso |
| ContosoHeaderValue |•••••••••••••••••••••• |Verdadeiro |Contoso |
| ExpressionProperty |@(DateTime.Now.ToString()) |Falso | |

## <a name="toouse-a-property"></a>toouse uma propriedade
como o nome da propriedade Olá local dentro de um duplo par de chaves toouse uma propriedade em uma política, `{{ContosoHeader}}`, conforme mostrado no exemplo a seguir de saudação.

```xml
<set-header name="{{ContosoHeader}}" exists-action="override">
  <value>{{ContosoHeaderValue}}</value>
</set-header>
```

Neste exemplo, `ContosoHeader` é usado como nome de saudação de um cabeçalho em um `set-header` política, e `ContosoHeaderValue` é usado como valor de saudação desse cabeçalho. Quando essa política é avaliada durante uma solicitação ou resposta toohello API gateway de gerenciamento, `{{ContosoHeader}}` e `{{ContosoHeaderValue}}` são substituídas por seus valores de propriedade do respectivos.

Propriedades podem ser usadas como atributo concluído ou valores de elemento, conforme mostrado no exemplo anterior hello, mas eles também podem ser inseridos ou combinados com parte de uma expressão de texto literal, conforme mostrado no exemplo a seguir de saudação:`<set-header name = "CustomHeader{{ContosoHeader}}" ...>`

As propriedades também podem conter expressões de política. Em Olá exemplo a seguir, Olá `ExpressionProperty` é usado.

```xml
<set-header name="CustomHeader" exists-action="override">
    <value>{{ExpressionProperty}}</value>
</set-header>
```

Quando essa política é avaliada, `{{ExpressionProperty}}` é substituído por seu valor: `@(DateTime.Now.ToString())`. Como valor de saudação é uma expressão de diretiva, Olá expressão é avaliada e política Olá prossegue com a sua execução.

Você pode testar isso no portal do desenvolvedor Olá chamando uma operação que tenha uma política com as propriedades no escopo. Em Olá exemplo a seguir, uma operação é chamada no exemplo anterior dois de saudação `set-header` políticas com propriedades. Observe que a resposta de saudação contém dois cabeçalhos personalizados que foram configurados usando políticas com propriedades.

![Portal do desenvolvedor][api-management-send-results]

Se você observar Olá [rastreamento de API do Inspetor](api-management-howto-api-inspector.md) para uma chamada que inclui Olá duas anterior exemplo políticas com propriedades, você pode ver Olá dois `set-header` políticas com valores de propriedade Olá inseridos, bem como expressão de diretiva Olá avaliação de propriedade Olá que continha a expressão de diretiva de saudação.

![Rastreamento do Inspetor de API][api-management-api-inspector-trace]

Observe que, embora os valores de propriedade possam conter expressões de política, os valores de propriedade não podem conter outras propriedades. Se o texto que contém uma referência de propriedade é usado para um valor de propriedade, como `Property value text {{MyProperty}}`, que referência da propriedade não será substituída e será incluída como parte do valor da propriedade hello.

## <a name="toocreate-a-property"></a>toocreate uma propriedade
toocreate uma propriedade, clique em **adicionar propriedade** em Olá **propriedades** guia.

![Adicionar propriedade][api-management-properties-add-property-menu]

**Nome** e **Valor** são valores obrigatórios. Se o valor dessa propriedade é um segredo, verifique Olá **é um segredo** caixa de seleção. Insira um ou mais toohelp de marcas opcionais com organizar suas propriedades e, em seguida, clique em **salvar**.

![Adicionar propriedade][api-management-properties-add-property]

Quando uma nova propriedade é salvo, Olá **propriedades de pesquisa** caixa de texto é preenchida com o nome hello da nova propriedade de saudação e nova propriedade de saudação é exibida. toodisplay todas as propriedades, desmarque Olá **propriedades de pesquisa** caixa de texto e pressione enter.

![Propriedades][api-management-properties-property-saved]

Para obter informações sobre a criação de uma propriedade usando Olá API REST, consulte [criar uma propriedade usando a API REST de saudação](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).

## <a name="tooedit-a-property"></a>tooedit uma propriedade
tooedit uma propriedade, clique em **editar** ao lado de saudação tooedit de propriedade.

![Editar propriedade][api-management-properties-edit]

Faça as alterações desejadas e clique em **Salvar**. Se você alterar o nome da propriedade hello, todas as políticas que fazem referência a essa propriedade são novo nome de saudação toouse atualizadas automaticamente.

![Editar propriedade][api-management-properties-edit-property]

Para obter informações sobre como editar uma propriedade usando Olá API REST, consulte [editar uma propriedade usando a API REST de saudação](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).

## <a name="toodelete-a-property"></a>toodelete uma propriedade
toodelete uma propriedade, clique em **excluir** ao lado de saudação toodelete de propriedade.

![Excluir propriedade][api-management-properties-delete]

Clique em **Sim, excluí-la** tooconfirm.

![Confirmar exclusão][api-management-delete-confirm]

> [!IMPORTANT]
> Se a propriedade de saudação é referenciada por nenhuma das políticas, não será possível toosuccessfully excluí-lo até que você remova a propriedade de saudação de todas as políticas que usá-lo.
> 
> 

Para obter informações sobre como excluir uma propriedade usando Olá API REST, consulte [excluir uma propriedade usando a API REST de saudação](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).

## <a name="toosearch-and-filter-properties"></a>propriedades toosearch e filtro
Olá **propriedades** guia inclui pesquisando e filtrando toohelp recursos gerenciar suas propriedades. lista de propriedades de saudação toofilter pelo nome da propriedade, digite um termo de pesquisa no hello **propriedades de pesquisa** caixa de texto. toodisplay todas as propriedades, desmarque Olá **propriedades de pesquisa** caixa de texto e pressione enter.

![Pesquisar][api-management-properties-search]

lista de propriedades de saudação toofilter pelos valores de marca, insira uma ou mais marcas em Olá **filtrar por marcas** caixa de texto. toodisplay todas as propriedades, desmarque Olá **filtrar por marcas** caixa de texto e pressione enter.

![Filter][api-management-properties-filter]

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre como trabalhar com políticas
  * [Políticas no Gerenciamento de API](api-management-howto-policies.md)
  * [Referência de política](https://msdn.microsoft.com/library/azure/dn894081.aspx)
  * [Expressões de política](https://msdn.microsoft.com/library/azure/dn910913.aspx)

## <a name="watch-a-video-overview"></a>Assista a uma visão geral em vídeo
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Use-Properties-in-Policies/player]
> 
> 

[api-management-properties]: ./media/api-management-howto-properties/api-management-properties.png
[api-management-properties-add-property]: ./media/api-management-howto-properties/api-management-properties-add-property.png
[api-management-properties-edit-property]: ./media/api-management-howto-properties/api-management-properties-edit-property.png
[api-management-properties-add-property-menu]: ./media/api-management-howto-properties/api-management-properties-add-property-menu.png
[api-management-properties-property-saved]: ./media/api-management-howto-properties/api-management-properties-property-saved.png
[api-management-properties-delete]: ./media/api-management-howto-properties/api-management-properties-delete.png
[api-management-properties-edit]: ./media/api-management-howto-properties/api-management-properties-edit.png
[api-management-delete-confirm]: ./media/api-management-howto-properties/api-management-delete-confirm.png
[api-management-properties-search]: ./media/api-management-howto-properties/api-management-properties-search.png
[api-management-send-results]: ./media/api-management-howto-properties/api-management-send-results.png
[api-management-properties-filter]: ./media/api-management-howto-properties/api-management-properties-filter.png
[api-management-api-inspector-trace]: ./media/api-management-howto-properties/api-management-api-inspector-trace.png

