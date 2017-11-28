---
title: "Limpeza de um banco de dados aaaUse funções do Azure tooperform tarefa | Microsoft Docs"
description: "Use funções do Azure tooschedule uma tarefa que conecta tooAzure banco de dados SQL tooperiodically limpar linhas."
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
ms.openlocfilehash: 063a25fe8d14a75d54e9b72cec9fc1e25fa3ff44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-functions-tooconnect-tooan-azure-sql-database"></a><span data-ttu-id="c7326-103">Use as funções do Azure tooconnect tooan banco de dados do SQL Azure</span><span class="sxs-lookup"><span data-stu-id="c7326-103">Use Azure Functions tooconnect tooan Azure SQL Database</span></span>
<span data-ttu-id="c7326-104">Este tópico mostra como toouse funções do Azure toocreate agendado do trabalho que limpa a linhas em uma tabela em um banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="c7326-104">This topic shows you how toouse Azure Functions toocreate a scheduled job that cleans up rows in a table in an Azure SQL Database.</span></span> <span data-ttu-id="c7326-105">Olá nova função c# é criada com base em um modelo de gatilho de timer predefinidos Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7326-105">hello new C# function is created based on a pre-defined timer trigger template in hello Azure portal.</span></span> <span data-ttu-id="c7326-106">toosupport neste cenário, você também deve definir uma cadeia de caracteres de conexão do banco de dados como uma configuração de aplicativo de função hello.</span><span class="sxs-lookup"><span data-stu-id="c7326-106">toosupport this scenario, you must also set a database connection string as a setting in hello function app.</span></span> <span data-ttu-id="c7326-107">Esse cenário usa uma operação em massa no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7326-107">This scenario uses a bulk operation against hello database.</span></span> <span data-ttu-id="c7326-108">toohave sua função processo CRUD operações individuais em uma tabela de aplicativos móveis, você deve usar [associações de aplicativos móveis](functions-bindings-mobile-apps.md).</span><span class="sxs-lookup"><span data-stu-id="c7326-108">toohave your function process individual CRUD operations in a Mobile Apps table, you should instead use [Mobile Apps bindings](functions-bindings-mobile-apps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7326-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c7326-109">Prerequisites</span></span>

+ <span data-ttu-id="c7326-110">Este tópico usa uma função disparada por temporizador.</span><span class="sxs-lookup"><span data-stu-id="c7326-110">This topic uses a timer triggered function.</span></span> <span data-ttu-id="c7326-111">Olá concluir etapas no tópico Olá [criar uma função no Azure que é disparado por um timer](functions-create-scheduled-function.md) toocreate c# versão dessa função.</span><span class="sxs-lookup"><span data-stu-id="c7326-111">Complete hello steps in hello topic [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md) toocreate a C# version of this function.</span></span>   

+ <span data-ttu-id="c7326-112">Este tópico demonstra o comando Transact-SQL que executa uma operação de limpeza em massa em Olá **SalesOrderHeader** tabela no banco de dados do exemplo hello AdventureWorksLT.</span><span class="sxs-lookup"><span data-stu-id="c7326-112">This topic demonstrates a Transact-SQL command that executes a bulk cleanup operation in hello **SalesOrderHeader** table in hello AdventureWorksLT sample database.</span></span> <span data-ttu-id="c7326-113">toocreate Olá AdventureWorksLT de dados de exemplo, Olá completa etapas no tópico Olá [criar um banco de dados do SQL Azure no portal do Azure de saudação](../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c7326-113">toocreate hello AdventureWorksLT sample database, complete hello steps in hello topic [Create an Azure SQL database in hello Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span> 

## <a name="get-connection-information"></a><span data-ttu-id="c7326-114">Obter informações de conexão</span><span class="sxs-lookup"><span data-stu-id="c7326-114">Get connection information</span></span>

<span data-ttu-id="c7326-115">Você precisa de cadeia de caracteres de conexão do tooget Olá para banco de dados de saudação criado quando você concluir a [criar um banco de dados do SQL Azure no portal do Azure de saudação](../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c7326-115">You need tooget hello connection string for hello database you created when you completed [Create an Azure SQL database in hello Azure portal](../sql-database/sql-database-get-started-portal.md).</span></span>

1. <span data-ttu-id="c7326-116">Faça logon no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c7326-116">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
 
3. <span data-ttu-id="c7326-117">Selecione **bancos de dados SQL** no menu esquerdo do hello e selecione o banco de dados no hello **bancos de dados SQL** página.</span><span class="sxs-lookup"><span data-stu-id="c7326-117">Select **SQL Databases** from hello left-hand menu, and select your database on hello **SQL databases** page.</span></span>

4. <span data-ttu-id="c7326-118">Selecione **Mostrar cadeias de conexão de banco de dados** e cópia hello completa **ADO.NET** cadeia de caracteres de conexão.</span><span class="sxs-lookup"><span data-stu-id="c7326-118">Select **Show database connection strings** and copy hello complete **ADO.NET** connection string.</span></span>

    ![Copie a cadeia de conexão ADO.NET hello.](./media/functions-scenario-database-table-cleanup/adonet-connection-string.png)

## <a name="set-hello-connection-string"></a><span data-ttu-id="c7326-120">Cadeia de caracteres de conexão do conjunto Olá</span><span class="sxs-lookup"><span data-stu-id="c7326-120">Set hello connection string</span></span> 

<span data-ttu-id="c7326-121">Um aplicativo de função hospeda execução Olá das funções no Azure.</span><span class="sxs-lookup"><span data-stu-id="c7326-121">A function app hosts hello execution of your functions in Azure.</span></span> <span data-ttu-id="c7326-122">É um cadeias de caracteres de conexão de toostore práticas recomendadas e outros segredos em suas configurações de aplicativo de função.</span><span class="sxs-lookup"><span data-stu-id="c7326-122">It is a best practice toostore connection strings and other secrets in your function app settings.</span></span> <span data-ttu-id="c7326-123">Usando configurações do aplicativo impede a divulgação acidental de cadeia de caracteres de conexão de saudação com seu código.</span><span class="sxs-lookup"><span data-stu-id="c7326-123">Using application settings prevents accidental disclosure of hello connection string with your code.</span></span> 

1. <span data-ttu-id="c7326-124">Navegue tooyour função aplicativo que você criou [criar uma função no Azure que é disparado por um timer](functions-create-scheduled-function.md).</span><span class="sxs-lookup"><span data-stu-id="c7326-124">Navigate tooyour function app you created [Create a function in Azure that is triggered by a timer](functions-create-scheduled-function.md).</span></span>

2. <span data-ttu-id="c7326-125">Selecione **Recursos da plataforma** > **Configurações de aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="c7326-125">Select **Platform features** > **Application settings**.</span></span>
   
    ![Configurações do aplicativo para o aplicativo de função hello.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings.png)

2. <span data-ttu-id="c7326-127">Role para baixo demais**cadeias de caracteres de Conexão** e adicionar uma cadeia de caracteres de conexão usando as configurações de saudação conforme especificado na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7326-127">Scroll down too**Connection strings** and add a connection string using hello settings as specified in hello table.</span></span>
   
    ![Adicione configurações de aplicativo de função de toohello uma conexão cadeia de caracteres.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings-connection-strings.png)

    | <span data-ttu-id="c7326-129">Configuração</span><span class="sxs-lookup"><span data-stu-id="c7326-129">Setting</span></span>       | <span data-ttu-id="c7326-130">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="c7326-130">Suggested value</span></span> | <span data-ttu-id="c7326-131">Descrição</span><span class="sxs-lookup"><span data-stu-id="c7326-131">Description</span></span>             | 
    | ------------ | ------------------ | --------------------- | 
    | <span data-ttu-id="c7326-132">**Nome**</span><span class="sxs-lookup"><span data-stu-id="c7326-132">**Name**</span></span>  |  <span data-ttu-id="c7326-133">sqldb_connection</span><span class="sxs-lookup"><span data-stu-id="c7326-133">sqldb_connection</span></span>  | <span data-ttu-id="c7326-134">Olá tooaccess usado armazenados cadeia de caracteres de conexão em seu código de função.</span><span class="sxs-lookup"><span data-stu-id="c7326-134">Used tooaccess hello stored connection string in your function code.</span></span>    |
    | <span data-ttu-id="c7326-135">**Valor**</span><span class="sxs-lookup"><span data-stu-id="c7326-135">**Value**</span></span> | <span data-ttu-id="c7326-136">Cadeia de caracteres copiada</span><span class="sxs-lookup"><span data-stu-id="c7326-136">Copied string</span></span>  | <span data-ttu-id="c7326-137">Após a cadeia de caracteres de conexão de saudação que você copiou na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="c7326-137">Past hello connection string you copied in hello previous section.</span></span> |
    | <span data-ttu-id="c7326-138">**Tipo**</span><span class="sxs-lookup"><span data-stu-id="c7326-138">**Type**</span></span> | <span data-ttu-id="c7326-139">Banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="c7326-139">SQL Database</span></span> | <span data-ttu-id="c7326-140">Use a conexão de banco de dados SQL do saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="c7326-140">Use hello default SQL Database connection.</span></span> |   

3. <span data-ttu-id="c7326-141">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="c7326-141">Click **Save**.</span></span>

<span data-ttu-id="c7326-142">Agora, você pode adicionar Olá função código c# que se conecta tooyour banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="c7326-142">Now, you can add hello C# function code that connects tooyour SQL Database.</span></span>

## <a name="update-your-function-code"></a><span data-ttu-id="c7326-143">Atualizar o código de função</span><span class="sxs-lookup"><span data-stu-id="c7326-143">Update your function code</span></span>

1. <span data-ttu-id="c7326-144">Em seu aplicativo de função, selecione a função de timer disparada de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7326-144">In your function app, select hello timer-triggered function.</span></span>
 
3. <span data-ttu-id="c7326-145">Adicione Olá referências de assembly na parte superior de saudação do código de função existente Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7326-145">Add hello following assembly references at hello top of hello existing function code:</span></span>

    ```cs
    #r "System.Configuration"
    #r "System.Data"
    ```

3. <span data-ttu-id="c7326-146">Adicione o seguinte Olá `using` função toohello de instruções:</span><span class="sxs-lookup"><span data-stu-id="c7326-146">Add hello following `using` statements toohello function:</span></span>
    ```cs
    using System.Configuration;
    using System.Data.SqlClient;
    using System.Threading.Tasks;
    ```

4. <span data-ttu-id="c7326-147">Substituir saudação **executar** função com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7326-147">Replace hello existing **Run** function with hello following code:</span></span>
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
                // Execute hello command and log hello # rows affected.
                var rows = await cmd.ExecuteNonQueryAsync();
                log.Info($"{rows} rows were updated");
            }
        }
    }
    ```

    <span data-ttu-id="c7326-148">Este comando de exemplo atualiza Olá **Status** coluna com base na data de envio de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7326-148">This sample command updates hello **Status** column based on hello ship date.</span></span> <span data-ttu-id="c7326-149">Ele deve atualizar 32 linhas de dados.</span><span class="sxs-lookup"><span data-stu-id="c7326-149">It should update 32 rows of data.</span></span>

5. <span data-ttu-id="c7326-150">Clique em **salvar**, Olá inspecionar **Logs** windows para Olá execução de função, em seguida, observe Olá número de linhas atualizadas na Olá **SalesOrderHeader** tabela.</span><span class="sxs-lookup"><span data-stu-id="c7326-150">Click **Save**, watch hello **Logs** windows for hello next function execution, then note hello number of rows updated in hello **SalesOrderHeader** table.</span></span>

    ![Exibir logs de função hello.](./media/functions-scenario-database-table-cleanup/functions-logs.png)

## <a name="next-steps"></a><span data-ttu-id="c7326-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c7326-152">Next steps</span></span>

<span data-ttu-id="c7326-153">Em seguida, Aprenda como toouse funciona com aplicativos lógicos toointegrate com outros serviços.</span><span class="sxs-lookup"><span data-stu-id="c7326-153">Next, learn how toouse Functions with Logic Apps toointegrate with other services.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="c7326-154">Criar uma função que se integra nos Aplicativos Lógicos</span><span class="sxs-lookup"><span data-stu-id="c7326-154">Create a function that integrates with Logic Apps</span></span>](functions-twitter-email.md)

<span data-ttu-id="c7326-155">Para obter mais informações sobre funções, consulte Olá seguintes tópicos:</span><span class="sxs-lookup"><span data-stu-id="c7326-155">For more information about Functions, see hello following topics:</span></span>

* [<span data-ttu-id="c7326-156">Referência do desenvolvedor do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="c7326-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  <span data-ttu-id="c7326-157">Referência do programador para codificação de funções e definição de gatilhos e de associações.</span><span class="sxs-lookup"><span data-stu-id="c7326-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="c7326-158">Testando o Azure Functions</span><span class="sxs-lookup"><span data-stu-id="c7326-158">Testing Azure Functions</span></span>](functions-test-a-function.md)  
  <span data-ttu-id="c7326-159">Descreve várias ferramentas e técnicas para testar suas funções.</span><span class="sxs-lookup"><span data-stu-id="c7326-159">Describes various tools and techniques for testing your functions.</span></span>  
