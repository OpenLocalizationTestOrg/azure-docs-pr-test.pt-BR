---
title: "aaaHow tooConfigure parâmetros do servidor no banco de dados do Azure para MySQL | Microsoft Docs"
description: "Este artigo descreve como tooconfigure os parâmetros de servidor disponível no banco de dados do Azure para MySQL usando Olá portal do Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/19/2017
ms.openlocfilehash: 8292c8eda605854a06b6a9c82185c857bd353cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-server-parameters-in-azure-database-for-mysql-using-hello-azure-portal"></a>Como parâmetros de servidor tooconfigure no banco de dados do Azure para MySQL usando Olá portal do Azure

O Banco de Dados do Azure para MySQL dá suporte à configuração de alguns parâmetros de servidor. Este artigo descreve como tooconfigure esses parâmetros usando Olá portal do Azure e listas Olá suporte parâmetros, valores padrão de saudação e intervalo de saudação de valores válidos. Nem todos os parâmetros de servidor podem ser ajustados. Olá listados aqui são suportados.

## <a name="navigate-tooserver-parameters-blade-on-azure-portal"></a>Navegue tooServer folha de parâmetros no portal do Azure

Faça logon no portal do Azure de toohello, clique em seu banco de dados do Azure para o nome do servidor MySQL. Em Olá **configurações** seção, clique em **parâmetros de servidor** folha de parâmetros de servidor tooopen Olá para Olá banco de dados do Azure para MySQL.

![Folha parâmetros de servidor no portal do Azure](./media/howto-server-parameters/auzre-portal-server-parameters.png)

## <a name="list-of-configurable-server-parameters"></a>Lista de parâmetros de servidor configuráveis

Olá a tabela a seguir lista os parâmetros de servidor de saudação tem suportada no momento. parâmetros de saudação podem ser configurados de acordo com tooyour requisitos do aplicativo.

> [!div class="mx-tableFixed"]
|Nome do Parâmetro|Valor Padrão|Intervalo|Descrição|
|---|---|---|---|
|binlog_group_commit_sync_delay|1000|0, 11-1000000|Controles microssegundos quantos Olá log binário esperas de confirmação antes de sincronizar Olá toodisk de arquivo de log binário.|
|binlog_group_commit_sync_no_delay_count|0|0-1000000|número máximo de saudação do toowait de transações para antes de cancelar o atraso de saudação atual conforme especificado por binlog grupo-confirmação-sync-atraso.|
|character_set_server|LATIN1|BIG5, UTF8MB4, etc.|Use charset_name como conjunto de caracteres de servidor saudação padrão.|
|div_precision_increment|4|0-30|Número de dígitos por qual escala de saudação tooincrease do resultado de saudação de operações de divisão.|
|group_concat_max_len|1.024|4-16777216|Comprimento máximo permitido de resultados em bytes para Olá GROUP_CONCAT().|
|innodb_adaptive_hash_index|ATIVADO|ATIVADO, DESATIVADO|Indica se os índices de hash adaptáveis do innodb são habilitados ou desabilitados.|
|innodb_lock_wait_timeout|50|1-3600|comprimento de saudação de tempo em segundos uma transação de InnoDB espera para um bloqueio de linha antes de desistir.|
|interactive_timeout|1800|10-1800|Número do servidor de saudação de segundos de espera para a atividade em uma conexão interativa antes de fechá-lo.|
|log_bin_trust_function_creators|DESATIVADO|ATIVADO, DESATIVADO|Essa variável se aplica quando o log binário está habilitado. Controla se armazenado criadores podem ser uma função confiável não toocreate armazenado funções que causam toobe unsafe eventos gravado log binário toohello.|
|log_queries_not_using_indexes|DESATIVADO|ATIVADO, DESATIVADO|Consultas de logs que são esperados tooretrieve todos os logs de consulta tooslow linhas.|
|log_slow_admin_statements|DESATIVADO|ATIVADO, DESATIVADO|Inclua instruções administrativas lenta em instruções de saudação gravadas toohello log de consultas lentas.|
|log_throttle_queries_not_using_indexes|0|0-4294967295|Limites Olá número dessas consultas por minuto que podem ser gravados toohello log de consultas lentas.|
|long_query_time|10|1-1E+100|Se uma consulta leva mais tempo do que esse número de segundos, o servidor de saudação incrementa variável de status Slow_queries hello.|
|max_allowed_packet|536870912|1024-1073741824|tamanho máximo de saudação de um pacote ou qualquer cadeia de caracteres gerados/intermediário ou qualquer parâmetro enviadas pelo Olá mysql_stmt_send_long_data() função da API do C.|
|min_examined_row_limit|0|0-18446744073709551615|Registra as consultas que têm maior que Olá configurado o número de linhas no log de consultas lentas hello. |
|server_id|3293747068|1000-4294967295|ID do servidor de saudação, usado em replicação toogive cada mestre e slave uma identidade exclusiva.|
|slave_net_timeout|60|30-3600|número de saudação de toowait segundos para mais dados do mestre de saudação antes subordinado Olá considera conexão Olá quebrado, anula Olá ler e tenta tooreconnect.|
|slow_query_log|DESATIVADO|ATIVADO, DESATIVADO|Habilitar ou desabilitar o log de consultas lentas hello.|
|sql_mode|0 selecionado|ALLOW_INVALID_DATES, IGNORE_SPACE, etc.|modo SQL server atual Hello.|
|time_zone|SYSTEM|exemplos: -8:00, +05:30|Olá servidor fuso horário.|
|wait_timeout|120|60-240|número de saudação do servidor de saudação de segundos de espera para a atividade em uma conexão não interativo antes de fechá-lo.|

## <a name="next-steps"></a>Próximas etapas
- [Bibliotecas de conexão para o Banco de Dados do Azure para MySQL](concepts-connection-libraries.md)
