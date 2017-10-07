---
title: " Gerenciar um Servidor de Configuração no Azure Site Recovery | Microsoft Docs"
description: "Este artigo descreve como tooset e gerenciar um servidor de configuração."
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
ms.openlocfilehash: 2852bcd25409121be46a1ebf135ebfcdce6e5de5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-configuration-server"></a><span data-ttu-id="e9be7-103">Gerenciar um Servidor de Configuração</span><span class="sxs-lookup"><span data-stu-id="e9be7-103">Manage a Configuration Server</span></span>

<span data-ttu-id="e9be7-104">Servidor de configuração atua como um coordenador entre serviços de recuperação de Site hello e sua infraestrutura local.</span><span class="sxs-lookup"><span data-stu-id="e9be7-104">Configuration Server acts as a coordinator between hello Site Recovery services and your on-premises infrastructure.</span></span> <span data-ttu-id="e9be7-105">Este artigo descreve como você pode configurar, configurar e gerenciar Olá servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="e9be7-105">This article describes how you can set up, configure, and manage hello Configuration Server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9be7-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e9be7-106">Prerequisites</span></span>
<span data-ttu-id="e9be7-107">Olá seguem mínimos de hardware hello, software e rede configuração necessária tooset um servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="e9be7-107">hello following are hello minimum hardware, software, and network configuration required tooset up a Configuration Server.</span></span>

> [!NOTE]
> <span data-ttu-id="e9be7-108">[Planejamento de capacidade](site-recovery-capacity-planner.md) é um tooensure etapa importante que você implante Olá servidor de configuração com uma configuração que conjuntos de seus requisitos de carga.</span><span class="sxs-lookup"><span data-stu-id="e9be7-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step tooensure that you deploy hello Configuration Server with a configuration that suites your load requirements.</span></span> <span data-ttu-id="e9be7-109">Leia mais sobre [requisitos para um servidor de configuração de dimensionamento](#sizing-requirements-for-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="e9be7-109">Read more about [Sizing requirements for a Configuration Server](#sizing-requirements-for-a-configuration-server).</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-configuration-server-software"></a><span data-ttu-id="e9be7-110">Baixar o software de servidor de configuração de saudação</span><span class="sxs-lookup"><span data-stu-id="e9be7-110">Downloading hello Configuration Server software</span></span>
1. <span data-ttu-id="e9be7-111">Faça logon no toohello tooyour Azure portal e procurar o Cofre de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="e9be7-111">Log on toohello Azure portal and browse tooyour Recovery Services Vault.</span></span>
2. <span data-ttu-id="e9be7-112">Procurar muito**infra-estrutura de recuperação de Site** > **servidores de configuração** (no VMware para o & máquinas físicas).</span><span class="sxs-lookup"><span data-stu-id="e9be7-112">Browse too**Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span></span>

  ![Página Adicionar Servidores](./media/site-recovery-vmware-to-azure-manage-configuration-server/AddServers.png)
3. <span data-ttu-id="e9be7-114">Clique em Olá **+ servidores** botão.</span><span class="sxs-lookup"><span data-stu-id="e9be7-114">Click hello **+Servers** button.</span></span>
4. <span data-ttu-id="e9be7-115">Em Olá **Adicionar servidor** , clique em chave de registro de Olá Olá Download botão toodownload.</span><span class="sxs-lookup"><span data-stu-id="e9be7-115">On hello **Add Server** page, click hello Download button toodownload hello Registration key.</span></span> <span data-ttu-id="e9be7-116">Você precisa essa chave durante a saudação tooregister de instalação de servidor de configuração com o serviço do Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="e9be7-116">You need this key during hello Configuration Server installation tooregister it with Azure Site Recovery service.</span></span>
5. <span data-ttu-id="e9be7-117">Clique em Olá **Download Olá instalação unificado do Microsoft Azure Site Recovery** versão mais recente do link toodownload Olá de saudação servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="e9be7-117">Click hello **Download hello Microsoft Azure Site Recovery Unified Setup** link toodownload hello latest version of hello Configuration Server.</span></span>

  ![Página Download](./media/site-recovery-vmware-to-azure-manage-configuration-server/downloadcs.png)

  > [!TIP]
  <span data-ttu-id="e9be7-119">Versão mais recente do hello servidor de configuração pode ser baixado diretamente do [página de download da Microsoft Download Center](http://aka.ms/unifiedsetup)</span><span class="sxs-lookup"><span data-stu-id="e9be7-119">Latest version of hello Configuration Server can be downloaded directly from [Microsoft Download Center download page](http://aka.ms/unifiedsetup)</span></span>

## <a name="installing-and-registering-a-configuration-server-from-gui"></a><span data-ttu-id="e9be7-120">Instalar e registrar um servidor de configuração da GUI</span><span class="sxs-lookup"><span data-stu-id="e9be7-120">Installing and Registering a Configuration Server from GUI</span></span>
[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

## <a name="installing-and-registering-a-configuration-server-using-command-line"></a><span data-ttu-id="e9be7-121">Instalar e registrar um servidor de configuração usando a linha de comando</span><span class="sxs-lookup"><span data-stu-id="e9be7-121">Installing and registering a Configuration Server using Command line</span></span>

  ```
  UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
  ```

### <a name="sample-usage"></a><span data-ttu-id="e9be7-122">Exemplo de uso</span><span class="sxs-lookup"><span data-stu-id="e9be7-122">Sample usage</span></span>
  ```
  MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
  cd C:\Temp\Extracted
  UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "CS" /InstallLocation "D:\" /MySQLCredsFilePath "C:\Temp\MySQLCredentialsfile.txt" /VaultCredsFilePath "C:\Temp\MyVault.vaultcredentials" /EnvType "VMWare"
  ```


### <a name="configuration-server-installer-command-line-arguments"></a><span data-ttu-id="e9be7-123">Argumentos de linha de comando do instalador do servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="e9be7-123">Configuration Server installer command-line arguments.</span></span>
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-mysql-credentials-file"></a><span data-ttu-id="e9be7-124">Criar um arquivo de credenciais do MySql</span><span class="sxs-lookup"><span data-stu-id="e9be7-124">Create a MySql credentials file</span></span>
<span data-ttu-id="e9be7-125">Parâmetro MySQLCredsFilePath utiliza um arquivo como entrada.</span><span class="sxs-lookup"><span data-stu-id="e9be7-125">MySQLCredsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="e9be7-126">Crie arquivo de saudação usando Olá seguinte formato e passá-lo como parâmetro de entrada MySQLCredsFilePath.</span><span class="sxs-lookup"><span data-stu-id="e9be7-126">Create hello file using hello following format and pass it as input MySQLCredsFilePath parameter.</span></span>
```
[MySQLCredentials]
MySQLRootPassword = "Password>"
MySQLUserPassword = "Password"
```
### <a name="create-a-proxy-settings-configuration-file"></a><span data-ttu-id="e9be7-127">Criar um arquivo de configuração de configurações de proxy</span><span class="sxs-lookup"><span data-stu-id="e9be7-127">Create a proxy settings configuration file</span></span>
<span data-ttu-id="e9be7-128">O parâmetro ProxySettingsFilePath utiliza um arquivo como entrada.</span><span class="sxs-lookup"><span data-stu-id="e9be7-128">ProxySettingsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="e9be7-129">Crie arquivo de saudação usando Olá seguinte formato e passá-lo como parâmetro de entrada ProxySettingsFilePath.</span><span class="sxs-lookup"><span data-stu-id="e9be7-129">Create hello file using hello following format and pass it as input ProxySettingsFilePath parameter.</span></span>

```
[ProxySettings]
ProxyAuthentication = "Yes/No"
Proxy IP = "IP Address"
ProxyPort = "Port"
ProxyUserName="UserName"
ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-configuration-server"></a><span data-ttu-id="e9be7-130">Modificando configurações de proxy de servidor de configuração</span><span class="sxs-lookup"><span data-stu-id="e9be7-130">Modifying proxy settings for Configuration Server</span></span>
1. <span data-ttu-id="e9be7-131">Logon tooyour servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="e9be7-131">Login tooyour Configuration Server.</span></span>
2. <span data-ttu-id="e9be7-132">Iniciar cspsconfigtool.exe hello usando o atalho de saudação em seu.</span><span class="sxs-lookup"><span data-stu-id="e9be7-132">Launch hello cspsconfigtool.exe using hello shortcut on your.</span></span>
3. <span data-ttu-id="e9be7-133">Clique em Olá **registro do cofre** guia.</span><span class="sxs-lookup"><span data-stu-id="e9be7-133">Click hello **Vault Registration** tab.</span></span>
4. <span data-ttu-id="e9be7-134">Download de um novo arquivo de registro do cofre no portal de saudação e fornecê-la como ferramenta de toohello de entrada.</span><span class="sxs-lookup"><span data-stu-id="e9be7-134">Download a new Vault Registration file from hello portal and provide it as input toohello tool.</span></span>

  ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
5. <span data-ttu-id="e9be7-136">Fornecer novos detalhes do servidor Proxy hello e clique em Olá **registrar** botão.</span><span class="sxs-lookup"><span data-stu-id="e9be7-136">Provide hello new Proxy Server details and click hello **Register** button.</span></span>
6. <span data-ttu-id="e9be7-137">Abra uma janela de comando do PowerShell do Administrador.</span><span class="sxs-lookup"><span data-stu-id="e9be7-137">Open an Admin PowerShell command window.</span></span>
7. <span data-ttu-id="e9be7-138">Olá executar comando a seguir</span><span class="sxs-lookup"><span data-stu-id="e9be7-138">Run hello following command</span></span>
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```

  >[!WARNING]
  <span data-ttu-id="e9be7-139">Se você tiver servidores de processo de expansão anexado toothis servidor de configuração, é necessário muito[corrigir as configurações de proxy de saudação em todos os servidores de processo de expansão Olá](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) em sua implantação.</span><span class="sxs-lookup"><span data-stu-id="e9be7-139">If you have Scale-out Process servers attached toothis Configuration Server, you need too[fix hello proxy settings on all hello scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) in your deployment.</span></span>

## <a name="re-register-a-configuration-server-with-hello-same-recovery-services-vault"></a><span data-ttu-id="e9be7-140">Registrar novamente um servidor de configuração com hello mesmo Cofre de serviços de recuperação</span><span class="sxs-lookup"><span data-stu-id="e9be7-140">Re-register a Configuration Server with hello same Recovery Services Vault</span></span>
  1. <span data-ttu-id="e9be7-141">Logon tooyour servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="e9be7-141">Login tooyour Configuration Server.</span></span>
  2. <span data-ttu-id="e9be7-142">Inicie cspsconfigtool.exe hello usando o atalho de saudação na área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="e9be7-142">Launch hello cspsconfigtool.exe using hello shortcut on your desktop.</span></span>
  3. <span data-ttu-id="e9be7-143">Clique em Olá **registro do cofre** guia.</span><span class="sxs-lookup"><span data-stu-id="e9be7-143">Click hello **Vault Registration** tab.</span></span>
  4. <span data-ttu-id="e9be7-144">Baixe um novo arquivo de registro do portal hello e fornecê-la como ferramenta de toohello de entrada.</span><span class="sxs-lookup"><span data-stu-id="e9be7-144">Download a new Registration file from hello portal and provide it as input toohello tool.</span></span>
        <span data-ttu-id="e9be7-145">![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)</span><span class="sxs-lookup"><span data-stu-id="e9be7-145">![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)</span></span>
  5. <span data-ttu-id="e9be7-146">Fornecer detalhes de servidor Proxy hello e clique em Olá **registrar** botão.</span><span class="sxs-lookup"><span data-stu-id="e9be7-146">Provide hello Proxy Server details and click hello **Register** button.</span></span>  
  6. <span data-ttu-id="e9be7-147">Abra uma janela de comando do PowerShell do Administrador.</span><span class="sxs-lookup"><span data-stu-id="e9be7-147">Open an Admin PowerShell command window.</span></span>
  7. <span data-ttu-id="e9be7-148">Olá executar comando a seguir</span><span class="sxs-lookup"><span data-stu-id="e9be7-148">Run hello following command</span></span>

      ```
      $pwd = ConvertTo-SecureString -String MyProxyUserPassword
      Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
      net stop obengine
      net start obengine
      ```

  >[!WARNING]
  <span data-ttu-id="e9be7-149">Se você tiver servidores de processo de expansão anexado toothis servidor de configuração, é necessário muito[registrar novamente todos os servidores de processo de expansão Olá](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) em sua implantação.</span><span class="sxs-lookup"><span data-stu-id="e9be7-149">If you have Scale-out Process servers attached toothis Configuration Server, you need too[re-register all hello scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) in your deployment.</span></span>

## <a name="registering-a-configuration-server-with-a-different-recovery-services-vault"></a><span data-ttu-id="e9be7-150">Registrar um servidor de configuração com um cofre de serviços de recuperação diferente.</span><span class="sxs-lookup"><span data-stu-id="e9be7-150">Registering a Configuration Server with a different Recovery Services Vault.</span></span>
1. <span data-ttu-id="e9be7-151">Logon tooyour servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="e9be7-151">Login tooyour Configuration Server.</span></span>
2. <span data-ttu-id="e9be7-152">em um prompt de comando do administrador, execute o comando de saudação</span><span class="sxs-lookup"><span data-stu-id="e9be7-152">from an admin command prompt, run hello command</span></span>

```
reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
net stop dra
```
3. <span data-ttu-id="e9be7-153">Iniciar cspsconfigtool.exe hello usando o atalho de saudação em seu.</span><span class="sxs-lookup"><span data-stu-id="e9be7-153">Launch hello cspsconfigtool.exe using hello shortcut on your.</span></span>
4. <span data-ttu-id="e9be7-154">Clique em Olá **registro do cofre** guia.</span><span class="sxs-lookup"><span data-stu-id="e9be7-154">Click hello **Vault Registration** tab.</span></span>
5. <span data-ttu-id="e9be7-155">Baixe um novo arquivo de registro do portal hello e fornecê-la como ferramenta de toohello de entrada.</span><span class="sxs-lookup"><span data-stu-id="e9be7-155">Download a new Registration file from hello portal and provide it as input toohello tool.</span></span>

    ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
6. <span data-ttu-id="e9be7-157">Fornecer detalhes de servidor Proxy hello e clique em Olá **registrar** botão.</span><span class="sxs-lookup"><span data-stu-id="e9be7-157">Provide hello Proxy Server details and click hello **Register** button.</span></span>  
7. <span data-ttu-id="e9be7-158">Abra uma janela de comando do PowerShell do Administrador.</span><span class="sxs-lookup"><span data-stu-id="e9be7-158">Open an Admin PowerShell command window.</span></span>
8. <span data-ttu-id="e9be7-159">Olá executar comando a seguir</span><span class="sxs-lookup"><span data-stu-id="e9be7-159">Run hello following command</span></span>
    ```
    $pwd = ConvertTo-SecureString -String MyProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
    ```

## <a name="decommissioning-a-configuration-server"></a><span data-ttu-id="e9be7-160">Encerramento de um Servidor de Configuração</span><span class="sxs-lookup"><span data-stu-id="e9be7-160">Decommissioning a Configuration Server</span></span>
<span data-ttu-id="e9be7-161">Certifique-se de seguir Olá antes de iniciar o encerramento de seu servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="e9be7-161">Ensure hello following before you start decommissioning your Configuration Server.</span></span>
1. <span data-ttu-id="e9be7-162">Desabilite a proteção para todas as máquinas virtuais por este servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="e9be7-162">Disable protection for all virtual machines under this Configuration Server.</span></span>
2. <span data-ttu-id="e9be7-163">Desassocie todas as políticas de replicação de saudação servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="e9be7-163">Disassociate all Replication policies from hello Configuration Server.</span></span>
3. <span data-ttu-id="e9be7-164">Exclua todos os hosts de servidores/vSphere vCenters que estão associado toohello servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="e9be7-164">Delete all vCenters servers/vSphere hosts that are associated toohello Configuration Server.</span></span>

### <a name="delete-hello-configuration-server-from-azure-portal"></a><span data-ttu-id="e9be7-165">Excluir Olá servidor de configuração do portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e9be7-165">Delete hello Configuration Server from Azure portal</span></span>
1. <span data-ttu-id="e9be7-166">No portal do Azure, procurar muito**infra-estrutura de recuperação de Site** > **servidores de configuração** no menu de cofre hello.</span><span class="sxs-lookup"><span data-stu-id="e9be7-166">In Azure portal, browse too**Site Recovery Infrastructure** > **Configuration Servers** from hello Vault menu.</span></span>
2. <span data-ttu-id="e9be7-167">Clique em Olá servidor de configuração que você deseja toodecommission.</span><span class="sxs-lookup"><span data-stu-id="e9be7-167">Click hello Configuration Server that you want toodecommission.</span></span>
3. <span data-ttu-id="e9be7-168">Na página de detalhes do servidor de configuração hello, clique botão de exclusão de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9be7-168">On hello Configuration Server's details page, click hello Delete button.</span></span>

  ![delete-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/delete-configuration-server.PNG)
4. <span data-ttu-id="e9be7-170">Clique em **Sim** tooconfirm exclusão de saudação do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9be7-170">Click **Yes** tooconfirm hello deletion of hello server.</span></span>

  >[!WARNING]
  <span data-ttu-id="e9be7-171">Se você tiver máquinas virtuais, políticas de replicação ou hosts de servidores/vSphere vCenter associados a este servidor de configuração, você não pode excluir o servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9be7-171">If you have any virtual machines, Replication policies or vCenter servers/vSphere hosts associated with this Configuration Server, you cannot delete hello server.</span></span> <span data-ttu-id="e9be7-172">Exclua essas entidades antes de tentar toodelete Cofre de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9be7-172">Delete these entities before you try toodelete hello vault.</span></span>

### <a name="uninstall-hello-configuration-server-software-and-its-dependencies"></a><span data-ttu-id="e9be7-173">Desinstalar o software de servidor de configuração de saudação e suas dependências</span><span class="sxs-lookup"><span data-stu-id="e9be7-173">Uninstall hello Configuration Server software and its dependencies</span></span>
  > [!TIP]
  <span data-ttu-id="e9be7-174">Se planejar Olá tooreuse servidor de configuração com o Azure Site Recovery novamente, em seguida, você poderá ignorar toostep 4 diretamente</span><span class="sxs-lookup"><span data-stu-id="e9be7-174">If you plan tooreuse hello Configuration Server with Azure Site Recovery again, then you can skip toostep 4 directly</span></span>

1. <span data-ttu-id="e9be7-175">Faça logon no toohello servidor de configuração como um administrador.</span><span class="sxs-lookup"><span data-stu-id="e9be7-175">Log on toohello Configuration Server as an Administrator.</span></span>
2. <span data-ttu-id="e9be7-176">Abrir o Painel de Controle > Programa > Desinstalar Programas</span><span class="sxs-lookup"><span data-stu-id="e9be7-176">Open up Control Panel > Program > Uninstall Programs</span></span>
3. <span data-ttu-id="e9be7-177">Desinstale programas Olá Olá sequência a seguir:</span><span class="sxs-lookup"><span data-stu-id="e9be7-177">Uninstall hello programs in hello following sequence:</span></span>
  * <span data-ttu-id="e9be7-178">Agente de Serviços dos Serviços de Recuperação do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="e9be7-178">Microsoft Azure Recovery Services Agent</span></span>
  * <span data-ttu-id="e9be7-179">Servidor de destino do Microsoft Azure Site Recovery mobilidade mestra do serviço</span><span class="sxs-lookup"><span data-stu-id="e9be7-179">Microsoft Azure Site Recovery Mobility Service/Master Target server</span></span>
  * <span data-ttu-id="e9be7-180">Provedor do Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="e9be7-180">Microsoft Azure Site Recovery Provider</span></span>
  * <span data-ttu-id="e9be7-181">Servidor de processo/servidor de configuração do Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="e9be7-181">Microsoft Azure Site Recovery Configuration Server/Process Server</span></span>
  * <span data-ttu-id="e9be7-182">Dependências de servidor de configuração do Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="e9be7-182">Microsoft Azure Site Recovery Configuration Server Dependencies</span></span>
  * <span data-ttu-id="e9be7-183">MySQL Server 5.5</span><span class="sxs-lookup"><span data-stu-id="e9be7-183">MySQL Server 5.5</span></span>
4. <span data-ttu-id="e9be7-184">Execute hello comando a seguir e o prompt de comando do administrador.</span><span class="sxs-lookup"><span data-stu-id="e9be7-184">Run hello following command from and admin command prompt.</span></span>
  ```
  reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
  ```

## <a name="renew-configuration-server-secure-socket-layerssl-certificates"></a><span data-ttu-id="e9be7-185">Renovar certificados de configuração de servidor Secure Socket Layer(SSL)</span><span class="sxs-lookup"><span data-stu-id="e9be7-185">Renew Configuration Server Secure Socket Layer(SSL) Certificates</span></span>
<span data-ttu-id="e9be7-186">Olá, servidor de configuração tem uma servidor Web embutida, que coordena as atividades de saudação do hello serviço de mobilidade, servidores de processo, e servidores de destino mestre conectado toohello servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="e9be7-186">hello Configuration Server has an inbuilt webserver, which orchestrates hello activities of hello Mobility Service, Process Servers, and Master Target servers connected toohello Configuration Server.</span></span> <span data-ttu-id="e9be7-187">servidor da Web do servidor de configuração Olá usa um tooauthenticate de certificado SSL seus clientes.</span><span class="sxs-lookup"><span data-stu-id="e9be7-187">hello Configuration Server's webserver uses an SSL certificate tooauthenticate its clients.</span></span> <span data-ttu-id="e9be7-188">Este certificado tem uma expiração de três anos e poderá ser renovado a qualquer momento usando Olá método a seguir:</span><span class="sxs-lookup"><span data-stu-id="e9be7-188">This certificate has an expiry of three years and can be renewed at any time using hello following method:</span></span>

> [!WARNING]
<span data-ttu-id="e9be7-189">Expiração do certificado pode ser executada somente na versão 9.4.XXXX. X ou superior.</span><span class="sxs-lookup"><span data-stu-id="e9be7-189">Certificate expiry can be performed only on version 9.4.XXXX.X or higher.</span></span> <span data-ttu-id="e9be7-190">Atualizar todos os componentes hello Azure Site Recovery (servidor de configuração, servidor de processo, o servidor de destino mestre, serviço de mobilidade) antes de iniciar o fluxo de trabalho do hello renovar certificados.</span><span class="sxs-lookup"><span data-stu-id="e9be7-190">Upgrade all hello Azure Site Recovery components (Configuration Server, Process Server, Master Target Server, Mobility Service) before you start hello Renew Certificates workflow.</span></span>

1. <span data-ttu-id="e9be7-191">Olá portal do Azure, procurar tooyour cofre > infraestrutura de recuperação do Site > Configuração do servidor.</span><span class="sxs-lookup"><span data-stu-id="e9be7-191">On hello Azure portal, browse tooyour Vault > Site Recovery Infrastructure > Configuration Server.</span></span>
2. <span data-ttu-id="e9be7-192">Clique em servidor de configuração de saudação para as quais você precisa toorenew Olá certificado SSL para.</span><span class="sxs-lookup"><span data-stu-id="e9be7-192">Click hello Configuration Server for which you need toorenew hello SSL Certificate for.</span></span>
3. <span data-ttu-id="e9be7-193">Em Olá integridade do servidor de configuração, você poderá ver a data de expiração de saudação para Olá certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="e9be7-193">Under hello Configuration Server health, you can see hello expiry date for hello SSL Certificate.</span></span>
4. <span data-ttu-id="e9be7-194">Renovar certificado de saudação clicando Olá **renovar certificados** ação conforme Olá a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="e9be7-194">Renew hello certificate by clicking hello **Renew Certificates** action as shown in hello following image:</span></span>

  ![delete-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/renew-cert-page.png)

### <a name="secure-socket-layer-certificate-expiry-warning"></a><span data-ttu-id="e9be7-196">Aviso de expiração de certificado SSL</span><span class="sxs-lookup"><span data-stu-id="e9be7-196">Secure Socket Layer certificate expiry warning</span></span>

> [!NOTE]
<span data-ttu-id="e9be7-197">Olá a validade do certificado SSL para todas as instalações que ocorreram antes de maio de 2016 foi definida tooone ano.</span><span class="sxs-lookup"><span data-stu-id="e9be7-197">hello SSL Certificate's validity for all installations that happened before May 2016 was set tooone year.</span></span> <span data-ttu-id="e9be7-198">você iniciou vendo notificações de expiração do certificado aparecendo no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e9be7-198">you have started seeing certificate expiry notifications showing up in hello Azure portal.</span></span>

1. <span data-ttu-id="e9be7-199">Se certificado SSL do servidor de configuração Olá tooexpire em Olá próximos dois meses, o serviço de saudação inicia notificar os usuários por meio de saudação portal do Azure & email (necessário notificações de recuperação de Site tooAzure toobe assinado).</span><span class="sxs-lookup"><span data-stu-id="e9be7-199">If hello Configuration Server's SSL certificate is going tooexpire in hello next two months, hello service starts notifying users via hello Azure portal & email (you need toobe subscribed tooAzure Site Recovery notifications).</span></span> <span data-ttu-id="e9be7-200">Você começar a ver uma faixa de notificação na página de recursos de saudação do cofre.</span><span class="sxs-lookup"><span data-stu-id="e9be7-200">You start seeing a notification banner on hello Vault's resource page.</span></span>

  ![certificate-notification](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-renew-notification.png)
2. <span data-ttu-id="e9be7-202">Clique em detalhes adicionais do hello faixa tooget na expiração do certificado hello.</span><span class="sxs-lookup"><span data-stu-id="e9be7-202">Click hello banner tooget additional details on hello Certificate expiry.</span></span>

  ![certificate-details](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-expiry-details.png)

  >[!TIP]
  <span data-ttu-id="e9be7-204">Se em vez de um botão **Renovar Agora** você vir um botão **Atualizar Agora**.</span><span class="sxs-lookup"><span data-stu-id="e9be7-204">If instead of a **Renew Now** button you see an **Upgrade Now** button.</span></span> <span data-ttu-id="e9be7-205">Isso significa que há alguns componentes em seu ambiente que ainda não foram atualizados too9.4.xxxx.x ou versões posteriores.</span><span class="sxs-lookup"><span data-stu-id="e9be7-205">This means that there are some components in your environment that have not yet been upgraded too9.4.xxxx.x or higher versions.</span></span>

## <a name="sizing-requirements-for-a-configuration-server"></a><span data-ttu-id="e9be7-206">Requisitos de dimensionamento para um servidor de configuração</span><span class="sxs-lookup"><span data-stu-id="e9be7-206">Sizing requirements for a Configuration Server</span></span>

| <span data-ttu-id="e9be7-207">**CPU**</span><span class="sxs-lookup"><span data-stu-id="e9be7-207">**CPU**</span></span> | <span data-ttu-id="e9be7-208">**Memória**</span><span class="sxs-lookup"><span data-stu-id="e9be7-208">**Memory**</span></span> | <span data-ttu-id="e9be7-209">**Tamanho do disco de cache**</span><span class="sxs-lookup"><span data-stu-id="e9be7-209">**Cache disk size**</span></span> | <span data-ttu-id="e9be7-210">**Taxa de alteração de dados**</span><span class="sxs-lookup"><span data-stu-id="e9be7-210">**Data change rate**</span></span> | <span data-ttu-id="e9be7-211">**Computadores protegidos**</span><span class="sxs-lookup"><span data-stu-id="e9be7-211">**Protected machines**</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="e9be7-212">8 vCPUs (2 soquetes * 4 núcleos @ 2,5 GHz)</span><span class="sxs-lookup"><span data-stu-id="e9be7-212">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="e9be7-213">16 GB</span><span class="sxs-lookup"><span data-stu-id="e9be7-213">16 GB</span></span> |<span data-ttu-id="e9be7-214">300 GB</span><span class="sxs-lookup"><span data-stu-id="e9be7-214">300 GB</span></span> |<span data-ttu-id="e9be7-215">500 GB ou menos</span><span class="sxs-lookup"><span data-stu-id="e9be7-215">500 GB or less</span></span> |<span data-ttu-id="e9be7-216">Replicar máquinas menos de 100.</span><span class="sxs-lookup"><span data-stu-id="e9be7-216">Replicate fewer than 100 machines.</span></span> |
| <span data-ttu-id="e9be7-217">12 vCPUs (2 soquetes * 6 núcleos @ 2,5 GHz)</span><span class="sxs-lookup"><span data-stu-id="e9be7-217">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="e9be7-218">18 GB</span><span class="sxs-lookup"><span data-stu-id="e9be7-218">18 GB</span></span> |<span data-ttu-id="e9be7-219">600 GB</span><span class="sxs-lookup"><span data-stu-id="e9be7-219">600 GB</span></span> |<span data-ttu-id="e9be7-220">500 GB too1 TB</span><span class="sxs-lookup"><span data-stu-id="e9be7-220">500 GB too1 TB</span></span> |<span data-ttu-id="e9be7-221">Replique entre 100 e 150 computadores.</span><span class="sxs-lookup"><span data-stu-id="e9be7-221">Replicate between 100-150 machines.</span></span> |
| <span data-ttu-id="e9be7-222">16 vCPUs (2 soquetes * 8 núcleos @ 2,5 GHz)</span><span class="sxs-lookup"><span data-stu-id="e9be7-222">16 vCPUs (2 sockets * 8 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="e9be7-223">32 GB</span><span class="sxs-lookup"><span data-stu-id="e9be7-223">32 GB</span></span> |<span data-ttu-id="e9be7-224">1 TB</span><span class="sxs-lookup"><span data-stu-id="e9be7-224">1 TB</span></span> |<span data-ttu-id="e9be7-225">1 TB too2 TB</span><span class="sxs-lookup"><span data-stu-id="e9be7-225">1 TB too2 TB</span></span> |<span data-ttu-id="e9be7-226">Replique entre 150 e 200 computadores.</span><span class="sxs-lookup"><span data-stu-id="e9be7-226">Replicate between 150-200 machines.</span></span> |

  >[!TIP]
  <span data-ttu-id="e9be7-227">Se a rotatividade de dados diariamente excede 2 TB, ou planejar tooreplicate mais de 200 máquinas virtuais, é recomendável tráfego de replicação toodeploy processo adicional servidores tooload saldo hello.</span><span class="sxs-lookup"><span data-stu-id="e9be7-227">If your daily data churn exceeds 2 TB, or you plan tooreplicate more than 200 virtual machines, it is recommended toodeploy additional process servers tooload balance hello replication traffic.</span></span> <span data-ttu-id="e9be7-228">Saiba mais sobre como os servidores de toodeploy o processo de expansão.</span><span class="sxs-lookup"><span data-stu-id="e9be7-228">Learn more about How toodeploy Scale-out Process severs.</span></span>


## <a name="common-issues"></a><span data-ttu-id="e9be7-229">Problemas comuns</span><span class="sxs-lookup"><span data-stu-id="e9be7-229">Common issues</span></span>
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]
