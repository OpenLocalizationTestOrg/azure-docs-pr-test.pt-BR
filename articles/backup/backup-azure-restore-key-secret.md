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
# <a name="restore-key-vault-key-and-secret-for-encrypted-vms-using-azure-backup"></a>Restaurar chave e segredo do Cofre de Chaves para VMs criptografadas usando o Backup do Azure
Este artigo trata usando a restauração do Backup de VM do Azure tooperform das VMs do Azure criptografados, se sua chave e o segredo não existem no cofre de chaves de saudação. Essas etapas também podem ser usadas se você quiser toomaintain uma cópia separada da chave (chave de criptografia) e segredo (chave de criptografia do BitLocker) para Olá restaurado VM.

## <a name="prerequisites"></a>Pré-requisitos
* **Backup de VMs criptografadas** – o backup de VMs do Azure criptografadas foi feito usando o Backup do Azure. Consulte o artigo Olá [gerenciar backup e restauração de máquinas virtuais do Azure usando o PowerShell](backup-azure-vms-automation.md) para obter detalhes sobre como toobackup criptografada VMs do Azure.
* **Configurar o Azure Key Vault** – Verifique se o Cofre de chaves toowhich chaves e segredos necessidade toobe restaurado já está presente. Consulte o artigo Olá [Introdução ao Azure Key Vault](../key-vault/key-vault-get-started.md) para obter detalhes sobre o gerenciamento de chave de cofre.
* **Restaurar o disco** – verifique se você disparou o trabalho de restauração para restaurar discos da VM criptografada usando as [etapas do PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm). Isso ocorre porque esse trabalho gera um arquivo JSON em sua conta de armazenamento que contém chaves e segredos para Olá criptografado VM toobe restaurado.

## <a name="get-key-and-secret-from-azure-backup"></a>Obter a chave e o segredo do Backup do Azure

> [!NOTE]
> Depois que o disco tiver sido restaurado Olá criptografados VM, certifique-se de que:
> 1. $details é populada com detalhes do trabalho de disco de restauração, conforme mencionado em [PowerShell as etapas na seção de discos de saudação de restauração](backup-azure-vms-automation.md#restore-an-azure-vm)
> 2. VM deve ser criada de discos restaurados somente **após a chave e o segredo do cofre restaurado tookey**.
>
>

Saudação de consulta restaurado propriedades do disco para obter detalhes do trabalho hello.

```
PS C:\> $properties = $details.properties
PS C:\> $storageAccountName = $properties["Target Storage Account Name"]
PS C:\> $containerName = $properties["Config Blob Container Name"]
PS C:\> $encryptedBlobName = $properties["Encryption Info Blob Name"]
```

Definir contexto do armazenamento do Azure hello e restaurar o arquivo de configuração JSON que contém a chave e os detalhes de segredo para VM criptografado.

```
PS C:\> Set-AzureRmCurrentStorageAccount -Name $storageaccountname -ResourceGroupName '<rg-name>'
PS C:\> $destination_path = 'C:\vmencryption_config.json'
PS C:\> Get-AzureStorageBlobContent -Blob $encryptedBlobName -Container $containerName -Destination $destination_path
PS C:\> $encryptionObject = Get-Content -Path $destination_path  | ConvertFrom-Json
```

## <a name="restore-key"></a>Restaurar chave
Depois que o arquivo JSON de saudação é gerado no caminho de destino Olá mencionado acima, gerar arquivo de blob da chave de saudação JSON e alimente-toorestore (KEK) de chave de saudação cmdlet chave tooput no cofre de chaves de saudação.

```
PS C:\> $keyDestination = 'C:\keyDetails.blob'
PS C:\> [io.file]::WriteAllBytes($keyDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyBackupData))
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile $keyDestination
```

## <a name="restore-secret"></a>Restaurar segredo
Usar arquivo de JSON de saudação gerado acima do valor e nome do segredo tooget e alimente-segredo de saudação do tooset cmdlet secreta tooput (BEK) no cofre de chaves de saudação. **Use esses cmdlets se sua VM for criptografada usando BEK e KEK.**

```
PS C:\> $secretdata = $encryptionObject.OsDiskKeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = $encryptionObject.OsDiskKeyAndSecretDetails.KeyUrl;'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $Secret -ContentType  'Wrapped BEK' -Tags $Tags
```

Se sua VM for **criptografado usando apenas o BEK**, gerar arquivo de blob secreta de saudação JSON e alimente-segredo de saudação do toorestore cmdlet secreta tooput (BEK) no cofre de chaves de saudação.

```
PS C:\> $secretDestination = 'C:\secret.blob'
PS C:\> [io.file]::WriteAllBytes($secretDestination, [System.Convert]::FromBase64String($encryptionObject.OsDiskKeyAndSecretDetails.KeyVaultSecretBackupData))
PS C:\> Restore-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -InputFile $secretDestination -Verbose
```

> [!NOTE]
> 1. Valor de $secretname pode ser obtido referindo-se a saída de toohello de $encryptionObject.OsDiskKeyAndSecretDetails.SecretUrl e usando o texto depois de segredos / por exemplo, a URL de segredo de saída é https://keyvaultname.vault.azure.net/secrets/ Nome do B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 e o segredo é B3284AAA-DAAA-4AAA-B393-60CAA848AAAA
> 2. Valor da marca de saudação DiskEncryptionKeyFileName é igual ao nome do segredo.
>
>

## <a name="create-virtual-machine-from-restored-disk"></a>Criar uma máquina virtual de um disco restaurado
Se você tiver feito backup criptografado VM usando o Backup de VM do Azure, Olá cmdlets do PowerShell mencionado acima ajuda que você restaurar a chave e o cofre da chave secreta toohello voltar. Depois de restaurá-los, consulte o artigo Olá [gerenciar backup e restauração de máquinas virtuais do Azure usando o PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate criptografado VMs do disco restaurado, a chave e o segredo.

## <a name="legacy-approach"></a>Abordagem herdada
abordagem de saudação mencionada acima funciona para todos os pontos de recuperação de saudação. No entanto, hello abordagem mais antiga da obtenção de chave e informações secretas do ponto de recuperação será válido para pontos de recuperação mais de 11 de julho de 2017 para VMs criptografadas usando BEK e KEK. Após o trabalho de restauração de disco ser concluído para a VM criptografada usando [etapas do PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm), verifique se $rp é populado com um valor válido.

### <a name="restore-key"></a>Restaurar chave
Use Olá segue as informações de chave (KEK) de tooget cmdlets de ponto de recuperação e alimente-toorestore cmdlet chave tooput-los de volta no cofre de chaves de saudação.

```
PS C:\> $rp1 = Get-AzureRmRecoveryServicesBackupRecoveryPoint -RecoveryPointId $rp[0].RecoveryPointId -Item $backupItem -KeyFileDownloadLocation 'C:\Users\downloads'
PS C:\> Restore-AzureKeyVaultKey -VaultName '<target_key_vault_name>' -InputFile 'C:\Users\downloads'
```

### <a name="restore-secret"></a>Restaurar segredo
Use Olá informações de segredo (BEK) tooget cmdlets a seguir de ponto de recuperação e alimente-tooset cmdlet secreta tooput-los de volta no cofre de chaves de saudação.

```
PS C:\> $secretname = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA'
PS C:\> $secretdata = $rp1.KeyAndSecretDetails.SecretData
PS C:\> $Secret = ConvertTo-SecureString -String $secretdata -AsPlainText -Force
PS C:\> $Tags = @{'DiskEncryptionKeyEncryptionAlgorithm' = 'RSA-OAEP';'DiskEncryptionKeyFileName' = 'B3284AAA-DAAA-4AAA-B393-60CAA848AAAA.BEK';'DiskEncryptionKeyEncryptionKeyURL' = 'https://mykeyvault.vault.azure.net:443/keys/KeyName/84daaac999949999030bf99aaa5a9f9';'MachineName' = 'vm-name'}
PS C:\> Set-AzureKeyVaultSecret -VaultName '<target_key_vault_name>' -Name $secretname -SecretValue $secret -Tags $Tags -SecretValue $Secret -ContentType  'Wrapped BEK'
```

> [!NOTE]
> 1. Valor de $secretname pode ser obtido consultando saída toohello de US $rp1. KeyAndSecretDetails.SecretUrl e usando o texto depois de segredos / por exemplo, a URL de segredo de saída é https://keyvaultname.vault.azure.net/secrets/B3284AAA-DAAA-4AAA-B393-60CAA848AAAA/xx000000xx0849999f3xx30000003163 e o nome do segredo é B3284AAA-DAAA-4AAA-B393-60CAA848AAAA
> 2. Valor da marca de saudação DiskEncryptionKeyFileName é igual ao nome do segredo.
> 3. Valor para DiskEncryptionKeyEncryptionKeyURL pode ser obtido do cofre da chave depois de restaurar chaves de saudação novamente e usando [Get-AzureKeyVaultKey](https://msdn.microsoft.com/library/dn868053.aspx) cmdlet
>
>

## <a name="next-steps"></a>Próximas etapas
Depois de restaurar a chave e o segredo tookey back cofre, consulte o artigo Olá [gerenciar backup e restauração de máquinas virtuais do Azure usando o PowerShell](backup-azure-vms-automation.md#create-a-vm-from-restored-disks) toocreate criptografado VMs do disco restaurado, chave e o segredo.
