---
title: "aaaSet as configurações de replicação para o Azure Site Recovery | Microsoft Docs"
description: "Descreve como a replicação de tooorchestrate de recuperação de Site toodeploy, failover e recuperação de máquinas virtuais do Hyper-V no VMM nuvens tooAzure."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: rayne-wiselman
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2017
ms.author: sutalasi
ms.openlocfilehash: 618e92e42411732a2a1bb75c5e5ea8a433cd7d58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-replication-policy-for-vmware-tooazure"></a><span data-ttu-id="fde09-103">Gerenciar a política de replicação para VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="fde09-103">Manage replication policy for VMware tooAzure</span></span>


## <a name="create-a-replication-policy"></a><span data-ttu-id="fde09-104">Criar uma política de replicação</span><span class="sxs-lookup"><span data-stu-id="fde09-104">Create a replication policy</span></span>

1. <span data-ttu-id="fde09-105">Selecione **Gerenciar** > **Infraestrutura do Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="fde09-105">Select **Manage** > **Site Recovery Infrastructure**.</span></span>
2. <span data-ttu-id="fde09-106">Selecione **Políticas de replicação** em **Para VMware e Computadores físicos**.</span><span class="sxs-lookup"><span data-stu-id="fde09-106">Select **Replication policies** under **For VMware and Physical machines**.</span></span>
3. <span data-ttu-id="fde09-107">Selecione **+ Política de replicação**.</span><span class="sxs-lookup"><span data-stu-id="fde09-107">Select **+Replication policy**.</span></span>

    ![Criar política de replicação](./media/site-recovery-setup-replication-settings-vmware/createpolicy.png)

4. <span data-ttu-id="fde09-109">Insira o nome da política de saudação.</span><span class="sxs-lookup"><span data-stu-id="fde09-109">Enter hello policy name.</span></span>

5. <span data-ttu-id="fde09-110">Em **limite de RPO**, especifique o limite RPO hello.</span><span class="sxs-lookup"><span data-stu-id="fde09-110">In **RPO threshold**, specify hello RPO limit.</span></span> <span data-ttu-id="fde09-111">Alertas serão gerados quando a replicação contínua excede esse limite.</span><span class="sxs-lookup"><span data-stu-id="fde09-111">Alerts will be generated when continuous replication exceeds this limit.</span></span>
6. <span data-ttu-id="fde09-112">Em **retenção de ponto de recuperação**, especifique (em horas) Olá duração da janela de retenção Olá para cada ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="fde09-112">In **Recovery point retention**, specify (in hours) hello duration of hello retention window for each recovery point.</span></span> <span data-ttu-id="fde09-113">Computadores protegidos podem ser recuperados tooany ponto dentro de uma janela de retenção.</span><span class="sxs-lookup"><span data-stu-id="fde09-113">Protected machines can be recovered tooany point within a retention window.</span></span>

    > [!NOTE]
    > <span data-ttu-id="fde09-114">Todas as horas de too24 de retenção são suportadas para armazenamento de toopremium replicado de máquinas.</span><span class="sxs-lookup"><span data-stu-id="fde09-114">Up too24 hours of retention is supported for machines replicated toopremium storage.</span></span> <span data-ttu-id="fde09-115">Todas as horas de too72 de retenção são suportadas para armazenamento de toostandard replicado de máquinas.</span><span class="sxs-lookup"><span data-stu-id="fde09-115">Up too72 hours of retention is supported for machines replicated toostandard storage.</span></span>

    > [!NOTE]
    > <span data-ttu-id="fde09-116">Uma política de replicação para failback é criada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="fde09-116">A replication policy for failback is automatically created.</span></span>

7. <span data-ttu-id="fde09-117">Em **Frequência de instantâneos consistente com o aplicativo**, especifique com que frequência (em minutos) serão criados os pontos de recuperação que contém instantâneos consistentes com aplicativos.</span><span class="sxs-lookup"><span data-stu-id="fde09-117">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points that contain application-consistent snapshots will be created.</span></span>

8. <span data-ttu-id="fde09-118">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="fde09-118">Click **OK**.</span></span> <span data-ttu-id="fde09-119">política de saudação deve ser criada em too60 de 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="fde09-119">hello policy should be created in 30 too60 seconds.</span></span>

![Geração de política de replicação](./media/site-recovery-setup-replication-settings-vmware/Creating-Policy.png)

## <a name="associate-a-configuration-server-with-a-replication-policy"></a><span data-ttu-id="fde09-121">Associar um servidor de configuração com uma política de replicação</span><span class="sxs-lookup"><span data-stu-id="fde09-121">Associate a configuration server with a replication policy</span></span>
1. <span data-ttu-id="fde09-122">Escolha Olá toowhich de política de replicação você deseja que o servidor de configuração de saudação tooassociate.</span><span class="sxs-lookup"><span data-stu-id="fde09-122">Choose hello replication policy toowhich you want tooassociate hello configuration server.</span></span>
2. <span data-ttu-id="fde09-123">Clique em **Associar**.</span><span class="sxs-lookup"><span data-stu-id="fde09-123">Click **Associate**.</span></span>
<span data-ttu-id="fde09-124">![Associar o servidor de configuração](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)</span><span class="sxs-lookup"><span data-stu-id="fde09-124">![Associate configuration server](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-1.PNG)</span></span>

3. <span data-ttu-id="fde09-125">Selecione o servidor de configuração de saudação da lista de saudação de servidores.</span><span class="sxs-lookup"><span data-stu-id="fde09-125">Select hello configuration server from hello list of servers.</span></span>
4. <span data-ttu-id="fde09-126">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="fde09-126">Click **OK**.</span></span> <span data-ttu-id="fde09-127">servidor de configuração de saudação deve ser associado em um tootwo minutos.</span><span class="sxs-lookup"><span data-stu-id="fde09-127">hello configuration server should be associated in one tootwo minutes.</span></span>

![Associação de servidor de configuração](./media/site-recovery-setup-replication-settings-vmware/Associate-CS-2.png)

## <a name="edit-a-replication-policy"></a><span data-ttu-id="fde09-129">Editar uma política de replicação</span><span class="sxs-lookup"><span data-stu-id="fde09-129">Edit a replication policy</span></span>
1. <span data-ttu-id="fde09-130">Escolha a política de replicação de saudação do qual você deseja que as configurações de replicação tooedit.</span><span class="sxs-lookup"><span data-stu-id="fde09-130">Choose hello replication policy for which you want tooedit replication settings.</span></span>
<span data-ttu-id="fde09-131">![Editar política de replicação](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)</span><span class="sxs-lookup"><span data-stu-id="fde09-131">![Edit replication policy](./media/site-recovery-setup-replication-settings-vmware/Select-Policy.png)</span></span>

2. <span data-ttu-id="fde09-132">Clique em **Editar Configurações**.</span><span class="sxs-lookup"><span data-stu-id="fde09-132">Click **Edit Settings**.</span></span>
<span data-ttu-id="fde09-133">![Editar configurações de política de replicação](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)</span><span class="sxs-lookup"><span data-stu-id="fde09-133">![Edit replication policy settings](./media/site-recovery-setup-replication-settings-vmware/Edit-Policy.png)</span></span>

3. <span data-ttu-id="fde09-134">Alterar configurações de saudação com base em suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="fde09-134">Change hello settings based on your need.</span></span>
4. <span data-ttu-id="fde09-135">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="fde09-135">Click **Save**.</span></span> <span data-ttu-id="fde09-136">política de saudação devem ser salvos em dois toofive minutos, dependendo de quantos VMs estão usando essa política de replicação.</span><span class="sxs-lookup"><span data-stu-id="fde09-136">hello policy should be saved in two toofive minutes, depending on how many VMs are using that replication policy.</span></span>

![Salvar política de replicação](./media/site-recovery-setup-replication-settings-vmware/Save-Policy.png)

## <a name="dissociate-a-configuration-server-from-a-replication-policy"></a><span data-ttu-id="fde09-138">Desassociar um servidor de configuração de uma política de replicação</span><span class="sxs-lookup"><span data-stu-id="fde09-138">Dissociate a configuration server from a replication policy</span></span>
1. <span data-ttu-id="fde09-139">Escolha Olá toowhich de política de replicação você deseja que o servidor de configuração de saudação tooassociate.</span><span class="sxs-lookup"><span data-stu-id="fde09-139">Choose hello replication policy toowhich you want tooassociate hello configuration server.</span></span>
2. <span data-ttu-id="fde09-140">Clique em **Desassociar**.</span><span class="sxs-lookup"><span data-stu-id="fde09-140">Click **Dissociate**.</span></span>
3. <span data-ttu-id="fde09-141">Selecione o servidor de configuração de saudação da lista de saudação de servidores.</span><span class="sxs-lookup"><span data-stu-id="fde09-141">Select hello configuration server from hello list of servers.</span></span>
4. <span data-ttu-id="fde09-142">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="fde09-142">Click **OK**.</span></span> <span data-ttu-id="fde09-143">servidor de configuração de saudação deve ser desassociada em um tootwo minutos.</span><span class="sxs-lookup"><span data-stu-id="fde09-143">hello configuration server should be dissociated in one tootwo minutes.</span></span>

    > [!NOTE]
    > <span data-ttu-id="fde09-144">Não é possível desassociar um servidor de configuração, se houver pelo menos um item replicado usando a política de saudação.</span><span class="sxs-lookup"><span data-stu-id="fde09-144">You cannot dissociate a configuration server if there is at least one replicated item using hello policy.</span></span> <span data-ttu-id="fde09-145">Verifique se não há nenhum item replicado usando a política de saudação antes de você desassociar o servidor de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="fde09-145">Make sure there are no replicated items using hello policy before you dissociate hello configuration server.</span></span>

## <a name="delete-a-replication-policy"></a><span data-ttu-id="fde09-146">Excluir uma política de replicação</span><span class="sxs-lookup"><span data-stu-id="fde09-146">Delete a replication policy</span></span>

1. <span data-ttu-id="fde09-147">Escolha a política de replicação Olá que você deseja toodelete.</span><span class="sxs-lookup"><span data-stu-id="fde09-147">Choose hello replication policy that you want toodelete.</span></span>
2. <span data-ttu-id="fde09-148">Clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="fde09-148">Click **Delete**.</span></span> <span data-ttu-id="fde09-149">política de saudação deve ser excluída em too60 de 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="fde09-149">hello policy should be deleted in 30 too60 seconds.</span></span>

    > [!NOTE]
    > <span data-ttu-id="fde09-150">Você não pode excluir uma política de replicação se ele tem pelo menos um tooit de associados do servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="fde09-150">You cannot delete a replication policy if it has at least one configuration server associated tooit.</span></span> <span data-ttu-id="fde09-151">Verifique se não existem itens replicados usando a política de saudação e exclua que todos os Olá associadas a servidores de configuração antes de excluir a política de saudação.</span><span class="sxs-lookup"><span data-stu-id="fde09-151">Make sure there are no replicated items using hello policy and delete all hello associated configuration servers before you delete hello policy.</span></span>
