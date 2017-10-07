---
title: "aaaAzure Interface de usuário do Mobile Engagement - segmentos"
description: "Saiba como toocreate e gerenciam segmentos de padrões de uso de tooidentify usuários usando o Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6a4f2205-4a3c-406e-a04f-5e6f2a36653f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: bb214c45d05ebfbf243978658a7e331d4a7c6e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-segments-of-users-tooidentify-usage-patterns"></a><span data-ttu-id="a88fc-103">Como toocreate e gerenciam segmentos de padrões de uso de tooidentify de usuários</span><span class="sxs-lookup"><span data-stu-id="a88fc-103">How toocreate and manage segments of users tooidentify usage patterns</span></span>
<span data-ttu-id="a88fc-104">Este artigo descreve Olá **segmentos** guia da saudação **Mobile Engagement** portal.</span><span class="sxs-lookup"><span data-stu-id="a88fc-104">This article describes hello **SEGMENTS** tab of hello **Mobile Engagement** portal.</span></span> <span data-ttu-id="a88fc-105">Use Olá **Mobile Engagement** toomonitor portal e gerenciar seus aplicativos móveis.</span><span class="sxs-lookup"><span data-stu-id="a88fc-105">You use hello **Mobile Engagement** portal toomonitor and manage your mobile apps.</span></span>

<span data-ttu-id="a88fc-106">seção de segmentos de saudação do hello da interface do usuário permite que você toowork em segmentando os usuários com base em um comportamento diferente hello e análise que você pode obter de um aplicativo hello e também pode acessar por meio de saudação segmentos de API.</span><span class="sxs-lookup"><span data-stu-id="a88fc-106">hello Segments section of hello UI allows you toowork on segmenting your users based on hello different behavior and analytics that you can get from hello application and can also access through hello Segments API.</span></span> <span data-ttu-id="a88fc-107">Segmentos são computados primeiro 24 horas depois que são criados, e eles são recalculados com base nas informações de análise mais recentes da saudação a cada 24 horas.</span><span class="sxs-lookup"><span data-stu-id="a88fc-107">Segments are first computed 24 hours after they are created, and they are recomputed every 24 hours based on hello latest analytics information.</span></span> <span data-ttu-id="a88fc-108">Quando um segmento é calculado, ele exibe um gráfico de "Histórico de tooday do dia" por dia.</span><span class="sxs-lookup"><span data-stu-id="a88fc-108">Once a segment is calculated, it displays a "Day tooday history" chart each day.</span></span>

> [!NOTE]
> <span data-ttu-id="a88fc-109">Muitas seções de saudação **Mobile Engagement** IU do portal contêm Olá **Mostrar Ajuda** botão.</span><span class="sxs-lookup"><span data-stu-id="a88fc-109">Many sections of hello **Mobile Engagement** portal UI contain hello **SHOW HELP** button.</span></span> <span data-ttu-id="a88fc-110">Pressione este botão tooget mais informações contextuais sobre uma seção.</span><span class="sxs-lookup"><span data-stu-id="a88fc-110">Press this button tooget more contextual information about a section.</span></span>
> 
> 

## <a name="create-segments"></a><span data-ttu-id="a88fc-111">Criação segmentos</span><span class="sxs-lookup"><span data-stu-id="a88fc-111">Create Segments</span></span>
<span data-ttu-id="a88fc-112">Você pode criar um segmento com base em critérios de too10 em um período específico se too60 dias Olá passado da seção de análise de saudação.</span><span class="sxs-lookup"><span data-stu-id="a88fc-112">You can create a segment based on up too10 criteria on a specific period up too60 days in hello past from hello analytics section.</span></span> <span data-ttu-id="a88fc-113">Por exemplo, você pode criar um segmento com base em pessoas Olá tiveram exibido certas páginas ou pesquisada em busca de conteúdo específico dentro de seu aplicativo em Olá últimos 10 dias.</span><span class="sxs-lookup"><span data-stu-id="a88fc-113">For example, you can create a segment based on hello people who have viewed certain pages or searched for specific content within your app within hello last 10 days.</span></span> <span data-ttu-id="a88fc-114">Essas informações estão disponíveis na seção de análise de saudação.</span><span class="sxs-lookup"><span data-stu-id="a88fc-114">This information is available in hello analytics section.</span></span> <span data-ttu-id="a88fc-115">Assim, usá-lo em um segmento de toocreate e em seguida, configure um tootarget de notificação por push esse subconjunto dos usuários tooget-los toocome toohello back aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a88fc-115">So, you can use it toocreate a segment, and then set up a push notification tootarget this subset of users tooget them toocome back toohello application.</span></span> 

> [!NOTE]
> <span data-ttu-id="a88fc-116">Após um segmento ter sido calculado, ele não pode ser editado; ele só pode ser clonado (copiado) ou destruído (excluído).</span><span class="sxs-lookup"><span data-stu-id="a88fc-116">Once a segment has been calculated, it cannot be edited; it can only be cloned (copied) or destroyed (deleted).</span></span> <span data-ttu-id="a88fc-117">Um segmento pode ser clonado em Olá mesmo aplicativo (com hello AppID mesmo), e também podem ser clonado em outros aplicativos (com um AppID diferente).</span><span class="sxs-lookup"><span data-stu-id="a88fc-117">A segment can be cloned within hello same application (with hello same AppID), and it can also be cloned into other applications (with a different AppID).</span></span> 

 ![segments1][35] 

## <a name="examples-segments"></a><span data-ttu-id="a88fc-119">Exemplos de segmentos</span><span class="sxs-lookup"><span data-stu-id="a88fc-119">Examples Segments</span></span>
 ![segments2][36]

<span data-ttu-id="a88fc-121">Segmentos permitem que você toosegment os usuários finais de saudação do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a88fc-121">Segments allow you toosegment hello end-users of your application.</span></span>
<span data-ttu-id="a88fc-122">Segmentar os usuários é uma importante estratégia de marketing.</span><span class="sxs-lookup"><span data-stu-id="a88fc-122">Segmenting your users is an important marketing strategy.</span></span> <span data-ttu-id="a88fc-123">O Azure Mobile Engagement permite que os dados históricos tooget e criar segmentos personalizados.</span><span class="sxs-lookup"><span data-stu-id="a88fc-123">Azure Mobile Engagement allows you tooget historic data and create custom segments.</span></span> <span data-ttu-id="a88fc-124">Essa ferramenta avançada permite que você toolearn sobre a experiência de seus clientes em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a88fc-124">This powerful tool enables you toolearn about your customers’ experience in your application.</span></span> <span data-ttu-id="a88fc-125">Você pode facilmente analisar os segmentos e usá-los como destinos de envio.</span><span class="sxs-lookup"><span data-stu-id="a88fc-125">You can easily analyze your segments and use your segments as push targets.</span></span>
<span data-ttu-id="a88fc-126">Um caso de uso comum é que você deseja toosend um tooencourage uma notificação de envio por push seu usuários finais toorate seu aplicativo no repositório de saudação.</span><span class="sxs-lookup"><span data-stu-id="a88fc-126">A common use-case is that you want toosend a push a notification tooencourage your end-users toorate your application in hello store.</span></span> <span data-ttu-id="a88fc-127">Em vez de enviar uma notificação tooall seus usuários finais, você pode criar um segmento que deve especificar apenas os usuários que usaram seu aplicativo diariamente para Olá no último mês e tiveram um usuário ótimo experiência.</span><span class="sxs-lookup"><span data-stu-id="a88fc-127">Rather than sending a notification tooall your end-users, you can create a segment that would specify only users that have used your application every day for hello last month and have had a great user experience.</span></span> <span data-ttu-id="a88fc-128">Quando você envia notificações por push menos extremamente específicas, você pode obter um melhor ROI.</span><span class="sxs-lookup"><span data-stu-id="a88fc-128">When you send fewer, highly targeted push notifications, you get a better ROI.</span></span>

 ![segments3][37]

### <a name="segments-you-can-create-based-on-hello-major-azure-mobile-engagement-elements"></a><span data-ttu-id="a88fc-130">Segmentos, que você pode criar com base nas principais elementos do Azure Mobile Engagement hello:</span><span class="sxs-lookup"><span data-stu-id="a88fc-130">Segments you can create based on hello major Azure Mobile Engagement elements:</span></span>
* <span data-ttu-id="a88fc-131">Evento: Crie um segmento de evento específico que destinos um aplicativo hello que ocorreram mais de duas vezes por semana.</span><span class="sxs-lookup"><span data-stu-id="a88fc-131">Event: create a segment that targets one specific event of hello application that happened more than twice a week.</span></span> 
* <span data-ttu-id="a88fc-132">Sessão: Crie um segmento de usuários que usaram o aplicativo hello mais de 5 vezes na semana passada.</span><span class="sxs-lookup"><span data-stu-id="a88fc-132">Session: create a segment of users that have used hello application more than 5 times last week.</span></span>
* <span data-ttu-id="a88fc-133">Atividade: crie um segmento de usuários que usaram uma página ou conteúdo mais ou menos 10 vezes no mês passado.</span><span class="sxs-lookup"><span data-stu-id="a88fc-133">Activity: create a segment of users that have used one page or content more or less than 10 time last month.</span></span>
* <span data-ttu-id="a88fc-134">Trabalho: crie um segmento de usuários que concluíram um trabalho mais de duas vezes ao dia.</span><span class="sxs-lookup"><span data-stu-id="a88fc-134">Job: create a segment of users that have completed a job more than twice a day.</span></span>
* <span data-ttu-id="a88fc-135">Falha: Crie um segmento de todos os usuários de saudação que tiveram uma falha de mais de 10 vezes na semana passada.</span><span class="sxs-lookup"><span data-stu-id="a88fc-135">Crash: create a segment of all hello users that have had a crash more than 10 times last week.</span></span> <span data-ttu-id="a88fc-136">(Você poderia enviar este segmento com uma desculpa ou até mesmo um cupom!)</span><span class="sxs-lookup"><span data-stu-id="a88fc-136">(You could push this segment with an apology or even a coupon!)</span></span>
* <span data-ttu-id="a88fc-137">Erro: Crie um segmento de todos os usuários de saudação que tiveram um erro mais do que o 100 vezes da últimos 3 dias.</span><span class="sxs-lookup"><span data-stu-id="a88fc-137">Error: create a segment of all hello users that have had an error more than 100 times last 3 days.</span></span>
* <span data-ttu-id="a88fc-138">Informações do aplicativo: Crie um segmento que tem como alvo um informações de aplicativo personalizado que ocorreram durante a saudação últimos 25 dias.</span><span class="sxs-lookup"><span data-stu-id="a88fc-138">App Info: create a segment that targets a custom App Info that happened during hello last 25 days.</span></span>
  
  ![segments4][38]

<span data-ttu-id="a88fc-140">toouse segmento de maneira ideal, você deve ter feito uma integração personalizada do hello SDK em seu aplicativo com um plano de marcação de marcas "Informações de aplicativo".</span><span class="sxs-lookup"><span data-stu-id="a88fc-140">toouse Segment in an optimal way, you must have done a customized integration of hello SDK in your application with a tagging plan of "App Info" tags.</span></span>
<span data-ttu-id="a88fc-141">Em seguida, vá toohello home page da interface Olá, selecione aplicativo hello desejado e clique na seção de "Segmentos" hello.</span><span class="sxs-lookup"><span data-stu-id="a88fc-141">Then, go toohello home page of hello interface, select hello application you want and click on hello "Segments" section.</span></span>

1. <span data-ttu-id="a88fc-142">Selecione a seção de "Segmentos" hello.</span><span class="sxs-lookup"><span data-stu-id="a88fc-142">Select hello "Segments" section.</span></span>
2. <span data-ttu-id="a88fc-143">Clique em hello "Novo segmento" botão toocreate um novo segmento.</span><span class="sxs-lookup"><span data-stu-id="a88fc-143">Click on hello "New segment" button toocreate a new segment.</span></span>

## <a name="real-life-example-create-a-simple-segment-based-on-session-information"></a><span data-ttu-id="a88fc-144">Crie um segmento simples com base nas informações de "Sessão".</span><span class="sxs-lookup"><span data-stu-id="a88fc-144">Real Life Example: Create a simple segment based on "Session" information</span></span>
<span data-ttu-id="a88fc-145">Crie um segmento de todos os usuários finais Olá que usou seu aplicativo pelo menos 50 vezes Olá última semana.</span><span class="sxs-lookup"><span data-stu-id="a88fc-145">Create a segment of all hello end-users that have used your app at least 50 times in hello last week.</span></span> <span data-ttu-id="a88fc-146">A partir daí, localize somente Olá os usuários finais que passaram pelo menos 30 segundos no seu aplicativo por sessão.</span><span class="sxs-lookup"><span data-stu-id="a88fc-146">From there, find only hello end-users that have spent at least 30 seconds in your app per session.</span></span> <span data-ttu-id="a88fc-147">Isso mostrará todos os usuários finais Olá tem uma experiência positiva em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a88fc-147">This will show all hello end-users who have a positive experience in your app.</span></span> <span data-ttu-id="a88fc-148">Em seguida, segmento Olá criado pode ser usado toopush um tooask de usuários finais notificação toothese-los toorate seu aplicativo hello armazenar.</span><span class="sxs-lookup"><span data-stu-id="a88fc-148">Then, hello segment created could be used toopush a notification toothese end-users tooask them toorate your app in hello store.</span></span>

 ![segments5][39]

1. <span data-ttu-id="a88fc-150">Nomeie o segmento em ordem toofind rapidamente na lista de "Segmento" hello.</span><span class="sxs-lookup"><span data-stu-id="a88fc-150">Give your segment a name in order toofind it quickly in hello "Segment" list.</span></span>
2. <span data-ttu-id="a88fc-151">Clique em Olá botão "Criar".</span><span class="sxs-lookup"><span data-stu-id="a88fc-151">Click on hello "Create" button.</span></span>
   
   ![segments6][40]

<span data-ttu-id="a88fc-153">Selecione a sessão.</span><span class="sxs-lookup"><span data-stu-id="a88fc-153">Select Session.</span></span>

 ![segments7][41]

1. <span data-ttu-id="a88fc-155">Selecione o período de saudação da "Última semana".</span><span class="sxs-lookup"><span data-stu-id="a88fc-155">Select hello period of "Last week".</span></span>
2. <span data-ttu-id="a88fc-156">Clique em Avançar.</span><span class="sxs-lookup"><span data-stu-id="a88fc-156">Click next.</span></span>
   
   ![segments8][42]
3. <span data-ttu-id="a88fc-158">Selecione Olá operador relevantes lista Olá: =; ≥, ≤.</span><span class="sxs-lookup"><span data-stu-id="a88fc-158">Select hello Operator that is relevant among hello list: =; ≥, ≤.</span></span>
4. <span data-ttu-id="a88fc-159">Digite hello contagem desejada.</span><span class="sxs-lookup"><span data-stu-id="a88fc-159">Enter hello Count you want.</span></span>
5. <span data-ttu-id="a88fc-160">Selecione Olá ocorrência desejado.</span><span class="sxs-lookup"><span data-stu-id="a88fc-160">Select hello Occurrence you want.</span></span> 
6. <span data-ttu-id="a88fc-161">Clique em Avançar.</span><span class="sxs-lookup"><span data-stu-id="a88fc-161">Click next.</span></span>
   <span data-ttu-id="a88fc-162">Este exemplo é definido para que mais Olá última semana, correspondência de usuários que fizeram pelo menos 50 sessões.</span><span class="sxs-lookup"><span data-stu-id="a88fc-162">This example is set so that over hello last week, match users that have made at least 50 sessions.</span></span>
   
   ![segments9][43]

<span data-ttu-id="a88fc-164">Para Olá segmentação de sessão, você pode escolher comprimento Olá por sessão como um critério.</span><span class="sxs-lookup"><span data-stu-id="a88fc-164">For hello Session segmentation, you can choose hello length per session as a criteria.</span></span>

1. <span data-ttu-id="a88fc-165">Selecione Olá operador na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="a88fc-165">Select hello Operator from hello list.</span></span>
2. <span data-ttu-id="a88fc-166">Fornece Olá comprimento por sessão.</span><span class="sxs-lookup"><span data-stu-id="a88fc-166">Provide hello Length per session.</span></span>
3. <span data-ttu-id="a88fc-167">Clique em Avançar.</span><span class="sxs-lookup"><span data-stu-id="a88fc-167">Click Next.</span></span>
   <span data-ttu-id="a88fc-168">Neste exemplo, ela diz que sobre todas hello sessões que foram segmentadas na seção de ocorrência hello, selecione apenas Olá usuários que passaram mais de 30 segundos por sessão.</span><span class="sxs-lookup"><span data-stu-id="a88fc-168">In this example, it says that over all hello sessions that have been segmented on hello occurrence section, select only hello users that have spent more than 30 seconds per session.</span></span>
   
   ![segments10][44]

<span data-ttu-id="a88fc-170">Nomeie seu critério em ordem tooretrieve concluí-lo em Olá funil e clique em Concluir.</span><span class="sxs-lookup"><span data-stu-id="a88fc-170">Name your criterion in order tooretrieve it in hello complete funnel, and click Finish.</span></span>

 ![segments11][45]

<span data-ttu-id="a88fc-172">Quando você terminar a configuração ao seu critério, ele será exibido no funil de segmento de saudação.</span><span class="sxs-lookup"><span data-stu-id="a88fc-172">When you have finished setting up your criterion, it will appear in hello segment funnel.</span></span>
<span data-ttu-id="a88fc-173">Como um segmento é baseado em dados de análise, os segmentos são calculados uma vez por dia.</span><span class="sxs-lookup"><span data-stu-id="a88fc-173">Because a segment is based on analytics data, segments are computed once per day.</span></span>
<span data-ttu-id="a88fc-174">Neste exemplo, 47,7% dos usuários finais de total Olá correspondentes ao critério de saudação.</span><span class="sxs-lookup"><span data-stu-id="a88fc-174">In this example, 47,7% of hello total end-users matched hello criterion.</span></span> <span data-ttu-id="a88fc-175">Eles devem ser usuários Olá que tiveram uma boa experiência e será ser tooprovide provavelmente uma classificação mais alta, se você enviar uma notificação solicitando toorate Olá aplicativo no repositório de saudação.</span><span class="sxs-lookup"><span data-stu-id="a88fc-175">They should be hello users who have had a good experience and will be likely tooprovide a higher rating if you push them a notification asking them toorate hello app in hello store.</span></span>

## <a name="see-also"></a><span data-ttu-id="a88fc-176">Consulte também</span><span class="sxs-lookup"><span data-stu-id="a88fc-176">See also</span></span>
* <span data-ttu-id="a88fc-177">[Conceitos][Link 6]</span><span class="sxs-lookup"><span data-stu-id="a88fc-177">[Concepts][Link 6]</span></span>
* <span data-ttu-id="a88fc-178">[Serviço do Guia de Solução de Problemas][Link 24]</span><span class="sxs-lookup"><span data-stu-id="a88fc-178">[Troubleshooting Guide Service][Link 24]</span></span>

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
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md

