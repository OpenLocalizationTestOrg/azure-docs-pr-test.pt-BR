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
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-mysql-using-hello-azure-portal"></a><span data-ttu-id="1597e-103">Como tooBackup e restauração de um servidor no banco de dados do Azure para MySQL usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1597e-103">How tooBackup and Restore a server in Azure Database for MySQL using hello Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="1597e-104">O backup ocorre automaticamente</span><span class="sxs-lookup"><span data-stu-id="1597e-104">Backup happens Automatically</span></span>
<span data-ttu-id="1597e-105">Ao usar o banco de dados do Azure para MySQL, o serviço de banco de dados de saudação torna automaticamente um backup do serviço de saudação a cada 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="1597e-105">When using Azure Database for MySQL, hello database service automatically makes a backup of hello service every 5 minutes.</span></span> 

<span data-ttu-id="1597e-106">backups de saudação estão disponíveis para 7 dias, ao usar a camada básica e 35 dias ao usar a camada padrão.</span><span class="sxs-lookup"><span data-stu-id="1597e-106">hello backups are available for 7 days when using Basic Tier, and 35 days when using Standard Tier.</span></span> <span data-ttu-id="1597e-107">Para saber mais, confira [Camadas do Banco de Dados do Azure para MySQL](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="1597e-107">For more information, see [Azure Database for MySQL service tiers](concepts-service-tiers.md)</span></span>

<span data-ttu-id="1597e-108">Usando esse recurso de backup automático poderá restaurar o servidor de saudação e todos os seus bancos de dados em um novo servidor tooan anteriormente point-in-time.</span><span class="sxs-lookup"><span data-stu-id="1597e-108">Using this automatic backup feature you may restore hello server and all its databases into a new server tooan earlier point-in-time.</span></span>

## <a name="restore-in-hello-azure-portal"></a><span data-ttu-id="1597e-109">Restaurar Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1597e-109">Restore in hello Azure portal</span></span>
<span data-ttu-id="1597e-110">Banco de dados do Azure para MySQL permite toorestore Olá server tooa back ponto no tempo e em tooa nova cópia do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="1597e-110">Azure Database for MySQL allows you toorestore hello server back tooa point in time and into tooa new copy of hello server.</span></span> <span data-ttu-id="1597e-111">Você pode usar esse novo toorecover de servidor a seus dados.</span><span class="sxs-lookup"><span data-stu-id="1597e-111">You can use this new server toorecover your data.</span></span> 

<span data-ttu-id="1597e-112">Por exemplo, se uma tabela tiver sido acidentalmente descartada ao meio-dia de hoje, você pode restaurar toohello tempo antes de meio-dia e recuperar Olá ausente e os dados dessa nova cópia do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="1597e-112">For example, if a table was accidentally dropped at noon today, you could restore toohello time just before noon and retrieve hello missing table and data from that new copy of hello server.</span></span>

<span data-ttu-id="1597e-113">Hello seguinte ponto de restauração Olá exemplo server tooa tempo:</span><span class="sxs-lookup"><span data-stu-id="1597e-113">hello following steps restore hello sample server tooa point in time:</span></span>

1. <span data-ttu-id="1597e-114">O logon no hello [portal do Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="1597e-114">Sign into hello [Azure portal](https://portal.azure.com/)</span></span>

2. <span data-ttu-id="1597e-115">Localizar seu servidor de Banco de Dados do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="1597e-115">Locate your Azure Database for MySQL server.</span></span> <span data-ttu-id="1597e-116">No painel esquerdo do hello, selecione **todos os recursos**, selecione o servidor na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="1597e-116">In hello left pane, select **All resources**, then select your server from hello list.</span></span>

3.  <span data-ttu-id="1597e-117">Na parte superior de saudação da folha de visão geral do servidor de saudação, clique em **restaurar** na barra de ferramentas de saudação.</span><span class="sxs-lookup"><span data-stu-id="1597e-117">On hello top of hello server overview blade, click **Restore** on hello toolbar.</span></span> <span data-ttu-id="1597e-118">Abre a folha de restauração Hello.</span><span class="sxs-lookup"><span data-stu-id="1597e-118">hello Restore blade opens.</span></span>
<span data-ttu-id="1597e-119">![clique no botão restaurar](./media/howto-restore-server-portal/click-restore-button.png)</span><span class="sxs-lookup"><span data-stu-id="1597e-119">![click restore button](./media/howto-restore-server-portal/click-restore-button.png)</span></span>

4. <span data-ttu-id="1597e-120">Preencha o formulário de restauração de saudação com informações de saudação necessárias:</span><span class="sxs-lookup"><span data-stu-id="1597e-120">Fill out hello Restore form with hello required information:</span></span>

- <span data-ttu-id="1597e-121">**(UTC) do ponto de restauração**: usando o seletor de data hello e seletor de tempo, selecione um toorestore point-in-time para.</span><span class="sxs-lookup"><span data-stu-id="1597e-121">**Restore point (UTC)**: Using hello Date picker and time picker, select a point-in-time toorestore to.</span></span> <span data-ttu-id="1597e-122">tempo de saudação especificado está em formato UTC, portanto, você provavelmente precisa tooconvert Olá local hora em UTC.</span><span class="sxs-lookup"><span data-stu-id="1597e-122">hello time specified is in UTC format, so you likely need tooconvert hello local time into UTC.</span></span>
- <span data-ttu-id="1597e-123">**Restaurar o servidor toonew**: forneça um novo servidor de nome toorestore saudação do servidor existente no.</span><span class="sxs-lookup"><span data-stu-id="1597e-123">**Restore toonew server**: Provide a new server name toorestore hello existing server into.</span></span>
- <span data-ttu-id="1597e-124">**Local**: opção de região Olá automaticamente preenche com a região de servidor de origem Olá e não pode ser alterada.</span><span class="sxs-lookup"><span data-stu-id="1597e-124">**Location**: hello region choice automatically populates with hello source server region, and cannot be changed.</span></span>
- <span data-ttu-id="1597e-125">**Camada de preços**: Olá escolha da camada de preços automaticamente preenche com hello preços do mesmo nível como servidor de origem Olá e não podem ser alteradas aqui.</span><span class="sxs-lookup"><span data-stu-id="1597e-125">**Pricing tier**: hello pricing tier choice automatically populates with hello same pricing tier as hello source server, and cannot be changed here.</span></span> 
<span data-ttu-id="1597e-126">![Restauração PITR](./media/howto-restore-server-portal/pitr-restore.png)</span><span class="sxs-lookup"><span data-stu-id="1597e-126">![PITR Restore](./media/howto-restore-server-portal/pitr-restore.png)</span></span>

5. <span data-ttu-id="1597e-127">Clique em **Okey** toorestore Olá servidor toorestore tooa ponto no tempo.</span><span class="sxs-lookup"><span data-stu-id="1597e-127">Click **OK** toorestore hello server toorestore tooa point in time.</span></span> 

6. <span data-ttu-id="1597e-128">Após a conclusão da restauração hello, localize o servidor de novo Olá criado Olá tooverify bancos de dados foram restaurados como esperado.</span><span class="sxs-lookup"><span data-stu-id="1597e-128">After hello restore finishes, locate hello new server that was created tooverify hello databases were restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1597e-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1597e-129">Next steps</span></span>
- [<span data-ttu-id="1597e-130">Bibliotecas de conexão para o Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="1597e-130">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)