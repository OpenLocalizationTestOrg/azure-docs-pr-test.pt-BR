---
title: "Configurar a origem e o destino de replicação de VMware para o Azure com o Azure Site Recovery | Microsoft Docs"
description: "Resume as etapas para definir as configurações de origem e destino para replicação de VMs VMware para armazenamento do Azure com o Azure Site Recovery"
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
ms.openlocfilehash: 94b629a62c3a54eee69ee397b2f27e3f20b753d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="step-8-set-up-the-source-and-target-for-vmware-replication-to-azure"></a><span data-ttu-id="cfd67-103">Etapa 8: Configurar a origem e o destino para replicação de VMware para o Azure</span><span class="sxs-lookup"><span data-stu-id="cfd67-103">Step 8: Set up the source and target for VMware replication to Azure</span></span>

<span data-ttu-id="cfd67-104">Este artigo descreve como definir as configurações de origem e destino ao replicar máquinas virtuais VMware locais para Azure utilizando o serviço [Azure Site Recovery](site-recovery-overview.md) no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="cfd67-104">This article describes how to configure source and target settings when replicating on-premises VMware virtual machines to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="cfd67-105">Poste perguntas e comentários na parte inferior deste artigo ou no [Fórum de Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="cfd67-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="set-up-the-source-environment"></a><span data-ttu-id="cfd67-106">Configurar o ambiente de origem</span><span class="sxs-lookup"><span data-stu-id="cfd67-106">Set up the source environment</span></span>

<span data-ttu-id="cfd67-107">Defina o servidor de configuração, registre-o no cofre e descubra VMs.</span><span class="sxs-lookup"><span data-stu-id="cfd67-107">Set up the configuration server, register it in the vault, and discover VMs.</span></span>

1. <span data-ttu-id="cfd67-108">Clique em **Site Recovery** > **Etapa 1: preparar a infraestrutura** > **Origem**.</span><span class="sxs-lookup"><span data-stu-id="cfd67-108">Click **Site Recovery** > **Step 1: Prepare Infrastructure** > **Source**.</span></span>
2. <span data-ttu-id="cfd67-109">Se não tiver um servidor de configuração, clique em **+Servidor de configuração**.</span><span class="sxs-lookup"><span data-stu-id="cfd67-109">If you don’t have a configuration server, click **+Configuration server**.</span></span>
3. <span data-ttu-id="cfd67-110">Em **Adicionar Servidor**, verifique se **Servidor de Configuração** aparece em **Tipo de servidor**.</span><span class="sxs-lookup"><span data-stu-id="cfd67-110">In **Add Server**, check that **Configuration Server** appears in **Server type**.</span></span>
4. <span data-ttu-id="cfd67-111">Baixe o arquivo de instalação Configuração Unificada da Recuperação de Site.</span><span class="sxs-lookup"><span data-stu-id="cfd67-111">Download the Site Recovery Unified Setup installation file.</span></span>
5. <span data-ttu-id="cfd67-112">Baixe a chave do registro do cofre.</span><span class="sxs-lookup"><span data-stu-id="cfd67-112">Download the vault registration key.</span></span> <span data-ttu-id="cfd67-113">Você precisará dela quando executar a Configuração Unificada.</span><span class="sxs-lookup"><span data-stu-id="cfd67-113">You need this when you run Unified Setup.</span></span> <span data-ttu-id="cfd67-114">A chave é válida por cinco dias após ser gerada.</span><span class="sxs-lookup"><span data-stu-id="cfd67-114">The key is valid for five days after you generate it.</span></span>

   ![Configurar origem](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-the-configuration-server-in-the-vault"></a><span data-ttu-id="cfd67-116">Registrar o servidor de configuração no cofre</span><span class="sxs-lookup"><span data-stu-id="cfd67-116">Register the configuration server in the vault</span></span>

<span data-ttu-id="cfd67-117">Faça o descrito a seguir antes de começar, então execute a Configuração Unificada para instalar o servidor de configuração, o servidor de processo e o servidor de destino mestre.</span><span class="sxs-lookup"><span data-stu-id="cfd67-117">Do the following before you start, then run Unified Setup to install the configuration server, the process server, and the master target server.</span></span>
    - <span data-ttu-id="cfd67-118">Obter uma rápida visão geral em vídeo</span><span class="sxs-lookup"><span data-stu-id="cfd67-118">Get a quick video overview</span></span>

        > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

    - <span data-ttu-id="cfd67-119">Na VM do servidor de configuração, certifique-se de que o relógio do sistema esteja sincronizado com um [Servidor de Horário](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span><span class="sxs-lookup"><span data-stu-id="cfd67-119">On the configuration server VM, make sure that the system clock is synchronized with a [Time Server](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service).</span></span> <span data-ttu-id="cfd67-120">Ele deve ser correspondente.</span><span class="sxs-lookup"><span data-stu-id="cfd67-120">It should match.</span></span> <span data-ttu-id="cfd67-121">Se ele estiver 15 minutos adiantado ou atrasado, a instalação poderá falhar.</span><span class="sxs-lookup"><span data-stu-id="cfd67-121">If it's 15 minutes in front or behind, setup might fail.</span></span>
    - <span data-ttu-id="cfd67-122">Execute a instalação como um Administrador Local na VM do servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="cfd67-122">Run setup as a Local Administrator on the configuration server VM.</span></span>
    - <span data-ttu-id="cfd67-123">Verifique se TLS 1.0 está habilitado na VM.</span><span class="sxs-lookup"><span data-stu-id="cfd67-123">Make sure TLS 1.0 is enabled on the VM.</span></span>


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> <span data-ttu-id="cfd67-124">O servidor de configuração também pode ser instalado [da linha de comando](http://aka.ms/installconfigsrv).</span><span class="sxs-lookup"><span data-stu-id="cfd67-124">The configuration server can also be installed [from the command line](http://aka.ms/installconfigsrv).</span></span>



## <a name="connect-to-vmware-servers"></a><span data-ttu-id="cfd67-125">Conectar a servidores VMware</span><span class="sxs-lookup"><span data-stu-id="cfd67-125">Connect to VMware servers</span></span>

<span data-ttu-id="cfd67-126">Para permitir que o Azure Site Recovery descubra máquinas virtuais em execução no ambiente local, você precisa conectar seu VMware vCenter Server ou hosts vSphere ESXi ao Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="cfd67-126">To allow Azure Site Recovery to discover virtual machines running in your on-premises environment, you need to connect your VMware vCenter Server or vSphere ESXi hosts with Site Recovery.</span></span> <span data-ttu-id="cfd67-127">Observe o seguinte antes de começar:</span><span class="sxs-lookup"><span data-stu-id="cfd67-127">Note the following before you start:</span></span>

- <span data-ttu-id="cfd67-128">Se você adicionar o servidor vCenter ou hosts vSphere ao Site Recovery com uma conta sem privilégios de administrador no servidor, a conta precisará ter esses privilégios habilitados:</span><span class="sxs-lookup"><span data-stu-id="cfd67-128">If you add the vCenter server or vSphere hosts to Site Recovery with an account without administrator privileges on the server, the account needs these privileges enabled:</span></span>
    - <span data-ttu-id="cfd67-129">Datacenter, Repositório de Dados, Pasta, Host, Rede, Recurso, Máquina Virtual, vSphere Distributed Switch.</span><span class="sxs-lookup"><span data-stu-id="cfd67-129">Datacenter, Datastore, Folder, Host, Network, Resource, Virtual machine, vSphere Distributed Switch.</span></span>
    - <span data-ttu-id="cfd67-130">O servidor vCenter precisa das permissões de exibição do Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="cfd67-130">The vCenter server needs Storage views permissions.</span></span>
- <span data-ttu-id="cfd67-131">Quando você adiciona servidores VMware ao Site Recovery, pode levar 15 minutos ou mais para que eles apareçam no portal.</span><span class="sxs-lookup"><span data-stu-id="cfd67-131">When you add VMware servers to Site Recovery, it can take 15 minutes or longer for them to appear in the portal.</span></span>

### <a name="add-the-account-for-automatic-discovery"></a><span data-ttu-id="cfd67-132">Adicione a conta para descoberta automática</span><span class="sxs-lookup"><span data-stu-id="cfd67-132">Add the account for automatic discovery</span></span>

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="set-up-a-connection"></a><span data-ttu-id="cfd67-133">Configurar uma conexão</span><span class="sxs-lookup"><span data-stu-id="cfd67-133">Set up a connection</span></span>

<span data-ttu-id="cfd67-134">Conecte-se aos servidores da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="cfd67-134">Connect to servers as follows:</span></span>

1. <span data-ttu-id="cfd67-135">Selecione **+vCenter** para iniciar a conexão de um VMware vCenter Server ou um host VMware vSphere ESXi.</span><span class="sxs-lookup"><span data-stu-id="cfd67-135">Select **+vCenter** to start connecting a VMware vCenter server or a VMware vSphere ESXi host.</span></span>
2. <span data-ttu-id="cfd67-136">Em **Adicionar vCenter**, especifique um nome amigável para o host vSphere ou servidor vCenter e então especifique o endereço IP ou o FQDN do servidor.</span><span class="sxs-lookup"><span data-stu-id="cfd67-136">In **Add vCenter**, specify a friendly name for the vSphere host or vCenter server, and then specify the IP address or FQDN of the server.</span></span>
3. <span data-ttu-id="cfd67-137">Deixe a porta como 443, a menos que os servidores do VMware estejam configurados para escutar solicitações em uma porta diferente.</span><span class="sxs-lookup"><span data-stu-id="cfd67-137">Leave the port as 443 unless your VMware servers are configured to listen for requests on a different port.</span></span> <span data-ttu-id="cfd67-138">Selecione a conta que deve se conectar ao VMware vCenter ou ao servidor vSphere ESXi.</span><span class="sxs-lookup"><span data-stu-id="cfd67-138">Select the account that is to connect to the VMware vCenter or vSphere ESXi server.</span></span> <span data-ttu-id="cfd67-139">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="cfd67-139">Click **OK**.</span></span>
4. <span data-ttu-id="cfd67-140">A Site Recovery conecta-se a servidores VMware usando as configurações especificadas e descobre VMs.</span><span class="sxs-lookup"><span data-stu-id="cfd67-140">Site Recovery connects to VMware servers using the specified settings, and discovers VMs.</span></span>

> [!NOTE]
> <span data-ttu-id="cfd67-141">Se você estiver adicionando um servidor ou host vCenter com uma conta que não tem privilégios de administrador no vCenter ou no servidor host, verifique se a conta tem estes privilégios habilitados: Data center, Armazenamento de Dados, Pasta, Host, Rede, Recursos, Máquina virtual e Comutador Distribuído do vSphere.</span><span class="sxs-lookup"><span data-stu-id="cfd67-141">If you're adding a server or host with an account that doesn't have administrator privileges on the vCenter or host server, make sure that the account has these privileges enabled: Datacenter, Datastore, Folder, Host, Network, Resource, Virtual machine, and vSphere Distributed Switch.</span></span> <span data-ttu-id="cfd67-142">Além disso, o servidor VMware vCenter precisa do privilégio de Exibição do Armazenamento habilitado.</span><span class="sxs-lookup"><span data-stu-id="cfd67-142">In addition, the VMware vCenter server needs the Storage Views privilege enabled.</span></span>


## <a name="set-up-the-target-environment"></a><span data-ttu-id="cfd67-143">Configurar o ambiente de origem</span><span class="sxs-lookup"><span data-stu-id="cfd67-143">Set up the target environment</span></span>

<span data-ttu-id="cfd67-144">Antes de configurar o ambiente de destino, certifique-se de ter uma conta de armazenamento do Azure e uma rede virtual configurada.</span><span class="sxs-lookup"><span data-stu-id="cfd67-144">Before you set up the target environment, make sure you have an Azure storage account and virtual network set up.</span></span>

1. <span data-ttu-id="cfd67-145">Clique em **Preparar infraestrutura** > **Destino** e selecione a assinatura do Azure que você deseja usar.</span><span class="sxs-lookup"><span data-stu-id="cfd67-145">Click **Prepare infrastructure** > **Target**, and select the Azure subscription you want to use.</span></span>
2. <span data-ttu-id="cfd67-146">Especifique se o seu modelo de implantação de destino é baseada no Gerenciador de Recursos ou clássico.</span><span class="sxs-lookup"><span data-stu-id="cfd67-146">Specify whether your target deployment model is Resource Manager-based, or classic.</span></span>
3. <span data-ttu-id="cfd67-147">A Recuperação de Site verifica se você tem uma ou mais contas de armazenamento e redes do Azure compatíveis.</span><span class="sxs-lookup"><span data-stu-id="cfd67-147">Site Recovery checks that you have one or more compatible Azure storage accounts and networks.</span></span>

   ![Destino](./media/vmware-walkthrough-source-target/gs-target.png)
4. <span data-ttu-id="cfd67-149">Se não tiver criado uma conta de armazenamento ou de rede, clique em **+Conta de armazenamento** ou **+Rede** para criar uma conta do Gerenciador de Recursos ou embutida de rede.</span><span class="sxs-lookup"><span data-stu-id="cfd67-149">If you haven't created a storage account or network, click **+Storage account** or **+Network**, to create a Resource Manager account or network inline.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cfd67-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cfd67-150">Next steps</span></span>

<span data-ttu-id="cfd67-151">Vá para a [Etapa 9: Configurar uma política de replicação](vmware-walkthrough-replication.md)</span><span class="sxs-lookup"><span data-stu-id="cfd67-151">Go to [Step 9: Set up a replication policy](vmware-walkthrough-replication.md)</span></span>
