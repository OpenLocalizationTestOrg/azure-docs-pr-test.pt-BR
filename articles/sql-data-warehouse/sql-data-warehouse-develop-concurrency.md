---
title: gerenciamento de aaaConcurrency e carga de trabalho no SQL Data Warehouse | Microsoft Docs
description: "Compreender o gerenciamento de simultaneidade e carga de trabalho no SQL Data Warehouse do Azure para desenvolvimento de soluções."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 08/23/2017
ms.author: joeyong;barbkess;kavithaj
ms.openlocfilehash: 7f7e77aa687760252aed16573b609817ed9111c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="concurrency-and-workload-management-in-sql-data-warehouse"></a>Gerenciamento de simultaneidade e carga de trabalho no SQL Data Warehouse
um desempenho previsível em grande escala, Microsoft Azure SQL Data Warehouse toodeliver ajuda a controlar os níveis de simultaneidade e alocações de recursos como priorização de CPU e memória. Este artigo apresenta os conceitos de toohello de gerenciamento de simultaneidade e a carga de trabalho, explicando como ambos os recursos foram implementados e como você pode controlá-los no data warehouse. Gerenciamento de carga de trabalho do SQL Data Warehouse é pretendido toohelp você oferece suporte a ambientes de vários usuários. Ele não se destina a cargas de trabalho com vários locatários.

## <a name="concurrency-limits"></a>Limites de simultaneidade
SQL Data Warehouse permite que até too1, 024 conexões simultâneas. Todas as 1.024 conexões podem enviar consultas ao mesmo tempo. No entanto, taxa de transferência toooptimize, SQL Data Warehouse pode enfileirar tooensure algumas consultas que cada consulta recebe uma concessão de memória mínima. O enfileiramento ocorre no tempo de execução de consulta. Por consultas de enfileiramento de mensagens quando simultaneidade limites são atingidos, o SQL Data Warehouse pode aumentar a taxa de transferência total, garantindo que consultas ativas obtenham acesso toocritically necessários recursos de memória.  

Os limites de simultaneidade são regidos por dois conceitos: *consultas simultâneas* e *slots de simultaneidade*. Para tooexecute uma consulta, ele deve executar dentro do limite de simultaneidade de consultas hello e alocação de slot de simultaneidade hello.

* Consultas simultâneas são consultas de saudação em execução a saudação mesmo tempo. SQL Data Warehouse dá suporte para até too32 de consultas simultâneas em Olá DWU maiores.
* Os slots de simultaneidade são alocados com base em DWU. Cada DWU 100 fornece quatro slots de simultaneidade. Por exemplo, um DW100 aloca quatro slots de simultaneidade e um DW1000 aloca 40. Cada consulta consome um ou mais simultaneidade slots, dependentes Olá [classe de recurso](#resource-classes) de consulta de saudação. Consultas em execução na classe de recurso de smallrc Olá consumam um slot de simultaneidade. As consultas em execução em uma classe de recurso superior consomem mais slots de simultaneidade.

Olá tabela a seguir descreve limites Olá para consultas simultâneas e slots de simultaneidade em Olá vários tamanhos DWU.

### <a name="concurrency-limits"></a>Limites de simultaneidade
| DWU | Máximo de consultas simultâneas | Slots de simultaneidade alocados |
|:--- |:---:|:---:|
| DW100 |4 |4 |
| DW200 |8 |8 |
| DW300 |12 |12 |
| DW400 |16 |16 |
| DW500 |20 |20 |
| DW600 |24 |24 |
| DW1000 |32 |40 |
| DW1200 |32 |48 |
| DW1500 |32 |60 |
| DW2000 |32 |80 |
| DW3000 |32 |120 |
| DW6000 |32 |240 |

Quando um desses limites for atingido, novas consultas serão enfileiradas e executadas em uma base de primeira a entrar, primeira a sair.  Como um consultas for concluído e número de saudação de consultas e slots cai abaixo limites hello, consultas em fila são liberadas. 

> [!NOTE]  
> *Selecione* consultas executando exclusivamente em exibições de gerenciamento dinâmico (DMVs) ou exibições do catálogo não são regidas por qualquer um dos limites de simultaneidade hello. Você pode monitorar o sistema hello, independentemente do número de saudação de consultas em execução nele.
> 
> 

## <a name="resource-classes"></a>Classes de recursos
Classes de recursos ajudam a controlar dado consulta de tooa de ciclos de CPU e alocação de memória. Você pode atribuir dois tipos de usuário de tooa de classes de recurso na forma de saudação de funções de banco de dados. Olá dois tipos de classes de recurso são da seguinte maneira:
1. Classes de recursos dinâmicos (**smallrc, mediumrc, largerc, xlargerc**) alocar uma variável quantidade de memória dependendo Olá DWU atual. Isso significa que, quando você escala verticalmente tooa DWU maior, suas consultas obtém automaticamente mais memória. 
2. Classes de recursos estáticos (**staticrc10, staticrc20, staticrc30, staticrc40, staticrc50, staticrc60, staticrc70, staticrc80**) alocar Olá Olá a mesma quantidade de memória, independentemente do DWU atual (desde que Olá DWU em si tem memória suficiente). Isso significa que em DWUs maiores, você pode executar mais consultas em cada classe de recursos simultaneamente.

Os usuários em **smallrc** e **staticrc10** recebem uma quantidade menor de memória e podem tirar proveito da simultaneidade superior. Em contraste, os usuários atribuídos muito**xlargerc** ou **staticrc80** recebem grandes quantidades de memória, e, portanto, menos suas consultas podem ser executados simultaneamente.

Por padrão, cada usuário é um membro da classe do recurso pequeno hello, **smallrc**. Olá procedimento `sp_addrolemember` é usado a classe de recurso tooincrease hello e `sp_droprolemember` é usada a classe de recurso de saudação toodecrease. Por exemplo, este comando poderia aumentar a classe de recurso de saudação do loaduser muito**largerc**:

```sql
EXEC sp_addrolemember 'largerc', 'loaduser'
```


### <a name="queries-that-do-not-honor-resource-classes"></a>Consultas que não consideram classes de recursos

Existem alguns tipos de consultas que não se beneficiam de uma alocação de memória maior. sistema Olá ignora a alocação de classe de recurso e sempre executa essas consultas na classe de recursos pequeno Olá em vez disso. Se essas consultas sempre em execução na classe de recursos pequeno hello, eles podem executar quando os slots de simultaneidade estão sob pressão e não consomem mais slots que o necessário. Consulte as [exceções de classe de recurso](#query-exceptions-to-concurrency-limits) para obter mais informações.

## <a name="details-on-resource-class-assignment"></a>Detalhes sobre a atribuição de classe de recursos


Mais alguns detalhes sobre classes de recurso:

* *Alterar função* é necessária a permissão toochange classe de recurso de saudação de um usuário.
* Embora você pode adicionar um usuário tooone ou mais classes superiores de recurso Olá, classes de recursos dinâmicos têm precedência sobre classes de recursos estáticos. Ou seja, se um usuário é atribuído tooboth **mediumrc**(dinâmico) e **staticrc80**(estático), **mediumrc** é a classe de recurso de saudação que é cumprido.
 * Quando um usuário é atribuído toomore que a classe de um recurso em um tipo de classe de recurso específico (mais de uma classe de recurso dinâmico ou mais de uma classe de recurso estático), a classe de recurso hello mais alto é cumprido. Ou seja, se um usuário é atribuído largerc e tooboth mediumrc, classe de recurso superior hello (largerc) é cumprido. E se um usuário é atribuído tooboth **staticrc20** e **statirc80**, **staticrc80** é respeitada.
* classe de recurso de saudação do usuário administrativo do sistema Olá não pode ser alterado.

Para obter um exemplo detalhado, consulte [Alterando o exemplo de classe de recurso de usuário](#changing-user-resource-class-example).

## <a name="memory-allocation"></a>Alocação de memória
Há prós e contras tooincreasing classe de recurso do usuário. Aumentando a uma classe de recurso para um usuário, fornece suas consultas de memória toomore, que pode significar que executar consultas mais rapidamente.  No entanto, o classes superiores de recurso também reduzem o número de saudação de consultas simultâneas que podem ser executados. Essa é a compensação de saudação entre a alocação de grandes quantidades de consulta única de tooa de memória ou permitindo que outras consultas, que também precisam de alocações de memória, toorun simultaneamente. Se um usuário receber alta alocações de memória para uma consulta, outros usuários não terão acesso toothat mesmo memória toorun uma consulta.

Olá, a tabela a seguir mapeia memória Olá alocada distribuição tooeach pela classe DWU e recursos.

### <a name="memory-allocations-per-distribution-for-dynamic-resource-classes-mb"></a>Alocações de memória por distribuição de classes de recursos dinâmicos (MB)
| DWU | smallrc | mediumrc | largerc | xlargerc |
|:--- |:---:|:---:|:---:|:---:|
| DW100 |100 |100 |200 |400 |
| DW200 |100 |200 |400 |800 |
| DW300 |100 |200 |400 |800 |
| DW400 |100 |400 |800 |1.600 |
| DW500 |100 |400 |800 |1.600 |
| DW600 |100 |400 |800 |1.600 |
| DW1000 |100 |800 |1.600 |3.200 |
| DW1200 |100 |800 |1.600 |3.200 |
| DW1500 |100 |800 |1.600 |3.200 |
| DW2000 |100 |1.600 |3.200 |6.400 |
| DW3000 |100 |1.600 |3.200 |6.400 |
| DW6000 |100 |3.200 |6.400 |12.800 |

Olá, a tabela a seguir mapeia memória Olá alocada distribuição tooeach por DWU e classe de recurso estático. Observe que as classes superiores de recurso Olá tem sua memória reduzido limites DWU toohonor Olá global.

### <a name="memory-allocations-per-distribution-for-static-resource-classes-mb"></a>Alocações de memória por distribuição de classes de recursos estáticos (MB)
| DWU | staticrc10 | staticrc20 | staticrc30 | staticrc40 | staticrc50 | staticrc60 | staticrc70 | staticrc80 |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DW100 |100 |200 |400 |400 |400 |400 |400 |400 |
| DW200 |100 |200 |400 |800 |800 |800 |800 |800 |
| DW300 |100 |200 |400 |800 |800 |800 |800 |800 |
| DW400 |100 |200 |400 |800 |1.600 |1.600 |1.600 |1.600 |
| DW500 |100 |200 |400 |800 |1.600 |1.600 |1.600 |1.600 |
| DW600 |100 |200 |400 |800 |1.600 |1.600 |1.600 |1.600 |
| DW1000 |100 |200 |400 |800 |1.600 |3.200 |3.200 |3.200 |
| DW1200 |100 |200 |400 |800 |1.600 |3.200 |3.200 |3.200 |
| DW1500 |100 |200 |400 |800 |1.600 |3.200 |3.200 |3.200 |
| DW2000 |100 |200 |400 |800 |1.600 |3.200 |6.400 |6.400 |
| DW3000 |100 |200 |400 |800 |1.600 |3.200 |6.400 |6.400 |
| DW6000 |100 |200 |400 |800 |1.600 |3.200 |6.400 |12.800 |

Olá anterior da tabela, você pode ver que uma consulta em execução em um DW2000 no hello **xlargerc** classe de recurso teria acesso too6, 400 MB de memória em cada banco de dados distribuído 60 de saudação.  Há 60 distribuições no SQL Data Warehouse. Portanto, alocação de memória total toocalculate Olá para uma consulta em uma classe de recurso fornecido, Olá acima valores deve ser multiplicada por 60.

### <a name="memory-allocations-system-wide-gb"></a>Alocações de memória em todo o sistema (GB)
| DWU | smallrc | mediumrc | largerc | xlargerc |
|:--- |:---:|:---:|:---:|:---:|
| DW100 |6 |6 |12 |23 |
| DW200 |6 |12 |23 |47 |
| DW300 |6 |12 |23 |47 |
| DW400 |6 |23 |47 |94 |
| DW500 |6 |23 |47 |94 |
| DW600 |6 |23 |47 |94 |
| DW1000 |6 |47 |94 |188 |
| DW1200 |6 |47 |94 |188 |
| DW1500 |6 |47 |94 |188 |
| DW2000 |6 |94 |188 |375 |
| DW3000 |6 |94 |188 |375 |
| DW6000 |6 |188 |375 |750 |

Essa tabela de alocações de memória do sistema, você pode ver que uma consulta em execução em um DW2000 na classe de recurso de xlargerc Olá é alocada um total de 375 GB de memória (distribuições 6.400 MB * 60 / 1.024 tooconvert tooGB) sobre a totalidade saudação do Data Warehouse do SQL.

Olá mesmo cálculo se aplica toostatic classes de recursos.
 
## <a name="concurrency-slot-consumption"></a>Consumo de slot de simultaneidade  
SQL Data Warehouse concede mais tooqueries de memória em execução em classes superiores de recurso. A memória é um recurso fixo.  Portanto, hello mais memória alocada por consulta, Olá menos consultas simultâneas podem executar. Olá tabela a seguir reitera todos os conceitos de saudação anterior em uma única exibição que mostra o número de saudação de slots de simultaneidade disponíveis por DWU e slots de saudação consumidos por cada classe de recurso.  

### <a name="allocation-and-consumption-of-concurrency-slots-for-dynamic-resource-classes"></a>Alocação e consumo de slots de simultaneidade para classes de recursos dinâmicos  
| DWU | Máximo de consultas simultâneas | Slots de simultaneidade alocados | Slots usados pelo smallrc | Slots usados pelo mediumrc | Slots usados pelo largerc | Slots usados pelo xlargerc |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|
| DW100 |4 |4 |1 |1 |2 |4 |
| DW200 |8 |8 |1 |2 |4 |8 |
| DW300 |12 |12 |1 |2 |4 |8 |
| DW400 |16 |16 |1 |4 |8 |16 |
| DW500 |20 |20 |1 |4 |8 |16 |
| DW600 |24 |24 |1 |4 |8 |16 |
| DW1000 |32 |40 |1 |8 |16 |32 |
| DW1200 |32 |48 |1 |8 |16 |32 |
| DW1500 |32 |60 |1 |8 |16 |32 |
| DW2000 |32 |80 |1 |16 |32 |64 |
| DW3000 |32 |120 |1 |16 |32 |64 |
| DW6000 |32 |240 |1 |32 |64 |128 |

### <a name="allocation-and-consumption-of-concurrency-slots-for-static-resource-classes"></a>Alocação e consumo de slots de simultaneidade para classes de recursos estáticos  
| DWU | Máximo de consultas simultâneas | Slots de simultaneidade alocados |staticrc10 | staticrc20 | staticrc30 | staticrc40 | staticrc50 | staticrc60 | staticrc70 | staticrc80 |
|:--- |:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| DW100 |4 |4 |1 |2 |4 |4 |4 |4 |4 |4 |
| DW200 |8 |8 |1 |2 |4 |8 |8 |8 |8 |8 |
| DW300 |12 |12 |1 |2 |4 |8 |8 |8 |8 |8 |
| DW400 |16 |16 |1 |2 |4 |8 |16 |16 |16 |16 |
| DW500 | 20| 20| 1| 2| 4| 8| 16| 16| 16| 16|
| DW600 | 24| 24| 1| 2| 4| 8| 16| 16| 16| 16|
| DW1000 | 32| 40| 1| 2| 4| 8| 16| 32| 32| 32|
| DW1200 | 32| 48| 1| 2| 4| 8| 16| 32| 32| 32|
| DW1500 | 32| 60| 1| 2| 4| 8| 16| 32| 32| 32|
| DW2000 | 32| 80| 1| 2| 4| 8| 16| 32| 64| 64|
| DW3000 | 32| 120| 1| 2| 4| 8| 16| 32| 64| 64|
| DW6000 | 32| 240| 1| 2| 4| 8| 16| 32| 64| 128|

Nestas tabelas, você pode ver que um SQL Data Warehouse em execução como DW1000 aloca uma quantidade máxima de 32 consultas simultâneas e um total de 40 slots de simultaneidade. Se todos os usuários estivessem em execução no smallrc, seriam permitidas 32 consultas simultâneas, pois cada consulta consumiria um slot de simultaneidade. Se todos os usuários em um DW1000 estavam em execução no mediumrc, cada consulta seria alocada 800 MB por distribuição de uma alocação de memória total de 47 GB por consulta, simultaneidade seria too5 limitado de usuários (40 slots de simultaneidade slots de 8 por usuário mediumrc /).

## <a name="selecting-proper-resource-class"></a>Selecionando a classe de recursos apropriada  
Uma prática recomendada é a classe de recurso do toopermanently atribuir usuários tooa em vez de alterar suas classes de recursos. Por exemplo, tabelas de columnstore cargas tooclustered criam índices de alta qualidade quando mais memória alocada. tooensure que carrega tem acesso toohigher memória, cria um usuário especificamente para carregar dados e atribui permanentemente esta classe de recursos do usuário tooa superior.
Há algumas toofollow práticas recomendada aqui. Como mencionado acima, o SQL DW dá suporte a dois tipos de classes de recursos: classes de recursos estáticos e classes de recursos dinâmicos.
### <a name="loading-best-practices"></a>Melhores práticas de carregamento
1.  Se as expectativas de saudação carrega com quantidade regular de dados, uma classe de recurso estático é uma boa opção. Posteriormente, quando o dimensionamento das tooget mais potência computacional, data warehouse de saudação será capaz de toorun simultâneo mais consultas out-of-the-box, como usuário de carga Olá não consome mais memória.
2.  Se as expectativas de saudação maiores cargas em algumas ocasiões, uma classe de recurso dinâmico é uma boa opção. Posteriormente, quando o dimensionamento das tooget mais potência computacional, Olá carga usuário receberá mais memória out-of-the-box, permitindo, portanto, Olá carga tooperform mais rapidamente.

Olá memória necessária tooprocess cargas com eficiência depende Olá natureza da tabela de saudação carregada e quantidade de saudação de dados processados. Por exemplo, carregar dados em tabelas CCI requer que algumas rowgroups CCI toolet memória alcançar ideais. Para obter mais detalhes, consulte índices de Columnstore Olá - diretrizes de carregamento de dados.

Como prática recomendada, aconselhamos que você toouse pelo menos 200MB de memória para cargas.

### <a name="querying-best-practices"></a>Melhores práticas de consulta
As consultas têm requisitos diferentes dependendo de sua complexidade. Aumentar a memória por consulta ou aumentar a simultaneidade de saudação são ambas as maneiras válidas tooaugment produtividade geral dependendo das necessidades de consulta hello.
1.  Se expectativas Olá são consultas complexas, regulares (toogenerate, por exemplo, relatórios de diários e semanais) e não é necessário tootake vantagem de simultaneidade, uma classe de recurso dinâmico é uma boa opção. Se o sistema Olá tem mais tooprocess de dados, expansão do data warehouse de saudação, portanto, fornecerá automaticamente usuário de toohello mais memória execução de consulta de saudação.
2.  Se as expectativas de saudação são padrões de simultaneidade diurnal ou variável (por exemplo se o banco de dados de saudação é consultado por meio de uma interface amplamente acessível da web), uma classe de recurso estático é uma boa opção. Posteriormente, ao aumento toodata warehouse, usuário Olá associado à classe de recurso estático hello serão automaticamente ser capaz de toorun consultas mais simultâneas.

Selecionando concessão de memória apropriada dependendo da necessidade de saudação da consulta é incomum, pois ele depende de muitos fatores, como quantidade de saudação de dados consultados, natureza Olá esquemas de tabela hello e vários junção, seleção e predicados de grupo. Alocar mais memória permitirá consultas toocomplete mais rápido do ponto de vista geral, mas reduziria Olá simultaneidade geral. Se a simultaneidade não for um problema, a alocação excessiva de memória não será prejudicial. taxa de transferência toofine ajustar, tentativa de vários tipos de classes de recursos pode ser necessária.

Você pode usar o seguinte Olá armazenados procedimento toofigure limite de concessão de memória e simultaneidade por classe de recurso a uma determinada SLO e hello mais próximo melhor recurso classe para memória intensiva CCI operações de tabela CCI não particionada em uma classe de recurso específico:

#### <a name="description"></a>Descrição:  
Aqui está a finalidade de saudação deste procedimento armazenado:  
1. toohelp usuário descobrir concessão de memória e simultaneidade por classe de recurso em um determinado SLO. Usuário precisa tooprovide NULL para o esquema e tablename isso conforme mostrado no exemplo hello abaixo.  
2. usuário toohelp descobrir hello mais próxima melhor classe de recurso para Olá memória intensed operações CCI (carga de tabela de cópia, recriar o índice, etc.) em uma tabela CCI não particionada em uma classe de recurso específico. Olá armazenado proc usa toofind de esquema de tabela out Olá concessão de memória necessária para isso.

#### <a name="dependencies--restrictions"></a>Dependências e restrições:
- Esse procedimento armazenado não é um requisito de memória toocalculate projetado para a tabela particionada cci.    
- Esse procedimento armazenado não tem um requisito de memória em consideração para a parte SELECT Olá de inserção/CTAS-SELECT e pressupõe que ele toobe SELECT simples.
- Esse procedimento armazenado usa uma tabela temporária para que isso pode ser usado na sessão Olá onde esse procedimento armazenado foi criado.    
- Esse procedimento armazenado depende de ofertas de saudação atual (por exemplo, a configuração de hardware, a configuração DMS) e se qualquer um dos que for alterado, em seguida, esse procedimento armazenado não funcionará corretamente.  
- Esse procedimento armazenado depende do limite de simultaneidade oferecidos existente e se isso mudar, o procedimento armazenado não funcionará corretamente.  
- Esse procedimento armazenado depende das ofertas de classe de recursos existentes e se isso mudar, o procedimento armazenado não funcionará corretamente.  

>  [!NOTE]  
>  Se nenhuma saída aparecer após a execução do procedimento armazenado com parâmetros fornecidos, isso poderá ser consequência de dois problemas. <br />1. Um parâmetro de DW contém o valor inválido de SLO <br />2. OU não há nenhuma classe de recurso correspondente para a operação CCI se o nome de tabela tiver sido fornecido. <br />Por exemplo, em DW100, concessão de memória mais alto disponível é de 400MB e se o esquema de tabela for grande o suficiente toocross Olá requisito de 400MB.
      
#### <a name="usage-example"></a>Exemplo de uso:
Sintaxe:  
`EXEC dbo.prc_workload_management_by_DWU @DWU VARCHAR(7), @SCHEMA_NAME VARCHAR(128), @TABLE_NAME VARCHAR(128)`  
1. @DWU:Forneça um tooextract de parâmetro NULL Olá DWU atual do BD de DW do hello ou fornecer qualquer suporte DWU na forma de saudação de 'DW100'
2. @SCHEMA_NAME:Forneça um nome de esquema da tabela de saudação
3. @TABLE_NAME:Forneça um nome de tabela de interesse Olá

Exemplos executando esse procedimento armazenado:  
```sql  
EXEC dbo.prc_workload_management_by_DWU 'DW2000', 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU NULL, 'dbo', 'Table1';  
EXEC dbo.prc_workload_management_by_DWU 'DW6000', NULL, NULL;  
EXEC dbo.prc_workload_management_by_DWU NULL, NULL, NULL;  
```

Table1 usado em Olá acima exemplos pôde ser criado como abaixo:  
`CREATE TABLE Table1 (a int, b varchar(50), c decimal (18,10), d char(10), e varbinary(15), f float, g datetime, h date);`

#### <a name="heres-hello-stored-procedure-definition"></a>Aqui está a definição do procedimento armazenada de saudação:
```sql  
-------------------------------------------------------------------------------
-- Dropping prc_workload_management_by_DWU procedure if it exists.
-------------------------------------------------------------------------------
IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'prc_workload_management_by_DWU')
DROP PROCEDURE dbo.prc_workload_management_by_DWU
GO

-------------------------------------------------------------------------------
-- Creating prc_workload_management_by_DWU.
-------------------------------------------------------------------------------
CREATE PROCEDURE dbo.prc_workload_management_by_DWU
(   @DWU VARCHAR(7),
      @SCHEMA_NAME VARCHAR(128),
       @TABLE_NAME VARCHAR(128)
)
AS
IF @DWU IS NULL
BEGIN
-- Selecting proper DWU for hello current DB if not specified.
SET @DWU = (
  SELECT 'DW'+CAST(COUNT(*)*100 AS VARCHAR(10))
  FROM sys.dm_pdw_nodes
  WHERE type = 'COMPUTE')
END

DECLARE @DWU_NUM INT
SET @DWU_NUM = CAST (SUBSTRING(@DWU, 3, LEN(@DWU)-2) AS INT)

-- Raise error if either schema name or table name is supplied but not both them supplied
--IF ((@SCHEMA_NAME IS NOT NULL AND @TABLE_NAME IS NULL) OR (@TABLE_NAME IS NULL AND @SCHEMA_NAME IS NOT NULL))
--     RAISEERROR('User need toosupply either both Schema Name and Table Name or none of them')
       
-- Dropping temp table if exists.
IF OBJECT_ID('tempdb..#ref') IS NOT NULL
BEGIN
  DROP TABLE #ref;
END

-- Creating ref. temptable (CTAS) toohold mapping info.
-- CREATE TABLE #ref
CREATE TABLE #ref
WITH (DISTRIBUTION = ROUND_ROBIN)
AS 
WITH
-- Creating concurrency slots mapping for various DWUs.
alloc
AS
(
  SELECT 'DW100' AS DWU, 4 AS max_queries, 4 AS max_slots, 1 AS slots_used_smallrc, 1 AS slots_used_mediumrc,
        2 AS slots_used_largerc, 4 AS slots_used_xlargerc, 1 AS slots_used_staticrc10, 2 AS slots_used_staticrc20,
        4 AS slots_used_staticrc30, 4 AS slots_used_staticrc40, 4 AS slots_used_staticrc50,
        4 AS slots_used_staticrc60, 4 AS slots_used_staticrc70, 4 AS slots_used_staticrc80
  UNION ALL
    SELECT 'DW200', 8, 8, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW300', 12, 12, 1, 2, 4, 8, 1, 2, 4, 8, 8, 8, 8, 8
  UNION ALL
    SELECT 'DW400', 16, 16, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
     SELECT 'DW500', 20, 20, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW600', 24, 24, 1, 4, 8, 16, 1, 2, 4, 8, 16, 16, 16, 16
  UNION ALL
    SELECT 'DW1000', 32, 40, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1200', 32, 48, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW1500', 32, 60, 1, 8, 16, 32, 1, 2, 4, 8, 16, 32, 32, 32
  UNION ALL
    SELECT 'DW2000', 32, 80, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
   SELECT 'DW3000', 32, 120, 1, 16, 32, 64, 1, 2, 4, 8, 16, 32, 64, 64
  UNION ALL
    SELECT 'DW6000', 32, 240, 1, 32, 64, 128, 1, 2, 4, 8, 16, 32, 64, 128
)
-- Creating workload mapping tootheir corresponding slot consumption and default memory grant.
,map
AS
(
  SELECT 'SloDWGroupC00' AS wg_name,1 AS slots_used,100 AS tgt_mem_grant_MB
  UNION ALL
    SELECT 'SloDWGroupC01',2,200
  UNION ALL
    SELECT 'SloDWGroupC02',4,400
  UNION ALL
    SELECT 'SloDWGroupC03',8,800
  UNION ALL
    SELECT 'SloDWGroupC04',16,1600
  UNION ALL
    SELECT 'SloDWGroupC05',32,3200
  UNION ALL
    SELECT 'SloDWGroupC06',64,6400
  UNION ALL
    SELECT 'SloDWGroupC07',128,12800
)
-- Creating ref based on current / asked DWU.
, ref
AS
(
  SELECT  a1.*
  ,       m1.wg_name          AS wg_name_smallrc
  ,       m1.tgt_mem_grant_MB AS tgt_mem_grant_MB_smallrc
  ,       m2.wg_name          AS wg_name_mediumrc
  ,       m2.tgt_mem_grant_MB AS tgt_mem_grant_MB_mediumrc
  ,       m3.wg_name          AS wg_name_largerc
  ,       m3.tgt_mem_grant_MB AS tgt_mem_grant_MB_largerc
  ,       m4.wg_name          AS wg_name_xlargerc
  ,       m4.tgt_mem_grant_MB AS tgt_mem_grant_MB_xlargerc
  ,       m5.wg_name          AS wg_name_staticrc10
  ,       m5.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc10
  ,       m6.wg_name          AS wg_name_staticrc20
  ,       m6.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc20
  ,       m7.wg_name          AS wg_name_staticrc30
  ,       m7.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc30
  ,       m8.wg_name          AS wg_name_staticrc40
  ,       m8.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc40
  ,       m9.wg_name          AS wg_name_staticrc50
  ,       m9.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc50
  ,       m10.wg_name          AS wg_name_staticrc60
  ,       m10.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc60
  ,       m11.wg_name          AS wg_name_staticrc70
  ,       m11.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc70
  ,       m12.wg_name          AS wg_name_staticrc80
  ,       m12.tgt_mem_grant_MB AS tgt_mem_grant_MB_staticrc80
  FROM alloc a1
  JOIN map   m1  ON a1.slots_used_smallrc     = m1.slots_used
  JOIN map   m2  ON a1.slots_used_mediumrc    = m2.slots_used
  JOIN map   m3  ON a1.slots_used_largerc     = m3.slots_used
  JOIN map   m4  ON a1.slots_used_xlargerc    = m4.slots_used
  JOIN map   m5  ON a1.slots_used_staticrc10    = m5.slots_used
  JOIN map   m6  ON a1.slots_used_staticrc20    = m6.slots_used
  JOIN map   m7  ON a1.slots_used_staticrc30    = m7.slots_used
  JOIN map   m8  ON a1.slots_used_staticrc40    = m8.slots_used
  JOIN map   m9  ON a1.slots_used_staticrc50    = m9.slots_used
  JOIN map   m10  ON a1.slots_used_staticrc60    = m10.slots_used
  JOIN map   m11  ON a1.slots_used_staticrc70    = m11.slots_used
  JOIN map   m12  ON a1.slots_used_staticrc80    = m12.slots_used
-- WHERE   a1.DWU = @DWU
  WHERE   a1.DWU = UPPER(@DWU)
)
SELECT  DWU
,       max_queries
,       max_slots
,       slots_used
,       wg_name
,       tgt_mem_grant_MB
,       up1 as rc
,       (ROW_NUMBER() OVER(PARTITION BY DWU ORDER BY DWU)) as rc_id
FROM
(
    SELECT  DWU
    ,       max_queries
    ,       max_slots
    ,       slots_used
    ,       wg_name
    ,       tgt_mem_grant_MB
    ,       REVERSE(SUBSTRING(REVERSE(wg_names),1,CHARINDEX('_',REVERSE(wg_names),1)-1)) as up1
    ,       REVERSE(SUBSTRING(REVERSE(tgt_mem_grant_MBs),1,CHARINDEX('_',REVERSE(tgt_mem_grant_MBs),1)-1)) as up2
    ,       REVERSE(SUBSTRING(REVERSE(slots_used_all),1,CHARINDEX('_',REVERSE(slots_used_all),1)-1)) as up3
    FROM    ref AS r1
    UNPIVOT
    (
        wg_name FOR wg_names IN (wg_name_smallrc,wg_name_mediumrc,wg_name_largerc,wg_name_xlargerc,
        wg_name_staticrc10, wg_name_staticrc20, wg_name_staticrc30, wg_name_staticrc40, wg_name_staticrc50,
        wg_name_staticrc60, wg_name_staticrc70, wg_name_staticrc80)
    ) AS r2
    UNPIVOT
    (
        tgt_mem_grant_MB FOR tgt_mem_grant_MBs IN (tgt_mem_grant_MB_smallrc,tgt_mem_grant_MB_mediumrc,
        tgt_mem_grant_MB_largerc,tgt_mem_grant_MB_xlargerc, tgt_mem_grant_MB_staticrc10, tgt_mem_grant_MB_staticrc20,
        tgt_mem_grant_MB_staticrc30, tgt_mem_grant_MB_staticrc40, tgt_mem_grant_MB_staticrc50,
        tgt_mem_grant_MB_staticrc60, tgt_mem_grant_MB_staticrc70, tgt_mem_grant_MB_staticrc80)
    ) AS r3
    UNPIVOT
    (
        slots_used FOR slots_used_all IN (slots_used_smallrc,slots_used_mediumrc,slots_used_largerc,
        slots_used_xlargerc, slots_used_staticrc10, slots_used_staticrc20, slots_used_staticrc30,
        slots_used_staticrc40, slots_used_staticrc50, slots_used_staticrc60, slots_used_staticrc70,
        slots_used_staticrc80)
    ) AS r4
) a
WHERE   up1 = up2
AND     up1 = up3
;
-- Getting current info about workload groups.
WITH  
dmv  
AS  
(
  SELECT
          rp.name                                           AS rp_name
  ,       rp.max_memory_kb*1.0/1048576                      AS rp_max_mem_GB
  ,       (rp.max_memory_kb*1.0/1024)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_MB
  ,       (rp.max_memory_kb*1.0/1048576)
          *(request_max_memory_grant_percent/100)           AS max_memory_grant_GB
  ,       wg.name                                           AS wg_name
  ,       wg.importance                                     AS importance
  ,       wg.request_max_memory_grant_percent               AS request_max_memory_grant_percent
  FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
  JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    ON  wg.pdw_node_id  = rp.pdw_node_id
                                                                  AND wg.pool_id      = rp.pool_id
  WHERE   rp.name = 'SloDWPool'
  GROUP BY
          rp.name
  ,       rp.max_memory_kb
  ,       wg.name
  ,       wg.importance
  ,       wg.request_max_memory_grant_percent
)
-- Creating resource class name mapping.
,names
AS
(
  SELECT 'smallrc' as resource_class, 1 as rc_id
  UNION ALL
    SELECT 'mediumrc', 2
  UNION ALL
    SELECT 'largerc', 3
  UNION ALL
    SELECT 'xlargerc', 4
  UNION ALL
    SELECT 'staticrc10', 5
  UNION ALL
    SELECT 'staticrc20', 6
  UNION ALL
    SELECT 'staticrc30', 7
  UNION ALL
    SELECT 'staticrc40', 8
  UNION ALL
    SELECT 'staticrc50', 9
  UNION ALL
    SELECT 'staticrc60', 10
  UNION ALL
    SELECT 'staticrc70', 11
  UNION ALL
    SELECT 'staticrc80', 12
)
,base AS
(   SELECT  schema_name
    ,       table_name
    ,       SUM(column_count)                   AS column_count
    ,       ISNULL(SUM(short_string_column_count),0)   AS short_string_column_count
    ,       ISNULL(SUM(long_string_column_count),0)    AS long_string_column_count
    FROM    (   SELECT  sm.name                                             AS schema_name
                ,       tb.name                                             AS table_name
                ,       COUNT(co.column_id)                                 AS column_count
                           ,       CASE    WHEN co.system_type_id IN (36,43,106,108,165,167,173,175,231,239) 
                                AND  co.max_length <= 32 
                                THEN COUNT(co.column_id) 
                        END                                                 AS short_string_column_count
                ,       CASE    WHEN co.system_type_id IN (165,167,173,175,231,239) 
                                AND  co.max_length > 32 and co.max_length <=8000
                                THEN COUNT(co.column_id) 
                        END                                                 AS long_string_column_count
                FROM    sys.schemas AS sm
                JOIN    sys.tables  AS tb   on sm.[schema_id] = tb.[schema_id]
                JOIN    sys.columns AS co   ON tb.[object_id] = co.[object_id]
                           WHERE tb.name = @TABLE_NAME AND sm.name = @SCHEMA_NAME
                GROUP BY sm.name
                ,        tb.name
                ,        co.system_type_id
                ,        co.max_length            ) a
GROUP BY schema_name
,        table_name
)
, size AS
(
SELECT  schema_name
,       table_name
,       75497472                                            AS table_overhead

,       column_count*1048576*8                              AS column_size
,       short_string_column_count*1048576*32                       AS short_string_size,       (long_string_column_count*16777216) AS long_string_size
FROM    base
UNION
SELECT CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as schema_name
         ,CASE WHEN COUNT(*) = 0 THEN 'EMPTY' END as table_name
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as table_overhead
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as column_size
         ,CASE WHEN COUNT(*) = 0 THEN 0 END as short_string_size

,CASE WHEN COUNT(*) = 0 THEN 0 END as long_string_size
FROM   base
)
, load_multiplier as 
(
SELECT  CASE 
                     WHEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) > 0 THEN FLOOR(8 * (CAST (@DWU_NUM AS FLOAT)/6000)) 
                     ELSE 1 
              END AS multipliplication_factor
) 
       SELECT  r1.DWU
       , schema_name
       , table_name
       , rc.resource_class as closest_rc_in_increasing_order
       , max_queries_at_this_rc = CASE
             WHEN (r1.max_slots / r1.slots_used > r1.max_queries)
                  THEN r1.max_queries
             ELSE r1.max_slots / r1.slots_used
                  END
       , r1.max_slots as max_concurrency_slots
       , r1.slots_used as required_slots_for_the_rc
       , r1.tgt_mem_grant_MB  as rc_mem_grant_MB
       , CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) AS est_mem_grant_required_for_cci_operation_MB       
       FROM    size, load_multiplier, #ref r1, names  rc
       WHERE r1.rc_id=rc.rc_id
                     AND CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) < r1.tgt_mem_grant_MB
       ORDER BY ABS(CAST((table_overhead*1.0+column_size+short_string_size+long_string_size)*multipliplication_factor/1048576    AS DECIMAL(18,2)) - r1.tgt_mem_grant_MB)
GO
```

## <a name="query-importance"></a>Importância da consulta
O SQL Data Warehouse implementa classes de recursos usando grupos de carga de trabalho. Há um total de oito grupos de cargas de trabalho que controlam o comportamento de Olá Olá de classes de recurso entre Olá vários tamanhos DWU. Para qualquer DWU SQL Data Warehouse usa apenas quatro das oito grupos de cargas de trabalho hello. Isso faz sentido porque é atribuída a cada grupo de carga de trabalho tooone de quatro classes de recursos: smallrc, mediumrc, largerc, ou xlargerc. Olá importância de Noções básicas sobre grupos de carga de trabalho de saudação é que alguns desses grupos de carga de trabalho estão definidos toohigher *importância*. A importância é usada para agendamento de CPU. As consultas executadas com importância alta obterão três vezes mais ciclos de CPU do que aquelas com importância média. Portanto, os mapeamentos de slot de simultaneidade também determinam a prioridade da CPU. Quando uma consulta consome 16 ou mais slots, ela é executada com alta importância.

Olá, tabela a seguir mostra Olá mapeamentos de importância para cada grupo de carga de trabalho.

### <a name="workload-group-mappings-tooconcurrency-slots-and-importance"></a>Importância e slots de tooconcurrency de mapeamentos de grupo de carga de trabalho
| Grupos de carga de trabalho | Mapeamento do slot de simultaneidade | MB / Distribuição | Mapeamento de importância |
|:--- |:---:|:---:|:--- |
| SloDWGroupC00 |1 |100 |Média |
| SloDWGroupC01 |2 |200 |Média |
| SloDWGroupC02 |4 |400 |Média |
| SloDWGroupC03 |8 |800 |Média |
| SloDWGroupC04 |16 |1.600 |Alto |
| SloDWGroupC05 |32 |3.200 |Alto |
| SloDWGroupC06 |64 |6.400 |Alto |
| SloDWGroupC07 |128 |12.800 |Alto |

De saudação **alocação e o consumo de slots de simultaneidade** gráfico, você pode ver que uma DW500 usa 1, 4, 8 ou slots de simultaneidade 16 para smallrc, mediumrc, largerc e xlargerc, respectivamente. Você pode procurar esses valores em Olá anterior a importância de saudação toofind gráfico para cada classe de recurso.

### <a name="dw500-mapping-of-resource-classes-tooimportance"></a>Mapeamento de DW500 de tooimportance de classes de recursos
| classe de recurso | Grupo de carga de trabalho | Slots de simultaneidade usados | MB / Distribuição | importância |
|:--- |:--- |:---:|:---:|:--- |
| smallrc |SloDWGroupC00 |1 |100 |Média |
| mediumrc |SloDWGroupC02 |4 |400 |Média |
| largerc |SloDWGroupC03 |8 |800 |Média |
| xlargerc |SloDWGroupC04 |16 |1.600 |Alto |
| staticrc10 |SloDWGroupC00 |1 |100 |Média |
| staticrc20 |SloDWGroupC01 |2 |200 |Média |
| staticrc30 |SloDWGroupC02 |4 |400 |Média |
| staticrc40 |SloDWGroupC03 |8 |800 |Média |
| staticrc50 |SloDWGroupC03 |16 |1.600 |Alto |
| staticrc60 |SloDWGroupC03 |16 |1.600 |Alto |
| staticrc70 |SloDWGroupC03 |16 |1.600 |Alto |
| staticrc80 |SloDWGroupC03 |16 |1.600 |Alto |

Você pode usar o hello toolook de consulta DMV em diferenças Olá na alocação de recursos de memória em detalhes da perspectiva de saudação do administrador de recursos de saudação ou tooanalyze ativo e históricos o uso de grupos de cargas de trabalho Olá a seguir ao solucionar o problema.

```sql
WITH rg
AS
(   SELECT  
     pn.name                        AS node_name
    ,pn.[type]                        AS node_type
    ,pn.pdw_node_id                    AS node_id
    ,rp.name                        AS pool_name
    ,rp.max_memory_kb*1.0/1024                AS pool_max_mem_MB
    ,wg.name                        AS group_name
    ,wg.importance                    AS group_importance
    ,wg.request_max_memory_grant_percent        AS group_request_max_memory_grant_pcnt
    ,wg.max_dop                        AS group_max_dop
    ,wg.effective_max_dop                AS group_effective_max_dop
    ,wg.total_request_count                AS group_total_request_count
    ,wg.total_queued_request_count            AS group_total_queued_request_count
    ,wg.active_request_count                AS group_active_request_count
    ,wg.queued_request_count                AS group_queued_request_count
    FROM    sys.dm_pdw_nodes_resource_governor_workload_groups wg
    JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools rp    
            ON  wg.pdw_node_id  = rp.pdw_node_id
            AND wg.pool_id      = rp.pool_id
    JOIN    sys.dm_pdw_nodes pn
            ON    wg.pdw_node_id    = pn.pdw_node_id
    WHERE   wg.name like 'SloDWGroup%'
        AND     rp.name = 'SloDWPool'
)
SELECT    pool_name
,        pool_max_mem_MB
,        group_name
,        group_importance
,        (pool_max_mem_MB/100)*group_request_max_memory_grant_pcnt AS max_memory_grant_MB
,        node_name
,        node_type
,       group_total_request_count
,       group_total_queued_request_count
,       group_active_request_count
,       group_queued_request_count
FROM    rg
ORDER BY
    node_name
,    group_request_max_memory_grant_pcnt
,    group_importance
;
```

## <a name="queries-that-honor-concurrency-limits"></a>Consultas que respeitam os limites de simultaneidade
A maioria das consultas é governada pelas classes de recurso. Essas consultas devem se ajustar dentro de consultas simultâneas hello e limites de slot de simultaneidade. Um usuário não pode escolher tooexclude uma consulta de modelo de slot Olá simultaneidade.

tooreiterate, hello instruções a seguir consideram classes de recursos:

* INSERT-SELECT
* UPDATE
* EXCLUIR
* SELECT (ao consultar tabelas de usuário)
* ALTER INDEX REBUILD
* ALTER INDEX REORGANIZE
* ALTER TABLE REBUILD
* CREATE INDEX
* CREATE CLUSTERED COLUMNSTORE INDEX
* CREATE TABLE AS SELECT (CTAS)
* Carregamento de dados
* Operações de movimentação de dados realizadas por Olá serviço de movimentação de dados (DMS)

## <a name="query-exceptions-tooconcurrency-limits"></a>Limites de tooconcurrency de exceções de consulta
Algumas consultas não consideram recurso Olá classe toowhich Olá usuário é atribuído. Esses limites de simultaneidade toohello exceções são feitas quando recursos de memória de saudação necessários para um determinado comando estão baixos, geralmente porque o comando Olá é uma operação de metadados. Olá objetivo essas exceções é tooavoid alocações de memória maior para consultas que nunca precisam delas. Nesses casos, o padrão de saudação classe do recurso pequeno (smallrc) é sempre usado, independentemente da classe de recurso real Olá atribuído toohello usuário. Por exemplo, `CREATE LOGIN` sempre será executado em smallrc. Olá recursos necessários toofulfill essa operação são muito baixo, portanto, não faz consultas de saudação tooinclude sentido no modelo de slot de simultaneidade de saudação.  Essas consultas também não são limitadas por limite de simultaneidade de usuário Olá 32, um número ilimitado dessas consultas pode executar o limite de sessão toohello de 1.024 sessões.

Olá instruções a seguir não consideram classes de recursos:

* CREATE ou DROP TABLE
* ALTER TABLE ... SWITCH, SPLIT ou MERGE PARTITION
* ALTER INDEX DISABLE
* DROP INDEX
* CREATE, UPDATE ou DROP STATISTICS
* TRUNCATE TABLE
* ALTER AUTHORIZATION
* CREATE LOGIN
* CREATE, ALTER ou DROP USER
* CREATE, ALTER ou DROP PROCEDURE
* CREATE ou DROP VIEW
* INSERT VALUES
* SELECT de exibições do sistema e DMVs
* EXPLAIN
* DBCC

<!--
Removed as these two are not confirmed / supported under SQLDW
- CREATE REMOTE TABLE AS SELECT
- CREATE EXTERNAL TABLE AS SELECT
- REDISTRIBUTE
-->

##  <a name="changing-user-resource-class-example"></a> Alterar um exemplo de classe de recursos de usuário
1. **Criar logon:** abrir uma conexão tooyour **mestre** banco de dados SQL server Olá que hospeda seu banco de dados do SQL Data Warehouse e executar Olá comandos a seguir.
   
    ```sql
    CREATE LOGIN newperson WITH PASSWORD = 'mypassword';
    CREATE USER newperson for LOGIN newperson;
    ```
   
   > [!NOTE]
   > É uma boa ideia toocreate um usuário no banco de dados mestre para usuários do Azure SQL Data Warehouse hello. Criando um usuário em mestre permite que um toologin de usuário usando ferramentas como o SSMS sem especificar um nome de banco de dados.  Ele também permite que toouse Olá objeto explorer tooview todos os bancos de dados em um SQL server.  Para obter mais detalhes sobre como criar e gerenciar usuários, consulte [Proteger um banco de dados no SQL Data Warehouse][Secure a database in SQL Data Warehouse].
   > 
   > 
2. **Criar usuário do SQL Data Warehouse:** abrir uma conexão toohello **SQL Data Warehouse** banco de dados e executar Olá comando a seguir.
   
    ```sql
    CREATE USER newperson FOR LOGIN newperson;
    ```
3. **Conceder permissões:** Olá seguinte exemplo concede `CONTROL` em Olá **SQL Data Warehouse** banco de dados. `CONTROL`em Olá nível de banco de dados é Olá equivalente de db_owner no SQL Server.
   
    ```sql
    GRANT CONTROL ON DATABASE::MySQLDW toonewperson;
    ```
4. **Aumentar a classe de recurso:** tooadd de consulta a seguir de saudação Use uma função de gerenciamento de carga de trabalho mais alto do usuário tooa.
   
    ```sql
    EXEC sp_addrolemember 'largerc', 'newperson'
    ```
5. **Diminuir a classe de recurso:** consulta a seguir do uso Olá tooremove um usuário de uma função de gerenciamento de carga de trabalho.
   
    ```sql
    EXEC sp_droprolemember 'largerc', 'newperson';
    ```
   
   > [!NOTE]
   > Não é possível tooremove de smallrc um usuário.
   > 
   > 

## <a name="queued-query-detection-and-other-dmvs"></a>Detecção de consulta enfileirada e outros DMVs
Você pode usar o hello `sys.dm_pdw_exec_requests` as consultas DMV tooidentify que estão aguardando na fila de simultaneidade. As consultas que estão aguardando um slot de simultaneidade terão um status de **suspensas**.

```sql
SELECT      r.[request_id]                 AS Request_ID
        ,r.[status]                 AS Request_Status
        ,r.[submit_time]             AS Request_SubmitTime
        ,r.[start_time]                 AS Request_StartTime
        ,DATEDIFF(ms,[submit_time],[start_time]) AS Request_InitiateDuration_ms
        ,r.resource_class                         AS Request_resource_class
FROM    sys.dm_pdw_exec_requests r;
```

As funções de gerenciamento de carga de trabalho podem ser exibidas com `sys.database_principals`.

```sql
SELECT  ro.[name]           AS [db_role_name]
FROM    sys.database_principals ro
WHERE   ro.[type_desc]      = 'DATABASE_ROLE'
AND     ro.[is_fixed_role]  = 0;
```

saudação de consulta a seguir mostra qual função de cada usuário é atribuído.

```sql
SELECT     r.name AS role_principal_name
        ,m.name AS member_principal_name
FROM    sys.database_role_members rm
JOIN    sys.database_principals AS r            ON rm.role_principal_id        = r.principal_id
JOIN    sys.database_principals AS m            ON rm.member_principal_id    = m.principal_id
WHERE    r.name IN ('mediumrc','largerc', 'xlargerc');
```

SQL Data Warehouse tem Olá seguintes tipos de espera:

* **LocalQueriesConcurrencyResourceType**: consultas que ficam fora do framework de slot de simultaneidade hello. Consultas DMV e funções de sistema, como `SELECT @@VERSION` , são exemplos de consultas de locais.
* **UserConcurrencyResourceType**: consultas que ficam dentro do framework de slot de simultaneidade hello. Consultas em tabelas do usuário final representam exemplos que usariam esse tipo de recurso.
* **DmsConcurrencyResourceType**: esperas resultantes de operações de movimentação de dados.
* **BackupConcurrencyResourceType**: essa espera indica que está sendo feito backup de um banco de dados. saudação de valor máximo para esse tipo de recurso é 1. Se vários backups foram solicitados em Olá simultaneamente, Olá outros colocará em fila.

Olá `sys.dm_pdw_waits` DMV pode ser usado toosee os recursos que uma solicitação está aguardando.

```sql
SELECT  w.[wait_id]
,       w.[session_id]
,       w.[type]            AS Wait_type
,       w.[object_type]
,       w.[object_name]
,       w.[request_id]
,       w.[request_time]
,       w.[acquire_time]
,       w.[state]
,       w.[priority]
,    SESSION_ID()            AS Current_session
,    s.[status]            AS Session_status
,    s.[login_name]
,    s.[query_count]
,    s.[client_id]
,    s.[sql_spid]
,    r.[command]            AS Request_command
,    r.[label]
,    r.[status]            AS Request_status
,    r.[submit_time]
,    r.[start_time]
,    r.[end_compile_time]
,    r.[end_time]
,    DATEDIFF(ms,r.[submit_time],r.[start_time])        AS Request_queue_time_ms
,    DATEDIFF(ms,r.[start_time],r.[end_compile_time])    AS Request_compile_time_ms
,    DATEDIFF(ms,r.[end_compile_time],r.[end_time])        AS Request_execution_time_ms
,    r.[total_elapsed_time]
FROM    sys.dm_pdw_waits w
JOIN    sys.dm_pdw_exec_sessions s  ON w.[session_id] = s.[session_id]
JOIN    sys.dm_pdw_exec_requests r  ON w.[request_id] = r.[request_id]
WHERE    w.[session_id] <> SESSION_ID();
```

Olá `sys.dm_pdw_resource_waits` DMV mostra apenas Olá esperas de recurso consumidas por uma determinada consulta. Tempo de espera de recursos só mede o tempo de saudação aguardando toobe de recursos fornecido, conforme toosignal contrário aguardar o tempo, o que é o tempo de saudação que leva para Olá base SQL servidores tooschedule Olá consulta para CPU hello.

```sql
SELECT  [session_id]
,       [type]
,       [object_type]
,       [object_name]
,       [request_id]
,       [request_time]
,       [acquire_time]
,       DATEDIFF(ms,[request_time],[acquire_time])  AS acquire_duration_ms
,       [concurrency_slots_used]                    AS concurrency_slots_reserved
,       [resource_class]
,       [wait_id]                                   AS queue_position
FROM    sys.dm_pdw_resource_waits
WHERE    [session_id] <> SESSION_ID();
```

Olá `sys.dm_pdw_wait_stats` DMV pode ser usada para análise de tendências históricas de esperas.

```sql
SELECT    w.[pdw_node_id]
,        w.[wait_name]
,        w.[max_wait_time]
,        w.[request_count]
,        w.[signal_time]
,        w.[completed_count]
,        w.[wait_time]
FROM    sys.dm_pdw_wait_stats w;
```

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre como gerenciar usuários de banco de dados e segurança, confira [Proteger um banco de dados no SQL Data Warehouse][Secure a database in SQL Data Warehouse]. Para obter mais informações sobre classes de recursos como maiores podem melhorar a qualidade do índice columnstore clusterizado, consulte [recriação de qualidade de segmento tooimprove índices].

<!--Image references-->

<!--Article references-->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[recriação de qualidade de segmento tooimprove índices]: ./sql-data-warehouse-tables-index.md#rebuilding-indexes-to-improve-segment-quality
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md

<!--MSDN references-->
[Managing Databases and Logins in Azure SQL Database]:https://msdn.microsoft.com/library/azure/ee336235.aspx

<!--Other Web references-->
