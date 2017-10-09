---
title: "bibliotecas de gerenciamento do barramento de serviço aaaAzure | Microsoft Docs"
description: "Gerencie namespaces e entidades de mensagens do Barramento de Serviço no .NET."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: sethm
ms.openlocfilehash: 9e4ad91f22815ca0838e6e4647a3606109b2b441
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-management-libraries"></a><span data-ttu-id="7fa5c-103">Bibliotecas de gerenciamento do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="7fa5c-103">Service Bus management libraries</span></span>

<span data-ttu-id="7fa5c-104">bibliotecas de gerenciamento do Azure Service Bus Olá dinamicamente podem provisionar entidades e namespaces de barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="7fa5c-104">hello Azure Service Bus management libraries can dynamically provision Service Bus namespaces and entities.</span></span> <span data-ttu-id="7fa5c-105">Isso permite cenários de mensagens e implantações complexas e torna possível tooprogrammatically determinar quais tooprovision de entidades.</span><span class="sxs-lookup"><span data-stu-id="7fa5c-105">This enables complex deployments and messaging scenarios, and makes it possible tooprogrammatically determine what entities tooprovision.</span></span> <span data-ttu-id="7fa5c-106">Essas bibliotecas estão atualmente disponíveis para .NET.</span><span class="sxs-lookup"><span data-stu-id="7fa5c-106">These libraries are currently available for .NET.</span></span>

## <a name="supported-functionality"></a><span data-ttu-id="7fa5c-107">Funcionalidade com suporte</span><span class="sxs-lookup"><span data-stu-id="7fa5c-107">Supported functionality</span></span>

* <span data-ttu-id="7fa5c-108">Criação, atualização, exclusão de namespace</span><span class="sxs-lookup"><span data-stu-id="7fa5c-108">Namespace creation, update, deletion</span></span>
* <span data-ttu-id="7fa5c-109">Criação da fila, atualização, exclusão</span><span class="sxs-lookup"><span data-stu-id="7fa5c-109">Queue creation, update, deletion</span></span>
* <span data-ttu-id="7fa5c-110">Criação de tópico, atualização, exclusão</span><span class="sxs-lookup"><span data-stu-id="7fa5c-110">Topic creation, update, deletion</span></span>
* <span data-ttu-id="7fa5c-111">Criação da assinatura, atualização, exclusão</span><span class="sxs-lookup"><span data-stu-id="7fa5c-111">Subscription creation, update, deletion</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7fa5c-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7fa5c-112">Prerequisites</span></span>

<span data-ttu-id="7fa5c-113">tooget iniciado usando bibliotecas de gerenciamento do Service Bus Olá, deve autenticar com hello serviço Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="7fa5c-113">tooget started using hello Service Bus management libraries, you must authenticate with hello Azure Active Directory (AAD) service.</span></span> <span data-ttu-id="7fa5c-114">AAD requer que você se autenticar como uma entidade de serviço, que fornece acesso tooyour recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="7fa5c-114">AAD requires that you authenticate as a service principal, which provides access tooyour Azure resources.</span></span> <span data-ttu-id="7fa5c-115">Para saber mais sobre como criar uma entidade de serviço, veja um dos seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="7fa5c-115">For information about creating a service principal, see one of these articles:</span></span>  

* [<span data-ttu-id="7fa5c-116">Use o aplicativo do hello toocreate portal do Azure Active Directory e a entidade de serviço que pode acessar os recursos</span><span class="sxs-lookup"><span data-stu-id="7fa5c-116">Use hello Azure portal toocreate Active Directory application and service principal that can access resources</span></span>](/azure/azure-resource-manager/resource-group-create-service-principal-portal)
* [<span data-ttu-id="7fa5c-117">Usar Azure PowerShell toocreate um serviço principal tooaccess recursos</span><span class="sxs-lookup"><span data-stu-id="7fa5c-117">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="7fa5c-118">Usar um serviço principal tooaccess recursos de toocreate CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="7fa5c-118">Use Azure CLI toocreate a service principal tooaccess resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)

<span data-ttu-id="7fa5c-119">Esses tutoriais fornecem uma `AppId` (ID do cliente), `TenantId`, e `ClientSecret` (chave de autenticação), que são usados para autenticação, as bibliotecas de gerenciamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="7fa5c-119">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by hello management libraries.</span></span> <span data-ttu-id="7fa5c-120">Você deve ter **proprietário** permissões para grupo de recursos de saudação no qual você deseja toorun.</span><span class="sxs-lookup"><span data-stu-id="7fa5c-120">You must have **Owner** permissions for hello resource group on which you wish toorun.</span></span>

## <a name="programming-pattern"></a><span data-ttu-id="7fa5c-121">Padrão de programação</span><span class="sxs-lookup"><span data-stu-id="7fa5c-121">Programming pattern</span></span>

<span data-ttu-id="7fa5c-122">Olá padrão toomanipulate qualquer recurso de barramento de serviço segue um protocolo comum:</span><span class="sxs-lookup"><span data-stu-id="7fa5c-122">hello pattern toomanipulate any Service Bus resource follows a common protocol:</span></span>

1. <span data-ttu-id="7fa5c-123">Obter um token do Active Directory do Azure usando Olá **ActiveDirectory** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="7fa5c-123">Obtain a token from Azure Active Directory using hello **Microsoft.IdentityModel.Clients.ActiveDirectory** library.</span></span>
   ```csharp
   var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

   var result = await context.AcquireTokenAsync("https://management.core.windows.net/", new ClientCredential(clientId, clientSecret));
   ```

1. <span data-ttu-id="7fa5c-124">Criar hello `ServiceBusManagementClient` objeto.</span><span class="sxs-lookup"><span data-stu-id="7fa5c-124">Create hello `ServiceBusManagementClient` object.</span></span>

   ```csharp
   var creds = new TokenCredentials(token);
   var sbClient = new ServiceBusManagementClient(creds)
   {
       SubscriptionId = SettingsCache["SubscriptionId"]
   };
   ```

1. <span data-ttu-id="7fa5c-125">Saudação de conjunto `CreateOrUpdate` valores de parâmetros tooyour especificados.</span><span class="sxs-lookup"><span data-stu-id="7fa5c-125">Set hello `CreateOrUpdate` parameters tooyour specified values.</span></span>

   ```csharp
   var queueParams = new QueueCreateOrUpdateParameters()
   {
       Location = SettingsCache["DataCenterLocation"],
       EnablePartitioning = true
   };
   ```

1. <span data-ttu-id="7fa5c-126">Olá chamada execute.</span><span class="sxs-lookup"><span data-stu-id="7fa5c-126">Execute hello call.</span></span>

   ```csharp
   await sbClient.Queues.CreateOrUpdateAsync(resourceGroupName, namespaceName, QueueName, queueParams);
   ```

## <a name="next-steps"></a><span data-ttu-id="7fa5c-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7fa5c-127">Next steps</span></span>
* [<span data-ttu-id="7fa5c-128">Amostra de gerenciamento do .NET</span><span class="sxs-lookup"><span data-stu-id="7fa5c-128">.NET management sample</span></span>](https://github.com/Azure-Samples/service-bus-dotnet-management/)
* [<span data-ttu-id="7fa5c-129">Referência de API de Microsoft.Azure.Management.ServiceBus</span><span class="sxs-lookup"><span data-stu-id="7fa5c-129">Microsoft.Azure.Management.ServiceBus API reference</span></span>](/dotnet/api/Microsoft.Azure.Management.ServiceBus)
