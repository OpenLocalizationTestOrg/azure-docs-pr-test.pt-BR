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
# <a name="send-events-tooazure-event-hubs-using-c"></a>Enviar eventos tooAzure Hubs de eventos usando C

## <a name="introduction"></a>Introdução
Hubs de eventos é um sistema de inclusão altamente escalonável que pode ingestão milhões de eventos por segundo, permitindo que um aplicativo tooprocess e analisar Olá grandes quantidades de dados produzidos por seus aplicativos e dispositivos conectados. Depois de coletados em um hub de eventos, você pode transformar e armazenar dados usando qualquer provedor de análise em tempo real ou cluster de armazenamento.

Para obter mais informações, consulte Olá [Visão geral de Hubs de eventos] [Visão geral de Hubs de eventos].

Neste tutorial, você aprenderá como o hub de eventos toosend eventos tooan usando um aplicativo de console em c. tooreceive eventos, clique em idioma de recebimento apropriado Olá Olá esquerdo sumário.

toocomplete neste tutorial, você precisará Olá a seguir:

* Um ambiente de desenvolvimento C. Para este tutorial, vamos pressupor pilha de gcc Olá em uma VM do Linux do Azure com o Ubuntu 14.04.
* [Microsoft Visual Studio](https://www.visualstudio.com/).
* Uma conta ativa do Azure. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).

## <a name="send-messages-tooevent-hubs"></a>Enviar mensagens tooEvent Hubs
Esta seção é escrever um hub de eventos C aplicativo toosend eventos tooyour. código Olá usa a biblioteca de AMQP Proton de saudação do hello [projeto Apache Qpid](http://qpid.apache.org/). Isso é análogo toousing filas de barramento de serviço e os tópicos com AMQP do C conforme mostrado [aqui](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504). Para obter mais informações, consulte a [documentação Qpid Proton](http://qpid.apache.org/proton/index.html).

1. De saudação [página Qpid AMQP Messenger](https://qpid.apache.org/proton/messenger.html), siga Olá instruções tooinstall Qpid Proton, dependendo do seu ambiente.
2. toocompile Olá biblioteca Proton, instale o hello pacotes a seguir:
   
    ```shell
    sudo apt-get install build-essential cmake uuid-dev openssl libssl-dev
    ```
3. Baixar Olá [biblioteca Qpid Proton](http://qpid.apache.org/proton/index.html)e extraí-lo, por exemplo:
   
    ```shell
    wget http://archive.apache.org/dist/qpid/proton/0.7/qpid-proton-0.7.tar.gz
    tar xvfz qpid-proton-0.7.tar.gz
    ```
4. Crie um diretório de compilação, compile e instale:
   
    ```shell
    cd qpid-proton-0.7
    mkdir build
    cd build
    cmake -DCMAKE_INSTALL_PREFIX=/usr ..
    sudo make install
    ```
5. Em seu diretório de trabalho, crie um novo arquivo chamado **sender.c** com hello código a seguir. Lembre-se o valor de saudação toosubstitute seu nome de hub de evento e o nome do namespace. Você também deve substituir uma versão codificada por URL da chave Olá Olá **SendRule** criado anteriormente. Você pode codificar a URL [aqui](http://www.w3schools.com/tags/ref_urlencode.asp).
   
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
6. Compilar arquivo hello, supondo que **gcc**:
   
    ```
    gcc sender.c -o sender -lqpid-proton
    ```

    > [!NOTE]
    > Esse código, usamos uma janela de saída 1 tooforce das mensagens de saudação out assim que possível. Em geral, seu aplicativo deve tentar a taxa de transferência toobatch mensagens tooincrease. Consulte Olá [página Qpid AMQP Messenger](https://qpid.apache.org/proton/messenger.html) para obter informações sobre como toouse Olá biblioteca Qpid Proton neste e em outros ambientes e de plataformas para o qual as associações são fornecidas (atualmente, Perl, PHP, Python e Ruby).


## <a name="next-steps"></a>Próximas etapas
Você pode aprender mais sobre os Hubs de eventos visitando Olá links a seguir:

* [Visão Geral dos Hubs de Eventos](event-hubs-what-is-event-hubs.md
)
* [Criar um hub de eventos](event-hubs-create.md)
* [Perguntas frequentes sobre os Hubs de Eventos](event-hubs-faq.md)

<!-- Images. -->
[21]: ./media/event-hubs-c-ephcs-getstarted/run-csharp-ephcs1.png
[24]: ./media/event-hubs-c-ephcs-getstarted/receive-eph-c.png
