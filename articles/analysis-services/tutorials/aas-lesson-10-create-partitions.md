---
título: aaa "lição do tutorial do Azure Analysis Services 10: criar partições | Descrição de Microsoft Docs": descreve como toocreate partições no projeto do tutorial hello Azure Analysis Services. serviços: documentationcenter do analysis services: ' autor: manager minewiskan: erikre editor: ' marcas: '

MS. AssetID: MS. Service: MS. devlang do analysis services: NA MS. Topic: get-started-article tgt_pltfrm: NA Workload: MS. Date na: 26/05/2017 Author: owend
---
# <a name="lesson-10-create-partitions"></a>Lição 10: criar partições

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Nesta lição, você pode criar tabelas tabelas FactInternetSales partições toodivide Olá em partes lógicas menores que podem ser processada (atualizadas) independentemente de outras partições. Por padrão, cada tabela incluída em seu modelo tem uma partição, o que inclui todas as tabelas Olá colunas e linhas. Para a tabela de FactInternetSales hello, queremos dados de saudação toodivide por ano; uma partição para cada um dos cinco anos da tabela hello. Cada partição pode ser então processada independentemente. mais, consulte toolearn [partições](https://docs.microsoft.com/sql/analysis-services/tabular-models/partitions-ssas-tabular). 
  
Estimado tempo toocomplete nesta lição: **15 minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem. Antes de executar tarefas de saudação nesta lição, você deverá ter completado lição anterior Olá: [lição 9: criar hierarquias](../tutorials/aas-lesson-9-create-hierarchies.md).  
  
## <a name="create-partitions"></a>Criar partições  
  
#### <a name="toocreate-partitions-in-hello-factinternetsales-table"></a>toocreate partições na tabela de FactInternetSales Olá  
  
1.  No Gerenciador de Modelos tabular, expanda **Tabelas** e, em seguida, clique com o botão direito do mouse em **FactInternetSales** > **Partições**.  
  
2.  No Gerenciador de partições, clique em **cópia**e, em seguida, altere o nome de saudação muito**FactInternetSales2010**.
  
    Porque você quer Olá partição tooinclude somente as linhas dentro de um determinado período, para o ano de saudação 2010, você deve modificar expressão de consulta de saudação.
  
4.  Clique em **Design** tooopen Editor de consultas e, em seguida, clique em Olá **FactInternetSales2010** consulta.

5.  Na visualização, clique em Olá seta em Olá **OrderDate** título de coluna e clique **filtros de data/hora** > **entre**.

    ![aas-lesson10-query-editor](../tutorials/media/aas-lesson10-query-editor.png)

6.  Na caixa de diálogo Filtrar linhas hello, em **Mostrar linhas onde: OrderDate**, deixe **é depois ou igual a**e, em seguida, no campo de data hello, digite **1/1/2010**. Deixe Olá **e** operador selecionado, selecione **é antes**, no campo de data hello, digite **1/1/2011**e, em seguida, clique em **Okey**.

    ![aas-lesson10-filter-rows](../tutorials/media/aas-lesson10-filter-rows.png)
    
    Observe que, no Editor de Consultas, em ETAPAS APLICADAS, você verá outra etapa chamada Linhas Filtradas. Esse filtro é tooselect somente datas de pedido de 2010.

8.  Clique em **Importar**.

    No Gerenciador de partições, observe a consulta Olá expressão agora tem uma cláusula filtrada linhas adicional.

    ![aas-lesson10-query](../tutorials/media/aas-lesson10-query.png)
  
    Essa instrução Especifica que essa partição deve incluir somente os dados Olá dessas linhas onde Olá OrderDate está Olá ano 2010 conforme especificado na cláusula de linhas filtradas hello.  
  
  
#### <a name="toocreate-a-partition-for-hello-2011-year"></a>toocreate uma partição para Olá ano de 2011  
  
1.  Na lista de partições hello, clique em Olá **FactInternetSales2010** partição que você criou e, em seguida, clique em **cópia**.  Alterar o nome da partição Olá muito**FactInternetSales2011**. 

    Não é necessário toouse toocreate do Editor de consultas uma nova cláusula de linhas filtradas. Como você criou uma cópia da consulta Olá para 2010, você só precisa toodo é fazer uma pequena alteração na consulta de saudação de 2011.
  
2.  Em **expressão de consulta**, em ordem para essa partição tooinclude somente as linhas de saudação ano de 2011, substituir anos Olá na cláusula de linhas filtradas Olá com **2011** e **2012**, respectivamente, como:  
  
    ```  
    let
        Source = #"SQL/localhost;AdventureWorksDW2014",
        dbo_FactInternetSales = Source{[Schema="dbo",Item="FactInternetSales"]}[Data],
        #"Removed Columns" = Table.RemoveColumns(dbo_FactInternetSales,{"OrderDateKey", "DueDateKey", "ShipDateKey"}),
        #"Filtered Rows" = Table.SelectRows(#"Removed Columns", each [OrderDate] >= #datetime(2011, 1, 1, 0, 0, 0) and [OrderDate] < #datetime(2012, 1, 1, 0, 0, 0))
    in
        #"Filtered Rows"
   
    ```  
  
#### <a name="toocreate-partitions-for-2012-2013-and-2014"></a>partições de toocreate de 2012, 2013 e 2014.  
  
- Execute as etapas anteriores de hello, criando partições para 2012 2013 e 2014, alterando anos Olá Olá linhas filtradas cláusula tooinclude somente as linhas daquele ano. 
  

## <a name="delete-hello-factinternetsales-partition"></a>Excluir Olá FactInternetSales partição
Agora que você tiver partições para cada ano, você pode excluir a partição de FactInternetSales Olá; impedindo a sobreposição ao escolher o processo de todos os durante o processamento de partições.

#### <a name="toodelete-hello-factinternetsales-partition"></a>Olá toodelete FactInternetSales partição
-  Clique em Olá FactInternetSales partição e, em seguida, clique em **excluir**.



## <a name="process-partitions"></a>Processar partições  
No Gerenciador de partições, observe Olá **último processados** coluna para cada uma das novas partições de saudação criado mostra essas partições nunca tiveram sido processadas. Quando você criar partições, você deve executar um processar partições ou processar tabela operação toorefresh Olá dados nessas partições.  
  
#### <a name="tooprocess-hello-factinternetsales-partitions"></a>tooprocess Olá FactInternetSales partições  
  
1.  Clique em **Okey** tooclose Gerenciador de partições.  
  
2.  Clique em Olá **FactInternetSales** de tabela, clique em Olá **modelo** menu > **processo** > **processar partições**.  
  
3.  Na caixa de diálogo processar partições hello, verifique se **modo** está definido muito**processar padrão**.  
  
4.  Marque a caixa de seleção de saudação em Olá **processo** coluna para cada Olá cinco partições criadas e depois clique em **Okey**.  

    ![aas-lesson10-process-partitions](../tutorials/media/aas-lesson10-process-partitions.png)
  
    Se você for solicitado a fornecer credenciais de representação, insira o nome de usuário do Windows hello e a senha que você especificou na lição 2.  
  
    Olá **processamento de dados** caixa de diálogo aparece e exibe os detalhes do processo para cada partição. Observe que um número diferente de linhas é transferido para cada partição. Cada partição inclui somente as linhas para ano Olá especificado na cláusula WHERE na instrução SQL de saudação do hello. Quando o processamento é concluído, vá em frente e fechar a caixa de diálogo de processamento de dados de saudação.  
  
    ![aas-lesson10-process-complete](../tutorials/media/aas-lesson10-process-complete.png)
  
 ## <a name="whats-next"></a>O que vem a seguir?
Vá toohello próxima lição: [lição 11: criar funções](../tutorials/aas-lesson-11-create-roles.md). 
