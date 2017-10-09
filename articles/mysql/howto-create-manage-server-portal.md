---
title: aaaCreate e gerenciar o banco de dados do Azure para o MySQL server usando o portal do Azure | Microsoft Docs
description: "Este artigo descreve como você pode rapidamente criar um novo banco de dados do Azure para o MySQL server e gerenciar o servidor de saudação usando Olá Portal do Azure."
services: mysql
author: v-chenyh
ms.author: nolanwu
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: c532df43b3d2124d7bd34875b32d52357f162af8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-server-using-azure-portal"></a><span data-ttu-id="51be5-103">Criar e gerenciar um servidor de Banco de Dados do Azure para MySQL usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="51be5-103">Create and manage Azure Database for MySQL server using Azure portal</span></span>
<span data-ttu-id="51be5-104">Este artigo descreve como você pode rapidamente criar um novo banco de dados do Azure para o MySQL server e gerenciar o servidor de saudação usando Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="51be5-104">This article describes how you can quickly create a new Azure Database for MySQL server and manage hello server using hello Azure Portal.</span></span> <span data-ttu-id="51be5-105">Gerenciamento de servidor inclui exibindo detalhes do servidor e bancos de dados, a redefinição de senha e excluindo o servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="51be5-105">Server management includes viewing server details & databases, resetting password and deleting hello server.</span></span>

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="51be5-106">Faça logon no toohello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="51be5-106">Log in toohello Azure portal</span></span>
<span data-ttu-id="51be5-107">Faça logon no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="51be5-107">Log in toohello [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="51be5-108">Criar um servidor de Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="51be5-108">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="51be5-109">Siga essas etapas toocreate um banco de dados do Azure para o servidor MySQL chamado "mysqlserver4demo"</span><span class="sxs-lookup"><span data-stu-id="51be5-109">Follow these steps toocreate an Azure Database for MySQL server named “mysqlserver4demo”</span></span>

<span data-ttu-id="51be5-110">1 Clique **novo** botão localizado no canto superior esquerdo de saudação do hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="51be5-110">1- Click **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

<span data-ttu-id="51be5-111">Selecione 2 **bancos de dados** de saudação nova página e selecione **banco de dados do Azure para MySQL** da página de bancos de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="51be5-111">2- Select **Databases** from hello New page, and select **Azure Database for MySQL** from hello Databases page.</span></span>

> <span data-ttu-id="51be5-112">Um Banco de Dados do Azure para MySQL é criado com um conjunto definido de recursos de [computação e armazenamento](./concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="51be5-112">An Azure Database for MySQL server is created with a defined set of [compute and storage](./concepts-compute-unit-and-storage.md) resources.</span></span> <span data-ttu-id="51be5-113">saudação de banco de dados criada em um grupo de recursos do Azure e em um banco de dados do Azure para o MySQL server.</span><span class="sxs-lookup"><span data-stu-id="51be5-113">hello database is created within an Azure resource group and in an Azure Database for MySQL server.</span></span>

![create-new-server](./media/howto-create-manage-server-portal/create-new-server.png)

<span data-ttu-id="51be5-115">3 - preencha hello banco de dados do Azure para o formulário do MySQL com hello informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="51be5-115">3- Fill out hello Azure Database for MySQL form with hello following information:</span></span>

| <span data-ttu-id="51be5-116">**Campo de Formulário**</span><span class="sxs-lookup"><span data-stu-id="51be5-116">**Form Field**</span></span> | <span data-ttu-id="51be5-117">**Descrição do Campo**</span><span class="sxs-lookup"><span data-stu-id="51be5-117">**Field Description**</span></span> |
|----------------|-----------------------|
| <span data-ttu-id="51be5-118">*Nome do servidor*</span><span class="sxs-lookup"><span data-stu-id="51be5-118">*Server name*</span></span> | <span data-ttu-id="51be5-119">azure-mysql (o nome do servidor é globalmente exclusivo)</span><span class="sxs-lookup"><span data-stu-id="51be5-119">azure-mysql (server name is globally unique)</span></span> |
| <span data-ttu-id="51be5-120">*Assinatura*</span><span class="sxs-lookup"><span data-stu-id="51be5-120">*Subscription*</span></span> | <span data-ttu-id="51be5-121">MySQLaaS (selecione na lista suspensa)</span><span class="sxs-lookup"><span data-stu-id="51be5-121">MySQLaaS (select from drop down)</span></span> |
| <span data-ttu-id="51be5-122">*Grupo de recursos*</span><span class="sxs-lookup"><span data-stu-id="51be5-122">*Resource group*</span></span> | <span data-ttu-id="51be5-123">myresource (crie um novo grupo de recursos ou use um existente)</span><span class="sxs-lookup"><span data-stu-id="51be5-123">myresource (create a new resource group or use an existing one)</span></span> |
| <span data-ttu-id="51be5-124">*Logon de administrador do servidor*</span><span class="sxs-lookup"><span data-stu-id="51be5-124">*Server admin login*</span></span> | <span data-ttu-id="51be5-125">myadmin (nome de conta do administrador de configuração)</span><span class="sxs-lookup"><span data-stu-id="51be5-125">myadmin (setup admin account name)</span></span> |
| <span data-ttu-id="51be5-126">*Senha*</span><span class="sxs-lookup"><span data-stu-id="51be5-126">*Password*</span></span> | <span data-ttu-id="51be5-127">configurar senha da conta do administrador</span><span class="sxs-lookup"><span data-stu-id="51be5-127">setup admin account password</span></span> |
| <span data-ttu-id="51be5-128">*Confirmar senha*</span><span class="sxs-lookup"><span data-stu-id="51be5-128">*Confirm password*</span></span> | <span data-ttu-id="51be5-129">confirmar senha da conta do administrador</span><span class="sxs-lookup"><span data-stu-id="51be5-129">confirm admin account password</span></span> |
| <span data-ttu-id="51be5-130">*Localidade*</span><span class="sxs-lookup"><span data-stu-id="51be5-130">*Location*</span></span> | <span data-ttu-id="51be5-131">Europa Setentrional (escolha entre o Europa Setentrional e Oeste dos EUA)</span><span class="sxs-lookup"><span data-stu-id="51be5-131">North Europe (select between North Europe and West US)</span></span> |
| <span data-ttu-id="51be5-132">*Versão*</span><span class="sxs-lookup"><span data-stu-id="51be5-132">*Version*</span></span> | <span data-ttu-id="51be5-133">5.6 (escolha uma versão do servidor de Banco de Dados do Azure para MySQL)</span><span class="sxs-lookup"><span data-stu-id="51be5-133">5.6 (choose Azure Database for MySQL server version)</span></span> |

<span data-ttu-id="51be5-134">4 Clique **preço** toospecify Olá desempenho e da camada de nível de serviço para o novo servidor.</span><span class="sxs-lookup"><span data-stu-id="51be5-134">4- Click **Pricing tier** toospecify hello service tier and performance level for your new server.</span></span> <span data-ttu-id="51be5-135">Unidade de Computação pode ser configurada entre 50 e 100 no Tipo básico, 100 e 200 no Tipo Standard, e o armazenamento pode ser adicionado com base na quantidade incluída.</span><span class="sxs-lookup"><span data-stu-id="51be5-135">Compute Unit can be configured between 50 and 100 in Basic tier, 100 and 200 in Standard tier, and storage can be added based on included amount.</span></span> <span data-ttu-id="51be5-136">Para este guia de instruções, vamos escolher 50 Unidades de Computação e 50 GB.</span><span class="sxs-lookup"><span data-stu-id="51be5-136">For this HowTo guide, let’s choose 50 Compute Unit and 50GB.</span></span> <span data-ttu-id="51be5-137">Clique em **Okey** toosave sua seleção.</span><span class="sxs-lookup"><span data-stu-id="51be5-137">Click **OK** toosave your selection.</span></span>
<span data-ttu-id="51be5-138">![create-server-pricing-tier](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)</span><span class="sxs-lookup"><span data-stu-id="51be5-138">![create-server-pricing-tier](./media/howto-create-manage-server-portal/create-server-pricing-tier.png)</span></span>

<span data-ttu-id="51be5-139">5 Clique **criar** tooprovision servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="51be5-139">5- Click **Create** tooprovision hello server.</span></span> <span data-ttu-id="51be5-140">O provisionamento demora alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="51be5-140">Provisioning takes a few minutes.</span></span>

> <span data-ttu-id="51be5-141">Verificar Olá **toodashboard Pin** opção tooallow facilidade no rastreamento de suas implantações.</span><span class="sxs-lookup"><span data-stu-id="51be5-141">Check hello **Pin toodashboard** option tooallow easy tracking of your deployments.</span></span>
> [!NOTE]
> <span data-ttu-id="51be5-142">Embora o too1000GB na camada básica e 10000GB no padrão camada terá suporte para o armazenamento, para visualização pública, armazenamento máximo hello está temporariamente too1000GB ainda limitado.</span><span class="sxs-lookup"><span data-stu-id="51be5-142">Although up too1000GB in Basic tier and 10000GB in Standard tier will be supported for storage, for Public Preview, hello maximum storage is still limited too1000GB temporarily.</span></span> 
</Include>

## <a name="update-an-azure-database-for-mysql-server"></a><span data-ttu-id="51be5-143">Atualizar um servidor de Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="51be5-143">Update an Azure Database for MySQL server</span></span>
<span data-ttu-id="51be5-144">Depois que o novo servidor é configurado, o usuário tem 2 tooedit de opções um servidor existente: redefinir a senha de administrador ou de escala para cima/para baixo do servidor de saudação alterando Olá as unidades de computação.</span><span class="sxs-lookup"><span data-stu-id="51be5-144">After new server is provisioned, user has 2 options tooedit an existing server: reset administrator password or scale up/down hello server by changing hello compute-units.</span></span>

### <a name="change-hello-administrator-user-password"></a><span data-ttu-id="51be5-145">Alterar senha de usuário de administrador Olá</span><span class="sxs-lookup"><span data-stu-id="51be5-145">Change hello administrator user password</span></span>
<span data-ttu-id="51be5-146">1 - no servidor de saudação **visão geral** folha, clique em **Redefinir senha** toopopulate uma janela de entrada e a confirmação de senha.</span><span class="sxs-lookup"><span data-stu-id="51be5-146">1- On hello server **Overview** blade, click **Reset password** toopopulate a password input and confirmation window.</span></span>

<span data-ttu-id="51be5-147">2 - Insira a nova senha e Confirmar senha Olá na janela hello como abaixo: ![redefinição de senha](./media/howto-create-manage-server-portal/reset-password.png)</span><span class="sxs-lookup"><span data-stu-id="51be5-147">2- Enter new password and confirm hello password in hello window as below: ![reset-password](./media/howto-create-manage-server-portal/reset-password.png)</span></span>

<span data-ttu-id="51be5-148">3 Clique **Okey** nova senha do toosave hello.</span><span class="sxs-lookup"><span data-stu-id="51be5-148">3- Click **OK** toosave hello new password.</span></span>

### <a name="scale-updown-by-changing-compute-units"></a><span data-ttu-id="51be5-149">Escalar verticalmente alterando as Unidades de Computação</span><span class="sxs-lookup"><span data-stu-id="51be5-149">Scale up/down by changing Compute Units</span></span>

<span data-ttu-id="51be5-150">1 - na folha do servidor de saudação, em **configurações**, clique em **preço** folha de camada de preços tooopen Olá para hello banco de dados para o servidor MySQL.</span><span class="sxs-lookup"><span data-stu-id="51be5-150">1- On hello server blade, under **Settings**, click **Pricing tier** tooopen hello Pricing tier blade for hello Azure Database for MySQL server.</span></span>

<span data-ttu-id="51be5-151">A etapa 2-siga 4 **criar um banco de dados do Azure para o MySQL server** toochange unidades de computação em Olá mesma camada de preços.</span><span class="sxs-lookup"><span data-stu-id="51be5-151">2- Follow Step 4 in **Create an Azure Database for MySQL server** toochange Compute Units in hello same pricing tier.</span></span>

## <a name="delete-an-azure-database-for-mysql-server"></a><span data-ttu-id="51be5-152">Excluir um servidor de Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="51be5-152">Delete an Azure Database for MySQL server</span></span>

<span data-ttu-id="51be5-153">1 - no servidor de saudação **visão geral** folha, clique em **excluir** folha de confirmação de exclusão do comando botão tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="51be5-153">1- On hello server **Overview** blade, click **Delete** command button tooopen hello Deleting confirmation blade.</span></span>

<span data-ttu-id="51be5-154">Nome do servidor correto Olá 2-tipo na caixa de entrada da folha de saudação confirmação duplo.</span><span class="sxs-lookup"><span data-stu-id="51be5-154">2- Type hello correct server name in input box of hello blade for double confirmation.</span></span>

<span data-ttu-id="51be5-155">3 Clique **excluir** novamente tooconfirm ação de exclusão e aguarde o pop-up "Excluindo sucesso" na barra de notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="51be5-155">3- Click **Delete** button again tooconfirm deleting action and wait for “Deleting success” popup on hello notification bar.</span></span>

## <a name="list-hello-azure-database-for-mysql-databases"></a><span data-ttu-id="51be5-156">Lista hello banco de dados do Azure para bancos de dados MySQL</span><span class="sxs-lookup"><span data-stu-id="51be5-156">List hello Azure Database for MySQL databases</span></span>
<span data-ttu-id="51be5-157">No servidor de saudação **visão geral** folha, role para baixo até ver o banco de dados de saudação lado a lado na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="51be5-157">On hello server **Overview** blade, scroll down until you see hello database tile on hello bottom.</span></span> <span data-ttu-id="51be5-158">Todos os bancos de dados hello serão listados na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="51be5-158">All hello databases will be listed in hello table.</span></span> <span data-ttu-id="51be5-159">Clique em **excluir** folha de confirmação de exclusão do comando botão tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="51be5-159">click **Delete** command button tooopen hello Deleting confirmation blade.</span></span>

![show-databases](./media/howto-create-manage-server-portal/show-databases.png)

## <a name="show-details-of-an-azure-database-for-mysql-server"></a><span data-ttu-id="51be5-161">Mostrar detalhes de um servidor de Banco de Dados do Azure para MySQL</span><span class="sxs-lookup"><span data-stu-id="51be5-161">Show details of an Azure Database for MySQL server</span></span>
<span data-ttu-id="51be5-162">Clique em **propriedades** em **configurações** no servidor de saudação folha será aberta, Olá **propriedades** folha.</span><span class="sxs-lookup"><span data-stu-id="51be5-162">Click **Properties** under **Settings** on hello server blade will open hello **Properties** blade.</span></span> <span data-ttu-id="51be5-163">Em seguida, você pode exibir todas as informações detalhadas sobre o servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="51be5-163">Then you can view all detailed information about hello server.</span></span>

## <a name="next-steps"></a><span data-ttu-id="51be5-164">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="51be5-164">Next steps</span></span>

[<span data-ttu-id="51be5-165">Início rápido: criar e gerenciar um servidor de Banco de Dados do Azure para MySQL usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="51be5-165">Quickstart: Create Azure Database for MySQL server using Azure portal</span></span>](./quickstart-create-mysql-server-database-using-azure-portal.md)
