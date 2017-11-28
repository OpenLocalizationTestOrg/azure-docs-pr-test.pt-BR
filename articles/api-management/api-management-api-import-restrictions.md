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
# <a name="api-import-restrictions-and-known-issues"></a><span data-ttu-id="e1848-103">Restrições de importação de API e problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="e1848-103">API import restrictions and known issues</span></span>
## <a name="about-this-list"></a><span data-ttu-id="e1848-104">Sobre esta lista</span><span class="sxs-lookup"><span data-stu-id="e1848-104">About this list</span></span>
<span data-ttu-id="e1848-105">Enquanto todos os esforços é feito tooensure que importar sua API para gerenciamento de API do Azure é a maneira mais uniforme e livre de problemas possível, podemos ocasionalmente impor restrições ou identificar problemas que precisará toobe corrigida antes de importar com êxito.</span><span class="sxs-lookup"><span data-stu-id="e1848-105">While every effort is made tooensure that importing your API into Azure API Management is as seamless and problem-free as possible, we do occasionally impose restrictions or identify issues that will need toobe rectified before you can successfully import.</span></span> <span data-ttu-id="e1848-106">Este artigo documenta essas, se organizado pelo formato de importação de saudação do hello API.</span><span class="sxs-lookup"><span data-stu-id="e1848-106">This article documents these, organised by hello import format of hello API.</span></span>

## <span data-ttu-id="e1848-107"><a name="open-api"> </a>Open API/Swagger</span><span class="sxs-lookup"><span data-stu-id="e1848-107"><a name="open-api"> </a>Open API/Swagger</span></span>
<span data-ttu-id="e1848-108">Em geral, se você estiver recebendo erros importar seu documento API aberta, verifique se você tiver validado - usando o designer de saudação em Olá novo Portal do Azure (Design - Front-End - abrir Editor de API Specification) ou com um 3ª parte ferramenta como <a href="http://www.swagger.io"> Editor de swagger</a>.</span><span class="sxs-lookup"><span data-stu-id="e1848-108">In general, if you are receiving errors importing your Open API document, please ensure you have validated it - either using hello designer in hello new Azure Portal (Design - Front End - Open API Specification Editor), or with a 3rd party tool such as <a href="http://www.swagger.io">Swagger Editor</a>.</span></span>

* <span data-ttu-id="e1848-109">**Nome do Host** exigimos um atributo de nome de host.</span><span class="sxs-lookup"><span data-stu-id="e1848-109">**Host Name** we require a host name attribute.</span></span>
* <span data-ttu-id="e1848-110">**Caminho Base** exigimos um atributo de caminho base.</span><span class="sxs-lookup"><span data-stu-id="e1848-110">**Base Path** we require a base path attribute.</span></span>
* <span data-ttu-id="e1848-111">**Esquemas** exigimos uma matriz de esquema.</span><span class="sxs-lookup"><span data-stu-id="e1848-111">**Schemes** we require a scheme array.</span></span> 

## <span data-ttu-id="e1848-112"><a name="wsdl"> </a>WSDL</span><span class="sxs-lookup"><span data-stu-id="e1848-112"><a name="wsdl"> </a>WSDL</span></span>
<span data-ttu-id="e1848-113">Arquivos WSDL são usada toogenerate APIs do SOAP de passagem ou servem como Olá back-end da API SOAP para REST.</span><span class="sxs-lookup"><span data-stu-id="e1848-113">WSDL files are used toogenerate SOAP Pass-through APIs, or serve as hello backend of a SOAP-to-REST API.</span></span>

* <span data-ttu-id="e1848-114">**WSDL:Import** no momento, não oferecemos suporte à APIs usando este atributo.</span><span class="sxs-lookup"><span data-stu-id="e1848-114">**WSDL:Import** we do not currently support APIs using this attribute.</span></span> <span data-ttu-id="e1848-115">Os clientes devem mesclar elementos Olá importado em um documento.</span><span class="sxs-lookup"><span data-stu-id="e1848-115">Customers should merge hello imported elements into one document.</span></span>
* <span data-ttu-id="e1848-116">No momento, não há suporte para **Mensagens com diversas partes**.</span><span class="sxs-lookup"><span data-stu-id="e1848-116">**Messages with multiple parts** are currently not supported.</span></span>
* <span data-ttu-id="e1848-117">**wsHttpBinding no WCF** Serviços SOAP criados com o Windows Communication Foundation devem usar basicHttpBinding – não há suporte para wsHttpBinding.</span><span class="sxs-lookup"><span data-stu-id="e1848-117">**WCF wsHttpBinding** SOAP services created with Windows Communication Foundation should use basicHttpBinding - wsHttpBinding is not supported.</span></span>
* <span data-ttu-id="e1848-118">**MTOM** Serviços que usam MTOM <em>podem</em> funcionar.</span><span class="sxs-lookup"><span data-stu-id="e1848-118">**MTOM** Services using MTOM <em>may</em> work.</span></span> <span data-ttu-id="e1848-119">No momento, não oferecemos suporte oficial.</span><span class="sxs-lookup"><span data-stu-id="e1848-119">Official support is not offered at this time.</span></span>
* <span data-ttu-id="e1848-120">**Recursão** tipos que são definidos recursivamente (por exemplo, consulte tooan matriz de si mesmos) não têm suporte.</span><span class="sxs-lookup"><span data-stu-id="e1848-120">**Recursion** types that are defined recursively (e.g. refer tooan array of themselves) are not supported.</span></span>

## <span data-ttu-id="e1848-121"><a name="wadl"> </a>WADL</span><span class="sxs-lookup"><span data-stu-id="e1848-121"><a name="wadl"> </a>WADL</span></span>
<span data-ttu-id="e1848-122">Atualmente, não há problemas de importação de WADL conhecidos.</span><span class="sxs-lookup"><span data-stu-id="e1848-122">There are no known WADL import issues currently.</span></span>


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
