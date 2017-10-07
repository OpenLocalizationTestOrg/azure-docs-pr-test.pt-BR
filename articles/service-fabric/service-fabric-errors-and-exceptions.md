---
title: "aaaCommon FabricClient exceções lançadas | Microsoft Docs"
description: "Descreve as exceções do common hello e erros que podem ser gerados por Olá FabricClient APIs ao realizar operações de gerenciamento de aplicativo e o cluster."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: bb821313-b221-479f-b08e-36cf07e60a07
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: ryanwi
ms.openlocfilehash: 55bb556b25150524ebc28756eb1bd3e91dc37853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="common-exceptions-and-errors-when-working-with-hello-fabricclient-apis"></a>Exceções e erros ao trabalhar com hello FabricClient APIs comuns
Olá [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) APIs permitem cluster e aplicativo administradores tooperform tarefas administrativas em um aplicativo, serviço ou cluster do Service Fabric. Por exemplo, implantação de aplicativo, atualização e remoção, verificando a integridade da saudação um cluster ou um serviço de teste. Os desenvolvedores de aplicativos e os administradores de cluster podem usar ferramentas de toodevelop Olá FabricClient APIs para gerenciamento de aplicativos e o cluster do Service Fabric hello.

Há muitos tipos de operações diferentes que podem ser executados usando o FabricClient.  Cada método pode lançar exceções para erros devido a entrada tooincorrect, erros de tempo de execução ou problemas de infraestrutura transitório.  Consulte toofind de documentação de referência Olá API quais exceções são geradas por um método específico. Há algumas exceções, no entanto, que podem ser lançadas por várias APIs [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) diferentes. Olá, tabela a seguir lista exceções Olá que são comuns em Olá FabricClient APIs.

| Exceção | Gerada quando |
| --- |:--- |
| [System.Fabric.FabricObjectClosedException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricobjectclosedexception#System_Fabric_FabricObjectClosedException) |Olá [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) objeto está em um estado fechado. Descartar Olá [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) está usando e criar uma instância de um novo objeto [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) objeto. |
| [System.TimeoutException](https://docs.microsoft.com/dotnet/core/api/system.timeoutexception#System_TimeoutException) |tempo limite da operação de saudação. [OperationTimedOut](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode#System_Fabric_FabricErrorCode) é retornado quando a operação de saudação leva mais de toocomplete MaxOperationTimeout. |
| [System.UnauthorizedAccessException](https://docs.microsoft.com/dotnet/core/api/system.unauthorizedaccessexception#System_UnauthorizedAccessException) |Falha na verificação de acesso Olá para operação de saudação. E_ACCESSDENIED é retornado. |
| [System.Fabric.FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException) |Ocorreu um erro de tempo de execução ao executar a operação de saudação. Qualquer um dos métodos de FabricClient Olá potencialmente podem gerar [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException), Olá [ErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException_ErrorCode) propriedade indica a causa exata de exceção Olá Olá. Códigos de erro estão definidos no hello [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode#System_Fabric_FabricErrorCode) enumeração. |
| [System.Fabric.FabricTransientException](https://docs.microsoft.com/dotnet/api/system.fabric.fabrictransientexception#System_Fabric_FabricTransientException) |Falha na operação de saudação devido a condição de erro transitório tooa de algum tipo. Por exemplo, uma operação pode falhar porque um quorum de réplicas está inacessível temporariamente. Exceções transitórias correspondem toofailed operações que podem ser recuperadas. |

Alguns erros [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode#System_Fabric_FabricErrorCode) comuns que podem ser retornados em uma [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException):

| Erro | Condição |
| --- |:--- |
| CommunicationError |Um erro de comunicação provocado Olá operação toofail, Olá nova tentativa. |
| InvalidCredentialType |tipo de credencial de saudação é inválido. |
| InvalidX509FindType |Olá X509FindType é inválido. |
| InvalidX509StoreLocation |Olá X509 repositório local é inválido. |
| InvalidX509StoreName |nome do repositório Olá X509 é inválido. |
| InvalidX509Thumbprint |cadeia de caracteres de impressão digital de certificado X509 de saudação é inválida. |
| InvalidProtectionLevel |nível de proteção de saudação é inválido. |
| InvalidX509Store |repositório de certificados X509 de saudação não pode ser aberto. |
| InvalidSubjectName |nome da entidade Olá é inválido. |
| InvalidAllowedCommonNameList |saudação de formato de cadeia de caracteres de lista Nome comum é inválida. Ele deve ser uma lista separada por vírgulas. |

