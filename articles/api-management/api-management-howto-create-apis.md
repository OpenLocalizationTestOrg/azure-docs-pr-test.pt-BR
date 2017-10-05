---
title: Como criar APIs no Gerenciamento de API do Azure
description: Saiba como criar e configurar APIs no Gerenciamento de API do Azure.
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
ms.openlocfilehash: ab08256fbc3caca05bf23a12016ad2acf4fc7412
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-apis-in-azure-api-management"></a><span data-ttu-id="4c13d-103">Como criar APIs no Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="4c13d-103">How to create APIs in Azure API Management</span></span>
<span data-ttu-id="4c13d-104">Uma API no Gerenciamento de API representa um conjunto de operações que pode ser invocado pelas aplicações clientes.</span><span class="sxs-lookup"><span data-stu-id="4c13d-104">An API in API Management represents a set of operations that can be invoked by client applications.</span></span> <span data-ttu-id="4c13d-105">Novas APIs são criadas no Portal do editor e, depois, as operações desejadas são adicionadas.</span><span class="sxs-lookup"><span data-stu-id="4c13d-105">New APIs are created in the publisher portal, and then the desired operations are added.</span></span> <span data-ttu-id="4c13d-106">Após as operações serem adicionadas, a API é adicionada a um produto e pode ser publicada.</span><span class="sxs-lookup"><span data-stu-id="4c13d-106">Once the operations are added, the API is added to a product and can be published.</span></span> <span data-ttu-id="4c13d-107">Após uma API ser publicada, ela pode ser usada e assinada por desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="4c13d-107">Once an API is published, it can be subscribed to and used by developers.</span></span>

<span data-ttu-id="4c13d-108">Este guia mostra a primeira etapa do processo: como criar e configurar uma nova API no Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="4c13d-108">This guide shows the first step in the process: how to create and configure a new API in API Management.</span></span> <span data-ttu-id="4c13d-109">Para obter mais informações sobre como adicionar operações e publicar um produto, consulte [Como adicionar operações a uma API][How to add operations to an API] e [Como criar e publicar um produto][How to create and publish a product].</span><span class="sxs-lookup"><span data-stu-id="4c13d-109">For more information on adding operations and publishing a product, see [How to add operations to an API][How to add operations to an API] and [How to create and publish a product][How to create and publish a product].</span></span>

## <span data-ttu-id="4c13d-110"><a name="create-new-api"> </a>Criar uma nova API</span><span class="sxs-lookup"><span data-stu-id="4c13d-110"><a name="create-new-api"> </a>Create a new API</span></span>
<span data-ttu-id="4c13d-111">APIs são criadas e configuradas no Portal do editor.</span><span class="sxs-lookup"><span data-stu-id="4c13d-111">APIs are created and configured in the publisher portal.</span></span> <span data-ttu-id="4c13d-112">Para acessar o Portal do editor, clique em **Portal do editor** no Portal do Azure para acessar o serviço de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="4c13d-112">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span>

![Portal do editor][api-management-management-console]

> <span data-ttu-id="4c13d-114">Se ainda não criou uma instância de serviço de Gerenciamento de API, confira [Criar uma instância de serviço de Gerenciamento de API][Create an API Management service instance] no tutorial [Introdução ao Gerenciamento de API do Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="4c13d-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="4c13d-115">Clique em **APIs** no menu **Gerenciamento de API** à esquerda e depois clique em **Adicionar API**.</span><span class="sxs-lookup"><span data-stu-id="4c13d-115">Click **APIs** from the **API Management** menu on the left, and then click **add API**.</span></span>

![Criar API][api-management-create-api]

<span data-ttu-id="4c13d-117">Use a janela **Adicionar nova API** para configurar a nova API.</span><span class="sxs-lookup"><span data-stu-id="4c13d-117">Use the **Add new API** window to configure the new API.</span></span>

![Adicionar nova API][api-management-add-new-api]

<span data-ttu-id="4c13d-119">Os campos a seguir são usados para configurar a nova API.</span><span class="sxs-lookup"><span data-stu-id="4c13d-119">The following fields are used to configure the new API.</span></span>

* <span data-ttu-id="4c13d-120">**Nome da API Web** fornece um nome descritivo exclusivo para a API.</span><span class="sxs-lookup"><span data-stu-id="4c13d-120">**Web API name** provides a unique and descriptive name for the API.</span></span> <span data-ttu-id="4c13d-121">Esse nome será exibido nos portais do desenvolvedor e do editor.</span><span class="sxs-lookup"><span data-stu-id="4c13d-121">It is displayed in the developer and publisher portals.</span></span>
* <span data-ttu-id="4c13d-122">**URL de Serviço Web** utiliza como referência o serviço HTTP que está implementando a API.</span><span class="sxs-lookup"><span data-stu-id="4c13d-122">**Web service URL** references the HTTP service implementing the API.</span></span> <span data-ttu-id="4c13d-123">O gerenciamento de API envia as solicitações para esse endereço.</span><span class="sxs-lookup"><span data-stu-id="4c13d-123">API management forwards requests to this address.</span></span>
* <span data-ttu-id="4c13d-124">**O sufixo da URL da API Web** está anexado à URL base do serviço de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="4c13d-124">**Web API URL suffix** is appended to the base URL for the API management service.</span></span> <span data-ttu-id="4c13d-125">A URL base é comum para todas as APIs hospedadas por uma instância de um serviço de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="4c13d-125">The base URL is common for all APIs hosted by an API Management service instance.</span></span> <span data-ttu-id="4c13d-126">O Gerenciamento de API diferencia as APIs pelo sufixo e, portanto, o sufixo deve ser único para cada API para um editor específico.</span><span class="sxs-lookup"><span data-stu-id="4c13d-126">API Management distinguishes APIs by their suffix and therefore the suffix must be unique for every API for a given publisher.</span></span>
* <span data-ttu-id="4c13d-127">**Esquema de URL da API da Web** determina quais protocolos podem ser usados para acessar a API.</span><span class="sxs-lookup"><span data-stu-id="4c13d-127">**Web API URL scheme** determines which protocols can be used to access the API.</span></span> <span data-ttu-id="4c13d-128">A HTTPs é especificada por padrão.</span><span class="sxs-lookup"><span data-stu-id="4c13d-128">HTTPs is specified by default.</span></span>
* <span data-ttu-id="4c13d-129">Para adicionar, opcionalmente, essa nova API a um produto, clique na lista suspensa **Produtos (opcional)** e escolha um produto.</span><span class="sxs-lookup"><span data-stu-id="4c13d-129">To optionally add this new API to a product, click the **Products (optional)** drop-down and choose a product.</span></span> <span data-ttu-id="4c13d-130">Esta etapa pode ser repetida várias vezes para adicionar a API a vários produtos.</span><span class="sxs-lookup"><span data-stu-id="4c13d-130">This step can be repeated multiple times to add the API to multiple products.</span></span>

<span data-ttu-id="4c13d-131">Após configurar os valores desejados, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="4c13d-131">Once the desired values are configured, click **Save**.</span></span> <span data-ttu-id="4c13d-132">Após criar a novas API, a página de resumo das APIs será exibida no Portal do Publicador.</span><span class="sxs-lookup"><span data-stu-id="4c13d-132">Once the new API is created, the summary page for the API is displayed in the publisher portal.</span></span>

![Resumo da API][api-management-api-summary]

## <span data-ttu-id="4c13d-134"><a name="configure-api-settings"> </a>Definir configurações de API</span><span class="sxs-lookup"><span data-stu-id="4c13d-134"><a name="configure-api-settings"> </a>Configure API settings</span></span>
<span data-ttu-id="4c13d-135">Você pode usar a guia **Configurações** para verificar e editar a configuração de uma API.</span><span class="sxs-lookup"><span data-stu-id="4c13d-135">You can use the **Settings** tab to verify and edit the configuration for an API.</span></span> <span data-ttu-id="4c13d-136">O **Nome da API Web**, a **URL do Serviço Web** e o **sufixo da URL da API Web** são definidos inicialmente, quando a API é criada, e podem ser modificados aqui.</span><span class="sxs-lookup"><span data-stu-id="4c13d-136">**Web API name**, **Web service URL**, and **Web API URL suffix** are initially set when the API is created and can be modified here.</span></span> <span data-ttu-id="4c13d-137">**Descrição** fornece uma descrição opcional, e o **Esquema de URL da API Web** determina quais protocolos podem ser usados para acessar a API.</span><span class="sxs-lookup"><span data-stu-id="4c13d-137">**Description** provides an optional description, and **Web API URL scheme** determines which protocols can be used to access the API.</span></span>

![Configurações da API][api-management-api-settings]

<span data-ttu-id="4c13d-139">Para configurar a autenticação de gateway para o serviço de back-end implementando a API, selecione a guia **Segurança** .</span><span class="sxs-lookup"><span data-stu-id="4c13d-139">To configure gateway authentication for the backend service implementing the API, select the **Security** tab.</span></span> <span data-ttu-id="4c13d-140">A lista suspensa **Com credenciais** pode ser usada para configurar a autenticação como **HTTP básica** ou **Certificados do cliente**.</span><span class="sxs-lookup"><span data-stu-id="4c13d-140">The **With credentials** drop-down can be used to configure **HTTP basic** or **Client certificates** authentication.</span></span> <span data-ttu-id="4c13d-141">Para usar a autenticação HTTP básica, basta inserir as credenciais desejadas.</span><span class="sxs-lookup"><span data-stu-id="4c13d-141">To use HTTP basic authentication, simply enter the desired credentials.</span></span> <span data-ttu-id="4c13d-142">Para informações sobre como usar a autenticação de certificados do cliente, consulte [Como garantir serviços de back-end usando autenticação de certificados do cliente no Gerenciamento de API do Azure][How to secure back-end services using client certificate authentication in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="4c13d-142">For information on using client certificate authentication, see [How to secure back-end services using client certificate authentication in Azure API Management][How to secure back-end services using client certificate authentication in Azure API Management].</span></span>

<span data-ttu-id="4c13d-143">A guia **Seguran**ça também pode ser usada para configurar **Autorização do usuário** usando OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="4c13d-143">The **Security** tab can also be used to configure **User authorization** using OAuth 2.0.</span></span> <span data-ttu-id="4c13d-144">Para obter mais informações, consulte [Como autorizar contas de desenvolvedor usando o OAuth 2.0 no Gerenciamento de API do Azure][How to authorize developer accounts using OAuth 2.0 in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="4c13d-144">For more information, see [How to authorize developer accounts using OAuth 2.0 in Azure API Management][How to authorize developer accounts using OAuth 2.0 in Azure API Management].</span></span>

![Configurações da autenticação Básica][api-management-api-settings-credentials]

<span data-ttu-id="4c13d-146">Clique em **Salvar** para salvar quaisquer mudanças feitas nas configurações da API.</span><span class="sxs-lookup"><span data-stu-id="4c13d-146">Click **Save** to save any changes you make to the API settings.</span></span>

## <span data-ttu-id="4c13d-147"><a name="next-steps"> </a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4c13d-147"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="4c13d-148">Após criar uma API e definir as configurações, as próximas etapas são adicionar as operações à API, adicionar a API a um produto e publicá-la para que fique disponível para desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="4c13d-148">Once an API is created and the settings configured, the next steps are to add the operations to the API, add the API to a product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="4c13d-149">Para obter mais informações, consulte os seguintes artigos.</span><span class="sxs-lookup"><span data-stu-id="4c13d-149">For more information, see the following articles.</span></span>

* <span data-ttu-id="4c13d-150">[Como adicionar operações a uma API][How to add operations to an API]</span><span class="sxs-lookup"><span data-stu-id="4c13d-150">[How to add operations to an API][How to add operations to an API]</span></span>
* <span data-ttu-id="4c13d-151">[Como criar e publicar um produto][How to create and publish a product]</span><span class="sxs-lookup"><span data-stu-id="4c13d-151">[How to create and publish a product][How to create and publish a product]</span></span>

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

[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance
[How to secure back-end services using client certificate authentication in Azure API Management]: api-management-howto-mutual-certificates.md
[How to authorize developer accounts using OAuth 2.0 in Azure API Management]: api-management-howto-oauth2.md
