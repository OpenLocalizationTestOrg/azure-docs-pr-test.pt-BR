---
title: "Passar um objeto JSON para um runbook de Automação do Azure | Microsoft Docs"
description: "Como passar parâmetros para um runbook como um objeto JSON"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: "powershell,  runbook, json, automação do azure"
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 06/15/2017
ms.author: eslesar
ms.openlocfilehash: eac0e95a46731b9d396ea0590e629d61ca6a7d70
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="pass-a-json-object-to-an-azure-automation-runbook"></a><span data-ttu-id="0373a-104">Passar um objeto JSON para um runbook de Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="0373a-104">Pass a JSON object to an Azure Automation runbook</span></span>

<span data-ttu-id="0373a-105">Isso pode ser útil para armazenar os dados que você deseja passar para um runbook em um arquivo JSON.</span><span class="sxs-lookup"><span data-stu-id="0373a-105">It can be useful to store data that you want to pass to a runbook in a JSON file.</span></span>
<span data-ttu-id="0373a-106">Por exemplo, você pode criar um arquivo JSON que contém todos os parâmetros que você deseja passar para um runbook.</span><span class="sxs-lookup"><span data-stu-id="0373a-106">For example, you might create a JSON file that contains all of the parameters you want to pass to a runbook.</span></span>
<span data-ttu-id="0373a-107">Para fazer isso, você precisa converter o JSON para uma cadeia de caracteres e, em seguida, converter a cadeia de caracteres em um objeto do PowerShell antes de passar o seu conteúdo para o runbook.</span><span class="sxs-lookup"><span data-stu-id="0373a-107">To do this, you have to convert the JSON to a string and then convert the string to a PowerShell object before passing its contents to the runbook.</span></span>

<span data-ttu-id="0373a-108">Neste exemplo, vamos criar um script do PowerShell que chama [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) para iniciar um runbook do PowerShell, passando o conteúdo de JSON para o runbook.</span><span class="sxs-lookup"><span data-stu-id="0373a-108">In this example, we'll create a PowerShell script that calls [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) to start a PowerShell runbook, passing the contents of the JSON to the runbook.</span></span>
<span data-ttu-id="0373a-109">O runbook do PowerShell inicia uma VM do Azure, obtendo os parâmetros para a VM de JSON que foi passado.</span><span class="sxs-lookup"><span data-stu-id="0373a-109">The PowerShell runbook starts an Azure VM, getting the parameters for the VM from the JSON that was passed in.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0373a-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0373a-110">Prerequisites</span></span>
<span data-ttu-id="0373a-111">Para concluir este tutorial, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="0373a-111">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="0373a-112">Assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="0373a-112">Azure subscription.</span></span> <span data-ttu-id="0373a-113">Se você ainda não tiver uma, poderá [ativar os benefícios de assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou <a href="/pricing/free-account/" target="_blank">[inscrever-se em uma conta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="0373a-113">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or <a href="/pricing/free-account/" target="_blank">[sign up for a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="0373a-114">[Conta de automação](automation-sec-configure-azure-runas-account.md) para manter o runbook e se autenticar nos recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="0373a-114">[Automation account](automation-sec-configure-azure-runas-account.md) to hold the runbook and authenticate to Azure resources.</span></span>  <span data-ttu-id="0373a-115">Esta conta deve ter permissão para iniciar e parar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0373a-115">This account must have permission to start and stop the virtual machine.</span></span>
* <span data-ttu-id="0373a-116">Uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="0373a-116">An Azure virtual machine.</span></span> <span data-ttu-id="0373a-117">Paramos e iniciamos o computador, portanto, ele não deve ser uma VM de produção.</span><span class="sxs-lookup"><span data-stu-id="0373a-117">We stop and start this machine so it should not be a production VM.</span></span>
* <span data-ttu-id="0373a-118">Azure PowerShell instalado em um computador local.</span><span class="sxs-lookup"><span data-stu-id="0373a-118">Azure Powershell installed on a local machine.</span></span> <span data-ttu-id="0373a-119">Consulte [Install and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) (Instalar e configurar o Azure PowerShell) para obter informações sobre como obter o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0373a-119">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how to get Azure PowerShell.</span></span>

## <a name="create-the-json-file"></a><span data-ttu-id="0373a-120">Criar o arquivo JSON</span><span class="sxs-lookup"><span data-stu-id="0373a-120">Create the JSON file</span></span>

<span data-ttu-id="0373a-121">Digite o seguinte teste em um arquivo de texto e salve-o como `test.json` em algum lugar no seu computador local.</span><span class="sxs-lookup"><span data-stu-id="0373a-121">Type the following test in a text file, and save it as `test.json` somewhere on your local computer.</span></span>

```json
{
   "VmName" : "TestVM",
   "ResourceGroup" : "AzureAutomationTest"
}
```

## <a name="create-the-runbook"></a><span data-ttu-id="0373a-122">Criar o runbook</span><span class="sxs-lookup"><span data-stu-id="0373a-122">Create the runbook</span></span>

<span data-ttu-id="0373a-123">Crie um novo runbook PowerShell chamado "Test-Json" na Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="0373a-123">Create a new PowerShell runbook named "Test-Json" in Azure Automation.</span></span>
<span data-ttu-id="0373a-124">Para saber como criar um novo runbook do PowerShell, consulte [Meu primeiro runbook do PowerShell](automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="0373a-124">To learn how to create a new PowerShell runbook, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span></span>

<span data-ttu-id="0373a-125">Para aceitar os dados JSON, o runbook deve utilizar um objeto como um parâmetro de entrada.</span><span class="sxs-lookup"><span data-stu-id="0373a-125">To accept the JSON data, the runbook must take an object as an input parameter.</span></span>

<span data-ttu-id="0373a-126">O runbook pode, então, usar as propriedades definidas no JSON.</span><span class="sxs-lookup"><span data-stu-id="0373a-126">The runbook can then use the properties defined in the JSON.</span></span>

```powershell
Param(
     [parameter(Mandatory=$true)]
     [object]$json
)

# Connect to Azure account   
$Conn = Get-AutomationConnection -Name AzureRunAsConnection
Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint

# Convert object to actual JSON
$json = $json | ConvertFrom-Json

# Use the values from the JSON object as the parameters for your command
Start-AzureRmVM -Name $json.VMName -ResourceGroupName $json.ResourceGroup
 ```

 <span data-ttu-id="0373a-127">Salve e publique este runbook na sua conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="0373a-127">Save and publish this runbook in your Automation account.</span></span>

## <a name="call-the-runbook-from-powershell"></a><span data-ttu-id="0373a-128">Chamar o runbook do PowerShell</span><span class="sxs-lookup"><span data-stu-id="0373a-128">Call the runbook from PowerShell</span></span>

<span data-ttu-id="0373a-129">Agora você pode chamar o runbook de seu computador local usando o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0373a-129">Now you can call the runbook from your local machine by using Azure PowerShell.</span></span>
<span data-ttu-id="0373a-130">Execute os seguintes comandos do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="0373a-130">Run the following PowerShell commands:</span></span>

1. <span data-ttu-id="0373a-131">Faça logon no Azure:</span><span class="sxs-lookup"><span data-stu-id="0373a-131">Log in to Azure:</span></span>
   ```powershell
   Login-AzureRmAccount
   ```
    <span data-ttu-id="0373a-132">Você recebe uma solicitação para inserir suas credenciais do Azure.</span><span class="sxs-lookup"><span data-stu-id="0373a-132">You are prompted to enter your Azure credentials.</span></span>
1. <span data-ttu-id="0373a-133">Obtenha o conteúdo do arquivo JSON e converta-o em uma cadeia de caracteres:</span><span class="sxs-lookup"><span data-stu-id="0373a-133">Get the contents of the JSON file and convert it to a string:</span></span>
    ```powershell
    $json =  (Get-content -path 'JsonPath\test.json' -Raw) | Out-string
    ```
    <span data-ttu-id="0373a-134">`JsonPath` é o caminho em que você salvou o arquivo JSON.</span><span class="sxs-lookup"><span data-stu-id="0373a-134">`JsonPath` is the path where you saved the JSON file.</span></span>
1. <span data-ttu-id="0373a-135">Converta o conteúdo da cadeia de caracteres do `$json` em um objeto do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="0373a-135">Convert the string contents of `$json` to a PowerShell object:</span></span>
   ```powershell
   $JsonParams = @{"json"=$json}
   ```
1. <span data-ttu-id="0373a-136">Crie uma tabela de hash para os parâmetros para `Start-AzureRmAutomstionRunbook`:</span><span class="sxs-lookup"><span data-stu-id="0373a-136">Create a hashtable for the parameters for `Start-AzureRmAutomstionRunbook`:</span></span>
   ```powershell
   $RBParams = @{
        AutomationAccountName = 'AATest'
        ResourceGroupName = 'RGTest'
        Name = 'Test-Json'
        Parameters = $JsonParams
   }
   ```
   <span data-ttu-id="0373a-137">Observe que você está definindo o valor de `Parameters` para o objeto do PowerShell que contém os valores do arquivo JSON.</span><span class="sxs-lookup"><span data-stu-id="0373a-137">Notice that you are setting the value of `Parameters` to the PowerShell object that contains the values from the JSON file.</span></span> 
1. <span data-ttu-id="0373a-138">Iniciar o runbook</span><span class="sxs-lookup"><span data-stu-id="0373a-138">Start the runbook</span></span>
   ```powershell
   $job = Start-AzureRmAutomationRunbook @RBParams
   ```

<span data-ttu-id="0373a-139">O runbook usa os valores do arquivo JSON para iniciar uma VM.</span><span class="sxs-lookup"><span data-stu-id="0373a-139">The runbook uses the values from the JSON file to start a VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0373a-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0373a-140">Next steps</span></span>

* <span data-ttu-id="0373a-141">Para saber mais sobre como editar runbooks do PowerShell e do Fluxo de Trabalho do PowerShell com um editor de texto, consulte [Editando runbooks textuais na Automação do Azure](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="0373a-141">To learn more about editing PowerShell and PowerShell Workflow runbooks with a textual editor, see [Editing textual runbooks in Azure Automation](automation-edit-textual-runbook.md)</span></span> 
* <span data-ttu-id="0373a-142">Para saber mais sobre a criação e a importação de runbooks, consulte [Criando ou importando um runbook na Automação do Azure](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="0373a-142">To learn more about creating and importing runbooks, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md)</span></span>


