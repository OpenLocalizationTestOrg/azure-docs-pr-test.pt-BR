---
title: "aaaService Gerenciador de recursos de Cluster de malha - integração do gerenciamento | Microsoft Docs"
description: "Uma visão geral dos pontos de integração de saudação entre hello Gerenciador de recursos de Cluster e gerenciamento de malha do serviço."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 956cd0b8-b6e3-4436-a224-8766320e8cd7
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 9a24c9de121fbe2e8e5e8e4d117e64686918936a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="cluster-resource-manager-integration-with-service-fabric-cluster-management"></a>Integração do Gerenciador de Recursos de Cluster com o gerenciamento de cluster do Service Fabric
Olá Gerenciador de recursos de Cluster do serviço de malha não faça upgrade na malha do serviço, mas ele está envolvido. Olá primeiro maneira Olá Gerenciador de recursos de Cluster ajuda com o gerenciamento pelo controle Olá desejada do estado do cluster hello e serviços hello dentro dele. Olá Gerenciador de recursos de Cluster envia relatórios de integridade quando ele não é possível colocar o cluster Olá na configuração de saudação desejado. Por exemplo, se houver insuficiente Olá capacidade Gerenciador de recursos de Cluster envia indicando um problema de saudação de erros e avisos de integridade. Outra parte da integração tem toodo com o funcionam das atualizações. Olá Gerenciador de recursos de Cluster altera seu comportamento um pouco durante as atualizações.  

## <a name="health-integration"></a>Integração da integridade
Olá Gerenciador de recursos de Cluster rastreia constantemente regras Olá definidas para colocar seus serviços. Ele também acompanha Olá restantes de capacidade para cada métrica em nós de saudação e em cluster Olá em cluster hello como um todo. Se ele não puder atender a essas regras ou se não houver capacidade insuficiente, erros e avisos de integridade serão emitidos. Por exemplo, se um nó está sobre capacidade e hello Gerenciador de recursos de Cluster tentará situação de saudação toofix movendo serviços. Se ele não pode corrigir a situação Olá emite um aviso de integridade indicando qual nó está acima da capacidade e para quais métricas.

Outro exemplo de avisos de integridade do Gerenciador de recursos de saudação é violações de restrições de posicionamento. Por exemplo, se você tiver definido uma restrição de posicionamento (como `“NodeColor == Blue”`) e Olá Gerenciador de recursos detecta uma violação de restrição, ele emite um aviso de integridade. Isso é verdadeiro para personalizado restrições e saudação padrão (como Olá restrições de domínio de falha e atualização do domínio).

Eis um exemplo de tal relatório de integridade. Nesse caso, o relatório de integridade Olá é para uma das partições do serviço de sistema hello. mensagem de saudação do integridade indica Olá réplicas dessa partição temporariamente são incluídas em poucos domínios de atualização.

```posh
PS C:\Users\User > Get-WindowsFabricPartitionHealth -PartitionId '00000000-0000-0000-0000-000000000001'


PartitionId           : 00000000-0000-0000-0000-000000000001
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.PLB', Property='ReplicaConstraintViolation_UpgradeDomain', HealthState='Warning', ConsiderWarningAsError=false.

ReplicaHealthStates   :
                        ReplicaId             : 130766528804733380
                        AggregatedHealthState : Ok

                        ReplicaId             : 130766528804577821
                        AggregatedHealthState : Ok

                        ReplicaId             : 130766528854889931
                        AggregatedHealthState : Ok

                        ReplicaId             : 130766528804577822
                        AggregatedHealthState : Ok

                        ReplicaId             : 130837073190680024
                        AggregatedHealthState : Ok

HealthEvents          :
                        SourceId              : System.PLB
                        Property              : ReplicaConstraintViolation_UpgradeDomain
                        HealthState           : Warning
                        SequenceNumber        : 130837100116930204
                        SentAt                : 8/10/2015 7:53:31 PM
                        ReceivedAt            : 8/10/2015 7:53:33 PM
                        TTL                   : 00:01:05
                        Description           : hello Load Balancer has detected a Constraint Violation for this Replica: fabric:/System/FailoverManagerService Secondary Partition 00000000-0000-0000-0000-000000000001 is
                        violating hello Constraint: UpgradeDomain Details: UpgradeDomain ID -- 4, Replica on NodeName -- Node.8 Currently Upgrading -- false Distribution Policy -- Packing
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Ok->Warning = 8/10/2015 7:13:02 PM, LastError = 1/1/0001 12:00:00 AM
```

Veja o que a mensagem de integridade está nos dizendo:

1. Todas as réplicas de saudação próprios estão íntegros: possuem AggregatedHealthState: Okey
2. Olá restrição de distribuição de atualização do domínio no momento está sendo violado. Isso significa que um determinado Domínio de Atualização tem mais réplicas desta partição do que deveria.
3. Nó que contém a violação de causando Olá Olá réplica. Nesse caso é Olá nó com o nome hello "Node.8"
4. Se uma atualização estiver ocorrendo no momento para essa partição ("Atualmente em Atualização - falso")
5. Olá a política de distribuição para este serviço: "Distribuição política--remessa". Isso é controlado por Olá `RequireDomainDistribution` [política de posicionamento](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md#requiring-replica-distribution-and-disallowing-packing). "Empacotamento" indica que, nesse caso, DomainDistribution _não_ era necessária, portanto sabemos que a política de posicionamento não era especificada para esse serviço. 
6. Quando o relatório de saudação aconteceu - 8/10/2015 19:13:02: 00

Informações como este alerta potências disparados em toolet de produção, você sabe, algo deu errado e também é usado toodetect e interromper atualizações incorretas. Nesse caso, queremos toosee se conseguimos descobrir por que Olá Resource Manager teve toopack réplicas de saudação em Olá domínio de atualização. Empacotando geralmente é transitório pois nós Olá Olá outros domínios de atualização foram para baixo, por exemplo.

Digamos que Olá Gerenciador de recursos de Cluster está tentando tooplace alguns serviços, mas não existem quaisquer soluções que funcionam. Quando os serviços não podem ser colocados, é normalmente para uma saudação motivos a seguir:

1. Algumas condições transitórias tornou impossível tooplace essa instância de serviço ou a réplica corretamente
2. requisitos de posicionamento do serviço Olá são satisfatória.

Nesses casos, os relatórios de integridade da saudação Gerenciador de recursos de Cluster ajudarão-lo a determinar por que o serviço Olá não pode ser colocado. Chamamos essa sequência de eliminação do processo Olá restrição. Durante a ele, sistema Olá orienta restrições Olá configurado afetando registros e serviço Olá que eliminam. Dessa forma, quando os serviços não são capaz toobe colocado, você pode ver quais nós foram eliminados e por quê.

## <a name="constraint-types"></a>Tipos de restrição
Vamos falar sobre cada uma das restrições de diferentes Olá nesses relatórios de integridade. Você verá integridade mensagens relacionadas toothese restrições ao réplicas não podem ser colocadas.

* **ReplicaExclusionStatic** e **ReplicaExclusionDynamic**: essas restrições indica que uma solução foi rejeitada porque dois objetos de serviço do hello mesma partição toobe colocaria em Olá mesmo nó. Isso não é permitido, pois a falha desse nó afetaria demais nessa partição. ReplicaExclusionStatic e ReplicaExclusionDynamic são quase Olá mesmo diferenças de regra e hello não são muito importam. Se você estiver vendo uma sequência de eliminação de restrição que contém qualquer restrição ReplicaExclusionStatic ou ReplicaExclusionDynamic, Olá Gerenciador de recursos de Cluster Olá considera se não houver nós suficientes. Isso requer restantes soluções toouse esses posicionamentos inválidos que não são permitidos. Olá outras restrições na sequência de saudação serão geralmente Conte-nos por que nós estão sendo eliminados em primeiro lugar de saudação.
* **PlacementConstraint**: se você vir essa mensagem, isso significa que podemos eliminado alguns nós porque eles não correspondem a restrições de posicionamento do serviço hello. Podemos rastrear restrições de posicionamento de saudação configurada atualmente como parte desta mensagem. Isso é normal se houver restrições de posicionamento em vigor. No entanto, se a restrição de posicionamento está causando incorretamente muitos toobe nós eliminado trata de como você perceberá.
* **NodeCapacity**: essa restrição significa que Olá Gerenciador de recursos de Cluster não pôde colocar réplicas Olá em Olá indicado nós porque que colocaria acima da capacidade.
* **Afinidade**: essa restrição indica que é não pôde colocar réplica Olá em nós Olá afetado porque isso causaria uma violação de restrição de afinidade de saudação. Veja mais informações sobre afinidade [neste artigo](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md)
* **FaultDomain** e **UpgradeDomain**: esta restrição elimina nós se inserir réplica Olá Olá indicado nós causaria a remessa em um domínio de atualização ou a falha específica. Vários exemplos de abordar essa restrição são apresentados no tópico de saudação em [restrições de domínio falha e atualização e o comportamento resultante](service-fabric-cluster-resource-manager-cluster-description.md)
* **PreferredLocation**: normalmente não verá essa restrição removendo nós da solução hello, pois ele é executado como uma otimização, por padrão. Olá preferencial a restrição de local também está presente durante as atualizações. Durante a atualização é usado toomove serviços back toowhere, que estavam quando Olá atualização iniciada.

## <a name="blocklisting-nodes"></a>Incluir os nós em lista de bloqueio
Outra mensagem hello Gerenciador de recursos de Cluster relatórios de integridade é quando os nós são blocklisted. Você pode pensar na inclusão em uma lista de bloqueio como uma restrição temporária aplicada automaticamente a você. Os nós são incluídos na lista de bloqueio quando sofrem falhas repetidas ao iniciar instâncias desse tipo de serviço. Os nós são incluídos em uma lista de bloqueio de acordo com o tipo de serviço. Um nó pode ser incluído em uma lista de bloqueio para um tipo de serviço, mas não outro. 

Você verá blocklisting ativada com frequência durante o desenvolvimento: alguns bugs que faz com que o toocrash de host de serviço na inicialização. Malha do serviço tenta host de serviço toocreate Olá algumas vezes e continua a ocorrer falha de saudação. Após algumas tentativas, nó Olá obtém blocklisted e Olá Gerenciador de recursos de Cluster tentará toocreate serviço de saudação em outro lugar. Se essa falha continuar acontecendo em vários nós, é possível que todos nós válido Olá Olá cluster terminam bloqueada. Blocklisting também pode remover tantos nós que insuficiente pode iniciar com êxito a escala do hello serviço toomeet Olá desejado. Normalmente, você verá erros adicionais ou avisos de saudação Gerenciador de recursos de Cluster que indica se o serviço de hello está abaixo da réplica desejada hello ou contagem de instância, bem como mensagens de integridade indicando falha que Olá é que está levando toohello blocklisting em primeiro lugar de saudação.

A inclusão na lista de bloqueio não é uma condição permanente. Após alguns minutos, nó de saudação for removido da lista de bloqueios de saudação e Service Fabric ativar serviços Olá nesse nó novamente. Se os serviços continuam toofail, o nó de saudação é blocklisted para esse tipo de serviço novamente. 

### <a name="constraint-priorities"></a>Prioridades de restrição

> [!WARNING]
> A alteração das prioridades de restrição não é recomendada e pode ter efeitos adversos consideráveis em seu cluster. Olá abaixo informações é fornecido para referência de prioridades de restrição de padrão de saudação e seu comportamento. 
>

Todas essas restrições, você pode ter pensado "Ei – acho que restrições de domínio de falha são hello mais importante no sistema. Em ordem tooensure hello restrição de domínio de falha não for violada, estou está disposto tooviolate outras restrições. "

As restrições podem ser configuradas com níveis de prioridade diferentes. Estes são:

   - "inflexível" (0)
   - "flexível" (1)
   - "otimização” (2)
   - "desativado" (-1). 
   
A maioria das restrições de saudação é configurada como restrições de disco rígidas por padrão.

Alterar a prioridade de saudação de restrições é incomum. Houve vezes onde prioridades de restrição necessário toochange, normalmente toowork em torno de alguns bugs ou comportamento que estava afetando o ambiente de saudação. Geralmente flexibilidade de saudação da infraestrutura de prioridade de restrição Olá funcionou muito bem, mas ela não é necessária com frequência. A maioria do tempo de saudação tudo o que se encontra em suas prioridades padrão. 

níveis de prioridade de saudação não significam que uma restrição de determinado _será_ ser violado, nem que ele sempre será atendido. As prioridades de restrição definem uma ordem de imposição das restrições. As prioridades definem compensações hello quando for impossível toosatisfy todas as restrições. Normalmente, todas as restrições de saudação podem ser atendidas a menos que haja algo mais ambiente de saudação. Alguns exemplos de cenários que levarão tooconstraint violações são restrições conflitantes, ou grandes números de falhas simultâneas.

Em situações avançadas, você pode alterar as prioridades de restrição de saudação. Por exemplo, digamos que você desejava tooensure que afinidade sempre seria violada quando problemas de capacidade do nó toosolve necessário. tooachieve isso, você pode definir a prioridade de saudação da restrição de afinidade Olá muito "soft" (1) e deixe a restrição de capacidade de saudação definida muito "grave" (0).

valores de prioridade saudação padrão para as diferentes restrições de saudação são especificados em Olá configuração a seguir:

ClusterManifest.xml

```xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PlacementConstraintPriority" Value="0" />
            <Parameter Name="CapacityConstraintPriority" Value="0" />
            <Parameter Name="AffinityConstraintPriority" Value="0" />
            <Parameter Name="FaultDomainConstraintPriority" Value="0" />
            <Parameter Name="UpgradeDomainConstraintPriority" Value="1" />
            <Parameter Name="PreferredLocationConstraintPriority" Value="2" />
        </Section>
```

via ClusterConfig.json para implantações Autônomas ou Template.json para clusters hospedados pelo Azure:

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "PlacementConstraintPriority",
          "value": "0"
      },
      {
          "name": "CapacityConstraintPriority",
          "value": "0"
      },
      {
          "name": "AffinityConstraintPriority",
          "value": "0"
      },
      {
          "name": "FaultDomainConstraintPriority",
          "value": "0"
      },
      {
          "name": "UpgradeDomainConstraintPriority",
          "value": "1"
      },
      {
          "name": "PreferredLocationConstraintPriority",
          "value": "2"
      }
    ]
  }
]
```

## <a name="fault-domain-and-upgrade-domain-constraints"></a>Restrições de domínio de falha e de atualização
Olá Gerenciador de recursos de Cluster deseja tookeep serviços distribuídos entre domínios de falha e atualização. Ele simula isso como uma restrição de dentro do Gerenciador de recursos do Cluster Olá mecanismo. Para obter mais informações sobre como eles são usados e seu comportamento específico, consulte o artigo de saudação em [configuração de cluster](service-fabric-cluster-resource-manager-cluster-description.md#fault-and-upgrade-domain-constraints-and-resulting-behavior).

Olá Gerenciador de recursos de Cluster pode ser necessário toopack duas réplicas em um domínio de atualização na ordem toodeal com atualizações, falhas ou outras violações de restrição. Empacotando em domínios de falha ou atualização normalmente ocorre somente quando há várias falhas ou outra variação no sistema Olá impedindo posicionamento corretas. Se você quiser tooprevent remessa mesmo durante nessas situações, você pode utilizar Olá `RequireDomainDistribution` [política de posicionamento](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md#requiring-replica-distribution-and-disallowing-packing). Observe que isso pode afetar a disponibilidade e a confiabilidade do serviço como um efeito colateral, portanto, considere com cuidado.

Se o ambiente de saudação está configurado corretamente, todas as restrições são respeitadas totalmente, mesmo durante as atualizações. Olá chave é que o Gerenciador de recursos de Cluster está observando as restrições de saudação. Ao detectar uma violação que imediatamente reporta e tente toocorrect problema de saudação.

## <a name="hello-preferred-location-constraint"></a>restrição de local de saudação preferida
Olá PreferredLocation restrição é um pouco diferente, pois tem dois usos diferentes. Uma utilização dessa restrição ocorre durante as atualizações de aplicativo. Olá Gerenciador de recursos de Cluster gerencia automaticamente essa restrição durante as atualizações. Ele é usado tooensure que, quando atualizações forem concluídas que réplicas retornam tootheir locais inicias. Hello outros Olá PreferredLocation restrição é usado para de saudação [ `PreferredPrimaryDomain` política de posicionamento](service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies.md). Ambos são otimizações e, portanto, Olá PreferredLocation restrição é única restrição de saudação definida muito "Otimização" por padrão.

## <a name="upgrades"></a>Atualizações
Olá Gerenciador de recursos de Cluster também ajuda a durante a aplicativos e atualizações de cluster, durante o qual ele tem dois trabalhos:

* Certifique-se de que as regras de saudação do cluster de saudação não sejam comprometidas
* tente ir de atualização de saudação toohelp suave

### <a name="keep-enforcing-hello-rules"></a>Manter impor regras de saudação
Olá principal toobe atento é que regras hello – restrições estrito hello como restrições de posicionamento e as capacidades - ainda são impostas durante as atualizações. Restrições de posicionamento garantem que suas cargas de trabalho serão executadas apenas onde elas são permitidas, mesmo durante atualizações. Quando os serviços forem altamente restritos, as atualizações podem demorar mais. Ao serviço hello ou nó Olá estiver em execução é interrompido para uma atualização que pode haver algumas opções para onde ele pode ficar.

### <a name="smart-replacements"></a>Substituições inteligentes
Quando uma atualização é iniciada, Olá Gerenciador de recursos de tira um instantâneo de organização atual de saudação do cluster hello. Como cada domínio de atualização for concluído, ele tenta tooreturn Olá serviços na organização original tootheir domínio de atualização. Dessa forma há no máximo dois faz a transição para um serviço durante a atualização de saudação. Há uma movimentação fora do nó Olá afetado e um retroceder em. Retornar Olá toohow cluster ou serviço que estava antes da atualização Olá também garante a atualização de saudação não afeta o layout de saudação do cluster hello. 

### <a name="reduced-churn"></a>Variação reduzida
Outra coisa que ocorre durante as atualizações é que hello desativa o Gerenciador de recursos de Cluster de balanceamento. Impedindo balanceamento impede a atualização de toohello de reações desnecessário em si, como mover serviços para nós removidos para atualização de saudação. Se a atualização de saudação em questão for uma atualização de Cluster, cluster inteiro Olá não é equilibrado durante a atualização de saudação. Verificações de restrição ficam ativas, movimentação somente com base em Olá balanceamento proativo de métricas está desabilitada.

### <a name="buffered-capacity--upgrade"></a>Capacidade de buffer e atualização
Geralmente, você deseja toocomplete atualização Olá mesmo se o cluster Olá é restrita ou fechar toofull. Gerenciamento de capacidade de saudação do cluster Olá é ainda mais importante durante as atualizações que o usual. Dependendo da saudação número de domínios de atualização entre 5 e 20% da capacidade deve ser migrado como hello atualização passa por cluster hello. Se o trabalho tem toogo em algum lugar. Isso é onde Olá noção de [buffer capacidades](service-fabric-cluster-resource-manager-cluster-description.md#buffered-capacity) é útil. A capacidade de buffer é respeitada durante a operação normal. Olá Gerenciador de recursos de Cluster pode preencher nós tootheir a capacidade total (consumindo buffer Olá) durante as atualizações, se necessário.

## <a name="next-steps"></a>Próximas etapas
* Desde o início de saudação e [obter uma introdução toohello Gerenciador de recursos de Cluster do serviço de malha](service-fabric-cluster-resource-manager-introduction.md)
