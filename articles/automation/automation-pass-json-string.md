---
title: "runbook de automação do Azure tooan aaaPass JSON do objeto | Microsoft Docs"
description: "Como toopass parâmetros tooa runbook como um objeto JSON"
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
ms.openlocfilehash: 8229a16015d549927ead5496c70e9fb391d35498
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="pass-a-json-object-tooan-azure-automation-runbook"></a><span data-ttu-id="bec3c-104">Passar um runbook de automação do Azure de tooan de objeto JSON</span><span class="sxs-lookup"><span data-stu-id="bec3c-104">Pass a JSON object tooan Azure Automation runbook</span></span>

<span data-ttu-id="bec3c-105">Ele pode ser útil toostore dados que você deseja toopass tooa runbook em um arquivo JSON.</span><span class="sxs-lookup"><span data-stu-id="bec3c-105">It can be useful toostore data that you want toopass tooa runbook in a JSON file.</span></span>
<span data-ttu-id="bec3c-106">Por exemplo, você pode criar um arquivo JSON que contém todos os parâmetros de saudação desejado toopass tooa runbook.</span><span class="sxs-lookup"><span data-stu-id="bec3c-106">For example, you might create a JSON file that contains all of hello parameters you want toopass tooa runbook.</span></span>
<span data-ttu-id="bec3c-107">toodo isso, você tem a cadeia de caracteres do tooconvert Olá JSON tooa e, em seguida, converter o objeto do PowerShell de tooa de cadeia de caracteres de saudação antes de passar o runbook de toohello seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="bec3c-107">toodo this, you have tooconvert hello JSON tooa string and then convert hello string tooa PowerShell object before passing its contents toohello runbook.</span></span>

<span data-ttu-id="bec3c-108">Neste exemplo, vamos criar um script do PowerShell que chama [AzureRmAutomationRunbook início](https://msdn.microsoft.com/library/mt603661.aspx) toostart um runbook do PowerShell, passando o conteúdo de saudação do hello JSON toohello runbook.</span><span class="sxs-lookup"><span data-stu-id="bec3c-108">In this example, we'll create a PowerShell script that calls [Start-AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) toostart a PowerShell runbook, passing hello contents of hello JSON toohello runbook.</span></span>
<span data-ttu-id="bec3c-109">Olá PowerShell runbook inicia uma VM do Azure, obter parâmetros Olá Olá VM de saudação JSON que foi passado.</span><span class="sxs-lookup"><span data-stu-id="bec3c-109">hello PowerShell runbook starts an Azure VM, getting hello parameters for hello VM from hello JSON that was passed in.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bec3c-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bec3c-110">Prerequisites</span></span>
<span data-ttu-id="bec3c-111">toocomplete neste tutorial, você precisa Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="bec3c-111">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="bec3c-112">Assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="bec3c-112">Azure subscription.</span></span> <span data-ttu-id="bec3c-113">Se você ainda não tiver uma, poderá [ativar os benefícios de assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou <a href="/pricing/free-account/" target="_blank">[inscrever-se em uma conta gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="bec3c-113">If you don't have one yet, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or <a href="/pricing/free-account/" target="_blank">[sign up for a free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="bec3c-114">[Conta de automação](automation-sec-configure-azure-runas-account.md) toohold Olá runbook e autenticar tooAzure recursos.</span><span class="sxs-lookup"><span data-stu-id="bec3c-114">[Automation account](automation-sec-configure-azure-runas-account.md) toohold hello runbook and authenticate tooAzure resources.</span></span>  <span data-ttu-id="bec3c-115">Essa conta deve ter permissão toostart e parar a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="bec3c-115">This account must have permission toostart and stop hello virtual machine.</span></span>
* <span data-ttu-id="bec3c-116">Uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="bec3c-116">An Azure virtual machine.</span></span> <span data-ttu-id="bec3c-117">Paramos e iniciamos o computador, portanto, ele não deve ser uma VM de produção.</span><span class="sxs-lookup"><span data-stu-id="bec3c-117">We stop and start this machine so it should not be a production VM.</span></span>
* <span data-ttu-id="bec3c-118">Azure PowerShell instalado em um computador local.</span><span class="sxs-lookup"><span data-stu-id="bec3c-118">Azure Powershell installed on a local machine.</span></span> <span data-ttu-id="bec3c-119">Consulte [instalar e configurar o Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) para obter informações sobre como tooget PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="bec3c-119">See [Install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) for information about how tooget Azure PowerShell.</span></span>

## <a name="create-hello-json-file"></a><span data-ttu-id="bec3c-120">Criar arquivo JSON Olá</span><span class="sxs-lookup"><span data-stu-id="bec3c-120">Create hello JSON file</span></span>

<span data-ttu-id="bec3c-121">Digite o seguinte Olá teste em um arquivo de texto e salve-o como `test.json` em algum lugar no seu computador local.</span><span class="sxs-lookup"><span data-stu-id="bec3c-121">Type hello following test in a text file, and save it as `test.json` somewhere on your local computer.</span></span>

```json
{
   "VmName" : "TestVM",
   "ResourceGroup" : "AzureAutomationTest"
}
```

## <a name="create-hello-runbook"></a><span data-ttu-id="bec3c-122">Criar hello runbook</span><span class="sxs-lookup"><span data-stu-id="bec3c-122">Create hello runbook</span></span>

<span data-ttu-id="bec3c-123">Crie um novo runbook PowerShell chamado "Test-Json" na Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="bec3c-123">Create a new PowerShell runbook named "Test-Json" in Azure Automation.</span></span>
<span data-ttu-id="bec3c-124">toolearn como toocreate um novo runbook do PowerShell, consulte [meu primeiro runbook do PowerShell](automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="bec3c-124">toolearn how toocreate a new PowerShell runbook, see [My first PowerShell runbook](automation-first-runbook-textual-powershell.md).</span></span>

<span data-ttu-id="bec3c-125">tooaccept dados JSON Olá Olá runbook deve obter um objeto como um parâmetro de entrada.</span><span class="sxs-lookup"><span data-stu-id="bec3c-125">tooaccept hello JSON data, hello runbook must take an object as an input parameter.</span></span>

<span data-ttu-id="bec3c-126">Olá runbook pode usar propriedades de saudação definidas em Olá JSON.</span><span class="sxs-lookup"><span data-stu-id="bec3c-126">hello runbook can then use hello properties defined in hello JSON.</span></span>

```powershell
Param(
     [parameter(Mandatory=$true)]
     [object]$json
)

# Connect tooAzure account   
$Conn = Get-AutomationConnection -Name AzureRunAsConnection
Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
    -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint

# Convert object tooactual JSON
$json = $json | ConvertFrom-Json

# Use hello values from hello JSON object as hello parameters for your command
Start-AzureRmVM -Name $json.VMName -ResourceGroupName $json.ResourceGroup
 ```

 <span data-ttu-id="bec3c-127">Salve e publique este runbook na sua conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="bec3c-127">Save and publish this runbook in your Automation account.</span></span>

## <a name="call-hello-runbook-from-powershell"></a><span data-ttu-id="bec3c-128">Chamar o runbook de saudação do PowerShell</span><span class="sxs-lookup"><span data-stu-id="bec3c-128">Call hello runbook from PowerShell</span></span>

<span data-ttu-id="bec3c-129">Agora você pode chamar hello runbook em seu computador local usando o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="bec3c-129">Now you can call hello runbook from your local machine by using Azure PowerShell.</span></span>
<span data-ttu-id="bec3c-130">Olá executar comandos do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="bec3c-130">Run hello following PowerShell commands:</span></span>

1. <span data-ttu-id="bec3c-131">Faça logon em tooAzure:</span><span class="sxs-lookup"><span data-stu-id="bec3c-131">Log in tooAzure:</span></span>
   ```powershell
   Login-AzureRmAccount
   ```
    <span data-ttu-id="bec3c-132">Você está tooenter solicitada suas credenciais do Azure.</span><span class="sxs-lookup"><span data-stu-id="bec3c-132">You are prompted tooenter your Azure credentials.</span></span>
1. <span data-ttu-id="bec3c-133">Obter conteúdo de saudação do arquivo JSON de saudação e convertê-lo a cadeia de caracteres tooa:</span><span class="sxs-lookup"><span data-stu-id="bec3c-133">Get hello contents of hello JSON file and convert it tooa string:</span></span>
    ```powershell
    $json =  (Get-content -path 'JsonPath\test.json' -Raw) | Out-string
    ```
    <span data-ttu-id="bec3c-134">`JsonPath`é o caminho de saudação onde você salvou o arquivo JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="bec3c-134">`JsonPath` is hello path where you saved hello JSON file.</span></span>
1. <span data-ttu-id="bec3c-135">Converter conteúdo de cadeia de caracteres de saudação do `$json` tooa objeto do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="bec3c-135">Convert hello string contents of `$json` tooa PowerShell object:</span></span>
   ```powershell
   $JsonParams = @{"json"=$json}
   ```
1. <span data-ttu-id="bec3c-136">Criar uma tabela de hash para os parâmetros de saudação para `Start-AzureRmAutomstionRunbook`:</span><span class="sxs-lookup"><span data-stu-id="bec3c-136">Create a hashtable for hello parameters for `Start-AzureRmAutomstionRunbook`:</span></span>
   ```powershell
   $RBParams = @{
        AutomationAccountName = 'AATest'
        ResourceGroupName = 'RGTest'
        Name = 'Test-Json'
        Parameters = $JsonParams
   }
   ```
   <span data-ttu-id="bec3c-137">Observe que você está definindo o valor de saudação do `Parameters` toohello objeto do PowerShell que contém valores da saudação de saudação JSON.</span><span class="sxs-lookup"><span data-stu-id="bec3c-137">Notice that you are setting hello value of `Parameters` toohello PowerShell object that contains hello values from hello JSON file.</span></span> 
1. <span data-ttu-id="bec3c-138">Iniciar o runbook Olá</span><span class="sxs-lookup"><span data-stu-id="bec3c-138">Start hello runbook</span></span>
   ```powershell
   $job = Start-AzureRmAutomationRunbook @RBParams
   ```

<span data-ttu-id="bec3c-139">Olá runbook usa valores de saudação do hello JSON arquivo toostart uma VM.</span><span class="sxs-lookup"><span data-stu-id="bec3c-139">hello runbook uses hello values from hello JSON file toostart a VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bec3c-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bec3c-140">Next steps</span></span>

* <span data-ttu-id="bec3c-141">toolearn mais sobre como editar runbooks do PowerShell e fluxo de trabalho do PowerShell com um editor de texto, consulte [edição textuais runbooks na automação do Azure](automation-edit-textual-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="bec3c-141">toolearn more about editing PowerShell and PowerShell Workflow runbooks with a textual editor, see [Editing textual runbooks in Azure Automation](automation-edit-textual-runbook.md)</span></span> 
* <span data-ttu-id="bec3c-142">toolearn mais sobre como criar e importar runbooks, consulte [criando ou importando um runbook na automação do Azure](automation-creating-importing-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="bec3c-142">toolearn more about creating and importing runbooks, see [Creating or importing a runbook in Azure Automation](automation-creating-importing-runbook.md)</span></span>


