---
title: "aaaAzure Interface de usuário do Mobile Engagement - acessar conteúdo"
description: "Saiba como o conteúdo de exclusivo Olá toomanage de tipos diferentes de saudação de notificação por push campanhas no Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: add64f06-43c9-475c-8722-51cd00bb844b
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: de389eb4368d986ef00135036c26e26a2464663e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-hello-unique-content-of-hello-different-types-of-push-notification-campaigns"></a><span data-ttu-id="809b2-103">Como toomanage Olá conteúdo exclusivo de tipos diferentes de saudação de campanhas de notificação por push</span><span class="sxs-lookup"><span data-stu-id="809b2-103">How toomanage hello unique content of hello different types of push notification campaigns</span></span>
<span data-ttu-id="809b2-104">Você pode usar a seção de conteúdo de saudação de um novo contato campanha toomodify Olá conteúdo de anúncios, votações, envia dados e blocos (somente no Windows Phone).</span><span class="sxs-lookup"><span data-stu-id="809b2-104">You can use hello Content section of a new reach campaign toomodify hello content of your Announcements, Polls, Data Pushes, and Tiles (Windows Phone only).</span></span> <span data-ttu-id="809b2-105">configuração de conteúdo de saudação de campanhas de Push é toohello específico de tipo de campanha.</span><span class="sxs-lookup"><span data-stu-id="809b2-105">hello content setting of Push campaigns is specific toohello type of campaign.</span></span> 

### <a name="content-types"></a><span data-ttu-id="809b2-106">Tipos de conteúdo:</span><span class="sxs-lookup"><span data-stu-id="809b2-106">Content types:</span></span>
* <span data-ttu-id="809b2-107">Anúncios</span><span class="sxs-lookup"><span data-stu-id="809b2-107">Announcements</span></span>
* <span data-ttu-id="809b2-108">Pesquisas</span><span class="sxs-lookup"><span data-stu-id="809b2-108">Polls</span></span>
* <span data-ttu-id="809b2-109">Envios de dados por push</span><span class="sxs-lookup"><span data-stu-id="809b2-109">Data pushes</span></span>
* <span data-ttu-id="809b2-110">Blocos (apenas no Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="809b2-110">Tiles (Windows Phone Only)</span></span>

## <a name="content-of-announcements"></a><span data-ttu-id="809b2-111">Conteúdo de anúncios</span><span class="sxs-lookup"><span data-stu-id="809b2-111">Content of Announcements</span></span>
 ![Reach-Content1][30] 

### <a name="choose-hello-type-of-your-announcement"></a><span data-ttu-id="809b2-113">Escolha o tipo de saudação da notificação:</span><span class="sxs-lookup"><span data-stu-id="809b2-113">Choose hello type of your announcement:</span></span>
* <span data-ttu-id="809b2-114">Somente notificação: é uma notificação simples padrão.</span><span class="sxs-lookup"><span data-stu-id="809b2-114">Notification only: It is a simple standard notification.</span></span> <span data-ttu-id="809b2-115">Isso significa que se um usuário clica nela, nenhuma exibição adicional será exibida, mas somente a ação de saudação associados tooit ocorrerá.</span><span class="sxs-lookup"><span data-stu-id="809b2-115">Meaning that if a user clicks on it, no additional view will appear, but only hello action associated tooit will occur.</span></span>
* <span data-ttu-id="809b2-116">Anúncio de texto: é uma notificação que envolva Olá usuário toohave uma olhada em uma exibição de texto.</span><span class="sxs-lookup"><span data-stu-id="809b2-116">Text announcement: It is a notification that engages hello user toohave a look at a text view.</span></span>
* <span data-ttu-id="809b2-117">Anúncio da Web: é uma notificação que envolva Olá usuário toohave uma olhada em uma exibição da web.</span><span class="sxs-lookup"><span data-stu-id="809b2-117">Web announcement: It is a notification that engages hello user toohave a look at a web view.</span></span>

### <a name="see-also"></a><span data-ttu-id="809b2-118">Consulte também</span><span class="sxs-lookup"><span data-stu-id="809b2-118">See also</span></span>
* <span data-ttu-id="809b2-119">[Alcance ‑ Instruções ‑ Anúncios][Link 3]</span><span class="sxs-lookup"><span data-stu-id="809b2-119">[Reach - How Tos - Announcements][Link 3]</span></span> 

### <a name="about-web-view-announcements"></a><span data-ttu-id="809b2-120">Sobre os anúncios de exibição na Web:</span><span class="sxs-lookup"><span data-stu-id="809b2-120">About Web View Announcements:</span></span>
<span data-ttu-id="809b2-121">Ocorrências do padrão de hello "{deviceid}" no código HTML da saudação ou código JavaScript fornecidos aqui serão automaticamente substituídas pelo identificador de saudação do dispositivo Olá exibindo comunicado hello.</span><span class="sxs-lookup"><span data-stu-id="809b2-121">Occurrences of hello pattern "{deviceid}" in hello HTML code or JavaScript code you provide here will be automatically replaced by hello identifier of hello device displaying hello announcement.</span></span> <span data-ttu-id="809b2-122">Este é um identificadores de dispositivo do modo fácil tooretrieve do Azure Mobile Engagement em externo web serviço hospedado em seu back office.</span><span class="sxs-lookup"><span data-stu-id="809b2-122">This is an easy way tooretrieve Azure Mobile Engagement device identifiers in an external web service hosted on your back office.</span></span>
<span data-ttu-id="809b2-123">Se você quiser toocreate uma completa da tela (sem saudação padrão botões ação e sair fornecemos) no modo de exibição web você pode usar o hello funções a seguir do código de JavaScript do anúncio de exibição da web:</span><span class="sxs-lookup"><span data-stu-id="809b2-123">If you want toocreate a full screen web view (without hello default Action and Exit buttons we provide) you can use hello following functions from your web view announcement's JavaScript code:</span></span> 

* <span data-ttu-id="809b2-124">executar ação da notificação Olá: ReachContent.actionContent()</span><span class="sxs-lookup"><span data-stu-id="809b2-124">perform hello announcement action: ReachContent.actionContent()</span></span>
* <span data-ttu-id="809b2-125">sair do anúncio de saudação: ReachContent.exitContent()</span><span class="sxs-lookup"><span data-stu-id="809b2-125">exit from hello announcement: ReachContent.exitContent()</span></span>

### <a name="choose-your-action"></a><span data-ttu-id="809b2-126">Escolha a ação:</span><span class="sxs-lookup"><span data-stu-id="809b2-126">Choose your Action:</span></span>
### <a name="about-action-urls"></a><span data-ttu-id="809b2-127">Sobre as URLs de ação:</span><span class="sxs-lookup"><span data-stu-id="809b2-127">About Action URLs:</span></span>
<span data-ttu-id="809b2-128">Qualquer URL que possa ser interpretada pelo sistema operacional de destino do dispositivo pode ser usada como uma URL de ação.</span><span class="sxs-lookup"><span data-stu-id="809b2-128">Any URL that can be interpreted by a targeted device's operating system can be used as an action URL.</span></span>
<span data-ttu-id="809b2-129">Qualquer URL dedicada que seu aplicativo pode suporte (por exemplo, os usuários toomake saltar tooa determinada tela) também pode ser usado como uma URL de ação.</span><span class="sxs-lookup"><span data-stu-id="809b2-129">Any dedicated URL that your application might support (e.g. toomake users jump tooa particular screen) can also be used as an action URL.</span></span>
<span data-ttu-id="809b2-130">Cada ocorrência do padrão de Olá {deviceid} é substituída automaticamente pelo identificador de saudação do dispositivo Olá executar ação hello.</span><span class="sxs-lookup"><span data-stu-id="809b2-130">Each occurrence of hello {deviceid} pattern is automatically replaced by hello identifier of hello device performing hello action.</span></span> <span data-ttu-id="809b2-131">Isso pode ser usado tooeasily recuperar identificadores de dispositivo do Azure Mobile Engagement por meio de um serviço web externo hospedado em seu back office.</span><span class="sxs-lookup"><span data-stu-id="809b2-131">This can be used tooeasily retrieve Azure Mobile Engagement device identifiers via an external web service hosted on your back office.</span></span>

* <span data-ttu-id="809b2-132">**Ações do Android + iOS**</span><span class="sxs-lookup"><span data-stu-id="809b2-132">**Android + iOS actions**</span></span>
  * <span data-ttu-id="809b2-133">Abrir uma página Web</span><span class="sxs-lookup"><span data-stu-id="809b2-133">Open a web page</span></span>
  * <span data-ttu-id="809b2-134">http://\[web-site-domain\]</span><span class="sxs-lookup"><span data-stu-id="809b2-134">http://\[web-site-domain\]</span></span> 
  * <span data-ttu-id="809b2-135">Exemplo:http://www.azure.com</span><span class="sxs-lookup"><span data-stu-id="809b2-135">Example:http://www.azure.com</span></span>
  * <span data-ttu-id="809b2-136">Enviar um email</span><span class="sxs-lookup"><span data-stu-id="809b2-136">Send an e-mail</span></span>
  * <span data-ttu-id="809b2-137">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span><span class="sxs-lookup"><span data-stu-id="809b2-137">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span></span> 
  * <span data-ttu-id="809b2-138">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span><span class="sxs-lookup"><span data-stu-id="809b2-138">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span></span>
  * <span data-ttu-id="809b2-139">Enviar um SMS</span><span class="sxs-lookup"><span data-stu-id="809b2-139">Send a SMS</span></span>
  * <span data-ttu-id="809b2-140">sms:\[número-de-telefone\]</span><span class="sxs-lookup"><span data-stu-id="809b2-140">sms:\[phone-number\]</span></span> 
  * <span data-ttu-id="809b2-141">Exemplo:sms:2125551212</span><span class="sxs-lookup"><span data-stu-id="809b2-141">Example:sms:2125551212</span></span>
  * <span data-ttu-id="809b2-142">Discar um número de telefone</span><span class="sxs-lookup"><span data-stu-id="809b2-142">Dial a phone number</span></span>
  * <span data-ttu-id="809b2-143">tel:\[número-de-telefone\]</span><span class="sxs-lookup"><span data-stu-id="809b2-143">tel:\[phone-number\]</span></span> 
  * <span data-ttu-id="809b2-144">Exemplo:tel:2125551212</span><span class="sxs-lookup"><span data-stu-id="809b2-144">Example:tel:2125551212</span></span>
* <span data-ttu-id="809b2-145">**Somente ações do Android**</span><span class="sxs-lookup"><span data-stu-id="809b2-145">**Android only actions**</span></span>
  * <span data-ttu-id="809b2-146">Baixar um aplicativo hello Play Store</span><span class="sxs-lookup"><span data-stu-id="809b2-146">Download an application on hello Play Store</span></span>
  * <span data-ttu-id="809b2-147">market://details?id=\[app package\]</span><span class="sxs-lookup"><span data-stu-id="809b2-147">market://details?id=\[app package\]</span></span> 
  * <span data-ttu-id="809b2-148">Exemplo:market://details?id=com.microsoft.office.word</span><span class="sxs-lookup"><span data-stu-id="809b2-148">Example:market://details?id=com.microsoft.office.word</span></span>
  * <span data-ttu-id="809b2-149">Iniciar uma pesquisa localizada geograficamente</span><span class="sxs-lookup"><span data-stu-id="809b2-149">Start a geo-localized search</span></span>
  * <span data-ttu-id="809b2-150">geo:0,0?q=\[search query\]</span><span class="sxs-lookup"><span data-stu-id="809b2-150">geo:0,0?q=\[search query\]</span></span> 
  * <span data-ttu-id="809b2-151">Exemplo:geo:0,0?q=starbucks,paris</span><span class="sxs-lookup"><span data-stu-id="809b2-151">Example:geo:0,0?q=starbucks,paris</span></span>
* <span data-ttu-id="809b2-152">**Somente ações do iOS**</span><span class="sxs-lookup"><span data-stu-id="809b2-152">**iOS only actions**</span></span>
  * <span data-ttu-id="809b2-153">Baixar um aplicativo hello App Store</span><span class="sxs-lookup"><span data-stu-id="809b2-153">Download an application on hello App Store</span></span>
  * <span data-ttu-id="809b2-154">http://itunes.apple.com/[country]/app/[app name]/id[app id]?mt=8</span><span class="sxs-lookup"><span data-stu-id="809b2-154">http://itunes.apple.com/[country]/app/[app name]/id[app id]?mt=8</span></span> 
  * <span data-ttu-id="809b2-155">Exemplo:http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8</span><span class="sxs-lookup"><span data-stu-id="809b2-155">Example:http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8</span></span>
  * <span data-ttu-id="809b2-156">Ações do Windows</span><span class="sxs-lookup"><span data-stu-id="809b2-156">Windows Actions</span></span>
  * <span data-ttu-id="809b2-157">Abrir uma página Web</span><span class="sxs-lookup"><span data-stu-id="809b2-157">Open a web page</span></span>
  * <span data-ttu-id="809b2-158">http://\[web-site-domain\]</span><span class="sxs-lookup"><span data-stu-id="809b2-158">http://\[web-site-domain\]</span></span> 
  * <span data-ttu-id="809b2-159">Exemplo:http://www.azure.com</span><span class="sxs-lookup"><span data-stu-id="809b2-159">Example:http://www.azure.com</span></span>
  * <span data-ttu-id="809b2-160">Enviar um email</span><span class="sxs-lookup"><span data-stu-id="809b2-160">Send an e-mail</span></span>
  * <span data-ttu-id="809b2-161">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span><span class="sxs-lookup"><span data-stu-id="809b2-161">mailto:\[e-mail-recipient\]?subject=\[subject\]&body=\[message\]</span></span> 
  * <span data-ttu-id="809b2-162">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span><span class="sxs-lookup"><span data-stu-id="809b2-162">Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&body=Good%20stuff!</span></span>
  * <span data-ttu-id="809b2-163">Enviar um SMS (necessário o aplicativo da Skype Store)</span><span class="sxs-lookup"><span data-stu-id="809b2-163">Send a SMS (Skype Store App required)</span></span>
  * <span data-ttu-id="809b2-164">sms:\[número-de-telefone\]</span><span class="sxs-lookup"><span data-stu-id="809b2-164">sms:\[phone-number\]</span></span> 
  * <span data-ttu-id="809b2-165">Exemplo:sms:2125551212</span><span class="sxs-lookup"><span data-stu-id="809b2-165">Example:sms:2125551212</span></span>
  * <span data-ttu-id="809b2-166">Discar um número de telefone (necessário o aplicativo da Skype Store)</span><span class="sxs-lookup"><span data-stu-id="809b2-166">Dial a phone number (Skype Store App required)</span></span>
  * <span data-ttu-id="809b2-167">tel:\[número-de-telefone\]</span><span class="sxs-lookup"><span data-stu-id="809b2-167">tel:\[phone-number\]</span></span> 
  * <span data-ttu-id="809b2-168">Exemplo:tel:2125551212</span><span class="sxs-lookup"><span data-stu-id="809b2-168">Example:tel:2125551212</span></span>
  * <span data-ttu-id="809b2-169">Baixar um aplicativo hello Play Store</span><span class="sxs-lookup"><span data-stu-id="809b2-169">Download an application on hello Play Store</span></span>
  * <span data-ttu-id="809b2-170">ms-windows-store:PDP?PFN=\[app package ID\]</span><span class="sxs-lookup"><span data-stu-id="809b2-170">ms-windows-store:PDP?PFN=\[app package ID\]</span></span> 
  * <span data-ttu-id="809b2-171">Exemplo: ms-windows-store:PDP?PFN=4d91298a-07cb-40fb-aecc-4cb5615d53c1</span><span class="sxs-lookup"><span data-stu-id="809b2-171">Example:ms-windows-store:PDP?PFN=4d91298a-07cb-40fb-aecc-4cb5615d53c1</span></span>
  * <span data-ttu-id="809b2-172">Iniciar uma pesquisa do Bing Mapas</span><span class="sxs-lookup"><span data-stu-id="809b2-172">Start a bingmaps search</span></span>
  * <span data-ttu-id="809b2-173">bingmaps:?q=\[consulta de pesquisa\]</span><span class="sxs-lookup"><span data-stu-id="809b2-173">bingmaps:?q=\[search query\]</span></span> 
  * <span data-ttu-id="809b2-174">Exemplo:bingmaps:? q=starbucks,paris</span><span class="sxs-lookup"><span data-stu-id="809b2-174">Example:bingmaps:?q=starbucks,paris</span></span>
  * <span data-ttu-id="809b2-175">Usar um esquema personalizado</span><span class="sxs-lookup"><span data-stu-id="809b2-175">Use a custom scheme</span></span>
  * <span data-ttu-id="809b2-176">\[esquema personalizado\]://\[parâmetros do esquema personalizado\]</span><span class="sxs-lookup"><span data-stu-id="809b2-176">\[custom scheme\]://\[custom scheme params\]</span></span> 
  * <span data-ttu-id="809b2-177">Exemplo:myCustomProtocol://myCustomParams</span><span class="sxs-lookup"><span data-stu-id="809b2-177">Example:myCustomProtocol://myCustomParams</span></span>
  * <span data-ttu-id="809b2-178">Usar um pacote de dados (necessário o aplicativo da Store para leitura de extensão)</span><span class="sxs-lookup"><span data-stu-id="809b2-178">Use a package data (Store App for extension read required)</span></span>
  * <span data-ttu-id="809b2-179">\[pasta\]\[dados\].\[extensão\]</span><span class="sxs-lookup"><span data-stu-id="809b2-179">\[folder\]\[data\].\[extension\]</span></span> 
  * <span data-ttu-id="809b2-180">Example:myfolderdata.txt</span><span class="sxs-lookup"><span data-stu-id="809b2-180">Example:myfolderdata.txt</span></span>

### <a name="build-a-tracking-url"></a><span data-ttu-id="809b2-181">Criar uma URL de rastreamento:</span><span class="sxs-lookup"><span data-stu-id="809b2-181">Build a Tracking URL:</span></span>
* <span data-ttu-id="809b2-182">Consulte Olá a seção "Configurações" hello <UI Documentation> para obter instruções sobre como criar uma URL de acompanhamento que permitirá toodownload usuários um de seus outros aplicativos.</span><span class="sxs-lookup"><span data-stu-id="809b2-182">See hello “Settings” section of hello <UI Documentation> for instruction on building a tracking URL that will allow users toodownload one of your other applications.</span></span>

### <a name="define-hello-texts-of-your-announcement"></a><span data-ttu-id="809b2-183">Definir Olá textos da notificação</span><span class="sxs-lookup"><span data-stu-id="809b2-183">Define hello texts of your announcement</span></span>
<span data-ttu-id="809b2-184">Preencha Olá título, conteúdo e textos de botão da notificação.</span><span class="sxs-lookup"><span data-stu-id="809b2-184">Fill in hello title, content, and button texts of your announcement.</span></span> <span data-ttu-id="809b2-185">Você pode direcionar um público-alvo de uma campanha futuras com base nos comentários de alcance Olá de como os usuários responderam toothis campanha.</span><span class="sxs-lookup"><span data-stu-id="809b2-185">You can target an audience of a future campaign based on hello reach feedback of how users responded toothis campaign.</span></span> <span data-ttu-id="809b2-186">Público-alvo pode ser com base nos comentários de saudação do se essa campanha foi apenas enviada, respondidas, acionadas ou encerradas.</span><span class="sxs-lookup"><span data-stu-id="809b2-186">Audience targeting can be based on hello feedback of whether this campaign was just pushed, replied, actioned, or exited.</span></span>

### <a name="see-also"></a><span data-ttu-id="809b2-187">Consulte também</span><span class="sxs-lookup"><span data-stu-id="809b2-187">See also</span></span>
* <span data-ttu-id="809b2-188">[Documentação da interface do usuário – Alcance – Novo Critério de Envio por Push][Link 28]</span><span class="sxs-lookup"><span data-stu-id="809b2-188">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-polls"></a><span data-ttu-id="809b2-189">Conteúdo das pesquisas</span><span class="sxs-lookup"><span data-stu-id="809b2-189">Content of Polls</span></span>
![Reach-Content2][31] 

<span data-ttu-id="809b2-191">Preencha Olá título, descrição e textos de botão da notificação.</span><span class="sxs-lookup"><span data-stu-id="809b2-191">Fill in hello title, description, and button texts of your announcement.</span></span> <span data-ttu-id="809b2-192">Em seguida, adicione perguntas e opções para Olá respostas tooyour perguntas.</span><span class="sxs-lookup"><span data-stu-id="809b2-192">Then, add questions and choices for hello answers tooyour questions.</span></span>
<span data-ttu-id="809b2-193">Você pode direcionar um público-alvo de uma campanha futuras com base nos comentários de alcance Olá de como os usuários responderam toothis campanha.</span><span class="sxs-lookup"><span data-stu-id="809b2-193">You can target an audience of a future campaign based on hello reach feedback of how users responded toothis campaign.</span></span> <span data-ttu-id="809b2-194">O público-alvo direcionado pode ser baseado no fato desta campanha ter sido apenas enviada por push, respondida, acionada ou encerrada.</span><span class="sxs-lookup"><span data-stu-id="809b2-194">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span></span> <span data-ttu-id="809b2-195">Público-alvo também pode ser baseado nos comentários de resposta de sondagem, em que escolha de pergunta e resposta hello são usadas como critérios.</span><span class="sxs-lookup"><span data-stu-id="809b2-195">Audience targeting can also be based on Poll answer feedback, where hello question and answer choice are used as criteria.</span></span>

### <a name="see-also"></a><span data-ttu-id="809b2-196">Consulte também</span><span class="sxs-lookup"><span data-stu-id="809b2-196">See also</span></span>
* <span data-ttu-id="809b2-197">[Documentação da interface do usuário – Alcance – Novo Critério de Envio por Push][Link 28]</span><span class="sxs-lookup"><span data-stu-id="809b2-197">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-data-pushes"></a><span data-ttu-id="809b2-198">Conteúdo de envio de dados por push</span><span class="sxs-lookup"><span data-stu-id="809b2-198">Content of Data Pushes</span></span>
![Reach-Content3][32] 

### <a name="choose-hello-type-of-your-data"></a><span data-ttu-id="809b2-200">Escolha o tipo de saudação de seus dados:</span><span class="sxs-lookup"><span data-stu-id="809b2-200">Choose hello type of your data:</span></span>
* <span data-ttu-id="809b2-201">Texto</span><span class="sxs-lookup"><span data-stu-id="809b2-201">Text</span></span>
* <span data-ttu-id="809b2-202">Dados binários</span><span class="sxs-lookup"><span data-stu-id="809b2-202">Binary data</span></span>
* <span data-ttu-id="809b2-203">Dados Base64</span><span class="sxs-lookup"><span data-stu-id="809b2-203">Base64 data</span></span>

### <a name="define-hello-content-of-your-data"></a><span data-ttu-id="809b2-204">Definir o conteúdo de saudação de seus dados</span><span class="sxs-lookup"><span data-stu-id="809b2-204">Define hello content of your data</span></span>
* <span data-ttu-id="809b2-205">Se você selecionou toopush dados de texto, copie e cole o texto de saudação na caixa "conteúdo" hello.</span><span class="sxs-lookup"><span data-stu-id="809b2-205">If you selected toopush text data, copy and paste hello text into hello "content" box.</span></span>
* <span data-ttu-id="809b2-206">Se você selecionou toopush dados binários ou base64, use tooupload de botão "carregar o arquivo" hello seu arquivo.</span><span class="sxs-lookup"><span data-stu-id="809b2-206">If you selected toopush either binary or base64 data, use hello "upload your file" button tooupload your file.</span></span>
* <span data-ttu-id="809b2-207">Você pode direcionar um público-alvo de uma campanha futuras com base nos comentários de alcance Olá de como os usuários responderam toothis campanha.</span><span class="sxs-lookup"><span data-stu-id="809b2-207">You can target an audience of a future campaign based on hello reach feedback of how users responded toothis campaign.</span></span> <span data-ttu-id="809b2-208">O público-alvo direcionado pode ser baseado no fato desta campanha ter sido apenas enviada por push, respondida, acionada ou encerrada.</span><span class="sxs-lookup"><span data-stu-id="809b2-208">Audience targeting can be based on whether this campaign was just pushed, replied, actioned, or exited.</span></span>

### <a name="see-also"></a><span data-ttu-id="809b2-209">Consulte também</span><span class="sxs-lookup"><span data-stu-id="809b2-209">See also</span></span>
* <span data-ttu-id="809b2-210">[Documentação da interface do usuário – Alcance – Novo Critério de Envio por Push][Link 28]</span><span class="sxs-lookup"><span data-stu-id="809b2-210">[UI Documentation - Reach - New Push Criterion][Link 28]</span></span>

## <a name="content-of-tiles-windows-phone-only"></a><span data-ttu-id="809b2-211">Conteúdo de blocos (somente para o Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="809b2-211">Content of Tiles (Windows Phone only)</span></span>
![Reach-Content4][33]

### <a name="define-hello-content-of-your-tile"></a><span data-ttu-id="809b2-213">Definir o conteúdo de saudação do bloco</span><span class="sxs-lookup"><span data-stu-id="809b2-213">Define hello content of your tile</span></span>
<span data-ttu-id="809b2-214">carga de bloco de saudação é toobe de texto de saudação exibida no bloco de saudação do seu aplicativo em dispositivos Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="809b2-214">hello tile payload is hello text toobe displayed in hello tile of your app on Windows Phone devices.</span></span>
<span data-ttu-id="809b2-215">Um envio por push de bloco é Olá Microsoft Push Notification Service (MPNS) versão um envio por push nativo para Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="809b2-215">A tile push is hello Microsoft Push Notification Service (MPNS) version of a native push for Windows Phone.</span></span> <span data-ttu-id="809b2-216">tipo de envio por push de bloco Olá é Olá único push tipo que não tem uma resposta e então público Olá futuras campanhas não pode ser criado em resultados de saudação de uma campanha de push de bloco.</span><span class="sxs-lookup"><span data-stu-id="809b2-216">hello tile push type is hello only push type that does not have a response and so hello audience of future campaigns can't be built on hello results of a tile push campaign.</span></span> 

### <a name="see-also"></a><span data-ttu-id="809b2-217">Consulte também</span><span class="sxs-lookup"><span data-stu-id="809b2-217">See also</span></span>
* <span data-ttu-id="809b2-218">[Documentação da API – API de Alcance – Envio por Push Nativo][Link 4]</span><span class="sxs-lookup"><span data-stu-id="809b2-218">[API Documentation - Reach API - Native Push][Link 4]</span></span>

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

