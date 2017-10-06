---
title: Importar aaaRestrictions e problemas conhecidos na API de gerenciamento de API do Azure | Microsoft Docs
description: "Detalhes dos problemas conhecidos e as restrições na importação para o gerenciamento de API do Azure usando os formatos de API aberta, WSDL ou WADL hello."
services: api-management
documentationcenter: 
author: mattfarm
manager: vlvinogr
editor: 
ms.assetid: 7a5a63f0-3e72-49d3-a28c-1bb23ab495e2
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: apipm
ms.openlocfilehash: 0bed5ace47de6ccbfbecba25ea6b69c5329de089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="api-import-restrictions-and-known-issues"></a>Restrições de importação de API e problemas conhecidos
## <a name="about-this-list"></a>Sobre esta lista
Enquanto todos os esforços é feito tooensure que importar sua API para gerenciamento de API do Azure é a maneira mais uniforme e livre de problemas possível, podemos ocasionalmente impor restrições ou identificar problemas que precisará toobe corrigida antes de importar com êxito. Este artigo documenta essas, se organizado pelo formato de importação de saudação do hello API.

## <a name="open-api"> </a>Open API/Swagger
Em geral, se você estiver recebendo erros importar seu documento API aberta, verifique se você tiver validado - usando o designer de saudação em Olá novo Portal do Azure (Design - Front-End - abrir Editor de API Specification) ou com um 3ª parte ferramenta como <a href="http://www.swagger.io"> Editor de swagger</a>.

* **Nome do Host** exigimos um atributo de nome de host.
* **Caminho Base** exigimos um atributo de caminho base.
* **Esquemas** exigimos uma matriz de esquema. 

## <a name="wsdl"> </a>WSDL
Arquivos WSDL são usada toogenerate APIs do SOAP de passagem ou servem como Olá back-end da API SOAP para REST.

* **WSDL:Import** no momento, não oferecemos suporte à APIs usando este atributo. Os clientes devem mesclar elementos Olá importado em um documento.
* No momento, não há suporte para **Mensagens com diversas partes**.
* **wsHttpBinding no WCF** Serviços SOAP criados com o Windows Communication Foundation devem usar basicHttpBinding – não há suporte para wsHttpBinding.
* **MTOM** Serviços que usam MTOM <em>podem</em> funcionar. No momento, não oferecemos suporte oficial.
* **Recursão** tipos que são definidos recursivamente (por exemplo, consulte tooan matriz de si mesmos) não têm suporte.

## <a name="wadl"> </a>WADL
Atualmente, não há problemas de importação de WADL conhecidos.


[api-management-management-console]: ./media/api-management-howto-add-operations/api-management-management-console.png
[api-management-operations]: ./media/api-management-howto-add-operations/api-management-operations.png
[api-management-add-operation]: ./media/api-management-howto-add-operations/api-management-add-operation.png
[api-management-http-method]: ./media/api-management-howto-add-operations/api-management-http-method.png
[api-management-url-template]: ./media/api-management-howto-add-operations/api-management-url-template.png
[api-management-url-template-rewrite]: ./media/api-management-howto-add-operations/api-management-url-template-rewrite.png
[api-management-description]: ./media/api-management-howto-add-operations/api-management-description.png
[api-management-caching-tab]: ./media/api-management-howto-add-operations/api-management-caching-tab.png
[api-management-request-parameters]: ./media/api-management-howto-add-operations/api-management-request-parameters.png
[api-management-request-body]: ./media/api-management-howto-add-operations/api-management-request-body.png
[api-management-response-code]: ./media/api-management-howto-add-operations/api-management-response-code.png
[api-management-response-body-content-type]: ./media/api-management-howto-add-operations/api-management-response-body-content-type.png
[api-management-response-body]: ./media/api-management-howto-add-operations/api-management-response-body.png


[api-management-contoso-api]: ./media/api-management-howto-add-operations/api-management-contoso-api.png

[api-management-add-new-api]: ./media/api-management-howto-add-operations/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-add-operations/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-add-operations/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-add-operations/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-add-operations/api-management-echo-operations.png

[Add an operation]: #add-operation
[Operation caching]: #operation-caching
[Request parameters]: #request-parameters
[Request body]: #request-body
[Responses]: #responses
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocache operation results in Azure API Management]: api-management-howto-cache.md
