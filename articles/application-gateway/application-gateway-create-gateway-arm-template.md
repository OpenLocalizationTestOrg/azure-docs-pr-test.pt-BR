---
title: Criar um Gateway de Aplicativo do Azure - modelos | Microsoft Docs
description: "Esta página oferece instruções para criar um gateway de aplicativo do Azure usando o modelo do Gerenciador de Recursos do Azure"
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
ms.openlocfilehash: 46cca89ccb5bd77d57fabc3e9027fcebd38da8e7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-application-gateway-by-using-the-azure-resource-manager-template"></a><span data-ttu-id="593fe-103">Criar um gateway de aplicativo usando o modelo do Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="593fe-103">Create an application gateway by using the Azure Resource Manager template</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="593fe-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="593fe-104">Azure portal</span></span>](application-gateway-create-gateway-portal.md)
> * [<span data-ttu-id="593fe-105">PowerShell do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="593fe-105">Azure Resource Manager PowerShell</span></span>](application-gateway-create-gateway-arm.md)
> * [<span data-ttu-id="593fe-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="593fe-106">Azure Classic PowerShell</span></span>](application-gateway-create-gateway.md)
> * [<span data-ttu-id="593fe-107">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="593fe-107">Azure Resource Manager template</span></span>](application-gateway-create-gateway-arm-template.md)
> * [<span data-ttu-id="593fe-108">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="593fe-108">Azure CLI</span></span>](application-gateway-create-gateway-cli.md)

<span data-ttu-id="593fe-109">O Gateway de Aplicativo do Azure é um balanceador de carga de camada 7.</span><span class="sxs-lookup"><span data-stu-id="593fe-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="593fe-110">Ele fornece failover e solicitações HTTP de roteamento de desempenho entre diferentes servidores, estejam eles na nuvem ou no local.</span><span class="sxs-lookup"><span data-stu-id="593fe-110">It provides failover and performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="593fe-111">O Gateway de Aplicativo fornece muitos recursos do ADC (Controlador de entrega de aplicativos), incluindo o balanceamento de carga de HTTP, a afinidade de sessão baseada em cookies, o descarregamento de protocolo SSL (Secure Sockets Layer), as sondas de integridade personalizadas, suporte para vários sites e muitos outros.</span><span class="sxs-lookup"><span data-stu-id="593fe-111">Application Gateway provides many application delivery controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="593fe-112">Para conferir uma lista completa dos recursos com suporte, visite [Visão geral do Gateway de Aplicativo](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="593fe-112">To find a complete list of supported features, visit [Application Gateway overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="593fe-113">Este artigo orienta a baixar e a modificar um modelo existente do Azure Resource Manager do GitHub e a implantar o modelo do GitHub, do PowerShell e da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="593fe-113">This article walks you through downloading and modifying an existing Azure Resource Manager template from GitHub and deploying the template from GitHub, PowerShell, and the Azure CLI.</span></span>

<span data-ttu-id="593fe-114">Se você estiver simplesmente implantando o modelo do Gerenciador de Recursos do Azure diretamente do GitHub, sem nenhuma alteração, ignore para implantar um modelo do GitHub.</span><span class="sxs-lookup"><span data-stu-id="593fe-114">If you are simply deploying the Azure Resource Manager template directly from GitHub without any changes, skip to deploy a template from GitHub.</span></span>

## <a name="scenario"></a><span data-ttu-id="593fe-115">Cenário</span><span class="sxs-lookup"><span data-stu-id="593fe-115">Scenario</span></span>

<span data-ttu-id="593fe-116">Neste cenário, você:</span><span class="sxs-lookup"><span data-stu-id="593fe-116">In this scenario you will:</span></span>

* <span data-ttu-id="593fe-117">Crie um Gateway de Aplicativo com o firewall do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="593fe-117">Create an application gateway with web application firewall.</span></span>
* <span data-ttu-id="593fe-118">Criará uma rede virtual chamada VirtualNetwork1, com um bloco CIDR 10.0.0.0/16 reservado.</span><span class="sxs-lookup"><span data-stu-id="593fe-118">Create a virtual network named VirtualNetwork1 with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="593fe-119">Criará uma sub-rede chamada Appgatewaysubnet que usa 10.0.0.0/28 como seu bloco CIDR.</span><span class="sxs-lookup"><span data-stu-id="593fe-119">Create a subnet called Appgatewaysubnet that uses 10.0.0.0/28 as its CIDR block.</span></span>
* <span data-ttu-id="593fe-120">Configurará dois IPs de back-end definidos anteriormente para os servidores Web nos quais deseja balancear a carga do tráfego.</span><span class="sxs-lookup"><span data-stu-id="593fe-120">Set up two previously configured back-end IPs for the web servers you want to load balance the traffic.</span></span> <span data-ttu-id="593fe-121">Neste exemplo de modelo, os IPs de back-end são 10.0.1.10 e 10.0.1.11.</span><span class="sxs-lookup"><span data-stu-id="593fe-121">In this template example, the back-end IPs are 10.0.1.10 and 10.0.1.11.</span></span>

> [!NOTE]
> <span data-ttu-id="593fe-122">Essas configurações são os parâmetros para esse modelo.</span><span class="sxs-lookup"><span data-stu-id="593fe-122">Those settings are the parameters for this template.</span></span> <span data-ttu-id="593fe-123">Para personalizar o modelo, você pode alterar as regras, o ouvinte, o SSL e outras opções no arquivo azuredeploy.json.</span><span class="sxs-lookup"><span data-stu-id="593fe-123">To customize the template, you can change rules, the listener, SSL, and other options in the azuredeploy.json file.</span></span>

![Cenário](./media/application-gateway-create-gateway-arm-template/scenario.png)

## <a name="download-and-understand-the-azure-resource-manager-template"></a><span data-ttu-id="593fe-125">Baixar e compreender o modelo do Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="593fe-125">Download and understand the Azure Resource Manager template</span></span>

<span data-ttu-id="593fe-126">Você pode baixar o modelo existente do Gerenciador de Recursos do Azure para criar uma rede virtual e duas sub-redes do GitHub, fazer as alterações desejadas e reutilizá-la.</span><span class="sxs-lookup"><span data-stu-id="593fe-126">You can download the existing Azure Resource Manager template to create a virtual network and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="593fe-127">Para fazer isso, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="593fe-127">To do so, use the following steps:</span></span>

1. <span data-ttu-id="593fe-128">Navegue até [Criar Gateway de Aplicativo com o firewall de aplicativo Web habilitado](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span><span class="sxs-lookup"><span data-stu-id="593fe-128">Navigate to [Create Application Gateway with web application firewall enabled](https://github.com/Azure/azure-quickstart-templates/tree/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="593fe-129">Clique em **azuredeploy.json** e em **RAW**.</span><span class="sxs-lookup"><span data-stu-id="593fe-129">Click **azuredeploy.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="593fe-130">Salve o arquivo em uma pasta local do computador.</span><span class="sxs-lookup"><span data-stu-id="593fe-130">Save the file to a local folder on your computer.</span></span>
1. <span data-ttu-id="593fe-131">Se você estiver familiarizado com os modelos do Gerenciador de Recursos do Azure, pule para a etapa 7.</span><span class="sxs-lookup"><span data-stu-id="593fe-131">If you are familiar with Azure Resource Manager templates, skip to step 7.</span></span>
1. <span data-ttu-id="593fe-132">Abra o arquivo que você salvou e examine o conteúdo em **parâmetros** na linha</span><span class="sxs-lookup"><span data-stu-id="593fe-132">Open the file that you saved and look at the contents under **parameters** in line</span></span>
1. <span data-ttu-id="593fe-133">Os parâmetros do modelo do Gerenciador de Recursos do Azure fornecem um espaço reservado para valores que podem ser preenchidos durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="593fe-133">Azure Resource Manager template parameters provide a placeholder for values that can be filled out during deployment.</span></span>

  | <span data-ttu-id="593fe-134">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="593fe-134">Parameter</span></span> | <span data-ttu-id="593fe-135">Descrição</span><span class="sxs-lookup"><span data-stu-id="593fe-135">Description</span></span> |
  | --- | --- |
  | <span data-ttu-id="593fe-136">**subnetPrefix**</span><span class="sxs-lookup"><span data-stu-id="593fe-136">**subnetPrefix**</span></span> |<span data-ttu-id="593fe-137">Bloco CIDR para a sub-rede do Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="593fe-137">CIDR block for the application gateway subnet.</span></span> |
  | <span data-ttu-id="593fe-138">**applicationGatewaySize**</span><span class="sxs-lookup"><span data-stu-id="593fe-138">**applicationGatewaySize**</span></span> | <span data-ttu-id="593fe-139">O tamanho do Gateway de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="593fe-139">Size of the application gateway.</span></span>  <span data-ttu-id="593fe-140">O WAF permite apenas médio e grande.</span><span class="sxs-lookup"><span data-stu-id="593fe-140">WAF only allows medium and large.</span></span> |
  | <span data-ttu-id="593fe-141">**backendIpaddress1**</span><span class="sxs-lookup"><span data-stu-id="593fe-141">**backendIpaddress1**</span></span> |<span data-ttu-id="593fe-142">Endereço IP do primeiro servidor Web.</span><span class="sxs-lookup"><span data-stu-id="593fe-142">IP address of the first web server.</span></span> |
  | <span data-ttu-id="593fe-143">**backendIpaddress2**</span><span class="sxs-lookup"><span data-stu-id="593fe-143">**backendIpaddress2**</span></span> |<span data-ttu-id="593fe-144">Endereço IP do segundo servidor Web.</span><span class="sxs-lookup"><span data-stu-id="593fe-144">IP address of the second web server.</span></span> |
  | <span data-ttu-id="593fe-145">**wafEnabled**</span><span class="sxs-lookup"><span data-stu-id="593fe-145">**wafEnabled**</span></span> | <span data-ttu-id="593fe-146">Configuração para determinar se o WAF está habilitado.</span><span class="sxs-lookup"><span data-stu-id="593fe-146">Setting to determine if WAF is enabled.</span></span>|
  | <span data-ttu-id="593fe-147">**wafMode**</span><span class="sxs-lookup"><span data-stu-id="593fe-147">**wafMode**</span></span> | <span data-ttu-id="593fe-148">Modo do firewall do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="593fe-148">Mode of the web application firewall.</span></span>  <span data-ttu-id="593fe-149">As opções disponíveis são **prevenção** ou **detecção**.</span><span class="sxs-lookup"><span data-stu-id="593fe-149">Available options are **prevention** or **detection**.</span></span>|
  | <span data-ttu-id="593fe-150">**wafRuleSetType**</span><span class="sxs-lookup"><span data-stu-id="593fe-150">**wafRuleSetType**</span></span> | <span data-ttu-id="593fe-151">Tipo de conjunto de regras para WAF.</span><span class="sxs-lookup"><span data-stu-id="593fe-151">Ruleset type for WAF.</span></span>  <span data-ttu-id="593fe-152">Atualmente, OWASP é a única opção com suporte.</span><span class="sxs-lookup"><span data-stu-id="593fe-152">Currently OWASP is the only supported option.</span></span> |
  | <span data-ttu-id="593fe-153">**wafRuleSetVersion**</span><span class="sxs-lookup"><span data-stu-id="593fe-153">**wafRuleSetVersion**</span></span> |<span data-ttu-id="593fe-154">Versão de conjunto de regras.</span><span class="sxs-lookup"><span data-stu-id="593fe-154">Ruleset version.</span></span> <span data-ttu-id="593fe-155">As opções com suporte atualmente são OWASP CRS 2.2.9 e 3.0.</span><span class="sxs-lookup"><span data-stu-id="593fe-155">OWASP CRS 2.2.9 and 3.0 are currently the supported options.</span></span> |

1. <span data-ttu-id="593fe-156">Verifique o conteúdo em **recursos** e observe as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="593fe-156">Check the content under **resources** and notice the following properties:</span></span>

   * <span data-ttu-id="593fe-157">**type**.</span><span class="sxs-lookup"><span data-stu-id="593fe-157">**type**.</span></span> <span data-ttu-id="593fe-158">Tipo de recurso que está sendo criado pelo modelo.</span><span class="sxs-lookup"><span data-stu-id="593fe-158">Type of resource being created by the template.</span></span> <span data-ttu-id="593fe-159">Nesse caso, o tipo é `Microsoft.Network/applicationGateways`, que representa um gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="593fe-159">In this case, the type is `Microsoft.Network/applicationGateways`, which represents an application gateway.</span></span>
   * <span data-ttu-id="593fe-160">**name**.</span><span class="sxs-lookup"><span data-stu-id="593fe-160">**name**.</span></span> <span data-ttu-id="593fe-161">Nome do recurso.</span><span class="sxs-lookup"><span data-stu-id="593fe-161">Name for the resource.</span></span> <span data-ttu-id="593fe-162">Observe o uso de `[parameters('applicationGatewayName')]`, que significa o nome que é fornecido como entrada por você ou um arquivo de parâmetro durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="593fe-162">Notice the use of `[parameters('applicationGatewayName')]`, which means that the name is provided as input by you or by a parameter file during deployment.</span></span>
   * <span data-ttu-id="593fe-163">**properties**.</span><span class="sxs-lookup"><span data-stu-id="593fe-163">**properties**.</span></span> <span data-ttu-id="593fe-164">Lista de propriedades do recurso.</span><span class="sxs-lookup"><span data-stu-id="593fe-164">List of properties for the resource.</span></span> <span data-ttu-id="593fe-165">Esse modelo usa a rede virtual e o endereço IP público durante a criação do gateway de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="593fe-165">This template uses the virtual network and public IP address during application gateway creation.</span></span>

   > [!NOTE]
   > <span data-ttu-id="593fe-166">Para obter mais informações sobre modelos, visite: [Referência de modelos do Resource Manager](/templates/)</span><span class="sxs-lookup"><span data-stu-id="593fe-166">For more information on templates visit: [Resource Manager templates reference](/templates/)</span></span>

1. <span data-ttu-id="593fe-167">Navegue de volta para [https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span><span class="sxs-lookup"><span data-stu-id="593fe-167">Navigate back to [https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf/](https://github.com/Azure/azure-quickstart-templates/blob/master/101-application-gateway-waf).</span></span>
1. <span data-ttu-id="593fe-168">Clique em **azuredeploy-parameters.json** e em **RAW**.</span><span class="sxs-lookup"><span data-stu-id="593fe-168">Click **azuredeploy-parameters.json**, and then click **RAW**.</span></span>
1. <span data-ttu-id="593fe-169">Salve o arquivo em uma pasta local do computador.</span><span class="sxs-lookup"><span data-stu-id="593fe-169">Save the file to a local folder on your computer.</span></span>
1. <span data-ttu-id="593fe-170">Abra o arquivo que você salvou e edite os valores dos parâmetros.</span><span class="sxs-lookup"><span data-stu-id="593fe-170">Open the file that you saved and edit the values for the parameters.</span></span> <span data-ttu-id="593fe-171">Use os valores a seguir para implantar o gateway de aplicativo descrito em nosso cenário.</span><span class="sxs-lookup"><span data-stu-id="593fe-171">Use the following values to deploy the application gateway described in our scenario.</span></span>

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

1. <span data-ttu-id="593fe-172">Salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="593fe-172">Save the file.</span></span> <span data-ttu-id="593fe-173">Você pode testar o modelo JSON e o modelo de parâmetro usando ferramentas de validação de JSON online, como [JSlint.com](http://www.jslint.com/).</span><span class="sxs-lookup"><span data-stu-id="593fe-173">You can test the JSON template and parameter template by using online JSON validation tools like [JSlint.com](http://www.jslint.com/).</span></span>

## <a name="deploy-the-azure-resource-manager-template-by-using-powershell"></a><span data-ttu-id="593fe-174">Implantar o modelo do Gerenciador de Recursos do Azure usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="593fe-174">Deploy the Azure Resource Manager template by using PowerShell</span></span>

<span data-ttu-id="593fe-175">Se você nunca usou o Azure PowerShell, visite: [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview) e siga as instruções para entrar no Azure e selecionar sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="593fe-175">If you have never used Azure PowerShell, visit: [How to install and configure Azure PowerShell](/powershell/azure/overview) and follow the instructions to sign into Azure and select your subscription.</span></span>

1. <span data-ttu-id="593fe-176">Fazer logon no PowerShell</span><span class="sxs-lookup"><span data-stu-id="593fe-176">Login to PowerShell</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="593fe-177">Verificar as assinaturas da conta.</span><span class="sxs-lookup"><span data-stu-id="593fe-177">Check the subscriptions for the account.</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

    <span data-ttu-id="593fe-178">Você deve se autenticar com suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="593fe-178">You are prompted to authenticate with your credentials.</span></span>

1. <span data-ttu-id="593fe-179">Escolha quais das suas assinaturas do Azure deseja usar.</span><span class="sxs-lookup"><span data-stu-id="593fe-179">Choose which of your Azure subscriptions to use.</span></span>

    ```powershell
    Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
    ```

1. <span data-ttu-id="593fe-180">Se necessário, crie um grupo de recursos usando o cmdlet **New-AzureResourceGroup** .</span><span class="sxs-lookup"><span data-stu-id="593fe-180">If needed, create a resource group by using the **New-AzureResourceGroup** cmdlet.</span></span> <span data-ttu-id="593fe-181">No exemplo a seguir, você cria um grupo de recursos chamado AppgatewayRG no local do Leste dos EUA.</span><span class="sxs-lookup"><span data-stu-id="593fe-181">In the following example, you create a resource group called AppgatewayRG in East US location.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name AppgatewayRG -Location "West US"
    ```

1. <span data-ttu-id="593fe-182">Execute o cmdlet **New-AzureRmResourceGroupDeployment** para implantar a nova rede virtual usando os arquivos de modelo e parâmetro anteriores que você baixou e modificou.</span><span class="sxs-lookup"><span data-stu-id="593fe-182">Run the **New-AzureRmResourceGroupDeployment** cmdlet to deploy the new virtual network by using the preceding template and parameter files you downloaded and modified.</span></span>
    
    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestAppgatewayDeployment -ResourceGroupName AppgatewayRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

## <a name="deploy-the-azure-resource-manager-template-by-using-the-azure-cli"></a><span data-ttu-id="593fe-183">Implantar o modelo do Gerenciador de Recursos do Azure usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="593fe-183">Deploy the Azure Resource Manager template by using the Azure CLI</span></span>

<span data-ttu-id="593fe-184">Para implantar o modelo do Azure Resource Manager baixado usando a CLI do Azure, execute as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="593fe-184">To deploy the Azure Resource Manager template you downloaded by using Azure CLI, follow the following steps:</span></span>

1. <span data-ttu-id="593fe-185">Se você nunca usou a CLI do Azure, confira [Instalar e configurar a CLI do Azure](/cli/azure/install-azure-cli) e siga as instruções até o ponto em que você seleciona sua conta e assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="593fe-185">If you have never used Azure CLI, see [Install and configure the Azure CLI](/cli/azure/install-azure-cli) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>

1. <span data-ttu-id="593fe-186">Se for necessário, execute o comando `az group create` para criar um grupo de recursos, conforme mostra o trecho de código abaixo.</span><span class="sxs-lookup"><span data-stu-id="593fe-186">If necessary, run the `az group create` command to create a resource group, as shown in the following code snippet.</span></span> <span data-ttu-id="593fe-187">Observe a saída do comando.</span><span class="sxs-lookup"><span data-stu-id="593fe-187">Notice the output of the command.</span></span> <span data-ttu-id="593fe-188">A lista exibida após a saída explicar os parâmetros usados.</span><span class="sxs-lookup"><span data-stu-id="593fe-188">The list shown after the output explains the parameters used.</span></span> <span data-ttu-id="593fe-189">Para saber mais sobre grupos de recursos, visite [Visão geral do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="593fe-189">For more information about resource groups, visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```azurecli
    az group create --location westus --name appgatewayRG
    ```
    
    <span data-ttu-id="593fe-190">**-n (or --name)**.</span><span class="sxs-lookup"><span data-stu-id="593fe-190">**-n (or --name)**.</span></span> <span data-ttu-id="593fe-191">Nome do novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="593fe-191">Name for the new resource group.</span></span> <span data-ttu-id="593fe-192">Para nosso cenário, é *appgatewayRG*.</span><span class="sxs-lookup"><span data-stu-id="593fe-192">For our scenario, it's *appgatewayRG*.</span></span>
    
    <span data-ttu-id="593fe-193">**-l (ou --location)**.</span><span class="sxs-lookup"><span data-stu-id="593fe-193">**-l (or --location)**.</span></span> <span data-ttu-id="593fe-194">Região do Azure onde o novo grupo de recursos é criado.</span><span class="sxs-lookup"><span data-stu-id="593fe-194">Azure region where the new resource group is created.</span></span> <span data-ttu-id="593fe-195">Para nosso cenário, esse grupo é *westus*.</span><span class="sxs-lookup"><span data-stu-id="593fe-195">For our scenario, it's *westus*.</span></span>

1. <span data-ttu-id="593fe-196">Execute o cmdlet `az group deployment create` para implantar a nova rede virtual usando o modelo e os arquivos de parâmetro que você baixou e modificou na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="593fe-196">Run the `az group deployment create` cmdlet to deploy the new virtual network by using the template and parameter files you downloaded and modified in the preceding step.</span></span> <span data-ttu-id="593fe-197">A lista exibida após a saída explicar os parâmetros usados.</span><span class="sxs-lookup"><span data-stu-id="593fe-197">The list shown after the output explains the parameters used.</span></span>

    ```azurecli
    az group deployment create --resource-group appgatewayRG --name TestAppgatewayDeployment --template-file azuredeploy.json --parameters @azuredeploy-parameters.json
    ```

## <a name="deploy-the-azure-resource-manager-template-by-using-click-to-deploy"></a><span data-ttu-id="593fe-198">Implantar o modelo do Gerenciador de Recursos do Azure usando o clique para implantar</span><span class="sxs-lookup"><span data-stu-id="593fe-198">Deploy the Azure Resource Manager template by using click-to-deploy</span></span>

<span data-ttu-id="593fe-199">Clique para implantar é outra maneira de usar modelos do Gerenciador de Recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="593fe-199">Click-to-deploy is another way to use Azure Resource Manager templates.</span></span> <span data-ttu-id="593fe-200">É uma maneira fácil de usar modelos com o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="593fe-200">It's an easy way to use templates with the Azure portal.</span></span>

1. <span data-ttu-id="593fe-201">Vá até [Criar um Gateway de Aplicativo com o firewall do aplicativo Web](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span><span class="sxs-lookup"><span data-stu-id="593fe-201">Go to [Create an application gateway with web application firewall](https://azure.microsoft.com/documentation/templates/101-application-gateway-waf/).</span></span>

1. <span data-ttu-id="593fe-202">Clique em **Implantar no Azure**.</span><span class="sxs-lookup"><span data-stu-id="593fe-202">Click **Deploy to Azure**.</span></span>

    ![Implantar no Azure](./media/application-gateway-create-gateway-arm-template/deploytoazure.png)
    
1. <span data-ttu-id="593fe-204">Preencha os parâmetros do modelo de implantação no portal e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="593fe-204">Fill out the parameters for the deployment template on the portal and click **OK**.</span></span>

    ![parâmetros](./media/application-gateway-create-gateway-arm-template/ibiza1.png)
    
1. <span data-ttu-id="593fe-206">Selecione **Concordo com os termos e condições declarados acima** e clique em **Comprar**.</span><span class="sxs-lookup"><span data-stu-id="593fe-206">Select **I agree to the terms and conditions stated above** and click **Purchase**.</span></span>

1. <span data-ttu-id="593fe-207">Na folha Implantação personalizada, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="593fe-207">On the Custom deployment blade, click **Create**.</span></span>

## <a name="providing-certificate-data-to-resource-manager-templates"></a><span data-ttu-id="593fe-208">Fornecendo dados de certificado aos modelos do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="593fe-208">Providing certificate data to Resource Manager templates</span></span>

<span data-ttu-id="593fe-209">Ao usar o SSL com um modelo, o certificado precisa ser fornecido em uma cadeia de caracteres base64 em vez de ser carregado.</span><span class="sxs-lookup"><span data-stu-id="593fe-209">When using SSL with a template, the certificate needs to be provided in a base64 string instead of being uploaded.</span></span> <span data-ttu-id="593fe-210">Para converter .pfx ou .cer para uma sequência de caracteres base64 usar um dos seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="593fe-210">To convert a .pfx or .cer to a base64 string use one of the following commands.</span></span> <span data-ttu-id="593fe-211">Os comandos a seguir convertem o certificado a uma sequência de caracteres base64, que pode ser fornecida ao modelo.</span><span class="sxs-lookup"><span data-stu-id="593fe-211">The following commands convert the certificate to a base64 string, which can be provided to the template.</span></span> <span data-ttu-id="593fe-212">A saída esperada é uma cadeia de caracteres que pode ser armazenada em uma variável e colada no modelo.</span><span class="sxs-lookup"><span data-stu-id="593fe-212">The expected output is a string that can be stored in a variable and pasted in the template.</span></span>

### <a name="macos"></a><span data-ttu-id="593fe-213">macOS</span><span class="sxs-lookup"><span data-stu-id="593fe-213">macOS</span></span>
```bash
cert=$( base64 <certificate path and name>.pfx )
echo $cert
```

### <a name="windows"></a><span data-ttu-id="593fe-214">Windows</span><span class="sxs-lookup"><span data-stu-id="593fe-214">Windows</span></span>
```powershell
[System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("<certificate path and name>.pfx"))
```

## <a name="delete-all-resources"></a><span data-ttu-id="593fe-215">Excluir todos os recursos</span><span class="sxs-lookup"><span data-stu-id="593fe-215">Delete all resources</span></span>

<span data-ttu-id="593fe-216">Para excluir todos os recursos criados neste artigo, conclua uma das seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="593fe-216">To delete all resources created in this article, complete one of the following steps:</span></span>

### <a name="powershell"></a><span data-ttu-id="593fe-217">PowerShell</span><span class="sxs-lookup"><span data-stu-id="593fe-217">PowerShell</span></span>

```powershell
Remove-AzureRmResourceGroup -Name appgatewayRG
```

### <a name="azure-cli"></a><span data-ttu-id="593fe-218">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="593fe-218">Azure CLI</span></span>

```azurecli
az group delete --name appgatewayRG
```

## <a name="next-steps"></a><span data-ttu-id="593fe-219">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="593fe-219">Next steps</span></span>

<span data-ttu-id="593fe-220">Se desejar configurar o descarregamento SSL, visite [Configurar um Gateway de Aplicativo para descarregamento SSL](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="593fe-220">If you want to configure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="593fe-221">Para configurar um Gateway de Aplicativo para usar com um balanceador de carga interno, visite [Criar um Gateway de Aplicativo com um ILB (balanceador de carga interno)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="593fe-221">If you want to configure an application gateway to use with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="593fe-222">Se deseja saber mais sobre as opções de balanceamento de carga no geral, visite:</span><span class="sxs-lookup"><span data-stu-id="593fe-222">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="593fe-223">Balanceador de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="593fe-223">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="593fe-224">Gerenciador de Tráfego do Azure</span><span class="sxs-lookup"><span data-stu-id="593fe-224">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

