---
title: Como restaurar um servidor no Banco de Dados do Azure para MySQL | Microsoft Docs
description: Este artigo descreve como restaurar um servidor no Banco de Dados do Azure para MySQL usando o Portal do Azure.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 8c06dce534b628a602127fd02b152c8e04e02cc4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-backup-and-restore-a-server-in-azure-database-for-mysql-using-the-azure-portal"></a><span data-ttu-id="10e25-103">Como fazer backup e restaurar um servidor no Banco de Dados do Azure para MySQL usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="10e25-103">How To Backup and Restore a server in Azure Database for MySQL using the Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="10e25-104">O backup ocorre automaticamente</span><span class="sxs-lookup"><span data-stu-id="10e25-104">Backup happens Automatically</span></span>
<span data-ttu-id="10e25-105">Ao usar o Banco de Dados para MySQL, o serviço de banco de dados faz automaticamente um backup do serviço a cada cinco minutos.</span><span class="sxs-lookup"><span data-stu-id="10e25-105">When using Azure Database for MySQL, the database service automatically makes a backup of the service every 5 minutes.</span></span> 

<span data-ttu-id="10e25-106">Os backups ficam disponíveis por sete dias ao usar a camada Basic e 35 dias ao usar a camada Standard.</span><span class="sxs-lookup"><span data-stu-id="10e25-106">The backups are available for 7 days when using Basic Tier, and 35 days when using Standard Tier.</span></span> <span data-ttu-id="10e25-107">Para saber mais, confira [Camadas do Banco de Dados do Azure para MySQL](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="10e25-107">For more information, see [Azure Database for MySQL service tiers](concepts-service-tiers.md)</span></span>

<span data-ttu-id="10e25-108">Com esse recurso de backup automático você pode restaurar o servidor e todos os seus bancos de dados em um novo servidor em um ponto anterior no tempo.</span><span class="sxs-lookup"><span data-stu-id="10e25-108">Using this automatic backup feature you may restore the server and all its databases into a new server to an earlier point-in-time.</span></span>

## <a name="restore-in-the-azure-portal"></a><span data-ttu-id="10e25-109">Restaurar no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="10e25-109">Restore in the Azure portal</span></span>
<span data-ttu-id="10e25-110">O Banco de Dados do Azure para MySQL permite a restauração do servidor em um ponto anterior no tempo e em uma nova cópia do servidor.</span><span class="sxs-lookup"><span data-stu-id="10e25-110">Azure Database for MySQL allows you to restore the server back to a point in time and into to a new copy of the server.</span></span> <span data-ttu-id="10e25-111">Use esse novo servidor para recuperar os dados.</span><span class="sxs-lookup"><span data-stu-id="10e25-111">You can use this new server to recover your data.</span></span> 

<span data-ttu-id="10e25-112">Por exemplo, se uma tabela for acidentalmente descartada ao meio-dia de hoje, você poderá restaurar em um momento logo antes do meio-dia e recuperar a tabela e os dados dessa nova cópia do servidor.</span><span class="sxs-lookup"><span data-stu-id="10e25-112">For example, if a table was accidentally dropped at noon today, you could restore to the time just before noon and retrieve the missing table and data from that new copy of the server.</span></span>

<span data-ttu-id="10e25-113">As etapas a seguir restauram o exemplo de servidor para um ponto no tempo:</span><span class="sxs-lookup"><span data-stu-id="10e25-113">The following steps restore the sample server to a point in time:</span></span>

1. <span data-ttu-id="10e25-114">Entre no [Portal do Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="10e25-114">Sign into the [Azure portal](https://portal.azure.com/)</span></span>

2. <span data-ttu-id="10e25-115">Localizar seu servidor de Banco de Dados do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="10e25-115">Locate your Azure Database for MySQL server.</span></span> <span data-ttu-id="10e25-116">No painel esquerdo, escolha **Todos os recursos**, depois selecione o servidor na lista.</span><span class="sxs-lookup"><span data-stu-id="10e25-116">In the left pane, select **All resources**, then select your server from the list.</span></span>

3.  <span data-ttu-id="10e25-117">Na parte superior da folha de visão geral do servidor, clique em **Restaurar** na barra de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="10e25-117">On the top of the server overview blade, click **Restore** on the toolbar.</span></span> <span data-ttu-id="10e25-118">A folha Restaurar é aberta.</span><span class="sxs-lookup"><span data-stu-id="10e25-118">The Restore blade opens.</span></span>
<span data-ttu-id="10e25-119">![clique no botão restaurar](./media/howto-restore-server-portal/click-restore-button.png)</span><span class="sxs-lookup"><span data-stu-id="10e25-119">![click restore button](./media/howto-restore-server-portal/click-restore-button.png)</span></span>

4. <span data-ttu-id="10e25-120">Preencha o formulário Restaurar com as informações necessárias:</span><span class="sxs-lookup"><span data-stu-id="10e25-120">Fill out the Restore form with the required information:</span></span>

- <span data-ttu-id="10e25-121">**Ponto de restauração (UTC)**: usando o seletor de data e o seletor de hora, selecione um ponto no tempo para o qual restaurar.</span><span class="sxs-lookup"><span data-stu-id="10e25-121">**Restore point (UTC)**: Using the Date picker and time picker, select a point-in-time to restore to.</span></span> <span data-ttu-id="10e25-122">A hora especificada está no formato UTC, então provavelmente você precisará converter a hora local em UTC.</span><span class="sxs-lookup"><span data-stu-id="10e25-122">The time specified is in UTC format, so you likely need to convert the local time into UTC.</span></span>
- <span data-ttu-id="10e25-123">**Restaurar em novo servidor**: forneça um novo nome de servidor no qual restaurar o servidor existente.</span><span class="sxs-lookup"><span data-stu-id="10e25-123">**Restore to new server**: Provide a new server name to restore the existing server into.</span></span>
- <span data-ttu-id="10e25-124">**Local**: a opção de região é preenchida automaticamente com a região do servidor de origem e não pode ser alterada.</span><span class="sxs-lookup"><span data-stu-id="10e25-124">**Location**: The region choice automatically populates with the source server region, and cannot be changed.</span></span>
- <span data-ttu-id="10e25-125">**Tipo de preço**: a opção de tipo de preço é preenchida automaticamente com o mesmo tipo de preço do servidor de origem e não pode ser alterada aqui.</span><span class="sxs-lookup"><span data-stu-id="10e25-125">**Pricing tier**: The pricing tier choice automatically populates with the same pricing tier as the source server, and cannot be changed here.</span></span> 
<span data-ttu-id="10e25-126">![Restauração PITR](./media/howto-restore-server-portal/pitr-restore.png)</span><span class="sxs-lookup"><span data-stu-id="10e25-126">![PITR Restore](./media/howto-restore-server-portal/pitr-restore.png)</span></span>

5. <span data-ttu-id="10e25-127">Clique em **OK** para restaurar o servidor em um ponto no tempo.</span><span class="sxs-lookup"><span data-stu-id="10e25-127">Click **OK** to restore the server to restore to a point in time.</span></span> 

6. <span data-ttu-id="10e25-128">Após a conclusão da restauração, localize o novo servidor criado para verificar se os bancos de dados foram restaurados conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="10e25-128">After the restore finishes, locate the new server that was created to verify the databases were restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="10e25-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="10e25-129">Next steps</span></span>
- [<span data-ttu-id="10e25-130">Bibliotecas de conexão para o Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="10e25-130">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)