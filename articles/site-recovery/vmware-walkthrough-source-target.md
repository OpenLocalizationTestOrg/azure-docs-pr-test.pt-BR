---
title: "aaaSet a origem de saudação e de destino para VMware tooAzure de replicação com o Azure Site Recovery | Microsoft Docs"
description: "Resume Olá etapas tooset as configurações de origem e destino de replicação de máquinas virtuais do VMware tooAzure armazenamento com o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99e422e-daf7-4fa8-af3c-af2340340136
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: ef33a44bc5da17afb0442be63f576925f5b9a8b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-vmware-replication-tooazure"></a><span data-ttu-id="c52a1-103">Etapa 8: Configurar a origem de saudação e de destino para VMware tooAzure de replicação</span><span class="sxs-lookup"><span data-stu-id="c52a1-103">Step 8: Set up hello source and target for VMware replication tooAzure</span></span>

<span data-ttu-id="c52a1-104">Este artigo descreve como tooconfigure configurações de origem e de destino durante a replicação local tooAzure de máquinas virtuais VMware, usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c52a1-104">This article describes how tooconfigure source and target settings when replicating on-premises VMware virtual machines tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="c52a1-105">Postar perguntas e comentários na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="c52a1-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-hello-source-environment"></a><span data-ttu-id="c52a1-106">Configurar o ambiente de origem Olá</span><span class="sxs-lookup"><span data-stu-id="c52a1-106">Set up hello source environment</span></span>

<span data-ttu-id="c52a1-107">Configurar o servidor de configuração de hello, registrá-lo no cofre hello e descobrir máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="c52a1-107">Set up hello configuration server, register it in hello vault, and discover VMs.</span></span>

1. <span data-ttu-id="c52a1-108">Clique em **Site Recovery** > **Etapa 1: preparar a infraestrutura** > **Origem**.</span><span class="sxs-lookup"><span data-stu-id="c52a1-108">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Source**.</span></span>
2. <span data-ttu-id="c52a1-109">Se não tiver um servidor de configuração, clique em **+Servidor de configuração**.</span><span class="sxs-lookup"><span data-stu-id="c52a1-109">If you don’t have a configuration server, click **+Configuration server**.</span></span>
3. <span data-ttu-id="c52a1-110">Em **Adicionar Servidor**, verifique se **Servidor de Configuração** aparece em **Tipo de servidor**.</span><span class="sxs-lookup"><span data-stu-id="c52a1-110">In **Add Server**, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="c52a1-111">Baixe o arquivo de instalação de configuração do Site Recovery unificado de hello.</span><span class="sxs-lookup"><span data-stu-id="c52a1-111">Download hello Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="c52a1-112">Baixe a chave de registro de cofre hello.</span><span class="sxs-lookup"><span data-stu-id="c52a1-112">Download hello vault registration key.</span></span> <span data-ttu-id="c52a1-113">Você precisará dela quando executar a Configuração Unificada.</span><span class="sxs-lookup"><span data-stu-id="c52a1-113">You need this when you run Unified Setup.</span></span> <span data-ttu-id="c52a1-114">chave de saudação é válida por cinco dias depois que ele é gerado.</span><span class="sxs-lookup"><span data-stu-id="c52a1-114">hello key is valid for five days after you generate it.</span></span>

   ![Configurar origem](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a><span data-ttu-id="c52a1-116">Registrar o servidor de configuração de saudação no cofre Olá</span><span class="sxs-lookup"><span data-stu-id="c52a1-116">Register hello configuration server in hello vault</span></span>

<span data-ttu-id="c52a1-117">Seguinte Olá antes de iniciar, em seguida executar instalação unificado tooinstall Olá configuração server, Olá processo server e o servidor de destino mestre hello.</span><span class="sxs-lookup"><span data-stu-id="c52a1-117">Do hello following before you start, then run Unified Setup tooinstall hello configuration server, hello process server, and hello master target server.</span></span>
    - <span data-ttu-id="c52a1-118">Obter uma rápida visão geral em vídeo</span><span class="sxs-lookup"><span data-stu-id="c52a1-118">Get a quick video overview</span></span>

        > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

    - <span data-ttu-id="c52a1-119">No servidor de configuração de saudação VM, certifique-se de que o relógio do sistema hello está sincronizado com um [tempo Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span><span class="sxs-lookup"><span data-stu-id="c52a1-119">On hello configuration server VM, make sure that hello system clock is synchronized with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span></span> <span data-ttu-id="c52a1-120">Ele deve ser correspondente.</span><span class="sxs-lookup"><span data-stu-id="c52a1-120">It should match.</span></span> <span data-ttu-id="c52a1-121">Se ele estiver 15 minutos adiantado ou atrasado, a instalação poderá falhar.</span><span class="sxs-lookup"><span data-stu-id="c52a1-121">If it's 15 minutes in front or behind, setup might fail.</span></span>
    - <span data-ttu-id="c52a1-122">Execute a instalação como Administrador Local no servidor de configuração de saudação VM.</span><span class="sxs-lookup"><span data-stu-id="c52a1-122">Run setup as a Local Administrator on hello configuration server VM.</span></span>
    - <span data-ttu-id="c52a1-123">Certifique-se de que TLS 1.0 está ativado Olá VM.</span><span class="sxs-lookup"><span data-stu-id="c52a1-123">Make sure TLS 1.0 is enabled on hello VM.</span></span>


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="c52a1-124">também pode ser instalado o servidor de configuração de saudação [da linha de comando Olá](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="c52a1-124">hello configuration server can also be installed [from hello command line](http://aka.ms/installconfigsrv).</span></span>



## <a name="connect-toovmware-servers"></a><span data-ttu-id="c52a1-125">Conectar servidores tooVMware</span><span class="sxs-lookup"><span data-stu-id="c52a1-125">Connect tooVMware servers</span></span>

<span data-ttu-id="c52a1-126">tooallow do Azure Site Recovery toodiscover máquinas virtuais em execução no seu ambiente local, você precisará tooconnect o VMware vCenter Server ou hosts de ESXi vSphere com a recuperação de Site.</span><span class="sxs-lookup"><span data-stu-id="c52a1-126">tooallow Azure Site Recovery toodiscover virtual machines running in your on-premises environment, you need tooconnect your VMware vCenter Server or vSphere ESXi hosts with Site Recovery.</span></span> <span data-ttu-id="c52a1-127">Observe o seguinte Olá antes de começar:</span><span class="sxs-lookup"><span data-stu-id="c52a1-127">Note hello following before you start:</span></span>

- <span data-ttu-id="c52a1-128">Se você adicionar o servidor do vCenter hello ou vSphere hosts tooSite recuperação com uma conta sem privilégios de administrador no servidor de saudação, conta de Olá precisa desses privilégios habilitados:</span><span class="sxs-lookup"><span data-stu-id="c52a1-128">If you add hello vCenter server or vSphere hosts tooSite Recovery with an account without administrator privileges on hello server, hello account needs these privileges enabled:</span></span>
    - <span data-ttu-id="c52a1-129">Datacenter, Repositório de Dados, Pasta, Host, Rede, Recurso, Máquina Virtual, vSphere Distributed Switch.</span><span class="sxs-lookup"><span data-stu-id="c52a1-129">Datacenter, Datastore, Folder, Host, Network, Resource, Virtual machine, vSphere Distributed Switch.</span></span>
    - <span data-ttu-id="c52a1-130">servidor do vCenter Olá precisa de permissões de exibições de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c52a1-130">hello vCenter server needs Storage views permissions.</span></span>
- <span data-ttu-id="c52a1-131">Quando você adiciona servidores de VMware tooSite recuperação, pode levar 15 minutos ou mais para que eles tooappear no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="c52a1-131">When you add VMware servers tooSite Recovery, it can take 15 minutes or longer for them tooappear in hello portal.</span></span>

### <a name="add-hello-account-for-automatic-discovery"></a><span data-ttu-id="c52a1-132">Adicionar conta Olá para descoberta automática</span><span class="sxs-lookup"><span data-stu-id="c52a1-132">Add hello account for automatic discovery</span></span>

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="set-up-a-connection"></a><span data-ttu-id="c52a1-133">Configurar uma conexão</span><span class="sxs-lookup"><span data-stu-id="c52a1-133">Set up a connection</span></span>

<span data-ttu-id="c52a1-134">Conecte-se tooservers da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="c52a1-134">Connect tooservers as follows:</span></span>

1. <span data-ttu-id="c52a1-135">Selecione **+ vCenter** toostart conectando um VMware vCenter server ou um host do VMware vSphere ESXi.</span><span class="sxs-lookup"><span data-stu-id="c52a1-135">Select **+vCenter** toostart connecting a VMware vCenter server or a VMware vSphere ESXi host.</span></span>
2. <span data-ttu-id="c52a1-136">Em **adicionar vCenter**, especifique um nome amigável para o servidor de host ou vCenter vSphere hello e em seguida, especifique o endereço IP hello ou FQDN do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="c52a1-136">In **Add vCenter**, specify a friendly name for hello vSphere host or vCenter server, and then specify hello IP address or FQDN of hello server.</span></span>
3. <span data-ttu-id="c52a1-137">Deixe a porta hello como 443, a menos que os servidores do VMware são toolisten configurada para solicitações em uma porta diferente.</span><span class="sxs-lookup"><span data-stu-id="c52a1-137">Leave hello port as 443 unless your VMware servers are configured toolisten for requests on a different port.</span></span> <span data-ttu-id="c52a1-138">Selecione a conta Olá tooconnect toohello VMware vCenter ou vSphere ESXi server.</span><span class="sxs-lookup"><span data-stu-id="c52a1-138">Select hello account that is tooconnect toohello VMware vCenter or vSphere ESXi server.</span></span> <span data-ttu-id="c52a1-139">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="c52a1-139">Click **OK**.</span></span>
4. <span data-ttu-id="c52a1-140">Recuperação de site se conecta a servidores tooVMware usar Olá especificado as configurações e descobre máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="c52a1-140">Site Recovery connects tooVMware servers using hello specified settings, and discovers VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="c52a1-141">Se você estiver adicionando um servidor ou host com uma conta que não tem privilégios de administrador no servidor de host ou vCenter Olá, certifique-se de que conta Olá tem esses privilégios habilitados: Datacenter repositório de dados, pasta, Host, rede, o recurso de máquina Virtual, e vSphere comutador distribuída.</span><span class="sxs-lookup"><span data-stu-id="c52a1-141">If you're adding a server or host with an account that doesn't have administrator privileges on hello vCenter or host server, make sure that hello account has these privileges enabled: Datacenter, Datastore, Folder, Host, Network, Resource, Virtual machine, and vSphere Distributed Switch.</span></span> <span data-ttu-id="c52a1-142">Além disso, Olá VMware vCenter server precisa de exibições de armazenamento Olá privilégio habilitado.</span><span class="sxs-lookup"><span data-stu-id="c52a1-142">In addition, hello VMware vCenter server needs hello Storage Views privilege enabled.</span></span>


## <a name="set-up-hello-target-environment"></a><span data-ttu-id="c52a1-143">Configurar o ambiente de destino Olá</span><span class="sxs-lookup"><span data-stu-id="c52a1-143">Set up hello target environment</span></span>

<span data-ttu-id="c52a1-144">Antes de configurar o ambiente de destino hello, verifique se que você tem uma conta de armazenamento do Azure e a configuração da rede virtual.</span><span class="sxs-lookup"><span data-stu-id="c52a1-144">Before you set up hello target environment, make sure you have an Azure storage account and virtual network set up.</span></span>

1. <span data-ttu-id="c52a1-145">Clique em **preparar infraestrutura** > **destino**, e selecione Olá assinatura do Azure que você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="c52a1-145">Click **Prepare infrastructure** > **Target**, and select hello Azure subscription you want toouse.</span></span>
2. <span data-ttu-id="c52a1-146">Especifique se o seu modelo de implantação de destino é baseada no Gerenciador de Recursos ou clássico.</span><span class="sxs-lookup"><span data-stu-id="c52a1-146">Specify whether your target deployment model is Resource Manager-based, or classic.</span></span>
3. <span data-ttu-id="c52a1-147">A Recuperação de Site verifica se você tem uma ou mais contas de armazenamento e redes do Azure compatíveis.</span><span class="sxs-lookup"><span data-stu-id="c52a1-147">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

   ![Destino](./media/vmware-walkthrough-source-target/gs-target.png)
4. <span data-ttu-id="c52a1-149">Se você não tiver criado uma conta de armazenamento ou de rede, clique em **+ conta de armazenamento** ou **+ rede**, toocreate embutido de rede ou a conta de um Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="c52a1-149">If you haven't created a storage account or network, click **+Storage account** or **+Network**, toocreate a Resource Manager account or network inline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c52a1-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c52a1-150">Next steps</span></span>

<span data-ttu-id="c52a1-151">Vá muito[etapa 9: configurar uma política de replicação](vmware-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="c52a1-151">Go too[Step 9: Set up a replication policy](vmware-walkthrough-replication.md)</span></span>
