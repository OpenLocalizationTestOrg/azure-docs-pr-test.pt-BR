---
title: aaaArchitecture do Azure Service Fabric | Microsoft Docs
description: "Service Fabric é que uma plataforma de sistemas distribuídos usado toobuild escalonável, confiável e fácil de gerenciar aplicativos de nuvem hello. Este artigo mostra a arquitetura de saudação do Service Fabric."
services: service-fabric
documentationcenter: .net
author: rishirsinha
manager: timlt
editor: rishirsinha
ms.assetid: 6b554243-70cb-4c22-9b28-1a8b4703f45e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/19/2017
ms.author: rsinha
ms.openlocfilehash: 0268578094ad1a0010ef44ed940f828b985f6c40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-architecture"></a>Arquitetura do Service Fabric
O Service Fabric é criado com subsistemas em camadas. Esses subsistemas habilitar toowrite aplicativos que são:

* Altamente disponível
* Escalonável
* Gerenciáveis
* Testável

Olá diagrama a seguir mostra os subsistemas principais de saudação do Service Fabric.

![Diagrama da arquitetura do Service Fabric](media/service-fabric-architecture/service-fabric-architecture.png)

Em um sistema distribuído, Olá capacidade toosecurely comunicação entre nós em um cluster é crucial. Em Olá base da pilha de saudação é subsistema de transporte hello, que fornece comunicação segura entre os nós. Acima de transporte Olá subsistema está no subsistema de Federação hello, quais clusters Olá nós diferentes em uma única entidade (chamada de clusters) para que Service Fabric possa detectar falhas, executar seleção líder e fornecer roteamento consistente. subsistema de confiabilidade Hello, colocada em camadas sobre o subsistema de Federação Olá, é responsável por confiabilidade de saudação de serviços de malha do serviço por meio de mecanismos, como replicação, gerenciamento de recursos e failover. subsistema de Federação Olá também serve como base para Olá hospedagem e a ativação de subsistema, que gerencia o ciclo de vida de saudação de um aplicativo em um único nó. subsistema de gerenciamento Olá gerencia saudação do ciclo de vida de aplicativos e serviços. subsistema de capacidade de teste Olá ajuda os desenvolvedores de aplicativos testar seus serviços por meio de falhas simuladas antes e depois de implantar os ambientes de tooproduction aplicativos e serviços. Malha do serviço fornece a capacidade de saudação tooresolve locais através de seu subsistema de comunicação. Olá modelos de programação de aplicativo toodevelopers expostos são colocadas em camadas sobre esses subsistemas junto com ferramentas de tooenable do modelo de aplicativo hello.

## <a name="transport-subsystem"></a>Subsistema de transporte
subsistema de transporte Olá implementa um canal de comunicação ponto a ponto datagrama. Esse canal é usado para comunicação em clusters de malha do serviço e a comunicação entre clientes e o cluster do service fabric hello. Ele dá suporte a unidirecional e padrões de comunicação de solicitação-resposta, que fornece a base de saudação para a implementação de transmissão e multicast em Olá camada de Federação. subsistema de transporte Olá protege a comunicação usando X509 certificados ou segurança do Windows. Esse subsistema é usado internamente pelo serviço de malha e não é diretamente acessível toodevelopers para programação de aplicativo.

## <a name="federation-subsystem"></a>Subsistema de federação
Em ordem tooreason sobre um conjunto de nós em um sistema distribuído, você precisa toohave uma exibição consistente do sistema de saudação. subsistema de Federação Olá usa primitivos de comunicação Olá fornecidos pelo subsistema de transporte hello e costuras Olá vários nós em um único cluster unificado que ele pode argumentar sobre. Ele fornece primitivos de sistemas distribuído de saudação necessário por Olá outros subsistemas - detecção de falha, seleção de preenchimento e roteamento consistente. subsistema de Federação Olá baseia-se sobre as tabelas de hash distribuído com um espaço de token de 128 bits. subsistema Olá cria uma topologia de anel sobre nós hello, com cada nó em anel de saudação que é alocado a um subconjunto do espaço de token de saudação de propriedade. Para detecção de falha, a camada de saudação usa um mecanismo de concessão com base em essência superando e arbitragem. subsistema de Federação Olá também garante através de protocolos de saída que existe apenas um único proprietário de um token a qualquer momento e junção complexa. Isso oferece garantias de eleição de líder e de roteamento consistente.

## <a name="reliability-subsystem"></a>Subsistema de confiabilidade
Olá, subsistema de confiabilidade fornece Olá mecanismo toomake Olá estado de um serviço de malha do serviço altamente disponível por meio do uso de saudação do hello *replicador*, *Gerenciador de Failover*, e  *Balanceador de recurso*.

* Olá replicador garante que as alterações de estado na réplica de serviço primário hello serão automaticamente replicados toosecondary réplicas, manter consistência entre réplicas primária e secundária de saudação em um conjunto de réplicas do serviço. replicador de saudação é responsável pelo gerenciamento de quorum entre réplicas Olá Olá conjunto. Ele interage com a lista de Olá Olá failover unidade tooget de operações tooreplicate e agente de reconfiguração de saudação fornece com a configuração de saudação do conjunto de réplicas de saudação. Essa configuração indica que operações de saudação réplicas necessário toobe replicada. Serviço de malha fornece um replicador padrão chamado replicador de malha, que pode ser usado por Olá programação API toomake Olá serviço estado do modelo confiável e altamente disponível.
* Olá Gerenciador de Failover garante que quando os nós são adicionados tooor removido do cluster hello, Olá carga é automaticamente redistribuída entre nós disponíveis hello. Se um nó de cluster Olá falhar, cluster Olá reconfigurar automaticamente toomaintain disponibilidade do hello serviço réplicas.
* Olá Gerenciador de recursos coloca réplicas do serviço em um domínio de falha no cluster hello e garante que todas as unidades de failover estão operacionais. Olá Gerenciador de recursos também equilibra os recursos de serviço em Olá subjacente pool compartilhado de distribuição de carga uniforme ideal de tooachieve de nós de cluster.

## <a name="management-subsystem"></a>Subsistema de gerenciamento
subsistema de gerenciamento Olá fornece serviço de ponta a ponta e gerenciamento de ciclo de vida do aplicativo. Cmdlets do PowerShell e APIs administrativos permitem que você tooprovision, implantar, patch, atualização e desprovisionar aplicativos sem perda de disponibilidade. subsistema de gerenciamento Olá realiza isso por meio de saudação serviços a seguir.

* **Gerenciador de cluster**: Este é Olá serviço primário que interage com hello Gerenciador de Failover de aplicativos de saudação tooplace confiabilidade em nós de saudação com base em restrições de posicionamento do serviço de saudação. Olá Gerenciador de recursos no subsistema de failover garante que restrições Olá nunca são desfeitas. Gerenciador de cluster de saudação gerencia Olá do ciclo de vida de aplicativos de saudação de provisionar toode-provisão. Ele se integra com tooensure de Gerenciador de integridade Olá que a disponibilidade dos aplicativos não seja perdida de uma perspectiva de semântica de integridade durante as atualizações.
* **Gerenciador de Integridade**: esse serviço permite o monitoramento de integridade de aplicativos, serviços e entidades de cluster. Entidades de cluster (por exemplo, nós, partições de serviço e réplicas) podem relatar informações de integridade, que são agregadas no repositório de integridade centralizado hello. Essas informações de integridade fornecem um instantâneo da integridade geral point-in-time de serviços hello e nós distribuídas em vários nós no cluster hello, permitindo que você tootake as ações corretivas necessárias. Consulta de integridade que APIs permitem que você tooquery eventos de integridade de saudação relatado toohello subsistema de integridade. APIs de consulta de integridade Olá retornar do repositório de dados de integridade bruto Olá armazenados em integridade hello ou Olá agregados, interpretada de dados de integridade para uma entidade de cluster específico.
* **Repositório de imagens**: este serviço fornece armazenamento e a distribuição de saudação binários do aplicativo. Esse serviço fornece um repositório de arquivos distribuído simples onde os aplicativos de saudação são carregado tooand baixado do.

## <a name="hosting-subsystem"></a>Subsistema de hospedagem
Gerenciador de cluster de saudação informa Olá subsistema (em execução em cada nó) que os serviços de hospedagem precisa toomanage para um nó específico. Olá, em seguida, o subsistema de hospedagem gerencia saudação do ciclo de vida do aplicativo hello nesse nó. Ele interage com hello tooensure de componentes confiabilidade e integridade que réplicas de saudação são colocadas corretamente e estão íntegros.

## <a name="communication-subsystem"></a>Subsistema de comunicação
Esse subsistema fornece mensagens confiáveis dentro de descoberta de cluster e o serviço de saudação por meio do serviço de nomeação de saudação. Olá Naming service resolve local tooa do serviço de nomes de cluster hello e permite que propriedades e nomes de serviço toomanage de usuários. Usando o serviço de nomenclatura hello, os clientes com segurança comunicar com qualquer nó no hello cluster tooresolve um nome de serviço e recuperar metadados de serviço. Usando uma API de cliente de nomenclatura simple, os usuários do serviço de malha podem desenvolver serviços e clientes capazes de resolver o local de rede atual Olá apesar do dinamismo de nó ou Olá de dimensionamento do cluster Olá novamente.

## <a name="testability-subsystem"></a>Subsistema de capacidade de teste
Capacidade de teste é um conjunto de ferramentas desenvolvidas especificamente para testar serviços criados com base na malha de serviço. Olá ferramentas permitem que um desenvolvedor induzir falhas significativas e execute tooexercise de cenários de teste e validar Olá vários estados e transições que um serviço enfrentam ao longo de seu ciclo de vida, tudo em uma maneira segura e controlada. Capacidade de teste também fornece um mecanismo toorun mais testes que podem iterar várias possíveis falhas sem perder a disponibilidade. Isso fornece a você um ambiente de teste em produção.

