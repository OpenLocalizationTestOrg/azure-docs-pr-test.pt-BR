---
title: "aaaUsing Axinom toodeliver Widevine licenças dos serviços de mídia tooAzure | Microsoft Docs"
description: "Este artigo descreve como você pode usar os serviços de mídia do Azure (AMS) toodeliver um fluxo criptografado dinamicamente pelo AMS com PlayReady e Widevine DRMs. licença do PlayReady Hello proveniente do servidor de licença do PlayReady dos serviços de mídia e licenças Widevine é fornecida pelo servidor de licença Axinom."
services: media-services
documentationcenter: 
author: willzhan
manager: cfowler
editor: 
ms.assetid: 9c93fa4e-b4da-4774-ab6d-8b12b371631d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: willzhan;Mingfeiy;rajputam;Juliako
ms.openlocfilehash: 2245d9269c30712ef779973ae021c00c76174d0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-axinom-toodeliver-widevine-licenses-tooazure-media-services"></a>Usando Axinom toodeliver Widevine licenças tooAzure serviços de mídia
> [!div class="op_single_selector"]
> * [castLabs](media-services-castlabs-integration.md)
> * [Axinom](media-services-axinom-integration.md)
> 
> 

## <a name="overview"></a>Visão geral
O AMS (Serviços de Mídia do Azure) adicionou a proteção dinâmica do Google Widevine (veja o [blog de Mingfei](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/) para obter detalhes). Além disso, o Azure Media Player (AMP) também adicionou suporte Widevine (consulte o [documento AMP](http://amp.azure.net/libs/amp/latest/docs/) para obter detalhes). Isso é uma grande conquista de streaming de conteúdo DASH protegido por CENC com DRM multinativo (PlayReady e Widevine) em navegadores modernos equipados com MSE e EME.

Serviços de mídia a partir do SDK do Media Services .NET versão 3.5.2 de saudação, permite que você tooconfigure Widevine modelo de licença e obter licenças Widevine. Você também pode usar o hello AMS parceiros toohelp fornecer licenças Widevine a seguir: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).

Este artigo descreve como toointegrate e teste Widevine servidor de licenças gerenciada pelo Axinom. Especificamente, ele abrange:  

* A configuração dinâmica da Criptografia Comum com multi-DRM (PlayReady e Widevine) com URLs de aquisição da licença correspondente;
* Gerar um token JWT em ordem toomeet Olá servidor os requisitos de licença;
* Desenvolvendo um aplicativo do Azure Media Player que lida com a aquisição de licenças com autenticação de token JWT;

Olá completa do sistema e Olá fluxo do conteúdo de que ID de chave, key, semente de chave, token JTW e suas declarações pode ser melhor descrita por Olá diagrama a seguir.

![DASH e CENC](./media/media-services-axinom-integration/media-services-axinom1.png)

## <a name="content-protection"></a>Proteção do conteúdo
Para configurar a proteção dinâmica e a política de distribuição de chaves, consulte o blog do Mingfei: [como tooconfigure Widevine empacotamento com os serviços de mídia do Azure](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services).

Você pode configurar a proteção de CENC dinâmica com DRM de múltiplas para traço streaming ter dois seguintes hello:

1. Proteção do PlayReady para o MS Edge e o IE11, que pode ter restrições de autorização de token. política de restrição de token de saudação deve ser acompanhada por um token emitido por um Token STS (serviço seguro), como o Active Directory do Azure;
2. Proteção do Widevine para o Chrome, pode exigir autenticação de token com um token emitido pelo outro STS. 

Consulte a seção [Geração de tokens JWT](media-services-axinom-integration.md#jwt-token-generation) para saber por que o Active Directory do Azure não pode ser usado como um STS para o servidor de licença Widevine da Axinom.

### <a name="considerations"></a>Considerações
1. Você deve usar o hello que axinom especificado semente de chave (8888000000000000000000000000000000000000) e sua gerado selecionado chave ID toogenerate Olá conteúdo ou chave para configurar o serviço de distribuição de chaves. Servidor de licença Axinom emitirá todas as licenças que contém as chaves de conteúdo com base em Olá mesma chave semente, o que é válido para teste e produção.
2. URL de aquisição de licença Olá Widevine para teste: [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense). HTTP e HTTS são permitidos.

## <a name="azure-media-player-preparation"></a>Preparação do Azure Media Player
O AMP v1.4.0 oferece suporte à reprodução de conteúdo AMS dinamicamente empacotado com o PlayReady e o Widevine DRM.
Se o servidor de licenças Widevine não exigir autenticação de token, não há nada adicional que é necessário toodo tootest um traço conteúdo protegido por Widevine. Por exemplo, a equipe de saudação AMP fornece um simples [exemplo](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html), onde poderá ver isso funcionando na borda e o IE11 com PlayReady e o Chrome com Widevine.
servidor de licenças Widevine Olá fornecido pelo Axinom requer autenticação de token de JWT. token JWT Olá precisa toobe enviado com a solicitação de licença por meio de um cabeçalho HTTP "X-AxDRM-Message". Para essa finalidade, é necessário tooadd Olá javascript na página de web hello hospedagem AMP antes da fonte de saudação de configuração a seguir:

    <script>AzureHtml5JS.KeySystem.WidevineCustomAuthorizationHeader = "X-AxDRM-Message"</script>

restante de saudação do código de AMP é API AMP padrão como documento AMP [aqui](http://amp.azure.net/libs/amp/latest/docs/).

Observe que Olá acima javascript para configuração de cabeçalho de autorização personalizada ainda é uma abordagem de curto prazo antes oficial Olá abordagem de longo prazo em AMP é liberada.

## <a name="jwt-token-generation"></a>Geração de tokens JWT
O servidor de licença Widevine da Axinom para testes requer a autenticação do token JWT. Além disso, uma saudação declarações no token JWT de saudação é de um tipo de objeto complexo em vez do tipo de dados primitivo.

Infelizmente, o AD do Azure só pode emitir tokens JWT com tipos primitivos. Da mesma forma, API do .NET Framework (System.IdentityModel.Tokens.SecurityTokenHandler e JwtPayload) permite somente tipo de objeto complexo tooinput como declarações. No entanto, as declarações de saudação ainda são serializadas como cadeia de caracteres. Portanto, não podemos usar qualquer Olá dois para gerar token de JWT Olá para solicitação de licença Widevine.

De John Sheehan [pacote Nuget JWT](https://www.nuget.org/packages/JWT) atende Olá necessidades vamos toouse este pacote do Nuget.

Abaixo está o código de saudação para gerar o token de JWT com hello necessários declarações conforme exigido pelo servidor de licenças Axinom Widevine para teste:

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using System.IdentityModel.Tokens;
    using System.IdentityModel.Protocols.WSTrust;
    using System.Security.Claims;

    namespace OpenIdConnectWeb.Utils
    {
        public class JwtUtils
        {
            //using John Sheehan's NuGet JWT library: https://www.nuget.org/packages/JWT/
            public static string CreateJwtSheehan(string symmetricKeyHex, string key_id)
            {
                byte[] symmetricKey = ConvertHexStringToByteArray(symmetricKeyHex);  //hex string toobyte[] Note: Note that hello key is a hex string, however it must be treated as a series of bytes not a string when encoding.

                var payload = new Dictionary<string, object>()
                             {
                                 { "version", 1 },
                                 { "com_key_id", System.Configuration.ConfigurationManager.AppSettings["ax:com_key_id"] },
                                 { "message", new { type = "entitlement_message", key_ids = new string[] { key_id } }  }
                             };

                string token = JWT.JsonWebToken.Encode(payload, symmetricKey, JWT.JwtHashAlgorithm.HS256);

                return token;
            }

            //convert hex string toobyte[]
            public static byte[] ConvertHexStringToByteArray(string hexString)
            {
                if (hexString.Length % 2 != 0)
                {
                    throw new ArgumentException(String.Format(System.Globalization.CultureInfo.InvariantCulture, "hello binary key cannot have an odd number of digits: {0}", hexString));
                }

                byte[] HexAsBytes = new byte[hexString.Length / 2];
                for (int index = 0; index < HexAsBytes.Length; index++)
                {
                    string byteValue = hexString.Substring(index * 2, 2);
                    HexAsBytes[index] = byte.Parse(byteValue, System.Globalization.NumberStyles.HexNumber, System.Globalization.CultureInfo.InvariantCulture);
                }

                return HexAsBytes;
            }

        }  

    }  

Servidor de licença Widevine da Axinom

    <add key="ax:laurl" value="http://drm-widevine-licensing.axtest.net/AcquireLicense" />
    <add key="ax:com_key_id" value="69e54088-e9e0-4530-8c1a-1eb6dcd0d14e" />
    <add key="ax:com_key" value="4861292d027e269791093327e62ceefdbea489a4c7e5a4974cc904b840fd7c0f" />
    <add key="ax:keyseed" value="8888000000000000000000000000000000000000" />

### <a name="considerations"></a>Considerações
1. Embora o serviço de entrega de licenças do PlayReady da AMS exija "Bearer=" antes de um token de autenticação, o servidor de licença Widevine da Axinom não o utiliza.
2. chave de comunicação de Axinom Olá é usada como chave de assinatura. Observe que Olá chave for uma cadeia de caracteres hexadecimal, no entanto, ele deve ser tratado como uma série de bytes não uma cadeia de caracteres durante a codificação. Isso é feito pelo método hello ConvertHexStringToByteArray.

## <a name="retrieving-key-id"></a>Recuperando a ID da chave
Você pode ter observado que no código Olá para gerar um JWT ID do token, a chave é necessária. Desde que o token JWT Olá precisa toobe pronto antes de carregar o player AMP, principais necessidades ID toobe recuperado na ordem toogenerate token JWT.

Obviamente, há várias maneiras que mantenha tooget da chave de ID. Por exemplo, uma pode armazenar ID da chave junto com os metadados de conteúdo em um banco de dados. Ou você pode recuperar a ID da chave do arquivo MPD (Media Presentation Description) DASH. Olá código a seguir é para Olá último.

    //get key_id from DASH MPD
    public static string GetKeyID(string dashUrl)
    {
        if (!dashUrl.EndsWith("(format=mpd-time-csf)"))
        {
            dashUrl += "(format=mpd-time-csf)";
        }

        XPathDocument objXPathDocument = new XPathDocument(dashUrl);
        XPathNavigator objXPathNavigator = objXPathDocument.CreateNavigator();
        XmlNamespaceManager objXmlNamespaceManager = new XmlNamespaceManager(objXPathNavigator.NameTable);
        objXmlNamespaceManager.AddNamespace("",     "urn:mpeg:dash:schema:mpd:2011");
        objXmlNamespaceManager.AddNamespace("ns1",  "urn:mpeg:dash:schema:mpd:2011");
        objXmlNamespaceManager.AddNamespace("cenc", "urn:mpeg:cenc:2013");
        objXmlNamespaceManager.AddNamespace("ms",   "urn:microsoft");
        objXmlNamespaceManager.AddNamespace("mspr", "urn:microsoft:playready");
        objXmlNamespaceManager.AddNamespace("xsi",  "http://www.w3.org/2001/XMLSchema-instance");
        objXmlNamespaceManager.PushScope();

        XPathNodeIterator objXPathNodeIterator;
        objXPathNodeIterator = objXPathNavigator.Select("//ns1:MPD/ns1:Period/ns1:AdaptationSet/ns1:ContentProtection[@value='cenc']", objXmlNamespaceManager);

        string key_id = string.Empty;
        if (objXPathNodeIterator.MoveNext())
        {
            key_id = objXPathNodeIterator.Current.GetAttribute("default_KID", "urn:mpeg:cenc:2013");
        }

        return key_id;
    }

## <a name="summary"></a>Resumo
Com a adição mais recente de suporte Widevine proteção de conteúdo do Azure Media Services e o Azure Media Player, é possível tooimplement streaming de traço + Multi native DRM (PlayReady + Widevine) com ambos os serviço de licenças do PlayReady na licença AMS e Widevine servidor de Axinom Olá navegadores modernos a seguir:

* Chrome
* Microsoft Edge no Windows 10
* IE 11 no Windows 8.1 e no Windows 10
* Firefox (área de trabalho) e o Safari no Mac (não iOS) também têm suporte por meio do Silverlight e Olá a mesma URL com o Azure Media Player

Hello parâmetros a seguir são necessários no servidor de licença de Axinom Widevine aproveitando do hello minisolução. Exceto para a chave de ID, rest Olá dos parâmetros fornecidos pelo Axinom com base em sua configuração de servidor Widevine.

| Parâmetro | Como ele é usado |
| --- | --- |
| ID da chave de comunicação |Deve ser incluída como valor de declaração hello "com_key_id" no token JWT (consulte [isso](media-services-axinom-integration.md#jwt-token-generation) seção). |
| Chave de comunicação |Deve ser usado como Olá chave de assinatura de token JWT (consulte [isso](media-services-axinom-integration.md#jwt-token-generation) seção). |
| Semente de chave |Deve ser usado toogenerate chave de conteúdo com qualquer dado conteúdo ID de chave (consulte [isso](media-services-axinom-integration.md#content-protection) seção). |
| URL de aquisição de licença de Widevine |Deve ser usada na configuração de política de entrega de ativos para streaming de DASH (consulte [esta](media-services-axinom-integration.md#content-protection) seção). |
| ID de chave de conteúdo |Deve ser incluído como parte do valor de saudação da declaração de mensagem de direitos de token JWT (consulte [isso](media-services-axinom-integration.md#jwt-token-generation) seção). |

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a>Agradecimentos
Gostaríamos Olá tooacknowledge pessoas que contribuíram para a criação deste documento a seguir: Kristjan Jõgi de Axinom Mingfei Yan e Rajput Amit.

