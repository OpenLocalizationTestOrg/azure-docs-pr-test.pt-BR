---
title: "portal do desenvolvedor do gerenciamento de API Olá aaaCustomize usando modelos-Azure | Microsoft Docs"
description: "Saiba como toocustomize Olá portal do desenvolvedor do gerenciamento de API do Azure usando modelos."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: a195675b-f7d0-4fc9-90bf-860e6f17ccf7
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: b00d5f1534e9466f30ff3920e7aae048feb8b8c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-hello-azure-api-management-developer-portal-using-templates"></a>Como toocustomize Olá portal do desenvolvedor do gerenciamento de API do Azure usando modelos

Há três portal do desenvolvedor maneiras fundamentais toocustomize Olá no gerenciamento de API do Azure:

* [Editar conteúdo Olá páginas estáticas e elementos de layout de página][modify-content-layout]
* [Atualizar estilos Olá usados para elementos de página entre o portal do desenvolvedor Olá][customize-styles]
* [Modificar modelos de saudação usados para as páginas geradas pelo portal de saudação] [ portal-templates] (explicado neste guia)

Os modelos são usados toocustomize Olá conteúdo das páginas de portal do desenvolvedor gerada pelo sistema (por exemplo, documentos de API, produtos, autenticação de usuário, etc.). Usando [DotLiquid](http://dotliquidmarkup.org/) sintaxe e um conjunto fornecido de recursos de cadeia de caracteres localizada, ícones e controles de página, você tiver um grande flexibilidade tooconfigure Olá conteúdo das páginas hello como desejar.

## <a name="developer-portal-templates-overview"></a>Visão geral de modelos de portal do desenvolvedor
Edição de modelos é feita da saudação **portal do desenvolvedor** ao que está sendo conectado como um administrador. Há tooget primeiro abra Olá Portal do Azure e clique em **portal do publicador** da barra de ferramentas de serviço de saudação da sua instância de gerenciamento de API.

![Portal do editor][api-management-management-console]

Em seguida, clique em **portal do desenvolvedor** no canto direito superior Olá. 

![Menu do portal do desenvolvedor][api-management-developer-portal-menu]

tooaccess Olá modelos portal do desenvolvedor, clique em Olá personalizar ícone no menu de personalização de Olá Olá toodisplay esquerdo e, em seguida, clique em **modelos**.

![Modelos de portal do desenvolvedor][api-management-customize-menu]

lista de modelos de saudação exibe várias categorias de modelos que abrangem diferentes páginas Olá no portal do desenvolvedor hello. Cada modelo é diferente, mas Olá etapas tooedit-los e publicar as alterações de saudação são Olá mesmo. tooedit um modelo, clique em nome de saudação do modelo de saudação.

![Modelos de portal do desenvolvedor][api-management-templates-menu]

Clicando em um modelo usa toohello desenvolvedor página de portal que é personalizável pelo modelo. Em Olá Este exemplo **lista de produtos** modelo é exibido. Olá **lista de produtos** controles de modelo Olá área da tela hello indicada pelo retângulo Olá vermelho. 

![Modelo de lista de produtos][api-management-developer-portal-templates-overview]

Alguns modelos, como Olá **perfil de usuário** modelos, personalizar partes diferentes da saudação mesma página. 

![Modelos de perfil do usuário][api-management-user-profile-templates]

editor de saudação para cada modelo de portal do desenvolvedor possui duas seções exibidas na parte inferior da saudação da página de saudação. lado esquerdo da saudação exibe Olá editando o painel para o modelo de saudação e do lado direito da saudação exibe o modelo de dados Olá para o modelo de saudação. 

Painel de edição de modelos de saudação contém marcação Olá que controla a aparência de saudação e o comportamento da página de saudação correspondente no portal do desenvolvedor hello. marcação de saudação no modelo de saudação usa Olá [DotLiquid](http://dotliquidmarkup.org/) sintaxe. É um editor popular para DotLiquid é [DotLiquid para Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers). Qualquer modelo de toohello as alterações feitas durante a edição são exibidos em tempo real no navegador Olá, mas são clientes tooyour não visível até que você [salvar](#to-save-a-template) e [publicar](#to-publish-a-template) modelo hello.

![Marcação de modelo][api-management-template]

Olá **dados de modelo** painel fornece um guia de toohello dados modelo para entidades de saudação que estão disponíveis para uso em um modelo específico. Ele fornece este guia exibindo dados ao vivo de saudação que estão atualmente exibidos no portal do desenvolvedor hello. Você pode expandir painéis de modelo Olá clicando retângulo Olá no canto superior direito Olá Olá **dados de modelo** painel.

![Modelo de dados de modelo][api-management-template-data]

No exemplo anterior Olá existem dois produtos exibidos no portal do desenvolvedor Olá que foram recuperados do dados Olá exibidos no hello **dados de modelo** painel, conforme mostrado no exemplo a seguir de saudação.

```json
{
    "Paging": {
        "Page": 1,
        "PageSize": 10,
        "TotalItemCount": 2,
        "ShowAll": false,
        "PageCount": 1
    },
    "Filtering": {
        "Pattern": null,
        "Placeholder": "Search products"
    },
    "Products": [
        {
            "Id": "56ec64c380ed850042060001",
            "Title": "Starter",
            "Description": "Subscribers will be able toorun 5 calls/minute up tooa maximum of 100 calls/week.",
            "Terms": "",
            "ProductState": 1,
            "AllowMultipleSubscriptions": false,
            "MultipleSubscriptionsCount": 1
        },
        {
            "Id": "56ec64c380ed850042060002",
            "Title": "Unlimited",
            "Description": "Subscribers have completely unlimited access toohello API. Administrator approval is required.",
            "Terms": null,
            "ProductState": 1,
            "AllowMultipleSubscriptions": false,
            "MultipleSubscriptionsCount": 1
        }
    ]
}
```

marcações Olá Olá **lista de produtos** processos de modelo Olá a saída de dados tooprovide Olá desejado através da iteração pela coleção de saudação de informações de toodisplay de produtos e um link tooeach individual do produto. Saudação de Observação `<search-control>` e `<page-control>` elementos na marcação hello. Eles controlam a exibição de Olá de Olá pesquisa e a paginação controles na página de saudação. `ProductsStrings|PageTitleProducts`é uma referência de cadeia de caracteres localizada que contém Olá `h2` texto do cabeçalho de página hello. Para obter uma lista de recursos de cadeia de caracteres, controles de página e ícones disponíveis para uso em modelos de portal do desenvolvedor, consulte [referência de modelos de portal do desenvolvedor do Gerenciamento de API](api-management-developer-portal-templates-reference.md).

```html
<search-control></search-control>
<div class="row">
    <div class="col-md-9">
        <h2>{% localized "ProductsStrings|PageTitleProducts" %}</h2>
    </div>
</div>
<div class="row">
    <div class="col-md-12">
    {% if products.size > 0 %}
    <ul class="list-unstyled">
    {% for product in products %}
        <li>
            <h3><a href="/products/{{product.id}}">{{product.title}}</a></h3>
            {{product.description}}
        </li>    
    {% endfor %}
    </ul>
    <paging-control></paging-control>
    {% else %}
    {% localized "CommonResources|NoItemsToDisplay" %}
    {% endif %}
    </div>
</div>
```

## <a name="toosave-a-template"></a>toosave um modelo
toosave um modelo, clique em Salvar no editor de modelo de saudação.

![Salvar modelo][api-management-save-template]

Alterações salvas não são em tempo real no portal do desenvolvedor Olá até que sejam publicados.

## <a name="toopublish-a-template"></a>toopublish um modelo
Modelos salvos podem ser publicados individualmente ou em conjunto. toopublish um modelo individual, clique em Publicar no editor de modelo de saudação.

![Publicar modelo][api-management-publish-template]

Clique em **Sim** tooconfirm e modelo de saudação ativo no portal do desenvolvedor hello.

![Confirmar publicação][api-management-publish-template-confirm]

toopublish cancelada todas as versões de modelo, clique em **publicar** na lista de modelos de saudação. Modelos não publicados são designados por um asterisco após o nome do modelo de saudação. Neste exemplo, Olá **lista de produtos** e **produto** modelos forem publicados.

![Publicar modelos][api-management-publish-templates]

Clique em **publicar personalizações** tooconfirm.

![Confirmar publicação][api-management-publish-customizations]

Modelos publicados recentemente entrarão em vigor imediatamente no portal do desenvolvedor de saudação.

## <a name="toorevert-a-template-toohello-previous-version"></a>toorevert uma versão anterior do modelo toohello
toorevert uma versão de publicada modelo toohello anterior, clique em Reverter no editor de modelo de saudação.

![Reverter modelo][api-management-revert-template]

Clique em **Sim** tooconfirm.

![Confirmar][api-management-revert-template-confirm]

Olá anteriormente versão publicada de um modelo é live no portal do desenvolvedor hello quando Olá reverter a operação foi concluída.

## <a name="toorestore-a-template-toohello-default-version"></a>toorestore uma versão do modelo toohello padrão
Versão de padrão de tootheir modelos restauração é um processo de duas etapas. Modelos de saudação primeiro devem ser restaurados e versões de saudação restaurada devem ser publicadas.

toorestore uma versão do modelo único toohello padrão clique em Restaurar no editor de modelo de saudação.

![Reverter modelo][api-management-reset-template]

Clique em **Sim** tooconfirm.

![Confirmar][api-management-reset-template-confirm]

toorestore todas as versões de padrão de tootheir de modelos, clique **restaurar modelos padrão** na lista de modelos de saudação.

![Restaurar modelos][api-management-restore-templates]

Olá modelos restaurados devem ser publicados individualmente ou ao mesmo tempo, seguindo as etapas de saudação em [toopublish um modelo](#to-publish-a-template).

## <a name="next-steps"></a>Próximas etapas
Para obter informações de referência para modelos do portal do desenvolvedor, recursos de cadeia de caracteres, ícones e controles de página, consulte [referência de modelos de portal do desenvolvedor do Gerenciamento de API](api-management-developer-portal-templates-reference.md).

[modify-content-layout]: api-management-modify-content-layout.md
[customize-styles]: api-management-customize-styles.md
[portal-templates]: api-management-developer-portal-templates.md

[api-management-customize-menu]: ./media/api-management-developer-portal-templates/api-management-customize-menu.png
[api-management-templates-menu]: ./media/api-management-developer-portal-templates/api-management-templates-menu.png
[api-management-developer-portal-templates-overview]: ./media/api-management-developer-portal-templates/api-management-developer-portal-templates-overview.png
[api-management-template]: ./media/api-management-developer-portal-templates/api-management-template.png
[api-management-template-data]: ./media/api-management-developer-portal-templates/api-management-template-data.png
[api-management-developer-portal-menu]: ./media/api-management-developer-portal-templates/api-management-developer-portal-menu.png
[api-management-management-console]: ./media/api-management-developer-portal-templates/api-management-management-console.png
[api-management-browse]: ./media/api-management-developer-portal-templates/api-management-browse.png
[api-management-user-profile-templates]: ./media/api-management-developer-portal-templates/api-management-user-profile-templates.png
[api-management-save-template]: ./media/api-management-developer-portal-templates/api-management-save-template.png
[api-management-publish-template]: ./media/api-management-developer-portal-templates/api-management-publish-template.png
[api-management-publish-template-confirm]: ./media/api-management-developer-portal-templates/api-management-publish-template-confirm.png
[api-management-publish-templates]: ./media/api-management-developer-portal-templates/api-management-publish-templates.png
[api-management-publish-customizations]: ./media/api-management-developer-portal-templates/api-management-publish-customizations.png
[api-management-revert-template]: ./media/api-management-developer-portal-templates/api-management-revert-template.png
[api-management-revert-template-confirm]: ./media/api-management-developer-portal-templates/api-management-revert-template-confirm.png
[api-management-reset-template]: ./media/api-management-developer-portal-templates/api-management-reset-template.png
[api-management-reset-template-confirm]: ./media/api-management-developer-portal-templates/api-management-reset-template-confirm.png
[api-management-restore-templates]: ./media/api-management-developer-portal-templates/api-management-restore-templates.png







