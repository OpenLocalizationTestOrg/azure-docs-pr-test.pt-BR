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
# <a name="deploy-an-hpc-pack-2016-cluster-in-azure"></a><span data-ttu-id="a13a6-103">Implantar um cluster HPC Pack 2016 no Azure</span><span class="sxs-lookup"><span data-stu-id="a13a6-103">Deploy an HPC Pack 2016 cluster in Azure</span></span>

<span data-ttu-id="a13a6-104">Siga as etapas de saudação toodeploy este artigo uma [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) cluster em máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="a13a6-104">Follow hello steps in this article toodeploy a [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) cluster in Azure virtual machines.</span></span> <span data-ttu-id="a13a6-105">HPC Pack é a solução de HPC gratuita da Microsoft fundamentada nas tecnologias Microsoft Azure e Windows Server e que dá suporte a uma ampla gama de cargas de trabalho de HPC.</span><span class="sxs-lookup"><span data-stu-id="a13a6-105">HPC Pack is Microsoft's free HPC solution built on Microsoft Azure and Windows Server technologies and supports a wide range of HPC workloads.</span></span>

<span data-ttu-id="a13a6-106">Use uma saudação [modelos do Azure Resource Manager](https://github.com/MsHpcPack/HPCPack2016) toodeploy cluster de HPC Pack 2016 de saudação.</span><span class="sxs-lookup"><span data-stu-id="a13a6-106">Use one of hello [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) toodeploy hello HPC Pack 2016 cluster.</span></span> <span data-ttu-id="a13a6-107">Você tem várias opções de topologia de cluster com quantidades diferentes de nós principais do cluster, e com nós de computação Linux ou Windows.</span><span class="sxs-lookup"><span data-stu-id="a13a6-107">You have several choices of cluster topology with different numbers of cluster head nodes, and with either Linux or Windows compute nodes.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a13a6-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a13a6-108">Prerequisites</span></span>

### <a name="pfx-certificate"></a><span data-ttu-id="a13a6-109">Certificado PFX</span><span class="sxs-lookup"><span data-stu-id="a13a6-109">PFX certificate</span></span>

<span data-ttu-id="a13a6-110">Um cluster do Microsoft HPC Pack 2016 requer uma troca de informações pessoais (PFX) certificado toosecure Olá a comunicação entre nós HPC Olá.</span><span class="sxs-lookup"><span data-stu-id="a13a6-110">A Microsoft HPC Pack 2016 cluster requires a Personal Information Exchange (PFX) certificate toosecure hello communication between hello HPC nodes.</span></span> <span data-ttu-id="a13a6-111">certificado Olá deve atender aos Olá requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="a13a6-111">hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="a13a6-112">Ele deve ter uma chave privada capaz de fazer a troca das chaves</span><span class="sxs-lookup"><span data-stu-id="a13a6-112">It must have a private key capable of key exchange</span></span>
* <span data-ttu-id="a13a6-113">O uso da chave inclui a Assinatura Digital e a Codificação de Chave</span><span class="sxs-lookup"><span data-stu-id="a13a6-113">Key usage includes Digital Signature and Key Encipherment</span></span>
* <span data-ttu-id="a13a6-114">O uso avançado de chave inclui a Autenticação de Servidor e a Autenticação de Cliente</span><span class="sxs-lookup"><span data-stu-id="a13a6-114">Enhanced key usage includes Client Authentication and Server Authentication</span></span>

<span data-ttu-id="a13a6-115">Se você ainda não tiver um certificado que atenda a esses requisitos, você pode solicitar o certificado de saudação da autoridade de certificação.</span><span class="sxs-lookup"><span data-stu-id="a13a6-115">If you don’t already have a certificate that meets these requirements, you can request hello certificate from a certification authority.</span></span> <span data-ttu-id="a13a6-116">Como alternativa, você pode usar o hello comandos toogenerate Olá certificado autoassinado com base no sistema de operacional Olá no qual executar o comando hello e exportar o certificado em formato PFX Olá com chave privada a seguir.</span><span class="sxs-lookup"><span data-stu-id="a13a6-116">Alternatively, you can use hello following commands toogenerate hello self-signed certificate based on hello operating system on which you run hello command, and export hello PFX format certificate with private key.</span></span>

* <span data-ttu-id="a13a6-117">**Para Windows 10 ou Windows Server 2016**, execute Olá interna **New-SelfSignedCertificate** cmdlet do PowerShell da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="a13a6-117">**For Windows 10 or Windows Server 2016**, run hello built-in **New-SelfSignedCertificate** PowerShell cmdlet as follows:</span></span>

  ```PowerShell
  New-SelfSignedCertificate -Subject "CN=HPC Pack 2016 Communication" -KeySpec KeyExchange -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2") -CertStoreLocation cert:\CurrentUser\My -KeyExportPolicy Exportable -NotAfter (Get-Date).AddYears(5)
  ```
* <span data-ttu-id="a13a6-118">**Para sistemas operacionais anteriores ao Windows 10 ou Windows Server 2016**, baixar Olá [gerador de certificado autoassinado](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) de saudação Microsoft Script Center.</span><span class="sxs-lookup"><span data-stu-id="a13a6-118">**For operating systems earlier than Windows 10 or Windows Server 2016**, download hello [self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from hello Microsoft Script Center.</span></span> <span data-ttu-id="a13a6-119">Extraia o conteúdo e execute Olá comandos em um prompt do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="a13a6-119">Extract its contents and run hello following commands at a PowerShell prompt:</span></span>

    ```PowerShell 
    Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
  
    New-SelfSignedCertificateEx -Subject "CN=HPC Pack 2016 Communication" -KeySpec Exchange -KeyUsage "DigitalSignature,KeyEncipherment" -EnhancedKeyUsage "Server Authentication","Client Authentication" -StoreLocation CurrentUser -Exportable -NotAfter (Get-Date).AddYears(5)
    ```

### <a name="upload-certificate-tooan-azure-key-vault"></a><span data-ttu-id="a13a6-120">Carregar certificado tooan Cofre de chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="a13a6-120">Upload certificate tooan Azure key vault</span></span>

<span data-ttu-id="a13a6-121">Antes de implantar o cluster HPC hello, carregar Olá certificado tooan [Cofre de chaves do Azure](../../key-vault/index.md) como uma saudação segreda e registrar informações para uso durante a implantação de saudação a seguir: **nome do cofre**,  **Grupo de recursos do cofre**, **URL de certificado**, e **impressão digital do certificado**.</span><span class="sxs-lookup"><span data-stu-id="a13a6-121">Before deploying hello HPC cluster, upload hello certificate tooan [Azure key vault](../../key-vault/index.md) as a secret, and record hello following information for use during hello deployment: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

<span data-ttu-id="a13a6-122">Segue uma amostra do PowerShell script tooupload saudação do certificado.</span><span class="sxs-lookup"><span data-stu-id="a13a6-122">A sample PowerShell script tooupload hello certificate follows.</span></span> <span data-ttu-id="a13a6-123">Para obter mais informações sobre como carregar um certificado tooan Cofre de chaves do Azure, consulte [Introdução ao Azure Key Vault](../../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a13a6-123">For more information about uploading a certificate tooan Azure key vault, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md).</span></span>

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


## <a name="supported-topologies"></a><span data-ttu-id="a13a6-124">Topologias com suporte</span><span class="sxs-lookup"><span data-stu-id="a13a6-124">Supported topologies</span></span>

<span data-ttu-id="a13a6-125">Escolha uma saudação [modelos do Azure Resource Manager](https://github.com/MsHpcPack/HPCPack2016) toodeploy cluster de HPC Pack 2016 de saudação.</span><span class="sxs-lookup"><span data-stu-id="a13a6-125">Choose one of hello [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) toodeploy hello HPC Pack 2016 cluster.</span></span> <span data-ttu-id="a13a6-126">A seguir estão as arquiteturas de alto nível das três topologias de cluster com suporte.</span><span class="sxs-lookup"><span data-stu-id="a13a6-126">Following are high-level architectures of three supported cluster topologies.</span></span> <span data-ttu-id="a13a6-127">As topologias de alta disponibilidade incluem vários nós de cabeçalho do cluster.</span><span class="sxs-lookup"><span data-stu-id="a13a6-127">High-availability topologies include multiple cluster head nodes.</span></span>

1. <span data-ttu-id="a13a6-128">Cluster de alta disponibilidade com o domínio do Active Directory</span><span class="sxs-lookup"><span data-stu-id="a13a6-128">High-availability cluster with Active Directory domain</span></span>

    ![Cluster de alta disponibilidade no domínio do AD](./media/hpcpack-2016-cluster/haad.png)



2. <span data-ttu-id="a13a6-130">Cluster de alta disponibilidade sem o domínio do Active Directory</span><span class="sxs-lookup"><span data-stu-id="a13a6-130">High-availability cluster without Active Directory domain</span></span>

    ![Cluster de alta disponibilidade sem domínio do AD](./media/hpcpack-2016-cluster/hanoad.png)

3. <span data-ttu-id="a13a6-132">Cluster com um único nó de cabeçalho</span><span class="sxs-lookup"><span data-stu-id="a13a6-132">Cluster with a single head node</span></span>

   ![Cluster com um único nó principal](./media/hpcpack-2016-cluster/singlehn.png)


## <a name="deploy-a-cluster"></a><span data-ttu-id="a13a6-134">Implantar um cluster</span><span class="sxs-lookup"><span data-stu-id="a13a6-134">Deploy a cluster</span></span>

<span data-ttu-id="a13a6-135">cluster de saudação toocreate, escolha um modelo e clique em **implantar tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="a13a6-135">toocreate hello cluster, choose a template and click **Deploy tooAzure**.</span></span> <span data-ttu-id="a13a6-136">Em Olá [portal do Azure](https://portal.azure.com), especificar parâmetros de modelo hello, conforme descrito em Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="a13a6-136">In hello [Azure portal](https://portal.azure.com), specify parameters for hello template as described in hello following steps.</span></span> <span data-ttu-id="a13a6-137">Cada modelo cria todos os recursos do Azure, necessários para a infraestrutura de cluster HPC hello.</span><span class="sxs-lookup"><span data-stu-id="a13a6-137">Each template creates all Azure resources required for hello HPC cluster infrastructure.</span></span> <span data-ttu-id="a13a6-138">Os recursos incluem uma rede virtual do Azure, um endereço IP público, um balanceador de carga (apenas para um cluster de alta disponibilidade), interfaces de rede, conjuntos de disponibilidade, contas de armazenamento e máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="a13a6-138">Resources include an Azure virtual network, public IP address, load balancer (only for a high-availability cluster), network interfaces, availability sets, storage accounts, and virtual machines.</span></span>

### <a name="step-1-select-hello-subscription-location-and-resource-group"></a><span data-ttu-id="a13a6-139">Etapa 1: Selecione a assinatura hello, o local e o grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="a13a6-139">Step 1: Select hello subscription, location, and resource group</span></span>

<span data-ttu-id="a13a6-140">Olá **assinatura** e hello **local** deve ser o mesmo que você especificou quando você carregar seu certificado PFX (consulte pré-requisitos).</span><span class="sxs-lookup"><span data-stu-id="a13a6-140">hello **Subscription** and hello **Location** must be same that you specified when you uploaded your PFX certificate (see Prerequisites).</span></span> <span data-ttu-id="a13a6-141">É recomendável que você crie um **grupo de recursos** para implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="a13a6-141">We recommend that you create a **Resource group** for hello deployment.</span></span>

### <a name="step-2-specify-hello-parameter-settings"></a><span data-ttu-id="a13a6-142">Etapa 2: Especificar as configurações de parâmetro hello</span><span class="sxs-lookup"><span data-stu-id="a13a6-142">Step 2: Specify hello parameter settings</span></span>

<span data-ttu-id="a13a6-143">Digite ou modifique os valores para parâmetros de modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="a13a6-143">Enter or modify values for hello template parameters.</span></span> <span data-ttu-id="a13a6-144">Clique em Olá ícone próximo tooeach parâmetro para obter informações de Ajuda.</span><span class="sxs-lookup"><span data-stu-id="a13a6-144">Click hello icon next tooeach parameter for help information.</span></span> <span data-ttu-id="a13a6-145">Consulte também as diretrizes de saudação para [tamanhos VM disponíveis](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="a13a6-145">Also see hello guidance for [available VM sizes](sizes.md).</span></span>

<span data-ttu-id="a13a6-146">Especificar valores hello registradas na Olá pré-requisitos para Olá parâmetros a seguir: **nome do cofre**, **grupo de recursos do cofre**, **URL de certificado**e **Impressão digital do certificado**.</span><span class="sxs-lookup"><span data-stu-id="a13a6-146">Specify hello values you recorded in hello Prerequisites for hello following parameters: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

### <a name="step-3-review-legal-terms-and-create"></a><span data-ttu-id="a13a6-147">Etapa 3.</span><span class="sxs-lookup"><span data-stu-id="a13a6-147">Step 3.</span></span> <span data-ttu-id="a13a6-148">Examinar os termos legais e criar</span><span class="sxs-lookup"><span data-stu-id="a13a6-148">Review legal terms and create</span></span>
<span data-ttu-id="a13a6-149">Clique em **revisar os termos legais** tooreview termos de saudação.</span><span class="sxs-lookup"><span data-stu-id="a13a6-149">Click **Review legal terms** tooreview hello terms.</span></span> <span data-ttu-id="a13a6-150">Se você concordar, clique em **compra**e, em seguida, clique em **criar** toostart implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="a13a6-150">If you agree, click **Purchase**, and then click **Create** toostart hello deployment.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="a13a6-151">Conecte-se o cluster toohello</span><span class="sxs-lookup"><span data-stu-id="a13a6-151">Connect toohello cluster</span></span>
1. <span data-ttu-id="a13a6-152">Após a implantação de cluster de HPC Pack hello, vá toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a13a6-152">After hello HPC Pack cluster is deployed, go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="a13a6-153">Clique em **grupos de recursos**e o grupo de recursos Olá localizar quais Olá cluster foi implantado.</span><span class="sxs-lookup"><span data-stu-id="a13a6-153">Click **Resource groups**, and find hello resource group in which hello cluster was deployed.</span></span> <span data-ttu-id="a13a6-154">Você pode encontrar hello máquinas virtuais de nó principal.</span><span class="sxs-lookup"><span data-stu-id="a13a6-154">You can find hello head node virtual machines.</span></span>

    ![Nós de cluster principal no portal de saudação](./media/hpcpack-2016-cluster/clusterhns.png)

2. <span data-ttu-id="a13a6-156">Clique em um nó principal (em um cluster de alta disponibilidade, clique em qualquer um de nós de cabeçalho Olá).</span><span class="sxs-lookup"><span data-stu-id="a13a6-156">Click one head node (in a high-availability cluster, click any of hello head nodes).</span></span> <span data-ttu-id="a13a6-157">Em **Essentials**, você pode encontrar o endereço IP público de saudação ou nome DNS completo do cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="a13a6-157">In **Essentials**, you can find hello public IP address or full DNS name of hello cluster.</span></span>

    ![Configurações de conexão do cluster](./media/hpcpack-2016-cluster/clusterconnect.png)

3. <span data-ttu-id="a13a6-159">Clique em **conectar** toolog na tooany de nós de cabeçalho hello usando a área de trabalho remota com seu nome de usuário de administrador especificada.</span><span class="sxs-lookup"><span data-stu-id="a13a6-159">Click **Connect** toolog on tooany of hello head nodes using Remote Desktop with your specified administrator user name.</span></span> <span data-ttu-id="a13a6-160">Se for cluster Olá implantado em um domínio do Active Directory, o nome de usuário de saudação é do formulário de saudação <privateDomainName> \<adminUsername > (por exemplo, hpc.local\hpcadmin).</span><span class="sxs-lookup"><span data-stu-id="a13a6-160">If hello cluster you deployed is in an Active Directory Domain, hello user name is of hello form <privateDomainName>\<adminUsername> (for example, hpc.local\hpcadmin).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a13a6-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a13a6-161">Next steps</span></span>
* <span data-ttu-id="a13a6-162">Cluster de tooyour trabalhos de envio.</span><span class="sxs-lookup"><span data-stu-id="a13a6-162">Submit jobs tooyour cluster.</span></span> <span data-ttu-id="a13a6-163">Consulte [enviar trabalhos tooHPC um cluster de HPC Pack no Azure](hpcpack-cluster-submit-jobs.md) e [gerenciar um cluster de HPC Pack 2016 no Azure usando o Active Directory do Azure](hpcpack-cluster-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="a13a6-163">See [Submit jobs tooHPC an HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md) and [Manage an HPC Pack 2016 cluster in Azure using Azure Active Directory](hpcpack-cluster-active-directory.md).</span></span>

