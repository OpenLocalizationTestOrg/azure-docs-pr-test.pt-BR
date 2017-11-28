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
# <a name="create-a-custom-image-from-a-vhd-file-using-powershell"></a><span data-ttu-id="f16cb-103">Criar uma imagem personalizada de um arquivo VHD usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="f16cb-103">Create a custom image from a VHD file using PowerShell</span></span>

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="f16cb-104">Instruções passo a passo</span><span class="sxs-lookup"><span data-stu-id="f16cb-104">Step-by-step instructions</span></span>

<span data-ttu-id="f16cb-105">Olá etapas a seguir orientam você durante a criação de uma imagem personalizada de um arquivo VHD usando o PowerShell:</span><span class="sxs-lookup"><span data-stu-id="f16cb-105">hello following steps walk you through creating a custom image from a VHD file using PowerShell:</span></span>

1. <span data-ttu-id="f16cb-106">Em um prompt do PowerShell, faça logon no tooyour conta do Azure com hello após a chamada toohello **AzureRmAccount Login** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f16cb-106">At a PowerShell prompt, log in tooyour Azure account with hello following call toohello **Login-AzureRmAccount** cmdlet.</span></span>  
    
    ```PowerShell
    Login-AzureRmAccount
    ```

1.  <span data-ttu-id="f16cb-107">Selecione Olá desejado assinatura do Azure por chamada hello **AzureRmSubscription selecione** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f16cb-107">Select hello desired Azure subscription by calling hello **Select-AzureRmSubscription** cmdlet.</span></span> <span data-ttu-id="f16cb-108">Substituir saudação seguindo o espaço reservado para Olá **$subscriptionId** variável com uma ID de assinatura do Azure válida.</span><span class="sxs-lookup"><span data-stu-id="f16cb-108">Replace hello following placeholder for hello **$subscriptionId** variable with a valid Azure subscription ID.</span></span> 

    ```PowerShell
    $subscriptionId = '<Specify your subscription ID here>'
    Select-AzureRmSubscription -SubscriptionId $subscriptionId
    ```

1.  <span data-ttu-id="f16cb-109">Obter o objeto de laboratório de saudação por chamada hello **Get-AzureRmResource** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f16cb-109">Get hello lab object by calling hello **Get-AzureRmResource** cmdlet.</span></span> <span data-ttu-id="f16cb-110">Substituir saudação espaços reservados para Olá a seguir **$labRg** e **$labName** variáveis com hello valores adequados para seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="f16cb-110">Replace hello following placeholders for hello **$labRg** and **$labName** variables with hello appropriate values for your environment.</span></span> 

    ```PowerShell
    $labRg = '<Specify your lab resource group name here>'
    $labName = '<Specify your lab name here>'
    $lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    ```
 
1.  <span data-ttu-id="f16cb-111">Obter conta de armazenamento do laboratório hello e conta de armazenamento do laboratório valores de chave do objeto de laboratório hello.</span><span class="sxs-lookup"><span data-stu-id="f16cb-111">Get hello lab storage account and lab storage account key values from hello lab object.</span></span> 

    ```PowerShell
    $labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
    $labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value
    ```

1.  <span data-ttu-id="f16cb-112">Substituir saudação seguindo o espaço reservado para Olá **$vhdUri** carregado tooyour variável com hello URI arquivo VHD.</span><span class="sxs-lookup"><span data-stu-id="f16cb-112">Replace hello following placeholder for hello **$vhdUri** variable with hello URI tooyour uploaded VHD file.</span></span> <span data-ttu-id="f16cb-113">Você pode obter o URI do arquivo VHD Olá da folha de blob da conta de armazenamento Olá no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f16cb-113">You can get hello VHD file's URI from hello storage account's blob blade in hello Azure portal.</span></span>

    ```PowerShell
    $vhdUri = '<Specify hello VHD URI here>'
    ```

1.  <span data-ttu-id="f16cb-114">Criar imagem personalizada do hello usando Olá **AzureRmResourceGroupDeployment novo** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f16cb-114">Create hello custom image using hello **New-AzureRmResourceGroupDeployment** cmdlet.</span></span> <span data-ttu-id="f16cb-115">Substituir saudação espaços reservados para Olá a seguir **$customImageName** e **$customImageDescription** nomes de toomeaningful de variáveis para o seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="f16cb-115">Replace hello following placeholders for hello **$customImageName** and **$customImageDescription** variables toomeaningful names for your environment.</span></span>

    ```PowerShell
    $customImageName = '<Specify hello custom image name>'
    $customImageDescription = '<Specify hello custom image description>'

    $parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

    New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
    ```

## <a name="powershell-script-toocreate-a-custom-image-from-a-vhd-file"></a><span data-ttu-id="f16cb-116">Toocreate de script do PowerShell uma imagem personalizada de um arquivo VHD</span><span class="sxs-lookup"><span data-stu-id="f16cb-116">PowerShell script toocreate a custom image from a VHD file</span></span>

<span data-ttu-id="f16cb-117">saudação de script do PowerShell a seguir pode ser usado toocreate uma imagem personalizada de um arquivo VHD.</span><span class="sxs-lookup"><span data-stu-id="f16cb-117">hello following PowerShell script can be used toocreate a custom image from a VHD file.</span></span> <span data-ttu-id="f16cb-118">Substitua espaços reservados de saudação (começando e terminando com colchetes angulares) com valores apropriados de saudação para suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="f16cb-118">Replace hello placeholders (starting and ending with angle brackets) with hello appropriate values for your needs.</span></span> 

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

## <a name="related-blog-posts"></a><span data-ttu-id="f16cb-119">Postagens de blogs relacionadas</span><span class="sxs-lookup"><span data-stu-id="f16cb-119">Related blog posts</span></span>

- [<span data-ttu-id="f16cb-120">Imagens personalizadas ou fórmulas?</span><span class="sxs-lookup"><span data-stu-id="f16cb-120">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="f16cb-121">Copiar imagens personalizadas entre Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="f16cb-121">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="f16cb-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f16cb-122">Next steps</span></span>

- [<span data-ttu-id="f16cb-123">Adicionar um laboratório de tooyour VM</span><span class="sxs-lookup"><span data-stu-id="f16cb-123">Add a VM tooyour lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
