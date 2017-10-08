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
# <a name="use-azure-functions-tooconnect-tooan-azure-sql-database"></a>Use as funções do Azure tooconnect tooan banco de dados do SQL Azure
Este tópico mostra como toouse funções do Azure toocreate agendado do trabalho que limpa a linhas em uma tabela em um banco de dados do SQL Azure. Olá nova função c# é criada com base em um modelo de gatilho de timer predefinidos Olá portal do Azure. toosupport neste cenário, você também deve definir uma cadeia de caracteres de conexão do banco de dados como uma configuração de aplicativo de função hello. Esse cenário usa uma operação em massa no banco de dados de saudação. toohave sua função processo CRUD operações individuais em uma tabela de aplicativos móveis, você deve usar [associações de aplicativos móveis](functions-bindings-mobile-apps.md).

## <a name="prerequisites"></a>Pré-requisitos

+ Este tópico usa uma função disparada por temporizador. Olá concluir etapas no tópico Olá [criar uma função no Azure que é disparado por um timer](functions-create-scheduled-function.md) toocreate c# versão dessa função.   

+ Este tópico demonstra o comando Transact-SQL que executa uma operação de limpeza em massa em Olá **SalesOrderHeader** tabela no banco de dados do exemplo hello AdventureWorksLT. toocreate Olá AdventureWorksLT de dados de exemplo, Olá completa etapas no tópico Olá [criar um banco de dados do SQL Azure no portal do Azure de saudação](../sql-database/sql-database-get-started-portal.md). 

## <a name="get-connection-information"></a>Obter informações de conexão

Você precisa de cadeia de caracteres de conexão do tooget Olá para banco de dados de saudação criado quando você concluir a [criar um banco de dados do SQL Azure no portal do Azure de saudação](../sql-database/sql-database-get-started-portal.md).

1. Faça logon no toohello [portal do Azure](https://portal.azure.com/).
 
3. Selecione **bancos de dados SQL** no menu esquerdo do hello e selecione o banco de dados no hello **bancos de dados SQL** página.

4. Selecione **Mostrar cadeias de conexão de banco de dados** e cópia hello completa **ADO.NET** cadeia de caracteres de conexão.

    ![Copie a cadeia de conexão ADO.NET hello.](./media/functions-scenario-database-table-cleanup/adonet-connection-string.png)

## <a name="set-hello-connection-string"></a>Cadeia de caracteres de conexão do conjunto Olá 

Um aplicativo de função hospeda execução Olá das funções no Azure. É um cadeias de caracteres de conexão de toostore práticas recomendadas e outros segredos em suas configurações de aplicativo de função. Usando configurações do aplicativo impede a divulgação acidental de cadeia de caracteres de conexão de saudação com seu código. 

1. Navegue tooyour função aplicativo que você criou [criar uma função no Azure que é disparado por um timer](functions-create-scheduled-function.md).

2. Selecione **Recursos da plataforma** > **Configurações de aplicativo**.
   
    ![Configurações do aplicativo para o aplicativo de função hello.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings.png)

2. Role para baixo demais**cadeias de caracteres de Conexão** e adicionar uma cadeia de caracteres de conexão usando as configurações de saudação conforme especificado na tabela de saudação.
   
    ![Adicione configurações de aplicativo de função de toohello uma conexão cadeia de caracteres.](./media/functions-scenario-database-table-cleanup/functions-app-service-settings-connection-strings.png)

    | Configuração       | Valor sugerido | Descrição             | 
    | ------------ | ------------------ | --------------------- | 
    | **Nome**  |  sqldb_connection  | Olá tooaccess usado armazenados cadeia de caracteres de conexão em seu código de função.    |
    | **Valor** | Cadeia de caracteres copiada  | Após a cadeia de caracteres de conexão de saudação que você copiou na seção anterior hello. |
    | **Tipo** | Banco de dados SQL | Use a conexão de banco de dados SQL do saudação padrão. |   

3. Clique em **Salvar**.

Agora, você pode adicionar Olá função código c# que se conecta tooyour banco de dados SQL.

## <a name="update-your-function-code"></a>Atualizar o código de função

1. Em seu aplicativo de função, selecione a função de timer disparada de saudação.
 
3. Adicione Olá referências de assembly na parte superior de saudação do código de função existente Olá a seguir:

    ```cs
    #r "System.Configuration"
    #r "System.Data"
    ```

3. Adicione o seguinte Olá `using` função toohello de instruções:
    ```cs
    using System.Configuration;
    using System.Data.SqlClient;
    using System.Threading.Tasks;
    ```

4. Substituir saudação **executar** função com hello código a seguir:
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

    Este comando de exemplo atualiza Olá **Status** coluna com base na data de envio de saudação. Ele deve atualizar 32 linhas de dados.

5. Clique em **salvar**, Olá inspecionar **Logs** windows para Olá execução de função, em seguida, observe Olá número de linhas atualizadas na Olá **SalesOrderHeader** tabela.

    ![Exibir logs de função hello.](./media/functions-scenario-database-table-cleanup/functions-logs.png)

## <a name="next-steps"></a>Próximas etapas

Em seguida, Aprenda como toouse funciona com aplicativos lógicos toointegrate com outros serviços.

> [!div class="nextstepaction"] 
> [Criar uma função que se integra nos Aplicativos Lógicos](functions-twitter-email.md)

Para obter mais informações sobre funções, consulte Olá seguintes tópicos:

* [Referência do desenvolvedor do Azure Functions](functions-reference.md)  
  Referência do programador para codificação de funções e definição de gatilhos e de associações.
* [Testando o Azure Functions](functions-test-a-function.md)  
  Descreve várias ferramentas e técnicas para testar suas funções.  
