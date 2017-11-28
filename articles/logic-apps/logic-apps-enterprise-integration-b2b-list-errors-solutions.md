---
title: "Lista de erros e soluções de Aplicativos Lógicos B2B: Serviço de Aplicativo do Azure | Microsoft Docs"
description: "Lista de erros e soluções de Aplicativos Lógicos B2B"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 1865d75f1b4c2aa18d5a3130f639572d19563b3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="logic-apps-b2b-list-of-errors-and-solutions"></a><span data-ttu-id="45773-103">Lista de erros e soluções de Aplicativos Lógicos B2B</span><span class="sxs-lookup"><span data-stu-id="45773-103">Logic Apps B2B list of errors and solutions</span></span>  
<span data-ttu-id="45773-104">Este artigo ajuda você a solucionar problemas de erros que podem ocorrer em cenários de Aplicativos Lógicos B2B e sugere ações adequadas para corrigir esses erros.</span><span class="sxs-lookup"><span data-stu-id="45773-104">This article helps you troubleshoot errors that might happen in Logic Apps B2B scenarios and suggests appropriate actions for correcting those errors.</span></span>


## <a name="agreement-resolution"></a><span data-ttu-id="45773-105">Resolução do contrato</span><span class="sxs-lookup"><span data-stu-id="45773-105">Agreement Resolution</span></span>

### <a name="no-agreement-found"></a><span data-ttu-id="45773-106">*Nenhum contrato encontrado</span><span class="sxs-lookup"><span data-stu-id="45773-106">*No agreement found</span></span> 

|   |   |  
|---|---|
| <span data-ttu-id="45773-107">Descrição do erro</span><span class="sxs-lookup"><span data-stu-id="45773-107">Error description</span></span> | <span data-ttu-id="45773-108">Não foi encontrado nenhum contrato com os Parâmetros de Resolução de Contrato</span><span class="sxs-lookup"><span data-stu-id="45773-108">No agreement found with Agreement Resolution Parameters</span></span>|    
| <span data-ttu-id="45773-109">Ação do usuário</span><span class="sxs-lookup"><span data-stu-id="45773-109">User action</span></span> | <span data-ttu-id="45773-110">O contrato deve ser adicionado à conta de integração com identidades comerciais acordadas.</span><span class="sxs-lookup"><span data-stu-id="45773-110">The agreement should be added to the integration account with agreed business identities.</span></span></br> <span data-ttu-id="45773-111">As identidades comerciais devem corresponder às IDs de mensagem de entrada</span><span class="sxs-lookup"><span data-stu-id="45773-111">The business identities should match to the input message ids</span></span>|  
|   |   |

### <a name="-no-agreement-found-with-identities"></a><span data-ttu-id="45773-112">* Não foi encontrado nenhum contrato com identidades</span><span class="sxs-lookup"><span data-stu-id="45773-112">* No agreement found with identities</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="45773-113">Descrição do erro</span><span class="sxs-lookup"><span data-stu-id="45773-113">Error description</span></span> | <span data-ttu-id="45773-114">Não foi encontrado nenhum contrato com as identidades: 'AS2Identity'::'Partner1' e 'AS2Identity'::'Partner3'</span><span class="sxs-lookup"><span data-stu-id="45773-114">No agreement found with identities: 'AS2Identity'::'Partner1' and'AS2Identity'::'Partner3'</span></span>| 
| <span data-ttu-id="45773-115">Ação do usuário</span><span class="sxs-lookup"><span data-stu-id="45773-115">User action</span></span> | <span data-ttu-id="45773-116">AS2-From ou AS2-To inválido configurado para o contrato.</span><span class="sxs-lookup"><span data-stu-id="45773-116">Invalid AS2-From or AS2-To configured for agreement.</span></span> </br> <span data-ttu-id="45773-117">Corrigir os cabeçalhos AS2-From ou AS2-To da mensagem AS2 ou o contrato para corresponder as IDs do AS2 nos cabeçalhos de mensagem AS2 com as configurações de contrato</span><span class="sxs-lookup"><span data-stu-id="45773-117">Correct AS2 message AS2-From or AS2-To headers or agreement to match AS2 ids in AS2 message headers with agreement configurations</span></span> |
|   |   |     

## <a name="as2"></a><span data-ttu-id="45773-118">AS2</span><span class="sxs-lookup"><span data-stu-id="45773-118">AS2</span></span>

### <a name="-missing-as2-message-headers"></a><span data-ttu-id="45773-119">* Cabeçalhos de mensagem AS2 ausentes</span><span class="sxs-lookup"><span data-stu-id="45773-119">* Missing AS2 message headers</span></span>  

|   |   |  
|---|---|
| <span data-ttu-id="45773-120">Descrição do erro</span><span class="sxs-lookup"><span data-stu-id="45773-120">Error description</span></span>| <span data-ttu-id="45773-121">Cabeçalhos de AS2 inválidos.</span><span class="sxs-lookup"><span data-stu-id="45773-121">Invalid AS2 headers.</span></span> <span data-ttu-id="45773-122">Um dos cabeçalhos “AS2-To” ou “AS2-From” está vazio</span><span class="sxs-lookup"><span data-stu-id="45773-122">One of 'AS2-To' or 'AS2-From' headers are empty</span></span>| 
| <span data-ttu-id="45773-123">Ação do usuário</span><span class="sxs-lookup"><span data-stu-id="45773-123">User action</span></span> | <span data-ttu-id="45773-124">Foi recebida uma mensagem AS2 que não continha o cabeçalho AS2-From ou AS2-To ou ambos.</span><span class="sxs-lookup"><span data-stu-id="45773-124">An AS2 message was received that did not contain the AS2-From or AS2-To or both headers.</span></span> </br> <span data-ttu-id="45773-125">Verificar os cabeçalhos AS2-From e AS2-To da mensagem AS2 e corrija-os com base na configuração do contrato</span><span class="sxs-lookup"><span data-stu-id="45773-125">Check AS2 message AS2-From and AS2-To headers and correct them based on agreement configuration</span></span> |
|  |  | 


### <a name="-missing-as2-message-body-and-headers"></a><span data-ttu-id="45773-126">* Cabeçalhos e corpo da mensagem AS2 ausentes</span><span class="sxs-lookup"><span data-stu-id="45773-126">* Missing AS2 message body and headers</span></span>    

|   |   |  
|---|---|
| <span data-ttu-id="45773-127">Descrição do erro</span><span class="sxs-lookup"><span data-stu-id="45773-127">Error description</span></span>| <span data-ttu-id="45773-128">O conteúdo da solicitação é nulo ou vazio</span><span class="sxs-lookup"><span data-stu-id="45773-128">The request content is null or empty</span></span> | 
| <span data-ttu-id="45773-129">Ação do usuário</span><span class="sxs-lookup"><span data-stu-id="45773-129">User action</span></span> | <span data-ttu-id="45773-130">Foi recebida uma mensagem AS2 que não continha o corpo da mensagem</span><span class="sxs-lookup"><span data-stu-id="45773-130">An AS2 message was received that did not contain the message body</span></span> |
|  |  | 

### <a name="-as2-message-decryption-failure"></a><span data-ttu-id="45773-131">* Falha na descriptografia mensagem AS2</span><span class="sxs-lookup"><span data-stu-id="45773-131">* AS2 message decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="45773-132">Descrição do erro</span><span class="sxs-lookup"><span data-stu-id="45773-132">Error description</span></span> |  <span data-ttu-id="45773-133">[processado/Erro: falha na descriptografia]</span><span class="sxs-lookup"><span data-stu-id="45773-133">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="45773-134">Ação do usuário</span><span class="sxs-lookup"><span data-stu-id="45773-134">User action</span></span> | <span data-ttu-id="45773-135">Adicionar @base64ToBinary à AS2Message antes de enviar ao parceiro</span><span class="sxs-lookup"><span data-stu-id="45773-135">Add @base64ToBinary to AS2Message before sending to partner</span></span> 
```java
            "HTTP": {
                "inputs": {
                    "body": "@base64ToBinary(body('Encode_to_AS2_message')?['AS2Message']?['Content'])",
                    "headers": "@body('Encode_to_AS2_message')?['AS2Message']?['OutboundHeaders']",
                    "method": "POST",
                    "uri": "xxxxx.xxx"
                },
                
``` 

### <a name="-mdn-decryption-failure"></a><span data-ttu-id="45773-136">* Falha na descriptografia do MDN</span><span class="sxs-lookup"><span data-stu-id="45773-136">* MDN decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="45773-137">Descrição do erro</span><span class="sxs-lookup"><span data-stu-id="45773-137">Error description</span></span> |  <span data-ttu-id="45773-138">[processado/Erro: falha na descriptografia]</span><span class="sxs-lookup"><span data-stu-id="45773-138">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="45773-139">Ação do usuário</span><span class="sxs-lookup"><span data-stu-id="45773-139">User action</span></span> | <span data-ttu-id="45773-140">Adicionar @base64ToBinary ao MDN antes de enviar ao parceiro</span><span class="sxs-lookup"><span data-stu-id="45773-140">Add @base64ToBinary to MDN before sending to partner</span></span> 
```java
            "Response": {
                "inputs": {
                    "body": "@base64ToBinary(body('Decode_AS2_message')?['OutgoingMDN']?['Content'])",
                    "headers": "@body('Decode_AS2_message')?['OutgoingMDN']?['OutboundHeaders']",
                    "statusCode": 200
                },
                
``` 

### <a name="-missing-signing-certificate"></a><span data-ttu-id="45773-141">* Certificado de assinatura ausente</span><span class="sxs-lookup"><span data-stu-id="45773-141">* Missing signing certificate</span></span>

|   |   |  
|---|---|
| <span data-ttu-id="45773-142">Descrição do erro</span><span class="sxs-lookup"><span data-stu-id="45773-142">Error description</span></span>| <span data-ttu-id="45773-143">O certificado de autenticação não foi configurado para a parte do AS2.</span><span class="sxs-lookup"><span data-stu-id="45773-143">The Signing Certificate has not been configured for AS2 party.</span></span> </br> <span data-ttu-id="45773-144">AS2-From: partner1 AS2-To: partner2</span><span class="sxs-lookup"><span data-stu-id="45773-144">AS2-From: partner1 AS2-To: partner2</span></span> | 
| <span data-ttu-id="45773-145">Ação do usuário</span><span class="sxs-lookup"><span data-stu-id="45773-145">User action</span></span> | <span data-ttu-id="45773-146">Definir as configurações do contrato AS2 com o certificado correto para assinatura</span><span class="sxs-lookup"><span data-stu-id="45773-146">Configure AS2 agreement settings with correct certificate for signature</span></span> |
|  |  | 

## <a name="x12-and-edifact"></a><span data-ttu-id="45773-147">X12 e EDIFACT</span><span class="sxs-lookup"><span data-stu-id="45773-147">X12 and EDIFACT</span></span>

### <a name="-leading-or-trailing-space-found"></a><span data-ttu-id="45773-148">* Espaço à esquerda ou à direita encontrado</span><span class="sxs-lookup"><span data-stu-id="45773-148">* Leading or trailing space found</span></span>    
    
|   |   | 
|---|---|
| <span data-ttu-id="45773-149">Descrição do erro</span><span class="sxs-lookup"><span data-stu-id="45773-149">Error description</span></span> | <span data-ttu-id="45773-150">Erro encontrado durante a análise.</span><span class="sxs-lookup"><span data-stu-id="45773-150">Error encountered during parsing.</span></span> <span data-ttu-id="45773-151">O conjunto de transações Edifact com ID “123456” contido no intercâmbio (sem grupo) com a ID’987654”, com a ID de remetente “Partner1”, ID do receptor “Partner2”, está sendo suspenso com os seguintes erros: Separador à direita/esquerda encontrado</span><span class="sxs-lookup"><span data-stu-id="45773-151">The Edifact transaction set with id '123456' contained in interchange (without group) with id '987654', with sender id 'Partner1', receiver id 'Partner2' is being suspended with following errors: Leading Trailing separator found</span></span> |
| <span data-ttu-id="45773-152">Ação do usuário</span><span class="sxs-lookup"><span data-stu-id="45773-152">User action</span></span> | <span data-ttu-id="45773-153">As configurações de contrato a serem configuradas para permitir o espaço à esquerda e à direita.</span><span class="sxs-lookup"><span data-stu-id="45773-153">The agreement settings to be configured to allow leading and trailing space.</span></span> </br> <span data-ttu-id="45773-154">Editar as configurações do contrato para permitir o espaço à esquerda e à direita</span><span class="sxs-lookup"><span data-stu-id="45773-154">Edit agreement settings to allow leading and trailing space</span></span> |
|   |   |

![permitir espaço](./media/logic-apps-enterprise-integration-b2b-list-errors-solutions/leadingandtrailing.png)

### <a name="-duplicate-check-has-enabled-in-the-agreement"></a><span data-ttu-id="45773-156">* A verificação dupla foi habilitada no contrato</span><span class="sxs-lookup"><span data-stu-id="45773-156">* Duplicate check has enabled in the agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="45773-157">Descrição do erro</span><span class="sxs-lookup"><span data-stu-id="45773-157">Error description</span></span> | <span data-ttu-id="45773-158">Duplicar Número de Controle</span><span class="sxs-lookup"><span data-stu-id="45773-158">Duplicate Control Number</span></span> |
| <span data-ttu-id="45773-159">Ação do usuário</span><span class="sxs-lookup"><span data-stu-id="45773-159">User action</span></span> | <span data-ttu-id="45773-160">Esse erro indica que a mensagem recebida tem números de controle duplicados.</span><span class="sxs-lookup"><span data-stu-id="45773-160">This error indicates the received message has duplicate control numbers.</span></span> </br> <span data-ttu-id="45773-161">Corrigir o número de controle e reenviar a mensagem</span><span class="sxs-lookup"><span data-stu-id="45773-161">Correct the control number and resend the message</span></span> |
|   |   |

### <a name="-missing-schema-in-the-agreement"></a><span data-ttu-id="45773-162">* Esquema ausente no contrato</span><span class="sxs-lookup"><span data-stu-id="45773-162">* Missing schema in the agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="45773-163">Descrição do erro</span><span class="sxs-lookup"><span data-stu-id="45773-163">Error description</span></span> | <span data-ttu-id="45773-164">Erro encontrado durante a análise.</span><span class="sxs-lookup"><span data-stu-id="45773-164">Error encountered during parsing.</span></span> <span data-ttu-id="45773-165">O conjunto de transações X12 com a ID “564220001” contido no grupo funcional com ID “56422”, no intercâmbio com ID “000056422”, com a ID de remetente “12345678”, ID de receptor “87654321”, está sendo suspenso com os seguintes erros: “A mensagem tem um tipo de documento desconhecido e não foi resolvida para nenhum dos esquemas existentes configurados no contrato”</span><span class="sxs-lookup"><span data-stu-id="45773-165">The X12 transaction set with id '564220001' contained in functional group with id '56422', in interchange with id '000056422', with sender id '12345678       ', receiver id '87654321       ' is being suspended with following errors "The message has an unknown document type and did not resolve to any of the existing schemas configured in the agreement"</span></span> |
| <span data-ttu-id="45773-166">Ação do usuário</span><span class="sxs-lookup"><span data-stu-id="45773-166">User action</span></span> | <span data-ttu-id="45773-167">Configurar o esquema nas configurações do contrato</span><span class="sxs-lookup"><span data-stu-id="45773-167">Configure schema in the agreement settings</span></span>  |
|   |   |

### <a name="-incorrect-schema-in-the-agreement"></a><span data-ttu-id="45773-168">* Esquema incorreto no contrato</span><span class="sxs-lookup"><span data-stu-id="45773-168">* Incorrect schema in the agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="45773-169">Descrição do erro</span><span class="sxs-lookup"><span data-stu-id="45773-169">Error description</span></span> | <span data-ttu-id="45773-170">A mensagem tem um tipo de documento desconhecido e não foi resolvida para nenhum dos esquemas existentes configurados no contrato.</span><span class="sxs-lookup"><span data-stu-id="45773-170">The message has an unknown document type and did not resolve to any of the existing schemas configured in the agreement.</span></span> |
| <span data-ttu-id="45773-171">Ação do usuário</span><span class="sxs-lookup"><span data-stu-id="45773-171">User action</span></span> | <span data-ttu-id="45773-172">Configurar o esquema correto nas configurações do contrato</span><span class="sxs-lookup"><span data-stu-id="45773-172">Configure correct schema in the agreement settings</span></span>  |
|   |   |

## <a name="flat-file"></a><span data-ttu-id="45773-173">Arquivo simples</span><span class="sxs-lookup"><span data-stu-id="45773-173">Flat file</span></span>

### <a name="-input-message-with-no-body"></a><span data-ttu-id="45773-174">* Mensagem de entrada sem corpo</span><span class="sxs-lookup"><span data-stu-id="45773-174">* Input message with no body</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="45773-175">Descrição do erro</span><span class="sxs-lookup"><span data-stu-id="45773-175">Error description</span></span> | <span data-ttu-id="45773-176">InvalidTemplate.</span><span class="sxs-lookup"><span data-stu-id="45773-176">InvalidTemplate.</span></span> <span data-ttu-id="45773-177">Não é possível processar as expressões da linguagem do modelo nas entradas da ação “Flat_File_Decoding” na linha “1” e coluna “1902”: “A propriedade obrigatória “content” espera um valor, mas recebeu nulo.</span><span class="sxs-lookup"><span data-stu-id="45773-177">Unable to process template language expressions in action 'Flat_File_Decoding' inputs at line '1' and column '1902': 'Required property 'content' expects a value but got null.</span></span> <span data-ttu-id="45773-178">Caminho “”.”.</span><span class="sxs-lookup"><span data-stu-id="45773-178">Path ''.'.</span></span> |
| <span data-ttu-id="45773-179">Ação do usuário</span><span class="sxs-lookup"><span data-stu-id="45773-179">User action</span></span> | <span data-ttu-id="45773-180">Esse erro indica que a mensagem de entrada não contém um corpo</span><span class="sxs-lookup"><span data-stu-id="45773-180">This error indicates the input message does not contain a body</span></span> |
|   |   | 

## <a name="learn-more"></a><span data-ttu-id="45773-181">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="45773-181">Learn more</span></span>
[<span data-ttu-id="45773-182">Saiba mais sobre o Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="45773-182">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)