---
title: aaaHow tooRestore um servidor de banco de dados do Azure para MySQL | Microsoft Docs
description: "Este artigo descreve como toorestore um servidor no banco de dados do Azure para MySQL usando Olá portal do Azure."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 4b990d5b37c5d4924de9571192b923e3c81094ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-mysql-using-hello-azure-portal"></a>Como tooBackup e restauração de um servidor no banco de dados do Azure para MySQL usando Olá portal do Azure

## <a name="backup-happens-automatically"></a>O backup ocorre automaticamente
Ao usar o banco de dados do Azure para MySQL, o serviço de banco de dados de saudação torna automaticamente um backup do serviço de saudação a cada 5 minutos. 

backups de saudação estão disponíveis para 7 dias, ao usar a camada básica e 35 dias ao usar a camada padrão. Para saber mais, confira [Camadas do Banco de Dados do Azure para MySQL](concepts-service-tiers.md)

Usando esse recurso de backup automático poderá restaurar o servidor de saudação e todos os seus bancos de dados em um novo servidor tooan anteriormente point-in-time.

## <a name="restore-in-hello-azure-portal"></a>Restaurar Olá portal do Azure
Banco de dados do Azure para MySQL permite toorestore Olá server tooa back ponto no tempo e em tooa nova cópia do servidor de saudação. Você pode usar esse novo toorecover de servidor a seus dados. 

Por exemplo, se uma tabela tiver sido acidentalmente descartada ao meio-dia de hoje, você pode restaurar toohello tempo antes de meio-dia e recuperar Olá ausente e os dados dessa nova cópia do servidor de saudação.

Hello seguinte ponto de restauração Olá exemplo server tooa tempo:

1. O logon no hello [portal do Azure](https://portal.azure.com/)

2. Localizar seu servidor de Banco de Dados do Azure para MySQL. No painel esquerdo do hello, selecione **todos os recursos**, selecione o servidor na lista de saudação.

3.  Na parte superior de saudação da folha de visão geral do servidor de saudação, clique em **restaurar** na barra de ferramentas de saudação. Abre a folha de restauração Hello.
![clique no botão restaurar](./media/howto-restore-server-portal/click-restore-button.png)

4. Preencha o formulário de restauração de saudação com informações de saudação necessárias:

- **(UTC) do ponto de restauração**: usando o seletor de data hello e seletor de tempo, selecione um toorestore point-in-time para. tempo de saudação especificado está em formato UTC, portanto, você provavelmente precisa tooconvert Olá local hora em UTC.
- **Restaurar o servidor toonew**: forneça um novo servidor de nome toorestore saudação do servidor existente no.
- **Local**: opção de região Olá automaticamente preenche com a região de servidor de origem Olá e não pode ser alterada.
- **Camada de preços**: Olá escolha da camada de preços automaticamente preenche com hello preços do mesmo nível como servidor de origem Olá e não podem ser alteradas aqui. 
![Restauração PITR](./media/howto-restore-server-portal/pitr-restore.png)

5. Clique em **Okey** toorestore Olá servidor toorestore tooa ponto no tempo. 

6. Após a conclusão da restauração hello, localize o servidor de novo Olá criado Olá tooverify bancos de dados foram restaurados como esperado.

## <a name="next-steps"></a>Próximas etapas
- [Bibliotecas de conexão para o Banco de Dados do Azure para MySQL](concepts-connection-libraries.md)