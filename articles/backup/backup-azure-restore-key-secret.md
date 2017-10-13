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
# <a name="restore-key-vault-key-and-secret-for-encrypted-vms-using-azure-backup"></a>Restaurar chave e segredo do Cofre de Chaves para VMs criptografadas usando o Backup do Azure
Este artigo fala sobre usar o Backup da VM do Azure para executar a restauração de VMs do Azure criptografadas se a chave e o segredo não existirem no cofre de chaves. Essas etapas também poderão ser usadas se vocês quiser manter uma cópia separada da chave (Chave de Criptografia de Chave) e o segredo (Chave de Criptografia do BitLocker) para a VM restaurada.

## <a name="prerequisites"></a>Pré-requisitos
* **Backup de VMs criptografadas** – o backup de VMs do Azure criptografadas foi feito usando o Backup do Azure. Consulte o artigo [Gerenciar backup e restauração de VMs do Azure usando o PowerShell](backup-azure-vms-automation.md) para obter detalhes sobre como fazer o backup de VMs do Azure criptografadas.
* **Configurar o Cofre de Chaves do Azure** – garanta que o cofre de chaves ao qual as chaves e segredos precisam ser restaurados já esteja presente. Consulte o artigo [Introdução ao Cofre de Chaves do Azure](../key-vault/key-vault-get-started.md) para obter detalhes sobre o gerenciamento do cofre de chaves.
* **Restaurar o disco** – verifique se você disparou o trabalho de restauração para restaurar discos da VM criptografada usando as [etapas do PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm). Isso ocorre porque esse trabalho gera um arquivo JSON em sua conta de armazenamento que contém chaves e segredos para a VM criptografada a ser restaurada.

## <a name="get-key-and-secret-from-azure-backup"></a>Obter a chave e o segredo do Backup do Azure

> [!NOTE]
> Depois que o disco tiver sido restaurado para a VM criptografada, verifique se:
> 1. $details está populado com os detalhes do trabalho de restauração de disco, conforme mencionado nas [etapas do PowerShell na seção Restaurar os Discos](backup-azure-vms-automation.md#restore-an-azure-vm)
> 2. A VM deve ser criada de discos restaurados somente **após a chave e o segredo serem restaurados para o cofre de chaves**.
>
>

Consulte as propriedades do disco restaurado para obter os detalhes do trabalho.

```
PS C:\> $properties = $details.properties
PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
PS C:\> $containerName = $properties["Config Blob Container Name"]
PS C:\> $encryptedBlobName = $properties["Encryption Info Blob Name"]
```

Defina o contexto de armazenamento do Azure e restaure o arquivo de configuração JSON que contém a chave e os detalhes de segredo da VM criptografada.

```
PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName '<rg-name>'
PS C:\> $destination_path = 'C:\vmencryption_config.json'
PS C:\> Get-AzureStorageBlobContent -Blob $encryptedBlobName -Container $containerName -Destination $destination_path
PS C:\> $encryptionObject = Get-Content -Path $destination_path  | ConvertFrom-Json
```

## <a name="restore-key"></a>Restaurar chave
Depois que o arquivo JSON é gerado no caminho de destino mencionado acima, gere o arquivo de blob de chave usando o JSON e insira-o no cmdlet restore key (restaurar chave) para colocar a chave (KEK) de volta no cofre de chaves.

```
PS C:\> $keyDestination = 'C:\keyDetails.blob'
PS C:\> [io.file]::WriteAllBytes($keyDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyBackupData))
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile $keyDestination
```

## <a name="restore-secret"></a>Restaurar segredo
Use o arquivo JSON gerado acima para obter o nome e o valor do segredo e insira-o no cmdlet set secret (definir segredo) para colocar a chave (BEK) de volta no cofre de chaves. **Use esses cmdlets se sua VM for criptografada usando BEK e KEK.**

```
PS C:\> $secretdata = $encryptionObject.OsDiskKeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = $encryptionObject.OsDiskKeyAndSecretDetails.KeyUrl;'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $Secret -ContentType  'Wrapped BEK' -Tags $Tags
```

Se sua VM foi **criptografado usando apenas BEK**, gere o arquivo de blob do segredo no JSON e alimente-o para restaurar o cmdlet de segredo a fim de colocar o segredo (BEK) de volta no cofre de chaves.

```
PS C:\> $secretDestination = 'C:\secret.blob'
PS C:\> [io.file]::WriteAllBytes($secretDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyVaultSecretBackupData))
PS C:\> Restore-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -InputFile $secretDestination -Verbose
```

> [!NOTE]
> 1. O valor para $secretname pode ser obtido referindo-se à saída de $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl e usando o texto depois de secrets/, por exemplo, a URL de segredo de saída é https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 e o nome do segredo é B3284AAA-DAAA-4AAA-B393-60CAA848AAAA
> 2. O valor da marca DiskEncryptionKeyFileName é igual ao do nome do segredo.
>
>

## <a name="create-virtual-machine-from-restored-disk"></a>Criar uma máquina virtual de um disco restaurado
Se você fez backup da VM criptografada usando o Backup de VM do Azure, os cmdlets do PowerShell mencionados acima ajudarão a restaurar a chave e o segredo de volta no cofre de chaves. Depois de restaurá-los, veja o artigo [Gerenciar backup e restauração de VMs do Azure usando o PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) para criar VMs criptografadas de disco, chave e segredo restaurados.

## <a name="legacy-approach"></a>Abordagem herdada
A abordagem mencionada acima funcionaria para todos os pontos de recuperação. No entanto, a abordagem antiga de obter informações de chave e segredo do ponto de recuperação seria válida para pontos de recuperação anteriores a 11 de julho de 2017 para VMs criptografadas usando BEK e KEK. Após o trabalho de restauração de disco ser concluído para a VM criptografada usando [etapas do PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm), verifique se $rp é populado com um valor válido.

### <a name="restore-key"></a>Restaurar chave
Use os cmdlets a seguir para obter informações de chave (KEK) do ponto de recuperação e insira-as no cmdlet restore key (restaurar chave) para colocá-las de volta no cofre de chaves.

```
PS C:\> $rp1 = Get-AzureRmRecoveryServicesBackupRecoveryPoint -RecoveryPointId $rp[0].RecoveryPointId -Item $backupItem -KeyFileDownloadLocation 'C:\Users\downloads'
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile 'C:\Users\downloads'
```

### <a name="restore-secret"></a>Restaurar segredo
Use os cmdlets a seguir para obter informações de segredo (BEK) do ponto de recuperação e insira-as no cmdlet set secret (definir segredo) para colocá-las de volta no cofre de chaves.

```
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $secretdata = $rp1.KeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = 'https://mykeyvault.vault.azure.net:443/keys/KeyName/84daaac999949999030bf99aaa5a9f9';'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $secret -Tags $Tags -SecretValue $Secret -ContentType  'Wrapped BEK'
```

> [!NOTE]
> 1. O valor para $secretname pode ser obtido referindo-se à saída de $rp1.KeyAndSecretDetails.SecretUrl e usando o texto depois de secrets/, por exemplo, a URL de segredo de saída é https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 e o nome do segredo é B3284AAA-DAAA-4AAA-B393-60CAA848AAAA
> 2. O valor da marca DiskEncryptionKeyFileName é igual ao do nome do segredo.
> 3. O valor para DiskEncryptionKeyEncryptionKeyURL pode ser obtido do cofre de chaves depois de restaurar as chaves de volta e usar o cmdlet [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx)
>
>

## <a name="next-steps"></a>Próximas etapas
Depois de restaurar a chave e o segredo de volta para o cofre de chaves, consulte o artigo [Gerenciar backup e restauração de VMs do Azure usando o PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) para criar VMs criptografadas com base em disco, chave e segredo restaurados.
