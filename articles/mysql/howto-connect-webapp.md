---
title: "tooAzure de serviço de aplicativo do Azure existente aaaConnect banco de dados MySQL | Microsoft Docs"
description: "Instruções sobre como tooproperly se conectar a um tooAzure de serviço de aplicativo do Azure banco de dados existente para MySQL"
services: mysql
author: v-chenyh
ms.author: v-chenyh
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 6d5b16f316e186d665370adcd8b7c7bb38c8d51a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-an-existing-azure-app-service-tooazure-database-for-mysql-server"></a><span data-ttu-id="438cc-103">Conecte-se um tooAzure do serviço de aplicativo do Azure banco de dados existente para o MySQL server</span><span class="sxs-lookup"><span data-stu-id="438cc-103">Connect an existing Azure App Service tooAzure Database for MySQL server</span></span>
<span data-ttu-id="438cc-104">Este documento explica como tooconnect uma tooyour do serviço de aplicativo do Azure existente do Azure banco de dados para o servidor MySQL.</span><span class="sxs-lookup"><span data-stu-id="438cc-104">This document explains how tooconnect an existing Azure App Service tooyour Azure Database for MySQL server.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="438cc-105">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="438cc-105">Before you begin</span></span>
<span data-ttu-id="438cc-106">Faça logon no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="438cc-106">Log in toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="438cc-107">Criar um servidor de Banco de Dados do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="438cc-107">Create an Azure Database for MySQL server.</span></span> <span data-ttu-id="438cc-108">Para obter detalhes, consulte muito[como toocreate Azure banco de dados para o MySQL server do Portal](quickstart-create-mysql-server-database-using-azure-portal.md) ou [como toocreate Azure banco de dados para o MySQL server usando a CLI](quickstart-create-mysql-server-database-using-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="438cc-108">For details, refer too[How toocreate Azure Database for MySQL server from Portal](quickstart-create-mysql-server-database-using-azure-portal.md) or [How toocreate Azure Database for MySQL server using CLI](quickstart-create-mysql-server-database-using-azure-cli.md).</span></span>

<span data-ttu-id="438cc-109">Atualmente, há duas soluções tooenable acesso de um serviço de aplicativo do Azure de tooan banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="438cc-109">Currently there are two solutions tooenable access from an Azure App Service tooan Azure Database for MySQL.</span></span> <span data-ttu-id="438cc-110">Ambas as soluções envolvem a configuração de regras de firewall de nível de servidor.</span><span class="sxs-lookup"><span data-stu-id="438cc-110">Both solutions involve setting up server-level firewall rules.</span></span>

## <a name="solution-1---create-a-firewall-rule-tooallow-all-ips"></a><span data-ttu-id="438cc-111">Solução 1: criar um tooallow de regra de firewall de todos os IPs</span><span class="sxs-lookup"><span data-stu-id="438cc-111">Solution 1 - Create a firewall rule tooallow all IPs</span></span>
<span data-ttu-id="438cc-112">Banco de dados do Azure para MySQL fornece segurança de acesso usando um firewall tooprotect seus dados.</span><span class="sxs-lookup"><span data-stu-id="438cc-112">Azure Database for MySQL provides access security using a firewall tooprotect your data.</span></span> <span data-ttu-id="438cc-113">Ao conectar-se de um banco de dados do tooAzure do serviço de aplicativo do Azure para MySQL server, tenha em mente que Olá saída IPs de serviço de aplicativo são dinâmicos por natureza.</span><span class="sxs-lookup"><span data-stu-id="438cc-113">When connecting from an Azure App Service tooAzure Database for MySQL server, keep in mind that hello outbound IPs of App Service are dynamic in nature.</span></span> 

<span data-ttu-id="438cc-114">disponibilidade de saudação tooensure do seu serviço de aplicativo do Azure, recomendamos usar tooallow essa solução todos os IPs.</span><span class="sxs-lookup"><span data-stu-id="438cc-114">tooensure hello availability of your Azure App Service, we recommend using this solution tooallow ALL IPs.</span></span>

> [!NOTE]
> <span data-ttu-id="438cc-115">A Microsoft está trabalhando para um tooavoid solução a longo prazo permitindo todos os IPs de serviços do Azure tooconnect tooAzure banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="438cc-115">Microsoft is working for a long-term solution tooavoid allowing all IPs for Azure services tooconnect tooAzure Database for MySQL.</span></span>

1. <span data-ttu-id="438cc-116">Na folha de servidor MySQL hello, em configurações de cabeçalho, clique em **segurança de Conexão** tooopen folha de segurança de Conexão Olá para Olá banco de dados do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="438cc-116">On hello MySQL server blade, under Settings heading, click **Connection Security** tooopen hello Connection Security blade for hello Azure Database for MySQL.</span></span>

   ![Portal do Azure - clique em Segurança de Conexão](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="438cc-118">Digite **NOME DA REGRA**, **IP INICIAL** e **IP FINAL**.</span><span class="sxs-lookup"><span data-stu-id="438cc-118">Enter **RULE NAME**, **START IP**, and **END IP**.</span></span> <span data-ttu-id="438cc-119">Em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="438cc-119">Then click **Save**.</span></span>
   - <span data-ttu-id="438cc-120">Nome da regra: Permitir-Todos os-IPs</span><span class="sxs-lookup"><span data-stu-id="438cc-120">Rule name: Allow-All-IPs</span></span>
   - <span data-ttu-id="438cc-121">IP inicial: 0.0.0.0</span><span class="sxs-lookup"><span data-stu-id="438cc-121">Start IP: 0.0.0.0</span></span>
   - <span data-ttu-id="438cc-122">IP final: 255.255.255.255</span><span class="sxs-lookup"><span data-stu-id="438cc-122">End IP: 255.255.255.255</span></span>

   ![Portal do Azure – adicionar todos os IPs](./media/howto-connect-webapp/1_2-add-all-ips.png)

## <a name="solution-2---create-a-firewall-rule-tooexplicitly-allow-outbound-ips"></a><span data-ttu-id="438cc-124">Solução 2: criar um firewall tooexplicitly de regra permitir saída IPs</span><span class="sxs-lookup"><span data-stu-id="438cc-124">Solution 2 - Create a firewall rule tooexplicitly allow outbound IPs</span></span>
<span data-ttu-id="438cc-125">Você pode adicionar explicitamente que todos Olá IPs de saída do seu serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="438cc-125">You can explicitly add all hello outbound IPs of your Azure App Service.</span></span>

1. <span data-ttu-id="438cc-126">Na folha de propriedades do serviço de aplicativo hello, exibir seu **endereço de IP de saída**.</span><span class="sxs-lookup"><span data-stu-id="438cc-126">On hello App Service Properties blade, view your **OUTBOUND IP ADDRESS**.</span></span>

   ![Portal do Azure – exibir IPs de saída](./media/howto-connect-webapp/2_1-outbound-ip-address.png)

2. <span data-ttu-id="438cc-128">Na folha de segurança de Conexão MySQL hello, adicione saída IPs uma.</span><span class="sxs-lookup"><span data-stu-id="438cc-128">On hello MySQL Connection security blade, add outbound IPs one by one.</span></span>

   ![Portal do Azure – adicionar IPs explícitos](./media/howto-connect-webapp/2_2-add-explicit-ips.png)

3. <span data-ttu-id="438cc-130">Lembre-se muito**salvar** suas regras de firewall.</span><span class="sxs-lookup"><span data-stu-id="438cc-130">Remember too**Save** your firewall rules.</span></span>

<span data-ttu-id="438cc-131">Embora a saudação do serviço de aplicativo do Azure tenta tookeep IP endereços constante ao longo do tempo, há casos em que os endereços IP de saudação podem mudar.</span><span class="sxs-lookup"><span data-stu-id="438cc-131">Though hello Azure App service attempts tookeep IP addresses constant over time, there are cases where hello IP addresses may change.</span></span> <span data-ttu-id="438cc-132">Por exemplo, quando Olá reciclagem de aplicativo, ocorre uma operação em escala ou quando são adicionados novos computadores no Azure dados regionais centros de capacidade de saudação tooincrease.</span><span class="sxs-lookup"><span data-stu-id="438cc-132">For example, when hello app recycles or a scale operation occurs, or when new machines are added in Azure regional data centers tooincrease hello capacity.</span></span> <span data-ttu-id="438cc-133">Quando endereços IP hello forem alterados, o aplicativo hello pode apresentar tempo de inatividade em caso de Olá não pode se conectar toohello MySQL server.</span><span class="sxs-lookup"><span data-stu-id="438cc-133">When hello IP addresses change, hello app could experience downtime in hello event it can no longer connect toohello MySQL server.</span></span> <span data-ttu-id="438cc-134">Considere essa possibilidade ao escolher uma saudação anterior soluções.</span><span class="sxs-lookup"><span data-stu-id="438cc-134">Consider this potential when choosing one of hello preceding solutions.</span></span>

## <a name="ssl-configuration"></a><span data-ttu-id="438cc-135">Configuração de SSL</span><span class="sxs-lookup"><span data-stu-id="438cc-135">SSL configuration</span></span>
<span data-ttu-id="438cc-136">O Banco de Dados do Azure para MySQL tem SSL habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="438cc-136">Azure Database for MySQL has SSL Enabled by default.</span></span> <span data-ttu-id="438cc-137">Se seu aplicativo não estiver usando o banco de dados do SSL tooconnect toohello, você precisa toodisable SSL no servidor MySQL.</span><span class="sxs-lookup"><span data-stu-id="438cc-137">If your application is not using SSL tooconnect toohello database, then you need toodisable SSL on MySQL server.</span></span> <span data-ttu-id="438cc-138">Para obter detalhes sobre como tooconfigure SSL, consulte [usando SSL com o banco de dados do Azure para MySQL](howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="438cc-138">For details on how tooconfigure SSL, See [Using SSL with Azure Database for MySQL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="438cc-139">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="438cc-139">Next steps</span></span>
<span data-ttu-id="438cc-140">Para obter mais informações sobre cadeias de caracteres de conexão, consulte muito[cadeias de caracteres de Conexão](howto-connection-string.md).</span><span class="sxs-lookup"><span data-stu-id="438cc-140">For more information about connection strings, refer too[Connection Strings](howto-connection-string.md).</span></span>
