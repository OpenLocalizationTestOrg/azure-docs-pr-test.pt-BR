---
title: "aaaConfigure modos para serviços de contêiner de malha do Azure serviço de rede | Microsoft Docs"
description: "Saiba como toosetup Olá diferentes modos de rede que o Azure Service Fabric suporta."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 5c5dd4c590c7698a947503cbe8ef66ff7d6b503a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-container-networking-modes"></a><span data-ttu-id="9d6ae-103">Modos de rede de contêiner do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9d6ae-103">Service Fabric container networking modes</span></span>

<span data-ttu-id="9d6ae-104">Hello modo de rede padrão oferecidos em Olá malha do serviço de cluster para serviços de contêiner é hello `nat` modo de rede.</span><span class="sxs-lookup"><span data-stu-id="9d6ae-104">hello default networking mode offered in hello Service Fabric cluster for container services is hello `nat` networking mode.</span></span> <span data-ttu-id="9d6ae-105">Com hello `nat` modo, ter mais de um toohello contêineres de escuta de serviço de rede da mesma porta resulta em erros de implantação.</span><span class="sxs-lookup"><span data-stu-id="9d6ae-105">With hello `nat` networking mode, having more than one containers service listening toohello same port results in deployment errors.</span></span> <span data-ttu-id="9d6ae-106">Para executar vários serviços de escutam Olá dá suporte a mesma porta do Service Fabric Olá `open` modo de rede (versão 5.7 ou superior).</span><span class="sxs-lookup"><span data-stu-id="9d6ae-106">For running several services that listen on hello same port, Service Fabric supports hello `open` networking mode (version 5.7 or higher).</span></span> <span data-ttu-id="9d6ae-107">Com hello `open` modo de acesso à rede, cada serviço de contêiner é um endereço IP atribuído dinamicamente, permitindo internamente toohello de toolisten vários serviços a mesma porta.</span><span class="sxs-lookup"><span data-stu-id="9d6ae-107">With hello `open` networking mode, each container service gets a dynamically assigned IP address internally allowing multiple services toolisten toohello same port.</span></span>   

<span data-ttu-id="9d6ae-108">Assim, com um único tipo de serviço com um ponto de extremidade estático definido no manifesto do serviço Olá, novos serviços podem ser criados e excluídos sem erros de implantação usando Olá `open` modo de rede.</span><span class="sxs-lookup"><span data-stu-id="9d6ae-108">Thus, with a single service type with a static endpoint defined in hello service manifest, new services may be created and deleted without deployment errors using hello `open` networking mode.</span></span> <span data-ttu-id="9d6ae-109">Da mesma forma, você pode usar Olá mesmo `docker-compose.yml` arquivo com mapeamentos de porta estática para a criação de vários serviços.</span><span class="sxs-lookup"><span data-stu-id="9d6ae-109">Similarly, one can use hello same `docker-compose.yml` file with static port mappings for creating multiple services.</span></span>

<span data-ttu-id="9d6ae-110">Usar Olá atribuído dinamicamente IP toodiscover services não é aconselhável desde alterações de endereço IP hello quando o serviço de saudação é reiniciado ou move tooanother nó.</span><span class="sxs-lookup"><span data-stu-id="9d6ae-110">Using hello dynamically assigned IP toodiscover services is not advisable since hello IP address changes when hello service restarts or moves tooanother node.</span></span> <span data-ttu-id="9d6ae-111">Use somente Olá **Service Fabric Naming Service** ou hello **serviço DNS** para descoberta de serviço.</span><span class="sxs-lookup"><span data-stu-id="9d6ae-111">Only use hello **Service Fabric Naming Service**  or hello **DNS Service** for service discovery.</span></span> 


> [!WARNING]
> <span data-ttu-id="9d6ae-112">Só há permissão para um total de 4096 IPs por rede virtual no Azure.</span><span class="sxs-lookup"><span data-stu-id="9d6ae-112">Only a total of 4096 IPs are allowed per vNET in Azure.</span></span> <span data-ttu-id="9d6ae-113">Assim, soma de saudação do número de saudação de nós e Olá contêiner de instâncias de serviço (com `open` rede) não pode exceder 4096 dentro de uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="9d6ae-113">Thus, hello sum of hello number of nodes and hello number of container service instances (with `open` networking) cannot exceed 4096 within a vNET.</span></span> <span data-ttu-id="9d6ae-114">Para esses cenários de alta densidade, Olá `nat` rede é recomendado.</span><span class="sxs-lookup"><span data-stu-id="9d6ae-114">For such high-density scenarios, hello `nat` networking mode is recommended.</span></span>
>

## <a name="setting-up-open-networking-mode"></a><span data-ttu-id="9d6ae-115">Configurar o modo de rede aberto</span><span class="sxs-lookup"><span data-stu-id="9d6ae-115">Setting up open networking mode</span></span>

1. <span data-ttu-id="9d6ae-116">Configurar modelo do Azure Resource Manager hello, permitindo que o serviço DNS e Olá provedor de IP em `fabricSettings`.</span><span class="sxs-lookup"><span data-stu-id="9d6ae-116">Set up hello Azure Resource Manager template by enabling DNS Service and hello IP Provider under `fabricSettings`.</span></span> 

    ```json
    "fabricSettings": [
                {
                    "name": "DnsService",
                    "parameters": [
                       {
                            "name": "IsEnabled",
                            "value": "true"
                      }
                    ]
                },
                {
                    "name": "Hosting",
                    "parameters": [
                      { 
                            "name": "IPProviderEnabled",
                            "value": "true"
                      }
                    ]
                },
                {
                    "name":  "Trace/Etw", 
                    "parameters": [
                    {
                            "name": "Level",
                            "value": "5"
                    }
                    ]
                },
                {
                    "name": "Setup",
                    "parameters": [
                    {
                            "name": "ContainerNetworkSetup",
                            "value": "true"
                    }
                    ]
                }
            ],
    ```

2. <span data-ttu-id="9d6ae-117">Configure o perfil de rede de saudação seção tooallow toobe configurado em cada nó do cluster de saudação de endereços de IP de vários.</span><span class="sxs-lookup"><span data-stu-id="9d6ae-117">Set up hello network profile section tooallow multiple IP addresses toobe configured on each node of hello cluster.</span></span> <span data-ttu-id="9d6ae-118">Olá exemplo a seguir define cinco endereços IP por nó (, portanto, você pode ter cinco instâncias de serviço escutando a porta toohello em cada nó) para um cluster do Windows Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9d6ae-118">hello following example sets up five IP addresses per node (thus you can have five service instances listening toohello port on each node) for a Windows Service Fabric cluster.</span></span>

    ```json
    "variables": {
        "nicName": "NIC",
        "vmName": "vm",
        "virtualNetworkName": "VNet",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
        "vmNodeType0Name": "[toLower(concat('NT1', variables('vmName')))]",
        "subnet0Name": "Subnet-0",
        "subnet0Prefix": "10.0.0.0/24",
        "subnet0Ref": "[concat(variables('vnetID'),'/subnets/',variables('subnet0Name'))]",
        "lbID0": "[resourceId('Microsoft.Network/loadBalancers',concat('LB','-', parameters('clusterName'),'-',variables('vmNodeType0Name')))]",
        "lbIPConfig0": "[concat(variables('lbID0'),'/frontendIPConfigurations/LoadBalancerIPConfig')]",
        "lbPoolID0": "[concat(variables('lbID0'),'/backendAddressPools/LoadBalancerBEAddressPool')]",
        "lbProbeID0": "[concat(variables('lbID0'),'/probes/FabricGatewayProbe')]",
        "lbHttpProbeID0": "[concat(variables('lbID0'),'/probes/FabricHttpGatewayProbe')]",
        "lbNatPoolID0": "[concat(variables('lbID0'),'/inboundNatPools/LoadBalancerBEAddressNatPool')]"
    }
    "networkProfile": {
                "networkInterfaceConfigurations": [
                  {
                    "name": "[concat(parameters('nicName'), '-0')]",
                    "properties": {
                      "ipConfigurations": [
                        {
                          "name": "[concat(parameters('nicName'),'-',0)]",
                          "properties": {
                            "primary": "true",
                            "loadBalancerBackendAddressPools": [
                              {
                                "id": "[variables('lbPoolID0')]"
                              }
                            ],
                            "loadBalancerInboundNatPools": [
                              {
                                "id": "[variables('lbNatPoolID0')]"
                              }
                            ],
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 1)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 2)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 3)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 4)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 5)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        }
                      ],
                      "primary": true
                    }
                  }
                ]
              }
    ```

    <span data-ttu-id="9d6ae-119">Para clusters do Linux, uma configuração de IP pública adicional é adicionada tooallow conectividade de saída.</span><span class="sxs-lookup"><span data-stu-id="9d6ae-119">For Linux clusters, an additional public IP configuration is added tooallow outbound connectivity.</span></span> <span data-ttu-id="9d6ae-120">Olá trecho a seguir configura a cinco endereços IP por nó de um cluster do Linux:</span><span class="sxs-lookup"><span data-stu-id="9d6ae-120">hello following snippet sets up five IP addresses per node for a Linux cluster:</span></span>

    ```json
    "networkProfile": {
                "networkInterfaceConfigurations": [
                  {
                    "name": "[concat(parameters('nicName'), '-0')]",
                    "properties": {
                      "ipConfigurations": [
                        {
                          "name": "[concat(parameters('nicName'),'-',0)]",
                          "properties": {
                            "primary": "true",
                            "publicipaddressconfiguration": {
                              "name": "devpub",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "loadBalancerBackendAddressPools": [
                              {
                                "id": "[variables('lbPoolID0')]"
                              }
                            ],
                            "loadBalancerInboundNatPools": [
                              {
                                "id": "[variables('lbNatPoolID0')]"
                              }
                            ],
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 1)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 1)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 2)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 2)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 3)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 3)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 4)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 4)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 5)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 5)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        }
                      ],
                      "primary": true
                    }
                  }
                ]
              }
    ```

3. <span data-ttu-id="9d6ae-121">Para Windows clusters somente, configurar um NSG regra abrindo a porta UDP/53 para a rede virtual de saudação com hello valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="9d6ae-121">For Windows clusters only, set up an NSG rule opening up port UDP/53 for hello vNET with hello following values:</span></span>

   | <span data-ttu-id="9d6ae-122">Prioridade</span><span class="sxs-lookup"><span data-stu-id="9d6ae-122">Priority</span></span> |    <span data-ttu-id="9d6ae-123">Nome</span><span class="sxs-lookup"><span data-stu-id="9d6ae-123">Name</span></span>    |    <span data-ttu-id="9d6ae-124">Fonte</span><span class="sxs-lookup"><span data-stu-id="9d6ae-124">Source</span></span>      |  <span data-ttu-id="9d6ae-125">Destino</span><span class="sxs-lookup"><span data-stu-id="9d6ae-125">Destination</span></span>   |   <span data-ttu-id="9d6ae-126">O Barramento de</span><span class="sxs-lookup"><span data-stu-id="9d6ae-126">Service</span></span>    | <span data-ttu-id="9d6ae-127">Ação</span><span class="sxs-lookup"><span data-stu-id="9d6ae-127">Action</span></span> |
   |:--------:|:----------:|:--------------:|:--------------:|:------------:|:------:|
   |     <span data-ttu-id="9d6ae-128">2000</span><span class="sxs-lookup"><span data-stu-id="9d6ae-128">2000</span></span> | <span data-ttu-id="9d6ae-129">Custom_Dns</span><span class="sxs-lookup"><span data-stu-id="9d6ae-129">Custom_Dns</span></span> | <span data-ttu-id="9d6ae-130">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="9d6ae-130">VirtualNetwork</span></span> | <span data-ttu-id="9d6ae-131">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="9d6ae-131">VirtualNetwork</span></span> | <span data-ttu-id="9d6ae-132">DNS (UDP/53)</span><span class="sxs-lookup"><span data-stu-id="9d6ae-132">DNS (UDP/53)</span></span> | <span data-ttu-id="9d6ae-133">PERMITIR</span><span class="sxs-lookup"><span data-stu-id="9d6ae-133">Allow</span></span>  |


4. <span data-ttu-id="9d6ae-134">Especifique o modo de rede Olá no manifesto de aplicativo hello para cada serviço `<NetworkConfig NetworkType="open">`.</span><span class="sxs-lookup"><span data-stu-id="9d6ae-134">Specify hello networking mode in hello app manifest for each service `<NetworkConfig NetworkType="open">`.</span></span>  <span data-ttu-id="9d6ae-135">modo de saudação `open` resulta em serviço Olá obtendo um endereço IP dedicado.</span><span class="sxs-lookup"><span data-stu-id="9d6ae-135">hello mode `open` results in hello service getting a dedicated IP address.</span></span> <span data-ttu-id="9d6ae-136">Se um modo não for especificado, o padrão é toohello básica `nat` modo.</span><span class="sxs-lookup"><span data-stu-id="9d6ae-136">If a mode isn't specified, it defaults toohello basic `nat` mode.</span></span> <span data-ttu-id="9d6ae-137">Assim, em Olá seguinte exemplo de manifesto, `NodeContainerServicePackage1` e `NodeContainerServicePackage2` pode cada toohello escuta mesma porta (os dois serviços estão escutando em `Endpoint1`).</span><span class="sxs-lookup"><span data-stu-id="9d6ae-137">Thus, in hello following manifest example, `NodeContainerServicePackage1` and `NodeContainerServicePackage2` can each listen toohello same port (both services are listening on `Endpoint1`).</span></span>

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <ApplicationManifest ApplicationTypeName="NodeJsApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
      <Description>Calculator Application</Description>
      <Parameters>
        <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
        <Parameter Name="MyCpuShares" DefaultValue="3"></Parameter>
      </Parameters>
      <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="NodeContainerServicePackage1" ServiceManifestVersion="1.0"/>
        <Policies>
          <ContainerHostPolicies CodePackageRef="NodeContainerService1.Code" Isolation="hyperv">
           <NetworkConfig NetworkType="open"/>
           <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
          </ContainerHostPolicies>
        </Policies>
      </ServiceManifestImport>
      <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="NodeContainerServicePackage2" ServiceManifestVersion="1.0"/>
        <Policies>
          <ContainerHostPolicies CodePackageRef="NodeContainerService2.Code" Isolation="default">
            <NetworkConfig NetworkType="open"/>
            <PortBinding ContainerPort="8910" EndpointRef="Endpoint1"/>
          </ContainerHostPolicies>
        </Policies>
      </ServiceManifestImport>
    </ApplicationManifest>
    ```
<span data-ttu-id="9d6ae-138">Você pode misturar e combinar modos de rede diferentes nos serviços dentro de um aplicativo para um cluster do Windows.</span><span class="sxs-lookup"><span data-stu-id="9d6ae-138">You can mix and match different networking modes across services within an application for a Windows cluster.</span></span> <span data-ttu-id="9d6ae-139">Assim, alguns serviços podem ficar no modo `open`, e outros no modo de rede `nat`.</span><span class="sxs-lookup"><span data-stu-id="9d6ae-139">Thus, you can have some services on `open` mode and some on `nat` networking mode.</span></span> <span data-ttu-id="9d6ae-140">Quando um serviço é configurado com `nat`, porta Olá é toomust escuta ser exclusivo.</span><span class="sxs-lookup"><span data-stu-id="9d6ae-140">When a service is configured with `nat`, hello port it is listening toomust be unique.</span></span> <span data-ttu-id="9d6ae-141">Não há suporte para a combinação de modos de rede para serviços diferentes em clusters do Linux.</span><span class="sxs-lookup"><span data-stu-id="9d6ae-141">Mixing networking modes for different services isn't supported on Linux clusters.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="9d6ae-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9d6ae-142">Next steps</span></span>
<span data-ttu-id="9d6ae-143">Neste artigo, você aprendeu sobre modos de rede oferecidos pelo Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="9d6ae-143">In this article, you learned about networking modes offered by Service Fabric.</span></span>  

* [<span data-ttu-id="9d6ae-144">Modelo de aplicativo da Malha do Serviço</span><span class="sxs-lookup"><span data-stu-id="9d6ae-144">Service Fabric application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="9d6ae-145">Recursos do manifesto do serviço Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9d6ae-145">Service Fabric service manifest resources</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="9d6ae-146">Implantar um contêiner de Windows tooService malha no Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="9d6ae-146">Deploy a Windows container tooService Fabric on Windows Server 2016</span></span>](service-fabric-get-started-containers.md)
* [<span data-ttu-id="9d6ae-147">Implantar um contêiner de Docker tooService malha no Linux</span><span class="sxs-lookup"><span data-stu-id="9d6ae-147">Deploy a Docker container tooService Fabric on Linux</span></span>](service-fabric-get-started-containers-linux.md)
