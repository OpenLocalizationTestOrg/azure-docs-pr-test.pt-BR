---
title: "Políticas de retenção de relatório do Azure Active Directory | Microsoft Docs"
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
ms.openlocfilehash: ffeba8a6c32a21c75af21f948bbd6ea88dd9278c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-report-retention-policies"></a><span data-ttu-id="395b1-103">Políticas de retenção de relatório do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="395b1-103">Azure Active Directory report retention policies</span></span>


<span data-ttu-id="395b1-104">Este tópico fornece respostas para as perguntas mais comuns em conjunto com a retenção de dados para os relatórios de atividade diferente no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="395b1-104">This topic provides you with answers to the most common questions in conjunction with the data retention for the different activity reports in Azure Active Directory.</span></span> 

<span data-ttu-id="395b1-105">**P: Como você pode iniciar a coleta de dados de atividade?**</span><span class="sxs-lookup"><span data-stu-id="395b1-105">**Q: How can you get the collection of activity data started?**</span></span>

<span data-ttu-id="395b1-106">**R:**</span><span class="sxs-lookup"><span data-stu-id="395b1-106">**A:**</span></span>

| <span data-ttu-id="395b1-107">Edição do Azure AD</span><span class="sxs-lookup"><span data-stu-id="395b1-107">Azure AD Edition</span></span> | <span data-ttu-id="395b1-108">Início da Coleta</span><span class="sxs-lookup"><span data-stu-id="395b1-108">Collection Start</span></span> |
| :--              | :--   |
| <span data-ttu-id="395b1-109">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="395b1-109">Azure AD Premium P1</span></span> <br /> <span data-ttu-id="395b1-110">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="395b1-110">Azure AD Premium P2</span></span> | <span data-ttu-id="395b1-111">Quando você se inscreve para uma assinatura</span><span class="sxs-lookup"><span data-stu-id="395b1-111">When you sign-up for a subscription</span></span> |
| <span data-ttu-id="395b1-112">AD do Azure Gratuito</span><span class="sxs-lookup"><span data-stu-id="395b1-112">Azure AD Free</span></span> | <span data-ttu-id="395b1-113">Na primeira vez que você abrir a [folha do Azure Active Directory](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) ou usar as [APIs de relatório](https://aka.ms/aadreports)</span><span class="sxs-lookup"><span data-stu-id="395b1-113">The first time you open the [Azure Active Directory blade](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) or use the [reporting APIs](https://aka.ms/aadreports)</span></span>  |

---
<span data-ttu-id="395b1-114">**P: Quando os dados de atividade estarão disponíveis no Portal do Azure?**</span><span class="sxs-lookup"><span data-stu-id="395b1-114">**Q: When is your activity data available in the Azure portal?**</span></span>

<span data-ttu-id="395b1-115">**R:**</span><span class="sxs-lookup"><span data-stu-id="395b1-115">**A:**</span></span>

- <span data-ttu-id="395b1-116">**Imediatamente** - se você já estiver trabalhando com relatórios no portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="395b1-116">**Immediately** - If you have already been working with reports in the Azure classic portal</span></span>
- <span data-ttu-id="395b1-117">**Em até 2 horas** - se você ainda não tiver ativado os relatórios no portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="395b1-117">**Within 2 hours** - If you haven’t turned reporting on  in the Azure classic portal</span></span>

---
<span data-ttu-id="395b1-118">**P: Como você pode iniciar a coleta de sinais de segurança?**</span><span class="sxs-lookup"><span data-stu-id="395b1-118">**Q: How can you get the collection of security signals started?**</span></span>  

<span data-ttu-id="395b1-119">**R:** Para sinais de segurança, o processo de coleta é iniciado quando você aceita usar o Centro de Proteção de Identidade.</span><span class="sxs-lookup"><span data-stu-id="395b1-119">**A:** For security signals, the collection process starts when you opt-in to use the Identity Protection Center.</span></span> 


---
<span data-ttu-id="395b1-120">**P: Por quanto tempo os dados coletados são armazenados?**</span><span class="sxs-lookup"><span data-stu-id="395b1-120">**Q: For how long is the collected data stored?**</span></span>

<span data-ttu-id="395b1-121">**R:**</span><span class="sxs-lookup"><span data-stu-id="395b1-121">**A:**</span></span>

<span data-ttu-id="395b1-122">**Relatórios de atividades**</span><span class="sxs-lookup"><span data-stu-id="395b1-122">**Activity reports**</span></span>    

| <span data-ttu-id="395b1-123">Relatório</span><span class="sxs-lookup"><span data-stu-id="395b1-123">Report</span></span>                 | <span data-ttu-id="395b1-124">AD do Azure Gratuito</span><span class="sxs-lookup"><span data-stu-id="395b1-124">Azure AD Free</span></span> | <span data-ttu-id="395b1-125">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="395b1-125">Azure AD Premium P1</span></span> | <span data-ttu-id="395b1-126">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="395b1-126">Azure AD Premium P2</span></span> |
| :--                    | :--           | :--                 | :--                 |
| <span data-ttu-id="395b1-127">Auditoria de Diretório</span><span class="sxs-lookup"><span data-stu-id="395b1-127">Directory Audit</span></span>        | <span data-ttu-id="395b1-128">7 dias</span><span class="sxs-lookup"><span data-stu-id="395b1-128">7 days</span></span>        | <span data-ttu-id="395b1-129">30 dias</span><span class="sxs-lookup"><span data-stu-id="395b1-129">30 days</span></span>             | <span data-ttu-id="395b1-130">30 dias</span><span class="sxs-lookup"><span data-stu-id="395b1-130">30 days</span></span>             |
| <span data-ttu-id="395b1-131">Atividade de Entrada</span><span class="sxs-lookup"><span data-stu-id="395b1-131">Sign-in Activity</span></span>       | <span data-ttu-id="395b1-132">7 dias</span><span class="sxs-lookup"><span data-stu-id="395b1-132">7 days</span></span>        | <span data-ttu-id="395b1-133">30 dias</span><span class="sxs-lookup"><span data-stu-id="395b1-133">30 days</span></span>             | <span data-ttu-id="395b1-134">30 dias</span><span class="sxs-lookup"><span data-stu-id="395b1-134">30 days</span></span>             |

<span data-ttu-id="395b1-135">**Sinais de Segurança**</span><span class="sxs-lookup"><span data-stu-id="395b1-135">**Security Signals**</span></span>

| <span data-ttu-id="395b1-136">Relatório</span><span class="sxs-lookup"><span data-stu-id="395b1-136">Report</span></span>         | <span data-ttu-id="395b1-137">AD do Azure Gratuito</span><span class="sxs-lookup"><span data-stu-id="395b1-137">Azure AD Free</span></span> | <span data-ttu-id="395b1-138">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="395b1-138">Azure AD Premium P1</span></span> | <span data-ttu-id="395b1-139">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="395b1-139">Azure AD Premium P2</span></span> |
| :--            | :--           | :--                 | :--                 |
| <span data-ttu-id="395b1-140">Usuários em risco</span><span class="sxs-lookup"><span data-stu-id="395b1-140">Users at risk</span></span>  | <span data-ttu-id="395b1-141">7 dias</span><span class="sxs-lookup"><span data-stu-id="395b1-141">7 days</span></span>        | <span data-ttu-id="395b1-142">30 dias</span><span class="sxs-lookup"><span data-stu-id="395b1-142">30 days</span></span>             | <span data-ttu-id="395b1-143">90 dias</span><span class="sxs-lookup"><span data-stu-id="395b1-143">90 days</span></span>             |
| <span data-ttu-id="395b1-144">Entradas de risco</span><span class="sxs-lookup"><span data-stu-id="395b1-144">Risky sign-ins</span></span> | <span data-ttu-id="395b1-145">7 dias</span><span class="sxs-lookup"><span data-stu-id="395b1-145">7 days</span></span>        | <span data-ttu-id="395b1-146">30 dias</span><span class="sxs-lookup"><span data-stu-id="395b1-146">30 days</span></span>             | <span data-ttu-id="395b1-147">90 dias</span><span class="sxs-lookup"><span data-stu-id="395b1-147">90 days</span></span>             |

---