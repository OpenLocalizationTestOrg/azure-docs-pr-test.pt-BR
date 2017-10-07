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
# <a name="network-resource-provider"></a><span data-ttu-id="85418-103">Provedor de recursos de rede</span><span class="sxs-lookup"><span data-stu-id="85418-103">Network Resource Provider</span></span>
<span data-ttu-id="85418-104">Uma necessidade de base no sucesso nos negócios atuais, é Olá toobuild de capacidade e gerenciar aplicativos com reconhecimento de rede de grande escala de uma maneira ágil, flexível, segura e reproduzível.</span><span class="sxs-lookup"><span data-stu-id="85418-104">An underpinning need in today’s business success, is hello ability toobuild and manage large scale network aware applications in an agile, flexible, secure and repeatable way.</span></span> <span data-ttu-id="85418-105">Gerenciador de recursos do Azure permite que você toocreate aplicativos, como um único conjunto de recursos em grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="85418-105">Azure Resource Manager enables you toocreate such applications, as a single collection of resources in resource groups.</span></span> <span data-ttu-id="85418-106">Esses recursos são gerenciados por meio de vários provedores de recursos no Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="85418-106">Such resources are managed through various resource providers under Resource Manager.</span></span>

<span data-ttu-id="85418-107">Gerenciador de recursos do Azure depende de outro recurso provedores tooprovide acessar tooyour os recursos.</span><span class="sxs-lookup"><span data-stu-id="85418-107">Azure Resource Manager relies on different resource providers tooprovide access tooyour resources.</span></span> <span data-ttu-id="85418-108">Existem três provedores de recurso principais: Rede, Armazenamento e Computação.</span><span class="sxs-lookup"><span data-stu-id="85418-108">There are three main resource providers: Network, Storage and Compute.</span></span> <span data-ttu-id="85418-109">Este documento aborda as características de saudação e os benefícios de saudação provedor de recursos de rede, incluindo:</span><span class="sxs-lookup"><span data-stu-id="85418-109">This document discusses hello characteristics and benefits of hello Network Resource Provider, including:</span></span>

* <span data-ttu-id="85418-110">**Metadados** – você pode adicionar informações tooresources usando marcas.</span><span class="sxs-lookup"><span data-stu-id="85418-110">**Metadata** – you can add information tooresources using tags.</span></span> <span data-ttu-id="85418-111">Essas marcas podem ser usadas tootrack utilização de recursos entre assinaturas e os grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="85418-111">These tags can be used tootrack resource utilization across resource groups and subscriptions.</span></span>
* <span data-ttu-id="85418-112">**Maior controle da sua rede** - recursos de rede são flexíveis e você pode controlá-los de forma mais granular.</span><span class="sxs-lookup"><span data-stu-id="85418-112">**Greater control of your network** - network resources are loosely coupled and you can control them in a more granular fashion.</span></span> <span data-ttu-id="85418-113">Isso significa que você tem mais flexibilidade no gerenciamento de recursos de rede hello.</span><span class="sxs-lookup"><span data-stu-id="85418-113">This means you have more flexibility in managing hello networking resources.</span></span>
* <span data-ttu-id="85418-114">**Configuração mais rápida** - já que os recursos de rede são agrupados de modo menos rígido, você pode criar e organizar os recursos de rede em paralelo.</span><span class="sxs-lookup"><span data-stu-id="85418-114">**Faster configuration** - because network resources are loosely coupled, you can create and orchestrate network resources in parallel.</span></span> <span data-ttu-id="85418-115">Isso reduziu drasticamente o tempo de configuração.</span><span class="sxs-lookup"><span data-stu-id="85418-115">This has drastically reduced configuration time.</span></span>
* <span data-ttu-id="85418-116">**Controle de acesso baseado em função** -RBAC oferece funções padrão, o escopo de segurança específico, na criação de saudação tooallowing adição de funções personalizadas para o gerenciamento de proteção.</span><span class="sxs-lookup"><span data-stu-id="85418-116">**Role Based Access Control** - RBAC provides default roles, with specific security scope, in addition tooallowing hello creation of custom roles for secure management.</span></span>
* <span data-ttu-id="85418-117">**Implantação e gerenciamento mais fácil** -é mais fácil toodeploy e gerenciar aplicativos, pois pode ser que você pode criar uma pilha de todo o aplicativo como um único conjunto de recursos em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="85418-117">**Easier management and deployment** - it’s easier toodeploy and manage applications since you can can create an entire application stack as a single collection of resources in a resource group.</span></span> <span data-ttu-id="85418-118">E toodeploy mais rápido, pois você pode implantar, simplesmente fornecendo uma carga JSON do modelo.</span><span class="sxs-lookup"><span data-stu-id="85418-118">And faster toodeploy, since you can deploy by simply providing a template JSON payload.</span></span>
* <span data-ttu-id="85418-119">**Personalização rápida** -você pode usar modelos de estilo declarativo tooenable repetível e rápido personalização das implantações.</span><span class="sxs-lookup"><span data-stu-id="85418-119">**Rapid customization** - you can use declarative-style templates tooenable repeatable and rapid customization of deployments.</span></span>
* <span data-ttu-id="85418-120">**Personalização REPEATABLE** -você pode usar modelos de estilo declarativo tooenable repetível e rápido personalização das implantações.</span><span class="sxs-lookup"><span data-stu-id="85418-120">**Repeatable customization** - you can use declarative-style templates tooenable repeatable and rapid customization of deployments.</span></span>
* <span data-ttu-id="85418-121">**Interfaces de gerenciamento** -você pode usar seus recursos para qualquer Olá toomanage interfaces a seguir:</span><span class="sxs-lookup"><span data-stu-id="85418-121">**Management interfaces** - you can use any of hello following interfaces toomanage your resources:</span></span>
  * <span data-ttu-id="85418-122">API baseada em REST</span><span class="sxs-lookup"><span data-stu-id="85418-122">REST based API</span></span>
  * <span data-ttu-id="85418-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="85418-123">PowerShell</span></span>
  * <span data-ttu-id="85418-124">SDK .NET</span><span class="sxs-lookup"><span data-stu-id="85418-124">.NET SDK</span></span>
  * <span data-ttu-id="85418-125">SDK do Node.JS</span><span class="sxs-lookup"><span data-stu-id="85418-125">Node.JS SDK</span></span>
  * <span data-ttu-id="85418-126">Java SDK</span><span class="sxs-lookup"><span data-stu-id="85418-126">Java SDK</span></span>
  * <span data-ttu-id="85418-127">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="85418-127">Azure CLI</span></span>
  * <span data-ttu-id="85418-128">Portal de Visualização</span><span class="sxs-lookup"><span data-stu-id="85418-128">Preview Portal</span></span>
  * <span data-ttu-id="85418-129">Linguagem de modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="85418-129">Resource Manager template language</span></span>

## <a name="network-resources"></a><span data-ttu-id="85418-130">Recursos de rede</span><span class="sxs-lookup"><span data-stu-id="85418-130">Network resources</span></span>
<span data-ttu-id="85418-131">Agora você pode gerenciar recursos de rede de modo independente, em vez de ter todos eles gerenciados por meio de um recurso de computação único (uma máquina virtual).</span><span class="sxs-lookup"><span data-stu-id="85418-131">You can now manage network resources independently, instead of having them all managed through a single compute resource (a virtual machine).</span></span> <span data-ttu-id="85418-132">Isso garante um maior grau de flexibilidade e agilidade em redigir uma infraestrutura complexa e em grande escala em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="85418-132">This ensures a higher degree of flexibility and agility in composing a complex and large scale infrastructure in a resource group.</span></span>

<span data-ttu-id="85418-133">Uma exibição conceitual de uma implantação de exemplo envolvendo um aplicativo de várias camadas é apresentado a seguir.</span><span class="sxs-lookup"><span data-stu-id="85418-133">A conceptual view of a sample deployment involving a multi-tiered application is presented below.</span></span> <span data-ttu-id="85418-134">Cada recurso que você vê, como NICs, endereços IP públicos e VMs, pode ser gerenciado independentemente.</span><span class="sxs-lookup"><span data-stu-id="85418-134">Each resource you see, such as NICs, public IP addresses, and VMs, can be managed independently.</span></span>

![Modelo de recursos de rede](./media/resource-groups-networking/Figure2.png)

<span data-ttu-id="85418-136">Cada recurso contém um conjunto comum de propriedades e seu conjunto de propriedades individuais.</span><span class="sxs-lookup"><span data-stu-id="85418-136">Every resource contains a common set of properties, and their individual property set.</span></span> <span data-ttu-id="85418-137">Olá as propriedades comuns são:</span><span class="sxs-lookup"><span data-stu-id="85418-137">hello common properties are:</span></span>

| <span data-ttu-id="85418-138">Propriedade</span><span class="sxs-lookup"><span data-stu-id="85418-138">Property</span></span> | <span data-ttu-id="85418-139">Descrição</span><span class="sxs-lookup"><span data-stu-id="85418-139">Description</span></span> | <span data-ttu-id="85418-140">Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="85418-140">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="85418-141">**name**</span><span class="sxs-lookup"><span data-stu-id="85418-141">**name**</span></span> |<span data-ttu-id="85418-142">Nome de recurso exclusivo.</span><span class="sxs-lookup"><span data-stu-id="85418-142">Unique resource name.</span></span> <span data-ttu-id="85418-143">Cada tipo de recurso tem suas próprias restrições de nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="85418-143">Each resource type has its own naming restrictions.</span></span> |<span data-ttu-id="85418-144">PIP01, VM01, NIC01</span><span class="sxs-lookup"><span data-stu-id="85418-144">PIP01, VM01, NIC01</span></span> |
| <span data-ttu-id="85418-145">**local**</span><span class="sxs-lookup"><span data-stu-id="85418-145">**location**</span></span> |<span data-ttu-id="85418-146">Região do Azure no qual Olá recurso reside</span><span class="sxs-lookup"><span data-stu-id="85418-146">Azure region in which hello resource resides</span></span> |<span data-ttu-id="85418-147">westus, eastus</span><span class="sxs-lookup"><span data-stu-id="85418-147">westus, eastus</span></span> |
| <span data-ttu-id="85418-148">**ID**</span><span class="sxs-lookup"><span data-stu-id="85418-148">**id**</span></span> |<span data-ttu-id="85418-149">Identificação baseada em URI exclusivo</span><span class="sxs-lookup"><span data-stu-id="85418-149">Unique URI based identification</span></span> |<span data-ttu-id="85418-150">/subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP</span><span class="sxs-lookup"><span data-stu-id="85418-150">/subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP</span></span> |

<span data-ttu-id="85418-151">Você pode verificar as propriedades individuais de saudação do recursos nas seções de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="85418-151">You can check hello individual properties of resources in hello sections below.</span></span>

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

## <a name="management-interfaces"></a><span data-ttu-id="85418-152">Interfaces de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="85418-152">Management interfaces</span></span>
<span data-ttu-id="85418-153">Você pode gerenciar os recursos de rede do Azure usando interfaces diferentes.</span><span class="sxs-lookup"><span data-stu-id="85418-153">You can manage your Azure networking resources using different interfaces.</span></span> <span data-ttu-id="85418-154">Neste documento, vamos nos concentrar em duas dessas interfaces: API REST e modelos.</span><span class="sxs-lookup"><span data-stu-id="85418-154">In this document we will focus on tow of those interfaces: REST API, and templates.</span></span>

### <a name="rest-api"></a><span data-ttu-id="85418-155">API REST</span><span class="sxs-lookup"><span data-stu-id="85418-155">REST API</span></span>
<span data-ttu-id="85418-156">Como mencionado anteriormente, os recursos de rede podem ser gerenciados por meio de uma variedade de interfaces, inclusive API REST, o SDK do .NET, SDK do Node.JS, Java SDK, PowerShell, CLI, Portal do Azure e modelos.</span><span class="sxs-lookup"><span data-stu-id="85418-156">As mentioned earlier, network resources can be managed via a variety of interfaces, including REST API,.NET SDK, Node.JS SDK, Java SDK, PowerShell, CLI, Azure Portal and templates.</span></span>

<span data-ttu-id="85418-157">API de Rest a saudação obedecer toohello especificação do protocolo HTTP 1.1.</span><span class="sxs-lookup"><span data-stu-id="85418-157">hello Rest API’s conform toohello HTTP 1.1 protocol specification.</span></span> <span data-ttu-id="85418-158">estrutura geral de URI Olá de saudação API é apresentada a seguir:</span><span class="sxs-lookup"><span data-stu-id="85418-158">hello general URI structure of hello API is presented below:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}/providers/{resource-provider-namespace}/locations/{region-location}/register?api-version={api-version}

<span data-ttu-id="85418-159">E parâmetros de saudação chaves representam Olá elementos a seguir:</span><span class="sxs-lookup"><span data-stu-id="85418-159">And hello parameters in braces represent hello following elements:</span></span>

* <span data-ttu-id="85418-160">**subscription-id** - a ID de sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="85418-160">**subscription-id** - your Azure subscription id.</span></span>
* <span data-ttu-id="85418-161">**namespace do provedor de recursos** -namespace para o provedor de hello está sendo usado.</span><span class="sxs-lookup"><span data-stu-id="85418-161">**resource-provider-namespace** - namespace for hello provider being used.</span></span> <span data-ttu-id="85418-162">provedor de recursos de rede Olá Olá valor é *Network*.</span><span class="sxs-lookup"><span data-stu-id="85418-162">hello value for hello network resource provider is *Microsoft.Network*.</span></span>
* <span data-ttu-id="85418-163">**nome da região** -nome da região do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="85418-163">**region-name** - hello Azure region name</span></span>

<span data-ttu-id="85418-164">métodos HTTP seguir Hello têm suporte ao fazer chamadas toohello API REST:</span><span class="sxs-lookup"><span data-stu-id="85418-164">hello following HTTP methods are supported when making calls toohello REST API:</span></span>

* <span data-ttu-id="85418-165">**COLOCAR** - usadas toocreate um recurso de um determinado tipo, modificar uma propriedade de recurso ou alterar uma associação entre os recursos.</span><span class="sxs-lookup"><span data-stu-id="85418-165">**PUT** - used toocreate a resource of a given type, modify a resource property or change an association between resources.</span></span>
* <span data-ttu-id="85418-166">**OBTER** -usado tooretrieve informações para um recurso de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="85418-166">**GET** - used tooretrieve information for a provisioned resource.</span></span>
* <span data-ttu-id="85418-167">**Excluir** -usado toodelete um recurso existente.</span><span class="sxs-lookup"><span data-stu-id="85418-167">**DELETE** - used toodelete an existing resource.</span></span>

<span data-ttu-id="85418-168">Saudação de solicitação e de resposta em conformidade tooa formato de carga JSON.</span><span class="sxs-lookup"><span data-stu-id="85418-168">Both hello request and response conform tooa JSON payload format.</span></span> <span data-ttu-id="85418-169">Para obter mais detalhes, consulte [APIs de Gerenciamento de Recursos do Azure](https://msdn.microsoft.com/library/azure/dn948464.aspx).</span><span class="sxs-lookup"><span data-stu-id="85418-169">For more details, see [Azure Resource Management APIs](https://msdn.microsoft.com/library/azure/dn948464.aspx).</span></span>

### <a name="resource-manager-template-language"></a><span data-ttu-id="85418-170">Linguagem de modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="85418-170">Resource Manager template language</span></span>
<span data-ttu-id="85418-171">Em recursos de toomanaging adição imperativa (por meio de APIs ou SDK), também pode usar um toobuild de estilo de programação declarativa e gerenciar recursos de rede usando Olá Gerenciador de recursos de linguagem de modelo.</span><span class="sxs-lookup"><span data-stu-id="85418-171">In addition toomanaging resources imperatively (via APIs or SDK), you can also use a declarative programming style toobuild and manage network resources by using hello Resource Manager Template Language.</span></span>

<span data-ttu-id="85418-172">Uma representação de um modelo de exemplo é fornecida abaixo -</span><span class="sxs-lookup"><span data-stu-id="85418-172">A sample representation of a template is provided below –</span></span>

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "<version-number-of-template>",
      "parameters": { <parameter-definitions-of-template> },
      "variables": { <variable-definitions-of-template> },
      "resources": [ { <definition-of-resource-to-deploy> } ],
      "outputs": { <output-of-template> }    
    }

<span data-ttu-id="85418-173">modelo de saudação é principalmente uma descrição JSON dos recursos de saudação e valores de instância Olá injetados por meio de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="85418-173">hello template is primarily a JSON description of hello resources and hello instance values injected via parameters.</span></span> <span data-ttu-id="85418-174">exemplo Hello abaixo pode ser usado toocreate uma rede virtual com 2 sub-redes.</span><span class="sxs-lookup"><span data-stu-id="85418-174">hello example below can be used toocreate a virtual network with 2 subnets.</span></span>

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

<span data-ttu-id="85418-175">Você tem a opção de saudação do fornecimento de valores de parâmetro hello manualmente ao usar um modelo, ou você pode usar um arquivo de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="85418-175">You have hello option of providing hello parameter values manually when using a template, or you can use a parameter file.</span></span> <span data-ttu-id="85418-176">exemplo Hello abaixo mostra um conjunto de possíveis de toobe de valores de parâmetro usado com o modelo de saudação acima:</span><span class="sxs-lookup"><span data-stu-id="85418-176">hello example below shows a possible set of parameter values toobe used with hello template above:</span></span>

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


<span data-ttu-id="85418-177">Olá principais vantagens de usar os modelos são:</span><span class="sxs-lookup"><span data-stu-id="85418-177">hello main advantages of using templates are:</span></span>

* <span data-ttu-id="85418-178">Você pode criar uma infraestrutura complexa em um grupo de recursos em um estilo declarativo.</span><span class="sxs-lookup"><span data-stu-id="85418-178">You can build a complex infrastructure in a resource group in a declarative style.</span></span> <span data-ttu-id="85418-179">Olá orquestração de criação de recursos hello, incluindo o gerenciamento de dependência é tratada pelo Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="85418-179">hello orchestration of creating hello resources, including dependency management, is handled by Resource Manager.</span></span>
* <span data-ttu-id="85418-180">infraestrutura de saudação pode ser criada de forma repetida por várias regiões e dentro de uma região, simplesmente alterando os parâmetros.</span><span class="sxs-lookup"><span data-stu-id="85418-180">hello infrastructure can be created in a repeatable way across various regions and within a region by simply changing parameters.</span></span>
* <span data-ttu-id="85418-181">estilo declarativo Olá leva prazo tooshorter na criação de modelos de saudação e implantação de infraestrutura de saudação.</span><span class="sxs-lookup"><span data-stu-id="85418-181">hello declarative style leads tooshorter lead time in building hello templates and rolling out hello infrastructure.</span></span>

<span data-ttu-id="85418-182">Para exemplos de modelo, consulte [Modelos de início rápido do Azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="85418-182">For sample templates, see [Azure quickstart templates](https://github.com/Azure/azure-quickstart-templates).</span></span>

<span data-ttu-id="85418-183">Para obter mais informações sobre Olá Gerenciador de recursos de linguagem de modelo, consulte [linguagem de modelo do Gerenciador de recursos do Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="85418-183">For more information on hello Resource Manager Template Language, see [Azure Resource Manager Template Language](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="85418-184">o modelo de saudação de exemplo acima usa Olá uma rede virtual e recursos de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="85418-184">hello sample template above uses hello virtual network and subnet resources.</span></span> <span data-ttu-id="85418-185">Há outros recursos de rede, que você pode usar, conforme listado abaixo:</span><span class="sxs-lookup"><span data-stu-id="85418-185">There are other network resources you can use as listed below:</span></span>

### <a name="using-a-template"></a><span data-ttu-id="85418-186">Criação de um modelo</span><span class="sxs-lookup"><span data-stu-id="85418-186">Using a template</span></span>
<span data-ttu-id="85418-187">Você pode implantar serviços tooAzure de um modelo usando o PowerShell, AzureCLI, ou executando um toodeploy clique do GitHub.</span><span class="sxs-lookup"><span data-stu-id="85418-187">You can deploy services tooAzure from a template by using PowerShell, AzureCLI, or by performing a click toodeploy from GitHub.</span></span> <span data-ttu-id="85418-188">serviços toodeploy de um modelo no GitHub, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="85418-188">toodeploy services from a template in GitHub, execute hello following steps:</span></span>

1. <span data-ttu-id="85418-189">Abra o arquivo de template3 de saudação do GitHub.</span><span class="sxs-lookup"><span data-stu-id="85418-189">Open hello template3 file from GitHub.</span></span> <span data-ttu-id="85418-190">Por exemplo, abra a rede Virtual do [com duas sub-redes](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="85418-190">As an example, open [Virtual network with two subnets](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).</span></span>
2. <span data-ttu-id="85418-191">Clique em **implantar tooAzure**e, em seguida, entre em toohello portal do Azure com suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="85418-191">Click on **Deploy tooAzure**, and then sign in on toohello Azure portal with your credentials.</span></span>
3. <span data-ttu-id="85418-192">Verifique se o modelo de saudação e, em seguida, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="85418-192">Verify hello template, and then click **Save**.</span></span>
4. <span data-ttu-id="85418-193">Clique em **Editar parâmetros** e selecione um local, como *Oeste dos EUA*, Olá redes e sub-redes.</span><span class="sxs-lookup"><span data-stu-id="85418-193">Click **Edit parameters** and select a location, such as *West US*, for hello vnet and subnets.</span></span>
5. <span data-ttu-id="85418-194">Se necessário, altere Olá **ADDRESSPREFIX** e **SUBNETPREFIX** parâmetros e clique **Okey**.</span><span class="sxs-lookup"><span data-stu-id="85418-194">If necessary, change hello **ADDRESSPREFIX** and **SUBNETPREFIX** parameters, and then click **OK**.</span></span>
6. <span data-ttu-id="85418-195">Clique em **selecionar um grupo de recursos** e, em seguida, clique no grupo de recursos de saudação deseja tooadd Olá redes e sub-redes.</span><span class="sxs-lookup"><span data-stu-id="85418-195">Click **Select a resource group** and then click on hello resource group you want tooadd hello vnet and subnets to.</span></span> <span data-ttu-id="85418-196">Como alternativa, você pode criar um novo grupo de recursos clicando **Ou criar novos**.</span><span class="sxs-lookup"><span data-stu-id="85418-196">Alternatively, you can create a new resource group by clicking **Or create new**.</span></span>
7. <span data-ttu-id="85418-197">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="85418-197">Click **Create**.</span></span> <span data-ttu-id="85418-198">Observe Olá bloco exibindo **implantação de modelo de provisionamento**.</span><span class="sxs-lookup"><span data-stu-id="85418-198">Notice hello tile displaying **Provisioning Template deployment**.</span></span> <span data-ttu-id="85418-199">Depois de implantação hello, você verá um tooone semelhante de tela abaixo.</span><span class="sxs-lookup"><span data-stu-id="85418-199">Once hello deployment is done, you will see a screen similar tooone below.</span></span>

![Implantação do modelo de exemplo](./media/resource-groups-networking/Figure6.png)

## <a name="next-steps"></a><span data-ttu-id="85418-201">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="85418-201">Next steps</span></span>
[<span data-ttu-id="85418-202">Idioma de modelo do Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="85418-202">Azure Resource Manager Template Language</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[<span data-ttu-id="85418-203">Rede do Azure - modelos usados frequentemente</span><span class="sxs-lookup"><span data-stu-id="85418-203">Azure Networking – commonly used templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

[<span data-ttu-id="85418-204">Azure Resource Manager vs implantação clássica</span><span class="sxs-lookup"><span data-stu-id="85418-204">Azure Resource Manager vs. classic deployment</span></span>](../azure-resource-manager/resource-manager-deployment-model.md)

[<span data-ttu-id="85418-205">Visão geral do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="85418-205">Azure Resource Manager Overview</span></span>](../azure-resource-manager/resource-group-overview.md)

