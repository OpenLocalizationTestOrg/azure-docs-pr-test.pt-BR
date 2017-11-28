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
# <a name="how-tooimport-hello-definition-of-an-api-with-operations-in-azure-api-management"></a><span data-ttu-id="f8754-103">Como tooimport Olá a definição de uma API com operações no gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="f8754-103">How tooimport hello definition of an API with operations in Azure API Management</span></span>
<span data-ttu-id="f8754-104">No gerenciamento de API, novas APIs podem ser criados e operações de saudação adicionadas manualmente ou Olá API pode ser importados juntamente com operações de saudação em uma única etapa.</span><span class="sxs-lookup"><span data-stu-id="f8754-104">In API Management, new APIs can be created and hello operations added manually, or hello API can be imported along with hello operations in one step.</span></span>

<span data-ttu-id="f8754-105">APIs e suas operações podem ser importadas usando Olá formatos a seguir.</span><span class="sxs-lookup"><span data-stu-id="f8754-105">APIs and their operations can be imported using hello following formats.</span></span>

* <span data-ttu-id="f8754-106">WADL</span><span class="sxs-lookup"><span data-stu-id="f8754-106">WADL</span></span>
* <span data-ttu-id="f8754-107">Swagger</span><span class="sxs-lookup"><span data-stu-id="f8754-107">Swagger</span></span>

<span data-ttu-id="f8754-108">Este guia mostra como criar uma nova API e importar suas operações em uma etapa.</span><span class="sxs-lookup"><span data-stu-id="f8754-108">This guide shows how create a new API and import its operations in one step.</span></span> <span data-ttu-id="f8754-109">Para obter informações sobre como criar manualmente uma API e adição de operações, consulte [como toocreate APIs] [ How toocreate APIs] e [como tooadd operações tooan API] [ How tooadd operations tooan API].</span><span class="sxs-lookup"><span data-stu-id="f8754-109">For information on manually creating an API and adding operations, see [How toocreate APIs][How toocreate APIs] and [How tooadd operations tooan API][How tooadd operations tooan API].</span></span>

## <span data-ttu-id="f8754-110"><a name="import-api"> </a>Importar uma API</span><span class="sxs-lookup"><span data-stu-id="f8754-110"><a name="import-api"> </a>Import an API</span></span>
<span data-ttu-id="f8754-111">APIs são criados e configurados no portal do publicador hello.</span><span class="sxs-lookup"><span data-stu-id="f8754-111">APIs are created and configured in hello publisher portal.</span></span> <span data-ttu-id="f8754-112">tooaccess Olá clique portal, publisher **portal do publicador** em hello Portal do Azure para seu serviço de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="f8754-112">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="f8754-113">Se você ainda não tiver criado uma instância do serviço de gerenciamento de API, consulte [criar uma instância do serviço de gerenciamento de API] [ Create an API Management service instance] em Olá [Introdução ao gerenciamento de API do Azure] [ Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="f8754-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![Portal do editor][api-management-management-console]

<span data-ttu-id="f8754-115">Clique em **APIs** de saudação **gerenciamento de API** menu saudação à esquerda e clique **importar API**.</span><span class="sxs-lookup"><span data-stu-id="f8754-115">Click **APIs** from hello **API Management** menu on hello left, and then click **import API**.</span></span>

![Importar API][api-management-import-apis]

<span data-ttu-id="f8754-117">Olá **importação API** janela tem três guias que correspondem a especificação do toohello três maneiras tooprovide Olá API.</span><span class="sxs-lookup"><span data-stu-id="f8754-117">hello **Import API** window has three tabs that correspond toohello three ways tooprovide hello API specification.</span></span>

* <span data-ttu-id="f8754-118">**Na área de transferência** permite que você toopaste especificação de saudação API na caixa de texto designado de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8754-118">**From clipboard** allows you toopaste hello API specification into hello designated text box.</span></span>
* <span data-ttu-id="f8754-119">**Do arquivo** permite você toobrowse tooand Olá select de arquivos que contém a especificação de saudação API.</span><span class="sxs-lookup"><span data-stu-id="f8754-119">**From file** allows you toobrowse tooand select hello file that contains hello API specification.</span></span>
* <span data-ttu-id="f8754-120">**De URL** permite que você toosupply Olá URL toohello especificação Olá API.</span><span class="sxs-lookup"><span data-stu-id="f8754-120">**From URL** allows you toosupply hello URL toohello specification for hello API.</span></span>

![Importar formato de API][api-management-import-api-clipboard]

<span data-ttu-id="f8754-122">Depois de fornecer especificação Olá API, use os botões de opção de saudação no formato de especificação de Olá Olá tooindicate à direita.</span><span class="sxs-lookup"><span data-stu-id="f8754-122">After providing hello API specification, use hello radio buttons on hello right tooindicate hello specification format.</span></span> <span data-ttu-id="f8754-123">Olá formatos a seguir têm suporte.</span><span class="sxs-lookup"><span data-stu-id="f8754-123">hello following formats are supported.</span></span>

* <span data-ttu-id="f8754-124">WADL</span><span class="sxs-lookup"><span data-stu-id="f8754-124">WADL</span></span>
* <span data-ttu-id="f8754-125">Swagger</span><span class="sxs-lookup"><span data-stu-id="f8754-125">Swagger</span></span>

<span data-ttu-id="f8754-126">Em seguida, insira um **sufixo de URL de API Web**.</span><span class="sxs-lookup"><span data-stu-id="f8754-126">Next, enter a **Web API URL suffix**.</span></span> <span data-ttu-id="f8754-127">Esta é a URL base toohello anexado para seu serviço de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="f8754-127">This is appended toohello base URL for your API management service.</span></span> <span data-ttu-id="f8754-128">URL base Olá é comum para todas as APIs hospedadas em cada instância de um serviço de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="f8754-128">hello base URL is common for all APIs hosted on each instance of an API Management service.</span></span> <span data-ttu-id="f8754-129">Gerenciamento de API distingue APIs pelo seu sufixo e, portanto, o sufixo de saudação deve ser exclusivo para cada API em uma instância de serviço de gerenciamento de API específica.</span><span class="sxs-lookup"><span data-stu-id="f8754-129">API Management distinguishes APIs by their suffix and therefore hello suffix must be unique for every API in a specific API management service instance.</span></span>

<span data-ttu-id="f8754-130">Depois que todos os valores são inseridos, clique em **salvar** toocreate Olá API e hello associaram a operações.</span><span class="sxs-lookup"><span data-stu-id="f8754-130">Once all values are entered, click **Save** toocreate hello API and hello associated operations.</span></span> 

> [!NOTE]
> <span data-ttu-id="f8754-131">Para obter um tutorial de importação de uma API básica de calculadora no formato Swagger, consulte [Gerenciar sua primeira API no Gerenciamento de API do Azure](api-management-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f8754-131">For a tutorial of importing a basic calculator API in Swagger format, see [Manage your first API in Azure API Management](api-management-get-started.md).</span></span>
> 
> 

## <span data-ttu-id="f8754-132"><a name="export-api"> </a> Exportar uma API</span><span class="sxs-lookup"><span data-stu-id="f8754-132"><a name="export-api"> </a> Export an API</span></span>
<span data-ttu-id="f8754-133">Em adição tooimporting novas APIs, você pode exportar definições de saudação de suas APIs do portal do publicador hello.</span><span class="sxs-lookup"><span data-stu-id="f8754-133">In addition tooimporting new APIs, you can export hello definitions of your APIs from hello publisher portal.</span></span> <span data-ttu-id="f8754-134">toodo, clique em **exportar API** de saudação **guia Resumo** de seu **API**.</span><span class="sxs-lookup"><span data-stu-id="f8754-134">toodo so, click **Export API** from hello **Summary tab** of your **API**.</span></span>

![Exportar API][api-management-export-api]

<span data-ttu-id="f8754-136">As APIs podem ser exportadas usando WADL ou Swagger.</span><span class="sxs-lookup"><span data-stu-id="f8754-136">APIs can be exported using WADL or Swagger.</span></span> <span data-ttu-id="f8754-137">Selecione o formato de saudação desejado, clique em **salvar**e escolha o local de saudação no qual o arquivo hello toosave.</span><span class="sxs-lookup"><span data-stu-id="f8754-137">Select hello desired format, click **Save**, and choose hello location in which toosave hello file.</span></span>

![Exportar formato de API][api-management-export-api-format]

## <span data-ttu-id="f8754-139"><a name="next-steps"> </a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f8754-139"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="f8754-140">Depois que uma API é criada e operações de saudação importadas, você pode revisar e configurar as configurações adicionais, adicione Olá API tooa produto e publicá-lo para que ele está disponível para desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="f8754-140">Once an API is created and hello operations imported, you can review and configure any additional settings, add hello API tooa Product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="f8754-141">Para obter mais informações, consulte Olá guias a seguir.</span><span class="sxs-lookup"><span data-stu-id="f8754-141">For more information, see hello following guides.</span></span>

* <span data-ttu-id="f8754-142">[Como as configurações de tooconfigure API][How tooconfigure API settings]</span><span class="sxs-lookup"><span data-stu-id="f8754-142">[How tooconfigure API settings][How tooconfigure API settings]</span></span>
* <span data-ttu-id="f8754-143">[Como toocreate e publicar um produto][How toocreate and publish a product]</span><span class="sxs-lookup"><span data-stu-id="f8754-143">[How toocreate and publish a product][How toocreate and publish a product]</span></span>

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
