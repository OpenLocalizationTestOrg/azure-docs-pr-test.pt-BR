---
title: "Adicionar o conector do Banco de Dados SQL em seus Aplicativos Lógicos | Microsoft Docs"
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
ms.openlocfilehash: a3d5cb909dbfcb00f3fbfa0165bb6cd58eb18688
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-azure-sql-database-connector"></a><span data-ttu-id="b5546-103">Introdução ao conector do Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="b5546-103">Get started with the Azure SQL Database connector</span></span>
<span data-ttu-id="b5546-104">Usando o conector do Banco de Dados SQL, crie fluxos de trabalho para sua organização que gerenciam dados nas tabelas.</span><span class="sxs-lookup"><span data-stu-id="b5546-104">Using the Azure SQL Database connector, create workflows for your organization that manage data in your tables.</span></span> 

<span data-ttu-id="b5546-105">Com o Banco de Dados SQL, você:</span><span class="sxs-lookup"><span data-stu-id="b5546-105">With SQL Database, you:</span></span>

* <span data-ttu-id="b5546-106">Compile o fluxo de trabalho adicionando um novo cliente a um banco de dados de clientes ou atualizando um pedido em um banco de dados de pedidos.</span><span class="sxs-lookup"><span data-stu-id="b5546-106">Build your workflow by adding a new customer to a customers database, or updating an order in an orders database.</span></span>
* <span data-ttu-id="b5546-107">Use as ações para obter uma linha de dados, inserir uma nova linha e até mesmo excluir.</span><span class="sxs-lookup"><span data-stu-id="b5546-107">Use actions to get a row of data, insert a new row, and even delete.</span></span> <span data-ttu-id="b5546-108">Por exemplo, quando um registro é criado no Dynamics CRM Online (um gatilho), insira uma linha em um Banco de Dados SQL do Azure (uma ação).</span><span class="sxs-lookup"><span data-stu-id="b5546-108">For example,  when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Azure SQL Database (an action).</span></span> 

<span data-ttu-id="b5546-109">Este tópico mostra como usar o conector do Banco de Dados SQL em um aplicativo lógico, além de listar as ações.</span><span class="sxs-lookup"><span data-stu-id="b5546-109">This topic shows you how to use the SQL Database connector in a logic app, and also lists the actions.</span></span>

<span data-ttu-id="b5546-110">Para saber mais sobre os Aplicativos Lógicos, consulte [O que são aplicativos lógicos](../logic-apps/logic-apps-what-are-logic-apps.md) e [Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="b5546-110">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-azure-sql-database"></a><span data-ttu-id="b5546-111">Conectar-se ao Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="b5546-111">Connect to Azure SQL Database</span></span>
<span data-ttu-id="b5546-112">Antes do aplicativo lógico poder acessar qualquer serviço, primeiro crie uma *conexão* com o serviço.</span><span class="sxs-lookup"><span data-stu-id="b5546-112">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="b5546-113">Uma conexão fornece uma conectividade entre um aplicativo lógico e outro serviço.</span><span class="sxs-lookup"><span data-stu-id="b5546-113">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="b5546-114">Por exemplo, para se conectar ao Banco de Dados SQL, você cria uma *conexão* do Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="b5546-114">For example, to connect to SQL Database, you first create a SQL Database *connection*.</span></span> <span data-ttu-id="b5546-115">Para criar uma conexão, insira as credenciais que normalmente usa para acessar o serviço ao qual você está se conectando.</span><span class="sxs-lookup"><span data-stu-id="b5546-115">To create a connection, you enter the credentials you normally use to access the service you are connecting to.</span></span> <span data-ttu-id="b5546-116">Desse modo, no Banco de Dados SQL, insira suas credenciais do Banco de Dados SQL para criar a conexão.</span><span class="sxs-lookup"><span data-stu-id="b5546-116">So, in SQL Database, enter your SQL Database credentials to create the connection.</span></span> 

#### <a name="create-the-connection"></a><span data-ttu-id="b5546-117">Criar a conexão</span><span class="sxs-lookup"><span data-stu-id="b5546-117">Create the connection</span></span>
> [!INCLUDE [Create the connection to SQL Azure](../../includes/connectors-create-api-sqlazure.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="b5546-118">Usar um gatilho</span><span class="sxs-lookup"><span data-stu-id="b5546-118">Use a trigger</span></span>
<span data-ttu-id="b5546-119">Esse conector não tem gatilhos.</span><span class="sxs-lookup"><span data-stu-id="b5546-119">This connector does not have any triggers.</span></span> <span data-ttu-id="b5546-120">Use outros gatilhos para iniciar o aplicativo lógico, como um gatilho de Recorrência, um gatilho de Webhook HTTP, gatilhos disponíveis com outros conectores e muito mais.</span><span class="sxs-lookup"><span data-stu-id="b5546-120">Use other triggers to start the logic app, such as a Recurrence trigger, an HTTP Webhook trigger, triggers available with other connectors, and more.</span></span> <span data-ttu-id="b5546-121">[Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md) fornece um exemplo.</span><span class="sxs-lookup"><span data-stu-id="b5546-121">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) provides an example.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="b5546-122">Usar uma ação</span><span class="sxs-lookup"><span data-stu-id="b5546-122">Use an action</span></span>
<span data-ttu-id="b5546-123">Uma ação é uma operação executada pelo fluxo de trabalho definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="b5546-123">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="b5546-124">[Saiba mais sobre ações](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="b5546-124">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="b5546-125">Selecione o sinal de mais.</span><span class="sxs-lookup"><span data-stu-id="b5546-125">Select the plus sign.</span></span> <span data-ttu-id="b5546-126">Você tem várias opções: **adicionar uma ação**, **adicionar uma condição** ou uma das opções **Mais**.</span><span class="sxs-lookup"><span data-stu-id="b5546-126">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/add-action.png)
2. <span data-ttu-id="b5546-127">Escolha **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="b5546-127">Choose **Add an action**.</span></span>
3. <span data-ttu-id="b5546-128">Na caixa de texto, digite "sql" para obter uma lista de todas as ações disponíveis.</span><span class="sxs-lookup"><span data-stu-id="b5546-128">In the text box, type “sql” to get a list of all the available actions.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sql-1.png) 
4. <span data-ttu-id="b5546-129">Em nosso exemplo, escolha **SQL Server – obter linha**.</span><span class="sxs-lookup"><span data-stu-id="b5546-129">In our example, choose **SQL Server - Get row**.</span></span> <span data-ttu-id="b5546-130">Se uma conexão já existir, escolha o **Nome da tabela** na lista suspensa e insira a **ID da Linha** que deseja retornar.</span><span class="sxs-lookup"><span data-stu-id="b5546-130">If a connection already exists, then select the **Table name** from the drop-down list, and enter the **Row ID** you want to return.</span></span>
   
    ![](./media/connectors-create-api-sqlazure/sample-table.png)
   
    <span data-ttu-id="b5546-131">Se as informações de conexão forem solicitadas, insira os detalhes para criar a conexão.</span><span class="sxs-lookup"><span data-stu-id="b5546-131">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="b5546-132">[Criar a conexão](connectors-create-api-sqlazure.md#create-the-connection) neste tópico descreve estas propriedades.</span><span class="sxs-lookup"><span data-stu-id="b5546-132">[Create the connection](connectors-create-api-sqlazure.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="b5546-133">Nesse exemplo, retornamos uma linha de uma tabela.</span><span class="sxs-lookup"><span data-stu-id="b5546-133">In this example, we return a row from a table.</span></span> <span data-ttu-id="b5546-134">Para ver os dados nessa linha, adicione outra ação que cria um arquivo usando os campos da tabela.</span><span class="sxs-lookup"><span data-stu-id="b5546-134">To see the data in this row, add another action that creates a file using the fields from the table.</span></span> <span data-ttu-id="b5546-135">Por exemplo, adicione uma ação do OneDrive que usa os campos FirstName e LastName para criar um novo arquivo na conta de armazenamento de nuvem.</span><span class="sxs-lookup"><span data-stu-id="b5546-135">For example, add a OneDrive action that uses the FirstName and LastName fields to create a new file in the cloud storage account.</span></span> 
   > 
   > 
5. <span data-ttu-id="b5546-136">**Salve** as alterações (canto superior esquerdo da barra de ferramentas).</span><span class="sxs-lookup"><span data-stu-id="b5546-136">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="b5546-137">Seu aplicativo lógico é salvo e pode ser habilitado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b5546-137">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="b5546-138">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="b5546-138">Connector-specific details</span></span>

<span data-ttu-id="b5546-139">Exiba os gatilhos e ações definidos no swagger e também os limites nos [detalhes do conector](/connectors/sql/).</span><span class="sxs-lookup"><span data-stu-id="b5546-139">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sql/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b5546-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b5546-140">Next steps</span></span>
<span data-ttu-id="b5546-141">[Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="b5546-141">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="b5546-142">Explore os outros conectores disponíveis nos Aplicativos Lógicos em nossa [lista de APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="b5546-142">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

