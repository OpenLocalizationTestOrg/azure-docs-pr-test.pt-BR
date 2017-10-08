---
title: "aaaConnect tooAzure Cosmos banco de dados usando ferramentas de análise de BI | Microsoft Docs"
description: "Saiba como toouse hello Azure Cosmos banco de dados ODBC driver toocreate tabelas e exibições para que dados normalizados podem ser exibidos no software de análise de BI e dados."
keywords: odbc, driver odbc
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 9967f4e5-4b71-4cd7-8324-221a8c789e6b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: rest-api
ms.topic: article
ms.date: 05/24/2017
ms.author: mimig
ms.openlocfilehash: e12a70f7805445f09fac01411e4bfbccc9a29c7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooazure-cosmos-db-using-bi-analytics-tools-with-hello-odbc-driver"></a>Conecte-se tooAzure Cosmos banco de dados usando ferramentas de análise de BI com o driver ODBC Olá

o driver permite Hello Azure Cosmos banco de dados ODBC que você tooAzure tooconnect Cosmos DB usando a análise de BI ferramentas como o SQL Server Integration Services, Power BI Desktop e Tableau para que você pode analisar e criar visualizações de seus dados do banco de dados do Azure Cosmos nessas soluções.

driver de ODBC de banco de dados do Azure Cosmos Olá é compatível com o ODBC 3.8 e oferece suporte à sintaxe ANSI SQL-92. Olá driver oferece recursos avançados toohelp renormalize dados no banco de dados do Azure Cosmos. Usando o driver hello, você pode representar dados no banco de dados do Azure Cosmos como tabelas e exibições. Olá driver permite operações de SQL tooperform em tabelas de saudação e modos de exibição como agrupar por consultas, inserções, atualizações e exclusões.

## <a name="why-do-i-need-toonormalize-my-data"></a>Por que preciso toonormalize meus dados?
Banco de dados do Azure Cosmos é um banco de dados schemaless, para que ele permite o rápido desenvolvimento de aplicativos, permitindo que aplicativos tooiterate seus dados rapidamente Olá de modelo e não confinar esquema estrita tooa. Um único banco de dados do Azure Cosmos DB pode conter documentos JSON de várias estruturas. Isso é ótimo para desenvolvimento rápido de aplicativos, mas quando você quiser tooanalyze e cria relatórios de seus dados usando a análise de dados e ferramentas de BI, dados saudação geralmente precisa toobe bidimensionais e aderem tooa específica de esquema.

Isso é aqui que entra o driver ODBC hello. Usando o driver ODBC hello, você pode agora renormalized dados no banco de dados do Azure Cosmos em tabelas e exibições, ajuste tooyour dados analíticos e de relatório precisa. esquemas Olá renormalized não têm impacto sobre Olá dados subjacentes e não restringir os desenvolvedores tooadhere toothem, elas simplesmente permitem que você tooleverage compatível com ODBC ferramentas tooaccess Olá dados. Agora seu banco de dados do Azure Cosmos DB não será apenas um favorito de sua equipe de desenvolvimento, mas seus analistas de dados vão adorá-lo também.

Agora permite começar com o driver ODBC hello.

## <a id="install"></a>Etapa 1: Instalar o driver de ODBC de banco de dados do Azure Cosmos Olá

1. Baixe drivers de saudação para seu ambiente:

    * [Microsoft Azure Cosmos DB ODBC 64-bit.msi](https://aka.ms/documentdb-odbc-64x64) para Windows de 64 bits
    * [Microsoft Azure Cosmos DB ODBC 32x64-bit.msi](https://aka.ms/documentdb-odbc-32x64) para 32 bits no Windows de 64 bits
    * [Microsoft Azure Cosmos DB ODBC 32-bit.msi](https://aka.ms/documentdb-odbc-32x32) para Windows de 32 bits

    Olá execução msi arquivo localmente, quais Olá inicia **Assistente de instalação do Microsoft Azure Cosmos banco de dados ODBC Driver**. 
2. Conclua o Assistente de instalação de saudação usando o driver ODBC do saudação padrão tooinstall entrada hello.
3. Olá abrir **administrador de fonte de dados ODBC** aplicativo no seu computador, você pode fazer isso digitando **fontes de dados ODBC** no Windows hello caixa de pesquisa. 
    Você pode confirmar Olá instalado clicando Olá **Drivers** guia e garantindo **Driver ODBC do Microsoft Azure Cosmos DB** está listado.

    ![Administrador de fonte de dados ODBC do Azure Cosmos DB](./media/odbc-driver/odbc-driver.png)

## <a id="connect"></a>Etapa 2: Conectar-se o banco de dados de banco de dados do Azure Cosmos tooyour

1. Depois de [instalando hello Azure Cosmos banco de dados ODBC driver](#install), em Olá **administrador de fonte de dados ODBC** janela, clique em **adicionar**. Você pode criar um DSN de usuário ou de sistema. Neste exemplo, estamos criando um DSN de usuário.
2. Em Olá **criar nova fonte de dados** janela, selecione **Driver ODBC do Microsoft Azure Cosmos DB**e, em seguida, clique em **concluir**.
3. Em Olá **Azure Cosmos banco de dados ODBC Driver SDN instalação** janela, preencha o seguinte hello: 

    ![Janela Configuração de DSN do Driver ODBC do Azure Cosmos DB](./media/odbc-driver/odbc-driver-dsn-setup.png)
    - **Nome da fonte de dados**: seu próprio nome amigável para Olá DSN ODBC. Esse nome é a conta de banco de dados do Azure Cosmos tooyour exclusivo, portanto denomine corretamente se você tiver várias contas.
    - **Descrição**: uma breve descrição da fonte de dados de saudação.
    - **Host**: URI de sua conta do Azure Cosmos DB. Você pode recuperar isso na folha de chaves de banco de dados do Azure Cosmos Olá no hello portal do Azure, conforme mostrado no hello captura de tela a seguir. 
    - **Chave de acesso**: Olá chave primária ou secundária, leitura / gravação ou somente leitura da folha de chaves de banco de dados do Azure Cosmos Olá no hello portal do Azure, conforme mostrado no hello captura de tela a seguir. Recomendamos que você use chave Olá de somente leitura se Olá DSN é usado para processamento de dados somente leitura e relatórios.
    ![Folha Chaves do Azure Cosmos DB](./media/odbc-driver/odbc-driver-keys.png)
    - **Criptografar a chave de acesso para**: selecionar melhor opção de saudação com base em usuários Olá dessa máquina. 
4. Clique em Olá **teste** botão toomake-se de que você pode se conectar a conta de banco de dados do Azure Cosmos tooyour. 
5. Clique em **opções avançadas** e saudação do conjunto de valores a seguir:
    - **Consistência de consulta**: selecione Olá [nível de consistência](consistency-levels.md) para suas operações. saudação padrão é sessão.
    - **Número de repetições**: Olá número de vezes tooretry uma operação se solicitação de saudação inicial não for concluída devido a limitação de tooservice.
    - **Arquivo de Esquema**: você tem várias opções aqui.
        - Por padrão, deixar essa entrada conforme é (em branco), o driver Olá verifica primeiro dados da página Olá para todos os esquemas de saudação toodetermine de coleções de cada coleção. Isso é conhecido como Mapeamento de Coleção. Sem um arquivo de esquema definido, o driver de saudação tem tooperform Olá verificação para cada sessão de driver e pode resultar em um tempo de um aplicativo usando Olá DSN de inicialização mais alto. É recomendável sempre associar um arquivo de esquema para um DSN.
        - Se você já tiver um arquivo de esquema (possivelmente um que você criou usando Olá [Editor de esquema](#schema-editor)), você pode clicar em **procurar**, navegar tooyour arquivo, clique em **salvar**e, em seguida, clique em **Okey**.
        - Se você quiser toocreate um novo esquema, clique em **Okey**e, em seguida, clique em **Editor de esquema** na janela principal do hello. Continue toohello [Editor de esquema](#schema-editor) informações. Ao criar um novo arquivo de esquema hello, lembre-se toohello back toogo **opções avançadas de** arquivo de esquema janela tooinclude Olá recém-criado.

6. Depois de preencher e fechar Olá **configuração de DSN do Azure Cosmos banco de dados ODBC Driver** janela, Olá novo DSN de usuário é adicionado toohello guia de DSN de usuário.

    ![Novo Azure Cosmos banco de dados ODBC DSN no guia de DSN de usuário Olá](./media/odbc-driver/odbc-driver-user-dsn.png)

## <a id="#collection-mapping"></a>Etapa 3: Criar uma definição de esquema usando o método de mapeamento de coleção hello

Há dois tipos de métodos de amostragem que você pode usar: **mapeamento de coleção** ou **delimitadores de tabela**. Uma sessão de amostragem pode utilizar ambos os métodos de amostragem, mas cada coleta pode usar apenas um método de amostragem específico. Olá estas etapas criam um esquema para dados de saudação em uma ou mais coleções usando o método de mapeamento de coleção hello. Esse método de amostragem recupera dados de saudação na página de saudação de uma estrutura de saudação toodetermine coleta de dados de saudação. Ele transpõe uma tabela tooa coleção saudação do lado do ODBC. Esse método de amostragem é rápida e eficiente quando dados de saudação em uma coleção são homogêneos. Se uma coleção contém heterogêneo tipo de dados, recomendamos que você use Olá [delimitadores da tabela de mapeamento de método](#table-mapping) como ele fornece um método de amostragem mais robusto estruturas de dados de saudação toodetermine na coleção de saudação. 

1. Depois de concluir as etapas 1 a 4 em [banco de dados do banco de dados do Azure Cosmos conectar tooyour](#connect), clique em **Editor de esquema** em Olá **configuração de DSN do Azure Cosmos banco de dados ODBC Driver** janela.

    ![Botão do editor de esquema na janela de configuração DSN do Driver de ODBC de banco de dados do Azure Cosmos Olá](./media/odbc-driver/odbc-driver-schema-editor.png)
2. Em Olá **Editor de esquema** janela, clique em **criar novo**.
    Olá **gerar esquema** janela exibe todas as coleções de saudação em hello Azure Cosmos DB conta. 
3. Selecione um ou mais toosample de coleções e, em seguida, clique em **exemplo**. 
4. Em Olá **modo Design** guia, banco de dados hello, esquema e tabela são representados. No modo de exibição de tabela hello, verificação de saudação exibe conjunto de saudação de propriedades associadas com os nomes de coluna hello (nome de SQL, nome da fonte, etc.).
    Para cada coluna, você pode modificar o nome SQL da coluna de saudação, tipo SQL hello, comprimento SQL (se aplicável), escala (se aplicável), precisão (se aplicável) e permite valor nulo.
    - Você pode definir **Ocultar coluna** muito**true** se você quiser tooexclude que a coluna de resultados da consulta. As colunas marcadas Ocultar coluna = true não são retornados para a seleção e projeção, embora ainda fazem parte do esquema de saudação. Por exemplo, você pode ocultar todas as propriedades de sistema necessárias de banco de dados do Azure Cosmos Olá começando com "_".
    - Olá **id** coluna é Olá único campo que não pode ser oculto como ele é usado como chave primária de saudação no esquema normalizado hello. 
5. Depois de concluir a definição de esquema hello, clique em **arquivo** | **salvar**, navegue esquema de saudação do toohello directory toosave e, em seguida, clique em **salvar**.

    Se no hello futuras você deseja toouse esse esquema com um DSN, Abrir janela de configuração DSN do Driver de ODBC de banco de dados do Azure Cosmos hello (via Olá administrador de fonte de dados ODBC), clique em Opções avançadas e, em seguida, na caixa do arquivo de esquema Olá, navegar toohello salvo o esquema. Salvando uma tooan do arquivo de esquema existente DSN modifica dados de toohello saudação DSN conexão tooscope e estrutura definida pelo esquema.

## <a id="table-mapping"></a>Etapa 4: Criar uma definição de esquema usando os delimitadores de tabela Olá mapeamento de método

Há dois tipos de métodos de amostragem que você pode usar: **mapeamento de coleção** ou **delimitadores de tabela**. Uma sessão de amostragem pode utilizar ambos os métodos de amostragem, mas cada coleta pode usar apenas um método de amostragem específico. 

Olá etapas a seguir criam um esquema para dados de saudação em uma ou mais coleções usando Olá **delimitadores de tabela** método de mapeamento. É recomendável que você use esse método de amostragem quando suas coleções contiverem tipos heterogêneos de dados. Você pode usar essa saudação de tooscope método tooa conjunto de atributos e seus valores correspondentes de amostragem. Por exemplo, se um documento contém uma propriedade "Type", você pode definir o escopo toohello valores amostragem Olá desta propriedade. resultado final Olá amostragem Olá seria um conjunto de tabelas para cada um dos valores de saudação para o tipo especificado. Por exemplo, Type = Carro gerará uma tabela Carro, enquanto Type = Avião gerará uma tabela Avião.

1. Depois de concluir as etapas 1 a 4 em [banco de dados do banco de dados do Azure Cosmos conectar tooyour](#connect), clique em **Editor de esquema** na janela de configuração DSN do Driver de ODBC de banco de dados do Azure Cosmos hello.
2. Em Olá **Editor de esquema** janela, clique em **criar novo**.
    Olá **gerar esquema** janela exibe todas as coleções de saudação em hello Azure Cosmos DB conta. 
3. Selecione uma coleção em Olá **exibição exemplo** guia Olá **definição de mapeamento** coluna na coleção hello, clique em **editar**. Em seguida, em Olá **definição de mapeamento** janela, selecione **delimitadores de tabela** método. Em seguida, Olá a seguir:

    a. Em Olá **atributos** caixa, digite o nome de saudação de uma propriedade de delimitador. Esta é uma propriedade do documento que você deseja que a amostragem de Olá tooscope, por exemplo, cidade e pressione enter. 

    b. Se você quiser apenas valores de toocertain tooscope Olá amostragem para atributo Olá inseridos, selecione atributo Olá na caixa de seleção hello e insira um valor em Olá **valor** caixa, por exemplo, Seattle e pressione enter. Você pode continuar tooadd vários valores para atributos. Apenas certifique-se de que Olá correto de atributo é selecionado quando você estiver digitando valores.

    Por exemplo, se você incluir um **atributos** valor de cidade e você deseja toolimit tooonly sua tabela incluir linhas com um valor de cidade de Nova York e Dubai, você digitaria cidade na caixa de atributos hello e Nova York e Dubai, Olá  **Valores** caixa.
4. Clique em **OK**. 
5. Depois de concluir as definições de mapeamento Olá para coleções de saudação desejado toosample em Olá **Editor de esquema** janela, clique em **exemplo**.
     Para cada coluna, você pode modificar o nome SQL da coluna de saudação, tipo SQL hello, comprimento SQL (se aplicável), escala (se aplicável), precisão (se aplicável) e permite valor nulo.
    - Você pode definir **Ocultar coluna** muito**true** se você quiser tooexclude que a coluna de resultados da consulta. As colunas marcadas Ocultar coluna = true não são retornados para a seleção e projeção, embora ainda fazem parte do esquema de saudação. Por exemplo, você pode ocultar todas as propriedades de sistema necessário do banco de dados do Azure Cosmos Olá começando com "_".
    - Olá **id** coluna é Olá único campo que não pode ser oculto como ele é usado como chave primária de saudação no esquema normalizado hello. 
6. Depois de concluir a definição de esquema hello, clique em **arquivo** | **salvar**, navegue esquema de saudação do toohello directory toosave e, em seguida, clique em **salvar**.
7. Em Olá **configuração de DSN do Azure Cosmos banco de dados ODBC Driver** janela, clique em * * Avançado Opções * *. Em seguida, no hello **arquivo de esquema** caixa, navegue toohello salvada arquivo de esquema e clique em **Okey**. Clique em **Okey** novamente toosave Olá DSN. Esse esquema de saudação salva criado toohello DSN. 

## <a name="optional-creating-views"></a>(Opcional) Criando exibições
Você pode definir e criar modos de exibição como parte do processo de amostragem de saudação. Essas exibições são tooSQL equivalente. Elas são somente leitura e são seleções de saudação do escopo e projeções de hello que Azure Cosmos banco de dados SQL definido. 

toocreate uma exibição para seus dados, no hello **Editor de esquema** janela no hello **definições de exibição** coluna, clique em **adicionar** na linha de saudação do hello coleção toosample. Em seguida, em Olá **definições de exibição** janela, Olá a seguir:
1. Clique em **novo**, insira um nome para exibição hello, por exemplo, EmployeesfromSeattleView e, em seguida, clique em **Okey**.
2. Em Olá **Editar exibição** janela, insira uma consulta de banco de dados do Azure Cosmos. Ela deve ser uma consulta SQL do Azure Cosmos DB, por exemplo, `SELECT c.City, c.EmployeeName, c.Level, c.Age, c.Gender, c.Manager FROM c WHERE c.City = “Seattle”`. Depois, clique em **OK**.

Você pode criar quantas exibições desejar. Feito definindo Olá exibições, você pode, em seguida, dados de exemplo hello. 

## <a name="step-5-view-your-data-in-bi-tools-such-as-power-bi-desktop"></a>Etapa 5: Exibir os dados em ferramentas de BI como Power BI Desktop

Você pode usar o novo tooconnect DSN DocumentADB com qualquer ferramenta compatível com ODBC - esta etapa simplesmente mostra como tooconnect tooPower BI Desktop e criar uma visualização do Power BI.

1. Abra o Power BI Desktop.
2. Clique em **Obter Dados**.
3. Em Olá **obter dados** janela, clique em **outros** | **ODBC** | **conectar**.
4. Em Olá **do ODBC** janela, nome de fonte de dados selecione Olá você criou e, em seguida, clique em **Okey**. Você pode deixar Olá **opções avançadas de** entradas em branco.
5. Em Olá **acessar uma fonte de dados usando um driver ODBC** janela, selecione **padrão ou personalizada** e, em seguida, clique em **conectar**. Não é necessário Olá tooinclude **propriedades de cadeia de caracteres de conexão de credencial**.
6. Em Olá **navegador** no painel esquerdo do hello, expanda o banco de dados hello, Olá esquema e tabela hello, em seguida, selecione. Painel de resultados de saudação inclui dados de saudação usando esquema Olá que você criou.
7. dados de Olá toovisualize no Power BI desktop, marque a caixa Olá na frente do nome da tabela hello e, em seguida, clique em **carga**.
8. No Power BI Desktop, na saudação à extrema esquerda, selecione o guia de dados de saudação ![Guia Dados no Power BI Desktop](./media/odbc-driver/odbc-driver-data-tab.png) tooconfirm os dados foram importados.
9. Agora você pode criar elementos visuais usando o Power BI clicando na guia relatório de saudação ![guia relatório no Power BI Desktop](./media/odbc-driver/odbc-driver-report-tab.png), clicando em **novo Visual**e, em seguida, personalizar seu bloco. Para obter mais informações sobre como criar visualizações no Power BI Desktop, consulte [Tipos de visualização no Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-visualization-types-for-reports-and-q-and-a/).

## <a name="troubleshooting"></a>Solucionar problemas

Se você receber Olá erro a seguir, certifique-se de saudação **Host** e **chave de acesso** valores que você copiou Olá portal do Azure em [etapa 2](#connect) estão corretas e tente novamente. Use Olá cópia botões toohello direito da saudação **Host** e **chave de acesso** valores hello livre de erro de valores de saudação à toocopy portal do Azure.

    [HY000]: [Microsoft][Azure Cosmos DB] (401) HTTP 401 Authentication Error: {"code":"Unauthorized","message":"hello input authorization token can't serve hello request. Please check that hello expected payload is built as per hello protocol, and check hello key being used. Server used hello following payload toosign: 'get\ndbs\n\nfri, 20 jan 2017 03:43:55 gmt\n\n'\r\nActivityId: 9acb3c0d-cb31-4b78-ac0a-413c8d33e373"}`

## <a name="next-steps"></a>Próximas etapas

toolearn mais sobre Azure Cosmos DB, consulte [o que é o banco de dados do Azure Cosmos?](introduction.md).
