---
title: Adicionar cache para melhorar o desempenho no Gerenciamento de API do Azure | Microsoft Docs
description: "Saiba como aprimorar a latência, carregar o consumo de largura de banda e o serviço Web para chamadas de serviço de Gerenciamento de API."
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
ms.openlocfilehash: 59c595f0d5ce849f44c46fdb6cab0b44d35fffa0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="add-caching-to-improve-performance-in-azure-api-management"></a><span data-ttu-id="a4196-103">Adicionar caching para melhorar o desempenho no Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="a4196-103">Add caching to improve performance in Azure API Management</span></span>
<span data-ttu-id="a4196-104">É possível configurar as operações do Gerenciamento de API para cache das respostas.</span><span class="sxs-lookup"><span data-stu-id="a4196-104">Operations in API Management can be configured for response caching.</span></span> <span data-ttu-id="a4196-105">O cache das respostas pode reduzir significativamente a latência da API, o consumo da largura de banda e a carga de serviço Web para dados que não são alterados com frequência.</span><span class="sxs-lookup"><span data-stu-id="a4196-105">Response caching can significantly reduce API latency, bandwidth consumption, and web service load for data that does not change frequently.</span></span>

<span data-ttu-id="a4196-106">Este guia mostra como adicionar o caching das respostas para sua API e configurar políticas para as operações de API de Eco.</span><span class="sxs-lookup"><span data-stu-id="a4196-106">This guide shows you how to add response caching for your API and configure policies for the sample Echo API operations.</span></span> <span data-ttu-id="a4196-107">Você pode chamar a operação por meio do portal do desenvolvedor para verificar o caching em ação.</span><span class="sxs-lookup"><span data-stu-id="a4196-107">You can then call the operation from the developer portal to verify caching in action.</span></span>

> [!NOTE]
> <span data-ttu-id="a4196-108">Para saber mais sobre itens de cache por chave usando expressões de política, confira [Cache personalizado no Gerenciamento de API do Azure](api-management-sample-cache-by-key.md).</span><span class="sxs-lookup"><span data-stu-id="a4196-108">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="a4196-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a4196-109">Prerequisites</span></span>
<span data-ttu-id="a4196-110">Antes de seguir as etapas neste guia, você deve ter uma instância do serviço de Gerenciamento de API com uma API e um produto configurado.</span><span class="sxs-lookup"><span data-stu-id="a4196-110">Before following the steps in this guide, you must have an API Management service instance with an API and a product configured.</span></span> <span data-ttu-id="a4196-111">Se ainda não criou uma instância de serviço de Gerenciamento de API, confira [Criar uma instância de serviço de Gerenciamento de API][Create an API Management service instance] no tutorial [Introdução ao Gerenciamento de API do Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="a4196-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

## <span data-ttu-id="a4196-112"><a name="configure-caching"> </a>Configurar uma operação para caching</span><span class="sxs-lookup"><span data-stu-id="a4196-112"><a name="configure-caching"> </a>Configure an operation for caching</span></span>
<span data-ttu-id="a4196-113">Nesta etapa, você examinará as configurações de cache da operação **Recurso GET (em cache)** do exemplo de API de Eco.</span><span class="sxs-lookup"><span data-stu-id="a4196-113">In this step, you will review the caching settings of the **GET Resource (cached)** operation of the sample Echo API.</span></span>

> [!NOTE]
> <span data-ttu-id="a4196-114">Cada instância de serviço de Gerenciamento de API vem pré-configurada com uma API de Eco que pode ser usada para experimentar e aprender sobre o Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="a4196-114">Each API Management service instance comes preconfigured with an Echo API that can be used to experiment with and learn about API Management.</span></span> <span data-ttu-id="a4196-115">Para obter mais informações, confira [Introdução ao Gerenciamento de API do Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="a4196-115">For more information, see [Get started with Azure API Management][Get started with Azure API Management].</span></span>
> 
> 

<span data-ttu-id="a4196-116">Para começar, clique em **Portal do Editor** no Portal do Azure para acessar o serviço de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="a4196-116">To get started, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="a4196-117">Isso levará você ao portal do editor de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="a4196-117">This takes you to the API Management publisher portal.</span></span>

![Portal do editor][api-management-management-console]

<span data-ttu-id="a4196-119">Clique em **APIs** no menu **Gerenciamento de API** à esquerda e clique em **API de Eco**.</span><span class="sxs-lookup"><span data-stu-id="a4196-119">Click **APIs** from the **API Management** menu on the left, and then click **Echo API**.</span></span>

![API de Eco][api-management-echo-api]

<span data-ttu-id="a4196-121">Clique na guia **Operações** e na operação **Recurso GET (em cache)**, na lista **Operações**.</span><span class="sxs-lookup"><span data-stu-id="a4196-121">Click the **Operations** tab, and then click the **GET Resource (cached)** operation from the **Operations** list.</span></span>

![Operações de API de ECO][api-management-echo-api-operations]

<span data-ttu-id="a4196-123">Clique na guia **Cache** para ver as configurações de cache para esta operação.</span><span class="sxs-lookup"><span data-stu-id="a4196-123">Click the **Caching** tab to view the caching settings for this operation.</span></span>

![Guia Cache][api-management-caching-tab]

<span data-ttu-id="a4196-125">Para habilitar o cache de uma operação, marque a caixa de seleção **Habilitar** .</span><span class="sxs-lookup"><span data-stu-id="a4196-125">To enable caching for an operation, select the **Enable** check box.</span></span> <span data-ttu-id="a4196-126">Neste exemplo, o caching está habilitado.</span><span class="sxs-lookup"><span data-stu-id="a4196-126">In this example, caching is enabled.</span></span>

<span data-ttu-id="a4196-127">A resposta de cada operação tem uma chave baseada nos valores dos campos **Variar por parâmetros da cadeia de consulta** e **Variar por cabeçalhos**.</span><span class="sxs-lookup"><span data-stu-id="a4196-127">Each operation response is keyed, based on the values in the **Vary by query string parameters** and **Vary by headers** fields.</span></span> <span data-ttu-id="a4196-128">Se quiser armazenar em cache várias respostas com base em cabeçalhos ou parâmetros de cadeias de consulta, você pode configurá-las nesses dois campos.</span><span class="sxs-lookup"><span data-stu-id="a4196-128">If you want to cache multiple responses based on query string parameters or headers, you can configure them in these two fields.</span></span>

<span data-ttu-id="a4196-129">**Duração** especifica o intervalo de vencimento das respostas armazenadas em cache.</span><span class="sxs-lookup"><span data-stu-id="a4196-129">**Duration** specifies the expiration interval of the cached responses.</span></span> <span data-ttu-id="a4196-130">Neste exemplo, o intervalo é de **3600** segundos, que equivale a uma hora.</span><span class="sxs-lookup"><span data-stu-id="a4196-130">In this example, the interval is **3600** seconds, which is equivalent to one hour.</span></span>

<span data-ttu-id="a4196-131">Utilizando a configuração de cache neste exemplo, a primeira solicitação para a operação **Recurso GET (em cache)** retorna uma resposta do serviço de back-end.</span><span class="sxs-lookup"><span data-stu-id="a4196-131">Using the caching configuration in this example, the first request to the **GET Resource (cached)** operation returns a response from the backend service.</span></span> <span data-ttu-id="a4196-132">Esta resposta será armazenada em cache, com uma chave de acordo com os parâmetros de cadeia de consulta e cabeçalhos especificados.</span><span class="sxs-lookup"><span data-stu-id="a4196-132">This response will be cached, keyed by the specified headers and query string parameters.</span></span> <span data-ttu-id="a4196-133">Chamadas subsequentes para a operação, com parâmetros correspondentes, retornarão respostas em cache até que o intervalo de duração de cache expire.</span><span class="sxs-lookup"><span data-stu-id="a4196-133">Subsequent calls to the operation, with matching parameters, will have the cached response returned, until the cache duration interval has expired.</span></span>

## <span data-ttu-id="a4196-134"><a name="caching-policies"> </a>Examinar as políticas de cache</span><span class="sxs-lookup"><span data-stu-id="a4196-134"><a name="caching-policies"> </a>Review the caching policies</span></span>
<span data-ttu-id="a4196-135">Nesta etapa, você analisará as configurações de cache da operação **Recurso GET (em cache)** do exemplo de API de Echo.</span><span class="sxs-lookup"><span data-stu-id="a4196-135">In this step, you review the caching settings for the **GET Resource (cached)** operation of the sample Echo API.</span></span>

<span data-ttu-id="a4196-136">Quando as configurações de cache são definidas para uma operação na guia **Cache** , políticas de cache são adicionadas à operação.</span><span class="sxs-lookup"><span data-stu-id="a4196-136">When caching settings are configured for an operation on the **Caching** tab, caching policies are added for the operation.</span></span> <span data-ttu-id="a4196-137">Essas políticas podem ser vistas e editadas no editor de políticas.</span><span class="sxs-lookup"><span data-stu-id="a4196-137">These policies can be viewed and edited in the policy editor.</span></span>

<span data-ttu-id="a4196-138">Clique em **Políticas** no menu **Gerenciamento de API** à esquerda e selecione **API de Eco/Recurso GET (em cache)** na lista suspensa **Operação**.</span><span class="sxs-lookup"><span data-stu-id="a4196-138">Click **Policies** from the **API Management** menu on the left, and then select **Echo API / GET Resource (cached)** from the **Operation** drop-down list.</span></span>

![Operação de escopo da política][api-management-operation-dropdown]

<span data-ttu-id="a4196-140">Exibe as políticas para esta operação no editor de políticas.</span><span class="sxs-lookup"><span data-stu-id="a4196-140">This displays the policies for this operation in the policy editor.</span></span>

![Editor de políticas de Gerenciamento de API][api-management-policy-editor]

<span data-ttu-id="a4196-142">A definição de política para esta operação inclui as políticas que definem a configuração de cache, que foram revisadas usando a guia **Cache** na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="a4196-142">The policy definition for this operation includes the policies that define the caching configuration that were reviewed using the **Caching** tab in the previous step.</span></span>

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
> <span data-ttu-id="a4196-143">As alterações feitas nas políticas de cache no editor de políticas serão refletidas na guia **Cache** de uma operação e vice-versa.</span><span class="sxs-lookup"><span data-stu-id="a4196-143">Changes made to the caching policies in the policy editor will be reflected on the **Caching** tab of an operation, and vice-versa.</span></span>
> 
> 

## <span data-ttu-id="a4196-144"><a name="test-operation"> </a>Chamar uma operação e testar o cache</span><span class="sxs-lookup"><span data-stu-id="a4196-144"><a name="test-operation"> </a>Call an operation and test the caching</span></span>
<span data-ttu-id="a4196-145">Para ver o cache em funcionamento, podemos chamar a operação por meio do portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="a4196-145">To see the caching in action, we can call the operation from the developer portal.</span></span> <span data-ttu-id="a4196-146">Clique em **Portal do desenvolvedor** no menu superior direito.</span><span class="sxs-lookup"><span data-stu-id="a4196-146">Click **Developer portal** in the top right menu.</span></span>

![Portal do desenvolvedor][api-management-developer-portal-menu]

<span data-ttu-id="a4196-148">Clique em **APIs** no menu superior e selecione **API de Eco**.</span><span class="sxs-lookup"><span data-stu-id="a4196-148">Click **APIs** in the top menu, and then select **Echo API**.</span></span>

![API de Eco][api-management-apis-echo-api]

> <span data-ttu-id="a4196-150">Se você tem apenas uma API configurada ou visível na conta, clicar em APIs levará você diretamente às operações dessa API.</span><span class="sxs-lookup"><span data-stu-id="a4196-150">If you have only one API configured or visible to your account, then clicking APIs takes you directly to the operations for that API.</span></span>
> 
> 

<span data-ttu-id="a4196-151">Selecione a operação **Recurso GET (em cache)** e clique em **Abrir Console**.</span><span class="sxs-lookup"><span data-stu-id="a4196-151">Select the **GET Resource (cached)** operation, and then click **Open Console**.</span></span>

![Abrir console][api-management-open-console]

<span data-ttu-id="a4196-153">O console permite que você invoque operações diretamente por meio do portal do desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="a4196-153">The console allows you to invoke operations directly from the developer portal.</span></span>

![Console][api-management-console]

<span data-ttu-id="a4196-155">Mantenha os valores padrão para **param1** e **param2**.</span><span class="sxs-lookup"><span data-stu-id="a4196-155">Keep the default values for **param1** and **param2**.</span></span>

<span data-ttu-id="a4196-156">Selecione a chave desejada na lista suspensa **subscription-key** .</span><span class="sxs-lookup"><span data-stu-id="a4196-156">Select the desired key from the **subscription-key** drop-down list.</span></span> <span data-ttu-id="a4196-157">Se a sua conta tiver somente uma assinatura, ela já estará selecionada.</span><span class="sxs-lookup"><span data-stu-id="a4196-157">If your account has only one subscription, it will already be selected.</span></span>

<span data-ttu-id="a4196-158">Insira **sampleheader:value1** na caixa de texto **Cabeçalhos de solicitação**.</span><span class="sxs-lookup"><span data-stu-id="a4196-158">Enter **sampleheader:value1** in the **Request headers** text box.</span></span>

<span data-ttu-id="a4196-159">Clique em **HTTP Get** e anote os cabeçalhos de resposta.</span><span class="sxs-lookup"><span data-stu-id="a4196-159">Click **HTTP Get** and make a note of the response headers.</span></span>

<span data-ttu-id="a4196-160">Insira **sampleheader:value2** na caixa de texto **Cabeçalhos de solicitação** e clique em **HTTP Get**.</span><span class="sxs-lookup"><span data-stu-id="a4196-160">Enter **sampleheader:value2** in the **Request headers** text box, and then click **HTTP Get**.</span></span>

<span data-ttu-id="a4196-161">Observe que o valor de **sampleheader** ainda será **value1** na resposta.</span><span class="sxs-lookup"><span data-stu-id="a4196-161">Note that the value of **sampleheader** is still **value1** in the response.</span></span> <span data-ttu-id="a4196-162">Teste alguns valores diferentes e observe que a resposta armazenada em cache da primeira chamada será retornada.</span><span class="sxs-lookup"><span data-stu-id="a4196-162">Try some different values and note that the cached response from the first call is returned.</span></span>

<span data-ttu-id="a4196-163">Insira **25** no campo **param2** e clique em **HTTP Get**.</span><span class="sxs-lookup"><span data-stu-id="a4196-163">Enter **25** into the **param2** field, and then click **HTTP Get**.</span></span>

<span data-ttu-id="a4196-164">Observe que agora o valor de **sampleheader** na resposta será **value2**.</span><span class="sxs-lookup"><span data-stu-id="a4196-164">Note that the value of **sampleheader** in the response is now **value2**.</span></span> <span data-ttu-id="a4196-165">Como os resultados da operação têm uma chave de acordo com a cadeia de consulta, a resposta em cache anterior não foi retornada.</span><span class="sxs-lookup"><span data-stu-id="a4196-165">Because the operation results are keyed by query string, the previous cached response was not returned.</span></span>

## <span data-ttu-id="a4196-166"><a name="next-steps"> </a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a4196-166"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="a4196-167">Para saber mais sobre as políticas de cache, veja [Políticas de cache][Caching policies] na [Referência de política do Gerenciamento de API][API Management policy reference].</span><span class="sxs-lookup"><span data-stu-id="a4196-167">For more information about caching policies, see [Caching policies][Caching policies] in the [API Management policy reference][API Management policy reference].</span></span>
* <span data-ttu-id="a4196-168">Para saber mais sobre itens de cache por chave usando expressões de política, confira [Cache personalizado no Gerenciamento de API do Azure](api-management-sample-cache-by-key.md).</span><span class="sxs-lookup"><span data-stu-id="a4196-168">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span></span>

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


[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md

[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx

[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Configure an operation for caching]: #configure-caching
[Review the caching policies]: #caching-policies
[Call an operation and test the caching]: #test-operation
[Next steps]: #next-steps
