---
title: Suporte a origens aaaCross recurso Compartilhamento (CORS) | Microsoft Docs
description: "Saiba como o suporte de CORS tooenable para Olá serviços de armazenamento do Microsoft Azure."
services: storage
documentationcenter: .net
author: cbrooksmsft
manager: carmonm
editor: tysonn
ms.assetid: a0229595-5b64-4898-b8d6-fa2625ea6887
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 2/22/2017
ms.author: cbrooks
ms.openlocfilehash: 0a6ec3bf6999c5faa7f0912dc2a47921aa01d3d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="cross-origin-resource-sharing-cors-support-for-hello-azure-storage-services"></a>Suporte a compartilhamento de recursos entre origens (CORS) Olá serviços de armazenamento do Azure
Serviços de armazenamento do Azure Olá começando com a versão 2013-08-15, suportam a compartilhamento de recursos entre origens (CORS) para serviços de Blob, tabela, fila e arquivo hello. CORS é um recurso HTTP que permite que um aplicativo web executando os recursos de tooaccess em um domínio em outro domínio. Navegadores da Web implementam uma restrição de segurança, conhecida como [política de mesma origem](http://www.w3.org/Security/wiki/Same_Origin_Policy) que impede que uma página da web de APIs de chamada em um domínio diferente; CORS fornece uma maneira segura tooallow um domínio (domínio de origem Olá) toocall APIs em outro domínio. Consulte Olá [especificação CORS](http://www.w3.org/TR/cors/) para obter detalhes sobre o CORS.

Você pode definir regras de CORS individualmente para cada Olá serviços de armazenamento, chamando [definir propriedades do serviço Blob](https://msdn.microsoft.com/library/hh452235.aspx), [definir propriedades de serviço de fila](https://msdn.microsoft.com/library/hh452232.aspx), e [definir propriedades do serviço tabela](https://msdn.microsoft.com/library/hh452240.aspx). Depois de definir regras de CORS Olá para serviço hello, uma solicitação autenticada corretamente feita no serviço de saudação de um domínio diferente será avaliada toodetermine se é permitido de acordo com as regras de toohello que você especificou.

> [!NOTE]
> Observe que CORS não é um mecanismo de autenticação. Qualquer solicitação feita em um recurso de armazenamento quando CORS estiver habilitado deve ter uma assinatura de autenticação adequada ou deverá ser feita em um recurso público.
> 
> 

## <a name="understanding-cors-requests"></a>Noções básicas sobre solicitações CORS
Uma solicitação CORS de um domínio de origem pode consistir em duas solicitações separadas:

* Uma solicitação de simulação, que consulta as restrições de CORS Olá impostas pelo serviço de saudação. solicitação de simulação de saudação é necessária a menos que seja o método de solicitação Olá um [método simples](http://www.w3.org/TR/cors/), significando GET, HEAD ou POST.
* solicitação de real Hello, feita no recurso de saudação desejado.

### <a name="preflight-request"></a>Solicitação de simulação
consultas de solicitação de simulação Olá Olá restrições de CORS que foram estabelecidas pelo proprietário da conta Olá Olá para serviço de armazenamento. navegador da web de Hello (ou outro agente do usuário) envia uma solicitação de opções que inclui os cabeçalhos de solicitação hello, domínio de origem e de método. serviço de armazenamento de saudação é avaliada com base em um conjunto pré-configurado de regras CORS que especifique quais domínios de origem, métodos de solicitação de operação de saudação que se destina e cabeçalhos de solicitação podem ser especificados em uma solicitação real em relação a um recurso de armazenamento.

Se CORS estiver habilitado para o serviço de saudação e houver uma regra CORS que corresponda a solicitação de simulação Olá, serviço de Olá responderá com o código de status 200 (Okey) e inclui cabeçalhos de controle de acesso de saudação necessários na resposta de saudação.

Se CORS não estiver habilitado para o serviço de saudação ou nenhuma regra CORS corresponder a solicitação de simulação hello, serviço Olá responderá com o código de status 403 (proibido).

Se Olá solicitação OPTIONS não contiver hello cabeçalhos de CORS obrigatórios (Olá origem e os cabeçalhos Access-Control-Request-Method), o serviço de saudação responderá com o código de status 400 (solicitação incorreta).

Observe que uma solicitação de simulação é avaliada no serviço de saudação (Blob, fila e tabela) e não em relação ao Olá recurso solicitado. proprietário da conta Olá deve ter habilitado CORS como parte das propriedades do serviço de conta Olá em ordem para Olá toosucceed de solicitação.

### <a name="actual-request"></a>Solicitação real
Depois de solicitação de simulação de saudação é aceita e Olá resposta é retornada, navegador Olá enviará a solicitação real Olá no recurso de armazenamento de saudação. navegador Olá negará a solicitação real Olá imediatamente se hello solicitação de simulação será rejeitada.

solicitação real Olá é tratada como normal solicitação no serviço de armazenamento de saudação. presença de saudação do cabeçalho de origem Olá indica que Olá solicitação é uma solicitação CORS e serviço de saudação verificará Olá CORS regras de correspondência. Se uma correspondência for encontrada, cabeçalhos de controle de acesso de saudação são adicionados toohello resposta e enviados toohello back cliente. Se uma correspondência não for encontrada, os cabeçalhos de controle de acesso de CORS Olá não são retornados.

## <a name="enabling-cors-for-hello-azure-storage-services"></a>Habilitando CORS para serviços de armazenamento do Azure Olá
Regras de CORS são definidas no nível de serviço hello, portanto, você precisa tooenable ou desabilitar CORS para cada serviço (Blob, fila e tabela) separadamente. Por padrão, o CORS está desabilitado para cada serviço. tooenable CORS, você precisa de propriedades de serviço adequadas Olá tooset usando a versão 2013-08-15 ou posterior e adicionar regras de CORS toohello propriedades de serviço. Para obter detalhes sobre como tooenable ou desabilitar CORS para um serviço e como tooset CORS regras, por favor consulte muito[definir propriedades do serviço Blob](https://msdn.microsoft.com/library/hh452235.aspx), [definir propriedades de serviço de fila](https://msdn.microsoft.com/library/hh452232.aspx), e [definir tabela Propriedades do serviço](https://msdn.microsoft.com/library/hh452240.aspx).

Aqui está um exemplo de uma única regra CORS, especificada por meio de uma operação de definir propriedades do serviço:

```xml
<Cors>    
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com, http://www.fabrikam.com</AllowedOrigins>
        <AllowedMethods>PUT,GET</AllowedMethods>
        <AllowedHeaders>x-ms-meta-data*,x-ms-meta-target*,x-ms-meta-abc</AllowedHeaders>
        <ExposedHeaders>x-ms-meta-*</ExposedHeaders>
        <MaxAgeInSeconds>200</MaxAgeInSeconds>
    </CorsRule>
<Cors>
```

Cada elemento incluído na regra CORS Olá é descrito abaixo:

* **AllowedOrigins**: domínios de origem Olá permitidos toomake uma solicitação em relação ao armazenamento de saudação do serviço por meio de CORS. Olá origem domínio é saudação do qual Olá se origina a solicitação. Observe que a origem Olá deve ser uma correspondência exata de maiusculas e minúsculas com idade de saudação do usuário envia toohello serviço de origem de saudação. Você também pode usar o caractere curinga de saudação ' *' tooallow todas as solicitações de toomake de domínios de origem por meio de CORS. O exemplo hello acima, Olá domínios [http://www.contoso.com](http://www.contoso.com) e [http://www.fabrikam.com](http://www.fabrikam.com) podem fazer solicitações para o serviço de saudação usando CORS.
* **AllowedMethods**: métodos de saudação (verbos de solicitação HTTP) desse domínio de origem Olá pode usar para uma solicitação de CORS. No exemplo hello acima, somente as solicitações PUT e GET são permitidas.
* **AllowedHeaders**: cabeçalhos de solicitação Olá desse domínio de origem Olá pode especificar na solicitação CORS hello. No exemplo hello acima, todos os cabeçalhos de metadados, começando com o x-ms-meta-data, x-ms-meta-alvo e x-ms-meta-abc são permitidos. Observe o caractere curinga Olá ' *' indica que todos os cabeçalhos que começam com hello especificado é permitido um prefixo.
* **ExposedHeaders**: Olá cabeçalhos de resposta que podem ser enviados na solicitação CORS Olá resposta toohello e expostos pelo emissor da solicitação Olá navegador toohello. No exemplo hello acima, o navegador de saudação é instruções tooexpose partir qualquer cabeçalho x-ms-meta.
* **MaxAgeInSeconds**: Olá quantidade máxima de tempo que um navegador deve armazenar em cache de solicitação do hello simulação OPTIONS.

Olá serviços de armazenamento do Azure dar suporte a especificação de cabeçalhos prefixados para ambos os Olá **AllowedHeaders** e **ExposedHeaders** elementos. tooallow uma categoria de cabeçalhos, você pode especificar uma categoria de toothat prefixo comum. Por exemplo, especificar *x-ms-meta** como um cabeçalho prefixado estabelece uma regra que corresponderá a todos os cabeçalhos que começam com x-ms-meta.

Olá seguintes limitações se aplicam a regras tooCORS:

* Você pode especificar o toofive regras CORS por serviço de armazenamento (Blob, tabela e fila).
* tamanho máximo de saudação de todas as regras as configurações CORS na solicitação hello, excluindo as marcas XML, não deve exceder 2 KB.
* comprimento de saudação de um cabeçalho permitido, cabeçalho exposto ou origem permitida não deve exceder 256 caracteres.
* Cabeçalhos expostos e cabeçalhos permitidos podem ser:
  * Cabeçalhos literais, onde nome exato do cabeçalho de saudação é fornecido, como **x-ms-meta-processed**. Um máximo de 64 cabeçalhos literais pode ser especificado na solicitação de saudação.
  * Cabeçalhos prefixados, onde um prefixo Olá cabeçalho é fornecido, como **x-ms-meta-data***. Especificar um prefixo dessa maneira permite ou expõe qualquer cabeçalho que comece com hello fornecido prefixo. Um máximo de dois cabeçalhos prefixados pode ser especificado na solicitação de saudação.
* Olá métodos (ou verbos HTTP) especificados no hello **AllowedMethods** elemento deve estar de acordo com os métodos de toohello suportados pelas APIs do serviço de armazenamento do Azure. Métodos com suporte são DELETE, GET, HEAD, MERGE, POST, OPTIONS e PUT.

## <a name="understanding-cors-rule-evaluation-logic"></a>Noções básicas sobre a lógica de avaliação da regra de CORS
Quando um serviço de armazenamento recebe uma solicitação de simulação ou real, ele avalia que a solicitação com base nas regras CORS Olá estabelecida para o serviço Olá por meio da operação de definir propriedades de serviço apropriada hello. Regras de CORS são avaliadas na ordem de saudação na qual eles foram definidos no corpo da solicitação de saudação da saudação operação definir propriedades de serviço.

As regras de CORS são avaliadas da seguinte maneira:

1. Primeiro, o domínio de origem de saudação da solicitação de saudação é verificado em relação Olá domínios listados para Olá **AllowedOrigins** elemento. Se o domínio de origem hello está incluído na lista de hello, ou todos os domínios são permitidos com caractere curinga de saudação ' *', prossegue de avaliação de regras. Se o domínio de origem de saudação não for incluído, solicitação de saudação falhará.
2. Em seguida, o método hello (ou verbo HTTP) da solicitação de saudação é verificado no hello métodos listados no hello **AllowedMethods** elemento. Se o método hello está incluído na lista de Olá, as regras avaliação serão continuadas; Se não, então Olá solicitação falhará.
3. Se a solicitação Olá corresponde a uma regra em seu domínio de origem e seu método, essa regra é selecionado tooprocess Olá solicitação e nenhuma regra adicional será avaliada. Antes de solicitação de saudação pode ser bem-sucedida, no entanto, todos os cabeçalhos especificados na solicitação de saudação são comparados Olá cabeçalhos listados no hello **AllowedHeaders** elemento. Se cabeçalhos de saudação enviados não corresponderem Olá cabeçalhos permitido, falha na solicitação de saudação.

Regras de saudação são processadas na ordem de saudação estiverem presentes no corpo da solicitação Olá, práticas recomendadas recomendam que você especifique as regras mais restritivas Olá com respeitam tooorigins primeiro na lista de hello, para que elas sejam avaliadas primeiro. Especifica regras que são menos restritivas – por exemplo, um tooallow regra todas as origens – no final de saudação da lista de saudação.

### <a name="example--cors-rules-evaluation"></a>Exemplo – avaliação das regras de CORS
Olá, exemplo a seguir mostra um corpo de solicitação parcial para uma operação tooset as regras de CORS para os serviços de armazenamento de saudação. Consulte [definir propriedades do serviço Blob](https://msdn.microsoft.com/library/hh452235.aspx), [definir propriedades de serviço de fila](https://msdn.microsoft.com/library/hh452232.aspx), e [definir propriedades do serviço de tabela](https://msdn.microsoft.com/library/hh452240.aspx) para obter detalhes sobre como construir a solicitação de saudação.

```xml
<Cors>
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com</AllowedOrigins>
        <AllowedMethods>PUT,HEAD</AllowedMethods>
        <MaxAgeInSeconds>5</MaxAgeInSeconds>
        <ExposedHeaders>x-ms-*</ExposedHeaders>
        <AllowedHeaders>x-ms-blob-content-type, x-ms-blob-content-disposition</AllowedHeaders>
    </CorsRule>
    <CorsRule>
        <AllowedOrigins>*</AllowedOrigins>
        <AllowedMethods>PUT,GET</AllowedMethods>
        <MaxAgeInSeconds>5</MaxAgeInSeconds>
        <ExposedHeaders>x-ms-*</ExposedHeaders>
        <AllowedHeaders>x-ms-blob-content-type, x-ms-blob-content-disposition</AllowedHeaders>
    </CorsRule>
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com</AllowedOrigins>
        <AllowedMethods>GET</AllowedMethods>
        <MaxAgeInSeconds>5</MaxAgeInSeconds>
        <ExposedHeaders>x-ms-*</ExposedHeaders>
        <AllowedHeaders>x-ms-client-request-id</AllowedHeaders>
    </CorsRule>
</Cors>
```

Em seguida, considere Olá solicitações CORS a seguir:

| Solicitação |  |  | Resposta |  |
| --- | --- | --- | --- | --- |
| **Método** |**Origem** |**Cabeçalhos da solicitação** |**Correspondência de regra** |**Resultado** |
| **PUT** |http://www.contoso.com |x-ms-blob-content-type |Primeira regra |Sucesso |
| **GET** |http://www.contoso.com |x-ms-blob-content-type |Segunda regra |Sucesso |
| **GET** |http://www.contoso.com |x-ms-client-request-id |Segunda regra |Failure |

Olá primeira solicitação corresponde a primeira regra de hello – domínio de origem Olá corresponde Olá permitido origens, método hello corresponde Olá permitido métodos e cabeçalho Olá corresponde Olá cabeçalhos – permitido e portanto, tem êxito.

segunda solicitação de saudação não corresponde a primeira regra de saudação porque método hello não coincide com hello permitido métodos. No entanto, ele, corresponder a segunda regra de hello, para que ele tenha êxito.

Olá terceira solicitação corresponde a segunda regra Olá em seu domínio de origem e o método, portanto nenhuma regra adicional será avaliada. No entanto, Olá *cabeçalho x-ms-client-request-id* não é permitido pela segunda regra de hello, para a solicitação de saudação falhar, apesar de saudação que semântica de saudação da regra de terceiro Olá teria permitido toosucceed.

> [!NOTE]
> Embora este exemplo mostra uma regra menos restritiva antes de uma mais restritiva, em geral Olá melhor prática é regras mais restritivas do toolist Olá primeiro.
> 
> 

## <a name="understanding-how-hello-vary-header-is-set"></a>Noções básicas sobre como o cabeçalho Vary de saudação é definido
Olá *Vary* cabeçalho é um cabeçalho HTTP/1.1 padrão consiste em um conjunto de campos de cabeçalho de solicitação que recomendam o agente de navegador ou usuário Olá sobre critérios de saudação que foram selecionadas por Olá server tooprocess Olá solicitação. Olá *Vary* cabeçalho é usado principalmente para armazenar em cache por proxies, navegadores e CDNs, que o usam toodetermine como Olá resposta deve ser armazenada em cache. Para obter detalhes, consulte a especificação Olá Olá [cabeçalho Vary](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html).

Quando o navegador hello ou outro agente de usuário armazena em cache a resposta saudação de uma solicitação CORS, domínio de origem de saudação é armazenado em cache como Olá permitido de origem. Quando um segundo problemas de domínio Olá mesma solicitação para um recurso de armazenamento enquanto Olá cache está ativo, o agente do usuário Olá recupera o domínio de origem armazenada em cache hello. segundo domínio de saudação não coincide domínio armazenado em cache do hello, portanto solicitação Olá falhará quando ele teria êxito caso contrário. Em alguns casos, o armazenamento do Azure define cabeçalho Vary de saudação muito**origem** tooinstruct Olá usuário toosend Olá subsequentes CORS solicitação toohello serviço agent quando Olá solicitando domínio difere da saudação armazenado em cache de origem.

Armazenamento do Azure define Olá *Vary* cabeçalho muito**origem** para solicitações atuais de GET/HEAD nos Olá casos a seguir:

* Quando a solicitação de Olá Olá coincide com origem permitida origem definida por uma regra CORS. toobe uma correspondência exata, regra CORS Olá não pode incluir um caractere curinga ' * ' caracteres.
* Não há nenhuma origem da solicitação correspondente Olá regra, mas CORS estiver habilitado para o serviço de armazenamento de saudação.

No caso de Olá onde uma solicitação GET/HEAD corresponde a uma regra CORS que permite que todas as origens, resposta Olá indica que todas as origens são permitidas e cache de agente de usuário Olá permitirá solicitações subsequentes de qualquer domínio de origem enquanto Olá cache está ativo.

Observe que para solicitações que usam métodos diferentes de GET/HEAD, serviços de armazenamento hello serão não definir cabeçalho Vary de hello, como métodos de toothese respostas não são armazenadas em cache por agentes de usuário.

Olá, tabela a seguir indica como o Azure storage responderá a solicitações de tooGET/HEAD com base em Olá anteriormente mencionados casos:

| Solicitação | Configuração da conta e o resultado da avaliação da regra |  |  | Resposta |  |  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **Cabeçalho da origem presente na solicitação** |**Regra(s) de CORS especificada(s) para este serviço** |**Existe uma regra correspondente que permite todas as origens(*)** |**Regra de correspondência existe para correspondência exata da origem** |**A resposta inclui tooOrigin de conjunto de cabeçalho Vary** |**Resposta inclui Access-Control-Allowed-Origin: "*"** |**Resposta inclui Access-Control-Exposed-Headers** |
| Não |Não |Não |Não |Não |Não |Não |
| Não |Sim |Não |Não |Sim |Não |Não |
| Não |Sim |Sim |Não |Não |Sim |Sim |
| Sim |Não |Não |Não |Não |Não |Não |
| Sim |Sim |Não |Sim |Sim |Não |Sim |
| Sim |Sim |Não |Não |Sim |Não |Não |
| Sim |Sim |Sim |Não |Não |Sim |Sim |

## <a name="billing-for-cors-requests"></a>Cobrança para solicitações CORS
Solicitações de simulação com êxito são faturadas se você tiver habilitado CORS para qualquer um dos serviços de armazenamento Olá para sua conta (chamando [definir propriedades do serviço Blob](https://msdn.microsoft.com/library/hh452235.aspx), [definir propriedades de serviço de fila](https://msdn.microsoft.com/library/hh452232.aspx), ou [ Definir propriedades do serviço tabela](https://msdn.microsoft.com/library/hh452240.aspx)). encargos de toominimize, considere definir Olá **MaxAgeInSeconds** elemento de CORS regras de valor grande tooa para que hello agente do usuário armazena em cache a solicitação de saudação.

Solicitações de simulação malsucedidas não serão cobradas.

## <a name="next-steps"></a>Próximas etapas
[Definir propriedades do serviço Blob](https://msdn.microsoft.com/library/hh452235.aspx)

[Definir propriedades do serviço Fila](https://msdn.microsoft.com/library/hh452232.aspx)

[Definir propriedades do serviço Tabela](https://msdn.microsoft.com/library/hh452240.aspx)

[Especificação de compartilhamento de recursos entre origens W3C](http://www.w3.org/TR/cors/)

