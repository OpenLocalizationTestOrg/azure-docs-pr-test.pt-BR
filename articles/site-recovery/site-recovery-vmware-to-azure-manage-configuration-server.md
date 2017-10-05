---
title: " Gerenciar um Servidor de Configuração no Azure Site Recovery | Microsoft Docs"
description: "Este artigo descreve como configurar e gerenciar um servidor de configuração."
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
ms.openlocfilehash: 36da8c7d0f3ace194522e5288f26069cf46d470e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-a-configuration-server"></a><span data-ttu-id="b3ada-103">Gerenciar um Servidor de Configuração</span><span class="sxs-lookup"><span data-stu-id="b3ada-103">Manage a Configuration Server</span></span>

<span data-ttu-id="b3ada-104">Servidor de configuração atua como um coordenador entre os serviços do Site Recovery e sua infraestrutura local.</span><span class="sxs-lookup"><span data-stu-id="b3ada-104">Configuration Server acts as a coordinator between the Site Recovery services and your on-premises infrastructure.</span></span> <span data-ttu-id="b3ada-105">Este artigo descreve como você pode definir, configurar e gerenciar o servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="b3ada-105">This article describes how you can set up, configure, and manage the Configuration Server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b3ada-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b3ada-106">Prerequisites</span></span>
<span data-ttu-id="b3ada-107">A seguir está os mínimos de hardware, software e configuração de rede necessária para configurar um servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="b3ada-107">The following are the minimum hardware, software, and network configuration required to set up a Configuration Server.</span></span>

> [!NOTE]
> <span data-ttu-id="b3ada-108">[Planejamento de capacidade](site-recovery-capacity-planner.md) é uma etapa importante para garantir que você implantar o servidor de configuração com uma configuração que conjuntos de seus requisitos de carga.</span><span class="sxs-lookup"><span data-stu-id="b3ada-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step to ensure that you deploy the Configuration Server with a configuration that suites your load requirements.</span></span> <span data-ttu-id="b3ada-109">Leia mais sobre [requisitos para um servidor de configuração de dimensionamento](#sizing-requirements-for-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="b3ada-109">Read more about [Sizing requirements for a Configuration Server](#sizing-requirements-for-a-configuration-server).</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-the-configuration-server-software"></a><span data-ttu-id="b3ada-110">Baixar o software de servidor de configuração</span><span class="sxs-lookup"><span data-stu-id="b3ada-110">Downloading the Configuration Server software</span></span>
1. <span data-ttu-id="b3ada-111">Faça logon no portal do Azure e navegue até seu Cofre de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="b3ada-111">Log on to the Azure portal and browse to your Recovery Services Vault.</span></span>
2. <span data-ttu-id="b3ada-112">Navegue até **Infraestrutura do Site Recovery** > **Servidores de Configuração** (sob Para Máquinas VMware e Físicas).</span><span class="sxs-lookup"><span data-stu-id="b3ada-112">Browse to **Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span></span>

  ![Página Adicionar Servidores](./media/site-recovery-vmware-to-azure-manage-configuration-server/AddServers.png)
3. <span data-ttu-id="b3ada-114">Clique no botão **+Servidores**.</span><span class="sxs-lookup"><span data-stu-id="b3ada-114">Click the **+Servers** button.</span></span>
4. <span data-ttu-id="b3ada-115">Na página **Adicionar Servidor**, clique no botão Baixar para baixar a chave de Registro.</span><span class="sxs-lookup"><span data-stu-id="b3ada-115">On the **Add Server** page, click the Download button to download the Registration key.</span></span> <span data-ttu-id="b3ada-116">Você precisa dessa chave durante a instalação do servidor de configuração para registrá-lo no serviço Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="b3ada-116">You need this key during the Configuration Server installation to register it with Azure Site Recovery service.</span></span>
5. <span data-ttu-id="b3ada-117">Clique no link **Baixar a instalação do Microsoft Azure Site Recovery Unified** para baixar a versão mais recente do Servidor de Configuração.</span><span class="sxs-lookup"><span data-stu-id="b3ada-117">Click the **Download the Microsoft Azure Site Recovery Unified Setup** link to download the latest version of the Configuration Server.</span></span>

  ![Página Download](./media/site-recovery-vmware-to-azure-manage-configuration-server/downloadcs.png)

  > [!TIP]
  <span data-ttu-id="b3ada-119">A versão mais recente do servidor de configuração pode ser baixada diretamente da [página de download do Microsoft Download Center](http://aka.ms/unifiedsetup)</span><span class="sxs-lookup"><span data-stu-id="b3ada-119">Latest version of the Configuration Server can be downloaded directly from [Microsoft Download Center download page](http://aka.ms/unifiedsetup)</span></span>

## <a name="installing-and-registering-a-configuration-server-from-gui"></a><span data-ttu-id="b3ada-120">Instalar e registrar um servidor de configuração da GUI</span><span class="sxs-lookup"><span data-stu-id="b3ada-120">Installing and Registering a Configuration Server from GUI</span></span>
[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

## <a name="installing-and-registering-a-configuration-server-using-command-line"></a><span data-ttu-id="b3ada-121">Instalar e registrar um servidor de configuração usando a linha de comando</span><span class="sxs-lookup"><span data-stu-id="b3ada-121">Installing and registering a Configuration Server using Command line</span></span>

  ```
  UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address to be used for data transfer] [/CSIP <IP address of CS to be registered with>] [/PassphraseFilePath <Passphrase file path>]
  ```

### <a name="sample-usage"></a><span data-ttu-id="b3ada-122">Exemplo de uso</span><span class="sxs-lookup"><span data-stu-id="b3ada-122">Sample usage</span></span>
  ```
  MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
  cd C:\Temp\Extracted
  UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "CS" /InstallLocation "D:\" /MySQLCredsFilePath "C:\Temp\MySQLCredentialsfile.txt" /VaultCredsFilePath "C:\Temp\MyVault.vaultcredentials" /EnvType "VMWare"
  ```


### <a name="configuration-server-installer-command-line-arguments"></a><span data-ttu-id="b3ada-123">Argumentos de linha de comando do instalador do servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="b3ada-123">Configuration Server installer command-line arguments.</span></span>
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-mysql-credentials-file"></a><span data-ttu-id="b3ada-124">Criar um arquivo de credenciais do MySql</span><span class="sxs-lookup"><span data-stu-id="b3ada-124">Create a MySql credentials file</span></span>
<span data-ttu-id="b3ada-125">Parâmetro MySQLCredsFilePath utiliza um arquivo como entrada.</span><span class="sxs-lookup"><span data-stu-id="b3ada-125">MySQLCredsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="b3ada-126">Crie o arquivo usando o formato a seguir e passá-lo como parâmetro de entrada MySQLCredsFilePath.</span><span class="sxs-lookup"><span data-stu-id="b3ada-126">Create the file using the following format and pass it as input MySQLCredsFilePath parameter.</span></span>
```
[MySQLCredentials]
MySQLRootPassword = "Password>"
MySQLUserPassword = "Password"
```
### <a name="create-a-proxy-settings-configuration-file"></a><span data-ttu-id="b3ada-127">Criar um arquivo de configuração de configurações de proxy</span><span class="sxs-lookup"><span data-stu-id="b3ada-127">Create a proxy settings configuration file</span></span>
<span data-ttu-id="b3ada-128">Parâmetro ProxySettingsFilePath utiliza um arquivo como entrada.</span><span class="sxs-lookup"><span data-stu-id="b3ada-128">ProxySettingsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="b3ada-129">Crie o arquivo usando o formato a seguir e passá-lo como parâmetro de entrada ProxySettingsFilePath.</span><span class="sxs-lookup"><span data-stu-id="b3ada-129">Create the file using the following format and pass it as input ProxySettingsFilePath parameter.</span></span>

```
[ProxySettings]
ProxyAuthentication = "Yes/No"
Proxy IP = "IP Address"
ProxyPort = "Port"
ProxyUserName="UserName"
ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-configuration-server"></a><span data-ttu-id="b3ada-130">Modificando configurações de proxy de servidor de configuração</span><span class="sxs-lookup"><span data-stu-id="b3ada-130">Modifying proxy settings for Configuration Server</span></span>
1. <span data-ttu-id="b3ada-131">Faça logon no Servidor de Configuração.</span><span class="sxs-lookup"><span data-stu-id="b3ada-131">Login to your Configuration Server.</span></span>
2. <span data-ttu-id="b3ada-132">Inicie o cspsconfigtool.exe usando o atalho.</span><span class="sxs-lookup"><span data-stu-id="b3ada-132">Launch the cspsconfigtool.exe using the shortcut on your.</span></span>
3. <span data-ttu-id="b3ada-133">Clique na guia **Registro do Cofre**.</span><span class="sxs-lookup"><span data-stu-id="b3ada-133">Click the **Vault Registration** tab.</span></span>
4. <span data-ttu-id="b3ada-134">Download de um novo arquivo de registro do cofre no portal e fornecê-la como entrada para a ferramenta.</span><span class="sxs-lookup"><span data-stu-id="b3ada-134">Download a new Vault Registration file from the portal and provide it as input to the tool.</span></span>

  ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
5. <span data-ttu-id="b3ada-136">Forneça os detalhes do novo servidor Proxy e clique no botão **Registrar**.</span><span class="sxs-lookup"><span data-stu-id="b3ada-136">Provide the new Proxy Server details and click the **Register** button.</span></span>
6. <span data-ttu-id="b3ada-137">Abra uma janela de comando do PowerShell do Administrador.</span><span class="sxs-lookup"><span data-stu-id="b3ada-137">Open an Admin PowerShell command window.</span></span>
7. <span data-ttu-id="b3ada-138">Execute o comando a seguir</span><span class="sxs-lookup"><span data-stu-id="b3ada-138">Run the following command</span></span>
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```

  >[!WARNING]
  <span data-ttu-id="b3ada-139">Se você tiver anexados a este servidor de configuração de servidores de processo de expansão, você precisa [corrigir as configurações de proxy em todos os servidores de processo de expansão](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) em sua implantação.</span><span class="sxs-lookup"><span data-stu-id="b3ada-139">If you have Scale-out Process servers attached to this Configuration Server, you need to [fix the proxy settings on all the scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#modifying-proxy-settings-for-scale-out-process-server) in your deployment.</span></span>

## <a name="re-register-a-configuration-server-with-the-same-recovery-services-vault"></a><span data-ttu-id="b3ada-140">Registrar novamente um Servidor de Configuração com o mesmo Cofre de Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="b3ada-140">Re-register a Configuration Server with the same Recovery Services Vault</span></span>
  1. <span data-ttu-id="b3ada-141">Faça logon no Servidor de Configuração.</span><span class="sxs-lookup"><span data-stu-id="b3ada-141">Login to your Configuration Server.</span></span>
  2. <span data-ttu-id="b3ada-142">Inicie o cspsconfigtool.exe usando o atalho na sua área de trabalho.</span><span class="sxs-lookup"><span data-stu-id="b3ada-142">Launch the cspsconfigtool.exe using the shortcut on your desktop.</span></span>
  3. <span data-ttu-id="b3ada-143">Clique na guia **Registro do Cofre**.</span><span class="sxs-lookup"><span data-stu-id="b3ada-143">Click the **Vault Registration** tab.</span></span>
  4. <span data-ttu-id="b3ada-144">Download de um novo arquivo de registro no portal e fornecê-la como entrada para a ferramenta.</span><span class="sxs-lookup"><span data-stu-id="b3ada-144">Download a new Registration file from the portal and provide it as input to the tool.</span></span>
        <span data-ttu-id="b3ada-145">![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)</span><span class="sxs-lookup"><span data-stu-id="b3ada-145">![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)</span></span>
  5. <span data-ttu-id="b3ada-146">Forneça os detalhes do servidor Proxy e clique no **registrar** botão.</span><span class="sxs-lookup"><span data-stu-id="b3ada-146">Provide the Proxy Server details and click the **Register** button.</span></span>  
  6. <span data-ttu-id="b3ada-147">Abra uma janela de comando do PowerShell do Administrador.</span><span class="sxs-lookup"><span data-stu-id="b3ada-147">Open an Admin PowerShell command window.</span></span>
  7. <span data-ttu-id="b3ada-148">Execute o comando a seguir</span><span class="sxs-lookup"><span data-stu-id="b3ada-148">Run the following command</span></span>

      ```
      $pwd = ConvertTo-SecureString -String MyProxyUserPassword
      Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
      net stop obengine
      net start obengine
      ```

  >[!WARNING]
  <span data-ttu-id="b3ada-149">Se você tiver anexados a este servidor de configuração de servidores de processo de expansão, você precisa [registrar novamente todos os servidores de processo de expansão](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) em sua implantação.</span><span class="sxs-lookup"><span data-stu-id="b3ada-149">If you have Scale-out Process servers attached to this Configuration Server, you need to [re-register all the scale-out process servers](site-recovery-vmware-to-azure-manage-scaleout-process-server.md#re-registering-a-scale-out-process-server) in your deployment.</span></span>

## <a name="registering-a-configuration-server-with-a-different-recovery-services-vault"></a><span data-ttu-id="b3ada-150">Registrar um servidor de configuração com um cofre de serviços de recuperação diferente.</span><span class="sxs-lookup"><span data-stu-id="b3ada-150">Registering a Configuration Server with a different Recovery Services Vault.</span></span>
1. <span data-ttu-id="b3ada-151">Faça logon no Servidor de Configuração.</span><span class="sxs-lookup"><span data-stu-id="b3ada-151">Login to your Configuration Server.</span></span>
2. <span data-ttu-id="b3ada-152">em um prompt de comando de administrador, execute o comando</span><span class="sxs-lookup"><span data-stu-id="b3ada-152">from an admin command prompt, run the command</span></span>

```
reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
net stop dra
```
3. <span data-ttu-id="b3ada-153">Inicie o cspsconfigtool.exe usando o atalho.</span><span class="sxs-lookup"><span data-stu-id="b3ada-153">Launch the cspsconfigtool.exe using the shortcut on your.</span></span>
4. <span data-ttu-id="b3ada-154">Clique na guia **Registro do Cofre**.</span><span class="sxs-lookup"><span data-stu-id="b3ada-154">Click the **Vault Registration** tab.</span></span>
5. <span data-ttu-id="b3ada-155">Download de um novo arquivo de registro no portal e fornecê-la como entrada para a ferramenta.</span><span class="sxs-lookup"><span data-stu-id="b3ada-155">Download a new Registration file from the portal and provide it as input to the tool.</span></span>

    ![register-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/register-csonfiguration-server.png)
6. <span data-ttu-id="b3ada-157">Forneça os detalhes do servidor Proxy e clique no **registrar** botão.</span><span class="sxs-lookup"><span data-stu-id="b3ada-157">Provide the Proxy Server details and click the **Register** button.</span></span>  
7. <span data-ttu-id="b3ada-158">Abra uma janela de comando do PowerShell do Administrador.</span><span class="sxs-lookup"><span data-stu-id="b3ada-158">Open an Admin PowerShell command window.</span></span>
8. <span data-ttu-id="b3ada-159">Execute o comando a seguir</span><span class="sxs-lookup"><span data-stu-id="b3ada-159">Run the following command</span></span>
    ```
    $pwd = ConvertTo-SecureString -String MyProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
    ```

## <a name="decommissioning-a-configuration-server"></a><span data-ttu-id="b3ada-160">Encerramento de um Servidor de Configuração</span><span class="sxs-lookup"><span data-stu-id="b3ada-160">Decommissioning a Configuration Server</span></span>
<span data-ttu-id="b3ada-161">Verifique o seguinte antes de iniciar, encerrar o servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="b3ada-161">Ensure the following before you start decommissioning your Configuration Server.</span></span>
1. <span data-ttu-id="b3ada-162">Desabilite a proteção para todas as máquinas virtuais por este servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="b3ada-162">Disable protection for all virtual machines under this Configuration Server.</span></span>
2. <span data-ttu-id="b3ada-163">Desassocie todas as políticas de replicação do servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="b3ada-163">Disassociate all Replication policies from the Configuration Server.</span></span>
3. <span data-ttu-id="b3ada-164">Exclua todos os servidores vCenter/hosts vSphere associados ao Servidor de Configuração.</span><span class="sxs-lookup"><span data-stu-id="b3ada-164">Delete all vCenters servers/vSphere hosts that are associated to the Configuration Server.</span></span>

### <a name="delete-the-configuration-server-from-azure-portal"></a><span data-ttu-id="b3ada-165">Excluir o servidor de configuração do portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b3ada-165">Delete the Configuration Server from Azure portal</span></span>
1. <span data-ttu-id="b3ada-166">No portal do Azure, navegue até **Infraestrutura do Site Recovery** > **Servidores de Configuração** no menu Cofre.</span><span class="sxs-lookup"><span data-stu-id="b3ada-166">In Azure portal, browse to **Site Recovery Infrastructure** > **Configuration Servers** from the Vault menu.</span></span>
2. <span data-ttu-id="b3ada-167">Clique no servidor de configuração que você deseja encerrar.</span><span class="sxs-lookup"><span data-stu-id="b3ada-167">Click the Configuration Server that you want to decommission.</span></span>
3. <span data-ttu-id="b3ada-168">Na página de detalhes de configuração do servidor, clique no botão Excluir.</span><span class="sxs-lookup"><span data-stu-id="b3ada-168">On the Configuration Server's details page, click the Delete button.</span></span>

  ![delete-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/delete-configuration-server.PNG)
4. <span data-ttu-id="b3ada-170">Clique em **Sim** para confirmar a exclusão do servidor.</span><span class="sxs-lookup"><span data-stu-id="b3ada-170">Click **Yes** to confirm the deletion of the server.</span></span>

  >[!WARNING]
  <span data-ttu-id="b3ada-171">Se você tiver máquinas virtuais, políticas de replicação ou hosts de servidores/vSphere vCenter associados a este servidor de configuração, você não pode excluir o servidor.</span><span class="sxs-lookup"><span data-stu-id="b3ada-171">If you have any virtual machines, Replication policies or vCenter servers/vSphere hosts associated with this Configuration Server, you cannot delete the server.</span></span> <span data-ttu-id="b3ada-172">Exclua essas entidades antes de tentar excluir o cofre.</span><span class="sxs-lookup"><span data-stu-id="b3ada-172">Delete these entities before you try to delete the vault.</span></span>

### <a name="uninstall-the-configuration-server-software-and-its-dependencies"></a><span data-ttu-id="b3ada-173">Desinstalar o software do servidor de configuração e suas dependências</span><span class="sxs-lookup"><span data-stu-id="b3ada-173">Uninstall the Configuration Server software and its dependencies</span></span>
  > [!TIP]
  <span data-ttu-id="b3ada-174">Se você planejar reutilizar o servidor de configuração com o Azure Site Recovery novamente, poderá ignorar a etapa 4 diretamente</span><span class="sxs-lookup"><span data-stu-id="b3ada-174">If you plan to reuse the Configuration Server with Azure Site Recovery again, then you can skip to step 4 directly</span></span>

1. <span data-ttu-id="b3ada-175">Faça logon no Servidor de Configuração como um Administrador.</span><span class="sxs-lookup"><span data-stu-id="b3ada-175">Log on to the Configuration Server as an Administrator.</span></span>
2. <span data-ttu-id="b3ada-176">Abra o painel de controle > programa > desinstalar programas</span><span class="sxs-lookup"><span data-stu-id="b3ada-176">Open up Control Panel > Program > Uninstall Programs</span></span>
3. <span data-ttu-id="b3ada-177">Desinstale os programas na sequência a seguir:</span><span class="sxs-lookup"><span data-stu-id="b3ada-177">Uninstall the programs in the following sequence:</span></span>
  * <span data-ttu-id="b3ada-178">Agente de Serviços de Recuperação do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="b3ada-178">Microsoft Azure Recovery Services Agent</span></span>
  * <span data-ttu-id="b3ada-179">Servidor de destino do Microsoft Azure Site Recovery mobilidade mestra do serviço</span><span class="sxs-lookup"><span data-stu-id="b3ada-179">Microsoft Azure Site Recovery Mobility Service/Master Target server</span></span>
  * <span data-ttu-id="b3ada-180">Provedor do Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="b3ada-180">Microsoft Azure Site Recovery Provider</span></span>
  * <span data-ttu-id="b3ada-181">Servidor de processo/servidor de configuração do Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="b3ada-181">Microsoft Azure Site Recovery Configuration Server/Process Server</span></span>
  * <span data-ttu-id="b3ada-182">Dependências de servidor de configuração do Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="b3ada-182">Microsoft Azure Site Recovery Configuration Server Dependencies</span></span>
  * <span data-ttu-id="b3ada-183">MySQL Server 5.5</span><span class="sxs-lookup"><span data-stu-id="b3ada-183">MySQL Server 5.5</span></span>
4. <span data-ttu-id="b3ada-184">Execute o seguinte comando de um prompt de comando de administrador.</span><span class="sxs-lookup"><span data-stu-id="b3ada-184">Run the following command from and admin command prompt.</span></span>
  ```
  reg delete HKLM\Software\Microsoft\Azure Site Recovery\Registration
  ```

## <a name="renew-configuration-server-secure-socket-layerssl-certificates"></a><span data-ttu-id="b3ada-185">Renovar certificados de configuração de servidor Secure Socket Layer(SSL)</span><span class="sxs-lookup"><span data-stu-id="b3ada-185">Renew Configuration Server Secure Socket Layer(SSL) Certificates</span></span>
<span data-ttu-id="b3ada-186">O servidor de configuração tem uma servidor Web embutida, que coordena as atividades dos servidores de destino mestre, servidores de processo e serviço de mobilidade conectados ao servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="b3ada-186">The Configuration Server has an inbuilt webserver, which orchestrates the activities of the Mobility Service, Process Servers, and Master Target servers connected to the Configuration Server.</span></span> <span data-ttu-id="b3ada-187">Servidor Web do servidor de configuração usa um certificado SSL para autenticar seus clientes.</span><span class="sxs-lookup"><span data-stu-id="b3ada-187">The Configuration Server's webserver uses an SSL certificate to authenticate its clients.</span></span> <span data-ttu-id="b3ada-188">Este certificado tem uma expiração de três anos e pode ser renovado a qualquer momento usando o seguinte método:</span><span class="sxs-lookup"><span data-stu-id="b3ada-188">This certificate has an expiry of three years and can be renewed at any time using the following method:</span></span>

> [!WARNING]
<span data-ttu-id="b3ada-189">Expiração do certificado pode ser executada somente na versão 9.4.XXXX. X ou superior.</span><span class="sxs-lookup"><span data-stu-id="b3ada-189">Certificate expiry can be performed only on version 9.4.XXXX.X or higher.</span></span> <span data-ttu-id="b3ada-190">Atualizar todos os componentes do Azure Site Recovery (servidor de configuração, servidor de processo, servidor de destino mestre, serviço de mobilidade) antes de iniciar o fluxo de trabalho renovar certificados.</span><span class="sxs-lookup"><span data-stu-id="b3ada-190">Upgrade all the Azure Site Recovery components (Configuration Server, Process Server, Master Target Server, Mobility Service) before you start the Renew Certificates workflow.</span></span>

1. <span data-ttu-id="b3ada-191">No portal do Azure, navegue até seu Cofre > Infraestrutura do Site Recovery > Servidor de Configuração.</span><span class="sxs-lookup"><span data-stu-id="b3ada-191">On the Azure portal, browse to your Vault > Site Recovery Infrastructure > Configuration Server.</span></span>
2. <span data-ttu-id="b3ada-192">Clique no Servidor de Configuração para o qual você precisa renovar o Certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="b3ada-192">Click the Configuration Server for which you need to renew the SSL Certificate for.</span></span>
3. <span data-ttu-id="b3ada-193">Sob a integridade do Servidor de Configuração, você pode ver a data de expiração do certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="b3ada-193">Under the Configuration Server health, you can see the expiry date for the SSL Certificate.</span></span>
4. <span data-ttu-id="b3ada-194">Renove o certificado clicando na ação **Renovar Certificados** conforme mostrado na imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="b3ada-194">Renew the certificate by clicking the **Renew Certificates** action as shown in the following image:</span></span>

  ![delete-configuration-server](./media/site-recovery-vmware-to-azure-manage-configuration-server/renew-cert-page.png)

### <a name="secure-socket-layer-certificate-expiry-warning"></a><span data-ttu-id="b3ada-196">Aviso de expiração de certificado SSL</span><span class="sxs-lookup"><span data-stu-id="b3ada-196">Secure Socket Layer certificate expiry warning</span></span>

> [!NOTE]
<span data-ttu-id="b3ada-197">A validade do certificado SSL para todas as instalações que ocorreram antes de maio de 2016 foi definida como um ano.</span><span class="sxs-lookup"><span data-stu-id="b3ada-197">The SSL Certificate's validity for all installations that happened before May 2016 was set to one year.</span></span> <span data-ttu-id="b3ada-198">Você começou a ver notificações de expiração do certificado aparecendo no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b3ada-198">you have started seeing certificate expiry notifications showing up in the Azure portal.</span></span>

1. <span data-ttu-id="b3ada-199">Se o certificado SSL do Servidor de Configuração expirar nos próximos dois meses, o serviço começa a notificar os usuários por meio do portal do Azure e por email (você precisa ter assinado as notificações do Azure Site Recovery).</span><span class="sxs-lookup"><span data-stu-id="b3ada-199">If the Configuration Server's SSL certificate is going to expire in the next two months, the service starts notifying users via the Azure portal & email (you need to be subscribed to Azure Site Recovery notifications).</span></span> <span data-ttu-id="b3ada-200">Você começa a ver uma faixa de notificação na página de recursos do Cofre.</span><span class="sxs-lookup"><span data-stu-id="b3ada-200">You start seeing a notification banner on the Vault's resource page.</span></span>

  ![certificate-notification](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-renew-notification.png)
2. <span data-ttu-id="b3ada-202">Clique na faixa para obter detalhes adicionais sobre a expiração do certificado.</span><span class="sxs-lookup"><span data-stu-id="b3ada-202">Click the banner to get additional details on the Certificate expiry.</span></span>

  ![certificate-details](./media/site-recovery-vmware-to-azure-manage-configuration-server/ssl-cert-expiry-details.png)

  >[!TIP]
  <span data-ttu-id="b3ada-204">Se em vez de um botão **Renovar Agora** você vir um botão **Atualizar Agora**.</span><span class="sxs-lookup"><span data-stu-id="b3ada-204">If instead of a **Renew Now** button you see an **Upgrade Now** button.</span></span> <span data-ttu-id="b3ada-205">Isso significa que há alguns componentes em seu ambiente que ainda não foram atualizados para a versão 9.4.xxxx.x ou posteriores.</span><span class="sxs-lookup"><span data-stu-id="b3ada-205">This means that there are some components in your environment that have not yet been upgraded to 9.4.xxxx.x or higher versions.</span></span>

## <a name="sizing-requirements-for-a-configuration-server"></a><span data-ttu-id="b3ada-206">Requisitos de dimensionamento para um servidor de configuração</span><span class="sxs-lookup"><span data-stu-id="b3ada-206">Sizing requirements for a Configuration Server</span></span>

| <span data-ttu-id="b3ada-207">**CPU**</span><span class="sxs-lookup"><span data-stu-id="b3ada-207">**CPU**</span></span> | <span data-ttu-id="b3ada-208">**Memória**</span><span class="sxs-lookup"><span data-stu-id="b3ada-208">**Memory**</span></span> | <span data-ttu-id="b3ada-209">**Tamanho do disco de cache**</span><span class="sxs-lookup"><span data-stu-id="b3ada-209">**Cache disk size**</span></span> | <span data-ttu-id="b3ada-210">**Taxa de alteração de dados**</span><span class="sxs-lookup"><span data-stu-id="b3ada-210">**Data change rate**</span></span> | <span data-ttu-id="b3ada-211">**Computadores protegidos**</span><span class="sxs-lookup"><span data-stu-id="b3ada-211">**Protected machines**</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="b3ada-212">8 vCPUs (2 soquetes * 4 núcleos @ 2,5 GHz)</span><span class="sxs-lookup"><span data-stu-id="b3ada-212">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="b3ada-213">16 GB</span><span class="sxs-lookup"><span data-stu-id="b3ada-213">16 GB</span></span> |<span data-ttu-id="b3ada-214">300 GB</span><span class="sxs-lookup"><span data-stu-id="b3ada-214">300 GB</span></span> |<span data-ttu-id="b3ada-215">500 GB ou menos</span><span class="sxs-lookup"><span data-stu-id="b3ada-215">500 GB or less</span></span> |<span data-ttu-id="b3ada-216">Replicar máquinas menos de 100.</span><span class="sxs-lookup"><span data-stu-id="b3ada-216">Replicate fewer than 100 machines.</span></span> |
| <span data-ttu-id="b3ada-217">12 vCPUs (2 soquetes * 6 núcleos @ 2,5 GHz)</span><span class="sxs-lookup"><span data-stu-id="b3ada-217">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="b3ada-218">18 GB</span><span class="sxs-lookup"><span data-stu-id="b3ada-218">18 GB</span></span> |<span data-ttu-id="b3ada-219">600 GB</span><span class="sxs-lookup"><span data-stu-id="b3ada-219">600 GB</span></span> |<span data-ttu-id="b3ada-220">500 GB a 1 TB</span><span class="sxs-lookup"><span data-stu-id="b3ada-220">500 GB to 1 TB</span></span> |<span data-ttu-id="b3ada-221">Replique entre 100 e 150 computadores.</span><span class="sxs-lookup"><span data-stu-id="b3ada-221">Replicate between 100-150 machines.</span></span> |
| <span data-ttu-id="b3ada-222">16 vCPUs (2 soquetes * 8 núcleos @ 2,5 GHz)</span><span class="sxs-lookup"><span data-stu-id="b3ada-222">16 vCPUs (2 sockets * 8 cores @ 2.5 GHz)</span></span> |<span data-ttu-id="b3ada-223">32 GB</span><span class="sxs-lookup"><span data-stu-id="b3ada-223">32 GB</span></span> |<span data-ttu-id="b3ada-224">1 TB</span><span class="sxs-lookup"><span data-stu-id="b3ada-224">1 TB</span></span> |<span data-ttu-id="b3ada-225">1 TB a 2 TB</span><span class="sxs-lookup"><span data-stu-id="b3ada-225">1 TB to 2 TB</span></span> |<span data-ttu-id="b3ada-226">Replique entre 150 e 200 computadores.</span><span class="sxs-lookup"><span data-stu-id="b3ada-226">Replicate between 150-200 machines.</span></span> |

  >[!TIP]
  <span data-ttu-id="b3ada-227">Se o diário rotatividade de dados excede 2 TB ou você deseja replicar mais de 200 máquinas virtuais, é recomendável implantar servidores de processo adicionais para equilibrar o tráfego de replicação.</span><span class="sxs-lookup"><span data-stu-id="b3ada-227">If your daily data churn exceeds 2 TB, or you plan to replicate more than 200 virtual machines, it is recommended to deploy additional process servers to load balance the replication traffic.</span></span> <span data-ttu-id="b3ada-228">Saiba mais sobre como implantar o processo de expansão servidores.</span><span class="sxs-lookup"><span data-stu-id="b3ada-228">Learn more about How to deploy Scale-out Process severs.</span></span>


## <a name="common-issues"></a><span data-ttu-id="b3ada-229">Problemas comuns</span><span class="sxs-lookup"><span data-stu-id="b3ada-229">Common issues</span></span>
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]
