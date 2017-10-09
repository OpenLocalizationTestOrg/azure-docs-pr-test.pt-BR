---
title: "políticas de proteção de conteúdo aaaConfiguring usando Olá portal do Azure | Microsoft Docs"
description: "Este artigo demonstra como toouse Olá políticas de proteção de conteúdo tooconfigure portal do Azure. Olá artigo também mostra como a criptografia dinâmica tooenable para seus ativos."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 270b3272-7411-40a9-ad42-5acdbba31154
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: juliako
ms.openlocfilehash: 3e7ce6ddaa0e738b5a1e26dafe9eef2df221f039
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-content-protection-policies-using-hello-azure-portal"></a>Configurando políticas de proteção de conteúdo usando Olá portal do Azure
> [!NOTE]
> toocomplete neste tutorial, você precisa de uma conta do Azure. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
> 
> 

## <a name="overview"></a>Visão geral
Microsoft Azure Media Services (AMS) permite que você toosecure sua mídia do tempo de saudação deixa o computador por meio de armazenamento, processamento e entrega. Serviços de mídia permitem toodeliver seu conteúdo criptografado dinamicamente com Advanced Encryption Standard (AES) (usando chaves de criptografia de 128 bits), criptografia comum (CENC) usando PlayReady e/ou Widevine DRM e FairPlay da Apple. 

AMS fornece um serviço para distribuir licenças do DRM e clientes de tooauthorized chaves não criptografada AES. Hello portal do Azure permite que você toocreate um **diretiva de autorização de chave/licença** para todos os tipos de criptografia.

Este artigo demonstra como tooconfigure conteúdo políticas de proteção com hello portal do Azure. Olá artigo também mostra como ativos de tooyour tooapply criptografia dinâmica.


> [!NOTE]
> Se você usou as políticas de proteção do hello toocreate de portal clássico do Azure, as políticas de saudação podem não aparecer no hello [portal do Azure](https://portal.azure.com/). No entanto, todos os Olá antigo políticas ainda existe. Você pode examiná-los usando Olá SDK do Azure Media Services .NET ou hello [Azure-Media Services Explorer](https://github.com/Azure/Azure-Media-Services-Explorer/releases) ferramenta (políticas de saudação toosee, com o botão direito no ativo de saudação -> exibição informações (F4) -> clique na guia -> chaves de conteúdo Clique na chave de saudação). 
> 
> Se você quiser tooencrypt seu ativo usando as novas políticas, configurá-los com hello portal do Azure, clique em Salvar e reaplicar criptografia dinâmica. 
> 
> 

## <a name="start-configuring-content-protection"></a>Iniciar a configuração da proteção de conteúdo
toouse Olá portal toostart, configurando a proteção de conteúdo, conta tooyour global AMS, Olá a seguir:

1. Em Olá [portal do Azure](https://portal.azure.com/), selecione sua conta de serviços de mídia do Azure.
2. Selecione **Configurações** > **Proteção de conteúdo**.

![Proteger conteúdo](./media/media-services-portal-content-protection/media-services-content-protection001.png)

## <a name="keylicense-authorization-policy"></a>política de autorização de chave/licença
O AMS oferece várias maneiras de autenticar os usuários que fazem solicitações de licença ou chave. política de autorização da chave de conteúdo Olá deve ser configurada por você e cumprida pelo cliente para Olá chave ou a licença toobe toohello delived cliente. Olá política de autorização da chave de conteúdo pode ter uma ou mais restrições de autorização: **abrir** ou **token** restrição.

Hello portal do Azure permite que você toocreate um **diretiva de autorização de chave/licença** para todos os tipos de criptografia.

### <a name="open"></a>Aberto
Restrição aberta significa que o sistema de saudação distribuirá Olá tooanyone chave que faz uma solicitação de chave. Essa restrição pode ser útil para o teste. 

### <a name="token"></a>Token
política de restrição de token de saudação deve ser acompanhada por um token emitido por um Token STS (serviço seguro). Serviços de mídia oferece suporte a tokens no formato do Simple Web Tokens (SWT) hello e JSON Web Token (JWT). Os serviços de mídia não fornecem Secure Token Services. Você pode criar um STS personalizado ou utilizar a tokens de tooissue ACS do Microsoft Azure. Olá STS deve ser configurado toocreate um token assinado com hello especificado chave e emitir declarações que você especificou na configuração de restrição de token hello. Serviços de mídia Olá serviço de entrega de chave retornará Olá solicitado hello e chave (ou licença) cliente toohello se Olá token for válido declarações em Olá token correspondam às configuradas para chave hello (ou licença).

Ao configurar a política de restrição de token do hello, você deve especificar parâmetros de público-alvo, emissor e chave de verificação primária hello. chave de verificação primária Olá contém Olá chave que Olá token foi assinado com, o emissor é Olá serviço de token seguro que emite o token de saudação. público Hello (às vezes chamado de escopo) descreve a intenção de saudação do token de saudação ou token de saudação do recurso de saudação autoriza o acesso ao. Olá serviço de distribuição de chaves de serviços de mídia valida que esses valores no token Olá correspondem a valores de saudação no modelo de saudação.

![Proteger conteúdo](./media/media-services-portal-content-protection/media-services-content-protection002.png)

## <a name="playready-rights-template"></a>Modelo de direitos do PlayReady
Para obter informações detalhadas sobre o modelo de direitos Olá PlayReady, consulte [visão geral do modelo de licença do Media Services PlayReady](media-services-playready-license-template-overview.md).

### <a name="non-persistent"></a>Não persistente
Se você configurar a licença como não persistente, ele só é mantido na memória enquanto player hello está usando a licença de saudação.  

![Proteger conteúdo](./media/media-services-portal-content-protection/media-services-content-protection003.png)

### <a name="persistent"></a>Persistente
Se você configurar a licença hello como persistente, ele será salvo no armazenamento persistente no cliente de saudação.

![Proteger conteúdo](./media/media-services-portal-content-protection/media-services-content-protection004.png)

## <a name="widevine-rights-template"></a>Modelo de direitos do Widevine
Para obter informações detalhadas sobre o modelo de direitos de Widevine hello, consulte [visão geral do modelo de licença Widevine](media-services-widevine-license-template-overview.md).

### <a name="basic"></a>Basic
Quando você seleciona **básica**, Olá modelo será criado com todos os valores padrões.

### <a name="advanced"></a>Avançado
Para obter uma explicação detalhada sobre a opção avançada das configurações do Widevine, consulte [este](media-services-widevine-license-template-overview.md) tópico.

![Proteger conteúdo](./media/media-services-portal-content-protection/media-services-content-protection005.png)

## <a name="fairplay-configuration"></a>Configuração do FairPlay
tooenable FairPlay criptografia, necessárias tooprovide Olá certificado do aplicativo e a chave de segredo do aplicativo (SOLICITAR) por meio de saudação opção de configuração FairPlay. Para obter informações detalhadas sobre a configuração e os requisitos do FairPlay, consulte [este](media-services-protect-hls-with-fairplay.md) artigo.

![Proteger conteúdo](./media/media-services-portal-content-protection/media-services-content-protection006.png)

## <a name="apply-dynamic-encryption-tooyour-asset"></a>Aplicar o ativo de tooyour criptografia dinâmica
tootake vantagem da criptografia dinâmica, você precisa de tooencode seu arquivo de origem em um conjunto de arquivos MP4 com taxa de bits adaptável.

### <a name="select-an-asset-that-you-want-tooencrypt"></a>Selecione um ativo que você deseja tooencrypt
Selecione de todos os seus ativos, toosee **configurações** > **ativos**.

![Proteger conteúdo](./media/media-services-portal-content-protection/media-services-content-protection007.png)

### <a name="encrypt-with-aes-or-drm"></a>Criptografar com AES ou DRM
Depois de pressionar **Criptografar** em um ativo, você verá duas opções: **AES** ou **DRM**. 

#### <a name="aes"></a>AES
A criptografia da chave de limpeza do AES será habilitada em todos os protocolos de streaming: Smooth Streaming, HLS e MPEG-DASH.

![Proteger conteúdo](./media/media-services-portal-content-protection/media-services-content-protection008.png)

#### <a name="drm"></a>DRM
Quando você seleciona Olá DRM guia, você verá diferentes opções de políticas de proteção de conteúdo (que você deve ter configurado agora) + um conjunto de protocolos de streaming.

* **PlayReady e Widevine com o MPEG-DASH** - irão criptografar dinamicamente seu fluxo MPEG DASH com os DRMs do PlayReady e do Widevine.
* **PlayReady e Widevine com o MPEG-DASH+ FairPlay com HLS** - irão criptografar dinamicamente seu fluxo MPEG DASH com os DRMs do PlayReady e do Widevine. Também irão criptografar seus fluxos HLS com o FairPlay.
* **PlayReady somente com Smooth Streaming, HLS e MPEG-DASH** - irão criptografar dinamicamente o Smooth Streaming, HLS e fluxos MPEG-DASH com o DRM do PlayReady.
* **Widevine apenas com MPEG-DASH** - irá criptografar dinamicamente seu MPEG-DASH com o DRM do Widevine.
* **FairPlay apenas com HLS** - irá criptografar dinamicamente seu fluxo HLS com o FairPlay.

tooenable FairPlay criptografia, necessárias tooprovide Olá certificado do aplicativo e a chave de segredo do aplicativo (SOLICITAR) por meio de saudação opção de configuração de FairPlay da folha de configurações de proteção de conteúdo de saudação.

![Proteger conteúdo](./media/media-services-portal-content-protection/media-services-content-protection009.png)

Depois de fazer a seleção de criptografia hello, pressione **aplicar**.

>[!NOTE] 
>Se você estiver planejando tooplay um AES criptografado HLS no Safari, consulte [este blog](https://azure.microsoft.com/blog/how-to-make-token-authorized-aes-encrypted-hls-stream-working-in-safari/).

## <a name="next-steps"></a>Próximas etapas
Examine os roteiros de aprendizagem dos Serviços de Mídia.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

