---
title: "Interface do usuário do Azure Mobile Engagement - Alcance - Critério"
description: "Saiba como usar critérios de direcionamento para campanhas de envio por push para selecionar um subconjunto de seus usuários usando o Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: a4ed03a0-55b1-4dd8-b0bd-c475005afb66
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 803b44721d0ab1ac7b5a8074e18857fc57adb724
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-targeting-criteria-to-send-push-campaigns-to-a-select-subset-of-your-users"></a><span data-ttu-id="9b9b4-103">Como usar critérios de direcionamento para enviar por push campanhas para selecionar um subconjunto de seus usuários</span><span class="sxs-lookup"><span data-stu-id="9b9b4-103">How to use targeting criteria to send push campaigns to a select subset of your users</span></span>
<span data-ttu-id="9b9b4-104">Direcionar seu público-alvo por critérios específicos com o botão "Novos Critérios" é um dos conceitos mais poderosos no Azure Mobile Engagement que ajuda a enviar importantes notificações por push que os clientes responderão em vez de enviar spam a todos.</span><span class="sxs-lookup"><span data-stu-id="9b9b4-104">Targeting your audience by specific criteria with the "New Criteria" button is one of the most powerful concepts in Azure Mobile Engagement that helps you send relevant push notifications that the customers will respond to instead of Spamming everyone.</span></span> <span data-ttu-id="9b9b4-105">Você pode limitar seu público-alvo com base em critérios padrão e simular envios por push para determinar quantas pessoas receberão a notificação.</span><span class="sxs-lookup"><span data-stu-id="9b9b4-105">You can limit your audience based on standard criteria and simulate pushes to determine how many people will receive the notification.</span></span>

<span data-ttu-id="9b9b4-106">**Consulte também:**</span><span class="sxs-lookup"><span data-stu-id="9b9b4-106">**See also:**</span></span>

* <span data-ttu-id="9b9b4-107">[Documentação da Interface do Usuário ‑ Alcance ‑ Nova Campanha por Push][Link 27]</span><span class="sxs-lookup"><span data-stu-id="9b9b4-107">[UI Documentation - Reach - New Push Campaign][Link 27]</span></span>

## <a name="audience-criteria-can-include"></a><span data-ttu-id="9b9b4-108">Os critérios de público-alvo podem incluir:</span><span class="sxs-lookup"><span data-stu-id="9b9b4-108">Audience criteria can include:</span></span>
* <span data-ttu-id="9b9b4-109">* * Technicals: * * você pode direcionar com as mesmas informações técnicas que você pode ver nas seções a análise e o Monitor.</span><span class="sxs-lookup"><span data-stu-id="9b9b4-109">**Technicals: ** You can target based on the same technical information you can see in the Analytics and Monitor sections.</span></span> <span data-ttu-id="9b9b4-110">**Veja também:** [Documentação da Interface do Usuário ‑ Análise][Link 15], [Documentação da Interface do Usuário ‑ Monitoramento][Link 16]</span><span class="sxs-lookup"><span data-stu-id="9b9b4-110">**See also:** [UI Documentation - Analytics][Link 15],  [UI Documentation - Monitor][Link 16]</span></span>
* <span data-ttu-id="9b9b4-111">**Local:** os aplicativos que usam "Relatórios de localização em tempo real” com isolamento geográfico podem usar a localização geográfica como um critério para direcionar para um público-alvo a partir da localização do GPS.</span><span class="sxs-lookup"><span data-stu-id="9b9b4-111">**Location:** Applications that use "Real time location reporting" with Geo-Fencing can use Geo-Location as a criteria to target an audience from the GPS location.</span></span> <span data-ttu-id="9b9b4-112">A chamada de "Relatórios de Localização de Área Lenta" também pode ser usada para direcionar para um público-alvo da localização do celular (“Relatórios de localização em tempo real” e “Relatórios de Localização de Área Lenta” devem ser ativados no SDK).</span><span class="sxs-lookup"><span data-stu-id="9b9b4-112">"Lazy Area Location Reporting" call also be used to target an audience from the cell phone location ("Real time location reporting" and "Lazy Area Location Reporting" must be activated from the SDK).</span></span> <span data-ttu-id="9b9b4-113">**Consulte também:** [Documentação do SDK ‑ iOS ‑ Integração][Link 5], [Documentação do SDK ‑ Android ‑ Integração][Link 5]</span><span class="sxs-lookup"><span data-stu-id="9b9b4-113">**See also:** [SDK Documentation - iOS -  Integration][Link 5], [SDK Documentation - Android -  Integration][Link 5]</span></span>
* <span data-ttu-id="9b9b4-114">**Comentários do Alcance:** você pode direcionar para o público-alvo com base nos comentários sobre notificações anteriores de alcance e nos comentários de Anúncios, Pesquisas e Envio de Dados por Push.</span><span class="sxs-lookup"><span data-stu-id="9b9b4-114">**Reach Feedback:** You can target your audience based on their feedback from previous reach notifications through reach feedback from Announcements, Polls, and Data Pushes.</span></span> <span data-ttu-id="9b9b4-115">Isso permite direcionar melhor para seu público-alvo depois de duas ou três campanhas de alcance em relação ao que poderia ser feito da primeira vez.</span><span class="sxs-lookup"><span data-stu-id="9b9b4-115">This enables you to better target your audience after two or three reach campaigns than you could the first time.</span></span> <span data-ttu-id="9b9b4-116">Também pode ser usado para filtrar os usuários que já receberam uma notificação com conteúdo semelhante, definindo uma campanha para NÃO ser enviada aos usuários que já receberam uma campanha anterior específica.</span><span class="sxs-lookup"><span data-stu-id="9b9b4-116">It can also be used to filter out users who already received a notification with similar content, by setting a campaign to NOT be sent to users who already received a specific previous campaign.</span></span> <span data-ttu-id="9b9b4-117">Você pode até mesmo excluir os usuários incluídos em uma campanha específica que ainda esteja ativa do recebimento de novos envios por Push.</span><span class="sxs-lookup"><span data-stu-id="9b9b4-117">You can even exclude users who are included a specific campaign that is still active from receiving new Pushes.</span></span> <span data-ttu-id="9b9b4-118">**Consulte também:** [Documentação da Interface do Usuário ‑ Alcance ‑ Enviar Conteúdo por Push][Link 29]</span><span class="sxs-lookup"><span data-stu-id="9b9b4-118">**See also:** [UI Documentation -  Reach - Push Content][Link 29]</span></span>
* <span data-ttu-id="9b9b4-119">**Instalar Rastreamento:** você pode rastrear informações com base no local onde seus usuários instalaram o seu Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9b9b4-119">**Install Tracking:** You can track information based on where your users installed your App.</span></span> <span data-ttu-id="9b9b4-120">**Consulte também:** [Documentação da interface do usuário ‑ Configurações][Link 20]</span><span class="sxs-lookup"><span data-stu-id="9b9b4-120">**See also:** [UI Documentation -  Settings][Link 20]</span></span>
* <span data-ttu-id="9b9b4-121">**Perfil do Usuário:** você pode direcionar com base nas informações de usuário padrão e pode direcionar com base em informações do aplicativo personalizado que você criou.</span><span class="sxs-lookup"><span data-stu-id="9b9b4-121">**User Profile:** You can target based on standard user information and you can target based on the custom app info that you have created.</span></span> <span data-ttu-id="9b9b4-122">Isso inclui usuários que estão conectados no momento e os usuários que responderam perguntas específicas que você fez a eles para definir o próprio aplicativo, em vez de apenas a forma como eles responderam a campanhas anteriores.</span><span class="sxs-lookup"><span data-stu-id="9b9b4-122">This includes users who are currently logged in and users that have answered specific questions you have asked them to set in the app itself instead of just how they have responded to previous campaigns.</span></span> <span data-ttu-id="9b9b4-123">Todas as Informações do Aplicativo definidas para seu aplicativo são mostradas nesta lista.</span><span class="sxs-lookup"><span data-stu-id="9b9b4-123">All of your App Info's defined for your app show up on this list.</span></span>
* <span data-ttu-id="9b9b4-124">Segmentos: também será possível direcionar com base em segmentos que você tenha criado com base no comportamento de um usuário específico com diversos critérios.</span><span class="sxs-lookup"><span data-stu-id="9b9b4-124">Segments: You can also target based on segments that you have created based on specific user behavior containing multiple criteria.</span></span> <span data-ttu-id="9b9b4-125">Todos os segmentos definidos para o seu aplicativo aparecem nessa lista.</span><span class="sxs-lookup"><span data-stu-id="9b9b4-125">All of your segments defined for your app show up on this list.</span></span> <span data-ttu-id="9b9b4-126">**Consulte também:** [Documentação da Interface do Usuário ‑ Segmentos][Link 18]</span><span class="sxs-lookup"><span data-stu-id="9b9b4-126">**See also:** [UI Documentation -  Segments][Link 18]</span></span>
* <span data-ttu-id="9b9b4-127">**Informações do Aplicativo:** as Marcas de Informações de Aplicativo Personalizadas podem ser criadas nas “Configurações" para controlar o comportamento do usuário.</span><span class="sxs-lookup"><span data-stu-id="9b9b4-127">**App Info:** Custom App Info Tags can be created from “Settings” to track user behavior.</span></span> <span data-ttu-id="9b9b4-128">**Consulte também:** [Documentação da interface do usuário ‑ Configurações][Link 20]</span><span class="sxs-lookup"><span data-stu-id="9b9b4-128">**See also:** [UI Documentation -  Settings][Link 20]</span></span>

## <a name="example"></a><span data-ttu-id="9b9b4-129">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="9b9b4-129">Example:</span></span>
<span data-ttu-id="9b9b4-130">Se você quiser enviar por push um anúncio apenas para o subconjunto de seus usuários que executaram uma ação no aplicativo de compra.</span><span class="sxs-lookup"><span data-stu-id="9b9b4-130">If you want to push an announcement only to the sub-set of your users that have performed an in-app purchase action.</span></span>

1. <span data-ttu-id="9b9b4-131">Vá para a página de configurações do aplicativo, selecione o menu "Informações do Aplicativo" e selecione "Nova informação do aplicativo"</span><span class="sxs-lookup"><span data-stu-id="9b9b4-131">Go to your application settings page, select the "App info" menu and select "New app info"</span></span>
2. <span data-ttu-id="9b9b4-132">Registre uma nova informação de aplicativo booliano chamada "inAppPurchase"</span><span class="sxs-lookup"><span data-stu-id="9b9b4-132">Register a new Boolean app info called "inAppPurchase"</span></span>
3. <span data-ttu-id="9b9b4-133">Defina as informações de aplicativo como "verdadeiro" quando o usuário executar com êxito uma compra no aplicativo (usando a função sendAppInfo("inAppPurchase",...))</span><span class="sxs-lookup"><span data-stu-id="9b9b4-133">Make your application set this app info to "true" when the user successfully performs an in-app purchase (by using the sendAppInfo("inAppPurchase", ...) function)</span></span>
4. <span data-ttu-id="9b9b4-134">Se você não quiser fazer isso no seu aplicativo, poderá fazer no seu back-end usando a API do dispositivo)</span><span class="sxs-lookup"><span data-stu-id="9b9b4-134">If you don't want to do this from your application, you can do it from your backend by using the device API)</span></span>
5. <span data-ttu-id="9b9b4-135">Em seguida, bastará criar o seu anúncio, com um critério limitando seu público-alvo aos usuários que tenham "inAppPurchase" definido como "verdadeiro")</span><span class="sxs-lookup"><span data-stu-id="9b9b4-135">Then, you just need to create your announcement, with a criterion limiting your audience to users having "inAppPurchase" set to "true")</span></span>

> [!NOTE]
> <span data-ttu-id="9b9b4-136">O direcionamento com base em critérios diferentes das marcas de informações de aplicativo requer que o Azure Mobile Engagement colete informações dos dispositivos de seus usuários antes de efetuar o envio e, portanto, pode causar um atraso.</span><span class="sxs-lookup"><span data-stu-id="9b9b4-136">Targeting based on criteria other than app info tags requires Azure Mobile Engagement to gather information from your users' devices before the push is sent and so can cause a delay.</span></span> <span data-ttu-id="9b9b4-137">As opções de configuração de envio por push complexas (como atualização de notificações) também podem atrasar o envio por push.</span><span class="sxs-lookup"><span data-stu-id="9b9b4-137">Complex push configuration options (like updating badges) can also delay pushes.</span></span> <span data-ttu-id="9b9b4-138">Usar uma campanha "monoestável" da API de envio por Push é o método de envio mais rápido no Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="9b9b4-138">Using a "one shot" campaign from the Push API is the absolute fastest push method in Azure Mobile Engagement.</span></span> <span data-ttu-id="9b9b4-139">Usar as marcas de informações de aplicativo apenas como critérios de envio por push para uma campanha de Alcance (a partir da API de Alcance ou da interface do usuário) é o próximo método mais rápido, já que as marcas de informações do aplicativo estão armazenadas no lado do servidor.</span><span class="sxs-lookup"><span data-stu-id="9b9b4-139">Using only app info tags as push criteria for a Reach campaign (either from the Reach API or the UI) is the next fastest method since app info tags are stored on the server side.</span></span> <span data-ttu-id="9b9b4-140">Usar outros critérios de direcionamento para uma campanha de envio é o método mais flexível, porém o método mais lento do envio por push, já que o Azure Mobile Engagement tem que consultar os dispositivos para enviar a campanha.</span><span class="sxs-lookup"><span data-stu-id="9b9b4-140">Using other targeting criteria for a push campaign is the most flexible but slowest push method since Azure Mobile Engagement has to query the devices in order to send the campaign.</span></span>

![Reach-Criterion1][29] 

## <a name="criterion-options-apply-to"></a><span data-ttu-id="9b9b4-142">As Opções de Critério se Aplicam a:</span><span class="sxs-lookup"><span data-stu-id="9b9b4-142">Criterion Options Apply to:</span></span>
* <span data-ttu-id="9b9b4-143">**Técnicos**</span><span class="sxs-lookup"><span data-stu-id="9b9b4-143">**Technicals**</span></span>     
* <span data-ttu-id="9b9b4-144">Nome do firmware: nome do firmware</span><span class="sxs-lookup"><span data-stu-id="9b9b4-144">Firmware name:    Firmware name</span></span>
* <span data-ttu-id="9b9b4-145">Versão do firmware: versão do firmware</span><span class="sxs-lookup"><span data-stu-id="9b9b4-145">Firmware version:    Firmware version</span></span>
* <span data-ttu-id="9b9b4-146">Modelo do dispositivo: modelo do dispositivo</span><span class="sxs-lookup"><span data-stu-id="9b9b4-146">Device model:    Device model</span></span>
* <span data-ttu-id="9b9b4-147">Fabricante do dispositivo: fabricante do dispositivo</span><span class="sxs-lookup"><span data-stu-id="9b9b4-147">Device manufacturer:    Device manufacturer</span></span>
* <span data-ttu-id="9b9b4-148">Versão do aplicativo: versão do aplicativo</span><span class="sxs-lookup"><span data-stu-id="9b9b4-148">Application version:    Application version</span></span>
* <span data-ttu-id="9b9b4-149">Nome da operadora: nome da operadora, indefinido</span><span class="sxs-lookup"><span data-stu-id="9b9b4-149">Carrier name:    Carrier name, undefined</span></span>
* <span data-ttu-id="9b9b4-150">País da operadora: país da operadora, indefinido</span><span class="sxs-lookup"><span data-stu-id="9b9b4-150">Carrier country:    Carrier country, undefined</span></span>
* <span data-ttu-id="9b9b4-151">Tipo de rede: tipo de rede</span><span class="sxs-lookup"><span data-stu-id="9b9b4-151">Network type:    Network type</span></span>
* <span data-ttu-id="9b9b4-152">Localidade: localidade</span><span class="sxs-lookup"><span data-stu-id="9b9b4-152">Locale:    Locale</span></span>
* <span data-ttu-id="9b9b4-153">Tamanho da tela: tamanho da tela</span><span class="sxs-lookup"><span data-stu-id="9b9b4-153">Screen size:    Screen size</span></span>
* <span data-ttu-id="9b9b4-154">**Localidade**</span><span class="sxs-lookup"><span data-stu-id="9b9b4-154">**Location**</span></span>      
* <span data-ttu-id="9b9b4-155">Última área conhecida: país, região, localidade</span><span class="sxs-lookup"><span data-stu-id="9b9b4-155">Last known area:    Country, Region, Locality</span></span>
* <span data-ttu-id="9b9b4-156">Isolamento geográfico em tempo real: lista de POIs (Nome, Ações), POI circular (Nome, Latitude, Longitude, Raio em metros)</span><span class="sxs-lookup"><span data-stu-id="9b9b4-156">Real time geo-fencing:    List of POIs (Name, Actions), Circular POI (Name, Latitude, Longitude, Radius in meters)</span></span>
* <span data-ttu-id="9b9b4-157">**Comentários de alcance**</span><span class="sxs-lookup"><span data-stu-id="9b9b4-157">**Reach feedback**</span></span>     
* <span data-ttu-id="9b9b4-158">Comentários de notificação: anúncio, comentários</span><span class="sxs-lookup"><span data-stu-id="9b9b4-158">Announcement feedback:    Announcement, feedback</span></span>
* <span data-ttu-id="9b9b4-159">Comentários da pesquisa: pesquisa, comentários</span><span class="sxs-lookup"><span data-stu-id="9b9b4-159">Poll feedback:    Poll, feedback</span></span>
* <span data-ttu-id="9b9b4-160">Comentários de resposta da pesquisa: comentários de resposta da pesquisa, pergunta, alternativa</span><span class="sxs-lookup"><span data-stu-id="9b9b4-160">Poll answer feedback:    Poll answer feedback, question, choice</span></span>
* <span data-ttu-id="9b9b4-161">Comentários de Push de Dados: push de dados, comentários</span><span class="sxs-lookup"><span data-stu-id="9b9b4-161">Data Push feedback:    Data Push, feedback</span></span>
* <span data-ttu-id="9b9b4-162">**Instalar o Rastreamento**</span><span class="sxs-lookup"><span data-stu-id="9b9b4-162">**Install Tracking**</span></span>     
* <span data-ttu-id="9b9b4-163">Loja: loja, indefinido</span><span class="sxs-lookup"><span data-stu-id="9b9b4-163">Store:    Store, Undefined</span></span>
* <span data-ttu-id="9b9b4-164">Fonte: fonte, indefinido</span><span class="sxs-lookup"><span data-stu-id="9b9b4-164">Source:    Source, Undefined</span></span>
* <span data-ttu-id="9b9b4-165">**Perfil do usuário**</span><span class="sxs-lookup"><span data-stu-id="9b9b4-165">**User profile**</span></span>     
* <span data-ttu-id="9b9b4-166">Sexo: masculino ou feminino, indefinido</span><span class="sxs-lookup"><span data-stu-id="9b9b4-166">Gender:    male or female, undefined</span></span>
* <span data-ttu-id="9b9b4-167">Data de nascimento: operador, data, indefinido</span><span class="sxs-lookup"><span data-stu-id="9b9b4-167">Birth date:    operator, date, undefined</span></span>
* <span data-ttu-id="9b9b4-168">Aceitação: verdadeiro ou falso, indefinido</span><span class="sxs-lookup"><span data-stu-id="9b9b4-168">Opt-in:    true or false, undefined</span></span>
* <span data-ttu-id="9b9b4-169">**Informações do aplicativo**</span><span class="sxs-lookup"><span data-stu-id="9b9b4-169">**App Info**</span></span>      
* <span data-ttu-id="9b9b4-170">Cadeia de caracteres: cadeia de caracteres, indefinido</span><span class="sxs-lookup"><span data-stu-id="9b9b4-170">String:    String, undefined</span></span>
* <span data-ttu-id="9b9b4-171">Data: operador, data, indefinido</span><span class="sxs-lookup"><span data-stu-id="9b9b4-171">Date:    operator, date, undefined</span></span>
* <span data-ttu-id="9b9b4-172">Inteiro: operador, número, indefinido</span><span class="sxs-lookup"><span data-stu-id="9b9b4-172">Integer:    operator, number, undefined</span></span>
* <span data-ttu-id="9b9b4-173">Booliano: verdadeiro ou falso, indefinido</span><span class="sxs-lookup"><span data-stu-id="9b9b4-173">Boolean:    true or false, undefined</span></span>
* <span data-ttu-id="9b9b4-174">**Segmento**</span><span class="sxs-lookup"><span data-stu-id="9b9b4-174">**Segment**</span></span>    
* <span data-ttu-id="9b9b4-175">Nome dos segmentos (da lista suspensa), Exclusão (usuários de destino que não fazem parte deste segmento).</span><span class="sxs-lookup"><span data-stu-id="9b9b4-175">Name of Segments (from dropdown list), Exclusion (target users that are not a part of this segment).</span></span>

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

