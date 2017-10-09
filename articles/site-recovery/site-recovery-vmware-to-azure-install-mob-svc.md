---
title: "aaaInstall serviço de mobilidade (VMware ou físico tooAzure) | Microsoft Docs"
description: "Saiba como tooinstall Olá tooprotect do agente de serviço de mobilidade seus computadores locais."
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
ms.openlocfilehash: f7836e6b35d3838bae1eff927838ce4b245b9f56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-mobility-service-vmware-or-physical-tooazure"></a><span data-ttu-id="a5f5c-103">Instalar serviço de mobilidade (VMware ou tooAzure físico)</span><span class="sxs-lookup"><span data-stu-id="a5f5c-103">Install Mobility Service (VMware or physical tooAzure)</span></span>
<span data-ttu-id="a5f5c-104">Serviço de mobilidade do Azure Site Recovery captura gravações de dados em um computador e, em seguida, encaminha toohello servidor de processo.</span><span class="sxs-lookup"><span data-stu-id="a5f5c-104">Azure Site Recovery Mobility Service captures data writes on a computer, and then forwards them toohello process server.</span></span> <span data-ttu-id="a5f5c-105">Implante o serviço de mobilidade tooevery computador (VM VMware ou servidor físico) que você deseja tooreplicate tooAzure.</span><span class="sxs-lookup"><span data-stu-id="a5f5c-105">Deploy Mobility Service tooevery computer (VMware VM or physical server) that you want tooreplicate tooAzure.</span></span> <span data-ttu-id="a5f5c-106">Você pode implantar servidores do serviço de mobilidade toohello que você deseja tooprotect usando Olá métodos a seguir:</span><span class="sxs-lookup"><span data-stu-id="a5f5c-106">You can deploy Mobility Service toohello servers that you want tooprotect by using hello following methods:</span></span>


* [<span data-ttu-id="a5f5c-107">Instalar o Serviço de Mobilidade usando as ferramentas de implantação de software, como o System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="a5f5c-107">Install Mobility Service by using software deployment tools like System Center Configuration Manager</span></span>](site-recovery-install-mobility-service-using-sccm.md)
* [<span data-ttu-id="a5f5c-108">Instalar o Serviço de Mobilidade usando a Automação do Azure e o DSC de Automação (Configuração de Estado Desejado)</span><span class="sxs-lookup"><span data-stu-id="a5f5c-108">Install Mobility Service by using Azure Automation and Desired State Configuration (Automation DSC)</span></span>](site-recovery-automate-mobility-service-install.md)
* [<span data-ttu-id="a5f5c-109">Instalar serviço de mobilidade manualmente usando a interface gráfica do usuário de saudação (GUI)</span><span class="sxs-lookup"><span data-stu-id="a5f5c-109">Install Mobility Service manually by using hello graphical user interface (GUI)</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)
* [<span data-ttu-id="a5f5c-110">Instalar o Serviço de Mobilidade manualmente em um prompt de comando</span><span class="sxs-lookup"><span data-stu-id="a5f5c-110">Install Mobility Service manually at a command prompt</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)
* [<span data-ttu-id="a5f5c-111">Instalar o Serviço de Mobilidade usando a instalação por push por meio do Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="a5f5c-111">Install Mobility Service by push installation from Azure Site Recovery</span></span>](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)


>[!IMPORTANT]
> <span data-ttu-id="a5f5c-112">Começando com a versão 9.7.0.0, em máquinas de virtuais (VMs) do Windows hello serviço de mobilidade instalador também instala hello mais recente disponível [agente de VM do Azure](../virtual-machines/windows/extensions-features.md#azure-vm-agent).</span><span class="sxs-lookup"><span data-stu-id="a5f5c-112">Beginning with version 9.7.0.0, on Windows virtual machines (VMs), hello Mobility Service installer also installs hello latest available [Azure VM agent](../virtual-machines/windows/extensions-features.md#azure-vm-agent).</span></span> <span data-ttu-id="a5f5c-113">Quando um computador faz failover tooAzure, computador Olá atende aos pré-requisitos para usar qualquer extensão VM de instalação do agente de saudação.</span><span class="sxs-lookup"><span data-stu-id="a5f5c-113">When a computer fails over tooAzure, hello computer meets hello agent installation prerequisite for using any VM extension.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5f5c-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a5f5c-114">Prerequisites</span></span>
<span data-ttu-id="a5f5c-115">Conclua estas etapas de pré-requisito antes de instalar o Serviço de Mobilidade manualmente no servidor:</span><span class="sxs-lookup"><span data-stu-id="a5f5c-115">Complete these prerequisite steps before you manually install Mobility Service on your server:</span></span>
1. <span data-ttu-id="a5f5c-116">Entre no servidor de configuração de tooyour e, em seguida, abra uma janela de Prompt de comando como administrador.</span><span class="sxs-lookup"><span data-stu-id="a5f5c-116">Sign in tooyour configuration server, and then open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="a5f5c-117">Alterar pasta bin do hello diretório toohello e, em seguida, crie um arquivo de senha:</span><span class="sxs-lookup"><span data-stu-id="a5f5c-117">Change hello directory toohello bin folder, and then create a passphrase file:</span></span>

    ```
    cd %ProgramData%\ASR\home\svsystems\bin
    genpassphrase.exe -v > MobSvc.passphrase
    ```
3. <span data-ttu-id="a5f5c-118">Armazene o arquivo de senha de saudação em um local seguro.</span><span class="sxs-lookup"><span data-stu-id="a5f5c-118">Store hello passphrase file in a secure location.</span></span> <span data-ttu-id="a5f5c-119">Use o arquivo hello durante a instalação do serviço de mobilidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="a5f5c-119">You use hello file during hello Mobility Service installation.</span></span>
4. <span data-ttu-id="a5f5c-120">Instaladores de serviço de mobilidade para todos os sistemas operacionais com suporte estão na pasta de %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository de saudação.</span><span class="sxs-lookup"><span data-stu-id="a5f5c-120">Mobility Service installers for all supported operating systems are in hello %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository folder.</span></span>

### <a name="mobility-service-installer-to-operating-system-mapping"></a><span data-ttu-id="a5f5c-121">Mapeamento do instalador para o sistema operacional do Serviço de Mobilidade</span><span class="sxs-lookup"><span data-stu-id="a5f5c-121">Mobility Service installer-to-operating system mapping</span></span>

| <span data-ttu-id="a5f5c-122">Nome do modelo do arquivo do instalador</span><span class="sxs-lookup"><span data-stu-id="a5f5c-122">Installer file template name</span></span>| <span data-ttu-id="a5f5c-123">Sistema operacional</span><span class="sxs-lookup"><span data-stu-id="a5f5c-123">Operating system</span></span> |
|---|--|
|<span data-ttu-id="a5f5c-124">Microsoft-ASR\_UA\*Windows\*release.exe</span><span class="sxs-lookup"><span data-stu-id="a5f5c-124">Microsoft-ASR\_UA\*Windows\*release.exe</span></span> | <span data-ttu-id="a5f5c-125">Windows Server 2008 R2 SP1 (64 bits)</span><span class="sxs-lookup"><span data-stu-id="a5f5c-125">Windows Server 2008 R2 SP1 (64-bit)</span></span> </br> <span data-ttu-id="a5f5c-126">Windows Server 2012 (64 bits)</span><span class="sxs-lookup"><span data-stu-id="a5f5c-126">Windows Server 2012 (64-bit)</span></span> </br> <span data-ttu-id="a5f5c-127">Windows Server 2012 R2 (64 bits)</span><span class="sxs-lookup"><span data-stu-id="a5f5c-127">Windows Server 2012 R2 (64-bit)</span></span> |
|<span data-ttu-id="a5f5c-128">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="a5f5c-128">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span></span>| <span data-ttu-id="a5f5c-129">RHEL (Red Hat Enterprise Linux) 6.4, 6.5, 6.6, 6.7, 6.8 (somente 64 bits)</span><span class="sxs-lookup"><span data-stu-id="a5f5c-129">Red Hat Enterprise Linux (RHEL) 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> </br> <span data-ttu-id="a5f5c-130">CentOS 6.4, 6.5, 6.6, 6.7, 6.8 (somente 64 bits)</span><span class="sxs-lookup"><span data-stu-id="a5f5c-130">CentOS 6.4, 6.5, 6.6, 6.7, 6.8 (64-bit only)</span></span> |
|<span data-ttu-id="a5f5c-131">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="a5f5c-131">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span></span> | <span data-ttu-id="a5f5c-132">Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (somente 64 bits)</span><span class="sxs-lookup"><span data-stu-id="a5f5c-132">Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (64-bit only)</span></span> </br> <span data-ttu-id="a5f5c-133">CentOS 7.0, 7.1, 7.2 (somente 64 bits)</span><span class="sxs-lookup"><span data-stu-id="a5f5c-133">CentOS 7.0, 7.1, 7.2 (64-bit only)</span></span></br> <span data-ttu-id="a5f5c-134">CentOs 7.3 (somente migração)</span><span class="sxs-lookup"><span data-stu-id="a5f5c-134">CentOs 7.3 (migration only)</span></span> |
|<span data-ttu-id="a5f5c-135">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="a5f5c-135">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span></span>| <span data-ttu-id="a5f5c-136">SUSE Linux Enterprise Server 11 SP3 (somente 64 bits)</span><span class="sxs-lookup"><span data-stu-id="a5f5c-136">SUSE Linux Enterprise Server 11 SP3 (64-bit only)</span></span>|
|<span data-ttu-id="a5f5c-137">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="a5f5c-137">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span></span>| <span data-ttu-id="a5f5c-138">SUSE Linux Enterprise Server 11 SP4 (somente 64 bits)</span><span class="sxs-lookup"><span data-stu-id="a5f5c-138">SUSE Linux Enterprise Server 11 SP4 (64-bit only)</span></span>|
|<span data-ttu-id="a5f5c-139">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="a5f5c-139">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span></span> | <span data-ttu-id="a5f5c-140">Oracle Enterprise Linux 6.4, 6.5 (somente 64 bits)</span><span class="sxs-lookup"><span data-stu-id="a5f5c-140">Oracle Enterprise Linux 6.4, 6.5 (64-bit only)</span></span>|
|<span data-ttu-id="a5f5c-141">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="a5f5c-141">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span></span> | <span data-ttu-id="a5f5c-142">Ubuntu Linux 14.04 (somente 64 bits)</span><span class="sxs-lookup"><span data-stu-id="a5f5c-142">Ubuntu Linux 14.04 (64-bit only)</span></span>|


## <a name="install-mobility-service-manually-by-using-hello-gui"></a><span data-ttu-id="a5f5c-143">Instalar serviço de mobilidade manualmente usando a GUI do hello</span><span class="sxs-lookup"><span data-stu-id="a5f5c-143">Install Mobility Service manually by using hello GUI</span></span>

>[!IMPORTANT]
> <span data-ttu-id="a5f5c-144">Se você estiver usando um **servidor de configuração** tooreplicate **máquinas virtuais do Azure IaaS** de um tooanother região da assinatura do Azure, em seguida, **usar saudação de linha de comando de instalação com base**  método</span><span class="sxs-lookup"><span data-stu-id="a5f5c-144">If you are using a **Configuration Server** tooreplicate **Azure IaaS virtual machines** from one Azure Subscription/Region tooanother then **use hello Command-line based installation** method</span></span>

[!INCLUDE [site-recovery-install-mob-svc-gui](../../includes/site-recovery-install-mob-svc-gui.md)]

## <a name="install-mobility-service-manually-at-a-command-prompt"></a><span data-ttu-id="a5f5c-145">Instalar o Serviço de Mobilidade manualmente em um prompt de comando</span><span class="sxs-lookup"><span data-stu-id="a5f5c-145">Install Mobility Service manually at a command prompt</span></span>

### <a name="command-line-installation-on-a-windows-computer"></a><span data-ttu-id="a5f5c-146">Instalação de linha de comando em um computador Windows</span><span class="sxs-lookup"><span data-stu-id="a5f5c-146">Command-line installation on a Windows computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-win-cmd](../../includes/site-recovery-install-mob-svc-win-cmd.md)]

### <a name="command-line-installation-on-a-linux-computer"></a><span data-ttu-id="a5f5c-147">Instalação de linha de comando em um computador Linux</span><span class="sxs-lookup"><span data-stu-id="a5f5c-147">Command-line installation on a Linux computer</span></span>
[!INCLUDE [site-recovery-install-mob-svc-lin-cmd](../../includes/site-recovery-install-mob-svc-lin-cmd.md)]


## <a name="install-mobility-service-by-push-installation-from-azure-site-recovery"></a><span data-ttu-id="a5f5c-148">Instalar o Serviço de Mobilidade usando a instalação por push por meio do Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="a5f5c-148">Install Mobility Service by push installation from Azure Site Recovery</span></span>
<span data-ttu-id="a5f5c-149">toodo uma instalação por push do serviço de mobilidade usando recuperação de Site, todos os computadores de destino devem atender aos Olá pré-requisitos a seguir.</span><span class="sxs-lookup"><span data-stu-id="a5f5c-149">toodo a push installation of Mobility Service by using Site Recovery, all target computers must meet hello following prerequisites.</span></span>

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-win](../../includes/site-recovery-prepare-push-install-mob-svc-win.md)]

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-lin](../../includes/site-recovery-prepare-push-install-mob-svc-lin.md)]


> [!NOTE]
<span data-ttu-id="a5f5c-150">Depois de instalar o serviço de mobilidade, em Olá portal do Azure, selecione Olá **replicar** toostart botão proteger essas VMs.</span><span class="sxs-lookup"><span data-stu-id="a5f5c-150">After Mobility Service is installed, in hello Azure portal, select hello **Replicate** button toostart protecting these VMs.</span></span>

## <a name="uninstall-mobility-service-on-a-windows-server-computer"></a><span data-ttu-id="a5f5c-151">Desinstalar o Serviço de Mobilidade de um computador Windows Server</span><span class="sxs-lookup"><span data-stu-id="a5f5c-151">Uninstall Mobility Service on a Windows Server computer</span></span>
<span data-ttu-id="a5f5c-152">Use um dos Olá métodos toouninstall serviço de mobilidade a seguir em um computador Windows Server.</span><span class="sxs-lookup"><span data-stu-id="a5f5c-152">Use one of hello following methods toouninstall Mobility Service on a Windows Server computer.</span></span>

### <a name="uninstall-by-using-hello-gui"></a><span data-ttu-id="a5f5c-153">Desinstalar usando a GUI do hello</span><span class="sxs-lookup"><span data-stu-id="a5f5c-153">Uninstall by using hello GUI</span></span>
1. <span data-ttu-id="a5f5c-154">No Painel de Controle, selecione **Programas**.</span><span class="sxs-lookup"><span data-stu-id="a5f5c-154">In Control Panel, select **Programs**.</span></span>
2. <span data-ttu-id="a5f5c-155">Selecione **Serviço de Mobilidade do Microsoft Azure Site Recovery/servidor de Destino Mestre** e, em seguida, **Desinstalar**.</span><span class="sxs-lookup"><span data-stu-id="a5f5c-155">Select **Microsoft Azure Site Recovery Mobility Service/Master Target server**, and then select **Uninstall**.</span></span>

### <a name="uninstall-at-a-command-prompt"></a><span data-ttu-id="a5f5c-156">Desinstalar em um prompt de comando</span><span class="sxs-lookup"><span data-stu-id="a5f5c-156">Uninstall at a command prompt</span></span>
1. <span data-ttu-id="a5f5c-157">Abra uma janela de Prompt de comando como administrador.</span><span class="sxs-lookup"><span data-stu-id="a5f5c-157">Open a Command Prompt window as an administrator.</span></span>
2. <span data-ttu-id="a5f5c-158">toouninstall serviço de mobilidade, executar Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="a5f5c-158">toouninstall Mobility Service, run hello following command:</span></span>

```
MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
```

## <a name="uninstall-mobility-service-on-a-linux-computer"></a><span data-ttu-id="a5f5c-159">Desinstalar o Serviço de Mobilidade de um computador Linux</span><span class="sxs-lookup"><span data-stu-id="a5f5c-159">Uninstall Mobility Service on a Linux computer</span></span>
1. <span data-ttu-id="a5f5c-160">No servidor Linux, entre como um usuário **raiz**.</span><span class="sxs-lookup"><span data-stu-id="a5f5c-160">On your Linux server, sign in as a **root** user.</span></span>
2. <span data-ttu-id="a5f5c-161">Em um terminal vá muito/usuário/local/ASR.</span><span class="sxs-lookup"><span data-stu-id="a5f5c-161">In a terminal, go too/user/local/ASR.</span></span>
3. <span data-ttu-id="a5f5c-162">toouninstall serviço de mobilidade, executar Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="a5f5c-162">toouninstall Mobility Service, run hello following command:</span></span>

```
uninstall.sh -Y
```
