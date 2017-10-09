---
title: logs do servidor aaaConfigure e acesso para PostgreSQL usando a CLI do Azure | Microsoft Docs
description: "Este artigo descreve como tooconfigure e acesso Olá logs do servidor no banco de dados do Azure para PostgreSQL usando a linha de comando CLI do Azure."
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 924d4e7634cc48405bcb0f813cf61d8b72ad8aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-access-server-logs-using-azure-cli"></a>Configurar e acessar logs de servidor usando a CLI do Azure
Você pode baixar os logs de erros do hello PostgreSQL server usando Olá Interface de linha de comando (CLI do Azure). No entanto, não há suporte para acesso tootransaction logs. 

## <a name="prerequisites"></a>Pré-requisitos
toostep por este tooguide como, você precisa:
- Um [servidor de Banco de Dados do Azure para PostgreSQL](quickstart-create-server-database-azure-cli.md)
- Instalar [2.0 do CLI do Azure](/cli/azure/install-azure-cli) de linha de comando utilitário ou use Olá Shell de nuvem do Azure no navegador de saudação.

## <a name="configure-logging-for-azure-database-for-postgresql"></a>Configurar o registro em log para o Banco de Dados do Azure para PostgreSQL
Você pode configurar logs de consulta Olá servidor tooaccess e logs de erros. Os logs de erros podem conter informações de pontos de verificação, conexão e vácuo automático.
1. Ativar o registro em log
2. Log de atualização\_instrução e log\_min\_duração\_log de consulta de tooenable de instrução
3. Atualizar o período de retenção

Para mais informações, confira [personalizando os parâmetros de configuração do servidor](howto-configure-server-parameters-using-cli.md).

## <a name="list-logs-for-azure-database-for-postgresql-server"></a>Liste os registros para servidor de Banco de Dados do Azure para PostgreSQL
arquivos de log disponíveis toolist Olá para o servidor, execute Olá [lista de logs do servidor postgres az](/cli/azure/postgres/server-logs#list) comando.

Você pode listar os arquivos de log Olá para o servidor **mypgserver 20170401.postgres.database.azure.com** no grupo de recursos **myresourcegroup**e direcioná-lo tooa texto arquivo chamado **log\_arquivos\_txt.**
```azurecli-interactive
az postgres server-logs list --resource-group myresourcegroup --server mypgserver-20170401 > log_files_list.txt
```
## <a name="download-logs-locally-from-hello-server"></a>Baixar os logs do servidor de saudação localmente
Olá [baixar logs de servidor az postgres](/cli/azure/postgres/server-logs#download) comando permite que os arquivos de log individuais toodownload para o servidor. 

Este exemplo hello de downloads de arquivo de log específico para o servidor de saudação **mypgserver 20170401.postgres.database.azure.com** no grupo de recursos **myresourcegroup** tooyour ambiente de local.
```azurecli-interactive
az postgres server-logs download --name 20170414-mypgserver-20170401-postgresql.log --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="next-steps"></a>Próximas etapas
- toolearn mais sobre os logs do servidor, consulte [Logs do servidor no banco de dados do Azure para PostgreSQL](concepts-server-logs.md)
- Para saber mais sobre os parâmetros de servidor, veja [Personalizar os parâmetros de configuração de servidor usando a CLI do Azure](howto-configure-server-parameters-using-cli.md)
