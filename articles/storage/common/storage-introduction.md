---
title: aaaIntroduction tooAzure armazenamento | Microsoft Docs
description: "Introdução tooAzure armazenamento, o armazenamento de dados da Microsoft na nuvem hello."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: a4a1bc58-ea14-4bf5-b040-f85114edc1f1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: robinsh
ms.openlocfilehash: f61324f98d0a8eb24023e4344acdb4ca58bb27f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
<!-- this is hello same version that is in hello MVC branch -->
# <a name="introduction-toomicrosoft-azure-storage"></a>Introdução tooMicrosoft armazenamento do Azure

Armazenamento do Microsoft Azure é um serviço de nuvem gerenciado pela Microsoft que fornece armazenamento altamente disponível, seguro, durável, escalonável e redundante. A Microsoft cuida da manutenção e lida com problemas importantes para você. 

O Armazenamento do Azure consiste em três serviços de dados: armazenamento de Blobs, armazenamento de Arquivos e armazenamento de Filas. Armazenamento de blob dá suporte a armazenamento standard e premium, com o armazenamento premium usando SSDs somente para possíveis de desempenho mais rápido de saudação. Outro recurso é moderado armazenamento, permitindo que você toostorage grandes quantidades de dados raramente acessados para um custo menor.

Neste artigo, você aprenderá a seguir hello:
* Serviços de armazenamento do Azure Olá
* tipos de saudação de contas de armazenamento
* acessando seus blobs, filas e arquivos
* criptografia
* replicação 
* transferência de dados para dentro ou fora do armazenamento
* Olá muitas bibliotecas de cliente de armazenamento disponíveis. 


<!-- RE-ENABLE THESE AFTER MVC GOES LIVE 
tooget up and running with Azure Storage quickly, check out one of hello following Quickstarts:
* [Create a storage account using PowerShell](storage-quick-create-storage-account-powershell.md)
* [Create a storage account using CLI](storage-quick-create-storage-account-cli.md)
-->


## <a name="introducing-hello-azure-storage-services"></a>Serviços de armazenamento do Azure apresentando Olá

toouse Olá serviços fornecidos pelo armazenamento do Azure – armazenamento de Blob, armazenamento de arquivo e armazenamento de fila-- você primeiro crie uma conta de armazenamento e, em seguida, você pode transferir dados para/de um serviço específico na conta de armazenamento. 

## <a name="blob-storage"></a>Armazenamento de blob

Blobs são basicamente arquivos, como aqueles que você armazena no seu computador (ou tablet, dispositivo móvel e assim por diante). Eles podem ser imagens, arquivos do Microsoft Excel, arquivos HTML, discos rígidos virtuais (VHDs), big data como logs, backups de banco de dados – basicamente tudo. BLOBs são armazenados em contêineres, que são toofolders semelhante. 

Depois de armazenar arquivos no armazenamento de Blob, você pode acessá-los de qualquer lugar no Olá, mundo usando URLs, Olá interface REST, ou uma das bibliotecas de cliente de armazenamento Olá SDK do Azure. As bibliotecas de clientes de armazenamento estão disponíveis para várias linguagens, incluindo Node.js, Java, PHP, Ruby, Python e .NET. 

Há três tipos de blobs – blobs de blocos, blobs de acréscimo e blobs de páginas (usados para arquivos VHD).

* Blobs de bloco são toohold utilizado de arquivos comuns backup tooabout 4.7 TB. 
* Blobs de página são arquivos de acesso aleatório de toohold usadas até too8 TB de tamanho. Eles são usados para os arquivos VHD Olá fazer VMs.
* Acrescentar blobs são compostos de blocos como blobs de bloco hello, mas são otimizados para operações de acréscimo. Eles são usados para tarefas como efetuar toohello informações mesmo blob de várias VMs.

Para grandes conjuntos de dados onde as restrições de rede fazer carregamento ou download de armazenamento tooBlob de dados em transmissão de saudação irreal, você pode enviar um conjunto de discos rígidos tooMicrosoft tooimport ou exportar dados diretamente do Centro de dados de saudação. Consulte [usar Olá serviço de importação/exportação do Microsoft Azure tooTransfer dados tooBlob armazenamento](../storage-import-export-service.md).

## <a name="file-storage"></a>Armazenamento de arquivos

Olá serviço arquivos do Azure permite que você tooset a compartilhamentos de arquivos de rede altamente disponível que podem ser acessados usando o protocolo de bloco de mensagens de servidor (SMB) padrão da saudação. Que significa que podem ser compartilhados por várias VMs Olá mesmo arquivos com acesso de leitura e gravação. Você também pode ler arquivos de hello usando a interface REST de saudação ou bibliotecas de saudação do cliente de armazenamento. 

Uma coisa que diferencia o armazenamento de arquivo do Azure dos arquivos em um compartilhamento de arquivos corporativo é que você pode acessar arquivos de saudação de qualquer lugar no mundo hello usando uma URL que aponta o arquivo toohello e inclui um token de acesso compartilhado (SAS) de assinatura. Você pode gerar tokens SAS; Eles permitem ativo privada de tooa de acesso específicos para um determinado período de tempo. 

Os compartilhamentos de arquivos podem ser usados para muitos cenários comuns: 

* Muitos aplicativos locais usam compartilhamentos de arquivos. Este recurso torna mais fácil toomigrate os aplicativos que compartilham dados tooAzure. Se você montar hello toohello de compartilhamento de arquivo mesma letra Olá de unidade local usada pelo aplicativo, parte de saudação do seu aplicativo que acessa o compartilhamento de arquivo hello deve funcionar com alterações mínimas, se houver.

* Os arquivos de configuração podem ser armazenados em um compartilhamento de arquivos e acessados de várias VMs. Ferramentas e utilitários usados por vários desenvolvedores em um grupo podem ser armazenados em um compartilhamento de arquivos, garantindo que todas as pessoas podem encontrá-los, e que usam Olá a mesma versão.

* Logs de diagnóstico, métricas e despejos de memória são apenas três exemplos de dados que podem ser gravados tooa compartilhamento de arquivos e processados ou analisados posteriormente.

Nesse momento, a autenticação baseada no Active Directory e acesso (ACLs) listas de controle não tem suporte, mas eles estarão em algum momento Olá futuras. Olá credenciais da conta de armazenamento são autenticação tooprovide usadas para compartilhamento de arquivos de toohello de acesso. Isso significa que qualquer pessoa com compartilhamento Olá montado terá o compartilhamento de toohello de acesso de leitura/gravação completa.

## <a name="queue-storage"></a>Armazenamento de filas

Olá serviço de fila do Azure é usadas mensagens toostore e recuperar. Fila de mensagens pode ser o too64 KB de tamanho e uma fila pode conter milhões de mensagens. As filas são toostore geralmente usadas listas de toobe de mensagens processadas de forma assíncrona. 

Por exemplo, digamos que você deseja imagens clientes toobe tooupload capaz de, e toocreate miniaturas de cada imagem. Você pode ter o cliente espere miniaturas de saudação toocreate durante o carregamento de imagens de saudação. Uma alternativa seria toouse uma fila. Quando o cliente Olá termina seu carregamento, escreva uma fila de mensagens toohello. Em seguida, ter uma função do Azure recuperar a mensagem de saudação da fila de saudação e criar miniaturas de saudação. Cada uma das partes Olá desse processamento separadamente, pode ser dimensionada oferecendo mais controle quando o ajuste para seu uso.

<!-- this bookmark is used by other articles; you'll need tooupdate them before this goes into production ROBIN-->
## <a name="table-storage"></a>Armazenamento de tabela
<!-- add a link toohello old table storage toothis paragraph once it's moved -->
O Armazenamento de Tabelas do Azure Standard agora é parte do Cosmos DB. As Tabelas Premium também estão disponíveis para o Armazenamento de Tabelas do Azure, oferecendo tabelas otimizadas para taxa de transferência, distribuição global e índices secundários automáticos. toolearn mais e experimentar a nova experiência de premium Olá, faça check-out [o banco de dados do Azure Cosmos: API de tabela](https://aka.ms/premiumtables).

## <a name="disk-storage"></a>Armazenamento em disco

equipe de armazenamento do Azure Olá também possui discos, que inclui todas Olá gerenciado e os recursos de disco não gerenciados usados por máquinas virtuais. Para obter mais informações sobre esses recursos, consulte Olá [documentação do serviço de computação](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).

## <a name="types-of-storage-accounts"></a>Tipos de contas de armazenamento 

Esta tabela mostra Olá vários tipos de contas de armazenamento e os objetos que podem ser usados com cada.

|**Tipo de conta de armazenamento**|**Standard de uso geral**|**Premium de uso geral**|**Armazenamento de blobs, níveis de acesso quente e frio**|
|-----|-----|-----|-----|
|**Serviços compatíveis**| Serviços de Filas, Arquivos e Blobs | Serviço Blob | Serviço Blob|
|**Tipos de blobs compatíveis**|Blobs de blocos, blobs de páginas e blobs de acréscimo | Blobs de página | Blobs de blocos e blobs de acréscimo|

### <a name="general-purpose-storage-accounts"></a>Contas de armazenamento de uso geral

Há dois tipos de contas de armazenamento de uso geral. 

#### <a name="standard-storage"></a>Armazenamento Standard 

Olá usado amplamente contas de armazenamento são contas de armazenamento padrão, que podem ser usadas para todos os tipos de dados. Contas de armazenamento padrão usam dados de toostore mídia magnética.

#### <a name="premium-storage"></a>Armazenamento Premium

O armazenamento Premium fornece armazenamento de alto desempenho para blobs de páginas, que são usados principalmente para arquivos VHD. Contas de armazenamento Premium usam dados de toostore SSD. A Microsoft recomenda usar o Armazenamento Premium para todas as suas VMs.

### <a name="blob-storage-accounts"></a>Contas de Armazenamento de Blobs

conta de armazenamento de Blob de saudação é uma conta de armazenamento especializado usado toostore blobs de bloco e blobs de acréscimo. Não é possível armazenar blobs de páginas nessas contas, portanto você não pode armazenar arquivos VHD. Essas contas permitem que você tooset um tooHot de camada de acesso ou legal; camada de saudação pode ser alterado a qualquer momento. 

camada de acesso quente Olá é usada para arquivos que são acessados com frequência – pagar um custo mais alto para o armazenamento, mas Olá custo acessar blobs Olá é muito menor. Para os blobs armazenados na camada de acesso moderado Olá, você paga um custo mais alto para acessar blobs hello, mas custo Olá de armazenamento é muito menor.

## <a name="accessing-your-blobs-files-and-queues"></a>Acessar blobs, arquivos e filas

Cada conta de armazenamento possui duas chaves de autenticação, que podem ser usadas para qualquer operação. Há duas chaves para que você pode passar Olá ocasionalmente chaves tooenhance segurança. É importante que essas chaves ser mantidos seguros porque sua posse, juntamente com o nome da conta hello, permite que os dados de tooall acesso ilimitado na conta de armazenamento hello. 

Esta seção aborda duas maneiras toosecure Olá armazenamento conta e seus dados. Para obter informações detalhadas sobre como proteger sua conta de armazenamento e seus dados, consulte Olá [guia de segurança do armazenamento do Azure](storage-security-guide.md).

### <a name="securing-access-toostorage-accounts-using-azure-ad"></a>Protegendo o acesso toostorage contas usando o Azure AD

Dados de armazenamento de tooyour toosecure um modo de acesso são por meio do controle de acesso toohello de chaves da conta de armazenamento. Com o Gerenciador de recursos de controle de acesso baseado em função (RBAC), você pode atribuir funções toousers, grupos ou aplicativos. Essas funções são associadas tooa o conjunto específico de ações que são permitidas ou não permitido. Usando o RBAC conta de armazenamento toogrant acesso tooa manipula apenas as operações de gerenciamento Olá para essa conta de armazenamento, como alterar o nível de acesso de saudação. Você não pode usar o RBAC toogrant acessar toodata objetos como um compartilhamento de arquivo ou contêiner específico. No entanto, você pode usar o RBAC toogrant acesso toohello chaves conta de armazenamento, que podem ser usado tooread Olá dados objetos. 

### <a name="securing-access-using-shared-access-signatures"></a>Protegendo o acesso usando assinaturas de acesso compartilhado 

Você pode usar assinaturas de acesso compartilhado e armazenados toosecure de políticas de acesso os objetos de dados. Uma assinatura de acesso compartilhado (SAS) é uma cadeia de caracteres que contém um token de segurança que pode ser anexados toohello URI para um ativo que permite que objetos de armazenamento de toospecific toodelegate acesso e restrições de toospecify como intervalo de data/hora de saudação de acesso e permissões. Esta funcionalidade tem recursos abrangentes. Para obter informações detalhadas, consulte muito[usando assinaturas (SAS de acesso compartilhado)](storage-dotnet-shared-access-signature-part-1.md).

### <a name="public-access-tooblobs"></a>Tooblobs de acesso público

Olá serviço Blob permite que você tooprovide acesso público tooa contêiner e seus blobs ou um blob específico. Quando você indica que um contêiner ou blob é público, qualquer pessoa pode lê-lo anonimamente. Nenhuma autenticação é necessária. Um exemplo de quando você desejaria toodo é quando você tiver um site que está usando imagens, vídeo ou documentos do armazenamento de Blob. Para obter mais informações, consulte [gerenciar o acesso de leitura anônimo toocontainers e blobs](../blobs/storage-manage-access-to-resources.md) 

## <a name="encryption"></a>Criptografia

Há dois tipos básicos de criptografia para serviços de armazenamento de saudação. 

### <a name="encryption-at-rest"></a>Criptografia em repouso 

Você pode habilitar a criptografia de serviço de armazenamento (SSE) em um dos serviços de arquivos de saudação (visualização) ou Olá serviço Blob para uma conta de armazenamento do Azure. Se habilitada, todos os dados gravados serviço específico toohello é criptografado antes de gravado. Quando você ler dados hello, ele é descriptografado antes retornado. 

### <a name="client-side-encryption"></a>Criptografia do cliente

Olá, bibliotecas de cliente de armazenamento têm métodos que você pode chamar tooprogrammatically criptografar os dados antes de enviá-la em transmissão de saudação do hello tooAzure de cliente. Ele são armazenados criptografados, o que significa que ele também é criptografado em repouso. Ao ler dados de saudação novamente, você descriptografa as informações de saudação depois de receber a ele. 

### <a name="encryption-in-transit-with-azure-file-shares"></a>Criptografia durante a transferência com Compartilhamentos de Arquivos do Azure

Confira [Usando Assinaturas de Acesso Compartilhado (SAS)](../storage-dotnet-shared-access-signature-part-1.md) para saber mais sobre as assinaturas de acesso compartilhado. Consulte [gerenciar o acesso de leitura anônimo toocontainers e blobs](../blobs/storage-manage-access-to-resources.md) e [autenticação para Olá serviços de armazenamento do Azure](https://msdn.microsoft.com/library/azure/dd179428.aspx) para obter mais informações sobre a conta de armazenamento de tooyour acesso seguro.

Para obter mais detalhes sobre como proteger sua conta de armazenamento e a criptografia, consulte Olá [guia de segurança do armazenamento do Azure](storage-security-guide.md).

## <a name="replication"></a>Replicação

Em tooensure de ordem que os dados sejam duráveis, o armazenamento do Azure tem Olá capacidade tookeep (e gerenciar) várias cópias de seus dados. Isso é chamado de replicação ou, algumas vezes, de redundância. Quando você configura sua conta de armazenamento, você seleciona o tipo de replicação. Na maioria dos casos, essa configuração pode ser modificada após a conta de armazenamento hello. 

Todas as contas de armazenamento possuem **armazenamento localmente redundante (LRS)**. Isso significa que três cópias de seus dados são gerenciadas pelo armazenamento do Azure no data center de saudação especificado quando a conta de armazenamento Olá foi configurada. Quando as alterações são confirmada tooone copiar, hello outras duas cópias são atualizadas antes de retornar êxito. Isso significa que três réplicas de saudação sempre estão em sincronia. Além disso, três cópias de saudação residem em domínios de falha e domínios de atualização, que significa que os dados estão disponíveis, mesmo se um nó de armazenamento, mantendo seus dados falha ou for feito toobe offline atualizado. 

**Armazenamento com redundância local (LRS)**

Conforme explicado acima, com o LRS você possui três cópias de seus dados em um único datacenter. Ele trata o problema de saudação de dados se tornar indisponível, se um nó de armazenamento falha ou fica offline toobe atualizado, mas não Olá caso de um datacenter inteiro fique indisponível.

**Armazenamento com redundância de zona (ZRS)**

Armazenamento com redundância de zona (ZRS) mantém três cópias locais Olá dos seus dados, bem como em outro conjunto de três cópias de seus dados. Olá segundo conjunto de três cópias é replicado de forma assíncrona em data centers dentro de uma ou duas regiões. Observe que o ZRS está disponível somente para blobs de blocos em contas de armazenamento de uso geral. Além disso, depois que você criou sua conta de armazenamento e selecionado ZRS, você não pode converter toouse tooany outro tipo de replicação, ou vice-versa.

Contas ZRS fornecem maior durabilidade do que o LRS, mas contas ZRS não possuem métricas ou recursos de registro em log. 

**Armazenamento com redundância geográfica (GRS)**

Armazenamento com redundância geográfica (GRS) mantém três cópias locais Olá dos seus dados em uma região primária e outro conjunto de três cópias de seus dados em uma região secundária a centenas de milhas de distância região primária hello. No evento de saudação de uma falha na região primária hello, armazenamento do Azure irão falhar região secundária toohello. 

**Armazenamento com redundância geográfica com acesso de leitura (RA-GRS)** 

Armazenamento com redundância geográfica com acesso de leitura é exatamente como GRS, exceto que você obtém dados de toohello de acesso de leitura no local secundário hello. Se Olá data center principal ficar indisponível temporariamente, você pode continuar tooread dados de saudação do local secundário hello. Isso pode ser muito útil. Por exemplo, ter um aplicativo da web que são alterados em modo somente leitura e pontos de cópia secundária de toohello, permitindo acesso, mesmo que as atualizações não estão disponíveis 

> [!IMPORTANT]
> Você pode alterar como os dados são replicados após sua conta de armazenamento tiver sido criada, a menos que especificado o ZRS quando você criou a conta de saudação. No entanto, observe que você pode incorrer em uma transferência de dados adicionais se você mudar de LRS tooGRS ou RA-GRS de custo.
>

Para saber mais informações sobre replicação, consulte [Replicação do Armazenamento do Azure](storage-redundancy.md).

Para obter informações de recuperação de desastres, consulte [que toodo se ocorrer uma interrupção de armazenamento do Azure](storage-disaster-recovery-guidance.md).

Para obter um exemplo de como tooleverage RA-GRS armazenamento tooensure alta disponibilidade, consulte [criação altamente disponível de aplicativos usando RA-GRS](storage-designing-ha-apps-with-ragrs.md).

## <a name="transferring-data-tooand-from-azure-storage"></a>Transferindo dados tooand do armazenamento do Azure

Você pode usar o blob de toocopy Olá AzCopy utilitário de linha de comando e dados de arquivos em sua conta de armazenamento ou em contas de armazenamento. Consulte um dos seguintes Olá artigos para obter ajuda:

* [Transferir dados com o AzCopy para Windows](storage-use-azcopy.md)
* [Transferir dados com o AzCopy para Linux](storage-use-azcopy-linux.md)

AzCopy é criado sobre Olá [biblioteca de movimentação de dados do Azure](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/), que está atualmente disponível na visualização.

Olá serviço de importação/exportação do Azure pode ser usado tooimport ou exportar grandes quantidades de tooor de dados de blob da conta de armazenamento. Você prepara e várias unidades de disco rígido tooan data center do Azure, onde eles transferirá Olá dados para/de discos rígidos hello e envia as unidades de disco rígido Olá tooyou de volta. Para obter mais informações sobre Olá serviço de importação/exportação, consulte [usar Olá serviço de importação/exportação do Microsoft Azure tooTransfer dados tooBlob armazenamento](../storage-import-export-service.md).

## <a name="pricing"></a>Preços

Para obter informações detalhadas sobre os preços de armazenamento do Azure, consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/storage/blobs/).

## <a name="storage-apis-libraries-and-tools"></a>APIs, bibliotecas e ferramentas de armazenamento
Os recursos do Armazenamento do Azure podem ser acessados por qualquer linguagem que possa fazer solicitações HTTP/HTTPS. Além disso, o Armazenamento do Azure oferece bibliotecas de programação para várias linguagens populares. Essas bibliotecas simplificam muitos aspectos do trabalho com o Armazenamento do Azure manipulando detalhes, como invocação síncrona e assíncrona, processamento em lotes de operações, gerenciamento de exceções, novas tentativas automáticas, comportamento operacional e assim por diante. Bibliotecas estão disponíveis para Olá idiomas a seguir e plataformas com outras pessoas em Olá pipeline:

### <a name="azure-storage-data-services"></a>Serviços de dados do Armazenamento do Azure
* [API REST dos Serviços de Armazenamento](/rest/api/storageservices/)
* [Biblioteca do Cliente de Armazenamento para .NET](https://docs.microsoft.com/dotnet/api/?view=azurestorage-8.1.1)
* [Biblioteca do Cliente de Armazenamento para C++](https://github.com/Azure/azure-storage-cpp)
* [Biblioteca do Cliente de Armazenamento para Java/Android](https://azure.microsoft.com/develop/java/)
* [Biblioteca do Cliente de Armazenamento para Node.js](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [Biblioteca do Cliente de Armazenamento para PHP](https://azure.microsoft.com/develop/php/)
* [Biblioteca do Cliente de Armazenamento para Python](https://azure.microsoft.com/develop/python/)
* [Biblioteca do Cliente de Armazenamento para Ruby](https://azure.microsoft.com/develop/ruby/)
* [Cmdlets de Armazenamento para PowerShell](/powershell/module/azure.storage/?view=azurermps-4.1.0&viewFallbackFrom=azurermps-4.0.0)
* [Comandos de Armazenamento para CLI 2.0](/cli/azure/storage)

## <a name="next-steps"></a>Próximas etapas

* [Saiba mais sobre o Armazenamento de Blobs](../blobs/storage-blobs-introduction.md)
* [Saiba mais sobre o Armazenamento de Arquivos](../storage-files-introduction.md)
* [Saiba mais sobre o Armazenamento de Filas](../queues/storage-queues-introduction.md)

<!-- RE-ENABLE THESE AFTER MVC GOES LIVE 
tooget up and running with Azure Storage quickly, check out one of hello following Quickstarts:
* [Create a storage account using PowerShell](storage-quick-create-storage-account-powershell.md)
* [Create a storage account using CLI](storage-quick-create-storage-account-cli.md)
-->

<!-- FIGURE OUT WHAT tooDO WITH ALL THESE LINKS.

Azure Storage resources can be accessed by any language that can make HTTP/HTTPS requests. Additionally, Azure Storage offers programming libraries for several popular languages. These libraries simplify many aspects of working with Azure Storage by handling details such as synchronous and asynchronous invocation, batching of operations, exception management, automatic retries, operational behavior and so forth. Libraries are currently available for hello following languages and platforms, with others in hello pipeline:

### Azure Storage data services
* [Storage Services REST API](https://docs.microsoft.com/rest/api/storageservices/)
* [Storage Client Library for .NET](https://docs.microsoft.com/dotnet/api/?view=azurestorage-8.1.1)
* [Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp)
* [Storage Client Library for Java/Android](https://azure.microsoft.com/develop/java/)
* [Storage Client Library for Node.js](http://dl.windowsazure.com/nodestoragedocs/index.html)
* [Storage Client Library for PHP](https://azure.microsoft.com/develop/php/)
* [Storage Client Library for Python](https://azure.microsoft.com/develop/python/)
* [Storage Client Library for Ruby](https://azure.microsoft.com/develop/ruby/)
* [Storage Cmdlets for PowerShell](/powershell/module/azure.storage/?view=azurermps-4.1.0&viewFallbackFrom=azurermps-4.0.0)

### Azure Storage management services
* [Storage Resource Provider REST API Reference](/rest/api/storagerp/)
* [Storage Resource Provider Client Library for .NET](/dotnet/api/microsoft.azure.management.storage)
* [Storage Resource Provider Cmdlets for PowerShell 1.0](/powershell/module/azure.storage)
* [Storage Service Management REST API (Classic)](https://msdn.microsoft.com/library/azure/ee460790.aspx)

### Azure Storage data movement services
* [Storage Import/Export Service REST API](../storage-import-export-service.md)
* [Storage Data Movement Client Library for .NET](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement/)

### Tools and utilities
* [Microsoft Azure Storage Explorer](../../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.
* [Azure Storage Client Tools](../storage-explorers.md)
* [Azure SDKs and Tools](https://azure.microsoft.com/tools/)
* [Azure Storage Emulator](http://www.microsoft.com/download/details.aspx?id=43709)
* [Azure PowerShell](/powershell/azure/overview)
* [AzCopy Command-Line Utility](http://aka.ms/downloadazcopy)

## Next steps
toolearn more about Azure Storage, explore these resources:

### Documentation
* [Azure Storage Documentation](https://azure.microsoft.com/documentation/services/storage/)
* [Create a storage account](../storage-create-storage-account.md)

<!-- after our quick starts are available, replace this link with a link tooone of those. 
Had tooremove this article, it refers toohello VS quickstarts, and they've stopped publishing them. Robin --> 
<!--* [Get started with Azure Storage in five minutes](storage-getting-started-guide.md)
-->

### <a name="for-administrators"></a>Para administradores
* [Usando o PowerShell do Azure com o Armazenamento do Azure](storage-powershell-guide-full.md)
* [Uso da CLI do Azure com o Armazenamento do Azure](../storage-azure-cli.md)

### <a name="for-net-developers"></a>Para desenvolvedores do .NET
* [Introdução ao armazenamento de Blobs do Azure usando o .NET](../blobs/storage-dotnet-how-to-use-blobs.md)
* [Introdução ao armazenamento de Tabelas do Azure usando o .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [Introdução ao armazenamento de Fila do Azure usando o .NET](../storage-dotnet-how-to-use-queues.md)
* [Introdução ao Armazenamento de Arquivos do Azure no Windows](../storage-dotnet-how-to-use-files.md)

### <a name="for-javaandroid-developers"></a>Para desenvolvedores de Java/Android
* [Como toouse armazenamento de Blob do Java](../blobs/storage-java-how-to-use-blob-storage.md)
* [Como toouse o armazenamento de tabela do Java](../../cosmos-db/table-storage-how-to-use-java.md)
* [Como toouse armazenamento de fila do Java](../storage-java-how-to-use-queue-storage.md)
* [Como toouse armazenamento de arquivo do Java](../storage-java-how-to-use-file-storage.md)

### <a name="for-nodejs-developers"></a>Para desenvolvedores do Node.js
* [Como toouse armazenamento de Blob do Node. js](../blobs/storage-nodejs-how-to-use-blob-storage.md)
* [Como toouse o armazenamento de tabela do Node. js](../../cosmos-db/table-storage-how-to-use-nodejs.md)
* [Como toouse armazenamento de fila do Node. js](../storage-nodejs-how-to-use-queues.md)

### <a name="for-php-developers"></a>Para desenvolvedores do PHP
* [Como toouse armazenamento de Blob do PHP](../blobs/storage-php-how-to-use-blobs.md)
* [Como toouse o armazenamento de tabela do PHP](../../cosmos-db/table-storage-how-to-use-php.md)
* [Como toouse armazenamento de fila do PHP](../storage-php-how-to-use-queues.md)

### <a name="for-ruby-developers"></a>Para desenvolvedores do Ruby
* [Como toouse armazenamento de Blob do Ruby](../blobs/storage-ruby-how-to-use-blob-storage.md)
* [Como toouse o armazenamento de tabela do Ruby](../../cosmos-db/table-storage-how-to-use-ruby.md)
* [Como toouse armazenamento de fila do Ruby](../storage-ruby-how-to-use-queue-storage.md)

### <a name="for-python-developers"></a>Para desenvolvedores do Python
* [Como toouse armazenamento de Blob do Python](../blobs/storage-python-how-to-use-blob-storage.md)
* [Como toouse o armazenamento de tabela do Python](../../cosmos-db/table-storage-how-to-use-python.md)
* [Como toouse armazenamento de fila do Python](../storage-python-how-to-use-queue-storage.md)   
* [Como toouse armazenamento de arquivo do Python](../storage-python-how-to-use-file-storage.md) 
-->