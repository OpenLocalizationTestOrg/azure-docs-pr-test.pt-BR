---
title: "Visão geral do Provedor de recursos de rede | Microsoft Docs"
description: Saiba mais sobre o novo Provedor de recursos de rede no Gerenciador de Recursos do Azure
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
ms.openlocfilehash: 2428c707ddeed281fddd1e57bc5574603f0b9b1c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="network-resource-provider"></a><span data-ttu-id="48c1a-103">Provedor de recursos de rede</span><span class="sxs-lookup"><span data-stu-id="48c1a-103">Network Resource Provider</span></span>
<span data-ttu-id="48c1a-104">Uma necessidade básica para sucesso nos negócios de hoje é a capacidade de compilar e gerenciar aplicativos com reconhecimento de rede de grande escala de uma maneira ágil, flexível, segura e repetível.</span><span class="sxs-lookup"><span data-stu-id="48c1a-104">An underpinning need in today’s business success, is the ability to build and manage large scale network aware applications in an agile, flexible, secure and repeatable way.</span></span> <span data-ttu-id="48c1a-105">O Azure Resource Manager permite criar tais aplicativos como uma única coleção de recursos nos grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="48c1a-105">Azure Resource Manager enables you to create such applications, as a single collection of resources in resource groups.</span></span> <span data-ttu-id="48c1a-106">Esses recursos são gerenciados por meio de vários provedores de recursos no Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="48c1a-106">Such resources are managed through various resource providers under Resource Manager.</span></span>

<span data-ttu-id="48c1a-107">O Gerenciador de Recursos do Azure utiliza diferentes provedores de recursos para fornecer acesso a seus recursos.</span><span class="sxs-lookup"><span data-stu-id="48c1a-107">Azure Resource Manager relies on different resource providers to provide access to your resources.</span></span> <span data-ttu-id="48c1a-108">Existem três provedores de recurso principais: Rede, Armazenamento e Computação.</span><span class="sxs-lookup"><span data-stu-id="48c1a-108">There are three main resource providers: Network, Storage and Compute.</span></span> <span data-ttu-id="48c1a-109">Este documento aborda as características e os benefícios do Provedor de Recursos de Rede, incluindo:</span><span class="sxs-lookup"><span data-stu-id="48c1a-109">This document discusses the characteristics and benefits of the Network Resource Provider, including:</span></span>

* <span data-ttu-id="48c1a-110">**Metadados** – você pode adicionar informações aos recursos usando marcas.</span><span class="sxs-lookup"><span data-stu-id="48c1a-110">**Metadata** – you can add information to resources using tags.</span></span> <span data-ttu-id="48c1a-111">Essas marcas podem ser usadas para controlar a utilização de recursos em grupos de recursos e assinaturas.</span><span class="sxs-lookup"><span data-stu-id="48c1a-111">These tags can be used to track resource utilization across resource groups and subscriptions.</span></span>
* <span data-ttu-id="48c1a-112">**Maior controle da sua rede** - recursos de rede são flexíveis e você pode controlá-los de forma mais granular.</span><span class="sxs-lookup"><span data-stu-id="48c1a-112">**Greater control of your network** - network resources are loosely coupled and you can control them in a more granular fashion.</span></span> <span data-ttu-id="48c1a-113">Isso significa que você tem mais flexibilidade no gerenciamento de recursos de rede.</span><span class="sxs-lookup"><span data-stu-id="48c1a-113">This means you have more flexibility in managing the networking resources.</span></span>
* <span data-ttu-id="48c1a-114">**Configuração mais rápida** - já que os recursos de rede são agrupados de modo menos rígido, você pode criar e organizar os recursos de rede em paralelo.</span><span class="sxs-lookup"><span data-stu-id="48c1a-114">**Faster configuration** - because network resources are loosely coupled, you can create and orchestrate network resources in parallel.</span></span> <span data-ttu-id="48c1a-115">Isso reduziu drasticamente o tempo de configuração.</span><span class="sxs-lookup"><span data-stu-id="48c1a-115">This has drastically reduced configuration time.</span></span>
* <span data-ttu-id="48c1a-116">**Controle de acesso com base em função** - o RBAC fornece funções padrão, com escopo de segurança específico, além de permitir a criação de funções personalizadas para gerenciamento seguro.</span><span class="sxs-lookup"><span data-stu-id="48c1a-116">**Role Based Access Control** - RBAC provides default roles, with specific security scope, in addition to allowing the creation of custom roles for secure management.</span></span>
* <span data-ttu-id="48c1a-117">**Gerenciamento e implantação simplificados** - é mais fácil implantar e gerenciar aplicativos, já que você pode criar uma pilha com todo o aplicativo como uma única coleção de recursos em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="48c1a-117">**Easier management and deployment** - it’s easier to deploy and manage applications since you can can create an entire application stack as a single collection of resources in a resource group.</span></span> <span data-ttu-id="48c1a-118">E isso agiliza a implantação, pois você pode implantar simplesmente fornecendo uma carga JSON de modelo.</span><span class="sxs-lookup"><span data-stu-id="48c1a-118">And faster to deploy, since you can deploy by simply providing a template JSON payload.</span></span>
* <span data-ttu-id="48c1a-119">**Personalização rápida** - você pode usar modelos de estilo declarativo para habilitar a personalização repetível e rápida de implantações.</span><span class="sxs-lookup"><span data-stu-id="48c1a-119">**Rapid customization** - you can use declarative-style templates to enable repeatable and rapid customization of deployments.</span></span>
* <span data-ttu-id="48c1a-120">**Personalização repetível** - você pode usar modelos de estilo declarativo para habilitar a personalização repetível e rápida de implantações.</span><span class="sxs-lookup"><span data-stu-id="48c1a-120">**Repeatable customization** - you can use declarative-style templates to enable repeatable and rapid customization of deployments.</span></span>
* <span data-ttu-id="48c1a-121">**Interfaces de gerenciamento** - você pode usar qualquer uma das seguintes interfaces para gerenciar seus recursos:</span><span class="sxs-lookup"><span data-stu-id="48c1a-121">**Management interfaces** - you can use any of the following interfaces to manage your resources:</span></span>
  * <span data-ttu-id="48c1a-122">API baseada em REST</span><span class="sxs-lookup"><span data-stu-id="48c1a-122">REST based API</span></span>
  * <span data-ttu-id="48c1a-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="48c1a-123">PowerShell</span></span>
  * <span data-ttu-id="48c1a-124">SDK .NET</span><span class="sxs-lookup"><span data-stu-id="48c1a-124">.NET SDK</span></span>
  * <span data-ttu-id="48c1a-125">SDK do Node.JS</span><span class="sxs-lookup"><span data-stu-id="48c1a-125">Node.JS SDK</span></span>
  * <span data-ttu-id="48c1a-126">Java SDK</span><span class="sxs-lookup"><span data-stu-id="48c1a-126">Java SDK</span></span>
  * <span data-ttu-id="48c1a-127">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="48c1a-127">Azure CLI</span></span>
  * <span data-ttu-id="48c1a-128">Portal de Visualização</span><span class="sxs-lookup"><span data-stu-id="48c1a-128">Preview Portal</span></span>
  * <span data-ttu-id="48c1a-129">Linguagem de modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="48c1a-129">Resource Manager template language</span></span>

## <a name="network-resources"></a><span data-ttu-id="48c1a-130">Recursos de rede</span><span class="sxs-lookup"><span data-stu-id="48c1a-130">Network resources</span></span>
<span data-ttu-id="48c1a-131">Agora você pode gerenciar recursos de rede de modo independente, em vez de ter todos eles gerenciados por meio de um recurso de computação único (uma máquina virtual).</span><span class="sxs-lookup"><span data-stu-id="48c1a-131">You can now manage network resources independently, instead of having them all managed through a single compute resource (a virtual machine).</span></span> <span data-ttu-id="48c1a-132">Isso garante um maior grau de flexibilidade e agilidade em redigir uma infraestrutura complexa e em grande escala em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="48c1a-132">This ensures a higher degree of flexibility and agility in composing a complex and large scale infrastructure in a resource group.</span></span>

<span data-ttu-id="48c1a-133">Uma exibição conceitual de uma implantação de exemplo envolvendo um aplicativo de várias camadas é apresentado a seguir.</span><span class="sxs-lookup"><span data-stu-id="48c1a-133">A conceptual view of a sample deployment involving a multi-tiered application is presented below.</span></span> <span data-ttu-id="48c1a-134">Cada recurso que você vê, como NICs, endereços IP públicos e VMs, pode ser gerenciado independentemente.</span><span class="sxs-lookup"><span data-stu-id="48c1a-134">Each resource you see, such as NICs, public IP addresses, and VMs, can be managed independently.</span></span>

![Modelo de recursos de rede](./media/resource-groups-networking/Figure2.png)

<span data-ttu-id="48c1a-136">Cada recurso contém um conjunto comum de propriedades e seu conjunto de propriedades individuais.</span><span class="sxs-lookup"><span data-stu-id="48c1a-136">Every resource contains a common set of properties, and their individual property set.</span></span> <span data-ttu-id="48c1a-137">As propriedades comuns são:</span><span class="sxs-lookup"><span data-stu-id="48c1a-137">The common properties are:</span></span>

| <span data-ttu-id="48c1a-138">Propriedade</span><span class="sxs-lookup"><span data-stu-id="48c1a-138">Property</span></span> | <span data-ttu-id="48c1a-139">Descrição</span><span class="sxs-lookup"><span data-stu-id="48c1a-139">Description</span></span> | <span data-ttu-id="48c1a-140">Valores de exemplo</span><span class="sxs-lookup"><span data-stu-id="48c1a-140">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="48c1a-141">**name**</span><span class="sxs-lookup"><span data-stu-id="48c1a-141">**name**</span></span> |<span data-ttu-id="48c1a-142">Nome de recurso exclusivo.</span><span class="sxs-lookup"><span data-stu-id="48c1a-142">Unique resource name.</span></span> <span data-ttu-id="48c1a-143">Cada tipo de recurso tem suas próprias restrições de nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="48c1a-143">Each resource type has its own naming restrictions.</span></span> |<span data-ttu-id="48c1a-144">PIP01, VM01, NIC01</span><span class="sxs-lookup"><span data-stu-id="48c1a-144">PIP01, VM01, NIC01</span></span> |
| <span data-ttu-id="48c1a-145">**local**</span><span class="sxs-lookup"><span data-stu-id="48c1a-145">**location**</span></span> |<span data-ttu-id="48c1a-146">Região do Azure na qual o recurso reside</span><span class="sxs-lookup"><span data-stu-id="48c1a-146">Azure region in which the resource resides</span></span> |<span data-ttu-id="48c1a-147">westus, eastus</span><span class="sxs-lookup"><span data-stu-id="48c1a-147">westus, eastus</span></span> |
| <span data-ttu-id="48c1a-148">**ID**</span><span class="sxs-lookup"><span data-stu-id="48c1a-148">**id**</span></span> |<span data-ttu-id="48c1a-149">Identificação baseada em URI exclusivo</span><span class="sxs-lookup"><span data-stu-id="48c1a-149">Unique URI based identification</span></span> |<span data-ttu-id="48c1a-150">/subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP</span><span class="sxs-lookup"><span data-stu-id="48c1a-150">/subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP</span></span> |

<span data-ttu-id="48c1a-151">Você pode verificar as propriedades individuais de recursos nas seções abaixo.</span><span class="sxs-lookup"><span data-stu-id="48c1a-151">You can check the individual properties of resources in the sections below.</span></span>

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

## <a name="management-interfaces"></a><span data-ttu-id="48c1a-152">Interfaces de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="48c1a-152">Management interfaces</span></span>
<span data-ttu-id="48c1a-153">Você pode gerenciar os recursos de rede do Azure usando interfaces diferentes.</span><span class="sxs-lookup"><span data-stu-id="48c1a-153">You can manage your Azure networking resources using different interfaces.</span></span> <span data-ttu-id="48c1a-154">Neste documento, vamos nos concentrar em duas dessas interfaces: API REST e modelos.</span><span class="sxs-lookup"><span data-stu-id="48c1a-154">In this document we will focus on tow of those interfaces: REST API, and templates.</span></span>

### <a name="rest-api"></a><span data-ttu-id="48c1a-155">API REST</span><span class="sxs-lookup"><span data-stu-id="48c1a-155">REST API</span></span>
<span data-ttu-id="48c1a-156">Como mencionado anteriormente, os recursos de rede podem ser gerenciados por meio de uma variedade de interfaces, inclusive API REST, o SDK do .NET, SDK do Node.JS, Java SDK, PowerShell, CLI, Portal do Azure e modelos.</span><span class="sxs-lookup"><span data-stu-id="48c1a-156">As mentioned earlier, network resources can be managed via a variety of interfaces, including REST API,.NET SDK, Node.JS SDK, Java SDK, PowerShell, CLI, Azure Portal and templates.</span></span>

<span data-ttu-id="48c1a-157">A API Rest está de acordo com a especificação do protocolo HTTP 1.1.</span><span class="sxs-lookup"><span data-stu-id="48c1a-157">The Rest API’s conform to the HTTP 1.1 protocol specification.</span></span> <span data-ttu-id="48c1a-158">A estrutura geral do URI da API é apresentada abaixo:</span><span class="sxs-lookup"><span data-stu-id="48c1a-158">The general URI structure of the API is presented below:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}/providers/{resource-provider-namespace}/locations/{region-location}/register?api-version={api-version}

<span data-ttu-id="48c1a-159">E os parâmetros entre chaves representam os elementos a seguir:</span><span class="sxs-lookup"><span data-stu-id="48c1a-159">And the parameters in braces represent the following elements:</span></span>

* <span data-ttu-id="48c1a-160">**subscription-id** - a ID de sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="48c1a-160">**subscription-id** - your Azure subscription id.</span></span>
* <span data-ttu-id="48c1a-161">**resource-provider-namespace** - namespace para o provedor que está sendo usado.</span><span class="sxs-lookup"><span data-stu-id="48c1a-161">**resource-provider-namespace** - namespace for the provider being used.</span></span> <span data-ttu-id="48c1a-162">O valor para o provedor de recursos de rede é *Microsoft.Network*.</span><span class="sxs-lookup"><span data-stu-id="48c1a-162">THe value for the network resource provider is *Microsoft.Network*.</span></span>
* <span data-ttu-id="48c1a-163">**region-name** - o nome da região do Azure</span><span class="sxs-lookup"><span data-stu-id="48c1a-163">**region-name** - the Azure region name</span></span>

<span data-ttu-id="48c1a-164">Os métodos HTTP a seguir têm suporte ao fazer chamadas para a API REST:</span><span class="sxs-lookup"><span data-stu-id="48c1a-164">The following HTTP methods are supported when making calls to the REST API:</span></span>

* <span data-ttu-id="48c1a-165">**PUT** - usado para criar um recurso de um determinado tipo, modificar uma propriedade de recurso ou alterar uma associação entre os recursos.</span><span class="sxs-lookup"><span data-stu-id="48c1a-165">**PUT** - used to create a resource of a given type, modify a resource property or change an association between resources.</span></span>
* <span data-ttu-id="48c1a-166">**GET** - usado para recuperar informações de um recurso provisionado.</span><span class="sxs-lookup"><span data-stu-id="48c1a-166">**GET** - used to retrieve information for a provisioned resource.</span></span>
* <span data-ttu-id="48c1a-167">**DELETE** - usado para excluir um recurso existente.</span><span class="sxs-lookup"><span data-stu-id="48c1a-167">**DELETE** - used to delete an existing resource.</span></span>

<span data-ttu-id="48c1a-168">Ambas a solicitação e a resposta têm conformidade com um formato de carga JSON.</span><span class="sxs-lookup"><span data-stu-id="48c1a-168">Both the request and response conform to a JSON payload format.</span></span> <span data-ttu-id="48c1a-169">Para obter mais detalhes, consulte [APIs de Gerenciamento de Recursos do Azure](https://msdn.microsoft.com/library/azure/dn948464.aspx).</span><span class="sxs-lookup"><span data-stu-id="48c1a-169">For more details, see [Azure Resource Management APIs](https://msdn.microsoft.com/library/azure/dn948464.aspx).</span></span>

### <a name="resource-manager-template-language"></a><span data-ttu-id="48c1a-170">Linguagem de modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="48c1a-170">Resource Manager template language</span></span>
<span data-ttu-id="48c1a-171">Além de gerenciar recursos de modo imperativo (por APIs ou SDK), você também pode usar um estilo de programação declarativo para criar e gerenciar recursos de rede usando a Linguagem de Modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="48c1a-171">In addition to managing resources imperatively (via APIs or SDK), you can also use a declarative programming style to build and manage network resources by using the Resource Manager Template Language.</span></span>

<span data-ttu-id="48c1a-172">Uma representação de um modelo de exemplo é fornecida abaixo -</span><span class="sxs-lookup"><span data-stu-id="48c1a-172">A sample representation of a template is provided below –</span></span>

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "<version-number-of-template>",
      "parameters": { <parameter-definitions-of-template> },
      "variables": { <variable-definitions-of-template> },
      "resources": [ { <definition-of-resource-to-deploy> } ],
      "outputs": { <output-of-template> }    
    }

<span data-ttu-id="48c1a-173">O modelo é basicamente uma descrição de JSON os recursos e os valores de instância injetados por meio de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="48c1a-173">The template is primarily a JSON description of the resources and the instance values injected via parameters.</span></span> <span data-ttu-id="48c1a-174">O exemplo a seguir pode ser usado para criar uma rede virtual com 2 sub-redes.</span><span class="sxs-lookup"><span data-stu-id="48c1a-174">The example below can be used to create a virtual network with 2 subnets.</span></span>

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

<span data-ttu-id="48c1a-175">Você tem a opção de fornecer os valores de parâmetro manualmente ao usar um modelo, ou então pode usar um arquivo de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="48c1a-175">You have the option of providing the parameter values manually when using a template, or you can use a parameter file.</span></span> <span data-ttu-id="48c1a-176">O exemplo a seguir mostra um conjunto possível de valores de parâmetro a ser usado com o modelo acima:</span><span class="sxs-lookup"><span data-stu-id="48c1a-176">The example below shows a possible set of parameter values to be used with the template above:</span></span>

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


<span data-ttu-id="48c1a-177">As principais vantagens de usar modelos são:</span><span class="sxs-lookup"><span data-stu-id="48c1a-177">The main advantages of using templates are:</span></span>

* <span data-ttu-id="48c1a-178">Você pode criar uma infraestrutura complexa em um grupo de recursos em um estilo declarativo.</span><span class="sxs-lookup"><span data-stu-id="48c1a-178">You can build a complex infrastructure in a resource group in a declarative style.</span></span> <span data-ttu-id="48c1a-179">A orquestração de criação de recursos, incluindo gerenciamento de dependências, é manipulada pelo Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="48c1a-179">The orchestration of creating the resources, including dependency management, is handled by Resource Manager.</span></span>
* <span data-ttu-id="48c1a-180">A infraestrutura pode ser criada de forma repetida por várias regiões e dentro de uma região, simplesmente alterando os parâmetros.</span><span class="sxs-lookup"><span data-stu-id="48c1a-180">The infrastructure can be created in a repeatable way across various regions and within a region by simply changing parameters.</span></span>
* <span data-ttu-id="48c1a-181">O estilo declarativo resulta em menor tempo de avanço na criação de modelos e implantação da infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="48c1a-181">The declarative style leads to shorter lead time in building the templates and rolling out the infrastructure.</span></span>

<span data-ttu-id="48c1a-182">Para exemplos de modelo, consulte [Modelos de início rápido do Azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="48c1a-182">For sample templates, see [Azure quickstart templates](https://github.com/Azure/azure-quickstart-templates).</span></span>

<span data-ttu-id="48c1a-183">Para obter mais informações sobre a Linguagem de Modelo do Resource Manager, confira [Linguagem de Modelo do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="48c1a-183">For more information on the Resource Manager Template Language, see [Azure Resource Manager Template Language](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="48c1a-184">O modelo de exemplo acima usa a rede virtual e recursos de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="48c1a-184">The sample template above uses the virtual network and subnet resources.</span></span> <span data-ttu-id="48c1a-185">Há outros recursos de rede, que você pode usar, conforme listado abaixo:</span><span class="sxs-lookup"><span data-stu-id="48c1a-185">There are other network resources you can use as listed below:</span></span>

### <a name="using-a-template"></a><span data-ttu-id="48c1a-186">Criação de um modelo</span><span class="sxs-lookup"><span data-stu-id="48c1a-186">Using a template</span></span>
<span data-ttu-id="48c1a-187">Você pode implantar serviços no Azure de um modelo usando o PowerShell, AzureCLI ou apenas clicando para implantar no GitHub.</span><span class="sxs-lookup"><span data-stu-id="48c1a-187">You can deploy services to Azure from a template by using PowerShell, AzureCLI, or by performing a click to deploy from GitHub.</span></span> <span data-ttu-id="48c1a-188">Para implantar os serviços de um modelo no GitHub, execute as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="48c1a-188">To deploy services from a template in GitHub, execute the following steps:</span></span>

1. <span data-ttu-id="48c1a-189">Abra o arquivo template3 no GitHub.</span><span class="sxs-lookup"><span data-stu-id="48c1a-189">Open the template3 file from GitHub.</span></span> <span data-ttu-id="48c1a-190">Por exemplo, abra a rede Virtual do [com duas sub-redes](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="48c1a-190">As an example, open [Virtual network with two subnets](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).</span></span>
2. <span data-ttu-id="48c1a-191">Clique em **implantar no Azure**e entre no portal do Azure com suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="48c1a-191">Click on **Deploy to Azure**, and then sign in on to the Azure portal with your credentials.</span></span>
3. <span data-ttu-id="48c1a-192">Verifique o modelo e, em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="48c1a-192">Verify the template, and then click **Save**.</span></span>
4. <span data-ttu-id="48c1a-193">Clique em **Editar parâmetros** e selecione um local, como *Oeste dos EUA*, para o vnet e sub-redes.</span><span class="sxs-lookup"><span data-stu-id="48c1a-193">Click **Edit parameters** and select a location, such as *West US*, for the vnet and subnets.</span></span>
5. <span data-ttu-id="48c1a-194">Se necessário, altere os parâmetros **ADDRESSPREFIX** e **SUBNETPREFIX** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="48c1a-194">If necessary, change the **ADDRESSPREFIX** and **SUBNETPREFIX** parameters, and then click **OK**.</span></span>
6. <span data-ttu-id="48c1a-195">Clique em **Selecionar um grupo de recursos** e, em seguida, clique no grupo de recursos ao qual você deseja adicionar o vnet e as sub-redes.</span><span class="sxs-lookup"><span data-stu-id="48c1a-195">Click **Select a resource group** and then click on the resource group you want to add the vnet and subnets to.</span></span> <span data-ttu-id="48c1a-196">Como alternativa, você pode criar um novo grupo de recursos clicando **Ou criar novos**.</span><span class="sxs-lookup"><span data-stu-id="48c1a-196">Alternatively, you can create a new resource group by clicking **Or create new**.</span></span>
7. <span data-ttu-id="48c1a-197">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="48c1a-197">Click **Create**.</span></span> <span data-ttu-id="48c1a-198">Observe a exibição lado a lado **Implantação de modelo de provisionamento**.</span><span class="sxs-lookup"><span data-stu-id="48c1a-198">Notice the tile displaying **Provisioning Template deployment**.</span></span> <span data-ttu-id="48c1a-199">Quando a implantação estiver concluída, você verá uma tela semelhante à tela abaixo.</span><span class="sxs-lookup"><span data-stu-id="48c1a-199">Once the deployment is done, you will see a screen similar to one below.</span></span>

![Implantação do modelo de exemplo](./media/resource-groups-networking/Figure6.png)

## <a name="next-steps"></a><span data-ttu-id="48c1a-201">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="48c1a-201">Next steps</span></span>
[<span data-ttu-id="48c1a-202">Idioma de modelo do Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="48c1a-202">Azure Resource Manager Template Language</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[<span data-ttu-id="48c1a-203">Rede do Azure - modelos usados frequentemente</span><span class="sxs-lookup"><span data-stu-id="48c1a-203">Azure Networking – commonly used templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

[<span data-ttu-id="48c1a-204">Azure Resource Manager vs implantação clássica</span><span class="sxs-lookup"><span data-stu-id="48c1a-204">Azure Resource Manager vs. classic deployment</span></span>](../azure-resource-manager/resource-manager-deployment-model.md)

[<span data-ttu-id="48c1a-205">Visão geral do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="48c1a-205">Azure Resource Manager Overview</span></span>](../azure-resource-manager/resource-group-overview.md)

