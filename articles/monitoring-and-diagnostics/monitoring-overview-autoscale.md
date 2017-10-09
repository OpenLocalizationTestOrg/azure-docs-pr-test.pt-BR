---
title: "aaaOverview de dimensionamento automático em aplicativos Web, serviços de nuvem e máquinas virtuais do Microsoft Azure | Microsoft Docs"
description: "Visão Geral do dimensionamento automático no Microsoft Azure. Aplica-se tooVirtual máquinas, serviços de nuvem e aplicativos Web."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 74bf03be-e658-4239-a214-c12424b53e4c
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2016
ms.author: robb
ms.openlocfilehash: ef68b722ea22c4149a7d7a89c5855ba761db9247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-autoscale-in-microsoft-azure-virtual-machines-cloud-services-and-web-apps"></a>Visão geral do dimensionamento automático em Aplicativos Web, Serviços de Nuvem e Máquinas Virtuais do Microsoft Azure
Este artigo descreve o Microsoft Azure o dimensionamento automático é, seus benefícios e como tooget iniciada usá-lo.  

Dimensionamento automático de Monitor do Azure se aplica apenas muito[conjuntos de escala de máquina Virtual](https://azure.microsoft.com/services/virtual-machine-scale-sets/), [serviços de nuvem](https://azure.microsoft.com/services/cloud-services/), e [do serviço de aplicativo - aplicativos Web](https://azure.microsoft.com/services/app-service/web/).

> [!NOTE]
> O Azure tem dois métodos de dimensionamento automático. Uma versão mais antiga de dimensionamento automático se aplica a máquinas de tooVirtual (conjuntos de disponibilidade). Esse recurso tem suporte limitado e é recomendável migrar escala de máquina toovirtual define para suporte de dimensionamento automático mais rápidas e confiáveis. Um link como a tecnologia mais antiga do toouse hello está incluído neste artigo.  
>
>

## <a name="what-is-autoscale"></a>O que é dimensionamento automático?
Dimensionamento automático permite que você toohave Olá ideal de recursos executando toohandle Olá carga em seu aplicativo. Ele permite que os recursos de tooadd toohandle aumentos de carregam e também economizar dinheiro removendo recursos que são estão ociosos. Especifique um número mínimo e máximo de instâncias toorun e adicionar ou remover VMs automaticamente com base em um conjunto de regras. Ter um mínimo assegura que seu aplicativo estará sempre em execução, mesmo sem carga. Ter um máximo limita seu custo por hora total possível. Você dimensiona automaticamente entre esses dois extremos usando as regras criadas.

 ![Dimensionamento automático explicado. Adicionar e remover as VMs](./media/monitoring-overview-autoscale/AutoscaleConcept.png)

Quando as condições da regra forem atendidas, uma ou mais ações de dimensionamento automático são disparadas. Você pode adicionar e remover as VMs ou executar outras ações. Olá diagrama conceitual a seguir mostra esse processo.  

 ![Diagrama do Fluxo do Dimensionamento Automático](./media/monitoring-overview-autoscale/Autoscale_Overview_v4.png)

Olá explicação a seguir aplica-se toohello partes do diagrama anterior hello.   

## <a name="resource-metrics"></a>Métricas do recurso
Os recursos emitem métricas, que são processadas posteriormente por regras. As métricas são fornecidas por métodos diferentes.
Conjuntos de escala de máquina virtual usam dados de telemetria de agentes de diagnóstico do Azure, enquanto a telemetria para aplicativos Web e serviços de nuvem oriundos diretamente de saudação infraestrutura do Azure. Algumas estatísticas usadas normalmente incluem o Uso da CPU, utilização de memória, contagens de thread, comprimento da fila e uso do disco. Para obter uma lista de quais dados de telemetria você pode usar, confira [Métricas comuns de dimensionamento automático](insights-autoscale-common-metrics.md).

## <a name="custom-metrics"></a>Métricas personalizadas
Você também pode usar suas próprias métricas personalizadas que seus aplicativos podem emitir. Se você tiver configurado seu tooApplication de métricas de toosend aplicativos Insights, você pode aproveitar as decisões de toomake de métricas se tooscale ou não. 

## <a name="time"></a>Hora
Regras com base em agendamento têm base em UTC. Ao configurar as regras, você deve definir o fuso horário corretamente.  

## <a name="rules"></a>Regras
diagrama de saudação mostra apenas uma regra de dimensionamento automático, mas você pode ter muitas delas. Você pode criar regras complexas de sobreposição, conforme o necessário para sua situação.  Os tipos de regra incluem  

* **Com base em métrica** - Por exemplo, executar esta ação quando o uso da CPU estiver acima de 50%.
* **Com base no tempo** - Por exemplo, disparar um webhook todas os sábados às 8h em um determinado fuso horário.

As regras baseadas na métrica medem a carga do aplicativo e adicionam ou removem as VMs com base nessa carga. Regras com base em agendamento permitem tooscale quando você veja os padrões de tempo na sua carga e deseja tooscale antes de um aumento de carga possíveis ou diminuir ocorre.  

## <a name="actions-and-automation"></a>Ações e automação
As regras podem disparar um ou mais tipos de ações.

* **Escala** - Aumenta ou diminui as VMs
* **Email** -enviar email toosubscription administradores, administradores de co e/ou endereço de email adicionais que você especificar
* **Automatizar via webhooks** - Chama webhooks, que podem disparar várias ações complexas dentro ou fora do Azure. Dentro do Azure, você pode iniciar um runbook de Automação do Azure, Função do Azure ou Aplicativo Lógico do Azure. Entre os exemplos de URL de terceiros fora do Azure estão serviços como o Slack e o Twilio.

## <a name="autoscale-settings"></a>Configurações de dimensionamento automático
AutoEscala usar seguinte Olá terminologia e estrutura.

- Um **configuração de dimensionamento automático** é lido pelo Olá AutoEscala mecanismo toodetermine se tooscale para cima ou para baixo. Ele contém um ou mais perfis, informações sobre o recurso de destino hello e configurações de notificação.

    - Um **perfil de dimensionamento automático** é um combinação de:

        - **configuração de capacidade de**, que indica que o mínimo, máximo de saudação e valores padrão para o número de instâncias.
        - **conjunto de regras**, cada um deles inclui um gatilho (tempo ou métrica) e uma ação de dimensionamento (para cima ou para baixo).
        - **recorrência**, que indica quando o dimensionamento automático deve colocar esse perfil em vigor.

        Você pode ter vários perfis, que permitem que você tootake respeito diferentes requisitos de sobreposição. Você pode ter perfis de AutoEscala diferentes para diferentes momentos do dia ou dias da semana hello, por exemplo.

    - Um **configuração de notificação** define quais notificações devem ocorrer quando um evento de dimensionamento automático ocorre com base no que satisfazem os critérios de saudação de um dos perfis de configuração de dimensionamento automático hello. Dimensionamento automático pode notificar um ou mais endereços de email ou fazer chamadas tooone ou mais webhooks.


![Configuração do dimensionamento automático do Azure, perfil e estrutura de regras](./media/monitoring-overview-autoscale/AzureResourceManagerRuleStructure3.png)

Olá lista completa dos campos configuráveis e descrições está disponível no hello [AutoEscala REST API](https://msdn.microsoft.com/library/dn931928.aspx).

Para obter exemplos de código, consulte

* [Configuração avançada de Dimensionamento Automático usando modelos do Resource Manager para conjuntos de escala de VM](insights-advanced-autoscale-virtual-machine-scale-sets.md)  
* [API REST do Dimensionamento Automático](https://msdn.microsoft.com/library/dn931953.aspx)

## <a name="horizontal-vs-vertical-scaling"></a>Dimensionamento horizontal vs. vertical
Dimensionamento automático somente pode ser dimensionado horizontalmente, que é um aumento ("out") ou diminuir ("em") no número de saudação de instâncias VM.  Horizontal é mais flexível em uma situação de nuvem que permite a você toorun milhares de máquinas virtuais toohandle carga.

Já o dimensionamento vertical é diferente. Ele mantém Olá mesmo número de VMs, mas torna Olá VMs mais ("a") ou menos ("baixo") avançada. O poder é medido em termos de memória, velocidade da CPU, espaço em disco etc.  O dimensionamento vertical tem mais limitações. Ele é dependente de disponibilidade de saudação do hardware maior, que rapidamente atinge um limite superior e pode variar por região. Vertical dimensionamento também geralmente requer um toostop VM e reinicie.

Para saber mais, confira [Dimensionar verticalmente uma máquina virtual do Azure com a Automação do Azure](../virtual-machines/linux/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="methods-of-access"></a>Métodos de acesso
Você pode configurar o dimensionamento automático via

* [Portal do Azure](insights-how-to-scale.md)
* [PowerShell](insights-powershell-samples.md#create-and-manage-autoscale-settings)
* [CLI (Interface de linha de comando) de plataforma cruzada](insights-cli-samples.md#autoscale)
* [API REST do Monitor do Azure](https://msdn.microsoft.com/library/azure/dn931953.aspx)

## <a name="supported-services-for-autoscale"></a>Serviços com suporte para o dimensionamento automático
| O Barramento de | Esquema e Documentos |
| --- | --- |
| Aplicativos Web |[Dimensionamento de Aplicativos Web](insights-how-to-scale.md) |
| Serviços de Nuvem |[Dimensionamento Automático de um Serviço de Nuvem](../cloud-services/cloud-services-how-to-scale.md) |
| Máquinas Virtuais: Clássico |[Dimensionamento de conjuntos de disponibilidade da máquina virtual clássica](https://blogs.msdn.microsoft.com/kaevans/2015/02/20/autoscaling-azurevirtual-machines/) |
| Máquinas Virtuais: Conjuntos de Dimensionamento do Windows |[Dimensionamento de conjuntos de dimensionamento de máquina virtual no Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) |
| Máquinas Virtuais: Conjunto de Dimensionamento do Linux |[Dimensionamento de conjuntos de dimensionamento de máquina virtual no Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) |
| Máquinas Virtuais: Exemplo para Windows |[Configuração avançada de Dimensionamento Automático usando modelos do Resource Manager para conjuntos de escala de VM](insights-advanced-autoscale-virtual-machine-scale-sets.md) |

## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre o dimensionamento automático, use Olá Autoscale Walkthroughs listadas anteriormente, ou consulte toohello recursos a seguir:

* [Métricas comuns de dimensionamento automático do Azure Monitor](insights-autoscale-common-metrics.md)
* [Práticas recomendadas para dimensionamento automático do Azure Monitor](insights-autoscale-best-practices.md)
* [Usar o dimensionamento automático ações toosend email e webhook notificações de alerta](insights-autoscale-to-webhook-email.md)
* [API REST do Dimensionamento Automático](https://msdn.microsoft.com/library/dn931953.aspx)
* [Solução de Problemas do Dimensionamento Automático dos Conjuntos de Dimensionamento da Máquina Virtual](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)
