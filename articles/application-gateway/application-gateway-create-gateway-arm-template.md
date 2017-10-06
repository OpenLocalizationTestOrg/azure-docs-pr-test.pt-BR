---
title: um Gateway de aplicativo do Azure - modelos de aaaCreate | Microsoft Docs
description: "Esta página fornece instruções toocreate um gateway de aplicativo do Azure usando o modelo do Azure Resource Manager Olá"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: fc18e553852551326d6a302abe2c7f8a08c2eb6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-resource-manager-template"></a>Criar um gateway de aplicativo usando o modelo do Azure Resource Manager Olá

> [!div class="op_single_selector"]
> * [Portal do Azure](application-gateway-create-gateway-portal.md)
> * [PowerShell do Azure Resource Manager](application-gateway-create-gateway-arm.md)
> * [Azure Classic PowerShell](application-gateway-create-gateway.md)
> * [Modelo do Azure Resource Manager](application-gateway-create-gateway-arm-template.md)
> * [CLI do Azure](application-gateway-create-gateway-cli.md)

O Gateway de Aplicativo do Azure é um balanceador de carga de camada 7. Ele fornece failover e roteamento de desempenho de solicitações HTTP entre diferentes servidores, independentemente de estarem em nuvem hello ou local. O Gateway de Aplicativo fornece muitos recursos do ADC (Controlador de entrega de aplicativos), incluindo o balanceamento de carga de HTTP, a afinidade de sessão baseada em cookies, o descarregamento de protocolo SSL (Secure Sockets Layer), as sondas de integridade personalizadas, suporte para vários sites e muitos outros. toofind uma lista completa de recursos com suporte, visite [visão geral do Application Gateway](application-gateway-introduction.md)

Este artigo o orienta por meio do download e modificando um modelo existente do Gerenciador de recursos do Azure do GitHub e implantar o modelo de saudação do GitHub, PowerShell e Olá CLI do Azure.

Se você simplesmente estiver implantando o modelo do Azure Resource Manager Olá diretamente do GitHub sem alterações, ignore toodeploy um modelo do GitHub.

## <a name="scenario"></a>Cenário

Neste cenário, você:

* Crie um Gateway de Aplicativo com o firewall do aplicativo Web.
* Criará uma rede virtual chamada VirtualNetwork1, com um bloco CIDR 10.0.0.0/16 reservado.
* Criará uma sub-rede chamada Appgatewaysubnet que usa 10.0.0.0/28 como seu bloco CIDR.
* Configurar dois IPs de back-end configurado anteriormente para servidores de web hello que deseja tooload Olá balancear. Neste exemplo de modelo, hello IPs de back-end são 10.0.1.10 e 10.0.1.11.

> [!NOTE]
> Essas configurações são parâmetros de saudação para este modelo. modelo de saudação toocustomize, você pode alterar regras, ouvinte hello, SSL e outras opções no arquivo de azuredeploy.json hello.

![Cenário](./media/application-gateway-create-gateway-arm-template/scenario.png)

## <a name="download-and-understand-hello-azure-resource-manager-template"></a>Baixe e entender o modelo do Azure Resource Manager Olá

Você pode baixar Olá existente do Azure Resource Manager modelo toocreate uma rede virtual e duas sub-redes do GitHub, faça as alterações que você pode desejar e reutilizá-la. Assim, o toodo use Olá etapas a seguir:

1. Navegue muito[criar Gateway de aplicativo com o firewall do aplicativo da web habilitado](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).
1. Clique em **azuredeploy.json** e em **RAW**.
1. Salve a pasta local do arquivo de saudação tooa em seu computador.
1. Se você estiver familiarizado com modelos do Azure Resource Manager, ignore toostep 7.
1. Abrir arquivo hello que você salvou e examine o conteúdo de saudação em **parâmetros** na linha
1. Os parâmetros do modelo do Gerenciador de Recursos do Azure fornecem um espaço reservado para valores que podem ser preenchidos durante a implantação.

  | Parâmetro | Descrição |
  | --- | --- |
  | **subnetPrefix** |Bloco CIDR para a sub-rede de gateway do aplicativo hello. |
  | **applicationGatewaySize** | Tamanho do gateway de aplicativo hello.  O WAF permite apenas médio e grande. |
  | **backendIpaddress1** |Endereço IP do primeiro servidor de web hello. |
  | **backendIpaddress2** |Endereço IP do servidor web da segunda hello. |
  | **wafEnabled** | Configuração toodetermine se WAF está habilitado.|
  | **wafMode** | Modo de firewall do aplicativo web hello.  As opções disponíveis são **prevenção** ou **detecção**.|
  | **wafRuleSetType** | Tipo de conjunto de regras para WAF.  No momento OWASP é a opção Olá somente com suporte. |
  | **wafRuleSetVersion** |Versão de conjunto de regras. OWASP CRS 2.2.9 e o 3.0 estão opções Olá com suporte. |

1. Verifique o conteúdo Olá **recursos** e observe Olá seguintes propriedades:

   * **type**. Tipo de recurso que está sendo criado pelo modelo de saudação. Nesse caso, o tipo de saudação é `Microsoft.Network/applicationGateways`, que representa um application gateway.
   * **name**. Nome de recurso de saudação. Uso de saudação de aviso de `[parameters('applicationGatewayName')]`, que significa que esse nome hello é fornecido como entrada por você ou por um arquivo de parâmetro durante a implantação.
   * **properties**. Lista de propriedades para o recurso de saudação. Este modelo usa o endereço IP público e rede virtual Olá durante a criação de gateway do aplicativo.

   > [!NOTE]
   > Para obter mais informações sobre modelos, visite: [Referência de modelos do Resource Manager](/templates/)

1. Navegue de volta muito[https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).
1. Clique em **azuredeploy-parameters.json** e em **RAW**.
1. Salve a pasta local do arquivo de saudação tooa em seu computador.
1. Abrir o arquivo hello que você salvou e editar Olá valores para parâmetros de saudação. Use Olá gateway valores toodeploy Olá aplicativo descrito em nosso cenário a seguir.

    ```json
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "addressPrefix": {
            "value": "10.0.0.0/16"
            },
            "subnetPrefix": {
            "value": "10.0.0.0/28"
            },
            "applicationGatewaySize": {
            "value": "WAF_Medium"
            },
            "capacity": {
            "value": 2
            },
            "backendIpAddress1": {
            "value": "10.0.1.10"
            },
            "backendIpAddress2": {
            "value": "10.0.1.11"
            },
            "wafEnabled": {
            "value": true
            },
            "wafMode": {
            "value": "Detection"
            },
            "wafRuleSetType": {
            "value": "OWASP"
            },
            "wafRuleSetVersion": {
            "value": "3.0"
            }
        }
    }
    ```

1. Salve o arquivo hello. Você pode testar Olá JSON parâmetro modelos e usando ferramentas de validação de JSON online como [JSlint.com](http://www.jslint.com/).

## <a name="deploy-hello-azure-resource-manager-template-by-using-powershell"></a>Implantar o modelo do Azure Resource Manager Olá usando o PowerShell

Se você nunca usou o Azure PowerShell, visite: [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) e siga Olá instruções toosign no Azure e selecione sua assinatura.

1. TooPowerShell de logon

    ```powershell
    Login-AzureRmAccount
    ```

1. Verificar as assinaturas de saudação para conta de saudação.

    ```powershell
    Get-AzureRmSubscription
    ```

    Você está tooauthenticate solicitado com suas credenciais.

1. Escolha qual toouse suas assinaturas do Azure.

    ```powershell
    Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
    ```

1. Se necessário, crie um grupo de recursos usando Olá **AzureResourceGroup novo** cmdlet. Em Olá exemplo a seguir, você deve criar um grupo de recursos chamado AppgatewayRG no local do Leste dos EUA.

    ```powershell
    New-AzureRmResourceGroup -Name AppgatewayRG -Location "West US"
    ```

1. Executar Olá **AzureRmResourceGroupDeployment novo** cmdlet toodeploy Olá nova rede virtual usando Olá anteriores de arquivos de modelo e o parâmetro baixado e modificado.
    
    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestAppgatewayDeployment -ResourceGroupName AppgatewayRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-hello-azure-cli"></a>Implantar o modelo do Azure Resource Manager hello usando Olá CLI do Azure

modelo de Gerenciador de recursos do Azure Olá toodeploy baixado usando a CLI do Azure, siga Olá etapas a seguir:

1. Se você nunca tiver usado a CLI do Azure, consulte [instalar e configurar Olá CLI do Azure](/cli/azure/install-azure-cli) e siga as instruções de saudação toohello ponto em que você selecione sua conta do Azure e assinatura.

1. Se necessário, execute hello `az group create` comando toocreate um grupo de recursos, conforme mostrado no trecho de código a seguir de saudação. Observe a saída de saudação do comando de saudação. lista de saudação mostrada após a saída de hello explica parâmetros Olá usados. Para saber mais sobre grupos de recursos, visite [Visão geral do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).

    ```azurecli
    az group create --location westus --name appgatewayRG
    ```
    
    **-n (or --name)**. Nome para o novo grupo de recursos hello. Para nosso cenário, é *appgatewayRG*.
    
    **-l (ou --location)**. Região do Azure onde o novo grupo de recursos Olá é criado. Para nosso cenário, esse grupo é *westus*.

1. Executar Olá `az group deployment create` cmdlet toodeploy Olá nova rede virtual usando o modelo de saudação e parâmetro arquivos que você baixou e modificadas no hello anterior da etapa. lista de saudação mostrada após a saída de hello explica parâmetros Olá usados.

    ```azurecli
    az group deployment create --resource-group appgatewayRG --name TestAppgatewayDeployment --template-file azuredeploy.json --parameters @azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-click-to-deploy"></a>Implante o modelo de Gerenciador de recursos do Azure hello usando clique para implantar

Clique em implantar é toouse de outra maneira modelos do Gerenciador de recursos do Azure. É um modelos de toouse de maneira fácil com hello portal do Azure.

1. Vá muito[criar um gateway de aplicativos com o firewall do aplicativo web](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).

1. Clique em **implantar tooAzure**.

    ![Implantar tooAzure](./media/application-gateway-create-gateway-arm-template/deploytoazure.png)
    
1. Insira parâmetros Olá para o modelo de implantação Olá no portal de saudação e clique em **Okey**.

    ![parâmetros](./media/application-gateway-create-gateway-arm-template/ibiza1.png)
    
1. Selecione **concordo toohello termos e condições declaradas acima** e clique em **compra**.

1. Na folha de implantação do hello personalizada, clique em **criar**.

## <a name="providing-certificate-data-tooresource-manager-templates"></a>Fornecendo Gerenciador de modelos de certificado dados tooResource

Ao usar o SSL com um modelo, o certificado de saudação deve toobe fornecido em uma cadeia de caracteres base64 em vez de ser carregado. tooconvert. pfx ou. cer tooa em base64 de cadeia de caracteres use um dos comandos a seguir de saudação. Olá seguintes comandos convertem Olá certificado tooa cadeia de caracteres base64, que pode ser fornecida toohello modelo. Olá esperado a saída é uma cadeia de caracteres que pode ser armazenada em uma variável e colada no modelo de saudação.

### <a name="macos"></a>macOS
```bash
cert=$( base64 <certificate path and name>.pfx )
echo $cert
```

### <a name="windows"></a>Windows
```powershell
[System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("<certificate path and name>.pfx"))
```

## <a name="delete-all-resources"></a>Excluir todos os recursos

toodelete todos os recursos criados neste artigo, complete um dos Olá etapas a seguir:

### <a name="powershell"></a>PowerShell

```powershell
Remove-AzureRmResourceGroup -Name appgatewayRG
```

### <a name="azure-cli"></a>CLI do Azure

```azurecli
az group delete --name appgatewayRG
```

## <a name="next-steps"></a>Próximas etapas

Se você quiser tooconfigure descarregamento de SSL, visite: [Configure um gateway de aplicativo para descarregamento SSL](application-gateway-ssl.md).

Se você quiser tooconfigure um toouse de gateway do aplicativo com um balanceador de carga interno, visite: [criar um gateway de aplicativo com um balanceador de carga interno (ILB)](application-gateway-ilb.md).

Se deseja saber mais sobre as opções de balanceamento de carga no geral, visite:

* [Balanceador de carga do Azure](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Gerenciador de Tráfego do Azure](https://azure.microsoft.com/documentation/services/traffic-manager/)

