---
title: "aaaOverview do modelo de programação de malha confiável serviço Olá | Microsoft Docs"
description: "Saiba mais sobre o modelo de programação dos Serviços Confiáveis da Malha de Serviços e comece a desenvolver seus próprios serviços."
services: Service-Fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: vturecek; mani-ramaswamy
ms.assetid: 0c88a533-73f8-4ae1-a939-67d17456ac06
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: masnider;
ms.openlocfilehash: 41d1826df902b1f1845c4702bf2567e6b9ca1f1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-services-overview"></a>Visão geral dos Reliable Services
O Azure Service Fabric simplifica o desenvolvimento e o gerenciamento de Reliable Services com e sem estado. Este tópico aborda:

* Olá serviços confiáveis modelo de programação para serviços com e sem monitoração de estado.
* Olá opções que você tem toomake ao escrever um serviço confiável.
* Alguns cenários e exemplos de quando toouse confiável serviços e como eles são gravados.

Serviços confiáveis é um dos Olá disponíveis no serviço de malha de modelos de programação. Olá outros é Olá Reliable Actor modelo de programação, que fornece um modelo de programação de ator virtual sobre o modelo de serviços confiáveis hello. Para obter mais informações sobre o modelo de programação de Reliable Actors hello, consulte [tooService Introdução malha Reliable Actors](service-fabric-reliable-actors-introduction.md).

Malha do serviço gerencia o tempo de vida de saudação dos serviços de provisionamento e implantação por meio de atualização e exclusão, por meio de [gerenciamento de aplicativos do Service Fabric](service-fabric-deploy-remove-applications.md).

## <a name="what-are-reliable-services"></a>O que são os Reliable Services?
Serviços confiáveis oferece um simples, eficiente, de nível superior de programação toohelp de modelo você express, o que é importante tooyour aplicativo. Com serviços confiáveis Olá modelo de programação, você obtém:

* Restante toohello acesso Olá APIs de programação do Service Fabric. Ao contrário de serviços de malha do serviço modelada como [convidado executáveis](service-fabric-deploy-existing-app.md), serviços confiáveis obter toouse restante Olá Olá APIs de malha do serviço diretamente. Isso permite que os serviços:
  * Sistema de saudação de consulta
  * integridade de relatório sobre as entidades no cluster Olá
  * receber notificações sobre alterações de configuração e código
  * localizar e comunicar-se com outros serviços,
  * (opcionalmente) use Olá [coleções confiável](service-fabric-reliable-services-reliable-collections.md)
  * ... e lhes acessar outros recursos, toomany tudo a partir de um modelo de programação de primeira classe em várias linguagens de programação.
* Um modelo simples para execução de seu próprio código que parece com os modelos de programação com os quais você está acostumado. Seu código tem um ponto de entrada bem definido e um ciclo de vida fácil de gerenciar.
* Um modelo de comunicação conectável. Usar o transporte de saudação de sua escolha, como HTTP com [API da Web](service-fabric-reliable-services-communication-webapi.md), WebSockets, protocolos TCP personalizados, ou qualquer outra coisa. O Reliable Services oferece excelentes opções de utilização ou permite que você forneça suas próprias.
* Para os serviços com monitoração de estado, serviços confiáveis hello, modelo de programação permite tooconsistently e confiável armazenar o estado dentro do seu serviço usando [coleções confiável](service-fabric-reliable-services-reliable-collections.md). Coleções confiáveis são um conjunto simples de classes de coleção confiável e altamente disponível que será familiar tooanyone que usou c# coleções. Tradicionalmente, os serviços precisavam de sistemas externos para um gerenciamento de estado confiável. Com coleções confiável, você pode armazenar sua computação tooyour próxima de estado com hello mesmo alta disponibilidade e confiabilidade que você tooexpect vêm dos repositórios externos altamente disponíveis. Esse modelo também melhora a latência porque você é co-Localizando computação hello e precisa toofunction de estado.

Assista a este vídeo da Microsoft Virtual Academy para ter uma visão geral dos Reliable Services: <center>
<a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=HhD9566yC_4106218965">
<img src="./media/service-fabric-reliable-services-introduction/ReliableServicesVid.png" WIDTH="360" HEIGHT="244" />
</a>
</center>

## <a name="what-makes-reliable-services-different"></a>O que torna o Reliable Services diferente?
Os Serviços Confiáveis na Malha de Serviços são diferentes dos serviços que você já desenvolveu anteriormente. A Malha de Serviços fornece confiabilidade, disponibilidade, consistência e escalabilidade.

* **Confiabilidade** - seu serviço permanece o mesmo em ambientes não confiáveis em que as máquinas falharam ou pressione problemas de rede, ou em casos onde Olá serviços se encontrar erros e falhas ou falhar. Para os serviços com monitoração de estado, seu estado é preservado mesmo na presença de saudação de rede ou outras falhas.
* **Disponibilidade** – Seu serviço estará acessível e responderá rapidamente. O Service Fabric mantém o número desejado de cópias de execução.
* **Escalabilidade** - serviços são separados do hardware específico e eles podem aumentar ou reduzir conforme necessário por meio da adição de saudação ou remoção de hardware ou outros recursos. Os serviços são tooensure facilmente particionado (especialmente no caso de monitoração de estado Olá) que pode ser dimensionada serviço hello e identificador falhas parciais. Serviços podem ser criados e excluídas dinamicamente por meio de código, permitindo mais toobe instâncias girado backup conforme necessário, digamos em resposta toocustomer solicitações. Finalmente, o Service Fabric incentiva leve de toobe de serviços. Serviço de malha permite que milhares de serviços toobe provisionados em um único processo, em vez de exigir ou dedicar instâncias inteiras do sistema operacional ou processos tooa única instância de um serviço.
* **Consistência** -quaisquer informações armazenadas neste serviço podem ser garantidas toobe consistente. Isso é verdadeiro mesmo entre várias coleções confiáveis dentro de um serviço. Alterações nas coleções dentro de um serviço podem ser feitas de forma transacional atômica.

## <a name="service-lifecycle"></a>Ciclo de vida do serviço
Independentemente de seu serviço ser com ou sem estado, o Reliable Services fornece um ciclo de vida simples que permite conectar rapidamente seu código e começar.  Há apenas um ou dois métodos que você precisa tooimplement tooget seu serviço em funcionamento.

* **CreateServiceReplicaListeners/CreateServiceInstanceListeners** -este método é onde o serviço Olá define Olá pilha (s) comunicação que ele deseja toouse. Olá pilha de comunicação, como [API da Web](service-fabric-reliable-services-communication-webapi.md), é o que define Olá escutando do ponto de extremidade ou pontos de extremidade para Olá serviço (como clientes acessar o serviço de saudação). Ele também define como as mensagens de saudação aparecem interagem com rest Olá Olá do código de serviço.
* **RunAsync** -esse método é onde o serviço é executado em sua lógica de negócios e onde ele seria iniciar as tarefas em segundo plano que devem ser executado pelo tempo de vida de saudação do serviço de saudação. token de cancelamento Olá fornecido é um sinal para quando o trabalho deve parar. Por exemplo, se o serviço Olá precisa toopull mensagens fora de uma fila confiável e processá-las, isso é onde acontece que funcionam.

Se você estiver aprendendo sobre serviços confiáveis para Olá primeira vez, continue lendo! Se você estiver procurando uma explicação detalhada de saudação do ciclo de vida de serviços confiáveis, você pode head muito sobre[neste artigo](service-fabric-reliable-services-lifecycle.md).

## <a name="example-services"></a>Exemplo de serviços
Conhecer o modelo de programação, vamos dar uma olhada rápida nas duas toosee diferentes serviços como essas partes se encaixam.

### <a name="stateless-reliable-services"></a>Serviços Confiáveis sem estado
Um serviço sem monitoração de estado é aquele em que não há nenhum estado mantido dentro de um serviço de saudação em chamadas. Qualquer estado presente é totalmente descartável e não requer sincronização, replicação, persistência ou alta disponibilidade.

Por exemplo, considere um cálculo que não tem memória e recebe todas as tooperform de termos e as operações de uma só vez.

Nesse caso, Olá `RunAsync()` (c#) ou `runAsync()` (Java) de saudação serviço pode estar vazio, porque não há nenhum plano de fundo desse serviço de saudação do processamento de tarefa necessidades toodo. Quando o serviço de cálculo de saudação é criado, ele retorna um `ICommunicationListener` (c#) ou `CommunicationListener` (Java) (por exemplo [API da Web](service-fabric-reliable-services-communication-webapi.md)) que abre um ponto de extremidade escutando em alguma porta. Esse ponto de extremidade de escutando conecta os métodos de cálculo diferente toohello (exemplo: "Adicionar (n1, n2)") que definem a API pública da Calculadora hello.

Quando é feita uma chamada de um cliente, método apropriado de saudação é chamado e serviço da Calculadora Olá executa operações de saudação em Olá dados fornecida e retorna o resultado de saudação. O estado não é armazenado.

Não armazenar nenhum estado interno torna este exemplo de calculadora muito simples. Mas a maioria dos serviços não é realmente sem estado. Em vez disso, eles Externalizar toosome seu estado outro repositório. (Por exemplo, qualquer aplicativo Web que depende da manutenção do estado de sessão em um repositório de backup ou do cache não é sem estado.)

Um exemplo comum de serviços como sem monitoração de estado são usados na malha do serviço é como um front-end que expõe Olá API público para um aplicativo web. serviço de front-end Hello, em seguida, fala toostateful serviços toocomplete uma solicitação de usuário. Nesse caso, chamadas de clientes são direcionado tooa conhecido de porta, por exemplo, 80, onde o serviço sem monitoração de estado hello está escutando. Esse serviço sem monitoração de estado receber chamada hello e determina se a chamada de saudação é de um terceiro confiável e que o serviço é destinado.  Em seguida, serviço sem monitoração de estado Olá encaminha a partição correta do hello chamada toohello do serviço com monitoração de estado hello e aguarda uma resposta. Quando o serviço sem monitoração de estado Olá recebe uma resposta, ele responde cliente original toohello. Veja um exemplo de um serviço como esse em nossas amostras de [C#](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started) / [Java](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Actors/VisualObjectActor/VisualObjectWebService). Isso é apenas um exemplo desse padrão nos exemplos hello, há outras também outros exemplos.

### <a name="stateful-reliable-services"></a>Serviços Confiáveis com estado
Um serviço com monitoração de estado é aquele que deve ter alguma parte do estado mantido consistente e presentes para Olá toofunction de serviço. Considere um serviço que calcula constantemente uma média móvel de algum valor com base em atualizações que recebe. toodo isso, ele deve ter Olá o conjunto atual de solicitações de entrada precisa tooprocess e Olá média atual. Qualquer serviço que recupera, processa e armazena informações em um repositório externo (como um repositório de tabelas ou blob do Azure) é um serviço com estado. Ele simplesmente mantém seu estado no armazenamento de estado externo de saudação.

A maioria dos serviços hoje armazenar seu estado externamente, como armazenamento externo de saudação é o que fornece confiabilidade, disponibilidade, escalabilidade e a consistência de estado. Serviços no serviço de malha, não é necessária toostore seu estado externamente. Service Fabric cuida desses requisitos para o código de saudação do serviço e o estado do serviço hello.

> [!NOTE]
> O suporte para Reliable Services com estado ainda não está disponível no Linux (para C# ou Java).
>

Vamos dizer que desejamos toowrite um serviço que processa imagens. toodo isso, Olá serviço aceita uma série de imagem e hello de conversões tooperform na imagem. Este serviço retorna um ouvinte de comunicação (suponhamos que é uma WebAPI) que expõe uma API como `ConvertImage(Image i, IList<Conversion> conversions)`. Quando ele recebe uma solicitação, o serviço de saudação armazena em um `IReliableQueue`e retorna algum cliente toohello de id para que ele possa rastrear solicitação hello.

Nesse serviço, `RunAsync()` poderia ser mais complexo. Olá serviço contém um loop dentro de seu `RunAsync()` que recebe solicitações de `IReliableQueue` e executa conversões Olá solicitados. resultados de saudação ficam armazenados em um `IReliableDictionary` para que quando o cliente de saudação volta a ficar obter suas imagens convertidas. tooensure ou até mesmo se algo falhar imagem Olá não seja perdido, esse serviço confiável seria retirar fila hello, executam conversões de saudação e armazenar o resultado de saudação tudo em uma única transação. Nesse caso, mensagem de saudação é removida da fila de saudação e resultados de saudação são armazenados no dicionário de resultado Olá somente quando conversões Olá forem concluídas. Como alternativa, serviço Olá pôde pull imagem Olá fora da fila de saudação e imediatamente armazená-lo em um repositório remoto. Isso reduz a saudação valor do estado Olá serviço tem toomanage, mas aumenta a complexidade como serviço Olá tem tookeep Olá necessário toomanage Olá remoto repositório de metadados de. Com essa abordagem, se algo Falha na solicitação de meio Olá Olá permanece no hello fila aguardando toobe processado.

Um toonote coisa sobre esse serviço é que parece um serviço .NET normal! Olá única diferença é que as estruturas de dados hello está sendo usada (`IReliableQueue` e `IReliableDictionary`) são fornecidas pelo serviço de malha e altamente confiáveis, disponíveis e consistentes.

## <a name="when-toouse-reliable-services-apis"></a>Quando toouse confiável APIs de serviços
Se qualquer um dos seguintes Olá caracterizam as necessidades do serviço de aplicativo, você deve considerar confiável APIs de serviços:

* Você deseja o código do serviço (e, opcionalmente, estado) toobe confiável e altamente disponível
* Você precisa de garantias transacionais entre várias unidades de estado (por exemplo, pedidos e itens de linha do pedido).
* O estado do aplicativo pode ser modelado naturalmente como Filas e Dicionários Confiáveis.
* O código de aplicativos ou o estado precisa toobe altamente disponível com baixa latência leituras e gravações.
* Seu aplicativo precisa de simultaneidade de saudação toocontrol ou granularidade de operações realizadas em uma ou mais coleções confiável.
* Você deseja toomanage comunicações de saudação ou Olá controle esquema para o serviço de particionamento.
* Seu código precisa de um ambiente de tempo de execução de thread livre.
* Seu aplicativo precisa toodynamically criar ou destruir dicionários confiável ou filas ou serviços inteiros em tempo de execução.
* É necessário tooprogrammatically fornecida pelo Service Fabric backup e restauração recursos de controle para o estado do serviço.
* Seu aplicativo precisa toomaintain histórico de alterações para suas unidades de estado.
* Deseja toodevelop ou consumir provedores de estado personalizado, desenvolvido por parte de terceiros.

## <a name="next-steps"></a>Próximas etapas
* [Início Rápido dos Serviços Confiáveis](service-fabric-reliable-services-quick-start.md)
* [Uso avançado de Reliable Services](service-fabric-reliable-services-advanced-usage.md)
* [modelo de programação Olá Reliable Actors](service-fabric-reliable-actors-introduction.md)
