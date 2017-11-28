---
title: "aaaLogic aplicativos B2B edifact decodificar resolver UNH2.5 - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Decodificação de edifact B2B dos Aplicativos Lógicos resolve UNH2.5"
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
ms.date: 04/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 6d85242d0f828fa52cdc9689938f3ba1e51b1183
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toohandle-edifact-documents-having-unh25-segment"></a><span data-ttu-id="b7c9e-103">Como toohandle EDIFACT documentos com UNH2.5 segmento</span><span class="sxs-lookup"><span data-stu-id="b7c9e-103">How toohandle EDIFACT documents having UNH2.5 segment</span></span>
<span data-ttu-id="b7c9e-104">Quando UNH2.5 estiver presente no documento EDIFACT hello, ele está sendo usado para pesquisa de esquema.</span><span class="sxs-lookup"><span data-stu-id="b7c9e-104">When UNH2.5 is present in hello EDIFACT document, it is being used for schema lookup.</span></span> 

<span data-ttu-id="b7c9e-105">Exemplo: campo UNH Olá é **EAN008** na mensagem de saudação do EDIFACT</span><span class="sxs-lookup"><span data-stu-id="b7c9e-105">Example: hello UNH field is **EAN008** in hello EDIFACT message</span></span>  
<span data-ttu-id="b7c9e-106">UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'</span><span class="sxs-lookup"><span data-stu-id="b7c9e-106">UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'</span></span>  

<span data-ttu-id="b7c9e-107">Mensagem de saudação do etapas toofollow toohandle</span><span class="sxs-lookup"><span data-stu-id="b7c9e-107">Steps toofollow toohandle hello message</span></span> 
1. <span data-ttu-id="b7c9e-108">Atualizar esquema da saudação</span><span class="sxs-lookup"><span data-stu-id="b7c9e-108">Update hello schema</span></span>
2. <span data-ttu-id="b7c9e-109">Verifique as configurações do contrato Olá</span><span class="sxs-lookup"><span data-stu-id="b7c9e-109">Check hello agreement settings</span></span>  

## <a name="update-hello-schema"></a><span data-ttu-id="b7c9e-110">Atualizar esquema da saudação</span><span class="sxs-lookup"><span data-stu-id="b7c9e-110">Update hello schema</span></span>
<span data-ttu-id="b7c9e-111">mensagem de saudação tooprocess, você precisa toodeploy um esquema com o nome do nó de raiz Olá UNH2.5.</span><span class="sxs-lookup"><span data-stu-id="b7c9e-111">tooprocess hello message, you need toodeploy a schema with hello UNH2.5 root node name.</span></span>  <span data-ttu-id="b7c9e-112">Para um exemplo, o nome de raiz do esquema Olá seria **EFACT_D03B_ORDERS_EAN008**</span><span class="sxs-lookup"><span data-stu-id="b7c9e-112">For given an example, hello schema root name would be **EFACT_D03B_ORDERS_EAN008**</span></span>  

<span data-ttu-id="b7c9e-113">Para cada D03B_ORDERS com um segmento UNH2.5 diferente, você teria toodeploy um esquema individual.</span><span class="sxs-lookup"><span data-stu-id="b7c9e-113">For each D03B_ORDERS with a different UNH2.5 segment, you would have toodeploy an individual schema.</span></span>  

## <a name="add-schema-toohello-edifact-agreement"></a><span data-ttu-id="b7c9e-114">Adicionar esquema toohello EDIFACT contrato</span><span class="sxs-lookup"><span data-stu-id="b7c9e-114">Add schema toohello EDIFACT agreement</span></span>
### <a name="edifact-decode"></a><span data-ttu-id="b7c9e-115">Decodificação de EDIFACT</span><span class="sxs-lookup"><span data-stu-id="b7c9e-115">EDIFACT Decode</span></span>
<span data-ttu-id="b7c9e-116">tooDecode Olá mensagem de entrada, configure o esquema de saudação em Olá EDIFACT configurações de recebimento do contrato</span><span class="sxs-lookup"><span data-stu-id="b7c9e-116">tooDecode hello incoming message, configure hello schema in hello EDIFACT agreement receive settings</span></span>
1. <span data-ttu-id="b7c9e-117">Adicionar conta de integração do hello esquema toohello</span><span class="sxs-lookup"><span data-stu-id="b7c9e-117">Add hello schema toohello integration account</span></span>    
2. <span data-ttu-id="b7c9e-118">Configurar o esquema de saudação em Olá EDIFACT configurações de recebimento do contrato.</span><span class="sxs-lookup"><span data-stu-id="b7c9e-118">Configure hello schema in hello EDIFACT agreement receive settings.</span></span> 
3. <span data-ttu-id="b7c9e-119">Selecione o contrato de EDIFACT e clique em **Editar como JSON**.</span><span class="sxs-lookup"><span data-stu-id="b7c9e-119">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="b7c9e-120">Adicione o valor UNH2.5 no contrato de recebimento de saudação **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)</span><span class="sxs-lookup"><span data-stu-id="b7c9e-120">Add UNH2.5 value in hello Receive Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)</span></span>

### <a name="edifact-encode"></a><span data-ttu-id="b7c9e-121">Codificação de EDIFACT</span><span class="sxs-lookup"><span data-stu-id="b7c9e-121">EDIFACT Encode</span></span>
<span data-ttu-id="b7c9e-122">tooEncode Olá mensagem de entrada, configure o esquema de saudação em configurações de envio do acordo de EDIFACT Olá</span><span class="sxs-lookup"><span data-stu-id="b7c9e-122">tooEncode hello incoming message, configure hello schema in hello EDIFACT agreement send settings</span></span>
1. <span data-ttu-id="b7c9e-123">Adicionar conta de integração do hello esquema toohello</span><span class="sxs-lookup"><span data-stu-id="b7c9e-123">Add hello schema toohello integration account</span></span>    
2. <span data-ttu-id="b7c9e-124">Configure o esquema de saudação em configurações de envio do acordo de EDIFACT hello.</span><span class="sxs-lookup"><span data-stu-id="b7c9e-124">Configure hello schema in hello EDIFACT agreement send settings.</span></span> 
3. <span data-ttu-id="b7c9e-125">Selecione o contrato de EDIFACT e clique em **Editar como JSON**.</span><span class="sxs-lookup"><span data-stu-id="b7c9e-125">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="b7c9e-126">Adicione o valor UNH2.5 em Olá enviar contrato **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)</span><span class="sxs-lookup"><span data-stu-id="b7c9e-126">Add UNH2.5 value in hello Send Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="b7c9e-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b7c9e-127">Next Steps</span></span>
* [<span data-ttu-id="b7c9e-128">Saiba mais sobre os contratos da conta de integração</span><span class="sxs-lookup"><span data-stu-id="b7c9e-128">Learn more about integration account agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Saiba mais sobre os contratos de integração corporativa")  