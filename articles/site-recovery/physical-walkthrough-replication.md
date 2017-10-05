---
title: "Configurar uma política de replicação para a replicação de servidor físico para o Azure com o Azure Site Recovery | Microsoft Docs"
description: "Resume as etapas necessárias para configurar uma política de replicação durante a replicação de servidores físicos locais para o armazenamento do Azure usando o serviço Azure Site Recovery"
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
ms.openlocfilehash: 9ce23382001b54e7b9b7a58b8dd9aa61b400826d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="step-8-set-up-a-replication-policy-for-physical-server-replication-to-azure"></a><span data-ttu-id="0bfc8-103">Etapa 8: Configurar uma política de replicação para a replicação de servidor físico para o Azure</span><span class="sxs-lookup"><span data-stu-id="0bfc8-103">Step 8: Set up a replication policy for physical server replication to Azure</span></span>


<span data-ttu-id="0bfc8-104">Este artigo descreve como configurar uma política de replicação quando você estiver replicando servidores físicos Windows/Linux para o Azure usando o serviço [Azure Site Recovery](site-recovery-overview.md) no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0bfc8-104">This article describes how to set up a replication policy when you're replicating Windows/Linux physical servers to Azure using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>


<span data-ttu-id="0bfc8-105">Poste perguntas e comentários na parte inferior deste artigo ou no [Fórum de Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="0bfc8-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="configure-a-policy"></a><span data-ttu-id="0bfc8-106">Configurar uma política</span><span class="sxs-lookup"><span data-stu-id="0bfc8-106">Configure a policy</span></span>

1. <span data-ttu-id="0bfc8-107">Clique em **Infraestrutura do Site Recovery** > **Políticas de Replicação** > **+Política de Replicação**.</span><span class="sxs-lookup"><span data-stu-id="0bfc8-107">Click **Site Recovery infrastructure** > **Replication Policies** > **+Replication Policy**.</span></span>
2. <span data-ttu-id="0bfc8-108">Em **Criar política de replicação**, especifique um nome de política.</span><span class="sxs-lookup"><span data-stu-id="0bfc8-108">In **Create replication policy**, specify a policy name.</span></span>
3. <span data-ttu-id="0bfc8-109">Em **Limite de RPO**, especifique o limite de RPO.</span><span class="sxs-lookup"><span data-stu-id="0bfc8-109">In **RPO threshold**, specify the RPO limit.</span></span> <span data-ttu-id="0bfc8-110">Esse valor indica com que frequência os pontos de recuperação de dados são criados.</span><span class="sxs-lookup"><span data-stu-id="0bfc8-110">This value indicates how often data recovery points are created.</span></span> <span data-ttu-id="0bfc8-111">Um alerta será gerado se a replicação contínua exceder esse limite.</span><span class="sxs-lookup"><span data-stu-id="0bfc8-111">An alert is generated if continuous replication exceeds this limit.</span></span>
4. <span data-ttu-id="0bfc8-112">Em **Retenção do ponto de recuperação**, especifique (em horas) qual será a duração da janela de retenção para cada ponto de recuperação.</span><span class="sxs-lookup"><span data-stu-id="0bfc8-112">In **Recovery point retention**, specify (in hours) how long the retention window is for each recovery point.</span></span> <span data-ttu-id="0bfc8-113">VMs replicadas podem ser recuperadas para qualquer ponto em uma janela.</span><span class="sxs-lookup"><span data-stu-id="0bfc8-113">Replicated VMs can be recovered to any point in a window.</span></span> <span data-ttu-id="0bfc8-114">Há suporte para retenção de até 24 horas para máquinas replicadas para armazenamento premium e 72 horas para o armazenamento padrão.</span><span class="sxs-lookup"><span data-stu-id="0bfc8-114">Up to 24 hours retention is supported for machines replicated to premium storage, and 72 hours for standard storage.</span></span>
5. <span data-ttu-id="0bfc8-115">Em **Frequência do instantâneo consistente com o aplicativo**, especifique com que frequência (em minutos) os pontos de recuperação contendo instantâneos consistentes com aplicativos serão criados.</span><span class="sxs-lookup"><span data-stu-id="0bfc8-115">In **App-consistent snapshot frequency**, specify how often (in minutes) recovery points containing application-consistent snapshots will be created.</span></span> <span data-ttu-id="0bfc8-116">Clique em **OK** para criar a política.</span><span class="sxs-lookup"><span data-stu-id="0bfc8-116">Click **OK** to create the policy.</span></span>

    ![Política de replicação](./media/physical-walkthrough-replication/gs-replication2.png)
8. <span data-ttu-id="0bfc8-118">Quando você cria uma nova política, ela é automaticamente associada ao servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="0bfc8-118">When you create a new policy it's automatically associated with the configuration server.</span></span> <span data-ttu-id="0bfc8-119">Por padrão, uma política de correspondência é criada automaticamente para failback.</span><span class="sxs-lookup"><span data-stu-id="0bfc8-119">By default, a matching policy is automatically created for failback.</span></span> <span data-ttu-id="0bfc8-120">Por exemplo, se a política de replicação for **rep-policy**, a política de failback será **rep-policy-failback**.</span><span class="sxs-lookup"><span data-stu-id="0bfc8-120">For example, if the replication policy is **rep-policy** then the failback policy will be **rep-policy-failback**.</span></span> <span data-ttu-id="0bfc8-121">Essa política não é usada até você iniciar um failback do Azure.</span><span class="sxs-lookup"><span data-stu-id="0bfc8-121">This policy isn't used until you initiate a failback from Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0bfc8-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0bfc8-122">Next steps</span></span>

<span data-ttu-id="0bfc8-123">Ir para a [Etapa 9: Instalar o Serviço de mobilidade](physical-walkthrough-install-mobility.md)</span><span class="sxs-lookup"><span data-stu-id="0bfc8-123">Go to [Step 9: Install the Mobility service](physical-walkthrough-install-mobility.md)</span></span>
