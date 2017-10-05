---
title: "Enterprise Integration para B2B – Aplicativo Lógico do Azure | Microsoft Docs"
description: "Crie fluxos de trabalho B2B e dê suporte à integração de cenários corporativos para aplicativos lógicos com o Enterprise Integration Pack"
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
ms.openlocfilehash: 9462707db03ecfcc3d5186ce7ded8655ad3bdcc9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="overview-b2b-scenarios-and-communication-with-the-enterprise-integration-pack"></a><span data-ttu-id="c83cd-103">Visão geral: cenários B2B e comunicação com o Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="c83cd-103">Overview: B2B scenarios and communication with the Enterprise Integration Pack</span></span>

<span data-ttu-id="c83cd-104">Para fluxos de trabalho entre empresas (B2B) e comunicação direta com o Aplicativo Lógico do Azure, você pode habilitar cenários de integração corporativa com a solução baseada em nuvem da Microsoft, o Enterprise Integration Pack.</span><span class="sxs-lookup"><span data-stu-id="c83cd-104">For business-to-business (B2B) workflows and seamless communication with Azure Logic Apps, you can enable enterprise integration scenarios with Microsoft's cloud-based solution, the Enterprise Integration Pack.</span></span> <span data-ttu-id="c83cd-105">Organizações podem trocar mensagens eletronicamente, mesmo usando diferentes protocolos e formatos.</span><span class="sxs-lookup"><span data-stu-id="c83cd-105">Organizations can exchange messages electronically, even if they use different protocols and formats.</span></span> <span data-ttu-id="c83cd-106">O pacote transforma diferentes formatos em um formato que os sistemas das organizações podem interpretar e processar.</span><span class="sxs-lookup"><span data-stu-id="c83cd-106">The pack transforms different formats into a format that organizations' systems can interpret and process.</span></span> <span data-ttu-id="c83cd-107">As organizações podem trocar mensagens por meio de protocolos padrão da indústria, incluindo [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md) e [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md).</span><span class="sxs-lookup"><span data-stu-id="c83cd-107">Organizations can exchange messages through industry-standard protocols, including [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md), [X12](logic-apps-enterprise-integration-x12.md), and [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md).</span></span> <span data-ttu-id="c83cd-108">Também é possível proteger mensagens com criptografia e assinaturas digitais.</span><span class="sxs-lookup"><span data-stu-id="c83cd-108">You can also secure messages with both encryption and digital signatures.</span></span>

<span data-ttu-id="c83cd-109">Se você estiver familiarizado com o BizTalk Server ou os Serviços BizTalk do Microsoft Azure, os recursos do Enterprise Integration serão fáceis de usar, pois a maioria dos conceitos é semelhante.</span><span class="sxs-lookup"><span data-stu-id="c83cd-109">If you are familiar with BizTalk Server or Microsoft Azure BizTalk Services, the Enterprise Integration features are easy to use because most concepts are similar.</span></span> <span data-ttu-id="c83cd-110">A principal diferença é que o Enterprise Integration usa contas de integração para simplificar o armazenamento e o gerenciamento de artefatos usados em comunicações B2B.</span><span class="sxs-lookup"><span data-stu-id="c83cd-110">One major difference is that Enterprise Integration uses integration accounts to simplify the storage and management of artifacts used in B2B communications.</span></span> 

<span data-ttu-id="c83cd-111">Em termos de arquitetura, o Enterprise Integration Pack se baseia em "contas de integração".</span><span class="sxs-lookup"><span data-stu-id="c83cd-111">Architecturally, the Enterprise Integration Pack is based on "integration accounts".</span></span> <span data-ttu-id="c83cd-112">Essas contas são contêineres baseados em nuvem que armazenam todos os artefatos, como esquemas, parceiros, certificados, mapas e contratos.</span><span class="sxs-lookup"><span data-stu-id="c83cd-112">These accounts are cloud-based containers that store all your artifacts, like schemas, partners, certificates, maps, and agreements.</span></span> <span data-ttu-id="c83cd-113">É possível utilizar esses artefatos para projetar, implantar e manter seus aplicativos B2B, bem como criar fluxos de trabalho B2B para aplicativos lógicos.</span><span class="sxs-lookup"><span data-stu-id="c83cd-113">You can use these artifacts to design, deploy, and maintain your B2B apps and also to build B2B workflows for logic apps.</span></span> <span data-ttu-id="c83cd-114">Porém, antes de usar esses artefatos, é necessário vincular sua conta de integração ao aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="c83cd-114">But before you can use these artifacts, you must first link your integration account to your logic app.</span></span> <span data-ttu-id="c83cd-115">Depois disso, o aplicativo lógico poderá acessar os artefatos da sua conta de integração.</span><span class="sxs-lookup"><span data-stu-id="c83cd-115">After that, your logic app can access your integration account's artifacts.</span></span>

## <a name="why-should-you-use-enterprise-integration"></a><span data-ttu-id="c83cd-116">Por que você deve usar a integração corporativa?</span><span class="sxs-lookup"><span data-stu-id="c83cd-116">Why should you use enterprise integration?</span></span>

* <span data-ttu-id="c83cd-117">Com a integração corporativa, é possível armazenar todos os artefatos em um único local: sua conta de integração.</span><span class="sxs-lookup"><span data-stu-id="c83cd-117">With enterprise integration, you can store all your artifacts in one place -- your integration account.</span></span>
* <span data-ttu-id="c83cd-118">É possível criar fluxos de trabalho B2B e integrá-los a aplicativos SaaS (software como serviço) de terceiros, locais e personalizados por meio do mecanismo dos Aplicativo Lógico do Azure e todos seus conectores.</span><span class="sxs-lookup"><span data-stu-id="c83cd-118">You can build B2B workflows and integrate with third-party software-as-service (SaaS) apps, on-premises apps, and custom apps by using the Azure Logic Apps engine and all its connectors.</span></span>
* <span data-ttu-id="c83cd-119">Você pode criar código personalizado para seus aplicativos lógicos com o Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="c83cd-119">You can create custom code for your logic apps with Azure functions.</span></span>

## <a name="how-to-get-started-with-enterprise-integration"></a><span data-ttu-id="c83cd-120">Como começar a usar a integração corporativa?</span><span class="sxs-lookup"><span data-stu-id="c83cd-120">How to get started with enterprise integration?</span></span>

<span data-ttu-id="c83cd-121">É possível criar e gerenciar aplicativos B2B com o Enterprise Integration Pack por meio do Designer de Aplicativos Lógicos no **Portal do Azure**.</span><span class="sxs-lookup"><span data-stu-id="c83cd-121">You can build and manage B2B apps with the Enterprise Integration Pack through the Logic App Designer in the **Azure portal**.</span></span> <span data-ttu-id="c83cd-122">Também é possível gerenciar aplicativos lógicos com o [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Tópicos do PowerShell para aplicativos lógicos").</span><span class="sxs-lookup"><span data-stu-id="c83cd-122">You can also manage your logic apps with [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Logic apps PowerShell topics").</span></span>

<span data-ttu-id="c83cd-123">Confira as etapas de alto nível necessárias para criar aplicativos no Portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="c83cd-123">Here are the high-level steps you must take before you can create apps in the Azure portal:</span></span>

![imagem da visão geral](media/logic-apps-enterprise-integration-overview/overview-0.png)  

## <a name="what-are-some-common-scenarios"></a><span data-ttu-id="c83cd-125">Quais são os cenários comuns?</span><span class="sxs-lookup"><span data-stu-id="c83cd-125">What are some common scenarios?</span></span>

<span data-ttu-id="c83cd-126">O Enterprise Integration oferece suporte a estes padrões do setor:</span><span class="sxs-lookup"><span data-stu-id="c83cd-126">Enterprise Integration supports these industry standards:</span></span>

* <span data-ttu-id="c83cd-127">EDI - Intercâmbio Eletrônico de Dados</span><span class="sxs-lookup"><span data-stu-id="c83cd-127">EDI - Electronic Data Interchange</span></span>
* <span data-ttu-id="c83cd-128">EAI - Integração de Aplicativos Empresariais</span><span class="sxs-lookup"><span data-stu-id="c83cd-128">EAI - Enterprise Application Integration</span></span>

## <a name="heres-what-you-need-to-get-started"></a><span data-ttu-id="c83cd-129">Para começar, você precisa do seguinte</span><span class="sxs-lookup"><span data-stu-id="c83cd-129">Here's what you need to get started</span></span>

* <span data-ttu-id="c83cd-130">Uma assinatura do Azure com uma conta de integração</span><span class="sxs-lookup"><span data-stu-id="c83cd-130">An Azure subscription with an integration account</span></span>
* <span data-ttu-id="c83cd-131">Visual Studio 2015 para criar esquemas e mapas</span><span class="sxs-lookup"><span data-stu-id="c83cd-131">Visual Studio 2015 to create maps and schemas</span></span>
* [<span data-ttu-id="c83cd-132">Microsoft Azure Logic Apps Enterprise Integration Tools for Visual Studio 2015 2.0 (Ferramentas de integração corporativa do Aplicativo Lógico do Microsoft Azure para Visual Studio 2015)</span><span class="sxs-lookup"><span data-stu-id="c83cd-132">Microsoft Azure Logic Apps Enterprise Integration Tools for Visual Studio 2015 2.0</span></span>](https://aka.ms/vsmapsandschemas)  

## <a name="try-it-now"></a><span data-ttu-id="c83cd-133">Teste agora</span><span class="sxs-lookup"><span data-stu-id="c83cd-133">Try it now</span></span>

<span data-ttu-id="c83cd-134">[Implante um exemplo de aplicativo lógico de envio e recebimento AS2 totalmente operacional](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) que usa os recursos B2B do Aplicativo Lógico do Azure.</span><span class="sxs-lookup"><span data-stu-id="c83cd-134">[Deploy a fully operational sample AS2 send & receive logic app](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive) that uses the B2B features for Azure Logic Apps.</span></span>

## <a name="learn-more"></a><span data-ttu-id="c83cd-135">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="c83cd-135">Learn more</span></span>
* [<span data-ttu-id="c83cd-136">Contratos</span><span class="sxs-lookup"><span data-stu-id="c83cd-136">Agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Saiba mais sobre contratos de integração corporativa")
* [<span data-ttu-id="c83cd-137">Cenários B2B (Entre empresas)</span><span class="sxs-lookup"><span data-stu-id="c83cd-137">Business to Business (B2B) scenarios</span></span>](../logic-apps/logic-apps-enterprise-integration-b2b.md "Aprenda a criar Aplicativos lógicos com recursos de B2B")  
* [<span data-ttu-id="c83cd-138">Certificados</span><span class="sxs-lookup"><span data-stu-id="c83cd-138">Certificates</span></span>](logic-apps-enterprise-integration-certificates.md "Saiba mais sobre certificados da integração corporativa")
* [<span data-ttu-id="c83cd-139">Codificação/decodificação de arquivo simples</span><span class="sxs-lookup"><span data-stu-id="c83cd-139">Flat file encoding/decoding</span></span>](logic-apps-enterprise-integration-flatfile.md "Aprenda a codificar e decodificar o conteúdo de arquivo simples")  
* [<span data-ttu-id="c83cd-140">Integration accounts</span><span class="sxs-lookup"><span data-stu-id="c83cd-140">Integration accounts</span></span>](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn about contas de integração")
* [<span data-ttu-id="c83cd-141">Mapas</span><span class="sxs-lookup"><span data-stu-id="c83cd-141">Maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "Saiba mais sobre mapas da integração corporativa")
* [<span data-ttu-id="c83cd-142">Parceiros</span><span class="sxs-lookup"><span data-stu-id="c83cd-142">Partners</span></span>](logic-apps-enterprise-integration-partners.md "Saiba mais sobre parceiros da integração corporativa")
* [<span data-ttu-id="c83cd-143">Esquemas</span><span class="sxs-lookup"><span data-stu-id="c83cd-143">Schemas</span></span>](logic-apps-enterprise-integration-schemas.md "Saiba mais sobre esquemas de integração corporativa")
* [<span data-ttu-id="c83cd-144">Validação de mensagem XML</span><span class="sxs-lookup"><span data-stu-id="c83cd-144">XML message validation</span></span>](logic-apps-enterprise-integration-xml.md "Aprenda a validar mensagens XML com Aplicativos lógicos")
* [<span data-ttu-id="c83cd-145">Transformação de XML</span><span class="sxs-lookup"><span data-stu-id="c83cd-145">XML transform</span></span>](logic-apps-enterprise-integration-transform.md "Saiba mais sobre mapas da integração corporativa")
* [<span data-ttu-id="c83cd-146">Conectores de integração Enterprise</span><span class="sxs-lookup"><span data-stu-id="c83cd-146">Enterprise Integration Connectors</span></span>](../connectors/apis-list.md "Saiba mais sobre os conectores do enterprise integration pack")
* [<span data-ttu-id="c83cd-147">Metadados da conta de integração</span><span class="sxs-lookup"><span data-stu-id="c83cd-147">Integration Account Metadata</span></span>](../logic-apps/logic-apps-enterprise-integration-metadata.md "Saiba mais sobre os metadados da conta de integração")
* [<span data-ttu-id="c83cd-148">Monitorar mensagens B2B</span><span class="sxs-lookup"><span data-stu-id="c83cd-148">Monitor B2B messages</span></span>](logic-apps-monitor-b2b-message.md "Saiba mais sobre o monitoramento de mensagens B2B")
* [<span data-ttu-id="c83cd-149">Rastreando mensagens B2B no portal do OMS</span><span class="sxs-lookup"><span data-stu-id="c83cd-149">Tracking B2B messages in OMS portal</span></span>](logic-apps-track-b2b-messages-omsportal.md "Saiba mais sobre o acompanhamento de mensagens B2B no portal do OMS")

