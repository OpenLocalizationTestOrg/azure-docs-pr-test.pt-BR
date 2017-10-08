---
title: "aaaHow toodelegate assinatura de produto e o registro do usuário"
description: "Saiba como tooa de assinatura toodelegate usuário registro e o produto de terceiros no gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: antonba
manager: erikre
editor: 
ms.assetid: 8b7ad5ee-a873-4966-a400-7e508bbbe158
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 406648db2d2f37c4dcda466294726d331cc0551b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodelegate-user-registration-and-product-subscription"></a>Como toodelegate assinatura de produto e o registro do usuário
A delegação permite que você toouse seu site da Web existente para lidar com tooproducts de entrada-em/entrada o e assinatura de desenvolvedor como oposição toousing Olá funcionalidade no portal do desenvolvedor hello. Isso permite que seus dados de usuário do site tooown hello e executar a validação de saudação dessas etapas de forma personalizada.

## <a name="delegate-signin-up"> </a>Delegando a entrada e inscrição de desenvolvedores
toodelegate desenvolvedor tooyour entrar e inscreva-se site existente que será necessário toocreate um ponto de extremidade de delegação especial em seu site que atua como Olá ponto de entrada para qualquer tal solicitação iniciada do portal do desenvolvedor de gerenciamento de API de saudação.

fluxo de trabalho final Olá será da seguinte maneira:

1. Desenvolvedor clica no link de saudação entrar ou se inscreva no portal do desenvolvedor de gerenciamento de API de saudação
2. Navegador é redirecionado toohello ponto de extremidade de delegação
3. Ponto de extremidade de delegação de retorno redireciona tooor apresenta interface de usuário solicitando usuário toosign ou de inscrição
4. Em caso de sucesso, usuário Olá é redirecionado toohello back API developer portal página Gerenciamento de que eles começaram a partir

toobegin, vamos primeiro tooroute de gerenciamento de API de configuração solicitações por meio de seu ponto de extremidade de delegação. No portal do publicador de gerenciamento de API de saudação, clique em **segurança** e, em seguida, clique em Olá **delegação** guia. Clique em tooenable caixa de seleção de saudação 'Delegado entrar & inscrição'.

![Página de delegação][api-management-delegation-signin-up]

* Decidir quais Olá URL de seu ponto de extremidade de delegação especial será e insira Olá **URL de ponto de extremidade de delegação** campo. 
* Dentro de saudação **chave de autenticação de delegação** campo Digite um segredo que será usado toocompute tooyou uma assinatura fornecida para verificação tooensure que Olá solicitação realmente vem de gerenciamento de API do Azure. Você pode clicar em Olá **gerar** toohave botão gerenciamento de API gerar aleatoriamente uma chave para você.

Agora você precisa Olá toocreate **ponto de extremidade de delegação**. Ele tem tooperform uma série de ações:

1. Receba uma solicitação em Olá formulário a seguir:
   
   > *http://www.yourwebsite.com/apimdelegation?operation=SignIn&returnUrl={URL da página de origem}&salt={string}&sig={string}*
   > 
   > 
   
    Parâmetros de consulta para o caso de entrada / inscrição hello:
   
   * **operation**: identifica o tipo de solicitação de delegação – neste caso, pode ser somente **SignIn**
   * **returnUrl**: Olá URL da página de saudação em que o usuário Olá clicou em um link entre ou inscreva-se
   * **salt**: uma cadeia de caracteres de salt especial usada para calcular um hash de segurança
   * **SIG**: hash calculado de uma toobe de hash computado de segurança usado para comparação tooyour próprio
2. Verifique se que essa solicitação de saudação é proveniente de gerenciamento de API do Azure (opcional, mas altamente recomendado para segurança)
   
   * Computar um hash HMAC-SHA512 de uma cadeia de caracteres com base em Olá **returnUrl** e **salt** parâmetros de consulta ([código de exemplo fornecido abaixo]):
     
     > HMAC(**salt**+ '\n' +**returnUrl**)
     > 
     > 
   * Comparar toohello valor hash calculado acima Olá Olá **sig** parâmetro de consulta. Se dois hashes de saudação corresponderem, move na toohello próxima etapa, caso contrário, negar a solicitação de saudação.
3. Verifique se que você está recebendo uma solicitação de entrada-no/sign-up: Olá **operação** parâmetro de consulta será definido muito "**SignIn**".
4. Apresentar Olá usuário da interface do usuário toosign ou de inscrição
5. Se o usuário Olá é registrar-se você tiver toocreate uma conta correspondente para eles no gerenciamento de API. [Criar um usuário] com hello API de REST de gerenciamento de API. Ao fazer isso, certifique-se de que você defina Olá toohello de ID de usuário, mesmo se que ele está em seu repositório do usuário ou ID tooan que você pode manter controle das.
6. Quando o usuário Olá for autenticado com êxito:
   
   * [solicitar um token single-sign-on (SSO)] via Olá API de REST de gerenciamento de API
   * Acrescente uma toohello de parâmetro de consulta returnUrl URL SSO você recebeu de chamada de API de saudação acima:
     
     > por exemplo: https://customer.portal.azure-api.net/signin-sso?token&returnUrl=/return/url 
     > 
     > 
   * Olá usuário toohello acima produzido URL de redirecionamento

Em adição toohello **SignIn** operação, você também pode executar o gerenciamento de conta, seguindo as etapas anteriores hello e usando uma das seguintes operações de saudação.

* **ChangePassword**
* **ChangeProfile**
* **CloseAccount**

Você deve passar Olá parâmetros de consulta para operações de gerenciamento de conta a seguir.

* **operation**: identifica o tipo de solicitação de delegação (ChangePassword, ChangeProfile ou CloseAccount)
* **userId**: id de usuário de saudação do hello conta toomanage
* **salt**: uma cadeia de caracteres de salt especial usada para calcular um hash de segurança
* **SIG**: hash calculado de uma toobe de hash computado de segurança usado para comparação tooyour próprio

## <a name="delegate-product-subscription"> </a>Delegando a assinatura de produtos
Delegando a assinatura de produto funciona da mesma forma toodelegating usuário entrar/backup. fluxo de trabalho final Olá seria a seguinte:

1. Desenvolvedor seleciona um produto no portal do desenvolvedor de gerenciamento de API hello e clica no botão de inscrição Olá
2. Navegador é redirecionado toohello ponto de extremidade de delegação
3. Ponto de extremidade de delegação executa etapas de assinatura de produto necessária - este é o tooyou e pode envolver o redirecionamento tooanother toorequest de página informações de cobrança, fazer perguntas adicionais, ou simplesmente armazenando informações de saudação e não exigem nenhuma ação do usuário

tooenable Olá funcionalidade, Olá **delegação** página clique **delegar assinatura produto**.

Em seguida, certifique-se de ponto de extremidade de delegação Olá executa Olá ações a seguir:

1. Receba uma solicitação em Olá formulário a seguir:
   
   > *http://www.yourwebsite.com/apimdelegation?Operation= {operação} & productId = {toosubscribe de produto para} & userId = {usuário fazer solicitação} & salt = {string} & sig = {string}*
   > 
   > 
   
    Parâmetros de consulta para o caso de assinatura de produto hello:
   
   * **operation**: identifica o tipo de solicitação de delegação. Para a assinatura de produto solicitações Olá as opções válidas são:
     * "Assinar": fornecidos de uma solicitação toosubscribe Olá usuário tooa, considerando o produto com ID (veja abaixo)
     * "Unsubscribe": toounsubscribe uma solicitação de um produto de um usuário
     * "Renovar": uma solicitação toorenew uma assinatura (por exemplo, que pode expirar)
   * **productId**: ID de saudação do usuário Olá Olá solicitado toosubscribe para
   * **userId**: Olá ID do usuário Olá para o qual é feita a solicitação de saudação
   * **salt**: uma cadeia de caracteres de salt especial usada para calcular um hash de segurança
   * **SIG**: hash calculado de uma toobe de hash computado de segurança usado para comparação tooyour próprio
2. Verifique se que essa solicitação de saudação é proveniente de gerenciamento de API do Azure (opcional, mas altamente recomendado para segurança)
   
   * Calcular um HMAC-SHA512 de uma cadeia de caracteres com base em Olá **productId**, **userId** e **salt** parâmetros de consulta:
     
     > HMAC(**salt**+ '\n' +**productId**+ '\n' +**userId**)
     > 
     > 
   * Comparar toohello valor hash calculado acima Olá Olá **sig** parâmetro de consulta. Se dois hashes de saudação corresponderem, move na toohello próxima etapa, caso contrário, negar a solicitação de saudação.
3. Executar qualquer processamento de assinatura de produto com base no tipo de saudação da operação solicitada no **operação** -por exemplo, cobrança, mais perguntas, etc.
4. Sobre a inscrição com êxito o produto de toohello Olá usuário ao seu lado, inscrever-se o produto de gerenciamento de API do hello usuário toohello por [chamada hello API REST para assinatura de produto].

## <a name="delegate-example-code"> </a> Código de exemplo
Eles mostram exemplos de código como Olá tootake *chave de validação de delegação*, que é definido na tela de delegação de saudação do portal do publicador hello, toocreate um HMAC que é então usado assinatura de saudação toovalidate, provando validade de saudação do hello returnUrl passado. Olá mesmo código funciona para productId hello e userId com pequenas modificações.

**C# hash de toogenerate código de returnUrl**

```c#
using System.Security.Cryptography;

string key = "delegation validation key";
string returnUrl = "returnUrl query parameter";
string salt = "salt query parameter";
string signature;
using (var encoder = new HMACSHA512(Convert.FromBase64String(key)))
{
    signature = Convert.ToBase64String(encoder.ComputeHash(Encoding.UTF8.GetBytes(salt + "\n" + returnUrl)));
    // change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
    // compare signature toosig query parameter
}
```

**Hash de toogenerate NodeJS código de returnUrl**

```
var crypto = require('crypto');

var key = 'delegation validation key'; 
var returnUrl = 'returnUrl query parameter';
var salt = 'salt query parameter';

var hmac = crypto.createHmac('sha512', new Buffer(key, 'base64'));
var digest = hmac.update(salt + '\n' + returnUrl).digest();
// change too(salt + "\n" + productId + "\n" + userId) when delegating product subscription
// compare signature toosig query parameter

var signature = digest.toString('base64');
```

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre a delegação, consulte Olá vídeo a seguir.

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Delegating-User-Authentication-and-Product-Subscription-to-a-3rd-Party-Site/player]
> 
> 

[Delegating developer sign-in and sign-up]: #delegate-signin-up
[Delegating product subscription]: #delegate-product-subscription
[solicitar um token single-sign-on (SSO)]: http://go.microsoft.com/fwlink/?LinkId=507409
[Crie um usuário]: http://go.microsoft.com/fwlink/?LinkId=507655#CreateUser
[chamada hello API REST para assinatura de produto]: http://go.microsoft.com/fwlink/?LinkId=507655#SSO
[Next steps]: #next-steps
[código de exemplo fornecido abaixo]: #delegate-example-code

[api-management-delegation-signin-up]: ./media/api-management-howto-setup-delegation/api-management-delegation-signin-up.png 
