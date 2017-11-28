---
title: "aaaPrepare System Center VMM para tooAzure de replicação do Hyper-V | Microsoft Docs"
description: "Descreve como servidor do System Center VMM tooprepare para tooAzure de replicação do Hyper-V, usando o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: afcd81ae-d192-4013-a0af-3dac45b3c7e9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 773b06afaf7d3eea1fe64f050bf3970943cf466a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-vmm-servers-and-hyper-v-hosts-for-hyper-v-replication-tooazure"></a><span data-ttu-id="62e12-103">Etapa 6: Preparar os servidores do VMM e hosts Hyper-V para tooAzure de replicação do Hyper-V</span><span class="sxs-lookup"><span data-stu-id="62e12-103">Step 6: Prepare VMM servers and Hyper-V hosts for Hyper-V replication tooAzure</span></span>

<span data-ttu-id="62e12-104">Depois de configurar o [componentes do Azure](vmm-to-azure-walkthrough-prepare-azure.md) para implantação de hello, use instruções Olá nesse toointeract de hosts do Hyper-V e servidores do artigo tooprepare locais do VMM com o Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="62e12-104">After setting up [Azure components](vmm-to-azure-walkthrough-prepare-azure.md) for hello deployment, use hello instructions in this article tooprepare on-premises VMM servers and Hyper-V hosts toointeract with Azure Site Recovery.</span></span>

<span data-ttu-id="62e12-105">Depois de ler este artigo, postar os comentários na parte inferior da saudação ou questões técnicas Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="62e12-105">After reading this article, post any comments at hello bottom, or ask technical questions on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="prepare-vmm-servers"></a><span data-ttu-id="62e12-106">Preparar servidores VMM</span><span class="sxs-lookup"><span data-stu-id="62e12-106">Prepare VMM servers</span></span>

- <span data-ttu-id="62e12-107">É necessário pelo menos um servidor do VMM que atendem aos requisitos de suporte de saudação para replicação de recuperação de Site (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).</span><span class="sxs-lookup"><span data-stu-id="62e12-107">You need at least one VMM server that meet hello support requirements for Site Recovery replication (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).</span></span>
- <span data-ttu-id="62e12-108">Certifique-se que você preparou o servidor do VMM Olá para [mapeamento de rede](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span><span class="sxs-lookup"><span data-stu-id="62e12-108">Make sure you've prepared hello VMM server for [network mapping](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).</span></span>
- <span data-ttu-id="62e12-109">Verifique se o que servidor VMM Olá pode acessar essas URLs</span><span class="sxs-lookup"><span data-stu-id="62e12-109">Make sure that hello VMM server can access these URLs</span></span>

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- <span data-ttu-id="62e12-110">Se você tiver regras de firewall baseado em endereço IP, certifique-se de que permitem comunicação tooAzure.</span><span class="sxs-lookup"><span data-stu-id="62e12-110">If you have IP address-based firewall rules, ensure they allow communication tooAzure.</span></span>
- <span data-ttu-id="62e12-111">Permitir Olá [intervalos de IP de Datacenter do Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)e hello porta HTTPS (443).</span><span class="sxs-lookup"><span data-stu-id="62e12-111">Allow hello [Azure Datacenter IP Ranges](https://www.microsoft.com/download/confirmation.aspx?id=41653), and hello HTTPS (443) port.</span></span>
- <span data-ttu-id="62e12-112">Permitir que os intervalos de endereços IP para Olá região do Azure de sua assinatura e Oeste dos EUA (usado para gerenciamento de identidade e controle de acesso).</span><span class="sxs-lookup"><span data-stu-id="62e12-112">Allow IP address ranges for hello Azure region of your subscription, and for West US (used for Access Control and Identity Management).</span></span>

<span data-ttu-id="62e12-113">Durante a implantação da recuperação de Site, você baixar Olá provedor de recuperação de Site e instale-o em cada servidor do VMM.</span><span class="sxs-lookup"><span data-stu-id="62e12-113">During Site Recovery deployment, you download hello Site Recovery Provider and install it on each VMM server.</span></span> <span data-ttu-id="62e12-114">servidor do VMM Hello está registrado no cofre de serviços de recuperação de saudação.</span><span class="sxs-lookup"><span data-stu-id="62e12-114">hello VMM server is registered in hello Recovery Services vault.</span></span>




## <a name="next-steps"></a><span data-ttu-id="62e12-115">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="62e12-115">Next steps</span></span>

<span data-ttu-id="62e12-116">Vá muito[etapa 7: criar um cofre](vmm-to-azure-walkthrough-create-vault.md)</span><span class="sxs-lookup"><span data-stu-id="62e12-116">Go too[Step 7: Create a vault](vmm-to-azure-walkthrough-create-vault.md)</span></span>

