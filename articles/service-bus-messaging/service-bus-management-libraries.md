---
title: "Bibliotecas de gerenciamento do Barramento de Serviço do Azure | Microsoft Docs"
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
ms.openlocfilehash: 1db00dc1f91e8976b622030450445babbe547ad8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="service-bus-management-libraries"></a><span data-ttu-id="0c361-103">Bibliotecas de gerenciamento do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="0c361-103">Service Bus management libraries</span></span>

<span data-ttu-id="0c361-104">As bibliotecas de gerenciamento do Barramento de Serviço do Azure podem provisionar dinamicamente namespaces e entidades do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="0c361-104">The Azure Service Bus management libraries can dynamically provision Service Bus namespaces and entities.</span></span> <span data-ttu-id="0c361-105">Isso permite implantações e cenários de mensagens complexos e possibilita determinar de forma programática quais entidades provisionar.</span><span class="sxs-lookup"><span data-stu-id="0c361-105">This enables complex deployments and messaging scenarios, and makes it possible to programmatically determine what entities to provision.</span></span> <span data-ttu-id="0c361-106">Essas bibliotecas estão atualmente disponíveis para .NET.</span><span class="sxs-lookup"><span data-stu-id="0c361-106">These libraries are currently available for .NET.</span></span>

## <a name="supported-functionality"></a><span data-ttu-id="0c361-107">Funcionalidade com suporte</span><span class="sxs-lookup"><span data-stu-id="0c361-107">Supported functionality</span></span>

* <span data-ttu-id="0c361-108">Criação, atualização, exclusão de namespace</span><span class="sxs-lookup"><span data-stu-id="0c361-108">Namespace creation, update, deletion</span></span>
* <span data-ttu-id="0c361-109">Criação da fila, atualização, exclusão</span><span class="sxs-lookup"><span data-stu-id="0c361-109">Queue creation, update, deletion</span></span>
* <span data-ttu-id="0c361-110">Criação de tópico, atualização, exclusão</span><span class="sxs-lookup"><span data-stu-id="0c361-110">Topic creation, update, deletion</span></span>
* <span data-ttu-id="0c361-111">Criação da assinatura, atualização, exclusão</span><span class="sxs-lookup"><span data-stu-id="0c361-111">Subscription creation, update, deletion</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0c361-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0c361-112">Prerequisites</span></span>

<span data-ttu-id="0c361-113">Para começar a usar as bibliotecas de gerenciamento do Barramento de Serviço, você deve se autenticar com o serviço AAD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="0c361-113">To get started using the Service Bus management libraries, you must authenticate with the Azure Active Directory (AAD) service.</span></span> <span data-ttu-id="0c361-114">AAD exige que você autentique como uma entidade de serviço, que fornece acesso aos recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="0c361-114">AAD requires that you authenticate as a service principal, which provides access to your Azure resources.</span></span> <span data-ttu-id="0c361-115">Para saber mais sobre como criar uma entidade de serviço, veja um dos seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="0c361-115">For information about creating a service principal, see one of these articles:</span></span>  

* [<span data-ttu-id="0c361-116">Usar o portal do Azure para criar um aplicativo e entidade de serviço do Active Directory que pode acessar recursos</span><span class="sxs-lookup"><span data-stu-id="0c361-116">Use the Azure portal to create Active Directory application and service principal that can access resources</span></span>](/azure/azure-resource-manager/resource-group-create-service-principal-portal)
* [<span data-ttu-id="0c361-117">Usar o Azure PowerShell para criar uma entidade de serviço a fim de acessar recursos</span><span class="sxs-lookup"><span data-stu-id="0c361-117">Use Azure PowerShell to create a service principal to access resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="0c361-118">Usar a CLI do Azure para criar uma entidade de serviço a fim de acessar recursos</span><span class="sxs-lookup"><span data-stu-id="0c361-118">Use Azure CLI to create a service principal to access resources</span></span>](/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)

<span data-ttu-id="0c361-119">Estes tutoriais fornecem uma `AppId` (ID do Cliente), `TenantId` e `ClientSecret` (chave de autenticação), todas usadas para autenticação pelas bibliotecas de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="0c361-119">These tutorials provide you with an `AppId` (Client ID), `TenantId`, and `ClientSecret` (authentication key), all of which are used for authentication by the management libraries.</span></span> <span data-ttu-id="0c361-120">Você deve ter as permissões **Proprietário** para o grupo de recursos no qual você deseja executar.</span><span class="sxs-lookup"><span data-stu-id="0c361-120">You must have **Owner** permissions for the resource group on which you wish to run.</span></span>

## <a name="programming-pattern"></a><span data-ttu-id="0c361-121">Padrão de programação</span><span class="sxs-lookup"><span data-stu-id="0c361-121">Programming pattern</span></span>

<span data-ttu-id="0c361-122">O padrão para manipular qualquer recurso do Barramento de Serviço segue um protocolo comum:</span><span class="sxs-lookup"><span data-stu-id="0c361-122">The pattern to manipulate any Service Bus resource follows a common protocol:</span></span>

1. <span data-ttu-id="0c361-123">Obtenha um token do Azure Active Directory usando a biblioteca **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="0c361-123">Obtain a token from Azure Active Directory using the **Microsoft.IdentityModel.Clients.ActiveDirectory** library.</span></span>
   ```csharp
   var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

   var result = await context.AcquireTokenAsync("https://management.core.windows.net/", new ClientCredential(clientId, clientSecret));
   ```

1. <span data-ttu-id="0c361-124">Crie o objeto `ServiceBusManagementClient`.</span><span class="sxs-lookup"><span data-stu-id="0c361-124">Create the `ServiceBusManagementClient` object.</span></span>

   ```csharp
   var creds = new TokenCredentials(token);
   var sbClient = new ServiceBusManagementClient(creds)
   {
       SubscriptionId = SettingsCache["SubscriptionId"]
   };
   ```

1. <span data-ttu-id="0c361-125">Defina os parâmetros `CreateOrUpdate` com os valores especificados.</span><span class="sxs-lookup"><span data-stu-id="0c361-125">Set the `CreateOrUpdate` parameters to your specified values.</span></span>

   ```csharp
   var queueParams = new QueueCreateOrUpdateParameters()
   {
       Location = SettingsCache["DataCenterLocation"],
       EnablePartitioning = true
   };
   ```

1. <span data-ttu-id="0c361-126">Execute a chamada.</span><span class="sxs-lookup"><span data-stu-id="0c361-126">Execute the call.</span></span>

   ```csharp
   await sbClient.Queues.CreateOrUpdateAsync(resourceGroupName, namespaceName, QueueName, queueParams);
   ```

## <a name="next-steps"></a><span data-ttu-id="0c361-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0c361-127">Next steps</span></span>
* [<span data-ttu-id="0c361-128">Amostra de gerenciamento do .NET</span><span class="sxs-lookup"><span data-stu-id="0c361-128">.NET management sample</span></span>](https://github.com/Azure-Samples/service-bus-dotnet-management/)
* [<span data-ttu-id="0c361-129">Referência de API de Microsoft.Azure.Management.ServiceBus</span><span class="sxs-lookup"><span data-stu-id="0c361-129">Microsoft.Azure.Management.ServiceBus API reference</span></span>](/dotnet/api/Microsoft.Azure.Management.ServiceBus)
