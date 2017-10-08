---
título: aaa "lição do tutorial do Azure Analysis Services 1: criar um novo projeto de modelo de tabela | Descrição de Microsoft Docs": descreve como toocreate uma nova análise do Azure Services projeto do tutorial. serviços: documentationcenter do analysis services: ' autor: manager minewiskan: erikre editor: ' marcas: '

MS. AssetID: MS. Service: MS. devlang do analysis services: NA MS. Topic: get-started-article tgt_pltfrm: NA Workload: MS. Date na: 01/06/2017 Author: owend
---
# <a name="lesson-1-create-a-tabular-model-project"></a>Lição 1: criar um projeto de modelo de tabela

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

Nesta lição, você pode usar SQL Server Data Tools (SSDT) toocreate um novo projeto de modelo de tabela no nível de compatibilidade de 1400 hello. Depois de criar o novo projeto, você pode começar a adicionar dados e criar seu modelo. Esta lição fornece um breve introdução toohello criação de modelo tabular ambiente no SSDT.  
  
Estimado tempo toocomplete nesta lição: **10 minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
Este tópico é a primeira lição Olá em um tutorial de criação de modelo tabular. toocomplete lição, existem vários pré-requisitos, você precisa toohave no local. mais, consulte toolearn [Azure Analysis Services – tutorial do Adventure Works](../tutorials/aas-adventure-works-tutorial.md).  
  
## <a name="create-a-new-tabular-model-project"></a>Criar um novo projeto de modelo tabular  
  
#### <a name="toocreate-a-new-tabular-model-project"></a>toocreate um novo projeto de modelo de tabela  
  
1.  No SSDT, Olá **arquivo** menu, clique em **novo** > **projeto**.  
  
2.  Em Olá **novo projeto** caixa de diálogo caixa, expanda **instalado** > **Business Intelligence** > **doAnalysisServices**e, em seguida, clique em **projeto Tabular do Analysis Services**.  
  
3.  Em **nome**, tipo **de vendas pela Internet AW**e, em seguida, especifique um local para arquivos de projeto hello.  
  
    Por padrão, **nome da solução** Olá mesmo como o nome do projeto Olá; no entanto, você pode digitar outro nome de solução.  
  
4.  Clique em **OK**.  
  
5.  Em Olá **designer de modelo Tabular** caixa de diálogo, selecione **integrado de espaço de trabalho**.  
  
    espaço de trabalho Olá hospeda um banco de dados de modelo de tabela com o mesmo nome do projeto Olá durante a criação do modelo de saudação. Espaço de trabalho integrado significa que SSDT usa uma instância interna, eliminando a necessidade de saudação tooinstall uma instância de servidor do Analysis Services separada apenas para a criação do modelo.
      
6.  Em **Nível de compatibilidade**, selecione **SQL Server 2017 / Azure Analysis Services (1400)**.   
 
    ![aas-lesson1-tmd](../tutorials/media/aas-lesson1-tmd.png)
      
    Se você não vir o SQL Server 2017 / Azure Analysis Services (1400) em listbox de nível de compatibilidade hello, você não estiver usando a versão mais recente saudação do SQL Server Data Tools. versão mais recente do tooget hello, consulte [instalar o SQL Server Data tools](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt).  
      
  
## <a name="understanding-hello-ssdt-tabular-model-authoring-environment"></a>Noções básicas sobre o modelo tabular do SSDT Olá ambiente de criação  
Agora que você criou um novo projeto de modelo de tabela, vamos dar um momento tooexplore Olá criação de modelo tabular ambiente no SSDT.  
  
Depois que o projeto é criado, ele é aberto no SSDT. Em Olá lado direito, em **Gerenciador de modelos de tabela**, verá uma exibição de árvore de objetos de saudação em seu modelo. Desde que você ainda não tiver importado dados, pastas Olá estão vazias. Clique um objeto ações da pasta tooperform, barra de menus toohello semelhante. Conforme você percorrer este tutorial, você usar objetos diferentes do toonavigate Olá Gerenciador de modelos de tabela em seu projeto de modelo.

![aas-lesson1-tme](../tutorials/media/aas-lesson1-tme.png)

Clique em Olá **Solution Explorer** guia. Aqui, você verá seu arquivo **Model.bim**. Se você não vir Olá janela designer toohello à esquerda (Olá janela vazia com a guia Model.bim de saudação), em **Solution Explorer**, em **projeto de vendas da Internet AW**, clique duas vezes em Olá  **Model.BIM** arquivo. arquivo Model.bim de saudação contém metadados de saudação de seu projeto de modelo. 

![aas-lesson1-se](../tutorials/media/aas-lesson1-se.png)
  
Clique em **Model.bim**. Em Olá **propriedades** janela, você ver as propriedades de modelo hello, mais importantes do que é hello **o modo DirectQuery** propriedade. Essa propriedade especifica se o modelo de saudação é implantado no modo na memória (desativado) ou no modo DirectQuery (ativado). Para este tutorial, você criará e implantará o modelo no modo Na Memória.

![aas-lesson1-properties](../tutorials/media/aas-lesson1-properties.png)
  
Quando você cria um projeto de modelo, determinadas propriedades de modelo são definidas automaticamente de acordo com toohello configurações de modelagem de dados que podem ser especificadas em Olá **ferramentas** menu > **opções** caixa de diálogo. Propriedades de Backup de dados, retenção de espaço de trabalho e servidor de espaço de trabalho especificam como e onde Olá o banco de dados de espaço de trabalho (o banco de dados de criação de modelo) é feito o backup, retido na memória e compilado. Você pode alterar essas configurações mais tarde se necessário, mas por enquanto, deixe essas propriedades como estão.  

No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Vendas pela Internet da AW** (projeto) e depois clique em **Propriedades**. Olá **páginas de propriedades de vendas de Internet AW** caixa de diálogo é exibida. Você definirá algumas dessas propriedades posteriormente quando implantar seu modelo.  
  
Quando você tiver instalado o SSDT, vários novos itens de menu foram adicionados toohello o ambiente do Visual Studio. Clique em Olá **modelo** menu. A partir daqui, você pode importar dados, atualizar dados de espaço de trabalho, procurar seu modelo no Excel, criar perspectivas e funções, o modo de exibição de modelo selecione Olá e definir opções de cálculo. Clique em Olá **tabela** menu. Daqui em diante, você poderá criar e gerenciar relações, especificar configurações de tabela de data, criar partições e editar propriedades da tabela. Se você clicar em Olá **coluna** menu, você pode adicionar e excluir colunas em uma tabela, congelar colunas e especificar a ordem de classificação. O SSDT também adiciona alguns barra toohello de botões. Mais útil é Olá AutoSoma recurso toocreate uma medida de agregação padrão para uma coluna selecionada. Outros botões da barra de ferramentas fornecem acesso rápido toofrequently usado recursos e comandos.  
  
Explore algumas das caixas de diálogo hello e locais de vários recursos tooauthoring específico para modelos de tabela. Enquanto alguns itens ainda não estiverem ativas, você pode obter uma boa ideia de modelo de tabela Olá ambiente de criação.  
  

## <a name="whats-next"></a>O que vem a seguir?
[Lição 2: obter dados](../tutorials/aas-lesson-2-get-data.md).

  
  
  
