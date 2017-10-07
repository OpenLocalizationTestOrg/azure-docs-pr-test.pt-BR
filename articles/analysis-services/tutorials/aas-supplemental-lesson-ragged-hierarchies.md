---
título: aaa "lição suplementar do tutorial do Azure Analysis Services: hierarquias desbalanceadas | Descrição de Microsoft Docs": descreve como toofix hierarquias desbalanceadas tutorial do hello Azure Analysis Services.
serviços: documentationcenter do analysis services: ' autor: manager minewiskan: erikre editor: ' marcas: '

MS. AssetID: MS. Service: MS. devlang do analysis services: NA MS. Topic: get-started-article tgt_pltfrm: NA Workload: MS. Date na: 26/05/2017 Author: owend
---
# <a name="supplemental-lesson---ragged-hierarchies"></a>Lição suplementar – hierarquias desbalanceadas

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Nesta lição suplementar, você resolver um problema comum ao dinamizar hierarquias que contêm valores em branco (membros) em diferentes níveis. Por exemplo, uma organização em que um gerente de alto nível tem tanto gerentes departamentais quanto não gerentes como subordinados diretos. Ou então, hierarquias geográficas compostas por país-região-cidade, em que algumas cidades não têm um estado ou província pai, por exemplo, Washington D.C. e Cidade do Vaticano. Quando uma hierarquia tem membros em branco, ele normalmente desce toodifferent ou irregulares, níveis.

![aas-lesson-detail-ragged-hierarchies-table](../tutorials/media/aas-lesson-detail-ragged-hierarchies-table.png)

Modelos de tabela no nível de compatibilidade Olá 1400 têm adicional **ocultar membros** propriedade para hierarquias. Olá **padrão** configuração pressupõe que não existem membros em branco em qualquer nível. Olá **ocultar membros em branco** configuração exclui membros em branco da hierarquia de saudação quando adicionado tooa tabela dinâmica ou relatório.  
  
Estimado tempo toocomplete nesta lição: **20 minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
Este tópico de lição suplementar faz parte de um tutorial de modelagem Tabular. Antes de executar tarefas de saudação nesta lição suplementar, você deve concluir todas as lições anteriores ou tem um projeto de modelo de exemplo Adventure Works Internet Sales concluído. 

Se você criou o projeto de vendas de Internet da AW hello como parte do tutorial hello, seu modelo ainda não contém dados ou hierarquias desbalanceadas. toocomplete nesta lição suplementar, você precisa primeiro toocreate Olá problema adicionando algumas tabelas adicionais, criar relações, colunas calculadas, uma medida e uma nova hierarquia da organização. Essa parte leva cerca de 15 minutos. Em seguida, você pode obter toosolve em apenas alguns minutos.  

## <a name="add-tables-and-objects"></a>Adicionar tabelas e objetos
  
### <a name="tooadd-new-tables-tooyour-model"></a>novo modelo de tooyour tabelas tooadd
  
1.  No Gerenciador de Modelos tabulares, expanda **Fontes de Dados**, clique com o botão direito do mouse em sua conexão > **Importar Novas Tabelas**.
  
2.  No navegador, selecione **DimEmployee** e **FactResellerSales** e, em seguida, clique em **OK**.

3.  No Editor de Consultas, clique em **Importar**

4.  Crie seguinte Olá [relações](../tutorials/aas-lesson-4-create-relationships.md):

    | Tabela 1           | Coluna       | Direção do Filtro   | Tabela 2     | Coluna      | Ativo |
    |-------------------|--------------|--------------------|-------------|-------------|--------|
    | FactResellerSales | OrderDateKey | Padrão            | DimDate     | Data        | Sim    |
    | FactResellerSales | DueDate      | Padrão            | DimDate     | Data        | Não     |
    | FactResellerSales | ShipDateKey  | Padrão            | DimDate     | Data        | Não     |
    | FactResellerSales | ProductKey   | Padrão            | DimProduct  | ProductKey  | Sim    |
    | FactResellerSales | EmployeeKey  | Tabelas de tooBoth | DimEmployee | EmployeeKey | Sim    |

5. Em Olá **DimEmployee** de tabela, crie a seguinte Olá [colunas calculadas](../tutorials/aas-lesson-5-create-calculated-columns.md): 

    **Caminho** 
    ```
    =PATH([EmployeeKey],[ParentEmployeeKey])
    ```

    **FullName** 
    ```
    =[FirstName] & " " & [MiddleName] & " " & [LastName]
    ```

    **Level1** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,1)) 
    ```

    **Level2** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,2)) 
    ```

    **Level3** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,3)) 
    ```

    **Level4** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,4)) 
    ```

    **Level5** 
    ```
    =LOOKUPVALUE(DimEmployee[FullName],DimEmployee[EmployeeKey],PATHITEM([Path],1,5)) 
    ```

6.  Em Olá **DimEmployee** de tabela, crie um [hierarquia](../tutorials/aas-lesson-9-create-hierarchies.md) chamado **organização**. Adicionar Olá colunas na ordem a seguir: **Level1**, **Level2**, **Level3**, **Level4**, **Level5**.

7.  Em Olá **FactResellerSales** de tabela, crie a seguinte Olá [medidas](../tutorials/aas-lesson-6-create-measures.md):

    ```
    ResellerTotalSales:=SUM([SalesAmount])
    ```

8.  Use [analisar no Excel](../tutorials/aas-lesson-12-analyze-in-excel.md) tooopen Excel e criar automaticamente uma tabela dinâmica.

9.  Em **PivotTable Fields**, adicionar Olá **organização** hierarquia da saudação **DimEmployee** tabela muito**linhas**e hello **ResellerTotalSales** medida da saudação **FactResellerSales** tabela muito**valores**.

    ![aas-lesson-detail-ragged-hierarchies-pivottable](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable.png)

    Como você pode ver na tabela dinâmica de hello, hierarquia Olá exibe linhas que são irregulares. Há muitas linhas em que os membros em branco são mostrados.

## <a name="toofix-hello-ragged-hierarchy-by-setting-hello-hide-members-property"></a>Olá toofix hierarquia imperfeita, definindo propriedade de membros de ocultar Olá

1.  Em **Gerenciador de Modelos tabulares**, expanda **Tabelas** > **DimEmployee** > **Hierarquias** > **Organização**.

2.  Em **Propriedades** > **Ocultar Membros**, selecione **Ocultar membros em branco**. 

    ![aas-lesson-detail-ragged-hierarchies-hidemembers](../tutorials/media/aas-lesson-detail-ragged-hierarchies-hidemembers.png)

3.  No Excel, atualize Olá tabela dinâmica. 

    ![aas-lesson-detail-ragged-hierarchies-pivottable-refresh](../tutorials/media/aas-lesson-detail-ragged-hierarchies-pivottable-refresh.png)

    Agora isso tem uma aparência muito melhor!

## <a name="see-also"></a>Consulte também   
[Lição 9: criar hierarquias](../tutorials/aas-lesson-9-create-hierarchies.md)  
[Lição Suplementar – Segurança Dinâmica](../tutorials/aas-supplemental-lesson-dynamic-security.md)  
[Lição suplementar – linhas de detalhes](../tutorials/aas-supplemental-lesson-detail-rows.md)  