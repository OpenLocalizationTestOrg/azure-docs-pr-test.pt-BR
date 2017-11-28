---
title: 'Tutorial do Azure Cosmos DB: criar, consultar e percorrer o console do Apache TinkerPops Gremlin | Microsoft Docs'
description: "Um toocreates de início rápido do banco de dados do Azure Cosmos vértices, bordas e consultas usando hello Azure Cosmos DB Graph API."
services: cosmos-db
author: dennyglee
manager: jhubbard
editor: monicar
ms.assetid: bf08e031-718a-4a2a-89d6-91e12ff8797d
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: terminal
ms.topic: hero-article
ms.date: 07/27/2017
ms.author: denlee
ms.openlocfilehash: 9de64c97fec89c45cecba9e14214db472ec76f57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-query-and-traverse-a-graph-in-hello-gremlin-console"></a><span data-ttu-id="cb566-103">Cosmos do Azure DB: Criar, consultar e percorrer um gráfico no console de Gremlin Olá</span><span class="sxs-lookup"><span data-stu-id="cb566-103">Azure Cosmos DB: Create, query, and traverse a graph in hello Gremlin console</span></span>

<span data-ttu-id="cb566-104">O BD Cosmos do Azure é o serviço multimodelo de banco de dados distribuído globalmente da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cb566-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="cb566-105">Você pode criar e consultar documentos, chave/valor e bancos de dados do gráfico, que se beneficiar de distribuição global hello e recursos de escala horizontal no núcleo de saudação do banco de dados do Azure Cosmos rapidamente.</span><span class="sxs-lookup"><span data-stu-id="cb566-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="cb566-106">Este guia rápido demonstra como toocreate uma conta de banco de dados do Azure Cosmos, o banco de dados e o uso de gráfico (contêiner) Olá portal do Azure e, em seguida, use Olá [Gremlin Console](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console) de [TinkerPop Apache](http://tinkerpop.apache.org) toowork com Dados de API (visualização) do gráfico.</span><span class="sxs-lookup"><span data-stu-id="cb566-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, database, and graph (container) using hello Azure portal and then use hello [Gremlin Console](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console) from  [Apache TinkerPop](http://tinkerpop.apache.org) toowork with Graph API (preview) data.</span></span> <span data-ttu-id="cb566-107">Neste tutorial, você cria e consulta vértices e bordas, atualizando uma propriedade de vértice, vértices de consulta, percorra o gráfico de saudação e descartar um vértice.</span><span class="sxs-lookup"><span data-stu-id="cb566-107">In this tutorial, you create and query vertices and edges, updating a vertex property, query vertices, traverse hello graph, and drop a vertex.</span></span>

![Azure DB Cosmos do console do Apache Gremlin Olá](./media/create-graph-gremlin-console/gremlin-console.png)

<span data-ttu-id="cb566-109">console de Gremlin Olá é Groovy/Java com base e executa no Linux, Mac e Windows.</span><span class="sxs-lookup"><span data-stu-id="cb566-109">hello Gremlin console is Groovy/Java based and runs on Linux, Mac, and Windows.</span></span> <span data-ttu-id="cb566-110">Você pode baixá-lo do hello [TinkerPop Apache site](https://www.apache.org/dyn/closer.lua/tinkerpop/3.2.5/apache-tinkerpop-gremlin-console-3.2.5-bin.zip).</span><span class="sxs-lookup"><span data-stu-id="cb566-110">You can download it from hello [Apache TinkerPop site](https://www.apache.org/dyn/closer.lua/tinkerpop/3.2.5/apache-tinkerpop-gremlin-console-3.2.5-bin.zip).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb566-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cb566-111">Prerequisites</span></span>

<span data-ttu-id="cb566-112">Você precisa toohave toocreate uma assinatura do Azure uma conta de banco de dados do Azure Cosmos para este guia de início rápido.</span><span class="sxs-lookup"><span data-stu-id="cb566-112">You need toohave an Azure subscription toocreate an Azure Cosmos DB account for this quickstart.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<span data-ttu-id="cb566-113">Você também precisa tooinstall Olá [Gremlin Console](http://tinkerpop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="cb566-113">You also need tooinstall hello [Gremlin Console](http://tinkerpop.apache.org/).</span></span> <span data-ttu-id="cb566-114">Use a versão 3.2.5 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="cb566-114">Use version 3.2.5 or above.</span></span>

## <a name="create-a-database-account"></a><span data-ttu-id="cb566-115">Criar uma conta de banco de dados</span><span class="sxs-lookup"><span data-stu-id="cb566-115">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="cb566-116">Adicionar um gráfico</span><span class="sxs-lookup"><span data-stu-id="cb566-116">Add a graph</span></span>

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <span data-ttu-id="cb566-117"><a id="ConnectAppService"></a>Conecte-se o serviço de aplicativo tooyour</span><span class="sxs-lookup"><span data-stu-id="cb566-117"><a id="ConnectAppService"></a>Connect tooyour app service</span></span>
1. <span data-ttu-id="cb566-118">Antes de iniciar Olá Gremlin Console, criar ou modificar Olá remoto secure.yaml arquivo no diretório de apache-tinkerpop-gremlin-console-3.2.5/conf Olá.</span><span class="sxs-lookup"><span data-stu-id="cb566-118">Before starting hello Gremlin Console, create or modify hello remote-secure.yaml configuration file in hello apache-tinkerpop-gremlin-console-3.2.5/conf directory.</span></span>
2. <span data-ttu-id="cb566-119">Preencha as configurações de *host*, *porta*, *nome de usuário*, *senha*, *connectionPool* e *serializador*:</span><span class="sxs-lookup"><span data-stu-id="cb566-119">Fill in your *host*, *port*, *username*, *password*, *connectionPool*, and *serializer* configurations:</span></span>

    <span data-ttu-id="cb566-120">Configuração</span><span class="sxs-lookup"><span data-stu-id="cb566-120">Setting</span></span>|<span data-ttu-id="cb566-121">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="cb566-121">Suggested value</span></span>|<span data-ttu-id="cb566-122">Descrição</span><span class="sxs-lookup"><span data-stu-id="cb566-122">Description</span></span>
    ---|---|---
    <span data-ttu-id="cb566-123">hosts</span><span class="sxs-lookup"><span data-stu-id="cb566-123">hosts</span></span>|<span data-ttu-id="cb566-124">[***.graphs.azure.com]</span><span class="sxs-lookup"><span data-stu-id="cb566-124">[***.graphs.azure.com]</span></span>|<span data-ttu-id="cb566-125">Confira a captura de tela abaixo.</span><span class="sxs-lookup"><span data-stu-id="cb566-125">See screenshot below.</span></span> <span data-ttu-id="cb566-126">O valor de URI Gremlin Olá na página de visão geral de saudação do hello portal do Azure, entre colchetes, com hello à direita é: 443 / removido.</span><span class="sxs-lookup"><span data-stu-id="cb566-126">This is hello Gremlin URI value on hello Overview page of hello Azure portal, in square brackets, with hello trailing :443/ removed.</span></span><br><br><span data-ttu-id="cb566-127">Esse valor também pode ser recuperado do guia de chaves hello, usando o valor URI Olá removendo https://, alterando toographs documentos e remoção de saudação à direita: 443 /.</span><span class="sxs-lookup"><span data-stu-id="cb566-127">This value can also be retrieved from hello Keys tab, using hello URI value by removing https://, changing documents toographs, and removing hello trailing :443/.</span></span>
    <span data-ttu-id="cb566-128">porta</span><span class="sxs-lookup"><span data-stu-id="cb566-128">port</span></span>|<span data-ttu-id="cb566-129">443</span><span class="sxs-lookup"><span data-stu-id="cb566-129">443</span></span>|<span data-ttu-id="cb566-130">Definir too443.</span><span class="sxs-lookup"><span data-stu-id="cb566-130">Set too443.</span></span>
    <span data-ttu-id="cb566-131">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="cb566-131">username</span></span>|<span data-ttu-id="cb566-132">*Seu nome de usuário*</span><span class="sxs-lookup"><span data-stu-id="cb566-132">*Your username*</span></span>|<span data-ttu-id="cb566-133">Olá recursos do formulário de saudação `/dbs/<db>/colls/<coll>` onde `<db>` é o nome do banco de dados e `<coll>` é o nome da coleção.</span><span class="sxs-lookup"><span data-stu-id="cb566-133">hello resource of hello form `/dbs/<db>/colls/<coll>` where `<db>` is your database name and `<coll>` is your collection name.</span></span>
    <span data-ttu-id="cb566-134">Senha</span><span class="sxs-lookup"><span data-stu-id="cb566-134">password</span></span>|<span data-ttu-id="cb566-135">*Sua chave primária*</span><span class="sxs-lookup"><span data-stu-id="cb566-135">*Your primary key*</span></span>| <span data-ttu-id="cb566-136">Confira a segunda captura de tela abaixo.</span><span class="sxs-lookup"><span data-stu-id="cb566-136">See second screenshot below.</span></span> <span data-ttu-id="cb566-137">Isso é sua chave primária, você pode recuperar da página de chaves de saudação do hello portal do Azure, na caixa de chave primária de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb566-137">This is your primary key, which you can retrieve from hello Keys page of hello Azure portal, in hello Primary Key box.</span></span> <span data-ttu-id="cb566-138">Use o botão de cópia de saudação no lado esquerdo de saudação do valor de Olá Olá caixa toocopy.</span><span class="sxs-lookup"><span data-stu-id="cb566-138">Use hello copy button on hello left side of hello box toocopy hello value.</span></span>
    <span data-ttu-id="cb566-139">connectionPool</span><span class="sxs-lookup"><span data-stu-id="cb566-139">connectionPool</span></span>|<span data-ttu-id="cb566-140">{enableSsl: true}</span><span class="sxs-lookup"><span data-stu-id="cb566-140">{enableSsl: true}</span></span>|<span data-ttu-id="cb566-141">Sua configuração do pool de conexão para SSL.</span><span class="sxs-lookup"><span data-stu-id="cb566-141">Your connection pool setting for SSL.</span></span>
    <span data-ttu-id="cb566-142">serializador</span><span class="sxs-lookup"><span data-stu-id="cb566-142">serializer</span></span>|<span data-ttu-id="cb566-143">{ className: org.apache.tinkerpop.gremlin.</span><span class="sxs-lookup"><span data-stu-id="cb566-143">{ className: org.apache.tinkerpop.gremlin.</span></span><br><span data-ttu-id="cb566-144">driver.ser.GraphSONMessageSerializerV1d0,</span><span class="sxs-lookup"><span data-stu-id="cb566-144">driver.ser.GraphSONMessageSerializerV1d0,</span></span><br> <span data-ttu-id="cb566-145">config: { serializeResultToString: true }}</span><span class="sxs-lookup"><span data-stu-id="cb566-145">config: { serializeResultToString: true }}</span></span>|<span data-ttu-id="cb566-146">Defina o valor de toothis e excluir qualquer `\n` quebras de linha ao colar no valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb566-146">Set toothis value and delete any `\n` line breaks when pasting in hello value.</span></span>

    <span data-ttu-id="cb566-147">Valor de hosts hello, copie Olá **Gremlin URI** valor da saudação **visão geral** página: ![exibir e copiar valor de URI Gremlin Olá página de visão geral de saudação do hello portal do Azure](./media/create-graph-gremlin-console/gremlin-uri.png)</span><span class="sxs-lookup"><span data-stu-id="cb566-147">For hello hosts value, copy hello **Gremlin URI** value from hello **Overview** page: ![View and copy hello Gremlin URI value on hello Overview page in hello Azure portal](./media/create-graph-gremlin-console/gremlin-uri.png)</span></span>

    <span data-ttu-id="cb566-148">Para o valor da senha hello, copie Olá **chave primária** de saudação **chaves** página: ![exibir e copiar a chave primária na Olá portal do Azure, chaves de página](./media/create-graph-gremlin-console/keys.png)</span><span class="sxs-lookup"><span data-stu-id="cb566-148">For hello password value, copy hello **Primary key** from hello **Keys** page: ![View and copy your primary key in hello Azure portal, Keys page](./media/create-graph-gremlin-console/keys.png)</span></span>


3. <span data-ttu-id="cb566-149">Em seu terminal, execute `bin/gremlin.bat` ou `bin/gremlin.sh` toostart Olá [Gremlin Console](http://tinkerpop.apache.org/docs/3.2.5/tutorials/getting-started/).</span><span class="sxs-lookup"><span data-stu-id="cb566-149">In your terminal, run `bin/gremlin.bat` or `bin/gremlin.sh` toostart hello [Gremlin Console](http://tinkerpop.apache.org/docs/3.2.5/tutorials/getting-started/).</span></span>
4. <span data-ttu-id="cb566-150">Em seu terminal, execute `:remote connect tinkerpop.server conf/remote-secure.yaml` tooconnect tooyour do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cb566-150">In your terminal, run `:remote connect tinkerpop.server conf/remote-secure.yaml` tooconnect tooyour app service.</span></span>

    > [!TIP]
    > <span data-ttu-id="cb566-151">Se você receber o erro Olá `No appenders could be found for logger` Certifique-se de que você atualizou o valor de serializador Olá no arquivo de secure.yaml remoto Olá conforme descrito na etapa 2.</span><span class="sxs-lookup"><span data-stu-id="cb566-151">If you receive hello error `No appenders could be found for logger` ensure that you updated hello serializer value in hello remote-secure.yaml file as described in step 2.</span></span> 

<span data-ttu-id="cb566-152">Ótimo!</span><span class="sxs-lookup"><span data-stu-id="cb566-152">Great!</span></span> <span data-ttu-id="cb566-153">Concluída a instalação Olá, vamos começar a executar alguns comandos do console.</span><span class="sxs-lookup"><span data-stu-id="cb566-153">Now that we finished hello setup, let's start running some console commands.</span></span>

<span data-ttu-id="cb566-154">Vamos tentar um comando count() simples.</span><span class="sxs-lookup"><span data-stu-id="cb566-154">Let's try a simple count() command.</span></span> <span data-ttu-id="cb566-155">Digite o seguinte de saudação em console Olá no prompt de saudação:</span><span class="sxs-lookup"><span data-stu-id="cb566-155">Type hello following into hello console at hello prompt:</span></span>
```
:> g.V().count()
```

> [!TIP]
> <span data-ttu-id="cb566-156">Saudação de aviso `:>` que precede Olá `g.V().count()` texto?</span><span class="sxs-lookup"><span data-stu-id="cb566-156">Notice hello `:>` that precedes hello `g.V().count()` text?</span></span> 
>
> <span data-ttu-id="cb566-157">Isso faz parte do comando Olá que necessário tootype.</span><span class="sxs-lookup"><span data-stu-id="cb566-157">This is part of hello command you need tootype.</span></span> <span data-ttu-id="cb566-158">É importante ao usar o console de Gremlin hello, com o banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="cb566-158">It is important when using hello Gremlin console, with Azure Cosmos DB.</span></span>  
>
> <span data-ttu-id="cb566-159">Omitir isso `:>` prefixo instrui o comando de saudação do hello console tooexecute localmente, geralmente em relação a um gráfico de memória.</span><span class="sxs-lookup"><span data-stu-id="cb566-159">Omitting this `:>` prefix instructs hello console tooexecute hello command locally, often against an in-memory graph.</span></span>
> <span data-ttu-id="cb566-160">Usando esse `:>` informa Olá console tooexecute um comando remoto, nesse caso contra Cosmos DB (o emulador de localhost hello, ou um > instância do Azure).</span><span class="sxs-lookup"><span data-stu-id="cb566-160">Using this `:>` tells hello console tooexecute a remote command, in this case against Cosmos DB (either hello localhost emulator, or an > Azure instance).</span></span>


## <a name="create-vertices-and-edges"></a><span data-ttu-id="cb566-161">Criar vértices e bordas</span><span class="sxs-lookup"><span data-stu-id="cb566-161">Create vertices and edges</span></span>

<span data-ttu-id="cb566-162">Vamos começar pela adição de quatro vértices pessoais para *Paulo*, *Maria Eduarda*, *Valentina*, *Pedro* e *Davi*.</span><span class="sxs-lookup"><span data-stu-id="cb566-162">Let's begin by adding five person vertices for *Thomas*, *Mary Kay*, *Robin*, *Ben*, and *Jack*.</span></span>

<span data-ttu-id="cb566-163">Entrada (Thomas):</span><span class="sxs-lookup"><span data-stu-id="cb566-163">Input (Thomas):</span></span>

```
:> g.addV('person').property('firstName', 'Thomas').property('lastName', 'Andersen').property('age', 44).property('userid', 1)
```

<span data-ttu-id="cb566-164">Saída:</span><span class="sxs-lookup"><span data-stu-id="cb566-164">Output:</span></span>

```
==>[id:796cdccc-2acd-4e58-a324-91d6f6f5ed6d,label:person,type:vertex,properties:[firstName:[[id:f02a749f-b67c-4016-850e-910242d68953,value:Thomas]],lastName:[[id:f5fa3126-8818-4fda-88b0-9bb55145ce5c,value:Andersen]],age:[[id:f6390f9c-e563-433e-acbf-25627628016e,value:44]],userid:[[id:796cdccc-2acd-4e58-a324-91d6f6f5ed6d|userid,value:1]]]]
```
<span data-ttu-id="cb566-165">Entrada (Mary Kay):</span><span class="sxs-lookup"><span data-stu-id="cb566-165">Input (Mary Kay):</span></span>

```
:> g.addV('person').property('firstName', 'Mary Kay').property('lastName', 'Andersen').property('age', 39).property('userid', 2)

```

<span data-ttu-id="cb566-166">Saída:</span><span class="sxs-lookup"><span data-stu-id="cb566-166">Output:</span></span>

```
==>[id:0ac9be25-a476-4a30-8da8-e79f0119ea5e,label:person,type:vertex,properties:[firstName:[[id:ea0604f8-14ee-4513-a48a-1734a1f28dc0,value:Mary Kay]],lastName:[[id:86d3bba5-fd60-4856-9396-c195ef7d7f4b,value:Andersen]],age:[[id:bc81b78d-30c4-4e03-8f40-50f72eb5f6da,value:39]],userid:[[id:0ac9be25-a476-4a30-8da8-e79f0119ea5e|userid,value:2]]]]

```

<span data-ttu-id="cb566-167">Entrada (Robin):</span><span class="sxs-lookup"><span data-stu-id="cb566-167">Input (Robin):</span></span>

```
:> g.addV('person').property('firstName', 'Robin').property('lastName', 'Wakefield').property('userid', 3)
```

<span data-ttu-id="cb566-168">Saída:</span><span class="sxs-lookup"><span data-stu-id="cb566-168">Output:</span></span>

```
==>[id:8dc14d6a-8683-4a54-8d74-7eef1fb43a3e,label:person,type:vertex,properties:[firstName:[[id:ec65f078-7a43-4cbe-bc06-e50f2640dc4e,value:Robin]],lastName:[[id:a3937d07-0e88-45d3-a442-26fcdfb042ce,value:Wakefield]],userid:[[id:8dc14d6a-8683-4a54-8d74-7eef1fb43a3e|userid,value:3]]]]
```

<span data-ttu-id="cb566-169">Entrada (Ben):</span><span class="sxs-lookup"><span data-stu-id="cb566-169">Input (Ben):</span></span>

```
:> g.addV('person').property('firstName', 'Ben').property('lastName', 'Miller').property('userid', 4)

```

<span data-ttu-id="cb566-170">Saída:</span><span class="sxs-lookup"><span data-stu-id="cb566-170">Output:</span></span>

```
==>[id:ee86b670-4d24-4966-9a39-30529284b66f,label:person,type:vertex,properties:[firstName:[[id:a632469b-30fc-4157-840c-b80260871e9a,value:Ben]],lastName:[[id:4a08d307-0719-47c6-84ae-1b0b06630928,value:Miller]],userid:[[id:ee86b670-4d24-4966-9a39-30529284b66f|userid,value:4]]]]
```

<span data-ttu-id="cb566-171">Entrada (tomada):</span><span class="sxs-lookup"><span data-stu-id="cb566-171">Input (Jack):</span></span>

```
:> g.addV('person').property('firstName', 'Jack').property('lastName', 'Connor').property('userid', 5)
```

<span data-ttu-id="cb566-172">Saída:</span><span class="sxs-lookup"><span data-stu-id="cb566-172">Output:</span></span>

```
==>[id:4c835f2a-ea5b-43bb-9b6b-215488ad8469,label:person,type:vertex,properties:[firstName:[[id:4250824e-4b72-417f-af98-8034aa15559f,value:Jack]],lastName:[[id:44c1d5e1-a831-480a-bf94-5167d133549e,value:Connor]],userid:[[id:4c835f2a-ea5b-43bb-9b6b-215488ad8469|userid,value:5]]]]
```


<span data-ttu-id="cb566-173">Em seguida, vamos adicionar bordas para relações entre as pessoas.</span><span class="sxs-lookup"><span data-stu-id="cb566-173">Next, let's add edges for relationships between our people.</span></span>

<span data-ttu-id="cb566-174">Entrada (Thomas -> Mary Kay):</span><span class="sxs-lookup"><span data-stu-id="cb566-174">Input (Thomas -> Mary Kay):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Mary Kay'))
```

<span data-ttu-id="cb566-175">Saída:</span><span class="sxs-lookup"><span data-stu-id="cb566-175">Output:</span></span>

```
==>[id:c12bf9fb-96a1-4cb7-a3f8-431e196e702f,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:0d1fa428-780c-49a5-bd3a-a68d96391d5c,outV:1ce821c6-aa3d-4170-a0b7-d14d2a4d18c3]
```

<span data-ttu-id="cb566-176">Entrada (Thomas -> Robin):</span><span class="sxs-lookup"><span data-stu-id="cb566-176">Input (Thomas -> Robin):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Robin'))
```

<span data-ttu-id="cb566-177">Saída:</span><span class="sxs-lookup"><span data-stu-id="cb566-177">Output:</span></span>

```
==>[id:58319bdd-1d3e-4f17-a106-0ddf18719d15,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:3e324073-ccfc-4ae1-8675-d450858ca116,outV:1ce821c6-aa3d-4170-a0b7-d14d2a4d18c3]
```

<span data-ttu-id="cb566-178">Entrada (Robin -> Ben):</span><span class="sxs-lookup"><span data-stu-id="cb566-178">Input (Robin -> Ben):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Robin').addE('knows').to(g.V().hasLabel('person').has('firstName', 'Ben'))
```

<span data-ttu-id="cb566-179">Saída:</span><span class="sxs-lookup"><span data-stu-id="cb566-179">Output:</span></span>

```
==>[id:889c4d3c-549e-4d35-bc21-a3d1bfa11e00,label:knows,type:edge,inVLabel:person,outVLabel:person,inV:40fd641d-546e-412a-abcc-58fe53891aab,outV:3e324073-ccfc-4ae1-8675-d450858ca116]
```

## <a name="update-a-vertex"></a><span data-ttu-id="cb566-180">Atualizar um vértice</span><span class="sxs-lookup"><span data-stu-id="cb566-180">Update a vertex</span></span>

<span data-ttu-id="cb566-181">Vamos atualizar Olá *Thomas* vértice com uma nova era *45*.</span><span class="sxs-lookup"><span data-stu-id="cb566-181">Let's update hello *Thomas* vertex with a new age of *45*.</span></span>

<span data-ttu-id="cb566-182">Entrada:</span><span class="sxs-lookup"><span data-stu-id="cb566-182">Input:</span></span>
```
:> g.V().hasLabel('person').has('firstName', 'Thomas').property('age', 45)
```
<span data-ttu-id="cb566-183">Saída:</span><span class="sxs-lookup"><span data-stu-id="cb566-183">Output:</span></span>

```
==>[id:ae36f938-210e-445a-92df-519f2b64c8ec,label:person,type:vertex,properties:[firstName:[[id:872090b6-6a77-456a-9a55-a59141d4ebc2,value:Thomas]],lastName:[[id:7ee7a39a-a414-4127-89b4-870bc4ef99f3,value:Andersen]],age:[[id:a2a75d5a-ae70-4095-806d-a35abcbfe71d,value:45]]]]
```

## <a name="query-your-graph"></a><span data-ttu-id="cb566-184">Consultar o gráfico</span><span class="sxs-lookup"><span data-stu-id="cb566-184">Query your graph</span></span>

<span data-ttu-id="cb566-185">Agora, vamos executar uma variedade de consultas em relação ao gráfico.</span><span class="sxs-lookup"><span data-stu-id="cb566-185">Now, let's run a variety of queries against your graph.</span></span>

<span data-ttu-id="cb566-186">Primeiro, vamos tentar uma consulta com uma filtro tooreturn somente as pessoas que mais de 40 anos de idade.</span><span class="sxs-lookup"><span data-stu-id="cb566-186">First, let's try a query with a filter tooreturn only people who are older than 40 years old.</span></span>

<span data-ttu-id="cb566-187">Entrada (consulta de filtro):</span><span class="sxs-lookup"><span data-stu-id="cb566-187">Input (filter query):</span></span>

```
:> g.V().hasLabel('person').has('age', gt(40))
```

<span data-ttu-id="cb566-188">Saída:</span><span class="sxs-lookup"><span data-stu-id="cb566-188">Output:</span></span>

```
==>[id:ae36f938-210e-445a-92df-519f2b64c8ec,label:person,type:vertex,properties:[firstName:[[id:872090b6-6a77-456a-9a55-a59141d4ebc2,value:Thomas]],lastName:[[id:7ee7a39a-a414-4127-89b4-870bc4ef99f3,value:Andersen]],age:[[id:a2a75d5a-ae70-4095-806d-a35abcbfe71d,value:45]]]]
```

<span data-ttu-id="cb566-189">Em seguida, vamos Olá primeiro nome de projeto para pessoas hello mais de 40 anos de idade.</span><span class="sxs-lookup"><span data-stu-id="cb566-189">Next, let's project hello first name for hello people who are older than 40 years old.</span></span>

<span data-ttu-id="cb566-190">Entrada (filtro + consulta de projeção):</span><span class="sxs-lookup"><span data-stu-id="cb566-190">Input (filter + projection query):</span></span>

```
:> g.V().hasLabel('person').has('age', gt(40)).values('firstName')
```

<span data-ttu-id="cb566-191">Saída:</span><span class="sxs-lookup"><span data-stu-id="cb566-191">Output:</span></span>

```
==>Thomas
```

## <a name="traverse-your-graph"></a><span data-ttu-id="cb566-192">Percorrer o gráfico</span><span class="sxs-lookup"><span data-stu-id="cb566-192">Traverse your graph</span></span>

<span data-ttu-id="cb566-193">Vamos percorrer Olá gráfico tooreturn todos os amigos de Thomas.</span><span class="sxs-lookup"><span data-stu-id="cb566-193">Let's traverse hello graph tooreturn all of Thomas's friends.</span></span>

<span data-ttu-id="cb566-194">Entrada (amigos de Thomas):</span><span class="sxs-lookup"><span data-stu-id="cb566-194">Input (friends of Thomas):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').outE('knows').inV().hasLabel('person')
```

<span data-ttu-id="cb566-195">Saída:</span><span class="sxs-lookup"><span data-stu-id="cb566-195">Output:</span></span> 

```
==>[id:f04bc00b-cb56-46c4-a3bb-a5870c42f7ff,label:person,type:vertex,properties:[firstName:[[id:14feedec-b070-444e-b544-62be15c7167c,value:Mary Kay]],lastName:[[id:107ab421-7208-45d4-b969-bbc54481992a,value:Andersen]],age:[[id:4b08d6e4-58f5-45df-8e69-6b790b692e0a,value:39]]]]
==>[id:91605c63-4988-4b60-9a30-5144719ae326,label:person,type:vertex,properties:[firstName:[[id:f760e0e6-652a-481a-92b0-1767d9bf372e,value:Robin]],lastName:[[id:352a4caa-bad6-47e3-a7dc-90ff342cf870,value:Wakefield]]]]
```

<span data-ttu-id="cb566-196">Em seguida, vamos fazer com que a próxima camada Olá dos vértices.</span><span class="sxs-lookup"><span data-stu-id="cb566-196">Next, let's get hello next layer of vertices.</span></span> <span data-ttu-id="cb566-197">Percorra Olá gráfico tooreturn todos os amigos Olá de amigos de Thomas.</span><span class="sxs-lookup"><span data-stu-id="cb566-197">Traverse hello graph tooreturn all hello friends of Thomas's friends.</span></span>

<span data-ttu-id="cb566-198">Entrada (amigos de amigos de Thomas):</span><span class="sxs-lookup"><span data-stu-id="cb566-198">Input (friends of friends of Thomas):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```
<span data-ttu-id="cb566-199">Saída:</span><span class="sxs-lookup"><span data-stu-id="cb566-199">Output:</span></span>

```
==>[id:a801a0cb-ee85-44ee-a502-271685ef212e,label:person,type:vertex,properties:[firstName:[[id:b9489902-d29a-4673-8c09-c2b3fe7f8b94,value:Ben]],lastName:[[id:e084f933-9a4b-4dbc-8273-f0171265cf1d,value:Miller]]]]
```

## <a name="drop-a-vertex"></a><span data-ttu-id="cb566-200">Remover um vértice</span><span class="sxs-lookup"><span data-stu-id="cb566-200">Drop a vertex</span></span>

<span data-ttu-id="cb566-201">Agora vamos excluir um vértice do banco de dados de gráfico de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb566-201">Let's now delete a vertex from hello graph database.</span></span>

<span data-ttu-id="cb566-202">Entrada (tirar conector da tomada):</span><span class="sxs-lookup"><span data-stu-id="cb566-202">Input (drop Jack vertex):</span></span>

```
:> g.V().hasLabel('person').has('firstName', 'Jack').drop()
```

## <a name="clear-your-graph"></a><span data-ttu-id="cb566-203">Limpar o gráfico</span><span class="sxs-lookup"><span data-stu-id="cb566-203">Clear your graph</span></span>

<span data-ttu-id="cb566-204">Por fim, vamos limpar o banco de dados de saudação de todos os vértices e bordas.</span><span class="sxs-lookup"><span data-stu-id="cb566-204">Finally, let's clear hello database of all vertices and edges.</span></span>

<span data-ttu-id="cb566-205">Entrada:</span><span class="sxs-lookup"><span data-stu-id="cb566-205">Input:</span></span>

```
:> g.E().drop()
:> g.V().drop()
```

<span data-ttu-id="cb566-206">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="cb566-206">Congratulations!</span></span> <span data-ttu-id="cb566-207">Você concluiu este tutorial sobre BD Cosmos do Azure: API do Graph!</span><span class="sxs-lookup"><span data-stu-id="cb566-207">You've completed this Azure Cosmos DB: Graph API tutorial!</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="cb566-208">Examine os SLAs em Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="cb566-208">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="cb566-209">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="cb566-209">Clean up resources</span></span>

<span data-ttu-id="cb566-210">Se você não vai toocontinue toouse este aplicativo, exclua todos os recursos criados por este guia de início rápido Olá portal do Azure com hello etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="cb566-210">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>  

1. <span data-ttu-id="cb566-211">No menu esquerdo de saudação do hello portal do Azure, clique em **grupos de recursos** e clique em nome de saudação do recurso de saudação criado por você.</span><span class="sxs-lookup"><span data-stu-id="cb566-211">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="cb566-212">Na sua página de grupo de recursos, clique em **excluir**, digite o nome de saudação do hello recurso toodelete na caixa de texto de saudação e, em seguida, clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="cb566-212">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb566-213">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cb566-213">Next steps</span></span>

<span data-ttu-id="cb566-214">Este guia de início rápido, você aprendeu como toocreate uma conta de banco de dados do Azure Cosmos, criar um gráfico usando Olá Explorador de dados, criar vértices e bordas e percorrer o gráfico usando o console de Gremlin hello.</span><span class="sxs-lookup"><span data-stu-id="cb566-214">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a graph using hello Data Explorer, create vertices and edges, and traverse your graph using hello Gremlin console.</span></span> <span data-ttu-id="cb566-215">Agora, você pode criar consultas mais complexas e implementar uma lógica de passagem de gráfico avançada usando o Gremlin.</span><span class="sxs-lookup"><span data-stu-id="cb566-215">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="cb566-216">Consultar usando o Gremlin</span><span class="sxs-lookup"><span data-stu-id="cb566-216">Query using Gremlin</span></span>](tutorial-query-graph.md)
