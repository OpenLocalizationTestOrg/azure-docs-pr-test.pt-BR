---
title: aaaTemplates
description: "Este tópico explica os modelos de hubs de notificação do Azure."
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: a41897bb-5b4b-48b2-bfd5-2e3c65edc37e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 0149f0c7473e5a4b952905bc8217582b58db2a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="templates"></a><span data-ttu-id="e1bc0-103">Modelos</span><span class="sxs-lookup"><span data-stu-id="e1bc0-103">Templates</span></span>
## <a name="overview"></a><span data-ttu-id="e1bc0-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="e1bc0-104">Overview</span></span>
<span data-ttu-id="e1bc0-105">Os modelos permitem a um cliente aplicativo toospecify Olá formato exato das notificações de saudação que ele deseja tooreceive.</span><span class="sxs-lookup"><span data-stu-id="e1bc0-105">Templates enable a client application toospecify hello exact format of hello notifications it wants tooreceive.</span></span> <span data-ttu-id="e1bc0-106">Usando modelos, um aplicativo pode obter várias vantagens, incluindo Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="e1bc0-106">Using templates, an app can realize several different benefits, including hello following :</span></span>

* <span data-ttu-id="e1bc0-107">Um back-end independente de plataforma</span><span class="sxs-lookup"><span data-stu-id="e1bc0-107">A platform-agnostic backend</span></span>
* <span data-ttu-id="e1bc0-108">Notificações personalizadas</span><span class="sxs-lookup"><span data-stu-id="e1bc0-108">Personalized notifications</span></span>
* <span data-ttu-id="e1bc0-109">Independência da versão do cliente</span><span class="sxs-lookup"><span data-stu-id="e1bc0-109">Client-version independence</span></span>
* <span data-ttu-id="e1bc0-110">Localização fácil</span><span class="sxs-lookup"><span data-stu-id="e1bc0-110">Easy localization</span></span>

<span data-ttu-id="e1bc0-111">Esta seção fornece dois exemplos detalhados de como as notificações de independente de plataforma toosend modelos toouse direcionamento todos os seus dispositivos em plataformas e toopersonalize difusão tooeach de dispositivo de notificação.</span><span class="sxs-lookup"><span data-stu-id="e1bc0-111">This section provides two in-depth examples of how toouse templates toosend platform-agnostic notifications targeting all your devices across platforms, and toopersonalize broadcast notification tooeach device.</span></span>

## <a name="using-templates-cross-platform"></a><span data-ttu-id="e1bc0-112">Como usar modelos de plataforma cruzada</span><span class="sxs-lookup"><span data-stu-id="e1bc0-112">Using templates cross-platform</span></span>
<span data-ttu-id="e1bc0-113">as notificações por push do Hello maneira padrão toosend é toosend, para cada notificação é enviada, de toobe serviços de notificação de tooplatform uma carga específica (WNS, APNS).</span><span class="sxs-lookup"><span data-stu-id="e1bc0-113">hello standard way toosend push notifications is toosend, for each notification that is toobe sent, a specific payload tooplatform notification services (WNS, APNS).</span></span> <span data-ttu-id="e1bc0-114">Por exemplo, toosend tooAPNS um alerta, a carga de saudação é um objeto Json de saudação formulário a seguir:</span><span class="sxs-lookup"><span data-stu-id="e1bc0-114">For example, toosend an alert tooAPNS, hello payload is a Json object of hello following form:</span></span>

    {"aps": {"alert" : "Hello!" }}

<span data-ttu-id="e1bc0-115">toosend uma mensagem de notificação do sistema semelhante em um aplicativo da Windows Store, Olá XML carga é da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e1bc0-115">toosend a similar toast message on a Windows Store application, hello XML payload is as follows:</span></span>

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">Hello!</text>
        </binding>
      </visual>
    </toast>

<span data-ttu-id="e1bc0-116">Você pode criar cargas similares para MPNS (Windows Phone) e para plataformas de GCM (Android).</span><span class="sxs-lookup"><span data-stu-id="e1bc0-116">You can create similar payloads for MPNS (Windows Phone) and GCM (Android) platforms.</span></span>

<span data-ttu-id="e1bc0-117">Esse requisito força Olá aplicativo back-end tooproduce diferentes cargas para cada plataforma e efetivamente faz Olá back-end responsável por parte da camada de apresentação de saudação do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="e1bc0-117">This requirement forces hello app backend tooproduce different payloads for each platform, and effectively makes hello backend responsible for part of hello presentation layer of hello app.</span></span> <span data-ttu-id="e1bc0-118">Algumas questões incluem a localização e layouts gráficos (especialmente para aplicativos da Windows Store que englobam notificações para vários tipos de blocos).</span><span class="sxs-lookup"><span data-stu-id="e1bc0-118">Some concerns include localization and graphical layouts (especially for Windows Store apps that include notifications for various types of tiles).</span></span>

<span data-ttu-id="e1bc0-119">recurso de modelo de Hubs de notificação de Olá permite que um aplicativo toocreate especiais registros de clientes, chamado de registros do modelo, que incluem, além de toohello conjunto de marcas, um modelo.</span><span class="sxs-lookup"><span data-stu-id="e1bc0-119">hello Notification Hubs template feature enables a client app toocreate special registrations, called template registrations, which include, in addition toohello set of tags, a template.</span></span> <span data-ttu-id="e1bc0-120">recurso de modelo do Hello Hubs de notificação permite que um dispositivo de tooassociate do aplicativo cliente com modelos se você estiver trabalhando com instalações (preferidas) ou registros.</span><span class="sxs-lookup"><span data-stu-id="e1bc0-120">hello Notification Hubs template feature enables a client app tooassociate devices with templates whether you are working with Installations (preferred) or Registrations.</span></span> <span data-ttu-id="e1bc0-121">Considerando Olá anterior exemplos de carga, hello apenas informações de independente de plataforma são Olá real alerta mensagem (Olá!).</span><span class="sxs-lookup"><span data-stu-id="e1bc0-121">Given hello preceding payload examples, hello only platform-independent information is hello actual alert message (Hello!).</span></span> <span data-ttu-id="e1bc0-122">Um modelo é um conjunto de instruções para Olá Hub de notificação em como tooformat um independente de plataforma de mensagens para o registro de saudação do que o aplicativo cliente específico.</span><span class="sxs-lookup"><span data-stu-id="e1bc0-122">A template is a set of instructions for hello Notification Hub on how tooformat a platform-independent message for hello registration of that specific client app.</span></span> <span data-ttu-id="e1bc0-123">Olá anterior de exemplo, mensagem independente de plataforma de saudação é uma propriedade única: **mensagem = Olá!**.</span><span class="sxs-lookup"><span data-stu-id="e1bc0-123">In hello preceding example, hello platform independent message is a single property: **message = Hello!**.</span></span>

<span data-ttu-id="e1bc0-124">Olá figura abaixo ilustra Olá acima do processo:</span><span class="sxs-lookup"><span data-stu-id="e1bc0-124">hello following picture illustrates hello above process:</span></span>

![](./media/notification-hubs-templates/notification-hubs-hello.png)

<span data-ttu-id="e1bc0-125">modelo de saudação para o registro do aplicativo cliente Olá iOS é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="e1bc0-125">hello template for hello iOS client app registration is as follows:</span></span>

    {"aps": {"alert": "$(message)"}}

<span data-ttu-id="e1bc0-126">saudação de modelo correspondente para o aplicativo de cliente de armazenamento do Windows hello é:</span><span class="sxs-lookup"><span data-stu-id="e1bc0-126">hello corresponding template for hello Windows Store client app is:</span></span>

    <toast>
        <visual>
            <binding template=\"ToastText01\">
                <text id=\"1\">$(message)</text>
            </binding>
        </visual>
    </toast>

<span data-ttu-id="e1bc0-127">Observe que Olá mensagem real é substituído Olá expressão $(mensagem).</span><span class="sxs-lookup"><span data-stu-id="e1bc0-127">Notice that hello actual message is substituted for hello expression $(message).</span></span> <span data-ttu-id="e1bc0-128">Essa expressão instrui Olá Hub de notificação, sempre que ele envia uma mensagem toothis registro específico, toobuild uma mensagem que segue a ele e comutadores no valor comum hello.</span><span class="sxs-lookup"><span data-stu-id="e1bc0-128">This expression instructs hello Notification Hub, whenever it sends a message toothis particular registration, toobuild a message that follows it and switches in hello common value.</span></span>

<span data-ttu-id="e1bc0-129">Se você estiver trabalhando com o modelo de instalação, chave de "modelos" hello instalação contém um JSON de vários modelos.</span><span class="sxs-lookup"><span data-stu-id="e1bc0-129">If you are working with Installation model, hello installation “templates” key holds a JSON of multiple templates.</span></span> <span data-ttu-id="e1bc0-130">Se você estiver trabalhando com o modelo de registro, aplicativo de cliente hello pode criar vários registros em ordem toouse vários modelos; Por exemplo, um modelo para mensagens de alerta e um modelo para atualizações de bloco.</span><span class="sxs-lookup"><span data-stu-id="e1bc0-130">If you are working with Registration model, hello client application can create multiple registrations in order toouse multiple templates; for example, a template for alert messages and a template for tile updates.</span></span> <span data-ttu-id="e1bc0-131">Os aplicativos clientes também podem mesclar registros nativos (registros sem um modelo) e registros de modelo.</span><span class="sxs-lookup"><span data-stu-id="e1bc0-131">Client applications can also mix native registrations (registrations with no template) and template registrations.</span></span>

<span data-ttu-id="e1bc0-132">Olá Hub de notificação envia uma notificação para cada modelo sem considerar se eles pertencem toohello mesmo aplicativo de cliente.</span><span class="sxs-lookup"><span data-stu-id="e1bc0-132">hello Notification Hub sends one notification for each template without considering whether they belong toohello same client app.</span></span> <span data-ttu-id="e1bc0-133">Esse comportamento pode ser usado tootranslate independente de plataforma notificações para notificações de mais.</span><span class="sxs-lookup"><span data-stu-id="e1bc0-133">This behavior can be used tootranslate platform-independent notifications into more notifications.</span></span> <span data-ttu-id="e1bc0-134">Por exemplo, Olá mesmo toohello mensagem independente de plataforma que hub de notificação podem ser convertido diretamente em um alerta de notificação do sistema e uma atualização de bloco, sem a necessidade de toobe de back-end Olá ciente dela.</span><span class="sxs-lookup"><span data-stu-id="e1bc0-134">For example, hello same platform independent message toohello Notification Hub can be seamlessly translated in a toast alert and a tile update, without requiring hello backend toobe aware of it.</span></span> <span data-ttu-id="e1bc0-135">Observe que algumas plataformas (por exemplo, iOS) podem recolher várias toohello de notificações mesmo dispositivo, caso sejam enviadas em um curto período de tempo.</span><span class="sxs-lookup"><span data-stu-id="e1bc0-135">Note that some platforms (for example, iOS) might collapse multiple notifications toohello same device if they are sent in a short period of time.</span></span>

## <a name="using-templates-for-personalization"></a><span data-ttu-id="e1bc0-136">Como usar modelos para personalização</span><span class="sxs-lookup"><span data-stu-id="e1bc0-136">Using templates for personalization</span></span>
<span data-ttu-id="e1bc0-137">Modelos de toousing outra vantagem é Olá capacidade toouse personalização de por registro tooperform Hubs de notificação de notificações.</span><span class="sxs-lookup"><span data-stu-id="e1bc0-137">Another advantage toousing templates is hello ability toouse Notification Hubs tooperform per-registration personalization of notifications.</span></span> <span data-ttu-id="e1bc0-138">Por exemplo, considere um aplicativo de tempo que exibe um bloco com condições de tempo de saudação em um local específico.</span><span class="sxs-lookup"><span data-stu-id="e1bc0-138">For example, consider a weather app that displays a tile with hello weather conditions at a specific location.</span></span> <span data-ttu-id="e1bc0-139">Um usuário pode escolher entre graus Celsius ou Fahrenheit e uma previsão única ou de cinco dias.</span><span class="sxs-lookup"><span data-stu-id="e1bc0-139">A user can choose between Celsius or Fahrenheit degrees, and a single or five-day forecast.</span></span> <span data-ttu-id="e1bc0-140">Usando modelos, cada instalação do aplicativo cliente pode se registrar no formato Olá necessário (1 dia Celsius, 1 dia Fahrenheit, 5 dias Celsius, 5 dias Fahrenheit), e ter Olá back-end enviar uma mensagem única que contém todas as informações de saudação necessária toofill aqueles modelos (por exemplo, um cinco dias de previsão com graus Celsius e Fahrenheit).</span><span class="sxs-lookup"><span data-stu-id="e1bc0-140">Using templates, each client app installation can register for hello format required (1-day Celsius, 1-day Fahrenheit, 5-days Celsius, 5-days Fahrenheit), and have hello backend send a single message that contains all hello information required toofill those templates (for example, a five-day forecast with Celsius and Fahrenheit degrees).</span></span>

<span data-ttu-id="e1bc0-141">modelo de Olá Olá um dia de previsão com Celsius temperaturas é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="e1bc0-141">hello template for hello one-day forecast with Celsius temperatures is as follows:</span></span>

    <tile>
      <visual>
        <binding template="TileWideSmallImageAndText04">
          <image id="1" src="$(day1_image)" alt="alt text"/>
          <text id="1">Seattle, WA</text>
          <text id="2">$(day1_tempC)</text>
        </binding>  
      </visual>
    </tile>

<span data-ttu-id="e1bc0-142">Olá mensagem enviada toohello Hub de notificação contém Olá todas as propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="e1bc0-142">hello message sent toohello Notification Hub contains all hello following properties:</span></span>

<table border="1">

<tr><td><span data-ttu-id="e1bc0-143">day1_image</span><span class="sxs-lookup"><span data-stu-id="e1bc0-143">day1_image</span></span></td><td><span data-ttu-id="e1bc0-144">day2_image</span><span class="sxs-lookup"><span data-stu-id="e1bc0-144">day2_image</span></span></td><td><span data-ttu-id="e1bc0-145">day3_image</span><span class="sxs-lookup"><span data-stu-id="e1bc0-145">day3_image</span></span></td><td><span data-ttu-id="e1bc0-146">day4_image</span><span class="sxs-lookup"><span data-stu-id="e1bc0-146">day4_image</span></span></td><td><span data-ttu-id="e1bc0-147">day5_image</span><span class="sxs-lookup"><span data-stu-id="e1bc0-147">day5_image</span></span></td></tr>

<tr><td><span data-ttu-id="e1bc0-148">day1_tempC</span><span class="sxs-lookup"><span data-stu-id="e1bc0-148">day1_tempC</span></span></td><td><span data-ttu-id="e1bc0-149">day2_tempC</span><span class="sxs-lookup"><span data-stu-id="e1bc0-149">day2_tempC</span></span></td><td><span data-ttu-id="e1bc0-150">day3_tempC</span><span class="sxs-lookup"><span data-stu-id="e1bc0-150">day3_tempC</span></span></td><td><span data-ttu-id="e1bc0-151">day4_tempC</span><span class="sxs-lookup"><span data-stu-id="e1bc0-151">day4_tempC</span></span></td><td><span data-ttu-id="e1bc0-152">day5_tempC</span><span class="sxs-lookup"><span data-stu-id="e1bc0-152">day5_tempC</span></span></td></tr>

<tr><td><span data-ttu-id="e1bc0-153">day1_tempF</span><span class="sxs-lookup"><span data-stu-id="e1bc0-153">day1_tempF</span></span></td><td><span data-ttu-id="e1bc0-154">day2_tempF</span><span class="sxs-lookup"><span data-stu-id="e1bc0-154">day2_tempF</span></span></td><td><span data-ttu-id="e1bc0-155">day3_tempF</span><span class="sxs-lookup"><span data-stu-id="e1bc0-155">day3_tempF</span></span></td><td><span data-ttu-id="e1bc0-156">day4_tempF</span><span class="sxs-lookup"><span data-stu-id="e1bc0-156">day4_tempF</span></span></td><td><span data-ttu-id="e1bc0-157">day5_tempF</span><span class="sxs-lookup"><span data-stu-id="e1bc0-157">day5_tempF</span></span></td></tr>
</table><br/>

<span data-ttu-id="e1bc0-158">Usando esse padrão, Olá back-end apenas envia uma única mensagem sem ter que opções de personalização específicas de toostore para os usuários do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="e1bc0-158">By using this pattern, hello backend only sends a single message without having toostore specific personalization options for hello app users.</span></span> <span data-ttu-id="e1bc0-159">Olá a imagem a seguir ilustra esse cenário:</span><span class="sxs-lookup"><span data-stu-id="e1bc0-159">hello following picture illustrates this scenario:</span></span>

![](./media/notification-hubs-templates/notification-hubs-registration-specific.png)

## <a name="how-tooregister-templates"></a><span data-ttu-id="e1bc0-160">Como modelos de tooregister</span><span class="sxs-lookup"><span data-stu-id="e1bc0-160">How tooregister templates</span></span>
<span data-ttu-id="e1bc0-161">tooregister com modelos usando o modelo de instalação de saudação (preferencial) ou Olá modelo de registro, consulte [Registration Management](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="e1bc0-161">tooregister with templates using hello Installation model (preferred), or hello Registration model, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span></span>

## <a name="template-expression-language"></a><span data-ttu-id="e1bc0-162">Linguagem de expressão do modelo</span><span class="sxs-lookup"><span data-stu-id="e1bc0-162">Template expression language</span></span>
<span data-ttu-id="e1bc0-163">Os modelos são tooXML limitado ou formatos de documentos JSON.</span><span class="sxs-lookup"><span data-stu-id="e1bc0-163">Templates are limited tooXML or JSON document formats.</span></span> <span data-ttu-id="e1bc0-164">Além disso, só é possível usar expressões em determinados locais. Por exemplo, os atributos de nó ou valores para XML, cadeia de valores de propriedade para JSON.</span><span class="sxs-lookup"><span data-stu-id="e1bc0-164">Also, you can only place expressions in particular places; for example, node attributes or values for XML, string property values for JSON.</span></span>

<span data-ttu-id="e1bc0-165">Olá tabela a seguir mostra idioma Olá permitido em modelos:</span><span class="sxs-lookup"><span data-stu-id="e1bc0-165">hello following table shows hello language allowed in templates:</span></span>

| <span data-ttu-id="e1bc0-166">Expression</span><span class="sxs-lookup"><span data-stu-id="e1bc0-166">Expression</span></span> | <span data-ttu-id="e1bc0-167">Descrição</span><span class="sxs-lookup"><span data-stu-id="e1bc0-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e1bc0-168">$(prop)</span><span class="sxs-lookup"><span data-stu-id="e1bc0-168">$(prop)</span></span> |<span data-ttu-id="e1bc0-169">Propriedade de evento de tooan de referência com hello determinado nome.</span><span class="sxs-lookup"><span data-stu-id="e1bc0-169">Reference tooan event property with hello given name.</span></span> <span data-ttu-id="e1bc0-170">Os nomes de propriedade não diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="e1bc0-170">Property names are not case-sensitive.</span></span> <span data-ttu-id="e1bc0-171">Essa expressão é resolvida no valor de texto da propriedade hello ou em uma cadeia de caracteres vazia se não houver propriedade Olá.</span><span class="sxs-lookup"><span data-stu-id="e1bc0-171">This expression resolves into hello property’s text value or into an empty string if hello property is not present.</span></span> |
| <span data-ttu-id="e1bc0-172">$(prop, n)</span><span class="sxs-lookup"><span data-stu-id="e1bc0-172">$(prop, n)</span></span> |<span data-ttu-id="e1bc0-173">Como acima, mas hello texto é explicitamente recortado n caracteres, por exemplo $(título, 20) recorta conteúdo de saudação da propriedade de título de saudação em 20 caracteres.</span><span class="sxs-lookup"><span data-stu-id="e1bc0-173">As above, but hello text is explicitly clipped at n characters, for example $(title, 20) clips hello contents of hello title property at 20 characters.</span></span> |
| <span data-ttu-id="e1bc0-174">.(prop, n)</span><span class="sxs-lookup"><span data-stu-id="e1bc0-174">.(prop, n)</span></span> |<span data-ttu-id="e1bc0-175">Como acima, mas hello texto é com o sufixo três pontos conforme ele é anexado.</span><span class="sxs-lookup"><span data-stu-id="e1bc0-175">As above, but hello text is suffixed with three dots as it is clipped.</span></span> <span data-ttu-id="e1bc0-176">tamanho total de saudação do hello recortado cadeia de caracteres e sufixo Olá não exceda n caracteres.</span><span class="sxs-lookup"><span data-stu-id="e1bc0-176">hello total size of hello clipped string and hello suffix does not exceed n characters.</span></span> <span data-ttu-id="e1bc0-177">. (título, 20) com uma propriedade de entrada de "Esta é a linha de título do hello" resulta em **este é o título de saudação...**</span><span class="sxs-lookup"><span data-stu-id="e1bc0-177">.(title, 20) with an input property of “This is hello title line” results in **This is hello title...**</span></span> |
| <span data-ttu-id="e1bc0-178">%(prop)</span><span class="sxs-lookup"><span data-stu-id="e1bc0-178">%(prop)</span></span> |<span data-ttu-id="e1bc0-179">Too$(name) semelhante, exceto por essa saída Olá URI codificado.</span><span class="sxs-lookup"><span data-stu-id="e1bc0-179">Similar too$(name) except that hello output is URI-encoded.</span></span> |
| <span data-ttu-id="e1bc0-180">#(prop)</span><span class="sxs-lookup"><span data-stu-id="e1bc0-180">#(prop)</span></span> |<span data-ttu-id="e1bc0-181">Usada em modelos JSON (por exemplo, para modelos iOS e Android).</span><span class="sxs-lookup"><span data-stu-id="e1bc0-181">Used in JSON templates (for example, for iOS and Android templates).</span></span><br><br><span data-ttu-id="e1bc0-182">Essa função funciona exatamente iguais Olá como $(prop) especificado anteriormente, exceto quando usado em modelos JSON (por exemplo, modelos de Apple).</span><span class="sxs-lookup"><span data-stu-id="e1bc0-182">This function works exactly hello same as $(prop) previously specified, except when used in JSON templates (for example, Apple templates).</span></span> <span data-ttu-id="e1bc0-183">Nesse caso, se essa função não é delimitada por "{','}" (por exemplo, 'myJsonProperty': '#(nome)'), e ele será avaliado tooa número no formato de Javascript, por exemplo, regexp: (0 &#124;) (&#91; 1-9 &#93; &#91; 0-9 & #93 ;*))(\. &#91; 0-9 &#93; +)? ((e &#124; E) (+ &#124;-)? &#91; 0-9 &#93; +)?, em seguida, Olá saída JSON é um número.</span><span class="sxs-lookup"><span data-stu-id="e1bc0-183">In this case, if this function is not surrounded by “{‘,’}” (for example, ‘myJsonProperty’ : ‘#(name)’), and it evaluates tooa number in Javascript format, for example, regexp: (0&#124;(&#91;1-9&#93;&#91;0-9&#93;*))(\.&#91;0-9&#93;+)?((e&#124;E)(+&#124;-)?&#91;0-9&#93;+)?, then hello output JSON is a number.</span></span><br><br><span data-ttu-id="e1bc0-184">Por exemplo, ‘badge : ‘#(name)’se torna 'badge': 40 (e não ‘40‘).</span><span class="sxs-lookup"><span data-stu-id="e1bc0-184">For example, ‘badge : ‘#(name)’ becomes ‘badge’ : 40 (and not ‘40‘).</span></span> |
| <span data-ttu-id="e1bc0-185">'texto' ou "texto"</span><span class="sxs-lookup"><span data-stu-id="e1bc0-185">‘text’ or “text”</span></span> |<span data-ttu-id="e1bc0-186">Um literal.</span><span class="sxs-lookup"><span data-stu-id="e1bc0-186">A literal.</span></span> <span data-ttu-id="e1bc0-187">Literais contêm texto arbitrário entre aspas simples ou duplas.</span><span class="sxs-lookup"><span data-stu-id="e1bc0-187">Literals contain arbitrary text enclosed in single or double quotes.</span></span> |
| <span data-ttu-id="e1bc0-188">expr1 + expr2</span><span class="sxs-lookup"><span data-stu-id="e1bc0-188">expr1 + expr2</span></span> |<span data-ttu-id="e1bc0-189">operador de concatenação de saudação unindo duas expressões em uma única cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="e1bc0-189">hello concatenation operator joining two expressions into a single string.</span></span> |

<span data-ttu-id="e1bc0-190">expressões de saudação podem ser qualquer Olá anterior formulários.</span><span class="sxs-lookup"><span data-stu-id="e1bc0-190">hello expressions can be any of hello preceding forms.</span></span>

<span data-ttu-id="e1bc0-191">Ao usar a concatenação, toda a expressão Olá deve estar entre {}.</span><span class="sxs-lookup"><span data-stu-id="e1bc0-191">When using concatenation, hello entire expression must be surrounded with {}.</span></span> <span data-ttu-id="e1bc0-192">Por exemplo, {$(prop) + “ - ” + $(prop2)}.</span><span class="sxs-lookup"><span data-stu-id="e1bc0-192">For example, {$(prop) + ‘ - ’ + $(prop2)}.</span></span> |

<span data-ttu-id="e1bc0-193">Por exemplo, o seguinte Olá não é um modelo XML válido:</span><span class="sxs-lookup"><span data-stu-id="e1bc0-193">For example, hello following is not a valid XML template:</span></span>

    <tile>
      <visual>
        <binding $(property)>
          <text id="1">Seattle, WA</text>
        </binding>  
      </visual>
    </tile>


<span data-ttu-id="e1bc0-194">Como explicado acima, ao usar concatenação, as expressões devem ser colocadas entre colchetes.</span><span class="sxs-lookup"><span data-stu-id="e1bc0-194">As explained above, when using concatenation, expressions must be wrapped in curly brackets.</span></span> <span data-ttu-id="e1bc0-195">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e1bc0-195">For example:</span></span>

    <tile>
      <visual>
        <binding template="ToastText01">
          <text id="1">{'Hi, ' + $(name)}</text>
        </binding>  
      </visual>
    </tile>

