---
title: Migrar VMs do AWS para o Azure | Microsoft Docs
description: "Este artigo descreve como migrar máquinas virtuais em execução no AWS (Amazon Web Services) para o Azure usando o Azure Site Recovery."
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
ms.openlocfilehash: b3c0727a279649f4f7dae30d41027129ce5b04ee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="migrate-virtual-machines-in-amazon-web-services-aws-to-azure-with-azure-site-recovery"></a><span data-ttu-id="5c05d-103">Migrar máquinas virtuais no AWS (Amazon Web Services) para Azure com o Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="5c05d-103">Migrate virtual machines in Amazon Web Services (AWS) to Azure with Azure Site Recovery</span></span>

<span data-ttu-id="5c05d-104">Este artigo descreve como migrar instâncias Windows do AWS para máquinas virtuais do Azure com o serviço do [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5c05d-104">This article describes how to migrate AWS Windows instances to Azure virtual machines with the [Azure Site Recovery](site-recovery-overview.md) service.</span></span>

<span data-ttu-id="5c05d-105">A migração é efetivamente um failover do AWS para o Azure.</span><span class="sxs-lookup"><span data-stu-id="5c05d-105">Migration is effectively a failover from AWS to Azure.</span></span> <span data-ttu-id="5c05d-106">Não é possível fazer failback dos computadores para AWS e não há replicação contínua.</span><span class="sxs-lookup"><span data-stu-id="5c05d-106">You can't failback machines to AWS, and there's no ongoing replication.</span></span> <span data-ttu-id="5c05d-107">Este artigo descreve as etapas para migração no Portal do Azure, que se baseiam nas instruções para [replicar um computador físico no Azure](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="5c05d-107">This article describes the steps for migration in the Azure portal, and are based on the instructions for [replicating a physical machine to Azure](site-recovery-vmware-to-azure.md).</span></span>

<span data-ttu-id="5c05d-108">Publique eventuais comentários ou perguntas no final deste artigo ou no [Fórum dos Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="5c05d-108">Post any comments or questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

## <a name="supported-operating-systems"></a><span data-ttu-id="5c05d-109">Sistemas operacionais com suporte</span><span class="sxs-lookup"><span data-stu-id="5c05d-109">Supported operating systems</span></span>

<span data-ttu-id="5c05d-110">O Site Recovery pode ser usado para migrar instâncias EC2 que estejam executando qualquer um dos seguintes sistemas operacionais:</span><span class="sxs-lookup"><span data-stu-id="5c05d-110">Site Recovery can be used to migrate EC2 instances running any of the following operating systems:</span></span>

- <span data-ttu-id="5c05d-111">Windows (somente 64 bits)</span><span class="sxs-lookup"><span data-stu-id="5c05d-111">Windows(64 bit only)</span></span>
    - <span data-ttu-id="5c05d-112">Windows Server 2008 R2 SP1+ (drivers Citrix PV ou somente drivers AWS PV.</span><span class="sxs-lookup"><span data-stu-id="5c05d-112">Windows Server 2008 R2 SP1+ (Citrix PV drivers or AWS PV drivers only.</span></span> <span data-ttu-id="5c05d-113">**Não há suporte para instâncias executando drivers RedHat PV**) Windows Server 2012 Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="5c05d-113">**Instances running RedHat PV drivers are not supported**) Windows Server 2012 Windows Server 2012 R2</span></span>
- <span data-ttu-id="5c05d-114">Linux (somente 64 bits)</span><span class="sxs-lookup"><span data-stu-id="5c05d-114">Linux (64 bit only)</span></span>
    - <span data-ttu-id="5c05d-115">Red Hat Enterprise Linux 6.7 (apenas instâncias de HVM virtualizadas)</span><span class="sxs-lookup"><span data-stu-id="5c05d-115">Red Hat Enterprise Linux 6.7 (HVM virtualized instances only)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c05d-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5c05d-116">Prerequisites</span></span>

<span data-ttu-id="5c05d-117">Aqui está o que você precisa para essa implantação:</span><span class="sxs-lookup"><span data-stu-id="5c05d-117">Here's what you need for this deployment:</span></span>

* <span data-ttu-id="5c05d-118">**Servidor de configuração**: uma VM do Amazon EC2 executando o Windows Server 2012 R2 é implantada como o servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="5c05d-118">**Configuration server**: An Amazon EC2 VM running Windows Server 2012 R2 is deployed as the configuration server.</span></span> <span data-ttu-id="5c05d-119">Por padrão, os outros componentes do Azure Site Recovery (servidor de processo e servidor de destino mestre) são instalados quando você implanta o servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="5c05d-119">By default, the other Azure Site Recovery components (process server and master target server) are installed when you deploy the configuration server.</span></span> <span data-ttu-id="5c05d-120">Este artigo descreve as etapas para migração no Portal do Azure, que se baseiam nas instruções para [Saiba mais](site-recovery-components.md)</span><span class="sxs-lookup"><span data-stu-id="5c05d-120">This article describes the steps for migration in the Azure portal, and are based on the instructions for  [Learn more](site-recovery-components.md)</span></span>

* <span data-ttu-id="5c05d-121">**Instâncias EC2**: as instâncias de máquinas virtuais do Amazon EC2 que você quer migrar.</span><span class="sxs-lookup"><span data-stu-id="5c05d-121">**EC2 instances**: The Amazon EC2 virtual machines instances that you want to migrate.</span></span>

## <a name="deployment-steps"></a><span data-ttu-id="5c05d-122">Etapas de implantação.</span><span class="sxs-lookup"><span data-stu-id="5c05d-122">Deployment steps</span></span>

1. <span data-ttu-id="5c05d-123">Crie um cofre dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="5c05d-123">Create a Recovery Services vault.</span></span>
2. <span data-ttu-id="5c05d-124">O Grupo de segurança das suas instâncias do EC2 devem ter regras configuradas para permitir a comunicação entre a instância do EC2 que você deseja migrar e a instância na qual você planeja implantar o Servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="5c05d-124">The Security Group of your EC2 instances should have rules configured to allow communication between the EC2 instance that you want to migrate, and the instance on which you plan to deploy the Configuration Server.</span></span>

3. <span data-ttu-id="5c05d-125">Na mesma nuvem privada virtual do Amazon que suas instâncias do EC2, implante um servidor de configuração de ASR.</span><span class="sxs-lookup"><span data-stu-id="5c05d-125">On the same Amazon Virtual Private Cloud as your EC2 instances, deploy an ASR configuration server.</span></span> <span data-ttu-id="5c05d-126">Consulte o VMware/Físico para os pré-requisitos do Azure para requisitos de implantação do servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="5c05d-126">Refer the VMware / Physical to Azure prerequisites for configuration server deployment requirements.</span></span>

    ![DeployCS](./media/site-recovery-migrate-aws-to-azure/migration_pic2.png)

4.  <span data-ttu-id="5c05d-128">Quando o servidor de configuração for implantado em AWS e registrado com o cofre dos Serviços de Recuperação, você deverá ver o servidor de configuração e o servidor de processo sob a infraestrutura do Site Recovery conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="5c05d-128">Once your configuration server is deployed in AWS and registered with your Recovery Services vault, you should see the configuration server and process server under Site Recovery infrastructure as shown below:</span></span>

    ![CSinVault](./media/site-recovery-migrate-aws-to-azure/migration_pic3.png)

5. <span data-ttu-id="5c05d-130">Depois que você implantou o servidor de configuração (ele pode levar 15 minutos para ser exibido), valide se ele pode se comunicar com a VM que você deseja migrar.</span><span class="sxs-lookup"><span data-stu-id="5c05d-130">After you've deployed the configuration server (it might take up to 15 minustes for it to appear), validate that it can communicate with the VMs that you want to migrate.</span></span>

6. <span data-ttu-id="5c05d-131">[Defina as configurações de replicação](site-recovery-setup-replication-settings-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="5c05d-131">[Set up replication settings](site-recovery-setup-replication-settings-vmware.md).</span></span>

7. <span data-ttu-id="5c05d-132">Habilitar replicação: habilite a replicação para as VMs que você deseja migrar.</span><span class="sxs-lookup"><span data-stu-id="5c05d-132">Enable replication: Enable replication for the VMs you want to migrate.</span></span> <span data-ttu-id="5c05d-133">Você pode descobrir as instâncias de EC2 usando os endereços IP privados, que podem ser obtidos no console EC2.</span><span class="sxs-lookup"><span data-stu-id="5c05d-133">You can discover the EC2 instances using the private IP addresses, which you can get from the EC2 console.</span></span>

    ![SelectVM](./media/site-recovery-migrate-aws-to-azure/migration_pic4.png)

8. <span data-ttu-id="5c05d-135">Depois que as instâncias de EC2 tiverem sido protegidas e a replicação para o Azure for concluída, [execute um Failover de teste](site-recovery-test-failover-to-azure.md) para validar o desempenho do aplicativo no Azure.</span><span class="sxs-lookup"><span data-stu-id="5c05d-135">Once the EC2 instances have been protected and the replication to Azure is complete, [run a Test Failover](site-recovery-test-failover-to-azure.md) to validate your application's performance in Azure.</span></span>

    ![TFI](./media/site-recovery-migrate-aws-to-azure/migration_pic5.png)

9. <span data-ttu-id="5c05d-137">Execute um failover do AWS para o Azure para cada VM.</span><span class="sxs-lookup"><span data-stu-id="5c05d-137">Run a Failover from AWS to Azure for each VM.</span></span> <span data-ttu-id="5c05d-138">Opcionalmente, é possível criar um plano de recuperação e executar um failover para migrar várias máquinas virtuais do AWS para o Azure.</span><span class="sxs-lookup"><span data-stu-id="5c05d-138">Optionally, you can create a recovery plan and run a Failover, to migrate multiple virtual machines from AWS to Azure.</span></span> <span data-ttu-id="5c05d-139">[Leia mais](site-recovery-create-recovery-plans.md) sobre planos de recuperação.</span><span class="sxs-lookup"><span data-stu-id="5c05d-139">[Learn more](site-recovery-create-recovery-plans.md) about recovery plans.</span></span>

10. <span data-ttu-id="5c05d-140">Para a migração, você não precisa confirmar um failover.</span><span class="sxs-lookup"><span data-stu-id="5c05d-140">For migration, you don't need to commit a failover.</span></span> <span data-ttu-id="5c05d-141">Em vez disso, você seleciona a opção Migração Completa para cada computador que deseja migrar.</span><span class="sxs-lookup"><span data-stu-id="5c05d-141">Instead, you select the Complete Migration option for each machine you want to migrate.</span></span> <span data-ttu-id="5c05d-142">A ação Concluir Migração conclui o processo de migração, remove a replicação do computador e interrompe a cobrança do Site Recovery para o computador.</span><span class="sxs-lookup"><span data-stu-id="5c05d-142">The Complete Migration action finishes up the migration process, removes replication for the machine, and stops Site Recovery billing for the machine.</span></span>

    ![Migrar](./media/site-recovery-migrate-aws-to-azure/migration_pic6.png)

## <a name="next-steps"></a><span data-ttu-id="5c05d-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5c05d-144">Next steps</span></span>

- <span data-ttu-id="5c05d-145">[Prepare as máquinas migradas para habilitar a replicação](site-recovery-azure-to-azure-after-migration.md) em outra região para necessidades de recuperação de desastres.</span><span class="sxs-lookup"><span data-stu-id="5c05d-145">[Prepare migrated machines to enable replication](site-recovery-azure-to-azure-after-migration.md) to another region for disaster recovery needs.</span></span>
- <span data-ttu-id="5c05d-146">Inicie a proteção de suas cargas de trabalho ao [replicar máquinas virtuais do Azure.](site-recovery-azure-to-azure.md)</span><span class="sxs-lookup"><span data-stu-id="5c05d-146">Start protecting your workloads by [replicating Azure virtual machines.](site-recovery-azure-to-azure.md)</span></span>
