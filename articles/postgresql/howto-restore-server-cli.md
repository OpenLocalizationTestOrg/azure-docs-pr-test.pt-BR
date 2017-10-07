---
title: Como tooback backup e restaurar um servidor no banco de dados do Azure para PostgreSQL | Microsoft Docs
description: "Saiba como tooback backup e restauração de um servidor de banco de dados do Azure para PostgreSQL usando Olá CLI do Azure."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 0b9ed25e3e3a88dd5c7ffe2ae7c27f8eef9be710
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooback-up-and-restore-a-server-in-azure-database-for-postgresql-by-using-hello-azure-cli"></a>Como tooback backup e restauração de um servidor de banco de dados do Azure para PostgreSQL usando Olá CLI do Azure

Use banco de dados PostgreSQL toorestore um tooan de banco de dados do servidor data anterior que abrange de 7 dias too35.

## <a name="prerequisites"></a>Pré-requisitos
toocomplete tooguide esse como, você precisa:
- Um [Banco de Dados do Azure para servidor e banco de dados PostgreSQL](quickstart-create-server-database-azure-cli.md)

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

 

> [!IMPORTANT]
> Se você instala e usa o hello CLI do Azure localmente, esse tooguide como requer que você use a CLI do Azure versão 2.0 ou posterior. versão de hello tooconfirm, no prompt de comando CLI do Azure hello, digite `az --version`. tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).

## <a name="back-up-happens-automatically"></a>O backup ocorre automaticamente
Quando você usa o banco de dados do Azure para PostgreSQL, o serviço de banco de dados de saudação torna automaticamente um backup do serviço de saudação a cada 5 minutos. 

Para a camada básica, os backups de saudação estão disponíveis para 7 dias. Para a camada padrão, os backups de saudação estão disponíveis para 35 dias. Para saber mais, confira [Tipos de preço do Banco de Dados do Azure para PostgreSQL](concepts-service-tiers.md).

Com esse recurso de backup automático, você pode restaurar o servidor de saudação e tooan seus bancos de dados data anterior ou ponto no tempo.

## <a name="restore-a-database-tooa-previous-point-in-time-by-using-hello-azure-cli"></a>Restaurar um ponto anterior do banco de dados tooa no tempo usando Olá CLI do Azure
Usar banco de dados do Azure para PostgreSQL toorestore Olá server tooa ponto anterior no tempo. dados saudação restaurado são copiado tooa novo servidor e servidor de saudação existente será deixado como está. Por exemplo, se uma tabela for descartada acidentalmente ao meio-dia hoje, você pode restaurar toohello tempo antes de meio-dia. Em seguida, você pode recuperar Olá ausente da tabela e dados de cópia de saudação restaurada do servidor de saudação. 

servidor de saudação toorestore, use Olá CLI do Azure [restauração do servidor postgres az](/cli/azure/postgres/server#restore) comando.

### <a name="run-hello-restore-command"></a>Execute o comando restore Olá

servidor de saudação toorestore, no prompt de comando CLI do Azure hello, digite Olá comando a seguir:

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

Olá `az postgres server restore` comando requer Olá parâmetros a seguir:
| Configuração | Valor sugerido | Descrição  |
| --- | --- | --- |
| resource-group |  myResourceGroup |  O grupo de recursos onde o servidor de origem de saudação existe.  |
| name | restaurado mypgserver | nome de Olá do novo servidor de saudação é criado pelo comando de restauração de saudação. |
| Restauração-point-in-time | 2017-04-13T13:59:00Z | Selecione um ponto no tempo toorestore para. A data e a hora devem estar dentro de saudação do servidor de origem período de retenção de backup. Use o formato de data e hora Olá ISO8601. Por exemplo, você pode usar seu fuso horário local, como `2017-04-13T05:59:00-08:00`. Você também pode usar o hello formato UTC Zulu, por exemplo, `2017-04-13T13:59:00Z`. |
| source-server | mypgserver-20170401 | nome de saudação ou ID do hello toorestore de servidor de origem do. |

Quando você restaurar um servidor tooan ponto anterior no tempo, um novo servidor é criado. servidor de saudação original e seus bancos de dados de saudação especificado ponto no tempo são copiados toohello novo servidor.

Olá local e preços de valores de nível para o servidor de saudação restaurado permanecer Olá mesmo o como servidor de saudação original. 

Olá `az postgres server restore` comando é síncrono. Depois que o servidor de saudação é restaurado, você pode usá-la novamente toorepeat Olá processo para outro ponto no tempo. 

Depois de saudação conclusão do processo de restauração, localize o novo servidor de saudação e verificar se os dados de saudação são restaurados conforme o esperado.

## <a name="next-steps"></a>Próximas etapas
[Bibliotecas de conexão para o Banco de Dados do Azure para PostgreSQL](concepts-connection-libraries.md)
