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
# <a name="automate-mobility-service-installation-by-using-software-deployment-tools"></a><span data-ttu-id="92a6b-103">Automatizar a instalação do Serviço de Mobilidade usando ferramentas de implantação de software</span><span class="sxs-lookup"><span data-stu-id="92a6b-103">Automate Mobility Service installation by using software deployment tools</span></span>

>[!IMPORTANT]
<span data-ttu-id="92a6b-104">Este documento presume que você esteja usando a versão **9.9.4510.1** ou superior.</span><span class="sxs-lookup"><span data-stu-id="92a6b-104">This document assumes you are using version **9.9.4510.1** or higher.</span></span>

<span data-ttu-id="92a6b-105">Este artigo fornece um exemplo de como você pode usar o System Center Configuration Manager toodeploy Olá serviço de mobilidade do Azure Site Recovery no seu datacenter.</span><span class="sxs-lookup"><span data-stu-id="92a6b-105">This article provides you an example of how you can use System Center Configuration Manager toodeploy hello Azure Site Recovery Mobility Service in your datacenter.</span></span> <span data-ttu-id="92a6b-106">Usando uma ferramenta de implantação de software como o Configuration Manager tem Olá vantagens a seguir:</span><span class="sxs-lookup"><span data-stu-id="92a6b-106">Using a software deployment tool like Configuration Manager has hello following advantages:</span></span>
* <span data-ttu-id="92a6b-107">Agendamento de implantação de novas instalações e atualizações, durante a janela de manutenção planejada para atualizações de software</span><span class="sxs-lookup"><span data-stu-id="92a6b-107">Scheduling deployment of fresh installations and upgrades, during your planned maintenance window for software updates</span></span>
* <span data-ttu-id="92a6b-108">Dimensionamento toohundreds implantação de servidores simultaneamente</span><span class="sxs-lookup"><span data-stu-id="92a6b-108">Scaling deployment toohundreds of servers simultaneously</span></span>


> [!NOTE]
> <span data-ttu-id="92a6b-109">Este artigo usa a atividade de implantação do System Center Configuration Manager 2012 R2 toodemonstrate hello.</span><span class="sxs-lookup"><span data-stu-id="92a6b-109">This article uses System Center Configuration Manager 2012 R2 toodemonstrate hello deployment activity.</span></span> <span data-ttu-id="92a6b-110">Você também poderá automatizar a instalação do Serviço de Mobilidade usando a [Automação do Azure e a Configuração de Estado Desejado](site-recovery-automate-mobility-service-install.md).</span><span class="sxs-lookup"><span data-stu-id="92a6b-110">You could also automate Mobility Service installation by using [Azure Automation and Desired State Configuration](site-recovery-automate-mobility-service-install.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92a6b-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="92a6b-111">Prerequisites</span></span>
1. <span data-ttu-id="92a6b-112">Uma ferramenta de implantação de software, como o Configuration Manager, já está implantada no ambiente.</span><span class="sxs-lookup"><span data-stu-id="92a6b-112">A software deployment tool, like Configuration Manager, that is already deployed in your environment.</span></span>
  <span data-ttu-id="92a6b-113">Criar dois [coleções de dispositivos](https://technet.microsoft.com/library/gg682169.aspx), um para todos os **servidores Windows**e outro para todos os **servidores Linux**, que você deseja tooprotect usando a recuperação de Site.</span><span class="sxs-lookup"><span data-stu-id="92a6b-113">Create two [device collections](https://technet.microsoft.com/library/gg682169.aspx), one for all **Windows servers**, and another for all **Linux servers**, that you want tooprotect by using Site Recovery.</span></span>
3. <span data-ttu-id="92a6b-114">Um servidor de configuração que já está registrado no Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="92a6b-114">A configuration server that is already registered with Site Recovery.</span></span>
4. <span data-ttu-id="92a6b-115">Um rede segura compartilhamento de arquivos (compartilhamento Server Message Block) que pode ser acessado pelo servidor do Configuration Manager hello.</span><span class="sxs-lookup"><span data-stu-id="92a6b-115">A secure network file share (Server Message Block share) that can be accessed by hello Configuration Manager server.</span></span>

## <a name="deploy-mobility-service-on-computers-running-windows"></a><span data-ttu-id="92a6b-116">Implantar o Serviço de Mobilidade em computadores que executam o Windows</span><span class="sxs-lookup"><span data-stu-id="92a6b-116">Deploy Mobility Service on computers running Windows</span></span>
> [!NOTE]
> <span data-ttu-id="92a6b-117">Este artigo pressupõe que o endereço IP de saudação saudação do servidor de configuração é 192.168.3.121, e esse compartilhamento de arquivos de rede segura Olá \\\ContosoSecureFS\MobilityServiceInstallers.</span><span class="sxs-lookup"><span data-stu-id="92a6b-117">This article assumes that hello IP address of hello configuration server is 192.168.3.121, and that hello secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="92a6b-118">Etapa 1: Preparar para a implantação</span><span class="sxs-lookup"><span data-stu-id="92a6b-118">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="92a6b-119">Crie uma pasta no compartilhamento de rede hello e nomeie- **MobSvcWindows**.</span><span class="sxs-lookup"><span data-stu-id="92a6b-119">Create a folder on hello network share, and name it **MobSvcWindows**.</span></span>
2. <span data-ttu-id="92a6b-120">Entre no servidor de configuração de tooyour e abra um prompt de comando administrativo.</span><span class="sxs-lookup"><span data-stu-id="92a6b-120">Sign in tooyour configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="92a6b-121">Execute Olá comandos toogenerate um arquivo de senha a seguir:</span><span class="sxs-lookup"><span data-stu-id="92a6b-121">Run hello following commands toogenerate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="92a6b-122">Saudação de cópia **MobSvc.passphrase** arquivo hello **MobSvcWindows** pasta no compartilhamento de rede.</span><span class="sxs-lookup"><span data-stu-id="92a6b-122">Copy hello **MobSvc.passphrase** file into hello **MobSvcWindows** folder on your network share.</span></span>
5. <span data-ttu-id="92a6b-123">Procure toohello repositório de instalador no servidor de configuração de saudação executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="92a6b-123">Browse toohello installer repository on hello configuration server by running hello following command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="92a6b-124">Saudação de cópia  **Microsoft ASR\_UA\_*versão*\_Windows\_GA\_*data* \_ Release.exe** toohello **MobSvcWindows** pasta no compartilhamento de rede.</span><span class="sxs-lookup"><span data-stu-id="92a6b-124">Copy hello **Microsoft-ASR\_UA\_*version*\_Windows\_GA\_*date*\_Release.exe** toohello **MobSvcWindows** folder on your network share.</span></span>
7. <span data-ttu-id="92a6b-125">Copiar Olá código a seguir e salve-o como **install.bat** em Olá **MobSvcWindows** pasta.</span><span class="sxs-lookup"><span data-stu-id="92a6b-125">Copy hello following code, and save it as **install.bat** into hello **MobSvcWindows** folder.</span></span>

   > [!NOTE]
   > <span data-ttu-id="92a6b-126">Substitua espaços reservados de saudação [CSIP] no script com valores reais de saudação do endereço IP de saudação do seu servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="92a6b-126">Replace hello [CSIP] placeholders in this script with hello actual values of hello IP address of your configuration server.</span></span>

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

### <a name="step-2-create-a-package"></a><span data-ttu-id="92a6b-127">Etapa 2: Criar um pacote</span><span class="sxs-lookup"><span data-stu-id="92a6b-127">Step 2: Create a package</span></span>

1. <span data-ttu-id="92a6b-128">Faça logon no console do Configuration Manager tooyour.</span><span class="sxs-lookup"><span data-stu-id="92a6b-128">Sign in tooyour Configuration Manager console.</span></span>
2. <span data-ttu-id="92a6b-129">Procurar muito**biblioteca de Software** > **gerenciamento de aplicativos** > **pacotes**.</span><span class="sxs-lookup"><span data-stu-id="92a6b-129">Browse too**Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="92a6b-130">Clique com o botão direito do mouse em **Pacotes** e selecione **Criar Pacote**.</span><span class="sxs-lookup"><span data-stu-id="92a6b-130">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="92a6b-131">Forneça valores para a versão, descrição, fabricante, linguagem e nome de saudação.</span><span class="sxs-lookup"><span data-stu-id="92a6b-131">Provide values for hello name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="92a6b-132">Selecione Olá **este pacote contém arquivos de origem** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="92a6b-132">Select hello **This package contains source files** check box.</span></span>
6. <span data-ttu-id="92a6b-133">Clique em **procurar**e compartilhamento de rede hello selecione onde está armazenado o instalador de saudação (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).</span><span class="sxs-lookup"><span data-stu-id="92a6b-133">Click **Browse**, and select hello network share where hello installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).</span></span>

  ![Captura de tela do Assistente para Criar Pacote e Programa](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package.png)

7. <span data-ttu-id="92a6b-135">Em Olá **Escolher tipo de programa de saudação que você deseja toocreate** página, selecione **programa padrão**e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="92a6b-135">On hello **Choose hello program type that you want toocreate** page, select **Standard Program**, and click **Next**.</span></span>

  ![Captura de tela do Assistente para Criar Pacote e Programa](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="92a6b-137">Em Olá **especificar informações sobre este programa padrão** página, forneça Olá entradas a seguir e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="92a6b-137">On hello **Specify information about this standard program** page, provide hello following inputs, and click **Next**.</span></span> <span data-ttu-id="92a6b-138">(hello outras entradas podem usar seus valores padrão.)</span><span class="sxs-lookup"><span data-stu-id="92a6b-138">(hello other inputs can use their default values.)</span></span>

  | <span data-ttu-id="92a6b-139">**Nome do parâmetro**</span><span class="sxs-lookup"><span data-stu-id="92a6b-139">**Parameter name**</span></span> | <span data-ttu-id="92a6b-140">**Valor**</span><span class="sxs-lookup"><span data-stu-id="92a6b-140">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="92a6b-141">Nome</span><span class="sxs-lookup"><span data-stu-id="92a6b-141">Name</span></span> | <span data-ttu-id="92a6b-142">Instalar o Serviço de Mobilidade do Microsoft Azure (Windows)</span><span class="sxs-lookup"><span data-stu-id="92a6b-142">Install Microsoft Azure Mobility Service (Windows)</span></span> |
  | <span data-ttu-id="92a6b-143">Linha de comando</span><span class="sxs-lookup"><span data-stu-id="92a6b-143">Command line</span></span> | <span data-ttu-id="92a6b-144">install.bat</span><span class="sxs-lookup"><span data-stu-id="92a6b-144">install.bat</span></span> |
  | <span data-ttu-id="92a6b-145">Programa pode ser executado</span><span class="sxs-lookup"><span data-stu-id="92a6b-145">Program can run</span></span> | <span data-ttu-id="92a6b-146">Se um usuário fez logon ou não</span><span class="sxs-lookup"><span data-stu-id="92a6b-146">Whether or not a user is logged on</span></span> |

  ![Captura de tela do Assistente para Criar Pacote e Programa](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties.png)

9. <span data-ttu-id="92a6b-148">Na página seguinte do hello, selecione Olá sistemas de operacionais de destino.</span><span class="sxs-lookup"><span data-stu-id="92a6b-148">On hello next page, select hello target operating systems.</span></span> <span data-ttu-id="92a6b-149">O Serviço de Mobilidade pode ser instalado somente no Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="92a6b-149">Mobility Service can be installed only on Windows Server 2012 R2, Windows Server 2012, and Windows Server 2008 R2.</span></span>

  ![Captura de tela do Assistente para Criar Pacote e Programa](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2.png)

10. <span data-ttu-id="92a6b-151">Assistente de saudação toocomplete, clique em **próximo** duas vezes.</span><span class="sxs-lookup"><span data-stu-id="92a6b-151">toocomplete hello wizard, click **Next** twice.</span></span>


> [!NOTE]
> <span data-ttu-id="92a6b-152">script Hello dá suporte a ambas as novas instalações de agentes do serviço de mobilidade e atualiza tooagents que já estão instalados.</span><span class="sxs-lookup"><span data-stu-id="92a6b-152">hello script supports both new installations of Mobility Service agents and updates tooagents that are already installed.</span></span>

### <a name="step-3-deploy-hello-package"></a><span data-ttu-id="92a6b-153">Etapa 3: Implantar o pacote de saudação</span><span class="sxs-lookup"><span data-stu-id="92a6b-153">Step 3: Deploy hello package</span></span>
1. <span data-ttu-id="92a6b-154">No console do Configuration Manager hello, seu pacote e selecione **distribuir conteúdo**.</span><span class="sxs-lookup"><span data-stu-id="92a6b-154">In hello Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="92a6b-155">![Captura de tela do console do Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="92a6b-155">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="92a6b-156">Selecione Olá  **[pontos de distribuição](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**  em toowhich pacotes Olá devem ser copiados.</span><span class="sxs-lookup"><span data-stu-id="92a6b-156">Select hello **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on toowhich hello packages should be copied.</span></span>
3. <span data-ttu-id="92a6b-157">Assistente de saudação concluída.</span><span class="sxs-lookup"><span data-stu-id="92a6b-157">Complete hello wizard.</span></span> <span data-ttu-id="92a6b-158">pacote Hello, em seguida, inicia a replicação toohello especificado pontos de distribuição.</span><span class="sxs-lookup"><span data-stu-id="92a6b-158">hello package then starts replicating toohello specified distribution points.</span></span>
4. <span data-ttu-id="92a6b-159">Após ter feita a distribuição do pacote hello, pacote hello e selecione **implantar**.</span><span class="sxs-lookup"><span data-stu-id="92a6b-159">After hello package distribution is done, right-click hello package, and select **Deploy**.</span></span>
  <span data-ttu-id="92a6b-160">![Captura de tela do console do Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="92a6b-160">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="92a6b-161">Selecione coleção de dispositivos do Windows Server Olá criado na seção pré-requisitos de saudação como coleção de destino Olá para implantação.</span><span class="sxs-lookup"><span data-stu-id="92a6b-161">Select hello Windows Server device collection you created in hello prerequisites section as hello target collection for deployment.</span></span>

  ![Captura de tela do Assistente de Implantação de Software](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection.png)

6. <span data-ttu-id="92a6b-163">Em Olá **especificar destino de conteúdo Olá** página, selecione seu **pontos de distribuição**.</span><span class="sxs-lookup"><span data-stu-id="92a6b-163">On hello **Specify hello content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="92a6b-164">Em Olá **toocontrol de configurações de especificar como este software é implantado** página, certifique-se de que o objetivo de saudação é **necessária**.</span><span class="sxs-lookup"><span data-stu-id="92a6b-164">On hello **Specify settings toocontrol how this software is deployed** page, ensure that hello purpose is **Required**.</span></span>

  ![Captura de tela do Assistente de Implantação de Software](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="92a6b-166">Em Olá **especificar agendamento de saudação para essa implantação** página, especifique uma agenda.</span><span class="sxs-lookup"><span data-stu-id="92a6b-166">On hello **Specify hello schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="92a6b-167">Para obter mais informações, consulte [Agendando pacotes](https://technet.microsoft.com/library/gg682178.aspx).</span><span class="sxs-lookup"><span data-stu-id="92a6b-167">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="92a6b-168">Em Olá **pontos de distribuição** página, configurar propriedades de saudação de acordo com as necessidades de toohello do seu datacenter.</span><span class="sxs-lookup"><span data-stu-id="92a6b-168">On hello **Distribution Points** page, configure hello properties according toohello needs of your datacenter.</span></span> <span data-ttu-id="92a6b-169">Conclua o Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="92a6b-169">Then complete hello wizard.</span></span>

> [!TIP]
> <span data-ttu-id="92a6b-170">reinicializa tooavoid desnecessário, agenda Olá a instalação do pacote durante sua janela de manutenção mensal ou a janela atualizações de software.</span><span class="sxs-lookup"><span data-stu-id="92a6b-170">tooavoid unnecessary reboots, schedule hello package installation during your monthly maintenance window or software updates window.</span></span>

<span data-ttu-id="92a6b-171">Você pode monitorar o progresso da implantação hello usando o console do Configuration Manager hello.</span><span class="sxs-lookup"><span data-stu-id="92a6b-171">You can monitor hello deployment progress by using hello Configuration Manager console.</span></span> <span data-ttu-id="92a6b-172">Vá muito**monitoramento** > **implantações** > *[nome do pacote]*.</span><span class="sxs-lookup"><span data-stu-id="92a6b-172">Go too**Monitoring** > **Deployments** > *[your package name]*.</span></span>

  ![Implantações de toomonitor de opção de captura de tela do Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/report.PNG)

## <a name="deploy-mobility-service-on-computers-running-linux"></a><span data-ttu-id="92a6b-174">Implantar o Serviço de Mobilidade em computadores que executam o Linux</span><span class="sxs-lookup"><span data-stu-id="92a6b-174">Deploy Mobility Service on computers running Linux</span></span>
> [!NOTE]
> <span data-ttu-id="92a6b-175">Este artigo pressupõe que o endereço IP de saudação saudação do servidor de configuração é 192.168.3.121, e esse compartilhamento de arquivos de rede segura Olá \\\ContosoSecureFS\MobilityServiceInstallers.</span><span class="sxs-lookup"><span data-stu-id="92a6b-175">This article assumes that hello IP address of hello configuration server is 192.168.3.121, and that hello secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="92a6b-176">Etapa 1: Preparar para a implantação</span><span class="sxs-lookup"><span data-stu-id="92a6b-176">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="92a6b-177">Crie uma pasta no compartilhamento de rede hello e nomeie-o como **MobSvcLinux**.</span><span class="sxs-lookup"><span data-stu-id="92a6b-177">Create a folder on hello network share, and name it as **MobSvcLinux**.</span></span>
2. <span data-ttu-id="92a6b-178">Entre no servidor de configuração de tooyour e abra um prompt de comando administrativo.</span><span class="sxs-lookup"><span data-stu-id="92a6b-178">Sign in tooyour configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="92a6b-179">Execute Olá comandos toogenerate um arquivo de senha a seguir:</span><span class="sxs-lookup"><span data-stu-id="92a6b-179">Run hello following commands toogenerate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="92a6b-180">Saudação de cópia **MobSvc.passphrase** arquivo hello **MobSvcLinux** pasta no compartilhamento de rede.</span><span class="sxs-lookup"><span data-stu-id="92a6b-180">Copy hello **MobSvc.passphrase** file into hello **MobSvcLinux** folder on your network share.</span></span>
5. <span data-ttu-id="92a6b-181">Procure toohello repositório de instalador no servidor de configuração de saudação executando o comando hello:</span><span class="sxs-lookup"><span data-stu-id="92a6b-181">Browse toohello installer repository on hello configuration server by running hello command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="92a6b-182">A seguir Olá copiar arquivos toohello **MobSvcLinux** pasta no compartilhamento de rede:</span><span class="sxs-lookup"><span data-stu-id="92a6b-182">Copy hello following files toohello **MobSvcLinux** folder on your network share:</span></span>
   * <span data-ttu-id="92a6b-183">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="92a6b-183">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span></span>
   * <span data-ttu-id="92a6b-184">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="92a6b-184">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span></span>
   * <span data-ttu-id="92a6b-185">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="92a6b-185">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span></span>
   * <span data-ttu-id="92a6b-186">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="92a6b-186">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span></span>
   * <span data-ttu-id="92a6b-187">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="92a6b-187">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span></span>
   * <span data-ttu-id="92a6b-188">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="92a6b-188">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span></span>


7. <span data-ttu-id="92a6b-189">Copiar Olá código a seguir e salve-o como **install_linux.sh** em Olá **MobSvcLinux** pasta.</span><span class="sxs-lookup"><span data-stu-id="92a6b-189">Copy hello following code, and save it as **install_linux.sh** into hello **MobSvcLinux** folder.</span></span>
   > [!NOTE]
   > <span data-ttu-id="92a6b-190">Substitua espaços reservados de saudação [CSIP] no script com valores reais de saudação do endereço IP de saudação do seu servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="92a6b-190">Replace hello [CSIP] placeholders in this script with hello actual values of hello IP address of your configuration server.</span></span>

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

### <a name="step-2-create-a-package"></a><span data-ttu-id="92a6b-191">Etapa 2: Criar um pacote</span><span class="sxs-lookup"><span data-stu-id="92a6b-191">Step 2: Create a package</span></span>

1. <span data-ttu-id="92a6b-192">Faça logon no console do Configuration Manager tooyour.</span><span class="sxs-lookup"><span data-stu-id="92a6b-192">Sign in  tooyour Configuration Manager console.</span></span>
2. <span data-ttu-id="92a6b-193">Procurar muito**biblioteca de Software** > **gerenciamento de aplicativos** > **pacotes**.</span><span class="sxs-lookup"><span data-stu-id="92a6b-193">Browse too**Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="92a6b-194">Clique com o botão direito do mouse em **Pacotes** e selecione **Criar Pacote**.</span><span class="sxs-lookup"><span data-stu-id="92a6b-194">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="92a6b-195">Forneça valores para a versão, descrição, fabricante, linguagem e nome de saudação.</span><span class="sxs-lookup"><span data-stu-id="92a6b-195">Provide values for hello name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="92a6b-196">Selecione Olá **este pacote contém arquivos de origem** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="92a6b-196">Select hello **This package contains source files** check box.</span></span>
6. <span data-ttu-id="92a6b-197">Clique em **procurar**e compartilhamento de rede hello selecione onde está armazenado o instalador de saudação (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).</span><span class="sxs-lookup"><span data-stu-id="92a6b-197">Click **Browse**, and select hello network share where hello installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).</span></span>

  ![Captura de tela do Assistente para Criar Pacote e Programa](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package-linux.png)

7. <span data-ttu-id="92a6b-199">Em Olá **Escolher tipo de programa de saudação que você deseja toocreate** página, selecione **programa padrão**e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="92a6b-199">On hello **Choose hello program type that you want toocreate** page, select **Standard Program**, and click **Next**.</span></span>

  ![Captura de tela do Assistente para Criar Pacote e Programa](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="92a6b-201">Em Olá **especificar informações sobre este programa padrão** página, forneça Olá entradas a seguir e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="92a6b-201">On hello **Specify information about this standard program** page, provide hello following inputs, and click **Next**.</span></span> <span data-ttu-id="92a6b-202">(hello outras entradas podem usar seus valores padrão.)</span><span class="sxs-lookup"><span data-stu-id="92a6b-202">(hello other inputs can use their default values.)</span></span>

    | <span data-ttu-id="92a6b-203">**Nome do parâmetro**</span><span class="sxs-lookup"><span data-stu-id="92a6b-203">**Parameter name**</span></span> | <span data-ttu-id="92a6b-204">**Valor**</span><span class="sxs-lookup"><span data-stu-id="92a6b-204">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="92a6b-205">Nome</span><span class="sxs-lookup"><span data-stu-id="92a6b-205">Name</span></span> | <span data-ttu-id="92a6b-206">Instalar o Serviço de Mobilidade do Microsoft Azure (Linux)</span><span class="sxs-lookup"><span data-stu-id="92a6b-206">Install Microsoft Azure Mobility Service (Linux)</span></span> |
  | <span data-ttu-id="92a6b-207">Linha de comando</span><span class="sxs-lookup"><span data-stu-id="92a6b-207">Command line</span></span> | <span data-ttu-id="92a6b-208">./install_linux.sh</span><span class="sxs-lookup"><span data-stu-id="92a6b-208">./install_linux.sh</span></span> |
  | <span data-ttu-id="92a6b-209">Programa pode ser executado</span><span class="sxs-lookup"><span data-stu-id="92a6b-209">Program can run</span></span> | <span data-ttu-id="92a6b-210">Se um usuário fez logon ou não</span><span class="sxs-lookup"><span data-stu-id="92a6b-210">Whether or not a user is logged on</span></span> |

  ![Captura de tela do Assistente para Criar Pacote e Programa](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-linux.png)

9. <span data-ttu-id="92a6b-212">Na próxima página do hello, selecione **este programa pode ser executado em qualquer plataforma**.</span><span class="sxs-lookup"><span data-stu-id="92a6b-212">On hello next page, select **This program can run on any platform**.</span></span>
  <span data-ttu-id="92a6b-213">![Captura de tela do Assistente para Criar Pacote e Programa](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span><span class="sxs-lookup"><span data-stu-id="92a6b-213">![Screenshot of Create Package and Program wizard](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span></span>

10. <span data-ttu-id="92a6b-214">Assistente de saudação toocomplete, clique em **próximo** duas vezes.</span><span class="sxs-lookup"><span data-stu-id="92a6b-214">toocomplete hello wizard, click **Next** twice.</span></span>

> [!NOTE]
> <span data-ttu-id="92a6b-215">script Hello dá suporte a ambas as novas instalações de agentes do serviço de mobilidade e atualiza tooagents que já estão instalados.</span><span class="sxs-lookup"><span data-stu-id="92a6b-215">hello script supports both new installations of Mobility Service agents and updates tooagents that are already installed.</span></span>

### <a name="step-3-deploy-hello-package"></a><span data-ttu-id="92a6b-216">Etapa 3: Implantar o pacote de saudação</span><span class="sxs-lookup"><span data-stu-id="92a6b-216">Step 3: Deploy hello package</span></span>
1. <span data-ttu-id="92a6b-217">No console do Configuration Manager hello, seu pacote e selecione **distribuir conteúdo**.</span><span class="sxs-lookup"><span data-stu-id="92a6b-217">In hello Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="92a6b-218">![Captura de tela do console do Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="92a6b-218">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="92a6b-219">Selecione Olá  **[pontos de distribuição](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)**  em toowhich pacotes Olá devem ser copiados.</span><span class="sxs-lookup"><span data-stu-id="92a6b-219">Select hello **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on toowhich hello packages should be copied.</span></span>
3. <span data-ttu-id="92a6b-220">Assistente de saudação concluída.</span><span class="sxs-lookup"><span data-stu-id="92a6b-220">Complete hello wizard.</span></span> <span data-ttu-id="92a6b-221">pacote Hello, em seguida, inicia a replicação toohello especificado pontos de distribuição.</span><span class="sxs-lookup"><span data-stu-id="92a6b-221">hello package then starts replicating toohello specified distribution points.</span></span>
4. <span data-ttu-id="92a6b-222">Após ter feita a distribuição do pacote hello, pacote hello e selecione **implantar**.</span><span class="sxs-lookup"><span data-stu-id="92a6b-222">After hello package distribution is done, right-click hello package, and select **Deploy**.</span></span>
  <span data-ttu-id="92a6b-223">![Captura de tela do console do Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="92a6b-223">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="92a6b-224">Selecione Olá criado na seção pré-requisitos de saudação como coleção de destino Olá para implantação de coleção de dispositivos de servidor Linux.</span><span class="sxs-lookup"><span data-stu-id="92a6b-224">Select hello Linux Server device collection you created in hello prerequisites section as hello target collection for deployment.</span></span>

  ![Captura de tela do Assistente de Implantação de Software](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection-linux.png)

6. <span data-ttu-id="92a6b-226">Em Olá **especificar destino de conteúdo Olá** página, selecione seu **pontos de distribuição**.</span><span class="sxs-lookup"><span data-stu-id="92a6b-226">On hello **Specify hello content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="92a6b-227">Em Olá **toocontrol de configurações de especificar como este software é implantado** página, certifique-se de que o objetivo de saudação é **necessária**.</span><span class="sxs-lookup"><span data-stu-id="92a6b-227">On hello **Specify settings toocontrol how this software is deployed** page, ensure that hello purpose is **Required**.</span></span>

  ![Captura de tela do Assistente de Implantação de Software](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="92a6b-229">Em Olá **especificar agendamento de saudação para essa implantação** página, especifique uma agenda.</span><span class="sxs-lookup"><span data-stu-id="92a6b-229">On hello **Specify hello schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="92a6b-230">Para obter mais informações, consulte [Agendando pacotes](https://technet.microsoft.com/library/gg682178.aspx).</span><span class="sxs-lookup"><span data-stu-id="92a6b-230">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="92a6b-231">Em Olá **pontos de distribuição** página, configurar propriedades de saudação de acordo com as necessidades de toohello do seu datacenter.</span><span class="sxs-lookup"><span data-stu-id="92a6b-231">On hello **Distribution Points** page, configure hello properties according toohello needs of your datacenter.</span></span> <span data-ttu-id="92a6b-232">Conclua o Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="92a6b-232">Then complete hello wizard.</span></span>

<span data-ttu-id="92a6b-233">Serviço de mobilidade é instalado em Olá coleção de dispositivos de servidor Linux, de acordo com o agendamento de toohello que você configurou.</span><span class="sxs-lookup"><span data-stu-id="92a6b-233">Mobility Service gets installed on hello Linux Server Device Collection, according toohello schedule you configured.</span></span>

## <a name="other-methods-tooinstall-mobility-service"></a><span data-ttu-id="92a6b-234">Outros métodos tooinstall serviço de mobilidade</span><span class="sxs-lookup"><span data-stu-id="92a6b-234">Other methods tooinstall Mobility Service</span></span>
<span data-ttu-id="92a6b-235">Estas são algumas outras opções para instalação do Serviço de Mobilidade:</span><span class="sxs-lookup"><span data-stu-id="92a6b-235">Here are some other options for installing Mobility Service:</span></span>
* [<span data-ttu-id="92a6b-236">Instalação manual usando GUI</span><span class="sxs-lookup"><span data-stu-id="92a6b-236">Manual Installation using GUI</span></span>](http://aka.ms/mobsvcmanualinstall)
* [<span data-ttu-id="92a6b-237">Instalação manual usando linha de comando</span><span class="sxs-lookup"><span data-stu-id="92a6b-237">Manual Installation using command-line</span></span>](http://aka.ms/mobsvcmanualinstallcli)
* [<span data-ttu-id="92a6b-238">Instalação por push usando o servidor de configuração </span><span class="sxs-lookup"><span data-stu-id="92a6b-238">Push Installation using configuration server </span></span>](http://aka.ms/pushinstall)
* [<span data-ttu-id="92a6b-239">Instalação automatizada usando a Automação do Azure e a Configuração de Estado Desejado </span><span class="sxs-lookup"><span data-stu-id="92a6b-239">Automated Installation using Azure Automation & Desired State Configuration </span></span>](http://aka.ms/mobsvcdscinstall)

## <a name="uninstall-mobility-service"></a><span data-ttu-id="92a6b-240">Desinstalar o Serviço de Mobilidade</span><span class="sxs-lookup"><span data-stu-id="92a6b-240">Uninstall Mobility Service</span></span>
<span data-ttu-id="92a6b-241">Você pode criar o Configuration Manager pacotes toouninstall serviço de mobilidade.</span><span class="sxs-lookup"><span data-stu-id="92a6b-241">You can create Configuration Manager packages toouninstall Mobility Service.</span></span> <span data-ttu-id="92a6b-242">Use Olá toodo de script a seguir para:</span><span class="sxs-lookup"><span data-stu-id="92a6b-242">Use hello following script toodo so:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="92a6b-243">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="92a6b-243">Next steps</span></span>
<span data-ttu-id="92a6b-244">Agora você está pronto muito[Habilitar proteção](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) para as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="92a6b-244">You are now ready too[enable protection](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) for your virtual machines.</span></span>
