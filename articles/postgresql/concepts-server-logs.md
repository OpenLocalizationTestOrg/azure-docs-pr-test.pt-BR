---
title: aaaServer Logs no banco de dados do Azure para PostgreSQL | Microsoft Docs
description: Gera logs de erro e de consulta no Banco de Dados do Azure para PostgreSQL.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 22575f3882ce67fe640952f0a8dbfd8dcb4b16fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="server-logs-in-azure-database-for-postgresql"></a>Logs de servidor no Banco de Dados do Azure para PostgreSQL 
Banco de Dados do Azure para PostgreSQL gera logs de consulta e de erro. No entanto, não há suporte para acesso tootransaction logs. Esses logs podem ser usado tooidentify, solucionar problemas e reparar erros de configuração e desempenho abaixo do ideal. Para saber mais, confira [Relatório de erros e registro em log](https://www.postgresql.org/docs/9.6/static/runtime-config-logging.html).

## <a name="access-server-logs"></a>Acessar logs do servidor
Você pode listar e baixar logs de erro do servidor do Azure PostgreSQL usando Olá Portal do Azure, [CLI do Azure](howto-configure-server-logs-using-cli.md) e APIs REST do Azure.

## <a name="log-retention"></a>Retenção de log
Você pode definir o período de retenção de saudação para logs de sistema usando o **log\_retenção\_período** parâmetro associado a seu servidor. unidade de saudação para esse parâmetro é dias (necessário tooconfirm). valor padrão de saudação é três dias. valor máximo de saudação é 7 dias. Observe que o servidor deve ter suficiente arquivos de log do armazenamento alocado toocontain Olá retido.
arquivos de log Olá gira cada 1 hora ou um tamanho de 100MB, o que ocorrer primeiro.

## <a name="configure-logging-for-azure-postgresql-server"></a>Configurar o registro em log para o servidor PostgreSQL do Azure
Você pode habilitar os registros em log de consulta e de erro para seu servidor. Os logs de erros podem conter informações de pontos de verificação, conexão e vácuo automática.

Habilite o registro em log de consulta para sua instância de Banco de Dados PostgreSQL definindo dois parâmetros de servidor: \_statement e log\_min\_duration\_statement.

Olá **log\_instrução** parâmetro controla quais instruções SQL são registradas. É recomendável definir esse parâmetro muito***todos os*** toolog todas as instruções; valor de padrão de saudação é none (necessário tooconfirm).

Olá **log\_min\_duração\_instrução** parâmetro define o limite de saudação em milissegundos, de um toobe de instrução conectado. Todas as instruções SQL que são executados mais do que a configuração de parâmetro hello são registradas. Esse parâmetro é desabilitada e defina toominus 1 (-1) por padrão (necessidade tooconfirm). A habilitação desse parâmetro pode ser útil para rastrear consultas não otimizadas em seus aplicativos.

Olá **log\_min\_mensagens** permite que você toocontrol quais níveis de mensagem são gravados toohello log do servidor. padrão de saudação é de aviso. (necessário tooconfirm)

Para saber mais sobre essas configurações, consulte a documentação [Relatório de erros e registro em log](https://www.postgresql.org/docs/9.6/static/runtime-config-logging.html). Para configurar especificamente os parâmetros do Banco de Dados do Azure para servidor PostgreSQL, consulte [Logs de servidor no Banco de Dados para PostgreSQL](concepts-server-logs.md).

## <a name="next-steps"></a>Próximas etapas
- logs de tooaccess usando a interface de linha de comando CLI do Azure, consulte [acesso e configurar logs de servidor usando a CLI do Azure](howto-configure-server-logs-using-cli.md)
- Para saber mais sobre os parâmetros de servidor, consulte [Personalizar os parâmetros de configuração de servidor usando a CLI do Azure](howto-configure-server-parameters-using-cli.md).