---
title: Problema ao adicionar um aplicativo inexistente na galeria | Microsoft Docs
description: Compreenda os problemas comuns que as pessoas enfrentam ao adicionar aplicativos personalizados inexistentes na galeria
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: bb3fc7877f4e7cafc3904fc67abd87b897874d8a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="problem-adding-a-non-gallery-application"></a><span data-ttu-id="b22c2-103">Problema ao adicionar um aplicativo inexistente na galeria</span><span class="sxs-lookup"><span data-stu-id="b22c2-103">Problem adding a non-gallery application</span></span>

<span data-ttu-id="b22c2-104">Este artigo ajuda você a compreender os problemas comuns que as pessoas enfrentam ao adicionar **aplicativos personalizados inexistentes na galeria** e o que você pode fazer para resolvê-los.</span><span class="sxs-lookup"><span data-stu-id="b22c2-104">This article help you to understand the common problems people face when adding **custom non-gallery applications** and what you can do to resolve them.</span></span> 

## <a name="i-clicked-the-add-button-and-my-application-took-a-long-time-to-appear"></a><span data-ttu-id="b22c2-105">Cliquei no botão "adicionar" e meu aplicativo demorou muito para aparecer</span><span class="sxs-lookup"><span data-stu-id="b22c2-105">I clicked the “add” button and my application took a long time to appear</span></span>

<span data-ttu-id="b22c2-106">Em algumas circunstâncias, pode demorar de 1 ou 2 minutos (às vezes mais) para um aplicativo aparecer após ser adicionado ao diretório.</span><span class="sxs-lookup"><span data-stu-id="b22c2-106">Under some circumstances, it can take 1-2 minutes (and sometimes longer) for an application to appear after adding it to your directory.</span></span> <span data-ttu-id="b22c2-107">Embora esse não seja o desempenho normal esperado, você pode ver que a adição do aplicativo está em andamento clicando no ícone **Notificações** (o sino) no canto superior direito do [Portal do Azure](https://portal.azure.com/) e procurando uma notificação **Em Andamento** ou **Concluído** rotulada **Criar aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="b22c2-107">While this is not the normal expected performance, you can see the application addition is in progress by clicking on the **Notifications** icon (the bell) in the upper right of the [Azure Portal](https://portal.azure.com/) and looking for an **In Progress** or **Completed** notification labeled **Create application**.</span></span>

<span data-ttu-id="b22c2-108">Se seu aplicativo nunca for adicionado, ou se você encontrar um erro ao clicar no botão **Adicionar**, você verá uma **Notificação** em um estado de **Erro**.</span><span class="sxs-lookup"><span data-stu-id="b22c2-108">If your application is never added, or you encounter an error when clicking the **Add** button, you’ll see a **Notification** in an **Error** state.</span></span> <span data-ttu-id="b22c2-109">Se quiser mais detalhes sobre o erro para saber mais ou para compartilhar com um engenheiro de suporte, você poderá ver mais informações sobre o erro seguindo as etapas na seção [Como ver os detalhes de uma notificação do portal](#how-to-see-the-details-of-a-portal-notification).</span><span class="sxs-lookup"><span data-stu-id="b22c2-109">If you want more details about the error to learn more to or share with a support engingeer, you can see more information about the error by following the steps in the [How to see the details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.</span></span>

## <a name="i-clicked-the-add-button-and-my-application-didnt-appear"></a><span data-ttu-id="b22c2-110">Cliquei no botão "adicionar" e meu aplicativo não apareceu</span><span class="sxs-lookup"><span data-stu-id="b22c2-110">I clicked the “add” button and my application didn’t appear</span></span>

<span data-ttu-id="b22c2-111">Às vezes, devido a problemas temporários, problemas de rede ou um bug, a adição de um aplicativo falha.</span><span class="sxs-lookup"><span data-stu-id="b22c2-111">Sometimes, due to transient issues, networking problems, or a bug, adding an application fail.</span></span> <span data-ttu-id="b22c2-112">Você sabe que isso aconteceu quando clica no ícone **Notificações** (o sino) na parte superior direita do Portal do Azure e vê um ícone vermelho (!) ao lado de sua notificação **Criar aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="b22c2-112">You can tell this happens when you click the **Notifications** icon (the bell) in the upper right of the Azure Portal and you see a red (!) icon next to your **Create application** notification.</span></span> <span data-ttu-id="b22c2-113">Isso indica que ocorreu um erro ao criar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b22c2-113">This indicates there was an error when creating the application.</span></span>

<span data-ttu-id="b22c2-114">Se encontrar um erro ao clicar no botão **Adicionar**, você verá uma **Notificação** em um estado **Erro**.</span><span class="sxs-lookup"><span data-stu-id="b22c2-114">If you encounter an error when clicking the **Add** button, you’ll see a **Notification** in an **Error** state.</span></span> <span data-ttu-id="b22c2-115">Se quiser mais detalhes sobre o erro para saber mais ou para compartilhar com um engenheiro de suporte, você poderá ver mais informações sobre o erro seguindo as etapas na seção [Como ver os detalhes de uma notificação do portal](#how-to-see-the-details-of-a-portal-notification).</span><span class="sxs-lookup"><span data-stu-id="b22c2-115">If you want more details about the error to learn more to or share with a support engingeer, you can see more information about the error by following the steps in the [How to see the details of a portal notification](#how-to-see-the-details-of-a-portal-notification) section.</span></span>

## <a name="i-dont-know-how-to-set-up-my-application-once-ive-added-it"></a><span data-ttu-id="b22c2-116">Não sei configurar meu aplicativo após tê-lo adicionado</span><span class="sxs-lookup"><span data-stu-id="b22c2-116">I don’t know how to set up my application once I’ve added it</span></span>

<span data-ttu-id="b22c2-117">Se você precisar de ajuda para aprender mais sobre aplicativos personalizados, a [Biblioteca de documentos de aplicativo do Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index) ajuda a saber mais sobre o logon único com o Azure AD e como ele funciona.</span><span class="sxs-lookup"><span data-stu-id="b22c2-117">If you need help learning about custom applications, the [Azure AD Applications Document Library](https://docs.microsoft.com/azure/active-directory/active-directory-apps-index) help you to learn more about single sign-on with Azure AD and how it works.</span></span>

## <a name="how-to-see-the-details-of-a-portal-notification"></a><span data-ttu-id="b22c2-118">Como ver os detalhes de uma notificação do portal</span><span class="sxs-lookup"><span data-stu-id="b22c2-118">How to see the details of a portal notification</span></span>

<span data-ttu-id="b22c2-119">Veja os detalhes de qualquer notificação do portal executando as etapas abaixo:</span><span class="sxs-lookup"><span data-stu-id="b22c2-119">You can see the details of any portal notification by following the steps below:</span></span>

1.  <span data-ttu-id="b22c2-120">Clique no ícone **Notificações** (o sino) na parte superior direita do Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b22c2-120">click the **Notifications** icon (the bell) in the upper right of the Azure Portal</span></span>

2.  <span data-ttu-id="b22c2-121">Selecione qualquer notificação com estado de **Erro** (aquelas com um (!) vermelho ao lado).</span><span class="sxs-lookup"><span data-stu-id="b22c2-121">Select any notification in an **Error** state (those with a red (!) next to them).</span></span>

   >[!NOTE]
   ><span data-ttu-id="b22c2-122">Não é possível clicar em notificações com estado de **Êxito** ou **Em Andamento**.</span><span class="sxs-lookup"><span data-stu-id="b22c2-122">You cannot click notifications in a **Successful** or **In Progress** state.</span></span>
   >
   >

3.  <span data-ttu-id="b22c2-123">Isso abre a folha **Detalhes da Notificação**.</span><span class="sxs-lookup"><span data-stu-id="b22c2-123">This open the **Notification Details** blade.</span></span>

4.  <span data-ttu-id="b22c2-124">Use essas informações para saber mais detalhes sobre o problema.</span><span class="sxs-lookup"><span data-stu-id="b22c2-124">Use this information yourself to understand more details about the problem.</span></span>

5.  <span data-ttu-id="b22c2-125">Se ainda precisar de ajuda, você também poderá compartilhar essas informações com um engenheiro de suporte ou com o grupo de produtos para obter ajuda com o problema.</span><span class="sxs-lookup"><span data-stu-id="b22c2-125">If you still need help, you can also share this information with a support engineer or the product group to get help with your problem.</span></span>

6.  <span data-ttu-id="b22c2-126">Clique no **ícone de cópia** à direita da caixa de texto **Copiar erro** para copiar todos os detalhes da notificação para compartilhar com um engenheiro de suporte ou de grupo de produtos.</span><span class="sxs-lookup"><span data-stu-id="b22c2-126">Click the **copy icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer.</span></span>

## <a name="how-to-get-help-by-sending-notification-details-to-a-support-engineer"></a><span data-ttu-id="b22c2-127">Como obter ajuda enviando detalhes da notificação a um engenheiro de suporte</span><span class="sxs-lookup"><span data-stu-id="b22c2-127">How to get help by sending notification details to a support engineer</span></span>

<span data-ttu-id="b22c2-128">É muito importante que você compartilhe **todos os detalhes abaixo** com um engenheiro de suporte caso precise de ajuda, para que ele possa ajudar rapidamente.</span><span class="sxs-lookup"><span data-stu-id="b22c2-128">It is very important that you share **all the details listed below** with a support engineer if you need help, so that they can help you quickly.</span></span> <span data-ttu-id="b22c2-129">Faça isso facilmente **tirando uma captura de tela** ou clicando no **ícone Copiar erro**, localizado à direita da caixa de texto **Copiar erro**.</span><span class="sxs-lookup"><span data-stu-id="b22c2-129">You can do this easily by **taking a screenshot,** or by clicking the **Copy error icon**, found to the right of the **Copy error** textbox.</span></span>

## <a name="notification-details-explained"></a><span data-ttu-id="b22c2-130">Detalhes da notificação explicados</span><span class="sxs-lookup"><span data-stu-id="b22c2-130">Notification Details Explained</span></span>

<span data-ttu-id="b22c2-131">Abaixo, explicamos mais sobre o significado de cada item de notificação e fornecemos exemplos de cada um deles.</span><span class="sxs-lookup"><span data-stu-id="b22c2-131">The below explains more what each of the notification items means, and gives examples of each of them.</span></span>

### <a name="essential-notification-items"></a><span data-ttu-id="b22c2-132">Itens de notificação essenciais</span><span class="sxs-lookup"><span data-stu-id="b22c2-132">Essential Notification Items</span></span>

-   <span data-ttu-id="b22c2-133">**Título** – o título descritivo da notificação</span><span class="sxs-lookup"><span data-stu-id="b22c2-133">**Title** – the descriptive title of the notification</span></span>
   *  <span data-ttu-id="b22c2-134">Exemplo – **Configurações do proxy do aplicativo**</span><span class="sxs-lookup"><span data-stu-id="b22c2-134">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="b22c2-135">**Descrição** – a descrição do que ocorreu como resultado da operação</span><span class="sxs-lookup"><span data-stu-id="b22c2-135">**Description** – the description of what occurred as a result of the operation</span></span>

   *  <span data-ttu-id="b22c2-136">Exemplo – **A URL interna inserida já está sendo usada por outro aplicativo**</span><span class="sxs-lookup"><span data-stu-id="b22c2-136">Example – **Internal url entered is already being used by another application**</span></span>

-   <span data-ttu-id="b22c2-137">**ID da Notificação** – a ID exclusiva da notificação</span><span class="sxs-lookup"><span data-stu-id="b22c2-137">**Notification Id** – the unique id of the notification</span></span>

   *  <span data-ttu-id="b22c2-138">Exemplo – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span><span class="sxs-lookup"><span data-stu-id="b22c2-138">Example – **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**</span></span>

-   <span data-ttu-id="b22c2-139">**ID de Solicitação do Cliente** – a ID de solicitação específica feita por seu navegador</span><span class="sxs-lookup"><span data-stu-id="b22c2-139">**Client Request Id** – the specific request id made by your browser</span></span>

   *  <span data-ttu-id="b22c2-140">Exemplo – **302fd775-3329-4670-a9f3-bea37004f0bc**</span><span class="sxs-lookup"><span data-stu-id="b22c2-140">Example – **302fd775-3329-4670-a9f3-bea37004f0bc**</span></span>

-   <span data-ttu-id="b22c2-141">**Carimbo de Data/Hora UTC** – o carimbo de data/hora durante o qual a notificação ocorreu, em UTC</span><span class="sxs-lookup"><span data-stu-id="b22c2-141">**Time Stamp UTC** – the timestamp during which the notification occurred, in UTC</span></span>

   *  <span data-ttu-id="b22c2-142">Exemplo – **2017-03-23T19:50:43.7583681Z**</span><span class="sxs-lookup"><span data-stu-id="b22c2-142">Example – **2017-03-23T19:50:43.7583681Z**</span></span>

-   <span data-ttu-id="b22c2-143">**ID de Transação Interna** – a ID interna que podemos usar para procurar o erro em nossos sistemas</span><span class="sxs-lookup"><span data-stu-id="b22c2-143">**Internal Transaction Id** – the internal ID we can use to look the error up in our systems</span></span>

   *  <span data-ttu-id="b22c2-144">Exemplo – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span><span class="sxs-lookup"><span data-stu-id="b22c2-144">Example – **71a2f329-ca29-402f-aa72-bc00a7aca603**</span></span>

-   <span data-ttu-id="b22c2-145">**UPN** – o usuário que realizou a operação</span><span class="sxs-lookup"><span data-stu-id="b22c2-145">**UPN** – the user who performed the operation</span></span>

   *  <span data-ttu-id="b22c2-146">Exemplo – **tperkins@f128.info**</span><span class="sxs-lookup"><span data-stu-id="b22c2-146">Example – **tperkins@f128.info**</span></span>

-   <span data-ttu-id="b22c2-147">**Id do Locatário** – a ID exclusiva do locatário do qual o usuário que realizou a operação era membro</span><span class="sxs-lookup"><span data-stu-id="b22c2-147">**Tenant Id** – the unique ID of the tenant that the user who performed the operation was a member of</span></span>

   *  <span data-ttu-id="b22c2-148">Exemplo – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span><span class="sxs-lookup"><span data-stu-id="b22c2-148">Example – **7918d4b5-0442-4a97-be2d-36f9f9962ece**</span></span>

-   <span data-ttu-id="b22c2-149">**Id de objeto de usuário** – a ID exclusiva do usuário que realizou a operação</span><span class="sxs-lookup"><span data-stu-id="b22c2-149">**User object Id** – the unique ID of the user who performed the operation</span></span>

 *  <span data-ttu-id="b22c2-150">Exemplo – **17f84be4-51f8-483a-b533-383791227a99**</span><span class="sxs-lookup"><span data-stu-id="b22c2-150">Example – **17f84be4-51f8-483a-b533-383791227a99**</span></span>

### <a name="detailed-notification-items"></a><span data-ttu-id="b22c2-151">Itens de notificação detalhados</span><span class="sxs-lookup"><span data-stu-id="b22c2-151">Detailed Notification Items</span></span>

-   <span data-ttu-id="b22c2-152">**Nome de Exibição** – **(pode estar vazio)** um nome de exibição mais detalhado do erro</span><span class="sxs-lookup"><span data-stu-id="b22c2-152">**Display Name** – **(can be empty)** a more detailed display name for the error</span></span>

  *  <span data-ttu-id="b22c2-153">Exemplo – **Configurações do proxy do aplicativo**</span><span class="sxs-lookup"><span data-stu-id="b22c2-153">Example – **Application proxy settings**</span></span>

-   <span data-ttu-id="b22c2-154">**Status** – o status específico da notificação</span><span class="sxs-lookup"><span data-stu-id="b22c2-154">**Status** – the specific status of the notification</span></span>

   *  <span data-ttu-id="b22c2-155">Exemplo – **Falha**</span><span class="sxs-lookup"><span data-stu-id="b22c2-155">Example – **Failed**</span></span>

-   <span data-ttu-id="b22c2-156">**Id do Objeto** – **(pode estar vazio)** a ID do objeto em que a operação foi executada</span><span class="sxs-lookup"><span data-stu-id="b22c2-156">**Object Id** – **(can be empty)** the object ID against which the operation was performed</span></span>

   *  <span data-ttu-id="b22c2-157">Exemplo – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span><span class="sxs-lookup"><span data-stu-id="b22c2-157">Example – **8e08161d-f2fd-40ad-a34a-a9632d6bb599**</span></span>

-   <span data-ttu-id="b22c2-158">**Detalhes** – a descrição detalhada do que ocorreu como resultado da operação</span><span class="sxs-lookup"><span data-stu-id="b22c2-158">**Details** – the detailed description of what occurred as a result of the operation</span></span>

   *  <span data-ttu-id="b22c2-159">Exemplo – **A URL interna 'http://bing.com/' é inválida, uma vez que está sendo utilizada**</span><span class="sxs-lookup"><span data-stu-id="b22c2-159">Example – **Internal url 'http://bing.com/' is invalid since it is already in use**</span></span>

-   <span data-ttu-id="b22c2-160">**Copiar erro** – clique no **ícone de cópia** à direita da caixa de texto **Copiar erro** para copiar todos os detalhes de notificação para compartilhar com um engenheiro de suporte ou de grupo de produtos</span><span class="sxs-lookup"><span data-stu-id="b22c2-160">**Copy error** – Click the **copy icon** to the right of the **Copy error** textbox to copy all the notification details to share with a support or product group engineer</span></span>

   *  <span data-ttu-id="b22c2-161">Exemplo ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span><span class="sxs-lookup"><span data-stu-id="b22c2-161">Example ```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```</span></span>

## <a name="next-steps"></a><span data-ttu-id="b22c2-162">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b22c2-162">Next steps</span></span>
[<span data-ttu-id="b22c2-163">Gerenciando aplicativos com o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b22c2-163">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)



