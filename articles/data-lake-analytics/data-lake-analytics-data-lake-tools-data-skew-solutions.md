---
title: "aaaResolve problemas de distorção de dados usando o Azure Data Lake Tools para Visual Studio | Microsoft Docs"
description: "Solucione problemas em possíveis soluções para problemas de distorção de dados usando as Ferramentas do Azure Data Lake para Visual Studio."
services: data-lake-analytics
documentationcenter: 
author: yanancai
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/16/2016
ms.author: yanacai
ms.openlocfilehash: 3909fbd89eb40f061268cb7128f7fa84a3c33de7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-data-skew-problems-by-using-azure-data-lake-tools-for-visual-studio"></a>Resolver problemas de distorção de dados usando as Ferramentas do Azure Data Lake para Visual Studio

## <a name="what-is-data-skew"></a>O que é distorção de dados?

Resumidamente, distorção de dados é a super-representação de um valor. Imagine que você atribuiu 50 examiners de imposto tooaudit devoluções de imposto, um examinador para cada estado dos EUA. examiner do Wyoming Hello, porque há população de saudação é pequena, tem pouco toodo. Na Califórnia, no entanto, examiner Olá é mantida muito ocupado devido a população grande do estado de saudação.
    ![Exemplo de problema de distorção de dados](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)

Em nosso cenário, dados saudação é desigualdade distribuídos por todos os examiners de imposto, que significa que alguns examiners devem funcionar mais do que outras pessoas. Em seu trabalho, com frequência você enfrentar situações como exemplo de imposto examiner hello aqui. Em termos mais técnicos, um vértice obtém dados muito mais do que seus colegas, uma situação que faz com que o vértice Olá funcionar mais do que outros e que eventualmente reduz a velocidade de todo o trabalho de saudação. O que é pior, trabalho Olá pode falhar, pois vértices podem ter, por exemplo, uma limitação de 5 horas de tempo de execução e uma limitação de 6 GB de memória.

## <a name="resolving-data-skew-problems"></a>Resolvendo problemas de distorções de dados

As Ferramentas do Azure Data Lake para Visual Studio podem ajudar a detectar se o trabalho tem um problema de distorção de dados. Se houver algum problema, você pode resolvê-lo experimentando soluções Olá nesta seção.

## <a name="solution-1-improve-table-partitioning"></a>Solução 1: melhorar o particionamento da tabela

### <a name="option-1-filter-hello-skewed-key-value-in-advance"></a>Opção 1: Olá filtro inclinada valor de chave com antecedência

Se ele não afeta sua lógica de negócios, você pode filtrar os valores de alta frequência Olá antecipadamente. Por exemplo, se houver muita 000-000 000 na coluna GUID, não convém tooaggregate esse valor. Antes de agregação, você pode escrever "GUID onde! ="000-000 000"" valor de alta frequência Olá toofilter.

### <a name="option-2-pick-a-different-partition-or-distribution-key"></a>Opção 2: separar uma chave de partição ou distribuição diferente

Olá anterior como exemplo, se quiser que as cargas de trabalho de auditoria de imposto de Olá toocheck somente todos sobre Olá país, você pode melhorar a distribuição de dados Olá selecionando o número de identificação de saudação como sua chave. Escolher uma partição diferente ou a chave de distribuição pode, às vezes, distribuir dados hello mais uniformemente, mas você precisa toomake-se de que essa opção não afeta sua lógica de negócios. Por exemplo, toocalculate soma de imposto de saudação para cada estado, talvez você queira toodesignate _estado_ como chave de partição hello. Se você continuar tooexperience esse problema, tente usar a opção 3.

### <a name="option-3-add-more-partition-or-distribution-keys"></a>Opção 3: adicionar mais chaves de partição ou distribuição

Em vez de usar apenas _Estado_ como uma chave de partição, você pode usar mais de uma chave para o particionamento. Por exemplo, considere adicionar _CEP_ como uma partição adicional partição de dados de chave tooreduce tamanhos e distribuir dados hello mais uniformemente.

### <a name="option-4-use-round-robin-distribution"></a>Opção 4: usar a distribuição round robin

Se você não encontrar uma chave adequada para a partição e a distribuição, você pode tentar toouse distribuição de round-robin. A distribuição round robin trata cada linha igualmente e as coloca aleatoriamente nos buckets correspondentes. dados de saudação obtém distribuídos uniformemente, mas ele perde informações de localidade, uma desvantagem que também pode reduzir o desempenho do trabalho para algumas operações. Além disso, se você estiver fazendo a agregação para a chave distorcidos Olá mesmo assim, o problema de distorção de dados de saudação persistirá. toolearn mais sobre a distribuição de round robin, consulte Olá U-SQL tabela distribuições seção [criar tabela (U-SQL): Criando uma tabela com esquema](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch).

## <a name="solution-2-improve-hello-query-plan"></a>Solução 2: Melhorar o plano de consulta Olá

### <a name="option-1-use-hello-create-statistics-statement"></a>Opção 1: Usar a instrução de CREATE STATISTICS Olá

U-SQL fornece a instrução CREATE STATISTICS de saudação em tabelas. Esta instrução oferece mais toohello Otimizador de consulta de informações sobre Olá características de dados, como distribuição de valor, que são armazenados em uma tabela. Para a maioria das consultas, o otimizador de consulta de saudação já gera as estatísticas necessárias para um plano de consulta de alta qualidade hello. Ocasionalmente, talvez seja necessário tooimprove desempenho de consulta criando estatísticas adicionais com CREATE STATISTICS ou modificar o design da consulta hello. Para obter mais informações, consulte Olá [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) página.

Exemplo de código:

    CREATE STATISTICS IF NOT EXISTS stats_SampleTable_date ON SampleDB.dbo.SampleTable(date) WITH FULLSCAN;

>[!NOTE]
>Informações de estatísticas não são atualizadas automaticamente. Se você atualizar os dados de saudação em uma tabela sem recriar estatísticas hello, desempenho de consulta Olá pode recusar.

### <a name="option-2-use-skewfactor"></a>Opção 2: Usar SKEWFACTOR

Se você quiser imposto de saudação toosum para cada estado, você deve usar GROUP BY estado, uma abordagem que não evita o problema de distorção de dados de saudação. No entanto, você pode fornecer uma dica de dados em seu tooidentify consulta dados distorcer chaves para que o otimizador Olá pode preparar um plano de execução para você.

Normalmente, você pode definir o parâmetro hello como 0,5 e 1, com o que significa não muito distorção de distorção e 1 significado pesada de 0,5. Como dica Olá afeta a otimização de plano de execução para a instrução atual hello e todas as instruções de downstream, ser dica de saudação tooadd se antes Olá potencial inclinada key-wise agregação.

    SKEWFACTOR (columns) = x

    Provides a hint that hello given columns have a skew factor x from 0 (no skew) through 1 (very heavy skew).

Exemplo de código:

    //Add a SKEWFACTOR hint.
    @Impressions =
        SELECT * FROM
        searchDM.SML.PageView(@start, @end) AS PageView
        OPTION(SKEWFACTOR(Query)=0.5)
        ;

    //Query 1 for key: Query, ClientId
    @Sessions =
        SELECT
            ClientId,
            Query,
            SUM(PageClicks) AS Clicks
        FROM
            @Impressions
        GROUP BY
            Query, ClientId
        ;

    //Query 2 for Key: Query
    @Display =
        SELECT * FROM @Sessions
            INNER JOIN @Campaigns
                ON @Sessions.Query == @Campaigns.Query
        ;   

### <a name="option-3-use-rowcount"></a>Opção 3: usar ROWCOUNT  
Além do tooSKEWFACTOR para inclinada-chave específica junção casos, se você souber que Olá outro conjunto de linhas unidas for pequeno, você pode informar o otimizador Olá adicionando uma dica de número de linhas na instrução de U-SQL Olá antes da junção. Dessa forma, otimizador pode escolher um toohelp de estratégia de junção difusão melhorar o desempenho. Lembre-se de que o número de linhas não resolve o problema de distorção de dados de saudação, mas possa oferecer ajuda adicional.

    OPTION(ROWCOUNT = n)

    Identify a small row set before JOIN by providing an estimated integer row count.

Exemplo de código:

    //Unstructured (24-hour daily log impressions)
    @Huge   = EXTRACT ClientId int, ...
                FROM @"wasb://ads@wcentralus/2015/10/30/{*}.nif"
                ;

    //Small subset (that is, ForgetMe opt out)
    @Small  = SELECT * FROM @Huge
                WHERE Bing.ForgetMe(x,y,z)
                OPTION(ROWCOUNT=500)
                ;

    //Result (not enough information toodetermine simple broadcast JOIN)
    @Remove = SELECT * FROM Bing.Sessions
                INNER JOIN @Small ON Sessions.Client == @Small.Client
                ;

## <a name="solution-3-improve-hello-user-defined-reducer-and-combiner"></a>Solução 3: Melhorar a combinação e Redutor definido pelo usuário de saudação

Às vezes, você pode escrever um toodeal de operador definido pelo usuário com a lógica do processo complicado e um redutor bem escrito e combinação podem reduzir um problema de distorção de dados em alguns casos.

### <a name="option-1-use-a-recursive-reducer-if-possible"></a>Opção 1: usar um redutor recursivo, se possível

Por padrão, um redutor definido pelo usuário será executado no modo não recursivo, o que significa que o trabalho de redução para uma chave será distribuído em um único vértice. Mas, se os dados forem precisos, Olá grandes conjuntos de dados podem ser processados em um único vértice e executados por um longo tempo.

tooimprove desempenho, você pode adicionar um atributo no seu toorun do código toodefine Redutor no modo recursivo. Em seguida, Olá grandes conjuntos de dados pode ser distribuída toomultiple vértices e executados em paralelo, o que acelera o seu trabalho.

toochange um toorecursive Redutor de não-recursivo, você precisa toomake-se de que o algoritmo de associação. Por exemplo, sum Olá é associativo e mediana Olá não é. Você também precisa toomake-se de que Olá de entrada e saída para Redutor lembre-Olá mesmo esquema.

Atributo do redutor recursivo:

    [SqlUserDefinedReducer(IsRecursive = true)]

Exemplo de código:

    [SqlUserDefinedReducer(IsRecursive = true)]
    public class TopNReducer : IReducer
    {
        public override IEnumerable<IRow>
            Reduce(IRowset input, IUpdatableRow output)
        {
            //Your reducer code goes here.
        }
    }

### <a name="option-2-use-row-level-combiner-mode-if-possible"></a>Opção 2: usar o modo combinador no nível de linha, se possível

Dica de número de linhas de toohello semelhante para casos de associação de chave inclinada específico, o modo de combinação tenta toodistribute grande valor de chave em horários diferentes conjuntos de toomultiple vértices para que o trabalho de saudação pode ser executado simultaneamente. O modo combinador não pode resolver problemas de distorção de dados, mas pode auxiliar em casos de grandes conjuntos de valores de chaves distorcidas.

Por padrão, o modo de combinação Olá está completo, o que significa que Olá deixado o conjunto de linhas e o conjunto correto de linhas não pode ser separado. Definindo o modo hello como interna/esquerda/direita permite que a junção de nível de linha. sistema de saudação separa os conjuntos de linhas correspondentes hello e distribui-los em vários vértices que são executados em paralelo. No entanto, antes de configurar o modo de combinação hello, tenha cuidado tooensure que Olá conjuntos de linhas correspondentes pode ser separado.

exemplo Hello a seguir mostra um conjunto de linha esquerda separados. Cada linha de saída depende de uma única linha de entrada da saudação esquerda, e potencialmente depende de todas as linhas de saudação à direita com hello mesmo valor de chave. Se você definir o modo de combinação hello como left, o sistema de saudação separa Olá enorme esquerda-conjunto de linhas em pequenas e atribui toomultiple vértices.

![Ilustração do modo combinador](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/combiner-mode-illustration.png)

>[!NOTE]
>Se você definir o modo de combinação incorreta Olá, combinação Olá é menos eficiente e resultados de saudação podem estar errados.

Atributos do modo de combinador:

- [SqlUserDefinedCombiner(Mode=CombinerMode.Full)]: Every output row potentially depends on all hello input rows from left and right with hello same key value.

- SqlUserDefinedCombiner(Mode=CombinerMode.Left): Depende de cada linha de saída em uma única linha de entrada da esquerda da saudação (e potencialmente todas as linhas a partir de saudação à direita com hello mesmo valor de chave).

- qlUserDefinedCombiner(Mode=CombinerMode.Right): cada linha de saída depende de uma única linha de entrada da saudação direito (e potencialmente todas as linhas da esquerda Olá com hello que mesmo valor de chave).

- SqlUserDefinedCombiner(Mode=CombinerMode.Inner): Cada linha de saída depende de uma única linha de entrada da saudação à esquerda e hello direita com hello mesmo valor.

Exemplo de código:

    [SqlUserDefinedCombiner(Mode = CombinerMode.Right)]
    public class WatsonDedupCombiner : ICombiner
    {
        public override IEnumerable<IRow>
            Combine(IRowset left, IRowset right, IUpdatableRow output)
        {
        //Your combiner code goes here.
        }
    }
