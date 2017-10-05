---
title: Criar uma imagem personalizada do Azure DevTest Labs de um arquivo VHD usando o PowerShell | Microsoft Docs
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
ms.openlocfilehash: a4729f70aae80a13233fbe96a5d8a56c0c9d01d3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-custom-image-from-a-vhd-file-using-powershell"></a><span data-ttu-id="bcc53-103">Criar uma imagem personalizada de um arquivo VHD usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="bcc53-103">Create a custom image from a VHD file using PowerShell</span></span>

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="bcc53-104">Instruções passo a passo</span><span class="sxs-lookup"><span data-stu-id="bcc53-104">Step-by-step instructions</span></span>

<span data-ttu-id="bcc53-105">As seguintes etapas orientam você durante a criação de uma imagem personalizada de um arquivo VHD usando o PowerShell:</span><span class="sxs-lookup"><span data-stu-id="bcc53-105">The following steps walk you through creating a custom image from a VHD file using PowerShell:</span></span>

1. <span data-ttu-id="bcc53-106">Em um prompt do PowerShell, entre na sua conta do Azure com a chamada a seguir ao cmdlet **Login-AzureRmAccount**.</span><span class="sxs-lookup"><span data-stu-id="bcc53-106">At a PowerShell prompt, log in to your Azure account with the following call to the **Login-AzureRmAccount** cmdlet.</span></span>  
    
    ```PowerShell
    Login-AzureRmAccount
    ```

1.  <span data-ttu-id="bcc53-107">Selecione a assinatura do Azure desejada chamando o cmdlet **Select-AzureRmSubscription**.</span><span class="sxs-lookup"><span data-stu-id="bcc53-107">Select the desired Azure subscription by calling the **Select-AzureRmSubscription** cmdlet.</span></span> <span data-ttu-id="bcc53-108">Substitua o espaço reservado a seguir para a variável **$subscriptionId** por uma ID de assinatura válida do Azure.</span><span class="sxs-lookup"><span data-stu-id="bcc53-108">Replace the following placeholder for the **$subscriptionId** variable with a valid Azure subscription ID.</span></span> 

    ```PowerShell
    $subscriptionId = '<Specify your subscription ID here>'
    Select-AzureRmSubscription -SubscriptionId $subscriptionId
    ```

1.  <span data-ttu-id="bcc53-109">Obtenha o objeto de laboratório chamando o cmdlet **Get-AzureRmResource**.</span><span class="sxs-lookup"><span data-stu-id="bcc53-109">Get the lab object by calling the **Get-AzureRmResource** cmdlet.</span></span> <span data-ttu-id="bcc53-110">Substitua os espaços reservados a seguir para as variáveis **$labRg** e **$labName** pelos valores apropriados para seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="bcc53-110">Replace the following placeholders for the **$labRg** and **$labName** variables with the appropriate values for your environment.</span></span> 

    ```PowerShell
    $labRg = '<Specify your lab resource group name here>'
    $labName = '<Specify your lab name here>'
    $lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)
    ```
 
1.  <span data-ttu-id="bcc53-111">Obtenha os valores da conta de armazenamento e da chave da conta de armazenamento do laboratório do objeto de laboratório.</span><span class="sxs-lookup"><span data-stu-id="bcc53-111">Get the lab storage account and lab storage account key values from the lab object.</span></span> 

    ```PowerShell
    $labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
    $labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value
    ```

1.  <span data-ttu-id="bcc53-112">Substitua o espaço reservado a seguir da variável **$vhdUri** pelo URI para seu arquivo VHD carregado.</span><span class="sxs-lookup"><span data-stu-id="bcc53-112">Replace the following placeholder for the **$vhdUri** variable with the URI to your uploaded VHD file.</span></span> <span data-ttu-id="bcc53-113">Você pode obter o URI do arquivo VHD na folha de blob da conta de armazenamento no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="bcc53-113">You can get the VHD file's URI from the storage account's blob blade in the Azure portal.</span></span>

    ```PowerShell
    $vhdUri = '<Specify the VHD URI here>'
    ```

1.  <span data-ttu-id="bcc53-114">Crie a imagem personalizada usando o cmdlet **New-AzureRmResourceGroupDeployment**.</span><span class="sxs-lookup"><span data-stu-id="bcc53-114">Create the custom image using the **New-AzureRmResourceGroupDeployment** cmdlet.</span></span> <span data-ttu-id="bcc53-115">Substitua os espaços reservados a seguir para as variáveis **$customImageName** e **$customImageDescription** por nomes significativos para seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="bcc53-115">Replace the following placeholders for the **$customImageName** and **$customImageDescription** variables to meaningful names for your environment.</span></span>

    ```PowerShell
    $customImageName = '<Specify the custom image name>'
    $customImageDescription = '<Specify the custom image description>'

    $parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

    New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
    ```

## <a name="powershell-script-to-create-a-custom-image-from-a-vhd-file"></a><span data-ttu-id="bcc53-116">Script do PowerShell para criar uma imagem personalizada de um arquivo VHD</span><span class="sxs-lookup"><span data-stu-id="bcc53-116">PowerShell script to create a custom image from a VHD file</span></span>

<span data-ttu-id="bcc53-117">O script do PowerShell a seguir pode ser usado para criar uma imagem personalizada de um arquivo VHD.</span><span class="sxs-lookup"><span data-stu-id="bcc53-117">The following PowerShell script can be used to create a custom image from a VHD file.</span></span> <span data-ttu-id="bcc53-118">Substitua os espaços reservados (que começam e terminam com colchetes angulares) pelos valores apropriados às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="bcc53-118">Replace the placeholders (starting and ending with angle brackets) with the appropriate values for your needs.</span></span> 

```PowerShell
# Log in to your Azure account.  
Login-AzureRmAccount

# Select the desired Azure subscription. 
$subscriptionId = '<Specify your subscription ID here>'
Select-AzureRmSubscription -SubscriptionId $subscriptionId

# Get the lab object.
$labRg = '<Specify your lab resource group name here>'
$labName = '<Specify your lab name here>'
$lab = Get-AzureRmResource -ResourceId ('/subscriptions/' + $subscriptionId + '/resourceGroups/' + $labRg + '/providers/Microsoft.DevTestLab/labs/' + $labName)

# Get the lab storage account and lab storage account key values.
$labStorageAccount = Get-AzureRmResource -ResourceId $lab.Properties.defaultStorageAccount 
$labStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $labStorageAccount.ResourceGroupName -Name $labStorageAccount.ResourceName)[0].Value

# Set the URI of the VHD file.  
$vhdUri = '<Specify the VHD URI here>'

# Set the custom image name and description values.
$customImageName = '<Specify the custom image name>'
$customImageDescription = '<Specify the custom image description>'

# Set up the parameters object.
$parameters = @{existingLabName="$($lab.Name)"; existingVhdUri=$vhdUri; imageOsType='windows'; isVhdSysPrepped=$false; imageName=$customImageName; imageDescription=$customImageDescription}

# Create the custom image. 
New-AzureRmResourceGroupDeployment -ResourceGroupName $lab.ResourceGroupName -Name CreateCustomImage -TemplateUri 'https://raw.githubusercontent.com/Azure/azure-devtestlab/master/Samples/201-dtl-create-customimage-from-vhd/azuredeploy.json' -TemplateParameterObject $parameters
```

## <a name="related-blog-posts"></a><span data-ttu-id="bcc53-119">Postagens de blogs relacionadas</span><span class="sxs-lookup"><span data-stu-id="bcc53-119">Related blog posts</span></span>

- [<span data-ttu-id="bcc53-120">Imagens personalizadas ou fórmulas?</span><span class="sxs-lookup"><span data-stu-id="bcc53-120">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="bcc53-121">Copiar imagens personalizadas entre Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="bcc53-121">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="bcc53-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bcc53-122">Next steps</span></span>

- [<span data-ttu-id="bcc53-123">Adicionar uma VM ao laboratório</span><span class="sxs-lookup"><span data-stu-id="bcc53-123">Add a VM to your lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)
