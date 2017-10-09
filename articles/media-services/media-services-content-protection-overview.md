---
title: "aaaProtect seu conteúdo com os serviços de mídia do Azure | Microsoft Docs"
description: "Este artigo fornece uma visão geral da proteção de conteúdo com os Serviços de Mídia."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 81bc00e1-dcda-4d69-b9ab-8768b793422b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: abab7602d71d7357a692976420ca9a988c0d096f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-content-overview"></a>Visão geral sobre a proteção de conteúdo
Serviços de mídia do Microsoft Azure permite que você toosecure sua mídia do tempo de saudação deixa o computador por meio de armazenamento, processamento e entrega. Serviços de mídia permitem toodeliver seu conteúdo ao vivo e sob demanda dinamicamente criptografado com AES Advanced Encryption Standard () (usando chaves de criptografia de 128 bits) ou qualquer um dos Olá DRMs principais: Microsoft PlayReady, Google Widevine e FairPlay da Apple. Serviços de mídia também fornece um serviço para distribuir chaves AES e DRM (PlayReady, Widevine e FairPlay) licencia tooauthorized clientes. 

Olá a imagem a seguir demonstra a fluxos de trabalho de proteção de conteúdo de saudação que AMS oferece suporte. 

![Proteger com o PlayReady](./media/media-services-content-protection-overview/media-services-content-protection-with-multi-drm.png)

>[!NOTE]
>Quando sua conta AMS é criada um **padrão** ponto de extremidade de streaming é adicionada conta tooyour Olá **parado** estado. toostart streaming seu conteúdo e execute aproveitar o empacotamento dinâmico e criptografia dinâmica, Olá ponto de extremidade de streaming do qual você deseja toostream conteúdo tem toobe em Olá **executando** estado. 

Este tópico explica [conceitos e terminologia](media-services-content-protection-overview.md) toounderstanding relevantes de proteção de conteúdo com AMS. Olá tópico também contém [links](media-services-content-protection-overview.md#common-scenarios) tootopics que mostram como tooachieve tarefas de proteção de conteúdo. 

## <a name="dynamic-encryption"></a>Criptografia dinâmica
Serviços de mídia do Microsoft Azure permite que você toodeliver seu conteúdo dinamicamente criptografado com chave não criptografada AES ou criptografia DRM: Microsoft PlayReady, Google Widevine e FairPlay da Apple.

No momento, você pode criptografar Olá seguintes formatos de streaming: Smooth Streaming, MPEG DASH e HLS. Não é possível criptografar downloads progressivos.

Se você quiser para serviços de mídia tooencrypt um ativo, você precisa tooassociate uma chave de criptografia (CommonEncryption ou EnvelopeEncryption) com seu ativo e também configurar políticas de autorização para a chave de saudação.

Você também precisa de política de distribuição do ativo de saudação tooconfigure. Se você quiser toostream um ativo de armazenamento criptografado, verifique se toospecify como você deseja toodelivê-lo ao configurar a política de entrega de ativos.

Quando um fluxo é solicitado por um player, o Media Services usa Olá especificado toodynamically chave criptografar seu conteúdo usando a chave não criptografada AES ou a criptografia de DRM. fluxo de saudação toodecrypt, player Olá solicitar chave Olá do serviço de distribuição de chaves de saudação. toodecide ou não usuário Olá é autorizado chave de saudação tooget, serviço Olá avalia as políticas de autorização de saudação que você especificou para a chave de saudação.


## <a name="storage-encryption"></a>Criptografia do armazenamento
Use tooencrypt de criptografia de armazenamento o conteúdo limpo localmente usando a criptografia AES de 256 bits e, em seguida, carregá-lo tooAzure armazenamento onde ele está armazenado criptografado em repouso. Ativos protegidos pela criptografia de armazenamento são descriptografados automaticamente e posicionados em um tooencoding anterior do sistema de arquivos criptografados e, opcionalmente, criptografada novamente toouploading anterior como um novo ativo de saída. caso de uso primário Olá para criptografia de armazenamento é quando você deseja toosecure seus arquivos de mídia de entrada de alta qualidade com criptografia forte em rest no disco.

Ordem toodeliver um ativo de armazenamento criptografado, você deve configurar a política de distribuição do ativo Olá para que serviços de mídia saibam como você deseja toodeliver seu conteúdo. Antes do ativo pode ser transmitido, Olá streaming fluxos e criptografia de armazenamento de saudação do servidor remove o conteúdo usando Olá especificado política de entrega (por exemplo, AES, criptografia comum ou sem criptografia).

## <a name="common-encryption-cenc"></a>Criptografia comum (CENC)
A criptografia comum é usada ao criptografar o conteúdo com PlayReady e/ou Widewine.

## <a name="using-cbcs-aapl-encryption"></a>Usando a criptografia cbcs-aapl
Cbcs-aapl é usado ao criptografar seu conteúdo com o FairPlay.

## <a name="envelope-encryption"></a>Criptografia de envelope
Use esta opção se você quiser tooprotect seu conteúdo com a chave não criptografada AES-128. Se você quiser uma opção mais segura, escolha uma saudação DRMs listadas neste tópico. 

## <a name="licenses-and-keys-delivery-service"></a>Serviço de entrega de licenças e chaves
Serviços de mídia fornecem um serviço para distribuir licenças do DRM (PlayReady, Widevine, FairPlay) e os clientes tooauthorized de chaves não criptografada AES. Você pode usar [Olá portal do Azure](media-services-portal-protect-content.md), API REST ou o SDK do Media Services para políticas de autenticação e autorização de tooconfigure de .NET para suas licenças e chaves.

## <a name="token-restriction"></a>Restrição de token
Olá política de autorização da chave de conteúdo pode ter uma ou mais restrições de autorização: abrir ou restrição de token. política de restrição de token de saudação deve ser acompanhada por um token emitido por um Token STS (serviço seguro). Serviços de mídia oferece suporte a tokens no formato do Simple Web Tokens (SWT) hello e JSON Web Token (JWT). Os serviços de mídia não fornecem Secure Token Services. Você pode criar um STS personalizado ou utilizar a tokens de tooissue ACS do Microsoft Azure. Olá STS deve ser configurado toocreate um token assinado com hello especificado chave e emitir declarações que você especificou na configuração de restrição de token hello. Serviços de mídia Olá serviço de entrega de chave retornará Olá solicitado hello e chave (ou licença) cliente toohello se Olá token for válido declarações em Olá token correspondam às configuradas para chave hello (ou licença).

Ao configurar a política de restrição de token do hello, você deve especificar a chave de verificação primária hello, emissor e parâmetros de público-alvo. chave de verificação primária Olá contém Olá chave que Olá token foi assinado com, o emissor é Olá serviço de token seguro que emite o token de saudação. público Hello (às vezes chamado de escopo) descreve a intenção de saudação do token de saudação ou token de saudação do recurso de saudação autoriza o acesso ao. Olá serviço de distribuição de chaves de serviços de mídia valida que esses valores no token Olá correspondem a valores de saudação no modelo de saudação.

## <a name="streaming-urls"></a>URLs de streaming
Se seu ativo foi criptografado com DRM de mais de um, você deve usar uma marca de criptografia na URL de streaming de saudação: (formato = 'm3u8-aapl', criptografia = 'xxx').

Olá considerações a seguir se aplicam:

* Pode ser especificado apenas zero ou um tipo de criptografia.
* Tipo de criptografia não tem toobe especificado na url de saudação se apenas uma criptografia foi aplicada toohello ativo.
* O tipo de criptografia diferencia as letras maiúsculas de minúsculas.
* Olá seguintes tipos de criptografia pode ser especificada:  
  * **cenc**: criptografia comum (Playready ou Widevine)
  * **cbcs-aapl**: Fairplay
  * **cbc**: criptografia de envelope AES.

## <a name="common-scenarios"></a>Cenários comuns
Olá tópicos a seguir demonstram como tooprotect conteúdo no armazenamento, entregar criptografado dinamicamente o streaming de mídia, use o serviço de entrega de chave ou a licença AMS

* [Proteger com o AES](media-services-protect-with-aes128.md) 
* [Proteger com o PlayReady e/ou Widevine ](media-services-protect-with-drm.md)
* [Transmitir seu conteúdo HLS Protegido com o Apple FairPlay e/ou PlayReady](media-services-protect-hls-with-fairplay.md)

### <a name="additional-scenarios"></a>Cenários adicionais
* [Como toointegrate licença do PlayReady Azure serviço com seu próprio servidor Criptografador/streaming](http://mingfeiy.com/integrate-azure-playready-license-service-encryptorstreaming-server).
* [Usando castLabs toodeliver DRM licenças tooAzure serviços de mídia](media-services-castlabs-integration.md)

>[!NOTE]
>Um cenário no qual você usa um servidor (tecnologia) DRM externo e, atualmente, não há suporte ao fluxo do AMS.


## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a>Links relacionados
[Anunciando o PlayReady como um serviço e a criptografia dinâmica AES com os Serviços de Mídia do Azure](http://mingfeiy.com/playready)

[Explicação dos preços de entrega da licença do PlayReady dos Serviços de Mídia do Azure](http://mingfeiy.com/playready-pricing-explained-in-azure-media-services)

[Como toodebug AES criptografada fluxo nos serviços de mídia do Azure](http://mingfeiy.com/debug-aes-encrypted-stream-azure-media-services)

[Autenticação do token JWT](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/)

<seg>
  [Integrar o aplicativo do MVC OWIN dos serviços de mídia do Azure com base no aplicativo com Active Directory do Azure e restringir o fornecimento da chave de conteúdo com base em declarações JWT](http://www.gtrifonov.com/2015/01/24/mvc-owin-azure-media-services-ad-integration/).</seg>

[Usar tokens do Azure ACS tooissue](http://mingfeiy.com/acs-with-key-services).

[content-protection]: ./media/media-services-content-protection-overview/media-services-content-protection.png
