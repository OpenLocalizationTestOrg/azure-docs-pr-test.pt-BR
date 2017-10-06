---
title: aaaIntroduction tooAzure armazenamento | Microsoft Docs
description: "Uma visão geral do armazenamento do Azure, armazenamento de dados on-line da Microsoft na nuvem hello. Saiba como toouse Olá melhor solução de armazenamento de nuvem disponíveis em seus aplicativos."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: a4a1bc58-ea14-4bf5-b040-f85114edc1f1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/26/2017
ms.author: marsma
ms.openlocfilehash: dec8280c77f4b23df4c2a471e1d755e365c14e58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toomicrosoft-azure-storage"></a>Introdução tooMicrosoft armazenamento do Azure

## <a name="overview"></a>Visão geral
Armazenamento do Azure é uma solução de armazenamento de nuvem Olá para aplicativos modernos que dependem de durabilidade, disponibilidade e escalabilidade toomeet Olá de seus clientes. Lendo este artigo, os desenvolvedores, profissionais de TI e responsáveis por decisões de negócios podem aprender sobre:

* O que é o Armazenamento do Azure e como você pode tirar proveito dele em aplicativos de nuvem, móveis, de servidor e de área de trabalho
* Os tipos de dados que você pode armazenar com os serviços de armazenamento do Azure Olá: blob de dados (objeto), dados da tabela NoSQL, fila de mensagens e compartilhamentos de arquivos.
* Como acessar dados de tooyour no armazenamento do Azure são gerenciados
* Como os dados do armazenamento do Azure tornam-se duráveis por meio de redundância e replicação
* Onde toobuild próximo toogo seu primeiro aplicativo de armazenamento do Azure

<!-- after our quick starts are available, replace this link with a link tooone of those. 
Had tooremove this article, it refers toohello VS quickstarts, and they've stopped publishing them. Robin --> 
<!-- tooget up and running with Azure Storage quickly, see [Get started with Azure Storage in five minutes](storage-getting-started-guide.md). -->

Para obter detalhes sobre ferramentas, bibliotecas e outros recursos para trabalhar com o armazenamento do Azure, confira as [Próximas etapas](#next-steps) abaixo.

## <a name="what-is-azure-storage"></a>O que é o armazenamento do Azure?
A computação na nuvem habilita novos cenários para aplicativos, que exigem armazenamento escalonável, durável e altamente disponível para seus dados - que é exatamente o motivo pelo qual a Microsoft desenvolveu o Armazenamento do Azure. Em adição toomaking-possível para os desenvolvedores toobuild aplicativos em larga escala toosupport novos cenários, o armazenamento do Azure também fornece Olá armazenamento base para máquinas virtuais do Azure, um ainda mais potente de tooits comprovação.

Armazenamento do Azure é altamente escalonável, portanto você pode armazenar e processar centenas de terabytes de cenários de dados grandes de dados toosupport Olá exigidos pela análise científica financeiro e aplicativos de mídia. Ou você pode armazenar Olá pequenas quantidades de dados necessários para um site de pequenas empresas. Sempre que se enquadram às suas necessidades, você paga somente para dados Olá que estiver armazenando. O Armazenamento do Azure atualmente armazena dezenas de trilhões de objetos exclusivos de clientes e manipula milhões de solicitações por segundo em média.

Armazenamento do Azure é Elástico, você pode projetar aplicativos para um público global grande e dimensionar os aplicativos conforme necessário - ambos em relação à quantidade de saudação dos dados armazenados e Olá o número de solicitações feitas em relação a ela. Você paga apenas pelo que usa e apenas quando usa.

O Armazenamento do Azure usa um sistema de particionamento automático que faz o balanço automático da carga de seus dados com base no tráfego. Isso significa que como demandas de saudação em aumentar seu aplicativo, o armazenamento do Azure automaticamente aloca Olá os recursos adequados toomeet-los.

Armazenamento do Azure é acessível a partir de qualquer lugar no Olá mundo, de qualquer tipo de aplicativo, se ele está em execução na nuvem hello, na área de trabalho hello, em um servidor local ou em um celular ou dispositivo tablet. Você pode usar o armazenamento do Azure em cenários móveis onde o aplicativo hello armazena um subconjunto de dados no dispositivo hello e sincroniza com um conjunto completo de dados armazenados na nuvem hello.

O Armazenamento do Azure dá suporte a clientes que usam um conjunto variado de sistemas operacionais (inclusive o Windows e o Linux) e uma variedade de linguagens de programação (incluindo .NET, Java, Node.js, Python, Ruby, PHP e C++ e linguagens de programação móveis) para tornar o desenvolvimento conveniente. Armazenamento do Azure também expõe os recursos de dados por meio de APIs REST simples, que estão disponíveis tooany cliente capaz de enviar e receber dados via HTTP/HTTPS.

O Armazenamento premium do Azure dá suporte a disco de alto desempenho e baixa latência para cargas de trabalho com uso intenso de entrada e saída em execução em máquinas virtuais do Azure. Com o armazenamento do Azure Premium, você pode anexar várias tooa de discos de dados persistentes máquina virtual e configurá-los toomeet seus requisitos de desempenho. Cada disco de dados é apoiado por um disco SSD no Armazenamento premium do Azure para máximo desempenho de entrada e saída. Para obter mais detalhes, confira [Armazenamento Premium: armazenamento de alto desempenho para as cargas de trabalho das máquinas virtuais do Azure](storage-premium-storage.md) .

## <a name="introducing-hello-azure-storage-services"></a>Serviços de armazenamento do Azure apresentando Olá
Armazenamento do Azure fornece Olá quatro serviços a seguir: armazenamento de Blob, o armazenamento de tabela, armazenamento de fila e o armazenamento de arquivos.

* O Armazenamento de Blobs armazena dados de objeto não estruturados. Um blob pode ser qualquer tipo de texto ou dados binários, como um documento, um arquivo de mídia ou um instalador do aplicativo. Armazenamento de blob também é chamado tooas armazenamento de objeto.
* O Armazenamento de Tabelas armazena conjuntos de dados estruturados. Armazenamento de tabela é um repositório de dados do atributo de chave NoSQL, que permite o desenvolvimento rápido e quantidades de toolarge acesso rápido de dados.
* O Armazenamento de Filas fornece um sistema confiável de mensagens para processamento de fluxo de trabalho e para comunicação entre componentes dos serviços de nuvem.
* Armazenamento de arquivos oferece armazenamento compartilhado para aplicativos herdados que usam protocolo SMB padrão de saudação. Serviços de nuvem e máquinas virtuais do Azure podem compartilhar dados de arquivo entre componentes de aplicativos por meio de compartilhamentos montados e aplicativos locais podem acessar dados de arquivo em um compartilhamento via Olá API REST do serviço de arquivo.

Uma conta de armazenamento do Azure é uma conta de segurança que lhe dá acesso tooservices no armazenamento do Azure. Sua conta de armazenamento fornece um namespace exclusivo Olá para seus recursos de armazenamento. imagem de saudação abaixo mostra as relações de saudação entre os recursos de armazenamento do Azure Olá em uma conta de armazenamento:

![Recursos de Armazenamento do Azure](./media/storage-introduction/storage-concepts.png)

[!INCLUDE [storage-account-types-include](../../includes/storage-account-types-include.md)]

[!INCLUDE [storage-versions-include](../../includes/storage-versions-include.md)]

## <a name="blob-storage"></a>Armazenamento de blob
Para usuários com grandes quantidades de toostore de dados não estruturados objeto na nuvem hello, armazenamento de Blob oferece uma solução econômica e dimensionável. Você pode usar o conteúdo de toostore de armazenamento de Blob, como:

* Documentos
* Dados sociais, como fotos, vídeos, música e blogs
* Backups de arquivos, computadores, bancos de dados e dispositivos
* Imagens e texto para aplicativos web
* Dados de configuração de aplicativos de nuvem
* Big data, como logs e outros grandes conjuntos de dados

Cada blob é organizado em um contêiner. Os contêineres fornecem também um toogroups de políticas de segurança de tooassign maneira útil de objetos. Uma conta de armazenamento pode conter qualquer número de contêineres e um contêiner pode conter qualquer número de blobs, o limite de capacidade de 500 TB toohello Olá da conta de armazenamento.

O armazenamento de blobs oferece três tipos de blobs: blob de blocos, blob de anexo e blob de páginas (discos).

* Os blobs de blocos são otimizados para streaming e armazenamento de objetos de nuvem e são uma boa opção para armazenar documentos, arquivos de mídia, backups etc.
* Acrescentar blobs são blobs de tooblock semelhantes, mas são otimizados para operações de acréscimo. Um blob de acréscimo pode ser atualizado apenas adicionando um novo end toohello bloco. Acrescentar blobs são uma boa escolha para cenários como registrar em log, em que novos dados precisam toobe gravada somente toohello final do blob hello.
* Blobs de página são otimizados para que representam os discos de IaaS e suporte aleatório grava e pode ser up too1 TB de tamanho. Um disco de IaaS anexado a uma rede de máquinas virtuais do Azure é um VHD armazenado como um blob de página.

Para grandes conjuntos de dados onde as restrições de rede fazer carregamento ou download de armazenamento tooBlob de dados em transmissão de saudação irreal, você pode enviar um tooimport tooMicrosoft de unidade de disco rígido ou exportar dados diretamente do Centro de dados de saudação. Consulte [usar Olá serviço de importação/exportação do Microsoft Azure tooTransfer dados tooBlob armazenamento](storage-import-export-service.md).

## <a name="table-storage"></a>Armazenamento de tabela

[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

Os aplicativos modernos geralmente demandam armazenamento de dados com maior escalabilidade e flexibilidade que as gerações anteriores de software exigiam. Armazenamento de tabela oferece armazenamento altamente disponível e altamente escalonável, para que seu aplicativo pode dimensionar automaticamente toomeet demanda do usuário. O armazenamento de tabelas é um armazenamento de chaves/atributos NoSQL da Microsoft - tem um design sem esquema, o que o torna diferente dos bancos de dados relacionais tradicionais. Com um repositório de dados schemaless, é fácil tooadapt seus dados como Olá precisam de evolve seu aplicativo. Armazenamento de tabela é fácil toouse, para que os desenvolvedores podem criar aplicativos rapidamente. Acesso toodata é rápida e econômica para todos os tipos de aplicativos.  O armazenamento de tabela normalmente tem um custo significativamente mais baixo do que o SQL tradicional para volumes de dados semelhantes.

O armazenamento de tabela é um repositório de chave-atributo, o que significa que cada valor em uma tabela é armazenado com um nome de propriedade. nome da propriedade Olá pode ser usado para filtragem e especificar critérios de seleção. Um conjunto de propriedades e seus valores compõem uma entidade. Como o armazenamento de tabela é schemaless, duas entidades no hello mesmo tabela pode conter diferentes conjuntos de propriedades e as propriedades podem ser de tipos diferentes.

Você pode usar a tabela armazenamento toostore flexíveis conjuntos de dados, como dados de usuário para aplicativos web, catálogos de endereços, informações de dispositivo e qualquer outro tipo de metadados que o serviço requer.  Você pode armazenar qualquer número de entidades em uma tabela, e uma conta de armazenamento pode conter qualquer número de tabelas, o limite de capacidade toohello Olá da conta de armazenamento.

Como Blobs e filas, os desenvolvedores podem gerenciar e acessar o armazenamento de tabela usando protocolos padrão de REST, no entanto armazenamento de tabela também oferece suporte a um subconjunto do protocolo do OData hello, simplificando a consultar recursos avançados e habilitando JSON e AtomPub (com base em XML) formatos.

Para aplicativos baseados na Internet de hoje, bancos de dados NoSQL como armazenamento de tabela oferecem um tootraditional alternativo popular bancos de dados relacionais.

## <a name="queue-storage"></a>Armazenamento de filas
Na criação de aplicativos para escala, os componentes do aplicativo geralmente são desassociados, para que possam ser redimensionados independentemente. Armazenamento de fila fornece uma solução de mensagens confiável para comunicação assíncrona entre componentes de aplicativos, quer eles estejam em execução na nuvem hello, na área de trabalho hello, em um servidor local ou em um dispositivo móvel. O Armazenamento de fila também oferece suporte ao gerenciamento de tarefas assíncronas e à criação de fluxos de trabalho do processo.

Uma conta de armazenamento pode conter qualquer número de filas. Uma fila pode conter qualquer número de mensagens, o limite de capacidade toohello Olá da conta de armazenamento. Mensagens individuais podem ser backup too64 KB de tamanho.

## <a name="file-storage"></a>Armazenamento de arquivos
Olá serviço arquivos do Azure permite que você tooset a compartilhamentos de arquivos de rede altamente disponível que podem ser acessados usando o protocolo de bloco de mensagens de servidor (SMB) padrão da saudação. Que significa que podem ser compartilhados por várias VMs Olá mesmo arquivos com acesso de leitura e gravação. Você também pode ler arquivos de hello usando a interface REST de saudação ou bibliotecas de saudação do cliente de armazenamento.

Uma coisa que diferencia o armazenamento de arquivo do Azure dos arquivos em um compartilhamento de arquivos corporativo é que você pode acessar arquivos de saudação de qualquer lugar no mundo hello usando uma URL que aponta o arquivo toohello e inclui um token de acesso compartilhado (SAS) de assinatura. Você pode gerar tokens SAS; Eles permitem ativo privada de tooa de acesso específicos para um determinado período de tempo.

Os compartilhamentos de arquivos podem ser usados para muitos cenários comuns:

* Muitos aplicativos locais usam compartilhamentos de arquivos. Este recurso torna mais fácil toomigrate os aplicativos que compartilham dados tooAzure. Se você montar hello toohello de compartilhamento de arquivo mesma letra Olá de unidade local usada pelo aplicativo, parte de saudação do seu aplicativo que acessa o compartilhamento de arquivo hello deve funcionar com alterações mínimas, se houver.

* Os arquivos de configuração podem ser armazenados em um compartilhamento de arquivos e acessados de várias VMs. Ferramentas e utilitários usados por vários desenvolvedores em um grupo podem ser armazenados em um compartilhamento de arquivos, garantindo que todas as pessoas podem encontrá-los, e que usam Olá a mesma versão.

* Logs de diagnóstico, métricas e despejos de memória são apenas três exemplos de dados que podem ser gravados tooa compartilhamento de arquivos e processados ou analisados posteriormente.

Nesse momento, a autenticação baseada no Active Directory e acesso (ACLs) listas de controle não tem suporte, mas eles estarão em algum momento Olá futuras. Olá credenciais da conta de armazenamento são autenticação tooprovide usadas para compartilhamento de arquivos de toohello de acesso. Isso significa que qualquer pessoa com compartilhamento Olá montado terá o compartilhamento de toohello de acesso de leitura/gravação completa.

## <a name="access-tooblob-table-queue-and-file-resources"></a>Acesso tooBlob, recursos de tabela, fila e arquivo
Por padrão, somente Olá armazenamento proprietário da conta pode acessar recursos na conta de armazenamento hello. Para segurança de saudação dos seus dados, cada solicitação feita nos recursos em sua conta deve ser autenticada. A autenticação conta com um modelo de Chave Compartilhada. BLOBs também podem ser configurado toosupport a autenticação anônima.

Sua conta de armazenamento recebe duas chaves de acesso privadas na criação, que são usadas para autenticação. Ter duas chaves garante que o seu aplicativo permaneça disponível ao regenerar chaves Olá regularmente como uma prática comum de gerenciamento de chaves de segurança.

Se você precisar de recursos de armazenamento tooyour do acesso de usuários controlados tooallow, você pode criar uma assinatura de acesso compartilhado. Uma assinatura de acesso compartilhado (SAS) é um token que pode ser acrescentadas tooa URL permite recebido acesso tooa de recursos de armazenamento. Qualquer pessoa que possua o token Olá pode acessar o recurso de saudação aponta toowith permissões de saudação especifica, por período Olá que ele é válido. A partir da versão de 5/4/2015, o Armazenamento do Azure dá suporte a dois tipos de assinaturas de acesso compartilhado: SAS de serviço e SAS de conta.

delegados SAS do serviço Olá acessam o recurso de tooa em apenas um dos serviços de armazenamento Olá: Olá serviço Blob, fila, tabela ou arquivo.

Uma conta SAS delega tooresources de acesso em um ou mais dos serviços de armazenamento de saudação. Você pode delegar as operações de tooservice nível de acesso que não estão disponíveis com um serviço de SAS. Você também pode delegar acesso tooread, gravação e operações de exclusão em contêineres de blob, tabelas, filas e compartilhamentos de arquivos que não são permitidos com um serviço de SAS.

Finalmente, você pode especificar que um contêiner e seus blobs ou um blob específico estão disponíveis para acesso público. Quando você indica que um contêiner ou blob é público, qualquer pessoa pode lê-lo anonimamente. Nenhuma autenticação é necessária.  Os contêineres e blobs públicos são úteis para expor recursos, como mídia e documentos, que são hospedados em sites.  latência de rede toodecrease para um público global, você pode armazenar dados blob usados por sites de saudação do Azure CDN.

Confira [Usando Assinaturas de Acesso Compartilhado (SAS)](storage-dotnet-shared-access-signature-part-1.md) para saber mais sobre as assinaturas de acesso compartilhado. Consulte [gerenciar o acesso de leitura anônimo toocontainers e blobs](storage-manage-access-to-resources.md) e [autenticação para Olá serviços de armazenamento do Azure](https://msdn.microsoft.com/library/azure/dd179428.aspx) para obter mais informações sobre a conta de armazenamento de tooyour acesso seguro.

## <a name="replication-for-durability-and-high-availability"></a>Replicação para durabilidade e alta disponibilidade
dados de saudação em sua conta de armazenamento é sempre do Microsoft Azure replicados tooensure durabilidade e alta disponibilidade. Cópias de replicação nos seus dados Olá mesmo data center ou tooa segundo data center, dependendo da opção de replicação que você escolher. A replicação protege seus dados e preserva o seu aplicativo tempo em caso de saudação de falhas de hardwares temporárias. Se os dados forem replicados tooa segundo data center, que também protege os dados contra uma falha catastrófica no local primário hello.

A replicação garante que sua conta de armazenamento atende Olá [contrato de nível de serviço (SLA) para armazenamento](https://azure.microsoft.com/support/legal/sla/storage/) mesmo em face de saudação de falhas. Consulte Olá SLA para obter informações sobre o armazenamento do Azure garante a disponibilidade e durabilidade.

Quando você cria uma conta de armazenamento, você pode selecionar uma saudação as opções de replicação a seguir:

* **Armazenamento com redundância local (LRS).** O armazenamento com redundância local mantém três cópias dos seus dados. O LRS é replicado três vezes em um único data center, em uma única região. LRS protege seus dados contra falhas de hardware normais, mas não de falha de saudação de um único data center.

    O LRS é oferecido com desconto. Para durabilidade máxima, recomendamos que você utilize o armazenamento com redundância geográfica, descrito abaixo.
* **Armazenamento com redundância de zona (ZRS).** O armazenamento com redundância de zona mantém três cópias dos seus dados. O ZRS é replicado três vezes em duas instalações toothree, dentro de uma única região ou em duas regiões, fornecendo maior durabilidade do que o LRS. O ZRS assegura que seus dados irão durar em uma única região.

    O ZRS proporciona maior durabilidade que o LRS, todavia, para durabilidade máxima recomendamos que você utilize o armazenamento com redundância geográfica, descrito abaixo.

  > [!NOTE]
  > O ZRS está atualmente disponível apenas para blobs de blocos e tem suporte apenas nas versões de 14/02/2014 e posteriores.
  >
  > Depois que você criou sua conta de armazenamento e selecionado ZRS, não é possível convertê-la toouse tooany outro tipo de replicação, ou vice-versa.
  >
  >
* **Armazenamento com redundância geográfica (GRS)**. O GRS mantém seis cópias de seus dados. Com o GRS, seus dados são replicados três vezes dentro de região primária hello e também são replicados três vezes em uma região secundária centenas de milhas de distância região primária do hello, fornecendo Olá de nível mais alto de durabilidade. No evento de saudação de uma falha na região primária hello, o armazenamento do Azure será região secundária do failover toohello. O GRS assegura que seus dados serão duráveis em duas regiões separadas.

    Para obter informações sobre os pares primários e secundários por região, consulte [Regiões do Azure](https://azure.microsoft.com/regions/).
* **Armazenamento com redundância geográfica com acesso de leitura (RA-GRS)**. Armazenamento com redundância geográfica com acesso de leitura replica seu dados tooa secundário geográfica e também fornece acesso de leitura tooyour dados no local secundário hello. Armazenamento com redundância geográfica com acesso de leitura permite que você tooaccess seus dados de saudação primária ou local secundário hello, no evento de saudação que um único local torna-se indisponível. Armazenamento com redundância geográfica com acesso de leitura é a opção de padrão de saudação para sua conta de armazenamento por padrão quando você criá-lo.

  > [!IMPORTANT]
  > Você pode alterar como os dados são replicados após sua conta de armazenamento tiver sido criada, a menos que especificado o ZRS quando você criou a conta de saudação. No entanto, observe que você pode incorrer em uma transferência de dados adicionais se você mudar de LRS tooGRS ou RA-GRS de custo.
  >
  >

Consulte [Replicação de armazenamento do Azure](storage-redundancy.md) para obter mais detalhes sobre as opções de replicação de armazenamento.

Para informações sobre preços de replicação da conta de armazenamento, consulte [Preços de Armazenamento do Azure](https://azure.microsoft.com/pricing/details/storage/). Consulte [Regiões do Azure](https://azure.microsoft.com/regions/#services) para obter mais informações sobre quais serviços estão disponíveis em cada região.

Para obter detalhes arquitetônicos sobre a durabilidade com o armazenamento do Azure, consulte [SOSP Paper - Azure Storage: A Highly Available Cloud Storage Service with Strong](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).

## <a name="transferring-data-tooand-from-azure-storage"></a>Transferindo dados tooand do armazenamento do Azure
Você pode usar o blob de toocopy Olá AzCopy utilitário de linha de comando, arquivo e dados de tabela em sua conta de armazenamento ou em contas de armazenamento. Consulte [transferir dados com o utilitário de linha de comando AzCopy de hello](storage-use-azcopy.md) para obter mais informações.

AzCopy é criado sobre Olá [biblioteca de movimentação de dados do Azure](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/), que está atualmente disponível na visualização.

Olá serviço de importação/exportação do Azure fornece um maneira tooimport blob dados ou exportar dados de blob da conta de armazenamento por meio de um disco rígido enviado toohello data center do Azure. Para obter mais informações sobre Olá serviço de importação/exportação, consulte [usar Olá serviço de importação/exportação do Microsoft Azure tooTransfer dados tooBlob armazenamento](storage-import-export-service.md).

## <a name="pricing"></a>Preços
[!INCLUDE [storage-account-billing-include](../../includes/storage-account-billing-include.md)]

## <a name="storage-apis-libraries-and-tools"></a>APIs, bibliotecas e ferramentas de armazenamento
Os recursos do Armazenamento do Azure podem ser acessados por qualquer linguagem que possa fazer solicitações HTTP/HTTPS. Além disso, o Armazenamento do Azure oferece bibliotecas de programação para várias linguagens populares. Essas bibliotecas simplificam muitos aspectos do trabalho com o Armazenamento do Azure manipulando detalhes, como invocação síncrona e assíncrona, processamento em lotes de operações, gerenciamento de exceções, novas tentativas automáticas, comportamento operacional e assim por diante. Bibliotecas estão disponíveis para Olá idiomas a seguir e plataformas com outras pessoas em Olá pipeline:

### <a name="azure-storage-data-services"></a>Serviços de dados do Armazenamento do Azure
* [API REST dos Serviços de Armazenamento](http://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Biblioteca do Cliente de Armazenamento para .NET, Windows Phone e Windows Runtime](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [Biblioteca do Cliente de Armazenamento para C++](https://github.com/Azure/azure-storage-cpp)
* [Biblioteca do Cliente de Armazenamento para Java/Android](https://azure.microsoft.com/develop/java/)
* [Biblioteca do Cliente de Armazenamento para Node.js](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [Biblioteca do Cliente de Armazenamento para PHP](https://azure.microsoft.com/develop/php/)
* [Biblioteca do Cliente de Armazenamento para Ruby](https://azure.microsoft.com/develop/ruby/)
* [Biblioteca do Cliente de Armazenamento para Python](https://azure.microsoft.com/develop/python/)
* [Cmdlets de armazenamento para PowerShell 1.0](/powershell/module/azurerm.storage/#storage)

### <a name="azure-storage-management-services"></a>Serviços de gerenciamento de Armazenamento do Azure
* [Referência da API REST do Provedor de Recursos de Armazenamento](/rest/api/storagerp/)
* [Biblioteca do Cliente do Provedor de Recursos de Armazenamento para .NET](/dotnet/api/microsoft.azure.management.storage)
* [Cmdlets do Provedor de Recursos de Armazenamento para PowerShell 1.0](/powershell/module/azure.storage)
* [API REST do Gerenciamento de Serviços de Armazenamento (clássico)](https://msdn.microsoft.com/library/azure/ee460790.aspx)

### <a name="azure-storage-data-movement-services"></a>Serviços de movimentação de dados do Armazenamento do Azure
* [API REST do Serviço de Importação/Exportação do Armazenamento](storage-import-export-service.md)
* [Biblioteca do Cliente de Movimentação de Dados do Armazenamento para .NET](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/)

### <a name="tools-and-utilities"></a>Ferramentas e utilitários
* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) é um aplicativo autônomo gratuito da Microsoft que permite que você toowork visualmente com dados de armazenamento do Azure no Linux, Windows e macOS.
* [Ferramentas de Cliente do Armazenamento do Azure](storage-explorers.md)
* [SDKs e Ferramentas do Azure](https://azure.microsoft.com/tools/)
* [Emulador de Armazenamento do Azure](http://www.microsoft.com/download/details.aspx?id=43709)
* [PowerShell do Azure](/powershell/azure/overview)
* [Utilitário de linha de comando AzCopy](http://aka.ms/downloadazcopy)

## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre o armazenamento do Azure, explore esses recursos:

### <a name="documentation"></a>Documentação
* [Documentação do Armazenamento do Azure](https://azure.microsoft.com/documentation/services/storage/)
* [Criar uma conta de armazenamento](storage-create-storage-account.md)

<!-- after our quick starts are available, replace this link with a link tooone of those. 
Had tooremove this article, it refers toohello VS quickstarts, and they've stopped publishing them. Robin --> 
<!--* [Get started with Azure Storage in five minutes](storage-getting-started-guide.md)
-->

### <a name="for-administrators"></a>Para administradores
* [Usando o PowerShell do Azure com o Armazenamento do Azure](storage-powershell-guide-full.md)
* [Uso da CLI do Azure com o Armazenamento do Azure](storage-azure-cli.md)

### <a name="for-net-developers"></a>Para desenvolvedores do .NET
* [Introdução ao armazenamento de Blobs do Azure usando o .NET](storage-dotnet-how-to-use-blobs.md)
* [Introdução ao armazenamento de Tabelas do Azure usando o .NET](storage-dotnet-how-to-use-tables.md)
* [Introdução ao armazenamento de Fila do Azure usando o .NET](storage-dotnet-how-to-use-queues.md)
* [Introdução ao Armazenamento de Arquivos do Azure no Windows](storage-dotnet-how-to-use-files.md)

### <a name="for-javaandroid-developers"></a>Para desenvolvedores de Java/Android
* [Como toouse armazenamento de Blob do Java](storage-java-how-to-use-blob-storage.md)
* [Como toouse o armazenamento de tabela do Java](storage-java-how-to-use-table-storage.md)
* [Como toouse armazenamento de fila do Java](storage-java-how-to-use-queue-storage.md)
* [Como toouse armazenamento de arquivo do Java](storage-java-how-to-use-file-storage.md)

### <a name="for-nodejs-developers"></a>Para desenvolvedores do Node.js
* [Como toouse armazenamento de Blob do Node. js](storage-nodejs-how-to-use-blob-storage.md)
* [Como toouse o armazenamento de tabela do Node. js](storage-nodejs-how-to-use-table-storage.md)
* [Como toouse armazenamento de fila do Node. js](storage-nodejs-how-to-use-queues.md)

### <a name="for-php-developers"></a>Para desenvolvedores do PHP
* [Como toouse armazenamento de Blob do PHP](storage-php-how-to-use-blobs.md)
* [Como toouse o armazenamento de tabela do PHP](storage-php-how-to-use-table-storage.md)
* [Como toouse armazenamento de fila do PHP](storage-php-how-to-use-queues.md)

### <a name="for-ruby-developers"></a>Para desenvolvedores do Ruby
* [Como toouse armazenamento de Blob do Ruby](storage-ruby-how-to-use-blob-storage.md)
* [Como toouse o armazenamento de tabela do Ruby](storage-ruby-how-to-use-table-storage.md)
* [Como toouse armazenamento de fila do Ruby](storage-ruby-how-to-use-queue-storage.md)

### <a name="for-python-developers"></a>Para desenvolvedores do Python
* [Como toouse armazenamento de Blob do Python](storage-python-how-to-use-blob-storage.md)
* [Como toouse o armazenamento de tabela do Python](storage-python-how-to-use-table-storage.md)
* [Como toouse armazenamento de fila do Python](storage-python-how-to-use-queue-storage.md)
* [Como toouse armazenamento de arquivo do Python](storage-python-how-to-use-file-storage.md)
