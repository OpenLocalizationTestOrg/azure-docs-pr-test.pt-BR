---
title: "Configurar um nome de domínio personalizado no Serviço de Aplicativo do Azure (GoDaddy)"
description: "Saiba como usar um nome de domínio do GoDaddy com Aplicativos Web do Azure"
services: app-service
documentationcenter: 
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 33233e30-5846-488f-83f3-b32e5c114564
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: 158c5dc06f83e16633d3c2fbb4eb27d3e8af030c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-custom-domain-name-in-azure-app-service-purchased-directly-from-godaddy"></a><span data-ttu-id="1b3a8-103">Configurar um nome de domínio personalizado no Serviço de Aplicativo do Azure (adquirido diretamente do GoDaddy)</span><span class="sxs-lookup"><span data-stu-id="1b3a8-103">Configure a custom domain name in Azure App Service (Purchased directly from GoDaddy)</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro.md)]

<span data-ttu-id="1b3a8-104">Se você tiver adquirido o domínio por meio de Aplicativos Web do Serviço de Aplicativo do Azure e consulte a etapa final de [Comprar domínio para aplicativos Web](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="1b3a8-104">If you have purchased domain through Azure App Service Web Apps then refer to the final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md).</span></span>

<span data-ttu-id="1b3a8-105">Este artigo fornece instruções sobre como usar um nome de domínio personalizado adquirido diretamente de [GoDaddy](https://godaddy.com) com [Aplicativos Web do Serviço de Aplicativo](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="1b3a8-105">This article provides instructions on using a custom domain name that was purchased directly from [GoDaddy](https://godaddy.com) with [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="1b3a8-106">Compreendendo os registros DNS</span><span class="sxs-lookup"><span data-stu-id="1b3a8-106">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-raw.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="1b3a8-107">Adicionar um registro DNS a seu domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="1b3a8-107">Add a DNS record for your custom domain</span></span>
<span data-ttu-id="1b3a8-108">Para associar seu domínio personalizado a um aplicativo Web no Serviço de Aplicativo, você deve adicionar uma nova entrada na tabela DNS para seu domínio personalizado usando as ferramentas fornecidas pelo GoDaddy.</span><span class="sxs-lookup"><span data-stu-id="1b3a8-108">To associate your custom domain with a web app in App Service, you must add a new entry in the DNS table for your custom domain by using tools provided by GoDaddy.</span></span> <span data-ttu-id="1b3a8-109">Use as seguintes etapas para localizar as ferramentas DNS para o GoDaddy.com</span><span class="sxs-lookup"><span data-stu-id="1b3a8-109">Use the following steps to locate the DNS tools for GoDaddy.com</span></span>

1. <span data-ttu-id="1b3a8-110">Faça logon na sua conta do GoDaddy.com e selecione **Minha Conta** e, em seguida, **Gerenciar meus domínios**.</span><span class="sxs-lookup"><span data-stu-id="1b3a8-110">Log on to your account with GoDaddy.com, and select **My Account** and then **Manage my domains**.</span></span> <span data-ttu-id="1b3a8-111">Selecione o menu suspenso para o nome de domínio que você deseja usar com seu aplicativo Web do Azure e selecione **Gerenciar DNS**.</span><span class="sxs-lookup"><span data-stu-id="1b3a8-111">Select the drop-down menu for the domain name that you wish to use with your Azure web app and select **Manage DNS**.</span></span>
   
    ![página de domínio personalizado para GoDaddy](./media/web-sites-godaddy-custom-domain-name/godaddy-customdomain.png)
2. <span data-ttu-id="1b3a8-113">Na página **Detalhes do domínio**, role até a guia **Arquivo de zona DNS**.</span><span class="sxs-lookup"><span data-stu-id="1b3a8-113">From the **Domain details** page, scroll to the **DNS Zone File** tab.</span></span> <span data-ttu-id="1b3a8-114">Esta é a seção usada para adicionar e modificar registros DNS para o nome do domínio.</span><span class="sxs-lookup"><span data-stu-id="1b3a8-114">This is the section used for adding and modifying DNS records for your domain name.</span></span>
   
    ![Guia Arquivo de Zona DNS](./media/web-sites-godaddy-custom-domain-name/godaddy-zonetab.png)
   
    <span data-ttu-id="1b3a8-116">Selecione **Adicionar registro** para adicionar um registro existente.</span><span class="sxs-lookup"><span data-stu-id="1b3a8-116">Select **Add Record** to add an existing record.</span></span>
   
    <span data-ttu-id="1b3a8-117">Para **editar** um registro existente, selecione o ícone de lápis e papel ao lado do registro.</span><span class="sxs-lookup"><span data-stu-id="1b3a8-117">To **edit** an existing record, select the pen & paper icon beside the record.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1b3a8-118">Antes de adicionar os novos registros, observe que o GoDaddy já criou os registros DNS para subdomínios populares (chamados **Host** no editor), como **email**, **arquivos**, **correio** e outros.</span><span class="sxs-lookup"><span data-stu-id="1b3a8-118">Before adding new records, note that GoDaddy has already created DNS records for popular sub-domains (called **Host** in editor,) such as **email**, **files**, **mail**, and others.</span></span> <span data-ttu-id="1b3a8-119">Se o nome que você deseja usar já existir, modifique o registro existente em vez de criar um novo.</span><span class="sxs-lookup"><span data-stu-id="1b3a8-119">If the name you wish to use already exists, modify the existing record instead of creating a new one.</span></span>
   > 
   > 
3. <span data-ttu-id="1b3a8-120">Ao adicionar um registro, você deve primeiro, selecionar o tipo de registro.</span><span class="sxs-lookup"><span data-stu-id="1b3a8-120">When adding a record, you must first select the record type.</span></span>
   
    ![selecione o tipo de registro](./media/web-sites-godaddy-custom-domain-name/godaddy-selectrecordtype.png)
   
    <span data-ttu-id="1b3a8-122">Em seguida, você deve fornecer o **Host** (o domínio ou subdomínio personalizado) e ao que ele **Aponta para**.</span><span class="sxs-lookup"><span data-stu-id="1b3a8-122">Next, you must provide the **Host** (the custom domain or sub-domain) and what it **Points to**.</span></span>
   
    ![adicionar um registro de zona](./media/web-sites-godaddy-custom-domain-name/godaddy-addzonerecord.png)
   
   * <span data-ttu-id="1b3a8-124">Ao adicionar um **registro A (host)** – você deve definir o campo **Host** como **@** (isso representa o nome do domínio raiz, como **contoso.com**), * (um caractere curinga para corresponder a vários subdomínios) ou o subdomínio que você deseja usar (por exemplo, **www**). Você deve definir o campo **Aponta para** como o endereço IP do seu aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="1b3a8-124">When adding an **A (host) record** - you must set the **Host** field to either **@** (this represents root domain name, such as **contoso.com**,) * (a wildcard for matching multiple sub-domains,) or the sub-domain you wish to use (for example, **www**.) You must set the **Points to** field to the IP address of your Azure web app.</span></span>
   * <span data-ttu-id="1b3a8-125">Ao adicionar um **registro CNAME (alias)** - você deve definir o campo **Host** como o subdomínio que deseja usar.</span><span class="sxs-lookup"><span data-stu-id="1b3a8-125">When adding a **CNAME (alias) record** - you must set the **Host** field to the sub-domain you wish to use.</span></span> <span data-ttu-id="1b3a8-126">Por exemplo, **www**.</span><span class="sxs-lookup"><span data-stu-id="1b3a8-126">For example, **www**.</span></span> <span data-ttu-id="1b3a8-127">Você deve definir o campo **Aponta para** como o nome do domínio **.azurewebsites.net** do aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="1b3a8-127">You must set the **Points to** field to the **.azurewebsites.net** domain name of your Azure web app.</span></span> <span data-ttu-id="1b3a8-128">Por exemplo, **contoso.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="1b3a8-128">For example, **contoso.azurewebsites.net**.</span></span>
4. <span data-ttu-id="1b3a8-129">Clique em **Adicionar Outro**.</span><span class="sxs-lookup"><span data-stu-id="1b3a8-129">Click **Add Another**.</span></span>
5. <span data-ttu-id="1b3a8-130">Selecione **TXT** como o tipo de registro e especifique um valor de **Host** de **@** e um valor de **Aponta para** de **&lt;yourwebappname&gt;.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="1b3a8-130">Select **TXT** as the record type, then specify a **Host** value of **@** and a **Points to** value of **&lt;yourwebappname&gt;.azurewebsites.net**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1b3a8-131">Esse registro TXT é usado pelo Azure para validar que você possui o domínio descrito pelo registro A do primeiro registro TXT.</span><span class="sxs-lookup"><span data-stu-id="1b3a8-131">This TXT record is used by Azure to validate that you own the domain described by the A record or the first TXT record.</span></span> <span data-ttu-id="1b3a8-132">Depois que o domínio tiver sido mapeado para o aplicativo Web no Portal do Azure, essa entrada do registro TXT poderá ser removida.</span><span class="sxs-lookup"><span data-stu-id="1b3a8-132">Once the domain has been mapped to the web app in the Azure Portal, this TXT record entry can be removed.</span></span>
   > 
   > 
6. <span data-ttu-id="1b3a8-133">Ao concluir a adição ou a modificação dos registros, clique em **Concluir** para salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="1b3a8-133">When you have finished adding or modifying records, click **Finish** to save changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-the-domain-name-on-your-web-app"></a><span data-ttu-id="1b3a8-134">Habilitar o nome do domínio no seu aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="1b3a8-134">Enable the domain name on your web app</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-web-site.md)]

> [!NOTE]
> <span data-ttu-id="1b3a8-135">Se desejar começar a usar o Serviço de Aplicativo do Azure antes de inscrever-se em uma conta do Azure, vá para [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo Web inicial de curta duração no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1b3a8-135">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="1b3a8-136">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="1b3a8-136">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="1b3a8-137">O que mudou</span><span class="sxs-lookup"><span data-stu-id="1b3a8-137">What's changed</span></span>
* <span data-ttu-id="1b3a8-138">Para obter um guia sobre a alteração de Sites para o Serviço de Aplicativo, consulte: [Serviço de Aplicativo do Azure e seu impacto sobre os serviços do Azure existentes](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="1b3a8-138">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

