---
title: "CENC com Vários DRMs e Controle de Acesso: um Design e Implementação de Referência no Azure e nos Serviços de Mídia do Azure | Microsoft Docs"
description: "Saiba mais sobre como toolicensing Olá Microsoft® Smooth Streaming Client Porting Kit."
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.assetid: 7814739b-cea9-4b9b-8370-538702e5c615
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: willzhan;kilroyh;yanmf;juliako
ms.openlocfilehash: 033fb618650c4fbe9069d467159a8734da759bba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="cenc-with-multi-drm-and-access-control-a-reference-design-and-implementation-on-azure-and-azure-media-services"></a>CENC com vários DRM e Controle de Acesso: design e implementação de referência no Azure e nos Serviços de Mídia do Azure
 
## <a name="introduction"></a>Introdução
É bem conhecido que é uma tarefa complexa toodesign e criar um subsistema DRM para um OTT ou online de solução de streaming. E é um comum prática para operadores/online toooutsource de provedores de vídeo provedores de serviço essa parte toospecialized DRM. meta de saudação deste documento é toopresent um design de referência e a implementação do subsistema de ponta a ponta DRM OTT ou solução de streaming on-line.

os leitores Olá alvo deste documento são engenheiros trabalhando no subsistema DRM do OTT streaming/multi-screen soluções online ou qualquer leitores interessados no subsistema DRM. Olá pressupõe-se que os leitores esteja familiarizados com pelo menos uma das tecnologias DRM Olá no mercado hello, como o PlayReady, Widevine, FairPlay ou Adobe acesso.

Em relação a DRM, também incluímos CENC (criptografia comum) com vários DRM. Uma tendência principais na transmissão online e do setor OTT é toouse CENC com multi-native-DRM em várias plataformas de cliente, que é uma mudança de tendência anterior de saudação do uso de um único DRM e o SDK de cliente para várias plataformas de cliente. Ao usar CENC com vários native DRM, PlayReady e Widevine são criptografados por Olá [criptografia comum (ISO/IEC 23001-7 CENC)](http://www.iso.org/iso/home/store/catalogue_ics/catalogue_detail_ics.htm?csnumber=65271/) especificação.

benefícios de saudação do CENC com DRM de vários são da seguinte maneira:

1. Reduz o custo de criptografia, já que um único processo de criptografia é usado para diferentes plataformas e seus DRMs nativos;
2. Reduz o custo de saudação do gerenciamento de ativos criptografados como uma única cópia de ativos criptografados não é necessário;
3. Elimina o custo de licenciamento desde Olá native client DRM é geralmente livre em sua plataforma nativo de clientes do DRM.

A Microsoft sempre promoveu ativamente DASH e CENC juntamente com alguns principais vetores da indústria. Os Serviços de Mídia do Microsoft Azure dão suporte a DASH e a CENC. Para obter comunicados recentes, confira os blogs da Mingfei: [Announcing Google Widevine license delivery services in Azure Media Services](https://azure.microsoft.com/blog/announcing-general-availability-of-google-widevine-license-services/) (Anunciando os serviços de entrega da licença Google Widevine nos Serviços de Mídia do Azure) e [Azure Media Services adds Google Widevine packaging for delivering multi-DRM stream](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/) (Serviços de Mídia do Azure adiciona pacote do Google Widevine para fornecer fluxo de vários DRMs).  

### <a name="overview-of-this-article"></a>Visão geral deste artigo
objetivo Olá deste artigo inclui o seguinte hello:

1. Fornece um design de referência do subsistema DRM usando CENC com vários DRM;
2. Fornece uma implementação de referência na plataforma Microsoft Azure/Serviços de Mídia do Azure;
3. Analisa alguns tópicos de design e implementação.

Artigo Olá, "multi-DRM" aborda a seguir hello:

1. Microsoft PlayReady
2. Google Widevine
3. Apple FairPlay 

Hello tabela a seguir resume os aplicativos de plataforma nativo/nativo hello e navegadores compatíveis com cada DRM.

| **Plataforma cliente** | **Suporte nativo ao DRM** | **Navegador/aplicativo** | **Formatos de streaming** |
| --- | --- | --- | --- |
| **Smart TVs, STBs de operador, STBs OTT** |Basicamente PlayReady e/ou Widevine e/ou outros |Linux, Opera, WebKit, outros |Vários formatos |
| **Dispositivos com Windows 10 (computadores Windows, tablets Windows, Windows Phone, Xbox)** |PlayReady |MS Edge/IE11/EME<br/><br/><br/>UWP |DASH (No HLS, o PlayReady não tem suporte)<br/><br/>DASH, Smooth Streaming (No HLS, o PlayReady não tem suporte) |
| **Dispositivos com Android (telefone, tablet, TV)** |Widevine |Chrome/EME |DASH, HLS |
| **iOS (iPhone, iPad), clientes OS X e Apple TV** |FairPlay |Safari 8+/EME |HLS |


Considerando o estado atual de saudação de implantação para cada DRM, um serviço normalmente deseja tooimplement 2 ou 3 DRMs toomake-se de que você resolver todos os tipos de saudação de pontos de extremidade no hello melhor maneira.

Há um equilíbrio entre a complexidade de saudação da lógica do serviço hello e experiência de complexidade de saudação em Olá cliente lado tooreach um determinado nível de usuário em hello vários clientes.

toomake sua seleção, tenha em mente esses fatos:

* O PlayReady é nativamente implementado em cada dispositivo com Windows, em alguns dispositivos com Android e está disponível em SDKs de software em praticamente qualquer plataforma
* O Widevine é nativamente implementado em cada dispositivo com Android, Chrome e alguns outros dispositivos
* O FairPlay está disponível apenas em clientes iOS e Mac OS, ou no iTunes.

Portanto, um típico DRM variado seria:

* Opção 1: PlayReady e Widevine
* Opção 2: PlayReady, Widevine e FairPlay

## <a name="a-reference-design"></a>Um design de referência
Nesta seção, vamos apresentar um design de referência que é desconhecido tootechnologies usado tooimplement-lo.

Um subsistema DRM pode conter Olá componentes a seguir:

1. Gerenciamento de chaves
2. Empacotamento de DRM
3. Entrega de licença do DRM
4. Verificação de autorização
5. Autenticação/autorização
6. Jogador
7. Origem/CDN

Olá diagrama a seguir ilustra interação de nível alto Olá entre componentes de saudação em um subsistema DRM.

![Subsistema DRM com CENC](./media/media-services-cenc-with-multidrm-access-control/media-services-generic-drm-subsystem-with-cenc.png)

Há três básico "camadas" no design de saudação:

1. A camada de back-office (em preto) que não é exposta externamente;
2. Camada de "Rede de Perímetro" (azul) que contém todos os pontos de extremidade Olá voltada para o público;
3. A camada de Internet pública (azul-clara) que contém CDN e players com tráfego pela Internet pública.

Deve haver uma ferramenta de gerenciamento de conteúdo para controlar a proteção do DRM, independentemente de a criptografia ser dinâmica ou estática. entradas de saudação para criptografia de DRM devem incluir:

1. Conteúdo de vídeo MBR;
2. Chave de conteúdo;
3. URLs de aquisição de licença.

Durante o tempo de reprodução, o fluxo de nível alto de saudação é:

1. O usuário é autenticado;
2. Token de autorização é criado para o usuário Olá;
3. Conteúdo protegido por DRM (manifesto) é baixado tooplayer;
4. Player envia os servidores de toolicense de solicitação de aquisição de licença junto com a ID de chave e autorização token.

Antes de mover próximo de tópico de toohello, algumas palavras sobre Olá design do gerenciamento de chaves.

| **ContentKey-para-ativo** | **Cenário** |
| --- | --- |
| 1 para 1 |caso mais simples de saudação. Ele fornece controle mais refinado hello. Mas, geralmente, resulta em custo de entrega de licença mais alto hello. Pelo menos uma solicitação de licença é necessária para cada ativo protegido. |
| 1-para-muitos |Você pode usar o mesmo conteúdo a chave de vários ativos de saudação. Por exemplo, para todos os ativos de saudação em um grupo lógico, como um gênero ou um subconjunto de gênero (ou filme Gene), você pode usar uma única chave de conteúdo. |
| Muitos-para-1 |Várias chaves de conteúdo são necessárias para cada ativo. <br/><br/>Por exemplo, se precisar de proteção de CENC dinâmica tooapply com várias DRM para MPEG-DASH e criptografia AES-128 dinâmica para HLS, será necessário duas separadas conteúdas chaves, cada qual com seu próprio ContentKeyType. (Para a chave de conteúdo do hello usada para proteção de CENC dinâmica, ContentKeyType.CommonEncryption deve ser usado, enquanto para Olá conteúdo chave usada para criptografia AES-128, ContentKeyType.EnvelopeEncryption deve ser usada.)<br/><br/>Outro exemplo, em proteção de CENC de traço de conteúdo, em tese, uma chave de conteúdo pode ser usado tooprotect fluxo de vídeo e outro fluxo de áudio tooprotect chave de conteúdo. |
| Muitos – muito-muitos |Combinação de saudação acima dois cenários: um conjunto de conteúdo, as chaves são usadas para cada um dos Olá ativos em Olá mesmo ativo "grupo". |

Tooconsider de outro fator importante é o uso de saudação de licenças persistentes e não persistentes.

Por que essas considerações são importantes?

Eles têm a entrega de toolicense impacto direto de custo se você usar a nuvem pública para entrega de licença. Vamos considerar Olá dois tooillustrate de casos de design diferentes a seguir:

1. Assinatura mensal: use a licença persistente e o mapeamento de chaves para ativos com conteúdo de um para muitos. Por exemplo para todos os filmes de crianças hello, usamos uma única chave de conteúdo para criptografia. Nesse caso:

    Número total de licenças solicitadas para todos os filmes de criança/dispositivo = 1
2. Assinatura mensal: use a licença não persistente e o mapeamento de um para um entre a chave e o ativo do conteúdo. Nesse caso:

    Número total de licenças solicitadas para todos os filmes de criança/dispositivo = [# de filmes observados] x [# de sessões]

Como você pode ver facilmente Olá dois projetos diferentes resultam na licença muito diferente solicitar padrões, portanto, se o serviço de entrega de licença é fornecido por uma nuvem pública, como os serviços de mídia do Azure de custo de entrega de licença.

## <a name="mapping-design-tootechnology-for-implementation"></a>Mapeamento de design tootechnology para implementação
Em seguida, podemos mapear tootechnologies nosso design genérico na plataforma Microsoft Azure/Azure Media Services, especificando quais toouse tecnologia para cada bloco de construção.

Olá tabela a seguir mostra o mapeamento de saudação:

| **Bloco de construção** | **Tecnologia** |
| --- | --- |
| **Player** |[Player de Mídia do Azure](https://azure.microsoft.com/services/media-services/media-player/) |
| **IDP (Provedor de identidade)** |Azure Active Directory |
| **STS (Serviço de Token Seguro)** |Azure Active Directory |
| **Fluxo de trabalho de proteção de DRM** |Proteção dinâmica dos Serviços de Mídia do Azure |
| **Entrega de licença do DRM** |1. Entrega de licença dos Serviços de Mídia do Azure (PlayReady, Widevine, FairPlay) ou <br/>2. Servidor de licença Axinom, <br/>3. Servidor de licença do PlayReady personalizado |
| **Origem** |Ponto de extremidade dos Serviços de Mídia do Azure |
| **Gerenciamento de Chaves** |Não é necessário para a implementação de referência |
| **Gerenciamento de Conteúdo** |Aplicativo do console C# |

Em outras palavras, tanto o IDP (provedor de identidade) quanto o STS (Serviço de Token Seguro) serão do AD do Azure. Para o player, usaremos a [API do Player de Mídia do Azure](http://amp.azure.net/libs/amp/latest/docs/). Os Serviços de Mídia do Azure e o Player de Mídia do Azure dão suporte a DASH e a CENC com vários DRM.

Olá seguinte diagrama mostra Olá estrutura geral e o fluxo com hello acima mapeamento de tecnologia.

![CENC em AMS](./media/media-services-cenc-with-multidrm-access-control/media-services-cenc-subsystem-on-AMS-platform.png)

Ordem tooset a criptografia dinâmica de CENC, ferramenta de gerenciamento de conteúdo Olá usará Olá entradas a seguir:

1. Abrir conteúdo;
2. Chave de conteúdo do gerenciamento/geração de chave;
3. URLs de aquisição de licença;
4. Uma lista de informações do AD do Azure.

Olá saída da ferramenta de gerenciamento de conteúdo de saudação será:

1. ContentKeyAuthorizationPolicy que contém a especificação de saudação em como entrega de licença verifica um token JWT e especificações de licença do DRM;
2. AssetDeliveryPolicy contendo especificações de formato de streaming, proteção DRM e URLs de aquisição de licença.

Durante a execução, o fluxo de saudação é como abaixo:

1. Após a autenticação de usuário, um token JWT é gerado;
2. Uma das declarações de saudação contidas no token JWT de saudação é declaração "groups" que contém a ID de objeto do grupo de saudação de "EntitledUserGroup". Essa declaração será usada para a passagem de "verificação de autorização".
3. Manifesto de cliente de downloads de Player de um CENC conteúdo protegido e seguir hello "vê":

   1. ID da chave;
   2. conteúdo de saudação é CENC protegido,
   3. URLs de aquisição de licença.
4. Player faz uma solicitação de aquisição de licença com base em Olá navegador/DRM com suporte. Na solicitação de aquisição de licença hello, ID de chave e Olá JWT token também será enviado. Serviço de entrega de licença verificará se o token JWT hello e declarações de saudação contidas antes de emitir Olá necessário licença.

## <a name="implementation"></a>Implementação
### <a name="implementation-procedures"></a>Procedimentos de implementação
implementação de saudação incluirá Olá etapas a seguir:

1. Preparar os ativos de teste: codificar/pacote uma teste de vídeo toomulti taxas de bits fragmentado MP4 nos serviços de mídia do Azure. Esse ativo NÃO é protegido por DRM. A proteção DRM será feita pela proteção dinâmica posteriormente.
2. Criar chave de ID e chave de conteúdo (opcionalmente da semente de chave). Para nosso objetivo, o sistema de gerenciamento de chaves não é necessário, pois estamos lidando com apenas um único conjunto de ID de chave ID e de chave de conteúdo para alguns recursos de teste;
3. Use os serviços de entrega de licença AMS API tooconfigure DRM várias ativo de teste de saudação. Se você estiver usando servidores de licença personalizado por sua empresa ou fornecedores de sua empresa em vez de serviços de licença nos serviços de mídia do Azure, você pode ignorar esta etapa e especificar URLs de aquisição de licença na etapa Olá para configurar a entrega de licença. API de AMS é necessário toospecify alguns detalhadas configurações, como restrição de política de autorização de licença modelos de resposta para diferentes serviços de licença do DRM, etc. Neste momento, Olá portal do Azure ainda não fornecer Olá necessária da interface do usuário para essa configuração. Você pode encontrar informações e códigos de exemplo no nível de API no documento de Julia Kornich: [Usando a criptografia dinâmica comum do PlayReady e/ou do Widevine](media-services-protect-with-drm.md).
4. Use política de entrega de ativos de tooconfigure AMS API para o ativo de teste de saudação. Você pode encontrar informações e códigos de exemplo no nível de API no documento de Julia Kornich: [Usando a criptografia dinâmica comum do PlayReady e/ou do Widevine](media-services-protect-with-drm.md).
5. Criar e configurar um locatário do Active Directory do Azure no Azure;
6. Criar algumas contas de usuário e grupos em seu locatário do Active Directory do Azure: você deve criar pelo menos "EntitledUser" e adicione um grupo de toothis do usuário. Os usuários desse grupo passará a verificação de autorização na aquisição da licença e os usuários não desse grupo falharão toopass verificação de autenticação e não será capaz de tooacquire qualquer licença. Ser um membro desse grupo "EntitledUser" é uma declaração de "grupos" necessários em Olá token JWT emitido pelo AD do Azure. Esse requisito de declaração deve ser especificado na etapa de configuração dos serviços de entrega de licença para vários DRM.
7. Crie um aplicativo MVC ASP.NET que hospedará o player de vídeo. Este aplicativo ASP.NET será protegido com a autenticação de usuário no locatário do Active Directory do Azure hello. Declarações apropriadas serão incluídas nos tokens de acesso Olá obtidos após a autenticação do usuário. A API Connect OpenID é recomendada para esta etapa. Você precisa Olá tooinstall pacotes do NuGet a seguir:
   * Install-Package Microsoft.Azure.ActiveDirectory.GraphClient
   * Install-Package Microsoft.Owin.Security.OpenIdConnect
   * Install-Package Microsoft.Owin.Security.Cookies
   * Install-Package Microsoft.Owin.Host.SystemWeb
   * Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
8. Crie um player usando a [API do Player de Mídia do Azure](http://amp.azure.net/libs/amp/latest/docs/). [API de ProtectionInfo do Azure Media Player](http://amp.azure.net/libs/amp/latest/docs/) permite que você toospecify quais toouse de tecnologia DRM em diferentes plataformas DRM.
9. Matriz de teste:

| **DRM** | **Navegador** | **Resultado de usuário qualificado** | **Resultado para usuário não qualificado** |
| --- | --- | --- | --- |
| **PlayReady** |MS Edge ou IE11 no Windows 10 |Êxito |Reprovado |
| **Widevine** |Chrome no Windows 10 |Êxito |Reprovado |
| **FairPlay** |TBD | | |

George Trifonov, da equipe de Serviços de Mídia do Azure, escreveu um blog fornecendo as etapas detalhadas de configuração do Active Directory do Azure para um aplicativo de player MVC do ASP.NET: [Integrate Azure Media Services OWIN MVC based app with Azure Active Directory and restrict content key delivery based on JWT claims](http://gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).

George também escreveu um blog sobre [JWT token Authentication in Azure Media Services and Dynamic Encryption](http://gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/). E aqui está seu [exemplo de integração do AD do Azure à distribuição de chaves dos Serviços de Mídia do Azure](https://github.com/AzureMediaServicesSamples/Key-delivery-with-AAD-integration/).

Para obter informações sobre o Active Directory do Azure:

* Você pode encontrar informações de desenvolvedor no [Guia do desenvolvedor do Active Directory do Azure](../active-directory/active-directory-developers-guide.md).
* Você pode encontrar informações de administrador em [Administrar seu diretório do AD do Azure](../active-directory/active-directory-administer.md).

### <a name="some-gotchas-in-implementation"></a>Algumas pegadinhas na implementação
Há algumas armadilhas"" na implementação de saudação. Esperamos que Olá lista de "armadilhas" a seguir pode ajudá-lo no caso de você se deparar com problemas de solução de problemas.

1. A URL do **emissor** deve terminar com **"/"**.  

    **Público-alvo** devem ser Olá ID do cliente de aplicativo de player e você também deve adicionar **"/"** final Olá Olá URL do emissor.

        <add key="ida:audience" value="[Application Client ID GUID]" />
        <add key="ida:issuer" value="https://sts.windows.net/[AAD Tenant ID]/" />

    Em [decodificador de JWT](http://jwt.calebb.net/), você deve ver **aud** e **iss** abaixo no token JWT hello:

    ![1ª pegadinha](./media/media-services-cenc-with-multidrm-access-control/media-services-1st-gotcha.png)
2. Adicione o aplicativo de toohello de permissões no AAD (na guia Configurar do aplicativo hello). Isso é necessário para cada aplicativo (versões locais e implantadas).

    ![2ª pegadinha](./media/media-services-cenc-with-multidrm-access-control/media-services-perms-to-other-apps.png)
3. Use o emissor de saudação à direita na configuração de proteção de CENC dinâmica:

        <add key="ida:issuer" value="https://sts.windows.net/[AAD Tenant ID]/"/>

    Olá seguinte não funcionará:

        <add key="ida:issuer" value="https://willzhanad.onmicrosoft.com/" />

    Olá GUID é o ID de locatário Olá AAD. Olá GUID pode ser encontrado no pop-up de pontos de extremidade no portal do Azure.
4. Conceder privilégios de declarações de associação de grupo. Certifique-se no arquivo de manifesto de aplicativo AAD, temos o seguinte Olá

    "groupMembershipClaims": "All" (o valor padrão de saudação é nulo)
5. Definir o TokenType apropriado durante a criação de requisitos de restrição.

        objTokenRestrictionTemplate.TokenType = TokenType.JWT;

    Como adicionar suporte de JWT (AAD) além do tooSWT (ACS), o padrão de saudação TokenType é TokenType.JWT. Se você usar o SWT/ACS, você deve definir tooTokenType.SWT.

## <a name="additional-topics-for-implementation"></a>Tópicos Adicionais para Implementação
Em seguida, iremos analisar alguns tópicos adicionais em nosso design e implementação.

### <a name="http-or-https"></a>HTTP ou HTTPS?
Olá aplicativo de player do ASP.NET MVC que criamos deve oferecer suporte a seguir hello:

1. Autenticação de usuário por meio do AD do Azure que precisa toobe em HTTPS.
2. Troca de token de JWT entre o cliente e o Azure AD que precisa toobe em HTTPS.
3. Aquisição de licença do DRM pelo cliente de saudação que é necessário toobe em HTTPS se a entrega de licença é fornecida pelos serviços de mídia do Azure. Obviamente, o pacote de produtos PlayReady não obriga HTTPS para entrega de licença. Se o servidor de licença do PlayReady estiver fora dos Serviços de Mídia do Azure, HTTP ou HTTPS poderão ser usados.

Portanto, Olá aplicativo de player ASP.NET usará o HTTPS como uma prática recomendada. Isso significa hello que Azure Media Player será uma página em HTTPS. No entanto, para streaming preferem HTTP, portanto, precisamos tooconsider misto problema conteúdo.

1. O navegador não permite conteúdo misto. Mas os plug-ins como o plug-in do Silverlight e do OSMF para smooth e DASH, sim. Conteúdo misto é uma preocupação de segurança - isso é devido a ameaça de toohello de saudação capacidade tooinject JS mal-intencionado que pode causar Olá toobe de dados do cliente em risco.  Esse bloqueiam navegadores por padrão e até o momento Olá toowork de maneira somente ao redor dele é no lado do servidor (origem) de hello, tooallow todos os domínios (independentemente https ou http). Isso provavelmente também não será uma boa ideia.
2. Devemos evitar conteúdo misto: ou ambos usam HTTP, ou ambos usam HTTPS. Durante a reprodução de conteúdo misto, a tecnologia silverlightSS exige a desmarcação de um aviso de conteúdo misto. A tecnologia flashSS lida com conteúdo misto sem aviso de conteúdo misto.
3. Se o ponto de extremidade de streaming foi criado antes de agosto de 2014, ele não dá suporte a HTTPS. Nesse caso, crie e use um novo ponto de extremidade de streaming para HTTPS.

Na implementação de referência de saudação para conteúdo protegido por DRM, aplicativo e o streaming será em HTTTPS. Para abrir o conteúdo, player Olá não precisa de autenticação ou licença, para que você tenha Olá liberty toouse o HTTP ou HTTPS.

### <a name="azure-active-directory-signing-key-rollover"></a>Substituição de chave de assinatura do Active Directory do Azure
Este é um tootake ponto importante em consideração de sua implementação. Se você não considere isto em sua implementação, sistema Olá concluída eventualmente deixarão de funcionar completamente dentro de no máximo de 6 semanas.

O AD do Azure usa setor tooestablish padrão confiança entre ele mesmo e aplicativos usando o Azure AD. Especificamente, o AD do Azure usa uma chave de assinatura que consiste em um par de chaves público e privado. Quando o AD do Azure cria um token de segurança que contém informações sobre o usuário hello, esse token é assinado pelo AD do Azure usando sua chave privada antes de serem enviado back toohello aplicativo. tooverify Olá token seja válido e realmente originado do AD do Azure, o aplicativo hello deve validar a assinatura do token hello usando a chave pública do hello exposto pelo AD do Azure que está contido no documento de metadados de Federação do locatário hello. Esta chave pública – e saudação da qual deriva de chave de assinatura – são hello mesmo aquele usado para todos os locatários no AD do Azure.

Informações detalhadas sobre a substituição de chave do AD do Azure podem ser encontradas no documento hello: [informações importantes sobre substituição de chave de assinatura no AD do Azure](../active-directory/active-directory-signing-key-rollover.md).

Entre hello [par de chaves públicas-privadas](https://login.microsoftonline.com/common/discovery/keys/),

* chave privada Olá é usado pelo Active Directory do Azure toogenerate um token JWT;
* chave pública de saudação é usada por um aplicativo, como serviços de distribuição de licença do DRM no token JWT de saudação do AMS tooverify;

Para fins de segurança, o Active Directory do Azure gira esse certificado periodicamente (a cada 6 semanas). No caso de violações de segurança, substituição de chave Olá pode ocorrer qualquer momento. Portanto, serviços de distribuição de licença Olá no AMS necessário chave pública do hello tooupdate usado como o AD do Azure gira o par de chaves hello, caso contrário, a autenticação de token em AMS falhará e nenhuma licença será emitida.

Isso é feito definindo TokenRestrictionTemplate.OpenIdConnectDiscoveryDocument ao configurar serviços de distribuição de licença do DRM.

Olá fluxo do token JWT é como abaixo:

1. AD do Azure emite o token de JWT Olá com chave privada atual de saudação para um usuário autenticado;
2. Quando um player vê um CENC com conteúdo protegido por DRM de várias, ele localizará primeiro token JWT de saudação emitido pelo AD do Azure.
3. player de saudação envia a solicitação de aquisição de licença com serviços de distribuição de toolicense token de JWT de saudação em AMS;
4. Serviços de distribuição de licença Olá no AMS usará Olá atual/uma chave pública válida do token JWT do AD do Azure tooverify hello, antes de emitir licenças.

Serviços de distribuição de licença do DRM sempre serão ser verificando Olá atual/uma chave pública válida do AD do Azure. chave pública de saudação apresentado pelo AD do Azure será chave Olá usado para verificar um token JWT emitido pelo AD do Azure.

E se substituição de chave Olá acontece depois AAD gera um token JWT, mas antes de saudação JWT token é enviado por jogadores tooDRM licença serviços de distribuição no AMS para verificação?

Como uma chave pode ser substituída em qualquer momento, há sempre mais de uma chave pública válida disponível no documento de metadados de Federação hello. Entrega de licença dos serviços de mídia do Azure pode usar qualquer um dos Olá chaves especificadas no documento hello, pois uma chave pode ser substituída em breve, outra pode ser seu substituição e assim por diante.

### <a name="where-is-hello-access-token"></a>Onde é Olá Token de acesso?
Se você examinar como um aplicativo web chama um aplicativo de API em [identidade do aplicativo com a concessão de credenciais de cliente OAuth 2.0](../active-directory/develop/active-directory-authentication-scenarios.md#web-application-to-web-api), é o fluxo de autenticação hello como abaixo:

1. Um usuário está conectado no tooAzure AD no aplicativo da web hello (consulte Olá [tooWeb do navegador da Web aplicativo](../active-directory/develop/active-directory-authentication-scenarios.md#web-browser-to-web-application).
2. ponto de extremidade de autorização de saudação do AD do Azure redireciona o agente do usuário de Olá toohello back aplicativo cliente com um código de autorização. agente do usuário Olá retorna o URI de redirecionamento do aplicativo do cliente toohello código autorização.
3. aplicativo da web Hello precisa tooacquire um token de acesso para que ele possa autenticar toohello web API e recuperar o recurso de saudação desejado. Faz uma tooAzure de solicitação do AD do ponto de extremidade token, fornecendo credenciais de hello, ID do cliente e URI de ID do aplicativo da API da web. Ele apresenta Olá tooprove de código de autorização que Olá usuário consentiu.
4. O AD do Azure autentica o aplicativo hello e retorna um token de acesso JWT que é usado toocall Olá web API.
5. Via HTTPS, o aplicativo da web hello usa Olá retornado Olá tooadd token de acesso JWT cadeia de caracteres JWT com uma designação "Portador" no cabeçalho de autorização de saudação da API da web do toohello Olá solicitação. Olá web API, em seguida, valida o token JWT hello e se a validação for bem-sucedida, retorna Olá desejado de recursos.

Nesse fluxo "identidade de aplicativo", Olá web API confia usuário Olá web aplicativo saudação autenticada. Por esse motivo, esse padrão é chamado de subsistema confiável. Olá [diagrama nesta página](https://docs.microsoft.com/azure/active-directory/active-directory-protocols-oauth-code) descreve como o código de autorização conceder fluxo funciona.

Na aquisição de licença com a restrição de token, podemos seguir Olá mesmo padrão de subsistema confiável. Serviço de entrega de licença Olá nos serviços de mídia do Azure é recurso Olá API da web hello "recursos de back-end" tooaccess precisa de um aplicativo da web. Onde está o token de acesso Olá?

Na verdade, podemos obter token de acesso do AD do Azure. Após a autenticação bem-sucedida do usuário, o código de autorização é retornado. código de autorização de saudação é usado, junto com a chave de ID e o aplicativo cliente, tooexchange de token de acesso. E o token de acesso Olá para acessar um aplicativo de "ponteiro" apontando ou que representa o serviço de entrega de licença de serviços de mídia do Azure.

Precisamos tooregister e configurar hello "ponteiro" aplicativo no AD do Azure seguindo as etapas de saudação abaixo:

1. No locatário de saudação do AD do Azure

   * adicione um aplicativo (recurso) com a URL de logon:

   https://[nome_do_recurso].azurewebsites.net/ e

   * URL da ID do aplicativo:

   https://[nome_do_locatário_aad].onmicrosoft.com/[nome_do_recurso];
2. Adicione uma nova chave para o aplicativo de recurso Olá;
3. Atualizar o arquivo de manifesto de aplicativo hello para que a propriedade de groupMembershipClaims Olá tem Olá seguinte valor: "groupMembershipClaims": "Todas",  
4. No aplicativo do AD do Azure Olá apontando toohello player web app, na seção hello "permissões tooother aplicativos", adicione Olá aplicativo de recurso que foi adicionado na etapa 1 acima. Em "permissões delegadas", verifique a marca de seleção de "Acessar [nome_recurso]". Isso dá permissão do aplicativo web hello toocreate tokens de acesso para acessar o aplicativo de recurso de saudação. Você deve fazer isso para a versão local e implantado do aplicativo de web hello, se você estiver desenvolvendo com o aplicativo web do Visual Studio e o Azure.

Portanto, token JWT de saudação emitido pelo AD do Azure é realmente token de acesso de saudação para acessar esse recurso de "ponteiro".

### <a name="what-about-live-streaming"></a>E quanto à Transmissão ao Vivo?
Em Olá acima, nossa discussão tem sido focando ativos sob demanda. E quanto à Transmissão ao Vivo?

Olá boa notícia é que você pode usar exatamente Olá mesmo design e implementação para proteger a transmissão ao vivo nos serviços de mídia do Azure, tratando ativo Olá associado a um programa como um ativo VOD"".

Especificamente, é bem conhecido que toodo live streaming nos serviços de mídia do Azure, é necessário toocreate um canal, em seguida, um programa em canal de saudação. programa de saudação toocreate, você precisa toocreate um ativo que conterá o arquivamento de dinâmico Olá para programa hello. Em ordem tooprovide CENC com proteção de várias DRM de conteúdo ao vivo Olá, tudo o que você precisa toodo, é tooapply Olá mesmo ativo toohello de instalação para o processamento como se fosse um ativo VOD"" antes de iniciar o programa de saudação.

### <a name="what-about-license-servers-outside-of-azure-media-services"></a>E os servidores de licença fora dos Serviços de Mídia do Azure?
Muitas vezes os clientes investiram em um farm de servidores de licença em seu próprio data center ou hospedado por provedores de serviço DRM. Felizmente, proteção de conteúdo do Azure Media Services permite que você toooperate no modo híbrido: conteúdo hospedado e dinamicamente protegida nos serviços de mídia do Azure, ao mesmo tempo licenças DRM são fornecidas pelos servidores fora do Azure Media Services. Nesse caso, há Olá considerações das alterações a seguir:

1. Olá serviço de Token seguro necessidades tooissue tokens que são aceitáveis e podem ser verificadas pelo farm de servidores de licença hello. Por exemplo, servidores de licenças Widevine Olá fornecidos pelo Axinom requer um token JWT específico que contém "mensagem de direitos". Portanto, você precisa toohave tooissue um STS tal token JWT. autores de saudação concluiu essa implementação e você pode encontrar detalhes de saudação em Olá seguindo o documento em [Centro de documentação do Azure](https://azure.microsoft.com/documentation/): [toodeliver Axinom usando Widevine licenças dos serviços de mídia tooAzure](media-services-axinom-integration.md).
2. Você não precisar mais serviço de entrega de licença tooconfigure (ContentKeyAuthorizationPolicy) nos serviços de mídia do Azure. O que você precisa é de toodo URLs de aquisição de licença tooprovide hello (para PlayReady, Widevine e FairPlay) quando você configura AssetDeliveryPolicy na configuração de CENC com DRM de várias.

### <a name="what-if-i-want-toouse-a-custom-sts"></a>E se eu desejar toouse um STS personalizado?
Pode haver alguns motivos que um cliente pode escolher toouse um STS personalizado (serviço de Token seguro) para fornecer tokens JWT. Alguns deles são:

1. Olá provedor de identidade (IDP) usado pelo cliente de saudação não oferece suporte para o STS. Nesse caso, um STS personalizado pode ser uma opção.
2. Prezado cliente talvez seja necessário mais flexível ou maior controle no STS integrando o assinante de cliente sistema de cobrança. Por exemplo, um operador MVPD pode oferecer vários pacotes de assinante OTT como premium, basic, tem, operador de saudação etc. Convém toomatch Olá declarações em um token com o pacote do assinante para que somente o conteúdo no pacote de saudação à direita é disponibilizada. Nesse caso, um STS personalizado fornece Olá necessário flexibilidade e controle.

Duas alterações necessário toobe feita ao usar um STS personalizado:

1. Ao configurar o serviço de entrega de licença para um ativo, você precisa de chave de segurança de saudação toospecify usado para verificação pelo STS personalizado hello (mais detalhes abaixo), em vez de chave atual de saudação do Active Directory do Azure.
2. Quando um token JTW é gerado, uma chave de segurança é especificada em vez da chave privada de saudação do certificado de saudação X509 atual no Active Directory do Azure.

Há dois tipos de chaves de segurança:

1. Chave simétrica: Olá a mesma chave é usada para gerar e verificar um token JWT;
2. Chave assimétrica: um par de chaves públicas-privadas no certificado é usado com a chave privada para criptografar/gerando um JWT token e hello chave pública para verificar o token Olá X509.

#### <a name="tech-note"></a>Nota técnica
Se você usar o .NET Framework / c# como sua plataforma de desenvolvimento, Olá X509 certificado usado para a chave assimétrica de segurança deve ter o comprimento da chave de pelo menos 2048. Este é um requisito da classe Olá System.IdentityModel.Tokens.X509AsymmetricSecurityKey no .NET Framework. Caso contrário, será lançada Olá a seguinte exceção:

IDX10630: Olá 'System.IdentityModel.Tokens.X509AsymmetricSecurityKey' para a assinatura não pode ser menor que '2048' bits.

## <a name="hello-completed-system-and-test"></a>teste e sistema Olá concluída
Vamos percorrer alguns cenários no sistema de ponta a ponta Olá concluída para que os leitores podem ter uma "imagem" do comportamento de saudação basic antes de obter uma conta de logon.

Olá aplicativo da web de player e seu logon podem ser encontrados [aqui](https://openidconnectweb.azurewebsites.net/).

Se você precisa é de "não integrado" cenário: ativos de vídeo hospedados nos serviços de mídia do Azure que são um desprotegido ou protegido por DRM, mas sem autenticação de token (uma toowhoever licença solicitá-la de emissão), você pode testá-lo sem logon (alternando tooHTTP se o streaming de vídeo é por HTTP).

Se você precisa é de cenário de ponta a ponta integrado: ativos de vídeo está sob proteção de DRM dinâmica nos serviços de mídia do Azure, com autenticação de token e o token JWT que está sendo gerada pelo AD do Azure, você precisa toologin.

### <a name="user-login"></a>Logon de usuário
Em ordem tootest Olá ponta a ponta DRM sistema integrado, você precisa toohave uma "conta" criados ou adicionados.

Qual conta?

Embora o Azure originalmente permitisse acesso somente por usuários de contas da Microsoft, ele agora permite o acesso por usuários de ambos os sistemas. Isso foi feito por ter confiança de propriedades Azure todos hello Azure AD para autenticação, com o AD do Azure autenticasse usuário institucionais e criando uma relação de Federação onde o AD do Azure confie o sistema de identidade de consumidor de conta do hello Microsoft usuários do consumidor tooauthenticate. Como resultado, o AD do Azure é tooauthenticate capaz de contas da Microsoft "convidado" como "nativas" contas do AD do Azure.

Desde que o AD do Azure confia no domínio de conta da Microsoft (MSA), você pode adicionar as contas de qualquer um dos Olá toohello domínios personalizados do AD do Azure a seguir de locatário e usam Olá conta toologin:

| **Nome de domínio** | **Domínio** |
| --- | --- |
| **Domínio de locatário do AD do Azure personalizado** |somename.onmicrosoft.com |
| **Domínio corporativo** |microsoft.com |
| **Domínio de MSA (Conta da Microsoft)** |outlook.com, live.com, hotmail.com |

Você pode contatar qualquer Olá autores toohave uma conta criada ou adicionadas para você.

Abaixo estão capturas de tela de saudação de páginas de logon diferentes usadas por diferentes contas de domínio.

**Conta de domínio de locatário do AD do Azure personalizado**: nesse caso, você ver a página de logon personalizada de saudação do domínio de locatário Olá personalizados do AD do Azure.

![Conta de domínio do locatário do AD do Azure personalizada](./media/media-services-cenc-with-multidrm-access-control/media-services-ad-tenant-domain1.png)

**Conta de domínio da Microsoft com cartão inteligente**: nesse caso você ver a página de logon Olá personalizada com a Microsoft corporativa IT com autenticação de dois fatores.

![Conta de domínio do locatário do AD do Azure personalizada](./media/media-services-cenc-with-multidrm-access-control/media-services-ad-tenant-domain2.png)

**Conta da Microsoft (MSA)**: nesse caso, você ver a página de logon de saudação do Account da Microsoft para consumidores.

![Conta de domínio do locatário do AD do Azure personalizada](./media/media-services-cenc-with-multidrm-access-control/media-services-ad-tenant-domain3.png)

### <a name="using-encrypted-media-extensions-for-playready"></a>Usando Extensões de Mídia Criptografada para PlayReady
Em um navegador moderno com criptografado mídia extensões (EME) para o PlayReady suporte, como navegador IE 11 no Windows 8.1 e backup e Microsoft Edge no Windows 10, PlayReady será hello DRM subjacente para EME.

![Usando EME para PlayReady](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-playready1.png)

área de player escuro Olá é devido fatos toohello proteção PlayReady impede que um façam a captura de tela de vídeo protegido.

Olá tela a seguir mostra plug-ins de player hello e suporte MSE/EME.

![Usando EME para PlayReady](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-playready2.png)

A EME no Microsoft Edge e no IE 11 no Windows 10 permite invocar o [PlayReady SL3000](https://www.microsoft.com/playready/features/EnhancedContentProtection.aspx/) em dispositivos com Windows 10 que o suportam. PlayReady SL3000 desbloqueia o fluxo de saudação do conteúdo premium avançado (4K, cabeçalho, etc.) e novos modelos de entrega de conteúdo (janela antecipado para aprimorar o conteúdo).

Se concentrar em dispositivos do Windows hello: PlayReady é Olá somente DRM no hello HW disponível em dispositivos do Windows (PlayReady SL3000). Um serviço de streaming pode usar o PlayReady por meio da EME ou de um aplicativo UWP e oferecer uma qualidade mais alta de vídeo usando o PlayReady SL3000 em vez de outro DRM. Normalmente, o conteúdo de 2K fluirá pelo Chrome ou Firefox e Olá de 4 K conteúdo por meio do Microsoft Edge/IE11 ou um aplicativo de UWP no mesmo dispositivo (dependendo da configuração de serviço e implementação).

#### <a name="using-eme-for-widevine"></a>Usando EME para Widevine
Em um navegador moderno com suporte no Android 4.4.4, EME/Widevine, como Chrome 41 + no Windows 10, Windows 8.1, Mac OSX Yosemite e Chrome Google Widevine é hello DRM atrás EME.

![Usando EME para Widevine](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-widevine1.png)

Observe que o Widevine não impede a captura de tela de vídeo protegido.

![Usando EME para Widevine](./media/media-services-cenc-with-multidrm-access-control/media-services-eme-for-widevine2.png)

### <a name="not-entitled-users"></a>Usuários não qualificados
Se um usuário não for um membro do grupo "Usuários intitulada", usuário Olá não será capaz de toopass "verificação de qualificação" e serviço de licença do DRM várias Olá recusará a licença solicitada do tooissue Olá conforme mostrado abaixo. Olá descrição detalhada é "adquirir licença falha", que é criado.

![Usuários não qualificados](./media/media-services-cenc-with-multidrm-access-control/media-services-unentitledusers.png)

### <a name="running-custom-secure-token-service"></a>Executando Serviço de Token Seguro personalizado
Para o cenário de saudação da execução personalizada Token STS (serviço seguro), token JWT Olá será emitido pelo STS personalizado hello usando chave simétrica ou assimétrica.

caso de saudação do uso de chave simétrica (usando o Chrome):

![Executando STS personalizado](./media/media-services-cenc-with-multidrm-access-control/media-services-running-sts1.png)

Olá caso de uso de chave assimétrica via X509 do certificado (usando o navegador moderno da Microsoft).

![Executando STS personalizado](./media/media-services-cenc-with-multidrm-access-control/media-services-running-sts2.png)

Em ambos Olá acima casos, a autenticação de usuário permanece Olá mesmo – por meio do AD do Azure. Olá única diferença é que os tokens JWT são emitidos pelo STS personalizado de saudação em vez do AD do Azure. É claro que, ao configurar a proteção de CENC dinâmica, restrição de saudação do serviço de entrega de licença especifica tipo de Olá de token JWT, chave simétrica ou assimétrica.

## <a name="summary"></a>Resumo
Neste documento, vimos CENC com vários DRM nativos e controle de acesso por meio de autenticação de token; seu design e sua implementação usando o Azure, os Serviços de Mídia do Azure e o Player de Mídia do Azure.

* Um projeto de referência é apresentado, que contém todos os componentes necessários do hello em um subsistema DRM/CENC;
* Uma implementação de referência no Azure, nos Serviços de Mídia do Azure e no Player de Mídia do Azure.
* Alguns tópicos diretamente envolvidas na implementação e design de saudação também são discutidos.

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
 
