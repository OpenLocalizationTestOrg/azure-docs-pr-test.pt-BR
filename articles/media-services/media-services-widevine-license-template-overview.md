---
title: "Visão geral do modelo de licença do Widevine | Microsoft Docs"
description: "Este tópico fornece uma visão geral de um modelo de licença do Widevine usado para configurar as licenças do Widevine."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 0e6f1f05-7ed6-4ed6-82a0-0cc2182b075a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 667ff16dc7608dab2a5b8b1fd7df715da4620ca1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="widevine-license-template-overview"></a><span data-ttu-id="b6790-103">Visão geral do modelo de licença do Widevine</span><span class="sxs-lookup"><span data-stu-id="b6790-103">Widevine license template overview</span></span>
## <a name="overview"></a><span data-ttu-id="b6790-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="b6790-104">Overview</span></span>
<span data-ttu-id="b6790-105">Agora, os Serviços de Mídia do Azure permitem que você configure e solicite licenças do Widevine.</span><span class="sxs-lookup"><span data-stu-id="b6790-105">Azure Media Services now enables you to configure and request Widevine licenses.</span></span> <span data-ttu-id="b6790-106">Quando o player do usuário final tentar reproduzir o conteúdo protegido do Widevine, uma solicitação será enviada ao serviço de entrega de licença para a obtenção de uma licença.</span><span class="sxs-lookup"><span data-stu-id="b6790-106">When the end user player tries to play your Widevine protected content, a request is sent to the license delivery service to obtain a license.</span></span> <span data-ttu-id="b6790-107">Se o serviço de licença aprova a solicitação, ele emite a licença que é enviada ao cliente e pode ser usada para descriptografar e reproduzir o conteúdo especificado.</span><span class="sxs-lookup"><span data-stu-id="b6790-107">If the license service approves the request, it issues the license which is sent to the client and can be used to decrypt and play the specified content.</span></span>

<span data-ttu-id="b6790-108">A solicitação de licença do Widevine é formatada como uma mensagem JSON.</span><span class="sxs-lookup"><span data-stu-id="b6790-108">Widevine license request is formatted as a JSON message.</span></span>  

>[!NOTE]
> <span data-ttu-id="b6790-109">Você pode optar por criar uma mensagem vazia sem valores, apenas "{}" e um modelo de licença será criado com todos os padrões.</span><span class="sxs-lookup"><span data-stu-id="b6790-109">You can choose to create an empty message with no values just "{}" and a license template will be created with all defaults.</span></span> <span data-ttu-id="b6790-110">O padrão funciona na maioria dos casos.</span><span class="sxs-lookup"><span data-stu-id="b6790-110">The default works for most cases.</span></span> <span data-ttu-id="b6790-111">Por exemplo, para cenários de entrega de licença com base em MS que sempre devem ser o padrão.</span><span class="sxs-lookup"><span data-stu-id="b6790-111">For example, for MS based license delivery scenarios that should always be default.</span></span> <span data-ttu-id="b6790-112">Se você precisar definir os valores de "content_id" e "provedor", um provedor deverá corresponder às credenciais de Widevine do Google.</span><span class="sxs-lookup"><span data-stu-id="b6790-112">If you do need to set the "provider" and "content_id" values, a provider must match Google's Widevine credentials.</span></span>

    {  
       “payload”:“<license challenge>”,
       “content_id”: “<content id>” 
       “provider”: ”<provider>”
       “allowed_track_types”:“<types>”,
       “content_key_specs”:[  
          {  
             “track_type”:“<track type 1>”
          },
          {  
             “track_type”:“<track type 2>”
          },
          …
       ],
       “policy_overrides”:{  
          “can_play”:<can play>,
          “can persist”:<can persist>,
          “can_renew”:<can renew>,
          “rental_duration_seconds”:<rental duration>,
          “playback_duration_seconds”:<playback duration>,
          “license_duration_seconds”:<license duration>,
          “renewal_recovery_duration_seconds”:<renewal recovery duration>,
          “renewal_server_url”:”<renewal server url>”,
          “renewal_delay_seconds”:<renewal delay>,
          “renewal_retry_interval_seconds”:<renewal retry interval>,
          “renew_with_usage”:<renew with usage>
       }
    }

## <a name="json-message"></a><span data-ttu-id="b6790-113">Mensagem JSON</span><span class="sxs-lookup"><span data-stu-id="b6790-113">JSON message</span></span>
| <span data-ttu-id="b6790-114">Nome</span><span class="sxs-lookup"><span data-stu-id="b6790-114">Name</span></span> | <span data-ttu-id="b6790-115">Valor</span><span class="sxs-lookup"><span data-stu-id="b6790-115">Value</span></span> | <span data-ttu-id="b6790-116">Descrição</span><span class="sxs-lookup"><span data-stu-id="b6790-116">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b6790-117">payload</span><span class="sxs-lookup"><span data-stu-id="b6790-117">payload</span></span> |<span data-ttu-id="b6790-118">Cadeia codificada em Base64</span><span class="sxs-lookup"><span data-stu-id="b6790-118">Base64 encoded string</span></span> |<span data-ttu-id="b6790-119">A solicitação de licença enviada por um cliente.</span><span class="sxs-lookup"><span data-stu-id="b6790-119">The license request sent by a client.</span></span> |
| <span data-ttu-id="b6790-120">content_id</span><span class="sxs-lookup"><span data-stu-id="b6790-120">content_id</span></span> |<span data-ttu-id="b6790-121">Cadeia codificada em Base64</span><span class="sxs-lookup"><span data-stu-id="b6790-121">Base64 encoded string</span></span> |<span data-ttu-id="b6790-122">Identificador usado para gerar KeyId(s) e chaves de conteúdo para cada content_key_specs.track_type.</span><span class="sxs-lookup"><span data-stu-id="b6790-122">Identifier used to derive KeyId(s) and Content Key(s) for each content_key_specs.track_type.</span></span> |
| <span data-ttu-id="b6790-123">provider</span><span class="sxs-lookup"><span data-stu-id="b6790-123">provider</span></span> |<span data-ttu-id="b6790-124">string</span><span class="sxs-lookup"><span data-stu-id="b6790-124">string</span></span> |<span data-ttu-id="b6790-125">Usado para pesquisar as políticas e chaves de conteúdo.</span><span class="sxs-lookup"><span data-stu-id="b6790-125">Used to look up content keys and policies.</span></span> <span data-ttu-id="b6790-126">Se a distribuição de chaves MS é usada para entrega de licença do Widevine, esse parâmetro é ignorado.</span><span class="sxs-lookup"><span data-stu-id="b6790-126">If MS key delivery is used for Widevine license delivery, this parameter is ignored.</span></span> |
| <span data-ttu-id="b6790-127">policy_name</span><span class="sxs-lookup"><span data-stu-id="b6790-127">policy_name</span></span> |<span data-ttu-id="b6790-128">string</span><span class="sxs-lookup"><span data-stu-id="b6790-128">string</span></span> |<span data-ttu-id="b6790-129">Nome de uma política registrada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b6790-129">Name of a previously registered policy.</span></span> <span data-ttu-id="b6790-130">Opcional</span><span class="sxs-lookup"><span data-stu-id="b6790-130">Optional</span></span> |
| <span data-ttu-id="b6790-131">allowed_track_types</span><span class="sxs-lookup"><span data-stu-id="b6790-131">allowed_track_types</span></span> |<span data-ttu-id="b6790-132">enum</span><span class="sxs-lookup"><span data-stu-id="b6790-132">enum</span></span> |<span data-ttu-id="b6790-133">SD_ONLY ou SD_HD.</span><span class="sxs-lookup"><span data-stu-id="b6790-133">SD_ONLY or SD_HD.</span></span> <span data-ttu-id="b6790-134">Controla quais chaves de conteúdo devem ser incluídas em uma licença</span><span class="sxs-lookup"><span data-stu-id="b6790-134">Controls which content keys should be included in a license</span></span> |
| <span data-ttu-id="b6790-135">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="b6790-135">content_key_specs</span></span> |<span data-ttu-id="b6790-136">matriz de estruturas JSON, confira **Especificações de chave de conteúdo** abaixo</span><span class="sxs-lookup"><span data-stu-id="b6790-136">array of JSON structures, see **Content Key Specs** below</span></span> |<span data-ttu-id="b6790-137">Um controle mais refinado sobre quais chaves de conteúdo retornar.</span><span class="sxs-lookup"><span data-stu-id="b6790-137">A finer grained control on what content keys to return.</span></span> <span data-ttu-id="b6790-138">Confira Especificações de chave de conteúdo a seguir para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="b6790-138">See Content Key Spec below for details.</span></span>  <span data-ttu-id="b6790-139">Apenas um entre allowed_track_types e content_key_specs pode ser especificado.</span><span class="sxs-lookup"><span data-stu-id="b6790-139">Only one of allowed_track_types and content_key_specs can be specified.</span></span> |
| <span data-ttu-id="b6790-140">use_policy_overrides_exclusively</span><span class="sxs-lookup"><span data-stu-id="b6790-140">use_policy_overrides_exclusively</span></span> |<span data-ttu-id="b6790-141">booliano.</span><span class="sxs-lookup"><span data-stu-id="b6790-141">boolean.</span></span> <span data-ttu-id="b6790-142">true ou false</span><span class="sxs-lookup"><span data-stu-id="b6790-142">true or false</span></span> |<span data-ttu-id="b6790-143">Use os atributos de política especificados por policy_overrides e omita todas as políticas armazenadas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="b6790-143">Use policy attributes specified by policy_overrides and omit all previously stored policy.</span></span> |
| <span data-ttu-id="b6790-144">policy_overrides</span><span class="sxs-lookup"><span data-stu-id="b6790-144">policy_overrides</span></span> |<span data-ttu-id="b6790-145">Estrutura JSON, confira **Substituições de política** abaixo</span><span class="sxs-lookup"><span data-stu-id="b6790-145">JSON structure, see **Policy Overrides** below</span></span> |<span data-ttu-id="b6790-146">Configurações de política para esta licença.</span><span class="sxs-lookup"><span data-stu-id="b6790-146">Policy settings for this license.</span></span>  <span data-ttu-id="b6790-147">Caso este ativo tenha uma política predefinida, esses valores especificados serão usados.</span><span class="sxs-lookup"><span data-stu-id="b6790-147">In the event this asset has a pre-defined policy, these specified values will be used.</span></span> |
| <span data-ttu-id="b6790-148">session_init</span><span class="sxs-lookup"><span data-stu-id="b6790-148">session_init</span></span> |<span data-ttu-id="b6790-149">Estrutura JSON, confira **Inicialização da sessão** abaixo</span><span class="sxs-lookup"><span data-stu-id="b6790-149">JSON structure, see **Session Initialization** below</span></span> |<span data-ttu-id="b6790-150">Dados opcionais passados para a licença.</span><span class="sxs-lookup"><span data-stu-id="b6790-150">Optional data passed to license.</span></span> |
| <span data-ttu-id="b6790-151">parse_only</span><span class="sxs-lookup"><span data-stu-id="b6790-151">parse_only</span></span> |<span data-ttu-id="b6790-152">booliano.</span><span class="sxs-lookup"><span data-stu-id="b6790-152">boolean.</span></span> <span data-ttu-id="b6790-153">true ou false</span><span class="sxs-lookup"><span data-stu-id="b6790-153">true or false</span></span> |<span data-ttu-id="b6790-154">A solicitação de licença é analisada, mas nenhuma licença é emitida.</span><span class="sxs-lookup"><span data-stu-id="b6790-154">The license request is parsed but no license is issued.</span></span> <span data-ttu-id="b6790-155">No entanto, os valores da solicitação de licença retornam na resposta.</span><span class="sxs-lookup"><span data-stu-id="b6790-155">However, values form the license request are returned in the response.</span></span> |

## <a name="content-key-specs"></a><span data-ttu-id="b6790-156">Especificações de chave de conteúdo</span><span class="sxs-lookup"><span data-stu-id="b6790-156">Content Key Specs</span></span>
<span data-ttu-id="b6790-157">Se já houver uma política, não será necessário especificar qualquer um dos valores nas Especificações de Chave de Conteúdo.  A política existente associada a este conteúdo será usada para determinar a proteção da saída, como HDCP e CGMS.</span><span class="sxs-lookup"><span data-stu-id="b6790-157">If a pre-existing policy exist, there is no need to specify any of the values in the Content Key Spec.  The pre-existing policy associated with this content will be used to determine the output protection such as HDCP and CGMS.</span></span>  <span data-ttu-id="b6790-158">Se uma política existente não estiver registrada no Servidor de Licenças do Widevine, o provedor de conteúdo poderá injetar os valores na solicitação de licença.</span><span class="sxs-lookup"><span data-stu-id="b6790-158">If a pre-existing policy is not registered with the Widevine License Server, the content provider can inject the values into the license request.</span></span>   

<span data-ttu-id="b6790-159">Cada content_key_specs deve ser especificado para todos os controles, independentemente da opção use_policy_overrides_exclusively.</span><span class="sxs-lookup"><span data-stu-id="b6790-159">Each content_key_specs must be specified for all tracks, regardless of the option use_policy_overrides_exclusively.</span></span> 

| <span data-ttu-id="b6790-160">Nome</span><span class="sxs-lookup"><span data-stu-id="b6790-160">Name</span></span> | <span data-ttu-id="b6790-161">Valor</span><span class="sxs-lookup"><span data-stu-id="b6790-161">Value</span></span> | <span data-ttu-id="b6790-162">Descrição</span><span class="sxs-lookup"><span data-stu-id="b6790-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b6790-163">content_key_specs.</span><span class="sxs-lookup"><span data-stu-id="b6790-163">content_key_specs.</span></span> <span data-ttu-id="b6790-164">track_type</span><span class="sxs-lookup"><span data-stu-id="b6790-164">track_type</span></span> |<span data-ttu-id="b6790-165">string</span><span class="sxs-lookup"><span data-stu-id="b6790-165">string</span></span> |<span data-ttu-id="b6790-166">Um nome de tipo de controle.</span><span class="sxs-lookup"><span data-stu-id="b6790-166">A track type name.</span></span> <span data-ttu-id="b6790-167">Se content_key_specs for especificado na solicitação de licença, especifique de forma explícita todos os tipos de controle.</span><span class="sxs-lookup"><span data-stu-id="b6790-167">If content_key_specs is specified in the license request, make sure to specify all track types explicitly.</span></span> <span data-ttu-id="b6790-168">Se você não fizer isso, haverá uma falha de reprodução após 10 segundos.</span><span class="sxs-lookup"><span data-stu-id="b6790-168">Failure to do so will result in failure to playback past 10 seconds.</span></span> |
| <span data-ttu-id="b6790-169">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="b6790-169">content_key_specs</span></span>  <br/> <span data-ttu-id="b6790-170">security_level</span><span class="sxs-lookup"><span data-stu-id="b6790-170">security_level</span></span> |<span data-ttu-id="b6790-171">uint32</span><span class="sxs-lookup"><span data-stu-id="b6790-171">uint32</span></span> |<span data-ttu-id="b6790-172">Define os requisitos de robustez de reprodução do cliente.</span><span class="sxs-lookup"><span data-stu-id="b6790-172">Defines client robustness requirements for playback.</span></span> <br/> <span data-ttu-id="b6790-173">1 - É necessário aplicar a criptografia whitebox baseada em software.</span><span class="sxs-lookup"><span data-stu-id="b6790-173">1 - Software-based whitebox crypto is required.</span></span> <br/> <span data-ttu-id="b6790-174">2 - É necessário aplicar a criptografia de software e um decodificador ofuscado.</span><span class="sxs-lookup"><span data-stu-id="b6790-174">2 - Software crypto and an obfuscated decoder is required.</span></span> <br/> <span data-ttu-id="b6790-175">3 - As principais operações de criptografia e de materiais devem ser executadas em um ambiente de execução confiável com suporte de hardware.</span><span class="sxs-lookup"><span data-stu-id="b6790-175">3 - The key material and crypto operations must be performed within a hardware backed trusted execution environment.</span></span> <br/> <span data-ttu-id="b6790-176">4 - A criptografia e decodificação do conteúdo devem ser executadas em um ambiente de execução confiável com suporte de hardware.</span><span class="sxs-lookup"><span data-stu-id="b6790-176">4 - The crypto and decoding of content must be performed within a hardware backed trusted execution environment.</span></span>  <br/> <span data-ttu-id="b6790-177">5 - A criptografia, decodificação e qualquer manipulação da mídia (compactada e descompactada) devem ser tratadas em um ambiente de execução confiável com suporte de hardware.</span><span class="sxs-lookup"><span data-stu-id="b6790-177">5 - The crypto, decoding and all handling of the media (compressed and uncompressed) must be handled within a hardware backed trusted execution environment.</span></span> |
| <span data-ttu-id="b6790-178">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="b6790-178">content_key_specs</span></span> <br/> <span data-ttu-id="b6790-179">required_output_protection.hdc</span><span class="sxs-lookup"><span data-stu-id="b6790-179">required_output_protection.hdc</span></span> |<span data-ttu-id="b6790-180">cadeia de caracteres - uma das seguintes: HDCP_NONE, HDCP_V1, HDCP_V2</span><span class="sxs-lookup"><span data-stu-id="b6790-180">string - one of: HDCP_NONE, HDCP_V1, HDCP_V2</span></span> |<span data-ttu-id="b6790-181">Indica se HDCP é necessário</span><span class="sxs-lookup"><span data-stu-id="b6790-181">Indicates whether HDCP is require</span></span> |
| <span data-ttu-id="b6790-182">content_key_specs</span><span class="sxs-lookup"><span data-stu-id="b6790-182">content_key_specs</span></span> <br/><span data-ttu-id="b6790-183">chave</span><span class="sxs-lookup"><span data-stu-id="b6790-183">key</span></span> |<span data-ttu-id="b6790-184">Cadeia codificada em </span><span class="sxs-lookup"><span data-stu-id="b6790-184">Base64</span></span> <br/><span data-ttu-id="b6790-185">Base64</span><span class="sxs-lookup"><span data-stu-id="b6790-185">encoded string</span></span> |<span data-ttu-id="b6790-186">Chave de conteúdo a ser usada para este controle. Se for especificado, o track_type ou a key_id será obrigatório.</span><span class="sxs-lookup"><span data-stu-id="b6790-186">Content key to use for this track. If specified, the track_type or key_id is required.</span></span>  <span data-ttu-id="b6790-187">Essa opção permite que o provedor de conteúdo insira a chave de conteúdo para este controle em vez de deixar o servidor de licença do Widevine gerar ou procurar uma chave.</span><span class="sxs-lookup"><span data-stu-id="b6790-187">This option allows the content provider to inject the content key for this track instead of letting Widevine license server generate or lookup a key.</span></span> |
| <span data-ttu-id="b6790-188">content_key_specs.key_id</span><span class="sxs-lookup"><span data-stu-id="b6790-188">content_key_specs.key_id</span></span> |<span data-ttu-id="b6790-189">Binário de cadeia de caracteres codificada em Base64, 16 bytes</span><span class="sxs-lookup"><span data-stu-id="b6790-189">Base64 encoded string  binary, 16 bytes</span></span> |<span data-ttu-id="b6790-190">Identificador exclusivo para a chave.</span><span class="sxs-lookup"><span data-stu-id="b6790-190">Unique identifier for the key.</span></span> |

## <a name="policy-overrides"></a><span data-ttu-id="b6790-191">Substituições de política</span><span class="sxs-lookup"><span data-stu-id="b6790-191">Policy Overrides</span></span>
| <span data-ttu-id="b6790-192">Nome</span><span class="sxs-lookup"><span data-stu-id="b6790-192">Name</span></span> | <span data-ttu-id="b6790-193">Valor</span><span class="sxs-lookup"><span data-stu-id="b6790-193">Value</span></span> | <span data-ttu-id="b6790-194">Descrição</span><span class="sxs-lookup"><span data-stu-id="b6790-194">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b6790-195">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="b6790-195">policy_overrides.</span></span> <span data-ttu-id="b6790-196">can_play</span><span class="sxs-lookup"><span data-stu-id="b6790-196">can_play</span></span> |<span data-ttu-id="b6790-197">booliano.</span><span class="sxs-lookup"><span data-stu-id="b6790-197">boolean.</span></span> <span data-ttu-id="b6790-198">true ou false</span><span class="sxs-lookup"><span data-stu-id="b6790-198">true or false</span></span> |<span data-ttu-id="b6790-199">Indica que a reprodução do conteúdo é permitida.</span><span class="sxs-lookup"><span data-stu-id="b6790-199">Indicates that playback of the content is allowed.</span></span> <span data-ttu-id="b6790-200">O padrão é falso.</span><span class="sxs-lookup"><span data-stu-id="b6790-200">Default is false.</span></span> |
| <span data-ttu-id="b6790-201">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="b6790-201">policy_overrides.</span></span> <span data-ttu-id="b6790-202">can_persist</span><span class="sxs-lookup"><span data-stu-id="b6790-202">can_persist</span></span> |<span data-ttu-id="b6790-203">booliano.</span><span class="sxs-lookup"><span data-stu-id="b6790-203">boolean.</span></span> <span data-ttu-id="b6790-204">true ou false</span><span class="sxs-lookup"><span data-stu-id="b6790-204">true or false</span></span> |<span data-ttu-id="b6790-205">Indica que a licença pode ser persistente para o armazenamento não volátil para uso offline.</span><span class="sxs-lookup"><span data-stu-id="b6790-205">Indicates that the license may be persisted to non-volatile storage for offline use.</span></span> <span data-ttu-id="b6790-206">O padrão é falso.</span><span class="sxs-lookup"><span data-stu-id="b6790-206">Default is false.</span></span> |
| <span data-ttu-id="b6790-207">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="b6790-207">policy_overrides.</span></span> <span data-ttu-id="b6790-208">can_renew</span><span class="sxs-lookup"><span data-stu-id="b6790-208">can_renew</span></span> |<span data-ttu-id="b6790-209">booliano true ou false</span><span class="sxs-lookup"><span data-stu-id="b6790-209">boolean true or false</span></span> |<span data-ttu-id="b6790-210">Indica que a renovação dessa licença é permitida.</span><span class="sxs-lookup"><span data-stu-id="b6790-210">Indicates that renewal of this license is allowed.</span></span> <span data-ttu-id="b6790-211">Se for true, a duração da licença poderá ser estendida por pulsação.</span><span class="sxs-lookup"><span data-stu-id="b6790-211">If true, the duration of the license can be extended by heartbeat.</span></span> <span data-ttu-id="b6790-212">O padrão é falso.</span><span class="sxs-lookup"><span data-stu-id="b6790-212">Default is false.</span></span> |
| <span data-ttu-id="b6790-213">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="b6790-213">policy_overrides.</span></span> <span data-ttu-id="b6790-214">license_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="b6790-214">license_duration_seconds</span></span> |<span data-ttu-id="b6790-215">int64</span><span class="sxs-lookup"><span data-stu-id="b6790-215">int64</span></span> |<span data-ttu-id="b6790-216">Indica o período para esta licença específica.</span><span class="sxs-lookup"><span data-stu-id="b6790-216">Indicates the time window for this specific license.</span></span> <span data-ttu-id="b6790-217">Um valor 0 indica que não há qualquer limite para a duração.</span><span class="sxs-lookup"><span data-stu-id="b6790-217">A value of 0 indicates that there is no limit to the duration.</span></span> <span data-ttu-id="b6790-218">O padrão é 0.</span><span class="sxs-lookup"><span data-stu-id="b6790-218">Default is 0.</span></span> |
| <span data-ttu-id="b6790-219">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="b6790-219">policy_overrides.</span></span> <span data-ttu-id="b6790-220">rental_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="b6790-220">rental_duration_seconds</span></span> |<span data-ttu-id="b6790-221">int64</span><span class="sxs-lookup"><span data-stu-id="b6790-221">int64</span></span> |<span data-ttu-id="b6790-222">Indica o período em que a reprodução é permitida.</span><span class="sxs-lookup"><span data-stu-id="b6790-222">Indicates the time window while playback is permitted.</span></span> <span data-ttu-id="b6790-223">Um valor 0 indica que não há qualquer limite para a duração.</span><span class="sxs-lookup"><span data-stu-id="b6790-223">A value of 0 indicates that there is no limit to the duration.</span></span> <span data-ttu-id="b6790-224">O padrão é 0.</span><span class="sxs-lookup"><span data-stu-id="b6790-224">Default is 0.</span></span> |
| <span data-ttu-id="b6790-225">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="b6790-225">policy_overrides.</span></span> <span data-ttu-id="b6790-226">playback_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="b6790-226">playback_duration_seconds</span></span> |<span data-ttu-id="b6790-227">int64</span><span class="sxs-lookup"><span data-stu-id="b6790-227">int64</span></span> |<span data-ttu-id="b6790-228">O período de exibição após o início da reprodução dentro da duração da licença.</span><span class="sxs-lookup"><span data-stu-id="b6790-228">The viewing window of time once playback starts within the license duration.</span></span> <span data-ttu-id="b6790-229">Um valor 0 indica que não há qualquer limite para a duração.</span><span class="sxs-lookup"><span data-stu-id="b6790-229">A value of 0 indicates that there is no limit to the duration.</span></span> <span data-ttu-id="b6790-230">O padrão é 0.</span><span class="sxs-lookup"><span data-stu-id="b6790-230">Default is 0.</span></span> |
| <span data-ttu-id="b6790-231">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="b6790-231">policy_overrides.</span></span> <span data-ttu-id="b6790-232">renewal_server_url</span><span class="sxs-lookup"><span data-stu-id="b6790-232">renewal_server_url</span></span> |<span data-ttu-id="b6790-233">string</span><span class="sxs-lookup"><span data-stu-id="b6790-233">string</span></span> |<span data-ttu-id="b6790-234">Todas as solicitações de pulsação (renovação) para esta licença devem ser direcionadas à URL especificada.</span><span class="sxs-lookup"><span data-stu-id="b6790-234">All heartbeat (renewal) requests for this license shall be directed to the specified URL.</span></span> <span data-ttu-id="b6790-235">Este campo só será usado se can_renew for true.</span><span class="sxs-lookup"><span data-stu-id="b6790-235">This field is only used if can_renew is true.</span></span> |
| <span data-ttu-id="b6790-236">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="b6790-236">policy_overrides.</span></span> <span data-ttu-id="b6790-237">renewal_delay_seconds</span><span class="sxs-lookup"><span data-stu-id="b6790-237">renewal_delay_seconds</span></span> |<span data-ttu-id="b6790-238">int64</span><span class="sxs-lookup"><span data-stu-id="b6790-238">int64</span></span> |<span data-ttu-id="b6790-239">O número de segundos após license_start_time, antes da primeira tentativa de renovação.</span><span class="sxs-lookup"><span data-stu-id="b6790-239">How many seconds after license_start_time, before renewal is first attempted.</span></span> <span data-ttu-id="b6790-240">Este campo só será usado se can_renew for true.</span><span class="sxs-lookup"><span data-stu-id="b6790-240">This field is only used if can_renew is true.</span></span> <span data-ttu-id="b6790-241">O padrão é 0</span><span class="sxs-lookup"><span data-stu-id="b6790-241">Default is 0</span></span> |
| <span data-ttu-id="b6790-242">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="b6790-242">policy_overrides.</span></span> <span data-ttu-id="b6790-243">renewal_retry_interval_seconds</span><span class="sxs-lookup"><span data-stu-id="b6790-243">renewal_retry_interval_seconds</span></span> |<span data-ttu-id="b6790-244">int64</span><span class="sxs-lookup"><span data-stu-id="b6790-244">int64</span></span> |<span data-ttu-id="b6790-245">Especifica o atraso em segundos entre as solicitações de renovação da licença subsequentes, em caso de falha.</span><span class="sxs-lookup"><span data-stu-id="b6790-245">Specifies the delay in seconds between subsequent license renewal requests, in case of failure.</span></span> <span data-ttu-id="b6790-246">Este campo só será usado se can_renew for true.</span><span class="sxs-lookup"><span data-stu-id="b6790-246">This field is only used if can_renew is true.</span></span> |
| <span data-ttu-id="b6790-247">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="b6790-247">policy_overrides.</span></span> <span data-ttu-id="b6790-248">renewal_recovery_duration_seconds</span><span class="sxs-lookup"><span data-stu-id="b6790-248">renewal_recovery_duration_seconds</span></span> |<span data-ttu-id="b6790-249">int64</span><span class="sxs-lookup"><span data-stu-id="b6790-249">int64</span></span> |<span data-ttu-id="b6790-250">O período durante o qual a reprodução é permitida enquanto ocorre a tentativa de renovação, porém sem êxito devido a problemas de back-end com o servidor de licença.</span><span class="sxs-lookup"><span data-stu-id="b6790-250">The window of time, in which playback is allowed to continue while renewal is attempted, yet unsuccessful due to backend problems with the license server.</span></span> <span data-ttu-id="b6790-251">Um valor 0 indica que não há qualquer limite para a duração.</span><span class="sxs-lookup"><span data-stu-id="b6790-251">A value of 0 indicates that there is no limit to the duration.</span></span> <span data-ttu-id="b6790-252">Este campo só será usado se can_renew for true.</span><span class="sxs-lookup"><span data-stu-id="b6790-252">This field is only used if can_renew is true.</span></span> |
| <span data-ttu-id="b6790-253">policy_overrides.</span><span class="sxs-lookup"><span data-stu-id="b6790-253">policy_overrides.</span></span> <span data-ttu-id="b6790-254">renew_with_usage</span><span class="sxs-lookup"><span data-stu-id="b6790-254">renew_with_usage</span></span> |<span data-ttu-id="b6790-255">booliano true ou false</span><span class="sxs-lookup"><span data-stu-id="b6790-255">boolean true or false</span></span> |<span data-ttu-id="b6790-256">Indica que a licença deve ser enviada para renovação quando o uso for iniciado.</span><span class="sxs-lookup"><span data-stu-id="b6790-256">Indicates that the license shall be sent for renewal when usage is started.</span></span> <span data-ttu-id="b6790-257">Este campo só será usado se can_renew for true.</span><span class="sxs-lookup"><span data-stu-id="b6790-257">This field is only used if can_renew is true.</span></span> |

## <a name="session-initialization"></a><span data-ttu-id="b6790-258">Inicialização da sessão</span><span class="sxs-lookup"><span data-stu-id="b6790-258">Session Initialization</span></span>
| <span data-ttu-id="b6790-259">Nome</span><span class="sxs-lookup"><span data-stu-id="b6790-259">Name</span></span> | <span data-ttu-id="b6790-260">Valor</span><span class="sxs-lookup"><span data-stu-id="b6790-260">Value</span></span> | <span data-ttu-id="b6790-261">Descrição</span><span class="sxs-lookup"><span data-stu-id="b6790-261">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b6790-262">provider_session_token</span><span class="sxs-lookup"><span data-stu-id="b6790-262">provider_session_token</span></span> |<span data-ttu-id="b6790-263">Cadeia codificada em Base64</span><span class="sxs-lookup"><span data-stu-id="b6790-263">Base64 encoded string</span></span> |<span data-ttu-id="b6790-264">Este token de sessão é repassado na licença e continuará a existir em renovações subsequentes.</span><span class="sxs-lookup"><span data-stu-id="b6790-264">This session token is passed back in the license and will exist in subsequent renewals.</span></span>  <span data-ttu-id="b6790-265">O token de sessão não persistirá além das sessões.</span><span class="sxs-lookup"><span data-stu-id="b6790-265">The session token will not persist beyond sessions.</span></span> |
| <span data-ttu-id="b6790-266">provider_client_token</span><span class="sxs-lookup"><span data-stu-id="b6790-266">provider_client_token</span></span> |<span data-ttu-id="b6790-267">Cadeia codificada em Base64</span><span class="sxs-lookup"><span data-stu-id="b6790-267">Base64 encoded string</span></span> |<span data-ttu-id="b6790-268">Token de cliente para envio na resposta da licença.</span><span class="sxs-lookup"><span data-stu-id="b6790-268">Client token to send back in the license response.</span></span>  <span data-ttu-id="b6790-269">Se a solicitação de licença contiver um token de cliente, esse valor será ignorado.</span><span class="sxs-lookup"><span data-stu-id="b6790-269">If the license request contains a client token, this value is ignored.</span></span> <span data-ttu-id="b6790-270">O token do cliente persistirá além das sessões da licença.</span><span class="sxs-lookup"><span data-stu-id="b6790-270">The client token will persist beyond license sessions.</span></span> |
| <span data-ttu-id="b6790-271">override_provider_client_token</span><span class="sxs-lookup"><span data-stu-id="b6790-271">override_provider_client_token</span></span> |<span data-ttu-id="b6790-272">booliano.</span><span class="sxs-lookup"><span data-stu-id="b6790-272">boolean.</span></span> <span data-ttu-id="b6790-273">true ou false</span><span class="sxs-lookup"><span data-stu-id="b6790-273">true or false</span></span> |<span data-ttu-id="b6790-274">Se for false e a solicitação de licença contiver um token de cliente, use o token da solicitação mesmo se houver um token do cliente especificado nessa estrutura.</span><span class="sxs-lookup"><span data-stu-id="b6790-274">If false and the license request contains a client token, use the token from the request even if a client token was specified in this structure.</span></span>  <span data-ttu-id="b6790-275">Se for true, sempre use o token especificado nessa estrutura.</span><span class="sxs-lookup"><span data-stu-id="b6790-275">If true, always use the token specified in this structure.</span></span> |

## <a name="configure-your-widevine-licenses-using-net-types"></a><span data-ttu-id="b6790-276">Configurar suas licenças do Widevine usando tipos .NET</span><span class="sxs-lookup"><span data-stu-id="b6790-276">Configure your Widevine licenses using .NET types</span></span>
<span data-ttu-id="b6790-277">Os Serviços de Mídia fornecem APIs .NET que permitem a configuração de suas licenças do Widevine.</span><span class="sxs-lookup"><span data-stu-id="b6790-277">Media Services provides .NET APIs that let you configure your Widevine licenses.</span></span> 

### <a name="classes-as-defined-in-the-media-services-net-sdk"></a><span data-ttu-id="b6790-278">Classes, como definido no SDK do .NET dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="b6790-278">Classes as defined in the Media Services .NET SDK</span></span>
<span data-ttu-id="b6790-279">Veja a seguir as definições desses tipos.</span><span class="sxs-lookup"><span data-stu-id="b6790-279">The following are the definitions of these types.</span></span>

    public class WidevineMessage
    {
        public WidevineMessage();

        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public AllowedTrackTypes? allowed_track_types { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public ContentKeySpecs[] content_key_specs { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public object policy_overrides { get; set; }
    }

    [JsonConverter(typeof(StringEnumConverter))]
    public enum AllowedTrackTypes
    {
        SD_ONLY = 0,
        SD_HD = 1
    }
    public class ContentKeySpecs
    {
        public ContentKeySpecs();

        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public string key_id { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public RequiredOutputProtection required_output_protection { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public int? security_level { get; set; }
        [JsonProperty(NullValueHandling = NullValueHandling.Ignore)]
        public string track_type { get; set; }
    }

    public class RequiredOutputProtection
    {
        public RequiredOutputProtection();

        public Hdcp hdcp { get; set; }
    }

    [JsonConverter(typeof(StringEnumConverter))]
    public enum Hdcp
    {
        HDCP_NONE = 0,
        HDCP_V1 = 1,
        HDCP_V2 = 2
    }

### <a name="example"></a><span data-ttu-id="b6790-280">Exemplo</span><span class="sxs-lookup"><span data-stu-id="b6790-280">Example</span></span>
<span data-ttu-id="b6790-281">O exemplo a seguir mostra como usar as APIs do .NET para configurar uma licença simples do Widevine.</span><span class="sxs-lookup"><span data-stu-id="b6790-281">The following example shows how to use .NET APIs to configure  a simple Widevine license.</span></span>

    private static string ConfigureWidevineLicenseTemplate()
    {
        var template = new WidevineMessage
        {
            allowed_track_types = AllowedTrackTypes.SD_HD,
            content_key_specs = new[]
            {
                new ContentKeySpecs
                {
                    required_output_protection = new RequiredOutputProtection { hdcp = Hdcp.HDCP_NONE},
                    security_level = 1,
                    track_type = "SD"
                }
            },
            policy_overrides = new
            {
                can_play = true,
                can_persist = true,
                can_renew = false
            }
        };

        string configuration = JsonConvert.SerializeObject(template);
        return configuration;
    }


## <a name="media-services-learning-paths"></a><span data-ttu-id="b6790-282">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="b6790-282">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="b6790-283">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="b6790-283">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a><span data-ttu-id="b6790-284">Consulte também</span><span class="sxs-lookup"><span data-stu-id="b6790-284">See also</span></span>
[<span data-ttu-id="b6790-285">Usando a PlayReady e/ou a Criptografia Comum Dinâmica Widevine</span><span class="sxs-lookup"><span data-stu-id="b6790-285">Using PlayReady and/or Widevine Dynamic Common Encryption</span></span>](media-services-protect-with-drm.md)

