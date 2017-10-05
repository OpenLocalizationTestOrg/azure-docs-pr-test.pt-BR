---
title: "Perguntas frequentes sobre relatórios do Azure Active Directory | Microsoft Docs"
description: "Perguntas frequentes sobre relatórios do Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 534da0b1-7858-4167-9986-7a62fbd10439
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: accf292f70bf0eafdefc00c3feeaf8e346605401
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-reporting-faq"></a><span data-ttu-id="7edc5-103">Perguntas frequentes sobre relatórios do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7edc5-103">Azure Active Directory reporting FAQ</span></span>

<span data-ttu-id="7edc5-104">Este artigo inclui respostas para FAQs (perguntas frequentes) sobre os relatórios do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7edc5-104">This article includes answers to frequently asked questions (FAQs) about Azure Active Directory reporting.</span></span>  
<span data-ttu-id="7edc5-105">Para obter mais detalhes, veja [Relatórios do Azure Active Directory](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7edc5-105">For more details, see [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span> 

<span data-ttu-id="7edc5-106">**P: O que é a retenção de dados para logs de atividade (de entradas e de auditoria) no Portal do Azure?**</span><span class="sxs-lookup"><span data-stu-id="7edc5-106">**Q: What is the data retention for activity logs (Audit and Sign-ins) in the Azure portal?**</span></span> 

<span data-ttu-id="7edc5-107">**R:** Fornecemos 7 dias de dados para nossos clientes com acesso gratuito e, alternando para uma licença Azure AD Premium 1 ou Premium 2, você pode acessar dados por até 30 dias.</span><span class="sxs-lookup"><span data-stu-id="7edc5-107">**A:** We provide 7 days of data for our free customers and by switching to an Azure AD Premium 1 or Premium 2 license, you can access data for up to 30 days.</span></span> <span data-ttu-id="7edc5-108">Para obter mais detalhes sobre a retenção, consulte [Políticas de retenção de relatório do Azure Active Directory](active-directory-reporting-retention.md)</span><span class="sxs-lookup"><span data-stu-id="7edc5-108">For more details on retention, see [Azure Active Directory report retention policies](active-directory-reporting-retention.md)</span></span>

--- 

<span data-ttu-id="7edc5-109">**P: Quanto tempo leva até que eu possa ver os dados de atividade depois que concluir minha tarefa?**</span><span class="sxs-lookup"><span data-stu-id="7edc5-109">**Q: How long does it take until I can see the Activity data after I have completed my task?**</span></span>

<span data-ttu-id="7edc5-110">**R:** Logs de atividade de auditoria têm uma latência variando de 15 minutos a uma hora.</span><span class="sxs-lookup"><span data-stu-id="7edc5-110">**A:** Audit activity logs have a latency ranging from 15 mins to an hour.</span></span> <span data-ttu-id="7edc5-111">Logs de atividade de entrada têm uma latência variando de 15 minutos para a maioria dos registros até 2 horas para alguns registros.</span><span class="sxs-lookup"><span data-stu-id="7edc5-111">Sign-in activity logs have a latency ranging from 15 mins for most records and up to 2 hours for a few records.</span></span>

---

<span data-ttu-id="7edc5-112">**P: É necessário ser um administrador global para ver a atividade de logs no Portal do Azure ou para obter dados por meio da API?**</span><span class="sxs-lookup"><span data-stu-id="7edc5-112">**Q: Do I need to be a global admin to see the activity logs in the Azure Portal or to get data through the API?**</span></span>

<span data-ttu-id="7edc5-113">**R:** Não.</span><span class="sxs-lookup"><span data-stu-id="7edc5-113">**A:** No.</span></span> <span data-ttu-id="7edc5-114">Você pode ser um **Leitor de segurança**, um **Administrador de segurança** ou um **Administrador Global** para ver dados de relatório no Portal do Azure ou acessando-os por meio da API.</span><span class="sxs-lookup"><span data-stu-id="7edc5-114">You can either be a **Security Reader**, a **Security Admin** or a **Global Admin** to see reporting data in Azure Portal or by accessing it through the API.</span></span>

---

<span data-ttu-id="7edc5-115">**P: Posso obter informações do log de atividades do Office 365 por meio do Portal do Azure?**</span><span class="sxs-lookup"><span data-stu-id="7edc5-115">**Q: Can I get Office 365 activity log information through the Azure portal?**</span></span>

<span data-ttu-id="7edc5-116">**R:** Embora os logs de atividades do Office 365 e de atividades do Azure AD compartilhem muitos dos recursos de diretório, se você quiser uma exibição completa dos logs de atividades do Office 365, vá para o Centro de administração do Office 365 para obter informações de log de atividades do Office 365.</span><span class="sxs-lookup"><span data-stu-id="7edc5-116">**A:** Even though Office 365 activity and Azure AD activity logs share a lot of the directory resources, if you want a full view of the Office 365 activity logs, you should go to the Office 365 Admin Center to get Office 365 Activity log information.</span></span>

---


<span data-ttu-id="7edc5-117">**P: Quais APIs devo usar para obter informações sobre logs de atividades do Office 365?**</span><span class="sxs-lookup"><span data-stu-id="7edc5-117">**Q: Which APIs do I use to get information about Office 365 Activity logs?**</span></span>

<span data-ttu-id="7edc5-118">**R:** Use as APIs de gerenciamento do Office 365 para acessar os [logs de atividades do Office 365 por meio de uma API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).</span><span class="sxs-lookup"><span data-stu-id="7edc5-118">**A:** Use the Office 365 Management APIs to access the [Office 365 Activity logs through an API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).</span></span>

---

<span data-ttu-id="7edc5-119">**P: Quantos registros posso baixar do Portal do Azure?**</span><span class="sxs-lookup"><span data-stu-id="7edc5-119">**Q: How many records I can download from Azure portal?**</span></span>

<span data-ttu-id="7edc5-120">**R:** Você pode baixar até 120 mil registros do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7edc5-120">**A:** You can download up to 120K records from the Azure portal.</span></span> <span data-ttu-id="7edc5-121">Os registros são classificados pelos *mais recentes* e, por padrão, você obterá os 120 mil registros mais recentes.</span><span class="sxs-lookup"><span data-stu-id="7edc5-121">The records are sorted by *most recent* and by default, you get the most recent 120K records.</span></span> 

---

<span data-ttu-id="7edc5-122">**P: Quantos registros posso consultar por meio da API de atividades?**</span><span class="sxs-lookup"><span data-stu-id="7edc5-122">**Q: How many records can I query through the activities API?**</span></span>

<span data-ttu-id="7edc5-123">**R:** Você pode consultar até 1 milhão de registros (se você não usar o operador top, que classifica o registro pelo mais recente).</span><span class="sxs-lookup"><span data-stu-id="7edc5-123">**A:** You can query up to 1 million records (if you don’t use the top operator, which sorts the record by most recent).</span></span> <span data-ttu-id="7edc5-124">Se usar o operador "top", você poderá consultar até 500 mil registros.</span><span class="sxs-lookup"><span data-stu-id="7edc5-124">If you do use the “top” operator, you can query up to 500K records.</span></span> <span data-ttu-id="7edc5-125">Você pode encontrar consultas de exemplo sobre como usar a API [aqui](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="7edc5-125">You can find sample queries on how to use the API here [here](active-directory-reporting-api-getting-started.md).</span></span>

---

<span data-ttu-id="7edc5-126">**P: Como obtenho uma licença premium?**</span><span class="sxs-lookup"><span data-stu-id="7edc5-126">**Q: How do I get a premium license?**</span></span>

<span data-ttu-id="7edc5-127">**A:** Consulte [Introdução ao Azure Active Directory Premium](active-directory-get-started-premium.md) para obter uma resposta para essa pergunta.</span><span class="sxs-lookup"><span data-stu-id="7edc5-127">**A:** See [Getting started with Azure Active Directory Premium](active-directory-get-started-premium.md) for an answer to this question.</span></span>

---

<span data-ttu-id="7edc5-128">**P: Em quanto tempo deverei ver dados de atividades depois de obter uma licença premium?**</span><span class="sxs-lookup"><span data-stu-id="7edc5-128">**Q: How soon should I see activities data after getting a premium license?**</span></span>

<span data-ttu-id="7edc5-129">**R:** Se você já tiver dados de atividades como uma licença gratuita, você poderá ver os mesmos dados.</span><span class="sxs-lookup"><span data-stu-id="7edc5-129">**A:** If you already have activities data as a free license, then you can see the same data.</span></span> <span data-ttu-id="7edc5-130">Se você não tiver nenhum dado, isso levará um ou dois dias.</span><span class="sxs-lookup"><span data-stu-id="7edc5-130">If you don’t have any data, then it will take one or two days.</span></span>

---

<span data-ttu-id="7edc5-131">**P: Eu vejo dados do último mês depois de obter uma licença premium do Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="7edc5-131">**Q: Do I see last month's data after getting an Azure AD premium license?**</span></span>

<span data-ttu-id="7edc5-132">**R:** Se você mudou recentemente para uma versão Premium (incluindo uma versão de avaliação), você poderá inicialmente ver dados de até 7 dias.</span><span class="sxs-lookup"><span data-stu-id="7edc5-132">**A:** If you have recently switched to a Premium version (including a trial version), you can see data up to 7 days initially.</span></span> <span data-ttu-id="7edc5-133">Quando os dados acumularem, você verá dados de até 30 dias.</span><span class="sxs-lookup"><span data-stu-id="7edc5-133">When data accumulates, you will see up to 30 days.</span></span>

---

<span data-ttu-id="7edc5-134">**P: Há um evento de risco no Identity Protection, mas não estou vendo a entrada correspondente em todas as entradas. Isso é esperado?**</span><span class="sxs-lookup"><span data-stu-id="7edc5-134">**Q: There is a risk event in Identity Protection but I’m not seeing corresponding sign-in in the all sign-ins. Is this expected?**</span></span>

<span data-ttu-id="7edc5-135">**R:** Sim, o Identity Protection avalia o risco de todos os fluxos de autenticação, sejam eles interativos ou não.</span><span class="sxs-lookup"><span data-stu-id="7edc5-135">**A:** Yes, Identity Protection evaluates risk for all authentication flows whether if be interactive or non-interactive.</span></span> <span data-ttu-id="7edc5-136">No entanto, o relatório de todas as entradas mostra apenas as entradas interativas.</span><span class="sxs-lookup"><span data-stu-id="7edc5-136">However, all sign-ins only report shows only the interactive sign-ins.</span></span>

---

<span data-ttu-id="7edc5-137">**P: Como posso baixar o relatório "Usuários sinalizados para risco" no portal do Azure?**</span><span class="sxs-lookup"><span data-stu-id="7edc5-137">**Q: How can I download the “Users flagged for risk” report in Azure portal?**</span></span>

<span data-ttu-id="7edc5-138">**R:**: A opção de baixar o relatório *Usuários sinalizados para risco* será adicionada em breve.</span><span class="sxs-lookup"><span data-stu-id="7edc5-138">**A:** The option to download *Users flagged for risk* report will be added soon.</span></span>

---

<span data-ttu-id="7edc5-139">**P: Como posso saber o motivo pelo qual uma entrada ou um usuário foi sinalizado como arriscado no Portal do Azure?**</span><span class="sxs-lookup"><span data-stu-id="7edc5-139">**Q: How do I know why a sign-in or a user was flagged risky in the Azure portal?**</span></span>

<span data-ttu-id="7edc5-140">**R:** Clientes do Premium Edition podem saber mais sobre os eventos de risco subjacentes clicando no usuário em "Usuários sinalizados para risco" ou clicando nas "Entradas arriscadas".</span><span class="sxs-lookup"><span data-stu-id="7edc5-140">**A:** Premium edition customers can learn more about the underlying risk events by clicking on the user in “Users flagged for risk” or by clicking on the “Risky sign-ins”.</span></span> <span data-ttu-id="7edc5-141">Clientes das edições Gratuita e Basic podem ver as entradas e os usuários em risco sem as informações de evento de risco subjacente.</span><span class="sxs-lookup"><span data-stu-id="7edc5-141">Free and Basic edition customers get to see the at-risk users and sign-ins without the underlying risk event information.</span></span>

---

<span data-ttu-id="7edc5-142">**P: Como os endereços IP são calculados no relatório de entradas e entradas arriscadas?**</span><span class="sxs-lookup"><span data-stu-id="7edc5-142">**Q: How are IP addresses calculated in the sign-ins and risky sign-ins report??**</span></span>

<span data-ttu-id="7edc5-143">**R:** Os endereços IP são emitidos de uma forma que não há nenhuma conexão definitiva entre um endereço IP e em que o computador com esse endereço está localizado fisicamente.</span><span class="sxs-lookup"><span data-stu-id="7edc5-143">**A:** IP addresses are issued in such a way that there is no definitive connection between an IP address and where the computer with that address is physically located.</span></span> <span data-ttu-id="7edc5-144">Isso é complicado por fatores como provedores móveis e VPNs que emitem endereços IP de pools centrais, frequentemente muito distantes do local no qual o dispositivo do cliente de fato é usado.</span><span class="sxs-lookup"><span data-stu-id="7edc5-144">This is complicated by factors such as mobile providers and VPNs issuing IP addresses from central pools often very far from where the client device is actually used.</span></span> <span data-ttu-id="7edc5-145">Devido a esses fatores, a conversão de endereços IP em um local físico é um esforço baseado em rastreamentos, dados de registro, pesquisas inversas e outras informações.</span><span class="sxs-lookup"><span data-stu-id="7edc5-145">Given the above, converting IP address to a physical location is a best effort based on traces, registry data, reverse look ups and other information.</span></span> 

---
