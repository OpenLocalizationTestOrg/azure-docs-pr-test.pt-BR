---
title: "Conectar seu aplicativo à rede virtual usando o PowerShell"
description: "Instruções sobre como se conectar a e trabalhar com redes virtuais usando o PowerShell"
services: app-service
documentationcenter: 
author: ccompy
manager: erikre
editor: cephalin
ms.assetid: a5c76e77-972a-431c-b14b-3611dae1631b
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/29/2016
ms.author: ccompy
ms.openlocfilehash: 6fae6a6c162fa326161d2b47a259b3151d6e3dd0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-app-to-your-virtual-network-by-using-powershell"></a><span data-ttu-id="4281c-103">Conectar seu aplicativo à rede virtual usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="4281c-103">Connect your app to your virtual network by using PowerShell</span></span>
## <a name="overview"></a><span data-ttu-id="4281c-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="4281c-104">Overview</span></span>
<span data-ttu-id="4281c-105">No serviço de aplicativo do Azure, você pode conectar seu aplicativo (Web, móvel ou de API) a uma VNet (rede virtual) do Azure em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="4281c-105">In Azure App Service, you can connect your app (web, mobile, or API) to an Azure virtual network (VNet) in your subscription.</span></span> <span data-ttu-id="4281c-106">Esse recurso é chamado de Integração VNet.</span><span class="sxs-lookup"><span data-stu-id="4281c-106">This feature is called VNet Integration.</span></span> <span data-ttu-id="4281c-107">O recurso de Integração VNet não deve ser confundido com o recurso de Ambiente de Serviço de Aplicativo, que permite a execução de uma instância do Serviço de Aplicativo do Azure em sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="4281c-107">The VNet Integration feature should not be confused with the App Service Environment feature, which allows you to run an instance of Azure App Service in your virtual network.</span></span>

<span data-ttu-id="4281c-108">O recurso de Integração VNet tem uma IU (interface de usuário) no novo portal que você pode usar para a integração com redes virtuais que são implantadas usando o modelo de implantação clássico ou o modelo de implantação do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4281c-108">The VNet Integration feature has a user interface (UI) in the new portal that you can use to integrate with virtual networks that are deployed by using either the classic deployment model or the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="4281c-109">Para saber mais sobre o recurso, confira [Integrar seu aplicativo a uma rede virtual do Azure](web-sites-integrate-with-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="4281c-109">If you want to learn more about the feature, see [Integrate your app with an Azure virtual network](web-sites-integrate-with-vnet.md).</span></span>

<span data-ttu-id="4281c-110">Este artigo não é sobre como usar a interface do usuário, mas sobre como habilitar a integração usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4281c-110">This article is not about how to use the UI but rather about how to enable integration by using PowerShell.</span></span> <span data-ttu-id="4281c-111">Como os comandos de cada modelo de implantação são diferentes, este artigo tem uma seção para cada modelo de implantação.</span><span class="sxs-lookup"><span data-stu-id="4281c-111">Because the commands for each deployment model are different, this article has a section for each deployment model.</span></span>  

<span data-ttu-id="4281c-112">Antes de continuar a ler este artigo, verifique se você tem:</span><span class="sxs-lookup"><span data-stu-id="4281c-112">Before you continue with this article, ensure that you have:</span></span>

* <span data-ttu-id="4281c-113">O SDK mais recente do Azure PowerShell instalado.</span><span class="sxs-lookup"><span data-stu-id="4281c-113">The latest Azure PowerShell SDK installed.</span></span> <span data-ttu-id="4281c-114">Você pode instalá-lo usando o Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="4281c-114">You can install this with the Web Platform Installer.</span></span>
* <span data-ttu-id="4281c-115">Um aplicativo no Serviço de Aplicativo do Azure em execução em uma SKU Standard ou Premium.</span><span class="sxs-lookup"><span data-stu-id="4281c-115">An app in Azure App Service running in a Standard or Premium SKU.</span></span>

## <a name="classic-virtual-networks"></a><span data-ttu-id="4281c-116">Redes virtuais clássicas</span><span class="sxs-lookup"><span data-stu-id="4281c-116">Classic virtual networks</span></span>
<span data-ttu-id="4281c-117">Esta seção explica as três tarefas para redes virtuais que usam o modelo de implantação clássico:</span><span class="sxs-lookup"><span data-stu-id="4281c-117">This section explains three tasks for virtual networks that use the classic deployment model:</span></span>

1. <span data-ttu-id="4281c-118">Conecte seu aplicativo a uma rede virtual pré-existente que tenha um gateway e esteja configurada para conectividade ponto a site.</span><span class="sxs-lookup"><span data-stu-id="4281c-118">Connect your app to a preexisting virtual network that has a gateway and is configured for point-to-site connectivity.</span></span>
2. <span data-ttu-id="4281c-119">Atualize as informações de integração de rede virtual para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4281c-119">Update your virtual network integration information for your app.</span></span>
3. <span data-ttu-id="4281c-120">Desconecte o aplicativo da rede virtual.</span><span class="sxs-lookup"><span data-stu-id="4281c-120">Disconnect your app from your virtual network.</span></span>

### <a name="connect-an-app-to-a-classic-vnet"></a><span data-ttu-id="4281c-121">Conectar um aplicativo a uma VNet clássica</span><span class="sxs-lookup"><span data-stu-id="4281c-121">Connect an app to a classic VNet</span></span>
<span data-ttu-id="4281c-122">Para conectar um aplicativo a uma rede virtual, siga estas três etapas:</span><span class="sxs-lookup"><span data-stu-id="4281c-122">To connect an app to a virtual network, follow these three steps:</span></span>

1. <span data-ttu-id="4281c-123">Declare ao aplicativo Web que ele ingressará em uma rede virtual específica.</span><span class="sxs-lookup"><span data-stu-id="4281c-123">Declare to the web app that it will be joining a particular virtual network.</span></span> <span data-ttu-id="4281c-124">O aplicativo gerará um certificado que será fornecido à rede virtual para a conectividade ponto a site.</span><span class="sxs-lookup"><span data-stu-id="4281c-124">The app will generate a certificate that will be given to the virtual network for point-to-site connectivity.</span></span>
2. <span data-ttu-id="4281c-125">Carregue o certificado do aplicativo Web na rede virtual e recupere o URI do pacote VPN ponto a site</span><span class="sxs-lookup"><span data-stu-id="4281c-125">Upload the web app certificate to the virtual network, and then retrieve the point-to-site VPN package URI.</span></span>
3. <span data-ttu-id="4281c-126">Atualize a conexão de rede virtual de aplicativos Web com o URI do pacote ponto a site</span><span class="sxs-lookup"><span data-stu-id="4281c-126">Update the web app's virtual network connection with the point-to-site package URI.</span></span>

<span data-ttu-id="4281c-127">A primeira e a terceira etapas são totalmente programáveis por scripts, mas a segunda etapa requer uma ação manual única por meio do portal ou acesso para executar ações **PUT** ou **PATCH** no ponto de extremidade do Azure Resource Manager da rede virtual.</span><span class="sxs-lookup"><span data-stu-id="4281c-127">The first and third steps are fully scriptable, but the second step requires a one-time, manual action through the portal, or access to perform **PUT** or **PATCH** actions on the virtual network Azure Resource Manager endpoint.</span></span> <span data-ttu-id="4281c-128">Entre em contato com o Suporte do Azure para habilitar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="4281c-128">Contact Azure Support to have this enabled.</span></span> <span data-ttu-id="4281c-129">Antes de começar, verifique se você tem uma rede virtual clássica que tenha a conectividade ponto a site já habilitada e um gateway implantado.</span><span class="sxs-lookup"><span data-stu-id="4281c-129">Before you start, make sure that you have a classic virtual network that has point-to-site connectivity already enabled and a deployed gateway.</span></span> <span data-ttu-id="4281c-130">Para criar o gateway e habilitar a conectividade ponto a site, você precisa usar o portal, conforme descrito em [Criando um gateway de VPN][createvpngateway].</span><span class="sxs-lookup"><span data-stu-id="4281c-130">To create the gateway and enable point-to-site connectivity, you need to use the portal as described at [Creating a VPN gateway][createvpngateway].</span></span>

<span data-ttu-id="4281c-131">A rede virtual clássica precisa estar na mesma assinatura que o plano do Serviço de Aplicativo que contém o aplicativo ao qual você está fazendo a integração.</span><span class="sxs-lookup"><span data-stu-id="4281c-131">The classic virtual network needs to be in the same subscription as your App Service plan that holds the app that you are integrating with.</span></span>

##### <a name="set-up-azure-powershell-sdk"></a><span data-ttu-id="4281c-132">Configurar o SDK do Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4281c-132">Set up Azure PowerShell SDK</span></span>
<span data-ttu-id="4281c-133">Abra uma janela do PowerShell e configure sua conta e assinatura do Azure usando:</span><span class="sxs-lookup"><span data-stu-id="4281c-133">Open a PowerShell window and set up your Azure account and subscription by using:</span></span>

    Login-AzureRmAccount

<span data-ttu-id="4281c-134">Esse comando abrirá um prompt para obter suas credenciais do Azure.</span><span class="sxs-lookup"><span data-stu-id="4281c-134">That command will open a prompt to get your Azure credentials.</span></span> <span data-ttu-id="4281c-135">Depois de entrar, use um dos comandos a seguir para escolher a assinatura que você deseja usar.</span><span class="sxs-lookup"><span data-stu-id="4281c-135">After you sign in, use either of the following commands to select the subscription that you want to use.</span></span> <span data-ttu-id="4281c-136">Use a assinatura que contém sua rede virtual e o plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4281c-136">Make sure that you are using the subscription that your virtual network and App Service plan are in.</span></span>

    Select-AzureRmSubscription –SubscriptionName [WebAppSubscriptionName]

<span data-ttu-id="4281c-137">ou o</span><span class="sxs-lookup"><span data-stu-id="4281c-137">or</span></span>

    Select-AzureRmSubscription –SubscriptionId [WebAppSubscriptionId]

##### <a name="variables-used-in-this-article"></a><span data-ttu-id="4281c-138">Variáveis usadas neste artigo</span><span class="sxs-lookup"><span data-stu-id="4281c-138">Variables used in this article</span></span>
<span data-ttu-id="4281c-139">Para simplificar os comandos, definiremos uma variável **$Configuration** do PowerShell com a configuração específica.</span><span class="sxs-lookup"><span data-stu-id="4281c-139">To simplify commands, we will set a **$Configuration** PowerShell variable with the specific configuration.</span></span>

<span data-ttu-id="4281c-140">Defina uma variável no PowerShell da seguinte forma com os parâmetros indicados:</span><span class="sxs-lookup"><span data-stu-id="4281c-140">Set a variable as follows in PowerShell with the following parameters:</span></span>

    $Configuration = @{}
    $Configuration.WebAppResourceGroup = "[Your web app resource group]"
    $Configuration.WebAppName = "[Your web app name]"
    $Configuration.VnetSubscriptionId = "[Your vnet subscription id]"
    $Configuration.VnetResourceGroup = "[Your vnet resource group]"
    $Configuration.VnetName = "[Your vnet name]"

<span data-ttu-id="4281c-141">O local do aplicativo deve ser o local sem espaços.</span><span class="sxs-lookup"><span data-stu-id="4281c-141">The app location should be the location without any spaces.</span></span> <span data-ttu-id="4281c-142">Por exemplo, Oeste dos EUA é westus.</span><span class="sxs-lookup"><span data-stu-id="4281c-142">For example, West US is westus.</span></span>

    $Configuration.WebAppLocation = "[Your web app Location]"

<span data-ttu-id="4281c-143">O próximo item é onde o certificado deve ser gravado.</span><span class="sxs-lookup"><span data-stu-id="4281c-143">The next item is where the certificate should be written.</span></span> <span data-ttu-id="4281c-144">Deve ser um caminho gravável no computador local.</span><span class="sxs-lookup"><span data-stu-id="4281c-144">It should be a writable path on your local computer.</span></span> <span data-ttu-id="4281c-145">Inclua .cer no final.</span><span class="sxs-lookup"><span data-stu-id="4281c-145">Make sure to include .cer at the end.</span></span>

    $Configuration.GeneratedCertificatePath = "[C:\Path\To\Certificate.cer]"

<span data-ttu-id="4281c-146">Para ver o que você definiu, digite **$Configuration**.</span><span class="sxs-lookup"><span data-stu-id="4281c-146">To see what you set, type **$Configuration**.</span></span>

    > $Configuration

    Name                           Value
    ----                           -----
    GeneratedCertificatePath       C:\vnetcert.cer
    VnetSubscriptionId             efc239a4-88f9-2c5e-a9a1-3034c21ad496
    WebAppResourceGroup            vnetdemo-rg
    VnetResourceGroup              testase1-rg
    VnetName                       TestNetwork
    WebAppName                     vnetintdemoapp
    WebAppLocation                 centralus

<span data-ttu-id="4281c-147">O restante desta seção pressupõe que você tenha criado uma variável como acabamos de descrever.</span><span class="sxs-lookup"><span data-stu-id="4281c-147">The rest of this section assumes that you have a variable created as just described.</span></span>

##### <a name="declare-the-virtual-network-to-the-app"></a><span data-ttu-id="4281c-148">Declarar a rede virtual para o aplicativo</span><span class="sxs-lookup"><span data-stu-id="4281c-148">Declare the virtual network to the app</span></span>
<span data-ttu-id="4281c-149">Use o comando a seguir para informar ao aplicativo que ele usará essa rede virtual específica.</span><span class="sxs-lookup"><span data-stu-id="4281c-149">Use the following command to tell the app that it will be using this particular virtual network.</span></span> <span data-ttu-id="4281c-150">Isso fará com que o aplicativo gere os certificados necessários:</span><span class="sxs-lookup"><span data-stu-id="4281c-150">This will cause the app to generate necessary certificates:</span></span>

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -PropertyObject @{"VnetResourceId" = "/subscriptions/$($Configuration.VnetSubscriptionId)/resourceGroups/$($Configuration.VnetResourceGroup)/providers/Microsoft.ClassicNetwork/virtualNetworks/$($Configuration.VnetName)"} -Location $Configuration.WebAppLocation -ApiVersion 2015-07-01

<span data-ttu-id="4281c-151">Se este comando for bem-sucedido, **$vnet** deverá conter uma variável **Properties**.</span><span class="sxs-lookup"><span data-stu-id="4281c-151">If this command succeeds, **$vnet** should have a **Properties** variable in it.</span></span> <span data-ttu-id="4281c-152">A variável **Properties** deve conter uma impressão digital do certificado, bem como os dados do certificado.</span><span class="sxs-lookup"><span data-stu-id="4281c-152">The **Properties** variable should contain both a certificate thumbprint and the certificate data.</span></span>

##### <a name="upload-the-web-app-certificate-to-the-virtual-network"></a><span data-ttu-id="4281c-153">Carregar o certificado do aplicativo Web para a rede virtual</span><span class="sxs-lookup"><span data-stu-id="4281c-153">Upload the web app certificate to the virtual network</span></span>
<span data-ttu-id="4281c-154">Uma única etapa manual é necessária para cada combinação de assinatura e rede virtual.</span><span class="sxs-lookup"><span data-stu-id="4281c-154">A manual, one-time step is required for each subscription and virtual network combination.</span></span> <span data-ttu-id="4281c-155">Ou seja, se estiver conectando aplicativos na Assinatura A à Rede Virtual A, você precisará executar essa etapa apenas uma vez, independentemente de quantos aplicativos configurar.</span><span class="sxs-lookup"><span data-stu-id="4281c-155">That is, if you are connecting apps in Subscription A to Virtual Network A, you will need to do this step only once regardless of how many apps you configure.</span></span> <span data-ttu-id="4281c-156">Se estiver adicionando um novo aplicativo a outra rede virtual, isso precisará ser refeito.</span><span class="sxs-lookup"><span data-stu-id="4281c-156">If you are adding a new app to another virtual network, you'll need to do this again.</span></span> <span data-ttu-id="4281c-157">O motivo é que um conjunto de certificados é gerado em um nível de assinatura no Serviço de Aplicativo do Azure, e o conjunto é gerado uma vez para cada rede virtual à qual os aplicativos se conectarão.</span><span class="sxs-lookup"><span data-stu-id="4281c-157">The reason for this is that a set of certificates is generated at a subscription level in Azure App Service, and the set is generated once for each virtual network that the apps will connect to.</span></span>

<span data-ttu-id="4281c-158">Os certificados já terão sido definidos se você tiver seguido as etapas ou se tiver feito a integração com a mesma rede virtual usando o portal.</span><span class="sxs-lookup"><span data-stu-id="4281c-158">The certificates will have already been set if you followed these steps or if you integrated with the same virtual network by using the portal.</span></span>

<span data-ttu-id="4281c-159">A primeira etapa é gerar o arquivo .cer.</span><span class="sxs-lookup"><span data-stu-id="4281c-159">The first step is to generate the .cer file.</span></span> <span data-ttu-id="4281c-160">A segunda etapa é carregar o arquivo .cer para a rede virtual.</span><span class="sxs-lookup"><span data-stu-id="4281c-160">The second step is to upload the .cer file to your virtual network.</span></span> <span data-ttu-id="4281c-161">Para gerar o arquivo .cer da chamada à API na etapa anterior, execute os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="4281c-161">To generate the .cer file from the API call in the earlier step, run the following commands.</span></span>

    $certBytes = [System.Convert]::FromBase64String($vnet.Properties.certBlob)
    [System.IO.File]::WriteAllBytes("$($Configuration.GeneratedCertificatePath)", $certBytes)

<span data-ttu-id="4281c-162">O certificado estará no local que **$Configuration.GeneratedCertificatePath** especifica.</span><span class="sxs-lookup"><span data-stu-id="4281c-162">The certificate will be found in the location that **$Configuration.GeneratedCertificatePath** specifies.</span></span>

<span data-ttu-id="4281c-163">Para carregar o certificado manualmente, use o [Portal do Azure][azureportal] e **Procurar Rede Virtual (clássica)** > **Conexões VPN** > **Ponto a site** > **Gerenciar certificados**.</span><span class="sxs-lookup"><span data-stu-id="4281c-163">To upload the certificate manually, use the [Azure portal][azureportal] and **Browse Virtual Network (classic)** > **VPN connections** > **Point-to-site** > **Manage certificates**.</span></span> <span data-ttu-id="4281c-164">Nesse local, carregue seu certificado.</span><span class="sxs-lookup"><span data-stu-id="4281c-164">From here, upload your certificate.</span></span>

##### <a name="get-the-point-to-site-package"></a><span data-ttu-id="4281c-165">Obter o pacote de ponto a site</span><span class="sxs-lookup"><span data-stu-id="4281c-165">Get the point-to-site package</span></span>
<span data-ttu-id="4281c-166">A próxima etapa na configuração de uma conexão de rede virtual em um aplicativo Web é obter o pacote de ponto a site e fornecê-lo ao aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="4281c-166">The next step in setting up a virtual network connection on a web app is to get the point-to-site package and provide it to your web app.</span></span>

<span data-ttu-id="4281c-167">Salve o modelo a seguir em um arquivo chamado GetNetworkPackageUri.json em algum lugar no computador; por exemplo, C:\Azure\Templates\GetNetworkPackageUri.json.</span><span class="sxs-lookup"><span data-stu-id="4281c-167">Save the following template to a file called GetNetworkPackageUri.json somewhere on your computer, for example, C:\Azure\Templates\GetNetworkPackageUri.json.</span></span>

    {
        "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "certData": {
                "type": "string"
            },
            "certThumbprint": {
                "type": "string"
            },
            "networkName": {
                "type": "string"
            }
        },
        "variables": {
            "legacyVnetName": "[concat('Group ', resourceGroup().name, ' ', parameters('networkName'))]"
            },
            "resources": [
            ],
        "outputs" : {
            "PackageUri" :
            {
            "value" : "[listPackage(resourceId('Microsoft.ClassicNetwork/virtualNetworks/gateways/clientRootCertificates', parameters('networkName'), 'primary', parameters('certThumbprint')), '2014-06-01').packageUri]", "type" : "string"
            }
        }
    }


<span data-ttu-id="4281c-168">Defina os parâmetros de entrada:</span><span class="sxs-lookup"><span data-stu-id="4281c-168">Set input parameters:</span></span>

    $parameters = @{"certData" = $vnet.Properties.certBlob ;
    certThumbprint = $vnet.Properties.certThumbprint ;
    "networkName" = $Configuration.VnetName }

<span data-ttu-id="4281c-169">Chame o script:</span><span class="sxs-lookup"><span data-stu-id="4281c-169">Call the script:</span></span>

    $output = New-AzureRmResourceGroupDeployment -Name unused -ResourceGroupName $Configuration.VnetResourceGroup -TemplateParameterObject $parameters -TemplateFile C:\PATH\TO\GetNetworkPackageUri.json


<span data-ttu-id="4281c-170">A variável **$output.Outputs.packageUri** conterá agora o URI do pacote a ser fornecido ao aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="4281c-170">The variable **$output.Outputs.packageUri** will now contain the package URI to be given to your web app.</span></span>

##### <a name="upload-the-point-to-site-package-to-your-app"></a><span data-ttu-id="4281c-171">Carregue o pacote de ponto a site em seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="4281c-171">Upload the point-to-site package to your app</span></span>
<span data-ttu-id="4281c-172">A etapa final é fornecer o aplicativo com este pacote.</span><span class="sxs-lookup"><span data-stu-id="4281c-172">The final step is to provide the app with this package.</span></span> <span data-ttu-id="4281c-173">Basta executar o próximo comando:</span><span class="sxs-lookup"><span data-stu-id="4281c-173">Simply run the next command:</span></span>

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)/primary" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-07-01 -PropertyObject @{"VnetName" = $Configuration.VnetName ; "VpnPackageUri" = $($output.Outputs.packageUri).Value } -Location $Configuration.WebAppLocation

<span data-ttu-id="4281c-174">Se uma mensagem solicitar a confirmação de que você está substituindo um recurso existente, permita essa ação.</span><span class="sxs-lookup"><span data-stu-id="4281c-174">If a message asks you to confirm that you are overwriting an existing resource, make sure to allow it.</span></span>

<span data-ttu-id="4281c-175">Depois que o comando for bem-sucedido, o aplicativo deverá estar conectado à rede virtual.</span><span class="sxs-lookup"><span data-stu-id="4281c-175">After this command succeeds, your app should now be connected to the virtual network.</span></span> <span data-ttu-id="4281c-176">Para confirmar o êxito, vá para o console do aplicativo e digite o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4281c-176">To confirm success, go to your app console, and type the following:</span></span>

    SET WEBSITE_

<span data-ttu-id="4281c-177">Se houver uma variável de ambiente chamada WEBSITE_VNETNAME com um valor que corresponda ao nome da rede virtual de destino, isso indicará que todas as configurações tiveram êxito.</span><span class="sxs-lookup"><span data-stu-id="4281c-177">If there is an environment variable called WEBSITE_VNETNAME that has a value that matches the name of the target virtual network, all configurations have succeeded.</span></span>

### <a name="update-classic-vnet-integration-information"></a><span data-ttu-id="4281c-178">Atualizar informações de integração VNet clássica</span><span class="sxs-lookup"><span data-stu-id="4281c-178">Update classic VNet integration information</span></span>
<span data-ttu-id="4281c-179">Para atualizar ou ressincronizar suas informações, basta repetir as etapas seguidas ao criar a integração.</span><span class="sxs-lookup"><span data-stu-id="4281c-179">To update or resync your information, simply repeat the steps that you followed when you created the integration in the first place.</span></span> <span data-ttu-id="4281c-180">Essas etapas são:</span><span class="sxs-lookup"><span data-stu-id="4281c-180">Those steps are:</span></span>

1. <span data-ttu-id="4281c-181">Defina as informações de configuração.</span><span class="sxs-lookup"><span data-stu-id="4281c-181">Define your configuration information.</span></span>
2. <span data-ttu-id="4281c-182">Declare a rede virtual para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4281c-182">Declare the virtual network to the app.</span></span>
3. <span data-ttu-id="4281c-183">Obtenha o pacote de ponto a site.</span><span class="sxs-lookup"><span data-stu-id="4281c-183">Get the point-to-site package.</span></span>
4. <span data-ttu-id="4281c-184">Carregue o pacote de ponto a site no aplicativo</span><span class="sxs-lookup"><span data-stu-id="4281c-184">Upload the point-to-site package to your app.</span></span>

### <a name="disconnect-your-app-from-a-classic-vnet"></a><span data-ttu-id="4281c-185">Desconectar o aplicativo de uma VNet clássica</span><span class="sxs-lookup"><span data-stu-id="4281c-185">Disconnect your app from a classic VNet</span></span>
<span data-ttu-id="4281c-186">Para desconectar o aplicativo, você precisa das informações de configuração definidas durante a integração da rede virtual.</span><span class="sxs-lookup"><span data-stu-id="4281c-186">To disconnect the app, you need the configuration information that was set during virtual network integration.</span></span> <span data-ttu-id="4281c-187">Com essas informações, há um comando para desconectar o aplicativo da rede virtual.</span><span class="sxs-lookup"><span data-stu-id="4281c-187">Using that information, there is then one command to disconnect your app from your virtual network.</span></span>

    $vnet = Remove-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-07-01

## <a name="resource-manager-virtual-networks"></a><span data-ttu-id="4281c-188">Redes virtuais do Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="4281c-188">Resource Manager virtual networks</span></span>
<span data-ttu-id="4281c-189">As redes virtuais do Resource Manager têm APIs do Azure Resource Manager que simplificam alguns processos se comparadas com redes virtuais clássicas.</span><span class="sxs-lookup"><span data-stu-id="4281c-189">Resource Manager virtual networks have Azure Resource Manager APIs, which simplify some processes when compared with classic virtual networks.</span></span> <span data-ttu-id="4281c-190">Há um script que o ajudará a concluir as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="4281c-190">We have a script that will help you complete the following tasks:</span></span>

* <span data-ttu-id="4281c-191">Criar uma rede virtual do Gerenciador de Recursos e integrar o aplicativo a ela.</span><span class="sxs-lookup"><span data-stu-id="4281c-191">Create a Resource Manager virtual network and integrate your app with it.</span></span>
* <span data-ttu-id="4281c-192">Criar um gateway, configurar a conectividade ponto a site em uma rede virtual do Gerenciador de Recursos pré-existente e integrar o aplicativo a ela.</span><span class="sxs-lookup"><span data-stu-id="4281c-192">Create a gateway, configure point-to-site connectivity in a preexisting Resource Manager virtual network, and then integrate your app with it.</span></span>
* <span data-ttu-id="4281c-193">Integrar o aplicativo a uma rede virtual do Gerenciador de Recursos pré-existente que tem um gateway e habilitar a conectividade ponto a site.</span><span class="sxs-lookup"><span data-stu-id="4281c-193">Integrate your app with a preexisting Resource Manager virtual network that has a gateway and point-to-site connectivity enabled.</span></span>
* <span data-ttu-id="4281c-194">Desconecte o aplicativo da rede virtual.</span><span class="sxs-lookup"><span data-stu-id="4281c-194">Disconnect your app from your virtual network.</span></span>

### <a name="resource-manager-vnet-app-service-integration-script"></a><span data-ttu-id="4281c-195">Script de integração do Serviço de Aplicativo de VNet do Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="4281c-195">Resource Manager VNet App Service integration script</span></span>
<span data-ttu-id="4281c-196">Copie o script a seguir e salve-o em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="4281c-196">Copy the following script and save it to a file.</span></span> <span data-ttu-id="4281c-197">Se não quiser usar o script, sinta-se à vontade para aprender com ele e saber como configurar itens com uma rede virtual do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="4281c-197">If you don’t want to use the script, feel free to learn from it to see how to set things up with a Resource Manager virtual network.</span></span>

    function ReadHostWithDefault($message, $default)
    {
        $result = Read-Host "$message [$default]"
        if($result -eq "")
        {
            $result = $default
        }
            return $result
        }

    function PromptCustom($title, $optionValues, $optionDescriptions)
    {
        Write-Host $title
        Write-Host
        $a = @()
        for($i = 0; $i -lt $optionValues.Length; $i++){
            Write-Host "$($i+1))" $optionDescriptions[$i]
        }
        Write-Host

        while($true)
        {
            Write-Host "Choose an option: "
            $option = Read-Host
            $option = $option -as [int]

            if($option -ge 1 -and $option -le $optionValues.Length)
            {
                return $optionValues[$option-1]
            }
        }
    }

    function PromptYesNo($title, $message, $default = 0)
    {
        $yes = New-Object System.Management.Automation.Host.ChoiceDescription "&Yes", ""
        $no = New-Object System.Management.Automation.Host.ChoiceDescription "&No", ""
        $options = [System.Management.Automation.Host.ChoiceDescription[]]($yes, $no)
        $result = $host.ui.PromptForChoice($title, $message, $options, $default)
        return $result
    }

    function CreateVnet($resourceGroupName, $vnetName, $vnetAddressSpace, $vnetGatewayAddressSpace, $location)
    {
        Write-Host "Creating a new VNET"
        $gatewaySubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix $vnetGatewayAddressSpace
        New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName -Location $location -AddressPrefix $vnetAddressSpace -Subnet $gatewaySubnet
    }

    function CreateVnetGateway($resourceGroupName, $vnetName, $vnetIpName, $location, $vnetIpConfigName, $vnetGatewayName, $certificateData, $vnetPointToSiteAddressSpace)
    {
        $vnet = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName
        $subnet=Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet

        Write-Host "Creating a public IP address for this VNET"
        $pip = New-AzureRmPublicIpAddress -Name $vnetIpName -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
        $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $vnetIpConfigName -Subnet $subnet -PublicIpAddress $pip

        Write-Host "Adding a root certificate to this VNET"
        $root = New-AzureRmVpnClientRootCertificate -Name "AppServiceCertificate.cer" -PublicCertData $certificateData

        Write-Host "Creating Azure VNET Gateway. This may take up to an hour."
        New-AzureRmVirtualNetworkGateway -Name $vnetGatewayName -ResourceGroupName $resourceGroupName -Location $location -IpConfigurations $ipconf -GatewayType Vpn -VpnType RouteBased -EnableBgp $false -GatewaySku Basic -VpnClientAddressPool $vnetPointToSiteAddressSpace -VpnClientRootCertificates $root
    }

    function AddNewVnet($subscriptionId, $webAppResourceGroup, $webAppName)
    {
        Write-Host "Adding a new Vnet"
        Write-Host
        $vnetName = Read-Host "Specify a name for this Virtual Network"

        $vnetGatewayName="$($vnetName)-gateway"
        $vnetIpName="$($vnetName)-ip"
        $vnetIpConfigName="$($vnetName)-ipconf"

        # Virtual Network settings
        $vnetAddressSpace="10.0.0.0/8"
        $vnetGatewayAddressSpace="10.5.0.0/16"
        $vnetPointToSiteAddressSpace="172.16.0.0/16"

        $changeRequested = 0
        $resourceGroupName = $webAppResourceGroup

        while($changeRequested -eq 0)
        {
            Write-Host
            Write-Host "Currently, I will create a VNET with the following settings:"
            Write-Host
            Write-Host "Virtual Network Name: $vnetName"
            Write-Host "Resource Group Name:  $resourceGroupName"
            Write-Host "Gateway Name: $vnetGatewayName"
            Write-Host "Vnet IP name: $vnetIpName"
            Write-Host "Vnet IP config name:  $vnetIpConfigName"
            Write-Host "Address Space:$vnetAddressSpace"
            Write-Host "Gateway Address Space:$vnetGatewayAddressSpace"
            Write-Host "Point-To-Site Address Space:  $vnetPointToSiteAddressSpace"
            Write-Host
            $changeRequested = PromptYesNo "" "Do you wish to change these settings?" 1

            if($changeRequested -eq 0)
            {
                $vnetName = ReadHostWithDefault "Virtual Network Name" $vnetName
                $resourceGroupName = ReadHostWithDefault "Resource Group Name" $resourceGroupName
                $vnetGatewayName = ReadHostWithDefault "Vnet Gateway Name" $vnetGatewayName
                $vnetIpName = ReadHostWithDefault "Vnet IP name" $vnetIpName
                $vnetIpConfigName = ReadHostWithDefault "Vnet IP configuration name" $vnetIpConfigName
                $vnetAddressSpace = ReadHostWithDefault "Vnet Address Space" $vnetAddressSpace
                $vnetGatewayAddressSpace = ReadHostWithDefault "Vnet Gateway Address Space" $vnetGatewayAddressSpace
                $vnetPointToSiteAddressSpace = ReadHostWithDefault "Vnet Point-to-site Address Space" $vnetPointToSiteAddressSpace
            }
        }

        $ErrorActionPreference = "Stop";

        # We create the virtual network and add it here. The way this works is:
        # 1) Add the VNET association to the App. This allows the App to generate certificates, etc. for the VNET.
        # 2) Create the VNET and VNET gateway, add the certificates, create the public IP, etc., required for the gateway
        # 3) Get the VPN package from the gateway and pass it back to the App.

        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup
        $location = $webApp.Location

        Write-Host "Creating App association to VNET"
        $propertiesObject = @{
         "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($resourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
        }
        $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        CreateVnet $resourceGroupName $vnetName $vnetAddressSpace $vnetGatewayAddressSpace $location

        CreateVnetGateway $resourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

        Write-Host "Retrieving VPN Package and supplying to App"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName -VirtualNetworkGatewayName $vnetGatewayName -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at the start and the end of the URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put the VPN client configuration package onto the App
        $PropertiesObject = @{
        "vnetName" = $VirtualNetworkName; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        Write-Host "Finished!"
    }

    function AddExistingVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $ErrorActionPreference = "Stop";

        # At this point, the gateway should be able to be joined to an App, but may require some minor tweaking. We will declare to the App now to use this VNET
        Write-Host "Getting App information"
        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $location = $webApp.Location

        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected to VNET $currentVnet"
        }

        # Display existing vnets
        $vnets = Get-AzureRmVirtualNetwork
        $vnetNames = @()
        foreach($vnet in $vnets)
        {
            $vnetNames += $vnet.Name
        }

        Write-Host
        $vnet = PromptCustom "Select a VNET to integrate with" $vnets $vnetNames

        # We need to check if this VNET is able to be joined to a App, based on following criteria
            # If there is no gateway, we can create one.
            # If there is a gateway:
                # It must be of type Vpn
                # It must be of VpnType RouteBased
                # If it doesn't have the right certificate, we will need to add it.
                # If it doesn't have a point-to-site range, we will need to add it.

        $gatewaySubnet = $vnet.Subnets | Where-Object { $_.Name -eq "GatewaySubnet" }

        if($gatewaySubnet -eq $null -or $gatewaySubnet.IpConfigurations -eq $null -or $gatewaySubnet.IpConfigurations.Count -eq 0)
        {
            $ErrorActionPreference = "Continue";
            # There is no gateway. We need to create one.
            Write-Host "This Virtual Network has no gateway. I will need to create one."

            $vnetName = $vnet.Name
            $vnetGatewayName="$($vnetName)-gateway"
            $vnetIpName="$($vnetName)-ip"
            $vnetIpConfigName="$($vnetName)-ipconf"

            # Virtual Network settings
            $vnetAddressSpace="10.0.0.0/8"
            $vnetGatewayAddressSpace="10.5.0.0/16"
            $vnetPointToSiteAddressSpace="172.16.0.0/16"

            $changeRequested = 0

            Write-Host "Your VNET is in the address space $($vnet.AddressSpace.AddressPrefixes), with the following Subnets:"
            foreach($subnet in $vnet.Subnets)
            {
                Write-Host "$($subnet.Name): $($subnet.AddressPrefix)"
            }

            $vnetGatewayAddressSpace = Read-Host "Please choose a GatewaySubnet address space"

            while($changeRequested -eq 0)
            {
                Write-Host
                Write-Host "Currently, I will create a VNET gateway with the following settings:"
                Write-Host
                Write-Host "Virtual Network Name: $vnetName"
                Write-Host "Resource Group Name:  $($vnet.ResourceGroupName)"
                Write-Host "Gateway Name: $vnetGatewayName"
                Write-Host "Vnet IP name: $vnetIpName"
                Write-Host "Vnet IP config name:  $vnetIpConfigName"
                Write-Host "Address Space:$($vnet.AddressSpace.AddressPrefixes)"
                Write-Host "Gateway Address Space:$vnetGatewayAddressSpace"
                Write-Host "Point-To-Site Address Space:  $vnetPointToSiteAddressSpace"
                Write-Host
                $changeRequested = PromptYesNo "" "Do you wish to change these settings?" 1

                if($changeRequested -eq 0)
                {
                    $vnetGatewayName = ReadHostWithDefault "Vnet Gateway Name" $vnetGatewayName
                    $vnetIpName = ReadHostWithDefault "Vnet IP name" $vnetIpName
                    $vnetIpConfigName = ReadHostWithDefault "Vnet IP configuration name" $vnetIpConfigName
                    $vnetGatewayAddressSpace = ReadHostWithDefault "Vnet Gateway Address Space" $vnetGatewayAddressSpace
                    $vnetPointToSiteAddressSpace = ReadHostWithDefault "Vnet Point-to-site Address Space" $vnetPointToSiteAddressSpace
                }
            }

            $ErrorActionPreference = "Stop";

            Write-Host "Creating App association to VNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # If there is no gateway subnet, we need to create one.
            if($gatewaySubnet -eq $null)
            {
                $gatewaySubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -AddressPrefix $vnetGatewayAddressSpace
                $vnet.Subnets.Add($gatewaySubnet);
                Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
            }

            CreateVnetGateway $vnet.ResourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

            $gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $vnet.ResourceGroupName -Name $vnetGatewayName
        }
        else
        {
            $uriParts = $gatewaySubnet.IpConfigurations[0].Id.Split('/')
            $gatewayResourceGroup = $uriParts[4]
            $gatewayName = $uriParts[8]

            $gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $vnet.ResourceGroupName -Name $gatewayName

            # validate gateway types, etc.
            if($gateway.GatewayType -ne "Vpn")
            {
                Write-Error "This gateway is not of the Vpn type. It cannot be joined to an App."
                return
            }

            if($gateway.VpnType -ne "RouteBased")
            {
                Write-Error "This gateways Vpn type is not RouteBased. It cannot be joined to an App."
                return
            }

            if($gateway.VpnClientConfiguration -eq $null -or $gateway.VpnClientConfiguration.VpnClientAddressPool -eq $null)
            {
                Write-Host "This gateway does not have a Point-to-site Address Range. Please specify one in CIDR notation, e.g. 10.0.0.0/8"
                $pointToSiteAddress = Read-Host "Point-To-Site Address Space"
                Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $gateway.Name -VpnClientAddressPool $pointToSiteAddress
            }

            Write-Host "Creating App association to VNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnet.Name)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # We need to check if the certificate here exists in the gateway.
            $certificates = $gateway.VpnClientConfiguration.VpnClientRootCertificates

            $certFound = $false
            foreach($certificate in $certificates)
            {
                if($certificate.PublicCertData -eq $virtualNetwork.Properties.CertBlob)
                {
                    $certFound = $true
                    break
                }
            }

            if(-not $certFound)
            {
                Write-Host "Adding certificate"
                Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName "AppServiceCertificate.cer" -PublicCertData $virtualNetwork.Properties.CertBlob -VirtualNetworkGatewayName $gateway.Name
            }
        }

        # Now finish joining by getting the VPN package and giving it to the App
        Write-Host "Retrieving VPN Package and supplying to App"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $vnet.ResourceGroupName -VirtualNetworkGatewayName $gateway.Name -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at the start and the end of the URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put the VPN client configuration package onto the App
        $PropertiesObject = @{
        "vnetName" = $vnet.Name; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

        Write-Host "Finished!"
    }

    function RemoveVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected to VNET $currentVnet"

            Remove-AzureRmResource -ResourceName "$($webAppName)/$($currentVnet)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        }
            else
        {
            Write-Host "Not connected to a VNET."
        }
    }

    Write-Host "Please Login"
    Login-AzureRmAccount

    # Choose subscription. If there's only one we will choose automatically

    $subs = Get-AzureRmSubscription
    $subscriptionId = ""

    if($subs.Length -eq 0)
    {
        Write-Error "No subscriptions bound to this account."
        return
    }

    if($subs.Length -eq 1)
    {
        $subscriptionId = $subs[0].SubscriptionId
    }
    else
    {
        $subscriptionChoices = @()
        $subscriptionValues = @()

        foreach($subscription in $subs){
        $subscriptionChoices += "$($subscription.SubscriptionName) ($($subscription.SubscriptionId))";
        $subscriptionValues += ($subscription.SubscriptionId);
        }

        $subscriptionId = PromptCustom "Choose a subscription" $subscriptionValues $subscriptionChoices
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    $resourceGroup = Read-Host "Please enter the Resource Group of your App"

    $appName = Read-Host "Please enter the Name of your App"

    $options = @("Add a NEW Virtual Network to an App", "Add an EXISTING Virtual Network to an App", "Remove a Virtual Network from an App");
    $optionValues = @(0, 1, 2)
    $option = PromptCustom "What do you want to do?" $optionValues $options

    if($option -eq 0)
    {
        AddNewVnet $subscriptionId $resourceGroup $appName
    }
    if($option -eq 1)
    {
        AddExistingVnet $subscriptionId $resourceGroup $appName
    }
    if($option -eq 2)
    {
        RemoveVnet $subscriptionId $resourceGroup $appName
    }

<span data-ttu-id="4281c-198">Salve uma cópia do script.</span><span class="sxs-lookup"><span data-stu-id="4281c-198">Save a copy of the script.</span></span> <span data-ttu-id="4281c-199">Neste artigo, ele é chamado de V2VnetAllinOne.ps1, mas você pode usar outro nome.</span><span class="sxs-lookup"><span data-stu-id="4281c-199">In this article, it is called V2VnetAllinOne.ps1, but you can use another name.</span></span> <span data-ttu-id="4281c-200">Não há nenhum argumento para esse script.</span><span class="sxs-lookup"><span data-stu-id="4281c-200">There are no arguments for this script.</span></span> <span data-ttu-id="4281c-201">Basta executá-lo.</span><span class="sxs-lookup"><span data-stu-id="4281c-201">You simply run it.</span></span> <span data-ttu-id="4281c-202">A primeira coisa que o script fará é solicitar sua entrada.</span><span class="sxs-lookup"><span data-stu-id="4281c-202">The first thing the script will do is prompt you to sign in.</span></span> <span data-ttu-id="4281c-203">Após sua entrada, o script obterá os detalhes sobre sua conta e retornará uma lista de assinaturas.</span><span class="sxs-lookup"><span data-stu-id="4281c-203">After you sign in, the script gets details about your account and returns a list of subscriptions.</span></span> <span data-ttu-id="4281c-204">Sem contar a solicitação de suas credenciais, a execução inicial do script tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="4281c-204">Not counting the request for your credentials, the initial script execution looks like this:</span></span>

    PS C:\Users\ccompy\Documents\VNET> .\V2VnetAllInOne.ps1
    Please Login

    Environment           : AzureCloud
    Account               : ccompy@microsoft.com
    TenantId              : 722278f-fef1-499f-91ab-2323d011db47
    SubscriptionId        : af5358e1-acac-2c90-a9eb-722190abf47a
    CurrentStorageAccount :

    Choose a subscription

    1) <span data-ttu-id="4281c-205">Assinatura de demonstração (af5358e1-acac-2c90-a9eb-722190abf47a)</span><span class="sxs-lookup"><span data-stu-id="4281c-205">Demo Subscription (af5358e1-acac-2c90-a9eb-722190abf47a)</span></span>
    2) <span data-ttu-id="4281c-206">Teste MS (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)</span><span class="sxs-lookup"><span data-stu-id="4281c-206">MS Test (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)</span></span>
    3) <span data-ttu-id="4281c-207">Assinatura de demonstração Purple (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)</span><span class="sxs-lookup"><span data-stu-id="4281c-207">Purple Demo Subscription (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)</span></span>

    <span data-ttu-id="4281c-208">Escolher uma opção: 3</span><span class="sxs-lookup"><span data-stu-id="4281c-208">Choose an option: 3</span></span>

    <span data-ttu-id="4281c-209">Conta      : ccompy@microsoft.com Ambiente  : Assinatura da Nuvem do Azure: 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Locatário       : 722278f-fef1-499f-91ab-2323d011db47</span><span class="sxs-lookup"><span data-stu-id="4281c-209">Account      : ccompy@microsoft.com Environment  : AzureCloud Subscription : 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Tenant       : 722278f-fef1-499f-91ab-2323d011db47</span></span>

    <span data-ttu-id="4281c-210">Insira o grupo de recursos de seu Aplicativo: hcdemo rg Insira o nome do seu aplicativo: v2vnetpowershell O que você deseja fazer?</span><span class="sxs-lookup"><span data-stu-id="4281c-210">Please enter the Resource Group of your App: hcdemo-rg Please enter the Name of your App: v2vnetpowershell What do you want to do?</span></span>

    1) <span data-ttu-id="4281c-211">Adicionar uma NOVA rede Virtual a um aplicativo</span><span class="sxs-lookup"><span data-stu-id="4281c-211">Add a NEW Virtual Network to an App</span></span>
    2) <span data-ttu-id="4281c-212">Adicionar uma rede virtual EXISTENTE a um aplicativo</span><span class="sxs-lookup"><span data-stu-id="4281c-212">Add an EXISTING Virtual Network to an App</span></span>
    3) <span data-ttu-id="4281c-213">Remover uma rede Virtual de um aplicativo</span><span class="sxs-lookup"><span data-stu-id="4281c-213">Remove a Virtual Network from an App</span></span>

<span data-ttu-id="4281c-214">O restante desta seção explica cada uma dessas três opções.</span><span class="sxs-lookup"><span data-stu-id="4281c-214">The rest of this section explains each of those three options.</span></span>

### <a name="create-a-resource-manager-vnet-and-integrate-with-it"></a><span data-ttu-id="4281c-215">Criar uma VNet do Gerenciador de Recursos e realizar a integração a ela</span><span class="sxs-lookup"><span data-stu-id="4281c-215">Create a Resource Manager VNet and integrate with it</span></span>
<span data-ttu-id="4281c-216">Para criar uma nova rede virtual que usa o modelo de implantação do Gerenciador de Recursos e integrá-la a seu aplicativo, escolha **1) Adicionar uma NOVA Rede Virtual a um Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="4281c-216">To create a new virtual network that uses the Resource Manager deployment model and integrate it with your app, select **1) Add a NEW Virtual Network to an App**.</span></span> <span data-ttu-id="4281c-217">Isso solicitará o nome da rede virtual.</span><span class="sxs-lookup"><span data-stu-id="4281c-217">This will prompt you for the name of the virtual network.</span></span> <span data-ttu-id="4281c-218">No meu caso, como você pode ver nas configurações a seguir, usei o nome v2pshell.</span><span class="sxs-lookup"><span data-stu-id="4281c-218">In my case, as you can see in the following settings, I used the name, v2pshell.</span></span>

<span data-ttu-id="4281c-219">O script fornece os detalhes sobre a rede virtual que está sendo criada.</span><span class="sxs-lookup"><span data-stu-id="4281c-219">The script gives the details about the virtual network that's being created.</span></span> <span data-ttu-id="4281c-220">Se eu quiser, posso alterar qualquer um dos valores.</span><span class="sxs-lookup"><span data-stu-id="4281c-220">If I want, I can change any of the values.</span></span> <span data-ttu-id="4281c-221">No exemplo em execução, criei uma rede virtual com as seguintes configurações:</span><span class="sxs-lookup"><span data-stu-id="4281c-221">In this example execution, I created a virtual network that has the following settings:</span></span>

    Virtual Network Name:         v2pshell
    Resource Group Name:          hcdemo-rg
    Gateway Name:                 v2pshell-gateway
    Vnet IP name:                 v2pshell-ip
    Vnet IP config name:          v2pshell-ipconf
    Address Space:                10.0.0.0/8
    Gateway Address Space:        10.5.0.0/16
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish to change these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):

<span data-ttu-id="4281c-222">Se quiser alterar algum dos valores, digite **Y** e faça as alterações.</span><span class="sxs-lookup"><span data-stu-id="4281c-222">If you want to change any of the values, type **Y** and make the changes.</span></span> <span data-ttu-id="4281c-223">Quando estiver satisfeito com as configurações de rede virtual, digite **N** ou apenas pressione Enter quando receber a solicitação para alterar as configurações.</span><span class="sxs-lookup"><span data-stu-id="4281c-223">When you are happy with the virtual network settings, type **N** or simply press Enter when prompted about changing the settings.</span></span> <span data-ttu-id="4281c-224">Desse ponto até a conclusão, o script informará um pouco do que está fazendo até começar a criar o gateway de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="4281c-224">From there on until completion, the script will tell you some of what it' i's doing until it starts to create the virtual network gateway.</span></span> <span data-ttu-id="4281c-225">Essa etapa pode demorar até uma hora.</span><span class="sxs-lookup"><span data-stu-id="4281c-225">That step can take up to an hour.</span></span> <span data-ttu-id="4281c-226">Não há um indicador de progresso durante essa fase, mas o script informará quando o gateway for criado.</span><span class="sxs-lookup"><span data-stu-id="4281c-226">There is no progress indicator during this phase, but the script will let you know when the gateway has been created.</span></span>

<span data-ttu-id="4281c-227">Após a conclusão do script, ele informará que foi **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="4281c-227">When the script finishes, it will say **Finished**.</span></span> <span data-ttu-id="4281c-228">Neste ponto, você terá uma rede virtual do Gerenciador de Recursos que tem o nome e as configurações que você selecionou.</span><span class="sxs-lookup"><span data-stu-id="4281c-228">At this point, you will have a Resource Manager virtual network that has the name and settings that you selected.</span></span> <span data-ttu-id="4281c-229">Essa nova rede virtual também será integrada ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4281c-229">This new virtual network will also be integrated with your app.</span></span>

### <a name="integrate-your-app-with-a-preexisting-resource-manager-vnet"></a><span data-ttu-id="4281c-230">Integrar seu aplicativo a uma VNet pré-existente do Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="4281c-230">Integrate your app with a preexisting Resource Manager VNet</span></span>
<span data-ttu-id="4281c-231">Ao fazer a integração a uma rede virtual pré-existente, se você fornecer uma rede virtual do Gerenciador de Recursos que não tenha um gateway ou a conectividade ponto a site, o script fará a configuração.</span><span class="sxs-lookup"><span data-stu-id="4281c-231">When you're integrating with a preexisting virtual network, if you provide a Resource Manager virtual network that doesn’t have a gateway or point-to-site connectivity, the script will set that up.</span></span> <span data-ttu-id="4281c-232">Se a VNET já tiver isso configurado, o script irá direto para a integração do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4281c-232">If the VNET already has those things set up, the script goes straight to the app integration.</span></span> <span data-ttu-id="4281c-233">Para iniciar esse processo, basta selecionar **2) Adicionar uma Rede Virtual EXISTENTE a um Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="4281c-233">To start this process, simply select **2) Add an EXISTING Virtual Network to an App**.</span></span>

<span data-ttu-id="4281c-234">Essa opção só funcionará se você tiver uma rede virtual pré-existente do Gerenciador de Recursos na mesma assinatura do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4281c-234">This option works only if you have a preexisting Resource Manager virtual network that is in the same subscription as your app.</span></span> <span data-ttu-id="4281c-235">Após escolher a opção, você verá uma lista de redes virtuais do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="4281c-235">After you select the option, you will be presented with a list of your Resource Manager virtual networks.</span></span>   

    Select a VNET to integrate with

    1) <span data-ttu-id="4281c-236">v2demonetwork</span><span class="sxs-lookup"><span data-stu-id="4281c-236">v2demonetwork</span></span>
    2) <span data-ttu-id="4281c-237">v2pshell</span><span class="sxs-lookup"><span data-stu-id="4281c-237">v2pshell</span></span>
    3) <span data-ttu-id="4281c-238">v2vnetintdemo</span><span class="sxs-lookup"><span data-stu-id="4281c-238">v2vnetintdemo</span></span>
    4) <span data-ttu-id="4281c-239">v2asenetwork</span><span class="sxs-lookup"><span data-stu-id="4281c-239">v2asenetwork</span></span>
    5) <span data-ttu-id="4281c-240">v2pshell2</span><span class="sxs-lookup"><span data-stu-id="4281c-240">v2pshell2</span></span>

    <span data-ttu-id="4281c-241">Escolher uma opção: 5</span><span class="sxs-lookup"><span data-stu-id="4281c-241">Choose an option: 5</span></span>

<span data-ttu-id="4281c-242">Basta selecionar a rede virtual com a qual você deseja fazer a integração.</span><span class="sxs-lookup"><span data-stu-id="4281c-242">Simply select the virtual network that you want to integrate with.</span></span> <span data-ttu-id="4281c-243">Se você já tiver um gateway com a conectividade ponto a site habilitada, o script simplesmente integrará seu aplicativo à rede virtual.</span><span class="sxs-lookup"><span data-stu-id="4281c-243">If you already have a gateway that has point-to-site connectivity enabled, the script will simply integrate your app with your virtual network.</span></span> <span data-ttu-id="4281c-244">Se não tiver um gateway, você precisará especificar a sub-rede de gateway.</span><span class="sxs-lookup"><span data-stu-id="4281c-244">If you do not have a gateway, you will need to specify the gateway subnet.</span></span> <span data-ttu-id="4281c-245">A sub-rede do gateway deve estar em seu espaço de endereço de Rede Virtual e não pode estar em outra sub-rede.</span><span class="sxs-lookup"><span data-stu-id="4281c-245">Your gateway subnet must be in your virtual network address space, and it cannot be in any other subnet.</span></span> <span data-ttu-id="4281c-246">se você tiver uma rede virtual sem um gateway e executar essa etapa, verá o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4281c-246">If you have a virtual network without a gateway and run this step, things look like this:</span></span>

    This Virtual Network has no gateway. I will need to create one.
    Your VNET is in the address space 172.16.0.0/16, with the following Subnets:
    default: 172.16.0.0/24
    Please choose a GatewaySubnet address space: 172.16.1.0/26

<span data-ttu-id="4281c-247">Neste exemplo, criei um gateway de rede virtual que tem as seguintes configurações:</span><span class="sxs-lookup"><span data-stu-id="4281c-247">In this example, I created a virtual network gateway that has the following settings:</span></span>

    Virtual Network Name:         v2pshell2
    Resource Group Name:          vnetdemo-rg
    Gateway Name:                 v2pshell2-gateway
    Vnet IP name:                 v2pshell2-ip
    Vnet IP config name:          v2pshell2-ipconf
    Address Space:                172.16.0.0/16
    Gateway Address Space:        172.16.1.0/26
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish to change these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):
    Creating App association to VNET

<span data-ttu-id="4281c-248">Se quiser, você pode alterar as configurações.</span><span class="sxs-lookup"><span data-stu-id="4281c-248">If you want to change any of those settings, you can do so.</span></span> <span data-ttu-id="4281c-249">Caso contrário, pressione Enter e o script criará o gateway e anexará o aplicativo à rede virtual.</span><span class="sxs-lookup"><span data-stu-id="4281c-249">Otherwise, press Enter and the script will create your gateway and attach your app to your virtual network.</span></span> <span data-ttu-id="4281c-250">O tempo de criação do gateway ainda é de uma hora; portanto, lembre-se disso.</span><span class="sxs-lookup"><span data-stu-id="4281c-250">The gateway creation time is still an hour, though, so make sure you keep that in mind.</span></span> <span data-ttu-id="4281c-251">Quando tudo estiver concluído, o script informará que foi **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="4281c-251">When everything is finished, the script will say **Finished**.</span></span>

### <a name="disconnect-your-app-from-a-resource-manager-vnet"></a><span data-ttu-id="4281c-252">Desconectar o aplicativo de uma VNet do Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="4281c-252">Disconnect your app from a Resource Manager VNet</span></span>
<span data-ttu-id="4281c-253">A desconexão de seu aplicativo da rede virtual não desativa o gateway nem desabilita a conectividade ponto a site.</span><span class="sxs-lookup"><span data-stu-id="4281c-253">Disconnecting your app from your virtual network does not take down the gateway or disable point-to-site connectivity.</span></span> <span data-ttu-id="4281c-254">Afinal de contas, você poderia usá-los para alguma outra coisa.</span><span class="sxs-lookup"><span data-stu-id="4281c-254">You might, after all, be using it for something else.</span></span> <span data-ttu-id="4281c-255">Também não o desconecta de outros aplicativos além daquele que você forneceu.</span><span class="sxs-lookup"><span data-stu-id="4281c-255">It also does not disconnect it from any other apps other than the one you provided.</span></span> <span data-ttu-id="4281c-256">Para executar essa ação, selecione **3) Remover uma Rede Virtual de um Aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="4281c-256">To perform this action, select **3) Remove a Virtual Network from an App**.</span></span> <span data-ttu-id="4281c-257">Quando você fizer isso, verá algo assim:</span><span class="sxs-lookup"><span data-stu-id="4281c-257">When you do so, you will see something like this:</span></span>

    Currently connected to VNET v2pshell

    Confirm
    Are you sure you want to delete the following resource:
    /subscriptions/edcc99a4-b7f9-4b5e-a9a1-3034c51db496/resourceGroups/hcdemo-rg/providers/Microsoft.Web/sites/v2vnetpowers
    hell/virtualNetworkConnections/v2pshell
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):

<span data-ttu-id="4281c-258">Embora o script indique a exclusão, ele não exclui a rede virtual.</span><span class="sxs-lookup"><span data-stu-id="4281c-258">Although the script says delete, it does not delete the virtual network.</span></span> <span data-ttu-id="4281c-259">Ele está simplesmente removendo a integração.</span><span class="sxs-lookup"><span data-stu-id="4281c-259">It’s just removing the integration.</span></span> <span data-ttu-id="4281c-260">Após confirmar que é isso o que você quer fazer, o comando será processado rapidamente e mostrará **True** quando for concluído.</span><span class="sxs-lookup"><span data-stu-id="4281c-260">After you confirm that this is what you want to do, the command is processed quite quickly and tells you **True** when it is done.</span></span>

<!--Links-->
[createvpngateway]: http://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/
[azureportal]: http://portal.azure.com
