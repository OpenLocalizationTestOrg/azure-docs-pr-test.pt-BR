---
title: aaaLearn terminologia do Azure Service Fabric | Microsoft Docs
description: "Uma visão geral da terminologia do Service Fabric. Descreve conceitos chave terminologia e termos usados no restante de saudação da documentação de saudação."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: chackdan;subramar
ms.assetid: 3a970679-e19e-43b3-9be8-71773f307c57
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/02/2017
ms.author: ryanwi
ms.openlocfilehash: 4781fc0527b8a58e534183249bc2759aded2730b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-terminology-overview"></a>Visão geral da terminologia do Service Fabric
O Service Fabric é uma plataforma de sistemas distribuídos que torna mais fácil toopackage, implantar e gerenciar microservices escalonável e confiável. Esta terminologia de saudação de detalhes tópico usada pelo Service Fabric toounderstand Olá termos usados na documentação de saudação.

Olá conceitos listados nesta seção também são discutidos no hello seguintes vídeos do Microsoft Virtual Academy: <a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965">conceitos principais</a>, <a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tlkI046yC_2906218965">conceitos de tempo de Design</a>, e <a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=x7CVH56yC_1406218965">deconceitosdetempodeexecução</a>.

## <a name="infrastructure-concepts"></a>Conceitos de infraestrutura
**Cluster**: um conjunto de máquinas físicas ou virtuais conectadas em rede, no qual os microsserviços são implantados e gerenciados.  Clusters podem ser dimensionado toothousands de máquinas.

**Nó**: uma máquina ou VM que faz parte de um cluster é chamado de nó. Cada nó recebe um nome de nó (uma cadeia de caracteres). Os nós têm características como propriedades de posicionamento. Cada máquina ou VM tem um serviço do Windows de início automático, `FabricHost.exe` que começa a ser executado na inicialização e então inicia dois executáveis: `Fabric.exe` e `FabricGateway.exe`. Esses dois executáveis compõem o nó de saudação. Para cenários de teste, você pode hospedar vários nós em um único computador ou VM, executando várias instâncias do `Fabric.exe` e do `FabricGateway.exe`.

## <a name="application-concepts"></a>Conceitos de aplicativo
**Tipo de aplicativo**: Olá nome/versão atribuída tooa coleção de tipos de serviço. Definido em um `ApplicationManifest.xml` de arquivo, inserido em um diretório do pacote de aplicativo, que é, em seguida, copiado o repositório de imagens do cluster do Service Fabric toohello. Você pode criar um aplicativo nomeada deste tipo de aplicativo no cluster hello.

Saudação de leitura [modelo de aplicativo](service-fabric-application-model.md) artigo para obter mais informações.

**Pacote de aplicativo**: um diretório de disco que contém o tipo de aplicativo a saudação `ApplicationManifest.xml` arquivo. Referências Olá pacotes de serviço para cada tipo de serviço que compõe o tipo de aplicativo hello. arquivos Olá no diretório do pacote de aplicativo hello são repositório de imagens do cluster de malha tooService copiado. Por exemplo, um pacote de aplicativo para um tipo de aplicativo de email pode conter um pacote de serviço do banco de dados, um pacote de serviço front-end e pacote de serviço de fila de tooa de referências.

**Aplicativo de chamada**: depois de um pacote de aplicativo é copiado toohello repositório de imagens, você cria uma instância de aplicativo hello em cluster Olá especificando um tipo de aplicativo do pacote de aplicativo hello (usando seu nome/versão). Cada instância do tipo de aplicativo é atribuído a um nome URI com esta aparência: `"fabric:/MyNamedApp"`. Em um cluster, você pode criar vários aplicativos nomeados a partir de um tipo de aplicativo único. Você também pode criar aplicativos nomeados a partir de diferentes tipos de aplicativos. Cada aplicativo nomeado é gerenciado e possui controle de versão independente.      

**Tipo de serviço**: Olá nome/versão atribuído pacotes de códigos, pacotes de dados e pacotes de configuração do serviço tooa. Definido em um `ServiceManifest.xml` arquivo, incorporado em um diretório do pacote de serviço e o diretório do pacote de serviço hello, em seguida, é referenciado por um pacote de aplicativo `ApplicationManifest.xml` arquivo. Em cluster hello, depois de criar um aplicativo nomeado, você pode criar um serviço nomeado de uma saudação tipos de serviço do tipo de aplicativo. Olá do tipo de serviço `ServiceManifest.xml` arquivo descreve serviço hello.

Saudação de leitura [modelo de aplicativo](service-fabric-application-model.md) artigo para obter mais informações.

Há dois tipos de serviço:

* **Sem monitoração de estado:** usar um serviço sem monitoração de estado quando o estado persistente do serviço Olá é armazenado em um serviço de armazenamento externo, como o armazenamento do Azure, banco de dados SQL ou banco de dados do Azure Cosmos. Use um serviço sem monitoração de estado quando o serviço de saudação não tem nenhum armazenamento persistente em todos os. Por exemplo, um serviço da Calculadora onde os valores são transmitidos toohello serviço, uma computação é executada usando esses valores, e um resultado é retornado.
* **Monitoração de estado:** usar um serviço com monitoração de estado quando desejar toomanage de malha do serviço de estado do serviço por meio de suas coleções confiável ou Reliable Actors modelos de programação. Especifique quantas partições você deseja toospread seu estado de failover (para escalabilidade) quando criar um serviço nomeado. Também especifique quantas vezes tooreplicate seu estado em nós (para confiabilidade). Cada serviço nomeado tem uma única réplica primária e várias réplicas secundárias. Modificar o estado do serviço nomeado gravando a réplica primária toohello. Malha do serviço, depois, replica esse estado tooall Olá réplicas secundárias mantendo seu estado em sincronia. Serviço de malha detecta automaticamente quando uma réplica primária falha e promove uma réplica primária do réplica secundária tooa existente. O Service Fabric cria então uma nova réplica secundária.  

**Pacote de serviço**: um diretório de disco que contém o tipo de serviço a saudação `ServiceManifest.xml` arquivo. Esse arquivo faz referência a código hello, dados estáticos e pacotes de configuração para o tipo de serviço hello. arquivos Olá no diretório do pacote de serviço Olá são referenciados por tipo de aplicativo a saudação `ApplicationManifest.xml` arquivo. Por exemplo, um pacote de serviço pode se referir a código toohello, dados estáticos e pacotes de configuração que compõem um serviço de banco de dados.

**Chamada de serviço**: depois de criar um aplicativo nomeada, você pode criar uma instância de um de seus tipos de serviço em cluster Olá especificando o tipo de serviço da saudação (usando seu nome/versão). Cada instância de tipo de serviço recebe um nome de URI com escopo dentro do URI de seu aplicativo nomeado. Por exemplo, se você criar uma chamada de serviço dentro de um aplicativo de chamada "MyNamedApp" "MyDatabase", Olá URI é parecido com: `"fabric:/MyNamedApp/MyDatabase"`. Dentro de um aplicativo nomeado, você pode criar vários serviços nomeados. Cada serviço nomeado pode ter seu próprio esquema de partição e contagens de instância/réplica.

**Pacote de código**: um diretório de disco que contém arquivos executáveis do tipo de serviço hello (normalmente, arquivos DLL/EXE). arquivos Olá no diretório do pacote de código Olá são referenciados por tipo de serviço a saudação `ServiceManifest.xml` arquivo. Quando um serviço nomeado é criado, pacote de códigos de saudação é copiado toohello nó ou Olá toorun selecionado de nós denominado service. Em seguida, código de saudação começa a ser executado. Há dois tipos de arquivos executáveis de pacote de códigos:

* **Executáveis de convidado**: arquivos executáveis que são executados como-está no sistema de operacional de host hello (Windows ou Linux). Ou seja, esses executáveis não referência de tooor de link não os arquivos de tempo de execução do Service Fabric e, portanto, não usam quaisquer modelos de programação do Service Fabric. Esses executáveis são toouse não é possível que alguns recursos de malha do serviço como Olá naming service para a descoberta de ponto de extremidade. Executáveis de convidado não podem relatar carga métricas tooeach específico a instância do serviço.
* **Executáveis de Host de serviço**: arquivos executáveis que usam o Service Fabric modelos de programação por meio da vinculação tooService arquivos de tempo de execução de malha, habilitando recursos de malha do serviço. Por exemplo, uma instância de serviço nomeada pode registrar pontos de extremidade com o Serviço de Nomenclatura do Service Fabric, e também pode relatar métricas de carga.      

**Pacote de dados**: um diretório de disco que contém arquivos de dados estáticos, somente leitura do tipo de serviço hello (normalmente fotos, vídeo e áudio arquivos). arquivos Olá no diretório do pacote de dados de saudação são referenciados por tipo de serviço a saudação `ServiceManifest.xml` arquivo. Quando um serviço nomeado é criado, o pacote de dados de saudação está nó toohello copiado ou Olá toorun selecionado de nós denominado service.  código de saudação começa a ser executado e agora pode acessar arquivos de dados de saudação.

**Pacote de configuração**: um diretório de disco que contém estático do tipo de serviço hello, arquivos de configuração de somente leitura (geralmente arquivos de texto). arquivos Olá no diretório do pacote de configuração de saudação são referenciados por tipo de serviço a saudação `ServiceManifest.xml` arquivo. Quando um serviço nomeado é criado, arquivos Olá no pacote de configuração de saudação são copiado toohello um ou mais Olá toorun selecionado de nós denominada serviço. Em seguida, o código de Olá começa a ser executado e agora pode acessar os arquivos de configuração de saudação.

**Contêineres**: por padrão, o Service Fabric implanta e ativa esses serviços como processos. O Service Fabric também pode implantar serviços em imagens de contêiner. Contêineres são uma tecnologia de virtualização que virtualiza a saudação de sistema operacional subjacente de aplicativos. Um aplicativo e suas bibliotecas de tempo de execução, dependências e sistema são executados dentro de um contêiner com exibição de contêiner próprio isolada toohello acesso completo, privada construções do sistema operacional. O Service Fabric dá suporte a contêineres do Docker em contêineres Linux e Windows Server.  Para obter mais informações, leia [Service Fabric e contêineres](service-fabric-containers-overview.md).

**Esquema de Partição**: ao criar um serviço nomeado, você especifica um esquema de partição. Serviços com grandes quantidades de estado dividir os dados de saudação em partições que se espalha estado Olá em nós do cluster hello. Isso permite que tooscale de estado do serviço nomeado. Dentro de uma partição, serviços nomeados sem estado têm instâncias, enquanto serviços nomeados com estado têm réplicas. Normalmente, os serviços nomeadas sem estado têm apenas uma partição, já que não têm estado interno. instâncias de partição Olá fornecem disponibilidade; Se uma instância falhar, outras instâncias continuam toooperate normalmente e, em seguida, o Service Fabric criará uma nova instância. Monitoração de estado chamada de serviços mantêm seu estado em réplicas e cada partição tem sua própria réplica definida com todos os estados de saudação sendo mantidos em sincronia. Uma réplica falhar, o Service Fabric cria uma nova réplica de réplicas existentes Olá.

Saudação de leitura [serviços confiáveis partição Service Fabric](service-fabric-concepts-partitioning.md) artigo para obter mais informações.

## <a name="system-services"></a>Serviços do sistema
Há serviços de sistema que são criados em cada cluster que fornecem recursos de plataforma de saudação do Service Fabric.

**Serviço de nomenclatura**: cluster de cada estrutura de serviço tem um serviço de nomeação, que resolve o local de tooa de nomes do serviço em cluster hello. Gerenciar propriedades e nomes de serviço hello, tooan semelhante internet serviço DNS (Domain Name) de cluster de saudação. Os clientes se comunicam com segurança com qualquer nó no cluster hello usando Olá Naming Service tooresolve um nome de serviço e sua localização.  Mover aplicativos em cluster Olá por exemplo devido toofailures, balanceamento de recursos ou Olá redimensionamento de cluster hello. Você pode desenvolver serviços e clientes que resolver o local de rede atual hello. Os clientes obtêm o endereço IP de máquina real hello e a porta em que ele está sendo executado.

Leitura [comunicação com serviços](service-fabric-connect-and-communicate-with-services.md) para mais informações sobre comunicação Olá cliente e serviço APIs que funcionam com hello Naming service.

**Serviço de Repositório de Imagens**: cada cluster do Service Fabric tem um serviço de Repositório de Imagens em que os pacotes de aplicativos implantados com versão são mantidos. Copiar um pacote de aplicativo toohello Image Store e, em seguida, registrar o tipo de aplicativo hello contido dentro desse pacote de aplicativo. Depois que o tipo de aplicativo hello for provisionado, você cria um aplicativo nomeado dele. Você pode cancelar o registro de um tipo de aplicativo de saudação serviço de repositório de imagem após a exclusão de todos os seus aplicativos nomeados.

Leitura [entender a configuração de ImageStoreConnectionString saudação](service-fabric-image-store-connection-string.md) para obter mais informações sobre Olá serviço de repositório de imagens.

Saudação de leitura [implantar um aplicativo](service-fabric-deploy-remove-applications.md) artigo para obter mais informações sobre como implantar o serviço de armazenamento de aplicativos toohello imagem.

## <a name="built-in-programming-models"></a>Modelos de programação internos
Modelos de programação do .NET Framework estão disponíveis para você, os serviços do Service Fabric toobuild:

**Serviços confiáveis**: serviços de com e sem monitoração de toobuild de uma API. O serviço com estado armazena seu estado em Reliable Collections (como um dicionário ou uma fila). Você também pode obter tooplug em várias pilhas de comunicação, como a API da Web e o Windows Communication Foundation (WCF).

**Reliable Actors**: os objetos uma API com e sem monitoração de toobuild por meio do modelo de programação de ator virtual hello. Esse modelo pode ser útil quando você tem muitas unidades independentes de computação/estado. Como esse modelo usa um modelo de threading por sua vez, é melhor tooavoid o código que chama tooother atores ou serviços como um ator individual não pode processar outras solicitações de entrada até que tem concluído todas as suas solicitações de saída.

Saudação de leitura [escolha um modelo de programação para o serviço](service-fabric-choose-framework.md) artigo para obter mais informações.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre o serviço de malha:

* [Visão geral da Malha do Serviço](service-fabric-overview.md)
* [Por que um microservices abordagem toobuilding aplicativos?](service-fabric-overview-microservices.md)
* [Cenários de aplicativos](service-fabric-application-scenarios.md)

