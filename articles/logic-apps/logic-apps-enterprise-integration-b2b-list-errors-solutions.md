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
ms.openlocfilehash: 0340e2979f1972ba631354e206c93969e55946e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-b2b-list-of-errors-and-solutions"></a><span data-ttu-id="39e2f-103">Lista de erros e soluções de Aplicativos Lógicos B2B</span><span class="sxs-lookup"><span data-stu-id="39e2f-103">Logic Apps B2B list of errors and solutions</span></span>  
<span data-ttu-id="39e2f-104">Este artigo ajuda você a solucionar problemas de erros que podem ocorrer em cenários de Aplicativos Lógicos B2B e sugere ações adequadas para corrigir esses erros.</span><span class="sxs-lookup"><span data-stu-id="39e2f-104">This article helps you troubleshoot errors that might happen in Logic Apps B2B scenarios and suggests appropriate actions for correcting those errors.</span></span>


## <a name="agreement-resolution"></a><span data-ttu-id="39e2f-105">Resolução do contrato</span><span class="sxs-lookup"><span data-stu-id="39e2f-105">Agreement Resolution</span></span>

### <a name="no-agreement-found"></a><span data-ttu-id="39e2f-106">*Nenhum contrato encontrado</span><span class="sxs-lookup"><span data-stu-id="39e2f-106">*No agreement found</span></span> 

|   |   |  
|---|---|
| <span data-ttu-id="39e2f-107">Descrição do erro</span><span class="sxs-lookup"><span data-stu-id="39e2f-107">Error description</span></span> | <span data-ttu-id="39e2f-108">Não foi encontrado nenhum contrato com os Parâmetros de Resolução de Contrato</span><span class="sxs-lookup"><span data-stu-id="39e2f-108">No agreement found with Agreement Resolution Parameters</span></span>|    
| <span data-ttu-id="39e2f-109">Ação do usuário</span><span class="sxs-lookup"><span data-stu-id="39e2f-109">User action</span></span> | <span data-ttu-id="39e2f-110">contrato Olá deve ser adicionado a conta de integração toohello com identidades comercial acordada.</span><span class="sxs-lookup"><span data-stu-id="39e2f-110">hello agreement should be added toohello integration account with agreed business identities.</span></span></br> <span data-ttu-id="39e2f-111">identidades de negócios Olá devem corresponder toohello ids de mensagem de entrada</span><span class="sxs-lookup"><span data-stu-id="39e2f-111">hello business identities should match toohello input message ids</span></span>|  
|   |   |

### <a name="-no-agreement-found-with-identities"></a><span data-ttu-id="39e2f-112">* Não foi encontrado nenhum contrato com identidades</span><span class="sxs-lookup"><span data-stu-id="39e2f-112">* No agreement found with identities</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="39e2f-113">Descrição do erro</span><span class="sxs-lookup"><span data-stu-id="39e2f-113">Error description</span></span> | <span data-ttu-id="39e2f-114">Não foi encontrado nenhum contrato com as identidades: 'AS2Identity'::'Partner1' e 'AS2Identity'::'Partner3'</span><span class="sxs-lookup"><span data-stu-id="39e2f-114">No agreement found with identities: 'AS2Identity'::'Partner1' and'AS2Identity'::'Partner3'</span></span>| 
| <span data-ttu-id="39e2f-115">Ação do usuário</span><span class="sxs-lookup"><span data-stu-id="39e2f-115">User action</span></span> | <span data-ttu-id="39e2f-116">AS2 inválido-de ou AS2-tooconfigured de acordo.</span><span class="sxs-lookup"><span data-stu-id="39e2f-116">Invalid AS2-From or AS2-tooconfigured for agreement.</span></span> </br> <span data-ttu-id="39e2f-117">Mensagem de AS2 correta AS2-de ou cabeçalhos com configurações de contrato de mensagem AS2 tooheaders ou contrato de ids de toomatch AS2 no AS2</span><span class="sxs-lookup"><span data-stu-id="39e2f-117">Correct AS2 message AS2-From or AS2-tooheaders or agreement toomatch AS2 ids in AS2 message headers with agreement configurations</span></span> |
|   |   |     

## <a name="as2"></a><span data-ttu-id="39e2f-118">AS2</span><span class="sxs-lookup"><span data-stu-id="39e2f-118">AS2</span></span>

### <a name="-missing-as2-message-headers"></a><span data-ttu-id="39e2f-119">* Cabeçalhos de mensagem AS2 ausentes</span><span class="sxs-lookup"><span data-stu-id="39e2f-119">* Missing AS2 message headers</span></span>  

|   |   |  
|---|---|
| <span data-ttu-id="39e2f-120">Descrição do erro</span><span class="sxs-lookup"><span data-stu-id="39e2f-120">Error description</span></span>| <span data-ttu-id="39e2f-121">Cabeçalhos de AS2 inválidos.</span><span class="sxs-lookup"><span data-stu-id="39e2f-121">Invalid AS2 headers.</span></span> <span data-ttu-id="39e2f-122">Um dos cabeçalhos “AS2-To” ou “AS2-From” está vazio</span><span class="sxs-lookup"><span data-stu-id="39e2f-122">One of 'AS2-To' or 'AS2-From' headers are empty</span></span>| 
| <span data-ttu-id="39e2f-123">Ação do usuário</span><span class="sxs-lookup"><span data-stu-id="39e2f-123">User action</span></span> | <span data-ttu-id="39e2f-124">Foi recebida uma mensagem AS2 que não continha Olá AS2-de ou AS2 tooor ambos os cabeçalhos.</span><span class="sxs-lookup"><span data-stu-id="39e2f-124">An AS2 message was received that did not contain hello AS2-From or AS2-tooor both headers.</span></span> </br> <span data-ttu-id="39e2f-125">Verifique a mensagem AS2 AS2-de e AS2-tooheaders e corrija-as com base na configuração do contrato</span><span class="sxs-lookup"><span data-stu-id="39e2f-125">Check AS2 message AS2-From and AS2-tooheaders and correct them based on agreement configuration</span></span> |
|  |  | 


### <a name="-missing-as2-message-body-and-headers"></a><span data-ttu-id="39e2f-126">* Cabeçalhos e corpo da mensagem AS2 ausentes</span><span class="sxs-lookup"><span data-stu-id="39e2f-126">* Missing AS2 message body and headers</span></span>    

|   |   |  
|---|---|
| <span data-ttu-id="39e2f-127">Descrição do erro</span><span class="sxs-lookup"><span data-stu-id="39e2f-127">Error description</span></span>| <span data-ttu-id="39e2f-128">conteúdo da solicitação Olá é nulo ou vazio</span><span class="sxs-lookup"><span data-stu-id="39e2f-128">hello request content is null or empty</span></span> | 
| <span data-ttu-id="39e2f-129">Ação do usuário</span><span class="sxs-lookup"><span data-stu-id="39e2f-129">User action</span></span> | <span data-ttu-id="39e2f-130">Foi recebida uma mensagem AS2 que não contém o corpo da mensagem de saudação</span><span class="sxs-lookup"><span data-stu-id="39e2f-130">An AS2 message was received that did not contain hello message body</span></span> |
|  |  | 

### <a name="-as2-message-decryption-failure"></a><span data-ttu-id="39e2f-131">* Falha na descriptografia mensagem AS2</span><span class="sxs-lookup"><span data-stu-id="39e2f-131">* AS2 message decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="39e2f-132">Descrição do erro</span><span class="sxs-lookup"><span data-stu-id="39e2f-132">Error description</span></span> |  <span data-ttu-id="39e2f-133">[processado/Erro: falha na descriptografia]</span><span class="sxs-lookup"><span data-stu-id="39e2f-133">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="39e2f-134">Ação do usuário</span><span class="sxs-lookup"><span data-stu-id="39e2f-134">User action</span></span> | <span data-ttu-id="39e2f-135">Adicionar @base64ToBinary tooAS2Message antes de enviar toopartner</span><span class="sxs-lookup"><span data-stu-id="39e2f-135">Add @base64ToBinary tooAS2Message before sending toopartner</span></span> 
```java
            "HTTP": {
                "inputs": {
                    "body": "@base64ToBinary(body('Encode_to_AS2_message')?['AS2Message']?['Content'])",
                    "headers": "@body('Encode_to_AS2_message')?['AS2Message']?['OutboundHeaders']",
                    "method": "POST",
                    "uri": "xxxxx.xxx"
                },
                
``` 

### <a name="-mdn-decryption-failure"></a><span data-ttu-id="39e2f-136">* Falha na descriptografia do MDN</span><span class="sxs-lookup"><span data-stu-id="39e2f-136">* MDN decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="39e2f-137">Descrição do erro</span><span class="sxs-lookup"><span data-stu-id="39e2f-137">Error description</span></span> |  <span data-ttu-id="39e2f-138">[processado/Erro: falha na descriptografia]</span><span class="sxs-lookup"><span data-stu-id="39e2f-138">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="39e2f-139">Ação do usuário</span><span class="sxs-lookup"><span data-stu-id="39e2f-139">User action</span></span> | <span data-ttu-id="39e2f-140">Adicionar @base64ToBinary tooMDN antes de enviar toopartner</span><span class="sxs-lookup"><span data-stu-id="39e2f-140">Add @base64ToBinary tooMDN before sending toopartner</span></span> 
```java
            "Response": {
                "inputs": {
                    "body": "@base64ToBinary(body('Decode_AS2_message')?['OutgoingMDN']?['Content'])",
                    "headers": "@body('Decode_AS2_message')?['OutgoingMDN']?['OutboundHeaders']",
                    "statusCode": 200
                },
                
``` 

### <a name="-missing-signing-certificate"></a><span data-ttu-id="39e2f-141">* Certificado de assinatura ausente</span><span class="sxs-lookup"><span data-stu-id="39e2f-141">* Missing signing certificate</span></span>

|   |   |  
|---|---|
| <span data-ttu-id="39e2f-142">Descrição do erro</span><span class="sxs-lookup"><span data-stu-id="39e2f-142">Error description</span></span>| <span data-ttu-id="39e2f-143">Olá certificado de assinatura não foi configurado para parte do AS2.</span><span class="sxs-lookup"><span data-stu-id="39e2f-143">hello Signing Certificate has not been configured for AS2 party.</span></span> </br> <span data-ttu-id="39e2f-144">AS2-From: partner1 AS2-To: partner2</span><span class="sxs-lookup"><span data-stu-id="39e2f-144">AS2-From: partner1 AS2-To: partner2</span></span> | 
| <span data-ttu-id="39e2f-145">Ação do usuário</span><span class="sxs-lookup"><span data-stu-id="39e2f-145">User action</span></span> | <span data-ttu-id="39e2f-146">Definir as configurações do contrato AS2 com o certificado correto para assinatura</span><span class="sxs-lookup"><span data-stu-id="39e2f-146">Configure AS2 agreement settings with correct certificate for signature</span></span> |
|  |  | 

## <a name="x12-and-edifact"></a><span data-ttu-id="39e2f-147">X12 e EDIFACT</span><span class="sxs-lookup"><span data-stu-id="39e2f-147">X12 and EDIFACT</span></span>

### <a name="-leading-or-trailing-space-found"></a><span data-ttu-id="39e2f-148">* Espaço à esquerda ou à direita encontrado</span><span class="sxs-lookup"><span data-stu-id="39e2f-148">* Leading or trailing space found</span></span>    
    
|   |   | 
|---|---|
| <span data-ttu-id="39e2f-149">Descrição do erro</span><span class="sxs-lookup"><span data-stu-id="39e2f-149">Error description</span></span> | <span data-ttu-id="39e2f-150">Erro encontrado durante a análise.</span><span class="sxs-lookup"><span data-stu-id="39e2f-150">Error encountered during parsing.</span></span> <span data-ttu-id="39e2f-151">Olá Edifact transação com id ' 123456 'contida no intercâmbio (sem grupo) com a id ' 987654', com a id do remetente 'Parceiro1', id do destinatário 'Parceiro2' está sendo suspenso com os seguintes erros: separador levam à direita encontrado</span><span class="sxs-lookup"><span data-stu-id="39e2f-151">hello Edifact transaction set with id '123456' contained in interchange (without group) with id '987654', with sender id 'Partner1', receiver id 'Partner2' is being suspended with following errors: Leading Trailing separator found</span></span> |
| <span data-ttu-id="39e2f-152">Ação do usuário</span><span class="sxs-lookup"><span data-stu-id="39e2f-152">User action</span></span> | <span data-ttu-id="39e2f-153">Olá contrato configurações toobe configurado tooallow à esquerda e à direita de espaço.</span><span class="sxs-lookup"><span data-stu-id="39e2f-153">hello agreement settings toobe configured tooallow leading and trailing space.</span></span> </br> <span data-ttu-id="39e2f-154">Editar o contrato configurações tooallow à esquerda e à direita de espaço</span><span class="sxs-lookup"><span data-stu-id="39e2f-154">Edit agreement settings tooallow leading and trailing space</span></span> |
|   |   |

![permitir espaço](./media/logic-apps-enterprise-integration-b2b-list-errors-solutions/leadingandtrailing.png)

### <a name="-duplicate-check-has-enabled-in-hello-agreement"></a><span data-ttu-id="39e2f-156">* Seleção duplicada habilitou no contrato de saudação</span><span class="sxs-lookup"><span data-stu-id="39e2f-156">* Duplicate check has enabled in hello agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="39e2f-157">Descrição do erro</span><span class="sxs-lookup"><span data-stu-id="39e2f-157">Error description</span></span> | <span data-ttu-id="39e2f-158">Duplicar Número de Controle</span><span class="sxs-lookup"><span data-stu-id="39e2f-158">Duplicate Control Number</span></span> |
| <span data-ttu-id="39e2f-159">Ação do usuário</span><span class="sxs-lookup"><span data-stu-id="39e2f-159">User action</span></span> | <span data-ttu-id="39e2f-160">Esse erro indica uma mensagem de saudação recebida tem números de controle duplicados.</span><span class="sxs-lookup"><span data-stu-id="39e2f-160">This error indicates hello received message has duplicate control numbers.</span></span> </br> <span data-ttu-id="39e2f-161">Corrija o número de controle hello e reenviar a mensagem de saudação</span><span class="sxs-lookup"><span data-stu-id="39e2f-161">Correct hello control number and resend hello message</span></span> |
|   |   |

### <a name="-missing-schema-in-hello-agreement"></a><span data-ttu-id="39e2f-162">* Esquema ausente no contrato de saudação</span><span class="sxs-lookup"><span data-stu-id="39e2f-162">* Missing schema in hello agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="39e2f-163">Descrição do erro</span><span class="sxs-lookup"><span data-stu-id="39e2f-163">Error description</span></span> | <span data-ttu-id="39e2f-164">Erro encontrado durante a análise.</span><span class="sxs-lookup"><span data-stu-id="39e2f-164">Error encountered during parsing.</span></span> <span data-ttu-id="39e2f-165">conjunto de transação Olá X12 com a id '564220001' contidos no grupo funcional com a id '56422', no intercâmbio com id '000056422' com a id de remetente 12345678 '', id do destinatário ' 87654321' está sendo suspenso com os seguintes erros "mensagem de saudação tem um tipo de documento desconhecido PE e não resolveu tooany de esquemas existentes de Olá configurados no contrato de hello "</span><span class="sxs-lookup"><span data-stu-id="39e2f-165">hello X12 transaction set with id '564220001' contained in functional group with id '56422', in interchange with id '000056422', with sender id '12345678       ', receiver id '87654321       ' is being suspended with following errors "hello message has an unknown document type and did not resolve tooany of hello existing schemas configured in hello agreement"</span></span> |
| <span data-ttu-id="39e2f-166">Ação do usuário</span><span class="sxs-lookup"><span data-stu-id="39e2f-166">User action</span></span> | <span data-ttu-id="39e2f-167">Configurar o esquema nas configurações do contrato Olá</span><span class="sxs-lookup"><span data-stu-id="39e2f-167">Configure schema in hello agreement settings</span></span>  |
|   |   |

### <a name="-incorrect-schema-in-hello-agreement"></a><span data-ttu-id="39e2f-168">* Esquema incorreto no contrato de saudação</span><span class="sxs-lookup"><span data-stu-id="39e2f-168">* Incorrect schema in hello agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="39e2f-169">Descrição do erro</span><span class="sxs-lookup"><span data-stu-id="39e2f-169">Error description</span></span> | <span data-ttu-id="39e2f-170">mensagem de saudação tem um tipo de documento desconhecido e não resolveu tooany de esquemas existentes de Olá configurados no contrato de saudação.</span><span class="sxs-lookup"><span data-stu-id="39e2f-170">hello message has an unknown document type and did not resolve tooany of hello existing schemas configured in hello agreement.</span></span> |
| <span data-ttu-id="39e2f-171">Ação do usuário</span><span class="sxs-lookup"><span data-stu-id="39e2f-171">User action</span></span> | <span data-ttu-id="39e2f-172">Configurar o esquema correto nas configurações do contrato Olá</span><span class="sxs-lookup"><span data-stu-id="39e2f-172">Configure correct schema in hello agreement settings</span></span>  |
|   |   |

## <a name="flat-file"></a><span data-ttu-id="39e2f-173">Arquivo simples</span><span class="sxs-lookup"><span data-stu-id="39e2f-173">Flat file</span></span>

### <a name="-input-message-with-no-body"></a><span data-ttu-id="39e2f-174">* Mensagem de entrada sem corpo</span><span class="sxs-lookup"><span data-stu-id="39e2f-174">* Input message with no body</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="39e2f-175">Descrição do erro</span><span class="sxs-lookup"><span data-stu-id="39e2f-175">Error description</span></span> | <span data-ttu-id="39e2f-176">InvalidTemplate.</span><span class="sxs-lookup"><span data-stu-id="39e2f-176">InvalidTemplate.</span></span> <span data-ttu-id="39e2f-177">Expressões de linguagem de modelo não é possível tooprocess em entradas de 'Flat_File_Decoding' ação na linha '1' e '1902' da coluna: ' necessária a propriedade 'content' espera um valor mas obteve nulo.</span><span class="sxs-lookup"><span data-stu-id="39e2f-177">Unable tooprocess template language expressions in action 'Flat_File_Decoding' inputs at line '1' and column '1902': 'Required property 'content' expects a value but got null.</span></span> <span data-ttu-id="39e2f-178">Caminho “”.”.</span><span class="sxs-lookup"><span data-stu-id="39e2f-178">Path ''.'.</span></span> |
| <span data-ttu-id="39e2f-179">Ação do usuário</span><span class="sxs-lookup"><span data-stu-id="39e2f-179">User action</span></span> | <span data-ttu-id="39e2f-180">Esse erro indica a mensagem de entrada hello não contém um corpo</span><span class="sxs-lookup"><span data-stu-id="39e2f-180">This error indicates hello input message does not contain a body</span></span> |
|   |   | 

## <a name="learn-more"></a><span data-ttu-id="39e2f-181">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="39e2f-181">Learn more</span></span>
[<span data-ttu-id="39e2f-182">Saiba mais sobre Olá Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="39e2f-182">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)
