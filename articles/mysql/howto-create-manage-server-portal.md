---
title: Criar e gerenciar um servidor de Banco de Dados do Azure para MySQL usando o Portal do Azure | Microsoft Docs
description: "Este artigo descreve como você pode criar rapidamente um novo servidor de Banco de Dados do Azure para MySQL e gerenciar o servidor usando o Portal do Azure."
services: mysql
author: v-chenyh
ms.author: nolanwu
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 4605518b6955d9943e76c25df2d4105a6a94433d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-azure-database-for-mysql-server-using-azure-portal"></a><span data-ttu-id="a6e70-103">Criar e gerenciar um servidor de Banco de Dados do Azure para MySQL usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a6e70-103">Create and manage Azure Database for MySQL server using Azure portal</span></span>
<span data-ttu-id="a6e70-104">Este artigo descreve como você pode criar rapidamente um novo servidor de Banco de Dados do Azure para MySQL e gerenciar o servidor usando o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a6e70-104">This article describes how you can quickly create a new Azure Database for MySQL server and manage the server using the Azure Portal.</span></span> <span data-ttu-id="a6e70-105">O gerenciamento de servidor inclui a exibição de detalhes do servidor e bancos de dados, redefinição de senha e exclusão do servidor.</span><span class="sxs-lookup"><span data-stu-id="a6e70-105">Server management includes viewing server details & databases, resetting password and deleting the server.</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="a6e70-106">Faça logon no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a6e70-106">Log in to the Azure portal</span></span>
<span data-ttu-id="a6e70-107">Faça logon no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a6e70-107">Log in to the [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="a6e70-108">Criar um servidor de Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="a6e70-108">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="a6e70-109">Execute estas etapas para criar um servidor de Banco de Dados do Azure para MySQL chamado "mysqlserver4demo"</span><span class="sxs-lookup"><span data-stu-id="a6e70-109">Follow these steps to create an Azure Database for MySQL server named “mysqlserver4demo”</span></span>

<span data-ttu-id="a6e70-110">1- Clique no botão **Novo** no canto superior esquerdo do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a6e70-110">1- Click **New** button found on the upper left-hand corner of the Azure portal.</span></span>

<span data-ttu-id="a6e70-111">2- Selecione **Bancos de Dados** na página Novo e selecione **Banco de Dados do Azure para MySQL** na página Bancos de Dados.</span><span class="sxs-lookup"><span data-stu-id="a6e70-111">2- Select **Databases** from the New page, and select **Azure Database for MySQL** from the Databases page.</span></span>

> <span data-ttu-id="a6e70-112">Um Banco de Dados do Azure para MySQL é criado com um conjunto definido de recursos de [computação e armazenamento](./concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="a6e70-112">An Azure Database for MySQL server is created with a defined set of [compute and storage](./concepts-compute-unit-and-storage.md) resources.</span></span> <span data-ttu-id="a6e70-113">O banco de dados é criado dentro de um grupo de recursos do Azure e em um servidor de Banco de Dados do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="a6e70-113">The database is created within an Azure resource group and in an Azure Database for MySQL server.</span></span>

![create-new-server](./media/howto-create-manage-server-portal/create-new-server.png)

<span data-ttu-id="a6e70-115">3- Preencha o formulário do Banco de Dados do Azure para MySQL com as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="a6e70-115">3- Fill out the Azure Database for MySQL form with the following information:</span></span>

| <span data-ttu-id="a6e70-116">**Campo de Formulário**</span><span class="sxs-lookup"><span data-stu-id="a6e70-116">**Form Field**</span></span> | <span data-ttu-id="a6e70-117">**Descrição do Campo**</span><span class="sxs-lookup"><span data-stu-id="a6e70-117">**Field Description**</span></span> |
|----------------|-----------------------|
| <span data-ttu-id="a6e70-118">*Nome do servidor*</span><span class="sxs-lookup"><span data-stu-id="a6e70-118">*Server name*</span></span> | <span data-ttu-id="a6e70-119">azure-mysql (o nome do servidor é globalmente exclusivo)</span><span class="sxs-lookup"><span data-stu-id="a6e70-119">azure-mysql (server name is globally unique)</span></span> |
| <span data-ttu-id="a6e70-120">*Assinatura*</span><span class="sxs-lookup"><span data-stu-id="a6e70-120">*Subscription*</span></span> | <span data-ttu-id="a6e70-121">MySQLaaS (selecione na lista suspensa)</span><span class="sxs-lookup"><span data-stu-id="a6e70-121">MySQLaaS (select from drop down)</span></span> |
| <span data-ttu-id="a6e70-122">*Grupo de recursos*</span><span class="sxs-lookup"><span data-stu-id="a6e70-122">*Resource group*</span></span> | <span data-ttu-id="a6e70-123">myresource (crie um novo grupo de recursos ou use um existente)</span><span class="sxs-lookup"><span data-stu-id="a6e70-123">myresource (create a new resource group or use an existing one)</span></span> |
| <span data-ttu-id="a6e70-124">*Logon de administrador do servidor*</span><span class="sxs-lookup"><span data-stu-id="a6e70-124">*Server admin login*</span></span> | <span data-ttu-id="a6e70-125">myadmin (nome de conta do administrador de configuração)</span><span class="sxs-lookup"><span data-stu-id="a6e70-125">myadmin (setup admin account name)</span></span> |
| <span data-ttu-id="a6e70-126">*Senha*</span><span class="sxs-lookup"><span data-stu-id="a6e70-126">*Password*</span></span> | <span data-ttu-id="a6e70-127">configurar senha da conta do administrador</span><span class="sxs-lookup"><span data-stu-id="a6e70-127">setup admin account password</span></span> |
| <span data-ttu-id="a6e70-128">*Confirmar senha*</span><span class="sxs-lookup"><span data-stu-id="a6e70-128">*Confirm password*</span></span> | <span data-ttu-id="a6e70-129">confirmar senha da conta do administrador</span><span class="sxs-lookup"><span data-stu-id="a6e70-129">confirm admin account password</span></span> |
| <span data-ttu-id="a6e70-130">*Localidade*</span><span class="sxs-lookup"><span data-stu-id="a6e70-130">*Location*</span></span> | <span data-ttu-id="a6e70-131">Europa Setentrional (escolha entre o Europa Setentrional e Oeste dos EUA)</span><span class="sxs-lookup"><span data-stu-id="a6e70-131">North Europe (select between North Europe and West US)</span></span> |
| <span data-ttu-id="a6e70-132">*Versão*</span><span class="sxs-lookup"><span data-stu-id="a6e70-132">*Version*</span></span> | <span data-ttu-id="a6e70-133">5.6 (escolha uma versão do servidor de Banco de Dados do Azure para MySQL)</span><span class="sxs-lookup"><span data-stu-id="a6e70-133">5.6 (choose Azure Database for MySQL server version)</span></span> |

<span data-ttu-id="a6e70-134">4- Clique em **Tipo de preço** para especificar o nível de desempenho e o tipo de serviço para o novo servidor.</span><span class="sxs-lookup"><span data-stu-id="a6e70-134">4- Click **Pricing tier** to specify the service tier and performance level for your new server.</span></span> <span data-ttu-id="a6e70-135">Unidade de Computação pode ser configurada entre 50 e 100 no Tipo básico, 100 e 200 no Tipo Standard, e o armazenamento pode ser adicionado com base na quantidade incluída.</span><span class="sxs-lookup"><span data-stu-id="a6e70-135">Compute Unit can be configured between 50 and 100 in Basic tier, 100 and 200 in Standard tier, and storage can be added based on included amount.</span></span> <span data-ttu-id="a6e70-136">Para este guia de instruções, vamos escolher 50 Unidades de Computação e 50 GB.</span><span class="sxs-lookup"><span data-stu-id="a6e70-136">For this HowTo guide, let’s choose 50 Compute Unit and 50GB.</span></span> <span data-ttu-id="a6e70-137">Clique em **OK** para salvar sua seleção.</span><span class="sxs-lookup"><span data-stu-id="a6e70-137">Click **OK** to save your selection.</span></span>
<span data-ttu-id="a6e70-138">![create-server-pricing-tier](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)</span><span class="sxs-lookup"><span data-stu-id="a6e70-138">![create-server-pricing-tier](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)</span></span>

<span data-ttu-id="a6e70-139">5- Clique em **Criar** para provisionar o servidor.</span><span class="sxs-lookup"><span data-stu-id="a6e70-139">5- Click **Create** to provision the server.</span></span> <span data-ttu-id="a6e70-140">O provisionamento demora alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="a6e70-140">Provisioning takes a few minutes.</span></span>

> <span data-ttu-id="a6e70-141">Marque a opção **Fixar no painel** para permitir o controle fácil de suas implantações.</span><span class="sxs-lookup"><span data-stu-id="a6e70-141">Check the **Pin to dashboard** option to allow easy tracking of your deployments.</span></span>
> [!NOTE]
> <span data-ttu-id="a6e70-142">Embora exista suporte para até 1000 GB na camada Basic e 10000 GB na camada Standard para armazenamento, para Visualização Pública, o armazenamento máximo ainda está limitado temporariamente a 1000 GB.</span><span class="sxs-lookup"><span data-stu-id="a6e70-142">Although up to 1000GB in Basic tier and 10000GB in Standard tier will be supported for storage, for Public Preview, the maximum storage is still limited to 1000GB temporarily.</span></span> 
</Include>

## <a name="update-an-azure-database-for-mysql-server"></a><span data-ttu-id="a6e70-143">Atualizar um servidor de Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="a6e70-143">Update an Azure Database for MySQL server</span></span>
<span data-ttu-id="a6e70-144">Após o provisionamento do novo servidor, o usuário terá duas opções para editar um servidor existente: redefinir a senha de administrador ou escalar verticalmente o servidor alterando as unidades de computação.</span><span class="sxs-lookup"><span data-stu-id="a6e70-144">After new server is provisioned, user has 2 options to edit an existing server: reset administrator password or scale up/down the server by changing the compute-units.</span></span>

### <a name="change-the-administrator-user-password"></a><span data-ttu-id="a6e70-145">Alterar a senha de usuário do administrador</span><span class="sxs-lookup"><span data-stu-id="a6e70-145">Change the administrator user password</span></span>
<span data-ttu-id="a6e70-146">1- Na folha **Visão geral** do servidor, clique em **Redefinir senha** para preencher uma janela de entrada e confirmação de senha.</span><span class="sxs-lookup"><span data-stu-id="a6e70-146">1- On the server **Overview** blade, click **Reset password** to populate a password input and confirmation window.</span></span>

<span data-ttu-id="a6e70-147">2- Insira a nova senha e confirme a senha na janela, conforme mostrado a seguir: ![reset-password](./media/howto-create-manage-server-portal/reset-password.png)</span><span class="sxs-lookup"><span data-stu-id="a6e70-147">2- Enter new password and confirm the password in the window as below: ![reset-password](./media/howto-create-manage-server-portal/reset-password.png)</span></span>

<span data-ttu-id="a6e70-148">3- Clique em **OK** para salvar a nova senha.</span><span class="sxs-lookup"><span data-stu-id="a6e70-148">3- Click **OK** to save the new password.</span></span>

### <a name="scale-updown-by-changing-compute-units"></a><span data-ttu-id="a6e70-149">Escalar verticalmente alterando as Unidades de Computação</span><span class="sxs-lookup"><span data-stu-id="a6e70-149">Scale up/down by changing Compute Units</span></span>

<span data-ttu-id="a6e70-150">1 - na folha do servidor, em **Configurações**, clique em **Tipo de preço** para abrir a folha Tipo de preço para o servidor de Banco de Dados do Azure para MySQL.</span><span class="sxs-lookup"><span data-stu-id="a6e70-150">1- On the server blade, under **Settings**, click **Pricing tier** to open the Pricing tier blade for the Azure Database for MySQL server.</span></span>

<span data-ttu-id="a6e70-151">2- Execute a Etapa 4 de **Criar um servidor de Banco de Dados para MySQL** para alterar as Unidades de Computação no mesmo Tipo de preço.</span><span class="sxs-lookup"><span data-stu-id="a6e70-151">2- Follow Step 4 in **Create an Azure Database for MySQL server** to change Compute Units in the same pricing tier.</span></span>

## <a name="delete-an-azure-database-for-mysql-server"></a><span data-ttu-id="a6e70-152">Excluir um servidor de Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="a6e70-152">Delete an Azure Database for MySQL server</span></span>

<span data-ttu-id="a6e70-153">1 - Na folha **Visão geral** do servidor, clique no botão de comando **Excluir** para abrir a folha de Confirmação de exclusão.</span><span class="sxs-lookup"><span data-stu-id="a6e70-153">1- On the server **Overview** blade, click **Delete** command button to open the Deleting confirmation blade.</span></span>

<span data-ttu-id="a6e70-154">2- Digite o nome correto do servidor na caixa de entrada da folha para confirmar duas vezes.</span><span class="sxs-lookup"><span data-stu-id="a6e70-154">2- Type the correct server name in input box of the blade for double confirmation.</span></span>

<span data-ttu-id="a6e70-155">3- Clique no botão **Excluir** novamente para confirmar a ação de exclusão e aguarde o pop-up "Exclusão bem-sucedida" na barra de notificação.</span><span class="sxs-lookup"><span data-stu-id="a6e70-155">3- Click **Delete** button again to confirm deleting action and wait for “Deleting success” popup on the notification bar.</span></span>

## <a name="list-the-azure-database-for-mysql-databases"></a><span data-ttu-id="a6e70-156">Listar os bancos de dados do Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="a6e70-156">List the Azure Database for MySQL databases</span></span>
<span data-ttu-id="a6e70-157">Na folha **Visão geral** do servidor, role para baixo até ver o bloco do banco de dados na parte inferior.</span><span class="sxs-lookup"><span data-stu-id="a6e70-157">On the server **Overview** blade, scroll down until you see the database tile on the bottom.</span></span> <span data-ttu-id="a6e70-158">Todos os bancos de dados estarão listados na tabela.</span><span class="sxs-lookup"><span data-stu-id="a6e70-158">All the databases will be listed in the table.</span></span> <span data-ttu-id="a6e70-159">clique no botão de comando **Excluir** para abrir a folha de Confirmação de exclusão.</span><span class="sxs-lookup"><span data-stu-id="a6e70-159">click **Delete** command button to open the Deleting confirmation blade.</span></span>

![show-databases](./media/howto-create-manage-server-portal/show-databases.png)

## <a name="show-details-of-an-azure-database-for-mysql-server"></a><span data-ttu-id="a6e70-161">Mostrar detalhes de um servidor de Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="a6e70-161">Show details of an Azure Database for MySQL server</span></span>
<span data-ttu-id="a6e70-162">Clique em **Propriedades** em **Configurações** na folha do servidor para abrir a folha **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="a6e70-162">Click **Properties** under **Settings** on the server blade will open the **Properties** blade.</span></span> <span data-ttu-id="a6e70-163">Veja todas as informações detalhadas sobre o servidor.</span><span class="sxs-lookup"><span data-stu-id="a6e70-163">Then you can view all detailed information about the server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6e70-164">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a6e70-164">Next steps</span></span>

[<span data-ttu-id="a6e70-165">Início rápido: criar e gerenciar um servidor de Banco de Dados do Azure para MySQL usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a6e70-165">Quickstart: Create Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
