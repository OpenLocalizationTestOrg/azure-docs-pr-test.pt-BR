---
title: "aaaAzure a recuperação de desastres do Service Fabric | Microsoft Docs"
description: "Azure Service Fabric oferece recursos de saudação toodeal necessárias com todos os tipos de desastres. Este artigo descreve os tipos de saudação de desastres que podem ocorrer e como toodeal com eles."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 04b8348fb63e8a1c76a8f722c4c8255b339908e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="disaster-recovery-in-azure-service-fabric"></a>Recuperação de desastre no Azure Service Fabric
Uma parte crítica da entrega de alta disponibilidade é garantir que os serviços possam sobreviver a todos os tipos diferentes de falhas. Isso é especialmente importante para falhas não planejadas e fora de seu controle. Este artigo descreve alguns modos de falha comuns que poderão se transformar em desastres se não forem modelados e gerenciados corretamente. Ele também aborda tootake atenuações e ações se um desastre acontecer mesmo assim. meta de saudação é toolimit ou eliminar o risco de saudação do tempo de inatividade ou perda de dados quando ocorrem falhas, planejadas ou caso contrário, ocorrerá.

## <a name="avoiding-disaster"></a>Evitando desastres
Objetivo do Service Fabric é toohelp modelo seu ambiente e seus serviços de forma que os tipos comuns de falha não são desastres. 

De modo geral, há dois tipos de cenários de desastre/falha:

1. Falhas de hardware ou software
2. Falhas operacionais

### <a name="hardware-and-software-faults"></a>Falhas de hardware e software
Falhas de hardware e software são imprevisíveis. falhas de toosurvive de maneira mais fácil Hello está sendo executado mais cópias do serviço Olá distribuída em limites de falha de hardware ou software. Por exemplo, se o serviço está em execução somente em um computador específico, em seguida, hello falha de uma máquina é um desastre para o serviço. tooavoid de maneira simples de saudação esse desastre é tooensure serviço hello está realmente em execução em vários computadores. O teste é também necessário tooensure falha de saudação de uma máquina não interrompe Olá executando o serviço. Planejamento de capacidade garante uma instância de substituição pode ser criada em outro lugar e que redução na capacidade não sobrecarregar Olá restante dos serviços. Olá mesmo padrão funciona independentemente do que você está tentando tooavoid falha de saudação do. Por exemplo. Se você estiver preocupado com a falha de saudação de uma SAN, você executar entre várias SANs. Se você estiver preocupado com a perda de saudação de um rack de servidores, executar entre vários racks. Se você estiver preocupado com a perda de saudação de datacenters, o serviço deve ser executado em várias regiões do Azure ou data centers. 

Quando em execução nesse tipo de modo estendido, você ainda estiver assunto toosome tipos de falhas simultâneas, mas único e até mesmo várias falhas de um determinado tipo (ex: uma única falha de link VM ou de rede) são tratadas automaticamente (e portanto não há mais de "desastre"). Serviço de malha fornece vários mecanismos para expandir o cluster hello e identificadores de retorno de nós com falha e serviços. Service Fabric também permite a execução de muitas instâncias de seus serviços em ordem tooavoid esses tipos de falhas não planejadas de ativação para desastres reais.

Pode haver razões por que a execução de um toospan de implantação grande o suficiente sobre falhas não é viável. Por exemplo, talvez demore mais recursos de hardware que não estiver disposto toopay para toohello relativo chance de falha. Ao lidar com aplicativos distribuídos, é possível que os saltos de comunicação adicionais ou os custos de replicação de estado entre distâncias geográficas causem latência inaceitável. Esse limite varia com cada aplicativo. Para falhas de software especificamente, Olá falha pode estar no serviço de saudação que você está tentando tooscale. Nesse caso mais cópias não impedir um desastre hello, desde que a condição de falha de saudação correlacionada em todas as instâncias de saudação.

### <a name="operational-faults"></a>Falhas operacionais
Mesmo se o serviço está distribuído globo Olá com muitos redundâncias, ainda pode passar eventos desastrosos. Por exemplo, se alguém acidentalmente reconfigura o nome de dns Olá para serviço hello, ou exclui-lo imediatamente. Por exemplo, digamos que você tivesse um serviço do Service Fabric com estado e alguém excluísse esse serviço acidentalmente. A menos que haja alguns outros mitigação, esse serviço e todos os estados de saudação tinha é agora desapareceu. Esses tipos de desastres operacionais ("ops") exigem mitigações e etapas de recuperação diferentes do que as que são necessárias para falhas não planejadas regulares. 

Olá melhores maneiras tooavoid esses tipos de falhas operacionais são para
1. restringir o ambiente de toohello acesso operacionais
2. realizar auditorias rígidas de operações perigosas
3. impor a automação, evitar manual ou alterações fora da banda e validar alterações específicas no ambiente real Olá antes aplicando-los
4. garantir que operações destrutivas sejam "suaves". Operações suaves não entram em efeito imediatamente ou podem ser desfeitas dentro de uma janela de tempo

Serviço de malha fornece alguns mecanismos falhas operacionais tooprevent, como fornecer [baseada em função](service-fabric-cluster-security-roles.md) controle para operações de cluster de acesso. No entanto, a maioria dessas falhas operacionais exige esforços organizacionais e outros sistemas. O Service Fabric fornece alguns mecanismos para sobreviver a falhas operacionais, mais notoriamente o backup e restauração para serviços com estado.

## <a name="managing-failures"></a>Gerenciando falhas
meta de saudação do Service Fabric é quase sempre o gerenciamento automático de falhas. No entanto, em ordem toohandle alguns tipos de falhas, serviços devem ter um código adicional. Outros tipos de falhas _não_ devem ser resolvidas automaticamente por motivos de segurança e de continuidade de negócios. 

### <a name="handling-single-failures"></a>Lidando com falhas únicas
Um único computador pode falhar por diversos tipos de motivos. Alguns deles são causados pelo hardware, como falhas de fontes de alimentação e de hardware de rede. Outras falhas estão no software. Esses incluem falhas de sistema operacional atual de saudação e o próprio serviço de saudação. Serviço de malha detecta automaticamente esses tipos de falhas, inclusive os casos em que a máquina Olá é isolada de outros computadores devido a problemas de toonetwork.

Independentemente do tipo de saudação do serviço, executando uma única instância resultados em tempo de inatividade para esse serviço se essa cópia única de código Olá falhar por qualquer motivo. 

Em ordem toohandle qualquer falha simples, a coisa mais simples Olá, que você pode fazer é tooensure que os serviços são executados em mais de um nó por padrão. Para serviços sem estado, isso pode ser feito tendo um `InstanceCount` maior que 1. Para serviços de monitoração de estado, recomendação mínimo Olá é sempre um `TargetReplicaSetSize` e `MinReplicaSetSize` pelo menos 3. Executar mais cópias do código de seu serviço garante que o serviço seja capaz de lidar com qualquer falha única automaticamente. 

### <a name="handling-coordinated-failures"></a>Lidando com falhas coordenadas
Falhas de coordenada podem ocorrer em um cluster de conclusão tooeither planejada ou falhas de infraestrutura não planejado e as alterações ou alterações de software planejado. O Service Fabric cria zonas de infraestrutura que passam por falhas coordenadas e são chamadas de Domínios de Falha. Áreas que passarão por alterações de software coordenadas são chamadas de Domínios de Atualização. Há mais informações sobre os domínios de falha e de atualização [neste documento](service-fabric-cluster-resource-manager-cluster-description.md), que descreve a topologia e a definição dos clusters.

Por padrão, o Service Fabric considera os domínios de falha e de atualização ao planejar onde os serviços devem ser executados. Por padrão, o serviço de malha tenta tooensure seus serviços executados em vários domínios de falha e atualização para que se ocorrerem alterações planejadas ou os serviços permanecerão disponíveis. 

Por exemplo, digamos que a falha de uma fonte de energia faz com que um rack de máquinas toofail simultaneamente. Com várias cópias do serviço Olá executando perda de saudação de muitas máquinas em falha de domínio se transforma em apenas outro exemplo de falha único para um determinado serviço. É por isso gerenciar domínios de falha é crítico tooensuring alta disponibilidade de seus serviços. Ao executar o Service Fabric no Azure, os domínios de falha são gerenciados automaticamente. Em outros ambientes, eles podem não ser. Se você estiver criando suas próprias clusters no local, ser toomap se e planejar o layout de domínio de falha corretamente.

Domínios de atualização são úteis para modelagem de áreas onde o software será toobe atualizado no hello mesmo tempo. Por isso, domínios de atualização também geralmente definir limites Olá onde o software é desativado durante as atualizações planejadas. Execute as atualizações de malha do serviço e seus serviços Olá mesmo modelo. Para obter mais informações sobre atualizações sem interrupção, domínios de atualização e modelo de integridade de malha do serviço de saudação que ajuda a impedir que alterações inadvertidas afetando cluster hello e seu serviço, consulte estes documentos:

 - [Atualização de aplicativo](service-fabric-application-upgrade.md)
 - [Tutorial de atualização de aplicativo](service-fabric-application-upgrade-tutorial.md)
 - [Modelo de integridade do Service Fabric](service-fabric-health-introduction.md)

Você pode visualizar o layout de saudação do cluster usando o mapa de cluster Olá fornecido no [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md):

<center>
![Nós espalhados pelos domínios de falha no Service Fabric Explorer][sfx-cluster-map]
</center>

> [!NOTE]
> Modelagem de áreas de falha, atualizações sem interrupção, executando várias instâncias do seu código de serviço e o estado, posicionamento regras tooensure seus serviços executados em domínios de falha e atualização e monitoramento de integridade interna são apenas **alguns** de saudação recursos fornecidos pelo serviço de malha em problemas operacionais do pedido tookeep normal e falhas tornem desastres. 
>

### <a name="handling-simultaneous-hardware-or-software-failures"></a>Lidando com falhas simultâneas de hardware ou software
Acima, falamos sobre falhas únicas. Como você pode ver, são toohandle fácil para os serviços com e sem monitoração apenas mantendo mais cópias do código de saudação (e estado) em execução em falha e domínios de atualização. Várias falhas aleatórias simultâneas também podem ocorrer. Esses são mais prováveis desastres reais tooan de toolead.


### <a name="random-failures-leading-tooservice-failures"></a>Falhas aleatórias esquerda tooservice falhas
Vamos supor que o serviço de saudação tinha um `InstanceCount` de 5 e vários nós executando essas instâncias todos falhou em Olá mesmo tempo. O Service Fabric responde criando automaticamente instâncias de substituição em outros nós. Ele continuará criando substituições até que o serviço hello está de volta tooits desejado a contagem de instâncias. Como outro exemplo, digamos que houve um serviço sem monitoração de estado com um `InstanceCount`de -1, que significa que ele é executado em todos os nós válido Olá cluster. Digamos que algumas dessas instâncias foram toofail. Nesse caso, o Service Fabric observa que o serviço de saudação não está no estado desejado e tenta toocreate instâncias de saudação em nós Olá onde eles estão ausentes. 

Para serviços com estado situação Olá depende se Olá serviço tem estado persistente ou não. Também depende do serviço de saudação quantas réplicas e quantas tentativas. Determinar se um desastre ocorreu para um serviço com estado e gerenciá-lo é um processo de três estágios:

1. Determinar se houve perda de quorum ou não
 - Uma perda de quorum é a qualquer momento em que a maioria das réplicas de saudação de um serviço com monitoração de estado estão inativos em Olá mesmo tempo, incluindo Olá primário.
2. Determinando se a perda de quorum Olá é permanente ou não
 - A maioria do tempo de saudação falhas são transitórias. Os processos são reiniciados, os nós são reiniciados, as VMs são relançadas e as partições de rede se recuperam. No entanto, algumas vezes as falhas são permanentes. 
    - Para serviços sem estado persistente, a falha de um quorum ou mais de réplicas causa _imediatamente_ uma perda de quorum permanente. Quando o Service Fabric detecta a perda de quorum em um serviço não persistente com monitoração de estado, ele prossegue imediatamente perda toostep 3 declarando (potencial). Continuar toodataloss faz sentido, porque o Service Fabric sabe que não faz sentido em espera de saudação réplicas toocome novamente, porque, mesmo se eles foram recuperados, eles seriam vazios.
    - Para serviços persistentes com monitoração de estado, uma falha de um quorum ou mais réplicas faz com que o Service Fabric toostart esperando Olá volta toocome de réplicas e quorum de restauração. Isso resulta em uma interrupção de serviço para qualquer _grava_ toohello afetado partição (ou "conjunto de réplicas") do serviço de saudação. No entanto, leituras ainda podem ser possíveis, com garantias de consistência reduzidas. a quantidade de tempo que o Service Fabric aguarda toobe quorum restaurado padrão Olá é infinita, como continuar é um evento de perda (potencial) e executa outros riscos. Substituindo saudação padrão `QuorumLossWaitDuration` valor é possível, mas não é recomendado. Em vez disso, no momento, todos os esforços devem ser feitos Olá toorestore para baixo de réplicas. Isso exige colocando nós Olá que estão abaixo back up e garantir que eles podem remontar unidades Olá onde o estado persistente local Olá armazenados. Se a perda de quorum Olá é causada por falha de processo, o Service Fabric automaticamente tenta toorecreate processos de saudação e reinicie réplicas hello dentro deles. Se isso falhar, o Service Fabric relatará erros de integridade. Se eles podem ser resolvidos réplicas Olá geralmente voltar. Às vezes, no entanto, as réplicas de saudação não podem ser trazidas de volta. Por exemplo, unidades Olá podem todos falharam, ou máquinas Olá fisicamente destruído alguma forma. Nesses casos, agora temos um evento de perda de quorum permanente. tootell Service Fabric toostop aguardando Olá para baixo toocome de réplicas, um administrador de cluster deve determinar quais partições dos quais serviços são afetados e chamar hello `Repair-ServiceFabricPartition -PartitionId` ou ` System.Fabric.FabricClient.ClusterManagementClient.RecoverPartitionAsync(Guid partitionId)` API.  Essa API permite especificar a ID de saudação do hello partição toomove QuorumLoss e na perda potencial.

> [!NOTE]
> É _nunca_ toouse seguro essa API diferente de uma maneira de destino em partições específicas. 
>

3. Determinando se houve perda de dados real e restaurando backups
  - Quando o Service Fabric chama Olá `OnDataLossAsync` método é sempre porque _suspeita_ perda. Service Fabric garante que essa chamada é entregue toohello _melhor_ réplica restante. Isso é que qualquer réplica fez Olá grande progresso. Olá motivo dizemos sempre _suspeita_ perda é que é possível que essa réplica restantes Olá realmente tem todos os mesmo estado Olá primário fez quando ele foi desativado. No entanto, sem que toocompare estado-lo, não é possível bom para serviço de malha ou operadores tooknow com certeza. Neste ponto, serviço de malha também sabe Olá outras réplicas não são provenientes de volta. Que foi decisão Olá feita quando é interrompida aguardando Olá tooresolve de perda de quorum em si. melhor o curso de ação para o serviço Olá Olá geralmente é toofreeze e aguarde intervenção administrativa específica. Então o que faz uma implementação típica de saudação `OnDataLossAsync` método fazer?
  - Primeiro, registrar em log que `OnDataLossAsync` foi disparado, bem como disparar os alertas administrativos necessários.
   - Normalmente neste ponto, toopause e aguarde mais decisões e ações manuais toobe realizada. Isso ocorre porque, mesmo que os backups estão disponíveis, eles precisarão toobe preparado. Por exemplo, se os dois serviços diferentes coordenam informações, esses backups podem ser necessário toobe modificada na ordem tooensure que depois que a restauração Olá acontece que informações Olá esses dois serviços importam é consistente. 
  - Geralmente há também alguns outros Telemetria ou exaustão do serviço de saudação. Esses metadados podem estar contidos em outros serviços ou em logs. Essas informações podem ser usado toodetermine necessário se houver qualquer chamada recebida e processada no hello primário que não estava presente na réplica específica do hello toothis backup ou replicado. Esses talvez seja necessário toobe toohello reproduzido ou adicionado backup antes da restauração é viável.  
   - Comparações de saudação restante toothat de estado da réplica contido em todos os backups que estão disponíveis. Se usando coleções confiáveis do Service Fabric hello, existem ferramentas e processos disponível para fazer isso, descrito em [neste artigo](service-fabric-reliable-services-backup-restore.md). meta de saudação é toosee se estado Olá réplica Olá é suficiente ou o backup Olá pode estar ausente.
  - Uma vez comparação Olá é feita, e se necessário Olá Restauração concluída, o código de serviço Olá deve retornar true se foram feitas alterações de estado. Se a réplica Olá determinou que ele era Olá melhor cópia disponível do estado de saudação e feito alterações, retornará false. True indica que qualquer _outra_ réplica restante agora pode estar inconsistente com esta. Elas serão descartadas e recriadas desta réplica. False indica que nenhuma alteração de estado foram feitas, então Olá outras réplicas podem manter o que eles têm. 

É extremamente importante que os autores do serviço pratiquem cenários potenciais de falha e perda de dados antes que os serviços sejam implantados em produção. tooprotect contra a possibilidade de saudação de perda, é importante tooperiodically [backup Olá estado](service-fabric-reliable-services-backup-restore.md) de qualquer do seu armazenamento com redundância geográfica de tooa services com monitoração de estado. Você também deve garantir que você tenha Olá capacidade toorestore-lo. Como são realizados backups de vários serviços diferentes em momentos diferentes, é necessário tooensure após uma restauração de seus serviços tem uma exibição consistente uns dos outros. Por exemplo, considere uma situação em que um serviço gera um número e armazena-o e as envia serviço tooanother que também armazena. Após uma restauração, talvez você descubra que serviço segundo Olá tem o número de saudação mas Olá primeiro não, porque seu backup não inclui essa operação.

Se você descobrir que Olá restantes réplicas são toocontinue insuficiente em um cenário de perda, e você não pode reconstruir o estado do serviço de telemetria ou exaustão, frequência Olá dos seus backups determina o melhor ponto de recuperação possíveis objetivo (RPO) . O Service Fabric fornece várias ferramentas para testar vários cenários de falha, incluindo a perda de quorum e de dados permanente que exige restauração de um backup. Esses cenários são incluídos como parte das ferramentas de capacidade de teste do Service Fabric, gerenciado pelo Olá serviço de análise de falha. Mais informações sobre essas ferramentas e padrões estão disponíveis [aqui](service-fabric-testability-overview.md). 

> [!NOTE]
> Serviços do sistema também podem sofrer perda de quorum, com impacto Olá sendo toohello específico de serviço em questão. Por exemplo, perda de quorum no serviço de nomeação de saudação afeta a resolução de nome, enquanto a perda de quorum no serviço de Gerenciador de failover Olá bloqueia failovers e criação de novos serviços. Enquanto os serviços do sistema do Service Fabric Olá seguem Olá mesmo padrão como os serviços de gerenciamento de estado, não é recomendável que você deverá tentar toomove-las de perda de Quorum e em potencial perda. recomendação de saudação em vez disso, é muito[busca suporte](service-fabric-support.md) toodetermine uma solução que é direcionado a situação específica tooyour.  Geralmente, é preferível toosimply espera até Olá para réplicas de retorno.
>

## <a name="availability-of-hello-service-fabric-cluster"></a>Disponibilidade do cluster do Service Fabric Olá
Em geral, Olá Service Fabric cluster é um ambiente altamente distribuído sem pontos únicos de falha. Uma falha de qualquer nó não causará problemas de confiabilidade para cluster hello, ou disponibilidade principalmente porque os serviços do sistema do Service Fabric Olá sigam Olá mesmas diretrizes fornecidas anteriormente: ele sempre é executado com três ou mais réplicas por padrão e aqueles serviços do sistema que são sem monitoração de estado é executado em todos os nós. rede de malha do serviço subjacente Hello e camadas de detecção de falha são totalmente distribuídas. A maioria dos serviços do sistema podem ser recriados de metadados no cluster hello ou saber como tooresynchronize seu estado em outros locais. disponibilidade de saudação do cluster Olá poderá ser comprometida se os serviços do sistema invadir quorum perda situações como as descritas acima. Nesses casos você não pode ser capaz de tooperform certas operações em cluster hello como iniciar uma atualização ou implantação de novos serviços, mas o próprio cluster Olá ainda estiver ativo. Serviços em execução já continuará em execução nas seguintes condições, a menos que eles exigem gravações toohello sistema serviços toocontinue funcionando. Por exemplo, se Olá Failover Manager está em perda de quorum todos os serviços continuarão toorun, mas todos os serviços que não não será capaz de tooautomatically reinicialização, pois isso requer o envolvimento Olá Olá Gerenciador de Failover. 

### <a name="failures-of-a-datacenter-or-azure-region"></a>Falhas de um data center ou região do Azure
Em casos raros, um data center físico pode se tornar indisponível devido tooloss de energia ou conectividade de rede. Nesses casos, seus clusters e serviços do Service Fabric nesse data center ou região do Azure ficarão indisponíveis. No entanto, _os dados ficam preservados_. Para clusters em execução no Azure, você pode exibir atualizações em interrupções no hello [página status do Azure][azure-status-dashboard]. Em Olá altamente improvável que um data center físico é parcialmente ou totalmente destruído, quaisquer clusters de malha do serviço hospedados lá ou serviços hello dentro deles poderão ser perdidos. Isso inclui qualquer estado que não esteja salvo em backup fora desse data center ou região.

Há duas estratégias diferentes para sobreviventes Olá falha prolongada ou permanente de um único data center ou região. 

1. Executar clusters separados do Service Fabric em várias dessas regiões e utilizar um mecanismo para failover e failback entre esses ambientes. Esse tipo de modelo ativo-ativo ou ativo-passivo multi-cluster requer código adicional de gerenciamento e operação. Isso também exige a coordenação de backups dos serviços de saudação em um data center ou região para que eles estejam disponíveis em outros data centers ou regiões quando uma falha. 
2. Executar um único cluster do Service Fabric que abrange vários data centers ou regiões. Olá mínimos de configuração com suporte para isso é três data centers ou regiões. Olá número recomendado de regiões ou data centers é cinco. Isso requer uma topologia de clusters mais complexa. No entanto, hello vantagem desse modelo é que a falha de um data center ou região é convertida de um desastre em uma falha normal. Essas falhas podem ser manipuladas pelos mecanismos de saudação que funcionam para clusters de dentro de uma única região. Domínios de falha, domínios de atualização e regras de posicionamento do Service Fabric garantem que as cargas de trabalho sejam distribuídas para que tolerem falhas normais. Para obter mais informações sobre políticas que podem ajudar a operar serviços nesse tipo de cluster, leia sobre as [políticas de posicionamento](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md)

### <a name="random-failures-leading-toocluster-failures"></a>Falhas aleatórias esquerda toocluster falhas
Malha do serviço tem o conceito de saudação de nós de propagação. Esses são nós que mantêm a disponibilidade de saudação do cluster subjacente hello. Esses nós ajudam tooensure Olá cluster permanece backup estabelecendo concessões com outros nós e servindo como tiebreakers durante determinados tipos de falhas de rede. Se falhas aleatórias remover a maioria de nós de propagação de saudação em cluster hello e elas não fossem trazidas de volta, cluster Olá desligado automaticamente. No Azure, nós de propagação são automaticamente gerenciadas: eles são distribuídos em Olá disponível domínios de falha e atualização, e se um nó de semente único é removido do cluster de saudação outra será criada em seu lugar. 

Em clusters Service Fabric independentes e do Azure, Olá "Tipo de nó primário" é hello aquele executado sementes de saudação. Ao definir um tipo de nó primário, Service Fabric será automaticamente tirar proveito do número de saudação de nós fornecida pela criação de nós de propagação de too9 e 9 réplicas de cada um dos serviços do sistema hello. Se um conjunto de falhas aleatórias ocupa a maior parte dessas réplicas do serviço de sistema simultaneamente, serviços do sistema Olá inserirá perda de quorum, conforme descrito acima. Se a maioria de nós de propagação de saudação é perdida, cluster Olá será desligado depois.

## <a name="next-steps"></a>Próximas etapas
- Saiba como toosimulate várias falhas usando Olá [framework de capacidade de teste](service-fabric-testability-overview.md)
- Leia outros recursos de recuperação de desastres e alta disponibilidade. A Microsoft publicou várias orientações sobre estes tópicos. Enquanto alguns desses documentos consulte toospecific técnicas para uso em outros produtos, eles contêm várias práticas recomendadas gerais, que você pode aplicar no contexto de malha do serviço Olá também:
  - [Lista de verificação de disponibilidade](../best-practices-availability-checklist.md)
  - [Executando a análise de recuperação de desastre](../sql-database/sql-database-disaster-recovery-drills.md)
  - [Recuperação de desastre e alta disponibilidade para aplicativos do Azure][dr-ha-guide]
- Saiba mais sobre as [opções de suporte do Service Fabric](service-fabric-support.md)

<!-- External links -->

[repair-partition-ps]: https://msdn.microsoft.com/library/mt163522.aspx
[azure-status-dashboard]:https://azure.microsoft.com/status/
[azure-regions]: https://azure.microsoft.com/regions/
[dr-ha-guide]: https://msdn.microsoft.com/library/azure/dn251004.aspx


<!-- Images -->

[sfx-cluster-map]: ./media/service-fabric-disaster-recovery/sfx-clustermap.png
