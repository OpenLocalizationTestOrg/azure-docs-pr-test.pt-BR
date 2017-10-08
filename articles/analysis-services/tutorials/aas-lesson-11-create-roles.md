---
título: aaa "lição do tutorial do Azure Analysis Services 11: criar funções | Descrição de Microsoft Docs": descreve como funções toocreate Olá projeto do tutorial do Azure Analysis Services. serviços: documentationcenter do analysis services: ' autor: manager minewiskan: erikre editor: ' marcas: '

MS. AssetID: MS. Service: MS. devlang do analysis services: NA MS. Topic: get-started-article tgt_pltfrm: NA Workload: MS. Date na: 26/05/2017 Author: owend
---
# <a name="lesson-11-create-roles"></a>Lição 11: criar funções

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Nesta lição, você cria funções. As funções fornecem segurança de dados e de objetos de banco de dados de modelo, limitando o acesso tooonly aos usuários que são membros da função. Cada função é definida com uma única permissão: Nenhum, Leitura, Leitura e Processo, Processo ou Administrador. Funções podem ser definidas durante a criação do modelo usando o Gerenciador de Funções. Depois que um modelo tiver sido implantado, você poderá gerenciar funções usando o SQL Server Management Studio (SSMS). mais, consulte toolearn [funções](https://docs.microsoft.com/sql/analysis-services/tabular-models/roles-ssas-tabular).
  
> [!NOTE]  
> Criação de funções é toocomplete não é necessário neste tutorial. Por padrão, a conta Olá com que você está conectado tem privilégios de administrador no modelo de saudação. No entanto, para outros usuários na toobrowse sua organização usando um cliente de relatório, você deve criar pelo menos uma função com leitura permissões e adicione esses usuários como membros.  
  
Você cria três funções:  
  
-   **Gerente de vendas** – essa função pode incluir usuários em sua organização para o qual você deseja toohave leitura permissão tooall objetos e dados modelo.  
  
-   **Analista de vendas dos EUA** – essa função pode incluir usuários em sua organização para o qual você deseja que apenas os dados de toobrowse capaz de toobe relacionados toosales em Olá dos Estados Unidos. Para essa função, você usar um toodefine de fórmula do DAX um *filtro de linha*, que restringe os membros toobrowse somente os dados do hello dos Estados Unidos.  
  
-   **Administrador** – essa função pode incluir os usuários para o qual você deseja toohave permissão de administrador, que permite acesso ilimitado e permissões de tarefas administrativas tooperform no banco de dados de modelo de saudação.  
  
Como contas de usuário e grupo do Windows em sua organização são exclusivas, você pode adicionar contas de toomembers sua organização. No entanto, para este tutorial, você também pode deixar os membros de saudação em branco. Testar o efeito de saudação de cada função posteriormente na lição 12: analisar no Excel.  
  
Estimado tempo toocomplete nesta lição: **15 minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem. Antes de executar tarefas de saudação nesta lição, você deverá ter completado lição anterior Olá: [lição 10: criar partições](../tutorials/aas-lesson-10-create-partitions.md).  
  
## <a name="create-roles"></a>Criar funções  
  
#### <a name="toocreate-a-sales-manager-user-role"></a>toocreate uma função de usuário do gerente de vendas  
  
1.  No Gerenciador de Modelos tabular, clique com o botão direito do mouse em **Funções** > **Funções**.  
  
2.  No Gerenciador de Funções, clique em **Novo**.  
  
3.  Clique em nova função de Olá e, em seguida, em Olá **nome** coluna, renomeie a função hello muito**gerente de vendas**.  
  
4.  Em Olá **permissões** coluna, clique em lista suspensa de saudação e selecione Olá **leitura** permissão. 

    ![aas-lesson11-new-role](../tutorials/media/aas-lesson11-new-role.png) 
  
5.  Opcional: Clique em Olá **membros** guia e, em seguida, clique em **adicionar**. Em Olá **selecionar usuários ou grupos** caixa de diálogo caixa, digite os usuários do Windows hello ou grupos da sua organização deseja tooinclude na função hello.  
  
#### <a name="toocreate-a-sales-analyst-us-user-role"></a>toocreate uma função de usuário analista de vendas dos EUA  
  
1.  No Gerenciador de Funções, clique em **Novo**.    
  
2.  Renomeie a função hello muito**analista de vendas dos EUA**.  
  
3.  Dê a essa função a permissão **Leitura**.  
  
4.  Guia de filtros de linha hello e, em seguida, para Olá **DimGeography** tabela somente na coluna de filtro DAX hello, Olá tipo seguinte fórmula:  
  
    ```Administrator
    =DimGeography[CountryRegionCode] = "US" 
    ```
    
    Fórmula de um filtro de linha deve resolver tooa valor de booliano (verdadeiro/falso). Com essa fórmula, você está especificando que somente as linhas com valor de código de região de país do hello "US" estão visíveis toohello usuário.  
    ![aas-lesson11-role-filter](../tutorials/media/aas-lesson11-role-filter.png) 
  
6.  Opcional: Clique em Olá **membros** guia e, em seguida, clique em **adicionar**. Em Olá **selecionar usuários ou grupos** caixa de diálogo caixa, digite os usuários do Windows hello ou grupos da sua organização deseja tooinclude na função hello.  
  
#### <a name="toocreate-an-administrator-user-role"></a>toocreate uma função de usuário administrador  
  
1.  Clique em **Novo**.  
  
2.  Renomeie a função hello muito**administrador**.  
  
3.  Dê permissão de **Administrador** a essa função.  
  
4.  Opcional: Clique em Olá **membros** guia e, em seguida, clique em **adicionar**. Em Olá **selecionar usuários ou grupos** caixa de diálogo caixa, digite os usuários do Windows hello ou grupos da sua organização deseja tooinclude na função hello. 
  
  
## <a name="whats-next"></a>O que vem a seguir?
[Lição 12: Analisar no Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).

  
  
