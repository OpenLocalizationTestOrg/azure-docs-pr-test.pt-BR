---
title: "Visão geral dos conjuntos de escala de máquinas virtuais aaaAzure | Microsoft Docs"
description: "Saiba mais sobre os Conjuntos de dimensionamento de máquinas virtuais do Azure"
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
ms.date: 07/03/2017
ms.author: guybo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 788b2d1636e0bf4ef3fbf94aed9b3303c5fafa82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-virtual-machine-scale-sets-in-azure"></a>O que são conjuntos de dimensionamento de máquinas virtuais no Azure?
Conjuntos de escala de máquinas virtuais são um recurso de computação do Azure que você pode usar toodeploy e gerenciar um conjunto de VMs idênticos. Com todas as máquinas virtuais configuradas Olá mesmo, conjuntos de escala são AutoEscala true toosupport projetado e nenhum provisionamento prévio de VMs é necessária. Portanto, é mais fácil serviços em grande escala toobuild que se destinam a computação intensa, dados grandes e cargas de trabalho em contêineres.

Para aplicativos que precisam de recursos de computação tooscale e em escala operações implicitamente são balanceadas entre domínios de falha e atualização. Define um adicional tooscale de Introdução, consulte toohello [comunicado do blog do Azure](https://azure.microsoft.com/blog/azure-virtual-machine-scale-sets-ga/).

Para saber mais sobre conjuntos de dimensionamento, assista a estes vídeos:

* [Mark Russinovich fala sobre os conjuntos de dimensionamento do Azure](https://channel9.msdn.com/Blogs/Regular-IT-Guy/Mark-Russinovich-Talks-Azure-Scale-Sets/)  
* [Conjuntos de Dimensionamento de Máquina Virtual com Guy Bowerman](https://channel9.msdn.com/Shows/Cloud+Cover/Episode-191-Virtual-Machine-Scale-Sets-with-Guy-Bowerman)

## <a name="creating-and-managing-scale-sets"></a>Criando e gerenciando conjuntos de dimensionamento
Você pode criar uma escala definida no hello [portal do Azure](https://portal.azure.com) selecionando **novo** e digitando **escala** na barra de pesquisa de saudação. **Conjunto de escalas da máquina virtual** está listado nos resultados de saudação. A partir daí, você pode preencher Olá necessários campos toocustomize e implantar seu conjunto de escala. Você também tem opções tooset as regras básicas de dimensionamento automático com base no uso de CPU em portal hello.

Você pode definir e implantar conjuntos de dimensionamento usando modelos JSON e [APIs REST](https://msdn.microsoft.com/library/mt589023.aspx), assim como as VMs individuais do Azure Resource Manager. Portanto, você pode usar qualquer método de implantação do Azure Resource Manager padrão. Para obter mais informações sobre modelos, confira [Criação de modelos do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-authoring-templates.md).

Você pode encontrar define um conjunto de modelos de exemplo para a escala de máquinas virtuais em Olá [repositório do GitHub de modelos de início rápido do Azure](https://github.com/Azure/azure-quickstart-templates). (Procurar os modelos com **vmss** no título hello.)

Para obter exemplos de modelo de início rápido da saudação, um botão "Implantar tooAzure" hello Leiame para cada modelo vincula toohello recurso de implantação do portal. escala de saudação toodeploy definido, clique botão de saudação e, em seguida, preencha os parâmetros que são necessários no portal de saudação. 

## <a name="scaling-a-scale-set-out-and-in"></a>Expandindo e reduzindo um conjunto de dimensionamento
Você pode alterar a capacidade de saudação de uma escala definida no portal do Azure de saudação clicando Olá **Scaling** seção em **configurações**. 

capacidade de conjunto de escala de toochange na linha de comando hello, use Olá **escala** do [CLI do Azure](https://github.com/Azure/azure-cli). Por exemplo, use este comando tooset uma capacidade de tooa do conjunto de escala de 10 VMs:

```bash
az vmss scale -g resourcegroupname -n scalesetname --new-capacity 10 
```

número de saudação tooset de VMs em uma escala de definir usando o PowerShell, use Olá **AzureRmVmss atualização** comando:

```PowerShell
$vmss = Get-AzureRmVmss -ResourceGroupName resourcegroupname -VMScaleSetName scalesetname  
$vmss.Sku.Capacity = 10
Update-AzureRmVmss -ResourceGroupName resourcegroupname -Name scalesetname -VirtualMachineScaleSet $vmss
```

tooincrease diminuição Olá número de máquinas virtuais em uma escala de definido por meio de um modelo do Gerenciador de recursos do Azure, altere Olá **capacidade** propriedade e reimplantar o modelo de saudação. Essa simplicidade torna fácil toointegrate conjuntos de escala com o dimensionamento automático do Azure ou toowrite que sua própria camada dimensionamento personalizada se você precisar de eventos de escala personalizada toodefine que o dimensionamento automático do Azure não dá suporte. 

Se estiver reimplantando uma capacidade de saudação do Azure Resource Manager modelo toochange, você pode definir um muito modelo menor que inclui apenas Olá **SKU** pacote de propriedade com hello atualizado capacidade. [Aqui está um exemplo](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing).

## <a name="autoscale"></a>Autoscale

Um conjunto de escala pode ser configurado opcionalmente com configurações de dimensionamento automático quando ele é criado no hello portal do Azure. número de saudação de VMs pode, em seguida, aumento ou redução com base no uso médio da CPU. 

Muitos hello dimensionar os modelos de conjunto em Olá [modelos de início rápido do Azure](https://github.com/Azure/azure-quickstart-templates) definir configurações de dimensionamento automático. Você também pode adicionar tooan de configurações de dimensionamento automático existentes do conjunto de escala. Por exemplo, este script do PowerShell do Azure adiciona o conjunto de escala do dimensionamento automático com base em CPU tooa:

```PowerShell

$subid = "yoursubscriptionid"
$rgname = "yourresourcegroup"
$vmssname = "yourscalesetname"
$location = "yourlocation" # e.g. southcentralus

$rule1 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/$subid/resourceGroups/$rgname/providers/Microsoft.Compute/virtualMachineScaleSets/$vmssname -Operator GreaterThan -MetricStatistic Average -Threshold 60 -TimeGrain 00:01:00 -TimeWindow 00:05:00 -ScaleActionCooldown 00:05:00 -ScaleActionDirection Increase -ScaleActionValue 1
$rule2 = New-AzureRmAutoscaleRule -MetricName "Percentage CPU" -MetricResourceId /subscriptions/$subid/resourceGroups/$rgname/providers/Microsoft.Compute/virtualMachineScaleSets/$vmssname -Operator LessThan -MetricStatistic Average -Threshold 30 -TimeGrain 00:01:00 -TimeWindow 00:05:00 -ScaleActionCooldown 00:05:00 -ScaleActionDirection Decrease -ScaleActionValue 1
$profile1 = New-AzureRmAutoscaleProfile -DefaultCapacity 2 -MaximumCapacity 10 -MinimumCapacity 2 -Rules $rule1,$rule2 -Name "autoprofile1"
Add-AzureRmAutoscaleSetting -Location $location -Name "autosetting1" -ResourceGroup $rgname -TargetResourceId /subscriptions/$subid/resourceGroups/$rgname/providers/Microsoft.Compute/virtualMachineScaleSets/$vmssname -AutoscaleProfiles $profile1
```

Você pode encontrar uma lista de métricas válido tooscale em [suporte para métricas com o Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md) em Olá título "Microsoft.Compute/virtualMachineScaleSets". As opções mais avançadas de dimensionamento automático também estão disponíveis, incluindo o dimensionamento automático com base em agendamento e usando webhooks toointegrate com sistemas de alerta.

## <a name="monitoring-your-scale-set"></a>Monitorando seu conjunto de dimensionamento
Olá [portal do Azure](https://portal.azure.com) listas escala define e mostra suas propriedades. portal de saudação também oferece suporte a operações de gerenciamento. Você pode executar operações de gerenciamento nos conjuntos de dimensionamento e nas VMs individuais em um conjunto de dimensionamento. portal de saudação também fornece um gráfico de uso do recurso personalizável. 

Se você precisa toosee ou editar Olá subjacente definição JSON de um recurso do Azure, você também pode usar [Gerenciador de recursos do Azure](https://resources.azure.com). Conjuntos de escala são um recurso em Olá provedor de recursos do Azure da Microsoft. Compute. Neste site, você pode vê-los expandindo Olá links a seguir:

**Assinaturas** > **sua assinatura** > **resourceGroups** > **provedores** > **Microsoft.Compute** > **virtualMachineScaleSets** > **seu conjunto de dimensionamento** > etc.

## <a name="scale-set-scenarios"></a>Cenários do conjunto de dimensionamento
Esta seção lista alguns cenários típicos de conjunto de dimensionamento. Além disso, alguns serviços do Azure de nível mais alto (como Lote, Service Fabric e Serviço de Contêiner) usam esses cenários.

* **Usar RDP ou SSH tooconnect tooscale conjunto de instâncias**: um conjunto de escala é criado dentro de uma rede virtual e VMs individuais no conjunto de escala de saudação não estão alocadas endereços IP públicos por padrão. Esta política evita despesas hello e sobrecarga de gerenciamento de alocação de IP público separado endereços tooall nós Olá a grade de computação. Se você precisa direcionar conexões externas tooscale definir VMs, você pode configurar uma escala conjunto tooautomatically atribuir pública IP endereços toonew VMs. Como alternativa, você pode conectar tooVMs de outros recursos em sua rede virtual pode estar endereços IP públicos, por exemplo, balanceadores de carga e máquinas virtuais autônomas. 
* **Conecte-se tooVMs usando regras NAT**: você pode criar um endereço IP público, atribua-o balanceador de carga tooa e definir um pool NAT de entrada. Essas ações portas Olá IP endereço tooa porta em uma máquina virtual no conjunto de escala de saudação do mapa. Por exemplo:
  
  | Fonte | Porta de origem | Destino | Porta de destino |
  | --- | --- | --- | --- |
  |  IP público |Porta 50000 |vmss\_0 |Porta 22 |
  |  IP público |Porta 50001 |vmss\_1 |Porta 22 |
  |  IP público |Porta 50002 |vmss\_2 |Porta 22 |
  
   Em [Este exemplo](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-linux-nat), regras de NAT são definida tooenable um tooevery de conexão SSH VM em um conjunto de escala, usando um IP público único endereço.
  
   [Este exemplo](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-nat) Olá mesmo com o RDP e o Windows.
* **Conecte-se tooVMs usando "jumpbox"**: se você criar um conjunto de escala e uma VM autônoma em Olá mesmo virtual de rede, hello autônomo VM e hello conjunto de escala de VM pode se conectar tooone endereços de outra usando seu endereço IP interno, conforme definido pelo Olá virtual rede ou sub-rede. Se você criar um endereço IP público e atribuí-la toohello autônomo VM, você pode usar RDP ou SSH tooconnect toohello VM autônoma. Você pode conectar da que máquina tooyour conjunto de escala de instâncias. Você pode perceber, nesse momento, que um simples conjunto de dimensionamento é inerentemente mais seguro do que uma simples VM autônoma com um endereço IP público em sua configuração padrão.
  
   Por exemplo, [este modelo](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-linux-jumpbox) implanta um conjunto de dimensionamento simples com uma VM autônoma. 
* **Tooscale conjunto de instâncias de balanceamento de carga**: se você quiser tooa toodeliver trabalho cluster de computação de VMs usando uma abordagem de rodízio, você pode configurar um balanceador de carga do Azure com regras de balanceamento de carga de camada 4 adequadamente. Você pode definir testes tooverify que seu aplicativo é executado usando o comando ping portas com um protocolo especificado, o intervalo e o caminho da solicitação. O [Gateway de Aplicativo](https://azure.microsoft.com/services/application-gateway/) do Azure também oferece suporte aos conjuntos de dimensionamento, além de cenários de balanceamento de carga de camada 7 e mais sofisticados.
  
   [Este exemplo](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-ubuntu-web-ssl) cria um conjunto de escala que é executado de servidores web Apache e usa uma toobalance Olá carga que cada VM recebe. (Observe o tipo de recurso de Microsoft.Network/loadBalancers hello e networkProfile e extensionProfile em virtualMachineScaleSet.)

   [Este exemplo de Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-ubuntu-app-gateway) e [Este exemplo de Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-app-gateway) usam o Gateway de Aplicativo.  

* **Implantar um conjunto de dimensionamento como um cluster de cálculo em um gerenciador de cluster de PaaS**: os conjuntos de dimensionamento são muitas vezes descritos como uma função de trabalho de próxima geração. Embora uma descrição válida, ele corre o risco de saudação de escala confuso conjunto de recursos com recursos de serviços de nuvem do Azure. De certa forma, os conjuntos de dimensionamento oferecem uma verdadeira função ou recurso de trabalho. Eles são um recurso de computação generalizado que independe da plataforma/do tempo de execução, é personalizável e se integra ao IaaS do Azure Resource Manager.
  
   Uma função de trabalho dos Serviços de Nuvem é limitada em termos de suporte de plataforma/tempo de execução (somente imagens da plataforma Windows). Mas ele também inclui serviços como permuta VIP, configurações de atualização editáveis e configurações específicas de implantação de aplicativo/tempo de execução. Esses serviços não estão *ainda* disponíveis nos conjuntos de dimensionamento ou são fornecidos por outros serviços de PaaS de nível mais alto, como o Azure Service Fabric. Você pode examinar os conjuntos de dimensionamento como uma infraestrutura que dá suporte a PaaS. Soluções PaaS como o [Service Fabric](https://azure.microsoft.com/services/service-fabric/) criam com base nessa infraestrutura.
  
   [Neste exemplo](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos) da abordagem, o [Serviço de Contêiner do Azure](https://azure.microsoft.com/services/container-service/) implanta um cluster com base em conjuntos de dimensionamento com um orquestrador de contêiner.

## <a name="scale-set-performance-and-scale-guidance"></a>Orientação de dimensionamento e desempenho do conjunto de dimensionamento
* Uma escala conjunto oferece suporte a too1, 000 VMs. Se você criar e carregar suas próprias imagens VM personalizadas, o limite de saudação é 100. Para considerações sobre o uso de conjuntos de dimensionamento grandes, confira [Trabalhando com conjuntos de dimensionamento de máquinas virtuais grandes](virtual-machine-scale-sets-placement-groups.md).
* Você não tem toopre-criar conjuntos de escala de toouse de contas de armazenamento do Azure. Suporte a conjuntos de escala do Azure gerenciados discos, o que negar questões de desempenho sobre o número de saudação de discos por conta de armazenamento. Para saber mais, confira [Conjuntos de dimensionamento de máquinas virtuais do Azure e discos gerenciados](virtual-machine-scale-sets-managed-disks.md).
* Considere o uso de armazenamento Premium do Azure, em vez de Armazenamento do Azure para ter tempos de provisionamento de VM mais rápidos e mais previsíveis, além de um melhor desempenho de E/S.
* cota de núcleo Olá na região Olá no qual você está implantando limita o número de saudação de VMs, você pode criar. Talvez seja necessário toocontact atendimento tooincrease seu limite de cota de computação, mesmo se você tiver um limite mais alto de núcleos para uso com os serviços de nuvem do Azure hoje. tooquery sua cota, execute este comando CLI do Azure: `azure vm list-usage`. Ou execute este comando do PowerShell: `Get-AzureRmVMUsage`.

## <a name="frequently-asked-questions-for-scale-sets"></a>Perguntas frequentes sobre os conjuntos de dimensionamento
**P.** Quantas VMs posso ter em um conjunto de dimensionamento?

**A.** Um conjunto de escala pode ter too1 0, 000 VMs baseiam em imagens de plataforma ou 0 VMs de too100 com base em imagens personalizadas. 

**P.** Há suporte para os discos de dados nos conjuntos de dimensionamento?

**A.** Sim. Um conjunto de escala pode definir uma configuração de discos de dados anexado que se aplica a tooall VMs no conjunto de saudação. Para saber mais, confira [Conjuntos de dimensionamento do Azure e discos de dados anexados](virtual-machine-scale-sets-attached-disks.md). Outras opções para armazenamento de dados incluem:

* Arquivos do Azure (unidades compartilhada de SMB)
* Unidade do sistema operacional
* Unidade TEMP (local, não tem relação com o Armazenamento do Azure)
* Serviço de dados do Azure (por exemplo, Tabelas e Blobs do Azure)
* Serviço de dados externo (por exemplo, banco de dados remoto)

**P.** Quais são as regiões do Azure que dão suporte aos conjuntos de dimensionamento?

**A.** Todas as regiões dão suporte aos conjuntos de dimensionamento.

**P.** Como posso criar um conjunto de dimensionamento usando uma imagem personalizada?

**A.** Crie um disco gerenciado com base em seu VHD de imagem personalizada e faça referência a ele em seu modelo de conjunto de dimensionamento. [Aqui está um exemplo](https://github.com/chagarw/MDPP/tree/master/101-vmss-custom-os).

**P.** Se eu reduzo meu conjunto de escala de capacidade de 20 too15, que VMs são removidas?

**A.** Máquinas virtuais são removidas da saudação escala definidas uniformemente entre os domínios de atualização e a disponibilidade de toomaximize de domínios de falha. VMs com hello que mais altos IDs são removidos primeiro.

**P.** E se, em seguida, aumentar a capacidade de saudação do too18 15?

**A.** Se você aumentar capacidade too18, 3 novas VMs são criadas. Cada vez, ID de instância VM Olá é incrementado de saudação anterior valor mais alto (por exemplo, 20, 21, 22). As VMs são balanceadas entre domínios de falha e domínios de atualização.

**P.** Ao usar várias extensões em um conjunto de dimensionamento, posso impor uma sequência de execução?

**A.** Não diretamente, mas para a extensão de customScript hello, o script pode aguardar toofinish de outra extensão. Para obter orientação adicional sobre sequenciamento de extensão na postagem de blog Olá [sequenciamento de extensão em conjuntos de escala de VM do Azure](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).

**P.** Os conjuntos de dimensionamento funcionam com os conjuntos de disponibilidade do Azure?

**A.** Sim. Um conjunto de dimensionamento é um conjunto de disponibilidade implícita com cinco domínios de falha e cinco domínios de atualização. Escala de conjuntos de mais de 100 VMs abrangem vários *grupos de posicionamento*, que são conjuntos de disponibilidade toomultiple equivalente. Para saber mais sobre grupos de posicionamento, confira [Como trabalhar com conjuntos de dimensionamento grandes de máquinas virtuais](virtual-machine-scale-sets-placement-groups.md). Um conjunto de disponibilidade de máquinas virtuais pode existir em Olá mesma rede virtual como um conjunto de escala de máquinas virtuais. Uma configuração comum é tooput controle VMs do nó (que geralmente requerem configuração exclusivas) em um disponibilidade definida e colocar os nós de dados no conjunto de escala de saudação.

Você pode encontrar mais tooquestions respostas sobre a escala define Olá [escala de máquina virtual do Azure define perguntas frequentes sobre](virtual-machine-scale-sets-faq.md).
