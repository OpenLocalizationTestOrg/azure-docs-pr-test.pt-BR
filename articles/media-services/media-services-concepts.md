---
title: "conceitos de serviços de mídia aaaAzure | Microsoft Docs"
description: "Este tópico oferece uma visão geral dos conceitos de Serviços de Mídia do Azure"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: dcefc8bc-e2ea-4b38-a643-9010f4436fb5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: juliako
ms.openlocfilehash: 0a45deff32336dfcf778552f720c1ea21927951b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-concepts"></a>Conceitos dos Serviços de Mídia do Azure
Este tópico fornece uma visão geral dos conceitos mais importantes de serviços de mídia hello.

## <a id="assets"></a>Ativos e armazenamento
### <a name="assets"></a>Ativos
Um [ativo](https://docs.microsoft.com/rest/api/media/operations/asset) contém arquivos digitais (incluindo vídeo, áudio, imagens, coleções de miniaturas, faixas de texto e arquivos de legenda codificada) e Olá metadados sobre esses arquivos. Depois de arquivos digitais Olá são carregados em um ativo, pode ser usados nos serviços de mídia Olá codificação e streaming de fluxos de trabalho.

Um ativo é mapeado tooa contêiner de blob na conta de armazenamento do Azure hello e arquivos Olá no ativo de saudação são armazenados como blobs de blocos no contêiner. Os blobs de páginas não são compatíveis com os Serviços de Mídia do Azure.

Ao decidir quais tooupload conteúdo de mídia e armazenamento em um ativo, Olá considerações a seguir se aplicam:

* Um ativo deve conter apenas uma instância única e exclusiva do conteúdo de mídia. Por exemplo, uma única edição de um episódio de TV, filme ou anúncio.
* Um ativo não deve conter representações ou edições múltiplas de um arquivo audiovisual. Um exemplo de uso inapropriado de um ativo deve tentar toostore mais de um episódio de TV, anúncio ou uma produção única dentro de um ativo de vários ângulos de câmera. Armazenar representações ou edições diversas de um arquivo audiovisual em um ativo pode resultar em dificuldades ao enviar trabalhos de codificação, transmissão e segurança de entrega de saudação do ativo Olá posteriormente no fluxo de trabalho de saudação.  

### <a name="asset-file"></a>Arquivo de ativo
Um [AssetFile](https://docs.microsoft.com/rest/api/media/operations/assetfile) representa um arquivo de áudio ou vídeo real que é armazenado em um contêiner de blob. Um arquivo de ativo está sempre associado a um ativo, e um ativo pode conter um ou vários arquivos. tarefa do Media Services Encoder Olá falhará se um objeto de arquivo do ativo não está associado um arquivo digital em um contêiner de blob.

Olá **AssetFile** instância e o arquivo de mídia real Olá são dois objetos distintos. instância de AssetFile Olá contém metadados sobre o arquivo de mídia Olá, enquanto o arquivo de mídia Olá contém conteúdo de mídia real hello.

Não tente toochange conteúdo de saudação de contêineres de blob que foram gerados pelos serviços de mídia sem o uso de APIs de serviços de mídia.

### <a name="asset-encryption-options"></a>Opções de criptografia de ativos
Dependendo do tipo de saudação do conteúdo que você deseja tooupload, armazenamento e entregar, os serviços de mídia oferece várias opções de criptografia que você pode escolher.

>[!NOTE]
>Nenhuma criptografia é usada. Este é o valor padrão de saudação. Ao usar essa opção, seu conteúdo não é protegido quando está em trânsito ou em repouso no armazenamento.

Se você planejar toodeliver um MP4 usando o download progressivo, use tooupload essa opção seu conteúdo.

**StorageEncrypted** – Use essa opção tooencrypt o conteúdo limpo localmente usando a criptografia AES de 256 bits e, em seguida, carregá-lo tooAzure armazenamento onde ele está armazenado criptografado em repouso. Ativos protegidos pela criptografia de armazenamento são descriptografados automaticamente e posicionados em um tooencoding anterior do sistema de arquivos criptografados e, opcionalmente, criptografada novamente toouploading anterior como um novo ativo de saída. caso de uso primário Olá para criptografia de armazenamento é quando você deseja toosecure seus arquivos de mídia de entrada de alta qualidade com criptografia forte em rest no disco. 

Ordem toodeliver um ativo de armazenamento criptografado, você deve configurar a política de distribuição do ativo Olá para que serviços de mídia saibam como você deseja toodeliver seu conteúdo. Antes do ativo pode ser transmitido, Olá streaming fluxos e criptografia de armazenamento de saudação do servidor remove o conteúdo usando Olá especificado política de entrega (por exemplo, AES, PlayReady ou sem criptografia). 

**CommonEncryptionProtected** -Use essa opção se você quiser tooencrypt (ou carregamento já criptografado) conteúdo com criptografia comum ou PlayReady DRM (por exemplo, Smooth Streaming protegido com DRM PlayReady).

**EnvelopeEncryptionProtected** – Use esta opção se você quiser tooprotect (ou carregamento já protegido) HTTP Live Streaming (HLS) criptografado com Advanced Encryption Standard (AES). Observe que, se você estiver carregando um HLS já criptografado com AES, ele deverá ter sido criptografado pelo Transform Manager.

### <a name="access-policy"></a>Política de acesso
Um [AccessPolicy](https://docs.microsoft.com/rest/api/media/operations/accesspolicy) define permissões (como leitura, gravação e lista) e a duração do ativo de tooan de acesso. Normalmente, você passaria um localizador de tooa de objeto AccessPolicy que seria usadas tooaccess arquivos de Olá contidos em um ativo.

>[!NOTE]
>Há um limite de 1.000.000 políticas para diferentes políticas de AMS (por exemplo, para política de Localizador ou ContentKeyAuthorizationPolicy). Você deve usar Olá Olá a mesma ID de política se você estiver usando sempre mesmo dias acesso permissões, por exemplo, as políticas para localizadores são tooremain desejado no local por um longo período (políticas de carregamento não). Para obter mais informações, consulte [este](media-services-dotnet-manage-entities.md#limit-access-policies) tópico.

### <a name="blob-container"></a>Contêiner de blob
Um contêiner de blob fornece um agrupamento de um conjunto de blobs. Contêineres de blob são usados nos serviços de mídia como ponto limite para controle de acesso e localizadores de assinatura de acesso compartilhado (SAS) em ativos. Uma conta de armazenamento do Azure pode conter um número ilimitado de contêineres de blob. Um contêiner pode armazenar um número ilimitado de blobs.

>[!NOTE]
> Não tente toochange conteúdo de saudação de contêineres de blob que foram gerados pelos serviços de mídia sem o uso de APIs de serviços de mídia.
> 
> 

### <a id="locators"></a>Localizadores
[Localizador](https://docs.microsoft.com/rest/api/media/operations/locator)s fornecer uma saudação tooaccess de ponto de entrada aos arquivos contidos em um ativo. Uma política de acesso é usado toodefine Olá permissões e duração de um cliente tooa acesso fornecido ativo. Os localizadores podem ter uma relação de tooone muitos com uma política de acesso, como que diferentes localizadores possam fornecer diferentes horas de início e clientes de toodifferent de tipos de conexão enquanto todos usando Olá mesma permissão e as configurações de duração; No entanto, devido a uma restrição de política de acesso compartilhado definida pelos serviços de armazenamento do Azure, você não pode ter mais do que cinco localizadores exclusivos associados a um determinado ativo ao mesmo tempo. 

Serviços de mídia oferece suporte a dois tipos de localizadores: localizadores OnDemandOrigin, usados toostream mídia (por exemplo, MPEG DASH, HLS ou Smooth Streaming) ou download progressivo de mídia e localizadores URL SAS, tooupload usado ou to\from de arquivos de mídia de download armazenamento do Azure. 

>[!NOTE]
>permissão de lista da saudação (Accesspermissions) não deve ser usado ao criar um localizador OnDemandOrigin. 

### <a name="storage-account"></a>Conta de armazenamento
Todos os tooAzure de acesso a armazenamento é feito por meio de uma conta de armazenamento. Uma conta do Serviço de Mídia pode ser associada a uma ou mais contas de armazenamento. Uma conta pode conter um número ilimitado de contêineres, desde que seu tamanho total esteja abaixo de 500 TB por conta de armazenamento.  Nível de tooallow de ferramentas do SDK do Media Services fornece você toomanage várias contas de armazenamento e carga de saldo da distribuição de ativos Olá durante o carregamento toothese contas baseadas em métricas ou distribuição aleatória. Para saber mais, consulte Trabalhando com [Armazenamento do Azure](https://msdn.microsoft.com/library/azure/dn767951.aspx). 

## <a name="jobs-and-tasks"></a>Trabalhos e tarefas
Um [trabalho](https://https://docs.microsoft.com/rest/api/media/operations/job) é tooprocess geralmente usados (por exemplo, índice ou codificar) uma apresentação de áudio/vídeo. Se você estiver processando vários vídeos, crie um trabalho para cada toobe vídeo codificado.

Um trabalho contém metadados sobre processamento Olá toobe executada. Cada Trabalho contém uma ou mais [tarefas](https://docs.microsoft.com/rest/api/media/operations/task)que especificam uma tarefa de processamento atômica, seus ativos de entrada e ativos de saída, um processador de mídia e suas configurações associadas. Tarefas de trabalho podem ser encadeadas, onde Olá ativo de saída de uma tarefa é determinado como Olá próxima tarefa toohello do ativo de entrada. Dessa forma, um trabalho pode conter todo Olá processamento necessário para uma apresentação de mídia.

## <a id="encoding"></a>Codificação
Serviços de mídia do Azure fornece várias opções para Olá codificação de mídia na nuvem hello.

Começando com os serviços de mídia, é importante toounderstand diferença de saudação entre codecs e formatos de arquivo.
Codecs são Olá de software que implementa os algoritmos de compactação/descompactação Olá enquanto formatos de arquivo são contêineres que armazenam o vídeo Olá compactado.

Serviços de mídia fornecem empacotamento dinâmico que permite que você toodeliver sua taxa de bits adaptável MP4 ou Smooth Streaming codificado conteúdo de streaming formatos suportados pelo Media Services (MPEG DASH, HLS, Smooth Streaming) sem a necessidade de toore-package nesses formatos de fluxo contínuo.

aproveitar tootake [empacotamento dinâmico](media-services-dynamic-packaging-overview.md), você precisa tooencode o arquivo de mezanino (origem) em um conjunto de arquivos MP4 de taxa de bits adaptável ou arquivos de Smooth Streaming de taxa de bits adaptável e ter pelo menos uma extremidade de streaming padrão ou premium no estado iniciado.

Serviços de mídia oferece suporte a saudação codificadores sob demanda que são descritos neste artigo a seguir:

* [Media Encoder Standard](media-services-encode-asset.md#media-encoder-standard)
* [Fluxo de trabalho do Media Encoder Premium](media-services-encode-asset.md#media-encoder-premium-workflow)

Para saber mais sobre codificadores com suporte, consulte [Codificadores](media-services-encode-asset.md)

## <a name="live-streaming"></a>Transmissão ao vivo
Nos Serviços de Mídia do Azure, um Canal representa um pipeline para processamento de conteúdo de streaming ao vivo. Um Canal recebe transmissões de entrada ao vivo de uma das duas maneiras a seguir:

* Um codificador ao vivo no local envia RTMP de taxa de bits múltipla ou canal de toohello Smooth Streaming (MP4 fragmentado). Você pode usar o hello codificadores ao vivo que geram várias taxas de bits Smooth Streaming a seguir: MediaExcel, Ateme, Imagine comunicações, Envivio, Cisco e Elemental. Olá, seguintes codificadores dinâmicos saída RTMP: codificadores Adobe Flash Live codificador Telestream Wirecast, Teradek, Haivision e Tricaster. Olá fluxos ingeridos passam por meio de canais sem codificação e transcodificação de outras. Quando solicitado, os serviços de mídia oferece Olá fluxo toocustomers.
* Um fluxo de taxa de bits única (em um dos formatos a seguir de saudação: RTP (MPEG-TS)), RTMP ou Smooth Streaming (MP4 fragmentado)) é enviada com o canal de toohello que é habilitado tooperform ao vivo de codificação com os serviços de mídia. Olá Channel, em seguida, executa a codificação ao vivo de entrada de saudação taxa de bits única fluxo tooa várias taxas de bits (adaptável) fluxo de vídeo. Quando solicitado, os serviços de mídia oferece Olá fluxo toocustomers.

### <a name="channel"></a>Canal
Nos Serviços de Mídia, [Canais](https://docs.microsoft.com/rest/api/media/operations/channel)são responsáveis pelo processamento de conteúdo de transmissão ao vivo. Um canal fornece um ponto de extremidade de entrada (URL de ingestão) que você forneça transcodificador ao vivo tooa. canal de saudação recebe fluxos ao vivo de entrada do transcodificador ao vivo hello e disponibiliza para transmissão através de um ou mais StreamingEndpoints. Os canais também oferecem uma empresa de visualização (URL de visualização) que você use toopreview e valida sua transmissão antes de processamento e entrega.

Você pode obter Olá ingestão URL e a URL de visualização hello quando você criar o canal de saudação. tooget essas URLs, Olá canal não ter toobe em estado Olá iniciado. Quando você estiver pronto toostart enviar dados de um transcodificador ao vivo no canal hello, canal Olá deve ser iniciado. Depois que o transcodificador ao vivo Olá inicia a ingestão de dados, você pode visualizar o fluxo.

Cada conta dos Serviços de Mídia pode conter vários canais, vários programas e vários StreamingEndpoints. Dependendo das necessidades de largura de banda e segurança hello, serviços de StreamingEndpoint podem ser tooone dedicado ou mais canais. Qualquer StreamingEndpoint pode executar pull de qualquer canal.

### <a name="program-event"></a>Programa (evento)
Um [programa (evento)](https://docs.microsoft.com/rest/api/media/operations/program) permite a publicação de saudação toocontrol e armazenamento de segmentos em uma transmissão ao vivo. Canais gerenciam Programas (eventos). Olá, relação de canal e programa é semelhante mídia tootraditional onde um canal tem um fluxo constante de conteúdo e um programa está no escopo toosome atingiu o tempo de evento naquele canal.
Você pode especificar o número de saudação horas deseja tooretain Olá registrada conteúdo para programa hello por configuração Olá **ArchiveWindowLength** propriedade. Esse valor pode ser definido no mínimo 5 minutos tooa máximo 25 horas.

ArchiveWindowLength também determina o período de tempo que os clientes podem procurar de volta no tempo da posição atual ao vivo da saudação máximo hello. Programas podem ser executados pelo período de tempo especificado hello, mas o conteúdo que sai da duração da janela de saudação é continuamente descartado. Esse valor dessa propriedade também determina quanto tempo cliente Olá manifestos podem crescer.

Cada programa (evento) está associado a um ativo. programa de saudação toopublish você deve criar um localizador para Olá associados ativo. Ter esse localizador permitirá que você toobuild uma URL de streaming que pode fornecer tooyour clientes.

Um canal dá suporte para até toothree simultaneamente programas em execução para que você pode criar diversos arquivos de saudação mesmo fluxo de entrada. Isso permite que você toopublish e arquivamento diferentes partes de um evento, conforme necessário. Por exemplo, o requisito de negócios é tooarchive 6 horas de um programa, mas toobroadcast apenas últimos 10 minutos. tooaccomplish isso, você precisa toocreate dois programas em execução simultaneamente. Um programa está definido tooarchive 6 horas do evento Olá mas Olá programa não será publicado. Olá outro programa é tooarchive conjunto por 10 minutos e esse programa é publicado.

Para obter mais informações, consulte:

* [Trabalhando com canais que é habilitado tooPerform Live codificação com os serviços de mídia do Azure](media-services-manage-live-encoder-enabled-channels.md)
* [Trabalhando com Canais que recebam transmissão ao vivo de múltiplas taxas de bits de codificadores locais](media-services-live-streaming-with-onprem-encoders.md)
* [Cotas e limitações](media-services-quotas-and-limitations.md).

## <a name="protecting-content"></a>Proteção de conteúdo
### <a name="dynamic-encryption"></a>Criptografia dinâmica
Serviços de mídia do Azure permite que você toosecure sua mídia do tempo de saudação deixa o computador por meio de armazenamento, processamento e entrega. Serviços de mídia permitem toodeliver seu conteúdo dinamicamente criptografado com AES Advanced Encryption Standard () (usando chaves de criptografia de 128 bits) e criptografia comum (CENC) usando PlayReady e/ou Widevine DRM. Serviços de mídia também fornecem um serviço para distribuir chaves AES e PlayReady licenças tooauthorized os clientes.

No momento, você pode criptografar Olá seguintes formatos de streaming: Smooth Streaming, MPEG DASH e HLS. Não é possível criptografar downloads progressivos.

Se você quiser para serviços de mídia tooencrypt um ativo, você precisa tooassociate uma chave de criptografia (CommonEncryption ou EnvelopeEncryption) com seu ativo e também configurar políticas de autorização para a chave de saudação.

Se você quiser toostream um ativo de armazenamento criptografado, você deve configurar a política de distribuição do ativo Olá em ordem toospecify como você deseja toodeliver seu ativo.

Quando um fluxo é solicitado por um player, o Media Services usa Olá especificado toodynamically chave criptografar seu conteúdo usando uma criptografia de envelope (com AES) ou criptografia comum (com PlayReady ou Widevine). fluxo de saudação toodecrypt, player Olá solicitar chave Olá do serviço de distribuição de chaves de saudação. toodecide ou não usuário Olá é autorizado chave de saudação tooget, serviço Olá avalia as políticas de autorização de saudação que você especificou para a chave de saudação.

### <a name="token-restriction"></a>Restrição de token
Olá política de autorização da chave de conteúdo pode ter uma ou mais restrições de autorização: aberta, restrição de token ou restrição de IP. política de restrição de token de saudação deve ser acompanhada por um token emitido por um Token STS (serviço seguro). Serviços de mídia oferece suporte a tokens no formato do Simple Web Tokens (SWT) hello e JSON Web Token (JWT). Os serviços de mídia não fornecem Secure Token Services. Você pode criar um STS personalizado ou utilizar a tokens de tooissue ACS do Microsoft Azure. Olá STS deve ser configurado toocreate um token assinado com hello especificado chave e emitir declarações que você especificou na configuração de restrição de token hello. Serviços de mídia Olá serviço de entrega de chave retornará Olá solicitado hello e chave (ou licença) cliente toohello se Olá token for válido declarações em Olá token correspondam às configuradas para chave hello (ou licença).

Ao configurar a política de restrição de token do hello, você deve especificar a chave de verificação primária hello, emissor e parâmetros de público-alvo. chave de verificação primária Olá contém Olá chave que Olá token foi assinado com, o emissor é Olá serviço de token seguro que emite o token de saudação. público Hello (às vezes chamado de escopo) descreve a intenção de saudação do token de saudação ou token de saudação do recurso de saudação autoriza o acesso ao. Olá serviço de distribuição de chaves de serviços de mídia valida que esses valores no token Olá correspondem a valores de saudação no modelo de saudação.

Para obter mais informações, consulte Olá artigos a seguir:

[Visão geral da proteção de conteúdo](media-services-content-protection-overview.md)
[Proteger com o AES-128](media-services-protect-with-aes128.md)
[Proteger com DRM](media-services-protect-with-drm.md)

## <a name="delivering"></a>Fornecimento
### <a id="dynamic_packaging"></a>Empacotamento dinâmico
Ao trabalhar com os serviços de mídia, é recomendável tooencode arquivos de mezanino em uma taxa de bits adaptável MP4 definir e, em seguida, converter Olá defina toohello formato desejado usando Olá [empacotamento dinâmico](media-services-dynamic-packaging-overview.md).

### <a name="streaming-endpoint"></a>ponto de extremidade de streaming
Um StreamingEndpoint representa um serviço de streaming que pode entregar conteúdo diretamente tooa Player do cliente ou tooa rede de fornecimento de conteúdo (CDN) para melhor distribuição (Azure Media Services agora fornece integração do Azure CDN hello.) Olá fluxo de saída de um serviço de ponto de extremidade de streaming pode ser uma transmissão ao vivo ou um ativo de vídeo sob demanda em sua conta de serviços de mídia. Os clientes de serviços de mídia escolhem um **padrão** streaming de ponto de extremidade ou um ou mais **Premium** pontos de extremidade, de acordo com as necessidades de tootheir de streaming. O ponto de extremidade de streaming Standard é adequado para a maioria das cargas de trabalho de streaming. 

O Ponto de Extremidade de Streaming Standard é adequado para a maior parte de cargas de trabalho de streaming. Pontos de extremidade de Streaming padrão oferecem Olá flexibilidade toodeliver seu conteúdo toovirtually cada dispositivo por meio de empacotamento dinâmico em HLS, MPEG-DASH e Smooth Streaming, bem como a criptografia dinâmica para o Microsoft PlayReady, Google Widevine, Apple Fairplay e AES128.  Eles também dimensionar de toovery muito pequena grandes públicos com milhares de visualizadores simultâneos por meio da integração do Azure CDN. Se você tiver uma carga de trabalho avançada ou seus requisitos de capacidade de streaming não se ajustam toostandard destinos de taxa de transferência do ponto de extremidade de streaming ou toocontrol capacidade de saudação do hello StreamingEndpoint toohandle cada vez maior largura de banda serviço precisa, recomenda-se tooallocate unidades de escala (também conhecido como premium unidades de streaming).

É recomendável empacotamento dinâmico toouse e/ou criptografia dinâmica.

>[!NOTE]
>Quando sua conta AMS é criada um **padrão** ponto de extremidade de streaming é adicionada conta tooyour Olá **parado** estado. toostart streaming seu conteúdo e execute aproveitar o empacotamento dinâmico e criptografia dinâmica, Olá ponto de extremidade de streaming do qual você deseja toostream conteúdo tem toobe em Olá **executando** estado. 

Para obter mais informações, consulte [este](media-services-portal-manage-streaming-endpoints.md) tópico.

Por padrão, você pode ter até too2 pontos de extremidade de streaming em sua conta de serviços de mídia. toorequest um limite superior, consulte [cotas e limitações](media-services-quotas-and-limitations.md).

Você será cobrado apenas quando seu StreamingEndpoint estiver em estado de execução.

### <a name="asset-delivery-policy"></a>Política de fornecimento de ativos
Uma das Olá etapas no hello Media Services é a configuração de fluxo de trabalho de fornecimento de conteúdo [políticas de entrega de ativos ](https://docs.microsoft.com/rest/api/media/operations/assetdeliverypolicy)que você deseja toobe transmitido. política de entrega de ativos de saudação informa os serviços de mídia como você deseja para sua toobe ativo entregue: em qual protocolo de streaming deve seu ativo dinamicamente empacotado (por exemplo, MPEG DASH, HLS, Smooth Streaming ou todos), se você deseja toodynamically ou não criptografar seu ativo e como (envelope ou criptografia comum).

Se você tiver um ativo de armazenamento criptografado, antes do ativo pode ser transmitido, Olá streaming fluxos e criptografia de armazenamento de saudação do servidor remove o conteúdo usando Olá especificado a política de distribuição. Por exemplo, toodeliver seu ativo criptografado com chave de criptografia AES Advanced Encryption Standard (), tooDynamicEnvelopeEncryption de tipo de política de saudação de conjunto. criptografia de armazenamento tooremove e ativo de saudação do fluxo em Olá claro, definidos Olá tooNoDynamicEncryption de tipo de política.

### <a name="progressive-download"></a>Download progressivo
O download progressivo permite que você toostart reproduzir mídia antes do download de todo o arquivo hello. Você só pode baixar apenas progressivamente um arquivo MP4.

>[!NOTE]
>Você deve descriptografar ativos criptografados se desejar toobe disponível para download progressivo.

URLs de download progressivo aos usuários tooprovide, primeiro você deve criar um localizador OnDemandOrigin. Criando o localizador de hello, fornece Olá base ativo toohello de caminho. Você precisa, em seguida, o nome de saudação de tooappend do arquivo MP4. Por exemplo:

http://amstest1.streaming.mediaservices.windows.net/3c5fe676-199c-4620-9b03-ba014900f214/BigBuckBunny_H264_650kbps_AAC_und_ch2_96kbps.mp4

### <a name="streaming-urls"></a>URLs de streaming
Streaming tooclients seu conteúdo. usuários de tooprovide com URLs de streaming, você primeiro deve criar um localizador OnDemandOrigin. Criando o localizador de hello, fornece Olá base ativo toohello caminho que contém o conteúdo de saudação deseja toostream. No entanto, esse conteúdo é necessário toomodify esse caminho ainda mais de toostream capaz de toobe. tooconstruct um toohello URL completa, o arquivo de manifesto de streaming, você deverá concatenar o caminho do localizador de saudação do valor e hello (filename.ism) o nome do arquivo de manifesto. Em seguida, anexe /Manifest e um caminho de localizador de toohello formato apropriado (se necessário).

Você também pode transmitir seu conteúdo por uma conexão SSL. toodo isso, verifique se suas URLs de streaming começam com HTTPS. Atualmente, o AMS não dá suporte ao SSL com domínios personalizados.  

>[!NOTE]
>Só é possível transmitir sobre SSL se saudação do qual você distribuir o conteúdo do ponto de extremidade de streaming foi criada após 10 de setembro de 2014. Se suas URLs de streaming se baseiam em Olá criados após 10 de setembro de pontos de extremidade de streaming, Olá URL contém "streaming.mediaservices.windows.net" (novo formato de saudação). As URLs de streaming que contêm "origin.mediaservices.windows.net" (formato antigo do hello) não dão suporte a SSL. Se a URL estiver no formato antigo hello e desejar toostream capaz de toobe sobre SSL, crie um novo ponto de extremidade de streaming. Use as URLs criadas com base em Olá novo streaming toostream de ponto de extremidade seu conteúdo sobre SSL.

Olá lista a seguir descreve os diferentes formatos de streaming e oferece exemplos:

* Smooth Streaming

{nome do ponto de extremidade de streaming - nome de conta do dos serviços de mídia}.streaming.mediaservices.windows.net/{ID do localizador}/{nome do arqui}.ism/Manifest

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest

* MPEG DASH

{nome do ponto de extremidade de streaming - nome de conta dos serviços de mídia}.streaming.mediaservices.windows.net/{ID do localizador}/{nome do arquivo}.ism/Manifest(format=mpd-time-csf)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=mpd-time-csf)

* Apple HTTP Live Streaming (HLS) V4

{nome do ponto de extremidade de streaming - nome de conta dos serviços de mídia}.streaming.mediaservices.windows.net/{ID do localizador}/{nome do arquivo}.ism/Manifest(format=m3u8-aapl)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl)

* Apple HTTP Live Streaming (HLS) V3

{nome do ponto de extremidade de streaming - nome de conta dos serviços de mídia}.streaming.mediaservices.windows.net/{ID do localizador}/{nome do arquivo}.ism/Manifest(format=m3u8-aapl-v3)

http://testendpoint-testaccount.streaming.mediaservices.windows.net/fecebb23-46f6-490d-8b70-203e86b0df58/BigBuckBunny.ism/Manifest(format=m3u8-aapl-v3)

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

