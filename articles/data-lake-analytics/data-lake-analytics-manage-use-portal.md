---
title: "aaaManage análise Azure Data Lake usando Olá portal do Azure | Microsoft Docs"
description: "Saiba como toomanage análise Data Lake contas, dados de fontes, usuários e trabalhos."
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
ms.openlocfilehash: f63ccdfae79772c92e92462194e8cdc636a73dc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-by-using-hello-azure-portal"></a><span data-ttu-id="58f64-103">Gerenciar análise Azure Data Lake usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="58f64-103">Manage Azure Data Lake Analytics by using hello Azure portal</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="58f64-104">Saiba como contas de análise do Azure Data Lake toomanage, fontes de dados de conta, os usuários e trabalhos usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="58f64-104">Learn how toomanage Azure Data Lake Analytics accounts, account data sources, users, and jobs by using hello Azure portal.</span></span> <span data-ttu-id="58f64-105">tópicos de gerenciamento toosee sobre como usar outras ferramentas, clique na guia na parte superior de saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="58f64-105">toosee management topics about using other tools, click a tab at hello top of hello page.</span></span>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-lake-analytics-accounts"></a><span data-ttu-id="58f64-106">Gerenciar contas do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="58f64-106">Manage Data Lake Analytics accounts</span></span>

### <a name="create-an-account"></a><span data-ttu-id="58f64-107">Criar uma conta</span><span class="sxs-lookup"><span data-stu-id="58f64-107">Create an account</span></span>

1. <span data-ttu-id="58f64-108">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="58f64-108">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="58f64-109">Clique em **Novo** > **Intelligence + análise** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="58f64-109">Click **New** > **Intelligence + analytics** > **Data Lake Analytics**.</span></span>
3. <span data-ttu-id="58f64-110">Selecione os valores para Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="58f64-110">Select values for hello following items:</span></span> 
   1. <span data-ttu-id="58f64-111">**Nome**: nome de saudação do hello conta da análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="58f64-111">**Name**: hello name of hello Data Lake Analytics account.</span></span>
   2. <span data-ttu-id="58f64-112">**Assinatura**: Olá usada para a conta de saudação de assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="58f64-112">**Subscription**: hello Azure subscription used for hello account.</span></span>
   3. <span data-ttu-id="58f64-113">**Grupo de recursos**: grupo de recursos do Azure Olá qual conta de saudação toocreate.</span><span class="sxs-lookup"><span data-stu-id="58f64-113">**Resource Group**: hello Azure resource group in which toocreate hello account.</span></span> 
   4. <span data-ttu-id="58f64-114">**Local**: Olá datacenter do Azure para a conta de análise Data Lake hello.</span><span class="sxs-lookup"><span data-stu-id="58f64-114">**Location**: hello Azure datacenter for hello Data Lake Analytics account.</span></span> 
   5. <span data-ttu-id="58f64-115">**Repositório data Lake**: Olá toobe de armazenamento padrão usado para a conta de análise Data Lake hello.</span><span class="sxs-lookup"><span data-stu-id="58f64-115">**Data Lake Store**: hello default store toobe used for hello Data Lake Analytics account.</span></span> <span data-ttu-id="58f64-116">Olá a conta do repositório Azure Data Lake Hello e hello análise Data Lake conta deve estar no mesmo local.</span><span class="sxs-lookup"><span data-stu-id="58f64-116">hello Azure Data Lake Store account and hello Data Lake Analytics account must be in hello same location.</span></span>
4. <span data-ttu-id="58f64-117">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="58f64-117">Click **Create**.</span></span> 

### <a name="delete-a-data-lake-analytics-account"></a><span data-ttu-id="58f64-118">Excluir uma conta do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="58f64-118">Delete a Data Lake Analytics account</span></span>

<span data-ttu-id="58f64-119">Antes de excluir uma conta do Data Lake Analytics, exclua sua conta padrão do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="58f64-119">Before you delete a Data Lake Analytics account, delete its default Data Lake Store account.</span></span>

1. <span data-ttu-id="58f64-120">No hello portal do Azure, vá tooyour conta de análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="58f64-120">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="58f64-121">Clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="58f64-121">Click **Delete**.</span></span>
3. <span data-ttu-id="58f64-122">Nome de conta de saudação do tipo.</span><span class="sxs-lookup"><span data-stu-id="58f64-122">Type hello account name.</span></span>
4. <span data-ttu-id="58f64-123">Clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="58f64-123">Click **Delete**.</span></span>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-sources"></a><span data-ttu-id="58f64-124">Gerenciar as fontes de dados</span><span class="sxs-lookup"><span data-stu-id="58f64-124">Manage data sources</span></span>

<span data-ttu-id="58f64-125">Análise data Lake dá suporte a saudação fontes de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="58f64-125">Data Lake Analytics supports hello following data sources:</span></span>

* <span data-ttu-id="58f64-126">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="58f64-126">Data Lake Store</span></span>
* <span data-ttu-id="58f64-127">Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="58f64-127">Azure Storage</span></span>

<span data-ttu-id="58f64-128">Você pode usar fontes de dados do Gerenciador de dados toobrowse e executar operações de gerenciamento de arquivo básico.</span><span class="sxs-lookup"><span data-stu-id="58f64-128">You can use Data Explorer toobrowse data sources and perform basic file management operations.</span></span> 

### <a name="add-a-data-source"></a><span data-ttu-id="58f64-129">Adicionar uma fonte de dados</span><span class="sxs-lookup"><span data-stu-id="58f64-129">Add a data source</span></span>

1. <span data-ttu-id="58f64-130">No hello portal do Azure, vá tooyour conta de análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="58f64-130">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="58f64-131">Clique em **Fontes de Dados**.</span><span class="sxs-lookup"><span data-stu-id="58f64-131">Click **Data Sources**.</span></span>
3. <span data-ttu-id="58f64-132">Clique em **Adicionar Fonte de Dados**.</span><span class="sxs-lookup"><span data-stu-id="58f64-132">Click **Add Data Source**.</span></span>
    
   * <span data-ttu-id="58f64-133">tooadd uma conta do repositório Data Lake, você precisa de conta de saudação toohello acesso e do nome de conta tooquery capaz de toobe-lo.</span><span class="sxs-lookup"><span data-stu-id="58f64-133">tooadd a Data Lake Store account, you need hello account name and access toohello account toobe able tooquery it.</span></span>
   * <span data-ttu-id="58f64-134">tooadd armazenamento de BLOBs do Azure, você precisa conta de armazenamento hello e chave de conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="58f64-134">tooadd Azure Blob storage, you need hello storage account and hello account key.</span></span> <span data-ttu-id="58f64-135">toofind toohello-los, vá a conta de armazenamento no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="58f64-135">toofind them, go toohello storage account in hello portal.</span></span>

## <a name="set-up-firewall-rules"></a><span data-ttu-id="58f64-136">Configurar regras de firewall</span><span class="sxs-lookup"><span data-stu-id="58f64-136">Set up firewall rules</span></span>

<span data-ttu-id="58f64-137">Você pode usar análise Data Lake toofurther bloquear acesso tooyour conta da análise Data Lake no nível de rede hello.</span><span class="sxs-lookup"><span data-stu-id="58f64-137">You can use Data Lake Analytics toofurther lock down access tooyour Data Lake Analytics account at hello network level.</span></span> <span data-ttu-id="58f64-138">Você pode habilitar um firewall e definir um endereço IP ou um intervalo de endereços IP para seus clientes confiáveis.</span><span class="sxs-lookup"><span data-stu-id="58f64-138">You can enable a firewall, specify an IP address, or define an IP address range for your trusted clients.</span></span> <span data-ttu-id="58f64-139">Depois de habilitar essas medidas, somente os clientes que têm endereços IP hello dentro do intervalo de saudação definido podem se conectar toohello repositório.</span><span class="sxs-lookup"><span data-stu-id="58f64-139">After you enable these measures, only clients that have hello IP addresses within hello defined range can connect toohello store.</span></span>

<span data-ttu-id="58f64-140">Se outros serviços do Azure, como Azure Data Factory ou VMs, conecte-se a conta de análise Data Lake toohello, verifique se **permitem que os serviços do Azure** está ativada **em**.</span><span class="sxs-lookup"><span data-stu-id="58f64-140">If other Azure services, like Azure Data Factory or VMs, connect toohello Data Lake Analytics account, make sure that **Allow Azure Services** is turned **On**.</span></span> 

### <a name="set-up-a-firewall-rule"></a><span data-ttu-id="58f64-141">Configurar uma regra de firewall</span><span class="sxs-lookup"><span data-stu-id="58f64-141">Set up a firewall rule</span></span>

1. <span data-ttu-id="58f64-142">No hello portal do Azure, vá tooyour conta de análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="58f64-142">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="58f64-143">No menu Olá Olá esquerda, clique em **Firewall**.</span><span class="sxs-lookup"><span data-stu-id="58f64-143">On hello menu on hello left, click **Firewall**.</span></span>

## <a name="add-a-new-user"></a><span data-ttu-id="58f64-144">Adicione um novo usuário</span><span class="sxs-lookup"><span data-stu-id="58f64-144">Add a new user</span></span>

<span data-ttu-id="58f64-145">Você pode usar o hello **Assistente para adicionar usuário** tooeasily provisionar novos usuários Data Lake.</span><span class="sxs-lookup"><span data-stu-id="58f64-145">You can use hello **Add User Wizard** tooeasily provision new Data Lake users.</span></span>

1. <span data-ttu-id="58f64-146">No hello portal do Azure, vá tooyour conta de análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="58f64-146">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="58f64-147">Em saudação à esquerda, em **Introdução**, clique em **Assistente para adicionar usuário**.</span><span class="sxs-lookup"><span data-stu-id="58f64-147">On hello left, under **Getting Started**, click **Add User Wizard**.</span></span>
3. <span data-ttu-id="58f64-148">Selecione um usuário e, em seguida, clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="58f64-148">Select a user, and then click **Select**.</span></span>
4. <span data-ttu-id="58f64-149">Selecione uma função e, em seguida, clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="58f64-149">Select a role, and then click **Select**.</span></span> <span data-ttu-id="58f64-150">tooset backup de um novo toouse de desenvolvedor do Azure Data Lake, selecione Olá **Data Lake análise desenvolvedor** função.</span><span class="sxs-lookup"><span data-stu-id="58f64-150">tooset up a new developer toouse Azure Data Lake, select hello **Data Lake Analytics Developer** role.</span></span>
5. <span data-ttu-id="58f64-151">Selecione as listas de controle de acesso hello (ACLs) para bancos de dados Olá U-SQL.</span><span class="sxs-lookup"><span data-stu-id="58f64-151">Select hello access control lists (ACLs) for hello U-SQL databases.</span></span> <span data-ttu-id="58f64-152">Quando estiver satisfeito com suas escolhas, clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="58f64-152">When you're satisfied with your choices, click **Select**.</span></span>
6. <span data-ttu-id="58f64-153">Selecione Olá ACLs para arquivos.</span><span class="sxs-lookup"><span data-stu-id="58f64-153">Select hello ACLs for files.</span></span> <span data-ttu-id="58f64-154">Para armazenamento de saudação padrão, não altere Olá ACLs para a pasta raiz de hello "/" e para a pasta de /system hello.</span><span class="sxs-lookup"><span data-stu-id="58f64-154">For hello default store, don't change hello ACLs for hello root folder "/" and for hello /system folder.</span></span> <span data-ttu-id="58f64-155">Clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="58f64-155">Click **Select**.</span></span>
7. <span data-ttu-id="58f64-156">Examine todas as alterações selecionadas e, em seguida, clique em **Executar**.</span><span class="sxs-lookup"><span data-stu-id="58f64-156">Review all your selected changes, and then click **Run**.</span></span>
8. <span data-ttu-id="58f64-157">Quando o Assistente de saudação for concluído, clique em **feito**.</span><span class="sxs-lookup"><span data-stu-id="58f64-157">When hello wizard is finished, click **Done**.</span></span>

## <a name="manage-role-based-access-control"></a><span data-ttu-id="58f64-158">Gerenciar o controle de acesso baseado em função</span><span class="sxs-lookup"><span data-stu-id="58f64-158">Manage Role-Based Access Control</span></span>

<span data-ttu-id="58f64-159">Como outros serviços do Azure, você pode usar toocontrol de controle de acesso baseado em função (RBAC) como os usuários interagem com o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="58f64-159">Like other Azure services, you can use Role-Based Access Control (RBAC) toocontrol how users interact with hello service.</span></span>

<span data-ttu-id="58f64-160">funções RBAC padrão Olá têm Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="58f64-160">hello standard RBAC roles have hello following capabilities:</span></span>
* <span data-ttu-id="58f64-161">**Proprietário**: pode enviar trabalhos, monitorar trabalhos, cancelar trabalhos de qualquer usuário e configurar a conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="58f64-161">**Owner**: Can submit jobs, monitor jobs, cancel jobs from any user, and configure hello account.</span></span>
* <span data-ttu-id="58f64-162">**Colaborador**: pode enviar trabalhos, monitorar trabalhos, cancelar trabalhos de qualquer usuário e configurar a conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="58f64-162">**Contributor**: Can submit jobs, monitor jobs, cancel jobs from any user, and configure hello account.</span></span>
* <span data-ttu-id="58f64-163">**Leitor**: pode monitorar trabalhos.</span><span class="sxs-lookup"><span data-stu-id="58f64-163">**Reader**: Can monitor jobs.</span></span>

<span data-ttu-id="58f64-164">Use Olá desenvolvedor de análise do Data Lake tooenable U-SQL desenvolvedores toouse Olá análise Data Lake serviço de função.</span><span class="sxs-lookup"><span data-stu-id="58f64-164">Use hello Data Lake Analytics Developer role tooenable U-SQL developers toouse hello Data Lake Analytics service.</span></span> <span data-ttu-id="58f64-165">Você pode usar a função de desenvolvedor de análise do Data Lake Olá para:</span><span class="sxs-lookup"><span data-stu-id="58f64-165">You can use hello Data Lake Analytics Developer role to:</span></span>
* <span data-ttu-id="58f64-166">Enviar trabalhos.</span><span class="sxs-lookup"><span data-stu-id="58f64-166">Submit jobs.</span></span>
* <span data-ttu-id="58f64-167">Monitorar o progresso de status e hello de trabalho dos trabalhos enviados por qualquer usuário.</span><span class="sxs-lookup"><span data-stu-id="58f64-167">Monitor job status and hello progress of jobs submitted by any user.</span></span>
* <span data-ttu-id="58f64-168">Consulte Olá U-SQL scripts de trabalhos enviados por qualquer usuário.</span><span class="sxs-lookup"><span data-stu-id="58f64-168">See hello U-SQL scripts from jobs submitted by any user.</span></span>
* <span data-ttu-id="58f64-169">Cancelar apenas seus próprios trabalhos.</span><span class="sxs-lookup"><span data-stu-id="58f64-169">Cancel only your own jobs.</span></span>

### <a name="add-users-or-security-groups-tooa-data-lake-analytics-account"></a><span data-ttu-id="58f64-170">Adicionar usuários ou grupos de segurança tooa conta da análise Data Lake</span><span class="sxs-lookup"><span data-stu-id="58f64-170">Add users or security groups tooa Data Lake Analytics account</span></span>

1. <span data-ttu-id="58f64-171">No hello portal do Azure, vá tooyour conta de análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="58f64-171">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="58f64-172">Clique em **Controle de acesso (IAM)** > **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="58f64-172">Click **Access control (IAM)** > **Add**.</span></span>
3. <span data-ttu-id="58f64-173">Selecione uma função.</span><span class="sxs-lookup"><span data-stu-id="58f64-173">Select a role.</span></span>
4. <span data-ttu-id="58f64-174">Adicione um usuário.</span><span class="sxs-lookup"><span data-stu-id="58f64-174">Add a user.</span></span>
5. <span data-ttu-id="58f64-175">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="58f64-175">Click **OK**.</span></span>

>[!NOTE]
><span data-ttu-id="58f64-176">Se um usuário ou um grupo de segurança precisa toosubmit trabalhos, eles também precisam de permissão na conta do repositório de saudação.</span><span class="sxs-lookup"><span data-stu-id="58f64-176">If a user or a security group needs toosubmit jobs, they also need permission on hello store account.</span></span> <span data-ttu-id="58f64-177">Para obter mais informações, consulte [Proteger os dados armazenados no Data Lake Store](../data-lake-store/data-lake-store-secure-data.md).</span><span class="sxs-lookup"><span data-stu-id="58f64-177">For more information, see [Secure data stored in Data Lake Store](../data-lake-store/data-lake-store-secure-data.md).</span></span>
>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-jobs"></a><span data-ttu-id="58f64-178">Gerenciar trabalhos</span><span class="sxs-lookup"><span data-stu-id="58f64-178">Manage jobs</span></span>

### <a name="submit-a-job"></a><span data-ttu-id="58f64-179">Enviar um trabalho</span><span class="sxs-lookup"><span data-stu-id="58f64-179">Submit a job</span></span>

1. <span data-ttu-id="58f64-180">No hello portal do Azure, vá tooyour conta de análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="58f64-180">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>

2. <span data-ttu-id="58f64-181">Clique em **Novo Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="58f64-181">Click **New Job**.</span></span> <span data-ttu-id="58f64-182">Para cada trabalho, configure:</span><span class="sxs-lookup"><span data-stu-id="58f64-182">For each job,  configure:</span></span>

    1. <span data-ttu-id="58f64-183">**Nome do trabalho**: nome de saudação do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="58f64-183">**Job Name**: hello name of hello job.</span></span>
    2. <span data-ttu-id="58f64-184">**Prioridade**: números menores têm prioridade mais alta.</span><span class="sxs-lookup"><span data-stu-id="58f64-184">**Priority**: Lower numbers have higher priority.</span></span> <span data-ttu-id="58f64-185">Se dois trabalhos são enfileirados, Olá com valor de prioridade inferior é executado primeiro.</span><span class="sxs-lookup"><span data-stu-id="58f64-185">If two jobs are queued, hello one with lower priority value runs first.</span></span>
    3. <span data-ttu-id="58f64-186">**Paralelismo**: número máximo de saudação de computação processa tooreserve para este trabalho.</span><span class="sxs-lookup"><span data-stu-id="58f64-186">**Parallelism**: hello maximum number of compute processes tooreserve for this job.</span></span>

3. <span data-ttu-id="58f64-187">Clique em **Enviar Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="58f64-187">Click **Submit Job**.</span></span>

### <a name="monitor-jobs"></a><span data-ttu-id="58f64-188">Monitorar trabalhos</span><span class="sxs-lookup"><span data-stu-id="58f64-188">Monitor jobs</span></span>

1. <span data-ttu-id="58f64-189">No hello portal do Azure, vá tooyour conta de análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="58f64-189">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="58f64-190">Clique em **Exibir Todos os Trabalhos**.</span><span class="sxs-lookup"><span data-stu-id="58f64-190">Click **View All Jobs**.</span></span> <span data-ttu-id="58f64-191">É mostrada uma lista de todos os trabalhos de ativo e concluído recentemente de saudação na conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="58f64-191">A list of all hello active and recently finished jobs in hello account is shown.</span></span>
3. <span data-ttu-id="58f64-192">Opcionalmente, clique em **filtro** toohelp localizar trabalhos Olá por **intervalo de tempo**, **nome do trabalho**, e **autor** valores.</span><span class="sxs-lookup"><span data-stu-id="58f64-192">Optionally, click **Filter** toohelp you find hello jobs by **Time Range**, **Job Name**, and **Author** values.</span></span> 

### <a name="monitoring-pipeline-jobs"></a><span data-ttu-id="58f64-193">Monitorando trabalhos de pipeline</span><span class="sxs-lookup"><span data-stu-id="58f64-193">Monitoring pipeline jobs</span></span>
<span data-ttu-id="58f64-194">Trabalhos que fazem parte de um pipeline funcionam juntos, geralmente em sequência, tooaccomplish um cenário específico.</span><span class="sxs-lookup"><span data-stu-id="58f64-194">Jobs that are part of a pipeline work together, usually sequentially, tooaccomplish a specific scenario.</span></span> <span data-ttu-id="58f64-195">Por exemplo, você pode ter um pipeline que limpa, extrai, transforma, agrega o uso de Customer Insights.</span><span class="sxs-lookup"><span data-stu-id="58f64-195">For example, you can have a pipeline that cleans, extracts, transforms, aggregates usage for customer insights.</span></span> <span data-ttu-id="58f64-196">Trabalhos do pipeline são identificados usando a propriedade de "Pipeline" hello quando Olá trabalho foi enviado.</span><span class="sxs-lookup"><span data-stu-id="58f64-196">Pipeline jobs are identified using hello "Pipeline" property when hello job was submitted.</span></span> <span data-ttu-id="58f64-197">Trabalhos agendados usando o ADF V2 terão, automaticamente, essa propriedade populada.</span><span class="sxs-lookup"><span data-stu-id="58f64-197">Jobs scheduled using ADF V2 will automatically have this property populated.</span></span> 

<span data-ttu-id="58f64-198">tooview uma lista de trabalhos de U-SQL que fazem parte de pipelines:</span><span class="sxs-lookup"><span data-stu-id="58f64-198">tooview a list of U-SQL jobs that are part of pipelines:</span></span> 

1. <span data-ttu-id="58f64-199">No hello portal do Azure, vá tooyour contas de análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="58f64-199">In hello Azure portal, go tooyour Data Lake Analytics accounts.</span></span>
2. <span data-ttu-id="58f64-200">Clique em **Insights de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="58f64-200">Click **Job Insights**.</span></span> <span data-ttu-id="58f64-201">Olá que guia de "Todos os trabalhos" padrão, mostrando uma lista de execução, na fila e foi encerrado trabalhos.</span><span class="sxs-lookup"><span data-stu-id="58f64-201">hello "All Jobs" tab will be defaulted, showing a list of running, queued, and ended jobs.</span></span>
3. <span data-ttu-id="58f64-202">Clique em Olá **Pipeline trabalhos** guia. Uma lista de trabalhos do pipeline será mostrada juntamente com estatísticas agregadas para cada pipeline.</span><span class="sxs-lookup"><span data-stu-id="58f64-202">Click hello **Pipeline Jobs** tab. A list of pipeline jobs will be shown along with aggregated statistics for each pipeline.</span></span>

### <a name="monitoring-recurring-jobs"></a><span data-ttu-id="58f64-203">Monitorando trabalhos recorrentes</span><span class="sxs-lookup"><span data-stu-id="58f64-203">Monitoring recurring jobs</span></span>
<span data-ttu-id="58f64-204">Um trabalho recorrente é aquele que tem Olá mesma lógica de negócios mas usa dados de entrada diferentes toda vez que ele é executado.</span><span class="sxs-lookup"><span data-stu-id="58f64-204">A recurring job is one that has hello same business logic but uses different input data every time it runs.</span></span> <span data-ttu-id="58f64-205">Idealmente, trabalhos recorrentes devem sempre ter êxito e têm relativamente estável de tempo de execução; monitoramento desses comportamentos ajuda a garantir o trabalho hello está íntegro.</span><span class="sxs-lookup"><span data-stu-id="58f64-205">Ideally, recurring jobs should always succeed, and have relatively stable execution time; monitoring these behaviors will help ensure hello job is healthy.</span></span> <span data-ttu-id="58f64-206">Trabalhos recorrentes são identificados usando a propriedade de "Recurrence" hello.</span><span class="sxs-lookup"><span data-stu-id="58f64-206">Recurring jobs are identified using hello "Recurrence" property.</span></span> <span data-ttu-id="58f64-207">Trabalhos agendados usando o ADF V2 terão, automaticamente, essa propriedade populada.</span><span class="sxs-lookup"><span data-stu-id="58f64-207">Jobs scheduled using ADF V2 will automatically have this property populated.</span></span>

<span data-ttu-id="58f64-208">tooview uma lista de trabalhos de U-SQL que são recorrentes:</span><span class="sxs-lookup"><span data-stu-id="58f64-208">tooview a list of U-SQL jobs that are recurring:</span></span> 

1. <span data-ttu-id="58f64-209">No hello portal do Azure, vá tooyour contas de análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="58f64-209">In hello Azure portal, go tooyour Data Lake Analytics accounts.</span></span>
2. <span data-ttu-id="58f64-210">Clique em **Insights de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="58f64-210">Click **Job Insights**.</span></span> <span data-ttu-id="58f64-211">Olá que guia de "Todos os trabalhos" padrão, mostrando uma lista de execução, na fila e foi encerrado trabalhos.</span><span class="sxs-lookup"><span data-stu-id="58f64-211">hello "All Jobs" tab will be defaulted, showing a list of running, queued, and ended jobs.</span></span>
3. <span data-ttu-id="58f64-212">Clique em Olá **trabalhos recorrentes** guia. Uma lista de trabalhos recorrentes será mostrada juntamente com estatísticas agregadas para cada trabalho recorrente.</span><span class="sxs-lookup"><span data-stu-id="58f64-212">Click hello **Recurring Jobs** tab. A list of recurring jobs will be shown along with aggregated statistics for each recurring job.</span></span>

## <a name="manage-policies"></a><span data-ttu-id="58f64-213">Gerenciar políticas</span><span class="sxs-lookup"><span data-stu-id="58f64-213">Manage policies</span></span>

### <a name="account-level-policies"></a><span data-ttu-id="58f64-214">Políticas no nível da conta</span><span class="sxs-lookup"><span data-stu-id="58f64-214">Account-level policies</span></span>

<span data-ttu-id="58f64-215">Essas políticas se aplicam a tooall trabalhos em uma conta da análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="58f64-215">These policies apply tooall jobs in a Data Lake Analytics account.</span></span>

#### <a name="maximum-number-of-aus-in-a-data-lake-analytics-account"></a><span data-ttu-id="58f64-216">Número máximo de AUs em uma conta do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="58f64-216">Maximum number of AUs in a Data Lake Analytics account</span></span>
<span data-ttu-id="58f64-217">Uma política controla o número total de saudação de unidades de análise (Austrália) pode usar sua conta da análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="58f64-217">A policy controls hello total number of Analytics Units (AUs) your Data Lake Analytics account can use.</span></span> <span data-ttu-id="58f64-218">Por padrão, o valor de saudação é definido too250.</span><span class="sxs-lookup"><span data-stu-id="58f64-218">By default, hello value is set too250.</span></span> <span data-ttu-id="58f64-219">Por exemplo, se esse valor é definido too250 Austrália, você pode ter um trabalho em execução com 250 tooit de AUs atribuídos ou 10 trabalhos em execução com 25 Austrália cada.</span><span class="sxs-lookup"><span data-stu-id="58f64-219">For example, if this value is set too250 AUs, you can have one job running with 250 AUs assigned tooit, or 10 jobs running with 25 AUs each.</span></span> <span data-ttu-id="58f64-220">Trabalhos adicionais que são enviados são enfileirados até que trabalhos em execução Olá tenham terminados.</span><span class="sxs-lookup"><span data-stu-id="58f64-220">Additional jobs that are submitted are queued until hello running jobs are finished.</span></span> <span data-ttu-id="58f64-221">Quando terminarem de trabalhos em execução, Austrália é liberadas para Olá na fila de trabalhos toorun.</span><span class="sxs-lookup"><span data-stu-id="58f64-221">When running jobs are finished, AUs are freed up for hello queued jobs toorun.</span></span>

<span data-ttu-id="58f64-222">número de saudação toochange de AUs para sua conta da análise Data Lake:</span><span class="sxs-lookup"><span data-stu-id="58f64-222">toochange hello number of AUs for your Data Lake Analytics account:</span></span>

1. <span data-ttu-id="58f64-223">No hello portal do Azure, vá tooyour conta de análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="58f64-223">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="58f64-224">Clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="58f64-224">Click **Properties**.</span></span>
3. <span data-ttu-id="58f64-225">Em **Austrália máximo**, mover o controle deslizante de saudação tooselect um valor ou insira o valor de saudação na caixa de texto de saudação.</span><span class="sxs-lookup"><span data-stu-id="58f64-225">Under **Maximum AUs**, move hello slider tooselect a value, or enter hello value in hello text box.</span></span> 
4. <span data-ttu-id="58f64-226">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="58f64-226">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="58f64-227">Se você precisa de mais do que Olá padrão (250) Austrália, no portal de saudação, clique em **ajuda + suporte** toosubmit uma solicitação de suporte.</span><span class="sxs-lookup"><span data-stu-id="58f64-227">If you need more than hello default (250) AUs, in hello portal, click **Help+Support** toosubmit a support request.</span></span> <span data-ttu-id="58f64-228">número de saudação de AUs disponíveis em sua conta da análise Data Lake pode ser aumentado.</span><span class="sxs-lookup"><span data-stu-id="58f64-228">hello number of AUs available in your Data Lake Analytics account can be increased.</span></span>
>

#### <a name="maximum-number-of-jobs-that-can-run-simultaneously"></a><span data-ttu-id="58f64-229">Número máximo de trabalhos que podem ser executados simultaneamente</span><span class="sxs-lookup"><span data-stu-id="58f64-229">Maximum number of jobs that can run simultaneously</span></span>
<span data-ttu-id="58f64-230">Uma política que controla quantos trabalhos podem ser executados em Olá simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="58f64-230">A policy controls how many jobs can run at hello same time.</span></span> <span data-ttu-id="58f64-231">Por padrão, esse valor é definido too20.</span><span class="sxs-lookup"><span data-stu-id="58f64-231">By default, this value is set too20.</span></span> <span data-ttu-id="58f64-232">Se sua análise Data Lake Austrália disponíveis novos trabalhos são agendado toorun imediatamente até que número total de saudação de trabalhos em execução atinja o valor de saudação dessa política.</span><span class="sxs-lookup"><span data-stu-id="58f64-232">If your Data Lake Analytics has AUs available, new jobs are scheduled toorun immediately until hello total number of running jobs reaches hello value of this policy.</span></span> <span data-ttu-id="58f64-233">Quando você atingir o número máximo de saudação de trabalhos que podem ser executadas simultaneamente, os trabalhos subsequentes são enfileirados em ordem de prioridade até que conclua a um ou mais trabalhos em execução (dependendo da disponibilidade Austrália).</span><span class="sxs-lookup"><span data-stu-id="58f64-233">When you reach hello maximum number of jobs that can run simultaneously, subsequent jobs are queued in priority order until one or more running jobs complete (depending on AU availability).</span></span>

<span data-ttu-id="58f64-234">número de saudação toochange de trabalhos que podem ser executadas simultaneamente:</span><span class="sxs-lookup"><span data-stu-id="58f64-234">toochange hello number of jobs that can run simultaneously:</span></span>

1. <span data-ttu-id="58f64-235">No hello portal do Azure, vá tooyour conta de análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="58f64-235">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="58f64-236">Clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="58f64-236">Click **Properties**.</span></span>
3. <span data-ttu-id="58f64-237">Em **máximo número de executando trabalhos**, mover o controle deslizante de saudação tooselect um valor ou insira o valor de saudação na caixa de texto de saudação.</span><span class="sxs-lookup"><span data-stu-id="58f64-237">Under **Maximum Number of Running Jobs**, move hello slider tooselect a value, or enter hello value in hello text box.</span></span> 
4. <span data-ttu-id="58f64-238">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="58f64-238">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="58f64-239">Se você precisar toorun mais de hello (20) o número de trabalhos, no portal de saudação padrão clique **ajuda + suporte** toosubmit uma solicitação de suporte.</span><span class="sxs-lookup"><span data-stu-id="58f64-239">If you need toorun more than hello default (20) number of jobs, in hello portal, click **Help+Support** toosubmit a support request.</span></span> <span data-ttu-id="58f64-240">número de saudação de trabalhos que podem ser executadas simultaneamente em sua conta da análise Data Lake pode ser aumentado.</span><span class="sxs-lookup"><span data-stu-id="58f64-240">hello number of jobs that can run simultaneously in your Data Lake Analytics account can be increased.</span></span>
>

#### <a name="how-long-tookeep-job-metadata-and-resources"></a><span data-ttu-id="58f64-241">Quanto tempo tookeep metadados de trabalho e recursos</span><span class="sxs-lookup"><span data-stu-id="58f64-241">How long tookeep job metadata and resources</span></span> 
<span data-ttu-id="58f64-242">Quando os usuários executam trabalhos de U-SQL, Olá serviço de análise Data Lake retém todos os arquivos relacionados.</span><span class="sxs-lookup"><span data-stu-id="58f64-242">When your users run U-SQL jobs, hello Data Lake Analytics service retains all related files.</span></span> <span data-ttu-id="58f64-243">Arquivos relacionados incluem script hello U-SQL, arquivos DLL Olá referenciados no script hello U-SQL, recursos compilados e estatísticas.</span><span class="sxs-lookup"><span data-stu-id="58f64-243">Related files include hello U-SQL script, hello DLL files referenced in hello U-SQL script, compiled resources, and statistics.</span></span> <span data-ttu-id="58f64-244">arquivos de saudação estão na pasta de /system/ de saudação da conta de armazenamento do Azure Data Lake saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="58f64-244">hello files are in hello /system/ folder of hello default Azure Data Lake Storage account.</span></span> <span data-ttu-id="58f64-245">Esta política controla por quanto tempo esses recursos são armazenados antes de serem excluídos automaticamente (o padrão de saudação é de 30 dias).</span><span class="sxs-lookup"><span data-stu-id="58f64-245">This policy controls how long these resources are stored before they are automatically deleted (hello default is 30 days).</span></span> <span data-ttu-id="58f64-246">Você pode usar esses arquivos para depuração e ajuste de desempenho de trabalhos que você vai executar novamente no futuro de saudação.</span><span class="sxs-lookup"><span data-stu-id="58f64-246">You can use these files for debugging, and for performance-tuning of jobs that you'll rerun in hello future.</span></span>

<span data-ttu-id="58f64-247">toochange quanto tookeep metadados de trabalho e recursos:</span><span class="sxs-lookup"><span data-stu-id="58f64-247">toochange how long tookeep job metadata and resources:</span></span>

1. <span data-ttu-id="58f64-248">No hello portal do Azure, vá tooyour conta de análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="58f64-248">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="58f64-249">Clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="58f64-249">Click **Properties**.</span></span>
3. <span data-ttu-id="58f64-250">Em **tooRetain dias consultas de trabalho**, mover o controle deslizante de saudação tooselect um valor ou insira o valor de saudação na caixa de texto de saudação.</span><span class="sxs-lookup"><span data-stu-id="58f64-250">Under **Days tooRetain Job Queries**, move hello slider tooselect a value, or enter hello value in hello text box.</span></span>  
4. <span data-ttu-id="58f64-251">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="58f64-251">Click **Save**.</span></span>

### <a name="job-level-policies"></a><span data-ttu-id="58f64-252">Políticas no nível do trabalho</span><span class="sxs-lookup"><span data-stu-id="58f64-252">Job-level policies</span></span>
<span data-ttu-id="58f64-253">Com as políticas de nível de trabalho, você pode controlar Olá máximo Austrália e Olá prioridade máxima que podem ser definida por usuários individuais (ou membros de grupos de segurança específicos) em trabalhos que são enviados.</span><span class="sxs-lookup"><span data-stu-id="58f64-253">With job-level policies, you can control hello maximum AUs and hello maximum priority that individual users (or members of specific security groups) can set on jobs that they submit.</span></span> <span data-ttu-id="58f64-254">Esse permite controlar Olá custos de usuários.</span><span class="sxs-lookup"><span data-stu-id="58f64-254">This lets you control hello costs incurred by users.</span></span> <span data-ttu-id="58f64-255">Ele também permite que você pode ter efeito de saudação do controle que os trabalhos agendados em alta prioridade trabalhos de produção que são executados em Olá a mesma conta da análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="58f64-255">It also lets you control hello effect that scheduled jobs might have on high-priority production jobs that are running in hello same Data Lake Analytics account.</span></span>

<span data-ttu-id="58f64-256">Análise data Lake tem duas políticas que podem ser definidas no nível de trabalho hello:</span><span class="sxs-lookup"><span data-stu-id="58f64-256">Data Lake Analytics has two policies that you can set at hello job level:</span></span>

* <span data-ttu-id="58f64-257">**Limite de Austrália por trabalho**: os usuários podem enviar apenas trabalhos com número de toothis de Austrália.</span><span class="sxs-lookup"><span data-stu-id="58f64-257">**AU limit per job**: Users can only submit jobs that have up toothis number of AUs.</span></span> <span data-ttu-id="58f64-258">Por padrão, esse limite é Olá mesmo que o limite máximo de Austrália Olá para conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="58f64-258">By default, this limit is hello same as hello maximum AU limit for hello account.</span></span>
* <span data-ttu-id="58f64-259">**Prioridade**: os usuários somente podem enviar trabalhos que têm um valor de prioridade toothis menores ou iguais.</span><span class="sxs-lookup"><span data-stu-id="58f64-259">**Priority**: Users can only submit jobs that have a priority lower than or equal toothis value.</span></span> <span data-ttu-id="58f64-260">Observe que um número maior significa uma prioridade mais baixa.</span><span class="sxs-lookup"><span data-stu-id="58f64-260">Note that a higher number means a lower priority.</span></span> <span data-ttu-id="58f64-261">Por padrão, isso é definido too1, que é a prioridade possível hello.</span><span class="sxs-lookup"><span data-stu-id="58f64-261">By default, this is set too1, which is hello highest possible priority.</span></span>

<span data-ttu-id="58f64-262">Há uma política padrão definida em cada conta.</span><span class="sxs-lookup"><span data-stu-id="58f64-262">There is a default policy set on every account.</span></span> <span data-ttu-id="58f64-263">política padrão de saudação aplica tooall usuários da conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="58f64-263">hello default policy applies tooall users of hello account.</span></span> <span data-ttu-id="58f64-264">Você pode definir políticas adicionais para usuários e grupos específicos.</span><span class="sxs-lookup"><span data-stu-id="58f64-264">You can set additional policies for specific users and groups.</span></span> 

> [!NOTE]
> <span data-ttu-id="58f64-265">As políticas no nível da conta e no nível do trabalho aplicam-se ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="58f64-265">Account-level policies and job-level policies apply simultaneously.</span></span>
>

#### <a name="add-a-policy-for-a-specific-user-or-group"></a><span data-ttu-id="58f64-266">Adicionar uma política para um usuário ou grupo específico</span><span class="sxs-lookup"><span data-stu-id="58f64-266">Add a policy for a specific user or group</span></span>

1. <span data-ttu-id="58f64-267">No hello portal do Azure, vá tooyour conta de análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="58f64-267">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="58f64-268">Clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="58f64-268">Click **Properties**.</span></span>
3. <span data-ttu-id="58f64-269">Em **limites de envio de trabalho**, clique em Olá **adicionar política** botão.</span><span class="sxs-lookup"><span data-stu-id="58f64-269">Under **Job Submission Limits**, click hello **Add Policy** button.</span></span> <span data-ttu-id="58f64-270">Em seguida, selecione ou insira Olá configurações a seguir:</span><span class="sxs-lookup"><span data-stu-id="58f64-270">Then, select or enter hello following settings:</span></span>
    1. <span data-ttu-id="58f64-271">**Nome da política de computação**: insira um nome de política, tooremind você finalidade de saudação da política de saudação.</span><span class="sxs-lookup"><span data-stu-id="58f64-271">**Compute Policy Name**: Enter a policy name, tooremind you of hello purpose of hello policy.</span></span>
    2. <span data-ttu-id="58f64-272">**Selecione o usuário ou grupo**: Selecionar usuário hello ou grupo essa política se aplica.</span><span class="sxs-lookup"><span data-stu-id="58f64-272">**Select User or Group**: Select hello user or group this policy applies to.</span></span>
    3. <span data-ttu-id="58f64-273">**Definir Olá trabalho Austrália limite**: limite de saudação Austrália definido que se aplica a toohello selecionado usuário ou grupo.</span><span class="sxs-lookup"><span data-stu-id="58f64-273">**Set hello Job AU Limit**: Set hello AU limit that applies toohello selected user or group.</span></span>
    4. <span data-ttu-id="58f64-274">**Definir Olá prioridade limite**: Definir limite de prioridade de saudação que se aplica a toohello selecionado usuário ou grupo.</span><span class="sxs-lookup"><span data-stu-id="58f64-274">**Set hello Priority Limit**: Set hello priority limit that applies toohello selected user or group.</span></span>

4. <span data-ttu-id="58f64-275">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="58f64-275">Click **Ok**.</span></span>

5. <span data-ttu-id="58f64-276">Olá nova diretiva é listada no hello **padrão** política de tabela, em **limites de envio de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="58f64-276">hello new policy is listed in hello **Default** policy table, under **Job Submission Limits**.</span></span> 

#### <a name="delete-or-edit-an-existing-policy"></a><span data-ttu-id="58f64-277">Excluir ou editar uma política existente</span><span class="sxs-lookup"><span data-stu-id="58f64-277">Delete or edit an existing policy</span></span>

1. <span data-ttu-id="58f64-278">No hello portal do Azure, vá tooyour conta de análise Data Lake.</span><span class="sxs-lookup"><span data-stu-id="58f64-278">In hello Azure portal, go tooyour Data Lake Analytics account.</span></span>
2. <span data-ttu-id="58f64-279">Clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="58f64-279">Click **Properties**.</span></span>
3. <span data-ttu-id="58f64-280">Em **limites de envio de trabalho**, localizar Olá política deseja tooedit.</span><span class="sxs-lookup"><span data-stu-id="58f64-280">Under **Job Submission Limits**, find hello policy you want tooedit.</span></span>
4.  <span data-ttu-id="58f64-281">Olá toosee **excluir** e **editar** opções, na coluna mais à direita de saudação da tabela de saudação, clique em **...** .</span><span class="sxs-lookup"><span data-stu-id="58f64-281">toosee hello **Delete** and **Edit** options, in hello rightmost column of hello table, click **...**.</span></span>

### <a name="additional-resources-for-job-policies"></a><span data-ttu-id="58f64-282">Recursos adicionais para políticas de trabalho</span><span class="sxs-lookup"><span data-stu-id="58f64-282">Additional resources for job policies</span></span>
* [<span data-ttu-id="58f64-283">Postagem no blog de visão geral de política</span><span class="sxs-lookup"><span data-stu-id="58f64-283">Policy overview blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-overview/)
* [<span data-ttu-id="58f64-284">Postagem no blog de políticas no nível da conta</span><span class="sxs-lookup"><span data-stu-id="58f64-284">Account-level policies blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-account-level-policy/)
* [<span data-ttu-id="58f64-285">Postagem no blog de políticas no nível do trabalho</span><span class="sxs-lookup"><span data-stu-id="58f64-285">Job-level policies blog post</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-job-level-policy/)

## <a name="next-steps"></a><span data-ttu-id="58f64-286">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="58f64-286">Next steps</span></span>

* [<span data-ttu-id="58f64-287">Visão geral do Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="58f64-287">Overview of Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="58f64-288">Introdução ao análise Data Lake usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="58f64-288">Get started with Data Lake Analytics by using hello Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="58f64-289">Gerenciar o Azure Data Lake Analytics usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="58f64-289">Manage Azure Data Lake Analytics by using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)

