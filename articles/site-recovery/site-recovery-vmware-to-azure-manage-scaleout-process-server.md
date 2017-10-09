---
title: " Gerenciar um servidor de processo de escalonamento horizontal no Azure Site Recovery | Microsoft Docs"
description: "Este artigo descreve como tooset e gerenciar um servidor de processo de expansão no Azure Site Recovery."
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
ms.openlocfilehash: 3d72f9c2c7014a4ff2fa2af168aa55ad1452eae5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-scale-out-process-server"></a><span data-ttu-id="2afcf-103">Gerenciar um servidor de processo de escalonamento horizontal</span><span class="sxs-lookup"><span data-stu-id="2afcf-103">Manage a Scale-out Process Server</span></span>

<span data-ttu-id="2afcf-104">Servidor de processo de expansão atua como um coordenador para transferir dados entre os serviços de recuperação de Site hello e sua infraestrutura local.</span><span class="sxs-lookup"><span data-stu-id="2afcf-104">Scale-out Process Server acts as a coordinator for data transfer between hello Site Recovery services and your on-premises infrastructure.</span></span> <span data-ttu-id="2afcf-105">Este artigo descreve como você pode definir, configurar e gerenciar um servidor de processo de escalonamento horizontal.</span><span class="sxs-lookup"><span data-stu-id="2afcf-105">This article describes how you can set up, configure, and manage a Scale-out Process Server.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2afcf-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2afcf-106">Prerequisites</span></span>
<span data-ttu-id="2afcf-107">Olá seguem Olá recomendados de hardware, software e rede configuração necessária tooset um servidor de processo de expansão.</span><span class="sxs-lookup"><span data-stu-id="2afcf-107">hello following are hello recommended hardware, software, and network configuration required tooset up a Scale-out Process Server.</span></span>

> [!NOTE]
> <span data-ttu-id="2afcf-108">[Planejamento de capacidade](site-recovery-capacity-planner.md) é um tooensure etapa importante que você implante Olá expansão de servidor de processo com uma configuração que conjuntos de seus requisitos de carga.</span><span class="sxs-lookup"><span data-stu-id="2afcf-108">[Capacity planning](site-recovery-capacity-planner.md) is an important step tooensure that you deploy hello Scale-out Process Server with a configuration that suites your load requirements.</span></span> <span data-ttu-id="2afcf-109">Leia mais sobre [Características de dimensionamento de um servidor de processo de escalonamento horizontal](#sizing-requirements-for-a-configuration-server).</span><span class="sxs-lookup"><span data-stu-id="2afcf-109">Read more about [Scaling characteristics for a Scale-out Process Server](#sizing-requirements-for-a-configuration-server).</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

## <a name="downloading-hello-scale-out-process-server-software"></a><span data-ttu-id="2afcf-110">Baixar o software de servidor de processo de expansão Olá</span><span class="sxs-lookup"><span data-stu-id="2afcf-110">Downloading hello Scale-out Process Server software</span></span>
1. <span data-ttu-id="2afcf-111">Faça logon no toohello tooyour Azure portal e procurar o Cofre de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="2afcf-111">Log on toohello Azure portal and browse tooyour Recovery Services Vault.</span></span>
2. <span data-ttu-id="2afcf-112">Procurar muito**infra-estrutura de recuperação de Site** > **servidores de configuração** (no VMware para o & máquinas físicas).</span><span class="sxs-lookup"><span data-stu-id="2afcf-112">Browse too**Site Recovery Infrastructure** > **Configuration Servers** (under For VMware & Physical Machines).</span></span>
3. <span data-ttu-id="2afcf-113">Selecione seu toodrill do servidor de configuração para baixo na página de detalhes do servidor de configuração hello.</span><span class="sxs-lookup"><span data-stu-id="2afcf-113">Select your configuration server toodrill down into hello configuration server's details page.</span></span>
4. <span data-ttu-id="2afcf-114">Clique em Olá **+ servidor de processo** botão.</span><span class="sxs-lookup"><span data-stu-id="2afcf-114">Click hello **+ Process Server** button.</span></span>
5. <span data-ttu-id="2afcf-115">Em Olá **do servidor em processo de adicionar** página, selecione **local do servidor de processo de implantar uma expansão** opção de saudação **escolha onde você deseja toodeploy seu servidor de processo** lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="2afcf-115">In hello **Add Process server** page, select **Deploy a Scale-out Process Server on-premises** option from hello **Choose where you want toodeploy your process server** drop-down.</span></span>

  ![Página Adicionar Servidores](./media/site-recovery-vmware-to-azure-manage-scaleout-process-server/add-process-server.png)
6. <span data-ttu-id="2afcf-117">Clique em Olá **Download Olá instalação unificado do Microsoft Azure Site Recovery** versão mais recente do link toodownload Olá da instalação do servidor de processo Olá expansão.</span><span class="sxs-lookup"><span data-stu-id="2afcf-117">Click hello **Download hello Microsoft Azure Site Recovery Unified Setup** link toodownload hello latest version of hello Scale-out Process Server installation.</span></span>

  > [!WARNING]
  <span data-ttu-id="2afcf-118">Olá versão do seu servidor de processo de expansão deve ser igual tooor menor que a versão de servidor de configuração de saudação em execução no seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="2afcf-118">hello version of your Scale-out Process Server should be equal tooor lesser than hello Configuration Server version running in your environment.</span></span> <span data-ttu-id="2afcf-119">Compatibilidade de versão de tooensure uma maneira simples é toouse Olá mesmo bits de instalador que você usou recentemente tooinstall/atualizar seu servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="2afcf-119">A simple way tooensure version compatibility is toouse hello same installer bits that you recently used tooinstall/update your Configuration Server.</span></span>

## <a name="installing-and-registering-a-scale-out-process-server-from-gui"></a><span data-ttu-id="2afcf-120">Instalar e registrar um servidor de processo de escalonamento horizontal por meio da GUI</span><span class="sxs-lookup"><span data-stu-id="2afcf-120">Installing and registering a Scale-out Process Server from GUI</span></span>
<span data-ttu-id="2afcf-121">Se você tiver tooscale sua implantação, além de 200 máquinas de origem, ou um total diário variação taxa de mais de 2 TB, você precisa o volume de tráfego de saudação do processo adicional servidores toohandle.</span><span class="sxs-lookup"><span data-stu-id="2afcf-121">If you have tooscale out your deployment beyond 200 source machines, or a total daily churn rate of more than 2 TB, you need additional process servers toohandle hello traffic volume.</span></span>

<span data-ttu-id="2afcf-122">Verificar Olá [tamanho recomendações para servidores de processo](#size-recommendations-for-the-process-server)e, em seguida, siga tooset essas instruções backup do servidor de processo hello.</span><span class="sxs-lookup"><span data-stu-id="2afcf-122">Check hello [size recommendations for process servers](#size-recommendations-for-the-process-server), and then follow these instructions tooset up hello process server.</span></span> <span data-ttu-id="2afcf-123">Depois de configurar o servidor de saudação, migrar fonte máquinas toouse-lo.</span><span class="sxs-lookup"><span data-stu-id="2afcf-123">After setting up hello server, you migrate source machines toouse it.</span></span>

[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-add-process-server.md)]


## <a name="installing-and-registering-a-scale-out-process-server-using-command-line"></a><span data-ttu-id="2afcf-124">Instalar e registrar um servidor de processo de escalonamento horizontal usando a linha de comando</span><span class="sxs-lookup"><span data-stu-id="2afcf-124">Installing and registering a Scale-out Process Server using command-line</span></span>

```
UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]
```

### <a name="sample-usage"></a><span data-ttu-id="2afcf-125">Amostra de uso</span><span class="sxs-lookup"><span data-stu-id="2afcf-125">Sample usage</span></span>
```
MicrosoftAzureSiteRecoveryUnifiedSetup.exe /q /xC:\Temp\Extracted
cd C:\Temp\Extracted
UNIFIEDSETUP.EXE /AcceptThirdpartyEULA /servermode "PS" /InstallLocation "D:\" /EnvType "VMWare" /CSIP "10.150.24.119" /PassphraseFilePath "C:\Users\Administrator\Desktop\Passphrase.txt" /DataTransferSecurePort 443
```

### <a name="scale-out-process-server-installer-command-line-arguments"></a><span data-ttu-id="2afcf-126">Argumentos de linha de comando do instalador do servidor de processo de escalonamento horizontal.</span><span class="sxs-lookup"><span data-stu-id="2afcf-126">Scale-out Process Server installer command-line arguments.</span></span>
[!INCLUDE [site-recovery-unified-setup-parameters](../../includes/site-recovery-unified-installer-command-parameters.md)]


### <a name="create-a-proxy-settings-configuration-file"></a><span data-ttu-id="2afcf-127">Criar um arquivo de configuração de configurações de proxy</span><span class="sxs-lookup"><span data-stu-id="2afcf-127">Create a proxy settings configuration file</span></span>
<span data-ttu-id="2afcf-128">O parâmetro ProxySettingsFilePath utiliza um arquivo como entrada.</span><span class="sxs-lookup"><span data-stu-id="2afcf-128">ProxySettingsFilePath parameter takes a file as input.</span></span> <span data-ttu-id="2afcf-129">Crie o arquivo usando Olá seguinte formato e passá-lo como parâmetro de entrada ProxySettingsFilePath.</span><span class="sxs-lookup"><span data-stu-id="2afcf-129">Create file using hello following format and pass it as input ProxySettingsFilePath parameter.</span></span>
```
* [ProxySettings]
* ProxyAuthentication = "Yes/No"
* Proxy IP = "IP Address"
* ProxyPort = "Port"
* ProxyUserName="UserName"
* ProxyPassword="Password"
```
## <a name="modifying-proxy-settings-for-scale-out-process-server"></a><span data-ttu-id="2afcf-130">Modificando configurações de proxy do servidor de processo de escalonamento horizontal</span><span class="sxs-lookup"><span data-stu-id="2afcf-130">Modifying proxy settings for Scale-out Process Server</span></span>
1. <span data-ttu-id="2afcf-131">Faça logon no servidor de processo de escalonamento horizontal.</span><span class="sxs-lookup"><span data-stu-id="2afcf-131">Login  into your Scale-out Process Server.</span></span>
2. <span data-ttu-id="2afcf-132">Abra uma janela de comando do PowerShell do Administrador.</span><span class="sxs-lookup"><span data-stu-id="2afcf-132">Open an Admin PowerShell command window.</span></span>
3. <span data-ttu-id="2afcf-133">Olá executar comando a seguir</span><span class="sxs-lookup"><span data-stu-id="2afcf-133">Run hello following command</span></span>
  ```
  $pwd = ConvertTo-SecureString -String MyProxyUserPassword
  Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumber –ProxyUserName domain\username -ProxyPassword $pwd
  net stop obengine
  net start obengine
  ```
4. <span data-ttu-id="2afcf-134">Procurar próximo diretório toohello **%PROGRAMDATA%\ASR\Agent** e o comando a seguir Olá execução</span><span class="sxs-lookup"><span data-stu-id="2afcf-134">Next browse toohello directory **%PROGRAMDATA%\ASR\Agent** and run hello following command</span></span>
  ```
  cmd
  cdpcli.exe --registermt

  net stop obengine

  net start obengine

  exit
  ```

## <a name="re-registering-a-scale-out-process-server"></a><span data-ttu-id="2afcf-135">Registrando novamente um servidor de processo de escalonamento horizontal</span><span class="sxs-lookup"><span data-stu-id="2afcf-135">Re-registering a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-register-process-server](../../includes/site-recovery-vmware-register-process-server.md)]

* <span data-ttu-id="2afcf-136">Em seguida, abra um prompt de comando de Administrador.</span><span class="sxs-lookup"><span data-stu-id="2afcf-136">Next open an Admin command prompt.</span></span>
* <span data-ttu-id="2afcf-137">Procurar diretório de toohello **%PROGRAMDATA%\ASR\Agent** e execute o comando Olá</span><span class="sxs-lookup"><span data-stu-id="2afcf-137">Browse toohello directory **%PROGRAMDATA%\ASR\Agent** and run hello command</span></span>

```
cdpcli.exe --registermt

net stop obengine

net start obengine
```

## <a name="upgrading-a-scale-out-process-server"></a><span data-ttu-id="2afcf-138">Atualizando um servidor de processo de escalonamento horizontal</span><span class="sxs-lookup"><span data-stu-id="2afcf-138">Upgrading a Scale-out Process Server</span></span>
[!INCLUDE [site-recovery-vmware-upgrade -process-server](../../includes/site-recovery-vmware-upgrade-process-server-internal.md)]

## <a name="decommissioning-a-scale-out-process-server"></a><span data-ttu-id="2afcf-139">Desativando um servidor de processo de escalonamento horizontal</span><span class="sxs-lookup"><span data-stu-id="2afcf-139">Decommissioning a Scale-out Process Server</span></span>
1. <span data-ttu-id="2afcf-140">Verifique se:</span><span class="sxs-lookup"><span data-stu-id="2afcf-140">Ensure that:</span></span>
  - <span data-ttu-id="2afcf-141">Mostra o estado de conexão do servidor de configuração como **conectado** em Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2afcf-141">Configuration Server's connection state shows as **Connected** in hello Azure portal</span></span>
  - <span data-ttu-id="2afcf-142">Servidor de processo é ainda poderá toocommunicate com o servidor de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="2afcf-142">Process Server's is still able toocommunicate with hello Configuration server.</span></span>
2. <span data-ttu-id="2afcf-143">Faça logon no servidor de processo toohello como um administrador</span><span class="sxs-lookup"><span data-stu-id="2afcf-143">Log in toohello process server as an administrator</span></span>
3. <span data-ttu-id="2afcf-144">Abrir o Painel de Controle > Programa > Desinstalar Programas</span><span class="sxs-lookup"><span data-stu-id="2afcf-144">Open up Control Panel > Program > Uninstall Programs</span></span>
4. <span data-ttu-id="2afcf-145">Desinstale programas Olá na sequência de saudação fornecida a seguir:</span><span class="sxs-lookup"><span data-stu-id="2afcf-145">Uninstall hello programs in hello sequence given following:</span></span>
  * <span data-ttu-id="2afcf-146">Servidor de processo/servidor de configuração do Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="2afcf-146">Microsoft Azure Site Recovery Configuration Server/Process Server</span></span>
  * <span data-ttu-id="2afcf-147">Dependências de servidor de configuração do Microsoft Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="2afcf-147">Microsoft Azure Site Recovery Configuration Server Dependencies</span></span>
  * <span data-ttu-id="2afcf-148">Agente de Serviços dos Serviços de Recuperação do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="2afcf-148">Microsoft Azure Recovery Services Agent</span></span>

<span data-ttu-id="2afcf-149">Pode levar até too15 minutos de saudação do servidor em processo exclusão tooreflect no portal do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="2afcf-149">It can take up-too15 minutes for hello Process Server deletion tooreflect in hello Azure portal.</span></span>

  > [!NOTE]
  <span data-ttu-id="2afcf-150">Se o servidor de processo de saudação é toocommunicate não é possível com hello configuração de servidor (estado de Conexão no portal está desconectado), em seguida, você precisa toofollow Olá seguindo as etapas toopurge-lo da saudação servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="2afcf-150">If hello Process server is unable toocommunicate with hello Configuration Server (Connection State in portal is Disconnected), then you need toofollow hello following steps toopurge it from hello Configuration Server.</span></span>

## <a name="unregistering-a-disconnected-scale-out-process-server-from-a-configuration-server"></a><span data-ttu-id="2afcf-151">Cancelando o registro de um servidor de processo de escalonamento horizontal desconectado de um servidor de configuração</span><span class="sxs-lookup"><span data-stu-id="2afcf-151">Unregistering a disconnected Scale-out Process server from a Configuration Server</span></span>

[!INCLUDE [site-recovery-vmware-upgrade-process-server](../../includes/site-recovery-vmware-unregister-process-server.md)]

## <a name="sizing-requirements-for-a-scale-out-process-server"></a><span data-ttu-id="2afcf-152">Requisitos de dimensionamento para um servidor de processo de escalonamento horizontal</span><span class="sxs-lookup"><span data-stu-id="2afcf-152">Sizing requirements for a Scale-out Process Server</span></span>

| <span data-ttu-id="2afcf-153">**Servidor de processo adicional**</span><span class="sxs-lookup"><span data-stu-id="2afcf-153">**Additional process server**</span></span> | <span data-ttu-id="2afcf-154">**Tamanho do disco de cache**</span><span class="sxs-lookup"><span data-stu-id="2afcf-154">**Cache disk size**</span></span> | <span data-ttu-id="2afcf-155">**Taxa de alteração de dados**</span><span class="sxs-lookup"><span data-stu-id="2afcf-155">**Data change rate**</span></span> | <span data-ttu-id="2afcf-156">**Computadores protegidos**</span><span class="sxs-lookup"><span data-stu-id="2afcf-156">**Protected machines**</span></span> |
| --- | --- | --- | --- |
|<span data-ttu-id="2afcf-157">4 vCPUs (2 soquetes * 2 núcleos @ 2,5 GHz), 8 GB de memória</span><span class="sxs-lookup"><span data-stu-id="2afcf-157">4 vCPUs (2 sockets * 2 cores @ 2.5 GHz), 8-GB memory</span></span> |<span data-ttu-id="2afcf-158">300 GB</span><span class="sxs-lookup"><span data-stu-id="2afcf-158">300 GB</span></span> |<span data-ttu-id="2afcf-159">250 GB ou menos</span><span class="sxs-lookup"><span data-stu-id="2afcf-159">250 GB or less</span></span> |<span data-ttu-id="2afcf-160">Replique 85 computadores ou menos.</span><span class="sxs-lookup"><span data-stu-id="2afcf-160">Replicate 85 or less machines.</span></span> |
|<span data-ttu-id="2afcf-161">8 vCPUs (2 soquetes * 4 núcleos @ 2,5 GHz), 12 GB de memória</span><span class="sxs-lookup"><span data-stu-id="2afcf-161">8 vCPUs (2 sockets * 4 cores @ 2.5 GHz), 12-GB memory</span></span> |<span data-ttu-id="2afcf-162">600 GB</span><span class="sxs-lookup"><span data-stu-id="2afcf-162">600 GB</span></span> |<span data-ttu-id="2afcf-163">250 GB too1 TB</span><span class="sxs-lookup"><span data-stu-id="2afcf-163">250 GB too1 TB</span></span> |<span data-ttu-id="2afcf-164">Replique entre 85 e 150 computadores.</span><span class="sxs-lookup"><span data-stu-id="2afcf-164">Replicate between 85-150 machines.</span></span> |
|<span data-ttu-id="2afcf-165">12 vCPUs (2 soquetes * 6 núcleos @ 2,5 GHz), 24 GB de memória</span><span class="sxs-lookup"><span data-stu-id="2afcf-165">12 vCPUs (2 sockets * 6 cores @ 2.5 GHz) 24-GB memory</span></span> |<span data-ttu-id="2afcf-166">1 TB</span><span class="sxs-lookup"><span data-stu-id="2afcf-166">1 TB</span></span> |<span data-ttu-id="2afcf-167">1 TB too2 TB</span><span class="sxs-lookup"><span data-stu-id="2afcf-167">1 TB too2 TB</span></span> |<span data-ttu-id="2afcf-168">Replique entre 150 e 225 computadores.</span><span class="sxs-lookup"><span data-stu-id="2afcf-168">Replicate between 150-225 machines.</span></span> |
