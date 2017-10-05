---
title: Usar o PowerShell para gerenciar backups do Windows Server no Azure | Microsoft Docs
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
ms.openlocfilehash: a8e20356ae383ee4fa2158ea544d5d0905028124
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-and-manage-backup-to-azure-for-windows-serverwindows-client-using-powershell"></a><span data-ttu-id="b9e06-103">Implantar e gerenciar o backup no Azure para o Windows Server/Windows Client usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9e06-103">Deploy and manage backup to Azure for Windows Server/Windows Client using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b9e06-104">ARM</span><span class="sxs-lookup"><span data-stu-id="b9e06-104">ARM</span></span>](backup-client-automation.md)
> * [<span data-ttu-id="b9e06-105">Clássico</span><span class="sxs-lookup"><span data-stu-id="b9e06-105">Classic</span></span>](backup-client-automation-classic.md)
>
>

<span data-ttu-id="b9e06-106">Este artigo explica como usar o PowerShell para fazer backup dos dados do Windows Server ou da estação de trabalho do Windows em um cofre de backup.</span><span class="sxs-lookup"><span data-stu-id="b9e06-106">This article explains how to use PowerShell to back up Windows Server or Windows workstation data to a backup vault.</span></span> <span data-ttu-id="b9e06-107">A Microsoft recomenda usar cofres dos Serviços de Recuperação para todas as novas implantações.</span><span class="sxs-lookup"><span data-stu-id="b9e06-107">Microsoft recommends using Recovery Services vaults for all new deployments.</span></span> <span data-ttu-id="b9e06-108">Se você for um novo usuário do Backup do Azure e não tiver criado um cofre de backup na sua assinatura, use o artigo [Implantar e gerenciar dados do Data Protection Manager para o Azure usando o PowerShell](backup-client-automation.md), de modo que você armazene seus dados em um cofre dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="b9e06-108">If you are a new Azure Backup user and have not created a backup vault in your subscription, use the article, [Deploy and manage Data Protection Manager data to Azure using PowerShell](backup-client-automation.md) so you store your data in a Recovery Services vault.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="b9e06-109">Agora você pode atualizar os cofres de Backup para cofres dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="b9e06-109">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="b9e06-110">Para obter detalhes, veja o artigo [Atualizar um cofre de Backup para um cofre dos Serviços de Recuperação](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="b9e06-110">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="b9e06-111">A Microsoft incentiva você a atualizar os cofres de Backup para os cofres dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="b9e06-111">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="b9e06-112">Após 15 de outubro de 2017, você não poderá usar o PowerShell para criar os Cofres do Backup.</span><span class="sxs-lookup"><span data-stu-id="b9e06-112">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="b9e06-113">**Em 1º de novembro de 2017**:</span><span class="sxs-lookup"><span data-stu-id="b9e06-113">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="b9e06-114">Todos os Cofres do Backup restantes serão atualizados automaticamente para os cofres dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="b9e06-114">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="b9e06-115">Você não poderá acessar os dados de backup no portal clássico.</span><span class="sxs-lookup"><span data-stu-id="b9e06-115">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="b9e06-116">Em vez disso, use o portal do Azure para acessar os dados de backup nos cofres dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="b9e06-116">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="install-azure-powershell"></a><span data-ttu-id="b9e06-117">Instalar o Azure Powershell</span><span class="sxs-lookup"><span data-stu-id="b9e06-117">Install Azure PowerShell</span></span>
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-include.md)]

<span data-ttu-id="b9e06-118">Em outubro de 2015, o Azure PowerShell 1.0 foi lançado.</span><span class="sxs-lookup"><span data-stu-id="b9e06-118">In October 2015, Azure PowerShell 1.0 was released.</span></span> <span data-ttu-id="b9e06-119">Essa versão veio logo após a 0.9.8 e trouxe algumas alterações importantes, especialmente no padrão de nomenclatura dos cmdlets.</span><span class="sxs-lookup"><span data-stu-id="b9e06-119">This release succeeded the 0.9.8 release and brought about some significant changes, especially in the naming pattern of the cmdlets.</span></span> <span data-ttu-id="b9e06-120">Os cmdlets da versão 1.0 seguem o padrão de nomenclatura {verbo}-AzureRm{substantivo}; por outro lado, os nomes da versão 0.9.8 não incluem **Rm** (por exemplo, New-AzureRmResourceGroup em vez de New-AzureResourceGroup).</span><span class="sxs-lookup"><span data-stu-id="b9e06-120">1.0 cmdlets follow the naming pattern {verb}-AzureRm{noun}; whereas, the 0.9.8 names do not include **Rm** (for example, New-AzureRmResourceGroup instead of New-AzureResourceGroup).</span></span> <span data-ttu-id="b9e06-121">Ao usar o Azure PowerShell 0.9.8, você deve primeiro habilitar o modo do Gerenciador de Recursos executando o comando **Switch-AzureMode AzureResourceManager** .</span><span class="sxs-lookup"><span data-stu-id="b9e06-121">When using Azure PowerShell 0.9.8, you must first enable the Resource Manager mode by running the **Switch-AzureMode AzureResourceManager** command.</span></span> <span data-ttu-id="b9e06-122">Este comando não é necessário na 1.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="b9e06-122">This command is not necessary in 1.0 or later.</span></span>

<span data-ttu-id="b9e06-123">Se você quiser usar seus scripts escritos para o ambiente da versão 0.9.8 no ambiente da versão 1.0 ou posterior, teste cuidadosamente os scripts em um ambiente de pré-produção antes de usá-los em produção, a fim de evitar o impacto inesperado.</span><span class="sxs-lookup"><span data-stu-id="b9e06-123">If you want to use your scripts written for the 0.9.8 environment, in the 1.0 or later environment, you should carefully test the scripts in a pre-production environment before using them in production to avoid unexpected impact.</span></span>

<span data-ttu-id="b9e06-124">[Baixe a última versão do PowerShell](https://github.com/Azure/azure-powershell/releases) (a versão mínima necessária é: 1.0.0)</span><span class="sxs-lookup"><span data-stu-id="b9e06-124">[Download the latest PowerShell release](https://github.com/Azure/azure-powershell/releases) (minimum version required is : 1.0.0)</span></span>

[!INCLUDE [arm-getting-setup-powershell](../../includes/arm-getting-setup-powershell.md)]

## <a name="create-a-backup-vault"></a><span data-ttu-id="b9e06-125">Criar um cofre de backup</span><span class="sxs-lookup"><span data-stu-id="b9e06-125">Create a backup vault</span></span>
> [!WARNING]
> <span data-ttu-id="b9e06-126">Para clientes usando o Backup do Azure pela primeira vez, você precisa registrar o provedor de Backup do Azure para ser usado com sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="b9e06-126">For customers using Azure Backup for the first time, you need to register the Azure Backup provider to be used with your subscription.</span></span> <span data-ttu-id="b9e06-127">Isso pode ser feito executando o seguinte comando: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span><span class="sxs-lookup"><span data-stu-id="b9e06-127">This can be done by running the following command: Register-AzureProvider -ProviderNamespace "Microsoft.Backup"</span></span>
>
>

<span data-ttu-id="b9e06-128">Você pode criar um novo cofre de backup usando o cmdlet **New-AzureRMBackupVault** .</span><span class="sxs-lookup"><span data-stu-id="b9e06-128">You can create a new backup vault using the **New-AzureRMBackupVault** cmdlet.</span></span> <span data-ttu-id="b9e06-129">O cofre de backup é um recurso do ARM e, portanto, você precisará colocá-lo em um Grupo de Recursos.</span><span class="sxs-lookup"><span data-stu-id="b9e06-129">The backup vault is an ARM resource, so you need to place it within a Resource Group.</span></span> <span data-ttu-id="b9e06-130">Em um console do Azure PowerShell com privilégios elevados, execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="b9e06-130">In an elevated Azure PowerShell console, run the following commands:</span></span>

```
PS C:\> New-AzureResourceGroup –Name “test-rg” -Region “West US”
PS C:\> $backupvault = New-AzureRMBackupVault –ResourceGroupName “test-rg” –Name “test-vault” –Region “West US” –Storage GeoRedundant
```

<span data-ttu-id="b9e06-131">Use o cmdlet **Get-AzureRMBackupVault** para listar os cofres de backup em uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="b9e06-131">Use the **Get-AzureRMBackupVault** cmdlet to list the backup vaults in a subscription.</span></span>

## <a name="installing-the-azure-backup-agent"></a><span data-ttu-id="b9e06-132">Instalando o agente de Backup do Azure</span><span class="sxs-lookup"><span data-stu-id="b9e06-132">Installing the Azure Backup agent</span></span>
<span data-ttu-id="b9e06-133">Antes de instalar o agente de Backup do Azure, você precisa ter o instalador baixado, já no Windows Server.</span><span class="sxs-lookup"><span data-stu-id="b9e06-133">Before you install the Azure Backup agent, you need to have the installer downloaded and present on the Windows Server.</span></span> <span data-ttu-id="b9e06-134">Você pode obter a versão mais recente do instalador no [Centro de Download da Microsoft](http://aka.ms/azurebackup_agent) ou da página Painel do cofre de backup.</span><span class="sxs-lookup"><span data-stu-id="b9e06-134">You can get the latest version of the installer from the [Microsoft Download Center](http://aka.ms/azurebackup_agent) or from the backup vault's Dashboard page.</span></span> <span data-ttu-id="b9e06-135">Salve o instalador em um local de fácil acesso, como *C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="b9e06-135">Save the installer to an easily accessible location like *C:\Downloads\*.</span></span>

<span data-ttu-id="b9e06-136">Para instalar o agente, execute o comando a seguir em um console do Azure PowerShell com privilégios elevados:</span><span class="sxs-lookup"><span data-stu-id="b9e06-136">To install the agent, run the following command in an elevated PowerShell console:</span></span>

```
PS C:\> MARSAgentInstaller.exe /q
```

<span data-ttu-id="b9e06-137">Isso instala o agente com todas as opções padrão.</span><span class="sxs-lookup"><span data-stu-id="b9e06-137">This installs the agent with all the default options.</span></span> <span data-ttu-id="b9e06-138">A instalação demora alguns minutos, em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="b9e06-138">The installation takes a few minutes in the background.</span></span> <span data-ttu-id="b9e06-139">Se você não especificar a opção */nu* , a janela do **Windows Update** será aberta no final da instalação para verificar se há atualizações.</span><span class="sxs-lookup"><span data-stu-id="b9e06-139">If you do not specify the */nu* option then the **Windows Update** window will open at the end of the installation to check for any updates.</span></span> <span data-ttu-id="b9e06-140">Uma vez instalado, o agente será exibido na lista de programas instalados.</span><span class="sxs-lookup"><span data-stu-id="b9e06-140">Once installed, the agent will show in the list of installed programs.</span></span>

<span data-ttu-id="b9e06-141">Para ver a lista de programas instalados, vá para **Painel de controle** > **Programas** > **Programas e recursos**.</span><span class="sxs-lookup"><span data-stu-id="b9e06-141">To see the list of installed programs, go to **Control Panel** > **Programs** > **Programs and Features**.</span></span>

![Agente instalado](./media/backup-client-automation/installed-agent-listing.png)

### <a name="installation-options"></a><span data-ttu-id="b9e06-143">Opções de instalação</span><span class="sxs-lookup"><span data-stu-id="b9e06-143">Installation options</span></span>
<span data-ttu-id="b9e06-144">Para ver todas as opções disponíveis por meio da linha de comando, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="b9e06-144">To see all the options available via the command-line, use the following command:</span></span>

```
PS C:\> MARSAgentInstaller.exe /?
```

<span data-ttu-id="b9e06-145">As opções disponíveis incluem:</span><span class="sxs-lookup"><span data-stu-id="b9e06-145">The available options include:</span></span>

| <span data-ttu-id="b9e06-146">Opção</span><span class="sxs-lookup"><span data-stu-id="b9e06-146">Option</span></span> | <span data-ttu-id="b9e06-147">Detalhes</span><span class="sxs-lookup"><span data-stu-id="b9e06-147">Details</span></span> | <span data-ttu-id="b9e06-148">Padrão</span><span class="sxs-lookup"><span data-stu-id="b9e06-148">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b9e06-149">/q</span><span class="sxs-lookup"><span data-stu-id="b9e06-149">/q</span></span> |<span data-ttu-id="b9e06-150">Instalação silenciosa</span><span class="sxs-lookup"><span data-stu-id="b9e06-150">Quiet installation</span></span> |- |
| <span data-ttu-id="b9e06-151">/p:"local"</span><span class="sxs-lookup"><span data-stu-id="b9e06-151">/p:"location"</span></span> |<span data-ttu-id="b9e06-152">Caminho para a pasta de instalação para o agente de Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9e06-152">Path to the installation folder for the Azure Backup agent.</span></span> |<span data-ttu-id="b9e06-153">C:\Arquivos de Programas\Microsoft Azure Recovery Services Agent</span><span class="sxs-lookup"><span data-stu-id="b9e06-153">C:\Program Files\Microsoft Azure Recovery Services Agent</span></span> |
| <span data-ttu-id="b9e06-154">/s:"local"</span><span class="sxs-lookup"><span data-stu-id="b9e06-154">/s:"location"</span></span> |<span data-ttu-id="b9e06-155">Caminho para a pasta de cache para o agente de Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9e06-155">Path to the cache folder for the Azure Backup agent.</span></span> |<span data-ttu-id="b9e06-156">C:\Arquivos de Programas\Microsoft Azure Recovery Services Agent\Scratch</span><span class="sxs-lookup"><span data-stu-id="b9e06-156">C:\Program Files\Microsoft Azure Recovery Services Agent\Scratch</span></span> |
| <span data-ttu-id="b9e06-157">/m</span><span class="sxs-lookup"><span data-stu-id="b9e06-157">/m</span></span> |<span data-ttu-id="b9e06-158">Aceitar o Microsoft Update</span><span class="sxs-lookup"><span data-stu-id="b9e06-158">Opt-in to Microsoft Update</span></span> |- |
| <span data-ttu-id="b9e06-159">/nu</span><span class="sxs-lookup"><span data-stu-id="b9e06-159">/nu</span></span> |<span data-ttu-id="b9e06-160">Não verificar se há atualizações após a conclusão da instalação</span><span class="sxs-lookup"><span data-stu-id="b9e06-160">Do not Check for updates after installation is complete</span></span> |- |
| <span data-ttu-id="b9e06-161">/d</span><span class="sxs-lookup"><span data-stu-id="b9e06-161">/d</span></span> |<span data-ttu-id="b9e06-162">Desinstala o agente dos Serviços de Recuperação do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="b9e06-162">Uninstalls Microsoft Azure Recovery Services Agent</span></span> |- |
| <span data-ttu-id="b9e06-163">/ph</span><span class="sxs-lookup"><span data-stu-id="b9e06-163">/ph</span></span> |<span data-ttu-id="b9e06-164">Endereço do host do proxy</span><span class="sxs-lookup"><span data-stu-id="b9e06-164">Proxy Host Address</span></span> |- |
| <span data-ttu-id="b9e06-165">/po</span><span class="sxs-lookup"><span data-stu-id="b9e06-165">/po</span></span> |<span data-ttu-id="b9e06-166">Número da porta do host do proxy</span><span class="sxs-lookup"><span data-stu-id="b9e06-166">Proxy Host Port Number</span></span> |- |
| <span data-ttu-id="b9e06-167">/pu</span><span class="sxs-lookup"><span data-stu-id="b9e06-167">/pu</span></span> |<span data-ttu-id="b9e06-168">UserName do host do proxy</span><span class="sxs-lookup"><span data-stu-id="b9e06-168">Proxy Host UserName</span></span> |- |
| <span data-ttu-id="b9e06-169">/pw</span><span class="sxs-lookup"><span data-stu-id="b9e06-169">/pw</span></span> |<span data-ttu-id="b9e06-170">Senha do proxy</span><span class="sxs-lookup"><span data-stu-id="b9e06-170">Proxy Password</span></span> |- |

## <a name="registering-with-the-azure-backup-service"></a><span data-ttu-id="b9e06-171">Registrando-se no serviço de Backup do Azure</span><span class="sxs-lookup"><span data-stu-id="b9e06-171">Registering with the Azure Backup service</span></span>
<span data-ttu-id="b9e06-172">Antes de poder se registrar no serviço de Backup do Azure, você precisa garantir que os [pré-requisitos](backup-configure-vault.md) sejam atendidos.</span><span class="sxs-lookup"><span data-stu-id="b9e06-172">Before you can register with the Azure Backup service, you need to ensure that the [prerequisites](backup-configure-vault.md) are met.</span></span> <span data-ttu-id="b9e06-173">Você deve:</span><span class="sxs-lookup"><span data-stu-id="b9e06-173">You must:</span></span>

* <span data-ttu-id="b9e06-174">Ter uma assinatura válida do Azure</span><span class="sxs-lookup"><span data-stu-id="b9e06-174">Have a valid Azure subscription</span></span>
* <span data-ttu-id="b9e06-175">Ter um cofre de backup</span><span class="sxs-lookup"><span data-stu-id="b9e06-175">Have a backup vault</span></span>

<span data-ttu-id="b9e06-176">Para baixar as credenciais do cofre, execute o cmdlet **Get-AzureRMBackupVaultCredentials** em um console do Azure PowerShell e armazene-o em um local conveniente, como *C:\Downloads\*.</span><span class="sxs-lookup"><span data-stu-id="b9e06-176">To download the vault credentials, run the **Get-AzureRMBackupVaultCredentials** cmdlet in an Azure PowerShell console and store it in a convenient location like *C:\Downloads\*.</span></span>

```
PS C:\> $credspath = "C:\"
PS C:\> $credsfilename = Get-AzureRMBackupVaultCredentials -Vault $backupvault -TargetLocation $credspath
PS C:\> $credsfilename
f5303a0b-fae4-4cdb-b44d-0e4c032dde26_backuprg_backuprn_2015-08-11--06-22-35.VaultCredentials
```

<span data-ttu-id="b9e06-177">O registro da máquina no cofre é feito usando o [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b9e06-177">Registering the machine with the vault is done using the [Start-OBRegistration](https://technet.microsoft.com/library/hh770398%28v=wps.630%29.aspx) cmdlet:</span></span>

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
> <span data-ttu-id="b9e06-178">Não use caminhos relativos para especificar o arquivo de credenciais do cofre.</span><span class="sxs-lookup"><span data-stu-id="b9e06-178">Do not use relative paths to specify the vault credentials file.</span></span> <span data-ttu-id="b9e06-179">Você deve fornecer um caminho absoluto como entrada para o cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b9e06-179">You must provide an absolute path as an input to the cmdlet.</span></span>
>
>

## <a name="networking-settings"></a><span data-ttu-id="b9e06-180">Configurações de rede</span><span class="sxs-lookup"><span data-stu-id="b9e06-180">Networking settings</span></span>
<span data-ttu-id="b9e06-181">Quando a conectividade do computador Windows com a internet for através de um servidor proxy, as configurações de proxy também podem ser fornecidas para o agente.</span><span class="sxs-lookup"><span data-stu-id="b9e06-181">When the connectivity of the Windows machine to the internet is through a proxy server, the proxy settings can also be provided to the agent.</span></span> <span data-ttu-id="b9e06-182">Neste exemplo, não há nenhum servidor proxy, por isso estamos explicitamente omitindo todas as informações relacionadas a proxy.</span><span class="sxs-lookup"><span data-stu-id="b9e06-182">In this example, there is no proxy server, so we are explicitly clearing any proxy-related information.</span></span>

<span data-ttu-id="b9e06-183">O uso de largura de banda também pode ser controlado com as opções de ```work hour bandwidth``` e ```non-work hour bandwidth``` para um determinado conjunto de dias da semana.</span><span class="sxs-lookup"><span data-stu-id="b9e06-183">Bandwidth usage can also be controlled with the options of ```work hour bandwidth``` and ```non-work hour bandwidth``` for a given set of days of the week.</span></span>

<span data-ttu-id="b9e06-184">A configuração dos detalhes de proxy e largura de banda é feita usando o [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="b9e06-184">Setting the proxy and bandwidth details is done using the [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409%28v=wps.630%29.aspx) cmdlet:</span></span>

```
PS C:\> Set-OBMachineSetting -NoProxy
Server properties updated successfully.

PS C:\> Set-OBMachineSetting -NoThrottle
Server properties updated successfully.
```

## <a name="encryption-settings"></a><span data-ttu-id="b9e06-185">Configurações de criptografia</span><span class="sxs-lookup"><span data-stu-id="b9e06-185">Encryption settings</span></span>
<span data-ttu-id="b9e06-186">Os dados de backup enviados para o Backup do Azure são criptografados para proteger a confidencialidade dos dados.</span><span class="sxs-lookup"><span data-stu-id="b9e06-186">The backup data sent to Azure Backup is encrypted to protect the confidentiality of the data.</span></span> <span data-ttu-id="b9e06-187">A senha de criptografia é a "senha" para descriptografar os dados no momento da restauração.</span><span class="sxs-lookup"><span data-stu-id="b9e06-187">The encryption passphrase is the "password" to decrypt the data at the time of restore.</span></span>

```
PS C:\> ConvertTo-SecureString -String "Complex!123_STRING" -AsPlainText -Force | Set-OBMachineSetting
Server properties updated successfully
```

> [!IMPORTANT]
> <span data-ttu-id="b9e06-188">Mantenha as informações de senha seguras e protegidas depois de defini-las.</span><span class="sxs-lookup"><span data-stu-id="b9e06-188">Keep the passphrase information safe and secure once it is set.</span></span> <span data-ttu-id="b9e06-189">Você não poderá restaurar os dados do Azure sem essa senha.</span><span class="sxs-lookup"><span data-stu-id="b9e06-189">You will not be able to restore data from Azure without this passphrase.</span></span>
>
>

## <a name="back-up-files-and-folders"></a><span data-ttu-id="b9e06-190">Fazer backup de arquivos e pastas</span><span class="sxs-lookup"><span data-stu-id="b9e06-190">Back up files and folders</span></span>
<span data-ttu-id="b9e06-191">Todos os seus backups de servidores e clientes Windows para o Azure Backup são controlados por uma política.</span><span class="sxs-lookup"><span data-stu-id="b9e06-191">All your backups from Windows Servers and clients to Azure Backup are governed by a policy.</span></span> <span data-ttu-id="b9e06-192">A política consiste em três partes:</span><span class="sxs-lookup"><span data-stu-id="b9e06-192">The policy comprises three parts:</span></span>

1. <span data-ttu-id="b9e06-193">Um **agendamento de backup** que especifica quando backups precisam ser efetuados e sincronizados com o serviço.</span><span class="sxs-lookup"><span data-stu-id="b9e06-193">A **backup schedule** that specifies when backups need to be taken and synchronized with the service.</span></span>
2. <span data-ttu-id="b9e06-194">Um **cronograma de retenção** que especifica quanto tempo deve-se manter os pontos de recuperação no Azure.</span><span class="sxs-lookup"><span data-stu-id="b9e06-194">A **retention schedule** that specifies how long to retain the recovery points in Azure.</span></span>
3. <span data-ttu-id="b9e06-195">Uma **especificação de inclusão/exclusão de arquivo** que determina de que conteúdo deve-se realizar o backup.</span><span class="sxs-lookup"><span data-stu-id="b9e06-195">A **file inclusion/exclusion specification** that dictates what should be backed up.</span></span>

<span data-ttu-id="b9e06-196">Neste documento, já que estamos automatizando o backup, vamos pressupor que nada foi configurado.</span><span class="sxs-lookup"><span data-stu-id="b9e06-196">In this document, since we're automating backup, we'll assume nothing has been configured.</span></span> <span data-ttu-id="b9e06-197">Começamos criando uma nova política de backup por meio do cmdlet [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) e usando-a.</span><span class="sxs-lookup"><span data-stu-id="b9e06-197">We begin by creating a new backup policy using the [New-OBPolicy](https://technet.microsoft.com/library/hh770416.aspx) cmdlet and using it.</span></span>

```
PS C:\> $newpolicy = New-OBPolicy
```

<span data-ttu-id="b9e06-198">Neste momento, a política está vazia e outros cmdlets são necessários para definir quais itens serão incluídos ou excluídos, quando backups serão executados e onde os backups serão armazenados.</span><span class="sxs-lookup"><span data-stu-id="b9e06-198">At this time the policy is empty and other cmdlets are needed to define what items will be included or excluded, when backups will run, and where the backups will be stored.</span></span>

### <a name="configuring-the-backup-schedule"></a><span data-ttu-id="b9e06-199">Configurando o agendamento de backup</span><span class="sxs-lookup"><span data-stu-id="b9e06-199">Configuring the backup schedule</span></span>
<span data-ttu-id="b9e06-200">A primeira das três partes de uma política é o agendamento de backup, que é criado usando o cmdlet [New-OBSchedule](https://technet.microsoft.com/library/hh770401) .</span><span class="sxs-lookup"><span data-stu-id="b9e06-200">The first of the 3 parts of a policy is the backup schedule, which is created using the [New-OBSchedule](https://technet.microsoft.com/library/hh770401) cmdlet.</span></span> <span data-ttu-id="b9e06-201">O agendamento de backup define quando os backups precisam ser executados.</span><span class="sxs-lookup"><span data-stu-id="b9e06-201">The backup schedule defines when backups need to be taken.</span></span> <span data-ttu-id="b9e06-202">Ao criar um agendamento, você precisa especificar dois parâmetros de entrada:</span><span class="sxs-lookup"><span data-stu-id="b9e06-202">When creating a schedule you need to specify 2 input parameters:</span></span>

* <span data-ttu-id="b9e06-203">**dias da semana** nos quais o backup deve ser executado.</span><span class="sxs-lookup"><span data-stu-id="b9e06-203">**Days of the week** that the backup should run.</span></span> <span data-ttu-id="b9e06-204">Você pode executar o trabalho de backup em apenas um dia ou em todos os dias da semana, ou qualquer combinação entre essas opções.</span><span class="sxs-lookup"><span data-stu-id="b9e06-204">You can run the backup job on just one day, or every day of the week, or any combination in between.</span></span>
* <span data-ttu-id="b9e06-205">**horários do dia** quando o backup deve ser executado.</span><span class="sxs-lookup"><span data-stu-id="b9e06-205">**Times of the day** when the backup should run.</span></span> <span data-ttu-id="b9e06-206">Você pode definir até três horários do dia diferentes quando o backup será disparado.</span><span class="sxs-lookup"><span data-stu-id="b9e06-206">You can define up to 3 different times of the day when the backup will be triggered.</span></span>

<span data-ttu-id="b9e06-207">Por exemplo, você poderia configurar uma política de backup que é executada às 16h todo sábado e domingo.</span><span class="sxs-lookup"><span data-stu-id="b9e06-207">For instance, you could configure a backup policy that runs at 4PM every Saturday and Sunday.</span></span>

```
PS C:\> $sched = New-OBSchedule -DaysofWeek Saturday, Sunday -TimesofDay 16:00
```

<span data-ttu-id="b9e06-208">O agendamento de backup deve ser associado a uma política, e isso pode ser realizado usando o cmdlet [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) .</span><span class="sxs-lookup"><span data-stu-id="b9e06-208">The backup schedule needs to be associated with a policy, and this can be achieved by using the [Set-OBSchedule](https://technet.microsoft.com/library/hh770407) cmdlet.</span></span>

```
PS C:> Set-OBSchedule -Policy $newpolicy -Schedule $sched
BackupSchedule : 4:00 PM Saturday, Sunday, Every 1 week(s) DsList : PolicyName : RetentionPolicy : State : New PolicyState : Valid
```
### <a name="configuring-a-retention-policy"></a><span data-ttu-id="b9e06-209">Configurando uma política de retenção</span><span class="sxs-lookup"><span data-stu-id="b9e06-209">Configuring a retention policy</span></span>
<span data-ttu-id="b9e06-210">A política de retenção define por quanto tempo os pontos de recuperação criados por meio de trabalhos de backup são mantidos.</span><span class="sxs-lookup"><span data-stu-id="b9e06-210">The retention policy defines how long recovery points created from backup jobs are retained.</span></span> <span data-ttu-id="b9e06-211">Ao criar uma nova política de retenção usando o cmdlet [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) , você pode especificar o número de dias durante os quais os pontos de recuperação de backup precisam ser mantidos com o Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9e06-211">When creating a new retention policy using the [New-OBRetentionPolicy](https://technet.microsoft.com/library/hh770425) cmdlet, you can specify the number of days that the backup recovery points need to be retained with Azure Backup.</span></span> <span data-ttu-id="b9e06-212">O exemplo a seguir define uma política de retenção de sete dias.</span><span class="sxs-lookup"><span data-stu-id="b9e06-212">The example below sets a retention policy of 7 days.</span></span>

```
PS C:\> $retentionpolicy = New-OBRetentionPolicy -RetentionDays 7
```

<span data-ttu-id="b9e06-213">A política de retenção deve ser associada à política principal usando o cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span><span class="sxs-lookup"><span data-stu-id="b9e06-213">The retention policy must be associated with the main policy using the cmdlet [Set-OBRetentionPolicy](https://technet.microsoft.com/library/hh770405):</span></span>

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
### <a name="including-and-excluding-files-to-be-backed-up"></a><span data-ttu-id="b9e06-214">Incluindo e excluindo arquivos destinados a backup</span><span class="sxs-lookup"><span data-stu-id="b9e06-214">Including and excluding files to be backed up</span></span>
<span data-ttu-id="b9e06-215">Um objeto ```OBFileSpec``` define os arquivos a serem incluídos e excluídos em um backup.</span><span class="sxs-lookup"><span data-stu-id="b9e06-215">An ```OBFileSpec``` object defines the files to be included and excluded in a backup.</span></span> <span data-ttu-id="b9e06-216">Este é um conjunto de regras que definem o escopo dos arquivos e pastas protegidos em um computador.</span><span class="sxs-lookup"><span data-stu-id="b9e06-216">This is a set of rules that scope out the protected files and folders on a machine.</span></span> <span data-ttu-id="b9e06-217">Você pode ter muitas regras de inclusão ou exclusão de arquivos conforme necessário e associá-las a uma política.</span><span class="sxs-lookup"><span data-stu-id="b9e06-217">You can have as many file inclusion or exclusion rules as required, and associate them with a policy.</span></span> <span data-ttu-id="b9e06-218">Ao criar um novo objeto OBFileSpec, você pode:</span><span class="sxs-lookup"><span data-stu-id="b9e06-218">When creating a new OBFileSpec object, you can:</span></span>

* <span data-ttu-id="b9e06-219">Especificar os arquivos e pastas a serem incluídos</span><span class="sxs-lookup"><span data-stu-id="b9e06-219">Specify the files and folders to be included</span></span>
* <span data-ttu-id="b9e06-220">Especificar os arquivos e pastas a serem excluídos</span><span class="sxs-lookup"><span data-stu-id="b9e06-220">Specify the files and folders to be excluded</span></span>
* <span data-ttu-id="b9e06-221">Especificar o backup recursivo de dados em uma pasta ou o backup apenas dos arquivos de nível superior na pasta especificada.</span><span class="sxs-lookup"><span data-stu-id="b9e06-221">Specify recursive backup of data in a folder (or) whether only the top-level files in the specified folder should be backed up.</span></span>

<span data-ttu-id="b9e06-222">A última opção é obtida usando o sinalizador -NonRecursive no comando New-OBFileSpec.</span><span class="sxs-lookup"><span data-stu-id="b9e06-222">The latter is achieved by using the -NonRecursive flag in the New-OBFileSpec command.</span></span>

<span data-ttu-id="b9e06-223">No exemplo a seguir, vamos fazer backup dos volumes C: e D: e excluir os binários do sistema operacional na pasta do Windows e em quaisquer pastas temporárias.</span><span class="sxs-lookup"><span data-stu-id="b9e06-223">In the example below, we'll back up volume C: and D: and exclude the OS binaries in the Windows folder and any temporary folders.</span></span> <span data-ttu-id="b9e06-224">Para isso, vamos criar duas especificações de arquivo usando o cmdlet [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) – uma para inclusão e outra para exclusão.</span><span class="sxs-lookup"><span data-stu-id="b9e06-224">To do so we'll create two file specifications using the [New-OBFileSpec](https://technet.microsoft.com/library/hh770408) cmdlet - one for inclusion and one for exclusion.</span></span> <span data-ttu-id="b9e06-225">Depois que as especificações de arquivo são criadas, elas são associadas à política usando o cmdlet [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) .</span><span class="sxs-lookup"><span data-stu-id="b9e06-225">Once the file specifications have been created, they're associated with the policy using the [Add-OBFileSpec](https://technet.microsoft.com/library/hh770424) cmdlet.</span></span>

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

### <a name="applying-the-policy"></a><span data-ttu-id="b9e06-226">Aplicando a política</span><span class="sxs-lookup"><span data-stu-id="b9e06-226">Applying the policy</span></span>
<span data-ttu-id="b9e06-227">Agora, o objeto de política está concluído e tem um agendamento de backup associado, política de retenção e uma lista de inclusão/exclusões de arquivos.</span><span class="sxs-lookup"><span data-stu-id="b9e06-227">Now the policy object is complete and has an associated backup schedule, retention policy, and an inclusion/exclusion list of files.</span></span> <span data-ttu-id="b9e06-228">Esta política agora pode ser confirmada para uso pelo Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9e06-228">This policy can now be committed for Azure Backup to use.</span></span> <span data-ttu-id="b9e06-229">Antes de aplicar a política recém-criada, verifique se não há nenhuma política de backup existente associada ao servidor, por meio do cmdlet [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) .</span><span class="sxs-lookup"><span data-stu-id="b9e06-229">Before you apply the newly created policy ensure that there are no existing backup policies associated with the server by using the [Remove-OBPolicy](https://technet.microsoft.com/library/hh770415) cmdlet.</span></span> <span data-ttu-id="b9e06-230">Remover a política gerará uma solicitação de confirmação.</span><span class="sxs-lookup"><span data-stu-id="b9e06-230">Removing the policy will prompt for confirmation.</span></span> <span data-ttu-id="b9e06-231">Para ignorar a confirmação, use o sinalizador ```-Confirm:$false``` com o cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b9e06-231">To skip the confirmation use the ```-Confirm:$false``` flag with the cmdlet.</span></span>

```
PS C:> Get-OBPolicy | Remove-OBPolicy
Microsoft Azure Backup Are you sure you want to remove this backup policy? This will delete all the backed up data. [Y] Yes [A] Yes to All [N] No [L] No to All [S] Suspend [?] Help (default is "Y"):
```

<span data-ttu-id="b9e06-232">A confirmação do objeto de política é realizada usando o cmdlet [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) .</span><span class="sxs-lookup"><span data-stu-id="b9e06-232">Committing the policy object is done using the [Set-OBPolicy](https://technet.microsoft.com/library/hh770421) cmdlet.</span></span> <span data-ttu-id="b9e06-233">Isso também gerará uma solicitação de confirmação.</span><span class="sxs-lookup"><span data-stu-id="b9e06-233">This will also ask for confirmation.</span></span> <span data-ttu-id="b9e06-234">Para ignorar a confirmação, use o sinalizador ```-Confirm:$false``` com o cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b9e06-234">To skip the confirmation use the ```-Confirm:$false``` flag with the cmdlet.</span></span>

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

<span data-ttu-id="b9e06-235">Você pode exibir os detalhes da política de backup existente usando o cmdlet [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) .</span><span class="sxs-lookup"><span data-stu-id="b9e06-235">You can view the details of the existing backup policy using the [Get-OBPolicy](https://technet.microsoft.com/library/hh770406) cmdlet.</span></span> <span data-ttu-id="b9e06-236">Você pode detalhar mais usando o cmdlet [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) para o agendamento de backup e o cmdlet [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) para as políticas de retenção</span><span class="sxs-lookup"><span data-stu-id="b9e06-236">You can drill-down further using the [Get-OBSchedule](https://technet.microsoft.com/library/hh770423) cmdlet for the backup schedule and the [Get-OBRetentionPolicy](https://technet.microsoft.com/library/hh770427) cmdlet for the retention policies</span></span>

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

### <a name="performing-an-ad-hoc-backup"></a><span data-ttu-id="b9e06-237">Executando um backup ad hoc</span><span class="sxs-lookup"><span data-stu-id="b9e06-237">Performing an ad-hoc backup</span></span>
<span data-ttu-id="b9e06-238">Depois de definir uma política de backup, os backups ocorrerão de acordo com o agendamento.</span><span class="sxs-lookup"><span data-stu-id="b9e06-238">Once a backup policy has been set the backups will occur per the schedule.</span></span> <span data-ttu-id="b9e06-239">Disparar um backup ad hoc também é possível usando o cmdlet [Start-OBBackup](https://technet.microsoft.com/library/hh770426) :</span><span class="sxs-lookup"><span data-stu-id="b9e06-239">Triggering an ad-hoc backup is also possible using the [Start-OBBackup](https://technet.microsoft.com/library/hh770426) cmdlet:</span></span>

```
PS C:> Get-OBPolicy | Start-OBBackup
Taking snapshot of volumes...
Preparing storage...
Estimating size of backup items...
Estimating size of backup items...
Transferring data...
Verifying backup...
Job completed.
The backup operation completed successfully.
```

## <a name="restore-data-from-azure-backup"></a><span data-ttu-id="b9e06-240">Restaurar dados por meio do Backup do Azure</span><span class="sxs-lookup"><span data-stu-id="b9e06-240">Restore data from Azure Backup</span></span>
<span data-ttu-id="b9e06-241">Esta seção o orientará pelas etapas para automatizar a recuperação de dados por meio do Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9e06-241">This section will guide you through the steps for automating recovery of data from Azure Backup.</span></span> <span data-ttu-id="b9e06-242">Isso envolve as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="b9e06-242">Doing so involves the following steps:</span></span>

1. <span data-ttu-id="b9e06-243">Selecionar o volume de origem</span><span class="sxs-lookup"><span data-stu-id="b9e06-243">Pick the source volume</span></span>
2. <span data-ttu-id="b9e06-244">Escolher um ponto de backup para restaurar</span><span class="sxs-lookup"><span data-stu-id="b9e06-244">Choose a backup point to restore</span></span>
3. <span data-ttu-id="b9e06-245">Escolha um item para restaurar</span><span class="sxs-lookup"><span data-stu-id="b9e06-245">Choose an item to restore</span></span>
4. <span data-ttu-id="b9e06-246">Disparar o processo de restauração</span><span class="sxs-lookup"><span data-stu-id="b9e06-246">Trigger the restore process</span></span>

### <a name="picking-the-source-volume"></a><span data-ttu-id="b9e06-247">Selecionar o volume de fonte</span><span class="sxs-lookup"><span data-stu-id="b9e06-247">Picking the source volume</span></span>
<span data-ttu-id="b9e06-248">Para restaurar um item por meio do Backup do Azure, é necessário primeiro identificar a fonte do item.</span><span class="sxs-lookup"><span data-stu-id="b9e06-248">In order to restore an item from Azure Backup, you first need to identify the source of the item.</span></span> <span data-ttu-id="b9e06-249">Como estamos executando os comandos no contexto de um Windows Server ou um cliente Windows, o computador já foi identificado.</span><span class="sxs-lookup"><span data-stu-id="b9e06-249">Since we're executing the commands in the context of a Windows Server or a Windows client, the machine is already identified.</span></span> <span data-ttu-id="b9e06-250">A próxima etapa para identificação da origem é identificar o volume que a contém.</span><span class="sxs-lookup"><span data-stu-id="b9e06-250">The next step in identifying the source is to identify the volume containing it.</span></span> <span data-ttu-id="b9e06-251">É possível recuperar uma lista de volumes ou fontes cujo backup está sendo executado neste computador pela execução do cmdlet [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) .</span><span class="sxs-lookup"><span data-stu-id="b9e06-251">A list of volumes or sources being backed up from this machine can be retrieved by executing the [Get-OBRecoverableSource](https://technet.microsoft.com/library/hh770410) cmdlet.</span></span> <span data-ttu-id="b9e06-252">Esse comando retorna uma matriz de todas as fontes desse servidor/cliente cujo backup foi executado.</span><span class="sxs-lookup"><span data-stu-id="b9e06-252">This command returns an array of all the sources backed up from this server/client.</span></span>

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

### <a name="choosing-a-backup-point-to-restore"></a><span data-ttu-id="b9e06-253">Escolhendo um ponto de backup para restaurar</span><span class="sxs-lookup"><span data-stu-id="b9e06-253">Choosing a backup point to restore</span></span>
<span data-ttu-id="b9e06-254">A lista de pontos de backup pode ser recuperada executando o cmdlet [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) com os parâmetros apropriados.</span><span class="sxs-lookup"><span data-stu-id="b9e06-254">The list of backup points can be retrieved by executing the [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet with appropriate parameters.</span></span> <span data-ttu-id="b9e06-255">Em nosso exemplo, escolheremos o último ponto de backup para o volume de fonte *D:* e o usaremos para recuperar um arquivo específico.</span><span class="sxs-lookup"><span data-stu-id="b9e06-255">In our example, we’ll choose the latest backup point for the source volume *D:* and use it to recover a specific file.</span></span>

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
<span data-ttu-id="b9e06-256">O objeto ```$rps``` é uma matriz de pontos de backup.</span><span class="sxs-lookup"><span data-stu-id="b9e06-256">The object ```$rps``` is an array of backup points.</span></span> <span data-ttu-id="b9e06-257">O primeiro elemento é o ponto mais recente e o enésimo elemento é o ponto mais antigo.</span><span class="sxs-lookup"><span data-stu-id="b9e06-257">The first element is the latest point and the Nth element is the oldest point.</span></span> <span data-ttu-id="b9e06-258">Para escolher o último ponto, usaremos ```$rps[0]```.</span><span class="sxs-lookup"><span data-stu-id="b9e06-258">To choose the latest point, we will use ```$rps[0]```.</span></span>

### <a name="choosing-an-item-to-restore"></a><span data-ttu-id="b9e06-259">Escolhendo um item para restaurar</span><span class="sxs-lookup"><span data-stu-id="b9e06-259">Choosing an item to restore</span></span>
<span data-ttu-id="b9e06-260">Para identificar o arquivo ou pasta exato a ser restaurado, use recursivamente o cmdlet [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) .</span><span class="sxs-lookup"><span data-stu-id="b9e06-260">To identify the exact file or folder to restore, recursively use the [Get-OBRecoverableItem](https://technet.microsoft.com/library/hh770399.aspx) cmdlet.</span></span> <span data-ttu-id="b9e06-261">Desse modo, a hierarquia de pastas pode ser pesquisada usando somente o ```Get-OBRecoverableItem```.</span><span class="sxs-lookup"><span data-stu-id="b9e06-261">That way the folder hierarchy can be browsed solely using the ```Get-OBRecoverableItem```.</span></span>

<span data-ttu-id="b9e06-262">Neste exemplo, se quisermos restaurar o arquivo *finances.xls*, poderemos fazer referência a ele usando o objeto ```$filesFolders[1]```.</span><span class="sxs-lookup"><span data-stu-id="b9e06-262">In this example, if we want to restore the file *finances.xls* we can reference that using the object ```$filesFolders[1]```.</span></span>

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

<span data-ttu-id="b9e06-263">Você também pode procurar itens a serem restaurados usando o cmdlet ```Get-OBRecoverableItem``` .</span><span class="sxs-lookup"><span data-stu-id="b9e06-263">You can also search for items to restore using the ```Get-OBRecoverableItem``` cmdlet.</span></span> <span data-ttu-id="b9e06-264">Em nosso exemplo, para procurar *finances.xls* , poderíamos obter um identificador no arquivo executando esse comando:</span><span class="sxs-lookup"><span data-stu-id="b9e06-264">In our example, to search for *finances.xls* we could get a handle on the file by running this command:</span></span>

```
PS C:\> $item = Get-OBRecoverableItem -RecoveryPoint $rps[0] -Location "D:\MyData" -SearchString "finance*"
```

### <a name="triggering-the-restore-process"></a><span data-ttu-id="b9e06-265">Disparando o processo de restauração</span><span class="sxs-lookup"><span data-stu-id="b9e06-265">Triggering the restore process</span></span>
<span data-ttu-id="b9e06-266">Para disparar o processo de restauração, primeiro precisamos especificar as opções de recuperação.</span><span class="sxs-lookup"><span data-stu-id="b9e06-266">To trigger the restore process, we first need to specify the recovery options.</span></span> <span data-ttu-id="b9e06-267">Isso pode ser feito usando o cmdlet [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) .</span><span class="sxs-lookup"><span data-stu-id="b9e06-267">This can be done by using the [New-OBRecoveryOption](https://technet.microsoft.com/library/hh770417.aspx) cmdlet.</span></span> <span data-ttu-id="b9e06-268">Para este exemplo, iremos supor que queremos restaurar os arquivos para *C:\temp*.</span><span class="sxs-lookup"><span data-stu-id="b9e06-268">For this example, let's assume that we want to restore the files to *C:\temp*.</span></span> <span data-ttu-id="b9e06-269">Iremos supor também que queremos ignorar os arquivos que já existem na pasta de destino *C:\temp*.</span><span class="sxs-lookup"><span data-stu-id="b9e06-269">Let's also assume that we want to skip files that already exist on the destination folder *C:\temp*.</span></span> <span data-ttu-id="b9e06-270">Para criar uma opção de recuperação desse tipo, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="b9e06-270">To create such a recovery option, use the following command:</span></span>

```
PS C:\> $recovery_option = New-OBRecoveryOption -DestinationPath "C:\temp" -OverwriteType Skip
```

<span data-ttu-id="b9e06-271">Agora dispare a restauração usando o comando [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) no ```$item``` selecionado na saída do cmdlet ```Get-OBRecoverableItem```:</span><span class="sxs-lookup"><span data-stu-id="b9e06-271">Now trigger restore by using the [Start-OBRecovery](https://technet.microsoft.com/library/hh770402.aspx) command on the selected ```$item``` from the output of the ```Get-OBRecoverableItem``` cmdlet:</span></span>

```
PS C:\> Start-OBRecovery -RecoverableItem $item -RecoveryOption $recover_option
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Estimating size of backup items...
Job completed.
The recovery operation completed successfully.
```


## <a name="uninstalling-the-azure-backup-agent"></a><span data-ttu-id="b9e06-272">Desinstalando o agente de Backup do Azure</span><span class="sxs-lookup"><span data-stu-id="b9e06-272">Uninstalling the Azure Backup agent</span></span>
<span data-ttu-id="b9e06-273">A desinstalação do agente de Backup do Azure pode ser feita usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="b9e06-273">Uninstalling the Azure Backup agent can be done by using the following command:</span></span>

```
PS C:\> .\MARSAgentInstaller.exe /d /q
```

<span data-ttu-id="b9e06-274">Antes de desinstalar os binários do agente do computador, é necessário considerar algumas consequências:</span><span class="sxs-lookup"><span data-stu-id="b9e06-274">Uninstalling the agent binaries from the machine has some consequences to consider:</span></span>

* <span data-ttu-id="b9e06-275">A desinstalação remove o filtro de arquivo do computador e interrompe o acompanhamento de alterações.</span><span class="sxs-lookup"><span data-stu-id="b9e06-275">It removes the file-filter from the machine, and tracking of changes is stopped.</span></span>
* <span data-ttu-id="b9e06-276">Todas as informações de política são removidas do computador, mas as informações de política continuam sendo armazenadas no serviço.</span><span class="sxs-lookup"><span data-stu-id="b9e06-276">All policy information is removed from the machine, but the policy information continues to be stored in the service.</span></span>
* <span data-ttu-id="b9e06-277">Todos os agendamentos de backup são removidos e nenhum backup posterior é realizado.</span><span class="sxs-lookup"><span data-stu-id="b9e06-277">All backup schedules are removed, and no further backups are taken.</span></span>

<span data-ttu-id="b9e06-278">No entanto, os dados armazenados no Azure permanecem e são mantidos de acordo com a política de retenção configurada por você.</span><span class="sxs-lookup"><span data-stu-id="b9e06-278">However, the data stored in Azure remains and is retained as per the retention policy setup by you.</span></span> <span data-ttu-id="b9e06-279">Os pontos mais antigos são desatualizados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b9e06-279">Older points are automatically aged out.</span></span>

## <a name="remote-management"></a><span data-ttu-id="b9e06-280">Gerenciamento remoto</span><span class="sxs-lookup"><span data-stu-id="b9e06-280">Remote management</span></span>
<span data-ttu-id="b9e06-281">Todo o gerenciamento relacionado ao agente, às políticas e às fontes de dados do Backup do Azure pode ser feito remotamente por meio do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b9e06-281">All the management around the Azure Backup agent, policies, and data sources can be done remotely through PowerShell.</span></span> <span data-ttu-id="b9e06-282">A máquina que será gerenciada remotamente precisa ser preparada corretamente.</span><span class="sxs-lookup"><span data-stu-id="b9e06-282">The machine that will be managed remotely needs to be prepared correctly.</span></span>

<span data-ttu-id="b9e06-283">Por padrão, o serviço WinRM é configurado para inicialização manual.</span><span class="sxs-lookup"><span data-stu-id="b9e06-283">By default, the WinRM service is configured for manual startup.</span></span> <span data-ttu-id="b9e06-284">O tipo de inicialização deve ser definido como *Automático* e o serviço deve ser iniciado.</span><span class="sxs-lookup"><span data-stu-id="b9e06-284">The startup type must be set to *Automatic* and the service should be started.</span></span> <span data-ttu-id="b9e06-285">Para verificar se o serviço WinRM está em execução, o valor da propriedade Status deve ser *Em execução*.</span><span class="sxs-lookup"><span data-stu-id="b9e06-285">To verify that the WinRM service is running, the value of the Status property should be *Running*.</span></span>

```
PS C:\> Get-Service WinRM

Status   Name               DisplayName
------   ----               -----------
Running  winrm              Windows Remote Management (WS-Manag...
```

<span data-ttu-id="b9e06-286">O PowerShell deve ser configurado remotamente.</span><span class="sxs-lookup"><span data-stu-id="b9e06-286">PowerShell should be configured for remoting.</span></span>

```
PS C:\> Enable-PSRemoting -force
WinRM is already set up to receive requests on this computer.
WinRM has been updated for remote management.
WinRM firewall exception enabled.

PS C:\> Set-ExecutionPolicy unrestricted -force
```

<span data-ttu-id="b9e06-287">O computador agora pode ser gerenciado remotamente - começando na instalação do agente.</span><span class="sxs-lookup"><span data-stu-id="b9e06-287">The machine can now be managed remotely - starting from the installation of the agent.</span></span> <span data-ttu-id="b9e06-288">Por exemplo, o script a seguir copia o agente para o computador remoto e o instala.</span><span class="sxs-lookup"><span data-stu-id="b9e06-288">For example, the following script copies the agent to the remote machine and installs it.</span></span>

```
PS C:\> $dloc = "\\REMOTESERVER01\c$\Windows\Temp"
PS C:\> $agent = "\\REMOTESERVER01\c$\Windows\Temp\MARSAgentInstaller.exe"
PS C:\> $args = "/q"
PS C:\> Copy-Item "C:\Downloads\MARSAgentInstaller.exe" -Destination $dloc - force

PS C:\> $s = New-PSSession -ComputerName REMOTESERVER01
PS C:\> Invoke-Command -Session $s -Script { param($d, $a) Start-Process -FilePath $d $a -Wait } -ArgumentList $agent $args
```

## <a name="next-steps"></a><span data-ttu-id="b9e06-289">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b9e06-289">Next steps</span></span>
<span data-ttu-id="b9e06-290">Para obter mais informações sobre o Backup do Azure para Windows Server/Client, consulte</span><span class="sxs-lookup"><span data-stu-id="b9e06-290">For more information about Azure Backup for Windows Server/Client see</span></span>

* [<span data-ttu-id="b9e06-291">Introdução ao Backup do Azure</span><span class="sxs-lookup"><span data-stu-id="b9e06-291">Introduction to Azure Backup</span></span>](backup-introduction-to-azure-backup.md)
* [<span data-ttu-id="b9e06-292">Fazer backup de servidores Windows</span><span class="sxs-lookup"><span data-stu-id="b9e06-292">Back up Windows Servers</span></span>](backup-configure-vault.md)
