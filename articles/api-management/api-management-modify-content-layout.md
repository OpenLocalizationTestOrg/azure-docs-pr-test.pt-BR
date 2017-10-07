---
title: "conteúdo da página aaaModify no portal do desenvolvedor Olá no gerenciamento de API do Azure | Microsoft Docs"
description: "Saiba como tooedit página de conteúdo no portal do desenvolvedor Olá no gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: antonba
manager: vlvinogr
editor: 
ms.assetid: 186128fe-41c0-4efb-9efe-2478ad4d103f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/09/2017
ms.author: antonba
ms.openlocfilehash: fd5a854e900d9512518643e593b1b59a0952621f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="modify-hello-content-and-layout-of-pages-on-hello-developer-portal-in-azure-api-management"></a>Modificar o conteúdo de saudação e o layout de páginas no portal do desenvolvedor Olá no gerenciamento de API do Azure
Há três portal do desenvolvedor maneiras fundamentais toocustomize Olá no gerenciamento de API do Azure:

* [Editar conteúdo Olá páginas estáticas e elementos de layout de página] [ modify-content-layout] (explicado neste guia)
* [Atualizar estilos Olá usados para elementos de página entre o portal do desenvolvedor Olá][customize-styles]
* [Modificar modelos de saudação usados para as páginas geradas pelo portal de saudação] [ portal-templates] (por exemplo, documentos de API, produtos, autenticação de usuário, etc.)

## <a name="page-structure"> </a>Estrutura das páginas do portal do desenvolvedor

portal do desenvolvedor Olá baseia-se em um sistema de gerenciamento de conteúdo. layout de saudação de cada página é criado com base no conjunto de elementos da página pequeno conhecido como widgets:

![Estrutura de página do portal do desenvolvedor][api-management-customization-widget-structure]

Todos os widgets são editáveis. 
* Olá core conteúdo específico tooeach cada página residem no widget de "Conteúdo" hello. Edição de uma página significa editando o conteúdo de saudação deste widget.
* Todos os elementos de layout de página estão contidos com os widgets de saudação restantes. As alterações feitas widgets toothese aplicará tooall páginas. Eles serão chamados tooas "widgets layout".

Na página diária editar um geralmente só modifica widget de conteúdo de saudação com conteúdo diferente para cada página.

## <a name="modify-layout-widget"></a>Modificar o conteúdo de saudação de um widget de layout

Conteúdo no portal do desenvolvedor Olá é modificado por meio do portal do publicador Olá acessível pelo Olá Portal do Azure. tooreach-la, clique em **portal do publicador** da barra de ferramentas de serviço de saudação da sua instância de gerenciamento de API.

![Portal do editor][api-management-management-console]

conteúdo Olá tooedit que widget, clique em **Widgets** de saudação **Portal do desenvolvedor** menu Olá esquerda. Para este exemplo permite modificar o conteúdo de saudação do widget de cabeçalho de saudação. Selecione Olá **cabeçalho** widget da lista de saudação.

![Cabeçalho de widget][api-management-widgets-header]

conteúdo de saudação do cabeçalho de saudação é editável de saudação **corpo** campo. Alterar o texto de saudação conforme desejado e, em seguida, clique em **salvar** final Olá Olá página.

Agora você deve ser capaz de toosee Olá novo cabeçalho em cada página no portal do desenvolvedor hello.

> portal do desenvolvedor Olá tooopen no portal do publicador hello, clique em **portal do desenvolvedor** na barra superior hello.
> 
> 

## <a name="edit-page-contents"></a>Editar Olá conteúdo de uma página

toosee Olá lista de todas as páginas de conteúdo existentes, clique em **conteúdo** de saudação **portal do desenvolvedor** menu no portal do publicador hello.

![Gerenciar conteúdo][api-management-customization-manage-content]

Clique em Olá **bem-vindo** página tooedit o que é exibido em Olá home page do portal do desenvolvedor hello. Fazer alterações de saudação você deseja visualizá-los, se necessário e, em seguida, clique em **publicar agora** toomake-los tooeveryone visível.

> home page do Hello usa um layout especial que permite que ele toodisplay uma faixa na parte superior da saudação. Esse cabeçalho não é editável de saudação **conteúdo** seção. tooedit nesse faixa, clique em **Widgets** de saudação **portal do desenvolvedor** menu, selecione **Home page** de saudação **camada atual** suspensa lista e, em seguida, abra Olá **faixa** item sob Olá **em destaque seção**. conteúdo de saudação deste widget é editável, assim como qualquer outra página.
> 
> 

## <a name="next-steps"> </a>Próximas etapas
* [Atualizar estilos Olá usados para elementos de página entre o portal do desenvolvedor Olá][customize-styles]
* [Modificar modelos de saudação usados para as páginas geradas pelo portal de saudação] [ portal-templates] (por exemplo, documentos de API, produtos, autenticação de usuário, etc.)

[Structure of developer portal pages]: #page-structure
[Modifying hello contents of a layout widget]: #modify-layout-widget
[Edit hello contents of a page]: #edit-page-contents
[Next steps]: #next-steps

[modify-content-layout]: api-management-modify-content-layout.md
[customize-styles]: api-management-customize-styles.md
[portal-templates]: api-management-developer-portal-templates.md

[api-management-customization-widget-structure]: ./media/api-management-modify-content-layout/portal-widget-structure.png
[api-management-management-console]: ./media/api-management-modify-content-layout/api-management-management-console.png
[api-management-widgets-header]: ./media/api-management-modify-content-layout/api-management-widgets-header.png
[api-management-customization-manage-content]: ./media/api-management-modify-content-layout/api-management-customization-manage-content.png
