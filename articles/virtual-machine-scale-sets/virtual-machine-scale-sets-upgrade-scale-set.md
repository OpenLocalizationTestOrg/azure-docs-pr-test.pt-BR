---
title: "conjunto de escala de uma máquina virtual do Azure aaaUpgrade | Microsoft Docs"
description: "Atualizar um conjunto de dimensionamento de máquinas virtuais do Azure"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e229664e-ee4e-4f12-9d2e-a4f456989e5d
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: guybo
ms.openlocfilehash: 068e98503f8d37ea71e45b8673a01da2e814f521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-virtual-machine-scale-set"></a>Atualizar um conjunto de escala de máquina virtual
Este artigo descreve como você pode implementar uma escala de máquina virtual do Azure do sistema operacional atualização tooan definida sem qualquer tempo de inatividade. Nesse contexto, uma atualização do sistema operacional envolve alterar versão hello ou SKU do hello SO ou Olá URI de uma imagem personalizada. Atualizar sem tempo de inatividade significa atualizar uma máquina virtual por vez ou em grupos (por exemplo, um domínio de falha por vez), em vez de todas de uma só vez. Ao fazer isso, todas as máquinas virtuais que não estiverem sendo atualizadas podem continuar em execução.

tooavoid ambiguidade, vamos distinguir quatro tipos de atualização do sistema operacional que talvez você queira tooperform:

* Alterar a versão hello ou SKU de uma imagem de plataforma. Por exemplo, a alteração Ubuntu versão 14.04.2-LTS de 14.04.201506100 too14.04.201507060 ou alterando Olá Ubuntu 15.10/mais recente SKU too16.04.0-LTS/latest. Esse cenário é abordado neste artigo.
* Alterando Olá URI que aponta tooa nova versão de uma imagem personalizada criada por você (**propriedades** > **virtualMachineProfile** > **storageProfile**  >  **osDisk** > **imagem** > **uri**). Esse cenário é abordado neste artigo.
* Alterando a referência de imagem de saudação de um conjunto de escala que foi criado usando discos gerenciado do Azure.
* Aplicação de patch Olá SO de dentro de uma máquina virtual (isso exemplos de instalar um patch de segurança e executar o Windows Update). Esse cenário tem suporte, mas não é abordado neste artigo.

Conjuntos de escala de máquina virtual implantados como parte de um cluster do [Azure Service Fabric](https://azure.microsoft.com/services/service-fabric/) não são abordados aqui. Consulte [Patch no SO do Windows no seu cluster de Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-patch-orchestration-application) para obter mais informações sobre aplicação de patch do Service Fabric.

Olá básica sequência para alterar Olá versão/SKU de sistema operacional de uma imagem de plataforma ou Olá URI de uma imagem personalizada será semelhante ao seguinte:

1. Obter o modelo de conjunto de escala de máquina virtual de saudação.
2. Alterar a versão de hello, SKU, referência de imagem ou valor URI no modelo de saudação.
3. Atualize o modelo de saudação.
4. Fazer um *manualUpgrade* chamar em máquinas virtuais Olá Olá conjunto de escala. Esta etapa só será relevante se *upgradePolicy* está definido muito**Manual** na sua escala definida. Se ele for definido muito**automáticas**, todas as máquinas virtuais de saudação são atualizadas ao mesmo tempo, fazendo com que o tempo de inatividade.

Com essas informações em mente, vamos ver como você poderia atualizar a versão de saudação de uma escala definidas no PowerShell e usando a API REST de saudação. Esses exemplos abrangem caso de saudação de uma imagem de plataforma, mas este artigo fornece informações suficientes para que você tooadapt essa imagem personalizada do processo tooa.

## <a name="powershell"></a>PowerShell
Este exemplo atualiza um conjunto de escala de máquinas virtuais do Windows (Criando toohello nova versão do 4.0.20160229. Depois de atualizar o modelo de hello, ele faz uma atualização de uma instância de máquina virtual por vez.

```powershell
$rgname = "myrg"
$vmssname = "myvmss"
$newversion = "4.0.20160229"
$instanceid = "1"

# get hello VMSS model
$vmss = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname

# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.version = $newversion

# update hello virtual machine scale set model
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $vmss

# now start updating instances
Update-AzureRmVmssInstance -ResourceGroupName $rgname -VMScaleSetName $vmssname -InstanceId $instanceId
```

Se você estiver atualizando hello URI para uma imagem personalizada em vez de alterar uma versão da imagem de plataforma, substitua hello "hello nova versão do conjunto de" linha com um comando que atualizará Olá URI da imagem de origem. Por exemplo, se o conjunto de escala de saudação foi criado sem o uso de discos gerenciado do Azure, atualização Olá teria esta aparência:

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.osDisk.image.uri= $newURI
```

Se uma imagem personalizada com base em conjunto de escala foi criado usando discos gerenciado do Azure, e a referência de imagem Olá deve ser atualizada. Por exemplo:

```powershell
# set hello new version in hello model data
$vmss.virtualMachineProfile.storageProfile.imageReference.id = $newImageReference
```

## <a name="hello-rest-api"></a>Olá API REST
Aqui estão alguns exemplos de Python que usam Olá API REST do Azure tooroll uma atualização de versão do sistema operacional. Ambos usam lightweight Olá [azurerm](https://pypi.python.org/pypi/azurerm) biblioteca da API REST do Azure wrapper funções toodo um GET em escala Olá definir modelo, seguido por um PUT com um modelo atualizado. Eles também examinar os modos de exibição de instâncias de máquina virtual tooidentify Olá máquinas virtuais do domínio de atualização.

### <a name="vmssupgrade"></a>Vmssupgrade
 [Vmssupgrade](https://github.com/gbowerman/vmsstools) é um script de Python que usou tooroll out um tooa de atualização de sistema operacional executando escala de máquinas virtuais definir um domínio de atualização por vez.

![Script Vmssupgrade para escolher máquinas virtuais ou um domínio de atualização](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssupgrade-screenshot.png)

Esse script permite que você escolher tooupdate de máquinas virtuais específicas ou especificar um domínio de atualização. Ele dá suporte a alteração de uma versão de imagem de plataforma ou a alteração Olá URI de uma imagem personalizada.

### <a name="vmsseditor"></a>Vmsseditor
[Vmsseditor](https://github.com/gbowerman/vmssdashboard) é um editor para fins gerais para conjuntos de escala de máquina virtual que mostra o status da máquina virtual como um mapa de dados no qual uma linha representa um domínio de atualização. Entre outras coisas, você pode atualizar o modelo de saudação para um conjunto de escala com uma nova versão, SKU ou URI da imagem personalizada e escolha tooupgrade de domínios de falha. Quando você fizer isso, todas as máquinas virtuais de saudação nesse domínio de atualização são atualizados toohello novo modelo. Como alternativa, você pode fazer uma atualização sem interrupção com base no tamanho de lote de saudação de sua escolha.  

Olá seguinte captura de tela mostra um modelo de uma escala definidas para Ubuntu 14.04-2LTS versão 14.04.201507060. Muito mais opções foram adicionadas toothis ferramenta desde que foi feita nesta captura de tela.

![Modelo de Vmsseditor de um conjunto de escala para o Ubuntu 14.04-2LTS](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor1.png)

Depois de clicar em **atualização** e **obter detalhes**, máquinas virtuais em UD 0 iniciar tooupdate.

![Vmsseditor mostrando atualização em andamento](./media/virtual-machine-scale-sets-upgrade-scale-set/vmssEditor2.png)

