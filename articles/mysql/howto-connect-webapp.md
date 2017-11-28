---
title: "Conectar um Serviço de Aplicativo do Azure existente ao Banco de Dados do Azure para MySQL | Microsoft Docs"
description: "Instruções sobre como conectar corretamente um Serviço de Aplicativo do Azure ao Banco de Dados do Azure para MySQL"
services: mysql
author: v-chenyh
ms.author: v-chenyh
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 735e21e8135d67405ec6b88d75be1711a2f071f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-an-existing-azure-app-service-to-azure-database-for-mysql-server"></a><span data-ttu-id="6f18d-103">Conectar um Serviço de Aplicativo do Azure existente ao Banco de Dados do Azure para MySQL server</span><span class="sxs-lookup"><span data-stu-id="6f18d-103">Connect an existing Azure App Service to Azure Database for MySQL server</span></span>
<span data-ttu-id="6f18d-104">Este documento explica como conectar a um Serviço de Aplicativo do Azure existente ao Banco de Dados do Azure para o servidor MySQL.</span><span class="sxs-lookup"><span data-stu-id="6f18d-104">This document explains how to connect an existing Azure App Service to your Azure Database for MySQL server.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6f18d-105">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="6f18d-105">Before you begin</span></span>
<span data-ttu-id="6f18d-106">Faça logon no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6f18d-106">Log in to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="6f18d-107">Criar um servidor de Banco de Dados do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="6f18d-107">Create an Azure Database for MySQL server.</span></span> <span data-ttu-id="6f18d-108">Para obter detalhes, confira [Como criar o Banco de Dados do Azure para servidor MySQL por meio do Portal](quickstart-create-mysql-server-database-using-azure-portal.md) ou [Como criar o Banco de Dados do Azure para servidor MySQL usando a CLI](quickstart-create-mysql-server-database-using-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="6f18d-108">For details, refer to [How to create Azure Database for MySQL server from Portal](quickstart-create-mysql-server-database-using-azure-portal.md) or [How to create Azure Database for MySQL server using CLI](quickstart-create-mysql-server-database-using-azure-cli.md).</span></span>

<span data-ttu-id="6f18d-109">Atualmente, há duas soluções para habilitar o acesso de um Serviço de Aplicativo do Azure a um Banco de Dados do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="6f18d-109">Currently there are two solutions to enable access from an Azure App Service to an Azure Database for MySQL.</span></span> <span data-ttu-id="6f18d-110">Ambas as soluções envolvem a configuração de regras de firewall de nível de servidor.</span><span class="sxs-lookup"><span data-stu-id="6f18d-110">Both solutions involve setting up server-level firewall rules.</span></span>

## <a name="solution-1---create-a-firewall-rule-to-allow-all-ips"></a><span data-ttu-id="6f18d-111">Solução 1: Criar uma regra de firewall para permitir todos os IPs</span><span class="sxs-lookup"><span data-stu-id="6f18d-111">Solution 1 - Create a firewall rule to allow all IPs</span></span>
<span data-ttu-id="6f18d-112">O Banco de Dados do Azure para MySQL fornece segurança de acesso usando um firewall para proteger os dados.</span><span class="sxs-lookup"><span data-stu-id="6f18d-112">Azure Database for MySQL provides access security using a firewall to protect your data.</span></span> <span data-ttu-id="6f18d-113">Ao se conectar de um Serviço de Aplicativo do Azure ao banco de dados para MySQL server, lembre-se de que os IPs de saída do Serviço de Aplicativo são dinâmicos por natureza.</span><span class="sxs-lookup"><span data-stu-id="6f18d-113">When connecting from an Azure App Service to Azure Database for MySQL server, keep in mind that the outbound IPs of App Service are dynamic in nature.</span></span> 

<span data-ttu-id="6f18d-114">Para garantir a disponibilidade do Serviço de Aplicativo do Azure, recomendamos o uso dessa solução para permitir TODOS os IPs.</span><span class="sxs-lookup"><span data-stu-id="6f18d-114">To ensure the availability of your Azure App Service, we recommend using this solution to allow ALL IPs.</span></span>

> [!NOTE]
> <span data-ttu-id="6f18d-115">A Microsoft está trabalhando para criar uma solução de longo prazo para evitar permitir que todos os IPs para serviços do Azure se conectem ao Banco de Dados do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="6f18d-115">Microsoft is working for a long-term solution to avoid allowing all IPs for Azure services to connect to Azure Database for MySQL.</span></span>

1. <span data-ttu-id="6f18d-116">Na folha do servidor MySQL, no título Configurações, clique em **Segurança de Conexão** para abrir a folha Segurança de Conexão para o Banco de Dados do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="6f18d-116">On the MySQL server blade, under Settings heading, click **Connection Security** to open the Connection Security blade for the Azure Database for MySQL.</span></span>

   ![Portal do Azure - clique em Segurança de Conexão](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="6f18d-118">Digite **NOME DA REGRA**, **IP INICIAL** e **IP FINAL**.</span><span class="sxs-lookup"><span data-stu-id="6f18d-118">Enter **RULE NAME**, **START IP**, and **END IP**.</span></span> <span data-ttu-id="6f18d-119">Em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="6f18d-119">Then click **Save**.</span></span>
   - <span data-ttu-id="6f18d-120">Nome da regra: Permitir-Todos os-IPs</span><span class="sxs-lookup"><span data-stu-id="6f18d-120">Rule name: Allow-All-IPs</span></span>
   - <span data-ttu-id="6f18d-121">IP inicial: 0.0.0.0</span><span class="sxs-lookup"><span data-stu-id="6f18d-121">Start IP: 0.0.0.0</span></span>
   - <span data-ttu-id="6f18d-122">IP final: 255.255.255.255</span><span class="sxs-lookup"><span data-stu-id="6f18d-122">End IP: 255.255.255.255</span></span>

   ![Portal do Azure – adicionar todos os IPs](./media/howto-connect-webapp/1_2-add-all-ips.png)

## <a name="solution-2---create-a-firewall-rule-to-explicitly-allow-outbound-ips"></a><span data-ttu-id="6f18d-124">Solução 2: Criar uma regra de firewall para permitir explicitamente IPs de saída</span><span class="sxs-lookup"><span data-stu-id="6f18d-124">Solution 2 - Create a firewall rule to explicitly allow outbound IPs</span></span>
<span data-ttu-id="6f18d-125">Você pode adicionar explicitamente todos os IPs de saída do Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="6f18d-125">You can explicitly add all the outbound IPs of your Azure App Service.</span></span>

1. <span data-ttu-id="6f18d-126">Na folha Propriedades do Serviço de Aplicativo, exiba o **ENDEREÇO IP DE SAÍDA**.</span><span class="sxs-lookup"><span data-stu-id="6f18d-126">On the App Service Properties blade, view your **OUTBOUND IP ADDRESS**.</span></span>

   ![Portal do Azure – exibir IPs de saída](./media/howto-connect-webapp/2_1-outbound-ip-address.png)

2. <span data-ttu-id="6f18d-128">Na folha Segurança de Conexão do MySQL, adicione os IPs de saída individualmente.</span><span class="sxs-lookup"><span data-stu-id="6f18d-128">On the MySQL Connection security blade, add outbound IPs one by one.</span></span>

   ![Portal do Azure – adicionar IPs explícitos](./media/howto-connect-webapp/2_2-add-explicit-ips.png)

3. <span data-ttu-id="6f18d-130">Lembre-se de **Salvar** as regras de firewall.</span><span class="sxs-lookup"><span data-stu-id="6f18d-130">Remember to **Save** your firewall rules.</span></span>

<span data-ttu-id="6f18d-131">Embora o serviço de aplicativo do Azure tente manter os endereços IP constantes ao longo do tempo, há casos em que os endereços IP podem mudar.</span><span class="sxs-lookup"><span data-stu-id="6f18d-131">Though the Azure App service attempts to keep IP addresses constant over time, there are cases where the IP addresses may change.</span></span> <span data-ttu-id="6f18d-132">Por exemplo, quando ocorre uma operação em escala, quando o aplicativo é reciclado ou quando são adicionadas novas máquinas aos data centers regionais do Azure para aumentar a capacidade.</span><span class="sxs-lookup"><span data-stu-id="6f18d-132">For example, when the app recycles or a scale operation occurs, or when new machines are added in Azure regional data centers to increase the capacity.</span></span> <span data-ttu-id="6f18d-133">Quando os endereços IP são alterados, o aplicativo pode apresentar tempo de inatividade, caso ele não possa mais se conectar ao servidor MySQL.</span><span class="sxs-lookup"><span data-stu-id="6f18d-133">When the IP addresses change, the app could experience downtime in the event it can no longer connect to the MySQL server.</span></span> <span data-ttu-id="6f18d-134">Considere esse potencial ao escolher uma das soluções anteriores.</span><span class="sxs-lookup"><span data-stu-id="6f18d-134">Consider this potential when choosing one of the preceding solutions.</span></span>

## <a name="ssl-configuration"></a><span data-ttu-id="6f18d-135">Configuração de SSL</span><span class="sxs-lookup"><span data-stu-id="6f18d-135">SSL configuration</span></span>
<span data-ttu-id="6f18d-136">O Banco de Dados do Azure para MySQL tem SSL habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="6f18d-136">Azure Database for MySQL has SSL Enabled by default.</span></span> <span data-ttu-id="6f18d-137">Se o aplicativo não estiver usando SSL para se conectar ao banco de dados, você precisará desabilitar o SSL no servidor MySQL.</span><span class="sxs-lookup"><span data-stu-id="6f18d-137">If your application is not using SSL to connect to the database, then you need to disable SSL on MySQL server.</span></span> <span data-ttu-id="6f18d-138">Para obter detalhes sobre como configurar o SSL, confira [Usar SSL com o Banco de Dados do Azure para MySQL](howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="6f18d-138">For details on how to configure SSL, See [Using SSL with Azure Database for MySQL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f18d-139">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6f18d-139">Next steps</span></span>
<span data-ttu-id="6f18d-140">Para saber mais sobre cadeias de conexão, confira [Cadeias de conexão](howto-connection-string.md).</span><span class="sxs-lookup"><span data-stu-id="6f18d-140">For more information about connection strings, refer to [Connection Strings](howto-connection-string.md).</span></span>
