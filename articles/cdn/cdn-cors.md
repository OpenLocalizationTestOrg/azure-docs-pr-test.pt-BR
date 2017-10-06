---
title: aaaUsing CDN do Azure com CORS | Microsoft Docs
description: Saiba como toouse hello Azure Content Delivery Network (CDN) toowith compartilhamento de recursos entre origens (CORS).
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 86740a96-4269-4060-aba3-a69f00e6f14e
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 6c743b56c32a2d3aacc9a77094cb87d61b95d2f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-cdn-with-cors"></a>Usar a CDN do Azure com o CORS
## <a name="what-is-cors"></a>O que é CORS?
CORS (Cross origem Resource Sharing) é um recurso HTTP que permite que um aplicativo web executando os recursos de tooaccess em um domínio em outro domínio. Possibilidade de saudação de tooreduce de ordem de ataques de script entre sites, todos os navegadores modernos implementam uma restrição de segurança, conhecida como [política de mesma origem](http://www.w3.org/Security/wiki/Same_Origin_Policy).  Isso impede que uma página da Web chame APIs em um domínio diferente.  CORS fornece uma maneira segura tooallow uma origem (domínio de origem Olá) toocall APIs em outra origem.

## <a name="how-it-works"></a>Como funciona
Há dois tipos de solicitações CORS, *solicitações simples* e *solicitações complexas.*

### <a name="for-simple-requests"></a>Para solicitações simples:

1. navegador Olá envia a solicitação CORS de saudação com adicional **origem** cabeçalho de solicitação HTTP. valor Olá desse cabeçalho é a origem de saudação que serviu a página pai hello, o que é definida como a combinação de saudação do *protocolo,* *domínio,* e *porta.*  Quando uma página da https://www.contoso.com tenta tooaccess dados de um usuário na origem de fabrikam.com hello, Olá cabeçalho de solicitação a seguir seria enviado toofabrikam.com:

   `Origin: https://www.contoso.com`

2. servidor de saudação pode responder com qualquer um dos seguintes hello:

   * Um cabeçalho **Access-Control-Allow-Origin** em sua resposta indicando qual site de origem é permitido. Por exemplo:

     `Access-Control-Allow-Origin: https://www.contoso.com`

   * Código de erro HTTP como 403 se o servidor de saudação não permitir solicitação entre origens de saudação depois de verificar se o cabeçalho de origem Olá

   * Um cabeçalho **Access-Control-Allow-Origin** com um caractere curinga que permite todas as origens:

     `Access-Control-Allow-Origin: *`

### <a name="for-complex-requests"></a>Para solicitações complexas:

Uma solicitação complexa é uma solicitação de CORS onde navegador Olá toosend necessária uma *solicitação de simulação* (ou seja, uma investigação preliminar) antes de enviar a solicitação CORS real hello. Olá solicitação de simulação solicita permissão do servidor de saudação se a solicitação CORS original Olá pode continuar e é um `OPTIONS` solicitação toohello mesma URL.

> [!TIP]
> Para obter mais detalhes sobre fluxos de CORS e armadilhas comuns, exibir hello [guia tooCORS para APIs REST](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).
>
>

## <a name="wildcard-or-single-origin-scenarios"></a>Cenários de origem única ou curinga
CORS na CDN do Azure funcionará automaticamente sem nenhuma configuração adicional quando hello **Access-Control-Allow-Origin** cabeçalho é definido toowildcard (*) ou uma origem única.  Olá CDN armazenará em cache primeira resposta do hello e solicitações subsequentes usarão Olá mesmo cabeçalho.

Se as solicitações já foram feitas toohello CDN anterior tooCORS, sendo definido Olá sua origem, você precisará toopurge conteúdo na sua Olá tooreload conteúdo de ponto de extremidade conteúdo com hello **Access-Control-Allow-Origin** cabeçalho.

## <a name="multiple-origin-scenarios"></a>Cenários de várias origens
Se você precisar tooallow uma lista específica de origens toobe permitido para CORS, as coisas são um pouco mais complicadas. problema de saudação ocorre quando Olá CDN armazena em cache Olá **Access-Control-Allow-Origin** cabeçalho para a origem CORS primeiro hello.  Quando uma origem diferente do CORS faz uma solicitação subsequente, Olá CDN servirá Olá armazenado em cache **Access-Control-Allow-Origin** cabeçalho, que não corresponde.  Há várias toocorrect de maneiras isso.

### <a name="azure-cdn-premium-from-verizon"></a>CDN Premium do Azure da Verizon
Olá tooenable de maneira melhor trata toouse **Premium do Azure CDN da Verizon**, que expõe alguns recursos avançados. 

Você precisará de muito[criar uma regra de](cdn-rules-engine.md) toocheck Olá **origem** cabeçalho na solicitação de saudação.  Se for uma origem válida, a regra será definida Olá **Access-Control-Allow-Origin** cabeçalho com origem Olá fornecido na solicitação de saudação.  Se origem Olá especificado em Olá **origem** cabeçalho não é permitido, a regra deve omitir Olá **Access-Control-Allow-Origin** cabeçalho que fará com que a solicitação de saudação do hello navegador tooreject. 

Há toodo de duas maneiras isso com o mecanismo de regras de saudação.  Em ambos os casos, Olá **Access-Control-Allow-Origin** cabeçalho do servidor de origem do arquivo hello completamente é ignorado, o mecanismo de regras do CDN Olá gerencia totalmente Olá permitido origens CORS.

#### <a name="one-regular-expression-with-all-valid-origins"></a>Uma expressão regular com todas as origens válidas
Nesse caso, você criará uma expressão regular que inclui todas as origens de saudação desejado tooallow: 

    https?:\/\/(www\.contoso\.com|contoso\.com|www\.microsoft\.com|microsoft.com\.com)$

> [!TIP]
> A **CDN do Azure da Verizon** usa as [Expressões Regulares Compatíveis com o Perl](http://pcre.org/) como seu mecanismo de expressões regulares.  Você pode usar uma ferramenta como [101 de expressões regulares](https://regex101.com/) toovalidate sua expressão regular.  Observe que o caractere "/" hello é válido em expressões regulares e não precisa de escape de toobe, no entanto, o escape de caractere é considerada uma prática recomendada e é esperado por alguns validadores de regex.
> 
> 

Se corresponder a expressão regular hello, sua regra substitui Olá **Access-Control-Allow-Origin** cabeçalho (se houver) da origem de saudação com origem de saudação que enviou a solicitação de saudação.  Você também pode adicionar outros cabeçalhos CORS, como **Access-Control-Allow-Methods**.

![Exemplo de regras com expressões regulares](./media/cdn-cors/cdn-cors-regex.png)

#### <a name="request-header-rule-for-each-origin"></a>Solicitar a regra de cabeçalho para cada origem.
Em vez de expressões regulares, você pode criar um separado de regra para cada origem você deseja tooallow usando Olá **curinga de cabeçalho de solicitação** [correspondem à condição](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1). Como com o método de expressão regular hello, Olá mecanismo de regras apenas conjuntos de cabeçalhos CORS de saudação. 

![Exemplo de regras sem expressões regulares](./media/cdn-cors/cdn-cors-no-regex.png)

> [!TIP]
> O exemplo hello acima, Olá uso do caractere curinga de saudação * informa ao mecanismo de regras de saudação toomatch HTTP e HTTPS.
> 
> 

### <a name="azure-cdn-standard"></a>Padrão do Azure CDN
No padrão do Azure CDN perfis, Olá somente tooallow do mecanismo de várias origens sem o uso de saudação de origem de curinga Olá é toouse [cache de cadeia de caracteres de consulta](cdn-query-string.md).  Você precisa tooenable configuração de cadeia de caracteres de consulta para o ponto de extremidade CDN hello e, em seguida, usa uma cadeia de caracteres de consulta exclusiva para solicitações de cada domínio permitido. Isso resultará em Olá um objeto separado para cada cadeia de caracteres de consulta exclusiva do cache da CDN. Essa abordagem não é ideal, no entanto, como resultará em várias cópias de saudação mesmo arquivo hello armazenado em cache na CDN.  

