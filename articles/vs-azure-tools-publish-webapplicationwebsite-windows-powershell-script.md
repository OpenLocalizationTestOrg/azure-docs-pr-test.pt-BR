---
title: aaaPublish-WebApplicationWebSite (script do Windows PowerShell) | Microsoft Docs
description: "Saiba como toopublish uma web projeto tooan site do Azure. Este script cria recursos Olá necessários em sua assinatura do Azure se não existirem."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 63cfaa2d-f04d-40dc-8677-345385c278d5
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d46904e30e3c2e040e57888fa31543e8e366527f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationwebsite-windows-powershell-script"></a>Publish-WebApplicationWebSite (script do Windows PowerShell)
## <a name="syntax"></a>Sintaxe
Publica um tooan do projeto web site do Azure. script Hello cria recursos Olá necessários em sua assinatura do Azure se não existirem.

    Publish-WebApplicationWebSite
    –Configuration <configuration>
    -SubscriptionName <subscriptionName>
    -WebDeployPackage <packageName>
    -DatabaseServerPassword @{Name = "name"; Password = "password"}
    -SendHostMessagesToOutput
    -Verbose


## <a name="configuration"></a>Configuração
Olá caminho toohello arquivo de configuração JSON que descreve os detalhes de saudação da implantação de saudação.

| Parâmetro | Valor padrão |
| --- | --- |
| Aliases |nenhum |
| Obrigatório? |verdadeiro |
| Position |nomeado |
| Valor padrão |nenhum |
| Aceitar entrada do Pipeline? |false |
| Aceitar caracteres curinga? |false |

## <a name="subscriptionname"></a>SubscriptionName
nome de saudação do hello assinatura do Azure que você quiser que toocreate Olá site no.

| Parâmetro | Valor padrão |
| --- | --- |
| Aliases |nenhum |
| Obrigatório? |false |
| Position |nomeado |
| Valor padrão |nenhum |
| Aceitar entrada do Pipeline? |false |
| Aceitar caracteres curinga? |false |

## <a name="webdeploypackage"></a>WebDeployPackage
Olá caminho toohello web pacote toopublish toohello site de implantação. Você pode criar esse pacote usando o Assistente de publicar Web Olá no Visual Studio. Para obter mais informações, consulte [Introdução aos serviços de nuvem do Azure e ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089).

| Parâmetro | Valor padrão |
| --- | --- |
| Aliases |nenhum |
| Obrigatório? |false |
| Position |nomeado |
| Valor padrão |nenhum |
| Aceitar entrada do Pipeline? |false |
| Aceitar caracteres curinga? |false |

## <a name="databaseserverpassword"></a>DatabaseServerPassword
saudação de nome de usuário e senha Olá banco de dados SQL no Azure.

| Parâmetro | Valor padrão |
| --- | --- |
| Aliases |nenhum |
| Obrigatório? |false |
| Position |nomeado |
| Valor padrão |nenhum |
| Aceitar entrada do Pipeline? |false |
| Aceitar caracteres curinga? |false |

## <a name="sendhostmessagestooutput"></a>SendHostMessagesToOutput
Se true, impressão mensagens de saudação script toohello fluxo de saída.

| Parâmetro | Valor padrão |
| --- | --- |
| Aliases |nenhum |
| Obrigatório? |false |
| Position |nomeado |
| Valor padrão |false |
| Aceitar entrada do Pipeline? |false |
| Aceitar caracteres curinga? |false |

## <a name="remarks"></a>Comentários
Para obter uma explicação completa de como toouse Olá script toocreate desenvolvimento e ambientes de teste, consulte [ambientes de teste e usando Scripts do Windows PowerShell tooPublish tooDev](vs-azure-tools-publishing-using-powershell-scripts.md).

arquivo de configuração JSON Olá Especifica detalhes de saudação do que é toobe implantado. Ela inclui informações de saudação que você especificou quando criou o projeto hello, como nome de saudação e o nome de usuário para o site de saudação. Ele também inclui Olá tooprovision do banco de dados, se houver. saudação de código a seguir mostra um exemplo de arquivo de configuração de JSON:

    {
        "environmentSettings": {
            "webSite": {
                "name": "WebApplication10554",
                "location": "West US"
            },
            "databases": [
                {
                    "connectionStringName": "DefaultConnection",
                    "databaseName": "WebApplication10554_db",
                    "serverName": "iss00brc88",
                    "user": "sqluser2",
                    "password": "",
                    "edition": "",
                    "size": "",
                    "collation": "",
                    "location": "West US"
                }
            ]
        }
    }

Você pode editar o arquivo de configuração do hello JSON toochange o que foi implantado. Uma seção do site é necessária, mas a seção de banco de dados de saudação é opcional.

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações, consulte [WebApplicationVM de publicação (script do Windows PowerShell)](vs-azure-tools-publish-webapplicationvm.md)

