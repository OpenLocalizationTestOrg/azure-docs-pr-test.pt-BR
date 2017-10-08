---
title: "ativos de aaaVariable na automação do Azure | Microsoft Docs"
description: "Os ativos de variável são valores que estão disponíveis tooall runbooks e as configurações de DSC na automação do Azure.  Este artigo explica detalhes de saudação de variáveis e como toowork-los na criação de texto e gráfico."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: b880c15f-46f5-4881-8e98-e034cc5a66ec
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/09/2017
ms.author: magoedte;bwren
ms.openlocfilehash: f9daa49fc1dc883ffb218a9adf26e36df1d6bb27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="variable-assets-in-azure-automation"></a><span data-ttu-id="0c8a8-104">Ativos variáveis na Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="0c8a8-104">Variable assets in Azure Automation</span></span>

<span data-ttu-id="0c8a8-105">Os ativos de variável são valores que estão disponíveis tooall runbooks e as configurações de DSC em sua conta de automação.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-105">Variable assets are values that are available tooall runbooks and DSC configurations in your automation account.</span></span> <span data-ttu-id="0c8a8-106">Eles podem ser criados, modificados e recuperados de saudação portal do Azure, Windows PowerShell e de um runbook ou a configuração DSC.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-106">They can be created, modified, and retrieved from hello Azure portal, Windows PowerShell, and from within a runbook or DSC configuration.</span></span> <span data-ttu-id="0c8a8-107">Variáveis de automação são úteis para Olá os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="0c8a8-107">Automation variables are useful for hello following scenarios:</span></span>

- <span data-ttu-id="0c8a8-108">Compartilhe um valor entre vários runbooks ou configurações DSC.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-108">Share a value between multiple runbooks or DSC configurations.</span></span>

- <span data-ttu-id="0c8a8-109">Compartilhar um valor entre vários trabalhos do hello mesmo runbook ou a configuração DSC.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-109">Share a value between multiple jobs from hello same runbook or DSC configuration.</span></span>

- <span data-ttu-id="0c8a8-110">Gerencie um valor no portal de saudação ou na linha de comando do Windows PowerShell Olá é usada por runbooks ou configurações de DSC, como um conjunto de itens de configuração comuns como lista específica de nomes de VM, um grupo de recursos específico, um nome de domínio do AD, etc.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-110">Manage a value from hello portal or from hello Windows PowerShell command line that is used by runbooks or DSC configurations, such as a set of common configuration items like specific list of VM names, a specific resource group,  an AD domain name, etc.</span></span>  

<span data-ttu-id="0c8a8-111">Variáveis de automação são mantidas para que continuem toobe disponível mesmo se houver falha Olá runbook ou a configuração DSC.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-111">Automation variables are persisted so that they continue toobe available even if hello runbook or DSC configuration fails.</span></span>  <span data-ttu-id="0c8a8-112">Isso também permite que um toobe valor definido por um runbook que é usado por outro, ou é usado por Olá mesmo runbook ou saudação de configuração DSC próxima vez que ele é executado.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-112">This also allows a value toobe set by one runbook that is then used by another, or is used by hello same runbook or DSC configuration hello next time that it is run.</span></span>

<span data-ttu-id="0c8a8-113">Quando uma variável é criada, você pode definir que ele seja armazenado criptografado.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-113">When a variable is created, you can specify that it be stored encrypted.</span></span>  <span data-ttu-id="0c8a8-114">Quando uma variável é criptografada, ela é armazenada com segurança na automação do Azure e seu valor não pode ser recuperado da saudação [AzureRmAutomationVariable Get](https://msdn.microsoft.com/library/mt603849.aspx) cmdlet que é fornecido como parte do módulo do PowerShell do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-114">When a variable is encrypted, it is stored securely in Azure Automation, and its value cannot be retrieved from hello [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) cmdlet that ships as part of hello Azure PowerShell module.</span></span>  <span data-ttu-id="0c8a8-115">Olá única maneira de recuperar um valor criptografado é de saudação **Get-AutomationVariable** atividade em um runbook ou a configuração DSC.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-115">hello only way that an encrypted value can be retrieved is from hello **Get-AutomationVariable** activity in a runbook or DSC configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="0c8a8-116">Os ativos protegidos na Automação do Azure incluem credenciais, certificados, conexões e variáveis criptografadas.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-116">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="0c8a8-117">Esses ativos são criptografados e armazenados em Olá automação do Azure usando uma chave exclusiva que é gerada para cada conta de automação.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-117">These assets are encrypted and stored in hello Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="0c8a8-118">Essa chave é criptografada por um certificado mestre e armazenada na Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-118">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="0c8a8-119">Antes de armazenar um ativo seguro, chave Olá para conta de automação de saudação é descriptografado usando certificado mestre hello e usado tooencrypt ativo de saudação.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-119">Before storing a secure asset, hello key for hello automation account is decrypted using hello master certificate and then used tooencrypt hello asset.</span></span>

## <a name="variable-types"></a><span data-ttu-id="0c8a8-120">Tipos de variável</span><span class="sxs-lookup"><span data-stu-id="0c8a8-120">Variable types</span></span>

<span data-ttu-id="0c8a8-121">Quando você cria uma variável com hello portal do Azure, você deve especificar um tipo de dados na lista suspensa de saudação para que portal Olá possa exibir o controle apropriado de saudação para inserir o valor da variável hello.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-121">When you create a variable with hello Azure portal, you must specify a data type from hello drop-down list so hello portal can display hello appropriate control for entering hello variable value.</span></span> <span data-ttu-id="0c8a8-122">Olá variável não é restrito toothis dados tipo, mas você deve definir variável de saudação usando o Windows PowerShell se você quiser toospecify um valor de um tipo diferente.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-122">hello variable is not restricted toothis data type, but you must set hello variable using Windows PowerShell if you want toospecify a value of a different type.</span></span> <span data-ttu-id="0c8a8-123">Se você especificar **não definido**, valor variável Olá Olá será definido muito**$null**, e você deve definir o valor de saudação com hello [Set-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) cmdlet ou **Set-AutomationVariable** atividade.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-123">If you specify **Not defined**, then hello value of hello variable will be set too**$null**, and you must set hello value with hello [Set-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) cmdlet or **Set-AutomationVariable** activity.</span></span>  <span data-ttu-id="0c8a8-124">Não é possível criar ou alterar o valor de saudação para um tipo complexo de variável no portal de saudação, mas você pode fornecer um valor de qualquer tipo usando o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-124">You cannot create or change hello value for a complex variable type in hello portal, but you can provide a value of any type using Windows PowerShell.</span></span> <span data-ttu-id="0c8a8-125">Tipos complexos serão retornados como um [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).</span><span class="sxs-lookup"><span data-stu-id="0c8a8-125">Complex types will be returned as a [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).</span></span>

<span data-ttu-id="0c8a8-126">Você pode armazenar vários valores tooa única variável criando uma matriz ou tabela de hash e salvando-o toohello variável.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-126">You can store multiple values tooa single variable by creating an array or hashtable and saving it toohello variable.</span></span>

<span data-ttu-id="0c8a8-127">Olá seguem uma lista de tipos de variáveis disponíveis na automação:</span><span class="sxs-lookup"><span data-stu-id="0c8a8-127">hello following are a list of variable types available in Automation:</span></span>

* <span data-ttu-id="0c8a8-128">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0c8a8-128">String</span></span>
* <span data-ttu-id="0c8a8-129">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="0c8a8-129">Integer</span></span>
* <span data-ttu-id="0c8a8-130">DateTime</span><span class="sxs-lookup"><span data-stu-id="0c8a8-130">DateTime</span></span>
* <span data-ttu-id="0c8a8-131">Booliano</span><span class="sxs-lookup"><span data-stu-id="0c8a8-131">Boolean</span></span>
* <span data-ttu-id="0c8a8-132">Nulo</span><span class="sxs-lookup"><span data-stu-id="0c8a8-132">Null</span></span>

## <a name="cmdlets-and-workflow-activities"></a><span data-ttu-id="0c8a8-133">Atividades de fluxo de trabalho e cmdlets</span><span class="sxs-lookup"><span data-stu-id="0c8a8-133">Cmdlets and workflow activities</span></span>

<span data-ttu-id="0c8a8-134">cmdlets Olá Olá a tabela a seguir são usada toocreate e gerenciar variáveis de automação com o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-134">hello cmdlets in hello following table are used toocreate and manage Automation variables with Windows PowerShell.</span></span> <span data-ttu-id="0c8a8-135">Eles são fornecidos como parte da saudação [módulo Azure PowerShell](../powershell-install-configure.md) que está disponível para uso em runbooks de automação e a configuração de DSC.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-135">They ship as part of hello [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configuration.</span></span>

|<span data-ttu-id="0c8a8-136">Cmdlets</span><span class="sxs-lookup"><span data-stu-id="0c8a8-136">Cmdlets</span></span>|<span data-ttu-id="0c8a8-137">Descrição</span><span class="sxs-lookup"><span data-stu-id="0c8a8-137">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="0c8a8-138">Get-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="0c8a8-138">Get-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603849.aspx)|<span data-ttu-id="0c8a8-139">Recupera o valor de saudação de uma variável existente.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-139">Retrieves hello value of an existing variable.</span></span>|
|[<span data-ttu-id="0c8a8-140">New-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="0c8a8-140">New-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603613.aspx)|<span data-ttu-id="0c8a8-141">Cria uma nova variável e define o seu valor.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-141">Creates a new variable and sets its value.</span></span>|
|[<span data-ttu-id="0c8a8-142">Remove-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="0c8a8-142">Remove-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt619354.aspx)|<span data-ttu-id="0c8a8-143">Remove uma variável existente.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-143">Removes an existing variable.</span></span>|
|[<span data-ttu-id="0c8a8-144">Set-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="0c8a8-144">Set-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603601.aspx)|<span data-ttu-id="0c8a8-145">Define o valor de saudação de uma variável existente.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-145">Sets hello value for an existing variable.</span></span>|

<span data-ttu-id="0c8a8-146">atividades de fluxo de trabalho de saudação em Olá a tabela a seguir são usadas tooaccess variáveis de automação em um runbook.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-146">hello workflow activities in hello following table are used tooaccess Automation variables in a runbook.</span></span> <span data-ttu-id="0c8a8-147">Eles só estão disponíveis para uso em um runbook ou a configuração DSC e não são fornecidas como parte do módulo do PowerShell do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-147">They are only available for use in a runbook or DSC configuration, and do not ship as part of hello Azure PowerShell module.</span></span>

|<span data-ttu-id="0c8a8-148">Atividades de fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="0c8a8-148">Workflow Activities</span></span>|<span data-ttu-id="0c8a8-149">Descrição</span><span class="sxs-lookup"><span data-stu-id="0c8a8-149">Description</span></span>|
|:---|:---|
|<span data-ttu-id="0c8a8-150">Get-AutomationVariable</span><span class="sxs-lookup"><span data-stu-id="0c8a8-150">Get-AutomationVariable</span></span>|<span data-ttu-id="0c8a8-151">Recupera o valor de saudação de uma variável existente.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-151">Retrieves hello value of an existing variable.</span></span>|
|<span data-ttu-id="0c8a8-152">Set-AutomationVariable</span><span class="sxs-lookup"><span data-stu-id="0c8a8-152">Set-AutomationVariable</span></span>|<span data-ttu-id="0c8a8-153">Define o valor de saudação de uma variável existente.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-153">Sets hello value for an existing variable.</span></span>|

> [!NOTE] 
> <span data-ttu-id="0c8a8-154">Você deve evitar usar variáveis em hello – o parâmetro Name do **Get-AutomationVariable** em um runbook ou a configuração de DSC, pois isso pode complicar a descoberta de dependências entre runbooks ou configuração de DSC e automação variáveis em tempo de design.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-154">You should avoid using variables in hello –Name parameter of **Get-AutomationVariable**  in a runbook or DSC configuration since this can complicate discovering dependencies between runbooks or DSC configuration, and Automation variables at design time.</span></span>

## <a name="creating-a-new-automation-variable"></a><span data-ttu-id="0c8a8-155">Criando uma nova variável de automação</span><span class="sxs-lookup"><span data-stu-id="0c8a8-155">Creating a new Automation variable</span></span>

### <a name="toocreate-a-new-variable-with-hello-azure-portal"></a><span data-ttu-id="0c8a8-156">toocreate uma nova variável com hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0c8a8-156">toocreate a new variable with hello Azure portal</span></span>

1. <span data-ttu-id="0c8a8-157">Na sua conta de automação, clique em Olá **ativos** lado a lado e, em seguida, em Olá **ativos** folha, selecione **variáveis**.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-157">From your Automation account, click hello **Assets** tile and then on hello **Assets** blade, select **Variables**.</span></span>
2. <span data-ttu-id="0c8a8-158">Em Olá **variáveis** lado a lado, selecione **adicionar uma variável**.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-158">On hello **Variables** tile, select **Add a variable**.</span></span>
3. <span data-ttu-id="0c8a8-159">Concluir opções Olá Olá **nova variável** folha e clique em **criar** salvar Olá nova variável.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-159">Complete hello options on hello **New Variable** blade and click **Create** save hello new variable.</span></span>

### <a name="toocreate-a-new-variable-with-windows-powershell"></a><span data-ttu-id="0c8a8-160">toocreate uma nova variável com o Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="0c8a8-160">toocreate a new variable with Windows PowerShell</span></span>

<span data-ttu-id="0c8a8-161">Olá [AzureRmAutomationVariable novo](https://msdn.microsoft.com/library/mt603613.aspx) cmdlet cria uma nova variável e define seu valor inicial.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-161">hello [New-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) cmdlet creates a new variable and sets its initial value.</span></span> <span data-ttu-id="0c8a8-162">Você pode recuperar o valor de saudação usando [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx).</span><span class="sxs-lookup"><span data-stu-id="0c8a8-162">You can retrieve hello value using [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx).</span></span> <span data-ttu-id="0c8a8-163">Se o valor de saudação é um tipo simples, esse mesmo tipo é retornado.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-163">If hello value is a simple type, then that same type is returned.</span></span> <span data-ttu-id="0c8a8-164">Se for um tipo complexo, um **PSCustomObject** é retornado.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-164">If it’s a complex type, then a **PSCustomObject** is returned.</span></span>

<span data-ttu-id="0c8a8-165">saudação de exemplo a seguir comandos mostram como toocreate uma variável do tipo cadeia de caracteres e, em seguida, seu valor de retorno.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-165">hello following sample commands show how toocreate a variable of type string and then return its value.</span></span>

    New-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" 
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable' `
    –Encrypted $false –Value 'My String'
    $string = (Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable').Value

<span data-ttu-id="0c8a8-166">saudação de exemplo a seguir comandos mostram como toocreate uma variável com um complexo de tipo e, em seguida, retornar suas propriedades.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-166">hello following sample commands show how toocreate a variable with a complex type and then return its properties.</span></span> <span data-ttu-id="0c8a8-167">Nesse caso, é usado um objeto máquina virtual de **Get-AzureRmVm** .</span><span class="sxs-lookup"><span data-stu-id="0c8a8-167">In this case, a virtual machine object from **Get-AzureRmVm** is used.</span></span>

    $vm = Get-AzureRmVm -ResourceGroupName "ResourceGroup01" –Name "VM01"
    New-AzureRmAutomationVariable –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable" –Encrypted $false –Value $vm
    
    $vmValue = (Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable").Value
    $vmName = $vmValue.Name
    $vmIpAddress = $vmValue.IpAddress



## <a name="using-a-variable-in-a-runbook-or-dsc-configuration"></a><span data-ttu-id="0c8a8-168">Usando uma variável em um runbook ou configuração DSC </span><span class="sxs-lookup"><span data-stu-id="0c8a8-168">Using a variable in a runbook or DSC configuration</span></span>

<span data-ttu-id="0c8a8-169">Saudação de uso **Set-AutomationVariable** valor de hello atividade tooset de uma variável de automação em um runbook ou a configuração DSC e a saudação **Get-AutomationVariable** tooretrieve-lo.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-169">Use hello **Set-AutomationVariable** activity tooset hello value of an Automation variable in a runbook or DSC configuration, and hello **Get-AutomationVariable** tooretrieve it.</span></span>  <span data-ttu-id="0c8a8-170">Você não deve usar o hello **Set-AzureAutomationVariable** ou **Get-AzureAutomationVariable** cmdlets em um runbook ou a configuração de DSC, já que eles são menos eficientes do que as atividades de fluxo de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-170">You shouldn't use hello **Set-AzureAutomationVariable** or  **Get-AzureAutomationVariable** cmdlets in a runbook or DSC configuration since they are less efficient than hello workflow activities.</span></span>  <span data-ttu-id="0c8a8-171">Também é possível recuperar valor de saudação de variáveis seguras com **Get-AzureAutomationVariable**.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-171">You also cannot retrieve hello value of secure variables with **Get-AzureAutomationVariable**.</span></span>  <span data-ttu-id="0c8a8-172">Olá toocreate de maneira somente uma nova variável de dentro de um runbook ou a configuração de DSC está Olá toouse [New-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-172">hello only way toocreate a new variable from within a runbook or DSC configuration is toouse hello [New-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx)  cmdlet.</span></span>


### <a name="textual-runbook-samples"></a><span data-ttu-id="0c8a8-173">Exemplos de runbook textual</span><span class="sxs-lookup"><span data-stu-id="0c8a8-173">Textual runbook samples</span></span>

#### <a name="setting-and-retrieving-a-simple-value-from-a-variable"></a><span data-ttu-id="0c8a8-174">Definindo e recuperando um valor simples de uma variável</span><span class="sxs-lookup"><span data-stu-id="0c8a8-174">Setting and retrieving a simple value from a variable</span></span>

<span data-ttu-id="0c8a8-175">saudação de exemplo a seguir comandos mostram como tooset e recuperar uma variável em um runbook textual.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-175">hello following sample commands show how tooset and retrieve a variable in a textual runbook.</span></span> <span data-ttu-id="0c8a8-176">Nesse exemplo, presume-se que as variáveis do tipo integer denominadas *NumberOfIterations* e *NumberOfRunnings*, além de uma variável do tipo cadeia de caracteres denominada *SampleMessage*, já foram criadas.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-176">In this sample, it is assumed that variables of type integer named *NumberOfIterations* and *NumberOfRunnings* and a variable of type string named *SampleMessage* have already been created.</span></span>

    $NumberOfIterations = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfIterations'
    $NumberOfRunnings = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfRunnings'
    $SampleMessage = Get-AutomationVariable -Name 'SampleMessage'
    
    Write-Output "Runbook has been run $NumberOfRunnings times."
    
    for ($i = 1; $i -le $NumberOfIterations; $i++) {
       Write-Output "$i`: $SampleMessage"
    }
    Set-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" –Name NumberOfRunnings –Value ($NumberOfRunnings += 1)

#### <a name="setting-and-retrieving-a-complex-object-in-a-variable"></a><span data-ttu-id="0c8a8-177">Definindo e recuperando um objeto complexo em uma variável</span><span class="sxs-lookup"><span data-stu-id="0c8a8-177">Setting and retrieving a complex object in a variable</span></span>

<span data-ttu-id="0c8a8-178">saudação de exemplo a seguir mostra código como tooupdate uma variável com um valor complexo em um runbook textual.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-178">hello following sample code shows how tooupdate a variable with a complex value in a textual runbook.</span></span> <span data-ttu-id="0c8a8-179">Neste exemplo, uma máquina virtual do Azure é recuperada com **Get-AzureVM** e tooan salvo variável de automação existente.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-179">In this sample, an Azure virtual machine is retrieved with **Get-AzureVM** and saved tooan existing Automation variable.</span></span>  <span data-ttu-id="0c8a8-180">Como explicado em [Tipos de variáveis](#variable-types), ela é armazenada como um PSCustomObject.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-180">As explained in [Variable types](#variable-types), this is stored as a PSCustomObject.</span></span>

    $vm = Get-AzureVM -ServiceName "MyVM" -Name "MyVM"
    Set-AutomationVariable -Name "MyComplexVariable" -Value $vm


<span data-ttu-id="0c8a8-181">Saudação de código a seguir, valor Olá é recuperada da máquina de virtual de Olá Olá toostart variável e usado.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-181">In hello following code, hello value is retrieved from hello variable and used toostart hello virtual machine.</span></span>

    $vmObject = Get-AutomationVariable -Name "MyComplexVariable"
    if ($vmObject.PowerState -eq 'Stopped') {
       Start-AzureVM -ServiceName $vmObject.ServiceName -Name $vmObject.Name
    }


#### <a name="setting-and-retrieving-a-collection-in-a-variable"></a><span data-ttu-id="0c8a8-182">Definindo e recuperando uma coleção em uma variável</span><span class="sxs-lookup"><span data-stu-id="0c8a8-182">Setting and retrieving a collection in a variable</span></span>

<span data-ttu-id="0c8a8-183">saudação de exemplo a seguir mostra código como toouse uma variável com uma coleção de valores complexos em um runbook textual.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-183">hello following sample code shows how toouse a variable with a collection of complex values in a textual runbook.</span></span> <span data-ttu-id="0c8a8-184">Neste exemplo, várias máquinas virtuais do Azure são recuperadas com **Get-AzureVM** e tooan salvo variável de automação existente.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-184">In this sample, multiple Azure virtual machines are retrieved with **Get-AzureVM** and saved tooan existing Automation variable.</span></span>  <span data-ttu-id="0c8a8-185">Como explicado em [Tipos de variáveis](#variable-types), elas são armazenadas como uma coleção de PSCustomObjects.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-185">As explained in [Variable types](#variable-types), this is stored as a collection of PSCustomObjects.</span></span>

    $vms = Get-AzureVM | Where -FilterScript {$_.Name -match "my"}     
    Set-AutomationVariable -Name 'MyComplexVariable' -Value $vms

<span data-ttu-id="0c8a8-186">Na Olá código a seguir, a coleção de saudação é recuperada da variável hello e usado toostart cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-186">In hello following code, hello collection is retrieved from hello variable and used toostart each virtual machine.</span></span>

    $vmValues = Get-AutomationVariable -Name "MyComplexVariable"
    ForEach ($vmValue in $vmValues)
    {
       if ($vmValue.PowerState -eq 'Stopped') {
          Start-AzureVM -ServiceName $vmValue.ServiceName -Name $vmValue.Name
       }
    }


### <a name="graphical-runbook-samples"></a><span data-ttu-id="0c8a8-187">Exemplos de runbook gráfico</span><span class="sxs-lookup"><span data-stu-id="0c8a8-187">Graphical runbook samples</span></span>

<span data-ttu-id="0c8a8-188">Um runbook gráfico, você adiciona Olá **Get-AutomationVariable** ou **Set-AutomationVariable** clicando duas vezes na variável de saudação no painel de biblioteca de saudação do editor gráfico hello e selecionando Olá atividade desejada.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-188">In a graphical runbook, you add hello **Get-AutomationVariable** or **Set-AutomationVariable** by right-clicking on hello variable in hello Library pane of hello graphical editor and selecting hello activity you want.</span></span>

![Adicionar variável toocanvas](media/automation-variables/runbook-variable-add-canvas.png)

#### <a name="setting-values-in-a-variable"></a><span data-ttu-id="0c8a8-190">Definindo valores em uma variável</span><span class="sxs-lookup"><span data-stu-id="0c8a8-190">Setting values in a variable</span></span>
<span data-ttu-id="0c8a8-191">Olá imagem a seguir mostra exemplo atividades tooupdate uma variável com um valor simples em um runbook gráfico.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-191">hello following image shows sample activities tooupdate a variable with a simple value in a graphical runbook.</span></span> <span data-ttu-id="0c8a8-192">Neste exemplo, uma única máquina virtual do Azure é recuperada com **Get-AzureRmVM** e nome do computador Olá é salvo tooan variável de automação existente com um tipo de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-192">In this sample, a single Azure virtual machine is retrieved with **Get-AzureRmVM** and hello computer name is saved tooan existing Automation variable with a type of String.</span></span>  <span data-ttu-id="0c8a8-193">Não importa se hello [link é um pipeline ou sequência](automation-graphical-authoring-intro.md#links-and-workflow) como Esperamos que apenas um único objeto na saída de hello.</span><span class="sxs-lookup"><span data-stu-id="0c8a8-193">It doesn't matter whether hello [link is a pipeline or sequence](automation-graphical-authoring-intro.md#links-and-workflow) since we only expect a single object in hello output.</span></span>

![Definir variável simples](media/automation-variables/runbook-set-simple-variable.png)

## <a name="next-steps"></a><span data-ttu-id="0c8a8-195">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0c8a8-195">Next Steps</span></span>

* <span data-ttu-id="0c8a8-196">toolearn mais sobre como conectar atividades juntas na criação do gráfico, consulte [Links no gráfico de criação](automation-graphical-authoring-intro.md#links-and-workflow)</span><span class="sxs-lookup"><span data-stu-id="0c8a8-196">toolearn more about connecting activities together in graphical authoring, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow)</span></span>
* <span data-ttu-id="0c8a8-197">tooget iniciado com runbooks gráficos, consulte [meu primeiro runbook gráfico](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="0c8a8-197">tooget started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span> 

