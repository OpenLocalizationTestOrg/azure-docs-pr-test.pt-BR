---
title: "Active Directory perguntas Frequentes dos relatórios de aaaAzure | Microsoft Docs"
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
ms.openlocfilehash: be65a05574ea3b5b190cd02a96b211c571ba70bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-faq"></a><span data-ttu-id="0f18c-103">Perguntas frequentes sobre relatórios do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0f18c-103">Azure Active Directory reporting FAQ</span></span>

<span data-ttu-id="0f18c-104">Este artigo inclui respostas toofrequently perguntas frequentes (FAQs) sobre os relatórios do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="0f18c-104">This article includes answers toofrequently asked questions (FAQs) about Azure Active Directory reporting.</span></span>  
<span data-ttu-id="0f18c-105">Para obter mais detalhes, veja [Relatórios do Azure Active Directory](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0f18c-105">For more details, see [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span> 

<span data-ttu-id="0f18c-106">**P: o que é a retenção de dados Olá para logs de atividade (e entradas de auditoria) Olá portal do Azure?**</span><span class="sxs-lookup"><span data-stu-id="0f18c-106">**Q: What is hello data retention for activity logs (Audit and Sign-ins) in hello Azure portal?**</span></span> 

<span data-ttu-id="0f18c-107">**R:** fornecemos sete dias de dados para nossos clientes livres e alternando tooan 1 do Azure AD Premium ou licença Premium 2, você pode acessar os dados de backup too30 dias.</span><span class="sxs-lookup"><span data-stu-id="0f18c-107">**A:** We provide 7 days of data for our free customers and by switching tooan Azure AD Premium 1 or Premium 2 license, you can access data for up too30 days.</span></span> <span data-ttu-id="0f18c-108">Para obter mais detalhes sobre a retenção, consulte [Políticas de retenção de relatório do Azure Active Directory](active-directory-reporting-retention.md)</span><span class="sxs-lookup"><span data-stu-id="0f18c-108">For more details on retention, see [Azure Active Directory report retention policies](active-directory-reporting-retention.md)</span></span>

--- 

<span data-ttu-id="0f18c-109">**P: quanto tempo leva até podem ver dados de atividade de saudação depois que concluir minha tarefa?**</span><span class="sxs-lookup"><span data-stu-id="0f18c-109">**Q: How long does it take until I can see hello Activity data after I have completed my task?**</span></span>

<span data-ttu-id="0f18c-110">**R:** logs de atividade de auditoria tem uma latência de 15 minutos tooan horas.</span><span class="sxs-lookup"><span data-stu-id="0f18c-110">**A:** Audit activity logs have a latency ranging from 15 mins tooan hour.</span></span> <span data-ttu-id="0f18c-111">Logs de atividade de entrada tem uma latência de 15 minutos para a maioria dos registros e backup too2 horas para alguns registros.</span><span class="sxs-lookup"><span data-stu-id="0f18c-111">Sign-in activity logs have a latency ranging from 15 mins for most records and up too2 hours for a few records.</span></span>

---

<span data-ttu-id="0f18c-112">**P: é necessário toobe que uma atividade de saudação do administrador global toosee fizer logon Olá Portal do Azure ou tooget dados por meio de saudação API?**</span><span class="sxs-lookup"><span data-stu-id="0f18c-112">**Q: Do I need toobe a global admin toosee hello activity logs in hello Azure Portal or tooget data through hello API?**</span></span>

<span data-ttu-id="0f18c-113">**R:** Não.</span><span class="sxs-lookup"><span data-stu-id="0f18c-113">**A:** No.</span></span> <span data-ttu-id="0f18c-114">Você pode ser um **segurança leitor**, um **Admin de segurança** ou um **Administrador Global** toosee dados no Portal do Azure ou acessá-lo por meio da API de saudação do relatório.</span><span class="sxs-lookup"><span data-stu-id="0f18c-114">You can either be a **Security Reader**, a **Security Admin** or a **Global Admin** toosee reporting data in Azure Portal or by accessing it through hello API.</span></span>

---

<span data-ttu-id="0f18c-115">**P: posso obter informações de log de atividade do Office 365 por meio de saudação portal do Azure?**</span><span class="sxs-lookup"><span data-stu-id="0f18c-115">**Q: Can I get Office 365 activity log information through hello Azure portal?**</span></span>

<span data-ttu-id="0f18c-116">**R:** apesar de atividade do Office 365 e o compartilhamento de logs de atividade do AD do Azure muitos recursos de diretório hello, se você quiser que uma exibição completa de Olá logs de atividade do Office 365, você deve se as informações do log de atividade do Office 365 toohello Centro de administração do Office 365 tooget.</span><span class="sxs-lookup"><span data-stu-id="0f18c-116">**A:** Even though Office 365 activity and Azure AD activity logs share a lot of hello directory resources, if you want a full view of hello Office 365 activity logs, you should go toohello Office 365 Admin Center tooget Office 365 Activity log information.</span></span>

---


<span data-ttu-id="0f18c-117">**P: qual pelas APIs uso tooget informações sobre os logs de atividade do Office 365?**</span><span class="sxs-lookup"><span data-stu-id="0f18c-117">**Q: Which APIs do I use tooget information about Office 365 Activity logs?**</span></span>

<span data-ttu-id="0f18c-118">**R:** Use Olá APIs de gerenciamento do Office 365 tooaccess Olá [logs de atividade do Office 365 por meio de uma API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).</span><span class="sxs-lookup"><span data-stu-id="0f18c-118">**A:** Use hello Office 365 Management APIs tooaccess hello [Office 365 Activity logs through an API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).</span></span>

---

<span data-ttu-id="0f18c-119">**P: Quantos registros posso baixar do Portal do Azure?**</span><span class="sxs-lookup"><span data-stu-id="0f18c-119">**Q: How many records I can download from Azure portal?**</span></span>

<span data-ttu-id="0f18c-120">**R:** você pode baixar os registros de too120K de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0f18c-120">**A:** You can download up too120K records from hello Azure portal.</span></span> <span data-ttu-id="0f18c-121">Olá registros são classificados por *mais recente* e por padrão, você obter registros Olá K de 120 mais recente.</span><span class="sxs-lookup"><span data-stu-id="0f18c-121">hello records are sorted by *most recent* and by default, you get hello most recent 120K records.</span></span> 

---

<span data-ttu-id="0f18c-122">**P: o número de registros pode consultar por meio de atividades de saudação API?**</span><span class="sxs-lookup"><span data-stu-id="0f18c-122">**Q: How many records can I query through hello activities API?**</span></span>

<span data-ttu-id="0f18c-123">**R:** consultar too1 milhões de registros (se você não usar o operador top hello, que classifica registro Olá por mais recente).</span><span class="sxs-lookup"><span data-stu-id="0f18c-123">**A:** You can query up too1 million records (if you don’t use hello top operator, which sorts hello record by most recent).</span></span> <span data-ttu-id="0f18c-124">Se você usar o operador de "top" Olá, você pode consultar os registros too500K.</span><span class="sxs-lookup"><span data-stu-id="0f18c-124">If you do use hello “top” operator, you can query up too500K records.</span></span> <span data-ttu-id="0f18c-125">Você pode encontrar exemplos de consultas em como toouse Olá API aqui [aqui](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="0f18c-125">You can find sample queries on how toouse hello API here [here](active-directory-reporting-api-getting-started.md).</span></span>

---

<span data-ttu-id="0f18c-126">**P: Como obtenho uma licença premium?**</span><span class="sxs-lookup"><span data-stu-id="0f18c-126">**Q: How do I get a premium license?**</span></span>

<span data-ttu-id="0f18c-127">**R:** consulte [guia de Introdução ao Azure Active Directory Premium](active-directory-get-started-premium.md) para uma pergunta de toothis de resposta.</span><span class="sxs-lookup"><span data-stu-id="0f18c-127">**A:** See [Getting started with Azure Active Directory Premium](active-directory-get-started-premium.md) for an answer toothis question.</span></span>

---

<span data-ttu-id="0f18c-128">**P: Em quanto tempo deverei ver dados de atividades depois de obter uma licença premium?**</span><span class="sxs-lookup"><span data-stu-id="0f18c-128">**Q: How soon should I see activities data after getting a premium license?**</span></span>

<span data-ttu-id="0f18c-129">**R:** se você já tiver dados de atividades como uma licença gratuita, você pode ver Olá os mesmos dados.</span><span class="sxs-lookup"><span data-stu-id="0f18c-129">**A:** If you already have activities data as a free license, then you can see hello same data.</span></span> <span data-ttu-id="0f18c-130">Se você não tiver nenhum dado, isso levará um ou dois dias.</span><span class="sxs-lookup"><span data-stu-id="0f18c-130">If you don’t have any data, then it will take one or two days.</span></span>

---

<span data-ttu-id="0f18c-131">**P: Eu vejo dados do último mês depois de obter uma licença premium do Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="0f18c-131">**Q: Do I see last month's data after getting an Azure AD premium license?**</span></span>

<span data-ttu-id="0f18c-132">**R:** se você recentemente alternou versão Premium de tooa (incluindo uma versão de avaliação), você pode ver os dados too7 dias inicialmente.</span><span class="sxs-lookup"><span data-stu-id="0f18c-132">**A:** If you have recently switched tooa Premium version (including a trial version), you can see data up too7 days initially.</span></span> <span data-ttu-id="0f18c-133">Quando se acumulando, você verá too30 dias.</span><span class="sxs-lookup"><span data-stu-id="0f18c-133">When data accumulates, you will see up too30 days.</span></span>

---

<span data-ttu-id="0f18c-134">**P: há um evento de risco na proteção de identidade, mas não vejo entrada correspondente no hello todas as entradas. Isso é esperado?**</span><span class="sxs-lookup"><span data-stu-id="0f18c-134">**Q: There is a risk event in Identity Protection but I’m not seeing corresponding sign-in in hello all sign-ins. Is this expected?**</span></span>

<span data-ttu-id="0f18c-135">**R:** Sim, o Identity Protection avalia o risco de todos os fluxos de autenticação, sejam eles interativos ou não.</span><span class="sxs-lookup"><span data-stu-id="0f18c-135">**A:** Yes, Identity Protection evaluates risk for all authentication flows whether if be interactive or non-interactive.</span></span> <span data-ttu-id="0f18c-136">No entanto, todos os relatórios somente de logons mostra somente Olá logons interativos.</span><span class="sxs-lookup"><span data-stu-id="0f18c-136">However, all sign-ins only report shows only hello interactive sign-ins.</span></span>

---

<span data-ttu-id="0f18c-137">**P: como baixar o relatório de "Usuários sinalizados riscos" hello no portal do Azure?**</span><span class="sxs-lookup"><span data-stu-id="0f18c-137">**Q: How can I download hello “Users flagged for risk” report in Azure portal?**</span></span>

<span data-ttu-id="0f18c-138">**R:** toodownload de opção Olá *usuários sinalizados riscos* relatório será adicionado em breve.</span><span class="sxs-lookup"><span data-stu-id="0f18c-138">**A:** hello option toodownload *Users flagged for risk* report will be added soon.</span></span>

---

<span data-ttu-id="0f18c-139">**P: como saber por que um logon ou um usuário foi sinalizado arriscados em Olá portal do Azure?**</span><span class="sxs-lookup"><span data-stu-id="0f18c-139">**Q: How do I know why a sign-in or a user was flagged risky in hello Azure portal?**</span></span>

<span data-ttu-id="0f18c-140">**R:** clientes de edição Premium podem aprender mais sobre Olá subjacente eventos de risco clicando no usuário hello "Usuários sinalizados riscos" ou clicando no hello "Arriscadas entradas".</span><span class="sxs-lookup"><span data-stu-id="0f18c-140">**A:** Premium edition customers can learn more about hello underlying risk events by clicking on hello user in “Users flagged for risk” or by clicking on hello “Risky sign-ins”.</span></span> <span data-ttu-id="0f18c-141">Os clientes da edição gratuita e Basic obtém usuários em risco de saudação toosee e entradas sem Olá subjacente informações de evento de risco.</span><span class="sxs-lookup"><span data-stu-id="0f18c-141">Free and Basic edition customers get toosee hello at-risk users and sign-ins without hello underlying risk event information.</span></span>

---

<span data-ttu-id="0f18c-142">**P: como os endereços IP são calculados em Olá entradas e o relatório de entradas arriscado?**</span><span class="sxs-lookup"><span data-stu-id="0f18c-142">**Q: How are IP addresses calculated in hello sign-ins and risky sign-ins report??**</span></span>

<span data-ttu-id="0f18c-143">**R:** endereços IP são emitidos de forma que não há nenhuma conexão definitiva entre um endereço IP e em que o computador Olá com o endereço estiver localizado fisicamente.</span><span class="sxs-lookup"><span data-stu-id="0f18c-143">**A:** IP addresses are issued in such a way that there is no definitive connection between an IP address and where hello computer with that address is physically located.</span></span> <span data-ttu-id="0f18c-144">Isso é complicado devido a fatores como provedores móveis e VPNs emitir endereços IP de pools centrais geralmente muito distantes de onde o dispositivo de cliente de saudação é realmente usado.</span><span class="sxs-lookup"><span data-stu-id="0f18c-144">This is complicated by factors such as mobile providers and VPNs issuing IP addresses from central pools often very far from where hello client device is actually used.</span></span> <span data-ttu-id="0f18c-145">Considerando Olá acima, converter o local físico de tooa de endereço IP é um melhor esforço com base em rastreamentos, dados de registro, pesquisa inversa no-break e outras informações.</span><span class="sxs-lookup"><span data-stu-id="0f18c-145">Given hello above, converting IP address tooa physical location is a best effort based on traces, registry data, reverse look ups and other information.</span></span> 

---
