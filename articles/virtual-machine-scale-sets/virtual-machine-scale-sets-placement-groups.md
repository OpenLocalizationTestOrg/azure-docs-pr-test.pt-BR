---
title: "aaaWorking com grandes conjuntos de escala de máquina Virtual do Azure | Microsoft Docs"
description: "O que você precisa conjuntos de escala tooknow toouse grande máquina virtual do Azure"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 2/7/2017
ms.author: guybo
ms.openlocfilehash: a39aab25925d7fc50763f0a20148b1f2213b492f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-large-virtual-machine-scale-sets"></a>Trabalhando com conjuntos de dimensionamento grandes de máquinas virtuais
Agora você pode criar Azure [conjuntos de escala de máquina virtual](/azure/virtual-machine-scale-sets/) com uma capacidade de backup too1, 000 VMs. Neste documento, uma _conjunto de escalas da máquina virtual grande_ é definido como uma escala definida capaz de dimensionamento toogreater que 100 VMs. Esse recurso é definido por uma propriedade de conjunto de dimensionamento (_singlePlacementGroup=False_). 

Define determinados aspectos de grande escala, como domínios de falha e de balanceamento de carga se comportam diferentemente tooa conjunto de escala padrão. Este documento explica as características de saudação de conjuntos de grande escala e descreve o que você precisa tooknow toosuccessfully usá-los em seus aplicativos. 

Uma abordagem comum para implantar a infraestrutura de nuvem em grande escala é toocreate um conjunto de _dimensionar unidades_, por exemplo, criando várias VMs dimensionar conjuntos em vários VNETs e contas de armazenamento. Essa abordagem fornece fácil gerenciamento comparado toosingle VMs e várias unidades de escala são úteis para muitos aplicativos, especialmente aqueles que exigem outros componentes empilháveis como várias redes virtuais e os pontos de extremidade. Se seu aplicativo requer um único cluster grande, porém, pode ser mais simples toodeploy uma única escala conjunto de backup too1, 000 VMs. Cenários de exemplo incluem implantações de big data centralizadas ou grades de computação que exigem o gerenciamento simples de um grande pool de nós de trabalho. Combinado com o conjunto de escala VM [discos de dados conectados](virtual-machine-scale-sets-attached-disks.md), conjuntos de grande escala permitem que você toodeploy uma infraestrutura escalável consiste em milhares de núcleos e petabytes de armazenamento, como uma única operação.

## <a name="placement-groups"></a>Grupos de posicionamento 
O que torna uma _grande_ conjunto especial de escala não é número de saudação de VMs, mas o número de saudação de _grupos de posicionamento_ contém. Um grupo de posicionamento é um construção semelhante tooan Azure conjunto de disponibilidade, com seus próprios domínios de falha e domínios de atualização. Por padrão, um conjunto de dimensionamento consiste em um único grupo de posicionamento com tamanho máximo de 100 VMs. Se uma escala de definir a propriedade chamada _singlePlacementGroup_ está definida too_false_, Olá conjunto de escala pode ser composto de vários grupos de posicionamento e tem um intervalo de 0-1.000 VMs. Quando define o valor padrão toohello _true_, um conjunto de escala é composto de um grupo único posicionamento e tem um intervalo de 0 a 100 máquinas virtuais.

## <a name="checklist-for-using-large-scale-sets"></a>Lista de verificação para uso em conjuntos de dimensionamento grandes
toodecide se seu aplicativo pode fazer uso eficiente de conjuntos de grande escala, considere Olá requisitos a seguir:

- Conjuntos de dimensionamento grandes exigem Discos Gerenciados do Azure. Conjuntos de dimensionamento que não são criados com Discos Gerenciados exigem várias contas de armazenamento (uma para cada 20 VMs). Conjuntos de grande escala são toowork projetado exclusivamente com discos gerenciados tooreduce limita seu armazenamento sobrecarga de gerenciamento e tooavoid Olá risco de execução para uma assinatura para contas de armazenamento. Se você não usar discos gerenciados, o conjunto de escala é limitada too100 VMs.
- Conjuntos de escala criados a partir de imagens do Azure Marketplace podem escalar verticalmente too1, 000 VMs.
- Conjuntos de escala criados a partir de imagens personalizadas (imagens VM você criar e carregar por conta própria) atualmente podem escalar verticalmente too100 VMs.
- Camada 4 balanceamento de carga com hello balanceador de carga do Azure ainda não é suportada para conjuntos de escala compostos de vários grupos de posicionamento. Se você precisar Olá toouse balanceador de carga do Azure Certifique-se de escala de saudação definido é toouse configurado um grupo único posicionamento, o que é a configuração padrão de saudação.
- 7 de camada de balanceamento de carga com hello Azure Application Gateway tem suporte para todos os conjuntos de escala.
- Um conjunto de escala é definido com uma única sub-rede - Certifique-se de que sua sub-rede tem um espaço de endereço grande o suficiente para todas as VMs de saudação é necessário. Por padrão, uma escala definida overprovisions (cria VMs adicionais no momento da implantação ou expansão, que você não será cobrado para) tooimprove o desempenho e confiabilidade de implantação. Permitir uma maior que Olá número de VMs planejar tooscale para endereço espaço 20%.
- Se você estiver planejando toodeploy muitas máquinas virtuais, seus limites de cota de núcleos de computação podem ser necessário toobe aumentado.
- Domínios de falha e domínios de atualização só são consistentes dentro de um grupo de posicionamento. Essa arquitetura não altera Olá geral de uma escala de conjunto de disponibilidade, como VMs são distribuídas uniformemente por distinto hardware físico, mas não significa que se você precisar tooguarantee duas VMs estão em um hardware diferente, certifique-se de que estão em diferentes de falha Olá a domínios no mesmo grupo de posicionamento. ID de grupo de domínio e o posicionamento de falha são mostrados no hello _exibição de instância_ de escala de uma conjunto de VM. Você pode exibir a exibição de instância de saudação de um conjunto de escala de VM no hello [Gerenciador de recursos do Azure](https://resources.azure.com/).


## <a name="creating-a-large-scale-set"></a>Criando um conjunto de dimensionamento grande
Quando você cria uma escala definida no hello portal do Azure, você pode permitir que ele tooscale toomultiple posicionamento grupos por configuração Olá _grupo de posicionamento único limite tooa_ too_False_ opção em Olá _Noções básicas sobre_ folha. Com too_False_ de definir essa opção, você pode especificar um _a contagem de instâncias_ valor de backup too1, 000.

![](./media/virtual-machine-scale-sets-placement-groups/portal-large-scale.png)

Você pode criar uma escala VM grande definida usando Olá [CLI do Azure](https://github.com/Azure/azure-cli) _vmss az criar_ comando. Este comando define padrões inteligentes como tamanho da sub-rede com base em Olá _contagem de instâncias_ argumento:

```bash
az group create -l southcentralus -n biginfra
az vmss create -g biginfra -n bigvmss --image ubuntults --instance-count 1000
```
Observe que Olá _vmss criar_ comando padrões determinados valores de configuração se você não especificá-los. toosee Olá opções disponíveis que você pode substituir, tente:
```bash
az vmss create --help
```

Se você estiver criando uma grande escala definida pela composição de um modelo do Azure Resource Manager, verifique se o modelo de saudação cria um conjunto de escala com base em discos gerenciado do Azure. Você pode definir Olá _singlePlacementGroup_ too_false_ de propriedade em Olá _propriedades_ seção Olá _Microsoft.Compute/virtualMAchineScaleSets_ recursos. Olá, fragmento de JSON a seguir mostra a partir de um modelo de conjunto de escala, incluindo a capacidade VM Olá 1.000 e Olá Olá _"singlePlacementGroup": falso_ configuração:
```json
{
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  "location": "australiaeast",
  "name": "bigvmss",
  "sku": {
    "name": "Standard_DS1_v2",
    "tier": "Standard",
    "capacity": 1000
  },
  "properties": {
    "singlePlacementGroup": false,
    "upgradePolicy": {
      "mode": "Automatic"
    }
```
Para obter um exemplo completo de grande escala definida no modelo, consulte muito[https://github.com/gbowerman/azure-myriad/blob/master/bigtest/bigbottle.json](https://github.com/gbowerman/azure-myriad/blob/master/bigtest/bigbottle.json).

## <a name="converting-an-existing-scale-set-toospan-multiple-placement-groups"></a>Converter uma escala existente definido toospan vários grupos de posicionamento
toomake uma escala VM existente definida capaz de dimensionamento toomore que 100 VMs, você precisa Olá toochange _singplePlacementGroup_ too_false_ de propriedade em escala Olá definir modelo. Você pode testar a alteração dessa propriedade com hello [Gerenciador de recursos do Azure](https://resources.azure.com/). Localizar um conjunto de escala existente, selecione _editar_ e alterar Olá _singlePlacementGroup_ propriedade. Se você não vir essa propriedade, você pode estar visualizando escala Olá definida com uma versão mais antiga do hello API Microsoft. Compute.

>[!NOTE] 
Você pode alterar uma conjunto de oferecer suporte a um único posicionamento grupo apenas (comportamento padrão de saudação) tooa dando suporte a vários grupos de posicionamento de escala, mas não é possível converter Olá oposto. Portanto, certifique-se de que entender propriedades Olá dos conjuntos de grande escala antes da conversão. Em particular, certifique-se de que você não precisa de camada 4 balanceamento de carga com hello balanceador de carga do Azure.


