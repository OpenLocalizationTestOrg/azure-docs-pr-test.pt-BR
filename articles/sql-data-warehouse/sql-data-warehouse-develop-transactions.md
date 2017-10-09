---
title: aaaTransactions no SQL Data Warehouse | Microsoft Docs
description: "Dicas para implementar transações no Azure SQL Data Warehouse para o desenvolvimento de soluções."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: ae621788-e575-41f5-8bfe-fa04dc4b0b53
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 7c541648553238443b407666612561918096eb61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="transactions-in-sql-data-warehouse"></a>Transações no SQL Data Warehouse
Como esperado, o SQL Data Warehouse oferece suporte a transações como parte da carga de trabalho do hello data warehouse. No entanto, tooensure Olá desempenho do SQL Data Warehouse é mantido em escala de que alguns recursos estão limitados quando tooSQL em comparação com o servidor. Este artigo destaca as diferenças de saudação e listas Olá outras pessoas. 

## <a name="transaction-isolation-levels"></a>Níveis de isolamento da transação
O SQL Data Warehouse implementa transações ACID. No entanto, Olá isolamento de suporte transacional Olá é limitado muito`READ UNCOMMITTED` e isso não pode ser alterado. Você pode implementar vários métodos de codificação tooprevent suja leituras de dados se isso for uma preocupação para você. Olá métodos mais comuns aproveitam CTAS e a alternância de partição de tabela (geralmente conhecido como Olá padrão de janela deslizante) tooprevent usuários consultando os dados que ainda está sendo preparados. Exibições de dados pré-filtragem saudação também são um método popular.  

## <a name="transaction-size"></a>Tamanho da transação
Uma única transação de modificação de dados é limitada em tamanho. limite de saudação hoje é aplicado "por distribuição de". Portanto, alocação total Olá pode ser calculada pela multiplicação de limite de saudação por contagem de distribuição de saudação. número máximo de saudação de tooapproximate de linhas em transação Olá divide cap de distribuição de saudação pelo tamanho total de saudação de cada linha. Para colunas de comprimento variável, considere colocar um comprimento médio de coluna em vez de usar o tamanho máximo de saudação.

Na tabela de saudação abaixo Olá foram feitas seguintes suposições:

* Ocorreu uma distribuição uniforme dos dados 
* Comprimento médio da linha de saudação é de 250 bytes

| [DWU][DWU] | Limite por distribuição (GiB) | Número de distribuições | Tamanho máximo de transações (GiB) | # Linhas por distribuição | Máximo de linhas por transação |
| --- | --- | --- | --- | --- | --- |
| DW100 |1 |60 |60 |4.000.000 |240.000.000 |
| DW200 |1.5 |60 |90 |6.000.000 |360.000.000 |
| DW300 |2.25 |60 |135 |9.000.000 |540.000.000 |
| DW400 |3 |60 |180 |12.000.000 |720.000.000 |
| DW500 |3,75 |60 |225 |15.000.000 |900.000.000 |
| DW600 |4.5 |60 |270 |18.000.000 |1.080.000.000 |
| DW1000 |7.5 |60 |450 |30.000.000 |1.800.000.000 |
| DW1200 |9 |60 |540 |36.000.000 |2.160.000.000 |
| DW1500 |11,25 |60 |675 |45.000.000 |2.700.000.000 |
| DW2000 |15 |60 |900 |60.000.000 |3.600.000.000 |
| DW3000 |22,5 |60 |1.350 |90.000.000 |5.400.000.000 |
| DW6000 |45 |60 |2.700 |180.000.000 |10.800.000.000 |

limite de tamanho de transação Olá é aplicado por transação ou a operação. Ele não é aplicado em todas as transações simultâneas. Portanto, cada transação é permitida toowrite essa quantidade de dados toohello log. 

toooptimize e minimizar Olá toohello log de gravação de dados, consulte toohello [transações práticas recomendadas] [ Transactions best practices] artigo.

> [!WARNING]
> Olá máximo de tamanho de transação só pode ser obtido para HASH ou tabelas ROUND_ROBIN distribuídas onde espalhar Olá Olá dados é par. Se transação hello está gravando os dados de maneira distorcida toohello distribuições, em seguida, hello limite é provavelmente toobe atingida o tamanho de máximo de transações de toohello anterior.
> <!--REPLICATED_TABLE-->
> 
> 

## <a name="transaction-state"></a>Estado da transação
SQL Data Warehouse usa Olá xact_state função tooreport uma transação com falha usando o valor de saudação -2. Isso significa que a transação Olá falhou e está marcada para reversão apenas

> [!NOTE]
> Olá usá -2 Olá XACT_STATE função toodenote tooSQL de um comportamento diferente de representa uma transação com falha Server. O SQL Server usa Olá valor -1 toorepresent uma transação não confirmável. SQL Server pode tolerar alguns erros dentro de uma transação sem que ele tenha toobe marcado como não confirmável. Por exemplo, `SELECT 1/0` poderia causar um erro, mas não forçar uma transação em um estado não confirmável. SQL Server também permite leituras de transação não confirmável hello. No entanto, o SQL Data Warehouse não permite que você faça isso. Se ocorrer um erro dentro de uma transação do SQL Data Warehouse, ele inserirá automaticamente o estado da saudação -2 e não será capaz de toomake qualquer mais instruções select até que a instrução de saudação foi revertida. Portanto, é importante toocheck que sua toosee de código do aplicativo se ele usa xact_state como você pode precisar de modificações no código toomake.
> 
> 

Por exemplo, no SQL Server, você verá uma transação com esta aparência:

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

Se você deixar seu código, pois ele está acima, em seguida, você obterá Olá a seguinte mensagem de erro:

Msg 111233, nível 16, estado 1, linha 1 111233; Olá atual transação foi anulada, e todas as alterações pendentes foram revertidas. Causa: uma transação no estado somente reversão não foi revertida explicitamente antes de uma instrução DDL, DML ou SELECT.

Você também não terá saída de saudação do erro. * funções de saudação.

No SQL Data Warehouse código Olá precisa toobe ligeiramente alterado:

```sql
SET NOCOUNT ON;
DECLARE @xact_state smallint = 0;

BEGIN TRAN
    BEGIN TRY
        DECLARE @i INT;
        SET     @i = CONVERT(INT,'ABC');
    END TRY
    BEGIN CATCH
        SET @xact_state = XACT_STATE();

        IF @@TRANCOUNT > 0
        BEGIN
            PRINT 'ROLLBACK';
            ROLLBACK TRAN;
        END

        SELECT  ERROR_NUMBER()    AS ErrNumber
        ,       ERROR_SEVERITY()  AS ErrSeverity
        ,       ERROR_STATE()     AS ErrState
        ,       ERROR_PROCEDURE() AS ErrProcedure
        ,       ERROR_MESSAGE()   AS ErrMessage
        ;
    END CATCH;

IF @@TRANCOUNT >0
BEGIN
    PRINT 'COMMIT';
    COMMIT TRAN;
END

SELECT @xact_state AS TransactionState;
```

Olá esperado comportamento observado agora. Erro de saudação na transação de saudação é gerenciado e Olá erro. * funções fornecem valores conforme o esperado.

Tudo o que mudou é que hello `ROLLBACK` de saudação transação tinha toohappen antes de ler Olá Olá informações de erro em Olá `CATCH` bloco.

## <a name="errorline-function"></a>Função Error_line()
Também vale a pena observar que SQL Data Warehouse não implementar ou oferecer suporte a função do hello error_line (). Se você tiver isso em seu código, você precisará tooremove-toobe compatível com o SQL Data Warehouse. Use rótulos de consulta em seu código em vez disso, tooimplement uma funcionalidade equivalente. Consulte toohello [rótulo] [ LABEL] artigo para obter mais detalhes sobre esse recurso.

## <a name="using-throw-and-raiserror"></a>Uso de THROW e RAISERROR
THROW é Olá implementação mais moderna para gerar exceções no SQL Data Warehouse, mas também há suporte para RAISERROR. Há algumas diferenças que vale a pena prestando atenção toohowever.

* Números não podem estar em Olá intervalo 100.000 150.000 THROW de mensagens de erro definidas pelo usuário
* As mensagens de erro do RAISERROR são fixadas em 50.000
* Não há suporte para o uso de sys.messages

## <a name="limitiations"></a>Limitações
SQL Data Warehouse tem algumas outras restrições que se relacionam tootransactions.

Elas são as seguintes:

* Sem transações distribuídas
* Não há transações aninhadas permitidas
* Não são permitidos pontos de salvamento
* Nenhuma transação nomeada
* Nenhuma transação marcada
* Não há suporte para DDL, como `CREATE TABLE` , em uma transação definida pelo usuário

## <a name="next-steps"></a>Próximas etapas
toolearn mais informações sobre a otimização de transações, consulte [transações práticas recomendadas][Transactions best practices].  toolearn sobre outras práticas recomendadas do SQL Data Warehouse, consulte [práticas recomendadas do SQL Data Warehouse][SQL Data Warehouse best practices].

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Transactions best practices]: ./sql-data-warehouse-develop-best-practices-transactions.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[LABEL]: ./sql-data-warehouse-develop-label.md

<!--MSDN references-->

<!--Other Web references-->
