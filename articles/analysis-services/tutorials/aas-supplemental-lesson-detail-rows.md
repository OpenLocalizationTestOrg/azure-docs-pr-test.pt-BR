---
título: aaa "lição suplementar do tutorial do Azure Analysis Services: linhas de detalhes | Descrição de Microsoft Docs": descreve como toocreate uma expressão de linhas de detalhes em Olá tutorial do Azure Analysis Services.
serviços: documentationcenter do analysis services: ' autor: manager minewiskan: erikre editor: ' marcas: '

MS. AssetID: MS. Service: MS. devlang do analysis services: NA MS. Topic: get-started-article tgt_pltfrm: NA Workload: MS. Date na: 26/05/2017 Author: owend
---
# <a name="supplemental-lesson---detail-rows"></a>Lição suplementar – Linhas de Detalhes

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Nesta lição suplementar, você use Olá Editor DAX toodefine uma expressão personalizada de linhas de detalhes. Uma expressão de linhas de detalhes é uma propriedade em uma medida, proporcionando aos usuários finais para obter mais informações sobre os resultados da saudação agregado de uma medida. 
  
Estimado tempo toocomplete nesta lição: **10 minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
Este tópico de lição suplementar faz parte de um tutorial de modelagem Tabular. Antes de executar tarefas de saudação nesta lição suplementar, você deve concluir todas as lições anteriores ou tem um projeto de modelo de exemplo Adventure Works Internet Sales concluído.  
  
## <a name="what-do-we-need-toosolve"></a>O que fazer precisamos toosolve?
Vamos examinar os detalhes de saudação de nossa medida InternetTotalSales, antes de adicionar uma expressão de linhas de detalhes.

1.  No SSDT, clique em Olá **modelo** menu > **analisar no Excel** tooopen Excel e criar uma tabela dinâmica em branco.
  
2.  Em **PivotTable Fields**, adicionar Olá **InternetTotalSales** de medidas da tabela de FactInternetSales Olá muito**valores**, **CalendarYear**de saudação DimDate tabela muito**colunas**, e **EnglishCountryRegionName** muito**linhas**. Agora, nossa tabela dinâmica oferece nos resultados agregados de medidas de InternetTotalSales Olá regiões e ano. 

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-pivottable.png)

3. Em Olá tabela dinâmica, clique duas vezes em um valor agregado para um ano e um nome de região. Aqui é clicado duas vezes valor Olá Austrália e hello ano 2014. Uma nova planilha abre os dados contidos, mas não os dados úteis.

    ![aas-lesson-detail-rows-pivottable](../tutorials/media/aas-lesson-detail-rows-sheet.png)
  
O que podemos gostariam de ter toosee aqui é uma tabela que contém colunas e linhas de dados que contribuem toohello agregado resultado de nossa medida InternetTotalSales. toodo que podemos adicionar uma expressão de linhas de detalhes como uma propriedade de medida hello.

## <a name="add-a-detail-rows-expression"></a>Adicionar uma expressão de linhas de detalhes

#### <a name="toocreate-a-detail-rows-expression"></a>toocreate uma expressão de linhas de detalhes 
  
1. No SSDT, na grade de medida da tabela de FactInternetSales hello, clique em Olá **InternetTotalSales** medidas. 

2. Em **propriedades** > **expressão de linhas de detalhes**, clique em Olá editor botão tooopen Olá Editor DAX.

    ![aas-lesson-detail-rows-ellipse](../tutorials/media/aas-lesson-detail-rows-ellipse.png)

3. No Editor do DAX, digite Olá expressão a seguir:

    ```
    SELECTCOLUMNS(
    FactInternetSales,
    "Sales Order Number", FactInternetSales[SalesOrderNumber],
    "Customer First Name", RELATED(DimCustomer[FirstName]),
    "Customer Last Name", RELATED(DimCustomer[LastName]),
    "City", RELATED(DimGeography[City]),
    "Order Date", FactInternetSales[OrderDate],
    "Internet Total Sales", [InternetTotalSales]
    )

    ```

    Essa expressão especifica nomes de colunas, e os resultados de medida de saudação tabelas FactInternetSales e tabelas relacionadas são retornados quando um usuário clica duas vezes em um resultado agregado em uma tabela dinâmica ou relatório.

4. Novamente no Excel, excluir planilha Olá criada na etapa 3, em seguida, clique duas vezes em um valor agregado. Neste momento, com uma propriedade de expressão de linhas de detalhes definida para medidas hello, uma nova planilha é aberta que contém dados muito mais útil.

    ![aas-lesson-detail-rows-detailsheet](../tutorials/media/aas-lesson-detail-rows-detailsheet.png)

5. Reimplante o modelo.

  
## <a name="see-also"></a>Consulte também  
[Função SELECTCOLUMNS (DAX)](https://msdn.microsoft.com/library/mt761759.aspx)   
[Lição Suplementar – Segurança Dinâmica](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[Lição Suplementar – hierarquias desbalanceadas](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)  
