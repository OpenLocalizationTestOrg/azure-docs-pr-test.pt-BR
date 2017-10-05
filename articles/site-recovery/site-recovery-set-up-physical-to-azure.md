---
title: "Configurar o ambiente de origem (servidores físicos para Azure) | Microsoft Docs"
description: "Este artigo descreve como configurar seu ambiente local para iniciar a replicação de servidores físicos executando Windows ou Linux no Azure."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 49b9d2e21dbcb612828a25f21ed4382327d6f64c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-the-source-environment-physical-server-to-azure"></a><span data-ttu-id="5c729-103">Configurar o ambiente de origem (servidor físico para Azure)</span><span class="sxs-lookup"><span data-stu-id="5c729-103">Set up the source environment (physical server to Azure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5c729-104">VMware no Azure</span><span class="sxs-lookup"><span data-stu-id="5c729-104">VMware to Azure</span></span>](./site-recovery-set-up-vmware-to-azure.md)
> * [<span data-ttu-id="5c729-105">Físico para Azure</span><span class="sxs-lookup"><span data-stu-id="5c729-105">Physical to Azure</span></span>](./site-recovery-set-up-physical-to-azure.md)

<span data-ttu-id="5c729-106">Este artigo descreve como configurar seu ambiente local para iniciar a replicação de servidores físicos executando Windows ou Linux no Azure.</span><span class="sxs-lookup"><span data-stu-id="5c729-106">This article describes how to set up your on-premises environment to start replicating physical servers running Windows or Linux into Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c729-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5c729-107">Prerequisites</span></span>

<span data-ttu-id="5c729-108">O artigo supõe que você já tenha:</span><span class="sxs-lookup"><span data-stu-id="5c729-108">The article assumes that you already have:</span></span>
1. <span data-ttu-id="5c729-109">Um cofre de Serviços de Recuperação no [Portal do Azure](http://portal.azure.com "Portal do Azure").</span><span class="sxs-lookup"><span data-stu-id="5c729-109">A Recovery Services vault in the [Azure portal](http://portal.azure.com "Azure portal").</span></span>
3. <span data-ttu-id="5c729-110">Um computador físico no qual instalar o servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="5c729-110">A physical computer on which to install the configuration server.</span></span>

### <a name="configuration-server-minimum-requirements"></a><span data-ttu-id="5c729-111">Requisitos mínimos do servidor de configuração</span><span class="sxs-lookup"><span data-stu-id="5c729-111">Configuration server minimum requirements</span></span>
<span data-ttu-id="5c729-112">A tabela a seguir lista os requisitos mínimos de hardware, software e rede para um servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="5c729-112">The following table lists the minimum hardware, software, and network requirements for a configuration server.</span></span>
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> <span data-ttu-id="5c729-113">Os servidores proxy baseados em HTTPS não são compatíveis com o servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="5c729-113">HTTPS-based proxy servers are not supported by the configuration server.</span></span>

## <a name="choose-your-protection-goals"></a><span data-ttu-id="5c729-114">Escolher as metas de proteção</span><span class="sxs-lookup"><span data-stu-id="5c729-114">Choose your protection goals</span></span>

1. <span data-ttu-id="5c729-115">No Portal do Azure, vá até a folha de cofres dos **Serviços de Recuperação** e selecione seu cofre.</span><span class="sxs-lookup"><span data-stu-id="5c729-115">In the Azure portal, go to the **Recovery Services** vaults blade and select your vault.</span></span>
2. <span data-ttu-id="5c729-116">No menu **Recurso** do cofre, clique em **Introdução** > **Site Recovery** > **Etapa 1: Preparar Infraestrutura** > **Meta de proteção**.</span><span class="sxs-lookup"><span data-stu-id="5c729-116">In the **Resource** menu of the vault, click **Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>

    ![Escolher metas](./media/site-recovery-set-up-physical-to-azure/choose-goals.png)
3. <span data-ttu-id="5c729-118">Em **Meta de proteção**, escolha **Para o Azure** e **Não virtualizado/Outro** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="5c729-118">In **Protection goal**, select **To Azure** and **Not virtualized/Other**, and then click **OK**.</span></span>

    ![Escolher metas](./media/site-recovery-set-up-physical-to-azure/physical-protection-goal.PNG)

## <a name="set-up-the-source-environment"></a><span data-ttu-id="5c729-120">Configurar o ambiente de origem</span><span class="sxs-lookup"><span data-stu-id="5c729-120">Set up the source environment</span></span>

1. <span data-ttu-id="5c729-121">Em **Preparar origem**, se você não tiver um servidor de configuração, clique em **+Servidor de configuração** para adicionar um.</span><span class="sxs-lookup"><span data-stu-id="5c729-121">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** to add one.</span></span>

  ![Configurar origem](./media/site-recovery-set-up-physical-to-azure/plus-config-srv.png)
2. <span data-ttu-id="5c729-123">Na folha **Adicionar Servidor**, verifique se o **Servidor de Configuração** é exibido no **Tipo de servidor**.</span><span class="sxs-lookup"><span data-stu-id="5c729-123">In the **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="5c729-124">Baixe o arquivo de instalação Configuração Unificada da Recuperação de Site.</span><span class="sxs-lookup"><span data-stu-id="5c729-124">Download the Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="5c729-125">Baixe a chave do registro do cofre.</span><span class="sxs-lookup"><span data-stu-id="5c729-125">Download the vault registration key.</span></span> <span data-ttu-id="5c729-126">Você precisa da chave de registro ao executar a Instalação Unificada.</span><span class="sxs-lookup"><span data-stu-id="5c729-126">You need the registration key when you run Unified Setup.</span></span> <span data-ttu-id="5c729-127">A chave é válida por cinco dias após ser gerada.</span><span class="sxs-lookup"><span data-stu-id="5c729-127">The key is valid for five days after you generate it.</span></span>

    ![Configurar origem](./media/site-recovery-set-up-physical-to-azure/set-source2.png)
6. <span data-ttu-id="5c729-129">No computador que você está usando como o servidor de configuração, execute a **Instalação Unificada do Azure Site Recovery** para instalar o servidor de configuração, o servidor de processo e o servidor de destino mestre.</span><span class="sxs-lookup"><span data-stu-id="5c729-129">On the machine you’re using as the configuration server, run **Azure Site Recovery Unified Setup** to install the configuration server, the process server, and the master target server.</span></span>

#### <a name="run-azure-site-recovery-unified-setup"></a><span data-ttu-id="5c729-130">Executar a Configuração Unificada do Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="5c729-130">Run Azure Site Recovery Unified Setup</span></span>

> [!TIP]
> <span data-ttu-id="5c729-131">O registro do servidor de configuração falhará se o relógio do sistema do computador estiver com uma diferença de mais de cinco minutos da hora local.</span><span class="sxs-lookup"><span data-stu-id="5c729-131">Configuration server registration fails if the time on your computer's system clock is more than five minutes off of local time.</span></span> <span data-ttu-id="5c729-132">Sincronize o relógio do sistema com um [servidor de horário](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) antes de iniciar a instalação.</span><span class="sxs-lookup"><span data-stu-id="5c729-132">Synchronize your system clock with a [time server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) before starting the installation.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="5c729-133">O servidor de configuração pode ser instalado por meio de uma linha de comando.</span><span class="sxs-lookup"><span data-stu-id="5c729-133">The configuration server can be installed via a command line.</span></span> <span data-ttu-id="5c729-134">Para obter mais informações, confira [Instalando o servidor de configuração usando ferramentas de linhas de comando](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="5c729-134">For more information, see [Installing configuration server using command-line tools](http://aka.ms/installconfigsrv).</span></span>


## <a name="common-issues"></a><span data-ttu-id="5c729-135">Problemas comuns</span><span class="sxs-lookup"><span data-stu-id="5c729-135">Common issues</span></span>

[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a><span data-ttu-id="5c729-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5c729-136">Next steps</span></span>

<span data-ttu-id="5c729-137">A próxima etapa envolve a [configuração do ambiente de destino](./site-recovery-prepare-target-physical-to-azure.md) no Azure.</span><span class="sxs-lookup"><span data-stu-id="5c729-137">Next step involves [setting up your target environment](./site-recovery-prepare-target-physical-to-azure.md) in Azure.</span></span>
