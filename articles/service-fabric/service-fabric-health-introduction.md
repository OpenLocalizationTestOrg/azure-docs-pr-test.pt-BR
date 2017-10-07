---
title: "monitoramento de aaaHealth na malha do serviço | Microsoft Docs"
description: "Uma introdução toohello Azure Service Fabric monitoramento de integridade modelo, que fornece o monitoramento do cluster hello e seus aplicativos e serviços."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 1d979210-b1eb-4022-be24-799fd9d8e003
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: oanapl
ms.openlocfilehash: 904f36374ca6ca7e4caa1d43c92584e7e4c50087
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooservice-fabric-health-monitoring"></a>Monitoramento da integridade de malha do tooService de Introdução
O Service Fabric do Azure introduz um modelo de integridade que fornece avaliação e relatório de integridade avançados, flexíveis e extensíveis. modelo de saudação permite o monitoramento de quase em tempo real do estado de saudação do cluster hello e serviços de saudação em execução. Você pode obter as informações sobre integridade facilmente e corrigir possíveis problemas antes que eles se espalhem e causem interrupções massivas. No modelo típico de Olá, serviços de enviar relatórios com base em suas exibições locais e que informações são agregadas tooprovide uma visão geral do nível de cluster.

Componentes do Service Fabric usam esta tooreport do modelo de integridade avançados seu estado atual. Você pode usar Olá mesmo integridade tooreport de mecanismo de seus aplicativos. Se investir em relatórios de integridade de alta qualidade que capturam suas condições personalizadas, você poderá detectar e corrigir problemas do seu aplicativo em execução com muito mais facilidade.

Olá que seguintes Microsoft Virtual Academy vídeo também descreve o modelo de integridade de malha do serviço hello e como ele é usado:<center><a target="_blank" href="https://mva.microsoft.com/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tevZw56yC_1906218965">
<img src="./media/service-fabric-health-introduction/HealthIntroVid.png" WIDTH="360" HEIGHT="244">
</a></center>

> [!NOTE]
> Começamos Olá integridade subsistema tooaddress a necessidade de atualizações monitoradas. Serviço de malha fornece monitoradas atualizações do aplicativo e o cluster de garantir a disponibilidade total, sem tempo de inatividade e toono mínima intervenção do usuário. tooachieve essas metas, a atualização de saudação verifica a integridade com base em configurado políticas de atualização. Uma atualização pode continuar somente quando a integridade respeita os limites desejados. Caso contrário, a atualização de saudação é seja revertida automaticamente ou pausado administradores toogive problemas de saudação de toofix uma chance. toolearn mais sobre atualizações de aplicativo, consulte [neste artigo](service-fabric-application-upgrade.md).
> 
> 

## <a name="health-store"></a>Repositório de Integridade
o repositório de integridade de Olá mantém relacionados à integridade informações sobre as entidades no cluster Olá para fácil recuperação e avaliação. Ele é implementado como um serviço de malha persistentes com monitoração de estado do serviço tooensure alta disponibilidade e escalabilidade. repositório de integridade Hello faz parte da saudação **fabric: / sistema** aplicativo e está disponível quando o cluster hello está ativo e em execução.

## <a name="health-entities-and-hierarchy"></a>Hierarquia e entidades de integridade
entidades de integridade de saudação são organizadas em uma hierarquia lógica que captura as interações e as dependências entre entidades diferentes. repositório de integridade Olá cria automaticamente a entidades de integridade e a hierarquia com base em relatórios recebidos de componentes da malha do serviço.

entidades de integridade Olá espelham entidades do Service Fabric hello. (Por exemplo, **entidade de aplicativo de integridade** corresponde a uma instância do aplicativo implantado em cluster hello, enquanto **entidade do nó de integridade** corresponde a um nó de cluster de malha do serviço.) a captura de hierarquia de integridade de saudação interações de saudação de entidades do sistema Olá e é a base de Olá para avaliação de integridade avançadas. Você pode aprender sobre os principais conceitos do Service Fabric em [Visão geral técnica do Service Fabric](service-fabric-technical-overview.md). Para saber mais sobre aplicativos, confira [Modelo de aplicativo do Service Fabric](service-fabric-application-model.md).

hierarquia e entidades de integridade Olá permitem Olá toobe de cluster e aplicativos efetivamente informado, depurado e monitorados. modelo de integridade Olá fornece um precisas *granular* representação de integridade de saudação do hello muitas partes móveis no cluster hello.

![Entidades de integridade.][1]
entidades de integridade Hello, organizadas em uma hierarquia com base nas relações pai-filho.

[1]: ./media/service-fabric-health-introduction/servicefabric-health-hierarchy.png

entidades de integridade de saudação são:

* **Cluster**. Representa a integridade de saudação de um cluster do Service Fabric. Relatórios de integridade do cluster descrevem as condições que afetam o cluster inteiro hello. Essas condições afetam várias entidades em cluster hello ou Olá em si. Com base na condição de Olá, Relator Olá não é possível restringir o problema Olá tooone ou mais filhos não íntegros. Os exemplos incluem cérebro de saudação do cluster Olá divisão devido a problemas de comunicação ou particionamento toonetwork.
* **Nó**. Representa a integridade de saudação de um nó de malha do serviço. Relatórios de integridade do nó descrevem as condições que afetam a funcionalidade de nó de saudação. Normalmente, eles afetam todas as entidades de saudação implantada em execução. Os exemplos incluem um nó sem espaço em disco (ou outras propriedades em todo o computador, como memória, conexões) ou quando o nó está desativado. entidade do nó de saudação é identificada pelo nome de nó da saudação (string).
* **Aplicativo**. Representa a integridade de saudação de uma instância de aplicativo em execução no cluster de saudação. Relatórios de integridade do aplicativo descrevem as condições que afetam o hello a integridade geral do aplicativo hello. Eles não podem ser reduzidos tooindividual filhos (serviços ou aplicativos implantados). Exemplos incluem a interação de ponta a ponta de saudação entre os diferentes serviços em um aplicativo hello. entidade de aplicativo Hello é identificada pelo nome do aplicativo hello (URI).
* **Serviço**. Representa a integridade de saudação de um serviço em execução no cluster de saudação. Relatórios de integridade do serviço descrevem as condições que afetam o hello a integridade geral do serviço de saudação. não é possível restringir Relator Olá partição não íntegro do hello problema tooan ou réplica. Os exemplos incluem uma configuração de serviço (como compartilhamento de arquivos externos ou porta) que está causando problemas em todas as partições. entidade de serviço Olá é identificada pelo nome do serviço de saudação (URI).
* **Partição**. Representa a integridade de saudação de uma partição de serviço. Relatórios de integridade da partição descrevem as condições que afetam o conjunto de réplica inteira hello. Exemplos incluem quando o número de saudação de réplicas está abaixo da contagem de destino e quando uma partição está em perda de quorum. entidade de partição Olá é identificada por partição Olá ID (GUID).
* **Réplica**. Representa a integridade de saudação de uma réplica de serviço com monitoração de estado ou uma instância de serviço sem monitoração de estado. réplica de saudação é Olá menor unidade watchdogs e componentes do sistema podem relatar para um aplicativo. Para os serviços com monitoração de estado, os exemplos incluem uma réplica primária que não é possível replicar operações toosecondaries e replicação lenta. Além disso, uma instância sem estado pode relatar quando estiver em execução sem recursos ou tiver problemas de conectividade. entidade de réplica Olá é identificada pelo Olá ID (GUID) e hello réplica ou instância de ID de partição (longo).
* **DeployedApplication**. Olá representa a integridade de um *aplicativo em execução em um nó*. Relatórios de integridade do aplicativo implantado descrevem o aplicativo de toohello específico de condições no nó de saudação que não pode ser reduzida tooservice pacotes implantados em Olá mesmo nó. Exemplos incluem erros quando o pacote de aplicativo não pode ser baixado no nó e problemas de configuração de entidades de segurança do aplicativo no nó de saudação. aplicativo Hello implantado é identificado pelo nome do aplicativo (URI) e o nome do nó (string).
* **DeployedServicePackage**. Representa a integridade de saudação de um pacote de serviço em execução em um nó de cluster de saudação. Ele descreve o pacote de serviço tooa específico de condições que não afetam a saudação outros pacotes de serviço em Olá mesmo nó para Olá mesmo aplicativo. Exemplos incluem um pacote de código no pacote de serviço de saudação que não pode ser iniciado e um pacote de configuração não pode ser lido. pacote de serviço Olá implantado é identificado pelo nome do aplicativo (URI), nome do nó (string), o nome manifesto do serviço (string) e ID de ativação de pacote de serviço (string).

granularidade de saudação do modelo de integridade Olá torna fácil toodetect e corrigir problemas. Por exemplo, se um serviço não está respondendo, é possível tooreport que Olá a instância do aplicativo não está íntegro. Emissão de relatórios que nível não é ideal, no entanto, porque o problema de saudação não pode estar afetando todos os serviços de saudação no aplicativo. relatório Olá deve ser serviço Íntegro toohello aplicado ou partição filho específicos de tooa, se a partição toothat pontos de obter mais informações. Olá dados automaticamente superfícies por meio da hierarquia de saudação e uma partição não íntegro ficam visíveis nos níveis de serviço e aplicativos. Essa agregação ajuda toopinpoint e resolver a causa raiz de saudação do problema hello mais rapidamente.

hierarquia de integridade de saudação é composta de relações pai-filho. Um cluster é composto de nós e aplicativos. Os aplicativos possuem serviços e aplicativos implantados. Os aplicativos implantados possuem pacotes de serviço implantados. Os serviços têm partições, e cada partição tem uma ou mais réplicas. Há uma relação especial entre nós e entidades implantadas. Um nó não íntegros conforme relatado pelo seu componente de sistema de autoridade, Olá Failover Manager service afeta Olá implantado aplicativos, pacotes de serviço e réplicas implantadas nele.

hierarquia de integridade Olá representa o estado mais recente de saudação do sistema de saudação com base em relatórios de integridade mais recentes hello, que é uma informação quase em tempo real.
Olá mesmas entidades com base em lógica específica do aplicativo ou condições monitoradas personalizadas podem relatar watchdogs internos e externos. Relatórios do usuário coexistirem com relatórios de saudação do sistema.

Planeje tooinvest em como toohealth tooreport e responder durante a saudação projeta um grande do serviço de nuvem. Este investement inicial torna toodebug mais fácil de serviço de hello, monitorar e operar.

## <a name="health-states"></a>Estados de integridade
Serviço de malha usa três toodescribe de estados de integridade se uma entidade é íntegra ou não: Okey, aviso e erro. Qualquer relatório enviado repositório de integridade toohello deve especificar um desses estados. resultado da avaliação de integridade Olá é um desses estados.

Olá possível [estados de integridade](https://docs.microsoft.com/dotnet/api/system.fabric.health.healthstate) são:

* **OK**. entidade Hello está íntegra. Não há nenhum problema conhecido reportado em seus filhos (quando aplicável).
* **Aviso**. entidade Olá tem alguns problemas, mas que ainda possa funcionar corretamente. Por exemplo, há atrasos, mas eles ainda não causam problemas funcionais. Em alguns casos, condição de aviso Olá pode corrigir próprio sem intervenção externa. Nesses casos, os relatórios de integridade aumentam o reconhecimento e fornecem visibilidade sobre o que está acontecendo. Em outros casos, a condição de aviso Olá pode prejudicar um problema grave sem intervenção do usuário.
* **Erro**. entidade Olá não está íntegra. Ação deve ser realizada toofix estado de saudação da entidade hello, porque ele não pode funcionar corretamente.
* **Desconhecido**. Olá entidade não existe no repositório de integridade de saudação. Esse resultado pode ser obtido em consultas de saudação distribuída que mesclagem os resultados de vários componentes. Por exemplo, consulta de lista de nó de get hello fica muito**FailoverManager**, **ClusterManager**, e **HealthManager**; aplicativo consulta lista fica muito **ClusterManager** e **HealthManager**. Essas consultas mesclam os resultados de vários componentes do sistema. Se outro componente do sistema retorna uma entidade que não está presente no repositório de integridade, hello mesclado resultado tem desconhecido estado de integridade. Uma entidade não está no repositório, como relatórios de integridade ainda não foi processados ou entidade Olá foram limpos após a exclusão.

## <a name="health-policies"></a>Políticas de integridade
repositório de integridade Olá se aplica a toodetermine de diretivas de integridade se uma entidade está íntegra, com base em seus relatórios e seus filhos.

> [!NOTE]
> Políticas de integridade podem ser especificadas no manifesto do cluster hello (para avaliação de integridade do nó e o cluster) ou no manifesto de aplicativo hello (para avaliação de aplicativo e qualquer um de seus filhos). As solicitações de avaliação de integridade também podem passar pelas políticas de avaliação de integridade personalizadas, que são usadas apenas para avaliação.
> 
> 

Por padrão, o Service Fabric aplica regras rígidas (tudo o que deve ser Íntegro) para uma relação hierárquica Olá pai-filho. Se mesmo um dos filhos Olá tem um evento não íntegro, pai Olá é considerado não íntegro.

### <a name="cluster-health-policy"></a>Política de integridade do cluster
Olá [política de integridade de cluster](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy) é tooevaluate usado Olá cluster integridade estados de integridade de estado e o nó. política de saudação pode ser definida no manifesto do cluster hello. Se não estiver presente, a política padrão de saudação (zero toleradas falhas) é usada.
política de integridade de cluster Olá contém:

* [ConsiderWarningAsError](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy.considerwarningaserror). Especifica se tootreat aviso relatórios de integridade como erros durante a avaliação de integridade. Padrão: falso.
* [MaxPercentUnhealthyApplications](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy.maxpercentunhealthyapplications). Especifica o percentual de tolerada máximo de saudação de aplicativos que podem ser não-íntegro, antes de cluster Olá é considerada em erro.
* [MaxPercentUnhealthyNodes](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy.maxpercentunhealthynodes). Especifica o percentual de tolerada máximo de saudação de nós que pode ser não-íntegro, antes de cluster Olá é considerada em erro. Em grandes clusters, alguns nós sempre estão inativos ou out para reparos, portanto essa porcentagem deve ser configurado tootolerate que.
* [ApplicationTypeHealthPolicyMap](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy.applicationtypehealthpolicymap). mapa de política integridade do tipo de aplicativo Hello pode ser usado durante a tipos de aplicativo especial toodescribe do avaliação de integridade de cluster. Por padrão, todos os aplicativos são colocados em um pool e avaliados com MaxPercentUnhealthyApplications. Se alguns tipos de aplicativos devem ser tratados de forma diferente, eles podem ser criados fora do pool global hello. Em vez disso, elas são avaliadas em porcentagens Olá associadas com seu nome de tipo de aplicativo no mapa de saudação. Por exemplo, em um cluster, há milhares de aplicativos de diferentes tipos e algumas instâncias de aplicativo de controle de um tipo especial de aplicativo. aplicativos de controle de saudação nunca devem ser em erro. Você pode especificar global MaxPercentUnhealthyApplications too20% tootolerate algumas falhas, mas para hello "ControlApplicationType" do tipo de aplicativo defina Olá MaxPercentUnhealthyApplications too0. Dessa forma, se alguns Olá muitos aplicativos não-íntegros, mas abaixo da porcentagem de não-íntegro global Olá, cluster Olá seria avaliado tooWarning. Um estado de integridade de aviso não afeta a atualização do cluster nem outros recursos de monitoramento disparados pelo estado de integridade Erro. Mas mesmo um controle de aplicativo no erro tornará o cluster não íntegro, que dispara a reversão ou pausa a atualização do cluster hello, dependendo da configuração de atualização de saudação.
  Para tipos de aplicativo hello definidos no mapa Olá, todas as instâncias do aplicativo são tiradas pool global de saudação de aplicativos. Eles são avaliados com base no número total de saudação de aplicativos do tipo de aplicativo hello, usando Olá MaxPercentUnhealthyApplications específicos de saudação do mapa. Todo o resto de saudação de aplicativos de saudação permanecem no pool global Olá e são avaliadas com MaxPercentUnhealthyApplications.

saudação de exemplo a seguir é um trecho de um manifesto do cluster. entradas toodefine no mapa de tipo de aplicativo hello, nome do parâmetro hello prefixo com "ApplicationTypeMaxPercentUnhealthyApplications-", seguido pelo nome do tipo de aplicativo hello.

```xml
<FabricSettings>
  <Section Name="HealthManager/ClusterHealthPolicy">
    <Parameter Name="ConsiderWarningAsError" Value="False" />
    <Parameter Name="MaxPercentUnhealthyApplications" Value="20" />
    <Parameter Name="MaxPercentUnhealthyNodes" Value="20" />
    <Parameter Name="ApplicationTypeMaxPercentUnhealthyApplications-ControlApplicationType" Value="0" />
  </Section>
</FabricSettings>
```

### <a name="application-health-policy"></a>Política de integridade do aplicativo
Olá [política de integridade do aplicativo](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy) descreve como a avaliação de saudação de agregação de eventos e estados filho é feita para aplicativos e seus filhos. Ela pode ser definida no manifesto de aplicativo hello, **ApplicationManifest.xml**, no pacote de aplicativo hello. Se não há políticas forem especificadas, Service Fabric pressupõe que a entidade hello está íntegra se ele tem um filho ou um relatório de integridade no estado de integridade de aviso ou erro de saudação.
políticas configuráveis Olá são:

* [ConsiderWarningAsError](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy.considerwarningaserror.aspx). Especifica se tootreat aviso relatórios de integridade como erros durante a avaliação de integridade. Padrão: falso.
* [MaxPercentUnhealthyDeployedApplications](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy.maxpercentunhealthydeployedapplications). Especifica a porcentagem de máximo de saudação tolerada de implantação de aplicativos que podem ser não-íntegro, antes que o aplicativo hello é considerado em erro. Essa porcentagem é calculada pela divisão número Olá dos aplicativos implantados não íntegros em número de saudação de nós aplicativos Olá atualmente implantados no cluster hello. computação Olá Arredonda tootolerate uma falha em um número pequeno de nós. Porcentagem padrão: zero.
* [DefaultServiceTypeHealthPolicy](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy.defaultservicetypehealthpolicy). Especifica o saudação padrão serviço tipo diretiva de integridade, que substitui a política de integridade saudação padrão para todos os tipos de serviço no aplicativo hello.
* [ServiceTypeHealthPolicyMap](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy.servicetypehealthpolicymap). Fornece um mapa de políticas de integridade do serviço por tipo de serviço. Essas políticas substituem diretivas de integridade de tipo saudação padrão serviço para cada tipo de serviço especificado. Por exemplo, se um aplicativo tem um tipo de serviço de gateway sem monitoração de estado e um tipo de serviço de mecanismo com monitoração de estado, você pode configurar políticas de integridade de Olá avaliação diferente. Quando você especificar política por tipo de serviço, você pode obter um controle mais granular de integridade de saudação do serviço de saudação.

### <a name="service-type-health-policy"></a>Políticas de integridade do tipo de serviço
Olá [política de integridade do tipo de serviço](https://docs.microsoft.com/dotnet/api/system.fabric.health.servicetypehealthpolicy) Especifica como tooevaluate e agregação Olá serviços e Olá filhos de serviços. política de saudação contém:

* [MaxPercentUnhealthyPartitionsPerService](https://docs.microsoft.com/dotnet/api/system.fabric.health.servicetypehealthpolicy.maxpercentunhealthypartitionsperservice). Especifica a porcentagem de máximo de saudação tolerada de partições problemáticas antes de um serviço é considerado não íntegro. Porcentagem padrão: zero.
* [MaxPercentUnhealthyReplicasPerPartition](https://docs.microsoft.com/dotnet/api/system.fabric.health.servicetypehealthpolicy.maxpercentunhealthyreplicasperpartition). Especifica o percentual máximo de saudação tolerada de réplicas antes de uma partição é considerada não íntegra. Porcentagem padrão: zero.
* [MaxPercentUnhealthyServices](https://docs.microsoft.com/dotnet/api/system.fabric.health.servicetypehealthpolicy.maxpercentunhealthyservices). Especifica a porcentagem de máximo de saudação tolerada de serviços problemáticos antes que o aplicativo hello é considerado não íntegro. Porcentagem padrão: zero.

saudação de exemplo a seguir é um trecho de um manifesto de aplicativo:

```xml
    <Policies>
        <HealthPolicy ConsiderWarningAsError="true" MaxPercentUnhealthyDeployedApplications="20">
            <DefaultServiceTypeHealthPolicy
                   MaxPercentUnhealthyServices="0"
                   MaxPercentUnhealthyPartitionsPerService="10"
                   MaxPercentUnhealthyReplicasPerPartition="0"/>
            <ServiceTypeHealthPolicy ServiceTypeName="FrontEndServiceType"
                   MaxPercentUnhealthyServices="0"
                   MaxPercentUnhealthyPartitionsPerService="20"
                   MaxPercentUnhealthyReplicasPerPartition="0"/>
            <ServiceTypeHealthPolicy ServiceTypeName="BackEndServiceType"
                   MaxPercentUnhealthyServices="20"
                   MaxPercentUnhealthyPartitionsPerService="0"
                   MaxPercentUnhealthyReplicasPerPartition="0">
            </ServiceTypeHealthPolicy>
        </HealthPolicy>
    </Policies>
```

## <a name="health-evaluation"></a>Avaliação da integridade
Os usuários ou serviços automatizados podem avaliar a integridade de qualquer entidade a qualquer momento. tooevaluate integridade da entidade, agregações de repositório de integridade Olá integridade de todos os relatórios na entidade hello e avalia todos os seus filhos (quando aplicável). algoritmo de agregação de integridade Olá usa políticas de integridade que especificam como os relatórios de integridade tooevaluate e como os estados de saúde do filho tooaggregate (quando aplicável).

### <a name="health-report-aggregation"></a>Agregação do relatório de integridade
Uma entidade pode ter vários relatórios de integridade enviados por diferentes relatores (componentes do sistema ou watchdogs) em propriedades diferentes. em particular Olá agregação usa Olá diretivas de integridade associada Olá ConsiderWarningAsError membro do aplicativo ou política de integridade de cluster. ConsiderWarningAsError Especifica como tooevaluate avisos.

Olá estado de integridade agregada é disparado por Olá *pior* relatórios de integridade na entidade hello. Se houver um relatório de integridade de pelo menos um erro, hello estado de integridade agregada é um erro.

![Agregação de relatório de integridade com o relatório de erro.][2]

Uma entidade de integridade que tem um ou mais relatórios de integridade de erro é avaliada como Erro. Olá mesmo é válido para um relatório de integridade expiradas, independentemente de seu estado de integridade.

[2]: ./media/service-fabric-health-introduction/servicefabric-health-report-eval-error.png

Se não houver nenhum relatório de erro e um ou mais avisos, hello estado de integridade agregada é aviso ou erro, dependendo do sinalizador de política de ConsiderWarningAsError hello.

![Agregação do relatório de integridade com o relatório de aviso e ConsiderWarningAsError false.][3]

Agregação de relatório de integridade com o relatório de aviso e ConsiderWarningAsError definir toofalse (padrão).

[3]: ./media/service-fabric-health-introduction/servicefabric-health-report-eval-warning.png

### <a name="child-health-aggregation"></a>Agregação de integridade de filhos
Olá, estado de integridade agregado de uma entidade reflete estados de integridade de filho hello (quando aplicável). algoritmo de saudação para agregar estados de integridade filho usa Olá integridade políticas aplicáveis com base no tipo de entidade hello.

![Agregação de integridade de entidades filho.][4]

Agregação de filhos com base nas políticas de integridade.

[4]: ./media/service-fabric-health-introduction/servicefabric-health-hierarchy-eval.png

Depois que o repositório de integridade Olá avaliar todos os filhos de Olá, ele agrega seus estados de integridade com base na porcentagem de máximo de saudação configurada de filhos não íntegros. Essa porcentagem é obtida da política de saudação com base no tipo de entidade e o filho de saudação.

* Se todos os filhos têm Okey estados, o estado de integridade de filhos agregados de saudação é Okey.
* Se os filhos têm Okey e estados de aviso, o estado de integridade de filhos agregados Olá é um aviso.
* Se não houver filhos com os estados de erro que não respeitam máximo Olá porcentagem permitido de filhos não íntegros, hello estado de integridade agregada é um erro.
* Se a porcentagem permitida de filhos não íntegros, Olá filho Olá Olá de relação de estados de erro máximo é de aviso estado de integridade agregada.

## <a name="health-reporting"></a>Relatório de integridade
Os componentes do sistema, os aplicativos do System Fabric e os watchdogs internos/externos podem ser relatados em relação às entidades do Service Fabric. Verifique Relatores Olá *local* decisões de integridade de saudação de entidades Olá monitorado, com base nas condições de saudação monitoramento. Eles não precisam de toolook em qualquer estado global ou agregar dados. Olá desejado comportamento é Relatores simples toohave e organismos não complexos que precisam toolook em tooinfer de muitas coisas que toosend informações.

dados toosend integridade de toohello repositório de integridade, um Relator precisa de entidade de saudação afetada tooidentify e criar um relatório de integridade. relatório de saudação toosend, use Olá [FabricClient.HealthClient.ReportHealth](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.reporthealth) API, relatar integridade APIs expostos no hello `Partition` ou `CodePackageActivationContext` objetos, os cmdlets do PowerShell ou REST.

### <a name="health-reports"></a>Relatórios de integridade
Olá [relatórios de integridade](https://docs.microsoft.com/dotnet/api/system.fabric.health.healthreport) para cada uma das entidades de saudação em cluster Olá contêm Olá informações a seguir:

* **SourceId**. Uma cadeia de caracteres que identifica exclusivamente o Relator de saudação do evento de integridade de saudação.
* **Identificador de entidade**. Identifica a entidade de saudação onde o relatório de saudação é aplicado. Ele varia de acordo com hello [tipo de entidade](service-fabric-health-introduction.md#health-entities-and-hierarchy):
  
  * Cluster. Nenhuma.
  * Nó. Nome do nó (cadeia de caracteres).
  * Console. Nome do aplicativo (URI). Representa o nome de saudação da instância do aplicativo hello implantada em cluster hello.
  * Serviço. Nome do serviço (URI). Representa o nome de saudação da instância de serviço Olá implantada em cluster hello.
  * Partição. ID da partição (GUID). Representa o identificador exclusivo do hello partição.
  * Réplica. ID de réplica de serviço com monitoração de estado de saudação ou ID de instância de serviço sem monitoração de estado de saudação (INT64).
  * DeployedApplication. Nome do aplicativo (URI) e o nome do nó (cadeia de caracteres).
  * DeployedServicePackage. Nome do aplicativo (URI), nome do nó (cadeia de caracteres) e nome do manifesto do serviço (cadeia de caracteres).
* **Property**. Um *cadeia de caracteres* (não uma enumeração fixa) que permite que Relator Olá toocategorize Olá integridade evento para uma propriedade específica da entidade de saudação. Por exemplo, Relator um pode relatar a integridade de saudação de propriedade de "Armazenamento" hello Node01 e Relator B pode relatar a integridade de saudação da propriedade de "Conectividade" hello Node01. No repositório de integridade hello, esses relatórios são tratados como eventos de integridade separado de saudação Node01 entidade.
* **Description**. Uma cadeia de caracteres que permite que um tooprovide Relator informações detalhadas sobre o evento de integridade hello. **SourceId**, **propriedade**, e **HealthState** totalmente deve descrever o relatório de saudação. Descrição de saudação adiciona legível informações sobre relatórios de saudação. texto de saudação torna mais fácil para o relatório de integridade de saudação toounderstand administradores e usuários.
* **HealthState**. Um [enumeração](service-fabric-health-introduction.md#health-states) que descreve o estado de integridade de saudação do relatório hello. Olá os valores aceitos são Okey, aviso e erro.
* **TimeToLive**. Um timespan que indica o relatório de integridade Olá quanto tempo é válido. Juntamente com **RemoveWhenExpired**, ele permite que o repositório de integridade hello como tooevaluate expirado eventos. Por padrão, valor Olá é infinito e relatório Olá é válido indefinidamente.
* **RemoveWhenExpired**. Um valor booleano. Se definir tootrue, Olá integridade expirada relatório será removido automaticamente do repositório de integridade hello e relatório Olá não afeta a avaliação de integridade de entidade. Usado quando o relatório de saudação é válido para um determinado período de tempo e Relator Olá não precisa tooexplicitly limpá-la. Também usou toodelete relatórios do repositório de integridade da saudação (por exemplo, uma vigia é alterada e interromperá o envio de relatórios com origem anterior e a propriedade). Ele pode enviar um relatório com uma breve TimeToLive junto com RemoveWhenExpired tooclear qualquer estado anterior do repositório de integridade de saudação. Se o valor de saudação é definido toofalse, hello relatório expirado é tratado como um erro na avaliação de integridade de saudação. valor falso Olá sinaliza toohello repositório de integridade que dessa fonte Olá deve relatar periodicamente esta propriedade. Se não estiver, deve haver algo de errado com watchdog hello. integridade do watchdog Olá é capturada, considerando o evento hello como um erro.
* **SequenceNumber**. Um inteiro positivo que precisa toobe crescentes, ele representa a ordem de saudação dos relatórios de saudação. Ele é usado por Olá repositório toodetect obsoletos relatórios de integridade recebidos atrasado devido a atrasos na rede ou outros problemas. Um relatório será rejeitado se o número de sequência de saudação é menor ou igual número toohello recentemente aplicada para Olá mesma entidade, fonte e à propriedade. Se não for especificado, o número de sequência de saudação é gerado automaticamente. É necessário tooput no número de sequência de saudação somente quando o relatório em transições de estado. Nessa situação, origem Olá deve tooremember quais relatórios-enviados e manter as informações de saudação para recuperação durante o failover.

Essas quatro informações: SourceId, identificador da entidade, Propriedade e HealthState são obrigatórios para cada relatório de integridade. Olá SourceId de cadeia de caracteres não é permitido toostart com prefixo hello "**System.**", que é reservado para relatórios do sistema. Para Olá mesma entidade, há apenas um relatório para Olá mesma origem e propriedade. Olá vários relatórios para a mesma fonte e substituição de propriedade entre si, do lado do cliente para o funcionamento de saudação (se eles são divididas em lotes) ou Olá integridade do lado da loja. substituição de saudação é baseada nos números de sequência; os relatórios mais recentes (com números de sequência mais alto) substituem relatórios mais antigos.

### <a name="health-events"></a>Eventos de integridade
Internamente, o repositório de integridade de saudação mantém [eventos de integridade](https://docs.microsoft.com/dotnet/api/system.fabric.health.healthevent), que contém todas as informações de saudação do hello relatórios e metadados adicionais. Olá metadados incluem relatório Olá recebeu toohello cliente de integridade do tempo de saudação e ele foi modificado no lado do servidor de saudação do tempo de saudação. eventos de integridade de saudação são retornados por [consultas de integridade](service-fabric-view-entities-aggregated-health.md#health-queries).

Olá adicionado metadados contém:

* **SourceUtcTimestamp**. relatório de Olá Olá horas recebeu toohello cliente de integridade (Coordinated Universal Time).
* **LastModifiedUtcTimestamp**. relatório de Olá Olá tempo da última modificação no lado do servidor de saudação (Coordinated Universal Time).
* **IsExpired**. Um sinalizador tooindicate se o relatório de saudação expirou quando Olá consulta foi executada pelo repositório de integridade de saudação. Um evento pode ter expirado somente se RemoveWhenExpired for false. Caso contrário, o evento de saudação não é retornado pela consulta e é removido do repositório de saudação.
* **LastOkTransitionAt**, **LastWarningTransitionAt**, **LastErrorTransitionAt**. Olá hora da última transições Okey/aviso/erro. Esses campos oferecem histórico de saudação de transições de estado de integridade saudação do evento hello.

campos de transição de estado Olá podem ser usados para alertas mais inteligentes ou informações de evento de integridade "históricos". Eles permitem cenários como:

* Alertar quando uma propriedade estiver no estado aviso/erro por mais de X minutos. Verificar condição Olá por um período de tempo evita alertas em condições temporárias. Por exemplo, um alerta se o estado de integridade de saudação tem sido aviso por mais de cinco minutos pode ser convertido em (HealthState = = aviso e agora - LastWarningTransitionTime > 5 minutos).
* Alertar somente nas condições que foram alterados no hello últimos X minutos. Se um relatório já foi erro antes de saudação especificado de tempo, pode ser ignorado porque ele já foi sinalizado anteriormente.
* Se uma propriedade estiver alternando entre aviso e erro, determine por quanto tempo ele esteve não íntegro (isto é, não OK). Por exemplo, um alerta se a propriedade Olá não estava íntegra por mais de cinco minutos pode ser convertido em (HealthState! = Okey e agora - LastOkTransitionTime > 5 minutos).

## <a name="example-report-and-evaluate-application-health"></a>Exemplo: relatar e avaliar integridade do aplicativo
Olá, exemplo a seguir envia um relatório de integridade por meio do PowerShell no aplicativo hello **fabric: / WordCount** de fonte Olá **MyWatchdog**. relatório de integridade Olá contém informações sobre propriedade de integridade hello "disponibilidade" em um estado de integridade de erro, com TimeToLive infinito. Em seguida, ele consultará a integridade do aplicativo hello, que retorna agregados erros de estado de integridade e hello relatado eventos de integridade na lista de saudação de eventos de integridade.

```powershell
PS C:\> Send-ServiceFabricApplicationHealthReport –ApplicationName fabric:/WordCount –SourceId "MyWatchdog" –HealthProperty "Availability" –HealthState Error

PS C:\> Get-ServiceFabricApplicationHealth fabric:/WordCount -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            :
                                  Error event: SourceId='MyWatchdog', Property='Availability'.

ServiceHealthStates             :
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Error

                                  ServiceName           : fabric:/WordCount/WordCountWebService
                                  AggregatedHealthState : Ok

DeployedApplicationHealthStates :
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_0
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_2
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_3
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_4
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_1
                                  AggregatedHealthState : Ok

HealthEvents                    :
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 360
                                  SentAt                : 3/22/2016 7:56:53 PM
                                  ReceivedAt            : 3/22/2016 7:56:53 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 3/22/2016 7:56:53 PM, LastWarning = 1/1/0001 12:00:00 AM

                                  SourceId              : MyWatchdog
                                  Property              : Availability
                                  HealthState           : Error
                                  SequenceNumber        : 131032204762818013
                                  SentAt                : 3/23/2016 3:27:56 PM
                                  ReceivedAt            : 3/23/2016 3:27:56 PM
                                  TTL                   : Infinite
                                  Description           :
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Ok->Error = 3/23/2016 3:27:56 PM, LastWarning = 1/1/0001 12:00:00 AM
```

## <a name="health-model-usage"></a>Uso do modelo de integridade
modelo de integridade de saudação permite que serviços de nuvem e plataforma tooscale de malha do serviço subjacente Olá, como monitoramento e integridade decisões são distribuídas entre monitores diferentes de saudação em cluster hello.
Outros sistemas têm um único serviço centralizado no nível do cluster Olá analisa Olá todos os *potencialmente* emitidas por serviços de informações úteis. Essa abordagem impede a escalabilidade dos mesmos. Ele também não permite obter informações específicas de toocollect toohelp identificar problemas e problemas potenciais, como fechar toohello causa possível.

modelo de integridade de saudação é usado intensamente para monitoramento e diagnóstico, para avaliar a integridade de cluster e o aplicativo e para atualizações monitoradas. Outros serviços de usam a integridade de dados tooperform automática repara, criar histórico de integridade do cluster e emitem alertas em determinadas condições.

## <a name="next-steps"></a>Próximas etapas
[Como exibir relatórios de integridade do Service Fabric](service-fabric-view-entities-aggregated-health.md)

[Usar relatórios de integridade do sistema para solução de problemas](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[Como tooreport e verificação de integridade do serviço](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[Adicionar relatórios de integridade personalizados do Service Fabric](service-fabric-report-health.md)

[Monitorar e diagnosticar serviços localmente](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Atualização de aplicativos do Service Fabric](service-fabric-application-upgrade.md)

