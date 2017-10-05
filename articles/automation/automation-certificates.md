---
title: "Ativos de certificado na Automação do Azure | Microsoft Docs"
description: "Os certificados podem ser armazenados com segurança na Automação do Azure para que possam ser acessados pelos runbooks ou pelas configurações DSC para serem autenticados em recursos do Azure e de terceiros.  Este artigo explica os detalhes de certificados e como trabalhar com elas na criação textual e gráfica."
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: ac9c22ae-501f-42b9-9543-ac841cf2cc36
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/19/2016
ms.author: magoedte;bwren
ms.openlocfilehash: fd1737a420c132dace9307436bfea98a9bde94a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="certificate-assets-in-azure-automation"></a><span data-ttu-id="7c8b7-104">Ativos de certificado na Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="7c8b7-104">Certificate assets in Azure Automation</span></span>

<span data-ttu-id="7c8b7-105">Os certificados podem ser armazenados com segurança na Automação do Azure para que possam ser acessados pelos runbooks ou pelas configurações DSC usando a atividade **Get-AzureRmAutomationRmCertificate** para recursos do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7c8b7-105">Certificates can be stored securely in Azure Automation so they can be accessed by runbooks or DSC configurations using the **Get-AzureRmAutomationRmCertificate** activity for Azure Resource Manager resources.</span></span> <span data-ttu-id="7c8b7-106">Isso permite criar runbooks e configurações DSC que usam certificados para autenticação ou adicioná-los a recursos do Azure ou de terceiros.</span><span class="sxs-lookup"><span data-stu-id="7c8b7-106">This allows you to create runbooks and DSC configurations that use certificates for authentication or adds them to Azure or third party resources.</span></span>

> [!NOTE] 
> <span data-ttu-id="7c8b7-107">Os ativos protegidos na Automação do Azure incluem credenciais, certificados, conexões e variáveis criptografadas.</span><span class="sxs-lookup"><span data-stu-id="7c8b7-107">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="7c8b7-108">Esses ativos são criptografados e armazenados na Automação do Azure usando uma chave exclusiva que é gerada para cada conta de automação.</span><span class="sxs-lookup"><span data-stu-id="7c8b7-108">These assets are encrypted and stored in the Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="7c8b7-109">Essa chave é criptografada por um certificado mestre e armazenada na Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="7c8b7-109">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="7c8b7-110">Antes de armazenar um ativo seguro, a chave para a conta de automação é descriptografada usando o certificado mestre e usada para criptografar o ativo.</span><span class="sxs-lookup"><span data-stu-id="7c8b7-110">Before storing a secure asset, the key for the automation account is decrypted using the master certificate and then used to encrypt the asset.</span></span>
> 

## <a name="windows-powershell-cmdlets"></a><span data-ttu-id="7c8b7-111">Cmdlets do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="7c8b7-111">Windows PowerShell Cmdlets</span></span>

<span data-ttu-id="7c8b7-112">Os cmdlets na tabela a seguir são usados para criar e gerenciar ativos de certificados de automação com o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7c8b7-112">The cmdlets in the following table are used to create and manage automation certificate assets with Windows PowerShell.</span></span> <span data-ttu-id="7c8b7-113">Eles são fornecidos como parte do [módulo do Azure PowerShell](../powershell-install-configure.md) que está disponível para uso em runbooks e na configuração DSC da Automação.</span><span class="sxs-lookup"><span data-stu-id="7c8b7-113">They ship as part of the [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configurations.</span></span>

|<span data-ttu-id="7c8b7-114">Cmdlets</span><span class="sxs-lookup"><span data-stu-id="7c8b7-114">Cmdlets</span></span>|<span data-ttu-id="7c8b7-115">Descrição</span><span class="sxs-lookup"><span data-stu-id="7c8b7-115">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="7c8b7-116">Get-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="7c8b7-116">Get-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603765.aspx)|<span data-ttu-id="7c8b7-117">Obtém informações sobre um certificado a ser usado em um runbook ou configuração DSC.</span><span class="sxs-lookup"><span data-stu-id="7c8b7-117">Retrieves information about a certificate to use in a runbook or DSC configuration.</span></span> <span data-ttu-id="7c8b7-118">Você só pode recuperar o certificado propriamente dito da atividade Get-AutomationCertificate.</span><span class="sxs-lookup"><span data-stu-id="7c8b7-118">You can only retrieve the certificate itself from Get-AutomationCertificate activity.</span></span>|
|[<span data-ttu-id="7c8b7-119">New-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="7c8b7-119">New-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603604.aspx)|<span data-ttu-id="7c8b7-120">Cria um novo certificado para a Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="7c8b7-120">Creates a new certificate into Azure Automation.</span></span>|
[<span data-ttu-id="7c8b7-121">Remove-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="7c8b7-121">Remove-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603529.aspx)|<span data-ttu-id="7c8b7-122">Remove um certificado da Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="7c8b7-122">Removes a certificate from Azure Automation.</span></span>|<span data-ttu-id="7c8b7-123">Cria um novo certificado para a Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="7c8b7-123">Creates a new certificate into Azure Automation.</span></span>
|[<span data-ttu-id="7c8b7-124">Set-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="7c8b7-124">Set-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603760.aspx)|<span data-ttu-id="7c8b7-125">Define as propriedades para um certificado existente, incluindo o carregamento do arquivo de certificado e a definição da senha para um. pfx.</span><span class="sxs-lookup"><span data-stu-id="7c8b7-125">Sets the properties for an existing certificate including uploading the certificate file and setting the password for a .pfx.</span></span>|
|[<span data-ttu-id="7c8b7-126">Add-AzureCertificate</span><span class="sxs-lookup"><span data-stu-id="7c8b7-126">Add-AzureCertificate</span></span>](https://msdn.microsoft.com/library/azure/dn495214.aspx)|<span data-ttu-id="7c8b7-127">Carrega um certificado de serviço para o serviço de nuvem especificado.</span><span class="sxs-lookup"><span data-stu-id="7c8b7-127">Uploads a service certificate for the specified cloud service.</span></span>|


## <a name="creating-a-new-certificate"></a><span data-ttu-id="7c8b7-128">Criando um novo certificado</span><span class="sxs-lookup"><span data-stu-id="7c8b7-128">Creating a new certificate</span></span>

<span data-ttu-id="7c8b7-129">Ao criar um novo certificado, você carrega um arquivo .cer ou .pfx na Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="7c8b7-129">When you create a new certificate, you upload a .cer or .pfx file to Azure Automation.</span></span> <span data-ttu-id="7c8b7-130">Se marcar certificado como exportável, você poderá transferi-lo do repositório de certificados da Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="7c8b7-130">If you mark the certificate as exportable, then you can transfer it out of the Azure Automation certificate store.</span></span> <span data-ttu-id="7c8b7-131">Se ele não for exportável, ele só poderá ser usado para a assinatura no runbook ou na configuração DSC.</span><span class="sxs-lookup"><span data-stu-id="7c8b7-131">If it is not exportable, then it can only be used for signing within the runbook or DSC configuration.</span></span>


### <a name="to-create-a-new-certificate-with-the-azure-portal"></a><span data-ttu-id="7c8b7-132">Para criar um novo certificado com o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7c8b7-132">To create a new certificate with the Azure portal</span></span>

1. <span data-ttu-id="7c8b7-133">Na sua conta de automação, clique no bloco **Ativos** para abrir a folha **Ativos**.</span><span class="sxs-lookup"><span data-stu-id="7c8b7-133">From your Automation account, click the **Assets** tile to open the **Assets** blade.</span></span>
1. <span data-ttu-id="7c8b7-134">Clique no bloco **Certificados** para abrir a folha **Certificados**.</span><span class="sxs-lookup"><span data-stu-id="7c8b7-134">Click the **Certificates** tile to open the **Certificates** blade.</span></span>
1. <span data-ttu-id="7c8b7-135">Clique em **Adicionar um certificado** na parte superior da folha.</span><span class="sxs-lookup"><span data-stu-id="7c8b7-135">Click **Add a certificate** at the top of the blade.</span></span>
2. <span data-ttu-id="7c8b7-136">Digite um nome para o certificado na caixa **Nome** .</span><span class="sxs-lookup"><span data-stu-id="7c8b7-136">Type a name for the certificate in the **Name** box.</span></span>
2. <span data-ttu-id="7c8b7-137">Clique em **Selecionar um arquivo** em **Carregar um arquivo de certificado** para procurar um arquivo .cer ou .pfx.</span><span class="sxs-lookup"><span data-stu-id="7c8b7-137">Click **Select a file** under **Upload a certificate file** to browse for a .cer or .pfx file.</span></span>  <span data-ttu-id="7c8b7-138">Se você selecionar um arquivo .pfx, especifique uma senha e se ele deve ter permissão para ser exportado.</span><span class="sxs-lookup"><span data-stu-id="7c8b7-138">If you select a .pfx file, specify a password and whether it should be allowed to be exported.</span></span>
1. <span data-ttu-id="7c8b7-139">Clique em **Criar** para salvar o novo ativo de certificado.</span><span class="sxs-lookup"><span data-stu-id="7c8b7-139">Click **Create** to save the new certificate asset.</span></span>


### <a name="to-create-a-new-certificate-with-windows-powershell"></a><span data-ttu-id="7c8b7-140">Para criar um novo certificado com o Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="7c8b7-140">To create a new certificate with Windows PowerShell</span></span>

<span data-ttu-id="7c8b7-141">O exemplo a seguir mostra como criar um novo Certificado de automação e marcá-lo como exportável.</span><span class="sxs-lookup"><span data-stu-id="7c8b7-141">The following example demonstrates how to create a new Automation certificate and mark it exportable.</span></span> <span data-ttu-id="7c8b7-142">Isso importa um arquivo .pfx existente.</span><span class="sxs-lookup"><span data-stu-id="7c8b7-142">This imports an existing .pfx file.</span></span>

    $certName = 'MyCertificate'
    $certPath = '.\MyCert.pfx'
    $certPwd = ConvertTo-SecureString -String 'P@$$w0rd' -AsPlainText -Force
    $ResourceGroup = "ResourceGroup01"
    
    New-AzureRmAutomationCertificate -AutomationAccountName "MyAutomationAccount" -Name $certName -Path $certPath –Password $certPwd -Exportable -ResourceGroupName $ResourceGroup

## <a name="using-a-certificate"></a><span data-ttu-id="7c8b7-143">Usando um certificado</span><span class="sxs-lookup"><span data-stu-id="7c8b7-143">Using a certificate</span></span>

<span data-ttu-id="7c8b7-144">Você deve usar a atividade **Get-AutomationCertificate** para usar um certificado.</span><span class="sxs-lookup"><span data-stu-id="7c8b7-144">You must use the **Get-AutomationCertificate** activity to use a certificate.</span></span> <span data-ttu-id="7c8b7-145">Não é possível usar o cmdlet [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx), pois ele retorna informações sobre o ativo de certificado, mas não sobre o próprio certificado.</span><span class="sxs-lookup"><span data-stu-id="7c8b7-145">You cannot use the [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet since it returns information about the certificate asset but not the certificate itself.</span></span>

### <a name="textual-runbook-sample"></a><span data-ttu-id="7c8b7-146">Exemplo de runbook textual</span><span class="sxs-lookup"><span data-stu-id="7c8b7-146">Textual runbook sample</span></span>

<span data-ttu-id="7c8b7-147">O código de exemplo a seguir mostra como adicionar um certificado a um serviço de nuvem em um runbook.</span><span class="sxs-lookup"><span data-stu-id="7c8b7-147">The following sample code shows how to add a certificate to a cloud service in a runbook.</span></span> <span data-ttu-id="7c8b7-148">Nesse exemplo, a senha é recuperada de uma variável de automação criptografada.</span><span class="sxs-lookup"><span data-stu-id="7c8b7-148">In this sample, the password is retrieved from an encrypted automation variable.</span></span>

    $serviceName = 'MyCloudService'
    $cert = Get-AutomationCertificate -Name 'MyCertificate'
    $certPwd = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyCertPassword'
    Add-AzureCertificate -ServiceName $serviceName -CertToDeploy $cert

### <a name="graphical-runbook-sample"></a><span data-ttu-id="7c8b7-149">Exemplo de runbook gráfico</span><span class="sxs-lookup"><span data-stu-id="7c8b7-149">Graphical runbook sample</span></span>

<span data-ttu-id="7c8b7-150">Você adiciona **Get-AutomationCertificate** a um runbook gráfico clicando com o botão direito no certificado no painel Biblioteca do editor gráfico e selecionando **Adicionar à tela**.</span><span class="sxs-lookup"><span data-stu-id="7c8b7-150">You add a **Get-AutomationCertificate** to a graphical runbook by right-clicking on the certificate in the Library pane of the graphical editor and selecting **Add to canvas**.</span></span>

![Adicionar certificado à tela](media/automation-certificates/automation-certificate-add-to-canvas.png)

<span data-ttu-id="7c8b7-152">A imagem a seguir mostra um exemplo do uso de um certificado em um runbook gráfico.</span><span class="sxs-lookup"><span data-stu-id="7c8b7-152">The following image shows an example of using a certificate in a graphical runbook.</span></span>  <span data-ttu-id="7c8b7-153">Esse é o mesmo exemplo mostrado acima para adicionar um certificado a um serviço de nuvem de um runbook textual.</span><span class="sxs-lookup"><span data-stu-id="7c8b7-153">This is the same example shown above for adding a certificate to a cloud service from a textual runbook.</span></span>

![<span data-ttu-id="7c8b7-154">Exemplo de criação gráfica</span><span class="sxs-lookup"><span data-stu-id="7c8b7-154">Example Graphical Authoring</span></span> ](media/automation-certificates/graphical-runbook-add-certificate.png)


## <a name="next-steps"></a><span data-ttu-id="7c8b7-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7c8b7-155">Next steps</span></span>

- <span data-ttu-id="7c8b7-156">Para saber mais sobre como trabalhar com links para controlar o fluxo lógico de atividades que o seu runbook é projetado para realizar, consulte [Links na criação gráfica](automation-graphical-authoring-intro.md#links-and-workflow).</span><span class="sxs-lookup"><span data-stu-id="7c8b7-156">To learn more about working with links to control the logical flow of activities your runbook is designed to perform, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow).</span></span> 
