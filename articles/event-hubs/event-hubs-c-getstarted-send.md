---
title: aaaSend eventos tooAzure Hubs de eventos usando C | Microsoft Docs
description: Enviar eventos tooAzure Hubs de eventos usando C
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: c
ms.devlang: csharp
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: bb53300c070debb4a3658a38df9d3966f08e81ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooazure-event-hubs-using-c"></a><span data-ttu-id="2531e-103">Enviar eventos tooAzure Hubs de eventos usando C</span><span class="sxs-lookup"><span data-stu-id="2531e-103">Send events tooAzure Event Hubs using C</span></span>

## <a name="introduction"></a><span data-ttu-id="2531e-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="2531e-104">Introduction</span></span>
<span data-ttu-id="2531e-105">Hubs de eventos é um sistema de inclusão altamente escalonável que pode ingestão milhões de eventos por segundo, permitindo que um aplicativo tooprocess e analisar Olá grandes quantidades de dados produzidos por seus aplicativos e dispositivos conectados.</span><span class="sxs-lookup"><span data-stu-id="2531e-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application tooprocess and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="2531e-106">Depois de coletados em um hub de eventos, você pode transformar e armazenar dados usando qualquer provedor de análise em tempo real ou cluster de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2531e-106">Once collected into an event hub, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="2531e-107">Para obter mais informações, consulte Olá [Visão geral de Hubs de eventos] [Visão geral de Hubs de eventos].</span><span class="sxs-lookup"><span data-stu-id="2531e-107">For more information, please see hello [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="2531e-108">Neste tutorial, você aprenderá como o hub de eventos toosend eventos tooan usando um aplicativo de console em c. tooreceive eventos, clique em idioma de recebimento apropriado Olá Olá esquerdo sumário.</span><span class="sxs-lookup"><span data-stu-id="2531e-108">In this tutorial, you will learn how toosend events tooan event hub using a console application in C. tooreceive events, click hello appropriate receiving language in hello left-hand table of contents.</span></span>

<span data-ttu-id="2531e-109">toocomplete neste tutorial, você precisará Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="2531e-109">toocomplete this tutorial, you will need hello following:</span></span>

* <span data-ttu-id="2531e-110">Um ambiente de desenvolvimento C.</span><span class="sxs-lookup"><span data-stu-id="2531e-110">A C development environment.</span></span> <span data-ttu-id="2531e-111">Para este tutorial, vamos pressupor pilha de gcc Olá em uma VM do Linux do Azure com o Ubuntu 14.04.</span><span class="sxs-lookup"><span data-stu-id="2531e-111">For this tutorial, we will assume hello gcc stack on an Azure Linux VM with Ubuntu 14.04.</span></span>
* <span data-ttu-id="2531e-112">[Microsoft Visual Studio](https://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="2531e-112">[Microsoft Visual Studio](https://www.visualstudio.com/).</span></span>
* <span data-ttu-id="2531e-113">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="2531e-113">An active Azure account.</span></span> <span data-ttu-id="2531e-114">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="2531e-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="2531e-115">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2531e-115">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="send-messages-tooevent-hubs"></a><span data-ttu-id="2531e-116">Enviar mensagens tooEvent Hubs</span><span class="sxs-lookup"><span data-stu-id="2531e-116">Send messages tooEvent Hubs</span></span>
<span data-ttu-id="2531e-117">Esta seção é escrever um hub de eventos C aplicativo toosend eventos tooyour.</span><span class="sxs-lookup"><span data-stu-id="2531e-117">In this section we write a C app toosend events tooyour event hub.</span></span> <span data-ttu-id="2531e-118">código Olá usa a biblioteca de AMQP Proton de saudação do hello [projeto Apache Qpid](http://qpid.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="2531e-118">hello code uses hello Proton AMQP library from hello [Apache Qpid project](http://qpid.apache.org/).</span></span> <span data-ttu-id="2531e-119">Isso é análogo toousing filas de barramento de serviço e os tópicos com AMQP do C conforme mostrado [aqui](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504).</span><span class="sxs-lookup"><span data-stu-id="2531e-119">This is analogous toousing Service Bus queues and topics with AMQP from C as shown [here](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504).</span></span> <span data-ttu-id="2531e-120">Para obter mais informações, consulte a [documentação Qpid Proton](http://qpid.apache.org/proton/index.html).</span><span class="sxs-lookup"><span data-stu-id="2531e-120">For more information, see [Qpid Proton documentation](http://qpid.apache.org/proton/index.html).</span></span>

1. <span data-ttu-id="2531e-121">De saudação [página Qpid AMQP Messenger](https://qpid.apache.org/proton/messenger.html), siga Olá instruções tooinstall Qpid Proton, dependendo do seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="2531e-121">From hello [Qpid AMQP Messenger page](https://qpid.apache.org/proton/messenger.html), follow hello instructions tooinstall Qpid Proton, depending on your environment.</span></span>
2. <span data-ttu-id="2531e-122">toocompile Olá biblioteca Proton, instale o hello pacotes a seguir:</span><span class="sxs-lookup"><span data-stu-id="2531e-122">toocompile hello Proton library, install hello following packages:</span></span>
   
    ```shell
    sudo apt-get install build-essential cmake uuid-dev openssl libssl-dev
    ```
3. <span data-ttu-id="2531e-123">Baixar Olá [biblioteca Qpid Proton](http://qpid.apache.org/proton/index.html)e extraí-lo, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="2531e-123">Download hello [Qpid Proton library](http://qpid.apache.org/proton/index.html), and extract it, e.g.:</span></span>
   
    ```shell
    wget http://archive.apache.org/dist/qpid/proton/0.7/qpid-proton-0.7.tar.gz
    tar xvfz qpid-proton-0.7.tar.gz
    ```
4. <span data-ttu-id="2531e-124">Crie um diretório de compilação, compile e instale:</span><span class="sxs-lookup"><span data-stu-id="2531e-124">Create a build directory, compile and install:</span></span>
   
    ```shell
    cd qpid-proton-0.7
    mkdir build
    cd build
    cmake -DCMAKE_INSTALL_PREFIX=/usr ..
    sudo make install
    ```
5. <span data-ttu-id="2531e-125">Em seu diretório de trabalho, crie um novo arquivo chamado **sender.c** com hello código a seguir.</span><span class="sxs-lookup"><span data-stu-id="2531e-125">In your work directory, create a new file called **sender.c** with hello following code.</span></span> <span data-ttu-id="2531e-126">Lembre-se o valor de saudação toosubstitute seu nome de hub de evento e o nome do namespace.</span><span class="sxs-lookup"><span data-stu-id="2531e-126">Remember toosubstitute hello value for your event hub name and namespace name.</span></span> <span data-ttu-id="2531e-127">Você também deve substituir uma versão codificada por URL da chave Olá Olá **SendRule** criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2531e-127">You must also substitute a URL-encoded version of hello key for hello **SendRule** created earlier.</span></span> <span data-ttu-id="2531e-128">Você pode codificar a URL [aqui](http://www.w3schools.com/tags/ref_urlencode.asp).</span><span class="sxs-lookup"><span data-stu-id="2531e-128">You can URL-encode it [here](http://www.w3schools.com/tags/ref_urlencode.asp).</span></span>
   
    ```c
    #include "proton/message.h"
    #include "proton/messenger.h"
   
    #include <getopt.h>
    #include <proton/util.h>
    #include <sys/time.h>
    #include <stddef.h>
    #include <stdio.h>
    #include <string.h>
    #include <unistd.h>
    #include <stdlib.h>
   
    #define check(messenger)                                                     
      {                                                                          
        if(pn_messenger_errno(messenger))                                        
        {                                                                        
          printf("check\n");                                                     
          die(__FILE__, __LINE__, pn_error_text(pn_messenger_error(messenger))); 
        }                                                                        
      }  
   
    pn_timestamp_t time_now(void)
    {
      struct timeval now;
      if (gettimeofday(&now, NULL)) pn_fatal("gettimeofday failed\n");
      return ((pn_timestamp_t)now.tv_sec) * 1000 + (now.tv_usec / 1000);
    }  
   
    void die(const char *file, int line, const char *message)
    {
      printf("Dead\n");
      fprintf(stderr, "%s:%i: %s\n", file, line, message);
      exit(1);
    }
   
    int sendMessage(pn_messenger_t * messenger) {
        char * address = (char *) "amqps://SendRule:{Send Rule key}@{namespace name}.servicebus.windows.net/{event hub name}";
        char * msgtext = (char *) "Hello from C!";
   
        pn_message_t * message;
        pn_data_t * body;
        message = pn_message();
   
        pn_message_set_address(message, address);
        pn_message_set_content_type(message, (char*) "application/octect-stream");
        pn_message_set_inferred(message, true);
   
        body = pn_message_body(message);
        pn_data_put_binary(body, pn_bytes(strlen(msgtext), msgtext));
   
        pn_messenger_put(messenger, message);
        check(messenger);
        pn_messenger_send(messenger, 1);
        check(messenger);
   
        pn_message_free(message);
    }
   
    int main(int argc, char** argv) {
        printf("Press Ctrl-C toostop hello sender process\n");
   
        pn_messenger_t *messenger = pn_messenger(NULL);
        pn_messenger_set_outgoing_window(messenger, 1);
        pn_messenger_start(messenger);
   
        while(true) {
            sendMessage(messenger);
            printf("Sent message\n");
            sleep(1);
        }
   
        // release messenger resources
        pn_messenger_stop(messenger);
        pn_messenger_free(messenger);
   
        return 0;
    }
    ```
6. <span data-ttu-id="2531e-129">Compilar arquivo hello, supondo que **gcc**:</span><span class="sxs-lookup"><span data-stu-id="2531e-129">Compile hello file, assuming **gcc**:</span></span>
   
    ```
    gcc sender.c -o sender -lqpid-proton
    ```

    > [!NOTE]
    > <span data-ttu-id="2531e-130">Esse código, usamos uma janela de saída 1 tooforce das mensagens de saudação out assim que possível.</span><span class="sxs-lookup"><span data-stu-id="2531e-130">In this code, we use an outgoing window of 1 tooforce hello messages out as soon as possible.</span></span> <span data-ttu-id="2531e-131">Em geral, seu aplicativo deve tentar a taxa de transferência toobatch mensagens tooincrease.</span><span class="sxs-lookup"><span data-stu-id="2531e-131">In general, your application should try toobatch messages tooincrease throughput.</span></span> <span data-ttu-id="2531e-132">Consulte Olá [página Qpid AMQP Messenger](https://qpid.apache.org/proton/messenger.html) para obter informações sobre como toouse Olá biblioteca Qpid Proton neste e em outros ambientes e de plataformas para o qual as associações são fornecidas (atualmente, Perl, PHP, Python e Ruby).</span><span class="sxs-lookup"><span data-stu-id="2531e-132">See hello [Qpid AMQP Messenger page](https://qpid.apache.org/proton/messenger.html) for information about how toouse hello Qpid Proton library in this and other environments, and from platforms for which bindings are provided (currently Perl, PHP, Python, and Ruby).</span></span>


## <a name="next-steps"></a><span data-ttu-id="2531e-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2531e-133">Next steps</span></span>
<span data-ttu-id="2531e-134">Você pode aprender mais sobre os Hubs de eventos visitando Olá links a seguir:</span><span class="sxs-lookup"><span data-stu-id="2531e-134">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="2531e-135">Visão Geral dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="2531e-135">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md
)
* [<span data-ttu-id="2531e-136">Criar um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="2531e-136">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="2531e-137">Perguntas frequentes sobre os Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="2531e-137">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Images. -->
[21]: ./media/event-hubs-c-ephcs-getstarted/run-csharp-ephcs1.png
[24]: ./media/event-hubs-c-ephcs-getstarted/receive-eph-c.png
