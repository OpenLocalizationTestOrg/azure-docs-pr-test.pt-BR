---
title: "Instalar o Serviço de Mobilidade (VMware ou físico no Azure) | Microsoft Docs"
description: "Saiba como instalar o agente do Serviço de Mobilidade para proteger os computadores locais."
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
ms.workload: backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 848284f37ae2470a169d8f8a8c9c0bb5b926abe3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="install-mobility-service-vmware-or-physical-to-azure"></a><span data-ttu-id="aa2d4-103">Instalar o Serviço de Mobilidade (VMware ou físico no Azure)</span><span class="sxs-lookup"><span data-stu-id="aa2d4-103">Install Mobility Service (VMware or physical to Azure)</span></span>
<span data-ttu-id="aa2d4-104">O Serviço de Mobilidade do Azure Site Recovery captura gravações de dados em um computador e, em seguida, encaminha-os para o servidor em processo.</span><span class="sxs-lookup"><span data-stu-id="aa2d4-104">Azure Site Recovery Mobility Service captures data writes on a computer, and then forwards them to the process server.</span></span> <span data-ttu-id="aa2d4-105">Implante o Serviço de Mobilidade em cada computador (VM VMware ou servidor físico) que você deseja replicar para o Azure.</span><span class="sxs-lookup"><span data-stu-id="aa2d4-105">Deploy Mobility Service to every computer (VMware VM or physical server) that you want to replicate to Azure.</span></span> <span data-ttu-id="aa2d4-106">É possível implantar o Serviço de Mobilidade nos servidores que você deseja proteger usando os seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="aa2d4-106">You can deploy Mobility Service to the servers that you want to protect by using the following methods:</span></span>


* [<span data-ttu-id="aa2d4-107">Instalar o Serviço de Mobilidade usando as ferramentas de implantação de software, como o System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="aa2d4-107">Install Mobility Service by using software deployment tools like System Center Configuration Manager</span></span>](site-recovery-install-mobility-service-using-sccm.md)
* [<span data-ttu-id="aa2d4-108">Instalar o Serviço de Mobilidade usando a Automação do Azure e o DSC de Automação (Configuração de Estado Desejado)</span><span class="sxs-lookup"><span data-stu-id="aa2d4-108">Install Mobility Service by using Azure Automation and Desired State Configuration (Automation DSC)</span></span>](site-recovery-automate-mobility-service-install.md)
* [<span data-ttu-id="aa2d4-109">Instalar o Serviço de Mobilidade manualmente usando a GUI (interface gráfica do usuário)</span><span class="sxs-lookup"><span data-stu-id="aa2d4-109">Install Mobility Service manually by using the graphical user interface (GUI)</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)
* [<span data-ttu-id="aa2d4-110">Instalar o Serviço de Mobilidade manualmente em um prompt de comando</span><span class="sxs-lookup"><span data-stu-id="aa2d4-110">Install Mobility Service manually at a command prompt</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)
* [<span data-ttu-id="aa2d4-111">Instalar o Serviço de Mobilidade usando a instalação por push por meio do Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="aa2d4-111">Install Mobility Service by push installation from Azure Site Recovery</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)


>[!IMPORTANT]
> <span data-ttu-id="aa2d4-112">A partir da versão 9.7.0.0, em VMs (máquinas virtuais) Windows, o instalador do Serviço de Mobilidade também instala o último [agente de VM do Azure](../virtual-machines/windows/extensions-features.md#azure-vm-agent) disponível.</span><span class="sxs-lookup"><span data-stu-id="aa2d4-112">Beginning with version 9.7.0.0, on Windows virtual machines (VMs), the Mobility Service installer also installs the latest available [Azure VM agent](../virtual-machines/windows/extensions-features.md#azure-vm-agent).</span></span> <span data-ttu-id="aa2d4-113">Quando um computador faz failover no Azure, o computador atende ao pré-requisito da instalação do agente para usar qualquer extensão de VM.</span><span class="sxs-lookup"><span data-stu-id="aa2d4-113">When a computer fails over to Azure, the computer meets the agent installation prerequisite for using any VM extension.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa2d4-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="aa2d4-114">Prerequisites</span></span>
<span data-ttu-id="aa2d4-115">Conclua estas etapas de pré-requisito antes de instalar o Serviço de Mobilidade manualmente no servidor:</span><span class="sxs-lookup"><span data-stu-id="aa2d4-115">Complete these prerequisite steps before you manually install Mobility Service on your server:</span></span>
1. <span data-ttu-id="aa2d4-116">Entre no servidor de configuração e, em seguida, abra uma janela de Prompt de Comando como administrador.</span><span class="sxs-lookup"><span data-stu-id="aa2d4-116">Sign in to your configuration server, and then open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="aa2d4-117">Altere o diretório para a pasta bin e, em seguida, crie um arquivo de senha:</span><span class="sxs-lookup"><span data-stu-id="aa2d4-117">Change the directory to the bin folder, and then create a passphrase file:</span></span>

    ```
    cd %ProgramData%\ASR\home\svsystems\bin
    genpassphrase.exe -v > MobSvc.passphrase
    ```
3. <span data-ttu-id="aa2d4-118">Armazene o arquivo de senha em uma localização segura.</span><span class="sxs-lookup"><span data-stu-id="aa2d4-118">Store the passphrase file in a secure location.</span></span> <span data-ttu-id="aa2d4-119">É possível usar o arquivo durante a instalação do Serviço de Mobilidade.</span><span class="sxs-lookup"><span data-stu-id="aa2d4-119">You use the file during the Mobility Service installation.</span></span>
4. <span data-ttu-id="aa2d4-120">Os instaladores do Serviço de Mobilidade para todos os sistemas operacionais com suporte estão na pasta %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository.</span><span class="sxs-lookup"><span data-stu-id="aa2d4-120">Mobility Service installers for all supported operating systems are in the %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository folder.</span></span>

### <a name="mobility-service-installer-to-operating-system-mapping"></a><span data-ttu-id="aa2d4-121">Mapeamento do instalador para o sistema operacional do Serviço de Mobilidade</span><span class="sxs-lookup"><span data-stu-id="aa2d4-121">Mobility Service installer-to-operating system mapping</span></span>

| <span data-ttu-id="aa2d4-122">Nome do modelo do arquivo do instalador</span><span class="sxs-lookup"><span data-stu-id="aa2d4-122">Installer file template name</span></span>| <span data-ttu-id="aa2d4-123">Sistema operacional</span><span class="sxs-lookup"><span data-stu-id="aa2d4-123">Operating system</span></span> |
|---|--|
|<span data-ttu-id="aa2d4-124">Microsoft-ASR\_UA\*Windows\*release.exe</span><span class="sxs-lookup"><span data-stu-id="aa2d4-124">Microsoft-ASR\_UA\*Windows\*release.exe</span></span> | <span data-ttu-id="aa2d4-125">Windows Server 2008 R2 SP1 (64 bits)</span><span class="sxs-lookup"><span data-stu-id="aa2d4-125">Windows Server 2008 R2 SP1 (64-bit)</span></span> </br> <span data-ttu-id="aa2d4-126">Windows Server 2012 (64 bits)</span><span class="sxs-lookup"><span data-stu-id="aa2d4-126">Windows Server 2012 (64-bit)</span></span> </br> <span data-ttu-id="aa2d4-127">Windows Server 2012 R2 (64 bits)</span><span class="sxs-lookup"><span data-stu-id="aa2d4-127">Windows Server 2012 R2 (64-bit)</span></span> |
|<span data-ttu-id="aa2d4-128">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="aa2d4-128">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span></span>| <span data-ttu-id="aa2d4-129">RHEL (Red Hat Enterprise Linux) 6.4, 6.5, 6.6, 6.7, 6.8 (somente 64 bits)</span><span class="sxs-lookup"><span data-stu-id="aa2d4-129">Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> </br> <span data-ttu-id="aa2d4-130">CentOS 6.4, 6.5, 6.6, 6.7, 6.8 (somente 64 bits)</span><span class="sxs-lookup"><span data-stu-id="aa2d4-130">CentOS 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> |
|<span data-ttu-id="aa2d4-131">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="aa2d4-131">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span></span> | <span data-ttu-id="aa2d4-132">Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (somente 64 bits)</span><span class="sxs-lookup"><span data-stu-id="aa2d4-132">Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (64-bit only)</span></span> </br> <span data-ttu-id="aa2d4-133">CentOS 7.0, 7.1, 7.2 (somente 64 bits)</span><span class="sxs-lookup"><span data-stu-id="aa2d4-133">CentOS 7.0, 7.1, 7.2 (64-bit only)</span></span></br> <span data-ttu-id="aa2d4-134">CentOs 7.3 (somente migração)</span><span class="sxs-lookup"><span data-stu-id="aa2d4-134">CentOs 7.3 (migration only)</span></span> |
|<span data-ttu-id="aa2d4-135">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="aa2d4-135">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span></span>| <span data-ttu-id="aa2d4-136">SUSE Linux Enterprise Server 11 SP3 (somente 64 bits)</span><span class="sxs-lookup"><span data-stu-id="aa2d4-136">SUSE Linux Enterprise Server 11 SP3 (64-bit only)</span></span>|
|<span data-ttu-id="aa2d4-137">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="aa2d4-137">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span></span>| <span data-ttu-id="aa2d4-138">SUSE Linux Enterprise Server 11 SP4 (somente 64 bits)</span><span class="sxs-lookup"><span data-stu-id="aa2d4-138">SUSE Linux Enterprise Server 11 SP4 (64-bit only)</span></span>|
|<span data-ttu-id="aa2d4-139">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="aa2d4-139">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span></span> | <span data-ttu-id="aa2d4-140">Oracle Enterprise Linux 6.4, 6.5 (somente 64 bits)</span><span class="sxs-lookup"><span data-stu-id="aa2d4-140">Oracle Enterprise Linux 6.4, 6.5 (64-bit only)</span></span>|
|<span data-ttu-id="aa2d4-141">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="aa2d4-141">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span></span> | <span data-ttu-id="aa2d4-142">Ubuntu Linux 14.04 (somente 64 bits)</span><span class="sxs-lookup"><span data-stu-id="aa2d4-142">Ubuntu Linux 14.04 (64-bit only)</span></span>|


## <a name="install-mobility-service-manually-by-using-the-gui"></a><span data-ttu-id="aa2d4-143">Instalar o Serviço de Mobilidade manualmente usando a GUI</span><span class="sxs-lookup"><span data-stu-id="aa2d4-143">Install Mobility Service manually by using the GUI</span></span>

>[!IMPORTANT]
> <span data-ttu-id="aa2d4-144">Se você estiver usando um **Servidor de Configuração** para replicar **máquinas virtuais do Azure IaaS** de uma Região/Assinatura do Azure para outra, **use o método de instalação baseado em Linha de comando**</span><span class="sxs-lookup"><span data-stu-id="aa2d4-144">If you are using a **Configuration Server** to replicate **Azure IaaS virtual machines** from one Azure Subscription/Region to another then **use the Command-line based installation** method</span></span>

[!INCLUDE [site-recovery-install-mob-svc-gui](../../includes/site-recovery-install-mob-svc-gui.md)]

## <a name="install-mobility-service-manually-at-a-command-prompt"></a><span data-ttu-id="aa2d4-145">Instalar o Serviço de Mobilidade manualmente em um prompt de comando</span><span class="sxs-lookup"><span data-stu-id="aa2d4-145">Install Mobility Service manually at a command prompt</span></span>

### <a name="command-line-installation-on-a-windows-computer"></a><span data-ttu-id="aa2d4-146">Instalação de linha de comando em um computador Windows</span><span class="sxs-lookup"><span data-stu-id="aa2d4-146">Command-line installation on a Windows computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-win-cmd](../../includes/site-recovery-install-mob-svc-win-cmd.md)]

### <a name="command-line-installation-on-a-linux-computer"></a><span data-ttu-id="aa2d4-147">Instalação de linha de comando em um computador Linux</span><span class="sxs-lookup"><span data-stu-id="aa2d4-147">Command-line installation on a Linux computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-lin-cmd](../../includes/site-recovery-install-mob-svc-lin-cmd.md)]


## <a name="install-mobility-service-by-push-installation-from-azure-site-recovery"></a><span data-ttu-id="aa2d4-148">Instalar o Serviço de Mobilidade usando a instalação por push por meio do Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="aa2d4-148">Install Mobility Service by push installation from Azure Site Recovery</span></span>
<span data-ttu-id="aa2d4-149">Para fazer uma instalação por push do Serviço de Mobilidade usando o Site Recovery, todos os computadores de destino devem atender aos pré-requisitos a seguir.</span><span class="sxs-lookup"><span data-stu-id="aa2d4-149">To do a push installation of Mobility Service by using Site Recovery, all target computers must meet the following prerequisites.</span></span>

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-win](../../includes/site-recovery-prepare-push-install-mob-svc-win.md)]

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-lin](../../includes/site-recovery-prepare-push-install-mob-svc-lin.md)]


> [!NOTE]
<span data-ttu-id="aa2d4-150">Depois de instalar o Serviço de Mobilidade, no portal do Azure, selecione o botão **Replicar** para começar a proteger essas VMs.</span><span class="sxs-lookup"><span data-stu-id="aa2d4-150">After Mobility Service is installed, in the Azure portal, select the **Replicate** button to start protecting these VMs.</span></span>

## <a name="uninstall-mobility-service-on-a-windows-server-computer"></a><span data-ttu-id="aa2d4-151">Desinstalar o Serviço de Mobilidade de um computador Windows Server</span><span class="sxs-lookup"><span data-stu-id="aa2d4-151">Uninstall Mobility Service on a Windows Server computer</span></span>
<span data-ttu-id="aa2d4-152">Use um dos métodos a seguir para desinstalar o Serviço de Mobilidade em um computador Windows Server.</span><span class="sxs-lookup"><span data-stu-id="aa2d4-152">Use one of the following methods to uninstall Mobility Service on a Windows Server computer.</span></span>

### <a name="uninstall-by-using-the-gui"></a><span data-ttu-id="aa2d4-153">Desinstalar usando a GUI</span><span class="sxs-lookup"><span data-stu-id="aa2d4-153">Uninstall by using the GUI</span></span>
1. <span data-ttu-id="aa2d4-154">No Painel de Controle, selecione **Programas**.</span><span class="sxs-lookup"><span data-stu-id="aa2d4-154">In Control Panel, select **Programs**.</span></span>
2. <span data-ttu-id="aa2d4-155">Selecione **Serviço de Mobilidade do Microsoft Azure Site Recovery/servidor de Destino Mestre** e, em seguida, **Desinstalar**.</span><span class="sxs-lookup"><span data-stu-id="aa2d4-155">Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.</span></span>

### <a name="uninstall-at-a-command-prompt"></a><span data-ttu-id="aa2d4-156">Desinstalar em um prompt de comando</span><span class="sxs-lookup"><span data-stu-id="aa2d4-156">Uninstall at a command prompt</span></span>
1. <span data-ttu-id="aa2d4-157">Abra uma janela de Prompt de comando como administrador.</span><span class="sxs-lookup"><span data-stu-id="aa2d4-157">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="aa2d4-158">Para desinstalar o Serviço de Mobilidade, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="aa2d4-158">To uninstall Mobility Service, run the following command:</span></span>

```
MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
```

## <a name="uninstall-mobility-service-on-a-linux-computer"></a><span data-ttu-id="aa2d4-159">Desinstalar o Serviço de Mobilidade de um computador Linux</span><span class="sxs-lookup"><span data-stu-id="aa2d4-159">Uninstall Mobility Service on a Linux computer</span></span>
1. <span data-ttu-id="aa2d4-160">No servidor Linux, entre como um usuário **raiz**.</span><span class="sxs-lookup"><span data-stu-id="aa2d4-160">On your Linux server, sign in as a **root** user.</span></span>
2. <span data-ttu-id="aa2d4-161">Em um terminal, acesse /user/local/ASR.</span><span class="sxs-lookup"><span data-stu-id="aa2d4-161">In a terminal, go to /user/local/ASR.</span></span>
3. <span data-ttu-id="aa2d4-162">Para desinstalar o Serviço de Mobilidade, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="aa2d4-162">To uninstall Mobility Service, run the following command:</span></span>

```
uninstall.sh -Y
```
