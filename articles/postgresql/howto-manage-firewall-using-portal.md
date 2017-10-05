---
title: Criar e gerenciar regras de firewall do Banco de Dados do Azure para PostgreSQL usando o Portal do Azure | Microsoft Docs
description: Criar e gerenciar regras de firewall do Banco de Dados do Azure para PostgreSQL usando o Portal do Azure
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 20ac1392949a6f604e68d984cb50273b61051037
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-the-azure-portal"></a><span data-ttu-id="d43b1-103">Criar e gerenciar regras de firewall do Banco de Dados do Azure para PostgreSQL usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d43b1-103">Create and manage Azure Database for PostgreSQL firewall rules using the Azure portal</span></span>
<span data-ttu-id="d43b1-104">As regras de firewall no nível de servidor permitem que os administradores acessem um servidor de Banco de Dados SQL do Azure para PostgreSQL de um endereço IP específico ou intervalo de endereços IP.</span><span class="sxs-lookup"><span data-stu-id="d43b1-104">Server-level firewall rules enable administrators to access an Azure Database for PostgreSQL Server from a specified IP address or range of IP addresses.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d43b1-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d43b1-105">Prerequisites</span></span>
<span data-ttu-id="d43b1-106">Para seguir este guia de instruções, você precisa:</span><span class="sxs-lookup"><span data-stu-id="d43b1-106">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="d43b1-107">Um servidor [Criar um servidor de Banco de Dados do Azure para o PostgreSQL](quickstart-create-server-database-portal.md)</span><span class="sxs-lookup"><span data-stu-id="d43b1-107">A server [Create an Azure Database for PostgreSQL](quickstart-create-server-database-portal.md)</span></span>

## <a name="create-a-server-level-firewall-rule-in-the-azure-portal"></a><span data-ttu-id="d43b1-108">Criar uma regra de firewall de nível de servidor no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d43b1-108">Create a server-level firewall rule in the Azure portal</span></span>
1. <span data-ttu-id="d43b1-109">Na folha do servidor PostgreSQL, no título Configurações, clique em **Segurança de Conexão** para abrir a folha Segurança de Conexão para o Banco de Dados do Azure para PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="d43b1-109">On the PostgreSQL server blade, under Settings heading, click **Connection Security** to open the Connection Security blade for the Azure Database for PostgreSQL.</span></span>

  ![Portal do Azure - clique em Segurança de Conexão](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="d43b1-111">Clique em **Adicionar Meu IP** na barra de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="d43b1-111">Click **Add My IP** on the toolbar.</span></span> <span data-ttu-id="d43b1-112">Isso criará automaticamente uma regra com o endereço IP de seu computador, como visto pelo sistema do Azure.</span><span class="sxs-lookup"><span data-stu-id="d43b1-112">This will create a rule automatically with the IP address of your computer, as perceived by the Azure system.</span></span>

  ![Portal do Azure - clique em Adicionar Meu IP](./media/howto-manage-firewall-using-portal/2-add-my-ip.png)

3. <span data-ttu-id="d43b1-114">Verifique seu endereço IP antes de salvar a configuração.</span><span class="sxs-lookup"><span data-stu-id="d43b1-114">Verify your IP address before saving the configuration.</span></span> <span data-ttu-id="d43b1-115">Em algumas situações, o endereço IP observado pelo Portal do Azure é diferente do endereço IP usado ao acessar a Internet e os servidores do Azure.</span><span class="sxs-lookup"><span data-stu-id="d43b1-115">In some situations, the IP address observed by Azure portal differs from the IP address used when accessing the internet and Azure servers.</span></span> <span data-ttu-id="d43b1-116">Portanto, talvez seja necessário alterar o IP inicial e o IP final para fazer a regra funcionar conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="d43b1-116">Therefore, you may need to change the Start IP and End IP to make the rule function as expected.</span></span>
<span data-ttu-id="d43b1-117">Use um mecanismo de pesquisa ou outra ferramenta online para verificar seu próprio endereço IP (por exemplo, pesquise no Bing "Qual é meu IP").</span><span class="sxs-lookup"><span data-stu-id="d43b1-117">Use a search engine or other online tool to check your own IP address (for example, Bing search "what is my IP").</span></span>

  ![Pesquisa do Bing para Qual é meu IP](./media/howto-manage-firewall-using-portal/3-what-is-my-ip.png)

4. <span data-ttu-id="d43b1-119">Adicionar outros intervalos de endereço.</span><span class="sxs-lookup"><span data-stu-id="d43b1-119">Add additional address ranges.</span></span> <span data-ttu-id="d43b1-120">Nas regras do firewall de Banco de Dados do Azure para PostgreSQL, você pode especificar um único endereço IP ou um intervalo de endereços.</span><span class="sxs-lookup"><span data-stu-id="d43b1-120">In the rules for the Azure Database for PostgreSQL firewall, you can specify a single IP address, or a range of addresses.</span></span> <span data-ttu-id="d43b1-121">Se você quiser limitar a regra para um único endereço IP, digite o mesmo endereço nos campos IP inicial e IP Final.</span><span class="sxs-lookup"><span data-stu-id="d43b1-121">If you want to limit the rule to one single IP address, type the same address in the field for Start IP and End IP.</span></span> <span data-ttu-id="d43b1-122">Abrir o firewall permite que os administradores e usuários façam logon em qualquer banco de dados no servidor PostgreSQL para o qual eles têm credenciais válidas.</span><span class="sxs-lookup"><span data-stu-id="d43b1-122">Opening the firewall enables administrators and users to login to any database on the PostgreSQL server to which they have valid credentials.</span></span>

  ![<span data-ttu-id="d43b1-123">Portal do Azure - regras de firewall</span><span class="sxs-lookup"><span data-stu-id="d43b1-123">Azure portal - firewall rules</span></span> ](./media/howto-manage-firewall-using-portal/4-specify-addresses.png)

5. <span data-ttu-id="d43b1-124">Clique em **Salvar** na barra de ferramentas para salvar essa regra de firewall no nível de servidor.</span><span class="sxs-lookup"><span data-stu-id="d43b1-124">Click **Save** on the toolbar to save this server-level firewall rule.</span></span> <span data-ttu-id="d43b1-125">Aguarde a confirmação de que a atualização das regras de firewall foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="d43b1-125">Wait for the confirmation that the update to the firewall rules was successful.</span></span>

  ![Portal do Azure - clique em Salvar](./media/howto-manage-firewall-using-portal/5-save-firewall-rule.png)


## <a name="manage-existing-server-level-firewall-rules-through-the-azure-portal"></a><span data-ttu-id="d43b1-127">Gerenciar regras de firewall existentes no nível de servidor pelo Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d43b1-127">Manage existing server-level firewall rules through the Azure portal</span></span>
<span data-ttu-id="d43b1-128">Repita as etapas para gerenciar as regras de firewall.</span><span class="sxs-lookup"><span data-stu-id="d43b1-128">Repeat the steps to manage the firewall rules.</span></span>
* <span data-ttu-id="d43b1-129">Para adicionar o computador atual, clique no botão + **Adicionar Meu IP**.</span><span class="sxs-lookup"><span data-stu-id="d43b1-129">To add the current computer, click the button to + **Add My IP**.</span></span> <span data-ttu-id="d43b1-130">Clique em **Salvar** para salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="d43b1-130">Click **Save** to save the changes.</span></span>
* <span data-ttu-id="d43b1-131">Para adicionar mais endereços IP, digite o Nome da Regra, o Endereço IP Inicial e o Endereço IP Final.</span><span class="sxs-lookup"><span data-stu-id="d43b1-131">To add additional IP addresses, type in the Rule Name, Start IP Address, and End IP Address.</span></span> <span data-ttu-id="d43b1-132">Clique em **Salvar** para salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="d43b1-132">Click **Save** to save the changes.</span></span>
* <span data-ttu-id="d43b1-133">Para modificar uma regra existente, clique em qualquer um dos campos na regra e modifique.</span><span class="sxs-lookup"><span data-stu-id="d43b1-133">To modify an existing rule, click any of the fields in the rule and modify.</span></span> <span data-ttu-id="d43b1-134">Clique em **Salvar** para salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="d43b1-134">Click **Save** to save the changes.</span></span>
* <span data-ttu-id="d43b1-135">Para excluir uma regra existente, clique nas reticências [...] e clique em Excluir para remover a regra.</span><span class="sxs-lookup"><span data-stu-id="d43b1-135">To delete an existing rule, click the ellipsis […] and click Delete remove the rule.</span></span> <span data-ttu-id="d43b1-136">Clique em **Salvar** para salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="d43b1-136">Click **Save** to save the changes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d43b1-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d43b1-137">Next steps</span></span>
- <span data-ttu-id="d43b1-138">Da mesma forma, você pode gerar um script para [Criar e gerenciar regras de firewall do Banco de Dados do Azure para PostgreSQL usando a CLI do Azure](howto-manage-firewall-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="d43b1-138">Similarly, you can script to [Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI](howto-manage-firewall-using-cli.md)</span></span>
- <span data-ttu-id="d43b1-139">Para obter ajuda com a conexão com um Banco de Dados para servidor PostgreSQL, veja [Bibliotecas de conexão para o Banco de Dados do Azure para PostgreSQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="d43b1-139">For help in connecting to an Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
