---
title: "aaaGetting iniciado com a API de relatório de saudação do AD do Azure | Microsoft Docs"
description: "Como tooget iniciada com hello Active Directory do Azure API de relatório"
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
ms.openlocfilehash: bb7d72ba445daa367d7502889c38a605a16f26d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-azure-active-directory-reporting-api"></a><span data-ttu-id="c7e7e-103">Guia de Introdução ao Olá do Active Directory do Azure API de relatório</span><span class="sxs-lookup"><span data-stu-id="c7e7e-103">Getting started with hello Azure Active Directory reporting API</span></span>

<span data-ttu-id="c7e7e-104">O Azure Active Directory fornece vários relatórios.</span><span class="sxs-lookup"><span data-stu-id="c7e7e-104">Azure Active Directory provides you with a variety of reports.</span></span> <span data-ttu-id="c7e7e-105">dados Olá desses relatórios podem ser muito útil tooyour aplicativos, como sistemas SIEM, auditoria e ferramentas de business intelligence.</span><span class="sxs-lookup"><span data-stu-id="c7e7e-105">hello data of these reports can be very useful tooyour applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="c7e7e-106">Olá AD do Azure reporting que APIs fornecem dados de toohello acesso programático por meio de um conjunto de APIs com base em REST.</span><span class="sxs-lookup"><span data-stu-id="c7e7e-106">hello Azure AD reporting APIs provide programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="c7e7e-107">Você pode chamar essas APIs de várias ferramentas e linguagens de programação.</span><span class="sxs-lookup"><span data-stu-id="c7e7e-107">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="c7e7e-108">Este artigo fornece informações de saudação necessário tooget iniciado com o relatório de saudação do AD do Azure APIs.</span><span class="sxs-lookup"><span data-stu-id="c7e7e-108">This article provides you with hello information you need tooget started with hello Azure AD reporting APIs.</span></span>
<span data-ttu-id="c7e7e-109">Na próxima seção, Olá, você pode encontrar mais detalhes sobre como usar o hello auditar e APIs de entrada.</span><span class="sxs-lookup"><span data-stu-id="c7e7e-109">In hello next section, you find more details about using hello audit and sign-in APIs.</span></span> 

<span data-ttu-id="c7e7e-110">Para ver perguntas frequentes, leia nossas [Perguntas Frequentes](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-faq).</span><span class="sxs-lookup"><span data-stu-id="c7e7e-110">For frequently asked questions,read our [FAQ](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-faq).</span></span> <span data-ttu-id="c7e7e-111">Para solucionar problemas, [registre um tíquete de suporte](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto)</span><span class="sxs-lookup"><span data-stu-id="c7e7e-111">For issues, please [file a support ticket](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto)</span></span>

## <a name="learning-map"></a><span data-ttu-id="c7e7e-112">Mapa de aprendizagem</span><span class="sxs-lookup"><span data-stu-id="c7e7e-112">Learning map</span></span>
1. <span data-ttu-id="c7e7e-113">**Preparar** -antes de testar as amostras da API, você precisa Olá toocomplete [pré-requisitos tooaccess Olá AD do Azure reporting API](active-directory-reporting-api-prerequisites-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c7e7e-113">**Prepare** - Before you can test your API samples, you need toocomplete hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites-azure-portal.md).</span></span>
2. <span data-ttu-id="c7e7e-114">**Explorar** -Obtenha uma primeira impressão de saudação reporting APIs:</span><span class="sxs-lookup"><span data-stu-id="c7e7e-114">**Explore** - Get a first impression of hello reporting APIs:</span></span>
   
   * [<span data-ttu-id="c7e7e-115">Usando os exemplos de saudação para auditoria Olá API</span><span class="sxs-lookup"><span data-stu-id="c7e7e-115">Using hello samples for hello audit API</span></span>](active-directory-reporting-api-audit-samples.md) 
   * [<span data-ttu-id="c7e7e-116">Usando os exemplos de saudação para a API de relatório de atividade de entrada hello</span><span class="sxs-lookup"><span data-stu-id="c7e7e-116">Using hello samples for hello sign-in activity report API</span></span>](active-directory-reporting-api-sign-in-activity-samples.md)
3. <span data-ttu-id="c7e7e-117">**Personalizar** – Criar sua própria solução:</span><span class="sxs-lookup"><span data-stu-id="c7e7e-117">**Customize** -  Create your own solution:</span></span> 
   
   * [<span data-ttu-id="c7e7e-118">Usando a referência de API de auditoria Olá</span><span class="sxs-lookup"><span data-stu-id="c7e7e-118">Using hello audit API reference</span></span>](active-directory-reporting-api-audit-reference.md) 
   * [<span data-ttu-id="c7e7e-119">Usando o relatório de atividade de entrada hello referência de API</span><span class="sxs-lookup"><span data-stu-id="c7e7e-119">Using hello sign-in activity report API reference</span></span>](active-directory-reporting-api-sign-in-activity-reference.md)

## <a name="next-steps"></a><span data-ttu-id="c7e7e-120">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c7e7e-120">Next Steps</span></span>
<span data-ttu-id="c7e7e-121">Se você estiver curioso toosee todos os pontos de API do Azure AD Graph disponíveis, use este link: [https://graph.windows.net/tenant-name/activities/$ metadados? api-version = beta](https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta).</span><span class="sxs-lookup"><span data-stu-id="c7e7e-121">If you are curious toosee all available Azure AD Graph API endpoints, use this link: [https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta](https://graph.windows.net/tenant-name/activities/$metadata?api-version=beta).</span></span>

