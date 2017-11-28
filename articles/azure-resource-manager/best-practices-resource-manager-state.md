---
title: valores complexos de aaaPass entre modelos do Azure | Microsoft Docs
description: Mostra recomendado abordagens para usar dados de estado de tooshare objetos complexos com modelos de Gerenciador de recursos do Azure e vinculado.
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
ms.openlocfilehash: 72df1dee351446cea6ce15269e6db288b1f1db79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="share-state-tooand-from-azure-resource-manager-templates"></a><span data-ttu-id="3916d-103">Tooand de estado de compartilhamento de modelos do Gerenciador de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="3916d-103">Share state tooand from Azure Resource Manager templates</span></span>
<span data-ttu-id="3916d-104">Este tópico mostra as melhores práticas para gerenciar e compartilhar o estado em modelos.</span><span class="sxs-lookup"><span data-stu-id="3916d-104">This topic shows best practices for managing and sharing state within templates.</span></span> <span data-ttu-id="3916d-105">Olá parâmetros e variáveis mostrados neste tópico são exemplos de tipo de saudação de objetos que você pode definir tooconveniently organizar seus requisitos de implantação.</span><span class="sxs-lookup"><span data-stu-id="3916d-105">hello parameters and variables shown in this topic are examples of hello type of objects you can define tooconveniently organize your deployment requirements.</span></span> <span data-ttu-id="3916d-106">A partir desses exemplos, você pode implementar seus próprios objetos com valores de propriedade que façam sentido para o seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="3916d-106">From these examples, you can implement your own objects with property values that make sense for your environment.</span></span>

<span data-ttu-id="3916d-107">Este tópico faz parte de um whitepaper mais amplo.</span><span class="sxs-lookup"><span data-stu-id="3916d-107">This topic is part of a larger whitepaper.</span></span> <span data-ttu-id="3916d-108">baixar tooread Olá completo papel, [World classe recurso Gerenciador de modelos de considerações e práticas comprovadas](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).</span><span class="sxs-lookup"><span data-stu-id="3916d-108">tooread hello full paper, download [World Class Resource Manager Templates Considerations and Proven Practices](http://download.microsoft.com/download/8/E/1/8E1DBEFA-CECE-4DC9-A813-93520A5D7CFE/World Class ARM Templates - Considerations and Proven Practices.pdf).</span></span>

## <a name="provide-standard-configuration-settings"></a><span data-ttu-id="3916d-109">Fornecer configurações padrão</span><span class="sxs-lookup"><span data-stu-id="3916d-109">Provide standard configuration settings</span></span>
<span data-ttu-id="3916d-110">Em vez de oferecer um modelo que oferece total flexibilidade e inúmeras variações, um padrão comum é tooprovide uma seleção de configurações conhecidas.</span><span class="sxs-lookup"><span data-stu-id="3916d-110">Rather than offer a template that provides total flexibility and countless variations, a common pattern is tooprovide a selection of known configurations.</span></span> <span data-ttu-id="3916d-111">Na verdade, os usuários podem selecionar tamanhos de camiseta padrão, como área restrita, pequeno, médio e grande.</span><span class="sxs-lookup"><span data-stu-id="3916d-111">In effect, users can select standard t-shirt sizes such as sandbox, small, medium, and large.</span></span> <span data-ttu-id="3916d-112">Outros exemplos de tamanhos de camiseta são ofertas de produtos, como community edition ou enterprise edition.</span><span class="sxs-lookup"><span data-stu-id="3916d-112">Other examples of t-shirt sizes are product offerings, such as community edition or enterprise edition.</span></span> <span data-ttu-id="3916d-113">Em outros casos, podem se tratar de configurações de uma tecnologia específicas para uma determinada carga de trabalho - como mapear/reduzir ou no SQL.</span><span class="sxs-lookup"><span data-stu-id="3916d-113">In other cases, it may be workload-specific configurations of a technology – such as map reduce or no sql.</span></span>

<span data-ttu-id="3916d-114">Com objetos complexos, você pode criar variáveis que contêm conjuntos de dados, às vezes conhecidos como "recipientes de propriedade" e usar essa declaração de recurso Olá dados toodrive em seu modelo.</span><span class="sxs-lookup"><span data-stu-id="3916d-114">With complex objects, you can create variables that contain collections of data, sometimes known as "property bags" and use that data toodrive hello resource declaration in your template.</span></span> <span data-ttu-id="3916d-115">Essa abordagem fornece boas configurações conhecidas, de tamanhos variados que são pré-configurados para os clientes.</span><span class="sxs-lookup"><span data-stu-id="3916d-115">This approach provides good, known configurations of varying sizes that are preconfigured for customers.</span></span> <span data-ttu-id="3916d-116">Sem configurações conhecidas, os usuários do modelo de saudação devem determinar dimensionamento do cluster em seu próprios, fator em restrições de recursos de plataforma e fazer matemática tooidentify Olá resultante de contas de armazenamento e outros recursos de particionamento (devido tamanho toocluster e restrições de recursos).</span><span class="sxs-lookup"><span data-stu-id="3916d-116">Without known configurations, users of hello template must determine cluster sizing on their own, factor in platform resource constraints, and do math tooidentify hello resulting partitioning of storage accounts and other resources (due toocluster size and resource constraints).</span></span> <span data-ttu-id="3916d-117">Além disso toomaking uma melhor experiência de cliente hello, algumas configurações conhecidas são toosupport mais fácil e podem ajudar a fornecer um nível mais alto de densidade.</span><span class="sxs-lookup"><span data-stu-id="3916d-117">In addition toomaking a better experience for hello customer, a few known configurations are easier toosupport and can help you deliver a higher level of density.</span></span>

<span data-ttu-id="3916d-118">Olá mostrado no exemplo a seguir como toodefine variáveis que contêm objetos complexos para representar os conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="3916d-118">hello following example shows how toodefine variables that contain complex objects for representing collections of data.</span></span> <span data-ttu-id="3916d-119">coleções de saudação definem valores que são usados para o tamanho da máquina virtual, as configurações de rede, configurações do sistema operacional e configurações de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="3916d-119">hello collections define values that are used for virtual machine size, network settings, operating system settings and availability settings.</span></span>

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

<span data-ttu-id="3916d-120">Observe que Olá **tshirtSize** variável concatena o tamanho de camisa Olá fornecido por meio de um parâmetro (**pequeno**, **médio**, **grande**) texto toohello **tshirtSize**.</span><span class="sxs-lookup"><span data-stu-id="3916d-120">Notice that hello **tshirtSize** variable concatenates hello t-shirt size you provided through a parameter (**Small**, **Medium**, **Large**) toohello text **tshirtSize**.</span></span> <span data-ttu-id="3916d-121">Você pode usar essa variável de objeto complexo associado Olá tooretrieve variável para que o tamanho do camisa.</span><span class="sxs-lookup"><span data-stu-id="3916d-121">You use this variable tooretrieve hello associated complex object variable for that t-shirt size.</span></span>

<span data-ttu-id="3916d-122">Você pode fazer referência a essas variáveis posteriormente no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="3916d-122">You can then reference these variables later in hello template.</span></span> <span data-ttu-id="3916d-123">Olá capacidade tooreference chamado variáveis e suas propriedades simplifica a sintaxe do modelo hello e torna fácil toounderstand contexto.</span><span class="sxs-lookup"><span data-stu-id="3916d-123">hello ability tooreference named-variables and their properties simplifies hello template syntax, and makes it easy toounderstand context.</span></span> <span data-ttu-id="3916d-124">saudação de exemplo a seguir define toodeploy um recurso por meio de objetos de saudação mostrados anteriormente tooset valores.</span><span class="sxs-lookup"><span data-stu-id="3916d-124">hello following example defines a resource toodeploy by using hello objects shown previously tooset values.</span></span> <span data-ttu-id="3916d-125">Por exemplo, Olá tamanho da VM é definido pela recuperação do valor de saudação de `variables('tshirtSize').vmSize` enquanto o valor de saudação para o tamanho do disco Olá é recuperado do `variables('tshirtSize').diskSize`.</span><span class="sxs-lookup"><span data-stu-id="3916d-125">For example, hello VM size is set by retrieving hello value for `variables('tshirtSize').vmSize` while hello value for hello disk size is retrieved from `variables('tshirtSize').diskSize`.</span></span> <span data-ttu-id="3916d-126">Além disso, Olá URI para um modelo vinculado é definido com valor de saudação para `variables('tshirtSize').vmTemplate`.</span><span class="sxs-lookup"><span data-stu-id="3916d-126">In addition, hello URI for a linked template is set with hello value for `variables('tshirtSize').vmTemplate`.</span></span>

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

## <a name="pass-state-tooa-template"></a><span data-ttu-id="3916d-127">Passar o modelo de tooa de estado</span><span class="sxs-lookup"><span data-stu-id="3916d-127">Pass state tooa template</span></span>
<span data-ttu-id="3916d-128">Você pode compartilhar o estado em um modelo por meio de parâmetros fornecidos diretamente durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="3916d-128">You share state into a template through parameters that you provide directly during deployment.</span></span>

<span data-ttu-id="3916d-129">Olá tabela parâmetros de listas usadas nos modelos a seguir.</span><span class="sxs-lookup"><span data-stu-id="3916d-129">hello following table lists commonly used parameters in templates.</span></span>

| <span data-ttu-id="3916d-130">Nome</span><span class="sxs-lookup"><span data-stu-id="3916d-130">Name</span></span> | <span data-ttu-id="3916d-131">Valor</span><span class="sxs-lookup"><span data-stu-id="3916d-131">Value</span></span> | <span data-ttu-id="3916d-132">Descrição</span><span class="sxs-lookup"><span data-stu-id="3916d-132">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3916d-133">location</span><span class="sxs-lookup"><span data-stu-id="3916d-133">location</span></span> |<span data-ttu-id="3916d-134">Cadeia de caracteres de uma lista restrita de regiões do Azure</span><span class="sxs-lookup"><span data-stu-id="3916d-134">String from a constrained list of Azure regions</span></span> |<span data-ttu-id="3916d-135">local de saudação onde os recursos de saudação são implantados.</span><span class="sxs-lookup"><span data-stu-id="3916d-135">hello location where hello resources are deployed.</span></span> |
| <span data-ttu-id="3916d-136">storageAccountNamePrefix</span><span class="sxs-lookup"><span data-stu-id="3916d-136">storageAccountNamePrefix</span></span> |<span data-ttu-id="3916d-137">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="3916d-137">String</span></span> |<span data-ttu-id="3916d-138">Nome DNS exclusivo para Olá conta de armazenamento em que os discos da VM Olá são colocados</span><span class="sxs-lookup"><span data-stu-id="3916d-138">Unique DNS name for hello Storage Account where hello VM's disks are placed</span></span> |
| <span data-ttu-id="3916d-139">domainName</span><span class="sxs-lookup"><span data-stu-id="3916d-139">domainName</span></span> |<span data-ttu-id="3916d-140">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="3916d-140">String</span></span> |<span data-ttu-id="3916d-141">Nome de domínio do hello jumpbox VM publicamente acessível no formato Olá: **{domainName}. { local}.cloudapp.com** por exemplo: **mydomainname.westus.cloudapp.azure.com**</span><span class="sxs-lookup"><span data-stu-id="3916d-141">Domain name of hello publicly accessible jumpbox VM in hello format: **{domainName}.{location}.cloudapp.com** For example: **mydomainname.westus.cloudapp.azure.com**</span></span> |
| <span data-ttu-id="3916d-142">adminUsername</span><span class="sxs-lookup"><span data-stu-id="3916d-142">adminUsername</span></span> |<span data-ttu-id="3916d-143">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="3916d-143">String</span></span> |<span data-ttu-id="3916d-144">Nome de usuário para Olá VMs</span><span class="sxs-lookup"><span data-stu-id="3916d-144">Username for hello VMs</span></span> |
| <span data-ttu-id="3916d-145">adminPassword</span><span class="sxs-lookup"><span data-stu-id="3916d-145">adminPassword</span></span> |<span data-ttu-id="3916d-146">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="3916d-146">String</span></span> |<span data-ttu-id="3916d-147">Senha de saudação VMs</span><span class="sxs-lookup"><span data-stu-id="3916d-147">Password for hello VMs</span></span> |
| <span data-ttu-id="3916d-148">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="3916d-148">tshirtSize</span></span> |<span data-ttu-id="3916d-149">Cadeia de caracteres de uma lista restrita de tamanhos de camiseta oferecidos</span><span class="sxs-lookup"><span data-stu-id="3916d-149">String from a constrained list of offered t-shirt sizes</span></span> |<span data-ttu-id="3916d-150">Olá denominado tooprovision de tamanho de unidade de escala.</span><span class="sxs-lookup"><span data-stu-id="3916d-150">hello named scale unit size tooprovision.</span></span> <span data-ttu-id="3916d-151">Por exemplo, "Pequeno", "Médio", "Grande"</span><span class="sxs-lookup"><span data-stu-id="3916d-151">For example, "Small", "Medium", "Large"</span></span> |
| <span data-ttu-id="3916d-152">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="3916d-152">virtualNetworkName</span></span> |<span data-ttu-id="3916d-153">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="3916d-153">String</span></span> |<span data-ttu-id="3916d-154">Nome de rede virtual Olá Olá consumidor deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="3916d-154">Name of hello virtual network that hello consumer wants toouse.</span></span> |
| <span data-ttu-id="3916d-155">enableJumpbox</span><span class="sxs-lookup"><span data-stu-id="3916d-155">enableJumpbox</span></span> |<span data-ttu-id="3916d-156">Cadeia de caracteres de uma lista restrita (habilitada/desabilitada)</span><span class="sxs-lookup"><span data-stu-id="3916d-156">String from a constrained list (enabled/disabled)</span></span> |<span data-ttu-id="3916d-157">Parâmetro identifica se tooenable um jumpbox para o ambiente de saudação.</span><span class="sxs-lookup"><span data-stu-id="3916d-157">Parameter that identifies whether tooenable a jumpbox for hello environment.</span></span> <span data-ttu-id="3916d-158">Valores: "habilitado", "desabilitado"</span><span class="sxs-lookup"><span data-stu-id="3916d-158">Values: "enabled", "disabled"</span></span> |

<span data-ttu-id="3916d-159">Olá **tshirtSize** parâmetro usado na seção anterior Olá é definido como:</span><span class="sxs-lookup"><span data-stu-id="3916d-159">hello **tshirtSize** parameter used in hello previous section is defined as:</span></span>

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
          "Description": "T-shirt size of hello MongoDB deployment"
        }
      }
    }


## <a name="pass-state-toolinked-templates"></a><span data-ttu-id="3916d-160">Passar modelos de toolinked de estado</span><span class="sxs-lookup"><span data-stu-id="3916d-160">Pass state toolinked templates</span></span>
<span data-ttu-id="3916d-161">Ao se conectar toolinked modelos, você geralmente usa uma combinação de estático e gerado variáveis.</span><span class="sxs-lookup"><span data-stu-id="3916d-161">When connecting toolinked templates, you often use a mix of static and generated variables.</span></span>

### <a name="static-variables"></a><span data-ttu-id="3916d-162">Variáveis estáticas</span><span class="sxs-lookup"><span data-stu-id="3916d-162">Static variables</span></span>
<span data-ttu-id="3916d-163">Variáveis estáticas geralmente são valores de base de tooprovide usadas, como URLs, que são usados em um modelo.</span><span class="sxs-lookup"><span data-stu-id="3916d-163">Static variables are often used tooprovide base values, such as URLs, that are used throughout a template.</span></span>

<span data-ttu-id="3916d-164">Em Olá seguinte trecho do modelo, `templateBaseUrl` Especifica o local de raiz de saudação para modelo Olá no GitHub.</span><span class="sxs-lookup"><span data-stu-id="3916d-164">In hello following template excerpt, `templateBaseUrl` specifies hello root location for hello template in GitHub.</span></span> <span data-ttu-id="3916d-165">linha seguinte Olá cria uma nova variável `sharedTemplateUrl` que concatena a URL base Olá com nome conhecido de saudação do modelo de recursos compartilhados hello.</span><span class="sxs-lookup"><span data-stu-id="3916d-165">hello next line builds a new variable `sharedTemplateUrl` that concatenates hello base URL with hello known name of hello shared resources template.</span></span> <span data-ttu-id="3916d-166">Abaixo da linha, uma variável de objeto complexo toostore usado um tamanho de camisa, onde é URL base Olá toohello concatenado conhecido local do modelo de configuração e armazenadas em Olá `vmTemplate` propriedade.</span><span class="sxs-lookup"><span data-stu-id="3916d-166">Below that line, a complex object variable is used toostore a t-shirt size, where hello base URL is concatenated toohello known configuration template location and stored in hello `vmTemplate` property.</span></span>

<span data-ttu-id="3916d-167">benefício de saudação dessa abordagem é que se Olá modelo local será alterado, basta variável estática do hello toochange em um único local, que passa em modelos Olá vinculado.</span><span class="sxs-lookup"><span data-stu-id="3916d-167">hello benefit of this approach is that if hello template location changes, you only need toochange hello static variable in one place, which passes it throughout hello linked templates.</span></span>

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

### <a name="generated-variables"></a><span data-ttu-id="3916d-168">Variáveis geradas</span><span class="sxs-lookup"><span data-stu-id="3916d-168">Generated variables</span></span>
<span data-ttu-id="3916d-169">Em variáveis de toostatic de adição, diversas variáveis são geradas dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="3916d-169">In addition toostatic variables, several variables are generated dynamically.</span></span> <span data-ttu-id="3916d-170">Esta seção identifica alguns dos tipos comuns de saudação de variáveis gerados.</span><span class="sxs-lookup"><span data-stu-id="3916d-170">This section identifies some of hello common types of generated variables.</span></span>

#### <a name="tshirtsize"></a><span data-ttu-id="3916d-171">tshirtSize</span><span class="sxs-lookup"><span data-stu-id="3916d-171">tshirtSize</span></span>
<span data-ttu-id="3916d-172">Você está familiarizado com essa variável gerado de exemplos de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="3916d-172">You are familiar with this generated variable from hello examples above.</span></span>

#### <a name="networksettings"></a><span data-ttu-id="3916d-173">networkSettings</span><span class="sxs-lookup"><span data-stu-id="3916d-173">networkSettings</span></span>
<span data-ttu-id="3916d-174">Em uma saudação de capacidade, recurso ou modelo de solução de ponta a ponta no escopo, vinculados modelos normalmente criam recursos que existem em uma rede.</span><span class="sxs-lookup"><span data-stu-id="3916d-174">In a capacity, capability, or end-to-end scoped solution template, hello linked templates typically create resources that exist on a network.</span></span> <span data-ttu-id="3916d-175">Uma abordagem simples é toouse as configurações de rede objeto complexo toostore e passá-las toolinked modelos.</span><span class="sxs-lookup"><span data-stu-id="3916d-175">One straightforward approach is toouse a complex object toostore network settings and pass them toolinked templates.</span></span>

<span data-ttu-id="3916d-176">Um exemplo de configurações de rede de comunicação pode ser visto abaixo.</span><span class="sxs-lookup"><span data-stu-id="3916d-176">An example of communicating network settings can be seen below.</span></span>

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

#### <a name="availabilitysettings"></a><span data-ttu-id="3916d-177">availabilitySettings</span><span class="sxs-lookup"><span data-stu-id="3916d-177">availabilitySettings</span></span>
<span data-ttu-id="3916d-178">Recursos criados em modelos vinculados geralmente são colocados em um conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="3916d-178">Resources created in linked templates are often placed in an availability set.</span></span> <span data-ttu-id="3916d-179">Em Olá exemplo a seguir, Olá nome do conjunto de disponibilidade for especificado e também Olá domínio de falha e toouse de contagem de domínio de atualização.</span><span class="sxs-lookup"><span data-stu-id="3916d-179">In hello following example, hello availability set name is specified and also hello fault domain and update domain count toouse.</span></span>

    "availabilitySetSettings": {
      "name": "pgsqlAvailabilitySet",
      "fdCount": 3,
      "udCount": 5
    }

<span data-ttu-id="3916d-180">Se você precisar de vários conjuntos de disponibilidade (por exemplo, um de nós mestres) e outro para os nós de dados, você pode usar um nome como um prefixo, especifique vários conjuntos de disponibilidade ou siga modelo Olá mostrado anteriormente para a criação de uma variável para um tamanho de camisa específico.</span><span class="sxs-lookup"><span data-stu-id="3916d-180">If you need multiple availability sets (for example, one for master nodes and another for data nodes), you can use a name as a prefix, specify multiple availability sets, or follow hello model shown earlier for creating a variable for a specific t-shirt size.</span></span>

#### <a name="storagesettings"></a><span data-ttu-id="3916d-181">storageSettings</span><span class="sxs-lookup"><span data-stu-id="3916d-181">storageSettings</span></span>
<span data-ttu-id="3916d-182">Detalhes de armazenamento geralmente são compartilhados com modelos vinculados.</span><span class="sxs-lookup"><span data-stu-id="3916d-182">Storage details are often shared with linked templates.</span></span> <span data-ttu-id="3916d-183">No exemplo abaixo, a saudação um *storageSettings* objeto fornece detalhes sobre Olá nomes de conta e o contêiner de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3916d-183">In hello example below, a *storageSettings* object provides details about hello storage account and container names.</span></span>

    "storageSettings": {
        "vhdStorageAccountName": "[parameters('storageAccountName')]",
        "vhdContainerName": "[variables('vmStorageAccountContainerName')]",
        "destinationVhdsContainer": "[concat('https://', parameters('storageAccountName'), variables('vmStorageAccountDomain'), '/', variables('vmStorageAccountContainerName'), '/')]"
    }

#### <a name="ossettings"></a><span data-ttu-id="3916d-184">osSettings</span><span class="sxs-lookup"><span data-stu-id="3916d-184">osSettings</span></span>
<span data-ttu-id="3916d-185">Com modelos vinculados, talvez seja necessário toopass configurações de sistema operacional toovarious tipos de nós em todos os tipos de configuração diferentes.</span><span class="sxs-lookup"><span data-stu-id="3916d-185">With linked templates, you may need toopass operating system settings toovarious nodes types across different known configuration types.</span></span> <span data-ttu-id="3916d-186">Um objeto complexo é uma informações do sistema operacional toostore e compartilhamento de maneira fácil e também torna mais fácil toosupport várias opções de sistema operacional para implantação.</span><span class="sxs-lookup"><span data-stu-id="3916d-186">A complex object is an easy way toostore and share operating system information and also makes it easier toosupport multiple operating system choices for deployment.</span></span>

<span data-ttu-id="3916d-187">Olá, exemplo a seguir mostra um objeto para *osSettings*:</span><span class="sxs-lookup"><span data-stu-id="3916d-187">hello following example shows an object for *osSettings*:</span></span>

    "osSettings": {
      "imageReference": {
        "publisher": "Canonical",
        "offer": "UbuntuServer",
        "sku": "14.04.2-LTS",
        "version": "latest"
      }
    }

#### <a name="machinesettings"></a><span data-ttu-id="3916d-188">machineSettings</span><span class="sxs-lookup"><span data-stu-id="3916d-188">machineSettings</span></span>
<span data-ttu-id="3916d-189">Variável gerada, *machineSettings* é um objeto complexo que contém uma mistura de variáveis principais para criar uma VM.</span><span class="sxs-lookup"><span data-stu-id="3916d-189">A generated variable, *machineSettings* is a complex object containing a mix of core variables for creating a VM.</span></span> <span data-ttu-id="3916d-190">variáveis de saudação incluem o nome de usuário administrador e senha, um prefixo para nomes VM hello e uma referência de imagem do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="3916d-190">hello variables include administrator user name and password, a prefix for hello VM names, and an operating system image reference.</span></span>

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

<span data-ttu-id="3916d-191">Observe que *osImageReference* recupera Olá valores de saudação *osSettings* variável definida no modelo principal hello.</span><span class="sxs-lookup"><span data-stu-id="3916d-191">Note that *osImageReference* retrieves hello values from hello *osSettings* variable defined in hello main template.</span></span> <span data-ttu-id="3916d-192">Isso significa que você pode facilmente alterar o sistema operacional de saudação para uma VM — completamente ou com base na preferência de saudação de um consumidor de modelo.</span><span class="sxs-lookup"><span data-stu-id="3916d-192">That means you can easily change hello operating system for a VM—entirely or based on hello preference of a template consumer.</span></span>

#### <a name="vmscripts"></a><span data-ttu-id="3916d-193">vmScripts</span><span class="sxs-lookup"><span data-stu-id="3916d-193">vmScripts</span></span>
<span data-ttu-id="3916d-194">Olá *vmScripts* contém detalhes sobre toodownload de scripts de saudação do objeto e executar em uma instância VM, incluindo referências externas e internas.</span><span class="sxs-lookup"><span data-stu-id="3916d-194">hello *vmScripts* object contains details about hello scripts toodownload and execute on a VM instance, including outside and inside references.</span></span> <span data-ttu-id="3916d-195">Fora de referências incluem infraestrutura hello.</span><span class="sxs-lookup"><span data-stu-id="3916d-195">Outside references include hello infrastructure.</span></span>
<span data-ttu-id="3916d-196">Referências internas incluem hello instalado software instalado e configuração.</span><span class="sxs-lookup"><span data-stu-id="3916d-196">Inside references include hello installed software installed and configuration.</span></span>

<span data-ttu-id="3916d-197">Use Olá *scriptsToDownload* toodownload toohello VM de scripts de saudação do toolist de propriedade.</span><span class="sxs-lookup"><span data-stu-id="3916d-197">You use hello *scriptsToDownload* property toolist hello scripts toodownload toohello VM.</span></span> <span data-ttu-id="3916d-198">Esse objeto também contém argumentos de linha de toocommand de referências para diferentes tipos de ações.</span><span class="sxs-lookup"><span data-stu-id="3916d-198">This object also contains references toocommand-line arguments for different types of actions.</span></span> <span data-ttu-id="3916d-199">Essas ações incluem executar saudação padrão instalação para cada nó individual, uma instalação que é executado depois que todos os nós são implantados e quaisquer scripts adicionais que podem ser tooa específico, considerando o modelo.</span><span class="sxs-lookup"><span data-stu-id="3916d-199">These actions include executing hello default installation for each individual node, an installation that runs after all nodes are deployed, and any additional scripts that may be specific tooa given template.</span></span>

<span data-ttu-id="3916d-200">Este exemplo é de um toodeploy MongoDB, que exige uma arbitrador toodeliver alta disponibilidade do modelo usado.</span><span class="sxs-lookup"><span data-stu-id="3916d-200">This example is from a template used toodeploy MongoDB, which requires an arbiter toodeliver high availability.</span></span> <span data-ttu-id="3916d-201">Olá *arbiterNodeInstallCommand* foi adicionado muito*vmScripts* tooinstall arbitrador de saudação.</span><span class="sxs-lookup"><span data-stu-id="3916d-201">hello *arbiterNodeInstallCommand* has been added too*vmScripts* tooinstall hello arbiter.</span></span>

<span data-ttu-id="3916d-202">seção de variáveis de saudação é onde você pode encontrar variáveis Olá que definem o script de saudação de tooexecute Olá texto específico com valores adequados hello.</span><span class="sxs-lookup"><span data-stu-id="3916d-202">hello variables section is where you find hello variables that define hello specific text tooexecute hello script with hello proper values.</span></span>

    "vmScripts": {
        "scriptsToDownload": [
            "[concat(variables('scriptUrl'), 'mongodb-', variables('osFamilySpec').osName, '-install.sh')]",
            "[concat(variables('sharedScriptUrl'), 'vm-disk-utils-0.1.sh')]"
        ],
        "regularNodeInstallCommand": "[variables('installCommand')]",
        "lastNodeInstallCommand": "[concat(variables('installCommand'), ' -l')]",
        "arbiterNodeInstallCommand": "[concat(variables('installCommand'), ' -a')]"
    },


## <a name="return-state-from-a-template"></a><span data-ttu-id="3916d-203">Retornar o estado de um modelo</span><span class="sxs-lookup"><span data-stu-id="3916d-203">Return state from a template</span></span>
<span data-ttu-id="3916d-204">Não só pode transmitir dados em um modelo, você também pode compartilhar dados toohello back chamada modelo.</span><span class="sxs-lookup"><span data-stu-id="3916d-204">Not only can you pass data into a template, you can also share data back toohello calling template.</span></span> <span data-ttu-id="3916d-205">Em Olá **gera** seção de um modelo vinculado, você pode fornecer os pares chave/valor que podem ser consumidos pelo modelo de origem de saudação.</span><span class="sxs-lookup"><span data-stu-id="3916d-205">In hello **outputs** section of a linked template, you can provide key/value pairs that can be consumed by hello source template.</span></span>

<span data-ttu-id="3916d-206">Olá exemplo a seguir mostra como toopass Olá endereço IP privado gerado em um modelo vinculado.</span><span class="sxs-lookup"><span data-stu-id="3916d-206">hello following example shows how toopass hello private IP address generated in a linked template.</span></span>

    "outputs": {
        "masterip": {
            "value": "[reference(concat(variables('nicName'),0)).ipConfigurations[0].properties.privateIPAddress]",
            "type": "string"
         }
    }

<span data-ttu-id="3916d-207">No modelo principal do hello, você pode usar esses dados com hello sintaxe a seguir:</span><span class="sxs-lookup"><span data-stu-id="3916d-207">Within hello main template, you can use that data with hello following syntax:</span></span>

    "[reference('master-node').outputs.masterip.value]"

<span data-ttu-id="3916d-208">Você pode usar essa expressão em Olá saídas seção ou seção de recursos de saudação do modelo principal hello.</span><span class="sxs-lookup"><span data-stu-id="3916d-208">You can use this expression in either hello outputs section or hello resources section of hello main template.</span></span> <span data-ttu-id="3916d-209">Você não pode usar a expressão Olá na seção de variáveis de saudação porque ele se baseia no estado de tempo de execução de saudação.</span><span class="sxs-lookup"><span data-stu-id="3916d-209">You cannot use hello expression in hello variables section because it relies on hello runtime state.</span></span> <span data-ttu-id="3916d-210">tooreturn este valor de modelo principal hello, use:</span><span class="sxs-lookup"><span data-stu-id="3916d-210">tooreturn this value from hello main template, use:</span></span>

    "outputs": {
      "masterIpAddress": {
        "value": "[reference('master-node').outputs.masterip.value]",
        "type": "string"
      }

<span data-ttu-id="3916d-211">Para um exemplo de como usar o hello gera seção um modelo vinculado tooreturn de discos de dados para uma máquina virtual, consulte [criando vários discos de dados para uma máquina Virtual](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="3916d-211">For an example of using hello outputs section of a linked template tooreturn data disks for a virtual machine, see [Creating multiple data disks for a Virtual Machine](resource-group-create-multiple.md).</span></span>

## <a name="define-authentication-settings-for-virtual-machine"></a><span data-ttu-id="3916d-212">Definir configurações de autenticação para uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="3916d-212">Define authentication settings for virtual machine</span></span>
<span data-ttu-id="3916d-213">Você pode usar o hello mesmo padrão mostrado anteriormente configurações toospecify Olá autenticação as definições de configuração para uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="3916d-213">You can use hello same pattern shown previously for configuration settings toospecify hello authentication settings for a virtual machine.</span></span> <span data-ttu-id="3916d-214">Você pode criar um parâmetro para passar no tipo de saudação de autenticação.</span><span class="sxs-lookup"><span data-stu-id="3916d-214">You create a parameter for passing in hello type of authentication.</span></span>

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

<span data-ttu-id="3916d-215">Você adicionar variáveis de saudação diferentes tipos de autenticação e uma variável toostore o tipo usado para essa implantação com base no valor de saudação do parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="3916d-215">You add variables for hello different authentication types, and a variable toostore which type is used for this deployment based on hello value of hello parameter.</span></span>

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

<span data-ttu-id="3916d-216">Ao definir a máquina virtual de saudação, você definir Olá **osProfile** toohello variável que você criou.</span><span class="sxs-lookup"><span data-stu-id="3916d-216">When defining hello virtual machine, you set hello **osProfile** toohello variable you created.</span></span>

    {
      "type": "Microsoft.Compute/virtualMachines",
      ...
      "osProfile": "[variables('osProfile')]"
    }


## <a name="next-steps"></a><span data-ttu-id="3916d-217">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3916d-217">Next steps</span></span>
* <span data-ttu-id="3916d-218">toolearn sobre seções de saudação do modelo hello, consulte [criação de modelos de Gerenciador de recursos do Azure](resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="3916d-218">toolearn about hello sections of hello template, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="3916d-219">toosee Olá funções que estão disponíveis em um modelo, consulte [funções de modelo do Gerenciador de recursos do Azure](resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="3916d-219">toosee hello functions that are available within a template, see [Azure Resource Manager Template Functions](resource-group-template-functions.md)</span></span>
