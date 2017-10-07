---
title: diretrizes de ajuste de desempenho de banco de dados SQL de aaaAzure | Microsoft Docs
description: "Este artigo pode ajudar a determinar qual toochoose de nível de serviço para seu aplicativo. Ele também recomenda maneiras tootune saudação de tooget seu aplicativo mais do banco de dados do SQL Azure."
services: sql-database
documentationcenter: na
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: dd8d95fa-24b2-4233-b3f1-8e8952a7a22b
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 02/09/2017
ms.author: carlrab
ms.openlocfilehash: 2699f755391e94ab488ac1e6acedd30f8aec4488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tuning-performance-in-azure-sql-database"></a>Ajustando o desempenho no Banco de Dados SQL do Azure

Banco de dados SQL do Azure fornece [recomendações](sql-database-advisor.md) que você pode usar tooimprove o desempenho do banco de dados, ou você pode deixar o banco de dados do SQL Azure [adaptar automaticamente o aplicativo tooyour](sql-database-automatic-tuning.md) e aplicar alterações que melhora o desempenho da carga de trabalho.

Você não tem nenhuma recomendação aplicável e ainda tiver problemas de desempenho, você pode usar o hello desempenhos de tooimprove dos métodos a seguir:
1. Aumentar [camadas de serviço](sql-database-service-tiers.md) e fornecer o banco de dados do mais recursos tooyour.
2. Ajustar o aplicativo e aplicar algumas melhores práticas que podem melhorar o desempenho. 
3. Ajuste o banco de dados de saudação Alterando consultas toomore trabalhar com eficiência com dados e índices.

Estes são os métodos manuais porque você o que precisa toodecide [camadas de serviço](sql-database-service-tiers.md) escolha ou seria necessário toorewrite aplicativo ou código de banco de dados e deply alterações hello.

## <a name="increasing-performance-tier-of-your-database"></a>Aumentando o nível de desempenho do banco de dados

O Banco de Dados SQL do Azure oferece quatro [camadas de serviço](sql-database-service-tiers.md) que estão à sua disposição: Básico, Standard, Premium e Premium RS (o desempenho é medido em unidades de produtividade do banco de dados ou [DTUs](sql-database-what-is-a-dtu.md). Cada camada de serviço isola estritamente recursos Olá que seu banco de dados SQL pode usar e garante um desempenho previsível para esse nível de serviço. Neste artigo, nós oferecemos orientações que podem ajudá-lo a escolher a camada de serviço Olá para seu aplicativo. Também discutimos maneiras que você pode ajustar a saudação de tooget aplicativo máximo do banco de dados do SQL Azure.

> [!NOTE]
> Este artigo se concentra em fornecer orientações sobre o desempenho de bancos de dados únicos no Banco de Dados SQL do Azure. Para obter diretrizes de desempenho pools tooelastic relacionados, consulte [considerações sobre preço e desempenho de pools Elásticos](sql-database-elastic-pool-guidance.md). Observe, porém, você pode aplicar muitos Olá toodatabases neste artigo em um pool Elástico recomendações de ajuste e obter benefícios de desempenho semelhante.
> 

* **Básico**: Olá serviço básico da camada oferece bom desempenho previsibilidade para cada banco de dados, a hora em hora. Em um banco de dados Básico, recursos suficientes dão suporte ao bom desempenho em um banco de dados pequeno que não tem várias solicitações simultâneas. Os casos de uso típicos em que você usará a camada de serviço Básica são:
  * **Você está apenas começando a usar o Banco de Dados SQL do Azure**. Aplicativos que estão em desenvolvimento normalmente não precisam de altos níveis de desempenho. Os bancos de dados Básicos são um ambiente ideal para o desenvolvimento ou teste de banco de dados, por uma faixa de preço reduzida.
  * **Você tem um banco de dados com um único usuário**. Aplicativos que associam um único usuário a um banco de dados normalmente não têm requisitos altos em termos de simultaneidade e desempenho. Esses aplicativos são candidatos para a camada de serviço Basic hello.
* **Padrão**: camada de serviço Standard Olá oferece melhor desempenho previsibilidade e fornece um bom desempenho para bancos de dados com várias solicitações simultâneas, como aplicativos web e de grupo de trabalho. Quando escolhe um banco de dados da camada de serviço Standard, você pode dimensionar seu aplicativo de banco de dados com base em um desempenho previsível, minuto a minuto.
  * **Seu banco de dados tem várias solicitações simultâneas**. Aplicativos que atendem mais de um usuário por vez normalmente precisam de níveis de desempenho mais altos. Por exemplo, aplicativos da web ou de grupo de trabalho que têm requisitos de tráfego de e/s toomedium baixa permitindo várias consultas simultâneas são bons candidatos para a camada de serviço Standard hello.
* **Premium**: camada de serviço Premium Olá oferece desempenho previsível, segundo por segundo, para cada banco de dados Premium. Quando você escolhe a camada de serviço Premium Olá, você pode dimensionar seu aplicativo de banco de dados com base na carga de pico de saudação do banco de dados. plano de saudação remove os casos em que a variação de desempenho pode fazer consultas pequenas tootake mais tempo que o esperado em operações sensíveis à latência. Esse modelo pode simplificar muito os ciclos de validação de desenvolvimento e produtos de saudação para aplicativos que precisam toomake de instruções fortes sobre necessidades de recursos de pico, variação de desempenho ou a latência da consulta. A maioria dos casos de uso da camada de serviço Premium tem uma ou mais destas características:
  * **Alta carga de pico**. Um aplicativo que requer substancial CPU, memória ou entrada/saída (e/s) toocomplete suas operações requer um nível dedicado, de alto desempenho. Por exemplo, uma operação de banco de dados conhecidos tooconsume vários núcleos de CPU por um longo período é um candidato à camada de serviço Premium Olá.
  * **Muitas solicitações simultâneas**. Alguns aplicativos de banco de dados atendem muitas solicitações simultâneas, por exemplo, ao servir um site com alto volume de tráfego. Básico e padrão camadas de serviço limitam o número de saudação de solicitações simultâneas por banco de dados. Aplicativos que exigem mais conexões precisariam toochoose um apropriado de reserva tamanho toohandle Olá número máximo de solicitações necessárias.
  * **Baixa latência**. Alguns aplicativos precisam de uma resposta do banco de dados de saudação do tooguarantee no tempo mínimo. Se um procedimento armazenado específico for chamado como parte de uma operação mais ampla do cliente, você pode ter um requisito toohave um retorno de chamada em não mais do que 20 milissegundos, 99% do tempo de saudação. Esse tipo de benefícios de aplicativo da camada de serviço Premium Olá, toomake-se de que Olá necessários a capacidade de computação está disponível.
* **Premium RS**: Olá camada Premium RS foi projetado para cargas de trabalho com uso intensivo de e/s que não exigem hello mais alta garantia de disponibilidade. Exemplos de teste de cargas de trabalho de alto desempenho, ou uma carga de trabalho analítica onde o banco de dados de saudação não é sistema saudação do registro.

nível de serviço de saudação que você precisa para seu banco de dados do SQL depende de requisitos de carga de pico Olá para cada dimensão de recurso. Alguns aplicativos usam quantidades comuns de um recurso, mas têm requisitos significativos para outros recursos.

### <a name="service-tier-capabilities-and-limits"></a>Limites e recursos da camada de serviço

Em cada camada de serviço, você deve definir um nível de desempenho Olá, para que você tenha Olá flexibilidade toopay apenas para a capacidade de saudação que é necessário. Você pode [ajustar a capacidade](sql-database-service-tiers.md), aumentando ou reduzindo-a, conforme a carga de trabalho mudar. Por exemplo, se sua carga de trabalho do banco de dados for alta durante a temporada de compras de volta às aulas hello, poderá aumentar o nível de desempenho de saudação do banco de dados de saudação para um período de tempo, julho a setembro. Você pode reduzi-lo quando sua temporada de pico terminar. Você pode minimizar o que você paga otimizando seu periodicidade de toohello do ambiente de nuvem de sua empresa. Esse modelo também funciona bem para ciclos de lançamento de produto de software. Uma equipe de teste pode alocar capacidade ao executar testes e liberar essa capacidade quando os testes forem concluídos. Em um modelo de solicitação de capacidade, você paga pela capacidade conforme precisa dela e evita gastos com recursos dedicados que raramente são usados.

### <a name="why-service-tiers"></a>Por que usar camadas de serviço?
Embora cada carga de trabalho do banco de dados diferente, a finalidade de saudação das camadas de serviço é tooprovide a previsibilidade do desempenho em vários níveis de desempenho. Clientes com requisitos de recursos de bancos de dados de grande escala podem trabalhar em um ambiente de computação mais dedicado.

## <a name="tune-your-application"></a>Ajustar seu aplicativo
No SQL Server local tradicional Olá processo de planejamento de capacidade inicial geralmente é separado do processo de saudação da execução de um aplicativo em produção. Hardwares e licenças de produtos são comprados primeiro e o ajuste de desempenho é feito posteriormente. Quando você usa o banco de dados do SQL Azure, é um boa ideia toointerweave Olá processo executando um aplicativo e ajuste. Com o modelo de saudação de pagar pela capacidade sob demanda, você pode ajustar seu aplicativo toouse Olá recursos mínimos necessários agora, em vez de excesso de provisionamento de hardware com base em palpites de planos de crescimento futuro para um aplicativo, que geralmente estão incorretos. Alguns clientes podem escolher não tootune um aplicativo e escolha toooverprovision recursos de hardware. Essa abordagem pode ser uma boa ideia se você não quiser toochange aplicativo principal durante um período ocupado. Porém, o ajuste de um aplicativo pode reduzir os requisitos de recursos e diminuir as contas mensais ao usar camadas de serviço Olá no banco de dados do SQL Azure.

### <a name="application-characteristics"></a>Características do aplicativo
Embora as camadas de serviço de banco de dados SQL são projetadas tooimprove estabilidade do desempenho e a previsibilidade de um aplicativo, algumas práticas recomendadas podem ajudá-lo a ajustar seu aplicativo toobetter aproveitar recursos de saudação em um nível de desempenho. Embora muitos aplicativos têm ganhos de desempenho significativos simplesmente pela alternância tooa mais alto nível de desempenho ou serviço de camada, alguns aplicativos precisam adicionais de ajuste toobenefit de um nível mais alto de serviço. Para melhorar o desempenho, considere realizar ajustes adicionais em aplicativos que têm estas características:

* **Aplicativos que têm desempenho lento devido a um comportamento "barulhento"**. Aplicativos verborrágicas fazer operações de acesso de dados em excesso são confidenciais toonetwork latência. Talvez seja necessário toomodify esses tipos de número de saudação de tooreduce aplicativos de banco de dados do data access operações toohello SQL. Por exemplo, você pode melhorar o desempenho do aplicativo usando técnicas como envio em lote de consultas ad hoc ou movendo Olá consultas toostored procedimentos. Para obter mais informações, consulte [Consultas em lote](#batch-queries).
* **Bancos de dados com uma carga de trabalho intensiva que não podem ter suporte de um único computador inteiro**. Bancos de dados que excedem os recursos de saudação do mais alto nível de desempenho Premium Olá podem se beneficiar com a expansão da carga de trabalho de saudação. Para obter mais informações, consulte [Fragmentação entre banco de dados](#cross-database-sharding) e [Particionamento funcional](#functional-partitioning).
* **Aplicativos com consultas de qualidade inferior**. Aplicativos, especialmente aqueles na camada de acesso de dados hello, que têm consultas mal ajustadas talvez não se beneficiar de um nível de desempenho superior. Isso inclui consultas sem uma cláusula WHERE, com índices ausentes ou com estatísticas desatualizadas. Esses aplicativos se beneficiam de técnicas de ajuste de desempenho de consulta padrão. Para obter mais informações, consulte [Índices ausentes](#identifying-and-adding-missing-indexes) e [Ajuste e dicas de consulta](#query-tuning-and-hinting).
* **Aplicativos com design de acesso a dados de qualidade inferior**. Aplicativos com problemas de simultaneidade de acesso a dados intrínsecos, por exemplo, deadlock, talvez não se beneficiem da seleção de um nível mais alto de desempenho. Considere a redução de viagens de ida e contra Olá banco de dados SQL armazenando em cache dados no lado do cliente de saudação com hello Azure Caching service ou outra tecnologia de armazenamento em cache. Consulte [Cache da camada de aplicativo](#application-tier-caching).

## <a name="tune-your-database"></a>Ajustar o banco de dados
Nesta seção, vamos examinar algumas técnicas que você pode usar tootune Azure SQL Database toogain Olá melhor desempenho para seu aplicativo e executá-lo no nível mais baixo de desempenho possível hello. Algumas dessas técnicas tradicionais do SQL Server práticas recomendadas de ajuste de corresponder, mas outras são específica tooAzure banco de dados SQL. Em alguns casos, você pode examinar os recursos de saudação consumido para um ajuste do banco de dados toofind áreas toofurther e estender toowork de técnicas tradicional do SQL Server no banco de dados do SQL Azure.

### <a name="identify-performance-issues-using-azure-portal"></a>Identificar problemas de desempenho usando o portal do Azure
Olá ferramentas no portal do Azure de saudação a seguir pode ajudá-lo a analisar e corrigir problemas de desempenho com o banco de dados SQL:

* [Visão de Desempenho de Consulta](sql-database-query-performance.md)
* [Advisor do Banco de Dados SQL](sql-database-advisor.md)

Olá, portal do Azure tem mais informações sobre essas duas ferramentas e como toouse-los. tooefficiently diagnosticar e corrigir problemas, recomendamos que você primeiro tente ferramentas Olá Olá portal do Azure. É recomendável que você use manual Olá ajuste abordagens que discutiremos a seguir, faltam índices e ajuste de consulta, em casos especiais.

Encontre mais informações sobre como identificar problemas no Banco de Dados SQL do Azure no artigo [Monitoramento de desempenho](sql-database-single-database-monitor.md).

### <a name="identifying-and-adding-missing-indexes"></a>Identificando e adicionando índices ausentes
Um problema comum no desempenho do banco de dados OLTP está relacionado a toohello design de banco de dados físico. Com frequência, os esquemas de banco de dados são projetados e enviados sem testes em escala (seja na carga ou no volume de dados). Infelizmente, desempenho de saudação de um plano de consulta pode ser aceitável em pequena escala, mas ser substancialmente em volumes de dados de nível de produção. origem de Hello mais comum desse problema é a falta de saudação de filtros de toosatisfy de índices apropriados ou outras restrições em uma consulta. Geralmente, os índices ausentes se manifestam como uma verificação de tabela quando uma busca de índice poderia bastar.

Neste exemplo, o plano de consulta selecionado Olá usa uma verificação de quando uma pesquisa seria suficiente:

    DROP TABLE dbo.missingindex;
    CREATE TABLE dbo.missingindex (col1 INT IDENTITY PRIMARY KEY, col2 INT);
    DECLARE @a int = 0;
    SET NOCOUNT ON;
    BEGIN TRANSACTION
    WHILE @a < 20000
    BEGIN
        INSERT INTO dbo.missingindex(col2) VALUES (@a);
        SET @a += 1;
    END
    COMMIT TRANSACTION;
    GO
    SELECT m1.col1
    FROM dbo.missingindex m1 INNER JOIN dbo.missingindex m2 ON(m1.col1=m2.col1)
    WHERE m1.col2 = 4;

![Plano de consulta com índices ausentes](./media/sql-database-performance-guidance/query_plan_missing_indexes.png)

O Banco de Dados SQL do Azure pode ajudá-lo a localizar e corrigir condições comuns de índice ausente. DMVs que são integrados ao banco de dados do SQL Azure examinar compilações de consulta no qual um índice reduziria significativamente os toorun de custo estimada de saudação uma consulta. Durante a execução de consulta, banco de dados SQL controla quantas vezes cada plano de consulta é executado e Olá rastreia estimado lacuna entre Olá Olá e plano de consulta em execução imaginado um onde esse índice existia. Você pode usar a estimativa de tooquickly esses DMVs quais alterações tooyour design físico pode melhorar o custo de carga de trabalho geral para um banco de dados e sua carga de trabalho real.

Você pode usar o potencial de tooevaluate esta consulta índices ausentes:

    SELECT CONVERT (varchar, getdate(), 126) AS runtime,
        mig.index_group_handle, mid.index_handle,
        CONVERT (decimal (28,1), migs.avg_total_user_cost * migs.avg_user_impact *
                (migs.user_seeks + migs.user_scans)) AS improvement_measure,
        'CREATE INDEX missing_index_' + CONVERT (varchar, mig.index_group_handle) + '_' +
                  CONVERT (varchar, mid.index_handle) + ' ON ' + mid.statement + '
                  (' + ISNULL (mid.equality_columns,'')
                  + CASE WHEN mid.equality_columns IS NOT NULL
                              AND mid.inequality_columns IS NOT NULL
                         THEN ',' ELSE '' END + ISNULL (mid.inequality_columns, '')
                  + ')'
                  + ISNULL (' INCLUDE (' + mid.included_columns + ')', '') AS create_index_statement,
        migs.*,
        mid.database_id,
        mid.[object_id]
    FROM sys.dm_db_missing_index_groups AS mig
    INNER JOIN sys.dm_db_missing_index_group_stats AS migs
        ON migs.group_handle = mig.index_group_handle
    INNER JOIN sys.dm_db_missing_index_details AS mid
        ON mig.index_handle = mid.index_handle
    ORDER BY migs.avg_total_user_cost * migs.avg_user_impact * (migs.user_seeks + migs.user_scans) DESC

Neste exemplo, a consulta de saudação resultou em sua sugestão:

    CREATE INDEX missing_index_5006_5005 ON [dbo].[missingindex] ([col2])  

Depois de criado, essa mesma instrução SELECT escolhe um plano diferente, que usa uma busca em vez de uma verificação e, em seguida, executa o plano de saudação com mais eficiência:

![Plano de consulta com índices corrigidos](./media/sql-database-performance-guidance/query_plan_corrected_indexes.png)

informações de chave de saudação é essa capacidade de e/s de compartilhado hello, sistema de mercadorias é mais limitado do que uma máquina de servidor dedicado. Há um bônus minimizando o desnecessária e/s tootake máximo proveito do sistema de saudação no hello DTU de cada nível de desempenho das camadas de serviço do Azure SQL Database hello. Opções de design de banco de dados físico apropriado significativamente podem melhorar a latência de saudação para consultas individuais, melhorar a taxa de transferência de saudação de solicitações simultâneas tratadas por unidade de escala e minimizar a consulta de Olá Olá custos toosatisfy necessário. Para obter mais informações sobre Olá ausente DMVs de índice, consulte [sys.DM db_missing_index_details](https://msdn.microsoft.com/library/ms345434.aspx).

### <a name="query-tuning-and-hinting"></a>Ajuste e dicas de consulta
Otimizador de consulta de saudação do banco de dados do SQL Azure é semelhante toohello tradicional do SQL Server Otimizador de consulta. A maioria das práticas recomendadas de saudação para ajustar consultas e Olá Noções básicas sobre raciocínio limitações de modelo para o otimizador de consulta Olá também se aplicam a tooAzure banco de dados SQL. Se você ajustar consultas no banco de dados do SQL Azure, você pode obter o benefício adicional de saudação de reduzir as demandas de recursos agregados. Seu aplicativo pode ser capaz de toorun em um custo menor do que um equivalente não ajustado porque ele pode ser executado em um nível de desempenho inferior.

Um exemplo que é comum no SQL Server e que também se aplica a tooAzure banco de dados SQL é como Olá otimizador "detecta" parâmetros da consulta. Durante a compilação, o otimizador de consulta Olá avalia valor atual de saudação do toodetermine parâmetro se ele pode gerar um plano de consulta melhor. Embora essa estratégia pode levar geralmente tooa plano de consulta significativamente mais rápido do que um plano compilado sem valores de parâmetro conhecidos, atualmente funciona imperfectly tanto no SQL Server e no banco de dados do SQL Azure. Às vezes, o parâmetro hello não é detectado e, às vezes, o parâmetro hello é detectado, mas plano gerado hello está abaixo do ideal para o conjunto completo de valores de parâmetro em uma carga de trabalho de saudação. A Microsoft inclui dicas de consulta (diretivas) para que você pode especificar a intenção mais deliberadamente e substituir o comportamento padrão de saudação de detecção de parâmetro. Geralmente, se você usar dicas, você pode corrigir casos nos quais o saudação padrão do SQL Server ou banco de dados do SQL Azure comportamento é imperfeito para uma carga de trabalho de cliente específico.

Olá exemplo a seguir demonstra como o processador de consultas Olá pode gerar um plano que está abaixo do ideal para desempenho e requisitos de recursos. Este exemplo também mostra que, se usar uma dica de consulta, você poderá reduzir requisitos de recursos e tempo de execução da consulta para o banco de dados SQL:

    DROP TABLE psptest1;
    CREATE TABLE psptest1(col1 int primary key identity, col2 int, col3 binary(200));

    DECLARE @a int = 0;
    SET NOCOUNT ON;
    BEGIN TRANSACTION
    WHILE @a < 20000
    BEGIN
        INSERT INTO psptest1(col2) values (1);
        INSERT INTO psptest1(col2) values (@a);
        SET @a += 1;
    END
    COMMIT TRANSACTION
    CREATE INDEX i1 on psptest1(col2);
    GO

    CREATE PROCEDURE psp1 (@param1 int)
    AS
    BEGIN
        INSERT INTO t1 SELECT * FROM psptest1
        WHERE col2 = @param1
        ORDER BY col2;
    END
    GO

    CREATE PROCEDURE psp2 (@param2 int)
    AS
    BEGIN
        INSERT INTO t1 SELECT * FROM psptest1 WHERE col2 = @param2
        ORDER BY col2
        OPTION (OPTIMIZE FOR (@param2 UNKNOWN))
    END
    GO

    CREATE TABLE t1 (col1 int primary key, col2 int, col3 binary(200));
    GO

o código de instalação Olá cria uma tabela que tenha sido desviada para distribuição de dados. difere do plano de consulta ideal do Hello com base no qual o parâmetro é selecionado. Infelizmente, o comportamento do cache de plano de saudação sempre não recompila a consulta de saudação com base no valor de parâmetro mais comum de saudação. Portanto, é possível que um toobe planos em cache e usado para vários valores, mesmo quando um plano diferente pode ser uma melhor opção de plano em média. Plano de consulta Olá cria dois procedimentos armazenados que são idênticos, exceto que um tem uma dica de consulta especiais.

**Exemplo, parte 1**

    -- Prime Procedure Cache with scan plan
    EXEC psp1 @param1=1;
    TRUNCATE TABLE t1;

    -- Iterate multiple times tooshow hello performance difference
    DECLARE @i int = 0;
    WHILE @i < 1000
    BEGIN
        EXEC psp1 @param1=2;
        TRUNCATE TABLE t1;
        SET @i += 1;
    END

**Exemplo, parte 2**

(É recomendável que você aguarde pelo menos 10 minutos antes de começar a parte 2 do exemplo hello, para que os resultados de saudação são distintos Olá resultante de dados de telemetria).

    EXEC psp2 @param2=1;
    TRUNCATE TABLE t1;

    DECLARE @i int = 0;
    WHILE @i < 1000
    BEGIN
        EXEC psp2 @param2=2;
        TRUNCATE TABLE t1;
        SET @i += 1;
    END

Cada parte desse exemplo tenta toorun uma instrução insert com parâmetros 1.000 vezes (toogenerate um toouse carga suficiente como um conjunto de dados de teste). Quando ele executa procedimentos armazenados, processador de consultas Olá examina o valor do parâmetro hello transmitido toohello procedimento durante a primeira compilação ("detecção de parâmetro"). processador Olá armazena em cache o plano resultante hello e usará para invocações posteriores, mesmo se o valor do parâmetro hello é diferente. o plano ideal Olá não pode ser usado em todos os casos. Às vezes você precisa tooguide Olá otimizador toopick um plano que é melhor para o caso comum de saudação em vez de caso específico Olá de quando a consulta Olá foi compilada pela primeira vez. Neste exemplo, o plano inicial hello gera um plano de "verificação" que lê toofind de todas as linhas de cada valor que corresponda ao parâmetro hello:

![Ajuste de consulta usando um plano de verificação](./media/sql-database-performance-guidance/query_tuning_1.png)

Como executamos o procedimento Olá Olá valor 1, o plano resultante Olá foi ideal para o valor de saudação 1, mas foi abaixo do ideal para todos os outros valores na tabela de saudação. resultado de saudação provavelmente não é o que você gostaria se foram toopick cada plano aleatoriamente, porque o plano de hello mais lento e usa mais recursos.

Se você executar o teste de saudação com `SET STATISTICS IO` definido muito`ON`, trabalho de verificação lógica Olá neste exemplo é feito em segundo plano da saudação. Você pode ver que há 1.148 leituras feitas pelo plano de saudação (que será ineficaz se caso médio Olá é tooreturn apenas uma linha):

![Ajuste de consulta usando uma verificação lógica](./media/sql-database-performance-guidance/query_tuning_2.png)

a segunda parte saudação do exemplo hello usa um toouse de otimizador Olá um valor específico do tootell de dica de consulta durante o processo de compilação de saudação. Nesse caso, ele força Olá processador tooignore Olá valor de consulta que é passado como parâmetro hello, e, em vez disso, tooassume `UNKNOWN`. Isso se refere a valor tooa com frequência média Olá na tabela de saudação (ignorando a distorção). plano de saudação resultante é um plano de busca que é mais rápida e usa menos recursos, em média, que o plano de saudação na parte 1 deste exemplo:

![Ajuste de consulta usando uma dica de consulta](./media/sql-database-performance-guidance/query_tuning_3.png)

Você pode ver o efeito Olá Olá **sys. resource_stats** tabela (há um atraso de tempo de saudação que você executar o teste de saudação e quando dados saudação preenchem a tabela de saudação). Para este exemplo, parte 1 executado durante a janela de tempo 22:25:00 hello e parte 2 executada às 22:35:00. Olá janela de tempo utilizou mais recursos nessa janela de tempo de Olá um posterior (devido a melhorias na eficiência do plano).

    SELECT TOP 1000 *
    FROM sys.resource_stats
    WHERE database_name = 'resource1'
    ORDER BY start_time DESC

![Exemplos de resultados de ajustes de consulta](./media/sql-database-performance-guidance/query_tuning_4.png)

> [!NOTE]
> Embora o volume de saudação neste exemplo é intencionalmente pequeno, o efeito de saudação dos parâmetros de qualidade inferior pode ser significativo, especialmente em bancos de dados maiores. diferença de Hello, em casos extremos, pode ser entre segundos para os casos rápidos e horas para casos lenta.
> 
> 

Você pode examinar **sys. resource_stats** toodetermine se o recurso de saudação para um teste usa mais ou menos recursos que outro teste. Ao comparar dados, separe tempo Olá de testes para que eles não sejam Olá mesma janela de 5 minutos no hello **sys. resource_stats** exibição. Olá meta do exercício Olá é toominimize Olá total de recursos usados e não toominimize recursos de pico de saudação. Em geral, a otimização de uma parte do código de latência também reduz o consumo de recursos. Certifique-se de que são necessárias alterações de saudação tornar o aplicativo tooan e que alterações Olá não afetarão negativamente a experiência do cliente Olá para alguém que possa estar usando dicas de consulta no aplicativo hello.

Se uma carga de trabalho tem um conjunto de repetir consultas, geralmente ela faz sentido toocapture e validar ideais Olá das suas escolhas de plano porque orienta Olá mínima de recursos tamanho unidade necessária toohost Olá banco de dados. Depois de validar, ocasionalmente reexaminar planos Olá que toohelp você certifique-se de que eles não tiveram degradação. Saiba mais sobre [dicas de consulta (Transact-SQL)](https://msdn.microsoft.com/library/ms181714.aspx).

### <a name="cross-database-sharding"></a>Fragmentação entre bancos de dados
Como o banco de dados do SQL Azure é executado em hardware de mercadoria, limites de capacidade de saudação para um único banco de dados são menores do que para uma instalação do SQL Server local tradicional. Alguns clientes usam operações de banco de dados de toospread de técnicas de fragmentação em vários bancos de dados quando operações de saudação não se ajustam Olá limites de um único banco de dados no banco de dados do SQL Azure. A maioria dos clientes que usam técnicas de fragmentação no Banco de Dados SQL do Azure divide seus dados em uma única dimensão entre vários bancos de dados. Para esta abordagem, você precisa toounderstand que os aplicativos OLTP executam frequentemente transações que se aplicam a tooonly uma linha ou tooa pequeno grupo de linhas no esquema de saudação.

> [!NOTE]
> Agora, o banco de dados SQL fornece tooassist uma biblioteca com a fragmentação. Para saber mais, confira [Visão geral da biblioteca de cliente de Banco de Dados Elástico](sql-database-elastic-database-client-library.md).
> 
> 

Por exemplo, se um banco de dados tem o nome do cliente, pedido e detalhes do pedido (como Olá exemplo tradicional Northwind banco de dados é fornecido com o SQL Server), você pode dividir dados em vários bancos de dados com o agrupamento de um cliente com hello relacionadas a ordem e os detalhes do pedido informações. Você pode garantir que os dados do cliente Olá permanecem em um único banco de dados. aplicativo Hello dividiria clientes diferentes nos bancos de dados, distribuindo efetivamente Olá carga em vários bancos de dados. Com a fragmentação, clientes não só podem evitar o limite de tamanho máximo do banco de dados de saudação, mas o banco de dados SQL também pode processar cargas de trabalho que são significativamente maiores do que os limites de Olá Olá diferentes níveis de desempenho, desde que cada banco de dados individual se encaixa no seu DTU.

Embora a fragmentação de banco de dados não reduza a capacidade de recurso de agregação de Olá para uma solução, é altamente eficaz em dando suporte a soluções muito grandes que são distribuídas por vários bancos de dados. Cada banco de dados pode executar em um desempenho diferentes nível toosupport muito grande, bancos de dados "efetivos" com altos requisitos de recursos.

### <a name="functional-partitioning"></a>Particionamento funcional
Com frequência, os usuários do SQL Server combinam muitas funções um banco de dados individual. Por exemplo, se um aplicativo tiver o inventário de toomanage de lógica de uma loja, esse banco de dados pode ter lógica associada com o controle de inventário, ordens de compra, procedimentos armazenados e exibições indexadas ou materializadas que gerenciar relatórios do fim do mês. Essa técnica torna mais fácil tooadminister Olá banco de dados para operações como backup, mas também requer toosize Olá toohandle Olá pico de carga de hardware em todas as funções de um aplicativo.

Se você usar uma arquitetura de expansão no banco de dados do SQL Azure, é uma boa ideia toosplit diferentes funções de um aplicativo em bancos de dados diferentes. Usando essa técnica, cada aplicativo é dimensionado de forma independente. Como um aplicativo se torna mais ocupado (e Olá carga no aumento de banco de dados de saudação), o administrador de saudação pode escolher níveis de desempenho independente para cada função no aplicativo hello. No limite de hello, com essa arquitetura, um aplicativo pode ser maior do que um único computador de mercadoria pode tratar pois Olá carga seja distribuída em vários computadores.

### <a name="batch-queries"></a>Consultas em lote
Para aplicativos que acessam dados por meio de alto volume, frequentes, consultas ad hoc, uma quantidade significativa de tempo de resposta é gasto na comunicação de rede entre a camada de aplicativo hello e da camada de banco de dados do Azure SQL hello. Mesmo quando ambos Olá aplicativo e banco de dados SQL estão no hello mesmo data center, latência de rede Olá entre hello dois pode ser aumentado por um grande número de operações de acesso de dados. rede de saudação tooreduce round retira dados Olá operações de acesso, considere o uso de consultas ad hoc do hello de lote de tooeither do hello opção ou toocompile-los como procedimentos armazenados. Se você lote consultas ad hoc hello, você pode enviar várias consultas como um lote grande em uma única viagem de tooAzure banco de dados SQL. Se você compilar consultas ad hoc em um procedimento armazenado, você pode obter o mesmo resultado como se você os lotes de saudação. Usando um procedimento armazenado também oferece Olá benefício de aumentar as chances de saudação do cache de planos de consulta de saudação no banco de dados do SQL Azure, você pode usar o hello procedimento armazenado novamente.

Alguns aplicativos apresentam gravação intensa. Às vezes, você pode reduzir a carga de e/s total Olá em um banco de dados considerando como toobatch grava juntos. Frequentemente, isso é tão simples quanto usar transações explícitas em vez de transações de confirmação automática em procedimentos armazenados e lotes ad hoc. Para ver uma avaliação das diferentes técnicas que você pode usar, consulte [Técnicas de envio em lote para aplicativos do Banco de Dados SQL no Azure](https://msdn.microsoft.com/library/windowsazure/dn132615.aspx). Fazer experiências com seu próprio modelo carga de trabalho toofind Olá certo para envio em lote. Ser toounderstand-se de que um modelo pode ter um pouco garante a consistência transacional diferentes. Localizando a carga de trabalho certa do hello que minimiza o uso de recursos requer a localização Olá a combinação certa de consistência e desempenho vantagens e desvantagens.

### <a name="application-tier-caching"></a>Cache de camada de aplicativo
Alguns aplicativos de banco de dados têm cargas de trabalho de leitura pesada. Camadas de armazenamento em cache pode reduzir a carga de saudação no banco de dados de saudação e pode reduzir toosupport necessário nível de desempenho de saudação um banco de dados usando o banco de dados do SQL Azure. Com [Cache Redis do Azure](https://azure.microsoft.com/services/cache/), se você tiver uma carga de trabalho pesadas de leitura, você pode ler dados de saudação uma vez (ou talvez uma vez por máquina de camada de aplicativo, dependendo de como estiver configurado) e, em seguida, armazene esses dados fora do banco de dados SQL. Este é um modo tooreduce banco de dados de carga (CPU e e/s de leitura), mas não há um efeito sobre a consistência transacional, pois dados hello está sendo lidos no cache de saudação podem estar fora de sincronia com dados de saudação no banco de dados de saudação. Embora em muitos aplicativos algum nível de inconsistência seja aceitável, isso não vale para todas as cargas de trabalho. É necessário compreender totalmente todos os requisitos do aplicativo antes de implementar uma estratégia de cache da camada do aplicativo.

## <a name="next-steps"></a>Próximas etapas
* Para obter mais informações sobre as camadas de serviço, consulte [Opções e desempenho de Banco de Dados SQL](sql-database-service-tiers.md)
* Para saber mais sobre pools elásticos, consulte [O que é um pool elástico do Azure?](sql-database-elastic-pool.md)
* Para obter informações sobre como criar pools Elásticos e desempenho, consulte [quando tooconsider um pool Elástico](sql-database-elastic-pool-guidance.md)

