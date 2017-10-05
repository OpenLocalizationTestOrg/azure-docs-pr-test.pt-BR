---
title: Criar e gerenciar regras de firewall do Banco de Dados do Azure para MySQL usando o Portal do Azure | Microsoft Docs
description: Criar e gerenciar regras de firewall do Banco de Dados do Azure para MySQL usando o Portal do Azure
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 33198e5a6e11df2db3a17fc96a0b3cd4b1a284e8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-the-azure-portal"></a><span data-ttu-id="ce236-103">Criar e gerenciar regras de firewall do Banco de Dados do Azure para MySQL usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ce236-103">Create and manage Azure Database for MySQL firewall rules using the Azure portal</span></span>
<span data-ttu-id="ce236-104">As regras de firewall no nível de servidor permitem que os administradores acessem um servidor de Banco de Dados SQL do Azure para MySQL de um endereço IP específico ou intervalo de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="ce236-104">Server-level firewall rules enable administrators to access an Azure Database for MySQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="create-a-server-level-firewall-rule-in-the-azure-portal"></a><span data-ttu-id="ce236-105">Criar uma regra de firewall de nível de servidor no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ce236-105">Create a server-level firewall rule in the Azure portal</span></span>

1. <span data-ttu-id="ce236-106">Na folha do servidor MySQL, no título Configurações, clique em **Segurança de Conexão** para abrir a folha Segurança de Conexão para o Banco de Dados do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="ce236-106">On the MySQL server blade, under Settings heading, click **Connection Security** to open the Connection Security blade for the Azure Database for MySQL.</span></span>

   ![Portal do Azure - clique em Segurança de Conexão](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="ce236-108">Clique em **Adicionar Meu IP** na barra de ferramentas para criar uma regra com o endereço IP de seu computador, como visto pelo sistema do Azure.</span><span class="sxs-lookup"><span data-stu-id="ce236-108">Click **Add My IP** on the toolbar to create a rule with the IP address of your computer, as perceived by the Azure system.</span></span>

   ![Portal do Azure - clique em Adicionar Meu IP](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="ce236-110">Verifique seu endereço IP antes de salvar a configuração.</span><span class="sxs-lookup"><span data-stu-id="ce236-110">Verify your IP address before saving the configuration.</span></span> <span data-ttu-id="ce236-111">Em algumas situações, o endereço IP observado pelo Portal do Azure é diferente do endereço IP usado ao acessar a Internet e os servidores do Azure.</span><span class="sxs-lookup"><span data-stu-id="ce236-111">In some situations, the IP address observed by Azure portal differs from the IP address used when accessing the internet and Azure servers.</span></span> <span data-ttu-id="ce236-112">Portanto, talvez seja necessário alterar o IP inicial e o IP final para fazer a regra funcionar conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="ce236-112">Therefore, you may need to change the Start IP and End IP to make the rule function as expected.</span></span>

   <span data-ttu-id="ce236-113">Use um mecanismo de pesquisa ou outra ferramenta online para verificar seu próprio endereço IP (por exemplo, pesquise "Qual é meu endereço IP").</span><span class="sxs-lookup"><span data-stu-id="ce236-113">Use a search engine or other online tool to check your own IP address (for example, search "what is my IP address").</span></span>

   ![Bing para Qual é meu IP](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="ce236-115">Adicionar outros intervalos de endereço.</span><span class="sxs-lookup"><span data-stu-id="ce236-115">Add additional address ranges.</span></span> <span data-ttu-id="ce236-116">Nas regras do firewall de Banco de Dados do Azure para MySQL, você pode especificar um único endereço IP ou um intervalo de endereços.</span><span class="sxs-lookup"><span data-stu-id="ce236-116">In the rules for the Azure Database for MySQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="ce236-117">Se você quiser limitar a regra para um único endereço IP, digite o mesmo endereço nos campos IP inicial e IP Final.</span><span class="sxs-lookup"><span data-stu-id="ce236-117">If you want to limit the rule to one single IP address, type the same address in the field for Start IP and End IP.</span></span> <span data-ttu-id="ce236-118">Abrir o firewall permite que os administradores e os usuários acessem qualquer banco de dados no servidor MySQL ao qual eles têm credenciais válidas.</span><span class="sxs-lookup"><span data-stu-id="ce236-118">Opening the firewall enables administrators and users to access any database on the MySQL server to which they have valid credentials.</span></span>

   ![<span data-ttu-id="ce236-119">Portal do Azure - regras de firewall</span><span class="sxs-lookup"><span data-stu-id="ce236-119">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/5-specify-addresses.png)


5. <span data-ttu-id="ce236-120">Clique em **Salvar** na barra de ferramentas para salvar essa regra de firewall no nível de servidor.</span><span class="sxs-lookup"><span data-stu-id="ce236-120">Click **Save** on the toolbar to save this server-level firewall rule.</span></span> <span data-ttu-id="ce236-121">Aguarde a confirmação de que a atualização das regras de firewall foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="ce236-121">Wait for the confirmation that the update to the firewall rules was successful.</span></span>

   ![Portal do Azure - clique em Salvar](./media/howto-manage-firewall-using-portal/4-save-firewall-rule.png)

## <a name="manage-existing-server-level-firewall-rules-through-the-azure-portal"></a><span data-ttu-id="ce236-123">Gerenciar regras de firewall existentes no nível de servidor pelo Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ce236-123">Manage existing server-level firewall rules through the Azure portal</span></span>
<span data-ttu-id="ce236-124">Repita as etapas para gerenciar as regras de firewall.</span><span class="sxs-lookup"><span data-stu-id="ce236-124">Repeat the steps to manage the firewall rules.</span></span>
* <span data-ttu-id="ce236-125">Para adicionar o computador atual, clique em **+ Adicionar Meu IP**.</span><span class="sxs-lookup"><span data-stu-id="ce236-125">To add the current computer, click **+ Add My IP**.</span></span>
* <span data-ttu-id="ce236-126">Para adicionar mais endereços IP, digite o **NOME DA REGRA**, o **IP INICIAL** e o **IP FINAL**.</span><span class="sxs-lookup"><span data-stu-id="ce236-126">To add additional IP addresses, type in the **RULE NAME**, **START IP**, and **END IP**.</span></span>
* <span data-ttu-id="ce236-127">Para modificar uma regra existente, clique em qualquer um dos campos na regra e modifique.</span><span class="sxs-lookup"><span data-stu-id="ce236-127">To modify an existing rule, click any of the fields in the rule and modify.</span></span>
* <span data-ttu-id="ce236-128">Para excluir uma regra existente, clique nas reticências [...] e clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="ce236-128">To delete an existing rule, click the ellipsis […] and click **Delete**.</span></span>
* <span data-ttu-id="ce236-129">Clique em **Salvar** para salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="ce236-129">Click **Save** to save the changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce236-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ce236-130">Next steps</span></span>
- <span data-ttu-id="ce236-131">Para obter ajuda com a conexão com um Banco de Dados para servidor MySQL, veja [Bibliotecas de conexão para o Banco de Dados para MySQL](./concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="ce236-131">For help in connecting to an Azure Database for MySQL server, see [Connection libraries for Azure Database for MySQL](./concepts-connection-libraries.md)</span></span>
