---
title: procedimentos de aaaStored no SQL Data Warehouse | Microsoft Docs
description: "Dicas para implementar procedimentos armazenados no SQL Data Warehouse do Azure para desenvolvimento de soluções."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 9b238789-6efe-4820-bf77-5a5da2afa0e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 416252dd3dea95c66aa5e886860b933b22578002
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="stored-procedures-in-sql-data-warehouse"></a>Procedimentos armazenados no SQL Data Warehouse
SQL Data Warehouse dá suporte a muitos dos recursos de Transact-SQL Olá encontrados no SQL Server. Mais importante é que há recursos específicos que queremos desempenho de saudação do tooleverage toomaximize de sua solução de expansão.

No entanto, escala de saudação toomaintain e o desempenho do SQL Data Warehouse lá também são alguns recursos e funcionalidades que têm diferenças de comportamento e outras que não têm suporte.

Este artigo explica como tooimplement armazenados procedimentos no SQL Data Warehouse.

## <a name="introducing-stored-procedures"></a>Apresentação dos procedimentos armazenados
Procedimentos armazenados são uma ótima maneira para encapsular o código SQL; armazenando dados tooyour Fechar no data warehouse de saudação. Encapsulando código Olá em unidades gerenciáveis procedimentos armazenados ajudam os desenvolvedores modularizar suas soluções; facilitando maior reutilização de código. Cada procedimento armazenado também pode aceitar parâmetros toomake-los ainda mais flexível.

O SQL Data Warehouse fornece uma implementação simplificada e otimizada de procedimentos armazenados. Olá maior diferença em comparação comparada tooSQL Server é que Olá procedimento armazenado não é código pré-compilado. Em data warehouses estamos geralmente menos preocupados com tempo de compilação de saudação. É mais importante do que o código do procedimento Olá armazenado corretamente é otimizado ao operar em grandes volumes de dados. meta de saudação é toosave horas, minutos e segundos não milissegundos. Portanto, é mais útil toothink de procedimentos armazenados como contêineres para lógica SQL.     

Quando o SQL Data Warehouse executa suas instruções de SQL de saudação do procedimento armazenado são analisadas, convertidas e otimizadas em tempo de execução. Durante esse processo, cada instrução é convertida em consultas distribuídas. Olá código SQL que realmente é executado em relação aos dados de saudação é toohello diferentes consulta enviada.

## <a name="nesting-stored-procedures"></a>Aninhamento de procedimentos armazenados
Quando os procedimentos armazenados chamam outros procedimentos armazenados ou executar sql dinâmico, procedimento armazenado de interna hello ou invocação de código é considerada toobe aninhados.

O SQL Data Warehouse oferece suporte a um máximo de 8 níveis de aninhamento. Este é um pouco diferente tooSQL Server. nível de aninhamento de saudação no SQL Server é 32.

chamada de procedimento armazenado de nível superior de saudação é igual a toonest nível 1

```sql
EXEC prc_nesting
```
Se Olá armazenado procedimento também faz EXEC outra chamada e isso aumentará too2 de nível de aninhamento de saudação

```sql
CREATE PROCEDURE prc_nesting
AS
EXEC prc_nesting_2  -- This call is nest level 2
GO
EXEC prc_nesting
```
Se o segundo procedimento de hello, em seguida, executa algum sql dinâmico, em seguida, isso aumentará too3 de nível de aninhamento de saudação

```sql
CREATE PROCEDURE prc_nesting_2
AS
EXEC sp_executesql 'SELECT 'another nest level'  -- This call is nest level 2
GO
EXEC prc_nesting
```

Observe que atualmente o SQL Data Warehouse não dá suporte ao @@NESTLEVEL. Você será necessário tookeep uma faixa de seu nível de aninhamento. É improvável que você atingirá o limite de nível de aninhamento de saudação 8, mas nesse caso você será necessário trabalho toore seu código e "mesclar"-la para que ela caiba dentro desse limite.

## <a name="insertexecute"></a>INSERT..EXECUTE
SQL Data Warehouse não permite que você tooconsume conjunto de resultados de saudação de um procedimento armazenado com uma instrução INSERT. No entanto, há uma abordagem alternativa.

Consulte toohello artigo a seguir [tabelas temporárias] para obter um exemplo sobre como toodo isso.

## <a name="limitations"></a>Limitações
Há alguns aspectos de procedimentos armazenados Transact-SQL que não são implementados no SQL Data Warehouse.

Eles são:

* procedimentos armazenados temporariamente
* procedimentos armazenados numerados
* procedimentos armazenados estendidos
* procedimentos armazenados de CLR
* opção de criptografia
* opção de replicação
* parâmetros com valor de tabela
* parâmetros somente leitura
* parâmetros padrão
* contextos de execução
* instrução return

## <a name="next-steps"></a>Próximas etapas
Para obter mais dicas de desenvolvimento, confira [visão geral de desenvolvimento][development overview].

<!--Image references-->

<!--Article references-->
[tabelas temporárias]: ./sql-data-warehouse-tables-temporary.md#modularizing-code
[development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[nest level]: https://msdn.microsoft.com/library/ms187371.aspx

<!--Other Web references-->
