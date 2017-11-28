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
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-postgresql-using-hello-azure-portal"></a><span data-ttu-id="da0c7-103">Como tooBackup e restauração de um servidor no banco de dados do Azure para usar PostgreSQL Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="da0c7-103">How tooBackup and Restore a server in Azure Database for PostgreSQL using hello Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="da0c7-104">O backup ocorre automaticamente</span><span class="sxs-lookup"><span data-stu-id="da0c7-104">Backup happens Automatically</span></span>
<span data-ttu-id="da0c7-105">Ao usar o banco de dados do Azure para PostgreSQL, o serviço de banco de dados de saudação torna automaticamente um backup do serviço de saudação a cada 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="da0c7-105">When using Azure Database for PostgreSQL, hello database service automatically makes a backup of hello service every 5 minutes.</span></span> 

<span data-ttu-id="da0c7-106">backups de saudação estão disponíveis para 7 dias, ao usar a camada básica e 35 dias ao usar a camada padrão.</span><span class="sxs-lookup"><span data-stu-id="da0c7-106">hello backups are available for 7 days when using Basic Tier, and 35 days when using Standard Tier.</span></span> <span data-ttu-id="da0c7-107">Para saber mais, confira [Camadas do Banco de Dados do Azure para PostgreSQL](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="da0c7-107">For more information, see [Azure Database for PostgreSQL service tiers](concepts-service-tiers.md)</span></span>

<span data-ttu-id="da0c7-108">Usando esse recurso de backup automático poderá restaurar o servidor de saudação e todos os seus bancos de dados em um novo servidor tooan anteriormente point-in-time.</span><span class="sxs-lookup"><span data-stu-id="da0c7-108">Using this automatic backup feature you may restore hello server and all its databases into a new server tooan earlier point-in-time.</span></span>

## <a name="restore-in-hello-azure-portal"></a><span data-ttu-id="da0c7-109">Restaurar Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="da0c7-109">Restore in hello Azure portal</span></span>
<span data-ttu-id="da0c7-110">Banco de dados do Azure para PostgreSQL permite que você toorestore Olá server tooa back ponto no tempo e em tooa nova cópia do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="da0c7-110">Azure Database for PostgreSQL allows you toorestore hello server back tooa point in time and into tooa new copy of hello server.</span></span> <span data-ttu-id="da0c7-111">Você pode usar esse novo toorecover de servidor a seus dados.</span><span class="sxs-lookup"><span data-stu-id="da0c7-111">You can use this new server toorecover your data.</span></span> 

<span data-ttu-id="da0c7-112">Por exemplo, se uma tabela tiver sido acidentalmente descartada ao meio-dia de hoje, você pode restaurar toohello tempo antes de meio-dia e recuperar Olá ausente e os dados dessa nova cópia do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="da0c7-112">For example, if a table was accidentally dropped at noon today, you could restore toohello time just before noon and retrieve hello missing table and data from that new copy of hello server.</span></span>

<span data-ttu-id="da0c7-113">Hello seguinte ponto de restauração Olá exemplo server tooa tempo:</span><span class="sxs-lookup"><span data-stu-id="da0c7-113">hello following steps restore hello sample server tooa point in time:</span></span>
1. <span data-ttu-id="da0c7-114">O logon no hello [portal do Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="da0c7-114">Sign into hello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="da0c7-115">Localize seu servidor de Banco de Dados do Azure para PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="da0c7-115">Locate your Azure Database for PostgreSQL server.</span></span> <span data-ttu-id="da0c7-116">No portal do Azure de Olá, clique em **todos os recursos** do menu esquerdo hello e digite nome hello, como **mypgserver 20170401**, toosearch de seu servidor existente.</span><span class="sxs-lookup"><span data-stu-id="da0c7-116">In hello Azure portal, click **All Resources** from hello left-hand menu and type in hello name, such as **mypgserver-20170401**, toosearch for your existing server.</span></span> <span data-ttu-id="da0c7-117">Clique em nome do servidor de saudação listado no resultado da pesquisa hello.</span><span class="sxs-lookup"><span data-stu-id="da0c7-117">Click hello server name listed in hello search result.</span></span> <span data-ttu-id="da0c7-118">Olá **visão geral** página para o servidor é aberta e oferece opções de configuração adicional.</span><span class="sxs-lookup"><span data-stu-id="da0c7-118">hello **Overview** page for your server opens and provides options for further configuration.</span></span>

   ![Portal do Azure - pesquisar toolocate seu servidor](media/postgresql-howto-restore-server-portal/1-locate.png)

3. <span data-ttu-id="da0c7-120">Na parte superior de saudação da folha de visão geral do servidor de saudação, clique em **restaurar** na barra de ferramentas de saudação.</span><span class="sxs-lookup"><span data-stu-id="da0c7-120">On hello top of hello server overview blade, click **Restore** on hello toolbar.</span></span> <span data-ttu-id="da0c7-121">Abre a folha de restauração Hello.</span><span class="sxs-lookup"><span data-stu-id="da0c7-121">hello Restore blade opens.</span></span>

   ![Banco de Dados do Azure para PostgreSQL - Visão geral - botão Restaurar](./media/postgresql-howto-restore-server-portal/2_server.png)

4. <span data-ttu-id="da0c7-123">Preencha o formulário de restauração de saudação com informações de saudação necessárias:</span><span class="sxs-lookup"><span data-stu-id="da0c7-123">Fill out hello Restore form with hello required information:</span></span>

   ![<span data-ttu-id="da0c7-124">Banco de Dados do Azure para PostgreSQL - Informações de restauração</span><span class="sxs-lookup"><span data-stu-id="da0c7-124">Azure Database for PostgreSQL - Restore information</span></span> ](./media/postgresql-howto-restore-server-portal/3_restore.png)
  - <span data-ttu-id="da0c7-125">**Ponto de restauração**: selecione um point-in-time que ocorre antes que o servidor de saudação foi alterado</span><span class="sxs-lookup"><span data-stu-id="da0c7-125">**Restore point**: Select a point-in-time that occurs before hello server was changed</span></span>
  - <span data-ttu-id="da0c7-126">**Servidor de destino**: forneça um novo nome de servidor que você deseja toorestore para</span><span class="sxs-lookup"><span data-stu-id="da0c7-126">**Target server**: Provide a new server name you want toorestore to</span></span>
  - <span data-ttu-id="da0c7-127">**Local**: não é possível selecionar região hello, por padrão, ele é igual ao servidor de origem Olá</span><span class="sxs-lookup"><span data-stu-id="da0c7-127">**Location**: You cannot select hello region, by default it is same as hello source server</span></span>
  - <span data-ttu-id="da0c7-128">**Tipo de preço**: não é possível alterar esse valor ao restaurar um servidor.</span><span class="sxs-lookup"><span data-stu-id="da0c7-128">**Pricing tier**: You cannot change this value when restoring a server.</span></span> <span data-ttu-id="da0c7-129">É igual ao servidor de origem de saudação.</span><span class="sxs-lookup"><span data-stu-id="da0c7-129">It is same as hello source server.</span></span> 

5. <span data-ttu-id="da0c7-130">Clique em **Okey** toorestore Olá servidor toorestore tooa ponto no tempo.</span><span class="sxs-lookup"><span data-stu-id="da0c7-130">Click **OK** toorestore hello server toorestore tooa point in time.</span></span> 

6. <span data-ttu-id="da0c7-131">Quando termina de restauração Olá, localize o servidor de novo Olá criado Olá tooverify dados foi restaurados conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="da0c7-131">Once hello restore finishes, locate hello new server that is created tooverify hello data was restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="da0c7-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="da0c7-132">Next steps</span></span>
- [<span data-ttu-id="da0c7-133">Bibliotecas de conexão para o Banco de Dados do Azure para PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="da0c7-133">Connection libraries for Azure Database for PostgreSQL</span></span>](concepts-connection-libraries.md)
