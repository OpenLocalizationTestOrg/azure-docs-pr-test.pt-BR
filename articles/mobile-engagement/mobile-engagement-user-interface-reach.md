---
title: "aaaAzure Interface de usuário do Mobile Engagement - alcance"
description: "Saiba como tooreach toohello usuários de seu aplicativo com notificações por push usando o Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: d96e2590-08dd-4481-a352-2c18f26a1643
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 40d5162ddeccec82c2c9f5b0d72b4cb10c9ddc38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreach-out-toohello-users-of-your-application-with-push-notifications"></a><span data-ttu-id="9b70c-103">Como tooreach toohello usuários de seu aplicativo com notificações por push</span><span class="sxs-lookup"><span data-stu-id="9b70c-103">How tooreach out toohello users of your application with push notifications</span></span>
<span data-ttu-id="9b70c-104">Este artigo descreve Olá **alcançar** guia da saudação **Mobile Engagement** portal.</span><span class="sxs-lookup"><span data-stu-id="9b70c-104">This article describes hello **REACH** tab of hello **Mobile Engagement** portal.</span></span> <span data-ttu-id="9b70c-105">Use Olá **Mobile Engagement** toomonitor portal e gerenciar seus aplicativos móveis.</span><span class="sxs-lookup"><span data-stu-id="9b70c-105">You use hello **Mobile Engagement** portal toomonitor and manage your mobile apps.</span></span> <span data-ttu-id="9b70c-106">Observe que toostart usando o portal de saudação toocreate primeiro é necessário um **do Azure Mobile Engagement** conta.</span><span class="sxs-lookup"><span data-stu-id="9b70c-106">Note that toostart using hello portal you first need toocreate an **Azure Mobile Engagement** account.</span></span> <span data-ttu-id="9b70c-107">Para obter mais informações, veja [Criar uma conta do Azure Mobile Engagement](mobile-engagement-create.md).</span><span class="sxs-lookup"><span data-stu-id="9b70c-107">For more information, see [Create an Azure Mobile Engagement account](mobile-engagement-create.md).</span></span>

<span data-ttu-id="9b70c-108">Olá atingir seção Olá interface do usuário é ferramenta de gerenciamento de campanha Olá Push onde você pode criar/editar/ativar/término/monitor e obter estatísticas sobre os recursos que também podem ser acessados por meio de hello API de alcance (e alguns elementos da saudação baixa e campanhas de notificação por Push nível de API do Push).</span><span class="sxs-lookup"><span data-stu-id="9b70c-108">hello Reach section of hello UI is hello Push campaign management tool where you can create/edit/activate/finish/monitor and get statistics on Push notification campaigns and features that can also be accessed via hello Reach API (and some elements of hello low level Push API).</span></span> <span data-ttu-id="9b70c-109">Lembre-se de que, se você estiver usando APIs de saudação ou saudação da interface do usuário, você precisará toointegrate do Azure Mobile Engagement e alcance em seu aplicativo para cada plataforma com hello SDK antes de usar alcançar campanhas.</span><span class="sxs-lookup"><span data-stu-id="9b70c-109">Remember that whether you are using hello APIs or hello UI, you will need toointegrate both Azure Mobile Engagement and Reach into your application for each platform with hello SDK before you can use Reach campaigns.</span></span>

> [!NOTE]
> <span data-ttu-id="9b70c-110">Muitas seções de saudação **Mobile Engagement** IU do portal contêm Olá **Mostrar Ajuda** botão.</span><span class="sxs-lookup"><span data-stu-id="9b70c-110">Many sections of hello **Mobile Engagement** portal UI contain hello **SHOW HELP** button.</span></span> <span data-ttu-id="9b70c-111">Pressione este botão tooget mais informações contextuais sobre uma seção.</span><span class="sxs-lookup"><span data-stu-id="9b70c-111">Press this button tooget more contextual information about a section.</span></span>
> 
> 

## <a name="four-types-of-push-notifications"></a><span data-ttu-id="9b70c-112">Quatro tipos de notificações por Push</span><span class="sxs-lookup"><span data-stu-id="9b70c-112">Four types of Push notifications</span></span>
1. <span data-ttu-id="9b70c-113">Anúncios - permitir toosend toousers de mensagens de anúncio que redirecioná-los tooanother local dentro de seu aplicativo ou toosend-los tooa página da Web ou armazenar fora de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9b70c-113">Announcements - allow you toosend advertising messages toousers that redirect them tooanother location inside your app or toosend them tooa webpage or store outside of your app.</span></span> 
2. <span data-ttu-id="9b70c-114">Pesquisas - permitir toogather informações de usuários finais por fazer perguntas a eles.</span><span class="sxs-lookup"><span data-stu-id="9b70c-114">Polls - allow you toogather information from end users by asking them questions.</span></span>
3. <span data-ttu-id="9b70c-115">Envios de dados - permitir toosend um arquivo de dados binário ou base64.</span><span class="sxs-lookup"><span data-stu-id="9b70c-115">Data Pushes - allow you toosend a binary or base64 data file.</span></span> <span data-ttu-id="9b70c-116">Olá informações contidas em um envio de dados são enviados tooyour aplicativo toomodify experiência atual dos usuários em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9b70c-116">hello information contained in a data push is sent tooyour application toomodify your users' current experience in your app.</span></span> <span data-ttu-id="9b70c-117">Seu aplicativo precisa de dados de saudação toobe tooprocess capaz em um envio de dados.</span><span class="sxs-lookup"><span data-stu-id="9b70c-117">Your application needs toobe able tooprocess hello data in a data push.</span></span>

## <a name="campaign-details"></a><span data-ttu-id="9b70c-118">Detalhes da campanha</span><span class="sxs-lookup"><span data-stu-id="9b70c-118">Campaign Details</span></span>
<span data-ttu-id="9b70c-119">Você pode editar, clonar, excluir ou ativar campanhas que não foram ativadas ainda focalizando seus nomes ou você pode clicar em tooopen-los.</span><span class="sxs-lookup"><span data-stu-id="9b70c-119">You can edit, clone, delete, or activate campaigns that have not been activated yet by hovering over their names or you can click tooopen them.</span></span> <span data-ttu-id="9b70c-120">Você pode clonar campanhas que já foi ativadas focalizando seus nomes ou você pode clicar em tooopen-los.</span><span class="sxs-lookup"><span data-stu-id="9b70c-120">You can clone campaigns that have already been activated by hovering over their names or you can click tooopen them.</span></span> <span data-ttu-id="9b70c-121">No entanto, você não pode alterar uma campanha depois que ela tiver sido ativada.</span><span class="sxs-lookup"><span data-stu-id="9b70c-121">However, you can't change a campaign once it has been activated.</span></span>

![Reach1][18]

## <a name="reach-feedback"></a><span data-ttu-id="9b70c-123">Comentários do Reach</span><span class="sxs-lookup"><span data-stu-id="9b70c-123">Reach Feedback</span></span>
<span data-ttu-id="9b70c-124">Clique em **estatísticas** toosee detalhes de saudação de uma campanha de alcance.</span><span class="sxs-lookup"><span data-stu-id="9b70c-124">Click on **Statistics** toosee hello details of a Reach campaign.</span></span> <span data-ttu-id="9b70c-125">Olá **simples** exibição fornece uma representação visual na forma de saudação de um gráfico de barras de coluna sobre o que aconteceu, depois de uma campanha foi ativada.</span><span class="sxs-lookup"><span data-stu-id="9b70c-125">hello **Simple** view provides a visual representation in hello form of a column bar graph about what happened after a campaign was activated.</span></span> <span data-ttu-id="9b70c-126">Olá **avançado** exibição fornece mais detalhes sobre a campanha de push hello.</span><span class="sxs-lookup"><span data-stu-id="9b70c-126">hello **Advanced** view provides more granular details about hello push campaign.</span></span> <span data-ttu-id="9b70c-127">Esses detalhes não estará disponíveis se você estiver enviando uma campanha de teste ou seja, um dispositivo de teste tooa enviados por push.</span><span class="sxs-lookup"><span data-stu-id="9b70c-127">These details will not be available if you are sending a test campaign i.e. a push sent tooa test device.</span></span> <span data-ttu-id="9b70c-128">Veja como você deve interpretar esses detalhes:</span><span class="sxs-lookup"><span data-stu-id="9b70c-128">Here is how you should interpret these details:</span></span>

1. <span data-ttu-id="9b70c-129">**Enviado por push** -Isso especifica o número de saudação de mensagens enviadas por push toohello dispositivos.</span><span class="sxs-lookup"><span data-stu-id="9b70c-129">**Pushed** - This specifies hello number of messages pushed toohello devices.</span></span> <span data-ttu-id="9b70c-130">Esse número dependerá de público-alvo Olá especificado ao criar a campanha de push hello.</span><span class="sxs-lookup"><span data-stu-id="9b70c-130">This number will depend on hello target audience you specified while creating hello push campaign.</span></span> <span data-ttu-id="9b70c-131">Se você não especificar qualquer público-alvo, em seguida, esse push será enviado tooall Olá registrado dispositivos.</span><span class="sxs-lookup"><span data-stu-id="9b70c-131">If you do not specify any target audience, then this push will be sent out tooall hello registered devices.</span></span> <span data-ttu-id="9b70c-132">Como todos os outros serviços de envio, nós não Olá enviar notificações por push diretamente toohello dispositivos, mas em vez disso, push toohello respectivas plataformas específicas Push Notification Services (PNS - GCM/APNS/WNS) para que eles podem oferecer notificações Olá toohello dispositivos.</span><span class="sxs-lookup"><span data-stu-id="9b70c-132">Like all other push services, we do not push hello notifications directly toohello devices but instead push them toohello respective platform specific Push Notification Services (PNS - APNS/GCM/WNS) so that they can deliver hello notifications toohello devices.</span></span> 
2. <span data-ttu-id="9b70c-133">**Entregue** -Isso especifica o número de saudação de mensagens que são entregues pelo dispositivo de toohello PNS hello e confirmada com êxito como recebida pelo SDK do Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="9b70c-133">**Delivered** - This specifies hello number of messages which are successfully delivered by hello PNS toohello device and acknowledged as received by Mobile Engagement SDK.</span></span> 
   
   <span data-ttu-id="9b70c-134">*Motivos para a contagem Entregues ser menor do que a contagem de Enviada por push:*</span><span class="sxs-lookup"><span data-stu-id="9b70c-134">*Reasons for Delivered count being less than Pushed count:*</span></span>
   
   1. <span data-ttu-id="9b70c-135">Se usuário Olá tiver desinstalado o aplicativo hello de dispositivo Olá mas Olá PNS não sabe sobre ele em tempo de saudação que podemos enviar por push de saudação toohello PNS a mensagem de saudação será removida.</span><span class="sxs-lookup"><span data-stu-id="9b70c-135">If hello user has uninstalled hello app from hello device but hello PNS doesn't know about it at hello time we send hello push toohello PNS then hello message will be dropped.</span></span>
   2. <span data-ttu-id="9b70c-136">Se dispositivo Olá Olá aplicativo mas próprios dispositivos Olá estavam offline por longos períodos de tempo, em seguida, hello PNS falhará toodeliver dispositivo de toohello de mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b70c-136">If hello device has hello app but hello devices themselves were offline for long periods of time, then hello PNS will fail toodeliver hello message toohello device.</span></span> 
   3. <span data-ttu-id="9b70c-137">Se mensagem entregue toohello dispositivo mas Olá SDK do Mobile Engagement no aplicativo hello não reconhece o conteúdo de saudação da mensagem de saudação, descarta essa mensagem.</span><span class="sxs-lookup"><span data-stu-id="9b70c-137">If hello message does get delivered toohello device but hello Mobile Engagement SDK in hello app doesn’t recognize hello content of hello message, then it drops that message.</span></span> <span data-ttu-id="9b70c-138">Isso pode acontecer se a personalização de saudação da notificação de saudação no aplicativo hello gera uma exceção que captura de nós na mensagem de saudação SDK e drop Olá.</span><span class="sxs-lookup"><span data-stu-id="9b70c-138">This could happen if hello customization of hello notification in hello app generates an exception which we catch in hello SDK and drop hello message.</span></span> <span data-ttu-id="9b70c-139">Isso também pode ocorrer se Olá aplicativo no dispositivo hello está usando uma versão do SDK do Mobile Engagement que não é capaz de toounderstand hello mais recente versão da mensagem de saudação do envio de saudação enviadas de plataforma hello, mas isso é somente quando o aplicativo hello foi atualizado após a notificação de saudação foi distribuída de plataforma de saudação do serviço.</span><span class="sxs-lookup"><span data-stu-id="9b70c-139">This could also occur if hello app on hello device is using a version of hello Mobile Engagement SDK which is not able toounderstand hello newer version of hello push message sent from hello platform but this is only when hello app was upgraded after hello notification was dispatched from hello service platform.</span></span> <span data-ttu-id="9b70c-140">Olá **avançado** guia informará quantas mensagens foram descartadas.</span><span class="sxs-lookup"><span data-stu-id="9b70c-140">hello **Advanced** tab will tell how many messages were dropped.</span></span> 
   4. <span data-ttu-id="9b70c-141">Em dispositivos iOS, mensagens, às vezes, não obter entregue se qualquer dispositivo hello está funcionando com bateria baixa ou se o aplicativo hello está consumindo uma quantidade significativa de energia durante o processamento de notificações remotas.</span><span class="sxs-lookup"><span data-stu-id="9b70c-141">On iOS devices, messages sometimes do not get delivered if either hello device is on low battery or if hello app is consuming significant amount of power when processing remote notifications.</span></span> <span data-ttu-id="9b70c-142">Essa é uma limitação de dispositivos iOS de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b70c-142">This is a limitation of hello iOS devices.</span></span>   
3. <span data-ttu-id="9b70c-143">**Exibido** -Isso especifica o número de saudação de mensagens com êxito mostrados toohello usuário de aplicativo no dispositivo de saudação na forma de saudação de uma notificação de push/fora-de-aplicativo de sistema no Centro de notificação de saudação ou uma notificação no aplicativo em hello móvel aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9b70c-143">**Displayed** - This specifies hello number of messages which are successfully shown toohello app user on hello device in hello form of a system push/out-of-app notification in hello notification center or an in-app notification within hello mobile app.</span></span>  <span data-ttu-id="9b70c-144">Olá **avançado** guia lhe indicará quantos foram notificações do sistema e quantos foram notificações no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9b70c-144">hello **Advanced** tab will tell you how many were system notifications and how many were in-app notifications.</span></span> 
   
   <span data-ttu-id="9b70c-145">*Motivos para exibidas contagem seja menor que a contagem de entregues (espera toobe exibido)*</span><span class="sxs-lookup"><span data-stu-id="9b70c-145">*Reasons for Displayed count being less than Delivered count (waiting toobe displayed)*</span></span>
   
   1. <span data-ttu-id="9b70c-146">Se a campanha de notificação Olá tinha uma data de término nele e em seguida, é possível que Olá notificação foi entregue, mas quando o tempo de saudação veio tooopen e exiba-o usuário do aplicativo toohello, ele já expirou para que ele nunca foi exibido.</span><span class="sxs-lookup"><span data-stu-id="9b70c-146">If hello notification campaign had an end date on it then it is possible that hello notification was delivered but when hello time came tooopen and display it toohello app user, it was already expired so it was never displayed.</span></span>   
   2. <span data-ttu-id="9b70c-147">Se a notificação de saudação é uma notificação no aplicativo notificação Olá é exibida apenas quando o usuário do aplicativo hello abre o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="9b70c-147">If hello notification is an in-app notification then hello notification is only displayed when hello app user opens hello app.</span></span> <span data-ttu-id="9b70c-148">Em casos onde o usuário de aplicativo hello ainda não abriu o aplicativo hello, Olá SDK relatará que notificação Olá foi entregue, mas ainda não exibida até que o aplicativo hello é aberto.</span><span class="sxs-lookup"><span data-stu-id="9b70c-148">In cases where hello app user hasn't opened hello app, hello SDK will report that hello notification was delivered but not yet displayed until hello app is opened.</span></span> 
   3. <span data-ttu-id="9b70c-149">Se notificação Olá é uma notificação no aplicativo e configurado toobe mostrado em uma determinada atividade/tela também notificação Olá será relatada como fornecidos, mas ainda não foram entregues até que o usuário de Olá abre aplicativo hello em uma tela específica.</span><span class="sxs-lookup"><span data-stu-id="9b70c-149">If hello notification is an in-app notification and configured toobe shown on a specific activity/screen then also hello notification will be reported as delivered but not yet delivered until hello user opens hello app on a specific screen.</span></span> 
4. <span data-ttu-id="9b70c-150">**Interações do usuário** -Especifica Olá número de mensagens de usuário do aplicativo que Olá interagiu com e incluirá mensagens de saudação que são acionadas ou encerradas.</span><span class="sxs-lookup"><span data-stu-id="9b70c-150">**User Interactions** - This specifies hello number of messages which hello app user has interacted with and will include hello messages which are either actioned or exited.</span></span> 
   
   * <span data-ttu-id="9b70c-151">*usuário do aplicativo Hello pode tomar uma ação em uma notificação em uma saudação maneiras a seguir:*</span><span class="sxs-lookup"><span data-stu-id="9b70c-151">*hello app user can action a notification in either of hello following ways:*</span></span>
     
     1. <span data-ttu-id="9b70c-152">Se hello notificação é uma notificação de sistema/fora-de-app ou uma notificação no aplicativo enviado como apenas de notificação e usuário do aplicativo hello clica na notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b70c-152">If hello notification is a system/out-of-app notification or an in-app notification sent as notification-only then hello app user clicks on hello notification.</span></span>
     2. <span data-ttu-id="9b70c-153">Se notificação Olá é uma notificação no aplicativo com um texto ou modo de exibição web ou pesquisas hello, em seguida, o usuário do aplicativo clica no hello botão de ação de notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b70c-153">If hello notification is an in-app notification with a text or web-view or polls then hello app user clicks on hello Action button in hello notification.</span></span>
     3. <span data-ttu-id="9b70c-154">Se a notificação de saudação é uma notificação no aplicativo com uma exibição da web, em seguida, Olá cliques do usuário do aplicativo em uma URL Olá web somente na exibição [Android]</span><span class="sxs-lookup"><span data-stu-id="9b70c-154">If hello notification is an in-app notification with a web-view then hello app user clicks on a URL in hello web view [Android Only]</span></span>
   * <span data-ttu-id="9b70c-155">*usuário do aplicativo Hello pode sair de uma notificação em uma saudação maneiras a seguir:*</span><span class="sxs-lookup"><span data-stu-id="9b70c-155">*hello app user can exit a notification in either of hello following ways:*</span></span>
     
     1. <span data-ttu-id="9b70c-156">Botão de saudação Fechar na notificação de saudação diretamente.</span><span class="sxs-lookup"><span data-stu-id="9b70c-156">Clicking hello close button on hello notification directly.</span></span> 
     2. <span data-ttu-id="9b70c-157">Passar o dedo ausente ou excluindo Olá notificação.</span><span class="sxs-lookup"><span data-stu-id="9b70c-157">Swiping away or deleting hello notification.</span></span> 
     3. <span data-ttu-id="9b70c-158">Notificações no aplicativo com o conteúdo de texto/web e pesquisas são exibidos normalmente toohello usuário de aplicativo em um processo de duas etapas.</span><span class="sxs-lookup"><span data-stu-id="9b70c-158">In-app notifications with text/web content and polls are typically displayed toohello app user in a two-step process.</span></span> <span data-ttu-id="9b70c-159">Eles veem uma notificação pela primeira vez e quando clicar nele, consulte o conteúdo de texto/web/sondagem subsequentes hello.</span><span class="sxs-lookup"><span data-stu-id="9b70c-159">They see a notification first and when they click on it, they see hello subsequent text/web/poll content.</span></span> <span data-ttu-id="9b70c-160">usuário do aplicativo Hello pode sair de uma notificação em qualquer uma dessas etapas e detalhes de saudação na exibição avançada Olá captura isso.</span><span class="sxs-lookup"><span data-stu-id="9b70c-160">hello app user can exit a notification in either of these steps and hello details in hello Advanced view captures this.</span></span> 
5. <span data-ttu-id="9b70c-161">**Acionadas** -Isso especifica o número de saudação de mensagens que foram acionadas explicitamente pelo usuário do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="9b70c-161">**Actioned** - This specifies hello number of messages which were explicitly actioned by hello app user.</span></span> <span data-ttu-id="9b70c-162">Este é o número de mais interessante de saudação como isso informa quantos usuários de aplicativo foram interessados por mensagem de saudação enviado na notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b70c-162">This is hello most interesting number as this tells how many app users were interested by hello message you pushed out in hello notification.</span></span> 

> [!NOTE]
> <span data-ttu-id="9b70c-163">No iOS e plataformas do Windows, se usuário Olá Olá aplicativo abrir e campanha Olá foi uma campanha "A qualquer momento", em seguida, é possível que as notificações do aplicativo e no aplicativo são exibidas em hello simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="9b70c-163">On iOS & Windows platforms, if hello user has hello app open and hello campaign was an "AnyTime" campaign then it is possible that both out of app and in-app notifications are displayed at hello same time.</span></span> <span data-ttu-id="9b70c-164">Isso pode causar uma contagem de exibidas maior Olá entregues.</span><span class="sxs-lookup"><span data-stu-id="9b70c-164">This may cause a Displayed count higher than hello Delivered.</span></span> <span data-ttu-id="9b70c-165">Se usuário Olá interage ou notificação de saudação de ações, Olá, em seguida, até mesmo as interações do usuário/Actioned contagem pode ser maior que entregues.</span><span class="sxs-lookup"><span data-stu-id="9b70c-165">If hello user interacts or actions hello notification, then even hello User Interactions/Actioned count could be greater than Delivered.</span></span> 
> 
> 

![Reach2][19]

## <a name="see-also"></a><span data-ttu-id="9b70c-167">Consulte também</span><span class="sxs-lookup"><span data-stu-id="9b70c-167">See also</span></span>
* <span data-ttu-id="9b70c-168">[Conceitos][Link 6]</span><span class="sxs-lookup"><span data-stu-id="9b70c-168">[Concepts][Link 6]</span></span>
* <span data-ttu-id="9b70c-169">[Serviço do Guia de Solução de Problemas][Link 24]</span><span class="sxs-lookup"><span data-stu-id="9b70c-169">[Troubleshooting Guide Service][Link 24]</span></span>

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

