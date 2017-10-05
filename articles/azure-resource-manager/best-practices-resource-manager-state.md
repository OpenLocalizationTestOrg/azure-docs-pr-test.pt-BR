---
title: Passar valores complexos entre modelos do Azure | Microsoft Docs
description: Mostra abordagens recomendadas para usar objetos complexos para compartilhar dados de estado com modelos e modelos vinculados do Azure Resource Manager.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: fd2f5e2d-d56d-4e01-a57d-34f3eaead4a9
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: tomfitz
ms.openlocfilehash: 23cc4321159a87b61c177b11381646af8bd9eb35
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="share-state-to-and-from-azure-resource-manager-templates"></a><span data-ttu-id="8dc8a-103">Compartilha o estado dos e para os modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8dc8a-103">Share state to and from Azure Resource Manager templates</span></span>
<span data-ttu-id="8dc8a-104">Este tópico mostra as melhores práticas para gerenciar e compartilhar o estado em modelos.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-104">This topic shows best practices for managing and sharing state within templates.</span></span> <span data-ttu-id="8dc8a-105">Os parâmetros e variáveis mostrados neste tópico são exemplos dos tipos de objetos que você pode definir para organizar seus requisitos de implantação convenientemente.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-105">The parameters and variables shown in this topic are examples of the type of objects you can define to conveniently organize your deployment requirements.</span></span> <span data-ttu-id="8dc8a-106">A partir desses exemplos, você pode implementar seus próprios objetos com valores de propriedade que façam sentido para o seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-106">From these examples, you can implement your own objects with property values that make sense for your environment.</span></span>

<span data-ttu-id="8dc8a-107">Este tópico faz parte de um whitepaper mais amplo.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-107">This topic is part of a larger whitepaper.</span></span> <span data-ttu-id="8dc8a-108">Para ler o artigo completo, baixe as [Considerações e práticas comprovadas dos modelos do Resource Manager da mais alta qualidade](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).</span><span class="sxs-lookup"><span data-stu-id="8dc8a-108">To read the full paper, download [World Class Resource Manager Templates Considerations and Proven Practices](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).</span></span>

## <a name="provide-standard-configuration-settings"></a><span data-ttu-id="8dc8a-109">Fornecer configurações padrão</span><span class="sxs-lookup"><span data-stu-id="8dc8a-109">Provide standard configuration settings</span></span>
<span data-ttu-id="8dc8a-110">Em vez de oferecer um modelo que fornece flexibilidade total e inúmeras variações, o normal é fornecer uma seleção de configurações conhecidas.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-110">Rather than offer a template that provides total flexibility and countless variations, a common pattern is to provide a selection of known configurations.</span></span> <span data-ttu-id="8dc8a-111">Na verdade, os usuários podem selecionar tamanhos de camiseta padrão, como área restrita, pequeno, médio e grande.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-111">In effect, users can select standard t-shirt sizes such as sandbox, small, medium, and large.</span></span> <span data-ttu-id="8dc8a-112">Outros exemplos de tamanhos de camiseta são ofertas de produtos, como community edition ou enterprise edition.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-112">Other examples of t-shirt sizes are product offerings, such as community edition or enterprise edition.</span></span> <span data-ttu-id="8dc8a-113">Em outros casos, podem se tratar de configurações de uma tecnologia específicas para uma determinada carga de trabalho - como mapear/reduzir ou no SQL.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-113">In other cases, it may be workload-specific configurations of a technology – such as map reduce or no sql.</span></span>

<span data-ttu-id="8dc8a-114">Com objetos complexos, você pode criar variáveis que contenham coleções de dados, às vezes conhecidos como "conjunto de propriedades", e usar esses dados para orientar a declaração de recurso em seu modelo.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-114">With complex objects, you can create variables that contain collections of data, sometimes known as "property bags" and use that data to drive the resource declaration in your template.</span></span> <span data-ttu-id="8dc8a-115">Essa abordagem fornece boas configurações conhecidas, de tamanhos variados que são pré-configurados para os clientes.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-115">This approach provides good, known configurations of varying sizes that are preconfigured for customers.</span></span> <span data-ttu-id="8dc8a-116">Sem configurações conhecidas, os usuários do modelo devem determinar o tamanho do cluster por conta própria, levar em consideração restrições de recursos de plataforma e fazer cálculos para identificar o particionamento resultante de contas de armazenamento e outros recursos (devido a restrições de recursos e de tamanho do cluster).</span><span class="sxs-lookup"><span data-stu-id="8dc8a-116">Without known configurations, users of the template must determine cluster sizing on their own, factor in platform resource constraints, and do math to identify the resulting partitioning of storage accounts and other resources (due to cluster size and resource constraints).</span></span> <span data-ttu-id="8dc8a-117">Além de criar uma experiência melhor para o cliente, é mais fácil dar suporte a algumas configurações conhecidas que podem ajudá-lo a oferecer um nível maior de densidade.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-117">In addition to making a better experience for the customer, a few known configurations are easier to support and can help you deliver a higher level of density.</span></span>

<span data-ttu-id="8dc8a-118">O exemplo a seguir mostra como definir variáveis que contêm objetos complexos para representar coleções de dados.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-118">The following example shows how to define variables that contain complex objects for representing collections of data.</span></span> <span data-ttu-id="8dc8a-119">As coleções definem os valores que são usados para o tamanho da máquina virtual, as configurações de rede, as configurações de sistema operacional e as configurações de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-119">The collections define values that are used for virtual machine size, network settings, operating system settings and availability settings.</span></span>

    "variables": {
      "tshirtSize": "[variables(concat('tshirtSize', parameters('tshirtSize')))]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      },
      "tshirtSizeMedium": {
        "vmSize": "Standard_A3",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-8disk-resources.json')]",
        "vmCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1],
          "jumpbox": 0
        }
      },
      "tshirtSizeLarge": {
        "vmSize": "Standard_A4",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-16disk-resources.json')]",
        "vmCount": 3,
        "slaveCount": 2,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 2,
          "pool": "db",
          "map": [0,1,1],
          "jumpbox": 0
        }
      },
      "osSettings": {
        "scripts": [
          "[concat(variables('templateBaseUrl'), 'install_postgresql.sh')]",
          "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/shared_scripts/ubuntu/vm-disk-utils-0.1.sh"
        ],
        "imageReference": {
          "publisher": "Canonical",
          "offer": "UbuntuServer",
          "sku": "14.04.2-LTS",
          "version": "latest"
        }
      },
      "networkSettings": {
        "vnetName": "[parameters('virtualNetworkName')]",
        "addressPrefix": "10.0.0.0/16",
        "subnets": {
          "dmz": {
            "name": "dmz",
            "prefix": "10.0.0.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          },
          "data": {
            "name": "data",
            "prefix": "10.0.1.0/24",
            "vnet": "[parameters('virtualNetworkName')]"
          }
        }
      },
      "availabilitySetSettings": {
        "name": "pgsqlAvailabilitySet",
        "fdCount": 3,
        "udCount": 5
      }
    }

<span data-ttu-id="8dc8a-120">Observe que a variável **tshirtSize** concatena o tamanho de camiseta que você forneceu através de um parâmetro (**Small**, **Medium**, **Large**) ao texto **tshirtSize**.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-120">Notice that the **tshirtSize** variable concatenates the t-shirt size you provided through a parameter (**Small**, **Medium**, **Large**) to the text **tshirtSize**.</span></span> <span data-ttu-id="8dc8a-121">Você usa essa variável para recuperar a variável de objeto complexo associada para o tamanho de camiseta.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-121">You use this variable to retrieve the associated complex object variable for that t-shirt size.</span></span>

<span data-ttu-id="8dc8a-122">Você pode fazer referência a essas variáveis posteriormente no modelo.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-122">You can then reference these variables later in the template.</span></span> <span data-ttu-id="8dc8a-123">A capacidade de fazer referência a variáveis nomeadas e às suas propriedades simplifica a sintaxe de modelo e facilita o entendimento do contexto.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-123">The ability to reference named-variables and their properties simplifies the template syntax, and makes it easy to understand context.</span></span> <span data-ttu-id="8dc8a-124">O exemplo a seguir define um recurso para implantar usando os objetos mostrados anteriormente para definir valores.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-124">The following example defines a resource to deploy by using the objects shown previously to set values.</span></span> <span data-ttu-id="8dc8a-125">Por exemplo, o tamanho da VM é definido pela recuperação do valor de `variables('tshirtSize').vmSize`, enquanto o valor do tamanho do disco é recuperado de `variables('tshirtSize').diskSize`.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-125">For example, the VM size is set by retrieving the value for `variables('tshirtSize').vmSize` while the value for the disk size is retrieved from `variables('tshirtSize').diskSize`.</span></span> <span data-ttu-id="8dc8a-126">Além disso, o URI de um modelo vinculado é definido com o valor de `variables('tshirtSize').vmTemplate`.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-126">In addition, the URI for a linked template is set with the value for `variables('tshirtSize').vmTemplate`.</span></span>

    "name": "master-node",
    "type": "Microsoft.Resources/deployments",
    "apiVersion": "2015-01-01",
    "dependsOn": [
        "[concat('Microsoft.Resources/deployments/', 'shared')]"
    ],
    "properties": {
        "mode": "Incremental",
        "templateLink": {
          "uri": "[variables('tshirtSize').vmTemplate]",
          "contentVersion": "1.0.0.0"
        },
        "parameters": {
          "adminPassword": {
            "value": "[parameters('adminPassword')]"
          },
          "replicatorPassword": {
            "value": "[parameters('replicatorPassword')]"
          },
          "osSettings": {
            "value": "[variables('osSettings')]"
          },
          "subnet": {
            "value": "[variables('networkSettings').subnets.data]"
          },
          "commonSettings": {
            "value": {
              "region": "[parameters('region')]",
              "adminUsername": "[parameters('adminUsername')]",
              "namespace": "ms"
            }
          },
          "storageSettings": {
            "value":"[variables('tshirtSize').storage]"
          },
          "machineSettings": {
            "value": {
              "vmSize": "[variables('tshirtSize').vmSize]",
              "diskSize": "[variables('tshirtSize').diskSize]",
              "vmCount": 1,
              "availabilitySet": "[variables('availabilitySetSettings').name]"
            }
          },
          "masterIpAddress": {
            "value": "0"
          },
          "dbType": {
            "value": "MASTER"
          }
        }
      }
    }

## <a name="pass-state-to-a-template"></a><span data-ttu-id="8dc8a-127">Passar o estado para um modelo</span><span class="sxs-lookup"><span data-stu-id="8dc8a-127">Pass state to a template</span></span>
<span data-ttu-id="8dc8a-128">Você pode compartilhar o estado em um modelo por meio de parâmetros fornecidos diretamente durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-128">You share state into a template through parameters that you provide directly during deployment.</span></span>

<span data-ttu-id="8dc8a-129">A tabela a seguir lista os parâmetros normalmente usados em modelos.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-129">The following table lists commonly used parameters in templates.</span></span>

| <span data-ttu-id="8dc8a-130">Nome</span><span class="sxs-lookup"><span data-stu-id="8dc8a-130">Name</span></span> | <span data-ttu-id="8dc8a-131">Valor</span><span class="sxs-lookup"><span data-stu-id="8dc8a-131">Value</span></span> | <span data-ttu-id="8dc8a-132">Descrição</span><span class="sxs-lookup"><span data-stu-id="8dc8a-132">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8dc8a-133">location</span><span class="sxs-lookup"><span data-stu-id="8dc8a-133">location</span></span> |<span data-ttu-id="8dc8a-134">Cadeia de caracteres de uma lista restrita de regiões do Azure</span><span class="sxs-lookup"><span data-stu-id="8dc8a-134">String from a constrained list of Azure regions</span></span> |<span data-ttu-id="8dc8a-135">O local onde os recursos são implantados.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-135">The location where the resources are deployed.</span></span> |
| <span data-ttu-id="8dc8a-136">storageAccountNamePrefix</span><span class="sxs-lookup"><span data-stu-id="8dc8a-136">storageAccountNamePrefix</span></span> |<span data-ttu-id="8dc8a-137">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="8dc8a-137">String</span></span> |<span data-ttu-id="8dc8a-138">Nome DNS exclusivo da conta de armazenamento na qual são colocados os discos da VM</span><span class="sxs-lookup"><span data-stu-id="8dc8a-138">Unique DNS name for the Storage Account where the VM's disks are placed</span></span> |
| <span data-ttu-id="8dc8a-139">domainName</span><span class="sxs-lookup"><span data-stu-id="8dc8a-139">domainName</span></span> |<span data-ttu-id="8dc8a-140">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="8dc8a-140">String</span></span> |<span data-ttu-id="8dc8a-141">Nome de domínio da VM jumpbox publicamente acessível no formato: **{domainName}.{local}.cloudapp.com** Por exemplo: **nomedomeudomínio.westus.cloudapp.azure.com**</span><span class="sxs-lookup"><span data-stu-id="8dc8a-141">Domain name of the publicly accessible jumpbox VM in the format: **{domainName}.{location}.cloudapp.com** For example: **mydomainname.westus.cloudapp.azure.com**</span></span> |
| <span data-ttu-id="8dc8a-142">adminUsername</span><span class="sxs-lookup"><span data-stu-id="8dc8a-142">adminUsername</span></span> |<span data-ttu-id="8dc8a-143">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="8dc8a-143">String</span></span> |<span data-ttu-id="8dc8a-144">Nome de usuário das VMs</span><span class="sxs-lookup"><span data-stu-id="8dc8a-144">Username for the VMs</span></span> |
| <span data-ttu-id="8dc8a-145">adminPassword</span><span class="sxs-lookup"><span data-stu-id="8dc8a-145">adminPassword</span></span> |<span data-ttu-id="8dc8a-146">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="8dc8a-146">String</span></span> |<span data-ttu-id="8dc8a-147">A senha das VMs</span><span class="sxs-lookup"><span data-stu-id="8dc8a-147">Password for the VMs</span></span> |
| <span data-ttu-id="8dc8a-148">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="8dc8a-148">tshirtSize</span></span> |<span data-ttu-id="8dc8a-149">Cadeia de caracteres de uma lista restrita de tamanhos de camiseta oferecidos</span><span class="sxs-lookup"><span data-stu-id="8dc8a-149">String from a constrained list of offered t-shirt sizes</span></span> |<span data-ttu-id="8dc8a-150">O tamanho da unidade de escala nomeada para provisionamento.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-150">The named scale unit size to provision.</span></span> <span data-ttu-id="8dc8a-151">Por exemplo, "Pequeno", "Médio", "Grande"</span><span class="sxs-lookup"><span data-stu-id="8dc8a-151">For example, "Small", "Medium", "Large"</span></span> |
| <span data-ttu-id="8dc8a-152">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="8dc8a-152">virtualNetworkName</span></span> |<span data-ttu-id="8dc8a-153">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="8dc8a-153">String</span></span> |<span data-ttu-id="8dc8a-154">Nome da rede virtual que o consumidor deseja usar.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-154">Name of the virtual network that the consumer wants to use.</span></span> |
| <span data-ttu-id="8dc8a-155">enableJumpbox</span><span class="sxs-lookup"><span data-stu-id="8dc8a-155">enableJumpbox</span></span> |<span data-ttu-id="8dc8a-156">Cadeia de caracteres de uma lista restrita (habilitada/desabilitada)</span><span class="sxs-lookup"><span data-stu-id="8dc8a-156">String from a constrained list (enabled/disabled)</span></span> |<span data-ttu-id="8dc8a-157">Parâmetro que identifica se um Jumpbox será habilitado para o ambiente.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-157">Parameter that identifies whether to enable a jumpbox for the environment.</span></span> <span data-ttu-id="8dc8a-158">Valores: "habilitado", "desabilitado"</span><span class="sxs-lookup"><span data-stu-id="8dc8a-158">Values: "enabled", "disabled"</span></span> |

<span data-ttu-id="8dc8a-159">O parâmetro **tshirtSize** usado na seção anterior é definido como:</span><span class="sxs-lookup"><span data-stu-id="8dc8a-159">The **tshirtSize** parameter used in the previous section is defined as:</span></span>

    "parameters": {
      "tshirtSize": {
        "type": "string",
        "defaultValue": "Small",
        "allowedValues": [
          "Small",
          "Medium",
          "Large"
        ],
        "metadata": {
          "Description": "T-shirt size of the MongoDB deployment"
        }
      }
    }


## <a name="pass-state-to-linked-templates"></a><span data-ttu-id="8dc8a-160">Passar o estado para modelos vinculados</span><span class="sxs-lookup"><span data-stu-id="8dc8a-160">Pass state to linked templates</span></span>
<span data-ttu-id="8dc8a-161">Ao conectar-se aos modelos vinculados, geralmente você utilizará uma combinação de variáveis estáticas e geradas.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-161">When connecting to linked templates, you often use a mix of static and generated variables.</span></span>

### <a name="static-variables"></a><span data-ttu-id="8dc8a-162">Variáveis estáticas</span><span class="sxs-lookup"><span data-stu-id="8dc8a-162">Static variables</span></span>
<span data-ttu-id="8dc8a-163">Variáveis estáticas geralmente são usadas para fornecer valores de base, como URLs, que são usados em um modelo.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-163">Static variables are often used to provide base values, such as URLs, that are used throughout a template.</span></span>

<span data-ttu-id="8dc8a-164">No trecho do modelo a seguir, `templateBaseUrl` especifica o local raiz do modelo no GitHub.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-164">In the following template excerpt, `templateBaseUrl` specifies the root location for the template in GitHub.</span></span> <span data-ttu-id="8dc8a-165">A próxima linha cria uma nova variável `sharedTemplateUrl` , que concatena o URL base com o nome conhecido do modelo de recursos compartilhados.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-165">The next line builds a new variable `sharedTemplateUrl` that concatenates the base URL with the known name of the shared resources template.</span></span> <span data-ttu-id="8dc8a-166">Abaixo dessa linha, uma variável de objeto complexo é usada para armazenar um tamanho de camiseta, em que o URL base é concatenado ao local do modelo de configuração conhecido e armazenado na propriedade `vmTemplate` .</span><span class="sxs-lookup"><span data-stu-id="8dc8a-166">Below that line, a complex object variable is used to store a t-shirt size, where the base URL is concatenated to the known configuration template location and stored in the `vmTemplate` property.</span></span>

<span data-ttu-id="8dc8a-167">O benefício desta abordagem é que, se o local do modelo for alterado, você só precisará alterar a variável estática em um único lugar, que a passará para os modelos vinculados.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-167">The benefit of this approach is that if the template location changes, you only need to change the static variable in one place, which passes it throughout the linked templates.</span></span>

    "variables": {
      "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
      "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
      "tshirtSizeSmall": {
        "vmSize": "Standard_A1",
        "diskSize": 1023,
        "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
        "vmCount": 2,
        "slaveCount": 1,
        "storage": {
          "name": "[parameters('storageAccountNamePrefix')]",
          "count": 1,
          "pool": "db",
          "map": [0,0],
          "jumpbox": 0
        }
      }
    }

### <a name="generated-variables"></a><span data-ttu-id="8dc8a-168">Variáveis geradas</span><span class="sxs-lookup"><span data-stu-id="8dc8a-168">Generated variables</span></span>
<span data-ttu-id="8dc8a-169">Além de variáveis estáticas, diversas variáveis são geradas dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-169">In addition to static variables, several variables are generated dynamically.</span></span> <span data-ttu-id="8dc8a-170">Esta seção identifica alguns dos tipos comuns de variáveis geradas.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-170">This section identifies some of the common types of generated variables.</span></span>

#### <a name="tshirtsize"></a><span data-ttu-id="8dc8a-171">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="8dc8a-171">tshirtSize</span></span>
<span data-ttu-id="8dc8a-172">Você está familiarizado com essa variável gerada dos exemplos acima.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-172">You are familiar with this generated variable from the examples above.</span></span>

#### <a name="networksettings"></a><span data-ttu-id="8dc8a-173">networkSettings</span><span class="sxs-lookup"><span data-stu-id="8dc8a-173">networkSettings</span></span>
<span data-ttu-id="8dc8a-174">Em um modelo de capacidade, recurso ou solução de escopo completa, os modelos vinculados normalmente criam recursos que existem em uma rede.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-174">In a capacity, capability, or end-to-end scoped solution template, the linked templates typically create resources that exist on a network.</span></span> <span data-ttu-id="8dc8a-175">Uma abordagem simples é usar um objeto complexo para armazenar as configurações de rede e passá-las para modelos vinculados.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-175">One straightforward approach is to use a complex object to store network settings and pass them to linked templates.</span></span>

<span data-ttu-id="8dc8a-176">Um exemplo de configurações de rede de comunicação pode ser visto abaixo.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-176">An example of communicating network settings can be seen below.</span></span>

    "networkSettings": {
      "vnetName": "[parameters('virtualNetworkName')]",
      "addressPrefix": "10.0.0.0/16",
      "subnets": {
        "dmz": {
          "name": "dmz",
          "prefix": "10.0.0.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        },
        "data": {
          "name": "data",
          "prefix": "10.0.1.0/24",
          "vnet": "[parameters('virtualNetworkName')]"
        }
      }
    }

#### <a name="availabilitysettings"></a><span data-ttu-id="8dc8a-177">availabilitySettings</span><span class="sxs-lookup"><span data-stu-id="8dc8a-177">availabilitySettings</span></span>
<span data-ttu-id="8dc8a-178">Recursos criados em modelos vinculados geralmente são colocados em um conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-178">Resources created in linked templates are often placed in an availability set.</span></span> <span data-ttu-id="8dc8a-179">No exemplo a seguir, o nome do conjunto de disponibilidade é especificado e também a contagem de domínios de falha e de atualização para uso.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-179">In the following example, the availability set name is specified and also the fault domain and update domain count to use.</span></span>

    "availabilitySetSettings": {
      "name": "pgsqlAvailabilitySet",
      "fdCount": 3,
      "udCount": 5
    }

<span data-ttu-id="8dc8a-180">Se precisar de vários conjuntos de disponibilidade (por exemplo, um para nós mestres e outro para nós de dados), você pode usar um nome como um prefixo, especificar vários conjuntos de disponibilidade ou seguir o modelo mostrado anteriormente para a criação de uma variável para um tamanho de camiseta específico.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-180">If you need multiple availability sets (for example, one for master nodes and another for data nodes), you can use a name as a prefix, specify multiple availability sets, or follow the model shown earlier for creating a variable for a specific t-shirt size.</span></span>

#### <a name="storagesettings"></a><span data-ttu-id="8dc8a-181">storageSettings</span><span class="sxs-lookup"><span data-stu-id="8dc8a-181">storageSettings</span></span>
<span data-ttu-id="8dc8a-182">Detalhes de armazenamento geralmente são compartilhados com modelos vinculados.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-182">Storage details are often shared with linked templates.</span></span> <span data-ttu-id="8dc8a-183">No exemplo abaixo, um objeto *storageSettings* fornece detalhes sobre os nomes de contêiner e da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-183">In the example below, a *storageSettings* object provides details about the storage account and container names.</span></span>

    "storageSettings": {
        "vhdStorageAccountName": "[parameters('storageAccountName')]",
        "vhdContainerName": "[variables('vmStorageAccountContainerName')]",
        "destinationVhdsContainer": "[concat('https://', parameters('storageAccountName'), variables('vmStorageAccountDomain'), '/', variables('vmStorageAccountContainerName'), '/')]"
    }

#### <a name="ossettings"></a><span data-ttu-id="8dc8a-184">osSettings</span><span class="sxs-lookup"><span data-stu-id="8dc8a-184">osSettings</span></span>
<span data-ttu-id="8dc8a-185">Com modelos vinculados, você precisa passar configurações do sistema operacional para vários tipos de nós em todos os tipos de configuração diferentes conhecidos.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-185">With linked templates, you may need to pass operating system settings to various nodes types across different known configuration types.</span></span> <span data-ttu-id="8dc8a-186">Um objeto complexo é uma maneira fácil de armazenar e compartilhar informações de sistema operacional e também torna mais fácil dar suporte a várias opções de sistema operacional para implantação.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-186">A complex object is an easy way to store and share operating system information and also makes it easier to support multiple operating system choices for deployment.</span></span>

<span data-ttu-id="8dc8a-187">O exemplo a seguir mostra um objeto para *osSettings*:</span><span class="sxs-lookup"><span data-stu-id="8dc8a-187">The following example shows an object for *osSettings*:</span></span>

    "osSettings": {
      "imageReference": {
        "publisher": "Canonical",
        "offer": "UbuntuServer",
        "sku": "14.04.2-LTS",
        "version": "latest"
      }
    }

#### <a name="machinesettings"></a><span data-ttu-id="8dc8a-188">machineSettings</span><span class="sxs-lookup"><span data-stu-id="8dc8a-188">machineSettings</span></span>
<span data-ttu-id="8dc8a-189">Variável gerada, *machineSettings* é um objeto complexo que contém uma mistura de variáveis principais para criar uma VM.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-189">A generated variable, *machineSettings* is a complex object containing a mix of core variables for creating a VM.</span></span> <span data-ttu-id="8dc8a-190">As variáveis incluem o nome de usuário e a senha do administrador, um prefixo para os nomes das VMs e uma referência de imagem do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-190">The variables include administrator user name and password, a prefix for the VM names, and an operating system image reference.</span></span>

    "machineSettings": {
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "machineNamePrefix": "mongodb-",
        "osImageReference": {
            "publisher": "[variables('osFamilySpec').imagePublisher]",
            "offer": "[variables('osFamilySpec').imageOffer]",
            "sku": "[variables('osFamilySpec').imageSKU]",
            "version": "latest"
        }
    },

<span data-ttu-id="8dc8a-191">Observe que *osImageReference* recupera os valores da variável *osSettings* definida no modelo principal.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-191">Note that *osImageReference* retrieves the values from the *osSettings* variable defined in the main template.</span></span> <span data-ttu-id="8dc8a-192">Isso significa que você pode alterar facilmente o sistema operacional de uma VM — completamente ou com base na preferência de um consumidor de modelo.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-192">That means you can easily change the operating system for a VM—entirely or based on the preference of a template consumer.</span></span>

#### <a name="vmscripts"></a><span data-ttu-id="8dc8a-193">vmScripts</span><span class="sxs-lookup"><span data-stu-id="8dc8a-193">vmScripts</span></span>
<span data-ttu-id="8dc8a-194">O objeto *vmScripts* contém detalhes sobre os scripts a serem baixados e executados em uma instância de VM, incluindo referências externas e internas.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-194">The *vmScripts* object contains details about the scripts to download and execute on a VM instance, including outside and inside references.</span></span> <span data-ttu-id="8dc8a-195">Referências externas incluem a infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-195">Outside references include the infrastructure.</span></span>
<span data-ttu-id="8dc8a-196">Referências internas incluem o software instalado e a configuração.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-196">Inside references include the installed software installed and configuration.</span></span>

<span data-ttu-id="8dc8a-197">Você usa a propriedade *scriptsToDownload* para listar os scripts a serem baixados na VM.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-197">You use the *scriptsToDownload* property to list the scripts to download to the VM.</span></span> <span data-ttu-id="8dc8a-198">Esse objeto também contém referências aos argumentos de linha de comando de diferentes tipos de ações.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-198">This object also contains references to command-line arguments for different types of actions.</span></span> <span data-ttu-id="8dc8a-199">Essas ações incluem a execução da instalação padrão para cada nó individual, uma instalação que é executada depois que todos os nós são implantados e quaisquer scripts adicionais que possam ser específicos de um determinado modelo.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-199">These actions include executing the default installation for each individual node, an installation that runs after all nodes are deployed, and any additional scripts that may be specific to a given template.</span></span>

<span data-ttu-id="8dc8a-200">Este exemplo é de um modelo usado para implantar MongoDB, que requer um arbitrador para oferecer alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-200">This example is from a template used to deploy MongoDB, which requires an arbiter to deliver high availability.</span></span> <span data-ttu-id="8dc8a-201">O *arbiterNodeInstallCommand* foi adicionado a *vmScripts* para instalar o arbitrador.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-201">The *arbiterNodeInstallCommand* has been added to *vmScripts* to install the arbiter.</span></span>

<span data-ttu-id="8dc8a-202">A seção de variáveis é onde você encontra as variáveis que definem o texto específico para executar o script com os valores adequados.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-202">The variables section is where you find the variables that define the specific text to execute the script with the proper values.</span></span>

    "vmScripts": {
        "scriptsToDownload": [
            "[concat(variables('scriptUrl'), 'mongodb-', variables('osFamilySpec').osName, '-install.sh')]",
            "[concat(variables('sharedScriptUrl'), 'vm-disk-utils-0.1.sh')]"
        ],
        "regularNodeInstallCommand": "[variables('installCommand')]",
        "lastNodeInstallCommand": "[concat(variables('installCommand'), ' -l')]",
        "arbiterNodeInstallCommand": "[concat(variables('installCommand'), ' -a')]"
    },


## <a name="return-state-from-a-template"></a><span data-ttu-id="8dc8a-203">Retornar o estado de um modelo</span><span class="sxs-lookup"><span data-stu-id="8dc8a-203">Return state from a template</span></span>
<span data-ttu-id="8dc8a-204">Você pode não só passar dados para um modelo, mas também pode compartilhar dados de volta para o modelo de chamada.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-204">Not only can you pass data into a template, you can also share data back to the calling template.</span></span> <span data-ttu-id="8dc8a-205">Na seção **outputs** de um modelo vinculado, você pode fornecer os pares de chave-valor que podem ser consumidos pelo modelo de origem.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-205">In the **outputs** section of a linked template, you can provide key/value pairs that can be consumed by the source template.</span></span>

<span data-ttu-id="8dc8a-206">O exemplo a seguir mostra como passar o endereço IP privado gerado em um modelo vinculado.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-206">The following example shows how to pass the private IP address generated in a linked template.</span></span>

    "outputs": {
        "masterip": {
            "value": "[reference(concat(variables('nicName'),0)).ipConfigurations[0].properties.privateIPAddress]",
            "type": "string"
         }
    }

<span data-ttu-id="8dc8a-207">No modelo principal, você pode usar esses dados com a seguinte sintaxe:</span><span class="sxs-lookup"><span data-stu-id="8dc8a-207">Within the main template, you can use that data with the following syntax:</span></span>

    "[reference('master-node').outputs.masterip.value]"

<span data-ttu-id="8dc8a-208">Você pode usar essa expressão na seção de saídas ou na seção de recursos do modelo principal.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-208">You can use this expression in either the outputs section or the resources section of the main template.</span></span> <span data-ttu-id="8dc8a-209">Não é possível usar a expressão na seção de variáveis porque ela se baseia no estado de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-209">You cannot use the expression in the variables section because it relies on the runtime state.</span></span> <span data-ttu-id="8dc8a-210">Para retornar esse valor do modelo principal, use:</span><span class="sxs-lookup"><span data-stu-id="8dc8a-210">To return this value from the main template, use:</span></span>

    "outputs": {
      "masterIpAddress": {
        "value": "[reference('master-node').outputs.masterip.value]",
        "type": "string"
      }

<span data-ttu-id="8dc8a-211">Para obter um exemplo de como usar a seção de saídas de um modelo vinculado para retornar discos de dados para uma máquina virtual, consulte [Criando vários discos de dados para uma Máquina Virtual](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="8dc8a-211">For an example of using the outputs section of a linked template to return data disks for a virtual machine, see [Creating multiple data disks for a Virtual Machine](resource-group-create-multiple.md).</span></span>

## <a name="define-authentication-settings-for-virtual-machine"></a><span data-ttu-id="8dc8a-212">Definir configurações de autenticação para uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="8dc8a-212">Define authentication settings for virtual machine</span></span>
<span data-ttu-id="8dc8a-213">Você pode usar o mesmo padrão mostrado anteriormente para definições de configuração, com o fim de especificar as configurações de autenticação para uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-213">You can use the same pattern shown previously for configuration settings to specify the authentication settings for a virtual machine.</span></span> <span data-ttu-id="8dc8a-214">Você cria um parâmetro para passar o tipo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-214">You create a parameter for passing in the type of authentication.</span></span>

    "parameters": {
      "authenticationType": {
        "allowedValues": [
          "password",
          "sshPublicKey"
        ],
        "defaultValue": "password",
        "metadata": {
          "description": "Authentication type"
        },
        "type": "string"
      }
    }

<span data-ttu-id="8dc8a-215">Adicione variáveis para os tipos de autenticação diferentes, bem como uma variável para armazenar qual tipo é usado para essa implantação com base no valor do parâmetro.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-215">You add variables for the different authentication types, and a variable to store which type is used for this deployment based on the value of the parameter.</span></span>

    "variables": {
      "osProfile": "[variables(concat('osProfile', parameters('authenticationType')))]",
      "osProfilepassword": {
        "adminPassword": "[parameters('adminPassword')]",
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]"
      },
      "osProfilesshPublicKey": {
        "adminUsername": "notused",
        "computerName": "[parameters('vmName')]",
        "customData": "[base64(variables('customData'))]",
        "linuxConfiguration": {
          "disablePasswordAuthentication": "true",
          "ssh": {
            "publicKeys": [
              {
                "keyData": "[parameters('sshPublicKey')]",
                "path": "/home/notused/.ssh/authorized_keys"
              }
            ]
          }
        }
      }
    }

<span data-ttu-id="8dc8a-216">Ao definir a máquina virtual, você define o **osProfile** para a variável que criou.</span><span class="sxs-lookup"><span data-stu-id="8dc8a-216">When defining the virtual machine, you set the **osProfile** to the variable you created.</span></span>

    {
      "type": "Microsoft.Compute/virtualMachines",
      ...
      "osProfile": "[variables('osProfile')]"
    }


## <a name="next-steps"></a><span data-ttu-id="8dc8a-217">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8dc8a-217">Next steps</span></span>
* <span data-ttu-id="8dc8a-218">Para saber mais sobre as seções do modelo, confira [Criando modelos do Azure Resource Manager](resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="8dc8a-218">To learn about the sections of the template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="8dc8a-219">Para ver as funções que estão disponíveis em um modelo, confira [Funções do modelo do Azure Resource Manager](resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="8dc8a-219">To see the functions that are available within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md)</span></span>
