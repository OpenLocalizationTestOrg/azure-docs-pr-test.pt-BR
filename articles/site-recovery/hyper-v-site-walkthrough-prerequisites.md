---
title: "pré-requisitos do aaaReview Olá para replicação de tooAzure Hyper-V (sem o System Center VMM) usando o Azure Site Recovery | Microsoft Docs"
description: "Descreve os pré-requisitos de saudação para configurar a replicação, failover e recuperação de local tooAzure de VMs Hyper-V com o Azure Site Recovery"
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
ms.openlocfilehash: 3eefc3b7e3982ec6c413c1db7f7784863f9c701d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-hyper-v-without-vmm-tooazure-replication"></a><span data-ttu-id="b687b-103">Etapa 2: Examinar os pré-requisitos de saudação para replicação do Hyper-V (sem VMM) tooAzure</span><span class="sxs-lookup"><span data-stu-id="b687b-103">Step 2: Review hello prerequisites for Hyper-V (without VMM) tooAzure replication</span></span>

<span data-ttu-id="b687b-104">pré-requisitos de saudação são resumidos na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="b687b-104">hello prerequisites are summarized in hello table.</span></span>


<span data-ttu-id="b687b-105">**Pré-requisito**</span><span class="sxs-lookup"><span data-stu-id="b687b-105">**Prerequisite**</span></span> | <span data-ttu-id="b687b-106">**Detalhes**</span><span class="sxs-lookup"><span data-stu-id="b687b-106">**Details**</span></span> 
--- | --- 
<span data-ttu-id="b687b-107">**As tabelas**</span><span class="sxs-lookup"><span data-stu-id="b687b-107">**Azure**</span></span> | <span data-ttu-id="b687b-108">Saiba mais sobre os [requisitos do Azure](site-recovery-prereq.md#azure-requirements).</span><span class="sxs-lookup"><span data-stu-id="b687b-108">Learn about [Azure requirements](site-recovery-prereq.md#azure-requirements).</span></span>
<span data-ttu-id="b687b-109">**Servidores locais**</span><span class="sxs-lookup"><span data-stu-id="b687b-109">**On-premises servers**</span></span> | <span data-ttu-id="b687b-110">[Saiba mais](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) sobre os requisitos para hosts de Hyper-V local hello.</span><span class="sxs-lookup"><span data-stu-id="b687b-110">[Learn more](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) about requirements for hello on-premises Hyper-V hosts.</span></span>
<span data-ttu-id="b687b-111">**VMs do Hyper-V locais**</span><span class="sxs-lookup"><span data-stu-id="b687b-111">**On-premises Hyper-V VMs**</span></span> | <span data-ttu-id="b687b-112">Máquinas virtuais que você deseja tooreplicate devem estar executando uma [sistema operacional com suporte](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)e em conformidade com [pré-requisitos do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="b687b-112">VMs you want tooreplicate should be running a [supported operating system](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions), and conform with [Azure prerequisites](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
<span data-ttu-id="b687b-113">**URLs do Azure**</span><span class="sxs-lookup"><span data-stu-id="b687b-113">**Azure URLs**</span></span> | <span data-ttu-id="b687b-114">Hosts Hyper-V precisará de acesso toothese URLs:</span><span class="sxs-lookup"><span data-stu-id="b687b-114">Hyper-V hosts need access toothese URLs:</span></span><br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> <span data-ttu-id="b687b-115">Se você tiver regras de firewall baseado em endereço IP, certifique-se de que permitem comunicação tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b687b-115">If you have IP address-based firewall rules, ensure they allow communication tooAzure.</span></span><br/></br> <span data-ttu-id="b687b-116">Permitir Olá [intervalos de IP de Datacenter do Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)e hello porta HTTPS (443).</span><span class="sxs-lookup"><span data-stu-id="b687b-116">Allow hello [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and hello HTTPS (443) port.</span></span><br/></br> <span data-ttu-id="b687b-117">Permitir que os intervalos de endereços IP para Olá região do Azure de sua assinatura e Oeste dos EUA (usado para gerenciamento de identidade e controle de acesso).</span><span class="sxs-lookup"><span data-stu-id="b687b-117">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>



## <a name="next-steps"></a><span data-ttu-id="b687b-118">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b687b-118">Next steps</span></span>

- <span data-ttu-id="b687b-119">Se você estiver fazendo uma implantação completa, vá muito[etapa 3: planejar a capacidade](hyper-v-site-walkthrough-capacity.md)</span><span class="sxs-lookup"><span data-stu-id="b687b-119">If you're doing a full deployment, go too[Step 3: Plan capacity](hyper-v-site-walkthrough-capacity.md)</span></span>
- <span data-ttu-id="b687b-120">Se você estiver fazendo uma implantação de teste simples, vá muito[etapa 4: planejar a rede](hyper-v-site-walkthrough-network.md).</span><span class="sxs-lookup"><span data-stu-id="b687b-120">If you're doing a simple test deployment, go too[Step 4: Plan networking](hyper-v-site-walkthrough-network.md).</span></span>
