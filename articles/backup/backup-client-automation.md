---
title: Usar o PowerShell para fazer backup do Windows Server no Azure | Microsoft Docs
description: Saiba como implantar e gerenciar o Backup do Azure usando o PowerShell
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 65218095-2996-44d9-917b-8c84fc9ac415
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: saurse;markgal;jimpark;nkolli;trinadhk
ms.openlocfilehash: d3f165c749af0553c4918b33b0d24cc1e21af2a9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-and-manage-backup-to-azure-for-windows-serverwindows-client-using-powershell"></a><span data-ttu-id="b1f32-103">Implantar e gerenciar o backup no Azure para o Windows Server/Windows Client usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="b1f32-103">Deploy and manage backup to Azure for Windows Server/Windows Client using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b1f32-104">ARM</span><span class="sxs-lookup"><span data-stu-id="b1f32-104">ARM</span></span>](backup-client-automation.md)
> * [<span data-ttu-id="b1f32-105">Clássico</span><span class="sxs-lookup"><span data-stu-id="b1f32-105">Classic</span></span>](backup-client-automation-classic.md)
>
>

<span data-ttu-id="b1f32-106">Este artigo mostra como usar o PowerShell para configurar o Backup do Azure no Windows Server ou no cliente Windows, e como gerenciar backups e recuperações.</span><span class="sxs-lookup"><span data-stu-id="b1f32-106">This article shows you how to use PowerShell for setting up Azure Backup on Windows Server or a Windows client, and managing backup and recovery.</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="b1f32-107">Instalar o Azure Powershell</span><span class="sxs-lookup"><span data-stu-id="b1f32-107">Install Azure PowerShell</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="b1f32-108">Este artigo se concentra nos cmdlets do PowerShell do ARM (Azure Resource Manager) e do Backup Online da MS que permitem que você use um cofre dos Serviços de Recuperação em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b1f32-108">This article focuses on the Azure Resource Manager (ARM) and the MS Online Backup PowerShell cmdlets that enable you to use a Recovery Services vault in a resource group.</span></span>

<span data-ttu-id="b1f32-109">Em outubro de 2015, o Azure PowerShell 1.0 foi lançado.</span><span class="sxs-lookup"><span data-stu-id="b1f32-109">In October 2015, Azure PowerShell 1.0 was released.</span></span> <span data-ttu-id="b1f32-110">Essa versão veio logo após a 0.9.8 e trouxe algumas alterações importantes, especialmente no padrão de nomenclatura dos cmdlets.</span><span class="sxs-lookup"><span data-stu-id="b1f32-110">This release succeeded the 0.9.8 release and brought about some significant changes, especially in the naming pattern of the cmdlets.</span></span> <span data-ttu-id="b1f32-111">Os cmdlets da versão 1.0 seguem o padrão de nomenclatura {verbo}-AzureRm{substantivo}; por outro lado, os nomes da versão 0.9.8 não incluem **Rm** (por exemplo, New-AzureRmResourceGroup em vez de New-AzureResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="b1f32-111">1.0 cmdlets follow the naming pattern {verb}-AzureRm{noun}; whereas, the 0.9.8 names do not include **Rm** (for example, New-AzureRmResourceGroup instead of New-AzureResourceGroup).</span></span> <span data-ttu-id="b1f32-112">Ao usar o Azure PowerShell 0.9.8, você deve primeiro habilitar o modo do Gerenciador de Recursos executando o comando **Switch-AzureMode AzureResourceManager** .</span><span class="sxs-lookup"><span data-stu-id="b1f32-112">When using Azure PowerShell 0.9.8, you must first enable the Resource Manager mode by running the **Switch-AzureMode AzureResourceManager** command.</span></span> <span data-ttu-id="b1f32-113">Este comando não é necessário na 1.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="b1f32-113">This command is not necessary in 1.0 or later.</span></span>

<span data-ttu-id="b1f32-114">Se você quiser usar seus scripts escritos para o ambiente da versão 0.9.8 no ambiente da versão 1.0 ou posterior, é necessário testar e atualizar cuidadosamente os scripts em um ambiente de pré-produção antes de usá-los em produção, a fim de evitar algum impacto inesperado.</span><span class="sxs-lookup"><span data-stu-id="b1f32-114">If you want to use your scripts written for the 0.9.8 environment, in the 1.0 or later environment, you should carefully update and test the scripts in a pre-production environment before using them in production to avoid unexpected impact.</span></span>

<span data-ttu-id="b1f32-115">[Baixe a última versão do PowerShell](https://github.com/Azure/azure-powershell/releases) (a versão mínima necessária é: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="b1f32-115">[Download the latest PowerShell release](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="b1f32-116">Criar um cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="b1f32-116">Create a recovery services vault</span></span>
<span data-ttu-id="b1f32-117">As etapas a seguir orientarão você durante a criação de um cofre dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="b1f32-117">The following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="b1f32-118">Um cofre dos Serviços de Recuperação é diferente de um cofre de Backup.</span><span class="sxs-lookup"><span data-stu-id="b1f32-118">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="b1f32-119">Se você estiver usando um Backup do Azure pela primeira vez, deverá usar o cmdlet **Register-AzureRMResourceProvider** para registrar o provedor do Serviço de Recuperação do Azure com sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="b1f32-119">If you are using Azure Backup for the first time, you must use the **Register-AzureRMResourceProvider** cmdlet to register the Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="b1f32-120">O cofre dos Serviços de Recuperação é um recurso do ARM e, portanto, você precisará colocá-lo em um Grupo de Recursos.</span><span class="sxs-lookup"><span data-stu-id="b1f32-120">The Recovery Services vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="b1f32-121">Você pode usar um grupo de recursos existente ou criar um novo.</span><span class="sxs-lookup"><span data-stu-id="b1f32-121">You can use an existing resource group, or create a new one.</span></span> <span data-ttu-id="b1f32-122">Ao criar um novo grupo de recursos, especifique o nome e o local para o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b1f32-122">When creating a new resource group, specify the name and location for the resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "WestUS"
    ```
3. <span data-ttu-id="b1f32-123">Use o cmdlet **New-AzureRmRecoveryServicesVault** para criar o novo cofre.</span><span class="sxs-lookup"><span data-stu-id="b1f32-123">Use the **New-AzureRmRecoveryServicesVault** cmdlet to create the new vault.</span></span> <span data-ttu-id="b1f32-124">Lembre-se de especificar o mesmo local para o cofre usado para o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="b1f32-124">Be sure to specify the same location for the vault as was used for the resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "WestUS"
    ```
4. <span data-ttu-id="b1f32-125">Especifique o tipo de redundância de armazenamento a usar. Você pode usar o [Armazenamento com Redundância Local (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) ou o [Armazenamento com Redundância Geográfica (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="b1f32-125">Specify the type of storage redundancy to use; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="b1f32-126">O exemplo a seguir mostra que a opção BackupStorageRedundancy para o testVault está definida como GeoRedundant.</span><span class="sxs-lookup"><span data-stu-id="b1f32-126">The following example shows the -BackupStorageRedundancy option for testVault is set to GeoRedundant.</span></span>

   > [!TIP]
   > <span data-ttu-id="b1f32-127">Muitos cmdlets do Backup do Azure exigem o objeto do cofre dos Serviços de Recuperação como entrada.</span><span class="sxs-lookup"><span data-stu-id="b1f32-127">Many Azure Backup cmdlets require the Recovery Services vault object as an input.</span></span> <span data-ttu-id="b1f32-128">Por esse motivo, pode ser útil armazenar o objeto do cofre dos Serviços de Recuperação de backup em uma variável.</span><span class="sxs-lookup"><span data-stu-id="b1f32-128">For this reason, it is convenient to store the Backup Recovery Services vault object in a variable.</span></span>
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-the-vaults-in-a-subscription"></a><span data-ttu-id="b1f32-129">Exibir os cofres em uma assinatura</span><span class="sxs-lookup"><span data-stu-id="b1f32-129">View the vaults in a subscription</span></span>
<span data-ttu-id="b1f32-130">Use **Get-AzureRmRecoveryServicesVault** para exibir a lista de todos os cofres da assinatura atual.</span><span class="sxs-lookup"><span data-stu-id="b1f32-130">Use **Get-AzureRmRecoveryServicesVault** to view the list of all vaults in the current subscription.</span></span> <span data-ttu-id="b1f32-131">Você pode usar esse comando para verificar se um novo cofre foi criado ou para ver quais cofres estão disponíveis na assinatura.</span><span class="sxs-lookup"><span data-stu-id="b1f32-131">You can use this command to check that a new  vault was created, or to see what vaults are available in the subscription.</span></span>

<span data-ttu-id="b1f32-132">Execute o comando **Get-AzureRmRecoveryServicesVault** e todos os cofres na assinatura serão listados.</span><span class="sxs-lookup"><span data-stu-id="b1f32-132">Run the command, **Get-AzureRmRecoveryServicesVault**, and all vaults in the subscription are listed.</span></span>

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


## <a name="installing-the-azure-backup-agent"></a><span data-ttu-id="b1f32-133">Instalando o agente de Backup do Azure</span><span class="sxs-lookup"><span data-stu-id="b1f32-133">Installing the Azure Backup agent</span></span>
<span data-ttu-id="b1f32-134">Antes de instalar o agente de Backup do Azure, você precisa ter o instalador baixado, já no Windows Server.</span><span class="sxs-lookup"><span data-stu-id="b1f32-134">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span></span> <span data-ttu-id="b1f32-135">Você pode obter a última versão do instalador no [Centro de Download da Microsoft](http://aka.ms/azurebackup_agent) ou na página Painel do cofre dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="b1f32-135">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the Recovery Services vault's Dashboard page.</span></span> <span data-ttu-id="b1f32-136">Salve o instalador em um local de fácil acesso, como *C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="b1f32-136">Save the installer to an easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="b1f32-137">Como alternativa, use o PowerShell para obter o downloader:</span><span class="sxs-lookup"><span data-stu-id="b1f32-137">Alternatively, use PowerShell to get the downloader:</span></span>
 
 ```
 $MarsAURL = 'Http://Aka.Ms/Azurebackup_Agent'
 $WC = New-Object System.Net.WebClient
 $WC.DownloadFile($MarsAURL,'C:\downloads\MARSAgentInstaller.EXE')
 C:\Downloads\MARSAgentInstaller.EXE /q
 ```

<span data-ttu-id="b1f32-138">Para instalar o agente, execute o comando a seguir em um console do Azure PowerShell com privilégios elevados:</span><span class="sxs-lookup"><span data-stu-id="b1f32-138">To install the agent, run the following command in an elevated PowerShell console:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="b1f32-139">Isso instala o agente com todas as opções padrão.</span><span class="sxs-lookup"><span data-stu-id="b1f32-139">This installs the agent with all the default options.</span></span> <span data-ttu-id="b1f32-140">A instalação demora alguns minutos, em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="b1f32-140">The installation takes a few minutes in the background.</span></span> <span data-ttu-id="b1f32-141">Se você não especificar a opção */nu* , a janela do **Windows Update** será aberta no final da instalação para verificar se há atualizações.</span><span class="sxs-lookup"><span data-stu-id="b1f32-141">If you do not specify the */nu* option then the **Windows Update** window will open at the end of the installation to check for any updates.</span></span> <span data-ttu-id="b1f32-142">Uma vez instalado, o agente será exibido na lista de programas instalados.</span><span class="sxs-lookup"><span data-stu-id="b1f32-142">Once installed, the agent will show in the list of installed programs.</span></span>

<span data-ttu-id="b1f32-143">Para ver a lista de programas instalados, vá para **Painel de controle** > **Programas** > **Programas e recursos**.</span><span class="sxs-lookup"><span data-stu-id="b1f32-143">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agente instalado](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="b1f32-145">Opções de instalação</span><span class="sxs-lookup"><span data-stu-id="b1f32-145">Installation options</span></span>
<span data-ttu-id="b1f32-146">Para ver todas as opções disponíveis por meio da linha de comando, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="b1f32-146">To see all the options available via the command-line, use the following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="b1f32-147">As opções disponíveis incluem:</span><span class="sxs-lookup"><span data-stu-id="b1f32-147">The available options include:</span></span>

| <span data-ttu-id="b1f32-148">Opção</span><span class="sxs-lookup"><span data-stu-id="b1f32-148">Option</span></span> | <span data-ttu-id="b1f32-149">Detalhes</span><span class="sxs-lookup"><span data-stu-id="b1f32-149">Details</span></span> | <span data-ttu-id="b1f32-150">Padrão</span><span class="sxs-lookup"><span data-stu-id="b1f32-150">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b1f32-151">/q</span><span class="sxs-lookup"><span data-stu-id="b1f32-151">/q</span></span> |<span data-ttu-id="b1f32-152">Instalação silenciosa</span><span class="sxs-lookup"><span data-stu-id="b1f32-152">Quiet installation</span></span> |- |
| <span data-ttu-id="b1f32-153">/p:"local"</span><span class="sxs-lookup"><span data-stu-id="b1f32-153">/p:"location"</span></span> |<span data-ttu-id="b1f32-154">Caminho para a pasta de instalação para o agente de Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="b1f32-154">Path to the installation folder for the Azure Backup agent.</span></span> |<span data-ttu-id="b1f32-155">C:\Arquivos de Programas\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="b1f32-155">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="b1f32-156">/s:"local"</span><span class="sxs-lookup"><span data-stu-id="b1f32-156">/s:"location"</span></span> |<span data-ttu-id="b1f32-157">Caminho para a pasta de cache para o agente de Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="b1f32-157">Path to the cache folder for the Azure Backup agent.</span></span> |<span data-ttu-id="b1f32-158">C:\Arquivos de Programas\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="b1f32-158">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="b1f32-159">/m</span><span class="sxs-lookup"><span data-stu-id="b1f32-159">/m</span></span> |<span data-ttu-id="b1f32-160">Aceitar o Microsoft Update</span><span class="sxs-lookup"><span data-stu-id="b1f32-160">Opt-in to Microsoft Update</span></span> |- |
| <span data-ttu-id="b1f32-161">/nu</span><span class="sxs-lookup"><span data-stu-id="b1f32-161">/nu</span></span> |<span data-ttu-id="b1f32-162">Não verificar se há atualizações após a conclusão da instalação</span><span class="sxs-lookup"><span data-stu-id="b1f32-162">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="b1f32-163">/d</span><span class="sxs-lookup"><span data-stu-id="b1f32-163">/d</span></span> |<span data-ttu-id="b1f32-164">Desinstala o agente dos Serviços de Recuperação do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="b1f32-164">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="b1f32-165">/ph</span><span class="sxs-lookup"><span data-stu-id="b1f32-165">/ph</span></span> |<span data-ttu-id="b1f32-166">Endereço do host do proxy</span><span class="sxs-lookup"><span data-stu-id="b1f32-166">Proxy Host Address</span></span> |- |
| <span data-ttu-id="b1f32-167">/po</span><span class="sxs-lookup"><span data-stu-id="b1f32-167">/po</span></span> |<span data-ttu-id="b1f32-168">Número da porta do host do proxy</span><span class="sxs-lookup"><span data-stu-id="b1f32-168">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="b1f32-169">/pu</span><span class="sxs-lookup"><span data-stu-id="b1f32-169">/pu</span></span> |<span data-ttu-id="b1f32-170">UserName do host do proxy</span><span class="sxs-lookup"><span data-stu-id="b1f32-170">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="b1f32-171">/pw</span><span class="sxs-lookup"><span data-stu-id="b1f32-171">/pw</span></span> |<span data-ttu-id="b1f32-172">Senha do proxy</span><span class="sxs-lookup"><span data-stu-id="b1f32-172">Proxy Password</span></span> |- |

## <a name="registering-windows-server-or-windows-client-machine-to-a-recovery-services-vault"></a><span data-ttu-id="b1f32-173">Registro do Windows Server ou do computador cliente do Windows em um Cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="b1f32-173">Registering Windows Server or Windows client machine to a Recovery Services Vault</span></span>
<span data-ttu-id="b1f32-174">Depois de criar o cofre dos Serviços de Recuperação, baixe o agente mais recente e as credenciais do cofre e armazene-os em um local conveniente como C:\Downloads.</span><span class="sxs-lookup"><span data-stu-id="b1f32-174">After you created the Recovery Services vault, download the latest agent and the vault credentials and store it in a convenient location like C:\Downloads.</span></span>

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
```

<span data-ttu-id="b1f32-175">No computador cliente do Windows Server ou do Windows, execute o cmdlet [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) para registrar o computador no cofre.</span><span class="sxs-lookup"><span data-stu-id="b1f32-175">On the Windows Server or Windows client machine, run the [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet to register the machine with the vault.</span></span>
<span data-ttu-id="b1f32-176">Este e outros cmdlets usados para backup, são do módulo MSONLINE que o AgentInstaller da Mars adicionou como parte do processo de instalação.</span><span class="sxs-lookup"><span data-stu-id="b1f32-176">This, and other cmdlets used for backup, are from the MSONLINE module which the Mars AgentInstaller added as part of the installation process.</span></span> 

<span data-ttu-id="b1f32-177">O instalador do agente não atualiza a variável $Env:PSModulePath.</span><span class="sxs-lookup"><span data-stu-id="b1f32-177">The Agent installer does not update the $Env:PSModulePath variable.</span></span> <span data-ttu-id="b1f32-178">Isso significa que o carregamento automático do módulo falhará.</span><span class="sxs-lookup"><span data-stu-id="b1f32-178">This means module auto-load fails.</span></span> <span data-ttu-id="b1f32-179">Para resolver esse problema, você pode fazer o seguinte:</span><span class="sxs-lookup"><span data-stu-id="b1f32-179">To resolve this you can do the following:</span></span>

```
PS C:\>  $Env:psmodulepath += ';C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules
```

<span data-ttu-id="b1f32-180">Como alternativa, você pode carregar manualmente o módulo em seu script da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="b1f32-180">Alternatively, you can manually load the module in your script as follows:</span></span>

```
PS C:\>  Import-Module  'C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules\MSOnlineBackup'

```

<span data-ttu-id="b1f32-181">Depois de carregar os cmdlets do Backup Online, você registra as credenciais do cofre:</span><span class="sxs-lookup"><span data-stu-id="b1f32-181">Once you load the Online Backup cmdlets, you register the vault credentials:</span></span>


```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration-VaultCredentials $cred -Confirm:$false
CertThumbprint      :7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName: testvault
Region              :WestUS
Machine registration succeeded.
```

> [!IMPORTANT]
> <span data-ttu-id="b1f32-182">Não use caminhos relativos para especificar o arquivo de credenciais do cofre.</span><span class="sxs-lookup"><span data-stu-id="b1f32-182">Do not use relative paths to specify the vault credentials file.</span></span> <span data-ttu-id="b1f32-183">Você deve fornecer um caminho absoluto como entrada para o cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b1f32-183">You must provide an absolute path as an input to the cmdlet.</span></span>
>
>

## <a name="networking-settings"></a><span data-ttu-id="b1f32-184">Configurações de rede</span><span class="sxs-lookup"><span data-stu-id="b1f32-184">Networking settings</span></span>
<span data-ttu-id="b1f32-185">Quando a conectividade do computador Windows com a internet for através de um servidor proxy, as configurações de proxy também podem ser fornecidas para o agente.</span><span class="sxs-lookup"><span data-stu-id="b1f32-185">When the connectivity of the Windows machine to the internet is through a proxy server, the proxy settings can also be provided to the agent.</span></span> <span data-ttu-id="b1f32-186">Neste exemplo, não há nenhum servidor proxy, por isso estamos explicitamente omitindo todas as informações relacionadas a proxy.</span><span class="sxs-lookup"><span data-stu-id="b1f32-186">In this example, there is no proxy server, so we are explicitly clearing any proxy-related information.</span></span>

<span data-ttu-id="b1f32-187">O uso de largura de banda também pode ser controlado com as opções de ```work hour bandwidth``` e ```non-work hour bandwidth``` para um determinado conjunto de dias da semana.</span><span class="sxs-lookup"><span data-stu-id="b1f32-187">Bandwidth usage can also be controlled with the options of ```work hour bandwidth``` and ```non-work hour bandwidth``` for a given set of days of the week.</span></span>

<span data-ttu-id="b1f32-188">A configuração dos detalhes de proxy e largura de banda é feita usando o [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b1f32-188">Setting the proxy and bandwidth details is done using the [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a><span data-ttu-id="b1f32-189">Configurações de criptografia</span><span class="sxs-lookup"><span data-stu-id="b1f32-189">Encryption settings</span></span>
<span data-ttu-id="b1f32-190">Os dados de backup enviados para o Backup do Azure são criptografados para proteger a confidencialidade dos dados.</span><span class="sxs-lookup"><span data-stu-id="b1f32-190">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span></span> <span data-ttu-id="b1f32-191">A senha de criptografia é a "senha" para descriptografar os dados no momento da restauração.</span><span class="sxs-lookup"><span data-stu-id="b1f32-191">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span></span>

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
PS C:\> $PassPhrase = ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force 
PS C:\> $PassCode   = 'AzureR0ckx'
PS C:\> Set-OBMachineSetting -EncryptionPassPhrase $PassPhrase
Server properties updated successfully
```

> [!IMPORTANT]
> <span data-ttu-id="b1f32-192">Mantenha as informações de senha seguras e protegidas depois de defini-las.</span><span class="sxs-lookup"><span data-stu-id="b1f32-192">Keep the passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="b1f32-193">Você não pode restaurar os dados do Azure sem essa frase secreta.</span><span class="sxs-lookup"><span data-stu-id="b1f32-193">You are not be able to restore data from Azure without this passphrase.</span></span>
>
>

## <a name="back-up-files-and-folders"></a><span data-ttu-id="b1f32-194">Fazer backup de arquivos e pastas</span><span class="sxs-lookup"><span data-stu-id="b1f32-194">Back up files and folders</span></span>
<span data-ttu-id="b1f32-195">Todos os backups de Windows Servers e de clientes para o Backup do Azure são controlados por uma política.</span><span class="sxs-lookup"><span data-stu-id="b1f32-195">All backups from Windows Servers and clients to Azure Backup are governed by a policy.</span></span> <span data-ttu-id="b1f32-196">A política consiste em três partes:</span><span class="sxs-lookup"><span data-stu-id="b1f32-196">The policy comprises three parts:</span></span>

1. <span data-ttu-id="b1f32-197">Um **agendamento de backup** que especifica quando backups precisam ser efetuados e sincronizados com o serviço.</span><span class="sxs-lookup"><span data-stu-id="b1f32-197">A **backup schedule** that specifies when backups need to be taken and synchronized with the service.</span></span>
2. <span data-ttu-id="b1f32-198">Um **cronograma de retenção** que especifica quanto tempo deve-se manter os pontos de recuperação no Azure.</span><span class="sxs-lookup"><span data-stu-id="b1f32-198">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span></span>
3. <span data-ttu-id="b1f32-199">Uma **especificação de inclusão/exclusão de arquivo** que determina de que conteúdo deve-se realizar o backup.</span><span class="sxs-lookup"><span data-stu-id="b1f32-199">A **file inclusion/exclusion specification** that dictates what should be backed up.</span></span>

<span data-ttu-id="b1f32-200">Neste documento, já que estamos automatizando o backup, vamos pressupor que nada foi configurado.</span><span class="sxs-lookup"><span data-stu-id="b1f32-200">In this document, since we're automating backup, we'll assume nothing has been configured.</span></span> <span data-ttu-id="b1f32-201">Começamos pela criação de uma nova política de backup usando o cmdlet [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) .</span><span class="sxs-lookup"><span data-stu-id="b1f32-201">We begin by creating a new backup policy using the [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet.</span></span>

```
PS C:\> $newpolicy = New-OBPolicy
```

<span data-ttu-id="b1f32-202">Neste momento, a política está vazia e outros cmdlets são necessários para definir quais itens serão incluídos ou excluídos, quando backups serão executados e onde os backups serão armazenados.</span><span class="sxs-lookup"><span data-stu-id="b1f32-202">At this time the policy is empty and other cmdlets are needed to define what items will be included or excluded, when backups will run, and where the backups will be stored.</span></span>

### <a name="configuring-the-backup-schedule"></a><span data-ttu-id="b1f32-203">Configurando o agendamento de backup</span><span class="sxs-lookup"><span data-stu-id="b1f32-203">Configuring the backup schedule</span></span>
<span data-ttu-id="b1f32-204">A primeira das três partes de uma política é o agendamento de backup, que é criado usando o cmdlet [New-OBSchedule](https://technet.microsoft.com/library/hh770401) .</span><span class="sxs-lookup"><span data-stu-id="b1f32-204">The first of the 3 parts of a policy is the backup schedule, which is created using the [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span></span> <span data-ttu-id="b1f32-205">O agendamento de backup define quando os backups precisam ser executados.</span><span class="sxs-lookup"><span data-stu-id="b1f32-205">The backup schedule defines when backups need to be taken.</span></span> <span data-ttu-id="b1f32-206">Ao criar um agendamento, você precisa especificar dois parâmetros de entrada:</span><span class="sxs-lookup"><span data-stu-id="b1f32-206">When creating a schedule you need to specify 2 input parameters:</span></span>

* <span data-ttu-id="b1f32-207">**dias da semana** nos quais o backup deve ser executado.</span><span class="sxs-lookup"><span data-stu-id="b1f32-207">**Days of the week** that the backup should run.</span></span> <span data-ttu-id="b1f32-208">Você pode executar o trabalho de backup em apenas um dia ou em todos os dias da semana, ou qualquer combinação entre essas opções.</span><span class="sxs-lookup"><span data-stu-id="b1f32-208">You can run the backup job on just one day, or every day of the week, or any combination in between.</span></span>
* <span data-ttu-id="b1f32-209">**horários do dia** quando o backup deve ser executado.</span><span class="sxs-lookup"><span data-stu-id="b1f32-209">**Times of the day** when the backup should run.</span></span> <span data-ttu-id="b1f32-210">Você pode definir até três horários do dia diferentes quando o backup será disparado.</span><span class="sxs-lookup"><span data-stu-id="b1f32-210">You can define up to 3 different times of the day when the backup will be triggered.</span></span>

<span data-ttu-id="b1f32-211">Por exemplo, você poderia configurar uma política de backup que é executada às 16h todo sábado e domingo.</span><span class="sxs-lookup"><span data-stu-id="b1f32-211">For instance, you could configure a backup policy that runs at 4PM every Saturday and Sunday.</span></span>

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

<span data-ttu-id="b1f32-212">O agendamento de backup deve ser associado a uma política, e isso pode ser realizado usando o cmdlet [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) .</span><span class="sxs-lookup"><span data-stu-id="b1f32-212">The backup schedule needs to be associated with a policy, and this can be achieved by using the [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span></span>

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a><span data-ttu-id="b1f32-213">Configurando uma política de retenção</span><span class="sxs-lookup"><span data-stu-id="b1f32-213">Configuring a retention policy</span></span>
<span data-ttu-id="b1f32-214">A política de retenção define por quanto tempo os pontos de recuperação criados por meio de trabalhos de backup são mantidos.</span><span class="sxs-lookup"><span data-stu-id="b1f32-214">The retention policy defines how long recovery points created from backup jobs are retained.</span></span> <span data-ttu-id="b1f32-215">Ao criar uma nova política de retenção usando o cmdlet [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) , você pode especificar o número de dias durante os quais os pontos de recuperação de backup precisam ser mantidos com o Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="b1f32-215">When creating a new retention policy using the [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, you can specify the number of days that the backup recovery points need to be retained with Azure Backup.</span></span> <span data-ttu-id="b1f32-216">O exemplo a seguir define uma política de retenção de sete dias.</span><span class="sxs-lookup"><span data-stu-id="b1f32-216">The example below sets a retention policy of 7 days.</span></span>

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

<span data-ttu-id="b1f32-217">A política de retenção deve ser associada à política principal usando o cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span><span class="sxs-lookup"><span data-stu-id="b1f32-217">The retention policy must be associated with the main policy using the cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span></span>

```
PS C:\> Set-OBRetentionPolicy -Policy $newpolicy -RetentionPolicy $retentionpolicy

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          :
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```
### <a name="including-and-excluding-files-to-be-backed-up"></a><span data-ttu-id="b1f32-218">Incluindo e excluindo arquivos destinados a backup</span><span class="sxs-lookup"><span data-stu-id="b1f32-218">Including and excluding files to be backed up</span></span>
<span data-ttu-id="b1f32-219">Um objeto ```OBFileSpec``` define os arquivos a serem incluídos e excluídos em um backup.</span><span class="sxs-lookup"><span data-stu-id="b1f32-219">An ```OBFileSpec``` object defines the files to be included and excluded in a backup.</span></span> <span data-ttu-id="b1f32-220">Este é um conjunto de regras que definem o escopo dos arquivos e pastas protegidos em um computador.</span><span class="sxs-lookup"><span data-stu-id="b1f32-220">This is a set of rules that scope out the protected files and folders on a machine.</span></span> <span data-ttu-id="b1f32-221">Você pode ter muitas regras de inclusão ou exclusão de arquivos conforme necessário e associá-las a uma política.</span><span class="sxs-lookup"><span data-stu-id="b1f32-221">You can have as many file inclusion or exclusion rules as required, and associate them with a policy.</span></span> <span data-ttu-id="b1f32-222">Ao criar um novo objeto OBFileSpec, você pode:</span><span class="sxs-lookup"><span data-stu-id="b1f32-222">When creating a new OBFileSpec object, you can:</span></span>

* <span data-ttu-id="b1f32-223">Especificar os arquivos e pastas a serem incluídos</span><span class="sxs-lookup"><span data-stu-id="b1f32-223">Specify the files and folders to be included</span></span>
* <span data-ttu-id="b1f32-224">Especificar os arquivos e pastas a serem excluídos</span><span class="sxs-lookup"><span data-stu-id="b1f32-224">Specify the files and folders to be excluded</span></span>
* <span data-ttu-id="b1f32-225">Especificar o backup recursivo de dados em uma pasta ou o backup apenas dos arquivos de nível superior na pasta especificada.</span><span class="sxs-lookup"><span data-stu-id="b1f32-225">Specify recursive backup of data in a folder (or) whether only the top-level files in the specified folder should be backed up.</span></span>

<span data-ttu-id="b1f32-226">A última opção é obtida usando o sinalizador -NonRecursive no comando New-OBFileSpec.</span><span class="sxs-lookup"><span data-stu-id="b1f32-226">The latter is achieved by using the -NonRecursive flag in the New-OBFileSpec command.</span></span>

<span data-ttu-id="b1f32-227">No exemplo a seguir, vamos fazer backup dos volumes C: e D: e excluir os binários do sistema operacional na pasta do Windows e em quaisquer pastas temporárias.</span><span class="sxs-lookup"><span data-stu-id="b1f32-227">In the example below, we'll back up volume C: and D: and exclude the OS binaries in the Windows folder and any temporary folders.</span></span> <span data-ttu-id="b1f32-228">Para isso, vamos criar duas especificações de arquivo usando o cmdlet [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) – uma para inclusão e outra para exclusão.</span><span class="sxs-lookup"><span data-stu-id="b1f32-228">To do so we'll create two file specifications using the [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - one for inclusion and one for exclusion.</span></span> <span data-ttu-id="b1f32-229">Depois que as especificações de arquivo são criadas, elas são associadas à política usando o cmdlet [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) .</span><span class="sxs-lookup"><span data-stu-id="b1f32-229">Once the file specifications have been created, they're associated with the policy using the [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span></span>

```
PS C:\> $inclusions = New-OBFileSpec -FileSpec @("C:\", "D:\")

PS C:\> $exclusions = New-OBFileSpec -FileSpec @("C:\windows", "C:\temp") -Exclude

PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $inclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid


PS C:\> Add-OBFileSpec -Policy $newpolicy -FileSpec $exclusions

BackupSchedule  : 4:00 PM
                  Saturday, Sunday,
                  Every 1 week(s)
DsList          : {DataSource
                  DatasourceId:0
                  Name:C:\
                  FileSpec:FileSpec
                  FileSpec:C:\
                  IsExclude:False
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\windows
                  IsExclude:True
                  IsRecursive:True
                  ,FileSpec
                  FileSpec:C:\temp
                  IsExclude:True
                  IsRecursive:True

                  , DataSource
                  DatasourceId:0
                  Name:D:\
                  FileSpec:FileSpec
                  FileSpec:D:\
                  IsExclude:False
                  IsRecursive:True

                  }
PolicyName      :
RetentionPolicy : Retention Days : 7

                  WeeklyLTRSchedule :
                  Weekly schedule is not set

                  MonthlyLTRSchedule :
                  Monthly schedule is not set

                  YearlyLTRSchedule :
                  Yearly schedule is not set

State           : New
PolicyState     : Valid
```

### <a name="applying-the-policy"></a><span data-ttu-id="b1f32-230">Aplicando a política</span><span class="sxs-lookup"><span data-stu-id="b1f32-230">Applying the policy</span></span>
<span data-ttu-id="b1f32-231">Agora, o objeto de política está concluído e tem um agendamento de backup associado, política de retenção e uma lista de inclusão/exclusões de arquivos.</span><span class="sxs-lookup"><span data-stu-id="b1f32-231">Now the policy object is complete and has an associated backup schedule, retention policy, and an inclusion/exclusion list of files.</span></span> <span data-ttu-id="b1f32-232">Esta política agora pode ser confirmada para uso pelo Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="b1f32-232">This policy can now be committed for Azure Backup to use.</span></span> <span data-ttu-id="b1f32-233">Antes de aplicar a política recém-criada, verifique se não há nenhuma política de backup existente associada ao servidor, por meio do cmdlet [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) .</span><span class="sxs-lookup"><span data-stu-id="b1f32-233">Before you apply the newly created policy ensure that there are no existing backup policies associated with the server by using the [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span></span> <span data-ttu-id="b1f32-234">Remover a política gerará uma solicitação de confirmação.</span><span class="sxs-lookup"><span data-stu-id="b1f32-234">Removing the policy will prompt for confirmation.</span></span> <span data-ttu-id="b1f32-235">Para ignorar a confirmação, use o sinalizador ```-Confirm:$false``` com o cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b1f32-235">To skip the confirmation use the ```-Confirm:$false``` flag with the cmdlet.</span></span>

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want to remove this backup policy? This will delete all the backed up data. [Y] Yes [A] Yes to All [N] No [L] No to All [S] Suspend [?] Help (default is "Y"):
```

<span data-ttu-id="b1f32-236">A confirmação do objeto de política é realizada usando o cmdlet [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) .</span><span class="sxs-lookup"><span data-stu-id="b1f32-236">Committing the policy object is done using the [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span></span> <span data-ttu-id="b1f32-237">Isso também gerará uma solicitação de confirmação.</span><span class="sxs-lookup"><span data-stu-id="b1f32-237">This will also ask for confirmation.</span></span> <span data-ttu-id="b1f32-238">Para ignorar a confirmação, use o sinalizador ```-Confirm:$false``` com o cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b1f32-238">To skip the confirmation use the ```-Confirm:$false``` flag with the cmdlet.</span></span>

```
PS C:> Set-OBPolicy -Policy $newpolicy
Microsoft Azure Backup Do you want to save this backup policy ? [Y] Yes [A] Yes to All [N] No [L] No to All [S] Suspend [?] Help (default is "Y"):
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s)
DsList : {DataSource
         DatasourceId:4508156004108672185
         Name:C:\
         FileSpec:FileSpec
         FileSpec:C:\
         IsExclude:False
         IsRecursive:True,

         FileSpec
         FileSpec:C:\windows
         IsExclude:True
         IsRecursive:True,

         FileSpec
         FileSpec:C:\temp
         IsExclude:True
         IsRecursive:True,

         DataSource
         DatasourceId:4508156005178868542
         Name:D:\
         FileSpec:FileSpec
         FileSpec:D:\
         IsExclude:False
         IsRecursive:True
    }
PolicyName : c2eb6568-8a06-49f4-a20e-3019ae411bac
RetentionPolicy : Retention Days : 7
              WeeklyLTRSchedule :
              Weekly schedule is not set

              MonthlyLTRSchedule :
              Monthly schedule is not set

              YearlyLTRSchedule :
              Yearly schedule is not set
State : Existing PolicyState : Valid
```

<span data-ttu-id="b1f32-239">Você pode exibir os detalhes da política de backup existente usando o cmdlet [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) .</span><span class="sxs-lookup"><span data-stu-id="b1f32-239">You can view the details of the existing backup policy using the [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span></span> <span data-ttu-id="b1f32-240">Você pode detalhar mais usando o cmdlet [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) para o agendamento de backup e o cmdlet [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) para as políticas de retenção</span><span class="sxs-lookup"><span data-stu-id="b1f32-240">You can drill-down further using the [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet for the backup schedule and the [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet for the retention policies</span></span>

```
PS C:> Get-OBPolicy | Get-OBSchedule
SchedulePolicyName : 71944081-9950-4f7e-841d-32f0a0a1359a
ScheduleRunDays : {Saturday, Sunday}
ScheduleRunTimes : {16:00:00}
State : Existing

PS C:> Get-OBPolicy | Get-OBRetentionPolicy
RetentionDays : 7
RetentionPolicyName : ca3574ec-8331-46fd-a605-c01743a5265e
State : Existing

PS C:> Get-OBPolicy | Get-OBFileSpec
FileName : *
FilePath : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
FileSpec : D:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\
FileSpec : C:\
IsExclude : False
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\windows
FileSpec : C:\windows
IsExclude : True
IsRecursive : True

FileName : *
FilePath : \?\Volume{cdd41007-a22f-11e2-be6c-806e6f6e6963}\temp
FileSpec : C:\temp
IsExclude : True
IsRecursive : True
```

### <a name="performing-an-ad-hoc-backup"></a><span data-ttu-id="b1f32-241">Executando um backup ad hoc</span><span class="sxs-lookup"><span data-stu-id="b1f32-241">Performing an ad-hoc backup</span></span>
<span data-ttu-id="b1f32-242">Depois de definir uma política de backup, os backups ocorrerão de acordo com o agendamento.</span><span class="sxs-lookup"><span data-stu-id="b1f32-242">Once a backup policy has been set the backups will occur per the schedule.</span></span> <span data-ttu-id="b1f32-243">Disparar um backup ad hoc também é possível usando o cmdlet [Start-OBBackup](https://technet.microsoft.com/library/hh770426) :</span><span class="sxs-lookup"><span data-stu-id="b1f32-243">Triggering an ad-hoc backup is also possible using the [Start-OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span></span>

```
PS C:> Get-OBPolicy | Start-OBBackup
Initializing
Taking snapshot of volumes...
Preparing storage...
Generating backup metadata information and preparing the metadata VHD...
Data transfer is in progress. It might take longer since it is the first backup and all data needs to be transferred...
Data transfer completed and all backed up data is in the cloud. Verifying data integrity...
Data transfer completed
In progress...
Job completed.
The backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a><span data-ttu-id="b1f32-244">Restaurar dados por meio do Backup do Azure</span><span class="sxs-lookup"><span data-stu-id="b1f32-244">Restore data from Azure Backup</span></span>
<span data-ttu-id="b1f32-245">Esta seção o orientará pelas etapas para automatizar a recuperação de dados por meio do Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="b1f32-245">This section will guide you through the steps for automating recovery of data from Azure Backup.</span></span> <span data-ttu-id="b1f32-246">Isso envolve as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="b1f32-246">Doing so involves the following steps:</span></span>

1. <span data-ttu-id="b1f32-247">Selecionar o volume de origem</span><span class="sxs-lookup"><span data-stu-id="b1f32-247">Pick the source volume</span></span>
2. <span data-ttu-id="b1f32-248">Escolher um ponto de backup para restaurar</span><span class="sxs-lookup"><span data-stu-id="b1f32-248">Choose a backup point to restore</span></span>
3. <span data-ttu-id="b1f32-249">Escolha um item para restaurar</span><span class="sxs-lookup"><span data-stu-id="b1f32-249">Choose an item to restore</span></span>
4. <span data-ttu-id="b1f32-250">Disparar o processo de restauração</span><span class="sxs-lookup"><span data-stu-id="b1f32-250">Trigger the restore process</span></span>

### <a name="picking-the-source-volume"></a><span data-ttu-id="b1f32-251">Selecionar o volume de fonte</span><span class="sxs-lookup"><span data-stu-id="b1f32-251">Picking the source volume</span></span>
<span data-ttu-id="b1f32-252">Para restaurar um item por meio do Backup do Azure, é necessário primeiro identificar a fonte do item.</span><span class="sxs-lookup"><span data-stu-id="b1f32-252">In order to restore an item from Azure Backup, you first need to identify the source of the item.</span></span> <span data-ttu-id="b1f32-253">Como estamos executando os comandos no contexto de um Windows Server ou um cliente Windows, o computador já foi identificado.</span><span class="sxs-lookup"><span data-stu-id="b1f32-253">Since we're executing the commands in the context of a Windows Server or a Windows client, the machine is already identified.</span></span> <span data-ttu-id="b1f32-254">A próxima etapa para identificação da origem é identificar o volume que a contém.</span><span class="sxs-lookup"><span data-stu-id="b1f32-254">The next step in identifying the source is to identify the volume containing it.</span></span> <span data-ttu-id="b1f32-255">É possível recuperar uma lista de volumes ou fontes cujo backup está sendo executado neste computador pela execução do cmdlet [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) .</span><span class="sxs-lookup"><span data-stu-id="b1f32-255">A list of volumes or sources being backed up from this machine can be retrieved by executing the [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span></span> <span data-ttu-id="b1f32-256">Esse comando retorna uma matriz de todas as fontes desse servidor/cliente cujo backup foi executado.</span><span class="sxs-lookup"><span data-stu-id="b1f32-256">This command returns an array of all the sources backed up from this server/client.</span></span>

```
PS C:> $source = Get-OBRecoverableSource
PS C:> $source
FriendlyName : C:\
RecoverySourceName : C:\
ServerName : myserver.microsoft.com

FriendlyName : D:\
RecoverySourceName : D:\
ServerName : myserver.microsoft.com
```

### <a name="choosing-a-backup-point-from-which-to-restore"></a><span data-ttu-id="b1f32-257">Escolhendo um ponto de backup do qual restaurar</span><span class="sxs-lookup"><span data-stu-id="b1f32-257">Choosing a backup point from which to restore</span></span>
<span data-ttu-id="b1f32-258">Você recupera uma lista de pontos de backup ao executar o cmdlet [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) com os parâmetros apropriados.</span><span class="sxs-lookup"><span data-stu-id="b1f32-258">You retreive a list of backup points by executing the [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet with appropriate parameters.</span></span> <span data-ttu-id="b1f32-259">Em nosso exemplo, escolheremos o último ponto de backup para o volume de fonte *D:* e o usaremos para recuperar um arquivo específico.</span><span class="sxs-lookup"><span data-stu-id="b1f32-259">In our example, we’ll choose the latest backup point for the source volume *D:* and use it to recover a specific file.</span></span>

```
PS C:> $rps = Get-OBRecoverableItem -Source $source[1]
IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :

IsDir : False
ItemNameFriendly : D:\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\
LocalMountPoint : D:\
MountPointName : D:\
Name : D:\
PointInTime : 17-Jun-15 6:31:31 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime :
```
<span data-ttu-id="b1f32-260">O objeto ```$rps``` é uma matriz de pontos de backup.</span><span class="sxs-lookup"><span data-stu-id="b1f32-260">The object ```$rps``` is an array of backup points.</span></span> <span data-ttu-id="b1f32-261">O primeiro elemento é o ponto mais recente e o enésimo elemento é o ponto mais antigo.</span><span class="sxs-lookup"><span data-stu-id="b1f32-261">The first element is the latest point and the Nth element is the oldest point.</span></span> <span data-ttu-id="b1f32-262">Para escolher o último ponto, usaremos ```$rps[0]```.</span><span class="sxs-lookup"><span data-stu-id="b1f32-262">To choose the latest point, we will use ```$rps[0]```.</span></span>

### <a name="choosing-an-item-to-restore"></a><span data-ttu-id="b1f32-263">Escolhendo um item para restaurar</span><span class="sxs-lookup"><span data-stu-id="b1f32-263">Choosing an item to restore</span></span>
<span data-ttu-id="b1f32-264">Para identificar o arquivo ou pasta exato a ser restaurado, use recursivamente o cmdlet [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) .</span><span class="sxs-lookup"><span data-stu-id="b1f32-264">To identify the exact file or folder to restore, recursively use the [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span></span> <span data-ttu-id="b1f32-265">Desse modo, a hierarquia de pastas pode ser pesquisada usando somente o ```Get-OBRecoverableItem```.</span><span class="sxs-lookup"><span data-stu-id="b1f32-265">That way the folder hierarchy can be browsed solely using the ```Get-OBRecoverableItem```.</span></span>

<span data-ttu-id="b1f32-266">Neste exemplo, se quisermos restaurar o arquivo *finances.xls*, poderemos fazer referência a ele usando o objeto ```$filesFolders[1]```.</span><span class="sxs-lookup"><span data-stu-id="b1f32-266">In this example, if we want to restore the file *finances.xls* we can reference that using the object ```$filesFolders[1]```.</span></span>

```
PS C:> $filesFolders = Get-OBRecoverableItem $rps[0]
PS C:> $filesFolders
IsDir : True
ItemNameFriendly : D:\MyData\
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\
LocalMountPoint : D:\
MountPointName : D:\
Name : MyData
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize :
ItemLastModifiedTime : 15-Jun-15 8:49:29 AM

PS C:> $filesFolders = Get-OBRecoverableItem $filesFolders[0]
PS C:> $filesFolders
IsDir : False
ItemNameFriendly : D:\MyData\screenshot.oxps
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\screenshot.oxps
LocalMountPoint : D:\
MountPointName : D:\
Name : screenshot.oxps
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 228313
ItemLastModifiedTime : 21-Jun-14 6:45:09 AM

IsDir : False
ItemNameFriendly : D:\MyData\finances.xls
ItemNameGuid : \?\Volume{b835d359-a1dd-11e2-be72-2016d8d89f0f}\MyData\finances.xls
LocalMountPoint : D:\
MountPointName : D:\
Name : finances.xls
PointInTime : 18-Jun-15 6:41:52 AM
ServerName : myserver.microsoft.com
ItemSize : 96256
ItemLastModifiedTime : 21-Jun-14 6:43:02 AM
```

<span data-ttu-id="b1f32-267">Você também pode procurar itens a serem restaurados usando o cmdlet ```Get-OBRecoverableItem``` .</span><span class="sxs-lookup"><span data-stu-id="b1f32-267">You can also search for items to restore using the ```Get-OBRecoverableItem``` cmdlet.</span></span> <span data-ttu-id="b1f32-268">Em nosso exemplo, para procurar *finances.xls* , poderíamos obter um identificador no arquivo executando esse comando:</span><span class="sxs-lookup"><span data-stu-id="b1f32-268">In our example, to search for *finances.xls* we could get a handle on the file by running this command:</span></span>

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-the-restore-process"></a><span data-ttu-id="b1f32-269">Disparando o processo de restauração</span><span class="sxs-lookup"><span data-stu-id="b1f32-269">Triggering the restore process</span></span>
<span data-ttu-id="b1f32-270">Para disparar o processo de restauração, primeiro precisamos especificar as opções de recuperação.</span><span class="sxs-lookup"><span data-stu-id="b1f32-270">To trigger the restore process, we first need to specify the recovery options.</span></span> <span data-ttu-id="b1f32-271">Isso pode ser feito usando o cmdlet [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) .</span><span class="sxs-lookup"><span data-stu-id="b1f32-271">This can be done by using the [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span></span> <span data-ttu-id="b1f32-272">Para este exemplo, iremos supor que queremos restaurar os arquivos para *C:\temp*. Iremos supor também que queremos ignorar os arquivos que já existem na pasta de destino *C:\temp*. Para criar uma opção de recuperação desse tipo, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="b1f32-272">For this example, let's assume that we want to restore the files to *C:\temp*. Let's also assume that we want to skip files that already exist on the destination folder *C:\temp*. To create such a recovery option, use the following command:</span></span>

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

<span data-ttu-id="b1f32-273">Agora dispare o processo de restauração usando o comando [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) no ```$item``` selecionado na saída do cmdlet ```Get-OBRecoverableItem```:</span><span class="sxs-lookup"><span data-stu-id="b1f32-273">Now trigger the restore process by using the [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) command on the selected ```$item``` from the output of the ```Get-OBRecoverableItem``` cmdlet:</span></span>

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
The recovery operation completed successfully.
```


## <a name="uninstalling-the-azure-backup-agent"></a><span data-ttu-id="b1f32-274">Desinstalando o agente de Backup do Azure</span><span class="sxs-lookup"><span data-stu-id="b1f32-274">Uninstalling the Azure Backup agent</span></span>
<span data-ttu-id="b1f32-275">A desinstalação do agente de Backup do Azure pode ser feita usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="b1f32-275">Uninstalling the Azure Backup agent can be done by using the following command:</span></span>

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

<span data-ttu-id="b1f32-276">Antes de desinstalar os binários do agente do computador, é necessário considerar algumas consequências:</span><span class="sxs-lookup"><span data-stu-id="b1f32-276">Uninstalling the agent binaries from the machine has some consequences to consider:</span></span>

* <span data-ttu-id="b1f32-277">A desinstalação remove o filtro de arquivo do computador e interrompe o acompanhamento de alterações.</span><span class="sxs-lookup"><span data-stu-id="b1f32-277">It removes the file-filter from the machine, and tracking of changes is stopped.</span></span>
* <span data-ttu-id="b1f32-278">Todas as informações de política são removidas do computador, mas as informações de política continuam sendo armazenadas no serviço.</span><span class="sxs-lookup"><span data-stu-id="b1f32-278">All policy information is removed from the machine, but the policy information continues to be stored in the service.</span></span>
* <span data-ttu-id="b1f32-279">Todos os agendamentos de backup são removidos e nenhum backup posterior é realizado.</span><span class="sxs-lookup"><span data-stu-id="b1f32-279">All backup schedules are removed, and no further backups are taken.</span></span>

<span data-ttu-id="b1f32-280">No entanto, os dados armazenados no Azure permanecem e são mantidos de acordo com a política de retenção configurada por você.</span><span class="sxs-lookup"><span data-stu-id="b1f32-280">However, the data stored in Azure remains and is retained as per the retention policy setup by you.</span></span> <span data-ttu-id="b1f32-281">Os pontos mais antigos são desatualizados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b1f32-281">Older points are automatically aged out.</span></span>

## <a name="remote-management"></a><span data-ttu-id="b1f32-282">Gerenciamento remoto</span><span class="sxs-lookup"><span data-stu-id="b1f32-282">Remote management</span></span>
<span data-ttu-id="b1f32-283">Todo o gerenciamento relacionado ao agente, às políticas e às fontes de dados do Backup do Azure pode ser feito remotamente por meio do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b1f32-283">All the management around the Azure Backup agent, policies, and data sources can be done remotely through PowerShell.</span></span> <span data-ttu-id="b1f32-284">A máquina que será gerenciada remotamente precisa ser preparada corretamente.</span><span class="sxs-lookup"><span data-stu-id="b1f32-284">The machine that will be managed remotely needs to be prepared correctly.</span></span>

<span data-ttu-id="b1f32-285">Por padrão, o serviço WinRM é configurado para inicialização manual.</span><span class="sxs-lookup"><span data-stu-id="b1f32-285">By default, the WinRM service is configured for manual startup.</span></span> <span data-ttu-id="b1f32-286">O tipo de inicialização deve ser definido como *Automático* e o serviço deve ser iniciado.</span><span class="sxs-lookup"><span data-stu-id="b1f32-286">The startup type must be set to *Automatic* and the service should be started.</span></span> <span data-ttu-id="b1f32-287">Para verificar se o serviço WinRM está em execução, o valor da propriedade Status deve ser *Em execução*.</span><span class="sxs-lookup"><span data-stu-id="b1f32-287">To verify that the WinRM service is running, the value of the Status property should be *Running*.</span></span>

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

<span data-ttu-id="b1f32-288">O PowerShell deve ser configurado remotamente.</span><span class="sxs-lookup"><span data-stu-id="b1f32-288">PowerShell should be configured for remoting.</span></span>

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up to receive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

<span data-ttu-id="b1f32-289">O computador agora pode ser gerenciado remotamente - começando na instalação do agente.</span><span class="sxs-lookup"><span data-stu-id="b1f32-289">The machine can now be managed remotely - starting from the installation of the agent.</span></span> <span data-ttu-id="b1f32-290">Por exemplo, o script a seguir copia o agente para o computador remoto e o instala.</span><span class="sxs-lookup"><span data-stu-id="b1f32-290">For example, the following script copies the agent to the remote machine and installs it.</span></span>

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a><span data-ttu-id="b1f32-291">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b1f32-291">Next steps</span></span>
<span data-ttu-id="b1f32-292">Para obter mais informações sobre o Backup do Azure para Windows Server/Client, consulte</span><span class="sxs-lookup"><span data-stu-id="b1f32-292">For more information about Azure Backup for Windows Server/Client see</span></span>

* [<span data-ttu-id="b1f32-293">Introdução ao Backup do Azure</span><span class="sxs-lookup"><span data-stu-id="b1f32-293">Introduction to Azure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="b1f32-294">Fazer backup de servidores Windows</span><span class="sxs-lookup"><span data-stu-id="b1f32-294">Back up Windows Servers</span></span>](backup-configure-vault.md)
