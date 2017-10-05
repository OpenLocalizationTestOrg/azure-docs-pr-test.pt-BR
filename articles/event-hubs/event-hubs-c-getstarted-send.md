---
title: Enviar eventos para Hubs de Eventos do Azure usando C | Microsoft Docs
description: Enviar eventos para Hubs de Eventos do Azure usando C
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
ms.openlocfilehash: a615ee39b6c3731cc7df366e9fabeed5219a71b4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="send-events-to-azure-event-hubs-using-c"></a><span data-ttu-id="c4375-103">Enviar eventos para Hubs de Eventos do Azure usando C</span><span class="sxs-lookup"><span data-stu-id="c4375-103">Send events to Azure Event Hubs using C</span></span>

## <a name="introduction"></a><span data-ttu-id="c4375-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="c4375-104">Introduction</span></span>
<span data-ttu-id="c4375-105">Os Hubs de Eventos são um sistema de ingestão altamente escalonável que pode ingerir milhões de eventos por segundo, permitindo que um aplicativo processe e analise grandes quantidades de dados produzidos por aplicativos e dispositivos conectados.</span><span class="sxs-lookup"><span data-stu-id="c4375-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application to process and analyze the massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="c4375-106">Depois de coletados em um hub de eventos, você pode transformar e armazenar dados usando qualquer provedor de análise em tempo real ou cluster de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c4375-106">Once collected into an event hub, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="c4375-107">Para saber mais, confira a [Visão geral dos Hubs de Eventos][Visão geral dos Hubs de Eventos].</span><span class="sxs-lookup"><span data-stu-id="c4375-107">For more information, please see the [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="c4375-108">Neste tutorial, você aprenderá a enviar eventos para um hub de eventos usando um aplicativo de console em C. Para receber eventos, clique na linguagem apropriada de recebimento no sumário à esquerda.</span><span class="sxs-lookup"><span data-stu-id="c4375-108">In this tutorial, you will learn how to send events to an event hub using a console application in C. To receive events, click the appropriate receiving language in the left-hand table of contents.</span></span>

<span data-ttu-id="c4375-109">Para concluir este tutorial, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="c4375-109">To complete this tutorial, you will need the following:</span></span>

* <span data-ttu-id="c4375-110">Um ambiente de desenvolvimento C.</span><span class="sxs-lookup"><span data-stu-id="c4375-110">A C development environment.</span></span> <span data-ttu-id="c4375-111">Para este tutorial, vamos pressupor a pilha gcc em uma Máquina Virtual Linux do Azure com Ubuntu 14.04.</span><span class="sxs-lookup"><span data-stu-id="c4375-111">For this tutorial, we will assume the gcc stack on an Azure Linux VM with Ubuntu 14.04.</span></span>
* <span data-ttu-id="c4375-112">[Microsoft Visual Studio](https://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="c4375-112">[Microsoft Visual Studio](https://www.visualstudio.com/).</span></span>
* <span data-ttu-id="c4375-113">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4375-113">An active Azure account.</span></span> <span data-ttu-id="c4375-114">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="c4375-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="c4375-115">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c4375-115">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="send-messages-to-event-hubs"></a><span data-ttu-id="c4375-116">Enviar mensagens ao Hub de Eventos</span><span class="sxs-lookup"><span data-stu-id="c4375-116">Send messages to Event Hubs</span></span>
<span data-ttu-id="c4375-117">Nesta seção, escreveremos um aplicativo C para enviar eventos ao seu hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="c4375-117">In this section we write a C app to send events to your event hub.</span></span> <span data-ttu-id="c4375-118">O código usa a biblioteca Proton AMQP do [projeto Apache Qpid](http://qpid.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="c4375-118">The code uses the Proton AMQP library from the [Apache Qpid project](http://qpid.apache.org/).</span></span> <span data-ttu-id="c4375-119">Isso é semelhante a usar Tópicos e Filas do Barramento de Serviço com AMQP por meio de C, como mostrado [aqui](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504).</span><span class="sxs-lookup"><span data-stu-id="c4375-119">This is analogous to using Service Bus queues and topics with AMQP from C as shown [here](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504).</span></span> <span data-ttu-id="c4375-120">Para obter mais informações, consulte a [documentação Qpid Proton](http://qpid.apache.org/proton/index.html).</span><span class="sxs-lookup"><span data-stu-id="c4375-120">For more information, see [Qpid Proton documentation](http://qpid.apache.org/proton/index.html).</span></span>

1. <span data-ttu-id="c4375-121">Na [página Qpid AMQP Messenger](https://qpid.apache.org/proton/messenger.html), siga as instruções para instalar o Qpid Proton, de acordo com o ambiente.</span><span class="sxs-lookup"><span data-stu-id="c4375-121">From the [Qpid AMQP Messenger page](https://qpid.apache.org/proton/messenger.html), follow the instructions to install Qpid Proton, depending on your environment.</span></span>
2. <span data-ttu-id="c4375-122">Para compilar a biblioteca Proton, instale os pacotes a seguir:</span><span class="sxs-lookup"><span data-stu-id="c4375-122">To compile the Proton library, install the following packages:</span></span>
   
    ```shell
    sudo apt-get install build-essential cmake uuid-dev openssl libssl-dev
    ```
3. <span data-ttu-id="c4375-123">Baixe a [biblioteca Qpid Proton](http://qpid.apache.org/proton/index.html) e extraia-a, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="c4375-123">Download the [Qpid Proton library](http://qpid.apache.org/proton/index.html), and extract it, e.g.:</span></span>
   
    ```shell
    wget http://archive.apache.org/dist/qpid/proton/0.7/qpid-proton-0.7.tar.gz
    tar xvfz qpid-proton-0.7.tar.gz
    ```
4. <span data-ttu-id="c4375-124">Crie um diretório de compilação, compile e instale:</span><span class="sxs-lookup"><span data-stu-id="c4375-124">Create a build directory, compile and install:</span></span>
   
    ```shell
    cd qpid-proton-0.7
    mkdir build
    cd build
    cmake -DCMAKE_INSTALL_PREFIX=/usr ..
    sudo make install
    ```
5. <span data-ttu-id="c4375-125">No seu diretório de trabalho, crie um novo arquivo chamado **sender.c** com o código a seguir.</span><span class="sxs-lookup"><span data-stu-id="c4375-125">In your work directory, create a new file called **sender.c** with the following code.</span></span> <span data-ttu-id="c4375-126">Lembre-se de substituir o valor do nome do hub de eventos e do nome de namespace.</span><span class="sxs-lookup"><span data-stu-id="c4375-126">Remember to substitute the value for your event hub name and namespace name.</span></span> <span data-ttu-id="c4375-127">Você também deve substituir uma versão codificada em URL da chave para o **SendRule** criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c4375-127">You must also substitute a URL-encoded version of the key for the **SendRule** created earlier.</span></span> <span data-ttu-id="c4375-128">Você pode codificar a URL [aqui](http://www.w3schools.com/tags/ref_urlencode.asp).</span><span class="sxs-lookup"><span data-stu-id="c4375-128">You can URL-encode it [here](http://www.w3schools.com/tags/ref_urlencode.asp).</span></span>
   
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
        printf("Press Ctrl-C to stop the sender process\n");
   
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
6. <span data-ttu-id="c4375-129">Compile o arquivo, supondo que **gcc**:</span><span class="sxs-lookup"><span data-stu-id="c4375-129">Compile the file, assuming **gcc**:</span></span>
   
    ```
    gcc sender.c -o sender -lqpid-proton
    ```

    > [!NOTE]
    > <span data-ttu-id="c4375-130">No código acima, usamos uma janela de saída de 1 para forçar a saída das mensagens assim que possível.</span><span class="sxs-lookup"><span data-stu-id="c4375-130">In this code, we use an outgoing window of 1 to force the messages out as soon as possible.</span></span> <span data-ttu-id="c4375-131">Em geral, o aplicativo deve tentar enviar mensagens em lote para aumentar a taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="c4375-131">In general, your application should try to batch messages to increase throughput.</span></span> <span data-ttu-id="c4375-132">Confira a [página Qpid AMQP Messenger](https://qpid.apache.org/proton/messenger.html) para obter informações sobre como usar a biblioteca Qpid Proton neste e em outros ambientes e de plataformas para as quais associações são fornecidas (atualmente Perl, PHP, Python e Ruby).</span><span class="sxs-lookup"><span data-stu-id="c4375-132">See the [Qpid AMQP Messenger page](https://qpid.apache.org/proton/messenger.html) for information about how to use the Qpid Proton library in this and other environments, and from platforms for which bindings are provided (currently Perl, PHP, Python, and Ruby).</span></span>


## <a name="next-steps"></a><span data-ttu-id="c4375-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c4375-133">Next steps</span></span>
<span data-ttu-id="c4375-134">Você pode saber mais sobre Hubs de Eventos visitando os links abaixo:</span><span class="sxs-lookup"><span data-stu-id="c4375-134">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="c4375-135">Visão Geral dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="c4375-135">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md
)
* [<span data-ttu-id="c4375-136">Criar um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="c4375-136">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="c4375-137">Perguntas frequentes sobre os Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="c4375-137">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Images. -->
[21]: ./media/event-hubs-c-ephcs-getstarted/run-csharp-ephcs1.png
[24]: ./media/event-hubs-c-ephcs-getstarted/receive-eph-c.png
