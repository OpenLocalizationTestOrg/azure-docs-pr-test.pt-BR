---
title: "recomendações de desempenho de aaaApply - banco de dados do SQL Azure | Microsoft Docs"
description: "Você pode usar as recomendações de desempenho do hello toofind portal do Azure que podem otimizar o desempenho do banco de dados do SQL Azure ou toocorrect algum problema identificado na carga de trabalho."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: cda8a646-0584-4368-b28a-85cdd9b54fcd
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 0b2234840fc3254d235db9e7d18f5bc912851c6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="find-and-apply-performance-recommendations"></a>Localizar e aplicar recomendações de desempenho

Você pode usar as recomendações de desempenho do hello toofind portal do Azure que podem otimizar o desempenho do banco de dados do SQL Azure ou toocorrect algum problema identificado na carga de trabalho. **Recomendação de desempenho** página no portal do Azure permite que você toofind Olá principais recomendações com base no impacto potencial. 

## <a name="viewing-recommendations"></a>Exibindo recomendações

tooview e aplicar recomendações de desempenho, você precisa Olá correto [controle de acesso baseado em função](../active-directory/role-based-access-control-what-is.md) permissões no Azure. **Leitor**, **Colaborador de banco de dados SQL** permissões são necessárias tooview recomendações, e **proprietário**, **Colaborador de banco de dados SQL** permissões são necessárias tooexecute quaisquer ações; Criar ou descartar índices e cancelar a criação do índice.

Use Olá recomendações de desempenho de toofind as etapas a seguir no portal do Azure:

1. Entrar toohello [portal do Azure](https://portal.azure.com/).
2. Vá muito**mais serviços** > **bancos de dados SQL**e selecione o banco de dados.
3. Navegue muito**recomendação desempenho** recomendações de tooview disponíveis para o banco de dados selecionado hello.

Recomendações de desempenho estão shonw em Olá tabela toohello semelhante mostrada na figura a seguir de saudação:

![Recomendações](./media/sql-database-advisor-portal/recommendations.png)

As recomendações são classificadas pelo impacto potencial no desempenho em Olá categorias a seguir:

| Impacto | Descrição |
|:--- |:--- |
| Alto |Recomendações de alto impacto devem fornecer o impacto mais significativo de desempenho hello. |
| Média |Recomendações de médio impacto devem melhorar o desempenho, mas não substancialmente. |
| Baixo |Recomendações de baixo impacto devem fornecer um desempenho melhor do que seria obtido sem elas, mas as melhorias podem não ser significativas. |


> [!NOTE]
> Banco de dados SQL do Azure precisa de atividades toomonitor pelo menos um dia na ordem tooidentify algumas recomendações. Olá banco de dados do SQL Azure mais facilmente pode otimizar para padrões de consulta consistente que para aleatórias intermitências irregular de atividade. Se as recomendações não corrently disponível, Olá **recomendação desempenho** página fornece uma mensagem explicando o motivo.
> 

Você também pode exibir o status de saudação de operações de históricos de saudação. Selecione uma recomendação ou status toosee obter mais detalhes.

Aqui está um exemplo de recomendação "Criar o índice" hello portal do Azure.

![Criar índice](./media/sql-database-advisor-portal/sql-database-performance-recommendation.png)

## <a name="applying-recommendations"></a>Aplicando recomendações
Banco de dados do SQL Azure lhe dá controle total sobre como as recomendações são habilitadas usando qualquer um dos Olá três opções a seguir: 

* Aplicar uma recomendação individual de cada vez.
* Habilitar Olá tooautomatically ajuste automático aplicar recomendações.
* tooimplement uma recomendação manualmente, execute Olá recomendado script T-SQL no banco de dados.

Selecione qualquer recomendação tooview seus detalhes e, em seguida, clique em **exibir script** tooreview Olá detalhes exatos de como recomendação de saudação é criada.

Olá permanecerá online enquanto a recomendação de saudação é aplicada - utilização de recomendação de desempenho ou de ajuste automático nunca tem um banco de dados offline.

### <a name="apply-an-individual-recommendation"></a>Aplicar uma recomendação individual
Você pode examinar e aceitar uma recomendação de cada vez.

1. Em Olá **recomendações** folha, selecione uma recomendação.
2. Em Olá **detalhes** folha clique **aplicar** botão.
   
    ![Aplicar recomendação](./media/sql-database-advisor-portal/apply.png)

Recomendação selecionada será aplicada no banco de dados de saudação.

### <a name="removing-recommendations-from-hello-list"></a>Removendo as recomendações da lista de saudação
Se a lista de recomendações contiver itens que você deseja tooremove da lista de saudação, você pode descartar recomendação hello:

1. Selecione uma recomendação na lista de saudação do **recomendações** tooopen detalhes de saudação.
2. Clique em **descartar** em Olá **detalhes** folha.

Se desejar, você pode adicionar itens descartados fazer toohello **recomendações** lista:

1. Em Olá **recomendações** folha clique **exibição descartada**.
2. Selecione um item descartado Olá lista tooview seus detalhes.
3. Opcionalmente, clique em **desfazer descartar** tooadd Olá índice toohello back lista principal de **recomendações**.


### <a name="enable-automatic-tuning"></a>Habilitar o ajuste automático
Você pode definir as recomendações do hello Azure SQL Database tooimplement automaticamente. Conforme as recomendações são disponibilizadas, elas serão aplicadas automaticamente. Como com todas as recomendações gerenciadas pelo Olá serviço se Olá impacto no desempenho é recomendação negativo hello será revertido.

1. Em Olá **recomendações** folha, clique em **automatizar**:
   
    ![Configurações do supervisor](./media/sql-database-advisor-portal/settings.png)
2. Selecione tooautomate de ações:
   
    ![Índices recomendados](./media/sql-database-advisor-portal/automation.png)

### <a name="manually-run-hello-recommended-t-sql-script"></a>Executar manualmente Olá recomendado script T-SQL
Selecione qualquer recomendação e clique em **Exibir script**. Execute este script no banco de dados toomanually aplicar a recomendação de saudação.

*Índices que são executados manualmente não são monitorados e validados para impacto no desempenho pelo serviço Olá* portanto é recomendável que você monitore esses índices após a criação tooverify eles prover ganhos de desempenho e ajustar ou excluí-los se é necessário. Para obter detalhes sobre a criação de índices, consulte [CRIAR ÍNDICE (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).

### <a name="canceling-recommendations"></a>Cancelando recomendações
Recomendações que estão com status **Pendente**, **Verificando** ou **Sucesso** podem ser canceladas. Recomendações com status **Executando** não podem ser canceladas.

1. Selecione uma recomendação na Olá **histórico ajuste** Olá de tooopen área **detalhes das recomendações** folha.
2. Clique em **Cancelar** tooabort processo de saudação da aplicação de recomendação de saudação.

## <a name="monitoring-operations"></a>Monitoramento de operações
A aplicação de uma recomendação pode não acontecer instantaneamente. portal Olá fornece detalhes sobre o status de saudação da recomendação. Olá seguem possíveis estados que um índice pode estar em:

| Status | Descrição |
|:--- |:--- |
| Pendente |O comando Aplicar recomendação foi recebido e está programado para execução. |
| Executando |recomendação Hello está sendo aplicada. |
| Verificando |Recomendação foi aplicada com êxito e serviço hello está medindo benefícios hello. |
| Sucesso |A recomendação foi aplicada com êxito e benefícios foram calculados. |
| Erro |Ocorreu um erro durante o processo de saudação da aplicação de recomendação de saudação. Isso pode ser um problema temporário ou possivelmente uma tabela de toohello de alteração de esquema e o script hello não é mais válido. |
| Revertendo |recomendação de saudação foi aplicada, mas foi considerada não funcionais e está sendo revertida automaticamente. |
| Revertida |recomendação de saudação foi revertida. |

Clique em uma recomendação no processo de saudação lista toosee mais detalhes:

![Índices recomendados](./media/sql-database-advisor-portal/operations.png)

### <a name="reverting-a-recommendation"></a>Revertendo uma recomendação
Se você usou a recomendação de Olá Olá desempenho recomendações tooapply (ou seja, que você não executou manualmente script hello T-SQL) ele será automaticamente revertê-lo se ele encontrar hello toobe de impacto de desempenho negativo. Se por algum motivo você simplesmente deseja toorevert uma recomendação você pode fazer a seguir hello:

1. Selecione uma recomendação aplicada com êxito no hello **histórico de ajuste** área.
2. Clique em **Revert** em Olá **detalhes de recomendação** folha.

![Índices recomendados](./media/sql-database-advisor-portal/details.png)

## <a name="monitoring-performance-impact-of-index-recommendations"></a>Monitorando o impacto do desempenho de recomendações de índice
Depois que as recomendações são implementadas com êxito (no momento, as operações de índice e parametrizar somente recomendações de consultas) você pode clicar em **consulta Insights** em Olá recomendação detalhes folha tooopen [consulta Informações de desempenho](sql-database-query-performance.md) e ver o impacto no desempenho Olá as consultas principais.

![Monitorar o impacto do desempenho](./media/sql-database-advisor-portal/query-insights.png)

## <a name="summary"></a>Resumo
O Banco de Dados SQL do Azure fornece recomendações para aprimorar o desempenho do bancos de dados SQL. Ao fornecer scripts T-SQL, além de individuais e totalmente automáticos, você obtém uma assistência útil ao otimizar seu banco de dados e, como resultado final, melhorar o desempenho da consulta.

## <a name="next-steps"></a>Próximas etapas
Monitorar suas recomendações e continuar tooapply-los toorefine desempenho. Cargas de trabalho de banco de dados são dinâmicas e mudam continuamente. Banco de dados SQL do Azure continuará toomonitor e fornece recomendações que potencialmente podem melhorar o desempenho de seu banco de dados. 

* Consulte [ajuste automático](sql-database-automatic-tuning.md) toolearn mais sobre Olá ajuste automático no banco de dados do SQL Azure.
* Consulte [Recomendações de desempenho](sql-database-advisor.md) para obter uma visão geral das recomendações de desempenho do Banco de Dados SQL do Azure.
* Consulte [Query Performance Insight](sql-database-query-performance.md) toolearn sobre como exibir o impacto no desempenho Olá as consultas principais.

## <a name="additional-resources"></a>Recursos adicionais
* [Repositório de Consultas](https://msdn.microsoft.com/library/dn817826.aspx)
* [CREATE INDEX](https://msdn.microsoft.com/library/ms188783.aspx)
* [Controle de acesso baseado em função](../active-directory/role-based-access-control-what-is.md)

