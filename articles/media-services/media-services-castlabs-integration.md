---
title: "aaaUsing castLabs toodeliver Widevine licenças dos serviços de mídia tooAzure | Microsoft Docs"
description: "Este artigo descreve como você pode usar os serviços de mídia do Azure (AMS) toodeliver um fluxo criptografado dinamicamente pelo AMS com PlayReady e Widevine DRMs. licença do PlayReady Hello proveniente do servidor de licença do PlayReady dos serviços de mídia e licenças Widevine é fornecida pelo servidor de licença castLabs."
services: media-services
documentationcenter: 
author: Mingfeiy
manager: cfowler
editor: 
ms.assetid: 2a9a408a-a995-49e1-8d8f-ac5b51e17d40
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: Mingfeiy;willzhan;Juliako
ms.openlocfilehash: 80d2778fb283a96361e7e511990a36c2f551a310
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-castlabs-toodeliver-widevine-licenses-tooazure-media-services"></a>Usando castLabs toodeliver Widevine licenças tooAzure serviços de mídia
> [!div class="op_single_selector"]
> * [Axinom](media-services-axinom-integration.md)
> * [castLabs](media-services-castlabs-integration.md)
> 
> 

## <a name="overview"></a>Visão geral
Este artigo descreve como você pode usar os serviços de mídia do Azure (AMS) toodeliver um fluxo criptografado dinamicamente pelo AMS com PlayReady e Widevine DRMs. licença do PlayReady Hello proveniente do servidor de licença do PlayReady dos serviços de mídia e licenças Widevine é entregue por **castLabs** servidor de licença.

tooplayback streaming de conteúdo protegido por CENC (PlayReady e/ou Widevine), você pode usar [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html). Consulte o [documento sobre AMP](http://amp.azure.net/libs/amp/latest/docs/) para obter detalhes.

Olá diagrama a seguir demonstra uma arquitetura de integração de serviços de mídia do Azure e castLabs alto nível.

![integração](./media/media-services-castlabs-integration/media-services-castlabs-integration.png)

## <a name="typical-system-set-up"></a>Configuração típica do sistema
* O conteúdo de mídia é armazenado em AMS.
* As IDs de chave de chaves de conteúdo são armazenados em castLabs e AMS.
* O castLabs e o AMS têm autenticação de token interna. Olá seções a seguir discutem os tokens de autenticação. 
* Quando um cliente solicita o vídeo de saudação toostream, conteúdo de saudação dinamicamente é criptografado com **criptografia comum** (CENC) e empacotado dinamicamente pelo AMS tooSmooth Streaming e traço. Também fornecemos criptografia de fluxo elementar PlayReady M2TS para protocolo de streaming do HLS.
* A licença do PlayReady é recuperada do servidor de licença do AMS e a licença Widevine é recuperada do servidor de licenças castLabs. 
* Media Player decide quais toofetch de licença com base na capacidade de plataforma de cliente Olá automaticamente. 

## <a name="authentication-token-generation-for-getting-a-license"></a>Geração de token de autenticação para obter uma licença
CastLabs e AMS suporte JWT (JSON Web Token) formato do token usado tooauthorize uma licença. 

### <a name="jwt-token-in-ams"></a>Token JWT no AMS
Olá, a tabela a seguir descreve o token JWT no AMS. 

| Emissor | Cadeia de caracteres do emissor de saudação escolhida Token STS (serviço seguro) |
| --- | --- |
| Público-alvo |Cadeia de caracteres de público-alvo de saudação usada STS |
| Declarações |Um conjunto de declarações |
| NotBefore |Iniciar a validade do token Olá |
| Expira |Final de validade do token Olá |
| SigningCredentials |chave de saudação que é compartilhado entre o servidor de licença do PlayReady, castLabs servidor de licença e STS, poderia ser chave simétrica ou assimétrica. |

### <a name="jwt-token-in-castlabs"></a>Token JWT no castLabs
Olá, a tabela a seguir descreve o token JWT no castLabs. 

| Nome | Descrição |
| --- | --- |
| optData |Uma cadeia de caracteres JSON que contém informações sobre você. |
| crt |Uma JSON cadeia de caracteres que contêm informações sobre ativos hello, seus direitos de reprodução e informações de licença. |
| iat |Olá data e hora atuais na época. |
| jti |Um identificador exclusivo sobre esse token (cada token pode somente ser usado uma vez no sistema de castLabs Olá). |

## <a name="sample-solution-set-up"></a>Configuração da solução de exemplo
Olá [solução de exemplo](https://github.com/AzureMediaServicesSamples/CastlabsIntegration) consiste em dois projetos:

* Um aplicativo de console que pode ser restrições de DRM tooset usado em um ativo já ingerido, para PlayReady e Widevine.
* Um aplicativo da Web que distribui os tokens, que poderia ser visto como uma versão MUITO SIMPLIFICADA de um STS.

aplicativo de console hello toouse:

1. Alterar credenciais de toosetup AMS Olá App. config, castLabs credenciais, configuração de STS e uma chave compartilhada.
2. Carregue um ativo no AMS.
3. Get hello UUID de saudação carregado ativo e alterar 32 de linha no arquivo Program.cs de saudação:
   
      var objIAsset = _context.Assets.Where(x => x.Id == "nb:cid:UUID:dac53a5d-1500-80bd-b864-f1e4b62594cf").FirstOrDefault();
4. Use um AssetId para nomear ativo Olá no sistema de castLabs hello (44 linha no arquivo Program.cs de saudação).
   
   Você deve definir AssetId para **castLabs**; ele precisa toobe uma cadeia de caracteres alfanumérica exclusiva.
5. Execute o programa de saudação.

Olá toouse aplicativo Web (STS):

1. Loja de castlabs alteração Olá Web. config toosetup ID, configuração de STS hello e uma chave compartilhada hello.
2. Implante tooAzure sites.
3. Navegue toohello site.

## <a name="playing-back-a-video"></a>Reproduzir um vídeo
um vídeo de tooplayback criptografada com criptografia comum (PlayReady e/ou Widevine), você pode usar o hello [Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html). Ao executar o aplicativo de console hello, Olá ID de chave de conteúdo e hello URL de manifesto são exibidos.

1. Abra uma nova guia e inicie seu STS: http://[yourStsName].azurewebsites.net/api/token/assetid/[yourCastLabsAssetId]/contentkeyid/[thecontentkeyid].
2. Vá muito[Azure Media Player](http://amsplayer.azurewebsites.net/azuremediaplayer.html).
3. Cole Olá URL de streaming.
4. Clique em Olá **opções avançadas de** caixa de seleção.
5. Em Olá **proteção** lista suspensa, selecione PlayReady e/ou Widevine.
6. Cole o token Olá que você obteve seu STS na caixa de texto de Token hello. 
   
   servidor de licença do Hello castLab não precisa hello "portador =" prefixo na frente do token de saudação. Então remova que antes de enviar o token hello.
7. Atualize o player de saudação.
8. Olá vídeo deve ser executado.

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

