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
# <a name="pass-a-json-object-tooan-azure-automation-runbook"></a>Passar um runbook de automação do Azure de tooan de objeto JSON

Ele pode ser útil toostore dados que você deseja toopass tooa runbook em um arquivo JSON.
Por exemplo, você pode criar um arquivo JSON que contém todos os parâmetros de saudação desejado toopass tooa runbook.
toodo isso, você tem a cadeia de caracteres do tooconvert Olá JSON tooa e, em seguida, converter o objeto do PowerShell de tooa de cadeia de caracteres de saudação antes de passar o runbook de toohello seu conteúdo.

Neste exemplo, vamos criar um script do PowerShell que chama [AzureRmAutomationRunbook início](https://msdn.microsoft.com/library/mt603661.aspx) toostart um runbook do PowerShell, passando o conteúdo de saudação do hello JSON toohello runbook.
Olá PowerShell runbook inicia uma VM do Azure, obter parâmetros Olá Olá VM de saudação JSON que foi passado.

## <a name="prerequisites"></a>Pré-requisitos
toocomplete neste tutorial, você precisa Olá a seguir:

* Assinatura do Azure. Se você ainda não tiver uma, poderá [ativar os benefícios de assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) ou <a href="/pricing/free-account/" target="_blank">[inscrever-se em uma conta gratuita](https://azure.microsoft.com/free/).
* [Conta de automação](automation-sec-configure-azure-runas-account.md) toohold Olá runbook e autenticar tooAzure recursos.  Essa conta deve ter permissão toostart e parar a máquina virtual de saudação.
* Uma máquina virtual do Azure. Paramos e iniciamos o computador, portanto, ele não deve ser uma VM de produção.
* Azure PowerShell instalado em um computador local. Consulte [instalar e configurar o Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.1.0) para obter informações sobre como tooget PowerShell do Azure.

## <a name="create-hello-json-file"></a>Criar arquivo JSON Olá

Digite o seguinte Olá teste em um arquivo de texto e salve-o como `test.json` em algum lugar no seu computador local.

```json
{
   "VmName" : "TestVM",
   "ResourceGroup" : "AzureAutomationTest"
}
```

## <a name="create-hello-runbook"></a>Criar hello runbook

Crie um novo runbook PowerShell chamado "Test-Json" na Automação do Azure.
toolearn como toocreate um novo runbook do PowerShell, consulte [meu primeiro runbook do PowerShell](automation-first-runbook-textual-powershell.md).

tooaccept dados JSON Olá Olá runbook deve obter um objeto como um parâmetro de entrada.

Olá runbook pode usar propriedades de saudação definidas em Olá JSON.

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

 Salve e publique este runbook na sua conta de Automação.

## <a name="call-hello-runbook-from-powershell"></a>Chamar o runbook de saudação do PowerShell

Agora você pode chamar hello runbook em seu computador local usando o PowerShell do Azure.
Olá executar comandos do PowerShell a seguir:

1. Faça logon em tooAzure:
   ```powershell
   Login-AzureRmAccount
   ```
    Você está tooenter solicitada suas credenciais do Azure.
1. Obter conteúdo de saudação do arquivo JSON de saudação e convertê-lo a cadeia de caracteres tooa:
    ```powershell
    $json =  (Get-content -path 'JsonPath\test.json' -Raw) | Out-string
    ```
    `JsonPath`é o caminho de saudação onde você salvou o arquivo JSON de saudação.
1. Converter conteúdo de cadeia de caracteres de saudação do `$json` tooa objeto do PowerShell:
   ```powershell
   $JsonParams = @{"json"=$json}
   ```
1. Criar uma tabela de hash para os parâmetros de saudação para `Start-AzureRmAutomstionRunbook`:
   ```powershell
   $RBParams = @{
        AutomationAccountName = 'AATest'
        ResourceGroupName = 'RGTest'
        Name = 'Test-Json'
        Parameters = $JsonParams
   }
   ```
   Observe que você está definindo o valor de saudação do `Parameters` toohello objeto do PowerShell que contém valores da saudação de saudação JSON. 
1. Iniciar o runbook Olá
   ```powershell
   $job = Start-AzureRmAutomationRunbook @RBParams
   ```

Olá runbook usa valores de saudação do hello JSON arquivo toostart uma VM.

## <a name="next-steps"></a>Próximas etapas

* toolearn mais sobre como editar runbooks do PowerShell e fluxo de trabalho do PowerShell com um editor de texto, consulte [edição textuais runbooks na automação do Azure](automation-edit-textual-runbook.md) 
* toolearn mais sobre como criar e importar runbooks, consulte [criando ou importando um runbook na automação do Azure](automation-creating-importing-runbook.md)


