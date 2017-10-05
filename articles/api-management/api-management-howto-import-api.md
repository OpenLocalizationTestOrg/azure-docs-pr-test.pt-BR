---
title: Importar uma API para o Gerenciamento de API do Azure | Microsoft Docs
description: "Saiba como importar uma API e suas operações para o Gerenciamento de API do Azure."
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
ms.openlocfilehash: c851b88fc1067e65044266d07775717c028e75d9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-import-the-definition-of-an-api-with-operations-in-azure-api-management"></a><span data-ttu-id="a36bf-103">Como importar a definição de uma API com operações no Gerenciamento da API do Azure</span><span class="sxs-lookup"><span data-stu-id="a36bf-103">How to import the definition of an API with operations in Azure API Management</span></span>
<span data-ttu-id="a36bf-104">No Gerenciamento de API, novas APIs podem ser criadas e as operações podem ser adicionadas manualmente, ou a API pode ser importada em conjunto com as operações em uma etapa.</span><span class="sxs-lookup"><span data-stu-id="a36bf-104">In API Management, new APIs can be created and the operations added manually, or the API can be imported along with the operations in one step.</span></span>

<span data-ttu-id="a36bf-105">As APIs e suas operações podem ser importadas usando os formatos a seguir.</span><span class="sxs-lookup"><span data-stu-id="a36bf-105">APIs and their operations can be imported using the following formats.</span></span>

* <span data-ttu-id="a36bf-106">WADL</span><span class="sxs-lookup"><span data-stu-id="a36bf-106">WADL</span></span>
* <span data-ttu-id="a36bf-107">Swagger</span><span class="sxs-lookup"><span data-stu-id="a36bf-107">Swagger</span></span>

<span data-ttu-id="a36bf-108">Este guia mostra como criar uma nova API e importar suas operações em uma etapa.</span><span class="sxs-lookup"><span data-stu-id="a36bf-108">This guide shows how create a new API and import its operations in one step.</span></span> <span data-ttu-id="a36bf-109">Para obter mais informações sobre como criar uma API e adicionar operações manualmente, consulte [Como criar APIs][How to create APIs] e [Como adicionar operações a uma API][How to add operations to an API].</span><span class="sxs-lookup"><span data-stu-id="a36bf-109">For information on manually creating an API and adding operations, see [How to create APIs][How to create APIs] and [How to add operations to an API][How to add operations to an API].</span></span>

## <span data-ttu-id="a36bf-110"><a name="import-api"> </a>Importar uma API</span><span class="sxs-lookup"><span data-stu-id="a36bf-110"><a name="import-api"> </a>Import an API</span></span>
<span data-ttu-id="a36bf-111">APIs são criadas e configuradas no Portal do editor.</span><span class="sxs-lookup"><span data-stu-id="a36bf-111">APIs are created and configured in the publisher portal.</span></span> <span data-ttu-id="a36bf-112">Para acessar o portal do editor, clique em **Portal do editor** no Portal do Azure para acessar o serviço Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="a36bf-112">To access the publisher portal, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="a36bf-113">Se ainda não criou uma instância de serviço de Gerenciamento de API, confira [Criar uma instância de serviço de Gerenciamento de API][Create an API Management service instance] no tutorial [Introdução ao Gerenciamento de API do Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="a36bf-113">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

![Portal do editor][api-management-management-console]

<span data-ttu-id="a36bf-115">Clique em **APIs** no menu **Gerenciamento de API** à esquerda e depois clique em **Importar API**.</span><span class="sxs-lookup"><span data-stu-id="a36bf-115">Click **APIs** from the **API Management** menu on the left, and then click **import API**.</span></span>

![Importar API][api-management-import-apis]

<span data-ttu-id="a36bf-117">A janela **Importar API** possui três guias que correspondem às três maneiras de fornecer a especificação da API.</span><span class="sxs-lookup"><span data-stu-id="a36bf-117">The **Import API** window has three tabs that correspond to the three ways to provide the API specification.</span></span>

* <span data-ttu-id="a36bf-118">**A partir da área de transferência** permite que você cole a especificação da API na caixa de texto designada.</span><span class="sxs-lookup"><span data-stu-id="a36bf-118">**From clipboard** allows you to paste the API specification into the designated text box.</span></span>
* <span data-ttu-id="a36bf-119">**A partir do arquivo** permite que você navegue até e selecione o arquivo que contém a especificação da API.</span><span class="sxs-lookup"><span data-stu-id="a36bf-119">**From file** allows you to browse to and select the file that contains the API specification.</span></span>
* <span data-ttu-id="a36bf-120">**A partir da URL** permite que você forneça a URL até a especificação para a API.</span><span class="sxs-lookup"><span data-stu-id="a36bf-120">**From URL** allows you to supply the URL to the specification for the API.</span></span>

![Importar formato de API][api-management-import-api-clipboard]

<span data-ttu-id="a36bf-122">Após fornecer a especificação da API, use os botões de opção à direita para indicar o formato da especificação.</span><span class="sxs-lookup"><span data-stu-id="a36bf-122">After providing the API specification, use the radio buttons on the right to indicate the specification format.</span></span> <span data-ttu-id="a36bf-123">Os formatos a seguir são suportados.</span><span class="sxs-lookup"><span data-stu-id="a36bf-123">The following formats are supported.</span></span>

* <span data-ttu-id="a36bf-124">WADL</span><span class="sxs-lookup"><span data-stu-id="a36bf-124">WADL</span></span>
* <span data-ttu-id="a36bf-125">Swagger</span><span class="sxs-lookup"><span data-stu-id="a36bf-125">Swagger</span></span>

<span data-ttu-id="a36bf-126">Em seguida, insira um **sufixo de URL de API Web**.</span><span class="sxs-lookup"><span data-stu-id="a36bf-126">Next, enter a **Web API URL suffix**.</span></span> <span data-ttu-id="a36bf-127">Ele está anexado à URL base do serviço de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="a36bf-127">This is appended to the base URL for your API management service.</span></span> <span data-ttu-id="a36bf-128">A URL base é comum para todas as APIs hospedadas em cada instância de um serviço de Gerenciamento da API.</span><span class="sxs-lookup"><span data-stu-id="a36bf-128">The base URL is common for all APIs hosted on each instance of an API Management service.</span></span> <span data-ttu-id="a36bf-129">O Gerenciamento da API diferencia as APIs pelo sufixo e, portanto, o sufixo deve ser único para cada API em uma instância de serviço de gerenciamento de API específica.</span><span class="sxs-lookup"><span data-stu-id="a36bf-129">API Management distinguishes APIs by their suffix and therefore the suffix must be unique for every API in a specific API management service instance.</span></span>

<span data-ttu-id="a36bf-130">Após inserir todos os valores, clique em **Salvar** para criar a API e as operações associadas.</span><span class="sxs-lookup"><span data-stu-id="a36bf-130">Once all values are entered, click **Save** to create the API and the associated operations.</span></span> 

> [!NOTE]
> <span data-ttu-id="a36bf-131">Para obter um tutorial de importação de uma API básica de calculadora no formato Swagger, consulte [Gerenciar sua primeira API no Gerenciamento de API do Azure](api-management-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a36bf-131">For a tutorial of importing a basic calculator API in Swagger format, see [Manage your first API in Azure API Management](api-management-get-started.md).</span></span>
> 
> 

## <span data-ttu-id="a36bf-132"><a name="export-api"> </a> Exportar uma API</span><span class="sxs-lookup"><span data-stu-id="a36bf-132"><a name="export-api"> </a> Export an API</span></span>
<span data-ttu-id="a36bf-133">Além de importar novas APIs, você pode exportar as definições de suas APIs no Portal do editor.</span><span class="sxs-lookup"><span data-stu-id="a36bf-133">In addition to importing new APIs, you can export the definitions of your APIs from the publisher portal.</span></span> <span data-ttu-id="a36bf-134">Para fazer isso, clique em **Exportar API** na **guia de Resumo** de sua **API**.</span><span class="sxs-lookup"><span data-stu-id="a36bf-134">To do so, click **Export API** from the **Summary tab** of your **API**.</span></span>

![Exportar API][api-management-export-api]

<span data-ttu-id="a36bf-136">As APIs podem ser exportadas usando WADL ou Swagger.</span><span class="sxs-lookup"><span data-stu-id="a36bf-136">APIs can be exported using WADL or Swagger.</span></span> <span data-ttu-id="a36bf-137">Selecione o formato desejado, clique em **Salvar**e escolha o local onde deseja salvar o arquivo.</span><span class="sxs-lookup"><span data-stu-id="a36bf-137">Select the desired format, click **Save**, and choose the location in which to save the file.</span></span>

![Exportar formato de API][api-management-export-api-format]

## <span data-ttu-id="a36bf-139"><a name="next-steps"> </a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a36bf-139"><a name="next-steps"> </a>Next steps</span></span>
<span data-ttu-id="a36bf-140">Após criar a API e importar as operações, você pode revisar e definir quaisquer configurações adicionais, adicionar a API a um produto e publicá-la para que fique disponível para desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="a36bf-140">Once an API is created and the operations imported, you can review and configure any additional settings, add the API to a Product, and publish it so that it is available for developers.</span></span> <span data-ttu-id="a36bf-141">Para obter mais informações, consulte os guias a seguir.</span><span class="sxs-lookup"><span data-stu-id="a36bf-141">For more information, see the following guides.</span></span>

* <span data-ttu-id="a36bf-142">[Como definir configurações de API][How to configure API settings]</span><span class="sxs-lookup"><span data-stu-id="a36bf-142">[How to configure API settings][How to configure API settings]</span></span>
* <span data-ttu-id="a36bf-143">[Como criar e publicar um produto][How to create and publish a product]</span><span class="sxs-lookup"><span data-stu-id="a36bf-143">[How to create and publish a product][How to create and publish a product]</span></span>

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

[How to add operations to an API]: api-management-howto-add-operations.md
[How to create and publish a product]: api-management-howto-add-products.md
[How to create APIs]: api-management-howto-create-apis.md
[How to configure API settings]: api-management-howto-create-apis.md#configure-api-settings
