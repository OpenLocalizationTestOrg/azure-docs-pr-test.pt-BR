---
title: "aaaPrepare Hyper-V hospeda (sem o System Center VMM) para a replicação tooAzure | Microsoft Docs"
description: "Descreve como tooprepare Hyper-V hospeda para tooAzure de replicação usando o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 0f204e24-8d78-4076-95c5-8137d1be9c01
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 714b229d5efbd66a9844bd09e36ac3f69919a6bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-hyper-v-hosts-for-replication-tooazure"></a><span data-ttu-id="edb27-103">Etapa 6: Preparar hosts Hyper-V para replicação tooAzure</span><span class="sxs-lookup"><span data-stu-id="edb27-103">Step 6: Prepare Hyper-V hosts for replication tooAzure</span></span>

<span data-ttu-id="edb27-104">Use instruções Olá tooprepare este artigo toointeract de hosts do Hyper-V com o Azure Site Recovery no local.</span><span class="sxs-lookup"><span data-stu-id="edb27-104">Use hello instructions in this article tooprepare on-premises Hyper-V hosts toointeract with Azure Site Recovery.</span></span>

<span data-ttu-id="edb27-105">Depois de ler este artigo, postar os comentários na parte inferior da saudação ou questões técnicas Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="edb27-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prepare-hosts"></a><span data-ttu-id="edb27-106">Preparar os hosts</span><span class="sxs-lookup"><span data-stu-id="edb27-106">Prepare hosts</span></span>

- <span data-ttu-id="edb27-107">Verifique se os hosts Hyper-V de saudação atendem Olá [pré-requisitos](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).</span><span class="sxs-lookup"><span data-stu-id="edb27-107">Make sure that hello Hyper-V hosts meet hello [prerequisites](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).</span></span>
- <span data-ttu-id="edb27-108">Certifique-se de que os hosts de saudação podem acessar Olá necessário URLs:</span><span class="sxs-lookup"><span data-stu-id="edb27-108">Make sure that hello hosts can access hello required URLs:</span></span>

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- <span data-ttu-id="edb27-109">Se você tiver regras de firewall baseado em endereço IP, certifique-se de que permitem comunicação tooAzure.</span><span class="sxs-lookup"><span data-stu-id="edb27-109">If you have IP address-based firewall rules, ensure they allow communication tooAzure.</span></span>
- <span data-ttu-id="edb27-110">Permitir Olá [intervalos de IP de Datacenter do Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)e hello porta HTTPS (443).</span><span class="sxs-lookup"><span data-stu-id="edb27-110">Allow hello [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and hello HTTPS (443) port.</span></span>
- <span data-ttu-id="edb27-111">Permitir que os intervalos de endereços IP para Olá região do Azure de sua assinatura e Oeste dos EUA (usado para gerenciamento de identidade e controle de acesso).</span><span class="sxs-lookup"><span data-stu-id="edb27-111">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

<span data-ttu-id="edb27-112">Durante a implantação da recuperação de Site, você deve adicionar hosts Hyper-V que contêm máquinas virtuais que você deseja tooreplicate tooa Hyper-V site.</span><span class="sxs-lookup"><span data-stu-id="edb27-112">During Site Recovery deployment, you add Hyper-V hosts that contain VMs you want tooreplicate tooa Hyper-V site.</span></span> <span data-ttu-id="edb27-113">Olá provedor de recuperação de Site e o agente de serviços de recuperação são instalados em cada host.</span><span class="sxs-lookup"><span data-stu-id="edb27-113">hello Site Recovery Provider, and Recovery Services agent are installed on each host.</span></span> <span data-ttu-id="edb27-114">site Olá Hyper-V é registrado no cofre de serviços de recuperação de saudação.</span><span class="sxs-lookup"><span data-stu-id="edb27-114">hello Hyper-V site is registered in hello Recovery Services vault.</span></span>

## <a name="next-steps"></a><span data-ttu-id="edb27-115">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="edb27-115">Next steps</span></span>

<span data-ttu-id="edb27-116">Vá muito[etapa 7: criar um cofre](hyper-v-site-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="edb27-116">Go too[Step 7: Create a vault](hyper-v-site-walkthrough-create-vault.md)</span></span>

