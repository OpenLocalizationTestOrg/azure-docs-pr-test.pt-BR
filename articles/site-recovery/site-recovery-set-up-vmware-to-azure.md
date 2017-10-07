---
title: "Configurar o ambiente de origem da saudação (VMware tooAzure) | Microsoft Docs"
description: "Este artigo descreve como tooset o seu toostart do ambiente local replicando o VMware virtual máquinas tooAzure."
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
ms.openlocfilehash: cbeeffc1061b11223e12ff3e237fa7e55b999aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-vmware-tooazure"></a><span data-ttu-id="9b7cc-103">Configurar o ambiente de origem da saudação (tooAzure VMware)</span><span class="sxs-lookup"><span data-stu-id="9b7cc-103">Set up hello source environment (VMware tooAzure)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9b7cc-104">VMware tooAzure</span><span class="sxs-lookup"><span data-stu-id="9b7cc-104">VMware tooAzure</span></span>](./site-recovery-set-up-vmware-to-azure.md)
> * [<span data-ttu-id="9b7cc-105">TooAzure físico</span><span class="sxs-lookup"><span data-stu-id="9b7cc-105">Physical tooAzure</span></span>](./site-recovery-set-up-physical-to-azure.md)

<span data-ttu-id="9b7cc-106">Este artigo descreve como tooset o seu toostart do ambiente local replicando virtual máquinas em execução no VMware tooAzure.</span><span class="sxs-lookup"><span data-stu-id="9b7cc-106">This article describes how tooset up your on-premises environment toostart replicating virtual machines running on VMware tooAzure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b7cc-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9b7cc-107">Prerequisites</span></span>

<span data-ttu-id="9b7cc-108">artigo de saudação pressupõe que você já tenha criado:</span><span class="sxs-lookup"><span data-stu-id="9b7cc-108">hello article assumes that you have already created:</span></span>
- <span data-ttu-id="9b7cc-109">Um cofre de serviços de recuperação Olá [portal do Azure](http://portal.azure.com "portal do Azure").</span><span class="sxs-lookup"><span data-stu-id="9b7cc-109">A Recovery Services Vault in hello [Azure portal](http://portal.azure.com "Azure portal").</span></span>
- <span data-ttu-id="9b7cc-110">Uma conta dedicada no seu VMware vCenter que pode ser usada para [descoberta automática](./site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="9b7cc-110">A dedicated account in your VMware vCenter that can be used for [automatic discovery](./site-recovery-vmware-to-azure.md).</span></span>
- <span data-ttu-id="9b7cc-111">Uma máquina virtual no qual servidor de configuração de saudação tooinstall.</span><span class="sxs-lookup"><span data-stu-id="9b7cc-111">A virtual machine on which tooinstall hello configuration server.</span></span>

## <a name="configuration-server-minimum-requirements"></a><span data-ttu-id="9b7cc-112">Requisitos mínimos do servidor de configuração</span><span class="sxs-lookup"><span data-stu-id="9b7cc-112">Configuration server minimum requirements</span></span>
<span data-ttu-id="9b7cc-113">software de servidor de configuração de saudação deve ser implantado em uma máquina virtual de VMware altamente disponível.</span><span class="sxs-lookup"><span data-stu-id="9b7cc-113">hello configuration server software should be deployed on a highly available VMware virtual machine.</span></span> <span data-ttu-id="9b7cc-114">Olá a tabela a seguir lista o hardware mínimo hello, software e requisitos de rede para um servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="9b7cc-114">hello following table lists hello minimum hardware, software, and network requirements for a configuration server.</span></span>
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> <span data-ttu-id="9b7cc-115">Servidores proxy baseado em HTTPS não são suportados pelo servidor de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b7cc-115">HTTPS-based proxy servers are not supported by hello configuration server.</span></span>

## <a name="choose-your-protection-goals"></a><span data-ttu-id="9b7cc-116">Escolher as metas de proteção</span><span class="sxs-lookup"><span data-stu-id="9b7cc-116">Choose your protection goals</span></span>

1. <span data-ttu-id="9b7cc-117">No portal do Azure de Olá, vá toohello **dos serviços de recuperação** cofre folha e selecione seu cofre.</span><span class="sxs-lookup"><span data-stu-id="9b7cc-117">In hello Azure portal, go toohello **Recovery Services** vault blade and select your vault.</span></span>
2. <span data-ttu-id="9b7cc-118">No menu de recursos de saudação do cofre hello, ir muito**Introdução** > **recuperação de Site** > **etapa 1: preparar a infraestrutura**  >  **Objetivo de proteção**.</span><span class="sxs-lookup"><span data-stu-id="9b7cc-118">On hello resource menu of hello vault, go too**Getting Started** > **Site Recovery** > **Step 1: Prepare Infrastructure** > **Protection goal**.</span></span>

    ![Escolher metas](./media/site-recovery-set-up-vmware-to-azure/choose-goals.png)
3. <span data-ttu-id="9b7cc-120">Em **objetivo de proteção**, selecione **tooAzure**e escolha **Sim, com VMware vSphere hipervisor**.</span><span class="sxs-lookup"><span data-stu-id="9b7cc-120">In **Protection goal**, select **tooAzure**, and choose **Yes, with VMware vSphere Hypervisor**.</span></span> <span data-ttu-id="9b7cc-121">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="9b7cc-121">Then click **OK**.</span></span>

    ![Escolher metas](./media/site-recovery-set-up-vmware-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a><span data-ttu-id="9b7cc-123">Configurar o ambiente de origem Olá</span><span class="sxs-lookup"><span data-stu-id="9b7cc-123">Set up hello source environment</span></span>
<span data-ttu-id="9b7cc-124">Configurando o ambiente de origem Olá envolve duas atividades principais:</span><span class="sxs-lookup"><span data-stu-id="9b7cc-124">Setting up hello source environment involves two main activities:</span></span>

- <span data-ttu-id="9b7cc-125">Instalar e registrar um servidor de configuração com o Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="9b7cc-125">Install and register a configuration server with Site Recovery.</span></span>
- <span data-ttu-id="9b7cc-126">Descobrir máquinas virtuais locais conectando o Site Recovery tooyour local VMware vCenter ou vSphere EXSi hosts.</span><span class="sxs-lookup"><span data-stu-id="9b7cc-126">Discover your on-premises virtual machines by connecting Site Recovery tooyour on-premises VMware vCenter or vSphere EXSi hosts.</span></span>

### <a name="step-1-install-and-register-a-configuration-server"></a><span data-ttu-id="9b7cc-127">Etapa 1: Instalar e registrar um servidor de configuração</span><span class="sxs-lookup"><span data-stu-id="9b7cc-127">Step 1: Install and register a configuration server</span></span>

1. <span data-ttu-id="9b7cc-128">Clique em **Etapa 1: Preparar a Infraestrutura** > **Origem**.</span><span class="sxs-lookup"><span data-stu-id="9b7cc-128">Click **Step 1: Prepare Infrastructure** > **Source**.</span></span> <span data-ttu-id="9b7cc-129">Em **preparar fonte**, se você não tiver um servidor de configuração, clique em **+ servidor de configuração** tooadd um.</span><span class="sxs-lookup"><span data-stu-id="9b7cc-129">In **Prepare source**, if you don’t have a configuration server, click **+Configuration server** tooadd one.</span></span>

    ![Configurar origem](./media/site-recovery-set-up-vmware-to-azure/set-source1.png)
2. <span data-ttu-id="9b7cc-131">Em Olá **Adicionar servidor** folha, verifique se **servidor de configuração** aparece na **tipo de servidor**.</span><span class="sxs-lookup"><span data-stu-id="9b7cc-131">On hello **Add Server** blade, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="9b7cc-132">Baixe o arquivo de instalação de configuração do Site Recovery unificado de hello.</span><span class="sxs-lookup"><span data-stu-id="9b7cc-132">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="9b7cc-133">Baixe a chave de registro de cofre hello.</span><span class="sxs-lookup"><span data-stu-id="9b7cc-133">Download hello vault registration key.</span></span> <span data-ttu-id="9b7cc-134">Você precisa chave de registro de hello quando você executa a instalação unificado.</span><span class="sxs-lookup"><span data-stu-id="9b7cc-134">You need hello registration key when you run Unified Setup.</span></span> <span data-ttu-id="9b7cc-135">chave de saudação é válida por cinco dias depois que ele é gerado.</span><span class="sxs-lookup"><span data-stu-id="9b7cc-135">hello key is valid for five days after you generate it.</span></span>

    ![Configurar origem](./media/site-recovery-set-up-vmware-to-azure/set-source2.png)
6. <span data-ttu-id="9b7cc-137">No computador de saudação estiver usando como o servidor de configuração hello, execute **instalação unificado do Azure Site Recovery** mestre de Olá, servidor de processo Olá e servidor de configuração de saudação tooinstall o servidor de destino.</span><span class="sxs-lookup"><span data-stu-id="9b7cc-137">On hello machine you’re using as hello configuration server, run **Azure Site Recovery Unified Setup** tooinstall hello configuration server, hello process server, and hello master target server.</span></span>

#### <a name="run-azure-site-recovery-unified-setup"></a><span data-ttu-id="9b7cc-138">Executar a Configuração Unificada do Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="9b7cc-138">Run Azure Site Recovery Unified Setup</span></span>

> [!TIP]
> <span data-ttu-id="9b7cc-139">Registro do servidor de configuração falhará se o tempo de saudação no relógio do sistema do computador difere da hora local em mais de cinco minutos.</span><span class="sxs-lookup"><span data-stu-id="9b7cc-139">Configuration server registration fails if hello time on your computer's system clock differs from local time by more than five minutes.</span></span> <span data-ttu-id="9b7cc-140">Sincronizar o relógio do sistema com uma [tempo Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) antes de iniciar a instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b7cc-140">Synchronize your system clock with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) before starting hello installation.</span></span>

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="9b7cc-141">servidor de configuração de saudação pode ser instalado por meio da linha de comando.</span><span class="sxs-lookup"><span data-stu-id="9b7cc-141">hello configuration server can be installed via command line.</span></span> <span data-ttu-id="9b7cc-142">Para obter mais informações, consulte [instalar servidor de configuração de saudação usando as ferramentas de linha de comando](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="9b7cc-142">For more information, see [Installing hello configuration server using Command-line tools](http://aka.ms/installconfigsrv).</span></span>

#### <a name="add-hello-vmware-account-for-automatic-discovery"></a><span data-ttu-id="9b7cc-143">Adicionar conta de VMware Olá para descoberta automática</span><span class="sxs-lookup"><span data-stu-id="9b7cc-143">Add hello VMware account for automatic discovery</span></span>

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="step-2-add-a-vcenter"></a><span data-ttu-id="9b7cc-144">Etapa 2: Adicionar um vCenter</span><span class="sxs-lookup"><span data-stu-id="9b7cc-144">Step 2: Add a vCenter</span></span>
<span data-ttu-id="9b7cc-145">tooallow do Azure Site Recovery toodiscover máquinas virtuais em execução no seu ambiente local, você precisará tooconnect o VMware vCenter Server ou hosts de ESXi vSphere com a recuperação de Site.</span><span class="sxs-lookup"><span data-stu-id="9b7cc-145">tooallow Azure Site Recovery toodiscover virtual machines running in your on-premises environment, you need tooconnect your VMware vCenter Server or vSphere ESXi hosts with Site Recovery.</span></span>

<span data-ttu-id="9b7cc-146">Selecione **+ vCenter** toostart conectando um VMware vCenter server ou um host do VMware vSphere ESXi.</span><span class="sxs-lookup"><span data-stu-id="9b7cc-146">Select **+vCenter** toostart connecting a VMware vCenter server or a VMware vSphere ESXi host.</span></span>

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]


## <a name="common-issues"></a><span data-ttu-id="9b7cc-147">Problemas comuns</span><span class="sxs-lookup"><span data-stu-id="9b7cc-147">Common issues</span></span>
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a><span data-ttu-id="9b7cc-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9b7cc-148">Next steps</span></span>
<span data-ttu-id="9b7cc-149">[Configurar o ambiente de destino](./site-recovery-prepare-target-vmware-to-azure.md) no Azure.</span><span class="sxs-lookup"><span data-stu-id="9b7cc-149">[Set up your target environment](./site-recovery-prepare-target-vmware-to-azure.md) in Azure.</span></span>
