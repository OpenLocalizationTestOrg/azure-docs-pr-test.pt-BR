---
title: "aaaManage computação power no Azure SQL Data Warehouse (visão geral) | Microsoft Docs"
description: "Funcionalidades de escala horizontal de desempenho no SQL Data Warehouse do Azure. Expansão ajustando DWUs ou pausar e retomar os custos de toosave de recursos de computação."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: johnmac
editor: 
ms.assetid: e13a82b0-abfe-429f-ac3c-f2b6789a70c6
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 03/22/2017
ms.author: elbutter
ms.openlocfilehash: 1ffbe8d694ac181eaeb6f585a2cee87a570ed7d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-overview"></a>Gerenciar poder de computação no SQL Data Warehouse do Azure (Visão Geral)
> [!div class="op_single_selector"]
> * [Visão geral](sql-data-warehouse-manage-compute-overview.md)
> * [Portal](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>

arquitetura de saudação do SQL Data Warehouse separa o armazenamento e computação, permitindo que cada tooscale independentemente. Como resultado, computação pode ser dimensionado toomeet as demandas de desempenho independente do valor de saudação de dados. Uma consequência natural dessa arquitetura é que a [cobrança][billed] pela computação e pelo armazenamento é separada. 

Esta visão geral descreve como expandir funciona com o SQL Data Warehouse e como tooutilize Olá pausar, retomar e recursos de escala do SQL Data Warehouse. Consulte Olá [unidades (DWUs) do data warehouse] [ data warehouse units (DWUs)] toolearn de página como DWUs e desempenho estão relacionados. 

## <a name="how-compute-management-operations-work-in-sql-data-warehouse"></a>Como as operações de gerenciamento de computação funcionam no SQL Data Warehouse
arquitetura de saudação do SQL Data Warehouse consiste em um nó de controle, nós de computação e Olá disseminadas por 60 distribuições de camada de armazenamento. 

Durante uma sessão ativa normal no SQL Data Warehouse, nó principal do sistema gerencia os metadados de saudação e contém o otimizador de consulta Olá distribuída. Sob esse nó principal estão os nós de computação e a camada de armazenamento. Para um DWU 400, o sistema tem um nó principal, quatro nós de computação e camada de armazenamento hello, consistindo de 60 distribuições. 

Quando você passar por uma escala ou pausa a operação, o sistema de saudação primeiro elimina todas as consultas de entrada e, em seguida, reverte as transações tooensure um estado consistente. Para operações de escala, o dimensionamento só ocorrerá após a conclusão dessa reversão transacional. Para uma operação de expansão, provisões de sistema Olá Olá número de nós de computação extra desejado e começa a reanexação de camada de armazenamento toohello de nós de computação hello. Para uma operação de redução de escala, hello nós desnecessários são liberados e nós de computação restantes Olá reconecte toohello o número apropriado de distribuições. Para uma operação de pausa de computação todos os nós são liberados e o sistema passará por uma variedade de metadados operações tooleave seu sistema final em um estado estável.

| DWU  | \# de nós de computação | \# de distribuições por nó |
| ---- | ------------------ | ---------------------------- |
| 100  | 1                  | 60                           |
| 200  | 2                  | 30                           |
| 300  | 3                  | 20                           |
| 400  | 4                  | 15                           |
| 500  | 5                  | 12                           |
| 600  | 6                  | 10                           |
| 1000 | 10                 | 6                            |
| 1.200 | 12                 | 5                            |
| 1500 | 15                 | 4                            |
| 2000 | 20                 | 3                            |
| 3000 | 30                 | 2                            |
| 6000 | 60                 | 1                            |

Olá três principais funções de gerenciamento de computação são:

1. Pausar
2. Continuar
3. Escala

Cada uma dessas operações pode levar vários toocomplete de minutos. Se você estiver dimensionando/interrompendo/retomando automaticamente, convém lógica tooimplement tooensure que determinadas operações tenham sido concluídas antes de continuar com a outra ação. 

Verificando o estado do banco de dados Olá por meio de vários pontos de extremidade permitirá toocorrectly implementar automação dessas operações. portal de saudação fornecerá notificação após a conclusão da operação e hello bancos de dados atual estado, mas não permite a verificação programático do estado. 

>  [!NOTE]
>
>  A funcionalidade de gerenciamento de computação não existe em todos os pontos de extremidade.
>
>  

|              | Pausar/Retomar | Escala | Verificar estado do banco de dados |
| ------------ | ------------ | ----- | -------------------- |
| Portal do Azure | Sim          | Sim   | **Não**               |
| PowerShell   | Sim          | Sim   | Sim                  |
| API REST     | Sim          | Sim   | Sim                  |
| T-SQL        | **Não**       | Sim   | Sim                  |



<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a>Computação de escala

O desempenho no SQL Data Warehouse é medido em [DWUs (unidades do data warehouse)][data warehouse units (DWUs)], que é uma medida abstrata de recursos de computação como CPU, memória e E/S de largura de banda. Um usuário que deseja tooscale o desempenho do seu sistema pode fazer isso através de várias maneiras, como por meio do portal hello, T-SQL e APIs REST. 

### <a name="how-do-i-scale-compute"></a>Como eu dimensiono a computação?
Capacidade de computação é gerenciada por você SQL Data Warehouse, alterando a configuração de DWU de saudação. O desempenho aumenta [linearmente][linearly] conforme você adiciona mais DWUs para determinadas operações.  Temos ofertas de DWU que asseguram que o desempenho será alterado visivelmente quando você escalar ou reduzir verticalmente seu sistema. 

tooadjust DWUs, você pode usar qualquer um desses métodos individuais.

* [Dimensionar a potência de computação com o Portal do Azure][Scale compute power with Azure portal]
* [Dimensionar a potência de computação com o PowerShell][Scale compute power with PowerShell]
* [Dimensionar a potência de computação com APIs REST][Scale compute power with REST APIs]
* [Dimensionar a potência de computação com o TSQL][Scale compute power with TSQL]

### <a name="how-many-dwus-should-i-use"></a>Quantas DWUs devo usar?

toounderstand é que o valor DWU ideal, tente dimensionamento para cima e para baixo e executando consultas alguns após o carregamento de dados. Como o dimensionamento é rápido, você pode experimentar vários níveis de desempenho diferentes durante uma hora ou menos. 

> [!Note] 
> SQL Data Warehouse é projetado tooprocess grandes quantidades de dados. toosee seus recursos true para dimensionar, especialmente em DWUs maior, você deseja toouse um grande conjunto de dados que se aproxima ou exceder 1 TB.

Recomendações para encontrar hello DWU melhor para sua carga de trabalho:

1. Para um data warehouse em desenvolvimento, comece selecionando um nível de desempenho de DWU menor.  Um bom ponto de partida é DW400 ou DW200.
2. Monitorar o desempenho do seu aplicativo, observar o número de saudação do DWUs selecionado em comparação com o desempenho toohello que você observar.
3. Determine quanto de desempenho mais rápido ou mais lento para você tooreach Olá nível de desempenho ideal para suas necessidades, supondo que a escala linear.
4. Aumentar ou diminuir o número de saudação de DWUs em proporção toohow muito mais rápida ou mais lenta do que você deseja tooperform sua carga de trabalho. 
5. Continue fazendo ajustes até alcançar um nível de desempenho ideal para seus requisitos de negócios.

> [!NOTE]
>
> Desempenho de consultas só aumenta com mais de paralelização se trabalho Olá pode ser dividido entre nós de computação. Se você encontrar o dimensionamento não está alterando seu desempenho, faça check-out nossos artigos toocheck se seus dados são distribuídos ou se você está implantando uma grande quantidade de movimentação de dados de ajuste de desempenho. 

### <a name="when-should-i-scale-dwus"></a>Quando devo dimensionar as DWUs?
Dimensionamento DWUs altera Olá cenários importantes a seguir:

1. Alterando o desempenho do sistema de verificações, agregações e instruções CTAS Olá linearmente
2. Aumentar o número de saudação de leitores e gravadores ao carregar com PolyBase
3. Número máximo de consultas simultâneas e slots de simultaneidade

Recomendações de quando tooscale DWUs:

1. Antes de executar uma operação de transformação ou carregamento de dados pesados, escale verticalmente as DWUs para que os dados fiquem disponíveis mais rapidamente.
2. Durante o horário comercial de pico, dimensione tooaccommodate um número maior de consultas simultâneas. 

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a>Pausar computação
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

toopause um banco de dados, use qualquer um desses métodos individuais.

* [Pausar a computação com o Portal do Azure][Pause compute with Azure portal]
* [Pausar a computação com o PowerShell][Pause compute with PowerShell]
* [Pausar a computação com APIs REST][Pause compute with REST APIs]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a>Retomar a computação
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

tooresume um banco de dados, use qualquer um desses métodos individuais.

* [Retomar a computação com o Portal do Azure][Resume compute with Azure portal]
* [Retomar a computação com o PowerShell][Resume compute with PowerShell]
* [Retomar a computação com APIs REST][Resume compute with REST APIs]

<a name="check-compute-bk"></a>

## <a name="check-database-state"></a>Verificar estado do banco de dados 

tooresume um banco de dados, use qualquer um desses métodos individuais.

- [Verificar estado do banco de dados com o T-SQL][Check database state with T-SQL]
- [Verificar estado do banco de dados com o PowerShell][Check database state with PowerShell]
- [Verificar estado do banco de dados com o APIs REST][Check database state with REST APIs]

## <a name="permissions"></a>Permissões

Banco de dados de Olá escala requer permissões Olá descritas [ALTER DATABASE][ALTER DATABASE].  Pausar e retomar exigem Olá [Colaborador de banco de dados SQL] [ SQL DB Contributor] permissão, especificamente Microsoft.Sql/servers/databases/action.

<a name="next-steps-bk"></a>

## <a name="next-steps"></a>Próximas etapas
Consulte toohello artigos toohelp entender alguns conceitos chave de desempenho adicionais a seguir:

* [Gerenciamento da carga de trabalho e simultaneidade][Workload and concurrency management]
* [Visão geral do design da tabela][Table design overview]
* [Distribuição de tabelas][Table distribution]
* [Indexação de tabelas][Table indexing]
* [Particionamento de tabelas][Table partitioning]
* [Estatísticas de tabelas][Table statistics]
* [Práticas recomendadas][Best practices]

<!--Image reference-->

<!--Article references-->
[data warehouse units (DWUs)]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[billed]: https://azure.microsoft.com/en-us/pricing/details/sql-data-warehouse/
[linearly]: ./sql-data-warehouse-overview-what-is.md#predictable-and-scalable-performance-with-data-warehouse-units
[Scale compute power with Azure portal]: ./sql-data-warehouse-manage-compute-portal.md#scale-compute-power
[Scale compute power with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#scale-compute-bk
[Scale compute power with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#scale-compute-bk
[Scale compute power with TSQL]: ./sql-data-warehouse-manage-compute-tsql.md#scale-compute-bk

[capacity limits]: ./sql-data-warehouse-service-capacity-limits.md

[Pause compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#pause-compute-bk
[Pause compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#pause-compute-bk
[Pause compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#pause-compute-bk

[Resume compute with Azure portal]:  ./sql-data-warehouse-manage-compute-portal.md#resume-compute-bk
[Resume compute with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#resume-compute-bk
[Resume compute with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#resume-compute-bk

[Check database state with T-SQL]: ./sql-data-warehouse-manage-compute-tsql.md#check-database-state-and-operation-progress
[Check database state with PowerShell]: ./sql-data-warehouse-manage-compute-powershell.md#check-database-state
[Check database state with REST APIs]: ./sql-data-warehouse-manage-compute-rest-api.md#check-database-state

[Workload and concurrency management]: ./sql-data-warehouse-develop-concurrency.md
[Table design overview]: ./sql-data-warehouse-tables-overview.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Table indexing]: ./sql-data-warehouse-tables-index.md
[Table partitioning]: ./sql-data-warehouse-tables-partition.md
[Table statistics]: ./sql-data-warehouse-tables-statistics.md
[Best practices]: ./sql-data-warehouse-best-practices.md
[development overview]: ./sql-data-warehouse-overview-develop.md

[SQL DB Contributor]: ../active-directory/role-based-access-built-in-roles.md#sql-db-contributor

<!--MSDN references-->
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx

<!--Other Web references-->
[Azure portal]: http://portal.azure.com/
