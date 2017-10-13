---
title: Tecnologias In-Memory do Banco de Dados SQL do Azure | Microsoft Docs
description: "As tecnologias In-Memory do Banco de Dados SQL do Azure melhoram muito o desempenho de cargas de trabalho transacionais e analíticas. Saiba como aproveitar as vantagens dessas tecnologias."
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
ms.openlocfilehash: 4cb45551c486263f26947e5684d54b4f2ecc7410
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="optimize-performance-by-using-in-memory-technologies-in-sql-database"></a>Otimizar o desempenho usando tecnologias In-Memory no Banco de Dados SQL

Usando tecnologias In-Memory no Banco de Dados SQL do Azure, você pode obter melhorias no desempenho com várias cargas de trabalho: transacional (OLTP [processamento transacional online]), análise (OLAP [processamento analítico online]) e misto (HTAP [processamento híbrido analítico/de transação]). Devido ao processamento de transações e consulta mais eficientes, as tecnologias In-Memory também ajudam a reduzir os custos. Você normalmente não precisa atualizar o tipo de preço do banco de dados para obter ganhos de desempenho. Em alguns casos, você mesmo poderá até mesmo reduzir o tipo de preço e ainda continuar a ver melhorias de desempenho com as tecnologias In-Memory.

Estes são dois exemplos de como o OLTP In-Memory ajudou a melhorar significativamente o desempenho:

- Usando o OLTP In-Memory, a [Quorum Business Solutions foi capaz de duplicar a carga de trabalho, melhorando as DTUs em 70%](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).
    - DTU significa *unidade de taxa de transferência de banco de dados* e inclui uma medição de consumo de recursos.
- O vídeo a seguir demonstra uma melhoria significativa no consumo de recursos com uma carga de trabalho de exemplo: [OLTP In-Memory no Vídeo do Banco de Dados SQL do Azure](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).
    - Para obter mais detalhes, confira a postagem no blog: [Postagem de Blog de OLTP na memória do Banco de Dados SQL do Azure](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)

As tecnologias In-Memory estão disponíveis em todos os bancos de dados da camada Premium, incluindo bancos de dados em pools elásticos Premium.

O vídeo a seguir explica os possíveis ganhos de desempenho com as tecnologias em memória no Banco de Dados SQL do Azure. Lembre-se de que o ganho de desempenho que você verá sempre dependerá de diversos fatores, incluindo a natureza da carga de trabalho e dos dados, o padrão de acesso do banco de dados e assim por diante.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-In-Memory-Technologies/player]
>
>

O Banco de Dados SQL do Azure conta com as seguintes tecnologias em memória:

- O *OLTP in-memory* aumenta a taxa de transferência e reduz a latência do processamento de transações. Os cenários que se beneficiam do OLTP In-Memory são: processamento de transações de alta taxa de transferência, como comércio e jogos, ingestão de dados de eventos ou dispositivos IoT, cache, carregamento de dados e cenários de variáveis de tabela e tabelas temporárias.
- Os *índices columnstore clusterizados* reduzem seu volume de armazenamento (em até 10 vezes) e melhoram o desempenho de relatórios e consultas de análise. Você pode usá-lo com tabelas de fatos em data marts para colocar mais dados no banco de dados e melhorar o desempenho. Além disso, também é possível usá-lo com os dados históricos no banco de dados operacional para arquivar e conseguir consultar até 10 vezes mais dados.
- *Índices columnstore não clusterizados* para HTAP ajudam a obter análises em tempo real sobre seus negócios consultando o banco de dados operacional diretamente, sem a necessidade de executar um processo ETL (extração, transformação e carregamento) caro e aguardar o data warehouse ser populado. Os índices columnstore não clusterizados permitem uma execução muito rápida das consultas de análise no banco de dados OLTP, enquanto reduzem o impacto sobre a carga de trabalho operacional.
- Você também pode ter a combinação de tabela com otimização de memória com um índice columnstore. Essa combinação permite que você execute o processamento de transações com muita rapidez e execute *simultaneamente* consultas de análise rapidamente nos mesmos dados.

Tanto os índices columnstore quanto o OLTP In-Memory integram o produto SQL Server desde 2012 e 2014, respectivamente. O Banco de Dados SQL do Azure e o SQL Server compartilham a mesma implementação de tecnologias In-Memory. Daqui em diante, os novos recursos para essas tecnologias serão lançados primeiro no Banco de Dados SQL do Azure, antes de serem lançados no SQL Server.

Este tópico descreve aspectos do OLTP In-Memory e dos índices Columnstore específicos ao Banco de Dados SQL do Azure, além de também incluir exemplos:
- Você verá o impacto dessas tecnologias no armazenamento e dos limites de tamanho dos dados.
- Você verá como gerenciar a movimentação dos bancos de dados que utilizam essas tecnologias entre os diferentes tipos de preço.
- Você verá dois exemplos que ilustram o uso do OLTP In-Memory, bem como dos índices columnstore, no Banco de Dados SQL do Azure.

Consulte os seguintes recursos para obter mais informações.

Informações detalhadas sobre as tecnologias:

- [Visão geral e cenários de uso do OLTP In-Memory](https://msdn.microsoft.com/library/mt774593.aspx) (incluindo referências a estudos de caso de cliente e informações para começar)
- [Documentação para OLTP in-memory](http://msdn.microsoft.com/library/dn133186.aspx)
- [Guia de índices ColumnStore](https://msdn.microsoft.com/library/gg492088.aspx)
- HTAP (Processamento Transacional e Analítico Híbrido), também conhecido como [análise operacional em tempo real](https://msdn.microsoft.com/library/dn817827.aspx)

Uma prévia rápida no OLTP In-Memory: [Início Rápido 1: tecnologias OLTP In-Memory para um desempenho mais rápido do T-SQL](http://msdn.microsoft.com/library/mt694156.aspx) (outro artigo para ajudar você a se familiarizar)

Vídeos detalhados sobre as tecnologias:

- [OLTP In-Memory no Banco de Dados SQL do Azure](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (que contém uma demonstração dos benefícios de desempenho e as etapas para você mesmo reproduzir esses resultados)
- [Vídeos sobre o OLTP in-memory: O que é e quando e como usá-lo](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/03/in-memory-oltp-video-what-it-is-and-whenhow-to-use-it/)
- [Índice Columnstore: vídeos sobre a análise em memória do Ignite 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/04/columnstore-index-in-memory-analytics-i-e-columnstore-index-videos-from-ignite-2016/)

## <a name="storage-and-data-size"></a>Armazenamento e tamanho dos dados

### <a name="data-size-and-storage-cap-for-in-memory-oltp"></a>Tamanho dos dados e limite de armazenamento do OLTP in-memory

O OLTP in-memory inclui tabelas com otimização de memória, que são usadas para armazenar dados do usuário. Essas tabelas precisam caber na memória. Como você gerencia a memória diretamente no serviço do Banco de Dados SQL, temos o conceito de uma cota para dados de usuário. Esse conceito é conhecido como *Armazenamento de OLTP In-Memory*.

Cada tipo de preço de banco de dados independente e cada tipo de preço de pool elástico com suporte incluem determinada quantidade de Armazenamento do OLTP in-memory. Até o momento em que esse documento foi redigido, você recebe um gigabyte de armazenamento para cada 125 DTUs (unidades de transação do banco de dados) ou eDTUs (unidades de transação do banco de dados elástico).

Os artigo [Tipos de preço do Banco de Dados SQL](sql-database-service-tiers.md) contém a lista oficial de armazenamento do OLTP in-memory disponível para cada tipo de preço de banco de dados independente e pool elástico com suporte.

Os itens a seguir contam para seu limite de armazenamento do OLTP in-memory:

- Linhas de dados de usuário ativo em tabelas com otimização de memória e variáveis de tabela. Observe que as versões de linha antigas não entram na contagem do limite.
- Índices em tabelas com otimização de memória.
- Custo operacional das operações ALTER TABLE.

Se atingir o limite, você receberá um erro de limite de cota atingido e não conseguirá inserir ou atualizar os dados. Para atenuar esse erro, exclua dados ou aumente o tipo de preço do banco de dados ou do pool.

Para obter detalhes sobre como monitorar a utilização do armazenamento do OLTP in-memory e configurar alertas quando estiver perto de atingir o limite, consulte [Monitorar o armazenamento in-memory](sql-database-in-memory-oltp-monitoring.md).

#### <a name="about-elastic-pools"></a>Sobre pools elásticos

Com os pools elásticos, o armazenamento do OLTP in-memory é compartilhado entre todos os bancos de dados no pool. Portanto, o uso de um banco de dados pode afetar outros bancos de dados. As duas mitigações para esse problema são:

- Configure um Max-eDTU para bancos de dados que seja menor que a contagem de eDTUs do pool como um todo. Isso proporciona um limite máximo à utilização no armazenamento do OLTP in-memory em qualquer banco de dados no pool ao tamanho que corresponde à contagem de eDTUs.
- Defina um Min-eDTU maior que 0. Isso garante o mínimo que cada banco de dados no pool tem a quantidade de armazenamento do OLTP in-memory disponível correspondente ao Min-eDTU configurado.

### <a name="data-size-and-storage-for-columnstore-indexes"></a>Tamanho dos dados e armazenamento para índices columnstore

Os índices columnstore não precisam caber na memória. Portanto, o único limite para o tamanho dos índices é o tamanho máximo do banco de dados geral, que está documentado no artigo [Camadas de serviço do Banco de Dados SQL](sql-database-service-tiers.md).

Ao usar os índices columnstore clusterizados, a compactação vertical é usada para o armazenamento de tabelas base. Essa compactação pode reduzir consideravelmente o volume de armazenamento dos dados do usuário, o que significa que você pode colocar mais dados no banco de dados. E a compactação pode ser ainda maior com a [compactação de arquivamento vertical](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression). A quantidade de compactação que pode ser obtida depende da natureza dos dados, mas uma compactação de 10 vezes não é incomum.

Por exemplo, se você tiver um banco de dados com tamanho máximo de 1 TB (terabyte) e obter uma compactação de 10 vezes usando índices columnstore, você poderá colocar um total de 10 TB de dados de usuário no banco de dados.

Quando você usa os índices columnstore não clusterizado, a tabela base ainda é armazenada no formato rowstore tradicional. Portanto, a economia de armazenamento não é tão grande quanto com os índices columnstore clusterizados. No entanto, se você estiver substituindo vários índices não clusterizados tradicionais por um único índice columnstore, você ainda poderá observar uma economia geral no espaço de armazenamento da tabela.

## <a name="moving-databases-that-use-in-memory-technologies-between-pricing-tiers"></a>Movendo bancos de dados que usam tecnologias In-Memory entre tipos de preço

Nunca há incompatibilidades ou outros problemas quando você atualiza para um preço mais alto, por exemplo, do Standard para Premium. Os recursos e funcionalidades disponíveis só aumentam.

Mas o downgrade do tipo de preço pode afetar negativamente seu banco de dados. O impacto é especialmente aparente quando você faz o downgrade de Premium para Básico ou Standard quando o banco de dados contém objetos OLTP in-memory. As tabelas otimizadas para memória e índices columnstore não ficam disponíveis após o downgrade (mesmo se permanecerem visíveis). As mesmas considerações se aplicam ao reduzir o tipo de preço de um pool elástico ou ao mover um banco de dados com tecnologias In-Memory para um pool elástico Standard ou Básico.

### <a name="in-memory-oltp"></a>OLTP Na Memória

*Fazer downgrade para Básico/Standard*: não há suporte para o OLTP in-memory em bancos de dados na camada Standard ou Básico. Além disso, não é possível mover um banco de dados que tem objetos OLTP in-memory para a camada Standard ou Básico.

Antes de fazer o downgrade do banco de dados para Standard/Básico, remova todas as tabelas com otimização de memória e os tipos de tabela, bem como todos os módulos do T-SQL compilados nativamente.

Há uma maneira programática de entender se determinado banco de dados dá suporte ao OLTP in-memory. Execute a seguinte consulta Transact-SQL:

```
SELECT DatabasePropertyEx(DB_NAME(), 'IsXTPSupported');
```

Se a consulta retorna **1**, há suporte para o OLTP in-memory neste banco de dados.


*Fazer downgrade para uma camada Premium mais baixa*: os dados em tabelas com otimização de memória devem caber no armazenamento OLTP in-memory associado ao tipo de preço do banco de dados ou disponível no pool elástico. Se você tentar reduzir o tipo de preço ou mover o banco de dados para um pool que não tem armazenamento do OLTP in-memory suficiente disponível, a operação falhará.

### <a name="columnstore-indexes"></a>Índices ColumnStore

*Downgrade para Básico ou Standard*: os índices columnstore só têm suporte no tipo de preço Premium, e não nos tipos Standard ou Básico. Ao fazer o downgrade de seu banco de dados para Básico ou Standard, seu índice columnstore fica indisponível. O sistema mantém seu índice columnstore, mas nunca utiliza o índice. Se, mais tarde, você atualizar para Premium, o índice columnstore será imediatamente disponibilizado para uso novamente.

Se você tiver um índice columnstore **clusterizado**, a tabela inteira ficará indisponível após o downgrade do tipo. Portanto, recomendamos que você remova todos os índices columnstore *clusterizado* antes de fazer o downgrade de seu banco de dados abaixo do tipo Premium.

*Fazer downgrade para um tipo Premium mais baixo*: esse downgrade terá êxito se todo o banco de dados couber dentro do tamanho máximo de banco de dados para o tipo de preço de destino, ou dentro do armazenamento disponível no pool elástico. Não há nenhum impacto específico nos índices columnstore.


<a id="install_oltp_manuallink" name="install_oltp_manuallink"></a>

&nbsp;

## <a name="1-install-the-in-memory-oltp-sample"></a>1. Instalar o exemplo de OLTP Na Memória.

Você pode criar o banco de dados de exemplo AdventureWorksLT com alguns cliques no [Portal do Azure](https://portal.azure.com/). Em seguida, as etapas desta seção explicam como você pode aprimorar seu banco de dados AdventureWorksLT com objetos OLTP in-memory e demonstram os benefícios de desempenho.

Para ver uma demonstração de desempenho mais simples, porém, mais visualmente interessante do OLTP in-memory, veja:

- Versão: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)
- Código-fonte: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)

#### <a name="installation-steps"></a>Etapas de instalação

1. No [Portal do Azure](https://portal.azure.com/), crie um banco de dados Premium em um servidor. Defina a **Origem** como o banco de dados de exemplo AdventureWorksLT. Para obter instruções detalhadas, consulte [Criar seu primeiro Banco de Dados SQL do Azure](sql-database-get-started-portal.md).

2. Conecte-se ao banco de dados com o SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).

3. Copie o [script Transact-SQL do OLTP Na Memória](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) para a área de transferência. O script T-SQL cria os objetos necessários In-Memory no banco de dados de exemplo AdventureWorksLT criado na etapa 1.

4. Cole o script T-SQL no SSMS e execute o script. As instruções CREATE TABLE da cláusula `MEMORY_OPTIMIZED = ON` são cruciais. Por exemplo:


```
CREATE TABLE [SalesLT].[SalesOrderHeader_inmem](
    [SalesOrderID] int IDENTITY NOT NULL PRIMARY KEY NONCLUSTERED ...,
    ...
) WITH (MEMORY_OPTIMIZED = ON);
```


#### <a name="error-40536"></a>Erro 40536


Se você receber o erro 40536 quando executar o script T-SQL, execute o seguinte script T-SQL para verificar se o banco de dados oferece suporte a Na Memória:


```
SELECT DatabasePropertyEx(DB_Name(), 'IsXTPSupported');
```


Um resultado **0** significa que não há suporte para In-Memory e **1** significa que há suporte. Para diagnosticar o problema, verifique se o banco de dados está na camada de serviço Premium.


#### <a name="about-the-created-memory-optimized-items"></a>Sobre os itens criados com otimização de memória

**Tabelas**: o exemplo contém as seguintes tabelas com otimização de memória:

- SalesLT.Product_inmem
- SalesLT.SalesOrderHeader_inmem
- SalesLT.SalesOrderDetail_inmem
- Demo.DemoSalesOrderHeaderSeed
- Demo.DemoSalesOrderDetailSeed


Você pode inspecionar as tabelas com otimização de memória por meio do **Pesquisador de Objetos** no SSMS. Clique com o botão direito do mouse em **Tabelas** > **Filtro** > **Configurações do Filtro** > **Com otimização de memória**. O valor é igual a 1.


Ou então, você pode consultar as exibições do catálogo, tal como:


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

### <a name="run-the-sample-oltp-workload"></a>Executar a carga de trabalho OLTP

A única diferença entre os dois *procedimentos armazenados* a seguir é que o primeiro procedimento usa versões com otimização de memória das tabelas, enquanto o segundo procedimento usa as tabelas em disco regulares:

- SalesLT**.**usp_InsertSalesOrder**_inmem**
- SalesLT**.**usp_InsertSalesOrder**_ondisk**


Nesta seção, você verá como usar o utilitário **ostress.exe** para executar os dois procedimentos armazenados em níveis estressantes. Você pode comparar quanto tempo as duas execuções demoram para serem concluídas.


Quando executar ostress.exe, recomendamos será passar valores de parâmetro projetados para ambos os seguintes:

- Execute um grande número de conexões simultâneas usando -n100.
- Faça com que cada conexão entre em loop centenas de vezes usando -r500.


No entanto, talvez você queira começar com valores muito menores, como -n10 e -r50 para garantir que tudo esteja funcionando.


### <a name="script-for-ostressexe"></a>Script para ostress.exe


Esta seção exibe o script T-SQL, que está inserido em nossa linha de comando do ostress.exe. O script usa itens que foram criados pelo script T-SQL instalado anteriormente.


O script a seguir insere um pedido de vendas de exemplo com cinco itens de linha nas seguintes *tabelas*com otimização de memória:

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


Para criar a versão *_ondisk* do script T-SQL anterior para ostress.exe, substitua as duas ocorrências da subcadeia de caracteres *_inmem* por *_ondisk*. Essas substituições afetam os nomes de tabelas e os procedimentos armazenados.


### <a name="install-rml-utilities-and-ostress"></a>Instalar utilitários RML e o ostress


O ideal é você planejar executar o ostress.exe em uma VM (máquina virtual) do Azure. Você criaria uma [VM do Azure](https://azure.microsoft.com/documentation/services/virtual-machines/) na mesma região geográfica do Azure em que seu banco de dados AdventureWorksLT reside. Mas você pode executar o ostress.exe em seu laptop.


Na VM ou em qualquer host que você escolher, instale os utilitários RML (Replay Markup Language). Os utilitários incluem ostress.exe.

Para obter mais informações, consulte:
- A discussão sobre ostress.exe no [Banco de dados de exemplo para OLTP In-Memory](http://msdn.microsoft.com/library/mt465764.aspx).
- [Banco de dados de exemplo para OLTP In-Memory](http://msdn.microsoft.com/library/mt465764.aspx).
- O [blog para instalar o ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).



<!--
dn511655.aspx is for SQL 2014,
[Extensions to AdventureWorks to Demonstrate In-Memory OLTP]
(http://msdn.microsoft.com/library/dn511655&#x28;v=sql.120&#x29;.aspx)

whereas for SQL 2016+
[Sample Database for In-Memory OLTP]
(http://msdn.microsoft.com/library/mt465764.aspx)
-->



### <a name="run-the-inmem-stress-workload-first"></a>Executar a carga de trabalho de estresse do *_inmem* primeiro


Você pode usar uma janela *Prompt Cmd RML* para executar nossa linha de comando do ostress.exe. Os parâmetros de linha de comando direcionam o ostress para:

- Execute 100 conexões simultaneamente (-n100).
- Faça cada conexão executar o script T-SQL 50 vezes (-r50).


```
ostress.exe -n100 -r50 -S<servername>.database.windows.net -U<login> -P<password> -d<database> -q -Q"DECLARE @i int = 0, @od SalesLT.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand()* 10000; INSERT INTO @od SELECT OrderQty, ProductID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*60) as int); WHILE (@i < 20) begin; EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od; set @i += 1; end"
```


Para executar a linha de comando do ostress.exe anterior:


1. Redefina o conteúdo de dados do banco de dados executando o seguinte comando no SSMS para excluir todos os dados inseridos por todas as execuções anteriores:

    ``` tsql
    EXECUTE Demo.usp_DemoReset;
    ```

2. Copie o texto da linha de comando anterior do ostress.exe para a área de transferência.

3. Substitua o `<placeholders>` para os parâmetros -S -U -P -d pelos valores reais corretos.

4. Execute a linha de comando editada em uma janela Cmd RML.


#### <a name="result-is-a-duration"></a>O resultado é uma duração


Quando o ostress.exe é concluído, ele grava a duração da execução como sua linha final de saída na janela Cmd RML. Por exemplo, uma execução de teste mais curta dura aproximadamente 1,5 minuto:

`11/12/15 00:35:00.873 [0x000030A8] OSTRESS exiting normally, elapsed time: 00:01:31.867`


#### <a name="reset-edit-for-ondisk-then-rerun"></a>Redefinir, editar *_ondisk* e executar novamente


Depois de obter o resultado da execução do *_inmem*, realize as seguintes etapas para a execução de *_ondisk*:


1. Redefina o banco de dados executando o seguinte comando no SSMS para excluir todos os dados inseridos pela execução anterior:
```
EXECUTE Demo.usp_DemoReset;
```

2. Edite a linha de comando do ostress.exe para substituir todos os *_inmem* por *_ondisk*.

3. Execute novamente o ostress.exe pela segunda vez e capture o resultado da duração.

4. Redefina novamente o banco de dados (para exclusão responsável do que pode ser uma grande quantidade de dados de teste).


#### <a name="expected-comparison-results"></a>Resultados esperados para a comparação

Os testes In-Memory mostraram uma melhoria de desempenho de **nove vezes** para essa carga de trabalho simplista, com o ostress sendo executado em uma VM do Azure na mesma região do Azure que o banco de dados.

<a id="install_analytics_manuallink" name="install_analytics_manuallink"></a>

&nbsp;

## <a name="2-install-the-in-memory-analytics-sample"></a>2. Instalar o exemplo de Análise Na Memória


Nesta seção, você vai comparar os resultados de E/S e de estatísticas ao usar um índice columnstore versus um índice b-tree tradicional.


Para fazer uma análise em tempo real em uma carga de trabalho OLTP, quase sempre será melhor usar um índice columnstore não clusterizado. Para ver mais detalhes, confira [Índices Columnstore Descritos](http://msdn.microsoft.com/library/gg492088.aspx).



### <a name="prepare-the-columnstore-analytics-test"></a>Preparar o teste de análise de columnstore


1. Use o portal do Azure para criar um novo banco de dados AdventureWorksLT desde o exemplo.
 - Use esse nome exato.
 - Escolha qualquer camada de serviço Premium.

2. Copie o [sql_in-memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) para sua área de transferência.
 - O script T-SQL cria os objetos necessários In-Memory no banco de dados de exemplo AdventureWorksLT criado na etapa 1.
 - O script cria a tabela Dimension e duas tabelas de fatos. As tabelas de fatos são preenchidas com 3,5 milhões de linhas cada.
 - O script pode levar 15 minutos para ser concluído.

3. Cole o script T-SQL no SSMS e execute o script. A palavra-chave **COLUMNSTORE** na instrução **CREATE INDEX** é crucial, como em:<br/>`CREATE NONCLUSTERED COLUMNSTORE INDEX ...;`

4. Defina o AdventureWorksLT com um nível de compatibilidade 130:<br/>`ALTER DATABASE AdventureworksLT SET compatibility_level = 130;`

    O nível 130 não está diretamente relacionado aos recursos Na Memória. Mas o nível 130 geralmente oferece desempenho de consulta mais rápido que o 120.


#### <a name="key-tables-and-columnstore-indexes"></a>Tabelas chave e índices de columnstore


- dbo.FactResellerSalesXL_CCI é uma tabela com um índice columnstore clusterizado, que tem compactação avançada no nível de *dados*.

- dbo.FactResellerSalesXL_PageCompressed é uma tabela com um índice clusterizado regular equivalente, compactado somente no nível de *página*.


#### <a name="key-queries-to-compare-the-columnstore-index"></a>Consultas chave para comparar o índice columnstore


Há [diversos tipos de consulta T-SQL que podem ser executados](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) para ver as melhorias de desempenho. Na etapa 2 no script T-SQL, preste atenção neste par de consultas. Elas diferem apenas em uma linha:


- `FROM FactResellerSalesXL_PageCompressed a`
- `FROM FactResellerSalesXL_CCI a`


Um índice columnstore clusterizado está na tabela FactResellerSalesXL\_CCI.

O seguinte trecho de script T-SQL imprime estatísticas de E/S e de TIME para a consulta de cada tabela.


```
/*********************************************************************
Step 2 -- Overview
-- Page Compressed BTree table v/s Columnstore table performance differences
-- Enable actual Query Plan in order to see Plan differences when Executing
*/
-- Ensure Database is in 130 compatibility mode
ALTER DATABASE AdventureworksLT SET compatibility_level = 130
GO

-- Execute a typical query that joins the Fact Table with dimension tables
-- Note this query will run on the Page Compressed table, Note down the time
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


-- This is the same Prior query on a table with a clustered columnstore index CCI
-- The comparison numbers are even more dramatic the larger the table is (this is an 11 million row table only)
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

Em um banco de dados com o tipo de preço P2, você pode esperar um ganho de desempenho de cerca de nove vezes para essa consulta usando o índice columnstore clusterizado em comparação com o índice tradicional. Com P15, você pode esperar cerca de 57 vezes o ganho de desempenho ao usar o índice columnstore.



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
