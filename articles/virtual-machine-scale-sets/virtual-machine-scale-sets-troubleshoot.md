---
title: "dimensionamento automático de aaaTroubleshoot com conjuntos de escala de máquinas virtuais | Microsoft Docs"
description: "Solução de problemas de dimensionamento automático com conjuntos de escala de máquina virtual. Entender os problemas comuns encontrados e como tooresolve-los."
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7d87b72-ee24-4e52-9377-a42f337f76fa
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: windows
ms.devlang: na
ms.topic: article
ms.date: 10/28/2016
ms.author: guybo
ms.openlocfilehash: 4c9a70992348d87fb43646421a90a027bf400a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-autoscale-with-virtual-machine-scale-sets"></a>Solução de problemas do dimensionamento automático com conjuntos de escala de máquina virtual
**Problema** – que você criou uma infraestrutura de dimensionamento automático no Azure Resource Manager usando conjuntos de escala de VM – por exemplo, ao implantar um modelo como este: https://github.com/Azure/azure-quickstart-templates/tree/master/201- garrafa de AutoEscala vmss – você tem suas regras de escala definidas e funciona muito bem, exceto que, independentemente de quanto é colocado no hello VMs de carga, não se preocupe dimensionamento automático.

## <a name="troubleshooting-steps"></a>Etapas para solucionar problemas
Algumas coisas tooconsider incluem:

* O número de núcleos cada VM tem e você estiver carregando cada núcleo? modelo de início rápido do Azure de exemplo Hello acima tem um script de do_work.php, que carrega um único núcleo. Se você estiver usando uma VM maior do que um único núcleo de tamanho da VM como Standard_A1 ou D1 e em seguida, você precisaria toorun load várias vezes. Verifique quantos núcleos suas VMs têm conferindo [Tamanhos para máquinas virtuais do Windows no Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* Como muitas máquinas virtuais em Olá conjunto de escala de VM, você está fazendo o trabalho em cada um deles?
  
    Um evento de expansão só ocorrerá quando Olá a média de CPU em **todos os** Olá VMs em um conjunto de escala excede Olá valor de limite, ao longo do tempo de saudação interno definido nas regras de AutoEscala hello.
* Você perdeu algum evento de escala?
  
    Verifique os logs de auditoria de saudação em Olá portal do Azure para eventos de escala. Pode ter ocorrido uma escala ou redução vertical que foi perdida. Você pode filtrar por “Escala”.
  
    ![Logs de Auditoria][audit]
* Os limites de escala e redução são diferentes o suficiente?
  
    Suponha que você defina uma regra tooscale out quando média de CPU é maior que 50% mais de 5 minutos e tooscale no quando a média de CPU for inferior a 50%. Isso faria com que um problema de "falta de sincronismo" quando o uso da CPU é o limite de fechamento toothis, com ações de escala Olá constantemente aumentar e diminuir o tamanho do conjunto de saudação. Por isso, Olá AutoEscala serviço tenta tooprevent "oscilando", que podem se manifestar como dimensionamento não. Portanto, certifique-se de sua expansão e limites de escala são suficientemente diferente tooallow algum espaço entre o dimensionamento.
* Você criou seu próprio modelo JSON?
  
    É fácil toomake erros, portanto iniciar com um modelo como Olá um acima do qual é aprovado toowork e fazer pequenas alterações incrementais. 
* Você consegue aumentar ou reduzir horizontalmente?
  
    Tente Olá reimplantação recurso conjunto de escala de VM com um número de saudação diferentes "capacidade" configuração toochange de máquinas virtuais manualmente. Um toodo do modelo de exemplo aqui: https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing – talvez seja necessário tooedit Olá modelo toomake se ele tem Olá mesmo tamanho de máquina usando o conjunto de escala. Se com êxito é possível alterar o número de saudação de VMs manualmente, em seguida, você sabe Olá problema tooautoscale isolado.
* Verifique seu Microsoft.Compute/virtualMachineScaleSet e recursos Insights Olá [Gerenciador de recursos do Azure](https://resources.azure.com/)
  
    Este é um indispensáveis Solucionando problemas de ferramenta que mostra Olá o estado de seus recursos do Gerenciador de recursos do Azure. Clique em sua assinatura e examinar Olá grupo de recursos de solução de problemas. Em um provedor de recursos de computação Olá Observe Olá conjunto de escala de VM é criada e verifique Olá exibição de instância, que mostra Olá o estado de uma implantação. Verifique também a exibição de instância Olá de VMs em Olá conjunto de escala de VM. Em seguida, vá para o provedor de recursos do hello Insights e verifique regras de AutoEscala Olá uma boas aparência.
* Olá extensão de diagnóstico está trabalhando e emissão de dados de desempenho?
  
    **Atualização:** dimensionamento automático do Azure foi aprimorado toouse pipeline de métricas que não requer mais um toobe de extensão de diagnóstico instalado com base em um host. Isso significa Olá Avançar alguns parágrafos já não se aplicam se você criar um aplicativo de dimensionamento automático usando o novo pipeline de saudação. É um exemplo de modelos do Azure que tenha sido convertido toouse pipeline de host de saudação: https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale. 
  
    Uso de métricas de baseado em host para dimensionamento automático é melhor para Olá motivos a seguir:
  
  * Menos partes móveis como nenhuma extensão de diagnóstico necessário toobe instalado.
  * Modelos mais simples. Basta adicione o modelo de conjunto de escala existentes do insights AutoEscala regras tooan.
  * Relatórios mais confiáveis e inicialização mais rápida de novas VMs.
    
    Olá apenas os motivos que talvez você queira tookeep usando uma extensão de diagnóstica seria se você precisa de memória diagnóstico reporting/dimensionamento. Métricas baseadas em host não fornecem relatório de memória.
    
    Com isso em mente, execute somente restante Olá deste artigo se você ainda estiver usando extensões de diagnósticas para o dimensionamento automático.
    
    Dimensionamento automático no Gerenciador de recursos do Azure pode funcionar (mas não precisa mais) por meio de uma extensão de VM chamada hello extensão de diagnóstico. Emite conta de armazenamento do desempenho dados tooa que você define no modelo de saudação. Esses dados são agregados, em seguida, pelo serviço do Monitor do Azure hello.
    
    Se Olá serviço Insights não é possível ler dados de saudação VMs, ele deve toosend um email – por exemplo se Olá VMs, portanto, verifique seu email (Olá especificada ao criar hello conta do Azure).
    
    Também pode ir e examinar dados saudação por conta própria. Examinar Olá conta de armazenamento do Azure usando um Gerenciador de nuvem. Por exemplo, usando Olá [Visual Studio Cloud Explorer](https://visualstudiogallery.msdn.microsoft.com/aaef6e67-4d99-40bc-aacf-662237db85a2), faça logon no e escolha Olá assinatura do Azure que você está usando e Olá nome referenciado no hello definição de extensão de diagnóstico em sua implantação de conta de armazenamento de diagnóstico modelo.
    
    ![Gerenciador de Nuvem][explorer]
    
    Aqui, você verá uma série de tabelas onde os dados de saudação de cada VM estão sendo armazenados. Colocar o Linux e Olá métrica de CPU como um exemplo, examine linhas mais recentes hello. Gerenciador de nuvem do Visual Studio Olá dá suporte a uma linguagem de consulta, você pode executar uma consulta como "Timestamp gt datetime'2016-02-02T21:20:00Z'" toomake-se de obter eventos mais recentes de saudação (supondo que o tempo é em UTC). Dados Olá que consulte em existe correspondem toohello dimensionar regras configuradas por você? O exemplo hello abaixo, Olá da CPU para a máquina 20 iniciado aumentando too100% ao longo de saudação últimos 5 minutos.
    
    ![Tabelas de Armazenamento][tables]
    
    Se dados saudação não estiverem lá, isso significa problema Olá está com a extensão de diagnóstico Olá em execução no hello VMs. Se dados saudação estiverem lá, significa que há um problema com as regras de escala, ou com o serviço de Insights hello. Verifique o [Status do Azure](https://azure.microsoft.com/status/).
    
    Depois de ter sido através dessas etapas, se você ainda estiver tendo problemas de dimensionamento automático tente fóruns Olá [MSDN](https://social.msdn.microsoft.com/forums/azure/home?category=windowsazureplatform%2Cazuremarketplace%2Cwindowsazureplatformctp), ou [estouro de pilha](http://stackoverflow.com/questions/tagged/azure), ou uma chamada de suporte de log. Ser o modelo de saudação tooshare preparada e uma exibição de dados de desempenho de saudação.

[audit]: ./media/virtual-machine-scale-sets-troubleshoot/image3.png
[explorer]: ./media/virtual-machine-scale-sets-troubleshoot/image1.png
[tables]: ./media/virtual-machine-scale-sets-troubleshoot/image4.png
