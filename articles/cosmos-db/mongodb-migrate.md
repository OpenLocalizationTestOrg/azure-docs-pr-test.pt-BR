---
title: aaaUse mongoimport e mongorestore com hello Azure Cosmos DB API para o MongoDB | Microsoft Docs
description: Saiba como toouse mongoimport e mongorestore tooimport dados tooan API para a conta do MongoDB
keywords: mongoimport, mongorestore
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 352c5fb9-8772-4c5f-87ac-74885e63ecac
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: anhoh
ms.custom: mvc
ms.openlocfilehash: 921354bc7b09a076a73e0cbf5e4aabcc9e83d5a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-import-mongodb-data"></a>Azure Cosmos DB: Importar dados do MongoDB 

dados de toomigrate do MongoDB tooan conta de banco de dados do Azure Cosmos para uso com hello API para o MongoDB, faça o seguinte:

* Baixar um *mongoimport.exe* ou *mongorestore.exe* de saudação [Centro de Download do MongoDB](https://www.mongodb.com/download-center).
* Obter a [cadeia de conexão da API para MongoDB](connect-mongodb-account.md).

Se você estiver importando dados do MongoDB e planejar toouse com hello Azure Cosmos DB, você deve usar o hello [ferramenta de migração de dados](import-data.md) tooimport dados.

Este tutorial aborda Olá tarefas a seguir:

> [!div class="checklist"]
> * Recuperando sua cadeia de conexão
> * Importar dados do MongoDB utilizando mongoimport
> * Importar dados do MongoDB utilizando mongorestore

## <a name="prerequisites"></a>Pré-requisitos

* Aumentar a taxa de transferência: duração Olá a migração de dados depende de quantidade de saudação de configurar para as coleções de taxa de transferência. Ser se tooincrease Olá taxa de transferência para migrações de dados maior. Depois de concluir a migração hello, reduzir os custos de toosave de taxa de transferência de saudação. Para obter mais informações sobre como aumentar a taxa de transferência em Olá [portal do Azure](https://portal.azure.com), consulte [níveis de desempenho e camadas de preços do banco de dados do Azure Cosmos](performance-levels.md).

* Habilitar SSL: o Azure Cosmos DB tem padrões e requisitos de segurança rígidos. Ser tooenable se SSL quando você interagir com sua conta. restante de saudação do artigo Olá Olá procedimentos incluem como tooenable SSL para mongoimport e mongorestore.

## <a name="find-your-connection-string-information-host-port-username-and-password"></a>Localizar informações de cadeia de conexão (host, porta, nome de usuário e senha)

1. Em Olá [portal do Azure](https://portal.azure.com), no painel esquerdo de hello, clique Olá **o banco de dados do Azure Cosmos** entrada.
2. Em Olá **assinaturas** painel, selecione o nome da conta.
3. Em Olá **cadeia de caracteres de Conexão** folha, clique em **cadeia de caracteres de Conexão**.  
Olá direita painel contém todas as informações de saudação que você precisa toosuccessfully conectar tooyour conta.

    ![Folha Cadeia de conexão](./media/mongodb-migrate/ConnectionStringBlade.png)

## <a name="import-data-toohello-api-for-mongodb-by-using-mongoimport"></a>Importar dados toohello API para o MongoDB usando mongoimport

tooimport dados tooyour conta Azure Cosmos DB, use Olá modelo a seguir. Preencha *host*, *username*, e *senha* com valores hello conta tooyour específico.  

Modelo:

    mongoimport.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates --type json --file C:\sample.json

Exemplo:  

    mongoimport.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates --db sampleDB --collection sampleColl --type json --file C:\Users\anhoh\Desktop\*.json

## <a name="import-data-toohello-api-for-mongodb-by-using-mongorestore"></a>Importar dados toohello API para o MongoDB usando mongorestore

toorestore dados tooyour API para a conta do MongoDB, use Olá após a importação do modelo tooexecute hello. Preencha *host*, *username*, e *senha* com valores hello conta tooyour específico.

Modelo:

    mongorestore.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates <path_to_backup>

Exemplo:

    mongorestore.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates ./dumps/dump-2016-12-07
    
## <a name="guide-for-a-successful-migration"></a>Guia para uma migração bem-sucedida

1. Crie previamente e dimensione suas coleções:
        
    * Por padrão, o Azure Cosmos DB prevê uma nova coleção MongoDB com 1.000 unidades de solicitação (RUs). Antes de começar a migração de saudação usando mongoimport, mongorestore ou mongomirror, pré-criar todas as coleções de saudação [portal do Azure](https://portal.azure.com) ou de ferramentas e os drivers do MongoDB. Se sua coleção for maior que 10 GB, verifique se toocreate um [fragmentados/particionada coleção](partition-data.md) com uma chave de fragmentação apropriada.

    * De saudação [portal do Azure](https://portal.azure.com), aumentar a produtividade de suas coleções de 1.000 RUs para uma coleção de partição única e 2.500 RUs para uma coleção fragmentada apenas para migração de saudação. Com a maior taxa de transferência de saudação, você pode evitar a limitação e migrar em menos tempo. Com cobrança por hora no banco de dados do Azure Cosmos, você pode reduzir a taxa de transferência Olá imediatamente após os custos de toosave de migração de saudação.

2. Calcule custos de RU aproximado Olá para gravação de um único documento:

    a. Conecte o banco de dados do Azure Cosmos DB MongoDB tooyour de Olá MongoDB Shell. Você pode encontrar instruções [se conectar a um aplicativo de MongoDB tooAzure Cosmos DB](connect-mongodb-account.md).
    
    b. Execute um comando de inserção de exemplo usando um dos seus documentos de exemplo de hello MongoDB Shell:
    
        ```db.coll.insert({ "playerId": "a067ff", "hashedid": "bb0091", "countryCode": "hk" })```
        
    c. Execute ```db.runCommand({getLastRequestStatistics: 1})``` e uma resposta semelhante à seguinte será exibida:
     
        ```
        globaldb:PRIMARY> db.runCommand({getLastRequestStatistics: 1})
        {
            "_t": "GetRequestStatisticsResponse",
            "ok": 1,
            "CommandName": "insert",
            "RequestCharge": 10,
            "RequestDurationInMilliSeconds": NumberLong(50)
        }
        ```
        
    d. Tome nota da carga de solicitação de saudação.
    
3. Determine a latência de saudação do toohello sua máquina serviço de nuvem do Azure Cosmos DB:
    
    a. Habilite o log detalhado de saudação MongoDB Shell usando este comando:```setVerboseShell(true)```
    
    b. Executar uma consulta simple no banco de dados de saudação: ```db.coll.find().limit(1)```. Uma resposta semelhante à seguinte será exibida:

        ```
        Fetched 1 record(s) in 100(ms)
        ```
        
4. Remova documento hello inserido antes Olá tooensure de migração que não haja nenhum documento duplicado. É possível remover documentos utilizando esse comando: ```db.coll.remove({})```

5. Calcular Olá aproximado *batchSize* e *numInsertionWorkers* valores:

    * Para *batchSize*, divisão Olá total provisionada RUs por RUs Olá consumidos de gravação seu documento único na etapa 3.
    
    * Se Olá calculado *batchSize* < = 24, use esse número como seu *batchSize* valor.
    
    * Se Olá calculado *batchSize* > 24, Olá conjunto *batchSize* too24 de valor.
    
    * Para *numInsertionWorkers*, use esta equação: *numInsertionWorkers =  (taxa de transferência provisionada * latência em segundos) / (tamanho do lote * RUs consumidas para uma gravação única)*.
        
    |Propriedade|Valor|
    |--------|-----|
    |batchSize| 24 |
    |RUs provisionadas | 10000 |
    |Latência | 0,100 s |
    |RU cobrada por 1 doc gravado | 10 RUs |
    |numInsertionWorkers | ? |
    
    *numInsertionWorkers = (10000 RUs x 0,1 s) / (24 x 10 RUs) = 4.1666*

6. Execute o comando de migração final hello:

   ```
   mongoimport.exe --host anhoh-mongodb.documents.azure.com:10255 -u anhoh-mongodb -p wzRJCyjtLPNuhm53yTwaefawuiefhbauwebhfuabweifbiauweb2YVdl2ZFNZNv8IU89LqFVm5U0bw== --ssl --sslAllowInvalidCertificates --jsonArray --db dabasename --collection collectionName --file "C:\sample.json" --numInsertionWorkers 4 --batchSize 24
   ```

## <a name="next-steps"></a>Próximas etapas

Você pode continuar tutorial próxima toohello e aprender como tooquery dados MongoDB usando o banco de dados do Azure Cosmos. 

> [!div class="nextstepaction"]
>[Como tooquery MongoDB dados?](../cosmos-db/tutorial-query-mongodb.md)
