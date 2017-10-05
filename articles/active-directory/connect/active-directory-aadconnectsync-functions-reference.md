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
ms.openlocfilehash: 926f52ef64eb79205dbfb344edc7d9bece2a6947
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-functions-reference"></a><span data-ttu-id="5a3e9-103">Azure AD Connect Sync: referência de funções</span><span class="sxs-lookup"><span data-stu-id="5a3e9-103">Azure AD Connect sync: Functions Reference</span></span>
<span data-ttu-id="5a3e9-104">No Azure Active Directory Sync, as funções são usadas para manipular um valor de atributo durante a sincronização.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-104">In Azure AD Connect, functions are used to manipulate an attribute value during synchronization.</span></span>  
<span data-ttu-id="5a3e9-105">A sintaxe das funções é expressa usando o seguinte formato: </span><span class="sxs-lookup"><span data-stu-id="5a3e9-105">The Syntax of the functions is expressed using the following format:</span></span>  
`<output type> FunctionName(<input type> <position name>, ..)`

<span data-ttu-id="5a3e9-106">Se uma função está sobrecarregada e aceita diversas sintaxes, todas as sintaxes válidas são listadas.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-106">If a function is overloaded and accepts multiple syntaxes, all valid syntaxes are listed.</span></span>  
<span data-ttu-id="5a3e9-107">As funções são fortemente tipadas e verificam que o tipo passado corresponde ao tipo documentado.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-107">The functions are strongly typed and they verify that the type passed in matches the documented type.</span></span>  
<span data-ttu-id="5a3e9-108">Se o tipo não corresponder, um erro será gerado.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-108">If the type does not match, an error is thrown.</span></span>

<span data-ttu-id="5a3e9-109">Os tipos são expressos com a seguinte sintaxe:</span><span class="sxs-lookup"><span data-stu-id="5a3e9-109">The types are expressed with the following syntax:</span></span>

* <span data-ttu-id="5a3e9-110">**bin** - binário</span><span class="sxs-lookup"><span data-stu-id="5a3e9-110">**bin** – Binary</span></span>
* <span data-ttu-id="5a3e9-111">**bool** - booliano</span><span class="sxs-lookup"><span data-stu-id="5a3e9-111">**bool** – Boolean</span></span>
* <span data-ttu-id="5a3e9-112">**dt** - data/hora UTC</span><span class="sxs-lookup"><span data-stu-id="5a3e9-112">**dt** – UTC Date/Time</span></span>
* <span data-ttu-id="5a3e9-113">**enum** - enumeração das constantes conhecidas</span><span class="sxs-lookup"><span data-stu-id="5a3e9-113">**enum** – Enumeration of known constants</span></span>
* <span data-ttu-id="5a3e9-114">**exp** - expressão, que espera-se que seja avaliada como um valor Booliano</span><span class="sxs-lookup"><span data-stu-id="5a3e9-114">**exp** – Expression, which is expected to evaluate to a Boolean</span></span>
* <span data-ttu-id="5a3e9-115">**mvbin** - Binário de Valores Múltiplos</span><span class="sxs-lookup"><span data-stu-id="5a3e9-115">**mvbin** – Multi-Valued Binary</span></span>
* <span data-ttu-id="5a3e9-116">**mvstr** - Cadeia de Caracteres de Valores Múltiplos</span><span class="sxs-lookup"><span data-stu-id="5a3e9-116">**mvstr** – Multi-Valued String</span></span>
* <span data-ttu-id="5a3e9-117">**mvstr** - Referência de Valores Múltiplos</span><span class="sxs-lookup"><span data-stu-id="5a3e9-117">**mvref** – Multi-Valued Reference</span></span>
* <span data-ttu-id="5a3e9-118">**num** - numérico</span><span class="sxs-lookup"><span data-stu-id="5a3e9-118">**num** – Numeric</span></span>
* <span data-ttu-id="5a3e9-119">**ref** – Referência</span><span class="sxs-lookup"><span data-stu-id="5a3e9-119">**ref** – Reference</span></span>
* <span data-ttu-id="5a3e9-120">**str** – Cadeia de Caracteres</span><span class="sxs-lookup"><span data-stu-id="5a3e9-120">**str** – String</span></span>
* <span data-ttu-id="5a3e9-121">**var** - uma variante de (quase) qualquer outro tipo</span><span class="sxs-lookup"><span data-stu-id="5a3e9-121">**var** – A variant of (almost) any other type</span></span>
* <span data-ttu-id="5a3e9-122">**void** - não retorna um valor</span><span class="sxs-lookup"><span data-stu-id="5a3e9-122">**void** – doesn’t return a value</span></span>

<span data-ttu-id="5a3e9-123">As funções com os tipos **mvbin**, **mvstr** e **mvref** funcionam somente nos atributos de valores múltiplos.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-123">The functions with the types **mvbin**, **mvstr**, and **mvref** can only work on multi-valued attributes.</span></span> <span data-ttu-id="5a3e9-124">As funções com **bin**, **str** e **ref** funcionam nos atributos de valor único e valores múltiplos.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-124">Functions with **bin**, **str**, and **ref** work on both single-valued and multi-valued attributes.</span></span>

## <a name="functions-reference"></a><span data-ttu-id="5a3e9-125">Referência de funções</span><span class="sxs-lookup"><span data-stu-id="5a3e9-125">Functions Reference</span></span>
| <span data-ttu-id="5a3e9-126">Lista de funções</span><span class="sxs-lookup"><span data-stu-id="5a3e9-126">List of functions</span></span> |  |  |  |  |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="5a3e9-127">**Certificate**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-127">**Certificate**</span></span> | | | | |
| [<span data-ttu-id="5a3e9-128">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="5a3e9-128">CertExtensionOids</span></span>](#certextensionoids) |[<span data-ttu-id="5a3e9-129">CertFormat</span><span class="sxs-lookup"><span data-stu-id="5a3e9-129">CertFormat</span></span>](#certformat) |[<span data-ttu-id="5a3e9-130">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="5a3e9-130">CertFriendlyName</span></span>](#certfriendlyname) |[<span data-ttu-id="5a3e9-131">CertHashString</span><span class="sxs-lookup"><span data-stu-id="5a3e9-131">CertHashString</span></span>](#certhashstring) | |
| [<span data-ttu-id="5a3e9-132">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="5a3e9-132">CertIssuer</span></span>](#certissuer) |[<span data-ttu-id="5a3e9-133">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="5a3e9-133">CertIssuerDN</span></span>](#certissuerdn) |[<span data-ttu-id="5a3e9-134">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="5a3e9-134">CertIssuerOid</span></span>](#certissueroid) |[<span data-ttu-id="5a3e9-135">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="5a3e9-135">CertKeyAlgorithm</span></span>](#certkeyalgorithm) | |
| [<span data-ttu-id="5a3e9-136">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="5a3e9-136">CertKeyAlgorithmParams</span></span>](#certkeyalgorithmparams) |[<span data-ttu-id="5a3e9-137">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="5a3e9-137">CertNameInfo</span></span>](#certnameinfo) |[<span data-ttu-id="5a3e9-138">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="5a3e9-138">CertNotAfter</span></span>](#certnotafter) |[<span data-ttu-id="5a3e9-139">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="5a3e9-139">CertNotBefore</span></span>](#certnotbefore) | |
| [<span data-ttu-id="5a3e9-140">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="5a3e9-140">CertPublicKeyOid</span></span>](#certpublickeyoid) |[<span data-ttu-id="5a3e9-141">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="5a3e9-141">CertPublicKeyParametersOid</span></span>](#certpublickeyparametersoid) |[<span data-ttu-id="5a3e9-142">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="5a3e9-142">CertSerialNumber</span></span>](#certserialnumber) |[<span data-ttu-id="5a3e9-143">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="5a3e9-143">CertSignatureAlgorithmOid</span></span>](#certsignaturealgorithmoid) | |
| [<span data-ttu-id="5a3e9-144">CertSubject</span><span class="sxs-lookup"><span data-stu-id="5a3e9-144">CertSubject</span></span>](#certsubject) |[<span data-ttu-id="5a3e9-145">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="5a3e9-145">CertSubjectNameDN</span></span>](#certsubjectnamedn) |[<span data-ttu-id="5a3e9-146">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="5a3e9-146">CertSubjectNameOid</span></span>](#certsubjectnameoid) |[<span data-ttu-id="5a3e9-147">CertThumbprint</span><span class="sxs-lookup"><span data-stu-id="5a3e9-147">CertThumbprint</span></span>](#certthumbprint) | |
[<span data-ttu-id="5a3e9-148"> CertVersion</span><span class="sxs-lookup"><span data-stu-id="5a3e9-148"> CertVersion</span></span>](#certversion) |[<span data-ttu-id="5a3e9-149">IsCert</span><span class="sxs-lookup"><span data-stu-id="5a3e9-149">IsCert</span></span>](#iscert) | | | |
| <span data-ttu-id="5a3e9-150">**Conversão**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-150">**Conversion**</span></span> | | | | |
| [<span data-ttu-id="5a3e9-151">CBool</span><span class="sxs-lookup"><span data-stu-id="5a3e9-151">CBool</span></span>](#cbool) |[<span data-ttu-id="5a3e9-152">CDate</span><span class="sxs-lookup"><span data-stu-id="5a3e9-152">CDate</span></span>](#cdate) |[<span data-ttu-id="5a3e9-153">CGuid</span><span class="sxs-lookup"><span data-stu-id="5a3e9-153">CGuid</span></span>](#cguid) |[<span data-ttu-id="5a3e9-154">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="5a3e9-154">ConvertFromBase64</span></span>](#convertfrombase64) | |
| [<span data-ttu-id="5a3e9-155">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="5a3e9-155">ConvertToBase64</span></span>](#converttobase64) |[<span data-ttu-id="5a3e9-156">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="5a3e9-156">ConvertFromUTF8Hex</span></span>](#convertfromutf8hex) |[<span data-ttu-id="5a3e9-157">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="5a3e9-157">ConvertToUTF8Hex</span></span>](#converttoutf8hex) |[<span data-ttu-id="5a3e9-158">CNum</span><span class="sxs-lookup"><span data-stu-id="5a3e9-158">CNum</span></span>](#cnum) | |
| [<span data-ttu-id="5a3e9-159">CRef</span><span class="sxs-lookup"><span data-stu-id="5a3e9-159">CRef</span></span>](#cref) |[<span data-ttu-id="5a3e9-160">CStr</span><span class="sxs-lookup"><span data-stu-id="5a3e9-160">CStr</span></span>](#cstr) |[<span data-ttu-id="5a3e9-161">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="5a3e9-161">StringFromGuid</span></span>](#StringFromGuid) |[<span data-ttu-id="5a3e9-162">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="5a3e9-162">StringFromSid</span></span>](#stringfromsid) | |
| <span data-ttu-id="5a3e9-163">**Data / hora**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-163">**Date / Time**</span></span> | | | | |
| [<span data-ttu-id="5a3e9-164">DateAdd</span><span class="sxs-lookup"><span data-stu-id="5a3e9-164">DateAdd</span></span>](#dateadd) |[<span data-ttu-id="5a3e9-165">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="5a3e9-165">DateFromNum</span></span>](#datefromnum) |[<span data-ttu-id="5a3e9-166">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="5a3e9-166">FormatDateTime</span></span>](#formatdatetime) |[<span data-ttu-id="5a3e9-167">Now</span><span class="sxs-lookup"><span data-stu-id="5a3e9-167">Now</span></span>](#now) | |
| [<span data-ttu-id="5a3e9-168">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="5a3e9-168">NumFromDate</span></span>](#numfromdate) | | | | |
| <span data-ttu-id="5a3e9-169">**Diretório**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-169">**Directory**</span></span> | | | | |
| [<span data-ttu-id="5a3e9-170">DNComponent</span><span class="sxs-lookup"><span data-stu-id="5a3e9-170">DNComponent</span></span>](#dncomponent) |[<span data-ttu-id="5a3e9-171">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="5a3e9-171">DNComponentRev</span></span>](#dncomponentrev) |[<span data-ttu-id="5a3e9-172">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="5a3e9-172">EscapeDNComponent</span></span>](#escapedncomponent) | | |
| <span data-ttu-id="5a3e9-173">**Avaliação**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-173">**Evaluation**</span></span> | | | | |
| [<span data-ttu-id="5a3e9-174">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="5a3e9-174">IsBitSet</span></span>](#isbitset) |[<span data-ttu-id="5a3e9-175">IsDate</span><span class="sxs-lookup"><span data-stu-id="5a3e9-175">IsDate</span></span>](#isdate) |[<span data-ttu-id="5a3e9-176">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="5a3e9-176">IsEmpty</span></span>](#isempty) |[<span data-ttu-id="5a3e9-177">IsGuid</span><span class="sxs-lookup"><span data-stu-id="5a3e9-177">IsGuid</span></span>](#isguid) | |
| [<span data-ttu-id="5a3e9-178">IsNull</span><span class="sxs-lookup"><span data-stu-id="5a3e9-178">IsNull</span></span>](#isnull) |[<span data-ttu-id="5a3e9-179">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="5a3e9-179">IsNullOrEmpty</span></span>](#isnullorempty) |[<span data-ttu-id="5a3e9-180">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="5a3e9-180">IsNumeric</span></span>](#isnumeric) |[<span data-ttu-id="5a3e9-181">IsPresent</span><span class="sxs-lookup"><span data-stu-id="5a3e9-181">IsPresent</span></span>](#ispresent) | |
| [<span data-ttu-id="5a3e9-182">IsString</span><span class="sxs-lookup"><span data-stu-id="5a3e9-182">IsString</span></span>](#isstring) | | | | |
| <span data-ttu-id="5a3e9-183">**Matemática**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-183">**Math**</span></span> | | | | |
| [<span data-ttu-id="5a3e9-184">BitAnd</span><span class="sxs-lookup"><span data-stu-id="5a3e9-184">BitAnd</span></span>](#bitand) |[<span data-ttu-id="5a3e9-185">BitOr</span><span class="sxs-lookup"><span data-stu-id="5a3e9-185">BitOr</span></span>](#bitor) |[<span data-ttu-id="5a3e9-186">RandomNum</span><span class="sxs-lookup"><span data-stu-id="5a3e9-186">RandomNum</span></span>](#randomnum) | | |
| <span data-ttu-id="5a3e9-187">**De valores múltiplos**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-187">**Multi-valued**</span></span> | | | | |
| [<span data-ttu-id="5a3e9-188">Contém:</span><span class="sxs-lookup"><span data-stu-id="5a3e9-188">Contains</span></span>](#contains) |[<span data-ttu-id="5a3e9-189">Contagem</span><span class="sxs-lookup"><span data-stu-id="5a3e9-189">Count</span></span>](#count) |[<span data-ttu-id="5a3e9-190">Item</span><span class="sxs-lookup"><span data-stu-id="5a3e9-190">Item</span></span>](#item) |[<span data-ttu-id="5a3e9-191">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="5a3e9-191">ItemOrNull</span></span>](#itemornull) | |
| [<span data-ttu-id="5a3e9-192">Join</span><span class="sxs-lookup"><span data-stu-id="5a3e9-192">Join</span></span>](#join) |[<span data-ttu-id="5a3e9-193">RemoveDuplicates</span><span class="sxs-lookup"><span data-stu-id="5a3e9-193">RemoveDuplicates</span></span>](#removeduplicates) |[<span data-ttu-id="5a3e9-194">Divisão</span><span class="sxs-lookup"><span data-stu-id="5a3e9-194">Split</span></span>](#split) | | |
| <span data-ttu-id="5a3e9-195">**Fluxo do Programa**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-195">**Program Flow**</span></span> | | | | |
| [<span data-ttu-id="5a3e9-196">Erro</span><span class="sxs-lookup"><span data-stu-id="5a3e9-196">Error</span></span>](#error) |[<span data-ttu-id="5a3e9-197">IIF</span><span class="sxs-lookup"><span data-stu-id="5a3e9-197">IIF</span></span>](#iif) |[<span data-ttu-id="5a3e9-198">Seleção</span><span class="sxs-lookup"><span data-stu-id="5a3e9-198">Select</span></span>](#select) |[<span data-ttu-id="5a3e9-199">Switch</span><span class="sxs-lookup"><span data-stu-id="5a3e9-199">Switch</span></span>](#switch) | |
| [<span data-ttu-id="5a3e9-200">Onde</span><span class="sxs-lookup"><span data-stu-id="5a3e9-200">Where</span></span>](#where) |[<span data-ttu-id="5a3e9-201">With</span><span class="sxs-lookup"><span data-stu-id="5a3e9-201">With</span></span>](#with) | | | |
| <span data-ttu-id="5a3e9-202">**Texto**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-202">**Text**</span></span> | | | | |
| [<span data-ttu-id="5a3e9-203">GUID</span><span class="sxs-lookup"><span data-stu-id="5a3e9-203">GUID</span></span>](#guid) |[<span data-ttu-id="5a3e9-204">InStr</span><span class="sxs-lookup"><span data-stu-id="5a3e9-204">InStr</span></span>](#instr) |[<span data-ttu-id="5a3e9-205">InStrRev</span><span class="sxs-lookup"><span data-stu-id="5a3e9-205">InStrRev</span></span>](#instrrev) |[<span data-ttu-id="5a3e9-206">LCase</span><span class="sxs-lookup"><span data-stu-id="5a3e9-206">LCase</span></span>](#lcase) | |
| [<span data-ttu-id="5a3e9-207">Left</span><span class="sxs-lookup"><span data-stu-id="5a3e9-207">Left</span></span>](#left) |[<span data-ttu-id="5a3e9-208">Len</span><span class="sxs-lookup"><span data-stu-id="5a3e9-208">Len</span></span>](#len) |[<span data-ttu-id="5a3e9-209">LTrim</span><span class="sxs-lookup"><span data-stu-id="5a3e9-209">LTrim</span></span>](#ltrim) |[<span data-ttu-id="5a3e9-210">Mid</span><span class="sxs-lookup"><span data-stu-id="5a3e9-210">Mid</span></span>](#mid) | |
| [<span data-ttu-id="5a3e9-211">PadLeft</span><span class="sxs-lookup"><span data-stu-id="5a3e9-211">PadLeft</span></span>](#padleft) |[<span data-ttu-id="5a3e9-212">PadRight</span><span class="sxs-lookup"><span data-stu-id="5a3e9-212">PadRight</span></span>](#padright) |[<span data-ttu-id="5a3e9-213">PCase</span><span class="sxs-lookup"><span data-stu-id="5a3e9-213">PCase</span></span>](#pcase) |[<span data-ttu-id="5a3e9-214">Substitua</span><span class="sxs-lookup"><span data-stu-id="5a3e9-214">Replace</span></span>](#replace) | |
| [<span data-ttu-id="5a3e9-215">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="5a3e9-215">ReplaceChars</span></span>](#replacechars) |[<span data-ttu-id="5a3e9-216">Right</span><span class="sxs-lookup"><span data-stu-id="5a3e9-216">Right</span></span>](#right) |[<span data-ttu-id="5a3e9-217">RTrim</span><span class="sxs-lookup"><span data-stu-id="5a3e9-217">RTrim</span></span>](#rtrim) |[<span data-ttu-id="5a3e9-218">Trim</span><span class="sxs-lookup"><span data-stu-id="5a3e9-218">Trim</span></span>](#trim) | |
| [<span data-ttu-id="5a3e9-219">UCase</span><span class="sxs-lookup"><span data-stu-id="5a3e9-219">UCase</span></span>](#ucase) |[<span data-ttu-id="5a3e9-220">Word</span><span class="sxs-lookup"><span data-stu-id="5a3e9-220">Word</span></span>](#word) | | | |

- - -
### <a name="bitand"></a><span data-ttu-id="5a3e9-221">BitAnd</span><span class="sxs-lookup"><span data-stu-id="5a3e9-221">BitAnd</span></span>
<span data-ttu-id="5a3e9-222">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-222">**Description:**</span></span>  
<span data-ttu-id="5a3e9-223">a função BitAnd define os bits especificados em um valor.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-223">The BitAnd function sets specified bits on a value.</span></span>

<span data-ttu-id="5a3e9-224">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-224">**Syntax:**</span></span>  
`num BitAnd(num value1, num value2)`

* <span data-ttu-id="5a3e9-225">value1, value2: os valores numéricos que devem ser agrupados com AND</span><span class="sxs-lookup"><span data-stu-id="5a3e9-225">value1, value2: numeric values that should be AND’ed together</span></span>

<span data-ttu-id="5a3e9-226">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-226">**Remarks:**</span></span>  
<span data-ttu-id="5a3e9-227">esta função converte ambos os parâmetros na representação binária e define um bit para:</span><span class="sxs-lookup"><span data-stu-id="5a3e9-227">This function converts both parameters to the binary representation and sets a bit to:</span></span>

* <span data-ttu-id="5a3e9-228">0 - se um ou ambos os bits correspondentes na *máscara* e no *sinalizador* forem 0</span><span class="sxs-lookup"><span data-stu-id="5a3e9-228">0 - if one or both of the corresponding bits in *mask* and *flag* are 0</span></span>
* <span data-ttu-id="5a3e9-229">1 - se ambos os bits correspondentes são 1.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-229">1 - if both of the corresponding bits are 1.</span></span>

<span data-ttu-id="5a3e9-230">Em outras palavras, ele retorna 0 em todos os casos, exceto quando os bits correspondentes de ambos os parâmetros são 1.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-230">In other words, it returns 0 in all cases except when the corresponding bits of both parameters are 1.</span></span>

<span data-ttu-id="5a3e9-231">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-231">**Example:**</span></span>  
`BitAnd(&HF, &HF7)`  
<span data-ttu-id="5a3e9-232">Retorna 7, já que os hexadecimais "F" AND "F7" são avaliados como esse valor.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-232">Returns 7 because hexadecimal "F" AND "F7" evaluate to this value.</span></span>

- - -
### <a name="bitor"></a><span data-ttu-id="5a3e9-233">BitOr</span><span class="sxs-lookup"><span data-stu-id="5a3e9-233">BitOr</span></span>
<span data-ttu-id="5a3e9-234">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-234">**Description:**</span></span>  
<span data-ttu-id="5a3e9-235">a função BitOr define os bits especificados em um valor.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-235">The BitOr function sets specified bits on a value.</span></span>

<span data-ttu-id="5a3e9-236">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-236">**Syntax:**</span></span>  
`num BitOr(num value1, num value2)`

* <span data-ttu-id="5a3e9-237">value1, value2: valores numéricos que devem ser agrupados com OR</span><span class="sxs-lookup"><span data-stu-id="5a3e9-237">value1, value2: numeric values that should be OR’ed together</span></span>

<span data-ttu-id="5a3e9-238">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-238">**Remarks:**</span></span>  
<span data-ttu-id="5a3e9-239">esta função converte ambos os parâmetros na representação binária e define um bit para 1 se um ou ambos os bits correspondentes na máscara e no sinalizador são 1; e para 0 se ambos os bits correspondentes são 0.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-239">This function converts both parameters to the binary representation and sets a bit to 1 if one or both of the corresponding bits in mask and flag are 1, and to 0 if both of the corresponding bits are 0.</span></span> <span data-ttu-id="5a3e9-240">Em outras palavras, ele retorna 1 em todos os casos, exceto naqueles em que os bits correspondentes de ambos os parâmetros são 0.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-240">In other words, it returns 1 in all cases except where the corresponding bits of both parameters are 0.</span></span>

- - -
### <a name="cbool"></a><span data-ttu-id="5a3e9-241">CBool</span><span class="sxs-lookup"><span data-stu-id="5a3e9-241">CBool</span></span>
<span data-ttu-id="5a3e9-242">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-242">**Description:**</span></span>  
<span data-ttu-id="5a3e9-243">a função CBool retorna um valor booliano com base na expressão avaliada</span><span class="sxs-lookup"><span data-stu-id="5a3e9-243">The CBool function returns a Boolean based on the evaluated expression</span></span>

<span data-ttu-id="5a3e9-244">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-244">**Syntax:**</span></span>  
`bool CBool(exp Expression)`

<span data-ttu-id="5a3e9-245">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-245">**Remarks:**</span></span>  
<span data-ttu-id="5a3e9-246">se a expressão é avaliada como um valor diferente de zero, CBool retorna True; caso contrário, retorna False.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-246">If the expression evaluates to a nonzero value, then CBool returns True, else it returns False.</span></span>

<span data-ttu-id="5a3e9-247">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-247">**Example:**</span></span>  
`CBool([attrib1] = [attrib2])`  

<span data-ttu-id="5a3e9-248">Retorna True se ambos os atributos têm o mesmo valor.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-248">Returns True if both attributes have the same value.</span></span>

- - -
### <a name="cdate"></a><span data-ttu-id="5a3e9-249">CDate</span><span class="sxs-lookup"><span data-stu-id="5a3e9-249">CDate</span></span>
<span data-ttu-id="5a3e9-250">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-250">**Description:**</span></span>  
<span data-ttu-id="5a3e9-251">a função CDate retorna um DateTime UTC a partir de uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-251">The CDate function returns a UTC DateTime from a string.</span></span> <span data-ttu-id="5a3e9-252">DateTime não é um tipo de atributo nativo no Sync, mas é usado por algumas funções.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-252">DateTime is not a native attribute type in Sync but is used by some functions.</span></span>

<span data-ttu-id="5a3e9-253">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-253">**Syntax:**</span></span>  
`dt CDate(str value)`

* <span data-ttu-id="5a3e9-254">Value: uma cadeia de caracteres com uma data, hora e opcionalmente um fuso horário</span><span class="sxs-lookup"><span data-stu-id="5a3e9-254">Value: A string with a date, time, and optionally time zone</span></span>

<span data-ttu-id="5a3e9-255">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-255">**Remarks:**</span></span>  
<span data-ttu-id="5a3e9-256">a cadeia de caracteres retornada é sempre em UTC.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-256">The returned string is always in UTC.</span></span>

<span data-ttu-id="5a3e9-257">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-257">**Example:**</span></span>  
`CDate([employeeStartTime])`  
<span data-ttu-id="5a3e9-258">retorna um DateTime com base na hora de início do funcionário</span><span class="sxs-lookup"><span data-stu-id="5a3e9-258">Returns a DateTime based on the employee’s start time</span></span>

`CDate("2013-01-10 4:00 PM -8")`  
<span data-ttu-id="5a3e9-259">Retorna um DateTime que representa "11/01/2013 12:00"</span><span class="sxs-lookup"><span data-stu-id="5a3e9-259">Returns a DateTime representing "2013-01-11 12:00 AM"</span></span>








- - -
### <a name="certextensionoids"></a><span data-ttu-id="5a3e9-260">CertExtensionOids</span><span class="sxs-lookup"><span data-stu-id="5a3e9-260">CertExtensionOids</span></span>
<span data-ttu-id="5a3e9-261">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-261">**Description:**</span></span>  
<span data-ttu-id="5a3e9-262">Retorna os valores de OID de todas as extensões críticas de um objeto de certificado.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-262">Returns the Oid values of all the critical extensions of a certificate object.</span></span>

<span data-ttu-id="5a3e9-263">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-263">**Syntax:**</span></span>  
`mvstr CertExtensionOids(binary certificateRawData)`  
*   <span data-ttu-id="5a3e9-264">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-264">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5a3e9-265">A matriz de bytes pode ser codificada binária (DER) ou de dados X.509 codificados em Base64.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-265">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certformat"></a><span data-ttu-id="5a3e9-266">CertFormat</span><span class="sxs-lookup"><span data-stu-id="5a3e9-266">CertFormat</span></span>
<span data-ttu-id="5a3e9-267">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-267">**Description:**</span></span>  
<span data-ttu-id="5a3e9-268">Retorna o nome do formato desse certificado X.509v3.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-268">Returns the name of the format of this X.509v3 certificate.</span></span>

<span data-ttu-id="5a3e9-269">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-269">**Syntax:**</span></span>  
`str CertFormat(binary certificateRawData)`  
*   <span data-ttu-id="5a3e9-270">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-270">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5a3e9-271">A matriz de bytes pode ser codificada binária (DER) ou de dados X.509 codificados em Base64.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-271">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certfriendlyname"></a><span data-ttu-id="5a3e9-272">CertFriendlyName</span><span class="sxs-lookup"><span data-stu-id="5a3e9-272">CertFriendlyName</span></span>
<span data-ttu-id="5a3e9-273">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-273">**Description:**</span></span>  
<span data-ttu-id="5a3e9-274">Retorna o alias associado de um certificado.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-274">Returns the associated alias for a certificate.</span></span>

<span data-ttu-id="5a3e9-275">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-275">**Syntax:**</span></span>  
`str CertFriendlyName(binary certificateRawData)`  
*   <span data-ttu-id="5a3e9-276">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-276">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5a3e9-277">A matriz de bytes pode ser codificada binária (DER) ou de dados X.509 codificados em Base64.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-277">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certhashstring"></a><span data-ttu-id="5a3e9-278">CertHashString</span><span class="sxs-lookup"><span data-stu-id="5a3e9-278">CertHashString</span></span>
<span data-ttu-id="5a3e9-279">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-279">**Description:**</span></span>  
<span data-ttu-id="5a3e9-280">Retorna o valor de hash SHA1 do certificado X.509v3 como uma cadeia de caracteres hexadecimal.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-280">Returns the SHA1 hash value for the X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="5a3e9-281">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-281">**Syntax:**</span></span>  
`str CertHashString(binary certificateRawData)`  
*   <span data-ttu-id="5a3e9-282">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-282">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5a3e9-283">A matriz de bytes pode ser codificada binária (DER) ou de dados X.509 codificados em Base64.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-283">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuer"></a><span data-ttu-id="5a3e9-284">CertIssuer</span><span class="sxs-lookup"><span data-stu-id="5a3e9-284">CertIssuer</span></span>
<span data-ttu-id="5a3e9-285">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-285">**Description:**</span></span>  
<span data-ttu-id="5a3e9-286">Retorna o nome da autoridade de certificação que emitiu o certificado X.509v3.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-286">Returns the name of the certificate authority that issued the X.509v3 certificate.</span></span>

<span data-ttu-id="5a3e9-287">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-287">**Syntax:**</span></span>  
`str CertIssuer(binary certificateRawData)`  
*   <span data-ttu-id="5a3e9-288">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-288">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5a3e9-289">A matriz de bytes pode ser codificada binária (DER) ou de dados X.509 codificados em Base64.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-289">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissuerdn"></a><span data-ttu-id="5a3e9-290">CertIssuerDN</span><span class="sxs-lookup"><span data-stu-id="5a3e9-290">CertIssuerDN</span></span>
<span data-ttu-id="5a3e9-291">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-291">**Description:**</span></span>  
<span data-ttu-id="5a3e9-292">Retorna o nome diferenciado do emissor do certificado.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-292">Returns the distinguished name of the certificate issuer.</span></span>

<span data-ttu-id="5a3e9-293">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-293">**Syntax:**</span></span>  
`str CertIssuerDN(binary certificateRawData)`  
*   <span data-ttu-id="5a3e9-294">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-294">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5a3e9-295">A matriz de bytes pode ser codificada binária (DER) ou de dados X.509 codificados em Base64.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-295">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certissueroid"></a><span data-ttu-id="5a3e9-296">CertIssuerOid</span><span class="sxs-lookup"><span data-stu-id="5a3e9-296">CertIssuerOid</span></span>
<span data-ttu-id="5a3e9-297">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-297">**Description:**</span></span>  
<span data-ttu-id="5a3e9-298">Retorna o OID do emissor do certificado.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-298">Returns the Oid of the certificate issuer.</span></span>

<span data-ttu-id="5a3e9-299">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-299">**Syntax:**</span></span>  
`str CertIssuerOid(binary certificateRawData)`  
*   <span data-ttu-id="5a3e9-300">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-300">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5a3e9-301">A matriz de bytes pode ser codificada binária (DER) ou de dados X.509 codificados em Base64.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-301">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithm"></a><span data-ttu-id="5a3e9-302">CertKeyAlgorithm</span><span class="sxs-lookup"><span data-stu-id="5a3e9-302">CertKeyAlgorithm</span></span>
<span data-ttu-id="5a3e9-303">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-303">**Description:**</span></span>  
<span data-ttu-id="5a3e9-304">Retorna as informações de algoritmo de chave do certificado X.509v3 como uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-304">Returns the key algorithm information for this X.509v3 certificate as a string.</span></span>

<span data-ttu-id="5a3e9-305">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-305">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="5a3e9-306">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-306">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5a3e9-307">A matriz de bytes pode ser codificada binária (DER) ou de dados X.509 codificados em Base64.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-307">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certkeyalgorithmparams"></a><span data-ttu-id="5a3e9-308">CertKeyAlgorithmParams</span><span class="sxs-lookup"><span data-stu-id="5a3e9-308">CertKeyAlgorithmParams</span></span>
<span data-ttu-id="5a3e9-309">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-309">**Description:**</span></span>  
<span data-ttu-id="5a3e9-310">Retorna os parâmetros de algoritmo de chave do certificado X.509v3 como uma cadeia de caracteres hexadecimal.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-310">Returns the key algorithm parameters for the X.509v3 certificate as a hexadecimal string.</span></span>

<span data-ttu-id="5a3e9-311">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-311">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="5a3e9-312">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-312">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5a3e9-313">A matriz de bytes pode ser codificada binária (DER) ou de dados X.509 codificados em Base64.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-313">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnameinfo"></a><span data-ttu-id="5a3e9-314">CertNameInfo</span><span class="sxs-lookup"><span data-stu-id="5a3e9-314">CertNameInfo</span></span>
<span data-ttu-id="5a3e9-315">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-315">**Description:**</span></span>  
<span data-ttu-id="5a3e9-316">Retorna os nomes de entidade e emissor de um certificado.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-316">Returns the subject and issuer names from a certificate.</span></span>

<span data-ttu-id="5a3e9-317">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-317">**Syntax:**</span></span>  
`str CertNameInfo(binary certificateRawData, str x509NameType, bool includesIssuerName)`  
*   <span data-ttu-id="5a3e9-318">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-318">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5a3e9-319">A matriz de bytes pode ser codificada binária (DER) ou de dados X.509 codificados em Base64.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-319">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
*   <span data-ttu-id="5a3e9-320">X509NameType: o valor de X509NameType para a entidade.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-320">X509NameType: The X509NameType value for the subject.</span></span>
*   <span data-ttu-id="5a3e9-321">includesIssuerName: verdadeiro para incluir o nome do emissor; caso contrário, falso.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-321">includesIssuerName: true to include the issuer name; otherwise, false.</span></span>

- - -
### <a name="certnotafter"></a><span data-ttu-id="5a3e9-322">CertNotAfter</span><span class="sxs-lookup"><span data-stu-id="5a3e9-322">CertNotAfter</span></span>
<span data-ttu-id="5a3e9-323">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-323">**Description:**</span></span>  
<span data-ttu-id="5a3e9-324">Retorna a data, em hora local, depois da qual um certificado não será mais válido.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-324">Returns the date in local time after which a certificate is no longer valid.</span></span>

<span data-ttu-id="5a3e9-325">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-325">**Syntax:**</span></span>  
`dt CertNotAfter(binary certificateRawData)`  
*   <span data-ttu-id="5a3e9-326">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-326">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5a3e9-327">A matriz de bytes pode ser codificada binária (DER) ou de dados X.509 codificados em Base64.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-327">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certnotbefore"></a><span data-ttu-id="5a3e9-328">CertNotBefore</span><span class="sxs-lookup"><span data-stu-id="5a3e9-328">CertNotBefore</span></span>
<span data-ttu-id="5a3e9-329">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-329">**Description:**</span></span>  
<span data-ttu-id="5a3e9-330">Retorna a data, em hora local, na qual um certificado se torna válido.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-330">Returns the date in local time on which a certificate becomes valid.</span></span>

<span data-ttu-id="5a3e9-331">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-331">**Syntax:**</span></span>  
`dt CertNotBefore(binary certificateRawData)`  
*   <span data-ttu-id="5a3e9-332">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-332">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5a3e9-333">A matriz de bytes pode ser codificada binária (DER) ou de dados X.509 codificados em Base64.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-333">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyoid"></a><span data-ttu-id="5a3e9-334">CertPublicKeyOid</span><span class="sxs-lookup"><span data-stu-id="5a3e9-334">CertPublicKeyOid</span></span>
<span data-ttu-id="5a3e9-335">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-335">**Description:**</span></span>  
<span data-ttu-id="5a3e9-336">Retorna o OID da chave pública do certificado X.509v3.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-336">Returns the Oid of the public key for the X.509v3 certificate.</span></span>

<span data-ttu-id="5a3e9-337">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-337">**Syntax:**</span></span>  
`str CertKeyAlgorithm(binary certificateRawData)`  
*   <span data-ttu-id="5a3e9-338">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-338">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5a3e9-339">A matriz de bytes pode ser codificada binária (DER) ou de dados X.509 codificados em Base64.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-339">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certpublickeyparametersoid"></a><span data-ttu-id="5a3e9-340">CertPublicKeyParametersOid</span><span class="sxs-lookup"><span data-stu-id="5a3e9-340">CertPublicKeyParametersOid</span></span>
<span data-ttu-id="5a3e9-341">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-341">**Description:**</span></span>  
<span data-ttu-id="5a3e9-342">Retorna o OID dos parâmetros de chave pública do certificado X.509v3.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-342">Returns the Oid of the public key parameters for the X.509v3 certificate.</span></span>

<span data-ttu-id="5a3e9-343">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-343">**Syntax:**</span></span>  
`str CertPublicKeyParametersOid(binary certificateRawData)`  
*   <span data-ttu-id="5a3e9-344">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-344">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5a3e9-345">A matriz de bytes pode ser codificada binária (DER) ou de dados X.509 codificados em Base64.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-345">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certserialnumber"></a><span data-ttu-id="5a3e9-346">CertSerialNumber</span><span class="sxs-lookup"><span data-stu-id="5a3e9-346">CertSerialNumber</span></span>
<span data-ttu-id="5a3e9-347">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-347">**Description:**</span></span>  
<span data-ttu-id="5a3e9-348">Retorna o número de série do certificado X.509v3.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-348">Returns the serial number of the X.509v3 certificate.</span></span>

<span data-ttu-id="5a3e9-349">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-349">**Syntax:**</span></span>  
`str CertSerialNumber(binary certificateRawData)`  
*   <span data-ttu-id="5a3e9-350">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-350">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5a3e9-351">A matriz de bytes pode ser codificada binária (DER) ou de dados X.509 codificados em Base64.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-351">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsignaturealgorithmoid"></a><span data-ttu-id="5a3e9-352">CertSignatureAlgorithmOid</span><span class="sxs-lookup"><span data-stu-id="5a3e9-352">CertSignatureAlgorithmOid</span></span>
<span data-ttu-id="5a3e9-353">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-353">**Description:**</span></span>  
<span data-ttu-id="5a3e9-354">Retorna o OID do algoritmo usado para criar a assinatura de um certificado.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-354">Returns the Oid of the algorithm used to create the signature of a certificate.</span></span>

<span data-ttu-id="5a3e9-355">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-355">**Syntax:**</span></span>  
`str CertSignatureAlgorithmOid(binary certificateRawData)`  
*   <span data-ttu-id="5a3e9-356">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-356">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5a3e9-357">A matriz de bytes pode ser codificada binária (DER) ou de dados X.509 codificados em Base64.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-357">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubject"></a><span data-ttu-id="5a3e9-358">CertSubject</span><span class="sxs-lookup"><span data-stu-id="5a3e9-358">CertSubject</span></span>
<span data-ttu-id="5a3e9-359">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-359">**Description:**</span></span>  
<span data-ttu-id="5a3e9-360">Obtém o nome diferenciado da entidade de um certificado.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-360">Gets the subject distinguished name from a certificate.</span></span>

<span data-ttu-id="5a3e9-361">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-361">**Syntax:**</span></span>  
`str CertSubject(binary certificateRawData)`  
*   <span data-ttu-id="5a3e9-362">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-362">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5a3e9-363">A matriz de bytes pode ser codificada binária (DER) ou de dados X.509 codificados em Base64.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-363">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnamedn"></a><span data-ttu-id="5a3e9-364">CertSubjectNameDN</span><span class="sxs-lookup"><span data-stu-id="5a3e9-364">CertSubjectNameDN</span></span>
<span data-ttu-id="5a3e9-365">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-365">**Description:**</span></span>  
<span data-ttu-id="5a3e9-366">Retorna o nome diferenciado da entidade de um certificado.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-366">Returns the subject distinguished name from a certificate.</span></span>

<span data-ttu-id="5a3e9-367">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-367">**Syntax:**</span></span>  
`str CertSubjectNameDN(binary certificateRawData)`  
*   <span data-ttu-id="5a3e9-368">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-368">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5a3e9-369">A matriz de bytes pode ser codificada binária (DER) ou de dados X.509 codificados em Base64.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-369">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certsubjectnameoid"></a><span data-ttu-id="5a3e9-370">CertSubjectNameOid</span><span class="sxs-lookup"><span data-stu-id="5a3e9-370">CertSubjectNameOid</span></span>
<span data-ttu-id="5a3e9-371">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-371">**Description:**</span></span>  
<span data-ttu-id="5a3e9-372">Retorna o OID do nome da entidade de um certificado.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-372">Returns the Oid of the subject name from a certificate.</span></span>

<span data-ttu-id="5a3e9-373">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-373">**Syntax:**</span></span>  
`str CertSubjectNameOid(binary certificateRawData)`  
*   <span data-ttu-id="5a3e9-374">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-374">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5a3e9-375">A matriz de bytes pode ser codificada binária (DER) ou de dados X.509 codificados em Base64.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-375">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certthumbprint"></a><span data-ttu-id="5a3e9-376">CertThumbprint</span><span class="sxs-lookup"><span data-stu-id="5a3e9-376">CertThumbprint</span></span>
<span data-ttu-id="5a3e9-377">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-377">**Description:**</span></span>  
<span data-ttu-id="5a3e9-378">Retorna a impressão digital de um certificado.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-378">Returns the thumbprint of a certificate.</span></span>

<span data-ttu-id="5a3e9-379">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-379">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="5a3e9-380">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-380">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5a3e9-381">A matriz de bytes pode ser codificada binária (DER) ou de dados X.509 codificados em Base64.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-381">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="certversion"></a><span data-ttu-id="5a3e9-382">CertVersion</span><span class="sxs-lookup"><span data-stu-id="5a3e9-382">CertVersion</span></span>
<span data-ttu-id="5a3e9-383">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-383">**Description:**</span></span>  
<span data-ttu-id="5a3e9-384">Retorna a versão do formato X.509 de um certificado.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-384">Returns the X.509 format version of a certificate.</span></span>

<span data-ttu-id="5a3e9-385">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-385">**Syntax:**</span></span>  
`str CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="5a3e9-386">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-386">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5a3e9-387">A matriz de bytes pode ser codificada binária (DER) ou de dados X.509 codificados em Base64.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-387">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>

- - -
### <a name="cguid"></a><span data-ttu-id="5a3e9-388">CGuid</span><span class="sxs-lookup"><span data-stu-id="5a3e9-388">CGuid</span></span>
<span data-ttu-id="5a3e9-389">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-389">**Description:**</span></span>  
<span data-ttu-id="5a3e9-390">a função CGuid converte a representação da cadeia de caracteres de um GUID em sua representação binária.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-390">The CGuid function converts the string representation of a GUID to its binary representation.</span></span>

<span data-ttu-id="5a3e9-391">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-391">**Syntax:**</span></span>  
`bin CGuid(str GUID)`

* <span data-ttu-id="5a3e9-392">Uma cadeia de caracteres formatada nesse padrão: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx ou {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span><span class="sxs-lookup"><span data-stu-id="5a3e9-392">A String formatted in this pattern: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

- - -
### <a name="contains"></a><span data-ttu-id="5a3e9-393">Contém:</span><span class="sxs-lookup"><span data-stu-id="5a3e9-393">Contains</span></span>
<span data-ttu-id="5a3e9-394">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-394">**Description:**</span></span>  
<span data-ttu-id="5a3e9-395">a função Contains localiza uma cadeia de caracteres dentro de um atributo de valores múltiplos</span><span class="sxs-lookup"><span data-stu-id="5a3e9-395">The Contains function finds a string inside a multi-valued attribute</span></span>

<span data-ttu-id="5a3e9-396">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-396">**Syntax:**</span></span>  
<span data-ttu-id="5a3e9-397">`num Contains (mvstring attribute, str search)` - diferencia letras maiúsculas de minúsculas</span><span class="sxs-lookup"><span data-stu-id="5a3e9-397">`num Contains (mvstring attribute, str search)` - case-sensitive</span></span>  
`num Contains (mvstring attribute, str search, enum Casetype)`  
<span data-ttu-id="5a3e9-398">`num Contains (mvref attribute, str search)` - diferencia letras maiúsculas de minúsculas</span><span class="sxs-lookup"><span data-stu-id="5a3e9-398">`num Contains (mvref attribute, str search)` - case-sensitive</span></span>

* <span data-ttu-id="5a3e9-399">attribute: o atributo de valores múltiplos para a pesquisa.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-399">attribute: the multi-valued attribute to search.</span></span>
* <span data-ttu-id="5a3e9-400">search: a cadeia de caracteres a localizar no atributo.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-400">search: string to find in the attribute.</span></span>
* <span data-ttu-id="5a3e9-401">Casetype: CaseInsensitive ou CaseSensitive.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-401">Casetype: CaseInsensitive or CaseSensitive.</span></span>

<span data-ttu-id="5a3e9-402">Retorna o índice no atributo com vários valores em que a cadeia de caracteres foi encontrada.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-402">Returns index in the multi-valued attribute where the string was found.</span></span> <span data-ttu-id="5a3e9-403">Se a cadeia de caracteres não for encontrada, 0 será retornado.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-403">0 is returned if the string is not found.</span></span>

<span data-ttu-id="5a3e9-404">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-404">**Remarks:**</span></span>  
<span data-ttu-id="5a3e9-405">para os atributos da cadeia de caracteres de valores múltiplos, a pesquisa encontra as subcadeias nos valores.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-405">For multi-valued string attributes, the search finds substrings in the values.</span></span>  
<span data-ttu-id="5a3e9-406">Para atributos de referência, a cadeia de caracteres pesquisada deve corresponder exatamente ao valor para que sejam considerados como uma correspondência.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-406">For reference attributes, the searched string must exactly match the value to be considered a match.</span></span>

<span data-ttu-id="5a3e9-407">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-407">**Example:**</span></span>  
`IIF(Contains([proxyAddresses],"SMTP:")>0,[proxyAddresses],Error("No primary SMTP address found."))`  
<span data-ttu-id="5a3e9-408">se o atributo proxyAddresses tiver um endereço de email principal (indicado pelas letras maiúsculas "SMTP:"), o atributo proxyAddress será retornado; caso contrário, um erro será retornado.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-408">If the proxyAddresses attribute has a primary email address (indicated by uppercase "SMTP:"), then return the proxyAddress attribute, else return an error.</span></span>

- - -
### <a name="convertfrombase64"></a><span data-ttu-id="5a3e9-409">ConvertFromBase64</span><span class="sxs-lookup"><span data-stu-id="5a3e9-409">ConvertFromBase64</span></span>
<span data-ttu-id="5a3e9-410">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-410">**Description:**</span></span>  
<span data-ttu-id="5a3e9-411">a função ConvertFromBase64 converte o valor codificado base64 especificado em uma cadeia de caracteres regular.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-411">The ConvertFromBase64 function converts the specified base64 encoded value to a regular string.</span></span>

<span data-ttu-id="5a3e9-412">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-412">**Syntax:**</span></span>  
<span data-ttu-id="5a3e9-413">`str ConvertFromBase64(str source)` - adota Unicode para codificação</span><span class="sxs-lookup"><span data-stu-id="5a3e9-413">`str ConvertFromBase64(str source)` - assumes Unicode for encoding</span></span>  
`str ConvertFromBase64(str source, enum Encoding)`

* <span data-ttu-id="5a3e9-414">source: cadeia de caracteres codificada em Base64</span><span class="sxs-lookup"><span data-stu-id="5a3e9-414">source: Base64 encoded string</span></span>  
* <span data-ttu-id="5a3e9-415">Codificação: Unicode, ASCII, UTF8</span><span class="sxs-lookup"><span data-stu-id="5a3e9-415">Encoding: Unicode, ASCII, UTF8</span></span>

<span data-ttu-id="5a3e9-416">**Exemplo**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-416">**Example**</span></span>  
`ConvertFromBase64("SABlAGwAbABvACAAdwBvAHIAbABkACEA")`  
`ConvertFromBase64("SGVsbG8gd29ybGQh", UTF8)`

<span data-ttu-id="5a3e9-417">Ambos os exemplos retornam "*Hello world!*"</span><span class="sxs-lookup"><span data-stu-id="5a3e9-417">Both examples return "*Hello world!*"</span></span>

- - -
### <a name="convertfromutf8hex"></a><span data-ttu-id="5a3e9-418">ConvertFromUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="5a3e9-418">ConvertFromUTF8Hex</span></span>
<span data-ttu-id="5a3e9-419">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-419">**Description:**</span></span>  
<span data-ttu-id="5a3e9-420">a função ConvertFromUTF8Hex converte o valor codificado em UTF8 hexadecimal especificado em uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-420">The ConvertFromUTF8Hex function converts the specified UTF8 Hex encoded value to a string.</span></span>

<span data-ttu-id="5a3e9-421">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-421">**Syntax:**</span></span>  
`str ConvertFromUTF8Hex(str source)`

* <span data-ttu-id="5a3e9-422">source: cadeia de caracteres codificada em UTF8 de 2 bytes</span><span class="sxs-lookup"><span data-stu-id="5a3e9-422">source: UTF8 2-byte encoded sting</span></span>

<span data-ttu-id="5a3e9-423">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-423">**Remarks:**</span></span>  
<span data-ttu-id="5a3e9-424">A diferença entre essa função e ConvertFromBase64([],UTF8) é que o resultado é amigável para o atributo DN.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-424">The difference between this function and ConvertFromBase64([],UTF8) in that the result is friendly for the DN attribute.</span></span>  
<span data-ttu-id="5a3e9-425">Esse formato é usado pelo Active Directory do Azure como DN.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-425">This format is used by Azure Active Directory as DN.</span></span>

<span data-ttu-id="5a3e9-426">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-426">**Example:**</span></span>  
`ConvertFromUTF8Hex("48656C6C6F20776F726C6421")`  
<span data-ttu-id="5a3e9-427">retorna "*Hello world!*"</span><span class="sxs-lookup"><span data-stu-id="5a3e9-427">Returns "*Hello world!*"</span></span>

- - -
### <a name="converttobase64"></a><span data-ttu-id="5a3e9-428">ConvertToBase64</span><span class="sxs-lookup"><span data-stu-id="5a3e9-428">ConvertToBase64</span></span>
<span data-ttu-id="5a3e9-429">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-429">**Description:**</span></span>  
<span data-ttu-id="5a3e9-430">a função ConvertToBase64 converte uma cadeia de caracteres em uma cadeia de caracteres Unicode em base64.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-430">The ConvertToBase64 function converts a string to a Unicode base64 string.</span></span>  
<span data-ttu-id="5a3e9-431">Converte o valor de uma matriz de inteiros em sua representação equivalente de cadeia de caracteres, que é codificada com dígitos em base 64.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-431">Converts the value of an array of integers to its equivalent string representation that is encoded with base-64 digits.</span></span>

<span data-ttu-id="5a3e9-432">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-432">**Syntax:**</span></span>  
`str ConvertToBase64(str source)`

<span data-ttu-id="5a3e9-433">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-433">**Example:**</span></span>  
`ConvertToBase64("Hello world!")`  
<span data-ttu-id="5a3e9-434">retorna "SABlAGwAbABvACAAdwBvAHIAbABkACEA"</span><span class="sxs-lookup"><span data-stu-id="5a3e9-434">Returns "SABlAGwAbABvACAAdwBvAHIAbABkACEA"</span></span>

- - -
### <a name="converttoutf8hex"></a><span data-ttu-id="5a3e9-435">ConvertToUTF8Hex</span><span class="sxs-lookup"><span data-stu-id="5a3e9-435">ConvertToUTF8Hex</span></span>
<span data-ttu-id="5a3e9-436">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-436">**Description:**</span></span>  
<span data-ttu-id="5a3e9-437">a função ConvertToUTF8Hex converte uma cadeia de caracteres em um valor codificado em UTF8 hexadecimal.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-437">The ConvertToUTF8Hex function converts a string to a UTF8 Hex encoded value.</span></span>

<span data-ttu-id="5a3e9-438">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-438">**Syntax:**</span></span>  
`str ConvertToUTF8Hex(str source)`

<span data-ttu-id="5a3e9-439">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-439">**Remarks:**</span></span>  
<span data-ttu-id="5a3e9-440">o formato de saída dessa função é usado pelo Azure Active Directory como o formato do atributo DN.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-440">The output format of this function is used by Azure Active Directory as DN attribute format.</span></span>

<span data-ttu-id="5a3e9-441">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-441">**Example:**</span></span>  
`ConvertToUTF8Hex("Hello world!")`  
<span data-ttu-id="5a3e9-442">retorna 48656C6C6F20776F726C6421</span><span class="sxs-lookup"><span data-stu-id="5a3e9-442">Returns 48656C6C6F20776F726C6421</span></span>

- - -
### <a name="count"></a><span data-ttu-id="5a3e9-443">Contagem</span><span class="sxs-lookup"><span data-stu-id="5a3e9-443">Count</span></span>
<span data-ttu-id="5a3e9-444">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-444">**Description:**</span></span>  
<span data-ttu-id="5a3e9-445">a função Count retorna o número de elementos em um atributo de valores múltiplos</span><span class="sxs-lookup"><span data-stu-id="5a3e9-445">The Count function returns the number of elements in a multi-valued attribute</span></span>

<span data-ttu-id="5a3e9-446">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-446">**Syntax:**</span></span>  
`num Count(mvstr attribute)`

- - -
### <a name="cnum"></a><span data-ttu-id="5a3e9-447">CNum</span><span class="sxs-lookup"><span data-stu-id="5a3e9-447">CNum</span></span>
<span data-ttu-id="5a3e9-448">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-448">**Description:**</span></span>  
<span data-ttu-id="5a3e9-449">a função CNum obtém uma cadeia de caracteres e retorna um tipo de dados numérico.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-449">The CNum function takes a string and returns a numeric data type.</span></span>

<span data-ttu-id="5a3e9-450">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-450">**Syntax:**</span></span>  
`num CNum(str value)`

- - -
### <a name="cref"></a><span data-ttu-id="5a3e9-451">CRef</span><span class="sxs-lookup"><span data-stu-id="5a3e9-451">CRef</span></span>
<span data-ttu-id="5a3e9-452">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-452">**Description:**</span></span>  
<span data-ttu-id="5a3e9-453">converte uma cadeia de caracteres em um atributo de referência</span><span class="sxs-lookup"><span data-stu-id="5a3e9-453">Converts a string to a reference attribute</span></span>

<span data-ttu-id="5a3e9-454">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-454">**Syntax:**</span></span>  
`ref CRef(str value)`

<span data-ttu-id="5a3e9-455">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-455">**Example:**</span></span>  
`CRef("CN=LC Services,CN=Microsoft,CN=lcspool01,CN=Pools,CN=RTC Service," & %Forest.LDAP%)`

- - -
### <a name="cstr"></a><span data-ttu-id="5a3e9-456">CStr</span><span class="sxs-lookup"><span data-stu-id="5a3e9-456">CStr</span></span>
<span data-ttu-id="5a3e9-457">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-457">**Description:**</span></span>  
<span data-ttu-id="5a3e9-458">a função CStr converte em um tipo de dados da cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-458">The CStr function converts to a string data type.</span></span>

<span data-ttu-id="5a3e9-459">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-459">**Syntax:**</span></span>  
`str CStr(num value)`  
`str CStr(ref value)`  
`str CStr(bool value)`  

* <span data-ttu-id="5a3e9-460">valor: pode ser um valor numérico, o atributo de referência ou booliano.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-460">value: Can be a numeric value, reference attribute, or Boolean.</span></span>

<span data-ttu-id="5a3e9-461">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-461">**Example:**</span></span>  
`CStr([dn])`  
<span data-ttu-id="5a3e9-462">poderia retornar "cn=Joe,dc=contoso,dc=com"</span><span class="sxs-lookup"><span data-stu-id="5a3e9-462">Could return "cn=Joe,dc=contoso,dc=com"</span></span>

- - -
### <a name="dateadd"></a><span data-ttu-id="5a3e9-463">DateAdd</span><span class="sxs-lookup"><span data-stu-id="5a3e9-463">DateAdd</span></span>
<span data-ttu-id="5a3e9-464">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-464">**Description:**</span></span>  
<span data-ttu-id="5a3e9-465">retorna um Date contendo uma data à qual um intervalo de tempo especificado foi adicionado.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-465">Returns a Date containing a date to which a specified time interval has been added.</span></span>

<span data-ttu-id="5a3e9-466">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-466">**Syntax:**</span></span>  
`dt DateAdd(str interval, num value, dt date)`

* <span data-ttu-id="5a3e9-467">interval: expressão de cadeia de caracteres que é o intervalo de tempo que você deseja adicionar.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-467">interval: String expression that is the interval of time you want to add.</span></span> <span data-ttu-id="5a3e9-468">A cadeia de caracteres deve ter um dos seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="5a3e9-468">The string must have one of the following values:</span></span>
  * <span data-ttu-id="5a3e9-469">aaaa Ano</span><span class="sxs-lookup"><span data-stu-id="5a3e9-469">yyyy Year</span></span>
  * <span data-ttu-id="5a3e9-470">q - Trimestre</span><span class="sxs-lookup"><span data-stu-id="5a3e9-470">q Quarter</span></span>
  * <span data-ttu-id="5a3e9-471">m - Mês</span><span class="sxs-lookup"><span data-stu-id="5a3e9-471">m Month</span></span>
  * <span data-ttu-id="5a3e9-472">y - Dia do ano</span><span class="sxs-lookup"><span data-stu-id="5a3e9-472">y Day of year</span></span>
  * <span data-ttu-id="5a3e9-473">d - Dia</span><span class="sxs-lookup"><span data-stu-id="5a3e9-473">d Day</span></span>
  * <span data-ttu-id="5a3e9-474">w - Dia da semana</span><span class="sxs-lookup"><span data-stu-id="5a3e9-474">w Weekday</span></span>
  * <span data-ttu-id="5a3e9-475">ww - Semana</span><span class="sxs-lookup"><span data-stu-id="5a3e9-475">ww Week</span></span>
  * <span data-ttu-id="5a3e9-476">h - Hora</span><span class="sxs-lookup"><span data-stu-id="5a3e9-476">h Hour</span></span>
  * <span data-ttu-id="5a3e9-477">m - Minuto</span><span class="sxs-lookup"><span data-stu-id="5a3e9-477">n Minute</span></span>
  * <span data-ttu-id="5a3e9-478">s - Segundo</span><span class="sxs-lookup"><span data-stu-id="5a3e9-478">s Second</span></span>
* <span data-ttu-id="5a3e9-479">valor: O número de unidades que você deseja adicionar.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-479">value: The number of units you want to add.</span></span> <span data-ttu-id="5a3e9-480">Ele pode ser positivo (para obter datas no futuro) ou negativo (para obter datas no passado).</span><span class="sxs-lookup"><span data-stu-id="5a3e9-480">It can be positive (to get dates in the future) or negative (to get dates in the past).</span></span>
* <span data-ttu-id="5a3e9-481">date: DateTime, representando a data à qual o intervalo é adicionado.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-481">date: DateTime representing date to which the interval is added.</span></span>

<span data-ttu-id="5a3e9-482">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-482">**Example:**</span></span>  
`DateAdd("m", 3, CDate("2001-01-01"))`  
<span data-ttu-id="5a3e9-483">adiciona três meses e retorna um DateTime que representa "01/04/2001".</span><span class="sxs-lookup"><span data-stu-id="5a3e9-483">Adds 3 months and returns a DateTime representing "2001-04-01".</span></span>

- - -
### <a name="datefromnum"></a><span data-ttu-id="5a3e9-484">DateFromNum</span><span class="sxs-lookup"><span data-stu-id="5a3e9-484">DateFromNum</span></span>
<span data-ttu-id="5a3e9-485">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-485">**Description:**</span></span>  
<span data-ttu-id="5a3e9-486">a função DateFromNum converte um valor, no formato de data do AD, em um tipo DateTime.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-486">The DateFromNum function converts a value in AD’s date format to a DateTime type.</span></span>

<span data-ttu-id="5a3e9-487">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-487">**Syntax:**</span></span>  
`dt DateFromNum(num value)`

<span data-ttu-id="5a3e9-488">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-488">**Example:**</span></span>  
`DateFromNum([lastLogonTimestamp])`  
`DateFromNum(129699324000000000)`  
<span data-ttu-id="5a3e9-489">retorna um DateTime que representa 01/01/2012 23:00:00</span><span class="sxs-lookup"><span data-stu-id="5a3e9-489">Returns a DateTime representing 2012-01-01 23:00:00</span></span>

- - -
### <a name="dncomponent"></a><span data-ttu-id="5a3e9-490">DNComponent</span><span class="sxs-lookup"><span data-stu-id="5a3e9-490">DNComponent</span></span>
<span data-ttu-id="5a3e9-491">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-491">**Description:**</span></span>  
<span data-ttu-id="5a3e9-492">a função DNComponent retorna o valor de um componente DN especificado saindo da esquerda.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-492">The DNComponent function returns the value of a specified DN component going from left.</span></span>

<span data-ttu-id="5a3e9-493">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-493">**Syntax:**</span></span>  
`str DNComponent(ref dn, num ComponentNumber)`

* <span data-ttu-id="5a3e9-494">dn: o atributo de referência a interpretar</span><span class="sxs-lookup"><span data-stu-id="5a3e9-494">dn: the reference attribute to interpret</span></span>
* <span data-ttu-id="5a3e9-495">ComponentNumber: o componente no DN a retornar</span><span class="sxs-lookup"><span data-stu-id="5a3e9-495">ComponentNumber: The component in the DN to return</span></span>

<span data-ttu-id="5a3e9-496">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-496">**Example:**</span></span>  
`DNComponent([dn],1)`  
<span data-ttu-id="5a3e9-497">se dn é “cn=Joe,ou=…,” ele retorna Joe</span><span class="sxs-lookup"><span data-stu-id="5a3e9-497">If dn is "cn=Joe,ou=…," it returns Joe</span></span>

- - -
### <a name="dncomponentrev"></a><span data-ttu-id="5a3e9-498">DNComponentRev</span><span class="sxs-lookup"><span data-stu-id="5a3e9-498">DNComponentRev</span></span>
<span data-ttu-id="5a3e9-499">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-499">**Description:**</span></span>  
<span data-ttu-id="5a3e9-500">a função DNComponentRev retorna o valor de um componente DN especificado saindo da direita (o final).</span><span class="sxs-lookup"><span data-stu-id="5a3e9-500">The DNComponentRev function returns the value of a specified DN component going from right (the end).</span></span>

<span data-ttu-id="5a3e9-501">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-501">**Syntax:**</span></span>  
`str DNComponentRev(ref dn, num ComponentNumber)`  
`str DNComponentRev(ref dn, num ComponentNumber, enum Options)`

* <span data-ttu-id="5a3e9-502">dn: o atributo de referência a interpretar</span><span class="sxs-lookup"><span data-stu-id="5a3e9-502">dn: the reference attribute to interpret</span></span>
* <span data-ttu-id="5a3e9-503">ComponentNumber - o componente no DN a retornar</span><span class="sxs-lookup"><span data-stu-id="5a3e9-503">ComponentNumber - The component in the DN to return</span></span>
* <span data-ttu-id="5a3e9-504">Opções: DC – ignorar todos os componentes com “dc=”</span><span class="sxs-lookup"><span data-stu-id="5a3e9-504">Options: DC – Ignore all components with "dc="</span></span>

<span data-ttu-id="5a3e9-505">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-505">**Example:**</span></span>  
<span data-ttu-id="5a3e9-506">Se dn for "cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com" então</span><span class="sxs-lookup"><span data-stu-id="5a3e9-506">If dn is "cn=Joe,ou=Atlanta,ou=GA,ou=US, dc=contoso,dc=com" then</span></span>  
`DNComponentRev([dn],3)`  
`DNComponentRev([dn],1,"DC")`  
<span data-ttu-id="5a3e9-507">ambos retornam US.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-507">Both return US.</span></span>

- - -
### <a name="error"></a><span data-ttu-id="5a3e9-508">Erro</span><span class="sxs-lookup"><span data-stu-id="5a3e9-508">Error</span></span>
<span data-ttu-id="5a3e9-509">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-509">**Description:**</span></span>  
<span data-ttu-id="5a3e9-510">a função Error é usada para retornar um erro personalizado.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-510">The Error function is used to return a custom error.</span></span>

<span data-ttu-id="5a3e9-511">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-511">**Syntax:**</span></span>  
`void Error(str ErrorMessage)`

<span data-ttu-id="5a3e9-512">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-512">**Example:**</span></span>  
`IIF(IsPresent([accountName]),[accountName],Error("AccountName is required"))`  
<span data-ttu-id="5a3e9-513">se o atributo accountName não estiver presente, gere um erro no objeto.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-513">If the attribute accountName is not present, throw an error on the object.</span></span>

- - -
### <a name="escapedncomponent"></a><span data-ttu-id="5a3e9-514">EscapeDNComponent</span><span class="sxs-lookup"><span data-stu-id="5a3e9-514">EscapeDNComponent</span></span>
<span data-ttu-id="5a3e9-515">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-515">**Description:**</span></span>  
<span data-ttu-id="5a3e9-516">a função EscapeDNComponent obtém um componente de um DN e aplica o escape para que ele possa ser representado no LDAP.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-516">The EscapeDNComponent function takes one component of a DN and escapes it so it can be represented in LDAP.</span></span>

<span data-ttu-id="5a3e9-517">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-517">**Syntax:**</span></span>  
`str EscapeDNComponent(str value)`

<span data-ttu-id="5a3e9-518">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-518">**Example:**</span></span>  
`EscapeDNComponent("cn=" & [displayName]) & "," & %ForestLDAP%)`  
<span data-ttu-id="5a3e9-519">garante que o objeto possa ser criado em um diretório LDAP, mesmo que o atributo displayName tenha caracteres que devam ter o escape aplicado no LDAP.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-519">Makes sure the object can be created in an LDAP directory even if the displayName attribute has characters that must be escaped in LDAP.</span></span>

- - -
### <a name="formatdatetime"></a><span data-ttu-id="5a3e9-520">FormatDateTime</span><span class="sxs-lookup"><span data-stu-id="5a3e9-520">FormatDateTime</span></span>
<span data-ttu-id="5a3e9-521">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-521">**Description:**</span></span>  
<span data-ttu-id="5a3e9-522">a função FormatDateTime é usada para formatar um DateTime para uma cadeia de caracteres com um formato especificado</span><span class="sxs-lookup"><span data-stu-id="5a3e9-522">The FormatDateTime function is used to format a DateTime to a string with a specified format</span></span>

<span data-ttu-id="5a3e9-523">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-523">**Syntax:**</span></span>  
`str FormatDateTime(dt value, str format)`

* <span data-ttu-id="5a3e9-524">value: um valor no formato DateTime</span><span class="sxs-lookup"><span data-stu-id="5a3e9-524">value: a value in the DateTime format</span></span>
* <span data-ttu-id="5a3e9-525">format: uma cadeia de caracteres que representa o formato para o qual converter.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-525">format: a string representing the format to convert to.</span></span>

<span data-ttu-id="5a3e9-526">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-526">**Remarks:**</span></span>  
<span data-ttu-id="5a3e9-527">Os possíveis valores para o formato podem ser encontrados aqui: [Formatos de Data/Hora Definidos pelo Usuário (Função Format)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span><span class="sxs-lookup"><span data-stu-id="5a3e9-527">The possible values for the format can be found here: [User-Defined Date/Time Formats (Format Function)](http://msdn2.microsoft.com/library/73ctwf33\(VS.90\).aspx)</span></span>

<span data-ttu-id="5a3e9-528">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-528">**Example:**</span></span>  

`FormatDateTime(CDate("12/25/2007"),"yyyy-mm-dd")`  
<span data-ttu-id="5a3e9-529">resulta em "25/12/2007".</span><span class="sxs-lookup"><span data-stu-id="5a3e9-529">Results in "2007-12-25".</span></span>

`FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")`  
<span data-ttu-id="5a3e9-530">pode resultar em "20140905081453.0Z"</span><span class="sxs-lookup"><span data-stu-id="5a3e9-530">Can result in "20140905081453.0Z"</span></span>

- - -
### <a name="guid"></a><span data-ttu-id="5a3e9-531">GUID</span><span class="sxs-lookup"><span data-stu-id="5a3e9-531">GUID</span></span>
<span data-ttu-id="5a3e9-532">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-532">**Description:**</span></span>  
<span data-ttu-id="5a3e9-533">a função GUID gera um novo GUID aleatório</span><span class="sxs-lookup"><span data-stu-id="5a3e9-533">The function GUID generates a new random GUID</span></span>

<span data-ttu-id="5a3e9-534">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-534">**Syntax:**</span></span>  
`str GUID()`

- - -
### <a name="iif"></a><span data-ttu-id="5a3e9-535">IIF</span><span class="sxs-lookup"><span data-stu-id="5a3e9-535">IIF</span></span>
<span data-ttu-id="5a3e9-536">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-536">**Description:**</span></span>  
<span data-ttu-id="5a3e9-537">a função IIF retorna um valor de um conjunto de valores possíveis com base em uma condição especificada.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-537">The IIF function returns one of a set of possible values based on a specified condition.</span></span>

<span data-ttu-id="5a3e9-538">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-538">**Syntax:**</span></span>  
`var IIF(exp condition, var valueIfTrue, var valueIfFalse)`

* <span data-ttu-id="5a3e9-539">condition: qualquer valor ou expressão que pode ser avaliada como true ou false.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-539">condition: any value or expression that can be evaluated to true or false.</span></span>
* <span data-ttu-id="5a3e9-540">valueIfTrue: se a condição for avaliada como true, o valor será retornado.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-540">valueIfTrue: If the condition evaluates to true, the returned value.</span></span>
* <span data-ttu-id="5a3e9-541">valueIfFalse: se a condição for avaliada como false, o valor será retornado.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-541">valueIfFalse: If the condition evaluates to false, the returned value.</span></span>

<span data-ttu-id="5a3e9-542">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-542">**Example:**</span></span>  
`IIF([employeeType]="Intern","t-" & [alias],[alias])`  
 <span data-ttu-id="5a3e9-543">se o usuário for um estagiário, retornará o alias de um usuário com "t-" adicionado ao início; caso contrário, retornará o alias do usuário como está.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-543">If the user is an intern, returns the alias of a user with "t-" added to the beginning of it, else returns the user’s alias as is.</span></span>

- - -
### <a name="instr"></a><span data-ttu-id="5a3e9-544">InStr</span><span class="sxs-lookup"><span data-stu-id="5a3e9-544">InStr</span></span>
<span data-ttu-id="5a3e9-545">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-545">**Description:**</span></span>  
<span data-ttu-id="5a3e9-546">a função InStr localiza a primeira ocorrência de uma subcadeia de caracteres em uma cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5a3e9-546">The InStr function finds the first occurrence of a substring in a string</span></span>

<span data-ttu-id="5a3e9-547">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-547">**Syntax:**</span></span>  

`num InStr(str stringcheck, str stringmatch)`  
`num InStr(str stringcheck, str stringmatch, num start)`  
`num InStr(str stringcheck, str stringmatch, num start , enum compare)`

* <span data-ttu-id="5a3e9-548">stringcheck: cadeia de caracteres a ser pesquisada</span><span class="sxs-lookup"><span data-stu-id="5a3e9-548">stringcheck: string to be searched</span></span>
* <span data-ttu-id="5a3e9-549">stringmatch: cadeia de caracteres a ser localizada</span><span class="sxs-lookup"><span data-stu-id="5a3e9-549">stringmatch: string to be found</span></span>
* <span data-ttu-id="5a3e9-550">start: posição inicial para se localizar a subcadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5a3e9-550">start: starting position to find the substring</span></span>
* <span data-ttu-id="5a3e9-551">compare: vbTextCompare ou vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="5a3e9-551">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="5a3e9-552">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-552">**Remarks:**</span></span>  
<span data-ttu-id="5a3e9-553">retorna a posição onde a subcadeia de caracteres foi encontrada ou 0, se não foi encontrada.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-553">Returns the position where the substring was found or 0 if not found.</span></span>

<span data-ttu-id="5a3e9-554">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-554">**Example:**</span></span>  
`InStr("The quick brown fox","quick")`  
<span data-ttu-id="5a3e9-555">é avaliado como 5</span><span class="sxs-lookup"><span data-stu-id="5a3e9-555">Evalues to 5</span></span>

`InStr("repEated","e",3,vbBinaryCompare)`  
<span data-ttu-id="5a3e9-556">é avaliado como 7</span><span class="sxs-lookup"><span data-stu-id="5a3e9-556">Evaluates to 7</span></span>

- - -
### <a name="instrrev"></a><span data-ttu-id="5a3e9-557">InStrRev</span><span class="sxs-lookup"><span data-stu-id="5a3e9-557">InStrRev</span></span>
<span data-ttu-id="5a3e9-558">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-558">**Description:**</span></span>  
<span data-ttu-id="5a3e9-559">a função InStrRev localiza a última ocorrência de uma subcadeia de caracteres em uma cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5a3e9-559">The InStrRev function finds the last occurrence of a substring in a string</span></span>

<span data-ttu-id="5a3e9-560">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-560">**Syntax:**</span></span>  
`num InstrRev(str stringcheck, str stringmatch)`  
`num InstrRev(str stringcheck, str stringmatch, num start)`  
`num InstrRev(str stringcheck, str stringmatch, num start, enum compare)`

* <span data-ttu-id="5a3e9-561">stringcheck: cadeia de caracteres a ser pesquisada</span><span class="sxs-lookup"><span data-stu-id="5a3e9-561">stringcheck: string to be searched</span></span>
* <span data-ttu-id="5a3e9-562">stringmatch: cadeia de caracteres a ser localizada</span><span class="sxs-lookup"><span data-stu-id="5a3e9-562">stringmatch: string to be found</span></span>
* <span data-ttu-id="5a3e9-563">start: posição inicial para se localizar a subcadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5a3e9-563">start: starting position to find the substring</span></span>
* <span data-ttu-id="5a3e9-564">compare: vbTextCompare ou vbBinaryCompare</span><span class="sxs-lookup"><span data-stu-id="5a3e9-564">compare: vbTextCompare or vbBinaryCompare</span></span>

<span data-ttu-id="5a3e9-565">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-565">**Remarks:**</span></span>  
<span data-ttu-id="5a3e9-566">retorna a posição onde a subcadeia de caracteres foi encontrada ou 0, se não foi encontrada.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-566">Returns the position where the substring was found or 0 if not found.</span></span>

<span data-ttu-id="5a3e9-567">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-567">**Example:**</span></span>  
`InStrRev("abbcdbbbef","bb")`  
<span data-ttu-id="5a3e9-568">retorna 7</span><span class="sxs-lookup"><span data-stu-id="5a3e9-568">Returns 7</span></span>

- - -
### <a name="isbitset"></a><span data-ttu-id="5a3e9-569">IsBitSet</span><span class="sxs-lookup"><span data-stu-id="5a3e9-569">IsBitSet</span></span>
<span data-ttu-id="5a3e9-570">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-570">**Description:**</span></span>  
<span data-ttu-id="5a3e9-571">a função IsBitSet testa se um bit está definido ou não</span><span class="sxs-lookup"><span data-stu-id="5a3e9-571">The function IsBitSet Tests if a bit is set or not</span></span>

<span data-ttu-id="5a3e9-572">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-572">**Syntax:**</span></span>  
`bool IsBitSet(num value, num flag)`

* <span data-ttu-id="5a3e9-573">value: um valor numérico que é evaluated.flag: um valor numérico que contém o bit a ser avaliado</span><span class="sxs-lookup"><span data-stu-id="5a3e9-573">value: a numeric value that is evaluated.flag: a numeric value that has the bit to be evaluated</span></span>

<span data-ttu-id="5a3e9-574">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-574">**Example:**</span></span>  
`IsBitSet(&HF,4)`  
<span data-ttu-id="5a3e9-575">retorna True porque o bit "4" está definido no valor hexadecimal "F"</span><span class="sxs-lookup"><span data-stu-id="5a3e9-575">Returns True because bit "4" is set in the hexadecimal value "F"</span></span>

- - -
### <a name="isdate"></a><span data-ttu-id="5a3e9-576">IsDate</span><span class="sxs-lookup"><span data-stu-id="5a3e9-576">IsDate</span></span>
<span data-ttu-id="5a3e9-577">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-577">**Description:**</span></span>  
<span data-ttu-id="5a3e9-578">se a expressão puder ser avaliada como um tipo DateTime, a função IsDate será avaliada como True.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-578">If the expression can be evaluates as a DateTime type, then the IsDate function evaluates to True.</span></span>

<span data-ttu-id="5a3e9-579">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-579">**Syntax:**</span></span>  
`bool IsDate(var Expression)`

<span data-ttu-id="5a3e9-580">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-580">**Remarks:**</span></span>  
<span data-ttu-id="5a3e9-581">usada para determinar se CDate() pode ter êxito.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-581">Used to determine if CDate() can be successful.</span></span>

- - -
### <a name="iscert"></a><span data-ttu-id="5a3e9-582">IsCert</span><span class="sxs-lookup"><span data-stu-id="5a3e9-582">IsCert</span></span>
<span data-ttu-id="5a3e9-583">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-583">**Description:**</span></span>  
<span data-ttu-id="5a3e9-584">Retorna verdadeiro se os dados brutos puderem ser serializados no objeto de certificado .NET X509Certificate2.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-584">Returns true if the raw data can be serialized into .NET X509Certificate2 certificate object.</span></span>

<span data-ttu-id="5a3e9-585">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-585">**Syntax:**</span></span>  
`bool CertThumbprint(binary certificateRawData)`  
*   <span data-ttu-id="5a3e9-586">certificateRawData: representação de matriz de bytes de um certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-586">certificateRawData: Byte array representation of an X.509 certificate.</span></span> <span data-ttu-id="5a3e9-587">A matriz de bytes pode ser codificada binária (DER) ou de dados X.509 codificados em Base64.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-587">The byte array can be binary (DER) encoded or Base64-encoded X.509 data.</span></span>
- - -
### <a name="isempty"></a><span data-ttu-id="5a3e9-588">IsEmpty</span><span class="sxs-lookup"><span data-stu-id="5a3e9-588">IsEmpty</span></span>
<span data-ttu-id="5a3e9-589">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-589">**Description:**</span></span>  
<span data-ttu-id="5a3e9-590">se o atributo estiver presente no CS ou no MV, mas for avaliado como uma cadeia de caracteres vazia, a função IsEmpty será avaliada como True.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-590">If the attribute is present in the CS or MV but evaluates to an empty string, then the IsEmpty function evaluates to True.</span></span>

<span data-ttu-id="5a3e9-591">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-591">**Syntax:**</span></span>  
`bool IsEmpty(var Expression)`

- - -
### <a name="isguid"></a><span data-ttu-id="5a3e9-592">IsGuid</span><span class="sxs-lookup"><span data-stu-id="5a3e9-592">IsGuid</span></span>
<span data-ttu-id="5a3e9-593">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-593">**Description:**</span></span>  
<span data-ttu-id="5a3e9-594">se a cadeia de caracteres puder ser convertida em um GUID, a função IsGuid será avaliada como true.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-594">If the string could be converted to a GUID, then the IsGuid function evaluated to true.</span></span>

<span data-ttu-id="5a3e9-595">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-595">**Syntax:**</span></span>  
`bool IsGuid(str GUID)`

<span data-ttu-id="5a3e9-596">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-596">**Remarks:**</span></span>  
<span data-ttu-id="5a3e9-597">um GUID é definido como uma cadeia de caracteres seguindo um destes padrões: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx ou {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span><span class="sxs-lookup"><span data-stu-id="5a3e9-597">A GUID is defined as a string following one of these patterns: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx or {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx}</span></span>

<span data-ttu-id="5a3e9-598">Usada para determinar se CGuid() pode ter êxito.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-598">Used to determine if CGuid() can be successful.</span></span>

<span data-ttu-id="5a3e9-599">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-599">**Example:**</span></span>  
`IIF(IsGuid([strAttribute]),CGuid([strAttribute]),NULL)`  
<span data-ttu-id="5a3e9-600">se StrAttribute tiver um formato de GUID, retornará uma representação binária; caso contrário, retornará Null.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-600">If the StrAttribute has a GUID format, return a binary representation, otherwise return a Null.</span></span>

- - -
### <a name="isnull"></a><span data-ttu-id="5a3e9-601">IsNull</span><span class="sxs-lookup"><span data-stu-id="5a3e9-601">IsNull</span></span>
<span data-ttu-id="5a3e9-602">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-602">**Description:**</span></span>  
<span data-ttu-id="5a3e9-603">se a expressão for avaliada como Null, a função IsNull retornará true.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-603">If the expression evaluates to Null, then the IsNull function returns true.</span></span>

<span data-ttu-id="5a3e9-604">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-604">**Syntax:**</span></span>  
`bool IsNull(var Expression)`

<span data-ttu-id="5a3e9-605">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-605">**Remarks:**</span></span>  
<span data-ttu-id="5a3e9-606">para um atributo, um valor Null é expresso pela ausência do atributo.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-606">For an attribute, a Null is expressed by the absence of the attribute.</span></span>

<span data-ttu-id="5a3e9-607">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-607">**Example:**</span></span>  
`IsNull([displayName])`  
<span data-ttu-id="5a3e9-608">retornará True se o atributo não estiver presente no CS ou no MV.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-608">Returns True if the attribute is not present in the CS or MV.</span></span>

- - -
### <a name="isnullorempty"></a><span data-ttu-id="5a3e9-609">IsNullOrEmpty</span><span class="sxs-lookup"><span data-stu-id="5a3e9-609">IsNullOrEmpty</span></span>
<span data-ttu-id="5a3e9-610">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-610">**Description:**</span></span>  
<span data-ttu-id="5a3e9-611">se a expressão for nula ou uma cadeia de caracteres vazia, a função IsNullOrEmpty retornará true.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-611">If the expression is null or an empty string, then the IsNullOrEmpty function returns true.</span></span>

<span data-ttu-id="5a3e9-612">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-612">**Syntax:**</span></span>  
`bool IsNullOrEmpty(var Expression)`

<span data-ttu-id="5a3e9-613">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-613">**Remarks:**</span></span>  
<span data-ttu-id="5a3e9-614">para um atributo, isso seria avaliado como True se o atributo estivesse ausente ou presente, mas fosse uma cadeia de caracteres vazia.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-614">For an attribute, this would evaluate to True if the attribute is absent or is present but is an empty string.</span></span>  
<span data-ttu-id="5a3e9-615">O inverso dessa função é chamado de IsPresent.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-615">The inverse of this function is named IsPresent.</span></span>

<span data-ttu-id="5a3e9-616">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-616">**Example:**</span></span>  
`IsNullOrEmpty([displayName])`  
<span data-ttu-id="5a3e9-617">retornará True se o atributo não estiver presente ou for uma cadeia de caracteres vazia no CS ou no MV.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-617">Returns True if the attribute is not present or is an empty string in the CS or MV.</span></span>

- - -
### <a name="isnumeric"></a><span data-ttu-id="5a3e9-618">IsNumeric</span><span class="sxs-lookup"><span data-stu-id="5a3e9-618">IsNumeric</span></span>
<span data-ttu-id="5a3e9-619">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-619">**Description:**</span></span>  
<span data-ttu-id="5a3e9-620">a função IsNumeric retorna um valor booliano que indica se uma expressão pode ser avaliada como um tipo numérico.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-620">The IsNumeric function returns a Boolean value indicating whether an expression can be evaluated as a number type.</span></span>

<span data-ttu-id="5a3e9-621">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-621">**Syntax:**</span></span>  
`bool IsNumeric(var Expression)`

<span data-ttu-id="5a3e9-622">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-622">**Remarks:**</span></span>  
<span data-ttu-id="5a3e9-623">usada para determinar se CNum() pode ter êxito ao analisar a expressão.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-623">Used to determine if CNum() can be successful to parse the expression.</span></span>

- - -
### <a name="isstring"></a><span data-ttu-id="5a3e9-624">IsString</span><span class="sxs-lookup"><span data-stu-id="5a3e9-624">IsString</span></span>
<span data-ttu-id="5a3e9-625">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-625">**Description:**</span></span>  
<span data-ttu-id="5a3e9-626">se a expressão puder ser avaliada como um tipo de cadeia de caracteres, a função IsString será avaliada como True.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-626">If the expression can be evaluated to a string type, then the IsString function evaluates to True.</span></span>

<span data-ttu-id="5a3e9-627">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-627">**Syntax:**</span></span>  
`bool IsString(var expression)`

<span data-ttu-id="5a3e9-628">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-628">**Remarks:**</span></span>  
<span data-ttu-id="5a3e9-629">usada para determinar se CStr() pode ter êxito ao analisar a expressão.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-629">Used to determine if CStr() can be successful to parse the expression.</span></span>

- - -
### <a name="ispresent"></a><span data-ttu-id="5a3e9-630">IsPresent</span><span class="sxs-lookup"><span data-stu-id="5a3e9-630">IsPresent</span></span>
<span data-ttu-id="5a3e9-631">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-631">**Description:**</span></span>  
<span data-ttu-id="5a3e9-632">se a expressão for avaliada como uma cadeia de caracteres que não é Null nem vazia, a função IsPresent retornará true.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-632">If the expression evaluates to a string that is not Null and is not empty, then the IsPresent function returns true.</span></span>

<span data-ttu-id="5a3e9-633">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-633">**Syntax:**</span></span>  
`bool IsPresent(var expression)`

<span data-ttu-id="5a3e9-634">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-634">**Remarks:**</span></span>  
<span data-ttu-id="5a3e9-635">o inverso dessa função é chamado de IsNullOrEmpty.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-635">The inverse of this function is named IsNullOrEmpty.</span></span>

<span data-ttu-id="5a3e9-636">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-636">**Example:**</span></span>  
`Switch(IsPresent([directManager]),[directManager], IsPresent([skiplevelManager]),[skiplevelManager], IsPresent([director]),[director])`

- - -
### <a name="item"></a><span data-ttu-id="5a3e9-637">Item</span><span class="sxs-lookup"><span data-stu-id="5a3e9-637">Item</span></span>
<span data-ttu-id="5a3e9-638">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-638">**Description:**</span></span>  
<span data-ttu-id="5a3e9-639">a função Item retorna um item de um atributo/cadeia de caracteres de valores múltiplos.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-639">The Item function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="5a3e9-640">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-640">**Syntax:**</span></span>  
`var Item(mvstr attribute, num index)`

* <span data-ttu-id="5a3e9-641">attribute: atributo com valores múltiplos</span><span class="sxs-lookup"><span data-stu-id="5a3e9-641">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="5a3e9-642">index: índice para um item na cadeia de caracteres com vários valores.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-642">index: index to an item in the multi-valued string.</span></span>

<span data-ttu-id="5a3e9-643">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-643">**Remarks:**</span></span>  
<span data-ttu-id="5a3e9-644">a função Item é útil com a função Contains, desde que a última função retorne o índice para um item no atributo de valores múltiplos.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-644">The Item function is useful together with the Contains function since the latter function returns the index to an item in the multi-valued attribute.</span></span>

<span data-ttu-id="5a3e9-645">Gera um erro se o índice está fora dos limites.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-645">Throws an error if index is out of bounds.</span></span>

<span data-ttu-id="5a3e9-646">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-646">**Example:**</span></span>  
`Mid(Item([proxyAddress],Contains([proxyAddress], "SMTP:")),6)`  
<span data-ttu-id="5a3e9-647">retorna o endereço de email principal.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-647">Returns the primary email address.</span></span>

- - -
### <a name="itemornull"></a><span data-ttu-id="5a3e9-648">ItemOrNull</span><span class="sxs-lookup"><span data-stu-id="5a3e9-648">ItemOrNull</span></span>
<span data-ttu-id="5a3e9-649">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-649">**Description:**</span></span>  
<span data-ttu-id="5a3e9-650">a função ItemOrNull retorna um item de um atributo/cadeia de caracteres de valores múltiplos.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-650">The ItemOrNull function returns one item from a multi-valued string/attribute.</span></span>

<span data-ttu-id="5a3e9-651">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-651">**Syntax:**</span></span>  
`var ItemOrNull(mvstr attribute, num index)`

* <span data-ttu-id="5a3e9-652">attribute: atributo com valores múltiplos</span><span class="sxs-lookup"><span data-stu-id="5a3e9-652">attribute: multi-valued attribute</span></span>
* <span data-ttu-id="5a3e9-653">index: índice para um item na cadeia de caracteres com vários valores.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-653">index: index to an item in the multi-valued string.</span></span>

<span data-ttu-id="5a3e9-654">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-654">**Remarks:**</span></span>  
<span data-ttu-id="5a3e9-655">a função ItemOrNull é útil com a função Contains, desde que a última função retorne o índice para um item no atributo de valores múltiplos.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-655">The ItemOrNull function is useful together with the Contains function since the latter function returns the index to an item in the multi-valued attribute.</span></span>

<span data-ttu-id="5a3e9-656">Se o índice estiver fora dos limites, retornará um valor Null.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-656">If index is out of bounds, then returns a Null value.</span></span>

- - -
### <a name="join"></a><span data-ttu-id="5a3e9-657">Join</span><span class="sxs-lookup"><span data-stu-id="5a3e9-657">Join</span></span>
<span data-ttu-id="5a3e9-658">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-658">**Description:**</span></span>  
<span data-ttu-id="5a3e9-659">a função Join obtém uma cadeia de caracteres de valores múltiplos e retorna uma cadeia de caracteres de um único valor com um separador especificado inserido entre cada item.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-659">The Join function takes a multi-valued string and returns a single-valued string with specified separator inserted between each item.</span></span>

<span data-ttu-id="5a3e9-660">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-660">**Syntax:**</span></span>  
`str Join(mvstr attribute)`  
`str Join(mvstr attribute, str Delimiter)`

* <span data-ttu-id="5a3e9-661">attribute: um atributo de valores múltiplos contendo cadeias de caracteres a serem unidas.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-661">attribute: Multi-valued attribute containing strings to be joined.</span></span>
* <span data-ttu-id="5a3e9-662">delimiter: qualquer cadeia de caracteres usada para separar as subcadeias de caracteres na cadeia de caracteres retornada.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-662">delimiter: Any string, used to separate the substrings in the returned string.</span></span> <span data-ttu-id="5a3e9-663">Se omitido, o caractere de espaço (" ") é usado.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-663">If omitted, the space character (" ") is used.</span></span> <span data-ttu-id="5a3e9-664">Se o Delimitador é uma cadeia de caracteres de comprimento zero ("") ou Nada, todos os itens na lista são concatenados sem delimitadores.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-664">If Delimiter is a zero-length string ("") or Nothing, all items in the list are concatenated with no delimiters.</span></span>

<span data-ttu-id="5a3e9-665">**Comentários**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-665">**Remarks**</span></span>  
<span data-ttu-id="5a3e9-666">há paridade entre as funções Join e Split.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-666">There is parity between the Join and Split functions.</span></span> <span data-ttu-id="5a3e9-667">A função Join pega uma matriz de cadeias de caracteres e une-as usando uma cadeia de caracteres do delimitador, para retornar uma única cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-667">The Join function takes an array of strings and joins them using a delimiter string, to return a single string.</span></span> <span data-ttu-id="5a3e9-668">A função Split pega uma cadeia de caracteres e a separa no delimitador, para retornar uma matriz de cadeias de caracteres.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-668">The Split function takes a string and separates it at the delimiter, to return an array of strings.</span></span> <span data-ttu-id="5a3e9-669">No entanto, uma diferença importante é que a Join pode concatenar cadeias de caracteres com qualquer cadeia de caracteres delimitadora, enquanto Split só pode separar cadeias de caracteres usando um único caractere delimitador.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-669">However, a key difference is that Join can concatenate strings with any delimiter string, Split can only separate strings using a single character delimiter.</span></span>

<span data-ttu-id="5a3e9-670">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-670">**Example:**</span></span>  
`Join([proxyAddresses],",")`  
<span data-ttu-id="5a3e9-671">Poderia retornar: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="5a3e9-671">Could return: "SMTP:john.doe@contoso.com,smtp:jd@contoso.com"</span></span>

- - -
### <a name="lcase"></a><span data-ttu-id="5a3e9-672">LCase</span><span class="sxs-lookup"><span data-stu-id="5a3e9-672">LCase</span></span>
<span data-ttu-id="5a3e9-673">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-673">**Description:**</span></span>  
<span data-ttu-id="5a3e9-674">a função LCase converte todos os caracteres de uma cadeia de caracteres em letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-674">The LCase function converts all characters in a string to lower case.</span></span>

<span data-ttu-id="5a3e9-675">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-675">**Syntax:**</span></span>  
`str LCase(str value)`

<span data-ttu-id="5a3e9-676">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-676">**Example:**</span></span>  
`LCase("TeSt")`  
<span data-ttu-id="5a3e9-677">retorna "test".</span><span class="sxs-lookup"><span data-stu-id="5a3e9-677">Returns "test".</span></span>

- - -
### <a name="left"></a><span data-ttu-id="5a3e9-678">Left</span><span class="sxs-lookup"><span data-stu-id="5a3e9-678">Left</span></span>
<span data-ttu-id="5a3e9-679">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-679">**Description:**</span></span>  
<span data-ttu-id="5a3e9-680">a função Left retorna um número especificado de caracteres a partir da esquerda de uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-680">The Left function returns a specified number of characters from the left of a string.</span></span>

<span data-ttu-id="5a3e9-681">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-681">**Syntax:**</span></span>  
`str Left(str string, num NumChars)`

* <span data-ttu-id="5a3e9-682">string: a cadeia de caracteres da qual retornar caracteres</span><span class="sxs-lookup"><span data-stu-id="5a3e9-682">string: the string to return characters from</span></span>
* <span data-ttu-id="5a3e9-683">NumChars: um número que identifica o número de caracteres a ser retroando do início (esquerda) da cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5a3e9-683">NumChars: a number identifying the number of characters to return from the beginning (left) of string</span></span>

<span data-ttu-id="5a3e9-684">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-684">**Remarks:**</span></span>  
<span data-ttu-id="5a3e9-685">uma cadeia de caracteres que contém os primeiros caracteres numChars na cadeia de caracteres:</span><span class="sxs-lookup"><span data-stu-id="5a3e9-685">A string containing the first numChars characters in string:</span></span>

* <span data-ttu-id="5a3e9-686">Se numChars = 0, retorne a cadeia de caracteres vazia.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-686">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="5a3e9-687">Se numChars < 0, retorne a cadeia de caracteres de entrada.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-687">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="5a3e9-688">Se a cadeia de caracteres for nula, retorne a cadeia de caracteres vazia.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-688">If string is null, return empty string.</span></span>

<span data-ttu-id="5a3e9-689">Se a cadeia de caracteres contiver menos caracteres que o número especificado em numChars, uma cadeia de caracteres idêntica à cadeia (ou seja, que contém todos os caracteres no parâmetro 1) será retornada.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-689">If string contains fewer characters than the number specified in numChars, a string identical to string (that is, containing all characters in parameter 1) is returned.</span></span>

<span data-ttu-id="5a3e9-690">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-690">**Example:**</span></span>  
`Left("John Doe", 3)`  
<span data-ttu-id="5a3e9-691">retorna "Joh".</span><span class="sxs-lookup"><span data-stu-id="5a3e9-691">Returns "Joh".</span></span>

- - -
### <a name="len"></a><span data-ttu-id="5a3e9-692">Len</span><span class="sxs-lookup"><span data-stu-id="5a3e9-692">Len</span></span>
<span data-ttu-id="5a3e9-693">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-693">**Description:**</span></span>  
<span data-ttu-id="5a3e9-694">a função Len retorna o número de caracteres em uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-694">The Len function returns number of characters in a string.</span></span>

<span data-ttu-id="5a3e9-695">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-695">**Syntax:**</span></span>  
`num Len(str value)`

<span data-ttu-id="5a3e9-696">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-696">**Example:**</span></span>  
`Len("John Doe")`  
<span data-ttu-id="5a3e9-697">retorna 8</span><span class="sxs-lookup"><span data-stu-id="5a3e9-697">Returns 8</span></span>

- - -
### <a name="ltrim"></a><span data-ttu-id="5a3e9-698">LTrim</span><span class="sxs-lookup"><span data-stu-id="5a3e9-698">LTrim</span></span>
<span data-ttu-id="5a3e9-699">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-699">**Description:**</span></span>  
<span data-ttu-id="5a3e9-700">a função LTrim remove os espaços em branco à esquerda de uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-700">The LTrim function removes leading white spaces from a string.</span></span>

<span data-ttu-id="5a3e9-701">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-701">**Syntax:**</span></span>  
`str LTrim(str value)`

<span data-ttu-id="5a3e9-702">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-702">**Example:**</span></span>  
`LTrim(" Test ")`  
<span data-ttu-id="5a3e9-703">retorna "Test"</span><span class="sxs-lookup"><span data-stu-id="5a3e9-703">Returns "Test "</span></span>

- - -
### <a name="mid"></a><span data-ttu-id="5a3e9-704">Mid</span><span class="sxs-lookup"><span data-stu-id="5a3e9-704">Mid</span></span>
<span data-ttu-id="5a3e9-705">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-705">**Description:**</span></span>  
<span data-ttu-id="5a3e9-706">a função Mid retorna um número especificado de caracteres a partir de uma posição especificada em uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-706">The Mid function returns a specified number of characters from a specified position in a string.</span></span>

<span data-ttu-id="5a3e9-707">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-707">**Syntax:**</span></span>  
`str Mid(str string, num start, num NumChars)`

* <span data-ttu-id="5a3e9-708">string: a cadeia de caracteres da qual retornar caracteres</span><span class="sxs-lookup"><span data-stu-id="5a3e9-708">string: the string to return characters from</span></span>
* <span data-ttu-id="5a3e9-709">start: um número que identifica a posição inicial na cadeia de caracteres da qual retornar caracteres</span><span class="sxs-lookup"><span data-stu-id="5a3e9-709">start: a number identifying the starting position in string to return characters from</span></span>
* <span data-ttu-id="5a3e9-710">NumChars: um número que identifica o número de caracteres a ser retornado da posição</span><span class="sxs-lookup"><span data-stu-id="5a3e9-710">NumChars: a number identifying the number of characters to return from position in string</span></span>

<span data-ttu-id="5a3e9-711">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-711">**Remarks:**</span></span>  
<span data-ttu-id="5a3e9-712">retorna os caracteres numChars começando na posição inicial da cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-712">Return numChars characters starting from position start in string.</span></span>  
<span data-ttu-id="5a3e9-713">Uma cadeia de caracteres contendo caracteres numChars desde a posição inicial na cadeia de caracteres:</span><span class="sxs-lookup"><span data-stu-id="5a3e9-713">A string containing numChars characters from position start in string:</span></span>

* <span data-ttu-id="5a3e9-714">Se numChars = 0, retorne a cadeia de caracteres vazia.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-714">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="5a3e9-715">Se numChars < 0, retorne a cadeia de caracteres de entrada.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-715">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="5a3e9-716">Se start > o comprimento da cadeia de caracteres, retorne a cadeia de caracteres de entrada.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-716">If start > the length of string, return input string.</span></span>
* <span data-ttu-id="5a3e9-717">Se start <= 0, retorne a cadeia de caracteres de entrada.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-717">If start <= 0, return input string.</span></span>
* <span data-ttu-id="5a3e9-718">Se a cadeia de caracteres for nula, retorne a cadeia de caracteres vazia.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-718">If string is null, return empty string.</span></span>

<span data-ttu-id="5a3e9-719">Se não houver nenhum caractere numChar restante na cadeia de caracteres a partir da posição inicial, o máximo possível de caracteres será retornado.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-719">If there are not numChar characters remaining in string from position start, as many characters as possible are returned.</span></span>

<span data-ttu-id="5a3e9-720">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-720">**Example:**</span></span>  
`Mid("John Doe", 3, 5)`  
<span data-ttu-id="5a3e9-721">retorna "hn Do".</span><span class="sxs-lookup"><span data-stu-id="5a3e9-721">Returns "hn Do".</span></span>

`Mid("John Doe", 6, 999)`  
<span data-ttu-id="5a3e9-722">retorna "Doe"</span><span class="sxs-lookup"><span data-stu-id="5a3e9-722">Returns "Doe"</span></span>

- - -
### <a name="now"></a><span data-ttu-id="5a3e9-723">Now</span><span class="sxs-lookup"><span data-stu-id="5a3e9-723">Now</span></span>
<span data-ttu-id="5a3e9-724">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-724">**Description:**</span></span>  
<span data-ttu-id="5a3e9-725">a função Now retorna um DateTime especificando a data e a hora atuais, de acordo com a data e a hora do sistema do seu computador.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-725">The Now function returns a DateTime specifying the current date and time, according to your computer's system date and time.</span></span>

<span data-ttu-id="5a3e9-726">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-726">**Syntax:**</span></span>  
`dt Now()`

- - -
### <a name="numfromdate"></a><span data-ttu-id="5a3e9-727">NumFromDate</span><span class="sxs-lookup"><span data-stu-id="5a3e9-727">NumFromDate</span></span>
<span data-ttu-id="5a3e9-728">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-728">**Description:**</span></span>  
<span data-ttu-id="5a3e9-729">a função NumFromDate retorna uma data no formato de data do AD.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-729">The NumFromDate function returns a date in AD’s date format.</span></span>

<span data-ttu-id="5a3e9-730">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-730">**Syntax:**</span></span>  
`num NumFromDate(dt value)`

<span data-ttu-id="5a3e9-731">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-731">**Example:**</span></span>  
`NumFromDate(CDate("2012-01-01 23:00:00"))`  
<span data-ttu-id="5a3e9-732">retorna 129699324000000000</span><span class="sxs-lookup"><span data-stu-id="5a3e9-732">Returns 129699324000000000</span></span>

- - -
### <a name="padleft"></a><span data-ttu-id="5a3e9-733">PadLeft</span><span class="sxs-lookup"><span data-stu-id="5a3e9-733">PadLeft</span></span>
<span data-ttu-id="5a3e9-734">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-734">**Description:**</span></span>  
<span data-ttu-id="5a3e9-735">a função PadLeft preenche à esquerda uma cadeia de caracteres até um tamanho especificado usando um caractere de preenchimento fornecido.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-735">The PadLeft function left-pads a string to a specified length using a provided padding character.</span></span>

<span data-ttu-id="5a3e9-736">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-736">**Syntax:**</span></span>  
`str PadLeft(str string, num length, str padCharacter)`

* <span data-ttu-id="5a3e9-737">string: a cadeia de caracteres a preencher.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-737">string: the string to pad.</span></span>
* <span data-ttu-id="5a3e9-738">length: um inteiro que representa o comprimento da cadeia de caracteres desejado.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-738">length: An integer representing the desired length of string.</span></span>
* <span data-ttu-id="5a3e9-739">padCharacter: uma cadeia de caracteres que consiste em um único caractere a ser usado como o caractere de preenchimento</span><span class="sxs-lookup"><span data-stu-id="5a3e9-739">padCharacter: A string consisting of a single character to use as the pad character</span></span>

<span data-ttu-id="5a3e9-740">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-740">**Remarks:**</span></span>

* <span data-ttu-id="5a3e9-741">Se o comprimento da cadeia de caracteres for menor que length, padCharacter será acrescentado repetidamente ao início (esquerda) da cadeia de caracteres até que ela tenha um comprimento igual a length.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-741">If the length of string is less than length, then padCharacter is repeatedly appended to the beginning (left) of string until it has a length equal to length.</span></span>
* <span data-ttu-id="5a3e9-742">PadCharacter pode ser um caractere de espaço, mas não pode ser um valor nulo.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-742">PadCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="5a3e9-743">Se o comprimento da cadeia de caracteres é igual ou maior que length, a cadeia de caracteres é retornada inalterada.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-743">If the length of string is equal to or greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="5a3e9-744">Se a cadeia de caracteres tem um comprimento maior que ou igual a length, uma cadeia de caracteres idêntica à cadeia de caracteres em questão será retornada.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-744">If string has a length greater than or equal to length, a string identical to string is returned.</span></span>
* <span data-ttu-id="5a3e9-745">Se o comprimento da cadeia de caracteres for menor que length, uma nova cadeia de caracteres do comprimento desejado é retornada, contendo a cadeia de caracteres preenchida com um padCharacter.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-745">If the length of string is less than length, then a new string of the desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="5a3e9-746">Se a cadeia de caracteres é nula, a função retorna uma cadeia de caracteres vazia.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-746">If string is null, the function returns an empty string.</span></span>

<span data-ttu-id="5a3e9-747">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-747">**Example:**</span></span>  
`PadLeft("User", 10, "0")`  
<span data-ttu-id="5a3e9-748">retorna "000000User".</span><span class="sxs-lookup"><span data-stu-id="5a3e9-748">Returns "000000User".</span></span>

- - -
### <a name="padright"></a><span data-ttu-id="5a3e9-749">PadRight</span><span class="sxs-lookup"><span data-stu-id="5a3e9-749">PadRight</span></span>
<span data-ttu-id="5a3e9-750">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-750">**Description:**</span></span>  
<span data-ttu-id="5a3e9-751">a função PadRight preenche à direita uma cadeia de caracteres até um comprimento especificado usando um caractere de preenchimento fornecido.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-751">The PadRight function right-pads a string to a specified length using a provided padding character.</span></span>

<span data-ttu-id="5a3e9-752">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-752">**Syntax:**</span></span>  
`str PadRight(str string, num length, str padCharacter)`

* <span data-ttu-id="5a3e9-753">string: a cadeia de caracteres a preencher.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-753">string: the string to pad.</span></span>
* <span data-ttu-id="5a3e9-754">length: um inteiro que representa o comprimento da cadeia de caracteres desejado.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-754">length: An integer representing the desired length of string.</span></span>
* <span data-ttu-id="5a3e9-755">padCharacter: uma cadeia de caracteres que consiste em um único caractere a ser usado como o caractere de preenchimento</span><span class="sxs-lookup"><span data-stu-id="5a3e9-755">padCharacter: A string consisting of a single character to use as the pad character</span></span>

<span data-ttu-id="5a3e9-756">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-756">**Remarks:**</span></span>

* <span data-ttu-id="5a3e9-757">Se o comprimento da cadeia de caracteres for menor que length, padCharacter será acrescentado repetidamente ao final (direita) da cadeia de caracteres até que ela tenha um comprimento igual a length.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-757">If the length of string is less than length, then padCharacter is repeatedly appended to the end (right) of string until it has a length equal to length.</span></span>
* <span data-ttu-id="5a3e9-758">PadCharacter pode ser um caractere de espaço, mas não pode ser um valor nulo.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-758">padCharacter can be a space character, but it cannot be a null value.</span></span>
* <span data-ttu-id="5a3e9-759">Se o comprimento da cadeia de caracteres é igual ou maior que length, a cadeia de caracteres é retornada inalterada.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-759">If the length of string is equal to or greater than length, string is returned unchanged.</span></span>
* <span data-ttu-id="5a3e9-760">Se a cadeia de caracteres tem um comprimento maior que ou igual a length, uma cadeia de caracteres idêntica à cadeia de caracteres em questão será retornada.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-760">If string has a length greater than or equal to length, a string identical to string is returned.</span></span>
* <span data-ttu-id="5a3e9-761">Se o comprimento da cadeia de caracteres for menor que length, uma nova cadeia de caracteres do comprimento desejado é retornada, contendo a cadeia de caracteres preenchida com um padCharacter.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-761">If the length of string is less than length, then a new string of the desired length is returned containing string padded with a padCharacter.</span></span>
* <span data-ttu-id="5a3e9-762">Se a cadeia de caracteres é nula, a função retorna uma cadeia de caracteres vazia.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-762">If string is null, the function returns an empty string.</span></span>

<span data-ttu-id="5a3e9-763">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-763">**Example:**</span></span>  
`PadRight("User", 10, "0")`  
<span data-ttu-id="5a3e9-764">retorna "User000000".</span><span class="sxs-lookup"><span data-stu-id="5a3e9-764">Returns "User000000".</span></span>

- - -
### <a name="pcase"></a><span data-ttu-id="5a3e9-765">PCase</span><span class="sxs-lookup"><span data-stu-id="5a3e9-765">PCase</span></span>
<span data-ttu-id="5a3e9-766">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-766">**Description:**</span></span>  
<span data-ttu-id="5a3e9-767">a função PCase converte em letras maiúsculas o primeiro caractere de cada palavra delimitada por espaço em uma cadeia de caracteres, enquanto todos os outros caracteres são convertidos em letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-767">The PCase function converts the first character of each space delimited word in a string to upper case, and all other characters are converted to lower case.</span></span>

<span data-ttu-id="5a3e9-768">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-768">**Syntax:**</span></span>  
`String PCase(string)`

<span data-ttu-id="5a3e9-769">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-769">**Remarks:**</span></span>

* <span data-ttu-id="5a3e9-770">Essa função atualmente não fornece o uso de maiúsculas apropriado para converter uma palavra que está totalmente em letras maiúsculas, como um acrônimo.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-770">This function does not currently provide proper casing to convert a word that is entirely uppercase, such as an acronym.</span></span>

<span data-ttu-id="5a3e9-771">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-771">**Example:**</span></span>  
`PCase("TEsT")`  
<span data-ttu-id="5a3e9-772">retorna "test".</span><span class="sxs-lookup"><span data-stu-id="5a3e9-772">Returns "Test".</span></span>

`PCase(LCase("TEST"))`  
<span data-ttu-id="5a3e9-773">Retorna "Test"</span><span class="sxs-lookup"><span data-stu-id="5a3e9-773">Returns "Test"</span></span>

- - -
### <a name="randomnum"></a><span data-ttu-id="5a3e9-774">RandomNum</span><span class="sxs-lookup"><span data-stu-id="5a3e9-774">RandomNum</span></span>
<span data-ttu-id="5a3e9-775">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-775">**Description:**</span></span>  
<span data-ttu-id="5a3e9-776">a função RandomNum retorna um número aleatório em um intervalo especificado.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-776">The RandomNum function returns a random number between a specified interval.</span></span>

<span data-ttu-id="5a3e9-777">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-777">**Syntax:**</span></span>  
`num RandomNum(num start, num end)`

* <span data-ttu-id="5a3e9-778">start: um número que identifica o limite inferior do valor aleatório a ser gerado</span><span class="sxs-lookup"><span data-stu-id="5a3e9-778">start: a number identifying the lower limit of the random value to generate</span></span>
* <span data-ttu-id="5a3e9-779">end: um número que identifica o limite superior do valor aleatório a gerar</span><span class="sxs-lookup"><span data-stu-id="5a3e9-779">end: a number identifying the upper limit of the random value to generate</span></span>

<span data-ttu-id="5a3e9-780">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-780">**Example:**</span></span>  
`Random(100,999)`  
<span data-ttu-id="5a3e9-781">pode retornar 734.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-781">Can return 734.</span></span>

- - -
### <a name="removeduplicates"></a><span data-ttu-id="5a3e9-782">RemoveDuplicates</span><span class="sxs-lookup"><span data-stu-id="5a3e9-782">RemoveDuplicates</span></span>
<span data-ttu-id="5a3e9-783">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-783">**Description:**</span></span>  
<span data-ttu-id="5a3e9-784">a função RemoveDuplicates obtém uma cadeia de caracteres de valores múltiplos e verifica se cada valor é exclusivo.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-784">The RemoveDuplicates function takes a multi-valued string and make sure each value is unique.</span></span>

<span data-ttu-id="5a3e9-785">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-785">**Syntax:**</span></span>  
`mvstr RemoveDuplicates(mvstr attribute)`

<span data-ttu-id="5a3e9-786">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-786">**Example:**</span></span>  
`RemoveDuplicates([proxyAddresses])`  
<span data-ttu-id="5a3e9-787">retorna um atributo proxyAddress corrigido no qual todos os valores duplicados foram removidos.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-787">Returns a sanitized proxyAddress attribute where all duplicate values have been removed.</span></span>

- - -
### <a name="replace"></a><span data-ttu-id="5a3e9-788">Substitua</span><span class="sxs-lookup"><span data-stu-id="5a3e9-788">Replace</span></span>
<span data-ttu-id="5a3e9-789">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-789">**Description:**</span></span>  
<span data-ttu-id="5a3e9-790">a função Replace substitui todas as ocorrências de uma cadeia de caracteres por outra cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-790">The Replace function replaces all occurrences of a string to another string.</span></span>

<span data-ttu-id="5a3e9-791">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-791">**Syntax:**</span></span>  
`str Replace(str string, str OldValue, str NewValue)`

* <span data-ttu-id="5a3e9-792">string: uma cadeia de caracteres na qual substituir valores.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-792">string: A string to replace values in.</span></span>
* <span data-ttu-id="5a3e9-793">OldValue: a cadeia de caracteres pela qual pesquisar e a qual substituir.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-793">OldValue: The string to search for and to replace.</span></span>
* <span data-ttu-id="5a3e9-794">NewValue: a cadeia de caracteres a substituir.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-794">NewValue: The string to replace to.</span></span>

<span data-ttu-id="5a3e9-795">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-795">**Remarks:**</span></span>  
<span data-ttu-id="5a3e9-796">a função reconhece os seguintes monikers especiais:</span><span class="sxs-lookup"><span data-stu-id="5a3e9-796">The function recognizes the following special monikers:</span></span>

* <span data-ttu-id="5a3e9-797">\n - Nova linha</span><span class="sxs-lookup"><span data-stu-id="5a3e9-797">\n – New Line</span></span>
* <span data-ttu-id="5a3e9-798">\r - Retorno de carro</span><span class="sxs-lookup"><span data-stu-id="5a3e9-798">\r – Carriage Return</span></span>
* <span data-ttu-id="5a3e9-799">\t - Guia</span><span class="sxs-lookup"><span data-stu-id="5a3e9-799">\t – Tab</span></span>

<span data-ttu-id="5a3e9-800">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-800">**Example:**</span></span>  
`Replace([address],"\r\n",", ")`  
<span data-ttu-id="5a3e9-801">substitui CRLF por uma vírgula e espaço, e pode levar a "One Microsoft Way, Redmond, WA, USA"</span><span class="sxs-lookup"><span data-stu-id="5a3e9-801">Replaces CRLF with a comma and space, and could lead to "One Microsoft Way, Redmond, WA, USA"</span></span>

- - -
### <a name="replacechars"></a><span data-ttu-id="5a3e9-802">ReplaceChars</span><span class="sxs-lookup"><span data-stu-id="5a3e9-802">ReplaceChars</span></span>
<span data-ttu-id="5a3e9-803">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-803">**Description:**</span></span>  
<span data-ttu-id="5a3e9-804">a função ReplaceChars substitui todas as ocorrências de caracteres encontradas na cadeia de caracteres ReplacePattern.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-804">The ReplaceChars function replaces all occurrences of characters found in the ReplacePattern string.</span></span>

<span data-ttu-id="5a3e9-805">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-805">**Syntax:**</span></span>  
`str ReplaceChars(str string, str ReplacePattern)`

* <span data-ttu-id="5a3e9-806">string: uma cadeia de caracteres na qual substituir caracteres.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-806">string: A string to replace characters in.</span></span>
* <span data-ttu-id="5a3e9-807">ReplacePattern: uma cadeia de caracteres que contém um dicionário com caracteres a substituir.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-807">ReplacePattern: a string containing a dictionary with characters to replace.</span></span>

<span data-ttu-id="5a3e9-808">O formato é {origem1}:{destino1},{origem2}:{destino2},{origemN},{destinoN}, em que a origem é o caractere a localizar e destino é a cadeia de caracteres com a qual trabalhar.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-808">The format is {source1}:{target1},{source2}:{target2},{sourceN},{targetN} where source is the character to find and target the string to replace with.</span></span>

<span data-ttu-id="5a3e9-809">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-809">**Remarks:**</span></span>

* <span data-ttu-id="5a3e9-810">A função considera cada ocorrência de origens definidas e as substitui pelos destinos.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-810">The function takes each occurrence of defined sources and replaces them with the targets.</span></span>
* <span data-ttu-id="5a3e9-811">A origem deve ter exatamente um caractere (unicode).</span><span class="sxs-lookup"><span data-stu-id="5a3e9-811">The source must be exactly one (unicode) character.</span></span>
* <span data-ttu-id="5a3e9-812">A origem não pode ser vazia nem maior que um caractere (erro de análise).</span><span class="sxs-lookup"><span data-stu-id="5a3e9-812">The source cannot be empty or longer than one character (parsing error).</span></span>
* <span data-ttu-id="5a3e9-813">O destino pode ter vários caracteres, por exemplo, ö:oe, β:ss.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-813">The target can have multiple characters, for example ö:oe, β:ss.</span></span>
* <span data-ttu-id="5a3e9-814">O destino pode ser vazio, o que indica que o caractere deve ser removido.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-814">The target can be empty indicating that the character should be removed.</span></span>
* <span data-ttu-id="5a3e9-815">A origem diferencia as letras maiúsculas de minúsculas e deve ser uma correspondência exata.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-815">The source is case-sensitive and must be an exact match.</span></span>
* <span data-ttu-id="5a3e9-816">A , (vírgula) e : (dois-pontos) são caracteres reservados e não podem ser substituídos usando essa função.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-816">The , (comma) and : (colon) are reserved characters and cannot be replaced using this function.</span></span>
* <span data-ttu-id="5a3e9-817">Espaços e outros caracteres em branco na cadeia de caracteres ReplacePattern são ignorados.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-817">Spaces and other white characters in the ReplacePattern string are ignored.</span></span>

<span data-ttu-id="5a3e9-818">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-818">**Example:**</span></span>  
`%ReplaceString% = ’:,Å:A,Ä:A,Ö:O,å:a,ä:a,ö,o`

`ReplaceChars("Räksmörgås",%ReplaceString%)`  
<span data-ttu-id="5a3e9-819">retorna Raksmorgas</span><span class="sxs-lookup"><span data-stu-id="5a3e9-819">Returns Raksmorgas</span></span>

`ReplaceChars("O’Neil",%ReplaceString%)`  
<span data-ttu-id="5a3e9-820">retorna "ONeil", o único tique é definido para ser removido.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-820">Returns "ONeil", the single tick is defined to be removed.</span></span>

- - -
### <a name="right"></a><span data-ttu-id="5a3e9-821">Right</span><span class="sxs-lookup"><span data-stu-id="5a3e9-821">Right</span></span>
<span data-ttu-id="5a3e9-822">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-822">**Description:**</span></span>  
<span data-ttu-id="5a3e9-823">a função Right retorna um número especificado de caracteres a partir da direita (final) de uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-823">The Right function returns a specified number of characters from the right (end) of a string.</span></span>

<span data-ttu-id="5a3e9-824">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-824">**Syntax:**</span></span>  
`str Right(str string, num NumChars)`

* <span data-ttu-id="5a3e9-825">string: a cadeia de caracteres da qual retornar caracteres</span><span class="sxs-lookup"><span data-stu-id="5a3e9-825">string: the string to return characters from</span></span>
* <span data-ttu-id="5a3e9-826">NumChars: um número que identifica o número de caracteres a ser retornado  do final (direita) da cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5a3e9-826">NumChars: a number identifying the number of characters to return from the end (right) of string</span></span>

<span data-ttu-id="5a3e9-827">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-827">**Remarks:**</span></span>  
<span data-ttu-id="5a3e9-828">os caracteres de NumChars são retornados a partir da última posição da cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-828">NumChars characters are returned from the last position of string.</span></span>

<span data-ttu-id="5a3e9-829">Uma cadeia de caracteres que contém os últimos caracteres numChars na cadeia de caracteres:</span><span class="sxs-lookup"><span data-stu-id="5a3e9-829">A string containing the last numChars characters in string:</span></span>

* <span data-ttu-id="5a3e9-830">Se numChars = 0, retorne a cadeia de caracteres vazia.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-830">If numChars = 0, return empty string.</span></span>
* <span data-ttu-id="5a3e9-831">Se numChars < 0, retorne a cadeia de caracteres de entrada.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-831">If numChars < 0, return input string.</span></span>
* <span data-ttu-id="5a3e9-832">Se a cadeia de caracteres for nula, retorne a cadeia de caracteres vazia.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-832">If string is null, return empty string.</span></span>

<span data-ttu-id="5a3e9-833">Se a cadeia de caracteres contém menos caracteres do que o número especificado em NumChars, uma cadeia de caracteres idêntica à cadeia de caracteres será retornada.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-833">If string contains fewer characters than the number specified in NumChars, a string identical to string is returned.</span></span>

<span data-ttu-id="5a3e9-834">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-834">**Example:**</span></span>  
`Right("John Doe", 3)`  
<span data-ttu-id="5a3e9-835">retorna "Doe".</span><span class="sxs-lookup"><span data-stu-id="5a3e9-835">Returns "Doe".</span></span>

- - -
### <a name="rtrim"></a><span data-ttu-id="5a3e9-836">RTrim</span><span class="sxs-lookup"><span data-stu-id="5a3e9-836">RTrim</span></span>
<span data-ttu-id="5a3e9-837">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-837">**Description:**</span></span>  
<span data-ttu-id="5a3e9-838">a função RTrim remove os espaços em branco à direita de uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-838">The RTrim function removes trailing white spaces from a string.</span></span>

<span data-ttu-id="5a3e9-839">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-839">**Syntax:**</span></span>  
`str RTrim(str value)`

<span data-ttu-id="5a3e9-840">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-840">**Example:**</span></span>  
`RTrim(" Test ")`  
<span data-ttu-id="5a3e9-841">retorna "Test".</span><span class="sxs-lookup"><span data-stu-id="5a3e9-841">Returns " Test".</span></span>

- - -
### <a name="select"></a><span data-ttu-id="5a3e9-842">Selecionar</span><span class="sxs-lookup"><span data-stu-id="5a3e9-842">Select</span></span>
<span data-ttu-id="5a3e9-843">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-843">**Description:**</span></span>  
<span data-ttu-id="5a3e9-844">Processa todos os valores em um atributo de valores múltiplos (ou a saída de uma expressão) com base na função especificada.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-844">Process all values in a multi-valued attribute (or output of an expression) based on function specified.</span></span>

<span data-ttu-id="5a3e9-845">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-845">**Syntax:**</span></span>  
`mvattr Select(variable item, mvattr attribute, func function)`  
`mvattr Select(variable item, exp expression, func function)`

* <span data-ttu-id="5a3e9-846">item: representa um elemento no atributo de valores múltiplos</span><span class="sxs-lookup"><span data-stu-id="5a3e9-846">item: Represents an element in the multi-valued attribute</span></span>
* <span data-ttu-id="5a3e9-847">attribute: o atributo de valores múltiplos</span><span class="sxs-lookup"><span data-stu-id="5a3e9-847">attribute: the multi-valued attribute</span></span>
* <span data-ttu-id="5a3e9-848">expression: uma expressão que retorna uma coleção de valores</span><span class="sxs-lookup"><span data-stu-id="5a3e9-848">expression: an expression that returns a collection of values</span></span>
* <span data-ttu-id="5a3e9-849">condition: qualquer função que possa processar um item no atributo</span><span class="sxs-lookup"><span data-stu-id="5a3e9-849">condition: any function that can process an item in the attribute</span></span>

<span data-ttu-id="5a3e9-850">**Exemplos:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-850">**Examples:**</span></span>  
`Select($item,[otherPhone],Replace($item,“-”,“”))`  
<span data-ttu-id="5a3e9-851">Retorna todos os valores no atributo de valores múltiplos otherPhone depois que os hifens (-) foram removidos.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-851">Return all the values in the multi-valued attribute otherPhone after hyphens (-) have been removed.</span></span>

- - -
### <a name="split"></a><span data-ttu-id="5a3e9-852">Divisão</span><span class="sxs-lookup"><span data-stu-id="5a3e9-852">Split</span></span>
<span data-ttu-id="5a3e9-853">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-853">**Description:**</span></span>  
<span data-ttu-id="5a3e9-854">a função Split obtém uma cadeia de caracteres separada por um delimitador e transforma-a em uma cadeia de caracteres de valores múltiplos.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-854">The Split function takes a string separated with a delimiter and makes it a multi-valued string.</span></span>

<span data-ttu-id="5a3e9-855">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-855">**Syntax:**</span></span>  
`mvstr Split(str value, str delimiter)`  
`mvstr Split(str value, str delimiter, num limit)`

* <span data-ttu-id="5a3e9-856">valor: a cadeia de caracteres com um caractere delimitador para separar.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-856">value: the string with a delimiter character to separate.</span></span>
* <span data-ttu-id="5a3e9-857">delimitador: um único caractere a ser usado como o delimitador.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-857">delimiter: single character to be used as the delimiter.</span></span>
* <span data-ttu-id="5a3e9-858">limite: o número máximo de valores que podem ser retornados.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-858">limit: maximum number of values that can return.</span></span>

<span data-ttu-id="5a3e9-859">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-859">**Example:**</span></span>  
`Split("SMTP:john.doe@contoso.com,smtp:jd@contoso.com",",")`  
<span data-ttu-id="5a3e9-860">retorna uma cadeia de caracteres de valores múltiplos com dois elementos úteis para o atributo proxyAddress.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-860">Returns a multi-valued string with 2 elements useful for the proxyAddress attribute.</span></span>

- - -
### <a name="stringfromguid"></a><span data-ttu-id="5a3e9-861">StringFromGuid</span><span class="sxs-lookup"><span data-stu-id="5a3e9-861">StringFromGuid</span></span>
<span data-ttu-id="5a3e9-862">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-862">**Description:**</span></span>  
<span data-ttu-id="5a3e9-863">a função StringFromGuid obtém um GUID binário e converte-o em uma cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5a3e9-863">The StringFromGuid function takes a binary GUID and converts it to a string</span></span>

<span data-ttu-id="5a3e9-864">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-864">**Syntax:**</span></span>  
`str StringFromGuid(bin GUID)`

- - -
### <a name="stringfromsid"></a><span data-ttu-id="5a3e9-865">StringFromSid</span><span class="sxs-lookup"><span data-stu-id="5a3e9-865">StringFromSid</span></span>
<span data-ttu-id="5a3e9-866">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-866">**Description:**</span></span>  
<span data-ttu-id="5a3e9-867">a função StringFromSid converte uma matriz de bytes, que contém um identificador de segurança, em uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-867">The StringFromSid function converts a byte array containing a security identifier to a string.</span></span>

<span data-ttu-id="5a3e9-868">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-868">**Syntax:**</span></span>  
`str StringFromSid(bin ObjectSID)`  

- - -
### <a name="switch"></a><span data-ttu-id="5a3e9-869">Switch</span><span class="sxs-lookup"><span data-stu-id="5a3e9-869">Switch</span></span>
<span data-ttu-id="5a3e9-870">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-870">**Description:**</span></span>  
<span data-ttu-id="5a3e9-871">a função Switch é usada para retornar um único valor com base nas condições avaliadas.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-871">The Switch function is used to return a single value based on evaluated conditions.</span></span>

<span data-ttu-id="5a3e9-872">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-872">**Syntax:**</span></span>  
`var Switch(exp expr1, var value1[, exp expr2, var value … [, exp expr, var valueN]])`

* <span data-ttu-id="5a3e9-873">expr: expressão variante que você deseja avaliar.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-873">expr: Variant expression you want to evaluate.</span></span>
* <span data-ttu-id="5a3e9-874">value: valor a ser retornado se a expressão correspondente for True.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-874">value: Value to be returned if the corresponding expression is True.</span></span>

<span data-ttu-id="5a3e9-875">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-875">**Remarks:**</span></span>  
<span data-ttu-id="5a3e9-876">a lista de argumentos da função Switch consiste em pares de expressões e valores.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-876">The Switch function argument list consists of pairs of expressions and values.</span></span> <span data-ttu-id="5a3e9-877">As expressões são avaliadas da esquerda para a direita e o valor associado à primeira expressão avaliada como True é retornado.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-877">The expressions are evaluated from left to right, and the value associated with the first expression to evaluate to True is returned.</span></span> <span data-ttu-id="5a3e9-878">Se as partes não tiverem pares adequados, ocorrerá um erro em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-878">If the parts aren't properly paired, a run-time error occurs.</span></span>

<span data-ttu-id="5a3e9-879">Por exemplo, se expr1 for True, o comutador retornará valor1.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-879">For example, if expr1 is True, Switch returns value1.</span></span> <span data-ttu-id="5a3e9-880">Se expr-1 for False, mas expr-2 for True, Switch retorna valor-2 e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-880">If expr-1 is False, but expr-2 is True, Switch returns value-2, and so on.</span></span>

<span data-ttu-id="5a3e9-881">Switch retorna um Nothing se:</span><span class="sxs-lookup"><span data-stu-id="5a3e9-881">Switch returns a Nothing if:</span></span>

* <span data-ttu-id="5a3e9-882">Nenhuma das expressões são True.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-882">None of the expressions are True.</span></span>
* <span data-ttu-id="5a3e9-883">A primeira expressão True tem um valor correspondente que é Null.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-883">The first True expression has a corresponding value that is Null.</span></span>

<span data-ttu-id="5a3e9-884">Switch avalia todas as expressões, mesmo que retorne apenas uma delas.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-884">Switch evaluates all expressions, even though it returns only one of them.</span></span> <span data-ttu-id="5a3e9-885">Por essa razão, você deve tomar cuidado com efeitos colaterais indesejáveis.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-885">For this reason, you should watch for undesirable side effects.</span></span> <span data-ttu-id="5a3e9-886">Por exemplo, se a avaliação de qualquer expressão resulta em um erro de divisão por zero, ocorrerá um erro.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-886">For example, if the evaluation of any expression results in a division by zero error, an error occurs.</span></span>

<span data-ttu-id="5a3e9-887">O valor também pode ser a função Error, que retornaria uma cadeia de caracteres personalizada.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-887">Value can also be the Error function, which would return a custom string.</span></span>

<span data-ttu-id="5a3e9-888">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-888">**Example:**</span></span>  
`Switch([city] = "London", "English", [city] = "Rome", "Italian", [city] = "Paris", "French", True, Error("Unknown city"))`  
<span data-ttu-id="5a3e9-889">retorna o idioma falado em algumas das maiores cidades; caso contrário, retorna um Erro.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-889">Returns the language spoken in some major cities, otherwise returns an Error.</span></span>

- - -
### <a name="trim"></a><span data-ttu-id="5a3e9-890">Trim</span><span class="sxs-lookup"><span data-stu-id="5a3e9-890">Trim</span></span>
<span data-ttu-id="5a3e9-891">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-891">**Description:**</span></span>  
<span data-ttu-id="5a3e9-892">a função Trim remove os espaços em branco à esquerda e à direita de uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-892">The Trim function removes leading and trailing white spaces from a string.</span></span>

<span data-ttu-id="5a3e9-893">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-893">**Syntax:**</span></span>  
`str Trim(str value)`  

<span data-ttu-id="5a3e9-894">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-894">**Example:**</span></span>  
`Trim(" Test ")`  
<span data-ttu-id="5a3e9-895">retorna "test".</span><span class="sxs-lookup"><span data-stu-id="5a3e9-895">Returns "Test".</span></span>

`Trim([proxyAddresses])`  
<span data-ttu-id="5a3e9-896">remove espaços à direita e à esquerda para cada valor no atributo proxyAddress.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-896">Removes leading and trailing spaces for each value in the proxyAddress attribute.</span></span>

- - -
### <a name="ucase"></a><span data-ttu-id="5a3e9-897">UCase</span><span class="sxs-lookup"><span data-stu-id="5a3e9-897">UCase</span></span>
<span data-ttu-id="5a3e9-898">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-898">**Description:**</span></span>  
<span data-ttu-id="5a3e9-899">a função UCase converte todos os caracteres de uma cadeia de caracteres em letras maiúsculas.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-899">The UCase function converts all characters in a string to upper case.</span></span>

<span data-ttu-id="5a3e9-900">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-900">**Syntax:**</span></span>  
`str UCase(str string)`

<span data-ttu-id="5a3e9-901">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-901">**Example:**</span></span>  
`UCase("TeSt")`  
<span data-ttu-id="5a3e9-902">retorna "test".</span><span class="sxs-lookup"><span data-stu-id="5a3e9-902">Returns "TEST".</span></span>

- - -
### <a name="where"></a><span data-ttu-id="5a3e9-903">Where</span><span class="sxs-lookup"><span data-stu-id="5a3e9-903">Where</span></span>

<span data-ttu-id="5a3e9-904">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-904">**Description:**</span></span>  
<span data-ttu-id="5a3e9-905">Retorna um subconjunto de valores de um atributo de valores múltiplos (ou a saída de uma expressão) com base em uma condição específica.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-905">Returns a subset of values from a multi-valued attribute (or output of an expression) based on specific condition.</span></span>

<span data-ttu-id="5a3e9-906">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-906">**Syntax:**</span></span>  
`mvattr Where(variable item, mvattr attribute, exp condition)`  
`mvattr Where(variable item, exp expression, exp condition)`  
* <span data-ttu-id="5a3e9-907">item: representa um elemento no atributo de valores múltiplos</span><span class="sxs-lookup"><span data-stu-id="5a3e9-907">item: Represents an element in the multi-valued attribute</span></span>
* <span data-ttu-id="5a3e9-908">attribute: o atributo de valores múltiplos</span><span class="sxs-lookup"><span data-stu-id="5a3e9-908">attribute: the multi-valued attribute</span></span>
* <span data-ttu-id="5a3e9-909">condition: qualquer expressão que possa ser avaliada como verdadeira ou falsa</span><span class="sxs-lookup"><span data-stu-id="5a3e9-909">condition: any expression that can be evaluated to true or false</span></span>
* <span data-ttu-id="5a3e9-910">expression: uma expressão que retorna uma coleção de valores</span><span class="sxs-lookup"><span data-stu-id="5a3e9-910">expression: an expression that returns a collection of values</span></span>

<span data-ttu-id="5a3e9-911">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-911">**Example:**</span></span>  
`Where($item,[userCertificate],CertNotAfter($item)>Now())`  
<span data-ttu-id="5a3e9-912">Retorna os valores do certificado no atributo de valores múltiplos userCertificate que não estão expirados.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-912">Return the certificate values in the multi-valued attribute userCertificate which aren’t expired.</span></span>

- - -
### <a name="with"></a><span data-ttu-id="5a3e9-913">With</span><span class="sxs-lookup"><span data-stu-id="5a3e9-913">With</span></span>
<span data-ttu-id="5a3e9-914">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-914">**Description:**</span></span>  
<span data-ttu-id="5a3e9-915">A função With fornece uma maneira para simplificar uma expressão complexa, usando uma variável para representar uma subexpressão que aparece uma ou mais vezes na expressão complexa.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-915">The With function provides a way to simplify a complex expression by using a variable to represent a subexpression which appears one or more times in the complex expression.</span></span>

<span data-ttu-id="5a3e9-916">**Sintaxe:**
`With(var variable, exp subExpression, exp complexExpression)`</span><span class="sxs-lookup"><span data-stu-id="5a3e9-916">**Syntax:**
`With(var variable, exp subExpression, exp complexExpression)`</span></span>  
* <span data-ttu-id="5a3e9-917">variable: representa a subexpressão.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-917">variable: Represents the subexpression.</span></span>
* <span data-ttu-id="5a3e9-918">subExpression: a subexpressão representada pela variável.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-918">subExpression: subexpression represented by variable.</span></span>
* <span data-ttu-id="5a3e9-919">complexExpression: uma expressão complexa.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-919">complexExpression: A complex expression.</span></span>

<span data-ttu-id="5a3e9-920">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-920">**Example:**</span></span>  
`With($unExpiredCerts,Where($item,[userCertificate],CertNotAfter($item)>Now()),IIF(Count($unExpiredCerts)>0,$unExpiredCerts,NULL))`  
<span data-ttu-id="5a3e9-921">É funcionalmente equivalente à:</span><span class="sxs-lookup"><span data-stu-id="5a3e9-921">Is functionally equivalent to:</span></span>  
`IIF (Count(Where($item,[userCertificate],CertNotAfter($item)>Now()))>0, Where($item,[userCertificate],CertNotAfter($item)>Now()),NULL)`  
<span data-ttu-id="5a3e9-922">Que retorna apenas os valores de certificado não expirados no atributo userCertificate.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-922">Which returns only unexpired certificate values in the userCertificate attribute.</span></span>


- - -
### <a name="word"></a><span data-ttu-id="5a3e9-923">Word</span><span class="sxs-lookup"><span data-stu-id="5a3e9-923">Word</span></span>
<span data-ttu-id="5a3e9-924">**Descrição:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-924">**Description:**</span></span>  
<span data-ttu-id="5a3e9-925">a função Word retorna uma palavra contida em uma cadeia de caracteres com base nos parâmetros que descrevem os delimitadores a serem usados e o número de palavras a serem retornadas.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-925">The Word function returns a word contained within a string, based on parameters describing the delimiters to use and the word number to return.</span></span>

<span data-ttu-id="5a3e9-926">**Sintaxe:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-926">**Syntax:**</span></span>  
`str Word(str string, num WordNumber, str delimiters)`

* <span data-ttu-id="5a3e9-927">string: a cadeia de caracteres da qual retornar uma palavra</span><span class="sxs-lookup"><span data-stu-id="5a3e9-927">string: the string to return a word from.</span></span>
* <span data-ttu-id="5a3e9-928">WordNumber: um número que identifica qual número de palavras deve retornar.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-928">WordNumber: a number identifying which word number should return.</span></span>
* <span data-ttu-id="5a3e9-929">delimitadores: uma cadeia de caracteres que representa o delimitador(es) que deve ser usado para identificar palavras</span><span class="sxs-lookup"><span data-stu-id="5a3e9-929">delimiters: a string representing the delimiter(s) that should be used to identify words</span></span>

<span data-ttu-id="5a3e9-930">**Comentários:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-930">**Remarks:**</span></span>  
<span data-ttu-id="5a3e9-931">cada cadeia de caracteres separada por um dos caracteres delimitadores na cadeia de caracteres é identificada como palavra:</span><span class="sxs-lookup"><span data-stu-id="5a3e9-931">Each string of characters in string separated by the one of the characters in delimiters are identified as words:</span></span>

* <span data-ttu-id="5a3e9-932">Se number < 1, retorna uma cadeia de caracteres vazia.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-932">If number < 1, returns empty string.</span></span>
* <span data-ttu-id="5a3e9-933">Se a cadeia de caracteres for nula, retorna a cadeia de caracteres vazia.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-933">If string is null, returns empty string.</span></span>

<span data-ttu-id="5a3e9-934">Se a cadeia de caracteres for menor que o número de palavras ou a cadeia não contiver nenhuma palavra identificada por delimitadores, uma cadeia de caracteres vazia será retornada.</span><span class="sxs-lookup"><span data-stu-id="5a3e9-934">If string contains less than number words, or string does not contain any words identified by delimiters, an empty string is returned.</span></span>

<span data-ttu-id="5a3e9-935">**Exemplo:**</span><span class="sxs-lookup"><span data-stu-id="5a3e9-935">**Example:**</span></span>  
`Word("The quick brown fox",3," ")`  
<span data-ttu-id="5a3e9-936">retorna "brown"</span><span class="sxs-lookup"><span data-stu-id="5a3e9-936">Returns "brown"</span></span>

`Word("This,string!has&many separators",3,",!&#")`  
<span data-ttu-id="5a3e9-937">retornaria "has"</span><span class="sxs-lookup"><span data-stu-id="5a3e9-937">Would return "has"</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5a3e9-938">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="5a3e9-938">Additional Resources</span></span>
* [<span data-ttu-id="5a3e9-939">Noções básicas sobre expressões de provisionamento declarativo</span><span class="sxs-lookup"><span data-stu-id="5a3e9-939">Understanding Declarative Provisioning Expressions</span></span>](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)
* [<span data-ttu-id="5a3e9-940">Azure AD Connect Sync: personalizando opções de sincronização</span><span class="sxs-lookup"><span data-stu-id="5a3e9-940">Azure AD Connect Sync: Customizing Synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="5a3e9-941">Integração de suas identidades locais com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="5a3e9-941">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
