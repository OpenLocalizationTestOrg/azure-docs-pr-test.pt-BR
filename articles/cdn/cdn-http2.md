---
title: Suporte a HTTP/2 na CDN do Azure | Microsoft Docs
description: Saiba mais sobre o suporte a HTTP/2 e CDN.
services: cdn
documentationcenter: 
author: lichard
manager: erikre
editor: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 5/04/2017
ms.author: rli
ms.openlocfilehash: 4f8dd685c3ae89535217d7a17a01c5129ca7e6e4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="http2-support-in-azure-cdn"></a>Suporte a HTTP/2 na CDN do Azure

HTTP/2 é uma revisão principal HTTP/1.1\. Ele fornece mais rápido do desempenho da web, tempo de reposta reduzido e melhor experiência de usuário, mantendo os métodos HTTP familiares, códigos de status e semântica. Embora o HTTP/2 seja projetado para trabalhar com HTTP e HTTPS, muitos navegadores da Web de cliente somente dão suporte a HTTP/2 por TLS.

###<a name="http2-benefits"></a>Benefícios do HTTP/2

Os benefícios do HTTP/2 incluem:

*   **Multiplexação e simultaneidade**

    Usando o HTTP 1.1, fazer várias solicitações de recursos requer várias conexões TCP, sendo que cada conexão tem uma sobrecarga de desempenho associada a ela. O HTTP/2 permite que vários recursos sejam solicitados em uma única conexão TCP.

*   **Compactação de cabeçalho**

    Compactando cabeçalhos HTTP para recursos fornecidos, o tempo de transmissão é reduzido significativamente.

*   **Dependências de fluxo**

    Dependências de fluxo permitem que o cliente indique ao servidor quais recursos têm prioridade.


##<a name="http2-browser-support"></a>Suporte a Navegador HTTP/2

Todos os principais navegadores implementaram o suporte a HTTP/2 em suas versões atuais. O fallback de navegadores sem suporte para HTTP/1.1 ocorrerá automaticamente.

|Navegador|Versão Mínima|
|-------------|------------|
|Microsoft Edge| 12|
|Google Chrome| 43|
|Mozilla Firefox| 38|
|Opera| 32|
|Safari| 9|

##<a name="enabling-http2-support-in-azure-cdn"></a>Habilitar o Suporte a HTTP/2 na CDN do Azure

No momento, o suporte a HTTP/2 está ativo para os perfis **CDN do Azure do Akamai** e **CDN do Azure da Verizon**. Nenhuma ação adicional dos clientes é necessária.

##<a name="next-steps"></a>Próximas etapas

Para ver os benefícios do HTTP/2 em ação, consulte [esta demonstração do Akamai](https://http2.akamai.com/demo).

Para saber mais sobre o HTTP/2, visite os seguintes recursos:

*   [Home page de especificação HTTP/2](https://http2.github.io/)
*   [Perguntas Frequentes Oficiais do HTTP/2](https://http2.github.io/faq/)
*   [Informações de HTTP/2 do Akamai](https://http2.akamai.com/)

Para saber mais sobre os recursos disponíveis da CDN do Azure, consulte a [Visão geral da CDN do Azure](https://azure.microsoft.com/documentation/articles/cdn-overview/).