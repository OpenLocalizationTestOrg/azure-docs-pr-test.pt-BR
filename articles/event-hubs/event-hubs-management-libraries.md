---
title: Bibliotecas de gerenciamento dos Hubs de Eventos do Azure | Microsoft Docs
description: Gerenciar namespaces de Hubs de eventos e entidades do .NET
services: event-hubs
cloud: na
documentationcenter: na
author: sethmanheim
manager: timlt
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 0d659cb860a6c98342b548212820efe046decfcc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="event-hubs-management-libraries"></a><span data-ttu-id="acf83-103">Bibliotecas de gerenciamento dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="acf83-103">Event Hubs management libraries</span></span>

<span data-ttu-id="acf83-104">As bibliotecas de gerenciamento de Hubs de eventos podem provisionar dinamicamente entidades e namespaces de Hubs de eventos.</span><span class="sxs-lookup"><span data-stu-id="acf83-104">The Event Hubs management libraries can dynamically provision Event Hubs namespaces and entities.</span></span> <span data-ttu-id="acf83-105">Isso permite implantações e cenários de mensagens complexos, de modo que você possa determinar de forma programática quais entidades provisionar.</span><span class="sxs-lookup"><span data-stu-id="acf83-105">This enables complex deployments and messaging scenarios, so that you can programmatically determine what entities to provision.</span></span> <span data-ttu-id="acf83-106">Essas bibliotecas estão atualmente disponíveis para .NET.</span><span class="sxs-lookup"><span data-stu-id="acf83-106">These libraries are currently available for .NET.</span></span>

## <a name="supported-functionality"></a><span data-ttu-id="acf83-107">Funcionalidade com suporte</span><span class="sxs-lookup"><span data-stu-id="acf83-107">Supported functionality</span></span>

* <span data-ttu-id="acf83-108">Criação, atualização, exclusão de namespace</span><span class="sxs-lookup"><span data-stu-id="acf83-108">Namespace creation, update, deletion</span></span>
* <span data-ttu-id="acf83-109">Criação de Hubs de eventos, atualização, exclusão</span><span class="sxs-lookup"><span data-stu-id="acf83-109">Event Hubs creation, update, deletion</span></span>
* <span data-ttu-id="acf83-110">Criação de grupo de consumidores, atualização, exclusão</span><span class="sxs-lookup"><span data-stu-id="acf83-110">Consumer Group creation, update, deletion</span></span>

## <a name="prerequisites"></a><span data-ttu-id="acf83-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="acf83-111">Prerequisites</span></span>

<span data-ttu-id="acf83-112">Para começar a usar as bibliotecas de gerenciamento de Hubs de eventos, você deverá se autenticar com o Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="acf83-112">To get started using the Event Hubs management libraries, you must authenticate with Azure Active Directory (AAD).</span></span> <span data-ttu-id="acf83-113">AAD exige que você autentique como uma entidade de serviço, que fornece acesso aos recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="acf83-113">AAD requires that you authenticate as a service principal, which provides access to your Azure resources.</span></span> <span data-ttu-id="acf83-114">Para saber mais sobre como criar uma entidade de serviço, veja um dos seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="acf83-114">For information about creating a service principal, see one of these articles:</span></span>  

* [<span data-ttu-id="acf83-115">Usar o portal do Azure para criar um aplicativo e entidade de serviço do Active Directory que pode acessar recursos</span><span class="sxs-lookup"><span data-stu-id="acf83-115">Use the Azure portal to create Active Directory application and service principal that can access resources</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [<span data-ttu-id="acf83-116">Usar o Azure PowerShell para criar uma entidade de serviço a fim de acessar recursos</span><span class="sxs-lookup"><span data-stu-id="acf83-116">Use Azure PowerShell to create a service principal to access resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="acf83-117">Usar a CLI do Azure para criar uma entidade de serviço a fim de acessar recursos</span><span class="sxs-lookup"><span data-stu-id="acf83-117">Use Azure CLI to create a service principal to access resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md)

<span data-ttu-id="acf83-118">Estes tutoriais fornecem uma `AppId` (ID do Cliente), `TenantId` e `ClientSecret` (chave de autenticação), todas usadas para autenticação pelas bibliotecas de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="acf83-118">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by the management libraries.</span></span> <span data-ttu-id="acf83-119">Você deve ter permissões de **Proprietário** para o grupo de recursos no qual você deseja executar.</span><span class="sxs-lookup"><span data-stu-id="acf83-119">You must have **Owner** permissions for the resource group on which you want to run.</span></span>

## <a name="programming-pattern"></a><span data-ttu-id="acf83-120">Padrão de programação</span><span class="sxs-lookup"><span data-stu-id="acf83-120">Programming pattern</span></span>

<span data-ttu-id="acf83-121">O padrão para manipular qualquer recurso de Hubs de eventos a seguir, um protocolo comum:</span><span class="sxs-lookup"><span data-stu-id="acf83-121">The pattern to manipulate any Event Hubs resource follows a common protocol:</span></span>

1. <span data-ttu-id="acf83-122">Obtenha um token do AAD usando a biblioteca `Microsoft.IdentityModel.Clients.ActiveDirectory`.</span><span class="sxs-lookup"><span data-stu-id="acf83-122">Obtain a token from AAD using the `Microsoft.IdentityModel.Clients.ActiveDirectory` library.</span></span>
    ```csharp
    var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

    var result = await context.AcquireTokenAsync(
        "https://management.core.windows.net/",
        new ClientCredential(clientId, clientSecret)
    );
    ```

1. <span data-ttu-id="acf83-123">Crie o objeto `EventHubManagementClient`.</span><span class="sxs-lookup"><span data-stu-id="acf83-123">Create the `EventHubManagementClient` object.</span></span>
    ```csharp
    var creds = new TokenCredentials(token);
    var ehClient = new EventHubManagementClient(creds)
    {
        SubscriptionId = SettingsCache["SubscriptionId"]
    };
    ```

1. <span data-ttu-id="acf83-124">Defina os parâmetros `CreateOrUpdate` com os valores especificados.</span><span class="sxs-lookup"><span data-stu-id="acf83-124">Set the `CreateOrUpdate` parameters to your specified values.</span></span>
    ```csharp
    var ehParams = new EventHubCreateOrUpdateParameters()
    {
        Location = SettingsCache["DataCenterLocation"]
    };
    ```

1. <span data-ttu-id="acf83-125">Execute a chamada.</span><span class="sxs-lookup"><span data-stu-id="acf83-125">Execute the call.</span></span>
    ```csharp
    await ehClient.EventHubs.CreateOrUpdateAsync(resourceGroupName, namespaceName, EventHubName, ehParams);
    ```

## <a name="next-steps"></a><span data-ttu-id="acf83-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="acf83-126">Next steps</span></span>
* [<span data-ttu-id="acf83-127">Exemplo do Gerenciamento do .NET</span><span class="sxs-lookup"><span data-stu-id="acf83-127">.NET Management sample</span></span>](https://github.com/Azure-Samples/event-hubs-dotnet-management/)
* [<span data-ttu-id="acf83-128">Referência de Microsoft.Azure.Management.EventHub</span><span class="sxs-lookup"><span data-stu-id="acf83-128">Microsoft.Azure.Management.EventHub Reference</span></span>](/dotnet/api/Microsoft.Azure.Management.EventHub) 
