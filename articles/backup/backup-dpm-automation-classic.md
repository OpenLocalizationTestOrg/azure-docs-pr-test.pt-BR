---
title: 'O Backup do Azure: Use o PowerShell tooback cargas de trabalho do DPM | Microsoft Docs'
description: Saiba como toodeploy e gerenciar o Backup do Azure para o Data Protection Manager (DPM) usando o PowerShell
services: backup
documentationcenter: 
author: Nkolli1
manager: shreeshd
editor: 
ms.assetid: bcbcef79-9d33-4e84-a558-9866614f2cae
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: nkolli;trinadhk;anuragm;markgal
ms.openlocfilehash: 48ebe6b520857836e89749ffb6fe83d1f14c5597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="d9747-103">Implantar e gerenciar o backup tooAzure para servidores do Data Protection Manager (DPM) usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9747-103">Deploy and manage backup tooAzure for Data Protection Manager (DPM) servers using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d9747-104">ARM</span><span class="sxs-lookup"><span data-stu-id="d9747-104">ARM</span></span>](backup-dpm-automation.md)
> * [<span data-ttu-id="d9747-105">Clássico</span><span class="sxs-lookup"><span data-stu-id="d9747-105">Classic</span></span>](backup-dpm-automation-classic.md)
>
>

<span data-ttu-id="d9747-106">Este artigo explica como toouse PowerShell tooback backup e recuperar dados do DPM de um cofre de backup.</span><span class="sxs-lookup"><span data-stu-id="d9747-106">This article explains how toouse PowerShell tooback up and recover DPM data from a backup vault.</span></span> <span data-ttu-id="d9747-107">A Microsoft recomenda usar cofres de Serviços de Recuperação para todas as implantações novas.</span><span class="sxs-lookup"><span data-stu-id="d9747-107">Microsoft recommends using Recovery Services vaults for all new deployments.</span></span> <span data-ttu-id="d9747-108">Se você for um novo usuário de Backup do Azure, use o artigo hello, [implantar e gerenciar tooAzure de dados do Data Protection Manager usando o PowerShell](backup-dpm-automation.md), de modo que você armazena seus dados em um cofre de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="d9747-108">If you are a new Azure Backup user, use hello article, [Deploy and manage Data Protection Manager data tooAzure using PowerShell](backup-dpm-automation.md), so you store your data in a Recovery Services vault.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d9747-109">Agora você pode atualizar seu cofres dos serviços de tooRecovery de cofres de Backup.</span><span class="sxs-lookup"><span data-stu-id="d9747-109">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="d9747-110">Para obter detalhes, consulte o artigo Olá [atualizar um tooa de Cofre de Backup Cofre de serviços de recuperação](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="d9747-110">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="d9747-111">A Microsoft incentiva tooupgrade cofres de serviços tooRecovery os cofres de Backup.</span><span class="sxs-lookup"><span data-stu-id="d9747-111">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="d9747-112">Após 15 de outubro de 2017, você não pode usar o PowerShell toocreate os cofres de Backup.</span><span class="sxs-lookup"><span data-stu-id="d9747-112">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="d9747-113">**Em 1º de novembro de 2017**:</span><span class="sxs-lookup"><span data-stu-id="d9747-113">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="d9747-114">Todos os cofres de Backup restantes serão automaticamente atualizados tooRecovery cofres de serviços.</span><span class="sxs-lookup"><span data-stu-id="d9747-114">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="d9747-115">Você não será capaz de tooaccess os dados de backup no portal clássico do hello.</span><span class="sxs-lookup"><span data-stu-id="d9747-115">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="d9747-116">Em vez disso, use Olá tooaccess portal do Azure os dados de backup em cofres de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="d9747-116">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="setting-up-hello-powershell-environment"></a><span data-ttu-id="d9747-117">Configurando o ambiente do PowerShell Olá</span><span class="sxs-lookup"><span data-stu-id="d9747-117">Setting up hello PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="d9747-118">Antes de usar PowerShell toomanage backups tooAzure Data Protection Manager, você precisará toohave Olá direita ambiente PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d9747-118">Before you can use PowerShell toomanage backups from Data Protection Manager tooAzure, you will need toohave hello right environment in PowerShell.</span></span> <span data-ttu-id="d9747-119">No início de saudação da sessão do PowerShell Olá, certifique-se de que você execute Olá módulos corretos do comando tooimport Olá a seguir e permitem que você toocorrectly Referência Olá DPM cmdlets:</span><span class="sxs-lookup"><span data-stu-id="d9747-119">At hello start of hello PowerShell session, ensure that you run hello following command tooimport hello right modules and allow you toocorrectly reference hello DPM cmdlets:</span></span>

```
PS C:> & "C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin\DpmCliInitScript.ps1"

Welcome toohello DPM Management Shell!

Full list of cmdlets: Get-Command
Only DPM cmdlets: Get-DPMCommand
Get general help: help
Get help for a cmdlet: help <cmdlet-name> or <cmdlet-name> -?
Get definition of a cmdlet: Get-Command <cmdlet-name> -Syntax
Sample DPM scripts: Get-DPMSampleScript
```

## <a name="setup-and-registration"></a><span data-ttu-id="d9747-120">Configuração e registro</span><span class="sxs-lookup"><span data-stu-id="d9747-120">Setup and Registration</span></span>
<span data-ttu-id="d9747-121">toobegin:</span><span class="sxs-lookup"><span data-stu-id="d9747-121">toobegin:</span></span>

1. <span data-ttu-id="d9747-122">[Baixe o PowerShell mais recente](https://github.com/Azure/azure-powershell/releases) (a versão mínima exigida é: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="d9747-122">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>
2. <span data-ttu-id="d9747-123">Habilitar cmdlets do Backup do Azure Olá alternando muito*AzureResourceManager* modo usando Olá **Switch-AzureMode** commandlet:</span><span class="sxs-lookup"><span data-stu-id="d9747-123">Enable hello Azure Backup commandlets by switching too*AzureResourceManager* mode by using hello **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="d9747-124">Olá tarefas de registro e configuração a seguir podem ser automatizadas com o PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d9747-124">hello following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="d9747-125">Criar um cofre de backup</span><span class="sxs-lookup"><span data-stu-id="d9747-125">Create a backup vault</span></span>
* <span data-ttu-id="d9747-126">Instalando o agente de Backup do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="d9747-126">Installing hello Azure Backup agent</span></span>
* <span data-ttu-id="d9747-127">Registrando Olá serviço Backup do Azure</span><span class="sxs-lookup"><span data-stu-id="d9747-127">Registering with hello Azure Backup service</span></span>
* <span data-ttu-id="d9747-128">Configurações de rede</span><span class="sxs-lookup"><span data-stu-id="d9747-128">Networking settings</span></span>
* <span data-ttu-id="d9747-129">Configurações de criptografia</span><span class="sxs-lookup"><span data-stu-id="d9747-129">Encryption settings</span></span>

### <a name="create-a-backup-vault"></a><span data-ttu-id="d9747-130">Criar um cofre de backup</span><span class="sxs-lookup"><span data-stu-id="d9747-130">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="d9747-131">Para clientes que usam o Backup do Azure para Olá primeira vez, você precisa tooregister hello Azure Backup provedor toobe usado com sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="d9747-131">For customers using Azure Backup for hello first time, you need tooregister hello Azure Backup provider toobe used with your subscription.</span></span> <span data-ttu-id="d9747-132">Isso pode ser feito executando o comando a seguir de saudação: Register-AzureProvider - ProviderNamespace "Microsoft.Backup"</span><span class="sxs-lookup"><span data-stu-id="d9747-132">This can be done by running hello following command: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="d9747-133">Você pode criar um novo cofre de backup usando Olá **AzureRMBackupVault novo** commandlet.</span><span class="sxs-lookup"><span data-stu-id="d9747-133">You can create a new backup vault using hello **New-AzureRMBackupVault** commandlet.</span></span> <span data-ttu-id="d9747-134">Cofre de backup Olá é um recurso do ARM, portanto, você precisa tooplace-lo em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d9747-134">hello backup vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="d9747-135">Em um console do Azure PowerShell com privilégios elevados, execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="d9747-135">In an elevated Azure PowerShell console, run hello following commands:</span></span>

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GRS
```

<span data-ttu-id="d9747-136">Você pode obter uma lista de todos os cofres de backup de saudação em uma determinada assinatura usando Olá **AzureRMBackupVault Get** commandlet.</span><span class="sxs-lookup"><span data-stu-id="d9747-136">You can get a list of all hello backup vaults in a given subscription using hello **Get-AzureRMBackupVault** commandlet.</span></span>

### <a name="installing-hello-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="d9747-137">Instalando o agente de Backup do Azure Olá em um servidor DPM</span><span class="sxs-lookup"><span data-stu-id="d9747-137">Installing hello Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="d9747-138">Antes de instalar o agente de Backup do Azure Olá, você precisará instalador de saudação toohave baixado e presente no saudação do Windows Server.</span><span class="sxs-lookup"><span data-stu-id="d9747-138">Before you install hello Azure Backup agent, you need toohave hello installer downloaded and present on hello Windows Server.</span></span> <span data-ttu-id="d9747-139">Você pode obter a versão mais recente de saudação do instalador de saudação de saudação [Microsoft Download Center](http://aka.ms/azurebackup_agent) ou da página de painel do Cofre de saudação backup.</span><span class="sxs-lookup"><span data-stu-id="d9747-139">You can get hello latest version of hello installer from hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from hello backup vault's Dashboard page.</span></span> <span data-ttu-id="d9747-140">Salvar instalador Olá tooan local facilmente acessível, como * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="d9747-140">Save hello installer tooan easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="d9747-141">tooinstall Olá execução do agente, Olá seguinte comando em um console do PowerShell com privilégios elevados **no servidor DPM Olá**:</span><span class="sxs-lookup"><span data-stu-id="d9747-141">tooinstall hello agent, run hello following command in an elevated PowerShell console **on hello DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="d9747-142">Isso instala o agente de saudação com todas as opções padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="d9747-142">This installs hello agent with all hello default options.</span></span> <span data-ttu-id="d9747-143">instalação de saudação leva alguns minutos no plano de fundo de saudação.</span><span class="sxs-lookup"><span data-stu-id="d9747-143">hello installation takes a few minutes in hello background.</span></span> <span data-ttu-id="d9747-144">Se você não especificar Olá */nu* Olá opção **Windows Update** janela será aberta no final de saudação do hello instalação toocheck para todas as atualizações.</span><span class="sxs-lookup"><span data-stu-id="d9747-144">If you do not specify hello */nu* option hello **Windows Update** window will open at hello end of hello installation toocheck for any updates.</span></span>

<span data-ttu-id="d9747-145">agente Hello serão mostrados na lista de saudação de programas instalados.</span><span class="sxs-lookup"><span data-stu-id="d9747-145">hello agent will show in hello list of installed programs.</span></span> <span data-ttu-id="d9747-146">lista de saudação toosee de instalado programas, consulte muito**painel de controle** > **programas** > **programas e recursos**.</span><span class="sxs-lookup"><span data-stu-id="d9747-146">toosee hello list of installed programs, go too**Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agente instalado](./media/backup-dpm-automation/installed-agent-listing.png)

#### <a name="installation-options"></a><span data-ttu-id="d9747-148">Opções de instalação</span><span class="sxs-lookup"><span data-stu-id="d9747-148">Installation options</span></span>
<span data-ttu-id="d9747-149">toosee todas as opções disponíveis por meio de Olá Olá de linha de comando, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="d9747-149">toosee all hello options available via hello command-line, use hello following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="d9747-150">Olá as opções disponíveis incluem:</span><span class="sxs-lookup"><span data-stu-id="d9747-150">hello available options include:</span></span>

| <span data-ttu-id="d9747-151">Opção</span><span class="sxs-lookup"><span data-stu-id="d9747-151">Option</span></span> | <span data-ttu-id="d9747-152">Detalhes</span><span class="sxs-lookup"><span data-stu-id="d9747-152">Details</span></span> | <span data-ttu-id="d9747-153">Padrão</span><span class="sxs-lookup"><span data-stu-id="d9747-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d9747-154">/q</span><span class="sxs-lookup"><span data-stu-id="d9747-154">/q</span></span> |<span data-ttu-id="d9747-155">Instalação silenciosa</span><span class="sxs-lookup"><span data-stu-id="d9747-155">Quiet installation</span></span> |- |
| <span data-ttu-id="d9747-156">/p:"local"</span><span class="sxs-lookup"><span data-stu-id="d9747-156">/p:"location"</span></span> |<span data-ttu-id="d9747-157">Pasta de instalação de toohello de caminho para o agente de Backup do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d9747-157">Path toohello installation folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="d9747-158">C:\Arquivos de Programas\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="d9747-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="d9747-159">/s:"local"</span><span class="sxs-lookup"><span data-stu-id="d9747-159">/s:"location"</span></span> |<span data-ttu-id="d9747-160">Pasta de cache de toohello de caminho para o agente de Backup do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d9747-160">Path toohello cache folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="d9747-161">C:\Arquivos de Programas\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="d9747-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="d9747-162">/m</span><span class="sxs-lookup"><span data-stu-id="d9747-162">/m</span></span> |<span data-ttu-id="d9747-163">Aceitar tooMicrosoft atualização</span><span class="sxs-lookup"><span data-stu-id="d9747-163">Opt-in tooMicrosoft Update</span></span> |- |
| <span data-ttu-id="d9747-164">/nu</span><span class="sxs-lookup"><span data-stu-id="d9747-164">/nu</span></span> |<span data-ttu-id="d9747-165">Não verificar se há atualizações após a conclusão da instalação</span><span class="sxs-lookup"><span data-stu-id="d9747-165">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="d9747-166">/d</span><span class="sxs-lookup"><span data-stu-id="d9747-166">/d</span></span> |<span data-ttu-id="d9747-167">Desinstala o agente dos Serviços de Recuperação do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="d9747-167">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="d9747-168">/ph</span><span class="sxs-lookup"><span data-stu-id="d9747-168">/ph</span></span> |<span data-ttu-id="d9747-169">Endereço do host do proxy</span><span class="sxs-lookup"><span data-stu-id="d9747-169">Proxy Host Address</span></span> |- |
| <span data-ttu-id="d9747-170">/po</span><span class="sxs-lookup"><span data-stu-id="d9747-170">/po</span></span> |<span data-ttu-id="d9747-171">Número da porta do host do proxy</span><span class="sxs-lookup"><span data-stu-id="d9747-171">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="d9747-172">/pu</span><span class="sxs-lookup"><span data-stu-id="d9747-172">/pu</span></span> |<span data-ttu-id="d9747-173">UserName do host do proxy</span><span class="sxs-lookup"><span data-stu-id="d9747-173">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="d9747-174">/pw</span><span class="sxs-lookup"><span data-stu-id="d9747-174">/pw</span></span> |<span data-ttu-id="d9747-175">Senha do proxy</span><span class="sxs-lookup"><span data-stu-id="d9747-175">Proxy Password</span></span> |- |

### <a name="registering-with-hello-azure-backup-service"></a><span data-ttu-id="d9747-176">Registrando Olá serviço Backup do Azure</span><span class="sxs-lookup"><span data-stu-id="d9747-176">Registering with hello Azure Backup service</span></span>
<span data-ttu-id="d9747-177">Antes de registrar com hello serviço Backup do Azure, você precisa tooensure que Olá [pré-requisitos](backup-azure-dpm-introduction.md) são atendidos.</span><span class="sxs-lookup"><span data-stu-id="d9747-177">Before you can register with hello Azure Backup service, you need tooensure that hello [prerequisites](backup-azure-dpm-introduction.md) are met.</span></span> <span data-ttu-id="d9747-178">Você deve:</span><span class="sxs-lookup"><span data-stu-id="d9747-178">You must:</span></span>

* <span data-ttu-id="d9747-179">Ter uma assinatura válida do Azure</span><span class="sxs-lookup"><span data-stu-id="d9747-179">Have a valid Azure subscription</span></span>
* <span data-ttu-id="d9747-180">Ter um cofre de backup</span><span class="sxs-lookup"><span data-stu-id="d9747-180">Have a backup vault</span></span>

<span data-ttu-id="d9747-181">credenciais do cofre Olá toodownload, executadas Olá **Get-AzureBackupVaultCredentials** commandlet em um console do PowerShell do Azure e armazenamento-lo em um local conveniente, como * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="d9747-181">toodownload hello vault credentials, run hello **Get-AzureBackupVaultCredentials** commandlet in an Azure PowerShell console and store it in a convenient location like *C:\Downloads\*.</span></span>

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

<span data-ttu-id="d9747-182">Máquina de saudação do registro com cofre Olá é feita usando Olá [DPMCloudRegistration início](https://technet.microsoft.com/library/jj612787) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="d9747-182">Registering hello machine with hello vault is done using hello [Start-DPMCloudRegistration](https://technet.microsoft.com/library/jj612787) cmdlet:</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-DPMCloudRegistration -DPMServerName "TestingServer" -VaultCredentialsFilePath $cred
```

<span data-ttu-id="d9747-183">Isso registrará Olá servidor DPM denominado "TestingServer" com o cofre do Microsoft Azure usando Olá especificada credenciais de cofre.</span><span class="sxs-lookup"><span data-stu-id="d9747-183">This will register hello DPM Server named “TestingServer” with Microsoft Azure Vault using hello specified vault credentials.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d9747-184">Não use o arquivo de credenciais de cofre do caminhos relativos toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="d9747-184">Do not use relative paths toospecify hello vault credentials file.</span></span> <span data-ttu-id="d9747-185">Você deve fornecer um caminho absoluto como um cmdlet toohello de entrada.</span><span class="sxs-lookup"><span data-stu-id="d9747-185">You must provide an absolute path as an input toohello cmdlet.</span></span>
>
>

### <a name="initial-configuration-settings"></a><span data-ttu-id="d9747-186">Definições de configuração iniciais</span><span class="sxs-lookup"><span data-stu-id="d9747-186">Initial configuration settings</span></span>
<span data-ttu-id="d9747-187">Quando hello servidor DPM está registrado com o Cofre de Backup do Azure hello, ele será inicializado com as configurações de assinatura padrão.</span><span class="sxs-lookup"><span data-stu-id="d9747-187">Once hello DPM Server is registered with hello Azure Backup vault, it will start with default subscription settings.</span></span> <span data-ttu-id="d9747-188">Essas configurações de assinatura incluem Olá área de preparação, a criptografia e a rede.</span><span class="sxs-lookup"><span data-stu-id="d9747-188">These subscription settings include Networking, Encryption and hello Staging area.</span></span> <span data-ttu-id="d9747-189">toobegin alteração Olá configurações de assinatura necessário toofirst obtém um identificador nas configurações (padrão) existentes hello usando Olá [DPMCloudSubscriptionSetting Get](https://technet.microsoft.com/library/jj612793) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="d9747-189">toobegin changing hello subscription settings you need toofirst get a handle on hello existing (default) settings using hello [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="d9747-190">Todas as modificações são feitas toothis local PowerShell objeto ```$setting``` e completa do objeto Olá é confirmada tooDPM e toosave de Backup do Azure-los usando Olá [DPMCloudSubscriptionSetting conjunto](https://technet.microsoft.com/library/jj612791) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d9747-190">All modifications are made toothis local PowerShell object ```$setting```  and then hello full object is committed tooDPM and Azure Backup toosave them using hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="d9747-191">Você precisa Olá toouse ```–Commit``` tooensure de sinalizador que Olá alterações são mantidas.</span><span class="sxs-lookup"><span data-stu-id="d9747-191">You need toouse hello ```–Commit``` flag tooensure that hello changes are persisted.</span></span> <span data-ttu-id="d9747-192">configurações de saudação não serão aplicadas e usadas pelo Backup do Azure, a menos que confirmada.</span><span class="sxs-lookup"><span data-stu-id="d9747-192">hello settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

### <a name="networking"></a><span data-ttu-id="d9747-193">Rede</span><span class="sxs-lookup"><span data-stu-id="d9747-193">Networking</span></span>
<span data-ttu-id="d9747-194">Se a conectividade de saudação do hello DPM máquina toohello serviço de Backup do Azure no hello internet for por meio de um servidor proxy, configurações do servidor proxy Olá devem ser fornecidas para toosucceed de backups.</span><span class="sxs-lookup"><span data-stu-id="d9747-194">If hello connectivity of hello DPM machine toohello Azure Backup service on hello internet is through a proxy server, then hello proxy server settings should be provided for backups toosucceed.</span></span> <span data-ttu-id="d9747-195">Isso é feito usando Olá ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` e hello ```ProxyPassword``` parâmetros com hello [DPMCloudSubscriptionSetting conjunto](https://technet.microsoft.com/library/jj612791) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d9747-195">This is done by using hello ```-ProxyServer```, ```-ProxyPort```, ```-ProxyUsername``` and hello ```ProxyPassword``` parameters with hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="d9747-196">Neste exemplo, não há nenhum servidor proxy, por isso estamos explicitamente omitindo todas as informações relacionadas a proxy.</span><span class="sxs-lookup"><span data-stu-id="d9747-196">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="d9747-197">Uso de largura de banda também pode ser controlado com opções de ```-WorkHourBandwidth``` e ```-NonWorkHourBandwidth``` para um determinado conjunto de dias da semana hello.</span><span class="sxs-lookup"><span data-stu-id="d9747-197">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of hello week.</span></span> <span data-ttu-id="d9747-198">Neste exemplo, não definimos nenhuma limitação.</span><span class="sxs-lookup"><span data-stu-id="d9747-198">In this example we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

### <a name="configuring-hello-staging-area"></a><span data-ttu-id="d9747-199">Configurando a área de preparação de saudação</span><span class="sxs-lookup"><span data-stu-id="d9747-199">Configuring hello staging Area</span></span>
<span data-ttu-id="d9747-200">Hello Azure Backup agent em execução no servidor DPM Olá precisa de armazenamento temporário para os dados restaurados da nuvem de saudação (área de preparação local).</span><span class="sxs-lookup"><span data-stu-id="d9747-200">hello Azure Backup agent running on hello DPM server needs temporary storage for data restored from hello cloud (local staging area).</span></span> <span data-ttu-id="d9747-201">Configurar área de preparação de saudação usando Olá [conjunto DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet e hello ```-StagingAreaPath``` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="d9747-201">Configure hello staging area using hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and hello ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="d9747-202">O exemplo hello acima, área de preparação de saudação será definida muito*C:\StagingArea* no objeto do PowerShell Olá ```$setting```.</span><span class="sxs-lookup"><span data-stu-id="d9747-202">In hello example above, hello staging area will be set too*C:\StagingArea* in hello PowerShell object ```$setting```.</span></span> <span data-ttu-id="d9747-203">Certifique-se de que Olá a pasta especificada já existe, ou então a confirmação final Olá das configurações de assinatura Olá falhará.</span><span class="sxs-lookup"><span data-stu-id="d9747-203">Ensure that hello specified folder already exists, or else hello final commit of hello subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="d9747-204">Configurações de criptografia</span><span class="sxs-lookup"><span data-stu-id="d9747-204">Encryption settings</span></span>
<span data-ttu-id="d9747-205">Olá enviados os dados de backup tooAzure Backup é tooprotect criptografados Olá confidencialidade de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="d9747-205">hello backup data sent tooAzure Backup is encrypted tooprotect hello confidentiality of hello data.</span></span> <span data-ttu-id="d9747-206">senha de criptografia de saudação é dados de saudação toodecrypt senha"Olá" no tempo de saudação da restauração.</span><span class="sxs-lookup"><span data-stu-id="d9747-206">hello encryption passphrase is hello "password" toodecrypt hello data at hello time of restore.</span></span> <span data-ttu-id="d9747-207">É importante tookeep este seguro de informações e seguro depois que ela é definida.</span><span class="sxs-lookup"><span data-stu-id="d9747-207">It is important tookeep this information safe and secure once it is set.</span></span>

<span data-ttu-id="d9747-208">Exemplo hello abaixo, comando primeiro Olá converte a cadeia de caracteres de saudação ```passphrase123456789``` tooa segura cadeia de caracteres e atribui Olá seguro toohello variável string denominada ```$Passphrase```.</span><span class="sxs-lookup"><span data-stu-id="d9747-208">In hello example below, hello first command converts hello string ```passphrase123456789``` tooa secure string and assigns hello secure string toohello variable named ```$Passphrase```.</span></span> <span data-ttu-id="d9747-209">Olá segundo comando define a cadeia de caracteres segura Olá ```$Passphrase``` como senha Olá para criptografia de backups.</span><span class="sxs-lookup"><span data-stu-id="d9747-209">hello second command sets hello secure string in ```$Passphrase``` as hello password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> <span data-ttu-id="d9747-210">Manter informações de senha Olá seguros e protegidos depois que ela é definida.</span><span class="sxs-lookup"><span data-stu-id="d9747-210">Keep hello passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="d9747-211">Você não será capaz de toorestore a dados do Azure sem essa frase secreta.</span><span class="sxs-lookup"><span data-stu-id="d9747-211">You will not be able toorestore data from Azure without this passphrase.</span></span>
>
>

<span data-ttu-id="d9747-212">Neste ponto, você deveria ter feito todas as toohello de alterações de saudação necessária ```$setting``` objeto.</span><span class="sxs-lookup"><span data-stu-id="d9747-212">At this point, you should have made all hello required changes toohello ```$setting``` object.</span></span> <span data-ttu-id="d9747-213">Lembre-se as alterações de saudação do toocommit.</span><span class="sxs-lookup"><span data-stu-id="d9747-213">Remember toocommit hello changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-tooazure-backup"></a><span data-ttu-id="d9747-214">Proteger dados tooAzure Backup</span><span class="sxs-lookup"><span data-stu-id="d9747-214">Protect data tooAzure Backup</span></span>
<span data-ttu-id="d9747-215">Nesta seção, você adicionará um tooDPM do servidor de produção e, em seguida, proteger o armazenamento do DPM toolocal Olá dados e, em seguida, tooAzure Backup.</span><span class="sxs-lookup"><span data-stu-id="d9747-215">In this section, you will add a production server tooDPM and then protect hello data toolocal DPM storage and then tooAzure Backup.</span></span> <span data-ttu-id="d9747-216">Exemplos de saudação demonstraremos como tooback backup de arquivos e pastas.</span><span class="sxs-lookup"><span data-stu-id="d9747-216">In hello examples we will demonstrate how tooback up files and folders.</span></span> <span data-ttu-id="d9747-217">Olá lógica pode facilmente ser estendido toobackup qualquer fonte de dados com suporte ao DPM.</span><span class="sxs-lookup"><span data-stu-id="d9747-217">hello logic can easily be extended toobackup any DPM-supported data source.</span></span> <span data-ttu-id="d9747-218">Todos os backups do DPM são regidos por um GP (Grupo de Proteção) com quatro partes:</span><span class="sxs-lookup"><span data-stu-id="d9747-218">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="d9747-219">**Os membros do grupo** é uma lista de todos os objetos protegíveis de saudação (também conhecido como *fontes de dados* no DPM) que você deseja tooprotect em Olá mesmo grupo de proteção.</span><span class="sxs-lookup"><span data-stu-id="d9747-219">**Group members** is a list of all hello protectable objects (also known as *Datasources* in DPM) that you want tooprotect in hello same protection group.</span></span> <span data-ttu-id="d9747-220">Por exemplo, convém tooprotect produção VMs em um grupo de proteção e bancos de dados do SQL Server em outro grupo de proteção como eles podem ter diferentes requisitos de backup.</span><span class="sxs-lookup"><span data-stu-id="d9747-220">For example, you may want tooprotect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="d9747-221">Antes de fazer backup de qualquer fonte de dados em um servidor de produção, você precisa toomake o hello-se de que o agente do DPM está instalado no servidor de saudação e é gerenciado pelo DPM.</span><span class="sxs-lookup"><span data-stu-id="d9747-221">Before you can back up any datasource on a production server you need toomake sure hello DPM Agent is installed on hello server and is managed by DPM.</span></span> <span data-ttu-id="d9747-222">Siga as etapas de saudação para [instalando Olá agente do DPM](https://technet.microsoft.com/library/bb870935.aspx) e vinculá-lo toohello apropriado do servidor DPM.</span><span class="sxs-lookup"><span data-stu-id="d9747-222">Follow hello steps for [installing hello DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it toohello appropriate DPM Server.</span></span>
2. <span data-ttu-id="d9747-223">**Método de proteção de dados** Especifica os locais de backup Olá destino - fita, disco e nuvem.</span><span class="sxs-lookup"><span data-stu-id="d9747-223">**Data protection method** specifies hello target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="d9747-224">Em nosso exemplo, protege dados toohello local em disco e toohello na nuvem.</span><span class="sxs-lookup"><span data-stu-id="d9747-224">In our example we will protect data toohello local disk and toohello cloud.</span></span>
3. <span data-ttu-id="d9747-225">Um **agendamento de backup** que especifica quando backups necessário toobe feito e frequência hello dados devem ser sincronizados entre hello servidor DPM e o servidor de produção de hello.</span><span class="sxs-lookup"><span data-stu-id="d9747-225">A **backup schedule** that specifies when backups need toobe taken and how often hello data should be synchronized between hello DPM Server and hello production server.</span></span>
4. <span data-ttu-id="d9747-226">Um **agenda de retenção** que especifica quanto tempo os pontos de recuperação de saudação do tooretain no Azure.</span><span class="sxs-lookup"><span data-stu-id="d9747-226">A **retention schedule** that specifies how long tooretain hello recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="d9747-227">Criando um grupo de proteção</span><span class="sxs-lookup"><span data-stu-id="d9747-227">Creating a protection group</span></span>
<span data-ttu-id="d9747-228">Comece criando um novo grupo de proteção usando Olá [DPMProtectionGroup novo](https://technet.microsoft.com/library/hh881722) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d9747-228">Start by creating a new Protection Group using hello [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="d9747-229">Olá acima cmdlet criará um grupo de proteção chamada *ProtectGroup01*.</span><span class="sxs-lookup"><span data-stu-id="d9747-229">hello above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="d9747-230">Um grupo de proteção também pode ser modificado posteriormente tooadd toohello backup nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="d9747-230">An existing protection group can also be modified later tooadd backup toohello Azure cloud.</span></span> <span data-ttu-id="d9747-231">No entanto, toomake alterações toohello grupo de proteção - novo ou existente - precisamos tooget um identificador em uma *modificável* objeto usando Olá [DPMModifiableProtectionGroup Get](https://technet.microsoft.com/library/hh881713) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d9747-231">However, toomake any changes toohello Protection Group - new or existing - we need tooget a handle on a *modifiable* object using hello [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-toohello-protection-group"></a><span data-ttu-id="d9747-232">Adicionar membros de grupo toohello grupo de proteção</span><span class="sxs-lookup"><span data-stu-id="d9747-232">Adding group members toohello Protection Group</span></span>
<span data-ttu-id="d9747-233">Cada agente do DPM sabe lista Olá de fontes de dados no servidor de saudação que ele está instalado.</span><span class="sxs-lookup"><span data-stu-id="d9747-233">Each DPM Agent knows hello list of datasources on hello server that it is installed on.</span></span> <span data-ttu-id="d9747-234">tooadd toohello uma fonte de dados grupo de proteção, Olá toofirst de necessidades de agente do DPM enviar uma lista de servidor DPM de toohello back Olá fontes de dados.</span><span class="sxs-lookup"><span data-stu-id="d9747-234">tooadd a datasource toohello Protection Group, hello DPM Agent needs toofirst send a list of hello datasources back toohello DPM server.</span></span> <span data-ttu-id="d9747-235">Uma ou mais fontes de dados forem selecionadas e adicionadas toohello grupo de proteção.</span><span class="sxs-lookup"><span data-stu-id="d9747-235">One or more datasources are then selected and added toohello Protection Group.</span></span> <span data-ttu-id="d9747-236">Olá PowerShell etapas necessárias tooget alcançar isso são:</span><span class="sxs-lookup"><span data-stu-id="d9747-236">hello PowerShell steps needed tooget achieve this are:</span></span>

1. <span data-ttu-id="d9747-237">Obter uma lista de todos os servidores gerenciados pelo DPM por meio de saudação agente do DPM.</span><span class="sxs-lookup"><span data-stu-id="d9747-237">Fetch a list of all servers managed by DPM through hello DPM Agent.</span></span>
2. <span data-ttu-id="d9747-238">Escolher um servidor específico.</span><span class="sxs-lookup"><span data-stu-id="d9747-238">Choose a specific server.</span></span>
3. <span data-ttu-id="d9747-239">Obter uma lista de todas as fontes de dados no servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="d9747-239">Fetch a list of all datasources on hello server.</span></span>
4. <span data-ttu-id="d9747-240">Escolha uma ou mais fontes de dados e adicioná-los toohello grupo de proteção</span><span class="sxs-lookup"><span data-stu-id="d9747-240">Choose one or more datasources and add them toohello Protection Group</span></span>

<span data-ttu-id="d9747-241">Olá lista de servidores nos quais Olá agente do DPM está instalado e está sendo gerenciado pelo servidor DPM da saudação é adquirida com hello [DPMProductionServer Get](https://technet.microsoft.com/library/hh881600) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d9747-241">hello list of servers on which hello DPM Agent is installed and is being managed by hello DPM Server is acquired with hello [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="d9747-242">Neste exemplo, filtraremos e configuraremos apenas o PS com o nome *productionserver01* para o backup.</span><span class="sxs-lookup"><span data-stu-id="d9747-242">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

<span data-ttu-id="d9747-243">Agora obter lista de saudação de fontes de dados em ```$server``` usando Olá [DPMDatasource Get](https://technet.microsoft.com/library/hh881605) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d9747-243">Now fetch hello list of datasources on ```$server``` using hello [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="d9747-244">Neste exemplo nós estamos filtrando para volume hello * unidade d:\* que queremos tooconfigure para backup.</span><span class="sxs-lookup"><span data-stu-id="d9747-244">In this example we are filtering for hello volume *D:\* which we want tooconfigure for backup.</span></span> <span data-ttu-id="d9747-245">Esta fonte de dados é adicionada toohello grupo de proteção usando Olá [DPMChildDatasource adicionar](https://technet.microsoft.com/library/hh881732) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d9747-245">This datasource is then added toohello Protection Group using hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="d9747-246">Lembre-se de saudação toouse *modifable* objeto do grupo de proteção ```$MPG``` toomake adições de saudação.</span><span class="sxs-lookup"><span data-stu-id="d9747-246">Remember toouse hello *modifable* protection group object ```$MPG``` toomake hello additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="d9747-247">Repita essa etapa, quantas vezes forem necessárias, até que você adicionou todos os Olá escolhido o grupo de proteção toohello fontes de dados.</span><span class="sxs-lookup"><span data-stu-id="d9747-247">Repeat this step as many times as required, until you have added all hello chosen datasources toohello protection group.</span></span> <span data-ttu-id="d9747-248">Você também pode iniciar com apenas uma fonte de dados e fluxo de trabalho Olá completa para a criação de grupo de proteção de saudação e posteriormente adicionar mais fontes de dados toohello grupo de proteção.</span><span class="sxs-lookup"><span data-stu-id="d9747-248">You can also start with just one datasource, and complete hello workflow for creating hello Protection Group, and at a later point add more datasources toohello Protection Group.</span></span>

### <a name="selecting-hello-data-protection-method"></a><span data-ttu-id="d9747-249">Selecionar método de proteção de dados hello</span><span class="sxs-lookup"><span data-stu-id="d9747-249">Selecting hello data protection method</span></span>
<span data-ttu-id="d9747-250">Depois de fontes de dados Olá adicionou toohello grupo de proteção, Olá próxima etapa é toospecify o método de proteção de saudação usando Olá [DPMProtectionType conjunto](https://technet.microsoft.com/library/hh881725) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d9747-250">Once hello datasources have been added toohello Protection Group, hello next step is toospecify hello protection method using hello [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="d9747-251">Neste exemplo, Olá grupo de proteção será instalado para o disco local e backup na nuvem.</span><span class="sxs-lookup"><span data-stu-id="d9747-251">In this example, hello Protection Group will be setup for local disk and cloud backup.</span></span> <span data-ttu-id="d9747-252">Você também precisa toospecify Olá a fonte de dados que você deseja toocloud tooprotect usando Olá [DPMChildDatasource adicionar](https://technet.microsoft.com/library/hh881732.aspx) cmdlet com - sinalizador Online.</span><span class="sxs-lookup"><span data-stu-id="d9747-252">You also need toospecify hello datasource that you want tooprotect toocloud using hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-hello-retention-range"></a><span data-ttu-id="d9747-253">Definir o período de retenção de saudação</span><span class="sxs-lookup"><span data-stu-id="d9747-253">Setting hello retention range</span></span>
<span data-ttu-id="d9747-254">Definir retenção Olá Olá backup pontos de usando Olá [DPMPolicyObjective conjunto](https://technet.microsoft.com/library/hh881762) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d9747-254">Set hello retention for hello backup points using hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="d9747-255">Enquanto a retenção de saudação ímpar tooset pode parecer antes de agendamento de backup Olá tiver sido definido, usando Olá ```Set-DPMPolicyObjective``` cmdlet automaticamente define uma agenda de backup padrão que pode ser modificada.</span><span class="sxs-lookup"><span data-stu-id="d9747-255">While it might seem odd tooset hello retention before hello backup schedule has been defined, using hello ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="d9747-256">É sempre agendamento de backup possível tooset Olá primeiro e Olá a política de retenção depois.</span><span class="sxs-lookup"><span data-stu-id="d9747-256">It is always possible tooset hello backup schedule first and hello retention policy after.</span></span>

<span data-ttu-id="d9747-257">O exemplo hello abaixo, Olá define parâmetros de retenção Olá para backups em disco.</span><span class="sxs-lookup"><span data-stu-id="d9747-257">In hello example below, hello cmdlet sets hello retention parameters for disk backups.</span></span> <span data-ttu-id="d9747-258">Isso manterá backups para 10 dias e os dados de sincronização entre servidores de produção de hello e DPM Olá a cada 6 horas.</span><span class="sxs-lookup"><span data-stu-id="d9747-258">This will retain backups for 10 days, and sync data every 6 hours between hello production server and hello DPM server.</span></span> <span data-ttu-id="d9747-259">Olá ```SynchronizationFrequencyMinutes``` não define quantas vezes um ponto de backup é criado, mas como frequência os dados de servidor DPM toohello copiado; Isso impede que os backups se torne muito grande.</span><span class="sxs-lookup"><span data-stu-id="d9747-259">hello ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied toohello DPM server; this prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="d9747-260">Intervalos de retenção de saudação para backups vai tooAzure (DPM refere-se toothese como backups Online) podem ser configurados para [usando um esquema de avô-pai-filho (GFS) de retenção de longo prazo](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="d9747-260">For backups going tooAzure (DPM refers toothese as Online backups) hello retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="d9747-261">Ou seja, você pode definir uma política de retenção combinada que envolva políticas de retenção diárias, semanais, mensais e anuais.</span><span class="sxs-lookup"><span data-stu-id="d9747-261">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="d9747-262">Neste exemplo, criamos uma matriz que representa o esquema de retenção complexas Olá que queremos e, em seguida, configurar o período de retenção hello usando Olá [DPMPolicyObjective conjunto](https://technet.microsoft.com/library/hh881762) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d9747-262">In this example, we create an array representing hello complex retention scheme that we want, and then configure hello retention range using hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-hello-backup-schedule"></a><span data-ttu-id="d9747-263">Agendamento de backup de saudação do conjunto</span><span class="sxs-lookup"><span data-stu-id="d9747-263">Set hello backup schedule</span></span>
<span data-ttu-id="d9747-264">O DPM define uma agenda de backup padrão automaticamente se você especificar o objetivo de proteção de saudação usando Olá ```Set-DPMPolicyObjective``` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d9747-264">DPM sets a default backup schedule automatically if you specify hello protection objective using hello ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="d9747-265">os agendamentos padrão Olá toochange, use Olá [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet seguido por Olá [DPMPolicySchedule conjunto](https://technet.microsoft.com/library/hh881723) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d9747-265">toochange hello default schedules, use hello [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by hello [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="d9747-266">No exemplo acima, a saudação ```$onlineSch``` é uma matriz que contém a agenda de proteção online existente Olá para Olá grupo de proteção no esquema GFS Olá com quatro elementos:</span><span class="sxs-lookup"><span data-stu-id="d9747-266">In hello example above, ```$onlineSch``` is an array with four elements that contains hello existing online protection schedule for hello Protection Group in hello GFS scheme:</span></span>

1. <span data-ttu-id="d9747-267">```$onlineSch[0]```conterá agenda diária Olá</span><span class="sxs-lookup"><span data-stu-id="d9747-267">```$onlineSch[0]``` will contain hello daily schedule</span></span>
2. <span data-ttu-id="d9747-268">```$onlineSch[1]```conterá a agenda semanal Olá</span><span class="sxs-lookup"><span data-stu-id="d9747-268">```$onlineSch[1]``` will contain hello weekly schedule</span></span>
3. <span data-ttu-id="d9747-269">```$onlineSch[2]```conterá o agendamento mensal Olá</span><span class="sxs-lookup"><span data-stu-id="d9747-269">```$onlineSch[2]``` will contain hello monthly schedule</span></span>
4. <span data-ttu-id="d9747-270">```$onlineSch[3]```conterá o agendamento de saudação anual</span><span class="sxs-lookup"><span data-stu-id="d9747-270">```$onlineSch[3]``` will contain hello yearly schedule</span></span>

<span data-ttu-id="d9747-271">Portanto, se você precisar agenda semanal do toomodify hello, você precisa toorefer toohello ```$onlineSch[1]```.</span><span class="sxs-lookup"><span data-stu-id="d9747-271">So if you need toomodify hello weekly schedule, you need toorefer toohello ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="d9747-272">Backup inicial</span><span class="sxs-lookup"><span data-stu-id="d9747-272">Initial backup</span></span>
<span data-ttu-id="d9747-273">Ao fazer backup de uma fonte de dados para Olá primeira vez, o DPM precisa toocreate uma réplica inicial que criará uma cópia da saudação toobe de fonte de dados protegido no volume de réplica do DPM.</span><span class="sxs-lookup"><span data-stu-id="d9747-273">When backing up a datasource for hello first time, DPM needs toocreate an initial replica which will create a copy of hello datasource toobe protected on DPM replica volume.</span></span> <span data-ttu-id="d9747-274">Essa atividade pode ser agendada durante um período específico ou pode ser disparada de manualmente, usando Olá [conjunto DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet com o parâmetro hello ```-NOW```.</span><span class="sxs-lookup"><span data-stu-id="d9747-274">This activity can either be scheduled for a specific time, or can be triggered manually, using hello [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with hello parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-hello-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="d9747-275">Alterando o tamanho de saudação de réplica do DPM e o volume de ponto de recuperação</span><span class="sxs-lookup"><span data-stu-id="d9747-275">Changing hello size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="d9747-276">Você também pode alterar o tamanho de saudação do volume de réplica do DPM, bem como cópia de sombra de volume usando [DPMDatasourceDiskAllocation conjunto](https://technet.microsoft.com/library/hh881618.aspx) cmdlet como Olá exemplo abaixo: Get-DatasourceDiskAllocation - Datasource $DS Set-DatasourceDiskAllocation - Datasource $DS - ProtectionGroup $MPG-manual - ReplicaArea (2 gb) - ShadowCopyArea (2 gb)</span><span class="sxs-lookup"><span data-stu-id="d9747-276">You can also change hello size of DPM Replica volume as well as Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in hello below example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-hello-changes-toohello-protection-group"></a><span data-ttu-id="d9747-277">Confirmar Olá altera toohello grupo de proteção</span><span class="sxs-lookup"><span data-stu-id="d9747-277">Committing hello changes toohello Protection Group</span></span>
<span data-ttu-id="d9747-278">Finalmente, alterações de saudação precisam toobe confirmada antes do DPM pode fazer backup de saudação por nova configuração de grupo de proteção hello.</span><span class="sxs-lookup"><span data-stu-id="d9747-278">Finally, hello changes need toobe committed before DPM can take hello backup per hello new Protection Group configuration.</span></span> <span data-ttu-id="d9747-279">Isso é feito usando Olá [DPMProtectionGroup conjunto](https://technet.microsoft.com/library/hh881758) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d9747-279">This is done using hello [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-hello-backup-points"></a><span data-ttu-id="d9747-280">Exibir pontos de backup Olá</span><span class="sxs-lookup"><span data-stu-id="d9747-280">View hello backup points</span></span>
<span data-ttu-id="d9747-281">Você pode usar o hello [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) tooget cmdlet uma lista de todos os pontos de recuperação para uma fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="d9747-281">You can use hello [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet tooget a list of all recovery points for a datasource.</span></span> <span data-ttu-id="d9747-282">Neste exemplo, iremos:</span><span class="sxs-lookup"><span data-stu-id="d9747-282">In this example, we will:</span></span>

* <span data-ttu-id="d9747-283">Buscar todas as páginas de saudação no servidor DPM de saudação que será armazenada em uma matriz```$PG```</span><span class="sxs-lookup"><span data-stu-id="d9747-283">fetch all hello PGs on hello DPM server which will be stored in an array ```$PG```</span></span>
* <span data-ttu-id="d9747-284">obter Olá fontes de dados correspondente toohello```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="d9747-284">get hello datasources corresponding toohello ```$PG[0]```</span></span>
* <span data-ttu-id="d9747-285">obter todos os pontos de recuperação Olá para uma fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="d9747-285">get all hello recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="d9747-286">Restaurar dados protegidos no Azure</span><span class="sxs-lookup"><span data-stu-id="d9747-286">Restore data protected on Azure</span></span>
<span data-ttu-id="d9747-287">A restauração de dados é uma combinação de um objeto ```RecoverableItem``` e um objeto ```RecoveryOption```.</span><span class="sxs-lookup"><span data-stu-id="d9747-287">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="d9747-288">Na seção anterior do hello, nós temos uma lista de pontos de backup Olá para uma fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="d9747-288">In hello previous section, we got a list of hello backup points for a datasource.</span></span>

<span data-ttu-id="d9747-289">O exemplo hello abaixo, demonstraremos como máquina virtual de toorestore um Hyper-V do Backup do Azure por pontos de backup combinando com hello de destino para recuperação.</span><span class="sxs-lookup"><span data-stu-id="d9747-289">In hello example below, we demonstrate how toorestore a Hyper-V virtual machine from Azure Backup by combining backup points with hello target for recovery.</span></span> <span data-ttu-id="d9747-290">Isso inclui:</span><span class="sxs-lookup"><span data-stu-id="d9747-290">This includes:</span></span>

* <span data-ttu-id="d9747-291">Criando uma opção de recuperação usando Olá [DPMRecoveryOption novo](https://technet.microsoft.com/library/hh881592) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d9747-291">Creating a recovery option using hello  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="d9747-292">Matriz de Olá busca de pontos de backup usando Olá ```Get-DPMRecoveryPoint``` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d9747-292">Fetching hello array of backup points using hello ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="d9747-293">Escolhendo um toorestore de ponto de backup do.</span><span class="sxs-lookup"><span data-stu-id="d9747-293">Choosing a backup point toorestore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="d9747-294">comandos de saudação podem ser facilmente estendidos para qualquer tipo de fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="d9747-294">hello commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9747-295">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d9747-295">Next steps</span></span>
* <span data-ttu-id="d9747-296">Para obter mais informações sobre Backup do Azure para DPM consulte [Introdução tooDPM Backup](backup-azure-dpm-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="d9747-296">For more information about Azure Backup for DPM see [Introduction tooDPM Backup](backup-azure-dpm-introduction.md)</span></span>
