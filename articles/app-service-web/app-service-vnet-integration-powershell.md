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
# <a name="connect-your-app-tooyour-virtual-network-by-using-powershell"></a>Conecte-se a sua rede virtual do aplicativo tooyour usando o PowerShell
## <a name="overview"></a>Visão geral
No serviço de aplicativo do Azure, você pode se conectar a seu aplicativo (web, móveis ou a API) tooan rede virtual do Azure (VNet) em sua assinatura. Esse recurso é chamado de Integração VNet. recurso de integração da VNet Olá não deve ser confundido com o recurso de ambiente de serviço de aplicativo hello, que permite que você toorun uma instância do serviço de aplicativo do Azure em sua rede virtual.

recurso de integração da VNet Olá tem uma interface de usuário (UI) no novo portal de saudação que você pode usar toointegrate com redes virtuais que são implantadas usando o modelo de implantação clássico hello ou modelo de implantação do Azure Resource Manager hello. Se você quiser toolearn mais sobre o recurso de hello, consulte [integrar seu aplicativo com uma rede virtual Azure](web-sites-integrate-with-vnet.md).

Este artigo é não sobre como toouse Olá da interface do usuário, mas em vez disso, sobre como tooenable integração usando o PowerShell. Como comandos Olá para cada modelo de implantação são diferentes, este artigo possui uma seção para cada modelo de implantação.  

Antes de continuar a ler este artigo, verifique se você tem:

* saudação do que SDK do Azure PowerShell mais recente instalado. Você pode instalá-lo com Olá Web Platform Installer.
* Um aplicativo no Serviço de Aplicativo do Azure em execução em uma SKU Standard ou Premium.

## <a name="classic-virtual-networks"></a>Redes virtuais clássicas
Esta seção explica três tarefas para redes virtuais que usam o modelo de implantação clássico hello:

1. Conecte seu aplicativo tooa preexistentes rede virtual que tem um gateway e é configurado para conectividade ponto a site.
2. Atualize as informações de integração de rede virtual para seu aplicativo.
3. Desconecte o aplicativo da rede virtual.

### <a name="connect-an-app-tooa-classic-vnet"></a>Conecte-se um aplicativo tooa VNet clássico
tooconnect uma rede virtual do tooa de aplicativo, siga estas três etapas:

1. Declare o aplicativo da web de toohello que ele for ingressar em uma rede virtual específico. aplicativo Hello irá gerar um certificado que será dada rede virtual toohello para conectividade ponto a site.
2. Carregar Olá web aplicativo certificado toohello VPN e, em seguida, recuperar o URI de pacote VPN de ponto para site do hello.
3. Atualize conexão de rede virtual do aplicativo da web de saudação com URI de pacote de ponto para site hello.

Hello primeira e terceira etapas são totalmente programável por scripts, mas a segunda etapa de saudação exige uma única ação manual por meio do portal hello, ou acesso tooperform **colocar** ou **PATCH** ações na rede virtual Olá Ponto de extremidade do Gerenciador de recursos do Azure. Entre em contato com suporte do Azure toohave isso habilitado. Antes de começar, verifique se você tem uma rede virtual clássica que tenha a conectividade ponto a site já habilitada e um gateway implantado. toocreate Olá gateway e habilitar ponto a site conectividade, você precisa toouse portal de saudação conforme descrito em [criar um gateway VPN][createvpngateway].

rede virtual clássica Hello precisa toobe Olá a mesma assinatura que o serviço de aplicativo planejar que mantém o aplicativo hello que você estiver integrando.

##### <a name="set-up-azure-powershell-sdk"></a>Configurar o SDK do Azure PowerShell
Abra uma janela do PowerShell e configure sua conta e assinatura do Azure usando:

    Login-AzureRmAccount

Esse comando abrirá um prompt tooget suas credenciais do Azure. Depois que você entrar, use um dos Olá assinatura de saudação tooselect de comandos que você deseja toouse a seguir. Certifique-se de que você está usando assinatura Olá que sua rede virtual e o plano de serviço de aplicativo estão em.

    Select-AzureRmSubscription –SubscriptionName [WebAppSubscriptionName]

ou o

    Select-AzureRmSubscription –SubscriptionId [WebAppSubscriptionId]

##### <a name="variables-used-in-this-article"></a>Variáveis usadas neste artigo
comandos toosimplify, vamos definir uma **$Configuration** variável do PowerShell com a configuração específica de saudação.

Defina uma variável como a seguir no PowerShell com hello parâmetros a seguir:

    $Configuration = @{}
    $Configuration.WebAppResourceGroup = "[Your web app resource group]"
    $Configuration.WebAppName = "[Your web app name]"
    $Configuration.VnetSubscriptionId = "[Your vnet subscription id]"
    $Configuration.VnetResourceGroup = "[Your vnet resource group]"
    $Configuration.VnetName = "[Your vnet name]"

local do aplicativo Hello deve ser local Olá sem espaços. Por exemplo, Oeste dos EUA é westus.

    $Configuration.WebAppLocation = "[Your web app Location]"

Olá próximo item é onde o certificado Olá deve ser gravado. Deve ser um caminho gravável no computador local. Verifique. cer de tooinclude-se no final de saudação.

    $Configuration.GeneratedCertificatePath = "[C:\Path\To\Certificate.cer]"

toosee o que você defina tipo **$Configuration**.

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

restante Olá desta seção pressupõe que você tenha uma variável criada conforme descrito apenas.

##### <a name="declare-hello-virtual-network-toohello-app"></a>Declarar Olá rede virtual toohello aplicativo
Use Olá seguindo comando tootell Olá aplicativo que ele usará essa rede virtual específico. Isso causará Olá aplicativo toogenerate certificados necessários:

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -PropertyObject @{"VnetResourceId" = "/subscriptions/$($Configuration.VnetSubscriptionId)/resourceGroups/$($Configuration.VnetResourceGroup)/providers/Microsoft.ClassicNetwork/virtualNetworks/$($Configuration.VnetName)"} -Location $Configuration.WebAppLocation -ApiVersion 2015-07-01

Se este comando for bem-sucedido, **$vnet** deverá conter uma variável **Properties**. Olá **propriedades** variável deve conter um certificado impressão digital e hello certificado de dados.

##### <a name="upload-hello-web-app-certificate-toohello-virtual-network"></a>Carregar Olá web aplicativo certificado toohello VPN
Uma única etapa manual é necessária para cada combinação de assinatura e rede virtual. Ou seja, se você estiver se conectando a aplicativos de assinatura A tooVirtual rede A, você precisará toodo esta etapa apenas uma vez, independentemente de quantos aplicativos você configurar. Se você estiver adicionando uma nova rede virtual de tooanother de aplicativo, você precisará toodo novamente. motivo de saudação para isso é que um conjunto de certificados é gerado em um nível de assinatura no serviço de aplicativo do Azure e conjunto de saudação é gerado uma vez para cada rede virtual que Olá aplicativos se conectam ao.

Olá certificados serão já foram definidos se você seguir essas etapas ou se você está integrada com hello mesmo rede virtual usando o portal de saudação.

Olá primeira etapa é o arquivo do toogenerate hello. cer. Olá segunda etapa é tooupload hello. cer arquivo tooyour VPN. arquivo do toogenerate hello. cer de chamada de API de saudação nos Olá etapa anterior, execute Olá comandos a seguir.

    $certBytes = [System.Convert]::FromBase64String($vnet.Properties.certBlob)
    [System.IO.File]::WriteAllBytes("$($Configuration.GeneratedCertificatePath)", $certBytes)

certificado Olá será encontrado no local de saudação que **$Configuration.GeneratedCertificatePath** especifica.

certificado de saudação tooupload manualmente, use Olá [portal do Azure] [ azureportal] e **(clássico) de rede Virtual procurar** > **asconexõesVPN**  >  **Ponto a site** > **gerenciar certificados**. Nesse local, carregue seu certificado.

##### <a name="get-hello-point-to-site-package"></a>Obter o pacote de ponto para site Olá
Olá próxima etapa na configuração de uma conexão de rede virtual em um aplicativo web é tooget Olá ponto a site pacote e fornecê-la tooyour web app.

Salve Olá seguir chamado GetNetworkPackageUri.json em algum lugar no seu computador, por exemplo, C:\Azure\Templates\GetNetworkPackageUri.json o arquivo de modelo tooa.

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


Defina os parâmetros de entrada:

    $parameters = @{"certData" = $vnet.Properties.certBlob ;
    certThumbprint = $vnet.Properties.certThumbprint ;
    "networkName" = $Configuration.VnetName }

Chame o script hello:

    $output = New-AzureRmResourceGroupDeployment -Name unused -ResourceGroupName $Configuration.VnetResourceGroup -TemplateParameterObject $parameters -TemplateFile C:\PATH\TO\GetNetworkPackageUri.json


variável de saudação **$output. Outputs.packageUri** agora conterá Olá pacote URI toobe fornecido tooyour web app.

##### <a name="upload-hello-point-to-site-package-tooyour-app"></a>Carregar Olá pacote de ponto para site tooyour aplicativo
Olá última etapa é tooprovide Olá aplicativo com este pacote. Basta executar o próximo comando de saudação:

    $vnet = New-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)/primary" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections/gateways" -ApiVersion 2015-07-01 -PropertyObject @{"VnetName" = $Configuration.VnetName ; "VpnPackageUri" = $($output.Outputs.packageUri).Value } -Location $Configuration.WebAppLocation

Se uma mensagem solicitará que você tooconfirm que você está substituindo um recurso existente, verifique se tooallow-lo.

Depois que esse comando for bem-sucedida, seu aplicativo agora deve ser a rede virtual conectado toohello. tooconfirm êxito, acesse o console do aplicativo tooyour e digite Olá a seguir:

    SET WEBSITE_

Se houver uma variável de ambiente chamada WEBSITE_VNETNAME que tem um valor que corresponda ao nome hello da rede virtual de destino de saudação, todas as configurações tiveram êxito.

### <a name="update-classic-vnet-integration-information"></a>Atualizar informações de integração VNet clássica
tooupdate ou ressincronizar as informações, simplesmente Repita as etapas de saudação que você seguiu quando você criou a integração de saudação em primeiro lugar de saudação. Essas etapas são:

1. Defina as informações de configuração.
2. Declare Olá rede virtual toohello aplicativo.
3. Obter pacote de ponto para site hello.
4. Carregar Olá pacote de ponto para site tooyour aplicativo.

### <a name="disconnect-your-app-from-a-classic-vnet"></a>Desconectar o aplicativo de uma VNet clássica
toodisconnect Olá aplicativo, você precisar de informações de configuração de Olá que foi definidas durante a integração da rede virtual. Usando essas informações, não há toodisconnect de comando, em seguida, um aplicativo de sua rede virtual.

    $vnet = Remove-AzureRmResource -Name "$($Configuration.WebAppName)/$($Configuration.VnetName)" -ResourceGroupName $Configuration.WebAppResourceGroup -ResourceType "Microsoft.Web/sites/virtualNetworkConnections" -ApiVersion 2015-07-01

## <a name="resource-manager-virtual-networks"></a>Redes virtuais do Gerenciador de Recursos
As redes virtuais do Resource Manager têm APIs do Azure Resource Manager que simplificam alguns processos se comparadas com redes virtuais clássicas. Temos um script que ajudarão você a concluir Olá tarefas a seguir:

* Criar uma rede virtual do Gerenciador de Recursos e integrar o aplicativo a ela.
* Criar um gateway, configurar a conectividade ponto a site em uma rede virtual do Gerenciador de Recursos pré-existente e integrar o aplicativo a ela.
* Integrar o aplicativo a uma rede virtual do Gerenciador de Recursos pré-existente que tem um gateway e habilitar a conectividade ponto a site.
* Desconecte o aplicativo da rede virtual.

### <a name="resource-manager-vnet-app-service-integration-script"></a>Script de integração do Serviço de Aplicativo de VNet do Gerenciador de Recursos
Copie Olá seguinte script e salve-o arquivo tooa. Se você não quiser o script de saudação toouse, sinta-se livre toolearn dele toosee como tooset as coisas com uma rede virtual do Gerenciador de recursos.

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

Salve uma cópia do script hello. Neste artigo, ele é chamado de V2VnetAllinOne.ps1, mas você pode usar outro nome. Não há nenhum argumento para esse script. Basta executá-lo. Olá primeiro script hello fará é solicitar que você toosign no. Depois que você entrar, o script hello obtém os detalhes sobre sua conta e retorna uma lista de assinaturas. Contagem não solicitação Olá suas credenciais, execução de script inicial Olá terá esta aparência:

    PS C:\Users\ccompy\Documents\VNET> .\V2VnetAllInOne.ps1
    Please Login

    Environment           : AzureCloud
    Account               : ccompy@microsoft.com
    TenantId              : 722278f-fef1-499f-91ab-2323d011db47
    SubscriptionId        : af5358e1-acac-2c90-a9eb-722190abf47a
    CurrentStorageAccount :

    Choose a subscription

    1) Assinatura de demonstração (af5358e1-acac-2c90-a9eb-722190abf47a)
    2) Teste MS (a5350f55-dd5a-41ec-2ddb-ff7b911bb2ef)
    3) Assinatura de demonstração Purple (2d4c99a4-57f9-4d5e-a0a1-0034c52db59d)

    Escolher uma opção: 3

    Conta      : ccompy@microsoft.com Ambiente  : Assinatura da Nuvem do Azure: 2d4c99a4-57f9-4d5e-a0a1-0034c52db59d Locatário       : 722278f-fef1-499f-91ab-2323d011db47

    Digite hello grupo de recursos do seu aplicativo: hcdemo rg digite Olá nome do seu aplicativo: v2vnetpowershell o que fazer você deseja toodo?

    1) Adicionar uma nova rede Virtual de tooan aplicativo
    2) Adicionar um aplicativo de tooan de rede Virtual existente
    3) Remover uma rede Virtual de um aplicativo

restante Olá desta seção explica cada uma dessas três opções.

### <a name="create-a-resource-manager-vnet-and-integrate-with-it"></a>Criar uma VNet do Gerenciador de Recursos e realizar a integração a ela
Selecione de uma nova rede virtual que usa Olá modelo de implantação do Gerenciador de recursos e integrá-lo com seu aplicativo, toocreate **1) adicionar uma nova rede Virtual de tooan aplicativo**. Isso solicitará nome hello da rede virtual hello. No meu caso, como você pode ver no hello configurações, a seguir, usei nome hello, v2pshell.

script Hello fornece detalhes de saudação sobre a rede virtual de saudação que está sendo criado. Se desejar, eu pode alterar qualquer um dos valores de saudação. Em execução neste exemplo, criei uma rede virtual que tenha Olá configurações a seguir:

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

Se você quiser toochange qualquer um dos valores hello, digite **Y** e fazer alterações de saudação. Quando estiver satisfeito com as configurações de rede virtual hello, digite **N** ou pressione Enter quando solicitado sobre como alterar configurações de saudação. A partir daí até a conclusão, script hello dirá alguns que ' i ' s fazer até que se inicie o gateway de rede virtual toocreate hello. Essa etapa pode levar horas tooan. Não há nenhum indicador de progresso durante essa fase, mas o script hello informará quando Olá gateway foi criado.

Quando o script hello termina, ele indicará que **concluído**. Neste ponto, você terá uma rede virtual do Gerenciador de recursos que tem nome hello e configurações que você selecionou. Essa nova rede virtual também será integrada ao aplicativo.

### <a name="integrate-your-app-with-a-preexisting-resource-manager-vnet"></a>Integrar seu aplicativo a uma VNet pré-existente do Gerenciador de Recursos
Quando você estiver integrando uma rede virtual preexistente, se você fornecer uma rede virtual do Gerenciador de recursos que não tem um gateway ou a conectividade ponto a site, script hello configurará que. Se Olá VNET já tiver essas coisas configuradas, script hello vai toohello alinhada a integração de aplicativo. toostart esse processo, basta selecionar **2) adicione uma rede Virtual existente de tooan aplicativo**.

Essa opção funciona somente se você tiver uma rede virtual preexistente Gerenciador de recursos que está em Olá mesma assinatura que seu aplicativo. Depois de selecionar a opção hello, você verá uma lista de suas redes virtuais do Gerenciador de recursos.   

    Select a VNET toointegrate with

    1) v2demonetwork
    2) v2pshell
    3) v2vnetintdemo
    4) v2asenetwork
    5) v2pshell2

    Escolher uma opção: 5

Basta selecione a rede virtual de saudação que você deseja toointegrate com. Se você já tiver um gateway que tenha conectividade de ponto para site habilitada, o script hello simplesmente integrará seu aplicativo com sua rede virtual. Se você não tiver um gateway, você precisará toospecify Olá gateway de sub-rede. A sub-rede do gateway deve estar em seu espaço de endereço de Rede Virtual e não pode estar em outra sub-rede. se você tiver uma rede virtual sem um gateway e executar essa etapa, verá o seguinte:

    This Virtual Network has no gateway. I will need toocreate one.
    Your VNET is in hello address space 172.16.0.0/16, with hello following Subnets:
    default: 172.16.0.0/24
    Please choose a GatewaySubnet address space: 172.16.1.0/26

Neste exemplo, criei um gateway de rede virtual que tenha Olá configurações a seguir:

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

Se você quiser toochange qualquer uma dessas configurações, você pode fazer isso. Caso contrário, pressione Enter e o script hello criará seu gateway e anexar a sua rede virtual do aplicativo tooyour. a hora de criação de gateway Olá ainda é uma hora, no entanto, portanto certifique-se de que que você tenha em mente. Quando tudo estiver concluído, o script hello dirá **concluído**.

### <a name="disconnect-your-app-from-a-resource-manager-vnet"></a>Desconectar o aplicativo de uma VNet do Gerenciador de Recursos
Desconectar-se seu aplicativo de sua rede virtual não derrubar o gateway de saudação ou desabilitar a conectividade ponto a site. Afinal de contas, você poderia usá-los para alguma outra coisa. Ele também não desconectá-lo de todos os outros aplicativos que não sejam Olá fornecido por você. tooperform esta ação, selecione **3) remover uma rede Virtual de um aplicativo**. Quando você fizer isso, verá algo assim:

    Currently connected tooVNET v2pshell

    Confirm
    Are you sure you want toodelete hello following resource:
    /subscriptions/edcc99a4-b7f9-4b5e-a9a1-3034c51db496/resourceGroups/hcdemo-rg/providers/Microsoft.Web/sites/v2vnetpowers
    hell/virtualNetworkConnections/v2pshell
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"):

Embora o script hello diz que a exclusão, não exclui rede virtual hello. Ele é apenas Removendo integração hello. Depois de confirmar que esse é o que você deseja toodo, o comando Olá é processado muito rapidamente e informa **True** quando é feito.

<!--Links-->
[createvpngateway]: http://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/
[azureportal]: http://portal.azure.com
