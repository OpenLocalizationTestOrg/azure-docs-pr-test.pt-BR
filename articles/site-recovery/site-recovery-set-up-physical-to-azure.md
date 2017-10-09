---
title: "Configurar o ambiente de origem da saudação (tooAzure servidores físicos) | Microsoft Docs"
description: "Este artigo descreve como tooset o seu toostart do ambiente local replicando servidores físicos executando o Windows ou Linux no Azure."
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
ms.openlocfilehash: d4702265bf36910015685d2bba99d6e577531bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-physical-server-tooazure"></a><span data-ttu-id="74253-103">Configurar o ambiente de origem da saudação (servidor físico tooAzure)</span><span class="sxs-lookup"><span data-stu-id="74253-103">Set up hello source environment (physical server tooAzure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="74253-104">VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="74253-104">VMware tooAzure</span></span>](./site-recovery-set-up-vmware-to-azure.md)
> * [<span data-ttu-id="74253-105">TooAzure físico</span><span class="sxs-lookup"><span data-stu-id="74253-105">Physical tooAzure</span></span>](./site-recovery-set-up-physical-to-azure.md)

<span data-ttu-id="74253-106">Este artigo descreve como tooset o seu toostart do ambiente local replicando servidores físicos executando o Windows ou Linux no Azure.</span><span class="sxs-lookup"><span data-stu-id="74253-106">This article describes how tooset up your on-premises environment toostart replicating physical servers running Windows or Linux into Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74253-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="74253-107">Prerequisites</span></span>

<span data-ttu-id="74253-108">artigo de saudação pressupõe que você já tem:</span><span class="sxs-lookup"><span data-stu-id="74253-108">hello article assumes that you already have:</span></span>
1. <span data-ttu-id="74253-109">Um cofre de serviços de recuperação no hello [portal do Azure](http://portal.azure.com "portal do Azure").</span><span class="sxs-lookup"><span data-stu-id="74253-109">A Recovery Services vault in hello [Azure portal](http://portal.azure.com "Azure portal").</span></span>
3. <span data-ttu-id="74253-110">Um computador físico no qual servidor de configuração de saudação tooinstall.</span><span class="sxs-lookup"><span data-stu-id="74253-110">A physical computer on which tooinstall hello configuration server.</span></span>

### <a name="configuration-server-minimum-requirements"></a><span data-ttu-id="74253-111">Requisitos mínimos do servidor de configuração</span><span class="sxs-lookup"><span data-stu-id="74253-111">Configuration server minimum requirements</span></span>
<span data-ttu-id="74253-112">Olá a tabela a seguir lista o hardware mínimo hello, software e requisitos de rede para um servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="74253-112">hello following table lists hello minimum hardware, software, and network requirements for a configuration server.</span></span>
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> <span data-ttu-id="74253-113">Servidores proxy baseado em HTTPS não são suportados pelo servidor de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="74253-113">HTTPS-based proxy servers are not supported by hello configuration server.</span></span>

## <a name="choose-your-protection-goals"></a><span data-ttu-id="74253-114">Escolher as metas de proteção</span><span class="sxs-lookup"><span data-stu-id="74253-114">Choose your protection goals</span></span>

1. <span data-ttu-id="74253-115">No portal do Azure de Olá, vá toohello **dos serviços de recuperação** cofres de folha e selecione seu cofre.</span><span class="sxs-lookup"><span data-stu-id="74253-115">In hello Azure portal, go toohello **Recovery Services** vaults blade and select your vault.</span></span>
2. <span data-ttu-id="74253-116">Em Olá **recurso** menu do cofre hello, clique em **Introdução** > **recuperação de Site** > **etapa 1: preparar Infraestrutura** > **objetivo de proteção**.</span><span class="sxs-lookup"><span data-stu-id="74253-116">In hello **Resource** menu of hello vault, click **Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>

    ![Escolher metas](./media/site-recovery-set-up-physical-to-azure/choose-goals.png)
3. <span data-ttu-id="74253-118">Em **objetivo de proteção**, selecione **tooAzure** e **não virtualizados/outros**e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="74253-118">In **Protection goal**, select **tooAzure** and **Not virtualized/Other**, and then click **OK**.</span></span>

    ![Escolher metas](./media/site-recovery-set-up-physical-to-azure/physical-protection-goal.PNG)

## <a name="set-up-hello-source-environment"></a><span data-ttu-id="74253-120">Configurar o ambiente de origem Olá</span><span class="sxs-lookup"><span data-stu-id="74253-120">Set up hello source environment</span></span>

1. <span data-ttu-id="74253-121">Em **preparar fonte**, se você não tiver um servidor de configuração, clique em **+ servidor de configuração** tooadd um.</span><span class="sxs-lookup"><span data-stu-id="74253-121">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** tooadd one.</span></span>

  ![Configurar origem](./media/site-recovery-set-up-physical-to-azure/plus-config-srv.png)
2. <span data-ttu-id="74253-123">Em Olá **Adicionar servidor** folha, verifique se **servidor de configuração** aparece na **tipo de servidor**.</span><span class="sxs-lookup"><span data-stu-id="74253-123">In hello **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="74253-124">Baixe o arquivo de instalação de configuração do Site Recovery unificado de hello.</span><span class="sxs-lookup"><span data-stu-id="74253-124">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="74253-125">Baixe a chave de registro de cofre hello.</span><span class="sxs-lookup"><span data-stu-id="74253-125">Download hello vault registration key.</span></span> <span data-ttu-id="74253-126">Você precisa chave de registro de hello quando você executa a instalação unificado.</span><span class="sxs-lookup"><span data-stu-id="74253-126">You need hello registration key when you run Unified Setup.</span></span> <span data-ttu-id="74253-127">chave de saudação é válida por cinco dias depois que ele é gerado.</span><span class="sxs-lookup"><span data-stu-id="74253-127">hello key is valid for five days after you generate it.</span></span>

    ![Configurar origem](./media/site-recovery-set-up-physical-to-azure/set-source2.png)
6. <span data-ttu-id="74253-129">No computador de saudação estiver usando como o servidor de configuração hello, execute **instalação unificado do Azure Site Recovery** mestre de Olá, servidor de processo Olá e servidor de configuração de saudação tooinstall o servidor de destino.</span><span class="sxs-lookup"><span data-stu-id="74253-129">On hello machine you’re using as hello configuration server, run **Azure Site Recovery Unified Setup** tooinstall hello configuration server, hello process server, and hello master target server.</span></span>

#### <a name="run-azure-site-recovery-unified-setup"></a><span data-ttu-id="74253-130">Executar a Configuração Unificada do Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="74253-130">Run Azure Site Recovery Unified Setup</span></span>

> [!TIP]
> <span data-ttu-id="74253-131">Registro do servidor de configuração falhará se o tempo de saudação no relógio do sistema do computador é mais de cinco minutos da hora local.</span><span class="sxs-lookup"><span data-stu-id="74253-131">Configuration server registration fails if hello time on your computer's system clock is more than five minutes off of local time.</span></span> <span data-ttu-id="74253-132">Sincronizar o relógio do sistema com uma [tempo server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) antes de iniciar a instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="74253-132">Synchronize your system clock with a [time server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) before starting hello installation.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="74253-133">servidor de configuração de saudação pode ser instalado por meio de uma linha de comando.</span><span class="sxs-lookup"><span data-stu-id="74253-133">hello configuration server can be installed via a command line.</span></span> <span data-ttu-id="74253-134">Para obter mais informações, confira [Instalando o servidor de configuração usando ferramentas de linhas de comando](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="74253-134">For more information, see [Installing configuration server using command-line tools](http://aka.ms/installconfigsrv).</span></span>


## <a name="common-issues"></a><span data-ttu-id="74253-135">Problemas comuns</span><span class="sxs-lookup"><span data-stu-id="74253-135">Common issues</span></span>

[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a><span data-ttu-id="74253-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="74253-136">Next steps</span></span>

<span data-ttu-id="74253-137">A próxima etapa envolve a [configuração do ambiente de destino](./site-recovery-prepare-target-physical-to-azure.md) no Azure.</span><span class="sxs-lookup"><span data-stu-id="74253-137">Next step involves [setting up your target environment](./site-recovery-prepare-target-physical-to-azure.md) in Azure.</span></span>
