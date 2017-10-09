---
title: aaaSet o acesso do WinRM para uma VM do Azure | Microsoft Docs
description: "Configurar o acesso do WinRM para uso com uma máquina virtual do Azure criada no modelo de implantação do Gerenciador de recursos de saudação."
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 9718e85b-d360-4621-90b8-0b0b84a21208
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/16/2016
ms.author: kasing
ms.openlocfilehash: 23d1d3a3065cbd8e4036be085c6d835cae36caae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-winrm-access-for-virtual-machines-in-azure-resource-manager"></a>Configurando o acesso do WinRM para as máquinas virtuais no Azure Resource Manager
## <a name="winrm-in-azure-service-management-vs-azure-resource-manager"></a>WinRM no Gerenciamento de Serviços do Azure vs. Azure Resource Manager

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

* Para obter uma visão geral de saudação do Azure Resource Manager, consulte esta [artigo](../../azure-resource-manager/resource-group-overview.md)
* Para encontrar as diferenças entre o Gerenciamento de Serviços do Azure e o Azure Resource Manager, consulte este [artigo](../../resource-manager-deployment-model.md)

Olá chave diferença na configuração de WinRM entre duas pilhas de saudação é como certificado Olá obtém instalado no hello VM. Na pilha do Gerenciador de recursos do Azure hello, certificados de saudação são modelados como recursos gerenciados pelo provedor de recursos do Cofre de chave de saudação. Portanto, o usuário Olá precisa tooprovide seu próprio certificado e carregá-lo tooa Cofre de chaves antes de usá-lo em uma VM.

Aqui estão as etapas de saudação necessário tooset tootake backup de uma VM com conectividade do WinRM

1. Criar um cofre de chaves
2. Crie um certificado autoassinado
3. Carregar tooKey seu certificado autoassinado cofre
4. Obter URL de saudação de seu certificado autoassinado no hello Cofre de chaves
5. Referenciar a URL de seus certificados autoassinados ao criar uma VM

## <a name="step-1-create-a-key-vault"></a>Etapa 1: Criar um cofre de chaves
Você pode usar o hello abaixo saudação do comando toocreate Cofre de chaves

```
New-AzureRmKeyVault -VaultName "<vault-name>" -ResourceGroupName "<rg-name>" -Location "<vault-location>" -EnabledForDeployment -EnabledForTemplateDeployment
```

## <a name="step-2-create-a-self-signed-certificate"></a>Etapa 2: Criar um certificado autoassinado
Você pode criar um certificado autoassinado usando esse script do PowerShell

```
$certificateName = "somename"

$thumbprint = (New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation Cert:\CurrentUser\My -KeySpec KeyExchange).Thumbprint

$cert = (Get-ChildItem -Path cert:\CurrentUser\My\$thumbprint)

$password = Read-Host -Prompt "Please enter hello certificate password." -AsSecureString

Export-PfxCertificate -Cert $cert -FilePath ".\$certificateName.pfx" -Password $password
```

## <a name="step-3-upload-your-self-signed-certificate-toohello-key-vault"></a>Etapa 3: Carregar toohello seu certificado autoassinado Cofre de chaves
Antes de carregar Olá certificado toohello Cofre de chaves criado na etapa 1, ele precisa tooconverted em uma saudação do formato Microsoft. Compute compreenda o provedor de recursos. Olá script do PowerShell abaixo permitirá a que você fazer isso

```
$fileName = "<Path toohello .pfx file>"
$fileContentBytes = Get-Content $fileName -Encoding Byte
$fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

$jsonObject = @"
{
  "data": "$filecontentencoded",
  "dataType" :"pfx",
  "password": "<password>"
}
"@

$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText –Force
Set-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>" -SecretValue $secret
```

## <a name="step-4-get-hello-url-for-your-self-signed-certificate-in-hello-key-vault"></a>Etapa 4: Obter a URL de saudação de seu certificado autoassinado no hello Cofre de chaves
provedor de recursos Microsoft. Compute Olá precisa de um segredo de toohello URL dentro de saudação Cofre de chaves durante o provisionamento Olá VM. Isso habilita o segredo de Olá Olá Microsoft. Compute recurso provedor toodownload e criar certificado equivalente Olá em Olá VM.

> [!NOTE]
> URL de saudação do segredo Olá precisa tooinclude Olá versão também. Uma URL de exemplo tem a aparência abaixo https://contosovault.vault.azure.net:443/secrets/contososecret/01h9db0df2cd4300a20ence585a6s7ve
> 
> 

#### <a name="templates"></a>Modelos
Você pode obter Olá link toohello URL no modelo Olá Olá código abaixo

    "certificateUrl": "[reference(resourceId(resourceGroup().name, 'Microsoft.KeyVault/vaults/secrets', '<vault-name>', '<secret-name>'), '2015-06-01').secretUriWithVersion]"

#### <a name="powershell"></a>PowerShell
Você pode obter essa URL usando Olá abaixo de comando do PowerShell

    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id

## <a name="step-5-reference-your-self-signed-certificates-url-while-creating-a-vm"></a>Etapa 5: Referenciar a URL de seus certificados autoassinados ao criar uma VM
#### <a name="azure-resource-manager-templates"></a>Modelos do Azure Resource Manager
Ao criar uma VM por meio de modelos, certificado Olá obtém referenciado nos Olá segredos seção e Olá winRM como abaixo:

    "osProfile": {
          ...
          "secrets": [
            {
              "sourceVault": {
                "id": "<resource id of hello Key Vault containing hello secret>"
              },
              "vaultCertificates": [
                {
                  "certificateUrl": "<URL for hello certificate you got in Step 4>",
                  "certificateStore": "<Name of hello certificate store on hello VM>"
                }
              ]
            }
          ],
          "windowsConfiguration": {
            ...
            "winRM": {
              "listeners": [
                {
                  "protocol": "http"
                },
                {
                  "protocol": "https",
                  "certificateUrl": "<URL for hello certificate you got in Step 4>"
                }
              ]
            },
            ...
          }
        },

Um modelo de exemplo hello acima pode ser encontrado aqui em [201 vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)

O código-fonte para este modelo pode ser encontrado no [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)

#### <a name="powershell"></a>PowerShell
    $vm = New-AzureRmVMConfig -VMName "<VM name>" -VMSize "<VM Size>"
    $credential = Get-Credential
    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName "<Computer Name>" -Credential $credential -WinRMHttp -WinRMHttps -WinRMCertificateUrl $secretURL
    $sourceVaultId = (Get-AzureRmKeyVault -ResourceGroupName "<Resource Group name>" -VaultName "<Vault Name>").ResourceId
    $CertificateStore = "My"
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore $CertificateStore -CertificateUrl $secretURL

## <a name="step-6-connecting-toohello-vm"></a>Etapa 6: Conectando toohello VM
Antes de poder conectar toohello VM precisará toomake se que seu computador está configurado para gerenciamento remoto do WinRM. Inicie o PowerShell como administrador e execute Olá abaixo comando toomake-se de que configurá-lo.

    Enable-PSRemoting -Force

> [!NOTE]
> Talvez seja necessário toomake se Olá serviço WinRM está em execução se Olá acima não funcionará. Você pode fazer isso usando `Get-Service WinRM`
> 
> 

Depois da instalação hello, você pode se conectar toohello VM usando Olá comando abaixo

    Enter-PSSession -ConnectionUri https://<public-ip-dns-of-the-vm>:5986 -Credential $cred -SessionOption (New-PSSessionOption -SkipCACheck -SkipCNCheck -SkipRevocationCheck) -Authentication Negotiate
