---
título: aaa "lição do tutorial do Azure Analysis Services 6: criar medidas | Descrição de Microsoft Docs": descreve como toocreate medidas no projeto do tutorial hello Azure Analysis Services. serviços: documentationcenter do analysis services: ' autor: manager minewiskan: erikre editor: ' marcas: '

MS. AssetID: MS. Service: MS. devlang do analysis services: NA MS. Topic: get-started-article tgt_pltfrm: NA Workload: MS. Date na: 01/06/2017 Author: owend
---
# <a name="lesson-6-create-measures"></a>Lição 6: criar medidas

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Nesta lição, você criará medidas toobe incluído em seu modelo. Toohello semelhante calculado colunas que você criou, uma medida é um cálculo criado usando uma fórmula DAX. No entanto, ao contrário de colunas calculadas, as medidas são avaliadas com base em um *filtro* selecionado pelo usuário. Por exemplo, uma coluna particular ou uma segmentação de dados adicionados toohello campo de rótulos de linha em uma tabela dinâmica. Um valor para cada célula no filtro de saudação é calculado pela medida de saudação aplicada. As medidas são cálculos avançados e flexíveis que você deseja tooinclude em quase todos os modelos de tabela tooperform dinâmico cálculos em dados numéricos. mais, consulte toolearn [medidas](https://docs.microsoft.com/sql/analysis-services/tabular-models/measures-ssas-tabular).
  
toocreate medidas, que você usar o hello *grade de medida*. Por padrão, cada tabela tem uma grade de medida vazia; no entanto, você normalmente não criará medidas para todas as tabelas. grade de medida de saudação aparece abaixo de uma tabela no designer de modelo hello quando no modo de exibição de dados. toohide ou Mostrar grade de medida Olá para uma tabela, clique em Olá **tabela** menu e clique **Mostrar grade de medida**.  
  
Você pode criar uma medida clicando em uma célula vazia na grade de medida hello e digitando uma fórmula DAX na barra de fórmulas hello. Quando você clique insira toocomplete Olá a fórmula, medida hello e aparece na célula de saudação. Você também pode criar medidas usando uma função de agregação padrão clicando em uma coluna e, em seguida, clicando em Olá botão AutoSoma (**∑**) na barra de ferramentas de saudação. As medidas criadas usando o recurso de AutoSoma Olá aparecem na célula de grade de medida Olá diretamente sob a coluna de hello, mas podem ser movidas.  
  
Nesta lição, você criará medidas inserindo uma fórmula DAX na barra de fórmulas hello e pelo recurso de AutoSoma hello.  
  
Estimado tempo toocomplete nesta lição: **30 minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem. Antes de executar tarefas de saudação nesta lição, você deverá ter completado lição anterior Olá: [lição 5: criar colunas calculadas](../tutorials/aas-lesson-5-create-calculated-columns.md).  
  
## <a name="create-measures"></a>Criar medidas  
  
#### <a name="toocreate-a-dayscurrentquartertodate-measure-in-hello-dimdate-table"></a>uma medida de DaysCurrentQuarterToDate na tabela DimDate de saudação do toocreate  
  
1.  No designer de modelo hello, clique em Olá **DimDate** tabela.  
  
2.  Na grade de medida hello, clique em célula vazia do hello superior esquerdo.  
  
3.  Na barra de fórmulas hello, digite Olá seguinte fórmula:  
  
    ```
    DaysCurrentQuarterToDate:=COUNTROWS( DATESQTD( 'DimDate'[Date])) 
    ```
  
    Célula do aviso Olá superior esquerda agora contém um nome de medida, **DaysCurrentQuarterToDate**, seguido pelo resultado hello, **92**.
    
      ![aas-lesson6-newmeasure](../tutorials/media/aas-lesson6-newmeasure.png) 
    
    Diferente das colunas calculadas, com fórmulas de medida, você pode digitar o nome de medida hello, seguido por dois-pontos, seguido pela expressão de fórmula hello.

  
#### <a name="toocreate-a-daysincurrentquarter-measure-in-hello-dimdate-table"></a>uma medida de DaysInCurrentQuarter na tabela DimDate de saudação do toocreate  
  
1.  Com hello **DimDate** ainda ativa no designer de modelo hello, na grade de medida de saudação da tabela, clique Olá a célula vazia abaixo da medida Olá criada.  
  
2.  Na barra de fórmulas hello, digite Olá seguinte fórmula:  
  
    ```
    DaysInCurrentQuarter:=COUNTROWS( DATESBETWEEN( 'DimDate'[Date], STARTOFQUARTER( LASTDATE('DimDate'[Date])), ENDOFQUARTER('DimDate'[Date])))
    ```
  
    Ao criar uma taxa de comparação entre um período incompleto e hello período anterior. fórmula de Olá deve calcular a proporção de saudação do período de saudação decorrido e compará-la toohello mesma proporção em Olá período anterior. Nesse caso, [DaysCurrentQuarterToDate] / [DaysInCurrentQuarter] fornece Olá proporção decorrido em Olá período atual.  
  
#### <a name="toocreate-an-internetdistinctcountsalesorder-measure-in-hello-factinternetsales-table"></a>toocreate uma medida InternetDistinctCountSalesOrder na tabela de FactInternetSales Olá  
  
1.  Clique em Olá **FactInternetSales** tabela.   
  
2.  Clique em Olá **SalesOrderNumber** título de coluna.  
  
3.  Na barra de ferramentas hello, clique em Olá de seta para baixo próxima toohello AutoSoma (**∑**) botão e, em seguida, selecione **DistinctCount**.  
  
    recurso de AutoSoma Olá automaticamente cria uma medida para a coluna selecionada hello, usando a fórmula de agregação padrão DistinctCount hello.  
    
       ![aas-lesson6-newmeasure2](../tutorials/media/aas-lesson6-newmeasure2.png)
  
4.  Na grade de medida hello, clique em nova medida de Olá e, em seguida, em Olá **propriedades** janela, na **nome da medida**, renomeie a medida de saudação muito**InternetDistinctCountSalesOrder**. 
 
  
#### <a name="toocreate-additional-measures-in-hello-factinternetsales-table"></a>medidas adicionais na tabela de FactInternetSales Olá toocreate  
  
1.  Usando o recurso de AutoSoma hello, crie e nomeie Olá medidas a seguir:  

    |Coluna|Nome da medida|AutoSoma (∑)|Fórmula|  
    |----------------|----------|-----------------|-----------|  
    |SalesOrderLineNumber|InternetOrderLinesCount|Contagem|=COUNTA([SalesOrderLineNumber])|  
    |OrderQuantity|InternetTotalUnits|Soma|=SUM([OrderQuantity])|  
    |DiscountAmount|InternetTotalDiscountAmount|Soma|=SUM([DiscountAmount])|  
    |TotalProductCost|InternetTotalProductCost|Soma|=SUM([TotalProductCost])|  
    |SalesAmount|InternetTotalSales|Soma|=SUM([SalesAmount])|  
    |Margin|InternetTotalMargin|Soma|=SUM([Margin])|  
    |TaxAmt|InternetTotalTaxAmt|Soma|=SUM([TaxAmt])|  
    |Freight|InternetTotalFreight|Soma|=SUM([Freight])|  
  
2.  Ao clicar em uma célula vazia na grade de medida hello e usando a barra de fórmulas hello, criar e mede a seguir Olá nome em ordem:  
  
      ```
      InternetPreviousQuarterMargin:=CALCULATE([InternetTotalMargin],PREVIOUSQUARTER('DimDate'[Date]))
      ```
      
      ```
      InternetCurrentQuarterMargin:=TOTALQTD([InternetTotalMargin],'DimDate'[Date])
      ```
  
      ```
      InternetPreviousQuarterMarginProportionToQTD:=[InternetPreviousQuarterMargin]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
      ```
      InternetPreviousQuarterSales:=CALCULATE([InternetTotalSales],PREVIOUSQUARTER('DimDate'[Date]))
      ```
  
      ```
      InternetCurrentQuarterSales:=TOTALQTD([InternetTotalSales],'DimDate'[Date])
      ```
      
      ```
      InternetPreviousQuarterSalesProportionToQTD:=[InternetPreviousQuarterSales]*([DaysCurrentQuarterToDate]/[DaysInCurrentQuarter])
      ```
  
Medidas criadas para Olá FactInternetSales tabela podem ser dados financeiros essenciais de tooanalyze usadas, como vendas, custos e margem de lucro para itens definidos pelo filtro selecionado do usuário Olá.  
  
## <a name="whats-next"></a>O que vem a seguir?
[Lição 7: criar indicadores chave de desempenho](../tutorials/aas-lesson-7-create-key-performance-indicators.md).  

  
