---
title: "aaaConfigure um nome de domínio personalizado para um aplicativo web no serviço de aplicativo do Azure que usa o Gerenciador de tráfego de balanceamento de carga."
description: "Use um nome de domínio personalizado para um aplicativo Web no Serviço de Aplicativo do Azure que inclua o Gerenciador de Tráfego para balanceamento de carga."
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 0f96c0e7-0901-489b-a95a-e3b66ca0a1c2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: dfde5fc6b445b30b10e03dcb03e8d072130d9377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-a-web-app-in-azure-app-service-using-traffic-manager"></a><span data-ttu-id="39c8b-103">Configurando um nome de domínio personalizado para um aplicativo Web no Serviço de Aplicativo do Azure usando o Gerenciador de Tráfego</span><span class="sxs-lookup"><span data-stu-id="39c8b-103">Configuring a custom domain name for a web app in Azure App Service using Traffic Manager</span></span>
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro-traffic-manager.md)]

<span data-ttu-id="39c8b-104">Este artigo fornece instruções genéricas sobre como usar um nome de domínio personalizado com o Serviço de Aplicativo do Azure que usa o Gerenciador de Tráfego para balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="39c8b-104">This article provides generic instructions for using a custom domain name with Azure App Service that use Traffic Manager for load balancing.</span></span>

[!INCLUDE [tmwebsitefooter](../../includes/custom-dns-web-site-traffic-manager-notes.md)]

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a><span data-ttu-id="39c8b-105">Compreendendo os registros DNS</span><span class="sxs-lookup"><span data-stu-id="39c8b-105">Understanding DNS records</span></span>
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-traffic-manager.md)]

<a name="bkmk_configsharedmode"></a>

## <a name="configure-your-web-apps-for-standard-mode"></a><span data-ttu-id="39c8b-106">Configurar seus aplicativos Web para o modo Padrão</span><span class="sxs-lookup"><span data-stu-id="39c8b-106">Configure your web apps for standard mode</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-modes-traffic-manager.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a><span data-ttu-id="39c8b-107">Adicionar um registro DNS a seu domínio personalizado</span><span class="sxs-lookup"><span data-stu-id="39c8b-107">Add a DNS record for your custom domain</span></span>
> [!NOTE]
> <span data-ttu-id="39c8b-108">Se você tiver adquirido por meio de aplicativos de Web do serviço de aplicativo do Azure ignorar as etapas a seguir e consulte a etapa final toohello do [comprar o domínio para aplicativos Web](custom-dns-web-site-buydomains-web-app.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="39c8b-108">If you have purchased domain through Azure App Service Web Apps then skip following steps and refer toohello final step of [Buy Domain for Web Apps](custom-dns-web-site-buydomains-web-app.md) article.</span></span>
> 
> 

<span data-ttu-id="39c8b-109">tooassociate seu domínio personalizado com um aplicativo web no serviço de aplicativo do Azure, você deve adicionar uma nova entrada na tabela DNS Olá para seu domínio personalizado usando as ferramentas fornecidas pelo registrador Olá que você adquiriu o seu nome de domínio.</span><span class="sxs-lookup"><span data-stu-id="39c8b-109">tooassociate your custom domain with a web app in Azure App Service, you must add a new entry in hello DNS table for your custom domain by using tools provided by hello domain registrar that you purchased your domain name from.</span></span> <span data-ttu-id="39c8b-110">Use Olá toolocate as etapas a seguir e as ferramentas do DNS hello.</span><span class="sxs-lookup"><span data-stu-id="39c8b-110">Use hello following steps toolocate and use hello DNS tools.</span></span>

1. <span data-ttu-id="39c8b-111">Entrar na conta tooyour no seu registrador de domínio e procure por uma página de gerenciamento de registros DNS.</span><span class="sxs-lookup"><span data-stu-id="39c8b-111">Sign in tooyour account at your domain registrar, and look for a page for managing DNS records.</span></span> <span data-ttu-id="39c8b-112">Procure links ou áreas do site de saudação rotulados como **nome de domínio**, **DNS**, ou **nome do servidor de gerenciamento**.</span><span class="sxs-lookup"><span data-stu-id="39c8b-112">Look for links or areas of hello site labeled as **Domain Name**, **DNS**, or **Name Server Management**.</span></span> <span data-ttu-id="39c8b-113">Geralmente um link de página toothis pode ser encontrada ser exibindo as informações da conta e procurando um link como **Meus domínios**.</span><span class="sxs-lookup"><span data-stu-id="39c8b-113">Often a link toothis page can be found be viewing your account information, and then looking for a link such as **My domains**.</span></span>
2. <span data-ttu-id="39c8b-114">Após localizar página de gerenciamento de saudação para seu nome de domínio, procure um link que permite que os registros DNS Olá tooedit.</span><span class="sxs-lookup"><span data-stu-id="39c8b-114">Once you have found hello management page for your domain name, look for a link that allows you tooedit hello DNS records.</span></span> <span data-ttu-id="39c8b-115">Ele pode estar listado como um **Arquivo de zona**, **Registros DNS** ou como um link de configuração **Avançado**.</span><span class="sxs-lookup"><span data-stu-id="39c8b-115">This might be listed as a **Zone file**, **DNS Records**, or as an **Advanced** configuration link.</span></span>
   
   * <span data-ttu-id="39c8b-116">página de saudação provavelmente terá alguns registros já criados, como uma associação de entrada '**@**'ou'\*' com uma página 'estacionamento domínio'.</span><span class="sxs-lookup"><span data-stu-id="39c8b-116">hello page will most likely have a few records already created, such as an entry associating '**@**' or '\*' with a 'domain parking' page.</span></span> <span data-ttu-id="39c8b-117">Ela também pode conter registros para subdomínios comuns como **www**.</span><span class="sxs-lookup"><span data-stu-id="39c8b-117">It may also contain records for common sub-domains such as **www**.</span></span>
   * <span data-ttu-id="39c8b-118">página Hello serão mencionar **registros CNAME**, ou forneça uma lista suspensa tooselect um tipo de registro.</span><span class="sxs-lookup"><span data-stu-id="39c8b-118">hello page will mention **CNAME records**, or provide a drop-down tooselect a record type.</span></span> <span data-ttu-id="39c8b-119">Ela também pode mencionar outros registros, como **registros A** e **registros MX**.</span><span class="sxs-lookup"><span data-stu-id="39c8b-119">It may also mention other records such as **A records** and **MX records**.</span></span> <span data-ttu-id="39c8b-120">Em alguns casos, os registros CNAME serão chamados por outros nomes como um **Registro de Alias**.</span><span class="sxs-lookup"><span data-stu-id="39c8b-120">In some cases, CNAME records will be called by other names such as an **Alias Record**.</span></span>
   * <span data-ttu-id="39c8b-121">página Olá também terá campos que permitem muito**mapa** de um **nome de Host** ou **nome de domínio** tooanother nome de domínio.</span><span class="sxs-lookup"><span data-stu-id="39c8b-121">hello page will also have fields that allow you too**map** from a **Host name** or **Domain name** tooanother domain name.</span></span>
3. <span data-ttu-id="39c8b-122">Embora especificidades de saudação do registrador de cada variam, em geral você mapear *de* seu nome de domínio personalizado (como **contoso.com**,) *para* nome de domínio do Traffic Manager hello (**contoso.trafficmanager.net**) que é usado para seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="39c8b-122">While hello specifics of each registrar vary, in general you map *from* your custom domain name (such as **contoso.com**,) *to* hello Traffic Manager domain name (**contoso.trafficmanager.net**) that is used for your web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="39c8b-123">Como alternativa, se um registro já está em uso e você precisar toopreemptively associar tooit seus aplicativos, você pode criar um registro CNAME adicional.</span><span class="sxs-lookup"><span data-stu-id="39c8b-123">Alternatively, if a record is already in use and you need toopreemptively bind your apps tooit, you can create an additional CNAME record.</span></span> <span data-ttu-id="39c8b-124">Por exemplo, associação de toopreemptively **www.contoso.com** tooyour web app, crie um registro CNAME do **awverify.www** muito**contoso.trafficmanager.net**.</span><span class="sxs-lookup"><span data-stu-id="39c8b-124">For example, toopreemptively bind **www.contoso.com** tooyour web app, create a CNAME record from **awverify.www** too**contoso.trafficmanager.net**.</span></span> <span data-ttu-id="39c8b-125">Em seguida, você pode adicionar tooyour "www.contoso.com" aplicativo Web sem alterar o registro CNAME "www" hello.</span><span class="sxs-lookup"><span data-stu-id="39c8b-125">You can then add "www.contoso.com" tooyour Web App without changing hello "www" CNAME record.</span></span> <span data-ttu-id="39c8b-126">Para saber mais, confira [Criar registros DNS para um aplicativo Web em um domínio personalizado][CREATEDNS].</span><span class="sxs-lookup"><span data-stu-id="39c8b-126">For more information, see [Create DNS records for a web app in a custom domain][CREATEDNS].</span></span>
   > 
   > 
4. <span data-ttu-id="39c8b-127">Depois de terminar de adicionar ou modificar os registros DNS no registrador, salve as alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="39c8b-127">Once you have finished adding or modifying DNS records at your registrar, save hello changes.</span></span>

<a name="enabledomain"></a>

## <a name="enable-traffic-manager"></a><span data-ttu-id="39c8b-128">Habilitar o Gerenciador de tráfego</span><span class="sxs-lookup"><span data-stu-id="39c8b-128">Enable Traffic Manager</span></span>
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-traffic-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="39c8b-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="39c8b-129">Next steps</span></span>
<span data-ttu-id="39c8b-130">Para obter mais informações, consulte Olá [Node. js Developer Center](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="39c8b-130">For more information, see hello [Node.js Developer Center](/develop/nodejs/).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[CREATEDNS]: ../dns/dns-web-sites-custom-domain.md
