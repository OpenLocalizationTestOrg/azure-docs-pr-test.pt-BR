---
title: aaaUse PowerShell tooback backup do Windows Server tooAzure | Microsoft Docs
description: Saiba como toodeploy e gerenciar o Backup do Azure usando o PowerShell
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
ms.openlocfilehash: f13224f53abd6fbd132fee4347b0b99e8f5e2678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-windows-serverwindows-client-using-powershell"></a><span data-ttu-id="10a53-103">Implantar e gerenciar o backup tooAzure para o cliente do Windows Server/Windows usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="10a53-103">Deploy and manage backup tooAzure for Windows Server/Windows Client using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="10a53-104">ARM</span><span class="sxs-lookup"><span data-stu-id="10a53-104">ARM</span></span>](backup-client-automation.md)
> * [<span data-ttu-id="10a53-105">Clássico</span><span class="sxs-lookup"><span data-stu-id="10a53-105">Classic</span></span>](backup-client-automation-classic.md)
>
>

<span data-ttu-id="10a53-106">Este artigo mostra como toouse do PowerShell para configurar o Backup do Azure no Windows Server ou um cliente do Windows e gerenciamento de backup e recuperação.</span><span class="sxs-lookup"><span data-stu-id="10a53-106">This article shows you how toouse PowerShell for setting up Azure Backup on Windows Server or a Windows client, and managing backup and recovery.</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="10a53-107">Instalar o Azure Powershell</span><span class="sxs-lookup"><span data-stu-id="10a53-107">Install Azure PowerShell</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="10a53-108">Este artigo enfoca hello Azure Resource Manager (ARM) e Olá cmdlets do PowerShell de Backup Online da MS que permitem que você toouse um cofre de serviços de recuperação em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="10a53-108">This article focuses on hello Azure Resource Manager (ARM) and hello MS Online Backup PowerShell cmdlets that enable you toouse a Recovery Services vault in a resource group.</span></span>

<span data-ttu-id="10a53-109">Em outubro de 2015, o Azure PowerShell 1.0 foi lançado.</span><span class="sxs-lookup"><span data-stu-id="10a53-109">In October 2015, Azure PowerShell 1.0 was released.</span></span> <span data-ttu-id="10a53-110">Esta versão foi bem-sucedido versão Olá 0.9.8 e colocado sobre alterações significativas, especialmente no padrão de nomenclatura Olá Olá cmdlets.</span><span class="sxs-lookup"><span data-stu-id="10a53-110">This release succeeded hello 0.9.8 release and brought about some significant changes, especially in hello naming pattern of hello cmdlets.</span></span> <span data-ttu-id="10a53-111">Acompanhamento de cmdlets 1.0 Olá {verbo} padrão de nomenclatura-AzureRm {substantivo;} Por outro lado, não incluem nomes Olá 0.9.8 **Rm** (por exemplo, New-AzureRmResourceGroup em vez de New-AzureResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="10a53-111">1.0 cmdlets follow hello naming pattern {verb}-AzureRm{noun}; whereas, hello 0.9.8 names do not include **Rm** (for example, New-AzureRmResourceGroup instead of New-AzureResourceGroup).</span></span> <span data-ttu-id="10a53-112">Ao usar o Azure PowerShell 0.9.8, você primeiro deve habilitar o modo de Gerenciador de recursos de Olá executando Olá **Switch-AzureMode AzureResourceManager** comando.</span><span class="sxs-lookup"><span data-stu-id="10a53-112">When using Azure PowerShell 0.9.8, you must first enable hello Resource Manager mode by running hello **Switch-AzureMode AzureResourceManager** command.</span></span> <span data-ttu-id="10a53-113">Este comando não é necessário na 1.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="10a53-113">This command is not necessary in 1.0 or later.</span></span>

<span data-ttu-id="10a53-114">Se quiser toouse seus scripts escritos para o ambiente Olá 0.9.8, Olá 1.0 ou posterior ambiente, você deve atualizar cuidadosamente e testar scripts de saudação em um ambiente de pré-produção antes de usá-las na produção tooavoid impacto inesperado.</span><span class="sxs-lookup"><span data-stu-id="10a53-114">If you want toouse your scripts written for hello 0.9.8 environment, in hello 1.0 or later environment, you should carefully update and test hello scripts in a pre-production environment before using them in production tooavoid unexpected impact.</span></span>

<span data-ttu-id="10a53-115">[Baixar a versão mais recente de PowerShell Olá](https://github.com/Azure/azure-powershell/releases) (versão mínima necessária é: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="10a53-115">[Download hello latest PowerShell release](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="10a53-116">Criar um cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="10a53-116">Create a recovery services vault</span></span>
<span data-ttu-id="10a53-117">Olá etapas levá-lo na criação de um cofre de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="10a53-117">hello following steps lead you through creating a Recovery Services vault.</span></span> <span data-ttu-id="10a53-118">Um cofre dos Serviços de Recuperação é diferente de um cofre de Backup.</span><span class="sxs-lookup"><span data-stu-id="10a53-118">A Recovery Services vault is different than a Backup vault.</span></span>

1. <span data-ttu-id="10a53-119">Se você estiver usando o Backup do Azure para Olá primeira vez, você deve usar o hello **registro AzureRMResourceProvider** provedor de serviço de recuperação do Azure do cmdlet tooregister Olá com sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="10a53-119">If you are using Azure Backup for hello first time, you must use hello **Register-AzureRMResourceProvider** cmdlet tooregister hello Azure Recovery Service provider with your subscription.</span></span>

    ```
    PS C:\> Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.RecoveryServices"
    ```
2. <span data-ttu-id="10a53-120">Olá Cofre de serviços de recuperação é um recurso do ARM, portanto, você precisa tooplace-lo em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="10a53-120">hello Recovery Services vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="10a53-121">Você pode usar um grupo de recursos existente ou criar um novo.</span><span class="sxs-lookup"><span data-stu-id="10a53-121">You can use an existing resource group, or create a new one.</span></span> <span data-ttu-id="10a53-122">Ao criar um novo grupo de recursos, especifique o nome de saudação e local para o grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="10a53-122">When creating a new resource group, specify hello name and location for hello resource group.</span></span>  

    ```
    PS C:\> New-AzureRmResourceGroup –Name "test-rg" –Location "WestUS"
    ```
3. <span data-ttu-id="10a53-123">Saudação de uso **AzureRmRecoveryServicesVault novo** novo cofre do cmdlet toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="10a53-123">Use hello **New-AzureRmRecoveryServicesVault** cmdlet toocreate hello new vault.</span></span> <span data-ttu-id="10a53-124">Certifique-se de que toospecify Olá mesmo local para o cofre Olá que foi usada para o grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="10a53-124">Be sure toospecify hello same location for hello vault as was used for hello resource group.</span></span>

    ```
    PS C:\> New-AzureRmRecoveryServicesVault -Name "testvault" -ResourceGroupName " test-rg" -Location "WestUS"
    ```
4. <span data-ttu-id="10a53-125">Especificar o tipo de saudação do toouse de redundância de armazenamento; Você pode usar [armazenamento localmente redundante (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) ou [Geo redundante GRS (armazenamento)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="10a53-125">Specify hello type of storage redundancy toouse; you can use [Locally Redundant Storage (LRS)](../storage/common/storage-redundancy.md#locally-redundant-storage) or [Geo Redundant Storage (GRS)](../storage/common/storage-redundancy.md#geo-redundant-storage).</span></span> <span data-ttu-id="10a53-126">Olá exemplo a seguir mostra Olá - BackupStorageRedundancy opção testVault é definida tooGeoRedundant.</span><span class="sxs-lookup"><span data-stu-id="10a53-126">hello following example shows hello -BackupStorageRedundancy option for testVault is set tooGeoRedundant.</span></span>

   > [!TIP]
   > <span data-ttu-id="10a53-127">Muitos cmdlets do Backup do Azure exigem Olá objeto de Cofre de serviços de recuperação como entrada.</span><span class="sxs-lookup"><span data-stu-id="10a53-127">Many Azure Backup cmdlets require hello Recovery Services vault object as an input.</span></span> <span data-ttu-id="10a53-128">Por esse motivo, é conveniente toostore Olá serviços de recuperação de Backup cofre objeto em uma variável.</span><span class="sxs-lookup"><span data-stu-id="10a53-128">For this reason, it is convenient toostore hello Backup Recovery Services vault object in a variable.</span></span>
   >
   >

    ```
    PS C:\> $vault1 = Get-AzureRmRecoveryServicesVault –Name "testVault"
    PS C:\> Set-AzureRmRecoveryServicesBackupProperties  -vault $vault1 -BackupStorageRedundancy GeoRedundant
    ```

## <a name="view-hello-vaults-in-a-subscription"></a><span data-ttu-id="10a53-129">Exibição Olá cofres em uma assinatura</span><span class="sxs-lookup"><span data-stu-id="10a53-129">View hello vaults in a subscription</span></span>
<span data-ttu-id="10a53-130">Use **Get-AzureRmRecoveryServicesVault** tooview lista de saudação de todos os cofres na assinatura atual hello.</span><span class="sxs-lookup"><span data-stu-id="10a53-130">Use **Get-AzureRmRecoveryServicesVault** tooview hello list of all vaults in hello current subscription.</span></span> <span data-ttu-id="10a53-131">Você pode usar este toocheck de comando que um novo cofre foi criado ou toosee que cofres estão disponíveis na assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="10a53-131">You can use this command toocheck that a new  vault was created, or toosee what vaults are available in hello subscription.</span></span>

<span data-ttu-id="10a53-132">Execute o comando hello, **Get-AzureRmRecoveryServicesVault**, e todos os cofres na assinatura de saudação são listados.</span><span class="sxs-lookup"><span data-stu-id="10a53-132">Run hello command, **Get-AzureRmRecoveryServicesVault**, and all vaults in hello subscription are listed.</span></span>

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


## <a name="installing-hello-azure-backup-agent"></a><span data-ttu-id="10a53-133">Instalando o agente de Backup do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="10a53-133">Installing hello Azure Backup agent</span></span>
<span data-ttu-id="10a53-134">Antes de instalar o agente de Backup do Azure Olá, você precisará instalador de saudação toohave baixado e presente no saudação do Windows Server.</span><span class="sxs-lookup"><span data-stu-id="10a53-134">Before you install hello Azure Backup agent, you need toohave hello installer downloaded and present on hello Windows Server.</span></span> <span data-ttu-id="10a53-135">Você pode obter a versão mais recente de saudação do instalador de saudação de saudação [Microsoft Download Center](http://aka.ms/azurebackup_agent) ou da página de painel do Cofre de serviços de recuperação hello.</span><span class="sxs-lookup"><span data-stu-id="10a53-135">You can get hello latest version of hello installer from hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from hello Recovery Services vault's Dashboard page.</span></span> <span data-ttu-id="10a53-136">Salvar instalador Olá tooan local facilmente acessível, como * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="10a53-136">Save hello installer tooan easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="10a53-137">Como alternativa, use o downloader de saudação de tooget do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="10a53-137">Alternatively, use PowerShell tooget hello downloader:</span></span>
 
 ```
 $MarsAURL = 'Http://Aka.Ms/Azurebackup_Agent'
 $WC = New-Object System.Net.WebClient
 $WC.DownloadFile($MarsAURL,'C:\downloads\MARSAgentInstaller.EXE')
 C:\Downloads\MARSAgentInstaller.EXE /q
 ```

<span data-ttu-id="10a53-138">Agente de saudação tooinstall, executar Olá seguinte comando em um console do PowerShell com privilégios elevados:</span><span class="sxs-lookup"><span data-stu-id="10a53-138">tooinstall hello agent, run hello following command in an elevated PowerShell console:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="10a53-139">Isso instala o agente de saudação com todas as opções padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="10a53-139">This installs hello agent with all hello default options.</span></span> <span data-ttu-id="10a53-140">instalação de saudação leva alguns minutos no plano de fundo de saudação.</span><span class="sxs-lookup"><span data-stu-id="10a53-140">hello installation takes a few minutes in hello background.</span></span> <span data-ttu-id="10a53-141">Se você não especificar Olá */nu* em seguida, Olá **Windows Update** janela será aberta no final de saudação do hello instalação toocheck para todas as atualizações.</span><span class="sxs-lookup"><span data-stu-id="10a53-141">If you do not specify hello */nu* option then hello **Windows Update** window will open at hello end of hello installation toocheck for any updates.</span></span> <span data-ttu-id="10a53-142">Uma vez instalado, agente hello serão mostradas na lista Olá de programas instalados.</span><span class="sxs-lookup"><span data-stu-id="10a53-142">Once installed, hello agent will show in hello list of installed programs.</span></span>

<span data-ttu-id="10a53-143">lista de saudação toosee de instalado programas, consulte muito**painel de controle** > **programas** > **programas e recursos**.</span><span class="sxs-lookup"><span data-stu-id="10a53-143">toosee hello list of installed programs, go too**Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agente instalado](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="10a53-145">Opções de instalação</span><span class="sxs-lookup"><span data-stu-id="10a53-145">Installation options</span></span>
<span data-ttu-id="10a53-146">toosee todas as opções disponíveis por meio de Olá Olá de linha de comando, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="10a53-146">toosee all hello options available via hello command-line, use hello following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="10a53-147">Olá as opções disponíveis incluem:</span><span class="sxs-lookup"><span data-stu-id="10a53-147">hello available options include:</span></span>

| <span data-ttu-id="10a53-148">Opção</span><span class="sxs-lookup"><span data-stu-id="10a53-148">Option</span></span> | <span data-ttu-id="10a53-149">Detalhes</span><span class="sxs-lookup"><span data-stu-id="10a53-149">Details</span></span> | <span data-ttu-id="10a53-150">Padrão</span><span class="sxs-lookup"><span data-stu-id="10a53-150">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="10a53-151">/q</span><span class="sxs-lookup"><span data-stu-id="10a53-151">/q</span></span> |<span data-ttu-id="10a53-152">Instalação silenciosa</span><span class="sxs-lookup"><span data-stu-id="10a53-152">Quiet installation</span></span> |- |
| <span data-ttu-id="10a53-153">/p:"local"</span><span class="sxs-lookup"><span data-stu-id="10a53-153">/p:"location"</span></span> |<span data-ttu-id="10a53-154">Pasta de instalação de toohello de caminho para o agente de Backup do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="10a53-154">Path toohello installation folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="10a53-155">C:\Arquivos de Programas\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="10a53-155">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="10a53-156">/s:"local"</span><span class="sxs-lookup"><span data-stu-id="10a53-156">/s:"location"</span></span> |<span data-ttu-id="10a53-157">Pasta de cache de toohello de caminho para o agente de Backup do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="10a53-157">Path toohello cache folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="10a53-158">C:\Arquivos de Programas\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="10a53-158">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="10a53-159">/m</span><span class="sxs-lookup"><span data-stu-id="10a53-159">/m</span></span> |<span data-ttu-id="10a53-160">Aceitar tooMicrosoft atualização</span><span class="sxs-lookup"><span data-stu-id="10a53-160">Opt-in tooMicrosoft Update</span></span> |- |
| <span data-ttu-id="10a53-161">/nu</span><span class="sxs-lookup"><span data-stu-id="10a53-161">/nu</span></span> |<span data-ttu-id="10a53-162">Não verificar se há atualizações após a conclusão da instalação</span><span class="sxs-lookup"><span data-stu-id="10a53-162">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="10a53-163">/d</span><span class="sxs-lookup"><span data-stu-id="10a53-163">/d</span></span> |<span data-ttu-id="10a53-164">Desinstala o agente dos Serviços de Recuperação do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="10a53-164">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="10a53-165">/ph</span><span class="sxs-lookup"><span data-stu-id="10a53-165">/ph</span></span> |<span data-ttu-id="10a53-166">Endereço do host do proxy</span><span class="sxs-lookup"><span data-stu-id="10a53-166">Proxy Host Address</span></span> |- |
| <span data-ttu-id="10a53-167">/po</span><span class="sxs-lookup"><span data-stu-id="10a53-167">/po</span></span> |<span data-ttu-id="10a53-168">Número da porta do host do proxy</span><span class="sxs-lookup"><span data-stu-id="10a53-168">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="10a53-169">/pu</span><span class="sxs-lookup"><span data-stu-id="10a53-169">/pu</span></span> |<span data-ttu-id="10a53-170">UserName do host do proxy</span><span class="sxs-lookup"><span data-stu-id="10a53-170">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="10a53-171">/pw</span><span class="sxs-lookup"><span data-stu-id="10a53-171">/pw</span></span> |<span data-ttu-id="10a53-172">Senha do proxy</span><span class="sxs-lookup"><span data-stu-id="10a53-172">Proxy Password</span></span> |- |

## <a name="registering-windows-server-or-windows-client-machine-tooa-recovery-services-vault"></a><span data-ttu-id="10a53-173">Registro do Windows Server ou Windows client máquina tooa Cofre de serviços de recuperação</span><span class="sxs-lookup"><span data-stu-id="10a53-173">Registering Windows Server or Windows client machine tooa Recovery Services Vault</span></span>
<span data-ttu-id="10a53-174">Depois que você criar o Cofre de serviços de recuperação de Olá, baixe o agente mais recente hello e as credenciais do cofre hello e armazená-lo em um local conveniente como C:\Downloads.</span><span class="sxs-lookup"><span data-stu-id="10a53-174">After you created hello Recovery Services vault, download hello latest agent and hello vault credentials and store it in a convenient location like C:\Downloads.</span></span>

```
PS C:\> $credspath = "C:\downloads"
PS C:\> $credsfilename = Get-AzureRmRecoveryServicesVaultSettingsFile -Backup -Vault $vault1 -Path  $credspath
```

<span data-ttu-id="10a53-175">Saudação do Windows Server ou máquina cliente Windows, executar Olá [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet tooregister Olá máquina cofre hello.</span><span class="sxs-lookup"><span data-stu-id="10a53-175">On hello Windows Server or Windows client machine, run hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet tooregister hello machine with hello vault.</span></span>
<span data-ttu-id="10a53-176">Este e outros cmdlets usados para backup, são de um módulo MSONLINE Olá quais Olá Mars AgentInstaller adicionado como parte do processo de instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="10a53-176">This, and other cmdlets used for backup, are from hello MSONLINE module which hello Mars AgentInstaller added as part of hello installation process.</span></span> 

<span data-ttu-id="10a53-177">instalador do agente de saudação não atualizar Olá $Env: variável PSModulePath.</span><span class="sxs-lookup"><span data-stu-id="10a53-177">hello Agent installer does not update hello $Env:PSModulePath variable.</span></span> <span data-ttu-id="10a53-178">Isso significa que o carregamento automático do módulo falhará.</span><span class="sxs-lookup"><span data-stu-id="10a53-178">This means module auto-load fails.</span></span> <span data-ttu-id="10a53-179">tooresolve isso você pode fazer a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="10a53-179">tooresolve this you can do hello following:</span></span>

```
PS C:\>  $Env:psmodulepath += ';C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules
```

<span data-ttu-id="10a53-180">Como alternativa, você pode carregar manualmente Olá módulo em seu script da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="10a53-180">Alternatively, you can manually load hello module in your script as follows:</span></span>

```
PS C:\>  Import-Module  'C:\Program Files\Microsoft Azure Recovery Services Agent\bin\Modules\MSOnlineBackup'

```

<span data-ttu-id="10a53-181">Depois de carregar os cmdlets do Backup Online Olá, é registrar credenciais do cofre hello:</span><span class="sxs-lookup"><span data-stu-id="10a53-181">Once you load hello Online Backup cmdlets, you register hello vault credentials:</span></span>


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
> <span data-ttu-id="10a53-182">Não use o arquivo de credenciais de cofre do caminhos relativos toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="10a53-182">Do not use relative paths toospecify hello vault credentials file.</span></span> <span data-ttu-id="10a53-183">Você deve fornecer um caminho absoluto como um cmdlet toohello de entrada.</span><span class="sxs-lookup"><span data-stu-id="10a53-183">You must provide an absolute path as an input toohello cmdlet.</span></span>
>
>

## <a name="networking-settings"></a><span data-ttu-id="10a53-184">Configurações de rede</span><span class="sxs-lookup"><span data-stu-id="10a53-184">Networking settings</span></span>
<span data-ttu-id="10a53-185">Quando a conectividade de saudação do hello Windows máquina toohello que Internet é por meio de um servidor proxy, as configurações de proxy Olá também podem ser fornecidas toohello agente.</span><span class="sxs-lookup"><span data-stu-id="10a53-185">When hello connectivity of hello Windows machine toohello internet is through a proxy server, hello proxy settings can also be provided toohello agent.</span></span> <span data-ttu-id="10a53-186">Neste exemplo, não há nenhum servidor proxy, por isso estamos explicitamente omitindo todas as informações relacionadas a proxy.</span><span class="sxs-lookup"><span data-stu-id="10a53-186">In this example, there is no proxy server, so we are explicitly clearing any proxy-related information.</span></span>

<span data-ttu-id="10a53-187">Uso de largura de banda também pode ser controlado com opções de saudação do ```work hour bandwidth``` e ```non-work hour bandwidth``` para um determinado conjunto de dias da semana hello.</span><span class="sxs-lookup"><span data-stu-id="10a53-187">Bandwidth usage can also be controlled with hello options of ```work hour bandwidth``` and ```non-work hour bandwidth``` for a given set of days of hello week.</span></span>

<span data-ttu-id="10a53-188">Configurar detalhes de proxy e de largura de banda de saudação é feita usando Olá [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="10a53-188">Setting hello proxy and bandwidth details is done using hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a><span data-ttu-id="10a53-189">Configurações de criptografia</span><span class="sxs-lookup"><span data-stu-id="10a53-189">Encryption settings</span></span>
<span data-ttu-id="10a53-190">Olá enviados os dados de backup tooAzure Backup é tooprotect criptografados Olá confidencialidade de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="10a53-190">hello backup data sent tooAzure Backup is encrypted tooprotect hello confidentiality of hello data.</span></span> <span data-ttu-id="10a53-191">senha de criptografia de saudação é dados de saudação toodecrypt senha"Olá" no tempo de saudação da restauração.</span><span class="sxs-lookup"><span data-stu-id="10a53-191">hello encryption passphrase is hello "password" toodecrypt hello data at hello time of restore.</span></span>

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
PS C:\> $PassPhrase = ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force 
PS C:\> $PassCode   = 'AzureR0ckx'
PS C:\> Set-OBMachineSetting -EncryptionPassPhrase $PassPhrase
Server properties updated successfully
```

> [!IMPORTANT]
> <span data-ttu-id="10a53-192">Manter informações de senha Olá seguros e protegidos depois que ela é definida.</span><span class="sxs-lookup"><span data-stu-id="10a53-192">Keep hello passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="10a53-193">Não será capaz de toorestore a dados do Azure sem essa frase secreta.</span><span class="sxs-lookup"><span data-stu-id="10a53-193">You are not be able toorestore data from Azure without this passphrase.</span></span>
>
>

## <a name="back-up-files-and-folders"></a><span data-ttu-id="10a53-194">Fazer backup de arquivos e pastas</span><span class="sxs-lookup"><span data-stu-id="10a53-194">Back up files and folders</span></span>
<span data-ttu-id="10a53-195">Todos os backups de clientes e servidores Windows tooAzure Backup são governados por uma política.</span><span class="sxs-lookup"><span data-stu-id="10a53-195">All backups from Windows Servers and clients tooAzure Backup are governed by a policy.</span></span> <span data-ttu-id="10a53-196">política de saudação consiste em três partes:</span><span class="sxs-lookup"><span data-stu-id="10a53-196">hello policy comprises three parts:</span></span>

1. <span data-ttu-id="10a53-197">Um **agendamento de backup** que especifica quando backups necessário toobe tomadas e sincronizados com o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="10a53-197">A **backup schedule** that specifies when backups need toobe taken and synchronized with hello service.</span></span>
2. <span data-ttu-id="10a53-198">Um **agenda de retenção** que especifica quanto tempo os pontos de recuperação de saudação do tooretain no Azure.</span><span class="sxs-lookup"><span data-stu-id="10a53-198">A **retention schedule** that specifies how long tooretain hello recovery points in Azure.</span></span>
3. <span data-ttu-id="10a53-199">Uma **especificação de inclusão/exclusão de arquivo** que determina de que conteúdo deve-se realizar o backup.</span><span class="sxs-lookup"><span data-stu-id="10a53-199">A **file inclusion/exclusion specification** that dictates what should be backed up.</span></span>

<span data-ttu-id="10a53-200">Neste documento, já que estamos automatizando o backup, vamos pressupor que nada foi configurado.</span><span class="sxs-lookup"><span data-stu-id="10a53-200">In this document, since we're automating backup, we'll assume nothing has been configured.</span></span> <span data-ttu-id="10a53-201">Começamos criando uma nova política de backup usando Olá [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="10a53-201">We begin by creating a new backup policy using hello [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet.</span></span>

```
PS C:\> $newpolicy = New-OBPolicy
```

<span data-ttu-id="10a53-202">Em Olá esse tempo política está vazia e outros cmdlets são necessário toodefine os itens a serem incluídos ou excluídos, quando os backups serão executados e Olá onde os backups serão armazenados.</span><span class="sxs-lookup"><span data-stu-id="10a53-202">At this time hello policy is empty and other cmdlets are needed toodefine what items will be included or excluded, when backups will run, and where hello backups will be stored.</span></span>

### <a name="configuring-hello-backup-schedule"></a><span data-ttu-id="10a53-203">Configurar o agendamento de backup Olá</span><span class="sxs-lookup"><span data-stu-id="10a53-203">Configuring hello backup schedule</span></span>
<span data-ttu-id="10a53-204">Olá pela primeira vez da saudação 3 partes de uma política é agenda de backup hello, que é criada usando Olá [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="10a53-204">hello first of hello 3 parts of a policy is hello backup schedule, which is created using hello [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span></span> <span data-ttu-id="10a53-205">agendamento de backup Olá define quando backups necessário toobe realizada.</span><span class="sxs-lookup"><span data-stu-id="10a53-205">hello backup schedule defines when backups need toobe taken.</span></span> <span data-ttu-id="10a53-206">Ao criar um agendamento, você precisa toospecify 2 parâmetros de entrada:</span><span class="sxs-lookup"><span data-stu-id="10a53-206">When creating a schedule you need toospecify 2 input parameters:</span></span>

* <span data-ttu-id="10a53-207">**Dias da semana Olá** backup Olá deve ser executado.</span><span class="sxs-lookup"><span data-stu-id="10a53-207">**Days of hello week** that hello backup should run.</span></span> <span data-ttu-id="10a53-208">Você pode executar o trabalho de backup de saudação em apenas um dia, ou todos os dias da semana hello ou qualquer combinação entre.</span><span class="sxs-lookup"><span data-stu-id="10a53-208">You can run hello backup job on just one day, or every day of hello week, or any combination in between.</span></span>
* <span data-ttu-id="10a53-209">**Horas do dia Olá** quando backup Olá deve ser executado.</span><span class="sxs-lookup"><span data-stu-id="10a53-209">**Times of hello day** when hello backup should run.</span></span> <span data-ttu-id="10a53-210">Você pode definir o too3 diferentes momentos do dia hello quando backup Olá será disparado.</span><span class="sxs-lookup"><span data-stu-id="10a53-210">You can define up too3 different times of hello day when hello backup will be triggered.</span></span>

<span data-ttu-id="10a53-211">Por exemplo, você poderia configurar uma política de backup que é executada às 16h todo sábado e domingo.</span><span class="sxs-lookup"><span data-stu-id="10a53-211">For instance, you could configure a backup policy that runs at 4PM every Saturday and Sunday.</span></span>

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

<span data-ttu-id="10a53-212">agendamento de backup Olá precisa toobe associado a uma política e isso pode ser obtido usando Olá [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="10a53-212">hello backup schedule needs toobe associated with a policy, and this can be achieved by using hello [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span></span>

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a><span data-ttu-id="10a53-213">Configurando uma política de retenção</span><span class="sxs-lookup"><span data-stu-id="10a53-213">Configuring a retention policy</span></span>
<span data-ttu-id="10a53-214">política de retenção Olá define quanto tempo recuperação pontos criados a partir de trabalhos de backup são mantidos.</span><span class="sxs-lookup"><span data-stu-id="10a53-214">hello retention policy defines how long recovery points created from backup jobs are retained.</span></span> <span data-ttu-id="10a53-215">Ao criar uma nova política de retenção usando Olá [OBRetentionPolicy novo](https://technet.microsoft.com/library/hh770425) cmdlet, você pode especificar Olá de dias que Olá pontos de recuperação de backup é necessário toobe mantida com o Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="10a53-215">When creating a new retention policy using hello [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, you can specify hello number of days that hello backup recovery points need toobe retained with Azure Backup.</span></span> <span data-ttu-id="10a53-216">exemplo Hello abaixo define uma política de retenção de sete dias.</span><span class="sxs-lookup"><span data-stu-id="10a53-216">hello example below sets a retention policy of 7 days.</span></span>

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

<span data-ttu-id="10a53-217">Olá política de retenção deve ser associada com a política principal hello, usando o cmdlet Olá [OBRetentionPolicy conjunto](https://technet.microsoft.com/library/hh770405):</span><span class="sxs-lookup"><span data-stu-id="10a53-217">hello retention policy must be associated with hello main policy using hello cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span></span>

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
### <a name="including-and-excluding-files-toobe-backed-up"></a><span data-ttu-id="10a53-218">Incluindo e excluindo arquivos toobe backup</span><span class="sxs-lookup"><span data-stu-id="10a53-218">Including and excluding files toobe backed up</span></span>
<span data-ttu-id="10a53-219">Um ```OBFileSpec``` objeto define Olá arquivos toobe incluído e excluído em um backup.</span><span class="sxs-lookup"><span data-stu-id="10a53-219">An ```OBFileSpec``` object defines hello files toobe included and excluded in a backup.</span></span> <span data-ttu-id="10a53-220">Este é um conjunto de regras que verificam a saudação arquivos e pastas protegidos em um computador.</span><span class="sxs-lookup"><span data-stu-id="10a53-220">This is a set of rules that scope out hello protected files and folders on a machine.</span></span> <span data-ttu-id="10a53-221">Você pode ter muitas regras de inclusão ou exclusão de arquivos conforme necessário e associá-las a uma política.</span><span class="sxs-lookup"><span data-stu-id="10a53-221">You can have as many file inclusion or exclusion rules as required, and associate them with a policy.</span></span> <span data-ttu-id="10a53-222">Ao criar um novo objeto OBFileSpec, você pode:</span><span class="sxs-lookup"><span data-stu-id="10a53-222">When creating a new OBFileSpec object, you can:</span></span>

* <span data-ttu-id="10a53-223">Especifique a saudação toobe arquivos e pastas incluído</span><span class="sxs-lookup"><span data-stu-id="10a53-223">Specify hello files and folders toobe included</span></span>
* <span data-ttu-id="10a53-224">Especifique a saudação toobe arquivos e pastas excluído</span><span class="sxs-lookup"><span data-stu-id="10a53-224">Specify hello files and folders toobe excluded</span></span>
* <span data-ttu-id="10a53-225">Especifica recursiva de backup de dados em uma pasta (ou) se apenas Olá nível superior arquivos na pasta especificada Olá devem ser feitos backup.</span><span class="sxs-lookup"><span data-stu-id="10a53-225">Specify recursive backup of data in a folder (or) whether only hello top-level files in hello specified folder should be backed up.</span></span>

<span data-ttu-id="10a53-226">Olá este último é obtida usando o sinalizador de não - recursivo Olá no comando Olá New-OBFileSpec.</span><span class="sxs-lookup"><span data-stu-id="10a53-226">hello latter is achieved by using hello -NonRecursive flag in hello New-OBFileSpec command.</span></span>

<span data-ttu-id="10a53-227">O exemplo hello abaixo, vamos fazer backup de volume c: e d e excluir os binários do sistema operacional Olá na pasta do Windows hello e qualquer pasta temporária.</span><span class="sxs-lookup"><span data-stu-id="10a53-227">In hello example below, we'll back up volume C: and D: and exclude hello OS binaries in hello Windows folder and any temporary folders.</span></span> <span data-ttu-id="10a53-228">toodo portanto vamos criar duas especificações de arquivo usando Olá [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - uma para inclusão e outra para exclusão.</span><span class="sxs-lookup"><span data-stu-id="10a53-228">toodo so we'll create two file specifications using hello [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - one for inclusion and one for exclusion.</span></span> <span data-ttu-id="10a53-229">Depois que criar especificações de arquivo hello, eles são associados com a política de saudação usando Olá [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="10a53-229">Once hello file specifications have been created, they're associated with hello policy using hello [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span></span>

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

### <a name="applying-hello-policy"></a><span data-ttu-id="10a53-230">Aplicar a diretiva de saudação</span><span class="sxs-lookup"><span data-stu-id="10a53-230">Applying hello policy</span></span>
<span data-ttu-id="10a53-231">Agora o objeto de diretiva de saudação for concluído e tem um agendamento de backup associado, política de retenção e uma lista de inclusão/exclusão de arquivos.</span><span class="sxs-lookup"><span data-stu-id="10a53-231">Now hello policy object is complete and has an associated backup schedule, retention policy, and an inclusion/exclusion list of files.</span></span> <span data-ttu-id="10a53-232">Esta política agora pode ser confirmada para toouse de Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="10a53-232">This policy can now be committed for Azure Backup toouse.</span></span> <span data-ttu-id="10a53-233">Antes de aplicar Olá recém-criado política Certifique-se de que não há nenhuma política de backup existente associada ao servidor de saudação usando Olá [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="10a53-233">Before you apply hello newly created policy ensure that there are no existing backup policies associated with hello server by using hello [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span></span> <span data-ttu-id="10a53-234">Remover a política de saudação solicita confirmação.</span><span class="sxs-lookup"><span data-stu-id="10a53-234">Removing hello policy will prompt for confirmation.</span></span> <span data-ttu-id="10a53-235">confirmação de saudação tooskip usar Olá ```-Confirm:$false``` sinalizador com hello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="10a53-235">tooskip hello confirmation use hello ```-Confirm:$false``` flag with hello cmdlet.</span></span>

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want tooremove this backup policy? This will delete all hello backed up data. [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
```

<span data-ttu-id="10a53-236">Objeto de diretiva de saudação de confirmação é feito usando Olá [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="10a53-236">Committing hello policy object is done using hello [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span></span> <span data-ttu-id="10a53-237">Isso também gerará uma solicitação de confirmação.</span><span class="sxs-lookup"><span data-stu-id="10a53-237">This will also ask for confirmation.</span></span> <span data-ttu-id="10a53-238">confirmação de saudação tooskip usar Olá ```-Confirm:$false``` sinalizador com hello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="10a53-238">tooskip hello confirmation use hello ```-Confirm:$false``` flag with hello cmdlet.</span></span>

```
PS C:> Set-OBPolicy -Policy $newpolicy
Microsoft Azure Backup Do you want toosave this backup policy ? [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
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

<span data-ttu-id="10a53-239">Você pode exibir detalhes de Olá Olá existente da política de backup usando Olá [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="10a53-239">You can view hello details of hello existing backup policy using hello [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span></span> <span data-ttu-id="10a53-240">Você pode detalhamento ainda mais usando Olá [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet para o agendamento de backup hello e hello [OBRetentionPolicy Get](https://technet.microsoft.com/library/hh770427) cmdlet Olá das políticas de retenção</span><span class="sxs-lookup"><span data-stu-id="10a53-240">You can drill-down further using hello [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet for hello backup schedule and hello [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet for hello retention policies</span></span>

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

### <a name="performing-an-ad-hoc-backup"></a><span data-ttu-id="10a53-241">Executando um backup ad hoc</span><span class="sxs-lookup"><span data-stu-id="10a53-241">Performing an ad-hoc backup</span></span>
<span data-ttu-id="10a53-242">Quando uma política de backup foi definida backups Olá ocorrerá por agendamento hello.</span><span class="sxs-lookup"><span data-stu-id="10a53-242">Once a backup policy has been set hello backups will occur per hello schedule.</span></span> <span data-ttu-id="10a53-243">Também é possível usar Olá acionar um backup ad-hoc [OBBackup início](https://technet.microsoft.com/library/hh770426) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="10a53-243">Triggering an ad-hoc backup is also possible using hello [Start-OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span></span>

```
PS C:> Get-OBPolicy | Start-OBBackup
Initializing
Taking snapshot of volumes...
Preparing storage...
Generating backup metadata information and preparing hello metadata VHD...
Data transfer is in progress. It might take longer since it is hello first backup and all data needs toobe transferred...
Data transfer completed and all backed up data is in hello cloud. Verifying data integrity...
Data transfer completed
In progress...
Job completed.
hello backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a><span data-ttu-id="10a53-244">Restaurar dados por meio do Backup do Azure</span><span class="sxs-lookup"><span data-stu-id="10a53-244">Restore data from Azure Backup</span></span>
<span data-ttu-id="10a53-245">Esta seção o guiará pelas etapas de saudação para automatizar a recuperação de dados de Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="10a53-245">This section will guide you through hello steps for automating recovery of data from Azure Backup.</span></span> <span data-ttu-id="10a53-246">Fazer assim envolve Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="10a53-246">Doing so involves hello following steps:</span></span>

1. <span data-ttu-id="10a53-247">Selecione o volume de origem Olá</span><span class="sxs-lookup"><span data-stu-id="10a53-247">Pick hello source volume</span></span>
2. <span data-ttu-id="10a53-248">Escolha um toorestore de ponto de backup</span><span class="sxs-lookup"><span data-stu-id="10a53-248">Choose a backup point toorestore</span></span>
3. <span data-ttu-id="10a53-249">Escolha um item toorestore</span><span class="sxs-lookup"><span data-stu-id="10a53-249">Choose an item toorestore</span></span>
4. <span data-ttu-id="10a53-250">Processo de restauração de saudação do gatilho</span><span class="sxs-lookup"><span data-stu-id="10a53-250">Trigger hello restore process</span></span>

### <a name="picking-hello-source-volume"></a><span data-ttu-id="10a53-251">Volume de origem de saudação de separação</span><span class="sxs-lookup"><span data-stu-id="10a53-251">Picking hello source volume</span></span>
<span data-ttu-id="10a53-252">Ordem toorestore um item de Backup do Azure, você primeiro precisa tooidentify origem de saudação do item de saudação.</span><span class="sxs-lookup"><span data-stu-id="10a53-252">In order toorestore an item from Azure Backup, you first need tooidentify hello source of hello item.</span></span> <span data-ttu-id="10a53-253">Como executamos comandos Olá no contexto de saudação de um servidor do Windows ou um cliente do Windows, a máquina Olá já está identificada.</span><span class="sxs-lookup"><span data-stu-id="10a53-253">Since we're executing hello commands in hello context of a Windows Server or a Windows client, hello machine is already identified.</span></span> <span data-ttu-id="10a53-254">Olá próxima etapa na identificação de fonte de saudação é tooidentify volume de saudação que o contém.</span><span class="sxs-lookup"><span data-stu-id="10a53-254">hello next step in identifying hello source is tooidentify hello volume containing it.</span></span> <span data-ttu-id="10a53-255">Uma lista de volumes ou fontes de backup deste computador pode ser recuperado por meio da execução Olá [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="10a53-255">A list of volumes or sources being backed up from this machine can be retrieved by executing hello [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span></span> <span data-ttu-id="10a53-256">Esse comando retorna uma matriz de todas as fontes de saudação backup desse servidor/cliente.</span><span class="sxs-lookup"><span data-stu-id="10a53-256">This command returns an array of all hello sources backed up from this server/client.</span></span>

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

### <a name="choosing-a-backup-point-from-which-toorestore"></a><span data-ttu-id="10a53-257">Escolhendo um ponto de backup da qual toorestore</span><span class="sxs-lookup"><span data-stu-id="10a53-257">Choosing a backup point from which toorestore</span></span>
<span data-ttu-id="10a53-258">Recuperar uma lista de pontos de backup executando Olá [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet com os parâmetros apropriados.</span><span class="sxs-lookup"><span data-stu-id="10a53-258">You retreive a list of backup points by executing hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet with appropriate parameters.</span></span> <span data-ttu-id="10a53-259">Em nosso exemplo, vamos escolher ponto de backup mais recente Olá para o volume de origem Olá *unidade d:* e usá-lo toorecover um arquivo específico.</span><span class="sxs-lookup"><span data-stu-id="10a53-259">In our example, we’ll choose hello latest backup point for hello source volume *D:* and use it toorecover a specific file.</span></span>

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
<span data-ttu-id="10a53-260">objeto Olá ```$rps``` é uma matriz de pontos de backup.</span><span class="sxs-lookup"><span data-stu-id="10a53-260">hello object ```$rps``` is an array of backup points.</span></span> <span data-ttu-id="10a53-261">Olá primeiro elemento é o último ponto de saudação e enésimo elemento de saudação é ponto mais antigo hello.</span><span class="sxs-lookup"><span data-stu-id="10a53-261">hello first element is hello latest point and hello Nth element is hello oldest point.</span></span> <span data-ttu-id="10a53-262">ponto mais recente do toochoose Olá, vamos usar ```$rps[0]```.</span><span class="sxs-lookup"><span data-stu-id="10a53-262">toochoose hello latest point, we will use ```$rps[0]```.</span></span>

### <a name="choosing-an-item-toorestore"></a><span data-ttu-id="10a53-263">Escolher um item toorestore</span><span class="sxs-lookup"><span data-stu-id="10a53-263">Choosing an item toorestore</span></span>
<span data-ttu-id="10a53-264">Olá tooidentify exato do arquivo ou pasta toorestore, recursivamente usar Olá [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="10a53-264">tooidentify hello exact file or folder toorestore, recursively use hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span></span> <span data-ttu-id="10a53-265">Essa hierarquia de pasta maneira Olá possa ser navegada exclusivamente usando Olá ```Get-OBRecoverableItem```.</span><span class="sxs-lookup"><span data-stu-id="10a53-265">That way hello folder hierarchy can be browsed solely using hello ```Get-OBRecoverableItem```.</span></span>

<span data-ttu-id="10a53-266">Neste exemplo, se quisermos que o arquivo de saudação toorestore *finances.xls* podemos fazer referência a esse usando objeto Olá ```$filesFolders[1]```.</span><span class="sxs-lookup"><span data-stu-id="10a53-266">In this example, if we want toorestore hello file *finances.xls* we can reference that using hello object ```$filesFolders[1]```.</span></span>

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

<span data-ttu-id="10a53-267">Você também pode procurar itens toorestore usando Olá ```Get-OBRecoverableItem``` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="10a53-267">You can also search for items toorestore using hello ```Get-OBRecoverableItem``` cmdlet.</span></span> <span data-ttu-id="10a53-268">Em nosso exemplo, toosearch para *finances.xls* foi possível obter um identificador de arquivo hello executando este comando:</span><span class="sxs-lookup"><span data-stu-id="10a53-268">In our example, toosearch for *finances.xls* we could get a handle on hello file by running this command:</span></span>

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-hello-restore-process"></a><span data-ttu-id="10a53-269">Disparar o processo de restauração Olá</span><span class="sxs-lookup"><span data-stu-id="10a53-269">Triggering hello restore process</span></span>
<span data-ttu-id="10a53-270">tootrigger o processo de restauração Olá, é preciso primeiro toospecify opções de recuperação de saudação.</span><span class="sxs-lookup"><span data-stu-id="10a53-270">tootrigger hello restore process, we first need toospecify hello recovery options.</span></span> <span data-ttu-id="10a53-271">Isso pode ser feito usando Olá [OBRecoveryOption novo](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="10a53-271">This can be done by using hello [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span></span> <span data-ttu-id="10a53-272">Neste exemplo, vamos supor que queremos arquivos de saudação toorestore muito*C:\temp*. Vamos supor também que desejamos tooskip arquivos já existentes na pasta de destino Olá *C:\temp*. toocreate tal uma opção de recuperação, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="10a53-272">For this example, let's assume that we want toorestore hello files too*C:\temp*. Let's also assume that we want tooskip files that already exist on hello destination folder *C:\temp*. toocreate such a recovery option, use hello following command:</span></span>

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

<span data-ttu-id="10a53-273">Agora disparar o processo de restauração hello usando Olá [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) comando Olá selecionado ```$item``` da saída de saudação de saudação ```Get-OBRecoverableItem``` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="10a53-273">Now trigger hello restore process by using hello [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) command on hello selected ```$item``` from hello output of hello ```Get-OBRecoverableItem``` cmdlet:</span></span>

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
hello recovery operation completed successfully.
```


## <a name="uninstalling-hello-azure-backup-agent"></a><span data-ttu-id="10a53-274">Desinstalar o agente de Backup do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="10a53-274">Uninstalling hello Azure Backup agent</span></span>
<span data-ttu-id="10a53-275">Desinstalando agente de Backup do Azure Olá pode ser feito usando o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="10a53-275">Uninstalling hello Azure Backup agent can be done by using hello following command:</span></span>

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

<span data-ttu-id="10a53-276">Desinstalar os binários de agente de saudação da máquina de saudação tem algumas tooconsider consequências:</span><span class="sxs-lookup"><span data-stu-id="10a53-276">Uninstalling hello agent binaries from hello machine has some consequences tooconsider:</span></span>

* <span data-ttu-id="10a53-277">Ele remove o filtro de arquivo hello da máquina de saudação e controle de alterações é interrompido.</span><span class="sxs-lookup"><span data-stu-id="10a53-277">It removes hello file-filter from hello machine, and tracking of changes is stopped.</span></span>
* <span data-ttu-id="10a53-278">Todas as informações de política são removidas da máquina de hello, mas as informações de política de saudação continuam toobe armazenado no serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="10a53-278">All policy information is removed from hello machine, but hello policy information continues toobe stored in hello service.</span></span>
* <span data-ttu-id="10a53-279">Todos os agendamentos de backup são removidos e nenhum backup posterior é realizado.</span><span class="sxs-lookup"><span data-stu-id="10a53-279">All backup schedules are removed, and no further backups are taken.</span></span>

<span data-ttu-id="10a53-280">No entanto, Olá dados armazenados no Azure permanece e retidos de acordo com a configuração de política de retenção Olá por você.</span><span class="sxs-lookup"><span data-stu-id="10a53-280">However, hello data stored in Azure remains and is retained as per hello retention policy setup by you.</span></span> <span data-ttu-id="10a53-281">Os pontos mais antigos são desatualizados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="10a53-281">Older points are automatically aged out.</span></span>

## <a name="remote-management"></a><span data-ttu-id="10a53-282">Gerenciamento remoto</span><span class="sxs-lookup"><span data-stu-id="10a53-282">Remote management</span></span>
<span data-ttu-id="10a53-283">Todo o gerenciamento de saudação em torno de agente de Backup do Azure hello, políticas e fontes de dados pode ser feito remotamente por meio do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="10a53-283">All hello management around hello Azure Backup agent, policies, and data sources can be done remotely through PowerShell.</span></span> <span data-ttu-id="10a53-284">máquina de saudação que será gerenciada remotamente precisa toobe preparado corretamente.</span><span class="sxs-lookup"><span data-stu-id="10a53-284">hello machine that will be managed remotely needs toobe prepared correctly.</span></span>

<span data-ttu-id="10a53-285">Por padrão, a saudação serviço WinRM está configurada para inicialização manual.</span><span class="sxs-lookup"><span data-stu-id="10a53-285">By default, hello WinRM service is configured for manual startup.</span></span> <span data-ttu-id="10a53-286">tipo de inicialização de saudação deve ser definido muito*automáticas* e Olá serviço deve ser iniciado.</span><span class="sxs-lookup"><span data-stu-id="10a53-286">hello startup type must be set too*Automatic* and hello service should be started.</span></span> <span data-ttu-id="10a53-287">tooverify que Olá serviço WinRM está em execução, o valor Olá Olá propriedade Status deve ser *executando*.</span><span class="sxs-lookup"><span data-stu-id="10a53-287">tooverify that hello WinRM service is running, hello value of hello Status property should be *Running*.</span></span>

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

<span data-ttu-id="10a53-288">O PowerShell deve ser configurado remotamente.</span><span class="sxs-lookup"><span data-stu-id="10a53-288">PowerShell should be configured for remoting.</span></span>

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up tooreceive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

<span data-ttu-id="10a53-289">máquina Olá agora pode ser gerenciada remotamente - a partir da instalação de saudação do agente de saudação.</span><span class="sxs-lookup"><span data-stu-id="10a53-289">hello machine can now be managed remotely - starting from hello installation of hello agent.</span></span> <span data-ttu-id="10a53-290">Por exemplo, hello script a seguir copia o computador remoto do hello agente toohello e instala-o.</span><span class="sxs-lookup"><span data-stu-id="10a53-290">For example, hello following script copies hello agent toohello remote machine and installs it.</span></span>

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a><span data-ttu-id="10a53-291">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="10a53-291">Next steps</span></span>
<span data-ttu-id="10a53-292">Para obter mais informações sobre o Backup do Azure para Windows Server/Client, consulte</span><span class="sxs-lookup"><span data-stu-id="10a53-292">For more information about Azure Backup for Windows Server/Client see</span></span>

* [<span data-ttu-id="10a53-293">Introdução tooAzure Backup</span><span class="sxs-lookup"><span data-stu-id="10a53-293">Introduction tooAzure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="10a53-294">Fazer backup de servidores Windows</span><span class="sxs-lookup"><span data-stu-id="10a53-294">Back up Windows Servers</span></span>](backup-configure-vault.md)
