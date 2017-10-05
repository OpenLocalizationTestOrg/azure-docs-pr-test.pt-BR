---
title: Usar o Azure Functions para executar uma tarefa de limpeza de banco de dados | Microsoft Docs
description: Use o Azure Functions para agendar uma tarefa que se conecta ao banco de dados SQL do Azure para limpar linhas periodicamente.
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 076f5f95-f8d2-42c7-b7fd-6798856ba0bb
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/22/2017
ms.author: glenga
ms.openlocfilehash: 6fd0e32374827b249f5aba1cbfc39117c88c6272
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-functions-to-connect-to-an-azure-sql-database"></a><span data-ttu-id="d6419-103">Usar o Azure Functions para conectar a um banco de dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="d6419-103">Use Azure Functions to connect to an Azure SQL Database</span></span>
<span data-ttu-id="d6419-104">Este tópico mostra como usar o Azure Functions para criar um trabalho agendado que limpa linhas em uma tabela em um banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="d6419-104">This topic shows you how to use Azure Functions to create a scheduled job that cleans up rows in a table in an Azure SQL Database.</span></span> <span data-ttu-id="d6419-105">A nova função C# é criada com base em um gatilho de temporizador predefinido no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d6419-105">The new C# function is created based on a pre-defined timer trigger template in the Azure portal.</span></span> <span data-ttu-id="d6419-106">Para dar suporte a esse cenário, você também precisa definir uma cadeia de conexão de banco de dados como uma configuração no aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="d6419-106">To support this scenario, you must also set a database connection string as a setting in the function app.</span></span> <span data-ttu-id="d6419-107">Esse cenário usa uma operação em massa no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="d6419-107">This scenario uses a bulk operation against the database.</span></span> <span data-ttu-id="d6419-108">Para que sua função processe operações CRUD individuais em uma tabela dos Aplicativos Móveis, você deve usar as [Associações de aplicativos móveis](functions-bindings-mobile-apps.md).</span><span class="sxs-lookup"><span data-stu-id="d6419-108">To have your function process individual CRUD operations in a Mobile Apps table, you should instead use [Mobile Apps bindings](functions-bindings-mobile-apps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6419-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d6419-109">Prerequisites</span></span>

+ <span data-ttu-id="d6419-110">Este tópico usa uma função disparada por temporizador.</span><span class="sxs-lookup"><span data-stu-id="d6419-110">This topic uses a timer triggered function.</span></span> <span data-ttu-id="d6419-111">Conclua as etapas no tópico [Criar uma função no Azure que seja disparada por um temporizador](functions-create-scheduled-function.md) para criar uma versão C# dessa função.</span><span class="sxs-lookup"><span data-stu-id="d6419-111">Complete the steps in the topic [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md) to create a C# version of this function.</span></span>   

+ <span data-ttu-id="d6419-112">Este tópico demonstra um comando Transact-SQL que executa uma operação de limpeza em massa na tabela **SalesOrderHeader** no banco de dados de amostra AdventureWorksLT.</span><span class="sxs-lookup"><span data-stu-id="d6419-112">This topic demonstrates a Transact-SQL command that executes a bulk cleanup operation in the **SalesOrderHeader** table in the AdventureWorksLT sample database.</span></span> <span data-ttu-id="d6419-113">Para criar o banco de dados de amostra AdventureWorksLT, conclua as etapas no tópico [Criar um Banco de Dados SQL do Azure no Portal do Azure](../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d6419-113">To create the AdventureWorksLT sample database, complete the steps in the topic [Create an Azure SQL database in the Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span> 

## <a name="get-connection-information"></a><span data-ttu-id="d6419-114">Obter informações de conexão</span><span class="sxs-lookup"><span data-stu-id="d6419-114">Get connection information</span></span>

<span data-ttu-id="d6419-115">Você precisa obter a cadeia de conexão para o banco de dados que você criou quando concluiu [Criar um Banco de Dados SQL do Azure no Portal do Azure](../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d6419-115">You need to get the connection string for the database you created when you completed [Create an Azure SQL database in the Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span>

1. <span data-ttu-id="d6419-116">Faça logon no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d6419-116">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
 
3. <span data-ttu-id="d6419-117">Selecione **Bancos de Dados SQL** no menu à esquerda e selecione seu banco de dados na página **Bancos de Dados SQL**.</span><span class="sxs-lookup"><span data-stu-id="d6419-117">Select **SQL Databases** from the left-hand menu, and select your database on the **SQL databases** page.</span></span>

4. <span data-ttu-id="d6419-118">Selecione **Mostrar cadeias de conexão do banco de dados** e copie a cadeia de conexão completa do **ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="d6419-118">Select **Show database connection strings** and copy the complete **ADO.NET** connection string.</span></span>

    ![Copie a cadeia de conexão ADO.NET.](./media/functions-scenario-database-table-cleanup/adonet-connection-string.png)

## <a name="set-the-connection-string"></a><span data-ttu-id="d6419-120">Definir a cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="d6419-120">Set the connection string</span></span> 

<span data-ttu-id="d6419-121">Um aplicativo de função hospeda a execução de suas funções no Azure.</span><span class="sxs-lookup"><span data-stu-id="d6419-121">A function app hosts the execution of your functions in Azure.</span></span> <span data-ttu-id="d6419-122">É uma prática recomendada armazenar cadeias de conexão e outros segredos nas configurações do seu aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="d6419-122">It is a best practice to store connection strings and other secrets in your function app settings.</span></span> <span data-ttu-id="d6419-123">Usar as configurações do aplicativo impede a divulgação acidental da cadeia de conexão com seu código.</span><span class="sxs-lookup"><span data-stu-id="d6419-123">Using application settings prevents accidental disclosure of the connection string with your code.</span></span> 

1. <span data-ttu-id="d6419-124">Navegue até seu aplicativo de funções criado em [Criar uma função no Azure que é disparada por um temporizador](functions-create-scheduled-function.md).</span><span class="sxs-lookup"><span data-stu-id="d6419-124">Navigate to your function app you created [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md).</span></span>

2. <span data-ttu-id="d6419-125">Selecione **Recursos da plataforma** > **Configurações de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="d6419-125">Select **Platform features** > **Application settings**.</span></span>
   
    ![Configurações de aplicativo para o aplicativo de funções.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings.png)

2. <span data-ttu-id="d6419-127">Role para baixo até **Cadeias de caracteres de conexão** e adicione uma cadeia de conexão usando as configurações especificadas na tabela.</span><span class="sxs-lookup"><span data-stu-id="d6419-127">Scroll down to **Connection strings** and add a connection string using the settings as specified in the table.</span></span>
   
    ![Adicione uma cadeia de conexão às configurações do aplicativo de funções.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings-connection-strings.png)

    | <span data-ttu-id="d6419-129">Configuração</span><span class="sxs-lookup"><span data-stu-id="d6419-129">Setting</span></span>       | <span data-ttu-id="d6419-130">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="d6419-130">Suggested value</span></span> | <span data-ttu-id="d6419-131">Descrição</span><span class="sxs-lookup"><span data-stu-id="d6419-131">Description</span></span>             | 
    | ------------ | ------------------ | --------------------- | 
    | <span data-ttu-id="d6419-132">**Nome**</span><span class="sxs-lookup"><span data-stu-id="d6419-132">**Name**</span></span>  |  <span data-ttu-id="d6419-133">sqldb_connection</span><span class="sxs-lookup"><span data-stu-id="d6419-133">sqldb_connection</span></span>  | <span data-ttu-id="d6419-134">Usado para acessar a cadeia de conexão armazenada no seu código de função.</span><span class="sxs-lookup"><span data-stu-id="d6419-134">Used to access the stored connection string in your function code.</span></span>    |
    | <span data-ttu-id="d6419-135">**Valor**</span><span class="sxs-lookup"><span data-stu-id="d6419-135">**Value**</span></span> | <span data-ttu-id="d6419-136">Cadeia de caracteres copiada</span><span class="sxs-lookup"><span data-stu-id="d6419-136">Copied string</span></span>  | <span data-ttu-id="d6419-137">Cole a cadeia de conexão que você copiou na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="d6419-137">Past the connection string you copied in the previous section.</span></span> |
    | <span data-ttu-id="d6419-138">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="d6419-138">**Type**</span></span> | <span data-ttu-id="d6419-139">Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="d6419-139">SQL Database</span></span> | <span data-ttu-id="d6419-140">Use a conexão do Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="d6419-140">Use the default SQL Database connection.</span></span> |   

3. <span data-ttu-id="d6419-141">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="d6419-141">Click **Save**.</span></span>

<span data-ttu-id="d6419-142">Agora, você pode adicionar o código de função C# que conecta ao Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="d6419-142">Now, you can add the C# function code that connects to your SQL Database.</span></span>

## <a name="update-your-function-code"></a><span data-ttu-id="d6419-143">Atualizar o código de função</span><span class="sxs-lookup"><span data-stu-id="d6419-143">Update your function code</span></span>

1. <span data-ttu-id="d6419-144">Em seu aplicativo de funções, selecione a Função disparada por temporizador.</span><span class="sxs-lookup"><span data-stu-id="d6419-144">In your function app, select the timer-triggered function.</span></span>
 
3. <span data-ttu-id="d6419-145">Adicione as seguintes referências de assembly na parte superior do código de função existente:</span><span class="sxs-lookup"><span data-stu-id="d6419-145">Add the following assembly references at the top of the existing function code:</span></span>

    ```cs
    #r "System.Configuration"
    #r "System.Data"
    ```

3. <span data-ttu-id="d6419-146">Adicione as instruções `using` a seguir à função:</span><span class="sxs-lookup"><span data-stu-id="d6419-146">Add the following `using` statements to the function:</span></span>
    ```cs
    using System.Configuration;
    using System.Data.SqlClient;
    using System.Threading.Tasks;
    ```

4. <span data-ttu-id="d6419-147">Substitua a função **Run** existente por este código:</span><span class="sxs-lookup"><span data-stu-id="d6419-147">Replace the existing **Run** function with the following code:</span></span>
    ```cs
    public static async Task Run(TimerInfo myTimer, TraceWriter log)
    {
        var str = ConfigurationManager.ConnectionStrings["sqldb_connection"].ConnectionString;
        using (SqlConnection conn = new SqlConnection(str))
        {
            conn.Open();
            var text = "UPDATE SalesLT.SalesOrderHeader " + 
                    "SET [Status] = 5  WHERE ShipDate < GetDate();";

            using (SqlCommand cmd = new SqlCommand(text, conn))
            {
                // Execute the command and log the # rows affected.
                var rows = await cmd.ExecuteNonQueryAsync();
                log.Info($"{rows} rows were updated");
            }
        }
    }
    ```

    <span data-ttu-id="d6419-148">Este comando atualiza a coluna **Status** com base na data de envio.</span><span class="sxs-lookup"><span data-stu-id="d6419-148">This sample command updates the **Status** column based on the ship date.</span></span> <span data-ttu-id="d6419-149">Ele deve atualizar 32 linhas de dados.</span><span class="sxs-lookup"><span data-stu-id="d6419-149">It should update 32 rows of data.</span></span>

5. <span data-ttu-id="d6419-150">Clique em **Salvar**, observe nas janelas de **Logs** a execução da próxima função e observe o número de linhas atualizadas na tabela **SalesOrderHeader**.</span><span class="sxs-lookup"><span data-stu-id="d6419-150">Click **Save**, watch the **Logs** windows for the next function execution, then note the number of rows updated in the **SalesOrderHeader** table.</span></span>

    ![Exibir os logs da função.](./media/functions-scenario-database-table-cleanup/functions-logs.png)

## <a name="next-steps"></a><span data-ttu-id="d6419-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d6419-152">Next steps</span></span>

<span data-ttu-id="d6419-153">Em seguida, saiba como usar o Functions com Aplicativos Lógicos para integração com outros serviços.</span><span class="sxs-lookup"><span data-stu-id="d6419-153">Next, learn how to use Functions with Logic Apps to integrate with other services.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="d6419-154">Criar uma função que se integra nos Aplicativos Lógicos</span><span class="sxs-lookup"><span data-stu-id="d6419-154">Create a function that integrates with Logic Apps</span></span>](functions-twitter-email.md)

<span data-ttu-id="d6419-155">Confira estes tópicos para obter mais informações sobre o Functions:</span><span class="sxs-lookup"><span data-stu-id="d6419-155">For more information about Functions, see the following topics:</span></span>

* [<span data-ttu-id="d6419-156">Referência do desenvolvedor do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="d6419-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="d6419-157">Referência do programador para codificação de funções e definição de gatilhos e de associações.</span><span class="sxs-lookup"><span data-stu-id="d6419-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="d6419-158">Testando o Azure Functions</span><span class="sxs-lookup"><span data-stu-id="d6419-158">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="d6419-159">Descreve várias ferramentas e técnicas para testar suas funções.</span><span class="sxs-lookup"><span data-stu-id="d6419-159">Describes various tools and techniques for testing your functions.</span></span>  
