---
title: "aaaEnterprise integração para B2B - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Criar fluxos de trabalho de B2B e dar suporte a cenários de integração do enterprise para os aplicativos lógicos com hello Enterprise Integration Pack"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: dd517c4d-1701-4247-b83c-183c4d8d8aae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8dc866533110b1d07f51cf446056d2ca5ce869ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-b2b-scenarios-and-communication-with-hello-enterprise-integration-pack"></a><span data-ttu-id="62326-103">Visão geral: Cenários B2B e comunicação com hello Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="62326-103">Overview: B2B scenarios and communication with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="62326-104">Para fluxos de trabalho entre empresas (B2B) e comunicação direta com os aplicativos lógicos do Azure, você pode habilitar cenários de integração do enterprise com a solução baseada em nuvem da Microsoft, Olá Enterprise Integration Pack.</span><span class="sxs-lookup"><span data-stu-id="62326-104">For business-to-business (B2B) workflows and seamless communication with Azure Logic Apps, you can enable enterprise integration scenarios with Microsoft's cloud-based solution, hello Enterprise Integration Pack.</span></span> <span data-ttu-id="62326-105">Organizações podem trocar mensagens eletronicamente, mesmo usando diferentes protocolos e formatos.</span><span class="sxs-lookup"><span data-stu-id="62326-105">Organizations can exchange messages electronically, even if they use different protocols and formats.</span></span> <span data-ttu-id="62326-106">pacote de saudação transforma formatos diferentes em um formato que sistemas de organizações podem interpretar e processar.</span><span class="sxs-lookup"><span data-stu-id="62326-106">hello pack transforms different formats into a format that organizations' systems can interpret and process.</span></span> <span data-ttu-id="62326-107">As organizações podem trocar mensagens por meio de protocolos padrão da indústria, incluindo [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md) e [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md).</span><span class="sxs-lookup"><span data-stu-id="62326-107">Organizations can exchange messages through industry-standard protocols, including [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md), and [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md).</span></span> <span data-ttu-id="62326-108">Também é possível proteger mensagens com criptografia e assinaturas digitais.</span><span class="sxs-lookup"><span data-stu-id="62326-108">You can also secure messages with both encryption and digital signatures.</span></span>

<span data-ttu-id="62326-109">Se você estiver familiarizado com o BizTalk Server ou serviços BizTalk do Microsoft Azure, recursos de integração do Enterprise Olá são toouse fácil porque a maioria dos conceitos são semelhantes.</span><span class="sxs-lookup"><span data-stu-id="62326-109">If you are familiar with BizTalk Server or Microsoft Azure BizTalk Services, hello Enterprise Integration features are easy toouse because most concepts are similar.</span></span> <span data-ttu-id="62326-110">A principal diferença é que a integração da empresa usa armazenamento de saudação de toosimplify de contas de integração e gerenciamento de artefatos usados nas comunicações de B2B.</span><span class="sxs-lookup"><span data-stu-id="62326-110">One major difference is that Enterprise Integration uses integration accounts toosimplify hello storage and management of artifacts used in B2B communications.</span></span> 

<span data-ttu-id="62326-111">Em termos de arquitetura, Olá Enterprise Integration Pack baseia-se em "contas de integração".</span><span class="sxs-lookup"><span data-stu-id="62326-111">Architecturally, hello Enterprise Integration Pack is based on "integration accounts".</span></span> <span data-ttu-id="62326-112">Essas contas são contêineres baseados em nuvem que armazenam todos os artefatos, como esquemas, parceiros, certificados, mapas e contratos.</span><span class="sxs-lookup"><span data-stu-id="62326-112">These accounts are cloud-based containers that store all your artifacts, like schemas, partners, certificates, maps, and agreements.</span></span> <span data-ttu-id="62326-113">Você pode usar toodesign esses artefatos, implantar e manter seus aplicativos B2B e também toobuild B2B fluxos de trabalho para os aplicativos lógicos.</span><span class="sxs-lookup"><span data-stu-id="62326-113">You can use these artifacts toodesign, deploy, and maintain your B2B apps and also toobuild B2B workflows for logic apps.</span></span> <span data-ttu-id="62326-114">Mas, antes de usar esses artefatos, primeiro você deve vincular o seu aplicativo de conta tooyour lógica da integração.</span><span class="sxs-lookup"><span data-stu-id="62326-114">But before you can use these artifacts, you must first link your integration account tooyour logic app.</span></span> <span data-ttu-id="62326-115">Depois disso, o aplicativo lógico poderá acessar os artefatos da sua conta de integração.</span><span class="sxs-lookup"><span data-stu-id="62326-115">After that, your logic app can access your integration account's artifacts.</span></span>

## <a name="why-should-you-use-enterprise-integration"></a><span data-ttu-id="62326-116">Por que você deve usar a integração corporativa?</span><span class="sxs-lookup"><span data-stu-id="62326-116">Why should you use enterprise integration?</span></span>

* <span data-ttu-id="62326-117">Com a integração corporativa, é possível armazenar todos os artefatos em um único local: sua conta de integração.</span><span class="sxs-lookup"><span data-stu-id="62326-117">With enterprise integration, you can store all your artifacts in one place -- your integration account.</span></span>
* <span data-ttu-id="62326-118">Você pode criar fluxos de trabalho de B2B e integrar aplicativos do terceiro software como serviço (SaaS), aplicativos locais e aplicativos personalizados usando o mecanismo de aplicativos do Azure lógica hello e todos os seus conectores.</span><span class="sxs-lookup"><span data-stu-id="62326-118">You can build B2B workflows and integrate with third-party software-as-service (SaaS) apps, on-premises apps, and custom apps by using hello Azure Logic Apps engine and all its connectors.</span></span>
* <span data-ttu-id="62326-119">Você pode criar código personalizado para seus aplicativos lógicos com o Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="62326-119">You can create custom code for your logic apps with Azure functions.</span></span>

## <a name="how-tooget-started-with-enterprise-integration"></a><span data-ttu-id="62326-120">Como tooget iniciado com a integração da empresa?</span><span class="sxs-lookup"><span data-stu-id="62326-120">How tooget started with enterprise integration?</span></span>

<span data-ttu-id="62326-121">Você pode criar e gerenciar aplicativos B2B com hello Enterprise Integration Pack por meio de saudação lógica de aplicativo Designer no hello **portal do Azure**.</span><span class="sxs-lookup"><span data-stu-id="62326-121">You can build and manage B2B apps with hello Enterprise Integration Pack through hello Logic App Designer in hello **Azure portal**.</span></span> <span data-ttu-id="62326-122">Também é possível gerenciar aplicativos lógicos com o [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Tópicos do PowerShell para aplicativos lógicos").</span><span class="sxs-lookup"><span data-stu-id="62326-122">You can also manage your logic apps with [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Logic apps PowerShell topics").</span></span>

<span data-ttu-id="62326-123">Aqui estão as etapas de alto nível hello, que você deve executar antes de criar aplicativos no hello portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="62326-123">Here are hello high-level steps you must take before you can create apps in hello Azure portal:</span></span>

![imagem da visão geral](media/logic-apps-enterprise-integration-overview/overview-0.png)  

## <a name="what-are-some-common-scenarios"></a><span data-ttu-id="62326-125">Quais são os cenários comuns?</span><span class="sxs-lookup"><span data-stu-id="62326-125">What are some common scenarios?</span></span>

<span data-ttu-id="62326-126">O Enterprise Integration oferece suporte a estes padrões do setor:</span><span class="sxs-lookup"><span data-stu-id="62326-126">Enterprise Integration supports these industry standards:</span></span>

* <span data-ttu-id="62326-127">EDI - Intercâmbio Eletrônico de Dados</span><span class="sxs-lookup"><span data-stu-id="62326-127">EDI - Electronic Data Interchange</span></span>
* <span data-ttu-id="62326-128">EAI - Integração de Aplicativos Empresariais</span><span class="sxs-lookup"><span data-stu-id="62326-128">EAI - Enterprise Application Integration</span></span>

## <a name="heres-what-you-need-tooget-started"></a><span data-ttu-id="62326-129">Aqui está o que você precisa tooget iniciado</span><span class="sxs-lookup"><span data-stu-id="62326-129">Here's what you need tooget started</span></span>

* <span data-ttu-id="62326-130">Uma assinatura do Azure com uma conta de integração</span><span class="sxs-lookup"><span data-stu-id="62326-130">An Azure subscription with an integration account</span></span>
* <span data-ttu-id="62326-131">Visual Studio 2015 toocreate mapas e esquemas</span><span class="sxs-lookup"><span data-stu-id="62326-131">Visual Studio 2015 toocreate maps and schemas</span></span>
* [<span data-ttu-id="62326-132">Microsoft Azure Logic Apps Enterprise Integration Tools for Visual Studio 2015 2.0 (Ferramentas de integração corporativa do Aplicativo Lógico do Microsoft Azure para Visual Studio 2015)</span><span class="sxs-lookup"><span data-stu-id="62326-132">Microsoft Azure Logic Apps Enterprise Integration Tools for Visual Studio 2015 2.0</span></span>](https://aka.ms/vsmapsandschemas)  

## <a name="try-it-now"></a><span data-ttu-id="62326-133">Teste agora</span><span class="sxs-lookup"><span data-stu-id="62326-133">Try it now</span></span>

<span data-ttu-id="62326-134">[Implantar um envio de AS2 exemplo totalmente operacional e lógica de aplicativo de recebimento](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) que usa recursos de saudação B2B para os aplicativos lógicos do Azure.</span><span class="sxs-lookup"><span data-stu-id="62326-134">[Deploy a fully operational sample AS2 send & receive logic app](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) that uses hello B2B features for Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="62326-135">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="62326-135">Learn more</span></span>
* [<span data-ttu-id="62326-136">Contratos</span><span class="sxs-lookup"><span data-stu-id="62326-136">Agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Saiba mais sobre contratos de integração corporativa")
* [<span data-ttu-id="62326-137">Cenários de tooBusiness (B2B) Business</span><span class="sxs-lookup"><span data-stu-id="62326-137">Business tooBusiness (B2B) scenarios</span></span>](../logic-apps/logic-apps-enterprise-integration-b2b.md "Saiba como toocreate lógica aplicativos com recursos de B2B")  
* [<span data-ttu-id="62326-138">Certificados</span><span class="sxs-lookup"><span data-stu-id="62326-138">Certificates</span></span>](logic-apps-enterprise-integration-certificates.md "Saiba mais sobre certificados da integração corporativa")
* [<span data-ttu-id="62326-139">Simples de codificação/decodificação de arquivo</span><span class="sxs-lookup"><span data-stu-id="62326-139">Flat file encoding/decoding</span></span>](logic-apps-enterprise-integration-flatfile.md "Saiba como tooencode e decodificar o conteúdo do arquivo simples")  
* [<span data-ttu-id="62326-140">Integration accounts</span><span class="sxs-lookup"><span data-stu-id="62326-140">Integration accounts</span></span>](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn about contas de integração")
* [<span data-ttu-id="62326-141">Mapas</span><span class="sxs-lookup"><span data-stu-id="62326-141">Maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "Saiba mais sobre mapas da integração corporativa")
* [<span data-ttu-id="62326-142">Parceiros</span><span class="sxs-lookup"><span data-stu-id="62326-142">Partners</span></span>](logic-apps-enterprise-integration-partners.md "Saiba mais sobre parceiros da integração corporativa")
* [<span data-ttu-id="62326-143">Esquemas</span><span class="sxs-lookup"><span data-stu-id="62326-143">Schemas</span></span>](logic-apps-enterprise-integration-schemas.md "Saiba mais sobre esquemas de integração corporativa")
* [<span data-ttu-id="62326-144">Validação de mensagem XML</span><span class="sxs-lookup"><span data-stu-id="62326-144">XML message validation</span></span>](logic-apps-enterprise-integration-xml.md "Saiba como toovalidate XML mensagens com aplicativos lógicos")
* [<span data-ttu-id="62326-145">Transformação de XML</span><span class="sxs-lookup"><span data-stu-id="62326-145">XML transform</span></span>](logic-apps-enterprise-integration-transform.md "Saiba mais sobre mapas da integração corporativa")
* [<span data-ttu-id="62326-146">Conectores de integração Enterprise</span><span class="sxs-lookup"><span data-stu-id="62326-146">Enterprise Integration Connectors</span></span>](../connectors/apis-list.md "Saiba mais sobre os conectores do enterprise integration pack")
* [<span data-ttu-id="62326-147">Metadados da conta de integração</span><span class="sxs-lookup"><span data-stu-id="62326-147">Integration Account Metadata</span></span>](../logic-apps/logic-apps-enterprise-integration-metadata.md "Saiba mais sobre os metadados da conta de integração")
* [<span data-ttu-id="62326-148">Monitorar mensagens B2B</span><span class="sxs-lookup"><span data-stu-id="62326-148">Monitor B2B messages</span></span>](logic-apps-monitor-b2b-message.md "Saiba mais sobre o monitoramento de mensagens B2B")
* [<span data-ttu-id="62326-149">Rastreando mensagens B2B no portal do OMS</span><span class="sxs-lookup"><span data-stu-id="62326-149">Tracking B2B messages in OMS portal</span></span>](logic-apps-track-b2b-messages-omsportal.md "Saiba mais sobre o acompanhamento de mensagens B2B no portal do OMS")

