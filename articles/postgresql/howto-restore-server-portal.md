---
title: Como tooRestore um servidor de banco de dados do Azure para PostgreSQL | Microsoft Docs
description: "Este artigo descreve como toorestore um servidor no banco de dados do Azure para usar PostgreSQL Olá portal do Azure."
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 07/20/2017
ms.openlocfilehash: bc7351f384607397806d837afd3e1d7a26575e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-postgresql-using-hello-azure-portal"></a>Como tooBackup e restauração de um servidor no banco de dados do Azure para usar PostgreSQL Olá portal do Azure

## <a name="backup-happens-automatically"></a>O backup ocorre automaticamente
Ao usar o banco de dados do Azure para PostgreSQL, o serviço de banco de dados de saudação torna automaticamente um backup do serviço de saudação a cada 5 minutos. 

backups de saudação estão disponíveis para 7 dias, ao usar a camada básica e 35 dias ao usar a camada padrão. Para saber mais, confira [Camadas do Banco de Dados do Azure para PostgreSQL](concepts-service-tiers.md)

Usando esse recurso de backup automático poderá restaurar o servidor de saudação e todos os seus bancos de dados em um novo servidor tooan anteriormente point-in-time.

## <a name="restore-in-hello-azure-portal"></a>Restaurar Olá portal do Azure
Banco de dados do Azure para PostgreSQL permite que você toorestore Olá server tooa back ponto no tempo e em tooa nova cópia do servidor de saudação. Você pode usar esse novo toorecover de servidor a seus dados. 

Por exemplo, se uma tabela tiver sido acidentalmente descartada ao meio-dia de hoje, você pode restaurar toohello tempo antes de meio-dia e recuperar Olá ausente e os dados dessa nova cópia do servidor de saudação.

Hello seguinte ponto de restauração Olá exemplo server tooa tempo:
1. O logon no hello [portal do Azure](https://portal.azure.com/)
2. Localize seu servidor de Banco de Dados do Azure para PostgreSQL. No portal do Azure de Olá, clique em **todos os recursos** do menu esquerdo hello e digite nome hello, como **mypgserver 20170401**, toosearch de seu servidor existente. Clique em nome do servidor de saudação listado no resultado da pesquisa hello. Olá **visão geral** página para o servidor é aberta e oferece opções de configuração adicional.

   ![Portal do Azure - pesquisar toolocate seu servidor](media/postgresql-howto-restore-server-portal/1-locate.png)

3. Na parte superior de saudação da folha de visão geral do servidor de saudação, clique em **restaurar** na barra de ferramentas de saudação. Abre a folha de restauração Hello.

   ![Banco de Dados do Azure para PostgreSQL - Visão geral - botão Restaurar](./media/postgresql-howto-restore-server-portal/2_server.png)

4. Preencha o formulário de restauração de saudação com informações de saudação necessárias:

   ![Banco de Dados do Azure para PostgreSQL - Informações de restauração ](./media/postgresql-howto-restore-server-portal/3_restore.png)
  - **Ponto de restauração**: selecione um point-in-time que ocorre antes que o servidor de saudação foi alterado
  - **Servidor de destino**: forneça um novo nome de servidor que você deseja toorestore para
  - **Local**: não é possível selecionar região hello, por padrão, ele é igual ao servidor de origem Olá
  - **Tipo de preço**: não é possível alterar esse valor ao restaurar um servidor. É igual ao servidor de origem de saudação. 

5. Clique em **Okey** toorestore Olá servidor toorestore tooa ponto no tempo. 

6. Quando termina de restauração Olá, localize o servidor de novo Olá criado Olá tooverify dados foi restaurados conforme o esperado.

## <a name="next-steps"></a>Próximas etapas
- [Bibliotecas de conexão para o Banco de Dados do Azure para PostgreSQL](concepts-connection-libraries.md)
