---
title: aaaConnect Excel tooSQL banco de dados | Microsoft Docs
description: "Saiba como o Microsoft Excel de tooconnect tooAzure SQL banco de dados na nuvem hello. Importar dados para o Excel para exploração de dados e geração de relatórios."
services: sql-database
keywords: conectar excel toosql, importar dados tooexcel
documentationcenter: 
author: joseidz
manager: jhubbard
editor: 
ms.assetid: 906924bc-2707-48d3-bac6-397976a0409d
ms.service: sql-database
ms.custom: develop apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: jhubbard
ms.openlocfilehash: 0048849432023145bd1009d45b6d9b64a9c7ac3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-tooan-azure-sql-database-and-create-a-report"></a>Conecte-se o banco de dados do Excel tooan SQL Azure e criar um relatório

Conecte-se o banco de dados do Excel tooa SQL na nuvem hello e importar dados e criar tabelas e gráficos com base nos valores no banco de dados de saudação. Neste tutorial, que você irá configurar a conexão de saudação entre o Excel e uma tabela de banco de dados, salvar arquivo hello que armazena informações de conexão de dados e Olá para Excel e, em seguida, criar um gráfico dinâmico de saudação valores do banco de dados.

Você precisará de um banco de dados SQL no Azure antes de começar. Se você não tiver um, consulte [criar seu primeiro banco de dados do SQL](sql-database-get-started-portal.md) tooget um banco de dados com dados de exemplo em funcionamento em poucos minutos. Neste artigo, você importará dados de exemplo do artigo para o Excel, mas poderá seguir etapas semelhantes em seus próprios dados.

Você também precisará de uma cópia do Excel. Este artigo usa o [Microsoft Excel 2016](https://products.office.com/).

## <a name="connect-excel-tooa-sql-database-and-create-an-odc-file"></a>Conecte-se o banco de dados do Excel tooa SQL e criar um arquivo odc
1. tooconnect Excel tooSQL banco de dados, abra o Excel e, em seguida, criar uma nova pasta de trabalho ou abrir uma pasta de trabalho do Excel existente.
2. Na barra de menus Olá na parte superior de saudação da página Olá clique **dados**, clique em **de outras fontes**e, em seguida, clique em **do SQL Server**.
   
   ![Selecionar fonte de dados: conectar-se o banco de dados do Excel tooSQL.](./media/sql-database-connect-excel/excel_data_source.png)
   
   Olá Assistente de Conexão de dados é aberto.
3. Em Olá **conectar tooDatabase servidor** caixa de diálogo, Olá do tipo banco de dados SQL **nome do servidor** deseja tooconnect tooin Olá formulário <*servername* > **. t**. Por exemplo, **adworkserver.database.windows.net**.
4. Em **credenciais de logon**, clique em **Olá usar nome de usuário e senha a seguir**, Olá tipo **nome de usuário** e **senha** configuradas para Olá o servidor de banco de dados SQL quando você criou e, em seguida, clique em **próximo**.
   
   ![Digite as credenciais de nome e logon do servidor de saudação](./media/sql-database-connect-excel/connect-to-server.png)
   
   > [!TIP]
   > Dependendo do seu ambiente de rede, você pode não ser capaz de tooconnect ou você pode perder a conexão de saudação se o servidor de banco de dados SQL Olá não permitir o tráfego do seu endereço IP do cliente. Vá toohello [portal do Azure](https://portal.azure.com/), clique em servidores SQL, seu servidor, clique em firewall em configurações e adicionar o endereço IP do cliente. Consulte [como configurações de firewall tooconfigure](sql-database-configure-firewall-settings.md) para obter detalhes.
   > 
   > 
5. Em Olá **Selecionar banco de dados e tabela** caixa de diálogo, o banco de dados selecione Olá deseja toowork com lista de saudação e, em seguida, clique em tabelas de saudação ou modos de exibição que você deseja toowork com (escolhemos **vGetAllCategories**) e, em seguida, Clique em **próximo**.
   
    ![Selecione um banco de dados e a tabela.](./media/sql-database-connect-excel/select-database-and-table.png)
   
    Olá **salvar arquivo de Conexão de dados e concluir** caixa de diálogo é aberta, onde você fornece informações sobre arquivo (*. odc) da conexão de banco de dados de Office de hello que usa o Excel. Você pode deixar os padrões de saudação ou personalizar suas seleções.
6. Você pode deixar Olá padrões, mas Olá Observação **nome de arquivo** em particular. Um **descrição**, um **nome amigável**, e **pesquisar palavras-chave** ajudam você e outros usuários Lembre-se de que você está se conectando tooand localizar conexão hello. Clique em **sempre tentar toouse esse arquivo de dados de toorefresh** se você deseja informações de conexão armazenadas no arquivo odc de saudação para que ele possa atualizar quando você conectar tooit e, em seguida, clique em **concluir**.
   
    ![Salvando um arquivo odc](./media/sql-database-connect-excel/save-odc-file.png)
   
    Olá **importar dados** caixa de diálogo é exibida.

## <a name="import-hello-data-into-excel-and-create-a-pivot-chart"></a>Importar dados de saudação no Excel e criar um gráfico dinâmico
Agora que que você estabeleceu conexão hello e arquivo hello criado com informações de conexão e de dados, você está lendo dados de saudação tooimport.

1. Em Olá **importar dados** caixa de diálogo, clique em opção Olá desejada para apresentar os dados na planilha de saudação e, em seguida, clique em **Okey**. Escolhemos **Gráfico Dinâmico**. Você também pode escolher toocreate um **nova planilha** ou muito**adicionar este tooa de dados modelo de dados**. Para obter mais informações sobre os Modelos de Dados, consulte [Criar um modelo de dados no Excel](https://support.office.com/article/Create-a-Data-Model-in-Excel-87E7A54C-87DC-488E-9410-5C75DBCB0F7B). Clique em **propriedades** tooexplore informações sobre o arquivo odc de saudação criado no hello etapa e toochoose opções anteriores para atualizar os dados de saudação.
   
    ![Escolher o formato de saudação para os dados no Excel](./media/sql-database-connect-excel/import-data.png)
   
    planilha de saudação agora tem uma tabela dinâmica vazia e um gráfico.
2. Em **PivotTable Fields**, selecione todos os Olá caixas de seleção para Olá campos que você deseja tooview.
   
    ![Configure o relatório do banco de dados.](./media/sql-database-connect-excel/power-pivot-results.png)

> [!TIP]
> Se quiser tooconnect outros Excel pastas de trabalho e planilhas toohello banco de dados, clique em **dados**, clique em **conexões**, clique em **adicionar**, escolher conexão Olá criado na lista de saudação e depois clique em **abrir**.
> ![Abrir uma conexão a partir de outra pasta de trabalho](./media/sql-database-connect-excel/open-from-another-workbook.png)
> 
> 

## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[conectar tooSQL banco de dados com o SQL Server Management Studio](sql-database-connect-query-ssms.md) avançadas de consulta e análise.
* Saiba mais sobre os benefícios de saudação do [pools Elásticos](sql-database-elastic-pool.md).
* Saiba como muito[criar um aplicativo web que se conecta tooSQL banco de dados back-end Olá](../app-service-web/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).

