---
title: suporte a aaaHTTP/2 no Azure CDN | Microsoft Docs
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
ms.openlocfilehash: 2e5e5345e8cf5c40e080ebf18b4f13a239a5aac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="http2-support-in-azure-cdn"></a>Suporte a HTTP/2 na CDN do Azure

HTTP/2 é tooHTTP/1.1\ uma revisão principal. Fornece mais rapidamente o desempenho da web, tempo de resposta reduzida e usuário aprimorada experiência, mantendo Olá familiares métodos HTTP, códigos de status e semântica. Embora HTTP/2 toowork projetado com HTTP e HTTPS, muitos navegadores da web de cliente suportam apenas HTTP/2 por TLS.

###<a name="http2-benefits"></a>Benefícios do HTTP/2

saudação de HTTP/2 benefícios:

*   **Multiplexação e simultaneidade**

    Usando o HTTP 1.1, fazer várias solicitações de recursos requer várias conexões TCP, sendo que cada conexão tem uma sobrecarga de desempenho associada a ela. 2/HTTP permite que vários toobe recursos solicitado em uma única conexão de TCP.

*   **Compactação de cabeçalho**

    Compactando cabeçalhos Olá HTTP para recursos atendidos, tempo de transmissão de saudação é reduzido significativamente.

*   **Dependências de fluxo**

    Dependências de fluxo permitir que o cliente Olá tooindicate toohello server quais recursos têm prioridade.


##<a name="http2-browser-support"></a>Suporte a Navegador HTTP/2

Todos os principais navegadores de saudação implementou o suporte HTTP/2 em suas versões atuais. Navegadores com suporte não serão automaticamente fallback tooHTTP/1.1.

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

benefícios de saudação toosee de HTTP/2 em ação, consulte [esta demonstração do Akamai](https://http2.akamai.com/demo).

toolearn mais sobre HTTP/2, visite Olá recursos a seguir:

*   [Home page de especificação HTTP/2](https://http2.github.io/)
*   [Perguntas Frequentes Oficiais do HTTP/2](https://http2.github.io/faq/)
*   [Informações de HTTP/2 do Akamai](https://http2.akamai.com/)

toolearn mais sobre os recursos disponíveis do Azure CDN, consulte Olá [visão geral do Azure CDN](https://azure.microsoft.com/documentation/articles/cdn-overview/).
