---
title: aaaGeneric SQL Connector | Microsoft Docs
description: "Este artigo descreve como conector do SQL genérico da Microsoft tooconfigure."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: fd8ccef3-6605-47ba-9219-e0c74ffc0ec9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2eab8f0894e83ab4738b9f2deb05b03cdc9a9d43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="generic-sql-connector-technical-reference"></a>Referência técnica do conector SQL genérico
Este artigo descreve Olá conector do SQL genérico. artigo Olá aplica toohello produtos a seguir:

* Microsoft Identity Manager 2016 (MIM2016)
* Forefront Identity Manager 2010 R2 (FIM2010R2)
  * É necessário usar o hotfix 4.1.3671.0 ou posterior [KB3092178](https://support.microsoft.com/kb/3092178).

Para MIM2016 e FIM2010R2, Olá Connector está disponível como um download do hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=717495).

toosee esse conector em ação, consulte Olá [conector do SQL genérico passo a passo](active-directory-aadconnectsync-connector-genericsql-step-by-step.md) artigo.

## <a name="overview-of-hello-generic-sql-connector"></a>Visão geral da saudação conector do SQL genérico
Olá genérico SQL Connector permite que você toointegrate serviço de sincronização de saudação com um sistema de banco de dados que oferece conectividade ODBC.  

De uma perspectiva de alto nível, Olá recursos a seguir é suportado pela versão atual de saudação do conector hello:

| Recurso | Suporte |
| --- | --- |
| Fonte de dados conectada |Olá conector é compatível com todos os drivers ODBC de 64 bits. Ela foi testada com a seguinte hello: <li>Microsoft SQL Server & SQL Azure</li><li>IBM DB2 10.x</li><li>IBM DB2 9.x</li><li>Oracle 10 & 11g</li><li>MySQL 5.x</li> |
| Cenários |<li>Gerenciamento de ciclo de vida do objeto</li><li>Gerenciamento de senha</li> |
| Operações |<li>Importação completa e importação delta, exportação</li><li>Para exportar: Adicionar, Excluir, Atualizar e Substituir</li><li>Definir senha, alterar senha</li> |
| Esquema |<li>Detecção dinâmica de objetos e atributos</li> |

### <a name="prerequisites"></a>Pré-requisitos
Antes de usar o conector de saudação, verifique se que você tem o seguinte Olá no servidor de sincronização de saudação:

* Microsoft .NET 4.5.2 Framework ou posterior
* Drivers de cliente ODBC de 64 bits

### <a name="permissions-in-connected-data-source"></a>Permissões na fonte de dados conectada
toocreate ou executar qualquer uma das tarefas de saudação com suporte no conector do SQL genérico, você deve ter:

* db_datareader
* db_datawriter

### <a name="ports-and-protocols"></a>Portas e protocolos
Para portas de saudação necessárias para Olá toowork de driver ODBC, consulte documentação do fornecedor do banco de dados de saudação.

## <a name="create-a-new-connector"></a>Criar um novo conector
tooCreate um conector do SQL genérico, na **serviço de sincronização** selecione **Management Agent** e **criar**. Selecione Olá **SQL genérico (Microsoft)** conector.

![CreateConnector](./media/active-directory-aadconnectsync-connector-genericsql/createconnector.png)

### <a name="connectivity"></a>Conectividade
Olá conector usa um arquivo de DSN ODBC para conectividade. Criar o arquivo usando o DSN Olá **fontes de dados ODBC** encontrado no menu Iniciar, Olá em **ferramentas administrativas**. Na ferramenta administrativa do hello, criar um **DSN de arquivo** para que ele pode ser fornecido toohello conector.

![CreateConnector](./media/active-directory-aadconnectsync-connector-genericsql/connectivity.png)

tela de conectividade Hello é primeiro hello quando você cria um novo conector do SQL genérico. Você precisa primeiro Olá tooprovide informações a seguir:

* Caminho do arquivo DSN
* Autenticação
  * Nome de usuário
  * Senha

banco de dados de saudação deve dar suporte a um dos seguintes métodos de autenticação:

* **Autenticação do Windows**: Olá autenticação de banco de dados usa o usuário de saudação do hello Windows credenciais tooverify. Olá nome de usuário/senha especificado é tooauthenticate usado com o banco de dados de saudação. Essa conta precisa de banco de dados de toohello de permissões.
* **Autenticação do SQL**: Olá autenticação de banco de dados usa Olá nome de usuário/senha definida uma saudação conectividade tela tooconnect toohello banco de dados. Se você armazenar Olá nome de usuário/senha no arquivo DSN hello, credenciais de Olá fornecidas na tela de conectividade hello têm precedência.
* **Autenticação de banco de dados SQL do Azure**: para obter mais informações, consulte [conectar tooSQL banco de dados, usando o Azure Active Directory Authentication](../../sql-database/sql-database-aad-authentication.md).

**DN é âncora**: se você selecionar essa opção, Olá DN também é usado como o atributo de âncora hello. Ele pode ser usado para uma implementação simples, mas também tem Olá limitação a seguir:

* O conector dá suporte a apenas um tipo de objeto. Portanto, qualquer referência só podem fazer referência a atributos Olá mesmo tipo de objeto.

**Tipo de exportação: Substituição de objeto**: durante a exportação, quando apenas alguns atributos foram alterados, todo objeto Olá com todos os atributos é exportado e substitui Olá objeto existente.

### <a name="schema-1-detect-object-types"></a>Esquema 1 (Detectar tipos de objeto)
Nessa página, você vai tooconfigure como Olá conector é contínuo toofind Olá diferentes tipos de objeto no banco de dados de saudação.

Cada tipo de objeto é apresentado como uma partição e configurado ainda mais em **Configurar Partições e Hierarquias**.

![schema1a](./media/active-directory-aadconnectsync-connector-genericsql/schema1a.png)

**Método de detecção do tipo de objeto**: Olá conector dá suporte a esses métodos de detecção do tipo de objeto.

* **O valor fixo**: fornecerá Olá a lista de tipos de objeto com uma lista separada por vírgulas. Por exemplo: `User,Group,Department`.  
  ![schema1b](./media/active-directory-aadconnectsync-connector-genericsql/schema1b.png)
* **Procedimento de tabela/exibição/armazenado**: fornecer nome de saudação do hello tabela/exibição/procedimento armazenado e, em seguida, nome da coluna Olá que fornece a lista de saudação de tipos de objeto. Se você usar um procedimento armazenado, em seguida, também fornecem parâmetros para ele no formato Olá **[nome]: [direção]: [valor]**. Fornece a cada parâmetro em uma linha separada (use Ctrl + Enter tooget uma nova linha).  
  ![schema1c](./media/active-directory-aadconnectsync-connector-genericsql/schema1c.png)
* **Consulta SQL**: essa opção permite que você tooprovide uma consulta SQL que retorna uma única coluna com tipos de objeto, por exemplo `SELECT [Column Name] FROM TABLENAME`. Olá retornado a coluna deve ser do tipo cadeia de caracteres (varchar).

### <a name="schema-2-detect-attribute-types"></a>Esquema 2 (Detectar tipos de atributo)
Nessa página, você vai tooconfigure Olá como nomes de atributos e tipos serão toobe detectado. Opções de configuração de saudação são listadas para cada tipo de objeto detectado na página anterior do hello.

![schema2a](./media/active-directory-aadconnectsync-connector-genericsql/schema2a.png)

**Método de detecção do tipo de atributo**: Olá conector dá suporte a esses métodos de detecção do tipo de atributo com cada tipo de objeto detectado na tela 1 do esquema.

* **Procedimento de tabela/exibição/armazenado**: fornecer nome de saudação do hello tabela/exibição/procedimento armazenado que deve ser nomes de atributo Olá toofind usado. Se você usar um procedimento armazenado, em seguida, também fornecem parâmetros para ele no formato Olá **[nome]: [direção]: [valor]**. Fornece a cada parâmetro em uma linha separada (use Ctrl + Enter tooget uma nova linha). nomes de atributo de saudação toodetect em um atributo com vários valores, forneça uma lista separada por vírgulas de tabelas ou exibições. Não haverá suporte para cenários de valores múltiplos quando a tabela pai e filho tiverem os mesmos nomes de coluna.
* **Consulta SQL**: essa opção permite que você tooprovide uma consulta SQL que retorna uma única coluna com nomes de atributo, por exemplo `SELECT [Column Name] FROM TABLENAME`. Olá retornado a coluna deve ser do tipo cadeia de caracteres (varchar).

### <a name="schema-3-define-anchor-and-dn"></a>Esquema 3 (Definir âncora e DN)
Esta página permite que você tooconfigure a âncora e atributo DN para cada tipo de objeto detectado. Você pode selecionar vários atributos toomake Olá âncora exclusiva.

![schema3a](./media/active-directory-aadconnectsync-connector-genericsql/schema3a.png)

* Atributos de valores múltiplos e boolianos não são listados.
* Mesmo atributo não pode usar para o DN e âncora, a menos que **DN é âncora** selecionada na página de conectividade de saudação.
* Se **DN é âncora** está selecionada na página de conectividade Olá, esta página requer o único atributo Olá DN. Esse atributo será usado também como atributo de âncora hello.

  ![schema3b](./media/active-directory-aadconnectsync-connector-genericsql/schema3b.png)

### <a name="schema-4-define-attribute-type-reference-and-direction"></a>Esquema 4 (Definir tipo de atributo, referência e direção)
Esta página permite que você tooconfigure o tipo de atributo hello, como inteiro, binário ou boolianos e direção para cada atributo. Todos os atributos da página **Esquema 2** estão listados como atributos de valores múltiplos.

![schema4a](./media/active-directory-aadconnectsync-connector-genericsql/schema4a.png)

* **Tipo de dados**: toomap Olá atributo tipo toothose tipos conhecidos pelo mecanismo de sincronização de saudação usados. padrão de saudação é Olá toouse mesmo tipo, conforme detectado no esquema SQL hello, mas DateTime e referência não são facilmente detectáveis. Para aqueles, você precisa toospecify **DateTime** ou **referência**.
* **Direção**: você pode definir Olá atributo direção tooImport, exportar ou ImportExport. ImportExport é o padrão.

![schema4b](./media/active-directory-aadconnectsync-connector-genericsql/schema4b.png)

Observações:

* Se um tipo de atributo não é detectável pelo Olá conector, ele usa o tipo de dados de cadeia de caracteres de saudação.
* **Tabelas aninhadas** podem ser consideradas tabelas de banco de dados de uma coluna. Oracle armazena linhas de saudação de uma tabela aninhada em nenhuma ordem específica. No entanto, ao recuperar a tabela aninhada Olá em uma variável de PL/SQL, linhas de saudação recebem subscritos consecutivos, começando em 1. Que retorna linhas de tooindividual de acesso de matriz.
* **VARRYS** não há suporte para o conector de saudação.

### <a name="schema-5-define-partition-for-reference-attributes"></a>Esquema 5 (Definir partição para atributos de referência)
Nesta página você configura todos os atributos de referência a cuja partição (tipo de objeto) um atributo está se referindo.

![schema5](./media/active-directory-aadconnectsync-connector-genericsql/schema5.png)

Se você usar **DN é âncora**, você deve usar Olá mesmo tipo de objeto Olá um você está referenciando de. Não é possível referenciar outro tipo de objeto.

>[!NOTE]
Iniciando atualização de março de 2017 Olá agora é uma opção para "*" quando essa opção for escolhida, em seguida, todos os tipos de membro possíveis serão importados.

![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/any-option.png)

>[!IMPORTANT]
 A partir de maio de 2017 hello "*" também conhecido como **qualquer opção** foi alterado toosupport importar e exportar o fluxo. Se você quiser que esta opção toouse sua tabela/exibição múltiplos devem ter um atributo que contém o tipo de objeto hello.

![](./media/active-directory-aadconnectsync-connector-genericsql/any-02.png)

 </br> Se "*" é selecionado e o nome de saudação da coluna de saudação com tipo de objeto Olá também deve ser especificado.</br> ![](./media/active-directory-aadconnectsync-connector-genericsql/any-03.png)

Após a importação, você verá algo semelhante imagem toohello abaixo:

  ![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/after-import.png)



### <a name="global-parameters"></a>Parâmetros Globais
página de parâmetros globais Hello é usado tooconfigure importação de Delta, o formato de data/hora e o método de senha.

![globalparameters1](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters1.png)



Olá conector do SQL genérico dá suporte a saudação métodos a seguir para importação de Delta:

* **Gatilho**: consulte [Gerar exibições de Delta usando gatilhos](https://technet.microsoft.com/library/cc708665.aspx).
* **Marca d'água**: uma abordagem genérica que pode ser usada com qualquer banco de dados. consulta de marca d'água Olá é previamente preenchida com base no fornecedor de banco de dados de saudação. Uma coluna de marca-d'água deve estar presente em cada tabela/exibição usada. Esta coluna deve controlar inserções e atualizações de tabelas de toohello como e seus dependentes (múltiplos ou filho) tabelas. relógios Olá entre o serviço de sincronização e o servidor de banco de dados de saudação devem ser sincronizados. Caso contrário, algumas entradas na importação de delta Olá podem ser omitidas.  
  Limitação:
  * A estratégia de marca-d'água não dá suporte a exclusão de objetos.
* **Instantâneo**(funciona somente com o Microsoft SQL Server) [Gerando exibições de Delta usando instantâneos](https://technet.microsoft.com/library/cc720640.aspx)
* **Acompanhamento de alterações**(funciona somente com o Microsoft SQL Server) [About Acompanhamento de alterações](https://msdn.microsoft.com/library/bb933875.aspx)  
  Limitações:
  * Atributo DN & de âncora devem ser parte da chave primária para o objeto selecionado do hello na tabela de saudação.
  * Consulta SQL não tem suporte durante importação e exportação com acompanhamento de alterações.

**Parâmetros adicionais**: especificar Olá fuso horário do banco de dados do servidor que indica onde o servidor de banco de dados está localizado. Esse valor é usado toosupport Olá vários formatos de data e hora de atributos.

Olá conector sempre armazena a data e a data e hora no formato UTC. toocorrectly de toobe capaz de converter vezes e date de hello, Olá fuso horário do servidor de banco de dados de saudação e formato Olá usado deve ser especificado. formato de saudação deve ser expressos em formato .net.

Durante a exportação, todos os atributos de tempo de data devem ser fornecido toohello conector no formato de hora UTC.

![globalparameters2](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters2.png)

**Configuração de senha**: conector Olá fornece recursos de sincronização de senha e dá suporte a definir e alterar a senha.

Olá conector fornece dois métodos de sincronização de senha toosupport:

* **Procedimento armazenado**: esse método requer dois procedimentos armazenados toosupport conjunto e alterar a senha. Digite todos os parâmetros para adicionar e alterar a operação de saudação de senha em **definir senha SP** e **alterar senha SP** parâmetros respectivamente como por exemplo abaixo.
  ![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters3.png)
* **Extensão de senha**: esse método requer a DLL de extensão de senha (necessário tooprovide Olá nome da DLL de extensão que está implementando Olá [IMAExtensible2Password](https://msdn.microsoft.com/library/microsoft.metadirectoryservices.imaextensible2password.aspx) interface). Assembly de extensão de senha deve ser colocado na pasta de extensão para que o conector de saudação pode carregar Olá DLL em tempo de execução.
  ![globalparameters4](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters4.png)

Você também tem tooenable Olá gerenciamento de senha em Olá **extensão configurar** página.
![globalparameters5](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters5.png)

### <a name="configure-partitions-and-hierarchies"></a>Configurar partições e hierarquias
Na página partições e hierarquias hello, selecione todos os tipos de objeto. Cada tipo de objeto está em sua própria partição.

![partitions1](./media/active-directory-aadconnectsync-connector-genericsql/partitions1.png)

Você também pode substituir valores hello definidos no hello **conectividade** ou **parâmetros globais** página.

![partitions2](./media/active-directory-aadconnectsync-connector-genericsql/partitions2.png)

### <a name="configure-anchors"></a>Configurar Âncoras
Esta página é somente leitura como âncora de saudação já foi definida. Olá atributo de âncora selecionado é sempre anexado com tooensure de tipo de objeto Olá ele permanece exclusivo em todos os tipos de objeto.

![âncoras](./media/active-directory-aadconnectsync-connector-genericsql/anchors.png)

## <a name="configure-run-step-parameter"></a>Configurar parâmetros da etapa de execução
Essas etapas são configuradas no hello perfis de execução em Olá conector. Essas configurações Olá real trabalho de importação e exportação de dados.

### <a name="full-and-delta-import"></a>Importação completa e Delta
O conector SQL genérico oferece suporte a importação completa e Delta usando estes métodos genérico:

* Tabela
* Visualizar
* Procedimento armazenado
* Consulta SQL

![runstep1](./media/active-directory-aadconnectsync-connector-genericsql/runstep1.png)

**Tabela/Exibição**  
atributos de múltiplos tooimport para um objeto, você tem nome de tabela/exibição separada por vírgulas de saudação tooprovide **exibições da tabela nome com valores múltiplos** e condições de junção do respectivos em Olá **dacondiçãodejunção**com a tabela pai de saudação.

Exemplo: Que você deseja que o objeto de funcionário Olá tooimport e todos os seus atributos com valores múltiplos. Há duas tabelas chamadas Funcionário (tabela principal) e Departamento (valores múltiplos).
Olá a seguir:

* Digite **Funcionário** em **Tabela/Exibição/SP**.
* Digite Departamento em **Nome da tabela/exibições de valores múltiplos**.
* Tipo de condição de junção Olá entre funcionários e departamento no **condição de junção**, por exemplo `Employee.DEPTID=Department.DepartmentID`.
  ![runstep2](./media/active-directory-aadconnectsync-connector-genericsql/runstep2.png)

**Procedimentos armazenados**  
![runstep3](./media/active-directory-aadconnectsync-connector-genericsql/runstep3.png)

* Se você tiver muitos dados, é recomendável paginação tooimplement com os procedimentos armazenados.
* Para a paginação de toosupport de procedimento armazenado, você precisa tooprovide índice do começo e o índice do fim. Consulte: [Paginação eficiente em grandes quantidades de dados](https://msdn.microsoft.com/library/bb445504.aspx).
* @StartIndex e @EndIndex são substituídos em tempo de execução pelo respectivo valor do tamanho de página configurado na página **Configurar Etapa**. Por exemplo, quando conector Olá recupera a primeira página e tamanho de página de saudação é definido 500, tal situação @StartIndex seria 1 e @EndIndex 500. Esses valores aumentar ao conector recupera as páginas subsequentes e alterar Olá @StartIndex & @EndIndex valor.
* tooexecute de procedimento armazenado com parâmetros, forneça parâmetros Olá `[Name]:[Direction]:[Value]` formato. Insira cada parâmetro em uma linha separada (Use Ctrl + Enter tooget uma nova linha).
* O conector do SQL genérico também dá suporte à operação de importação de Servidores Vinculados no Microsoft SQL Server. Se as informações devem ser recuperadas de uma tabela no servidor vinculado, tabela deve ser fornecida no formato de saudação:`[ServerName].[Database].[Schema].[TableName]`
* O conector SQL genérico só dá suporte a objetos com estrutura semelhante (nome de alias e tipo de dados) entre informações de etapas de execução e detecção de esquema. Se tiver selecionado Olá objeto de esquema e as informações fornecidas na etapa de execução é diferente e o conector do SQL é toosupport não é possível esse tipo de cenários.

**Consulta SQL**  
![runstep4](./media/active-directory-aadconnectsync-connector-genericsql/runstep4.png)

![runstep5](./media/active-directory-aadconnectsync-connector-genericsql/runstep5.png)

* Consultas com vários conjuntos de resultados não têm suporte.
* Consulta SQL dá suporte a Olá paginação e fornece o início e término índice como uma variável toosupport a paginação.

### <a name="delta-import"></a>Importação de delta
![runstep6](./media/active-directory-aadconnectsync-connector-genericsql/runstep6.png)

A configuração de Importação de Delta exige alguma configuração adicional, em comparação com a Importação Completa.

* Se você escolher a abordagem de gatilho ou instantâneo Olá as alterações delta na tootrack, em seguida, fornecer banco de dados de uma tabela de histórico ou instantâneo em **nome de banco de dados de tabela de histórico ou instantâneo** caixa.
* Você também precisa tooprovide condição de junção entre a tabela de histórico e a tabela pai, por exemplo`Employee.ID=History.EmployeeID`
* transação de saudação tootrack na tabela de pai Olá Olá da tabela de histórico, você deve fornecer o nome de coluna de saudação que contém informações de operação da saudação (Adicionar/atualizar/excluir).
* Se você escolher a marca d'água tootrack as alterações delta, em seguida, forneça o nome de coluna de saudação que contém informações de operação de saudação em **nome de coluna de marca d'água**.
* Olá **alterar o atributo de tipo** coluna é necessária para o tipo de alteração de saudação. Esta coluna é uma alteração que ocorre na tabela primária Olá mapeada ou tooa da tabela de valores múltiplos alterar tipo na exibição de delta hello. Esta coluna pode conter o tipo de alteração de Modify_Attribute Olá para alteração do nível de atributo ou adicionar, modificar ou excluir alterar para um tipo de alteração do nível de objeto. Se for diferente do valor de padrão de saudação adicionar, modificar ou excluir, em seguida, você pode definir esses valores usando essa opção.

### <a name="export"></a>Exportação
![runstep7](./media/active-directory-aadconnectsync-connector-genericsql/runstep7.png)

O conector SQL genérico oferece suporte à exportação usando quatro métodos:

* Tabela
* Visualizar
* Procedimento armazenado
* Consulta SQL

**Tabela/Exibição**  
Se você escolher Olá opção de tabela/exibição, conector hello gera Olá respectivas consultas toodo Olá exportação.

**Procedimentos armazenados**  
![runstep8](./media/active-directory-aadconnectsync-connector-genericsql/runstep8.png)

Se você escolher a opção de procedimento armazenado hello, exportação requer três diferentes armazenado procedimentos tooperform inserir/atualizar/excluir operações.

* **Adicionar nome de SP**: This SP será executada se qualquer objeto vem tooconnector para inserção na tabela respectivos hello.
* **Atualizar nome SP**: This SP será executada se qualquer objeto vem tooconnector para atualização na tabela respectivos hello.
* **Excluir o nome de SP**: This SP será executada se qualquer objeto vem tooconnector para exclusão na tabela respectivos hello.
* Atributo selecionado do esquema de saudação usado como um procedimento de toohello armazenado do valor de parâmetro. Por exemplo, `EmployeeName: INPUT: @EmployeeName` (EmployeeName está selecionado no esquema de conector hello e conector Olá substitui o respectivo valor de saudação durante o processo de exportação)
* toorun de procedimento armazenado com parâmetros, forneça parâmetros em `[Name]:[Direction]:[Value]` formato. Insira cada parâmetro em uma linha separada (Use Ctrl + Enter tooget uma nova linha).

**SQL query**  
![runstep9](./media/active-directory-aadconnectsync-connector-genericsql/runstep9.png)

Se você escolher a opção de consulta SQL hello, exportação requer que três diferentes consultas tooperform inserir/atualizar/excluir operações.

* **Consulta INSERT**: esta consulta é executada se qualquer objeto vem tooconnector para inserção na tabela respectivos hello.
* **Consulta atualização**: esta consulta é executada se qualquer objeto vem tooconnector para atualização na tabela respectivos hello.
* **Consulta exclusão**: esta consulta é executada se qualquer objeto vem tooconnector para exclusão na tabela respectivos hello.
* Atributo selecionado do esquema Olá usada como uma consulta de toohello de valor de parâmetro, por exemplo`Insert into Employee (ID, Name) Values (@ID, @EmployeeName)`

## <a name="troubleshooting"></a>Solucionar problemas
* Para obter informações sobre como o log tooenable tootroubleshoot Olá conector, consulte Olá [como tooEnable o rastreamento ETW para conectores](http://go.microsoft.com/fwlink/?LinkId=335731).
