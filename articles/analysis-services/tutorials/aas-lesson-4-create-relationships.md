---
título: aaa "lição do tutorial do Azure Analysis Services 4: criar relações | Descrição de Microsoft Docs": descreve como toocreate relações em Olá projeto do tutorial do Azure Analysis Services. serviços: documentationcenter do analysis services: ' autor: manager minewiskan: erikre editor: ' marcas: '

MS. AssetID: MS. Service: MS. devlang do analysis services: NA MS. Topic: get-started-article tgt_pltfrm: NA Workload: MS. Date na: 26/05/2017 Author: owend
---
# <a name="lesson-4-create-relationships"></a>Lição 4: criar relações

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Nesta lição, você verificar as relações de saudação que foram criadas automaticamente quando você importou os dados e adicionar novas relações entre tabelas diferentes. Uma relação é uma conexão entre duas tabelas que estabelece como os dados de saudação nessas tabelas devem ser correlacionados. Por exemplo, tabelas de DimProduct hello e Olá DimProductSubcategory têm uma relação com base no fato de saudação que cada produto pertence tooa subcategoria. mais, consulte toolearn [relações](https://docs.microsoft.com/sql/analysis-services/tabular-models/relationships-ssas-tabular).
  
Estimado tempo toocomplete nesta lição: **10 minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem. Antes de executar tarefas de saudação nesta lição, você deverá ter completado lição anterior Olá: [lição 3: marcar como tabela de data](../tutorials/aas-lesson-3-mark-as-date-table.md). 
  
## <a name="review-existing-relationships-and-add-new-relationships"></a>Examinar relações existentes e adicionar novas relações  
Quando você importar dados usando obter dados, você tem sete tabelas do banco de dados de AdventureWorksDW2014 hello. Em geral, quando você importa dados de uma fonte relacional, as relações existentes são importadas automaticamente junto com dados de saudação. No entanto, antes de prosseguir com a criação de seu modelo, você deve verificar se essas relações entre tabelas foram criadas corretamente. Para este tutorial, você também adicionará três novas relações.  
  
#### <a name="tooreview-existing-relationships"></a>tooreview as relações existentes  
  
1.  Clique em Olá **modelo** menu > **exibição do modelo de** > **exibição de diagrama**.  

    Olá designer de modelo agora aparece no modo de exibição de diagrama, um formato gráfico que exibe todas as tabelas de saudação que você importou com linhas entre elas. linhas de saudação entre tabelas indicam relações Olá que foram criadas automaticamente quando você importou dados saudação.
    
    ![aas-lesson4-diagram](../tutorials/media/aas-lesson4-diagram.png)
  
    Inclua como muitas das tabelas de saudação possível por meio de controles de minimapa no canto inferior direito de saudação do designer de modelo de saudação. Clique e arraste locais de toodifferent de tabelas, reunindo tabelas mais próximo ou colocá-los em uma ordem específica. Movendo tabelas não afeta relações Olá já existentes entre tabelas de saudação. tooview todas as colunas de saudação em uma tabela específica, clique e arraste um tooexpand de borda da tabela ou diminuí-lo.  
  
2.  Clique em uma linha sólida entre Olá Olá **DimCustomer** tabela e hello **DimGeography** tabela. uma linha sólida entre essas duas tabelas Olá mostra que essa relação está ativa, ou seja, que ele é usado por padrão quando o cálculo das fórmulas DAX.  
  
    Saudação de aviso **GeographyKey** coluna Olá **DimCustomer** tabela e hello **GeographyKey** coluna Olá **DimGeography** tabela agora aparecem cada dentro de uma caixa. Essas colunas são usadas na relação de saudação. Olá propriedades da relação agora também aparecem nas Olá **propriedades** janela.  
  
    > [!TIP]  
    > Além disso toousing Olá designer de modelo na exibição de diagrama, você também pode usar o hello gerenciar relações diálogo caixa tooshow Olá relações entre todas as tabelas em um formato de tabela. No Gerenciador de Modelos tabulares, clique com o botão direito do mouse em **Relações** > **Gerenciar Relações**.
  
3.  Verifique se Olá relações a seguir foram criada quando cada uma das tabelas de saudação foram importados do banco de dados do AdventureWorksDW hello:  
  
    |Ativo|Tabela|Tabela de Pesquisa Relacionada|  
    |----------|---------|------------------------|  
    |Sim|**DimCustomer [GeographyKey]**|**DimGeography [GeographyKey]**|  
    |Sim|**DimProduct [ProductSubcategoryKey]**|**DimProductSubcategory [ProductSubcategoryKey]**|  
    |Sim|**DimProductSubcategory [ProductCategoryKey]**|**DimProductCategory [ProductCategoryKey]**|  
    |Sim|**FactInternetSales [CustomerKey]**|**DimCustomer [CustomerKey]**|  
    |Sim|**FactInternetSales [ProductKey]**|**DimProduct [ProductKey]**|  
  
    Se alguma das relações Olá estiverem ausentes, verifique se o modelo inclui Olá tabelas a seguir: DimCustomer, DimDate, DimGeography, DimProduct, DimProductCategory, DimProductSubcategory e FactInternetSales. Se tabelas da saudação mesma conexão de fonte de dados são importados em separarem vezes, as relações entre essas tabelas não são criadas e devem ser criadas manualmente.  

### <a name="take-a-closer-look"></a>Veja uma análise mais detalhada
Na exibição de diagrama, observe um número de linhas de saudação que mostram a relação de saudação entre tabelas, um asterisco e uma seta.

![aas-lesson4-line](../tutorials/media/aas-lesson4-line.png)

seta de saudação mostra a direção do filtro hello. asterisco Olá mostra que essa tabela é Olá lado muitos de cardinalidade da relação hello e hello um mostra que esta tabela é um lado de saudação da relação de saudação. Se você precisar tooedit uma relação; Por exemplo, altere a direção do filtro ou a cardinalidade da relação hello, clique duas vezes Olá relação tooopen Olá Editar relação de diálogo linha.

![aas-lesson4-edit](../tutorials/media/aas-lesson4-edit.png)

Esses recursos destinam-se para modelagem de dados avançados e estão fora do escopo Olá neste tutorial. mais, consulte toolearn [bidirecional entre os filtros para modelos de tabela no Analysis Services](https://docs.microsoft.com/sql/analysis-services/tabular-models/bi-directional-cross-filters-tabular-models-analysis-services).

Em alguns casos, talvez seja necessário toocreate de relacionamentos adicionais entre tabelas em seu modelo toosupport determinada lógica de negócios. Para este tutorial, você precisa toocreate três relações adicionais entre tabelas de FactInternetSales hello e Olá DimDate.  
  
#### <a name="tooadd-new-relationships-between-tables"></a>tooadd novas relações entre tabelas  
  
1.  No designer de modelo de saudação em Olá **FactInternetSales** de tabela, clique e mantenha Olá **OrderDate** coluna, em seguida, arraste Olá cursor toohello **data** coluna Olá  **DimDate** da tabela e, em seguida, solte.  

    Uma linha sólida aparece, indicando que você criou uma relação ativa entre hello **OrderDate** coluna Olá **vendas pela Internet** tabela e hello **data** coluna Olá **Data** tabela. 
  
      ![aas-lesson4-new](../tutorials/media/aas-lesson4-new.png) 
  
    > [!NOTE]  
    > Ao criar relações, direção de cardinalidade e filtro Olá entre a tabela primária hello e tabela de pesquisa relacionada Olá é selecionada automaticamente.  
  
2.  Em Olá **FactInternetSales** de tabela, clique e mantenha em Olá **DueDate** coluna, em seguida, arraste Olá cursor toohello **data** coluna Olá **DimDate** da tabela e, em seguida, solte.  
  
    Uma linha pontilhada aparece, mostrando a você criou uma relação inativa entre hello **DueDate** coluna Olá **FactInternetSales** tabela e hello **data** coluna Olá **DimDate** tabela. Você pode ter várias relações entre tabelas, mas somente uma relação pode estar ativa por vez. Relações inativas podem ser feitas agregações especial tooperform ativa em expressões DAX personalizadas.  
  
3.  Por fim, crie mais uma relação. Em Olá **FactInternetSales** de tabela, clique e mantenha em Olá **ShipDate** coluna, em seguida, arraste Olá cursor toohello **data** coluna Olá **DimDate** da tabela e, em seguida, solte.  
    
     ![aas-lesson4-newinactive](../tutorials/media/aas-lesson4-newinactive.png)
  
## <a name="whats-next"></a>O que vem a seguir?
[Lição 5: criar colunas calculadas](../tutorials/aas-lesson-5-create-calculated-columns.md).
  
  
  
