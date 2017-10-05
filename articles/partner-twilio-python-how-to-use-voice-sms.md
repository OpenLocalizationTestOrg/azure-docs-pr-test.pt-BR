---
title: Como usar o Twilio para voz e SMS (Python) | Microsoft Docs
description: "Saiba como fazer uma chamada telefônica e enviar uma mensagem SMS com o serviço de API do Twilio no Azure. Exemplos de códigos escritos em Python."
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
ms.openlocfilehash: f4a02bb7a7c46e7a0e3c75b870c522eae8294339
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-in-python"></a><span data-ttu-id="04809-104">Como usar o Twilio para obter recursos de voz e SMS no Python</span><span class="sxs-lookup"><span data-stu-id="04809-104">How to Use Twilio for Voice and SMS Capabilities in Python</span></span>
<span data-ttu-id="04809-105">Este guia demonstra como executar tarefas comuns de programação com o serviço de API do Twilio no Azure.</span><span class="sxs-lookup"><span data-stu-id="04809-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="04809-106">Os cenários abrangidos incluem fazer uma chamada telefônica e enviar uma mensagem serviço de mensagem curta (SMS).</span><span class="sxs-lookup"><span data-stu-id="04809-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="04809-107">Para obter mais informações sobre o Twilio e o uso de voz e SMS em seus aplicativos, consulte a seção [Próximas etapas](#NextSteps) .</span><span class="sxs-lookup"><span data-stu-id="04809-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="04809-108"><a id="WhatIs"></a>O que é Twilio?</span><span class="sxs-lookup"><span data-stu-id="04809-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="04809-109">Twilio é alimentar o futuro das comunicações de negócios, que permite aos desenvolvedores incorporar voz, VoIP e mensagens em aplicativos.</span><span class="sxs-lookup"><span data-stu-id="04809-109">Twilio is powering the future of business communications, enabling developers to embed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="04809-110">Eles virtualizam toda a infra-estrutura necessária em um ambiente baseado em nuvem, global, expondo-as por meio da plataforma de comunicações API Twilio.</span><span class="sxs-lookup"><span data-stu-id="04809-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through the Twilio communications API platform.</span></span> <span data-ttu-id="04809-111">Os aplicativos são simples de criar e dimensionável.</span><span class="sxs-lookup"><span data-stu-id="04809-111">Applications are simple to build and scalable.</span></span> <span data-ttu-id="04809-112">Aproveite a flexibilidade com pagamento medida que vá preços e se beneficiar da confiabilidade da nuvem.</span><span class="sxs-lookup"><span data-stu-id="04809-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="04809-113">**Twilio Voice** permite que seus aplicativos façam e recebam chamadas telefônicas.</span><span class="sxs-lookup"><span data-stu-id="04809-113">**Twilio Voice** allows your applications to make and receive phone calls.</span></span>
<span data-ttu-id="04809-114">**SMS da Twilio** permite que seu aplicativo envie e receba mensagens de texto.</span><span class="sxs-lookup"><span data-stu-id="04809-114">**Twilio SMS** enables your application to send and receive text messages.</span></span>
<span data-ttu-id="04809-115">**Cliente de Twilio** permite que você faça chamadas VoIP de qualquer telefone, tablet ou navegador e oferece suporte a WebRTC.</span><span class="sxs-lookup"><span data-stu-id="04809-115">**Twilio Client** allows you to make VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="04809-116"><a id="Pricing"></a>Preços e ofertas especiais da Twilio</span><span class="sxs-lookup"><span data-stu-id="04809-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="04809-117">Os clientes do Azure recebem uma [oferta especial][special_offer] de US$ 10 de crédito do Twilio quando você atualiza sua conta do Twilio.</span><span class="sxs-lookup"><span data-stu-id="04809-117">Azure customers receive a [special offer][special_offer] $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="04809-118">Esse crédito de Twilio pode ser aplicado a qualquer uso de Twilio (equivalente a até 1.000 mensagens SMS de envio ou recebimento de até 1000 minutos de voz entrados, dependendo da localização do seu destino de chamada e mensagem ou número de telefone de crédito de US $10).</span><span class="sxs-lookup"><span data-stu-id="04809-118">This Twilio Credit can be applied to any Twilio usage ($10 credit equivalent to sending as many as 1,000 SMS messages or receiving up to 1000 inbound Voice minutes, depending on the location of your phone number and message or call destination).</span></span> <span data-ttu-id="04809-119">Resgate esse [crédito do Twilio][special_offer] e comece a usar.</span><span class="sxs-lookup"><span data-stu-id="04809-119">Redeem this [Twilio credit][special_offer] and get started.</span></span>

<span data-ttu-id="04809-120">Twilio é um serviço flexível.</span><span class="sxs-lookup"><span data-stu-id="04809-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="04809-121">Não há nenhuma taxa de configuração e você pode fechar sua conta a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="04809-121">There are no set-up fees and you can close your account at any time.</span></span> <span data-ttu-id="04809-122">Você pode encontrar mais detalhes em [Preços do Twilio][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="04809-122">You can find more details at [Twilio Pricing][twilio_pricing].</span></span>

## <span data-ttu-id="04809-123"><a id="Concepts"></a>Conceitos</span><span class="sxs-lookup"><span data-stu-id="04809-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="04809-124">A API do Twilio é uma API RESTful que fornece os recursos de voz e SMS para aplicativos.</span><span class="sxs-lookup"><span data-stu-id="04809-124">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="04809-125">As bibliotecas de cliente estão disponíveis em vários idiomas. Para obter uma lista, consulte [Bibliotecas de API do Twilio][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="04809-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="04809-126">Os principais aspectos da API do Twilio são os verbos Twilio e a TwiML (Linguagem de Marcação do Twilio).</span><span class="sxs-lookup"><span data-stu-id="04809-126">Key aspects of the Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="04809-127"><a id="Verbs"></a>Verbos da Twilio</span><span class="sxs-lookup"><span data-stu-id="04809-127"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="04809-128">A API usa os verbos do Twilio; por exemplo, o verbo **&lt;Say&gt;** instrui o Twilio a fornecer de forma audível uma mensagem em uma chamada.</span><span class="sxs-lookup"><span data-stu-id="04809-128">The API makes use of Twilio verbs; for example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span>

<span data-ttu-id="04809-129">A seguir está uma lista de verbos do Twilio.</span><span class="sxs-lookup"><span data-stu-id="04809-129">The following is a list of Twilio verbs.</span></span> <span data-ttu-id="04809-130">Saiba mais sobre os outros verbos e recursos na [Documentação da linguagem de marcação da Twilio][twiml].</span><span class="sxs-lookup"><span data-stu-id="04809-130">Learn about the other verbs and capabilities via [Twilio Markup Language documentation][twiml].</span></span>

* <span data-ttu-id="04809-131">**&lt;Dial&gt;**: conecta o chamador com outro telefone.</span><span class="sxs-lookup"><span data-stu-id="04809-131">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="04809-132">**&lt;Gather&gt;**: coleta os dígitos numéricos inseridos no teclado numérico de telefone.</span><span class="sxs-lookup"><span data-stu-id="04809-132">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="04809-133">**&lt;Hangup&gt;**: termina uma chamada.</span><span class="sxs-lookup"><span data-stu-id="04809-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="04809-134">**&lt;Pause&gt;**: espera silenciosamente por um número especificado de segundos.</span><span class="sxs-lookup"><span data-stu-id="04809-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="04809-135">**&lt;Play&gt;**: reproduz um arquivo de áudio.</span><span class="sxs-lookup"><span data-stu-id="04809-135">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="04809-136">**&lt;Fila&gt;**: adicionar a chamada a uma fila de chamadores.</span><span class="sxs-lookup"><span data-stu-id="04809-136">**&lt;Queue&gt;**: Add the to a queue of callers.</span></span>
* <span data-ttu-id="04809-137">**&lt;Record&gt;**: grava a voz do chamador e retorna uma URL de um arquivo que contém a gravação.</span><span class="sxs-lookup"><span data-stu-id="04809-137">**&lt;Record&gt;**: Records the voice of the caller and returns a URL of a file that contains the recording.</span></span>
* <span data-ttu-id="04809-138">**&lt;Redirect&gt;**: transfere o controle de uma chamada ou SMS para TwiML em um URL diferente.</span><span class="sxs-lookup"><span data-stu-id="04809-138">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="04809-139">**&lt;Reject&gt;**: rejeita uma chamada recebida para o número do Twilio sem cobrar você.</span><span class="sxs-lookup"><span data-stu-id="04809-139">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you.</span></span>
* <span data-ttu-id="04809-140">**&lt;Say&gt;**: converte o texto em fala que é executada em uma chamada.</span><span class="sxs-lookup"><span data-stu-id="04809-140">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="04809-141">**&lt;Sms&gt;**: envia uma mensagem SMS.</span><span class="sxs-lookup"><span data-stu-id="04809-141">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="04809-142"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="04809-142"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="04809-143">TwiML é um conjunto de instruções em XML com base nos verbos do Twilio que informam o Twilio como processar uma chamada ou SMS.</span><span class="sxs-lookup"><span data-stu-id="04809-143">TwiML is a set of XML-based instructions based on the Twilio verbs that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="04809-144">Por exemplo, o seguinte TwiML converteria a mensagem **Olá, mundo** em fala.</span><span class="sxs-lookup"><span data-stu-id="04809-144">As an example, the following TwiML would convert the text **Hello World** to speech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

<span data-ttu-id="04809-145">Quando o aplicativo chama a API Twilio, um dos parâmetros a API é a URL que retorna a resposta TwiML.</span><span class="sxs-lookup"><span data-stu-id="04809-145">When your application calls the Twilio API, one of the API parameters is the URL that returns the TwiML response.</span></span> <span data-ttu-id="04809-146">Para fins de desenvolvimento, você pode usar URLs fornecidos Twilio para fornecer as respostas de TwiML usadas por seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="04809-146">For development purposes, you can use Twilio-provided URLs to provide the TwiML responses used by your applications.</span></span> <span data-ttu-id="04809-147">Você também pode hospedar seus próprio URLs para produzir as respostas TwiML e outra opção é usar o objeto `TwiMLResponse`.</span><span class="sxs-lookup"><span data-stu-id="04809-147">You could also host your own URLs to produce the TwiML responses, and another option is to use the `TwiMLResponse` object.</span></span>

<span data-ttu-id="04809-148">Para obter mais informações sobre os verbos do Twilio, seus atributos e o TwiML, consulte [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="04809-148">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="04809-149">Para obter mais informações sobre a API do Twilio, consulte [API do Twilio][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="04809-149">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="04809-150"><a id="CreateAccount"></a>Criar uma conta na Twilio</span><span class="sxs-lookup"><span data-stu-id="04809-150"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="04809-151">Quando você estiver pronto para obter uma conta do Twilio, inscreva-se em [Experimentar o Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="04809-151">When you are ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="04809-152">Você pode começar com uma conta gratuita e atualizá-la depois.</span><span class="sxs-lookup"><span data-stu-id="04809-152">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="04809-153">Ao se inscrever em uma conta do Twilio, você receberá uma SID de conta e um token de autenticação.</span><span class="sxs-lookup"><span data-stu-id="04809-153">When you sign up for a Twilio account, you receive an account SID and an authentication token.</span></span> <span data-ttu-id="04809-154">Eles serão necessários para fazer chamadas de API do Twilio.</span><span class="sxs-lookup"><span data-stu-id="04809-154">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="04809-155">Para evitar o acesso não autorizado em sua conta, mantenha o token da autenticação seguro.</span><span class="sxs-lookup"><span data-stu-id="04809-155">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="04809-156">A SID de sua conta e o token de autenticação estão visíveis no [Console do Twilio][twilio_console], nos campos rotulados **ACCOUNT SID** e **AUTH TOKEN**, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="04809-156">Your account SID and authentication token are viewable in the [Twilio Console][twilio_console], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="04809-157"><a id="create_app"></a>Criar um Aplicativo Python</span><span class="sxs-lookup"><span data-stu-id="04809-157"><a id="create_app"></a>Create a Python Application</span></span>
<span data-ttu-id="04809-158">Um aplicativo Python que usa o serviço do Twilio e está em execução no Azure não é diferente de qualquer outro aplicativo Python que usa o serviço do Twilio.</span><span class="sxs-lookup"><span data-stu-id="04809-158">A Python application that uses the Twilio service and is running in Azure is no different than any other Python application that uses the Twilio service.</span></span> <span data-ttu-id="04809-159">Embora os serviços da Twilio sejam baseados em REST e possam ser chamados no Python de várias maneiras, este artigo se concentra em como usar os serviços da Twilio com a [Biblioteca da Twilio para Python no GitHub][twilio_python].</span><span class="sxs-lookup"><span data-stu-id="04809-159">While Twilio services are REST-based and can be called from Python in several ways, this article will focus on how to use Twilio services with [Twilio library for Python from GitHub][twilio_python].</span></span> <span data-ttu-id="04809-160">Para obter mais informações sobre como usar a biblioteca da Twilio para Python, consulte [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].</span><span class="sxs-lookup"><span data-stu-id="04809-160">For more information about using the Twilio library for Python, see [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].</span></span>

<span data-ttu-id="04809-161">Primeiro, [configure uma nova VM Linux do Azure][azure_vm_setup] para agir como um host para o novo aplicativo Web do Python.</span><span class="sxs-lookup"><span data-stu-id="04809-161">First, [set-up a new Azure Linux VM][azure_vm_setup] to act as a host for your new Python web application.</span></span> <span data-ttu-id="04809-162">Quando a Máquina Virtual está em execução, você precisará expor seu aplicativo em uma porta pública, conforme descrito abaixo.</span><span class="sxs-lookup"><span data-stu-id="04809-162">Once the Virtual Machine is running, you will need to expose your application on a public port as described below.</span></span>

### <a name="add-an-incoming-rule"></a><span data-ttu-id="04809-163">Adicionar Uma Regra de Entrada</span><span class="sxs-lookup"><span data-stu-id="04809-163">Add An Incoming Rule</span></span>
  1. <span data-ttu-id="04809-164">Vá para a página [Grupo de Segurança de Rede][azure_nsg].</span><span class="sxs-lookup"><span data-stu-id="04809-164">Go to the [Network Security Group][azure_nsg] page.</span></span>
  2. <span data-ttu-id="04809-165">Selecione o grupo de segurança de rede que corresponde à sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="04809-165">Select the Network Security Group that corresponds with your Virtual Machine.</span></span>
  3. <span data-ttu-id="04809-166">Adicione uma **regra de saída** para a **porta 80**.</span><span class="sxs-lookup"><span data-stu-id="04809-166">Add and **Outgoing Rule** for **port 80**.</span></span> <span data-ttu-id="04809-167">Certifique-se de permitir a entrada de qualquer endereço.</span><span class="sxs-lookup"><span data-stu-id="04809-167">Be sure to allow incoming from any address.</span></span>

### <a name="set-the-dns-name-label"></a><span data-ttu-id="04809-168">Definir o rótulo do Nome DNS</span><span class="sxs-lookup"><span data-stu-id="04809-168">Set the DNS Name Label</span></span>
  1. <span data-ttu-id="04809-169">Vá para a página [Os Endereços IP Públicos][azure_ips].</span><span class="sxs-lookup"><span data-stu-id="04809-169">Go to the [The Public IP Adresses][azure_ips] page.</span></span>
  2. <span data-ttu-id="04809-170">Selecione o IP Público que corresponde à sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="04809-170">Select the Public IP that correspends with your Virtual Machine.</span></span>
  3. <span data-ttu-id="04809-171">Defina o **Rótulo de Nome DNS** na seção **Configuração**.</span><span class="sxs-lookup"><span data-stu-id="04809-171">Set the **DNS Name Label** in the **Configuration** section.</span></span> <span data-ttu-id="04809-172">No caso deste exemplo, você verá algo semelhante a *rótulo-do-seu-domínio*.centralus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="04809-172">In the case of this example it will look something like this *your-domain-label*.centralus.cloudapp.azure.com</span></span>

<span data-ttu-id="04809-173">Assim que você for capaz de se conectar à máquina virtual por meio de SSH, você poderá instalar a estrutura da Web de sua escolha (as duas mais conhecidas do Python são [Flask](http://flask.pocoo.org/) e [Django](https://www.djangoproject.com)).</span><span class="sxs-lookup"><span data-stu-id="04809-173">Once you are able to connect through SSH to the Virtual Machine you can install the Web Framework of your choice (the two most well known in Python being [Flask](http://flask.pocoo.org/) and [Django](https://www.djangoproject.com)).</span></span> <span data-ttu-id="04809-174">Você pode instalar qualquer um deles apenas executando o comando `pip install`.</span><span class="sxs-lookup"><span data-stu-id="04809-174">You can install either of them just by running the `pip install` command.</span></span>

<span data-ttu-id="04809-175">Tenha em mente que podemos configurar a máquina virtual para permitir tráfego apenas na porta 80.</span><span class="sxs-lookup"><span data-stu-id="04809-175">Keep in mind that we configured the Virtual Machine to allow traffic only on port 80.</span></span> <span data-ttu-id="04809-176">Assim, certifique-se de configurar o aplicativo para usar essa porta.</span><span class="sxs-lookup"><span data-stu-id="04809-176">So make sure to configure the application to use this port.</span></span>

## <span data-ttu-id="04809-177"><a id="configure_app"></a>Configurar seu aplicativo para usar bibliotecas Twilio</span><span class="sxs-lookup"><span data-stu-id="04809-177"><a id="configure_app"></a>Configure Your Application to Use Twilio Libraries</span></span>
<span data-ttu-id="04809-178">Você pode configurar seu aplicativo para usar a biblioteca do Twilio para Python de duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="04809-178">You can configure your application to use the Twilio library for Python in two ways:</span></span>

* <span data-ttu-id="04809-179">Instalar a biblioteca da Twilio para Python como um pacote Pip.</span><span class="sxs-lookup"><span data-stu-id="04809-179">Install the Twilio library for Python as a Pip package.</span></span> <span data-ttu-id="04809-180">Ela pode ser instalada com os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="04809-180">It can be installed with the following commands:</span></span>
   
        $ pip install twilio

    <span data-ttu-id="04809-181">-OU-</span><span class="sxs-lookup"><span data-stu-id="04809-181">-OR-</span></span>

* <span data-ttu-id="04809-182">Baixar a biblioteca do Twilio para o Python do GitHub ([https://github.com/twilio/twilio-python][twilio_python]) e instale-a assim:</span><span class="sxs-lookup"><span data-stu-id="04809-182">Download the Twilio library for Python from GitHub ([https://github.com/twilio/twilio-python][twilio_python]) and install it like this:</span></span>

        $ python setup.py install

<span data-ttu-id="04809-183">Depois de instalar a biblioteca do Twilio para o Python, você pode então `import`-lo em seus arquivos de Python:</span><span class="sxs-lookup"><span data-stu-id="04809-183">Once you have installed the Twilio library for Python, you can then `import` it in your Python files:</span></span>

        import twilio

<span data-ttu-id="04809-184">Para obter mais informações, consulte [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].</span><span class="sxs-lookup"><span data-stu-id="04809-184">For more information, see [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].</span></span>

## <span data-ttu-id="04809-185"><a id="howto_make_call"></a>Como fazer uma chamada externa</span><span class="sxs-lookup"><span data-stu-id="04809-185"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="04809-186">A seguir você verá como fazer uma chamada de saída.</span><span class="sxs-lookup"><span data-stu-id="04809-186">The following shows how to make an outgoing call.</span></span> <span data-ttu-id="04809-187">Esse código também usa um site fornecido pelo Twilio para retornar a resposta TwiML (Linguagem de Marcação do Twilio).</span><span class="sxs-lookup"><span data-stu-id="04809-187">This code also uses a Twilio-provided site to return the Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="04809-188">Substitua os valores dos números telefônico **from_number** e **to_number** e certifique-se de verificar o número telefônico **from_number** de sua conta do Twilio antes de executar o código.</span><span class="sxs-lookup"><span data-stu-id="04809-188">Substitute your values for the **from_number** and **to_number** phone numbers, and ensure that you've verified the **from_number** phone number for your Twilio account before running the code.</span></span>

    from urllib.parse import urlencode

    # Import the Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    # The number of the phone initiating the the call.
    # This should either be a Twilio number or a number that you've verified
    from_number = "NNNNNNNNNNN"

    # The number of the phone receiving call.
    to_number = "NNNNNNNNNNN"

    # Use the Twilio-provided site for the TwiML response.
    url = "http://twimlets.com/message?"

    # The phone message text.
    message = "Hello world."

    # Initialize the Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make the call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url + urlencode({'Message': message}))
    print(call.sid)

<span data-ttu-id="04809-189">Como mencionado, esse código utiliza um site fornecido pelo Twilio para retornar a resposta de TwiML.</span><span class="sxs-lookup"><span data-stu-id="04809-189">As mentioned, this code uses a Twilio-provided site to return the TwiML response.</span></span> <span data-ttu-id="04809-190">Em vez disso, você pode usar seu próprio site para fornecer a resposta TwiML. Para obter mais informações, consulte [Como fornecer respostas TwiML em seu próprio site](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="04809-190">You could instead use your own site to provide the TwiML response; for more information, see [How to Provide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="04809-191"><a id="howto_send_sms"></a>Como enviar uma mensagem de SMS</span><span class="sxs-lookup"><span data-stu-id="04809-191"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="04809-192">O conteúdo abaixo mostra como enviar uma mensagem SMS usando a classe `TwilioRestClient`.</span><span class="sxs-lookup"><span data-stu-id="04809-192">The following shows how to send an SMS message using the `TwilioRestClient` class.</span></span> <span data-ttu-id="04809-193">O número **from_number** é fornecido pelo Twilio para contas de avaliação para enviar mensagens SMS.</span><span class="sxs-lookup"><span data-stu-id="04809-193">The **from_number** number is provided by Twilio for trial accounts to send SMS messages.</span></span> <span data-ttu-id="04809-194">O número **to_number** deve ser verificado para sua conta de Twilio antes de executar o código.</span><span class="sxs-lookup"><span data-stu-id="04809-194">The **to_number** number must be verified for your Twilio account before running the code.</span></span>

    # Import the Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    from_number = "NNNNNNNNNNN"  # With trial account, texts can only be sent from your Twilio number.
    to_number = "NNNNNNNNNNN"
    message = "Hello world."

    # Initialize the Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Send the SMS message.
    message = client.messages.create(to=to_number,
                                     from_=from_number,
                                     body=message)

## <span data-ttu-id="04809-195"><a id="howto_provide_twiml_responses"></a>Como fornecer respostas TwiML de seu próprio site</span><span class="sxs-lookup"><span data-stu-id="04809-195"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="04809-196">Quando o aplicativo inicia uma chamada para a API do Twilio, o Twilio enviará a solicitação a uma URL que deve retornar uma resposta TwiML.</span><span class="sxs-lookup"><span data-stu-id="04809-196">When your application initiates a call to the Twilio API, Twilio will send your request to a URL that is expected to return a TwiML response.</span></span> <span data-ttu-id="04809-197">O exemplo acima usa a URL fornecida pelo Twilio [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="04809-197">The example above uses the Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="04809-198">(Embora o TwiML tenha sido criado para uso do Twilio, você pode exibi-lo em seu navegador.</span><span class="sxs-lookup"><span data-stu-id="04809-198">(While TwiML is designed for use by Twilio, you can view it in your browser.</span></span> <span data-ttu-id="04809-199">Por exemplo, clique em [http://twimlets.com/message][twimlet_message_url] para ver um elemento `<Response>` vazio. Como outro exemplo, clique em [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] para ver um elemento `<Response>` que contém um elemento `<Say>`.)</span><span class="sxs-lookup"><span data-stu-id="04809-199">For example, click [http://twimlets.com/message][twimlet_message_url] to see an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] to see a `<Response>` element that contains a `<Say>` element.)</span></span>

<span data-ttu-id="04809-200">Em vez de contar com a URL fornecida pela Twilio, você pode criar seu próprio site que retorne respostas HTTP.</span><span class="sxs-lookup"><span data-stu-id="04809-200">Instead of relying on the Twilio-provided URL, you can create your own site that returns HTTP responses.</span></span> <span data-ttu-id="04809-201">Você pode criar o site em qualquer linguagem que retorna respostas XML; este tópico pressupõe que você usará Python para criar o TwiML.</span><span class="sxs-lookup"><span data-stu-id="04809-201">You can create the site in any language that returns XML responses; this topic assumes you will be using Python to create the TwiML.</span></span>

<span data-ttu-id="04809-202">Os exemplos a seguir terão como saída uma resposta em TwiML que diz **Hello World** na chamada.</span><span class="sxs-lookup"><span data-stu-id="04809-202">The following examples will output a TwiML response that says **Hello World** on the call.</span></span>

<span data-ttu-id="04809-203">Com o Flash:</span><span class="sxs-lookup"><span data-stu-id="04809-203">With Flask:</span></span>

    from flask import Response
    @app.route("/")
    def hello():
        xml = '<Response><Say>Hello world.</Say></Response>'
        return Response(xml, mimetype='text/xml')

<span data-ttu-id="04809-204">Com o Django:</span><span class="sxs-lookup"><span data-stu-id="04809-204">With Django:</span></span>

    from django.http import HttpResponse
    def hello(request):
        xml = '<Response><Say>Hello world.</Say></Response>'
        return HttpResponse(xml, content_type='text/xml')

<span data-ttu-id="04809-205">Como você pode ver no exemplo acima, a resposta de TwiML é simplesmente um documento XML.</span><span class="sxs-lookup"><span data-stu-id="04809-205">As you can see from the example above, the TwiML response is simply an XML document.</span></span> <span data-ttu-id="04809-206">A biblioteca da Twilio para Python contém classes que geram TwiML para você.</span><span class="sxs-lookup"><span data-stu-id="04809-206">The Twilio library for Python contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="04809-207">O exemplo a seguir produz a resposta equivalente conforme mostrado acima, mas usa o módulo `twiml` na biblioteca da Twilio para Python:</span><span class="sxs-lookup"><span data-stu-id="04809-207">The example below produces the equivalent response as shown above, but uses the `twiml` module in the Twilio library for Python:</span></span>

    from twilio import twiml

    response = twiml.Response()
    response.say("Hello world.")
    print(str(response))

<span data-ttu-id="04809-208">Para obter mais informações sobre TwiML, consulte [https://www.twilio.com/docs/api/twiml][twiml_reference].</span><span class="sxs-lookup"><span data-stu-id="04809-208">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span></span>

<span data-ttu-id="04809-209">Uma vez que o aplicativo Python esteja configurado para fornecer respostas TwiML, use a URL do aplicativo como a URL passada para o método `client.calls.create`.</span><span class="sxs-lookup"><span data-stu-id="04809-209">Once you have your Python application set up to provide TwiML responses, use the URL of the application as the URL passed into the `client.calls.create`  method.</span></span> <span data-ttu-id="04809-210">Por exemplo, se você tiver um aplicativo Web chamado **MyTwiML** implantado em uma serviço hospedado do Azure, você poderá usar a URL como webhook, conforme mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="04809-210">For example, if you have a Web application named **MyTwiML** deployed to an Azure hosted service, you can use its url as webhook as shown in the following example:</span></span>

    from twilio.rest import TwilioRestClient

    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"
    from_number = "NNNNNNNNNNN"
    to_number = "NNNNNNNNNNN"
    url = "http://your-domain-label.centralus.cloudapp.azure.com/MyTwiML/"

    # Initialize the Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make the call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url)
    print(call.sid)

## <span data-ttu-id="04809-211"><a id="AdditionalServices"></a>Como Usar os Serviços Adicionais do Twilio</span><span class="sxs-lookup"><span data-stu-id="04809-211"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="04809-212">Além dos exemplos mostrados aqui, o Twilio oferece APIs baseadas na Web que podem ser usadas para aproveitar a funcionalidade adicional do Twilio do aplicativo Azure.</span><span class="sxs-lookup"><span data-stu-id="04809-212">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="04809-213">Para obter detalhes completos, consulte a [Documentação da API do Twilio][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="04809-213">For full details, see the [Twilio API documentation][twilio_api].</span></span>

## <span data-ttu-id="04809-214"><a id="NextSteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="04809-214"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="04809-215">Agora que você aprendeu as noções básicas do serviço Twilio, siga estes links para saber mais:</span><span class="sxs-lookup"><span data-stu-id="04809-215">Now that you have learned the basics of the Twilio service, follow these links to learn more:</span></span>

* <span data-ttu-id="04809-216">[Diretrizes de segurança do Twilio][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="04809-216">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="04809-217">[Código de Exemplo e Guias de Procedimentos do Twilio][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="04809-217">[Twilio HowTo Guides and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="04809-218">[Tutoriais do Guia de início rápido do Twilio][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="04809-218">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span>
* <span data-ttu-id="04809-219">[Twilio no GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="04809-219">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="04809-220">[Fale com o suporte do Twilio][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="04809-220">[Talk to Twilio Support][twilio_support]</span></span>

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
