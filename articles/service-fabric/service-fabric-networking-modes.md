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
# <a name="service-fabric-container-networking-modes"></a>Modos de rede de contêiner do Service Fabric

Hello modo de rede padrão oferecidos em Olá malha do serviço de cluster para serviços de contêiner é hello `nat` modo de rede. Com hello `nat` modo, ter mais de um toohello contêineres de escuta de serviço de rede da mesma porta resulta em erros de implantação. Para executar vários serviços de escutam Olá dá suporte a mesma porta do Service Fabric Olá `open` modo de rede (versão 5.7 ou superior). Com hello `open` modo de acesso à rede, cada serviço de contêiner é um endereço IP atribuído dinamicamente, permitindo internamente toohello de toolisten vários serviços a mesma porta.   

Assim, com um único tipo de serviço com um ponto de extremidade estático definido no manifesto do serviço Olá, novos serviços podem ser criados e excluídos sem erros de implantação usando Olá `open` modo de rede. Da mesma forma, você pode usar Olá mesmo `docker-compose.yml` arquivo com mapeamentos de porta estática para a criação de vários serviços.

Usar Olá atribuído dinamicamente IP toodiscover services não é aconselhável desde alterações de endereço IP hello quando o serviço de saudação é reiniciado ou move tooanother nó. Use somente Olá **Service Fabric Naming Service** ou hello **serviço DNS** para descoberta de serviço. 


> [!WARNING]
> Só há permissão para um total de 4096 IPs por rede virtual no Azure. Assim, soma de saudação do número de saudação de nós e Olá contêiner de instâncias de serviço (com `open` rede) não pode exceder 4096 dentro de uma rede virtual. Para esses cenários de alta densidade, Olá `nat` rede é recomendado.
>

## <a name="setting-up-open-networking-mode"></a>Configurar o modo de rede aberto

1. Configurar modelo do Azure Resource Manager hello, permitindo que o serviço DNS e Olá provedor de IP em `fabricSettings`. 

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

2. Configure o perfil de rede de saudação seção tooallow toobe configurado em cada nó do cluster de saudação de endereços de IP de vários. Olá exemplo a seguir define cinco endereços IP por nó (, portanto, você pode ter cinco instâncias de serviço escutando a porta toohello em cada nó) para um cluster do Windows Service Fabric.

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

    Para clusters do Linux, uma configuração de IP pública adicional é adicionada tooallow conectividade de saída. Olá trecho a seguir configura a cinco endereços IP por nó de um cluster do Linux:

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

3. Para Windows clusters somente, configurar um NSG regra abrindo a porta UDP/53 para a rede virtual de saudação com hello valores a seguir:

   | Prioridade |    Nome    |    Fonte      |  Destino   |   O Barramento de    | Ação |
   |:--------:|:----------:|:--------------:|:--------------:|:------------:|:------:|
   |     2000 | Custom_Dns | VirtualNetwork | VirtualNetwork | DNS (UDP/53) | PERMITIR  |


4. Especifique o modo de rede Olá no manifesto de aplicativo hello para cada serviço `<NetworkConfig NetworkType="open">`.  modo de saudação `open` resulta em serviço Olá obtendo um endereço IP dedicado. Se um modo não for especificado, o padrão é toohello básica `nat` modo. Assim, em Olá seguinte exemplo de manifesto, `NodeContainerServicePackage1` e `NodeContainerServicePackage2` pode cada toohello escuta mesma porta (os dois serviços estão escutando em `Endpoint1`).

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
Você pode misturar e combinar modos de rede diferentes nos serviços dentro de um aplicativo para um cluster do Windows. Assim, alguns serviços podem ficar no modo `open`, e outros no modo de rede `nat`. Quando um serviço é configurado com `nat`, porta Olá é toomust escuta ser exclusivo. Não há suporte para a combinação de modos de rede para serviços diferentes em clusters do Linux. 


## <a name="next-steps"></a>Próximas etapas
Neste artigo, você aprendeu sobre modos de rede oferecidos pelo Service Fabric.  

* [Modelo de aplicativo da Malha do Serviço](service-fabric-application-model.md)
* [Recursos do manifesto do serviço Service Fabric](service-fabric-application-model.md)
* [Implantar um contêiner de Windows tooService malha no Windows Server 2016](service-fabric-get-started-containers.md)
* [Implantar um contêiner de Docker tooService malha no Linux](service-fabric-get-started-containers-linux.md)
