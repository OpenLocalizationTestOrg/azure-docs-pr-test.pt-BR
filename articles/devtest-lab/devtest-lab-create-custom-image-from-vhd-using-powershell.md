---
title: aaaCreate uma imagem personalizada do Azure DevTest Labs de um arquivo VHD usando o PowerShell | Microsoft Docs
description: "Automatizar a criação de uma imagem personalizada no Azure DevTest Labs de um arquivo VHD usando o PowerShell"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 39b4005fa46cdf86cf0800ca376128134bcfb650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-from-a-vhd-file-using-powershell"></a>Criar uma imagem personalizada de um arquivo VHD usando o PowerShell

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a>Instruções passo a passo

Olá etapas a seguir orientam você durante a criação de uma imagem personalizada de um arquivo VHD usando o PowerShell:

1. Em um prompt do PowerShell, faça logon no tooyour conta do Azure com hello após a chamada toohello **AzureRmAccount Login** cmdlet.  
    
    ```PowerShell
    Login-AzureRmAccount
    ```

1.  Selecione Olá desejado assinatura do Azure por chamada hello **AzureRmSubscription selecione** cmdlet. Substituir saudação seguindo o espaço reservado para Olá **$subscriptionId** variável com uma ID de assinatura do Azure válida. 

    ```PowerShell
    $subscriptionId = '<Specify your subscription ID here>'
    Select-AzureRmSubscription -SubscriptionId $subscriptionId
    ```

1.  Obter o objeto de laboratório de saudação por chamada hello **Get-AzureRmResource** cmdlet. Substituir saudação espaços reservados para Olá a seguir **$labRg** e **$labName** variáveis com hello valores adequados para seu ambiente. 

    ```PowerShell
    $labRg = '<Specify your lab resource group name here>'
    $labName = '<Specify your lab name here>'
    $lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    ```
 
1.  Obter conta de armazenamento do laboratório hello e conta de armazenamento do laboratório valores de chave do objeto de laboratório hello. 

    ```PowerShell
    $labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
    $labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value
    ```

1.  Substituir saudação seguindo o espaço reservado para Olá **$vhdUri** carregado tooyour variável com hello URI arquivo VHD. Você pode obter o URI do arquivo VHD Olá da folha de blob da conta de armazenamento Olá no hello portal do Azure.

    ```PowerShell
    $vhdUri = '<Specify hello VHD URI here>'
    ```

1.  Criar imagem personalizada do hello usando Olá **AzureRmResourceGroupDeployment novo** cmdlet. Substituir saudação espaços reservados para Olá a seguir **$customImageName** e **$customImageDescription** nomes de toomeaningful de variáveis para o seu ambiente.

    ```PowerShell
    $customImageName = '<Specify hello custom image name>'
    $customImageDescription = '<Specify hello custom image description>'

    $parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

    New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
    ```

## <a name="powershell-script-toocreate-a-custom-image-from-a-vhd-file"></a>Toocreate de script do PowerShell uma imagem personalizada de um arquivo VHD

saudação de script do PowerShell a seguir pode ser usado toocreate uma imagem personalizada de um arquivo VHD. Substitua espaços reservados de saudação (começando e terminando com colchetes angulares) com valores apropriados de saudação para suas necessidades. 

```PowerShell
# Log in tooyour Azure account.  
Login-AzureRmAccount

# Select hello desired Azure subscription. 
$subscriptionId = '<Specify your subscription ID here>'
Select-AzureRmSubscription -SubscriptionId $subscriptionId

# Get hello lab object.
$labRg = '<Specify your lab resource group name here>'
$labName = '<Specify your lab name here>'
$lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)

# Get hello lab storage account and lab storage account key values.
$labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
$labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value

# Set hello URI of hello VHD file.  
$vhdUri = '<Specify hello VHD URI here>'

# Set hello custom image name and description values.
$customImageName = '<Specify hello custom image name>'
$customImageDescription = '<Specify hello custom image description>'

# Set up hello parameters object.
$parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

# Create hello custom image. 
New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
```

## <a name="related-blog-posts"></a>Postagens de blogs relacionadas

- [Imagens personalizadas ou fórmulas?](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [Copiar imagens personalizadas entre Azure DevTest Labs](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a>Próximas etapas

- [Adicionar um laboratório de tooyour VM](./devtest-lab-add-vm-with-artifacts.md)
