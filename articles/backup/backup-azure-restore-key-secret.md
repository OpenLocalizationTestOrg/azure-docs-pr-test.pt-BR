---
title: "chave de Cofre de chaves aaaRestore e o segredo para criptografado máquinas virtuais usando o Backup do Azure | Microsoft Docs"
description: Saiba como o Cofre de chave toorestore chave e o segredo no Backup do Azure usando o PowerShell
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 45214083-d5fc-4eb3-a367-0239dc59e0f6
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/28/2017
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 659b2f647493ffcc9494caee111c8bd584ef9c7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-key-vault-key-and-secret-for-encrypted-vms-using-azure-backup"></a><span data-ttu-id="2c25b-103">Restaurar chave e segredo do Cofre de Chaves para VMs criptografadas usando o Backup do Azure</span><span class="sxs-lookup"><span data-stu-id="2c25b-103">Restore Key Vault key and secret for encrypted VMs using Azure Backup</span></span>
<span data-ttu-id="2c25b-104">Este artigo trata usando a restauração do Backup de VM do Azure tooperform das VMs do Azure criptografados, se sua chave e o segredo não existem no cofre de chaves de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c25b-104">This article talks about using Azure VM Backup tooperform restore of encrypted Azure VMs, if your key and secret do not exist in hello key vault.</span></span> <span data-ttu-id="2c25b-105">Essas etapas também podem ser usadas se você quiser toomaintain uma cópia separada da chave (chave de criptografia) e segredo (chave de criptografia do BitLocker) para Olá restaurado VM.</span><span class="sxs-lookup"><span data-stu-id="2c25b-105">These steps can also be used if you want toomaintain a separate copy of key (Key Encryption Key) and secret (BitLocker Encryption Key) for hello restored VM.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c25b-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2c25b-106">Prerequisites</span></span>
* <span data-ttu-id="2c25b-107">**Backup de VMs criptografadas** – o backup de VMs do Azure criptografadas foi feito usando o Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="2c25b-107">**Backup encrypted VMs** - Encrypted Azure VMs have been backed up using Azure Backup.</span></span> <span data-ttu-id="2c25b-108">Consulte o artigo Olá [gerenciar backup e restauração de máquinas virtuais do Azure usando o PowerShell](backup-azure-vms-automation.md) para obter detalhes sobre como toobackup criptografada VMs do Azure.</span><span class="sxs-lookup"><span data-stu-id="2c25b-108">Refer hello article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md) for details about how toobackup encrypted Azure VMs.</span></span>
* <span data-ttu-id="2c25b-109">**Configurar o Azure Key Vault** – Verifique se o Cofre de chaves toowhich chaves e segredos necessidade toobe restaurado já está presente.</span><span class="sxs-lookup"><span data-stu-id="2c25b-109">**Configure Azure Key Vault** – Ensure that key vault toowhich keys and secrets need toobe restored is already present.</span></span> <span data-ttu-id="2c25b-110">Consulte o artigo Olá [Introdução ao Azure Key Vault](../key-vault/key-vault-get-started.md) para obter detalhes sobre o gerenciamento de chave de cofre.</span><span class="sxs-lookup"><span data-stu-id="2c25b-110">Refer hello article [Get Started with Azure Key Vault](../key-vault/key-vault-get-started.md) for details about key vault management.</span></span>
* <span data-ttu-id="2c25b-111">**Restaurar o disco** – verifique se você disparou o trabalho de restauração para restaurar discos da VM criptografada usando as [etapas do PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="2c25b-111">**Restore disk** - Ensure that you have triggered restore job for restoring disks for encrypted VM using [PowerShell steps](backup-azure-vms-automation.md#restore-an-azure-vm).</span></span> <span data-ttu-id="2c25b-112">Isso ocorre porque esse trabalho gera um arquivo JSON em sua conta de armazenamento que contém chaves e segredos para Olá criptografado VM toobe restaurado.</span><span class="sxs-lookup"><span data-stu-id="2c25b-112">This is because this job generates a JSON file in your storage account containing keys and secrets for hello encrypted VM toobe restored.</span></span>

## <a name="get-key-and-secret-from-azure-backup"></a><span data-ttu-id="2c25b-113">Obter a chave e o segredo do Backup do Azure</span><span class="sxs-lookup"><span data-stu-id="2c25b-113">Get key and secret from Azure Backup</span></span>

> [!NOTE]
> <span data-ttu-id="2c25b-114">Depois que o disco tiver sido restaurado Olá criptografados VM, certifique-se de que:</span><span class="sxs-lookup"><span data-stu-id="2c25b-114">Once disk has been restored for hello encrypted VM, ensure that:</span></span>
> 1. <span data-ttu-id="2c25b-115">$details é populada com detalhes do trabalho de disco de restauração, conforme mencionado em [PowerShell as etapas na seção de discos de saudação de restauração](backup-azure-vms-automation.md#restore-an-azure-vm)</span><span class="sxs-lookup"><span data-stu-id="2c25b-115">$details is populated with restore disk job details, as mentioned in [PowerShell steps in Restore hello Disks section](backup-azure-vms-automation.md#restore-an-azure-vm)</span></span>
> 2. <span data-ttu-id="2c25b-116">VM deve ser criada de discos restaurados somente **após a chave e o segredo do cofre restaurado tookey**.</span><span class="sxs-lookup"><span data-stu-id="2c25b-116">VM should be created from restored disks only **after key and secret is restored tookey vault**.</span></span>
>
>

<span data-ttu-id="2c25b-117">Saudação de consulta restaurado propriedades do disco para obter detalhes do trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="2c25b-117">Query hello restored disk properties for hello job details.</span></span>

```
PS C:\> $properties = $details.properties
PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
PS C:\> $containerName = $properties["Config Blob Container Name"]
PS C:\> $encryptedBlobName = $properties["Encryption Info Blob Name"]
```

<span data-ttu-id="2c25b-118">Definir contexto do armazenamento do Azure hello e restaurar o arquivo de configuração JSON que contém a chave e os detalhes de segredo para VM criptografado.</span><span class="sxs-lookup"><span data-stu-id="2c25b-118">Set hello Azure storage context and restore JSON configuration file containing key and secret details for encrypted VM.</span></span>

```
PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName '<rg-name>'
PS C:\> $destination_path = 'C:\vmencryption_config.json'
PS C:\> Get-AzureStorageBlobContent -Blob $encryptedBlobName -Container $containerName -Destination $destination_path
PS C:\> $encryptionObject = Get-Content -Path $destination_path  | ConvertFrom-Json
```

## <a name="restore-key"></a><span data-ttu-id="2c25b-119">Restaurar chave</span><span class="sxs-lookup"><span data-stu-id="2c25b-119">Restore key</span></span>
<span data-ttu-id="2c25b-120">Depois que o arquivo JSON de saudação é gerado no caminho de destino Olá mencionado acima, gerar arquivo de blob da chave de saudação JSON e alimente-toorestore (KEK) de chave de saudação cmdlet chave tooput no cofre de chaves de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c25b-120">Once hello JSON file is generated in hello destination path mentioned above, generate key blob file from hello JSON and feed it toorestore key cmdlet tooput hello key (KEK) back in hello key vault.</span></span>

```
PS C:\> $keyDestination = 'C:\keyDetails.blob'
PS C:\> [io.file]::WriteAllBytes($keyDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyBackupData))
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile $keyDestination
```

## <a name="restore-secret"></a><span data-ttu-id="2c25b-121">Restaurar segredo</span><span class="sxs-lookup"><span data-stu-id="2c25b-121">Restore secret</span></span>
<span data-ttu-id="2c25b-122">Usar arquivo de JSON de saudação gerado acima do valor e nome do segredo tooget e alimente-segredo de saudação do tooset cmdlet secreta tooput (BEK) no cofre de chaves de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c25b-122">Use hello JSON file generated above tooget secret name and value and feed it tooset secret cmdlet tooput hello secret (BEK) back in hello key vault.</span></span> <span data-ttu-id="2c25b-123">**Use esses cmdlets se sua VM for criptografada usando BEK e KEK.**</span><span class="sxs-lookup"><span data-stu-id="2c25b-123">**Use these cmdlets if your VM is encrypted using BEK and KEK.**</span></span>

```
PS C:\> $secretdata = $encryptionObject.OsDiskKeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = $encryptionObject.OsDiskKeyAndSecretDetails.KeyUrl;'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $Secret -ContentType  'Wrapped BEK' -Tags $Tags
```

<span data-ttu-id="2c25b-124">Se sua VM for **criptografado usando apenas o BEK**, gerar arquivo de blob secreta de saudação JSON e alimente-segredo de saudação do toorestore cmdlet secreta tooput (BEK) no cofre de chaves de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c25b-124">If your VM is **encrypted using BEK only**, generate secret blob file from hello JSON and feed it toorestore secret cmdlet tooput hello secret (BEK) back in hello key vault.</span></span>

```
PS C:\> $secretDestination = 'C:\secret.blob'
PS C:\> [io.file]::WriteAllBytes($secretDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyVaultSecretBackupData))
PS C:\> Restore-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -InputFile $secretDestination -Verbose
```

> [!NOTE]
> 1. <span data-ttu-id="2c25b-125">Valor de $secretname pode ser obtido referindo-se a saída de toohello de $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl e usando o texto depois de segredos / por exemplo, a URL de segredo de saída é https://keyvaultname.vault.azure.net/secrets/ Nome do B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 e o segredo é B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span><span class="sxs-lookup"><span data-stu-id="2c25b-125">Value for $secretname can be obtained by referring toohello output of $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl and using text after secrets/ e.g. output secret URL is https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 and secret name is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span></span>
> 2. <span data-ttu-id="2c25b-126">Valor da marca de saudação DiskEncryptionKeyFileName é igual ao nome do segredo.</span><span class="sxs-lookup"><span data-stu-id="2c25b-126">Value of hello tag DiskEncryptionKeyFileName is same as secret name.</span></span>
>
>

## <a name="create-virtual-machine-from-restored-disk"></a><span data-ttu-id="2c25b-127">Criar uma máquina virtual de um disco restaurado</span><span class="sxs-lookup"><span data-stu-id="2c25b-127">Create virtual machine from restored disk</span></span>
<span data-ttu-id="2c25b-128">Se você tiver feito backup criptografado VM usando o Backup de VM do Azure, Olá cmdlets do PowerShell mencionado acima ajuda que você restaurar a chave e o cofre da chave secreta toohello voltar.</span><span class="sxs-lookup"><span data-stu-id="2c25b-128">If you have backed up encrypted VM using Azure VM Backup, hello PowerShell cmdlets mentioned above help you restore key and secret back toohello key vault.</span></span> <span data-ttu-id="2c25b-129">Depois de restaurá-los, consulte o artigo Olá [gerenciar backup e restauração de máquinas virtuais do Azure usando o PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate criptografado VMs do disco restaurado, a chave e o segredo.</span><span class="sxs-lookup"><span data-stu-id="2c25b-129">After restoring them, refer hello article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate encrypted VMs from restored disk, key, and secret.</span></span>

## <a name="legacy-approach"></a><span data-ttu-id="2c25b-130">Abordagem herdada</span><span class="sxs-lookup"><span data-stu-id="2c25b-130">Legacy approach</span></span>
<span data-ttu-id="2c25b-131">abordagem de saudação mencionada acima funciona para todos os pontos de recuperação de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c25b-131">hello approach mentioned above would work for all hello recovery points.</span></span> <span data-ttu-id="2c25b-132">No entanto, hello abordagem mais antiga da obtenção de chave e informações secretas do ponto de recuperação será válido para pontos de recuperação mais de 11 de julho de 2017 para VMs criptografadas usando BEK e KEK.</span><span class="sxs-lookup"><span data-stu-id="2c25b-132">However, hello older approach of getting key and secret information from recovery point, would be valid for recovery points older than July 11, 2017 for VMs encrypted using BEK and KEK.</span></span> <span data-ttu-id="2c25b-133">Após o trabalho de restauração de disco ser concluído para a VM criptografada usando [etapas do PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm), verifique se $rp é populado com um valor válido.</span><span class="sxs-lookup"><span data-stu-id="2c25b-133">Once restore disk job is complete for encrypted VM using [PowerShell steps](backup-azure-vms-automation.md#restore-an-azure-vm), ensure that $rp is populated with a valid value.</span></span>

### <a name="restore-key"></a><span data-ttu-id="2c25b-134">Restaurar chave</span><span class="sxs-lookup"><span data-stu-id="2c25b-134">Restore key</span></span>
<span data-ttu-id="2c25b-135">Use Olá segue as informações de chave (KEK) de tooget cmdlets de ponto de recuperação e alimente-toorestore cmdlet chave tooput-los de volta no cofre de chaves de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c25b-135">Use hello following cmdlets tooget key (KEK) information from recovery point and feed it toorestore key cmdlet tooput it back in hello key vault.</span></span>

```
PS C:\> $rp1 = Get-AzureRmRecoveryServicesBackupRecoveryPoint -RecoveryPointId $rp[0].RecoveryPointId -Item $backupItem -KeyFileDownloadLocation 'C:\Users\downloads'
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile 'C:\Users\downloads'
```

### <a name="restore-secret"></a><span data-ttu-id="2c25b-136">Restaurar segredo</span><span class="sxs-lookup"><span data-stu-id="2c25b-136">Restore secret</span></span>
<span data-ttu-id="2c25b-137">Use Olá informações de segredo (BEK) tooget cmdlets a seguir de ponto de recuperação e alimente-tooset cmdlet secreta tooput-los de volta no cofre de chaves de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c25b-137">Use hello following cmdlets tooget secret (BEK) information from recovery point and feed it tooset secret cmdlet tooput it back in hello key vault.</span></span>

```
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $secretdata = $rp1.KeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = 'https://mykeyvault.vault.azure.net:443/keys/KeyName/84daaac999949999030bf99aaa5a9f9';'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $secret -Tags $Tags -SecretValue $Secret -ContentType  'Wrapped BEK'
```

> [!NOTE]
> 1. <span data-ttu-id="2c25b-138">Valor de $secretname pode ser obtido consultando saída toohello de US $rp1. KeyAndSecretDetails.SecretUrl e usando o texto depois de segredos / por exemplo, a URL de segredo de saída é https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 e o nome do segredo é B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span><span class="sxs-lookup"><span data-stu-id="2c25b-138">Value for $secretname can be obtained by referring toohello output of $rp1.KeyAndSecretDetails.SecretUrl and using text after secrets/ e.g. output secret URL is https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 and secret name is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span></span>
> 2. <span data-ttu-id="2c25b-139">Valor da marca de saudação DiskEncryptionKeyFileName é igual ao nome do segredo.</span><span class="sxs-lookup"><span data-stu-id="2c25b-139">Value of hello tag DiskEncryptionKeyFileName is same as secret name.</span></span>
> 3. <span data-ttu-id="2c25b-140">Valor para DiskEncryptionKeyEncryptionKeyURL pode ser obtido do cofre da chave depois de restaurar chaves de saudação novamente e usando [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) cmdlet</span><span class="sxs-lookup"><span data-stu-id="2c25b-140">Value for DiskEncryptionKeyEncryptionKeyURL can be obtained from key vault after restoring hello keys back and using [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) cmdlet</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="2c25b-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2c25b-141">Next steps</span></span>
<span data-ttu-id="2c25b-142">Depois de restaurar a chave e o segredo tookey back cofre, consulte o artigo Olá [gerenciar backup e restauração de máquinas virtuais do Azure usando o PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate criptografado VMs do disco restaurado, chave e o segredo.</span><span class="sxs-lookup"><span data-stu-id="2c25b-142">After restoring key and secret back tookey vault, refer hello article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate encrypted VMs from restored disk, key and secret.</span></span>
