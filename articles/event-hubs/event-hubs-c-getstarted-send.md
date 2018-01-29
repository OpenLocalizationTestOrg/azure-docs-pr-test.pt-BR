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
ms.date: 12/4/2017
ms.author: sethm
ms.openlocfilehash: 2b714c5de96a8fb7ed66a30c62daaa38b84fdc5b
ms.sourcegitcommit: 7136d06474dd20bb8ef6a821c8d7e31edf3a2820
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="send-events-to-azure-event-hubs-using-c"></a>Enviar eventos para Hubs de Eventos do Azure usando C

## <a name="introduction"></a>Introdução
Os Hubs de Eventos são um sistema de ingestão altamente escalonável que pode ingerir milhões de eventos por segundo, permitindo que um aplicativo processe e analise grandes quantidades de dados produzidos por aplicativos e dispositivos conectados. Depois de coletados em um hub de eventos, você pode transformar e armazenar dados usando qualquer provedor de análise em tempo real ou cluster de armazenamento.

Para saber mais, confira a [Visão geral dos Hubs de Eventos][Visão geral dos Hubs de Eventos].

Este tutorial descreve como enviar eventos para um hub de eventos usando um aplicativo de console em C. Para saber mais sobre o recebimento de eventos, clique na linguagem de recebimento apropriada no sumário à esquerda.

Para concluir este tutorial, você precisará do seguinte:

* Um ambiente de desenvolvimento C. Este tutorial considera a pilha gcc em uma VM Linux do Azure com o Ubuntu 14.04.
* [Microsoft Visual Studio](https://www.visualstudio.com/).
* Uma conta ativa do Azure. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).

## <a name="send-messages-to-event-hubs"></a>Enviar mensagens ao Hub de Eventos
Esta seção mostra como gravar um aplicativo em C para enviar eventos ao hub de eventos. O código usa a biblioteca Proton AMQP do [projeto Apache Qpid](http://qpid.apache.org/). Isso é semelhante a usar tópicos e filas do Barramento de Serviço com AMQP do C, como é mostrado [neste exemplo](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504). Para obter mais informações, consulte a [Documentação do Qpid Proton](http://qpid.apache.org/proton/index.html).

1. Na [página Qpid AMQP Messenger](https://qpid.apache.org/proton/messenger.html), siga as instruções para instalar o Qpid Proton, de acordo com o ambiente.
2. Para compilar a biblioteca Proton, instale os pacotes a seguir:
   
    ```shell
    sudo apt-get install build-essential cmake uuid-dev openssl libssl-dev
    ```
3. Baixe a [biblioteca Qpid Proton](http://qpid.apache.org/proton/index.html) e extraia-a, por exemplo:
   
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
5. No seu diretório de trabalho, crie um novo arquivo chamado **sender.c** com o código a seguir. Lembre-se de substituir os valores de chave/nome de SAS, de nome do hub de eventos e de namespace. Você também deve substituir uma versão codificada em URL da chave para o **SendRule** criado anteriormente. Você pode codificar a URL [aqui](http://www.w3schools.com/tags/ref_urlencode.asp).
   
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
   
    #define check(messenger)                                                     \
      {                                                                          \
        if(pn_messenger_errno(messenger))                                        \
        {                                                                        \
          printf("check\n");                                                     \
          die(__FILE__, __LINE__, pn_error_text(pn_messenger_error(messenger))); \
        }                                                                        \
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
        char * address = (char *) "amqps://{SAS Key Name}:{SAS key}@{namespace name}.servicebus.windows.net/{event hub name}";
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
6. Compile o arquivo, supondo que **gcc**:
   
    ```
    gcc sender.c -o sender -lqpid-proton
    ```

    > [!NOTE]
    > Esse código usa uma janela de saída igual a 1 para forçar o envio de mensagens assim que possível. É recomendável que o aplicativo tente enviar mensagens em lote para aumentar a produtividade. Confira a [página Qpid AMQP Messenger](https://qpid.apache.org/proton/messenger.html) para obter informações sobre como usar a biblioteca Qpid Proton neste e em outros ambientes e de plataformas para as quais associações são fornecidas (atualmente Perl, PHP, Python e Ruby).


## <a name="next-steps"></a>Próximas etapas
Você pode saber mais sobre Hubs de Eventos visitando os links abaixo:

* [Visão Geral dos Hubs de Eventos](event-hubs-what-is-event-hubs.md)
* [Perguntas frequentes sobre os Hubs de Eventos](event-hubs-faq.md)

<!-- Images. -->
[21]: ./media/event-hubs-c-ephcs-getstarted/run-csharp-ephcs1.png
[24]: ./media/event-hubs-c-ephcs-getstarted/receive-eph-c.png
