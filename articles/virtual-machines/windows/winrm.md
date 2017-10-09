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
# <a name="setting-up-winrm-access-for-virtual-machines-in-azure-resource-manager"></a><span data-ttu-id="66d4e-103">Configurando o acesso do WinRM para as máquinas virtuais no Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="66d4e-103">Setting up WinRM access for Virtual Machines in Azure Resource Manager</span></span>
## <a name="winrm-in-azure-service-management-vs-azure-resource-manager"></a><span data-ttu-id="66d4e-104">WinRM no Gerenciamento de Serviços do Azure vs. Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="66d4e-104">WinRM in Azure Service Management vs Azure Resource Manager</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

* <span data-ttu-id="66d4e-105">Para obter uma visão geral de saudação do Azure Resource Manager, consulte esta [artigo](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="66d4e-105">For an overview of hello Azure Resource Manager, please see this [article](../../azure-resource-manager/resource-group-overview.md)</span></span>
* <span data-ttu-id="66d4e-106">Para encontrar as diferenças entre o Gerenciamento de Serviços do Azure e o Azure Resource Manager, consulte este [artigo](../../resource-manager-deployment-model.md)</span><span class="sxs-lookup"><span data-stu-id="66d4e-106">For differences between Azure Service Management and Azure Resource Manager, please see this [article](../../resource-manager-deployment-model.md)</span></span>

<span data-ttu-id="66d4e-107">Olá chave diferença na configuração de WinRM entre duas pilhas de saudação é como certificado Olá obtém instalado no hello VM.</span><span class="sxs-lookup"><span data-stu-id="66d4e-107">hello key difference in setting up WinRM configuration between hello two stacks is how hello certificate gets installed on hello VM.</span></span> <span data-ttu-id="66d4e-108">Na pilha do Gerenciador de recursos do Azure hello, certificados de saudação são modelados como recursos gerenciados pelo provedor de recursos do Cofre de chave de saudação.</span><span class="sxs-lookup"><span data-stu-id="66d4e-108">In hello Azure Resource Manager stack, hello certificates are modeled as resources managed by hello Key Vault Resource Provider.</span></span> <span data-ttu-id="66d4e-109">Portanto, o usuário Olá precisa tooprovide seu próprio certificado e carregá-lo tooa Cofre de chaves antes de usá-lo em uma VM.</span><span class="sxs-lookup"><span data-stu-id="66d4e-109">Therefore, hello user needs tooprovide their own certificate and upload it tooa Key Vault before using it in a VM.</span></span>

<span data-ttu-id="66d4e-110">Aqui estão as etapas de saudação necessário tooset tootake backup de uma VM com conectividade do WinRM</span><span class="sxs-lookup"><span data-stu-id="66d4e-110">Here are hello steps you need tootake tooset up a VM with WinRM connectivity</span></span>

1. <span data-ttu-id="66d4e-111">Criar um cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="66d4e-111">Create a Key Vault</span></span>
2. <span data-ttu-id="66d4e-112">Crie um certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="66d4e-112">Create a self-signed certificate</span></span>
3. <span data-ttu-id="66d4e-113">Carregar tooKey seu certificado autoassinado cofre</span><span class="sxs-lookup"><span data-stu-id="66d4e-113">Upload your self-signed certificate tooKey Vault</span></span>
4. <span data-ttu-id="66d4e-114">Obter URL de saudação de seu certificado autoassinado no hello Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="66d4e-114">Get hello URL for your self-signed certificate in hello Key Vault</span></span>
5. <span data-ttu-id="66d4e-115">Referenciar a URL de seus certificados autoassinados ao criar uma VM</span><span class="sxs-lookup"><span data-stu-id="66d4e-115">Reference your self-signed certificates URL while creating a VM</span></span>

## <a name="step-1-create-a-key-vault"></a><span data-ttu-id="66d4e-116">Etapa 1: Criar um cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="66d4e-116">Step 1: Create a Key Vault</span></span>
<span data-ttu-id="66d4e-117">Você pode usar o hello abaixo saudação do comando toocreate Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="66d4e-117">You can use hello below command toocreate hello Key Vault</span></span>

```
New-AzureRmKeyVault -VaultName "<vault-name>" -ResourceGroupName "<rg-name>" -Location "<vault-location>" -EnabledForDeployment -EnabledForTemplateDeployment
```

## <a name="step-2-create-a-self-signed-certificate"></a><span data-ttu-id="66d4e-118">Etapa 2: Criar um certificado autoassinado</span><span class="sxs-lookup"><span data-stu-id="66d4e-118">Step 2: Create a self-signed certificate</span></span>
<span data-ttu-id="66d4e-119">Você pode criar um certificado autoassinado usando esse script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="66d4e-119">You can create a self-signed certificate using this PowerShell script</span></span>

```
$certificateName = "somename"

$thumbprint = (New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation Cert:\CurrentUser\My -KeySpec KeyExchange).Thumbprint

$cert = (Get-ChildItem -Path cert:\CurrentUser\My\$thumbprint)

$password = Read-Host -Prompt "Please enter hello certificate password." -AsSecureString

Export-PfxCertificate -Cert $cert -FilePath ".\$certificateName.pfx" -Password $password
```

## <a name="step-3-upload-your-self-signed-certificate-toohello-key-vault"></a><span data-ttu-id="66d4e-120">Etapa 3: Carregar toohello seu certificado autoassinado Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="66d4e-120">Step 3: Upload your self-signed certificate toohello Key Vault</span></span>
<span data-ttu-id="66d4e-121">Antes de carregar Olá certificado toohello Cofre de chaves criado na etapa 1, ele precisa tooconverted em uma saudação do formato Microsoft. Compute compreenda o provedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="66d4e-121">Before uploading hello certificate toohello Key Vault created in step 1, it needs tooconverted into a format hello Microsoft.Compute resource provider will understand.</span></span> <span data-ttu-id="66d4e-122">Olá script do PowerShell abaixo permitirá a que você fazer isso</span><span class="sxs-lookup"><span data-stu-id="66d4e-122">hello below PowerShell script will allow you do that</span></span>

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

## <a name="step-4-get-hello-url-for-your-self-signed-certificate-in-hello-key-vault"></a><span data-ttu-id="66d4e-123">Etapa 4: Obter a URL de saudação de seu certificado autoassinado no hello Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="66d4e-123">Step 4: Get hello URL for your self-signed certificate in hello Key Vault</span></span>
<span data-ttu-id="66d4e-124">provedor de recursos Microsoft. Compute Olá precisa de um segredo de toohello URL dentro de saudação Cofre de chaves durante o provisionamento Olá VM.</span><span class="sxs-lookup"><span data-stu-id="66d4e-124">hello Microsoft.Compute resource provider needs a URL toohello secret inside hello Key Vault while provisioning hello VM.</span></span> <span data-ttu-id="66d4e-125">Isso habilita o segredo de Olá Olá Microsoft. Compute recurso provedor toodownload e criar certificado equivalente Olá em Olá VM.</span><span class="sxs-lookup"><span data-stu-id="66d4e-125">This enables hello Microsoft.Compute resource provider toodownload hello secret and create hello equivalent certificate on hello VM.</span></span>

> [!NOTE]
> <span data-ttu-id="66d4e-126">URL de saudação do segredo Olá precisa tooinclude Olá versão também.</span><span class="sxs-lookup"><span data-stu-id="66d4e-126">hello URL of hello secret needs tooinclude hello version as well.</span></span> <span data-ttu-id="66d4e-127">Uma URL de exemplo tem a aparência abaixo https://contosovault.vault.azure.net:443/secrets/contososecret/01h9db0df2cd4300a20ence585a6s7ve</span><span class="sxs-lookup"><span data-stu-id="66d4e-127">An example URL looks like below https://contosovault.vault.azure.net:443/secrets/contososecret/01h9db0df2cd4300a20ence585a6s7ve</span></span>
> 
> 

#### <a name="templates"></a><span data-ttu-id="66d4e-128">Modelos</span><span class="sxs-lookup"><span data-stu-id="66d4e-128">Templates</span></span>
<span data-ttu-id="66d4e-129">Você pode obter Olá link toohello URL no modelo Olá Olá código abaixo</span><span class="sxs-lookup"><span data-stu-id="66d4e-129">You can get hello link toohello URL in hello template using hello below code</span></span>

    "certificateUrl": "[reference(resourceId(resourceGroup().name, 'Microsoft.KeyVault/vaults/secrets', '<vault-name>', '<secret-name>'), '2015-06-01').secretUriWithVersion]"

#### <a name="powershell"></a><span data-ttu-id="66d4e-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="66d4e-130">PowerShell</span></span>
<span data-ttu-id="66d4e-131">Você pode obter essa URL usando Olá abaixo de comando do PowerShell</span><span class="sxs-lookup"><span data-stu-id="66d4e-131">You can get this URL using hello below PowerShell command</span></span>

    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id

## <a name="step-5-reference-your-self-signed-certificates-url-while-creating-a-vm"></a><span data-ttu-id="66d4e-132">Etapa 5: Referenciar a URL de seus certificados autoassinados ao criar uma VM</span><span class="sxs-lookup"><span data-stu-id="66d4e-132">Step 5: Reference your self-signed certificates URL while creating a VM</span></span>
#### <a name="azure-resource-manager-templates"></a><span data-ttu-id="66d4e-133">Modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="66d4e-133">Azure Resource Manager Templates</span></span>
<span data-ttu-id="66d4e-134">Ao criar uma VM por meio de modelos, certificado Olá obtém referenciado nos Olá segredos seção e Olá winRM como abaixo:</span><span class="sxs-lookup"><span data-stu-id="66d4e-134">While creating a VM through templates, hello certificate gets referenced in hello secrets section and hello winRM section as below:</span></span>

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

<span data-ttu-id="66d4e-135">Um modelo de exemplo hello acima pode ser encontrado aqui em [201 vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)</span><span class="sxs-lookup"><span data-stu-id="66d4e-135">A sample template for hello above can be found here at [201-vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)</span></span>

<span data-ttu-id="66d4e-136">O código-fonte para este modelo pode ser encontrado no [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)</span><span class="sxs-lookup"><span data-stu-id="66d4e-136">Source code for this template can be found on [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)</span></span>

#### <a name="powershell"></a><span data-ttu-id="66d4e-137">PowerShell</span><span class="sxs-lookup"><span data-stu-id="66d4e-137">PowerShell</span></span>
    $vm = New-AzureRmVMConfig -VMName "<VM name>" -VMSize "<VM Size>"
    $credential = Get-Credential
    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName "<Computer Name>" -Credential $credential -WinRMHttp -WinRMHttps -WinRMCertificateUrl $secretURL
    $sourceVaultId = (Get-AzureRmKeyVault -ResourceGroupName "<Resource Group name>" -VaultName "<Vault Name>").ResourceId
    $CertificateStore = "My"
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore $CertificateStore -CertificateUrl $secretURL

## <a name="step-6-connecting-toohello-vm"></a><span data-ttu-id="66d4e-138">Etapa 6: Conectando toohello VM</span><span class="sxs-lookup"><span data-stu-id="66d4e-138">Step 6: Connecting toohello VM</span></span>
<span data-ttu-id="66d4e-139">Antes de poder conectar toohello VM precisará toomake se que seu computador está configurado para gerenciamento remoto do WinRM.</span><span class="sxs-lookup"><span data-stu-id="66d4e-139">Before you can connect toohello VM you'll need toomake sure your machine is configured for WinRM remote management.</span></span> <span data-ttu-id="66d4e-140">Inicie o PowerShell como administrador e execute Olá abaixo comando toomake-se de que configurá-lo.</span><span class="sxs-lookup"><span data-stu-id="66d4e-140">Start PowerShell as an administrator and execute hello below command toomake sure you're set up.</span></span>

    Enable-PSRemoting -Force

> [!NOTE]
> <span data-ttu-id="66d4e-141">Talvez seja necessário toomake se Olá serviço WinRM está em execução se Olá acima não funcionará.</span><span class="sxs-lookup"><span data-stu-id="66d4e-141">You might need toomake sure hello WinRM service is running if hello above does not work.</span></span> <span data-ttu-id="66d4e-142">Você pode fazer isso usando `Get-Service WinRM`</span><span class="sxs-lookup"><span data-stu-id="66d4e-142">You can do that using `Get-Service WinRM`</span></span>
> 
> 

<span data-ttu-id="66d4e-143">Depois da instalação hello, você pode se conectar toohello VM usando Olá comando abaixo</span><span class="sxs-lookup"><span data-stu-id="66d4e-143">Once hello setup is done, you can connect toohello VM using hello below command</span></span>

    Enter-PSSession -ConnectionUri https://<public-ip-dns-of-the-vm>:5986 -Credential $cred -SessionOption (New-PSSessionOption -SkipCACheck -SkipCNCheck -SkipRevocationCheck) -Authentication Negotiate
