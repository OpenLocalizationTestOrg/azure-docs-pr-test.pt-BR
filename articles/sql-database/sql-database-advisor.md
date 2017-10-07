---
title: "recomendações de aaaPerformance - banco de dados do SQL Azure | Microsoft Docs"
description: "Olá banco de dados do SQL Azure fornece recomendações para bancos de dados SQL que pode melhorar o desempenho da consulta atual."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: 1db441ff-58f5-45da-8d38-b54dc2aa6145
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 77db338a0a395aec78c9e02849ae5ba4f2d01680
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-recommendations"></a>Recomendações do desempenho

Banco de dados do SQL Azure aprende e se adapta ao seu aplicativo e fornece recomendações personalizadas, permitindo que você toomaximize desempenho de saudação de bancos de dados SQL. O desempenho é avaliado continuamente analisando seu histórico de uso do Banco de Dados SQL. recomendações de saudação fornecidos baseiam-se em um padrão de carga de trabalho exclusivo do banco de dados e ajudam a melhorar o desempenho.

> [!NOTE]
> A maneira recomendada de usar as recomendações é habilitar o 'Ajuste automático' no banco de dados. Para obter detalhes, confira [Ajuste automático](sql-database-automatic-tuning.md).
>

## <a name="create-index-recommendations"></a>Criar recomendações de índice
Banco de dados SQL do Azure monitora consultas hello está sendo executadas continuamente e identifica os índices de saudação que podem melhorar o desempenho de saudação. Após haver certeza suficiente de que determinado índice está ausente, uma nova recomendação **Criar índice** será criada. Confiança de compilações de banco de dados SQL do Azure, calculando o índice de saudação do ganho de desempenho seria coloque através do tempo. Dependendo da saudação estimado de ganho de desempenho, as recomendações são categorizadas como alta, média ou baixa. 

Índices criados usando as recomendações sempre são sinalizados como índices auto_created. Você pode ver quais índices são auto_created examinando a exibição sys.indexes. Índices criados automaticamente não bloqueiam os comandos ALTER/RENAME. Se você tentar toodrop coluna de saudação um automático que criou o índice por ele, Olá comando passa e automática Olá criada o índice é descartada com o comando Olá também. Índices regulares bloquearia comando de alterar/RENOMEAR Olá em colunas que são indexados.

Depois que criar hello recomendação de índice é aplicada, banco de dados do SQL Azure irá comparar o desempenho das consultas de saudação com desempenho de linha de base de saudação. Se o novo índice colocado melhorias no desempenho hello, recomendação será sinalizada como bem-sucedida e relatório de impacto estarão disponível. No caso de índice Olá não trazem benefícios de hello, ele será revertido automaticamente. Dessa forma, o banco de dados do Azure SQL garante que o uso de recomendações, apenas melhorar o desempenho de banco de dados de saudação.

Qualquer **criar índice** recomendação tem uma política que não permite a aplicação de recomendação de saudação se o uso de DTU banco de dados ou o pool Olá estava acima de 80% em últimos 20 minutos ou se o armazenamento de saudação é acima de 90% de uso de retirada. Nesse caso, recomendação Olá será adiada.

## <a name="drop-index-recommendations"></a>Recomendações para Remover Índice
Além disso toodetecting um índice ausente, o banco de dados SQL continuamente analisa o desempenho de saudação de índices existentes. Se o índice não for usado, o banco de dados do SQL Azure recomendará cancelá-lo. Descartar um índice é recomendado em dois casos:
* O índice é uma duplicata de outro índice (mesma coluna indexada e incluída, esquema de partição e filtros)
* O índice é não utilizado por um período prolongado (93 dias)

Descarte índice recomendações também passam por verificação de saudação depois da implementação. Se o hello desempenho é melhorado relatório de impacto de saudação estará disponível. Caso uma degradação do desempenho seja detectada, a recomendação será revertida.


## <a name="parameterize-queries-recommendations"></a>Recomendações para parametrizar consultas
**Parametrizar consultas** recomendações aparecem quando você tiver uma ou mais consultas que estão constantemente sendo recompiladas mas acabam com hello mesmo plano de execução de consulta. Essa condição abre uma tooapply oportunidade forçado parametrização, que permitirá que os planos de consulta toobe armazenado em cache e reutilizado em Olá futuro, melhorando o desempenho e reduzindo o uso de recursos. 

Cada consulta emitida para o SQL Server inicialmente precisa toogenerate toobe compilado de um plano de execução. Cada plano gerado é adicionado toohello cache de plano e as execuções subsequentes da saudação mesma consulta pode reutilizar esse plano do cache hello, eliminando a necessidade de saudação para compilação adicional. 

Aplicativos que enviam consultas que incluem valores sem parâmetros, podem levar tooa sobrecarga de desempenho, onde cada tal consulta com valores de parâmetros diferentes Olá execução plano é compilado novamente. Em muitos Olá de casos mesmo consultas com parâmetros diferentes valores geram Olá mesmo planos de execução, mas esses planos ainda separadamente são adicionados toohello cache de plano. Planos de execução de recompilação usar recursos de banco de dados, aumentar Olá duração tempo e estouro Olá plano de consulta cache causando planos toobe removido do cache de saudação. Esse comportamento do SQL Server pode ser alterado definindo Olá forçado a opção parameterization no banco de dados de saudação. 

toohelp estimar o impacto de saudação dessa recomendação, são fornecidos com uma comparação entre real de CPU Olá Olá e uso projetado uso da CPU (como se recomendação Olá foi aplicada). Além disso tooCPU economia, a duração da consulta diminui para Olá tempo gasto na compilação. Também haverá menos sobrecarga no cache de plano, permitindo que a maioria dos Olá toostay no cache de planos e ser reutilizado. Você pode aplicar essa recomendação rapidamente e facilmente clicando em Olá **aplicar** comando. 

Depois que você aplicar essa recomendação, habilitar a parametrização forçada em minutos no banco de dados e começa Olá monitoramento de processo que dura cerca de 24 horas. Após esse período, você vai ser capaz de toosee Olá validação relatório que mostra o uso da CPU do seu banco de dados 24 horas antes e depois de recomendação Olá foi aplicada. Orientador de banco de dados SQL tem um mecanismo de segurança que é revertida automaticamente recomendação Olá aplicado no caso de uma regressão de desempenho foi detectada.

## <a name="fix-schema-issues-recommendations"></a>Recomendações para corrigir problemas do esquema
**Corrigir problemas de esquema** recomendações aparecem quando hello serviço de banco de dados SQL observa uma anomalia no número de saudação relacionados ao esquema de erros do SQL está ocorrendo no banco de dados SQL do Azure. Essa recomendação normalmente aparece quando seu banco de dados encontra vários erros relacionados ao esquema (nome da coluna inválido, nome do objeto inválido etc.) no período de uma hora.

"Problemas de esquema" são uma classe de erros de sintaxe no SQL Server que ocorrem quando a definição de saudação de consulta do SQL hello e definição de saudação do esquema de banco de dados de saudação não estão alinhados. Por exemplo, uma das colunas Olá esperadas pela consulta Olá poderá faltar na tabela de destino hello, ou vice-versa. 

Recomendação de "Corrigir o problema de esquema" é exibida quando o serviço do Azure SQL Database observa uma anomalia no número de saudação relacionados ao esquema de erros do SQL está ocorrendo no banco de dados SQL do Azure. Olá tabela mostra Olá erros que são relacionadas tooschema problemas a seguir:

| Código do Erro SQL | Mensagem |
| --- | --- |
| 201 |Procedimento ou função '*' espera o parâmetro '*', que não foi fornecido. |
| 207 |Nome de coluna inválido '*'. |
| 208 |Nome de objeto inválido '*'. |
| 213 |O nome da coluna ou o número de valores fornecidos não corresponde à definição da tabela. |
| 2812 |Não foi possível encontrar o procedimento armazenado '*'. |
| 8144 |Função ou procedimento * tem muitos argumentos especificados. |

## <a name="next-steps"></a>Próximas etapas
Monitorar suas recomendações e continuar tooapply-los toorefine desempenho. Cargas de trabalho de banco de dados são dinâmicas e mudam continuamente. O Supervisor de banco de dados SQL continua toomonitor e fornecer recomendações potencialmente podem melhorar o desempenho de seu banco de dados. 

* Consulte [recomendações de desempenho Olá portal do Azure](sql-database-advisor-portal.md) para obter etapas sobre como recomendações de desempenho toouse Olá portal do Azure.
* Consulte [Query Performance Insight](sql-database-query-performance.md) toolearn sobre e exibição Olá impacto no desempenho de suas principais consultas.

## <a name="additional-resources"></a>Recursos adicionais
* [Repositório de Consultas](https://msdn.microsoft.com/library/dn817826.aspx)
* [CREATE INDEX](https://msdn.microsoft.com/library/ms188783.aspx)
* [Controle de acesso baseado em função](../active-directory/role-based-access-control-what-is.md)

