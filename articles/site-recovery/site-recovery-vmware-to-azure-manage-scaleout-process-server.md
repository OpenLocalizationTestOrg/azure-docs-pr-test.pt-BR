---
title: " Gerenciar um servidor de processo de escalonamento horizontal no Azure Site Recovery | Microsoft Docs"
description: Este artigo descreve como configurar e gerenciar um servidor de processo de escalonamento horizontal no Azure Site Recovery.
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
ms.openlocfilehash: e5c01de19917235c34c035415df86291b9152bf0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-a-scale-out-process-server"></a><span data-ttu-id="fdce7-103">Gerenciar um servidor de processo de escalonamento horizontal</span><span class="sxs-lookup"><span data-stu-id="fdce7-103">Manage a Scale-out Process Server</span></span>

<span data-ttu-id="fdce7-104">Um servidor de processo de escalonamento horizontal atua como um coordenador para transferência de dados entre os serviços do Site Recovery e sua infraestrutura local.</span><span class="sxs-lookup"><span data-stu-id="fdce7-104">Scale-out Process Server acts as a coordinator for data transfer between the Site Recovery services and your on-premises infrastructure.</span></span> <span data-ttu-id="fdce7-105">Este artigo descreve como você pode definir, configurar e gerenciar um servidor de processo de escalonamento horizontal.</span><span class="sxs-lookup"><span data-stu-id="fdce7-105">This article describes how you can set up, configure, and manage a Scale-out Process Server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fdce7-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fdce7-106">Prerequisites</span></span>
<span data-ttu-id="fdce7-107">A seguir estão o hardware e software recomendados e a configuração de rede necessária para configurar um servidor de processo de escalonamento horizontal.</span><span class="sxs-lookup"><span data-stu-id="fdce7-107">The following are the recommended hardware, software, and network configuration required to set up a Scale-out Process Server.</span></span>

> [!NOTE]
> <span data-ttu-id="fdce7-108">[Planejamento de capacidade](site-recovery-capacity-planner.md) é uma etapa importante para assegurar que você implante o servidor de processo de escalonamento horizontal com uma configuração que se adeque aos seus requisitos de carga.</span><span class="sxs-lookup"><span data-stu-id="fdce7-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step to ensure that you deploy the Scale-out Process Server with a configuration that suites your load requirements.</span></span> <span data-ttu-id="fdce7-109">Leia mais sobre [Características de dimensionamento de um servidor de processo de escalonamento horizontal](#sizing-requirements-for-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="fdce7-109">Read more about [Scaling characteristics for a Scale-out Process Server](#sizing-requirements-for-a-configuration-server).</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-the-scale-out-process-server-software"></a><span data-ttu-id="fdce7-110">Baixar o software para servidores de processo de escalonamento horizontal</span><span class="sxs-lookup"><span data-stu-id="fdce7-110">Downloading the Scale-out Process Server software</span></span>
1. <span data-ttu-id="fdce7-111">Faça logon no Portal do Azure e navegue até seu Cofre dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="fdce7-111">Log on to the Azure portal and browse to your Recovery Services Vault.</span></span>
2. <span data-ttu-id="fdce7-112">Navegue até **Infraestrutura do Site Recovery** > **Servidores de Configuração** (sob Para VMware e Computadores Físicos).</span><span class="sxs-lookup"><span data-stu-id="fdce7-112">Browse to **Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span></span>
3. <span data-ttu-id="fdce7-113">Selecione o servidor de configuração para fazer drill down na página de detalhes do servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="fdce7-113">Select your configuration server to drill down into the configuration server's details page.</span></span>
4. <span data-ttu-id="fdce7-114">Clique no botão **+Servidor de Processo**.</span><span class="sxs-lookup"><span data-stu-id="fdce7-114">Click the **+ Process Server** button.</span></span>
5. <span data-ttu-id="fdce7-115">Na página **Adicionar servidor de processo**, selecione a opção **Implantar um servidor de processo de escalonamento horizontal local** na lista suspensa **Escolher onde você deseja implantar o servidor de processo**.</span><span class="sxs-lookup"><span data-stu-id="fdce7-115">In the **Add Process server** page, select **Deploy a Scale-out Process Server on-premises** option from the **Choose where you want to deploy your process server** drop-down.</span></span>

  ![Página Adicionar Servidores](./media/site-recovery-vmware-to-azure-manage-scaleout-process-server/add-process-server.png)
6. <span data-ttu-id="fdce7-117">Clique no link **Baixar a instalação unificada do Microsoft Azure Site Recovery** para baixar a versão mais recente da instalação do servidor de processo de escalonamento horizontal.</span><span class="sxs-lookup"><span data-stu-id="fdce7-117">Click the **Download the Microsoft Azure Site Recovery Unified Setup** link to download the latest version of the Scale-out Process Server installation.</span></span>

  > [!WARNING]
  <span data-ttu-id="fdce7-118">A versão do seu servidor de processo de escalonamento horizontal deve ser igual ou menor que a versão do servidor de configuração em execução no seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="fdce7-118">The version of your Scale-out Process Server should be equal to or lesser than the Configuration Server version running in your environment.</span></span> <span data-ttu-id="fdce7-119">Uma maneira simples de garantir a compatibilidade de versão é usar os mesmos bits do instalador usados recentemente para instalar/atualizar o servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="fdce7-119">A simple way to ensure version compatibility is to use the same installer bits that you recently used to install/update your Configuration Server.</span></span>

## <a name="installing-and-registering-a-scale-out-process-server-from-gui"></a><span data-ttu-id="fdce7-120">Instalar e registrar um servidor de processo de escalonamento horizontal por meio da GUI</span><span class="sxs-lookup"><span data-stu-id="fdce7-120">Installing and registering a Scale-out Process Server from GUI</span></span>
<span data-ttu-id="fdce7-121">Se for necessário escalar horizontalmente sua implantação para além de 200 computadores de origem ou uma taxa diária de rotatividade total acima de 2 TB, você precisará de servidores em processo adicionais para manipular o volume de tráfego.</span><span class="sxs-lookup"><span data-stu-id="fdce7-121">If you have to scale out your deployment beyond 200 source machines, or a total daily churn rate of more than 2 TB, you need additional process servers to handle the traffic volume.</span></span>

<span data-ttu-id="fdce7-122">Verifique as [recomendações de tamanho para servidores em processo](#size-recommendations-for-the-process-server) e siga estas instruções para configurar o servidor em processo.</span><span class="sxs-lookup"><span data-stu-id="fdce7-122">Check the [size recommendations for process servers](#size-recommendations-for-the-process-server), and then follow these instructions to set up the process server.</span></span> <span data-ttu-id="fdce7-123">Depois de configurar o servidor, você migrará os computadores de origem para usá-lo.</span><span class="sxs-lookup"><span data-stu-id="fdce7-123">After setting up the server, you migrate source machines to use it.</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-add-process-server.md)]


## <a name="installing-and-registering-a-scale-out-process-server-using-command-line"></a><span data-ttu-id="fdce7-124">Instalar e registrar um servidor de processo de escalonamento horizontal usando a linha de comando</span><span class="sxs-lookup"><span data-stu-id="fdce7-124">Installing and registering a Scale-out Process Server using command-line</span></span>

```
UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address to be used for data transfer] [/CSIP <IP address of CS to be registered with>] [/PassphraseFilePath <Passphrase file path>]
```

### <a name="sample-usage"></a><span data-ttu-id="fdce7-125">Amostra de uso</span><span class="sxs-lookup"><span data-stu-id="fdce7-125">Sample usage</span></span>
```
MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
cd C:\Temp\Extracted
UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "PS" /InstallLocation "D:\" /EnvType "VMWare" /CSIP "10.150.24.119" /PassphraseFilePath "C:\Users\Administrator\Desktop\Passphrase.txt" /DataTransferSecurePort 443
```

### <a name="scale-out-process-server-installer-command-line-arguments"></a><span data-ttu-id="fdce7-126">Argumentos de linha de comando do instalador do servidor de processo de escalonamento horizontal.</span><span class="sxs-lookup"><span data-stu-id="fdce7-126">Scale-out Process Server installer command-line arguments.</span></span>
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-proxy-settings-configuration-file"></a><span data-ttu-id="fdce7-127">Criar um arquivo de configuração de configurações de proxy</span><span class="sxs-lookup"><span data-stu-id="fdce7-127">Create a proxy settings configuration file</span></span>
<span data-ttu-id="fdce7-128">O parâmetro ProxySettingsFilePath utiliza um arquivo como entrada.</span><span class="sxs-lookup"><span data-stu-id="fdce7-128">ProxySettingsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="fdce7-129">Crie o arquivo usando o formato a seguir e passe-o como o parâmetro ProxySettingsFilePath de entrada.</span><span class="sxs-lookup"><span data-stu-id="fdce7-129">Create file using the following format and pass it as input ProxySettingsFilePath parameter.</span></span>
```
* [ProxySettings]
* ProxyAuthentication = "Yes/No"
* Proxy IP = "IP Address"
* ProxyPort = "Port"
* ProxyUserName="UserName"
* ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-scale-out-process-server"></a><span data-ttu-id="fdce7-130">Modificando configurações de proxy do servidor de processo de escalonamento horizontal</span><span class="sxs-lookup"><span data-stu-id="fdce7-130">Modifying proxy settings for Scale-out Process Server</span></span>
1. <span data-ttu-id="fdce7-131">Faça logon no servidor de processo de escalonamento horizontal.</span><span class="sxs-lookup"><span data-stu-id="fdce7-131">Login  into your Scale-out Process Server.</span></span>
2. <span data-ttu-id="fdce7-132">Abra uma janela de comando do PowerShell do Administrador.</span><span class="sxs-lookup"><span data-stu-id="fdce7-132">Open an Admin PowerShell command window.</span></span>
3. <span data-ttu-id="fdce7-133">Execute o comando a seguir</span><span class="sxs-lookup"><span data-stu-id="fdce7-133">Run the following command</span></span>
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber –ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```
4. <span data-ttu-id="fdce7-134">Em seguida, navegue até o diretório **%PROGRAMDATA%\ASR\Agent** e execute o comando a seguir</span><span class="sxs-lookup"><span data-stu-id="fdce7-134">Next browse to the directory **%PROGRAMDATA%\ASR\Agent** and run the following command</span></span>
  ```
  cmd
  cdpcli.exe --registermt

  net stop obengine

  net start obengine

  exit
  ```

## <a name="re-registering-a-scale-out-process-server"></a><span data-ttu-id="fdce7-135">Registrando novamente um servidor de processo de escalonamento horizontal</span><span class="sxs-lookup"><span data-stu-id="fdce7-135">Re-registering a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

* <span data-ttu-id="fdce7-136">Em seguida, abra um prompt de comando de Administrador.</span><span class="sxs-lookup"><span data-stu-id="fdce7-136">Next open an Admin command prompt.</span></span>
* <span data-ttu-id="fdce7-137">Navegue até o diretório **%PROGRAMDATA%\ASR\Agent** e execute o comando</span><span class="sxs-lookup"><span data-stu-id="fdce7-137">Browse to the directory **%PROGRAMDATA%\ASR\Agent** and run the command</span></span>

```
cdpcli.exe --registermt

net stop obengine

net start obengine
```

## <a name="upgrading-a-scale-out-process-server"></a><span data-ttu-id="fdce7-138">Atualizando um servidor de processo de escalonamento horizontal</span><span class="sxs-lookup"><span data-stu-id="fdce7-138">Upgrading a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-upgrade -process-server](../../includes/site-recovery-vmware-upgrade-process-server-internal.md)]

## <a name="decommissioning-a-scale-out-process-server"></a><span data-ttu-id="fdce7-139">Desativando um servidor de processo de escalonamento horizontal</span><span class="sxs-lookup"><span data-stu-id="fdce7-139">Decommissioning a Scale-out Process Server</span></span>
1. <span data-ttu-id="fdce7-140">Verifique se:</span><span class="sxs-lookup"><span data-stu-id="fdce7-140">Ensure that:</span></span>
  - <span data-ttu-id="fdce7-141">O estado de conexão do servidor de configuração é mostrado como **Conectado** no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="fdce7-141">Configuration Server's connection state shows as **Connected** in the Azure portal</span></span>
  - <span data-ttu-id="fdce7-142">O servidor de processo ainda pode se comunicar com o servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="fdce7-142">Process Server's is still able to communicate with the Configuration server.</span></span>
2. <span data-ttu-id="fdce7-143">Fazer logon no servidor de processo como administrador</span><span class="sxs-lookup"><span data-stu-id="fdce7-143">Log in to the process server as an administrator</span></span>
3. <span data-ttu-id="fdce7-144">Abrir o Painel de Controle > Programa > Desinstalar Programas</span><span class="sxs-lookup"><span data-stu-id="fdce7-144">Open up Control Panel > Program > Uninstall Programs</span></span>
4. <span data-ttu-id="fdce7-145">Desinstale os programas na sequência fornecida a seguir:</span><span class="sxs-lookup"><span data-stu-id="fdce7-145">Uninstall the programs in the sequence given following:</span></span>
  * <span data-ttu-id="fdce7-146">Servidor de processo/servidor de configuração do Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="fdce7-146">Microsoft Azure Site Recovery Configuration Server/Process Server</span></span>
  * <span data-ttu-id="fdce7-147">Dependências de servidor de configuração do Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="fdce7-147">Microsoft Azure Site Recovery Configuration Server Dependencies</span></span>
  * <span data-ttu-id="fdce7-148">Agente de Serviços dos Serviços de Recuperação do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="fdce7-148">Microsoft Azure Recovery Services Agent</span></span>

<span data-ttu-id="fdce7-149">Pode levar até 15 minutos para que a exclusão do servidor de processo reflita no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fdce7-149">It can take up-to 15 minutes for the Process Server deletion to reflect in the Azure portal.</span></span>

  > [!NOTE]
  <span data-ttu-id="fdce7-150">Se o servidor de processo não for capaz de se comunicar com o servidor de configuração (o estado de conexão no portal será Desconectado), você precisará seguir as etapas a seguir para limpá-lo do servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="fdce7-150">If the Process server is unable to communicate with the Configuration Server (Connection State in portal is Disconnected), then you need to follow the following steps to purge it from the Configuration Server.</span></span>

## <a name="unregistering-a-disconnected-scale-out-process-server-from-a-configuration-server"></a><span data-ttu-id="fdce7-151">Cancelando o registro de um servidor de processo de escalonamento horizontal desconectado de um servidor de configuração</span><span class="sxs-lookup"><span data-stu-id="fdce7-151">Unregistering a disconnected Scale-out Process server from a Configuration Server</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]

## <a name="sizing-requirements-for-a-scale-out-process-server"></a><span data-ttu-id="fdce7-152">Requisitos de dimensionamento para um servidor de processo de escalonamento horizontal</span><span class="sxs-lookup"><span data-stu-id="fdce7-152">Sizing requirements for a Scale-out Process Server</span></span>

| <span data-ttu-id="fdce7-153">**Servidor de processo adicional**</span><span class="sxs-lookup"><span data-stu-id="fdce7-153">**Additional process server**</span></span> | <span data-ttu-id="fdce7-154">**Tamanho do disco de cache**</span><span class="sxs-lookup"><span data-stu-id="fdce7-154">**Cache disk size**</span></span> | <span data-ttu-id="fdce7-155">**Taxa de alteração de dados**</span><span class="sxs-lookup"><span data-stu-id="fdce7-155">**Data change rate**</span></span> | <span data-ttu-id="fdce7-156">**Computadores protegidos**</span><span class="sxs-lookup"><span data-stu-id="fdce7-156">**Protected machines**</span></span> |
| --- | --- | --- | --- |
|<span data-ttu-id="fdce7-157">4 vCPUs (2 soquetes * 2 núcleos @ 2,5 GHz), 8 GB de memória</span><span class="sxs-lookup"><span data-stu-id="fdce7-157">4 vCPUs (2 sockets * 2 cores @ 2.5 GHz), 8-GB memory</span></span> |<span data-ttu-id="fdce7-158">300 GB</span><span class="sxs-lookup"><span data-stu-id="fdce7-158">300 GB</span></span> |<span data-ttu-id="fdce7-159">250 GB ou menos</span><span class="sxs-lookup"><span data-stu-id="fdce7-159">250 GB or less</span></span> |<span data-ttu-id="fdce7-160">Replique 85 computadores ou menos.</span><span class="sxs-lookup"><span data-stu-id="fdce7-160">Replicate 85 or less machines.</span></span> |
|<span data-ttu-id="fdce7-161">8 vCPUs (2 soquetes * 4 núcleos @ 2,5 GHz), 12 GB de memória</span><span class="sxs-lookup"><span data-stu-id="fdce7-161">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz), 12-GB memory</span></span> |<span data-ttu-id="fdce7-162">600 GB</span><span class="sxs-lookup"><span data-stu-id="fdce7-162">600 GB</span></span> |<span data-ttu-id="fdce7-163">250 GB a 1 TB</span><span class="sxs-lookup"><span data-stu-id="fdce7-163">250 GB to 1 TB</span></span> |<span data-ttu-id="fdce7-164">Replique entre 85 e 150 computadores.</span><span class="sxs-lookup"><span data-stu-id="fdce7-164">Replicate between 85-150 machines.</span></span> |
|<span data-ttu-id="fdce7-165">12 vCPUs (2 soquetes * 6 núcleos @ 2,5 GHz), 24 GB de memória</span><span class="sxs-lookup"><span data-stu-id="fdce7-165">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz) 24-GB memory</span></span> |<span data-ttu-id="fdce7-166">1 TB</span><span class="sxs-lookup"><span data-stu-id="fdce7-166">1 TB</span></span> |<span data-ttu-id="fdce7-167">1 TB a 2 TB</span><span class="sxs-lookup"><span data-stu-id="fdce7-167">1 TB to 2 TB</span></span> |<span data-ttu-id="fdce7-168">Replique entre 150 e 225 computadores.</span><span class="sxs-lookup"><span data-stu-id="fdce7-168">Replicate between 150-225 machines.</span></span> |
