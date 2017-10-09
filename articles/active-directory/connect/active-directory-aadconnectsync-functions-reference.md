---
title: "Sincronização do Azure AD Connect: referência de funções | Microsoft Docs"
description: "Referência de expressões de provisionamento declarativo na sincronização do Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 4f525ca0-be0e-4a2e-8da1-09b6b567ed5f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: fbe0df856ca2efda965650fb85c7e831a0be32c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-functions-reference"></a><span data-ttu-id="86613-103">Azure AD Connect Sync: referência de funções</span><span class="sxs-lookup"><span data-stu-id="86613-103">Azure AD Connect sync: Functions Reference</span></span>
<span data-ttu-id="86613-104">No Azure AD Connect, funções são toomanipulate usado um valor de atributo durante a sincronização.</span><span class="sxs-lookup"><span data-stu-id="86613-104">In Azure AD Connect, functions are used toomanipulate an attribute value during synchronization.</span></span>  
<span data-ttu-id="86613-105">Olá sintaxe de funções de saudação é expressa usando Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="86613-105">hello Syntax of hello functions is expressed using hello following format:</span></span>  
`<output type> FunctionName(<input type> <position name>, ..)`

<span data-ttu-id="86613-106">Se uma função está sobrecarregada e aceita diversas sintaxes, todas as sintaxes válidas são listadas.</span><span class="sxs-lookup"><span data-stu-id="86613-106">If a function is overloaded and accepts multiple syntaxes, all valid syntaxes are listed.</span></span>  
<span data-ttu-id="86613-107">Olá funções são fortemente tipadas e verificam que tipo de saudação passado no tipo de Olá documentado de correspondências.</span><span class="sxs-lookup"><span data-stu-id="86613-107">hello functions are strongly typed and they verify that hello type passed in matches hello documented type.</span></span>  
<span data-ttu-id="86613-108">Se o tipo de saudação não corresponder, um erro será lançado.</span><span class="sxs-lookup"><span data-stu-id="86613-108">If hello type does not match, an error is thrown.</span></span>

<span data-ttu-id="86613-109">Olá tipos são expressos com hello sintaxe a seguir:</span><span class="sxs-lookup"><span data-stu-id="86613-109">hello types are expressed with hello following syntax:</span></span>

* <span data-ttu-id="86613-110">**bin** - binário</span><span class="sxs-lookup"><span data-stu-id="86613-110">**bin** – Binary</span></span>
* <span data-ttu-id="86613-111">**bool** - booliano</span><span class="sxs-lookup"><span data-stu-id="86613-111">**bool** – Boolean</span></span>
* <span data-ttu-id="86613-112">**dt** - data/hora UTC</span><span class="sxs-lookup"><span data-stu-id="86613-112">**dt** – UTC Date/Time</span></span>
* <span data-ttu-id="86613-113">**enum** - enumeração das constantes conhecidas</span><span class="sxs-lookup"><span data-stu-id="86613-113">**enum** – Enumeration of known constants</span></span>
* <span data-ttu-id="86613-114">**EXP** – expressão, que é esperado tooevaluate tooa booliano</span><span class="sxs-lookup"><span data-stu-id="86613-114">**exp** – Expression, which is expected tooevaluate tooa Boolean</span></span>
* <span data-ttu-id="86613-115">**mvbin** - Binário de Valores Múltiplos</span><span class="sxs-lookup"><span data-stu-id="86613-115">**mvbin** – Multi-Valued Binary</span></span>
* <span data-ttu-id="86613-116">**mvstr** - Cadeia de Caracteres de Valores Múltiplos</span><span class="sxs-lookup"><span data-stu-id="86613-116">**mvstr** – Multi-Valued String</span></span>
* <span data-ttu-id="86613-117">**mvstr** - Referência de Valores Múltiplos</span><span class="sxs-lookup"><span data-stu-id="86613-117">**mvref** – Multi-Valued Reference</span></span>
* <span data-ttu-id="86613-118">**num** - numérico</span><span class="sxs-lookup"><span data-stu-id="86613-118">**num** – Numeric</span></span>
* <span data-ttu-id="86613-119">**ref** – Referência</span><span class="sxs-lookup"><span data-stu-id="86613-119">**ref** – Reference</span></span>
* <span data-ttu-id="86613-120">**str** – Cadeia de Caracteres</span><span class="sxs-lookup"><span data-stu-id="86613-120">**str** – String</span></span>
* <span data-ttu-id="86613-121">**var** - uma variante de (quase) qualquer outro tipo</span><span class="sxs-lookup"><span data-stu-id="86613-121">**var** – A variant of (almost) any other type</span></span>
* <span data-ttu-id="86613-122">**void** - não retorna um valor</span><span class="sxs-lookup"><span data-stu-id="86613-122">**void** – doesn’t return a value</span></span>

<span data-ttu-id="86613-123">Olá funções com tipos de saudação **mvbin**, **mvstr**, e **mvref** funciona somente em atributos com valores múltiplos.</span><span class="sxs-lookup"><span data-stu-id="86613-123">hello functions with hello types **mvbin**, **mvstr**, and **mvref** can only work on multi-valued attributes.</span></span> <span data-ttu-id="86613-124">As funções com **bin**, **str** e **ref** funcionam nos atributos de valor único e valores múltiplos.</span><span class="sxs-lookup"><span data-stu-id="86613-124">Functions with **bin**, **str**, and **ref** work on both single-valued and multi-valued attributes.</span></span>

## <a name="functions-reference"></a><span data-ttu-id="86613-125">Referência de funções</span><span class="sxs-lookup"><span data-stu-id="86613-125">Functions Reference</span></span>
| <span data-ttu-id="86613-126">Lista de funções</span><span class="sxs-lookup"><span data-stu-id="86613-126">List of functions</span></span> |  |  |  |  |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="86613-127">**Certificate**</span><span class="sxs-lookup"><span data-stu-id="86613-127">**Certificate**</span></span> | | | | |
| [<span data-ttu-id="86613-128">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="86613-128">CertExtensionOids</span></span>](#certextensionoids) |[<span data-ttu-id="86613-129">CertFormat</span><span class="sxs-lookup"><span data-stu-id="86613-129">CertFormat</span></span>](#certformat) |[<span data-ttu-id="86613-130">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="86613-130">CertFriendlyName</span></span>](#certfriendlyname) |[<span data-ttu-id="86613-131">CertHashString</span><span class="sxs-lookup"><span data-stu-id="86613-131">CertHashString</span></span>](#certhashstring) | |
| [<span data-ttu-id="86613-132">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="86613-132">CertIssuer</span></span>](#certissuer) |[<span data-ttu-id="86613-133">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="86613-133">CertIssuerDN</span></span>](#certissuerdn) |[<span data-ttu-id="86613-134">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="86613-134">CertIssuerOid</span></span>](#certissueroid) |[<span data-ttu-id="86613-135">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="86613-135">CertKeyAlgorithm</span></span>](#certkeyalgorithm) | |
| [<span data-ttu-id="86613-136">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="86613-136">CertKeyAlgorithmParams</span></span>](#certkeyalgorithmparams) |[<span data-ttu-id="86613-137">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="86613-137">CertNameInfo</span></span>](#certnameinfo) |[<span data-ttu-id="86613-138">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="86613-138">CertNotAfter</span></span>](#certnotafter) |[<span data-ttu-id="86613-139">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="86613-139">CertNotBefore</span></span>](#certnotbefore) | |
| [<span data-ttu-id="86613-140">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="86613-140">CertPublicKeyOid</span></span>](#certpublickeyoid) |[<span data-ttu-id="86613-141">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="86613-141">CertPublicKeyParametersOid</span></span>](#certpublickeyparametersoid) |[<span data-ttu-id="86613-142">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="86613-142">CertSerialNumber</span></span>](#certserialnumber) |[<span data-ttu-id="86613-143">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="86613-143">CertSignatureAlgorithmOid</span></span>](#certsignaturealgorithmoid) | |
| [<span data-ttu-id="86613-144">CertSubject</span><span class="sxs-lookup"><span data-stu-id="86613-144">CertSubject</span></span>](#certsubject) |[<span data-ttu-id="86613-145">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="86613-145">CertSubjectNameDN</span></span>](#certsubjectnamedn) |[<span data-ttu-id="86613-146">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="86613-146">CertSubjectNameOid</span></span>](#certsubjectnameoid) |[<span data-ttu-id="86613-147">CertThumbprint</span><span class="sxs-lookup"><span data-stu-id="86613-147">CertThumbprint</span></span>](#certthumbprint) | |
[<span data-ttu-id="86613-148"> CertVersion</span><span class="sxs-lookup"><span data-stu-id="86613-148"> CertVersion</span></span>](#certversion) |[<span data-ttu-id="86613-149">IsCert</span><span class="sxs-lookup"><span data-stu-id="86613-149">IsCert</span></span>](#iscert) | | | |
| <span data-ttu-id="86613-150">**Conversão**</span><span class="sxs-lookup"><span data-stu-id="86613-150">**Conversion**</span></span> | | | | |
| [<span data-ttu-id="86613-151">CBool</span><span class="sxs-lookup"><span data-stu-id="86613-151">CBool</span></span>](#cbool) |[<span data-ttu-id="86613-152">CDate</span><span class="sxs-lookup"><span data-stu-id="86613-152">CDate</span></span>](#cdate) |[<span data-ttu-id="86613-153">CGuid</span><span class="sxs-lookup"><span data-stu-id="86613-153">CGuid</span></span>](#cguid) |[<span data-ttu-id="86613-154">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="86613-154">ConvertFromBase64</span></span>](#convertfrombase64) | |
| [<span data-ttu-id="86613-155">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="86613-155">ConvertToBase64</span></span>](#converttobase64) |[<span data-ttu-id="86613-156">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="86613-156">ConvertFromUTF8Hex</span></span>](#convertfromutf8hex) |[<span data-ttu-id="86613-157">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="86613-157">ConvertToUTF8Hex</span></span>](#converttoutf8hex) |[<span data-ttu-id="86613-158">CNum</span><span class="sxs-lookup"><span data-stu-id="86613-158">CNum</span></span>](#cnum) | |
| [<span data-ttu-id="86613-159">CRef</span><span class="sxs-lookup"><span data-stu-id="86613-159">CRef</span></span>](#cref) |[<span data-ttu-id="86613-160">CStr</span><span class="sxs-lookup"><span data-stu-id="86613-160">CStr</span></span>](#cstr) |[<span data-ttu-id="86613-161">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="86613-161">StringFromGuid</span></span>](#StringFromGuid) |[<span data-ttu-id="86613-162">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="86613-162">StringFromSid</span></span>](#stringfromsid) | |
| <span data-ttu-id="86613-163">**Data / hora**</span><span class="sxs-lookup"><span data-stu-id="86613-163">**Date / Time**</span></span> | | | | |
| [<span data-ttu-id="86613-164">DateAdd</span><span class="sxs-lookup"><span data-stu-id="86613-164">DateAdd</span></span>](#dateadd) |[<span data-ttu-id="86613-165">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="86613-165">DateFromNum</span></span>](#datefromnum) |[<span data-ttu-id="86613-166">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="86613-166">FormatDateTime</span></span>](#formatdatetime) |[<span data-ttu-id="86613-167">Now</span><span class="sxs-lookup"><span data-stu-id="86613-167">Now</span></span>](#now) | |
| [<span data-ttu-id="86613-168">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="86613-168">NumFromDate</span></span>](#numfromdate) | | | | |
| <span data-ttu-id="86613-169">**Diretório**</span><span class="sxs-lookup"><span data-stu-id="86613-169">**Directory**</span></span> | | | | |
| [<span data-ttu-id="86613-170">DNComponent</span><span class="sxs-lookup"><span data-stu-id="86613-170">DNComponent</span></span>](#dncomponent) |[<span data-ttu-id="86613-171">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="86613-171">DNComponentRev</span></span>](#dncomponentrev) |[<span data-ttu-id="86613-172">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="86613-172">EscapeDNComponent</span></span>](#escapedncomponent) | | |
| <span data-ttu-id="86613-173">**Avaliação**</span><span class="sxs-lookup"><span data-stu-id="86613-173">**Evaluation**</span></span> | | | | |
| [<span data-ttu-id="86613-174">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="86613-174">IsBitSet</span></span>](#isbitset) |[<span data-ttu-id="86613-175">IsDate</span><span class="sxs-lookup"><span data-stu-id="86613-175">IsDate</span></span>](#isdate) |[<span data-ttu-id="86613-176">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="86613-176">IsEmpty</span></span>](#isempty) |[<span data-ttu-id="86613-177">IsGuid</span><span class="sxs-lookup"><span data-stu-id="86613-177">IsGuid</span></span>](#isguid) | |
| [<span data-ttu-id="86613-178">IsNull</span><span class="sxs-lookup"><span data-stu-id="86613-178">IsNull</span></span>](#isnull) |[<span data-ttu-id="86613-179">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="86613-179">IsNullOrEmpty</span></span>](#isnullorempty) |[<span data-ttu-id="86613-180">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="86613-180">IsNumeric</span></span>](#isnumeric) |[<span data-ttu-id="86613-181">IsPresent</span><span class="sxs-lookup"><span data-stu-id="86613-181">IsPresent</span></span>](#ispresent) | |
| [<span data-ttu-id="86613-182">IsString</span><span class="sxs-lookup"><span data-stu-id="86613-182">IsString</span></span>](#isstring) | | | | |
| <span data-ttu-id="86613-183">**Matemática**</span><span class="sxs-lookup"><span data-stu-id="86613-183">**Math**</span></span> | | | | |
| [<span data-ttu-id="86613-184">BitAnd</span><span class="sxs-lookup"><span data-stu-id="86613-184">BitAnd</span></span>](#bitand) |[<span data-ttu-id="86613-185">BitOr</span><span class="sxs-lookup"><span data-stu-id="86613-185">BitOr</span></span>](#bitor) |[<span data-ttu-id="86613-186">RandomNum</span><span class="sxs-lookup"><span data-stu-id="86613-186">RandomNum</span></span>](#randomnum) | | |
| <span data-ttu-id="86613-187">**De valores múltiplos**</span><span class="sxs-lookup"><span data-stu-id="86613-187">**Multi-valued**</span></span> | | | | |
| [<span data-ttu-id="86613-188">Contém:</span><span class="sxs-lookup"><span data-stu-id="86613-188">Contains</span></span>](#contains) |[<span data-ttu-id="86613-189">Contagem</span><span class="sxs-lookup"><span data-stu-id="86613-189">Count</span></span>](#count) |[<span data-ttu-id="86613-190">Item</span><span class="sxs-lookup"><span data-stu-id="86613-190">Item</span></span>](#item) |[<span data-ttu-id="86613-191">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="86613-191">ItemOrNull</span></span>](#itemornull) | |
| [<span data-ttu-id="86613-192">Join</span><span class="sxs-lookup"><span data-stu-id="86613-192">Join</span></span>](#join) |[<span data-ttu-id="86613-193">RemoveDuplicates</span><span class="sxs-lookup"><span data-stu-id="86613-193">RemoveDuplicates</span></span>](#removeduplicates) |[<span data-ttu-id="86613-194">Divisão</span><span class="sxs-lookup"><span data-stu-id="86613-194">Split</span></span>](#split) | | |
| <span data-ttu-id="86613-195">**Fluxo do Programa**</span><span class="sxs-lookup"><span data-stu-id="86613-195">**Program Flow**</span></span> | | | | |
| [<span data-ttu-id="86613-196">Erro</span><span class="sxs-lookup"><span data-stu-id="86613-196">Error</span></span>](#error) |[<span data-ttu-id="86613-197">IIF</span><span class="sxs-lookup"><span data-stu-id="86613-197">IIF</span></span>](#iif) |[<span data-ttu-id="86613-198">Seleção</span><span class="sxs-lookup"><span data-stu-id="86613-198">Select</span></span>](#select) |[<span data-ttu-id="86613-199">Switch</span><span class="sxs-lookup"><span data-stu-id="86613-199">Switch</span></span>](#switch) | |
| [<span data-ttu-id="86613-200">Onde</span><span class="sxs-lookup"><span data-stu-id="86613-200">Where</span></span>](#where) |[<span data-ttu-id="86613-201">With</span><span class="sxs-lookup"><span data-stu-id="86613-201">With</span></span>](#with) | | | |
| <span data-ttu-id="86613-202">**Texto**</span><span class="sxs-lookup"><span data-stu-id="86613-202">**Text**</span></span> | | | | |
| [<span data-ttu-id="86613-203">GUID</span><span class="sxs-lookup"><span data-stu-id="86613-203">GUID</span></span>](#guid) |[<span data-ttu-id="86613-204">InStr</span><span class="sxs-lookup"><span data-stu-id="86613-204">InStr</span></span>](#instr) |[<span data-ttu-id="86613-205">InStrRev</span><span class="sxs-lookup"><span data-stu-id="86613-205">InStrRev</span></span>](#instrrev) |[<span data-ttu-id="86613-206">LCase</span><span class="sxs-lookup"><span data-stu-id="86613-206">LCase</span></span>](#lcase) | |
| [<span data-ttu-id="86613-207">Left</span><span class="sxs-lookup"><span data-stu-id="86613-207">Left</span></span>](#left) |[<span data-ttu-id="86613-208">Len</span><span class="sxs-lookup"><span data-stu-id="86613-208">Len</span></span>](#len) |[<span data-ttu-id="86613-209">LTrim</span><span class="sxs-lookup"><span data-stu-id="86613-209">LTrim</span></span>](#ltrim) |[<span data-ttu-id="86613-210">Mid</span><span class="sxs-lookup"><span data-stu-id="86613-210">Mid</span></span>](#mid) | |
| [<span data-ttu-id="86613-211">PadLeft</span><span class="sxs-lookup"><span data-stu-id="86613-211">PadLeft</span></span>](#padleft) |[<span data-ttu-id="86613-212">PadRight</span><span class="sxs-lookup"><span data-stu-id="86613-212">PadRight</span></span>](#padright) |[<span data-ttu-id="86613-213">PCase</span><span class="sxs-lookup"><span data-stu-id="86613-213">PCase</span></span>](#pcase) |[<span data-ttu-id="86613-214">Substitua</span><span class="sxs-lookup"><span data-stu-id="86613-214">Replace</span></span>](#replace) | |
| [<span data-ttu-id="86613-215">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="86613-215">ReplaceChars</span></span>](#replacechars) |[<span data-ttu-id="86613-216">Right</span><span class="sxs-lookup"><span data-stu-id="86613-216">Right</span></span>](#right) |[<span data-ttu-id="86613-217">RTrim</span><span class="sxs-lookup"><span data-stu-id="86613-217">RTrim</span></span>](#rtrim) |[<span data-ttu-id="86613-218">Trim</span><span class="sxs-lookup"><span data-stu-id="86613-218">Trim</span></span>](#trim) | |
| [<span data-ttu-id="86613-219">UCase</span><span class="sxs-lookup"><span data-stu-id="86613-219">UCase</span></span>](#ucase) |[<span data-ttu-id="86613-220">Word</span><span class="sxs-lookup"><span data-stu-id="86613-220">Word</span></span>](#word) | | | |

- - -
### <a name="bitand"></a><span data-ttu-id="86613-221">BitAnd</span><span class="sxs-lookup"><span data-stu-id="86613-221">BitAnd</span></span>
<span data-ttu-id="86613-222">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-222">**Description:**</span></span>  
<span data-ttu-id="86613-223">Olá função BitAnd define bits específicos em um valor.</span><span class="sxs-lookup"><span data-stu-id="86613-223">hello BitAnd function sets specified bits on a value.</span></span>

<span data-ttu-id="86613-224">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-224">**Syntax:**</span></span>  
`num BitAnd(num value1, num value2)`

* <span data-ttu-id="86613-225">value1, value2: os valores numéricos que devem ser agrupados com AND</span><span class="sxs-lookup"><span data-stu-id="86613-225">value1, value2: numeric values that should be AND’ed together</span></span>

<span data-ttu-id="86613-226">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="86613-226">**Remarks:**</span></span>  
<span data-ttu-id="86613-227">Esta função converte ambos os representação binária de toohello parâmetros e define um bit:</span><span class="sxs-lookup"><span data-stu-id="86613-227">This function converts both parameters toohello binary representation and sets a bit to:</span></span>

* <span data-ttu-id="86613-228">0 - se uma ou ambas Olá bits correspondentes em *máscara* e *sinalizador* são 0</span><span class="sxs-lookup"><span data-stu-id="86613-228">0 - if one or both of hello corresponding bits in *mask* and *flag* are 0</span></span>
* <span data-ttu-id="86613-229">1 - se dois bits correspondentes Olá são 1.</span><span class="sxs-lookup"><span data-stu-id="86613-229">1 - if both of hello corresponding bits are 1.</span></span>

<span data-ttu-id="86613-230">Em outras palavras, ele retorna 0 em todos os casos, exceto quando o bits correspondentes de saudação de ambos os parâmetros são 1.</span><span class="sxs-lookup"><span data-stu-id="86613-230">In other words, it returns 0 in all cases except when hello corresponding bits of both parameters are 1.</span></span>

<span data-ttu-id="86613-231">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-231">**Example:**</span></span>  
`BitAnd(&HF, &HF7)`  
<span data-ttu-id="86613-232">Retorna 7 porque hexadecimal "F" e "F7" avaliam o valor de toothis.</span><span class="sxs-lookup"><span data-stu-id="86613-232">Returns 7 because hexadecimal "F" AND "F7" evaluate toothis value.</span></span>

- - -
### <a name="bitor"></a><span data-ttu-id="86613-233">BitOr</span><span class="sxs-lookup"><span data-stu-id="86613-233">BitOr</span></span>
<span data-ttu-id="86613-234">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-234">**Description:**</span></span>  
<span data-ttu-id="86613-235">Olá função BitOr define bits específicos em um valor.</span><span class="sxs-lookup"><span data-stu-id="86613-235">hello BitOr function sets specified bits on a value.</span></span>

<span data-ttu-id="86613-236">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-236">**Syntax:**</span></span>  
`num BitOr(num value1, num value2)`

* <span data-ttu-id="86613-237">value1, value2: valores numéricos que devem ser agrupados com OR</span><span class="sxs-lookup"><span data-stu-id="86613-237">value1, value2: numeric values that should be OR’ed together</span></span>

<span data-ttu-id="86613-238">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="86613-238">**Remarks:**</span></span>  
<span data-ttu-id="86613-239">Esta função converte ambos os representação binária de toohello parâmetros e define um bit too1 se um ou os dois bits correspondentes de saudação da máscara e o sinalizador são 1 e too0 se os dois bits correspondentes Olá são 0.</span><span class="sxs-lookup"><span data-stu-id="86613-239">This function converts both parameters toohello binary representation and sets a bit too1 if one or both of hello corresponding bits in mask and flag are 1, and too0 if both of hello corresponding bits are 0.</span></span> <span data-ttu-id="86613-240">Em outras palavras, ele retornará 1 em todos os casos, exceto onde os bits correspondentes de saudação de ambos os parâmetros são 0.</span><span class="sxs-lookup"><span data-stu-id="86613-240">In other words, it returns 1 in all cases except where hello corresponding bits of both parameters are 0.</span></span>

- - -
### <a name="cbool"></a><span data-ttu-id="86613-241">CBool</span><span class="sxs-lookup"><span data-stu-id="86613-241">CBool</span></span>
<span data-ttu-id="86613-242">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-242">**Description:**</span></span>  
<span data-ttu-id="86613-243">Olá Função CBool retorna que um valor booleano com base na expressão Olá avaliada</span><span class="sxs-lookup"><span data-stu-id="86613-243">hello CBool function returns a Boolean based on hello evaluated expression</span></span>

<span data-ttu-id="86613-244">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-244">**Syntax:**</span></span>  
`bool CBool(exp Expression)`

<span data-ttu-id="86613-245">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="86613-245">**Remarks:**</span></span>  
<span data-ttu-id="86613-246">Se Olá avalia tooa de valor diferente de zero, então o CBool retorna True, caso contrário retornará False.</span><span class="sxs-lookup"><span data-stu-id="86613-246">If hello expression evaluates tooa nonzero value, then CBool returns True, else it returns False.</span></span>

<span data-ttu-id="86613-247">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-247">**Example:**</span></span>  
`CBool([attrib1] = [attrib2])`  

<span data-ttu-id="86613-248">Retorna True se ambos os atributos têm Olá mesmo valor.</span><span class="sxs-lookup"><span data-stu-id="86613-248">Returns True if both attributes have hello same value.</span></span>

- - -
### <a name="cdate"></a><span data-ttu-id="86613-249">CDate</span><span class="sxs-lookup"><span data-stu-id="86613-249">CDate</span></span>
<span data-ttu-id="86613-250">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-250">**Description:**</span></span>  
<span data-ttu-id="86613-251">Olá função CDate retorna um DateTime UTC de uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="86613-251">hello CDate function returns a UTC DateTime from a string.</span></span> <span data-ttu-id="86613-252">DateTime não é um tipo de atributo nativo no Sync, mas é usado por algumas funções.</span><span class="sxs-lookup"><span data-stu-id="86613-252">DateTime is not a native attribute type in Sync but is used by some functions.</span></span>

<span data-ttu-id="86613-253">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-253">**Syntax:**</span></span>  
`dt CDate(str value)`

* <span data-ttu-id="86613-254">Value: uma cadeia de caracteres com uma data, hora e opcionalmente um fuso horário</span><span class="sxs-lookup"><span data-stu-id="86613-254">Value: A string with a date, time, and optionally time zone</span></span>

<span data-ttu-id="86613-255">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="86613-255">**Remarks:**</span></span>  
<span data-ttu-id="86613-256">Olá retornou uma cadeia de caracteres é sempre UTC.</span><span class="sxs-lookup"><span data-stu-id="86613-256">hello returned string is always in UTC.</span></span>

<span data-ttu-id="86613-257">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-257">**Example:**</span></span>  
`CDate([employeeStartTime])`  
<span data-ttu-id="86613-258">Retorna um DateTime com base na hora de início do funcionário Olá</span><span class="sxs-lookup"><span data-stu-id="86613-258">Returns a DateTime based on hello employee’s start time</span></span>

`CDate("2013-01-10 4:00 PM -8")`  
<span data-ttu-id="86613-259">Retorna um DateTime que representa "11/01/2013 12:00"</span><span class="sxs-lookup"><span data-stu-id="86613-259">Returns a DateTime representing "2013-01-11 12:00 AM"</span></span>








- - -
### <a name="certextensionoids"></a><span data-ttu-id="86613-260">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="86613-260">CertExtensionOids</span></span>
<span data-ttu-id="86613-261">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-261">**Description:**</span></span>  
<span data-ttu-id="86613-262">Retorna Olá valores de Oid de todas as extensões críticas de saudação de um objeto de certificado.</span><span class="sxs-lookup"><span data-stu-id="86613-262">Returns hello Oid values of all hello critical extensions of a certificate object.</span></span>

<span data-ttu-id="86613-263">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-263">**Syntax:**</span></span>  
`mvstr CertExtensionOids(binary certificateRawData)`  
*   <span data-ttu-id="86613-264">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="86613-264">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="86613-265">matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.</span><span class="sxs-lookup"><span data-stu-id="86613-265">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certformat"></a><span data-ttu-id="86613-266">CertFormat</span><span class="sxs-lookup"><span data-stu-id="86613-266">CertFormat</span></span>
<span data-ttu-id="86613-267">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-267">**Description:**</span></span>  
<span data-ttu-id="86613-268">Retorna Olá nome do formato de saudação do certificado x. 509v3.</span><span class="sxs-lookup"><span data-stu-id="86613-268">Returns hello name of hello format of this X.509v3 certificate.</span></span>

<span data-ttu-id="86613-269">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-269">**Syntax:**</span></span>  
`str CertFormat(binary certificateRawData)`  
*   <span data-ttu-id="86613-270">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="86613-270">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="86613-271">matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.</span><span class="sxs-lookup"><span data-stu-id="86613-271">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certfriendlyname"></a><span data-ttu-id="86613-272">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="86613-272">CertFriendlyName</span></span>
<span data-ttu-id="86613-273">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-273">**Description:**</span></span>  
<span data-ttu-id="86613-274">Retorna a saudação alias associada um certificado.</span><span class="sxs-lookup"><span data-stu-id="86613-274">Returns hello associated alias for a certificate.</span></span>

<span data-ttu-id="86613-275">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-275">**Syntax:**</span></span>  
`str CertFriendlyName(binary certificateRawData)`  
*   <span data-ttu-id="86613-276">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="86613-276">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="86613-277">matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.</span><span class="sxs-lookup"><span data-stu-id="86613-277">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certhashstring"></a><span data-ttu-id="86613-278">CertHashString</span><span class="sxs-lookup"><span data-stu-id="86613-278">CertHashString</span></span>
<span data-ttu-id="86613-279">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-279">**Description:**</span></span>  
<span data-ttu-id="86613-280">Retorna Olá valor de hash SHA1 para certificado de x. 509v3 hello como uma cadeia de caracteres hexadecimal.</span><span class="sxs-lookup"><span data-stu-id="86613-280">Returns hello SHA1 hash value for hello X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="86613-281">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-281">**Syntax:**</span></span>  
`str CertHashString(binary certificateRawData)`  
*   <span data-ttu-id="86613-282">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="86613-282">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="86613-283">matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.</span><span class="sxs-lookup"><span data-stu-id="86613-283">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuer"></a><span data-ttu-id="86613-284">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="86613-284">CertIssuer</span></span>
<span data-ttu-id="86613-285">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-285">**Description:**</span></span>  
<span data-ttu-id="86613-286">Retorna Olá nome da autoridade de certificação de saudação que emitiu o certificado x. 509v3 de saudação.</span><span class="sxs-lookup"><span data-stu-id="86613-286">Returns hello name of hello certificate authority that issued hello X.509v3 certificate.</span></span>

<span data-ttu-id="86613-287">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-287">**Syntax:**</span></span>  
`str CertIssuer(binary certificateRawData)`  
*   <span data-ttu-id="86613-288">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="86613-288">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="86613-289">matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.</span><span class="sxs-lookup"><span data-stu-id="86613-289">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuerdn"></a><span data-ttu-id="86613-290">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="86613-290">CertIssuerDN</span></span>
<span data-ttu-id="86613-291">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-291">**Description:**</span></span>  
<span data-ttu-id="86613-292">Retorna Olá nome diferenciado do emissor do certificado hello.</span><span class="sxs-lookup"><span data-stu-id="86613-292">Returns hello distinguished name of hello certificate issuer.</span></span>

<span data-ttu-id="86613-293">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-293">**Syntax:**</span></span>  
`str CertIssuerDN(binary certificateRawData)`  
*   <span data-ttu-id="86613-294">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="86613-294">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="86613-295">matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.</span><span class="sxs-lookup"><span data-stu-id="86613-295">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissueroid"></a><span data-ttu-id="86613-296">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="86613-296">CertIssuerOid</span></span>
<span data-ttu-id="86613-297">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-297">**Description:**</span></span>  
<span data-ttu-id="86613-298">Retorna Olá Oid de emissor do certificado hello.</span><span class="sxs-lookup"><span data-stu-id="86613-298">Returns hello Oid of hello certificate issuer.</span></span>

<span data-ttu-id="86613-299">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-299">**Syntax:**</span></span>  
`str CertIssuerOid(binary certificateRawData)`  
*   <span data-ttu-id="86613-300">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="86613-300">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="86613-301">matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.</span><span class="sxs-lookup"><span data-stu-id="86613-301">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithm"></a><span data-ttu-id="86613-302">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="86613-302">CertKeyAlgorithm</span></span>
<span data-ttu-id="86613-303">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-303">**Description:**</span></span>  
<span data-ttu-id="86613-304">Retorna informações de algoritmo de chave de saudação do certificado x. 509v3 como uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="86613-304">Returns hello key algorithm information for this X.509v3 certificate as a string.</span></span>

<span data-ttu-id="86613-305">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-305">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="86613-306">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="86613-306">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="86613-307">matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.</span><span class="sxs-lookup"><span data-stu-id="86613-307">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithmparams"></a><span data-ttu-id="86613-308">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="86613-308">CertKeyAlgorithmParams</span></span>
<span data-ttu-id="86613-309">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-309">**Description:**</span></span>  
<span data-ttu-id="86613-310">Retorna os parâmetros de algoritmo de chave de saudação do certificado x. 509v3 de saudação como uma cadeia de caracteres hexadecimal.</span><span class="sxs-lookup"><span data-stu-id="86613-310">Returns hello key algorithm parameters for hello X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="86613-311">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-311">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="86613-312">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="86613-312">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="86613-313">matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.</span><span class="sxs-lookup"><span data-stu-id="86613-313">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnameinfo"></a><span data-ttu-id="86613-314">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="86613-314">CertNameInfo</span></span>
<span data-ttu-id="86613-315">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-315">**Description:**</span></span>  
<span data-ttu-id="86613-316">Retorna emissor e assunto Olá nomes de um certificado.</span><span class="sxs-lookup"><span data-stu-id="86613-316">Returns hello subject and issuer names from a certificate.</span></span>

<span data-ttu-id="86613-317">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-317">**Syntax:**</span></span>  
`str CertNameInfo(binary certificateRawData, str x509NameType, bool includesIssuerName)`  
*   <span data-ttu-id="86613-318">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="86613-318">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="86613-319">matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.</span><span class="sxs-lookup"><span data-stu-id="86613-319">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
*   <span data-ttu-id="86613-320">X509NameType: Olá valor X509NameType assunto hello.</span><span class="sxs-lookup"><span data-stu-id="86613-320">X509NameType: hello X509NameType value for hello subject.</span></span>
*   <span data-ttu-id="86613-321">includesIssuerName: nome do emissor Olá tooinclude true; Caso contrário, false.</span><span class="sxs-lookup"><span data-stu-id="86613-321">includesIssuerName: true tooinclude hello issuer name; otherwise, false.</span></span>

- - -
### <a name="certnotafter"></a><span data-ttu-id="86613-322">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="86613-322">CertNotAfter</span></span>
<span data-ttu-id="86613-323">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-323">**Description:**</span></span>  
<span data-ttu-id="86613-324">Retorna a data de saudação na hora local depois que um certificado não é válido.</span><span class="sxs-lookup"><span data-stu-id="86613-324">Returns hello date in local time after which a certificate is no longer valid.</span></span>

<span data-ttu-id="86613-325">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-325">**Syntax:**</span></span>  
`dt CertNotAfter(binary certificateRawData)`  
*   <span data-ttu-id="86613-326">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="86613-326">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="86613-327">matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.</span><span class="sxs-lookup"><span data-stu-id="86613-327">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnotbefore"></a><span data-ttu-id="86613-328">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="86613-328">CertNotBefore</span></span>
<span data-ttu-id="86613-329">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-329">**Description:**</span></span>  
<span data-ttu-id="86613-330">Retorna a data de saudação na hora local no qual o certificado é validado.</span><span class="sxs-lookup"><span data-stu-id="86613-330">Returns hello date in local time on which a certificate becomes valid.</span></span>

<span data-ttu-id="86613-331">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-331">**Syntax:**</span></span>  
`dt CertNotBefore(binary certificateRawData)`  
*   <span data-ttu-id="86613-332">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="86613-332">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="86613-333">matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.</span><span class="sxs-lookup"><span data-stu-id="86613-333">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyoid"></a><span data-ttu-id="86613-334">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="86613-334">CertPublicKeyOid</span></span>
<span data-ttu-id="86613-335">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-335">**Description:**</span></span>  
<span data-ttu-id="86613-336">Retorna Olá Oid de chave pública Olá certificado x. 509v3 de saudação.</span><span class="sxs-lookup"><span data-stu-id="86613-336">Returns hello Oid of hello public key for hello X.509v3 certificate.</span></span>

<span data-ttu-id="86613-337">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-337">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="86613-338">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="86613-338">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="86613-339">matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.</span><span class="sxs-lookup"><span data-stu-id="86613-339">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyparametersoid"></a><span data-ttu-id="86613-340">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="86613-340">CertPublicKeyParametersOid</span></span>
<span data-ttu-id="86613-341">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-341">**Description:**</span></span>  
<span data-ttu-id="86613-342">Retorna Olá Oid de parâmetros de chave pública Olá para o certificado x. 509v3 de saudação.</span><span class="sxs-lookup"><span data-stu-id="86613-342">Returns hello Oid of hello public key parameters for hello X.509v3 certificate.</span></span>

<span data-ttu-id="86613-343">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-343">**Syntax:**</span></span>  
`str CertPublicKeyParametersOid(binary certificateRawData)`  
*   <span data-ttu-id="86613-344">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="86613-344">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="86613-345">matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.</span><span class="sxs-lookup"><span data-stu-id="86613-345">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certserialnumber"></a><span data-ttu-id="86613-346">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="86613-346">CertSerialNumber</span></span>
<span data-ttu-id="86613-347">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-347">**Description:**</span></span>  
<span data-ttu-id="86613-348">Retorna o número de série de saudação do certificado x. 509v3 de saudação.</span><span class="sxs-lookup"><span data-stu-id="86613-348">Returns hello serial number of hello X.509v3 certificate.</span></span>

<span data-ttu-id="86613-349">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-349">**Syntax:**</span></span>  
`str CertSerialNumber(binary certificateRawData)`  
*   <span data-ttu-id="86613-350">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="86613-350">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="86613-351">matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.</span><span class="sxs-lookup"><span data-stu-id="86613-351">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsignaturealgorithmoid"></a><span data-ttu-id="86613-352">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="86613-352">CertSignatureAlgorithmOid</span></span>
<span data-ttu-id="86613-353">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-353">**Description:**</span></span>  
<span data-ttu-id="86613-354">Olá retorna Oid do algoritmo Olá usado toocreate assinatura de saudação de um certificado.</span><span class="sxs-lookup"><span data-stu-id="86613-354">Returns hello Oid of hello algorithm used toocreate hello signature of a certificate.</span></span>

<span data-ttu-id="86613-355">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-355">**Syntax:**</span></span>  
`str CertSignatureAlgorithmOid(binary certificateRawData)`  
*   <span data-ttu-id="86613-356">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="86613-356">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="86613-357">matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.</span><span class="sxs-lookup"><span data-stu-id="86613-357">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubject"></a><span data-ttu-id="86613-358">CertSubject</span><span class="sxs-lookup"><span data-stu-id="86613-358">CertSubject</span></span>
<span data-ttu-id="86613-359">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-359">**Description:**</span></span>  
<span data-ttu-id="86613-360">Obtém Olá nome diferenciado do assunto de um certificado.</span><span class="sxs-lookup"><span data-stu-id="86613-360">Gets hello subject distinguished name from a certificate.</span></span>

<span data-ttu-id="86613-361">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-361">**Syntax:**</span></span>  
`str CertSubject(binary certificateRawData)`  
*   <span data-ttu-id="86613-362">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="86613-362">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="86613-363">matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.</span><span class="sxs-lookup"><span data-stu-id="86613-363">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnamedn"></a><span data-ttu-id="86613-364">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="86613-364">CertSubjectNameDN</span></span>
<span data-ttu-id="86613-365">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-365">**Description:**</span></span>  
<span data-ttu-id="86613-366">Retorna Olá nome diferenciado do assunto de um certificado.</span><span class="sxs-lookup"><span data-stu-id="86613-366">Returns hello subject distinguished name from a certificate.</span></span>

<span data-ttu-id="86613-367">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-367">**Syntax:**</span></span>  
`str CertSubjectNameDN(binary certificateRawData)`  
*   <span data-ttu-id="86613-368">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="86613-368">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="86613-369">matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.</span><span class="sxs-lookup"><span data-stu-id="86613-369">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnameoid"></a><span data-ttu-id="86613-370">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="86613-370">CertSubjectNameOid</span></span>
<span data-ttu-id="86613-371">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-371">**Description:**</span></span>  
<span data-ttu-id="86613-372">Retorna Olá Oid do nome da entidade de saudação de um certificado.</span><span class="sxs-lookup"><span data-stu-id="86613-372">Returns hello Oid of hello subject name from a certificate.</span></span>

<span data-ttu-id="86613-373">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-373">**Syntax:**</span></span>  
`str CertSubjectNameOid(binary certificateRawData)`  
*   <span data-ttu-id="86613-374">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="86613-374">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="86613-375">matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.</span><span class="sxs-lookup"><span data-stu-id="86613-375">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certthumbprint"></a><span data-ttu-id="86613-376">CertThumbprint</span><span class="sxs-lookup"><span data-stu-id="86613-376">CertThumbprint</span></span>
<span data-ttu-id="86613-377">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-377">**Description:**</span></span>  
<span data-ttu-id="86613-378">Retorna Olá impressão digital de um certificado.</span><span class="sxs-lookup"><span data-stu-id="86613-378">Returns hello thumbprint of a certificate.</span></span>

<span data-ttu-id="86613-379">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-379">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="86613-380">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="86613-380">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="86613-381">matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.</span><span class="sxs-lookup"><span data-stu-id="86613-381">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certversion"></a><span data-ttu-id="86613-382">CertVersion</span><span class="sxs-lookup"><span data-stu-id="86613-382">CertVersion</span></span>
<span data-ttu-id="86613-383">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-383">**Description:**</span></span>  
<span data-ttu-id="86613-384">Retorna Olá x. 509 versão de formato de um certificado.</span><span class="sxs-lookup"><span data-stu-id="86613-384">Returns hello X.509 format version of a certificate.</span></span>

<span data-ttu-id="86613-385">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-385">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="86613-386">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="86613-386">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="86613-387">matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.</span><span class="sxs-lookup"><span data-stu-id="86613-387">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="cguid"></a><span data-ttu-id="86613-388">CGuid</span><span class="sxs-lookup"><span data-stu-id="86613-388">CGuid</span></span>
<span data-ttu-id="86613-389">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-389">**Description:**</span></span>  
<span data-ttu-id="86613-390">Olá função CGuid converte a representação de cadeia de caracteres de saudação de uma representação binária do GUID tooits.</span><span class="sxs-lookup"><span data-stu-id="86613-390">hello CGuid function converts hello string representation of a GUID tooits binary representation.</span></span>

<span data-ttu-id="86613-391">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-391">**Syntax:**</span></span>  
`bin CGuid(str GUID)`

* <span data-ttu-id="86613-392">Uma cadeia de caracteres formatada nesse padrão: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx ou {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span><span class="sxs-lookup"><span data-stu-id="86613-392">A String formatted in this pattern: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

- - -
### <a name="contains"></a><span data-ttu-id="86613-393">Contém:</span><span class="sxs-lookup"><span data-stu-id="86613-393">Contains</span></span>
<span data-ttu-id="86613-394">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-394">**Description:**</span></span>  
<span data-ttu-id="86613-395">função do Hello Contains localiza uma cadeia de caracteres dentro de um atributo com vários valores</span><span class="sxs-lookup"><span data-stu-id="86613-395">hello Contains function finds a string inside a multi-valued attribute</span></span>

<span data-ttu-id="86613-396">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-396">**Syntax:**</span></span>  
<span data-ttu-id="86613-397">`num Contains (mvstring attribute, str search)` - diferencia letras maiúsculas de minúsculas</span><span class="sxs-lookup"><span data-stu-id="86613-397">`num Contains (mvstring attribute, str search)` - case-sensitive</span></span>  
`num Contains (mvstring attribute, str search, enum Casetype)`  
<span data-ttu-id="86613-398">`num Contains (mvref attribute, str search)` - diferencia letras maiúsculas de minúsculas</span><span class="sxs-lookup"><span data-stu-id="86613-398">`num Contains (mvref attribute, str search)` - case-sensitive</span></span>

* <span data-ttu-id="86613-399">atributo: Olá toosearch de atributo com vários valores.</span><span class="sxs-lookup"><span data-stu-id="86613-399">attribute: hello multi-valued attribute toosearch.</span></span>
* <span data-ttu-id="86613-400">pesquisa: toofind no atributo de saudação de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="86613-400">search: string toofind in hello attribute.</span></span>
* <span data-ttu-id="86613-401">Casetype: CaseInsensitive ou CaseSensitive.</span><span class="sxs-lookup"><span data-stu-id="86613-401">Casetype: CaseInsensitive or CaseSensitive.</span></span>

<span data-ttu-id="86613-402">Retorna o índice no atributo de múltiplos Olá onde a cadeia de caracteres de saudação foi encontrada.</span><span class="sxs-lookup"><span data-stu-id="86613-402">Returns index in hello multi-valued attribute where hello string was found.</span></span> <span data-ttu-id="86613-403">Se a cadeia de caracteres de saudação não for encontrada, será retornado 0.</span><span class="sxs-lookup"><span data-stu-id="86613-403">0 is returned if hello string is not found.</span></span>

<span data-ttu-id="86613-404">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="86613-404">**Remarks:**</span></span>  
<span data-ttu-id="86613-405">Para atributos com vários valores de cadeia de caracteres, pesquisa Olá localiza subcadeias de caracteres em valores hello.</span><span class="sxs-lookup"><span data-stu-id="86613-405">For multi-valued string attributes, hello search finds substrings in hello values.</span></span>  
<span data-ttu-id="86613-406">Para atributos de referência, hello cadeia de caracteres pesquisada deve corresponder exatamente ao Olá valor toobe considerado uma correspondência.</span><span class="sxs-lookup"><span data-stu-id="86613-406">For reference attributes, hello searched string must exactly match hello value toobe considered a match.</span></span>

<span data-ttu-id="86613-407">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-407">**Example:**</span></span>  
`IIF(Contains([proxyAddresses],"SMTP:")>0,[proxyAddresses],Error("No primary SMTP address found."))`  
<span data-ttu-id="86613-408">Se o atributo proxyAddresses de saudação tem um endereço de email primário (indicado por letras maiusculas "SMTP:"), em seguida, retornar o atributo proxyAddress de saudação, caso contrário, retornará um erro.</span><span class="sxs-lookup"><span data-stu-id="86613-408">If hello proxyAddresses attribute has a primary email address (indicated by uppercase "SMTP:"), then return hello proxyAddress attribute, else return an error.</span></span>

- - -
### <a name="convertfrombase64"></a><span data-ttu-id="86613-409">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="86613-409">ConvertFromBase64</span></span>
<span data-ttu-id="86613-410">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-410">**Description:**</span></span>  
<span data-ttu-id="86613-411">Olá ConvertFromBase64 função converte Olá especificado codificado na base64 valor tooa cadeia de caracteres regulares.</span><span class="sxs-lookup"><span data-stu-id="86613-411">hello ConvertFromBase64 function converts hello specified base64 encoded value tooa regular string.</span></span>

<span data-ttu-id="86613-412">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-412">**Syntax:**</span></span>  
<span data-ttu-id="86613-413">`str ConvertFromBase64(str source)` - adota Unicode para codificação</span><span class="sxs-lookup"><span data-stu-id="86613-413">`str ConvertFromBase64(str source)` - assumes Unicode for encoding</span></span>  
`str ConvertFromBase64(str source, enum Encoding)`

* <span data-ttu-id="86613-414">source: cadeia de caracteres codificada em Base64</span><span class="sxs-lookup"><span data-stu-id="86613-414">source: Base64 encoded string</span></span>  
* <span data-ttu-id="86613-415">Codificação: Unicode, ASCII, UTF8</span><span class="sxs-lookup"><span data-stu-id="86613-415">Encoding: Unicode, ASCII, UTF8</span></span>

<span data-ttu-id="86613-416">**Exemplo**</span><span class="sxs-lookup"><span data-stu-id="86613-416">**Example**</span></span>  
`ConvertFromBase64("SABlAGwAbABvACAAdwBvAHIAbABkACEA")`  
`ConvertFromBase64("SGVsbG8gd29ybGQh", UTF8)`

<span data-ttu-id="86613-417">Ambos os exemplos retornam "*Hello world!*"</span><span class="sxs-lookup"><span data-stu-id="86613-417">Both examples return "*Hello world!*"</span></span>

- - -
### <a name="convertfromutf8hex"></a><span data-ttu-id="86613-418">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="86613-418">ConvertFromUTF8Hex</span></span>
<span data-ttu-id="86613-419">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-419">**Description:**</span></span>  
<span data-ttu-id="86613-420">Olá ConvertFromUTF8Hex função converte Olá especificado a cadeia de caracteres hexadecimal UTF8 codificado valor tooa.</span><span class="sxs-lookup"><span data-stu-id="86613-420">hello ConvertFromUTF8Hex function converts hello specified UTF8 Hex encoded value tooa string.</span></span>

<span data-ttu-id="86613-421">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-421">**Syntax:**</span></span>  
`str ConvertFromUTF8Hex(str source)`

* <span data-ttu-id="86613-422">source: cadeia de caracteres codificada em UTF8 de 2 bytes</span><span class="sxs-lookup"><span data-stu-id="86613-422">source: UTF8 2-byte encoded sting</span></span>

<span data-ttu-id="86613-423">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="86613-423">**Remarks:**</span></span>  
<span data-ttu-id="86613-424">Olá diferença entre esta função e ConvertFromBase64([],UTF8) que resultam de saudação é amigável para o atributo DN de saudação.</span><span class="sxs-lookup"><span data-stu-id="86613-424">hello difference between this function and ConvertFromBase64([],UTF8) in that hello result is friendly for hello DN attribute.</span></span>  
<span data-ttu-id="86613-425">Esse formato é usado pelo Active Directory do Azure como DN.</span><span class="sxs-lookup"><span data-stu-id="86613-425">This format is used by Azure Active Directory as DN.</span></span>

<span data-ttu-id="86613-426">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-426">**Example:**</span></span>  
`ConvertFromUTF8Hex("48656C6C6F20776F726C6421")`  
<span data-ttu-id="86613-427">retorna "*Hello world!*"</span><span class="sxs-lookup"><span data-stu-id="86613-427">Returns "*Hello world!*"</span></span>

- - -
### <a name="converttobase64"></a><span data-ttu-id="86613-428">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="86613-428">ConvertToBase64</span></span>
<span data-ttu-id="86613-429">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-429">**Description:**</span></span>  
<span data-ttu-id="86613-430">Olá função ConvertToBase64 converte uma cadeia de caracteres de base64 Unicode de tooa de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="86613-430">hello ConvertToBase64 function converts a string tooa Unicode base64 string.</span></span>  
<span data-ttu-id="86613-431">Converte o valor de saudação de uma matriz de representação de cadeia de caracteres equivalente de tooits inteiros que é codificada com dígitos de base 64.</span><span class="sxs-lookup"><span data-stu-id="86613-431">Converts hello value of an array of integers tooits equivalent string representation that is encoded with base-64 digits.</span></span>

<span data-ttu-id="86613-432">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-432">**Syntax:**</span></span>  
`str ConvertToBase64(str source)`

<span data-ttu-id="86613-433">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-433">**Example:**</span></span>  
`ConvertToBase64("Hello world!")`  
<span data-ttu-id="86613-434">retorna "SABlAGwAbABvACAAdwBvAHIAbABkACEA"</span><span class="sxs-lookup"><span data-stu-id="86613-434">Returns "SABlAGwAbABvACAAdwBvAHIAbABkACEA"</span></span>

- - -
### <a name="converttoutf8hex"></a><span data-ttu-id="86613-435">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="86613-435">ConvertToUTF8Hex</span></span>
<span data-ttu-id="86613-436">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-436">**Description:**</span></span>  
<span data-ttu-id="86613-437">Olá função ConvertToUTF8Hex converte uma cadeia de caracteres de tooa valor hexadecimal UTF8 codificado.</span><span class="sxs-lookup"><span data-stu-id="86613-437">hello ConvertToUTF8Hex function converts a string tooa UTF8 Hex encoded value.</span></span>

<span data-ttu-id="86613-438">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-438">**Syntax:**</span></span>  
`str ConvertToUTF8Hex(str source)`

<span data-ttu-id="86613-439">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="86613-439">**Remarks:**</span></span>  
<span data-ttu-id="86613-440">saudação de formato de saída dessa função é usado pelo Active Directory do Azure como o formato do atributo DN.</span><span class="sxs-lookup"><span data-stu-id="86613-440">hello output format of this function is used by Azure Active Directory as DN attribute format.</span></span>

<span data-ttu-id="86613-441">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-441">**Example:**</span></span>  
`ConvertToUTF8Hex("Hello world!")`  
<span data-ttu-id="86613-442">retorna 48656C6C6F20776F726C6421</span><span class="sxs-lookup"><span data-stu-id="86613-442">Returns 48656C6C6F20776F726C6421</span></span>

- - -
### <a name="count"></a><span data-ttu-id="86613-443">Contagem</span><span class="sxs-lookup"><span data-stu-id="86613-443">Count</span></span>
<span data-ttu-id="86613-444">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-444">**Description:**</span></span>  
<span data-ttu-id="86613-445">Olá função Count retorna o número de saudação de elementos em um atributo com valores múltiplos</span><span class="sxs-lookup"><span data-stu-id="86613-445">hello Count function returns hello number of elements in a multi-valued attribute</span></span>

<span data-ttu-id="86613-446">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-446">**Syntax:**</span></span>  
`num Count(mvstr attribute)`

- - -
### <a name="cnum"></a><span data-ttu-id="86613-447">CNum</span><span class="sxs-lookup"><span data-stu-id="86613-447">CNum</span></span>
<span data-ttu-id="86613-448">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-448">**Description:**</span></span>  
<span data-ttu-id="86613-449">Olá função CNum usa uma cadeia de caracteres e retorna um tipo de dados numérico.</span><span class="sxs-lookup"><span data-stu-id="86613-449">hello CNum function takes a string and returns a numeric data type.</span></span>

<span data-ttu-id="86613-450">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-450">**Syntax:**</span></span>  
`num CNum(str value)`

- - -
### <a name="cref"></a><span data-ttu-id="86613-451">CRef</span><span class="sxs-lookup"><span data-stu-id="86613-451">CRef</span></span>
<span data-ttu-id="86613-452">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-452">**Description:**</span></span>  
<span data-ttu-id="86613-453">Converte um atributo de cadeia de caracteres de referência tooa</span><span class="sxs-lookup"><span data-stu-id="86613-453">Converts a string tooa reference attribute</span></span>

<span data-ttu-id="86613-454">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-454">**Syntax:**</span></span>  
`ref CRef(str value)`

<span data-ttu-id="86613-455">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-455">**Example:**</span></span>  
`CRef("CN=LC Services,CN=Microsoft,CN=lcspool01,CN=Pools,CN=RTC Service," & %Forest.LDAP%)`

- - -
### <a name="cstr"></a><span data-ttu-id="86613-456">CStr</span><span class="sxs-lookup"><span data-stu-id="86613-456">CStr</span></span>
<span data-ttu-id="86613-457">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-457">**Description:**</span></span>  
<span data-ttu-id="86613-458">Olá função CStr converte o tipo de dados de cadeia de caracteres tooa.</span><span class="sxs-lookup"><span data-stu-id="86613-458">hello CStr function converts tooa string data type.</span></span>

<span data-ttu-id="86613-459">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-459">**Syntax:**</span></span>  
`str CStr(num value)`  
`str CStr(ref value)`  
`str CStr(bool value)`  

* <span data-ttu-id="86613-460">valor: pode ser um valor numérico, o atributo de referência ou booliano.</span><span class="sxs-lookup"><span data-stu-id="86613-460">value: Can be a numeric value, reference attribute, or Boolean.</span></span>

<span data-ttu-id="86613-461">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-461">**Example:**</span></span>  
`CStr([dn])`  
<span data-ttu-id="86613-462">poderia retornar "cn=Joe,dc=contoso,dc=com"</span><span class="sxs-lookup"><span data-stu-id="86613-462">Could return "cn=Joe,dc=contoso,dc=com"</span></span>

- - -
### <a name="dateadd"></a><span data-ttu-id="86613-463">DateAdd</span><span class="sxs-lookup"><span data-stu-id="86613-463">DateAdd</span></span>
<span data-ttu-id="86613-464">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-464">**Description:**</span></span>  
<span data-ttu-id="86613-465">Retorna uma data que contém um toowhich data que um intervalo de tempo especificado foi adicionado.</span><span class="sxs-lookup"><span data-stu-id="86613-465">Returns a Date containing a date toowhich a specified time interval has been added.</span></span>

<span data-ttu-id="86613-466">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-466">**Syntax:**</span></span>  
`dt DateAdd(str interval, num value, dt date)`

* <span data-ttu-id="86613-467">intervalo: expressão que é o intervalo de tempo que deseja tooadd de saudação de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="86613-467">interval: String expression that is hello interval of time you want tooadd.</span></span> <span data-ttu-id="86613-468">cadeia de caracteres de saudação deve ter uma saudação valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="86613-468">hello string must have one of hello following values:</span></span>
  * <span data-ttu-id="86613-469">aaaa Ano</span><span class="sxs-lookup"><span data-stu-id="86613-469">yyyy Year</span></span>
  * <span data-ttu-id="86613-470">q - Trimestre</span><span class="sxs-lookup"><span data-stu-id="86613-470">q Quarter</span></span>
  * <span data-ttu-id="86613-471">m - Mês</span><span class="sxs-lookup"><span data-stu-id="86613-471">m Month</span></span>
  * <span data-ttu-id="86613-472">y - Dia do ano</span><span class="sxs-lookup"><span data-stu-id="86613-472">y Day of year</span></span>
  * <span data-ttu-id="86613-473">d - Dia</span><span class="sxs-lookup"><span data-stu-id="86613-473">d Day</span></span>
  * <span data-ttu-id="86613-474">w - Dia da semana</span><span class="sxs-lookup"><span data-stu-id="86613-474">w Weekday</span></span>
  * <span data-ttu-id="86613-475">ww - Semana</span><span class="sxs-lookup"><span data-stu-id="86613-475">ww Week</span></span>
  * <span data-ttu-id="86613-476">h - Hora</span><span class="sxs-lookup"><span data-stu-id="86613-476">h Hour</span></span>
  * <span data-ttu-id="86613-477">m - Minuto</span><span class="sxs-lookup"><span data-stu-id="86613-477">n Minute</span></span>
  * <span data-ttu-id="86613-478">s - Segundo</span><span class="sxs-lookup"><span data-stu-id="86613-478">s Second</span></span>
* <span data-ttu-id="86613-479">valor: Olá o número de unidades que você deseja tooadd.</span><span class="sxs-lookup"><span data-stu-id="86613-479">value: hello number of units you want tooadd.</span></span> <span data-ttu-id="86613-480">Pode ser positivo (tooget datas em Olá futuro) ou negativo (tooget datas em Olá anterior).</span><span class="sxs-lookup"><span data-stu-id="86613-480">It can be positive (tooget dates in hello future) or negative (tooget dates in hello past).</span></span>
* <span data-ttu-id="86613-481">Data: DateTime representando data toowhich Olá intervalo é adicionado.</span><span class="sxs-lookup"><span data-stu-id="86613-481">date: DateTime representing date toowhich hello interval is added.</span></span>

<span data-ttu-id="86613-482">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-482">**Example:**</span></span>  
`DateAdd("m", 3, CDate("2001-01-01"))`  
<span data-ttu-id="86613-483">adiciona três meses e retorna um DateTime que representa "01/04/2001".</span><span class="sxs-lookup"><span data-stu-id="86613-483">Adds 3 months and returns a DateTime representing "2001-04-01".</span></span>

- - -
### <a name="datefromnum"></a><span data-ttu-id="86613-484">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="86613-484">DateFromNum</span></span>
<span data-ttu-id="86613-485">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-485">**Description:**</span></span>  
<span data-ttu-id="86613-486">Olá função DateFromNum converte um valor em tooa de formato de data do AD tipo DateTime.</span><span class="sxs-lookup"><span data-stu-id="86613-486">hello DateFromNum function converts a value in AD’s date format tooa DateTime type.</span></span>

<span data-ttu-id="86613-487">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-487">**Syntax:**</span></span>  
`dt DateFromNum(num value)`

<span data-ttu-id="86613-488">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-488">**Example:**</span></span>  
`DateFromNum([lastLogonTimestamp])`  
`DateFromNum(129699324000000000)`  
<span data-ttu-id="86613-489">retorna um DateTime que representa 01/01/2012 23:00:00</span><span class="sxs-lookup"><span data-stu-id="86613-489">Returns a DateTime representing 2012-01-01 23:00:00</span></span>

- - -
### <a name="dncomponent"></a><span data-ttu-id="86613-490">DNComponent</span><span class="sxs-lookup"><span data-stu-id="86613-490">DNComponent</span></span>
<span data-ttu-id="86613-491">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-491">**Description:**</span></span>  
<span data-ttu-id="86613-492">Olá função DNComponent retorna o valor de saudação de um componente DN especificado vindo da esquerda.</span><span class="sxs-lookup"><span data-stu-id="86613-492">hello DNComponent function returns hello value of a specified DN component going from left.</span></span>

<span data-ttu-id="86613-493">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-493">**Syntax:**</span></span>  
`str DNComponent(ref dn, num ComponentNumber)`

* <span data-ttu-id="86613-494">DN: Olá toointerpret de atributo de referência</span><span class="sxs-lookup"><span data-stu-id="86613-494">dn: hello reference attribute toointerpret</span></span>
* <span data-ttu-id="86613-495">ComponentNumber: componente Olá Olá DN tooreturn</span><span class="sxs-lookup"><span data-stu-id="86613-495">ComponentNumber: hello component in hello DN tooreturn</span></span>

<span data-ttu-id="86613-496">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-496">**Example:**</span></span>  
`DNComponent([dn],1)`  
<span data-ttu-id="86613-497">se dn é “cn=Joe,ou=…,” ele retorna Joe</span><span class="sxs-lookup"><span data-stu-id="86613-497">If dn is "cn=Joe,ou=…," it returns Joe</span></span>

- - -
### <a name="dncomponentrev"></a><span data-ttu-id="86613-498">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="86613-498">DNComponentRev</span></span>
<span data-ttu-id="86613-499">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-499">**Description:**</span></span>  
<span data-ttu-id="86613-500">Olá função DNComponentRev retorna o valor de saudação de um componente DN especificado vindo da direita (fim Olá).</span><span class="sxs-lookup"><span data-stu-id="86613-500">hello DNComponentRev function returns hello value of a specified DN component going from right (hello end).</span></span>

<span data-ttu-id="86613-501">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-501">**Syntax:**</span></span>  
`str DNComponentRev(ref dn, num ComponentNumber)`  
`str DNComponentRev(ref dn, num ComponentNumber, enum Options)`

* <span data-ttu-id="86613-502">DN: Olá toointerpret de atributo de referência</span><span class="sxs-lookup"><span data-stu-id="86613-502">dn: hello reference attribute toointerpret</span></span>
* <span data-ttu-id="86613-503">ComponentNumber - componente Olá Olá DN tooreturn</span><span class="sxs-lookup"><span data-stu-id="86613-503">ComponentNumber - hello component in hello DN tooreturn</span></span>
* <span data-ttu-id="86613-504">Opções: DC – ignorar todos os componentes com “dc=”</span><span class="sxs-lookup"><span data-stu-id="86613-504">Options: DC – Ignore all components with "dc="</span></span>

<span data-ttu-id="86613-505">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-505">**Example:**</span></span>  
<span data-ttu-id="86613-506">Se dn for "cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com" então</span><span class="sxs-lookup"><span data-stu-id="86613-506">If dn is "cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com" then</span></span>  
`DNComponentRev([dn],3)`  
`DNComponentRev([dn],1,"DC")`  
<span data-ttu-id="86613-507">ambos retornam US.</span><span class="sxs-lookup"><span data-stu-id="86613-507">Both return US.</span></span>

- - -
### <a name="error"></a><span data-ttu-id="86613-508">Erro</span><span class="sxs-lookup"><span data-stu-id="86613-508">Error</span></span>
<span data-ttu-id="86613-509">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-509">**Description:**</span></span>  
<span data-ttu-id="86613-510">Olá função Error é usada tooreturn um erro personalizado.</span><span class="sxs-lookup"><span data-stu-id="86613-510">hello Error function is used tooreturn a custom error.</span></span>

<span data-ttu-id="86613-511">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-511">**Syntax:**</span></span>  
`void Error(str ErrorMessage)`

<span data-ttu-id="86613-512">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-512">**Example:**</span></span>  
`IIF(IsPresent([accountName]),[accountName],Error("AccountName is required"))`  
<span data-ttu-id="86613-513">Se Olá atributo accountName não estiver presente, gera um erro no objeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="86613-513">If hello attribute accountName is not present, throw an error on hello object.</span></span>

- - -
### <a name="escapedncomponent"></a><span data-ttu-id="86613-514">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="86613-514">EscapeDNComponent</span></span>
<span data-ttu-id="86613-515">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-515">**Description:**</span></span>  
<span data-ttu-id="86613-516">Olá função EscapeDNComponent usa um componente de um DN e foge de forma que ele pode ser representado no LDAP.</span><span class="sxs-lookup"><span data-stu-id="86613-516">hello EscapeDNComponent function takes one component of a DN and escapes it so it can be represented in LDAP.</span></span>

<span data-ttu-id="86613-517">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-517">**Syntax:**</span></span>  
`str EscapeDNComponent(str value)`

<span data-ttu-id="86613-518">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-518">**Example:**</span></span>  
`EscapeDNComponent("cn=" & [displayName]) & "," & %ForestLDAP%)`  
<span data-ttu-id="86613-519">Verifica se o objeto de saudação pode ser criado em um diretório LDAP, mesmo se o atributo de displayName Olá tem caracteres que devem ser substituídos no LDAP.</span><span class="sxs-lookup"><span data-stu-id="86613-519">Makes sure hello object can be created in an LDAP directory even if hello displayName attribute has characters that must be escaped in LDAP.</span></span>

- - -
### <a name="formatdatetime"></a><span data-ttu-id="86613-520">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="86613-520">FormatDateTime</span></span>
<span data-ttu-id="86613-521">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-521">**Description:**</span></span>  
<span data-ttu-id="86613-522">função FormatDateTime de saudação é usado tooformat uma cadeia de caracteres de tooa DateTime com um formato especificado</span><span class="sxs-lookup"><span data-stu-id="86613-522">hello FormatDateTime function is used tooformat a DateTime tooa string with a specified format</span></span>

<span data-ttu-id="86613-523">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-523">**Syntax:**</span></span>  
`str FormatDateTime(dt value, str format)`

* <span data-ttu-id="86613-524">valor: um valor no formato de data e hora Olá</span><span class="sxs-lookup"><span data-stu-id="86613-524">value: a value in hello DateTime format</span></span>
* <span data-ttu-id="86613-525">formato: uma cadeia de caracteres que representa a saudação formato tooconvert para.</span><span class="sxs-lookup"><span data-stu-id="86613-525">format: a string representing hello format tooconvert to.</span></span>

<span data-ttu-id="86613-526">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="86613-526">**Remarks:**</span></span>  
<span data-ttu-id="86613-527">Olá os valores possíveis para o formato de saudação pode ser encontrado aqui: [definida pelo usuário (função Format) de formatos de data/hora](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span><span class="sxs-lookup"><span data-stu-id="86613-527">hello possible values for hello format can be found here: [User-Defined Date/Time Formats (Format Function)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span></span>

<span data-ttu-id="86613-528">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-528">**Example:**</span></span>  

`FormatDateTime(CDate("12/25/2007"),"yyyy-mm-dd")`  
<span data-ttu-id="86613-529">resulta em "25/12/2007".</span><span class="sxs-lookup"><span data-stu-id="86613-529">Results in "2007-12-25".</span></span>

`FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")`  
<span data-ttu-id="86613-530">pode resultar em "20140905081453.0Z"</span><span class="sxs-lookup"><span data-stu-id="86613-530">Can result in "20140905081453.0Z"</span></span>

- - -
### <a name="guid"></a><span data-ttu-id="86613-531">GUID</span><span class="sxs-lookup"><span data-stu-id="86613-531">GUID</span></span>
<span data-ttu-id="86613-532">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-532">**Description:**</span></span>  
<span data-ttu-id="86613-533">GUID da função Hello gera um novo GUID aleatório</span><span class="sxs-lookup"><span data-stu-id="86613-533">hello function GUID generates a new random GUID</span></span>

<span data-ttu-id="86613-534">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-534">**Syntax:**</span></span>  
`str GUID()`

- - -
### <a name="iif"></a><span data-ttu-id="86613-535">IIF</span><span class="sxs-lookup"><span data-stu-id="86613-535">IIF</span></span>
<span data-ttu-id="86613-536">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-536">**Description:**</span></span>  
<span data-ttu-id="86613-537">Olá função IIF retorna um de um conjunto de valores possíveis com base em uma condição especificada.</span><span class="sxs-lookup"><span data-stu-id="86613-537">hello IIF function returns one of a set of possible values based on a specified condition.</span></span>

<span data-ttu-id="86613-538">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-538">**Syntax:**</span></span>  
`var IIF(exp condition, var valueIfTrue, var valueIfFalse)`

* <span data-ttu-id="86613-539">condição: qualquer valor ou expressão que pode ser avaliada tootrue ou false.</span><span class="sxs-lookup"><span data-stu-id="86613-539">condition: any value or expression that can be evaluated tootrue or false.</span></span>
* <span data-ttu-id="86613-540">ValorSeVerdadeiro: se a condição de saudação avalia tootrue, Olá retornou o valor.</span><span class="sxs-lookup"><span data-stu-id="86613-540">valueIfTrue: If hello condition evaluates tootrue, hello returned value.</span></span>
* <span data-ttu-id="86613-541">ValorSeFalso: se a condição de saudação avalia toofalse, Olá retornou o valor.</span><span class="sxs-lookup"><span data-stu-id="86613-541">valueIfFalse: If hello condition evaluates toofalse, hello returned value.</span></span>

<span data-ttu-id="86613-542">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-542">**Example:**</span></span>  
`IIF([employeeType]="Intern","t-" & [alias],[alias])`  
 <span data-ttu-id="86613-543">Se o usuário Olá for um estagiário, retorna Olá alias de um usuário com"t" adicionado toohello a partir dele, else retorna o alias do usuário hello como é.</span><span class="sxs-lookup"><span data-stu-id="86613-543">If hello user is an intern, returns hello alias of a user with "t-" added toohello beginning of it, else returns hello user’s alias as is.</span></span>

- - -
### <a name="instr"></a><span data-ttu-id="86613-544">InStr</span><span class="sxs-lookup"><span data-stu-id="86613-544">InStr</span></span>
<span data-ttu-id="86613-545">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-545">**Description:**</span></span>  
<span data-ttu-id="86613-546">Olá função InStr localiza a primeira ocorrência de saudação de uma subcadeia de caracteres em uma cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="86613-546">hello InStr function finds hello first occurrence of a substring in a string</span></span>

<span data-ttu-id="86613-547">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-547">**Syntax:**</span></span>  

`num InStr(str stringcheck, str stringmatch)`  
`num InStr(str stringcheck, str stringmatch, num start)`  
`num InStr(str stringcheck, str stringmatch, num start , enum compare)`

* <span data-ttu-id="86613-548">stringcheck: toobe pesquisado de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="86613-548">stringcheck: string toobe searched</span></span>
* <span data-ttu-id="86613-549">stringmatch: cadeia de caracteres toobe encontrado</span><span class="sxs-lookup"><span data-stu-id="86613-549">stringmatch: string toobe found</span></span>
* <span data-ttu-id="86613-550">Iniciar: Iniciando posição toofind Olá substring</span><span class="sxs-lookup"><span data-stu-id="86613-550">start: starting position toofind hello substring</span></span>
* <span data-ttu-id="86613-551">compare: vbTextCompare ou vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="86613-551">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="86613-552">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="86613-552">**Remarks:**</span></span>  
<span data-ttu-id="86613-553">Posição de saudação retorna onde a subcadeia de caracteres hello foi encontrada ou 0 se não encontrado.</span><span class="sxs-lookup"><span data-stu-id="86613-553">Returns hello position where hello substring was found or 0 if not found.</span></span>

<span data-ttu-id="86613-554">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-554">**Example:**</span></span>  
`InStr("hello quick brown fox","quick")`  
<span data-ttu-id="86613-555">/ / Avalia too5</span><span class="sxs-lookup"><span data-stu-id="86613-555">Evalues too5</span></span>

`InStr("repEated","e",3,vbBinaryCompare)`  
<span data-ttu-id="86613-556">Avalia too7</span><span class="sxs-lookup"><span data-stu-id="86613-556">Evaluates too7</span></span>

- - -
### <a name="instrrev"></a><span data-ttu-id="86613-557">InStrRev</span><span class="sxs-lookup"><span data-stu-id="86613-557">InStrRev</span></span>
<span data-ttu-id="86613-558">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-558">**Description:**</span></span>  
<span data-ttu-id="86613-559">Olá função InStrRev localiza a última ocorrência de saudação de uma subcadeia de caracteres em uma cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="86613-559">hello InStrRev function finds hello last occurrence of a substring in a string</span></span>

<span data-ttu-id="86613-560">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-560">**Syntax:**</span></span>  
`num InstrRev(str stringcheck, str stringmatch)`  
`num InstrRev(str stringcheck, str stringmatch, num start)`  
`num InstrRev(str stringcheck, str stringmatch, num start, enum compare)`

* <span data-ttu-id="86613-561">stringcheck: toobe pesquisado de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="86613-561">stringcheck: string toobe searched</span></span>
* <span data-ttu-id="86613-562">stringmatch: cadeia de caracteres toobe encontrado</span><span class="sxs-lookup"><span data-stu-id="86613-562">stringmatch: string toobe found</span></span>
* <span data-ttu-id="86613-563">Iniciar: Iniciando posição toofind Olá substring</span><span class="sxs-lookup"><span data-stu-id="86613-563">start: starting position toofind hello substring</span></span>
* <span data-ttu-id="86613-564">compare: vbTextCompare ou vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="86613-564">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="86613-565">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="86613-565">**Remarks:**</span></span>  
<span data-ttu-id="86613-566">Posição de saudação retorna onde a subcadeia de caracteres hello foi encontrada ou 0 se não encontrado.</span><span class="sxs-lookup"><span data-stu-id="86613-566">Returns hello position where hello substring was found or 0 if not found.</span></span>

<span data-ttu-id="86613-567">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-567">**Example:**</span></span>  
`InStrRev("abbcdbbbef","bb")`  
<span data-ttu-id="86613-568">retorna 7</span><span class="sxs-lookup"><span data-stu-id="86613-568">Returns 7</span></span>

- - -
### <a name="isbitset"></a><span data-ttu-id="86613-569">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="86613-569">IsBitSet</span></span>
<span data-ttu-id="86613-570">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-570">**Description:**</span></span>  
<span data-ttu-id="86613-571">função Hello IsBitSet testa se um bit é definida ou não</span><span class="sxs-lookup"><span data-stu-id="86613-571">hello function IsBitSet Tests if a bit is set or not</span></span>

<span data-ttu-id="86613-572">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-572">**Syntax:**</span></span>  
`bool IsBitSet(num value, num flag)`

* <span data-ttu-id="86613-573">valor: um valor numérico que é evaluated. Flag: um valor numérico que tem Olá bit toobe avaliada</span><span class="sxs-lookup"><span data-stu-id="86613-573">value: a numeric value that is evaluated.flag: a numeric value that has hello bit toobe evaluated</span></span>

<span data-ttu-id="86613-574">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-574">**Example:**</span></span>  
`IsBitSet(&HF,4)`  
<span data-ttu-id="86613-575">Retorna True porque o bit "4" está definido no valor hexadecimal da saudação "F"</span><span class="sxs-lookup"><span data-stu-id="86613-575">Returns True because bit "4" is set in hello hexadecimal value "F"</span></span>

- - -
### <a name="isdate"></a><span data-ttu-id="86613-576">IsDate</span><span class="sxs-lookup"><span data-stu-id="86613-576">IsDate</span></span>
<span data-ttu-id="86613-577">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-577">**Description:**</span></span>  
<span data-ttu-id="86613-578">Se Olá expressão pode ser é avaliada como um tipo DateTime, Olá função IsDate avalia tooTrue.</span><span class="sxs-lookup"><span data-stu-id="86613-578">If hello expression can be evaluates as a DateTime type, then hello IsDate function evaluates tooTrue.</span></span>

<span data-ttu-id="86613-579">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-579">**Syntax:**</span></span>  
`bool IsDate(var Expression)`

<span data-ttu-id="86613-580">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="86613-580">**Remarks:**</span></span>  
<span data-ttu-id="86613-581">Usado toodetermine se CDate () pode ser bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="86613-581">Used toodetermine if CDate() can be successful.</span></span>

- - -
### <a name="iscert"></a><span data-ttu-id="86613-582">IsCert</span><span class="sxs-lookup"><span data-stu-id="86613-582">IsCert</span></span>
<span data-ttu-id="86613-583">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-583">**Description:**</span></span>  
<span data-ttu-id="86613-584">Retorna true se os dados brutos Olá podem ser serializados para o objeto de certificado X509Certificate2 .NET.</span><span class="sxs-lookup"><span data-stu-id="86613-584">Returns true if hello raw data can be serialized into .NET X509Certificate2 certificate object.</span></span>

<span data-ttu-id="86613-585">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-585">**Syntax:**</span></span>  
`bool CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="86613-586">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="86613-586">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="86613-587">matriz de bytes de saudação pode ser codificada binária (DER) ou dados x. 509 codificado na Base64.</span><span class="sxs-lookup"><span data-stu-id="86613-587">hello byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
- - -
### <a name="isempty"></a><span data-ttu-id="86613-588">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="86613-588">IsEmpty</span></span>
<span data-ttu-id="86613-589">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-589">**Description:**</span></span>  
<span data-ttu-id="86613-590">Se o atributo hello está presente no hello CS ou MV mas é avaliada tooan cadeia de caracteres vazia, função do hello IsEmpty avalia tooTrue.</span><span class="sxs-lookup"><span data-stu-id="86613-590">If hello attribute is present in hello CS or MV but evaluates tooan empty string, then hello IsEmpty function evaluates tooTrue.</span></span>

<span data-ttu-id="86613-591">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-591">**Syntax:**</span></span>  
`bool IsEmpty(var Expression)`

- - -
### <a name="isguid"></a><span data-ttu-id="86613-592">IsGuid</span><span class="sxs-lookup"><span data-stu-id="86613-592">IsGuid</span></span>
<span data-ttu-id="86613-593">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-593">**Description:**</span></span>  
<span data-ttu-id="86613-594">Se a cadeia de caracteres hello pode ser convertido tooa GUID, função de isguid avalia Olá avaliada tootrue.</span><span class="sxs-lookup"><span data-stu-id="86613-594">If hello string could be converted tooa GUID, then hello IsGuid function evaluated tootrue.</span></span>

<span data-ttu-id="86613-595">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-595">**Syntax:**</span></span>  
`bool IsGuid(str GUID)`

<span data-ttu-id="86613-596">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="86613-596">**Remarks:**</span></span>  
<span data-ttu-id="86613-597">um GUID é definido como uma cadeia de caracteres seguindo um destes padrões: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx ou {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span><span class="sxs-lookup"><span data-stu-id="86613-597">A GUID is defined as a string following one of these patterns: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

<span data-ttu-id="86613-598">Usado toodetermine se cguid () pode ser bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="86613-598">Used toodetermine if CGuid() can be successful.</span></span>

<span data-ttu-id="86613-599">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-599">**Example:**</span></span>  
`IIF(IsGuid([strAttribute]),CGuid([strAttribute]),NULL)`  
<span data-ttu-id="86613-600">Se Olá StrAttribute tem um formato GUID, retorna uma representação binária, caso contrário, retornará um valor nulo.</span><span class="sxs-lookup"><span data-stu-id="86613-600">If hello StrAttribute has a GUID format, return a binary representation, otherwise return a Null.</span></span>

- - -
### <a name="isnull"></a><span data-ttu-id="86613-601">IsNull</span><span class="sxs-lookup"><span data-stu-id="86613-601">IsNull</span></span>
<span data-ttu-id="86613-602">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-602">**Description:**</span></span>  
<span data-ttu-id="86613-603">Se a expressão Olá avalia tooNull, a função IsNull de saudação retorna true.</span><span class="sxs-lookup"><span data-stu-id="86613-603">If hello expression evaluates tooNull, then hello IsNull function returns true.</span></span>

<span data-ttu-id="86613-604">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-604">**Syntax:**</span></span>  
`bool IsNull(var Expression)`

<span data-ttu-id="86613-605">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="86613-605">**Remarks:**</span></span>  
<span data-ttu-id="86613-606">Para um atributo, um valor nulo é expressa pela ausência de saudação do atributo hello.</span><span class="sxs-lookup"><span data-stu-id="86613-606">For an attribute, a Null is expressed by hello absence of hello attribute.</span></span>

<span data-ttu-id="86613-607">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-607">**Example:**</span></span>  
`IsNull([displayName])`  
<span data-ttu-id="86613-608">Retornará True se o atributo de saudação não está presente no hello CS ou MV.</span><span class="sxs-lookup"><span data-stu-id="86613-608">Returns True if hello attribute is not present in hello CS or MV.</span></span>

- - -
### <a name="isnullorempty"></a><span data-ttu-id="86613-609">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="86613-609">IsNullOrEmpty</span></span>
<span data-ttu-id="86613-610">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-610">**Description:**</span></span>  
<span data-ttu-id="86613-611">Se a expressão de saudação é nulo ou uma cadeia de caracteres vazia, a função IsNullOrEmpty de saudação retorna true.</span><span class="sxs-lookup"><span data-stu-id="86613-611">If hello expression is null or an empty string, then hello IsNullOrEmpty function returns true.</span></span>

<span data-ttu-id="86613-612">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-612">**Syntax:**</span></span>  
`bool IsNullOrEmpty(var Expression)`

<span data-ttu-id="86613-613">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="86613-613">**Remarks:**</span></span>  
<span data-ttu-id="86613-614">Para um atributo, isso seria avaliado tooTrue se Olá atributo está ausente ou está presente, mas uma cadeia de caracteres vazia.</span><span class="sxs-lookup"><span data-stu-id="86613-614">For an attribute, this would evaluate tooTrue if hello attribute is absent or is present but is an empty string.</span></span>  
<span data-ttu-id="86613-615">Olá inverso dessa função é chamado IsPresent.</span><span class="sxs-lookup"><span data-stu-id="86613-615">hello inverse of this function is named IsPresent.</span></span>

<span data-ttu-id="86613-616">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-616">**Example:**</span></span>  
`IsNullOrEmpty([displayName])`  
<span data-ttu-id="86613-617">Retornará True se o atributo de saudação não está presente ou é uma cadeia de caracteres vazia Olá CS ou MV.</span><span class="sxs-lookup"><span data-stu-id="86613-617">Returns True if hello attribute is not present or is an empty string in hello CS or MV.</span></span>

- - -
### <a name="isnumeric"></a><span data-ttu-id="86613-618">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="86613-618">IsNumeric</span></span>
<span data-ttu-id="86613-619">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-619">**Description:**</span></span>  
<span data-ttu-id="86613-620">Olá função IsNumeric retorna um valor booliano que indica se uma expressão pode ser avaliada como um tipo numérico.</span><span class="sxs-lookup"><span data-stu-id="86613-620">hello IsNumeric function returns a Boolean value indicating whether an expression can be evaluated as a number type.</span></span>

<span data-ttu-id="86613-621">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-621">**Syntax:**</span></span>  
`bool IsNumeric(var Expression)`

<span data-ttu-id="86613-622">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="86613-622">**Remarks:**</span></span>  
<span data-ttu-id="86613-623">Usado toodetermine se cnum () pode ser uma expressão de saudação tooparse com êxito.</span><span class="sxs-lookup"><span data-stu-id="86613-623">Used toodetermine if CNum() can be successful tooparse hello expression.</span></span>

- - -
### <a name="isstring"></a><span data-ttu-id="86613-624">IsString</span><span class="sxs-lookup"><span data-stu-id="86613-624">IsString</span></span>
<span data-ttu-id="86613-625">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-625">**Description:**</span></span>  
<span data-ttu-id="86613-626">Se a expressão Olá pode ser avaliada tooa tipo string, função IsString de saudação avalia tooTrue.</span><span class="sxs-lookup"><span data-stu-id="86613-626">If hello expression can be evaluated tooa string type, then hello IsString function evaluates tooTrue.</span></span>

<span data-ttu-id="86613-627">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-627">**Syntax:**</span></span>  
`bool IsString(var expression)`

<span data-ttu-id="86613-628">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="86613-628">**Remarks:**</span></span>  
<span data-ttu-id="86613-629">Usado toodetermine se CStr () pode ser uma expressão de saudação tooparse com êxito.</span><span class="sxs-lookup"><span data-stu-id="86613-629">Used toodetermine if CStr() can be successful tooparse hello expression.</span></span>

- - -
### <a name="ispresent"></a><span data-ttu-id="86613-630">IsPresent</span><span class="sxs-lookup"><span data-stu-id="86613-630">IsPresent</span></span>
<span data-ttu-id="86613-631">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-631">**Description:**</span></span>  
<span data-ttu-id="86613-632">Se Olá avalia tooa de cadeia de caracteres que não seja nulo e não está vazio, em seguida, Olá IsPresent função retorna true.</span><span class="sxs-lookup"><span data-stu-id="86613-632">If hello expression evaluates tooa string that is not Null and is not empty, then hello IsPresent function returns true.</span></span>

<span data-ttu-id="86613-633">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-633">**Syntax:**</span></span>  
`bool IsPresent(var expression)`

<span data-ttu-id="86613-634">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="86613-634">**Remarks:**</span></span>  
<span data-ttu-id="86613-635">Olá inverso dessa função é chamado IsNullOrEmpty.</span><span class="sxs-lookup"><span data-stu-id="86613-635">hello inverse of this function is named IsNullOrEmpty.</span></span>

<span data-ttu-id="86613-636">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-636">**Example:**</span></span>  
`Switch(IsPresent([directManager]),[directManager], IsPresent([skiplevelManager]),[skiplevelManager], IsPresent([director]),[director])`

- - -
### <a name="item"></a><span data-ttu-id="86613-637">Item</span><span class="sxs-lookup"><span data-stu-id="86613-637">Item</span></span>
<span data-ttu-id="86613-638">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-638">**Description:**</span></span>  
<span data-ttu-id="86613-639">Olá função Item Retorna um item de um cadeia de caracteres/atributo com vários valores.</span><span class="sxs-lookup"><span data-stu-id="86613-639">hello Item function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="86613-640">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-640">**Syntax:**</span></span>  
`var Item(mvstr attribute, num index)`

* <span data-ttu-id="86613-641">attribute: atributo com valores múltiplos</span><span class="sxs-lookup"><span data-stu-id="86613-641">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="86613-642">índice: índice tooan item da cadeia de caracteres com valores múltiplos hello.</span><span class="sxs-lookup"><span data-stu-id="86613-642">index: index tooan item in hello multi-valued string.</span></span>

<span data-ttu-id="86613-643">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="86613-643">**Remarks:**</span></span>  
<span data-ttu-id="86613-644">Olá função Item é útil junto com hello função Contains como função último hello retorna Olá índice tooan item no atributo de múltiplos hello.</span><span class="sxs-lookup"><span data-stu-id="86613-644">hello Item function is useful together with hello Contains function since hello latter function returns hello index tooan item in hello multi-valued attribute.</span></span>

<span data-ttu-id="86613-645">Gera um erro se o índice está fora dos limites.</span><span class="sxs-lookup"><span data-stu-id="86613-645">Throws an error if index is out of bounds.</span></span>

<span data-ttu-id="86613-646">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-646">**Example:**</span></span>  
`Mid(Item([proxyAddress],Contains([proxyAddress], "SMTP:")),6)`  
<span data-ttu-id="86613-647">Retorna Olá endereço de email principal.</span><span class="sxs-lookup"><span data-stu-id="86613-647">Returns hello primary email address.</span></span>

- - -
### <a name="itemornull"></a><span data-ttu-id="86613-648">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="86613-648">ItemOrNull</span></span>
<span data-ttu-id="86613-649">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-649">**Description:**</span></span>  
<span data-ttu-id="86613-650">Olá função ItemOrNull retorna um item de um cadeia de caracteres/atributo com vários valores.</span><span class="sxs-lookup"><span data-stu-id="86613-650">hello ItemOrNull function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="86613-651">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-651">**Syntax:**</span></span>  
`var ItemOrNull(mvstr attribute, num index)`

* <span data-ttu-id="86613-652">attribute: atributo com valores múltiplos</span><span class="sxs-lookup"><span data-stu-id="86613-652">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="86613-653">índice: índice tooan item da cadeia de caracteres com valores múltiplos hello.</span><span class="sxs-lookup"><span data-stu-id="86613-653">index: index tooan item in hello multi-valued string.</span></span>

<span data-ttu-id="86613-654">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="86613-654">**Remarks:**</span></span>  
<span data-ttu-id="86613-655">Olá função ItemOrNull é útil junto com hello função Contains, como função último hello retorna Olá índice tooan item no atributo de múltiplos hello.</span><span class="sxs-lookup"><span data-stu-id="86613-655">hello ItemOrNull function is useful together with hello Contains function since hello latter function returns hello index tooan item in hello multi-valued attribute.</span></span>

<span data-ttu-id="86613-656">Se o índice estiver fora dos limites, retornará um valor Null.</span><span class="sxs-lookup"><span data-stu-id="86613-656">If index is out of bounds, then returns a Null value.</span></span>

- - -
### <a name="join"></a><span data-ttu-id="86613-657">Join</span><span class="sxs-lookup"><span data-stu-id="86613-657">Join</span></span>
<span data-ttu-id="86613-658">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-658">**Description:**</span></span>  
<span data-ttu-id="86613-659">função Hello usa uma cadeia de caracteres com valores múltiplos e retorna uma cadeia de caracteres de valor único com o separador especificado inserido entre cada item.</span><span class="sxs-lookup"><span data-stu-id="86613-659">hello Join function takes a multi-valued string and returns a single-valued string with specified separator inserted between each item.</span></span>

<span data-ttu-id="86613-660">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-660">**Syntax:**</span></span>  
`str Join(mvstr attribute)`  
`str Join(mvstr attribute, str Delimiter)`

* <span data-ttu-id="86613-661">atributo: atributo com valores múltiplos contendo cadeias de caracteres toobe associado.</span><span class="sxs-lookup"><span data-stu-id="86613-661">attribute: Multi-valued attribute containing strings toobe joined.</span></span>
* <span data-ttu-id="86613-662">delimitador: qualquer cadeia de caracteres, tooseparate usado Olá subcadeias de caracteres em Olá retornou uma cadeia.</span><span class="sxs-lookup"><span data-stu-id="86613-662">delimiter: Any string, used tooseparate hello substrings in hello returned string.</span></span> <span data-ttu-id="86613-663">Se omitido, Olá caractere de espaço ("") é usado.</span><span class="sxs-lookup"><span data-stu-id="86613-663">If omitted, hello space character (" ") is used.</span></span> <span data-ttu-id="86613-664">Se o delimitador é uma cadeia de caracteres de comprimento zero ("") ou nada, todos os itens na lista de saudação são concatenados sem delimitadores.</span><span class="sxs-lookup"><span data-stu-id="86613-664">If Delimiter is a zero-length string ("") or Nothing, all items in hello list are concatenated with no delimiters.</span></span>

<span data-ttu-id="86613-665">**Comentários**</span><span class="sxs-lookup"><span data-stu-id="86613-665">**Remarks**</span></span>  
<span data-ttu-id="86613-666">Há uma paridade entre hello associação e funções de divisão.</span><span class="sxs-lookup"><span data-stu-id="86613-666">There is parity between hello Join and Split functions.</span></span> <span data-ttu-id="86613-667">Olá função Join pega uma matriz de cadeias de caracteres e associa usando uma cadeia de caracteres delimitadora, tooreturn uma única cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="86613-667">hello Join function takes an array of strings and joins them using a delimiter string, tooreturn a single string.</span></span> <span data-ttu-id="86613-668">Olá função Split usa uma cadeia de caracteres e separa no delimitador hello, tooreturn uma matriz de cadeias de caracteres.</span><span class="sxs-lookup"><span data-stu-id="86613-668">hello Split function takes a string and separates it at hello delimiter, tooreturn an array of strings.</span></span> <span data-ttu-id="86613-669">No entanto, uma diferença importante é que a Join pode concatenar cadeias de caracteres com qualquer cadeia de caracteres delimitadora, enquanto Split só pode separar cadeias de caracteres usando um único caractere delimitador.</span><span class="sxs-lookup"><span data-stu-id="86613-669">However, a key difference is that Join can concatenate strings with any delimiter string, Split can only separate strings using a single character delimiter.</span></span>

<span data-ttu-id="86613-670">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-670">**Example:**</span></span>  
`Join([proxyAddresses],",")`  
<span data-ttu-id="86613-671">Poderia retornar: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="86613-671">Could return: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"</span></span>

- - -
### <a name="lcase"></a><span data-ttu-id="86613-672">LCase</span><span class="sxs-lookup"><span data-stu-id="86613-672">LCase</span></span>
<span data-ttu-id="86613-673">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-673">**Description:**</span></span>  
<span data-ttu-id="86613-674">Olá Função LCase converte todos os caracteres no caso de toolower cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="86613-674">hello LCase function converts all characters in a string toolower case.</span></span>

<span data-ttu-id="86613-675">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-675">**Syntax:**</span></span>  
`str LCase(str value)`

<span data-ttu-id="86613-676">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-676">**Example:**</span></span>  
`LCase("TeSt")`  
<span data-ttu-id="86613-677">retorna "test".</span><span class="sxs-lookup"><span data-stu-id="86613-677">Returns "test".</span></span>

- - -
### <a name="left"></a><span data-ttu-id="86613-678">Left</span><span class="sxs-lookup"><span data-stu-id="86613-678">Left</span></span>
<span data-ttu-id="86613-679">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-679">**Description:**</span></span>  
<span data-ttu-id="86613-680">função Left Olá retorna um número especificado de caracteres da esquerda de saudação de uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="86613-680">hello Left function returns a specified number of characters from hello left of a string.</span></span>

<span data-ttu-id="86613-681">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-681">**Syntax:**</span></span>  
`str Left(str string, num NumChars)`

* <span data-ttu-id="86613-682">cadeia de caracteres: Olá tooreturn caracteres de</span><span class="sxs-lookup"><span data-stu-id="86613-682">string: hello string tooreturn characters from</span></span>
* <span data-ttu-id="86613-683">NumChars: um número que identifica Olá número de caracteres tooreturn desde o início de saudação (à esquerda) da cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="86613-683">NumChars: a number identifying hello number of characters tooreturn from hello beginning (left) of string</span></span>

<span data-ttu-id="86613-684">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="86613-684">**Remarks:**</span></span>  
<span data-ttu-id="86613-685">Uma cadeia de caracteres que contém a saudação primeiro os caracteres numChars na cadeia de caracteres:</span><span class="sxs-lookup"><span data-stu-id="86613-685">A string containing hello first numChars characters in string:</span></span>

* <span data-ttu-id="86613-686">Se numChars = 0, retorne a cadeia de caracteres vazia.</span><span class="sxs-lookup"><span data-stu-id="86613-686">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="86613-687">Se numChars < 0, retorne a cadeia de caracteres de entrada.</span><span class="sxs-lookup"><span data-stu-id="86613-687">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="86613-688">Se a cadeia de caracteres for nula, retorne a cadeia de caracteres vazia.</span><span class="sxs-lookup"><span data-stu-id="86613-688">If string is null, return empty string.</span></span>

<span data-ttu-id="86613-689">Se a cadeia de caracteres contém caracteres menores do que o número de saudação especificado em numChars, uma toostring idênticos de cadeia de caracteres (isto é, que contém todos os caracteres no parâmetro 1) será retornado.</span><span class="sxs-lookup"><span data-stu-id="86613-689">If string contains fewer characters than hello number specified in numChars, a string identical toostring (that is, containing all characters in parameter 1) is returned.</span></span>

<span data-ttu-id="86613-690">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-690">**Example:**</span></span>  
`Left("John Doe", 3)`  
<span data-ttu-id="86613-691">retorna "Joh".</span><span class="sxs-lookup"><span data-stu-id="86613-691">Returns "Joh".</span></span>

- - -
### <a name="len"></a><span data-ttu-id="86613-692">Len</span><span class="sxs-lookup"><span data-stu-id="86613-692">Len</span></span>
<span data-ttu-id="86613-693">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-693">**Description:**</span></span>  
<span data-ttu-id="86613-694">Olá função Len retorna o número de caracteres em uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="86613-694">hello Len function returns number of characters in a string.</span></span>

<span data-ttu-id="86613-695">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-695">**Syntax:**</span></span>  
`num Len(str value)`

<span data-ttu-id="86613-696">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-696">**Example:**</span></span>  
`Len("John Doe")`  
<span data-ttu-id="86613-697">retorna 8</span><span class="sxs-lookup"><span data-stu-id="86613-697">Returns 8</span></span>

- - -
### <a name="ltrim"></a><span data-ttu-id="86613-698">LTrim</span><span class="sxs-lookup"><span data-stu-id="86613-698">LTrim</span></span>
<span data-ttu-id="86613-699">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-699">**Description:**</span></span>  
<span data-ttu-id="86613-700">Olá função LTrim remove espaços em branco à esquerda de uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="86613-700">hello LTrim function removes leading white spaces from a string.</span></span>

<span data-ttu-id="86613-701">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-701">**Syntax:**</span></span>  
`str LTrim(str value)`

<span data-ttu-id="86613-702">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-702">**Example:**</span></span>  
`LTrim(" Test ")`  
<span data-ttu-id="86613-703">retorna "Test"</span><span class="sxs-lookup"><span data-stu-id="86613-703">Returns "Test "</span></span>

- - -
### <a name="mid"></a><span data-ttu-id="86613-704">Mid</span><span class="sxs-lookup"><span data-stu-id="86613-704">Mid</span></span>
<span data-ttu-id="86613-705">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-705">**Description:**</span></span>  
<span data-ttu-id="86613-706">Olá Mid função retorna um número especificado de caracteres de uma posição especificada em uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="86613-706">hello Mid function returns a specified number of characters from a specified position in a string.</span></span>

<span data-ttu-id="86613-707">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-707">**Syntax:**</span></span>  
`str Mid(str string, num start, num NumChars)`

* <span data-ttu-id="86613-708">cadeia de caracteres: Olá tooreturn caracteres de</span><span class="sxs-lookup"><span data-stu-id="86613-708">string: hello string tooreturn characters from</span></span>
* <span data-ttu-id="86613-709">Iniciar: um número que identifica a saudação em caracteres de tooreturn de cadeia de caracteres do início</span><span class="sxs-lookup"><span data-stu-id="86613-709">start: a number identifying hello starting position in string tooreturn characters from</span></span>
* <span data-ttu-id="86613-710">NumChars: um número que identifica Olá número de caracteres tooreturn da posição na cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="86613-710">NumChars: a number identifying hello number of characters tooreturn from position in string</span></span>

<span data-ttu-id="86613-711">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="86613-711">**Remarks:**</span></span>  
<span data-ttu-id="86613-712">retorna os caracteres numChars começando na posição inicial da cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="86613-712">Return numChars characters starting from position start in string.</span></span>  
<span data-ttu-id="86613-713">Uma cadeia de caracteres contendo caracteres numChars desde a posição inicial na cadeia de caracteres:</span><span class="sxs-lookup"><span data-stu-id="86613-713">A string containing numChars characters from position start in string:</span></span>

* <span data-ttu-id="86613-714">Se numChars = 0, retorne a cadeia de caracteres vazia.</span><span class="sxs-lookup"><span data-stu-id="86613-714">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="86613-715">Se numChars < 0, retorne a cadeia de caracteres de entrada.</span><span class="sxs-lookup"><span data-stu-id="86613-715">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="86613-716">Se Iniciar > Olá comprimento da cadeia de caracteres, retorna a cadeia de caracteres de entrada.</span><span class="sxs-lookup"><span data-stu-id="86613-716">If start > hello length of string, return input string.</span></span>
* <span data-ttu-id="86613-717">Se start <= 0, retorne a cadeia de caracteres de entrada.</span><span class="sxs-lookup"><span data-stu-id="86613-717">If start <= 0, return input string.</span></span>
* <span data-ttu-id="86613-718">Se a cadeia de caracteres for nula, retorne a cadeia de caracteres vazia.</span><span class="sxs-lookup"><span data-stu-id="86613-718">If string is null, return empty string.</span></span>

<span data-ttu-id="86613-719">Se não houver nenhum caractere numChar restante na cadeia de caracteres a partir da posição inicial, o máximo possível de caracteres será retornado.</span><span class="sxs-lookup"><span data-stu-id="86613-719">If there are not numChar characters remaining in string from position start, as many characters as possible are returned.</span></span>

<span data-ttu-id="86613-720">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-720">**Example:**</span></span>  
`Mid("John Doe", 3, 5)`  
<span data-ttu-id="86613-721">retorna "hn Do".</span><span class="sxs-lookup"><span data-stu-id="86613-721">Returns "hn Do".</span></span>

`Mid("John Doe", 6, 999)`  
<span data-ttu-id="86613-722">retorna "Doe"</span><span class="sxs-lookup"><span data-stu-id="86613-722">Returns "Doe"</span></span>

- - -
### <a name="now"></a><span data-ttu-id="86613-723">Now</span><span class="sxs-lookup"><span data-stu-id="86613-723">Now</span></span>
<span data-ttu-id="86613-724">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-724">**Description:**</span></span>  
<span data-ttu-id="86613-725">Olá agora função retorna um DateTime especifico Olá atual data e hora, tooyour data do sistema do computador e a hora de acordo com.</span><span class="sxs-lookup"><span data-stu-id="86613-725">hello Now function returns a DateTime specifying hello current date and time, according tooyour computer's system date and time.</span></span>

<span data-ttu-id="86613-726">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-726">**Syntax:**</span></span>  
`dt Now()`

- - -
### <a name="numfromdate"></a><span data-ttu-id="86613-727">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="86613-727">NumFromDate</span></span>
<span data-ttu-id="86613-728">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-728">**Description:**</span></span>  
<span data-ttu-id="86613-729">Olá função NumFromDate retorna uma data no formato de data do AD.</span><span class="sxs-lookup"><span data-stu-id="86613-729">hello NumFromDate function returns a date in AD’s date format.</span></span>

<span data-ttu-id="86613-730">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-730">**Syntax:**</span></span>  
`num NumFromDate(dt value)`

<span data-ttu-id="86613-731">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-731">**Example:**</span></span>  
`NumFromDate(CDate("2012-01-01 23:00:00"))`  
<span data-ttu-id="86613-732">retorna 129699324000000000</span><span class="sxs-lookup"><span data-stu-id="86613-732">Returns 129699324000000000</span></span>

- - -
### <a name="padleft"></a><span data-ttu-id="86613-733">PadLeft</span><span class="sxs-lookup"><span data-stu-id="86613-733">PadLeft</span></span>
<span data-ttu-id="86613-734">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-734">**Description:**</span></span>  
<span data-ttu-id="86613-735">Olá PadLeft preenche à esquerda de função um tooa de cadeia de caracteres especificada comprimento usando um caractere de preenchimento fornecido.</span><span class="sxs-lookup"><span data-stu-id="86613-735">hello PadLeft function left-pads a string tooa specified length using a provided padding character.</span></span>

<span data-ttu-id="86613-736">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-736">**Syntax:**</span></span>  
`str PadLeft(str string, num length, str padCharacter)`

* <span data-ttu-id="86613-737">cadeia de caracteres: Olá toopad de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="86613-737">string: hello string toopad.</span></span>
* <span data-ttu-id="86613-738">comprimento: um inteiro que representa a saudação desejado comprimento da cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="86613-738">length: An integer representing hello desired length of string.</span></span>
* <span data-ttu-id="86613-739">padCharacter: uma cadeia de caracteres que consiste em toouse um único caractere como caractere de preenchimento de saudação</span><span class="sxs-lookup"><span data-stu-id="86613-739">padCharacter: A string consisting of a single character toouse as hello pad character</span></span>

<span data-ttu-id="86613-740">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="86613-740">**Remarks:**</span></span>

* <span data-ttu-id="86613-741">Se o comprimento de saudação de cadeia de caracteres for menor que o comprimento, padCharacter é repetidamente anexado toohello início (à esquerda) da cadeia de caracteres até que tenha uma toolength de comprimento igual.</span><span class="sxs-lookup"><span data-stu-id="86613-741">If hello length of string is less than length, then padCharacter is repeatedly appended toohello beginning (left) of string until it has a length equal toolength.</span></span>
* <span data-ttu-id="86613-742">PadCharacter pode ser um caractere de espaço, mas não pode ser um valor nulo.</span><span class="sxs-lookup"><span data-stu-id="86613-742">PadCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="86613-743">Se o comprimento de Olá de cadeia de caracteres for maior que o comprimento de tooor igual, a cadeia de caracteres é retornada inalterada.</span><span class="sxs-lookup"><span data-stu-id="86613-743">If hello length of string is equal tooor greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="86613-744">Se a cadeia de caracteres tem um comprimento maior que ou igual toolength, será retornado um toostring idênticos de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="86613-744">If string has a length greater than or equal toolength, a string identical toostring is returned.</span></span>
* <span data-ttu-id="86613-745">Se o comprimento de saudação de cadeia de caracteres for menor que o comprimento, uma nova cadeia de caracteres de saudação desejado comprimento é retornado que contém a cadeia de caracteres preenchida com um padCharacter.</span><span class="sxs-lookup"><span data-stu-id="86613-745">If hello length of string is less than length, then a new string of hello desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="86613-746">Se a cadeia de caracteres for nula, a função hello retorna uma cadeia de caracteres vazia.</span><span class="sxs-lookup"><span data-stu-id="86613-746">If string is null, hello function returns an empty string.</span></span>

<span data-ttu-id="86613-747">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-747">**Example:**</span></span>  
`PadLeft("User", 10, "0")`  
<span data-ttu-id="86613-748">retorna "000000User".</span><span class="sxs-lookup"><span data-stu-id="86613-748">Returns "000000User".</span></span>

- - -
### <a name="padright"></a><span data-ttu-id="86613-749">PadRight</span><span class="sxs-lookup"><span data-stu-id="86613-749">PadRight</span></span>
<span data-ttu-id="86613-750">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-750">**Description:**</span></span>  
<span data-ttu-id="86613-751">Olá PadRight preenche à direita de função um tooa de cadeia de caracteres especificada comprimento usando um caractere de preenchimento fornecido.</span><span class="sxs-lookup"><span data-stu-id="86613-751">hello PadRight function right-pads a string tooa specified length using a provided padding character.</span></span>

<span data-ttu-id="86613-752">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-752">**Syntax:**</span></span>  
`str PadRight(str string, num length, str padCharacter)`

* <span data-ttu-id="86613-753">cadeia de caracteres: Olá toopad de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="86613-753">string: hello string toopad.</span></span>
* <span data-ttu-id="86613-754">comprimento: um inteiro que representa a saudação desejado comprimento da cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="86613-754">length: An integer representing hello desired length of string.</span></span>
* <span data-ttu-id="86613-755">padCharacter: uma cadeia de caracteres que consiste em toouse um único caractere como caractere de preenchimento de saudação</span><span class="sxs-lookup"><span data-stu-id="86613-755">padCharacter: A string consisting of a single character toouse as hello pad character</span></span>

<span data-ttu-id="86613-756">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="86613-756">**Remarks:**</span></span>

* <span data-ttu-id="86613-757">Se o comprimento de saudação de cadeia de caracteres for menor que o comprimento, padCharacter é repetidamente anexado toohello final (à direita) da cadeia de caracteres até que tenha uma toolength de comprimento igual.</span><span class="sxs-lookup"><span data-stu-id="86613-757">If hello length of string is less than length, then padCharacter is repeatedly appended toohello end (right) of string until it has a length equal toolength.</span></span>
* <span data-ttu-id="86613-758">PadCharacter pode ser um caractere de espaço, mas não pode ser um valor nulo.</span><span class="sxs-lookup"><span data-stu-id="86613-758">padCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="86613-759">Se o comprimento de Olá de cadeia de caracteres for maior que o comprimento de tooor igual, a cadeia de caracteres é retornada inalterada.</span><span class="sxs-lookup"><span data-stu-id="86613-759">If hello length of string is equal tooor greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="86613-760">Se a cadeia de caracteres tem um comprimento maior que ou igual toolength, será retornado um toostring idênticos de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="86613-760">If string has a length greater than or equal toolength, a string identical toostring is returned.</span></span>
* <span data-ttu-id="86613-761">Se o comprimento de saudação de cadeia de caracteres for menor que o comprimento, uma nova cadeia de caracteres de saudação desejado comprimento é retornado que contém a cadeia de caracteres preenchida com um padCharacter.</span><span class="sxs-lookup"><span data-stu-id="86613-761">If hello length of string is less than length, then a new string of hello desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="86613-762">Se a cadeia de caracteres for nula, a função hello retorna uma cadeia de caracteres vazia.</span><span class="sxs-lookup"><span data-stu-id="86613-762">If string is null, hello function returns an empty string.</span></span>

<span data-ttu-id="86613-763">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-763">**Example:**</span></span>  
`PadRight("User", 10, "0")`  
<span data-ttu-id="86613-764">retorna "User000000".</span><span class="sxs-lookup"><span data-stu-id="86613-764">Returns "User000000".</span></span>

- - -
### <a name="pcase"></a><span data-ttu-id="86613-765">PCase</span><span class="sxs-lookup"><span data-stu-id="86613-765">PCase</span></span>
<span data-ttu-id="86613-766">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-766">**Description:**</span></span>  
<span data-ttu-id="86613-767">Olá função PCase converte Olá primeiro caractere de cada palavra delimitada por espaço em um caso de tooupper de cadeia de caracteres, e todos os outros caracteres são convertidos toolower caso.</span><span class="sxs-lookup"><span data-stu-id="86613-767">hello PCase function converts hello first character of each space delimited word in a string tooupper case, and all other characters are converted toolower case.</span></span>

<span data-ttu-id="86613-768">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-768">**Syntax:**</span></span>  
`String PCase(string)`

<span data-ttu-id="86613-769">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="86613-769">**Remarks:**</span></span>

* <span data-ttu-id="86613-770">Essa função no momento não oferece tooconvert de maiusculas e minúsculas adequadas uma palavra que está totalmente em letras maiusculas, como um acrônimo.</span><span class="sxs-lookup"><span data-stu-id="86613-770">This function does not currently provide proper casing tooconvert a word that is entirely uppercase, such as an acronym.</span></span>

<span data-ttu-id="86613-771">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-771">**Example:**</span></span>  
`PCase("TEsT")`  
<span data-ttu-id="86613-772">retorna "test".</span><span class="sxs-lookup"><span data-stu-id="86613-772">Returns "Test".</span></span>

`PCase(LCase("TEST"))`  
<span data-ttu-id="86613-773">Retorna "Test"</span><span class="sxs-lookup"><span data-stu-id="86613-773">Returns "Test"</span></span>

- - -
### <a name="randomnum"></a><span data-ttu-id="86613-774">RandomNum</span><span class="sxs-lookup"><span data-stu-id="86613-774">RandomNum</span></span>
<span data-ttu-id="86613-775">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-775">**Description:**</span></span>  
<span data-ttu-id="86613-776">Olá função RandomNum retorna um número aleatório entre um intervalo especificado.</span><span class="sxs-lookup"><span data-stu-id="86613-776">hello RandomNum function returns a random number between a specified interval.</span></span>

<span data-ttu-id="86613-777">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-777">**Syntax:**</span></span>  
`num RandomNum(num start, num end)`

* <span data-ttu-id="86613-778">Iniciar: um número identificação Olá limite inferior de saudação valor aleatório toogenerate</span><span class="sxs-lookup"><span data-stu-id="86613-778">start: a number identifying hello lower limit of hello random value toogenerate</span></span>
* <span data-ttu-id="86613-779">fim: um número identificação Olá limite superior de saudação valor aleatório toogenerate</span><span class="sxs-lookup"><span data-stu-id="86613-779">end: a number identifying hello upper limit of hello random value toogenerate</span></span>

<span data-ttu-id="86613-780">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-780">**Example:**</span></span>  
`Random(100,999)`  
<span data-ttu-id="86613-781">pode retornar 734.</span><span class="sxs-lookup"><span data-stu-id="86613-781">Can return 734.</span></span>

- - -
### <a name="removeduplicates"></a><span data-ttu-id="86613-782">RemoveDuplicates</span><span class="sxs-lookup"><span data-stu-id="86613-782">RemoveDuplicates</span></span>
<span data-ttu-id="86613-783">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-783">**Description:**</span></span>  
<span data-ttu-id="86613-784">Olá função RemoveDuplicates usa uma cadeia de caracteres com valores múltiplos e certificar-se de que cada valor é exclusivo.</span><span class="sxs-lookup"><span data-stu-id="86613-784">hello RemoveDuplicates function takes a multi-valued string and make sure each value is unique.</span></span>

<span data-ttu-id="86613-785">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-785">**Syntax:**</span></span>  
`mvstr RemoveDuplicates(mvstr attribute)`

<span data-ttu-id="86613-786">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-786">**Example:**</span></span>  
`RemoveDuplicates([proxyAddresses])`  
<span data-ttu-id="86613-787">retorna um atributo proxyAddress corrigido no qual todos os valores duplicados foram removidos.</span><span class="sxs-lookup"><span data-stu-id="86613-787">Returns a sanitized proxyAddress attribute where all duplicate values have been removed.</span></span>

- - -
### <a name="replace"></a><span data-ttu-id="86613-788">Substitua</span><span class="sxs-lookup"><span data-stu-id="86613-788">Replace</span></span>
<span data-ttu-id="86613-789">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-789">**Description:**</span></span>  
<span data-ttu-id="86613-790">Olá função Replace substitui todas as ocorrências de uma cadeia de caracteres de tooanother de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="86613-790">hello Replace function replaces all occurrences of a string tooanother string.</span></span>

<span data-ttu-id="86613-791">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-791">**Syntax:**</span></span>  
`str Replace(str string, str OldValue, str NewValue)`

* <span data-ttu-id="86613-792">cadeia de caracteres: uma cadeia de caracteres tooreplace valores em.</span><span class="sxs-lookup"><span data-stu-id="86613-792">string: A string tooreplace values in.</span></span>
* <span data-ttu-id="86613-793">OldValue: Olá toosearch de cadeia de caracteres para e tooreplace.</span><span class="sxs-lookup"><span data-stu-id="86613-793">OldValue: hello string toosearch for and tooreplace.</span></span>
* <span data-ttu-id="86613-794">NewValue: Olá tooreplace de cadeia de caracteres para.</span><span class="sxs-lookup"><span data-stu-id="86613-794">NewValue: hello string tooreplace to.</span></span>

<span data-ttu-id="86613-795">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="86613-795">**Remarks:**</span></span>  
<span data-ttu-id="86613-796">função Hello reconhece Olá monikers especiais a seguir:</span><span class="sxs-lookup"><span data-stu-id="86613-796">hello function recognizes hello following special monikers:</span></span>

* <span data-ttu-id="86613-797">\n - Nova linha</span><span class="sxs-lookup"><span data-stu-id="86613-797">\n – New Line</span></span>
* <span data-ttu-id="86613-798">\r - Retorno de carro</span><span class="sxs-lookup"><span data-stu-id="86613-798">\r – Carriage Return</span></span>
* <span data-ttu-id="86613-799">\t - Guia</span><span class="sxs-lookup"><span data-stu-id="86613-799">\t – Tab</span></span>

<span data-ttu-id="86613-800">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-800">**Example:**</span></span>  
`Replace([address],"\r\n",", ")`  
<span data-ttu-id="86613-801">Substitui CRLF com uma vírgula e um espaço e pode levar muito "One Microsoft maneira, Redmond, WA, EUA"</span><span class="sxs-lookup"><span data-stu-id="86613-801">Replaces CRLF with a comma and space, and could lead too"One Microsoft Way, Redmond, WA, USA"</span></span>

- - -
### <a name="replacechars"></a><span data-ttu-id="86613-802">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="86613-802">ReplaceChars</span></span>
<span data-ttu-id="86613-803">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-803">**Description:**</span></span>  
<span data-ttu-id="86613-804">Olá função ReplaceChars substitui todas as ocorrências de caracteres encontradas na cadeia de caracteres ReplacePattern de saudação.</span><span class="sxs-lookup"><span data-stu-id="86613-804">hello ReplaceChars function replaces all occurrences of characters found in hello ReplacePattern string.</span></span>

<span data-ttu-id="86613-805">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-805">**Syntax:**</span></span>  
`str ReplaceChars(str string, str ReplacePattern)`

* <span data-ttu-id="86613-806">cadeia de caracteres: caracteres tooreplace uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="86613-806">string: A string tooreplace characters in.</span></span>
* <span data-ttu-id="86613-807">ReplacePattern: uma cadeia de caracteres que contém um dicionário com caracteres tooreplace.</span><span class="sxs-lookup"><span data-stu-id="86613-807">ReplacePattern: a string containing a dictionary with characters tooreplace.</span></span>

<span data-ttu-id="86613-808">Olá formato é {source1}: {target1}, {source2}: {target2}, {sourceN}, {targetN} em que a fonte é Olá caractere toofind e destino Olá cadeia de caracteres tooreplace com.</span><span class="sxs-lookup"><span data-stu-id="86613-808">hello format is {source1}:{target1},{source2}:{target2},{sourceN},{targetN} where source is hello character toofind and target hello string tooreplace with.</span></span>

<span data-ttu-id="86613-809">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="86613-809">**Remarks:**</span></span>

* <span data-ttu-id="86613-810">função Hello usa cada ocorrência de fontes definidas e substitui-los com os destinos de saudação.</span><span class="sxs-lookup"><span data-stu-id="86613-810">hello function takes each occurrence of defined sources and replaces them with hello targets.</span></span>
* <span data-ttu-id="86613-811">fonte de saudação deve estar exatamente um caractere (unicode).</span><span class="sxs-lookup"><span data-stu-id="86613-811">hello source must be exactly one (unicode) character.</span></span>
* <span data-ttu-id="86613-812">origem de saudação não pode ser vazio ou maior que o caractere (erro de análise).</span><span class="sxs-lookup"><span data-stu-id="86613-812">hello source cannot be empty or longer than one character (parsing error).</span></span>
* <span data-ttu-id="86613-813">destino de saudação pode ter vários caracteres, por exemplo, OE, β: ss.</span><span class="sxs-lookup"><span data-stu-id="86613-813">hello target can have multiple characters, for example ö:oe, β:ss.</span></span>
* <span data-ttu-id="86613-814">Olá destino pode ser vazio, indicando que o caractere de saudação deve ser removida.</span><span class="sxs-lookup"><span data-stu-id="86613-814">hello target can be empty indicating that hello character should be removed.</span></span>
* <span data-ttu-id="86613-815">origem de saudação diferencia maiusculas de minúsculas e deve ser uma correspondência exata.</span><span class="sxs-lookup"><span data-stu-id="86613-815">hello source is case-sensitive and must be an exact match.</span></span>
* <span data-ttu-id="86613-816">Olá, (vírgula) e: (dois-pontos) são caracteres reservados e não podem ser substituídos usando essa função.</span><span class="sxs-lookup"><span data-stu-id="86613-816">hello , (comma) and : (colon) are reserved characters and cannot be replaced using this function.</span></span>
* <span data-ttu-id="86613-817">Espaços e outros caracteres em branco na cadeia de caracteres ReplacePattern de saudação é ignorado.</span><span class="sxs-lookup"><span data-stu-id="86613-817">Spaces and other white characters in hello ReplacePattern string are ignored.</span></span>

<span data-ttu-id="86613-818">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-818">**Example:**</span></span>  
`%ReplaceString% = ’:,Å:A,Ä:A,Ö:O,å:a,ä:a,ö,o`

`ReplaceChars("Räksmörgås",%ReplaceString%)`  
<span data-ttu-id="86613-819">retorna Raksmorgas</span><span class="sxs-lookup"><span data-stu-id="86613-819">Returns Raksmorgas</span></span>

`ReplaceChars("O’Neil",%ReplaceString%)`  
<span data-ttu-id="86613-820">Retorna "ONeil", o único tique de saudação é definido toobe removido.</span><span class="sxs-lookup"><span data-stu-id="86613-820">Returns "ONeil", hello single tick is defined toobe removed.</span></span>

- - -
### <a name="right"></a><span data-ttu-id="86613-821">Right</span><span class="sxs-lookup"><span data-stu-id="86613-821">Right</span></span>
<span data-ttu-id="86613-822">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-822">**Description:**</span></span>  
<span data-ttu-id="86613-823">função Right Olá retorna um número especificado de caracteres de saudação à direita (fim) de uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="86613-823">hello Right function returns a specified number of characters from hello right (end) of a string.</span></span>

<span data-ttu-id="86613-824">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-824">**Syntax:**</span></span>  
`str Right(str string, num NumChars)`

* <span data-ttu-id="86613-825">cadeia de caracteres: Olá tooreturn caracteres de</span><span class="sxs-lookup"><span data-stu-id="86613-825">string: hello string tooreturn characters from</span></span>
* <span data-ttu-id="86613-826">NumChars: um número que identifica Olá número de caracteres tooreturn de término hello (à direita) da cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="86613-826">NumChars: a number identifying hello number of characters tooreturn from hello end (right) of string</span></span>

<span data-ttu-id="86613-827">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="86613-827">**Remarks:**</span></span>  
<span data-ttu-id="86613-828">Os caracteres NumChars são retornados da última posição Olá de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="86613-828">NumChars characters are returned from hello last position of string.</span></span>

<span data-ttu-id="86613-829">Uma cadeia de caracteres que contém os últimos caracteres numChars Olá na cadeia de caracteres:</span><span class="sxs-lookup"><span data-stu-id="86613-829">A string containing hello last numChars characters in string:</span></span>

* <span data-ttu-id="86613-830">Se numChars = 0, retorne a cadeia de caracteres vazia.</span><span class="sxs-lookup"><span data-stu-id="86613-830">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="86613-831">Se numChars < 0, retorne a cadeia de caracteres de entrada.</span><span class="sxs-lookup"><span data-stu-id="86613-831">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="86613-832">Se a cadeia de caracteres for nula, retorne a cadeia de caracteres vazia.</span><span class="sxs-lookup"><span data-stu-id="86613-832">If string is null, return empty string.</span></span>

<span data-ttu-id="86613-833">Se a cadeia de caracteres contiver menos caracteres que Olá número especificado no NumChars, uma toostring idênticos de cadeia de caracteres é retornado.</span><span class="sxs-lookup"><span data-stu-id="86613-833">If string contains fewer characters than hello number specified in NumChars, a string identical toostring is returned.</span></span>

<span data-ttu-id="86613-834">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-834">**Example:**</span></span>  
`Right("John Doe", 3)`  
<span data-ttu-id="86613-835">retorna "Doe".</span><span class="sxs-lookup"><span data-stu-id="86613-835">Returns "Doe".</span></span>

- - -
### <a name="rtrim"></a><span data-ttu-id="86613-836">RTrim</span><span class="sxs-lookup"><span data-stu-id="86613-836">RTrim</span></span>
<span data-ttu-id="86613-837">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-837">**Description:**</span></span>  
<span data-ttu-id="86613-838">Olá função RTrim remove espaços em branco à direita de uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="86613-838">hello RTrim function removes trailing white spaces from a string.</span></span>

<span data-ttu-id="86613-839">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-839">**Syntax:**</span></span>  
`str RTrim(str value)`

<span data-ttu-id="86613-840">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-840">**Example:**</span></span>  
`RTrim(" Test ")`  
<span data-ttu-id="86613-841">retorna "Test".</span><span class="sxs-lookup"><span data-stu-id="86613-841">Returns " Test".</span></span>

- - -
### <a name="select"></a><span data-ttu-id="86613-842">Selecionar</span><span class="sxs-lookup"><span data-stu-id="86613-842">Select</span></span>
<span data-ttu-id="86613-843">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-843">**Description:**</span></span>  
<span data-ttu-id="86613-844">Processa todos os valores em um atributo de valores múltiplos (ou a saída de uma expressão) com base na função especificada.</span><span class="sxs-lookup"><span data-stu-id="86613-844">Process all values in a multi-valued attribute (or output of an expression) based on function specified.</span></span>

<span data-ttu-id="86613-845">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-845">**Syntax:**</span></span>  
`mvattr Select(variable item, mvattr attribute, func function)`  
`mvattr Select(variable item, exp expression, func function)`

* <span data-ttu-id="86613-846">item: representa um elemento no atributo de múltiplos Olá</span><span class="sxs-lookup"><span data-stu-id="86613-846">item: Represents an element in hello multi-valued attribute</span></span>
* <span data-ttu-id="86613-847">atributo: atributo de múltiplos Olá</span><span class="sxs-lookup"><span data-stu-id="86613-847">attribute: hello multi-valued attribute</span></span>
* <span data-ttu-id="86613-848">expression: uma expressão que retorna uma coleção de valores</span><span class="sxs-lookup"><span data-stu-id="86613-848">expression: an expression that returns a collection of values</span></span>
* <span data-ttu-id="86613-849">condição: qualquer função que pode processar um item no atributo Olá</span><span class="sxs-lookup"><span data-stu-id="86613-849">condition: any function that can process an item in hello attribute</span></span>

<span data-ttu-id="86613-850">**Exemplos:**</span><span class="sxs-lookup"><span data-stu-id="86613-850">**Examples:**</span></span>  
`Select($item,[otherPhone],Replace($item,“-”,“”))`  
<span data-ttu-id="86613-851">Retorne todos os valores de Olá no otherPhone de atributo com vários valores hello depois hifens (-) foram removidos.</span><span class="sxs-lookup"><span data-stu-id="86613-851">Return all hello values in hello multi-valued attribute otherPhone after hyphens (-) have been removed.</span></span>

- - -
### <a name="split"></a><span data-ttu-id="86613-852">Divisão</span><span class="sxs-lookup"><span data-stu-id="86613-852">Split</span></span>
<span data-ttu-id="86613-853">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-853">**Description:**</span></span>  
<span data-ttu-id="86613-854">Olá função Split usa uma cadeia de caracteres separada por um delimitador e facilita uma cadeia de caracteres com valores múltiplos.</span><span class="sxs-lookup"><span data-stu-id="86613-854">hello Split function takes a string separated with a delimiter and makes it a multi-valued string.</span></span>

<span data-ttu-id="86613-855">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-855">**Syntax:**</span></span>  
`mvstr Split(str value, str delimiter)`  
`mvstr Split(str value, str delimiter, num limit)`

* <span data-ttu-id="86613-856">valor: Olá a cadeia de caracteres com um tooseparate de caractere delimitador.</span><span class="sxs-lookup"><span data-stu-id="86613-856">value: hello string with a delimiter character tooseparate.</span></span>
* <span data-ttu-id="86613-857">delimitador: único toobe caractere usado como Olá delimitador.</span><span class="sxs-lookup"><span data-stu-id="86613-857">delimiter: single character toobe used as hello delimiter.</span></span>
* <span data-ttu-id="86613-858">limite: o número máximo de valores que podem ser retornados.</span><span class="sxs-lookup"><span data-stu-id="86613-858">limit: maximum number of values that can return.</span></span>

<span data-ttu-id="86613-859">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-859">**Example:**</span></span>  
`Split("SMTP:john.doe@contoso.com,smtp:jd@contoso.com",",")`  
<span data-ttu-id="86613-860">Retorna uma cadeia de caracteres com valores múltiplos com 2 elementos úteis para o atributo proxyAddress de saudação.</span><span class="sxs-lookup"><span data-stu-id="86613-860">Returns a multi-valued string with 2 elements useful for hello proxyAddress attribute.</span></span>

- - -
### <a name="stringfromguid"></a><span data-ttu-id="86613-861">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="86613-861">StringFromGuid</span></span>
<span data-ttu-id="86613-862">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-862">**Description:**</span></span>  
<span data-ttu-id="86613-863">Olá função StringFromGuid usa um GUID binário e converte-a cadeia de caracteres tooa</span><span class="sxs-lookup"><span data-stu-id="86613-863">hello StringFromGuid function takes a binary GUID and converts it tooa string</span></span>

<span data-ttu-id="86613-864">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-864">**Syntax:**</span></span>  
`str StringFromGuid(bin GUID)`

- - -
### <a name="stringfromsid"></a><span data-ttu-id="86613-865">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="86613-865">StringFromSid</span></span>
<span data-ttu-id="86613-866">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-866">**Description:**</span></span>  
<span data-ttu-id="86613-867">Olá função StringFromSid converte uma matriz de bytes que contém uma cadeia de caracteres de tooa de identificador de segurança.</span><span class="sxs-lookup"><span data-stu-id="86613-867">hello StringFromSid function converts a byte array containing a security identifier tooa string.</span></span>

<span data-ttu-id="86613-868">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-868">**Syntax:**</span></span>  
`str StringFromSid(bin ObjectSID)`  

- - -
### <a name="switch"></a><span data-ttu-id="86613-869">Switch</span><span class="sxs-lookup"><span data-stu-id="86613-869">Switch</span></span>
<span data-ttu-id="86613-870">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-870">**Description:**</span></span>  
<span data-ttu-id="86613-871">função de comutador Hello é tooreturn usado um único valor com base nas condições avaliadas.</span><span class="sxs-lookup"><span data-stu-id="86613-871">hello Switch function is used tooreturn a single value based on evaluated conditions.</span></span>

<span data-ttu-id="86613-872">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-872">**Syntax:**</span></span>  
`var Switch(exp expr1, var value1[, exp expr2, var value … [, exp expr, var valueN]])`

* <span data-ttu-id="86613-873">expr: expressão Variant que você deseja tooevaluate.</span><span class="sxs-lookup"><span data-stu-id="86613-873">expr: Variant expression you want tooevaluate.</span></span>
* <span data-ttu-id="86613-874">valor: toobe do valor retornado se a expressão correspondente Olá é True.</span><span class="sxs-lookup"><span data-stu-id="86613-874">value: Value toobe returned if hello corresponding expression is True.</span></span>

<span data-ttu-id="86613-875">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="86613-875">**Remarks:**</span></span>  
<span data-ttu-id="86613-876">Olá argumento da função Switch consiste em pares de expressões e valores.</span><span class="sxs-lookup"><span data-stu-id="86613-876">hello Switch function argument list consists of pairs of expressions and values.</span></span> <span data-ttu-id="86613-877">Olá expressões são avaliadas da esquerda tooright e valor Olá associado Olá primeira expressão tooevaluate tooTrue será retornado.</span><span class="sxs-lookup"><span data-stu-id="86613-877">hello expressions are evaluated from left tooright, and hello value associated with hello first expression tooevaluate tooTrue is returned.</span></span> <span data-ttu-id="86613-878">Se partes da saudação não tiverem pares adequados, ocorrerá um erro de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="86613-878">If hello parts aren't properly paired, a run-time error occurs.</span></span>

<span data-ttu-id="86613-879">Por exemplo, se expr1 for True, o comutador retornará valor1.</span><span class="sxs-lookup"><span data-stu-id="86613-879">For example, if expr1 is True, Switch returns value1.</span></span> <span data-ttu-id="86613-880">Se expr-1 for False, mas expr-2 for True, Switch retorna valor-2 e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="86613-880">If expr-1 is False, but expr-2 is True, Switch returns value-2, and so on.</span></span>

<span data-ttu-id="86613-881">Switch retorna um Nothing se:</span><span class="sxs-lookup"><span data-stu-id="86613-881">Switch returns a Nothing if:</span></span>

* <span data-ttu-id="86613-882">Nenhuma das expressões Olá forem True.</span><span class="sxs-lookup"><span data-stu-id="86613-882">None of hello expressions are True.</span></span>
* <span data-ttu-id="86613-883">primeira expressão True de saudação tem um valor correspondente que é Null.</span><span class="sxs-lookup"><span data-stu-id="86613-883">hello first True expression has a corresponding value that is Null.</span></span>

<span data-ttu-id="86613-884">Switch avalia todas as expressões, mesmo que retorne apenas uma delas.</span><span class="sxs-lookup"><span data-stu-id="86613-884">Switch evaluates all expressions, even though it returns only one of them.</span></span> <span data-ttu-id="86613-885">Por essa razão, você deve tomar cuidado com efeitos colaterais indesejáveis.</span><span class="sxs-lookup"><span data-stu-id="86613-885">For this reason, you should watch for undesirable side effects.</span></span> <span data-ttu-id="86613-886">Por exemplo, se a avaliação de saudação de qualquer expressão resulta em uma divisão por zero, ocorrerá um erro.</span><span class="sxs-lookup"><span data-stu-id="86613-886">For example, if hello evaluation of any expression results in a division by zero error, an error occurs.</span></span>

<span data-ttu-id="86613-887">Valor também pode ser a função de erro hello, que retorna uma cadeia de caracteres personalizada.</span><span class="sxs-lookup"><span data-stu-id="86613-887">Value can also be hello Error function, which would return a custom string.</span></span>

<span data-ttu-id="86613-888">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-888">**Example:**</span></span>  
`Switch([city] = "London", "English", [city] = "Rome", "Italian", [city] = "Paris", "French", True, Error("Unknown city"))`  
<span data-ttu-id="86613-889">Retorna Olá idioma falado em algumas cidades, caso contrário, retornará um erro.</span><span class="sxs-lookup"><span data-stu-id="86613-889">Returns hello language spoken in some major cities, otherwise returns an Error.</span></span>

- - -
### <a name="trim"></a><span data-ttu-id="86613-890">Trim</span><span class="sxs-lookup"><span data-stu-id="86613-890">Trim</span></span>
<span data-ttu-id="86613-891">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-891">**Description:**</span></span>  
<span data-ttu-id="86613-892">função Trim Olá remove espaços à direita e branco de uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="86613-892">hello Trim function removes leading and trailing white spaces from a string.</span></span>

<span data-ttu-id="86613-893">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-893">**Syntax:**</span></span>  
`str Trim(str value)`  

<span data-ttu-id="86613-894">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-894">**Example:**</span></span>  
`Trim(" Test ")`  
<span data-ttu-id="86613-895">retorna "test".</span><span class="sxs-lookup"><span data-stu-id="86613-895">Returns "Test".</span></span>

`Trim([proxyAddresses])`  
<span data-ttu-id="86613-896">Remove espaços à direita e para cada valor no atributo proxyAddress de saudação.</span><span class="sxs-lookup"><span data-stu-id="86613-896">Removes leading and trailing spaces for each value in hello proxyAddress attribute.</span></span>

- - -
### <a name="ucase"></a><span data-ttu-id="86613-897">UCase</span><span class="sxs-lookup"><span data-stu-id="86613-897">UCase</span></span>
<span data-ttu-id="86613-898">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-898">**Description:**</span></span>  
<span data-ttu-id="86613-899">Olá função UCase converte todos os caracteres no caso de tooupper cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="86613-899">hello UCase function converts all characters in a string tooupper case.</span></span>

<span data-ttu-id="86613-900">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-900">**Syntax:**</span></span>  
`str UCase(str string)`

<span data-ttu-id="86613-901">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-901">**Example:**</span></span>  
`UCase("TeSt")`  
<span data-ttu-id="86613-902">retorna "test".</span><span class="sxs-lookup"><span data-stu-id="86613-902">Returns "TEST".</span></span>

- - -
### <a name="where"></a><span data-ttu-id="86613-903">Where</span><span class="sxs-lookup"><span data-stu-id="86613-903">Where</span></span>

<span data-ttu-id="86613-904">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-904">**Description:**</span></span>  
<span data-ttu-id="86613-905">Retorna um subconjunto de valores de um atributo de valores múltiplos (ou a saída de uma expressão) com base em uma condição específica.</span><span class="sxs-lookup"><span data-stu-id="86613-905">Returns a subset of values from a multi-valued attribute (or output of an expression) based on specific condition.</span></span>

<span data-ttu-id="86613-906">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-906">**Syntax:**</span></span>  
`mvattr Where(variable item, mvattr attribute, exp condition)`  
`mvattr Where(variable item, exp expression, exp condition)`  
* <span data-ttu-id="86613-907">item: representa um elemento no atributo de múltiplos Olá</span><span class="sxs-lookup"><span data-stu-id="86613-907">item: Represents an element in hello multi-valued attribute</span></span>
* <span data-ttu-id="86613-908">atributo: atributo de múltiplos Olá</span><span class="sxs-lookup"><span data-stu-id="86613-908">attribute: hello multi-valued attribute</span></span>
* <span data-ttu-id="86613-909">condição: qualquer expressão que pode ser avaliada tootrue ou false</span><span class="sxs-lookup"><span data-stu-id="86613-909">condition: any expression that can be evaluated tootrue or false</span></span>
* <span data-ttu-id="86613-910">expression: uma expressão que retorna uma coleção de valores</span><span class="sxs-lookup"><span data-stu-id="86613-910">expression: an expression that returns a collection of values</span></span>

<span data-ttu-id="86613-911">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-911">**Example:**</span></span>  
`Where($item,[userCertificate],CertNotAfter($item)>Now())`  
<span data-ttu-id="86613-912">Retorne valores de certificado Olá Olá userCertificate de atributo com vários valores que não estão expiradas.</span><span class="sxs-lookup"><span data-stu-id="86613-912">Return hello certificate values in hello multi-valued attribute userCertificate which aren’t expired.</span></span>

- - -
### <a name="with"></a><span data-ttu-id="86613-913">With</span><span class="sxs-lookup"><span data-stu-id="86613-913">With</span></span>
<span data-ttu-id="86613-914">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-914">**Description:**</span></span>  
<span data-ttu-id="86613-915">Olá com função fornece uma maneira toosimplify uma expressão complexa usando uma variável toorepresent uma subexpressão que aparece uma ou mais vezes na expressão complexa hello.</span><span class="sxs-lookup"><span data-stu-id="86613-915">hello With function provides a way toosimplify a complex expression by using a variable toorepresent a subexpression which appears one or more times in hello complex expression.</span></span>

<span data-ttu-id="86613-916">**Sintaxe:**
`With(var variable, exp subExpression, exp complexExpression)`</span><span class="sxs-lookup"><span data-stu-id="86613-916">**Syntax:**
`With(var variable, exp subExpression, exp complexExpression)`</span></span>  
* <span data-ttu-id="86613-917">variável: representa Olá subexpressão.</span><span class="sxs-lookup"><span data-stu-id="86613-917">variable: Represents hello subexpression.</span></span>
* <span data-ttu-id="86613-918">subExpression: a subexpressão representada pela variável.</span><span class="sxs-lookup"><span data-stu-id="86613-918">subExpression: subexpression represented by variable.</span></span>
* <span data-ttu-id="86613-919">complexExpression: uma expressão complexa.</span><span class="sxs-lookup"><span data-stu-id="86613-919">complexExpression: A complex expression.</span></span>

<span data-ttu-id="86613-920">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-920">**Example:**</span></span>  
`With($unExpiredCerts,Where($item,[userCertificate],CertNotAfter($item)>Now()),IIF(Count($unExpiredCerts)>0,$unExpiredCerts,NULL))`  
<span data-ttu-id="86613-921">É funcionalmente equivalente à:</span><span class="sxs-lookup"><span data-stu-id="86613-921">Is functionally equivalent to:</span></span>  
`IIF (Count(Where($item,[userCertificate],CertNotAfter($item)>Now()))>0, Where($item,[userCertificate],CertNotAfter($item)>Now()),NULL)`  
<span data-ttu-id="86613-922">Que retorna apenas os valores de certificado não expirados no atributo de userCertificate hello.</span><span class="sxs-lookup"><span data-stu-id="86613-922">Which returns only unexpired certificate values in hello userCertificate attribute.</span></span>


- - -
### <a name="word"></a><span data-ttu-id="86613-923">Word</span><span class="sxs-lookup"><span data-stu-id="86613-923">Word</span></span>
<span data-ttu-id="86613-924">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="86613-924">**Description:**</span></span>  
<span data-ttu-id="86613-925">Olá função Word retorna uma palavra contida em uma cadeia de caracteres, com base nos parâmetros que descrevem Olá delimitadores toouse e hello word número tooreturn.</span><span class="sxs-lookup"><span data-stu-id="86613-925">hello Word function returns a word contained within a string, based on parameters describing hello delimiters toouse and hello word number tooreturn.</span></span>

<span data-ttu-id="86613-926">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="86613-926">**Syntax:**</span></span>  
`str Word(str string, num WordNumber, str delimiters)`

* <span data-ttu-id="86613-927">cadeia de caracteres: Olá tooreturn de cadeia de caracteres de uma palavra.</span><span class="sxs-lookup"><span data-stu-id="86613-927">string: hello string tooreturn a word from.</span></span>
* <span data-ttu-id="86613-928">WordNumber: um número que identifica qual número de palavras deve retornar.</span><span class="sxs-lookup"><span data-stu-id="86613-928">WordNumber: a number identifying which word number should return.</span></span>
* <span data-ttu-id="86613-929">delimitadores: uma cadeia de caracteres que representa a saudação delimiter(s) que deve ser usado tooidentify palavras</span><span class="sxs-lookup"><span data-stu-id="86613-929">delimiters: a string representing hello delimiter(s) that should be used tooidentify words</span></span>

<span data-ttu-id="86613-930">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="86613-930">**Remarks:**</span></span>  
<span data-ttu-id="86613-931">Cada cadeia de caracteres na cadeia de caracteres separados por Olá um Olá caracteres delimitadores são identificados como palavras:</span><span class="sxs-lookup"><span data-stu-id="86613-931">Each string of characters in string separated by hello one of hello characters in delimiters are identified as words:</span></span>

* <span data-ttu-id="86613-932">Se number < 1, retorna uma cadeia de caracteres vazia.</span><span class="sxs-lookup"><span data-stu-id="86613-932">If number < 1, returns empty string.</span></span>
* <span data-ttu-id="86613-933">Se a cadeia de caracteres for nula, retorna a cadeia de caracteres vazia.</span><span class="sxs-lookup"><span data-stu-id="86613-933">If string is null, returns empty string.</span></span>

<span data-ttu-id="86613-934">Se a cadeia de caracteres for menor que o número de palavras ou a cadeia não contiver nenhuma palavra identificada por delimitadores, uma cadeia de caracteres vazia será retornada.</span><span class="sxs-lookup"><span data-stu-id="86613-934">If string contains less than number words, or string does not contain any words identified by delimiters, an empty string is returned.</span></span>

<span data-ttu-id="86613-935">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="86613-935">**Example:**</span></span>  
`Word("hello quick brown fox",3," ")`  
<span data-ttu-id="86613-936">retorna "brown"</span><span class="sxs-lookup"><span data-stu-id="86613-936">Returns "brown"</span></span>

`Word("This,string!has&many separators",3,",!&#")`  
<span data-ttu-id="86613-937">retornaria "has"</span><span class="sxs-lookup"><span data-stu-id="86613-937">Would return "has"</span></span>

## <a name="additional-resources"></a><span data-ttu-id="86613-938">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="86613-938">Additional Resources</span></span>
* [<span data-ttu-id="86613-939">Noções básicas sobre expressões de provisionamento declarativo</span><span class="sxs-lookup"><span data-stu-id="86613-939">Understanding Declarative Provisioning Expressions</span></span>](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)
* [<span data-ttu-id="86613-940">Azure AD Connect Sync: personalizando opções de sincronização</span><span class="sxs-lookup"><span data-stu-id="86613-940">Azure AD Connect Sync: Customizing Synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="86613-941">Integração de suas identidades locais com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="86613-941">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
