---
title: "Examinar os pré-requisitos da replicação do Hyper-V para o Azure (sem o System Center VMM) usando o Azure Site Recovery | Microsoft Docs"
description: "Descreve os pré-requisitos para a configuração de replicação, failover e recuperação de VMs locais do Hyper-V para o Azure com o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 7ef3fb46-52f5-4c8a-b1a1-658c2305762a
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: cbb5d3598ef91512991d7d1e9f854eb12980752b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="step-2-review-the-prerequisites-for-hyper-v-without-vmm-to-azure-replication"></a><span data-ttu-id="034ad-103">Etapa 2: Examinar os pré-requisitos do Hyper-V (sem o VMM) para a replicação do Azure</span><span class="sxs-lookup"><span data-stu-id="034ad-103">Step 2: Review the prerequisites for Hyper-V (without VMM) to Azure replication</span></span>

<span data-ttu-id="034ad-104">Os pré-requisitos são resumidos na tabela.</span><span class="sxs-lookup"><span data-stu-id="034ad-104">The prerequisites are summarized in the table.</span></span>


<span data-ttu-id="034ad-105">**Pré-requisito**</span><span class="sxs-lookup"><span data-stu-id="034ad-105">**Prerequisite**</span></span> | <span data-ttu-id="034ad-106">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="034ad-106">**Details**</span></span> 
--- | --- 
<span data-ttu-id="034ad-107">**As tabelas**</span><span class="sxs-lookup"><span data-stu-id="034ad-107">**Azure**</span></span> | <span data-ttu-id="034ad-108">Saiba mais sobre os [requisitos do Azure](site-recovery-prereq.md#azure-requirements).</span><span class="sxs-lookup"><span data-stu-id="034ad-108">Learn about [Azure requirements](site-recovery-prereq.md#azure-requirements).</span></span>
<span data-ttu-id="034ad-109">**Servidores locais**</span><span class="sxs-lookup"><span data-stu-id="034ad-109">**On-premises servers**</span></span> | <span data-ttu-id="034ad-110">[Saiba mais](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) sobre os requisitos dos hosts Hyper-V locais.</span><span class="sxs-lookup"><span data-stu-id="034ad-110">[Learn more](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) about requirements for the on-premises Hyper-V hosts.</span></span>
<span data-ttu-id="034ad-111">**VMs do Hyper-V locais**</span><span class="sxs-lookup"><span data-stu-id="034ad-111">**On-premises Hyper-V VMs**</span></span> | <span data-ttu-id="034ad-112">As VMs que você deseja replicar devem estar executando um [sistema operacional com suporte](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions) e estar de acordo com os [pré-requisitos do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="034ad-112">VMs you want to replicate should be running a [supported operating system](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions), and conform with [Azure prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
<span data-ttu-id="034ad-113">**URLs do Azure**</span><span class="sxs-lookup"><span data-stu-id="034ad-113">**Azure URLs**</span></span> | <span data-ttu-id="034ad-114">Os hosts Hyper-V precisam de acesso a essas URLs:</span><span class="sxs-lookup"><span data-stu-id="034ad-114">Hyper-V hosts need access to these URLs:</span></span><br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> <span data-ttu-id="034ad-115">Se tiver regras de firewall baseadas no endereço IP, verifique se elas permitem a comunicação com o Azure.</span><span class="sxs-lookup"><span data-stu-id="034ad-115">If you have IP address-based firewall rules, ensure they allow communication to Azure.</span></span><br/></br> <span data-ttu-id="034ad-116">Permita os [Intervalos de IP do Datacenter do Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) e a porta HTTPS (443).</span><span class="sxs-lookup"><span data-stu-id="034ad-116">Allow the [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and the HTTPS (443) port.</span></span><br/></br> <span data-ttu-id="034ad-117">Permita os intervalos de endereços IP para a região do Azure da sua assinatura e para o Oeste dos EUA (usados para Controle de Acesso e Gerenciamento de Identidade).</span><span class="sxs-lookup"><span data-stu-id="034ad-117">Allow IP address ranges for the Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>



## <a name="next-steps"></a><span data-ttu-id="034ad-118">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="034ad-118">Next steps</span></span>

- <span data-ttu-id="034ad-119">Se estiver fazendo uma implantação completa, vá para a [Etapa 3: planejar a capacidade](hyper-v-site-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="034ad-119">If you're doing a full deployment, go to [Step 3: Plan capacity](hyper-v-site-walkthrough-capacity.md)</span></span>
- <span data-ttu-id="034ad-120">Se estiver fazendo uma implantação de teste simples, vá para a [Etapa 4: Planejar a rede](hyper-v-site-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="034ad-120">If you're doing a simple test deployment, go to [Step 4: Plan networking](hyper-v-site-walkthrough-network.md).</span></span>
