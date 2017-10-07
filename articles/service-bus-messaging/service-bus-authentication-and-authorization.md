---
title: "aaaAzure barramento de serviço de autenticação e autorização | Microsoft Docs"
description: "Autentica aplicativos tooService barramento com autenticação de assinatura de acesso compartilhado (SAS)."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 18bad0ed-1cee-4a5c-a377-facc4785c8c9
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/09/2017
ms.author: sethm
ms.openlocfilehash: 898a2144c99d8fac074b6d85604f710bf512e71e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-authentication-and-authorization"></a>Autenticação e autorização do Barramento de Serviço

Aplicativos podem se autenticar tooAzure barramento de serviço usando a assinatura de acesso compartilhado (SAS) autenticação. Compartilhado assinatura de acesso autenticação permite que aplicativos tooauthenticate tooService barramento usando uma chave de acesso configurada no namespace hello, ou na entidade Olá com a qual direitos específicos associados. Você pode usar essa chave toogenerate um token de assinatura de acesso compartilhado que os clientes podem usar tooauthenticate tooService barramento.

> [!IMPORTANT]
> Você deve usar a SAS em vez do Controle de Acesso do Azure Active Directory c(também conhecido como Serviço de Controle de Acesso ou ACS), já que o ACS está sendo preterido. A SAS fornece um esquema de autenticação simples, flexível e fácil de usar para o Barramento de Serviço. Os aplicativos podem usar SAS em cenários em que eles não precisarem toomanage noção de saudação de um "usuário" autorizado. Para saber mais, confira [esta postagem no blog](https://blogs.msdn.microsoft.com/servicebus/2017/06/01/upcoming-changes-to-acs-enabled-namespaces/).

## <a name="shared-access-signature-authentication"></a>Autenticação SAS

[Autenticação SAS](service-bus-sas.md) permite que você toogrant um recursos de barramento de tooService de acesso do usuário com direitos específicos. Autenticação de SAS no barramento de serviço envolve a configuração de saudação de uma chave criptográfica com direitos associados em um recurso de barramento de serviço. Os clientes podem obter acesso toothat recurso apresentando um token SAS, que consiste em Olá URI de recurso que está sendo acessado e uma expiração assinada com hello configurado chave.

É possível configurar chaves para SAS em um namespace do Barramento de Serviço. chave Olá se aplica a entidades de mensagens tooall naquele namespace. Também é possível configurar chaves em tópicos e filas do Barramento de Serviço. Também há suporte para SAS na [Retransmissão do Azure](../service-bus-relay/relay-authentication-and-authorization.md).

toouse SAS, você pode configurar um [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) objeto em um namespace, fila ou tópico. Essa regra consiste Olá elementos a seguir:

* *KeyName* que identifica a regra de saudação.
* *PrimaryKey* é uma chave criptográfica usada toosign/validar tokens SAS.
* *Chave secundária* é uma chave criptográfica usada toosign/validar tokens SAS.
* *Direitos* que representa a coleção de saudação de escuta, envio ou gerenciamento de direitos concedidos.

Regras de autorização configuradas no nível de namespace Olá podem conceder acesso tooall entidades em um namespace para clientes com tokens assinados usando a chave correspondente hello. Backup too12 tais regras de autorização podem ser configuradas em um namespace, fila ou tópico do barramento de serviço. Por padrão, uma [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) com todos os direitos é configurada para cada namespace quando ele é provisionado pela primeira vez.

tooaccess uma entidade, o cliente Olá requer um token SAS gerado usando um determinado [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule). token SAS Olá é gerado usando Olá HMAC-SHA256 de uma cadeia de caracteres de recurso é composto de acesso de toowhich do URI de recurso de saudação é declarado e uma expiração com uma chave criptográfica associada à regra de autorização de saudação.

Suporte à autenticação de SAS para o barramento de serviço é incluída no hello Azure .NET SDK versões 2.0 e posterior. A SAS dá suporte a uma [SharedAccessAuthorizationRule](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule). Todas as APIs que aceitam uma cadeia de conexão como parâmetro incluem suporte para cadeias de conexão SAS.

## <a name="next-steps"></a>Próximas etapas

- Continue lendo [Autenticação de Barramento de Serviço com Assinaturas de Acesso Compartilhado](service-bus-sas.md) para obter mais detalhes sobre SAS.
- [Altera tooACS habilitado namespaces.](https://blogs.msdn.microsoft.com/servicebus/2017/06/01/upcoming-changes-to-acs-enabled-namespaces/)
- Para informações correspondentes sobre a autenticação e autorização da Retransmissão do Azure, confira [Autenticação e autorização da Retransmissão do Azure](../service-bus-relay/relay-authentication-and-authorization.md). 

