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
# <a name="creating-an-internet-facing-load-balancer-using-a-template"></a>Criar um balanceador de carga voltado para a Internet usando um modelo

> [!div class="op_single_selector"]
> * [Portal](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [CLI do Azure](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [Modelo](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Este artigo aborda o modelo de implantação do Gerenciador de recursos de saudação. Você também pode [Saiba como toocreate um voltados à Internet carregar balanceador usando o modelo de implantação clássico](load-balancer-get-started-internet-classic-portal.md)

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a>Implantar o modelo de saudação usando clique toodeploy

Olá modelo de exemplo disponível no repositório público Olá usa um arquivo de parâmetro que contém cenário saudação padrão valores usados toogenerate Olá descrito acima. toodeploy usando esse modelo clique toodeploy, execute [este link](http://go.microsoft.com/fwlink/?LinkId=544801), clique em **implantar tooAzure**, substitua os valores de parâmetro de padrão de saudação se necessário e siga as instruções de saudação no portal de saudação.

## <a name="deploy-hello-template-by-using-powershell"></a>Implante o modelo de saudação usando o PowerShell

modelo de saudação toodeploy baixados usando o PowerShell, execute as etapas de saudação abaixo.

1. Se você nunca usou o Azure PowerShell, consulte [como tooInstall e configurar o Azure PowerShell](/powershell/azure/overview) e siga as instruções Olá todos os toohello de maneira Olá terminar toosign no Azure e selecione sua assinatura.
2. Executar Olá **AzureRmResourceGroupDeployment novo** Olá de cmdlet toocreate um grupo de recursos usando o modelo.

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestRG -Location uswest `
        -TemplateFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' `
        -TemplateParameterFile 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.parameters.json'
    ```

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a>Implantar o modelo hello usando Olá CLI do Azure

modelo de saudação toodeploy usando Olá CLI do Azure, siga as etapas de saudação abaixo.

1. Se você nunca tiver usado a CLI do Azure, consulte [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md) e siga as instruções de saudação toohello ponto em que você selecione sua conta do Azure e assinatura.
2. Executar Olá **modo de configuração do azure** modo do Gerenciador de tooResource do comando tooswitch, conforme mostrado abaixo.

    ```azurecli
    azure config mode arm
    ```

    Aqui está a saída Olá esperado para o comando de saudação acima:

        info:    New mode is arm

3. Em seu navegador, navegue muito[Olá Quickstart modelo](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-loadbalancer-lbrules), conteúdo de saudação do arquivo json de saudação de copiar e colar em um novo arquivo em seu computador. Para este cenário, deve copiar valores hello abaixo arquivo tooa chamado **c:\lb\azuredeploy.parameters.json**.
4. Executar Olá **criar implantação de grupo do azure** cmdlet toodeploy Olá novo balanceador de carga usando o modelo de saudação e parâmetro arquivos que você baixou e modificado acima. lista de saudação mostrada após a saída de hello explica parâmetros Olá usados.

    ```azurecli
    azure group create --name TestRG --location westus --template-file 'https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json' --parameters-file 'c:\lb\azuredeploy.parameters.json'
    ```

## <a name="next-steps"></a>Próximas etapas

[Introdução à configuração de um balanceador de carga interno](load-balancer-get-started-ilb-arm-ps.md)

[Configurar um modo de distribuição do balanceador de carga](load-balancer-distribution-mode.md)

[Definir configurações de tempo limite de TCP ocioso para o balanceador de carga](load-balancer-tcp-idle-timeout.md)
