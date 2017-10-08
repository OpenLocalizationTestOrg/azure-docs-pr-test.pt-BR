---
título: aaa "lição do tutorial do Azure Analysis Services 12: analisar no Excel | Descrição de Microsoft Docs": descreve como toouse analisar no Excel em hello Azure Analysis Services projeto do tutorial. serviços: documentationcenter do analysis services: ' autor: manager minewiskan: erikre editor: ' marcas: '

MS. AssetID: MS. Service: MS. devlang do analysis services: NA MS. Topic: get-started-article tgt_pltfrm: NA Workload: MS. Date na: 26/05/2017 Author: owend
---
# <a name="lesson-12-analyze-in-excel"></a>Lição 12: analisar no Excel

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Nesta lição, use Olá analisar no Excel recurso tooopen Microsoft Excel, criar automaticamente um espaço de trabalho de modelo de toohello de conexão e adicionar automaticamente uma planilha de toohello de tabela dinâmica. Olá analisar no recurso do Excel destina-se tooprovide eficácia de saudação de tootest uma maneira rápida e fácil do seu modelo criar toodeploying anterior seu modelo. Você não executará nenhuma análise de dados nesta lição. Olá finalidade desta lição é toofamiliarize, criar modelo hello e, em seguida, com ferramentas Olá você pode usar tootest design de modelo.   
  
toocomplete nesta lição, o Excel deve ser instalada em Olá mesmo computador que o SSDT.
  
Estimado tempo toocomplete nesta lição: **cinco minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem. Antes de executar tarefas de saudação nesta lição, você deverá ter completado lição anterior Olá: [lição 11: criar funções](../tutorials/aas-lesson-11-create-roles.md).  
  
## <a name="browse-using-hello-default-and-internet-sales-perspectives"></a>Procurar usando as perspectivas de saudação padrão e vendas pela Internet  
Nestas primeiras tarefas, procurar seu modelo usando os dois saudação padrão perspectiva, que inclui todos os objetos de modelo, e também usando a perspectiva de vendas pela Internet Olá você anteriormente. Olá perspectiva vendas pela Internet exclui o objeto de tabela de cliente hello.  
  
#### <a name="toobrowse-by-using-hello-default-perspective"></a>toobrowse usando a perspectiva do saudação padrão  
  
1.  Clique em Olá **modelo** menu > **analisar no Excel**.  
  
2.  Em Olá **analisar no Excel** caixa de diálogo, clique em **Okey**.  
  
    O Excel abre com uma nova pasta de trabalho. Uma conexão de fonte de dados é criado usando a conta de usuário atual hello e Olá perspectiva padrão é campos exibíveis toodefine usado. Uma tabela dinâmica é adicionada automaticamente toohello planilha.  
  
3.  No Excel, na Olá **lista de campos da tabela dinâmica**, observe Olá **DimDate** e **FactInternetSales** grupos de medidas são exibidos. Olá **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**, **DimProductCategory**, **DimProductSubcategory**, e **FactInternetSales** também as tabelas com suas respectivas colunas aparecem.  
  
4.  Feche o Excel sem salvar a pasta de trabalho de saudação.  
  
#### <a name="toobrowse-by-using-hello-internet-sales-perspective"></a>toobrowse usando a perspectiva de vendas pela Internet Olá  
  
1.  Clique em Olá **modelo** menu e clique **analisar no Excel**.  
  
2.  Em Olá **analisar no Excel** caixa de diálogo, deixe **usuário Windows atual** selecionado, em seguida, no hello **perspectiva** caixa de listagem suspensa, selecione **vendas pela Internet** e, em seguida, clique em **Okey**. 
    
    ![aas-lesson12-perspective](../tutorials/media/aas-lesson12-perspective.png)
    
3.  No Excel, na **PivotTable Fields**, observe a tabela DimCustomer de saudação é excluída da lista de campos de saudação.  
    
    ![aas-lesson12-fields](../tutorials/media/aas-lesson12-fields.png)
    
4.  Feche o Excel sem salvar a pasta de trabalho de saudação.  
  
## <a name="browse-by-using-roles"></a>Navegar usando funções  
As funções são parte importante de qualquer modelo tabular. Pelo menos uma função toowhich usuários são adicionados como membros, os usuários não podem acessar e analisar dados usando seu modelo. Olá analisar no recurso do Excel fornece uma maneira para você funções de saudação tootest que você definiu.  
  
#### <a name="toobrowse-by-using-hello-sales-manager-user-role"></a>toobrowse usando a função de usuário do gerente de vendas Olá  
  
1.  No SSDT, clique em Olá **modelo** menu e clique **analisar no Excel**.  
  
2.  Em **especifique Olá usuário nome ou a função toouse tooconnect toohello modelo**, selecione **função**e, em seguida, Olá caixa de listagem suspensa, selecione **gerente de vendas**e, em seguida, clique em  **Okey**.  
  
    O Excel abre com uma nova pasta de trabalho. Uma tabela dinâmica é criada automaticamente. Olá lista de campos de tabela dinâmica inclui todos os campos de dados Olá disponíveis no novo modelo.  
      
3.  Feche o Excel sem salvar a pasta de trabalho de saudação.  
  
## <a name="whats-next"></a>O que vem a seguir?
Vá toohello próxima lição: [lição 13: implantar](../tutorials/aas-lesson-13-deploy.md).

  
  
  
