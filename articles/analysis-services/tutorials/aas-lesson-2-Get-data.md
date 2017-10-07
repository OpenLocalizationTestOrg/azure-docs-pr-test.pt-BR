---
título: aaa "lição do tutorial do Azure Analysis Services 2: obter dados | Descrição de Microsoft Docs": descreve como tooget e importar dados em Olá projeto do tutorial do Azure Analysis Services. serviços: documentationcenter do analysis services: ' autor: manager minewiskan: erikre editor: ' marcas: '

MS. AssetID: MS. Service: MS. devlang do analysis services: NA MS. Topic: get-started-article tgt_pltfrm: NA Workload: MS. Date na: 01/06/2017 Author: owend
---

# <a name="lesson-2-get-data"></a>Lição 2: obter dados

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Nesta lição, você usa obter dados no banco de dados de exemplo do tooconnect toohello AdventureWorksDW2014 SSDT, selecione os dados, visualizar e filtrar e, em seguida, importa para seu espaço de trabalho do modelo.  
  
Pelo uso do Obter Dados, você pode importar dados de uma ampla variedade de fontes: Banco de Dados SQL do Azure, Oracle, Sybase, OData Feed, Teradata, arquivos e muito mais. Os dados também podem ser consultados usando uma expressão de fórmula Power Query M.
  
Estimado tempo toocomplete nesta lição: **10 minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem. Antes de executar tarefas de saudação nesta lição, você deverá ter completado lição anterior Olá: [lição 1: criar um novo projeto de modelo de tabela](../tutorials/aas-lesson-1-create-a-new-tabular-model-project.md).  
  
## <a name="create-a-connection"></a>Criar uma conexão  
  
#### <a name="toocreate-a-connection-toohello-adventureworksdw2014-database"></a>toocreate um banco de dados de toohello AdventureWorksDW2014 de conexão  
  
1.  No Gerenciador de Modelos tabulares, clique com o botão direito do mouse em **Fontes de Dados** > **Importar de Fonte de Dados**.  
  
    Obter dados, que guiará você por meio da fonte de dados tooa conexão é iniciado. Se você não vir o Gerenciador de modelos de tabela, em **Solution Explorer**, clique duas vezes em **Model.bim** tooopen modelo de saudação no designer de saudação. 
    
    ![aas-lesson2-getdata](../tutorials/media/aas-lesson2-getdata.png)
  
2.  Em Obter Dados, clique em **Banco de Dados** > **Banco de Dados do SQL Server** > **Conectar**.  
  
3.  Em Olá **o banco de dados do SQL Server** caixa de diálogo, na **servidor**, digite o nome de saudação do servidor de saudação onde você instalou o banco de dados de saudação AdventureWorksDW2014 e, em seguida, clique em **conectar**.  

4.  Quando solicitado tooenter credenciais, você precisa ter credenciais de saudação toospecify tooconnect toohello fonte de dados ao importar e processar dados do Analysis Services usa. Em **Modo de Representação**, selecione **Representar Conta** e, em seguida, insira as credenciais e clique em **Conectar**. É recomendável que usar uma conta em que as senhas de saudação não expiram.

    ![aas-lesson2-account](../tutorials/media/aas-lesson2-account.png)
  
    > [!NOTE]  
    > Usar uma conta de usuário do Windows e senha fornece o método mais seguro hello conexão tooa da fonte de dados.
  
5.  No navegador, selecione Olá **AdventureWorksDW2014** banco de dados e, em seguida, clique em **Okey**. Isso cria o banco de dados do hello conexão toohello. 
  
6.  No navegador, selecione Olá a caixa de seleção para Olá tabelas a seguir: **DimCustomer**, **DimDate**, **DimGeography**, **DimProduct**,  **DimProductCategory**, **DimProductSubcategory**, e **FactInternetSales**.  

    ![aas-lesson2-select-tables](../tutorials/media/aas-lesson2-select-tables.png)
  
Depois que você clicar em OK, o Editor de Consultas será aberto. Na próxima seção, Olá, você seleciona somente os dados de saudação tooimport desejado.

  
## <a name="filter-hello-table-data"></a>Filtrar dados da tabela Olá  
Tabelas no banco de dados do exemplo hello AdventureWorksDW2014 tem dados que não seja necessário tooinclude em seu modelo. Quando possível, você deseja toofilter espaço de na memória toosave desnecessária de dados usado pelo modelo de saudação. Você filtrará algumas das Olá colunas de tabelas para não importação para o banco de dados de espaço de trabalho de saudação ou banco de dados de modelo Olá após ele ter sido implantado. 
  
#### <a name="toofilter-hello-table-data-before-importing"></a>dados da tabela toofilter Olá antes de importar  
  
1.  No Editor de consultas, selecione Olá **DimCustomer** tabela. Uma exibição de tabela DimCustomer Olá Olá datasource (seus dados de exemplo AdventureWorksDWQ2014) é exibida. 
  
2.  Faça uma seleção múltipla (Ctrl + clique) de **SpanishEducation**, **FrenchEducation**, **SpanishOccupation** e **FrenchOccupation** e, em seguida, clique com o botão direito do mouse e clique em **Remover Colunas**. 

    ![aas-lesson2-remove-columns](../tutorials/media/aas-lesson2-remove-columns.png)
  
    Como valores de saudação para essas colunas não são relevantes tooInternet análise de vendas, há tooimport sem necessidade dessas colunas. A eliminação das colunas desnecessárias torna seu modelo menor e mais eficiente.  
  
4.  Filtre Olá restantes tabelas removendo Olá colunas em cada tabela a seguir:  
    
    **DimDate**
    
      |Coluna|  
      |--------|  
      |DateKey|  
      |**SpanishDayNameOfWeek**|  
      |**FrenchDayNameOfWeek**|  
      |**SpanishMonthName**|  
      |**FrenchMonthName**|  
  
    **DimGeography**
  
      |Coluna|  
      |-------------|  
      |**SpanishCountryRegionName**|  
      |**FrenchCountryRegionName**|  
      |**IpAddressLocator**|  
  
    **DimProduct**
  
      |Coluna|  
      |-----------|  
      |**SpanishProductName**|  
      |**FrenchProductName**|  
      |**FrenchDescription**|  
      |**ChineseDescription**|  
      |**ArabicDescription**|  
      |**HebrewDescription**|  
      |**ThaiDescription**|  
      |**GermanDescription**|  
      |**JapaneseDescription**|  
      |**TurkishDescription**|  
  
    **DimProductCategory**
  
      |Coluna|  
      |--------------------|  
      |**SpanishProductCategoryName**|  
      |**FrenchProductCategoryName**|  
  
    **DimProductSubcategory**
  
      |Coluna|  
      |-----------------------|  
      |**SpanishProductSubcategoryName**|  
      |**FrenchProductSubcategoryName**|  
  
    **FactInternetSales**
  
      |Coluna|  
      |------------------|  
      |**OrderDateKey**|  
      |**DueDateKey**|  
      |**ShipDateKey**|   
  
## <a name="Import"></a>Saudação de importação selecionar tabelas e os dados da coluna  
Agora que você visualizou e filtrou os dados desnecessários, você pode importar restante Olá Olá dados. Assistente de saudação importa dados da tabela Olá junto com as relações entre tabelas. Novas tabelas e colunas são criadas no modelo de saudação e não é possível importar dados que você filtrou.  
  
#### <a name="tooimport-hello-selected-tables-and-column-data"></a>Olá tooimport selecionar tabelas e os dados da coluna  
  
1.  Examine suas seleções. Se tudo estiver ok, clique em **Importar**. caixa de diálogo de processamento de dados Olá mostra o status de saudação de dados sendo importados de sua fonte de dados para seu banco de dados do espaço de trabalho.
  
    ![aas-lesson2-success](../tutorials/media/aas-lesson2-success.png) 
  
2.  Clique em **fechar**  

  
## <a name="save-your-model-project"></a>Salvar o projeto de modelo  
É importante toofrequently salvar seu projeto de modelo.  
  
#### <a name="toosave-hello-model-project"></a>projeto de modelo de saudação toosave  
  
-   Clique em **Arquivo** > **Salvar Tudo**.  
  
## <a name="whats-next"></a>O que vem a seguir?
[Lição 3: marcar como tabela de data](../tutorials/aas-lesson-3-mark-as-date-table.md).

  
  
