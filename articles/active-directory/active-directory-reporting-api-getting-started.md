---
title: "aaaGetting iniciado com a API de relatório de saudação do AD do Azure no portal clássico de saudação do AD do Azure | Microsoft Docs"
description: "Como tooget iniciada com hello Active Directory do Azure API de relatório"
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
ms.openlocfilehash: 52e22d442650731fc6ed28991fc65f9182af0540
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-azure-active-directory-reporting-api-on-hello-azure-ad-classic-portal"></a><span data-ttu-id="5d8e7-103">Guia de Introdução com hello API de relatórios no portal clássico de saudação do AD do Azure Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="5d8e7-103">Getting started with hello Azure Active Directory reporting API on hello Azure AD classic portal</span></span>
<span data-ttu-id="5d8e7-104">*Este tópico faz parte da saudação [do Azure Active Directory Reporting guia](active-directory-reporting-guide.md).*</span><span class="sxs-lookup"><span data-stu-id="5d8e7-104">*This topic is part of hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).*</span></span>

<span data-ttu-id="5d8e7-105">O Azure Active Directory fornece vários relatórios.</span><span class="sxs-lookup"><span data-stu-id="5d8e7-105">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="5d8e7-106">dados Olá desses relatórios podem ser muito útil tooyour aplicativos, como sistemas SIEM, auditoria e ferramentas de business intelligence.</span><span class="sxs-lookup"><span data-stu-id="5d8e7-106">hello data of these reports can be very useful tooyour applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="5d8e7-107">Olá AD do Azure reporting que APIs fornecem dados de toohello acesso programático por meio de um conjunto de APIs com base em REST.</span><span class="sxs-lookup"><span data-stu-id="5d8e7-107">hello Azure AD reporting APIs provide programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="5d8e7-108">Você pode chamar essas APIs de várias ferramentas e linguagens de programação.</span><span class="sxs-lookup"><span data-stu-id="5d8e7-108">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="5d8e7-109">Este artigo fornece informações de saudação necessário tooget iniciado com o relatório de saudação do AD do Azure APIs.</span><span class="sxs-lookup"><span data-stu-id="5d8e7-109">This article provides you with hello information you need tooget started with hello Azure AD reporting APIs.</span></span>
<span data-ttu-id="5d8e7-110">Na próxima seção, Olá, você pode encontrar mais detalhes sobre como usar o hello auditar e APIs de entrada.</span><span class="sxs-lookup"><span data-stu-id="5d8e7-110">In hello next section, you find more details about using hello audit and sign-in APIs.</span></span> <span data-ttu-id="5d8e7-111">Para todas as outras APIs, consulte Olá [relatórios do AD do Azure e events(preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) artigo.</span><span class="sxs-lookup"><span data-stu-id="5d8e7-111">For all other APIs, see hello [Azure AD reports and events(preview)](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-reports-and-events-preview) article.</span></span>

<span data-ttu-id="5d8e7-112">Para dúvidas, problemas ou comentários, entre em contato com a [Ajuda de relatório do AAD](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="5d8e7-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="learning-map"></a><span data-ttu-id="5d8e7-113">Mapa de aprendizagem</span><span class="sxs-lookup"><span data-stu-id="5d8e7-113">Learning map</span></span>
1. <span data-ttu-id="5d8e7-114">**Preparar** -antes de testar as amostras da API, você precisa Olá toocomplete [pré-requisitos tooaccess Olá AD do Azure reporting API](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="5d8e7-114">**Prepare** - Before you can test your API samples, you need toocomplete hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>
2. <span data-ttu-id="5d8e7-115">**Explorar** -Obtenha uma primeira impressão de saudação reporting APIs:</span><span class="sxs-lookup"><span data-stu-id="5d8e7-115">**Explore** - Get a first impression of hello reporting APIs:</span></span>
   
   * [<span data-ttu-id="5d8e7-116">Usando os exemplos de saudação para auditoria Olá API</span><span class="sxs-lookup"><span data-stu-id="5d8e7-116">Using hello samples for hello audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="5d8e7-117">Usando os exemplos de saudação para a API de relatório de atividade de entrada hello</span><span class="sxs-lookup"><span data-stu-id="5d8e7-117">Using hello samples for hello sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="5d8e7-118">**Personalizar** – Criar sua própria solução:</span><span class="sxs-lookup"><span data-stu-id="5d8e7-118">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="5d8e7-119">Usando a referência de API de auditoria Olá</span><span class="sxs-lookup"><span data-stu-id="5d8e7-119">Using hello audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="5d8e7-120">Usando o relatório de atividade de entrada hello referência de API</span><span class="sxs-lookup"><span data-stu-id="5d8e7-120">Using hello sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="5d8e7-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5d8e7-121">Next Steps</span></span>
<span data-ttu-id="5d8e7-122">Se você estiver curioso toosee todos Olá pontos de extremidade de API do Azure AD Graph disponíveis navegando muito[https://graph.windows.net/tenant-name/reports/$ metadados? api-version = beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span><span class="sxs-lookup"><span data-stu-id="5d8e7-122">If you are curious toosee all of hello available Azure AD Graph API endpoints by navigating too[https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta](https://graph.windows.net/tenant-name/reports/$metadata?api-version=beta).</span></span>

