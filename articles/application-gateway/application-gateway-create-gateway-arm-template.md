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
# <a name="create-an-application-gateway-by-using-hello-azure-resource-manager-template"></a><span data-ttu-id="63df1-103">Criar um gateway de aplicativo usando o modelo do Azure Resource Manager Olá</span><span class="sxs-lookup"><span data-stu-id="63df1-103">Create an application gateway by using hello Azure Resource Manager template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="63df1-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="63df1-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="63df1-105">PowerShell do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="63df1-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="63df1-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="63df1-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="63df1-107">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="63df1-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="63df1-108">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="63df1-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="63df1-109">O Gateway de Aplicativo do Azure é um balanceador de carga de camada 7.</span><span class="sxs-lookup"><span data-stu-id="63df1-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="63df1-110">Ele fornece failover e roteamento de desempenho de solicitações HTTP entre diferentes servidores, independentemente de estarem em nuvem hello ou local.</span><span class="sxs-lookup"><span data-stu-id="63df1-110">It provides failover and performance-routing HTTP requests between different servers, whether they are on hello cloud or on-premises.</span></span> <span data-ttu-id="63df1-111">O Gateway de Aplicativo fornece muitos recursos do ADC (Controlador de entrega de aplicativos), incluindo o balanceamento de carga de HTTP, a afinidade de sessão baseada em cookies, o descarregamento de protocolo SSL (Secure Sockets Layer), as sondas de integridade personalizadas, suporte para vários sites e muitos outros.</span><span class="sxs-lookup"><span data-stu-id="63df1-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="63df1-112">toofind uma lista completa de recursos com suporte, visite [visão geral do Application Gateway](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="63df1-112">toofind a complete list of supported features, visit [Application Gateway overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="63df1-113">Este artigo o orienta por meio do download e modificando um modelo existente do Gerenciador de recursos do Azure do GitHub e implantar o modelo de saudação do GitHub, PowerShell e Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="63df1-113">This article walks you through downloading and modifying an existing Azure Resource Manager template from GitHub and deploying hello template from GitHub, PowerShell, and hello Azure CLI.</span></span>

<span data-ttu-id="63df1-114">Se você simplesmente estiver implantando o modelo do Azure Resource Manager Olá diretamente do GitHub sem alterações, ignore toodeploy um modelo do GitHub.</span><span class="sxs-lookup"><span data-stu-id="63df1-114">If you are simply deploying hello Azure Resource Manager template directly from GitHub without any changes, skip toodeploy a template from GitHub.</span></span>

## <a name="scenario"></a><span data-ttu-id="63df1-115">Cenário</span><span class="sxs-lookup"><span data-stu-id="63df1-115">Scenario</span></span>

<span data-ttu-id="63df1-116">Neste cenário, você:</span><span class="sxs-lookup"><span data-stu-id="63df1-116">In this scenario you will:</span></span>

* <span data-ttu-id="63df1-117">Crie um Gateway de Aplicativo com o firewall do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="63df1-117">Create an application gateway with web application firewall.</span></span>
* <span data-ttu-id="63df1-118">Criará uma rede virtual chamada VirtualNetwork1, com um bloco CIDR 10.0.0.0/16 reservado.</span><span class="sxs-lookup"><span data-stu-id="63df1-118">Create a virtual network named VirtualNetwork1 with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="63df1-119">Criará uma sub-rede chamada Appgatewaysubnet que usa 10.0.0.0/28 como seu bloco CIDR.</span><span class="sxs-lookup"><span data-stu-id="63df1-119">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>
* <span data-ttu-id="63df1-120">Configurar dois IPs de back-end configurado anteriormente para servidores de web hello que deseja tooload Olá balancear.</span><span class="sxs-lookup"><span data-stu-id="63df1-120">Set up two previously configured back-end IPs for hello web servers you want tooload balance hello traffic.</span></span> <span data-ttu-id="63df1-121">Neste exemplo de modelo, hello IPs de back-end são 10.0.1.10 e 10.0.1.11.</span><span class="sxs-lookup"><span data-stu-id="63df1-121">In this template example, hello back-end IPs are 10.0.1.10 and 10.0.1.11.</span></span>

> [!NOTE]
> <span data-ttu-id="63df1-122">Essas configurações são parâmetros de saudação para este modelo.</span><span class="sxs-lookup"><span data-stu-id="63df1-122">Those settings are hello parameters for this template.</span></span> <span data-ttu-id="63df1-123">modelo de saudação toocustomize, você pode alterar regras, ouvinte hello, SSL e outras opções no arquivo de azuredeploy.json hello.</span><span class="sxs-lookup"><span data-stu-id="63df1-123">toocustomize hello template, you can change rules, hello listener, SSL, and other options in hello azuredeploy.json file.</span></span>

![Cenário](./media/application-gateway-create-gateway-arm-template/scenario.png)

## <a name="download-and-understand-hello-azure-resource-manager-template"></a><span data-ttu-id="63df1-125">Baixe e entender o modelo do Azure Resource Manager Olá</span><span class="sxs-lookup"><span data-stu-id="63df1-125">Download and understand hello Azure Resource Manager template</span></span>

<span data-ttu-id="63df1-126">Você pode baixar Olá existente do Azure Resource Manager modelo toocreate uma rede virtual e duas sub-redes do GitHub, faça as alterações que você pode desejar e reutilizá-la.</span><span class="sxs-lookup"><span data-stu-id="63df1-126">You can download hello existing Azure Resource Manager template toocreate a virtual network and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="63df1-127">Assim, o toodo use Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="63df1-127">toodo so, use hello following steps:</span></span>

1. <span data-ttu-id="63df1-128">Navegue muito[criar Gateway de aplicativo com o firewall do aplicativo da web habilitado](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span><span class="sxs-lookup"><span data-stu-id="63df1-128">Navigate too[Create Application Gateway with web application firewall enabled](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="63df1-129">Clique em **azuredeploy.json** e em **RAW**.</span><span class="sxs-lookup"><span data-stu-id="63df1-129">Click **azuredeploy.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="63df1-130">Salve a pasta local do arquivo de saudação tooa em seu computador.</span><span class="sxs-lookup"><span data-stu-id="63df1-130">Save hello file tooa local folder on your computer.</span></span>
1. <span data-ttu-id="63df1-131">Se você estiver familiarizado com modelos do Azure Resource Manager, ignore toostep 7.</span><span class="sxs-lookup"><span data-stu-id="63df1-131">If you are familiar with Azure Resource Manager templates, skip toostep 7.</span></span>
1. <span data-ttu-id="63df1-132">Abrir arquivo hello que você salvou e examine o conteúdo de saudação em **parâmetros** na linha</span><span class="sxs-lookup"><span data-stu-id="63df1-132">Open hello file that you saved and look at hello contents under **parameters** in line</span></span>
1. <span data-ttu-id="63df1-133">Os parâmetros do modelo do Gerenciador de Recursos do Azure fornecem um espaço reservado para valores que podem ser preenchidos durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="63df1-133">Azure Resource Manager template parameters provide a placeholder for values that can be filled out during deployment.</span></span>

  | <span data-ttu-id="63df1-134">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="63df1-134">Parameter</span></span> | <span data-ttu-id="63df1-135">Descrição</span><span class="sxs-lookup"><span data-stu-id="63df1-135">Description</span></span> |
  | --- | --- |
  | <span data-ttu-id="63df1-136">**subnetPrefix**</span><span class="sxs-lookup"><span data-stu-id="63df1-136">**subnetPrefix**</span></span> |<span data-ttu-id="63df1-137">Bloco CIDR para a sub-rede de gateway do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="63df1-137">CIDR block for hello application gateway subnet.</span></span> |
  | <span data-ttu-id="63df1-138">**applicationGatewaySize**</span><span class="sxs-lookup"><span data-stu-id="63df1-138">**applicationGatewaySize**</span></span> | <span data-ttu-id="63df1-139">Tamanho do gateway de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="63df1-139">Size of hello application gateway.</span></span>  <span data-ttu-id="63df1-140">O WAF permite apenas médio e grande.</span><span class="sxs-lookup"><span data-stu-id="63df1-140">WAF only allows medium and large.</span></span> |
  | <span data-ttu-id="63df1-141">**backendIpaddress1**</span><span class="sxs-lookup"><span data-stu-id="63df1-141">**backendIpaddress1**</span></span> |<span data-ttu-id="63df1-142">Endereço IP do primeiro servidor de web hello.</span><span class="sxs-lookup"><span data-stu-id="63df1-142">IP address of hello first web server.</span></span> |
  | <span data-ttu-id="63df1-143">**backendIpaddress2**</span><span class="sxs-lookup"><span data-stu-id="63df1-143">**backendIpaddress2**</span></span> |<span data-ttu-id="63df1-144">Endereço IP do servidor web da segunda hello.</span><span class="sxs-lookup"><span data-stu-id="63df1-144">IP address of hello second web server.</span></span> |
  | <span data-ttu-id="63df1-145">**wafEnabled**</span><span class="sxs-lookup"><span data-stu-id="63df1-145">**wafEnabled**</span></span> | <span data-ttu-id="63df1-146">Configuração toodetermine se WAF está habilitado.</span><span class="sxs-lookup"><span data-stu-id="63df1-146">Setting toodetermine if WAF is enabled.</span></span>|
  | <span data-ttu-id="63df1-147">**wafMode**</span><span class="sxs-lookup"><span data-stu-id="63df1-147">**wafMode**</span></span> | <span data-ttu-id="63df1-148">Modo de firewall do aplicativo web hello.</span><span class="sxs-lookup"><span data-stu-id="63df1-148">Mode of hello web application firewall.</span></span>  <span data-ttu-id="63df1-149">As opções disponíveis são **prevenção** ou **detecção**.</span><span class="sxs-lookup"><span data-stu-id="63df1-149">Available options are **prevention** or **detection**.</span></span>|
  | <span data-ttu-id="63df1-150">**wafRuleSetType**</span><span class="sxs-lookup"><span data-stu-id="63df1-150">**wafRuleSetType**</span></span> | <span data-ttu-id="63df1-151">Tipo de conjunto de regras para WAF.</span><span class="sxs-lookup"><span data-stu-id="63df1-151">Ruleset type for WAF.</span></span>  <span data-ttu-id="63df1-152">No momento OWASP é a opção Olá somente com suporte.</span><span class="sxs-lookup"><span data-stu-id="63df1-152">Currently OWASP is hello only supported option.</span></span> |
  | <span data-ttu-id="63df1-153">**wafRuleSetVersion**</span><span class="sxs-lookup"><span data-stu-id="63df1-153">**wafRuleSetVersion**</span></span> |<span data-ttu-id="63df1-154">Versão de conjunto de regras.</span><span class="sxs-lookup"><span data-stu-id="63df1-154">Ruleset version.</span></span> <span data-ttu-id="63df1-155">OWASP CRS 2.2.9 e o 3.0 estão opções Olá com suporte.</span><span class="sxs-lookup"><span data-stu-id="63df1-155">OWASP CRS 2.2.9 and 3.0 are currently hello supported options.</span></span> |

1. <span data-ttu-id="63df1-156">Verifique o conteúdo Olá **recursos** e observe Olá seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="63df1-156">Check hello content under **resources** and notice hello following properties:</span></span>

   * <span data-ttu-id="63df1-157">**type**.</span><span class="sxs-lookup"><span data-stu-id="63df1-157">**type**.</span></span> <span data-ttu-id="63df1-158">Tipo de recurso que está sendo criado pelo modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="63df1-158">Type of resource being created by hello template.</span></span> <span data-ttu-id="63df1-159">Nesse caso, o tipo de saudação é `Microsoft.Network/applicationGateways`, que representa um application gateway.</span><span class="sxs-lookup"><span data-stu-id="63df1-159">In this case, hello type is `Microsoft.Network/applicationGateways`, which represents an application gateway.</span></span>
   * <span data-ttu-id="63df1-160">**name**.</span><span class="sxs-lookup"><span data-stu-id="63df1-160">**name**.</span></span> <span data-ttu-id="63df1-161">Nome de recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="63df1-161">Name for hello resource.</span></span> <span data-ttu-id="63df1-162">Uso de saudação de aviso de `[parameters('applicationGatewayName')]`, que significa que esse nome hello é fornecido como entrada por você ou por um arquivo de parâmetro durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="63df1-162">Notice hello use of `[parameters('applicationGatewayName')]`, which means that hello name is provided as input by you or by a parameter file during deployment.</span></span>
   * <span data-ttu-id="63df1-163">**properties**.</span><span class="sxs-lookup"><span data-stu-id="63df1-163">**properties**.</span></span> <span data-ttu-id="63df1-164">Lista de propriedades para o recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="63df1-164">List of properties for hello resource.</span></span> <span data-ttu-id="63df1-165">Este modelo usa o endereço IP público e rede virtual Olá durante a criação de gateway do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="63df1-165">This template uses hello virtual network and public IP address during application gateway creation.</span></span>

   > [!NOTE]
   > <span data-ttu-id="63df1-166">Para obter mais informações sobre modelos, visite: [Referência de modelos do Resource Manager](/templates/)</span><span class="sxs-lookup"><span data-stu-id="63df1-166">For more information on templates visit: [Resource Manager templates reference](/templates/)</span></span>

1. <span data-ttu-id="63df1-167">Navegue de volta muito[https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span><span class="sxs-lookup"><span data-stu-id="63df1-167">Navigate back too[https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="63df1-168">Clique em **azuredeploy-parameters.json** e em **RAW**.</span><span class="sxs-lookup"><span data-stu-id="63df1-168">Click **azuredeploy-parameters.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="63df1-169">Salve a pasta local do arquivo de saudação tooa em seu computador.</span><span class="sxs-lookup"><span data-stu-id="63df1-169">Save hello file tooa local folder on your computer.</span></span>
1. <span data-ttu-id="63df1-170">Abrir o arquivo hello que você salvou e editar Olá valores para parâmetros de saudação.</span><span class="sxs-lookup"><span data-stu-id="63df1-170">Open hello file that you saved and edit hello values for hello parameters.</span></span> <span data-ttu-id="63df1-171">Use Olá gateway valores toodeploy Olá aplicativo descrito em nosso cenário a seguir.</span><span class="sxs-lookup"><span data-stu-id="63df1-171">Use hello following values toodeploy hello application gateway described in our scenario.</span></span>

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

1. <span data-ttu-id="63df1-172">Salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="63df1-172">Save hello file.</span></span> <span data-ttu-id="63df1-173">Você pode testar Olá JSON parâmetro modelos e usando ferramentas de validação de JSON online como [JSlint.com](http://www.jslint.com/).</span><span class="sxs-lookup"><span data-stu-id="63df1-173">You can test hello JSON template and parameter template by using online JSON validation tools like [JSlint.com](http://www.jslint.com/).</span></span>

## <a name="deploy-hello-azure-resource-manager-template-by-using-powershell"></a><span data-ttu-id="63df1-174">Implantar o modelo do Azure Resource Manager Olá usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="63df1-174">Deploy hello Azure Resource Manager template by using PowerShell</span></span>

<span data-ttu-id="63df1-175">Se você nunca usou o Azure PowerShell, visite: [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) e siga Olá instruções toosign no Azure e selecione sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="63df1-175">If you have never used Azure PowerShell, visit: [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions toosign into Azure and select your subscription.</span></span>

1. <span data-ttu-id="63df1-176">TooPowerShell de logon</span><span class="sxs-lookup"><span data-stu-id="63df1-176">Login tooPowerShell</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="63df1-177">Verificar as assinaturas de saudação para conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="63df1-177">Check hello subscriptions for hello account.</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

    <span data-ttu-id="63df1-178">Você está tooauthenticate solicitado com suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="63df1-178">You are prompted tooauthenticate with your credentials.</span></span>

1. <span data-ttu-id="63df1-179">Escolha qual toouse suas assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="63df1-179">Choose which of your Azure subscriptions toouse.</span></span>

    ```powershell
    Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
    ```

1. <span data-ttu-id="63df1-180">Se necessário, crie um grupo de recursos usando Olá **AzureResourceGroup novo** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="63df1-180">If needed, create a resource group by using hello **New-AzureResourceGroup** cmdlet.</span></span> <span data-ttu-id="63df1-181">Em Olá exemplo a seguir, você deve criar um grupo de recursos chamado AppgatewayRG no local do Leste dos EUA.</span><span class="sxs-lookup"><span data-stu-id="63df1-181">In hello following example, you create a resource group called AppgatewayRG in East US location.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name AppgatewayRG -Location "West US"
    ```

1. <span data-ttu-id="63df1-182">Executar Olá **AzureRmResourceGroupDeployment novo** cmdlet toodeploy Olá nova rede virtual usando Olá anteriores de arquivos de modelo e o parâmetro baixado e modificado.</span><span class="sxs-lookup"><span data-stu-id="63df1-182">Run hello **New-AzureRmResourceGroupDeployment** cmdlet toodeploy hello new virtual network by using hello preceding template and parameter files you downloaded and modified.</span></span>
    
    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestAppgatewayDeployment -ResourceGroupName AppgatewayRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-hello-azure-cli"></a><span data-ttu-id="63df1-183">Implantar o modelo do Azure Resource Manager hello usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="63df1-183">Deploy hello Azure Resource Manager template by using hello Azure CLI</span></span>

<span data-ttu-id="63df1-184">modelo de Gerenciador de recursos do Azure Olá toodeploy baixado usando a CLI do Azure, siga Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="63df1-184">toodeploy hello Azure Resource Manager template you downloaded by using Azure CLI, follow hello following steps:</span></span>

1. <span data-ttu-id="63df1-185">Se você nunca tiver usado a CLI do Azure, consulte [instalar e configurar Olá CLI do Azure](/cli/azure/install-azure-cli) e siga as instruções de saudação toohello ponto em que você selecione sua conta do Azure e assinatura.</span><span class="sxs-lookup"><span data-stu-id="63df1-185">If you have never used Azure CLI, see [Install and configure hello Azure CLI](/cli/azure/install-azure-cli) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>

1. <span data-ttu-id="63df1-186">Se necessário, execute hello `az group create` comando toocreate um grupo de recursos, conforme mostrado no trecho de código a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="63df1-186">If necessary, run hello `az group create` command toocreate a resource group, as shown in hello following code snippet.</span></span> <span data-ttu-id="63df1-187">Observe a saída de saudação do comando de saudação.</span><span class="sxs-lookup"><span data-stu-id="63df1-187">Notice hello output of hello command.</span></span> <span data-ttu-id="63df1-188">lista de saudação mostrada após a saída de hello explica parâmetros Olá usados.</span><span class="sxs-lookup"><span data-stu-id="63df1-188">hello list shown after hello output explains hello parameters used.</span></span> <span data-ttu-id="63df1-189">Para saber mais sobre grupos de recursos, visite [Visão geral do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="63df1-189">For more information about resource groups, visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```azurecli
    az group create --location westus --name appgatewayRG
    ```
    
    <span data-ttu-id="63df1-190">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="63df1-190">**-n (or --name)**.</span></span> <span data-ttu-id="63df1-191">Nome para o novo grupo de recursos hello.</span><span class="sxs-lookup"><span data-stu-id="63df1-191">Name for hello new resource group.</span></span> <span data-ttu-id="63df1-192">Para nosso cenário, é *appgatewayRG*.</span><span class="sxs-lookup"><span data-stu-id="63df1-192">For our scenario, it's *appgatewayRG*.</span></span>
    
    <span data-ttu-id="63df1-193">**-l (ou --location)**.</span><span class="sxs-lookup"><span data-stu-id="63df1-193">**-l (or --location)**.</span></span> <span data-ttu-id="63df1-194">Região do Azure onde o novo grupo de recursos Olá é criado.</span><span class="sxs-lookup"><span data-stu-id="63df1-194">Azure region where hello new resource group is created.</span></span> <span data-ttu-id="63df1-195">Para nosso cenário, esse grupo é *westus*.</span><span class="sxs-lookup"><span data-stu-id="63df1-195">For our scenario, it's *westus*.</span></span>

1. <span data-ttu-id="63df1-196">Executar Olá `az group deployment create` cmdlet toodeploy Olá nova rede virtual usando o modelo de saudação e parâmetro arquivos que você baixou e modificadas no hello anterior da etapa.</span><span class="sxs-lookup"><span data-stu-id="63df1-196">Run hello `az group deployment create` cmdlet toodeploy hello new virtual network by using hello template and parameter files you downloaded and modified in hello preceding step.</span></span> <span data-ttu-id="63df1-197">lista de saudação mostrada após a saída de hello explica parâmetros Olá usados.</span><span class="sxs-lookup"><span data-stu-id="63df1-197">hello list shown after hello output explains hello parameters used.</span></span>

    ```azurecli
    az group deployment create --resource-group appgatewayRG --name TestAppgatewayDeployment --template-file azuredeploy.json --parameters @azuredeploy-parameters.json
    ```

## <a name="deploy-hello-azure-resource-manager-template-by-using-click-to-deploy"></a><span data-ttu-id="63df1-198">Implante o modelo de Gerenciador de recursos do Azure hello usando clique para implantar</span><span class="sxs-lookup"><span data-stu-id="63df1-198">Deploy hello Azure Resource Manager template by using click-to-deploy</span></span>

<span data-ttu-id="63df1-199">Clique em implantar é toouse de outra maneira modelos do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="63df1-199">Click-to-deploy is another way toouse Azure Resource Manager templates.</span></span> <span data-ttu-id="63df1-200">É um modelos de toouse de maneira fácil com hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="63df1-200">It's an easy way toouse templates with hello Azure portal.</span></span>

1. <span data-ttu-id="63df1-201">Vá muito[criar um gateway de aplicativos com o firewall do aplicativo web](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span><span class="sxs-lookup"><span data-stu-id="63df1-201">Go too[Create an application gateway with web application firewall](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span></span>

1. <span data-ttu-id="63df1-202">Clique em **implantar tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="63df1-202">Click **Deploy tooAzure**.</span></span>

    ![Implantar tooAzure](./media/application-gateway-create-gateway-arm-template/deploytoazure.png)
    
1. <span data-ttu-id="63df1-204">Insira parâmetros Olá para o modelo de implantação Olá no portal de saudação e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="63df1-204">Fill out hello parameters for hello deployment template on hello portal and click **OK**.</span></span>

    ![parâmetros](./media/application-gateway-create-gateway-arm-template/ibiza1.png)
    
1. <span data-ttu-id="63df1-206">Selecione **concordo toohello termos e condições declaradas acima** e clique em **compra**.</span><span class="sxs-lookup"><span data-stu-id="63df1-206">Select **I agree toohello terms and conditions stated above** and click **Purchase**.</span></span>

1. <span data-ttu-id="63df1-207">Na folha de implantação do hello personalizada, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="63df1-207">On hello Custom deployment blade, click **Create**.</span></span>

## <a name="providing-certificate-data-tooresource-manager-templates"></a><span data-ttu-id="63df1-208">Fornecendo Gerenciador de modelos de certificado dados tooResource</span><span class="sxs-lookup"><span data-stu-id="63df1-208">Providing certificate data tooResource Manager templates</span></span>

<span data-ttu-id="63df1-209">Ao usar o SSL com um modelo, o certificado de saudação deve toobe fornecido em uma cadeia de caracteres base64 em vez de ser carregado.</span><span class="sxs-lookup"><span data-stu-id="63df1-209">When using SSL with a template, hello certificate needs toobe provided in a base64 string instead of being uploaded.</span></span> <span data-ttu-id="63df1-210">tooconvert. pfx ou. cer tooa em base64 de cadeia de caracteres use um dos comandos a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="63df1-210">tooconvert a .pfx or .cer tooa base64 string use one of hello following commands.</span></span> <span data-ttu-id="63df1-211">Olá seguintes comandos convertem Olá certificado tooa cadeia de caracteres base64, que pode ser fornecida toohello modelo.</span><span class="sxs-lookup"><span data-stu-id="63df1-211">hello following commands convert hello certificate tooa base64 string, which can be provided toohello template.</span></span> <span data-ttu-id="63df1-212">Olá esperado a saída é uma cadeia de caracteres que pode ser armazenada em uma variável e colada no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="63df1-212">hello expected output is a string that can be stored in a variable and pasted in hello template.</span></span>

### <a name="macos"></a><span data-ttu-id="63df1-213">macOS</span><span class="sxs-lookup"><span data-stu-id="63df1-213">macOS</span></span>
```bash
cert=$( base64 <certificate path and name>.pfx )
echo $cert
```

### <a name="windows"></a><span data-ttu-id="63df1-214">Windows</span><span class="sxs-lookup"><span data-stu-id="63df1-214">Windows</span></span>
```powershell
[System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("<certificate path and name>.pfx"))
```

## <a name="delete-all-resources"></a><span data-ttu-id="63df1-215">Excluir todos os recursos</span><span class="sxs-lookup"><span data-stu-id="63df1-215">Delete all resources</span></span>

<span data-ttu-id="63df1-216">toodelete todos os recursos criados neste artigo, complete um dos Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="63df1-216">toodelete all resources created in this article, complete one of hello following steps:</span></span>

### <a name="powershell"></a><span data-ttu-id="63df1-217">PowerShell</span><span class="sxs-lookup"><span data-stu-id="63df1-217">PowerShell</span></span>

```powershell
Remove-AzureRmResourceGroup -Name appgatewayRG
```

### <a name="azure-cli"></a><span data-ttu-id="63df1-218">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="63df1-218">Azure CLI</span></span>

```azurecli
az group delete --name appgatewayRG
```

## <a name="next-steps"></a><span data-ttu-id="63df1-219">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="63df1-219">Next steps</span></span>

<span data-ttu-id="63df1-220">Se você quiser tooconfigure descarregamento de SSL, visite: [Configure um gateway de aplicativo para descarregamento SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="63df1-220">If you want tooconfigure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="63df1-221">Se você quiser tooconfigure um toouse de gateway do aplicativo com um balanceador de carga interno, visite: [criar um gateway de aplicativo com um balanceador de carga interno (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="63df1-221">If you want tooconfigure an application gateway toouse with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="63df1-222">Se deseja saber mais sobre as opções de balanceamento de carga no geral, visite:</span><span class="sxs-lookup"><span data-stu-id="63df1-222">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="63df1-223">Balanceador de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="63df1-223">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="63df1-224">Gerenciador de Tráfego do Azure</span><span class="sxs-lookup"><span data-stu-id="63df1-224">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

