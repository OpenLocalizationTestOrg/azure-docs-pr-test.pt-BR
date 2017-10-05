---
title: "Decodificação de edifact B2B dos Aplicativos Lógicos resolve UNH2.5 – Aplicativos Lógicos do Azure | Microsoft Docs"
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
ms.openlocfilehash: 62ad8183cc6e9f56255b2729a04ee7710d00a21a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-handle-edifact-documents-having-unh25-segment"></a><span data-ttu-id="41967-103">Como tratar documentos EDIFACT tendo o segmento UNH2.5</span><span class="sxs-lookup"><span data-stu-id="41967-103">How to handle EDIFACT documents having UNH2.5 segment</span></span>
<span data-ttu-id="41967-104">Quando está presente no documento EDIFACT, UNH2.5 está sendo usado para pesquisa de esquema.</span><span class="sxs-lookup"><span data-stu-id="41967-104">When UNH2.5 is present in the EDIFACT document, it is being used for schema lookup.</span></span> 

<span data-ttu-id="41967-105">Exemplo: o campo UNH é **EAN008** na mensagem EDIFACT</span><span class="sxs-lookup"><span data-stu-id="41967-105">Example: The UNH field is **EAN008** in the EDIFACT message</span></span>  
<span data-ttu-id="41967-106">UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'</span><span class="sxs-lookup"><span data-stu-id="41967-106">UNH+SSDD1+ORDERS:D:03B:UN:**EAN008**'</span></span>  

<span data-ttu-id="41967-107">Etapas a seguir para manipular a mensagem</span><span class="sxs-lookup"><span data-stu-id="41967-107">Steps to follow to handle the message</span></span> 
1. <span data-ttu-id="41967-108">Atualizar o esquema</span><span class="sxs-lookup"><span data-stu-id="41967-108">Update the schema</span></span>
2. <span data-ttu-id="41967-109">Verificar as configurações do contrato</span><span class="sxs-lookup"><span data-stu-id="41967-109">Check the agreement settings</span></span>  

## <a name="update-the-schema"></a><span data-ttu-id="41967-110">Atualizar o esquema</span><span class="sxs-lookup"><span data-stu-id="41967-110">Update the schema</span></span>
<span data-ttu-id="41967-111">Para processar a mensagem, você precisa implantar um esquema com o nome do nó raiz UNH2.5.</span><span class="sxs-lookup"><span data-stu-id="41967-111">To process the message, you need to deploy a schema with the UNH2.5 root node name.</span></span>  <span data-ttu-id="41967-112">Para dar um exemplo, o nome raiz do esquema seria **EFACT_D03B_ORDERS_EAN008**</span><span class="sxs-lookup"><span data-stu-id="41967-112">For given an example, the schema root name would be **EFACT_D03B_ORDERS_EAN008**</span></span>  

<span data-ttu-id="41967-113">Para cada D03B_ORDERS com um segmento UNH2.5 diferente, você precisaria implantar um esquema individual.</span><span class="sxs-lookup"><span data-stu-id="41967-113">For each D03B_ORDERS with a different UNH2.5 segment, you would have to deploy an individual schema.</span></span>  

## <a name="add-schema-to-the-edifact-agreement"></a><span data-ttu-id="41967-114">Adicionar o esquema ao contrato de EDIFACT</span><span class="sxs-lookup"><span data-stu-id="41967-114">Add schema to the EDIFACT agreement</span></span>
### <a name="edifact-decode"></a><span data-ttu-id="41967-115">Decodificação de EDIFACT</span><span class="sxs-lookup"><span data-stu-id="41967-115">EDIFACT Decode</span></span>
<span data-ttu-id="41967-116">Para decodificar a mensagem de entrada, configure o esquema nas definições de recebimento do contrato de EDIFACT</span><span class="sxs-lookup"><span data-stu-id="41967-116">To Decode the incoming message, configure the schema in the EDIFACT agreement receive settings</span></span>
1. <span data-ttu-id="41967-117">Adicionar o esquema à conta de integração</span><span class="sxs-lookup"><span data-stu-id="41967-117">Add the schema to the integration account</span></span>    
2. <span data-ttu-id="41967-118">Configure o esquema nas definições de recebimento do contrato de EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="41967-118">Configure the schema in the EDIFACT agreement receive settings.</span></span> 
3. <span data-ttu-id="41967-119">Selecione o contrato de EDIFACT e clique em **Editar como JSON**.</span><span class="sxs-lookup"><span data-stu-id="41967-119">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="41967-120">Adicionar o valor UNH2.5 no contrato de recebimento **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)</span><span class="sxs-lookup"><span data-stu-id="41967-120">Add UNH2.5 value in the Receive Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image1.png)</span></span>

### <a name="edifact-encode"></a><span data-ttu-id="41967-121">Codificação de EDIFACT</span><span class="sxs-lookup"><span data-stu-id="41967-121">EDIFACT Encode</span></span>
<span data-ttu-id="41967-122">Para codificar a mensagem de entrada, configure o esquema nas definições de envio do contrato de EDIFACT</span><span class="sxs-lookup"><span data-stu-id="41967-122">To Encode the incoming message, configure the schema in the EDIFACT agreement send settings</span></span>
1. <span data-ttu-id="41967-123">Adicionar o esquema à conta de integração</span><span class="sxs-lookup"><span data-stu-id="41967-123">Add the schema to the integration account</span></span>    
2. <span data-ttu-id="41967-124">Configure o esquema nas definições de envio do contrato de EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="41967-124">Configure the schema in the EDIFACT agreement send settings.</span></span> 
3. <span data-ttu-id="41967-125">Selecione o contrato de EDIFACT e clique em **Editar como JSON**.</span><span class="sxs-lookup"><span data-stu-id="41967-125">Select EDIFACT agreement and click **Edit as JSON**.</span></span>  <span data-ttu-id="41967-126">Adicione o valor UNH2.5 no contrato de envio **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)</span><span class="sxs-lookup"><span data-stu-id="41967-126">Add UNH2.5 value in the Send Agreement **schemaReferences**
![](./media/logic-apps-enterprise-integration-edifact_inputfile_unh2.5/image2.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="41967-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="41967-127">Next Steps</span></span>
* [<span data-ttu-id="41967-128">Saiba mais sobre os contratos da conta de integração</span><span class="sxs-lookup"><span data-stu-id="41967-128">Learn more about integration account agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Saiba mais sobre os contratos de integração corporativa")  