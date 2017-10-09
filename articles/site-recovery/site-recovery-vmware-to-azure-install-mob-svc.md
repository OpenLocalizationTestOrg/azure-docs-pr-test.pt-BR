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
# <a name="install-mobility-service-vmware-or-physical-tooazure"></a>Instalar serviço de mobilidade (VMware ou tooAzure físico)
Serviço de mobilidade do Azure Site Recovery captura gravações de dados em um computador e, em seguida, encaminha toohello servidor de processo. Implante o serviço de mobilidade tooevery computador (VM VMware ou servidor físico) que você deseja tooreplicate tooAzure. Você pode implantar servidores do serviço de mobilidade toohello que você deseja tooprotect usando Olá métodos a seguir:


* [Instalar o Serviço de Mobilidade usando as ferramentas de implantação de software, como o System Center Configuration Manager](site-recovery-install-mobility-service-using-sccm.md)
* [Instalar o Serviço de Mobilidade usando a Automação do Azure e o DSC de Automação (Configuração de Estado Desejado)](site-recovery-automate-mobility-service-install.md)
* [Instalar serviço de mobilidade manualmente usando a interface gráfica do usuário de saudação (GUI)](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-by-using-the-gui)
* [Instalar o Serviço de Mobilidade manualmente em um prompt de comando](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-manually-at-a-command-prompt)
* [Instalar o Serviço de Mobilidade usando a instalação por push por meio do Azure Site Recovery](site-recovery-vmware-to-azure-install-mob-svc.md#install-mobility-service-by-push-installation-from-azure-site-recovery)


>[!IMPORTANT]
> Começando com a versão 9.7.0.0, em máquinas de virtuais (VMs) do Windows hello serviço de mobilidade instalador também instala hello mais recente disponível [agente de VM do Azure](../virtual-machines/windows/extensions-features.md#azure-vm-agent). Quando um computador faz failover tooAzure, computador Olá atende aos pré-requisitos para usar qualquer extensão VM de instalação do agente de saudação.

## <a name="prerequisites"></a>Pré-requisitos
Conclua estas etapas de pré-requisito antes de instalar o Serviço de Mobilidade manualmente no servidor:
1. Entre no servidor de configuração de tooyour e, em seguida, abra uma janela de Prompt de comando como administrador.
2. Alterar pasta bin do hello diretório toohello e, em seguida, crie um arquivo de senha:

    ```
    cd %ProgramData%\ASR\home\svsystems\bin
    genpassphrase.exe -v > MobSvc.passphrase
    ```
3. Armazene o arquivo de senha de saudação em um local seguro. Use o arquivo hello durante a instalação do serviço de mobilidade de saudação.
4. Instaladores de serviço de mobilidade para todos os sistemas operacionais com suporte estão na pasta de %ProgramData%\ASR\home\svsystems\pushinstallsvc\repository de saudação.

### <a name="mobility-service-installer-to-operating-system-mapping"></a>Mapeamento do instalador para o sistema operacional do Serviço de Mobilidade

| Nome do modelo do arquivo do instalador| Sistema operacional |
|---|--|
|Microsoft-ASR\_UA\*Windows\*release.exe | Windows Server 2008 R2 SP1 (64 bits) </br> Windows Server 2012 (64 bits) </br> Windows Server 2012 R2 (64 bits) |
|Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz| RHEL (Red Hat Enterprise Linux) 6.4, 6.5, 6.6, 6.7, 6.8 (somente 64 bits) </br> CentOS 6.4, 6.5, 6.6, 6.7, 6.8 (somente 64 bits) |
|Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz | Red Hat Enterprise Linux (RHEL) 7.1, 7.2 (somente 64 bits) </br> CentOS 7.0, 7.1, 7.2 (somente 64 bits)</br> CentOs 7.3 (somente migração) |
|Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz| SUSE Linux Enterprise Server 11 SP3 (somente 64 bits)|
|Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz| SUSE Linux Enterprise Server 11 SP4 (somente 64 bits)|
|Microsoft-ASR\_UA\*OL6-64\*release.tar.gz | Oracle Enterprise Linux 6.4, 6.5 (somente 64 bits)|
|Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz | Ubuntu Linux 14.04 (somente 64 bits)|


## <a name="install-mobility-service-manually-by-using-hello-gui"></a>Instalar serviço de mobilidade manualmente usando a GUI do hello

>[!IMPORTANT]
> Se você estiver usando um **servidor de configuração** tooreplicate **máquinas virtuais do Azure IaaS** de um tooanother região da assinatura do Azure, em seguida, **usar saudação de linha de comando de instalação com base**  método

[!INCLUDE [site-recovery-install-mob-svc-gui](../../includes/site-recovery-install-mob-svc-gui.md)]

## <a name="install-mobility-service-manually-at-a-command-prompt"></a>Instalar o Serviço de Mobilidade manualmente em um prompt de comando

### <a name="command-line-installation-on-a-windows-computer"></a>Instalação de linha de comando em um computador Windows
[!INCLUDE [site-recovery-install-mob-svc-win-cmd](../../includes/site-recovery-install-mob-svc-win-cmd.md)]

### <a name="command-line-installation-on-a-linux-computer"></a>Instalação de linha de comando em um computador Linux
[!INCLUDE [site-recovery-install-mob-svc-lin-cmd](../../includes/site-recovery-install-mob-svc-lin-cmd.md)]


## <a name="install-mobility-service-by-push-installation-from-azure-site-recovery"></a>Instalar o Serviço de Mobilidade usando a instalação por push por meio do Azure Site Recovery
toodo uma instalação por push do serviço de mobilidade usando recuperação de Site, todos os computadores de destino devem atender aos Olá pré-requisitos a seguir.

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-win](../../includes/site-recovery-prepare-push-install-mob-svc-win.md)]

[!INCLUDE [site-recovery-prepare-push-install-mob-svc-lin](../../includes/site-recovery-prepare-push-install-mob-svc-lin.md)]


> [!NOTE]
Depois de instalar o serviço de mobilidade, em Olá portal do Azure, selecione Olá **replicar** toostart botão proteger essas VMs.

## <a name="uninstall-mobility-service-on-a-windows-server-computer"></a>Desinstalar o Serviço de Mobilidade de um computador Windows Server
Use um dos Olá métodos toouninstall serviço de mobilidade a seguir em um computador Windows Server.

### <a name="uninstall-by-using-hello-gui"></a>Desinstalar usando a GUI do hello
1. No Painel de Controle, selecione **Programas**.
2. Selecione **Serviço de Mobilidade do Microsoft Azure Site Recovery/servidor de Destino Mestre** e, em seguida, **Desinstalar**.

### <a name="uninstall-at-a-command-prompt"></a>Desinstalar em um prompt de comando
1. Abra uma janela de Prompt de comando como administrador.
2. toouninstall serviço de mobilidade, executar Olá comando a seguir:

```
MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
```

## <a name="uninstall-mobility-service-on-a-linux-computer"></a>Desinstalar o Serviço de Mobilidade de um computador Linux
1. No servidor Linux, entre como um usuário **raiz**.
2. Em um terminal vá muito/usuário/local/ASR.
3. toouninstall serviço de mobilidade, executar Olá comando a seguir:

```
uninstall.sh -Y
```
