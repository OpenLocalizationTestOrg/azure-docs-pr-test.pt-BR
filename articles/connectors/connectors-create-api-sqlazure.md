---
title: "conector de banco de dados do Azure SQL Olá aaaAdd em seus aplicativos lógicos | Microsoft Docs"
description: "Visão geral do conector do Banco de Dados SQL do Azure com parâmetros da API REST"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d8a319d0-e4df-40cf-88f0-29a6158c898c
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: a9ca0f446d05dc00f310a908eee8d50e41fcd82b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-azure-sql-database-connector"></a><span data-ttu-id="bda9f-103">Introdução ao conector do Azure SQL Database Olá</span><span class="sxs-lookup"><span data-stu-id="bda9f-103">Get started with hello Azure SQL Database connector</span></span>
<span data-ttu-id="bda9f-104">Usando o conector do Azure SQL Database hello, crie fluxos de trabalho para a sua organização que gerenciam dados nas tabelas.</span><span class="sxs-lookup"><span data-stu-id="bda9f-104">Using hello Azure SQL Database connector, create workflows for your organization that manage data in your tables.</span></span> 

<span data-ttu-id="bda9f-105">Com o Banco de Dados SQL, você:</span><span class="sxs-lookup"><span data-stu-id="bda9f-105">With SQL Database, you:</span></span>

* <span data-ttu-id="bda9f-106">Crie o fluxo de trabalho adicionando um novo cliente tooa clientes banco de dados, ou atualizando um pedido em um banco de dados de pedidos.</span><span class="sxs-lookup"><span data-stu-id="bda9f-106">Build your workflow by adding a new customer tooa customers database, or updating an order in an orders database.</span></span>
* <span data-ttu-id="bda9f-107">Use ações tooget uma linha de dados, inserir uma nova linha e até mesmo excluir.</span><span class="sxs-lookup"><span data-stu-id="bda9f-107">Use actions tooget a row of data, insert a new row, and even delete.</span></span> <span data-ttu-id="bda9f-108">Por exemplo, quando um registro é criado no Dynamics CRM Online (um gatilho), insira uma linha em um Banco de Dados SQL do Azure (uma ação).</span><span class="sxs-lookup"><span data-stu-id="bda9f-108">For example,  when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Azure SQL Database (an action).</span></span> 

<span data-ttu-id="bda9f-109">Este tópico mostra como toouse Olá conector de banco de dados SQL em um aplicativo lógico e também lista Olá ações.</span><span class="sxs-lookup"><span data-stu-id="bda9f-109">This topic shows you how toouse hello SQL Database connector in a logic app, and also lists hello actions.</span></span>

<span data-ttu-id="bda9f-110">toolearn mais sobre aplicativos lógicos, consulte [quais são os aplicativos lógicos](../logic-apps/logic-apps-what-are-logic-apps.md) e [criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="bda9f-110">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooazure-sql-database"></a><span data-ttu-id="bda9f-111">Conecte-se tooAzure banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="bda9f-111">Connect tooAzure SQL Database</span></span>
<span data-ttu-id="bda9f-112">Antes de sua lógica de aplicativo pode acessar qualquer serviço, você primeiro crie um *conexão* toohello service.</span><span class="sxs-lookup"><span data-stu-id="bda9f-112">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="bda9f-113">Uma conexão fornece uma conectividade entre um aplicativo lógico e outro serviço.</span><span class="sxs-lookup"><span data-stu-id="bda9f-113">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="bda9f-114">Por exemplo, tooconnect tooSQL banco de dados, você primeiro crie um banco de dados SQL *conexão*.</span><span class="sxs-lookup"><span data-stu-id="bda9f-114">For example, tooconnect tooSQL Database, you first create a SQL Database *connection*.</span></span> <span data-ttu-id="bda9f-115">toocreate uma conexão, em que você insira as credenciais de saudação que você normalmente usa o serviço de saudação tooaccess que você está se conectando.</span><span class="sxs-lookup"><span data-stu-id="bda9f-115">toocreate a connection, you enter hello credentials you normally use tooaccess hello service you are connecting to.</span></span> <span data-ttu-id="bda9f-116">Portanto, no banco de dados SQL, insira sua conexão do banco de dados SQL credenciais toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="bda9f-116">So, in SQL Database, enter your SQL Database credentials toocreate hello connection.</span></span> 

#### <a name="create-hello-connection"></a><span data-ttu-id="bda9f-117">Criar conexão Olá</span><span class="sxs-lookup"><span data-stu-id="bda9f-117">Create hello connection</span></span>
> [!INCLUDE [Create hello connection tooSQL Azure](../../includes/connectors-create-api-sqlazure.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="bda9f-118">Usar um gatilho</span><span class="sxs-lookup"><span data-stu-id="bda9f-118">Use a trigger</span></span>
<span data-ttu-id="bda9f-119">Esse conector não tem gatilhos.</span><span class="sxs-lookup"><span data-stu-id="bda9f-119">This connector does not have any triggers.</span></span> <span data-ttu-id="bda9f-120">Use outros gatilhos toostart Olá lógica aplicativo, como um disparador de recorrência, um gatilho de HTTP Webhook, disparadores disponíveis com outros conectores e muito mais.</span><span class="sxs-lookup"><span data-stu-id="bda9f-120">Use other triggers toostart hello logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="bda9f-121">[Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md) fornece um exemplo.</span><span class="sxs-lookup"><span data-stu-id="bda9f-121">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="bda9f-122">Usar uma ação</span><span class="sxs-lookup"><span data-stu-id="bda9f-122">Use an action</span></span>
<span data-ttu-id="bda9f-123">Uma ação é uma operação executada pelo fluxo de trabalho Olá definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="bda9f-123">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="bda9f-124">[Saiba mais sobre ações](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="bda9f-124">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="bda9f-125">Selecione o sinal de adição hello.</span><span class="sxs-lookup"><span data-stu-id="bda9f-125">Select hello plus sign.</span></span> <span data-ttu-id="bda9f-126">Consulte várias opções: **adicionar uma ação**, **adicionar uma condição**, ou uma saudação **mais** opções.</span><span class="sxs-lookup"><span data-stu-id="bda9f-126">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/add-action.png)
2. <span data-ttu-id="bda9f-127">Escolha **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="bda9f-127">Choose **Add an action**.</span></span>
3. <span data-ttu-id="bda9f-128">Na caixa de texto de saudação, digite "sql" tooget uma lista de todas as ações disponíveis de saudação.</span><span class="sxs-lookup"><span data-stu-id="bda9f-128">In hello text box, type “sql” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sql-1.png) 
4. <span data-ttu-id="bda9f-129">Em nosso exemplo, escolha **SQL Server – obter linha**.</span><span class="sxs-lookup"><span data-stu-id="bda9f-129">In our example, choose **SQL Server - Get row**.</span></span> <span data-ttu-id="bda9f-130">Se uma conexão já existir, selecione Olá **nome de tabela** Olá suspenso lista e digite Olá **ID da linha** deseja tooreturn.</span><span class="sxs-lookup"><span data-stu-id="bda9f-130">If a connection already exists, then select hello **Table name** from hello drop-down list, and enter hello **Row ID** you want tooreturn.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sample-table.png)
   
    <span data-ttu-id="bda9f-131">Se você for solicitado para obter informações de conexão do hello, digite conexão de Olá Olá detalhes toocreate.</span><span class="sxs-lookup"><span data-stu-id="bda9f-131">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="bda9f-132">[Criar conexão Olá](connectors-create-api-sqlazure.md#create-the-connection) neste tópico descreve essas propriedades.</span><span class="sxs-lookup"><span data-stu-id="bda9f-132">[Create hello connection](connectors-create-api-sqlazure.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="bda9f-133">Nesse exemplo, retornamos uma linha de uma tabela.</span><span class="sxs-lookup"><span data-stu-id="bda9f-133">In this example, we return a row from a table.</span></span> <span data-ttu-id="bda9f-134">dados de saudação toosee nessa linha, adicione outra ação que cria um arquivo usando Olá campos da tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="bda9f-134">toosee hello data in this row, add another action that creates a file using hello fields from hello table.</span></span> <span data-ttu-id="bda9f-135">Por exemplo, adicione uma ação de OneDrive que usa hello FirstName e LastName campos toocreate um novo arquivo na conta de armazenamento de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="bda9f-135">For example, add a OneDrive action that uses hello FirstName and LastName fields toocreate a new file in hello cloud storage account.</span></span> 
   > 
   > 
5. <span data-ttu-id="bda9f-136">**Salvar** as alterações (canto superior esquerdo da barra de ferramentas de saudação).</span><span class="sxs-lookup"><span data-stu-id="bda9f-136">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="bda9f-137">Seu aplicativo lógico é salvo e pode ser habilitado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="bda9f-137">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="bda9f-138">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="bda9f-138">Connector-specific details</span></span>

<span data-ttu-id="bda9f-139">Exibir quaisquer gatilhos e ações definidas em swagger Olá e também os limites de saudação [detalhes conector](/connectors/sql/).</span><span class="sxs-lookup"><span data-stu-id="bda9f-139">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/sql/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="bda9f-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bda9f-140">Next steps</span></span>
<span data-ttu-id="bda9f-141">[Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="bda9f-141">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="bda9f-142">Explorar Olá outros conectores disponíveis na lógica de aplicativos no nosso [lista APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="bda9f-142">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

