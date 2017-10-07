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
# <a name="create-an-internal-load-balancer-using-a-template"></a>Criar um balanceador de carga interno usando um modelo

> [!div class="op_single_selector"]
> * [Portal do Azure](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [CLI do Azure](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Modelo](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../azure-resource-manager/resource-manager-deployment-model.md).  Este artigo aborda usando o modelo de implantação do hello Gerenciador de recursos, a Microsoft recomenda para a maioria das novas implantações em vez da saudação [modelo de implantação clássico](load-balancer-get-started-ilb-classic-ps.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-template-by-using-click-toodeploy"></a>Implantar o modelo de saudação usando clique toodeploy

Olá modelo de exemplo disponível no repositório público Olá usa um arquivo de parâmetro que contém cenário saudação padrão valores usados toogenerate Olá descrito acima. toodeploy usando esse modelo clique toodeploy, execute [este link](https://github.com/Azure/azure-quickstart-templates/tree/master/201-2-vms-internal-load-balancer), clique em **implantar tooAzure**, substitua os valores de parâmetro de padrão de saudação se necessário e siga as instruções de saudação no portal de saudação.

## <a name="deploy-hello-template-by-using-powershell"></a>Implante o modelo de saudação usando o PowerShell

modelo de saudação toodeploy baixados usando o PowerShell, execute as etapas de saudação abaixo.

1. Se você nunca usou o Azure PowerShell, consulte [como tooInstall e configurar o Azure PowerShell](/powershell/azure/overview) e siga as instruções Olá todos os toohello de maneira Olá terminar toosign no Azure e selecione sua assinatura.
2. Baixe o disco local do tooyour do arquivo hello parâmetros.
3. Edite o arquivo hello e salvá-lo.
4. Executar Olá **AzureRmResourceGroupDeployment novo** Olá de cmdlet toocreate um grupo de recursos usando o modelo.

    ```azurecli
    New-AzureRmResourceGroupDeployment -Name TestRG -Location westus `
        -TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json' `
        -TemplateParameterFile 'C:\temp\azuredeploy.parameters.json'
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

3. Abra o arquivo de parâmetro hello, selecione seu conteúdo e salve-o arquivo tooa no seu computador. Neste exemplo, nós salvamos o arquivo de parâmetros Olá muito*parameters.json*.
4. Executar Olá **criar implantação de grupo do azure** toodeploy Olá novo balanceador de carga interno usando o modelo de saudação e o parâmetro de comando arquivos que você baixou e modificado acima. lista de saudação mostrada após a saída de hello explica parâmetros Olá usados.

    ```azurecli
    azure group create --name TestRG --location westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-internal-load-balancer/azuredeploy.json --parameters-file parameters.json
    ```

## <a name="next-steps"></a>Próximas etapas

[Configurar um modo de distribuição do balanceador de carga usando a afinidade de IP de origem](load-balancer-distribution-mode.md)

[Definir configurações de tempo limite de TCP ocioso para o balanceador de carga](load-balancer-tcp-idle-timeout.md)

