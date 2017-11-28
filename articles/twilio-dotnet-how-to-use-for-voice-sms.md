---
title: aaaHow tooUse Twilio para voz e SMS (.NET) | Microsoft Docs
description: "Saiba como toomake uma chamada telefônica e enviar um SMS de mensagem com o serviço de API do Twilio Olá no Azure. Amostras de código gravadas no .NET."
services: 
documentationcenter: .net
author: devinrader
manager: twilio
editor: 
ms.assetid: 74d4f3c9-f1cb-4968-b744-36b32cd0e834
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/24/2015
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: f568da87ef15e9f540fee9674de31e983d4acb6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-from-azure"></a><span data-ttu-id="e438f-104">Como toouse Twilio para recursos SMS do Azure e voz</span><span class="sxs-lookup"><span data-stu-id="e438f-104">How toouse Twilio for voice and SMS capabilities from Azure</span></span>
<span data-ttu-id="e438f-105">Este guia demonstra como tooperform as tarefas de programação comuns com hello Twilio API de serviço no Azure.</span><span class="sxs-lookup"><span data-stu-id="e438f-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="e438f-106">cenários de saudação abordados incluem fazer uma chamada telefônica e enviar uma mensagem do serviço SMS (Short Message).</span><span class="sxs-lookup"><span data-stu-id="e438f-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="e438f-107">Para obter mais informações sobre o Twilio e o uso de voz e SMS em seus aplicativos, consulte Olá [próximas etapas](#NextSteps) seção.</span><span class="sxs-lookup"><span data-stu-id="e438f-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next steps](#NextSteps) section.</span></span>

## <span data-ttu-id="e438f-108"><a id="WhatIs"></a>O que é Twilio?</span><span class="sxs-lookup"><span data-stu-id="e438f-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="e438f-109">Twilio é capacitam Olá futuro das comunicações de negócios, habilitar os desenvolvedores tooembed voice, VoIP e mensagens em aplicativos.</span><span class="sxs-lookup"><span data-stu-id="e438f-109">Twilio is powering hello future of business communications, enabling developers tooembed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="e438f-110">Eles virtualizam todos infraestrutura necessária em um ambiente baseado em nuvem, global, expô-lo por meio da plataforma Olá Twilio API de comunicação.</span><span class="sxs-lookup"><span data-stu-id="e438f-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through hello Twilio communications API platform.</span></span> <span data-ttu-id="e438f-111">Os aplicativos são toobuild simple e escalonável.</span><span class="sxs-lookup"><span data-stu-id="e438f-111">Applications are simple toobuild and scalable.</span></span> <span data-ttu-id="e438f-112">Aproveite a flexibilidade com preço pré-pago e se beneficie da confiabilidade da nuvem.</span><span class="sxs-lookup"><span data-stu-id="e438f-112">Enjoy flexibility with pay-as-you-go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="e438f-113">**Voz Twilio** permite que seus aplicativos toomake e receber chamadas telefônicas.</span><span class="sxs-lookup"><span data-stu-id="e438f-113">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="e438f-114">**Twilio SMS** permite que seus aplicativos toosend e receber mensagens SMS.</span><span class="sxs-lookup"><span data-stu-id="e438f-114">**Twilio SMS** enables your applications toosend and receive SMS messages.</span></span> <span data-ttu-id="e438f-115">**Clientes do Twilio** permite chamadas de VoIP toomake de qualquer telefone, tablet ou navegador e dá suporte a WebRTC.</span><span class="sxs-lookup"><span data-stu-id="e438f-115">**Twilio Client** allows you toomake VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="e438f-116"><a id="Pricing"></a>Preços e ofertas especiais da Twilio</span><span class="sxs-lookup"><span data-stu-id="e438f-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="e438f-117">Os clientes do Azure recebem uma [oferta especial](http://www.twilio.com/azure): US$ 10 de cortesia de crédito da Twilio quando atualizam a sua conta da Twilio.</span><span class="sxs-lookup"><span data-stu-id="e438f-117">Azure customers receive a [special offer](http://www.twilio.com/azure): complimentary $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="e438f-118">Esse crédito Twilio podem ser aplicadas tooany Twilio uso (US $10 crédito equivalente toosending até 1.000 mensagens SMS ou recebimento de too1000 minutos de voz, dependendo do local de saudação do seu destino de número e a mensagem ou chamada telefônica de entrada).</span><span class="sxs-lookup"><span data-stu-id="e438f-118">This Twilio Credit can be applied tooany Twilio usage ($10 credit equivalent toosending as many as 1,000 SMS messages or receiving up too1000 inbound Voice minutes, depending on hello location of your phone number and message or call destination).</span></span> <span data-ttu-id="e438f-119">Resgate esse crédito da Twilio e faça uma introdução em [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span><span class="sxs-lookup"><span data-stu-id="e438f-119">Redeem this Twilio credit and get started at [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span></span>

<span data-ttu-id="e438f-120">Twilio é um serviço flexível.</span><span class="sxs-lookup"><span data-stu-id="e438f-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="e438f-121">Não há nenhuma taxa de configuração e você pode fechar sua conta a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="e438f-121">There are no set-up fees, and you can close your account at any time.</span></span> <span data-ttu-id="e438f-122">Você pode encontrar mais detalhes em [Preços da Twilio](http://www.twilio.com/voice/pricing).</span><span class="sxs-lookup"><span data-stu-id="e438f-122">You can find more details at [Twilio Pricing](http://www.twilio.com/voice/pricing).</span></span>

## <span data-ttu-id="e438f-123"><a id="Concepts"></a>Conceitos</span><span class="sxs-lookup"><span data-stu-id="e438f-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="e438f-124">Olá Twilio API é uma API RESTful que fornece funcionalidade SMS e voz para aplicativos.</span><span class="sxs-lookup"><span data-stu-id="e438f-124">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="e438f-125">As bibliotecas de cliente estão disponíveis em vários idiomas. Para obter uma lista, consulte [Bibliotecas de API do Twilio][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="e438f-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="e438f-126">Principais aspectos da saudação Twilio API são verbos do Twilio e Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="e438f-126">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="e438f-127"><a id="Verbs"></a>Verbos da Twilio</span><span class="sxs-lookup"><span data-stu-id="e438f-127"><a id="Verbs"></a>Twilio verbs</span></span>
<span data-ttu-id="e438f-128">Olá API faz uso do Twilio verbos; Por exemplo, Olá  **&lt;diga&gt;**  verbo instrui Twilio tooaudibly entregar uma mensagem em uma chamada.</span><span class="sxs-lookup"><span data-stu-id="e438f-128">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="e438f-129">a seguir Olá é uma lista de verbos do Twilio.</span><span class="sxs-lookup"><span data-stu-id="e438f-129">hello following is a list of Twilio verbs.</span></span>  <span data-ttu-id="e438f-130">Saiba sobre Olá outros verbos e recursos por meio de [documentação de linguagem de marcação do Twilio](http://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="e438f-130">Learn about hello other verbs and capabilities via [Twilio Markup Language documentation](http://www.twilio.com/docs/api/twiml).</span></span>

* <span data-ttu-id="e438f-131">**&lt;Discagem&gt;**: conecta-se o telefone de tooanother Olá chamador.</span><span class="sxs-lookup"><span data-stu-id="e438f-131">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="e438f-132">**&lt;Coletar&gt;**: coleta dígitos numéricos inseridos no teclado numérico do telefone hello.</span><span class="sxs-lookup"><span data-stu-id="e438f-132">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="e438f-133">**&lt;Hangup&gt;**: termina uma chamada.</span><span class="sxs-lookup"><span data-stu-id="e438f-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="e438f-134">**&lt;Play&gt;**: reproduz um arquivo de áudio.</span><span class="sxs-lookup"><span data-stu-id="e438f-134">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="e438f-135">**&lt;Pause&gt;**: espera silenciosamente por um número especificado de segundos.</span><span class="sxs-lookup"><span data-stu-id="e438f-135">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="e438f-136">**&lt;Registro&gt;**: registra a voz do chamador hello e retorna uma URL de um arquivo que contém a gravação da saudação.</span><span class="sxs-lookup"><span data-stu-id="e438f-136">**&lt;Record&gt;**: Records hello caller's voice and returns an URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="e438f-137">**&lt;Redirecionar&gt;**: transfere o controle de uma chamada ou SMS toohello TwiML em uma URL diferente.</span><span class="sxs-lookup"><span data-stu-id="e438f-137">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="e438f-138">**&lt;Rejeitar&gt;**: rejeita uma entrada chamar tooyour Twilio número sem cobrança você</span><span class="sxs-lookup"><span data-stu-id="e438f-138">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you</span></span>
* <span data-ttu-id="e438f-139">**&lt;Digamos que&gt;**: converte texto toospeech que é feita em uma chamada.</span><span class="sxs-lookup"><span data-stu-id="e438f-139">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="e438f-140">**&lt;Sms&gt;**: envia uma mensagem SMS.</span><span class="sxs-lookup"><span data-stu-id="e438f-140">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="e438f-141"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="e438f-141"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="e438f-142">TwiML é um conjunto de instruções baseadas em XML com base em verbos do Twilio Olá que informam o Twilio como tooprocess uma chamada ou SMS.</span><span class="sxs-lookup"><span data-stu-id="e438f-142">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="e438f-143">Por exemplo, Olá TwiML a seguir seria converter o texto de saudação **Hello World** toospeech.</span><span class="sxs-lookup"><span data-stu-id="e438f-143">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

<span data-ttu-id="e438f-144">Quando a aplicativo chama hello Twilio API, um dos parâmetros de API de saudação é URL Olá retorna Olá TwiML resposta.</span><span class="sxs-lookup"><span data-stu-id="e438f-144">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="e438f-145">Para fins de desenvolvimento, você pode usar URLs fornecido Twilio tooprovide Olá TwiML as respostas usadas pelos aplicativos.</span><span class="sxs-lookup"><span data-stu-id="e438f-145">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="e438f-146">Você também pode hospedar seus próprio respostas de TwiML URLs tooproduce hello e outra opção é Olá toouse **TwiMLResponse** objeto.</span><span class="sxs-lookup"><span data-stu-id="e438f-146">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello **TwiMLResponse** object.</span></span>

<span data-ttu-id="e438f-147">Para obter mais informações sobre os verbos do Twilio, seus atributos e o TwiML, consulte [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="e438f-147">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="e438f-148">Para obter informações adicionais sobre Olá Twilio API, consulte [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="e438f-148">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="e438f-149"><a id="CreateAccount"></a>Criar uma conta na Twilio</span><span class="sxs-lookup"><span data-stu-id="e438f-149"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="e438f-150">Quando você estiver pronto tooget uma conta do Twilio, inscreva-se em [tente Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="e438f-150">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="e438f-151">Você pode começar com uma conta gratuita e atualizá-la depois.</span><span class="sxs-lookup"><span data-stu-id="e438f-151">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="e438f-152">Quando você se inscrever para uma conta de Twilio, você receberá uma ID de conta e um token de autenticação.</span><span class="sxs-lookup"><span data-stu-id="e438f-152">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="e438f-153">Ambos serão chamadas à API do Twilio toomake necessários.</span><span class="sxs-lookup"><span data-stu-id="e438f-153">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="e438f-154">tooprevent não autorizado acessar conta tooyour, mantenha o token de autenticação segura.</span><span class="sxs-lookup"><span data-stu-id="e438f-154">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="e438f-155">Sua ID da conta e a autenticação token são visíveis no hello [página de conta do Twilio][twilio_account], no hello campos rotulados **SID da conta** e **TOKEN de autenticação**, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="e438f-155">Your account ID and authentication token are viewable at hello [Twilio account page][twilio_account], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="e438f-156"><a id="create_app"></a>Criar um aplicativo Azure</span><span class="sxs-lookup"><span data-stu-id="e438f-156"><a id="create_app"></a>Create an Azure Application</span></span>
<span data-ttu-id="e438f-157">Um aplicativo do Azure que hospeda um aplicativo Twilio habilitado não é diferente de qualquer outro aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="e438f-157">An Azure application that hosts a Twilio enabled application is no different from any other Azure application.</span></span> <span data-ttu-id="e438f-158">Adicionar a biblioteca do .NET do Twilio hello e configurar Olá função toouse Olá Twilio .NET bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="e438f-158">You add hello Twilio .NET library and configure hello role toouse hello Twilio .NET libraries.</span></span>
<span data-ttu-id="e438f-159">Para obter informações sobre como criar um projeto inicial do Azure, consulte [Creating an Azure project with Visual Studio][vs_project] (Criando um projeto do Azure com o Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="e438f-159">For information on creating an initial Azure project, see [Creating an Azure project with Visual Studio][vs_project].</span></span>

## <span data-ttu-id="e438f-160"><a id="configure_app"></a>Configurar seu aplicativo toouse Twilio bibliotecas</span><span class="sxs-lookup"><span data-stu-id="e438f-160"><a id="configure_app"></a>Configure Your Application toouse Twilio Libraries</span></span>
<span data-ttu-id="e438f-161">Twilio fornece um conjunto de bibliotecas do auxiliar de .NET que envolvem vários aspectos do Twilio tooprovide maneiras simples e fácil toointeract com hello API REST do Twilio e clientes do Twilio toogenerate TwiML respostas.</span><span class="sxs-lookup"><span data-stu-id="e438f-161">Twilio provides a set of .NET helper libraries that wrap various aspects of Twilio tooprovide simple and easy ways toointeract with hello Twilio REST API and Twilio Client toogenerate TwiML responses.</span></span>

<span data-ttu-id="e438f-162">Twilio fornece cinco bibliotecas para desenvolvedores .NET:</span><span class="sxs-lookup"><span data-stu-id="e438f-162">Twilio provides five libraries for .NET developers:</span></span>
<span data-ttu-id="e438f-163">Biblioteca</span><span class="sxs-lookup"><span data-stu-id="e438f-163">Library</span></span>|<span data-ttu-id="e438f-164">Descrição</span><span class="sxs-lookup"><span data-stu-id="e438f-164">Description</span></span>
---|---
<span data-ttu-id="e438f-165">Twilio.API</span><span class="sxs-lookup"><span data-stu-id="e438f-165">Twilio.API</span></span>|<span data-ttu-id="e438f-166">Olá Twilio biblioteca principal que encapsula Olá API REST do Twilio em uma biblioteca .NET amigável.</span><span class="sxs-lookup"><span data-stu-id="e438f-166">hello core Twilio library that wraps hello Twilio REST API in a friendly .NET library.</span></span> <span data-ttu-id="e438f-167">Essa biblioteca está disponível para o .NET, Silverlight e Windows Phone 7.</span><span class="sxs-lookup"><span data-stu-id="e438f-167">This library is available for .NET, Silverlight, and Windows Phone 7.</span></span>
<span data-ttu-id="e438f-168">Twilio.TwiML</span><span class="sxs-lookup"><span data-stu-id="e438f-168">Twilio.TwiML</span></span>|<span data-ttu-id="e438f-169">Fornece uma marcação de TwiML toogenerate .NET forma amigável.</span><span class="sxs-lookup"><span data-stu-id="e438f-169">Provides a .NET friendly way toogenerate TwiML markup.</span></span>
<span data-ttu-id="e438f-170">Twilio.MVC</span><span class="sxs-lookup"><span data-stu-id="e438f-170">Twilio.MVC</span></span>|<span data-ttu-id="e438f-171">Para os desenvolvedores que usam o ASP.NET MVC, esta biblioteca inclui um TwilioController, o TwiML ActionResult e o atributo de validação de solicitação.</span><span class="sxs-lookup"><span data-stu-id="e438f-171">For developers using ASP.NET MVC, this library includes a TwilioController, TwiML ActionResult, and request validation attribute.</span></span>
<span data-ttu-id="e438f-172">Twilio.WebMatrix</span><span class="sxs-lookup"><span data-stu-id="e438f-172">Twilio.WebMatrix</span></span>|<span data-ttu-id="e438f-173">Para os desenvolvedores usando a ferramenta de desenvolvimento do WebMatrix gratuita da Microsoft, esta biblioteca contém auxiliares de sintaxe do Razor para várias ações de Twilio.</span><span class="sxs-lookup"><span data-stu-id="e438f-173">For developers using Microsoft's free WebMatrix development tool, this library contains Razor syntax helpers for various Twilio actions.</span></span>
<span data-ttu-id="e438f-174">Twilio.Client.Capability</span><span class="sxs-lookup"><span data-stu-id="e438f-174">Twilio.Client.Capability</span></span>|<span data-ttu-id="e438f-175">Contém o gerador de token de recurso Olá para uso com hello Twilio SDK de JavaScript do cliente.</span><span class="sxs-lookup"><span data-stu-id="e438f-175">Contains hello Capability token generator for use with hello Twilio Client JavaScript SDK.</span></span>

<span data-ttu-id="e438f-176">Observe que todas as bibliotecas requerem o .NET 3.5, Silverlight 4 ou Windows Phone 7 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="e438f-176">Note that all libraries require .NET 3.5, Silverlight 4, or Windows Phone 7 or later.</span></span>

<span data-ttu-id="e438f-177">exemplos de saudação fornecidos neste guia usam biblioteca de Twilio.API hello.</span><span class="sxs-lookup"><span data-stu-id="e438f-177">hello samples provided in this guide use hello Twilio.API library.</span></span>

<span data-ttu-id="e438f-178">Olá bibliotecas podem ser [instalados usando a extensão do Gerenciador de pacote de NuGet de saudação](http://www.twilio.com/docs/csharp/install) disponíveis para o Visual Studio 2010 para cima too2015.</span><span class="sxs-lookup"><span data-stu-id="e438f-178">hello libraries can be [installed using hello NuGet package manager extension](http://www.twilio.com/docs/csharp/install) available for Visual Studio 2010 up too2015.</span></span>  <span data-ttu-id="e438f-179">Olá código-fonte está hospedado em [GitHub][twilio_github_repo], que inclui um Wiki que contém a documentação completa do uso de bibliotecas de saudação.</span><span class="sxs-lookup"><span data-stu-id="e438f-179">hello source code is hosted on [GitHub][twilio_github_repo], which includes a Wiki that contains complete documentation for using hello libraries.</span></span>

<span data-ttu-id="e438f-180">Por padrão, o Microsoft Visual Studio 2010 instala a versão 1.2 do NuGet.</span><span class="sxs-lookup"><span data-stu-id="e438f-180">By default, Microsoft Visual Studio 2010 installs version 1.2 of NuGet.</span></span> <span data-ttu-id="e438f-181">Instalar bibliotecas do Twilio Olá requer a versão 1.6 do NuGet ou superior.</span><span class="sxs-lookup"><span data-stu-id="e438f-181">Installing hello Twilio libraries requires version 1.6 of NuGet or higher.</span></span> <span data-ttu-id="e438f-182">Para obter mais informações sobre como instalar ou atualizar o NuGet, consulte [http://nuget.org/][nuget].</span><span class="sxs-lookup"><span data-stu-id="e438f-182">For information on installing or updating NuGet, see [http://nuget.org/][nuget].</span></span>

> [!NOTE]
> <span data-ttu-id="e438f-183">tooinstall Olá última versão do NuGet, você deve primeiro desinstalar Olá versão carregado usando Olá Gerenciador de extensões do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e438f-183">tooinstall hello latest version of NuGet, you must first uninstall hello loaded version using hello Visual Studio Extension Manager.</span></span> <span data-ttu-id="e438f-184">toodo, portanto, você deve executar o Visual Studio como administrador.</span><span class="sxs-lookup"><span data-stu-id="e438f-184">toodo so, you must run Visual Studio as administrator.</span></span> <span data-ttu-id="e438f-185">Caso contrário, o botão de desinstalação hello está desabilitado.</span><span class="sxs-lookup"><span data-stu-id="e438f-185">Otherwise, hello Uninstall button is disabled.</span></span>
>
>

### <span data-ttu-id="e438f-186"><a id="use_nuget"></a>tooadd Olá Twilio bibliotecas tooyour projeto do Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="e438f-186"><a id="use_nuget"></a>tooadd hello Twilio libraries tooyour Visual Studio project:</span></span>
1. <span data-ttu-id="e438f-187">Abra sua solução no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e438f-187">Open your solution in Visual Studio.</span></span>
2. <span data-ttu-id="e438f-188">Clique com o botão direito do mouse em **Referências**.</span><span class="sxs-lookup"><span data-stu-id="e438f-188">Right-click **References**.</span></span>
3. <span data-ttu-id="e438f-189">Clique em **Gerenciar Pacotes NuGet...**</span><span class="sxs-lookup"><span data-stu-id="e438f-189">Click **Manage NuGet Packages...**</span></span>
4. <span data-ttu-id="e438f-190">Clique em **Online**.</span><span class="sxs-lookup"><span data-stu-id="e438f-190">Click **Online**.</span></span>
5. <span data-ttu-id="e438f-191">Na caixa online de pesquisa de hello, digite *twilio*.</span><span class="sxs-lookup"><span data-stu-id="e438f-191">In hello search online box, type *twilio*.</span></span>
6. <span data-ttu-id="e438f-192">Clique em **instalar** no pacote do Twilio hello.</span><span class="sxs-lookup"><span data-stu-id="e438f-192">Click **Install** on hello Twilio package.</span></span>

## <span data-ttu-id="e438f-193"><a id="howto_make_call"></a>Como fazer uma chamada externa</span><span class="sxs-lookup"><span data-stu-id="e438f-193"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="e438f-194">Olá a seguir mostra como uma saída de toomake chamar usando Olá **CallResource** classe.</span><span class="sxs-lookup"><span data-stu-id="e438f-194">hello following shows how toomake an outgoing call using hello **CallResource** class.</span></span> <span data-ttu-id="e438f-195">Esse código também usa uma saudação do site fornecidos Twilio tooreturn resposta Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="e438f-195">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="e438f-196">Substitua os valores para Olá **para** e **de** números de telefone e certifique-se de que você verifique Olá **de** número de telefone para sua conta do Twilio antes de executar código hello.</span><span class="sxs-lookup"><span data-stu-id="e438f-196">Substitute your values for hello **to** and **from** phone numbers, and ensure that you verify hello **from** phone number for your Twilio account before running hello code.</span></span>

    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    const string accountSID = "your_twilio_account";
    const string authToken = "your_twilio_authentication_token";

    // Initialize hello TwilioClient.
    TwilioClient.Init(accountSID, authToken);

    // Use hello Twilio-provided site for hello TwiML response.
    var url = "http://twimlets.com/message";
    url = $"{url}?Message%5B0%5D=Hello%20World";

    // Set hello call From, To, and URL values toouse for hello call.
    // This sample uses hello sandbox number provided by
    // Twilio toomake hello call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri(url));
        }

<span data-ttu-id="e438f-197">Para obter mais informações sobre parâmetros de saudação passado toohello **CallResource.Create** método, consulte [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span><span class="sxs-lookup"><span data-stu-id="e438f-197">For more information about hello parameters passed in toohello **CallResource.Create** method, see [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span></span>

<span data-ttu-id="e438f-198">Conforme mencionado, esse código usa uma saudação do site fornecidos Twilio tooreturn TwiML resposta.</span><span class="sxs-lookup"><span data-stu-id="e438f-198">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="e438f-199">Em vez disso, você pode usar seu próprio hello tooprovide do site TwiML resposta.</span><span class="sxs-lookup"><span data-stu-id="e438f-199">You could instead use your own site tooprovide hello TwiML response.</span></span> <span data-ttu-id="e438f-200">Para obter mais informações, consulte [Como fornecer respostas do TwiML de seu próprio site](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="e438f-200">For more information, see [How to: Provide TwiML responses from your own website](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="e438f-201"><a id="howto_send_sms"></a>Como enviar uma mensagem de SMS</span><span class="sxs-lookup"><span data-stu-id="e438f-201"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="e438f-202">Olá seguinte captura de tela mostra como toosend uma mensagem SMS usando Olá **MessageResource** classe.</span><span class="sxs-lookup"><span data-stu-id="e438f-202">hello following screenshot shows how toosend an SMS message using hello **MessageResource**  class.</span></span> <span data-ttu-id="e438f-203">Olá **de** número é fornecido por Twilio para contas de avaliação toosend mensagens SMS.</span><span class="sxs-lookup"><span data-stu-id="e438f-203">hello **from** number is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="e438f-204">Olá **para** número deve ser verificado para sua conta do Twilio antes de executar código hello.</span><span class="sxs-lookup"><span data-stu-id="e438f-204">hello **to** number must be verified for your Twilio account before you run hello code.</span></span>

    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    const string accountSID = "your_twilio_account";
    const string authToken = "your_twilio_authentication_token";

    // Initialize hello TwilioClient.
    TwilioClient.Init(accountSID, authToken);

    try
    {
        // Send an SMS message.
        var message = MessageResource.Create(
            to: new PhoneNumber("+12069419717"),
            from: new PhoneNumber("+14155992671"),
            body: "This is my SMS message.");
    }
    catch (TwilioException ex)
    {
        // An exception occurred making hello REST call
        Console.WriteLine(ex.Message);
    }

## <span data-ttu-id="e438f-205"><a id="howto_provide_twiml_responses"></a>Como fornecer respostas TwiML de seu próprio site</span><span class="sxs-lookup"><span data-stu-id="e438f-205"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own website</span></span>
<span data-ttu-id="e438f-206">Quando o aplicativo inicia toohello uma chamada de API do Twilio - por exemplo, por meio de saudação **CallResource.Create** método - Twilio envia sua solicitação URL de tooan que é esperado tooreturn uma resposta TwiML.</span><span class="sxs-lookup"><span data-stu-id="e438f-206">When your application initiates a call toohello Twilio API - for example, via hello **CallResource.Create** method - Twilio sends your request tooan URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="e438f-207">exemplo Hello [como: fazer uma chamada de saída](#howto_make_call) usa Olá URL fornecida Twilio [http://twimlets.com/message] [ twimlet_message_url] tooreturn resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="e438f-207">hello example in [How to: Make an outgoing call](#howto_make_call) uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url] tooreturn hello response.</span></span>

> [!NOTE]
> <span data-ttu-id="e438f-208">Enquanto TwiML é projetado para uso pelos serviços da web, você pode exibir hello TwiML em seu navegador.</span><span class="sxs-lookup"><span data-stu-id="e438f-208">While TwiML is designed for use by web services, you can view hello TwiML in your browser.</span></span> <span data-ttu-id="e438f-209">Por exemplo, clique em [http://twimlets.com/message] [ twimlet_message_url] toosee vazio &lt;resposta&gt; elemento; como outro exemplo, clique em [http://twimlets.com/message ? Mensagem % 5B0 %5D = Olá % 20World](http://twimlets.com/message?Message%5B0%5D=Hello%20World) toosee um &lt;resposta&gt; elemento que contém um &lt;diga&gt; elemento.</span><span class="sxs-lookup"><span data-stu-id="e438f-209">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty &lt;Response&gt; element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World](http://twimlets.com/message?Message%5B0%5D=Hello%20World) toosee a &lt;Response&gt; element that contains a &lt;Say&gt; element.</span></span>
>
>

<span data-ttu-id="e438f-210">Em vez de depender de URL fornecido Twilio de saudação, você pode criar seu próprio site de URL que retorna respostas de HTTP.</span><span class="sxs-lookup"><span data-stu-id="e438f-210">Instead of relying on hello Twilio-provided URL, you can create your own URL site that returns HTTP responses.</span></span> <span data-ttu-id="e438f-211">Você pode criar o site de saudação em qualquer linguagem que retorna respostas de HTTP.</span><span class="sxs-lookup"><span data-stu-id="e438f-211">You can create hello site in any language that returns HTTP responses.</span></span> <span data-ttu-id="e438f-212">Este tópico pressupõe que você vai hospedando Olá URL de um manipulador genérico do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="e438f-212">This topic assumes you'll be hosting hello URL from an ASP.NET generic handler.</span></span>

<span data-ttu-id="e438f-213">Olá seguindo o manipulador ASP.NET monta uma resposta de TwiML diz **Hello World** na chamada de saudação.</span><span class="sxs-lookup"><span data-stu-id="e438f-213">hello following ASP.NET Handler crafts a TwiML response that says **Hello World** on hello call.</span></span>

    using System.Text;
    using System.Web;

    namespace WebRole1
    {
        /// <summary>
        /// Summary description for Handler1
        /// </summary>
        public class Handler1 : IHttpHandler
        {
            public void ProcessRequest(HttpContext context)
            {
                const string twiMLResponse =
                    "<Response><Say>Hello World.</Say></Response>";
                
                context.Response.Clear();
                context.Response.ContentType = "text/xml";
                context.Response.ContentEncoding = Encoding.UTF8;
                context.Response.Write(twiMLResponse);
                context.Response.End();
            }

            public bool IsReusable
            {
                get
                {
                    return false;
                }
            }
        }
    }
    
<span data-ttu-id="e438f-214">Como você pode ver do exemplo hello acima, Olá TwiML resposta é simplesmente um documento XML.</span><span class="sxs-lookup"><span data-stu-id="e438f-214">As you can see from hello example above, hello TwiML response is simply an XML document.</span></span> <span data-ttu-id="e438f-215">biblioteca de Twilio.TwiML Olá contém classes que irá gerar TwiML para você.</span><span class="sxs-lookup"><span data-stu-id="e438f-215">hello Twilio.TwiML library contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="e438f-216">Olá exemplo a seguir produz resposta equivalente hello como mostrado acima, mas usa Olá **VoiceResponse** classe.</span><span class="sxs-lookup"><span data-stu-id="e438f-216">hello example below produces hello equivalent response as shown above, but uses hello **VoiceResponse** class.</span></span>

    using System.Web;
    using Twilio.TwiML;

    namespace WebRole1
    {
        /// <summary>
        /// Summary description for Handler1
        /// </summary>
        public class Handler1 : IHttpHandler
        {

            public void ProcessRequest(HttpContext context)
            {
                var twiml = new VoiceResponse();
                twiml.Say("Hello World.");

                context.Response.Clear();
                context.Response.ContentType = "text/xml";
                context.Response.Write(twiml.ToString());
                context.Response.End();
            }

            public bool IsReusable
            {
                get
                {
                    return false;
                }
            }
        }
    }

<span data-ttu-id="e438f-217">Para obter mais informações sobre TwiML, consulte [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="e438f-217">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml).</span></span>

<span data-ttu-id="e438f-218">Depois que você configurar respostas de TwiML de tooprovide uma forma, você pode passar essa URL toohello **CallResource.Create** método.</span><span class="sxs-lookup"><span data-stu-id="e438f-218">Once you have set up a way tooprovide TwiML responses, you can pass that URL toohello **CallResource.Create** method.</span></span> <span data-ttu-id="e438f-219">Por exemplo, se você tiver um aplicativo web chamado tooan MyTwiML implantado o serviço de nuvem do Azure e nome de saudação do seu manipulador ASP.NET é mytwiml.ashx, Olá URL pode ser passado muito**CallResource.Create** conforme Olá código a seguir exemplo:</span><span class="sxs-lookup"><span data-stu-id="e438f-219">For example, if you have a web application named MyTwiML deployed tooan Azure cloud service, and hello name of your ASP.NET Handler is mytwiml.ashx, hello URL can be passed too**CallResource.Create** as shown in hello following code sample:</span></span>

    // This sample uses hello sandbox number provided by Twilio toomake hello call.
    // Place hello call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.ashx"));
        }

<span data-ttu-id="e438f-220">Para obter informações adicionais sobre como usar o Twilio no Azure com o ASP.NET, consulte [como toomake um telefone de chamada usando o Twilio em uma função web no Azure][howto_phonecall_dotnet].</span><span class="sxs-lookup"><span data-stu-id="e438f-220">For additional information about using Twilio on Azure with ASP.NET, see [How toomake a phone call using Twilio in a web role on Azure][howto_phonecall_dotnet].</span></span>

[!INCLUDE [twilio-additional-services-and-next-steps](../includes/twilio-additional-services-and-next-steps.md)]

[howto_phonecall_dotnet]: partner-twilio-cloud-services-dotnet-phone-call-web-role.md

[twimlet_message_url]: http://twimlets.com/message

[twilio_rest_making_calls]: http://www.twilio.com/docs/api/rest/making-calls

[vs_project]:http://msdn.microsoft.com/library/windowsazure/ee405487.aspx
[nuget]:http://nuget.org/
[twilio_github_repo]:https://github.com/twilio/twilio-csharp

[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_account]:  https://www.twilio.com/console
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified
