---
title: aaaHPC 2016 de pacote de cluster no Azure | Microsoft Docs
description: Saiba como toodeploy uma 2016 do HPC Pack cluster no Azure
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3dde6a68-e4a6-4054-8b67-d6a90fdc5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/15/2016
ms.author: danlep
ms.openlocfilehash: 9e21ec70c822a783474b96da77ce925940279abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-hpc-pack-2016-cluster-in-azure"></a>Implantar um cluster HPC Pack 2016 no Azure

Siga as etapas de saudação toodeploy este artigo uma [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) cluster em máquinas virtuais do Azure. HPC Pack é a solução de HPC gratuita da Microsoft fundamentada nas tecnologias Microsoft Azure e Windows Server e que dá suporte a uma ampla gama de cargas de trabalho de HPC.

Use uma saudação [modelos do Azure Resource Manager](https://github.com/MsHpcPack/HPCPack2016) toodeploy cluster de HPC Pack 2016 de saudação. Você tem várias opções de topologia de cluster com quantidades diferentes de nós principais do cluster, e com nós de computação Linux ou Windows.

## <a name="prerequisites"></a>Pré-requisitos

### <a name="pfx-certificate"></a>Certificado PFX

Um cluster do Microsoft HPC Pack 2016 requer uma troca de informações pessoais (PFX) certificado toosecure Olá a comunicação entre nós HPC Olá. certificado Olá deve atender aos Olá requisitos a seguir:

* Ele deve ter uma chave privada capaz de fazer a troca das chaves
* O uso da chave inclui a Assinatura Digital e a Codificação de Chave
* O uso avançado de chave inclui a Autenticação de Servidor e a Autenticação de Cliente

Se você ainda não tiver um certificado que atenda a esses requisitos, você pode solicitar o certificado de saudação da autoridade de certificação. Como alternativa, você pode usar o hello comandos toogenerate Olá certificado autoassinado com base no sistema de operacional Olá no qual executar o comando hello e exportar o certificado em formato PFX Olá com chave privada a seguir.

* **Para Windows 10 ou Windows Server 2016**, execute Olá interna **New-SelfSignedCertificate** cmdlet do PowerShell da seguinte maneira:

  ```PowerShell
  New-SelfSignedCertificate -Subject "CN=HPC Pack 2016 Communication" -KeySpec KeyExchange -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2") -CertStoreLocation cert:\CurrentUser\My -KeyExportPolicy Exportable -NotAfter (Get-Date).AddYears(5)
  ```
* **Para sistemas operacionais anteriores ao Windows 10 ou Windows Server 2016**, baixar Olá [gerador de certificado autoassinado](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) de saudação Microsoft Script Center. Extraia o conteúdo e execute Olá comandos em um prompt do PowerShell a seguir:

    ```PowerShell 
    Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
  
    New-SelfSignedCertificateEx -Subject "CN=HPC Pack 2016 Communication" -KeySpec Exchange -KeyUsage "DigitalSignature,KeyEncipherment" -EnhancedKeyUsage "Server Authentication","Client Authentication" -StoreLocation CurrentUser -Exportable -NotAfter (Get-Date).AddYears(5)
    ```

### <a name="upload-certificate-tooan-azure-key-vault"></a>Carregar certificado tooan Cofre de chaves do Azure

Antes de implantar o cluster HPC hello, carregar Olá certificado tooan [Cofre de chaves do Azure](../../key-vault/index.md) como uma saudação segreda e registrar informações para uso durante a implantação de saudação a seguir: **nome do cofre**,  **Grupo de recursos do cofre**, **URL de certificado**, e **impressão digital do certificado**.

Segue uma amostra do PowerShell script tooupload saudação do certificado. Para obter mais informações sobre como carregar um certificado tooan Cofre de chaves do Azure, consulte [Introdução ao Azure Key Vault](../../key-vault/key-vault-get-started.md).

```powershell
#Give hello following values
$VaultName = "mytestvault"
$SecretName = "hpcpfxcert"
$VaultRG = "myresourcegroup"
$location = "westus"
$PfxFile = "c:\Temp\mytest.pfx"
$Password = "yourpfxkeyprotectionpassword"
#Validate hello pfx file
try {
    $pfxCert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList $PfxFile, $Password
}
catch [System.Management.Automation.MethodInvocationException]
{
    throw $_.Exception.InnerException
}
$thumbprint = $pfxCert.Thumbprint
$pfxCert.Dispose()
# Create and encode hello JSON object
$pfxContentBytes = Get-Content $PfxFile -Encoding Byte
$pfxContentEncoded = [System.Convert]::ToBase64String($pfxContentBytes)
$jsonObject = @"
{
"data": "$pfxContentEncoded",
"dataType": "pfx",
"password": "$Password"
}
"@
$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)
#Create an Azure key vault and upload hello certificate as a secret
$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
$rg = Get-AzureRmResourceGroup -Name $VaultRG -Location $location -ErrorAction SilentlyContinue
if($null -eq $rg)
{
    $rg = New-AzureRmResourceGroup -Name $VaultRG -Location $location
}
$hpcKeyVault = New-AzureRmKeyVault -VaultName $VaultName -ResourceGroupName $VaultRG -Location $location -EnabledForDeployment -EnabledForTemplateDeployment
$hpcSecret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secret
"hello following Information will be used in hello deployment template"
"Vault Name             :   $VaultName"
"Vault Resource Group   :   $VaultRG"
"Certificate URL        :   $($hpcSecret.Id)"
"Certificate Thumbprint :   $thumbprint"

```


## <a name="supported-topologies"></a>Topologias com suporte

Escolha uma saudação [modelos do Azure Resource Manager](https://github.com/MsHpcPack/HPCPack2016) toodeploy cluster de HPC Pack 2016 de saudação. A seguir estão as arquiteturas de alto nível das três topologias de cluster com suporte. As topologias de alta disponibilidade incluem vários nós de cabeçalho do cluster.

1. Cluster de alta disponibilidade com o domínio do Active Directory

    ![Cluster de alta disponibilidade no domínio do AD](./media/hpcpack-2016-cluster/haad.png)



2. Cluster de alta disponibilidade sem o domínio do Active Directory

    ![Cluster de alta disponibilidade sem domínio do AD](./media/hpcpack-2016-cluster/hanoad.png)

3. Cluster com um único nó de cabeçalho

   ![Cluster com um único nó principal](./media/hpcpack-2016-cluster/singlehn.png)


## <a name="deploy-a-cluster"></a>Implantar um cluster

cluster de saudação toocreate, escolha um modelo e clique em **implantar tooAzure**. Em Olá [portal do Azure](https://portal.azure.com), especificar parâmetros de modelo hello, conforme descrito em Olá etapas a seguir. Cada modelo cria todos os recursos do Azure, necessários para a infraestrutura de cluster HPC hello. Os recursos incluem uma rede virtual do Azure, um endereço IP público, um balanceador de carga (apenas para um cluster de alta disponibilidade), interfaces de rede, conjuntos de disponibilidade, contas de armazenamento e máquinas virtuais.

### <a name="step-1-select-hello-subscription-location-and-resource-group"></a>Etapa 1: Selecione a assinatura hello, o local e o grupo de recursos

Olá **assinatura** e hello **local** deve ser o mesmo que você especificou quando você carregar seu certificado PFX (consulte pré-requisitos). É recomendável que você crie um **grupo de recursos** para implantação de saudação.

### <a name="step-2-specify-hello-parameter-settings"></a>Etapa 2: Especificar as configurações de parâmetro hello

Digite ou modifique os valores para parâmetros de modelo de saudação. Clique em Olá ícone próximo tooeach parâmetro para obter informações de Ajuda. Consulte também as diretrizes de saudação para [tamanhos VM disponíveis](sizes.md).

Especificar valores hello registradas na Olá pré-requisitos para Olá parâmetros a seguir: **nome do cofre**, **grupo de recursos do cofre**, **URL de certificado**e **Impressão digital do certificado**.

### <a name="step-3-review-legal-terms-and-create"></a>Etapa 3. Examinar os termos legais e criar
Clique em **revisar os termos legais** tooreview termos de saudação. Se você concordar, clique em **compra**e, em seguida, clique em **criar** toostart implantação de saudação.

## <a name="connect-toohello-cluster"></a>Conecte-se o cluster toohello
1. Após a implantação de cluster de HPC Pack hello, vá toohello [portal do Azure](https://portal.azure.com). Clique em **grupos de recursos**e o grupo de recursos Olá localizar quais Olá cluster foi implantado. Você pode encontrar hello máquinas virtuais de nó principal.

    ![Nós de cluster principal no portal de saudação](./media/hpcpack-2016-cluster/clusterhns.png)

2. Clique em um nó principal (em um cluster de alta disponibilidade, clique em qualquer um de nós de cabeçalho Olá). Em **Essentials**, você pode encontrar o endereço IP público de saudação ou nome DNS completo do cluster de saudação.

    ![Configurações de conexão do cluster](./media/hpcpack-2016-cluster/clusterconnect.png)

3. Clique em **conectar** toolog na tooany de nós de cabeçalho hello usando a área de trabalho remota com seu nome de usuário de administrador especificada. Se for cluster Olá implantado em um domínio do Active Directory, o nome de usuário de saudação é do formulário de saudação <privateDomainName> \<adminUsername > (por exemplo, hpc.local\hpcadmin).

## <a name="next-steps"></a>Próximas etapas
* Cluster de tooyour trabalhos de envio. Consulte [enviar trabalhos tooHPC um cluster de HPC Pack no Azure](hpcpack-cluster-submit-jobs.md) e [gerenciar um cluster de HPC Pack 2016 no Azure usando o Active Directory do Azure](hpcpack-cluster-active-directory.md).

