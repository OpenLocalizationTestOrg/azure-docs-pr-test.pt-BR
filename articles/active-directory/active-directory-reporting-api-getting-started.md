---
title: "Introdução à API de relatório do Azure AD no Portal clássico do Azure AD | Microsoft Docs"
description: "Como começar a usar a API de relatório do Azure Active Directory"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 8813b911-a4ec-4234-8474-2eef9afea11e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/18/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 5e98b660fe19bb8abebf1c3b996b6295a6c4e728
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-the-azure-active-directory-reporting-api-on-the-azure-ad-classic-portal"></a><span data-ttu-id="6cb19-103">Introdução à API de relatório do Azure Active Directory no Portal clássico do Azure AD</span><span class="sxs-lookup"><span data-stu-id="6cb19-103">Getting started with the Azure Active Directory reporting API on the Azure AD classic portal</span></span>
<span data-ttu-id="6cb19-104">*Este tópico faz parte do [Guia de Relatórios do Azure Active Directory](active-directory-reporting-guide.md).*</span><span class="sxs-lookup"><span data-stu-id="6cb19-104">*This topic is part of the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).*</span></span>

<span data-ttu-id="6cb19-105">O Azure Active Directory fornece vários relatórios.</span><span class="sxs-lookup"><span data-stu-id="6cb19-105">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="6cb19-106">Os dados desses relatórios podem ser muito úteis para seus aplicativos, como sistemas SIEM, auditoria e ferramentas de business intelligence.</span><span class="sxs-lookup"><span data-stu-id="6cb19-106">The data of these reports can be very useful to your applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="6cb19-107">As APIs de relatório do Azure AD fornecem acesso programático aos dados através de um conjunto de APIs baseadas em REST.</span><span class="sxs-lookup"><span data-stu-id="6cb19-107">The Azure AD reporting APIs provide programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="6cb19-108">Você pode chamar essas APIs de várias ferramentas e linguagens de programação.</span><span class="sxs-lookup"><span data-stu-id="6cb19-108">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="6cb19-109">Este artigo fornece as informações necessárias para começar com as APIs de relatório do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6cb19-109">This article provides you with the information you need to get started with the Azure AD reporting APIs.</span></span>
<span data-ttu-id="6cb19-110">Na próxima seção, você encontrará mais detalhes sobre como usar as APIs de auditoria e de entrada.</span><span class="sxs-lookup"><span data-stu-id="6cb19-110">In the next section, you find more details about using the audit and sign-in APIs.</span></span> <span data-ttu-id="6cb19-111">Para todas as outras APIs, consulte o artigo [Eventos e relatórios do Azure AD (versão prévia)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview).</span><span class="sxs-lookup"><span data-stu-id="6cb19-111">For all other APIs, see the [Azure AD reports and events(preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) article.</span></span>

<span data-ttu-id="6cb19-112">Para dúvidas, problemas ou comentários, entre em contato com a [Ajuda de relatório do AAD](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="6cb19-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="learning-map"></a><span data-ttu-id="6cb19-113">Mapa de aprendizagem</span><span class="sxs-lookup"><span data-stu-id="6cb19-113">Learning map</span></span>
1. <span data-ttu-id="6cb19-114">**Prepare-se** – Antes de testar os exemplos de API, você precisa atender aos [pré-requisitos para acessar a API de relatório do Azure AD](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="6cb19-114">**Prepare** - Before you can test your API samples, you need to complete the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>
2. <span data-ttu-id="6cb19-115">**Explore** – Tenha uma primeira impressão das APIs de relatórios:</span><span class="sxs-lookup"><span data-stu-id="6cb19-115">**Explore** - Get a first impression of the reporting APIs:</span></span>
   
   * [<span data-ttu-id="6cb19-116">Usar os exemplos para a API de auditoria</span><span class="sxs-lookup"><span data-stu-id="6cb19-116">Using the samples for the audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="6cb19-117">Usar os exemplos para a API de relatório de atividade de entrada</span><span class="sxs-lookup"><span data-stu-id="6cb19-117">Using the samples for the sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="6cb19-118">**Personalizar** – Criar sua própria solução:</span><span class="sxs-lookup"><span data-stu-id="6cb19-118">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="6cb19-119">Usar a referência de API de auditoria</span><span class="sxs-lookup"><span data-stu-id="6cb19-119">Using the audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="6cb19-120">Usar a referência da API de relatório de atividade de entrada</span><span class="sxs-lookup"><span data-stu-id="6cb19-120">Using the sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="6cb19-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6cb19-121">Next Steps</span></span>
<span data-ttu-id="6cb19-122">Se você estiver curioso para ver todos os pontos de extremidade de API do Graph do Azure AD navegando até [https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span><span class="sxs-lookup"><span data-stu-id="6cb19-122">If you are curious to see all of the available Azure AD Graph API endpoints by navigating to [https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span></span>

