---
title: toouse aaaHow envio em lote tooimprove desempenho de aplicativos de banco de dados SQL
description: "tópico Hello fornece evidência que envio em lote do banco de dados operações muito imroves Olá velocidade e a escalabilidade de seus aplicativos de banco de dados SQL. Embora essas técnicas de envio em lote funcionam para qualquer banco de dados do SQL Server, o foco Olá artigo Olá é no Azure."
services: sql-database
documentationcenter: na
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 563862ca-c65a-46f6-975d-10df7ff6aa9c
ms.service: sql-database
ms.custom: develop apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/12/2016
ms.author: sstein
ms.openlocfilehash: 124b203ee69c595f0813852ff09ef9ec6841233a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-batching-tooimprove-sql-database-application-performance"></a>Como toouse envio em lote tooimprove desempenho de aplicativos de banco de dados SQL
Processamento em lotes de operações tooAzure banco de dados SQL significativamente melhora o desempenho de saudação e escalabilidade de seus aplicativos. Benefícios de saudação do toounderstand de ordem, a primeira parte Olá deste artigo abrange alguns resultados do teste de exemplo que comparam solicitações em lote e não sequenciais tooa banco de dados SQL. Olá restante do artigo Olá mostra técnicas hello, cenários e considerações toohelp toouse envio em lote com êxito em seus aplicativos do Azure.

## <a name="why-is-batching-important-for-sql-database"></a>Por que o envio em lote é importante para o Banco de Dados SQL?
O serviço remoto tooa chamadas de envio em lote é uma estratégia conhecida para aumentar o desempenho e escalabilidade. Há corrigidos processar custos tooany interações com um serviço remoto, como a transferência de rede, serialização e desserialização. O empacotamento de muitas transações separadas em um único lote minimiza esses custos.

Neste documento, queremos tooexamine vários cenários e estratégias de envio em lote do banco de dados SQL. Embora essas estratégias também são importantes para aplicativos locais que usam o SQL Server, há vários motivos para realçar o uso de saudação do envio em lote para o banco de dados SQL:

* Há potencialmente maior latência de rede ao acessar o banco de dados SQL, especialmente se você estiver acessando o banco de dados SQL de saudação externa mesmo datacenter do Microsoft Azure.
* características de multilocatário Olá significa de banco de dados SQL que Olá eficiência dos dados Olá acessar camada correlaciona toohello escalabilidade total do banco de dados de saudação. Banco de dados SQL deve impedir que qualquer locatário/usuário monopolize detrimento de toohello de recursos de banco de dados de outros locatários. Na resposta toousage além das cotas predefinidas, o banco de dados SQL pode reduzir a taxa de transferência ou responder com exceções de limitação. As eficiências, como envio em lote, permitem que você toodo mais trabalho no banco de dados SQL antes de alcançar esses limites. 
* O envio em lote também é eficaz para arquiteturas que usam vários bancos de dados (fragmentação). eficiência de saudação de sua interação com cada unidade de banco de dados ainda é um fator essencial em sua escalabilidade total. 

Um dos benefícios de saudação do uso de banco de dados SQL é que você não tem servidores de saudação toomanage esse banco de dados de saudação do host. No entanto, essa infraestrutura gerenciada também significa que você tenha toothink diferente sobre otimizações de banco de dados. Não é possível examinar infraestrutura de hardware ou de rede de banco de dados de saudação do tooimprove. O Microsoft Azure controla esses ambientes. Olá principal área que você pode controlar é como seu aplicativo interage com o banco de dados SQL. O envio em lote é uma dessas otimizações. 

a primeira parte saudação do papel Olá examina várias técnicas de envio em lote para aplicativos .NET que usam o banco de dados SQL. Olá duas últimas seções abordam diretrizes e cenários de envio em lote.

## <a name="batching-strategies"></a>Estratégias de envio em lote
### <a name="note-about-timing-results-in-this-topic"></a>Observação sobre os resultados de tempo neste tópico
> [!NOTE]
> Resultados não são parâmetros de comparação, mas devem tooshow **desempenho relativo**. Os intervalos se baseiam em uma média de pelo menos 10 execuções de teste. As operações são inserções em uma tabela vazia. Esses testes foram medidos pre-V12 e não necessariamente correspondem toothroughput que podem ocorrer no banco de dados V12 usando Olá novo [camadas de serviço](sql-database-service-tiers.md). benefício relativo Olá Olá técnica de envio em lote deve ser semelhante.
> 
> 

### <a name="transactions"></a>Transações
Parece estranho toobegin uma revisão do envio em lote discutindo transações. Mas o uso de saudação de transações do lado do cliente tem um efeito sutil envio em lote do lado do servidor que melhora o desempenho. E transações podem ser adicionadas com apenas algumas linhas de código, para que eles fornecem um desempenho de tooimprove de maneira rápida de operações sequenciais.

Considere Olá código em c# que contém uma sequência de inserção a seguir e operações de atualização em uma tabela simples.

    List<string> dbOperations = new List<string>();
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 1");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 2");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 3");
    dbOperations.Add("insert MyTable values ('new value',1)");
    dbOperations.Add("insert MyTable values ('new value',2)");
    dbOperations.Add("insert MyTable values ('new value',3)");

Olá código ADO.NET a seguir sequencialmente executa essas operações.

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();

        foreach(string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn);
            cmd.ExecuteNonQuery();                   
        }
    }

Olá toooptimize de maneira melhor esse código é tooimplement alguma forma de envio em lote do lado do cliente dessas chamadas. Mas há um modo simples tooincrease Olá de desempenho do código simplesmente encapsulando sequência Olá de chamadas em uma transação. Eis Olá mesmo código que usa uma transação.

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();
        SqlTransaction transaction = conn.BeginTransaction();

        foreach (string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn, transaction);
            cmd.ExecuteNonQuery();
        }

        transaction.Commit();
    }

Na verdade, as transações estão sendo usadas nos dois exemplos. No primeiro exemplo de hello, cada chamada individual é uma transação implícita. No segundo exemplo de hello, uma transação explícita encapsula todas as chamadas de saudação. Por documentação Olá Olá [log de transações write-ahead](https://msdn.microsoft.com/library/ms186259.aspx), registros de log são liberados toohello disco quando Olá transação confirmada. Portanto, incluindo mais chamadas em uma transação, hello grava toohello o log de transações pode atrasar até que Olá a transação é confirmada. Na verdade, você habilitará o envio em lote para o log de transações do servidor do toohello Olá gravações.

Olá, a tabela a seguir mostra alguns resultados de teste ad-hoc. testes de saudação executada Olá que mesmo sequencial insere com e sem transações. Para obter mais perspectiva, primeiro o conjunto de testes Olá foi executado remotamente de um banco de dados de toohello laptop no Microsoft Azure. Hello segundo conjunto de testes foi executado de um serviço de nuvem e o banco de dados que residiam no hello mesmo datacenter do Microsoft Azure (Oeste dos Estados Unidos). Olá tabela a seguir mostra Olá duração em milissegundos de inserções sequenciais com e sem transações.

**TooAzure local**:

| Operações | Sem transação (ms) | Com transação (ms) |
| --- | --- | --- |
| 1 |130 |402 |
| 10 |1208 |1226 |
| 100 |12662 |10395 |
| 1000 |128852 |102917 |

**TooAzure do Azure (mesmo datacenter)**:

| Operações | Sem transação (ms) | Com transação (ms) |
| --- | --- | --- |
| 1 |21 |26 |
| 10 |220 |56 |
| 100 |2145 |341 |
| 1000 |21479 |2756 |

> [!NOTE]
> Os resultados não são parâmetros de comparação. Consulte Olá [Observação sobre resultados neste tópico](#note-about-timing-results-in-this-topic).
> 
> 

Com base nos resultados de teste anteriores hello, quebra automática de uma única operação em uma transação, na verdade, reduz o desempenho. Mas, conforme você aumenta o número de saudação de operações em uma única transação, a melhoria de desempenho Olá fica mais evidente. diferença de desempenho Olá também é mais perceptível quando todas as operações ocorrem no datacenter do Microsoft Azure hello. Olá, latência aumentada do uso do banco de dados SQL do data center do Microsoft Azure Olá fora ofusca ganho de desempenho de saudação do uso de transações.

Embora o uso de saudação de transações pode aumentar o desempenho, continuar muito[seguindo as práticas recomendadas para transações e conexões](https://msdn.microsoft.com/library/ms187484.aspx). Mantenha a transação de saudação tão curta quanto a conexão de banco de dados de saudação possíveis e de fechamento após a conclusão do trabalho de saudação. Olá usando a instrução no exemplo anterior Olá garante que conexão Olá é fechada quando o bloco de código subsequente Olá for concluída.

Olá anterior demonstra que você pode adicionar um código do ADO.NET do tooany de transação local com duas linhas. As transações oferecem uma maneira rápida tooimprove desempenho de saudação do código que faz sequencial inserir, atualizar e excluir operações. No entanto, para um desempenho mais rápido hello, considere alterar Olá código adicional tootake vantagem de lote no lado do cliente, como parâmetros com valor de tabela.

Para saber mais sobre transações no ADO.NET, consulte [Transações locais no ADO.NET](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions).

### <a name="table-valued-parameters"></a>Parâmetros com valor de tabela
Os parâmetros com valor de tabela oferecem suporte a tipos de tabela definidos pelo usuário como parâmetros em instruções Transact-SQL, procedimentos armazenados e funções. Essa técnica de envio em lote do lado do cliente permite que você toosend várias linhas de dados no parâmetro com valor de tabela do hello. parâmetros com valor de tabela toouse, primeiro defina um tipo de tabela. Olá instrução Transact-SQL a seguir cria um tipo de tabela denominada **MyTableType**.

    CREATE TYPE MyTableType AS TABLE 
    ( mytext TEXT,
      num INT );


No código, você cria um **DataTable** com hello exato mesmos nomes e tipos de saudação do tipo de tabela. Passe essa **DataTable** em um parâmetro em uma consulta de texto ou em uma chamada de procedimento armazenado. Olá, exemplo a seguir mostra essa técnica:

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        DataTable table = new DataTable();
        // Add columns and rows. hello following is a simple example.
        table.Columns.Add("mytext", typeof(string));
        table.Columns.Add("num", typeof(int));    
        for (var i = 0; i < 10; i++)
        {
            table.Rows.Add(DateTime.Now.ToString(), DateTime.Now.Millisecond);
        }

        SqlCommand cmd = new SqlCommand(
            "INSERT INTO MyTable(mytext, num) SELECT mytext, num FROM @TestTvp",
            connection);

        cmd.Parameters.Add(
            new SqlParameter()
            {
                ParameterName = "@TestTvp",
                SqlDbType = SqlDbType.Structured,
                TypeName = "MyTableType",
                Value = table,
            });

        cmd.ExecuteNonQuery();
    }

No exemplo anterior de saudação, Olá **SqlCommand** objeto insere linhas de um parâmetro com valor de tabela,  **@TestTvp** . Olá criado anteriormente **DataTable** objeto será atribuído o parâmetro hello toothis **SqlCommand.Parameters.Add** método. Inserções de saudação envio em lote em uma chamada significativamente aumenta desempenho Olá sobre inserções sequenciais.

tooimprove anterior exemplo hello Além disso, use um procedimento armazenado, em vez de um comando baseado em texto. Olá comando Transact-SQL a seguir cria um procedimento armazenado que entra Olá **SimpleTestTableType** parâmetro com valor de tabela.

    CREATE PROCEDURE [dbo].[sp_InsertRows] 
    @TestTvp as MyTableType READONLY
    AS
    BEGIN
    INSERT INTO MyTable(mytext, num) 
    SELECT mytext, num FROM @TestTvp
    END
    GO

Em seguida, altere Olá **SqlCommand** declaração a seguir do hello anterior código exemplo toohello do objeto.

    SqlCommand cmd = new SqlCommand("sp_InsertRows", connection);
    cmd.CommandType = CommandType.StoredProcedure;

Na maioria dos casos, os parâmetros com valor de tabela têm um desempenho equivalente ou superior às outras técnicas de envio em lote. Normalmente, a preferência fica com os parâmetros com valor de tabela, pois são mais flexíveis do que as outras opções. Por exemplo, outras técnicas, como cópia em massa SQL, só permitem a inserção de saudação de novas linhas. Mas com parâmetros com valor de tabela, você pode usar lógica toodetermine de procedimento armazenada de saudação quais linhas são atualizações e quais são inserções. tipo de tabela Olá também pode ser modificado toocontain uma coluna "Operação" que indica se Olá especificada linha deve ser inserida, atualizada ou excluída.

Olá, a tabela a seguir mostra os resultados do teste ad-hoc para uso de saudação de parâmetros com valor de tabela em milissegundos.

| Operações | Local tooAzure (ms) | Mesmo datacenter do Azure (ms) |
| --- | --- | --- |
| 1 |124 |32 |
| 10 |131 |25 |
| 100 |338 |51 |
| 1000 |2615 |382 |
| 10000 |23830 |3586 |

> [!NOTE]
> Os resultados não são parâmetros de comparação. Consulte Olá [Observação sobre resultados neste tópico](#note-about-timing-results-in-this-topic).
> 
> 

ganho de desempenho de saudação do envio em lote é imediatamente evidente. No teste sequencial anterior de saudação, 1000 operações levaram 129 segundos fora Olá datacenter e 21 segundos dentro do datacenter hello. Mas, com parâmetros com valor de tabela, 1000 operações levam somente 2,6 segundos fora Olá datacenter e 0,4 segundos no datacenter hello.

Para saber mais sobre parâmetros com valor de tabela, consulte [Parâmetros com valor de tabela](https://msdn.microsoft.com/library/bb510489.aspx).

### <a name="sql-bulk-copy"></a>Cópia em massa do SQL
Cópia em massa SQL é outra maneira tooinsert grandes quantidades de dados em um banco de dados de destino. Aplicativos .NET podem usar Olá **SqlBulkCopy** operações de inserção em massa tooperform de classe. **SqlBulkCopy** é semelhante na ferramenta de linha de comando de função toohello, **Bcp.exe**, ou hello instrução Transact-SQL, **BULK INSERT**. Olá exemplo de código a seguir mostra como saudação de cópia toobulk linhas na fonte de saudação **DataTable**, tabela, a tabela de destino toohello no SQL Server, MyTable.

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        using (SqlBulkCopy bulkCopy = new SqlBulkCopy(connection))
        {
            bulkCopy.DestinationTableName = "MyTable";
            bulkCopy.ColumnMappings.Add("mytext", "mytext");
            bulkCopy.ColumnMappings.Add("num", "num");
            bulkCopy.WriteToServer(table);
        }
    }

Há alguns casos nos quais é preferível usar a cópia em massa do que os parâmetros com valor de tabela. Consulte Olá a tabela de comparação de parâmetros com valor de tabela versus operações BULK INSERT no tópico Olá [parâmetros com valor de tabela](https://msdn.microsoft.com/library/bb510489.aspx).

Olá, seguintes resultados do teste ad hoc mostram Olá desempenho do envio em lote com **SqlBulkCopy** em milissegundos.

| Operações | Local tooAzure (ms) | Mesmo datacenter do Azure (ms) |
| --- | --- | --- |
| 1 |433 |57 |
| 10 |441 |32 |
| 100 |636 |53 |
| 1000 |2535 |341 |
| 10000 |21605 |2737 |

> [!NOTE]
> Os resultados não são parâmetros de comparação. Consulte Olá [Observação sobre resultados neste tópico](#note-about-timing-results-in-this-topic).
> 
> 

Em tamanhos de lote menores, os parâmetros com valor de tabela de uso Olá superaram Olá **SqlBulkCopy** classe. No entanto, **SqlBulkCopy** executada 12-31% mais rápido do que parâmetros com valor de tabela para testes de saudação de 1.000 e 10.000 linhas. Como parâmetros com valor de tabela, **SqlBulkCopy** é uma boa opção para inserções em lotes, especialmente quando comparado toohello desempenho de operações não em lotes.

Para saber mais sobre a cópia em massa no ADO.NET, consulte [Operações de cópia em massa no SQL Server](https://msdn.microsoft.com/library/7ek5da1a.aspx).

### <a name="multiple-row-parameterized-insert-statements"></a>Instruções INSERT com parâmetros de várias linhas
Uma alternativa para lotes pequenos é parametrizada de tooconstruct uma grande instrução INSERT que insere várias linhas. saudação de exemplo de código a seguir demonstra essa técnica.

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        string insertCommand = "INSERT INTO [MyTable] ( mytext, num ) " +
            "VALUES (@p1, @p2), (@p3, @p4), (@p5, @p6), (@p7, @p8), (@p9, @p10)";

        SqlCommand cmd = new SqlCommand(insertCommand, connection);

        for (int i = 1; i <= 10; i += 2)
        {
            cmd.Parameters.Add(new SqlParameter("@p" + i.ToString(), "test"));
            cmd.Parameters.Add(new SqlParameter("@p" + (i+1).ToString(), i));
        }

        cmd.ExecuteNonQuery();
    }


Este exemplo visa conceito básico de saudação tooshow. Um cenário mais realista seria loop por meio de cadeia de consulta Olá necessário entidades tooconstruct hello e parâmetros de comando Olá simultaneamente. Você está limitado tooa total de 2100 parâmetros de consulta, e isso limita o número total de saudação de linhas que podem ser processadas dessa maneira.

Olá ad-hoc teste resultados Mostrar Olá desempenho desse tipo de instrução de inserção em milissegundos a seguir.

| Operações | Parâmetros com valor de tabela (ms) | Instrução INSERT única (ms) |
| --- | --- | --- |
| 1 |32 |20 |
| 10 |30 |25 |
| 100 |33 |51 |

> [!NOTE]
> Os resultados não são parâmetros de comparação. Consulte Olá [Observação sobre resultados neste tópico](#note-about-timing-results-in-this-topic).
> 
> 

Essa abordagem pode ser ligeiramente mais rápida para lotes com menos de 100 linhas. Embora Olá melhoria seja pequena, essa técnica é outra opção que pode funcionar bem em seu cenário de aplicativo específico.

### <a name="dataadapter"></a>DataAdapter
Olá **DataAdapter** classe permite que você toomodify uma **DataSet** do objeto e, em seguida, enviar alterações hello como operações INSERT, UPDATE e DELETE. Se você estiver usando Olá **DataAdapter** dessa maneira, é importante toonote que separam as chamadas são feitas para cada operação distinta. tooimprove desempenho, use Olá **UpdateBatchSize** número de toohello de propriedade de operações que deve ser colocado em lote por vez. Para saber mais, consulte [Executando operações em lote usando DataAdapters](https://msdn.microsoft.com/library/aadf8fk2.aspx).

### <a name="entity-framework"></a>Entity Framework
No momento, o Entity Framework não oferece suporte para o envio em lote. Os desenvolvedores diferentes na comunidade de saudação tentaram toodemonstrate alternativas, como substituição Olá **SaveChanges** método. Mas soluções Olá geralmente são complexas e personalizadas toohello aplicativo e o modelo de dados. projeto do codeplex Entity Framework Olá atualmente tem uma página de discussão sobre essa solicitação de recurso. tooview esta discussão, consulte [Design Meeting Notes - 2 de agosto de 2012](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).

### <a name="xml"></a>XML
Para fins de integridade, achamos que é importante tootalk sobre XML como uma estratégia de envio em lote. No entanto, o uso de saudação do XML tem nenhuma vantagem sobre outros métodos e várias desvantagens. abordagem de saudação é parâmetros com valor tootable semelhantes, mas um arquivo XML ou uma cadeia de caracteres é passada procedimento tooa armazenado em vez de uma tabela definida pelo usuário. procedimento armazenado de saudação analisa os comandos de saudação no procedimento armazenado de saudação.

Há várias desvantagens toothis abordagem:

* Trabalhar com XML pode ser complicado e pode apresentar muitos erros.
* Olá análise XML no banco de dados de saudação pode ser com uso intensivo de CPU.
* Na maioria dos casos, esse método é mais lento se comparado ao uso de parâmetros com valor de tabela.

Por esses motivos, o uso de saudação do XML para consultas de lote não é recomendado.

## <a name="batching-considerations"></a>Considerações sobre o envio em lote
Olá seções a seguir fornece mais diretrizes sobre o uso de saudação do envio em lote em aplicativos de banco de dados SQL.

### <a name="tradeoffs"></a>Compensações
Dependendo de sua arquitetura, o envio em lote pode envolver uma compensação entre desempenho e resiliência. Por exemplo, considere o cenário de saudação onde sua função fica ativa inesperadamente. Se você perder uma linha de dados, o impacto de saudação é menor do que o impacto de saudação de perder um lote grande de linhas não enviadas. Há um risco maior ao buffer de linhas antes de enviá-los toohello banco de dados em uma janela de tempo especificado.

Devido a essa compensação, avalie o tipo de Olá das operações que você envia em lote. Utilize o envio em lote de forma mais agressiva (lotes maiores e períodos maiores) com dados menos críticos.

### <a name="batch-size"></a>Tamanho do lote
Em nossos testes, geralmente não houve nenhuma vantagem toobreaking grandes lotes em partes menores. Na verdade, frequentemente essa subdivisão resultou em um desempenho mais lento do que enviar um único lote grande. Por exemplo, considere um cenário onde você deseja tooinsert 1000 linhas. Olá tabela a seguir mostra o tempo de parâmetros com valor de tabela de toouse tooinsert 1000 linhas quando divididas em lotes menores.

| Tamanho do lote | Iterações | Parâmetros com valor de tabela (ms) |
| --- | --- | --- |
| 1000 |1 |347 |
| 500 |2 |355 |
| 100 |10 |465 |
| 50 |20 |630 |

> [!NOTE]
> Os resultados não são parâmetros de comparação. Consulte Olá [Observação sobre resultados neste tópico](#note-about-timing-results-in-this-topic).
> 
> 

Você pode ver que o melhor desempenho de saudação de 1000 linhas é toosubmit-los todos de uma vez. Em outros testes (não mostrados aqui) Houve um toobreak de ganho de desempenho pequeno um lote de 10000 linhas em dois lotes de 5000. Mas o esquema da tabela Olá para esses testes é relativamente simple, portanto, você deve executar testes em seus dados específicos e tooverify de tamanhos de lote essas descobertas.

Tooconsider de outro fator é que, se o lote total Olá ficar muito grande, banco de dados SQL poderá limitar e recusar o lote de saudação toocommit. Para obter melhores resultados de hello, teste toodetermine seu cenário específico se não houver um tamanho de lote ideal. Tornar o tamanho do lote Olá configurável em tempo de execução tooenable ajustes rápidos com base no desempenho ou erros.

Finalmente, equilibre o tamanho de saudação do lote de saudação com hello riscos associados ao envio em lote. Se houver erros transitórios ou função hello falhar, considere as consequências de saudação de repetir a operação de saudação ou de perda de dados de saudação do lote hello.

### <a name="parallel-processing"></a>Processamento paralelo
E se você Olá abordagem de reduzir o tamanho do lote Olá mas usados vários threads tooexecute Olá trabalho? Novamente, nossos testes mostraram que vários lotes menores multithreaded geralmente apresentaram um desempenho pior do que um único lote maior. Olá, teste a seguir tenta tooinsert 1000 linhas em um ou mais lotes paralelos. Este teste mostra como uma quantidade maior de lotes simultâneos na verdade diminuiu o desempenho.

| Tamanho do lote [Iterações] | Dois threads (ms) | Quatro threads (ms) | Seis threads (ms) |
| --- | --- | --- | --- |
| 1000 [1] |277 |315 |266 |
| 500 [2] |548 |278 |256 |
| 250 [4] |405 |329 |265 |
| 100 [10] |488 |439 |391 |

> [!NOTE]
> Os resultados não são parâmetros de comparação. Consulte Olá [Observação sobre resultados neste tópico](#note-about-timing-results-in-this-topic).
> 
> 

Há várias razões possíveis para a diminuição do desempenho de saudação tooparallelism vencimento:

* Há várias chamadas simultâneas de rede em vez de uma.
* Várias operações em uma única tabela podem resultar em contenção e bloqueio.
* Há sobrecargas associadas ao multithreading.
* despesa de saudação de abrir várias conexões supera o benefício de saudação do processamento paralelo.

Se você selecionar bancos de dados ou tabelas diferentes, é possível toosee ganho de alguns desempenho com essa estratégia. A fragmentação ou federações do banco de dados seria um cenário para essa abordagem. Fragmentação usa vários bancos de dados e rotas diferentes dados tooeach banco de dados. Se cada lote pequeno for tooa banco de dados diferente, pode ser mais eficiente, em seguida, executar operações de saudação em paralelo. No entanto, Olá ganho de desempenho não é toouse significativo o suficiente como base de saudação de fragmentação de banco de dados de toouse uma decisão em sua solução.

Em alguns designs, a execução paralela de lotes menores pode resultar em uma produtividade maior das solicitações em um sistema sob carga. Nesse caso, mesmo que seja mais rápido tooprocess um único lote maior, processar vários lotes em paralelo poderá ser mais eficiente.

Se você usar a execução paralela, considere o número de máximo de saudação controladora de threads de trabalho. Uma quantidade menor poderia resultar em menos contenção e um tempo de execução mais rápido. Além disso, considere Olá uma carga adicional que isso coloca nos dados de destino Olá nas conexões e transações.

### <a name="related-performance-factors"></a>Fatores de desempenho relacionados
As orientações típicas sobre o desempenho do banco de dados também dizem respeito ao envio em lote. Por exemplo, ocorre a redução do desempenho de inserção para tabelas com uma chave primária grande ou vários índices não clusterizados.

Se os parâmetros com valor de tabela usam um procedimento armazenado, você pode usar o comando Olá **SET NOCOUNT ON** no início de saudação do procedimento de saudação. Essa instrução suprime o retorno de saudação da contagem de saudação de linhas de saudação afetada no procedimento hello. No entanto, em nossos testes, Olá uso de **SET NOCOUNT ON** não teve nenhum efeito ou diminuiu o desempenho. Olá procedimento armazenado de teste foi simple com um único **inserir** comando de parâmetro com valor de tabela do hello. É possível que outros procedimentos armazenados mais complexos possam se beneficiar dessa instrução. Mas não suponha que a adição **SET NOCOUNT ON** procedimento tooyour armazenado automaticamente melhora o desempenho. toounderstand Olá efeito, teste o procedimento armazenado com e sem Olá **SET NOCOUNT ON** instrução.

## <a name="batching-scenarios"></a>Cenários de envio em lote
Olá seções a seguir descrevem como parâmetros com valor de tabela de toouse em três cenários de aplicativo. Olá primeiro cenário mostra como o buffer e envio em lote podem trabalhar juntos. Olá segundo cenário melhora o desempenho executando operações mestre-detalhes em uma chamada de procedimento armazenado único. Olá cenário final mostra como parâmetros com valor de tabela de toouse em uma operação "UPSERT".

### <a name="buffering"></a>Armazenamento em buffer
Embora alguns cenários sejam candidatos óbvios ao envio em lote, há muitos cenários que poderiam se beneficiar do envio em lote por meio do processamento atrasado. No entanto, o processamento atrasado também apresenta um risco maior que dados hello serão perdidos em caso de saudação de uma falha inesperada. É importante toounderstand esse risco e considerar as consequências de saudação.

Por exemplo, considere um aplicativo web que controla o histórico de navegação de saudação de cada usuário. Em cada solicitação de página, aplicativo hello pode fazer a exibição de página do banco de dados chamada toorecord saudação do usuário. Mas o melhor desempenho e escalabilidade podem ser obtidos com atividades de navegação dos usuários da saudação de buffer e, em seguida, enviar esse banco de dados de toohello de dados em lotes. Você pode disparar a atualização do banco de dados de saudação pelo tempo decorrido e/ou o tamanho do buffer. Por exemplo, uma regra pode especificar que esse lote Olá deve ser processado depois de 20 segundos ou quando o buffer de saudação atingir 1000 itens.

usos de exemplo de código a seguir Olá [extensões reativas - Rx](https://msdn.microsoft.com/data/gg577609) tooprocess em buffer os eventos gerados por uma classe de monitoramento. Olá quando preenchimentos de buffer ou um tempo limite é atingido, lote Olá dos dados do usuário é enviado toohello banco de dados com um parâmetro com valor de tabela.

Olá NavHistoryData classe modelos Olá usuário navegação detalhes a seguir. Contém informações básicas, como o identificador de usuário hello, Olá URL acessada e Olá tempo de acesso.

    public class NavHistoryData
    {
        public NavHistoryData(int userId, string url, DateTime accessTime)
        { UserId = userId; URL = url; AccessTime = accessTime; }
        public int UserId { get; set; }
        public string URL { get; set; }
        public DateTime AccessTime { get; set; }
    }

Olá classe NavHistoryDataMonitor é responsável por buffer Olá usuário navegação dados toohello banco de dados. Ela contém um método, RecordUserNavigationEntry, que responde gerando um evento **OnAdded** . Olá código a seguir mostra a lógica do construtor Olá que usa Rx toocreate uma coleção observável com base em evento hello. Ele, em seguida, assina coleção observável toothis com método de Buffer hello. sobrecarga de saudação especifica que buffer Olá deve ser enviado a cada 20 segundos ou 1000 entradas.

    public NavHistoryDataMonitor()
    {
        var observableData =
            Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

        observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
    }

manipulador de saudação converte todos os itens de saudação em buffer em um tipo com valor de tabela e passa esse procedimento de tooa armazenado tipo daquele lote de saudação de processos. Olá código a seguir mostra a definição completa Olá Olá NavHistoryDataEventArgs e classes de NavHistoryDataMonitor hello.

    public class NavHistoryDataEventArgs : System.EventArgs
    {
        public NavHistoryDataEventArgs(NavHistoryData data) { Data = data; }
        public NavHistoryData Data { get; set; }
    }

    public class NavHistoryDataMonitor
    {
        public event EventHandler<NavHistoryDataEventArgs> OnAdded;

        public NavHistoryDataMonitor()
        {
            var observableData =
                Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

            observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
        }

        public void RecordUserNavigationEntry(NavHistoryData data)
        {    
            if (OnAdded != null)
                OnAdded(this, new NavHistoryDataEventArgs(data));
        }

        protected void Handler(IList<EventPattern<NavHistoryDataEventArgs>> items)
        {
            DataTable navHistoryBatch = new DataTable("NavigationHistoryBatch");
            navHistoryBatch.Columns.Add("UserId", typeof(int));
            navHistoryBatch.Columns.Add("URL", typeof(string));
            navHistoryBatch.Columns.Add("AccessTime", typeof(DateTime));
            foreach (EventPattern<NavHistoryDataEventArgs> item in items)
            {
                NavHistoryData data = item.EventArgs.Data;
                navHistoryBatch.Rows.Add(data.UserId, data.URL, data.AccessTime);
            }

            using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
            {
                connection.Open();

                SqlCommand cmd = new SqlCommand("sp_RecordUserNavigation", connection);
                cmd.CommandType = CommandType.StoredProcedure;

                cmd.Parameters.Add(
                    new SqlParameter()
                    {
                        ParameterName = "@NavHistoryBatch",
                        SqlDbType = SqlDbType.Structured,
                        TypeName = "NavigationHistoryTableType",
                        Value = navHistoryBatch,
                    });

                cmd.ExecuteNonQuery();
            }
        }
    }

toouse essa classe de buffer, o aplicativo hello cria um objeto NavHistoryDataMonitor estático. Cada vez que um usuário acessa uma página, aplicativo hello chama o método de NavHistoryDataMonitor.RecordUserNavigationEntry hello. Olá buffer lógica continua tootake respeito enviar esses bancos de dados de toohello entradas em lotes.

### <a name="master-detail"></a>Detalhes da tabela mestra
Parâmetros com valor de tabela são úteis para cenários INSERT simples. No entanto, pode ser mais difícil inserções toobatch que envolvem mais de uma tabela. cenário de "mestre/detalhes" Hello é um bom exemplo. tabela mestre Olá identifica a entidade principal hello. Uma ou mais tabelas de detalhes armazenam mais dados sobre a entidade de saudação. Nesse cenário, relações de chave estrangeira impõem relação Olá de entidade mestra exclusiva de tooa detalhes. Considere uma versão simplificada de uma tabela PurchaseOrder e sua tabela associada OrderDetail. Olá Transact-SQL a seguir cria a tabela de PurchaseOrder de saudação com quatro colunas: Status, OrderDate, CustomerID e OrderID.

    CREATE TABLE [dbo].[PurchaseOrder](
    [OrderID] [int] IDENTITY(1,1) NOT NULL,
    [OrderDate] [datetime] NOT NULL,
    [CustomerID] [int] NOT NULL,
    [Status] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrder] 
    PRIMARY KEY CLUSTERED ( [OrderID] ASC ))

Cada pedido contém uma ou mais compras de produtos. Essas informações são capturadas na tabela de PurchaseOrderDetail hello. Olá Transact-SQL a seguir cria a tabela PurchaseOrderDetail de saudação com cinco colunas: OrderID, OrderDetailID, ProductID, UnitPrice e OrderQty.

    CREATE TABLE [dbo].[PurchaseOrderDetail](
    [OrderID] [int] NOT NULL,
    [OrderDetailID] [int] IDENTITY(1,1) NOT NULL,
    [ProductID] [int] NOT NULL,
    [UnitPrice] [money] NULL,
    [OrderQty] [smallint] NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrderDetail] PRIMARY KEY CLUSTERED 
    ( [OrderID] ASC, [OrderDetailID] ASC ))

coluna de OrderID Olá na tabela de PurchaseOrderDetail Olá deve fazer referência a uma ordem da tabela de PurchaseOrder hello. Olá após a definição de uma chave estrangeira impõe essa restrição.

    ALTER TABLE [dbo].[PurchaseOrderDetail]  WITH CHECK ADD 
    CONSTRAINT [FK_OrderID_PurchaseOrder] FOREIGN KEY([OrderID])
    REFERENCES [dbo].[PurchaseOrder] ([OrderID])

Ordem toouse com valor de tabela parâmetros in, você deve ter um tipo de tabela definido pelo usuário para cada tabela de destino.

    CREATE TYPE PurchaseOrderTableType AS TABLE 
    ( OrderID INT,
      OrderDate DATETIME,
      CustomerID INT,
      Status NVARCHAR(50) );
    GO

    CREATE TYPE PurchaseOrderDetailTableType AS TABLE 
    ( OrderID INT,
      ProductID INT,
      UnitPrice MONEY,
      OrderQty SMALLINT );
    GO

Em seguida, defina um procedimento armazenado que aceite tabelas desses tipos. Esse procedimento permite que um aplicativo toolocally lote um conjunto de pedidos e detalhes do pedido em uma única chamada. Olá Transact-SQL a seguir fornece Olá declaração de procedimento armazenado completa para este exemplo de ordem de compra.

    CREATE PROCEDURE sp_InsertOrdersBatch (
    @orders as PurchaseOrderTableType READONLY,
    @details as PurchaseOrderDetailTableType READONLY )
    AS
    SET NOCOUNT ON;

    -- Table that connects hello order identifiers in hello @orders
    -- table with hello actual order identifiers in hello PurchaseOrder table
    DECLARE @IdentityLink AS TABLE ( 
    SubmittedKey int, 
    ActualKey int, 
    RowNumber int identity(1,1)
    );

          -- Add new orders toohello PurchaseOrder table, storing hello actual
    -- order identifiers in hello @IdentityLink table   
    INSERT INTO PurchaseOrder ([OrderDate], [CustomerID], [Status])
    OUTPUT inserted.OrderID INTO @IdentityLink (ActualKey)
    SELECT [OrderDate], [CustomerID], [Status] FROM @orders ORDER BY OrderID;

    -- Match hello passed-in order identifiers with hello actual identifiers
    -- and complete hello @IdentityLink table for use with inserting hello details
    WITH OrderedRows As (
    SELECT OrderID, ROW_NUMBER () OVER (ORDER BY OrderID) As RowNumber 
    FROM @orders
    )
    UPDATE @IdentityLink SET SubmittedKey = M.OrderID
    FROM @IdentityLink L JOIN OrderedRows M ON L.RowNumber = M.RowNumber;

    -- Insert hello order details into hello PurchaseOrderDetail table, 
          -- using hello actual order identifiers of hello master table, PurchaseOrder
    INSERT INTO PurchaseOrderDetail (
    [OrderID],
    [ProductID],
    [UnitPrice],
    [OrderQty] )
    SELECT L.ActualKey, D.ProductID, D.UnitPrice, D.OrderQty
    FROM @details D
    JOIN @IdentityLink L ON L.SubmittedKey = D.OrderID;
    GO

Neste exemplo, Olá definidos localmente @IdentityLink tabela armazena valores reais de OrderID Olá das linhas recentemente inserida de saudação. Esses identificadores de ordem sejam diferentes dos valores de OrderID temporários Olá no hello @orders e @details parâmetros com valor de tabela. Por esse motivo, Olá @IdentityLink tabela, em seguida, conecta-se valores de OrderID Olá em Olá @orders toohello real OrderID valores de parâmetro para novas linhas Olá na tabela de PurchaseOrder hello. Após essa etapa, Olá @IdentityLink pode facilitar a tabela Detalhes do pedido Olá inserindo com hello OrderID real que satisfaz a restrição de chave estrangeira hello.

Esse procedimento armazenado pode ser usado do código ou de outras chamadas Transact-SQL. Consulte a seção de parâmetros com valor de tabela de saudação deste documento para obter um exemplo de código. Olá Transact-SQL a seguir mostra como toocall Olá sp_InsertOrdersBatch.

    declare @orders as PurchaseOrderTableType
    declare @details as PurchaseOrderDetailTableType

    INSERT @orders 
    ([OrderID], [OrderDate], [CustomerID], [Status])
    VALUES(1, '1/1/2013', 1125, 'Complete'),
    (2, '1/13/2013', 348, 'Processing'),
    (3, '1/12/2013', 2504, 'Shipped')

    INSERT @details
    ([OrderID], [ProductID], [UnitPrice], [OrderQty])
    VALUES(1, 10, $11.50, 1),
    (1, 12, $1.58, 1),
    (2, 23, $2.57, 2),
    (3, 4, $10.00, 1)

    exec sp_InsertOrdersBatch @orders, @details

Esta solução permite que cada lote toouse um conjunto de valores de OrderID que começam com 1. Os valores de OrderID temporários descrevem relações Olá em lote hello, mas valores reais de OrderID Olá são determinados no tempo de saudação da operação de inserção de saudação. Você pode executar Olá mesmas instruções no exemplo anterior Olá repetidamente e gerar pedidos exclusivos no banco de dados de saudação. Por esse motivo, considere a adição de mais código ou lógica de banco de dados que impeça os pedidos duplicados ao usar esta técnica de envio em lote.

Este exemplo demonstra que até mesmo as operações de banco de dados mais complexas, como operações de mestre-detalhes, podem ser enviadas em lote usando parâmetros com valor de tabela.

### <a name="upsert"></a>UPSERT
Outro cenário de envio em lote envolve a atualização simultânea de linhas existentes e a inserção de novas linhas. Esta operação é às vezes chamado tooas uma operação "UPSERT" (atualização + inserção). Em vez de fazer chamadas separadas tooINSERT e atualização, instrução de mesclagem Olá é melhor adequada toothis tarefa. Olá instrução MERGE pode executar os dois insert e operações em uma única chamada de atualização.

Parâmetros com valor de tabela podem ser usados com hello mesclagem instrução tooperform atualizações e inserções. Por exemplo, considere uma tabela funcionário simplificada que contém Olá colunas a seguir: EmployeeID, FirstName, LastName, NúmeroDoINPS:

    CREATE TABLE [dbo].[Employee](
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [SocialSecurityNumber] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_Employee] PRIMARY KEY CLUSTERED 
    ([EmployeeID] ASC ))

Neste exemplo, você pode usar o fato de saudação que Olá NúmeroDoINPS é exclusivo tooperform uma mesclagem de vários funcionários. Primeiro, crie o tipo de tabela definido pelo usuário de saudação:

    CREATE TYPE EmployeeTableType AS TABLE 
    ( Employee_ID INT,
      FirstName NVARCHAR(50),
      LastName NVARCHAR(50),
      SocialSecurityNumber NVARCHAR(50) );
    GO

Em seguida, criar um procedimento armazenado ou escreva código que usa Olá atualização de saudação de tooperform de instrução direta e insert. Olá exemplo a seguir usa Olá instrução MERGE em um parâmetro com valor de tabela, @employees, do tipo EmployeeTableType. Olá conteúdo da saudação @employees tabela não são mostradas aqui.

    MERGE Employee AS target
    USING (SELECT [FirstName], [LastName], [SocialSecurityNumber] FROM @employees) 
    AS source ([FirstName], [LastName], [SocialSecurityNumber])
    ON (target.[SocialSecurityNumber] = source.[SocialSecurityNumber])
    WHEN MATCHED THEN 
    UPDATE SET
    target.FirstName = source.FirstName, 
    target.LastName = source.LastName
    WHEN NOT MATCHED THEN
       INSERT ([FirstName], [LastName], [SocialSecurityNumber])
       VALUES (source.[FirstName], source.[LastName], source.[SocialSecurityNumber]);

Para obter mais informações, consulte documentação hello e exemplos Olá instrução de mesclagem. Embora Olá mesmo trabalho possa ser executado em várias etapas armazenados chamada de procedimento com operações INSERT e UPDATE separadas, Olá instrução MERGE é mais eficiente. Código do banco de dados também pode criar as chamadas Transact-SQL que usam a instrução de mesclagem Olá diretamente sem exigir duas chamadas de banco de dados para INSERT e UPDATE.

## <a name="recommendation-summary"></a>Resumo de recomendações
Olá lista a seguir fornece um resumo da saudação envio em lote recomendações discutidas neste tópico:

* Use buffer e envio em lote de desempenho de saudação tooincrease e escalabilidade de aplicativos de banco de dados SQL.
* Entenda as compensações de saudação entre o envio em lote/buffer e a resiliência. Durante uma falha de função, o risco de saudação de perder um lote não processado de dados essenciais aos negócios pode compensar benefício de desempenho de saudação do envio em lote.
* Tentativa de tookeep todas as chamadas toohello banco de dados de latência de tooreduce um único datacenter.
* Se você escolher uma única técnica de envio em lote, parâmetros com valor de tabela oferecem flexibilidade e Olá melhor desempenho.
* Para hello mais rápido desempenho de inserção, siga estas diretrizes gerais mas testar seu cenário:
  * Para menos de 100 linhas, use um único comando INSERT com parâmetros.
  * Para menos de 1000 linhas, use parâmetros com valor de tabela.
  * Para 1000 linhas ou mais, use SqlBulkCopy.
* Para atualizar e excluir operações, use parâmetros com valor de tabela com a lógica de procedimento armazenado que determina a operação correta de saudação em cada linha no parâmetro de tabela hello.
* Diretrizes para o tamanho do lote:
  * Use Olá tamanhos de lote maiores que fazem sentido para o aplicativo e os requisitos de negócios.
  * Ganho de desempenho de saudação do saldo de lotes grandes com riscos de saudação de falhas catastróficas ou temporárias. O que é a consequência de saudação de repetições ou perda de dados de saudação em lote Olá? 
  * Teste Olá maior lote tamanho tooverify que banco de dados SQL não rejeitá-la.
  * Crie definições de configuração que controle envio em lote, como tamanho de lote de saudação ou janela de tempo de buffer de saudação. Essas configurações fornecem flexibilidade. Você pode alterar Olá envio em lote comportamento na produção sem reimplantar o serviço de nuvem hello.
* Evite a execução paralela de lotes que operam em uma única tabela em um banco de dados. Se você escolher toodivide um único lote em vários threads de trabalho, execute testes toodetermine Olá número ideal de threads. Após um limite não especificado, uma quantidade maior de threads diminuirá o desempenho em vez de aumentá-lo.
* Considere o armazenamento em buffer de acordo com o tamanho e o tempo como uma maneira de implementar o envio em lote para mais cenários.

## <a name="next-steps"></a>Próximas etapas
Este artigo se concentra em como o design de banco de dados e técnicas de codificação relacionam toobatching pode melhorar o desempenho do aplicativo e a escalabilidade. Mas isso é apenas um fator em sua estratégia geral. Para obter escalabilidade e desempenho de tooimprove maneiras, consulte [diretrizes de desempenho de banco de dados SQL para bancos de dados único](sql-database-performance-guidance.md) e [considerações de preço e desempenho para um pool Elástico](sql-database-elastic-pool-guidance.md).

