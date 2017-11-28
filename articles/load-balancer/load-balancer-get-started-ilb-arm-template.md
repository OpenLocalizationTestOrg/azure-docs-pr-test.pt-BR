---
title: aaaCreate um balanceador de carga interno - modelo do Azure | Microsoft Docs
description: Saiba como o toocreate um interno balanceador usando um modelo no Gerenciador de recursos de carga
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
ms.openlocfilehash: 3ffa8178b863367cd79e2bc2b7ce4e45b23267e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-using-a-template"></a><span data-ttu-id="7b843-103">Criar um balanceador de carga interno usando um modelo</span><span class="sxs-lookup"><span data-stu-id="7b843-103">Create an internal load balancer using a template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7b843-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7b843-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="7b843-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7b843-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="7b843-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="7b843-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="7b843-107">Modelo</span><span class="sxs-lookup"><span data-stu-id="7b843-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="7b843-108">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7b843-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="7b843-109">Este artigo aborda usando o modelo de implantação do hello Gerenciador de recursos, a Microsoft recomenda para a maioria das novas implantações em vez da saudação [modelo de implantação clássico](load-balancer-get-started-ilb-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="7b843-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a><span data-ttu-id="7b843-110">Implantar o modelo de saudação usando clique toodeploy</span><span class="sxs-lookup"><span data-stu-id="7b843-110">Deploy hello template by using click toodeploy</span></span>

<span data-ttu-id="7b843-111">Olá modelo de exemplo disponível no repositório público Olá usa um arquivo de parâmetro que contém cenário saudação padrão valores usados toogenerate Olá descrito acima.</span><span class="sxs-lookup"><span data-stu-id="7b843-111">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="7b843-112">toodeploy usando esse modelo clique toodeploy, execute [este link](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), clique em **implantar tooAzure**, substitua os valores de parâmetro de padrão de saudação se necessário e siga as instruções de saudação no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="7b843-112">toodeploy this template using click toodeploy, follow [this link](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="7b843-113">Implante o modelo de saudação usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="7b843-113">Deploy hello template by using PowerShell</span></span>

<span data-ttu-id="7b843-114">modelo de saudação toodeploy baixados usando o PowerShell, execute as etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="7b843-114">toodeploy hello template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="7b843-115">Se você nunca usou o Azure PowerShell, consulte [como tooInstall e configurar o Azure PowerShell](/powershell/azure/overview) e siga as instruções Olá todos os toohello de maneira Olá terminar toosign no Azure e selecione sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="7b843-115">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="7b843-116">Baixe o disco local do tooyour do arquivo hello parâmetros.</span><span class="sxs-lookup"><span data-stu-id="7b843-116">Download hello parameters file tooyour local disk.</span></span>
3. <span data-ttu-id="7b843-117">Edite o arquivo hello e salvá-lo.</span><span class="sxs-lookup"><span data-stu-id="7b843-117">Edit hello file and save it.</span></span>
4. <span data-ttu-id="7b843-118">Executar Olá **AzureRmResourceGroupDeployment novo** Olá de cmdlet toocreate um grupo de recursos usando o modelo.</span><span class="sxs-lookup"><span data-stu-id="7b843-118">Run hello **New-AzureRmResourceGroupDeployment** cmdlet toocreate a resource group using hello template.</span></span>

    ```azurecli
    New-AzureRmResourceGroupDeployment -Name TestRG -Location westus `
        -TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json' `
        -TemplateParameterFile 'C:\temp\azuredeploy.parameters.json'
    ```

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="7b843-119">Implantar o modelo hello usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="7b843-119">Deploy hello template by using hello Azure CLI</span></span>

<span data-ttu-id="7b843-120">modelo de saudação toodeploy usando Olá CLI do Azure, siga as etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="7b843-120">toodeploy hello template by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="7b843-121">Se você nunca tiver usado a CLI do Azure, consulte [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md) e siga as instruções de saudação toohello ponto em que você selecione sua conta do Azure e assinatura.</span><span class="sxs-lookup"><span data-stu-id="7b843-121">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="7b843-122">Executar Olá **modo de configuração do azure** modo do Gerenciador de tooResource do comando tooswitch, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="7b843-122">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="7b843-123">Aqui está a saída Olá esperado para o comando de saudação acima:</span><span class="sxs-lookup"><span data-stu-id="7b843-123">Here is hello expected output for hello command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="7b843-124">Abra o arquivo de parâmetro hello, selecione seu conteúdo e salve-o arquivo tooa no seu computador.</span><span class="sxs-lookup"><span data-stu-id="7b843-124">Open hello parameter file, select its contents, and save it tooa file in your computer.</span></span> <span data-ttu-id="7b843-125">Neste exemplo, nós salvamos o arquivo de parâmetros Olá muito*parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="7b843-125">For this example, we saved hello parameters file too*parameters.json*.</span></span>
4. <span data-ttu-id="7b843-126">Executar Olá **criar implantação de grupo do azure** toodeploy Olá novo balanceador de carga interno usando o modelo de saudação e o parâmetro de comando arquivos que você baixou e modificado acima.</span><span class="sxs-lookup"><span data-stu-id="7b843-126">Run hello **azure group deployment create** command toodeploy hello new internal load balancer by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="7b843-127">lista de saudação mostrada após a saída de hello explica parâmetros Olá usados.</span><span class="sxs-lookup"><span data-stu-id="7b843-127">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    azure group create --name TestRG --location westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json --parameters-file parameters.json
    ```

## <a name="next-steps"></a><span data-ttu-id="7b843-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7b843-128">Next steps</span></span>

[<span data-ttu-id="7b843-129">Configurar um modo de distribuição do balanceador de carga usando a afinidade de IP de origem</span><span class="sxs-lookup"><span data-stu-id="7b843-129">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="7b843-130">Definir configurações de tempo limite de TCP ocioso para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="7b843-130">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

