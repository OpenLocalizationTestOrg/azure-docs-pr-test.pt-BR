---
title: "aaaOperating repositório de consultas no banco de dados do SQL Azure"
description: "Saiba como toooperate Olá repositório de consultas no banco de dados do SQL Azure"
keywords: 
services: sql-database
documentationcenter: 
author: bonova
manager: jhubbard
editor: 
ms.assetid: 0cccf6bd-1327-44f7-a6f9-8eff0c210463
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: sqldb-performance
ms.workload: data-management
ms.date: 11/08/2016
ms.author: bonova
ms.openlocfilehash: ab741e49685bf6df3bceab219aaf57ea51cdb25d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="operating-hello-query-store-in-azure-sql-database"></a>Olá operacional repositório de consultas no banco de dados do SQL Azure
O Repositório de Consultas no Azure é um recurso de banco de dados totalmente gerenciado que continuamente coleta e apresenta informações históricas sobre todas as consultas. Você pode pensar sobre o repositório de consultas como gravador de dados de voo do avião tooan semelhante que significativamente simplifica a solução de problemas para a nuvem de desempenho de consulta e os clientes no local. Este artigo explica os aspectos específicos da operação de Repositório de Consultas no Azure. Usando esta consulta de dados previamente coletados, você pode diagnosticar e resolver problemas de desempenho rapidamente e, portanto, gastar mais tempo concentrando-se em seus negócios. 

O Repositório de Consultas ficou [disponível globalmente](https://azure.microsoft.com/updates/general-availability-azure-sql-database-query-store/) no Banco de Dados SQL do Azure desde novembro de 2015. Repositório de consultas é a base de saudação para análise de desempenho e otimização de recursos, tais como [orientador de banco de dados SQL e painel de desempenho](https://azure.microsoft.com/updates/sqldatabaseadvisorga/). No momento de saudação da publicação deste artigo, o repositório de consultas está em execução em mais de 200.000 bancos de dados de usuário no Azure, coletando informações relacionadas à consulta para vários meses, sem interrupção.

> [!IMPORTANT]
> A Microsoft está no processo de saudação de ativação de repositório de consultas para bancos de dados do SQL Azure todos (novos e existentes). 
> 
> 

## <a name="optimal-query-store-configuration"></a>Configuração do Repositório de Consulta ideais
Esta seção descreve os padrões de configuração ideal que são uma operação confiável tooensure projetado de repositório de consultas hello e recursos dependentes, tais como [orientador de banco de dados SQL e painel de desempenho](https://azure.microsoft.com/updates/sqldatabaseadvisorga/). A configuração padrão é otimizada para coleta de dados contínua, ou seja, tempo mínimo gasto nos estados OFF/READ_ONLY.

| Configuração | Descrição | Padrão | Comentário |
| --- | --- | --- | --- |
| MAX_STORAGE_SIZE_MB |Especifica o limite de saudação para espaço de dados de saudação que pode levar o repositório de consultas no banco de dados de cliente z |100 |Imposto para novos bancos de dados |
| INTERVAL_LENGTH_MINUTES |Define o tamanho da janela de tempo durante o qual as estatísticas de tempo de execução coletadas para planos de consulta são agregadas e persistidas. Cada plano de consulta ativa tem no máximo uma linha por um período de tempo definido com esta configuração |60 |Imposto para novos bancos de dados |
| STALE_QUERY_THRESHOLD_DAYS |Política de limpeza com base no tempo que controla o período de retenção de saudação de estatísticas de tempo de execução persistentes e consultas inativas |30 |Imposto para novos bancos de dados e bancos de dados padrão anteriores (367) |
| SIZE_BASED_CLEANUP_MODE |Especifica se a limpeza automática de dados ocorre quando o limite de saudação se aproximar do tamanho de dados de repositório de consultas |AUTO |Imposto para todos os bancos de dados |
| QUERY_CAPTURE_MODE |Especifica se todas as consultas ou apenas um subconjunto de consultas será controlado |AUTO |Imposto para todos os bancos de dados |
| FLUSH_INTERVAL_SECONDS |Especifica o período máximo durante o qual estatísticas capturadas de tempo de execução são mantidas na memória, antes de liberar toodisk |900 |Imposto para novos bancos de dados |
|  | | | |

> [!IMPORTANT]
> Esses padrões são aplicados automaticamente no estágio final de saudação de ativação de repositório de consultas em todos os bancos de dados do SQL Azure (consulte a observação importante anterior). Após essa luz backup, banco de dados do SQL Azure não será alterada valores de configuração definidos por clientes, a menos que eles afetarem negativamente a carga de trabalho primária ou operações confiáveis de saudação repositório de consultas.
> 
> 

Se você quiser toostay com as configurações personalizadas, use [ALTER DATABASE com as opções de repositório de consultas](https://msdn.microsoft.com/library/bb522682.aspx) estado anterior da configuração do toorevert toohello. Check-out [práticas recomendadas com hello repositório de consultas](https://msdn.microsoft.com/library/mt604821.aspx) em ordem toolearn superior como escolher parâmetros de configuração ideal.

## <a name="next-steps"></a>Próximas etapas
[Análise de Desempenho de Banco de Dados SQL](sql-database-performance.md)

## <a name="additional-resources"></a>Recursos adicionais
Para mais informações, consulte Olá artigos a seguir:

* [Uma caixa-preta de bordo para seu banco de dados](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database) 
* [Monitoramento de desempenho, usando o repositório de consultas Olá](https://msdn.microsoft.com/library/dn817826.aspx)
* [Cenários de Uso do Repositório de Consultas](https://msdn.microsoft.com/library/mt614796.aspx)
* [Monitoramento de desempenho, usando o repositório de consultas Olá](https://msdn.microsoft.com/library/dn817826.aspx) 

