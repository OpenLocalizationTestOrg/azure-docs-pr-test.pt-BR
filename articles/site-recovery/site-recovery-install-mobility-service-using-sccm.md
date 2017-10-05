---
title: "Automatizar a instalação do Serviço de Mobilidade para o Azure Site Recovery usando ferramentas de implantação de software | Microsoft Docs"
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
ms.openlocfilehash: 49b72cd306aa91f114af7688f02d95db6f6eca05
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="automate-mobility-service-installation-by-using-software-deployment-tools"></a><span data-ttu-id="347e6-103">Automatizar a instalação do Serviço de Mobilidade usando ferramentas de implantação de software</span><span class="sxs-lookup"><span data-stu-id="347e6-103">Automate Mobility Service installation by using software deployment tools</span></span>

>[!IMPORTANT]
<span data-ttu-id="347e6-104">Este documento presume que você esteja usando a versão **9.9.4510.1** ou superior.</span><span class="sxs-lookup"><span data-stu-id="347e6-104">This document assumes you are using version **9.9.4510.1** or higher.</span></span>

<span data-ttu-id="347e6-105">Este artigo fornece um exemplo de como você pode usar o System Center Configuration Manager para implantar o Serviço de Mobilidade do Azure Site Recovery em seu datacenter.</span><span class="sxs-lookup"><span data-stu-id="347e6-105">This article provides you an example of how you can use System Center Configuration Manager to deploy the Azure Site Recovery Mobility Service in your datacenter.</span></span> <span data-ttu-id="347e6-106">O uso de uma ferramenta de implantação de software como o Configuration Manager traz as seguintes vantagens:</span><span class="sxs-lookup"><span data-stu-id="347e6-106">Using a software deployment tool like Configuration Manager has the following advantages:</span></span>
* <span data-ttu-id="347e6-107">Agendamento de implantação de novas instalações e atualizações, durante a janela de manutenção planejada para atualizações de software</span><span class="sxs-lookup"><span data-stu-id="347e6-107">Scheduling deployment of fresh installations and upgrades, during your planned maintenance window for software updates</span></span>
* <span data-ttu-id="347e6-108">Dimensionamento de implantação para centenas de servidores simultaneamente</span><span class="sxs-lookup"><span data-stu-id="347e6-108">Scaling deployment to hundreds of servers simultaneously</span></span>


> [!NOTE]
> <span data-ttu-id="347e6-109">Este artigo usa o System Center Configuration Manager 2012 R2 para demonstrar a atividade de implantação.</span><span class="sxs-lookup"><span data-stu-id="347e6-109">This article uses System Center Configuration Manager 2012 R2 to demonstrate the deployment activity.</span></span> <span data-ttu-id="347e6-110">Você também poderá automatizar a instalação do Serviço de Mobilidade usando a [Automação do Azure e a Configuração de Estado Desejado](site-recovery-automate-mobility-service-install.md).</span><span class="sxs-lookup"><span data-stu-id="347e6-110">You could also automate Mobility Service installation by using [Azure Automation and Desired State Configuration](site-recovery-automate-mobility-service-install.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="347e6-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="347e6-111">Prerequisites</span></span>
1. <span data-ttu-id="347e6-112">Uma ferramenta de implantação de software, como o Configuration Manager, já está implantada no ambiente.</span><span class="sxs-lookup"><span data-stu-id="347e6-112">A software deployment tool, like Configuration Manager, that is already deployed in your environment.</span></span>
  <span data-ttu-id="347e6-113">Crie duas [coleções de dispositivos](https://technet.microsoft.com/library/gg682169.aspx), uma para todos os **servidores Windows** e outra para todos os **servidores Linux** que você deseja proteger com o Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="347e6-113">Create two [device collections](https://technet.microsoft.com/library/gg682169.aspx), one for all **Windows servers**, and another for all **Linux servers**, that you want to protect by using Site Recovery.</span></span>
3. <span data-ttu-id="347e6-114">Um servidor de configuração que já está registrado no Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="347e6-114">A configuration server that is already registered with Site Recovery.</span></span>
4. <span data-ttu-id="347e6-115">Um compartilhamento de arquivos de rede segura (compartilhamento do protocolo SMB) que pode ser acessado pelo servidor do Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="347e6-115">A secure network file share (Server Message Block share) that can be accessed by the Configuration Manager server.</span></span>

## <a name="deploy-mobility-service-on-computers-running-windows"></a><span data-ttu-id="347e6-116">Implantar o Serviço de Mobilidade em computadores que executam o Windows</span><span class="sxs-lookup"><span data-stu-id="347e6-116">Deploy Mobility Service on computers running Windows</span></span>
> [!NOTE]
> <span data-ttu-id="347e6-117">Este artigo pressupõe que o endereço IP do servidor de configuração é 192.168.3.121 e que o compartilhamento de arquivos de rede segura é \\\ContosoSecureFS\MobilityServiceInstallers.</span><span class="sxs-lookup"><span data-stu-id="347e6-117">This article assumes that the IP address of the configuration server is 192.168.3.121, and that the secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="347e6-118">Etapa 1: Preparar para a implantação</span><span class="sxs-lookup"><span data-stu-id="347e6-118">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="347e6-119">Crie uma pasta no compartilhamento de rede e nomeie-a **MobSvcWindows**.</span><span class="sxs-lookup"><span data-stu-id="347e6-119">Create a folder on the network share, and name it **MobSvcWindows**.</span></span>
2. <span data-ttu-id="347e6-120">Entre no servidor de configuração e abra um prompt de comando administrativo.</span><span class="sxs-lookup"><span data-stu-id="347e6-120">Sign in to your configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="347e6-121">Execute os seguintes comandos para gerar um arquivo de frase secreta:</span><span class="sxs-lookup"><span data-stu-id="347e6-121">Run the following commands to generate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="347e6-122">Copie o arquivo **MobSvc.passphrase** para a pasta **MobSvcWindows** no compartilhamento de rede.</span><span class="sxs-lookup"><span data-stu-id="347e6-122">Copy the **MobSvc.passphrase** file into the **MobSvcWindows** folder on your network share.</span></span>
5. <span data-ttu-id="347e6-123">Procure o repositório do instalador no servidor de configuração executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="347e6-123">Browse to the installer repository on the configuration server by running the following command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="347e6-124">Copie o **Microsoft-ASR\_UA\_*version*\_Windows\_GA\_*date*\_Release.exe** para a pasta **MobSvcWindows** no compartilhamento de rede.</span><span class="sxs-lookup"><span data-stu-id="347e6-124">Copy the **Microsoft-ASR\_UA\_*version*\_Windows\_GA\_*date*\_Release.exe** to the **MobSvcWindows** folder on your network share.</span></span>
7. <span data-ttu-id="347e6-125">Copie o código a seguir e salve-o como **install.bat** na pasta **MobSvcWindows**.</span><span class="sxs-lookup"><span data-stu-id="347e6-125">Copy the following code, and save it as **install.bat** into the **MobSvcWindows** folder.</span></span>

   > [!NOTE]
   > <span data-ttu-id="347e6-126">Substitua os espaços reservados de [CSIP] neste script pelos valores reais do endereço IP do servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="347e6-126">Replace the [CSIP] placeholders in this script with the actual values of the IP address of your configuration server.</span></span>

```DOS
Time /t >> C:\Temp\logfile.log
REM ==================================================
REM ==== Clean up the folders ========================
RMDIR /S /q %temp%\MobSvc
MKDIR %Temp%\MobSvc
MKDIR C:\Temp
REM ==================================================

REM ==== Copy new files ==============================
COPY M*.* %Temp%\MobSvc
CD %Temp%\MobSvc
REN Micro*.exe MobSvcInstaller.exe
REM ==================================================

REM ==== Extract the installer =======================
MobSvcInstaller.exe /q /x:%Temp%\MobSvc\Extracted
REM ==== Wait 10s for extraction to complete =========
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

### <a name="step-2-create-a-package"></a><span data-ttu-id="347e6-127">Etapa 2: Criar um pacote</span><span class="sxs-lookup"><span data-stu-id="347e6-127">Step 2: Create a package</span></span>

1. <span data-ttu-id="347e6-128">Conecte-se ao console do Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="347e6-128">Sign in to your Configuration Manager console.</span></span>
2. <span data-ttu-id="347e6-129">Navegue para **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="347e6-129">Browse to **Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="347e6-130">Clique com o botão direito do mouse em **Pacotes** e selecione **Criar Pacote**.</span><span class="sxs-lookup"><span data-stu-id="347e6-130">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="347e6-131">Forneça valores para nome, descrição, fabricante, idioma e versão.</span><span class="sxs-lookup"><span data-stu-id="347e6-131">Provide values for the name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="347e6-132">Marque a caixa de seleção **Este pacote contém os arquivos de origem**.</span><span class="sxs-lookup"><span data-stu-id="347e6-132">Select the **This package contains source files** check box.</span></span>
6. <span data-ttu-id="347e6-133">Clique em **Procurar** e selecione o compartilhamento de rede em que o instalador está armazenado (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).</span><span class="sxs-lookup"><span data-stu-id="347e6-133">Click **Browse**, and select the network share where the installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcWindows).</span></span>

  ![Captura de tela do Assistente para Criar Pacote e Programa](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package.png)

7. <span data-ttu-id="347e6-135">Na página **Escolha o tipo de programa que você deseja criar**, selecione **Programa Padrão** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="347e6-135">On the **Choose the program type that you want to create** page, select **Standard Program**, and click **Next**.</span></span>

  ![Captura de tela do Assistente para Criar Pacote e Programa](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="347e6-137">Na página **Especificar informações sobre este programa padrão**, forneça as entradas a seguir e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="347e6-137">On the **Specify information about this standard program** page, provide the following inputs, and click **Next**.</span></span> <span data-ttu-id="347e6-138">(As outras entradas podem usar seus valores padrão.)</span><span class="sxs-lookup"><span data-stu-id="347e6-138">(The other inputs can use their default values.)</span></span>

  | <span data-ttu-id="347e6-139">**Nome do parâmetro**</span><span class="sxs-lookup"><span data-stu-id="347e6-139">**Parameter name**</span></span> | <span data-ttu-id="347e6-140">**Valor**</span><span class="sxs-lookup"><span data-stu-id="347e6-140">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="347e6-141">Nome</span><span class="sxs-lookup"><span data-stu-id="347e6-141">Name</span></span> | <span data-ttu-id="347e6-142">Instalar o Serviço de Mobilidade do Microsoft Azure (Windows)</span><span class="sxs-lookup"><span data-stu-id="347e6-142">Install Microsoft Azure Mobility Service (Windows)</span></span> |
  | <span data-ttu-id="347e6-143">Linha de comando</span><span class="sxs-lookup"><span data-stu-id="347e6-143">Command line</span></span> | <span data-ttu-id="347e6-144">install.bat</span><span class="sxs-lookup"><span data-stu-id="347e6-144">install.bat</span></span> |
  | <span data-ttu-id="347e6-145">Programa pode ser executado</span><span class="sxs-lookup"><span data-stu-id="347e6-145">Program can run</span></span> | <span data-ttu-id="347e6-146">Se um usuário fez logon ou não</span><span class="sxs-lookup"><span data-stu-id="347e6-146">Whether or not a user is logged on</span></span> |

  ![Captura de tela do Assistente para Criar Pacote e Programa](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties.png)

9. <span data-ttu-id="347e6-148">Na próxima página, selecione os sistemas operacionais de destino.</span><span class="sxs-lookup"><span data-stu-id="347e6-148">On the next page, select the target operating systems.</span></span> <span data-ttu-id="347e6-149">O Serviço de Mobilidade pode ser instalado somente no Windows Server 2012 R2, Windows Server 2012 e Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="347e6-149">Mobility Service can be installed only on Windows Server 2012 R2, Windows Server 2012, and Windows Server 2008 R2.</span></span>

  ![Captura de tela do Assistente para Criar Pacote e Programa](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2.png)

10. <span data-ttu-id="347e6-151">Para concluir o assistente, clique em **Avançar** duas vezes.</span><span class="sxs-lookup"><span data-stu-id="347e6-151">To complete the wizard, click **Next** twice.</span></span>


> [!NOTE]
> <span data-ttu-id="347e6-152">O script dá suporte tanto a instalações novas dos agentes do Serviço de Mobilidade quanto a atualizações de agentes já instalados.</span><span class="sxs-lookup"><span data-stu-id="347e6-152">The script supports both new installations of Mobility Service agents and updates to agents that are already installed.</span></span>

### <a name="step-3-deploy-the-package"></a><span data-ttu-id="347e6-153">Etapa 3: Implantar o pacote</span><span class="sxs-lookup"><span data-stu-id="347e6-153">Step 3: Deploy the package</span></span>
1. <span data-ttu-id="347e6-154">No console do Configuration Manager, clique com o botão direito do mouse no pacote e selecione **Distribuir Conteúdo**.</span><span class="sxs-lookup"><span data-stu-id="347e6-154">In the Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="347e6-155">![Captura de tela do console do Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="347e6-155">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="347e6-156">Selecione os **[pontos de distribuição](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** para os quais os pacotes devem ser copiados.</span><span class="sxs-lookup"><span data-stu-id="347e6-156">Select the **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on to which the packages should be copied.</span></span>
3. <span data-ttu-id="347e6-157">Conclua o assistente.</span><span class="sxs-lookup"><span data-stu-id="347e6-157">Complete the wizard.</span></span> <span data-ttu-id="347e6-158">Em seguida, o pacote começa a ser replicado para os pontos de distribuição especificados.</span><span class="sxs-lookup"><span data-stu-id="347e6-158">The package then starts replicating to the specified distribution points.</span></span>
4. <span data-ttu-id="347e6-159">Após a conclusão da distribuição do pacote, clique com o botão direito do mouse no pacote e selecione **Implantar**.</span><span class="sxs-lookup"><span data-stu-id="347e6-159">After the package distribution is done, right-click the package, and select **Deploy**.</span></span>
  <span data-ttu-id="347e6-160">![Captura de tela do console do Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="347e6-160">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="347e6-161">Selecione a coleção de dispositivos do Windows Server criada na seção de pré-requisitos como a coleção de destino para a implantação.</span><span class="sxs-lookup"><span data-stu-id="347e6-161">Select the Windows Server device collection you created in the prerequisites section as the target collection for deployment.</span></span>

  ![Captura de tela do Assistente de Implantação de Software](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection.png)

6. <span data-ttu-id="347e6-163">Na página **Especificar o destino de conteúdo**, selecione os **Pontos de Distribuição**.</span><span class="sxs-lookup"><span data-stu-id="347e6-163">On the **Specify the content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="347e6-164">Na página **Especificar as configurações para controlar como este software é implantado**, verifique se a finalidade é **Obrigatória**.</span><span class="sxs-lookup"><span data-stu-id="347e6-164">On the **Specify settings to control how this software is deployed** page, ensure that the purpose is **Required**.</span></span>

  ![Captura de tela do Assistente de Implantação de Software](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="347e6-166">Na página **Especificar o agendamento para esta implantação**, especifique um agendamento.</span><span class="sxs-lookup"><span data-stu-id="347e6-166">On the **Specify the schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="347e6-167">Para obter mais informações, consulte [Agendando pacotes](https://technet.microsoft.com/library/gg682178.aspx).</span><span class="sxs-lookup"><span data-stu-id="347e6-167">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="347e6-168">Na página **Pontos de Distribuição**, configure as propriedades de acordo com as necessidades de seu datacenter.</span><span class="sxs-lookup"><span data-stu-id="347e6-168">On the **Distribution Points** page, configure the properties according to the needs of your datacenter.</span></span> <span data-ttu-id="347e6-169">Em seguida, conclua o assistente.</span><span class="sxs-lookup"><span data-stu-id="347e6-169">Then complete the wizard.</span></span>

> [!TIP]
> <span data-ttu-id="347e6-170">Para evitar reinicializações desnecessárias, agende a instalação do pacote durante a janela de manutenção mensal ou a janela de atualizações de software.</span><span class="sxs-lookup"><span data-stu-id="347e6-170">To avoid unnecessary reboots, schedule the package installation during your monthly maintenance window or software updates window.</span></span>

<span data-ttu-id="347e6-171">É possível monitorar o andamento da implantação usando o console do Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="347e6-171">You can monitor the deployment progress by using the Configuration Manager console.</span></span> <span data-ttu-id="347e6-172">Acesse **Monitoramento** > **Implantações** > *[nome do pacote]*.</span><span class="sxs-lookup"><span data-stu-id="347e6-172">Go to **Monitoring** > **Deployments** > *[your package name]*.</span></span>

  ![Captura de tela da opção Configuration Manager para monitorar as implantações](./media/site-recovery-install-mobility-service-using-sccm/report.PNG)

## <a name="deploy-mobility-service-on-computers-running-linux"></a><span data-ttu-id="347e6-174">Implantar o Serviço de Mobilidade em computadores que executam o Linux</span><span class="sxs-lookup"><span data-stu-id="347e6-174">Deploy Mobility Service on computers running Linux</span></span>
> [!NOTE]
> <span data-ttu-id="347e6-175">Este artigo pressupõe que o endereço IP do servidor de configuração é 192.168.3.121 e que o compartilhamento de arquivos de rede segura é \\\ContosoSecureFS\MobilityServiceInstallers.</span><span class="sxs-lookup"><span data-stu-id="347e6-175">This article assumes that the IP address of the configuration server is 192.168.3.121, and that the secure network file share is \\\ContosoSecureFS\MobilityServiceInstallers.</span></span>

### <a name="step-1-prepare-for-deployment"></a><span data-ttu-id="347e6-176">Etapa 1: Preparar para a implantação</span><span class="sxs-lookup"><span data-stu-id="347e6-176">Step 1: Prepare for deployment</span></span>
1. <span data-ttu-id="347e6-177">Crie uma pasta no compartilhamento de rede e nomeie-a **MobSvcLinux**.</span><span class="sxs-lookup"><span data-stu-id="347e6-177">Create a folder on the network share, and name it as **MobSvcLinux**.</span></span>
2. <span data-ttu-id="347e6-178">Entre no servidor de configuração e abra um prompt de comando administrativo.</span><span class="sxs-lookup"><span data-stu-id="347e6-178">Sign in to your configuration server, and open an administrative command prompt.</span></span>
3. <span data-ttu-id="347e6-179">Execute os seguintes comandos para gerar um arquivo de frase secreta:</span><span class="sxs-lookup"><span data-stu-id="347e6-179">Run the following commands to generate a passphrase file:</span></span>

    `cd %ProgramData%\ASR\home\svsystems\bin`

    `genpassphrase.exe -v > MobSvc.passphrase`
4. <span data-ttu-id="347e6-180">Copie o arquivo **MobSvc.passphrase** para a pasta **MobSvcLinux** no compartilhamento de rede.</span><span class="sxs-lookup"><span data-stu-id="347e6-180">Copy the **MobSvc.passphrase** file into the **MobSvcLinux** folder on your network share.</span></span>
5. <span data-ttu-id="347e6-181">Procure o repositório do instalador no servidor de configuração executando o comando:</span><span class="sxs-lookup"><span data-stu-id="347e6-181">Browse to the installer repository on the configuration server by running the command:</span></span>

   `cd %ProgramData%\ASR\home\svsystems\puhsinstallsvc\repository`

6. <span data-ttu-id="347e6-182">Copie os seguintes arquivos para a pasta **MobSvcLinux** no compartilhamento de rede:</span><span class="sxs-lookup"><span data-stu-id="347e6-182">Copy the following files to the **MobSvcLinux** folder on your network share:</span></span>
   * <span data-ttu-id="347e6-183">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="347e6-183">Microsoft-ASR\_UA\*RHEL6-64*release.tar.gz</span></span>
   * <span data-ttu-id="347e6-184">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="347e6-184">Microsoft-ASR\_UA\*RHEL7-64\*release.tar.gz</span></span>
   * <span data-ttu-id="347e6-185">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="347e6-185">Microsoft-ASR\_UA\*SLES11-SP3-64\*release.tar.gz</span></span>
   * <span data-ttu-id="347e6-186">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="347e6-186">Microsoft-ASR\_UA\*SLES11-SP4-64\*release.tar.gz</span></span>
   * <span data-ttu-id="347e6-187">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="347e6-187">Microsoft-ASR\_UA\*OL6-64\*release.tar.gz</span></span>
   * <span data-ttu-id="347e6-188">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span><span class="sxs-lookup"><span data-stu-id="347e6-188">Microsoft-ASR\_UA\*UBUNTU-14.04-64\*release.tar.gz</span></span>


7. <span data-ttu-id="347e6-189">Copie o código a seguir e salve-o como **install_linux.sh** na pasta **MobSvcLinux**.</span><span class="sxs-lookup"><span data-stu-id="347e6-189">Copy the following code, and save it as **install_linux.sh** into the **MobSvcLinux** folder.</span></span>
   > [!NOTE]
   > <span data-ttu-id="347e6-190">Substitua os espaços reservados de [CSIP] neste script pelos valores reais do endereço IP do servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="347e6-190">Replace the [CSIP] placeholders in this script with the actual values of the IP address of your configuration server.</span></span>

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
        echo "Installation has succeeded. Proceed to configuration." >> /tmp/MobSvc/sccm.log
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
        echo "Agent is already configured. Proceed to Upgrade." >> /tmp/MobSvc/sccm.log
        Upgrade
    else
        echo "Agent is not configured. Proceed to Configure." >> /tmp/MobSvc/sccm.log
        Configure
    fi
else
    Install
fi

cd /tmp

```

### <a name="step-2-create-a-package"></a><span data-ttu-id="347e6-191">Etapa 2: Criar um pacote</span><span class="sxs-lookup"><span data-stu-id="347e6-191">Step 2: Create a package</span></span>

1. <span data-ttu-id="347e6-192">Conecte-se ao console do Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="347e6-192">Sign in  to your Configuration Manager console.</span></span>
2. <span data-ttu-id="347e6-193">Navegue para **Biblioteca de Software** > **Gerenciamento de Aplicativos** > **Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="347e6-193">Browse to **Software Library** > **Application Management** > **Packages**.</span></span>
3. <span data-ttu-id="347e6-194">Clique com o botão direito do mouse em **Pacotes** e selecione **Criar Pacote**.</span><span class="sxs-lookup"><span data-stu-id="347e6-194">Right-click **Packages**, and select **Create Package**.</span></span>
4. <span data-ttu-id="347e6-195">Forneça valores para nome, descrição, fabricante, idioma e versão.</span><span class="sxs-lookup"><span data-stu-id="347e6-195">Provide values for the name, description, manufacturer, language, and version.</span></span>
5. <span data-ttu-id="347e6-196">Marque a caixa de seleção **Este pacote contém os arquivos de origem**.</span><span class="sxs-lookup"><span data-stu-id="347e6-196">Select the **This package contains source files** check box.</span></span>
6. <span data-ttu-id="347e6-197">Clique em **Procurar** e selecione o compartilhamento de rede em que o instalador está armazenado (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).</span><span class="sxs-lookup"><span data-stu-id="347e6-197">Click **Browse**, and select the network share where the installer is stored (\\\ContosoSecureFS\MobilityServiceInstaller\MobSvcLinux).</span></span>

  ![Captura de tela do Assistente para Criar Pacote e Programa](./media/site-recovery-install-mobility-service-using-sccm/create_sccm_package-linux.png)

7. <span data-ttu-id="347e6-199">Na página **Escolha o tipo de programa que você deseja criar**, selecione **Programa Padrão** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="347e6-199">On the **Choose the program type that you want to create** page, select **Standard Program**, and click **Next**.</span></span>

  ![Captura de tela do Assistente para Criar Pacote e Programa](./media/site-recovery-install-mobility-service-using-sccm/sccm-standard-program.png)

8. <span data-ttu-id="347e6-201">Na página **Especificar informações sobre este programa padrão**, forneça as entradas a seguir e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="347e6-201">On the **Specify information about this standard program** page, provide the following inputs, and click **Next**.</span></span> <span data-ttu-id="347e6-202">(As outras entradas podem usar seus valores padrão.)</span><span class="sxs-lookup"><span data-stu-id="347e6-202">(The other inputs can use their default values.)</span></span>

    | <span data-ttu-id="347e6-203">**Nome do parâmetro**</span><span class="sxs-lookup"><span data-stu-id="347e6-203">**Parameter name**</span></span> | <span data-ttu-id="347e6-204">**Valor**</span><span class="sxs-lookup"><span data-stu-id="347e6-204">**Value**</span></span> |
  |--|--|
  | <span data-ttu-id="347e6-205">Nome</span><span class="sxs-lookup"><span data-stu-id="347e6-205">Name</span></span> | <span data-ttu-id="347e6-206">Instalar o Serviço de Mobilidade do Microsoft Azure (Linux)</span><span class="sxs-lookup"><span data-stu-id="347e6-206">Install Microsoft Azure Mobility Service (Linux)</span></span> |
  | <span data-ttu-id="347e6-207">Linha de comando</span><span class="sxs-lookup"><span data-stu-id="347e6-207">Command line</span></span> | <span data-ttu-id="347e6-208">./install_linux.sh</span><span class="sxs-lookup"><span data-stu-id="347e6-208">./install_linux.sh</span></span> |
  | <span data-ttu-id="347e6-209">Programa pode ser executado</span><span class="sxs-lookup"><span data-stu-id="347e6-209">Program can run</span></span> | <span data-ttu-id="347e6-210">Se um usuário fez logon ou não</span><span class="sxs-lookup"><span data-stu-id="347e6-210">Whether or not a user is logged on</span></span> |

  ![Captura de tela do Assistente para Criar Pacote e Programa](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-linux.png)

9. <span data-ttu-id="347e6-212">Na próxima página, selecione **Este programa pode ser executado em qualquer plataforma**.</span><span class="sxs-lookup"><span data-stu-id="347e6-212">On the next page, select **This program can run on any platform**.</span></span>
  <span data-ttu-id="347e6-213">![Captura de tela do Assistente para Criar Pacote e Programa](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span><span class="sxs-lookup"><span data-stu-id="347e6-213">![Screenshot of Create Package and Program wizard](./media/site-recovery-install-mobility-service-using-sccm/sccm-program-properties-page2-linux.png)</span></span>

10. <span data-ttu-id="347e6-214">Para concluir o assistente, clique em **Avançar** duas vezes.</span><span class="sxs-lookup"><span data-stu-id="347e6-214">To complete the wizard, click **Next** twice.</span></span>

> [!NOTE]
> <span data-ttu-id="347e6-215">O script dá suporte tanto a instalações novas dos agentes do Serviço de Mobilidade quanto a atualizações de agentes já instalados.</span><span class="sxs-lookup"><span data-stu-id="347e6-215">The script supports both new installations of Mobility Service agents and updates to agents that are already installed.</span></span>

### <a name="step-3-deploy-the-package"></a><span data-ttu-id="347e6-216">Etapa 3: Implantar o pacote</span><span class="sxs-lookup"><span data-stu-id="347e6-216">Step 3: Deploy the package</span></span>
1. <span data-ttu-id="347e6-217">No console do Configuration Manager, clique com o botão direito do mouse no pacote e selecione **Distribuir Conteúdo**.</span><span class="sxs-lookup"><span data-stu-id="347e6-217">In the Configuration Manager console, right-click your package, and select **Distribute Content**.</span></span>
  <span data-ttu-id="347e6-218">![Captura de tela do console do Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span><span class="sxs-lookup"><span data-stu-id="347e6-218">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_distribute.png)</span></span>
2. <span data-ttu-id="347e6-219">Selecione os **[pontos de distribuição](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** para os quais os pacotes devem ser copiados.</span><span class="sxs-lookup"><span data-stu-id="347e6-219">Select the **[distribution points](https://technet.microsoft.com/library/gg712321.aspx#BKMK_PlanForDistributionPoints)** on to which the packages should be copied.</span></span>
3. <span data-ttu-id="347e6-220">Conclua o assistente.</span><span class="sxs-lookup"><span data-stu-id="347e6-220">Complete the wizard.</span></span> <span data-ttu-id="347e6-221">Em seguida, o pacote começa a ser replicado para os pontos de distribuição especificados.</span><span class="sxs-lookup"><span data-stu-id="347e6-221">The package then starts replicating to the specified distribution points.</span></span>
4. <span data-ttu-id="347e6-222">Após a conclusão da distribuição do pacote, clique com o botão direito do mouse no pacote e selecione **Implantar**.</span><span class="sxs-lookup"><span data-stu-id="347e6-222">After the package distribution is done, right-click the package, and select **Deploy**.</span></span>
  <span data-ttu-id="347e6-223">![Captura de tela do console do Configuration Manager](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span><span class="sxs-lookup"><span data-stu-id="347e6-223">![Screenshot of Configuration Manager console](./media/site-recovery-install-mobility-service-using-sccm/sccm_deploy.png)</span></span>
5. <span data-ttu-id="347e6-224">Selecione a coleção de dispositivos do Linux Server criada na seção de pré-requisitos como a coleção de destino para implantação.</span><span class="sxs-lookup"><span data-stu-id="347e6-224">Select the Linux Server device collection you created in the prerequisites section as the target collection for deployment.</span></span>

  ![Captura de tela do Assistente de Implantação de Software](./media/site-recovery-install-mobility-service-using-sccm/sccm-select-target-collection-linux.png)

6. <span data-ttu-id="347e6-226">Na página **Especificar o destino de conteúdo**, selecione os **Pontos de Distribuição**.</span><span class="sxs-lookup"><span data-stu-id="347e6-226">On the **Specify the content destination** page, select your **Distribution Points**.</span></span>
7. <span data-ttu-id="347e6-227">Na página **Especificar as configurações para controlar como este software é implantado**, verifique se a finalidade é **Obrigatória**.</span><span class="sxs-lookup"><span data-stu-id="347e6-227">On the **Specify settings to control how this software is deployed** page, ensure that the purpose is **Required**.</span></span>

  ![Captura de tela do Assistente de Implantação de Software](./media/site-recovery-install-mobility-service-using-sccm/sccm-deploy-select-purpose.png)

8. <span data-ttu-id="347e6-229">Na página **Especificar o agendamento para esta implantação**, especifique um agendamento.</span><span class="sxs-lookup"><span data-stu-id="347e6-229">On the **Specify the schedule for this deployment** page, specify a schedule.</span></span> <span data-ttu-id="347e6-230">Para obter mais informações, consulte [Agendando pacotes](https://technet.microsoft.com/library/gg682178.aspx).</span><span class="sxs-lookup"><span data-stu-id="347e6-230">For more information, see [scheduling packages](https://technet.microsoft.com/library/gg682178.aspx).</span></span>
9. <span data-ttu-id="347e6-231">Na página **Pontos de Distribuição**, configure as propriedades de acordo com as necessidades de seu datacenter.</span><span class="sxs-lookup"><span data-stu-id="347e6-231">On the **Distribution Points** page, configure the properties according to the needs of your datacenter.</span></span> <span data-ttu-id="347e6-232">Em seguida, conclua o assistente.</span><span class="sxs-lookup"><span data-stu-id="347e6-232">Then complete the wizard.</span></span>

<span data-ttu-id="347e6-233">O Serviço de Mobilidade é instalado na Coleção de Dispositivos do Linux Server de acordo com o agendamento configurado.</span><span class="sxs-lookup"><span data-stu-id="347e6-233">Mobility Service gets installed on the Linux Server Device Collection, according to the schedule you configured.</span></span>

## <a name="other-methods-to-install-mobility-service"></a><span data-ttu-id="347e6-234">Outros métodos para instalação do Serviço de Mobilidade</span><span class="sxs-lookup"><span data-stu-id="347e6-234">Other methods to install Mobility Service</span></span>
<span data-ttu-id="347e6-235">Estas são algumas outras opções para instalação do Serviço de Mobilidade:</span><span class="sxs-lookup"><span data-stu-id="347e6-235">Here are some other options for installing Mobility Service:</span></span>
* [<span data-ttu-id="347e6-236">Instalação manual usando GUI</span><span class="sxs-lookup"><span data-stu-id="347e6-236">Manual Installation using GUI</span></span>](http://aka.ms/mobsvcmanualinstall)
* [<span data-ttu-id="347e6-237">Instalação manual usando linha de comando</span><span class="sxs-lookup"><span data-stu-id="347e6-237">Manual Installation using command-line</span></span>](http://aka.ms/mobsvcmanualinstallcli)
* [<span data-ttu-id="347e6-238">Instalação por push usando o servidor de configuração </span><span class="sxs-lookup"><span data-stu-id="347e6-238">Push Installation using configuration server </span></span>](http://aka.ms/pushinstall)
* [<span data-ttu-id="347e6-239">Instalação automatizada usando a Automação do Azure e a Configuração de Estado Desejado </span><span class="sxs-lookup"><span data-stu-id="347e6-239">Automated Installation using Azure Automation & Desired State Configuration </span></span>](http://aka.ms/mobsvcdscinstall)

## <a name="uninstall-mobility-service"></a><span data-ttu-id="347e6-240">Desinstalar o Serviço de Mobilidade</span><span class="sxs-lookup"><span data-stu-id="347e6-240">Uninstall Mobility Service</span></span>
<span data-ttu-id="347e6-241">Você pode criar pacotes do Configuration Manager para desinstalar o Serviço de Mobilidade.</span><span class="sxs-lookup"><span data-stu-id="347e6-241">You can create Configuration Manager packages to uninstall Mobility Service.</span></span> <span data-ttu-id="347e6-242">Use o seguinte script para fazer isso:</span><span class="sxs-lookup"><span data-stu-id="347e6-242">Use the following script to do so:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="347e6-243">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="347e6-243">Next steps</span></span>
<span data-ttu-id="347e6-244">Agora você está pronto para [habilitar a proteção](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) para as máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="347e6-244">You are now ready to [enable protection](https://docs.microsoft.com/en-us/azure/site-recovery/site-recovery-vmware-to-azure#step-6-replicate-applications) for your virtual machines.</span></span>
