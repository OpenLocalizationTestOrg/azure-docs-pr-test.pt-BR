---
title: "aaaAutomate a instalação do serviço de mobilidade para o Azure Site Recovery usando ferramentas de implantação de software | Microsoft Docs"
description: "Este artigo ajudará você a automatizar a instalação do Serviço de Mobilidade usando ferramentas de implantação de software, como o System Center Configuration Manager."
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: 6c883c6d5308dcec6e0628b0c2196b3a12e08ebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-mobility-service-installation-by-using-software-deployment-tools"></a>Automatizar a instalação do Serviço de Mobilidade usando ferramentas de implantação de software

>[!IMPORTANT]
Este documento presume que você esteja usando a versão **9.9.4510.1** ou superior.

Este artigo fornece um exemplo de como você pode usar o System Center Configuration Manager toodeploy Olá serviço de mobilidade do Azure Site Recovery no seu datacenter. Usando uma ferramenta de implantação de software como o Configuration Manager tem Olá vantagens a seguir:
* Agendamento de implantação de novas instalações e atualizações, durante a janela de manutenção planejada para atualizações de software
* Dimensionamento toohundreds implantação de servidores simultaneamente


> [!NOTE]
> Este artigo usa a atividade de implantação do System Center Configuration Manager 2012 R2 toodemonstrate hello. Você também poderá automatizar a instalação do Serviço de Mobilidade usando a [Automação do Azure e a Configuração de Estado Desejado](site-recovery-automate-mobility-service-install.md).

## <a name="prerequisites"></a>Pré-requisitos
1. Uma ferramenta de implantação de software, como o Configuration Manager, já está implantada no ambiente.
  Criar dois [coleções de dispositivos](https://technet.microsoft.com/library/gg682169.aspx), um para todos os **servidores Windows**e outro para todos os **servidores Linux**, que você deseja tooprotect usando a recuperação de Site.
3. Um servidor de configuração que já está registrado no Site Recovery.
4. Um rede segura compartilhamento de arquivos (compartilhamento Server Message Block) que pode ser acessado pelo servidor do Configuration Manager hello.

## <a name="deploy-mobility-service-on-computers-running-windows"></a>Implantar o Serviço de Mobilidade em computadores que executam o Windows
> [!NOTE]
> Este artigo pressupõe que o endereço IP de saudação saudação do servidor de configuração é 192.168.3.121, e esse compartilhamento de arquivos de rede segura Olá \\\ContosoSecureFS\MobilityServiceInstallers.

### <a name="step-1-prepare-for-deployment"></a>Etapa 1: Preparar para a implantação
1. Crie uma pasta no compartilhamento de rede hello e nomeie- **MobSvcWindows**.
2. Entre no servidor de configuração de tooyour e abra um prompt de comando administrativo.
3. Execute Olá comandos toogenerate um arquivo de senha a seguir:

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. Saudação de cópia **MobSvc.passphrase** arquivo hello **MobSvcWindows** pasta no compartilhamento de rede.
5. Procure toohello repositório de instalador no servidor de configuração de saudação executando Olá comando a seguir:

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. Saudação de cópia  **Microsoft ASR\_UA\_*versão*\_Windows\_GA\_*data* \_ Release.exe** toohello **MobSvcWindows** pasta no compartilhamento de rede.
7. Copiar Olá código a seguir e salve-o como **install.bat** em Olá **MobSvcWindows** pasta.

   > [!NOTE]
   > Substitua espaços reservados de saudação [CSIP] no script com valores reais de saudação do endereço IP de saudação do seu servidor de configuração.

```DOS
Time /t >> C:\Temp\logfile.log
REM ==================================================
REM ==== Clean up hello folders ========================
RMDIR /S /q %temp%\MobSvc
MKDIR %Temp%\MobSvc
MKDIR C:\Temp
REM ==================================================

REM ==== Copy new files ==============================
COPY M*.* %Temp%\MobSvc
CD %Temp%\MobSvc
REN Micro*.exe MobSvcInstaller.exe
REM ==================================================

REM ==== Extract hello installer =======================
MobSvcInstaller.exe /q /x:%Temp%\MobSvc\Extracted
REM ==== Wait 10s for extraction toocomplete =========
TIMEOUT /t 10
REM =================================================

REM ==== Perform installation =======================
REM =================================================

CD %Temp%\MobSvc\Extracted
whoami >> C:\Temp\logfile.log
SET PRODKEY=HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall
REG QUERY %PRODKEY%\{275197FC-14FD-4560-A5EB-38217F80CBD1}
IF NOT %ERRORLEVEL% EQU 0 (
    echo "Product is not installed. Goto INSTALL." >> C:\Temp\logfile.log
    GOTO :INSTALL
) ELSE (
    echo "Product is installed." >> C:\Temp\logfile.log

    echo "Checking for Post-install action status." >> C:\Temp\logfile.log
    GOTO :POSTINSTALLCHECK
)

:POSTINSTALLCHECK
    REG QUERY "HKLM\SOFTWARE\Wow6432Node\InMage Systems\Installed Products\5" /v "PostInstallActions" | Find "Succeeded"
    If %ERRORLEVEL% EQU 0 (
        echo "Post-install actions succeeded. Checking for Configuration status." >> C:\Temp\logfile.log
        GOTO :CONFIGURATIONCHECK
    ) ELSE (
        echo "Post-install actions didn't succeed. Goto INSTALL." >> C:\Temp\logfile.log
        GOTO :INSTALL
    )

:CONFIGURATIONCHECK
    REG QUERY "HKLM\SOFTWARE\Wow6432Node\InMage Systems\Installed Products\5" /v "AgentConfigurationStatus" | Find "Succeeded"
    If %ERRORLEVEL% EQU 0 (
        echo "Configuration has succeeded. Goto UPGRADE." >> C:\Temp\logfile.log
        GOTO :UPGRADE
    ) ELSE (
        echo "Configuration didn't succeed. Goto CONFIGURE." >> C:\Temp\logfile.log
        GOTO :CONFIGURE
    )


:INSTALL
    echo "Perform installation." >> C:\Temp\logfile.log
    UnifiedAgent.exe /Role MS /InstallLocation "C:\Program Files (x86)\Microsoft Azure Site Recovery" /Platform "VmWare" /Silent
    IF %ERRORLEVEL% EQU 0 (
        echo "Installation has succeeded." >> C:\Temp\logfile.log
        (GOTO :CONFIGURE)
    ) ELSE (
        echo "Installation has failed." >> C:\Temp\logfile.log
        GOTO :ENDSCRIPT
    )

:CONFIGURE
    echo "Perform configuration." >> C:\Temp\logfile.log
    cd "C:\Program Files (x86)\Microsoft Azure Site Recovery\agent"
    UnifiedAgentConfigurator.exe  /CSEndPoint "[CSIP]" /PassphraseFilePath %Temp%\MobSvc\MobSvc.passphrase
    IF %ERRORLEVEL% EQU 0 (
        echo "Configuration has succeeded." >> C:\Temp\logfile.log
    ) ELSE (
        echo "Configuration has failed." >> C:\Temp\logfile.log
    )
    GOTO :ENDSCRIPT

:UPGRADE
    echo "Perform upgrade." >> C:\Temp\logfile.log
    UnifiedAgent.exe /Platform "VmWare" /Silent
    IF %ERRORLEVEL% EQU 0 (
        echo "Upgrade has succeeded." >> C:\Temp\logfile.log
    ) ELSE (
        echo "Upgrade has failed." >> C:\Temp\logfile.log
    )
    GOTO :ENDSCRIPT

:ENDSCRIPT
    echo "End of script." >> C:\Temp\logfile.log


```

### <a name="step-2-create-a-package"></a>Etapa 2: Criar um pacote

1. Faça logon no console do Configuration Manager tooyour.
2. Procurar muito**biblioteca de Software** > **gerenciamento de aplicativos** > **pacotes**.
3. Clique com o botão direito do mouse em **Pacotes** e selecione **Criar Pacote**.
4. Forneça valores para a versão, descrição, fabricante, linguagem e nome de saudação.
5. Selecione Olá **este pacote contém arquivos de origem** caixa de seleção.
6. Clique em **procurar**e compartilhamento de rede hello selecione onde está armazenado o instalador de saudação (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).

  ![Captura de tela do Assistente para Criar Pacote e Programa](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package.png)

7. Em Olá **Escolher tipo de programa de saudação que você deseja toocreate** página, selecione **programa padrão**e clique em **próximo**.

  ![Captura de tela do Assistente para Criar Pacote e Programa](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. Em Olá **especificar informações sobre este programa padrão** página, forneça Olá entradas a seguir e clique em **próximo**. (hello outras entradas podem usar seus valores padrão.)

  | **Nome do parâmetro** | **Valor** |
  |--|--|
  | Nome | Instalar o Serviço de Mobilidade do Microsoft Azure (Windows) |
  | Linha de comando | install.bat |
  | Programa pode ser executado | Se um usuário fez logon ou não |

  ![Captura de tela do Assistente para Criar Pacote e Programa](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties.png)

9. Na página seguinte do hello, selecione Olá sistemas de operacionais de destino. O Serviço de Mobilidade pode ser instalado somente no Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008 R2.

  ![Captura de tela do Assistente para Criar Pacote e Programa](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2.png)

10. Assistente de saudação toocomplete, clique em **próximo** duas vezes.


> [!NOTE]
> script Hello dá suporte a ambas as novas instalações de agentes do serviço de mobilidade e atualiza tooagents que já estão instalados.

### <a name="step-3-deploy-hello-package"></a>Etapa 3: Implantar o pacote de saudação
1. No console do Configuration Manager hello, seu pacote e selecione **distribuir conteúdo**.
  ![Captura de tela do console do Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)
2. Selecione Olá  **[pontos de distribuição](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**  em toowhich pacotes Olá devem ser copiados.
3. Assistente de saudação concluída. pacote Hello, em seguida, inicia a replicação toohello especificado pontos de distribuição.
4. Após ter feita a distribuição do pacote hello, pacote hello e selecione **implantar**.
  ![Captura de tela do console do Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)
5. Selecione coleção de dispositivos do Windows Server Olá criado na seção pré-requisitos de saudação como coleção de destino Olá para implantação.

  ![Captura de tela do Assistente de Implantação de Software](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection.png)

6. Em Olá **especificar destino de conteúdo Olá** página, selecione seu **pontos de distribuição**.
7. Em Olá **toocontrol de configurações de especificar como este software é implantado** página, certifique-se de que o objetivo de saudação é **necessária**.

  ![Captura de tela do Assistente de Implantação de Software](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. Em Olá **especificar agendamento de saudação para essa implantação** página, especifique uma agenda. Para obter mais informações, consulte [Agendando pacotes](https://technet.microsoft.com/library/gg682178.aspx).
9. Em Olá **pontos de distribuição** página, configurar propriedades de saudação de acordo com as necessidades de toohello do seu datacenter. Conclua o Assistente de saudação.

> [!TIP]
> reinicializa tooavoid desnecessário, agenda Olá a instalação do pacote durante sua janela de manutenção mensal ou a janela atualizações de software.

Você pode monitorar o progresso da implantação hello usando o console do Configuration Manager hello. Vá muito**monitoramento** > **implantações** > *[nome do pacote]*.

  ![Implantações de toomonitor de opção de captura de tela do Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/report.PNG)

## <a name="deploy-mobility-service-on-computers-running-linux"></a>Implantar o Serviço de Mobilidade em computadores que executam o Linux
> [!NOTE]
> Este artigo pressupõe que o endereço IP de saudação saudação do servidor de configuração é 192.168.3.121, e esse compartilhamento de arquivos de rede segura Olá \\\ContosoSecureFS\MobilityServiceInstallers.

### <a name="step-1-prepare-for-deployment"></a>Etapa 1: Preparar para a implantação
1. Crie uma pasta no compartilhamento de rede hello e nomeie-o como **MobSvcLinux**.
2. Entre no servidor de configuração de tooyour e abra um prompt de comando administrativo.
3. Execute Olá comandos toogenerate um arquivo de senha a seguir:

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. Saudação de cópia **MobSvc.passphrase** arquivo hello **MobSvcLinux** pasta no compartilhamento de rede.
5. Procure toohello repositório de instalador no servidor de configuração de saudação executando o comando hello:

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. A seguir Olá copiar arquivos toohello **MobSvcLinux** pasta no compartilhamento de rede:
   * Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz
   * Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz
   * Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz
   * Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz
   * Microsoft-ASR\_UA\*OL6-64\*release.tar.gz
   * Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz


7. Copiar Olá código a seguir e salve-o como **install_linux.sh** em Olá **MobSvcLinux** pasta.
   > [!NOTE]
   > Substitua espaços reservados de saudação [CSIP] no script com valores reais de saudação do endereço IP de saudação do seu servidor de configuração.

```Bash
#!/usr/bin/env bash

rm -rf /tmp/MobSvc
mkdir -p /tmp/MobSvc
INSTALL_DIR='/usr/local/ASR'
VX_VERSION_FILE='/usr/local/.vx_version'

echo "=============================" >> /tmp/MobSvc/sccm.log
echo `date` >> /tmp/MobSvc/sccm.log
echo "=============================" >> /tmp/MobSvc/sccm.log

if [ -f /etc/oracle-release ] && [ -f /etc/redhat-release ]; then
    if grep -q 'Oracle Linux Server release 6.*' /etc/oracle-release; then
        if uname -a | grep -q x86_64; then
            OS="OL6-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *OL6*.tar.gz /tmp/MobSvc
        fi
    fi
elif [ -f /etc/redhat-release ]; then
    if grep -q 'Red Hat Enterprise Linux Server release 6.* (Santiago)' /etc/redhat-release || \
        grep -q 'CentOS Linux release 6.* (Final)' /etc/redhat-release || \
        grep -q 'CentOS release 6.* (Final)' /etc/redhat-release; then
        if uname -a | grep -q x86_64; then
            OS="RHEL6-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *RHEL6*.tar.gz /tmp/MobSvc
        fi
    elif grep -q 'Red Hat Enterprise Linux Server release 7.* (Maipo)' /etc/redhat-release || \
        grep -q 'CentOS Linux release 7.* (Core)' /etc/redhat-release; then
        if uname -a | grep -q x86_64; then
            OS="RHEL7-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *RHEL7*.tar.gz /tmp/MobSvc
                fi
    fi
elif [ -f /etc/SuSE-release ] && grep -q 'VERSION = 11' /etc/SuSE-release; then
    if grep -q "SUSE Linux Enterprise Server 11" /etc/SuSE-release && grep -q 'PATCHLEVEL = 3' /etc/SuSE-release; then
        if uname -a | grep -q x86_64; then
            OS="SLES11-SP3-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *SLES11-SP3*.tar.gz /tmp/MobSvc
        fi
    elif grep -q "SUSE Linux Enterprise Server 11" /etc/SuSE-release && grep -q 'PATCHLEVEL = 4' /etc/SuSE-release; then
        if uname -a | grep -q x86_64; then
            OS="SLES11-SP4-64"
            echo $OS >> /tmp/MobSvc/sccm.log
            cp *SLES11-SP4*.tar.gz /tmp/MobSvc
        fi
    fi
elif [ -f /etc/lsb-release ] ; then
    if grep -q 'DISTRIB_RELEASE=14.04' /etc/lsb-release ; then
       if uname -a | grep -q x86_64; then
           OS="UBUNTU-14.04-64"
           echo $OS >> /tmp/MobSvc/sccm.log
           cp *UBUNTU-14*.tar.gz /tmp/MobSvc
       fi
    fi
else
    exit 1
fi

if [ -z "$OS" ]; then
    exit 1
fi

Install()
{
    echo "Perform Installation." >> /tmp/MobSvc/sccm.log
    ./install -q -d ${INSTALL_DIR} -r MS -v VmWare
    RET_VAL=$?
    echo "Installation Returncode: $RET_VAL" >> /tmp/MobSvc/sccm.log
    if [ $RET_VAL -eq 0 ]; then
        echo "Installation has succeeded. Proceed tooconfiguration." >> /tmp/MobSvc/sccm.log
        Configure
    else
        echo "Installation has failed." >> /tmp/MobSvc/sccm.log
        exit $RET_VAL
    fi
}

Configure()
{
    echo "Perform configuration." >> /tmp/MobSvc/sccm.log
    ${INSTALL_DIR}/Vx/bin/UnifiedAgentConfigurator.sh -i [CSIP] -P MobSvc.passphrase
    RET_VAL=$?
    echo "Configuration Returncode: $RET_VAL" >> /tmp/MobSvc/sccm.log
    if [ $RET_VAL -eq 0 ]; then
        echo "Configuration has succeeded." >> /tmp/MobSvc/sccm.log
    else
        echo "Configuration has failed." >> /tmp/MobSvc/sccm.log
        exit $RET_VAL
    fi
}

Upgrade()
{
    echo "Perform Upgrade." >> /tmp/MobSvc/sccm.log
    ./install -q -v VmWare
    RET_VAL=$?
    echo "Upgrade Returncode: $RET_VAL" >> /tmp/MobSvc/sccm.log
    if [ $RET_VAL -eq 0 ]; then
        echo "Upgrade has succeeded." >> /tmp/MobSvc/sccm.log
    else
        echo "Upgrade has failed." >> /tmp/MobSvc/sccm.log
        exit $RET_VAL
    fi
}

cp MobSvc.passphrase /tmp/MobSvc
cd /tmp/MobSvc

tar -zxvf *.tar.gz

if [ -e ${VX_VERSION_FILE} ]; then
    echo "${VX_VERSION_FILE} exists. Checking for configuration status." >> /tmp/MobSvc/sccm.log
    agent_configuration=$(grep ^AGENT_CONFIGURATION_STATUS "${VX_VERSION_FILE}" | cut -d"=" -f2 | tr -d " ")
    echo "agent_configuration=$agent_configuration" >> /tmp/MobSvc/sccm.log
     if [ "$agent_configuration" == "Succeeded" ]; then
        echo "Agent is already configured. Proceed tooUpgrade." >> /tmp/MobSvc/sccm.log
        Upgrade
    else
        echo "Agent is not configured. Proceed tooConfigure." >> /tmp/MobSvc/sccm.log
        Configure
    fi
else
    Install
fi

cd /tmp

```

### <a name="step-2-create-a-package"></a>Etapa 2: Criar um pacote

1. Faça logon no console do Configuration Manager tooyour.
2. Procurar muito**biblioteca de Software** > **gerenciamento de aplicativos** > **pacotes**.
3. Clique com o botão direito do mouse em **Pacotes** e selecione **Criar Pacote**.
4. Forneça valores para a versão, descrição, fabricante, linguagem e nome de saudação.
5. Selecione Olá **este pacote contém arquivos de origem** caixa de seleção.
6. Clique em **procurar**e compartilhamento de rede hello selecione onde está armazenado o instalador de saudação (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).

  ![Captura de tela do Assistente para Criar Pacote e Programa](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package-linux.png)

7. Em Olá **Escolher tipo de programa de saudação que você deseja toocreate** página, selecione **programa padrão**e clique em **próximo**.

  ![Captura de tela do Assistente para Criar Pacote e Programa](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. Em Olá **especificar informações sobre este programa padrão** página, forneça Olá entradas a seguir e clique em **próximo**. (hello outras entradas podem usar seus valores padrão.)

    | **Nome do parâmetro** | **Valor** |
  |--|--|
  | Nome | Instalar o Serviço de Mobilidade do Microsoft Azure (Linux) |
  | Linha de comando | ./install_linux.sh |
  | Programa pode ser executado | Se um usuário fez logon ou não |

  ![Captura de tela do Assistente para Criar Pacote e Programa](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-linux.png)

9. Na próxima página do hello, selecione **este programa pode ser executado em qualquer plataforma**.
  ![Captura de tela do Assistente para Criar Pacote e Programa](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)

10. Assistente de saudação toocomplete, clique em **próximo** duas vezes.

> [!NOTE]
> script Hello dá suporte a ambas as novas instalações de agentes do serviço de mobilidade e atualiza tooagents que já estão instalados.

### <a name="step-3-deploy-hello-package"></a>Etapa 3: Implantar o pacote de saudação
1. No console do Configuration Manager hello, seu pacote e selecione **distribuir conteúdo**.
  ![Captura de tela do console do Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)
2. Selecione Olá  **[pontos de distribuição](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**  em toowhich pacotes Olá devem ser copiados.
3. Assistente de saudação concluída. pacote Hello, em seguida, inicia a replicação toohello especificado pontos de distribuição.
4. Após ter feita a distribuição do pacote hello, pacote hello e selecione **implantar**.
  ![Captura de tela do console do Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)
5. Selecione Olá criado na seção pré-requisitos de saudação como coleção de destino Olá para implantação de coleção de dispositivos de servidor Linux.

  ![Captura de tela do Assistente de Implantação de Software](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection-linux.png)

6. Em Olá **especificar destino de conteúdo Olá** página, selecione seu **pontos de distribuição**.
7. Em Olá **toocontrol de configurações de especificar como este software é implantado** página, certifique-se de que o objetivo de saudação é **necessária**.

  ![Captura de tela do Assistente de Implantação de Software](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. Em Olá **especificar agendamento de saudação para essa implantação** página, especifique uma agenda. Para obter mais informações, consulte [Agendando pacotes](https://technet.microsoft.com/library/gg682178.aspx).
9. Em Olá **pontos de distribuição** página, configurar propriedades de saudação de acordo com as necessidades de toohello do seu datacenter. Conclua o Assistente de saudação.

Serviço de mobilidade é instalado em Olá coleção de dispositivos de servidor Linux, de acordo com o agendamento de toohello que você configurou.

## <a name="other-methods-tooinstall-mobility-service"></a>Outros métodos tooinstall serviço de mobilidade
Estas são algumas outras opções para instalação do Serviço de Mobilidade:
* [Instalação manual usando GUI](http://aka.ms/mobsvcmanualinstall)
* [Instalação manual usando linha de comando](http://aka.ms/mobsvcmanualinstallcli)
* [Instalação por push usando o servidor de configuração ](http://aka.ms/pushinstall)
* [Instalação automatizada usando a Automação do Azure e a Configuração de Estado Desejado ](http://aka.ms/mobsvcdscinstall)

## <a name="uninstall-mobility-service"></a>Desinstalar o Serviço de Mobilidade
Você pode criar o Configuration Manager pacotes toouninstall serviço de mobilidade. Use Olá toodo de script a seguir para:

```
Time /t >> C:\logfile.log
REM ==================================================
REM ==== Check if Mob Svc is already installed =======
REM ==== If not installed no operation required ========
REM ==== Else run uninstall command =====================
REM ==== {275197FC-14FD-4560-A5EB-38217F80CBD1} is ====
REM ==== guid for Mob Svc Installer ====================
whoami >> C:\logfile.log
NET START | FIND "InMage Scout Application Service"
IF  %ERRORLEVEL% EQU 1 (GOTO :INSTALL) ELSE GOTO :UNINSTALL
:NOOPERATION
                echo "No Operation Required." >> c:\logfile.log
                GOTO :ENDSCRIPT
:UNINSTALL
                echo "Uninstall" >> C:\logfile.log
                MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1} /L+*V "C:\ProgramData\ASRSetupLogs\UnifiedAgentMSIUninstall.log"
:ENDSCRIPT

```

## <a name="next-steps"></a>Próximas etapas
Agora você está pronto muito[Habilitar proteção](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) para as máquinas virtuais.
