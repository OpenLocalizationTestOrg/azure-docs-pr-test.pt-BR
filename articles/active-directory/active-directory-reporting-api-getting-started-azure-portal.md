---
title: "Introdução à API de relatório do Azure AD | Microsoft Docs"
description: "Como começar a usar a API de relatório do Azure Active Directory"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8813b911-a4ec-4234-8474-2eef9afea11e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/18/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 9944cbd2b1b7c4acb18d37da1394c0bbc170f77d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="getting-started-with-the-azure-active-directory-reporting-api"></a><span data-ttu-id="cbb13-103">Introdução à API de relatório do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cbb13-103">Getting started with the Azure Active Directory reporting API</span></span>

<span data-ttu-id="cbb13-104">O Azure Active Directory fornece vários relatórios.</span><span class="sxs-lookup"><span data-stu-id="cbb13-104">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="cbb13-105">Os dados desses relatórios podem ser muito úteis para seus aplicativos, como sistemas SIEM, auditoria e ferramentas de business intelligence.</span><span class="sxs-lookup"><span data-stu-id="cbb13-105">The data of these reports can be very useful to your applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="cbb13-106">As APIs de relatório do Azure AD fornecem acesso programático aos dados através de um conjunto de APIs baseadas em REST.</span><span class="sxs-lookup"><span data-stu-id="cbb13-106">The Azure AD reporting APIs provide programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="cbb13-107">Você pode chamar essas APIs de várias ferramentas e linguagens de programação.</span><span class="sxs-lookup"><span data-stu-id="cbb13-107">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="cbb13-108">Este artigo fornece as informações necessárias para começar com as APIs de relatório do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cbb13-108">This article provides you with the information you need to get started with the Azure AD reporting APIs.</span></span>
<span data-ttu-id="cbb13-109">Na próxima seção, você encontrará mais detalhes sobre como usar as APIs de auditoria e de entrada.</span><span class="sxs-lookup"><span data-stu-id="cbb13-109">In the next section, you find more details about using the audit and sign-in APIs.</span></span> 

<span data-ttu-id="cbb13-110">Para ver perguntas frequentes, leia nossas [Perguntas Frequentes](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-faq).</span><span class="sxs-lookup"><span data-stu-id="cbb13-110">For frequently asked questions,read our [FAQ](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-faq).</span></span> <span data-ttu-id="cbb13-111">Para solucionar problemas, [registre um tíquete de suporte](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto)</span><span class="sxs-lookup"><span data-stu-id="cbb13-111">For issues, please [file a support ticket](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto)</span></span>

## <a name="learning-map"></a><span data-ttu-id="cbb13-112">Mapa de aprendizagem</span><span class="sxs-lookup"><span data-stu-id="cbb13-112">Learning map</span></span>
1. <span data-ttu-id="cbb13-113">**Prepare-se** – Antes de testar os exemplos de API, você precisa atender aos [pré-requisitos para acessar a API de relatório do Azure AD](active-directory-reporting-api-prerequisites-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cbb13-113">**Prepare** - Before you can test your API samples, you need to complete the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites-azure-portal.md).</span></span>
2. <span data-ttu-id="cbb13-114">**Explore** – Tenha uma primeira impressão das APIs de relatórios:</span><span class="sxs-lookup"><span data-stu-id="cbb13-114">**Explore** - Get a first impression of the reporting APIs:</span></span>
   
   * [<span data-ttu-id="cbb13-115">Usar os exemplos para a API de auditoria</span><span class="sxs-lookup"><span data-stu-id="cbb13-115">Using the samples for the audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="cbb13-116">Usar os exemplos para a API de relatório de atividade de entrada</span><span class="sxs-lookup"><span data-stu-id="cbb13-116">Using the samples for the sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="cbb13-117">**Personalizar** – Criar sua própria solução:</span><span class="sxs-lookup"><span data-stu-id="cbb13-117">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="cbb13-118">Usar a referência de API de auditoria</span><span class="sxs-lookup"><span data-stu-id="cbb13-118">Using the audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="cbb13-119">Usar a referência da API de relatório de atividade de entrada</span><span class="sxs-lookup"><span data-stu-id="cbb13-119">Using the sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="cbb13-120">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cbb13-120">Next Steps</span></span>
<span data-ttu-id="cbb13-121">Se estiver curioso para ver todos os pontos de extremidade disponíveis da API do Graph do Azure AD, use este link [https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta](https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta).</span><span class="sxs-lookup"><span data-stu-id="cbb13-121">If you are curious to see all available Azure AD Graph API endpoints, use this link: [https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta](https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta).</span></span>

