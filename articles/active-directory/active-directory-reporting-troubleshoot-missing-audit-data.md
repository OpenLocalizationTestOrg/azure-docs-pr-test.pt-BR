---
title: "Solução de problemas: dados ausentes no log de atividades do Azure Active Directory | Microsoft Docs"
description: "Lista os diversos relatórios disponíveis no Azure Active Directory"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 7cbe4337-bb77-4ee0-b254-3e368be06db7
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 47617f8f727027de113a0f503308c8accc58859e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="i-cant-find-some-actions-that-i-performed-in-the-azure-active-directory-activity-log"></a><span data-ttu-id="a4092-103">Não consigo localizar algumas ações que executei no log de atividades do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a4092-103">I can’t find some actions that I performed in the Azure Active Directory activity log</span></span>


## <a name="symptoms"></a><span data-ttu-id="a4092-104">Sintomas</span><span class="sxs-lookup"><span data-stu-id="a4092-104">Symptoms</span></span>

<span data-ttu-id="a4092-105">Eu executei algumas ações no portal do Azure e esperava ver os logs de auditoria para essas ações na folha `Activity logs > Audit Logs`, mas não é possível encontrá-los.</span><span class="sxs-lookup"><span data-stu-id="a4092-105">I performed some actions in the Azure portal and expected to see the audit logs for those actions in the `Activity logs > Audit Logs` blade, but I can’t find them.</span></span>

 ![Relatórios](./media/active-directory-reporting-troubleshoot-missing-audit-data/01.png)
 

## <a name="cause"></a><span data-ttu-id="a4092-107">Causa</span><span class="sxs-lookup"><span data-stu-id="a4092-107">Cause</span></span>

<span data-ttu-id="a4092-108">As ações não são exibidas imediatamente no log de Auditoria da Atividade.</span><span class="sxs-lookup"><span data-stu-id="a4092-108">Actions don’t appear immediately in the Activity Audit log.</span></span> <span data-ttu-id="a4092-109">Ele pode levar de 15 minutos a uma hora para ver os logs de auditoria no portal desde o momento em que a operação é executada.</span><span class="sxs-lookup"><span data-stu-id="a4092-109">It can take anywhere from 15 minutes to an hour to see the audit logs in the portal from the time the operation is performed.</span></span>

## <a name="resolution"></a><span data-ttu-id="a4092-110">Resolução</span><span class="sxs-lookup"><span data-stu-id="a4092-110">Resolution</span></span>

<span data-ttu-id="a4092-111">Aguarde de 15 minutos a uma hora e verifique se as ações aparecem no log.</span><span class="sxs-lookup"><span data-stu-id="a4092-111">Wait for 15 minutes to an hour and see if the actions appear in the log.</span></span> <span data-ttu-id="a4092-112">Se você ainda não os vê, gere um tíquete de suporte conosco e verificaremos o problema.</span><span class="sxs-lookup"><span data-stu-id="a4092-112">If you still don’t see them, please raise a support ticket with us and we will look into it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a4092-113">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a4092-113">Next steps</span></span>
<span data-ttu-id="a4092-114">Veja as [Perguntas frequentes sobre os relatórios do Azure Active Directory](active-directory-reporting-faq.md).</span><span class="sxs-lookup"><span data-stu-id="a4092-114">See the [Azure Active Directory reporting FAQ](active-directory-reporting-faq.md).</span></span>

