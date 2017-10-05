---
title: Logs de servidor no Banco de Dados do Azure para PostgreSQL | Microsoft Docs
description: Gera logs de erro e de consulta no Banco de Dados do Azure para PostgreSQL.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 10f6c490a4fdb4c70cb80b035eaebb9d2ad2e699
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="server-logs-in-azure-database-for-postgresql"></a>Logs de servidor no Banco de Dados do Azure para PostgreSQL 
Banco de Dados do Azure para PostgreSQL gera logs de consulta e de erro. No entanto, não há suporte para acesso aos logs de transação. Esses logs podem ser usados para identificar, solucionar problemas e reparar erros de configuração e desempenho abaixo do ideal. Para saber mais, confira [Relatório de erros e registro em log](https://www.postgresql.org/docs/9.6/static/runtime-config-logging.html).

## <a name="access-server-logs"></a>Acessar logs do servidor
Você pode listar e baixar logs de erro do servidor PostgreSQL do Azure usando o Portal do Azure, a [CLI do Azure](howto-configure-server-logs-using-cli.md) e as APIs REST do Azure.

## <a name="log-retention"></a>Retenção de log
Você pode definir o período de retenção para logs do sistema usando o parâmetro **log\_retention\_period** associado ao seu servidor. A unidade para esse parâmetro é dias (é preciso confirmar). O valor padrão são três dias. O valor máximo são sete dias. Observe que o servidor deve ter um armazenamento alocado suficiente para conter os arquivos de log mantidos.
Os arquivos de log farão um rodízio a cada uma hora ou a cada 100 MB, o que ocorrer primeiro.

## <a name="configure-logging-for-azure-postgresql-server"></a>Configurar o registro em log para o servidor PostgreSQL do Azure
Você pode habilitar os registros em log de consulta e de erro para seu servidor. Os logs de erros podem conter informações de pontos de verificação, conexão e vácuo automática.

Habilite o registro em log de consulta para sua instância de Banco de Dados PostgreSQL definindo dois parâmetros de servidor: \_statement e log\_min\_duration\_statement.

O parâmetro **log\_statement** controla quais instruções SQL são registradas. Recomendamos a definição desse parâmetro como ***all*** para registrar todas as instruções; o valor padrão é nenhum (é preciso confirmar).

O parâmetro **log\_min\_duration\_statement** define o limite em milissegundos para o registro de uma instrução. Todas as instruções SQL cuja execução demorar mais do que a configuração do parâmetro serão registradas. Esse parâmetro é desabilitado e definido como menos um (-1) por padrão (é preciso confirmar). A habilitação desse parâmetro pode ser útil para rastrear consultas não otimizadas em seus aplicativos.

**log\_min\_messages** permite a você controlar quais níveis de mensagem são gravados no log de servidor. O padrão é WARNING. (é preciso confirmar)

Para saber mais sobre essas configurações, consulte a documentação [Relatório de erros e registro em log](https://www.postgresql.org/docs/9.6/static/runtime-config-logging.html). Para configurar especificamente os parâmetros do Banco de Dados do Azure para servidor PostgreSQL, consulte [Logs de servidor no Banco de Dados para PostgreSQL](concepts-server-logs.md).

## <a name="next-steps"></a>Próximas etapas
- Para acessar os logs usando a CLI (interface de linha de comando ) do Azure, consulte [Configurar e acessar os logs de servidor usando a CLI do Azure](howto-configure-server-logs-using-cli.md)
- Para saber mais sobre os parâmetros de servidor, consulte [Personalizar os parâmetros de configuração de servidor usando a CLI do Azure](howto-configure-server-parameters-using-cli.md).