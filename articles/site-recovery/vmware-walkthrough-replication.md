---
title: "aaaSet uma política de replicação para tooAzure de replicação de VM do VMware com o Azure Site Recovery | Microsoft Docs"
description: "Resume as etapas de saudação tooset uma política de replicação é necessário ao replicar máquinas virtuais do VMware tooAzure armazenamento"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d7874bd8-6626-4668-9ec9-dbd2d26f8f81
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 12870f3f98a4dd412221b817581403cd4bf7a76d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-set-up-a-replication-policy-for-vmware-vm-replication-tooazure"></a><span data-ttu-id="6397f-103">Etapa 9: Configurar uma política de replicação para tooAzure de replicação de VM do VMware</span><span class="sxs-lookup"><span data-stu-id="6397f-103">Step 9: Set up a replication policy for VMware VM replication tooAzure</span></span>


<span data-ttu-id="6397f-104">Este artigo descreve como tooset uma política de replicação quando você estiver replicando máquinas virtuais do VMware tooAzure usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6397f-104">This article describes how tooset up a replication policy when you're replicating VMware VMs tooAzure using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>


<span data-ttu-id="6397f-105">Postar perguntas e comentários na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="6397f-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="configure-a-policy"></a><span data-ttu-id="6397f-106">Configurar uma política</span><span class="sxs-lookup"><span data-stu-id="6397f-106">Configure a policy</span></span>

<span data-ttu-id="6397f-107">Obtenha uma rápida visão geral em vídeo antes de começar:</span><span class="sxs-lookup"><span data-stu-id="6397f-107">Get a quick video overview before you start:</span></span>
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. <span data-ttu-id="6397f-108">toocreate uma nova política de replicação, clique em **infra-estrutura de recuperação de Site** > **políticas de replicação** > **+ política de replicação**.</span><span class="sxs-lookup"><span data-stu-id="6397f-108">toocreate a new replication policy, click **Site Recovery infrastructure** > **Replication Policies** > **+Replication Policy**.</span></span>
2. <span data-ttu-id="6397f-109">Em **Criar política de replicação**, especifique um nome de política.</span><span class="sxs-lookup"><span data-stu-id="6397f-109">In **Create replication policy**, specify a policy name.</span></span>
3. <span data-ttu-id="6397f-110">Em **limite de RPO**, especifique o limite RPO hello.</span><span class="sxs-lookup"><span data-stu-id="6397f-110">In **RPO threshold**, specify hello RPO limit.</span></span> <span data-ttu-id="6397f-111">Esse valor especifica com que frequência os pontos de recuperação de dados são criados.</span><span class="sxs-lookup"><span data-stu-id="6397f-111">This value specifies how often data recovery points are created.</span></span> <span data-ttu-id="6397f-112">Um alerta será gerado se a replicação contínua exceder esse limite.</span><span class="sxs-lookup"><span data-stu-id="6397f-112">An alert is generated if continuous replication exceeds this limit.</span></span>
4. <span data-ttu-id="6397f-113">Em **retenção de ponto de recuperação**, especifique quanto tempo (em horas) é uma janela de retenção Olá para cada ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="6397f-113">In **Recovery point retention**, specify (in hours) how long hello retention window is for each recovery point.</span></span> <span data-ttu-id="6397f-114">Máquinas virtuais replicadas podem ser recuperados tooany ponto em uma janela.</span><span class="sxs-lookup"><span data-stu-id="6397f-114">Replicated VMs can be recovered tooany point in a window.</span></span> <span data-ttu-id="6397f-115">A retenção horas tem suporte para máquinas de too24 replicado toopremium armazenamento e 72 horas para o armazenamento padrão.</span><span class="sxs-lookup"><span data-stu-id="6397f-115">Up too24 hours retention is supported for machines replicated toopremium storage, and 72 hours for standard storage.</span></span>
5. <span data-ttu-id="6397f-116">Em **Frequência do instantâneo consistente com o aplicativo**, especifique com que frequência (em minutos) os pontos de recuperação contendo instantâneos consistentes com aplicativos serão criados.</span><span class="sxs-lookup"><span data-stu-id="6397f-116">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="6397f-117">Clique em **Okey** toocreate política de saudação.</span><span class="sxs-lookup"><span data-stu-id="6397f-117">Click **OK** toocreate hello policy.</span></span>

    ![Política de replicação](./media/vmware-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="6397f-119">Quando você cria uma nova política automaticamente associado com o servidor de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="6397f-119">When you create a new policy it's automatically associated with hello configuration server.</span></span> <span data-ttu-id="6397f-120">Por padrão, uma política de correspondência é criada automaticamente para failback.</span><span class="sxs-lookup"><span data-stu-id="6397f-120">By default, a matching policy is automatically created for failback.</span></span> <span data-ttu-id="6397f-121">Por exemplo, se hello política de replicação é **política rep** diretiva de failback hello serão **representante de diretiva de failback**.</span><span class="sxs-lookup"><span data-stu-id="6397f-121">For example, if hello replication policy is **rep-policy** then hello failback policy will be **rep-policy-failback**.</span></span> <span data-ttu-id="6397f-122">Essa política não é usada até você iniciar um failback do Azure.</span><span class="sxs-lookup"><span data-stu-id="6397f-122">This policy isn't used until you initiate a failback from Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6397f-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6397f-123">Next steps</span></span>

<span data-ttu-id="6397f-124">Vá muito[etapa 10: instalar o serviço de mobilidade Olá](vmware-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="6397f-124">Go too[Step 10: Install hello Mobility service](vmware-walkthrough-install-mobility.md)</span></span>
