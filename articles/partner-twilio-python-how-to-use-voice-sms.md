---
title: aaaHow tooUse Twilio para voz e SMS (Python) | Microsoft Docs
description: "Saiba como toomake uma chamada telefônica e enviar um SMS de mensagem com o serviço de API do Twilio Olá no Azure. Exemplos de códigos escritos em Python."
services: 
documentationcenter: python
author: devinrader
manager: twilio
editor: 
ms.assetid: 561bc75b-4ac4-40ba-bcba-48e901f27cc3
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2015
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: 1f16a107d95c94589b8d61a0971c5b62d639c571
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-python"></a><span data-ttu-id="b4c09-104">Como tooUse Twilio para recursos de SMS em Python e voz</span><span class="sxs-lookup"><span data-stu-id="b4c09-104">How tooUse Twilio for Voice and SMS Capabilities in Python</span></span>
<span data-ttu-id="b4c09-105">Este guia demonstra como tooperform as tarefas de programação comuns com hello Twilio API de serviço no Azure.</span><span class="sxs-lookup"><span data-stu-id="b4c09-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="b4c09-106">cenários de saudação abordados incluem fazer uma chamada telefônica e enviar uma mensagem do serviço SMS (Short Message).</span><span class="sxs-lookup"><span data-stu-id="b4c09-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="b4c09-107">Para obter mais informações sobre o Twilio e o uso de voz e SMS em seus aplicativos, consulte Olá [próximas etapas](#NextSteps) seção.</span><span class="sxs-lookup"><span data-stu-id="b4c09-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="b4c09-108"><a id="WhatIs"></a>O que é Twilio?</span><span class="sxs-lookup"><span data-stu-id="b4c09-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="b4c09-109">Twilio é capacitam Olá futuro das comunicações de negócios, habilitar os desenvolvedores tooembed voice, VoIP e mensagens em aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b4c09-109">Twilio is powering hello future of business communications, enabling developers tooembed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="b4c09-110">Eles virtualizam todos infraestrutura necessária em um ambiente baseado em nuvem, global, expô-lo por meio da plataforma Olá Twilio API de comunicação.</span><span class="sxs-lookup"><span data-stu-id="b4c09-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through hello Twilio communications API platform.</span></span> <span data-ttu-id="b4c09-111">Os aplicativos são toobuild simple e escalonável.</span><span class="sxs-lookup"><span data-stu-id="b4c09-111">Applications are simple toobuild and scalable.</span></span> <span data-ttu-id="b4c09-112">Aproveite a flexibilidade com pagamento medida que vá preços e se beneficiar da confiabilidade da nuvem.</span><span class="sxs-lookup"><span data-stu-id="b4c09-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="b4c09-113">**Voz Twilio** permite que seus aplicativos toomake e receber chamadas telefônicas.</span><span class="sxs-lookup"><span data-stu-id="b4c09-113">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span>
<span data-ttu-id="b4c09-114">**Twilio SMS** permite que seu aplicativo toosend e receber mensagens de texto.</span><span class="sxs-lookup"><span data-stu-id="b4c09-114">**Twilio SMS** enables your application toosend and receive text messages.</span></span>
<span data-ttu-id="b4c09-115">**Clientes do Twilio** permite chamadas de VoIP toomake de qualquer telefone, tablet ou navegador e dá suporte a WebRTC.</span><span class="sxs-lookup"><span data-stu-id="b4c09-115">**Twilio Client** allows you toomake VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="b4c09-116"><a id="Pricing"></a>Preços e ofertas especiais da Twilio</span><span class="sxs-lookup"><span data-stu-id="b4c09-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="b4c09-117">Os clientes do Azure recebem uma [oferta especial][special_offer] de US$ 10 de crédito do Twilio quando você atualiza sua conta do Twilio.</span><span class="sxs-lookup"><span data-stu-id="b4c09-117">Azure customers receive a [special offer][special_offer] $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="b4c09-118">Esse crédito Twilio podem ser aplicadas tooany Twilio uso (US $10 crédito equivalente toosending até 1.000 mensagens SMS ou recebimento de too1000 minutos de voz, dependendo do local de saudação do seu destino de número e a mensagem ou chamada telefônica de entrada).</span><span class="sxs-lookup"><span data-stu-id="b4c09-118">This Twilio Credit can be applied tooany Twilio usage ($10 credit equivalent toosending as many as 1,000 SMS messages or receiving up too1000 inbound Voice minutes, depending on hello location of your phone number and message or call destination).</span></span> <span data-ttu-id="b4c09-119">Resgate esse [crédito do Twilio][special_offer] e comece a usar.</span><span class="sxs-lookup"><span data-stu-id="b4c09-119">Redeem this [Twilio credit][special_offer] and get started.</span></span>

<span data-ttu-id="b4c09-120">Twilio é um serviço flexível.</span><span class="sxs-lookup"><span data-stu-id="b4c09-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="b4c09-121">Não há nenhuma taxa de configuração e você pode fechar sua conta a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="b4c09-121">There are no set-up fees and you can close your account at any time.</span></span> <span data-ttu-id="b4c09-122">Você pode encontrar mais detalhes em [Preços do Twilio][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="b4c09-122">You can find more details at [Twilio Pricing][twilio_pricing].</span></span>

## <span data-ttu-id="b4c09-123"><a id="Concepts"></a>Conceitos</span><span class="sxs-lookup"><span data-stu-id="b4c09-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="b4c09-124">Olá Twilio API é uma API RESTful que fornece funcionalidade SMS e voz para aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b4c09-124">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="b4c09-125">As bibliotecas de cliente estão disponíveis em vários idiomas. Para obter uma lista, consulte [Bibliotecas de API do Twilio][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="b4c09-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="b4c09-126">Principais aspectos da saudação Twilio API são verbos do Twilio e Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="b4c09-126">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="b4c09-127"><a id="Verbs"></a>Verbos da Twilio</span><span class="sxs-lookup"><span data-stu-id="b4c09-127"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="b4c09-128">Olá API faz uso do Twilio verbos; Por exemplo, Olá  **&lt;diga&gt;**  verbo instrui Twilio tooaudibly entregar uma mensagem em uma chamada.</span><span class="sxs-lookup"><span data-stu-id="b4c09-128">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="b4c09-129">a seguir Olá é uma lista de verbos do Twilio.</span><span class="sxs-lookup"><span data-stu-id="b4c09-129">hello following is a list of Twilio verbs.</span></span> <span data-ttu-id="b4c09-130">Saiba sobre Olá outros verbos e recursos por meio de [documentação de linguagem de marcação do Twilio][twiml].</span><span class="sxs-lookup"><span data-stu-id="b4c09-130">Learn about hello other verbs and capabilities via [Twilio Markup Language documentation][twiml].</span></span>

* <span data-ttu-id="b4c09-131">**&lt;Discagem&gt;**: conecta-se o telefone de tooanother Olá chamador.</span><span class="sxs-lookup"><span data-stu-id="b4c09-131">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="b4c09-132">**&lt;Coletar&gt;**: coleta dígitos numéricos inseridos no teclado numérico do telefone hello.</span><span class="sxs-lookup"><span data-stu-id="b4c09-132">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="b4c09-133">**&lt;Hangup&gt;**: termina uma chamada.</span><span class="sxs-lookup"><span data-stu-id="b4c09-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="b4c09-134">**&lt;Pause&gt;**: espera silenciosamente por um número especificado de segundos.</span><span class="sxs-lookup"><span data-stu-id="b4c09-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="b4c09-135">**&lt;Play&gt;**: reproduz um arquivo de áudio.</span><span class="sxs-lookup"><span data-stu-id="b4c09-135">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="b4c09-136">**&lt;Fila&gt;**: Adicionar Olá tooa fila de chamadores.</span><span class="sxs-lookup"><span data-stu-id="b4c09-136">**&lt;Queue&gt;**: Add hello tooa queue of callers.</span></span>
* <span data-ttu-id="b4c09-137">**&lt;Registro&gt;**: registros de voz de saudação do chamador hello e retorna uma URL de um arquivo que contém a gravação da saudação.</span><span class="sxs-lookup"><span data-stu-id="b4c09-137">**&lt;Record&gt;**: Records hello voice of hello caller and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="b4c09-138">**&lt;Redirecionar&gt;**: transfere o controle de uma chamada ou SMS toohello TwiML em uma URL diferente.</span><span class="sxs-lookup"><span data-stu-id="b4c09-138">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="b4c09-139">**&lt;Rejeitar&gt;**: rejeita uma entrada chamar tooyour Twilio número sem cobrança você.</span><span class="sxs-lookup"><span data-stu-id="b4c09-139">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you.</span></span>
* <span data-ttu-id="b4c09-140">**&lt;Digamos que&gt;**: converte texto toospeech que é feita em uma chamada.</span><span class="sxs-lookup"><span data-stu-id="b4c09-140">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="b4c09-141">**&lt;Sms&gt;**: envia uma mensagem SMS.</span><span class="sxs-lookup"><span data-stu-id="b4c09-141">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="b4c09-142"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="b4c09-142"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="b4c09-143">TwiML é um conjunto de instruções baseadas em XML com base em verbos do Twilio Olá que informam o Twilio como tooprocess uma chamada ou SMS.</span><span class="sxs-lookup"><span data-stu-id="b4c09-143">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="b4c09-144">Por exemplo, Olá TwiML a seguir seria converter o texto de saudação **Hello World** toospeech.</span><span class="sxs-lookup"><span data-stu-id="b4c09-144">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

<span data-ttu-id="b4c09-145">Quando a aplicativo chama hello Twilio API, um dos parâmetros de API de saudação é URL Olá retorna Olá TwiML resposta.</span><span class="sxs-lookup"><span data-stu-id="b4c09-145">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="b4c09-146">Para fins de desenvolvimento, você pode usar URLs fornecido Twilio tooprovide Olá TwiML as respostas usadas pelos aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b4c09-146">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="b4c09-147">Você também pode hospedar seus próprio respostas de TwiML URLs tooproduce hello e outra opção é toouse Olá `TwiMLResponse` objeto.</span><span class="sxs-lookup"><span data-stu-id="b4c09-147">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello `TwiMLResponse` object.</span></span>

<span data-ttu-id="b4c09-148">Para obter mais informações sobre os verbos do Twilio, seus atributos e o TwiML, consulte [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="b4c09-148">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="b4c09-149">Para obter informações adicionais sobre Olá Twilio API, consulte [Twilio API][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="b4c09-149">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="b4c09-150"><a id="CreateAccount"></a>Criar uma conta na Twilio</span><span class="sxs-lookup"><span data-stu-id="b4c09-150"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="b4c09-151">Quando você estiver pronto tooget uma conta do Twilio, inscreva-se em [tente Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="b4c09-151">When you are ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="b4c09-152">Você pode começar com uma conta gratuita e atualizá-la depois.</span><span class="sxs-lookup"><span data-stu-id="b4c09-152">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="b4c09-153">Ao se inscrever em uma conta do Twilio, você receberá uma SID de conta e um token de autenticação.</span><span class="sxs-lookup"><span data-stu-id="b4c09-153">When you sign up for a Twilio account, you receive an account SID and an authentication token.</span></span> <span data-ttu-id="b4c09-154">Ambos serão chamadas à API do Twilio toomake necessários.</span><span class="sxs-lookup"><span data-stu-id="b4c09-154">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="b4c09-155">tooprevent não autorizado acessar conta tooyour, mantenha o token de autenticação segura.</span><span class="sxs-lookup"><span data-stu-id="b4c09-155">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="b4c09-156">O SID da conta e o token de autenticação são visíveis no hello [Twilio Console][twilio_console], no hello campos rotulados **SID de conta** e **TOKEN de autenticação**, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="b4c09-156">Your account SID and authentication token are viewable in hello [Twilio Console][twilio_console], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="b4c09-157"><a id="create_app"></a>Criar um Aplicativo Python</span><span class="sxs-lookup"><span data-stu-id="b4c09-157"><a id="create_app"></a>Create a Python Application</span></span>
<span data-ttu-id="b4c09-158">Um aplicativo do Python que usa o serviço do Twilio hello e está em execução no Azure não é diferente de qualquer outro aplicativo do Python que usa o serviço do Twilio hello.</span><span class="sxs-lookup"><span data-stu-id="b4c09-158">A Python application that uses hello Twilio service and is running in Azure is no different than any other Python application that uses hello Twilio service.</span></span> <span data-ttu-id="b4c09-159">Enquanto o Twilio serviços são baseados em REST e podem ser chamados do Python de várias maneiras, este artigo se concentrará em como os serviços de toouse Twilio com [Twilio biblioteca para Python do GitHub][twilio_python].</span><span class="sxs-lookup"><span data-stu-id="b4c09-159">While Twilio services are REST-based and can be called from Python in several ways, this article will focus on how toouse Twilio services with [Twilio library for Python from GitHub][twilio_python].</span></span> <span data-ttu-id="b4c09-160">Para obter mais informações sobre como usar a biblioteca do Twilio Olá para Python, consulte [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].</span><span class="sxs-lookup"><span data-stu-id="b4c09-160">For more information about using hello Twilio library for Python, see [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].</span></span>

<span data-ttu-id="b4c09-161">Primeiro, [configuração de uma nova VM Linux do Azure] [azure_vm_setup] tooact como um host para o novo aplicativo web Python.</span><span class="sxs-lookup"><span data-stu-id="b4c09-161">First, [set-up a new Azure Linux VM][azure_vm_setup] tooact as a host for your new Python web application.</span></span> <span data-ttu-id="b4c09-162">Depois de hello Máquina Virtual está em execução, será necessário tooexpose seu aplicativo em uma porta pública conforme descrito abaixo.</span><span class="sxs-lookup"><span data-stu-id="b4c09-162">Once hello Virtual Machine is running, you will need tooexpose your application on a public port as described below.</span></span>

### <a name="add-an-incoming-rule"></a><span data-ttu-id="b4c09-163">Adicionar Uma Regra de Entrada</span><span class="sxs-lookup"><span data-stu-id="b4c09-163">Add An Incoming Rule</span></span>
  1. <span data-ttu-id="b4c09-164">Vá toohello [grupo de segurança de rede] [azure_nsg] página.</span><span class="sxs-lookup"><span data-stu-id="b4c09-164">Go toohello [Network Security Group][azure_nsg] page.</span></span>
  2. <span data-ttu-id="b4c09-165">Olá selecione grupo de segurança de rede que corresponda com sua máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="b4c09-165">Select hello Network Security Group that corresponds with your Virtual Machine.</span></span>
  3. <span data-ttu-id="b4c09-166">Adicione uma **regra de saída** para a **porta 80**.</span><span class="sxs-lookup"><span data-stu-id="b4c09-166">Add and **Outgoing Rule** for **port 80**.</span></span> <span data-ttu-id="b4c09-167">Ser tooallow-se de entrada de qualquer endereço.</span><span class="sxs-lookup"><span data-stu-id="b4c09-167">Be sure tooallow incoming from any address.</span></span>

### <a name="set-hello-dns-name-label"></a><span data-ttu-id="b4c09-168">Saudação de conjunto de rótulo do nome DNS</span><span class="sxs-lookup"><span data-stu-id="b4c09-168">Set hello DNS Name Label</span></span>
  1. <span data-ttu-id="b4c09-169">Vá toohello [Olá endereços de IP público] [azure_ips] página.</span><span class="sxs-lookup"><span data-stu-id="b4c09-169">Go toohello [hello Public IP Adresses][azure_ips] page.</span></span>
  2. <span data-ttu-id="b4c09-170">Selecione Olá IP público que correspends com sua máquina Virtual.</span><span class="sxs-lookup"><span data-stu-id="b4c09-170">Select hello Public IP that correspends with your Virtual Machine.</span></span>
  3. <span data-ttu-id="b4c09-171">Saudação de conjunto **rótulo do nome DNS** em Olá **configuração** seção.</span><span class="sxs-lookup"><span data-stu-id="b4c09-171">Set hello **DNS Name Label** in hello **Configuration** section.</span></span> <span data-ttu-id="b4c09-172">No caso de Olá deste exemplo terá aparência semelhante a esta *o rótulo de domínio*. centralus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="b4c09-172">In hello case of this example it will look something like this *your-domain-label*.centralus.cloudapp.azure.com</span></span>

<span data-ttu-id="b4c09-173">Depois que você é capaz de tooconnect por meio do SSH toohello Máquina Virtual que você pode instalar Olá Framework do Web de sua escolha (Olá dois mais conhecidas do Python que está sendo [bulbo](http://flask.pocoo.org/) e [Django](https://www.djangoproject.com)).</span><span class="sxs-lookup"><span data-stu-id="b4c09-173">Once you are able tooconnect through SSH toohello Virtual Machine you can install hello Web Framework of your choice (hello two most well known in Python being [Flask](http://flask.pocoo.org/) and [Django](https://www.djangoproject.com)).</span></span> <span data-ttu-id="b4c09-174">Você pode instalar qualquer um deles apenas executando Olá `pip install` comando.</span><span class="sxs-lookup"><span data-stu-id="b4c09-174">You can install either of them just by running hello `pip install` command.</span></span>

<span data-ttu-id="b4c09-175">Tenha em mente que configuramos o tráfego de tooallow de máquina Virtual Olá apenas na porta 80.</span><span class="sxs-lookup"><span data-stu-id="b4c09-175">Keep in mind that we configured hello Virtual Machine tooallow traffic only on port 80.</span></span> <span data-ttu-id="b4c09-176">Portanto, certifique-se de que tooconfigure Olá aplicativo toouse essa porta.</span><span class="sxs-lookup"><span data-stu-id="b4c09-176">So make sure tooconfigure hello application toouse this port.</span></span>

## <span data-ttu-id="b4c09-177"><a id="configure_app"></a>Configurar seu aplicativo tooUse Twilio bibliotecas</span><span class="sxs-lookup"><span data-stu-id="b4c09-177"><a id="configure_app"></a>Configure Your Application tooUse Twilio Libraries</span></span>
<span data-ttu-id="b4c09-178">Você pode configurar sua biblioteca do aplicativo toouse Olá Twilio para Python de duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="b4c09-178">You can configure your application toouse hello Twilio library for Python in two ways:</span></span>

* <span data-ttu-id="b4c09-179">Instale biblioteca do Twilio Olá para Python como um pacote de Pip.</span><span class="sxs-lookup"><span data-stu-id="b4c09-179">Install hello Twilio library for Python as a Pip package.</span></span> <span data-ttu-id="b4c09-180">Ele pode ser instalado com hello comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="b4c09-180">It can be installed with hello following commands:</span></span>
   
        $ pip install twilio

    <span data-ttu-id="b4c09-181">-OU-</span><span class="sxs-lookup"><span data-stu-id="b4c09-181">-OR-</span></span>

* <span data-ttu-id="b4c09-182">Baixar a biblioteca do Twilio Olá para Python do GitHub ([https://github.com/twilio/twilio-python][twilio_python]) e instalá-lo assim:</span><span class="sxs-lookup"><span data-stu-id="b4c09-182">Download hello Twilio library for Python from GitHub ([https://github.com/twilio/twilio-python][twilio_python]) and install it like this:</span></span>

        $ python setup.py install

<span data-ttu-id="b4c09-183">Depois que você instalou a biblioteca do Twilio Olá para Python, você pode, em seguida, `import` -lo em seus arquivos de Python:</span><span class="sxs-lookup"><span data-stu-id="b4c09-183">Once you have installed hello Twilio library for Python, you can then `import` it in your Python files:</span></span>

        import twilio

<span data-ttu-id="b4c09-184">Para obter mais informações, consulte [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].</span><span class="sxs-lookup"><span data-stu-id="b4c09-184">For more information, see [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].</span></span>

## <span data-ttu-id="b4c09-185"><a id="howto_make_call"></a>Como fazer uma chamada externa</span><span class="sxs-lookup"><span data-stu-id="b4c09-185"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="b4c09-186">Olá a seguir mostra como chamar toomake uma saída.</span><span class="sxs-lookup"><span data-stu-id="b4c09-186">hello following shows how toomake an outgoing call.</span></span> <span data-ttu-id="b4c09-187">Esse código também usa uma saudação do site fornecidos Twilio tooreturn resposta Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="b4c09-187">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="b4c09-188">Substitua os valores para Olá **from_number** e **to_number** números de telefone e certifique-se de que você verificou Olá **from_number** número de telefone para sua conta do Twilio antes da execução de código hello.</span><span class="sxs-lookup"><span data-stu-id="b4c09-188">Substitute your values for hello **from_number** and **to_number** phone numbers, and ensure that you've verified hello **from_number** phone number for your Twilio account before running hello code.</span></span>

    from urllib.parse import urlencode

    # Import hello Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    # hello number of hello phone initiating hello hello call.
    # This should either be a Twilio number or a number that you've verified
    from_number = "NNNNNNNNNNN"

    # hello number of hello phone receiving call.
    to_number = "NNNNNNNNNNN"

    # Use hello Twilio-provided site for hello TwiML response.
    url = "http://twimlets.com/message?"

    # hello phone message text.
    message = "Hello world."

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make hello call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url + urlencode({'Message': message}))
    print(call.sid)

<span data-ttu-id="b4c09-189">Conforme mencionado, esse código usa uma saudação do site fornecidos Twilio tooreturn TwiML resposta.</span><span class="sxs-lookup"><span data-stu-id="b4c09-189">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="b4c09-190">Em vez disso, você pode usar seu próprio hello tooprovide do site TwiML resposta; Para obter mais informações, consulte [como tooProvide TwiML respostas do seu próprio Site](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="b4c09-190">You could instead use your own site tooprovide hello TwiML response; for more information, see [How tooProvide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="b4c09-191"><a id="howto_send_sms"></a>Como enviar uma mensagem de SMS</span><span class="sxs-lookup"><span data-stu-id="b4c09-191"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="b4c09-192">Olá a seguir mostra como toosend uma mensagem SMS usando Olá `TwilioRestClient` classe.</span><span class="sxs-lookup"><span data-stu-id="b4c09-192">hello following shows how toosend an SMS message using hello `TwilioRestClient` class.</span></span> <span data-ttu-id="b4c09-193">Olá **from_number** número é fornecido por Twilio para contas de avaliação toosend mensagens SMS.</span><span class="sxs-lookup"><span data-stu-id="b4c09-193">hello **from_number** number is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="b4c09-194">Olá **to_number** número deve ser verificado para sua conta do Twilio antes de executar código hello.</span><span class="sxs-lookup"><span data-stu-id="b4c09-194">hello **to_number** number must be verified for your Twilio account before running hello code.</span></span>

    # Import hello Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    from_number = "NNNNNNNNNNN"  # With trial account, texts can only be sent from your Twilio number.
    to_number = "NNNNNNNNNNN"
    message = "Hello world."

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Send hello SMS message.
    message = client.messages.create(to=to_number,
                                     from_=from_number,
                                     body=message)

## <span data-ttu-id="b4c09-195"><a id="howto_provide_twiml_responses"></a>Como fornecer respostas TwiML de seu próprio site</span><span class="sxs-lookup"><span data-stu-id="b4c09-195"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="b4c09-196">Quando o aplicativo inicia toohello uma chamada de API do Twilio, Twilio enviará a URL de tooa de solicitação que é esperado tooreturn uma resposta TwiML.</span><span class="sxs-lookup"><span data-stu-id="b4c09-196">When your application initiates a call toohello Twilio API, Twilio will send your request tooa URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="b4c09-197">exemplo Hello acima usa a URL fornecida Twilio de saudação [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="b4c09-197">hello example above uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="b4c09-198">(Embora o TwiML tenha sido criado para uso do Twilio, você pode exibi-lo em seu navegador.</span><span class="sxs-lookup"><span data-stu-id="b4c09-198">(While TwiML is designed for use by Twilio, you can view it in your browser.</span></span> <span data-ttu-id="b4c09-199">Por exemplo, clique em [http://twimlets.com/message] [ twimlet_message_url] toosee vazio `<Response>` elemento; como outro exemplo, clique em [http://twimlets.com/message? Mensagem % 5B0 %5D = Olá % 20World] [ twimlet_message_url_hello_world] toosee um `<Response>` elemento que contém um `<Say>` elemento.)</span><span class="sxs-lookup"><span data-stu-id="b4c09-199">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] toosee a `<Response>` element that contains a `<Say>` element.)</span></span>

<span data-ttu-id="b4c09-200">Em vez de depender de URL fornecido Twilio de saudação, você pode criar seu próprio site que retorna respostas de HTTP.</span><span class="sxs-lookup"><span data-stu-id="b4c09-200">Instead of relying on hello Twilio-provided URL, you can create your own site that returns HTTP responses.</span></span> <span data-ttu-id="b4c09-201">Você pode criar site hello em qualquer linguagem que retorna respostas XML; Este tópico pressupõe que você usará saudação do Python toocreate TwiML.</span><span class="sxs-lookup"><span data-stu-id="b4c09-201">You can create hello site in any language that returns XML responses; this topic assumes you will be using Python toocreate hello TwiML.</span></span>

<span data-ttu-id="b4c09-202">Olá exemplos a seguir produzirá uma resposta de TwiML diz **Hello World** na chamada de saudação.</span><span class="sxs-lookup"><span data-stu-id="b4c09-202">hello following examples will output a TwiML response that says **Hello World** on hello call.</span></span>

<span data-ttu-id="b4c09-203">Com o Flash:</span><span class="sxs-lookup"><span data-stu-id="b4c09-203">With Flask:</span></span>

    from flask import Response
    @app.route("/")
    def hello():
        xml = '<Response><Say>Hello world.</Say></Response>'
        return Response(xml, mimetype='text/xml')

<span data-ttu-id="b4c09-204">Com o Django:</span><span class="sxs-lookup"><span data-stu-id="b4c09-204">With Django:</span></span>

    from django.http import HttpResponse
    def hello(request):
        xml = '<Response><Say>Hello world.</Say></Response>'
        return HttpResponse(xml, content_type='text/xml')

<span data-ttu-id="b4c09-205">Como você pode ver do exemplo hello acima, Olá TwiML resposta é simplesmente um documento XML.</span><span class="sxs-lookup"><span data-stu-id="b4c09-205">As you can see from hello example above, hello TwiML response is simply an XML document.</span></span> <span data-ttu-id="b4c09-206">biblioteca do Twilio Olá para Python contém classes que irá gerar TwiML para você.</span><span class="sxs-lookup"><span data-stu-id="b4c09-206">hello Twilio library for Python contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="b4c09-207">Olá exemplo a seguir produz resposta equivalente hello como mostrado acima, mas usa Olá `twiml` módulo na biblioteca do Twilio de saudação do Python:</span><span class="sxs-lookup"><span data-stu-id="b4c09-207">hello example below produces hello equivalent response as shown above, but uses hello `twiml` module in hello Twilio library for Python:</span></span>

    from twilio import twiml

    response = twiml.Response()
    response.say("Hello world.")
    print(str(response))

<span data-ttu-id="b4c09-208">Para obter mais informações sobre TwiML, consulte [https://www.twilio.com/docs/api/twiml][twiml_reference].</span><span class="sxs-lookup"><span data-stu-id="b4c09-208">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span></span>

<span data-ttu-id="b4c09-209">Uma vez que seu aplicativo Python configurar tooprovide TwiML respostas, use Olá URL do aplicativo hello como Olá URL passada em hello `client.calls.create` método.</span><span class="sxs-lookup"><span data-stu-id="b4c09-209">Once you have your Python application set up tooprovide TwiML responses, use hello URL of hello application as hello URL passed into hello `client.calls.create`  method.</span></span> <span data-ttu-id="b4c09-210">Por exemplo, se você tiver um aplicativo Web chamado **MyTwiML** tooan implantado Azure o serviço hospedado, você pode usar a url como webhook, conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="b4c09-210">For example, if you have a Web application named **MyTwiML** deployed tooan Azure hosted service, you can use its url as webhook as shown in hello following example:</span></span>

    from twilio.rest import TwilioRestClient

    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"
    from_number = "NNNNNNNNNNN"
    to_number = "NNNNNNNNNNN"
    url = "http://your-domain-label.centralus.cloudapp.azure.com/MyTwiML/"

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make hello call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url)
    print(call.sid)

## <span data-ttu-id="b4c09-211"><a id="AdditionalServices"></a>Como Usar os Serviços Adicionais do Twilio</span><span class="sxs-lookup"><span data-stu-id="b4c09-211"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="b4c09-212">Além disso toohello exemplos mostrados aqui, que twilio oferece APIs baseado na web que você pode usar uma funcionalidade adicional Twilio tooleverage do aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="b4c09-212">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="b4c09-213">Para obter detalhes completos, consulte Olá [documentação da API do Twilio][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="b4c09-213">For full details, see hello [Twilio API documentation][twilio_api].</span></span>

## <span data-ttu-id="b4c09-214"><a id="NextSteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b4c09-214"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="b4c09-215">Agora que você aprendeu os fundamentos de saudação do hello Twilio serviço, siga essas toolearn links mais:</span><span class="sxs-lookup"><span data-stu-id="b4c09-215">Now that you have learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="b4c09-216">[Diretrizes de segurança do Twilio][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="b4c09-216">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="b4c09-217">[Código de Exemplo e Guias de Procedimentos do Twilio][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="b4c09-217">[Twilio HowTo Guides and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="b4c09-218">[Tutoriais do Guia de início rápido do Twilio][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="b4c09-218">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span>
* <span data-ttu-id="b4c09-219">[Twilio no GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="b4c09-219">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="b4c09-220">[Fale tooTwilio suporte][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="b4c09-220">[Talk tooTwilio Support][twilio_support]</span></span>

[special_offer]: http://ahoy.twilio.com/azure
[twilio_python]: https://github.com/twilio/twilio-python
[twilio_lib_docs]: http://readthedocs.org/docs/twilio-python/en/latest/index.html
[twilio_github_readme]: https://github.com/twilio/twilio-python/blob/master/README.md

[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World
[twiml_reference]: https://www.twilio.com/docs/api/twiml
[twilio_pricing]: http://www.twilio.com/pricing

[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_console]:  https://www.twilio.com/console
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
