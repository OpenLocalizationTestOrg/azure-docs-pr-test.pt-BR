---
título: aaa "lição 3 do tutorial do Azure Analysis Services: marcar como tabela de data | Descrição de Microsoft Docs": descreve como toomark uma data de tabela no projeto do tutorial hello Azure Analysis Services. serviços: documentationcenter do analysis services: ' autor: manager minewiskan: erikre editor: ' marcas: '

MS. AssetID: MS. Service: MS. devlang do analysis services: NA MS. Topic: get-started-article tgt_pltfrm: NA Workload: MS. Date na: 01/06/2017 Author: owend
---
# <a name="lesson-3-mark-as-date-table"></a>Lição 3: marcar como tabela de data

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Na Lição 2: obter dados, você importou uma tabela de dimensões chamada DimDate. Enquanto no seu modelo essa tabela é denominada DimDate, ela também é conhecida como uma *Tabela de data*, que contém dados de data e hora.  
  
Sempre que usar funções de inteligência de dados temporais DAX, como fará quando criar medidas mais adiante, você deverá especificar as propriedades, que incluem uma *Tabela de data* e uma *coluna Data*, que é um identificador exclusivo nessa tabela.
  
Nesta lição, você marca a tabela DimDate Olá Olá *a tabela de data* e a coluna de data de saudação (na tabela de data Olá) como Olá *coluna data* (identificador exclusivo).  

Antes de marcar a coluna de data e a tabela de data Olá, é um toodo bom momento um pouco de limpeza toomake seu toounderstand mais fácil de modelo. Observe na tabela de DimDate Olá uma coluna denominada **FullDateAlternateKey**. Esta coluna contém uma linha para cada dia em cada ano civil incluído na tabela de saudação. Você usará muito essa coluna em fórmulas de medida e em relatórios. No entanto, FullDateAlternateKey não é um bom identificador para essa coluna. Você o renomear muito**data**, tornando mais fácil tooidentify e incluir em fórmulas. Sempre que possível, é uma boa ideia toorename objetos como tabelas e colunas toomake-los mais fácil tooidentify no SSDT e o cliente de relatório de aplicativos, como o Power BI e Excel. 
  
Estimado tempo toocomplete nesta lição: **três minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem. Antes de executar tarefas de saudação nesta lição, você deverá ter completado lição anterior Olá: [lição 2: obter dados](../tutorials/aas-lesson-2-get-data.md). 

### <a name="toorename-hello-fulldatealternatekey-column"></a>coluna de FullDateAlternateKey toorename Olá

1.  No designer de modelo hello, clique em Olá **DimDate** tabela.

2.  Clique duas vezes no cabeçalho Olá Olá **FullDateAlternateKey** coluna e, em seguida, renomeie-a muito**data**.

  
### <a name="tooset-mark-as-date-table"></a>tooset marcar como tabela de data  
  
1.  Selecione Olá **data** coluna e, em seguida, em Olá **propriedades** janela, em **tipo de dados**, certifique-se de **data** está selecionado.  
  
2.  Clique em Olá **tabela** menu, clique em **data**e, em seguida, clique em **marcar como tabela de data**.  
  
3.  Em Olá **marcar como tabela de data** caixa de diálogo Olá **data** caixa de listagem, selecione Olá **data** coluna como Olá identificador exclusivo. Ela geralmente é selecionada por padrão. Clique em **OK**. 

    ![aas-lesson3-date-table](../tutorials/media/aas-lesson3-date-table.png)
  

## <a name="whats-next"></a>O que vem a seguir?
[Lição 4: criar relações](../tutorials/aas-lesson-4-create-relationships.md).
  
