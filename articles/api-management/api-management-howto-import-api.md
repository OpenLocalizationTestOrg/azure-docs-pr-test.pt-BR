---
title: aaaImport uma API para o gerenciamento de API do Azure | Microsoft Docs
description: "Saiba como tooimport uma API e suas operações de gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 40398b0a-ac2c-43f0-89e1-07e4abbf502f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 20fbbb53243aecc24d72833ec0904ae8fab97863
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimport-hello-definition-of-an-api-with-operations-in-azure-api-management"></a>Como tooimport Olá a definição de uma API com operações no gerenciamento de API do Azure
No gerenciamento de API, novas APIs podem ser criados e operações de saudação adicionadas manualmente ou Olá API pode ser importados juntamente com operações de saudação em uma única etapa.

APIs e suas operações podem ser importadas usando Olá formatos a seguir.

* WADL
* Swagger

Este guia mostra como criar uma nova API e importar suas operações em uma etapa. Para obter informações sobre como criar manualmente uma API e adição de operações, consulte [como toocreate APIs] [ How toocreate APIs] e [como tooadd operações tooan API] [ How tooadd operations tooan API].

## <a name="import-api"> </a>Importar uma API
APIs são criados e configurados no portal do publicador hello. tooaccess Olá clique portal, publisher **portal do publicador** em hello Portal do Azure para seu serviço de gerenciamento de API. Se você ainda não tiver criado uma instância do serviço de gerenciamento de API, consulte [criar uma instância do serviço de gerenciamento de API] [ Create an API Management service instance] em Olá [Introdução ao gerenciamento de API do Azure] [ Get started with Azure API Management] tutorial.

![Portal do editor][api-management-management-console]

Clique em **APIs** de saudação **gerenciamento de API** menu saudação à esquerda e clique **importar API**.

![Importar API][api-management-import-apis]

Olá **importação API** janela tem três guias que correspondem a especificação do toohello três maneiras tooprovide Olá API.

* **Na área de transferência** permite que você toopaste especificação de saudação API na caixa de texto designado de saudação.
* **Do arquivo** permite você toobrowse tooand Olá select de arquivos que contém a especificação de saudação API.
* **De URL** permite que você toosupply Olá URL toohello especificação Olá API.

![Importar formato de API][api-management-import-api-clipboard]

Depois de fornecer especificação Olá API, use os botões de opção de saudação no formato de especificação de Olá Olá tooindicate à direita. Olá formatos a seguir têm suporte.

* WADL
* Swagger

Em seguida, insira um **sufixo de URL de API Web**. Esta é a URL base toohello anexado para seu serviço de gerenciamento de API. URL base Olá é comum para todas as APIs hospedadas em cada instância de um serviço de gerenciamento de API. Gerenciamento de API distingue APIs pelo seu sufixo e, portanto, o sufixo de saudação deve ser exclusivo para cada API em uma instância de serviço de gerenciamento de API específica.

Depois que todos os valores são inseridos, clique em **salvar** toocreate Olá API e hello associaram a operações. 

> [!NOTE]
> Para obter um tutorial de importação de uma API básica de calculadora no formato Swagger, consulte [Gerenciar sua primeira API no Gerenciamento de API do Azure](api-management-get-started.md).
> 
> 

## <a name="export-api"> </a> Exportar uma API
Em adição tooimporting novas APIs, você pode exportar definições de saudação de suas APIs do portal do publicador hello. toodo, clique em **exportar API** de saudação **guia Resumo** de seu **API**.

![Exportar API][api-management-export-api]

As APIs podem ser exportadas usando WADL ou Swagger. Selecione o formato de saudação desejado, clique em **salvar**e escolha o local de saudação no qual o arquivo hello toosave.

![Exportar formato de API][api-management-export-api-format]

## <a name="next-steps"> </a>Próximas etapas
Depois que uma API é criada e operações de saudação importadas, você pode revisar e configurar as configurações adicionais, adicione Olá API tooa produto e publicá-lo para que ele está disponível para desenvolvedores. Para obter mais informações, consulte Olá guias a seguir.

* [Como as configurações de tooconfigure API][How tooconfigure API settings]
* [Como toocreate e publicar um produto][How toocreate and publish a product]

[api-management-management-console]: ./media/api-management-howto-import-api/api-management-management-console.png
[api-management-import-apis]: ./media/api-management-howto-import-api/api-management-api-import-apis.png
[api-management-import-api-clipboard]: ./media/api-management-howto-import-api/api-management-import-api-wizard.png
[api-management-export-api]: ./media/api-management-howto-import-api/api-management-export-api.png
[api-management-export-api-format]: ./media/api-management-howto-import-api/api-management-export-api-format.png

[Import an API]: #import-api
[Export an API]: #export-api
[Configure API settings]: #configure-api-settings
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocreate APIs]: api-management-howto-create-apis.md
[How tooconfigure API settings]: api-management-howto-create-apis.md#configure-api-settings
