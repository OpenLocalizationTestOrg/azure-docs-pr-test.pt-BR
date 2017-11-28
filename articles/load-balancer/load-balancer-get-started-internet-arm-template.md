---
title: Balanceador de carga aaaCreate um voltados para Internet - modelo do Azure | Microsoft Docs
description: "Saiba como toocreate um voltados à Internet balanceador de carga no Resource Manager usando um modelo"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: b24f4729-4559-4458-8527-71009d242647
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 2bce8cb87303838f3bc732d51228ab46d8015552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-facing-load-balancer-using-a-template"></a><span data-ttu-id="9debf-103">Criar um balanceador de carga voltado para a Internet usando um modelo</span><span class="sxs-lookup"><span data-stu-id="9debf-103">Creating an Internet facing load balancer using a template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9debf-104">Portal</span><span class="sxs-lookup"><span data-stu-id="9debf-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="9debf-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9debf-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="9debf-106">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="9debf-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="9debf-107">Modelo</span><span class="sxs-lookup"><span data-stu-id="9debf-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="9debf-108">Este artigo aborda o modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="9debf-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="9debf-109">Você também pode [Saiba como toocreate um voltados à Internet carregar balanceador usando o modelo de implantação clássico](load-balancer-get-started-internet-classic-portal.md)</span><span class="sxs-lookup"><span data-stu-id="9debf-109">You can also [Learn how toocreate an Internet facing load balancer using classic deployment model](load-balancer-get-started-internet-classic-portal.md)</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a><span data-ttu-id="9debf-110">Implantar o modelo de saudação usando clique toodeploy</span><span class="sxs-lookup"><span data-stu-id="9debf-110">Deploy hello template by using click toodeploy</span></span>

<span data-ttu-id="9debf-111">Olá modelo de exemplo disponível no repositório público Olá usa um arquivo de parâmetro que contém cenário saudação padrão valores usados toogenerate Olá descrito acima.</span><span class="sxs-lookup"><span data-stu-id="9debf-111">hello sample template available in hello public repository uses a parameter file containing hello default values used toogenerate hello scenario described above.</span></span> <span data-ttu-id="9debf-112">toodeploy usando esse modelo clique toodeploy, execute [este link](http://go.microsoft.com/fwlink/?LinkId=544801), clique em **implantar tooAzure**, substitua os valores de parâmetro de padrão de saudação se necessário e siga as instruções de saudação no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="9debf-112">toodeploy this template using click toodeploy, follow [this link](http://go.microsoft.com/fwlink/?LinkId=544801), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

## <a name="deploy-hello-template-by-using-powershell"></a><span data-ttu-id="9debf-113">Implante o modelo de saudação usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="9debf-113">Deploy hello template by using PowerShell</span></span>

<span data-ttu-id="9debf-114">modelo de saudação toodeploy baixados usando o PowerShell, execute as etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="9debf-114">toodeploy hello template you downloaded by using PowerShell, follow hello steps below.</span></span>

1. <span data-ttu-id="9debf-115">Se você nunca usou o Azure PowerShell, consulte [como tooInstall e configurar o Azure PowerShell](/powershell/azure/overview) e siga as instruções Olá todos os toohello de maneira Olá terminar toosign no Azure e selecione sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="9debf-115">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="9debf-116">Executar Olá **AzureRmResourceGroupDeployment novo** Olá de cmdlet toocreate um grupo de recursos usando o modelo.</span><span class="sxs-lookup"><span data-stu-id="9debf-116">Run hello **New-AzureRmResourceGroupDeployment** cmdlet toocreate a resource group using hello template.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestRG -Location uswest `
        -TemplateFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' `
        -TemplateParameterFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.parameters.json'
    ```

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a><span data-ttu-id="9debf-117">Implantar o modelo hello usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="9debf-117">Deploy hello template by using hello Azure CLI</span></span>

<span data-ttu-id="9debf-118">modelo de saudação toodeploy usando Olá CLI do Azure, siga as etapas de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="9debf-118">toodeploy hello template by using hello Azure CLI, follow hello steps below.</span></span>

1. <span data-ttu-id="9debf-119">Se você nunca tiver usado a CLI do Azure, consulte [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md) e siga as instruções de saudação toohello ponto em que você selecione sua conta do Azure e assinatura.</span><span class="sxs-lookup"><span data-stu-id="9debf-119">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="9debf-120">Executar Olá **modo de configuração do azure** modo do Gerenciador de tooResource do comando tooswitch, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="9debf-120">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="9debf-121">Aqui está a saída Olá esperado para o comando de saudação acima:</span><span class="sxs-lookup"><span data-stu-id="9debf-121">Here is hello expected output for hello command above:</span></span>

        info:    New mode is arm

3. <span data-ttu-id="9debf-122">Em seu navegador, navegue muito[Olá Quickstart modelo](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules), conteúdo de saudação do arquivo json de saudação de copiar e colar em um novo arquivo em seu computador.</span><span class="sxs-lookup"><span data-stu-id="9debf-122">From your browser, navigate too[hello Quickstart Template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules), copy hello contents of hello json file and paste into a new file in your computer.</span></span> <span data-ttu-id="9debf-123">Para este cenário, deve copiar valores hello abaixo arquivo tooa chamado **c:\lb\azuredeploy.parameters.json**.</span><span class="sxs-lookup"><span data-stu-id="9debf-123">For this scenario, you would be copying hello values below tooa file named **c:\lb\azuredeploy.parameters.json**.</span></span>
4. <span data-ttu-id="9debf-124">Executar Olá **criar implantação de grupo do azure** cmdlet toodeploy Olá novo balanceador de carga usando o modelo de saudação e parâmetro arquivos que você baixou e modificado acima.</span><span class="sxs-lookup"><span data-stu-id="9debf-124">Run hello **azure group deployment create** cmdlet toodeploy hello new load balancer by using hello template and parameter files you downloaded and modified above.</span></span> <span data-ttu-id="9debf-125">lista de saudação mostrada após a saída de hello explica parâmetros Olá usados.</span><span class="sxs-lookup"><span data-stu-id="9debf-125">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    azure group create --name TestRG --location westus --template-file 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' --parameters-file 'c:\lb\azuredeploy.parameters.json'
    ```

## <a name="next-steps"></a><span data-ttu-id="9debf-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9debf-126">Next steps</span></span>

[<span data-ttu-id="9debf-127">Introdução à configuração de um balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="9debf-127">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="9debf-128">Configurar um modo de distribuição do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="9debf-128">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="9debf-129">Definir configurações de tempo limite de TCP ocioso para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="9debf-129">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
