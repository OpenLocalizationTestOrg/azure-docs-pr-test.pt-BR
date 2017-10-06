---
título: aaa "lição do tutorial do Azure Analysis Services 9: criar hierarquias | Descrição de Microsoft Docs": serviços: documentationcenter do analysis services: ' autor: manager minewiskan: erikre editor: ' marcas: '

MS. AssetID: MS. Service: MS. devlang do analysis services: NA MS. Topic: get-started-article tgt_pltfrm: NA Workload: MS. Date na: 26/05/2017 Author: owend
---
# <a name="lesson-9-create-hierarchies"></a>Lição 9: criar hierarquias

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Nesta lição, você cria hierarquias. As hierarquias são grupos de colunas organizados em níveis. Por exemplo, uma hierarquia de Geografia pode ter subníveis para País, Estado, Região e Cidade. Hierarquias podem parecer separadas de outras colunas em uma lista de campos de aplicativo cliente relatório, tornando mais fácil para o cliente toonavigate usuários e incluir em um relatório. toolearn mais, consulte [hierarquias](https://docs.microsoft.com/sql/analysis-services/tabular-models/hierarchies-ssas-tabular)
  
hierarquias toocreate, use o designer de modelo Olá no *exibição de diagrama*. Não há suporte para criar e gerenciar hierarquias na Exibição de Dados.  
  
Estimado tempo toocomplete nesta lição: **20 minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem. Antes de executar tarefas de saudação nesta lição, você deverá ter completado lição anterior Olá: [lição 8: criar perspectivas](../tutorials/aas-lesson-8-create-perspectives.md).  
  
## <a name="create-hierarchies"></a>Criar hierarquias  
  
#### <a name="toocreate-a-category-hierarchy-in-hello-dimproduct-table"></a>uma hierarquia de categoria na tabela DimProduct de saudação do toocreate  
  
1.  No designer de modelo da saudação (modo de exibição de diagrama), clique com botão direito Olá **DimProduct** tabela > **criar hierarquia**. Uma nova hierarquia aparece na parte inferior da saudação da janela de tabela de saudação. Renomear hierarquia Olá **categoria**.  
  
2.  Clique e arraste Olá **ProductCategoryName** toohello de coluna nova **categoria** hierarquia.  
  
3.  Em Olá **categoria** hierarquia, Olá atalho **ProductCategoryName** > **Renomear**e, em seguida, digite **categoria**.  
  
    > [!NOTE]  
    > Renomear uma coluna em uma hierarquia não renomeia essa coluna na tabela de saudação. Uma coluna em uma hierarquia é apenas uma representação de coluna Olá na tabela de saudação.  
  
4.  Clique e arraste Olá **ProductSubcategoryName** coluna toohello **categoria** hierarquia. Renomeie-a como **Subcategoria**. 
  
5.  Saudação de atalho **ModelName** coluna > **adicionar toohierarchy**e, em seguida, selecione **categoria**. Renomeie-a como **Modelo**.

6.  Finalmente, adicione **EnglishProductName** toohello a hierarquia de categoria. Renomeie-a como **Produto**.  

    ![aas-lesson9-category](../tutorials/media/aas-lesson9-category.png)
  
#### <a name="toocreate-hierarchies-in-hello-dimdate-table"></a>hierarquias de toocreate na tabela DimDate de saudação  
  
1.  Em Olá **DimDate** de tabela, crie uma hierarquia chamada **calendário**.  
  
3.  Adicione Olá colunas na ordem a seguir:

    *  CalendarYear
    *  CalendarSemester
    *  CalendarQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
    
4.  Em Olá **DimDate** de tabela, crie um **Fiscal** hierarquia. Inclua Olá colunas na ordem a seguir:  
  
    *  FiscalYear
    *  FiscalSemester
    *  FiscalQuarter
    *  MonthCalendar
    *  DayNumberOfMonth
  
5.  Por fim, na Olá **DimDate** de tabela, crie um **ProductionCalendar** hierarquia. Inclua Olá colunas na ordem a seguir:  
    *  CalendarYear
    *  WeekNumberOfYear
    *  DayNumberOfWeek
  
 ## <a name="whats-next"></a>O que vem a seguir?
[Lição 10: criar partições](../tutorials/aas-lesson-10-create-partitions.md). 
  
  
