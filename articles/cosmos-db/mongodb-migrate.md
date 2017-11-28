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
# <a name="azure-cosmos-db-import-mongodb-data"></a><span data-ttu-id="b1330-104">Azure Cosmos DB: Importar dados do MongoDB</span><span class="sxs-lookup"><span data-stu-id="b1330-104">Azure Cosmos DB: Import MongoDB data</span></span> 

<span data-ttu-id="b1330-105">dados de toomigrate do MongoDB tooan conta de banco de dados do Azure Cosmos para uso com hello API para o MongoDB, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="b1330-105">toomigrate data from MongoDB tooan Azure Cosmos DB account for use with hello API for MongoDB, you must:</span></span>

* <span data-ttu-id="b1330-106">Baixar um *mongoimport.exe* ou *mongorestore.exe* de saudação [Centro de Download do MongoDB](https://www.mongodb.com/download-center).</span><span class="sxs-lookup"><span data-stu-id="b1330-106">Download either *mongoimport.exe* or *mongorestore.exe* from hello [MongoDB Download Center](https://www.mongodb.com/download-center).</span></span>
* <span data-ttu-id="b1330-107">Obter a [cadeia de conexão da API para MongoDB](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="b1330-107">Get your [API for MongoDB connection string](connect-mongodb-account.md).</span></span>

<span data-ttu-id="b1330-108">Se você estiver importando dados do MongoDB e planejar toouse com hello Azure Cosmos DB, você deve usar o hello [ferramenta de migração de dados](import-data.md) tooimport dados.</span><span class="sxs-lookup"><span data-stu-id="b1330-108">If you are importing data from MongoDB and plan toouse it with hello Azure Cosmos DB, you should use hello [Data Migration tool](import-data.md) tooimport data.</span></span>

<span data-ttu-id="b1330-109">Este tutorial aborda Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b1330-109">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b1330-110">Recuperando sua cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="b1330-110">Retrieving your connection string</span></span>
> * <span data-ttu-id="b1330-111">Importar dados do MongoDB utilizando mongoimport</span><span class="sxs-lookup"><span data-stu-id="b1330-111">Importing MongoDB data by using mongoimport</span></span>
> * <span data-ttu-id="b1330-112">Importar dados do MongoDB utilizando mongorestore</span><span class="sxs-lookup"><span data-stu-id="b1330-112">Importing MongoDB data by using mongorestore</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b1330-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b1330-113">Prerequisites</span></span>

* <span data-ttu-id="b1330-114">Aumentar a taxa de transferência: duração Olá a migração de dados depende de quantidade de saudação de configurar para as coleções de taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="b1330-114">Increase throughput: hello duration of your data migration depends on hello amount of throughput you set up for your collections.</span></span> <span data-ttu-id="b1330-115">Ser se tooincrease Olá taxa de transferência para migrações de dados maior.</span><span class="sxs-lookup"><span data-stu-id="b1330-115">Be sure tooincrease hello throughput for larger data migrations.</span></span> <span data-ttu-id="b1330-116">Depois de concluir a migração hello, reduzir os custos de toosave de taxa de transferência de saudação.</span><span class="sxs-lookup"><span data-stu-id="b1330-116">After you've completed hello migration, decrease hello throughput toosave costs.</span></span> <span data-ttu-id="b1330-117">Para obter mais informações sobre como aumentar a taxa de transferência em Olá [portal do Azure](https://portal.azure.com), consulte [níveis de desempenho e camadas de preços do banco de dados do Azure Cosmos](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="b1330-117">For more information about increasing throughput in hello [Azure portal](https://portal.azure.com), see [Performance levels and pricing tiers in Azure Cosmos DB](performance-levels.md).</span></span>

* <span data-ttu-id="b1330-118">Habilitar SSL: o Azure Cosmos DB tem padrões e requisitos de segurança rígidos.</span><span class="sxs-lookup"><span data-stu-id="b1330-118">Enable SSL: Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="b1330-119">Ser tooenable se SSL quando você interagir com sua conta.</span><span class="sxs-lookup"><span data-stu-id="b1330-119">Be sure tooenable SSL when you interact with your account.</span></span> <span data-ttu-id="b1330-120">restante de saudação do artigo Olá Olá procedimentos incluem como tooenable SSL para mongoimport e mongorestore.</span><span class="sxs-lookup"><span data-stu-id="b1330-120">hello procedures in hello rest of hello article include how tooenable SSL for mongoimport and mongorestore.</span></span>

## <a name="find-your-connection-string-information-host-port-username-and-password"></a><span data-ttu-id="b1330-121">Localizar informações de cadeia de conexão (host, porta, nome de usuário e senha)</span><span class="sxs-lookup"><span data-stu-id="b1330-121">Find your connection string information (host, port, username, and password)</span></span>

1. <span data-ttu-id="b1330-122">Em Olá [portal do Azure](https://portal.azure.com), no painel esquerdo de hello, clique Olá **o banco de dados do Azure Cosmos** entrada.</span><span class="sxs-lookup"><span data-stu-id="b1330-122">In hello [Azure portal](https://portal.azure.com), in hello left pane, click hello **Azure Cosmos DB** entry.</span></span>
2. <span data-ttu-id="b1330-123">Em Olá **assinaturas** painel, selecione o nome da conta.</span><span class="sxs-lookup"><span data-stu-id="b1330-123">In hello **Subscriptions** pane, select your account name.</span></span>
3. <span data-ttu-id="b1330-124">Em Olá **cadeia de caracteres de Conexão** folha, clique em **cadeia de caracteres de Conexão**.</span><span class="sxs-lookup"><span data-stu-id="b1330-124">In hello **Connection String** blade, click **Connection String**.</span></span>  
<span data-ttu-id="b1330-125">Olá direita painel contém todas as informações de saudação que você precisa toosuccessfully conectar tooyour conta.</span><span class="sxs-lookup"><span data-stu-id="b1330-125">hello right pane contains all hello information that you need toosuccessfully connect tooyour account.</span></span>

    ![Folha Cadeia de conexão](./media/mongodb-migrate/ConnectionStringBlade.png)

## <a name="import-data-toohello-api-for-mongodb-by-using-mongoimport"></a><span data-ttu-id="b1330-127">Importar dados toohello API para o MongoDB usando mongoimport</span><span class="sxs-lookup"><span data-stu-id="b1330-127">Import data toohello API for MongoDB by using mongoimport</span></span>

<span data-ttu-id="b1330-128">tooimport dados tooyour conta Azure Cosmos DB, use Olá modelo a seguir.</span><span class="sxs-lookup"><span data-stu-id="b1330-128">tooimport data tooyour Azure Cosmos DB account, use hello following template.</span></span> <span data-ttu-id="b1330-129">Preencha *host*, *username*, e *senha* com valores hello conta tooyour específico.</span><span class="sxs-lookup"><span data-stu-id="b1330-129">Fill in *host*, *username*, and *password* with hello values that are specific tooyour account.</span></span>  

<span data-ttu-id="b1330-130">Modelo:</span><span class="sxs-lookup"><span data-stu-id="b1330-130">Template:</span></span>

    mongoimport.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates --type json --file C:\sample.json

<span data-ttu-id="b1330-131">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="b1330-131">Example:</span></span>  

    mongoimport.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates --db sampleDB --collection sampleColl --type json --file C:\Users\anhoh\Desktop\*.json

## <a name="import-data-toohello-api-for-mongodb-by-using-mongorestore"></a><span data-ttu-id="b1330-132">Importar dados toohello API para o MongoDB usando mongorestore</span><span class="sxs-lookup"><span data-stu-id="b1330-132">Import data toohello API for MongoDB by using mongorestore</span></span>

<span data-ttu-id="b1330-133">toorestore dados tooyour API para a conta do MongoDB, use Olá após a importação do modelo tooexecute hello.</span><span class="sxs-lookup"><span data-stu-id="b1330-133">toorestore data tooyour API for MongoDB account, use hello following template tooexecute hello import.</span></span> <span data-ttu-id="b1330-134">Preencha *host*, *username*, e *senha* com valores hello conta tooyour específico.</span><span class="sxs-lookup"><span data-stu-id="b1330-134">Fill in *host*, *username*, and *password* with hello values that are specific tooyour account.</span></span>

<span data-ttu-id="b1330-135">Modelo:</span><span class="sxs-lookup"><span data-stu-id="b1330-135">Template:</span></span>

    mongorestore.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates <path_to_backup>

<span data-ttu-id="b1330-136">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="b1330-136">Example:</span></span>

    mongorestore.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates ./dumps/dump-2016-12-07
    
## <a name="guide-for-a-successful-migration"></a><span data-ttu-id="b1330-137">Guia para uma migração bem-sucedida</span><span class="sxs-lookup"><span data-stu-id="b1330-137">Guide for a successful migration</span></span>

1. <span data-ttu-id="b1330-138">Crie previamente e dimensione suas coleções:</span><span class="sxs-lookup"><span data-stu-id="b1330-138">Pre-create and scale your collections:</span></span>
        
    * <span data-ttu-id="b1330-139">Por padrão, o Azure Cosmos DB prevê uma nova coleção MongoDB com 1.000 unidades de solicitação (RUs).</span><span class="sxs-lookup"><span data-stu-id="b1330-139">By default, Azure Cosmos DB provisions a new MongoDB collection with 1,000 request units (RUs).</span></span> <span data-ttu-id="b1330-140">Antes de começar a migração de saudação usando mongoimport, mongorestore ou mongomirror, pré-criar todas as coleções de saudação [portal do Azure](https://portal.azure.com) ou de ferramentas e os drivers do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="b1330-140">Before you start hello migration by using mongoimport, mongorestore, or mongomirror, pre-create all your collections from hello [Azure portal](https://portal.azure.com) or from MongoDB drivers and tools.</span></span> <span data-ttu-id="b1330-141">Se sua coleção for maior que 10 GB, verifique se toocreate um [fragmentados/particionada coleção](partition-data.md) com uma chave de fragmentação apropriada.</span><span class="sxs-lookup"><span data-stu-id="b1330-141">If your collection is greater than 10 GB, make sure toocreate a [sharded/partitioned collection](partition-data.md) with an appropriate shard key.</span></span>

    * <span data-ttu-id="b1330-142">De saudação [portal do Azure](https://portal.azure.com), aumentar a produtividade de suas coleções de 1.000 RUs para uma coleção de partição única e 2.500 RUs para uma coleção fragmentada apenas para migração de saudação.</span><span class="sxs-lookup"><span data-stu-id="b1330-142">From hello [Azure portal](https://portal.azure.com), increase your collections' throughput from 1,000 RUs for a single partition collection and 2,500 RUs for a sharded collection just for hello migration.</span></span> <span data-ttu-id="b1330-143">Com a maior taxa de transferência de saudação, você pode evitar a limitação e migrar em menos tempo.</span><span class="sxs-lookup"><span data-stu-id="b1330-143">With hello higher throughput, you can avoid throttling and migrate in less time.</span></span> <span data-ttu-id="b1330-144">Com cobrança por hora no banco de dados do Azure Cosmos, você pode reduzir a taxa de transferência Olá imediatamente após os custos de toosave de migração de saudação.</span><span class="sxs-lookup"><span data-stu-id="b1330-144">With hourly billing in Azure Cosmos DB, you can reduce hello throughput immediately after hello migration toosave costs.</span></span>

2. <span data-ttu-id="b1330-145">Calcule custos de RU aproximado Olá para gravação de um único documento:</span><span class="sxs-lookup"><span data-stu-id="b1330-145">Calculate hello approximate RU charge for a single document write:</span></span>

    <span data-ttu-id="b1330-146">a.</span><span class="sxs-lookup"><span data-stu-id="b1330-146">a.</span></span> <span data-ttu-id="b1330-147">Conecte o banco de dados do Azure Cosmos DB MongoDB tooyour de Olá MongoDB Shell.</span><span class="sxs-lookup"><span data-stu-id="b1330-147">Connect tooyour Azure Cosmos DB MongoDB database from hello MongoDB Shell.</span></span> <span data-ttu-id="b1330-148">Você pode encontrar instruções [se conectar a um aplicativo de MongoDB tooAzure Cosmos DB](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="b1330-148">You can find instructions in [Connect a MongoDB application tooAzure Cosmos DB](connect-mongodb-account.md).</span></span>
    
    <span data-ttu-id="b1330-149">b.</span><span class="sxs-lookup"><span data-stu-id="b1330-149">b.</span></span> <span data-ttu-id="b1330-150">Execute um comando de inserção de exemplo usando um dos seus documentos de exemplo de hello MongoDB Shell:</span><span class="sxs-lookup"><span data-stu-id="b1330-150">Run a sample insert command by using one of your sample documents from hello MongoDB Shell:</span></span>
    
        ```db.coll.insert({ "playerId": "a067ff", "hashedid": "bb0091", "countryCode": "hk" })```
        
    <span data-ttu-id="b1330-151">c.</span><span class="sxs-lookup"><span data-stu-id="b1330-151">c.</span></span> <span data-ttu-id="b1330-152">Execute ```db.runCommand({getLastRequestStatistics: 1})``` e uma resposta semelhante à seguinte será exibida:</span><span class="sxs-lookup"><span data-stu-id="b1330-152">Run ```db.runCommand({getLastRequestStatistics: 1})``` and you will receive a response like this one:</span></span>
     
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
        
    <span data-ttu-id="b1330-153">d.</span><span class="sxs-lookup"><span data-stu-id="b1330-153">d.</span></span> <span data-ttu-id="b1330-154">Tome nota da carga de solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b1330-154">Take note of hello request charge.</span></span>
    
3. <span data-ttu-id="b1330-155">Determine a latência de saudação do toohello sua máquina serviço de nuvem do Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="b1330-155">Determine hello latency from your machine toohello Azure Cosmos DB cloud service:</span></span>
    
    <span data-ttu-id="b1330-156">a.</span><span class="sxs-lookup"><span data-stu-id="b1330-156">a.</span></span> <span data-ttu-id="b1330-157">Habilite o log detalhado de saudação MongoDB Shell usando este comando:```setVerboseShell(true)```</span><span class="sxs-lookup"><span data-stu-id="b1330-157">Enable verbose logging from hello MongoDB Shell by using this command: ```setVerboseShell(true)```</span></span>
    
    <span data-ttu-id="b1330-158">b.</span><span class="sxs-lookup"><span data-stu-id="b1330-158">b.</span></span> <span data-ttu-id="b1330-159">Executar uma consulta simple no banco de dados de saudação: ```db.coll.find().limit(1)```.</span><span class="sxs-lookup"><span data-stu-id="b1330-159">Run a simple query against hello database: ```db.coll.find().limit(1)```.</span></span> <span data-ttu-id="b1330-160">Uma resposta semelhante à seguinte será exibida:</span><span class="sxs-lookup"><span data-stu-id="b1330-160">You will receive a response like this one:</span></span>

        ```
        Fetched 1 record(s) in 100(ms)
        ```
        
4. <span data-ttu-id="b1330-161">Remova documento hello inserido antes Olá tooensure de migração que não haja nenhum documento duplicado.</span><span class="sxs-lookup"><span data-stu-id="b1330-161">Remove hello inserted document before hello migration tooensure that there are no duplicate documents.</span></span> <span data-ttu-id="b1330-162">É possível remover documentos utilizando esse comando: ```db.coll.remove({})```</span><span class="sxs-lookup"><span data-stu-id="b1330-162">You can remove documents by using this command: ```db.coll.remove({})```</span></span>

5. <span data-ttu-id="b1330-163">Calcular Olá aproximado *batchSize* e *numInsertionWorkers* valores:</span><span class="sxs-lookup"><span data-stu-id="b1330-163">Calculate hello approximate *batchSize* and *numInsertionWorkers* values:</span></span>

    * <span data-ttu-id="b1330-164">Para *batchSize*, divisão Olá total provisionada RUs por RUs Olá consumidos de gravação seu documento único na etapa 3.</span><span class="sxs-lookup"><span data-stu-id="b1330-164">For *batchSize*, divide hello total provisioned RUs by hello RUs consumed from your single document write in step 3.</span></span>
    
    * <span data-ttu-id="b1330-165">Se Olá calculado *batchSize* < = 24, use esse número como seu *batchSize* valor.</span><span class="sxs-lookup"><span data-stu-id="b1330-165">If hello calculated *batchSize* <= 24, use that number as your *batchSize* value.</span></span>
    
    * <span data-ttu-id="b1330-166">Se Olá calculado *batchSize* > 24, Olá conjunto *batchSize* too24 de valor.</span><span class="sxs-lookup"><span data-stu-id="b1330-166">If hello calculated *batchSize* > 24, set hello *batchSize* value too24.</span></span>
    
    * <span data-ttu-id="b1330-167">Para *numInsertionWorkers*, use esta equação: *numInsertionWorkers =  (taxa de transferência provisionada * latência em segundos) / (tamanho do lote * RUs consumidas para uma gravação única)*.</span><span class="sxs-lookup"><span data-stu-id="b1330-167">For *numInsertionWorkers*, use this equation:   *numInsertionWorkers =  (provisioned throughput * latency in seconds) / (batch size * consumed RUs for a single write)*.</span></span>
        
    |<span data-ttu-id="b1330-168">Propriedade</span><span class="sxs-lookup"><span data-stu-id="b1330-168">Property</span></span>|<span data-ttu-id="b1330-169">Valor</span><span class="sxs-lookup"><span data-stu-id="b1330-169">Value</span></span>|
    |--------|-----|
    |<span data-ttu-id="b1330-170">batchSize</span><span class="sxs-lookup"><span data-stu-id="b1330-170">batchSize</span></span>| <span data-ttu-id="b1330-171">24</span><span class="sxs-lookup"><span data-stu-id="b1330-171">24</span></span> |
    |<span data-ttu-id="b1330-172">RUs provisionadas</span><span class="sxs-lookup"><span data-stu-id="b1330-172">RUs provisioned</span></span> | <span data-ttu-id="b1330-173">10000</span><span class="sxs-lookup"><span data-stu-id="b1330-173">10000</span></span> |
    |<span data-ttu-id="b1330-174">Latência</span><span class="sxs-lookup"><span data-stu-id="b1330-174">Latency</span></span> | <span data-ttu-id="b1330-175">0,100 s</span><span class="sxs-lookup"><span data-stu-id="b1330-175">0.100 s</span></span> |
    |<span data-ttu-id="b1330-176">RU cobrada por 1 doc gravado</span><span class="sxs-lookup"><span data-stu-id="b1330-176">RU charged for 1 doc write</span></span> | <span data-ttu-id="b1330-177">10 RUs</span><span class="sxs-lookup"><span data-stu-id="b1330-177">10 RUs</span></span> |
    |<span data-ttu-id="b1330-178">numInsertionWorkers</span><span class="sxs-lookup"><span data-stu-id="b1330-178">numInsertionWorkers</span></span> | <span data-ttu-id="b1330-179">?</span><span class="sxs-lookup"><span data-stu-id="b1330-179">?</span></span> |
    
    <span data-ttu-id="b1330-180">*numInsertionWorkers = (10000 RUs x 0,1 s) / (24 x 10 RUs) = 4.1666*</span><span class="sxs-lookup"><span data-stu-id="b1330-180">*numInsertionWorkers = (10000 RUs x 0.1 s) / (24 x 10 RUs) = 4.1666*</span></span>

6. <span data-ttu-id="b1330-181">Execute o comando de migração final hello:</span><span class="sxs-lookup"><span data-stu-id="b1330-181">Run hello final migration command:</span></span>

   ```
   mongoimport.exe --host anhoh-mongodb.documents.azure.com:10255 -u anhoh-mongodb -p wzRJCyjtLPNuhm53yTwaefawuiefhbauwebhfuabweifbiauweb2YVdl2ZFNZNv8IU89LqFVm5U0bw== --ssl --sslAllowInvalidCertificates --jsonArray --db dabasename --collection collectionName --file "C:\sample.json" --numInsertionWorkers 4 --batchSize 24
   ```

## <a name="next-steps"></a><span data-ttu-id="b1330-182">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b1330-182">Next steps</span></span>

<span data-ttu-id="b1330-183">Você pode continuar tutorial próxima toohello e aprender como tooquery dados MongoDB usando o banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="b1330-183">You can proceed toohello next tutorial and learn how tooquery MongoDB data by using Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="b1330-184">Como tooquery MongoDB dados?</span><span class="sxs-lookup"><span data-stu-id="b1330-184">How tooquery MongoDB data?</span></span>](../cosmos-db/tutorial-query-mongodb.md)
