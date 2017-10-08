---
title: backups do aaaUse PowerShell toomanage Windows Server no Azure | Microsoft Docs
description: Implantar e gerenciar backups do Windows Server usando o PowerShell.
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: e7e269e2-1f11-41a9-957b-a2155de6a1e0
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: saurse;markgal;nkolli;trinadhk
ms.openlocfilehash: 72292e510b0f059102440bd49a195be4ef700a6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-backup-tooazure-for-windows-serverwindows-client-using-powershell"></a><span data-ttu-id="8807d-103">Implantar e gerenciar o backup tooAzure para o cliente do Windows Server/Windows usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="8807d-103">Deploy and manage backup tooAzure for Windows Server/Windows Client using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8807d-104">ARM</span><span class="sxs-lookup"><span data-stu-id="8807d-104">ARM</span></span>](backup-client-automation.md)
> * [<span data-ttu-id="8807d-105">Clássico</span><span class="sxs-lookup"><span data-stu-id="8807d-105">Classic</span></span>](backup-client-automation-classic.md)
>
>

<span data-ttu-id="8807d-106">Este artigo explica como o Cofre de backup toouse PowerShell tooback o tooa de dados de estação de trabalho do Windows ou o Windows Server.</span><span class="sxs-lookup"><span data-stu-id="8807d-106">This article explains how toouse PowerShell tooback up Windows Server or Windows workstation data tooa backup vault.</span></span> <span data-ttu-id="8807d-107">A Microsoft recomenda usar cofres de Serviços de Recuperação para todas as implantações novas.</span><span class="sxs-lookup"><span data-stu-id="8807d-107">Microsoft recommends using Recovery Services vaults for all new deployments.</span></span> <span data-ttu-id="8807d-108">Se você for um novo usuário de Backup do Azure e não tiver criado um cofre de backup na sua assinatura, use o artigo hello, [implantar e gerenciar tooAzure de dados do Data Protection Manager usando o PowerShell](backup-client-automation.md) para armazenar os dados em um cofre de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="8807d-108">If you are a new Azure Backup user and have not created a backup vault in your subscription, use hello article, [Deploy and manage Data Protection Manager data tooAzure using PowerShell](backup-client-automation.md) so you store your data in a Recovery Services vault.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="8807d-109">Agora você pode atualizar seu cofres dos serviços de tooRecovery de cofres de Backup.</span><span class="sxs-lookup"><span data-stu-id="8807d-109">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="8807d-110">Para obter detalhes, consulte o artigo Olá [atualizar um tooa de Cofre de Backup Cofre de serviços de recuperação](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="8807d-110">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="8807d-111">A Microsoft incentiva tooupgrade cofres de serviços tooRecovery os cofres de Backup.</span><span class="sxs-lookup"><span data-stu-id="8807d-111">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="8807d-112">Após 15 de outubro de 2017, você não pode usar o PowerShell toocreate os cofres de Backup.</span><span class="sxs-lookup"><span data-stu-id="8807d-112">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="8807d-113">**Em 1º de novembro de 2017**:</span><span class="sxs-lookup"><span data-stu-id="8807d-113">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="8807d-114">Todos os cofres de Backup restantes serão automaticamente atualizados tooRecovery cofres de serviços.</span><span class="sxs-lookup"><span data-stu-id="8807d-114">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="8807d-115">Você não será capaz de tooaccess os dados de backup no portal clássico do hello.</span><span class="sxs-lookup"><span data-stu-id="8807d-115">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="8807d-116">Em vez disso, use Olá tooaccess portal do Azure os dados de backup em cofres de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="8807d-116">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="install-azure-powershell"></a><span data-ttu-id="8807d-117">Instalar o Azure Powershell</span><span class="sxs-lookup"><span data-stu-id="8807d-117">Install Azure PowerShell</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="8807d-118">Em outubro de 2015, o Azure PowerShell 1.0 foi lançado.</span><span class="sxs-lookup"><span data-stu-id="8807d-118">In October 2015, Azure PowerShell 1.0 was released.</span></span> <span data-ttu-id="8807d-119">Esta versão foi bem-sucedido versão Olá 0.9.8 e colocado sobre alterações significativas, especialmente no padrão de nomenclatura Olá Olá cmdlets.</span><span class="sxs-lookup"><span data-stu-id="8807d-119">This release succeeded hello 0.9.8 release and brought about some significant changes, especially in hello naming pattern of hello cmdlets.</span></span> <span data-ttu-id="8807d-120">Acompanhamento de cmdlets 1.0 Olá {verbo} padrão de nomenclatura-AzureRm {substantivo;} Por outro lado, não incluem nomes Olá 0.9.8 **Rm** (por exemplo, New-AzureRmResourceGroup em vez de New-AzureResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="8807d-120">1.0 cmdlets follow hello naming pattern {verb}-AzureRm{noun}; whereas, hello 0.9.8 names do not include **Rm** (for example, New-AzureRmResourceGroup instead of New-AzureResourceGroup).</span></span> <span data-ttu-id="8807d-121">Ao usar o Azure PowerShell 0.9.8, você primeiro deve habilitar o modo de Gerenciador de recursos de Olá executando Olá **Switch-AzureMode AzureResourceManager** comando.</span><span class="sxs-lookup"><span data-stu-id="8807d-121">When using Azure PowerShell 0.9.8, you must first enable hello Resource Manager mode by running hello **Switch-AzureMode AzureResourceManager** command.</span></span> <span data-ttu-id="8807d-122">Este comando não é necessário na 1.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="8807d-122">This command is not necessary in 1.0 or later.</span></span>

<span data-ttu-id="8807d-123">Se você quiser toouse seus scripts escritos para o ambiente Olá 0.9.8, Olá 1.0 ou posterior ambiente, você cuidadosamente deve testar Olá scripts em um ambiente de pré-produção antes de usá-las na produção tooavoid impacto inesperado.</span><span class="sxs-lookup"><span data-stu-id="8807d-123">If you want toouse your scripts written for hello 0.9.8 environment, in hello 1.0 or later environment, you should carefully test hello scripts in a pre-production environment before using them in production tooavoid unexpected impact.</span></span>

<span data-ttu-id="8807d-124">[Baixar a versão mais recente de PowerShell Olá](https://github.com/Azure/azure-powershell/releases) (versão mínima necessária é: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="8807d-124">[Download hello latest PowerShell release](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-backup-vault"></a><span data-ttu-id="8807d-125">Criar um cofre de backup</span><span class="sxs-lookup"><span data-stu-id="8807d-125">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="8807d-126">Para clientes que usam o Backup do Azure para Olá primeira vez, você precisa tooregister hello Azure Backup provedor toobe usado com sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="8807d-126">For customers using Azure Backup for hello first time, you need tooregister hello Azure Backup provider toobe used with your subscription.</span></span> <span data-ttu-id="8807d-127">Isso pode ser feito executando o comando a seguir de saudação: Register-AzureProvider - ProviderNamespace "Microsoft.Backup"</span><span class="sxs-lookup"><span data-stu-id="8807d-127">This can be done by running hello following command: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="8807d-128">Você pode criar um novo cofre de backup usando Olá **AzureRMBackupVault novo** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8807d-128">You can create a new backup vault using hello **New-AzureRMBackupVault** cmdlet.</span></span> <span data-ttu-id="8807d-129">Cofre de backup Olá é um recurso do ARM, portanto, você precisa tooplace-lo em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8807d-129">hello backup vault is an ARM resource, so you need tooplace it within a Resource Group.</span></span> <span data-ttu-id="8807d-130">Em um console do Azure PowerShell com privilégios elevados, execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="8807d-130">In an elevated Azure PowerShell console, run hello following commands:</span></span>

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

<span data-ttu-id="8807d-131">Saudação de uso **Get-AzureRMBackupVault** os cofres de backup de saudação do cmdlet toolist em uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="8807d-131">Use hello **Get-AzureRMBackupVault** cmdlet toolist hello backup vaults in a subscription.</span></span>

## <a name="installing-hello-azure-backup-agent"></a><span data-ttu-id="8807d-132">Instalando o agente de Backup do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="8807d-132">Installing hello Azure Backup agent</span></span>
<span data-ttu-id="8807d-133">Antes de instalar o agente de Backup do Azure Olá, você precisará instalador de saudação toohave baixado e presente no saudação do Windows Server.</span><span class="sxs-lookup"><span data-stu-id="8807d-133">Before you install hello Azure Backup agent, you need toohave hello installer downloaded and present on hello Windows Server.</span></span> <span data-ttu-id="8807d-134">Você pode obter a versão mais recente de saudação do instalador de saudação de saudação [Microsoft Download Center](http://aka.ms/azurebackup_agent) ou da página de painel do Cofre de saudação backup.</span><span class="sxs-lookup"><span data-stu-id="8807d-134">You can get hello latest version of hello installer from hello [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from hello backup vault's Dashboard page.</span></span> <span data-ttu-id="8807d-135">Salvar instalador Olá tooan local facilmente acessível, como * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="8807d-135">Save hello installer tooan easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="8807d-136">Agente de saudação tooinstall, executar Olá seguinte comando em um console do PowerShell com privilégios elevados:</span><span class="sxs-lookup"><span data-stu-id="8807d-136">tooinstall hello agent, run hello following command in an elevated PowerShell console:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="8807d-137">Isso instala o agente de saudação com todas as opções padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="8807d-137">This installs hello agent with all hello default options.</span></span> <span data-ttu-id="8807d-138">instalação de saudação leva alguns minutos no plano de fundo de saudação.</span><span class="sxs-lookup"><span data-stu-id="8807d-138">hello installation takes a few minutes in hello background.</span></span> <span data-ttu-id="8807d-139">Se você não especificar Olá */nu* em seguida, Olá **Windows Update** janela será aberta no final de saudação do hello instalação toocheck para todas as atualizações.</span><span class="sxs-lookup"><span data-stu-id="8807d-139">If you do not specify hello */nu* option then hello **Windows Update** window will open at hello end of hello installation toocheck for any updates.</span></span> <span data-ttu-id="8807d-140">Uma vez instalado, agente hello serão mostradas na lista Olá de programas instalados.</span><span class="sxs-lookup"><span data-stu-id="8807d-140">Once installed, hello agent will show in hello list of installed programs.</span></span>

<span data-ttu-id="8807d-141">lista de saudação toosee de instalado programas, consulte muito**painel de controle** > **programas** > **programas e recursos**.</span><span class="sxs-lookup"><span data-stu-id="8807d-141">toosee hello list of installed programs, go too**Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agente instalado](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="8807d-143">Opções de instalação</span><span class="sxs-lookup"><span data-stu-id="8807d-143">Installation options</span></span>
<span data-ttu-id="8807d-144">toosee todas as opções disponíveis por meio de Olá Olá de linha de comando, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="8807d-144">toosee all hello options available via hello command-line, use hello following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="8807d-145">Olá as opções disponíveis incluem:</span><span class="sxs-lookup"><span data-stu-id="8807d-145">hello available options include:</span></span>

| <span data-ttu-id="8807d-146">Opção</span><span class="sxs-lookup"><span data-stu-id="8807d-146">Option</span></span> | <span data-ttu-id="8807d-147">Detalhes</span><span class="sxs-lookup"><span data-stu-id="8807d-147">Details</span></span> | <span data-ttu-id="8807d-148">Padrão</span><span class="sxs-lookup"><span data-stu-id="8807d-148">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8807d-149">/q</span><span class="sxs-lookup"><span data-stu-id="8807d-149">/q</span></span> |<span data-ttu-id="8807d-150">Instalação silenciosa</span><span class="sxs-lookup"><span data-stu-id="8807d-150">Quiet installation</span></span> |- |
| <span data-ttu-id="8807d-151">/p:"local"</span><span class="sxs-lookup"><span data-stu-id="8807d-151">/p:"location"</span></span> |<span data-ttu-id="8807d-152">Pasta de instalação de toohello de caminho para o agente de Backup do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8807d-152">Path toohello installation folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="8807d-153">C:\Arquivos de Programas\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="8807d-153">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="8807d-154">/s:"local"</span><span class="sxs-lookup"><span data-stu-id="8807d-154">/s:"location"</span></span> |<span data-ttu-id="8807d-155">Pasta de cache de toohello de caminho para o agente de Backup do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8807d-155">Path toohello cache folder for hello Azure Backup agent.</span></span> |<span data-ttu-id="8807d-156">C:\Arquivos de Programas\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="8807d-156">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="8807d-157">/m</span><span class="sxs-lookup"><span data-stu-id="8807d-157">/m</span></span> |<span data-ttu-id="8807d-158">Aceitar tooMicrosoft atualização</span><span class="sxs-lookup"><span data-stu-id="8807d-158">Opt-in tooMicrosoft Update</span></span> |- |
| <span data-ttu-id="8807d-159">/nu</span><span class="sxs-lookup"><span data-stu-id="8807d-159">/nu</span></span> |<span data-ttu-id="8807d-160">Não verificar se há atualizações após a conclusão da instalação</span><span class="sxs-lookup"><span data-stu-id="8807d-160">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="8807d-161">/d</span><span class="sxs-lookup"><span data-stu-id="8807d-161">/d</span></span> |<span data-ttu-id="8807d-162">Desinstala o agente dos Serviços de Recuperação do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="8807d-162">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="8807d-163">/ph</span><span class="sxs-lookup"><span data-stu-id="8807d-163">/ph</span></span> |<span data-ttu-id="8807d-164">Endereço do host do proxy</span><span class="sxs-lookup"><span data-stu-id="8807d-164">Proxy Host Address</span></span> |- |
| <span data-ttu-id="8807d-165">/po</span><span class="sxs-lookup"><span data-stu-id="8807d-165">/po</span></span> |<span data-ttu-id="8807d-166">Número da porta do host do proxy</span><span class="sxs-lookup"><span data-stu-id="8807d-166">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="8807d-167">/pu</span><span class="sxs-lookup"><span data-stu-id="8807d-167">/pu</span></span> |<span data-ttu-id="8807d-168">UserName do host do proxy</span><span class="sxs-lookup"><span data-stu-id="8807d-168">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="8807d-169">/pw</span><span class="sxs-lookup"><span data-stu-id="8807d-169">/pw</span></span> |<span data-ttu-id="8807d-170">Senha do proxy</span><span class="sxs-lookup"><span data-stu-id="8807d-170">Proxy Password</span></span> |- |

## <a name="registering-with-hello-azure-backup-service"></a><span data-ttu-id="8807d-171">Registrando Olá serviço Backup do Azure</span><span class="sxs-lookup"><span data-stu-id="8807d-171">Registering with hello Azure Backup service</span></span>
<span data-ttu-id="8807d-172">Antes de registrar com hello serviço Backup do Azure, você precisa tooensure que Olá [pré-requisitos](backup-configure-vault.md) são atendidos.</span><span class="sxs-lookup"><span data-stu-id="8807d-172">Before you can register with hello Azure Backup service, you need tooensure that hello [prerequisites](backup-configure-vault.md) are met.</span></span> <span data-ttu-id="8807d-173">Você deve:</span><span class="sxs-lookup"><span data-stu-id="8807d-173">You must:</span></span>

* <span data-ttu-id="8807d-174">Ter uma assinatura válida do Azure</span><span class="sxs-lookup"><span data-stu-id="8807d-174">Have a valid Azure subscription</span></span>
* <span data-ttu-id="8807d-175">Ter um cofre de backup</span><span class="sxs-lookup"><span data-stu-id="8807d-175">Have a backup vault</span></span>

<span data-ttu-id="8807d-176">credenciais do cofre Olá toodownload, executadas Olá **Get-AzureRMBackupVaultCredentials** cmdlet em um console do PowerShell do Azure e armazenamento-lo em um local conveniente, como * C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="8807d-176">toodownload hello vault credentials, run hello **Get-AzureRMBackupVaultCredentials** cmdlet in an Azure PowerShell console and store it in a convenient location like *C:\Downloads\*.</span></span>

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

<span data-ttu-id="8807d-177">Máquina de saudação do registro com cofre Olá é feita usando Olá [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="8807d-177">Registering hello machine with hello vault is done using hello [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> $cred = $credspath + $credsfilename
PS C:\> Start-OBRegistration -VaultCredentials $cred -Confirm:$false

CertThumbprint      : 7a2ef2caa2e74b6ed1222a5e89288ddad438df2
SubscriptionID      : ef4ab577-c2c0-43e4-af80-af49f485f3d1
ServiceResourceName : test-vault
Region              : West US

Machine registration succeeded.
```

> [!IMPORTANT]
> <span data-ttu-id="8807d-178">Não use o arquivo de credenciais de cofre do caminhos relativos toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="8807d-178">Do not use relative paths toospecify hello vault credentials file.</span></span> <span data-ttu-id="8807d-179">Você deve fornecer um caminho absoluto como um cmdlet toohello de entrada.</span><span class="sxs-lookup"><span data-stu-id="8807d-179">You must provide an absolute path as an input toohello cmdlet.</span></span>
>
>

## <a name="networking-settings"></a><span data-ttu-id="8807d-180">Configurações de rede</span><span class="sxs-lookup"><span data-stu-id="8807d-180">Networking settings</span></span>
<span data-ttu-id="8807d-181">Quando a conectividade de saudação do hello Windows máquina toohello que Internet é por meio de um servidor proxy, as configurações de proxy Olá também podem ser fornecidas toohello agente.</span><span class="sxs-lookup"><span data-stu-id="8807d-181">When hello connectivity of hello Windows machine toohello internet is through a proxy server, hello proxy settings can also be provided toohello agent.</span></span> <span data-ttu-id="8807d-182">Neste exemplo, não há nenhum servidor proxy, por isso estamos explicitamente omitindo todas as informações relacionadas a proxy.</span><span class="sxs-lookup"><span data-stu-id="8807d-182">In this example, there is no proxy server, so we are explicitly clearing any proxy-related information.</span></span>

<span data-ttu-id="8807d-183">Uso de largura de banda também pode ser controlado com opções de saudação do ```work hour bandwidth``` e ```non-work hour bandwidth``` para um determinado conjunto de dias da semana hello.</span><span class="sxs-lookup"><span data-stu-id="8807d-183">Bandwidth usage can also be controlled with hello options of ```work hour bandwidth``` and ```non-work hour bandwidth``` for a given set of days of hello week.</span></span>

<span data-ttu-id="8807d-184">Configurar detalhes de proxy e de largura de banda de saudação é feita usando Olá [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="8807d-184">Setting hello proxy and bandwidth details is done using hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a><span data-ttu-id="8807d-185">Configurações de criptografia</span><span class="sxs-lookup"><span data-stu-id="8807d-185">Encryption settings</span></span>
<span data-ttu-id="8807d-186">Olá enviados os dados de backup tooAzure Backup é tooprotect criptografados Olá confidencialidade de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="8807d-186">hello backup data sent tooAzure Backup is encrypted tooprotect hello confidentiality of hello data.</span></span> <span data-ttu-id="8807d-187">senha de criptografia de saudação é dados de saudação toodecrypt senha"Olá" no tempo de saudação da restauração.</span><span class="sxs-lookup"><span data-stu-id="8807d-187">hello encryption passphrase is hello "password" toodecrypt hello data at hello time of restore.</span></span>

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
Server properties updated successfully
```

> [!IMPORTANT]
> <span data-ttu-id="8807d-188">Manter informações de senha Olá seguros e protegidos depois que ela é definida.</span><span class="sxs-lookup"><span data-stu-id="8807d-188">Keep hello passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="8807d-189">Você não será capaz de toorestore a dados do Azure sem essa frase secreta.</span><span class="sxs-lookup"><span data-stu-id="8807d-189">You will not be able toorestore data from Azure without this passphrase.</span></span>
>
>

## <a name="back-up-files-and-folders"></a><span data-ttu-id="8807d-190">Fazer backup de arquivos e pastas</span><span class="sxs-lookup"><span data-stu-id="8807d-190">Back up files and folders</span></span>
<span data-ttu-id="8807d-191">Todos os backups de clientes e servidores Windows tooAzure Backup são governados por uma política.</span><span class="sxs-lookup"><span data-stu-id="8807d-191">All your backups from Windows Servers and clients tooAzure Backup are governed by a policy.</span></span> <span data-ttu-id="8807d-192">política de saudação consiste em três partes:</span><span class="sxs-lookup"><span data-stu-id="8807d-192">hello policy comprises three parts:</span></span>

1. <span data-ttu-id="8807d-193">Um **agendamento de backup** que especifica quando backups necessário toobe tomadas e sincronizados com o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="8807d-193">A **backup schedule** that specifies when backups need toobe taken and synchronized with hello service.</span></span>
2. <span data-ttu-id="8807d-194">Um **agenda de retenção** que especifica quanto tempo os pontos de recuperação de saudação do tooretain no Azure.</span><span class="sxs-lookup"><span data-stu-id="8807d-194">A **retention schedule** that specifies how long tooretain hello recovery points in Azure.</span></span>
3. <span data-ttu-id="8807d-195">Uma **especificação de inclusão/exclusão de arquivo** que determina de que conteúdo deve-se realizar o backup.</span><span class="sxs-lookup"><span data-stu-id="8807d-195">A **file inclusion/exclusion specification** that dictates what should be backed up.</span></span>

<span data-ttu-id="8807d-196">Neste documento, já que estamos automatizando o backup, vamos pressupor que nada foi configurado.</span><span class="sxs-lookup"><span data-stu-id="8807d-196">In this document, since we're automating backup, we'll assume nothing has been configured.</span></span> <span data-ttu-id="8807d-197">Começamos criando uma nova política de backup usando Olá [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet e usá-lo.</span><span class="sxs-lookup"><span data-stu-id="8807d-197">We begin by creating a new backup policy using hello [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet and using it.</span></span>

```
PS C:\> $newpolicy = New-OBPolicy
```

<span data-ttu-id="8807d-198">Em Olá esse tempo política está vazia e outros cmdlets são necessário toodefine os itens a serem incluídos ou excluídos, quando os backups serão executados e Olá onde os backups serão armazenados.</span><span class="sxs-lookup"><span data-stu-id="8807d-198">At this time hello policy is empty and other cmdlets are needed toodefine what items will be included or excluded, when backups will run, and where hello backups will be stored.</span></span>

### <a name="configuring-hello-backup-schedule"></a><span data-ttu-id="8807d-199">Configurar o agendamento de backup Olá</span><span class="sxs-lookup"><span data-stu-id="8807d-199">Configuring hello backup schedule</span></span>
<span data-ttu-id="8807d-200">Olá pela primeira vez da saudação 3 partes de uma política é agenda de backup hello, que é criada usando Olá [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8807d-200">hello first of hello 3 parts of a policy is hello backup schedule, which is created using hello [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span></span> <span data-ttu-id="8807d-201">agendamento de backup Olá define quando backups necessário toobe realizada.</span><span class="sxs-lookup"><span data-stu-id="8807d-201">hello backup schedule defines when backups need toobe taken.</span></span> <span data-ttu-id="8807d-202">Ao criar um agendamento, você precisa toospecify 2 parâmetros de entrada:</span><span class="sxs-lookup"><span data-stu-id="8807d-202">When creating a schedule you need toospecify 2 input parameters:</span></span>

* <span data-ttu-id="8807d-203">**Dias da semana Olá** backup Olá deve ser executado.</span><span class="sxs-lookup"><span data-stu-id="8807d-203">**Days of hello week** that hello backup should run.</span></span> <span data-ttu-id="8807d-204">Você pode executar o trabalho de backup de saudação em apenas um dia, ou todos os dias da semana hello ou qualquer combinação entre.</span><span class="sxs-lookup"><span data-stu-id="8807d-204">You can run hello backup job on just one day, or every day of hello week, or any combination in between.</span></span>
* <span data-ttu-id="8807d-205">**Horas do dia Olá** quando backup Olá deve ser executado.</span><span class="sxs-lookup"><span data-stu-id="8807d-205">**Times of hello day** when hello backup should run.</span></span> <span data-ttu-id="8807d-206">Você pode definir o too3 diferentes momentos do dia hello quando backup Olá será disparado.</span><span class="sxs-lookup"><span data-stu-id="8807d-206">You can define up too3 different times of hello day when hello backup will be triggered.</span></span>

<span data-ttu-id="8807d-207">Por exemplo, você poderia configurar uma política de backup que é executada às 16h todo sábado e domingo.</span><span class="sxs-lookup"><span data-stu-id="8807d-207">For instance, you could configure a backup policy that runs at 4PM every Saturday and Sunday.</span></span>

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

<span data-ttu-id="8807d-208">agendamento de backup Olá precisa toobe associado a uma política e isso pode ser obtido usando Olá [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8807d-208">hello backup schedule needs toobe associated with a policy, and this can be achieved by using hello [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span></span>

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a><span data-ttu-id="8807d-209">Configurando uma política de retenção</span><span class="sxs-lookup"><span data-stu-id="8807d-209">Configuring a retention policy</span></span>
<span data-ttu-id="8807d-210">política de retenção Olá define quanto tempo recuperação pontos criados a partir de trabalhos de backup são mantidos.</span><span class="sxs-lookup"><span data-stu-id="8807d-210">hello retention policy defines how long recovery points created from backup jobs are retained.</span></span> <span data-ttu-id="8807d-211">Ao criar uma nova política de retenção usando Olá [OBRetentionPolicy novo](https://technet.microsoft.com/library/hh770425) cmdlet, você pode especificar Olá de dias que Olá pontos de recuperação de backup é necessário toobe mantida com o Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="8807d-211">When creating a new retention policy using hello [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, you can specify hello number of days that hello backup recovery points need toobe retained with Azure Backup.</span></span> <span data-ttu-id="8807d-212">exemplo Hello abaixo define uma política de retenção de sete dias.</span><span class="sxs-lookup"><span data-stu-id="8807d-212">hello example below sets a retention policy of 7 days.</span></span>

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

<span data-ttu-id="8807d-213">Olá política de retenção deve ser associada com a política principal hello, usando o cmdlet Olá [OBRetentionPolicy conjunto](https://technet.microsoft.com/library/hh770405):</span><span class="sxs-lookup"><span data-stu-id="8807d-213">hello retention policy must be associated with hello main policy using hello cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span></span>

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
### <a name="including-and-excluding-files-toobe-backed-up"></a><span data-ttu-id="8807d-214">Incluindo e excluindo arquivos toobe backup</span><span class="sxs-lookup"><span data-stu-id="8807d-214">Including and excluding files toobe backed up</span></span>
<span data-ttu-id="8807d-215">Um ```OBFileSpec``` objeto define Olá arquivos toobe incluído e excluído em um backup.</span><span class="sxs-lookup"><span data-stu-id="8807d-215">An ```OBFileSpec``` object defines hello files toobe included and excluded in a backup.</span></span> <span data-ttu-id="8807d-216">Este é um conjunto de regras que verificam a saudação arquivos e pastas protegidos em um computador.</span><span class="sxs-lookup"><span data-stu-id="8807d-216">This is a set of rules that scope out hello protected files and folders on a machine.</span></span> <span data-ttu-id="8807d-217">Você pode ter muitas regras de inclusão ou exclusão de arquivos conforme necessário e associá-las a uma política.</span><span class="sxs-lookup"><span data-stu-id="8807d-217">You can have as many file inclusion or exclusion rules as required, and associate them with a policy.</span></span> <span data-ttu-id="8807d-218">Ao criar um novo objeto OBFileSpec, você pode:</span><span class="sxs-lookup"><span data-stu-id="8807d-218">When creating a new OBFileSpec object, you can:</span></span>

* <span data-ttu-id="8807d-219">Especifique a saudação toobe arquivos e pastas incluído</span><span class="sxs-lookup"><span data-stu-id="8807d-219">Specify hello files and folders toobe included</span></span>
* <span data-ttu-id="8807d-220">Especifique a saudação toobe arquivos e pastas excluído</span><span class="sxs-lookup"><span data-stu-id="8807d-220">Specify hello files and folders toobe excluded</span></span>
* <span data-ttu-id="8807d-221">Especifica recursiva de backup de dados em uma pasta (ou) se apenas Olá nível superior arquivos na pasta especificada Olá devem ser feitos backup.</span><span class="sxs-lookup"><span data-stu-id="8807d-221">Specify recursive backup of data in a folder (or) whether only hello top-level files in hello specified folder should be backed up.</span></span>

<span data-ttu-id="8807d-222">Olá este último é obtida usando o sinalizador de não - recursivo Olá no comando Olá New-OBFileSpec.</span><span class="sxs-lookup"><span data-stu-id="8807d-222">hello latter is achieved by using hello -NonRecursive flag in hello New-OBFileSpec command.</span></span>

<span data-ttu-id="8807d-223">O exemplo hello abaixo, vamos fazer backup de volume c: e d e excluir os binários do sistema operacional Olá na pasta do Windows hello e qualquer pasta temporária.</span><span class="sxs-lookup"><span data-stu-id="8807d-223">In hello example below, we'll back up volume C: and D: and exclude hello OS binaries in hello Windows folder and any temporary folders.</span></span> <span data-ttu-id="8807d-224">toodo portanto vamos criar duas especificações de arquivo usando Olá [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - uma para inclusão e outra para exclusão.</span><span class="sxs-lookup"><span data-stu-id="8807d-224">toodo so we'll create two file specifications using hello [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - one for inclusion and one for exclusion.</span></span> <span data-ttu-id="8807d-225">Depois que criar especificações de arquivo hello, eles são associados com a política de saudação usando Olá [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8807d-225">Once hello file specifications have been created, they're associated with hello policy using hello [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span></span>

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

### <a name="applying-hello-policy"></a><span data-ttu-id="8807d-226">Aplicar a diretiva de saudação</span><span class="sxs-lookup"><span data-stu-id="8807d-226">Applying hello policy</span></span>
<span data-ttu-id="8807d-227">Agora o objeto de diretiva de saudação for concluído e tem um agendamento de backup associado, política de retenção e uma lista de inclusão/exclusão de arquivos.</span><span class="sxs-lookup"><span data-stu-id="8807d-227">Now hello policy object is complete and has an associated backup schedule, retention policy, and an inclusion/exclusion list of files.</span></span> <span data-ttu-id="8807d-228">Esta política agora pode ser confirmada para toouse de Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="8807d-228">This policy can now be committed for Azure Backup toouse.</span></span> <span data-ttu-id="8807d-229">Antes de aplicar Olá recém-criado política Certifique-se de que não há nenhuma política de backup existente associada ao servidor de saudação usando Olá [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8807d-229">Before you apply hello newly created policy ensure that there are no existing backup policies associated with hello server by using hello [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span></span> <span data-ttu-id="8807d-230">Remover a política de saudação solicita confirmação.</span><span class="sxs-lookup"><span data-stu-id="8807d-230">Removing hello policy will prompt for confirmation.</span></span> <span data-ttu-id="8807d-231">confirmação de saudação tooskip usar Olá ```-Confirm:$false``` sinalizador com hello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8807d-231">tooskip hello confirmation use hello ```-Confirm:$false``` flag with hello cmdlet.</span></span>

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want tooremove this backup policy? This will delete all hello backed up data. [Y] Yes [A] Yes tooAll [N] No [L] No tooAll [S] Suspend [?] Help (default is "Y"):
```

<span data-ttu-id="8807d-232">Objeto de diretiva de saudação de confirmação é feito usando Olá [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8807d-232">Committing hello policy object is done using hello [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span></span> <span data-ttu-id="8807d-233">Isso também gerará uma solicitação de confirmação.</span><span class="sxs-lookup"><span data-stu-id="8807d-233">This will also ask for confirmation.</span></span> <span data-ttu-id="8807d-234">confirmação de saudação tooskip usar Olá ```-Confirm:$false``` sinalizador com hello cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8807d-234">tooskip hello confirmation use hello ```-Confirm:$false``` flag with hello cmdlet.</span></span>

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

<span data-ttu-id="8807d-235">Você pode exibir detalhes de Olá Olá existente da política de backup usando Olá [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8807d-235">You can view hello details of hello existing backup policy using hello [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span></span> <span data-ttu-id="8807d-236">Você pode detalhamento ainda mais usando Olá [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet para o agendamento de backup hello e hello [OBRetentionPolicy Get](https://technet.microsoft.com/library/hh770427) cmdlet Olá das políticas de retenção</span><span class="sxs-lookup"><span data-stu-id="8807d-236">You can drill-down further using hello [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet for hello backup schedule and hello [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet for hello retention policies</span></span>

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

### <a name="performing-an-ad-hoc-backup"></a><span data-ttu-id="8807d-237">Executando um backup ad hoc</span><span class="sxs-lookup"><span data-stu-id="8807d-237">Performing an ad-hoc backup</span></span>
<span data-ttu-id="8807d-238">Quando uma política de backup foi definida backups Olá ocorrerá por agendamento hello.</span><span class="sxs-lookup"><span data-stu-id="8807d-238">Once a backup policy has been set hello backups will occur per hello schedule.</span></span> <span data-ttu-id="8807d-239">Também é possível usar Olá acionar um backup ad-hoc [OBBackup início](https://technet.microsoft.com/library/hh770426) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="8807d-239">Triggering an ad-hoc backup is also possible using hello [Start-OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span></span>

```
PS C:> Get-OBPolicy | Start-OBBackup
Taking snapshot of volumes...
Preparing storage...
Estimating size of backup items...
Estimating size of backup items...
Transferring data...
Verifying backup...
Job completed.
hello backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a><span data-ttu-id="8807d-240">Restaurar dados por meio do Backup do Azure</span><span class="sxs-lookup"><span data-stu-id="8807d-240">Restore data from Azure Backup</span></span>
<span data-ttu-id="8807d-241">Esta seção o guiará pelas etapas de saudação para automatizar a recuperação de dados de Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="8807d-241">This section will guide you through hello steps for automating recovery of data from Azure Backup.</span></span> <span data-ttu-id="8807d-242">Fazer assim envolve Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="8807d-242">Doing so involves hello following steps:</span></span>

1. <span data-ttu-id="8807d-243">Selecione o volume de origem Olá</span><span class="sxs-lookup"><span data-stu-id="8807d-243">Pick hello source volume</span></span>
2. <span data-ttu-id="8807d-244">Escolha um toorestore de ponto de backup</span><span class="sxs-lookup"><span data-stu-id="8807d-244">Choose a backup point toorestore</span></span>
3. <span data-ttu-id="8807d-245">Escolha um item toorestore</span><span class="sxs-lookup"><span data-stu-id="8807d-245">Choose an item toorestore</span></span>
4. <span data-ttu-id="8807d-246">Processo de restauração de saudação do gatilho</span><span class="sxs-lookup"><span data-stu-id="8807d-246">Trigger hello restore process</span></span>

### <a name="picking-hello-source-volume"></a><span data-ttu-id="8807d-247">Volume de origem de saudação de separação</span><span class="sxs-lookup"><span data-stu-id="8807d-247">Picking hello source volume</span></span>
<span data-ttu-id="8807d-248">Ordem toorestore um item de Backup do Azure, você primeiro precisa tooidentify origem de saudação do item de saudação.</span><span class="sxs-lookup"><span data-stu-id="8807d-248">In order toorestore an item from Azure Backup, you first need tooidentify hello source of hello item.</span></span> <span data-ttu-id="8807d-249">Como executamos comandos Olá no contexto de saudação de um servidor do Windows ou um cliente do Windows, a máquina Olá já está identificada.</span><span class="sxs-lookup"><span data-stu-id="8807d-249">Since we're executing hello commands in hello context of a Windows Server or a Windows client, hello machine is already identified.</span></span> <span data-ttu-id="8807d-250">Olá próxima etapa na identificação de fonte de saudação é tooidentify volume de saudação que o contém.</span><span class="sxs-lookup"><span data-stu-id="8807d-250">hello next step in identifying hello source is tooidentify hello volume containing it.</span></span> <span data-ttu-id="8807d-251">Uma lista de volumes ou fontes de backup deste computador pode ser recuperado por meio da execução Olá [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8807d-251">A list of volumes or sources being backed up from this machine can be retrieved by executing hello [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span></span> <span data-ttu-id="8807d-252">Esse comando retorna uma matriz de todas as fontes de saudação backup desse servidor/cliente.</span><span class="sxs-lookup"><span data-stu-id="8807d-252">This command returns an array of all hello sources backed up from this server/client.</span></span>

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

### <a name="choosing-a-backup-point-toorestore"></a><span data-ttu-id="8807d-253">Escolhendo um toorestore de ponto de backup</span><span class="sxs-lookup"><span data-stu-id="8807d-253">Choosing a backup point toorestore</span></span>
<span data-ttu-id="8807d-254">Olá lista de pontos de backup pode ser recuperada por meio da execução Olá [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet com os parâmetros apropriados.</span><span class="sxs-lookup"><span data-stu-id="8807d-254">hello list of backup points can be retrieved by executing hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet with appropriate parameters.</span></span> <span data-ttu-id="8807d-255">Em nosso exemplo, vamos escolher ponto de backup mais recente Olá para o volume de origem Olá *unidade d:* e usá-lo toorecover um arquivo específico.</span><span class="sxs-lookup"><span data-stu-id="8807d-255">In our example, we’ll choose hello latest backup point for hello source volume *D:* and use it toorecover a specific file.</span></span>

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
<span data-ttu-id="8807d-256">objeto Olá ```$rps``` é uma matriz de pontos de backup.</span><span class="sxs-lookup"><span data-stu-id="8807d-256">hello object ```$rps``` is an array of backup points.</span></span> <span data-ttu-id="8807d-257">Olá primeiro elemento é o último ponto de saudação e enésimo elemento de saudação é ponto mais antigo hello.</span><span class="sxs-lookup"><span data-stu-id="8807d-257">hello first element is hello latest point and hello Nth element is hello oldest point.</span></span> <span data-ttu-id="8807d-258">ponto mais recente do toochoose Olá, vamos usar ```$rps[0]```.</span><span class="sxs-lookup"><span data-stu-id="8807d-258">toochoose hello latest point, we will use ```$rps[0]```.</span></span>

### <a name="choosing-an-item-toorestore"></a><span data-ttu-id="8807d-259">Escolher um item toorestore</span><span class="sxs-lookup"><span data-stu-id="8807d-259">Choosing an item toorestore</span></span>
<span data-ttu-id="8807d-260">Olá tooidentify exato do arquivo ou pasta toorestore, recursivamente usar Olá [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8807d-260">tooidentify hello exact file or folder toorestore, recursively use hello [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span></span> <span data-ttu-id="8807d-261">Essa hierarquia de pasta maneira Olá possa ser navegada exclusivamente usando Olá ```Get-OBRecoverableItem```.</span><span class="sxs-lookup"><span data-stu-id="8807d-261">That way hello folder hierarchy can be browsed solely using hello ```Get-OBRecoverableItem```.</span></span>

<span data-ttu-id="8807d-262">Neste exemplo, se quisermos que o arquivo de saudação toorestore *finances.xls* podemos fazer referência a esse usando objeto Olá ```$filesFolders[1]```.</span><span class="sxs-lookup"><span data-stu-id="8807d-262">In this example, if we want toorestore hello file *finances.xls* we can reference that using hello object ```$filesFolders[1]```.</span></span>

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

<span data-ttu-id="8807d-263">Você também pode procurar itens toorestore usando Olá ```Get-OBRecoverableItem``` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8807d-263">You can also search for items toorestore using hello ```Get-OBRecoverableItem``` cmdlet.</span></span> <span data-ttu-id="8807d-264">Em nosso exemplo, toosearch para *finances.xls* foi possível obter um identificador de arquivo hello executando este comando:</span><span class="sxs-lookup"><span data-stu-id="8807d-264">In our example, toosearch for *finances.xls* we could get a handle on hello file by running this command:</span></span>

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-hello-restore-process"></a><span data-ttu-id="8807d-265">Disparar o processo de restauração Olá</span><span class="sxs-lookup"><span data-stu-id="8807d-265">Triggering hello restore process</span></span>
<span data-ttu-id="8807d-266">tootrigger o processo de restauração Olá, é preciso primeiro toospecify opções de recuperação de saudação.</span><span class="sxs-lookup"><span data-stu-id="8807d-266">tootrigger hello restore process, we first need toospecify hello recovery options.</span></span> <span data-ttu-id="8807d-267">Isso pode ser feito usando Olá [OBRecoveryOption novo](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8807d-267">This can be done by using hello [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span></span> <span data-ttu-id="8807d-268">Neste exemplo, vamos supor que queremos arquivos de saudação toorestore muito*C:\temp*. Vamos supor também que desejamos tooskip arquivos já existentes na pasta de destino Olá *C:\temp*. toocreate tal uma opção de recuperação, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="8807d-268">For this example, let's assume that we want toorestore hello files too*C:\temp*. Let's also assume that we want tooskip files that already exist on hello destination folder *C:\temp*. toocreate such a recovery option, use hello following command:</span></span>

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

<span data-ttu-id="8807d-269">Agora acionar a restauração usando Olá [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) comando Olá selecionado ```$item``` da saída de saudação de saudação ```Get-OBRecoverableItem``` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="8807d-269">Now trigger restore by using hello [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) command on hello selected ```$item``` from hello output of hello ```Get-OBRecoverableItem``` cmdlet:</span></span>

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
hello recovery operation completed successfully.
```


## <a name="uninstalling-hello-azure-backup-agent"></a><span data-ttu-id="8807d-270">Desinstalar o agente de Backup do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="8807d-270">Uninstalling hello Azure Backup agent</span></span>
<span data-ttu-id="8807d-271">Desinstalando agente de Backup do Azure Olá pode ser feito usando o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="8807d-271">Uninstalling hello Azure Backup agent can be done by using hello following command:</span></span>

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

<span data-ttu-id="8807d-272">Desinstalar os binários de agente de saudação da máquina de saudação tem algumas tooconsider consequências:</span><span class="sxs-lookup"><span data-stu-id="8807d-272">Uninstalling hello agent binaries from hello machine has some consequences tooconsider:</span></span>

* <span data-ttu-id="8807d-273">Ele remove o filtro de arquivo hello da máquina de saudação e controle de alterações é interrompido.</span><span class="sxs-lookup"><span data-stu-id="8807d-273">It removes hello file-filter from hello machine, and tracking of changes is stopped.</span></span>
* <span data-ttu-id="8807d-274">Todas as informações de política são removidas da máquina de hello, mas as informações de política de saudação continuam toobe armazenado no serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="8807d-274">All policy information is removed from hello machine, but hello policy information continues toobe stored in hello service.</span></span>
* <span data-ttu-id="8807d-275">Todos os agendamentos de backup são removidos e nenhum backup posterior é realizado.</span><span class="sxs-lookup"><span data-stu-id="8807d-275">All backup schedules are removed, and no further backups are taken.</span></span>

<span data-ttu-id="8807d-276">No entanto, Olá dados armazenados no Azure permanece e retidos de acordo com a configuração de política de retenção Olá por você.</span><span class="sxs-lookup"><span data-stu-id="8807d-276">However, hello data stored in Azure remains and is retained as per hello retention policy setup by you.</span></span> <span data-ttu-id="8807d-277">Os pontos mais antigos são desatualizados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8807d-277">Older points are automatically aged out.</span></span>

## <a name="remote-management"></a><span data-ttu-id="8807d-278">Gerenciamento remoto</span><span class="sxs-lookup"><span data-stu-id="8807d-278">Remote management</span></span>
<span data-ttu-id="8807d-279">Todo o gerenciamento de saudação em torno de agente de Backup do Azure hello, políticas e fontes de dados pode ser feito remotamente por meio do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8807d-279">All hello management around hello Azure Backup agent, policies, and data sources can be done remotely through PowerShell.</span></span> <span data-ttu-id="8807d-280">máquina de saudação que será gerenciada remotamente precisa toobe preparado corretamente.</span><span class="sxs-lookup"><span data-stu-id="8807d-280">hello machine that will be managed remotely needs toobe prepared correctly.</span></span>

<span data-ttu-id="8807d-281">Por padrão, a saudação serviço WinRM está configurada para inicialização manual.</span><span class="sxs-lookup"><span data-stu-id="8807d-281">By default, hello WinRM service is configured for manual startup.</span></span> <span data-ttu-id="8807d-282">tipo de inicialização de saudação deve ser definido muito*automáticas* e Olá serviço deve ser iniciado.</span><span class="sxs-lookup"><span data-stu-id="8807d-282">hello startup type must be set too*Automatic* and hello service should be started.</span></span> <span data-ttu-id="8807d-283">tooverify que Olá serviço WinRM está em execução, o valor Olá Olá propriedade Status deve ser *executando*.</span><span class="sxs-lookup"><span data-stu-id="8807d-283">tooverify that hello WinRM service is running, hello value of hello Status property should be *Running*.</span></span>

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

<span data-ttu-id="8807d-284">O PowerShell deve ser configurado remotamente.</span><span class="sxs-lookup"><span data-stu-id="8807d-284">PowerShell should be configured for remoting.</span></span>

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up tooreceive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

<span data-ttu-id="8807d-285">máquina Olá agora pode ser gerenciada remotamente - a partir da instalação de saudação do agente de saudação.</span><span class="sxs-lookup"><span data-stu-id="8807d-285">hello machine can now be managed remotely - starting from hello installation of hello agent.</span></span> <span data-ttu-id="8807d-286">Por exemplo, hello script a seguir copia o computador remoto do hello agente toohello e instala-o.</span><span class="sxs-lookup"><span data-stu-id="8807d-286">For example, hello following script copies hello agent toohello remote machine and installs it.</span></span>

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a><span data-ttu-id="8807d-287">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8807d-287">Next steps</span></span>
<span data-ttu-id="8807d-288">Para obter mais informações sobre o Backup do Azure para Windows Server/Client, consulte</span><span class="sxs-lookup"><span data-stu-id="8807d-288">For more information about Azure Backup for Windows Server/Client see</span></span>

* [<span data-ttu-id="8807d-289">Introdução tooAzure Backup</span><span class="sxs-lookup"><span data-stu-id="8807d-289">Introduction tooAzure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="8807d-290">Fazer backup de servidores Windows</span><span class="sxs-lookup"><span data-stu-id="8807d-290">Back up Windows Servers</span></span>](backup-configure-vault.md)
