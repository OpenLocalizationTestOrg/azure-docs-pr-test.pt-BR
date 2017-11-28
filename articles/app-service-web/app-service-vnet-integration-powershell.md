---
title: aaaConnect sua rede virtual do aplicativo tooyour usando o PowerShell
description: "Instruções sobre como tooconnect tooand funcionam com redes virtuais usando o PowerShell"
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
ms.openlocfilehash: c9d0fa99d02cab7b2c7211a1b2f7b7d0cd27ee8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-app-tooyour-virtual-network-by-using-powershell"></a><span data-ttu-id="54640-103">Conecte-se a sua rede virtual do aplicativo tooyour usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="54640-103">Connect your app tooyour virtual network by using PowerShell</span></span>
## <a name="overview"></a><span data-ttu-id="54640-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="54640-104">Overview</span></span>
<span data-ttu-id="54640-105">No serviço de aplicativo do Azure, você pode se conectar a seu aplicativo (web, móveis ou a API) tooan rede virtual do Azure (VNet) em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="54640-105">In Azure App Service, you can connect your app (web, mobile, or API) tooan Azure virtual network (VNet) in your subscription.</span></span> <span data-ttu-id="54640-106">Esse recurso é chamado de Integração VNet.</span><span class="sxs-lookup"><span data-stu-id="54640-106">This feature is called VNet Integration.</span></span> <span data-ttu-id="54640-107">recurso de integração da VNet Olá não deve ser confundido com o recurso de ambiente de serviço de aplicativo hello, que permite que você toorun uma instância do serviço de aplicativo do Azure em sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="54640-107">hello VNet Integration feature should not be confused with hello App Service Environment feature, which allows you toorun an instance of Azure App Service in your virtual network.</span></span>

<span data-ttu-id="54640-108">recurso de integração da VNet Olá tem uma interface de usuário (UI) no novo portal de saudação que você pode usar toointegrate com redes virtuais que são implantadas usando o modelo de implantação clássico hello ou modelo de implantação do Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="54640-108">hello VNet Integration feature has a user interface (UI) in hello new portal that you can use toointegrate with virtual networks that are deployed by using either hello classic deployment model or hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="54640-109">Se você quiser toolearn mais sobre o recurso de hello, consulte [integrar seu aplicativo com uma rede virtual Azure](web-sites-integrate-with-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="54640-109">If you want toolearn more about hello feature, see [Integrate your app with an Azure virtual network](web-sites-integrate-with-vnet.md).</span></span>

<span data-ttu-id="54640-110">Este artigo é não sobre como toouse Olá da interface do usuário, mas em vez disso, sobre como tooenable integração usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="54640-110">This article is not about how toouse hello UI but rather about how tooenable integration by using PowerShell.</span></span> <span data-ttu-id="54640-111">Como comandos Olá para cada modelo de implantação são diferentes, este artigo possui uma seção para cada modelo de implantação.</span><span class="sxs-lookup"><span data-stu-id="54640-111">Because hello commands for each deployment model are different, this article has a section for each deployment model.</span></span>  

<span data-ttu-id="54640-112">Antes de continuar a ler este artigo, verifique se você tem:</span><span class="sxs-lookup"><span data-stu-id="54640-112">Before you continue with this article, ensure that you have:</span></span>

* <span data-ttu-id="54640-113">saudação do que SDK do Azure PowerShell mais recente instalado.</span><span class="sxs-lookup"><span data-stu-id="54640-113">hello latest Azure PowerShell SDK installed.</span></span> <span data-ttu-id="54640-114">Você pode instalá-lo com Olá Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="54640-114">You can install this with hello Web Platform Installer.</span></span>
* <span data-ttu-id="54640-115">Um aplicativo no Serviço de Aplicativo do Azure em execução em uma SKU Standard ou Premium.</span><span class="sxs-lookup"><span data-stu-id="54640-115">An app in Azure App Service running in a Standard or Premium SKU.</span></span>

## <a name="classic-virtual-networks"></a><span data-ttu-id="54640-116">Redes virtuais clássicas</span><span class="sxs-lookup"><span data-stu-id="54640-116">Classic virtual networks</span></span>
<span data-ttu-id="54640-117">Esta seção explica três tarefas para redes virtuais que usam o modelo de implantação clássico hello:</span><span class="sxs-lookup"><span data-stu-id="54640-117">This section explains three tasks for virtual networks that use hello classic deployment model:</span></span>

1. <span data-ttu-id="54640-118">Conecte seu aplicativo tooa preexistentes rede virtual que tem um gateway e é configurado para conectividade ponto a site.</span><span class="sxs-lookup"><span data-stu-id="54640-118">Connect your app tooa preexisting virtual network that has a gateway and is configured for point-to-site connectivity.</span></span>
2. <span data-ttu-id="54640-119">Atualize as informações de integração de rede virtual para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="54640-119">Update your virtual network integration information for your app.</span></span>
3. <span data-ttu-id="54640-120">Desconecte o aplicativo da rede virtual.</span><span class="sxs-lookup"><span data-stu-id="54640-120">Disconnect your app from your virtual network.</span></span>

### <a name="connect-an-app-tooa-classic-vnet"></a><span data-ttu-id="54640-121">Conecte-se um aplicativo tooa VNet clássico</span><span class="sxs-lookup"><span data-stu-id="54640-121">Connect an app tooa classic VNet</span></span>
<span data-ttu-id="54640-122">tooconnect uma rede virtual do tooa de aplicativo, siga estas três etapas:</span><span class="sxs-lookup"><span data-stu-id="54640-122">tooconnect an app tooa virtual network, follow these three steps:</span></span>

1. <span data-ttu-id="54640-123">Declare o aplicativo da web de toohello que ele for ingressar em uma rede virtual específico.</span><span class="sxs-lookup"><span data-stu-id="54640-123">Declare toohello web app that it will be joining a particular virtual network.</span></span> <span data-ttu-id="54640-124">aplicativo Hello irá gerar um certificado que será dada rede virtual toohello para conectividade ponto a site.</span><span class="sxs-lookup"><span data-stu-id="54640-124">hello app will generate a certificate that will be given toohello virtual network for point-to-site connectivity.</span></span>
2. <span data-ttu-id="54640-125">Carregar Olá web aplicativo certificado toohello VPN e, em seguida, recuperar o URI de pacote VPN de ponto para site do hello.</span><span class="sxs-lookup"><span data-stu-id="54640-125">Upload hello web app certificate toohello virtual network, and then retrieve hello point-to-site VPN package URI.</span></span>
3. <span data-ttu-id="54640-126">Atualize conexão de rede virtual do aplicativo da web de saudação com URI de pacote de ponto para site hello.</span><span class="sxs-lookup"><span data-stu-id="54640-126">Update hello web app's virtual network connection with hello point-to-site package URI.</span></span>

<span data-ttu-id="54640-127">Hello primeira e terceira etapas são totalmente programável por scripts, mas a segunda etapa de saudação exige uma única ação manual por meio do portal hello, ou acesso tooperform **colocar** ou **PATCH** ações na rede virtual Olá Ponto de extremidade do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="54640-127">hello first and third steps are fully scriptable, but hello second step requires a one-time, manual action through hello portal, or access tooperform **PUT** or **PATCH** actions on hello virtual network Azure Resource Manager endpoint.</span></span> <span data-ttu-id="54640-128">Entre em contato com suporte do Azure toohave isso habilitado.</span><span class="sxs-lookup"><span data-stu-id="54640-128">Contact Azure Support toohave this enabled.</span></span> <span data-ttu-id="54640-129">Antes de começar, verifique se você tem uma rede virtual clássica que tenha a conectividade ponto a site já habilitada e um gateway implantado.</span><span class="sxs-lookup"><span data-stu-id="54640-129">Before you start, make sure that you have a classic virtual network that has point-to-site connectivity already enabled and a deployed gateway.</span></span> <span data-ttu-id="54640-130">toocreate Olá gateway e habilitar ponto a site conectividade, você precisa toouse portal de saudação conforme descrito em [criar um gateway VPN][createvpngateway].</span><span class="sxs-lookup"><span data-stu-id="54640-130">toocreate hello gateway and enable point-to-site connectivity, you need toouse hello portal as described at [Creating a VPN gateway][createvpngateway].</span></span>

<span data-ttu-id="54640-131">rede virtual clássica Hello precisa toobe Olá a mesma assinatura que o serviço de aplicativo planejar que mantém o aplicativo hello que você estiver integrando.</span><span class="sxs-lookup"><span data-stu-id="54640-131">hello classic virtual network needs toobe in hello same subscription as your App Service plan that holds hello app that you are integrating with.</span></span>

##### <a name="set-up-azure-powershell-sdk"></a><span data-ttu-id="54640-132">Configurar o SDK do Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="54640-132">Set up Azure PowerShell SDK</span></span>
<span data-ttu-id="54640-133">Abra uma janela do PowerShell e configure sua conta e assinatura do Azure usando:</span><span class="sxs-lookup"><span data-stu-id="54640-133">Open a PowerShell window and set up your Azure account and subscription by using:</span></span>

    Login-AzureRmAccount

<span data-ttu-id="54640-134">Esse comando abrirá um prompt tooget suas credenciais do Azure.</span><span class="sxs-lookup"><span data-stu-id="54640-134">That command will open a prompt tooget your Azure credentials.</span></span> <span data-ttu-id="54640-135">Depois que você entrar, use um dos Olá assinatura de saudação tooselect de comandos que você deseja toouse a seguir.</span><span class="sxs-lookup"><span data-stu-id="54640-135">After you sign in, use either of hello following commands tooselect hello subscription that you want toouse.</span></span> <span data-ttu-id="54640-136">Certifique-se de que você está usando assinatura Olá que sua rede virtual e o plano de serviço de aplicativo estão em.</span><span class="sxs-lookup"><span data-stu-id="54640-136">Make sure that you are using hello subscription that your virtual network and App Service plan are in.</span></span>

    Select-AzureRmSubscription –SubscriptionName [WebAppSubscriptionName]

<span data-ttu-id="54640-137">ou o</span><span class="sxs-lookup"><span data-stu-id="54640-137">or</span></span>

    Select-AzureRmSubscription –SubscriptionId [WebAppSubscriptionId]

##### <a name="variables-used-in-this-article"></a><span data-ttu-id="54640-138">Variáveis usadas neste artigo</span><span class="sxs-lookup"><span data-stu-id="54640-138">Variables used in this article</span></span>
<span data-ttu-id="54640-139">comandos toosimplify, vamos definir uma **$Configuration** variável do PowerShell com a configuração específica de saudação.</span><span class="sxs-lookup"><span data-stu-id="54640-139">toosimplify commands, we will set a **$Configuration** PowerShell variable with hello specific configuration.</span></span>

<span data-ttu-id="54640-140">Defina uma variável como a seguir no PowerShell com hello parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="54640-140">Set a variable as follows in PowerShell with hello following parameters:</span></span>

    $Configuration = @{}
    $Configuration.WebAppResourceGroup = "[Your web app resource group]"
    $Configuration.WebAppName = "[Your web app name]"
    $Configuration.VnetSubscriptionId = "[Your vnet subscription id]"
    $Configuration.VnetResourceGroup = "[Your vnet resource group]"
    $Configuration.VnetName = "[Your vnet name]"

<span data-ttu-id="54640-141">local do aplicativo Hello deve ser local Olá sem espaços.</span><span class="sxs-lookup"><span data-stu-id="54640-141">hello app location should be hello location without any spaces.</span></span> <span data-ttu-id="54640-142">Por exemplo, Oeste dos EUA é westus.</span><span class="sxs-lookup"><span data-stu-id="54640-142">For example, West US is westus.</span></span>

    $Configuration.WebAppLocation = "[Your web app Location]"

<span data-ttu-id="54640-143">Olá próximo item é onde o certificado Olá deve ser gravado.</span><span class="sxs-lookup"><span data-stu-id="54640-143">hello next item is where hello certificate should be written.</span></span> <span data-ttu-id="54640-144">Deve ser um caminho gravável no computador local.</span><span class="sxs-lookup"><span data-stu-id="54640-144">It should be a writable path on your local computer.</span></span> <span data-ttu-id="54640-145">Verifique. cer de tooinclude-se no final de saudação.</span><span class="sxs-lookup"><span data-stu-id="54640-145">Make sure tooinclude .cer at hello end.</span></span>

    $Configuration.GeneratedCertificatePath = "[C:\Path\To\Certificate.cer]"

<span data-ttu-id="54640-146">toosee o que você defina tipo **$Configuration**.</span><span class="sxs-lookup"><span data-stu-id="54640-146">toosee what you set, type **$Configuration**.</span></span>

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

<span data-ttu-id="54640-147">restante Olá desta seção pressupõe que você tenha uma variável criada conforme descrito apenas.</span><span class="sxs-lookup"><span data-stu-id="54640-147">hello rest of this section assumes that you have a variable created as just described.</span></span>

##### <a name="declare-hello-virtual-network-toohello-app"></a><span data-ttu-id="54640-148">Declarar Olá rede virtual toohello aplicativo</span><span class="sxs-lookup"><span data-stu-id="54640-148">Declare hello virtual network toohello app</span></span>
<span data-ttu-id="54640-149">Use Olá seguindo comando tootell Olá aplicativo que ele usará essa rede virtual específico.</span><span class="sxs-lookup"><span data-stu-id="54640-149">Use hello following command tootell hello app that it will be using this particular virtual network.</span></span> <span data-ttu-id="54640-150">Isso causará Olá aplicativo toogenerate certificados necessários:</span><span class="sxs-lookup"><span data-stu-id="54640-150">This will cause hello app toogenerate necessary certificates:</span></span>

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -PropertyObject @{"VnetResourceId" = "/subscriptions/$($Configuration.VnetSubscriptionId)/resourceGroups/$($Configuration.VnetResourceGroup)/providers/Microsoft.ClassicNetwork/virtualNetworks/$($Configuration.VnetName)"} -Location $Configuration.WebAppLocation -ApiVersion 2015-07-01

<span data-ttu-id="54640-151">Se este comando for bem-sucedido, **$vnet** deverá conter uma variável **Properties**.</span><span class="sxs-lookup"><span data-stu-id="54640-151">If this command succeeds, **$vnet** should have a **Properties** variable in it.</span></span> <span data-ttu-id="54640-152">Olá **propriedades** variável deve conter um certificado impressão digital e hello certificado de dados.</span><span class="sxs-lookup"><span data-stu-id="54640-152">hello **Properties** variable should contain both a certificate thumbprint and hello certificate data.</span></span>

##### <a name="upload-hello-web-app-certificate-toohello-virtual-network"></a><span data-ttu-id="54640-153">Carregar Olá web aplicativo certificado toohello VPN</span><span class="sxs-lookup"><span data-stu-id="54640-153">Upload hello web app certificate toohello virtual network</span></span>
<span data-ttu-id="54640-154">Uma única etapa manual é necessária para cada combinação de assinatura e rede virtual.</span><span class="sxs-lookup"><span data-stu-id="54640-154">A manual, one-time step is required for each subscription and virtual network combination.</span></span> <span data-ttu-id="54640-155">Ou seja, se você estiver se conectando a aplicativos de assinatura A tooVirtual rede A, você precisará toodo esta etapa apenas uma vez, independentemente de quantos aplicativos você configurar.</span><span class="sxs-lookup"><span data-stu-id="54640-155">That is, if you are connecting apps in Subscription A tooVirtual Network A, you will need toodo this step only once regardless of how many apps you configure.</span></span> <span data-ttu-id="54640-156">Se você estiver adicionando uma nova rede virtual de tooanother de aplicativo, você precisará toodo novamente.</span><span class="sxs-lookup"><span data-stu-id="54640-156">If you are adding a new app tooanother virtual network, you'll need toodo this again.</span></span> <span data-ttu-id="54640-157">motivo de saudação para isso é que um conjunto de certificados é gerado em um nível de assinatura no serviço de aplicativo do Azure e conjunto de saudação é gerado uma vez para cada rede virtual que Olá aplicativos se conectam ao.</span><span class="sxs-lookup"><span data-stu-id="54640-157">hello reason for this is that a set of certificates is generated at a subscription level in Azure App Service, and hello set is generated once for each virtual network that hello apps will connect to.</span></span>

<span data-ttu-id="54640-158">Olá certificados serão já foram definidos se você seguir essas etapas ou se você está integrada com hello mesmo rede virtual usando o portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="54640-158">hello certificates will have already been set if you followed these steps or if you integrated with hello same virtual network by using hello portal.</span></span>

<span data-ttu-id="54640-159">Olá primeira etapa é o arquivo do toogenerate hello. cer.</span><span class="sxs-lookup"><span data-stu-id="54640-159">hello first step is toogenerate hello .cer file.</span></span> <span data-ttu-id="54640-160">Olá segunda etapa é tooupload hello. cer arquivo tooyour VPN.</span><span class="sxs-lookup"><span data-stu-id="54640-160">hello second step is tooupload hello .cer file tooyour virtual network.</span></span> <span data-ttu-id="54640-161">arquivo do toogenerate hello. cer de chamada de API de saudação nos Olá etapa anterior, execute Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="54640-161">toogenerate hello .cer file from hello API call in hello earlier step, run hello following commands.</span></span>

    $certBytes = [System.Convert]::FromBase64String($vnet.Properties.certBlob)
    [System.IO.File]::WriteAllBytes("$($Configuration.GeneratedCertificatePath)", $certBytes)

<span data-ttu-id="54640-162">certificado Olá será encontrado no local de saudação que **$Configuration.GeneratedCertificatePath** especifica.</span><span class="sxs-lookup"><span data-stu-id="54640-162">hello certificate will be found in hello location that **$Configuration.GeneratedCertificatePath** specifies.</span></span>

<span data-ttu-id="54640-163">certificado de saudação tooupload manualmente, use Olá [portal do Azure] [ azureportal] e **(clássico) de rede Virtual procurar** > **asconexõesVPN**  >  **Ponto a site** > **gerenciar certificados**.</span><span class="sxs-lookup"><span data-stu-id="54640-163">tooupload hello certificate manually, use hello [Azure portal][azureportal] and **Browse Virtual Network (classic)** > **VPN connections** > **Point-to-site** > **Manage certificates**.</span></span> <span data-ttu-id="54640-164">Nesse local, carregue seu certificado.</span><span class="sxs-lookup"><span data-stu-id="54640-164">From here, upload your certificate.</span></span>

##### <a name="get-hello-point-to-site-package"></a><span data-ttu-id="54640-165">Obter o pacote de ponto para site Olá</span><span class="sxs-lookup"><span data-stu-id="54640-165">Get hello point-to-site package</span></span>
<span data-ttu-id="54640-166">Olá próxima etapa na configuração de uma conexão de rede virtual em um aplicativo web é tooget Olá ponto a site pacote e fornecê-la tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="54640-166">hello next step in setting up a virtual network connection on a web app is tooget hello point-to-site package and provide it tooyour web app.</span></span>

<span data-ttu-id="54640-167">Salve Olá seguir chamado GetNetworkPackageUri.json em algum lugar no seu computador, por exemplo, C:\Azure\Templates\GetNetworkPackageUri.json o arquivo de modelo tooa.</span><span class="sxs-lookup"><span data-stu-id="54640-167">Save hello following template tooa file called GetNetworkPackageUri.json somewhere on your computer, for example, C:\Azure\Templates\GetNetworkPackageUri.json.</span></span>

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


<span data-ttu-id="54640-168">Defina os parâmetros de entrada:</span><span class="sxs-lookup"><span data-stu-id="54640-168">Set input parameters:</span></span>

    $parameters = @{"certData" = $vnet.Properties.certBlob ;
    certThumbprint = $vnet.Properties.certThumbprint ;
    "networkName" = $Configuration.VnetName }

<span data-ttu-id="54640-169">Chame o script hello:</span><span class="sxs-lookup"><span data-stu-id="54640-169">Call hello script:</span></span>

    $output = New-AzureRmResourceGroupDeployment -Name unused -ResourceGroupName $Configuration.VnetResourceGroup -TemplateParameterObject $parameters -TemplateFile C:\PATH\TO\GetNetworkPackageUri.json


<span data-ttu-id="54640-170">variável de saudação **$output. Outputs.packageUri** agora conterá Olá pacote URI toobe fornecido tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="54640-170">hello variable **$output.Outputs.packageUri** will now contain hello package URI toobe given tooyour web app.</span></span>

##### <a name="upload-hello-point-to-site-package-tooyour-app"></a><span data-ttu-id="54640-171">Carregar Olá pacote de ponto para site tooyour aplicativo</span><span class="sxs-lookup"><span data-stu-id="54640-171">Upload hello point-to-site package tooyour app</span></span>
<span data-ttu-id="54640-172">Olá última etapa é tooprovide Olá aplicativo com este pacote.</span><span class="sxs-lookup"><span data-stu-id="54640-172">hello final step is tooprovide hello app with this package.</span></span> <span data-ttu-id="54640-173">Basta executar o próximo comando de saudação:</span><span class="sxs-lookup"><span data-stu-id="54640-173">Simply run hello next command:</span></span>

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)/primary" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-07-01 -PropertyObject @{"VnetName" = $Configuration.VnetName ; "VpnPackageUri" = $($output.Outputs.packageUri).Value } -Location $Configuration.WebAppLocation

<span data-ttu-id="54640-174">Se uma mensagem solicitará que você tooconfirm que você está substituindo um recurso existente, verifique se tooallow-lo.</span><span class="sxs-lookup"><span data-stu-id="54640-174">If a message asks you tooconfirm that you are overwriting an existing resource, make sure tooallow it.</span></span>

<span data-ttu-id="54640-175">Depois que esse comando for bem-sucedida, seu aplicativo agora deve ser a rede virtual conectado toohello.</span><span class="sxs-lookup"><span data-stu-id="54640-175">After this command succeeds, your app should now be connected toohello virtual network.</span></span> <span data-ttu-id="54640-176">tooconfirm êxito, acesse o console do aplicativo tooyour e digite Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="54640-176">tooconfirm success, go tooyour app console, and type hello following:</span></span>

    SET WEBSITE_

<span data-ttu-id="54640-177">Se houver uma variável de ambiente chamada WEBSITE_VNETNAME que tem um valor que corresponda ao nome hello da rede virtual de destino de saudação, todas as configurações tiveram êxito.</span><span class="sxs-lookup"><span data-stu-id="54640-177">If there is an environment variable called WEBSITE_VNETNAME that has a value that matches hello name of hello target virtual network, all configurations have succeeded.</span></span>

### <a name="update-classic-vnet-integration-information"></a><span data-ttu-id="54640-178">Atualizar informações de integração VNet clássica</span><span class="sxs-lookup"><span data-stu-id="54640-178">Update classic VNet integration information</span></span>
<span data-ttu-id="54640-179">tooupdate ou ressincronizar as informações, simplesmente Repita as etapas de saudação que você seguiu quando você criou a integração de saudação em primeiro lugar de saudação.</span><span class="sxs-lookup"><span data-stu-id="54640-179">tooupdate or resync your information, simply repeat hello steps that you followed when you created hello integration in hello first place.</span></span> <span data-ttu-id="54640-180">Essas etapas são:</span><span class="sxs-lookup"><span data-stu-id="54640-180">Those steps are:</span></span>

1. <span data-ttu-id="54640-181">Defina as informações de configuração.</span><span class="sxs-lookup"><span data-stu-id="54640-181">Define your configuration information.</span></span>
2. <span data-ttu-id="54640-182">Declare Olá rede virtual toohello aplicativo.</span><span class="sxs-lookup"><span data-stu-id="54640-182">Declare hello virtual network toohello app.</span></span>
3. <span data-ttu-id="54640-183">Obter pacote de ponto para site hello.</span><span class="sxs-lookup"><span data-stu-id="54640-183">Get hello point-to-site package.</span></span>
4. <span data-ttu-id="54640-184">Carregar Olá pacote de ponto para site tooyour aplicativo.</span><span class="sxs-lookup"><span data-stu-id="54640-184">Upload hello point-to-site package tooyour app.</span></span>

### <a name="disconnect-your-app-from-a-classic-vnet"></a><span data-ttu-id="54640-185">Desconectar o aplicativo de uma VNet clássica</span><span class="sxs-lookup"><span data-stu-id="54640-185">Disconnect your app from a classic VNet</span></span>
<span data-ttu-id="54640-186">toodisconnect Olá aplicativo, você precisar de informações de configuração de Olá que foi definidas durante a integração da rede virtual.</span><span class="sxs-lookup"><span data-stu-id="54640-186">toodisconnect hello app, you need hello configuration information that was set during virtual network integration.</span></span> <span data-ttu-id="54640-187">Usando essas informações, não há toodisconnect de comando, em seguida, um aplicativo de sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="54640-187">Using that information, there is then one command toodisconnect your app from your virtual network.</span></span>

    $vnet = Remove-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-07-01

## <a name="resource-manager-virtual-networks"></a><span data-ttu-id="54640-188">Redes virtuais do Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="54640-188">Resource Manager virtual networks</span></span>
<span data-ttu-id="54640-189">As redes virtuais do Resource Manager têm APIs do Azure Resource Manager que simplificam alguns processos se comparadas com redes virtuais clássicas.</span><span class="sxs-lookup"><span data-stu-id="54640-189">Resource Manager virtual networks have Azure Resource Manager APIs, which simplify some processes when compared with classic virtual networks.</span></span> <span data-ttu-id="54640-190">Temos um script que ajudarão você a concluir Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="54640-190">We have a script that will help you complete hello following tasks:</span></span>

* <span data-ttu-id="54640-191">Criar uma rede virtual do Gerenciador de Recursos e integrar o aplicativo a ela.</span><span class="sxs-lookup"><span data-stu-id="54640-191">Create a Resource Manager virtual network and integrate your app with it.</span></span>
* <span data-ttu-id="54640-192">Criar um gateway, configurar a conectividade ponto a site em uma rede virtual do Gerenciador de Recursos pré-existente e integrar o aplicativo a ela.</span><span class="sxs-lookup"><span data-stu-id="54640-192">Create a gateway, configure point-to-site connectivity in a preexisting Resource Manager virtual network, and then integrate your app with it.</span></span>
* <span data-ttu-id="54640-193">Integrar o aplicativo a uma rede virtual do Gerenciador de Recursos pré-existente que tem um gateway e habilitar a conectividade ponto a site.</span><span class="sxs-lookup"><span data-stu-id="54640-193">Integrate your app with a preexisting Resource Manager virtual network that has a gateway and point-to-site connectivity enabled.</span></span>
* <span data-ttu-id="54640-194">Desconecte o aplicativo da rede virtual.</span><span class="sxs-lookup"><span data-stu-id="54640-194">Disconnect your app from your virtual network.</span></span>

### <a name="resource-manager-vnet-app-service-integration-script"></a><span data-ttu-id="54640-195">Script de integração do Serviço de Aplicativo de VNet do Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="54640-195">Resource Manager VNet App Service integration script</span></span>
<span data-ttu-id="54640-196">Copie Olá seguinte script e salve-o arquivo tooa.</span><span class="sxs-lookup"><span data-stu-id="54640-196">Copy hello following script and save it tooa file.</span></span> <span data-ttu-id="54640-197">Se você não quiser o script de saudação toouse, sinta-se livre toolearn dele toosee como tooset as coisas com uma rede virtual do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="54640-197">If you don’t want toouse hello script, feel free toolearn from it toosee how tooset things up with a Resource Manager virtual network.</span></span>

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

        Write-Host "Adding a root certificate toothis VNET"
        $root = New-AzureRmVpnClientRootCertificate -Name "AppServiceCertificate.cer" -PublicCertData $certificateData

        Write-Host "Creating Azure VNET Gateway. This may take up tooan hour."
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
            Write-Host "Currently, I will create a VNET with hello following settings:"
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
            $changeRequested = PromptYesNo "" "Do you wish toochange these settings?" 1

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

        # We create hello virtual network and add it here. hello way this works is:
        # 1) Add hello VNET association toohello App. This allows hello App toogenerate certificates, etc. for hello VNET.
        # 2) Create hello VNET and VNET gateway, add hello certificates, create hello public IP, etc., required for hello gateway
        # 3) Get hello VPN package from hello gateway and pass it back toohello App.

        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup
        $location = $webApp.Location

        Write-Host "Creating App association tooVNET"
        $propertiesObject = @{
         "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($resourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
        }
        $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        CreateVnet $resourceGroupName $vnetName $vnetAddressSpace $vnetGatewayAddressSpace $location

        CreateVnetGateway $resourceGroupName $vnetName $vnetIpName $location $vnetIpConfigName $vnetGatewayName $virtualNetwork.Properties.CertBlob $vnetPointToSiteAddressSpace

        Write-Host "Retrieving VPN Package and supplying tooApp"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $resourceGroupName -VirtualNetworkGatewayName $vnetGatewayName -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at hello start and hello end of hello URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put hello VPN client configuration package onto hello App
        $PropertiesObject = @{
        "vnetName" = $VirtualNetworkName; "vpnPackageUri" = $packageUri
        }

        New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnetName)/primary" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-08-01 -ResourceGroupName $webAppResourceGroup -Force

        Write-Host "Finished!"
    }

    function AddExistingVnet($subscriptionId, $resourceGroupName, $webAppName)
    {
        $ErrorActionPreference = "Stop";

        # At this point, hello gateway should be able toobe joined tooan App, but may require some minor tweaking. We will declare toohello App now toouse this VNET
        Write-Host "Getting App information"
        $webApp = Get-AzureRmResource -ResourceName $webAppName -ResourceType "Microsoft.Web/sites" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $location = $webApp.Location

        $webAppConfig = Get-AzureRmResource -ResourceName "$($webAppName)/web" -ResourceType "Microsoft.Web/sites/config" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        $currentVnet = $webAppConfig.Properties.VnetName
        if($currentVnet -ne $null -and $currentVnet -ne "")
        {
            Write-Host "Currently connected tooVNET $currentVnet"
        }

        # Display existing vnets
        $vnets = Get-AzureRmVirtualNetwork
        $vnetNames = @()
        foreach($vnet in $vnets)
        {
            $vnetNames += $vnet.Name
        }

        Write-Host
        $vnet = PromptCustom "Select a VNET toointegrate with" $vnets $vnetNames

        # We need toocheck if this VNET is able toobe joined tooa App, based on following criteria
            # If there is no gateway, we can create one.
            # If there is a gateway:
                # It must be of type Vpn
                # It must be of VpnType RouteBased
                # If it doesn't have hello right certificate, we will need tooadd it.
                # If it doesn't have a point-to-site range, we will need tooadd it.

        $gatewaySubnet = $vnet.Subnets | Where-Object { $_.Name -eq "GatewaySubnet" }

        if($gatewaySubnet -eq $null -or $gatewaySubnet.IpConfigurations -eq $null -or $gatewaySubnet.IpConfigurations.Count -eq 0)
        {
            $ErrorActionPreference = "Continue";
            # There is no gateway. We need toocreate one.
            Write-Host "This Virtual Network has no gateway. I will need toocreate one."

            $vnetName = $vnet.Name
            $vnetGatewayName="$($vnetName)-gateway"
            $vnetIpName="$($vnetName)-ip"
            $vnetIpConfigName="$($vnetName)-ipconf"

            # Virtual Network settings
            $vnetAddressSpace="10.0.0.0/8"
            $vnetGatewayAddressSpace="10.5.0.0/16"
            $vnetPointToSiteAddressSpace="172.16.0.0/16"

            $changeRequested = 0

            Write-Host "Your VNET is in hello address space $($vnet.AddressSpace.AddressPrefixes), with hello following Subnets:"
            foreach($subnet in $vnet.Subnets)
            {
                Write-Host "$($subnet.Name): $($subnet.AddressPrefix)"
            }

            $vnetGatewayAddressSpace = Read-Host "Please choose a GatewaySubnet address space"

            while($changeRequested -eq 0)
            {
                Write-Host
                Write-Host "Currently, I will create a VNET gateway with hello following settings:"
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
                $changeRequested = PromptYesNo "" "Do you wish toochange these settings?" 1

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

            Write-Host "Creating App association tooVNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnetName)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # If there is no gateway subnet, we need toocreate one.
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
                Write-Error "This gateway is not of hello Vpn type. It cannot be joined tooan App."
                return
            }

            if($gateway.VpnType -ne "RouteBased")
            {
                Write-Error "This gateways Vpn type is not RouteBased. It cannot be joined tooan App."
                return
            }

            if($gateway.VpnClientConfiguration -eq $null -or $gateway.VpnClientConfiguration.VpnClientAddressPool -eq $null)
            {
                Write-Host "This gateway does not have a Point-to-site Address Range. Please specify one in CIDR notation, e.g. 10.0.0.0/8"
                $pointToSiteAddress = Read-Host "Point-To-Site Address Space"
                Set-AzureRmVirtualNetworkGatewayVpnClientConfig -VirtualNetworkGateway $gateway.Name -VpnClientAddressPool $pointToSiteAddress
            }

            Write-Host "Creating App association tooVNET"
            $propertiesObject = @{
             "vnetResourceId" = "/subscriptions/$($subscriptionId)/resourceGroups/$($vnet.ResourceGroupName)/providers/Microsoft.Network/virtualNetworks/$($vnet.Name)"
            }

            $virtualNetwork = New-AzureRmResource -Location $location -Properties $PropertiesObject -ResourceName "$($webAppName)/$($vnet.Name)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName -Force

            # We need toocheck if hello certificate here exists in hello gateway.
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

        # Now finish joining by getting hello VPN package and giving it toohello App
        Write-Host "Retrieving VPN Package and supplying tooApp"
        $packageUri = Get-AzureRmVpnClientPackage -ResourceGroupName $vnet.ResourceGroupName -VirtualNetworkGatewayName $gateway.Name -ProcessorArchitecture Amd64
        
        # $packageUri may contain literal double-quotes at hello start and hello end of hello URL
        if($packageUri.Length -gt 0 -and $packageUri.Substring(0, 1) -eq '"' -and $packageUri.Substring($packageUri.Length - 1, 1) -eq '"')
        {
            $packageUri = $packageUri.Substring(1, $packageUri.Length - 2)
        }

        # Put hello VPN client configuration package onto hello App
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
            Write-Host "Currently connected tooVNET $currentVnet"

            Remove-AzureRmResource -ResourceName "$($webAppName)/$($currentVnet)" -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-08-01 -ResourceGroupName $resourceGroupName
        }
            else
        {
            Write-Host "Not connected tooa VNET."
        }
    }

    Write-Host "Please Login"
    Login-AzureRmAccount

    # Choose subscription. If there's only one we will choose automatically

    $subs = Get-AzureRmSubscription
    $subscriptionId = ""

    if($subs.Length -eq 0)
    {
        Write-Error "No subscriptions bound toothis account."
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

    $resourceGroup = Read-Host "Please enter hello Resource Group of your App"

    $appName = Read-Host "Please enter hello Name of your App"

    $options = @("Add a NEW Virtual Network tooan App", "Add an EXISTING Virtual Network tooan App", "Remove a Virtual Network from an App");
    $optionValues = @(0, 1, 2)
    $option = PromptCustom "What do you want toodo?" $optionValues $options

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

<span data-ttu-id="54640-198">Salve uma cópia do script hello.</span><span class="sxs-lookup"><span data-stu-id="54640-198">Save a copy of hello script.</span></span> <span data-ttu-id="54640-199">Neste artigo, ele é chamado de V2VnetAllinOne.ps1, mas você pode usar outro nome.</span><span class="sxs-lookup"><span data-stu-id="54640-199">In this article, it is called V2VnetAllinOne.ps1, but you can use another name.</span></span> <span data-ttu-id="54640-200">Não há nenhum argumento para esse script.</span><span class="sxs-lookup"><span data-stu-id="54640-200">There are no arguments for this script.</span></span> <span data-ttu-id="54640-201">Basta executá-lo.</span><span class="sxs-lookup"><span data-stu-id="54640-201">You simply run it.</span></span> <span data-ttu-id="54640-202">Olá primeiro script hello fará é solicitar que você toosign no.</span><span class="sxs-lookup"><span data-stu-id="54640-202">hello first thing hello script will do is prompt you toosign in.</span></span> <span data-ttu-id="54640-203">Depois que você entrar, o script hello obtém os detalhes sobre sua conta e retorna uma lista de assinaturas.</span><span class="sxs-lookup"><span data-stu-id="54640-203">After you sign in, hello script gets details about your account and returns a list of subscriptions.</span></span> <span data-ttu-id="54640-204">Contagem não solicitação Olá suas credenciais, execução de script inicial Olá terá esta aparência:</span><span class="sxs-lookup"><span data-stu-id="54640-204">Not counting hello request for your credentials, hello initial script execution looks like this:</span></span>

    PS C:\Users\ccompy\Documents\VNET> .\V2VnetAllInOne.ps1
    Please Login

    Environment           : AzureCloud
    Account               : ccompy@microsoft.com
    TenantId              : 722278f-fef1-499f-91ab-2323d011db47
    SubscriptionId        : af5358e1-acac-2c90-a9eb-722190abf47a
    CurrentStorageAccount :

    Choose a subscription

    1) <span data-ttu-id="54640-205">Assinatura de demonstração (af5358e1-acac-2c90-a9eb-722190abf47a)</span><span class="sxs-lookup"><span data-stu-id="54640-205">Demo Subscription (af5358e1-acac-2c90-a9eb-722190abf47a)</span></span>
    2) <span data-ttu-id="54640-206">Teste MS (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)</span><span class="sxs-lookup"><span data-stu-id="54640-206">MS Test (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)</span></span>
    3) <span data-ttu-id="54640-207">Assinatura de demonstração Purple (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)</span><span class="sxs-lookup"><span data-stu-id="54640-207">Purple Demo Subscription (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)</span></span>

    <span data-ttu-id="54640-208">Escolher uma opção: 3</span><span class="sxs-lookup"><span data-stu-id="54640-208">Choose an option: 3</span></span>

    <span data-ttu-id="54640-209">Conta      : ccompy@microsoft.com Ambiente  : Assinatura da Nuvem do Azure: 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Locatário       : 722278f-fef1-499f-91ab-2323d011db47</span><span class="sxs-lookup"><span data-stu-id="54640-209">Account      : ccompy@microsoft.com Environment  : AzureCloud Subscription : 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Tenant       : 722278f-fef1-499f-91ab-2323d011db47</span></span>

    <span data-ttu-id="54640-210">Digite hello grupo de recursos do seu aplicativo: hcdemo rg digite Olá nome do seu aplicativo: v2vnetpowershell o que fazer você deseja toodo?</span><span class="sxs-lookup"><span data-stu-id="54640-210">Please enter hello Resource Group of your App: hcdemo-rg Please enter hello Name of your App: v2vnetpowershell What do you want toodo?</span></span>

    1) <span data-ttu-id="54640-211">Adicionar uma nova rede Virtual de tooan aplicativo</span><span class="sxs-lookup"><span data-stu-id="54640-211">Add a NEW Virtual Network tooan App</span></span>
    2) <span data-ttu-id="54640-212">Adicionar um aplicativo de tooan de rede Virtual existente</span><span class="sxs-lookup"><span data-stu-id="54640-212">Add an EXISTING Virtual Network tooan App</span></span>
    3) <span data-ttu-id="54640-213">Remover uma rede Virtual de um aplicativo</span><span class="sxs-lookup"><span data-stu-id="54640-213">Remove a Virtual Network from an App</span></span>

<span data-ttu-id="54640-214">restante Olá desta seção explica cada uma dessas três opções.</span><span class="sxs-lookup"><span data-stu-id="54640-214">hello rest of this section explains each of those three options.</span></span>

### <a name="create-a-resource-manager-vnet-and-integrate-with-it"></a><span data-ttu-id="54640-215">Criar uma VNet do Gerenciador de Recursos e realizar a integração a ela</span><span class="sxs-lookup"><span data-stu-id="54640-215">Create a Resource Manager VNet and integrate with it</span></span>
<span data-ttu-id="54640-216">Selecione de uma nova rede virtual que usa Olá modelo de implantação do Gerenciador de recursos e integrá-lo com seu aplicativo, toocreate **1) adicionar uma nova rede Virtual de tooan aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="54640-216">toocreate a new virtual network that uses hello Resource Manager deployment model and integrate it with your app, select **1) Add a NEW Virtual Network tooan App**.</span></span> <span data-ttu-id="54640-217">Isso solicitará nome hello da rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="54640-217">This will prompt you for hello name of hello virtual network.</span></span> <span data-ttu-id="54640-218">No meu caso, como você pode ver no hello configurações, a seguir, usei nome hello, v2pshell.</span><span class="sxs-lookup"><span data-stu-id="54640-218">In my case, as you can see in hello following settings, I used hello name, v2pshell.</span></span>

<span data-ttu-id="54640-219">script Hello fornece detalhes de saudação sobre a rede virtual de saudação que está sendo criado.</span><span class="sxs-lookup"><span data-stu-id="54640-219">hello script gives hello details about hello virtual network that's being created.</span></span> <span data-ttu-id="54640-220">Se desejar, eu pode alterar qualquer um dos valores de saudação.</span><span class="sxs-lookup"><span data-stu-id="54640-220">If I want, I can change any of hello values.</span></span> <span data-ttu-id="54640-221">Em execução neste exemplo, criei uma rede virtual que tenha Olá configurações a seguir:</span><span class="sxs-lookup"><span data-stu-id="54640-221">In this example execution, I created a virtual network that has hello following settings:</span></span>

    Virtual Network Name:         v2pshell
    Resource Group Name:          hcdemo-rg
    Gateway Name:                 v2pshell-gateway
    Vnet IP name:                 v2pshell-ip
    Vnet IP config name:          v2pshell-ipconf
    Address Space:                10.0.0.0/8
    Gateway Address Space:        10.5.0.0/16
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish toochange these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):

<span data-ttu-id="54640-222">Se você quiser toochange qualquer um dos valores hello, digite **Y** e fazer alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="54640-222">If you want toochange any of hello values, type **Y** and make hello changes.</span></span> <span data-ttu-id="54640-223">Quando estiver satisfeito com as configurações de rede virtual hello, digite **N** ou pressione Enter quando solicitado sobre como alterar configurações de saudação.</span><span class="sxs-lookup"><span data-stu-id="54640-223">When you are happy with hello virtual network settings, type **N** or simply press Enter when prompted about changing hello settings.</span></span> <span data-ttu-id="54640-224">A partir daí até a conclusão, script hello dirá alguns que ' i ' s fazer até que se inicie o gateway de rede virtual toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="54640-224">From there on until completion, hello script will tell you some of what it' i's doing until it starts toocreate hello virtual network gateway.</span></span> <span data-ttu-id="54640-225">Essa etapa pode levar horas tooan.</span><span class="sxs-lookup"><span data-stu-id="54640-225">That step can take up tooan hour.</span></span> <span data-ttu-id="54640-226">Não há nenhum indicador de progresso durante essa fase, mas o script hello informará quando Olá gateway foi criado.</span><span class="sxs-lookup"><span data-stu-id="54640-226">There is no progress indicator during this phase, but hello script will let you know when hello gateway has been created.</span></span>

<span data-ttu-id="54640-227">Quando o script hello termina, ele indicará que **concluído**.</span><span class="sxs-lookup"><span data-stu-id="54640-227">When hello script finishes, it will say **Finished**.</span></span> <span data-ttu-id="54640-228">Neste ponto, você terá uma rede virtual do Gerenciador de recursos que tem nome hello e configurações que você selecionou.</span><span class="sxs-lookup"><span data-stu-id="54640-228">At this point, you will have a Resource Manager virtual network that has hello name and settings that you selected.</span></span> <span data-ttu-id="54640-229">Essa nova rede virtual também será integrada ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="54640-229">This new virtual network will also be integrated with your app.</span></span>

### <a name="integrate-your-app-with-a-preexisting-resource-manager-vnet"></a><span data-ttu-id="54640-230">Integrar seu aplicativo a uma VNet pré-existente do Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="54640-230">Integrate your app with a preexisting Resource Manager VNet</span></span>
<span data-ttu-id="54640-231">Quando você estiver integrando uma rede virtual preexistente, se você fornecer uma rede virtual do Gerenciador de recursos que não tem um gateway ou a conectividade ponto a site, script hello configurará que.</span><span class="sxs-lookup"><span data-stu-id="54640-231">When you're integrating with a preexisting virtual network, if you provide a Resource Manager virtual network that doesn’t have a gateway or point-to-site connectivity, hello script will set that up.</span></span> <span data-ttu-id="54640-232">Se Olá VNET já tiver essas coisas configuradas, script hello vai toohello alinhada a integração de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="54640-232">If hello VNET already has those things set up, hello script goes straight toohello app integration.</span></span> <span data-ttu-id="54640-233">toostart esse processo, basta selecionar **2) adicione uma rede Virtual existente de tooan aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="54640-233">toostart this process, simply select **2) Add an EXISTING Virtual Network tooan App**.</span></span>

<span data-ttu-id="54640-234">Essa opção funciona somente se você tiver uma rede virtual preexistente Gerenciador de recursos que está em Olá mesma assinatura que seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="54640-234">This option works only if you have a preexisting Resource Manager virtual network that is in hello same subscription as your app.</span></span> <span data-ttu-id="54640-235">Depois de selecionar a opção hello, você verá uma lista de suas redes virtuais do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="54640-235">After you select hello option, you will be presented with a list of your Resource Manager virtual networks.</span></span>   

    Select a VNET toointegrate with

    1) <span data-ttu-id="54640-236">v2demonetwork</span><span class="sxs-lookup"><span data-stu-id="54640-236">v2demonetwork</span></span>
    2) <span data-ttu-id="54640-237">v2pshell</span><span class="sxs-lookup"><span data-stu-id="54640-237">v2pshell</span></span>
    3) <span data-ttu-id="54640-238">v2vnetintdemo</span><span class="sxs-lookup"><span data-stu-id="54640-238">v2vnetintdemo</span></span>
    4) <span data-ttu-id="54640-239">v2asenetwork</span><span class="sxs-lookup"><span data-stu-id="54640-239">v2asenetwork</span></span>
    5) <span data-ttu-id="54640-240">v2pshell2</span><span class="sxs-lookup"><span data-stu-id="54640-240">v2pshell2</span></span>

    <span data-ttu-id="54640-241">Escolher uma opção: 5</span><span class="sxs-lookup"><span data-stu-id="54640-241">Choose an option: 5</span></span>

<span data-ttu-id="54640-242">Basta selecione a rede virtual de saudação que você deseja toointegrate com.</span><span class="sxs-lookup"><span data-stu-id="54640-242">Simply select hello virtual network that you want toointegrate with.</span></span> <span data-ttu-id="54640-243">Se você já tiver um gateway que tenha conectividade de ponto para site habilitada, o script hello simplesmente integrará seu aplicativo com sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="54640-243">If you already have a gateway that has point-to-site connectivity enabled, hello script will simply integrate your app with your virtual network.</span></span> <span data-ttu-id="54640-244">Se você não tiver um gateway, você precisará toospecify Olá gateway de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="54640-244">If you do not have a gateway, you will need toospecify hello gateway subnet.</span></span> <span data-ttu-id="54640-245">A sub-rede do gateway deve estar em seu espaço de endereço de Rede Virtual e não pode estar em outra sub-rede.</span><span class="sxs-lookup"><span data-stu-id="54640-245">Your gateway subnet must be in your virtual network address space, and it cannot be in any other subnet.</span></span> <span data-ttu-id="54640-246">se você tiver uma rede virtual sem um gateway e executar essa etapa, verá o seguinte:</span><span class="sxs-lookup"><span data-stu-id="54640-246">If you have a virtual network without a gateway and run this step, things look like this:</span></span>

    This Virtual Network has no gateway. I will need toocreate one.
    Your VNET is in hello address space 172.16.0.0/16, with hello following Subnets:
    default: 172.16.0.0/24
    Please choose a GatewaySubnet address space: 172.16.1.0/26

<span data-ttu-id="54640-247">Neste exemplo, criei um gateway de rede virtual que tenha Olá configurações a seguir:</span><span class="sxs-lookup"><span data-stu-id="54640-247">In this example, I created a virtual network gateway that has hello following settings:</span></span>

    Virtual Network Name:         v2pshell2
    Resource Group Name:          vnetdemo-rg
    Gateway Name:                 v2pshell2-gateway
    Vnet IP name:                 v2pshell2-ip
    Vnet IP config name:          v2pshell2-ipconf
    Address Space:                172.16.0.0/16
    Gateway Address Space:        172.16.1.0/26
    Point-To-Site Address Space:  172.16.0.0/12

    Do you wish toochange these settings?
    [Y] Yes  [N] No  [?] Help (default is "N"):
    Creating App association tooVNET

<span data-ttu-id="54640-248">Se você quiser toochange qualquer uma dessas configurações, você pode fazer isso.</span><span class="sxs-lookup"><span data-stu-id="54640-248">If you want toochange any of those settings, you can do so.</span></span> <span data-ttu-id="54640-249">Caso contrário, pressione Enter e o script hello criará seu gateway e anexar a sua rede virtual do aplicativo tooyour.</span><span class="sxs-lookup"><span data-stu-id="54640-249">Otherwise, press Enter and hello script will create your gateway and attach your app tooyour virtual network.</span></span> <span data-ttu-id="54640-250">a hora de criação de gateway Olá ainda é uma hora, no entanto, portanto certifique-se de que que você tenha em mente.</span><span class="sxs-lookup"><span data-stu-id="54640-250">hello gateway creation time is still an hour, though, so make sure you keep that in mind.</span></span> <span data-ttu-id="54640-251">Quando tudo estiver concluído, o script hello dirá **concluído**.</span><span class="sxs-lookup"><span data-stu-id="54640-251">When everything is finished, hello script will say **Finished**.</span></span>

### <a name="disconnect-your-app-from-a-resource-manager-vnet"></a><span data-ttu-id="54640-252">Desconectar o aplicativo de uma VNet do Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="54640-252">Disconnect your app from a Resource Manager VNet</span></span>
<span data-ttu-id="54640-253">Desconectar-se seu aplicativo de sua rede virtual não derrubar o gateway de saudação ou desabilitar a conectividade ponto a site.</span><span class="sxs-lookup"><span data-stu-id="54640-253">Disconnecting your app from your virtual network does not take down hello gateway or disable point-to-site connectivity.</span></span> <span data-ttu-id="54640-254">Afinal de contas, você poderia usá-los para alguma outra coisa.</span><span class="sxs-lookup"><span data-stu-id="54640-254">You might, after all, be using it for something else.</span></span> <span data-ttu-id="54640-255">Ele também não desconectá-lo de todos os outros aplicativos que não sejam Olá fornecido por você.</span><span class="sxs-lookup"><span data-stu-id="54640-255">It also does not disconnect it from any other apps other than hello one you provided.</span></span> <span data-ttu-id="54640-256">tooperform esta ação, selecione **3) remover uma rede Virtual de um aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="54640-256">tooperform this action, select **3) Remove a Virtual Network from an App**.</span></span> <span data-ttu-id="54640-257">Quando você fizer isso, verá algo assim:</span><span class="sxs-lookup"><span data-stu-id="54640-257">When you do so, you will see something like this:</span></span>

    Currently connected tooVNET v2pshell

    Confirm
    Are you sure you want toodelete hello following resource:
    /subscriptions/edcc99a4-b7f9-4b5e-a9a1-3034c51db496/resourceGroups/hcdemo-rg/providers/Microsoft.Web/sites/v2vnetpowers
    hell/virtualNetworkConnections/v2pshell
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):

<span data-ttu-id="54640-258">Embora o script hello diz que a exclusão, não exclui rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="54640-258">Although hello script says delete, it does not delete hello virtual network.</span></span> <span data-ttu-id="54640-259">Ele é apenas Removendo integração hello.</span><span class="sxs-lookup"><span data-stu-id="54640-259">It’s just removing hello integration.</span></span> <span data-ttu-id="54640-260">Depois de confirmar que esse é o que você deseja toodo, o comando Olá é processado muito rapidamente e informa **True** quando é feito.</span><span class="sxs-lookup"><span data-stu-id="54640-260">After you confirm that this is what you want toodo, hello command is processed quite quickly and tells you **True** when it is done.</span></span>

<!--Links-->
[createvpngateway]: http://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/
[azureportal]: http://portal.azure.com
