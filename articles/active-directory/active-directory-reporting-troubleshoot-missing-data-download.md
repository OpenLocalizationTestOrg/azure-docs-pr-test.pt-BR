---
title: "Solução de problemas: Dados ausentes no hello baixado logs de atividade do Active Directory do Azure | Microsoft Docs"
description: "Fornece dados de toomissing uma resolução nos logs de atividade baixados do Active Directory do Azure."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 027b70e6efc570f81d3c836f50ee52aaa89be71a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="i-cant-find-any-data-in-hello-azure-active-directory-activity-logs-i-have-downloaded"></a><span data-ttu-id="04386-103">Não é possível localizar nenhum dado nos logs de atividade do Active Directory do Azure Olá que eu tenha baixado</span><span class="sxs-lookup"><span data-stu-id="04386-103">I can’t find any data in hello Azure Active Directory activity logs I have downloaded</span></span>


## <a name="symptoms"></a><span data-ttu-id="04386-104">Sintomas</span><span class="sxs-lookup"><span data-stu-id="04386-104">Symptoms</span></span>

<span data-ttu-id="04386-105">Baixei logs de atividade hello (ou entradas de auditoria) e não vejo todos os registros de saudação para tempo de saudação que escolher.</span><span class="sxs-lookup"><span data-stu-id="04386-105">I downloaded hello activity logs (audit or sign-ins) and I don’t see all hello records for hello time I chose.</span></span> <span data-ttu-id="04386-106">Por quê?</span><span class="sxs-lookup"><span data-stu-id="04386-106">Why?</span></span> 

 ![Relatórios](./media/active-directory-reporting-troubleshoot-missing-data-download/01.png)
 

## <a name="cause"></a><span data-ttu-id="04386-108">Causa</span><span class="sxs-lookup"><span data-stu-id="04386-108">Cause</span></span>

<span data-ttu-id="04386-109">Quando você baixa os logs de atividade no hello portal do Azure, estamos limitar os registros de too120K de escala hello, classificados por mais recente.</span><span class="sxs-lookup"><span data-stu-id="04386-109">When you download activity logs in hello Azure portal, we limit hello scale too120K records, sorted by most recent.</span></span> 

## <a name="resolution"></a><span data-ttu-id="04386-110">Resolução</span><span class="sxs-lookup"><span data-stu-id="04386-110">Resolution</span></span>

<span data-ttu-id="04386-111">Você pode aproveitar [APIs de relatórios do Azure AD](active-directory-reporting-api-getting-started.md) toofetch tooa milhões de registros em qualquer momento específico.</span><span class="sxs-lookup"><span data-stu-id="04386-111">You can leverage [Azure AD Reporting APIs](active-directory-reporting-api-getting-started.md) toofetch up tooa million records at any given point.</span></span> <span data-ttu-id="04386-112">Nossa abordagem recomendada é toorun um script em uma base agendada que chama Olá reporting APIs toofetch registra de forma incremental em um período de tempo (por exemplo, diária ou semanalmente).</span><span class="sxs-lookup"><span data-stu-id="04386-112">Our recommended approach is toorun a script on a scheduled basis that calls hello reporting APIs toofetch records in an incremental fashion over a period of time (e.g., daily or weekly).</span></span>

## <a name="next-steps"></a><span data-ttu-id="04386-113">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="04386-113">Next steps</span></span>
<span data-ttu-id="04386-114">Consulte Olá [reporting perguntas frequentes sobre o Active Directory do Azure](active-directory-reporting-faq.md).</span><span class="sxs-lookup"><span data-stu-id="04386-114">See hello [Azure Active Directory reporting FAQ](active-directory-reporting-faq.md).</span></span>

