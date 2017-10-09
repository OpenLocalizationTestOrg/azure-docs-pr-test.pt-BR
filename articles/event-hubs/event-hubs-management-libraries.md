---
title: bibliotecas de gerenciamento de Hubs de eventos aaaAzure | Microsoft Docs
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
ms.openlocfilehash: b7db0077f6f31397ae46e926c3c28630a157824c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-management-libraries"></a><span data-ttu-id="0dd01-103">Bibliotecas de gerenciamento dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="0dd01-103">Event Hubs management libraries</span></span>

<span data-ttu-id="0dd01-104">bibliotecas de gerenciamento de Hubs de eventos Olá dinamicamente podem provisionar entidades e namespaces de Hubs de eventos.</span><span class="sxs-lookup"><span data-stu-id="0dd01-104">hello Event Hubs management libraries can dynamically provision Event Hubs namespaces and entities.</span></span> <span data-ttu-id="0dd01-105">Isso permite implantações complexas e cenários de mensagens, para que você possa determinar programaticamente tooprovision quais entidades.</span><span class="sxs-lookup"><span data-stu-id="0dd01-105">This enables complex deployments and messaging scenarios, so that you can programmatically determine what entities tooprovision.</span></span> <span data-ttu-id="0dd01-106">Essas bibliotecas estão atualmente disponíveis para .NET.</span><span class="sxs-lookup"><span data-stu-id="0dd01-106">These libraries are currently available for .NET.</span></span>

## <a name="supported-functionality"></a><span data-ttu-id="0dd01-107">Funcionalidade com suporte</span><span class="sxs-lookup"><span data-stu-id="0dd01-107">Supported functionality</span></span>

* <span data-ttu-id="0dd01-108">Criação, atualização, exclusão de namespace</span><span class="sxs-lookup"><span data-stu-id="0dd01-108">Namespace creation, update, deletion</span></span>
* <span data-ttu-id="0dd01-109">Criação de Hubs de eventos, atualização, exclusão</span><span class="sxs-lookup"><span data-stu-id="0dd01-109">Event Hubs creation, update, deletion</span></span>
* <span data-ttu-id="0dd01-110">Criação de grupo de consumidores, atualização, exclusão</span><span class="sxs-lookup"><span data-stu-id="0dd01-110">Consumer Group creation, update, deletion</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0dd01-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0dd01-111">Prerequisites</span></span>

<span data-ttu-id="0dd01-112">tooget iniciado usando bibliotecas de gerenciamento de Hubs de eventos hello, você deverá se autenticar com o Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="0dd01-112">tooget started using hello Event Hubs management libraries, you must authenticate with Azure Active Directory (AAD).</span></span> <span data-ttu-id="0dd01-113">AAD requer que você se autenticar como uma entidade de serviço, que fornece acesso tooyour recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="0dd01-113">AAD requires that you authenticate as a service principal, which provides access tooyour Azure resources.</span></span> <span data-ttu-id="0dd01-114">Para saber mais sobre como criar uma entidade de serviço, veja um dos seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="0dd01-114">For information about creating a service principal, see one of these articles:</span></span>  

* [<span data-ttu-id="0dd01-115">Use o aplicativo do hello toocreate portal do Azure Active Directory e a entidade de serviço que pode acessar os recursos</span><span class="sxs-lookup"><span data-stu-id="0dd01-115">Use hello Azure portal toocreate Active Directory application and service principal that can access resources</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [<span data-ttu-id="0dd01-116">Usar Azure PowerShell toocreate um serviço principal tooaccess recursos</span><span class="sxs-lookup"><span data-stu-id="0dd01-116">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="0dd01-117">Usar um serviço principal tooaccess recursos de toocreate CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="0dd01-117">Use Azure CLI toocreate a service principal tooaccess resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md)

<span data-ttu-id="0dd01-118">Esses tutoriais fornecem uma `AppId` (ID do cliente), `TenantId`, e `ClientSecret` (chave de autenticação), que são usados para autenticação, as bibliotecas de gerenciamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="0dd01-118">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by hello management libraries.</span></span> <span data-ttu-id="0dd01-119">Você deve ter **proprietário** permissões para grupo de recursos de saudação no qual você deseja toorun.</span><span class="sxs-lookup"><span data-stu-id="0dd01-119">You must have **Owner** permissions for hello resource group on which you want toorun.</span></span>

## <a name="programming-pattern"></a><span data-ttu-id="0dd01-120">Padrão de programação</span><span class="sxs-lookup"><span data-stu-id="0dd01-120">Programming pattern</span></span>

<span data-ttu-id="0dd01-121">Olá padrão toomanipulate qualquer recurso de Hubs de eventos segue um protocolo comum:</span><span class="sxs-lookup"><span data-stu-id="0dd01-121">hello pattern toomanipulate any Event Hubs resource follows a common protocol:</span></span>

1. <span data-ttu-id="0dd01-122">Obter um token do AAD usando Olá `Microsoft.IdentityModel.Clients.ActiveDirectory` biblioteca.</span><span class="sxs-lookup"><span data-stu-id="0dd01-122">Obtain a token from AAD using hello `Microsoft.IdentityModel.Clients.ActiveDirectory` library.</span></span>
    ```csharp
    var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

    var result = await context.AcquireTokenAsync(
        "https://management.core.windows.net/",
        new ClientCredential(clientId, clientSecret)
    );
    ```

1. <span data-ttu-id="0dd01-123">Criar hello `EventHubManagementClient` objeto.</span><span class="sxs-lookup"><span data-stu-id="0dd01-123">Create hello `EventHubManagementClient` object.</span></span>
    ```csharp
    var creds = new TokenCredentials(token);
    var ehClient = new EventHubManagementClient(creds)
    {
        SubscriptionId = SettingsCache["SubscriptionId"]
    };
    ```

1. <span data-ttu-id="0dd01-124">Saudação de conjunto `CreateOrUpdate` valores de parâmetros tooyour especificados.</span><span class="sxs-lookup"><span data-stu-id="0dd01-124">Set hello `CreateOrUpdate` parameters tooyour specified values.</span></span>
    ```csharp
    var ehParams = new EventHubCreateOrUpdateParameters()
    {
        Location = SettingsCache["DataCenterLocation"]
    };
    ```

1. <span data-ttu-id="0dd01-125">Olá chamada execute.</span><span class="sxs-lookup"><span data-stu-id="0dd01-125">Execute hello call.</span></span>
    ```csharp
    await ehClient.EventHubs.CreateOrUpdateAsync(resourceGroupName, namespaceName, EventHubName, ehParams);
    ```

## <a name="next-steps"></a><span data-ttu-id="0dd01-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0dd01-126">Next steps</span></span>
* [<span data-ttu-id="0dd01-127">Exemplo do Gerenciamento do .NET</span><span class="sxs-lookup"><span data-stu-id="0dd01-127">.NET Management sample</span></span>](https://github.com/Azure-Samples/event-hubs-dotnet-management/)
* [<span data-ttu-id="0dd01-128">Referência de Microsoft.Azure.Management.EventHub</span><span class="sxs-lookup"><span data-stu-id="0dd01-128">Microsoft.Azure.Management.EventHub Reference</span></span>](/dotnet/api/Microsoft.Azure.Management.EventHub) 
