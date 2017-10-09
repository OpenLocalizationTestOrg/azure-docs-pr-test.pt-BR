---
title: aaaAzure Backup - Use o PowerShell tooback cargas de trabalho do DPM | Microsoft Docs
description: Saiba como toodeploy e gerenciar o Backup do Azure para o Data Protection Manager (DPM) usando o PowerShell
services: backup
documentationcenter: 
author: NKolli1
manager: shreeshd
editor: 
ms.assetid: e9bd223c-2398-4eb1-9bf3-50e08970fea7
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/23/2017
ms.author: adigan;anuragm;trinadhk;markgal
ms.openlocfilehash: 27d2b4b3127b68c9da564697eb61dc3ccbc34b3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="d5f8d-103">Implantar e gerenciar o backup tooAzure para servidores do Data Protection Manager (DPM) usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="d5f8d-103">Deploy and manage backup tooAzure for Data Protection Manager (DPM) servers using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d5f8d-104">ARM</span><span class="sxs-lookup"><span data-stu-id="d5f8d-104">ARM</span></span>](backup-dpm-automation.md)
> * [<span data-ttu-id="d5f8d-105">Clássico</span><span class="sxs-lookup"><span data-stu-id="d5f8d-105">Classic</span></span>](backup-dpm-automation-classic.md)
>
>

<span data-ttu-id="d5f8d-106">Este artigo mostra como toouse PowerShell toosetup Backup do Azure em um servidor DPM e toomanage backup e recuperação.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-106">This article shows you how toouse PowerShell toosetup Azure Backup on a DPM server, and toomanage backup and recovery.</span></span>

## <a name="setting-up-hello-powershell-environment"></a><span data-ttu-id="d5f8d-107">Configurando o ambiente do PowerShell Olá</span><span class="sxs-lookup"><span data-stu-id="d5f8d-107">Setting up hello PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="d5f8d-108">Antes de você pode usar o PowerShell toomanage backups tooAzure Data Protection Manager, é necessário toohave Olá direita ambiente PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-108">Before you can use PowerShell toomanage backups from Data Protection Manager tooAzure, you need toohave hello right environment in PowerShell.</span></span> <span data-ttu-id="d5f8d-109">No início de saudação da sessão do PowerShell Olá, certifique-se de que você execute Olá módulos corretos do comando tooimport Olá a seguir e permitem que você toocorrectly Referência Olá DPM cmdlets:</span><span class="sxs-lookup"><span data-stu-id="d5f8d-109">At hello start of hello PowerShell session, ensure that you run hello following command tooimport hello right modules and allow you toocorrectly reference hello DPM cmdlets:</span></span>

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

## <a name="setup-and-registration"></a><span data-ttu-id="d5f8d-110">Configuração e registro</span><span class="sxs-lookup"><span data-stu-id="d5f8d-110">Setup and Registration</span></span>
<span data-ttu-id="d5f8d-111">toobegin:</span><span class="sxs-lookup"><span data-stu-id="d5f8d-111">toobegin:</span></span>

1. <span data-ttu-id="d5f8d-112">[Baixe o PowerShell mais recente](https://github.com/Azure/azure-powershell/releases) (a versão mínima exigida é: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="d5f8d-112">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is: 1.0.0)</span></span>
2. <span data-ttu-id="d5f8d-113">Habilitar cmdlets do Backup do Azure Olá alternando muito*AzureResourceManager* modo usando Olá **Switch-AzureMode** commandlet:</span><span class="sxs-lookup"><span data-stu-id="d5f8d-113">Enable hello Azure Backup commandlets by switching too*AzureResourceManager* mode by using hello **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="d5f8d-114">Olá tarefas de registro e configuração a seguir podem ser automatizadas com o PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d5f8d-114">hello following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="d5f8d-115">Criar um cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="d5f8d-115">Create a Recovery Services vault</span></span>
* <span data-ttu-id="d5f8d-116">Instalando o agente de Backup do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="d5f8d-116">Installing hello Azure Backup agent</span></span>
* <span data-ttu-id="d5f8d-117">Registrando Olá serviço Backup do Azure</span><span class="sxs-lookup"><span data-stu-id="d5f8d-117">Registering with hello Azure Backup service</span></span>
* <span data-ttu-id="d5f8d-118">Configurações de rede</span><span class="sxs-lookup"><span data-stu-id="d5f8d-118">Networking settings</span></span>
* <span data-ttu-id="d5f8d-119">Configurações de criptografia</span><span class="sxs-lookup"><span data-stu-id="d5f8d-119">Encryption settings</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="d5f8d-120">Criar um cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="d5f8d-120">Create a recovery services vault</span></span>
<span data-ttu-id="d5f8d-121">Olá etapas levá-lo na criação de um cofre de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-121">hello following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="d5f8d-122">Um cofre dos Serviços de Recuperação é diferente de um cofre de Backup.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-122">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="d5f8d-123">Se você estiver usando o Backup do Azure para Olá primeira vez, você deve usar o hello **registro AzureRMResourceProvider** provedor de serviço de recuperação do Azure do cmdlet tooregister Olá com sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-123">If you are using Azure Backup for hello first time, you must use hello **Register-AzureRMResourceProvider** cmdlet tooregister hello Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="d5f8d-124">Olá Cofre de serviços de recuperação é um recurso do ARM, portanto, você precisa tooplace-lo em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-124">hello Recovery Services vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="d5f8d-125">Você pode usar um grupo de recursos existente ou criar um novo.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-125">You can use an existing resource group, or create a new one.</span></span> <span data-ttu-id="d5f8d-126">Ao criar um novo grupo de recursos, especifique o nome de saudação e local para o grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-126">When creating a new resource group, specify hello name and location for hello resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="d5f8d-127">Saudação de uso **AzureRmRecoveryServicesVault novo** cmdlet toocreate um novo cofre.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-127">Use hello **New-AzureRmRecoveryServicesVault** cmdlet toocreate a new vault.</span></span> <span data-ttu-id="d5f8d-128">Certifique-se de que toospecify Olá mesmo local para o cofre Olá que foi usada para o grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-128">Be sure toospecify hello same location for hello vault as was used for hello resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="d5f8d-129">Especificar o tipo de saudação do toouse de redundância de armazenamento; Você pode usar [armazenamento localmente redundante (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) ou [Geo redundante GRS (armazenamento)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="d5f8d-129">Specify hello type of storage redundancy toouse; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="d5f8d-130">Olá exemplo a seguir mostra Olá - BackupStorageRedundancy opção testVault é definida tooGeoRedundant.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-130">hello following example shows hello -BackupStorageRedundancy option for testVault is set tooGeoRedundant.</span></span>

   > [!TIP]
   > <span data-ttu-id="d5f8d-131">Muitos cmdlets do Backup do Azure exigem Olá objeto de Cofre de serviços de recuperação como entrada.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-131">Many Azure Backup cmdlets require hello Recovery Services vault object as an input.</span></span> <span data-ttu-id="d5f8d-132">Por esse motivo, é conveniente toostore Olá serviços de recuperação de Backup cofre objeto em uma variável.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-132">For this reason, it is convenient toostore hello Backup Recovery Services vault object in a variable.</span></span>
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-hello-vaults-in-a-subscription"></a><span data-ttu-id="d5f8d-133">Exibição Olá cofres em uma assinatura</span><span class="sxs-lookup"><span data-stu-id="d5f8d-133">View hello vaults in a subscription</span></span>
<span data-ttu-id="d5f8d-134">Use **Get-AzureRmRecoveryServicesVault** tooview lista de saudação de todos os cofres na assinatura atual hello.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-134">Use **Get-AzureRmRecoveryServicesVault** tooview hello list of all vaults in hello current subscription.</span></span> <span data-ttu-id="d5f8d-135">Você pode usar este toocheck de comando que um novo cofre foi criado ou toosee que cofres estão disponíveis na assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-135">You can use this command toocheck that a new  vault was created, or toosee what vaults are available in hello subscription.</span></span>

<span data-ttu-id="d5f8d-136">Execute o comando hello, Get-AzureRmRecoveryServicesVault, e todos os cofres na assinatura de saudação são listados.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-136">Run hello command, Get-AzureRmRecoveryServicesVault, and all vaults in hello subscription are listed.</span></span>

```
PS C:\> Get-AzureRmRecoveryServicesVault
Name              : Contoso-vault
ID                : /subscriptions/1234
Type              : Microsoft.RecoveryServices/vaults
Location          : WestUS
ResourceGroupName : Contoso-docs-rg
SubscriptionId    : 1234-567f-8910-abc
Properties        : Microsoft.Azure.Commands.RecoveryServices.ARSVaultProperties
```


## <a name="installing-hello-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="d5f8d-137">Instalando o agente de Backup do Azure Olá em um servidor DPM</span><span class="sxs-lookup"><span data-stu-id="d5f8d-137">Installing hello Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="d5f8d-138">Antes de instalar o agente de Backup do Azure Olá, você precisará instalador de saudação toohave baixado e presente no saudação do Windows Server.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-138">Before you install hello Azure Backup agent, you need toohave hello installer downloaded and present on hello Windows Server.</span></span> <span data-ttu-id="d5f8d-139">Você pode obter a versão mais recente de saudação do instalador de saudação de saudação [Microsoft Download Center](http://aka.ms/azurebackup_agent) ou da página de painel do Cofre de serviços de recuperação hello.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-139">You can get hello latest version of hello installer from hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from hello Recovery Services vault's Dashboard page.</span></span> <span data-ttu-id="d5f8d-140">Salvar instalador Olá tooan local facilmente acessível, como * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-140">Save hello installer tooan easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="d5f8d-141">tooinstall Olá execução do agente, Olá seguinte comando em um console do PowerShell com privilégios elevados **no servidor DPM Olá**:</span><span class="sxs-lookup"><span data-stu-id="d5f8d-141">tooinstall hello agent, run hello following command in an elevated PowerShell console **on hello DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="d5f8d-142">Isso instala o agente de saudação com todas as opções padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-142">This installs hello agent with all hello default options.</span></span> <span data-ttu-id="d5f8d-143">instalação de saudação leva alguns minutos no plano de fundo de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-143">hello installation takes a few minutes in hello background.</span></span> <span data-ttu-id="d5f8d-144">Se você não especificar Olá */nu* Olá opção **Windows Update** janela será aberta no final de saudação do hello instalação toocheck para todas as atualizações.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-144">If you do not specify hello */nu* option hello **Windows Update** window opens at hello end of hello installation toocheck for any updates.</span></span>

<span data-ttu-id="d5f8d-145">Agente de saudação são mostrados na lista de saudação de programas instalados.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-145">hello agent shows up in hello list of installed programs.</span></span> <span data-ttu-id="d5f8d-146">lista de saudação toosee de instalado programas, consulte muito**painel de controle** > **programas** > **programas e recursos**.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-146">toosee hello list of installed programs, go too**Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agente instalado](./media/backup-dpm-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="d5f8d-148">Opções de instalação</span><span class="sxs-lookup"><span data-stu-id="d5f8d-148">Installation options</span></span>
<span data-ttu-id="d5f8d-149">toosee todas as opções de saudação disponíveis por meio de saudação de linha de comando, use Olá a seguir de comando:</span><span class="sxs-lookup"><span data-stu-id="d5f8d-149">toosee all hello options available via hello commandline, use hello following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="d5f8d-150">Olá as opções disponíveis incluem:</span><span class="sxs-lookup"><span data-stu-id="d5f8d-150">hello available options include:</span></span>

| <span data-ttu-id="d5f8d-151">Opção</span><span class="sxs-lookup"><span data-stu-id="d5f8d-151">Option</span></span> | <span data-ttu-id="d5f8d-152">Detalhes</span><span class="sxs-lookup"><span data-stu-id="d5f8d-152">Details</span></span> | <span data-ttu-id="d5f8d-153">Padrão</span><span class="sxs-lookup"><span data-stu-id="d5f8d-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d5f8d-154">/q</span><span class="sxs-lookup"><span data-stu-id="d5f8d-154">/q</span></span> |<span data-ttu-id="d5f8d-155">Instalação silenciosa</span><span class="sxs-lookup"><span data-stu-id="d5f8d-155">Quiet installation</span></span> |- |
| <span data-ttu-id="d5f8d-156">/p:"local"</span><span class="sxs-lookup"><span data-stu-id="d5f8d-156">/p:"location"</span></span> |<span data-ttu-id="d5f8d-157">Pasta de instalação de toohello de caminho para o agente de Backup do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-157">Path toohello installation folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="d5f8d-158">C:\Arquivos de Programas\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="d5f8d-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="d5f8d-159">/s:"local"</span><span class="sxs-lookup"><span data-stu-id="d5f8d-159">/s:"location"</span></span> |<span data-ttu-id="d5f8d-160">Pasta de cache de toohello de caminho para o agente de Backup do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-160">Path toohello cache folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="d5f8d-161">C:\Arquivos de Programas\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="d5f8d-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="d5f8d-162">/m</span><span class="sxs-lookup"><span data-stu-id="d5f8d-162">/m</span></span> |<span data-ttu-id="d5f8d-163">Aceitar tooMicrosoft atualização</span><span class="sxs-lookup"><span data-stu-id="d5f8d-163">Opt-in tooMicrosoft Update</span></span> |- |
| <span data-ttu-id="d5f8d-164">/nu</span><span class="sxs-lookup"><span data-stu-id="d5f8d-164">/nu</span></span> |<span data-ttu-id="d5f8d-165">Não verificar se há atualizações após a conclusão da instalação</span><span class="sxs-lookup"><span data-stu-id="d5f8d-165">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="d5f8d-166">/d</span><span class="sxs-lookup"><span data-stu-id="d5f8d-166">/d</span></span> |<span data-ttu-id="d5f8d-167">Desinstala o agente dos Serviços de Recuperação do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="d5f8d-167">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="d5f8d-168">/ph</span><span class="sxs-lookup"><span data-stu-id="d5f8d-168">/ph</span></span> |<span data-ttu-id="d5f8d-169">Endereço do host do proxy</span><span class="sxs-lookup"><span data-stu-id="d5f8d-169">Proxy Host Address</span></span> |- |
| <span data-ttu-id="d5f8d-170">/po</span><span class="sxs-lookup"><span data-stu-id="d5f8d-170">/po</span></span> |<span data-ttu-id="d5f8d-171">Número da porta do host do proxy</span><span class="sxs-lookup"><span data-stu-id="d5f8d-171">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="d5f8d-172">/pu</span><span class="sxs-lookup"><span data-stu-id="d5f8d-172">/pu</span></span> |<span data-ttu-id="d5f8d-173">UserName do host do proxy</span><span class="sxs-lookup"><span data-stu-id="d5f8d-173">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="d5f8d-174">/pw</span><span class="sxs-lookup"><span data-stu-id="d5f8d-174">/pw</span></span> |<span data-ttu-id="d5f8d-175">Senha do proxy</span><span class="sxs-lookup"><span data-stu-id="d5f8d-175">Proxy Password</span></span> |- |

## <a name="registering-dpm-tooa-recovery-services-vault"></a><span data-ttu-id="d5f8d-176">Registrando o DPM tooa Cofre de serviços de recuperação</span><span class="sxs-lookup"><span data-stu-id="d5f8d-176">Registering DPM tooa Recovery Services Vault</span></span>
<span data-ttu-id="d5f8d-177">Depois que você criar o Cofre de serviços de recuperação de Olá, baixe o agente mais recente hello e as credenciais do cofre hello e armazená-lo em um local conveniente como C:\Downloads.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-177">After you created hello Recovery Services vault, download hello latest agent and hello vault credentials and store it in a convenient location like C:\Downloads.</span></span>

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
PS C:\> $credsfilename
C:\downloads\testvault\_Sun Apr 10 2016.VaultCredentials
```

<span data-ttu-id="d5f8d-178">No servidor DPM hello, executar Olá [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet tooregister Olá máquina cofre hello.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-178">On hello DPM server, run hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet tooregister hello machine with hello vault.</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :West US
Machine registration succeeded.
```

### <a name="initial-configuration-settings"></a><span data-ttu-id="d5f8d-179">Definições de configuração iniciais</span><span class="sxs-lookup"><span data-stu-id="d5f8d-179">Initial configuration settings</span></span>
<span data-ttu-id="d5f8d-180">Depois que o hello servidor DPM está registrado com hello Cofre de serviços de recuperação, ele começa com as configurações de assinatura padrão.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-180">Once hello DPM Server is registered with hello Recovery Services vault, it starts with default subscription settings.</span></span> <span data-ttu-id="d5f8d-181">Essas configurações de assinatura incluem Olá área de preparação, a criptografia e a rede.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-181">These subscription settings include Networking, Encryption and hello Staging area.</span></span> <span data-ttu-id="d5f8d-182">configurações de assinatura toochange necessário toofirst obtém um identificador nas configurações (padrão) existentes hello usando Olá [DPMCloudSubscriptionSetting Get](https://technet.microsoft.com/library/jj612793) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="d5f8d-182">toochange subscription settings you need toofirst get a handle on hello existing (default) settings using hello [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="d5f8d-183">Todas as modificações são feitas toothis local PowerShell objeto ```$setting``` e completa do objeto Olá é confirmada tooDPM e toosave de Backup do Azure-los usando Olá [DPMCloudSubscriptionSetting conjunto](https://technet.microsoft.com/library/jj612791) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-183">All modifications are made toothis local PowerShell object ```$setting```  and then hello full object is committed tooDPM and Azure Backup toosave them using hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="d5f8d-184">Você precisa Olá toouse ```–Commit``` tooensure de sinalizador que Olá alterações são mantidas.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-184">You need toouse hello ```–Commit``` flag tooensure that hello changes are persisted.</span></span> <span data-ttu-id="d5f8d-185">configurações de saudação não serão aplicadas e usadas pelo Backup do Azure, a menos que confirmada.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-185">hello settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="networking"></a><span data-ttu-id="d5f8d-186">Rede</span><span class="sxs-lookup"><span data-stu-id="d5f8d-186">Networking</span></span>
<span data-ttu-id="d5f8d-187">Se a conectividade de saudação do hello DPM máquina toohello serviço de Backup do Azure no hello internet for por meio de um servidor proxy, configurações do servidor proxy Olá devem ser fornecidas para os backups bem-sucedidos.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-187">If hello connectivity of hello DPM machine toohello Azure Backup service on hello internet is through a proxy server, then hello proxy server settings should be provided for successful backups.</span></span> <span data-ttu-id="d5f8d-188">Isso é feito usando Olá ```-ProxyServer```e ```-ProxyPort```, ```-ProxyUsername``` e hello ```ProxyPassword``` parâmetros com hello [DPMCloudSubscriptionSetting conjunto](https://technet.microsoft.com/library/jj612791) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-188">This is done by using hello ```-ProxyServer```and ```-ProxyPort```, ```-ProxyUsername``` and hello ```ProxyPassword``` parameters with hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="d5f8d-189">Neste exemplo, não há nenhum servidor proxy, por isso estamos explicitamente omitindo todas as informações relacionadas a proxy.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-189">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="d5f8d-190">Uso de largura de banda também pode ser controlado com opções de ```-WorkHourBandwidth``` e ```-NonWorkHourBandwidth``` para um determinado conjunto de dias da semana hello.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-190">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of hello week.</span></span> <span data-ttu-id="d5f8d-191">Neste exemplo, não definimos nenhuma limitação.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-191">In this example, we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

## <a name="configuring-hello-staging-area"></a><span data-ttu-id="d5f8d-192">Configurando a área de preparação de saudação</span><span class="sxs-lookup"><span data-stu-id="d5f8d-192">Configuring hello staging Area</span></span>
<span data-ttu-id="d5f8d-193">Hello Azure Backup agent em execução no servidor DPM Olá precisa de armazenamento temporário para os dados restaurados da nuvem de saudação (área de preparação local).</span><span class="sxs-lookup"><span data-stu-id="d5f8d-193">hello Azure Backup agent running on hello DPM server needs temporary storage for data restored from hello cloud (local staging area).</span></span> <span data-ttu-id="d5f8d-194">Configurar área de preparação de saudação usando Olá [conjunto DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet e hello ```-StagingAreaPath``` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-194">Configure hello staging area using hello [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and hello ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="d5f8d-195">O exemplo hello acima, área de preparação de saudação será definida muito*C:\StagingArea* no objeto do PowerShell Olá ```$setting```.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-195">In hello example above, hello staging area will be set too*C:\StagingArea* in hello PowerShell object ```$setting```.</span></span> <span data-ttu-id="d5f8d-196">Certifique-se de que Olá a pasta especificada já existe, ou então a confirmação final Olá das configurações de assinatura Olá falhará.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-196">Ensure that hello specified folder already exists, or else hello final commit of hello subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="d5f8d-197">Configurações de criptografia</span><span class="sxs-lookup"><span data-stu-id="d5f8d-197">Encryption settings</span></span>
<span data-ttu-id="d5f8d-198">Olá enviados os dados de backup tooAzure Backup é tooprotect criptografados Olá confidencialidade de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-198">hello backup data sent tooAzure Backup is encrypted tooprotect hello confidentiality of hello data.</span></span> <span data-ttu-id="d5f8d-199">senha de criptografia de saudação é dados de saudação toodecrypt senha"Olá" no tempo de saudação da restauração.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-199">hello encryption passphrase is hello "password" toodecrypt hello data at hello time of restore.</span></span> <span data-ttu-id="d5f8d-200">É importante tookeep este seguro de informações e seguro depois que ela é definida.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-200">It is important tookeep this information safe and secure once it is set.</span></span>

<span data-ttu-id="d5f8d-201">Exemplo hello abaixo, comando primeiro Olá converte a cadeia de caracteres de saudação ```passphrase123456789``` tooa segura cadeia de caracteres e atribui Olá seguro toohello variável string denominada ```$Passphrase```.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-201">In hello example below, hello first command converts hello string ```passphrase123456789``` tooa secure string and assigns hello secure string toohello variable named ```$Passphrase```.</span></span> <span data-ttu-id="d5f8d-202">Olá segundo comando define a cadeia de caracteres segura Olá ```$Passphrase``` como senha Olá para criptografia de backups.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-202">hello second command sets hello secure string in ```$Passphrase``` as hello password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> <span data-ttu-id="d5f8d-203">Manter informações de senha Olá seguros e protegidos depois que ela é definida.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-203">Keep hello passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="d5f8d-204">Você não será capaz de toorestore a dados do Azure sem essa frase secreta.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-204">You will not be able toorestore data from Azure without this passphrase.</span></span>
>
>

<span data-ttu-id="d5f8d-205">Neste ponto, você deveria ter feito todas as toohello de alterações de saudação necessária ```$setting``` objeto.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-205">At this point, you should have made all hello required changes toohello ```$setting``` object.</span></span> <span data-ttu-id="d5f8d-206">Lembre-se as alterações de saudação do toocommit.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-206">Remember toocommit hello changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-tooazure-backup"></a><span data-ttu-id="d5f8d-207">Proteger dados tooAzure Backup</span><span class="sxs-lookup"><span data-stu-id="d5f8d-207">Protect data tooAzure Backup</span></span>
<span data-ttu-id="d5f8d-208">Nesta seção, você adicionará um tooDPM do servidor de produção e, em seguida, proteger o armazenamento do DPM toolocal Olá dados e, em seguida, tooAzure Backup.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-208">In this section, you will add a production server tooDPM and then protect hello data toolocal DPM storage and then tooAzure Backup.</span></span> <span data-ttu-id="d5f8d-209">Exemplos de hello, demonstraremos como tooback backup de arquivos e pastas.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-209">In hello examples, we will demonstrate how tooback up files and folders.</span></span> <span data-ttu-id="d5f8d-210">Olá lógica pode facilmente ser estendido toobackup qualquer fonte de dados com suporte ao DPM.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-210">hello logic can easily be extended toobackup any DPM-supported data source.</span></span> <span data-ttu-id="d5f8d-211">Todos os backups do DPM são regidos por um GP (Grupo de Proteção) com quatro partes:</span><span class="sxs-lookup"><span data-stu-id="d5f8d-211">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="d5f8d-212">**Os membros do grupo** é uma lista de todos os objetos protegíveis de saudação (também conhecido como *fontes de dados* no DPM) que você deseja tooprotect em Olá mesmo grupo de proteção.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-212">**Group members** is a list of all hello protectable objects (also known as *Datasources* in DPM) that you want tooprotect in hello same protection group.</span></span> <span data-ttu-id="d5f8d-213">Por exemplo, convém tooprotect produção VMs em um grupo de proteção e bancos de dados do SQL Server em outro grupo de proteção como eles podem ter diferentes requisitos de backup.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-213">For example, you may want tooprotect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="d5f8d-214">Antes de fazer backup de qualquer fonte de dados em um servidor de produção, você precisa toomake o hello-se de que o agente do DPM está instalado no servidor de saudação e é gerenciado pelo DPM.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-214">Before you can back up any datasource on a production server you need toomake sure hello DPM Agent is installed on hello server and is managed by DPM.</span></span> <span data-ttu-id="d5f8d-215">Siga as etapas de saudação para [instalando Olá agente do DPM](https://technet.microsoft.com/library/bb870935.aspx) e vinculá-lo toohello apropriado do servidor DPM.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-215">Follow hello steps for [installing hello DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it toohello appropriate DPM Server.</span></span>
2. <span data-ttu-id="d5f8d-216">**Método de proteção de dados** Especifica os locais de backup Olá destino - fita, disco e nuvem.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-216">**Data protection method** specifies hello target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="d5f8d-217">Em nosso exemplo, protege dados toohello local em disco e toohello na nuvem.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-217">In our example we will protect data toohello local disk and toohello cloud.</span></span>
3. <span data-ttu-id="d5f8d-218">Um **agendamento de backup** que especifica quando backups necessário toobe feito e frequência hello dados devem ser sincronizados entre hello servidor DPM e o servidor de produção de hello.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-218">A **backup schedule** that specifies when backups need toobe taken and how often hello data should be synchronized between hello DPM Server and hello production server.</span></span>
4. <span data-ttu-id="d5f8d-219">Um **agenda de retenção** que especifica quanto tempo os pontos de recuperação de saudação do tooretain no Azure.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-219">A **retention schedule** that specifies how long tooretain hello recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="d5f8d-220">Criando um grupo de proteção</span><span class="sxs-lookup"><span data-stu-id="d5f8d-220">Creating a protection group</span></span>
<span data-ttu-id="d5f8d-221">Comece criando um novo grupo de proteção usando Olá [DPMProtectionGroup novo](https://technet.microsoft.com/library/hh881722) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-221">Start by creating a new Protection Group using hello [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="d5f8d-222">Olá acima cmdlet criará um grupo de proteção chamada *ProtectGroup01*.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-222">hello above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="d5f8d-223">Um grupo de proteção também pode ser modificado posteriormente tooadd toohello backup nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-223">An existing protection group can also be modified later tooadd backup toohello Azure cloud.</span></span> <span data-ttu-id="d5f8d-224">No entanto, toomake alterações toohello grupo de proteção - novo ou existente - precisamos tooget um identificador em uma *modificável* objeto usando Olá [DPMModifiableProtectionGroup Get](https://technet.microsoft.com/library/hh881713) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-224">However, toomake any changes toohello Protection Group - new or existing - we need tooget a handle on a *modifiable* object using hello [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-toohello-protection-group"></a><span data-ttu-id="d5f8d-225">Adicionar membros de grupo toohello grupo de proteção</span><span class="sxs-lookup"><span data-stu-id="d5f8d-225">Adding group members toohello Protection Group</span></span>
<span data-ttu-id="d5f8d-226">Cada agente do DPM sabe lista Olá de fontes de dados no servidor de saudação que ele está instalado.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-226">Each DPM Agent knows hello list of datasources on hello server that it is installed on.</span></span> <span data-ttu-id="d5f8d-227">tooadd toohello uma fonte de dados grupo de proteção, Olá toofirst de necessidades de agente do DPM enviar uma lista de servidor DPM de toohello back Olá fontes de dados.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-227">tooadd a datasource toohello Protection Group, hello DPM Agent needs toofirst send a list of hello datasources back toohello DPM server.</span></span> <span data-ttu-id="d5f8d-228">Uma ou mais fontes de dados forem selecionadas e adicionadas toohello grupo de proteção.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-228">One or more datasources are then selected and added toohello Protection Group.</span></span> <span data-ttu-id="d5f8d-229">etapas do PowerShell Olá necessárias tooachieve isso são:</span><span class="sxs-lookup"><span data-stu-id="d5f8d-229">hello PowerShell steps needed tooachieve this are:</span></span>

1. <span data-ttu-id="d5f8d-230">Obter uma lista de todos os servidores gerenciados pelo DPM por meio de saudação agente do DPM.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-230">Fetch a list of all servers managed by DPM through hello DPM Agent.</span></span>
2. <span data-ttu-id="d5f8d-231">Escolher um servidor específico.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-231">Choose a specific server.</span></span>
3. <span data-ttu-id="d5f8d-232">Obter uma lista de todas as fontes de dados no servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-232">Fetch a list of all datasources on hello server.</span></span>
4. <span data-ttu-id="d5f8d-233">Escolha uma ou mais fontes de dados e adicioná-los toohello grupo de proteção</span><span class="sxs-lookup"><span data-stu-id="d5f8d-233">Choose one or more datasources and add them toohello Protection Group</span></span>

<span data-ttu-id="d5f8d-234">Olá lista de servidores nos quais Olá agente do DPM está instalado e está sendo gerenciado pelo servidor DPM da saudação é adquirida com hello [DPMProductionServer Get](https://technet.microsoft.com/library/hh881600) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-234">hello list of servers on which hello DPM Agent is installed and is being managed by hello DPM Server is acquired with hello [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="d5f8d-235">Neste exemplo, filtraremos e configuraremos apenas o PS com o nome *productionserver01* para o backup.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-235">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

<span data-ttu-id="d5f8d-236">Agora obter lista de saudação de fontes de dados em ```$server``` usando Olá [DPMDatasource Get](https://technet.microsoft.com/library/hh881605) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-236">Now fetch hello list of datasources on ```$server``` using hello [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="d5f8d-237">Neste exemplo nós estamos filtrando para volume hello * unidade d:\* que desejamos tooconfigure para backup.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-237">In this example we are filtering for hello volume *D:\* that we want tooconfigure for backup.</span></span> <span data-ttu-id="d5f8d-238">Esta fonte de dados é adicionada toohello grupo de proteção usando Olá [DPMChildDatasource adicionar](https://technet.microsoft.com/library/hh881732) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-238">This datasource is then added toohello Protection Group using hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="d5f8d-239">Lembre-se de saudação toouse *modificável* objeto do grupo de proteção ```$MPG``` toomake adições de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-239">Remember toouse hello *modifiable* protection group object ```$MPG``` toomake hello additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="d5f8d-240">Repita essa etapa, quantas vezes forem necessárias, até que você adicionou todos os Olá escolhido o grupo de proteção toohello fontes de dados.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-240">Repeat this step as many times as required, until you have added all hello chosen datasources toohello protection group.</span></span> <span data-ttu-id="d5f8d-241">Você também pode iniciar com apenas uma fonte de dados e fluxo de trabalho Olá completa para a criação de grupo de proteção de saudação e posteriormente adicionar mais fontes de dados toohello grupo de proteção.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-241">You can also start with just one datasource, and complete hello workflow for creating hello Protection Group, and at a later point add more datasources toohello Protection Group.</span></span>

### <a name="selecting-hello-data-protection-method"></a><span data-ttu-id="d5f8d-242">Selecionar método de proteção de dados hello</span><span class="sxs-lookup"><span data-stu-id="d5f8d-242">Selecting hello data protection method</span></span>
<span data-ttu-id="d5f8d-243">Depois de fontes de dados Olá adicionou toohello grupo de proteção, Olá próxima etapa é toospecify o método de proteção de saudação usando Olá [DPMProtectionType conjunto](https://technet.microsoft.com/library/hh881725) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-243">Once hello datasources have been added toohello Protection Group, hello next step is toospecify hello protection method using hello [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="d5f8d-244">Neste exemplo, Olá grupo de proteção está configurado para o disco local e backup na nuvem.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-244">In this example, hello Protection Group is setup for local disk and cloud backup.</span></span> <span data-ttu-id="d5f8d-245">Você também precisa toospecify Olá a fonte de dados que você deseja toocloud tooprotect usando Olá [DPMChildDatasource adicionar](https://technet.microsoft.com/library/hh881732.aspx) cmdlet com - sinalizador Online.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-245">You also need toospecify hello datasource that you want tooprotect toocloud using hello [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-hello-retention-range"></a><span data-ttu-id="d5f8d-246">Definir o período de retenção de saudação</span><span class="sxs-lookup"><span data-stu-id="d5f8d-246">Setting hello retention range</span></span>
<span data-ttu-id="d5f8d-247">Definir retenção Olá Olá backup pontos de usando Olá [DPMPolicyObjective conjunto](https://technet.microsoft.com/library/hh881762) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-247">Set hello retention for hello backup points using hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="d5f8d-248">Enquanto a retenção de saudação ímpar tooset pode parecer antes de agendamento de backup Olá tiver sido definido, usando Olá ```Set-DPMPolicyObjective``` cmdlet automaticamente define uma agenda de backup padrão que pode ser modificada.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-248">While it might seem odd tooset hello retention before hello backup schedule has been defined, using hello ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="d5f8d-249">É sempre agendamento de backup possível tooset Olá primeiro e Olá a política de retenção depois.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-249">It is always possible tooset hello backup schedule first and hello retention policy after.</span></span>

<span data-ttu-id="d5f8d-250">O exemplo hello abaixo, Olá define parâmetros de retenção Olá para backups em disco.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-250">In hello example below, hello cmdlet sets hello retention parameters for disk backups.</span></span> <span data-ttu-id="d5f8d-251">Isso manterá backups para 10 dias e os dados de sincronização entre servidores de produção de hello e DPM Olá a cada 6 horas.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-251">This will retain backups for 10 days, and sync data every 6 hours between hello production server and hello DPM server.</span></span> <span data-ttu-id="d5f8d-252">Olá ```SynchronizationFrequencyMinutes``` não define quantas vezes um ponto de backup é criado, mas como dados geralmente são servidor DPM toohello copiado.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-252">hello ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied toohello DPM server.</span></span>  <span data-ttu-id="d5f8d-253">Essa configuração impede que os backups fiquem grandes demais.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-253">This setting prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="d5f8d-254">Intervalos de retenção de saudação para backups vai tooAzure (DPM refere-se toothem como backups Online) podem ser configurados para [usando um esquema de avô-pai-filho (GFS) de retenção de longo prazo](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="d5f8d-254">For backups going tooAzure (DPM refers toothem as Online backups) hello retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="d5f8d-255">Ou seja, você pode definir uma política de retenção combinada que envolva políticas de retenção diárias, semanais, mensais e anuais.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-255">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="d5f8d-256">Neste exemplo, criamos uma matriz que representa o esquema de retenção complexas Olá que queremos e, em seguida, configurar o período de retenção hello usando Olá [DPMPolicyObjective conjunto](https://technet.microsoft.com/library/hh881762) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-256">In this example, we create an array representing hello complex retention scheme that we want, and then configure hello retention range using hello [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-hello-backup-schedule"></a><span data-ttu-id="d5f8d-257">Agendamento de backup de saudação do conjunto</span><span class="sxs-lookup"><span data-stu-id="d5f8d-257">Set hello backup schedule</span></span>
<span data-ttu-id="d5f8d-258">O DPM define uma agenda de backup padrão automaticamente se você especificar o objetivo de proteção de saudação usando Olá ```Set-DPMPolicyObjective``` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-258">DPM sets a default backup schedule automatically if you specify hello protection objective using hello ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="d5f8d-259">os agendamentos padrão Olá toochange, use Olá [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet seguido por Olá [DPMPolicySchedule conjunto](https://technet.microsoft.com/library/hh881723) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-259">toochange hello default schedules, use hello [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by hello [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="d5f8d-260">Em hello, o exemplo acima ```$onlineSch``` é uma matriz que contém a agenda de proteção online existente Olá para Olá grupo de proteção no esquema GFS Olá com quatro elementos:</span><span class="sxs-lookup"><span data-stu-id="d5f8d-260">In hello above example, ```$onlineSch``` is an array with four elements that contains hello existing online protection schedule for hello Protection Group in hello GFS scheme:</span></span>

1. <span data-ttu-id="d5f8d-261">```$onlineSch[0]```contém a agenda diária Olá</span><span class="sxs-lookup"><span data-stu-id="d5f8d-261">```$onlineSch[0]``` contains hello daily schedule</span></span>
2. <span data-ttu-id="d5f8d-262">```$onlineSch[1]```contém a agenda semanal Olá</span><span class="sxs-lookup"><span data-stu-id="d5f8d-262">```$onlineSch[1]``` contains hello weekly schedule</span></span>
3. <span data-ttu-id="d5f8d-263">```$onlineSch[2]```contém o agendamento mensal Olá</span><span class="sxs-lookup"><span data-stu-id="d5f8d-263">```$onlineSch[2]``` contains hello monthly schedule</span></span>
4. <span data-ttu-id="d5f8d-264">```$onlineSch[3]```contém a agenda de saudação anual</span><span class="sxs-lookup"><span data-stu-id="d5f8d-264">```$onlineSch[3]``` contains hello yearly schedule</span></span>

<span data-ttu-id="d5f8d-265">Portanto, se você precisar agenda semanal do toomodify hello, você precisa toorefer toohello ```$onlineSch[1]```.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-265">So if you need toomodify hello weekly schedule, you need toorefer toohello ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="d5f8d-266">Backup inicial</span><span class="sxs-lookup"><span data-stu-id="d5f8d-266">Initial backup</span></span>
<span data-ttu-id="d5f8d-267">Ao fazer backup de uma fonte de dados para Olá primeira vez, o DPM necessidades cria réplica inicial que cria uma cópia completa de saudação toobe de fonte de dados protegido no volume de réplica do DPM.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-267">When backing up a datasource for hello first time, DPM needs creates initial replica that creates a full copy of hello datasource toobe protected on DPM replica volume.</span></span> <span data-ttu-id="d5f8d-268">Essa atividade pode ser agendada durante um período específico ou pode ser disparada de manualmente, usando Olá [conjunto DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet com o parâmetro hello ```-NOW```.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-268">This activity can either be scheduled for a specific time, or can be triggered manually, using hello [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with hello parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-hello-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="d5f8d-269">Alterando o tamanho de saudação de réplica do DPM e o volume de ponto de recuperação</span><span class="sxs-lookup"><span data-stu-id="d5f8d-269">Changing hello size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="d5f8d-270">Você também pode alterar o tamanho de saudação do volume de réplica do DPM e a cópia de sombra de volume usando [DPMDatasourceDiskAllocation conjunto](https://technet.microsoft.com/library/hh881618.aspx) cmdlet como no exemplo a seguir de saudação: Get-DatasourceDiskAllocation - Datasource $DS Set-DatasourceDiskAllocation - Datasource $DS - ProtectionGroup $MPG-manual - ReplicaArea (2 gb) - ShadowCopyArea (2 gb)</span><span class="sxs-lookup"><span data-stu-id="d5f8d-270">You can also change hello size of DPM Replica volume and Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in hello following example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-hello-changes-toohello-protection-group"></a><span data-ttu-id="d5f8d-271">Confirmar Olá altera toohello grupo de proteção</span><span class="sxs-lookup"><span data-stu-id="d5f8d-271">Committing hello changes toohello Protection Group</span></span>
<span data-ttu-id="d5f8d-272">Finalmente, alterações de saudação precisam toobe confirmada antes do DPM pode fazer backup de saudação por nova configuração de grupo de proteção hello.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-272">Finally, hello changes need toobe committed before DPM can take hello backup per hello new Protection Group configuration.</span></span> <span data-ttu-id="d5f8d-273">Isso pode ser feito usando Olá [DPMProtectionGroup conjunto](https://technet.microsoft.com/library/hh881758) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-273">This can be achieved using hello [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-hello-backup-points"></a><span data-ttu-id="d5f8d-274">Exibir pontos de backup Olá</span><span class="sxs-lookup"><span data-stu-id="d5f8d-274">View hello backup points</span></span>
<span data-ttu-id="d5f8d-275">Você pode usar o hello [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) tooget cmdlet uma lista de todos os pontos de recuperação para uma fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-275">You can use hello [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet tooget a list of all recovery points for a datasource.</span></span> <span data-ttu-id="d5f8d-276">Neste exemplo, iremos:</span><span class="sxs-lookup"><span data-stu-id="d5f8d-276">In this example, we will:</span></span>

* <span data-ttu-id="d5f8d-277">busca todas Olá páginas no servidor DPM hello e armazenados em uma matriz```$PG```</span><span class="sxs-lookup"><span data-stu-id="d5f8d-277">fetch all hello PGs on hello DPM server and stored in an array ```$PG```</span></span>
* <span data-ttu-id="d5f8d-278">obter Olá fontes de dados correspondente toohello```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="d5f8d-278">get hello datasources corresponding toohello ```$PG[0]```</span></span>
* <span data-ttu-id="d5f8d-279">obter todos os pontos de recuperação Olá para uma fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-279">get all hello recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="d5f8d-280">Restaurar dados protegidos no Azure</span><span class="sxs-lookup"><span data-stu-id="d5f8d-280">Restore data protected on Azure</span></span>
<span data-ttu-id="d5f8d-281">A restauração de dados é uma combinação de um objeto ```RecoverableItem``` e um objeto ```RecoveryOption```.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-281">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="d5f8d-282">Na seção anterior do hello, nós temos uma lista de pontos de backup Olá para uma fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-282">In hello previous section, we got a list of hello backup points for a datasource.</span></span>

<span data-ttu-id="d5f8d-283">O exemplo hello abaixo, demonstraremos como máquina virtual de toorestore um Hyper-V do Backup do Azure por pontos de backup combinando com hello de destino para recuperação.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-283">In hello example below, we demonstrate how toorestore a Hyper-V virtual machine from Azure Backup by combining backup points with hello target for recovery.</span></span> <span data-ttu-id="d5f8d-284">Este exemplo inclui:</span><span class="sxs-lookup"><span data-stu-id="d5f8d-284">This example includes:</span></span>

* <span data-ttu-id="d5f8d-285">Criando uma opção de recuperação usando Olá [DPMRecoveryOption novo](https://technet.microsoft.com/library/hh881592) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-285">Creating a recovery option using hello  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="d5f8d-286">Matriz de Olá busca de pontos de backup usando Olá ```Get-DPMRecoveryPoint``` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-286">Fetching hello array of backup points using hello ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="d5f8d-287">Escolhendo um toorestore de ponto de backup do.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-287">Choosing a backup point toorestore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="d5f8d-288">comandos de saudação podem ser facilmente estendidos para qualquer tipo de fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="d5f8d-288">hello commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5f8d-289">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d5f8d-289">Next steps</span></span>
* <span data-ttu-id="d5f8d-290">Para obter mais informações sobre o DPM tooAzure Backup consulte [Introdução tooDPM Backup](backup-azure-dpm-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="d5f8d-290">For more information about DPM tooAzure Backup see [Introduction tooDPM Backup](backup-azure-dpm-introduction.md)</span></span>
