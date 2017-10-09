---
title: "mensagens de aaaWorking com XML em seus fluxos de trabalho - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Processar, validar, transformar e enriquecer XML mensagens em aplicativos lógicos e o uso de negócios tooscenarios Olá Enterprise Integration Pack"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 47672dc4-1caa-44e5-b8cb-68ec3a76b7dc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 02/27/2017
ms.author: LADocs; mandia
ms.openlocfilehash: f90ae89fef0a4bd17286adbce398e573940bb790
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="validate-and-transform-xml-encode-and-decode-flat-files-and-enrich-messages-features-in-logic-apps"></a><span data-ttu-id="5fa7d-103">Validar e transformar o XML, codificar e decodificar arquivos simples e enriquecer os recursos de mensagens em aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="5fa7d-103">Validate and transform XML, encode and decode flat files, and enrich messages features in logic apps</span></span>

<span data-ttu-id="5fa7d-104">Usar aplicativos lógicos, você tem capacidade tooprocess XML mensagens de saudação do que você envia e recebe.</span><span class="sxs-lookup"><span data-stu-id="5fa7d-104">Using logic apps, you have hello ability tooprocess XML messages that you send and receive.</span></span> <span data-ttu-id="5fa7d-105">Este recurso está incluído com hello Enterprise Integration Pack.</span><span class="sxs-lookup"><span data-stu-id="5fa7d-105">This feature is included with hello Enterprise Integration Pack.</span></span> <span data-ttu-id="5fa7d-106">Para os usuários com um plano de fundo do BizTalk Server, Olá Enterprise Integration Pack fornece tootransform de recursos semelhantes e validar mensagens, trabalhar com arquivos simples e até mesmo usar XPath tooenrich ou extrair propriedades específicas de uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="5fa7d-106">For those users with a BizTalk Server background, hello Enterprise Integration Pack gives you similar abilities tootransform and validate messages, work with flat files, and even use XPath tooenrich or extract specific properties from a message.</span></span> 

<span data-ttu-id="5fa7d-107">Para os usuários que são um novo espaço de toothis, esses recursos expanda como processar mensagens de fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="5fa7d-107">For those users who are new toothis space, these features expand how you process messages within your workflow.</span></span> <span data-ttu-id="5fa7d-108">Por exemplo, se você estiver em um cenário de business-to-business e trabalhar com esquemas XML específicos, você pode usar o hello Enterprise Integration Pack tooenhance como sua empresa processa essas mensagens.</span><span class="sxs-lookup"><span data-stu-id="5fa7d-108">For example, if you are in a business-to-business scenario, and work with specific XML schemas, then you can use hello Enterprise Integration Pack tooenhance how your company processes these messages.</span></span> 

<span data-ttu-id="5fa7d-109">Olá Enterprise Integration Pack inclui:</span><span class="sxs-lookup"><span data-stu-id="5fa7d-109">hello Enterprise Integration Pack includes:</span></span> 

* <span data-ttu-id="5fa7d-110">[Validação de XML](logic-apps-enterprise-integration-xml-validation.md "Saiba mais sobre a validação de mensagens XML") – Validar uma mensagem XML de entrada ou de saída em relação a um esquema específico.</span><span class="sxs-lookup"><span data-stu-id="5fa7d-110">[XML validation](logic-apps-enterprise-integration-xml-validation.md "Learn about XML message validation") - Validate an incoming or outgoing XML message against a specific schema.</span></span>
* <span data-ttu-id="5fa7d-111">[Transformação XML](../logic-apps/logic-apps-enterprise-integration-transform.md "Saiba mais sobre as transformações de mensagens XML e mapas") - converter ou personalizar uma mensagem XML com base em seus requisitos ou requisitos de saudação de um parceiro.</span><span class="sxs-lookup"><span data-stu-id="5fa7d-111">[XML transform](../logic-apps/logic-apps-enterprise-integration-transform.md "Learn about XML message transformations and maps") - Convert or customize an XML message based on your requirements, or hello requirements of a partner.</span></span>
* <span data-ttu-id="5fa7d-112">[Codificação e decodificação de arquivos simples](logic-apps-enterprise-integration-flatfile.md "Saiba mais sobre a codificação/decodificação de arquivos simples") Codificar ou decodificar arquivos simples.</span><span class="sxs-lookup"><span data-stu-id="5fa7d-112">[Flat file encoding and flat file decoding](logic-apps-enterprise-integration-flatfile.md "Learn about flat file encoding/decoding") - Encode or decode a flat file.</span></span> <span data-ttu-id="5fa7d-113">Por exemplo, o SAP aceita e envia arquivos IDOC no formato de arquivo simples.</span><span class="sxs-lookup"><span data-stu-id="5fa7d-113">For example, SAP accepts and sends IDOC files in flat file format.</span></span> <span data-ttu-id="5fa7d-114">Muitas plataformas de integração criam mensagens XML, incluindo Aplicativos Lógicos.</span><span class="sxs-lookup"><span data-stu-id="5fa7d-114">Many integration platforms create XML messages, including Logic Apps.</span></span> <span data-ttu-id="5fa7d-115">Portanto, você pode criar um aplicativo de lógica que usa Olá arquivo simples codificador muito "converter" arquivos de tooflat de arquivos XML.</span><span class="sxs-lookup"><span data-stu-id="5fa7d-115">So, you can create a logic app that uses hello flat file encoder too"convert" XML files tooflat files.</span></span> 
* <span data-ttu-id="5fa7d-116">[XPath](https://msdn.microsoft.com/library/mt643789.aspx) - enriquecer uma mensagem e extrair propriedades específicas de mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="5fa7d-116">[XPath](https://msdn.microsoft.com/library/mt643789.aspx) - Enrich a message and extract specific properties from hello message.</span></span> <span data-ttu-id="5fa7d-117">Você pode então usar Olá extraído tooa destino da mensagem de saudação propriedades tooroute ou um ponto de extremidade intermediário.</span><span class="sxs-lookup"><span data-stu-id="5fa7d-117">You can then use hello extracted properties tooroute hello message tooa destination, or an intermediary endpoint.</span></span>

## <a name="try-it-out"></a><span data-ttu-id="5fa7d-118">Experimentar</span><span class="sxs-lookup"><span data-stu-id="5fa7d-118">Try it out</span></span>
<span data-ttu-id="5fa7d-119">[Implantar um aplicativo totalmente operacional lógica ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (exemplo GitHub) usando recursos do XML de saudação do Azure lógica de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="5fa7d-119">[Deploy a fully operational logic app ](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-veter-pipeline) (GitHub sample) by using hello XML features in Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="5fa7d-120">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="5fa7d-120">Learn more</span></span>
[<span data-ttu-id="5fa7d-121">Saiba mais sobre Olá Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="5fa7d-121">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Saiba mais sobre o pacote de integração do Enterprise")
