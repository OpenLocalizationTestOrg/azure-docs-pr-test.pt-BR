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
# <a name="get-started-with-hello-azure-sql-database-connector"></a>Introdução ao conector do Azure SQL Database Olá
Usando o conector do Azure SQL Database hello, crie fluxos de trabalho para a sua organização que gerenciam dados nas tabelas. 

Com o Banco de Dados SQL, você:

* Crie o fluxo de trabalho adicionando um novo cliente tooa clientes banco de dados, ou atualizando um pedido em um banco de dados de pedidos.
* Use ações tooget uma linha de dados, inserir uma nova linha e até mesmo excluir. Por exemplo, quando um registro é criado no Dynamics CRM Online (um gatilho), insira uma linha em um Banco de Dados SQL do Azure (uma ação). 

Este tópico mostra como toouse Olá conector de banco de dados SQL em um aplicativo lógico e também lista Olá ações.

toolearn mais sobre aplicativos lógicos, consulte [quais são os aplicativos lógicos](../logic-apps/logic-apps-what-are-logic-apps.md) e [criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-tooazure-sql-database"></a>Conecte-se tooAzure banco de dados SQL
Antes de sua lógica de aplicativo pode acessar qualquer serviço, você primeiro crie um *conexão* toohello service. Uma conexão fornece uma conectividade entre um aplicativo lógico e outro serviço. Por exemplo, tooconnect tooSQL banco de dados, você primeiro crie um banco de dados SQL *conexão*. toocreate uma conexão, em que você insira as credenciais de saudação que você normalmente usa o serviço de saudação tooaccess que você está se conectando. Portanto, no banco de dados SQL, insira sua conexão do banco de dados SQL credenciais toocreate hello. 

#### <a name="create-hello-connection"></a>Criar conexão Olá
> [!INCLUDE [Create hello connection tooSQL Azure](../../includes/connectors-create-api-sqlazure.md)]
> 
> 

## <a name="use-a-trigger"></a>Usar um gatilho
Esse conector não tem gatilhos. Use outros gatilhos toostart Olá lógica aplicativo, como um disparador de recorrência, um gatilho de HTTP Webhook, disparadores disponíveis com outros conectores e muito mais. [Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md) fornece um exemplo.

## <a name="use-an-action"></a>Usar uma ação
Uma ação é uma operação executada pelo fluxo de trabalho Olá definido em um aplicativo lógico. [Saiba mais sobre ações](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

1. Selecione o sinal de adição hello. Consulte várias opções: **adicionar uma ação**, **adicionar uma condição**, ou uma saudação **mais** opções.
   
    ![](./media/connectors-create-api-sqlazure/add-action.png)
2. Escolha **Adicionar uma ação**.
3. Na caixa de texto de saudação, digite "sql" tooget uma lista de todas as ações disponíveis de saudação.
   
    ![](./media/connectors-create-api-sqlazure/sql-1.png) 
4. Em nosso exemplo, escolha **SQL Server – obter linha**. Se uma conexão já existir, selecione Olá **nome de tabela** Olá suspenso lista e digite Olá **ID da linha** deseja tooreturn.
   
    ![](./media/connectors-create-api-sqlazure/sample-table.png)
   
    Se você for solicitado para obter informações de conexão do hello, digite conexão de Olá Olá detalhes toocreate. [Criar conexão Olá](connectors-create-api-sqlazure.md#create-the-connection) neste tópico descreve essas propriedades. 
   
   > [!NOTE]
   > Nesse exemplo, retornamos uma linha de uma tabela. dados de saudação toosee nessa linha, adicione outra ação que cria um arquivo usando Olá campos da tabela de saudação. Por exemplo, adicione uma ação de OneDrive que usa hello FirstName e LastName campos toocreate um novo arquivo na conta de armazenamento de nuvem hello. 
   > 
   > 
5. **Salvar** as alterações (canto superior esquerdo da barra de ferramentas de saudação). Seu aplicativo lógico é salvo e pode ser habilitado automaticamente.

## <a name="connector-specific-details"></a>Detalhes específicos do conector

Exibir quaisquer gatilhos e ações definidas em swagger Olá e também os limites de saudação [detalhes conector](/connectors/sql/). 

## <a name="next-steps"></a>Próximas etapas
[Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md). Explorar Olá outros conectores disponíveis na lógica de aplicativos no nosso [lista APIs](apis-list.md).

