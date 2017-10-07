---
title: "Descrição do recurso Gerenciador de Cluster de aaaCluster | Microsoft Docs"
description: "Que descreve um cluster do Service Fabric especificando domínios de falha, domínios de atualização, as propriedades de nó e as capacidades de nó para Olá Gerenciador de recursos de Cluster."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 55f8ab37-9399-4c9a-9e6c-d2d859de6766
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: f2822075976bd54402af5ad56991b5b360dfb1d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="describing-a-service-fabric-cluster"></a>Descrevendo um cluster do Service Fabric
Olá Gerenciador de recursos de Cluster do serviço de malha fornece vários mecanismos para descrever um cluster. Durante a execução, Olá Gerenciador de recursos de Cluster usa essa informações tooensure alta disponibilidade de serviços de saudação em execução no cluster de saudação. Ao impor essas regras importantes, ele também tenta toooptimize consumo de recursos de saudação em cluster hello.

## <a name="key-concepts"></a>Principais conceitos
Olá Gerenciador de recursos de Cluster dá suporte a vários recursos que descrevem um cluster:

* Domínios de falha
* Domínios de atualização
* Propriedades de nó
* Capacidades de nó

## <a name="fault-domains"></a>Domínios de falha
Um domínio de falha é qualquer área da falha coordenada. Um único computador é um domínio de falha (desde que ele pode falhar em seus próprio para vários motivos, de firmware NIC toobad de falhas toodrive de falhas fonte de energia). Computadores conectado toohello mesmo comutador Ethernet estão em Olá mesmo domínio de falha, como são computadores que compartilham uma única fonte de energia ou em um único local. Como é natural para toooverlap de falhas de hardware, os domínios de falha são inerentemente hierárquicos e são representados como URIs na malha do serviço.

É importante que domínios de falha são definidos corretamente como o Service Fabric usa os serviços de informações toosafely local. Serviço de malha não quer tooplace serviços, de forma que a perda de saudação de um domínio de falha (causado por falha de saudação de algum componente) faz com que um serviço toogo para baixo. Olá ambiente do Azure Service Fabric usa informações de domínio de falha de saudação fornecidas pelo Olá ambiente toocorrectly configure nós Olá cluster Olá em seu nome. Para Service Fabric autônomo, domínios de falha são definidas em tempo de saudação cluster hello está configurado 

> [!WARNING]
> É importante que as informações de domínio de falha de saudação fornecido tooService malha está correta. Por exemplo, digamos que nós do cluster do Service Fabric estejam em execução dentro de dez máquinas virtuais que são executadas em cinco hosts físicos. Nesse caso, mesmo que haja dez máquinas virtuais, há apenas cinco domínios de falha (de nível superior) diferentes. Compartilhamento Olá faz com que o mesmo host físico tooshare VMs Olá mesmo domínio de falha de raiz, pois Olá experiência de VMs coordenada falha se o host físico falhar.  
>
> Como a espera do Service Fabric Olá domínio de falha de um nó não toochange. Outros mecanismos de garantir a alta disponibilidade do hello VMs, como [HA VMs](https://technet.microsoft.com/en-us/library/cc967323.aspx), use a migração transparente de VMs de um host tooanother. Esses mecanismos não reconfigurar ou notificar Olá executando código dentro Olá VM. Sendo assim, eles **não têm suporte** como ambientes para executar clusters do Service Fabric. Malha do serviço deve ser tecnologia de alta disponibilidade só Olá empregada. Mecanismos como migração dinâmica de VMs e SANs, entre outros, não são necessários. Se usados em conjunto com o Service Fabric, esses mecanismos _reduzem_ a confiabilidade e a disponibilidade dos aplicativos, pois eles introduzem complexidade adicional, adicionam fontes de falha centralizadas e utilizam estratégias de disponibilidade e confiabilidade que entram em conflito com aquelas em vigor no Service Fabric. 
>
>

No gráfico de saudação abaixo é cores de todas as entidades de saudação que contribuem tooFault domínios e lista que todos os diferentes domínios de falha que resultam de hello. Neste exemplo, temos datacenters (“DC”), racks (“R”) e folhas (“B”). Em termos conceituais, se cada folha contém mais de uma máquina virtual, pode haver outra camada na hierarquia de domínio de falha de saudação.

<center>
![Nós organizados por meio de domínios de falha][Image1]
</center>

Durante a execução, Olá Gerenciador de recursos de Cluster do serviço de malha considera Olá domínios de falha no cluster hello e planos de layouts. Olá réplicas com monitoração de estado ou instâncias sem monitoração de estado de um serviço específico são distribuídas para que fiquem em domínios de falha separados. Distribuir o serviço de saudação em domínios de falha garante a disponibilidade de saudação do serviço de saudação não seja comprometida quando um domínio de falha falhar em qualquer nível da hierarquia de saudação.

Gerenciador de recursos de Cluster do Service Fabric não importa quantas camadas na hierarquia de domínio de falha de saudação. No entanto, ele tenta tooensure perda de saudação de qualquer parte de uma hierarquia Olá não afeta os serviços em execução. 

É melhor se houver Olá o mesmo número de nós em cada nível de profundidade na hierarquia de domínio de falha de saudação. Se hello "árvore" de domínios de falha está faltando em seu cluster, dificulta para Olá toofigure do Gerenciador de recursos de Cluster de limite de alocação de saudação recomendada dos serviços. Layouts de domínios de falha desequilibrados significam essa perda de saudação de alguns domínios disponibilidade de saudação do impacto de serviços mais do que outros domínios. Como resultado, Olá Gerenciador de recursos de Cluster é interrompida entre as duas metas: ele deseja máquinas de saudação toouse no domínio "pesada" colocando serviços neles e desejar tooplace serviços em outros domínios para que a perda de saudação de um domínio não causa problemas. 

Qual é a aparência de um domínio desequilibrado? No diagrama de saudação seguir, mostramos dois layouts de cluster diferente. No primeiro exemplo de hello, nós de saudação são distribuídos uniformemente por Olá domínios de falha. No segundo exemplo de hello, um domínio de falha tem mais nós do que Olá outros domínios de falha. 

<center>
![Dois layouts de cluster diferentes][Image2]
</center>

No Azure, a opção de saudação do qual o domínio de falha contém um nó é gerenciada por você. No entanto, dependendo do número de saudação de nós que você provisionar você ainda poderá acabar com domínios de falha com mais nós neles que outros. Por exemplo, digamos que você tem cinco domínios de falha no cluster Olá mas provisiona sete nós para um determinado tipo. Nesse caso, hello primeiro dois domínios de falha acabar com mais nós. Se você continuar toodeploy mais NodeTypes com apenas algumas instâncias, o problema de saudação é pior. Por esse motivo, que é recomendável que Olá o número de nós em cada tipo de nó é um múltiplo do número de saudação de domínios de falha.

## <a name="upgrade-domains"></a>Domínios de atualização
Domínios de atualização são outro recurso que ajuda a Olá Gerenciador de recursos de Cluster do serviço de malha entender o layout de saudação do cluster hello. Domínios de atualização definam conjuntos de nós que são atualizados ao Olá simultaneamente. Saudação de Ajuda do Gerenciador de recursos de Cluster de entender e coordenar operações de gerenciamento, como atualizações de domínios de atualização.

Os Domínios de Atualização são muito semelhantes aos Domínios de Falha, mas com algumas diferenças importantes. Primeiro, as áreas de falhas de hardware coordenadas definem os domínios de falha. Domínios de atualização, na Olá outro lado, são definidas pela política. Você obtém toodecide quantos desejar, em vez de ele seja ditada pelo ambiente de saudação. Você pode ter tantos domínios de atualização quantos forem o número de nós. Outra diferença entre domínios de falha e domínios de atualização é que os domínios de atualização não são hierárquicos. Em vez disso, eles são mais parecidos com uma marca simples. 

Olá diagrama a seguir mostra três que domínios de atualização são distribuídos em três domínios de falha. Ele também mostra um possível posicionamento para três réplicas diferentes de um serviço com estado, em que cada um fica em domínios de atualização e de falha diferentes. Esse posicionamento permite perda de saudação de um domínio de falha enquanto estiver no meio de saudação de uma atualização de serviço e ainda ter uma cópia de dados e código de saudação.  

<center>
![Posicionamento com domínios de falha e atualização][Image3]
</center>

Há vantagens e desvantagens toohaving grande número de domínios de atualização. Domínios de atualização mais significa que cada etapa de atualização de hello mais granular e, portanto, afeta um número menor de nós ou serviços. Como resultado, serviços menos tem toomove ao mesmo tempo, apresentando menos variação no sistema de saudação. Isso tende a tooimprove confiabilidade, desde que a menor do serviço de saudação é afetado por qualquer problema introduzido durante a atualização de saudação. Domínios de atualização mais também significa que você precisa de menos buffer disponível em outros impacto nós toohandle Olá Olá atualize. Por exemplo, se você tiver cinco domínios de atualização, nós de saudação em cada lidar com aproximadamente 20% do tráfego. Se você precisar tootake para baixo desse domínio de atualização para uma atualização, o que a carga geralmente precisa toogo em algum lugar. Como você tem quatro domínios de atualização restantes, cada um deve ter espaço para aproximadamente 5% do total de tráfego hello. Domínios de atualização mais significa que você precise de menos buffer em nós Olá cluster hello. Por exemplo, imagine que você tivesse 10 domínios de atualização. Nesse caso, cada UD apenas manipula cerca de 10% do total do tráfego de saudação. Quando uma atualização percorre cluster hello, cada domínio apenas necessário espaço toohave 1.1 cerca de % do total de tráfego hello. Domínios de atualização mais geralmente permitem toorun seus nós em maior utilização, desde que você precisa de capacidade menor reservada. Olá mesmo é verdadeiro para domínios de falha.  

desvantagem de saudação de ter vários domínios de atualização é que atualizações tendem tootake mais. Malha do serviço espera um curto período de tempo depois de um domínio de atualização é concluído e executa verificações antes de iniciar tooupgrade Olá próximo. Esses atrasos habilitar detectando problemas introduzidos pela atualização Olá antes Olá atualização continua. compensação de saudação é aceitável, porque evita que as alterações incorretas afetar muito do serviço de saudação de cada vez.

Ter um número muito reduzido de domínios de atualização tem muitos efeitos negativos – enquanto cada domínio de atualização individual fica inoperante e é atualizado, uma grande parte de sua capacidade geral fica indisponível. Por exemplo, se tiver apenas três domínios de atualização, você desativará cerca de um terço de sua capacidade geral de serviço ou de cluster de uma vez. Ter grande parte do seu serviço para baixo de uma vez não é desejável, desde que você tem capacidade suficiente toohave restante de saudação da sua carga de trabalho do cluster toohandle hello. Manter esse buffer significa que, durante a operação normal, esses nós ficam menos carregados do que ficariam em caso contrário. Isso aumenta o custo de saudação da execução do seu serviço.

Não há nenhum limite real toohello número total de falhas ou domínios de atualização em um ambiente ou restrições em como eles se sobrepõem. Dito isso, há vários padrões comuns:

- Domínios de falha e domínios de atualização mapeados 1:1
- Um domínio de atualização por nó (instância de sistema operacional física ou virtual)
- Um modelo de "distribuído" ou "matriz" onde Olá domínios de falha e domínios de atualização formam uma matriz com máquinas geralmente executar diagonais Olá

<center>
![Layouts de domínios de falha e de atualização][Image4]
</center>

Não há que nenhum melhor responder qual toochoose de layout, cada um tem algumas vantagens e desvantagens. Por exemplo, o modelo de 1FD:1UD de saudação é simple tooset backup. Olá, domínio de atualização 1 por modelo de nó é mais parecida com o que as pessoas são usadas para. Durante atualizações, cada nó é atualizado de forma independente. Isso é semelhante toohow pequenos conjuntos de máquinas foram atualizados manualmente no hello anterior. 

modelo mais comum de saudação é matriz Olá FD/UD onde hello FDs e UDs formam uma tabela e nós são colocados ao longo Olá diagonal. Este é o modelo de saudação usado por padrão em clusters de malha do serviço no Azure. Para clusters com vários nós, tudo o que acaba parecida Olá matriz densa padrão acima.

## <a name="fault-and-upgrade-domain-constraints-and-resulting-behavior"></a>Restrições de domínio de falha e de atualização e o comportamento resultante
Olá Gerenciador de recursos do Cluster trata desejo Olá tookeep um serviço balanceado em domínios de falha e atualização como uma restrição. Você pode encontrar mais informações sobre restrições [neste artigo](service-fabric-cluster-resource-manager-management-integration.md). Olá estado de restrições de falha e atualização do domínio: "para uma partição de determinado serviço nunca deverá haver uma diferença *maior do que um* no número de saudação de objetos de serviço (instâncias de serviço sem monitoração de estado ou réplicas com monitoração de estado do serviço) entre dois domínios." Isso impede determinados movimentos ou disposições que violam essa restrição.

Vejamos um exemplo. Digamos que temos um cluster com seis nós, configurados com cinco domínios de falha e cinco domínios de atualização.

|  | FD0 | FD1 | FD2 | FD3 | FD4 |
| --- |:---:|:---:|:---:|:---:|:---:|
| **UD0** |N1 | | | | |
| **UD1** |N6 |N2 | | | |
| **UD2** | | |N3 | | |
| **UD3** | | | |N4 | |
| **UD4** | | | | |N5 |

Agora, digamos que nós criemos um serviço com um TargetReplicaSetSize (ou, para um serviço sem estado, um InstanceCount) igual a cinco. réplicas Olá parar em N1 N5. Na verdade, N6 nunca será usado, independentemente de quantos serviços como este você criar. Mas por quê? Vamos examinar a diferença de saudação entre layout atual hello e o que aconteceria se N6 for escolhida.

Aqui está o layout de saudação nós temos e Olá número total de réplicas por falha e atualização do domínio:

|  | FD0 | FD1 | FD2 | FD3 | FD4 | UDTotal |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| **UD0** |R1 | | | | |1 |
| **UD1** | |R2 | | | |1 |
| **UD2** | | |R3 | | |1 |
| **UD3** | | | |R4 | |1 |
| **UD4** | | | | |R5 |1 |
| **FDTotal** |1 |1 |1 |1 |1 |- |

Este layout é balanceado em termos de nós por domínio de falha e domínio de atualização. Ele também é equilibrado em termos de número de saudação de réplicas por falha e atualização do domínio. Cada domínio tem Olá o mesmo número de nós e Olá o mesmo número de réplicas.

Agora, vamos ver o que aconteceria se tivéssemos usado N6 em vez de N2. Como seriam réplicas Olá ser distribuídas em seguida?

|  | FD0 | FD1 | FD2 | FD3 | FD4 | UDTotal |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| **UD0** |R1 | | | | |1 |
| **UD1** |R5 | | | | |1 |
| **UD2** | | |R2 | | |1 |
| **UD3** | | | |R3 | |1 |
| **UD4** | | | | |R4 |1 |
| **FDTotal** |2 |0 |1 |1 |1 |- |

Esse layout viola a nossa definição de restrição de domínio de falha de saudação. FD0 tem duas réplicas, enquanto FD1 tem zero, fazer diferença Olá entre FD0 e FD1 um total de dois. Olá Gerenciador de recursos de Cluster não permite essa organização. Da mesma forma, se escolhêssemos N2 e N6 (em vez de N1 e N2), teríamos:

|  | FD0 | FD1 | FD2 | FD3 | FD4 | UDTotal |
| --- |:---:|:---:|:---:|:---:|:---:|:---:|
| **UD0** | | | | | |0 |
| **UD1** |R5 |R1 | | | |2 |
| **UD2** | | |R2 | | |1 |
| **UD3** | | | |R3 | |1 |
| **UD4** | | | | |R4 |1 |
| **FDTotal** |1 |1 |1 |1 |1 |- |

Este layout é equilibrado em termos de domínios de falha. No entanto, agora ele está violando restrição de domínio de atualização de saudação. Isso acontece porque UD0 tem zero réplicas, enquanto UD1 tem cinco. Portanto, este layout também é inválido e não ser separado por Olá Gerenciador de recursos de Cluster. 

## <a name="configuring-fault-and-upgrade-domains"></a>Configurando domínios de falha e atualização
A definição de domínios de falha e domínios de atualização é feita automaticamente em implantações hospedadas do Azure Service Fabric. Service Fabric seleciona e usa as informações de ambiente de saudação do Azure.

Se você estiver criando seu próprio cluster (ou toorun uma topologia específica em desenvolvimento), você pode fornecer informações de domínio de falha e atualização do domínio Olá por conta própria. Neste exemplo, definimos um cluster de desenvolvimento local de nove nós que abrange três "datacenters" (cada um com três racks). Este cluster também tem três domínios de atualização distribuídos entre esses três datacenters. Um exemplo de configuração de saudação está abaixo: 

ClusterManifest.xml

```xml
  <Infrastructure>
    <!-- IsScaleMin indicates that this cluster runs on one-box /one single server -->
    <WindowsServer IsScaleMin="true">
      <NodeList>
        <Node NodeName="Node01" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType01" FaultDomain="fd:/DC01/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node02" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType02" FaultDomain="fd:/DC01/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node03" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType03" FaultDomain="fd:/DC01/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
        <Node NodeName="Node04" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType04" FaultDomain="fd:/DC02/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node05" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType05" FaultDomain="fd:/DC02/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node06" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType06" FaultDomain="fd:/DC02/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
        <Node NodeName="Node07" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType07" FaultDomain="fd:/DC03/Rack01" UpgradeDomain="UpgradeDomain1" IsSeedNode="true" />
        <Node NodeName="Node08" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType08" FaultDomain="fd:/DC03/Rack02" UpgradeDomain="UpgradeDomain2" IsSeedNode="true" />
        <Node NodeName="Node09" IPAddressOrFQDN="localhost" NodeTypeRef="NodeType09" FaultDomain="fd:/DC03/Rack03" UpgradeDomain="UpgradeDomain3" IsSeedNode="true" />
      </NodeList>
    </WindowsServer>
  </Infrastructure>
```

por meio de ClusterConfig.json para implantações autônomas

```json
"nodes": [
  {
    "nodeName": "vm1",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm2",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm3",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc1/r0",
    "upgradeDomain": "UD3"
  },
  {
    "nodeName": "vm4",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm5",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm6",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc2/r0",
    "upgradeDomain": "UD3"
  },
  {
    "nodeName": "vm7",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD1"
  },
  {
    "nodeName": "vm8",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD2"
  },
  {
    "nodeName": "vm9",
    "iPAddress": "localhost",
    "nodeTypeRef": "NodeType0",
    "faultDomain": "fd:/dc3/r0",
    "upgradeDomain": "UD3"
  }
],
```

> [!NOTE]
> Ao definir clusters por meio do Azure Resource Manager, domínios de falha e domínios de atualização são atribuídos pelo Azure. Portanto, a definição de saudação de seus tipos de nós e os conjuntos de escala de máquina Virtual no modelo do Azure Resource Manager não incluir informações de atualização do domínio ou domínio de falha.
>

## <a name="node-properties-and-placement-constraints"></a>Restrições de posicionamento e propriedades do nó
Às vezes (na verdade, a maioria do tempo de saudação), você vai tooensure toowant determinadas cargas de trabalho executados somente em determinados tipos de nós no cluster de saudação. Por exemplo, algumas cargas de trabalho podem exigir GPUs ou SSDs, enquanto outras, não. Um ótimo exemplo de direcionamento de cargas de trabalho do hardware tooparticular é quase todos os arquitetura de n camadas lá. Alguns computadores servem como Olá front-end ou a API que atende ao lado do aplicativo hello e são expostos toohello clientes ou Olá internet. Diferentes máquinas, geralmente com recursos de hardware diferente, tratar o trabalho de saudação de camadas de computação ou armazenamento hello. Esses são normalmente _não_ diretamente expostos tooclients ou Olá da internet. Serviço de malha espera que há casos em que as cargas de trabalho específicas necessário toorun em configurações de hardware específica. Por exemplo:

* um aplicativo de n camadas existente foi "transferido e posicionado" em um ambiente do Service Fabric
* uma carga de trabalho quer toorun em hardware específico por motivos de isolamento de segurança, de desempenho ou de escala
* Uma carga de trabalho deve ser isolada de outras cargas de trabalho por motivos de política ou consumo de recursos

Esses tipos de configurações, de toosupport serviço malha tem uma noção de primeira classe marcas que podem ser aplicadas toonodes. Essas marcas são chamadas de **propriedades de nó**. **Restrições de posicionamento** são instruções Olá anexado tooindividual serviços selecionados para uma ou mais propriedades de nó. Restrições de posicionamento definem onde os serviços devem ser executados. conjunto de saudação de restrições é extensível - qualquer par chave/valor pode funcionar. 

<center>
![Cargas de trabalho diferentes do layout do cluster][Image5]
</center>

### <a name="built-in-node-properties"></a>Propriedades de nó internas
Malha do serviço define algumas propriedades de nó padrão que podem ser usadas, automaticamente, sem ter que toodefine do usuário Olá-los. Propriedades de padrão de saudação definidas em cada nó são Olá **NodeType** e hello **NodeName**. Por exemplo, você poderia escrever uma restrição de posicionamento como `"(NodeType == NodeType03)"`. Geralmente encontramos NodeType toobe uma das propriedades hello mais comumente usada. Ela é útil porque corresponde individualmente a um tipo de um computador. Cada tipo de computador corresponde tooa tipo de carga de trabalho em um aplicativo de n camadas tradicional.

<center>
![Restrições de posicionamento e propriedades do nó][Image6]
</center>

## <a name="placement-constraint-and-node-property-syntax"></a>Sintaxe de restrição de posicionamento e propriedades do nó 
valor de saudação especificado na propriedade do nó Olá pode ser uma cadeia de caracteres, bool, ou assinado longa. instrução Olá no serviço de saudação é chamada um posicionamento *restrição* desde que ela restringe onde Olá serviço pode ser executado no cluster de saudação. restrição de saudação pode ser qualquer instrução Boolean que opera em Propriedades de nó diferente de saudação em cluster hello. seletores de válido Olá nessas instruções boolean são:

1) verificações condicionais para a criação de instruções

| Instrução | Sintaxe |
| --- |:---:|
| "igual a" | "==" |
| "diferente de" | "!=" |
| "maior que" | ">" |
| "maior ou igual a" | ">=" |
| "menor que" | "<" |
| "menor ou igual a" | "<=" |

2) instruções boolianas para operações de agrupamento e lógicas

| Instrução | Sintaxe |
| --- |:---:|
| "e" | "&&" |
| "ou" | "&#124;&#124;" |
| "não" | "!" |
| "agrupar como instrução única" | "()" |

Aqui estão alguns exemplos de instruções de restrição básicas.

  * `"Value >= 5"`
  * `"NodeColor != green"`
  * `"((OneProperty < 100) || ((AnotherProperty == false) && (OneProperty >= 100)))"`

Apenas nós onde hello geral instrução de restrição de posicionamento avalia muito "True" podem ter serviço Olá colocado nela. Os nós que não têm uma propriedade definida não correspondem a nenhuma restrição de posicionamento que contém essa propriedade.

Digamos que Olá nó propriedades foram definidas para um tipo de nó a seguir:

ClusterManifest.xml

```xml
    <NodeType Name="NodeType01">
      <PlacementProperties>
        <Property Name="HasSSD" Value="true"/>
        <Property Name="NodeColor" Value="green"/>
        <Property Name="SomeProperty" Value="5"/>
      </PlacementProperties>
    </NodeType>
```

via ClusterConfig.json para implantações Autônomas ou Template.json para clusters hospedados pelo Azure. 

> [!NOTE]
> No nó do Azure Resource Manager modelo Olá tipo geralmente é parametrizado. Ele seria semelhante a "[parameters('vmNodeType1Name')]", em vez de "NodeType01".
>

```json
"nodeTypes": [
    {
        "name": "NodeType01",
        "placementProperties": {
            "HasSSD": "true",
            "NodeColor": "green",
            "SomeProperty": "5"
        },
    }
],
```

Você pode criar *restrições* de posicionamento de serviço para um serviço da seguinte forma:

C#

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
serviceDescription.PlacementConstraints = "(HasSSD == true && SomeProperty >= 4)";
// add other required servicedescription fields
//...
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

Powershell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceType -Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementConstraint "HasSSD == true && SomeProperty >= 4"
```

Se todos os nós do NodeType01 forem válidos, você também pode selecionar esse tipo de nó com restrição Olá "(NodeType == NodeType01)".

Uma das coisas legais que Olá sobre restrições de posicionamento do serviço é que eles podem ser atualizados dinamicamente em tempo de execução. Então se você precisar, você pode mover um serviço em cluster hello, adicionar e remover requisitos, etc. Serviço de malha cuida de assegurar que o serviço de saudação permanece e disponível mesmo quando esses tipos de alterações são feitos.

C#:

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.PlacementConstraints = "NodeType == NodeType01";
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/app/service"), updateDescription);
```

Powershell:

```posh
Update-ServiceFabricService -Stateful -ServiceName $serviceName -PlacementConstraints "NodeType == NodeType01"
```

Restrições de posicionamento são especificadas para cada instância de serviço nomeada diferente. Atualizações sempre substituir saudação (substituir) que foi especificado anteriormente.

definição de cluster Olá define propriedades de saudação em um nó. Alterar as propriedades de um nó requer uma atualização de configuração do cluster. Atualizar propriedades do nó requer tooreport de toorestart cada nó afetado suas propriedades de novo. Essas atualizações sem interrupção são gerenciadas pelo Service Fabric.

## <a name="describing-and-managing-cluster-resources"></a>Descrever e gerenciar Recursos de Cluster
Um dos mais importantes de trabalhos de qualquer orchestrator é toohelp de saudação gerenciar o consumo de recursos em cluster hello. Gerenciar recursos de cluster pode significar algumas coisas diferentes. Primeiro, é necessário garantir que os computadores não sejam sobrecarregados. Isso significa garantir que eles não executem mais serviços do que conseguem tratar. Em segundo lugar, há balanceamento e otimização que é crítico toorunning serviços com eficiência. Custo efetivo ou desempenho confidenciais serviços não podem permitir toobe alguns nós hot enquanto outras são frios. Nós hot levam tooresource contenção e baixo desempenho e nós frios representam desperdiçada de recursos e aumento dos custos. 

O Service Fabric representa recursos como `Metrics`. Métricas são qualquer recurso lógico ou físico que você deseja toodescribe tooService malha. Exemplos de métricas são itens como "WorkQueueDepth" ou "MemoryInMb". Para obter informações sobre recursos físicos de saudação que controlam a malha do serviço em nós, consulte [governança de recursos](service-fabric-resource-governance.md). Para obter informações sobre como configurar métricas personalizadas e seus usos, consulte [este artigo](service-fabric-cluster-resource-manager-metrics.md)

As métricas são diferentes das restrições de posicionamento e das propriedades de nó. Propriedades de nó são descritores estáticos de nós Olá propriamente ditos. As métricas descrevem os recursos que os nós têm e que os serviços consomem quando são executados em um nó. Uma propriedade do nó poderia ser "HasSSD" e pode ser definida tootrue ou false. quantidade de saudação de espaço disponível em que SSD e a quantidade é consumida pelos serviços seria uma métrica como "DriveSpaceInMb". 

É importante toonote que assim como para restrições de posicionamento e as propriedades de nó, Olá Gerenciador de recursos de Cluster do serviço de malha não entende quais nomes de saudação da média de métricas de saudação. Os nomes de métrica são apenas cadeias de caracteres. É unidades de toodeclare uma boa prática como parte de nomes de métrica Olá criado quando é ambíguo.

## <a name="capacity"></a>Capacity
Se você desativasse todo o *balanceamento* de recursos, o Gerenciador de Recursos de Cluster do Service Fabric ainda garantiria que nenhum nó ficasse acima de sua capacidade. É possível saturações de capacidade de gerenciamento, a menos que o cluster de hello está muito cheio ou carga de trabalho de saudação é maior do que qualquer nó. A capacidade é outro *restrição* que Olá Gerenciador de recursos de Cluster usa toounderstand como quanto de um recurso de um nó. Capacidade restante também é controlada para cluster hello como um todo. Capacidade de saudação e consumo de saudação no nível de serviço de saudação são expressos em termos de métricas. Por exemplo, a métrica de saudação pode ser "ClientConnections" e um nó pode ter a capacidade para "ClientConnections" de 32768. Outros nós podem ter outros limites de algum serviço em execução em que possa nó significa que ele está consumindo atualmente 32256 da métrica hello "ClientConnections".

Durante a execução, Olá Gerenciador de recursos de Cluster controla a capacidade restante no cluster hello e em nós. Em ordem tootrack Olá capacidade Gerenciador de recursos de Cluster subtrai o uso de cada serviço de capacidade do nó onde Olá serviço é executado. Com essas informações, Olá Gerenciador de recursos de Cluster do serviço de malha pode decidir onde tooplace ou mover réplicas para que nós não passam pela capacidade.

<center>
![Capacidade e nós de cluster][Image7]
</center>

C#:

```csharp
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
ServiceLoadMetricDescription metric = new ServiceLoadMetricDescription();
metric.Name = "ClientConnections";
metric.PrimaryDefaultLoad = 1024;
metric.SecondaryDefaultLoad = 0;
metric.Weight = ServiceLoadMetricWeight.High;
serviceDescription.Metrics.Add(metric);
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

Powershell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton –Metric @("ClientConnections,High,1024,0)
```

Você pode ver as capacidades definidas no manifesto do cluster Olá:

ClusterManifest.xml

```xml
    <NodeType Name="NodeType03">
      <Capacities>
        <Capacity Name="ClientConnections" Value="65536"/>
      </Capacities>
    </NodeType>
```

via ClusterConfig.json para implantações Autônomas ou Template.json para clusters hospedados pelo Azure. 

```json
"nodeTypes": [
    {
        "name": "NodeType03",
        "capacities": {
            "ClientConnections": "65536",
        }
    }
],
```

Normalmente, a carga de um serviço é alterada dinamicamente. Digamos que a carga da réplica de "ClientConnections" alterado de 1024 too2048, mas o nó Olá ele estava em execução no e tinha apenas a capacidade restante de métrica de 512. Agora essa réplica ou posicionamento da instância é inválido, pois não há espaço suficiente no nó. Olá Gerenciador de recursos de Cluster tem tookick no e obter nó Olá abaixo de capacidade. Ela reduz a carga no nó de saudação que está acima da capacidade, movendo um ou mais réplicas de saudação ou instâncias de nós de tooother esse nó. Ao mover réplicas, Olá Gerenciador de recursos de Cluster tenta toominimize custo Olá essas movimentações. O custo de movimento é abordado em [neste artigo](service-fabric-cluster-resource-manager-movement-cost.md) e mais sobre Olá Gerenciador de recursos de Cluster do rebalanceamento estratégias e regras é descrito [aqui](service-fabric-cluster-resource-manager-metrics.md).

## <a name="cluster-capacity"></a>Capacidade do cluster
Como hello geral do Gerenciador de recursos de Cluster do Service Fabric manter Olá cluster sejam muito cheio? Bem, com a carga dinâmica, não há muito que ele possa fazer. Serviços podem ter o pico de carga independentemente das ações tomadas pelo Olá Gerenciador de recursos de Cluster. Como resultado, o cluster com bastante reserva dinâmica hoje pode não ter espaço suficiente quando você ficar famoso amanhã. Dito isso, há alguns controles que são baked tooprevent problemas. primeira coisa Olá que podemos fazer é impedir a criação de saudação de novas cargas de trabalho que levariam Olá cluster toobecome completo.

Digamos que você crie um serviço sem estado e que haja alguma carga associada a ele. Digamos que o serviço de saudação se preocupa com métrica de "DiskSpaceInMb" hello. Digamos que também que é contínuo tooconsume cinco unidades do "DiskSpaceInMb" para cada instância do serviço de saudação. Você deseja toocreate três instâncias do serviço de saudação. Ótimo! Para que significa que precisamos 15 unidades de "DiskSpaceInMb" toobe apresenta em cluster para que possamos Olá tooeven ser capaz de toocreate essas instâncias de serviço. Olá Gerenciador de recursos de Cluster continuamente calcula capacidade hello e consumo de cada métrica para que ele possa determinar capacidade restante de saudação em cluster hello. Se não houver espaço suficiente, Olá Olá do Gerenciador de recursos de Cluster rejeita criar chamada de serviço.

Desde que o requisito Olá existe somente que ser 15 unidades disponíveis, esse espaço pôde ser alocado muitas maneiras diferentes. Por exemplo, poderia haver uma unidade restante de capacidade em 15 nós diferentes ou três unidades restantes de capacidade em cinco nós diferente. Se Olá Gerenciador de recursos de Cluster pode reorganizar coisas, portanto, há cinco unidades disponíveis em três nós, coloca o serviço de saudação. Cluster de saudação reorganizando é geralmente possível, a menos que o cluster hello está quase cheio ou os serviços existentes Olá não podem ser consolidados por algum motivo.

## <a name="buffered-capacity"></a>Capacidade de buffer
Capacidade de buffer é outro recurso de saudação Gerenciador de recursos de Cluster. Ele permite que a reserva de alguma parte do hello capacidade total do nó. Esse buffer de capacidade é serviços tooplace usado somente durante falhas de nó e as atualizações. A capacidade em buffer é especificada globalmente por métrica para todos os nós. valor de saudação que você escolher para a capacidade de saudação reservada é uma função do número de saudação de domínios de falha e atualização ter no cluster hello. Mais domínios de falha e de atualização significa que você pode escolher um número menor para a capacidade em buffer. Se você tiver mais de domínios, você pode esperar pequenas quantidades de toobe seu cluster não está disponível durante falhas e as atualizações. Especificação de capacidade em buffer só faz sentido, se você também tiver capacidade do nó Olá especificado para uma métrica.

Aqui está um exemplo de como toospecify buffer capacidade:

ClusterManifest.xml

```xml
        <Section Name="NodeBufferPercentage">
            <Parameter Name="SomeMetric" Value="0.15" />
            <Parameter Name="SomeOtherMetric" Value="0.20" />
        </Section>
```

via ClusterConfig.json para implantações Autônomas ou Template.json para clusters hospedados pelo Azure:

```json
"fabricSettings": [
  {
    "name": "NodeBufferPercentage",
    "parameters": [
      {
          "name": "SomeMetric",
          "value": "0.15"
      },
      {
          "name": "SomeOtherMetric",
          "value": "0.20"
      }
    ]
  }
]
```

a criação de novos serviços Olá falha quando cluster Olá fora da capacidade de buffer de uma métrica. Impedindo a criação de saudação do buffer de saudação do novo serviços toopreserve garante que atualizações e falhas não causam nós toogo acima da capacidade. A capacidade em buffer é opcional, mas é recomendada em qualquer cluster que define uma capacidade para uma métrica.

Olá Gerenciador de recursos de Cluster expõe essas informações de carga. Para cada métrica, as informações incluem: 
  - Olá em buffer as definições de capacidade
  - capacidade total Olá
  - consumo atual Olá
  - se cada métrica é considerada balanceada ou não
  - estatísticas sobre o desvio padrão de saudação
  - nós de saudação que têm hello mais e menos carga  
  
Abaixo, vemos um exemplo dessa saída:

```posh
PS C:\Users\user> Get-ServiceFabricClusterLoadInformation
LastBalancingStartTimeUtc : 9/1/2016 12:54:59 AM
LastBalancingEndTimeUtc   : 9/1/2016 12:54:59 AM
LoadMetricInformation     :
                            LoadMetricName        : Metric1
                            IsBalancedBefore      : False
                            IsBalancedAfter       : False
                            DeviationBefore       : 0.192450089729875
                            DeviationAfter        : 0.192450089729875
                            BalancingThreshold    : 1
                            Action                : NoActionNeeded
                            ActivityThreshold     : 0
                            ClusterCapacity       : 189
                            ClusterLoad           : 45
                            ClusterRemainingCapacity : 144
                            NodeBufferPercentage  : 10
                            ClusterBufferedCapacity : 170
                            ClusterRemainingBufferedCapacity : 125
                            ClusterCapacityViolation : False
                            MinNodeLoadValue      : 0
                            MinNodeLoadNodeId     : 3ea71e8e01f4b0999b121abcbf27d74d
                            MaxNodeLoadValue      : 15
                            MaxNodeLoadNodeId     : 2cc648b6770be1bc9824fa995d5b68b1
```

## <a name="next-steps"></a>Próximas etapas
* Para obter informações sobre o fluxo de informações e arquitetura de hello dentro Olá Gerenciador de recursos de Cluster, check-out [neste artigo](service-fabric-cluster-resource-manager-architecture.md)
* Definir métricas de desfragmentação é carga tooconsolidate unidirecional em nós em vez de propagação de. toolearn como tooconfigure desfragmentação, consulte muito[neste artigo](service-fabric-cluster-resource-manager-defragmentation-metrics.md)
* Desde o início de saudação e [obter uma introdução toohello Gerenciador de recursos de Cluster do serviço de malha](service-fabric-cluster-resource-manager-introduction.md)
* toofind out sobre como Olá Gerenciador de recursos de Cluster gerencia e equilibra a carga no cluster hello, check-out artigo Olá em [balanceamento de carga](service-fabric-cluster-resource-manager-balancing.md)

[Image1]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-domains.png
[Image2]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-uneven-fault-domain-layout.png
[Image3]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-and-upgrade-domains-with-placement.png
[Image4]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-fault-and-upgrade-domain-layout-strategies.png
[Image5]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-layout-different-workloads.png
[Image6]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-placement-constraints-node-properties.png
[Image7]:./media/service-fabric-cluster-resource-manager-cluster-description/cluster-nodes-and-capacity.png
