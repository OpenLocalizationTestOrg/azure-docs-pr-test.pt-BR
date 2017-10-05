---
title: Criar um balanceador de carga interno - Modelo do Azure | Microsoft Docs
description: Saiba como criar um balanceador de carga interno no Gerenciador de Recursos usando um modelo
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 64150862-6ced-42de-85dc-89d323257d7c
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 5e0278cf5c605298932d6ac55d147a1c43fd9d23
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-internal-load-balancer-using-a-template"></a><span data-ttu-id="314d9-103">Criar um balanceador de carga interno usando um modelo</span><span class="sxs-lookup"><span data-stu-id="314d9-103">Create an internal load balancer using a template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="314d9-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="314d9-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="314d9-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="314d9-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="314d9-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="314d9-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="314d9-107">Modelo</span><span class="sxs-lookup"><span data-stu-id="314d9-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="314d9-108">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="314d9-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="314d9-109">Este artigo aborda usando o modelo de implantação do Gerenciador de Recursos, que a Microsoft recomenda para a maioria das novas implantações em vez de do [modelo de implantação clássico](load-balancer-get-started-ilb-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="314d9-109">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-the-template-by-using-click-to-deploy"></a><span data-ttu-id="314d9-110">Implantar o modelo usando o clique para implantar</span><span class="sxs-lookup"><span data-stu-id="314d9-110">Deploy the template by using click to deploy</span></span>

<span data-ttu-id="314d9-111">O modelo de exemplo disponível no repositório público usa um arquivo de parâmetro que contém os valores padrão usados para gerar o cenário descrito acima.</span><span class="sxs-lookup"><span data-stu-id="314d9-111">The sample template available in the public repository uses a parameter file containing the default values used to generate the scenario described above.</span></span> <span data-ttu-id="314d9-112">Para implantar esse modelo usando a opção de clique para implantar, acesse [este link](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), clique em **Implantar no Azure**, substitua os valores de parâmetro padrão, se necessário, e siga as instruções no portal.</span><span class="sxs-lookup"><span data-stu-id="314d9-112">To deploy this template using click to deploy, follow [this link](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>

## <a name="deploy-the-template-by-using-powershell"></a><span data-ttu-id="314d9-113">Implantar o modelo usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="314d9-113">Deploy the template by using PowerShell</span></span>

<span data-ttu-id="314d9-114">Para implantar o modelo baixado usando o PowerShell, faça o seguinte.</span><span class="sxs-lookup"><span data-stu-id="314d9-114">To deploy the template you downloaded by using PowerShell, follow the steps below.</span></span>

1. <span data-ttu-id="314d9-115">Se você nunca usou o Azure PowerShell, consulte [Como Instalar e Configurar o Azure PowerShell](/powershell/azure/overview) e siga as instruções até o fim para entrar no Azure e selecionar sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="314d9-115">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azure/overview) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="314d9-116">Baixe o arquivo de parâmetros no disco local.</span><span class="sxs-lookup"><span data-stu-id="314d9-116">Download the parameters file to your local disk.</span></span>
3. <span data-ttu-id="314d9-117">Edite o arquivo e salve-o.</span><span class="sxs-lookup"><span data-stu-id="314d9-117">Edit the file and save it.</span></span>
4. <span data-ttu-id="314d9-118">Execute o cmdlet **New-AzureRmResourceGroupDeployment** para criar um grupo de recursos usando o modelo.</span><span class="sxs-lookup"><span data-stu-id="314d9-118">Run the **New-AzureRmResourceGroupDeployment** cmdlet to create a resource group using the template.</span></span>

    ```azurecli
    New-AzureRmResourceGroupDeployment -Name TestRG -Location westus `
        -TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json' `
        -TemplateParameterFile 'C:\temp\azuredeploy.parameters.json'
    ```

## <a name="deploy-the-template-by-using-the-azure-cli"></a><span data-ttu-id="314d9-119">Implantar o modelo usando a CLI do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="314d9-119">Deploy the template by using the Azure CLI</span></span>

<span data-ttu-id="314d9-120">Para implantar o modelo usando a CLI do Microsoft Azure, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="314d9-120">To deploy the template by using the Azure CLI, follow the steps below.</span></span>

1. <span data-ttu-id="314d9-121">Se você nunca usou a CLI do Azure, veja [Instalar e configurar a CLI do Azure](../cli-install-nodejs.md) e siga as instruções até o ponto em que você seleciona sua conta e assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="314d9-121">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="314d9-122">Execute o comando **azure config mode** para alternar para o modo do Gerenciador de Recursos, como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="314d9-122">Run the **azure config mode** command to switch to Resource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="314d9-123">Este é o resultado esperado para o comando descrito acima:</span><span class="sxs-lookup"><span data-stu-id="314d9-123">Here is the expected output for the command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="314d9-124">Abra o arquivo de parâmetro, selecione o seu conteúdo e salve-o em um arquivo em seu computador.</span><span class="sxs-lookup"><span data-stu-id="314d9-124">Open the parameter file, select its contents, and save it to a file in your computer.</span></span> <span data-ttu-id="314d9-125">Para este exemplo, salvamos o arquivo de parâmetros em *parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="314d9-125">For this example, we saved the parameters file to *parameters.json*.</span></span>
4. <span data-ttu-id="314d9-126">Execute o comando **azure group deployment create** para implantar o novo balanceador de carga interno usando o modelo e os arquivos de parâmetro baixados e modificados acima.</span><span class="sxs-lookup"><span data-stu-id="314d9-126">Run the **azure group deployment create** command to deploy the new internal load balancer by using the template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="314d9-127">A lista exibida após a saída explicar os parâmetros usados.</span><span class="sxs-lookup"><span data-stu-id="314d9-127">The list shown after the output explains the parameters used.</span></span>

    ```azurecli
    azure group create --name TestRG --location westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json --parameters-file parameters.json
    ```

## <a name="next-steps"></a><span data-ttu-id="314d9-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="314d9-128">Next steps</span></span>

[<span data-ttu-id="314d9-129">Configurar um modo de distribuição do balanceador de carga usando a afinidade de IP de origem</span><span class="sxs-lookup"><span data-stu-id="314d9-129">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="314d9-130">Definir configurações de tempo limite de TCP ocioso para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="314d9-130">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

