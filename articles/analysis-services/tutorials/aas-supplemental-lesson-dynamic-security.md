---
título: aaa "lição suplementar do tutorial do Azure Analysis Services: segurança dinâmica | Descrição de Microsoft Docs": descreve como os filtros de segurança dinâmica em toouse usando a linha no tutorial do hello Azure Analysis Services.
serviços: documentationcenter do analysis services: ' autor: manager minewiskan: erikre editor: ' marcas: '

MS. AssetID: MS. Service: MS. devlang do analysis services: NA MS. Topic: get-started-article tgt_pltfrm: NA Workload: MS. Date na: 26/05/2017 Author: owend
---
# <a name="supplemental-lesson---dynamic-security"></a>Lição suplementar – segurança dinâmica

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Nesta lição suplementar, você cria uma função adicional que implementa a segurança dinâmica. Segurança dinâmica oferece segurança no nível de linha com base na id de nome ou o logon de usuário de saudação do usuário Olá conectado no momento. 
  
segurança dinâmica em tooimplement, adicionar um modelo de tooyour de tabela que contém os nomes de usuário Olá desses usuários que podem conectar-se o modelo de toohello e procurar dados e objetos de modelo. modelo Olá que você cria usando este tutorial está no contexto de saudação do Adventure Works; No entanto, toocomplete esta lição, você deve adicionar uma tabela que contém os usuários de seu próprio domínio. Não é necessário senhas Olá Olá para nomes de usuário que são adicionados. toocreate uma tabela EmployeeSecurity, com uma pequena amostra dos usuários de seu próprio domínio, você usa Olá recurso de colar, colando dados de funcionários de uma planilha do Excel. Em um cenário do mundo real, tabela Olá contendo nomes de usuário normalmente seria uma tabela de banco de dados real como uma fonte de dados; Por exemplo, uma tabela DimEmployee real.  
  
segurança dinâmica em tooimplement, você usar duas funções DAX: [função USERNAME (DAX)](http://msdn.microsoft.com/22dddc4b-1648-4c89-8c93-f1151162b93f) e [função LOOKUPVALUE (DAX)](http://msdn.microsoft.com/73a51c4d-131c-4c33-a139-b1342d10caab). Essas funções, aplicadas em uma fórmula de filtro de linha, são definidas em uma nova função. Usando a função LOOKUPVALUE hello, fórmula Olá Especifica um valor de tabela de EmployeeSecurity hello. fórmula de Hello, em seguida, passa a função USERNAME toohello de valor, que especifica o nome de usuário saudação do usuário Olá conectado pertence toothis função. Olá usuário pode procurar apenas nos dados especificados pelos filtros de linha da função hello. Nesse cenário, você especificar que os funcionários de vendas só podem procurar dados de vendas pela Internet para territórios de vendas Olá no qual eles são membros.  
  
As tarefas que são exclusivos toothis cenário de modelo de tabela do Adventure Works, mas não seriam aplicariam necessariamente o cenário do mundo real tooa são identificadas como tal. Cada tarefa inclui informações adicionais que descreve a finalidade de saudação da tarefa de saudação.  
  
Estimado tempo toocomplete nesta lição: **30 minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
Este tópico de lição suplementar faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem. Antes de executar tarefas de saudação nesta lição suplementar, você deve concluir todas as lições anteriores.  
  
## <a name="add-hello-dimsalesterritory-table-toohello-aw-internet-sales-tabular-model-project"></a>Adicionar Olá DimSalesTerritory tabela toohello projeto de modelo Tabular do AW Internet Sales  
tooimplement segurança dinâmica para este cenário do Adventure Works, você deve adicionar o modelo de tooyour duas tabelas adicionais. tabela do primeiro Olá você adicionar é DimSalesTerritory (como Sales Territory) do hello mesmo banco de dados AdventureWorksDW. Você aplicar posteriormente uma tabela de SalesTerritory de toohello de filtro de linha que define os dados específicos de saudação saudação do usuário conectada pode procurar.  
  
#### <a name="tooadd-hello-dimsalesterritory-table"></a>tabela de DimSalesTerritory tooadd Olá  
  
1.  Em Gerenciador de Modelos tabulares > **Fontes de Dados**, clique com o botão direito do mouse em sua conexão e clique em **Importar Novas Tabelas**.  

    Se for exibida a caixa de diálogo de credenciais de representação Olá, digite as credenciais de representação de saudação usado na lição 2: adicionar dados.
  
2.  No navegador, selecione Olá **DimSalesTerritory** de tabela e, em seguida, clique em **Okey**.    
  
3.  No Editor de consultas, clique em Olá **DimSalesTerritory** de consulta e, em seguida, remover **SalesTerritoryAlternateKey** coluna.  
  
7.  Clique em **Importar**.  
  
    Olá nova tabela será adicionada toohello espaço de trabalho do modelo. Objetos e dados Olá DimSalesTerritory da tabela de origem, em seguida, são importados para o modelo de tabela de vendas de Internet AW.  
  
9. Depois de tabela Olá foi importada com êxito, clique em **fechar**.  

## <a name="add-a-table-with-user-name-data"></a>Adicionar uma tabela com os dados de nome de usuário  
tabela do Hello DimEmployee no banco de dados do exemplo hello AdventureWorksDW contém usuários do domínio de AdventureWorks da saudação. Esses nomes de usuários não existem em seu ambiente. Você deve criar uma tabela em seu modelo que contenha um exemplo pequeno (pelo menos três) de usuários reais de sua organização. Você, em seguida, adicionar esses usuários como nova função de toohello de membros. Você não precisa senhas Olá para nomes de usuário de exemplo hello, mas é necessário nomes de usuário do Windows reais de seu próprio domínio.  
  
#### <a name="tooadd-an-employeesecurity-table"></a>tooadd uma tabela EmployeeSecurity  
  
1.  Abra o Microsoft Excel e crie uma planilha.  
  
2.  Copie Olá tabela, incluindo a linha de cabeçalho hello, a seguir e cole-o na planilha de saudação.  

    ```
      |EmployeeId|SalesTerritoryId|FirstName|LastName|LoginId|  
      |---------------|----------------------|--------------|-------------|------------|  
      |1|2|<user first name>|<user last name>|\<domain\username>|  
      |1|3|<user first name>|<user last name>|\<domain\username>|  
      |2|4|<user first name>|<user last name>|\<domain\username>|  
      |3|5|<user first name>|<user last name>|\<domain\username>|  
    ```

3.  Substitua saudação primeiro nome, sobrenome e domínio ome de usuário com nomes de saudação e ids de logon de três usuários em sua organização. Colocar Olá mesmo usuário em Olá duas primeiras linhas, para 1 EmployeeId, mostrando a este usuário pertence toomore que um território de vendas. Deixe Olá campos EmployeeId e SalesTerritoryId como estão.  
  
4.  Salvar a planilha hello como **SampleEmployee**.  
  
5.  Na planilha de hello, selecione todas as células de saudação com dados de funcionário, incluindo os cabeçalhos de hello, em seguida, clique dados saudação selecionado e, em seguida, clique em **cópia**.  
  
6.  No SSDT, clique em Olá **editar** menu e clique **colar**.  
  
    Se colar estiver esmaecido, clique em qualquer coluna em qualquer tabela na janela de designer de modelo hello e tente novamente.  
  
7.  Em Olá **visualização de colagem** na caixa **nome de tabela**, tipo **EmployeeSecurity**.  
  
8.  Em **toobe dados colado**, verifique se dados saudação incluem todos os dados de saudação do usuário e cabeçalhos de planilha de SampleEmployee hello.  
  
9. Verifique se a opção **Usar primeira linha como cabeçalhos de coluna** está marcada e clique em **Ok**.  
  
    Uma nova tabela denominada EmployeeSecurity com dados de funcionário copiados da planilha de SampleEmployee Olá é criada.  
  
## <a name="create-relationships-between-factinternetsales-dimgeography-and-dimsalesterritory-table"></a>Criar relações entre as tabelas FactInternetSales, DimGeography e DimSalesTerritory  
Olá FactInternetSales, DimGeography e DimSalesTerritory tabelas contém uma coluna comum, SalesTerritoryId. coluna de SalesTerritoryId de saudação na tabela de DimSalesTerritory Olá contém valores com uma Id diferente para cada região de vendas.  
  
#### <a name="toocreate-relationships-between-hello-factinternetsales-dimgeography-and-hello-dimsalesterritory-table"></a>relações de toocreate entre Olá FactInternetSales, DimGeography e tabela de DimSalesTerritory Olá  
  
1.  Na exibição de diagrama no hello **DimGeography** de tabela, clique e mantenha Olá **SalesTerritoryId** coluna, em seguida, arraste Olá cursor toohello **SalesTerritoryId** coluna Olá **DimSalesTerritory** de tabela e, em seguida, solte.  
  
2.  Em Olá **FactInternetSales** de tabela, clique e mantenha Olá **SalesTerritoryId** coluna, em seguida, arraste Olá cursor toohello **SalesTerritoryId** coluna Olá  **DimSalesTerritory** da tabela e, em seguida, solte.  
  
    Olá aviso propriedade ativa desta relação é False, o que significa que ele está inativo. tabela de FactInternetSales Olá já tem outra relação ativa.  
  
## <a name="hide-hello-employeesecurity-table-from-client-applications"></a>Ocultar Olá EmployeeSecurity tabela de aplicativos cliente  
Nesta tarefa, você ocultar tabela de EmployeeSecurity hello, impedindo que ela apareça na lista de campos de um aplicativo cliente. Lembre-se de que a ocultação de uma tabela não a protege. Se souberem como, os usuários ainda poderão consultar os dados da tabela EmployeeSecurity. toosecure Olá EmployeeSecurity dados da tabela, impedindo que os usuários que estão sendo tooquery capaz de qualquer um dos seus dados, aplicar um filtro em uma tarefa posterior.  
  
#### <a name="toohide-hello-employeesecurity-table-from-client-applications"></a>tabela de EmployeeSecurity toohide Olá de aplicativos cliente  
  
-   No designer de modelo hello, na exibição de diagrama, clique com botão direito Olá **funcionário** cabeçalho de tabela e, em seguida, clique em **ocultar das ferramentas de cliente**.  
  
## <a name="create-a-sales-employees-by-territory-user-role"></a>Criar uma função de usuário de Funcionários de Vendas por Região  
Nesta tarefa, você deve criar uma função de usuário. Essa função inclui um filtro de linha que define quais linhas da tabela de DimSalesTerritory Olá são toousers visível. Olá filtro é aplicado em relação um-para-muitos da saudação direção tooall outras tabelas relacionada tooDimSalesTerritory. Você também pode aplicar um filtro que protege a tabela de consulta por qualquer usuário que seja membro da função de saudação do hello inteira EmployeeSecurity.  
  
> [!NOTE]  
> Olá funcionários de vendas por função Territory criada nesta lição restringe os membros toobrowse (consulta) apenas dados de vendas ou para Olá território de vendas toowhich pertencem. Se você adicionar um usuário como um membro toohello funcionários de vendas pela função de território que também existe como um membro em uma função criada em [lição 11: criar funções](../tutorials/aas-lesson-11-create-roles.md), você obtém uma combinação de permissões. Quando um usuário for um membro de várias funções, permissões de saudação e filtros de linha definidos para cada função serão cumulativas. Ou seja, o usuário Olá tem permissões de maior Olá determinadas pela combinação de saudação de funções.  
  
#### <a name="toocreate-a-sales-employees-by-territory-user-role"></a>toocreate um funcionários de vendas por função de usuário de território  
  
1.  No SSDT, clique em Olá **modelo** menu e clique **funções**.  
  
2.  No **Gerenciador de Funções**, clique em **Novo**.  
  
    Uma nova função com hello nenhuma permissão é adicionado toohello lista.  
  
3.  Clique em nova função de Olá e, em seguida, em Olá **nome** coluna, renomeie a função hello muito**funcionários de vendas por território**.  
  
4.  Em Olá **permissões** coluna, clique em lista suspensa de saudação e selecione Olá **leitura** permissão.  
  
5.  Clique em Olá **membros** guia e, em seguida, clique em **adicionar**.  
  
6.  Em Olá **Selecionar usuário ou grupo** na caixa **objeto de saudação Enter denominado tooselect**, tipo hello primeiro exemplo nome de usuário usado ao criar a tabela de EmployeeSecurity hello. Clique em **verificar nomes** tooverify nome de usuário de saudação é válido e, em seguida, clique em **Okey**.  
  
    Repita essa etapa, adicionando Olá outros exemplos de nomes de usuário usado ao criar a tabela de EmployeeSecurity hello.  
  
7.  Clique em Olá **filtros de linha** guia.  
  
8.  Para Olá **EmployeeSecurity** tabela Olá **filtro DAX** coluna, Olá tipo seguinte fórmula:  
  
    ```
      =FALSE()  
    ```
  
    Esta fórmula Especifica que todas as colunas são resolvidas condição booliana false de toohello. Nenhuma coluna da tabela de EmployeeSecurity Olá pode ser consultada por um membro da saudação funcionários de vendas por função de usuário de território.  
  
9. Para Olá **DimSalesTerritory** tabela, Olá tipo seguinte fórmula:  

    ```  
    ='Sales Territory'[Sales Territory Id]=LOOKUPVALUE('Employee Security'[Sales Territory Id], 
      'Employee Security'[Login Id], USERNAME(), 
      'Employee Security'[Sales Territory Id], 
      'Sales Territory'[Sales Territory Id]) 
    ```
  
    Nesta fórmula, Olá função LOOKUPVALUE retorna todos os valores para a coluna de DimEmployeeSecurity [SalesTerritoryId] hello, onde hello EmployeeSecurity [LoginId] é Olá mesmo como Olá atual do logon de nome de usuário do Windows e EmployeeSecurity [ SalesTerritoryId] é Olá igual a saudação DimSalesTerritory [SalesTerritoryId].  
  
    Olá conjunto de IDs de território de vendas retornado por LOOKUPVALUE é usado toorestrict Olá linhas mostradas na tabela DimSalesTerritory de saudação. Somente as linhas onde hello SalesTerritoryID para linha hello está no conjunto de saudação de IDs retornadas pela função LOOKUPVALUE de saudação são exibidas.  
  
10. Em Gerenciador de Funções, clique em **Ok**.  
  
## <a name="test-hello-sales-employees-by-territory-user-role"></a>Olá funcionários de vendas por território de função de usuário de teste  
Nesta tarefa, você pode usar Olá analisar no recurso do Excel no SSDT tootest Olá eficácia Olá funcionários de vendas por função de usuário de território. Especifique uma saudação nomes de usuário que você adicionou toohello EmployeeSecurity tabela e como um membro da função de saudação. Este nome de usuário, em seguida, é usado como nome de usuário efetivo Olá na conexão Olá criada entre o modelo do Excel e hello.  
  
#### <a name="tootest-hello-sales-employees-by-territory-user-role"></a>Olá tootest funcionários de vendas por função de usuário de território  
  
1.  No SSDT, clique em Olá **modelo** menu e clique **analisar no Excel**.  
  
2.  Em Olá **analisar no Excel** na caixa **especifique Olá usuário nome ou a função toouse tooconnect toohello modelo**, selecione **outro usuário do Windows**e, em seguida, clique em **Procurar**.  
  
3.  Em Olá **Selecionar usuário ou grupo** na caixa **digite Olá objeto nome tooselect**, digite um nome de usuário incluídos na tabela de EmployeeSecurity hello e, em seguida, clique em **verificar nomes**.  
  
4.  Clique em **Okey** tooclose Olá **Selecionar usuário ou grupo** caixa de diálogo e clique **Okey** tooclose Olá **analisar no Excel** caixa de diálogo.  
  
    O Excel abre com uma nova pasta de trabalho. Uma tabela dinâmica é criada automaticamente. Olá lista PivotTable Fields inclui a maioria Olá de campos de dados disponíveis no novo modelo.  
  
    Tabela de EmployeeSecurity de saudação aviso não é visível no hello lista PivotTable Fields. Você ocultou essa tabela das ferramentas de cliente em uma tarefa anterior.  
  
5.  Em Olá **campos** listar, **∑ Internet Sales** (medidas), selecione Olá **InternetTotalSales** medidas. medida de saudação é inserida no hello **valores** campos.  
  
6.  Selecione Olá **SalesTerritoryId** coluna da saudação **DimSalesTerritory** tabela. coluna de saudação é inserida no hello **rótulos de linha** campos.  
  
    Aviso Internet vendas aparecem apenas para Olá uma região toowhich Olá efetivo nome de usuário usado pertence. Se você selecionar outra coluna, como cidade da tabela de DimGeography hello como campo Row Label, cidades apenas no usuário efetivo do Olá Olá território de vendas toowhich pertence são exibidos.  
  
    Este usuário não pode pesquisar ou consultar quaisquer dados de vendas da Internet para regiões que não sejam Olá um pertencerem a. Essa restrição é porque o filtro de linha definido para a tabela de DimSalesTerritory hello, em Olá funcionários de vendas por função de usuário de território, hello protege os dados para todos os dados relacionados tooother territórios de vendas.  
  
## <a name="see-also"></a>Consulte também  
[Função USERNAME (DAX)](https://msdn.microsoft.com/library/hh230954.aspx)  
[Função LOOKUPVALUE (DAX)](https://msdn.microsoft.com/library/gg492170.aspx)  
[Função CUSTOMDATA (DAX)](https://msdn.microsoft.com/library/hh213140.aspx)  