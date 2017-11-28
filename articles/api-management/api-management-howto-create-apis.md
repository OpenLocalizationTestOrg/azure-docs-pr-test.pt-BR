---
title: aaaHow toocreate APIs no gerenciamento de API do Azure
description: Saiba como toocreate e configurar APIs no gerenciamento de API do Azure.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 14c20da4-f29f-4b28-bec7-3d4c50b734da
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 48ed8d93947253aa1e67ad995927ed6101cac072
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-apis-in-azure-api-management"></a><span data-ttu-id="0776e-103">Como toocreate APIs no gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="0776e-103">How toocreate APIs in Azure API Management</span></span>
<span data-ttu-id="0776e-104">Uma API no Gerenciamento de API representa um conjunto de operações que pode ser invocado pelas aplicações clientes.</span><span class="sxs-lookup"><span data-stu-id="0776e-104">An API in API Management represents a set of operations that can be invoked by client applications.</span></span> <span data-ttu-id="0776e-105">Novas APIs são criadas no portal do publicador hello e, em seguida, Olá desejado operações são adicionadas.</span><span class="sxs-lookup"><span data-stu-id="0776e-105">New APIs are created in hello publisher portal, and then hello desired operations are added.</span></span> <span data-ttu-id="0776e-106">Quando as operações de saudação são adicionadas, Olá API é adicionado tooa produto e pode ser publicado.</span><span class="sxs-lookup"><span data-stu-id="0776e-106">Once hello operations are added, hello API is added tooa product and can be published.</span></span> <span data-ttu-id="0776e-107">Quando uma API for publicada, pode ser assinado tooand usado por desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="0776e-107">Once an API is published, it can be subscribed tooand used by developers.</span></span>

<span data-ttu-id="0776e-108">Este guia mostra a primeira etapa de saudação no processo de saudação: como toocreate e configurar uma nova API de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="0776e-108">This guide shows hello first step in hello process: how toocreate and configure a new API in API Management.</span></span> <span data-ttu-id="0776e-109">Para obter mais informações sobre operações de adicionar e publicar um produto, consulte [como tooadd operações tooan API] [ How tooadd operations tooan API] e [como toocreate e publicar um produto] [ How toocreate and publish a product].</span><span class="sxs-lookup"><span data-stu-id="0776e-109">For more information on adding operations and publishing a product, see [How tooadd operations tooan API][How tooadd operations tooan API] and [How toocreate and publish a product][How toocreate and publish a product].</span></span>

## <span data-ttu-id="0776e-110"><a name="create-new-api"> </a>Criar uma nova API</span><span class="sxs-lookup"><span data-stu-id="0776e-110"><a name="create-new-api"> </a>Create a new API</span></span>
<span data-ttu-id="0776e-111">APIs são criados e configurados no portal do publicador hello.</span><span class="sxs-lookup"><span data-stu-id="0776e-111">APIs are created and configured in hello publisher portal.</span></span> <span data-ttu-id="0776e-112">tooaccess Olá clique portal, publisher **portal do publicador** em hello Portal do Azure para seu serviço de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="0776e-112">tooaccess hello publisher portal, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Portal do editor][api-management-management-console]

> <span data-ttu-id="0776e-114">Se você ainda não tiver criado uma instância do serviço de gerenciamento de API, consulte [criar uma instância do serviço de gerenciamento de API] [ Create an API Management service instance] em Olá [Introdução ao gerenciamento de API do Azure] [ Get started with Azure API Management] tutorial.</span><span class="sxs-lookup"><span data-stu-id="0776e-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="0776e-115">Clique em **APIs** de saudação **gerenciamento de API** menu saudação à esquerda e clique **adicionar API**.</span><span class="sxs-lookup"><span data-stu-id="0776e-115">Click **APIs** from hello **API Management** menu on hello left, and then click **add API**.</span></span>

![Criar API][api-management-create-api]

<span data-ttu-id="0776e-117">Saudação de uso **adicionar nova API** tooconfigure janela Olá nova API.</span><span class="sxs-lookup"><span data-stu-id="0776e-117">Use hello **Add new API** window tooconfigure hello new API.</span></span>

![Adicionar nova API][api-management-add-new-api]

<span data-ttu-id="0776e-119">Olá campos a seguir é usadas tooconfigure Olá nova API.</span><span class="sxs-lookup"><span data-stu-id="0776e-119">hello following fields are used tooconfigure hello new API.</span></span>

* <span data-ttu-id="0776e-120">**Nome da API da Web** fornece um nome exclusivo e descritivo para Olá API.</span><span class="sxs-lookup"><span data-stu-id="0776e-120">**Web API name** provides a unique and descriptive name for hello API.</span></span> <span data-ttu-id="0776e-121">Ela é exibida em portais de desenvolvedor e o publicador hello.</span><span class="sxs-lookup"><span data-stu-id="0776e-121">It is displayed in hello developer and publisher portals.</span></span>
* <span data-ttu-id="0776e-122">**URL do serviço Web** referências Olá implementando Olá API de serviço HTTP.</span><span class="sxs-lookup"><span data-stu-id="0776e-122">**Web service URL** references hello HTTP service implementing hello API.</span></span> <span data-ttu-id="0776e-123">Gerenciamento de API encaminha solicitações toothis endereço.</span><span class="sxs-lookup"><span data-stu-id="0776e-123">API management forwards requests toothis address.</span></span>
* <span data-ttu-id="0776e-124">**Sufixo de URL da API da Web** é toohello acrescentadas a URL base para serviço de gerenciamento de API de saudação.</span><span class="sxs-lookup"><span data-stu-id="0776e-124">**Web API URL suffix** is appended toohello base URL for hello API management service.</span></span> <span data-ttu-id="0776e-125">URL base Olá é comum para todas as APIs hospedadas por uma instância do serviço de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="0776e-125">hello base URL is common for all APIs hosted by an API Management service instance.</span></span> <span data-ttu-id="0776e-126">Gerenciamento de API distingue APIs pelo seu sufixo e, portanto, o sufixo Olá deve ser exclusivo para cada API para um determinado publicador.</span><span class="sxs-lookup"><span data-stu-id="0776e-126">API Management distinguishes APIs by their suffix and therefore hello suffix must be unique for every API for a given publisher.</span></span>
* <span data-ttu-id="0776e-127">**Esquema de URL da API da Web** determina quais protocolos podem ser usados tooaccess Olá API.</span><span class="sxs-lookup"><span data-stu-id="0776e-127">**Web API URL scheme** determines which protocols can be used tooaccess hello API.</span></span> <span data-ttu-id="0776e-128">A HTTPs é especificada por padrão.</span><span class="sxs-lookup"><span data-stu-id="0776e-128">HTTPs is specified by default.</span></span>
* <span data-ttu-id="0776e-129">toooptionally adicionar esse novo produto tooa API, clique em Olá **produtos (opcionais)** suspensa e escolha um produto.</span><span class="sxs-lookup"><span data-stu-id="0776e-129">toooptionally add this new API tooa product, click hello **Products (optional)** drop-down and choose a product.</span></span> <span data-ttu-id="0776e-130">Esta etapa pode ser repetida várias vezes tooadd Olá API toomultiple produtos.</span><span class="sxs-lookup"><span data-stu-id="0776e-130">This step can be repeated multiple times tooadd hello API toomultiple products.</span></span>

<span data-ttu-id="0776e-131">Depois de saudação desejado valores estão configurados, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="0776e-131">Once hello desired values are configured, click **Save**.</span></span> <span data-ttu-id="0776e-132">Depois que Olá nova API é criada, hello página Resumo para a API de saudação é exibida no portal do publicador hello.</span><span class="sxs-lookup"><span data-stu-id="0776e-132">Once hello new API is created, hello summary page for hello API is displayed in hello publisher portal.</span></span>

![Resumo da API][api-management-api-summary]

## <span data-ttu-id="0776e-134"><a name="configure-api-settings"> </a>Definir configurações de API</span><span class="sxs-lookup"><span data-stu-id="0776e-134"><a name="configure-api-settings"> </a>Configure API settings</span></span>
<span data-ttu-id="0776e-135">Você pode usar o hello **configurações** guia tooverify e editar a configuração de saudação de uma API.</span><span class="sxs-lookup"><span data-stu-id="0776e-135">You can use hello **Settings** tab tooverify and edit hello configuration for an API.</span></span> <span data-ttu-id="0776e-136">**Nome da API da Web**, **URL do serviço Web**, e **sufixo de URL da API da Web** são inicialmente definidas quando Olá API é criada e pode ser modificado aqui.</span><span class="sxs-lookup"><span data-stu-id="0776e-136">**Web API name**, **Web service URL**, and **Web API URL suffix** are initially set when hello API is created and can be modified here.</span></span> <span data-ttu-id="0776e-137">**Descrição** fornece uma descrição opcional e **esquema de URL da API da Web** determina quais protocolos podem ser usados tooaccess Olá API.</span><span class="sxs-lookup"><span data-stu-id="0776e-137">**Description** provides an optional description, and **Web API URL scheme** determines which protocols can be used tooaccess hello API.</span></span>

![Configurações da API][api-management-api-settings]

<span data-ttu-id="0776e-139">autenticação de gateway tooconfigure hello de back-end serviço API de implementação hello, selecione Olá **segurança** Olá guia **com credenciais** suspenso pode ser usado tooconfigure **HTTP básico** ou **certificados de cliente** autenticação.</span><span class="sxs-lookup"><span data-stu-id="0776e-139">tooconfigure gateway authentication for hello backend service implementing hello API, select hello **Security** tab. hello **With credentials** drop-down can be used tooconfigure **HTTP basic** or **Client certificates** authentication.</span></span> <span data-ttu-id="0776e-140">a autenticação básica HTTP de toouse, basta digitar as credenciais de saudação desejada.</span><span class="sxs-lookup"><span data-stu-id="0776e-140">toouse HTTP basic authentication, simply enter hello desired credentials.</span></span> <span data-ttu-id="0776e-141">Para obter informações sobre como usar a autenticação de certificado de cliente, consulte [como toosecure serviços de back-end usando o cliente de certificado autenticação no gerenciamento de API do Azure][How toosecure back-end services using client certificate authentication in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="0776e-141">For information on using client certificate authentication, see [How toosecure back-end services using client certificate authentication in Azure API Management][How toosecure back-end services using client certificate authentication in Azure API Management].</span></span>

<span data-ttu-id="0776e-142">Olá **segurança** guia também pode ser usado tooconfigure **autorização do usuário** usando OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="0776e-142">hello **Security** tab can also be used tooconfigure **User authorization** using OAuth 2.0.</span></span> <span data-ttu-id="0776e-143">Para obter mais informações, consulte [como desenvolvedor tooauthorize contas usando OAuth 2.0 no gerenciamento de API do Azure][How tooauthorize developer accounts using OAuth 2.0 in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="0776e-143">For more information, see [How tooauthorize developer accounts using OAuth 2.0 in Azure API Management][How tooauthorize developer accounts using OAuth 2.0 in Azure API Management].</span></span>

![Configurações da autenticação Básica][api-management-api-settings-credentials]

<span data-ttu-id="0776e-145">Clique em **salvar** toosave qualquer alteração feita toohello configurações de API.</span><span class="sxs-lookup"><span data-stu-id="0776e-145">Click **Save** toosave any changes you make toohello API settings.</span></span>

## <span data-ttu-id="0776e-146"><a name="next-steps"> </a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0776e-146"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="0776e-147">Depois que uma API é criada e configurações hello, Olá próximas etapas são tooadd Olá operações toohello API, adicionar Olá API tooa produto e publicá-lo para que ele está disponível para desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="0776e-147">Once an API is created and hello settings configured, hello next steps are tooadd hello operations toohello API, add hello API tooa product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="0776e-148">Para obter mais informações, consulte Olá artigos a seguir.</span><span class="sxs-lookup"><span data-stu-id="0776e-148">For more information, see hello following articles.</span></span>

* <span data-ttu-id="0776e-149">[Como as operações de tooadd tooan API][How tooadd operations tooan API]</span><span class="sxs-lookup"><span data-stu-id="0776e-149">[How tooadd operations tooan API][How tooadd operations tooan API]</span></span>
* <span data-ttu-id="0776e-150">[Como toocreate e publicar um produto][How toocreate and publish a product]</span><span class="sxs-lookup"><span data-stu-id="0776e-150">[How toocreate and publish a product][How toocreate and publish a product]</span></span>

[api-management-create-api]: ./media/api-management-howto-create-apis/api-management-create-api.png
[api-management-management-console]: ./media/api-management-howto-create-apis/api-management-management-console.png
[api-management-add-new-api]: ./media/api-management-howto-create-apis/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-create-apis/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-create-apis/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-create-apis/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-create-apis/api-management-echo-operations.png

[What is an API?]: #what-is-api
[Create a new API]: #create-new-api
[Configure API settings]: #configure-api-settings
[Configure API operations]: #configure-api-operations
[Next steps]: #next-steps

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[How toosecure back-end services using client certificate authentication in Azure API Management]: api-management-howto-mutual-certificates.md
[How tooauthorize developer accounts using OAuth 2.0 in Azure API Management]: api-management-howto-oauth2.md
