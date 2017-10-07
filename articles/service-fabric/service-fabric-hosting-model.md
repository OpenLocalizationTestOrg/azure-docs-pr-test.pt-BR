---
title: "aaaAzure modelo de host de malha do serviço | Microsoft Docs"
description: "Descreve a relação entre réplicas (ou instâncias) de um serviço do Service Fabric implantado e o processo de host do serviço."
services: service-fabric
documentationcenter: .net
author: harahma
manager: timlt
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/15/2017
ms.author: harahma
ms.openlocfilehash: 30e0ba19cd672a722f76477a311ecef7c213b055
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-hosting-model"></a>Modelo de hospedagem do Service Fabric
Este artigo fornece uma visão geral dos modelos fornecidos pela malha do serviço de hospedagem de aplicativos e descreve as diferenças de saudação entre hello **processo compartilhado** e **processo exclusivo** modelos. Ele descreve a aparência de um aplicativo implantado em um nó de malha do serviço e a relação entre réplicas (ou instâncias) do serviço de saudação e o processo de host de serviço hello.

Antes de continuar, familiarize-se com o [Modelo de Aplicativo do Service Fabric][a1] e compreenda vários conceitos e a relação entre eles. 

> [!NOTE]
> Neste artigo, para fins de simplicidade, a menos que mencionado explicitamente:
>
> - Todos os usos do word *réplica* refere-se tooboth uma réplica de um serviço com monitoração de estado ou uma instância de um serviço statless.
> - *CodePackage* é o equivalente tratada muito*ServiceHost* processo registra um *ServiceType* e hosts de réplicas de serviços do que *ServiceType*.
>

toounderstand Olá modelo de hospedagem, vamos percorrer um exemplo. Digamos que temos um *ApplicationType* “MyAppType”, que tem um *ServiceType* “MyServiceType”, que é fornecido por *ServicePackage* “MyServicePackage”, que tem um *CodePackage* “MyCodePackage”, que registra *ServiceType* “MyServiceType” quando é executado.

Vamos supor que temos um cluster de 3 nós e que criamos um *aplicativo* **fabric:/App1** do tipo “MyAppType”. Nesse *aplicativo* **fabric:/App1**, criamos um serviço **fabric:/App1/ServiceA** do tipo “MyServiceType”, que tem 2 partições (digamos **P1** & **P2**) e 3 réplicas por partição. Olá diagrama a seguir mostra exibição Olá deste aplicativo como ele acaba implantado em um nó.

<center>
![Exibição do nó do aplicativo implantado][node-view-one]
</center>

Service Fabric ativado 'MyServicePackage' que foi iniciado 'MyCodePackage', que está hospedando réplicas de ambas as partições de saudação ou seja, **P1** & **P2**. Observe que todos os nós de saudação em cluster Olá terá mesma exibição desde que escolhemos o número de réplicas por toonumber igual de partição de nós no cluster de saudação. Vamos criar outro serviço **fabric:/App1/ServiceB** no aplicativo **fabric:/App1** que tem 1 partição (digamos **P3**) e 3 réplicas por partição. Diagrama a seguir mostra a nova exibição Olá no nó de saudação:

<center>
![Exibição do nó do aplicativo implantado][node-view-two]
</center>

Como podemos ver Service Fabric colocada a nova réplica Olá para partição **P3** do serviço **fabric: / App1/ServiceB** na ativação existente de saudação do 'MyServicePackage'. Agora, vamos criar outro *aplicativo* **fabric:/App2** do tipo “MyAppType” e dentro de **fabric:/App2** criar o serviço **fabric:/App2/ServiceA**, que tem 2 partições (digamos **P4** & **P5**) e 3 réplicas por partição. Diagramas a seguir mostra a nova exibição de nó hello:

<center>
![Exibição do nó do aplicativo implantado][node-view-three]
</center>

Desta vez, o Service Fabric ativou uma nova cópia de “MyServicePackage”, que inicia uma nova cópia de “MyCodePackage” e as réplicas de ambas as partições do serviço **fabric:/App2/ServiceA** (ou seja, **P4** & **P5**) são colocadas nessa nova cópia de “MyCodePackage”.

## <a name="shared-process-model"></a>Modelo de processo compartilhado
O que vimos acima é o padrão de saudação do modelo fornecido pela malha do serviço de hospedagem e é chamado tooas **processo compartilhado** modelo. Nesse modelo, para um determinado *aplicativo*, apenas uma cópia de um determinado *ServicePackage* é ativado em um *nó* (que iniciará o hello todos os *CodePackages* contidos nele) e todos os Olá réplicas de todos os serviços de um determinado *ServiceType* são colocados em Olá *CodePackage* que registra que *ServiceType*. Em outras palavras, todos os Olá réplicas de todos os serviços de um determinado *ServiceType* compartilhar Olá mesmo processo.

## <a name="exclusive-process-model"></a>Modelo de processo exclusivo
Olá outro modelo de hospedagem fornecido pelo Service Fabric é **processo exclusivo** modelo. Nesse modelo, em um determinado *nó*, para colocar cada réplica, o Service Fabric ativa uma nova cópia do *ServicePackage* (que iniciará o hello todos os *CodePackages* contidos nele ) e a réplica é colocada no hello *CodePackage* que Olá registrado *ServiceType* de saudação serviço toowhich réplica pertence. Em outras palavras, cada réplica reside em seu próprio processo dedicado. 

Há suporte para esse modelo a partir da versão 5.6 do Service Fabric. **Processo exclusivo** modelo pode ser escolhido no tempo de saudação de criação de serviço de saudação (usando [PowerShell][p1], [REST] [ r1]ou [FabricClient][c1]), especificando **ServicePackageActivationMode** como 'ExclusiveProcess'.

```powershell
PS C:\>New-ServiceFabricService -ApplicationName "fabric:/App1" -ServiceName "fabric:/App1/ServiceA" -ServiceTypeName "MyServiceType" -Stateless -PartitionSchemeSingleton -InstanceCount -1 -ServicePackageActivationMode "ExclusiveProcess"
```

```csharp
var serviceDescription = new StatelessServiceDescription
{
    ApplicationName = new Uri("fabric:/App1"),
    ServiceName = new Uri("fabric:/App1/ServiceA"),
    ServiceTypeName = "MyServiceType",
    PartitionSchemeDescription = new SingletonPartitionSchemeDescription(),
    InstanceCount = -1,
    ServicePackageActivationMode = ServicePackageActivationMode.ExclusiveProcess
};

var fabricClient = new FabricClient(clusterEndpoints);
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

Se você tiver um serviço padrão no manifesto do aplicativo, poderá escolher o modelo de **Processo Exclusivo** especificando o atributo **ServicePackageActivationMode** conforme mostrado abaixo:

```xml
<DefaultServices>
  <Service Name="MyService" ServicePackageActivationMode="ExclusiveProcess">
    <StatelessService ServiceTypeName="MyServiceType" InstanceCount="1">
      <SingletonPartition/>
    </StatelessService>
  </Service>
</DefaultServices>
```
Continuando com o nosso exemplo acima, permite criar outro serviço **fabric: / App1/ServiceC** no aplicativo **fabric: / App1** que tem 2 partições (digamos **P6**  &  **P7**) e 3 réplicas por partição com **ServicePackageActivationMode** definir too'ExclusiveProcess'. Diagrama a seguir mostra o novo modo de exibição no nó hello:

<center>
![Exibição do nó do aplicativo implantado][node-view-four]
</center>

Como você pode ver, o Service Fabric ativou duas novas cópias de “MyServicePackage” (uma para cada réplica da partição **P6** & **P7**) e colocou cada réplica em sua cópia dedicada de *CodePackage*. Outro toonote coisa aqui é, quando **processo exclusivo** modelo é usado, para um determinado *aplicativo*, várias cópias de um determinado *ServicePackage* podem estar ativas em um  *Nó*. No exemplo acima, vemos que três cópias de “MyServicePackage” estão ativas em **fabric:/App1**. Cada uma dessas cópias ativas de “MyServicePackage” tem uma **ServicePackageAtivationId** associada a ela que identifica essa cópia no *aplicativo* **fabric:/App1**.

Quando apenas o modelo de **Processo Compartilhado** é usado para um *aplicativo*, como **fabric:/App2** no exemplo acima, há apenas uma cópia ativa do *ServicePackage* em um *Nó* e uma **ServicePackageAtivationId** dessa ativação do *ServicePackage* é uma “cadeia de caracteres vazia”.

> [!NOTE]
>- **Compartilhado processo** hospedando modelo corresponde muito**ServicePackageAtivationMode** igual **SharedProcess**. Este é o padrão de saudação hospedando modelo e **ServicePackageAtivationMode** não precisa ser especificado em tempo de saudação de criação de serviço de saudação.
>
>- **Processo exclusivo** hospedando modelo corresponde muito**ServicePackageAtivationMode** igual **ExclusiveProcess** e precisa toobe especificado explicitamente no tempo de saudação de criação de saudação serviço. 
>
>- Modelo de hospedagem de um serviço pode ser conhecido por consultar Olá [descrição do serviço] [ p2] e examinando o valor de **ServicePackageAtivationMode**.
>
>

## <a name="working-with-deployed-service-package"></a>Trabalhando com o pacote de serviço implantado
Uma cópia ativa de um *ServicePackage* em um nó é conhecido como um [pacote de serviço implantado][p3]. Conforme mencionado anteriormente acima, quando **processo exclusivo** modelo é usado para criar serviços, para um determinado *aplicativo*, pode haver vários serviço implantado pacotes para Olá mesmo  *ServicePackage*. Ao executar operações como o pacote de serviço específico toodeployed [relatório de integridade de um pacote de serviço implantado] [ p4] ou [reiniciar o pacote de código de um pacote de serviço implantado] [ p5] etc., **ServicePackageActivationId** toobe necessidades fornecido tooidentify um pacote de serviço implantado específico.

 **ServicePackageActivationId** de um serviço implantado o pacote pode ser obtido consultando a lista de saudação do [pacotes de serviço implantados] [ p3] em um nó. Ao consultar [implantado tipos de serviço][p6], [implantado réplicas] [ p7] e [implantado pacotes de códigos] [ p8] em um nó, o resultado da consulta Olá também contém Olá **ServicePackageActivationId** de pacote de serviço pai implantado.

> [!NOTE]
>- No modelo de hospedagem do **Processo Compartilhado**, em determinado *nó* de determinado *aplicativo*, apenas uma cópia de um *ServicePackage* é ativada. Ele tem **ServicePackageActivationId** igual muito*cadeia de caracteres vazia* e não precisa ser especificada enquanto operações relacionadas à execução de pacote de serviço implantado. 
>
> - No modelo de hospedagem do **Processo Exclusivo**, em um determinado *nó* de determinado *aplicativo*, uma ou mais cópias de um *ServicePackage* podem estar ativas. Cada ativação tem um *não vazio* **ServicePackageActivationId** e precisa toobe especificado enquanto operações relacionadas à execução de pacote de serviço implantado. 
>
> - Se **ServicePackageActivationId** é omitido, o padrão é too'empty de cadeia de caracteres '. Se um serviço implantado do pacote que foi ativada em **processo compartilhado** modelo está presente, em seguida, será possível executar a operação, caso contrário, Olá operação falhará.
>
> - Não é recomendável tooquery uma vez e cache **ServicePackageActivationId** conforme ele é gerado dinamicamente e pode alterar por vários motivos. Antes de executar uma operação que precisa **ServicePackageActivationId**, você primeiro deve consultar a lista de saudação do [pacotes de serviço implantados] [ p3] em um nó e, em seguida, use  *ServicePackageActivationId** de operação de Olá de tooperform resultados de consulta original.
>
>

## <a name="guest-executable-and-container-applications"></a>Aplicativos executáveis e de contêiner convidados
O Service Fabric trata os aplicativos [executáveis][a2] e de [contêiner convidados][a3] como serviços sem estado que são independentes; ou seja, não há nenhum tempo de execução do Service Fabric em *ServiceHost* (um processo ou contêiner). Como esses serviços são independentes, o número de réplicas por *ServiceHost* não é aplicável a esses serviços. Olá, configuração mais comum usada com esses serviços é única partição com [InstanceCount] [ c2] igual muito-1 (ou seja, uma cópia do código de saudação do serviço em execução em cada nó do cluster). 

Olá padrão **ServicePackageActivationMode** para esses serviços é **SharedProcess** caso em que o Service Fabric ativa somente uma cópia de *ServicePackage* em um *Nó* para um determinado *aplicativo* que significa que apenas uma cópia do código de serviço será executado um *nó*. Se você quiser várias cópias de seu toorun de código de serviço em um *nó* quando você criar vários serviços (*Service1* muito*ServiceN*) de *ServiceType* (especificado na *ServiceManifest*) ou ao seu serviço for particionado vários, você deve especificar **ServicePackageActivationMode** como **ExclusiveProcess**em tempo de saudação de criação de serviço de saudação.

## <a name="changing-hosting-model-of-an-existing-service"></a>Alterando o modelo de hospedagem de um serviço existente
Alterar o modelo de hospedagem de um serviço existente do **processo compartilhado** muito**processo exclusivo** e vice-versa por meio de atualização ou mecanismo de atualização (ou especificação de aplicativo de serviço padrão manifesto) não é suportado atualmente. O suporte a esse recurso será fornecido em versões futuras.

## <a name="choosing-between-shared-process-and-exclusive-process-model"></a>Escolhendo entre o modelo de processo compartilhado e processo exclusivo
Esses modelos de hospedagem têm seus prós e contras e o usuário deve tooevaluate que melhor atenda suas necessidades. **Compartilhado processo** modelo permite melhor utilização de recursos do sistema operacional porque menos processos são gerados, Olá de várias réplicas no mesmo processo pode compartilhar portas, etc. No entanto, se uma das réplicas Olá atinge um erro em que ele precisa toobring para baixo de host de serviço hello, isso afetará todas as outras réplicas no mesmo processo.

 O modelo de **Processo Exclusivo** fornece um melhor isolamento com cada réplica em seu próprio processo e uma réplica com comportamento inadequado não afetará outras réplicas. Essa opção é útil para casos onde o compartilhamento de porta não é suportado pelo protocolo de comunicação de saudação. Ele facilita a governança de recursos de tooapply Olá capacidade no nível da réplica. Olá por outro lado, **processo exclusivo** consumirá mais recursos do sistema operacional, ele gera um processo para cada réplica no nó de saudação.

## <a name="exclusive-process-model-and-application-model-considerations"></a>Considerações sobre o modelo de processo exclusivo e o modelo de aplicativo
Olá recomendado maneira toomodel seu aplicativo no serviço de malha é tookeep uma *ServiceType* por *ServicePackage* e esse modelo funciona bem para a maioria dos aplicativos de saudação. 

No entanto, cenários especiais tooenable onde um *ServiceType* por *ServicePackage* pode não ser desejável, funcionalmente, Service Fabric permite toohave mais de uma *ServiceType* por *ServicePackage* (um *CodePackage* pode registrar mais de um *ServiceType*). A seguir estão alguns dos cenários de saudação onde essas configurações podem ser úteis:

- Você deseja toooptimize utilização de recursos de sistema operacional, gerando menos processos e tornando maior densidade de réplica por processo.
- Réplicas de diferentes ServiceTypes necessário tooshare alguns dados comuns que tem uma alta inicialização ou o custo de memória.
- Você tem uma oferta de serviço gratuito e deseja tooput um limite de utilização de recursos, colocando todas as réplicas do serviço de saudação no mesmo processo.

O modelo de hospedagem de **Processo Exclusivo** não é coerente com o modelo de aplicativo que tem vários *ServiceTypes* por *ServicePackage*. Isso ocorre porque vários *ServiceTypes* por *ServicePackage* é projetado tooachieve mais recursos de compartilhamento entre réplicas e permite maior densidade de réplica por processo. Isso é toowhat contrary **processo exclusivo** modelo é tooachieve projetado.

Considere o caso de saudação de vários *ServiceTypes* por *ServicePackage* com diferentes *CodePackage* registrar cada *ServiceType*. Digamos que temos um *ServicePackage* “MultiTypeServicePackge”, que tem dois *CodePackages*:

- “MyCodePackageA”, que registra *ServiceType* “MyServiceTypeA”.
- “MyCodePackageB”, que registra *ServiceType* “MyServiceTypeB”.

Agora, digamos que criamos um *aplicativo* **fabric:/SpecialApp** e dentro de **fabric:/SpecialApp** criamos os dois seguintes serviços com o modelo de **Processo Exclusivo**:

- Serviço **fabric:/SpecialApp/ServiceA** do tipo “MyServiceTypeA” com duas partições (digamos **P1** e **P2**) e 3 réplicas por partição.
- Serviço **fabric:/SpecialApp/ServiceB** do tipo “MyServiceTypeB” com duas partições (digamos **P3** e **P4**) e 3 réplicas por partição.

Em um nó específico, os dois serviços Olá terá duas réplicas. Como usamos **processo exclusivo** serviços do modelo toocreate hello, Service Fabric ativará uma nova cópia de 'MyServicePackge' para cada réplica. Cada ativação de “MultiTypeServicePackge” iniciará uma cópia de “MyCodePackageA” e “MyCodePackageB”. No entanto, apenas um dos 'MyCodePackageA' ou 'MyCodePackageB' hospedará a réplica Olá para o qual 'MultiTypeServicePackge' foi ativado. Diagrama a seguir mostra a exibição do nó de saudação:

<center>
![Exibição do nó do aplicativo implantado][node-view-five]
</center>

 Como podemos ver, na ativação de saudação do 'MultiTypeServicePackge' para a réplica da partição **P1** do serviço **fabric: / SpecialApp/Services**, 'MyCodePackageA' está hospedando a réplica hello e ' MyCodePackageB' está apenas em execução. Da mesma forma, na ativação de 'MultiTypeServicePackge' para a réplica da partição **P3** do serviço **fabric: / SpecialApp/ServiceB**, 'MyCodePackageB' está hospedando a réplica de saudação e é 'MyCodePackageA' apenas em funcionamento e assim por diante. Portanto, Olá mais o número de *CodePackages* (Registrando diferentes *ServiceTypes*) por *ServicePackage*, maior será o uso de recursos de redundância. 
 
 Olá no outro lado, se criarmos Serviços **malha: / SpecialApp/Services** e **fabric: / SpecialApp/ServiceB** com **processo compartilhado** modelo será Service Fabric Ativar somente uma cópia de 'MultiTypeServicePackge' para *aplicativo* **fabric: / SpecialApp** (como visto anteriormente). 'MyCodePackageA' hospedará todas as réplicas para o serviço **fabric: / SpecialApp/Services** (ou de qualquer serviço do tipo 'MyServiceTypeA' toobe mais preciso) e 'MyCodePackageB' hospedará todas as réplicas para o serviço **fabric: / SpecialApp/ServiceB** (ou de qualquer serviço do tipo 'MyServiceTypeB' toobe mais preciso). Diagrama a seguir mostra a exibição do nó Olá nessa configuração: 

<center>
![Exibição do nó do aplicativo implantado][node-view-six]
</center>

Olá, o exemplo acima, você pode pensar se 'MyCodePackageA' registra 'MyServiceTypeA' e 'MyServiceTypeB' e não há nenhum MyCodePackageB, será redundante não *CodePackage* em execução. Isso está correto, mas, como mencionado anteriormente, esse modelo de aplicativo não se alinha com o modelo de hospedagem de **Processo Exclusivo**. Se o objetivo é tooput cada réplica em seu próprio dedicado processo de registro de ambos *ServiceTypes* mesmo *CodePackage* não é necessária e colocando cada *ServiceType* em seu próprio *ServicePacakge* é uma escolha mais natural.

## <a name="next-steps"></a>Próximas etapas
[Empacotar um aplicativo] [ a4] e deixá-lo toodeploy pronto.

[Implantar e remover aplicativos] [ a5] descreve como instâncias do aplicativo toouse PowerShell toomanage.

<!--Image references-->
[node-view-one]: ./media/service-fabric-hosting-model/node-view-one.png
[node-view-two]: ./media/service-fabric-hosting-model/node-view-two.png
[node-view-three]: ./media/service-fabric-hosting-model/node-view-three.png
[node-view-four]: ./media/service-fabric-hosting-model/node-view-four.png
[node-view-five]: ./media/service-fabric-hosting-model/node-view-five.png
[node-view-six]: ./media/service-fabric-hosting-model/node-view-six.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[a1]: service-fabric-application-model.md
[a2]: service-fabric-deploy-existing-app.md
[a3]: service-fabric-containers-overview.md
[a4]: service-fabric-package-apps.md
[a5]: service-fabric-deploy-remove-applications.md

[r1]: https://docs.microsoft.com/rest/api/servicefabric/sfclient-api-createservice

[c1]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync
[c2]: https://docs.microsoft.com/dotnet/api/system.fabric.description.statelessservicedescription.instancecount

[p1]: https://docs.microsoft.com/powershell/servicefabric/vlatest/new-servicefabricservice
[p2]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricservicedescription
[p3]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedservicePackage
[p4]: https://docs.microsoft.com/powershell/servicefabric/vlatest/send-servicefabricdeployedservicepackagehealthreport
[p5]: https://docs.microsoft.com/powershell/servicefabric/vlatest/restart-servicefabricdeployedcodepackage
[p6]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedservicetype
[p7]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedreplica
[p8]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedcodepackage