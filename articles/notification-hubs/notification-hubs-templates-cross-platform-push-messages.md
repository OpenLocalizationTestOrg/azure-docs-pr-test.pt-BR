---
title: Modelos
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
ms.openlocfilehash: 1ca24a4bf08ecdbe1c1e47a931613144309a04a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="templates"></a><span data-ttu-id="d22ee-103">Modelos</span><span class="sxs-lookup"><span data-stu-id="d22ee-103">Templates</span></span>
## <a name="overview"></a><span data-ttu-id="d22ee-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d22ee-104">Overview</span></span>
<span data-ttu-id="d22ee-105">Os modelos permitem que um aplicativo cliente especifique o formato exato das notificações que deseja receber.</span><span class="sxs-lookup"><span data-stu-id="d22ee-105">Templates enable a client application to specify the exact format of the notifications it wants to receive.</span></span> <span data-ttu-id="d22ee-106">Ao usar modelos, um aplicativo pode reconhecer diversos benefícios diferentes, incluindo os seguintes:</span><span class="sxs-lookup"><span data-stu-id="d22ee-106">Using templates, an app can realize several different benefits, including the following :</span></span>

* <span data-ttu-id="d22ee-107">Um back-end independente de plataforma</span><span class="sxs-lookup"><span data-stu-id="d22ee-107">A platform-agnostic backend</span></span>
* <span data-ttu-id="d22ee-108">Notificações personalizadas</span><span class="sxs-lookup"><span data-stu-id="d22ee-108">Personalized notifications</span></span>
* <span data-ttu-id="d22ee-109">Independência da versão do cliente</span><span class="sxs-lookup"><span data-stu-id="d22ee-109">Client-version independence</span></span>
* <span data-ttu-id="d22ee-110">Localização fácil</span><span class="sxs-lookup"><span data-stu-id="d22ee-110">Easy localization</span></span>

<span data-ttu-id="d22ee-111">Esta seção fornece dois exemplos detalhados de como usar modelos para enviar notificações independentes de plataformas ao direcionar todos os dispositivos em plataformas e para personalizar a notificação de difusão para cada dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d22ee-111">This section provides two in-depth examples of how to use templates to send platform-agnostic notifications targeting all your devices across platforms, and to personalize broadcast notification to each device.</span></span>

## <a name="using-templates-cross-platform"></a><span data-ttu-id="d22ee-112">Como usar modelos de plataforma cruzada</span><span class="sxs-lookup"><span data-stu-id="d22ee-112">Using templates cross-platform</span></span>
<span data-ttu-id="d22ee-113">O modo padrão para enviar notificações por push é enviar, para cada notificação que será enviada, uma carga específica aos serviços de notificação de plataforma (WNS, APNS).</span><span class="sxs-lookup"><span data-stu-id="d22ee-113">The standard way to send push notifications is to send, for each notification that is to be sent, a specific payload to platform notification services (WNS, APNS).</span></span> <span data-ttu-id="d22ee-114">Por exemplo, para enviar um alerta para APNS, a carga é um objeto JSON da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="d22ee-114">For example, to send an alert to APNS, the payload is a Json object of the following form:</span></span>

    {"aps": {"alert" : "Hello!" }}

<span data-ttu-id="d22ee-115">Para enviar uma mensagem de notificação do sistema semelhante em um aplicativo da Windows Store, a carga XML é a seguinte:</span><span class="sxs-lookup"><span data-stu-id="d22ee-115">To send a similar toast message on a Windows Store application, the XML payload is as follows:</span></span>

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">Hello!</text>
        </binding>
      </visual>
    </toast>

<span data-ttu-id="d22ee-116">Você pode criar cargas similares para MPNS (Windows Phone) e para plataformas de GCM (Android).</span><span class="sxs-lookup"><span data-stu-id="d22ee-116">You can create similar payloads for MPNS (Windows Phone) and GCM (Android) platforms.</span></span>

<span data-ttu-id="d22ee-117">Esse requisito força o back-end do aplicativo a produzir cargas diferentes para cada plataforma e torna o back-end responsável por parte da camada de apresentação do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d22ee-117">This requirement forces the app backend to produce different payloads for each platform, and effectively makes the backend responsible for part of the presentation layer of the app.</span></span> <span data-ttu-id="d22ee-118">Algumas questões incluem a localização e layouts gráficos (especialmente para aplicativos da Windows Store que englobam notificações para vários tipos de blocos).</span><span class="sxs-lookup"><span data-stu-id="d22ee-118">Some concerns include localization and graphical layouts (especially for Windows Store apps that include notifications for various types of tiles).</span></span>

<span data-ttu-id="d22ee-119">O recurso de modelo de Hubs de Notificação permite que um aplicativo cliente crie registros especiais, chamados registros modelos, que abrangem, além do conjunto de marcas, um modelo.</span><span class="sxs-lookup"><span data-stu-id="d22ee-119">The Notification Hubs template feature enables a client app to create special registrations, called template registrations, which include, in addition to the set of tags, a template.</span></span> <span data-ttu-id="d22ee-120">O recurso modelo dos Hubs de Notificação permite que um aplicativo cliente associe os dispositivos com modelos se você estiver trabalhando com instalações (preferidas) ou Registros.</span><span class="sxs-lookup"><span data-stu-id="d22ee-120">The Notification Hubs template feature enables a client app to associate devices with templates whether you are working with Installations (preferred) or Registrations.</span></span> <span data-ttu-id="d22ee-121">Considerando os exemplos anteriores de carga, a única informação independente de plataforma é a mensagem de alerta real (Olá!).</span><span class="sxs-lookup"><span data-stu-id="d22ee-121">Given the preceding payload examples, the only platform-independent information is the actual alert message (Hello!).</span></span> <span data-ttu-id="d22ee-122">Um modelo é um conjunto de instruções para o Hub de Notificação sobre como formatar uma mensagem independente de plataforma para o registro daquele aplicativo cliente específico.</span><span class="sxs-lookup"><span data-stu-id="d22ee-122">A template is a set of instructions for the Notification Hub on how to format a platform-independent message for the registration of that specific client app.</span></span> <span data-ttu-id="d22ee-123">No exemplo anterior, a mensagem independente de plataforma é uma propriedade única: **message = Olá!**.</span><span class="sxs-lookup"><span data-stu-id="d22ee-123">In the preceding example, the platform independent message is a single property: **message = Hello!**.</span></span>

<span data-ttu-id="d22ee-124">A figura a seguir ilustra o processo acima:</span><span class="sxs-lookup"><span data-stu-id="d22ee-124">The following picture illustrates the above process:</span></span>

![](./media/notification-hubs-templates/notification-hubs-hello.png)

<span data-ttu-id="d22ee-125">O modelo para o registro do aplicativo cliente iOS é como segue:</span><span class="sxs-lookup"><span data-stu-id="d22ee-125">The template for the iOS client app registration is as follows:</span></span>

    {"aps": {"alert": "$(message)"}}

<span data-ttu-id="d22ee-126">O modelo correspondente para o aplicativo do cliente da Windows Store é:</span><span class="sxs-lookup"><span data-stu-id="d22ee-126">The corresponding template for the Windows Store client app is:</span></span>

    <toast>
        <visual>
            <binding template=\"ToastText01\">
                <text id=\"1\">$(message)</text>
            </binding>
        </visual>
    </toast>

<span data-ttu-id="d22ee-127">Observe que a mensagem real é substituída pela expressão $(message).</span><span class="sxs-lookup"><span data-stu-id="d22ee-127">Notice that the actual message is substituted for the expression $(message).</span></span> <span data-ttu-id="d22ee-128">A expressão instrui o Hub de Notificação, sempre que ele envia uma mensagem para este determinado registro, para compilar uma mensagem que segue a ele e aos comutadores no valor comum.</span><span class="sxs-lookup"><span data-stu-id="d22ee-128">This expression instructs the Notification Hub, whenever it sends a message to this particular registration, to build a message that follows it and switches in the common value.</span></span>

<span data-ttu-id="d22ee-129">Se você estiver trabalhando com o modelo de instalação, a chave de instalação “modelos” terá uma JSON de vários modelos.</span><span class="sxs-lookup"><span data-stu-id="d22ee-129">If you are working with Installation model, the installation “templates” key holds a JSON of multiple templates.</span></span> <span data-ttu-id="d22ee-130">Se você estiver trabalhando com o modelo de registro, o aplicativo cliente poderá criar vários registros para usar vários modelos. Por exemplo, um modelo para mensagens de alerta e um modelo para atualizações de bloco.</span><span class="sxs-lookup"><span data-stu-id="d22ee-130">If you are working with Registration model, the client application can create multiple registrations in order to use multiple templates; for example, a template for alert messages and a template for tile updates.</span></span> <span data-ttu-id="d22ee-131">Os aplicativos clientes também podem mesclar registros nativos (registros sem um modelo) e registros de modelo.</span><span class="sxs-lookup"><span data-stu-id="d22ee-131">Client applications can also mix native registrations (registrations with no template) and template registrations.</span></span>

<span data-ttu-id="d22ee-132">O Hub de Notificação envia uma notificação para cada modelo sem considerar se eles pertencem ao mesmo aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="d22ee-132">The Notification Hub sends one notification for each template without considering whether they belong to the same client app.</span></span> <span data-ttu-id="d22ee-133">Esse comportamento pode ser usado para converter notificações independentes de plataforma em mais notificações.</span><span class="sxs-lookup"><span data-stu-id="d22ee-133">This behavior can be used to translate platform-independent notifications into more notifications.</span></span> <span data-ttu-id="d22ee-134">Por exemplo, a mesma mensagem independente de plataforma para o Hub de Notificação pode ser convertida em um alerta de notificação do sistema e uma atualização de bloco, sem a necessidade de back-end para estar ciente dele.</span><span class="sxs-lookup"><span data-stu-id="d22ee-134">For example, the same platform independent message to the Notification Hub can be seamlessly translated in a toast alert and a tile update, without requiring the backend to be aware of it.</span></span> <span data-ttu-id="d22ee-135">Observe que algumas plataformas (por exemplo, iOS) podem recolher diversas notificações no mesmo dispositivo se elas forem enviadas em um curto período de tempo.</span><span class="sxs-lookup"><span data-stu-id="d22ee-135">Note that some platforms (for example, iOS) might collapse multiple notifications to the same device if they are sent in a short period of time.</span></span>

## <a name="using-templates-for-personalization"></a><span data-ttu-id="d22ee-136">Como usar modelos para personalização</span><span class="sxs-lookup"><span data-stu-id="d22ee-136">Using templates for personalization</span></span>
<span data-ttu-id="d22ee-137">Outra vantagem de usar modelos é a capacidade de usar os Hubs de Notificação para realizar a personalização por registro de notificações.</span><span class="sxs-lookup"><span data-stu-id="d22ee-137">Another advantage to using templates is the ability to use Notification Hubs to perform per-registration personalization of notifications.</span></span> <span data-ttu-id="d22ee-138">Por exemplo, considere um aplicativo sobre clima que exibe um bloco com as condições climáticas em um local específico.</span><span class="sxs-lookup"><span data-stu-id="d22ee-138">For example, consider a weather app that displays a tile with the weather conditions at a specific location.</span></span> <span data-ttu-id="d22ee-139">Um usuário pode escolher entre graus Celsius ou Fahrenheit e uma previsão única ou de cinco dias.</span><span class="sxs-lookup"><span data-stu-id="d22ee-139">A user can choose between Celsius or Fahrenheit degrees, and a single or five-day forecast.</span></span> <span data-ttu-id="d22ee-140">Ao usar modelos, cada instalação do aplicativo cliente pode registrar para o formato necessário (1 dia Celsius, 1 dia Fahrenheit, 5 dias Celsius, 5 dias Fahrenheit) e o back-end pode enviar uma única mensagem que contenha todas as informações necessárias para preencher esses modelos (por exemplo, uma previsão de cinco dias com graus Celsius e Fahrenheit).</span><span class="sxs-lookup"><span data-stu-id="d22ee-140">Using templates, each client app installation can register for the format required (1-day Celsius, 1-day Fahrenheit, 5-days Celsius, 5-days Fahrenheit), and have the backend send a single message that contains all the information required to fill those templates (for example, a five-day forecast with Celsius and Fahrenheit degrees).</span></span>

<span data-ttu-id="d22ee-141">O modelo para a previsão de um dia com temperaturas em graus Celsius é como segue:</span><span class="sxs-lookup"><span data-stu-id="d22ee-141">The template for the one-day forecast with Celsius temperatures is as follows:</span></span>

    <tile>
      <visual>
        <binding template="TileWideSmallImageAndText04">
          <image id="1" src="$(day1_image)" alt="alt text"/>
          <text id="1">Seattle, WA</text>
          <text id="2">$(day1_tempC)</text>
        </binding>  
      </visual>
    </tile>

<span data-ttu-id="d22ee-142">A mensagem enviada ao Hub de Notificação contém as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="d22ee-142">The message sent to the Notification Hub contains all the following properties:</span></span>

<table border="1">

<tr><td><span data-ttu-id="d22ee-143">day1_image</span><span class="sxs-lookup"><span data-stu-id="d22ee-143">day1_image</span></span></td><td><span data-ttu-id="d22ee-144">day2_image</span><span class="sxs-lookup"><span data-stu-id="d22ee-144">day2_image</span></span></td><td><span data-ttu-id="d22ee-145">day3_image</span><span class="sxs-lookup"><span data-stu-id="d22ee-145">day3_image</span></span></td><td><span data-ttu-id="d22ee-146">day4_image</span><span class="sxs-lookup"><span data-stu-id="d22ee-146">day4_image</span></span></td><td><span data-ttu-id="d22ee-147">day5_image</span><span class="sxs-lookup"><span data-stu-id="d22ee-147">day5_image</span></span></td></tr>

<tr><td><span data-ttu-id="d22ee-148">day1_tempC</span><span class="sxs-lookup"><span data-stu-id="d22ee-148">day1_tempC</span></span></td><td><span data-ttu-id="d22ee-149">day2_tempC</span><span class="sxs-lookup"><span data-stu-id="d22ee-149">day2_tempC</span></span></td><td><span data-ttu-id="d22ee-150">day3_tempC</span><span class="sxs-lookup"><span data-stu-id="d22ee-150">day3_tempC</span></span></td><td><span data-ttu-id="d22ee-151">day4_tempC</span><span class="sxs-lookup"><span data-stu-id="d22ee-151">day4_tempC</span></span></td><td><span data-ttu-id="d22ee-152">day5_tempC</span><span class="sxs-lookup"><span data-stu-id="d22ee-152">day5_tempC</span></span></td></tr>

<tr><td><span data-ttu-id="d22ee-153">day1_tempF</span><span class="sxs-lookup"><span data-stu-id="d22ee-153">day1_tempF</span></span></td><td><span data-ttu-id="d22ee-154">day2_tempF</span><span class="sxs-lookup"><span data-stu-id="d22ee-154">day2_tempF</span></span></td><td><span data-ttu-id="d22ee-155">day3_tempF</span><span class="sxs-lookup"><span data-stu-id="d22ee-155">day3_tempF</span></span></td><td><span data-ttu-id="d22ee-156">day4_tempF</span><span class="sxs-lookup"><span data-stu-id="d22ee-156">day4_tempF</span></span></td><td><span data-ttu-id="d22ee-157">day5_tempF</span><span class="sxs-lookup"><span data-stu-id="d22ee-157">day5_tempF</span></span></td></tr>
</table><br/>

<span data-ttu-id="d22ee-158">Ao usar esse padrão, o back-end envia apenas uma única mensagem sem ter que armazenar opções de personalização específicas para os usuários do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d22ee-158">By using this pattern, the backend only sends a single message without having to store specific personalization options for the app users.</span></span> <span data-ttu-id="d22ee-159">A figura a seguir ilustra esse cenário:</span><span class="sxs-lookup"><span data-stu-id="d22ee-159">The following picture illustrates this scenario:</span></span>

![](./media/notification-hubs-templates/notification-hubs-registration-specific.png)

## <a name="how-to-register-templates"></a><span data-ttu-id="d22ee-160">Como registrar modelos</span><span class="sxs-lookup"><span data-stu-id="d22ee-160">How to register templates</span></span>
<span data-ttu-id="d22ee-161">Para registrar usando modelos de instalação (preferencial) ou o modelo de registro, consulte a seção [Gerenciamento de registro](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="d22ee-161">To register with templates using the Installation model (preferred), or the Registration model, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span></span>

## <a name="template-expression-language"></a><span data-ttu-id="d22ee-162">Linguagem de expressão do modelo</span><span class="sxs-lookup"><span data-stu-id="d22ee-162">Template expression language</span></span>
<span data-ttu-id="d22ee-163">Os modelos são limitados aos formatos de documento XML ou JSON.</span><span class="sxs-lookup"><span data-stu-id="d22ee-163">Templates are limited to XML or JSON document formats.</span></span> <span data-ttu-id="d22ee-164">Além disso, só é possível usar expressões em determinados locais. Por exemplo, os atributos de nó ou valores para XML, cadeia de valores de propriedade para JSON.</span><span class="sxs-lookup"><span data-stu-id="d22ee-164">Also, you can only place expressions in particular places; for example, node attributes or values for XML, string property values for JSON.</span></span>

<span data-ttu-id="d22ee-165">A tabela a seguir mostra a linguagem permitida nos modelos:</span><span class="sxs-lookup"><span data-stu-id="d22ee-165">The following table shows the language allowed in templates:</span></span>

| <span data-ttu-id="d22ee-166">Expressão</span><span class="sxs-lookup"><span data-stu-id="d22ee-166">Expression</span></span> | <span data-ttu-id="d22ee-167">Descrição</span><span class="sxs-lookup"><span data-stu-id="d22ee-167">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d22ee-168">$(prop)</span><span class="sxs-lookup"><span data-stu-id="d22ee-168">$(prop)</span></span> |<span data-ttu-id="d22ee-169">Referência para uma propriedade de evento com o nome fornecido.</span><span class="sxs-lookup"><span data-stu-id="d22ee-169">Reference to an event property with the given name.</span></span> <span data-ttu-id="d22ee-170">Os nomes de propriedade não diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="d22ee-170">Property names are not case-sensitive.</span></span> <span data-ttu-id="d22ee-171">Esta expressão é convertida para o valor de texto da propriedade ou em uma sequência de caracteres vazia se a propriedade não estiver presente.</span><span class="sxs-lookup"><span data-stu-id="d22ee-171">This expression resolves into the property’s text value or into an empty string if the property is not present.</span></span> |
| <span data-ttu-id="d22ee-172">$(prop, n)</span><span class="sxs-lookup"><span data-stu-id="d22ee-172">$(prop, n)</span></span> |<span data-ttu-id="d22ee-173">Como consta acima, mas o texto é explicitamente cortado em n caracteres, por exemplo, $(title, 20) corta o conteúdo da propriedade de título em 20 caracteres.</span><span class="sxs-lookup"><span data-stu-id="d22ee-173">As above, but the text is explicitly clipped at n characters, for example $(title, 20) clips the contents of the title property at 20 characters.</span></span> |
| <span data-ttu-id="d22ee-174">.(prop, n)</span><span class="sxs-lookup"><span data-stu-id="d22ee-174">.(prop, n)</span></span> |<span data-ttu-id="d22ee-175">Como consta acima, mas o texto é sufixado com três pontos quando é cortado.</span><span class="sxs-lookup"><span data-stu-id="d22ee-175">As above, but the text is suffixed with three dots as it is clipped.</span></span> <span data-ttu-id="d22ee-176">O tamanho total da cadeia de caracteres cortada e do sufixo não excede n caracteres.</span><span class="sxs-lookup"><span data-stu-id="d22ee-176">The total size of the clipped string and the suffix does not exceed n characters.</span></span> <span data-ttu-id="d22ee-177">.(title, 20) com uma propriedade de entrada de "Esta é a linha de título" resulta em **Este é o título...**</span><span class="sxs-lookup"><span data-stu-id="d22ee-177">.(title, 20) with an input property of “This is the title line” results in **This is the title...**</span></span> |
| <span data-ttu-id="d22ee-178">%(prop)</span><span class="sxs-lookup"><span data-stu-id="d22ee-178">%(prop)</span></span> |<span data-ttu-id="d22ee-179">Semelhante ao $(name), exceto que a saída é codificada para URI.</span><span class="sxs-lookup"><span data-stu-id="d22ee-179">Similar to $(name) except that the output is URI-encoded.</span></span> |
| <span data-ttu-id="d22ee-180">#(prop)</span><span class="sxs-lookup"><span data-stu-id="d22ee-180">#(prop)</span></span> |<span data-ttu-id="d22ee-181">Usada em modelos JSON (por exemplo, para modelos iOS e Android).</span><span class="sxs-lookup"><span data-stu-id="d22ee-181">Used in JSON templates (for example, for iOS and Android templates).</span></span><br><br><span data-ttu-id="d22ee-182">Essa função funciona exatamente como $(prop) anteriormente especificada, exceto quando usada em modelos JSON (por exemplo, modelos Apple).</span><span class="sxs-lookup"><span data-stu-id="d22ee-182">This function works exactly the same as $(prop) previously specified, except when used in JSON templates (for example, Apple templates).</span></span> <span data-ttu-id="d22ee-183">Nesse caso, se essa função não for delimitada por "{','}" (por exemplo, 'myJsonProperty': '#(name)') e for avaliada como um número em formato Javascript, por exemplo,regexp: (0&#124;(&#91;1-9&#93;&#91;0-9&#93;*))(\.&#91;0-9&#93;+)?((e&#124;E)(+&#124;-)?&#91;0-9&#93;+)?, a saída JSON será um número.</span><span class="sxs-lookup"><span data-stu-id="d22ee-183">In this case, if this function is not surrounded by “{‘,’}” (for example, ‘myJsonProperty’ : ‘#(name)’), and it evaluates to a number in Javascript format, for example, regexp: (0&#124;(&#91;1-9&#93;&#91;0-9&#93;*))(\.&#91;0-9&#93;+)?((e&#124;E)(+&#124;-)?&#91;0-9&#93;+)?, then the output JSON is a number.</span></span><br><br><span data-ttu-id="d22ee-184">Por exemplo, ‘badge : ‘#(name)’se torna 'badge': 40 (e não ‘40‘).</span><span class="sxs-lookup"><span data-stu-id="d22ee-184">For example, ‘badge : ‘#(name)’ becomes ‘badge’ : 40 (and not ‘40‘).</span></span> |
| <span data-ttu-id="d22ee-185">'texto' ou "texto"</span><span class="sxs-lookup"><span data-stu-id="d22ee-185">‘text’ or “text”</span></span> |<span data-ttu-id="d22ee-186">Um literal.</span><span class="sxs-lookup"><span data-stu-id="d22ee-186">A literal.</span></span> <span data-ttu-id="d22ee-187">Literais contêm texto arbitrário entre aspas simples ou duplas.</span><span class="sxs-lookup"><span data-stu-id="d22ee-187">Literals contain arbitrary text enclosed in single or double quotes.</span></span> |
| <span data-ttu-id="d22ee-188">expr1 + expr2</span><span class="sxs-lookup"><span data-stu-id="d22ee-188">expr1 + expr2</span></span> |<span data-ttu-id="d22ee-189">O operador de concatenação que une duas expressões em uma única cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="d22ee-189">The concatenation operator joining two expressions into a single string.</span></span> |

<span data-ttu-id="d22ee-190">As expressões podem ter qualquer uma das formas anteriores.</span><span class="sxs-lookup"><span data-stu-id="d22ee-190">The expressions can be any of the preceding forms.</span></span>

<span data-ttu-id="d22ee-191">Ao usar concatenação, toda a expressão deve estar entre {}.</span><span class="sxs-lookup"><span data-stu-id="d22ee-191">When using concatenation, the entire expression must be surrounded with {}.</span></span> <span data-ttu-id="d22ee-192">Por exemplo, {$(prop) + “ - ” + $(prop2)}.</span><span class="sxs-lookup"><span data-stu-id="d22ee-192">For example, {$(prop) + ‘ - ’ + $(prop2)}.</span></span> |

<span data-ttu-id="d22ee-193">Por exemplo, o seguinte não é um modelo XML válido:</span><span class="sxs-lookup"><span data-stu-id="d22ee-193">For example, the following is not a valid XML template:</span></span>

    <tile>
      <visual>
        <binding $(property)>
          <text id="1">Seattle, WA</text>
        </binding>  
      </visual>
    </tile>


<span data-ttu-id="d22ee-194">Como explicado acima, ao usar concatenação, as expressões devem ser colocadas entre colchetes.</span><span class="sxs-lookup"><span data-stu-id="d22ee-194">As explained above, when using concatenation, expressions must be wrapped in curly brackets.</span></span> <span data-ttu-id="d22ee-195">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="d22ee-195">For example:</span></span>

    <tile>
      <visual>
        <binding template="ToastText01">
          <text id="1">{'Hi, ' + $(name)}</text>
        </binding>  
      </visual>
    </tile>

