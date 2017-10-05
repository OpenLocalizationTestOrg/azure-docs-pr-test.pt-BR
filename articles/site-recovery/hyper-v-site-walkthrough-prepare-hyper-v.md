---
title: "Preparar os hosts Hyper-V (sem o System Center VMM) para replicação para o Azure | Microsoft Docs"
description: "Descreve como preparar os hosts Hyper-V para replicação para o Azure usando o Azure Site Recovery"
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
ms.openlocfilehash: f9bcaa8e55be6e8fddaf88ebc3f18f5dbb2811e4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="step-6-prepare-hyper-v-hosts-for-replication-to-azure"></a><span data-ttu-id="15863-103">Etapa 6: Preparar os hosts Hyper-V para replicação para o Azure</span><span class="sxs-lookup"><span data-stu-id="15863-103">Step 6: Prepare Hyper-V hosts for replication to Azure</span></span>

<span data-ttu-id="15863-104">Use as instruções deste artigo para preparar os hosts Hyper-V locais para interagir com o Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="15863-104">Use the instructions in this article to prepare on-premises Hyper-V hosts to interact with Azure Site Recovery.</span></span>

<span data-ttu-id="15863-105">Depois de ler este artigo, poste comentários no final ou faça perguntas técnicas no [Fórum dos Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="15863-105">After reading this article, post any comments at the bottom, or ask technical questions on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prepare-hosts"></a><span data-ttu-id="15863-106">Preparar os hosts</span><span class="sxs-lookup"><span data-stu-id="15863-106">Prepare hosts</span></span>

- <span data-ttu-id="15863-107">Verifique se os hosts do Hyper-V satisfazem os [pré-requisitos](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).</span><span class="sxs-lookup"><span data-stu-id="15863-107">Make sure that the Hyper-V hosts meet the [prerequisites](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).</span></span>
- <span data-ttu-id="15863-108">Verifique se os hosts podem acessar as URLs necessárias:</span><span class="sxs-lookup"><span data-stu-id="15863-108">Make sure that the hosts can access the required URLs:</span></span>

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- <span data-ttu-id="15863-109">Se tiver regras de firewall baseadas no endereço IP, verifique se elas permitem a comunicação com o Azure.</span><span class="sxs-lookup"><span data-stu-id="15863-109">If you have IP address-based firewall rules, ensure they allow communication to Azure.</span></span>
- <span data-ttu-id="15863-110">Permita os [Intervalos de IP do Datacenter do Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) e a porta HTTPS (443).</span><span class="sxs-lookup"><span data-stu-id="15863-110">Allow the [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and the HTTPS (443) port.</span></span>
- <span data-ttu-id="15863-111">Permita os intervalos de endereços IP para a região do Azure da sua assinatura e para o Oeste dos EUA (usados para Controle de Acesso e Gerenciamento de Identidade).</span><span class="sxs-lookup"><span data-stu-id="15863-111">Allow IP address ranges for the Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

<span data-ttu-id="15863-112">Durante a implantação do Site Recovery, você adiciona hosts Hyper-V que contêm VMs que você deseja replicar para um site do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="15863-112">During Site Recovery deployment, you add Hyper-V hosts that contain VMs you want to replicate to a Hyper-V site.</span></span> <span data-ttu-id="15863-113">O Provedor do Site Recovery e o agente dos Serviços de Recuperação são instalados em cada host.</span><span class="sxs-lookup"><span data-stu-id="15863-113">The Site Recovery Provider, and Recovery Services agent are installed on each host.</span></span> <span data-ttu-id="15863-114">O site do Hyper-V é registrado no cofre dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="15863-114">The Hyper-V site is registered in the Recovery Services vault.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15863-115">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="15863-115">Next steps</span></span>

<span data-ttu-id="15863-116">Vá para a [Etapa 7: Criar um cofre](hyper-v-site-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="15863-116">Go to [Step 7: Create a vault](hyper-v-site-walkthrough-create-vault.md)</span></span>

