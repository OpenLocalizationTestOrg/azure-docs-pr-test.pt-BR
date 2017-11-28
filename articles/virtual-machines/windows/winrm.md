---
title: Configurar o acesso do WinRM para uma VM do Azure | Microsoft Docs
description: "Configure o acesso do WinRM para uso com uma máquina virtual do Azure criada no modelo de implantação do Resource Manager."
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
ms.openlocfilehash: 2d6533462400bc1d93d0d3b0227769784e2658a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="setting-up-winrm-access-for-virtual-machines-in-azure-resource-manager"></a><span data-ttu-id="7e001-103">Configurando o acesso do WinRM para as máquinas virtuais no Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7e001-103">Setting up WinRM access for Virtual Machines in Azure Resource Manager</span></span>
## <a name="winrm-in-azure-service-management-vs-azure-resource-manager"></a><span data-ttu-id="7e001-104">WinRM no Gerenciamento de Serviços do Azure vs. Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7e001-104">WinRM in Azure Service Management vs Azure Resource Manager</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

* <span data-ttu-id="7e001-105">Para uma visão geral do Azure Resource Manager, veja este [artigo](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="7e001-105">For an overview of the Azure Resource Manager, please see this [article](../../azure-resource-manager/resource-group-overview.md)</span></span>
* <span data-ttu-id="7e001-106">Para encontrar as diferenças entre o Gerenciamento de Serviços do Azure e o Azure Resource Manager, consulte este [artigo](../../resource-manager-deployment-model.md)</span><span class="sxs-lookup"><span data-stu-id="7e001-106">For differences between Azure Service Management and Azure Resource Manager, please see this [article](../../resource-manager-deployment-model.md)</span></span>

<span data-ttu-id="7e001-107">A principal diferença na definição da configuração do WinRM entre as duas pilhas é como o certificado é instalado na VM.</span><span class="sxs-lookup"><span data-stu-id="7e001-107">The key difference in setting up WinRM configuration between the two stacks is how the certificate gets installed on the VM.</span></span> <span data-ttu-id="7e001-108">Na pilha do Azure Resource Manager, os certificados são modelados como recursos gerenciados pelo Provedor de Recursos do Cofre de Chaves.</span><span class="sxs-lookup"><span data-stu-id="7e001-108">In the Azure Resource Manager stack, the certificates are modeled as resources managed by the Key Vault Resource Provider.</span></span> <span data-ttu-id="7e001-109">Portanto, o usuário precisa fornecer seu próprio certificado e carregá-lo em um Cofre de Chaves antes de usá-lo em uma VM.</span><span class="sxs-lookup"><span data-stu-id="7e001-109">Therefore, the user needs to provide their own certificate and upload it to a Key Vault before using it in a VM.</span></span>

<span data-ttu-id="7e001-110">Aqui estão as etapas que você precisa realizar para configurar uma VM com conectividade do WinRM</span><span class="sxs-lookup"><span data-stu-id="7e001-110">Here are the steps you need to take to set up a VM with WinRM connectivity</span></span>

1. <span data-ttu-id="7e001-111">Criar um cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="7e001-111">Create a Key Vault</span></span>
2. <span data-ttu-id="7e001-112">Crie um certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="7e001-112">Create a self-signed certificate</span></span>
3. <span data-ttu-id="7e001-113">Carregar seu certificado autoassinado no Cofre de Chaves</span><span class="sxs-lookup"><span data-stu-id="7e001-113">Upload your self-signed certificate to Key Vault</span></span>
4. <span data-ttu-id="7e001-114">Obtenha a URL para seu certificado autoassinado no Cofre de Chaves</span><span class="sxs-lookup"><span data-stu-id="7e001-114">Get the URL for your self-signed certificate in the Key Vault</span></span>
5. <span data-ttu-id="7e001-115">Referenciar a URL de seus certificados autoassinados ao criar uma VM</span><span class="sxs-lookup"><span data-stu-id="7e001-115">Reference your self-signed certificates URL while creating a VM</span></span>

## <a name="step-1-create-a-key-vault"></a><span data-ttu-id="7e001-116">Etapa 1: Criar um cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="7e001-116">Step 1: Create a Key Vault</span></span>
<span data-ttu-id="7e001-117">Você pode usar o comando abaixo para criar o Cofre de Chaves</span><span class="sxs-lookup"><span data-stu-id="7e001-117">You can use the below command to create the Key Vault</span></span>

```
New-AzureRmKeyVault -VaultName "<vault-name>" -ResourceGroupName "<rg-name>" -Location "<vault-location>" -EnabledForDeployment -EnabledForTemplateDeployment
```

## <a name="step-2-create-a-self-signed-certificate"></a><span data-ttu-id="7e001-118">Etapa 2: Criar um certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="7e001-118">Step 2: Create a self-signed certificate</span></span>
<span data-ttu-id="7e001-119">Você pode criar um certificado autoassinado usando esse script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="7e001-119">You can create a self-signed certificate using this PowerShell script</span></span>

```
$certificateName = "somename"

$thumbprint = (New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation Cert:\CurrentUser\My -KeySpec KeyExchange).Thumbprint

$cert = (Get-ChildItem -Path cert:\CurrentUser\My\$thumbprint)

$password = Read-Host -Prompt "Please enter the certificate password." -AsSecureString

Export-PfxCertificate -Cert $cert -FilePath ".\$certificateName.pfx" -Password $password
```

## <a name="step-3-upload-your-self-signed-certificate-to-the-key-vault"></a><span data-ttu-id="7e001-120">Etapa 3: Carregar seu certificado autoassinado no Cofre de Chaves</span><span class="sxs-lookup"><span data-stu-id="7e001-120">Step 3: Upload your self-signed certificate to the Key Vault</span></span>
<span data-ttu-id="7e001-121">Antes de carregar o certificado para o Cofre de Chaves criado na Etapa 1, ele precisa ser convertido em um formato que o provedor de recursos Microsoft.Compute entenda.</span><span class="sxs-lookup"><span data-stu-id="7e001-121">Before uploading the certificate to the Key Vault created in step 1, it needs to converted into a format the Microsoft.Compute resource provider will understand.</span></span> <span data-ttu-id="7e001-122">O script do PowerShell abaixo permitirá que você faça isso</span><span class="sxs-lookup"><span data-stu-id="7e001-122">The below PowerShell script will allow you do that</span></span>

```
$fileName = "<Path to the .pfx file>"
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

## <a name="step-4-get-the-url-for-your-self-signed-certificate-in-the-key-vault"></a><span data-ttu-id="7e001-123">Etapa 4: Obter a URL para seu certificado autoassinado no Cofre de Chaves</span><span class="sxs-lookup"><span data-stu-id="7e001-123">Step 4: Get the URL for your self-signed certificate in the Key Vault</span></span>
<span data-ttu-id="7e001-124">O provedor de recursos Microsoft.Compute precisa de uma URL para o segredo do Cofre de Chaves ao provisionar a VM.</span><span class="sxs-lookup"><span data-stu-id="7e001-124">The Microsoft.Compute resource provider needs a URL to the secret inside the Key Vault while provisioning the VM.</span></span> <span data-ttu-id="7e001-125">Isso permite que o provedor de recursos Microsoft.Compute baixe o segredo e crie o certificado equivalente na VM.</span><span class="sxs-lookup"><span data-stu-id="7e001-125">This enables the Microsoft.Compute resource provider to download the secret and create the equivalent certificate on the VM.</span></span>

> [!NOTE]
> <span data-ttu-id="7e001-126">A URL do segredo precisa incluir a versão também.</span><span class="sxs-lookup"><span data-stu-id="7e001-126">The URL of the secret needs to include the version as well.</span></span> <span data-ttu-id="7e001-127">Uma URL de exemplo tem a aparência abaixo https://contosovault.vault.azure.net:443/secrets/contososecret/01h9db0df2cd4300a20ence585a6s7ve</span><span class="sxs-lookup"><span data-stu-id="7e001-127">An example URL looks like below https://contosovault.vault.azure.net:443/secrets/contososecret/01h9db0df2cd4300a20ence585a6s7ve</span></span>
> 
> 

#### <a name="templates"></a><span data-ttu-id="7e001-128">Modelos</span><span class="sxs-lookup"><span data-stu-id="7e001-128">Templates</span></span>
<span data-ttu-id="7e001-129">Você pode obter o link para a URL no modelo usando o código abaixo</span><span class="sxs-lookup"><span data-stu-id="7e001-129">You can get the link to the URL in the template using the below code</span></span>

    "certificateUrl": "[reference(resourceId(resourceGroup().name, 'Microsoft.KeyVault/vaults/secrets', '<vault-name>', '<secret-name>'), '2015-06-01').secretUriWithVersion]"

#### <a name="powershell"></a><span data-ttu-id="7e001-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7e001-130">PowerShell</span></span>
<span data-ttu-id="7e001-131">Você pode obter essa URL usando o comando do PowerShell abaixo</span><span class="sxs-lookup"><span data-stu-id="7e001-131">You can get this URL using the below PowerShell command</span></span>

    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id

## <a name="step-5-reference-your-self-signed-certificates-url-while-creating-a-vm"></a><span data-ttu-id="7e001-132">Etapa 5: Referenciar a URL de seus certificados autoassinados ao criar uma VM</span><span class="sxs-lookup"><span data-stu-id="7e001-132">Step 5: Reference your self-signed certificates URL while creating a VM</span></span>
#### <a name="azure-resource-manager-templates"></a><span data-ttu-id="7e001-133">Modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7e001-133">Azure Resource Manager Templates</span></span>
<span data-ttu-id="7e001-134">Ao criar uma VM por meio de modelos, o certificado é referenciado na seção de segredos e na seção winRM como é apresentado abaixo:</span><span class="sxs-lookup"><span data-stu-id="7e001-134">While creating a VM through templates, the certificate gets referenced in the secrets section and the winRM section as below:</span></span>

    "osProfile": {
          ...
          "secrets": [
            {
              "sourceVault": {
                "id": "<resource id of the Key Vault containing the secret>"
              },
              "vaultCertificates": [
                {
                  "certificateUrl": "<URL for the certificate you got in Step 4>",
                  "certificateStore": "<Name of the certificate store on the VM>"
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
                  "certificateUrl": "<URL for the certificate you got in Step 4>"
                }
              ]
            },
            ...
          }
        },

<span data-ttu-id="7e001-135">É possível encontrar um modelo de exemplo para o indicado acima em [201-vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)</span><span class="sxs-lookup"><span data-stu-id="7e001-135">A sample template for the above can be found here at [201-vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)</span></span>

<span data-ttu-id="7e001-136">O código-fonte para este modelo pode ser encontrado no [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)</span><span class="sxs-lookup"><span data-stu-id="7e001-136">Source code for this template can be found on [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)</span></span>

#### <a name="powershell"></a><span data-ttu-id="7e001-137">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7e001-137">PowerShell</span></span>
    $vm = New-AzureRmVMConfig -VMName "<VM name>" -VMSize "<VM Size>"
    $credential = Get-Credential
    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName "<Computer Name>" -Credential $credential -WinRMHttp -WinRMHttps -WinRMCertificateUrl $secretURL
    $sourceVaultId = (Get-AzureRmKeyVault -ResourceGroupName "<Resource Group name>" -VaultName "<Vault Name>").ResourceId
    $CertificateStore = "My"
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore $CertificateStore -CertificateUrl $secretURL

## <a name="step-6-connecting-to-the-vm"></a><span data-ttu-id="7e001-138">Etapa 6: Conectando-se à VM</span><span class="sxs-lookup"><span data-stu-id="7e001-138">Step 6: Connecting to the VM</span></span>
<span data-ttu-id="7e001-139">Antes de poder se conectar à VM você precisará se certificar de que seu computador esteja configurado para o gerenciamento remoto do WinRM.</span><span class="sxs-lookup"><span data-stu-id="7e001-139">Before you can connect to the VM you'll need to make sure your machine is configured for WinRM remote management.</span></span> <span data-ttu-id="7e001-140">Inicie o PowerShell como administrador e execute o comando abaixo para garantir que você esteja configurado.</span><span class="sxs-lookup"><span data-stu-id="7e001-140">Start PowerShell as an administrator and execute the below command to make sure you're set up.</span></span>

    Enable-PSRemoting -Force

> [!NOTE]
> <span data-ttu-id="7e001-141">Você precisará garantir que o serviço WinRM está em execução se o indicado acima não funcionar.</span><span class="sxs-lookup"><span data-stu-id="7e001-141">You might need to make sure the WinRM service is running if the above does not work.</span></span> <span data-ttu-id="7e001-142">Você pode fazer isso usando `Get-Service WinRM`</span><span class="sxs-lookup"><span data-stu-id="7e001-142">You can do that using `Get-Service WinRM`</span></span>
> 
> 

<span data-ttu-id="7e001-143">Quando a instalação estiver concluída, você poderá se conectar à VM usando o comando abaixo</span><span class="sxs-lookup"><span data-stu-id="7e001-143">Once the setup is done, you can connect to the VM using the below command</span></span>

    Enter-PSSession -ConnectionUri https://<public-ip-dns-of-the-vm>:5986 -Credential $cred -SessionOption (New-PSSessionOption -SkipCACheck -SkipCNCheck -SkipRevocationCheck) -Authentication Negotiate
