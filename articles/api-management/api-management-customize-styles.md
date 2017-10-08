---
title: "estilos de aaaCustomize no portal do desenvolvedor Olá no gerenciamento de API do Azure | Microsoft Docs"
description: "Saiba como estilos de saudação toomodify usado para qualquer página no portal do desenvolvedor Olá no gerenciamento de API do Azure."
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
ms.openlocfilehash: aaaa86527992ba43e64eab5fd35c7f57b573c812
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hello-styling-of-hello-developer-portal-in-azure-api-management"></a>Personalizar o estilo de saudação do portal do desenvolvedor Olá no gerenciamento de API do Azure
Há três portal do desenvolvedor maneiras fundamentais toocustomize Olá no gerenciamento de API do Azure:

* [Editar conteúdo Olá páginas estáticas e elementos de layout de página][modify-content-layout]
* [Atualizar estilos Olá usados para elementos de página entre o portal do desenvolvedor Olá] [ customize-styles] (explicado neste guia)
* [Modificar modelos de saudação usados para as páginas geradas pelo portal de saudação] [ portal-templates] (por exemplo, documentos de API, produtos, autenticação de usuário, etc.)

## <a name="change-headers-styling"></a>Alterar o estilo de saudação de elementos da página

Olá cores, fontes, tamanhos, espaços e outros elementos relacionados ao estilo de qualquer página no portal de saudação são definidos pelas regras de estilo. 

Editar regras de estilo de saudação é feita da saudação **portal do desenvolvedor** ao que está sendo conectado como um administrador. Há tooget primeiro abra Olá Portal do Azure e clique em **portal do publicador** da barra de ferramentas de serviço de saudação da sua instância de gerenciamento de API.

![Portal do editor][api-management-management-console]

Em seguida, clique em **portal do desenvolvedor** no canto direito superior Olá. 

![Link do portal desenvolvedor no portal do publicador Olá][api-management-pp-dp-link]

barra de ferramentas de personalização de saudação tooopen mova seu mouse sobre o ícone de personalização hello (ou selecioná-la) e, em seguida, clique em "estilos" na barra de ferramentas de saudação.

![Botão da barra de personalização][api-management-customization-toolbar-button]

Há dois forma principal de edição de regras de estilo - você pode examinar a lista de saudação de todas as regras de estilo de saudação usada em qualquer lugar que é exibida por padrão e modifique um estilo conforme necessário, ou você pode escolher **seleciona um elemento na página Olá** e, em seguida, Clique em qualquer lugar no hello toosee somente Olá estilos de página para esse elemento.

![Barra de ferramentas de personalização][api-management-customization-toolbar]

Clique em Olá **seleciona um elemento na página Olá** opção para este exemplo.  Elementos agora se tornam realçados conforme você focalizá-los com hello mouse toosignify estilos do elemento que você começaria edição se você clicou. Mover Olá passe o mouse sobre texto de saudação no cabeçalho da saudação (normalmente você tem o nome de empresa Olá aqui) e depois clique em-lo. Um conjunto de regras de estilo nomeada e categorizados aparece no editor de estilo de saudação. Cada regra representa uma propriedade de estilo do elemento selecionado hello. Por exemplo, para o texto do cabeçalho de saudação selecionado acima, tamanho de saudação do texto de saudação está em @font-size-h1 enquanto Olá nome da fonte de saudação com alternativas está em @headings-font-family.

> Se você estiver familiarizado com [bootstrap][bootstrap], essas regras são na verdade [variáveis LESS] [ LESS variables] no tema de inicialização Olá usado pelo Olá portal do desenvolvedor.
> 
> 

Vamos alterar a cor de saudação do texto do título de saudação. Selecione entrada hello em Olá  **@headings-color**  campo e tipo **#000000**. Este é Olá o código hexadecimal para a cor da saudação preto. Como fazer isso, você verá que um indicador de quadrado de cores é exibido no final de saudação da caixa de texto de saudação. Se você clicar neste indicador, um seletor de cores permite que você toochoose uma cor.

![Seletor de cor][api-management-customization-toolbar-color-picker]

As alterações são visualizadas em tempo real conforme você torná-los, mas é visíveis tooadministrators somente. toomake essas alterações tooeveryone visível, clique em Olá **publicar** botão no editor de estilo hello e confirmar as alterações de saudação.

![Menu Publicar][api-management-customization-toolbar-publish-form]

> Olá toochange estilo regras que se aplicam a tooany outro elemento na página hello, siga Olá mesmo procedimento como você fez para o cabeçalho de saudação. Clique em **seleciona um elemento na página Olá** do editor de estilo hello, elemento select Olá que lhe interessam e início modificando valores Olá Olá de regras de estilo exibidos na tela hello.
> 
> 


## <a name="next-steps"> </a>Próximas etapas
* Saiba como o conteúdo de saudação toocustomize do portal do desenvolvedor páginas usando [modelos portais do desenvolvedor](api-management-developer-portal-templates.md).

[Change hello styling of hello headers]: #change-headers-styling
[Next steps]: #next-steps

[Azure Classic Portal]: https://manage.windowsazure.com/

[api-management-management-console]: ./media/api-management-customize-styles/api-management-management-console.png
[api-management-pp-dp-link]: ./media/api-management-customize-styles/api-management-pp-dp-link.png
[api-management-customization-toolbar-button]: ./media/api-management-customize-styles/api-management-customization-toolbar-button.png
[api-management-customization-toolbar]: ./media/api-management-customize-styles/api-management-customization-toolbar.png
[api-management-customization-toolbar-color-picker]: ./media/api-management-customize-styles/api-management-customization-toolbar-color-picker.png
[api-management-customization-toolbar-publish-form]: ./media/api-management-customize-styles/api-management-customization-toolbar-publish-form.png

[modify-content-layout]: api-management-modify-content-layout.md
[customize-styles]: api-management-customize-styles.md
[portal-templates]: api-management-developer-portal-templates.md

[bootstrap]: http://getbootstrap.com/
[LESS variables]: http://getbootstrap.com/css/
