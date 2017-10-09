---
título: aaa "lição do tutorial do Azure Analysis Services 7: criar indicadores chave de desempenho | Descrição de Microsoft Docs": descreve como indicadores de desempenho chave toocreate em Olá projeto do tutorial do Azure Analysis Services. serviços: documentationcenter do analysis services: ' autor: manager minewiskan: erikre editor: ' marcas: '

MS. AssetID: MS. Service: MS. devlang do analysis services: NA MS. Topic: get-started-article tgt_pltfrm: NA Workload: MS. Date na: 26/05/2017 Author: owend
---
# <a name="lesson-7-create-key-performance-indicators"></a>Lição 7: criar indicadores chave de desempenho

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Nesta lição, você cria KPIs (indicadores chave de desempenho). Os KPIs são usados toogauge o desempenho de um valor definido por um *Base* medidas, em relação a um *destino* também definido por uma medida ou valor absoluto do valor. Em aplicativos cliente de relatório, os KPIs podem proporcionar os profissionais de negócios toounderstand uma maneira rápida e fácil um resumo das tendências de êxito ou tooidentify de negócios. toolearn mais, consulte [KPIs](https://docs.microsoft.com/sql/analysis-services/tabular-models/kpis-ssas-tabular)
  
Estimado tempo toocomplete nesta lição: **15 minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem. Antes de executar tarefas de saudação nesta lição, você deverá ter completado lição anterior Olá: [lição 6: criar medidas](../tutorials/aas-lesson-6-create-measures.md).   
  
## <a name="create-key-performance-indicators"></a>Criar indicadores chave de desempenho  
  
#### <a name="toocreate-an-internetcurrentquartersalesperformance-kpi"></a>toocreate um KPI InternetCurrentQuarterSalesPerformance  
  
1.  No designer de modelo hello, clique em Olá **FactInternetSales** tabela.  
  
2.  Na grade de medida hello, clique em uma célula vazia.  
  
3.  Na barra de fórmulas hello, acima da tabela hello, digite Olá seguinte fórmula: 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    Essa medida serve como a medida Base Olá Olá KPI.  
  
4.  Clique com o botão direito do mouse em **InternetCurrentQuarterSalesPerformance** > **Criar KPI**.   
  
5.  Na caixa de diálogo do hello desempenho KPI (indicador chave), em **destino** selecione **valor absoluto**e, em seguida, digite **1.1**.  
  
7.  No campo de (baixa) de controle deslizante esquerdo hello, digite **1**e, em seguida, no controle deslizante à direita (alto) de hello, digite **1.07**.  
  
8.  Em **selecionar estilo de ícone**, selecione o triângulo de losango (vermelho), hello (amarelo), círculo de tipo de ícone (verde).
  
    ![aas-lesson7-kpi](../tutorials/media/aas-lesson7-kpi.png)
    
    > [!TIP]  
    > Saudação de aviso expansível **descrições** rótulo abaixo estilos de ícone disponíveis hello. Use as descrições para Olá várias toomake de elementos KPI-los mais identificáveis nos aplicativos cliente.  
  
9. Clique em **Okey** toocomplete Olá KPI.  
  
    Na grade de medida hello, observe Olá ícone próximo toohello **InternetCurrentQuarterSalesPerformance** medidas. Esse ícone indica que essa medida serve como um valor Base para um KPI.  
  
#### <a name="toocreate-an-internetcurrentquartermarginperformance-kpi"></a>toocreate um KPI InternetCurrentQuarterMarginPerformance  
  
1.  Na grade de medida Olá para Olá **FactInternetSales** da tabela, clique em uma célula vazia.  
  
2.  Na barra de fórmulas hello, acima da tabela hello, digite Olá seguinte fórmula:  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  Clique com o botão direito do mouse em **InternetCurrentQuarterMarginPerformance** > **Criar KPI**.  
  
4.  Na caixa de diálogo do hello desempenho KPI (indicador chave), em **destino** selecione **valor absoluto**e, em seguida, digite **1.25**.   
  
5.  No campo de controle deslizante de (baixa) à esquerda de hello, slides até que o campo Olá exibe **0,8**, e saudação de slide, em seguida, no campo de controle deslizante (alto), até que o campo Olá exibe **1.03**.  
  
6.  Em **selecionar estilo de ícone**, selecione a forma de losango hello (vermelha), triângulo (amarelo), tipo de ícone de círculo (verde) e, em seguida, clique em **Okey**.  
  
## <a name="whats-next"></a>O que vem a seguir?
[Lição 8: criar perspectivas](../tutorials/aas-lesson-8-create-perspectives.md).
  
  
