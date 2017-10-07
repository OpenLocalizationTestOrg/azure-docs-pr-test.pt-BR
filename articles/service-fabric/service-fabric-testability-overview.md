---
title: "Visão geral do serviço de análise de aaaFault | Microsoft Docs"
description: "Este artigo descreve Olá serviço de análise de falha no serviço de malha para induzindo falhas e execução de cenários de teste em relação a seus serviços."
services: service-fabric
documentationcenter: .net
author: anmolah
manager: timlt
editor: vturecek
ms.assetid: 1f064276-293a-4989-a513-e0d0b9fdf703
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/15/2017
ms.author: anmola
ms.openlocfilehash: deac16ec830aa10d4e488e60691faa9ef2b6cd33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-fault-analysis-service"></a>Introdução toohello serviço de análise de falha
Olá serviço de análise de falha foi projetado para testar os serviços que são criados no Microsoft Azure Service Fabric. Com hello serviço de análise de falha, você pode induzir falhas significativas e executar cenários de teste concluída em relação a seus aplicativos. Esses cenários e falhas de exercício em validar Olá vários estados e transições que um serviço enfrentam ao longo de seu ciclo de vida, tudo em uma maneira consistente, segura e controlada.

As ações são falhas individuais de saudação direcionando um serviço para testá-lo. Um desenvolvedor de serviço pode usá-los como blocos de construção toowrite complicado cenários. Por exemplo:

* Reinicie um nó toosimulate inúmeras situações em que um computador ou VM for reinicializado.
* Mova uma réplica de seu serviço com monitoração de estado toosimulate balanceamento de carga, failover ou atualização do aplicativo.
* Invocação de perda de quorum em um serviço com monitoração de estado de toocreate uma situação em que as operações de gravação não podem continuar porque não existem dados novos de tooaccept suficientes réplicas "backup" ou "secondary".
* Invocação de perda de dados em um serviço com monitoração de estado de toocreate uma situação em que todos os estados de memória é completamente apagados.

Os cenários são operações complexas compostas de uma ou mais ações. Olá falhas Analysis Services fornece dois cenários completos internos:

* Cenário de caos
* Cenário de failover

## <a name="testing-as-a-service"></a>Teste como serviço
Olá serviço de análise de falha é um serviço de sistema do Service Fabric é iniciado automaticamente com um cluster do Service Fabric. Esse serviço atua como host Olá para injeção de falha, a execução de cenário de teste e análise de integridade. 

![Serviço de Análise de Falha][0]

Quando um cenário de teste ou a ação de falha é iniciado, um comando é enviado toohello serviço de análise de falha toorun Olá ação ou teste de cenário de falha. Olá serviço de análise de falha é com monitoração de estado para que pode executar falhas e cenários e validar os resultados de forma confiável. Por exemplo, um cenário de teste de execução longa pode ser executado com confiança por Olá serviço de análise de falha. E porque testes estão sendo executados dentro do cluster Olá, serviço Olá pode examinar estado de saudação do cluster de saudação e seu serviços tooprovide informações mais detalhadas sobre falhas.

## <a name="testing-distributed-systems"></a>Testando sistemas distribuídos
Malha do serviço torna o trabalho de saudação de gravação e gerenciamento de aplicativos distribuídos escalonáveis muito mais fácil. Olá falhas Analysis Service simplifica o teste de um aplicativo distribuído da mesma forma mais fácil. Há três principais problemas que precisam toobe resolvido durante o teste:

1. Simulando/gerar falhas que podem ocorrer em cenários do mundo real: um dos aspectos importantes de saudação do Service Fabric é que ele permite que aplicativos distribuídos toorecover de várias falhas. No entanto, tootest que Olá aplicativo é capaz de toorecover dessas falhas, precisamos de um mecanismo toosimulate/gerar essas falhas reais em um ambiente de teste controlado.
2. Olá capacidade toogenerate correlacionado falhas: básicas falhas no sistema de saudação, como falhas de rede e de máquina, são tooproduce fácil individualmente. Gerar um número significativo de cenários que podem ocorrer em Olá, mundo real como resultado de interações Olá dessas falhas individuais é incomum.
3. Experiência unificada em vários níveis de desenvolvimento e implantação: há muitos sistemas de injeção de falha que podem executar vários tipos de falhas. No entanto, Olá experiência em todas elas é ruim quando a mudança de cenários de caixa de um desenvolvedor, Olá toorunning mesmos testes em ambientes de teste grandes, toousing-los para testes em produção.

Embora haja muitos toosolve de mecanismos esses problemas, um sistema que Olá mesmo com garantias exigidas – todo caminho de saudação de um ambiente de desenvolvedor de uma caixa tootest em clusters de produção – está ausente. Olá falhas Analysis Service ajuda os desenvolvedores de aplicativos de saudação se concentrar no teste sua lógica de negócios. Olá falhas Analysis Services fornece que todos os recursos de saudação necessário tootest a interação de saudação do serviço de saudação com sistema distribuído subjacente de saudação.

### <a name="simulatinggenerating-real-world-failure-scenarios"></a>Simulação/geração de cenários reais de falha
robustez do hello tootest de um sistema distribuído contra falhas, precisamos de falhas de toogenerate um mecanismo. Em teoria, gerando uma falha, como um nó para baixo parece fácil, que ele começa a atingir Olá mesmo conjunto de problemas de consistência que o Service Fabric está tentando toosolve. Por exemplo, se quisermos tooshut para baixo de um nó, Olá necessário seguinte de saudação do fluxo de trabalho é:

1. Saudação do cliente de, emita uma solicitação de nó de desligamento.
2. Envie o nó correto da saudação solicitação toohello.
   
    a. Se o nó de saudação não for encontrado, ele apresentará falha.
   
    b. Se Olá nó for encontrado, ele deverá retornar somente se o nó de saudação é desligado.

Falha de saudação tooverify de uma perspectiva de teste, teste Olá precisa tooknow que quando esta falha seja induzida, falha de saudação realmente acontece. garantia de saudação do Service Fabric fornece é que qualquer nó Olá ficará inativo ou já foi pressionada quando o comando Olá atingido nó hello. Em qualquer caso Olá teste deve ser capaz de toocorrectly motivo sobre o estado de saudação e ter êxito ou falhar corretamente em sua validação. Um sistema implementado fora de saudação do Service Fabric toodo que mesmo conjunto de falhas foi atingido que muitos de rede, hardware e problemas de software, o que o impediria de fornecer Olá garantias anteriores. Na presença de saudação de problemas de saudação mencionado antes, Service Fabric será reconfigurar Olá cluster estado toowork problemas hello e hello, portanto, o serviço de análise de falha ainda será capaz de toogive Olá direito definido de garantias.

### <a name="generating-required-events-and-scenarios"></a>Gerando os eventos e cenários necessários
Enquanto simular uma falha do mundo real consistentemente toostart difíceis com, Olá capacidade toogenerate correlacionado falhas é cada vez mais difícil. Por exemplo, uma perda de dados ocorre em um serviço persistente com monitoração de estado quando Olá coisas a seguir ocorrem:

1. Somente um quorum de gravação de réplicas Olá são capturadas para cima na replicação. Todas as réplicas secundárias de saudação atrasem Olá primário.
2. quorum de gravação da saudação falhar devido a réplicas Olá ficar inativo (devido tooa pacote de códigos ou nó ficar inativo).
3. quorum de gravação da saudação não é possível voltar como dados de saudação para réplicas de saudação são perdidos (devido a danos toodisk ou fazer uma nova imagem de máquina).

Essas falhas correlacionadas acontecer em Olá, mundo real, mas não tão frequentemente como falhas individuais. Olá tootest de capacidade para esses cenários antes que ocorram na produção é essencial. Ainda mais importante é Olá capacidade toosimulate esses cenários com cargas de trabalho de produção em circunstâncias controladas (no meio de saudação do dia de saudação com todos os engenheiros em slides). Isso é muito melhor do que ele ocorrer por Olá primeira vez em produção às 2:00.

### <a name="unified-experience-across-different-environments"></a>Experiência unificada em ambientes diferentes
prática de saudação tradicionalmente toocreate três diferentes conjuntos de experiências, um para o ambiente de desenvolvimento hello, para testes e um para produção. modelo de saudação foi:

1. No ambiente de desenvolvimento hello, produza as transições de estado que permitem que os testes de unidade de métodos individuais.
2. No ambiente de teste hello, gerar testes de ponta a ponta de tooallow falhas que exercitam vários cenários de falha.
3. Manter Olá produção ambiente puro tooprevent qualquer natural não falhas e tooensure que há toofailure resposta humana extremamente rápida.

Na malha do serviço, por meio de saudação serviço de análise de falha, estamos propondo tooturn isso ao redor e use Olá mesmo metodologia de tooproduction do ambiente de desenvolvedor. Há dois tooachieve de maneiras isso:

1. falhas tooinduce controlado, use Olá APIs de serviços de análise de falha de um ambiente de uma caixa tooproduction de maneira Olá todos os clusters.
2. Olá toogive uma busca por que faz com que o indução automática de falhas, use Olá falhas Analysis Service toogenerate automática falhas do cluster. Taxa de Olá controle de falhas por meio da configuração habilita Olá toobe do mesmo serviço testado diferentemente em diferentes ambientes.

Com o Service Fabric, embora a escala de saudação de falhas deve ser diferente em diferentes ambientes de Olá, mecanismos real Olá seriam idênticos. Isso permite que um muito mais rápido código para implantação pipeline e hello capacidade tootest Olá serviços sob cargas do mundo real.

## <a name="using-hello-fault-analysis-service"></a>Usando Olá serviço de análise de falha
**C#**

Recursos do serviço de análise de falha são no namespace System.Fabric Olá Olá pacote Microsoft.ServiceFabric NuGet. recursos do serviço de análise de falha de Olá toouse, incluem o pacote do nuget hello como uma referência em seu projeto.

**PowerShell**

toouse PowerShell, você deve instalar Olá SDK do Service Fabric. Depois de saudação que SDK está instalado, Olá ServiceFabric do PowerShell módulo é automaticamente carregado para você toouse.

## <a name="next-steps"></a>Próximas etapas
toocreate realmente serviços de nuvem escala é tooensure crítica, antes e após a implantação, que serviços podem suportar falhas do mundo real. Na Olá mundo de serviços hoje, Olá tooinnovate capacidade rapidamente e mova o código tooproduction rapidamente é muito importante. Olá serviço de análise de falha ajuda toodo de desenvolvedores de serviço exatamente isso.

Começar a testar seus aplicativos e serviços usando internas Olá [testar cenários](service-fabric-testability-scenarios.md), ou criar seus próprios cenários de teste usando Olá [ações de falha](service-fabric-testability-actions.md) fornecida pelo Olá serviço de análise de falha.

<!--Image references-->
[0]: ./media/service-fabric-testability-overview/faultanalysisservice.png
