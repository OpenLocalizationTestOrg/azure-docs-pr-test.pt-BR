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
# <a name="service-bus-management-libraries"></a>Bibliotecas de gerenciamento do Barramento de Serviço

bibliotecas de gerenciamento do Azure Service Bus Olá dinamicamente podem provisionar entidades e namespaces de barramento de serviço. Isso permite cenários de mensagens e implantações complexas e torna possível tooprogrammatically determinar quais tooprovision de entidades. Essas bibliotecas estão atualmente disponíveis para .NET.

## <a name="supported-functionality"></a>Funcionalidade com suporte

* Criação, atualização, exclusão de namespace
* Criação da fila, atualização, exclusão
* Criação de tópico, atualização, exclusão
* Criação da assinatura, atualização, exclusão

## <a name="prerequisites"></a>Pré-requisitos

tooget iniciado usando bibliotecas de gerenciamento do Service Bus Olá, deve autenticar com hello serviço Azure Active Directory (AAD). AAD requer que você se autenticar como uma entidade de serviço, que fornece acesso tooyour recursos do Azure. Para saber mais sobre como criar uma entidade de serviço, veja um dos seguintes artigos:  

* [Use o aplicativo do hello toocreate portal do Azure Active Directory e a entidade de serviço que pode acessar os recursos](/azure/azure-resource-manager/resource-group-create-service-principal-portal)
* [Usar Azure PowerShell toocreate um serviço principal tooaccess recursos](/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [Usar um serviço principal tooaccess recursos de toocreate CLI do Azure](/azure/azure-resource-manager/resource-group-authenticate-service-principal-cli)

Esses tutoriais fornecem uma `AppId` (ID do cliente), `TenantId`, e `ClientSecret` (chave de autenticação), que são usados para autenticação, as bibliotecas de gerenciamento de saudação. Você deve ter **proprietário** permissões para grupo de recursos de saudação no qual você deseja toorun.

## <a name="programming-pattern"></a>Padrão de programação

Olá padrão toomanipulate qualquer recurso de barramento de serviço segue um protocolo comum:

1. Obter um token do Active Directory do Azure usando Olá **ActiveDirectory** biblioteca.
   ```csharp
   var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

   var result = await context.AcquireTokenAsync("https://management.core.windows.net/", new ClientCredential(clientId, clientSecret));
   ```

1. Criar hello `ServiceBusManagementClient` objeto.

   ```csharp
   var creds = new TokenCredentials(token);
   var sbClient = new ServiceBusManagementClient(creds)
   {
       SubscriptionId = SettingsCache["SubscriptionId"]
   };
   ```

1. Saudação de conjunto `CreateOrUpdate` valores de parâmetros tooyour especificados.

   ```csharp
   var queueParams = new QueueCreateOrUpdateParameters()
   {
       Location = SettingsCache["DataCenterLocation"],
       EnablePartitioning = true
   };
   ```

1. Olá chamada execute.

   ```csharp
   await sbClient.Queues.CreateOrUpdateAsync(resourceGroupName, namespaceName, QueueName, queueParams);
   ```

## <a name="next-steps"></a>Próximas etapas
* [Amostra de gerenciamento do .NET](https://github.com/Azure-Samples/service-bus-dotnet-management/)
* [Referência de API de Microsoft.Azure.Management.ServiceBus](/dotnet/api/Microsoft.Azure.Management.ServiceBus)
