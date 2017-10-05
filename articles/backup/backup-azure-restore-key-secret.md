---
title: Restaurar chave e segredo do Cofre de Chaves para VMs criptografadas usando o Backup do Azure | Microsoft Docs
description: Saiba como restaurar a chave e o segredo do Cofre de Chaves no Backup do Azure usando o PowerShell
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
ms.openlocfilehash: f2db3449187d655248b13198b268841052570626
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="restore-key-vault-key-and-secret-for-encrypted-vms-using-azure-backup"></a><span data-ttu-id="5eb2a-103">Restaurar chave e segredo do Cofre de Chaves para VMs criptografadas usando o Backup do Azure</span><span class="sxs-lookup"><span data-stu-id="5eb2a-103">Restore Key Vault key and secret for encrypted VMs using Azure Backup</span></span>
<span data-ttu-id="5eb2a-104">Este artigo fala sobre usar o Backup da VM do Azure para executar a restauração de VMs do Azure criptografadas se a chave e o segredo não existirem no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="5eb2a-104">This article talks about using Azure VM Backup to perform restore of encrypted Azure VMs, if your key and secret do not exist in the key vault.</span></span> <span data-ttu-id="5eb2a-105">Essas etapas também poderão ser usadas se vocês quiser manter uma cópia separada da chave (Chave de Criptografia de Chave) e o segredo (Chave de Criptografia do BitLocker) para a VM restaurada.</span><span class="sxs-lookup"><span data-stu-id="5eb2a-105">These steps can also be used if you want to maintain a separate copy of key (Key Encryption Key) and secret (BitLocker Encryption Key) for the restored VM.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5eb2a-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5eb2a-106">Prerequisites</span></span>
* <span data-ttu-id="5eb2a-107">**Backup de VMs criptografadas** – o backup de VMs do Azure criptografadas foi feito usando o Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="5eb2a-107">**Backup encrypted VMs** - Encrypted Azure VMs have been backed up using Azure Backup.</span></span> <span data-ttu-id="5eb2a-108">Consulte o artigo [Gerenciar backup e restauração de VMs do Azure usando o PowerShell](backup-azure-vms-automation.md) para obter detalhes sobre como fazer o backup de VMs do Azure criptografadas.</span><span class="sxs-lookup"><span data-stu-id="5eb2a-108">Refer the article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md) for details about how to backup encrypted Azure VMs.</span></span>
* <span data-ttu-id="5eb2a-109">**Configurar o Cofre de Chaves do Azure** – garanta que o cofre de chaves ao qual as chaves e segredos precisam ser restaurados já esteja presente.</span><span class="sxs-lookup"><span data-stu-id="5eb2a-109">**Configure Azure Key Vault** – Ensure that key vault to which keys and secrets need to be restored is already present.</span></span> <span data-ttu-id="5eb2a-110">Consulte o artigo [Introdução ao Cofre de Chaves do Azure](../key-vault/key-vault-get-started.md) para obter detalhes sobre o gerenciamento do cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="5eb2a-110">Refer the article [Get Started with Azure Key Vault](../key-vault/key-vault-get-started.md) for details about key vault management.</span></span>
* <span data-ttu-id="5eb2a-111">**Restaurar o disco** – verifique se você disparou o trabalho de restauração para restaurar discos da VM criptografada usando as [etapas do PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="5eb2a-111">**Restore disk** - Ensure that you have triggered restore job for restoring disks for encrypted VM using [PowerShell steps](backup-azure-vms-automation.md#restore-an-azure-vm).</span></span> <span data-ttu-id="5eb2a-112">Isso ocorre porque esse trabalho gera um arquivo JSON em sua conta de armazenamento que contém chaves e segredos para a VM criptografada a ser restaurada.</span><span class="sxs-lookup"><span data-stu-id="5eb2a-112">This is because this job generates a JSON file in your storage account containing keys and secrets for the encrypted VM to be restored.</span></span>

## <a name="get-key-and-secret-from-azure-backup"></a><span data-ttu-id="5eb2a-113">Obter a chave e o segredo do Backup do Azure</span><span class="sxs-lookup"><span data-stu-id="5eb2a-113">Get key and secret from Azure Backup</span></span>

> [!NOTE]
> <span data-ttu-id="5eb2a-114">Depois que o disco tiver sido restaurado para a VM criptografada, verifique se:</span><span class="sxs-lookup"><span data-stu-id="5eb2a-114">Once disk has been restored for the encrypted VM, ensure that:</span></span>
> 1. <span data-ttu-id="5eb2a-115">$details está populado com os detalhes do trabalho de restauração de disco, conforme mencionado nas [etapas do PowerShell na seção Restaurar os Discos](backup-azure-vms-automation.md#restore-an-azure-vm)</span><span class="sxs-lookup"><span data-stu-id="5eb2a-115">$details is populated with restore disk job details, as mentioned in [PowerShell steps in Restore the Disks section](backup-azure-vms-automation.md#restore-an-azure-vm)</span></span>
> 2. <span data-ttu-id="5eb2a-116">A VM deve ser criada de discos restaurados somente **após a chave e o segredo serem restaurados para o cofre de chaves**.</span><span class="sxs-lookup"><span data-stu-id="5eb2a-116">VM should be created from restored disks only **after key and secret is restored to key vault**.</span></span>
>
>

<span data-ttu-id="5eb2a-117">Consulte as propriedades do disco restaurado para obter os detalhes do trabalho.</span><span class="sxs-lookup"><span data-stu-id="5eb2a-117">Query the restored disk properties for the job details.</span></span>

```
PS C:\> $properties = $details.properties
PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
PS C:\> $containerName = $properties["Config Blob Container Name"]
PS C:\> $encryptedBlobName = $properties["Encryption Info Blob Name"]
```

<span data-ttu-id="5eb2a-118">Defina o contexto de armazenamento do Azure e restaure o arquivo de configuração JSON que contém a chave e os detalhes de segredo da VM criptografada.</span><span class="sxs-lookup"><span data-stu-id="5eb2a-118">Set the Azure storage context and restore JSON configuration file containing key and secret details for encrypted VM.</span></span>

```
PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName '<rg-name>'
PS C:\> $destination_path = 'C:\vmencryption_config.json'
PS C:\> Get-AzureStorageBlobContent -Blob $encryptedBlobName -Container $containerName -Destination $destination_path
PS C:\> $encryptionObject = Get-Content -Path $destination_path  | ConvertFrom-Json
```

## <a name="restore-key"></a><span data-ttu-id="5eb2a-119">Restaurar chave</span><span class="sxs-lookup"><span data-stu-id="5eb2a-119">Restore key</span></span>
<span data-ttu-id="5eb2a-120">Depois que o arquivo JSON é gerado no caminho de destino mencionado acima, gere o arquivo de blob de chave usando o JSON e insira-o no cmdlet restore key (restaurar chave) para colocar a chave (KEK) de volta no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="5eb2a-120">Once the JSON file is generated in the destination path mentioned above, generate key blob file from the JSON and feed it to restore key cmdlet to put the key (KEK) back in the key vault.</span></span>

```
PS C:\> $keyDestination = 'C:\keyDetails.blob'
PS C:\> [io.file]::WriteAllBytes($keyDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyBackupData))
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile $keyDestination
```

## <a name="restore-secret"></a><span data-ttu-id="5eb2a-121">Restaurar segredo</span><span class="sxs-lookup"><span data-stu-id="5eb2a-121">Restore secret</span></span>
<span data-ttu-id="5eb2a-122">Use o arquivo JSON gerado acima para obter o nome e o valor do segredo e insira-o no cmdlet set secret (definir segredo) para colocar a chave (BEK) de volta no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="5eb2a-122">Use the JSON file generated above to get secret name and value and feed it to set secret cmdlet to put the secret (BEK) back in the key vault.</span></span> <span data-ttu-id="5eb2a-123">**Use esses cmdlets se sua VM for criptografada usando BEK e KEK.**</span><span class="sxs-lookup"><span data-stu-id="5eb2a-123">**Use these cmdlets if your VM is encrypted using BEK and KEK.**</span></span>

```
PS C:\> $secretdata = $encryptionObject.OsDiskKeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = $encryptionObject.OsDiskKeyAndSecretDetails.KeyUrl;'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $Secret -ContentType  'Wrapped BEK' -Tags $Tags
```

<span data-ttu-id="5eb2a-124">Se sua VM foi **criptografado usando apenas BEK**, gere o arquivo de blob do segredo no JSON e alimente-o para restaurar o cmdlet de segredo a fim de colocar o segredo (BEK) de volta no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="5eb2a-124">If your VM is **encrypted using BEK only**, generate secret blob file from the JSON and feed it to restore secret cmdlet to put the secret (BEK) back in the key vault.</span></span>

```
PS C:\> $secretDestination = 'C:\secret.blob'
PS C:\> [io.file]::WriteAllBytes($secretDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyVaultSecretBackupData))
PS C:\> Restore-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -InputFile $secretDestination -Verbose
```

> [!NOTE]
> 1. <span data-ttu-id="5eb2a-125">O valor para $secretname pode ser obtido referindo-se à saída de $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl e usando o texto depois de secrets/, por exemplo, a URL de segredo de saída é https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 e o nome do segredo é B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span><span class="sxs-lookup"><span data-stu-id="5eb2a-125">Value for $secretname can be obtained by referring to the output of $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl and using text after secrets/ e.g. output secret URL is https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 and secret name is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span></span>
> 2. <span data-ttu-id="5eb2a-126">O valor da marca DiskEncryptionKeyFileName é igual ao do nome do segredo.</span><span class="sxs-lookup"><span data-stu-id="5eb2a-126">Value of the tag DiskEncryptionKeyFileName is same as secret name.</span></span>
>
>

## <a name="create-virtual-machine-from-restored-disk"></a><span data-ttu-id="5eb2a-127">Criar uma máquina virtual de um disco restaurado</span><span class="sxs-lookup"><span data-stu-id="5eb2a-127">Create virtual machine from restored disk</span></span>
<span data-ttu-id="5eb2a-128">Se você fez backup da VM criptografada usando o Backup de VM do Azure, os cmdlets do PowerShell mencionados acima ajudarão a restaurar a chave e o segredo de volta no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="5eb2a-128">If you have backed up encrypted VM using Azure VM Backup, the PowerShell cmdlets mentioned above help you restore key and secret back to the key vault.</span></span> <span data-ttu-id="5eb2a-129">Depois de restaurá-los, veja o artigo [Gerenciar backup e restauração de VMs do Azure usando o PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) para criar VMs criptografadas de disco, chave e segredo restaurados.</span><span class="sxs-lookup"><span data-stu-id="5eb2a-129">After restoring them, refer the article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) to create encrypted VMs from restored disk, key, and secret.</span></span>

## <a name="legacy-approach"></a><span data-ttu-id="5eb2a-130">Abordagem herdada</span><span class="sxs-lookup"><span data-stu-id="5eb2a-130">Legacy approach</span></span>
<span data-ttu-id="5eb2a-131">A abordagem mencionada acima funcionaria para todos os pontos de recuperação.</span><span class="sxs-lookup"><span data-stu-id="5eb2a-131">The approach mentioned above would work for all the recovery points.</span></span> <span data-ttu-id="5eb2a-132">No entanto, a abordagem antiga de obter informações de chave e segredo do ponto de recuperação seria válida para pontos de recuperação anteriores a 11 de julho de 2017 para VMs criptografadas usando BEK e KEK.</span><span class="sxs-lookup"><span data-stu-id="5eb2a-132">However, the older approach of getting key and secret information from recovery point, would be valid for recovery points older than July 11, 2017 for VMs encrypted using BEK and KEK.</span></span> <span data-ttu-id="5eb2a-133">Após o trabalho de restauração de disco ser concluído para a VM criptografada usando [etapas do PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm), verifique se $rp é populado com um valor válido.</span><span class="sxs-lookup"><span data-stu-id="5eb2a-133">Once restore disk job is complete for encrypted VM using [PowerShell steps](backup-azure-vms-automation.md#restore-an-azure-vm), ensure that $rp is populated with a valid value.</span></span>

### <a name="restore-key"></a><span data-ttu-id="5eb2a-134">Restaurar chave</span><span class="sxs-lookup"><span data-stu-id="5eb2a-134">Restore key</span></span>
<span data-ttu-id="5eb2a-135">Use os cmdlets a seguir para obter informações de chave (KEK) do ponto de recuperação e insira-as no cmdlet restore key (restaurar chave) para colocá-las de volta no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="5eb2a-135">Use the following cmdlets to get key (KEK) information from recovery point and feed it to restore key cmdlet to put it back in the key vault.</span></span>

```
PS C:\> $rp1 = Get-AzureRmRecoveryServicesBackupRecoveryPoint -RecoveryPointId $rp[0].RecoveryPointId -Item $backupItem -KeyFileDownloadLocation 'C:\Users\downloads'
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile 'C:\Users\downloads'
```

### <a name="restore-secret"></a><span data-ttu-id="5eb2a-136">Restaurar segredo</span><span class="sxs-lookup"><span data-stu-id="5eb2a-136">Restore secret</span></span>
<span data-ttu-id="5eb2a-137">Use os cmdlets a seguir para obter informações de segredo (BEK) do ponto de recuperação e insira-as no cmdlet set secret (definir segredo) para colocá-las de volta no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="5eb2a-137">Use the following cmdlets to get secret (BEK) information from recovery point and feed it to set secret cmdlet to put it back in the key vault.</span></span>

```
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $secretdata = $rp1.KeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = 'https://mykeyvault.vault.azure.net:443/keys/KeyName/84daaac999949999030bf99aaa5a9f9';'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $secret -Tags $Tags -SecretValue $Secret -ContentType  'Wrapped BEK'
```

> [!NOTE]
> 1. <span data-ttu-id="5eb2a-138">O valor para $secretname pode ser obtido referindo-se à saída de $rp1.KeyAndSecretDetails.SecretUrl e usando o texto depois de secrets/, por exemplo, a URL de segredo de saída é https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 e o nome do segredo é B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span><span class="sxs-lookup"><span data-stu-id="5eb2a-138">Value for $secretname can be obtained by referring to the output of $rp1.KeyAndSecretDetails.SecretUrl and using text after secrets/ e.g. output secret URL is https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 and secret name is B3284AAA-DAAA-4AAA-B393-60CAA848AAAA</span></span>
> 2. <span data-ttu-id="5eb2a-139">O valor da marca DiskEncryptionKeyFileName é igual ao do nome do segredo.</span><span class="sxs-lookup"><span data-stu-id="5eb2a-139">Value of the tag DiskEncryptionKeyFileName is same as secret name.</span></span>
> 3. <span data-ttu-id="5eb2a-140">O valor para DiskEncryptionKeyEncryptionKeyURL pode ser obtido do cofre de chaves depois de restaurar as chaves de volta e usar o cmdlet [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx)</span><span class="sxs-lookup"><span data-stu-id="5eb2a-140">Value for DiskEncryptionKeyEncryptionKeyURL can be obtained from key vault after restoring the keys back and using [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) cmdlet</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="5eb2a-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5eb2a-141">Next steps</span></span>
<span data-ttu-id="5eb2a-142">Depois de restaurar a chave e o segredo de volta para o cofre de chaves, consulte o artigo [Gerenciar backup e restauração de VMs do Azure usando o PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) para criar VMs criptografadas com base em disco, chave e segredo restaurados.</span><span class="sxs-lookup"><span data-stu-id="5eb2a-142">After restoring key and secret back to key vault, refer the article [Manage backup and restore of Azure VMs using PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) to create encrypted VMs from restored disk, key and secret.</span></span>
