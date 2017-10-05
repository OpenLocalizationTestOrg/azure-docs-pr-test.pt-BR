---
title: "Ativos de variáveis na Automação do Azure | Microsoft Docs"
description: "Ativos de variáveis são valores que estão disponíveis para todos os runbooks e configurações DSC na Automação do Azure.  Este artigo explica os detalhes das variáveis e como trabalhar com elas na criação de textos e gráficos."
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
ms.openlocfilehash: dc00e1e5fa8df5cb55e7e2672137d1df44133773
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="variable-assets-in-azure-automation"></a><span data-ttu-id="dec7e-104">Ativos variáveis na Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="dec7e-104">Variable assets in Azure Automation</span></span>

<span data-ttu-id="dec7e-105">Ativos de variáveis são valores que estão disponíveis para todos os runbooks e configurações DSC em sua conta de automação.</span><span class="sxs-lookup"><span data-stu-id="dec7e-105">Variable assets are values that are available to all runbooks and DSC configurations in your automation account.</span></span> <span data-ttu-id="dec7e-106">Eles podem ser criados, modificados e recuperados no portal do Azure, no Windows PowerShell e em um runbook ou uma configuração DSC.</span><span class="sxs-lookup"><span data-stu-id="dec7e-106">They can be created, modified, and retrieved from the Azure portal, Windows PowerShell, and from within a runbook or DSC configuration.</span></span> <span data-ttu-id="dec7e-107">As variáveis de automação são úteis para os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="dec7e-107">Automation variables are useful for the following scenarios:</span></span>

- <span data-ttu-id="dec7e-108">Compartilhe um valor entre vários runbooks ou configurações DSC.</span><span class="sxs-lookup"><span data-stu-id="dec7e-108">Share a value between multiple runbooks or DSC configurations.</span></span>

- <span data-ttu-id="dec7e-109">Compartilhe um valor entre vários trabalhos do mesmo runbook ou configuração DSC.</span><span class="sxs-lookup"><span data-stu-id="dec7e-109">Share a value between multiple jobs from the same runbook or DSC configuration.</span></span>

- <span data-ttu-id="dec7e-110">Gerencie um valor do portal ou da linha de comando do Windows PowerShell usada por runbooks ou configurações de DSC, tal como conjunto de itens de configuração comuns como, por exemplo, lista específica de nomes de VM, grupo de recursos específico, nome de domínio de AD, etc.</span><span class="sxs-lookup"><span data-stu-id="dec7e-110">Manage a value from the portal or from the Windows PowerShell command line that is used by runbooks or DSC configurations, such as a set of common configuration items like specific list of VM names, a specific resource group,  an AD domain name, etc.</span></span>  

<span data-ttu-id="dec7e-111">As variáveis de automação são mantidas para que continuem disponíveis mesmo se o runbook ou a configuração DSC falhar.</span><span class="sxs-lookup"><span data-stu-id="dec7e-111">Automation variables are persisted so that they continue to be available even if the runbook or DSC configuration fails.</span></span>  <span data-ttu-id="dec7e-112">Isso também permite que um valor seja definido por um runbook que é depois usado por outro, ou que é usado pelo mesmo runbook ou configuração DSC na próxima vez em que for executado.</span><span class="sxs-lookup"><span data-stu-id="dec7e-112">This also allows a value to be set by one runbook that is then used by another, or is used by the same runbook or DSC configuration the next time that it is run.</span></span>

<span data-ttu-id="dec7e-113">Quando uma variável é criada, você pode definir que ele seja armazenado criptografado.</span><span class="sxs-lookup"><span data-stu-id="dec7e-113">When a variable is created, you can specify that it be stored encrypted.</span></span>  <span data-ttu-id="dec7e-114">Quando uma variável é criptografada, ela é armazenada com segurança na Automação do Azure e seu valor não pode ser recuperado do cmdlet [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) enviado como parte do módulo do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dec7e-114">When a variable is encrypted, it is stored securely in Azure Automation, and its value cannot be retrieved from the [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx) cmdlet that ships as part of the Azure PowerShell module.</span></span>  <span data-ttu-id="dec7e-115">A única maneira de recuperar um valor criptografado é por meio da atividade **Get-AutomationVariable** em um runbook ou configuração DSC.</span><span class="sxs-lookup"><span data-stu-id="dec7e-115">The only way that an encrypted value can be retrieved is from the **Get-AutomationVariable** activity in a runbook or DSC configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="dec7e-116">Os ativos protegidos na Automação do Azure incluem credenciais, certificados, conexões e variáveis criptografadas.</span><span class="sxs-lookup"><span data-stu-id="dec7e-116">Secure assets in Azure Automation include credentials, certificates, connections, and encrypted variables.</span></span> <span data-ttu-id="dec7e-117">Esses ativos são criptografados e armazenados na Automação do Azure usando uma chave exclusiva que é gerada para cada conta de automação.</span><span class="sxs-lookup"><span data-stu-id="dec7e-117">These assets are encrypted and stored in the Azure Automation using a unique key that is generated for each automation account.</span></span> <span data-ttu-id="dec7e-118">Essa chave é criptografada por um certificado mestre e armazenada na Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="dec7e-118">This key is encrypted by a master certificate and stored in Azure Automation.</span></span> <span data-ttu-id="dec7e-119">Antes de armazenar um ativo seguro, a chave para a conta de automação é descriptografada usando o certificado mestre e usada para criptografar o ativo.</span><span class="sxs-lookup"><span data-stu-id="dec7e-119">Before storing a secure asset, the key for the automation account is decrypted using the master certificate and then used to encrypt the asset.</span></span>

## <a name="variable-types"></a><span data-ttu-id="dec7e-120">Tipos de variável</span><span class="sxs-lookup"><span data-stu-id="dec7e-120">Variable types</span></span>

<span data-ttu-id="dec7e-121">Quando você cria uma variável com o portal do Azure, deve especificar um tipo de dados na lista suspensa para que o portal possa exibir o controle adequado para a inserção do valor da variável.</span><span class="sxs-lookup"><span data-stu-id="dec7e-121">When you create a variable with the Azure portal, you must specify a data type from the drop-down list so the portal can display the appropriate control for entering the variable value.</span></span> <span data-ttu-id="dec7e-122">A variável não está restrita a esse tipo de dados, mas você deve definir a variável usando o Windows PowerShell se desejar especificar um valor de um tipo diferente.</span><span class="sxs-lookup"><span data-stu-id="dec7e-122">The variable is not restricted to this data type, but you must set the variable using Windows PowerShell if you want to specify a value of a different type.</span></span> <span data-ttu-id="dec7e-123">Se você especificar **Indefinido**, o valor da variável será definido como **$null** e você deverá definir o valor com o cmdlet [Set-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) ou atividade **Set-AutomationVariable**.</span><span class="sxs-lookup"><span data-stu-id="dec7e-123">If you specify **Not defined**, then the value of the variable will be set to **$null**, and you must set the value with the [Set-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913767.aspx) cmdlet or **Set-AutomationVariable** activity.</span></span>  <span data-ttu-id="dec7e-124">Você não pode criar ou alterar o valor de um tipo complexo de variável no portal, mas pode fornecer um valor de qualquer tipo usando o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dec7e-124">You cannot create or change the value for a complex variable type in the portal, but you can provide a value of any type using Windows PowerShell.</span></span> <span data-ttu-id="dec7e-125">Tipos complexos serão retornados como um [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).</span><span class="sxs-lookup"><span data-stu-id="dec7e-125">Complex types will be returned as a [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx).</span></span>

<span data-ttu-id="dec7e-126">Você pode armazenar vários valores para uma única variável criando uma matriz ou hashtable e salvando-a na variável.</span><span class="sxs-lookup"><span data-stu-id="dec7e-126">You can store multiple values to a single variable by creating an array or hashtable and saving it to the variable.</span></span>

<span data-ttu-id="dec7e-127">A seguir está uma lista de tipos de variáveis disponíveis na automação:</span><span class="sxs-lookup"><span data-stu-id="dec7e-127">The following are a list of variable types available in Automation:</span></span>

* <span data-ttu-id="dec7e-128">string</span><span class="sxs-lookup"><span data-stu-id="dec7e-128">String</span></span>
* <span data-ttu-id="dec7e-129">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="dec7e-129">Integer</span></span>
* <span data-ttu-id="dec7e-130">DateTime</span><span class="sxs-lookup"><span data-stu-id="dec7e-130">DateTime</span></span>
* <span data-ttu-id="dec7e-131">Booliano</span><span class="sxs-lookup"><span data-stu-id="dec7e-131">Boolean</span></span>
* <span data-ttu-id="dec7e-132">Nulo</span><span class="sxs-lookup"><span data-stu-id="dec7e-132">Null</span></span>

## <a name="cmdlets-and-workflow-activities"></a><span data-ttu-id="dec7e-133">Atividades de fluxo de trabalho e cmdlets</span><span class="sxs-lookup"><span data-stu-id="dec7e-133">Cmdlets and workflow activities</span></span>

<span data-ttu-id="dec7e-134">Os cmdlets na tabela a seguir são usados para criar e gerenciar variáveis de automação com o Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dec7e-134">The cmdlets in the following table are used to create and manage Automation variables with Windows PowerShell.</span></span> <span data-ttu-id="dec7e-135">Eles são fornecidos como parte do [módulo do Azure PowerShell](../powershell-install-configure.md) que está disponível para uso em runbooks e na configuração DSC da Automação.</span><span class="sxs-lookup"><span data-stu-id="dec7e-135">They ship as part of the [Azure PowerShell module](../powershell-install-configure.md) which is available for use in Automation runbooks and DSC configuration.</span></span>

|<span data-ttu-id="dec7e-136">Cmdlets</span><span class="sxs-lookup"><span data-stu-id="dec7e-136">Cmdlets</span></span>|<span data-ttu-id="dec7e-137">Descrição</span><span class="sxs-lookup"><span data-stu-id="dec7e-137">Description</span></span>|
|:---|:---|
|[<span data-ttu-id="dec7e-138">Get-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="dec7e-138">Get-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603849.aspx)|<span data-ttu-id="dec7e-139">Recupera o valor de uma variável existente.</span><span class="sxs-lookup"><span data-stu-id="dec7e-139">Retrieves the value of an existing variable.</span></span>|
|[<span data-ttu-id="dec7e-140">New-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="dec7e-140">New-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603613.aspx)|<span data-ttu-id="dec7e-141">Cria uma nova variável e define o seu valor.</span><span class="sxs-lookup"><span data-stu-id="dec7e-141">Creates a new variable and sets its value.</span></span>|
|[<span data-ttu-id="dec7e-142">Remove-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="dec7e-142">Remove-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt619354.aspx)|<span data-ttu-id="dec7e-143">Remove uma variável existente.</span><span class="sxs-lookup"><span data-stu-id="dec7e-143">Removes an existing variable.</span></span>|
|[<span data-ttu-id="dec7e-144">Set-AzureRmAutomationVariable</span><span class="sxs-lookup"><span data-stu-id="dec7e-144">Set-AzureRmAutomationVariable</span></span>](https://msdn.microsoft.com/library/mt603601.aspx)|<span data-ttu-id="dec7e-145">Define o valor de uma variável existente.</span><span class="sxs-lookup"><span data-stu-id="dec7e-145">Sets the value for an existing variable.</span></span>|

<span data-ttu-id="dec7e-146">As atividades de fluxo de trabalho na tabela a seguir são usadas para acessar variáveis de automação em um runbook.</span><span class="sxs-lookup"><span data-stu-id="dec7e-146">The workflow activities in the following table are used to access Automation variables in a runbook.</span></span> <span data-ttu-id="dec7e-147">Elas só estão disponíveis para uso em um runbook ou uma configuração DSC e não são fornecidas como parte do módulo do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dec7e-147">They are only available for use in a runbook or DSC configuration, and do not ship as part of the Azure PowerShell module.</span></span>

|<span data-ttu-id="dec7e-148">Atividades de fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="dec7e-148">Workflow Activities</span></span>|<span data-ttu-id="dec7e-149">Descrição</span><span class="sxs-lookup"><span data-stu-id="dec7e-149">Description</span></span>|
|:---|:---|
|<span data-ttu-id="dec7e-150">Get-AutomationVariable</span><span class="sxs-lookup"><span data-stu-id="dec7e-150">Get-AutomationVariable</span></span>|<span data-ttu-id="dec7e-151">Recupera o valor de uma variável existente.</span><span class="sxs-lookup"><span data-stu-id="dec7e-151">Retrieves the value of an existing variable.</span></span>|
|<span data-ttu-id="dec7e-152">Set-AutomationVariable</span><span class="sxs-lookup"><span data-stu-id="dec7e-152">Set-AutomationVariable</span></span>|<span data-ttu-id="dec7e-153">Define o valor de uma variável existente.</span><span class="sxs-lookup"><span data-stu-id="dec7e-153">Sets the value for an existing variable.</span></span>|

> [!NOTE] 
> <span data-ttu-id="dec7e-154">Evite usar variáveis no parâmetro –Name de **Get-AutomationVariable** em um runbook ou na configuração DSC, pois isso pode complicar a descoberta de dependências entre runbooks ou configurações DSC e variáveis da Automação no momento do design.</span><span class="sxs-lookup"><span data-stu-id="dec7e-154">You should avoid using variables in the –Name parameter of **Get-AutomationVariable**  in a runbook or DSC configuration since this can complicate discovering dependencies between runbooks or DSC configuration, and Automation variables at design time.</span></span>

## <a name="creating-a-new-automation-variable"></a><span data-ttu-id="dec7e-155">Criando uma nova variável de automação</span><span class="sxs-lookup"><span data-stu-id="dec7e-155">Creating a new Automation variable</span></span>

### <a name="to-create-a-new-variable-with-the-azure-portal"></a><span data-ttu-id="dec7e-156">Para criar uma nova variável com o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="dec7e-156">To create a new variable with the Azure portal</span></span>

1. <span data-ttu-id="dec7e-157">Na sua conta de automação, clique no bloco **Ativos** e então, na folha, **Ativos**, selecione **Variáveis**.</span><span class="sxs-lookup"><span data-stu-id="dec7e-157">From your Automation account, click the **Assets** tile and then on the **Assets** blade, select **Variables**.</span></span>
2. <span data-ttu-id="dec7e-158">No bloco **Variáveis**, clique em **Adicionar uma variável**.</span><span class="sxs-lookup"><span data-stu-id="dec7e-158">On the **Variables** tile, select **Add a variable**.</span></span>
3. <span data-ttu-id="dec7e-159">Complete as opções na folha **Nova Variável** e clique em **Criar** para salvar a nova variável.</span><span class="sxs-lookup"><span data-stu-id="dec7e-159">Complete the options on the **New Variable** blade and click **Create** save the new variable.</span></span>

### <a name="to-create-a-new-variable-with-windows-powershell"></a><span data-ttu-id="dec7e-160">Para criar uma nova variável com o Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="dec7e-160">To create a new variable with Windows PowerShell</span></span>

<span data-ttu-id="dec7e-161">O cmdlet [New-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) cria uma nova variável e define o seu valor inicial.</span><span class="sxs-lookup"><span data-stu-id="dec7e-161">The [New-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) cmdlet creates a new variable and sets its initial value.</span></span> <span data-ttu-id="dec7e-162">Você pode recuperar o valor usando [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx).</span><span class="sxs-lookup"><span data-stu-id="dec7e-162">You can retrieve the value using [Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx).</span></span> <span data-ttu-id="dec7e-163">Se o valor for um tipo simples, é retornado o mesmo tipo.</span><span class="sxs-lookup"><span data-stu-id="dec7e-163">If the value is a simple type, then that same type is returned.</span></span> <span data-ttu-id="dec7e-164">Se for um tipo complexo, um **PSCustomObject** é retornado.</span><span class="sxs-lookup"><span data-stu-id="dec7e-164">If it’s a complex type, then a **PSCustomObject** is returned.</span></span>

<span data-ttu-id="dec7e-165">Os comandos de exemplo a seguir mostram como criar uma variável do tipo cadeia de caracteres e retornar o seu valor.</span><span class="sxs-lookup"><span data-stu-id="dec7e-165">The following sample commands show how to create a variable of type string and then return its value.</span></span>

    New-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" 
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable' `
    –Encrypted $false –Value 'My String'
    $string = (Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable').Value

<span data-ttu-id="dec7e-166">Os comandos de exemplo a seguir mostram como criar uma variável do tipo complexo e retornar as suas propriedades.</span><span class="sxs-lookup"><span data-stu-id="dec7e-166">The following sample commands show how to create a variable with a complex type and then return its properties.</span></span> <span data-ttu-id="dec7e-167">Nesse caso, é usado um objeto máquina virtual de **Get-AzureRmVm** .</span><span class="sxs-lookup"><span data-stu-id="dec7e-167">In this case, a virtual machine object from **Get-AzureRmVm** is used.</span></span>

    $vm = Get-AzureRmVm -ResourceGroupName "ResourceGroup01" –Name "VM01"
    New-AzureRmAutomationVariable –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable" –Encrypted $false –Value $vm
    
    $vmValue = (Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable").Value
    $vmName = $vmValue.Name
    $vmIpAddress = $vmValue.IpAddress



## <a name="using-a-variable-in-a-runbook-or-dsc-configuration"></a><span data-ttu-id="dec7e-168">Usando uma variável em um runbook ou configuração DSC </span><span class="sxs-lookup"><span data-stu-id="dec7e-168">Using a variable in a runbook or DSC configuration</span></span>

<span data-ttu-id="dec7e-169">Use a atividade **Set-AutomationVariable** para definir o valor de uma variável da Automação em um runbook ou uma configuração DSC e **Get-AutomationVariable** para recuperá-la.</span><span class="sxs-lookup"><span data-stu-id="dec7e-169">Use the **Set-AutomationVariable** activity to set the value of an Automation variable in a runbook or DSC configuration, and the **Get-AutomationVariable** to retrieve it.</span></span>  <span data-ttu-id="dec7e-170">Você não deve usar os cmdlets **Set-AzureAutomationVariable** ou **Get-AzureAutomationVariable** em um runbook ou configuração DSC, já que eles são menos eficientes do que as atividades de fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="dec7e-170">You shouldn't use the **Set-AzureAutomationVariable** or  **Get-AzureAutomationVariable** cmdlets in a runbook or DSC configuration since they are less efficient than the workflow activities.</span></span>  <span data-ttu-id="dec7e-171">Também não é possível recuperar o valor de variáveis protegidas com o **Get-AzureAutomationVariable**.</span><span class="sxs-lookup"><span data-stu-id="dec7e-171">You also cannot retrieve the value of secure variables with **Get-AzureAutomationVariable**.</span></span>  <span data-ttu-id="dec7e-172">A única maneira de criar uma nova variável de dentro de um runbook ou configuração DSC é usar o cmdlet [New-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx) .</span><span class="sxs-lookup"><span data-stu-id="dec7e-172">The only way to create a new variable from within a runbook or DSC configuration is to use the [New-AzureAutomationVariable](http://msdn.microsoft.com/library/dn913771.aspx)  cmdlet.</span></span>


### <a name="textual-runbook-samples"></a><span data-ttu-id="dec7e-173">Exemplos de runbook textual</span><span class="sxs-lookup"><span data-stu-id="dec7e-173">Textual runbook samples</span></span>

#### <a name="setting-and-retrieving-a-simple-value-from-a-variable"></a><span data-ttu-id="dec7e-174">Definindo e recuperando um valor simples de uma variável</span><span class="sxs-lookup"><span data-stu-id="dec7e-174">Setting and retrieving a simple value from a variable</span></span>

<span data-ttu-id="dec7e-175">Os comandos de exemplo a seguir mostram como definir e recuperar uma variável em um runbook textual.</span><span class="sxs-lookup"><span data-stu-id="dec7e-175">The following sample commands show how to set and retrieve a variable in a textual runbook.</span></span> <span data-ttu-id="dec7e-176">Nesse exemplo, presume-se que as variáveis do tipo integer denominadas *NumberOfIterations* e *NumberOfRunnings*, além de uma variável do tipo cadeia de caracteres denominada *SampleMessage*, já foram criadas.</span><span class="sxs-lookup"><span data-stu-id="dec7e-176">In this sample, it is assumed that variables of type integer named *NumberOfIterations* and *NumberOfRunnings* and a variable of type string named *SampleMessage* have already been created.</span></span>

    $NumberOfIterations = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfIterations'
    $NumberOfRunnings = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfRunnings'
    $SampleMessage = Get-AutomationVariable -Name 'SampleMessage'
    
    Write-Output "Runbook has been run $NumberOfRunnings times."
    
    for ($i = 1; $i -le $NumberOfIterations; $i++) {
       Write-Output "$i`: $SampleMessage"
    }
    Set-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" –Name NumberOfRunnings –Value ($NumberOfRunnings += 1)

#### <a name="setting-and-retrieving-a-complex-object-in-a-variable"></a><span data-ttu-id="dec7e-177">Definindo e recuperando um objeto complexo em uma variável</span><span class="sxs-lookup"><span data-stu-id="dec7e-177">Setting and retrieving a complex object in a variable</span></span>

<span data-ttu-id="dec7e-178">O código de exemplo a seguir mostra como atualizar uma variável com um valor complexo em um runbook textual.</span><span class="sxs-lookup"><span data-stu-id="dec7e-178">The following sample code shows how to update a variable with a complex value in a textual runbook.</span></span> <span data-ttu-id="dec7e-179">Nesse exemplo, uma máquina virtual do Azure é recuperada com **Get-AzureVM** e salva em uma variável de automação existente.</span><span class="sxs-lookup"><span data-stu-id="dec7e-179">In this sample, an Azure virtual machine is retrieved with **Get-AzureVM** and saved to an existing Automation variable.</span></span>  <span data-ttu-id="dec7e-180">Como explicado em [Tipos de variáveis](#variable-types), ela é armazenada como um PSCustomObject.</span><span class="sxs-lookup"><span data-stu-id="dec7e-180">As explained in [Variable types](#variable-types), this is stored as a PSCustomObject.</span></span>

    $vm = Get-AzureVM -ServiceName "MyVM" -Name "MyVM"
    Set-AutomationVariable -Name "MyComplexVariable" -Value $vm


<span data-ttu-id="dec7e-181">No código a seguir, o valor é recuperado da variável e usado para iniciar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="dec7e-181">In the following code, the value is retrieved from the variable and used to start the virtual machine.</span></span>

    $vmObject = Get-AutomationVariable -Name "MyComplexVariable"
    if ($vmObject.PowerState -eq 'Stopped') {
       Start-AzureVM -ServiceName $vmObject.ServiceName -Name $vmObject.Name
    }


#### <a name="setting-and-retrieving-a-collection-in-a-variable"></a><span data-ttu-id="dec7e-182">Definindo e recuperando uma coleção em uma variável</span><span class="sxs-lookup"><span data-stu-id="dec7e-182">Setting and retrieving a collection in a variable</span></span>

<span data-ttu-id="dec7e-183">O código de exemplo a seguir mostra como usar uma variável com uma coleção de valores complexos em um runbook textual.</span><span class="sxs-lookup"><span data-stu-id="dec7e-183">The following sample code shows how to use a variable with a collection of complex values in a textual runbook.</span></span> <span data-ttu-id="dec7e-184">Nesse exemplo, várias máquinas virtuais do Azure são recuperadas com **Get-AzureVM** e salvas em uma variável de automação existente.</span><span class="sxs-lookup"><span data-stu-id="dec7e-184">In this sample, multiple Azure virtual machines are retrieved with **Get-AzureVM** and saved to an existing Automation variable.</span></span>  <span data-ttu-id="dec7e-185">Como explicado em [Tipos de variáveis](#variable-types), elas são armazenadas como uma coleção de PSCustomObjects.</span><span class="sxs-lookup"><span data-stu-id="dec7e-185">As explained in [Variable types](#variable-types), this is stored as a collection of PSCustomObjects.</span></span>

    $vms = Get-AzureVM | Where -FilterScript {$_.Name -match "my"}     
    Set-AutomationVariable -Name 'MyComplexVariable' -Value $vms

<span data-ttu-id="dec7e-186">No código a seguir, a coleção é recuperada da variável e usada para iniciar cada máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="dec7e-186">In the following code, the collection is retrieved from the variable and used to start each virtual machine.</span></span>

    $vmValues = Get-AutomationVariable -Name "MyComplexVariable"
    ForEach ($vmValue in $vmValues)
    {
       if ($vmValue.PowerState -eq 'Stopped') {
          Start-AzureVM -ServiceName $vmValue.ServiceName -Name $vmValue.Name
       }
    }


### <a name="graphical-runbook-samples"></a><span data-ttu-id="dec7e-187">Exemplos de runbook gráfico</span><span class="sxs-lookup"><span data-stu-id="dec7e-187">Graphical runbook samples</span></span>

<span data-ttu-id="dec7e-188">Em um runbook gráfico, você adiciona o **Get-AutomationVariable** ou o **Set-AutomationVariable** clicando na variável com o botão direito do mouse no painel Biblioteca do editor gráfico e selecionando a atividade desejada.</span><span class="sxs-lookup"><span data-stu-id="dec7e-188">In a graphical runbook, you add the **Get-AutomationVariable** or **Set-AutomationVariable** by right-clicking on the variable in the Library pane of the graphical editor and selecting the activity you want.</span></span>

![Adicionar variável à tela](media/automation-variables/runbook-variable-add-canvas.png)

#### <a name="setting-values-in-a-variable"></a><span data-ttu-id="dec7e-190">Definindo valores em uma variável</span><span class="sxs-lookup"><span data-stu-id="dec7e-190">Setting values in a variable</span></span>
<span data-ttu-id="dec7e-191">A imagem a seguir mostra as atividades de exemplo para atualizar uma variável com um valor simples em um runbook gráfico.</span><span class="sxs-lookup"><span data-stu-id="dec7e-191">The following image shows sample activities to update a variable with a simple value in a graphical runbook.</span></span> <span data-ttu-id="dec7e-192">Nesse exemplo, uma única máquina virtual do Azure é recuperada com **Get-AzureRmVM** e o nome do computador é salvo em uma variável de automação existente com um tipo de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="dec7e-192">In this sample, a single Azure virtual machine is retrieved with **Get-AzureRmVM** and the computer name is saved to an existing Automation variable with a type of String.</span></span>  <span data-ttu-id="dec7e-193">Não importa se o [link é um pipeline ou uma sequência](automation-graphical-authoring-intro.md#links-and-workflow) , já que esperamos somente um único objeto na saída.</span><span class="sxs-lookup"><span data-stu-id="dec7e-193">It doesn't matter whether the [link is a pipeline or sequence](automation-graphical-authoring-intro.md#links-and-workflow) since we only expect a single object in the output.</span></span>

![Definir variável simples](media/automation-variables/runbook-set-simple-variable.png)

## <a name="next-steps"></a><span data-ttu-id="dec7e-195">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dec7e-195">Next Steps</span></span>

* <span data-ttu-id="dec7e-196">Para saber mais sobre como interligar as atividades na criação gráfica, confira [Links na criação gráfica](automation-graphical-authoring-intro.md#links-and-workflow)</span><span class="sxs-lookup"><span data-stu-id="dec7e-196">To learn more about connecting activities together in graphical authoring, see [Links in graphical authoring](automation-graphical-authoring-intro.md#links-and-workflow)</span></span>
* <span data-ttu-id="dec7e-197">Para começar a usar runbooks gráficos, veja [O meu primeiro runbook gráfico](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="dec7e-197">To get started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span> 

