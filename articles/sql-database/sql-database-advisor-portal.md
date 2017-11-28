---
title: "recomendações de desempenho de aaaApply - banco de dados do SQL Azure | Microsoft Docs"
description: "Você pode usar as recomendações de desempenho do hello toofind portal do Azure que podem otimizar o desempenho do banco de dados do SQL Azure ou toocorrect algum problema identificado na carga de trabalho."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: cda8a646-0584-4368-b28a-85cdd9b54fcd
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 0b2234840fc3254d235db9e7d18f5bc912851c6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="find-and-apply-performance-recommendations"></a><span data-ttu-id="9f4d8-103">Localizar e aplicar recomendações de desempenho</span><span class="sxs-lookup"><span data-stu-id="9f4d8-103">Find and apply performance recommendations</span></span>

<span data-ttu-id="9f4d8-104">Você pode usar as recomendações de desempenho do hello toofind portal do Azure que podem otimizar o desempenho do banco de dados do SQL Azure ou toocorrect algum problema identificado na carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-104">You can use hello Azure portal toofind performance recommendations that can optimize performance of your Azure SQL Database or toocorrect some issue identified in your workload.</span></span> <span data-ttu-id="9f4d8-105">**Recomendação de desempenho** página no portal do Azure permite que você toofind Olá principais recomendações com base no impacto potencial.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-105">**Performance recommendation** page in Azure portal enables you toofind hello top recommendations based on their potential impact.</span></span> 

## <a name="viewing-recommendations"></a><span data-ttu-id="9f4d8-106">Exibindo recomendações</span><span class="sxs-lookup"><span data-stu-id="9f4d8-106">Viewing recommendations</span></span>

<span data-ttu-id="9f4d8-107">tooview e aplicar recomendações de desempenho, você precisa Olá correto [controle de acesso baseado em função](../active-directory/role-based-access-control-what-is.md) permissões no Azure.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-107">tooview and apply performance recommendations, you need hello correct [role-based access control](../active-directory/role-based-access-control-what-is.md) permissions in Azure.</span></span> <span data-ttu-id="9f4d8-108">**Leitor**, **Colaborador de banco de dados SQL** permissões são necessárias tooview recomendações, e **proprietário**, **Colaborador de banco de dados SQL** permissões são necessárias tooexecute quaisquer ações; Criar ou descartar índices e cancelar a criação do índice.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-108">**Reader**, **SQL DB Contributor** permissions are required tooview recommendations, and **Owner**, **SQL DB Contributor** permissions are required tooexecute any actions; create or drop indexes and cancel index creation.</span></span>

<span data-ttu-id="9f4d8-109">Use Olá recomendações de desempenho de toofind as etapas a seguir no portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="9f4d8-109">Use hello following steps toofind performance recommendations on Azure portal:</span></span>

1. <span data-ttu-id="9f4d8-110">Entrar toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9f4d8-110">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="9f4d8-111">Vá muito**mais serviços** > **bancos de dados SQL**e selecione o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-111">Go too**More services** > **SQL databases**, and select your database.</span></span>
3. <span data-ttu-id="9f4d8-112">Navegue muito**recomendação desempenho** recomendações de tooview disponíveis para o banco de dados selecionado hello.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-112">Navigate too**Performance recommendation** tooview available recommendations for hello selected database.</span></span>

<span data-ttu-id="9f4d8-113">Recomendações de desempenho estão shonw em Olá tabela toohello semelhante mostrada na figura a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="9f4d8-113">Performance recommendations are shonw in hello table similar toohello one shown on hello following figure:</span></span>

![Recomendações](./media/sql-database-advisor-portal/recommendations.png)

<span data-ttu-id="9f4d8-115">As recomendações são classificadas pelo impacto potencial no desempenho em Olá categorias a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f4d8-115">Recommendations are sorted by their potential impact on performance into hello following categories:</span></span>

| <span data-ttu-id="9f4d8-116">Impacto</span><span class="sxs-lookup"><span data-stu-id="9f4d8-116">Impact</span></span> | <span data-ttu-id="9f4d8-117">Descrição</span><span class="sxs-lookup"><span data-stu-id="9f4d8-117">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="9f4d8-118">Alto</span><span class="sxs-lookup"><span data-stu-id="9f4d8-118">High</span></span> |<span data-ttu-id="9f4d8-119">Recomendações de alto impacto devem fornecer o impacto mais significativo de desempenho hello.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-119">High impact recommendations should provide hello most significant performance impact.</span></span> |
| <span data-ttu-id="9f4d8-120">Média</span><span class="sxs-lookup"><span data-stu-id="9f4d8-120">Medium</span></span> |<span data-ttu-id="9f4d8-121">Recomendações de médio impacto devem melhorar o desempenho, mas não substancialmente.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-121">Medium impact recommendations should improve performance, but not substantially.</span></span> |
| <span data-ttu-id="9f4d8-122">Baixo</span><span class="sxs-lookup"><span data-stu-id="9f4d8-122">Low</span></span> |<span data-ttu-id="9f4d8-123">Recomendações de baixo impacto devem fornecer um desempenho melhor do que seria obtido sem elas, mas as melhorias podem não ser significativas.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-123">Low impact recommendations should provide better performance than without, but improvements might not be significant.</span></span> |


> [!NOTE]
> <span data-ttu-id="9f4d8-124">Banco de dados SQL do Azure precisa de atividades toomonitor pelo menos um dia na ordem tooidentify algumas recomendações.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-124">Azure SQL Database needs toomonitor activities at least for a day in order tooidentify some recommendations.</span></span> <span data-ttu-id="9f4d8-125">Olá banco de dados do SQL Azure mais facilmente pode otimizar para padrões de consulta consistente que para aleatórias intermitências irregular de atividade.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-125">hello Azure SQL Database can more easily optimize for consistent query patterns than it can for random spotty bursts of activity.</span></span> <span data-ttu-id="9f4d8-126">Se as recomendações não corrently disponível, Olá **recomendação desempenho** página fornece uma mensagem explicando o motivo.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-126">If recommendations are not corrently available, hello **Performance recommendation** page provides a message explaining why.</span></span>
> 

<span data-ttu-id="9f4d8-127">Você também pode exibir o status de saudação de operações de históricos de saudação.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-127">You can also view hello status of hello historical operations.</span></span> <span data-ttu-id="9f4d8-128">Selecione uma recomendação ou status toosee obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-128">Select a recommendation or status toosee  more details.</span></span>

<span data-ttu-id="9f4d8-129">Aqui está um exemplo de recomendação "Criar o índice" hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-129">Here is an example of "Create index" recommendation in hello Azure portal.</span></span>

![Criar índice](./media/sql-database-advisor-portal/sql-database-performance-recommendation.png)

## <a name="applying-recommendations"></a><span data-ttu-id="9f4d8-131">Aplicando recomendações</span><span class="sxs-lookup"><span data-stu-id="9f4d8-131">Applying recommendations</span></span>
<span data-ttu-id="9f4d8-132">Banco de dados do SQL Azure lhe dá controle total sobre como as recomendações são habilitadas usando qualquer um dos Olá três opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="9f4d8-132">Azure SQL Database gives you full control over how recommendations are enabled using any of hello following three options:</span></span> 

* <span data-ttu-id="9f4d8-133">Aplicar uma recomendação individual de cada vez.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-133">Apply individual recommendations one at a time.</span></span>
* <span data-ttu-id="9f4d8-134">Habilitar Olá tooautomatically ajuste automático aplicar recomendações.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-134">Enable hello Automatic tuning tooautomatically apply recommendations.</span></span>
* <span data-ttu-id="9f4d8-135">tooimplement uma recomendação manualmente, execute Olá recomendado script T-SQL no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-135">tooimplement a recommendation manually, run hello recommended T-SQL script against your database.</span></span>

<span data-ttu-id="9f4d8-136">Selecione qualquer recomendação tooview seus detalhes e, em seguida, clique em **exibir script** tooreview Olá detalhes exatos de como recomendação de saudação é criada.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-136">Select any recommendation tooview its details and then click **View script** tooreview hello exact details of how hello recommendation is created.</span></span>

<span data-ttu-id="9f4d8-137">Olá permanecerá online enquanto a recomendação de saudação é aplicada - utilização de recomendação de desempenho ou de ajuste automático nunca tem um banco de dados offline.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-137">hello database remains online while hello recommendation is applied -- using performance recommendation or automatic tuning never takes a database offline.</span></span>

### <a name="apply-an-individual-recommendation"></a><span data-ttu-id="9f4d8-138">Aplicar uma recomendação individual</span><span class="sxs-lookup"><span data-stu-id="9f4d8-138">Apply an individual recommendation</span></span>
<span data-ttu-id="9f4d8-139">Você pode examinar e aceitar uma recomendação de cada vez.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-139">You can review and accept recommendations one at a time.</span></span>

1. <span data-ttu-id="9f4d8-140">Em Olá **recomendações** folha, selecione uma recomendação.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-140">On hello **Recommendations** blade, select a recommendation.</span></span>
2. <span data-ttu-id="9f4d8-141">Em Olá **detalhes** folha clique **aplicar** botão.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-141">On hello **Details** blade click **Apply** button.</span></span>
   
    ![Aplicar recomendação](./media/sql-database-advisor-portal/apply.png)

<span data-ttu-id="9f4d8-143">Recomendação selecionada será aplicada no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-143">Selected recommendation will be applied on hello database.</span></span>

### <a name="removing-recommendations-from-hello-list"></a><span data-ttu-id="9f4d8-144">Removendo as recomendações da lista de saudação</span><span class="sxs-lookup"><span data-stu-id="9f4d8-144">Removing recommendations from hello list</span></span>
<span data-ttu-id="9f4d8-145">Se a lista de recomendações contiver itens que você deseja tooremove da lista de saudação, você pode descartar recomendação hello:</span><span class="sxs-lookup"><span data-stu-id="9f4d8-145">If your list of recommendations contains items that you want tooremove from hello list, you can discard hello recommendation:</span></span>

1. <span data-ttu-id="9f4d8-146">Selecione uma recomendação na lista de saudação do **recomendações** tooopen detalhes de saudação.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-146">Select a recommendation in hello list of **Recommendations** tooopen hello details.</span></span>
2. <span data-ttu-id="9f4d8-147">Clique em **descartar** em Olá **detalhes** folha.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-147">Click **Discard** on hello **Details** blade.</span></span>

<span data-ttu-id="9f4d8-148">Se desejar, você pode adicionar itens descartados fazer toohello **recomendações** lista:</span><span class="sxs-lookup"><span data-stu-id="9f4d8-148">If desired, you can add discarded items back toohello **Recommendations** list:</span></span>

1. <span data-ttu-id="9f4d8-149">Em Olá **recomendações** folha clique **exibição descartada**.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-149">On hello **Recommendations** blade click **View discarded**.</span></span>
2. <span data-ttu-id="9f4d8-150">Selecione um item descartado Olá lista tooview seus detalhes.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-150">Select a discarded item from hello list tooview its details.</span></span>
3. <span data-ttu-id="9f4d8-151">Opcionalmente, clique em **desfazer descartar** tooadd Olá índice toohello back lista principal de **recomendações**.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-151">Optionally, click **Undo Discard** tooadd hello index back toohello main list of **Recommendations**.</span></span>


### <a name="enable-automatic-tuning"></a><span data-ttu-id="9f4d8-152">Habilitar o ajuste automático</span><span class="sxs-lookup"><span data-stu-id="9f4d8-152">Enable automatic tuning</span></span>
<span data-ttu-id="9f4d8-153">Você pode definir as recomendações do hello Azure SQL Database tooimplement automaticamente.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-153">You can set hello Azure SQL Database tooimplement recommendations automatically.</span></span> <span data-ttu-id="9f4d8-154">Conforme as recomendações são disponibilizadas, elas serão aplicadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-154">As recommendations become available they will automatically be applied.</span></span> <span data-ttu-id="9f4d8-155">Como com todas as recomendações gerenciadas pelo Olá serviço se Olá impacto no desempenho é recomendação negativo hello será revertido.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-155">As with all recommendations managed by hello service if hello performance impact is negative hello recommendation will be reverted.</span></span>

1. <span data-ttu-id="9f4d8-156">Em Olá **recomendações** folha, clique em **automatizar**:</span><span class="sxs-lookup"><span data-stu-id="9f4d8-156">On hello **Recommendations** blade, click **Automate**:</span></span>
   
    ![Configurações do supervisor](./media/sql-database-advisor-portal/settings.png)
2. <span data-ttu-id="9f4d8-158">Selecione tooautomate de ações:</span><span class="sxs-lookup"><span data-stu-id="9f4d8-158">Select actions tooautomate:</span></span>
   
    ![Índices recomendados](./media/sql-database-advisor-portal/automation.png)

### <a name="manually-run-hello-recommended-t-sql-script"></a><span data-ttu-id="9f4d8-160">Executar manualmente Olá recomendado script T-SQL</span><span class="sxs-lookup"><span data-stu-id="9f4d8-160">Manually run hello recommended T-SQL script</span></span>
<span data-ttu-id="9f4d8-161">Selecione qualquer recomendação e clique em **Exibir script**.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-161">Select any recommendation and then click **View script**.</span></span> <span data-ttu-id="9f4d8-162">Execute este script no banco de dados toomanually aplicar a recomendação de saudação.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-162">Run this script against your database toomanually apply hello recommendation.</span></span>

<span data-ttu-id="9f4d8-163">*Índices que são executados manualmente não são monitorados e validados para impacto no desempenho pelo serviço Olá* portanto é recomendável que você monitore esses índices após a criação tooverify eles prover ganhos de desempenho e ajustar ou excluí-los se é necessário.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-163">*Indexes that are manually executed are not monitored and validated for performance impact by hello service* so it is suggested that you monitor these indexes after creation tooverify they provide performance gains and adjust or delete them if necessary.</span></span> <span data-ttu-id="9f4d8-164">Para obter detalhes sobre a criação de índices, consulte [CRIAR ÍNDICE (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).</span><span class="sxs-lookup"><span data-stu-id="9f4d8-164">For details about creating indexes, see [CREATE INDEX (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).</span></span>

### <a name="canceling-recommendations"></a><span data-ttu-id="9f4d8-165">Cancelando recomendações</span><span class="sxs-lookup"><span data-stu-id="9f4d8-165">Canceling recommendations</span></span>
<span data-ttu-id="9f4d8-166">Recomendações que estão com status **Pendente**, **Verificando** ou **Sucesso** podem ser canceladas.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-166">Recommendations that are in a **Pending**, **Verifying**, or **Success** status can be canceled.</span></span> <span data-ttu-id="9f4d8-167">Recomendações com status **Executando** não podem ser canceladas.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-167">Recommendations with a status of **Executing** cannot be canceled.</span></span>

1. <span data-ttu-id="9f4d8-168">Selecione uma recomendação na Olá **histórico ajuste** Olá de tooopen área **detalhes das recomendações** folha.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-168">Select a recommendation in hello **Tuning History** area tooopen hello **recommendations details** blade.</span></span>
2. <span data-ttu-id="9f4d8-169">Clique em **Cancelar** tooabort processo de saudação da aplicação de recomendação de saudação.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-169">Click **Cancel** tooabort hello process of applying hello recommendation.</span></span>

## <a name="monitoring-operations"></a><span data-ttu-id="9f4d8-170">Monitoramento de operações</span><span class="sxs-lookup"><span data-stu-id="9f4d8-170">Monitoring operations</span></span>
<span data-ttu-id="9f4d8-171">A aplicação de uma recomendação pode não acontecer instantaneamente.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-171">Applying a recommendation might not happen instantaneously.</span></span> <span data-ttu-id="9f4d8-172">portal Olá fornece detalhes sobre o status de saudação da recomendação.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-172">hello portal provides details regarding hello status of recommendation.</span></span> <span data-ttu-id="9f4d8-173">Olá seguem possíveis estados que um índice pode estar em:</span><span class="sxs-lookup"><span data-stu-id="9f4d8-173">hello following are possible states that an index can be in:</span></span>

| <span data-ttu-id="9f4d8-174">Status</span><span class="sxs-lookup"><span data-stu-id="9f4d8-174">Status</span></span> | <span data-ttu-id="9f4d8-175">Descrição</span><span class="sxs-lookup"><span data-stu-id="9f4d8-175">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="9f4d8-176">Pendente</span><span class="sxs-lookup"><span data-stu-id="9f4d8-176">Pending</span></span> |<span data-ttu-id="9f4d8-177">O comando Aplicar recomendação foi recebido e está programado para execução.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-177">Apply recommendation command has been received and is scheduled for execution.</span></span> |
| <span data-ttu-id="9f4d8-178">Executando</span><span class="sxs-lookup"><span data-stu-id="9f4d8-178">Executing</span></span> |<span data-ttu-id="9f4d8-179">recomendação Hello está sendo aplicada.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-179">hello recommendation is being applied.</span></span> |
| <span data-ttu-id="9f4d8-180">Verificando</span><span class="sxs-lookup"><span data-stu-id="9f4d8-180">Verifying</span></span> |<span data-ttu-id="9f4d8-181">Recomendação foi aplicada com êxito e serviço hello está medindo benefícios hello.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-181">Recommendation was successfully applied and hello service is measuring hello benefits.</span></span> |
| <span data-ttu-id="9f4d8-182">Sucesso</span><span class="sxs-lookup"><span data-stu-id="9f4d8-182">Success</span></span> |<span data-ttu-id="9f4d8-183">A recomendação foi aplicada com êxito e benefícios foram calculados.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-183">Recommendation was successfully applied and benefits have been measured.</span></span> |
| <span data-ttu-id="9f4d8-184">Erro</span><span class="sxs-lookup"><span data-stu-id="9f4d8-184">Error</span></span> |<span data-ttu-id="9f4d8-185">Ocorreu um erro durante o processo de saudação da aplicação de recomendação de saudação.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-185">An error occurred during hello process of applying hello recommendation.</span></span> <span data-ttu-id="9f4d8-186">Isso pode ser um problema temporário ou possivelmente uma tabela de toohello de alteração de esquema e o script hello não é mais válido.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-186">This can be a transient issue, or possibly a schema change toohello table and hello script is no longer valid.</span></span> |
| <span data-ttu-id="9f4d8-187">Revertendo</span><span class="sxs-lookup"><span data-stu-id="9f4d8-187">Reverting</span></span> |<span data-ttu-id="9f4d8-188">recomendação de saudação foi aplicada, mas foi considerada não funcionais e está sendo revertida automaticamente.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-188">hello recommendation was applied, but has been deemed non-performant and is being automatically reverted.</span></span> |
| <span data-ttu-id="9f4d8-189">Revertida</span><span class="sxs-lookup"><span data-stu-id="9f4d8-189">Reverted</span></span> |<span data-ttu-id="9f4d8-190">recomendação de saudação foi revertida.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-190">hello recommendation was reverted.</span></span> |

<span data-ttu-id="9f4d8-191">Clique em uma recomendação no processo de saudação lista toosee mais detalhes:</span><span class="sxs-lookup"><span data-stu-id="9f4d8-191">Click an in-process recommendation from hello list toosee more details:</span></span>

![Índices recomendados](./media/sql-database-advisor-portal/operations.png)

### <a name="reverting-a-recommendation"></a><span data-ttu-id="9f4d8-193">Revertendo uma recomendação</span><span class="sxs-lookup"><span data-stu-id="9f4d8-193">Reverting a recommendation</span></span>
<span data-ttu-id="9f4d8-194">Se você usou a recomendação de Olá Olá desempenho recomendações tooapply (ou seja, que você não executou manualmente script hello T-SQL) ele será automaticamente revertê-lo se ele encontrar hello toobe de impacto de desempenho negativo.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-194">If you used hello performance recommendations tooapply hello recommendation (meaning you did not manually run hello T-SQL script) it will automatically revert it if it finds hello performance impact toobe negative.</span></span> <span data-ttu-id="9f4d8-195">Se por algum motivo você simplesmente deseja toorevert uma recomendação você pode fazer a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="9f4d8-195">If for any reason you simply want toorevert a recommendation you can do hello following:</span></span>

1. <span data-ttu-id="9f4d8-196">Selecione uma recomendação aplicada com êxito no hello **histórico de ajuste** área.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-196">Select a successfully applied recommendation in hello **Tuning history** area.</span></span>
2. <span data-ttu-id="9f4d8-197">Clique em **Revert** em Olá **detalhes de recomendação** folha.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-197">Click **Revert** on hello **recommendation details** blade.</span></span>

![Índices recomendados](./media/sql-database-advisor-portal/details.png)

## <a name="monitoring-performance-impact-of-index-recommendations"></a><span data-ttu-id="9f4d8-199">Monitorando o impacto do desempenho de recomendações de índice</span><span class="sxs-lookup"><span data-stu-id="9f4d8-199">Monitoring performance impact of index recommendations</span></span>
<span data-ttu-id="9f4d8-200">Depois que as recomendações são implementadas com êxito (no momento, as operações de índice e parametrizar somente recomendações de consultas) você pode clicar em **consulta Insights** em Olá recomendação detalhes folha tooopen [consulta Informações de desempenho](sql-database-query-performance.md) e ver o impacto no desempenho Olá as consultas principais.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-200">After recommendations are successfully implemented (currently, index operations and parameterize queries recommendations only) you can click **Query Insights** on hello recommendation details blade tooopen [Query Performance Insights](sql-database-query-performance.md) and see hello performance impact of your top queries.</span></span>

![Monitorar o impacto do desempenho](./media/sql-database-advisor-portal/query-insights.png)

## <a name="summary"></a><span data-ttu-id="9f4d8-202">Resumo</span><span class="sxs-lookup"><span data-stu-id="9f4d8-202">Summary</span></span>
<span data-ttu-id="9f4d8-203">O Banco de Dados SQL do Azure fornece recomendações para aprimorar o desempenho do bancos de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-203">Azure SQL Database provides recommendations for improving SQL database performance.</span></span> <span data-ttu-id="9f4d8-204">Ao fornecer scripts T-SQL, além de individuais e totalmente automáticos, você obtém uma assistência útil ao otimizar seu banco de dados e, como resultado final, melhorar o desempenho da consulta.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-204">By providing T-SQL scripts, as well as individual and fully-automatic, you get a helpful assistance in optimizing your database and ultimately improving query performance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f4d8-205">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9f4d8-205">Next steps</span></span>
<span data-ttu-id="9f4d8-206">Monitorar suas recomendações e continuar tooapply-los toorefine desempenho.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-206">Monitor your recommendations and continue tooapply them toorefine performance.</span></span> <span data-ttu-id="9f4d8-207">Cargas de trabalho de banco de dados são dinâmicas e mudam continuamente.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-207">Database workloads are dynamic and change continuously.</span></span> <span data-ttu-id="9f4d8-208">Banco de dados SQL do Azure continuará toomonitor e fornece recomendações que potencialmente podem melhorar o desempenho de seu banco de dados.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-208">Azure SQL Database will continue toomonitor and provide recommendations that can potentially improve your database's performance.</span></span> 

* <span data-ttu-id="9f4d8-209">Consulte [ajuste automático](sql-database-automatic-tuning.md) toolearn mais sobre Olá ajuste automático no banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-209">See [Automatic tuning](sql-database-automatic-tuning.md) toolearn more about hello automatic tuning in Azure SQL Database.</span></span>
* <span data-ttu-id="9f4d8-210">Consulte [Recomendações de desempenho](sql-database-advisor.md) para obter uma visão geral das recomendações de desempenho do Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-210">See [Performance recommendations](sql-database-advisor.md) for an overview of Azure SQL Database performance recommendations.</span></span>
* <span data-ttu-id="9f4d8-211">Consulte [Query Performance Insight](sql-database-query-performance.md) toolearn sobre como exibir o impacto no desempenho Olá as consultas principais.</span><span class="sxs-lookup"><span data-stu-id="9f4d8-211">See [Query Performance Insights](sql-database-query-performance.md) toolearn about viewing hello performance impact of your top queries.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9f4d8-212">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="9f4d8-212">Additional resources</span></span>
* [<span data-ttu-id="9f4d8-213">Repositório de Consultas</span><span class="sxs-lookup"><span data-stu-id="9f4d8-213">Query Store</span></span>](https://msdn.microsoft.com/library/dn817826.aspx)
* [<span data-ttu-id="9f4d8-214">CREATE INDEX</span><span class="sxs-lookup"><span data-stu-id="9f4d8-214">CREATE INDEX</span></span>](https://msdn.microsoft.com/library/ms188783.aspx)
* [<span data-ttu-id="9f4d8-215">Controle de acesso baseado em função</span><span class="sxs-lookup"><span data-stu-id="9f4d8-215">Role-based access control</span></span>](../active-directory/role-based-access-control-what-is.md)

