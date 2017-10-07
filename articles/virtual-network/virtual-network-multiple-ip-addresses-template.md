---
title: "aaaMultiple endereços IP para máquinas virtuais do Azure - modelo | Microsoft Docs"
description: "Saiba como tooassign vários endereços IP tooa máquina de virtual usando um modelo do Gerenciador de recursos do Azure."
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/08/2016
ms.author: jdial
ms.openlocfilehash: e7660257b2d5c7da4b8b86771abe51a2c5012fa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-an-azure-resource-manager-template"></a>Atribuir vários endereços IP toovirtual máquinas usando um modelo do Gerenciador de recursos do Azure

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

Este artigo explica como toocreate uma máquina virtual (VM) por meio da implantação do Azure Resource Manager Olá modelo usando um modelo do Gerenciador de recursos. Vários endereços públicos e privados de IP não podem ser atribuídos a toohello NIC mesmo ao implantar uma VM por meio do modelo de implantação clássico hello. toolearn mais sobre modelos de implantação do Azure, leia Olá [entender os modelos de implantação](../resource-manager-deployment-model.md) artigo.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name="template-description"></a>Descrição do modelo

Implantar um modelo permite que você tooquickly e consistentemente criar recursos do Azure com valores de configuração diferentes. Saudação de leitura [passo a passo do Gerenciador de recursos modelo](../azure-resource-manager/resource-manager-template-walkthrough.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigo se você não estiver familiarizado com modelos do Gerenciador de recursos do Azure. Olá [implantar uma VM com vários endereços IP](https://azure.microsoft.com/resources/templates/101-vm-multiple-ipconfig) modelo utilizado neste artigo.

<a name="resources"></a>Modelo de implantação Olá cria Olá recursos a seguir:

|Recurso|Nome|Descrição|
|---|---|---|
|Interface de rede|*myNic1*|configurações de IP três Olá descritas na seção de cenário Olá deste artigo são criadas e atribuídas toothis NIC.|
|Recurso de endereço IP público|2 são criados: *myPublicIP* e *myPublicIP2*|Esses recursos são atribuídos endereços IP públicos estáticos e recebem toohello *IPConfig 1* e *2 IPConfig* descritas no cenário de saudação de configurações de IP.|
|VM|*myVM1*|Uma VM DS3 Standard.|
|Rede virtual|*myVNet1*|Crie uma rede virtual com uma sub-rede denominada *mySubnet*.|
|Conta de armazenamento|Implantação de toohello exclusivo|Uma conta de armazenamento.|

<a name="parameters"></a>Ao implantar o modelo Olá, você deve especificar valores para Olá parâmetros a seguir:

|Nome|Descrição|
|---|---|
|adminUsername|Nome de usuário do administrador. saudação de nome de usuário deve estar em conformidade com [requisitos de nome de usuário do Azure](../virtual-machines/windows/faq.md?toc=%2fazure%2fvirtual-network%2ftoc.json).|
|adminPassword|Senha de saudação de senha do administrador deve estar em conformidade com [requisitos de senha do Azure](../virtual-machines/windows/faq.md?toc=%2fazure%2fvirtual-network%2ftoc.json#what-are-the-password-requirements-when-creating-a-vm).|
|dnsLabelPrefix|Nome DNS para PublicIPAddressName1. nome DNS Olá resolverá tooone de endereços IP públicos Olá atribuído toohello VM. Olá nome deve ser exclusivo dentro de hello Azure região (local) criar hello VM.|
|dnsLabelPrefix1|Nome DNS para PublicIPAddressName2. nome DNS Olá resolverá tooone de endereços IP públicos Olá atribuído toohello VM. Olá nome deve ser exclusivo dentro de hello Azure região (local) criar hello VM.|
|OSVersion|versão do Windows/Linux Olá para Olá VM. sistema operacional de saudação é uma imagem totalmente atualizada de saudação fornecida Windows/Linux versão selecionada.|
|imagePublisher|Editor de imagem do Windows/Linux de saudação para Olá selecionado de VM.|
|imageOffer|imagem do Windows/Linux Olá Olá selecionado de VM.|

Cada um dos recursos de saudação implantados pelo modelo de saudação é configurada com várias configurações padrão. Você pode exibir essas configurações por meio de qualquer um dos métodos a seguir de saudação:

- **Modelo de exibição de saudação no GitHub:** se você estiver familiarizado com modelos, você pode exibir configurações Olá Olá [modelo](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json).
- **Exibir configurações de saudação depois de implantar:** se você não estiver familiarizado com modelos, você pode implantar modelo hello usando as etapas em uma das seguintes seções de saudação e, em seguida, exibir configurações de saudação após a implantação.

Você pode usar Olá portal do Azure, o PowerShell ou o modelo de saudação do hello Azure interface de linha de comando (CLI) toodeploy. Todos os métodos geram Olá mesmo resultado. modelo de saudação toodeploy, Olá completa etapas em uma saudação seções a seguir:

## <a name="deploy-using-hello-azure-portal"></a>Implantar usando Olá portal do Azure

etapas do modelo de saudação toodeploy usando Olá portal do Azure, Olá completo a seguir:

1. Modificar modelo hello, se desejado. modelo Olá implanta recursos hello e configurações listadas Olá [recursos](#resources) deste artigo. toolearn mais sobre modelos e como tooauthor-los, leia hello [modelos de autoria do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-network%2ftoc.json)artigo.
2. Implante o modelo de saudação com uma saudação métodos a seguir:
    - **Modelo selecione Olá no portal de saudação:** Olá concluir as etapas em Olá [implantar recursos de modelo personalizado](../azure-resource-manager/resource-group-template-deploy-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json#deploy-resources-from-custom-template) artigo. Escolha Olá modelo pré-existente nomeado *101-vm vários ipconfig*.
    - **Diretamente:** clique Olá modelo de saudação do botão tooopen diretamente no portal de saudação a seguir:<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-vm-multiple-ipconfig%2Fazuredeploy.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a>

Independentemente do método hello escolher, você precisará toosupply valores para Olá [parâmetros](#parameters) listadas anteriormente neste artigo. Após Olá VM é implantada, conectar toohello VM e adicionar a saudação privada IP endereços toohello sistema operacional implantado Concluindo Olá etapas Olá [tooa sistema de operacional VM de endereços de IP adicionar](#os-config) deste artigo. Não adicione Olá pública IP endereços toohello sistema operacional.

## <a name="deploy-using-powershell"></a>Implantar usando o PowerShell

modelo de saudação toodeploy usando o PowerShell, Olá concluir as etapas a seguir:

1. Implantar o modelo de saudação completando as etapas de saudação do hello [implantar um modelo com o PowerShell](../azure-resource-manager/resource-group-template-deploy-cli.md) artigo. Olá descreve várias opções para implantar um modelo. Se você escolher toodeploy usando Olá `-TemplateUri parameter`, Olá URI para este modelo é *https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json*. Se você escolher toodeploy usando Olá `-TemplateFile` parâmetro, copia o conteúdo de saudação do hello [arquivo de modelo](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json) do GitHub em um novo arquivo em seu computador. Modificar o conteúdo do modelo hello, se desejado. modelo Olá implanta recursos hello e configurações listadas Olá [recursos](#resources) deste artigo. toolearn mais sobre modelos e como tooauthor-los, leia hello [modelos de autoria do Azure Resource Manager ](../azure-resource-manager/resource-group-authoring-templates.md)artigo.

    Independentemente da opção de saudação escolher toodeploy Olá modelo com, você deve fornecer valores para valores de parâmetro de saudação listados na Olá [parâmetros](#parameters) deste artigo. Se você escolher parâmetros toosupply usando um arquivo de parâmetros, copie o conteúdo Olá Olá [arquivo de parâmetros](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.parameters.json) do GitHub em um novo arquivo em seu computador. Modificar valores hello no arquivo hello. Usar arquivo de saudação criado como valor Olá Olá `-TemplateParameterFile` parâmetro.

    toodetermine os valores válidos para Olá OSVersion, ImagePublisher e imageOffer parâmetros, Olá concluir as etapas em Olá [navegue e selecione artigo de imagens de VM do Windows](../virtual-machines/windows/cli-ps-findimage.md) artigo.

    >[!TIP]
    >Se você não tiver certeza se um dnslabelprefix está disponível, digite Olá `Test-AzureRmDnsAvailability -DomainNameLabel <name-you-want-to-use> -Location <location>` toofind comando out. Se estiver disponível, Olá comando retornará `True`.

2. Após Olá VM é implantada, conectar toohello VM e adicionar a saudação privada IP endereços toohello sistema operacional implantado Concluindo Olá etapas Olá [tooa sistema de operacional VM de endereços de IP adicionar](#os-config) deste artigo. Não adicione Olá pública IP endereços toohello sistema operacional.

## <a name="deploy-using-hello-azure-cli"></a>Implantar usando Olá CLI do Azure

modelo de saudação toodeploy usando hello Azure CLI 1.0, Olá concluir as etapas a seguir:

1. Implantar o modelo de saudação completando as etapas de saudação do hello [implantar um modelo com hello CLI do Azure](../azure-resource-manager/resource-group-template-deploy-cli.md) artigo. Olá descreve várias opções para implantar o modelo de saudação. Se você escolher toodeploy usando Olá `--template-uri` (-f), Olá URI para este modelo é *https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json*. Se você escolher toodeploy usando Olá `--template-file` (-f) parâmetro, copia o conteúdo de saudação do hello [arquivo de modelo](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.json) do GitHub em um novo arquivo em seu computador. Modificar o conteúdo do modelo hello, se desejado. modelo Olá implanta recursos hello e configurações listadas Olá [recursos](#resources) deste artigo. toolearn mais sobre modelos e como tooauthor-los, leia hello [modelos de autoria do Azure Resource Manager ](../azure-resource-manager/resource-group-authoring-templates.md)artigo.

    Independentemente da opção de saudação escolher toodeploy Olá modelo com, você deve fornecer valores para valores de parâmetro de saudação listados na Olá [parâmetros](#parameters) deste artigo. Se você escolher parâmetros toosupply usando um arquivo de parâmetros, copie o conteúdo Olá Olá [arquivo de parâmetros](https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-multiple-ipconfig/azuredeploy.parameters.json) do GitHub em um novo arquivo em seu computador. Modificar valores hello no arquivo hello. Usar arquivo de saudação criado como valor Olá Olá `--parameters-file` (-e) parâmetro.

    toodetermine os valores válidos para Olá OSVersion, ImagePublisher e imageOffer parâmetros, Olá concluir as etapas em Olá [navegue e selecione artigo de imagens de VM do Windows](../virtual-machines/windows/cli-ps-findimage.md) artigo.

2. Após Olá VM é implantada, conectar toohello VM e adicionar a saudação privada IP endereços toohello sistema operacional implantado Concluindo Olá etapas Olá [tooa sistema de operacional VM de endereços de IP adicionar](#os-config) deste artigo. Não adicione Olá pública IP endereços toohello sistema operacional.

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
