---
title: "políticas de retenção de relatórios do Active Directory aaaAzure | Microsoft Docs"
description: "Políticas de retenção sobre dados de relatório no Active Directory do Azure"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 183e53b0-0647-42e7-8abe-3e9ff424de12
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c46a68198cb34e9c92662b2f8461010745392c04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-report-retention-policies"></a><span data-ttu-id="7cf46-103">Políticas de retenção de relatório do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7cf46-103">Azure Active Directory report retention policies</span></span>


<span data-ttu-id="7cf46-104">Este tópico fornece respostas a perguntas mais comuns toohello em conjunto com a retenção de dados Olá para relatórios de atividade diferente Olá no Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="7cf46-104">This topic provides you with answers toohello most common questions in conjunction with hello data retention for hello different activity reports in Azure Active Directory.</span></span> 

<span data-ttu-id="7cf46-105">**P: como você pode obter a coleção Olá de dados da atividade iniciados?**</span><span class="sxs-lookup"><span data-stu-id="7cf46-105">**Q: How can you get hello collection of activity data started?**</span></span>

<span data-ttu-id="7cf46-106">**R:**</span><span class="sxs-lookup"><span data-stu-id="7cf46-106">**A:**</span></span>

| <span data-ttu-id="7cf46-107">Edição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7cf46-107">Azure AD Edition</span></span> | <span data-ttu-id="7cf46-108">Início da Coleta</span><span class="sxs-lookup"><span data-stu-id="7cf46-108">Collection Start</span></span> |
| :--              | :--   |
| <span data-ttu-id="7cf46-109">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="7cf46-109">Azure AD Premium P1</span></span> <br /> <span data-ttu-id="7cf46-110">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="7cf46-110">Azure AD Premium P2</span></span> | <span data-ttu-id="7cf46-111">Quando você se inscreve para uma assinatura</span><span class="sxs-lookup"><span data-stu-id="7cf46-111">When you sign-up for a subscription</span></span> |
| <span data-ttu-id="7cf46-112">AD do Azure Gratuito</span><span class="sxs-lookup"><span data-stu-id="7cf46-112">Azure AD Free</span></span> | <span data-ttu-id="7cf46-113">Olá a primeira vez que abrir Olá [folha do Active Directory do Azure](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) ou use Olá [reporting APIs](https://aka.ms/aadreports)</span><span class="sxs-lookup"><span data-stu-id="7cf46-113">hello first time you open hello [Azure Active Directory blade](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) or use hello [reporting APIs](https://aka.ms/aadreports)</span></span>  |

---
<span data-ttu-id="7cf46-114">**P: quando seus dados de atividade está disponível no portal do Azure de saudação?**</span><span class="sxs-lookup"><span data-stu-id="7cf46-114">**Q: When is your activity data available in hello Azure portal?**</span></span>

<span data-ttu-id="7cf46-115">**R:**</span><span class="sxs-lookup"><span data-stu-id="7cf46-115">**A:**</span></span>

- <span data-ttu-id="7cf46-116">**Imediatamente** - se você já estiver trabalhando com relatórios no hello portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="7cf46-116">**Immediately** - If you have already been working with reports in hello Azure classic portal</span></span>
- <span data-ttu-id="7cf46-117">**Dentro de 2 horas** - se você não tiver ativado reporting em Olá portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="7cf46-117">**Within 2 hours** - If you haven’t turned reporting on  in hello Azure classic portal</span></span>

---
<span data-ttu-id="7cf46-118">**P: como você pode obter a coleção Olá de sinais de segurança iniciado?**</span><span class="sxs-lookup"><span data-stu-id="7cf46-118">**Q: How can you get hello collection of security signals started?**</span></span>  

<span data-ttu-id="7cf46-119">**R:** para sinais de segurança, o processo de coleta Olá inicia quando você participar do Centro de proteção de identidade toouse hello.</span><span class="sxs-lookup"><span data-stu-id="7cf46-119">**A:** For security signals, hello collection process starts when you opt-in toouse hello Identity Protection Center.</span></span> 


---
<span data-ttu-id="7cf46-120">**P: por quanto tempo hello coletados dados são armazenados?**</span><span class="sxs-lookup"><span data-stu-id="7cf46-120">**Q: For how long is hello collected data stored?**</span></span>

<span data-ttu-id="7cf46-121">**R:**</span><span class="sxs-lookup"><span data-stu-id="7cf46-121">**A:**</span></span>

<span data-ttu-id="7cf46-122">**Relatórios de atividades**</span><span class="sxs-lookup"><span data-stu-id="7cf46-122">**Activity reports**</span></span>    

| <span data-ttu-id="7cf46-123">Relatório</span><span class="sxs-lookup"><span data-stu-id="7cf46-123">Report</span></span>                 | <span data-ttu-id="7cf46-124">AD do Azure Gratuito</span><span class="sxs-lookup"><span data-stu-id="7cf46-124">Azure AD Free</span></span> | <span data-ttu-id="7cf46-125">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="7cf46-125">Azure AD Premium P1</span></span> | <span data-ttu-id="7cf46-126">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="7cf46-126">Azure AD Premium P2</span></span> |
| :--                    | :--           | :--                 | :--                 |
| <span data-ttu-id="7cf46-127">Auditoria de Diretório</span><span class="sxs-lookup"><span data-stu-id="7cf46-127">Directory Audit</span></span>        | <span data-ttu-id="7cf46-128">7 dias</span><span class="sxs-lookup"><span data-stu-id="7cf46-128">7 days</span></span>        | <span data-ttu-id="7cf46-129">30 dias</span><span class="sxs-lookup"><span data-stu-id="7cf46-129">30 days</span></span>             | <span data-ttu-id="7cf46-130">30 dias</span><span class="sxs-lookup"><span data-stu-id="7cf46-130">30 days</span></span>             |
| <span data-ttu-id="7cf46-131">Atividade de Entrada</span><span class="sxs-lookup"><span data-stu-id="7cf46-131">Sign-in Activity</span></span>       | <span data-ttu-id="7cf46-132">7 dias</span><span class="sxs-lookup"><span data-stu-id="7cf46-132">7 days</span></span>        | <span data-ttu-id="7cf46-133">30 dias</span><span class="sxs-lookup"><span data-stu-id="7cf46-133">30 days</span></span>             | <span data-ttu-id="7cf46-134">30 dias</span><span class="sxs-lookup"><span data-stu-id="7cf46-134">30 days</span></span>             |

<span data-ttu-id="7cf46-135">**Sinais de Segurança**</span><span class="sxs-lookup"><span data-stu-id="7cf46-135">**Security Signals**</span></span>

| <span data-ttu-id="7cf46-136">Relatório</span><span class="sxs-lookup"><span data-stu-id="7cf46-136">Report</span></span>         | <span data-ttu-id="7cf46-137">AD do Azure Gratuito</span><span class="sxs-lookup"><span data-stu-id="7cf46-137">Azure AD Free</span></span> | <span data-ttu-id="7cf46-138">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="7cf46-138">Azure AD Premium P1</span></span> | <span data-ttu-id="7cf46-139">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="7cf46-139">Azure AD Premium P2</span></span> |
| :--            | :--           | :--                 | :--                 |
| <span data-ttu-id="7cf46-140">Usuários em risco</span><span class="sxs-lookup"><span data-stu-id="7cf46-140">Users at risk</span></span>  | <span data-ttu-id="7cf46-141">7 dias</span><span class="sxs-lookup"><span data-stu-id="7cf46-141">7 days</span></span>        | <span data-ttu-id="7cf46-142">30 dias</span><span class="sxs-lookup"><span data-stu-id="7cf46-142">30 days</span></span>             | <span data-ttu-id="7cf46-143">90 dias</span><span class="sxs-lookup"><span data-stu-id="7cf46-143">90 days</span></span>             |
| <span data-ttu-id="7cf46-144">Entradas de risco</span><span class="sxs-lookup"><span data-stu-id="7cf46-144">Risky sign-ins</span></span> | <span data-ttu-id="7cf46-145">7 dias</span><span class="sxs-lookup"><span data-stu-id="7cf46-145">7 days</span></span>        | <span data-ttu-id="7cf46-146">30 dias</span><span class="sxs-lookup"><span data-stu-id="7cf46-146">30 days</span></span>             | <span data-ttu-id="7cf46-147">90 dias</span><span class="sxs-lookup"><span data-stu-id="7cf46-147">90 days</span></span>             |

---