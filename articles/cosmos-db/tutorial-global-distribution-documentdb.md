---
title: "tutorial de distribuição global aaaAzure Cosmos DB para a API DocumentDB | Microsoft Docs"
description: "Saiba como distribuição global usando o banco de dados do Azure Cosmos toosetup Olá API DocumentDB."
services: cosmos-db
keywords: "distribuição global, documentDB"
documentationcenter: 
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: a1d5f01faa62407fbbc9c078ef4a9589a1a29219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosetup-azure-cosmos-db-global-distribution-using-hello-documentdb-api"></a>Como a distribuição global usando o banco de dados do Azure Cosmos toosetup Olá API DocumentDB

Neste artigo, mostramos como toouse Olá toosetup portal do Azure distribuição global do banco de dados do Azure Cosmos e, em seguida, conecte-se usando Olá API DocumentDB.

Este artigo aborda Olá tarefas a seguir: 

> [!div class="checklist"]
> * Configurar a distribuição global usando Olá portal do Azure
> * Configurar a distribuição global usando Olá [APIs do DocumentDB](documentdb-introduction.md)

<a id="portal"></a>
[!INCLUDE [cosmos-db-tutorial-global-distribution-portal](../../includes/cosmos-db-tutorial-global-distribution-portal.md)]


## <a name="connecting-tooa-preferred-region-using-hello-documentdb-api"></a>Conectar-se a região preferida tooa usando Olá API DocumentDB

Em ordem tootake aproveitar [distribuição global](distribute-data-globally.md), aplicativos cliente podem especificar Olá ordenados lista de preferência de regiões toobe usada tooperform operações de documento. Isso pode ser feito definindo a diretiva de conexão hello. Com base na configuração de conta do banco de dados do Azure Cosmos hello, disponibilidade regional atual e a lista de preferência de saudação especificado, Olá ponto de extremidade mais ideal será escolhido por Olá SDK do DocumentDB tooperform gravar e operações de leitura.

Esta lista de preferência é especificada durante a inicialização de uma conexão usando Olá SDKs do DocumentDB. Olá SDKs aceitar um parâmetro opcional "PreferredLocations" que é uma lista ordenada de regiões do Azure.

Olá SDK enviará automaticamente todas as gravações toohello gravação região atual.

Todas as leituras serão enviadas toohello primeira região disponível na lista de PreferredLocations hello. Se Olá solicitação falhar, o cliente Olá falhar para baixo próxima região do hello lista toohello e assim por diante.

Olá SDKs somente tentará tooread de regiões de saudação especificado em PreferredLocations. Assim, por exemplo, se Olá conta de banco de dados está disponível em três regiões, mas somente cliente Olá especifica duas regiões de gravação não Olá para PreferredLocations, em seguida, nenhuma leitura será servida fora da região de gravação hello, mesmo no caso de saudação de failover.

aplicativo Hello pode verificar o ponto de extremidade de gravação atual Olá e ler escolhido pelo Olá SDK pela verificação duas propriedades, WriteEndpoint e ReadEndpoint, disponível no SDK versão 1.8 e acima do ponto de extremidade.

Se Olá PreferredLocations propriedade não for definida, todas as solicitações serão atendidas a partir de região de gravação atual hello.

## <a name="net-sdk"></a>SDK .NET
Olá SDK pode ser usado sem quaisquer alterações de código. Nesse caso, hello SDK automaticamente ambas as leituras e gravações toohello região de gravação atual.

Na versão 1.8 e mais recente do SDK .NET de hello, o parâmetro de ConnectionPolicy Olá para construtor de DocumentClient Olá tem uma propriedade chamada Microsoft.Azure.Documents.ConnectionPolicy.PreferredLocations. Essa propriedade é do tipo `<string>` de Coleção e deve conter uma lista de nomes de região. valores de cadeia de caracteres de saudação são formatados por coluna de nome de região Olá Olá [regiões do Azure] [ regions] página, sem espaços antes ou depois de saudação primeiro e último caractere respectivamente.

pontos de extremidade de leitura e gravação atual Olá estão disponíveis em DocumentClient.WriteEndpoint e DocumentClient.ReadEndpoint respectivamente.

> [!NOTE]
> Olá URLs para pontos de extremidade de saudação não devem ser consideradas como constantes e longa duração. serviço de saudação pode atualizar essas a qualquer momento. Olá SDK manipula essa alteração automaticamente.
>
>

```csharp
// Getting endpoints from application settings or other configuration location
Uri accountEndPoint = new Uri(Properties.Settings.Default.GlobalDatabaseUri);
string accountKey = Properties.Settings.Default.GlobalDatabaseKey;
  
ConnectionPolicy connectionPolicy = new ConnectionPolicy();

//Setting read region selection preference
connectionPolicy.PreferredLocations.Add(LocationNames.WestUS); // first preference
connectionPolicy.PreferredLocations.Add(LocationNames.EastUS); // second preference
connectionPolicy.PreferredLocations.Add(LocationNames.NorthEurope); // third preference

// initialize connection
DocumentClient docClient = new DocumentClient(
    accountEndPoint,
    accountKey,
    connectionPolicy);

// connect tooDocDB
await docClient.OpenAsync().ConfigureAwait(false);
```

## <a name="nodejs-javascript-and-python-sdks"></a>SDKs para NodeJS, JavaScript e Python
Olá SDK pode ser usado sem quaisquer alterações de código. Nesse caso, Olá que SDK direcionará automaticamente os lê e grava toohello região de gravação atual.

Na versão 1.8 e mais tarde de cada SDK, Olá ConnectionPolicy parâmetro para o construtor de DocumentClient Olá uma nova propriedade chamada DocumentClient.ConnectionPolicy.PreferredLocations. Esse parâmetro é uma matriz de cadeias de caracteres que usa uma lista de nomes de região. nomes de saudação são formatados por coluna de nome de região de Olá Olá [regiões do Azure] [ regions] página. Você também pode usar constantes Olá predefinido no objeto de conveniência Olá AzureDocuments.Regions

pontos de extremidade de leitura e gravação atual Olá estão disponíveis em DocumentClient.getWriteEndpoint e DocumentClient.getReadEndpoint respectivamente.

> [!NOTE]
> Olá URLs para pontos de extremidade de saudação não devem ser consideradas como constantes e longa duração. serviço de saudação pode atualizar essas a qualquer momento. Olá SDK tratará essa alteração automaticamente.
>
>

Veja abaixo um exemplo de código para NodeJS/Javascript. Python e Java seguirá Olá mesmo padrão.

```java
// Creating a ConnectionPolicy object
var connectionPolicy = new DocumentBase.ConnectionPolicy();

// Setting read region selection preference, in hello following order -
// 1 - West US
// 2 - East US
// 3 - North Europe
connectionPolicy.PreferredLocations = ['West US', 'East US', 'North Europe'];

// initialize hello connection
var client = new DocumentDBClient(host, { masterKey: masterKey }, connectionPolicy);
```

## <a name="rest"></a>REST
Depois que uma conta de banco de dados tenha sido disponibilizada em várias regiões, os clientes podem consultar sua disponibilidade ao executar uma solicitação GET em Olá URI a seguir.

    https://{databaseaccount}.documents.azure.com/

serviço de saudação retornará uma lista de regiões e seu banco de dados do Azure Cosmos ponto de extremidade correspondente URIs para réplicas de saudação. região de gravação atual Olá será indicado na resposta de saudação. cliente Olá pode selecionar ponto de extremidade apropriado para todas as solicitações da API REST Olá da seguinte maneira.

Exemplo de resposta

    {
        "_dbs": "//dbs/",
        "media": "//media/",
        "writableLocations": [
            {
                "Name": "West US",
                "DatabaseAccountEndpoint": "https://globaldbexample-westus.documents.azure.com:443/"
            }
        ],
        "readableLocations": [
            {
                "Name": "East US",
                "DatabaseAccountEndpoint": "https://globaldbexample-eastus.documents.azure.com:443/"
            }
        ],
        "MaxMediaStorageUsageInMB": 2048,
        "MediaStorageUsageInMB": 0,
        "ConsistencyPolicy": {
            "defaultConsistencyLevel": "Session",
            "maxStalenessPrefix": 100,
            "maxIntervalInSeconds": 5
        },
        "addresses": "//addresses/",
        "id": "globaldbexample",
        "_rid": "globaldbexample.documents.azure.com",
        "_self": "",
        "_ts": 0,
        "_etag": null
    }


* PUT, POST e DELETE todas as solicitações devem ir toohello indicado gravar URI
* Obtém todas as e outras solicitações somente leitura (por exemplo, consultas) podem ir tooany de ponto de extremidade de escolha do cliente Olá

Grave solicitações regiões de somente tooread falhará com o código de erro HTTP 403 ("proibido").

Se a região de gravação da saudação alterações após a fase de descoberta inicial do cliente hello, subsequente grava toohello anterior região de gravação falhará com o código de erro HTTP 403 ("proibido"). cliente Olá deve, em seguida, obter Olá lista de regiões novamente região do tooget Olá gravação atualizado.

Assim, concluímos este tutorial. Você pode aprender como toomanage Olá consistência da sua conta global replicada lendo [níveis de consistência no banco de dados do Azure Cosmos](consistency-levels.md). E para saber mais sobre como a replicação de banco de dados global funciona no Azure Cosmos DB, veja [Distribuir dados globalmente com o Azure Cosmos DB](distribute-data-globally.md).

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você fez a seguir hello:

> [!div class="checklist"]
> * Configurar a distribuição global usando Olá portal do Azure
> * Configurar a distribuição global usando Olá APIs do DocumentDB

Você pode continuar toolearn tutorial do próximo toohello como toodevelop localmente usando Olá emulador local do banco de dados do Azure Cosmos.

> [!div class="nextstepaction"]
> [Desenvolva localmente com o emulador de saudação](local-emulator.md)

[regions]: https://azure.microsoft.com/regions/

