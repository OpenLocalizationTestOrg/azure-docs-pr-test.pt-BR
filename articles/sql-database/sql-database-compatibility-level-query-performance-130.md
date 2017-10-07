---
title: "nível de compatibilidade 130 - banco de dados SQL do aaaDatabase | Microsoft Docs"
description: "Neste artigo, vamos explore Olá benefícios da execução do seu banco de dados do SQL Azure no nível de compatibilidade 130 e aproveitar os benefícios de Olá Olá novo Otimizador de consulta e recursos do processador de consulta. Podemos também abordam Olá possíveis efeitos colaterais no desempenho da consulta Olá para aplicativos de SQL existentes hello."
services: sql-database
documentationcenter: 
author: alainlissoir
manager: jhubbard
editor: 
ms.assetid: 8619f90b-7516-46dc-9885-98429add0053
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.devlang: NA
ms.tgt_pltfrm: NA
ms.topic: article
ms.date: 08/08/2016
ms.author: alainl
ms.openlocfilehash: 25693c5f7b01405b7073fa7d4cc2833fbe125e2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="improved-query-performance-with-compatibility-level-130-in-azure-sql-database"></a>Desempenho aprimorado de consultas com nível de compatibilidade 130 no Banco de Dados SQL do Azure
Banco de dados SQL do Azure está executando transparentemente centenas de milhares de bancos de dados em vários níveis de compatibilidade diferentes, preservando e garantindo a versão correspondente do hello compatibilidade com versões anteriores toohello do Microsoft SQL Server para todos os seus clientes!

Neste artigo, vamos explore Olá benefícios da execução do seu banco de dados do SQL Azure no nível de compatibilidade 130 e aproveitar os benefícios de Olá Olá novo Otimizador de consulta e recursos do processador de consulta. Podemos também abordam Olá possíveis efeitos colaterais no desempenho da consulta Olá para aplicativos de SQL existentes hello.

Como um lembrete de histórico, alinhamento de saudação de níveis de compatibilidade com versões SQL toodefault são:

* 100: no SQL Server 2008 e no Banco de Dados SQL do Azure V11.
* 110: no SQL Server 2012 e no Banco de Dados SQL do Azure V11.
* 120: no SQL Server 2014 e no Banco de Dados SQL do Azure V12.
* 130: no SQL Server 2016 e no Banco de Dados SQL do Azure V12.

> [!IMPORTANT]
> A partir do **meados de junho de 2016**, no banco de dados SQL Azure, o nível de compatibilidade padrão Olá será 130 em vez de 120 para **recém-criado** bancos de dados.
> 
> Bancos de dados criados antes de meados de junho de 2016 *não* serão afetados e manterão seu nível de compatibilidade atual (100, 110 ou 120). Bancos de dados migrados de banco de dados SQL versão V11 tooV12 terá um nível de compatibilidade de 100 ou 110. 
> 

## <a name="about-compatibility-level-130"></a>Sobre o nível de compatibilidade 130
Primeiro, se você quiser tooknow Olá atual nível de compatibilidade do banco de dados, execute Olá instrução Transact-SQL a seguir.

```
SELECT compatibility_level
    FROM sys.databases
    WHERE name = '<YOUR DATABASE_NAME>’;
```


Antes desta alteração toolevel 130 ocorre para **recentemente** criar bancos de dados, vamos examinar o que essa alteração está relacionado a alguns exemplos de consulta muito básica e ver como qualquer pessoa pode se beneficiar dela.

Processamento de consultas em bancos de dados relacionais pode ser muito complexo e pode levar toolots computador ciência e matemática toounderstand Olá inerente escolhas de design e comportamentos. Neste documento, conteúdo de saudação foi tooensure intencionalmente simplificado que qualquer pessoa com algumas técnicas básicas mínimo pode entender o impacto de saudação de alteração do nível de compatibilidade hello e determinar como ele pode se beneficiar de aplicativos.

Vamos dar uma olhada rápida o nível de compatibilidade 130 Olá coloca na tabela de saudação.  Você pode encontrar mais detalhes em [ALTERAR o nível de compatibilidade do BANCO DE DADOS (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), mas aqui está um breve resumo:

* Hello operação de inserção de uma instrução Insert select pode ser multithread ou pode ter um plano paralelo, embora antes dessa operação era single-threaded.
* Tabela com Otimização de Memória e consultas de variáveis de tabela agora podem ter planos paralelos, enquanto antes essa operação também era de single-thread.
* As estatísticas de tabela com Otimização de Memória agora podem ser utilizadas e são atualizadas automaticamente. Consulte [O que há de novo no mecanismo de banco de dados: OLTP na memória](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) para obter mais detalhes.
* Modo de lote vs. Modo de Linha muda com índices de Repositório de Coluna
  * As classificações em uma tabela com um índice de Repositório de Coluna agora estão em modo de lote.
  * As agregações em janela agora operam em modo de lote como instruções TSQL LAG/LEAD.
  * Consultas em tabelas de Repositório de Coluna com Múltiplas cláusulas distintas operam em modo de Lote.
  * Consultas em execução com DOP = 1 ou um plano serial também são executadas em Modo de Lote.
* Por último, melhorias de estimativa de cardinalidade realmente são provenientes com nível de compatibilidade 120, mas para aqueles em execução em uma compatibilidade mais baixo nível (ou seja, 100 ou 110), hello mover toocompatibility nível 130 também fará com que esses melhorias e eles também podem tirar proveito do desempenho de consulta de saudação de seus aplicativos.

## <a name="practicing-compatibility-level-130"></a>Praticando o nível de compatibilidade 130
Primeiro, vamos algumas tabelas, índices e dados aleatórios criados toopractice alguns desses recursos. exemplos de script TSQL Olá podem ser executados no SQL Server 2016 ou no banco de dados do SQL Azure. No entanto, ao criar um banco de dados do SQL Azure, certifique-se de escolher por Olá mínimo um P2 de banco de dados porque você precisa de pelo menos dois núcleos tooallow multithreading e, portanto, aproveitar esses recursos.

```
-- Create a Premium P2 Database in Azure SQL Database

CREATE DATABASE MyTestDB
    (EDITION=’Premium’, SERVICE_OBJECTIVE=’P2′);
GO

-- Create 2 tables with a column store index on
-- hello second one (only available on Premium databases)

CREATE TABLE T_source
    (Color varchar(10), c1 bigint, c2 bigint);

CREATE TABLE T_target
    (c1 bigint, c2 bigint);

CREATE CLUSTERED COLUMNSTORE INDEX CCI ON T_target;
GO

-- Insert few rows.

INSERT T_source VALUES
    (‘Blue’, RAND() * 100000, RAND() * 100000),
    (‘Yellow’, RAND() * 100000, RAND() * 100000),
    (‘Red’, RAND() * 100000, RAND() * 100000),
    (‘Green’, RAND() * 100000, RAND() * 100000),
    (‘Black’, RAND() * 100000, RAND() * 100000);

GO 200

INSERT T_source SELECT * FROM T_source;

GO 10
```


Agora, vamos dar uma toosome aparência dos recursos de processamento de consulta Olá vêm com o nível de compatibilidade 130.

## <a name="parallel-insert"></a>INSERT paralela
Executar instruções de TSQL Olá abaixo executa Olá operação de inserção no nível de compatibilidade 120 e 130, que executa respectivamente Olá operação de inserção em um único modelo de thread (120) e em um modelo multi-threaded (130).

```
-- Parallel INSERT … SELECT … in heap or CCI
-- is available under 130 only

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO 

-- hello INSERT part is in serial

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130
GO

-- hello INSERT part is in parallel

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

SET STATISTICS XML OFF;
```


Solicitando o plano de consulta real Olá Olá, examinando sua representação gráfica ou seu conteúdo XML, você pode determinar quais estimativa de cardinalidade função está em execução. Analisar planos de saudação lado a lado na Figura 1, podem ver claramente que Olá execução de inserção de repositório de coluna for de serial em 120 tooparallel em 130. Observe também, essa alteração de saudação do ícone de iterador Olá no plano de 130 Olá mostrando duas setas paralelas, ilustrar o fato de Olá Olá agora a execução do iterador é realmente paralela. Se você tiver grande toocomplete de operações de inserção, execução paralela hello, número toohello vinculado do núcleo que à sua disposição para banco de dados Olá, terão um desempenho melhor; Dependendo da sua situação backup tooa 100 vezes mais rápido!

*Figura 1: Inserir alterações de operação de tooparallel serial com nível de compatibilidade 130.*

![A figura 1](./media/sql-database-compatibility-level-query-performance-130/figure-1.jpg)

## <a name="serial-batch-mode"></a>Modo de lote SERIAL
Da mesma forma, mover toocompatibility nível 130 durante o processamento de linhas de dados permite o processamento de modo de lote. Primeiro, operações no modo de lote só estão disponíveis quando você tem um índice de repositório de coluna em vigor. Em segundo lugar, um lote normalmente representa aproximadamente 900 linhas e usa uma lógica de código otimizada para CPU com vários núcleos, a maior taxa de transferência de memória e diretamente aproveita Olá dados compactados de saudação repositório de coluna sempre que possível. Sob essas condições, SQL Server 2016 pode processar aproximadamente 900 linhas ao mesmo tempo, em vez de 1 linha no tempo de saudação, e como consequência, hello custo geral da operação de saudação agora compartilhado por lote inteiro de hello, reduzindo o custo por linha hello geral. Essa quantidade compartilhada de operações combinada com a compactação do repositório de coluna Olá basicamente reduz a latência de saudação envolvida em uma operação de modo de seleção de lote. Você pode encontrar mais detalhes sobre o repositório de coluna hello e lotes de modo a [guia de índices Columnstore](https://msdn.microsoft.com/library/gg492088.aspx).

```
-- Serial batch mode execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT (C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO 

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


Como visível abaixo, observando Olá consulta planos-lado a lado na Figura 2, podemos ver que o modo de processamento Olá foi alterado com o nível de compatibilidade de saudação e como consequência, ao executar consultas de saudação em ambos os nível de compatibilidade completamente, podemos ver que a maioria do tempo de processamento de saudação é gasto em linha em comparação com o modo (86%) toohello modo de lote (% 14), onde 2 lotes foram processadas. Aumentar conjunto de dados hello, hello benefício aumentam.

*Figura 2: Selecione as alterações de operação de modo serial toobatch com nível de compatibilidade 130.*

![Figura 2](./media/sql-database-compatibility-level-query-performance-130/figure-2.jpg)

## <a name="batch-mode-on-sort-execution"></a>Modo em lotes em Execução de Classificação
Semelhante toohello acima, mas a operação de classificação tooa aplicada, a transição de saudação do (nível de compatibilidade 120) toobatch modo linha (nível de compatibilidade 130) aprimora o desempenho Olá Olá a operação de classificação para Olá mesmos motivos.

```
-- Batch mode on sort execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


Visível-lado a lado na Figura 3, podemos ver que a operação de classificação Olá no modo de linha representa 81% de saudação de custo, enquanto o modo de lote Olá representa apenas 19% do custo da saudação (respectivamente 81% e % de 56 na classificação de saudação em si).

*Figura 3: Operação de classificação é alterado de modo de toobatch de linha com o nível de compatibilidade 130.*

![A figura 3](./media/sql-database-compatibility-level-query-performance-130/figure-3.png)

Obviamente, esses exemplos só contêm dezenas de milhares de linhas, que é nada ao analisar dados de saudação disponíveis na maioria dos SQL Servers hoje em dia. Apenas projeto esses executada em milhões de linhas em vez disso, e isso pode se transformar em alguns minutos de execução dispensados diariamente pendentes natureza Olá da carga de trabalho.

## <a name="cardinality-estimation-ce-improvements"></a>Aprimoramentos de CE (Estimativa de Cardinalidade)
Introduzido com o SQL Server 2014, qualquer banco de dados em execução em um nível de compatibilidade 120 ou acima fará com que usa Olá nova funcionalidade de estimativa de cardinalidade. Essencialmente, a estimativa de cardinalidade é lógica Olá usado toodetermine como o SQL server executará uma consulta com base em seu custo estimado. estimativa de saudação é calculada com a entrada de estatísticas associadas a objetos envolvidos na consulta. Praticamente, em um nível alto, as funções de estimativa de cardinalidade são estimativas de contagem de linha juntamente com informações sobre distribuição de saudação de valores hello, contagens de valores distintos e contagens duplicadas contido no hello tabelas e objetos referenciados na consulta de saudação. Obtendo essas estimativas errado, pode levar a e/s de disco toounnecessary devido tooinsufficient concessões de memória (ou seja, o TempDB derramamentos) ou tooa seleção de um plano serial em paralelo plano de execução, tooname alguns. Conclusão, estimativas incorretas podem levar tooan degradação do desempenho geral Olá da execução da consulta. Em Olá outro lado, melhores estimativas, mais estimativas precisas, clientes potenciais toobetter as execuções de consulta!

Como mencionado anteriormente, otimizações de consulta e as previsões são um assunto complexo, mas toolearn mais informações sobre planos de consulta e o avaliador de cardinalidade, você pode consultar documentos toohello em [otimizar seus planos de consulta com hello SQL Server 2014 Avaliador de cardinalidade](https://msdn.microsoft.com/library/dn673537.aspx) para aprofundar.

## <a name="which-cardinality-estimation-do-you-currently-use"></a>Que Estimativa de Cardinalidade você usa atualmente?
toodetermine sob qual estimativa de cardinalidade executam suas consultas, vamos usar apenas a consulta de saudação exemplos abaixo. Observe que este primeiro exemplo será executado com nível de compatibilidade 110, indicando o uso de saudação de funções de estimativa de cardinalidade antigos hello.

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 110;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


Após a conclusão da execução, clique no link XML hello e examinar propriedades de saudação do iterador primeiro hello, conforme mostrado abaixo. Observe o nome da propriedade Olá chamado CardinalityEstimationModelVersion definido no momento em 70. Isso não significa que nível de compatibilidade do banco de dados de saudação é definido a versão do SQL Server 7.0 toohello (definido em 110 como visível em instruções de TSQL Olá acima), mas valor Olá 70 simplesmente representa Olá herdada estimativa de cardinalidade funcionalidade disponível desde o SQL Servidor 7.0, que não tinha nenhum revisões principais até que o SQL Server 2014 (que vem com um nível de compatibilidade 120).

*Figura 4: Olá CardinalityEstimationModelVersion é definido too70 ao usar um nível de compatibilidade de 110 ou abaixo.*

![Figura 4](./media/sql-database-compatibility-level-query-performance-130/figure-4.png)

Como alternativa, você pode alterar too130 de nível de compatibilidade de saudação e desabilitar o uso de saudação da nova função de estimativa de cardinalidade hello usando Olá LEGACY_CARDINALITY_ESTIMATION definir tooON com [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx). Isso será ser exatamente Olá mesmo que usar 110 de estimativa de cardinalidade função de uma perspectiva, ao usar o nível de compatibilidade de processamento de consulta mais recente hello. Dessa forma, que você pode se beneficiar de nova consulta de saudação vêm com o nível de compatibilidade mais recente hello (ou seja, o modo de lote) de recursos de processamento, mas ainda dependem de funcionalidade de estimativa de cardinalidade antiga Olá se necessário.

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


Simplesmente mover toohello nível de compatibilidade 120 ou 130 habilita a funcionalidade de estimativa de cardinalidade novo hello. Nesse caso, Olá padrão CardinalityEstimationModelVersion será definido adequadamente too120 ou 130 como visível abaixo.

```
-- New CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


*Figura 5: Olá CardinalityEstimationModelVersion é definido too130 ao usar um nível de compatibilidade 130.*

![Figura 5](./media/sql-database-compatibility-level-query-performance-130/figure-5.jpg)

## <a name="witnessing-hello-cardinality-estimation-differences"></a>Diferenças de estimativa de cardinalidade Olá testemunhando
Agora, vamos executar um pouco mais complexo que envolvem uma INNER JOIN com uma cláusula WHERE com alguns predicados de consulta e vamos dar uma olhada na estimativa de contagem de linha de saudação da função de estimativa de cardinalidade antiga hello primeiro.

```
-- Old CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


A execução desta consulta efetivamente retorna 200,704 linhas, enquanto Olá estimativa de linha com a funcionalidade de estimativa de cardinalidade antiga Olá declarações 194,284 linhas. Obviamente, como já dissemos, esses resultados de contagem de linha também dependerá quantas vezes você executou Olá exemplos anteriores, que preenche as tabelas de exemplo hello repetidamente em cada execução. Obviamente, predicados de saudação em sua consulta também terá uma influência na estimativa de real Olá além de forma de tabela hello, conteúdo de dados e como esses dados realmente correlacionam entre si.

*Figura 6: estimativa de contagem de linha de saudação é 194,284 ou 6.000 linhas fora de linhas de 200,704 Olá esperadas.*

![Figura 6](./media/sql-database-compatibility-level-query-performance-130/figure-6.jpg)

Em Olá mesma forma, vamos executar agora Olá mesma consulta com a nova funcionalidade de estimativa de cardinalidade hello.

```
-- New CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


Observando Olá abaixo, agora vemos que estimativa de linha de saudação é 202,877, ou muito mais próximo e maior do que o hello estimativa de cardinalidade antigo.

*Figura 7: estimativa de contagem de linha hello agora é 202,877, em vez de 194,284.*

![Figura 7](./media/sql-database-compatibility-level-query-performance-130/figure-7.jpg)

Na realidade, o conjunto de resultados de saudação é 200,704 linhas (mas tudo depende de quantas vezes você tiver executado consultas Olá Olá exemplos anteriores, mas é mais importante, como Olá TSQL usa a instrução de rand () do hello, Olá real valores retornados podem variar com toohello de execução de um lado). Portanto, nesse exemplo específico, hello nova estimativa de cardinalidade faz um trabalho melhor ao estimar o número de saudação de linhas porque 202,877 é muito mais perto too200, 704, que 194,284! Último, se você alterar Olá cláusula WHERE predicados tooequality (em vez de ">" para a instância), isso poderia fazer estimativas de saudação entre hello antiga e nova função de cardinalidade ainda mais diferentes, dependendo de quantas correspondências, você pode obter.

Obviamente, nesse caso, estar ~6000 aquém da contagem real não representa muitos dados em algumas situações. Agora, transpor essa toomillions de linhas em várias tabelas e consultas mais complexas e estimativa de saudação às vezes pode ficar inativo por milhões de linhas e hello, portanto, o risco de separação-up Olá incorreto de plano de execução, ou solicitar memória insuficiente concede à esquerda derramamentos tooTempDB e assim por mais de e/s, são muito maior.

Se você tem a oportunidade de hello, práticas essa comparação com suas consultas mais comuns e os conjuntos de dados e ver por conta própria em quanto algumas das estimativas de saudação antiga e nova são afetadas, enquanto alguns podem acabou de se tornar mais fora da realidade hello, ou alguns outros simplesmente as contagens de linhas de real toohello mais próxima, na verdade, retornadas em conjuntos de resultados de saudação. Tudo depende da forma de saudação de consultas, características de banco de dados do SQL Azure hello, natureza hello e tamanho de saudação de conjuntos de dados e estatísticas de saudação disponíveis sobre eles. Se você acabou de criar sua instância de banco de dados SQL, a consulta de saudação otimizador terá toobuild seu conhecimento do zero, em vez de estatísticas reutilizando feitas da consulta anterior Olá será executado. Portanto, Olá estimativas são situação tooevery muito contextuais e quase específico de servidores e aplicativos. Ele é tookeep um aspecto importante em mente!

## <a name="some-considerations-tootake-into-account"></a>Tootake algumas considerações para a conta
Embora a maioria das cargas de trabalho pode se beneficiar do nível de compatibilidade 130, Olá antes de adoção de nível de compatibilidade de saudação para seu ambiente de produção, você basicamente tem 3 opções:

1. Mover toocompatibility nível 130 e veja como fazer as coisas. No caso de você observar algumas regressões, simplesmente definir tooits back nível de compatibilidade Olá nível original, ou manter 130 e reverter somente modo herdado do hello estimativa de cardinalidade toohello back (conforme explicado acima, isso sozinho pode solucionar problema de saudação).
2. Testar seus aplicativos existentes em semelhante à carga de produção, ajustar e validar o desempenho de saudação antes tooproduction contínuo. No caso de problemas, mesmo que acima, você pode sempre voltar toohello nível de compatibilidade original ou simplesmente reverter modo herdado do toohello back Olá estimativa de cardinalidade.
3. Como uma opção final e hello tooaddress de maneira mais recente essas perguntas, é o repositório de consultas Olá tooleverage. Essa é a opção recomendada de hoje! análise de saudação tooassist de suas consultas sob compatibilidade nível 120 ou abaixo versus 130, não recomendamos que você suficiente toouse repositório de consultas. Repositório de consultas está disponível com a versão mais recente de saudação do Azure SQL Database V12 e foi projetada toohelp é uma solução de problemas de desempenho de consulta. Pense Olá repositório de consultas como um gravador de dados de voo para seu banco de dados coletar e apresentar informações históricas sobre todas as consultas. Isso bastante simplifica a análise forense de desempenho, reduzindo Olá tempo toodiagnose e resolver problemas. Você pode encontrar mais informações no artigo sobre [Repositório de Consultas: o gravador de dados de voo para o banco de dados](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).

Em alto nível, se você já tiver um conjunto de bancos de dados em execução no nível de compatibilidade 120 ou abaixo e planejar toomove de saudação algumas delas too130, ou porque sua carga de trabalho provisionar novos bancos de dados que serão automaticamente assim ser definido por padrão too130, considere seguinte Hello:

* Antes de alterar o novo nível de compatibilidade toohello em produção, habilite o repositório de consultas. Você pode consultar muito[alterar o repositório de consultas de saudação de modo de compatibilidade do banco de dados e o uso de saudação](https://msdn.microsoft.com/library/bb895281.aspx) para obter mais informações.
* Em seguida, teste críticas todas as cargas de trabalho usando dados representativos e as consultas de um ambiente de produção e compare o desempenho Olá apresentou e como relatado pelo repositório de consultas. Se você tiver algum regressões, você pode identificar Olá consultas retornadas por hello repositório de consultas e usar a opção de armazenamento de consulta para forçar o plano hello (também conhecido como plano de fixação). Nesse caso, você definitivamente permanecer com o nível de compatibilidade de saudação 130 e usar plano de consulta anterior hello como sugerido pelo Olá repositório de consultas.
* Se você quiser tooleverage novos recursos e funcionalidades do banco de dados do SQL Azure (que está executando o SQL Server 2016), mas é confidenciais toochanges trazido pelo nível de compatibilidade 130, Olá como um último recurso, é possível considerar o forçar novamente o nível de compatibilidade Olá nível de toohello que atenda às suas cargas de trabalho usando a instrução ALTER DATABASE. Mas primeiro, lembre-se desse plano do repositório de consultas Olá fixação de opção é a melhor opção porque não usando 130 basicamente permanecer no nível de funcionalidade de saudação de uma versão mais antiga do SQL Server.
* Se você tiver aplicativos multilocatários, abrangendo vários bancos de dados, pode ser necessário tooupdate Olá provisionamento de lógica de seu bancos de dados de tooensure um nível de compatibilidade consistente em todos os bancos de dados; os antigos e provisionados recentemente. O desempenho da carga de trabalho de aplicativo poderia ser fatos toohello confidenciais que alguns bancos de dados estão em execução em níveis de compatibilidade diferentes, e portanto, a consistência de nível de compatibilidade em qualquer banco de dados poderão ser necessária na ordem tooprovide Olá mesmo experiência de clientes tooyour todo quadro hello. Observe que não é uma exigência, ela realmente depende de como seu aplicativo é afetado pelo nível de compatibilidade de saudação.
* Por fim, sobre Olá estimativa de cardinalidade e como alterar o nível de compatibilidade hello, antes de continuar na produção, é recomendável tootest sua carga de trabalho de produção em Olá novas condições toodetermine se beneficia do seu aplicativo melhorias de estimativa de cardinalidade Hello.

## <a name="conclusion"></a>Conclusão
Usando o banco de dados do SQL Azure toobenefit de todos os aprimoramentos do SQL Server 2016 claramente pode melhorar as execuções de sua consulta. Exatamente como é! É claro que, como qualquer novo recurso, uma avaliação adequada deve ser feita condições exata do hello toodetermine sob a qual sua carga de trabalho do banco de dados opera Olá melhor. Experiência mostra que a maioria das cargas de trabalho esperada tooat menos executado de maneira transparente em nível de compatibilidade 130, aproveitando as novas funções e a nova estimativa de cardinalidade de processamento de consulta. Que diz, na verdade, sempre há algumas exceções e fazendo adequado devido auditoria é um toodetermine importante avaliação quanto você pode aproveitar esses aprimoramentos. E, novamente, o repositório de consultas de saudação podem ser de muito útil para fazer esse trabalho!

Como a evolução do SQL Azure, você pode esperar um nível de compatibilidade 140 em Olá futuras. No momento adequado, começaremos a falar sobre o que esse futuro nível de compatibilidade 140 trará, assim como brevemente discutimos aqui o que o nível de compatibilidade 130 está trazendo hoje.

Por enquanto, vamos não se esqueça de, a partir de junho de 2016, banco de dados do SQL Azure será alterado nível de compatibilidade padrão de saudação de 120 too130 para bancos de dados recém-criado. Lembre-se!

## <a name="references"></a>Referências
* [O que há de novo no mecanismo de banco de dados](https://msdn.microsoft.com/library/bb510411.aspx#InMemory)
* [Blog: Repositório de Consultas: um gravador de dados de voo para o banco de dados, por Borko Novakovic, de 8 de junho de 2016](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)
* [Nível de compatibilidade ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx)
* [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx)
* [Nível de compatibilidade 130 para Banco de Dados SQL do Azure V12](https://azure.microsoft.com/updates/compatibility-level-130-for-azure-sql-database-v12/)
* [Otimizando a seus planos de consulta com hello avaliador de cardinalidade do SQL Server 2014](https://msdn.microsoft.com/library/dn673537.aspx)
* [Guia de índices ColumnStore](https://msdn.microsoft.com/library/gg492088.aspx)
* [Blog: Desempenho aprimorado de consultas com nível de compatibilidade 130 no Banco de Dados SQL do Azure, por Alain Lissoir, 6 de maio de 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/)

<!--
Improved Query Performance with Compatibility Level 130 in Azure SQL Database

May 6, 2016 by Alain Lissoir (AlainL), on GitHub 'alainlissoir'.

https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/

..... Now, above.
....................
..... Soon, below?

CAPS / MSDN ideally, but instead on ACom:
.. # Assess effects of latest compatibility level on query performance, how to

sql-database-compatibility-level-query-performance-130.md

genemi = MightyPen , 2016-05-20  Friday  17:00pm
-->
