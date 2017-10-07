---
title: AAA "Azure Analysis Services Adventure Works Tutorial | Microsoft Docs"
description: "Apresenta um tutorial do Adventure Works Olá para o Azure Analysis Services"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 06/01/2017
ms.author: owend
ms.openlocfilehash: 2df8b3ab4e8c4ffbe0086418d60fd2e2abd35e7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-analysis-services---adventure-works-tutorial"></a>Azure Analysis Services – tutorial da Adventure Works

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Este tutorial fornece lições sobre como toocreate e implantar um modelo de tabela no nível de compatibilidade Olá 1400 usando [SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).  

Se você estiver novos serviços tooAnalysis e modelagem de tabela, concluir este tutorial é toolearn de maneira mais rápida de saudação como toocreate e implantar um modelo de tabela básico. Quando tiver Olá pré-requisitos no local, ele deve levar entre dois toocomplete de horas toothree.  
  
## <a name="what-you-learn"></a>O que você aprenderá   
  
-   Como toocreate um novo modelo tabular do projeto em Olá **o nível de compatibilidade 1400** no SSDT.
  
-   Como tooimport dados de um banco de dados relacional em um projeto de modelo de tabela.  
  
-   Como toocreate e gerenciar relações entre tabelas no modelo de saudação.  
  
-   Como toocreate calculada colunas, medidas e indicadores chave de desempenho que ajudam os usuários analisam métricas comerciais críticas.  
  
-   Como toocreate e gerenciar perspectivas e hierarquias que ajudam os usuários mais facilmente procurar dados de modelo, fornecendo pontos de vista específicos do aplicativo e de negócios.  
  
-   Como toocreate as partições que dividem dados de tabela em partes lógicas menores que podem ser processadas de forma independente de outras partições.  
  
-   Como toosecure modelo de objetos e dados criando funções com membros de usuário.  
  
-   Como toodeploy um modelo de tabela tooan **Azure Analysis Services** servidor ou um servidor do SQL Server de 2017 Analysis Services local.  
  
## <a name="prerequisites"></a>Pré-requisitos  
toocomplete neste tutorial, você precisa:  
  
-   Um Azure Analysis Services ou o Analysis Services do SQL Server de 2017 instância toodeploy seu modelo. Inscreva-se para uma [avaliação gratuita do Azure Analysis Services](https://azure.microsoft.com/services/analysis-services/) e [crie um servidor](../analysis-services-create-server.md). Ou então, inscreva-se e baixe o [SQL Server 2017 Community Technology Preview](https://www.microsoft.com/evalcenter/evaluate-sql-server-vnext-ctp). 

-   Um Data Warehouse do SQL Server ou o Azure SQL Data Warehouse com hello [banco de dados de exemplo AdventureWorksDW2014](http://go.microsoft.com/fwlink/?LinkID=335807). Este banco de dados de exemplo inclui Olá dados necessário toocomplete neste tutorial. Baixe as [edições gratuitas do SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads). Ou então, inscreva-se para uma [avaliação gratuita do Banco de Dados SQL do Azure](https://azure.microsoft.com/services/sql-database/). 

    **Importante:** se você instalar o banco de dados de exemplo hello em um SQL Server local e implantar o servidor do modelo tooan Azure Analysis Services, uma [gateway de dados no local](../analysis-services-gateway.md) é necessária.

-   versão mais recente de saudação do [SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).

-   versão mais recente de saudação do [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).    

-   Um aplicativo cliente como [Power BI Desktop](https://powerbi.microsoft.com/desktop/) ou Excel. 

## <a name="scenario"></a>Cenário  
Esse tutorial se baseia na Adventure Works Cycles, uma empresa fictícia. A Adventure Works é uma empresa de fabricação grande, empresa multinacional que produz e distribui Bicicletas, peças e mercados de toocommercial Acessórios na América do Norte, Europa e Ásia. Olá emprega 500 funcionários. Além disso, a Adventure Works emprega várias equipes regionais de vendas em toda a sua base de mercado. O projeto está toocreate um modelo de tabela para os usuários de vendas e marketing tooanalyze dados de vendas pela Internet no banco de dados do hello AdventureWorksDW.  
  
tutorial de saudação toocomplete, você deve concluir várias lições. Em cada lição, há tarefas. Conclusão de cada tarefa na ordem é necessária para concluir a lição hello. Embora em uma lição específica possam existir várias tarefas que geram um resultado semelhante, o modo como você conclui cada tarefa é ligeiramente diferente. Esse método mostra normalmente, há mais de uma maneira toocomplete uma tarefa e toochallenge você usar as habilidades você aprendeu em tarefas e lições anteriores.  
  
Olá finalidade lições Olá é tooguide você pelo processo de criação de um modelo de tabela básico usando muitos dos recursos de saudação incluído no SSDT. Porque cada lição é criada na lição anterior Olá, você deve concluir as lições Olá na ordem.
  
Este tutorial não fornece lições sobre como gerenciar um servidor no portal do Azure, gerenciar um servidor ou banco de dados usando o SSMS, ou usando um cliente de dados de modelo do aplicativo toobrowse. 


## <a name="lessons"></a>Lições  
Este tutorial inclui Olá lições a seguir:  
  
|Lição|Tempo estimado toocomplete|  
|----------|------------------------------|  
|[1 - Criar um novo projeto de modelo tabular](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md)|10 minutos|  
|[2 - Obter dados](../tutorials/aas-lesson-2-get-data.md)|10 minutos|  
|[3 - Marcar como tabela de data](../tutorials/aas-lesson-3-mark-as-date-table.md)|3 minutos|  
|[4 - Criar relações](../tutorials/aas-lesson-4-create-relationships.md)|10 minutos|  
|[5 - Criar colunas calculadas](../tutorials/aas-lesson-5-create-calculated-columns.md)|15 minutos|
|[6 - Criar medidas](../tutorials/aas-lesson-6-create-measures.md)|30 minutos|  
|[7 - Criar KPIs (indicadores chave de desempenho)](../tutorials/aas-lesson-7-create-key-performance-indicators.md)|15 minutos|  
|[8 - Criar perspectivas](../tutorials/aas-lesson-8-create-perspectives.md)|5 minutos|  
|[9 - Criar hierarquias](../tutorials/aas-lesson-9-create-hierarchies.md)|20 minutos|  
|[10 - Criar partições](../tutorials/aas-lesson-10-create-partitions.md)|15 minutos|  
|[11 - Criar funções](../tutorials/aas-lesson-11-create-roles.md)|15 minutos|  
|[12 - Analisar no Excel](../tutorials/aas-lesson-12-analyze-in-excel.md)|5 minutos| 
|[13 - Implantar](../tutorials/aas-lesson-13-deploy.md)|5 minutos|  
  
## <a name="supplemental-lessons"></a>Lições suplementares  
Nestas lições não são tutorial de saudação toocomplete necessária, mas podem ser útil para melhor compreensão advanced criação de modelo tabular recursos.  
  
|Lição|Tempo estimado toocomplete|  
|----------|------------------------------|  
|[Linhas de Detalhes](../tutorials/aas-supplemental-lesson-detail-rows.md)|10 minutos|
|[Segurança dinâmica](../tutorials/aas-supplemental-lesson-dynamic-security.md)|30 minutos|
|[Hierarquias desbalanceadas](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)|20 minutos| 

  
## <a name="next-steps"></a>Próximas etapas  
tooget iniciado, consulte [lição 1: criar um novo projeto de modelo de tabela](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).  
  
  
  

