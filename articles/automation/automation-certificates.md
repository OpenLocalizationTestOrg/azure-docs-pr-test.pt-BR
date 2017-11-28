---
title: "ativos de aaaCertificate na automação do Azure | Microsoft Docs"
description: "Certificados podem ser armazenados com segurança na automação do Azure para que eles possam ser acessados por runbooks ou tooauthenticate de configurações DSC no Azure e os recursos de terceiros.  Este artigo explica detalhes de saudação de certificados e como toowork-los na criação de texto e gráfico."
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
ms.openlocfilehash: 2c25bee937890438ea9022669be2c24c77a110b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="certificate-assets-in-azure-automation"></a><span data-ttu-id="20686-104">Ativos de certificado na Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="20686-104">Certificate assets in Azure Automation</span></span>

<span data-ttu-id="20686-105">Certificados podem ser armazenados com segurança na automação do Azure para que eles possam ser acessados por runbooks ou configurações de DSC usando Olá **AzureRmAutomationRmCertificate Get** atividade para recursos do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="20686-105">Certificates can be stored securely in Azure Automation so they can be accessed by runbooks or DSC configurations using hello **Get-AzureRmAutomationRmCertificate** activity for Azure Resource Manager resources.</span></span> <span data-ttu-id="20686-106">Isso permite que você toocreate runbooks e as configurações de DSC que usam certificados para autenticação ou adiciona recursos tooAzure ou de terceiros.</span><span class="sxs-lookup"><span data-stu-id="20686-106">This allows you toocreate runbooks and DSC configurations that use certificates for authentication or adds them tooAzure or third party resources.</span></span>

> [!NOTE] 
> <span data-ttu-id="20686-107">Os ativos protegidos na Automação do Azure incluem credenciais, certificados, conexões e variáveis criptografadas.</span><span class="sxs-lookup"><span data-stu-id="20686-107">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="20686-108">Esses ativos são criptografados e armazenados em Olá automação do Azure usando uma chave exclusiva que é gerada para cada conta de automação.</span><span class="sxs-lookup"><span data-stu-id="20686-108">These assets are encrypted and stored in hello Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="20686-109">Essa chave é criptografada por um certificado mestre e armazenada na Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="20686-109">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="20686-110">Antes de armazenar um ativo seguro, chave Olá para conta de automação de saudação é descriptografado usando certificado mestre hello e usado tooencrypt ativo de saudação.</span><span class="sxs-lookup"><span data-stu-id="20686-110">Before storing a secure asset, hello key for hello automation account is decrypted using hello master certificate and then used tooencrypt hello asset.</span></span>
> 

## <a name="windows-powershell-cmdlets"></a><span data-ttu-id="20686-111">Cmdlets do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="20686-111">Windows PowerShell Cmdlets</span></span>

<span data-ttu-id="20686-112">cmdlets Olá Olá a tabela a seguir são usada toocreate e gerenciar ativos de certificado de automação com o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="20686-112">hello cmdlets in hello following table are used toocreate and manage automation certificate assets with Windows PowerShell.</span></span> <span data-ttu-id="20686-113">Eles são fornecidos como parte da saudação [módulo Azure PowerShell](../powershell-install-configure.md) que está disponível para uso em runbooks de automação e configurações de DSC.</span><span class="sxs-lookup"><span data-stu-id="20686-113">They ship as part of hello [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configurations.</span></span>

|<span data-ttu-id="20686-114">Cmdlets</span><span class="sxs-lookup"><span data-stu-id="20686-114">Cmdlets</span></span>|<span data-ttu-id="20686-115">Descrição</span><span class="sxs-lookup"><span data-stu-id="20686-115">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="20686-116">Get-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="20686-116">Get-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603765.aspx)|<span data-ttu-id="20686-117">Recupera informações sobre toouse um certificado em um runbook ou a configuração DSC.</span><span class="sxs-lookup"><span data-stu-id="20686-117">Retrieves information about a certificate toouse in a runbook or DSC configuration.</span></span> <span data-ttu-id="20686-118">Você só pode recuperar o certificado de saudação da atividade de Get-AutomationCertificate.</span><span class="sxs-lookup"><span data-stu-id="20686-118">You can only retrieve hello certificate itself from Get-AutomationCertificate activity.</span></span>|
|[<span data-ttu-id="20686-119">New-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="20686-119">New-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603604.aspx)|<span data-ttu-id="20686-120">Cria um novo certificado para a Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="20686-120">Creates a new certificate into Azure Automation.</span></span>|
[<span data-ttu-id="20686-121">Remove-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="20686-121">Remove-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603529.aspx)|<span data-ttu-id="20686-122">Remove um certificado da Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="20686-122">Removes a certificate from Azure Automation.</span></span>|<span data-ttu-id="20686-123">Cria um novo certificado para a Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="20686-123">Creates a new certificate into Azure Automation.</span></span>
|[<span data-ttu-id="20686-124">Set-AzureRmAutomationCertificate</span><span class="sxs-lookup"><span data-stu-id="20686-124">Set-AzureRmAutomationCertificate</span></span>](https://msdn.microsoft.com/library/mt603760.aspx)|<span data-ttu-id="20686-125">Define as propriedades de saudação para um certificado existente, incluindo o carregamento de arquivo de certificado hello e a senha de saudação de configuração para um. pfx.</span><span class="sxs-lookup"><span data-stu-id="20686-125">Sets hello properties for an existing certificate including uploading hello certificate file and setting hello password for a .pfx.</span></span>|
|[<span data-ttu-id="20686-126">Add-AzureCertificate</span><span class="sxs-lookup"><span data-stu-id="20686-126">Add-AzureCertificate</span></span>](https://msdn.microsoft.com/library/azure/dn495214.aspx)|<span data-ttu-id="20686-127">Carrega um serviço de certificado para Olá especificado serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="20686-127">Uploads a service certificate for hello specified cloud service.</span></span>|


## <a name="creating-a-new-certificate"></a><span data-ttu-id="20686-128">Criando um novo certificado</span><span class="sxs-lookup"><span data-stu-id="20686-128">Creating a new certificate</span></span>

<span data-ttu-id="20686-129">Quando você cria um novo certificado, você pode carregar um tooAzure de arquivo. cer ou. pfx automação.</span><span class="sxs-lookup"><span data-stu-id="20686-129">When you create a new certificate, you upload a .cer or .pfx file tooAzure Automation.</span></span> <span data-ttu-id="20686-130">Se você marcar certificado hello como exportável, você pode transferi-lo fora do repositório de certificados de automação do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="20686-130">If you mark hello certificate as exportable, then you can transfer it out of hello Azure Automation certificate store.</span></span> <span data-ttu-id="20686-131">Se não for exportável, ele pode apenas ser usado para assinatura no runbook hello ou configuração de DSC.</span><span class="sxs-lookup"><span data-stu-id="20686-131">If it is not exportable, then it can only be used for signing within hello runbook or DSC configuration.</span></span>


### <a name="toocreate-a-new-certificate-with-hello-azure-portal"></a><span data-ttu-id="20686-132">toocreate um novo certificado com hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="20686-132">toocreate a new certificate with hello Azure portal</span></span>

1. <span data-ttu-id="20686-133">Na sua conta de automação, clique em Olá **ativos** bloco tooopen Olá **ativos** folha.</span><span class="sxs-lookup"><span data-stu-id="20686-133">From your Automation account, click hello **Assets** tile tooopen hello **Assets** blade.</span></span>
1. <span data-ttu-id="20686-134">Clique em Olá **certificados** bloco tooopen Olá **certificados** folha.</span><span class="sxs-lookup"><span data-stu-id="20686-134">Click hello **Certificates** tile tooopen hello **Certificates** blade.</span></span>
1. <span data-ttu-id="20686-135">Clique em **adicionar um certificado** na parte superior de saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="20686-135">Click **Add a certificate** at hello top of hello blade.</span></span>
2. <span data-ttu-id="20686-136">Digite um nome para o certificado de saudação Olá **nome** caixa.</span><span class="sxs-lookup"><span data-stu-id="20686-136">Type a name for hello certificate in hello **Name** box.</span></span>
2. <span data-ttu-id="20686-137">Clique em **selecionar um arquivo** em **carregar um arquivo de certificado** toobrowse para um arquivo. cer ou. pfx.</span><span class="sxs-lookup"><span data-stu-id="20686-137">Click **Select a file** under **Upload a certificate file** toobrowse for a .cer or .pfx file.</span></span>  <span data-ttu-id="20686-138">Se você selecionar um arquivo. pfx, especifique uma senha e se ele deve ter permissão toobe exportado.</span><span class="sxs-lookup"><span data-stu-id="20686-138">If you select a .pfx file, specify a password and whether it should be allowed toobe exported.</span></span>
1. <span data-ttu-id="20686-139">Clique em **criar** toosave Olá novo certificado ativo.</span><span class="sxs-lookup"><span data-stu-id="20686-139">Click **Create** toosave hello new certificate asset.</span></span>


### <a name="toocreate-a-new-certificate-with-windows-powershell"></a><span data-ttu-id="20686-140">toocreate um novo certificado com o Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="20686-140">toocreate a new certificate with Windows PowerShell</span></span>

<span data-ttu-id="20686-141">Olá exemplo a seguir demonstra como toocreate automação uma novo certificado e marcá-la exportável.</span><span class="sxs-lookup"><span data-stu-id="20686-141">hello following example demonstrates how toocreate a new Automation certificate and mark it exportable.</span></span> <span data-ttu-id="20686-142">Isso importa um arquivo .pfx existente.</span><span class="sxs-lookup"><span data-stu-id="20686-142">This imports an existing .pfx file.</span></span>

    $certName = 'MyCertificate'
    $certPath = '.\MyCert.pfx'
    $certPwd = ConvertTo-SecureString -String 'P@$$w0rd' -AsPlainText -Force
    $ResourceGroup = "ResourceGroup01"
    
    New-AzureRmAutomationCertificate -AutomationAccountName "MyAutomationAccount" -Name $certName -Path $certPath –Password $certPwd -Exportable -ResourceGroupName $ResourceGroup

## <a name="using-a-certificate"></a><span data-ttu-id="20686-143">Usando um certificado</span><span class="sxs-lookup"><span data-stu-id="20686-143">Using a certificate</span></span>

<span data-ttu-id="20686-144">Você deve usar o hello **Get-AutomationCertificate** toouse de atividade um certificado.</span><span class="sxs-lookup"><span data-stu-id="20686-144">You must use hello **Get-AutomationCertificate** activity toouse a certificate.</span></span> <span data-ttu-id="20686-145">Você não pode usar o hello [AzureRmAutomationCertificate Get](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet desde que ele retorna informações sobre o ativo de certificado hello, mas não Olá próprio certificado.</span><span class="sxs-lookup"><span data-stu-id="20686-145">You cannot use hello [Get-AzureRmAutomationCertificate](https://msdn.microsoft.com/library/mt603765.aspx) cmdlet since it returns information about hello certificate asset but not hello certificate itself.</span></span>

### <a name="textual-runbook-sample"></a><span data-ttu-id="20686-146">Exemplo de runbook textual</span><span class="sxs-lookup"><span data-stu-id="20686-146">Textual runbook sample</span></span>

<span data-ttu-id="20686-147">Olá, código de exemplo a seguir mostra como o serviço em um runbook de nuvem tooadd tooa um certificado.</span><span class="sxs-lookup"><span data-stu-id="20686-147">hello following sample code shows how tooadd a certificate tooa cloud service in a runbook.</span></span> <span data-ttu-id="20686-148">Neste exemplo, a senha Olá é recuperada de uma variável de automação criptografada.</span><span class="sxs-lookup"><span data-stu-id="20686-148">In this sample, hello password is retrieved from an encrypted automation variable.</span></span>

    $serviceName = 'MyCloudService'
    $cert = Get-AutomationCertificate -Name 'MyCertificate'
    $certPwd = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyCertPassword'
    Add-AzureCertificate -ServiceName $serviceName -CertToDeploy $cert

### <a name="graphical-runbook-sample"></a><span data-ttu-id="20686-149">Exemplo de runbook gráfico</span><span class="sxs-lookup"><span data-stu-id="20686-149">Graphical runbook sample</span></span>

<span data-ttu-id="20686-150">Adicionar um **Get-AutomationCertificate** tooa runbook gráfico clicando no certificado de saudação no painel de biblioteca de saudação do editor gráfico hello e selecionando **adicionar toocanvas**.</span><span class="sxs-lookup"><span data-stu-id="20686-150">You add a **Get-AutomationCertificate** tooa graphical runbook by right-clicking on hello certificate in hello Library pane of hello graphical editor and selecting **Add toocanvas**.</span></span>

![Adicionar certificado toohello tela](media/automation-certificates/automation-certificate-add-to-canvas.png)

<span data-ttu-id="20686-152">Olá imagem a seguir mostra um exemplo de como usar um certificado em um runbook gráfico.</span><span class="sxs-lookup"><span data-stu-id="20686-152">hello following image shows an example of using a certificate in a graphical runbook.</span></span>  <span data-ttu-id="20686-153">Isso é hello mesmo exemplo mostrado acima para adicionar um serviço de nuvem tooa certificado de um runbook textual.</span><span class="sxs-lookup"><span data-stu-id="20686-153">This is hello same example shown above for adding a certificate tooa cloud service from a textual runbook.</span></span>

![<span data-ttu-id="20686-154">Exemplo de criação gráfica</span><span class="sxs-lookup"><span data-stu-id="20686-154">Example Graphical Authoring</span></span> ](media/automation-certificates/graphical-runbook-add-certificate.png)


## <a name="next-steps"></a><span data-ttu-id="20686-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="20686-155">Next steps</span></span>

- <span data-ttu-id="20686-156">toolearn mais sobre como trabalhar com o fluxo lógico de saudação do toocontrol de links de atividades de runbook é projetado tooperform, consulte [Links no gráfico de criação](automation-graphical-authoring-intro.md#links-and-workflow).</span><span class="sxs-lookup"><span data-stu-id="20686-156">toolearn more about working with links toocontrol hello logical flow of activities your runbook is designed tooperform, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow).</span></span> 
