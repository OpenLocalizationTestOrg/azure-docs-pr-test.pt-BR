---
title: "aaaCreate um modelo de tabela usando o designer de Web do Azure Analysis Services Olá | Microsoft Docs"
description: "Saiba como toocreate um modelo de tabela do Azure Analysis Services usando Olá Web designer no portal do Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/21/2017
ms.author: owend
ms.openlocfilehash: a37b326b76c84fc3a4300827bc1c8706b0584701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-model-in-azure-portal"></a>Criar um modelo no portal do Azure

recurso do Hello Azure Analysis Services na web designer (visualização) no portal do Azure fornece uma maneira rápida e fácil toocreate e editar modelos de tabela e consulta modelo dados diretamente no seu navegador. 

Tenha em mente, Olá web designer é **visualização**. Enquanto a nova funcionalidade está sendo adicionada tempo Olá todo, na visualização, a funcionalidade é limitada. Para mais avançados modelo teste e desenvolvimento, é melhor toouse Visual Studio (SSDT) e o SQL Server Management Studio (SSMS).

## <a name="prerequisites"></a>Pré-requisitos

- Um servidor do Azure Analysis Services na camada Standard ou o desenvolvedor de saudação. Novos modelos criados usando o designer de Web hello são DirectQuery com suporte apenas essas camadas.
- Um Banco de Dados SQL Azure, Azure SQL Data Warehouse ou arquivo Power BI Desktop (.pbix) como fonte de dados. Novos modelos criados por meio de arquivos Power BI Desktop dão suporte às fontes de dados de Banco de Dados SQL Azure, Azure SQL Data Warehouse, Oracle e Teradata.
- Uma conta do SQL Server e a senha para se conectar a fontes de dados de banco de dados SQL ou do Azure SQL Data Warehouse tooAzure.

## <a name="toocreate-a-new-tabular-model"></a>toocreate um novo modelo de tabela

1. Na folha **Visão geral** > **Designer de Web** do seu servidor, clique em **Abrir**.

    ![Criar um modelo no portal do Azure](./media/analysis-services-create-model-portal/aas-create-portal-overview-wd.png)

2. Em **Designer de Web** > **Modelos**, clique em **+ Adicionar**.

    ![Criar um modelo no portal do Azure](./media/analysis-services-create-model-portal/aas-create-portal-models.png)

3. Em **Novo modelo**, digite um nome de modelo e, em seguida, selecione uma fonte de dados.

    ![Caixa de diálogo Novo modelo no portal do Azure](./media/analysis-services-create-model-portal/aas-create-portal-new-model.png)

4. Em **conectar**, insira as propriedades de conexão de saudação. Nome de usuário e senha devem ser uma conta do SQL Server.

     ![Caixa de diálogo Conectar no portal do Azure](./media/analysis-services-create-model-portal/aas-create-portal-connect.png)

5. Em **tabelas e exibições**, selecione Olá tooinclude de tabelas em seu modelo e, em seguida, clique em **criar**. São criadas automaticamente relações entre tabelas com um par de chaves.

     ![Selecionar tabelas e exibições](./media/analysis-services-create-model-portal/aas-create-portal-tables.png)

O novo modelo é exibido no navegador. A partir daqui, você pode:   

- Dados de modelo de consulta arrastando o designer de consulta toohello campos e adicionar filtros.
- Crie novas medidas nas tabelas.
- Edite metadados do modelo usando o editor de json hello.
- Abra o modelo de saudação no Visual Studio (SSDT), o Power BI Desktop ou o Excel.

![Selecionar tabelas e exibições](./media/analysis-services-create-model-portal/aas-create-portal-query.png)

> [!NOTE]
> Quando você editar os metadados de modelo ou cria novas medidas em seu navegador, você está salvando modelo de tooyour essas alterações no Azure. Se você também estiver trabalhando em seu modelo no SSDT, Power BI Desktop ou Excel, o modelo pode ficar fora de sincronia.


## <a name="next-steps"></a>Próximas etapas 
[Gerenciar usuários e funções de banco de dados](analysis-services-database-users.md)  
[Conectar com o Excel](analysis-services-connect-excel.md)  


