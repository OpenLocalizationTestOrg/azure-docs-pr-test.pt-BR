---
title: Gerenciar o Azure Data Lake Analytics usando o portal do Azure | Microsoft Docs
description: "Saiba como gerenciar contas, fontes de dados, usuários e trabalhos da Análise Data Lake."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: a0e045f1-73d6-427f-868d-7b55c10f811b
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: e49d1a0e0ccc6567d0a6841817667717ff5dba76
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-azure-data-lake-analytics-by-using-the-azure-portal"></a><span data-ttu-id="6a79e-103">Gerenciar o Azure Data Lake Analytics usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6a79e-103">Manage Azure Data Lake Analytics by using the Azure portal</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="6a79e-104">Saiba como gerenciar contas, fontes de dados da conta, usuários e trabalhos do Azure Data Lake Analytics usando o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6a79e-104">Learn how to manage Azure Data Lake Analytics accounts, account data sources, users, and jobs by using the Azure portal.</span></span> <span data-ttu-id="6a79e-105">Para ver os tópicos de gerenciamento sobre como usar outras ferramentas, clique na guia na parte superior da página.</span><span class="sxs-lookup"><span data-stu-id="6a79e-105">To see management topics about using other tools, click a tab at the top of the page.</span></span>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-lake-analytics-accounts"></a><span data-ttu-id="6a79e-106">Gerenciar contas do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="6a79e-106">Manage Data Lake Analytics accounts</span></span>

### <a name="create-an-account"></a><span data-ttu-id="6a79e-107">Criar uma conta</span><span class="sxs-lookup"><span data-stu-id="6a79e-107">Create an account</span></span>

1. <span data-ttu-id="6a79e-108">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6a79e-108">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6a79e-109">Clique em **Novo** > **Intelligence + análise** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="6a79e-109">Click **New** > **Intelligence + analytics** > **Data Lake Analytics**.</span></span>
3. <span data-ttu-id="6a79e-110">Selecione os valores para os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="6a79e-110">Select values for the following items:</span></span> 
   1. <span data-ttu-id="6a79e-111">**Nome**: o nome da conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="6a79e-111">**Name**: The name of the Data Lake Analytics account.</span></span>
   2. <span data-ttu-id="6a79e-112">**Assinatura**: a assinatura do Azure usada para a conta.</span><span class="sxs-lookup"><span data-stu-id="6a79e-112">**Subscription**: The Azure subscription used for the account.</span></span>
   3. <span data-ttu-id="6a79e-113">**Grupo de recursos**: o grupo de recursos do Azure no qual a conta será criada.</span><span class="sxs-lookup"><span data-stu-id="6a79e-113">**Resource Group**: The Azure resource group in which to create the account.</span></span> 
   4. <span data-ttu-id="6a79e-114">**Local**: o datacenter do Azure para a conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="6a79e-114">**Location**: The Azure datacenter for the Data Lake Analytics account.</span></span> 
   5. <span data-ttu-id="6a79e-115">**Data Lake Store**: o repositório padrão a ser usado para a conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="6a79e-115">**Data Lake Store**: The default store to be used for the Data Lake Analytics account.</span></span> <span data-ttu-id="6a79e-116">A conta do Azure Data Lake Store e a conta do Data Lake Analytics devem estar no mesmo local.</span><span class="sxs-lookup"><span data-stu-id="6a79e-116">The Azure Data Lake Store account and the Data Lake Analytics account must be in the same location.</span></span>
4. <span data-ttu-id="6a79e-117">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="6a79e-117">Click **Create**.</span></span> 

### <a name="delete-a-data-lake-analytics-account"></a><span data-ttu-id="6a79e-118">Excluir uma conta do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="6a79e-118">Delete a Data Lake Analytics account</span></span>

<span data-ttu-id="6a79e-119">Antes de excluir uma conta do Data Lake Analytics, exclua sua conta padrão do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="6a79e-119">Before you delete a Data Lake Analytics account, delete its default Data Lake Store account.</span></span>

1. <span data-ttu-id="6a79e-120">No portal do Azure, acesse sua conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="6a79e-120">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="6a79e-121">Clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="6a79e-121">Click **Delete**.</span></span>
3. <span data-ttu-id="6a79e-122">Digite o nome da conta.</span><span class="sxs-lookup"><span data-stu-id="6a79e-122">Type the account name.</span></span>
4. <span data-ttu-id="6a79e-123">Clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="6a79e-123">Click **Delete**.</span></span>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-sources"></a><span data-ttu-id="6a79e-124">Gerenciar as fontes de dados</span><span class="sxs-lookup"><span data-stu-id="6a79e-124">Manage data sources</span></span>

<span data-ttu-id="6a79e-125">O Data Lake Analytics dá suporte às seguintes fontes de dados:</span><span class="sxs-lookup"><span data-stu-id="6a79e-125">Data Lake Analytics supports the following data sources:</span></span>

* <span data-ttu-id="6a79e-126">Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="6a79e-126">Data Lake Store</span></span>
* <span data-ttu-id="6a79e-127">Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="6a79e-127">Azure Storage</span></span>

<span data-ttu-id="6a79e-128">Você pode usar o Data Explorer para procurar fontes de dados e executar operações básicas de gerenciamento de arquivo.</span><span class="sxs-lookup"><span data-stu-id="6a79e-128">You can use Data Explorer to browse data sources and perform basic file management operations.</span></span> 

### <a name="add-a-data-source"></a><span data-ttu-id="6a79e-129">Adicionar uma fonte de dados</span><span class="sxs-lookup"><span data-stu-id="6a79e-129">Add a data source</span></span>

1. <span data-ttu-id="6a79e-130">No portal do Azure, acesse sua conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="6a79e-130">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="6a79e-131">Clique em **Fontes de Dados**.</span><span class="sxs-lookup"><span data-stu-id="6a79e-131">Click **Data Sources**.</span></span>
3. <span data-ttu-id="6a79e-132">Clique em **Adicionar Fonte de Dados**.</span><span class="sxs-lookup"><span data-stu-id="6a79e-132">Click **Add Data Source**.</span></span>
    
   * <span data-ttu-id="6a79e-133">Para adicionar uma conta do Data Lake Store, são necessários o nome da conta e o acesso à conta para poder consultá-la.</span><span class="sxs-lookup"><span data-stu-id="6a79e-133">To add a Data Lake Store account, you need the account name and access to the account to be able to query it.</span></span>
   * <span data-ttu-id="6a79e-134">Para adicionar o armazenamento de Blobs do Azure, são necessárias a conta de armazenamento e a chave de conta.</span><span class="sxs-lookup"><span data-stu-id="6a79e-134">To add Azure Blob storage, you need the storage account and the account key.</span></span> <span data-ttu-id="6a79e-135">Para encontrá-las, acesse a conta de armazenamento no portal.</span><span class="sxs-lookup"><span data-stu-id="6a79e-135">To find them, go to the storage account in the portal.</span></span>

## <a name="set-up-firewall-rules"></a><span data-ttu-id="6a79e-136">Configurar regras de firewall</span><span class="sxs-lookup"><span data-stu-id="6a79e-136">Set up firewall rules</span></span>

<span data-ttu-id="6a79e-137">Você pode usar o Data Lake Analytics para bloquear ainda mais o acesso à sua conta do Data Lake Analytics no nível da rede.</span><span class="sxs-lookup"><span data-stu-id="6a79e-137">You can use Data Lake Analytics to further lock down access to your Data Lake Analytics account at the network level.</span></span> <span data-ttu-id="6a79e-138">Você pode habilitar um firewall e definir um endereço IP ou um intervalo de endereços IP para seus clientes confiáveis.</span><span class="sxs-lookup"><span data-stu-id="6a79e-138">You can enable a firewall, specify an IP address, or define an IP address range for your trusted clients.</span></span> <span data-ttu-id="6a79e-139">Depois de habilitar essas medidas, somente os clientes que tiverem os endereços IP dentro do intervalo definido poderão se conectar ao repositório.</span><span class="sxs-lookup"><span data-stu-id="6a79e-139">After you enable these measures, only clients that have the IP addresses within the defined range can connect to the store.</span></span>

<span data-ttu-id="6a79e-140">Se outros serviços do Azure, como o Azure Data Factory ou VMs, se conectam à conta do Data Lake Analytics, verifique se **Permitir Serviços do Azure** está **Ativado**.</span><span class="sxs-lookup"><span data-stu-id="6a79e-140">If other Azure services, like Azure Data Factory or VMs, connect to the Data Lake Analytics account, make sure that **Allow Azure Services** is turned **On**.</span></span> 

### <a name="set-up-a-firewall-rule"></a><span data-ttu-id="6a79e-141">Configurar uma regra de firewall</span><span class="sxs-lookup"><span data-stu-id="6a79e-141">Set up a firewall rule</span></span>

1. <span data-ttu-id="6a79e-142">No portal do Azure, acesse sua conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="6a79e-142">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="6a79e-143">No menu à esquerda, clique em **Firewall**.</span><span class="sxs-lookup"><span data-stu-id="6a79e-143">On the menu on the left, click **Firewall**.</span></span>

## <a name="add-a-new-user"></a><span data-ttu-id="6a79e-144">Adicione um novo usuário</span><span class="sxs-lookup"><span data-stu-id="6a79e-144">Add a new user</span></span>

<span data-ttu-id="6a79e-145">Você pode usar o **Assistente para Adicionar Usuário** para provisionar facilmente novos usuários do Data Lake.</span><span class="sxs-lookup"><span data-stu-id="6a79e-145">You can use the **Add User Wizard** to easily provision new Data Lake users.</span></span>

1. <span data-ttu-id="6a79e-146">No portal do Azure, acesse sua conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="6a79e-146">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="6a79e-147">À esquerda, em **Introdução**, clique em **Assistente para Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="6a79e-147">On the left, under **Getting Started**, click **Add User Wizard**.</span></span>
3. <span data-ttu-id="6a79e-148">Selecione um usuário e, em seguida, clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="6a79e-148">Select a user, and then click **Select**.</span></span>
4. <span data-ttu-id="6a79e-149">Selecione uma função e, em seguida, clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="6a79e-149">Select a role, and then click **Select**.</span></span> <span data-ttu-id="6a79e-150">Para configurar um novo desenvolvedor para usar o Azure Data Lake, selecione a função **Desenvolvedor do Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="6a79e-150">To set up a new developer to use Azure Data Lake, select the **Data Lake Analytics Developer** role.</span></span>
5. <span data-ttu-id="6a79e-151">Selecione as ACLs (listas de controle de acesso) para os bancos de dados U-SQL.</span><span class="sxs-lookup"><span data-stu-id="6a79e-151">Select the access control lists (ACLs) for the U-SQL databases.</span></span> <span data-ttu-id="6a79e-152">Quando estiver satisfeito com suas escolhas, clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="6a79e-152">When you're satisfied with your choices, click **Select**.</span></span>
6. <span data-ttu-id="6a79e-153">Selecione as ACLs de arquivos.</span><span class="sxs-lookup"><span data-stu-id="6a79e-153">Select the ACLs for files.</span></span> <span data-ttu-id="6a79e-154">Para o repositório padrão, não altere as ACLs da pasta raiz "/" e da pasta /system.</span><span class="sxs-lookup"><span data-stu-id="6a79e-154">For the default store, don't change the ACLs for the root folder "/" and for the /system folder.</span></span> <span data-ttu-id="6a79e-155">Clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="6a79e-155">Click **Select**.</span></span>
7. <span data-ttu-id="6a79e-156">Examine todas as alterações selecionadas e, em seguida, clique em **Executar**.</span><span class="sxs-lookup"><span data-stu-id="6a79e-156">Review all your selected changes, and then click **Run**.</span></span>
8. <span data-ttu-id="6a79e-157">Quando o assistente for concluído, clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="6a79e-157">When the wizard is finished, click **Done**.</span></span>

## <a name="manage-role-based-access-control"></a><span data-ttu-id="6a79e-158">Gerenciar o controle de acesso baseado em função</span><span class="sxs-lookup"><span data-stu-id="6a79e-158">Manage Role-Based Access Control</span></span>

<span data-ttu-id="6a79e-159">Como outros serviços do Azure, você pode usar o RBAC (controle de acesso baseado em função) para controlar como os usuários interagem com o serviço.</span><span class="sxs-lookup"><span data-stu-id="6a79e-159">Like other Azure services, you can use Role-Based Access Control (RBAC) to control how users interact with the service.</span></span>

<span data-ttu-id="6a79e-160">As funções padrão do RBAC têm os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="6a79e-160">The standard RBAC roles have the following capabilities:</span></span>
* <span data-ttu-id="6a79e-161">**Proprietário**: pode enviar, monitorar e cancelar trabalhos de qualquer usuário e configurar a conta.</span><span class="sxs-lookup"><span data-stu-id="6a79e-161">**Owner**: Can submit jobs, monitor jobs, cancel jobs from any user, and configure the account.</span></span>
* <span data-ttu-id="6a79e-162">**Colaborador**: pode enviar, monitorar e cancelar trabalhos de qualquer usuário e configurar a conta.</span><span class="sxs-lookup"><span data-stu-id="6a79e-162">**Contributor**: Can submit jobs, monitor jobs, cancel jobs from any user, and configure the account.</span></span>
* <span data-ttu-id="6a79e-163">**Leitor**: pode monitorar trabalhos.</span><span class="sxs-lookup"><span data-stu-id="6a79e-163">**Reader**: Can monitor jobs.</span></span>

<span data-ttu-id="6a79e-164">Use a função de desenvolvedor do Data Lake Analytics para permitir que os desenvolvedores de U-SQL usem o serviço do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="6a79e-164">Use the Data Lake Analytics Developer role to enable U-SQL developers to use the Data Lake Analytics service.</span></span> <span data-ttu-id="6a79e-165">Você pode usar a função de desenvolvedor do Data Lake Analytics:</span><span class="sxs-lookup"><span data-stu-id="6a79e-165">You can use the Data Lake Analytics Developer role to:</span></span>
* <span data-ttu-id="6a79e-166">Enviar trabalhos.</span><span class="sxs-lookup"><span data-stu-id="6a79e-166">Submit jobs.</span></span>
* <span data-ttu-id="6a79e-167">Monitorar o status do trabalho e o andamento dos trabalhos enviados por qualquer usuário.</span><span class="sxs-lookup"><span data-stu-id="6a79e-167">Monitor job status and the progress of jobs submitted by any user.</span></span>
* <span data-ttu-id="6a79e-168">Consultar os scripts de U-SQL de trabalhos enviados por qualquer usuário.</span><span class="sxs-lookup"><span data-stu-id="6a79e-168">See the U-SQL scripts from jobs submitted by any user.</span></span>
* <span data-ttu-id="6a79e-169">Cancelar apenas seus próprios trabalhos.</span><span class="sxs-lookup"><span data-stu-id="6a79e-169">Cancel only your own jobs.</span></span>

### <a name="add-users-or-security-groups-to-a-data-lake-analytics-account"></a><span data-ttu-id="6a79e-170">Adicionar usuários ou grupos de segurança a uma conta do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="6a79e-170">Add users or security groups to a Data Lake Analytics account</span></span>

1. <span data-ttu-id="6a79e-171">No portal do Azure, acesse sua conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="6a79e-171">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="6a79e-172">Clique em **Controle de acesso (IAM)** > **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="6a79e-172">Click **Access control (IAM)** > **Add**.</span></span>
3. <span data-ttu-id="6a79e-173">Selecione uma função.</span><span class="sxs-lookup"><span data-stu-id="6a79e-173">Select a role.</span></span>
4. <span data-ttu-id="6a79e-174">Adicione um usuário.</span><span class="sxs-lookup"><span data-stu-id="6a79e-174">Add a user.</span></span>
5. <span data-ttu-id="6a79e-175">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="6a79e-175">Click **OK**.</span></span>

>[!NOTE]
><span data-ttu-id="6a79e-176">Se um usuário ou um grupo de segurança precisar enviar trabalhos, eles também precisarão de permissão na conta de repositório.</span><span class="sxs-lookup"><span data-stu-id="6a79e-176">If a user or a security group needs to submit jobs, they also need permission on the store account.</span></span> <span data-ttu-id="6a79e-177">Para obter mais informações, consulte [Proteger os dados armazenados no Data Lake Store](../data-lake-store/data-lake-store-secure-data.md).</span><span class="sxs-lookup"><span data-stu-id="6a79e-177">For more information, see [Secure data stored in Data Lake Store](../data-lake-store/data-lake-store-secure-data.md).</span></span>
>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-jobs"></a><span data-ttu-id="6a79e-178">Gerenciar trabalhos</span><span class="sxs-lookup"><span data-stu-id="6a79e-178">Manage jobs</span></span>

### <a name="submit-a-job"></a><span data-ttu-id="6a79e-179">Enviar um trabalho</span><span class="sxs-lookup"><span data-stu-id="6a79e-179">Submit a job</span></span>

1. <span data-ttu-id="6a79e-180">No portal do Azure, acesse sua conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="6a79e-180">In the Azure portal, go to your Data Lake Analytics account.</span></span>

2. <span data-ttu-id="6a79e-181">Clique em **Novo Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="6a79e-181">Click **New Job**.</span></span> <span data-ttu-id="6a79e-182">Para cada trabalho, configure:</span><span class="sxs-lookup"><span data-stu-id="6a79e-182">For each job,  configure:</span></span>

    1. <span data-ttu-id="6a79e-183">**Nome do Trabalho**: o nome do trabalho.</span><span class="sxs-lookup"><span data-stu-id="6a79e-183">**Job Name**: The name of the job.</span></span>
    2. <span data-ttu-id="6a79e-184">**Prioridade**: números menores têm prioridade mais alta.</span><span class="sxs-lookup"><span data-stu-id="6a79e-184">**Priority**: Lower numbers have higher priority.</span></span> <span data-ttu-id="6a79e-185">Se dois trabalhos estiverem enfileirados, aquele com o menor valor de prioridade será executado primeiro.</span><span class="sxs-lookup"><span data-stu-id="6a79e-185">If two jobs are queued, the one with lower priority value runs first.</span></span>
    3. <span data-ttu-id="6a79e-186">**Paralelismo**: o número máximo de processos de computação a serem reservados para este trabalho.</span><span class="sxs-lookup"><span data-stu-id="6a79e-186">**Parallelism**: The maximum number of compute processes to reserve for this job.</span></span>

3. <span data-ttu-id="6a79e-187">Clique em **Enviar Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="6a79e-187">Click **Submit Job**.</span></span>

### <a name="monitor-jobs"></a><span data-ttu-id="6a79e-188">Monitorar trabalhos</span><span class="sxs-lookup"><span data-stu-id="6a79e-188">Monitor jobs</span></span>

1. <span data-ttu-id="6a79e-189">No portal do Azure, acesse sua conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="6a79e-189">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="6a79e-190">Clique em **Exibir Todos os Trabalhos**.</span><span class="sxs-lookup"><span data-stu-id="6a79e-190">Click **View All Jobs**.</span></span> <span data-ttu-id="6a79e-191">Uma lista de todos os trabalhos ativos e concluídos recentemente é exibida.</span><span class="sxs-lookup"><span data-stu-id="6a79e-191">A list of all the active and recently finished jobs in the account is shown.</span></span>
3. <span data-ttu-id="6a79e-192">Opcionalmente, clique em **Filtrar** para ajudá-lo a localizar os trabalhos por valores de **Intervalo de Tempo**, **Nome do Trabalho** e **Autor**.</span><span class="sxs-lookup"><span data-stu-id="6a79e-192">Optionally, click **Filter** to help you find the jobs by **Time Range**, **Job Name**, and **Author** values.</span></span> 

### <a name="monitoring-pipeline-jobs"></a><span data-ttu-id="6a79e-193">Monitorando trabalhos de pipeline</span><span class="sxs-lookup"><span data-stu-id="6a79e-193">Monitoring pipeline jobs</span></span>
<span data-ttu-id="6a79e-194">Trabalhos que fazem parte de um pipeline trabalham juntos, geralmente em sequência, para realizar um cenário específico.</span><span class="sxs-lookup"><span data-stu-id="6a79e-194">Jobs that are part of a pipeline work together, usually sequentially, to accomplish a specific scenario.</span></span> <span data-ttu-id="6a79e-195">Por exemplo, você pode ter um pipeline que limpa, extrai, transforma, agrega o uso de Customer Insights.</span><span class="sxs-lookup"><span data-stu-id="6a79e-195">For example, you can have a pipeline that cleans, extracts, transforms, aggregates usage for customer insights.</span></span> <span data-ttu-id="6a79e-196">Trabalhos do pipeline são identificados usando a propriedade "Pipeline" quando o trabalho foi enviado.</span><span class="sxs-lookup"><span data-stu-id="6a79e-196">Pipeline jobs are identified using the "Pipeline" property when the job was submitted.</span></span> <span data-ttu-id="6a79e-197">Trabalhos agendados usando o ADF V2 terão, automaticamente, essa propriedade populada.</span><span class="sxs-lookup"><span data-stu-id="6a79e-197">Jobs scheduled using ADF V2 will automatically have this property populated.</span></span> 

<span data-ttu-id="6a79e-198">Para exibir uma lista de trabalhos de U-SQL que fazem parte dos pipelines:</span><span class="sxs-lookup"><span data-stu-id="6a79e-198">To view a list of U-SQL jobs that are part of pipelines:</span></span> 

1. <span data-ttu-id="6a79e-199">No portal do Azure, acesse sua conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="6a79e-199">In the Azure portal, go to your Data Lake Analytics accounts.</span></span>
2. <span data-ttu-id="6a79e-200">Clique em **Insights de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="6a79e-200">Click **Job Insights**.</span></span> <span data-ttu-id="6a79e-201">A guia "Todos os trabalhos" será padronizada, mostrando trabalhos em execução, na fila e encerrados.</span><span class="sxs-lookup"><span data-stu-id="6a79e-201">The "All Jobs" tab will be defaulted, showing a list of running, queued, and ended jobs.</span></span>
3. <span data-ttu-id="6a79e-202">Clique na guia **Trabalhos de pipeline**. Uma lista de trabalhos do pipeline será mostrada juntamente com estatísticas agregadas para cada pipeline.</span><span class="sxs-lookup"><span data-stu-id="6a79e-202">Click the **Pipeline Jobs** tab. A list of pipeline jobs will be shown along with aggregated statistics for each pipeline.</span></span>

### <a name="monitoring-recurring-jobs"></a><span data-ttu-id="6a79e-203">Monitorando trabalhos recorrentes</span><span class="sxs-lookup"><span data-stu-id="6a79e-203">Monitoring recurring jobs</span></span>
<span data-ttu-id="6a79e-204">Um trabalho recorrente é aquele que tem a mesma lógica de negócios, mas usa dados de entrada diferentes toda vez que é executado.</span><span class="sxs-lookup"><span data-stu-id="6a79e-204">A recurring job is one that has the same business logic but uses different input data every time it runs.</span></span> <span data-ttu-id="6a79e-205">Idealmente, trabalhos recorrentes devem sempre ter êxito e ter um tempo de execução relativamente estável. O monitoramento desses comportamentos ajuda a garantir que o trabalho tenha integridade.</span><span class="sxs-lookup"><span data-stu-id="6a79e-205">Ideally, recurring jobs should always succeed, and have relatively stable execution time; monitoring these behaviors will help ensure the job is healthy.</span></span> <span data-ttu-id="6a79e-206">Trabalhos recorrentes são identificados usando a propriedade "Recorrente".</span><span class="sxs-lookup"><span data-stu-id="6a79e-206">Recurring jobs are identified using the "Recurrence" property.</span></span> <span data-ttu-id="6a79e-207">Trabalhos agendados usando o ADF V2 terão, automaticamente, essa propriedade populada.</span><span class="sxs-lookup"><span data-stu-id="6a79e-207">Jobs scheduled using ADF V2 will automatically have this property populated.</span></span>

<span data-ttu-id="6a79e-208">Para exibir uma lista de trabalhos de U-SQL que são recorrentes:</span><span class="sxs-lookup"><span data-stu-id="6a79e-208">To view a list of U-SQL jobs that are recurring:</span></span> 

1. <span data-ttu-id="6a79e-209">No portal do Azure, acesse sua conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="6a79e-209">In the Azure portal, go to your Data Lake Analytics accounts.</span></span>
2. <span data-ttu-id="6a79e-210">Clique em **Insights de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="6a79e-210">Click **Job Insights**.</span></span> <span data-ttu-id="6a79e-211">A guia "Todos os trabalhos" será padronizada, mostrando trabalhos em execução, na fila e encerrados.</span><span class="sxs-lookup"><span data-stu-id="6a79e-211">The "All Jobs" tab will be defaulted, showing a list of running, queued, and ended jobs.</span></span>
3. <span data-ttu-id="6a79e-212">Clique na guia **Trabalhos recorrentes**. Uma lista de trabalhos recorrentes será mostrada juntamente com estatísticas agregadas para cada trabalho recorrente.</span><span class="sxs-lookup"><span data-stu-id="6a79e-212">Click the **Recurring Jobs** tab. A list of recurring jobs will be shown along with aggregated statistics for each recurring job.</span></span>

## <a name="manage-policies"></a><span data-ttu-id="6a79e-213">Gerenciar políticas</span><span class="sxs-lookup"><span data-stu-id="6a79e-213">Manage policies</span></span>

### <a name="account-level-policies"></a><span data-ttu-id="6a79e-214">Políticas no nível da conta</span><span class="sxs-lookup"><span data-stu-id="6a79e-214">Account-level policies</span></span>

<span data-ttu-id="6a79e-215">Essas políticas aplicam-se a todos os trabalhos em uma conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="6a79e-215">These policies apply to all jobs in a Data Lake Analytics account.</span></span>

#### <a name="maximum-number-of-aus-in-a-data-lake-analytics-account"></a><span data-ttu-id="6a79e-216">Número máximo de AUs em uma conta do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="6a79e-216">Maximum number of AUs in a Data Lake Analytics account</span></span>
<span data-ttu-id="6a79e-217">Uma política controla o número total de AUs (Unidades de Análise) que a conta do Data Lake Analytics pode usar.</span><span class="sxs-lookup"><span data-stu-id="6a79e-217">A policy controls the total number of Analytics Units (AUs) your Data Lake Analytics account can use.</span></span> <span data-ttu-id="6a79e-218">Por padrão, o valor é definido como 250.</span><span class="sxs-lookup"><span data-stu-id="6a79e-218">By default, the value is set to 250.</span></span> <span data-ttu-id="6a79e-219">Por exemplo, se esse valor for definido como 250 AUs, você poderá ter um trabalho em execução com 250 AUs atribuídas ou 10 trabalhos em execução com 25 AUs cada um.</span><span class="sxs-lookup"><span data-stu-id="6a79e-219">For example, if this value is set to 250 AUs, you can have one job running with 250 AUs assigned to it, or 10 jobs running with 25 AUs each.</span></span> <span data-ttu-id="6a79e-220">Os trabalhos adicionais enviados são enfileirados até que os trabalhos em execução sejam concluídos.</span><span class="sxs-lookup"><span data-stu-id="6a79e-220">Additional jobs that are submitted are queued until the running jobs are finished.</span></span> <span data-ttu-id="6a79e-221">Quando os trabalhos em execução são concluídos, as AUs são liberadas para que os trabalhos na fila sejam executados.</span><span class="sxs-lookup"><span data-stu-id="6a79e-221">When running jobs are finished, AUs are freed up for the queued jobs to run.</span></span>

<span data-ttu-id="6a79e-222">Para alterar o número de AUs da sua conta do Data Lake Analytics:</span><span class="sxs-lookup"><span data-stu-id="6a79e-222">To change the number of AUs for your Data Lake Analytics account:</span></span>

1. <span data-ttu-id="6a79e-223">No portal do Azure, acesse sua conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="6a79e-223">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="6a79e-224">Clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="6a79e-224">Click **Properties**.</span></span>
3. <span data-ttu-id="6a79e-225">Em **Máximo de AUs**, mova o controle deslizante para selecionar um valor ou insira o valor na caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="6a79e-225">Under **Maximum AUs**, move the slider to select a value, or enter the value in the text box.</span></span> 
4. <span data-ttu-id="6a79e-226">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="6a79e-226">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="6a79e-227">Se você precisar de mais do que as AUs padrão (250), no portal, clique em **Ajuda + Suporte** para enviar uma solicitação de suporte.</span><span class="sxs-lookup"><span data-stu-id="6a79e-227">If you need more than the default (250) AUs, in the portal, click **Help+Support** to submit a support request.</span></span> <span data-ttu-id="6a79e-228">O número de AUs disponíveis em sua conta do Data Lake Analytics pode ser aumentado.</span><span class="sxs-lookup"><span data-stu-id="6a79e-228">The number of AUs available in your Data Lake Analytics account can be increased.</span></span>
>

#### <a name="maximum-number-of-jobs-that-can-run-simultaneously"></a><span data-ttu-id="6a79e-229">Número máximo de trabalhos que podem ser executados simultaneamente</span><span class="sxs-lookup"><span data-stu-id="6a79e-229">Maximum number of jobs that can run simultaneously</span></span>
<span data-ttu-id="6a79e-230">Uma política controla quantos trabalhos podem ser executados ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="6a79e-230">A policy controls how many jobs can run at the same time.</span></span> <span data-ttu-id="6a79e-231">Por padrão, esse valor é definido como 20.</span><span class="sxs-lookup"><span data-stu-id="6a79e-231">By default, this value is set to 20.</span></span> <span data-ttu-id="6a79e-232">Se o Data Lake Analytics tiver AUs disponíveis, novos trabalhos serão agendados para execução imediata até que o número total de trabalhos em execução atinja o valor dessa política.</span><span class="sxs-lookup"><span data-stu-id="6a79e-232">If your Data Lake Analytics has AUs available, new jobs are scheduled to run immediately until the total number of running jobs reaches the value of this policy.</span></span> <span data-ttu-id="6a79e-233">Quando você alcançar o número máximo de trabalhos que podem ser executados simultaneamente, os próximos trabalhos serão enfileirados em ordem de prioridade até que um ou mais trabalhos em execução sejam concluídos (dependendo da disponibilidade de AU).</span><span class="sxs-lookup"><span data-stu-id="6a79e-233">When you reach the maximum number of jobs that can run simultaneously, subsequent jobs are queued in priority order until one or more running jobs complete (depending on AU availability).</span></span>

<span data-ttu-id="6a79e-234">Para alterar o número de trabalhos que podem ser executadas simultaneamente:</span><span class="sxs-lookup"><span data-stu-id="6a79e-234">To change the number of jobs that can run simultaneously:</span></span>

1. <span data-ttu-id="6a79e-235">No portal do Azure, acesse sua conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="6a79e-235">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="6a79e-236">Clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="6a79e-236">Click **Properties**.</span></span>
3. <span data-ttu-id="6a79e-237">Em **Número Máximo de Trabalhos em Execução**, mova o controle deslizante para selecionar um valor ou insira o valor na caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="6a79e-237">Under **Maximum Number of Running Jobs**, move the slider to select a value, or enter the value in the text box.</span></span> 
4. <span data-ttu-id="6a79e-238">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="6a79e-238">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="6a79e-239">Se você precisar executar mais do que o número de trabalhos padrão (20) no portal, clique em **Ajuda + Suporte** para enviar uma solicitação de suporte.</span><span class="sxs-lookup"><span data-stu-id="6a79e-239">If you need to run more than the default (20) number of jobs, in the portal, click **Help+Support** to submit a support request.</span></span> <span data-ttu-id="6a79e-240">O número de trabalhos que podem ser executados simultaneamente em sua conta do Data Lake Analytics pode ser aumentado.</span><span class="sxs-lookup"><span data-stu-id="6a79e-240">The number of jobs that can run simultaneously in your Data Lake Analytics account can be increased.</span></span>
>

#### <a name="how-long-to-keep-job-metadata-and-resources"></a><span data-ttu-id="6a79e-241">Por quanto tempo os metadados e recursos de trabalho devem ser mantidos</span><span class="sxs-lookup"><span data-stu-id="6a79e-241">How long to keep job metadata and resources</span></span> 
<span data-ttu-id="6a79e-242">Quando os usuários executam trabalhos de U-SQL, o serviço do Data Lake Analytics mantém todos os arquivos relacionados.</span><span class="sxs-lookup"><span data-stu-id="6a79e-242">When your users run U-SQL jobs, the Data Lake Analytics service retains all related files.</span></span> <span data-ttu-id="6a79e-243">Os arquivos relacionados incluem o script U-SQL, os arquivos DLL referenciados no script U-SQL, os recursos compilados e as estatísticas.</span><span class="sxs-lookup"><span data-stu-id="6a79e-243">Related files include the U-SQL script, the DLL files referenced in the U-SQL script, compiled resources, and statistics.</span></span> <span data-ttu-id="6a79e-244">Os arquivos estão na pasta /system/ da conta de armazenamento padrão do Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="6a79e-244">The files are in the /system/ folder of the default Azure Data Lake Storage account.</span></span> <span data-ttu-id="6a79e-245">Esta política controla por quanto tempo esses recursos serão armazenados antes de serem excluídos automaticamente (o padrão é 30 dias).</span><span class="sxs-lookup"><span data-stu-id="6a79e-245">This policy controls how long these resources are stored before they are automatically deleted (the default is 30 days).</span></span> <span data-ttu-id="6a79e-246">Você pode usar esses arquivos para depuração e ajuste de desempenho de trabalhos que serão executados novamente no futuro.</span><span class="sxs-lookup"><span data-stu-id="6a79e-246">You can use these files for debugging, and for performance-tuning of jobs that you'll rerun in the future.</span></span>

<span data-ttu-id="6a79e-247">Para alterar o tempo para reter os recursos e metadados de trabalho:</span><span class="sxs-lookup"><span data-stu-id="6a79e-247">To change how long to keep job metadata and resources:</span></span>

1. <span data-ttu-id="6a79e-248">No portal do Azure, acesse sua conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="6a79e-248">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="6a79e-249">Clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="6a79e-249">Click **Properties**.</span></span>
3. <span data-ttu-id="6a79e-250">Em **Dias para Reter Consultas de Trabalho**, mova o controle deslizante para selecionar um valor ou insira o valor na caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="6a79e-250">Under **Days to Retain Job Queries**, move the slider to select a value, or enter the value in the text box.</span></span>  
4. <span data-ttu-id="6a79e-251">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="6a79e-251">Click **Save**.</span></span>

### <a name="job-level-policies"></a><span data-ttu-id="6a79e-252">Políticas no nível do trabalho</span><span class="sxs-lookup"><span data-stu-id="6a79e-252">Job-level policies</span></span>
<span data-ttu-id="6a79e-253">Com as políticas no nível do trabalho, você pode controlar o máximo de AUs e a prioridade máxima que podem ser definidos por usuários individuais (ou membros de grupos de segurança específicos) nos trabalhos que eles enviam.</span><span class="sxs-lookup"><span data-stu-id="6a79e-253">With job-level policies, you can control the maximum AUs and the maximum priority that individual users (or members of specific security groups) can set on jobs that they submit.</span></span> <span data-ttu-id="6a79e-254">Isso lhe permite controlar os custos gerados pelos usuários.</span><span class="sxs-lookup"><span data-stu-id="6a79e-254">This lets you control the costs incurred by users.</span></span> <span data-ttu-id="6a79e-255">Ele também permite que você controle o efeito que os trabalhos agendados podem ter nos trabalhos de produção de alta prioridade que estão em execução na mesma conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="6a79e-255">It also lets you control the effect that scheduled jobs might have on high-priority production jobs that are running in the same Data Lake Analytics account.</span></span>

<span data-ttu-id="6a79e-256">O Data Lake Analytics tem duas políticas que podem ser definidas no nível do trabalho:</span><span class="sxs-lookup"><span data-stu-id="6a79e-256">Data Lake Analytics has two policies that you can set at the job level:</span></span>

* <span data-ttu-id="6a79e-257">**Limite de AU por trabalho**: os usuários apenas podem enviar trabalhos que tenham até esse número de AUs.</span><span class="sxs-lookup"><span data-stu-id="6a79e-257">**AU limit per job**: Users can only submit jobs that have up to this number of AUs.</span></span> <span data-ttu-id="6a79e-258">Por padrão, esse limite é o mesmo que o limite máximo de AUs da conta.</span><span class="sxs-lookup"><span data-stu-id="6a79e-258">By default, this limit is the same as the maximum AU limit for the account.</span></span>
* <span data-ttu-id="6a79e-259">**Prioridade**: os usuários apenas podem enviar trabalhos com prioridade menor ou igual a esse valor.</span><span class="sxs-lookup"><span data-stu-id="6a79e-259">**Priority**: Users can only submit jobs that have a priority lower than or equal to this value.</span></span> <span data-ttu-id="6a79e-260">Observe que um número maior significa uma prioridade mais baixa.</span><span class="sxs-lookup"><span data-stu-id="6a79e-260">Note that a higher number means a lower priority.</span></span> <span data-ttu-id="6a79e-261">Por padrão, ela é definida como 1, que é a prioridade mais alta possível.</span><span class="sxs-lookup"><span data-stu-id="6a79e-261">By default, this is set to 1, which is the highest possible priority.</span></span>

<span data-ttu-id="6a79e-262">Há uma política padrão definida em cada conta.</span><span class="sxs-lookup"><span data-stu-id="6a79e-262">There is a default policy set on every account.</span></span> <span data-ttu-id="6a79e-263">A política padrão aplica-se a todos os usuários da conta.</span><span class="sxs-lookup"><span data-stu-id="6a79e-263">The default policy applies to all users of the account.</span></span> <span data-ttu-id="6a79e-264">Você pode definir políticas adicionais para usuários e grupos específicos.</span><span class="sxs-lookup"><span data-stu-id="6a79e-264">You can set additional policies for specific users and groups.</span></span> 

> [!NOTE]
> <span data-ttu-id="6a79e-265">As políticas no nível da conta e no nível do trabalho aplicam-se ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="6a79e-265">Account-level policies and job-level policies apply simultaneously.</span></span>
>

#### <a name="add-a-policy-for-a-specific-user-or-group"></a><span data-ttu-id="6a79e-266">Adicionar uma política para um usuário ou grupo específico</span><span class="sxs-lookup"><span data-stu-id="6a79e-266">Add a policy for a specific user or group</span></span>

1. <span data-ttu-id="6a79e-267">No portal do Azure, acesse sua conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="6a79e-267">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="6a79e-268">Clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="6a79e-268">Click **Properties**.</span></span>
3. <span data-ttu-id="6a79e-269">Em **Limites de Envio de Trabalho**, clique no botão **Adicionar Política**.</span><span class="sxs-lookup"><span data-stu-id="6a79e-269">Under **Job Submission Limits**, click the **Add Policy** button.</span></span> <span data-ttu-id="6a79e-270">Em seguida, selecione ou insira as seguintes configurações:</span><span class="sxs-lookup"><span data-stu-id="6a79e-270">Then, select or enter the following settings:</span></span>
    1. <span data-ttu-id="6a79e-271">**Nome da Política de Computação**: insira um nome de política para lembrá-lo da finalidade da política.</span><span class="sxs-lookup"><span data-stu-id="6a79e-271">**Compute Policy Name**: Enter a policy name, to remind you of the purpose of the policy.</span></span>
    2. <span data-ttu-id="6a79e-272">**Selecionar Usuário ou Grupo**: selecione o usuário ou o grupo ao qual essa política se aplica.</span><span class="sxs-lookup"><span data-stu-id="6a79e-272">**Select User or Group**: Select the user or group this policy applies to.</span></span>
    3. <span data-ttu-id="6a79e-273">**Definir o Limite de AUs de Trabalho**: defina o limite de AUs que se aplica ao usuário ou ao grupo selecionado.</span><span class="sxs-lookup"><span data-stu-id="6a79e-273">**Set the Job AU Limit**: Set the AU limit that applies to the selected user or group.</span></span>
    4. <span data-ttu-id="6a79e-274">**Definir o Limite de Prioridade**: defina o limite de prioridade que se aplica ao usuário ou ao grupo selecionado.</span><span class="sxs-lookup"><span data-stu-id="6a79e-274">**Set the Priority Limit**: Set the priority limit that applies to the selected user or group.</span></span>

4. <span data-ttu-id="6a79e-275">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="6a79e-275">Click **Ok**.</span></span>

5. <span data-ttu-id="6a79e-276">A nova política é listada na tabela de política **Padrão**, em **Limites de Envio de Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="6a79e-276">The new policy is listed in the **Default** policy table, under **Job Submission Limits**.</span></span> 

#### <a name="delete-or-edit-an-existing-policy"></a><span data-ttu-id="6a79e-277">Excluir ou editar uma política existente</span><span class="sxs-lookup"><span data-stu-id="6a79e-277">Delete or edit an existing policy</span></span>

1. <span data-ttu-id="6a79e-278">No portal do Azure, acesse sua conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="6a79e-278">In the Azure portal, go to your Data Lake Analytics account.</span></span>
2. <span data-ttu-id="6a79e-279">Clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="6a79e-279">Click **Properties**.</span></span>
3. <span data-ttu-id="6a79e-280">Em **Limites de Envio de Trabalho**, localize a política que deseja editar.</span><span class="sxs-lookup"><span data-stu-id="6a79e-280">Under **Job Submission Limits**, find the policy you want to edit.</span></span>
4.  <span data-ttu-id="6a79e-281">Para ver as opções **Excluir** e **Editar**, na coluna mais à direita da tabela, clique em **...**.</span><span class="sxs-lookup"><span data-stu-id="6a79e-281">To see the **Delete** and **Edit** options, in the rightmost column of the table, click **...**.</span></span>

### <a name="additional-resources-for-job-policies"></a><span data-ttu-id="6a79e-282">Recursos adicionais para políticas de trabalho</span><span class="sxs-lookup"><span data-stu-id="6a79e-282">Additional resources for job policies</span></span>
* [<span data-ttu-id="6a79e-283">Postagem no blog de visão geral de política</span><span class="sxs-lookup"><span data-stu-id="6a79e-283">Policy overview blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-overview/)
* [<span data-ttu-id="6a79e-284">Postagem no blog de políticas no nível da conta</span><span class="sxs-lookup"><span data-stu-id="6a79e-284">Account-level policies blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-account-level-policy/)
* [<span data-ttu-id="6a79e-285">Postagem no blog de políticas no nível do trabalho</span><span class="sxs-lookup"><span data-stu-id="6a79e-285">Job-level policies blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-job-level-policy/)

## <a name="next-steps"></a><span data-ttu-id="6a79e-286">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6a79e-286">Next steps</span></span>

* [<span data-ttu-id="6a79e-287">Visão geral do Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="6a79e-287">Overview of Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="6a79e-288">Introdução ao Data Lake Analytics usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6a79e-288">Get started with Data Lake Analytics by using the Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="6a79e-289">Gerenciar o Azure Data Lake Analytics usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6a79e-289">Manage Azure Data Lake Analytics by using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)

