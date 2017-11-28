---
title: Cluster HPC Pack 2016 no Azure | Microsoft Docs
description: Saiba como implantar um cluster HPC Pack 2016 no Azure
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
ms.openlocfilehash: 88d1f4e29f38ba1a6bef57c2da43bee205575eee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-an-hpc-pack-2016-cluster-in-azure"></a><span data-ttu-id="c3441-103">Implantar um cluster HPC Pack 2016 no Azure</span><span class="sxs-lookup"><span data-stu-id="c3441-103">Deploy an HPC Pack 2016 cluster in Azure</span></span>

<span data-ttu-id="c3441-104">Siga as etapas neste artigo para implantar um cluster [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) em máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="c3441-104">Follow the steps in this article to deploy a [Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) cluster in Azure virtual machines.</span></span> <span data-ttu-id="c3441-105">HPC Pack é a solução de HPC gratuita da Microsoft fundamentada nas tecnologias Microsoft Azure e Windows Server e que dá suporte a uma ampla gama de cargas de trabalho de HPC.</span><span class="sxs-lookup"><span data-stu-id="c3441-105">HPC Pack is Microsoft's free HPC solution built on Microsoft Azure and Windows Server technologies and supports a wide range of HPC workloads.</span></span>

<span data-ttu-id="c3441-106">Use um do [modelos do Azure Resource Manager](https://github.com/MsHpcPack/HPCPack2016) para implantar o cluster HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="c3441-106">Use one of the [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) to deploy the HPC Pack 2016 cluster.</span></span> <span data-ttu-id="c3441-107">Você tem várias opções de topologia de cluster com quantidades diferentes de nós principais do cluster, e com nós de computação Linux ou Windows.</span><span class="sxs-lookup"><span data-stu-id="c3441-107">You have several choices of cluster topology with different numbers of cluster head nodes, and with either Linux or Windows compute nodes.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3441-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c3441-108">Prerequisites</span></span>

### <a name="pfx-certificate"></a><span data-ttu-id="c3441-109">Certificado PFX</span><span class="sxs-lookup"><span data-stu-id="c3441-109">PFX certificate</span></span>

<span data-ttu-id="c3441-110">Um cluster Microsoft HPC Pack 2016 requer um certificado PFX (Troca de Informações Pessoais) para proteger a comunicação entre os nós HPC.</span><span class="sxs-lookup"><span data-stu-id="c3441-110">A Microsoft HPC Pack 2016 cluster requires a Personal Information Exchange (PFX) certificate to secure the communication between the HPC nodes.</span></span> <span data-ttu-id="c3441-111">O certificado deve atender aos seguintes requisitos:</span><span class="sxs-lookup"><span data-stu-id="c3441-111">The certificate must meet the following requirements:</span></span>

* <span data-ttu-id="c3441-112">Ele deve ter uma chave privada capaz de fazer a troca das chaves</span><span class="sxs-lookup"><span data-stu-id="c3441-112">It must have a private key capable of key exchange</span></span>
* <span data-ttu-id="c3441-113">O uso da chave inclui a Assinatura Digital e a Codificação de Chave</span><span class="sxs-lookup"><span data-stu-id="c3441-113">Key usage includes Digital Signature and Key Encipherment</span></span>
* <span data-ttu-id="c3441-114">O uso avançado de chave inclui a Autenticação de Servidor e a Autenticação de Cliente</span><span class="sxs-lookup"><span data-stu-id="c3441-114">Enhanced key usage includes Client Authentication and Server Authentication</span></span>

<span data-ttu-id="c3441-115">Se você ainda não tiver um certificado que atende a esses requisitos, solicite o certificado de uma autoridade de certificação.</span><span class="sxs-lookup"><span data-stu-id="c3441-115">If you don’t already have a certificate that meets these requirements, you can request the certificate from a certification authority.</span></span> <span data-ttu-id="c3441-116">Como alternativa, você pode usar os comandos a seguir para gerar o certificado autoassinado com base no sistema operacional em que o comando é executado e exportar o certificado em formato PFX com a chave privada.</span><span class="sxs-lookup"><span data-stu-id="c3441-116">Alternatively, you can use the following commands to generate the self-signed certificate based on the operating system on which you run the command, and export the PFX format certificate with private key.</span></span>

* <span data-ttu-id="c3441-117">**Para o Windows 10 ou Windows Server 2016**, execute o cmdlet **New-SelfSignedCertificate** interno do PowerShell da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="c3441-117">**For Windows 10 or Windows Server 2016**, run the built-in **New-SelfSignedCertificate** PowerShell cmdlet as follows:</span></span>

  ```PowerShell
  New-SelfSignedCertificate -Subject "CN=HPC Pack 2016 Communication" -KeySpec KeyExchange -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2") -CertStoreLocation cert:\CurrentUser\My -KeyExportPolicy Exportable -NotAfter (Get-Date).AddYears(5)
  ```
* <span data-ttu-id="c3441-118">**Para sistemas operacionais anteriores ao Windows 10 ou Windows Server 2016**, baixe o [gerador de certificado autoassinado](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) no Microsoft Script Center.</span><span class="sxs-lookup"><span data-stu-id="c3441-118">**For operating systems earlier than Windows 10 or Windows Server 2016**, download the [self-signed certificate generator](https://gallery.technet.microsoft.com/scriptcenter/Self-signed-certificate-5920a7c6/) from the Microsoft Script Center.</span></span> <span data-ttu-id="c3441-119">Extraia o conteúdo e execute os seguintes comandos em um prompt do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c3441-119">Extract its contents and run the following commands at a PowerShell prompt:</span></span>

    ```PowerShell 
    Import-Module -Name c:\ExtractedModule\New-SelfSignedCertificateEx.ps1
  
    New-SelfSignedCertificateEx -Subject "CN=HPC Pack 2016 Communication" -KeySpec Exchange -KeyUsage "DigitalSignature,KeyEncipherment" -EnhancedKeyUsage "Server Authentication","Client Authentication" -StoreLocation CurrentUser -Exportable -NotAfter (Get-Date).AddYears(5)
    ```

### <a name="upload-certificate-to-an-azure-key-vault"></a><span data-ttu-id="c3441-120">Carregar o certificado em um Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="c3441-120">Upload certificate to an Azure key vault</span></span>

<span data-ttu-id="c3441-121">Antes de implantar o cluster HPC, carregue o certificado em um [cofre de chaves do Azure](../../key-vault/index.md) como um segredo e registre as seguintes informações para uso durante a implantação: **Nome do cofre**, **Grupo de recursos do cofre**, **URL do certificado** e **Impressão digital do certificado**.</span><span class="sxs-lookup"><span data-stu-id="c3441-121">Before deploying the HPC cluster, upload the certificate to an [Azure key vault](../../key-vault/index.md) as a secret, and record the following information for use during the deployment: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

<span data-ttu-id="c3441-122">Segue um exemplo de script do PowerShell para carregar o certificado.</span><span class="sxs-lookup"><span data-stu-id="c3441-122">A sample PowerShell script to upload the certificate follows.</span></span> <span data-ttu-id="c3441-123">Para saber mais sobre como carregar um certificado em um cofre de chaves do Azure, confira [Introdução ao Cofre de Chaves do Azure](../../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c3441-123">For more information about uploading a certificate to an Azure key vault, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md).</span></span>

```powershell
#Give the following values
$VaultName = "mytestvault"
$SecretName = "hpcpfxcert"
$VaultRG = "myresourcegroup"
$location = "westus"
$PfxFile = "c:\Temp\mytest.pfx"
$Password = "yourpfxkeyprotectionpassword"
#Validate the pfx file
try {
    $pfxCert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList $PfxFile, $Password
}
catch [System.Management.Automation.MethodInvocationException]
{
    throw $_.Exception.InnerException
}
$thumbprint = $pfxCert.Thumbprint
$pfxCert.Dispose()
# Create and encode the JSON object
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
#Create an Azure key vault and upload the certificate as a secret
$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
$rg = Get-AzureRmResourceGroup -Name $VaultRG -Location $location -ErrorAction SilentlyContinue
if($null -eq $rg)
{
    $rg = New-AzureRmResourceGroup -Name $VaultRG -Location $location
}
$hpcKeyVault = New-AzureRmKeyVault -VaultName $VaultName -ResourceGroupName $VaultRG -Location $location -EnabledForDeployment -EnabledForTemplateDeployment
$hpcSecret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secret
"The following Information will be used in the deployment template"
"Vault Name             :   $VaultName"
"Vault Resource Group   :   $VaultRG"
"Certificate URL        :   $($hpcSecret.Id)"
"Certificate Thumbprint :   $thumbprint"

```


## <a name="supported-topologies"></a><span data-ttu-id="c3441-124">Topologias com suporte</span><span class="sxs-lookup"><span data-stu-id="c3441-124">Supported topologies</span></span>

<span data-ttu-id="c3441-125">Escolha uma da [modelos do Azure Resource Manager](https://github.com/MsHpcPack/HPCPack2016) para implantar o cluster HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="c3441-125">Choose one of the [Azure Resource Manager templates](https://github.com/MsHpcPack/HPCPack2016) to deploy the HPC Pack 2016 cluster.</span></span> <span data-ttu-id="c3441-126">A seguir estão as arquiteturas de alto nível das três topologias de cluster com suporte.</span><span class="sxs-lookup"><span data-stu-id="c3441-126">Following are high-level architectures of three supported cluster topologies.</span></span> <span data-ttu-id="c3441-127">As topologias de alta disponibilidade incluem vários nós de cabeçalho do cluster.</span><span class="sxs-lookup"><span data-stu-id="c3441-127">High-availability topologies include multiple cluster head nodes.</span></span>

1. <span data-ttu-id="c3441-128">Cluster de alta disponibilidade com o domínio do Active Directory</span><span class="sxs-lookup"><span data-stu-id="c3441-128">High-availability cluster with Active Directory domain</span></span>

    ![Cluster de alta disponibilidade no domínio do AD](./media/hpcpack-2016-cluster/haad.png)



2. <span data-ttu-id="c3441-130">Cluster de alta disponibilidade sem o domínio do Active Directory</span><span class="sxs-lookup"><span data-stu-id="c3441-130">High-availability cluster without Active Directory domain</span></span>

    ![Cluster de alta disponibilidade sem domínio do AD](./media/hpcpack-2016-cluster/hanoad.png)

3. <span data-ttu-id="c3441-132">Cluster com um único nó de cabeçalho</span><span class="sxs-lookup"><span data-stu-id="c3441-132">Cluster with a single head node</span></span>

   ![Cluster com um único nó principal](./media/hpcpack-2016-cluster/singlehn.png)


## <a name="deploy-a-cluster"></a><span data-ttu-id="c3441-134">Implantar um cluster</span><span class="sxs-lookup"><span data-stu-id="c3441-134">Deploy a cluster</span></span>

<span data-ttu-id="c3441-135">Para criar o cluster, escolha um modelo e clique em **Implantar no Azure**.</span><span class="sxs-lookup"><span data-stu-id="c3441-135">To create the cluster, choose a template and click **Deploy to Azure**.</span></span> <span data-ttu-id="c3441-136">No [portal do Azure](https://portal.azure.com), especifique parâmetros para o modelo, conforme descrito nas etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="c3441-136">In the [Azure portal](https://portal.azure.com), specify parameters for the template as described in the following steps.</span></span> <span data-ttu-id="c3441-137">Cada modelo cria todos os recursos do Azure necessários para a infraestrutura do cluster HPC.</span><span class="sxs-lookup"><span data-stu-id="c3441-137">Each template creates all Azure resources required for the HPC cluster infrastructure.</span></span> <span data-ttu-id="c3441-138">Os recursos incluem uma rede virtual do Azure, um endereço IP público, um balanceador de carga (apenas para um cluster de alta disponibilidade), interfaces de rede, conjuntos de disponibilidade, contas de armazenamento e máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="c3441-138">Resources include an Azure virtual network, public IP address, load balancer (only for a high-availability cluster), network interfaces, availability sets, storage accounts, and virtual machines.</span></span>

### <a name="step-1-select-the-subscription-location-and-resource-group"></a><span data-ttu-id="c3441-139">Etapa 1: selecionar a assinatura, o local e o grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="c3441-139">Step 1: Select the subscription, location, and resource group</span></span>

<span data-ttu-id="c3441-140">A **assinatura** e o **local** devem ser os mesmos que você especificou quando carregou o certificado PFX (confira os pré-requisitos).</span><span class="sxs-lookup"><span data-stu-id="c3441-140">The **Subscription** and the **Location** must be same that you specified when you uploaded your PFX certificate (see Prerequisites).</span></span> <span data-ttu-id="c3441-141">Recomendamos que você crie um **grupo de recursos** para a implantação.</span><span class="sxs-lookup"><span data-stu-id="c3441-141">We recommend that you create a **Resource group** for the deployment.</span></span>

### <a name="step-2-specify-the-parameter-settings"></a><span data-ttu-id="c3441-142">Etapa 2: especificar as configurações de parâmetro</span><span class="sxs-lookup"><span data-stu-id="c3441-142">Step 2: Specify the parameter settings</span></span>

<span data-ttu-id="c3441-143">Digite ou modifique os valores dos parâmetros do modelo.</span><span class="sxs-lookup"><span data-stu-id="c3441-143">Enter or modify values for the template parameters.</span></span> <span data-ttu-id="c3441-144">Clique no ícone ao lado de cada parâmetro para obter informações de Ajuda.</span><span class="sxs-lookup"><span data-stu-id="c3441-144">Click the icon next to each parameter for help information.</span></span> <span data-ttu-id="c3441-145">Confira também as diretrizes sobre os [tamanhos de VM disponíveis](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="c3441-145">Also see the guidance for [available VM sizes](sizes.md).</span></span>

<span data-ttu-id="c3441-146">Especifique os valores registrados nos pré-requisitos para os seguintes parâmetros: **Nome do cofre**, **Grupo de recursos do cofre**, **URL do certificado** e **Impressão digital do certificado**.</span><span class="sxs-lookup"><span data-stu-id="c3441-146">Specify the values you recorded in the Prerequisites for the following parameters: **Vault name**, **Vault resource group**, **Certificate URL**, and **Certificate thumbprint**.</span></span>

### <a name="step-3-review-legal-terms-and-create"></a><span data-ttu-id="c3441-147">Etapa 3.</span><span class="sxs-lookup"><span data-stu-id="c3441-147">Step 3.</span></span> <span data-ttu-id="c3441-148">Examinar os termos legais e criar</span><span class="sxs-lookup"><span data-stu-id="c3441-148">Review legal terms and create</span></span>
<span data-ttu-id="c3441-149">Clique em **Examinar termos legais** para examinar os termos.</span><span class="sxs-lookup"><span data-stu-id="c3441-149">Click **Review legal terms** to review the terms.</span></span> <span data-ttu-id="c3441-150">Se você concordar, clique em **Comprar** e clique em **Criar** para iniciar a implantação.</span><span class="sxs-lookup"><span data-stu-id="c3441-150">If you agree, click **Purchase**, and then click **Create** to start the deployment.</span></span>

## <a name="connect-to-the-cluster"></a><span data-ttu-id="c3441-151">Conectar-se ao cluster</span><span class="sxs-lookup"><span data-stu-id="c3441-151">Connect to the cluster</span></span>
1. <span data-ttu-id="c3441-152">Depois que o cluster HPC Pack for implantado, vá para o [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c3441-152">After the HPC Pack cluster is deployed, go to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="c3441-153">Clique em **Grupos de recursos** e encontre o grupo de recursos no qual o cluster foi implantado.</span><span class="sxs-lookup"><span data-stu-id="c3441-153">Click **Resource groups**, and find the resource group in which the cluster was deployed.</span></span> <span data-ttu-id="c3441-154">Você pode encontrar as máquinas virtuais do nó de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="c3441-154">You can find the head node virtual machines.</span></span>

    ![Nós de cabeçalho de cluster no portal](./media/hpcpack-2016-cluster/clusterhns.png)

2. <span data-ttu-id="c3441-156">Clique em um nó de cabeçalho (em um cluster de alta disponibilidade, clique em qualquer um dos nós de cabeçalho).</span><span class="sxs-lookup"><span data-stu-id="c3441-156">Click one head node (in a high-availability cluster, click any of the head nodes).</span></span> <span data-ttu-id="c3441-157">Em **Essentials**, você pode encontrar o endereço IP público ou o nome DNS completo do cluster.</span><span class="sxs-lookup"><span data-stu-id="c3441-157">In **Essentials**, you can find the public IP address or full DNS name of the cluster.</span></span>

    ![Configurações de conexão do cluster](./media/hpcpack-2016-cluster/clusterconnect.png)

3. <span data-ttu-id="c3441-159">Clique em **Conectar** para fazer logon em um dos nós de cabeçalho usando a Área de Trabalho Remota com seu nome de usuário de administrador especificado.</span><span class="sxs-lookup"><span data-stu-id="c3441-159">Click **Connect** to log on to any of the head nodes using Remote Desktop with your specified administrator user name.</span></span> <span data-ttu-id="c3441-160">Se o cluster implantado estiver em um domínio do Active Directory, o nome de usuário estará no formato <privateDomainName>\<NomedeUsuárioAdmin > (por exemplo, hpc.local\hpcadmin).</span><span class="sxs-lookup"><span data-stu-id="c3441-160">If the cluster you deployed is in an Active Directory Domain, the user name is of the form <privateDomainName>\<adminUsername> (for example, hpc.local\hpcadmin).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3441-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c3441-161">Next steps</span></span>
* <span data-ttu-id="c3441-162">Envie trabalhos para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="c3441-162">Submit jobs to your cluster.</span></span> <span data-ttu-id="c3441-163">Confira [Enviar trabalhos para HPC e cluster HCP Pack no Azure](hpcpack-cluster-submit-jobs.md) e [Gerenciar um cluster HPC Pack 2016 no Azure usando o Azure Active Directory](hpcpack-cluster-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="c3441-163">See [Submit jobs to HPC an HPC Pack cluster in Azure](hpcpack-cluster-submit-jobs.md) and [Manage an HPC Pack 2016 cluster in Azure using Azure Active Directory](hpcpack-cluster-active-directory.md).</span></span>

