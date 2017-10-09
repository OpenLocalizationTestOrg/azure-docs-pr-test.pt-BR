---
title: "aaaConfigure política de autorização de chave de conteúdo usando Olá portal do Azure | Microsoft Docs"
description: "Saiba como tooconfigure uma política de autorização para uma chave de conteúdo."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ee82a3fa-c34b-48f2-a108-8ba321f1691e
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: 157fb691b7f71f4889228817e1dc64555e327d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-content-key-authorization-policy"></a>Configurar a Política de Autorização de Chave de Conteúdo
[!INCLUDE [media-services-selector-content-key-auth-policy](../../includes/media-services-selector-content-key-auth-policy.md)]

## <a name="overview"></a>Visão geral
Serviços de mídia do Microsoft Azure permite que você toodeliver MPEG-DASH, Smooth Streaming e fluxos de HTTP-Live-Streaming (HLS) protegidos com Advanced Encryption Standard (AES) (usando chaves de criptografia de 128 bits) ou [Microsoft PlayReady DRM](https://www.microsoft.com/playready/overview/). AMS também permite que você toodeliver DASH streams criptografados com Widevine DRM. PlayReady e Widevine são criptografados por Olá especificação de criptografia comum (ISO/IEC 23001-7 CENC).

Serviços de mídia também fornecem um **serviço de entrega de chave ou a licença** dos quais os clientes podem obter chaves AES ou tooplay de licenças do PlayReady/Widevine Olá conteúdo criptografado.

Este tópico mostra como toouse Olá política de autorização da chave de conteúdo de saudação tooconfigure portal do Azure. chave Olá pode ser usado posteriormente toodynamically criptografar seu conteúdo. Observe que no momento você pode criptografar Olá seguintes formatos de streaming: Smooth Streaming, MPEG DASH e HLS. Não é possível criptografar downloads progressivos.

Quando um player solicita um fluxo que é definido toobe dinamicamente criptografado, o Media Services usa Olá configurado chave toodynamically criptografar o conteúdo usando a criptografia AES ou DRM. fluxo de saudação toodecrypt, player Olá solicitar chave Olá do serviço de distribuição de chaves de saudação. toodecide ou não usuário Olá é autorizado chave de saudação tooget, serviço Olá avalia as políticas de autorização de saudação que você especificou para a chave de saudação.

Se você planejar toohave várias chaves de conteúdo ou toospecify um **serviço de entrega de chave ou a licença** URL diferente Olá serviço de distribuição de chaves de serviços de mídia, usar o SDK do Media Services .NET ou APIs REST.

[Configurar política de autorização de chave de conteúdo usando o SDK do .NET dos Serviços de Mídia](media-services-dotnet-configure-content-key-auth-policy.md)

[Configurar política de autorização de chave de conteúdo usando a API REST dos Serviços de Mídia](media-services-rest-configure-content-key-auth-policy.md)

### <a name="some-considerations-apply"></a>Algumas considerações se aplicam:
* Quando sua conta AMS é criada um **padrão** ponto de extremidade de streaming é adicionada conta tooyour Olá **parado** estado. toostart seu conteúdo e execute aproveitar o empacotamento dinâmico e criptografia dinâmica, o ponto de extremidade de streaming de streaming tem toobe em Olá **executando** estado. 
* O ativo deve conter um conjunto de MP4s de taxa de bits adaptável ou arquivos de Smooth Streaming de taxa de bits adaptável. Para obter mais informações, consulte [Codificar um ativo](media-services-encode-asset.md).
* Olá serviço de entrega de chave armazena ContentKeyAuthorizationPolicy e seus objetos relacionados (restrições e opções de política) por 15 minutos.  Se você criar um ContentKeyAuthorizationPolicy e especifica toouse uma restrição por "Token", em seguida, testá-lo e, em seguida, atualizar a política de saudação muito "abrir" restrição, levará aproximadamente 15 minutos antes de saudação política comutadores toohello versão "Aberta da política de saudação".

## <a name="how-to-configure-hello-key-authorization-policy"></a>Como: configurar a política de autorização da chave de saudação
política de autorização da chave tooconfigure hello, selecione Olá **proteção de conteúdo** página.

Os serviços de mídia oferecem suporte a várias maneiras de autenticar os usuários que fazem solicitações de chave. política de autorização da chave de conteúdo Olá pode ter **abrir**, **token**, ou **IP** restrições de autorização (**IP** pode ser configurado com SDK .NET ou REST).

### <a name="open-restriction"></a>Restrição aberta
Olá **abrir** restrição significa sistema Olá fornecerá Olá tooanyone chave que faz uma solicitação de chave. Essa restrição pode ser útil para fins de teste.

![OpenPolicy][open_policy]

### <a name="token-restriction"></a>Restrição de token
política, pressione Olá restrita do token de saudação toochoose **TOKEN** botão.

Olá **token** política de restrição deve ser acompanhada por um token emitido por uma **serviço de Token seguro** (STS). Serviços de mídia oferece suporte a tokens no hello **Simple Web Tokens** ([SWT](https://msdn.microsoft.com/library/gg185950.aspx#BKMK_2)) formato e **JSON Web Token** formato (JWT). Para obter informações, consulte [Autenticação de token JWT](http://www.gtrifonov.com/2015/01/03/jwt-token-authentication-in-azure-media-services-and-dynamic-encryption/).

Os Serviços de Mídia não fornecem **Serviços de Token Seguro**. Você pode criar um STS personalizado ou utilizar a tokens de tooissue ACS do Microsoft Azure. Olá STS deve ser configurado toocreate um token assinado com hello especificado chave e emitir declarações que você especificou na configuração de restrição de token hello. Olá serviço de distribuição de chaves de serviços de mídia retornará cliente de toohello chave de criptografia de saudação se Olá token é válido e hello declarações no token Olá correspondam às configuradas para chave de conteúdo de saudação. Para obter mais informações, consulte [tokens do uso do Azure ACS tooissue](http://mingfeiy.com/acs-with-key-services).

Ao configurar Olá **TOKEN** política de restrição, você deve definir valores para **chave de verificação**, **emissor** e **público**. chave de verificação primária Olá contém Olá chave que Olá token foi assinado com, o emissor é Olá serviço de token seguro que emite o token de saudação. público Hello (às vezes chamado de escopo) descreve a intenção de saudação do token de saudação ou token de saudação do recurso de saudação autoriza o acesso ao. Olá serviço de distribuição de chaves de serviços de mídia valida que esses valores no token Olá correspondem a valores de saudação no modelo de saudação.

### <a name="playready"></a>PlayReady
Ao proteger seu conteúdo com **PlayReady**, uma das coisas Olá precisar toospecify em sua política de autorização é uma cadeia de caracteres XML que define o modelo de licença do PlayReady hello. Por padrão, Olá seguindo a política é definida:

<PlayReadyLicenseResponseTemplate xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1"> <LicenseTemplates> <PlayReadyLicenseTemplate><AllowTestDevices>true</AllowTestDevices> <ContentKey i:type="ContentEncryptionKeyFromHeader" /> <LicenseType>Nonpersistent</LicenseType> <PlayRight> <AllowPassingVideoContentToUnknownOutput>Allowed</AllowPassingVideoContentToUnknownOutput> </PlayRight> </PlayReadyLicenseTemplate> </LicenseTemplates> </PlayReadyLicenseResponseTemplate>

Você pode clicar em Olá **importar política xml** botão e fornecer um XML diferente que esteja de acordo com toohello esquema XML definido [aqui](media-services-playready-license-template-overview.md).

## <a name="next-step"></a>Próxima etapa
Revise os roteiros de aprendizagem dos Serviços de Mídia.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

[open_policy]: ./media/media-services-portal-configure-content-key-auth-policy/media-services-protect-content-with-open-restriction.png
[token_policy]: ./media/media-services-key-authorization-policy/media-services-protect-content-with-token-restriction.png

