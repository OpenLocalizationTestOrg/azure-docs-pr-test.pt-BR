---
title: "aaaMongoDB cadeia de caracteres de conexão para uma conta de banco de dados do Azure Cosmos | Microsoft Docs"
description: "Saiba como tooconnect tooan de aplicativo o MongoDB Azure Cosmos DB conta usando uma cadeia de caracteres de conexão do MongoDB."
keywords: "cadeia de conexão do mongodb"
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: e36f7375-9329-403b-afd1-4ab49894f75e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: anhoh
ms.openlocfilehash: c0b81cb49a10e09e3f02411b91731c7f980ec47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-mongodb-application-tooazure-cosmos-db"></a>Conecte-se um aplicativo de MongoDB tooAzure Cosmos DB
Saiba como tooconnect tooan de aplicativo o MongoDB Azure Cosmos DB conta usando uma cadeia de caracteres de conexão do MongoDB. Você pode usar um banco de dados do banco de dados do Azure Cosmos como dados saudação armazenar para seu aplicativo do MongoDB. 

Este tutorial fornece informações de cadeia de caracteres de conexão tooretrieve de duas maneiras:

- [Olá rápida iniciar método](#QuickstartConnection), para uso com drivers .NET, Node.js, MongoDB Shell, Java e Python
- [Olá método de cadeia de caracteres de conexão personalizada](#GetCustomConnection), para uso com outros drivers

## <a name="prerequisites"></a>Pré-requisitos

- Uma conta do Azure. Se você ainda não tiver uma, crie agora mesmo uma [conta gratuita do Azure](https://azure.microsoft.com/free/). 
- Uma conta do Azure Cosmos DB. Para obter instruções, consulte [compilar um aplicativo de web do MongoDB API com .NET e Olá portal do Azure](create-mongodb-dotnet.md).

## <a id="QuickstartConnection"></a>Obter cadeia de caracteres de conexão do hello MongoDB usando o início rápido Olá
1. Em um navegador da Internet, entrar toohello [portal do Azure](https://portal.azure.com).
2. Em Olá **o banco de dados do Azure Cosmos** folha, selecione Olá API para a conta do MongoDB. 
3. No painel esquerdo de saudação da folha de conta hello, clique em **início rápido**. 
4. Escolha sua plataforma (**.NET**, **Node.js**, **MongoDB Shell**, **Java**, **Python**). Caso não veja seu driver ou ferramenta na lista, não se preocupe, pois documentamos continuamente mais trechos de código de conexão. Comente abaixo sobre o que você gostaria que toosee. toolearn como toocraft sua conexão, leitura [obter informações de cadeia de caracteres de conexão da conta Olá](#GetCustomConnection).
5. Copie e cole o trecho de código Olá em seu aplicativo do MongoDB.

    ![Folha início rápido](./media/connect-mongodb-account/QuickStartBlade.png)

## <a id="GetCustomConnection"></a>Obter toocustomize de cadeia de caracteres de conexão do hello MongoDB
1. Em um navegador da Internet, entrar toohello [portal do Azure](https://portal.azure.com).
2. Em Olá **o banco de dados do Azure Cosmos** folha, selecione Olá API para a conta do MongoDB. 
3. No painel esquerdo de saudação da folha de conta hello, clique em **cadeia de caracteres de Conexão**. 
4. Olá **cadeia de caracteres de Conexão** folha é aberta. Ele tem todas as contas de toohello Olá informações tooconnect necessário, usando um driver para o MongoDB, incluindo uma cadeia de caracteres de conexão pré-construído.

    ![Folha Cadeia de conexão](./media/connect-mongodb-account/ConnectionStringBlade.png)

## <a name="connection-string-requirements"></a>Requisitos da cadeia de conexão
> [!Important]
> O Azure Cosmos DB tem padrões e requisitos de segurança rígidos. As contas do Azure Cosmos DB exigem autenticação e comunicação segura por *SSL*. 
>
>

Banco de dados do Azure Cosmos dá suporte a saudação MongoDB conexão string URI formato padrão, com alguns requisitos específicos: contas do Azure Cosmos DB exigem autenticação e comunicação segura via SSL. Portanto, o formato de cadeia de caracteres de conexão de saudação é:

    mongodb://username:password@host:port/[database]?ssl=true

os valores da cadeia de caracteres Hello estão disponíveis no hello **cadeia de caracteres de Conexão** folha mostrada anteriormente:

* Nome de usuário (obrigatória): nome da conta do Azure Cosmos DB.
* Senha (obrigatória): senha da conta do Azure Cosmos DB.
* Host (obrigatório): FQDN do hello Azure Cosmos DB conta.
* Porta (obrigatória): 10255.
* Banco de dados (opcional): banco de dados Olá Olá conexão usa. Se nenhum banco de dados for fornecido, o banco de dados do saudação padrão é "teste".
* ssl=true (obrigatório)

Por exemplo, considere conta Olá mostrada no hello **cadeia de caracteres de Conexão** folha. Uma cadeia de conexão válida é:

    mongodb://contoso123:0Fc3IolnL12312asdfawejunASDF@asdfYXX2t8a97kghVcUzcDv98hawelufhawefafnoQRGwNj2nMPL1Y9qsIr9Srdw==@anhohmongo.documents.azure.com:10255/mydatabase?ssl=true

## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[usar MongoChef](mongodb-mongochef.md) com uma API de banco de dados do Azure Cosmos para a conta do MongoDB.
* Explorar hello Azure Cosmos DB API para o MongoDB exibindo [exemplos](mongodb-samples.md).
