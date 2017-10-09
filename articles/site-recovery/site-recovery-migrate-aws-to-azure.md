---
title: aaaMigrate VMs do AWS tooAzure | Microsoft Docs
description: "Este artigo descreve como toomigrate virtual máquinas em execução no tooAzure serviços AWS (Amazon Web) usando o Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: bsiva
manager: jwhit
editor: 
ms.assetid: ddb412fd-32a8-4afa-9e39-738b11b91118
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/31/2017
ms.author: bsiva
ms.openlocfilehash: c99b781ec9cca5b8f9a847d3fc48408062b120b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-virtual-machines-in-amazon-web-services-aws-tooazure-with-azure-site-recovery"></a><span data-ttu-id="ac039-103">Migrar máquinas virtuais em tooAzure AWS Amazon Web Services () com o Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="ac039-103">Migrate virtual machines in Amazon Web Services (AWS) tooAzure with Azure Site Recovery</span></span>

<span data-ttu-id="ac039-104">Este artigo descreve como toomigrate Windows AWS instâncias de máquinas virtuais de tooAzure com hello [do Azure Site Recovery](site-recovery-overview.md) serviço.</span><span class="sxs-lookup"><span data-stu-id="ac039-104">This article describes how toomigrate AWS Windows instances tooAzure virtual machines with hello [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="ac039-105">A migração é efetivamente um failover do AWS tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ac039-105">Migration is effectively a failover from AWS tooAzure.</span></span> <span data-ttu-id="ac039-106">Não é possível failback máquinas tooAWS e não há nenhuma replicação em andamento.</span><span class="sxs-lookup"><span data-stu-id="ac039-106">You can't failback machines tooAWS, and there's no ongoing replication.</span></span> <span data-ttu-id="ac039-107">Este artigo descreve etapas Olá para migração em Olá portal do Azure e são baseados em instruções Olá para [replicar uma máquina física tooAzure](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="ac039-107">This article describes hello steps for migration in hello Azure portal, and are based on hello instructions for [replicating a physical machine tooAzure](site-recovery-vmware-to-azure.md).</span></span>

<span data-ttu-id="ac039-108">Postar comentários e perguntas na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="ac039-108">Post any comments or questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

## <a name="supported-operating-systems"></a><span data-ttu-id="ac039-109">Sistemas operacionais com suporte</span><span class="sxs-lookup"><span data-stu-id="ac039-109">Supported operating systems</span></span>

<span data-ttu-id="ac039-110">Recuperação de site pode ser usado toomigrate EC2 instâncias executando qualquer um dos Olá sistemas operacionais a seguir:</span><span class="sxs-lookup"><span data-stu-id="ac039-110">Site Recovery can be used toomigrate EC2 instances running any of hello following operating systems:</span></span>

- <span data-ttu-id="ac039-111">Windows (somente 64 bits)</span><span class="sxs-lookup"><span data-stu-id="ac039-111">Windows(64 bit only)</span></span>
    - <span data-ttu-id="ac039-112">Windows Server 2008 R2 SP1+ (drivers Citrix PV ou somente drivers AWS PV.</span><span class="sxs-lookup"><span data-stu-id="ac039-112">Windows Server 2008 R2 SP1+ (Citrix PV drivers or AWS PV drivers only.</span></span> <span data-ttu-id="ac039-113">**Não há suporte para instâncias executando drivers RedHat PV**) Windows Server 2012 Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="ac039-113">**Instances running RedHat PV drivers are not supported**) Windows Server 2012 Windows Server 2012 R2</span></span>
- <span data-ttu-id="ac039-114">Linux (somente 64 bits)</span><span class="sxs-lookup"><span data-stu-id="ac039-114">Linux (64 bit only)</span></span>
    - <span data-ttu-id="ac039-115">Red Hat Enterprise Linux 6.7 (apenas instâncias de HVM virtualizadas)</span><span class="sxs-lookup"><span data-stu-id="ac039-115">Red Hat Enterprise Linux 6.7 (HVM virtualized instances only)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac039-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ac039-116">Prerequisites</span></span>

<span data-ttu-id="ac039-117">Aqui está o que você precisa para essa implantação:</span><span class="sxs-lookup"><span data-stu-id="ac039-117">Here's what you need for this deployment:</span></span>

* <span data-ttu-id="ac039-118">**Servidor de configuração**: uma VM de EC2 Amazon executando o Windows Server 2012 R2 é implantado como servidor de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="ac039-118">**Configuration server**: An Amazon EC2 VM running Windows Server 2012 R2 is deployed as hello configuration server.</span></span> <span data-ttu-id="ac039-119">Por padrão, hello outros componentes do Azure Site Recovery (servidor de processo e servidor de destino mestre) são instalados quando você implanta o servidor de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="ac039-119">By default, hello other Azure Site Recovery components (process server and master target server) are installed when you deploy hello configuration server.</span></span> <span data-ttu-id="ac039-120">Este artigo descreve etapas Olá para migração em Olá portal do Azure e são baseados em instruções Olá para [Saiba mais](site-recovery-components.md)</span><span class="sxs-lookup"><span data-stu-id="ac039-120">This article describes hello steps for migration in hello Azure portal, and are based on hello instructions for  [Learn more](site-recovery-components.md)</span></span>

* <span data-ttu-id="ac039-121">**Instâncias de EC2**: Olá Amazon EC2 instâncias de máquinas virtuais que você deseja toomigrate.</span><span class="sxs-lookup"><span data-stu-id="ac039-121">**EC2 instances**: hello Amazon EC2 virtual machines instances that you want toomigrate.</span></span>

## <a name="deployment-steps"></a><span data-ttu-id="ac039-122">Etapas de implantação.</span><span class="sxs-lookup"><span data-stu-id="ac039-122">Deployment steps</span></span>

1. <span data-ttu-id="ac039-123">Crie um cofre dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="ac039-123">Create a Recovery Services vault.</span></span>
2. <span data-ttu-id="ac039-124">saudação de grupo de segurança de suas instâncias de EC2 deve ter regras configuradas tooallow comunicação entre Olá EC2 a instância que você toomigrate e instância de saudação em que planeje Olá toodeploy servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="ac039-124">hello Security Group of your EC2 instances should have rules configured tooallow communication between hello EC2 instance that you want toomigrate, and hello instance on which you plan toodeploy hello Configuration Server.</span></span>

3. <span data-ttu-id="ac039-125">Em Olá mesmo Amazon Virtual nuvem privada que suas instâncias de EC2, implantar um servidor de configuração de ASR.</span><span class="sxs-lookup"><span data-stu-id="ac039-125">On hello same Amazon Virtual Private Cloud as your EC2 instances, deploy an ASR configuration server.</span></span> <span data-ttu-id="ac039-126">Consulte Olá VMware / físicos tooAzure pré-requisitos para requisitos de implantação de servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="ac039-126">Refer hello VMware / Physical tooAzure prerequisites for configuration server deployment requirements.</span></span>

    ![DeployCS](./media/site-recovery-migrate-aws-to-azure/migration_pic2.png)

4.  <span data-ttu-id="ac039-128">Depois que o servidor de configuração é implantado em AWS e registrado com o Cofre de serviços de recuperação, você deve ver o servidor de configuração hello e servidor de processo na infraestrutura de recuperação de Site conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="ac039-128">Once your configuration server is deployed in AWS and registered with your Recovery Services vault, you should see hello configuration server and process server under Site Recovery infrastructure as shown below:</span></span>

    ![CSinVault](./media/site-recovery-migrate-aws-to-azure/migration_pic3.png)

5. <span data-ttu-id="ac039-130">Depois que você implantou o servidor de configuração de saudação (pode levar até too15 minustes para ele tooappear), valide que ele possa se comunicar com VMs Olá que você deseja toomigrate.</span><span class="sxs-lookup"><span data-stu-id="ac039-130">After you've deployed hello configuration server (it might take up too15 minustes for it tooappear), validate that it can communicate with hello VMs that you want toomigrate.</span></span>

6. <span data-ttu-id="ac039-131">[Defina as configurações de replicação](site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="ac039-131">[Set up replication settings](site-recovery-setup-replication-settings-vmware.md).</span></span>

7. <span data-ttu-id="ac039-132">Habilitar a replicação: habilitar a replicação para Olá VMs que você deseja toomigrate.</span><span class="sxs-lookup"><span data-stu-id="ac039-132">Enable replication: Enable replication for hello VMs you want toomigrate.</span></span> <span data-ttu-id="ac039-133">Você pode descobrir instâncias de EC2 hello usando Olá endereços IP privados, que pode ser obtido do console de EC2 hello.</span><span class="sxs-lookup"><span data-stu-id="ac039-133">You can discover hello EC2 instances using hello private IP addresses, which you can get from hello EC2 console.</span></span>

    ![SelectVM](./media/site-recovery-migrate-aws-to-azure/migration_pic4.png)

8. <span data-ttu-id="ac039-135">Depois de instâncias de saudação EC2 foram protegidas e Olá replicação tooAzure estiver concluída, [executar um Failover de teste](site-recovery-test-failover-to-azure.md) toovalidate o desempenho do aplicativo no Azure.</span><span class="sxs-lookup"><span data-stu-id="ac039-135">Once hello EC2 instances have been protected and hello replication tooAzure is complete, [run a Test Failover](site-recovery-test-failover-to-azure.md) toovalidate your application's performance in Azure.</span></span>

    ![TFI](./media/site-recovery-migrate-aws-to-azure/migration_pic5.png)

9. <span data-ttu-id="ac039-137">Execute um Failover de AWS tooAzure para cada VM.</span><span class="sxs-lookup"><span data-stu-id="ac039-137">Run a Failover from AWS tooAzure for each VM.</span></span> <span data-ttu-id="ac039-138">Opcionalmente, você pode criar um plano de recuperação e executar um Failover, toomigrate várias máquinas virtuais do AWS tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ac039-138">Optionally, you can create a recovery plan and run a Failover, toomigrate multiple virtual machines from AWS tooAzure.</span></span> <span data-ttu-id="ac039-139">[Saiba mais](site-recovery-create-recovery-plans.md) sobre planos de recuperação.</span><span class="sxs-lookup"><span data-stu-id="ac039-139">[Learn more](site-recovery-create-recovery-plans.md) about recovery plans.</span></span>

10. <span data-ttu-id="ac039-140">Para a migração, você não precisa toocommit um failover.</span><span class="sxs-lookup"><span data-stu-id="ac039-140">For migration, you don't need toocommit a failover.</span></span> <span data-ttu-id="ac039-141">Em vez disso, você selecionar a opção de concluir a migração de saudação para cada máquina que você deseja toomigrate.</span><span class="sxs-lookup"><span data-stu-id="ac039-141">Instead, you select hello Complete Migration option for each machine you want toomigrate.</span></span> <span data-ttu-id="ac039-142">Olá ação concluir a migração termina o processo de migração de hello, remove a replicação para máquina hello e interrompe a recuperação de Site de cobrança para a máquina de saudação.</span><span class="sxs-lookup"><span data-stu-id="ac039-142">hello Complete Migration action finishes up hello migration process, removes replication for hello machine, and stops Site Recovery billing for hello machine.</span></span>

    ![Migrar](./media/site-recovery-migrate-aws-to-azure/migration_pic6.png)

## <a name="next-steps"></a><span data-ttu-id="ac039-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ac039-144">Next steps</span></span>

- <span data-ttu-id="ac039-145">[Preparar máquinas migradas tooenable replicação](site-recovery-azure-to-azure-after-migration.md) tooanother região para necessidades de recuperação de desastres.</span><span class="sxs-lookup"><span data-stu-id="ac039-145">[Prepare migrated machines tooenable replication](site-recovery-azure-to-azure-after-migration.md) tooanother region for disaster recovery needs.</span></span>
- <span data-ttu-id="ac039-146">Inicie a proteção de suas cargas de trabalho ao [replicar máquinas virtuais do Azure.](site-recovery-azure-to-azure.md)</span><span class="sxs-lookup"><span data-stu-id="ac039-146">Start protecting your workloads by [replicating Azure virtual machines.](site-recovery-azure-to-azure.md)</span></span>
