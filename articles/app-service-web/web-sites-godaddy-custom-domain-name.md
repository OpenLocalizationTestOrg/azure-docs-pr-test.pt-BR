---
title: "aaaConfigure um nome de domínio personalizado no serviço de aplicativo do Azure (GoDaddy)"
description: "Saiba como toouse um domínio nome do GoDaddy com aplicativos Web do Azure"
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
ms.openlocfilehash: 48158ee752f9833249bbf85adf80f572d1c68486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-custom-domain-name-in-azure-app-service-purchased-directly-from-godaddy"></a><span data-ttu-id="a558e-103">Configurar um nome de domínio personalizado no Serviço de Aplicativo do Azure (adquirido diretamente do GoDaddy)</span><span class="sxs-lookup"><span data-stu-id="a558e-103">Configure a custom domain name in Azure App Service (Purchased directly from GoDaddy)</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro.md)]

<span data-ttu-id="a558e-104">Se você tiver adquirido por meio de aplicativos de Web do serviço de aplicativo do Azure, consulte a etapa final toohello do [comprar o domínio para aplicativos Web](custom-dns-web-site-buydomains-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="a558e-104">If you have purchased domain through Azure App Service Web Apps then refer toohello final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md).</span></span>

<span data-ttu-id="a558e-105">Este artigo fornece instruções sobre como usar um nome de domínio personalizado adquirido diretamente de [GoDaddy](https://godaddy.com) com [Aplicativos Web do Serviço de Aplicativo](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="a558e-105">This article provides instructions on using a custom domain name that was purchased directly from [GoDaddy](https://godaddy.com) with [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="a558e-106">Compreendendo os registros DNS</span><span class="sxs-lookup"><span data-stu-id="a558e-106">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-raw.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="a558e-107">Adicionar um registro DNS a seu domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="a558e-107">Add a DNS record for your custom domain</span></span>
<span data-ttu-id="a558e-108">tooassociate seu domínio personalizado com um aplicativo web no serviço de aplicativo, você deve adicionar uma nova entrada na tabela DNS Olá para seu domínio personalizado usando as ferramentas fornecidas pelo GoDaddy.</span><span class="sxs-lookup"><span data-stu-id="a558e-108">tooassociate your custom domain with a web app in App Service, you must add a new entry in hello DNS table for your custom domain by using tools provided by GoDaddy.</span></span> <span data-ttu-id="a558e-109">Olá uso seguindo as etapas toolocate Olá DNS ferramentas para GoDaddy.com</span><span class="sxs-lookup"><span data-stu-id="a558e-109">Use hello following steps toolocate hello DNS tools for GoDaddy.com</span></span>

1. <span data-ttu-id="a558e-110">Fazer logon na conta tooyour com GoDaddy.com e selecione **minha conta** e **gerenciar Meus domínios**.</span><span class="sxs-lookup"><span data-stu-id="a558e-110">Log on tooyour account with GoDaddy.com, and select **My Account** and then **Manage my domains**.</span></span> <span data-ttu-id="a558e-111">Menu suspenso de seleção Olá Olá nome de domínio que você deseja toouse com seu aplicativo web do Azure e selecione **gerenciar DNS**.</span><span class="sxs-lookup"><span data-stu-id="a558e-111">Select hello drop-down menu for hello domain name that you wish toouse with your Azure web app and select **Manage DNS**.</span></span>
   
    ![página de domínio personalizado para GoDaddy](./media/web-sites-godaddy-custom-domain-name/godaddy-customdomain.png)
2. <span data-ttu-id="a558e-113">De saudação **detalhes do domínio** página, role toohello **arquivo de zona DNS** guia. Isso é usada para adicionar e modificar os registros DNS para seu nome de domínio da seção de saudação.</span><span class="sxs-lookup"><span data-stu-id="a558e-113">From hello **Domain details** page, scroll toohello **DNS Zone File** tab. This is hello section used for adding and modifying DNS records for your domain name.</span></span>
   
    ![Guia Arquivo de Zona DNS](./media/web-sites-godaddy-custom-domain-name/godaddy-zonetab.png)
   
    <span data-ttu-id="a558e-115">Selecione **adicionar registro** tooadd um registro existente.</span><span class="sxs-lookup"><span data-stu-id="a558e-115">Select **Add Record** tooadd an existing record.</span></span>
   
    <span data-ttu-id="a558e-116">muito**editar** um registro existente, o ícone de caneta e papel Olá select ao lado de registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="a558e-116">too**edit** an existing record, select hello pen & paper icon beside hello record.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a558e-117">Antes de adicionar os novos registros, observe que o GoDaddy já criou os registros DNS para subdomínios populares (chamados **Host** no editor), como **email**, **arquivos**, **correio** e outros.</span><span class="sxs-lookup"><span data-stu-id="a558e-117">Before adding new records, note that GoDaddy has already created DNS records for popular sub-domains (called **Host** in editor,) such as **email**, **files**, **mail**, and others.</span></span> <span data-ttu-id="a558e-118">Se nome hello desejar toouse já existir, modifique o registro existente do hello em vez de criar um novo.</span><span class="sxs-lookup"><span data-stu-id="a558e-118">If hello name you wish toouse already exists, modify hello existing record instead of creating a new one.</span></span>
   > 
   > 
3. <span data-ttu-id="a558e-119">Ao adicionar um registro, você deve primeiro selecionar tipo de registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="a558e-119">When adding a record, you must first select hello record type.</span></span>
   
    ![selecione o tipo de registro](./media/web-sites-godaddy-custom-domain-name/godaddy-selectrecordtype.png)
   
    <span data-ttu-id="a558e-121">Em seguida, você deve fornecer Olá **Host** (Olá domínio personalizado ou subdomínio) e o que ele **aponta para**.</span><span class="sxs-lookup"><span data-stu-id="a558e-121">Next, you must provide hello **Host** (hello custom domain or sub-domain) and what it **Points to**.</span></span>
   
    ![adicionar um registro de zona](./media/web-sites-godaddy-custom-domain-name/godaddy-addzonerecord.png)
   
   * <span data-ttu-id="a558e-123">Ao adicionar um **um registro (host)** -você deve definir Olá **Host** campo tooeither  **@**  (isso representa o nome do domínio raiz, como  **Contoso.com**,) * (curinga para correspondência de vários subdomínios,) ou subdomínio de saudação desejar toouse (por exemplo, **www**.) Você deve definir Olá **aponta para** campo toohello endereço IP de seu aplicativo web do Azure.</span><span class="sxs-lookup"><span data-stu-id="a558e-123">When adding an **A (host) record** - you must set hello **Host** field tooeither **@** (this represents root domain name, such as **contoso.com**,) * (a wildcard for matching multiple sub-domains,) or hello sub-domain you wish toouse (for example, **www**.) You must set hello **Points to** field toohello IP address of your Azure web app.</span></span>
   * <span data-ttu-id="a558e-124">Ao adicionar um **registro CNAME (alias)** -você deve definir Olá **Host** campo toohello subdomínio desejar toouse.</span><span class="sxs-lookup"><span data-stu-id="a558e-124">When adding a **CNAME (alias) record** - you must set hello **Host** field toohello sub-domain you wish toouse.</span></span> <span data-ttu-id="a558e-125">Por exemplo, **www**.</span><span class="sxs-lookup"><span data-stu-id="a558e-125">For example, **www**.</span></span> <span data-ttu-id="a558e-126">Você deve definir Olá **aponta para** campo toohello **. azurewebsites.net** nome de domínio do seu aplicativo web do Azure.</span><span class="sxs-lookup"><span data-stu-id="a558e-126">You must set hello **Points to** field toohello **.azurewebsites.net** domain name of your Azure web app.</span></span> <span data-ttu-id="a558e-127">Por exemplo, **contoso.azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="a558e-127">For example, **contoso.azurewebsites.net**.</span></span>
4. <span data-ttu-id="a558e-128">Clique em **Adicionar Outro**.</span><span class="sxs-lookup"><span data-stu-id="a558e-128">Click **Add Another**.</span></span>
5. <span data-ttu-id="a558e-129">Selecione **TXT** como o tipo de registro hello, em seguida, especifique um **Host** valor  **@**  e um **aponta para** valor  **&lt;yourwebappname&gt;. azurewebsites.net**.</span><span class="sxs-lookup"><span data-stu-id="a558e-129">Select **TXT** as hello record type, then specify a **Host** value of **@** and a **Points to** value of **&lt;yourwebappname&gt;.azurewebsites.net**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a558e-130">Esse registro TXT é usado pelo toovalidate do Azure que você possui o domínio Olá descrito pelo Olá um registro TXT de primeiro do registro ou hello.</span><span class="sxs-lookup"><span data-stu-id="a558e-130">This TXT record is used by Azure toovalidate that you own hello domain described by hello A record or hello first TXT record.</span></span> <span data-ttu-id="a558e-131">Depois que o domínio de saudação foi mapeada toohello aplicativo web hello Portal do Azure, essa entrada de registro TXT pode ser removida.</span><span class="sxs-lookup"><span data-stu-id="a558e-131">Once hello domain has been mapped toohello web app in hello Azure Portal, this TXT record entry can be removed.</span></span>
   > 
   > 
6. <span data-ttu-id="a558e-132">Quando você terminar de adicionar ou modificar registros, clique em **concluir** toosave alterações.</span><span class="sxs-lookup"><span data-stu-id="a558e-132">When you have finished adding or modifying records, click **Finish** toosave changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-hello-domain-name-on-your-web-app"></a><span data-ttu-id="a558e-133">Habilitar o nome de domínio de saudação em seu aplicativo web</span><span class="sxs-lookup"><span data-stu-id="a558e-133">Enable hello domain name on your web app</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-web-site.md)]

> [!NOTE]
> <span data-ttu-id="a558e-134">Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo web de curta duração starter no serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a558e-134">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="a558e-135">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="a558e-135">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="a558e-136">O que mudou</span><span class="sxs-lookup"><span data-stu-id="a558e-136">What's changed</span></span>
* <span data-ttu-id="a558e-137">Para um guia toohello alteração de sites tooApp serviço consulte: [do serviço de aplicativo do Azure e seu impacto sobre os serviços do Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="a558e-137">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

