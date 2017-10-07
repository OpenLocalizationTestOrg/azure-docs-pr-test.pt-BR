---
title: "aaaVM reiniciar manutenção para VMs do Linux no Azure | Microsoft Docs"
description: "Reinicialização de manutenção da VM para máquinas virtuais do Linux."
services: virtual-machines-linux
documentationcenter: 
author: zivr
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: eb4b92d8-be0f-44f6-a6c3-f8f7efab09fe
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: zivr
ms.openlocfilehash: 41caa2e56740cdfa95d2ea67278e5c1d15a174c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="vm-restarting-maintenance"></a>Reinicialização de manutenção da VM

Há alguns casos em que suas VMs são reiniciadas devido tooplanned manutenção toohello infra-estrutura subjacente. Sendo disponibilidade toothe impacto das suas máquinas virtuais hospedadas no Azure, o seguinte Olá agora está disponíveis para você toouse:

-   Notificação enviada pelo menos 30 dias antes de impacto de saudação.

-   Janelas de manutenção visibilidade toohello por cada VM.

-   Flexibilidade e controle na configuração de tempo de saudação exato para manutenção de afetar suas VMs.

A manutenção no Microsoft Azure é agendada em iterações. Iterações inicias tem escopo menor risco de saudação de tooreduce de ordem envolvidas na implementação de recursos e correções novas. Iterações posteriores podem abranger várias regiões (nunca da saudação mesmo par de região). Uma VM está incluída em uma única iteração de manutenção. Se uma iteração for anulada, as VMs restantes serão incluídas em outra iteração futura.

manutenção planejada iteração Hello tem duas fases: janela de manutenção de Pre-emptive e uma janela de manutenção agendada.

Olá **janela de manutenção Pre-emptive** fornece Olá flexibilidade tooinitiate Olá manutenção suas VMs. Fazendo isso, você pode determinar quando suas VMs são afetadas, Olá a sequência de atualização de saudação e tempo de saudação entre cada VM que está sendo mantido. Você pode consultar cada VM toosee se ele está planejado para manutenção e verificar Olá resultado de sua última solicitação de manutenção iniciada.

Olá **a janela de manutenção agendada** é quando o Azure agendou a suas VMs para manutenção de saudação. Durante essa janela de tempo, o que segue a janela de manutenção preventiva, você pode ainda consultar para a janela de manutenção hello, mas deixará de ser capaz de tooorchestrate manutenção de saudação.

## <a name="availability-considerations-during-planned-maintenance"></a>Considerações sobre disponibilidade durante a manutenção planejada 

### <a name="paired-regions"></a>Regiões emparelhadas

Cada região do Azure é emparelhado com outra região dentro de saudação mesmo geografia, juntos, tornando um par regional. Ao executar a manutenção, o Azure atualizará apenas instâncias de máquina Virtual de saudação em uma única região do seu par. Por exemplo, ao atualizar Olá máquinas virtuais no Centro Norte dos EUA, Azure não atualizará todas as máquinas virtuais no Centro Sul dos EUA em Olá simultaneamente. Isso será agendado em outro momento, permitindo o failover ou o balanceamento de carga entre regiões. No entanto, outras regiões como Norte da Europa pode estar em manutenção no hello mesmo tempo como Leste dos EUA.
Leia mais sobre os [pares de regiões do Azure](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).

### <a name="single-instance-vms-vs-availability-set-or-vm-scale-set"></a>VMs de instância única versus conjunto de disponibilidade ou conjunto de dimensionamento de VMs

Ao implantar uma carga de trabalho usando máquinas virtuais no Azure, você pode criar hello VMs dentro de uma conjunto de disponibilidade no aplicativo de tooyour ordem tooprovide alta disponibilidade. Essa configuração garante que, durante uma interrupção ou eventos de manutenção, pelo menos uma máquina virtual estará disponível.

Em um conjunto de disponibilidade, VMs individuais são distribuídas entre os domínios de atualização too20. Durante a manutenção planejada, somente um único domínio de atualização é afetado em um período específico. ordem de saudação dos domínios de atualização sendo afetado não pode prosseguir sequencialmente durante a manutenção planejada. De única instância VMs (que não faz parte do conjunto de disponibilidade), não há nenhuma maneira toopredict ou determinar quais e quantos VMs impactadas juntos.

Conjuntos de escala de máquinas virtuais são um recurso de computação do Azure que permite que você toodeploy e gerenciam um conjunto de VMs idênticos como um único recurso.
conjunto de escala Olá fornece garantias semelhantes tooan disponibilidade definida na forma de domínios de atualização. 

Para obter mais informações sobre como configurar as máquinas virtuais para alta disponibilidade, consulte [ *gerenciar Olá disponibilidade das máquinas virtuais Windows*](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

### <a name="scheduled-events"></a>Eventos agendados

Azure Metadata Service permite que você toodiscover informações sobre sua máquina Virtual hospedada no Azure. Agendado eventos, uma das categorias de saudação exposta, informações de superfícies sobre eventos futuros (por exemplo, reinicializar) para seu aplicativo possa se preparar e limitar interrupções.

Para obter mais informações sobre eventos agendados, consulte muito[serviço de metadados do Azure - eventos agendados](../virtual-machines-scheduled-events.md).

## <a name="maintenance-discovery-and-notifications"></a>Descoberta de manutenção e notificações

Agenda de manutenção é toocustomers visíveis no nível de saudação de VMs individuais. Você pode usar o Azure portal, tooquery API, o PowerShell ou CLI para as janelas de manutenção agendada e preventivo. Além disso, a esperar receber uma notificação (email) no caso de Olá onde uma (ou mais) de suas VMs são afetados durante o processo de saudação.

As fases de manutenção preemptiva e agendada começam com uma notificação. Espere tooreceive uma única notificação por assinatura do Azure. notificação de saudação é enviada co-administrador e o administrador da assinatura toohello por padrão. Você também pode configurar o público-alvo Olá para a notificação de manutenção.

### <a name="view-hello-maintenance-window-in-hello-portal"></a>Janela de manutenção de saudação de exibição no portal de saudação 

Você pode usar o hello portal do Azure e procurar VMs agendadas para manutenção.

1.  Entrar toohello portal do Azure.

2.  Clique em e abra Olá **máquinas virtuais** folha.

3.  Clique em Olá **colunas** lista de saudação do botão tooopen de toochoose de colunas disponíveis do

4.  Selecione e adicione Olá **janela de manutenção** colunas. Máquinas virtuais que estão agendados para manutenção têm as janelas de manutenção Olá apresentadas. Depois que a manutenção é concluída ou anulada para uma, a janela de manutenção não é mais apresentada.

### <a name="query-maintenance-details-using-hello-azure-api"></a>Detalhes de manutenção de consulta usando Olá API do Azure

Saudação de uso [obter informações de VM API](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-get) e procure Olá exibição toodiscover Olá manutenção detalhes da instância em uma VM individual. resposta de saudação inclui Olá elementos a seguir:

  - isCustomerInitiatedMaintenanceAllowed: indica se você pode iniciar agora preventiva reimplantação em Olá VM.

  - preMaintenanceWindowStartTime: Olá hora de início da janela de manutenção preventiva hello.

  - preMaintenanceWindowEndTime: Olá hora de término da janela de manutenção preventiva hello. Após esse período, você não será tooinitiate capaz de manutenção nessa VM.
    
  - maintenanceWindowStartTime: Olá hora de início da janela de manutenção agendada hello quando sua VM são afetados.

  - maintenanceWindowEndTime: Olá hora de término da janela de manutenção agendada hello.
  
  - lastOperationResultCode: Olá resultado da última operação de reimplantação de manutenção.
 
  - lastOperationMessage: mensagem descrevendo resultado de saudação de sua última operação de reimplantação de manutenção.


## <a name="pre-emptive-redeploy"></a>Reimplantação preemptiva

Ação de reimplantação preventivo fornece tempo de saudação do hello flexibilidade toocontrol quando a manutenção é aplicado tooyour VMs no Azure. Manutenção planejada começa com uma janela de manutenção preventiva onde você pode decidir sobre a hora exata Olá para cada um dos seu toobe VMs reinicializado. Estes são os casos de uso em que uma funcionalidade desse tipo é útil:

-   Toobe da necessidade de manutenção coordenado com o cliente de final de saudação.

-   janela de manutenção agendada Olá oferecida pelo Azure não é suficiente.
    É possível que a janela de saudação ocorre toobe no tempo mais ocupado de saudação da semana ou é muito longo.

-   Para várias instâncias ou aplicativos de várias camadas, é preciso tempo suficiente entre duas VMs ou um determinado toofollow de sequência.

Quando você chama para preventiva reimplantação em uma máquina virtual, ele move Olá VM tooan já atualizou o nó e, em seguida, liga-lo novamente, retém suas opções de configuração e recursos associados. Enquanto isso, disco temporário Olá for perdido e endereços IP dinâmicos associados com a interface de rede virtual são atualizadas.

A reimplantação preemptiva é habilitada uma vez por VM. Se houver um erro durante o processo de hello, Olá operação é anulada, hello VM não é afetada e ele é excluído da iteração de manutenção Olá planejado. Você será contatado em um momento posterior com uma nova agenda e oferecida uma nova oportunidade tooschedule e sequência Olá impacto em suas VMs.
