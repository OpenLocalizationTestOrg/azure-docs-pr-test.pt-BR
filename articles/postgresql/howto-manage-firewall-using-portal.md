---
title: "aaaCreate e gerenciar o banco de dados PostgreSQL para regras de firewall usando o portal do Azure de saudação | Microsoft Docs"
description: "Criar e gerenciar o banco de dados PostgreSQL para regras de firewall usando Olá portal do Azure"
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 6a41a077168657769e442401e9df9931aa809240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-hello-azure-portal"></a><span data-ttu-id="98e77-103">Criar e gerenciar o banco de dados PostgreSQL para regras de firewall usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="98e77-103">Create and manage Azure Database for PostgreSQL firewall rules using hello Azure portal</span></span>
<span data-ttu-id="98e77-104">Regras de firewall de nível de servidor Habilitar administradores tooaccess um banco de dados do Azure para PostgreSQL Server de um endereço IP especificado ou o intervalo de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="98e77-104">Server-level firewall rules enable administrators tooaccess an Azure Database for PostgreSQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="98e77-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="98e77-105">Prerequisites</span></span>
<span data-ttu-id="98e77-106">toostep por este tooguide como, você precisa:</span><span class="sxs-lookup"><span data-stu-id="98e77-106">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="98e77-107">Um servidor [Criar um servidor de Banco de Dados do Azure para o PostgreSQL](quickstart-create-server-database-portal.md)</span><span class="sxs-lookup"><span data-stu-id="98e77-107">A server [Create an Azure Database for PostgreSQL](quickstart-create-server-database-portal.md)</span></span>

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="98e77-108">Criar uma regra de firewall de nível de servidor no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="98e77-108">Create a server-level firewall rule in hello Azure portal</span></span>
1. <span data-ttu-id="98e77-109">Na folha de servidor Olá PostgreSQL, em configurações de cabeçalho, clique em **segurança de Conexão** tooopen folha de segurança de Conexão Olá para hello Azure banco de dados PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="98e77-109">On hello PostgreSQL server blade, under Settings heading, click **Connection Security** tooopen hello Connection Security blade for hello Azure Database for PostgreSQL.</span></span>

  ![Portal do Azure - clique em Segurança de Conexão](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="98e77-111">Clique em **adicionar meu IP** na barra de ferramentas de saudação.</span><span class="sxs-lookup"><span data-stu-id="98e77-111">Click **Add My IP** on hello toolbar.</span></span> <span data-ttu-id="98e77-112">Isso criará uma regra de automaticamente com o endereço IP de saudação do seu computador, conforme percebido pelo Olá sistema do Azure.</span><span class="sxs-lookup"><span data-stu-id="98e77-112">This will create a rule automatically with hello IP address of your computer, as perceived by hello Azure system.</span></span>

  ![Portal do Azure - clique em Adicionar Meu IP](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="98e77-114">Verifique se o endereço IP antes de salvar a configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="98e77-114">Verify your IP address before saving hello configuration.</span></span> <span data-ttu-id="98e77-115">Em algumas situações, endereço IP hello observado pelo portal do Azure é diferente do endereço IP hello usado ao acessar Olá internet e servidores do Azure.</span><span class="sxs-lookup"><span data-stu-id="98e77-115">In some situations, hello IP address observed by Azure portal differs from hello IP address used when accessing hello internet and Azure servers.</span></span> <span data-ttu-id="98e77-116">Portanto, talvez seja necessário toochange Olá IP inicial e final IP toomake Olá regra funcionar como esperado.</span><span class="sxs-lookup"><span data-stu-id="98e77-116">Therefore, you may need toochange hello Start IP and End IP toomake hello rule function as expected.</span></span>
<span data-ttu-id="98e77-117">Use um mecanismo de pesquisa ou outra ferramenta on-line toocheck seu próprio endereço IP (por exemplo, pesquisa do Bing "qual é o meu IP").</span><span class="sxs-lookup"><span data-stu-id="98e77-117">Use a search engine or other online tool toocheck your own IP address (for example, Bing search "what is my IP").</span></span>

  ![Pesquisa do Bing para Qual é meu IP](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="98e77-119">Adicionar outros intervalos de endereço.</span><span class="sxs-lookup"><span data-stu-id="98e77-119">Add additional address ranges.</span></span> <span data-ttu-id="98e77-120">Em regras de Olá para Olá banco de dados PostgreSQL firewall, você pode especificar um único endereço IP ou um intervalo de endereços.</span><span class="sxs-lookup"><span data-stu-id="98e77-120">In hello rules for hello Azure Database for PostgreSQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="98e77-121">Se você quiser toolimit Olá regra tooone único endereço IP, Olá tipo mesmo endereço no campo Olá para o IP inicial e final de IP.</span><span class="sxs-lookup"><span data-stu-id="98e77-121">If you want toolimit hello rule tooone single IP address, type hello same address in hello field for Start IP and End IP.</span></span> <span data-ttu-id="98e77-122">Abrir firewall Olá permite que administradores e usuários toologin tooany banco de dados em Olá PostgreSQL server toowhich têm credenciais válidas.</span><span class="sxs-lookup"><span data-stu-id="98e77-122">Opening hello firewall enables administrators and users toologin tooany database on hello PostgreSQL server toowhich they have valid credentials.</span></span>

  ![<span data-ttu-id="98e77-123">Portal do Azure - regras de firewall</span><span class="sxs-lookup"><span data-stu-id="98e77-123">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/4-specify-addresses.png)

5. <span data-ttu-id="98e77-124">Clique em **salvar** em Olá barra de ferramentas toosave essa regra de firewall de nível de servidor.</span><span class="sxs-lookup"><span data-stu-id="98e77-124">Click **Save** on hello toolbar toosave this server-level firewall rule.</span></span> <span data-ttu-id="98e77-125">Aguarde a confirmação Olá Olá atualização toohello as regras de firewall foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="98e77-125">Wait for hello confirmation that hello update toohello firewall rules was successful.</span></span>

  ![Portal do Azure - clique em Salvar](./media/howto-manage-firewall-using-portal/5-save-firewall-rule.png)


## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a><span data-ttu-id="98e77-127">Gerenciar regras de firewall de nível de servidor existente por meio de saudação portal do Azure</span><span class="sxs-lookup"><span data-stu-id="98e77-127">Manage existing server-level firewall rules through hello Azure portal</span></span>
<span data-ttu-id="98e77-128">Repita as regras de firewall Olá etapas toomanage hello.</span><span class="sxs-lookup"><span data-stu-id="98e77-128">Repeat hello steps toomanage hello firewall rules.</span></span>
* <span data-ttu-id="98e77-129">tooadd Olá o computador atual, clique botão de saudação muito + **adicionar meu IP**.</span><span class="sxs-lookup"><span data-stu-id="98e77-129">tooadd hello current computer, click hello button too+ **Add My IP**.</span></span> <span data-ttu-id="98e77-130">Clique em **salvar** toosave alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="98e77-130">Click **Save** toosave hello changes.</span></span>
* <span data-ttu-id="98e77-131">os endereços IP adicionais tooadd, digite Olá nome da regra, o endereço IP inicial e o endereço IP final.</span><span class="sxs-lookup"><span data-stu-id="98e77-131">tooadd additional IP addresses, type in hello Rule Name, Start IP Address, and End IP Address.</span></span> <span data-ttu-id="98e77-132">Clique em **salvar** toosave alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="98e77-132">Click **Save** toosave hello changes.</span></span>
* <span data-ttu-id="98e77-133">toomodify uma regra existente, clique em qualquer um dos campos de saudação na regra hello e modificar.</span><span class="sxs-lookup"><span data-stu-id="98e77-133">toomodify an existing rule, click any of hello fields in hello rule and modify.</span></span> <span data-ttu-id="98e77-134">Clique em **salvar** toosave alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="98e77-134">Click **Save** toosave hello changes.</span></span>
* <span data-ttu-id="98e77-135">toodelete uma regra existente, clique botão de reticências Olá [...] e clique em Excluir regra de saudação remover.</span><span class="sxs-lookup"><span data-stu-id="98e77-135">toodelete an existing rule, click hello ellipsis […] and click Delete remove hello rule.</span></span> <span data-ttu-id="98e77-136">Clique em **salvar** toosave alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="98e77-136">Click **Save** toosave hello changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98e77-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="98e77-137">Next steps</span></span>
- <span data-ttu-id="98e77-138">Da mesma forma, você pode gerar um script muito[criar e gerenciar o banco de dados PostgreSQL para regras de firewall usando a CLI do Azure](howto-manage-firewall-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="98e77-138">Similarly, you can script too[Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI](howto-manage-firewall-using-cli.md)</span></span>
- <span data-ttu-id="98e77-139">Para obter ajuda na conexão tooan banco de dados para o servidor PostgreSQL, consulte [bibliotecas de Conexão para o banco de dados do Azure para PostgreSQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="98e77-139">For help in connecting tooan Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
