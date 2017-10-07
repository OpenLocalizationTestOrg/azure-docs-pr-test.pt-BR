---
title: aaaUse Emoji emoticons dentro do Azure Mobile Engagement
description: "Como toouse Emoji emoticons dentro de suas notificações de push"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 663317d7-3c93-4e8f-b13d-c6fb342124ee
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 63bfc59ef472e9fe9aa28b5ac8761017b9250e0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-emoji-emoticon-within-push-notifications"></a><span data-ttu-id="ff325-103">Use o emoticon Emoji em notificações por Push</span><span class="sxs-lookup"><span data-stu-id="ff325-103">Use Emoji emoticon within Push Notifications</span></span>
<span data-ttu-id="ff325-104">Você pode incluir emoticons Emoji em notificações por push em algumas etapas fáceis:</span><span class="sxs-lookup"><span data-stu-id="ff325-104">You can include Emoji emoticons in you push notification in a few easy steps:</span></span> 

1. <span data-ttu-id="ff325-105">Em primeiro lugar, você precisa toofind Olá Emoji deseja toosend na mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="ff325-105">First of all you need toofind hello Emoji you want toosend in hello message.</span></span> <span data-ttu-id="ff325-106">Certifique-se de que Olá Emoji que você está selecionando será suportado pelo dispositivo de destino hello como fabricantes de dispositivo levar algum tempo tooadd plataformas de dispositivo de toohello Emojis aprovadas recentemente.</span><span class="sxs-lookup"><span data-stu-id="ff325-106">Please ensure that hello Emoji you are selecting will be supported by hello target device as device manufactures take some time tooadd newly approved Emojis toohello device platforms.</span></span> 
2. <span data-ttu-id="ff325-107">Em **Windows** -você pode navegar toothis [link](http://apps.timwhitlock.info/emoji/tables/unicode) e ícone para copiar Olá 'Native'.</span><span class="sxs-lookup"><span data-stu-id="ff325-107">On **Windows** - you can navigate toothis [link](http://apps.timwhitlock.info/emoji/tables/unicode) and copy hello 'Native' icon.</span></span>
   
    ![][7] 
3. <span data-ttu-id="ff325-108">Em **Mac** -você pode encontrar hello Emojis no aplicativo de dicionário em Editar -> Emoji & símbolos.</span><span class="sxs-lookup"><span data-stu-id="ff325-108">On **Mac** - you can find hello Emojis in Dictionary application under Edit -> Emoji & Symbols.</span></span>
   
    ![][6] 
4. <span data-ttu-id="ff325-109">Agora, vamos toohello **alcançar** guia no portal do Azure Mobile Engagement Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="ff325-109">Now, go toohello **Reach** tab on hello hello Azure Mobile Engagement portal.</span></span> <span data-ttu-id="ff325-110">Selecione o tipo de saudação de sua notificação por push (anúncio, pesquisa etc).</span><span class="sxs-lookup"><span data-stu-id="ff325-110">Select hello type of your push notification (Announcement, polls etc).</span></span> <span data-ttu-id="ff325-111">Para este exemplo, escolhemos um envio de anúncio.</span><span class="sxs-lookup"><span data-stu-id="ff325-111">For this example we choose an announcement push.</span></span>
5. <span data-ttu-id="ff325-112">Especifica campos diferentes de saudação da notificação de saudação até alcançar o texto de saudação da notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="ff325-112">Specify hello different fields of hello notification until you reach hello text of hello notification.</span></span> <span data-ttu-id="ff325-113">Este é o lugar onde você irá adicionar seu emoticom Emoji.</span><span class="sxs-lookup"><span data-stu-id="ff325-113">This is where you will add your Emoji Emoticon.</span></span> <span data-ttu-id="ff325-114">Você pode escolher tooput no título hello, mensagem de saudação ou ambos.</span><span class="sxs-lookup"><span data-stu-id="ff325-114">You can choose tooput it in hello title, hello message, or both.</span></span> <span data-ttu-id="ff325-115">Você será necessário toodrag e drop ou copie Olá Emoji encontrar locais de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="ff325-115">You will need toodrag and drop or copy hello Emoji that you find from hello locations above.</span></span> 
   
    ![][1]
6. <span data-ttu-id="ff325-116">Concluída Olá outros campos para a notificação de saudação e salvá-lo.</span><span class="sxs-lookup"><span data-stu-id="ff325-116">Complete hello other fields for hello notification and save it.</span></span> 
7. <span data-ttu-id="ff325-117">Quando você executa um teste ou ativar comunicado hello, você verá uma notificação com emoticons Olá conforme especificado.</span><span class="sxs-lookup"><span data-stu-id="ff325-117">When you run a test or activate hello announcement you will see a notification with hello emoticon as specified.</span></span>   
   
    <span data-ttu-id="ff325-118">![][3] ![][4] ![][5]</span><span class="sxs-lookup"><span data-stu-id="ff325-118">![][3] ![][4] ![][5]</span></span>

<!-- Images. -->
[1]: ./media/mobile-engagement-use-emoji-with-push/notification_input.png
[3]: ./media/mobile-engagement-use-emoji-with-push/iOS_Emoji.png
[4]: ./media/mobile-engagement-use-emoji-with-push/Android_Emoji.png
[5]: ./media/mobile-engagement-use-emoji-with-push/WindowsPhone_Emoji.png
[6]: ./media/mobile-engagement-use-emoji-with-push/Mac_SelectEmoji.png
[7]: ./media/mobile-engagement-use-emoji-with-push/Windows_SelectEmoji.png

