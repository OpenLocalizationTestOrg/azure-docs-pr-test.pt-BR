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
# <a name="event-hubs-management-libraries"></a>Bibliotecas de gerenciamento dos Hubs de Eventos

bibliotecas de gerenciamento de Hubs de eventos Olá dinamicamente podem provisionar entidades e namespaces de Hubs de eventos. Isso permite implantações complexas e cenários de mensagens, para que você possa determinar programaticamente tooprovision quais entidades. Essas bibliotecas estão atualmente disponíveis para .NET.

## <a name="supported-functionality"></a>Funcionalidade com suporte

* Criação, atualização, exclusão de namespace
* Criação de Hubs de eventos, atualização, exclusão
* Criação de grupo de consumidores, atualização, exclusão

## <a name="prerequisites"></a>Pré-requisitos

tooget iniciado usando bibliotecas de gerenciamento de Hubs de eventos hello, você deverá se autenticar com o Azure Active Directory (AAD). AAD requer que você se autenticar como uma entidade de serviço, que fornece acesso tooyour recursos do Azure. Para saber mais sobre como criar uma entidade de serviço, veja um dos seguintes artigos:  

* [Use o aplicativo do hello toocreate portal do Azure Active Directory e a entidade de serviço que pode acessar os recursos](../azure-resource-manager/resource-group-create-service-principal-portal.md)
* [Usar Azure PowerShell toocreate um serviço principal tooaccess recursos](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [Usar um serviço principal tooaccess recursos de toocreate CLI do Azure](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md)

Esses tutoriais fornecem uma `AppId` (ID do cliente), `TenantId`, e `ClientSecret` (chave de autenticação), que são usados para autenticação, as bibliotecas de gerenciamento de saudação. Você deve ter **proprietário** permissões para grupo de recursos de saudação no qual você deseja toorun.

## <a name="programming-pattern"></a>Padrão de programação

Olá padrão toomanipulate qualquer recurso de Hubs de eventos segue um protocolo comum:

1. Obter um token do AAD usando Olá `Microsoft.IdentityModel.Clients.ActiveDirectory` biblioteca.
    ```csharp
    var context = new AuthenticationContext($"https://login.microsoftonline.com/{tenantId}");

    var result = await context.AcquireTokenAsync(
        "https://management.core.windows.net/",
        new ClientCredential(clientId, clientSecret)
    );
    ```

1. Criar hello `EventHubManagementClient` objeto.
    ```csharp
    var creds = new TokenCredentials(token);
    var ehClient = new EventHubManagementClient(creds)
    {
        SubscriptionId = SettingsCache["SubscriptionId"]
    };
    ```

1. Saudação de conjunto `CreateOrUpdate` valores de parâmetros tooyour especificados.
    ```csharp
    var ehParams = new EventHubCreateOrUpdateParameters()
    {
        Location = SettingsCache["DataCenterLocation"]
    };
    ```

1. Olá chamada execute.
    ```csharp
    await ehClient.EventHubs.CreateOrUpdateAsync(resourceGroupName, namespaceName, EventHubName, ehParams);
    ```

## <a name="next-steps"></a>Próximas etapas
* [Exemplo do Gerenciamento do .NET](https://github.com/Azure-Samples/event-hubs-dotnet-management/)
* [Referência de Microsoft.Azure.Management.EventHub](/dotnet/api/Microsoft.Azure.Management.EventHub) 
