---
title: "tecnologias de banco de dados de SQL na memória aaaAzure | Microsoft Docs"
description: "Tecnologias de banco de dados de SQL na memória do Azure aprimorar o desempenho de saudação do transacional e de cargas de trabalho de análise. Saiba como tootake proveito dessas tecnologias."
services: sql-database
documentationCenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: 250ef341-90e5-492f-b075-b4750d237c05
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jodebrui
ms.openlocfilehash: 1bacd7297b2f9b018853088eabf2a2ee66a9cb43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-performance-by-using-in-memory-technologies-in-sql-database"></a>Otimizar o desempenho usando tecnologias In-Memory no Banco de Dados SQL

Usando tecnologias In-Memory no Banco de Dados SQL do Azure, você pode obter melhorias no desempenho com várias cargas de trabalho: transacional (OLTP [processamento transacional online]), análise (OLAP [processamento analítico online]) e misto (HTAP [processamento híbrido analítico/de transação]). Porque hello mais eficiente de consultas e processamento de transações, tecnologias na memória também ajudarão-lo tooreduce custo. Normalmente, você não precisa tooupgrade Olá preço de saudação ganhos de desempenho de tooachieve de banco de dados. Em alguns casos, você mesmo poderá reduzir Olá preço, enquanto continua vendo melhorias de desempenho com tecnologias na memória.

Aqui estão dois exemplos de como o OLTP na memória ajudou toosignificantly melhorar o desempenho:

- Usando OLTP na memória, [soluções de negócios de Quorum foi capaz de toodouble sua carga de trabalho melhorando DTUs em 70%](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).
    - DTU significa *unidade de taxa de transferência de banco de dados* e inclui uma medição de consumo de recursos.
- Olá, vídeo a seguir demonstra uma melhoria significativa no consumo de recursos com uma carga de trabalho de exemplo: [OLTP na memória de vídeo de banco de dados do SQL Azure](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).
    - Para obter mais detalhes, consulte Olá postagem de blog: [OLTP na memória na postagem do Blog de banco de dados do Azure SQL](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)

Tecnologias na memória estão disponíveis em todos os bancos de dados da camada Premium Olá, incluindo bancos de dados em pools Elásticos Premium.

Hello vídeo a seguir explica os ganhos potenciais de desempenho com tecnologias na memória no banco de dados do SQL Azure. Lembre-se que o ganho de desempenho Olá que você sempre vê depende de muitos fatores, incluindo a natureza de saudação de carga de trabalho de saudação e dados, o padrão de acesso de banco de dados Olá e assim por diante.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-In-Memory-Technologies/player]
>
>

Banco de dados SQL do Azure tem Olá tecnologias na memória a seguir:

- O *OLTP in-memory* aumenta a taxa de transferência e reduz a latência do processamento de transações. Os cenários que se beneficiam do OLTP In-Memory são: processamento de transações de alta taxa de transferência, como comércio e jogos, ingestão de dados de eventos ou dispositivos IoT, cache, carregamento de dados e cenários de variáveis de tabela e tabelas temporárias.
- *Índices columnstore clusterizados* reduzir o volume de armazenamento (os tempos de too10) e melhorar o desempenho de consultas de relatórios e análises. Você pode usá-lo com as tabelas de fatos em seu toofit armazéns de dados mais dados no banco de dados e melhorar o desempenho. Além disso, você pode usá-lo com os dados históricos em tooarchive seu banco de dados operacional e ser capaz de tooquery too10 horas mais dados.
- *Índices columnstore não clusterizados* para obter ajuda HTAP você toogain de informações em tempo real em seus negócios por meio de consulta Olá operacional do banco de dados diretamente, sem Olá necessidade toorun um cara extração, transformação e processo de carregamento (ETL) e aguarde para toobe de depósito de dados Olá preenchido. Índices columnstore não clusterizados permitem a execução muito rápida de consultas de análise no banco de dados OLTP hello, reduzindo o impacto de Olá na carga de trabalho operacional hello.
- Você também pode ter a combinação de saudação de uma tabela com otimização de memória com um índice columnstore. Essa combinação permite que você tooperform transação muito rápido processamento e muito*simultaneamente* executar análise de consultas muito rapidamente em Olá mesmo dados.

Índices columnstore e OLTP na memória tem sido parte do produto do SQL Server Olá desde 2012 e 2014, respectivamente. SQL Server e banco de dados SQL do Azure compartilham Olá mesma implementação das tecnologias na memória. Daqui em diante, os novos recursos para essas tecnologias serão lançados primeiro no Banco de Dados SQL do Azure, antes de serem lançados no SQL Server.

Este tópico descreve os aspectos de índices columnstore e OLTP na memória que são específico tooAzure banco de dados SQL e também inclui exemplos:
- Você verá o impacto de saudação dessas tecnologias em limites de tamanho de armazenamento e os dados.
- Você verá como toomanage Olá movimentação de bancos de dados usar essas tecnologias entre hello diferente camadas de preços.
- Você verá dois exemplos que ilustram o uso de saudação do OLTP na memória, bem como índices columnstore no banco de dados do SQL Azure.

Consulte Olá recursos para obter mais informações a seguir.

Informações detalhadas sobre as tecnologias de saudação:

- [Visão geral de OLTP na memória e cenários de uso](https://msdn.microsoft.com/library/mt774593.aspx) (inclui referências estudos de caso de toocustomer e informações tooget iniciado)
- [Documentação para OLTP in-memory](http://msdn.microsoft.com/library/dn133186.aspx)
- [Guia de índices ColumnStore](https://msdn.microsoft.com/library/gg492088.aspx)
- HTAP (Processamento Transacional e Analítico Híbrido), também conhecido como [análise operacional em tempo real](https://msdn.microsoft.com/library/dn817827.aspx)

Uma rápida introdução em OLTP na memória: [início rápido 1: tecnologias do OLTP na memória para um desempenho mais rápido do T-SQL](http://msdn.microsoft.com/library/mt694156.aspx) (outro artigo toohelp começar)

Vídeos detalhados sobre as tecnologias de saudação:

- [O OLTP na memória no banco de dados do SQL Azure](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (que contém uma demonstração de desempenho de benefícios e as etapas tooreproduce esses resultados por conta própria)
- [Vídeos OLTP na memória: O que é e quando/como toouse-lo](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/03/in-memory-oltp-video-what-it-is-and-whenhow-to-use-it/)
- [Índice Columnstore: vídeos sobre a análise em memória do Ignite 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/04/columnstore-index-in-memory-analytics-i-e-columnstore-index-videos-from-ignite-2016/)

## <a name="storage-and-data-size"></a>Armazenamento e tamanho dos dados

### <a name="data-size-and-storage-cap-for-in-memory-oltp"></a>Tamanho dos dados e limite de armazenamento do OLTP in-memory

O OLTP in-memory inclui tabelas com otimização de memória, que são usadas para armazenar dados do usuário. Essas tabelas são necessária toofit na memória. Porque você gerencia memória diretamente em Olá serviço de banco de dados SQL, temos o conceito de saudação de uma cota para dados de usuário. Essa ideia é chamado tooas *armazenamento OLTP na memória*.

Cada tipo de preço de banco de dados independente e cada tipo de preço de pool elástico com suporte incluem determinada quantidade de Armazenamento do OLTP in-memory. No momento da saudação de gravação, você obterá um gigabyte de armazenamento para cada 125 unidades de transação do banco de dados (DTUs) ou o banco de dados Elástico unidades de transação (eDTUs).

Olá [camadas de serviço do banco de dados SQL](sql-database-service-tiers.md) artigo possui a lista oficial Olá Olá OLTP na memória de armazenamento do que está disponível para cada banco de dados autônomo e camada de preços de pool Elástico.

saudação de contagem de itens para o limite de armazenamento do OLTP na memória a seguir:

- Linhas de dados de usuário ativo em tabelas com otimização de memória e variáveis de tabela. Observe que as versões antigas de linha não são contadas cap hello.
- Índices em tabelas com otimização de memória.
- Custo operacional das operações ALTER TABLE.

Se você atingir o limite Olá, você receberá um erro de limite de cota, e você não é mais capaz de dados tooinsert ou atualização. toomitigate esse erro, exclua dados ou aumente Olá preço do banco de dados de saudação ou pool.

Para obter detalhes sobre como monitorar a utilização de armazenamento do OLTP na memória e como configurar alertas quando é atingido o limite de saudação quase, consulte [armazenamento na memória do Monitor](sql-database-in-memory-oltp-monitoring.md).

#### <a name="about-elastic-pools"></a>Sobre pools elásticos

Com pools Elásticos, Olá armazenamento OLTP na memória é compartilhada entre todos os bancos de dados no pool de saudação. Portanto, o uso de saudação em um banco de dados pode afetar potencialmente outros bancos de dados. As duas mitigações para esse problema são:

- Configure um Max-eDTU para bancos de dados que é menor do que a contagem de eDTU Olá para pool hello como um todo. Esse máximo Arredonda a utilização do armazenamento Olá OLTP na memória, em qualquer banco de dados no pool de hello, tamanho toohello que corresponde a contagem de eDTU toohello.
- Defina um Min-eDTU maior que 0. Este mínimo garante que cada banco de dados no pool de saudação tenha a quantidade de saudação do armazenamento de OLTP na memória disponível que corresponde a toohello configurado eDTU mínimo.

### <a name="data-size-and-storage-for-columnstore-indexes"></a>Tamanho dos dados e armazenamento para índices columnstore

Índices ColumnStore não são necessária toofit na memória. Portanto, Olá apenas limite no tamanho de saudação de índices Olá Olá geral o tamanho máximo, que está documentado na Olá [camadas de serviço do banco de dados SQL](sql-database-service-tiers.md) artigo.

Quando você usa os índices columnstore clusterizados, compactação Colunar é usada para o armazenamento de tabela base hello. Essa compactação pode reduzir significativamente o volume de armazenamento de saudação de seus dados de usuário, o que significa que você pode colocar mais dados no banco de dados de saudação. E compactação Olá pode ser aumentada com [compactação de arquivamento Colunar](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression). Olá compactação que você pode obter depende da natureza de saudação do dados saudação, mas a compactação de saudação 10 vezes não é incomum.

Por exemplo, se você tiver um banco de dados com um tamanho máximo de 1 TB (terabyte) e obter a compactação Olá 10 vezes usando índices columnstore, você pode ajustar um total de 10 TB de dados de usuário no banco de dados de saudação.

Quando você usar índices columnstore não clusterizado, tabela base Olá ainda é armazenada em formato de rowstore tradicionais de saudação. Portanto, Olá economia de armazenamento não é tão grande como com índices columnstore clusterizados. No entanto, se você estiver substituindo um número de índices não clusterizados tradicionais com um único índice columnstore, você ainda pode ver uma economia geral no espaço de armazenamento Olá para a tabela de saudação.

## <a name="moving-databases-that-use-in-memory-technologies-between-pricing-tiers"></a>Movendo bancos de dados que usam tecnologias In-Memory entre tipos de preço

Há nunca quaisquer incompatibilidades ou outros problemas ao atualizar tooa maior preço, como de tooPremium padrão. recursos e funcionalidades disponíveis Olá apenas aumentam.

Mas Olá downgrade preço pode afetar negativamente o seu banco de dados. impacto de saudação é especialmente aparente quando você fazer o downgrade de tooStandard Premium ou Basic ao seu banco de dados contém objetos OLTP na memória. Tabelas com otimização de memória e índices columnstore, não estão disponíveis após o downgrade da saudação (mesmo se elas permanecem visíveis). Olá mesmas considerações se aplicam quando você está diminuindo Olá preço de um pool Elástico ou mover um banco de dados com tecnologias na memória, em um padrão ou básico pool Elástico.

### <a name="in-memory-oltp"></a>OLTP Na Memória

*Fazendo downgrade tooBasic/Standard*: OLTP na memória não tem suporte em bancos de dados Olá camada Standard ou Basic. Além disso, não é possível toomove um banco de dados que tenha qualquer toohello de objetos OLTP na memória camada Standard ou Basic.

Antes de fazer o downgrade do banco de dados de saudação tooStandard/Basic, remova todas as tabelas com otimização de memória e os tipos de tabela, bem como todos os módulos do T-SQL compilados nativamente.

Não há um modo programático toounderstand se um determinado banco de dados oferece suporte a OLTP na memória. Você pode executar Olá consulta Transact-SQL a seguir:

```
SELECT DatabasePropertyEx(DB_NAME(), 'IsXTPSupported');
```

Se a consulta Olá retorna **1**, há suporte para o OLTP na memória no banco de dados.


*Fazendo downgrade de nível mais baixo de Premium tooa*: dados em tabelas com otimização de memória devem se ajustar no armazenamento do OLTP na memória Olá que está associado a saudação de preço do banco de dados de saudação ou está disponível no pool Elástico hello. Se você tentar Olá toolower preço ou move o banco de dados de saudação em um pool que não tem o armazenamento de OLTP na memória suficiente disponível, Olá operação falhará.

### <a name="columnstore-indexes"></a>Índices ColumnStore

*Fazendo downgrade tooBasic ou padrão*: Columnstore índices têm suporte apenas de preço Premium Olá e não no hello camadas Standard ou Basic. Quando você fazer downgrade do seu banco de dados tooStandard ou Basic, o índice columnstore ficará indisponível. sistema de saudação mantém o índice columnstore, mas ele nunca utiliza um índice de saudação. Se você atualizar o tooPremium voltar mais tarde, o índice columnstore é imediatamente pronto toobe utilizada novamente.

Se você tiver um **clusterizado** índice columnstore, toda a tabela Olá fica indisponível após o downgrade da camada. Portanto, recomendamos que você remova todos os *clusterizado* antes de fazer o downgrade do seu banco de dados abaixo da camada de Premium Olá dos índices columnstore.

*Fazendo downgrade de nível mais baixo de Premium tooa*: este downgrade terá êxito se o banco de dados inteiro Olá adequada Olá o tamanho máximo para o destino de saudação preço, ou em armazenamento de saudação disponível no pool Elástico hello. Não há nenhum impacto específico de índices de columnstore hello.


<a id="install_oltp_manuallink" name="install_oltp_manuallink"></a>

&nbsp;

## <a name="1-install-hello-in-memory-oltp-sample"></a>1. Instalar o exemplo de OLTP na memória hello

Você pode criar o banco de dados do exemplo hello AdventureWorksLT com alguns cliques no hello [portal do Azure](https://portal.azure.com/). Em seguida, hello etapas nesta seção explicam como você pode aprimorar seu banco de dados AdventureWorksLT com objetos OLTP na memória e demonstrar os benefícios de desempenho.

Para ver uma demonstração de desempenho mais simples, porém, mais visualmente interessante do OLTP in-memory, veja:

- Versão: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)
- Código-fonte: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)

#### <a name="installation-steps"></a>Etapas de instalação

1. Em Olá [portal do Azure](https://portal.azure.com/), criar um banco de dados Premium em um servidor. Saudação de conjunto **fonte** toohello AdventureWorksLT de dados de exemplo. Para obter instruções detalhadas, consulte [Criar seu primeiro Banco de Dados SQL do Azure](sql-database-get-started-portal.md).

2. Conecte-se o banco de dados toohello com o SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).

3. Saudação de cópia [script In-Memory OLTP Transact-SQL](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) tooyour área de transferência. Olá script T-SQL cria Olá objetos na memória necessária no banco de dados do hello AdventureWorksLT exemplo que você criou na etapa 1.

4. Cole o script T-SQL de saudação no SSMS e, em seguida, execute o script hello. Olá `MEMORY_OPTIMIZED = ON` instruções CREATE TABLE de cláusula são cruciais. Por exemplo:


```
CREATE TABLE [SalesLT].[SalesOrderHeader_inmem](
    [SalesOrderID] int IDENTITY NOT NULL PRIMARY KEY NONCLUSTERED ...,
    ...
) WITH (MEMORY_OPTIMIZED = ON);
```


#### <a name="error-40536"></a>Erro 40536


Se você receber o erro 40536 quando você executar o script hello T-SQL, execute Olá tooverify de script T-SQL a seguir se na memória oferece suporte a banco de dados de saudação:


```
SELECT DatabasePropertyEx(DB_Name(), 'IsXTPSupported');
```


Um resultado **0** significa que não há suporte para In-Memory e **1** significa que há suporte. problema de saudação toodiagnose, certifique-se de que esse banco de dados de saudação é a camada de serviço Premium Olá.


#### <a name="about-hello-created-memory-optimized-items"></a>Sobre Olá criado itens com otimização de memória

**Tabelas**: exemplo hello contém Olá tabelas com otimização de memória a seguir:

- SalesLT.Product_inmem
- SalesLT.SalesOrderHeader_inmem
- SalesLT.SalesOrderDetail_inmem
- Demo.DemoSalesOrderHeaderSeed
- Demo.DemoSalesOrderDetailSeed


Você pode inspecionar as tabelas com otimização de memória por meio de saudação **Pesquisador de objetos** no SSMS. Clique com o botão direito do mouse em **Tabelas** > **Filtro** > **Configurações do Filtro** > **Com otimização de memória**. valor de saudação é igual a 1.


Ou você pode consultar as exibições do catálogo hello, como:


```
SELECT is_memory_optimized, name, type_desc, durability_desc
    FROM sys.tables
    WHERE is_memory_optimized = 1;
```


**Procedimento armazenado compilado nativamente**: você pode inspecionar SalesLT.usp_InsertSalesOrder_inmem por meio de uma consulta de exibição de catálogo:


```
SELECT uses_native_compilation, OBJECT_NAME(object_id), definition
    FROM sys.sql_modules
    WHERE uses_native_compilation = 1;
```


&nbsp;

### <a name="run-hello-sample-oltp-workload"></a>Executar a carga de trabalho OLTP de exemplo hello

Olá a única diferença entre Olá após dois *procedimentos armazenados* é que o primeiro procedimento de saudação usa versões com otimização de memória das tabelas de saudação, durante a saudação segundo procedimento usa tabelas em disco regulares de saudação:

- SalesLT**.**usp_InsertSalesOrder**_inmem**
- SalesLT**.**usp_InsertSalesOrder**_ondisk**


Nesta seção, consulte como toouse Olá útil **ostress.exe** tooexecute utilitário Olá dois procedimentos armazenados nos níveis estressantes. Você pode comparar quanto tempo demora para Olá dois estresse executa toofinish.


Ao executar ostress.exe, recomendamos que você passa valores de parâmetro projetados para os seguintes hello:

- Execute um grande número de conexões simultâneas usando -n100.
- Faça com que cada conexão entre em loop centenas de vezes usando -r500.


No entanto, você talvez queira toostart com valores muito menores como - n10 e - r50 tooensure que tudo está funcionando.


### <a name="script-for-ostressexe"></a>Script para ostress.exe


Esta seção exibe o script T-SQL Olá incorporado em nossa linha de comando ostress.exe. script Hello usa itens que foram criados pelo Olá script T-SQL que você instalou anteriormente.


Olá script a seguir insere um pedido de vendas de exemplo com cinco itens de linha com otimização de memória a seguir Olá *tabelas*:

- SalesLT.SalesOrderHeader_inmem
- SalesLT.SalesOrderDetail_inmem


```
DECLARE
    @i int = 0,
    @od SalesLT.SalesOrderDetailType_inmem,
    @SalesOrderID int,
    @DueDate datetime2 = sysdatetime(),
    @CustomerID int = rand() * 8000,
    @BillToAddressID int = rand() * 10000,
    @ShipToAddressID int = rand() * 10000;

INSERT INTO @od
    SELECT OrderQty, ProductID
    FROM Demo.DemoSalesOrderDetailSeed
    WHERE OrderID= cast((rand()*60) as int);

WHILE (@i < 20)
begin;
    EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT,
        @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od;
    SET @i = @i + 1;
end
```


Olá toomake *ondisk* Olá a versão do script T-SQL anterior para ostress.exe, você substituiria as duas ocorrências de saudação *inmem* subcadeia de caracteres com *ondisk*. Essas substituições afetam os nomes de saudação de tabelas e procedimentos armazenados.


### <a name="install-rml-utilities-and-ostress"></a>Instalar utilitários RML e o ostress


Idealmente, você deve planejar toorun ostress.exe em uma máquina virtual do Azure (VM). Você deve criar um [VM do Azure](https://azure.microsoft.com/documentation/services/virtual-machines/) em Olá mesma região geográfica do Azure onde seu banco de dados AdventureWorksLT reside. Mas você pode executar o ostress.exe em seu laptop.


Olá VM, ou em qualquer host que você escolher, instalar utilitários de linguagem de marcação de reprodução (RML) hello. utilitários de saudação incluem ostress.exe.

Para obter mais informações, consulte:
- Olá discussão ostress.exe [banco de dados de exemplo para OLTP na memória](http://msdn.microsoft.com/library/mt465764.aspx).
- [Banco de dados de exemplo para OLTP In-Memory](http://msdn.microsoft.com/library/mt465764.aspx).
- Olá [blog para a instalação ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).



<!--
dn511655.aspx is for SQL 2014,
[Extensions tooAdventureWorks tooDemonstrate In-Memory OLTP]
(http://msdn.microsoft.com/library/dn511655&#x28;v=sql.120&#x29;.aspx)

whereas for SQL 2016+
[Sample Database for In-Memory OLTP]
(http://msdn.microsoft.com/library/mt465764.aspx)
-->



### <a name="run-hello-inmem-stress-workload-first"></a>Executar Olá *inmem* enfatizar a carga de trabalho pela primeira vez


Você pode usar um *Cmd Prompt RML* janela toorun nossa linha de comando ostress.exe. parâmetros de linha de comando Olá direcionam ostress para:

- Execute 100 conexões simultaneamente (-n100).
- Ter cada conexão que executar o script T-SQL de saudação 50 vezes (-r50).


```
ostress.exe -n100 -r50 -S<servername>.database.windows.net -U<login> -P<password> -d<database> -q -Q"DECLARE @i int = 0, @od SalesLT.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand()* 10000; INSERT INTO @od SELECT OrderQty, ProductID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*60) as int); WHILE (@i < 20) begin; EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od; set @i += 1; end"
```


Olá toorun anterior ostress.exe linha de comando:


1. Redefina conteúdo de dados do banco de dados de saudação executando todos os dados de saudação que foi inseridos por todas as execuções anteriores Olá comando no SSMS, toodelete a seguir:

    ``` tsql
    EXECUTE Demo.usp_DemoReset;
    ```

2. Copie o texto de saudação de saudação anterior ostress.exe linha de comando tooyour área de transferência.

3. Substituir saudação `<placeholders>` para Olá parâmetros -S - U -P -d com hello corrigir os valores reais.

4. Execute a linha de comando editada em uma janela Cmd RML.


#### <a name="result-is-a-duration"></a>O resultado é uma duração


Quando ostress.exe é concluído, ele grava Olá duração da execução como a linha final de saída na janela de Cmd RML hello. Por exemplo, uma execução de teste mais curta dura aproximadamente 1,5 minuto:

`11/12/15 00:35:00.873 [0x000030A8] OSTRESS exiting normally, elapsed time: 00:01:31.867`


#### <a name="reset-edit-for-ondisk-then-rerun"></a>Redefinir, editar *_ondisk* e executar novamente


Depois de ter resultado de saudação do hello *inmem* executar, execute Olá seguindo as etapas para Olá *ondisk* executar:


1. Redefina o banco de dados de Olá executando todos os dados de saudação que foi inseridos por Olá anterior executar Olá comando no SSMS toodelete a seguir:
```
EXECUTE Demo.usp_DemoReset;
```

2. Editar saudação ostress.exe linha de comando tooreplace todos os *inmem* com *ondisk*.

3. Execute novamente o ostress.exe para Olá pela segunda vez e capturar resultados de duração de saudação.

4. Novamente, redefina Olá banco de dados (com responsabilidade excluindo o que pode ser uma grande quantidade de dados de teste).


#### <a name="expected-comparison-results"></a>Resultados esperados para a comparação

Nossos testes na memória mostraram que o desempenho aprimorado por **nove vezes** para essa carga de trabalho simples, com ostress em execução em uma VM do Azure no hello mesma região do Azure como banco de dados de saudação.

<a id="install_analytics_manuallink" name="install_analytics_manuallink"></a>

&nbsp;

## <a name="2-install-hello-in-memory-analytics-sample"></a>2. Instalar o exemplo de análise in-memory hello


Nesta seção, você comparar hello e/s e resultados de estatísticas quando você estiver usando um índice columnstore em vez de um índice de árvore b tradicional.


Para análise em tempo real em uma carga de trabalho OLTP, geralmente é melhor toouse um índice columnstore não clusterizado. Para ver mais detalhes, confira [Índices Columnstore Descritos](http://msdn.microsoft.com/library/gg492088.aspx).



### <a name="prepare-hello-columnstore-analytics-test"></a>Preparar o teste de análise de columnstore Olá


1. Use Olá toocreate portal do Azure um banco de dados novo AdventureWorksLT do exemplo hello.
 - Use esse nome exato.
 - Escolha qualquer camada de serviço Premium.

2. Saudação de cópia [sql_in memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) tooyour área de transferência.
 - Olá script T-SQL cria Olá objetos na memória necessária no banco de dados do hello AdventureWorksLT exemplo que você criou na etapa 1.
 - script Hello cria a tabela de dimensões hello e duas tabelas de fatos. tabelas de fatos Olá são preenchidas com 3.5 milhões de linhas cada.
 - script Hello pode levar 15 minutos toocomplete.

3. Cole o script T-SQL de saudação no SSMS e, em seguida, execute o script hello. Olá **COLUMNSTORE** palavra-chave em Olá **CREATE INDEX** instrução é fundamental, como:<br/>`CREATE NONCLUSTERED COLUMNSTORE INDEX ...;`

4. Defina nível de toocompatibility AdventureWorksLT 130:<br/>`ALTER DATABASE AdventureworksLT SET compatibility_level = 130;`

    Nível 130 não é recursos de memória de tooIn diretamente relacionados. Mas o nível 130 geralmente oferece desempenho de consulta mais rápido que o 120.


#### <a name="key-tables-and-columnstore-indexes"></a>Tabelas chave e índices de columnstore


- dbo. FactResellerSalesXL_CCI é uma tabela que tem um índice columnstore clusterizado, avançou compactação no hello *dados* nível.

- dbo. FactResellerSalesXL_PageCompressed é uma tabela que tem um equivalente regular índice clusterizado, é compactado apenas no hello *página* nível.


#### <a name="key-queries-toocompare-hello-columnstore-index"></a>Índice de columnstore consultas chave toocompare Olá


Há [vários tipos de consultas T-SQL que você pode executar](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) toosee melhorias de desempenho. Na etapa 2 Olá script T-SQL, paga par de toothis atenção de consultas. Elas diferem apenas em uma linha:


- `FROM FactResellerSalesXL_PageCompressed a`
- `FROM FactResellerSalesXL_CCI a`


Um índice columnstore clusterizado está em Olá FactResellerSalesXL\_tabela CCI.

Olá trecho de script T-SQL a seguir imprime estatísticas de e/s e o tempo de consulta de saudação de cada tabela.


```
/*********************************************************************
Step 2 -- Overview
-- Page Compressed BTree table v/s Columnstore table performance differences
-- Enable actual Query Plan in order toosee Plan differences when Executing
*/
-- Ensure Database is in 130 compatibility mode
ALTER DATABASE AdventureworksLT SET compatibility_level = 130
GO

-- Execute a typical query that joins hello Fact Table with dimension tables
-- Note this query will run on hello Page Compressed table, Note down hello time
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO

SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_PageCompressed a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO
SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO


-- This is hello same Prior query on a table with a clustered columnstore index CCI
-- hello comparison numbers are even more dramatic hello larger hello table is (this is an 11 million row table only)
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO
SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_CCI a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO

SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO
```

Em um banco de dados de preço P2 hello, você pode esperar aproximadamente nove vezes Olá ganho de desempenho para essa consulta usando um índice columnstore clusterizado Olá em comparação com um índice tradicional hello. Com P15, você pode esperar aproximadamente 57 vezes ganho de desempenho de saudação usando o índice de columnstore hello.



## <a name="next-steps"></a>Próximas etapas

- [Início Rápido 1: Tecnologias OLTP in-memory para um desempenho mais rápido do T-SQL](http://msdn.microsoft.com/library/mt694156.aspx)

- [Usar o OLTP In-Memory em um aplicativo existente do SQL Azure](sql-database-in-memory-oltp-migration.md)

- [Monitorar o armazenamento do OLTP In-Memory](sql-database-in-memory-oltp-monitoring.md) para o OLTP In-Memory


## <a name="additional-resources"></a>Recursos adicionais

#### <a name="deeper-information"></a>Informações mais detalhadas

- [Saiba como o Quorum dobra a principal carga de trabalho do banco de dados, enquanto reduz a DTU em 70% com o OLTP in-memory no Banco de Dados SQL](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)

- [Postagem de Blog de OLTP na memória do Banco de Dados SQL do Azure](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)

- [Saiba mais sobre o OLTP in-memory](http://msdn.microsoft.com/library/dn133186.aspx)

- [Saiba mais sobre os índices columnstore](https://msdn.microsoft.com/library/gg492088.aspx)

- [Saiba mais sobre a análise operacional em tempo real](http://msdn.microsoft.com/library/dn817827.aspx)

- Veja [Padrões comuns de carga de trabalho e considerações sobre migração](http://msdn.microsoft.com/library/dn673538.aspx) (que descreve os padrões de carga de trabalho para os quais o OLTP In-Memory geralmente fornece ganhos significativos de desempenho)

#### <a name="application-design"></a>Design do aplicativo

- [OLTP Na Memória (Otimização Na Memória)](http://msdn.microsoft.com/library/dn133186.aspx)

- [Usar o OLTP In-Memory em um aplicativo existente do SQL Azure](sql-database-in-memory-oltp-migration.md)

#### <a name="tools"></a>Ferramentas

- [Portal do Azure](https://portal.azure.com/)

- [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx)

- [SSDT (Ferramentas de Dados do SQL Server)](http://msdn.microsoft.com/library/mt204009.aspx)
