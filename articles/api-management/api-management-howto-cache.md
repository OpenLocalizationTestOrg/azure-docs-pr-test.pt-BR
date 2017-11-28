---
title: aaaAdd cache tooimprove desempenho no gerenciamento de API do Azure | Microsoft Docs
description: "Saiba como latência de saudação tooimprove, consumo de largura de banda e serviço web de carga para chamadas de serviço de gerenciamento de API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 740f6a27-8323-474d-ade2-828ae0c75e7a
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 056ab7cf788218327e30bd5c028b76e3b1977fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-caching-tooimprove-performance-in-azure-api-management"></a><span data-ttu-id="918f0-103">Adicionar cache tooimprove desempenho no gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="918f0-103">Add caching tooimprove performance in Azure API Management</span></span>
<span data-ttu-id="918f0-104">É possível configurar as operações do Gerenciamento de API para cache das respostas.</span><span class="sxs-lookup"><span data-stu-id="918f0-104">Operations in API Management can be configured for response caching.</span></span> <span data-ttu-id="918f0-105">O cache das respostas pode reduzir significativamente a latência da API, o consumo da largura de banda e a carga de serviço Web para dados que não são alterados com frequência.</span><span class="sxs-lookup"><span data-stu-id="918f0-105">Response caching can significantly reduce API latency, bandwidth consumption, and web service load for data that does not change frequently.</span></span>

<span data-ttu-id="918f0-106">Este guia mostra como tooadd resposta para a sua API de cache e configurar políticas para operações de API de eco do exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="918f0-106">This guide shows you how tooadd response caching for your API and configure policies for hello sample Echo API operations.</span></span> <span data-ttu-id="918f0-107">Em seguida, você pode chamar operação Olá do cache tooverify portal do desenvolvedor do hello em ação.</span><span class="sxs-lookup"><span data-stu-id="918f0-107">You can then call hello operation from hello developer portal tooverify caching in action.</span></span>

> [!NOTE]
> <span data-ttu-id="918f0-108">Para saber mais sobre itens de cache por chave usando expressões de política, confira [Cache personalizado no Gerenciamento de API do Azure](api-management-sample-cache-by-key.md).</span><span class="sxs-lookup"><span data-stu-id="918f0-108">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="918f0-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="918f0-109">Prerequisites</span></span>
<span data-ttu-id="918f0-110">Antes de saudação seguir as etapas neste guia, você deve ter uma instância do serviço de gerenciamento de API com uma API e um produto configurado.</span><span class="sxs-lookup"><span data-stu-id="918f0-110">Before following hello steps in this guide, you must have an API Management service instance with an API and a product configured.</span></span> <span data-ttu-id="918f0-111">Se você ainda não tiver criado uma instância do serviço de gerenciamento de API, consulte [criar uma instância do serviço de gerenciamento de API] [ Create an API Management service instance] em Olá [Introdução ao gerenciamento de API do Azure] [ Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="918f0-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

## <span data-ttu-id="918f0-112"><a name="configure-caching"> </a>Configurar uma operação para caching</span><span class="sxs-lookup"><span data-stu-id="918f0-112"><a name="configure-caching"> </a>Configure an operation for caching</span></span>
<span data-ttu-id="918f0-113">Nesta etapa, você revisará Olá configurações de saudação de cache **obter recursos (em cache)** operação do exemplo hello Echo API.</span><span class="sxs-lookup"><span data-stu-id="918f0-113">In this step, you will review hello caching settings of hello **GET Resource (cached)** operation of hello sample Echo API.</span></span>

> [!NOTE]
> <span data-ttu-id="918f0-114">Cada instância de serviço de gerenciamento de API vem pré-configurada com uma API de eco que podem ser usado tooexperiment com e saiba mais sobre o gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="918f0-114">Each API Management service instance comes preconfigured with an Echo API that can be used tooexperiment with and learn about API Management.</span></span> <span data-ttu-id="918f0-115">Para obter mais informações, confira [Introdução ao Gerenciamento de API do Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="918f0-115">For more information, see [Get started with Azure API Management][Get started with Azure API Management].</span></span>
> 
> 

<span data-ttu-id="918f0-116">tooget iniciado, clique em **portal do publicador** em hello Portal do Azure para seu serviço de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="918f0-116">tooget started, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="918f0-117">Isso leva toohello portal do publicador de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="918f0-117">This takes you toohello API Management publisher portal.</span></span>

![Portal do editor][api-management-management-console]

<span data-ttu-id="918f0-119">Clique em **APIs** de saudação **gerenciamento de API** menu saudação à esquerda e clique **Echo API**.</span><span class="sxs-lookup"><span data-stu-id="918f0-119">Click **APIs** from hello **API Management** menu on hello left, and then click **Echo API**.</span></span>

![API de Eco][api-management-echo-api]

<span data-ttu-id="918f0-121">Clique em Olá **operações** guia e, em seguida, clique em Olá **obter recursos (em cache)** operação Olá **operações** lista.</span><span class="sxs-lookup"><span data-stu-id="918f0-121">Click hello **Operations** tab, and then click hello **GET Resource (cached)** operation from hello **Operations** list.</span></span>

![Operações de API de ECO][api-management-echo-api-operations]

<span data-ttu-id="918f0-123">Clique em Olá **cache** Olá tooview de guia Configurações para esta operação de cache.</span><span class="sxs-lookup"><span data-stu-id="918f0-123">Click hello **Caching** tab tooview hello caching settings for this operation.</span></span>

![Guia Cache][api-management-caching-tab]

<span data-ttu-id="918f0-125">tooenable cache para uma operação, selecione Olá **habilitar** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="918f0-125">tooenable caching for an operation, select hello **Enable** check box.</span></span> <span data-ttu-id="918f0-126">Neste exemplo, o caching está habilitado.</span><span class="sxs-lookup"><span data-stu-id="918f0-126">In this example, caching is enabled.</span></span>

<span data-ttu-id="918f0-127">Cada resposta de operação é organizada com base nos valores Olá Olá **variar por parâmetros de cadeia de caracteres de consulta** e **variam por cabeçalhos** campos.</span><span class="sxs-lookup"><span data-stu-id="918f0-127">Each operation response is keyed, based on hello values in hello **Vary by query string parameters** and **Vary by headers** fields.</span></span> <span data-ttu-id="918f0-128">Se você quiser toocache várias respostas com base em parâmetros de cadeia de caracteres de consulta ou cabeçalhos, você pode configurá-los nesses dois campos.</span><span class="sxs-lookup"><span data-stu-id="918f0-128">If you want toocache multiple responses based on query string parameters or headers, you can configure them in these two fields.</span></span>

<span data-ttu-id="918f0-129">**Duração** Especifica o intervalo de expiração de saudação de respostas de saudação armazenado em cache.</span><span class="sxs-lookup"><span data-stu-id="918f0-129">**Duration** specifies hello expiration interval of hello cached responses.</span></span> <span data-ttu-id="918f0-130">Neste exemplo, o intervalo de saudação é **3600** segundos, que é hora de tooone equivalente.</span><span class="sxs-lookup"><span data-stu-id="918f0-130">In this example, hello interval is **3600** seconds, which is equivalent tooone hour.</span></span>

<span data-ttu-id="918f0-131">Usando Olá configuração neste exemplo de cache, Olá primeiro toohello de solicitação **obter recursos (em cache)** operação retorna uma resposta do serviço de back-end de saudação.</span><span class="sxs-lookup"><span data-stu-id="918f0-131">Using hello caching configuration in this example, hello first request toohello **GET Resource (cached)** operation returns a response from hello backend service.</span></span> <span data-ttu-id="918f0-132">Essa resposta será armazenada, chaveado Olá especificado parâmetros de cadeia de caracteres de cabeçalhos e consulta.</span><span class="sxs-lookup"><span data-stu-id="918f0-132">This response will be cached, keyed by hello specified headers and query string parameters.</span></span> <span data-ttu-id="918f0-133">Chamadas subsequentes operação toohello, com parâmetros, será necessário Olá armazenados em cache resposta retornada, até que o intervalo de duração do cache de saudação expirou.</span><span class="sxs-lookup"><span data-stu-id="918f0-133">Subsequent calls toohello operation, with matching parameters, will have hello cached response returned, until hello cache duration interval has expired.</span></span>

## <span data-ttu-id="918f0-134"><a name="caching-policies"></a>Olá revisão políticas de cache</span><span class="sxs-lookup"><span data-stu-id="918f0-134"><a name="caching-policies"> </a>Review hello caching policies</span></span>
<span data-ttu-id="918f0-135">Nesta etapa, você examine Olá cache configurações para Olá **obter recursos (em cache)** operação do exemplo hello Echo API.</span><span class="sxs-lookup"><span data-stu-id="918f0-135">In this step, you review hello caching settings for hello **GET Resource (cached)** operation of hello sample Echo API.</span></span>

<span data-ttu-id="918f0-136">Quando as configurações de cache são configuradas para uma operação em Olá **cache** guia cache políticas são adicionadas para a operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="918f0-136">When caching settings are configured for an operation on hello **Caching** tab, caching policies are added for hello operation.</span></span> <span data-ttu-id="918f0-137">Essas políticas podem ser exibidas e editadas no editor de diretiva de saudação.</span><span class="sxs-lookup"><span data-stu-id="918f0-137">These policies can be viewed and edited in hello policy editor.</span></span>

<span data-ttu-id="918f0-138">Clique em **políticas** de saudação **gerenciamento de API** menu Olá esquerdo e, em seguida, selecione **Echo API / obter recursos (em cache)** de saudação **operação**lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="918f0-138">Click **Policies** from hello **API Management** menu on hello left, and then select **Echo API / GET Resource (cached)** from hello **Operation** drop-down list.</span></span>

![Operação de escopo da política][api-management-operation-dropdown]

<span data-ttu-id="918f0-140">Isso exibe políticas Olá para esta operação no editor de diretiva de saudação.</span><span class="sxs-lookup"><span data-stu-id="918f0-140">This displays hello policies for this operation in hello policy editor.</span></span>

![Editor de políticas de Gerenciamento de API][api-management-policy-editor]

<span data-ttu-id="918f0-142">definição de política de saudação para essa operação inclui Olá as políticas que definem Olá configuração de cache que foram examinadas usando Olá **cache** guia na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="918f0-142">hello policy definition for this operation includes hello policies that define hello caching configuration that were reviewed using hello **Caching** tab in hello previous step.</span></span>

```xml
<policies>
    <inbound>
        <base />
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false">
            <vary-by-header>Accept</vary-by-header>
            <vary-by-header>Accept-Charset</vary-by-header>
        </cache-lookup>
        <rewrite-uri template="/resource" />
    </inbound>
    <outbound>
        <base />
        <cache-store caching-mode="cache-on" duration="3600" />
    </outbound>
</policies>
```

> [!NOTE]
> <span data-ttu-id="918f0-143">As alterações feitas toohello políticas no editor de diretiva de saudação de cache será refletida no hello **cache** guia de uma operação e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="918f0-143">Changes made toohello caching policies in hello policy editor will be reflected on hello **Caching** tab of an operation, and vice-versa.</span></span>
> 
> 

## <span data-ttu-id="918f0-144"><a name="test-operation"></a>Chamar uma operação e testar o caching Olá</span><span class="sxs-lookup"><span data-stu-id="918f0-144"><a name="test-operation"> </a>Call an operation and test hello caching</span></span>
<span data-ttu-id="918f0-145">Olá toosee cache em ação, podemos chamar a operação de saudação do portal do desenvolvedor Olá.</span><span class="sxs-lookup"><span data-stu-id="918f0-145">toosee hello caching in action, we can call hello operation from hello developer portal.</span></span> <span data-ttu-id="918f0-146">Clique em **portal do desenvolvedor** no menu superior direito da saudação.</span><span class="sxs-lookup"><span data-stu-id="918f0-146">Click **Developer portal** in hello top right menu.</span></span>

![Portal do desenvolvedor][api-management-developer-portal-menu]

<span data-ttu-id="918f0-148">Clique em **APIs** Olá menu superior e, em seguida, selecione **Echo API**.</span><span class="sxs-lookup"><span data-stu-id="918f0-148">Click **APIs** in hello top menu, and then select **Echo API**.</span></span>

![API de Eco][api-management-apis-echo-api]

> <span data-ttu-id="918f0-150">Se você tiver apenas uma API configurada ou conta tooyour visível, clique em APIs leva você diretamente toohello operações para essa API.</span><span class="sxs-lookup"><span data-stu-id="918f0-150">If you have only one API configured or visible tooyour account, then clicking APIs takes you directly toohello operations for that API.</span></span>
> 
> 

<span data-ttu-id="918f0-151">Selecione Olá **obter recursos (em cache)** operação e depois clique em **abrir o Console**.</span><span class="sxs-lookup"><span data-stu-id="918f0-151">Select hello **GET Resource (cached)** operation, and then click **Open Console**.</span></span>

![Abrir console][api-management-open-console]

<span data-ttu-id="918f0-153">Olá console permite operações tooinvoke diretamente do portal do desenvolvedor hello.</span><span class="sxs-lookup"><span data-stu-id="918f0-153">hello console allows you tooinvoke operations directly from hello developer portal.</span></span>

![Console][api-management-console]

<span data-ttu-id="918f0-155">Manter valores padrão Olá **param1** e **param2**.</span><span class="sxs-lookup"><span data-stu-id="918f0-155">Keep hello default values for **param1** and **param2**.</span></span>

<span data-ttu-id="918f0-156">Selecione Olá tecla desejada da saudação **chave de assinatura** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="918f0-156">Select hello desired key from hello **subscription-key** drop-down list.</span></span> <span data-ttu-id="918f0-157">Se a sua conta tiver somente uma assinatura, ela já estará selecionada.</span><span class="sxs-lookup"><span data-stu-id="918f0-157">If your account has only one subscription, it will already be selected.</span></span>

<span data-ttu-id="918f0-158">Digite **sampleheader:value1** em Olá **cabeçalhos de solicitação** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="918f0-158">Enter **sampleheader:value1** in hello **Request headers** text box.</span></span>

<span data-ttu-id="918f0-159">Clique em **HTTP Get** e anote Olá cabeçalhos de resposta.</span><span class="sxs-lookup"><span data-stu-id="918f0-159">Click **HTTP Get** and make a note of hello response headers.</span></span>

<span data-ttu-id="918f0-160">Digite **sampleheader:value2** em Olá **cabeçalhos de solicitação** caixa de texto e clique **HTTP Get**.</span><span class="sxs-lookup"><span data-stu-id="918f0-160">Enter **sampleheader:value2** in hello **Request headers** text box, and then click **HTTP Get**.</span></span>

<span data-ttu-id="918f0-161">Observe que valor Olá **sampleheader** ainda é **value1** em resposta hello.</span><span class="sxs-lookup"><span data-stu-id="918f0-161">Note that hello value of **sampleheader** is still **value1** in hello response.</span></span> <span data-ttu-id="918f0-162">Tente alguns valores diferentes e observe que Olá a resposta armazenada em cache na primeira chamada de saudação é retornado.</span><span class="sxs-lookup"><span data-stu-id="918f0-162">Try some different values and note that hello cached response from hello first call is returned.</span></span>

<span data-ttu-id="918f0-163">Digite **25** em Olá **param2** campo e, em seguida, clique em **HTTP Get**.</span><span class="sxs-lookup"><span data-stu-id="918f0-163">Enter **25** into hello **param2** field, and then click **HTTP Get**.</span></span>

<span data-ttu-id="918f0-164">Observe que valor Olá **sampleheader** Olá resposta agora é **value2**.</span><span class="sxs-lookup"><span data-stu-id="918f0-164">Note that hello value of **sampleheader** in hello response is now **value2**.</span></span> <span data-ttu-id="918f0-165">Porque os resultados da operação Olá inseridos pela cadeia de caracteres de consulta, a resposta armazenada em cache anterior de saudação não foi retornada.</span><span class="sxs-lookup"><span data-stu-id="918f0-165">Because hello operation results are keyed by query string, hello previous cached response was not returned.</span></span>

## <span data-ttu-id="918f0-166"><a name="next-steps"> </a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="918f0-166"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="918f0-167">Para obter mais informações sobre políticas de cache, consulte [políticas de cache] [ Caching policies] em Olá [referência de política de gerenciamento de API][API Management policy reference].</span><span class="sxs-lookup"><span data-stu-id="918f0-167">For more information about caching policies, see [Caching policies][Caching policies] in hello [API Management policy reference][API Management policy reference].</span></span>
* <span data-ttu-id="918f0-168">Para saber mais sobre itens de cache por chave usando expressões de política, confira [Cache personalizado no Gerenciamento de API do Azure](api-management-sample-cache-by-key.md).</span><span class="sxs-lookup"><span data-stu-id="918f0-168">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span></span>

[api-management-management-console]: ./media/api-management-howto-cache/api-management-management-console.png
[api-management-echo-api]: ./media/api-management-howto-cache/api-management-echo-api.png
[api-management-echo-api-operations]: ./media/api-management-howto-cache/api-management-echo-api-operations.png
[api-management-caching-tab]: ./media/api-management-howto-cache/api-management-caching-tab.png
[api-management-operation-dropdown]: ./media/api-management-howto-cache/api-management-operation-dropdown.png
[api-management-policy-editor]: ./media/api-management-howto-cache/api-management-policy-editor.png
[api-management-developer-portal-menu]: ./media/api-management-howto-cache/api-management-developer-portal-menu.png
[api-management-apis-echo-api]: ./media/api-management-howto-cache/api-management-apis-echo-api.png
[api-management-open-console]: ./media/api-management-howto-cache/api-management-open-console.png
[api-management-console]: ./media/api-management-howto-cache/api-management-console.png


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md

[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx

[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Configure an operation for caching]: #configure-caching
[Review hello caching policies]: #caching-policies
[Call an operation and test hello caching]: #test-operation
[Next steps]: #next-steps
