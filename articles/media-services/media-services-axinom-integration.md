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
# <a name="using-axinom-toodeliver-widevine-licenses-tooazure-media-services"></a><span data-ttu-id="853b2-104">Usando Axinom toodeliver Widevine licenças tooAzure serviços de mídia</span><span class="sxs-lookup"><span data-stu-id="853b2-104">Using Axinom toodeliver Widevine licenses tooAzure Media Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="853b2-105">castLabs</span><span class="sxs-lookup"><span data-stu-id="853b2-105">castLabs</span></span>](media-services-castlabs-integration.md)
> * [<span data-ttu-id="853b2-106">Axinom</span><span class="sxs-lookup"><span data-stu-id="853b2-106">Axinom</span></span>](media-services-axinom-integration.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="853b2-107">Visão geral</span><span class="sxs-lookup"><span data-stu-id="853b2-107">Overview</span></span>
<span data-ttu-id="853b2-108">O AMS (Serviços de Mídia do Azure) adicionou a proteção dinâmica do Google Widevine (veja o [blog de Mingfei](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/) para obter detalhes).</span><span class="sxs-lookup"><span data-stu-id="853b2-108">Azure Media Services (AMS) has added Google Widevine dynamic protection (see [Mingfei’s blog](https://azure.microsoft.com/blog/azure-media-services-adds-google-widevine-packaging-for-delivering-multi-drm-stream/) for details).</span></span> <span data-ttu-id="853b2-109">Além disso, o Azure Media Player (AMP) também adicionou suporte Widevine (consulte o [documento AMP](http://amp.azure.net/libs/amp/latest/docs/) para obter detalhes).</span><span class="sxs-lookup"><span data-stu-id="853b2-109">In addition, Azure Media Player (AMP) has also added Widevine support (see [AMP document](http://amp.azure.net/libs/amp/latest/docs/) for details).</span></span> <span data-ttu-id="853b2-110">Isso é uma grande conquista de streaming de conteúdo DASH protegido por CENC com DRM multinativo (PlayReady e Widevine) em navegadores modernos equipados com MSE e EME.</span><span class="sxs-lookup"><span data-stu-id="853b2-110">This is a major accomplishment in streaming DASH content protected by CENC with multi-native-DRM (PlayReady and Widevine) on modern browsers equipped with MSE and EME.</span></span>

<span data-ttu-id="853b2-111">Serviços de mídia a partir do SDK do Media Services .NET versão 3.5.2 de saudação, permite que você tooconfigure Widevine modelo de licença e obter licenças Widevine.</span><span class="sxs-lookup"><span data-stu-id="853b2-111">Starting with hello Media Services .NET SDK version 3.5.2, Media Services enables you tooconfigure Widevine license template and get Widevine licenses.</span></span> <span data-ttu-id="853b2-112">Você também pode usar o hello AMS parceiros toohelp fornecer licenças Widevine a seguir: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span><span class="sxs-lookup"><span data-stu-id="853b2-112">You can also use hello following AMS partners toohelp you deliver Widevine licenses: [Axinom](http://www.axinom.com/press/ibc-axinom-drm-6/), [EZDRM](http://ezdrm.com/), [castLabs](http://castlabs.com/company/partners/azure/).</span></span>

<span data-ttu-id="853b2-113">Este artigo descreve como toointegrate e teste Widevine servidor de licenças gerenciada pelo Axinom.</span><span class="sxs-lookup"><span data-stu-id="853b2-113">This article describes how toointegrate and test Widevine license server managed by Axinom.</span></span> <span data-ttu-id="853b2-114">Especificamente, ele abrange:</span><span class="sxs-lookup"><span data-stu-id="853b2-114">Specifically, it covers:</span></span>  

* <span data-ttu-id="853b2-115">A configuração dinâmica da Criptografia Comum com multi-DRM (PlayReady e Widevine) com URLs de aquisição da licença correspondente;</span><span class="sxs-lookup"><span data-stu-id="853b2-115">Configuring dynamic Common Encryption with multi-DRM (PlayReady and Widevine) with corresponding license acquisition URLs;</span></span>
* <span data-ttu-id="853b2-116">Gerar um token JWT em ordem toomeet Olá servidor os requisitos de licença;</span><span class="sxs-lookup"><span data-stu-id="853b2-116">Generating a JWT token in order toomeet hello license server requirements;</span></span>
* <span data-ttu-id="853b2-117">Desenvolvendo um aplicativo do Azure Media Player que lida com a aquisição de licenças com autenticação de token JWT;</span><span class="sxs-lookup"><span data-stu-id="853b2-117">Developing Azure Media Player app which handles license acquisition with JWT token authentication;</span></span>

<span data-ttu-id="853b2-118">Olá completa do sistema e Olá fluxo do conteúdo de que ID de chave, key, semente de chave, token JTW e suas declarações pode ser melhor descrita por Olá diagrama a seguir.</span><span class="sxs-lookup"><span data-stu-id="853b2-118">hello complete system and hello flow of content key, key ID, key seed, JTW token and its claims can be best described by hello following diagram.</span></span>

![DASH e CENC](./media/media-services-axinom-integration/media-services-axinom1.png)

## <a name="content-protection"></a><span data-ttu-id="853b2-120">Proteção do conteúdo</span><span class="sxs-lookup"><span data-stu-id="853b2-120">Content Protection</span></span>
<span data-ttu-id="853b2-121">Para configurar a proteção dinâmica e a política de distribuição de chaves, consulte o blog do Mingfei: [como tooconfigure Widevine empacotamento com os serviços de mídia do Azure](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services).</span><span class="sxs-lookup"><span data-stu-id="853b2-121">For configuring dynamic protection and key delivery policy, please see Mingfei’s blog: [How tooconfigure Widevine packaging with Azure Media Services](http://mingfeiy.com/how-to-configure-widevine-packaging-with-azure-media-services).</span></span>

<span data-ttu-id="853b2-122">Você pode configurar a proteção de CENC dinâmica com DRM de múltiplas para traço streaming ter dois seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="853b2-122">You can configure dynamic CENC protection with multi-DRM for DASH streaming having both of hello following:</span></span>

1. <span data-ttu-id="853b2-123">Proteção do PlayReady para o MS Edge e o IE11, que pode ter restrições de autorização de token.</span><span class="sxs-lookup"><span data-stu-id="853b2-123">PlayReady protection for MS Edge and IE11, that could have a token authorization restrictions.</span></span> <span data-ttu-id="853b2-124">política de restrição de token de saudação deve ser acompanhada por um token emitido por um Token STS (serviço seguro), como o Active Directory do Azure;</span><span class="sxs-lookup"><span data-stu-id="853b2-124">hello token restricted policy must be accompanied by a token issued by a Secure Token Service (STS), such as Azure Active Directory;</span></span>
2. <span data-ttu-id="853b2-125">Proteção do Widevine para o Chrome, pode exigir autenticação de token com um token emitido pelo outro STS.</span><span class="sxs-lookup"><span data-stu-id="853b2-125">Widevine protection for Chrome, it can require token authentication with token issued by another STS.</span></span> 

<span data-ttu-id="853b2-126">Consulte a seção [Geração de tokens JWT](media-services-axinom-integration.md#jwt-token-generation) para saber por que o Active Directory do Azure não pode ser usado como um STS para o servidor de licença Widevine da Axinom.</span><span class="sxs-lookup"><span data-stu-id="853b2-126">Please see [JWT Token Generation](media-services-axinom-integration.md#jwt-token-generation) section for why Azure Active Directory cannot be used as an STS for Axinom’s Widevine license server.</span></span>

### <a name="considerations"></a><span data-ttu-id="853b2-127">Considerações</span><span class="sxs-lookup"><span data-stu-id="853b2-127">Considerations</span></span>
1. <span data-ttu-id="853b2-128">Você deve usar o hello que axinom especificado semente de chave (8888000000000000000000000000000000000000) e sua gerado selecionado chave ID toogenerate Olá conteúdo ou chave para configurar o serviço de distribuição de chaves.</span><span class="sxs-lookup"><span data-stu-id="853b2-128">You must use hello Axinom specified key seed (8888000000000000000000000000000000000000) and your generated or selected key ID toogenerate hello content key for configuring key delivery service.</span></span> <span data-ttu-id="853b2-129">Servidor de licença Axinom emitirá todas as licenças que contém as chaves de conteúdo com base em Olá mesma chave semente, o que é válido para teste e produção.</span><span class="sxs-lookup"><span data-stu-id="853b2-129">Axinom license server will issue all licenses containing content keys based on hello same key seed, which is valid for both testing and production.</span></span>
2. <span data-ttu-id="853b2-130">URL de aquisição de licença Olá Widevine para teste: [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense).</span><span class="sxs-lookup"><span data-stu-id="853b2-130">hello Widevine license acquisition URL for testing: [https://drm-widevine-licensing.axtest.net/AcquireLicense](https://drm-widevine-licensing.axtest.net/AcquireLicense).</span></span> <span data-ttu-id="853b2-131">HTTP e HTTS são permitidos.</span><span class="sxs-lookup"><span data-stu-id="853b2-131">Both HTTP and HTTS are allowed.</span></span>

## <a name="azure-media-player-preparation"></a><span data-ttu-id="853b2-132">Preparação do Azure Media Player</span><span class="sxs-lookup"><span data-stu-id="853b2-132">Azure Media Player Preparation</span></span>
<span data-ttu-id="853b2-133">O AMP v1.4.0 oferece suporte à reprodução de conteúdo AMS dinamicamente empacotado com o PlayReady e o Widevine DRM.</span><span class="sxs-lookup"><span data-stu-id="853b2-133">AMP v1.4.0 supports playback of AMS content that is dynamically packaged with both PlayReady and Widevine DRM.</span></span>
<span data-ttu-id="853b2-134">Se o servidor de licenças Widevine não exigir autenticação de token, não há nada adicional que é necessário toodo tootest um traço conteúdo protegido por Widevine.</span><span class="sxs-lookup"><span data-stu-id="853b2-134">If Widevine license server does not require token authentication, there is nothing additional you need toodo tootest a DASH content protected by Widevine.</span></span> <span data-ttu-id="853b2-135">Por exemplo, a equipe de saudação AMP fornece um simples [exemplo](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html), onde poderá ver isso funcionando na borda e o IE11 com PlayReady e o Chrome com Widevine.</span><span class="sxs-lookup"><span data-stu-id="853b2-135">For an example, hello AMP team provides a simple [sample](http://amp.azure.net/libs/amp/latest/samples/dynamic_multiDRM_PlayReadyWidevine_notoken.html), where you can see it working in Edge and IE11 with PlayReady and Chrome with Widevine.</span></span>
<span data-ttu-id="853b2-136">servidor de licenças Widevine Olá fornecido pelo Axinom requer autenticação de token de JWT.</span><span class="sxs-lookup"><span data-stu-id="853b2-136">hello Widevine license server provided by Axinom requires JWT token authentication.</span></span> <span data-ttu-id="853b2-137">token JWT Olá precisa toobe enviado com a solicitação de licença por meio de um cabeçalho HTTP "X-AxDRM-Message".</span><span class="sxs-lookup"><span data-stu-id="853b2-137">hello JWT token needs toobe submitted with license request through an HTTP header “X-AxDRM-Message”.</span></span> <span data-ttu-id="853b2-138">Para essa finalidade, é necessário tooadd Olá javascript na página de web hello hospedagem AMP antes da fonte de saudação de configuração a seguir:</span><span class="sxs-lookup"><span data-stu-id="853b2-138">For this purpose, you need tooadd hello following javascript in hello web page hosting AMP before setting hello source:</span></span>

    <script>AzureHtml5JS.KeySystem.WidevineCustomAuthorizationHeader = "X-AxDRM-Message"</script>

<span data-ttu-id="853b2-139">restante de saudação do código de AMP é API AMP padrão como documento AMP [aqui](http://amp.azure.net/libs/amp/latest/docs/).</span><span class="sxs-lookup"><span data-stu-id="853b2-139">hello rest of AMP code is standard AMP API as in AMP document [here](http://amp.azure.net/libs/amp/latest/docs/).</span></span>

<span data-ttu-id="853b2-140">Observe que Olá acima javascript para configuração de cabeçalho de autorização personalizada ainda é uma abordagem de curto prazo antes oficial Olá abordagem de longo prazo em AMP é liberada.</span><span class="sxs-lookup"><span data-stu-id="853b2-140">Note that hello above javascript for setting custom authorization header is still a short term approach before hello official long term approach in AMP is released.</span></span>

## <a name="jwt-token-generation"></a><span data-ttu-id="853b2-141">Geração de tokens JWT</span><span class="sxs-lookup"><span data-stu-id="853b2-141">JWT Token Generation</span></span>
<span data-ttu-id="853b2-142">O servidor de licença Widevine da Axinom para testes requer a autenticação do token JWT.</span><span class="sxs-lookup"><span data-stu-id="853b2-142">Axinom Widevine license server for testing requires JWT token authentication.</span></span> <span data-ttu-id="853b2-143">Além disso, uma saudação declarações no token JWT de saudação é de um tipo de objeto complexo em vez do tipo de dados primitivo.</span><span class="sxs-lookup"><span data-stu-id="853b2-143">In addition, one of hello claims in hello JWT token is of a complex object type instead of primitive data type.</span></span>

<span data-ttu-id="853b2-144">Infelizmente, o AD do Azure só pode emitir tokens JWT com tipos primitivos.</span><span class="sxs-lookup"><span data-stu-id="853b2-144">Unfortunately, Azure AD can only issue JWT tokens with primitive types.</span></span> <span data-ttu-id="853b2-145">Da mesma forma, API do .NET Framework (System.IdentityModel.Tokens.SecurityTokenHandler e JwtPayload) permite somente tipo de objeto complexo tooinput como declarações.</span><span class="sxs-lookup"><span data-stu-id="853b2-145">Similarly, .NET Framework API (System.IdentityModel.Tokens.SecurityTokenHandler and JwtPayload) only allows you tooinput complex object type as claims.</span></span> <span data-ttu-id="853b2-146">No entanto, as declarações de saudação ainda são serializadas como cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="853b2-146">However, hello claims are still serialized as string.</span></span> <span data-ttu-id="853b2-147">Portanto, não podemos usar qualquer Olá dois para gerar token de JWT Olá para solicitação de licença Widevine.</span><span class="sxs-lookup"><span data-stu-id="853b2-147">Therefore we cannot use any of hello two for generating hello JWT token for Widevine license request.</span></span>

<span data-ttu-id="853b2-148">De John Sheehan [pacote Nuget JWT](https://www.nuget.org/packages/JWT) atende Olá necessidades vamos toouse este pacote do Nuget.</span><span class="sxs-lookup"><span data-stu-id="853b2-148">John Sheehan’s [JWT Nuget package](https://www.nuget.org/packages/JWT) meets hello needs so we are going toouse this Nuget package.</span></span>

<span data-ttu-id="853b2-149">Abaixo está o código de saudação para gerar o token de JWT com hello necessários declarações conforme exigido pelo servidor de licenças Axinom Widevine para teste:</span><span class="sxs-lookup"><span data-stu-id="853b2-149">Below is hello code for generating JWT token with hello needed claims as required by Axinom Widevine license server for testing:</span></span>

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

<span data-ttu-id="853b2-150">Servidor de licença Widevine da Axinom</span><span class="sxs-lookup"><span data-stu-id="853b2-150">Axinom Widevine license server</span></span>

    <add key="ax:laurl" value="http://drm-widevine-licensing.axtest.net/AcquireLicense" />
    <add key="ax:com_key_id" value="69e54088-e9e0-4530-8c1a-1eb6dcd0d14e" />
    <add key="ax:com_key" value="4861292d027e269791093327e62ceefdbea489a4c7e5a4974cc904b840fd7c0f" />
    <add key="ax:keyseed" value="8888000000000000000000000000000000000000" />

### <a name="considerations"></a><span data-ttu-id="853b2-151">Considerações</span><span class="sxs-lookup"><span data-stu-id="853b2-151">Considerations</span></span>
1. <span data-ttu-id="853b2-152">Embora o serviço de entrega de licenças do PlayReady da AMS exija "Bearer=" antes de um token de autenticação, o servidor de licença Widevine da Axinom não o utiliza.</span><span class="sxs-lookup"><span data-stu-id="853b2-152">Even though AMS PlayReady license delivery service requires “Bearer=” preceding an authentication token, Axinom Widevine license server does not use it.</span></span>
2. <span data-ttu-id="853b2-153">chave de comunicação de Axinom Olá é usada como chave de assinatura.</span><span class="sxs-lookup"><span data-stu-id="853b2-153">hello Axinom communication key is used as signing key.</span></span> <span data-ttu-id="853b2-154">Observe que Olá chave for uma cadeia de caracteres hexadecimal, no entanto, ele deve ser tratado como uma série de bytes não uma cadeia de caracteres durante a codificação.</span><span class="sxs-lookup"><span data-stu-id="853b2-154">Note that hello key is a hex string, however it must be treated as a series of bytes not a string when encoding.</span></span> <span data-ttu-id="853b2-155">Isso é feito pelo método hello ConvertHexStringToByteArray.</span><span class="sxs-lookup"><span data-stu-id="853b2-155">This is achieved by hello method ConvertHexStringToByteArray.</span></span>

## <a name="retrieving-key-id"></a><span data-ttu-id="853b2-156">Recuperando a ID da chave</span><span class="sxs-lookup"><span data-stu-id="853b2-156">Retrieving Key ID</span></span>
<span data-ttu-id="853b2-157">Você pode ter observado que no código Olá para gerar um JWT ID do token, a chave é necessária.</span><span class="sxs-lookup"><span data-stu-id="853b2-157">You may have noticed that in hello code for generating a JWT token, key ID is required.</span></span> <span data-ttu-id="853b2-158">Desde que o token JWT Olá precisa toobe pronto antes de carregar o player AMP, principais necessidades ID toobe recuperado na ordem toogenerate token JWT.</span><span class="sxs-lookup"><span data-stu-id="853b2-158">Since hello JWT token needs toobe ready before loading AMP player, key ID needs toobe retrieved in order toogenerate JWT token.</span></span>

<span data-ttu-id="853b2-159">Obviamente, há várias maneiras que mantenha tooget da chave de ID.</span><span class="sxs-lookup"><span data-stu-id="853b2-159">Of course there are multiple ways tooget hold of key ID.</span></span> <span data-ttu-id="853b2-160">Por exemplo, uma pode armazenar ID da chave junto com os metadados de conteúdo em um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="853b2-160">For example, one may store key ID together with content metadata in a database.</span></span> <span data-ttu-id="853b2-161">Ou você pode recuperar a ID da chave do arquivo MPD (Media Presentation Description) DASH.</span><span class="sxs-lookup"><span data-stu-id="853b2-161">Or you can retrieve key ID from DASH MPD (Media Presentation Description) file.</span></span> <span data-ttu-id="853b2-162">Olá código a seguir é para Olá último.</span><span class="sxs-lookup"><span data-stu-id="853b2-162">hello code below is for hello latter.</span></span>

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

## <a name="summary"></a><span data-ttu-id="853b2-163">Resumo</span><span class="sxs-lookup"><span data-stu-id="853b2-163">Summary</span></span>
<span data-ttu-id="853b2-164">Com a adição mais recente de suporte Widevine proteção de conteúdo do Azure Media Services e o Azure Media Player, é possível tooimplement streaming de traço + Multi native DRM (PlayReady + Widevine) com ambos os serviço de licenças do PlayReady na licença AMS e Widevine servidor de Axinom Olá navegadores modernos a seguir:</span><span class="sxs-lookup"><span data-stu-id="853b2-164">With latest addition of Widevine support in both Azure Media Services Content Protection and Azure Media Player, we are able tooimplement streaming of DASH + Multi-native-DRM (PlayReady + Widevine) with both PlayReady license service in AMS and Widevine license server from Axinom for hello following modern browsers:</span></span>

* <span data-ttu-id="853b2-165">Chrome</span><span class="sxs-lookup"><span data-stu-id="853b2-165">Chrome</span></span>
* <span data-ttu-id="853b2-166">Microsoft Edge no Windows 10</span><span class="sxs-lookup"><span data-stu-id="853b2-166">Microsoft Edge on Windows 10</span></span>
* <span data-ttu-id="853b2-167">IE 11 no Windows 8.1 e no Windows 10</span><span class="sxs-lookup"><span data-stu-id="853b2-167">IE 11 on Windows 8.1 and Windows 10</span></span>
* <span data-ttu-id="853b2-168">Firefox (área de trabalho) e o Safari no Mac (não iOS) também têm suporte por meio do Silverlight e Olá a mesma URL com o Azure Media Player</span><span class="sxs-lookup"><span data-stu-id="853b2-168">Both Firefox (Desktop) and Safari on Mac (not iOS) are also supported via Silverlight and hello same URL with Azure Media Player</span></span>

<span data-ttu-id="853b2-169">Hello parâmetros a seguir são necessários no servidor de licença de Axinom Widevine aproveitando do hello minisolução.</span><span class="sxs-lookup"><span data-stu-id="853b2-169">hello following parameters are required in hello mini-solution leveraging Axinom Widevine license server.</span></span> <span data-ttu-id="853b2-170">Exceto para a chave de ID, rest Olá dos parâmetros fornecidos pelo Axinom com base em sua configuração de servidor Widevine.</span><span class="sxs-lookup"><span data-stu-id="853b2-170">Except for key ID, hello rest of parameters are provided by Axinom based on their Widevine server setup.</span></span>

| <span data-ttu-id="853b2-171">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="853b2-171">Parameter</span></span> | <span data-ttu-id="853b2-172">Como ele é usado</span><span class="sxs-lookup"><span data-stu-id="853b2-172">How it is used</span></span> |
| --- | --- |
| <span data-ttu-id="853b2-173">ID da chave de comunicação</span><span class="sxs-lookup"><span data-stu-id="853b2-173">Communication key ID</span></span> |<span data-ttu-id="853b2-174">Deve ser incluída como valor de declaração hello "com_key_id" no token JWT (consulte [isso](media-services-axinom-integration.md#jwt-token-generation) seção).</span><span class="sxs-lookup"><span data-stu-id="853b2-174">Must be included as value of hello claim "com_key_id" in JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |
| <span data-ttu-id="853b2-175">Chave de comunicação</span><span class="sxs-lookup"><span data-stu-id="853b2-175">Communication key</span></span> |<span data-ttu-id="853b2-176">Deve ser usado como Olá chave de assinatura de token JWT (consulte [isso](media-services-axinom-integration.md#jwt-token-generation) seção).</span><span class="sxs-lookup"><span data-stu-id="853b2-176">Must be used as hello signing key of JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |
| <span data-ttu-id="853b2-177">Semente de chave</span><span class="sxs-lookup"><span data-stu-id="853b2-177">Key seed</span></span> |<span data-ttu-id="853b2-178">Deve ser usado toogenerate chave de conteúdo com qualquer dado conteúdo ID de chave (consulte [isso](media-services-axinom-integration.md#content-protection) seção).</span><span class="sxs-lookup"><span data-stu-id="853b2-178">Must be used toogenerate content key with any given content key ID (see  [this](media-services-axinom-integration.md#content-protection) section).</span></span> |
| <span data-ttu-id="853b2-179">URL de aquisição de licença de Widevine</span><span class="sxs-lookup"><span data-stu-id="853b2-179">Widevine License acquisition URL</span></span> |<span data-ttu-id="853b2-180">Deve ser usada na configuração de política de entrega de ativos para streaming de DASH (consulte [esta](media-services-axinom-integration.md#content-protection) seção).</span><span class="sxs-lookup"><span data-stu-id="853b2-180">Must be used in configuring asset delivery policy for DASH streaming (see  [this](media-services-axinom-integration.md#content-protection) section ).</span></span> |
| <span data-ttu-id="853b2-181">ID de chave de conteúdo</span><span class="sxs-lookup"><span data-stu-id="853b2-181">Content Key ID</span></span> |<span data-ttu-id="853b2-182">Deve ser incluído como parte do valor de saudação da declaração de mensagem de direitos de token JWT (consulte [isso](media-services-axinom-integration.md#jwt-token-generation) seção).</span><span class="sxs-lookup"><span data-stu-id="853b2-182">Must be included as part of hello value of Entitlement Message claim of JWT token (see [this](media-services-axinom-integration.md#jwt-token-generation) section).</span></span> |

## <a name="media-services-learning-paths"></a><span data-ttu-id="853b2-183">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="853b2-183">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="853b2-184">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="853b2-184">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

### <a name="acknowledgments"></a><span data-ttu-id="853b2-185">Agradecimentos</span><span class="sxs-lookup"><span data-stu-id="853b2-185">Acknowledgments</span></span>
<span data-ttu-id="853b2-186">Gostaríamos Olá tooacknowledge pessoas que contribuíram para a criação deste documento a seguir: Kristjan Jõgi de Axinom Mingfei Yan e Rajput Amit.</span><span class="sxs-lookup"><span data-stu-id="853b2-186">We would like tooacknowledge hello following people who contributed towards creating this document: Kristjan Jõgi of Axinom, Mingfei Yan, and Amit Rajput.</span></span>

