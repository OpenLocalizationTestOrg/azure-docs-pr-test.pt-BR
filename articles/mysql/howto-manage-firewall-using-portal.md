---
title: "aaaCreate e gerenciar o banco de dados MySQL para regras de firewall usando o portal do Azure de saudação | Microsoft Docs"
description: "Criar e gerenciar o banco de dados MySQL para regras de firewall usando Olá portal do Azure"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 30dbdde4299df564fbf6581419e908186fe3b823
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-hello-azure-portal"></a><span data-ttu-id="65661-103">Criar e gerenciar o banco de dados MySQL para regras de firewall usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="65661-103">Create and manage Azure Database for MySQL firewall rules using hello Azure portal</span></span>
<span data-ttu-id="65661-104">Regras de firewall de nível de servidor Habilitar administradores tooaccess um banco de dados do Azure para MySQL Server de um endereço IP especificado ou o intervalo de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="65661-104">Server-level firewall rules enable administrators tooaccess an Azure Database for MySQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a><span data-ttu-id="65661-105">Criar uma regra de firewall de nível de servidor no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="65661-105">Create a server-level firewall rule in hello Azure portal</span></span>

1. <span data-ttu-id="65661-106">Na folha de servidor MySQL hello, em configurações de cabeçalho, clique em **segurança de Conexão** tooopen folha de segurança de Conexão Olá para Olá banco de dados do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="65661-106">On hello MySQL server blade, under Settings heading, click **Connection Security** tooopen hello Connection Security blade for hello Azure Database for MySQL.</span></span>

   ![Portal do Azure - clique em Segurança de Conexão](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="65661-108">Clique em **adicionar meu IP** em Olá barra de ferramentas toocreate uma regra com o endereço IP de saudação do seu computador, conforme percebido pelo Olá sistema do Azure.</span><span class="sxs-lookup"><span data-stu-id="65661-108">Click **Add My IP** on hello toolbar toocreate a rule with hello IP address of your computer, as perceived by hello Azure system.</span></span>

   ![Portal do Azure - clique em Adicionar Meu IP](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="65661-110">Verifique se o endereço IP antes de salvar a configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="65661-110">Verify your IP address before saving hello configuration.</span></span> <span data-ttu-id="65661-111">Em algumas situações, endereço IP hello observado pelo portal do Azure é diferente do endereço IP hello usado ao acessar Olá internet e servidores do Azure.</span><span class="sxs-lookup"><span data-stu-id="65661-111">In some situations, hello IP address observed by Azure portal differs from hello IP address used when accessing hello internet and Azure servers.</span></span> <span data-ttu-id="65661-112">Portanto, talvez seja necessário toochange Olá IP inicial e final IP toomake Olá regra funcionar como esperado.</span><span class="sxs-lookup"><span data-stu-id="65661-112">Therefore, you may need toochange hello Start IP and End IP toomake hello rule function as expected.</span></span>

   <span data-ttu-id="65661-113">Use um mecanismo de pesquisa ou outra ferramenta on-line toocheck seu próprio endereço IP (por exemplo, procure "qual é o endereço IP").</span><span class="sxs-lookup"><span data-stu-id="65661-113">Use a search engine or other online tool toocheck your own IP address (for example, search "what is my IP address").</span></span>

   ![Bing para Qual é meu IP](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="65661-115">Adicionar outros intervalos de endereço.</span><span class="sxs-lookup"><span data-stu-id="65661-115">Add additional address ranges.</span></span> <span data-ttu-id="65661-116">Em regras de saudação para Olá banco de dados do Azure para o firewall do MySQL, você pode especificar um único endereço IP ou um intervalo de endereços.</span><span class="sxs-lookup"><span data-stu-id="65661-116">In hello rules for hello Azure Database for MySQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="65661-117">Se você quiser toolimit Olá regra tooone único endereço IP, Olá tipo mesmo endereço no campo Olá para o IP inicial e final de IP.</span><span class="sxs-lookup"><span data-stu-id="65661-117">If you want toolimit hello rule tooone single IP address, type hello same address in hello field for Start IP and End IP.</span></span> <span data-ttu-id="65661-118">Abrir o firewall Olá permite tooaccess administradores e usuários qualquer banco de dados Olá MySQL server toowhich têm credenciais válidas.</span><span class="sxs-lookup"><span data-stu-id="65661-118">Opening hello firewall enables administrators and users tooaccess any database on hello MySQL server toowhich they have valid credentials.</span></span>

   ![<span data-ttu-id="65661-119">Portal do Azure - regras de firewall</span><span class="sxs-lookup"><span data-stu-id="65661-119">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/5-specify-addresses.png)


5. <span data-ttu-id="65661-120">Clique em **salvar** em Olá barra de ferramentas toosave essa regra de firewall de nível de servidor.</span><span class="sxs-lookup"><span data-stu-id="65661-120">Click **Save** on hello toolbar toosave this server-level firewall rule.</span></span> <span data-ttu-id="65661-121">Aguarde a confirmação Olá Olá atualização toohello as regras de firewall foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="65661-121">Wait for hello confirmation that hello update toohello firewall rules was successful.</span></span>

   ![Portal do Azure - clique em Salvar](./media/howto-manage-firewall-using-portal/4-save-firewall-rule.png)

## <a name="manage-existing-server-level-firewall-rules-through-hello-azure-portal"></a><span data-ttu-id="65661-123">Gerenciar regras de firewall de nível de servidor existente por meio de saudação portal do Azure</span><span class="sxs-lookup"><span data-stu-id="65661-123">Manage existing server-level firewall rules through hello Azure portal</span></span>
<span data-ttu-id="65661-124">Repita as regras de firewall Olá etapas toomanage hello.</span><span class="sxs-lookup"><span data-stu-id="65661-124">Repeat hello steps toomanage hello firewall rules.</span></span>
* <span data-ttu-id="65661-125">tooadd Olá o computador atual, clique em **+ adicionar meu IP**.</span><span class="sxs-lookup"><span data-stu-id="65661-125">tooadd hello current computer, click **+ Add My IP**.</span></span>
* <span data-ttu-id="65661-126">os endereços IP adicionais tooadd, digite Olá **o nome da regra**, **IP inicial**, e **IP final**.</span><span class="sxs-lookup"><span data-stu-id="65661-126">tooadd additional IP addresses, type in hello **RULE NAME**, **START IP**, and **END IP**.</span></span>
* <span data-ttu-id="65661-127">toomodify uma regra existente, clique em qualquer um dos campos de saudação na regra hello e modificar.</span><span class="sxs-lookup"><span data-stu-id="65661-127">toomodify an existing rule, click any of hello fields in hello rule and modify.</span></span>
* <span data-ttu-id="65661-128">regra de toodelete existente, clique botão de reticências Olá […] e clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="65661-128">toodelete an existing rule, click hello ellipsis […] and click **Delete**.</span></span>
* <span data-ttu-id="65661-129">Clique em **salvar** toosave alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="65661-129">Click **Save** toosave hello changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65661-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="65661-130">Next steps</span></span>
- <span data-ttu-id="65661-131">Para obter ajuda na conexão tooan banco de dados do Azure para o MySQL server, consulte [bibliotecas de Conexão para o banco de dados do Azure para MySQL](./concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="65661-131">For help in connecting tooan Azure Database for MySQL server, see [Connection libraries for Azure Database for MySQL](./concepts-connection-libraries.md)</span></span>
