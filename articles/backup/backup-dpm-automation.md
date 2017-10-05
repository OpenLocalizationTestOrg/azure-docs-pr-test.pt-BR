---
title: 'Backup do Azure: Usar o PowerShell para fazer backup de cargas de trabalho de DPM | Microsoft Docs'
description: Saiba como implantar e gerenciar o backup do Azure para o Data Protection Manager (DPM) usando o PowerShell
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
ms.openlocfilehash: 2e3b4a094511a59cfa02917efc2e3e053840af0c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-and-manage-backup-to-azure-for-data-protection-manager-dpm-servers-using-powershell"></a><span data-ttu-id="e6d11-103">Implantar e gerenciar o backup do Azure para servidores do Data Protection Manager (DPM) usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="e6d11-103">Deploy and manage backup to Azure for Data Protection Manager (DPM) servers using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e6d11-104">ARM</span><span class="sxs-lookup"><span data-stu-id="e6d11-104">ARM</span></span>](backup-dpm-automation.md)
> * [<span data-ttu-id="e6d11-105">Clássico</span><span class="sxs-lookup"><span data-stu-id="e6d11-105">Classic</span></span>](backup-dpm-automation-classic.md)
>
>

<span data-ttu-id="e6d11-106">Este artigo mostra como usar o Azure PowerShell para configurar o Backup do Azure em um servidor DPM e para gerenciar backups e recuperações.</span><span class="sxs-lookup"><span data-stu-id="e6d11-106">This article shows you how to use PowerShell to setup Azure Backup on a DPM server, and to manage backup and recovery.</span></span>

## <a name="setting-up-the-powershell-environment"></a><span data-ttu-id="e6d11-107">Configurando o ambiente do PowerShell</span><span class="sxs-lookup"><span data-stu-id="e6d11-107">Setting up the PowerShell environment</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="e6d11-108">Antes de usar o PowerShell para gerenciar backups do Data Protection Manager para o Azure, você precisará ter o ambiente certo no PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e6d11-108">Before you can use PowerShell to manage backups from Data Protection Manager to Azure, you need to have the right environment in PowerShell.</span></span> <span data-ttu-id="e6d11-109">No início da sessão do PowerShell, certifique-se de executar o comando a seguir para importar os módulos corretos e permitir que você faça referência corretamente aos cmdlets do DPM:</span><span class="sxs-lookup"><span data-stu-id="e6d11-109">At the start of the PowerShell session, ensure that you run the following command to import the right modules and allow you to correctly reference the DPM cmdlets:</span></span>

```
PS C:> & "C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin\DpmCliInitScript.ps1"

Welcome to the DPM Management Shell!

Full list of cmdlets: Get-Command
Only DPM cmdlets: Get-DPMCommand
Get general help: help
Get help for a cmdlet: help <cmdlet-name> or <cmdlet-name> -?
Get definition of a cmdlet: Get-Command <cmdlet-name> -Syntax
Sample DPM scripts: Get-DPMSampleScript
```

## <a name="setup-and-registration"></a><span data-ttu-id="e6d11-110">Configuração e registro</span><span class="sxs-lookup"><span data-stu-id="e6d11-110">Setup and Registration</span></span>
<span data-ttu-id="e6d11-111">Para começar:</span><span class="sxs-lookup"><span data-stu-id="e6d11-111">To begin:</span></span>

1. <span data-ttu-id="e6d11-112">[Baixe o PowerShell mais recente](https://github.com/Azure/azure-powershell/releases) (a versão mínima exigida é: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="e6d11-112">[Download latest PowerShell](https://github.com/Azure/azure-powershell/releases) (minimum version required is: 1.0.0)</span></span>
2. <span data-ttu-id="e6d11-113">Habilite os commandlets do Backup do Azure alternando para o modo *AzureResourceManager* usando o commandlet **Switch-AzureMode** :</span><span class="sxs-lookup"><span data-stu-id="e6d11-113">Enable the Azure Backup commandlets by switching to *AzureResourceManager* mode by using the **Switch-AzureMode** commandlet:</span></span>

```
PS C:\> Switch-AzureMode AzureResourceManager
```

<span data-ttu-id="e6d11-114">As seguintes tarefas de configuração e de registro podem ser automatizadas com o PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e6d11-114">The following setup and registration tasks can be automated with PowerShell:</span></span>

* <span data-ttu-id="e6d11-115">Criar um cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="e6d11-115">Create a Recovery Services vault</span></span>
* <span data-ttu-id="e6d11-116">Instalando o agente de Backup do Azure</span><span class="sxs-lookup"><span data-stu-id="e6d11-116">Installing the Azure Backup agent</span></span>
* <span data-ttu-id="e6d11-117">Registrando-se no serviço de Backup do Azure</span><span class="sxs-lookup"><span data-stu-id="e6d11-117">Registering with the Azure Backup service</span></span>
* <span data-ttu-id="e6d11-118">Configurações de rede</span><span class="sxs-lookup"><span data-stu-id="e6d11-118">Networking settings</span></span>
* <span data-ttu-id="e6d11-119">Configurações de criptografia</span><span class="sxs-lookup"><span data-stu-id="e6d11-119">Encryption settings</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="e6d11-120">Criar um cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="e6d11-120">Create a recovery services vault</span></span>
<span data-ttu-id="e6d11-121">As etapas a seguir orientarão você durante a criação de um cofre dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="e6d11-121">The following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="e6d11-122">Um cofre dos Serviços de Recuperação é diferente de um cofre de Backup.</span><span class="sxs-lookup"><span data-stu-id="e6d11-122">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="e6d11-123">Se você estiver usando um Backup do Azure pela primeira vez, deverá usar o cmdlet **Register-AzureRMResourceProvider** para registrar o provedor do Serviço de Recuperação do Azure com sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="e6d11-123">If you are using Azure Backup for the first time, you must use the **Register-AzureRMResourceProvider** cmdlet to register the Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="e6d11-124">O cofre dos Serviços de Recuperação é um recurso do ARM e, portanto, você precisará colocá-lo em um Grupo de Recursos.</span><span class="sxs-lookup"><span data-stu-id="e6d11-124">The Recovery Services vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="e6d11-125">Você pode usar um grupo de recursos existente ou criar um novo.</span><span class="sxs-lookup"><span data-stu-id="e6d11-125">You can use an existing resource group, or create a new one.</span></span> <span data-ttu-id="e6d11-126">Ao criar um novo grupo de recursos, especifique o nome e o local para o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e6d11-126">When creating a new resource group, specify the name and location for the resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "West US"
    ```
3. <span data-ttu-id="e6d11-127">Use o cmdlet **New-AzureRmRecoveryServicesVault** para criar um novo cofre.</span><span class="sxs-lookup"><span data-stu-id="e6d11-127">Use the **New-AzureRmRecoveryServicesVault** cmdlet to create a new vault.</span></span> <span data-ttu-id="e6d11-128">Lembre-se de especificar o mesmo local para o cofre usado para o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e6d11-128">Be sure to specify the same location for the vault as was used for the resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "West US"
    ```
4. <span data-ttu-id="e6d11-129">Especifique o tipo de redundância de armazenamento a usar. Você pode usar o [Armazenamento com Redundância Local (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) ou o [Armazenamento com Redundância Geográfica (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="e6d11-129">Specify the type of storage redundancy to use; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="e6d11-130">O exemplo a seguir mostra que a opção BackupStorageRedundancy para o testVault está definida como GeoRedundant.</span><span class="sxs-lookup"><span data-stu-id="e6d11-130">The following example shows the -BackupStorageRedundancy option for testVault is set to GeoRedundant.</span></span>

   > [!TIP]
   > <span data-ttu-id="e6d11-131">Muitos cmdlets do Backup do Azure exigem o objeto do cofre dos Serviços de Recuperação como entrada.</span><span class="sxs-lookup"><span data-stu-id="e6d11-131">Many Azure Backup cmdlets require the Recovery Services vault object as an input.</span></span> <span data-ttu-id="e6d11-132">Por esse motivo, pode ser útil armazenar o objeto do cofre dos Serviços de Recuperação de backup em uma variável.</span><span class="sxs-lookup"><span data-stu-id="e6d11-132">For this reason, it is convenient to store the Backup Recovery Services vault object in a variable.</span></span>
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-the-vaults-in-a-subscription"></a><span data-ttu-id="e6d11-133">Exibir os cofres em uma assinatura</span><span class="sxs-lookup"><span data-stu-id="e6d11-133">View the vaults in a subscription</span></span>
<span data-ttu-id="e6d11-134">Use **Get-AzureRmRecoveryServicesVault** para exibir a lista de todos os cofres da assinatura atual.</span><span class="sxs-lookup"><span data-stu-id="e6d11-134">Use **Get-AzureRmRecoveryServicesVault** to view the list of all vaults in the current subscription.</span></span> <span data-ttu-id="e6d11-135">Você pode usar esse comando para verificar se um novo cofre foi criado ou para ver quais cofres estão disponíveis na assinatura.</span><span class="sxs-lookup"><span data-stu-id="e6d11-135">You can use this command to check that a new  vault was created, or to see what vaults are available in the subscription.</span></span>

<span data-ttu-id="e6d11-136">Execute o comando Get-AzureRmRecoveryServicesVault e todos os cofres na assinatura serão listados.</span><span class="sxs-lookup"><span data-stu-id="e6d11-136">Run the command, Get-AzureRmRecoveryServicesVault, and all vaults in the subscription are listed.</span></span>

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


## <a name="installing-the-azure-backup-agent-on-a-dpm-server"></a><span data-ttu-id="e6d11-137">Instalando o agente de Backup do Azure em um Servidor de DPM</span><span class="sxs-lookup"><span data-stu-id="e6d11-137">Installing the Azure Backup agent on a DPM Server</span></span>
<span data-ttu-id="e6d11-138">Antes de instalar o agente de Backup do Azure, você precisa ter o instalador baixado, já no Windows Server.</span><span class="sxs-lookup"><span data-stu-id="e6d11-138">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span></span> <span data-ttu-id="e6d11-139">Você pode obter a última versão do instalador no [Centro de Download da Microsoft](http://aka.ms/azurebackup_agent) ou na página Painel do cofre dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="e6d11-139">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the Recovery Services vault's Dashboard page.</span></span> <span data-ttu-id="e6d11-140">Salve o instalador em um local de fácil acesso, como *C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="e6d11-140">Save the installer to an easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="e6d11-141">Para instalar o agente, execute o seguinte comando em um console do PowerShell com privilégios elevados **no servidor do DPM**:</span><span class="sxs-lookup"><span data-stu-id="e6d11-141">To install the agent, run the following command in an elevated PowerShell console **on the DPM server**:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="e6d11-142">Isso instala o agente com todas as opções padrão.</span><span class="sxs-lookup"><span data-stu-id="e6d11-142">This installs the agent with all the default options.</span></span> <span data-ttu-id="e6d11-143">A instalação demora alguns minutos, em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="e6d11-143">The installation takes a few minutes in the background.</span></span> <span data-ttu-id="e6d11-144">Se você não especificar a opção */nu* , a janela do **Windows Update** será aberta ao fim da instalação para verificar se há atualizações.</span><span class="sxs-lookup"><span data-stu-id="e6d11-144">If you do not specify the */nu* option the **Windows Update** window opens at the end of the installation to check for any updates.</span></span>

<span data-ttu-id="e6d11-145">O agente será mostrado na lista de programas instalados.</span><span class="sxs-lookup"><span data-stu-id="e6d11-145">The agent shows up in the list of installed programs.</span></span> <span data-ttu-id="e6d11-146">Para ver a lista de programas instalados, vá para **Painel de controle** > **Programas** > **Programas e recursos**.</span><span class="sxs-lookup"><span data-stu-id="e6d11-146">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agente instalado](./media/backup-dpm-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="e6d11-148">Opções de instalação</span><span class="sxs-lookup"><span data-stu-id="e6d11-148">Installation options</span></span>
<span data-ttu-id="e6d11-149">Para ver todas as opções disponíveis por meio da linha de comando, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="e6d11-149">To see all the options available via the commandline, use the following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="e6d11-150">As opções disponíveis incluem:</span><span class="sxs-lookup"><span data-stu-id="e6d11-150">The available options include:</span></span>

| <span data-ttu-id="e6d11-151">Opção</span><span class="sxs-lookup"><span data-stu-id="e6d11-151">Option</span></span> | <span data-ttu-id="e6d11-152">Detalhes</span><span class="sxs-lookup"><span data-stu-id="e6d11-152">Details</span></span> | <span data-ttu-id="e6d11-153">Padrão</span><span class="sxs-lookup"><span data-stu-id="e6d11-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e6d11-154">/q</span><span class="sxs-lookup"><span data-stu-id="e6d11-154">/q</span></span> |<span data-ttu-id="e6d11-155">Instalação silenciosa</span><span class="sxs-lookup"><span data-stu-id="e6d11-155">Quiet installation</span></span> |- |
| <span data-ttu-id="e6d11-156">/p:"local"</span><span class="sxs-lookup"><span data-stu-id="e6d11-156">/p:"location"</span></span> |<span data-ttu-id="e6d11-157">Caminho para a pasta de instalação para o agente de Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="e6d11-157">Path to the installation folder for the Azure Backup agent.</span></span> |<span data-ttu-id="e6d11-158">C:\Arquivos de Programas\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="e6d11-158">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="e6d11-159">/s:"local"</span><span class="sxs-lookup"><span data-stu-id="e6d11-159">/s:"location"</span></span> |<span data-ttu-id="e6d11-160">Caminho para a pasta de cache para o agente de Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="e6d11-160">Path to the cache folder for the Azure Backup agent.</span></span> |<span data-ttu-id="e6d11-161">C:\Arquivos de Programas\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="e6d11-161">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="e6d11-162">/m</span><span class="sxs-lookup"><span data-stu-id="e6d11-162">/m</span></span> |<span data-ttu-id="e6d11-163">Aceitar o Microsoft Update</span><span class="sxs-lookup"><span data-stu-id="e6d11-163">Opt-in to Microsoft Update</span></span> |- |
| <span data-ttu-id="e6d11-164">/nu</span><span class="sxs-lookup"><span data-stu-id="e6d11-164">/nu</span></span> |<span data-ttu-id="e6d11-165">Não verificar se há atualizações após a conclusão da instalação</span><span class="sxs-lookup"><span data-stu-id="e6d11-165">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="e6d11-166">/d</span><span class="sxs-lookup"><span data-stu-id="e6d11-166">/d</span></span> |<span data-ttu-id="e6d11-167">Desinstala o agente dos Serviços de Recuperação do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="e6d11-167">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="e6d11-168">/ph</span><span class="sxs-lookup"><span data-stu-id="e6d11-168">/ph</span></span> |<span data-ttu-id="e6d11-169">Endereço do host do proxy</span><span class="sxs-lookup"><span data-stu-id="e6d11-169">Proxy Host Address</span></span> |- |
| <span data-ttu-id="e6d11-170">/po</span><span class="sxs-lookup"><span data-stu-id="e6d11-170">/po</span></span> |<span data-ttu-id="e6d11-171">Número da porta do host do proxy</span><span class="sxs-lookup"><span data-stu-id="e6d11-171">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="e6d11-172">/pu</span><span class="sxs-lookup"><span data-stu-id="e6d11-172">/pu</span></span> |<span data-ttu-id="e6d11-173">UserName do host do proxy</span><span class="sxs-lookup"><span data-stu-id="e6d11-173">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="e6d11-174">/pw</span><span class="sxs-lookup"><span data-stu-id="e6d11-174">/pw</span></span> |<span data-ttu-id="e6d11-175">Senha do proxy</span><span class="sxs-lookup"><span data-stu-id="e6d11-175">Proxy Password</span></span> |- |

## <a name="registering-dpm-to-a-recovery-services-vault"></a><span data-ttu-id="e6d11-176">Registrar o DPM para um Cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="e6d11-176">Registering DPM to a Recovery Services Vault</span></span>
<span data-ttu-id="e6d11-177">Depois de criar o cofre dos Serviços de Recuperação, baixe o agente mais recente e as credenciais do cofre e armazene-os em um local conveniente como C:\Downloads.</span><span class="sxs-lookup"><span data-stu-id="e6d11-177">After you created the Recovery Services vault, download the latest agent and the vault credentials and store it in a convenient location like C:\Downloads.</span></span>

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
PS C:\> $credsfilename
C:\downloads\testvault\_Sun Apr 10 2016.VaultCredentials
```

<span data-ttu-id="e6d11-178">No servidor DPM, execute o cmdlet [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) para registrar o computador no cofre.</span><span class="sxs-lookup"><span data-stu-id="e6d11-178">On the DPM server, run the [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet to register the machine with the vault.</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :West US
Machine registration succeeded.
```

### <a name="initial-configuration-settings"></a><span data-ttu-id="e6d11-179">Definições de configuração iniciais</span><span class="sxs-lookup"><span data-stu-id="e6d11-179">Initial configuration settings</span></span>
<span data-ttu-id="e6d11-180">Depois que o Servidor de DPM estiver registrado no cofre dos Serviços de Recuperação, ele será iniciado com as configurações de assinatura padrão.</span><span class="sxs-lookup"><span data-stu-id="e6d11-180">Once the DPM Server is registered with the Recovery Services vault, it starts with default subscription settings.</span></span> <span data-ttu-id="e6d11-181">Essas configurações de assinatura incluem Rede, Criptografia e Área de preparo.</span><span class="sxs-lookup"><span data-stu-id="e6d11-181">These subscription settings include Networking, Encryption and the Staging area.</span></span> <span data-ttu-id="e6d11-182">Para alterar as configurações de assinatura, primeiro você precisa obter um identificador nas configurações existentes (padrão) usando o cmdlet [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) :</span><span class="sxs-lookup"><span data-stu-id="e6d11-182">To change subscription settings you need to first get a handle on the existing (default) settings using the [Get-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612793) cmdlet:</span></span>

```
$setting = Get-DPMCloudSubscriptionSetting -DPMServerName "TestingServer"
```

<span data-ttu-id="e6d11-183">Todas as modificações são feitas a este objeto local ```$setting``` do PowerShell e o objeto completo é confirmado no DPM e no Backup do Azure para salvá-los usando o cmdlet [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) .</span><span class="sxs-lookup"><span data-stu-id="e6d11-183">All modifications are made to this local PowerShell object ```$setting```  and then the full object is committed to DPM and Azure Backup to save them using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="e6d11-184">Você precisa usar o sinalizador ```–Commit``` para garantir que as alterações sejam mantidas.</span><span class="sxs-lookup"><span data-stu-id="e6d11-184">You need to use the ```–Commit``` flag to ensure that the changes are persisted.</span></span> <span data-ttu-id="e6d11-185">As configurações não serão aplicadas nem usadas pelo Backup do Azure, a menos que sejam confirmadas.</span><span class="sxs-lookup"><span data-stu-id="e6d11-185">The settings will not be applied and used by Azure Backup unless committed.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="networking"></a><span data-ttu-id="e6d11-186">Rede</span><span class="sxs-lookup"><span data-stu-id="e6d11-186">Networking</span></span>
<span data-ttu-id="e6d11-187">Se a conectividade do computador de DPM ao serviço de Backup do Azure na Internet é feita por meio de um servidor proxy, as configurações do servidor proxy devem ser fornecidas para backups bem-sucedidos.</span><span class="sxs-lookup"><span data-stu-id="e6d11-187">If the connectivity of the DPM machine to the Azure Backup service on the internet is through a proxy server, then the proxy server settings should be provided for successful backups.</span></span> <span data-ttu-id="e6d11-188">Isso é feito usando os parâmetros ```-ProxyServer``` e ```-ProxyPort```, ```-ProxyUsername``` e ```ProxyPassword``` com o cmdlet [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791).</span><span class="sxs-lookup"><span data-stu-id="e6d11-188">This is done by using the ```-ProxyServer```and ```-ProxyPort```, ```-ProxyUsername``` and the ```ProxyPassword``` parameters with the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet.</span></span> <span data-ttu-id="e6d11-189">Neste exemplo, não há nenhum servidor proxy, por isso estamos explicitamente omitindo todas as informações relacionadas a proxy.</span><span class="sxs-lookup"><span data-stu-id="e6d11-189">In this example, there is no proxy server so we are explicitly clearing any proxy-related information.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoProxy
```

<span data-ttu-id="e6d11-190">O uso de largura de banda também pode ser controlado com as opções de ```-WorkHourBandwidth``` e ```-NonWorkHourBandwidth``` para um determinado conjunto de dias da semana.</span><span class="sxs-lookup"><span data-stu-id="e6d11-190">Bandwidth usage can also be controlled with options of ```-WorkHourBandwidth``` and ```-NonWorkHourBandwidth``` for a given set of days of the week.</span></span> <span data-ttu-id="e6d11-191">Neste exemplo, não definimos nenhuma limitação.</span><span class="sxs-lookup"><span data-stu-id="e6d11-191">In this example, we are not setting any throttling.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -NoThrottle
```

## <a name="configuring-the-staging-area"></a><span data-ttu-id="e6d11-192">Configurando a Área de preparo</span><span class="sxs-lookup"><span data-stu-id="e6d11-192">Configuring the staging Area</span></span>
<span data-ttu-id="e6d11-193">O agente de Backup do Azure em execução no servidor DPM precisa armazenar temporariamente os dados restaurados da nuvem (área de preparação local).</span><span class="sxs-lookup"><span data-stu-id="e6d11-193">The Azure Backup agent running on the DPM server needs temporary storage for data restored from the cloud (local staging area).</span></span> <span data-ttu-id="e6d11-194">Configure a área de preparo usando o cmdlet [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) e o parâmetro ```-StagingAreaPath```.</span><span class="sxs-lookup"><span data-stu-id="e6d11-194">Configure the staging area using the [Set-DPMCloudSubscriptionSetting](https://technet.microsoft.com/library/jj612791) cmdlet and the ```-StagingAreaPath``` parameter.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -StagingAreaPath "C:\StagingArea"
```

<span data-ttu-id="e6d11-195">No exemplo acima, a área de preparo será definida como *C:\StagingArea* no objeto do PowerShell```$setting```.</span><span class="sxs-lookup"><span data-stu-id="e6d11-195">In the example above, the staging area will be set to *C:\StagingArea* in the PowerShell object ```$setting```.</span></span> <span data-ttu-id="e6d11-196">Verifique se a pasta especificada já existe, ou a confirmação final das configurações de assinatura falhará.</span><span class="sxs-lookup"><span data-stu-id="e6d11-196">Ensure that the specified folder already exists, or else the final commit of the subscription settings will fail.</span></span>

### <a name="encryption-settings"></a><span data-ttu-id="e6d11-197">Configurações de criptografia</span><span class="sxs-lookup"><span data-stu-id="e6d11-197">Encryption settings</span></span>
<span data-ttu-id="e6d11-198">Os dados de backup enviados para o Backup do Azure são criptografados para proteger a confidencialidade dos dados.</span><span class="sxs-lookup"><span data-stu-id="e6d11-198">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span></span> <span data-ttu-id="e6d11-199">A senha de criptografia é a "senha" para descriptografar os dados no momento da restauração.</span><span class="sxs-lookup"><span data-stu-id="e6d11-199">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span></span> <span data-ttu-id="e6d11-200">É importante manter essas informações seguras depois de defini-las.</span><span class="sxs-lookup"><span data-stu-id="e6d11-200">It is important to keep this information safe and secure once it is set.</span></span>

<span data-ttu-id="e6d11-201">No exemplo abaixo, o primeiro comando converte a cadeia de caracteres ```passphrase123456789``` em uma cadeia de caracteres segura e atribui a sequência segura à variável chamada de ```$Passphrase```.</span><span class="sxs-lookup"><span data-stu-id="e6d11-201">In the example below, the first command converts the string ```passphrase123456789``` to a secure string and assigns the secure string to the variable named ```$Passphrase```.</span></span> <span data-ttu-id="e6d11-202">O segundo comando define a cadeia de caracteres segura em ```$Passphrase``` como a senha para a criptografia de backups.</span><span class="sxs-lookup"><span data-stu-id="e6d11-202">the second command sets the secure string in ```$Passphrase``` as the password for encrypting backups.</span></span>

```
PS C:\> $Passphrase = ConvertTo-SecureString -string "passphrase123456789" -AsPlainText -Force

PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -EncryptionPassphrase $Passphrase
```

> [!IMPORTANT]
> <span data-ttu-id="e6d11-203">Mantenha as informações de senha seguras e protegidas depois de defini-las.</span><span class="sxs-lookup"><span data-stu-id="e6d11-203">Keep the passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="e6d11-204">Você não poderá restaurar os dados do Azure sem essa senha.</span><span class="sxs-lookup"><span data-stu-id="e6d11-204">You will not be able to restore data from Azure without this passphrase.</span></span>
>
>

<span data-ttu-id="e6d11-205">Neste ponto, você deve fez todas as alterações necessárias ao objeto ```$setting``` .</span><span class="sxs-lookup"><span data-stu-id="e6d11-205">At this point, you should have made all the required changes to the ```$setting``` object.</span></span> <span data-ttu-id="e6d11-206">Lembre-se de confirmar as alterações.</span><span class="sxs-lookup"><span data-stu-id="e6d11-206">Remember to commit the changes.</span></span>

```
PS C:\> Set-DPMCloudSubscriptionSetting -DPMServerName "TestingServer" -SubscriptionSetting $setting -Commit
```

## <a name="protect-data-to-azure-backup"></a><span data-ttu-id="e6d11-207">Proteger dados no Backup do Azure</span><span class="sxs-lookup"><span data-stu-id="e6d11-207">Protect data to Azure Backup</span></span>
<span data-ttu-id="e6d11-208">Nesta seção, você adicionará um servidor de produção ao DPM, protegerá os dados primeiro no armazenamento local do DPM e, em seguida, no Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="e6d11-208">In this section, you will add a production server to DPM and then protect the data to local DPM storage and then to Azure Backup.</span></span> <span data-ttu-id="e6d11-209">Nos exemplos, demonstraremos como fazer backup de arquivos e pastas.</span><span class="sxs-lookup"><span data-stu-id="e6d11-209">In the examples, we will demonstrate how to back up files and folders.</span></span> <span data-ttu-id="e6d11-210">A lógica pode ser facilmente estendida para fazer backup de qualquer fonte de dados para a qual há suporte no DPM.</span><span class="sxs-lookup"><span data-stu-id="e6d11-210">The logic can easily be extended to backup any DPM-supported data source.</span></span> <span data-ttu-id="e6d11-211">Todos os backups do DPM são regidos por um GP (Grupo de Proteção) com quatro partes:</span><span class="sxs-lookup"><span data-stu-id="e6d11-211">All your DPM backups are governed by a Protection Group (PG) with four parts:</span></span>

1. <span data-ttu-id="e6d11-212">**Membros do grupo** é uma lista de todos os objetos protegíveis (também conhecidos como *Fontes de dados* no DPM) que você deseja proteger no mesmo grupo de proteção.</span><span class="sxs-lookup"><span data-stu-id="e6d11-212">**Group members** is a list of all the protectable objects (also known as *Datasources* in DPM) that you want to protect in the same protection group.</span></span> <span data-ttu-id="e6d11-213">Por exemplo, convém proteger as VMs de produção em um grupo de proteção e os bancos de dados do SQL Server em outro grupo de proteção, pois eles podem ter requisitos de backup diferentes.</span><span class="sxs-lookup"><span data-stu-id="e6d11-213">For example, you may want to protect production VMs in one protection group and SQL Server databases in another protection group as they may have different backup requirements.</span></span> <span data-ttu-id="e6d11-214">Antes de poder fazer backup de qualquer fonte de dados em um servidor de produção, é necessário verificar se o agente do DPM está instalado no servidor e é gerenciado pelo DPM.</span><span class="sxs-lookup"><span data-stu-id="e6d11-214">Before you can back up any datasource on a production server you need to make sure the DPM Agent is installed on the server and is managed by DPM.</span></span> <span data-ttu-id="e6d11-215">Siga as etapas para a [instalação do Agente do DPM](https://technet.microsoft.com/library/bb870935.aspx) e vincule-o ao Servidor DPM apropriado.</span><span class="sxs-lookup"><span data-stu-id="e6d11-215">Follow the steps for [installing the DPM Agent](https://technet.microsoft.com/library/bb870935.aspx) and linking it to the appropriate DPM Server.</span></span>
2. <span data-ttu-id="e6d11-216">**Método de proteção de dados** especifica os locais de destino de backup – fita, disco e nuvem.</span><span class="sxs-lookup"><span data-stu-id="e6d11-216">**Data protection method** specifies the target backup locations - tape, disk, and cloud.</span></span> <span data-ttu-id="e6d11-217">Em nosso exemplo, protegeremos os dados no disco local e na nuvem.</span><span class="sxs-lookup"><span data-stu-id="e6d11-217">In our example we will protect data to the local disk and to the cloud.</span></span>
3. <span data-ttu-id="e6d11-218">Um **agendamento de backup** que especifica quando os backups precisam ser executados e a frequência com que os dados devem ser sincronizados entre o servidor DPM e o servidor de produção.</span><span class="sxs-lookup"><span data-stu-id="e6d11-218">A **backup schedule** that specifies when backups need to be taken and how often the data should be synchronized between the DPM Server and the production server.</span></span>
4. <span data-ttu-id="e6d11-219">Um **cronograma de retenção** que especifica quanto tempo deve-se manter os pontos de recuperação no Azure.</span><span class="sxs-lookup"><span data-stu-id="e6d11-219">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span></span>

### <a name="creating-a-protection-group"></a><span data-ttu-id="e6d11-220">Criando um grupo de proteção</span><span class="sxs-lookup"><span data-stu-id="e6d11-220">Creating a protection group</span></span>
<span data-ttu-id="e6d11-221">Comece criando um novo Grupo de Proteção usando o cmdlet [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) .</span><span class="sxs-lookup"><span data-stu-id="e6d11-221">Start by creating a new Protection Group using the [New-DPMProtectionGroup](https://technet.microsoft.com/library/hh881722) cmdlet.</span></span>

```
PS C:\> $PG = New-DPMProtectionGroup -DPMServerName " TestingServer " -Name "ProtectGroup01"
```

<span data-ttu-id="e6d11-222">O cmdlet acima criará um Grupo de Proteção chamado *ProtectGroup01*.</span><span class="sxs-lookup"><span data-stu-id="e6d11-222">The above cmdlet will create a Protection Group named *ProtectGroup01*.</span></span> <span data-ttu-id="e6d11-223">Um grupo de proteção existente também pode ser modificado posteriormente para adicionar o backup à nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="e6d11-223">An existing protection group can also be modified later to add backup to the Azure cloud.</span></span> <span data-ttu-id="e6d11-224">No entanto, para fazer alterações ao Grupo de Proteção – novo ou existente – precisamos obter um identificador em um objeto *modificável* usando o cmdlet [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) .</span><span class="sxs-lookup"><span data-stu-id="e6d11-224">However, to make any changes to the Protection Group - new or existing - we need to get a handle on a *modifiable* object using the [Get-DPMModifiableProtectionGroup](https://technet.microsoft.com/library/hh881713) cmdlet.</span></span>

```
PS C:\> $MPG = Get-ModifiableProtectionGroup $PG
```

### <a name="adding-group-members-to-the-protection-group"></a><span data-ttu-id="e6d11-225">Adicionando membros do grupo ao Grupo de Proteção</span><span class="sxs-lookup"><span data-stu-id="e6d11-225">Adding group members to the Protection Group</span></span>
<span data-ttu-id="e6d11-226">Cada Agente do DPM conhece a lista de fontes de dados no servidor em que está instalado.</span><span class="sxs-lookup"><span data-stu-id="e6d11-226">Each DPM Agent knows the list of datasources on the server that it is installed on.</span></span> <span data-ttu-id="e6d11-227">Para adicionar uma fonte de dados ao Grupo de Proteção, o Agente do DPM precisa enviar primeiro uma lista das fontes de dados de volta ao servidor DPM.</span><span class="sxs-lookup"><span data-stu-id="e6d11-227">To add a datasource to the Protection Group, the DPM Agent needs to first send a list of the datasources back to the DPM server.</span></span> <span data-ttu-id="e6d11-228">Uma ou mais fontes de dados são então selecionadas e adicionadas ao Grupo de Proteção.</span><span class="sxs-lookup"><span data-stu-id="e6d11-228">One or more datasources are then selected and added to the Protection Group.</span></span> <span data-ttu-id="e6d11-229">As etapas do PowerShell necessárias para realizar isso são:</span><span class="sxs-lookup"><span data-stu-id="e6d11-229">The PowerShell steps needed to achieve this are:</span></span>

1. <span data-ttu-id="e6d11-230">Obter uma lista de todos os servidores gerenciados pelo DPM por meio do Agente do DPM.</span><span class="sxs-lookup"><span data-stu-id="e6d11-230">Fetch a list of all servers managed by DPM through the DPM Agent.</span></span>
2. <span data-ttu-id="e6d11-231">Escolher um servidor específico.</span><span class="sxs-lookup"><span data-stu-id="e6d11-231">Choose a specific server.</span></span>
3. <span data-ttu-id="e6d11-232">Obter uma lista de todas as fontes de dados no servidor.</span><span class="sxs-lookup"><span data-stu-id="e6d11-232">Fetch a list of all datasources on the server.</span></span>
4. <span data-ttu-id="e6d11-233">Escolher uma ou mais fontes de dados e adicioná-las ao Grupo de Proteção</span><span class="sxs-lookup"><span data-stu-id="e6d11-233">Choose one or more datasources and add them to the Protection Group</span></span>

<span data-ttu-id="e6d11-234">A lista dos servidores nos quais o Agente do DPM está instalado e sendo gerenciado pelo servidor DPM é obtida usando o cmdlet [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) .</span><span class="sxs-lookup"><span data-stu-id="e6d11-234">The list of servers on which the DPM Agent is installed and is being managed by the DPM Server is acquired with the [Get-DPMProductionServer](https://technet.microsoft.com/library/hh881600) cmdlet.</span></span> <span data-ttu-id="e6d11-235">Neste exemplo, filtraremos e configuraremos apenas o PS com o nome *productionserver01* para o backup.</span><span class="sxs-lookup"><span data-stu-id="e6d11-235">In this example we will filter and only configure PS with name *productionserver01* for backup.</span></span>

```
PS C:\> $server = Get-ProductionServer -DPMServerName "TestingServer" | where {($_.servername) –contains “productionserver01”
```

<span data-ttu-id="e6d11-236">Agora obtenha a lista de fontes de dados em ```$server``` usando o cmdlet [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605).</span><span class="sxs-lookup"><span data-stu-id="e6d11-236">Now fetch the list of datasources on ```$server``` using the [Get-DPMDatasource](https://technet.microsoft.com/library/hh881605) cmdlet.</span></span> <span data-ttu-id="e6d11-237">Neste exemplo, estamos filtrando para o volume *D:\*, que desejamos configurar para o backup.</span><span class="sxs-lookup"><span data-stu-id="e6d11-237">In this example we are filtering for the volume *D:\* that we want to configure for backup.</span></span> <span data-ttu-id="e6d11-238">Esta fonte de dados é adicionada ao Grupo de Proteção usando o cmdlet [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732).</span><span class="sxs-lookup"><span data-stu-id="e6d11-238">This datasource is then added to the Protection Group using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732) cmdlet.</span></span> <span data-ttu-id="e6d11-239">Lembre-se de usar o objeto de grupo de proteção *modificável*```$MPG``` para fazer as adições.</span><span class="sxs-lookup"><span data-stu-id="e6d11-239">Remember to use the *modifiable* protection group object ```$MPG``` to make the additions.</span></span>

```
PS C:\> $DS = Get-Datasource -ProductionServer $server -Inquire | where { $_.Name -contains “D:\” }

PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS
```

<span data-ttu-id="e6d11-240">Repita essa etapa quantas vezes for necessário, até adicionar todas as fontes de dados escolhidas ao grupo de proteção.</span><span class="sxs-lookup"><span data-stu-id="e6d11-240">Repeat this step as many times as required, until you have added all the chosen datasources to the protection group.</span></span> <span data-ttu-id="e6d11-241">Você também pode começar com apenas uma fonte de dados e concluir o fluxo de trabalho para criar o Grupo de Proteção e, posteriormente, adicionar mais fontes de dados ao Grupo de Proteção.</span><span class="sxs-lookup"><span data-stu-id="e6d11-241">You can also start with just one datasource, and complete the workflow for creating the Protection Group, and at a later point add more datasources to the Protection Group.</span></span>

### <a name="selecting-the-data-protection-method"></a><span data-ttu-id="e6d11-242">Selecionando o método de proteção de dados</span><span class="sxs-lookup"><span data-stu-id="e6d11-242">Selecting the data protection method</span></span>
<span data-ttu-id="e6d11-243">Depois de adicionar as fontes de dados ao Grupo de Proteção, a próxima etapa é especificar o método de proteção usando o cmdlet [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) .</span><span class="sxs-lookup"><span data-stu-id="e6d11-243">Once the datasources have been added to the Protection Group, the next step is to specify the protection method using the [Set-DPMProtectionType](https://technet.microsoft.com/library/hh881725) cmdlet.</span></span> <span data-ttu-id="e6d11-244">Neste exemplo, o Grupo de Proteção é configurado para backup no disco local e na nuvem.</span><span class="sxs-lookup"><span data-stu-id="e6d11-244">In this example, the Protection Group is setup for local disk and cloud backup.</span></span> <span data-ttu-id="e6d11-245">Você também precisa especificar a fonte de dados que deseja proteger na nuvem usando o cmdlet [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) com o sinalizador -Online.</span><span class="sxs-lookup"><span data-stu-id="e6d11-245">You also need to specify the datasource that you want to protect to cloud using the [Add-DPMChildDatasource](https://technet.microsoft.com/library/hh881732.aspx) cmdlet with -Online flag.</span></span>

```
PS C:\> Set-DPMProtectionType -ProtectionGroup $MPG -ShortTerm Disk –LongTerm Online
PS C:\> Add-DPMChildDatasource -ProtectionGroup $MPG -ChildDatasource $DS –Online
```

### <a name="setting-the-retention-range"></a><span data-ttu-id="e6d11-246">Configurando o intervalo de retenção</span><span class="sxs-lookup"><span data-stu-id="e6d11-246">Setting the retention range</span></span>
<span data-ttu-id="e6d11-247">Defina a retenção dos pontos de backup usando o cmdlet [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) .</span><span class="sxs-lookup"><span data-stu-id="e6d11-247">Set the retention for the backup points using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span> <span data-ttu-id="e6d11-248">Embora possa parecer estranho definir a retenção antes de definir o agendamento de backup, usar o cmdlet ```Set-DPMPolicyObjective``` define automaticamente um agendamento de backup padrão que pode então ser modificado.</span><span class="sxs-lookup"><span data-stu-id="e6d11-248">While it might seem odd to set the retention before the backup schedule has been defined, using the ```Set-DPMPolicyObjective``` cmdlet automatically sets a default backup schedule that can then be modified.</span></span> <span data-ttu-id="e6d11-249">Sempre é possível definir o agendamento de backup primeiro e a política de retenção posteriormente.</span><span class="sxs-lookup"><span data-stu-id="e6d11-249">It is always possible to set the backup schedule first and the retention policy after.</span></span>

<span data-ttu-id="e6d11-250">No exemplo abaixo, o cmdlet define os parâmetros de retenção para backups em disco.</span><span class="sxs-lookup"><span data-stu-id="e6d11-250">In the example below, the cmdlet sets the retention parameters for disk backups.</span></span> <span data-ttu-id="e6d11-251">Isso manterá backups por 10 dias e sincronizará dados entre o servidor de produção e o servidor DPM a cada 6 horas.</span><span class="sxs-lookup"><span data-stu-id="e6d11-251">This will retain backups for 10 days, and sync data every 6 hours between the production server and the DPM server.</span></span> <span data-ttu-id="e6d11-252">O ```SynchronizationFrequencyMinutes``` não define a frequência em que um ponto de backup é criado, mas a frequência em que os dados são copiados para o servidor DPM.</span><span class="sxs-lookup"><span data-stu-id="e6d11-252">The ```SynchronizationFrequencyMinutes``` doesn't define how often a backup point is created, but how often data is copied to the DPM server.</span></span>  <span data-ttu-id="e6d11-253">Essa configuração impede que os backups fiquem grandes demais.</span><span class="sxs-lookup"><span data-stu-id="e6d11-253">This setting prevents backups from becoming too large.</span></span>

```
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -RetentionRangeInDays 10 -SynchronizationFrequencyMinutes 360
```

<span data-ttu-id="e6d11-254">Para backups destinados ao Azure (o DPM refere-se a eles como backups Online), os períodos de retenção podem ser configurados para a [retenção de longo prazo usando um esquema GFS (Avô-Pai-Filho)](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="e6d11-254">For backups going to Azure (DPM refers to them as Online backups) the retention ranges can be configured for [long term retention using a Grandfather-Father-Son scheme (GFS)](backup-azure-backup-cloud-as-tape.md).</span></span> <span data-ttu-id="e6d11-255">Ou seja, você pode definir uma política de retenção combinada que envolva políticas de retenção diárias, semanais, mensais e anuais.</span><span class="sxs-lookup"><span data-stu-id="e6d11-255">That is, you can define a combined retention policy involving daily, weekly, monthly and yearly retention policies.</span></span> <span data-ttu-id="e6d11-256">Neste exemplo, criamos uma matriz que representa o esquema de retenção complexo que queremos e, em seguida, configuramos o intervalo de retenção usando o cmdlet [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) .</span><span class="sxs-lookup"><span data-stu-id="e6d11-256">In this example, we create an array representing the complex retention scheme that we want, and then configure the retention range using the [Set-DPMPolicyObjective](https://technet.microsoft.com/library/hh881762) cmdlet.</span></span>

```
PS C:\> $RRlist = @()
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 180, Days)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 104, Weeks)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 60, Month)
PS C:\> $RRList += (New-Object -TypeName Microsoft.Internal.EnterpriseStorage.Dls.UI.ObjectModel.OMCommon.RetentionRange -ArgumentList 10, Years)
PS C:\> Set-DPMPolicyObjective –ProtectionGroup $MPG -OnlineRetentionRangeList $RRlist
```

### <a name="set-the-backup-schedule"></a><span data-ttu-id="e6d11-257">Definir o agendamento de backup</span><span class="sxs-lookup"><span data-stu-id="e6d11-257">Set the backup schedule</span></span>
<span data-ttu-id="e6d11-258">O DPM define um agendamento padrão automaticamente se você especificar o objetivo de proteção usando o cmdlet ```Set-DPMPolicyObjective``` .</span><span class="sxs-lookup"><span data-stu-id="e6d11-258">DPM sets a default backup schedule automatically if you specify the protection objective using the ```Set-DPMPolicyObjective``` cmdlet.</span></span> <span data-ttu-id="e6d11-259">Para alterar os agendamentos padrão, use o cmdlet [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) seguido do cmdlet [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723).</span><span class="sxs-lookup"><span data-stu-id="e6d11-259">To change the default schedules, use the [Get-DPMPolicySchedule](https://technet.microsoft.com/library/hh881749) cmdlet followed by the [Set-DPMPolicySchedule](https://technet.microsoft.com/library/hh881723) cmdlet.</span></span>

```
PS C:\> $onlineSch = Get-DPMPolicySchedule -ProtectionGroup $mpg -LongTerm Online
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[0] -TimesOfDay 02:00
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[1] -TimesOfDay 02:00 -DaysOfWeek Sa,Su –Interval 1
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[2] -TimesOfDay 02:00 -RelativeIntervals First,Third –DaysOfWeek Sa
PS C:\> Set-DPMPolicySchedule -ProtectionGroup $MPG -Schedule $onlineSch[3] -TimesOfDay 02:00 -DaysOfMonth 2,5,8,9 -Months Jan,Jul
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```

<span data-ttu-id="e6d11-260">No exemplo acima, ```$onlineSch``` é uma matriz com quatro elementos que contém o agendamento de proteção online existente para o Grupo de Proteção no esquema GFS:</span><span class="sxs-lookup"><span data-stu-id="e6d11-260">In the above example, ```$onlineSch``` is an array with four elements that contains the existing online protection schedule for the Protection Group in the GFS scheme:</span></span>

1. <span data-ttu-id="e6d11-261">```$onlineSch[0]``` contém a agenda diária</span><span class="sxs-lookup"><span data-stu-id="e6d11-261">```$onlineSch[0]``` contains the daily schedule</span></span>
2. <span data-ttu-id="e6d11-262">```$onlineSch[1]``` contém a agenda semanal</span><span class="sxs-lookup"><span data-stu-id="e6d11-262">```$onlineSch[1]``` contains the weekly schedule</span></span>
3. <span data-ttu-id="e6d11-263">```$onlineSch[2]``` contém a agenda mensal</span><span class="sxs-lookup"><span data-stu-id="e6d11-263">```$onlineSch[2]``` contains the monthly schedule</span></span>
4. <span data-ttu-id="e6d11-264">```$onlineSch[3]``` contém a agenda anual</span><span class="sxs-lookup"><span data-stu-id="e6d11-264">```$onlineSch[3]``` contains the yearly schedule</span></span>

<span data-ttu-id="e6d11-265">Portanto, se precisar modificar o agendamento semanal, você precisa se referir a ```$onlineSch[1]```.</span><span class="sxs-lookup"><span data-stu-id="e6d11-265">So if you need to modify the weekly schedule, you need to refer to the ```$onlineSch[1]```.</span></span>

### <a name="initial-backup"></a><span data-ttu-id="e6d11-266">Backup inicial</span><span class="sxs-lookup"><span data-stu-id="e6d11-266">Initial backup</span></span>
<span data-ttu-id="e6d11-267">Ao fazer backup de uma fonte de dados pela primeira vez, o DPM precisa criar uma réplica inicial que cria uma cópia completa da fonte de dados que será protegida no volume de réplica do DPM.</span><span class="sxs-lookup"><span data-stu-id="e6d11-267">When backing up a datasource for the first time, DPM needs creates initial replica that creates a full copy of the datasource to be protected on DPM replica volume.</span></span> <span data-ttu-id="e6d11-268">Essa atividade pode ser agendada para um horário específico ou pode ser disparada manualmente usando o cmdlet [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) com o parâmetro ```-NOW```.</span><span class="sxs-lookup"><span data-stu-id="e6d11-268">This activity can either be scheduled for a specific time, or can be triggered manually, using the [Set-DPMReplicaCreationMethod](https://technet.microsoft.com/library/hh881715) cmdlet with the parameter ```-NOW```.</span></span>

```
PS C:\> Set-DPMReplicaCreationMethod -ProtectionGroup $MPG -NOW
```
### <a name="changing-the-size-of-dpm-replica--recovery-point-volume"></a><span data-ttu-id="e6d11-269">Alterando o tamanho da réplica do DPM e o volume de ponto de recuperação</span><span class="sxs-lookup"><span data-stu-id="e6d11-269">Changing the size of DPM Replica & recovery point volume</span></span>
<span data-ttu-id="e6d11-270">Você também pode alterar o tamanho do volume de Réplica do DPM, e o volume de Cópia de Sombra usando o cmdlet [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) , como no exemplo a seguir: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span><span class="sxs-lookup"><span data-stu-id="e6d11-270">You can also change the size of DPM Replica volume and Shadow Copy volume using [Set-DPMDatasourceDiskAllocation](https://technet.microsoft.com/library/hh881618.aspx) cmdlet as in the following example: Get-DatasourceDiskAllocation -Datasource $DS Set-DatasourceDiskAllocation -Datasource $DS -ProtectionGroup $MPG -manual -ReplicaArea (2gb) -ShadowCopyArea (2gb)</span></span>

### <a name="committing-the-changes-to-the-protection-group"></a><span data-ttu-id="e6d11-271">Confirmando as alterações ao Grupo de Proteção</span><span class="sxs-lookup"><span data-stu-id="e6d11-271">Committing the changes to the Protection Group</span></span>
<span data-ttu-id="e6d11-272">Por último, as alterações precisam ser confirmadas antes que o DPM possa fazer o backup de acordo com a nova configuração do Grupo de Proteção.</span><span class="sxs-lookup"><span data-stu-id="e6d11-272">Finally, the changes need to be committed before DPM can take the backup per the new Protection Group configuration.</span></span> <span data-ttu-id="e6d11-273">Isso pode ser obtido usando o cmdlet [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) .</span><span class="sxs-lookup"><span data-stu-id="e6d11-273">This can be achieved using the [Set-DPMProtectionGroup](https://technet.microsoft.com/library/hh881758) cmdlet.</span></span>

```
PS C:\> Set-DPMProtectionGroup -ProtectionGroup $MPG
```
## <a name="view-the-backup-points"></a><span data-ttu-id="e6d11-274">Exibir os pontos de backup</span><span class="sxs-lookup"><span data-stu-id="e6d11-274">View the backup points</span></span>
<span data-ttu-id="e6d11-275">Você pode usar o cmdlet [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) para obter uma lista de todos os pontos de recuperação para uma fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="e6d11-275">You can use the [Get-DPMRecoveryPoint](https://technet.microsoft.com/library/hh881746) cmdlet to get a list of all recovery points for a datasource.</span></span> <span data-ttu-id="e6d11-276">Neste exemplo, iremos:</span><span class="sxs-lookup"><span data-stu-id="e6d11-276">In this example, we will:</span></span>

* <span data-ttu-id="e6d11-277">buscar todos os PGs no servidor DPM e armazenados em uma matriz ```$PG```</span><span class="sxs-lookup"><span data-stu-id="e6d11-277">fetch all the PGs on the DPM server and stored in an array ```$PG```</span></span>
* <span data-ttu-id="e6d11-278">obter as fontes de dados correspondente ao ```$PG[0]```</span><span class="sxs-lookup"><span data-stu-id="e6d11-278">get the datasources corresponding to the ```$PG[0]```</span></span>
* <span data-ttu-id="e6d11-279">obter todos os pontos de recuperação para uma fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="e6d11-279">get all the recovery points for a datasource.</span></span>

```
PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online
```

## <a name="restore-data-protected-on-azure"></a><span data-ttu-id="e6d11-280">Restaurar dados protegidos no Azure</span><span class="sxs-lookup"><span data-stu-id="e6d11-280">Restore data protected on Azure</span></span>
<span data-ttu-id="e6d11-281">A restauração de dados é uma combinação de um objeto ```RecoverableItem``` e um objeto ```RecoveryOption```.</span><span class="sxs-lookup"><span data-stu-id="e6d11-281">Restoring data is a combination of a ```RecoverableItem``` object and a ```RecoveryOption``` object.</span></span> <span data-ttu-id="e6d11-282">Na seção anterior, obtivemos uma lista de pontos de backup para uma fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="e6d11-282">In the previous section, we got a list of the backup points for a datasource.</span></span>

<span data-ttu-id="e6d11-283">No exemplo a seguir, demonstramos como restaurar uma máquina virtual Hyper-V por meio do Backup do Azure, combinando os pontos de backup com o destino para recuperação.</span><span class="sxs-lookup"><span data-stu-id="e6d11-283">In the example below, we demonstrate how to restore a Hyper-V virtual machine from Azure Backup by combining backup points with the target for recovery.</span></span> <span data-ttu-id="e6d11-284">Este exemplo inclui:</span><span class="sxs-lookup"><span data-stu-id="e6d11-284">This example includes:</span></span>

* <span data-ttu-id="e6d11-285">Criar uma opção de recuperação usando o cmdlet [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) .</span><span class="sxs-lookup"><span data-stu-id="e6d11-285">Creating a recovery option using the  [New-DPMRecoveryOption](https://technet.microsoft.com/library/hh881592) cmdlet.</span></span>
* <span data-ttu-id="e6d11-286">Obter a matriz de pontos de backup usando o cmdlet ```Get-DPMRecoveryPoint``` .</span><span class="sxs-lookup"><span data-stu-id="e6d11-286">Fetching the array of backup points using the ```Get-DPMRecoveryPoint``` cmdlet.</span></span>
* <span data-ttu-id="e6d11-287">Escolher um ponto de backup por meio do qual fazer a restauração.</span><span class="sxs-lookup"><span data-stu-id="e6d11-287">Choosing a backup point to restore from.</span></span>

```
PS C:\> $RecoveryOption = New-DPMRecoveryOption -HyperVDatasource -TargetServer "HVDCenter02" -RecoveryLocation AlternateHyperVServer -RecoveryType Recover -TargetLocation “C:\VMRecovery”

PS C:\> $PG = Get-DPMProtectionGroup –DPMServerName "TestingServer"
PS C:\> $DS = Get-DPMDatasource -ProtectionGroup $PG[0]
PS C:\> $RecoveryPoints = Get-DPMRecoverypoint -Datasource $DS[0] -Online

PS C:\> Restore-DPMRecoverableItem -RecoverableItem $RecoveryPoints[0] -RecoveryOption $RecoveryOption
```

<span data-ttu-id="e6d11-288">Os comandos podem ser facilmente estendidos para qualquer tipo de fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="e6d11-288">The commands can easily be extended for any datasource type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6d11-289">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e6d11-289">Next steps</span></span>
* <span data-ttu-id="e6d11-290">Para saber mais sobre o DPM para o Backup do Azure, confira [Introdução ao Backup do DPM](backup-azure-dpm-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="e6d11-290">For more information about DPM to Azure Backup see [Introduction to DPM Backup](backup-azure-dpm-introduction.md)</span></span>
