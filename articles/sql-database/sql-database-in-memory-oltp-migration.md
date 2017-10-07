---
title: OLTP in-memory aaaIn melhora o desempenho do SQL txn | Microsoft Docs
description: "Desempenho transacional de tooimprove de adotar o OLTP na memória em um banco de dados existente do SQL."
services: sql-database
documentationcenter: 
author: jodebrui
manager: jhubbard
editor: MightyPen
ms.assetid: c2bf14a0-905b-47b4-afb6-efe9a61147d5
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: jodebrui
ms.openlocfilehash: 1bed796069565eb6741953837cf0477c2ddd8519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-in-memory-oltp-tooimprove-your-application-performance-in-sql-database"></a>Use o OLTP na memória tooimprove o desempenho do seu aplicativo no banco de dados SQL
[OLTP na memória](sql-database-in-memory.md) pode ser usado tooimprove Olá desempenho de processamento de transações, ingestão de dados e cenários de dados transitórios, em [Premium](sql-database-service-tiers.md) bancos de dados SQL Azure sem aumentar Olá camada de preços. 

> [!NOTE] 
> Saiba como o [Quorum dobra a principal carga de trabalho do banco de dados, enquanto reduz a DTU em 70% com o Banco de Dados SQL](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)


Siga essas etapas tooadopt OLTP na memória no banco de dados existente.

## <a name="step-1-ensure-you-are-using-a-premium-database"></a>Etapa 1: Garantir que você está usando um banco de dados Premium
Há suporte para o OLTP in-memory apenas em bancos de dados Premium. Na memória é suportada se Olá retornou resultado é 1 (não em 0):

```
SELECT DatabasePropertyEx(Db_Name(), 'IsXTPSupported');
```

*XTP* significa *Processamento Extremo de Transações*



## <a name="step-2-identify-objects-toomigrate-tooin-memory-oltp"></a>Etapa 2: Identificar objetos tooIn toomigrate memória OLTP
O SSMS inclui um relatório **Visão Geral da Análise do Desempenho da Transação** que pode ser executado em um banco de dados com uma carga de trabalho ativa. relatório de saudação identifica tabelas e procedimentos armazenados que são candidatos à migração de OLTP in-memory tooIn.

No SSMS, relatório de saudação toogenerate:

* Em Olá **Pesquisador de objetos**, clique o nó do banco de dados.
* Clique em **Relatórios** > **Relatórios Padrão** > **Visão Geral da Análise de Desempenho da Transação**.

Para obter mais informações, consulte [determinando se uma tabela ou procedimento armazenado deve ser movido OLTP de memória tooIn](http://msdn.microsoft.com/library/dn205133.aspx).

## <a name="step-3-create-a-comparable-test-database"></a>Etapa 3: Criar um banco de dados de teste comparável
Suponha que o relatório de saudação indica seu banco de dados tem uma tabela que pode se beneficiar do que está sendo convertido tooa tabela de otimização de memória. É recomendável que você primeiro teste indicação de saudação tooconfirm testando.

Você precisa de uma cópia de teste do seu banco de dados de produção. Olá banco de dados de teste deve ser no hello mesmo nível de serviço da camada do banco de dados de produção.

tooease de teste, ajustar o banco de dados de teste da seguinte maneira:

1. Conecte o banco de dados de teste toohello usando o SSMS.
2. tooavoid necessidade Olá a opção WITH (SNAPSHOT) em consultas, defina a opção de banco de dados de saudação conforme Olá instrução T-SQL a seguir:
   
   ```
   ALTER DATABASE CURRENT
    SET
        MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;
   ```

## <a name="step-4-migrate-tables"></a>Etapa 4: migrar tabelas
Você deve criar e preencher uma cópia com otimização de memória da tabela Olá deseja tootest. Você pode criá-la usando:

* Olá útil Assistente de otimização de memória no SSMS.
* T-SQL Manual.

#### <a name="memory-optimization-wizard-in-ssms"></a>Assistente de Otimização de Memória no SSMS
toouse essa opção de migração:

1. Conecte o banco de dados de teste de toohello com o SSMS.
2. Em Olá **Pesquisador de objetos**, com o botão direito na tabela hello e, em seguida, clique em **orientador de otimização de memória**.
   
   * Olá **orientador otimizador memória da tabela** assistente é exibido.
3. No Assistente de saudação, clique em **validação de migração** (ou hello **próximo** botão) toosee se Olá tabela possui recursos sem suporte que não têm suporte em tabelas com otimização de memória. Para obter mais informações, consulte:
   
   * Olá *lista de verificação de otimização de memória* na [orientador de otimização de memória](http://msdn.microsoft.com/library/dn284308.aspx).
   * [Construções Transact-SQL sem suporte do OLTP Na Memória](http://msdn.microsoft.com/library/dn246937.aspx).
   * [Migrando OLTP de memória tooIn](http://msdn.microsoft.com/library/dn247639.aspx).
4. Se a tabela de saudação tem recursos sem suporte, advisor Olá pode executar o esquema real hello e migração de dados para você.

#### <a name="manual-t-sql"></a>T-SQL Manual
toouse essa opção de migração:

1. Conecte o banco de dados de teste tooyour usando o SSMS (ou um utilitário semelhante).
2. Obter script de T-SQL completo Olá para sua tabela e seus índices.
   
   * No SSMS, clique com o botão direito do mouse no nó da sua tabela.
   * Clique em **Script de Tabela como** > **CRIAR Para** > **Nova Janela de Consulta**.
3. Na janela de script hello, adicione WITH (MEMORY_OPTIMIZED = ON) toohello instrução CREATE TABLE.
4. Se houver um índice CLUSTERIZADO, altere tooNONCLUSTERED.
5. Renomear tabela existente hello usando SP_RENAME.
6. Crie cópia Olá com otimização de memória nova da tabela Olá executando o script CREATE TABLE editado.
7. Copie a tabela Olá dados tooyour otimização de memória usando INSERT... SELECIONE * EM:

```
INSERT INTO <new_memory_optimized_table>
        SELECT * FROM <old_disk_based_table>;
```


## <a name="step-5-optional-migrate-stored-procedures"></a>Etapa 5 (opcional): migrar procedimentos armazenados
recurso do Hello na memória também pode modificar um procedimento armazenado para melhorar o desempenho.

### <a name="considerations-with-natively-compiled-stored-procedures"></a>Considerações sobre procedimentos armazenados compilados nativamente
Um procedimento armazenado compilado nativamente deve ter uma saudação em sua cláusula T-SQL com as opções a seguir:

* NATIVE_COMPILATION
* SCHEMABINDING: tabelas significado Olá procedimento armazenado não podem ter suas definições de coluna alteradas de qualquer maneira que possa afetar o procedimento armazenado de saudação, a menos que você remover o procedimento armazenado de saudação.

Um módulo nativo deve usar grandes [blocos ATOMIC](http://msdn.microsoft.com/library/dn452281.aspx) para o gerenciamento de transações. Não há uma função para BEGIN TRANSACTION explícita ou para ROLLBACK TRANSACTION. Se o seu código detectar uma violação de uma regra de negócio, ele pode ser encerrado bloco atômico de saudação com um [gerar](http://msdn.microsoft.com/library/ee677615.aspx) instrução.

### <a name="typical-create-procedure-for-natively-compiled"></a>CREATE PROCEDURE típico para compilados nativamente
Normalmente, Olá T-SQL toocreate um procedimento armazenado nativamente compilado é semelhante toohello modelo a seguir:

```
CREATE PROCEDURE schemaname.procedurename
    @param1 type1, …
    WITH NATIVE_COMPILATION, SCHEMABINDING
    AS
        BEGIN ATOMIC WITH
            (TRANSACTION ISOLATION LEVEL = SNAPSHOT,
            LANGUAGE = N'your_language__see_sys.languages'
            )
        …
        END;
```

* Para Olá TRANSACTION_ISOLATION_LEVEL, o instantâneo é procedimento mais comum de valor para Olá compilado nativamente armazenado hello. No entanto, um subconjunto de Olá outros valores também são suportados:
  
  * REPEATABLE READ
  * SERIALIZABLE
* Olá valor de idioma deve estar presente no modo de exibição de sys.languages hello.

### <a name="how-toomigrate-a-stored-procedure"></a>Como toomigrate um procedimento armazenado
etapas de migração de saudação são:

1. Obter Olá CREATE PROCEDURE script toohello regular procedimento armazenado interpretado.
2. Reescreva o modelo do cabeçalho toomatch Olá anterior.
3. Verificar se o procedimento armazenado de saudação código T-SQL usa todos os recursos que não há suporte para procedimentos armazenados compilados nativamente. Implemente soluções alternativas, se necessário.
   
   * Para obter detalhes, consulte [Problemas de migração para procedimentos armazenados compilados nativamente](http://msdn.microsoft.com/library/dn296678.aspx).
4. Renomear o procedimento armazenado do antigo hello usando SP_RENAME. Ou simplesmente descarte-o usando DROP.
5. Execute o script T-SQL CREATE PROCEDURE editado.

## <a name="step-6-run-your-workload-in-test"></a>Etapa 6: executar sua carga de trabalho no teste
Execute uma carga de trabalho em seu banco de dados de teste é semelhante toohello carga de trabalho é executado em seu banco de dados de produção. Isso deve revelar o ganho de desempenho Olá obtido com o uso do recurso de na memória de saudação para tabelas e procedimentos armazenados.

Os atributos principais de carga de trabalho de saudação são:

* Número de conexões simultâneas.
* Taxa de leitura/gravação.

tootailor e carga de trabalho de teste de execução hello, considere o uso de ferramenta de ostress.exe útil hello, que ilustrado na [aqui](sql-database-in-memory.md).

latência de rede toominimize, executar o teste em Olá mesma região geográfica do Azure onde o banco de dados de saudação existe.

## <a name="step-7-post-implementation-monitoring"></a>Etapa 7: Monitoramento pós-implementação
Considere a possibilidade de monitorar os efeitos do desempenho de saudação de suas implementações de memória em produção:

* [Monitorar o armazenamento na memória](sql-database-in-memory-oltp-monitoring.md).
* [Monitoramento de Banco de Dados SQL usando exibições de gerenciamento dinâmico](sql-database-monitoring-with-dmvs.md)

## <a name="related-links"></a>Links relacionados
* [OLTP Na Memória (Otimização Na Memória)](http://msdn.microsoft.com/library/dn133186.aspx)
* [Introdução tooNatively Compiled Stored Procedures](http://msdn.microsoft.com/library/dn133184.aspx)
* [Supervisor de Otimização de Memória](http://msdn.microsoft.com/library/dn284308.aspx)

