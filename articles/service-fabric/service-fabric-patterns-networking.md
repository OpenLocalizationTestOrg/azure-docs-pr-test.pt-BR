---
title: "padrões de aaaNetworking para o Azure Service Fabric | Microsoft Docs"
description: "Descreve os padrões comuns de rede de malha do serviço e como toocreate um cluster usando os recursos de rede do Azure."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2017
ms.author: ryanwi
ms.openlocfilehash: 5973e3f9917076c6a36e71443ec256e0f414ff87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-networking-patterns"></a>Padrões de rede do Service Fabric
Você pode integrar seu cluster do Azure Service Fabric a outros recursos de rede do Azure. Neste artigo, mostramos como toocreate clusters que Olá use recursos a seguir:

- [Rede virtual ou sub-rede existente](#existingvnet)
- [Endereço IP público estático](#staticpublicip)
- [Balanceador de carga somente interno](#internallb)
- [Balanceador interno e externo de carga](#internalexternallb)

O Service Fabric é executado em um conjunto de dimensionamento de máquinas virtuais padrão. Qualquer funcionalidade que você pode usar em um conjunto de dimensionamento de máquinas virtuais você pode usar também com um cluster do Service Fabric. seções de rede Olá dos modelos do Azure Resource Manager Olá para conjuntos de escala de máquina virtual e serviço de malha são idênticas. Depois de implantar tooan existentes de rede virtual, é fácil tooincorporate outros recursos, como a rota expressa do Azure, o Gateway de VPN do Azure, um grupo de segurança de rede e o emparelhamento de rede virtual do sistema de rede.

O Service Fabric é único entre outros recursos de rede em um aspecto. Olá [portal do Azure](https://portal.azure.com) internamente usa Olá Service Fabric recurso provedor toocall tooa cluster tooget informações sobre nós e aplicativos. provedor de recursos de malha do serviço Olá requer acesso de entrada publicamente acessível toohello HTTP gateway porta (19080, por padrão) no ponto de extremidade de gerenciamento de saudação. [Gerenciador do Service Fabric](service-fabric-visualizing-your-cluster.md) usa Olá toomanage de ponto de extremidade de gerenciamento de cluster. provedor de recursos de malha do serviço Olá também usa essas informações de tooquery de porta sobre o cluster, toodisplay em Olá portal do Azure. 

Se a porta 19080 não é acessível pelo provedor de recursos de malha do serviço hello, uma mensagem como *nós não encontrado* aparece no portal do hello, e sua lista de nó e o aplicativo estiver vazia. Se você quiser toosee seu cluster em Olá portal do Azure, o balanceador de carga deve expor um endereço IP público e seu grupo de segurança de rede deve permitir o tráfego da porta 19080. Se a configuração não atender a esses requisitos, Olá portal do Azure não exibir o status de saudação do cluster.

## <a name="templates"></a>Modelos

Todos os modelos do Service Fabric estão em [um arquivo de download](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip). Você deve ser capaz de toodeploy modelos hello como-usando Olá comandos do PowerShell a seguir. Se você estiver implantando Olá modelo de rede Virtual do Azure existente ou Olá estático público modelo de IP, leia primeiro a saudação [inicial instalação](#initialsetup) deste artigo.

<a id="initialsetup"></a>
## <a name="initial-setup"></a>Configuração inicial

### <a name="existing-virtual-network"></a>Rede virtual existente

Olá exemplo a seguir, vamos começar com uma rede virtual existente chamada ExistingRG-vnet no hello **ExistingRG** grupo de recursos. subrede Olá é denominado default. Esses recursos padrão são criados quando você usar Olá toocreate portal do Azure uma máquina de virtual (VM) padrão. Você pode criar uma rede virtual hello e sub-rede sem criar hello VM, mas Olá principal objetivo de adicionar uma rede de virtual cluster tooan existente é tooother de conectividade de rede tooprovide VMs. Olá criar VM fornece um bom exemplo de como uma rede virtual existente normalmente é usada. Se o cluster do Service Fabric usa apenas um balanceador de carga interno, sem um endereço IP público, você pode usar Olá VM e seu IP público como seguro *saltar caixa*.

### <a name="static-public-ip-address"></a>Endereço IP público estático

Um endereço IP público estático geralmente é um recurso dedicado gerenciado separadamente do hello VM ou VMs que ele está atribuído. Ela é provisionada em um grupo de recursos de rede dedicado (como tooin contrário Olá Service Fabric grupo de recursos em si). Criar um endereço IP público estático chamado staticIP1 em Olá mesmo grupo de recursos de ExistingRG, no portal do Azure de saudação ou usando o PowerShell:

```powershell
PS C:\Users\user> New-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG -Location westus -AllocationMethod Static -DomainNameLabel sfnetworking

Name                     : staticIP1
ResourceGroupName        : ExistingRG
Location                 : westus
Id                       : /subscriptions/1237f4d2-3dce-1236-ad95-123f764e7123/resourceGroups/ExistingRG/providers/Microsoft.Network/publicIPAddresses/staticIP1
Etag                     : W/"fc8b0c77-1f84-455d-9930-0404ebba1b64"
ResourceGuid             : 77c26c06-c0ae-496c-9231-b1a114e08824
ProvisioningState        : Succeeded
Tags                     :
PublicIpAllocationMethod : Static
IpAddress                : 40.83.182.110
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : null
DnsSettings              : {
                             "DomainNameLabel": "sfnetworking",
                             "Fqdn": "sfnetworking.westus.cloudapp.azure.com"
                           }
```

### <a name="service-fabric-template"></a>Modelo do Service Fabric

Exemplos de saudação neste artigo, usamos Olá Service Fabric template.json. Você pode usar o modelo de Olá de toodownload de assistente padrão do portal de saudação do portal de saudação antes de criar um cluster. Você também pode usar um dos modelos de saudação em Olá [Galeria de modelos de](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric), como Olá [cluster do Service Fabric de cinco nós](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/).

<a id="existingvnet"></a>
## <a name="existing-virtual-network-or-subnet"></a>Rede virtual ou sub-rede existente

1. Alterar nome de toohello de parâmetro hello sub-rede da sub-rede existente hello e, em seguida, adicione dois novos parâmetros tooreference Olá rede virtual existente:

    ```
        "subnet0Name": {
                "type": "string",
                "defaultValue": "default"
            },
            "existingVNetRGName": {
                "type": "string",
                "defaultValue": "ExistingRG"
            },

            "existingVNetName": {
                "type": "string",
                "defaultValue": "ExistingRG-vnet"
            },
            /*
            "subnet0Name": {
                "type": "string",
                "defaultValue": "Subnet-0"
            },
            "subnet0Prefix": {
                "type": "string",
                "defaultValue": "10.0.0.0/24"
            },*/
    ```


2. Saudação de alteração `vnetID` toopoint variável toohello rede virtual existente:

    ```
            /*old "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",*/
            "vnetID": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingVNetRGName'), '/providers/Microsoft.Network/virtualNetworks/', parameters('existingVNetName'))]",
    ```

3. Remova `Microsoft.Network/virtualNetworks` de seus recursos de modo que o Azure não crie uma nova rede virtual:

    ```
    /*{
    "apiVersion": "[variables('vNetApiVersion')]",
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[parameters('virtualNetworkName')]",
    "location": "[parameters('computeLocation')]",
    "properities": {
        "addressSpace": {
            "addressPrefixes": [
                "[parameters('addressPrefix')]"
            ]
        },
        "subnets": [
            {
                "name": "[parameters('subnet0Name')]",
                "properties": {
                    "addressPrefix": "[parameters('subnet0Prefix')]"
                }
            }
        ]
    },
    "tags": {
        "resourceType": "Service Fabric",
        "clusterName": "[parameters('clusterName')]"
    }
    },*/
    ```

4. Comente a rede virtual de saudação da saudação `dependsOn` atributo de `Microsoft.Compute/virtualMachineScaleSets`, portanto, não dependem criando uma nova rede virtual:

    ```
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Computer/virtualMachineScaleSets",
    "name": "[parameters('vmNodeType0Name')]",
    "location": "[parameters('computeLocation')]",
    "dependsOn": [
        /*"[concat('Microsoft.Network/virtualNetworks/', parameters('virtualNetworkName'))]",
        */
        "[Concat('Microsoft.Storage/storageAccounts/', variables('uniqueStringArray0')[0])]",

    ```

5. Implante o modelo de saudação:

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingexistingvnet -Location westus
    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingexistingvnet -TemplateFile C:\SFSamples\Final\template\_existingvnet.json
    ```

    Após a implantação, sua rede virtual deve incluir as VMs de conjunto de escala de novo hello. tipo de nó de conjunto de escala do Hello máquina virtual deve mostrar a sub-rede e a rede virtual existente do hello. Você também pode usar protocolo de área de trabalho remota (RDP) tooaccess Olá VM que já estava na rede virtual hello e tooping Olá nova escala definida como VMs:

    ```
    C:>\Users\users>ping 10.0.0.5 -n 1
    C:>\Users\users>ping NOde1000000 -n 1
    ```

Outro exemplo, consulte [que não é específico tooService malha](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet).


<a id="staticpublicip"></a>
## <a name="static-public-ip-address"></a>Endereço IP público estático

1. Adicione parâmetros de nome de saudação do hello existentes do grupo de recursos IP estático, o nome e o nome de domínio totalmente qualificado (FQDN):

    ```
    "existingStaticIPResourceGroup": {
                "type": "string"
            },
            "existingStaticIPName": {
                "type": "string"
            },
            "existingStaticIPDnsFQDN": {
                "type": "string"
    }
    ```

2. Remover Olá `dnsName` parâmetro. (endereço IP estático de saudação já tem um.)

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

3. Adicione um variável tooreference Olá endereço IP estático existente:

    ```
    "existingStaticIP": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingStaticIPResourceGroup'), '/providers/Microsoft.Network/publicIPAddresses/', parameters('existingStaticIPName'))]",
    ```

4. Remova `Microsoft.Network/publicIPAddresses` de seus recursos de modo que o Azure não crie um novo endereço IP:

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

5. Comente o endereço IP de saudação do hello `dependsOn` atributo de `Microsoft.Network/loadBalancers`, portanto, você não depende de criar um novo endereço IP:

    ```
    "apiVersion": "[variables('lbIPApiVersion')]",
    "type": "Microsoft.Network/loadBalancers",
    "name": "[concat('LB', '-', parameters('clusterName'), '-', parameters('vmNodeType0Name'))]",
    "location": "[parameters('computeLocation')]",
    /*
    "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', concat(parameters('lbIPName'), '-', '0'))]"
    ], */
    "properties": {
    ```

6. Em hello `Microsoft.Network/loadBalancers` recurso, alteração Olá `publicIPAddress` elemento `frontendIPConfigurations` tooreference Olá endereço IP estático existente em vez de um criado recentemente:

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                "publicIPAddress": {
                                    /*"id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"*/
                                    "id": "[variables('existingStaticIP')]"
                                }
                            }
                        }
                    ],
    ```

7. Em Olá `Microsoft.ServiceFabric/clusters` recursos, alteração `managementEndpoint` toohello FQDN do DNS do endereço IP estático de saudação. Se você estiver usando um cluster seguro, certifique-se de alterar *http://* muito*https://*. (Observe que essa etapa se aplica somente os clusters de malha tooService. Se estiver usando um conjunto de dimensionamento de máquinas virtuais, ignore esta etapa.)

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',parameters('existingStaticIPDnsFQDN'),':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

8. Implante o modelo de saudação:

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingstaticip -Location westus

    $staticip = Get-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG

    $staticip

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingstaticip -TemplateFile C:\SFSamples\Final\template\_staticip.json -existingStaticIPResourceGroup $staticip.ResourceGroupName -existingStaticIPName $staticip.Name -existingStaticIPDnsFQDN $staticip.DnsSettings.Fqdn
    ```

Após a implantação, você pode ver que o balanceador de carga é toohello associada público endereço IP estático de saudação outro grupo de recursos. Olá ponto de extremidade de conexão de cliente do Service Fabric e [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) toohello de ponto de extremidade FQDN do DNS do endereço IP estático de saudação.

<a id="internallb"></a>
## <a name="internal-only-load-balancer"></a>Balanceador de carga somente interno

Este cenário substitui Olá balanceador externo de carga no modelo de serviço malha saudação padrão com um balanceador de carga interno somente. Para implicações para Olá portal do Azure e para o provedor de recursos de malha do serviço Olá, consulte Olá anterior de seção.

1. Remover Olá `dnsName` parâmetro. (Ele não é necessário.)

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

2. Opcionalmente, você poderá adicionar um parâmetro de endereço IP estático se estiver usando o método de alocação estática. Se você usar um método de alocação dinâmica, você não precisará toodo desta etapa.

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

3. Remova `Microsoft.Network/publicIPAddresses` de seus recursos de modo que o Azure não crie um novo endereço IP:

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

4. Remova o endereço IP hello `dependsOn` atributo de `Microsoft.Network/loadBalancers`, portanto, você não depende de criar um novo endereço IP. Adicionar a rede virtual Olá `dependsOn` atributo porque balanceador de carga Olá agora depende de subrede da rede virtual Olá Olá:

    ```
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'))]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /*"[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"*/
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
    ```

5. Alterar do balanceador de carga Olá `frontendIPConfigurations` configuração que usa um `publicIPAddress`, toousing uma sub-rede e `privateIPAddress`. `privateIPAddress` usa um endereço IP interno estático predefinido. toouse um endereço IP dinâmico, remover Olá `privateIPAddress` elemento e altere `privateIPAllocationMethod` muito**dinâmico**.

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /*
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                } */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
    ```

6. Em Olá `Microsoft.ServiceFabric/clusters` recursos, alteração `managementEndpoint` endereço de Balanceador de carga interno toopoint toohello. Se você usar um cluster seguro, certifique-se de alterar *http://* muito*https://*. (Observe que essa etapa se aplica somente os clusters de malha tooService. Se estiver usando um conjunto de dimensionamento de máquinas virtuais, ignore esta etapa.)

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',reference(variables('lbID0')).frontEndIPConfigurations[0].properties.privateIPAddress,':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

7. Implante o modelo de saudação:

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternallb -TemplateFile C:\SFSamples\Final\template\_internalonlyLB.json
    ```

Após a implantação, o balanceador de carga usa endereço IP de saudação privada 10.0.0.250 estático. Se você tiver outro computador na mesma rede virtual, você pode ir toohello interno [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) ponto de extremidade. Observe que se conecta tooone de nós de saudação por trás do balanceador de carga de saudação.

<a id="internalexternallb"></a>
## <a name="internal-and-external-load-balancer"></a>Balanceador de carga interno e externo

Nesse cenário, você começar com balanceador de carga externo de tipo de nó único existente hello e adicionar um balanceador de carga interno para Olá mesmo tipo de nó. Balanceador de carga único tooa só pode ser atribuído a um pool de endereços de back-end de tooa de porta de back-end conectado. Escolha qual balanceador de carga terá as suas portas do aplicativo e o balanceador de carga terá seus pontos de extremidade de gerenciamento (portas 19000 e 19080). Se você colocar pontos de extremidade de gerenciamento Olá no balanceador de carga interno hello, lembre-Olá mente recursos de malha do serviço discutidas anteriormente no artigo de saudação de restrições de provedor. O exemplo hello que usamos, pontos de extremidade de gerenciamento Olá permanecem em Olá balanceador externo de carga. Você também adicionar uma porta de aplicativo 80 e colocá-lo no balanceador de carga interno hello.

Em um cluster de dois tipo de nó, um tipo de nó é no balanceador de carga externo hello. Olá outro tipo de nó é no balanceador de carga interno hello. toouse um cluster de dois tipo de nó, Olá portal dois tipo de nó modelo criado (o que vem com dois balanceadores de carga), comutador hello segundo carga balanceador tooan balanceador de carga interno. Para obter mais informações, consulte Olá [balanceador de carga interno somente](#internallb) seção.

1. Adicione o parâmetro do endereço IP estático de carga interno balanceador da saudação. (Para anotações relacionadas toousing um endereço IP dinâmico, consulte as seções anteriores deste artigo).

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

2. Adicione um parâmetro de porta 80 do aplicativo.

3. versões interno tooadd Olá existente rede variáveis, copie e cole-os e adicionar "-Int" toohello nome:

    ```
    /* Add internal load balancer networking variables */
            "lbID0-Int": "[resourceId('Microsoft.Network/loadBalancers', concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal'))]",
            "lbIPConfig0-Int": "[concat(variables('lbID0-Int'),'/frontendIPConfigurations/LoadBalancerIPConfig')]",
            "lbPoolID0-Int": "[concat(variables('lbID0-Int'),'/backendAddressPools/LoadBalancerBEAddressPool')]",
            "lbProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricGatewayProbe')]",
            "lbHttpProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricHttpGatewayProbe')]",
            "lbNatPoolID0-Int": "[concat(variables('lbID0-Int'),'/inboundNatPools/LoadBalancerBEAddressNatPool')]",
            /* Internal load balancer networking variables end */
    ```

4. Se você iniciar com o modelo gerado pelo portal Olá que usa a porta 80 do aplicativo, o modelo de portal saudação padrão adiciona AppPort1 (porta 80) no balanceador de carga externo hello. Nesse caso, remova AppPort1 balanceador externo de saudação `loadBalancingRules` e testes, para que você possa adicionar balanceador de carga interno toohello:

    ```
    "loadBalancingRules": [
        {
            "name": "LBHttpRule",
            "properties":{
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[variables('lbHttpProbeID0')]"
                },
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from hello external load balancer.
        {
            "name": "AppPortLBRule1",
            "properties": {
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('loadBalancedAppPort1')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[concate(variables('lbID0'), '/probes/AppPortProbe1')]"
                },
                "protocol": "tcp"
            }
        }*/

    ],
    "probes": [
        {
            "name": "FabricGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricTcpGatewayPort')]",
                "protocol": "tcp"
            }
        },
        {
            "name": "FabricHttpGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricHttpGatewayPort')]",
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from hello external load balancer.
        {
            "name": "AppPortProbe1",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('loadBalancedAppPort1')]",
                "protocol": "tcp"
            }
        } */

    ],
    "inboundNatPools": [
    ```

5. Adicione um segundo recurso `Microsoft.Network/loadBalancers`. Parece semelhante balanceador de carga interno toohello criado no hello [balanceador de carga interno somente](#internallb) seção, mas usa hello "-Int" carregar balanceador variáveis e implementa somente Olá aplicativo porta 80. Isso também remove `inboundNatPools`, tookeep pontos de extremidade RDP no balanceador de carga público hello. Se você quiser RDP no balanceador de carga interno hello, mover `inboundNatPools` de toothis de Balanceador de carga externo de saudação interno balanceador de carga:

    ```
            /* Add a second load balancer, configured with a static privateIPAddress and hello "-Int" load balancer variables. */
            {
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                /* Add "-Internal" toohello name. */
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal')]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /* Remove public IP dependsOn, add vnet dependsOn
                    "[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"
                    */
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
                "properties": {
                    "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /* Switch from Public tooPrivate IP address
                                */
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                }
                                */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
                    "backendAddressPools": [
                        {
                            "name": "LoadBalancerBEAddressPool",
                            "properties": {}
                        }
                    ],
                    "loadBalancingRules": [
                        /* Add hello AppPort rule. Be sure tooreference hello "-Int" versions of backendAddressPool, frontendIPConfiguration, and hello probe variables. */
                        {
                            "name": "AppPortLBRule1",
                            "properties": {
                                "backendAddressPool": {
                                    "id": "[variables('lbPoolID0-Int')]"
                                },
                                "backendPort": "[parameters('loadBalancedAppPort1')]",
                                "enableFloatingIP": "false",
                                "frontendIPConfiguration": {
                                    "id": "[variables('lbIPConfig0-Int')]"
                                },
                                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                                "idleTimeoutInMinutes": "5",
                                "probe": {
                                    "id": "[concat(variables('lbID0-Int'),'/probes/AppPortProbe1')]"
                                },
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "probes": [
                    /* Add hello probe for hello app port. */
                    {
                            "name": "AppPortProbe1",
                            "properties": {
                                "intervalInSeconds": 5,
                                "numberOfProbes": 2,
                                "port": "[parameters('loadBalancedAppPort1')]",
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "inboundNatPools": [
                    ]
                },
                "tags": {
                    "resourceType": "Service Fabric",
                    "clusterName": "[parameters('clusterName')]"
                }
            },
    ```

6. Em `networkProfile` para Olá `Microsoft.Compute/virtualMachineScaleSets` recursos, adicionar pool de endereços de back-end interno de saudação:

    ```
    "loadBalancerBackendAddressPools": [
                                                        {
                                                            "id": "[variables('lbPoolID0')]"
                                                        },
                                                        {
                                                            /* Add internal BE pool */
                                                            "id": "[variables('lbPoolID0-Int')]"
                                                        }
    ],
    ```

7. Implante o modelo de saudação:

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternalexternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternalexternallb -TemplateFile C:\SFSamples\Final\template\_internalexternalLB.json
    ```

Após a implantação, você pode ver dois balanceadores de carga no grupo de recursos de saudação. Se você procurar balanceadores de carga hello, você pode ver o endereço IP público de saudação e pontos de extremidade (portas 19000 e 19080) atribuídos toohello público endereço IP de gerenciamento. Você também pode ver Olá estático interno IP endereço e o aplicativo de ponto de extremidade (porta 80) atribuído toohello interno balanceador de carga. Uso de balanceadores de carga mesma escala de máquina virtual hello definir pool de back-end.

## <a name="next-steps"></a>Próximas etapas
[Criar um cluster](service-fabric-cluster-creation-via-arm.md)
