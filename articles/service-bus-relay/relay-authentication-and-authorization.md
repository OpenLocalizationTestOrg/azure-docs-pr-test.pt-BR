---
title: "aaaAzure retransmissão de autenticação e autorização | Microsoft Docs"
description: "Visão geral da autenticação SAS (Assinatura de Acesso Compartilhado) na Retransmissão do Azure"
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm
ms.openlocfilehash: b27914672ce968da2bddba8dafc5683ebf3834ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-authentication-and-authorization"></a>Autenticação e autorização da Retransmissão do Azure
Aplicativos podem se autenticar tooAzure retransmissão usando a autenticação de assinatura de acesso compartilhado (SAS). Semelhante muito[mensagens do barramento de serviço](../service-bus-messaging/service-bus-authentication-and-authorization.md), autenticação SAS permite que aplicativos tooauthenticate toohello serviço de retransmissão do Azure usando uma chave de acesso configurada no namespace de retransmissão hello. Você pode usar essa chave toogenerate um token de assinatura de acesso compartilhado que os clientes podem usar o serviço de retransmissão toohello tooauthenticate.

## <a name="shared-access-signature-authentication"></a>Autenticação SAS
[Autenticação SAS](../service-bus-messaging/service-bus-sas.md) permite que você toogrant um recursos de retransmissão de tooAzure de acesso do usuário com direitos específicos. Autenticação SAS envolve a configuração de saudação de uma chave criptográfica com direitos associados em um recurso. Os clientes podem obter acesso toothat recurso apresentando um token SAS, que consiste em Olá URI de recurso que está sendo acessado e uma expiração assinada com hello configurado chave.

É possível configurar chaves para SAS em um namespace da Retransmissão. Ao contrário do sistema de mensagens do Barramento de Serviço, as [Conexões Híbridas de Retransmissão](relay-hybrid-connections-protocol.md) dão suporte a remetentes anônimos ou não autorizados. Você pode habilitar o acesso anônimo para entidade hello quando ela for criada, conforme mostrado no hello captura do portal de saudação de tela a seguir:

![][0]

toouse SAS, você pode configurar um [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) objeto em um namespace de retransmissão consiste Olá seguinte:

* *KeyName* que identifica a regra de saudação.
* *PrimaryKey* é uma chave criptográfica usada toosign/validar tokens SAS.
* *Chave secundária* é uma chave criptográfica usada toosign/validar tokens SAS.
* *Direitos* que representa a coleção de saudação de escuta, envio ou gerenciamento de direitos concedidos.

Regras de autorização configuradas no nível de namespace Olá podem conceder acesso tooall conexões de retransmissão em um namespace para clientes com tokens assinados usando a chave correspondente hello. Backup too12 tais regras de autorização podem ser configuradas em um namespace de retransmissão. Por padrão, uma [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule) com todos os direitos é configurada para cada namespace quando ele é provisionado pela primeira vez.

tooaccess uma entidade, o cliente Olá requer um token SAS gerado usando um determinado [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule). token SAS Olá é gerado usando Olá HMAC-SHA256 de uma cadeia de caracteres de recurso é composto de acesso de toowhich do URI de recurso de saudação é declarado e uma expiração com uma chave criptográfica associada à regra de autorização de saudação.

Suporte à autenticação de SAS para retransmissão do Azure é incluída no hello Azure .NET SDK versões 2.0 e posterior. A SAS dá suporte a uma [SharedAccessAuthorizationRule](/dotnet/api/microsoft.servicebus.messaging.sharedaccessauthorizationrule). Todas as APIs que aceitam uma cadeia de conexão como parâmetro incluem suporte para cadeias de conexão SAS.

## <a name="next-steps"></a>Próximas etapas
- Continue lendo [Autenticação de Barramento de Serviço com Assinaturas de Acesso Compartilhado](../service-bus-messaging/service-bus-sas.md) para obter mais detalhes sobre SAS.
- Consulte Olá [guia de protocolo de conexões do Azure retransmissão híbridas](relay-hybrid-connections-protocol.md) para obter informações detalhadas sobre Olá recurso conexões híbridas.
- Para informações correspondentes sobre a autenticação do sistema de mensagens do Barramento de Serviço, confira [Autenticação e autorização do Barramento de Serviço](../service-bus-messaging/service-bus-authentication-and-authorization.md). 

[0]: ./media/relay-authentication-and-authorization/hcanon.png