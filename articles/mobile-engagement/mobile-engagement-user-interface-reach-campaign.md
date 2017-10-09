---
title: "aaaAzure Interface de usuário do Mobile Engagement - campanha de alcance"
description: "Laern como toocreate e gerenciar campanhas de notificação por push usando o Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2fe124a2-a86f-4136-81ba-a9d298ec798a
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 825e550ace63a34d1a90b10fa976a61eb15a6d04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-push-notification-campaigns"></a><span data-ttu-id="b6cf3-103">Como toocreate e gerenciar campanhas de notificação por push</span><span class="sxs-lookup"><span data-stu-id="b6cf3-103">How toocreate and manage push notification campaigns</span></span>
<span data-ttu-id="b6cf3-104">Você pode usar o hello seção alcance de saudação da interface do usuário toocreate uma nova campanha de Push com uma fórmula complexa, fornecendo todas as informações de saudação necessário toosend uma notificação por push.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-104">You can use hello Reach section of hello UI toocreate a new Push campaign with a complex formula by providing all hello information you need toosend a push notification.</span></span> <span data-ttu-id="b6cf3-105">Olá opções de uma campanha de Push variam ligeiramente, dependendo tipos de campanha Olá quatro: anúncios, votações, envia dados e lado a lado (somente no Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="b6cf3-105">hello options of a Push campaign vary slightly depending on hello four campaign types: Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span>

### <a name="option-applies-to"></a><span data-ttu-id="b6cf3-106">As Opções se Aplicam a:</span><span class="sxs-lookup"><span data-stu-id="b6cf3-106">Option Applies to:</span></span>
* <span data-ttu-id="b6cf3-107">Idiomas: todos (Anúncios, Pesquisas, Envio de Dados por Push, Blocos)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-107">Languages:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="b6cf3-108">Campanha: todos (Anúncios, Pesquisas, Envio de Dados por Push, Blocos)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-108">Campaign:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="b6cf3-109">Notificação: anúncios, pesquisas</span><span class="sxs-lookup"><span data-stu-id="b6cf3-109">Notification:     Announcements, Polls</span></span>
* <span data-ttu-id="b6cf3-110">Conteúdo: exclusivo para cada tipo de campanha</span><span class="sxs-lookup"><span data-stu-id="b6cf3-110">Content:    Unique for each campaign type</span></span>
* <span data-ttu-id="b6cf3-111">Público-alvo: todos (Anúncios, Pesquisas, Envio de Dados por Push, Blocos)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-111">Audience:     All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="b6cf3-112">Período: anúncios, pesquisas, blocos</span><span class="sxs-lookup"><span data-stu-id="b6cf3-112">Time frame:     Announcements, Polls, Tiles</span></span>
* <span data-ttu-id="b6cf3-113">Teste: todos (Anúncios, Pesquisas, Envio de Dados por Push, Blocos)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-113">Test:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>

![Reach-Campaign1][20]

## <a name="languages"></a><span data-ttu-id="b6cf3-115">Linguagens</span><span class="sxs-lookup"><span data-stu-id="b6cf3-115">Languages</span></span>
<span data-ttu-id="b6cf3-116">Você pode usar o hello idiomas lista suspensa menu toosend uma versão diferente do seu toodevices Push definidas toouse diferentes idiomas.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-116">You can use hello Languages drop-down menu toosend a different version of your Push toodevices that are set toouse different languages.</span></span> <span data-ttu-id="b6cf3-117">Por padrão, todos os dispositivos receberá Olá mesmo Push, independentemente da linguagem em que elas são definidas toouse.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-117">By default, all devices will receive hello same Push regardless of what language they are set toouse.</span></span> <span data-ttu-id="b6cf3-118">Os usuários com idioma diferente do conjunto tooa seu dispositivo receberá a versão de idioma padrão de saudação do hello por Push.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-118">Users with their device set tooa different language will receive hello Default Language version of hello Push.</span></span> <span data-ttu-id="b6cf3-119">Muitas das opções de campanha de push Olá permitem conteúdo alternativo toospecify para cada um dos idiomas adicionais hello, que você selecionar.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-119">Many of hello push campaign options allow you toospecify alternate content for each of hello additional languages you select.</span></span> 

![Reach-Campaign2][21]

### <a name="language-differences-apply-to"></a><span data-ttu-id="b6cf3-121">As diferenças de idioma se aplicam a:</span><span class="sxs-lookup"><span data-stu-id="b6cf3-121">Language differences apply to:</span></span>
* <span data-ttu-id="b6cf3-122">Idiomas: Idiomas exclusivos podem ser selecionados de linguagem adição toohello padrão</span><span class="sxs-lookup"><span data-stu-id="b6cf3-122">Languages:    Unique languages may be selected in addition toohello default language</span></span>
* <span data-ttu-id="b6cf3-123">Campanha: a mesma para todos os idiomas</span><span class="sxs-lookup"><span data-stu-id="b6cf3-123">Campaign:    Same for all languages</span></span>
* <span data-ttu-id="b6cf3-124">Notificação: Exclusivo para cada idioma além toohello idioma padrão</span><span class="sxs-lookup"><span data-stu-id="b6cf3-124">Notification:    Unique for each language in addition toohello default language</span></span>
* <span data-ttu-id="b6cf3-125">Conteúdo: Exclusivo para cada idioma além toohello idioma padrão</span><span class="sxs-lookup"><span data-stu-id="b6cf3-125">Content:    Unique for each language in addition toohello default language</span></span>
* <span data-ttu-id="b6cf3-126">Público-alvo: pode ser filtrado por um critério de idioma separado</span><span class="sxs-lookup"><span data-stu-id="b6cf3-126">Audience:     May be filtered by a separate language criterion</span></span>
* <span data-ttu-id="b6cf3-127">Período: o mesmo para todos os idiomas</span><span class="sxs-lookup"><span data-stu-id="b6cf3-127">Time frame:     Same for all languages</span></span>
* <span data-ttu-id="b6cf3-128">Teste: Podem ser enviados a linguagem tooeach por vez</span><span class="sxs-lookup"><span data-stu-id="b6cf3-128">Test:    May be sent tooeach language at a time</span></span>

### <a name="supported-languages"></a><span data-ttu-id="b6cf3-129">Idiomas com suporte:</span><span class="sxs-lookup"><span data-stu-id="b6cf3-129">Supported Languages:</span></span>
* <span data-ttu-id="b6cf3-130">Árabe (ar)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-130">Arabic (ar)</span></span> 
* <span data-ttu-id="b6cf3-131">Búlgaro (bg)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-131">Bulgarian (bg)</span></span> 
* <span data-ttu-id="b6cf3-132">Catalão (ca)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-132">Catalan (ca)</span></span> 
* <span data-ttu-id="b6cf3-133">Chinês (zh)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-133">Chinese (zh)</span></span> 
* <span data-ttu-id="b6cf3-134">Croata (h)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-134">Croatian (hr)</span></span> 
* <span data-ttu-id="b6cf3-135">Tcheco (cs)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-135">Czech (cs)</span></span> 
* <span data-ttu-id="b6cf3-136">Dinamarquês (da)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-136">Danish (da)</span></span> 
* <span data-ttu-id="b6cf3-137">Holandês (nl)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-137">Dutch (nl)</span></span> 
* <span data-ttu-id="b6cf3-138">Inglês (en)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-138">English (en)</span></span> 
* <span data-ttu-id="b6cf3-139">Finlandês (fi)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-139">Finnish (fi)</span></span> 
* <span data-ttu-id="b6cf3-140">Francês (fr)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-140">French (fr)</span></span> 
* <span data-ttu-id="b6cf3-141">Alemão (de)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-141">German (de)</span></span> 
* <span data-ttu-id="b6cf3-142">Grego (el)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-142">Greek (el)</span></span> 
* <span data-ttu-id="b6cf3-143">Hebraico (he)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-143">Hebrew (he)</span></span> 
* <span data-ttu-id="b6cf3-144">Híndi (Olá)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-144">Hindi (hi)</span></span> 
* <span data-ttu-id="b6cf3-145">Húngaro (hu)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-145">Hungarian (hu)</span></span> 
* <span data-ttu-id="b6cf3-146">Indonésio (id)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-146">Indonesian (id)</span></span> 
* <span data-ttu-id="b6cf3-147">Italiano (it)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-147">Italian (it)</span></span> 
* <span data-ttu-id="b6cf3-148">Japonês (ja)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-148">Japanese (ja)</span></span> 
* <span data-ttu-id="b6cf3-149">Coreano (ko)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-149">Korean (ko)</span></span> 
* <span data-ttu-id="b6cf3-150">Letão (lv)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-150">Latvian (lv)</span></span> 
* <span data-ttu-id="b6cf3-151">Lituano (lt)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-151">Lithuanian (lt)</span></span> 
* <span data-ttu-id="b6cf3-152">Malaio (macroidioma) (ms)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-152">Malay (macrolanguage) (ms)</span></span> 
* <span data-ttu-id="b6cf3-153">Norueguês Bokmål (nb)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-153">Norwegian Bokmål (nb)</span></span> 
* <span data-ttu-id="b6cf3-154">Polonês (pl)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-154">Polish (pl)</span></span> 
* <span data-ttu-id="b6cf3-155">Português (Portugal)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-155">Portuguese (pt)</span></span> 
* <span data-ttu-id="b6cf3-156">Romeno (ro)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-156">Romanian (ro)</span></span> 
* <span data-ttu-id="b6cf3-157">Russo (ru)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-157">Russian (ru)</span></span> 
* <span data-ttu-id="b6cf3-158">Sérvio (sr)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-158">Serbian (sr)</span></span> 
* <span data-ttu-id="b6cf3-159">Eslovaco (discos)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-159">Slovak (sk)</span></span> 
* <span data-ttu-id="b6cf3-160">Esloveno (sl)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-160">Slovenian (sl)</span></span> 
* <span data-ttu-id="b6cf3-161">Espanhol (es)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-161">Spanish (es)</span></span> 
* <span data-ttu-id="b6cf3-162">Sueco (sv)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-162">Swedish (sv)</span></span> 
* <span data-ttu-id="b6cf3-163">Tagalo (NFA)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-163">Tagalog (tl)</span></span> 
* <span data-ttu-id="b6cf3-164">Tailandês (th)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-164">Thai (th)</span></span> 
* <span data-ttu-id="b6cf3-165">Turco (tr)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-165">Turkish (tr)</span></span> 
* <span data-ttu-id="b6cf3-166">Ucraniano (uk)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-166">Ukrainian (uk)</span></span> 
* <span data-ttu-id="b6cf3-167">Vietnamita (vi)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-167">Vietnamese (vi)</span></span> 

## <a name="campaign"></a><span data-ttu-id="b6cf3-168">Campanha</span><span class="sxs-lookup"><span data-stu-id="b6cf3-168">Campaign</span></span>
<span data-ttu-id="b6cf3-169">Você pode usar Olá campanha seção tooset Olá nome e a categoria da campanha, bem como se você planejar tooignore seção de público-alvo de saudação de uma campanha de Push e envia essa campanha via API de alcance da saudação (e alguns elementos de nível baixo de saudação API por Push) em vez disso.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-169">You can use hello Campaign section tooset hello name and category of your campaign as well as if you plan tooignore hello audience section of a Push campaign and send this campaign via hello Reach API (and some elements with hello low level Push API) instead.</span></span> <span data-ttu-id="b6cf3-170">Categorias podem ser usadas com uma notificação personalizada modelo toocontrol no aplicativo as notificações com base em configurações predefinidas.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-170">Categories can be used with a custom notification template toocontrol in-app notifications based on predefined settings.</span></span> <span data-ttu-id="b6cf3-171">Você pode obter uma lista existente "categorias" via Olá API de alcance.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-171">You can get a list of your existing “Categories” via hello Reach API.</span></span>

> [!WARNING]
> <span data-ttu-id="b6cf3-172">Se você usar a opção de "Ignorar público, push será enviado toousers via API de hello" Olá, na seção de "Da campanha" hello de uma campanha de alcance, campanha de saudação não enviará automaticamente, você precisará toosend-los manualmente por meio de saudação API de alcance.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-172">If you use hello "Ignore Audience, push will be sent toousers via hello API" option in hello "Campaign" section of a Reach campaign, hello campaign will NOT automatically send, you will need toosend it manually via hello Reach API.</span></span>

![Reach-Campaign3][22]

### <a name="option-applies-to"></a><span data-ttu-id="b6cf3-174">As Opções se Aplicam a:</span><span class="sxs-lookup"><span data-stu-id="b6cf3-174">Option Applies to:</span></span>
* <span data-ttu-id="b6cf3-175">Nome: todos</span><span class="sxs-lookup"><span data-stu-id="b6cf3-175">Name:    All</span></span>
* <span data-ttu-id="b6cf3-176">Categoria: anúncios, pesquisas</span><span class="sxs-lookup"><span data-stu-id="b6cf3-176">Category:    Announcements, Polls</span></span>
* <span data-ttu-id="b6cf3-177">Ignorar o público-alvo, push será enviado toousers via Olá API: todos os</span><span class="sxs-lookup"><span data-stu-id="b6cf3-177">Ignore Audience, push will be sent toousers via hello API:    All</span></span>

## <a name="notification"></a><span data-ttu-id="b6cf3-178">Notificação</span><span class="sxs-lookup"><span data-stu-id="b6cf3-178">Notification</span></span>
<span data-ttu-id="b6cf3-179">Você pode usar o hello notificação seção tooset as configurações básicas para seu envio, incluindo: Olá título da saudação Push, mensagem de saudação, uma imagem no aplicativo, ou se ele for dispensáveis.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-179">You can use hello Notification section tooset basic settings for your push including: hello title of hello Push, hello message, an in-app image, or if it is dismissible.</span></span> <span data-ttu-id="b6cf3-180">Muitas configurações de notificação são toohello específicas à plataforma do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-180">Many notification settings are specific toohello platform of your device.</span></span> <span data-ttu-id="b6cf3-181">Você pode selecionar se o envio por push será feito “no aplicativo” ou “fora do aplicativo” ou ambos.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-181">You can select whether your push will be sent "in app" or "out of app" or both.</span></span> <span data-ttu-id="b6cf3-182">(Lembre-se de que os usuários podem "aceitar" ou "recusar" de "fora do aplicativo" envia no sistema operacional de saudação nível em seus dispositivos e do Azure Mobile Engagement não poderá ser capaz de toooverride essa configuração.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-182">(Remember that users can "opt-in" or "opt-out" of "out of app" Pushes at hello Operating System level on their devices, and Azure Mobile Engagement will not be able toooverride this setting.</span></span> <span data-ttu-id="b6cf3-183">Também Lembre-se de que trata de API de alcance hello "no aplicativo" e "fora do aplicativo" envia.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-183">Also remember that hello Reach API handles "in app" and "out of app" Pushes.</span></span> <span data-ttu-id="b6cf3-184">Olá Push API pode ser usado toohandle "fora do aplicativo" leva muito). Envios por push podem ser personalizados com imagens ou conteúdo HTML, incluindo links profundos para vinculação fora de seu local de aplicativo ou tooanother em seu aplicativo (SDK do Android 2.1.0 ou posteriores categorias intenção necessárias).</span><span class="sxs-lookup"><span data-stu-id="b6cf3-184">hello Push API can be used toohandle "out of app" pushes too.) Pushes can be customized with pictures or HTML content, including deep links for linking outside of your App or tooanother location in your App (Android SDK 2.1.0 or later intent categories required).</span></span> <span data-ttu-id="b6cf3-185">Você pode alterar a notificação de ícone ou iOS hello e enviar o conteúdo da web ou de texto (um pop-up com html, URL link tooanother local de conteúdo dentro ou fora do aplicativo hello).</span><span class="sxs-lookup"><span data-stu-id="b6cf3-185">You can change hello icon or iOS badge, and send either text or web content (a popup with html content, URL link tooanother location either inside or outside of hello app).</span></span> <span data-ttu-id="b6cf3-186">Você também pode fazer o anel de dispositivos com Android ou Vibrar com hello por Push.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-186">You can also make Android devices ring or vibrate with hello Push.</span></span> <span data-ttu-id="b6cf3-187">(Lembre-se de que você será necessário Olá correto permissões SDK em seu Android tooring do arquivo de manifesto ou Vibrar um dispositivo.) Atualmente, não há nenhum padrão no setor para tamanhos de “Foto Grande" do Android, haja visto que os tamanhos das telas são diferentes em cada dispositivo, porém imagens de 400 x 100 funciona bem em quase todos os tamanhos de tela.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-187">(Remember that you will need hello correct SDK permissions in your Android manifest file tooring or vibrate a device.) There is currently no industry standard for Android "Big Picture" sizes, since screen sizes are different on every device, but 400x100 pictures work on almost any screen size.</span></span>

### <a name="delivery-types"></a><span data-ttu-id="b6cf3-188">Tipos de entrega:</span><span class="sxs-lookup"><span data-stu-id="b6cf3-188">Delivery Types:</span></span>
* <span data-ttu-id="b6cf3-189">Somente fora do aplicativo: Olá notificação será enviada ao usuário Olá não usa o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-189">Out of app only: hello notification will be delivered when hello user does not use hello application.</span></span>
* <span data-ttu-id="b6cf3-190">Olá sem notificação somente de aplicativo requer um certificado da Apple ou do Google (certificado APNS ou GCM).</span><span class="sxs-lookup"><span data-stu-id="b6cf3-190">hello out of app only notification requires a certificate from Apple or Google (APNS or GCM certificate).</span></span>
* <span data-ttu-id="b6cf3-191">No aplicativo somente: notificação de saudação aparece apenas quando o aplicativo hello está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-191">In-app only: hello notification appears only when hello application is running.</span></span>
* <span data-ttu-id="b6cf3-192">notificação de saudação usa Olá Capptain entrega tooreach Olá de usuário do sistema.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-192">hello notification uses hello Capptain delivery system tooreach hello user.</span></span> <span data-ttu-id="b6cf3-193">Totalmente, você pode personalizar layout/exibição Olá visual de seu envio.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-193">You can fully customize hello visual layout/display of your push.</span></span>
* <span data-ttu-id="b6cf3-194">A qualquer momento: Essa opção garante que você enviar uma notificação que o aplicativo hello está em execução ou não.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-194">Anytime: This option ensures that you send a notification either hello application is running or not.</span></span>

![Reach-Campaign4][23]

### <a name="option-applies-to"></a><span data-ttu-id="b6cf3-196">As Opções se Aplicam a:</span><span class="sxs-lookup"><span data-stu-id="b6cf3-196">Option Applies to:</span></span>
* <span data-ttu-id="b6cf3-197">Notificação: anúncios, pesquisas</span><span class="sxs-lookup"><span data-stu-id="b6cf3-197">Notification:     Announcements, Polls</span></span>

## <a name="content"></a><span data-ttu-id="b6cf3-198">Conteúdo</span><span class="sxs-lookup"><span data-stu-id="b6cf3-198">Content</span></span>
<span data-ttu-id="b6cf3-199">Você pode usar o conteúdo de saudação de toomodify Olá seção de conteúdo de anúncios, votações, envia dados e blocos (somente no Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="b6cf3-199">You can use hello Content section toomodify hello content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span> <span data-ttu-id="b6cf3-200">configuração de conteúdo de saudação de campanhas de Push é toohello específico de tipo de campanha.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-200">hello Content setting of Push campaigns is specific toohello type of campaign.</span></span> 

### <a name="see-also"></a><span data-ttu-id="b6cf3-201">Consulte também</span><span class="sxs-lookup"><span data-stu-id="b6cf3-201">See also</span></span>
* <span data-ttu-id="b6cf3-202">[Documentação da Interface do Usuário ‑ Alcance ‑ Enviar conteúdo por push][Link 29]</span><span class="sxs-lookup"><span data-stu-id="b6cf3-202">[UI Documentation - Reach - Push Content][Link 29]</span></span>

![Reach-Campaign5][24]

## <a name="audience"></a><span data-ttu-id="b6cf3-204">Público-alvo</span><span class="sxs-lookup"><span data-stu-id="b6cf3-204">Audience</span></span>
<span data-ttu-id="b6cf3-205">Você pode usar o hello público seção toodefine uma lista padrão de itens toolimit sua campanha ou limites de sua campanha com base em critérios personalizados.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-205">You can use hello Audience section toodefine a standard list of items toolimit your campaign or limits your campaign based on customized criteria.</span></span> <span data-ttu-id="b6cf3-206">conjunto padrão de saudação de opções tooLimit seu público-alvo permite toopush tooeither novo ou antigo usuários ou somente usuários de envio por push nativo.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-206">hello standard set of options tooLimit your Audience allows you toopush tooeither new or old users or native push users only.</span></span> <span data-ttu-id="b6cf3-207">Você também pode definir um número de saudação toolimit cota de usuários que recebem o envio de saudação.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-207">You can also set a quota toolimit hello number of users who receive hello push.</span></span> <span data-ttu-id="b6cf3-208">Você pode editar manualmente a expressão hello como sua campanha é filtrado tooinclude um ou mais usuários tootarget de critério.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-208">You can manually Edit hello expression for how your campaign is filtered tooinclude one or more criterion tootarget users.</span></span> <span data-ttu-id="b6cf3-209">Você pode digitar manualmente uma expressão de público-alvo.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-209">You can manually type an audience expression.</span></span> <span data-ttu-id="b6cf3-210">Essa expressão deve definir explicitamente uma relação entre a critérios Olá.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-210">Such an expression must explicitly define hello relation between criteria.</span></span> <span data-ttu-id="b6cf3-211">Um critério é descrito por um identificador que deve começar com uma letra maiúscula e não pode conter espaços.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-211">A criterion is described by an identifier that must start with a capital letter and cannot contain spaces.</span></span> <span data-ttu-id="b6cf3-212">uma relação entre a critérios Olá Olá pode ser descrita usando 'e', 'ou', 'not' operadores, bem como '(',')'.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-212">hello relation between hello criteria can be described using 'and', 'or', 'not' operators as well as '(', ')'.</span></span> <span data-ttu-id="b6cf3-213">Exemplo: "Critérion1 ou (Critérion1 e não Critérion2)".</span><span class="sxs-lookup"><span data-stu-id="b6cf3-213">Example: "Criterion1 or (Criterion1 and not Criterion2)".</span></span>

> [!NOTE]
> <span data-ttu-id="b6cf3-214">Com um grande público incluído em campanhas, Olá servidor direcionamento do lado do verificação pode ser lento, especialmente se você tentar toostart várias campanhas em Olá mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-214">With a large audience included in campaigns, hello server side targeting scan can be slow, especially if you attempt toostart multiple campaigns at hello same time.</span></span>

* <span data-ttu-id="b6cf3-215">Se possível, só inicie uma campanha por vez.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-215">If possible, only start one campaign at a time.</span></span>
* <span data-ttu-id="b6cf3-216">No máximo, Olá apenas iniciar quatro campanhas de cada vez.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-216">At hello most, only start four campaigns at a time.</span></span>
* <span data-ttu-id="b6cf3-217">Enviar por push apenas usuários ativos tooyour (caixa de seleção "envolver somente usuários que podem ser alcançados usando Push nativo" e "Envolver apenas usuários ativos") para que somente os usuários que ainda têm o aplicativo hello instalado e usá-lo precisará toobe verificado.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-217">Push only tooyour active users (checkbox "Engage only users who can be reached using Native Push" and "Engage only active users") so that only your users who still have hello app installed and use it will need toobe scanned.</span></span>
  <span data-ttu-id="b6cf3-218">Quando seu público-alvo é definido, você pode usar o hello simular toofind botão out quantos usuários receberão esse envio.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-218">Once your audience is defined, you can use hello simulate button toofind out how many users will receive this Push.</span></span> <span data-ttu-id="b6cf3-219">Isso será calcula o número de saudação de usuários conhecidos potencialmente direcionados por esse público-alvo (essa é uma estimativa com base em uma amostra aleatória de usuários).</span><span class="sxs-lookup"><span data-stu-id="b6cf3-219">This will compute hello number of known users potentially targeted by this audience (this is an estimate based on a random sample of users).</span></span> <span data-ttu-id="b6cf3-220">Lembre-se de que os usuários que tenham desinstalado o aplicativo hello também fazem parte desse público, mas não podem ser alcançados.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-220">Be aware that users who have uninstalled hello application are also part of this audience, but cannot be reached.</span></span>

### <a name="see-also"></a><span data-ttu-id="b6cf3-221">Consulte também</span><span class="sxs-lookup"><span data-stu-id="b6cf3-221">See also</span></span>
* <span data-ttu-id="b6cf3-222">[Documentação da interface do usuário – Alcance – Novo Critério de Envio por Push][Link 28]</span><span class="sxs-lookup"><span data-stu-id="b6cf3-222">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

![Reach-Campaign6][25]

### <a name="edit-expression"></a><span data-ttu-id="b6cf3-224">Editar expressão</span><span class="sxs-lookup"><span data-stu-id="b6cf3-224">Edit expression</span></span>
![Reach-Campaign7][26]

### <a name="limit-your-audience-option-applies-to"></a><span data-ttu-id="b6cf3-226">A opção para limitar seu público-alvo se aplica a:</span><span class="sxs-lookup"><span data-stu-id="b6cf3-226">Limit your audience option applies to:</span></span>
* <span data-ttu-id="b6cf3-227">Envolver somente um subconjunto de usuários: todos (Anúncios, Pesquisas, Envios de dados por push, Blocos)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-227">Engage only a subset of users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="b6cf3-228">Envolver apenas usuários antigos: todos (Anúncios, Pesquisas, Envios de dados por push, Blocos)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-228">Engage only old users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="b6cf3-229">Envolver apenas usuários novos: todos (Anúncios, Pesquisas, Envios de dados por push, Blocos)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-229">Engage only new users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="b6cf3-230">Envolver apenas usuários inativos: anúncios, pesquisas, blocos</span><span class="sxs-lookup"><span data-stu-id="b6cf3-230">Engage only idle users:    Announcements, Polls, Tiles</span></span>
* <span data-ttu-id="b6cf3-231">Envolver apenas usuários ativos: todos (Anúncios, Pesquisas, Envios de dados por push, Blocos)</span><span class="sxs-lookup"><span data-stu-id="b6cf3-231">Engage only active users:    All (Announcements, Polls, Data Pushes, Tiles)</span></span>
* <span data-ttu-id="b6cf3-232">Envolver apenas os usuários que podem ser alcançados usando Push Nativo: anúncios, pesquisas</span><span class="sxs-lookup"><span data-stu-id="b6cf3-232">Engage only users who can be reached using Native Push:     Announcements, Polls</span></span>

## <a name="time-frame"></a><span data-ttu-id="b6cf3-233">Período</span><span class="sxs-lookup"><span data-stu-id="b6cf3-233">Time Frame</span></span>
<span data-ttu-id="b6cf3-234">Você pode usar o hello período seção tooset quando Olá push será enviado ou você pode deixar a campanha de Olá Olá período de tempo em branco toostart imediatamente.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-234">You can use hello Time Frame section tooset when hello push will be sent or you can leave hello time frame blank toostart hello campaign immediately.</span></span> <span data-ttu-id="b6cf3-235">Lembre-se de que usar o fuso horário de usuários finais da saudação pode iniciar campanha Olá um dia antes do que esperar para seus usuários finais na Ásia e enviem lotes pequenos de avanços cada vez até que todos os fusos horários no período de tempo de saudação do hello world correspondência definida para sua campanha.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-235">Remember that using hello end-users' time zone may start hello campaign a day earlier than you expect for your end-users in Asia and send small batches of pushes at a time until all time zones in hello world match hello time frame set for your campaign.</span></span> <span data-ttu-id="b6cf3-236">Usar o fuso horário Olá dos usuários finais também pode causar atrasos em campanhas porque ele tem tempo de saudação toorequest de telefone de saudação antes de iniciar o envio de saudação.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-236">Using hello end users' time zone can also cause delays in campaigns since it has toorequest hello time from hello phone before starting hello push.</span></span>

> [!NOTE]
> <span data-ttu-id="b6cf3-237">Campanhas sem uma data de término podem armazenar localmente em cachês de envios e ainda exibi-los após as suas campanhas completas manualmente.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-237">Campaigns without an end date can cache pushes locally and still display them after you manually complete campaigns.</span></span> <span data-ttu-id="b6cf3-238">tooavoid esse comportamento, específica de uma hora de término para campanhas.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-238">tooavoid this behavior, specific an end time for campaigns.</span></span>

### <a name="see-also"></a><span data-ttu-id="b6cf3-239">Consulte também</span><span class="sxs-lookup"><span data-stu-id="b6cf3-239">See also</span></span>
* <span data-ttu-id="b6cf3-240">[Alcance ‑ Instruções – Agendamento][Link 3]</span><span class="sxs-lookup"><span data-stu-id="b6cf3-240">[Reach - How Tos – Scheduling][Link 3]</span></span> 

![Reach-Campaign8][27]

### <a name="settings-apply-to"></a><span data-ttu-id="b6cf3-242">As configurações se aplicam a:</span><span class="sxs-lookup"><span data-stu-id="b6cf3-242">Settings Apply to:</span></span>
* <span data-ttu-id="b6cf3-243">Período: anúncios, pesquisas, blocos</span><span class="sxs-lookup"><span data-stu-id="b6cf3-243">Time frame:     Announcements, Polls, Tiles</span></span>

## <a name="test"></a><span data-ttu-id="b6cf3-244">Teste</span><span class="sxs-lookup"><span data-stu-id="b6cf3-244">Test</span></span>
<span data-ttu-id="b6cf3-245">Você pode usar o hello teste seção toosend este dispositivo do push tooyour próprio teste antes de salvar campanha hello.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-245">You can use hello Test section toosend this push tooyour own test device before saving hello campaign.</span></span> <span data-ttu-id="b6cf3-246">Se você tiver configurado qualquer idiomas personalizados para essa campanha, você pode testar o envio de saudação em cada idioma.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-246">If you have configured any custom languages for this campaign, you can test hello push in each language.</span></span> <span data-ttu-id="b6cf3-247">Você pode configurar um dispositivo de teste para "Minha Conta".</span><span class="sxs-lookup"><span data-stu-id="b6cf3-247">You can setup a test device from “My Account”.</span></span>

> [!NOTE]
> <span data-ttu-id="b6cf3-248">Nenhum lado servidor dados são registrados quando você usar o botão de saudação muito "testar" envia, somente os dados serão registrados para campanhas de push real.</span><span class="sxs-lookup"><span data-stu-id="b6cf3-248">No server side data is logged when you use hello button too"test" pushes, data is only logged for real push campaigns.</span></span>

### <a name="see-also"></a><span data-ttu-id="b6cf3-249">Consulte também</span><span class="sxs-lookup"><span data-stu-id="b6cf3-249">See also</span></span>
* <span data-ttu-id="b6cf3-250">[Documentação da Interface do Usuário ‑ Minha Conta][Link 14]</span><span class="sxs-lookup"><span data-stu-id="b6cf3-250">[UI Documentation - My Account][Link 14]</span></span>

![Reach-Campaign9][28]

<!--Image references-->
[1]: ./media/mobile-engagement-user-interface-navigation/navigation1.png
[2]: ./media/mobile-engagement-user-interface-home/home1.png
[3]: ./media/mobile-engagement-user-interface-home/home2.png
[4]: ./media/mobile-engagement-user-interface-home/home3.png
[5]: ./media/mobile-engagement-user-interface-home/home4.png
[6]: ./media/mobile-engagement-user-interface-home/home5.png
[7]: ./media/mobile-engagement-user-interface-my-account/myaccount1.png
[8]: ./media/mobile-engagement-user-interface-my-account/myaccount2.png
[9]: ./media/mobile-engagement-user-interface-my-account/myaccount3.png
[10]: ./media/mobile-engagement-user-interface-analytics/analytics1.png
[11]: ./media/mobile-engagement-user-interface-analytics/analytics2.png
[12]: ./media/mobile-engagement-user-interface-analytics/analytics3.png
[13]: ./media/mobile-engagement-user-interface-analytics/analytics4.png
[14]: ./media/mobile-engagement-user-interface-monitor/monitor1.png
[15]: ./media/mobile-engagement-user-interface-monitor/monitor2.png
[16]: ./media/mobile-engagement-user-interface-monitor/monitor3.png
[17]: ./media/mobile-engagement-user-interface-monitor/monitor4.png
[18]: ./media/mobile-engagement-user-interface-reach/reach1.png
[19]: ./media/mobile-engagement-user-interface-reach/reach2.png
[20]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign1.png
[21]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign2.png
[22]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign3.png
[23]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign4.png
[24]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign5.png
[25]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign6.png
[26]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign7.png
[27]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign8.png
[28]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign9.png
[29]: ./media/mobile-engagement-user-interface-reach-criterion/Reach-Criterion1.png
[30]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content1.png
[31]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content2.png
[32]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content3.png
[33]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content4.png
[34]: ./media/mobile-engagement-user-interface-dashboard/dashboard1.png
[35]: ./media/mobile-engagement-user-interface-segments/segments1.png
[36]: ./media/mobile-engagement-user-interface-segments/segments2.png
[37]: ./media/mobile-engagement-user-interface-segments/segments3.png
[38]: ./media/mobile-engagement-user-interface-segments/segments4.png
[39]: ./media/mobile-engagement-user-interface-segments/segments5.png
[40]: ./media/mobile-engagement-user-interface-segments/segments6.png
[41]: ./media/mobile-engagement-user-interface-segments/segments7.png
[42]: ./media/mobile-engagement-user-interface-segments/segments8.png
[43]: ./media/mobile-engagement-user-interface-segments/segments9.png
[44]: ./media/mobile-engagement-user-interface-segments/segments10.png
[45]: ./media/mobile-engagement-user-interface-segments/segments11.png
[46]: ./media/mobile-engagement-user-interface-settings/settings1.png
[47]: ./media/mobile-engagement-user-interface-settings/settings2.png
[48]: ./media/mobile-engagement-user-interface-settings/settings3.png
[49]: ./media/mobile-engagement-user-interface-settings/settings4.png
[50]: ./media/mobile-engagement-user-interface-settings/settings5.png
[51]: ./media/mobile-engagement-user-interface-settings/settings6.png
[52]: ./media/mobile-engagement-user-interface-settings/settings7.png
[53]: ./media/mobile-engagement-user-interface-settings/settings8.png
[54]: ./media/mobile-engagement-user-interface-settings/settings9.png
[55]: ./media/mobile-engagement-user-interface-settings/settings10.png
[56]: ./media/mobile-engagement-user-interface-settings/settings11.png
[57]: ./media/mobile-engagement-user-interface-settings/settings12.png
[58]: ./media/mobile-engagement-user-interface-settings/settings13.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

