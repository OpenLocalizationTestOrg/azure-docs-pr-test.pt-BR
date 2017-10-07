---
title: "Visão geral do provedor de recursos de aaaNetwork | Microsoft Docs"
description: "Saiba mais sobre Olá novo provedor de recursos de rede no Gerenciador de recursos do Azure"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 79bf09da-4809-45cb-8d21-705616ef24dc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: 81b8f51fe8ee180d8f7885c6e04eb953904d7be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="network-resource-provider"></a>Provedor de recursos de rede
Uma necessidade de base no sucesso nos negócios atuais, é Olá toobuild de capacidade e gerenciar aplicativos com reconhecimento de rede de grande escala de uma maneira ágil, flexível, segura e reproduzível. Gerenciador de recursos do Azure permite que você toocreate aplicativos, como um único conjunto de recursos em grupos de recursos. Esses recursos são gerenciados por meio de vários provedores de recursos no Resource Manager.

Gerenciador de recursos do Azure depende de outro recurso provedores tooprovide acessar tooyour os recursos. Existem três provedores de recurso principais: Rede, Armazenamento e Computação. Este documento aborda as características de saudação e os benefícios de saudação provedor de recursos de rede, incluindo:

* **Metadados** – você pode adicionar informações tooresources usando marcas. Essas marcas podem ser usadas tootrack utilização de recursos entre assinaturas e os grupos de recursos.
* **Maior controle da sua rede** - recursos de rede são flexíveis e você pode controlá-los de forma mais granular. Isso significa que você tem mais flexibilidade no gerenciamento de recursos de rede hello.
* **Configuração mais rápida** - já que os recursos de rede são agrupados de modo menos rígido, você pode criar e organizar os recursos de rede em paralelo. Isso reduziu drasticamente o tempo de configuração.
* **Controle de acesso baseado em função** -RBAC oferece funções padrão, o escopo de segurança específico, na criação de saudação tooallowing adição de funções personalizadas para o gerenciamento de proteção.
* **Implantação e gerenciamento mais fácil** -é mais fácil toodeploy e gerenciar aplicativos, pois pode ser que você pode criar uma pilha de todo o aplicativo como um único conjunto de recursos em um grupo de recursos. E toodeploy mais rápido, pois você pode implantar, simplesmente fornecendo uma carga JSON do modelo.
* **Personalização rápida** -você pode usar modelos de estilo declarativo tooenable repetível e rápido personalização das implantações.
* **Personalização REPEATABLE** -você pode usar modelos de estilo declarativo tooenable repetível e rápido personalização das implantações.
* **Interfaces de gerenciamento** -você pode usar seus recursos para qualquer Olá toomanage interfaces a seguir:
  * API baseada em REST
  * PowerShell
  * SDK .NET
  * SDK do Node.JS
  * Java SDK
  * CLI do Azure
  * Portal de Visualização
  * Linguagem de modelo do Resource Manager

## <a name="network-resources"></a>Recursos de rede
Agora você pode gerenciar recursos de rede de modo independente, em vez de ter todos eles gerenciados por meio de um recurso de computação único (uma máquina virtual). Isso garante um maior grau de flexibilidade e agilidade em redigir uma infraestrutura complexa e em grande escala em um grupo de recursos.

Uma exibição conceitual de uma implantação de exemplo envolvendo um aplicativo de várias camadas é apresentado a seguir. Cada recurso que você vê, como NICs, endereços IP públicos e VMs, pode ser gerenciado independentemente.

![Modelo de recursos de rede](./media/resource-groups-networking/Figure2.png)

Cada recurso contém um conjunto comum de propriedades e seu conjunto de propriedades individuais. Olá as propriedades comuns são:

| Propriedade | Descrição | Valores de exemplo |
| --- | --- | --- |
| **name** |Nome de recurso exclusivo. Cada tipo de recurso tem suas próprias restrições de nomenclatura. |PIP01, VM01, NIC01 |
| **local** |Região do Azure no qual Olá recurso reside |westus, eastus |
| **ID** |Identificação baseada em URI exclusivo |/subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP |

Você pode verificar as propriedades individuais de saudação do recursos nas seções de saudação abaixo.

[!INCLUDE [virtual-networks-nrp-pip-include](../../includes/virtual-networks-nrp-pip-include.md)]

[!INCLUDE [virtual-networks-nrp-nic-include](../../includes/virtual-networks-nrp-nic-include.md)]

[!INCLUDE [virtual-networks-nrp-nsg-include](../../includes/virtual-networks-nrp-nsg-include.md)]

[!INCLUDE [virtual-networks-nrp-udr-include](../../includes/virtual-networks-nrp-udr-include.md)]

[!INCLUDE [virtual-networks-nrp-vnet-include](../../includes/virtual-networks-nrp-vnet-include.md)]

[!INCLUDE [virtual-networks-nrp-dns-include](../../includes/virtual-networks-nrp-dns-include.md)]

[!INCLUDE [virtual-networks-nrp-lb-include](../../includes/virtual-networks-nrp-lb-include.md)]

[!INCLUDE [virtual-networks-nrp-appgw-include](../../includes/virtual-networks-nrp-appgw-include.md)]

[!INCLUDE [virtual-networks-nrp-vpn-include](../../includes/virtual-networks-nrp-vpn-include.md)]

[!INCLUDE [virtual-networks-nrp-tm-include](../../includes/virtual-networks-nrp-tm-include.md)]

## <a name="management-interfaces"></a>Interfaces de gerenciamento
Você pode gerenciar os recursos de rede do Azure usando interfaces diferentes. Neste documento, vamos nos concentrar em duas dessas interfaces: API REST e modelos.

### <a name="rest-api"></a>API REST
Como mencionado anteriormente, os recursos de rede podem ser gerenciados por meio de uma variedade de interfaces, inclusive API REST, o SDK do .NET, SDK do Node.JS, Java SDK, PowerShell, CLI, Portal do Azure e modelos.

API de Rest a saudação obedecer toohello especificação do protocolo HTTP 1.1. estrutura geral de URI Olá de saudação API é apresentada a seguir:

    https://management.azure.com/subscriptions/{subscription-id}/providers/{resource-provider-namespace}/locations/{region-location}/register?api-version={api-version}

E parâmetros de saudação chaves representam Olá elementos a seguir:

* **subscription-id** - a ID de sua assinatura do Azure.
* **namespace do provedor de recursos** -namespace para o provedor de hello está sendo usado. provedor de recursos de rede Olá Olá valor é *Network*.
* **nome da região** -nome da região do Azure Olá

métodos HTTP seguir Hello têm suporte ao fazer chamadas toohello API REST:

* **COLOCAR** - usadas toocreate um recurso de um determinado tipo, modificar uma propriedade de recurso ou alterar uma associação entre os recursos.
* **OBTER** -usado tooretrieve informações para um recurso de provisionamento.
* **Excluir** -usado toodelete um recurso existente.

Saudação de solicitação e de resposta em conformidade tooa formato de carga JSON. Para obter mais detalhes, consulte [APIs de Gerenciamento de Recursos do Azure](https://msdn.microsoft.com/library/azure/dn948464.aspx).

### <a name="resource-manager-template-language"></a>Linguagem de modelo do Resource Manager
Em recursos de toomanaging adição imperativa (por meio de APIs ou SDK), também pode usar um toobuild de estilo de programação declarativa e gerenciar recursos de rede usando Olá Gerenciador de recursos de linguagem de modelo.

Uma representação de um modelo de exemplo é fornecida abaixo -

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "<version-number-of-template>",
      "parameters": { <parameter-definitions-of-template> },
      "variables": { <variable-definitions-of-template> },
      "resources": [ { <definition-of-resource-to-deploy> } ],
      "outputs": { <output-of-template> }    
    }

modelo de saudação é principalmente uma descrição JSON dos recursos de saudação e valores de instância Olá injetados por meio de parâmetros. exemplo Hello abaixo pode ser usado toocreate uma rede virtual com 2 sub-redes.

    {
        "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/VNET.json",
        "contentVersion": "1.0.0.0",
        "parameters" : {
          "location": {
            "type": "String",
            "allowedValues": ["East US", "West US", "West Europe", "East Asia", "South East Asia"],
            "metadata" : {
              "Description" : "Deployment location"
            }
          },
          "virtualNetworkName":{
            "type" : "string",
            "defaultValue":"myVNET",
            "metadata" : {
              "Description" : "VNET name"
            }
          },
          "addressPrefix":{
            "type" : "string",
            "defaultValue" : "10.0.0.0/16",
            "metadata" : {
              "Description" : "Address prefix"
            }

          },
          "subnet1Name": {
            "type" : "string",
            "defaultValue" : "Subnet-1",
            "metadata" : {
              "Description" : "Subnet 1 Name"
            }
          },
          "subnet2Name": {
            "type" : "string",
            "defaultValue" : "Subnet-2",
            "metadata" : {
              "Description" : "Subnet 2 name"
            }
          },
          "subnet1Prefix" : {
            "type" : "string",
            "defaultValue" : "10.0.0.0/24",
            "metadata" : {
              "Description" : "Subnet 1 Prefix"
            }
          },
          "subnet2Prefix" : {
            "type" : "string",
            "defaultValue" : "10.0.1.0/24",
            "metadata" : {
              "Description" : "Subnet 2 Prefix"
            }
          }
        },
        "resources": [
        {
          "apiVersion": "2015-05-01-preview",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "[parameters('virtualNetworkName')]",
          "location": "[parameters('location')]",
          "properties": {
            "addressSpace": {
              "addressPrefixes": [
                "[parameters('addressPrefix')]"
              ]
            },
            "subnets": [
              {
                "name": "[parameters('subnet1Name')]",
                "properties" : {
                  "addressPrefix": "[parameters('subnet1Prefix')]"
                }
              },
              {
                "name": "[parameters('subnet2Name')]",
                "properties" : {
                  "addressPrefix": "[parameters('subnet2Prefix')]"
                }
              }
            ]
          }
        }
        ]
    }

Você tem a opção de saudação do fornecimento de valores de parâmetro hello manualmente ao usar um modelo, ou você pode usar um arquivo de parâmetro. exemplo Hello abaixo mostra um conjunto de possíveis de toobe de valores de parâmetro usado com o modelo de saudação acima:

    {
      "location": {
          "value": "East US"
      },
      "virtualNetworkName": {
          "value": "VNET1"
      },
      "subnet1Name": {
          "value": "Subnet1"
      },
      "subnet2Name": {
          "value": "Subnet2"
      },
      "addressPrefix": {
          "value": "192.168.0.0/16"
      },
      "subnet1Prefix": {
          "value": "192.168.1.0/24"
      },
      "subnet2Prefix": {
          "value": "192.168.2.0/24"
      }
    }


Olá principais vantagens de usar os modelos são:

* Você pode criar uma infraestrutura complexa em um grupo de recursos em um estilo declarativo. Olá orquestração de criação de recursos hello, incluindo o gerenciamento de dependência é tratada pelo Gerenciador de recursos.
* infraestrutura de saudação pode ser criada de forma repetida por várias regiões e dentro de uma região, simplesmente alterando os parâmetros.
* estilo declarativo Olá leva prazo tooshorter na criação de modelos de saudação e implantação de infraestrutura de saudação.

Para exemplos de modelo, consulte [Modelos de início rápido do Azure](https://github.com/Azure/azure-quickstart-templates).

Para obter mais informações sobre Olá Gerenciador de recursos de linguagem de modelo, consulte [linguagem de modelo do Gerenciador de recursos do Azure](../azure-resource-manager/resource-group-authoring-templates.md).

o modelo de saudação de exemplo acima usa Olá uma rede virtual e recursos de sub-rede. Há outros recursos de rede, que você pode usar, conforme listado abaixo:

### <a name="using-a-template"></a>Criação de um modelo
Você pode implantar serviços tooAzure de um modelo usando o PowerShell, AzureCLI, ou executando um toodeploy clique do GitHub. serviços toodeploy de um modelo no GitHub, execute Olá etapas a seguir:

1. Abra o arquivo de template3 de saudação do GitHub. Por exemplo, abra a rede Virtual do [com duas sub-redes](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).
2. Clique em **implantar tooAzure**e, em seguida, entre em toohello portal do Azure com suas credenciais.
3. Verifique se o modelo de saudação e, em seguida, clique em **salvar**.
4. Clique em **Editar parâmetros** e selecione um local, como *Oeste dos EUA*, Olá redes e sub-redes.
5. Se necessário, altere Olá **ADDRESSPREFIX** e **SUBNETPREFIX** parâmetros e clique **Okey**.
6. Clique em **selecionar um grupo de recursos** e, em seguida, clique no grupo de recursos de saudação deseja tooadd Olá redes e sub-redes. Como alternativa, você pode criar um novo grupo de recursos clicando **Ou criar novos**.
7. Clique em **Criar**. Observe Olá bloco exibindo **implantação de modelo de provisionamento**. Depois de implantação hello, você verá um tooone semelhante de tela abaixo.

![Implantação do modelo de exemplo](./media/resource-groups-networking/Figure6.png)

## <a name="next-steps"></a>Próximas etapas
[Idioma de modelo do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-authoring-templates.md)

[Rede do Azure - modelos usados frequentemente](https://github.com/Azure/azure-quickstart-templates)

[Azure Resource Manager vs implantação clássica](../azure-resource-manager/resource-manager-deployment-model.md)

[Visão geral do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)

