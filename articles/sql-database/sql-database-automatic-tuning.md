---
title: "aaaSQL banco de dados - ajuste automático | Microsoft Docs"
description: Banco de dados SQL analisa a consulta SQL e automaticamente se adapta a carga de trabalho toouser.
services: sql-database
documentationcenter: 
author: jovanpop-msft
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: jovanpop
ms.openlocfilehash: 897a8deaabedb6727dc49958c64d0433c5f2e4f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automatic-tuning"></a>Ajuste automático

Banco de dados do SQL Azure é um serviço de dados totalmente gerenciado que monitora a consultas de saudação que são executadas no banco de dados de saudação e automaticamente podem melhorar o desempenho da carga de trabalho de saudação. Banco de dados SQL do Azure tem um mecanismo de inteligência incorporada que pode ajustar e melhorar o desempenho de suas consultas adaptando dinamicamente cargas de trabalho de tooyour de banco de dados Olá automaticamente. O ajuste automático no banco de dados do SQL Azure pode ser um dos recursos mais importantes de saudação que pode ser habilitado no desempenho do banco de dados do Azure SQL toooptimize de suas consultas.

Consulte este artigo para obter as etapas Olá muito[Ativar ajuste automático](sql-database-automatic-tuning-enable.md) usando Olá portal do Azure.

## <a name="why-automatic-tuning"></a>Por que usar o ajuste automático?

Uma das tarefas de saudação principal na administração clássico do banco de dados está monitorando a carga de trabalho Olá, identificando críticas SQL consultas, índices que devem ser adicionados tooimprove desempenho e raramente usado índices. Banco de dados SQL do Azure fornece informações detalhadas sobre as consultas de saudação e índices que você precisa toomonitor. No entanto, monitorar o banco de dados é uma tarefa difícil e entediante, especialmente ao lidar com muitos bancos de dados. Gerenciar um grande número de bancos de dados pode ser impossível toodo com eficiência mesmo com todas as ferramentas disponíveis e relatórios que fornecem banco de dados do SQL Azure e o portal do Azure. Em vez de monitorar e ajustar o banco de dados manualmente, você pode considerar delegar algumas Olá monitoramento e ajuste ações tooAzure banco de dados SQL usando o recurso de ajuste automático. 


> [!VIDEO https://channel9.msdn.com/Blogs/Azure-in-the-Enterprise/Enabling-Azure-SQL-Database-Auto-Tuning-at-Scale-for-Microsoft-IT/player]
>

## <a name="how-does-automatic-tuning-work"></a>Como funciona o trabalho de ajuste automático?

Banco de dados SQL do Azure tem um processo de análise e monitoramento de desempenho contínuo que constantemente aprende Olá característica da carga de trabalho e identificar possíveis problemas e melhorias.

![Processo de ajuste automático](./media/sql-database-automatic-tuning/tuning-process.png)

Isso permite que o processo toodynamically de banco de dados SQL adaptar carga de trabalho tooyour Localizando quais planos e índices podem melhorar o desempenho das cargas de trabalho e o que indexa afeta suas cargas de trabalho. Com base nessas conclusões, o ajuste automático aplica ações de ajuste que melhoram o desempenho da carga de trabalho. Além disso, o banco de dados do SQL Azure monitora continuamente desempenho após qualquer alteração feita pelo tooensure de ajuste automático que melhora o desempenho da carga de trabalho. Qualquer ação que não melhorar o desempenho é revertida automaticamente. Esse processo de verificação é um recurso importante que garante que qualquer alteração feita pelo ajuste automático não diminuir o desempenho de saudação da carga de trabalho.

Há dois aspectos de ajuste automático que estão disponíveis no Banco de Dados SQL do Azure:

 -  **Gerenciamento de índice automático** que identifica os índices que devem ser adicionados ao seu banco de dados e os índices que devem ser removidos.
 -  **Correção automática de plano** (em breve; já está disponível no SQL Server 2017) que identifica planos problemáticos e corrige problemas de desempenho do plano SQL .

## <a name="automatic-index-management"></a>Gerenciamento de índice automático

No Banco de Dados SQL do Azure, o gerenciamento de índice é fácil porque o Banco de Dados SQL do Azure aprende sobre sua carga de trabalho e garante que seus dados são indexados sempre da melhor forma. Um design de índice apropriado é crucial para otimizar o desempenho da carga de trabalho e o gerenciamento de índice automático pode ajudar a otimizar seus índices. Gerenciamento automático de índice pode corrigir problemas de desempenho em bancos de dados indexados incorretamente ou manter e aprimore os índices no esquema de banco de dados existente do hello. 

### <a name="why-do-you-need-index-management"></a>Por que você precisa de gerenciamento de índice?

Índices de acelerar algumas de suas consultas que leem dados de tabelas de saudação; No entanto, eles podem retardar consultas Olá que atualizam dados. Você precisa toocarefully analisar quando toocreate um índice e quais colunas são necessárias tooinclude em Olá índice. Alguns índices podem não ser mais necessários após algum tempo. Portanto, você precisaria tooperiodically identificar e remover índices de saudação que não coloque nenhum benefício. Se você ignorar Olá índices não utilizados, o desempenho das consultas de saudação que atualizam dados deve ser diminuído sem nenhum benefício em consultas de saudação que ler dados. Índices não utilizados também afetam o desempenho geral do sistema de saudação porque atualizações adicionais precisam do log desnecessário.

Localizar o conjunto ideal de saudação de índices que melhoram o desempenho de consultas de saudação que ler dados das tabelas e têm impacto mínimo sobre as atualizações pode exigir análise contínua e complexa.

Banco de dados SQL do Azure usa inteligência interna e regras avançadas para analisar suas consultas, identifique os índices que seriam ideais para suas cargas de trabalho atuais e índices Olá podem ser removidos. Banco de dados SQL do Azure garante que você tenha um conjunto mínimo necessário de índices que otimizar consultas Olá que leem dados, afetar a saudação minimizada Olá outras consultas.

### <a name="how-tooidentify-indexes-that-need-toobe-changed-in-your-database"></a>Como tooidentify índices que toobe necessidade alterado no banco de dados?

O Banco de Dados SQL do Azure facilita o processo de gerenciamento de índice. Em vez de processo entediante de saudação de carga de trabalho manual análise e monitoramento de índice, banco de dados do SQL Azure analisa sua carga de trabalho, identifica as consultas de saudação que podem ser executadas mais rapidamente com um novo índice e identifica os índices duplicados ou não utilizados. Encontre mais informações sobre a identificação de índices que devem ser alterados em [Encontrar recomendações de índice no portal do Azure](sql-database-advisor-portal.md).

### <a name="automatic-index-management-considerations"></a>Considerações sobre o gerenciamento de índice automático

Se você achar que regras internas Olá melhorar o desempenho de saudação do banco de dados, você pode permitir que banco de dados SQL do Azure gerenciar automaticamente seus índices.

Ações necessárias toocreate os índices necessários em bancos de dados do SQL Azure podem consumir recursos e temporariamente afetam o desempenho da carga de trabalho. impacto de saudação toominimize de criação de índice no desempenho da carga de trabalho, banco de dados do SQL Azure localiza a janela de tempo apropriado de saudação para qualquer operação de gerenciamento de índice. Ação de ajuste é adiada Se o banco de dados de saudação precisa tooexecute de recursos de sua carga de trabalho e iniciado quando o banco de dados de saudação tem suficiente recursos não utilizados que podem ser usados para tarefas de manutenção de saudação. Um recurso importante no gerenciamento automático de índice é uma verificação de ações de saudação. Quando o banco de dados do SQL Azure cria ou descarta o índice, um processo de monitoramento analisa o desempenho de seu tooverify de carga de trabalho que ação Olá melhor desempenho de saudação. Se ele não colocar uma melhoria significativa – ação Olá será revertida imediatamente. Dessa forma, o Banco de Dados SQL do Azure garante que as ações automáticas não afetam negativamente o desempenho da carga de trabalho. Índices criados com o ajuste automático são transparentes para a operação de manutenção Olá no esquema subjacente hello. Alterações de esquema, como remover ou renomear colunas não são bloqueadas pela presença de saudação de índices criados automaticamente. Os índices criados automaticamente pelo Banco de Dados SQL do Azure são imediatamente descartados quando a tabela ou colunas relacionadas são descartadas.

## <a name="automatic-plan-choice-correction"></a>Correção automática de escolha do plano

A correção automática de plano é um novo recurso de ajuste automático adicionado no SQL Server 2017 CTP 2.0 que identifica os planos de SQL inadequados. Essa opção de ajuste automático estará disponível em breve no Banco de Dados SQL do Azure. Veja mais informações em [Ajuste automático no SQL Server 2017](https://docs.microsoft.com/sql/relational-databases/automatic-tuning/automatic-tuning).

## <a name="next-steps"></a>Próximas etapas

- tooenable automático de ajuste no banco de dados do SQL Azure e permita automática totalmente o recurso de ajuste gerenciar sua carga de trabalho, consulte [Ativar ajuste automático](sql-database-automatic-tuning-enable.md).
- ajuste manual toouse, você pode examinar [recomendações no portal do Azure de ajuste](sql-database-advisor-portal.md) e aplicar manualmente Olá aqueles que melhoram o desempenho de suas consultas.
