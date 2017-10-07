---
title: "Azure Active Directory B2C: políticas internas | Microsoft Docs"
description: "Um tópico em estrutura da política extensível saudação do Azure Active Directory B2C e como toocreate vários tipos de política"
services: active-directory-b2c
documentationcenter: 
author: sama
manager: mbaldwin
editor: PatAltimore
ms.assetid: 0d453e72-7f70-4aa2-953d-938d2814d5a9
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: sama
ms.openlocfilehash: 24bb85eba30f888c6ea7d0401e05235e8eb6ea79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-built-in-policies"></a>Azure Active Directory B2C: políticas internas


estrutura da política extensível saudação do B2C do Azure Active Directory (AD do Azure) é a intensidade de núcleo saudação do serviço de saudação. As políticas descrevem totalmente as experiências de identidade do consumidor, como inscrição, entrada ou edição de perfil. Por exemplo, uma política de inscrição permite que você toocontrol comportamentos Configurando Olá configurações a seguir:

* Tipos (contas sociais, como Facebook) ou local, como endereços de email que os consumidores podem utilizar toosign para o aplicativo hello de conta
* Atributos (por exemplo, nome, código postal e tamanho de sapato) toobe coletados de consumidor Olá durante a inscrição
* Uso da Autenticação Multifator do Microsoft Azure
* Olá aparência de todas as páginas de inscrição
* Informações (que se manifesta como declarações em um token) Olá aplicativo recebe quando termina de execução da diretiva Olá

Você pode criar várias políticas de tipos diferentes em seu locatário e usá-las em seus aplicativos, conforme necessário. As políticas podem ser reutilizadas entre os aplicativos. Essa flexibilidade permite que os desenvolvedores toodefine e modificar as experiências de identidade do consumidor com pouca ou nenhuma tootheir altera o código.

As políticas estão disponíveis para uso por meio de uma interface simples do desenvolvedor. O aplicativo dispara uma política usando uma solicitação de autenticação HTTP padrão (passando um parâmetro de política na solicitação de saudação) e recebe um token personalizado como resposta. Por exemplo, Olá única diferença entre solicitações invocar uma política de inscrição e as que invocam uma política de entrada é usada no parâmetro de cadeia de caracteres de consulta hello "p" nome da política hello:

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siup                                       // Your sign-up policy

```

```

https://login.microsoftonline.com/contosob2c.onmicrosoft.com/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e      // Your registered Application ID
&redirect_uri=https%3A%2F%2Flocalhost%3A44321%2F    // Your registered Reply URL, url encoded
&response_mode=form_post                            // 'query', 'form_post' or 'fragment'
&response_type=id_token
&scope=openid
&nonce=dummy
&state=12345                                        // Any value provided by your application
&p=b2c_1_siin                                       // Your sign-in policy

```

Para obter mais informações sobre a estrutura da política hello, consulte [esta postagem de blog sobre o Blog de segurança e o Azure AD B2C em Olá Enterprise Mobility](http://blogs.technet.com/b/ad/archive/2015/11/02/a-look-inside-azuread-b2c-with-kim-cameron.aspx).

## <a name="create-a-sign-up-or-sign-in-policy"></a>Criar uma política de inscrição ou credenciais

Esta política controla as duas experiências de inscrição e credenciais do consumidor com uma única configuração. Os consumidores são led Olá direita caminho (inscrever ou entrar) dependendo do contexto de saudação. Ele também descreve o conteúdo de saudação de tokens que o aplicativo hello receberá inscrições bem-sucedida ou entradas.  É um exemplo de código para política de inscrever-se ou entrar Olá [disponível aqui](active-directory-b2c-devquickstarts-web-dotnet-susi.md).  É recomendável que você use esta política em vez de uma política de inscrição e entrada.  

[!INCLUDE [active-directory-b2c-create-sign-in-sign-up-policy](../../includes/active-directory-b2c-create-sign-in-sign-up-policy.md)]

## <a name="create-a-sign-up-policy"></a>Criar uma política de inscrição

[!INCLUDE [active-directory-b2c-create-sign-up-policy](../../includes/active-directory-b2c-create-sign-up-policy.md)]

## <a name="create-a-sign-in-policy"></a>Usar uma política de entrada

[!INCLUDE [active-directory-b2c-create-sign-in-policy](../../includes/active-directory-b2c-create-sign-in-policy.md)]

## <a name="create-a-profile-editing-policy"></a>Criar uma política de edição de perfil

[!INCLUDE [active-directory-b2c-create-profile-editing-policy](../../includes/active-directory-b2c-create-profile-editing-policy.md)]

## <a name="create-a-password-reset-policy"></a>Criar uma política de redefinição de senha

[!INCLUDE [active-directory-b2c-create-password-reset-policy](../../includes/active-directory-b2c-create-password-reset-policy.md)]

## <a name="frequently-asked-questions"></a>Perguntas frequentes

### <a name="how-do-i-link-a-sign-up-or-sign-in-policy-with-a-password-reset-policy"></a>Como fazer para vincular uma política de inscrição ou entrada a uma política de redefinição de senha?
Quando você cria uma política de inscrever-se ou entrar (com contas locais), você verá um **senha Esqueceu?** link na primeira página Olá da experiência de saudação. Clicar nesse link não dispara automaticamente uma política de redefinição de senha. 

Olá em vez disso, o código de erro  **`AADB2C90118`**  é retornado tooyour aplicativo. Seu aplicativo precisa toohandle esse código de erro com a invocação de uma política de redefinição de senha específica. Para obter mais informações, consulte um [exemplo que demonstra a abordagem de saudação de vinculação políticas](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-DotNet-SUSI).

### <a name="should-i-use-a-sign-up-or-sign-in-policy-or-a-sign-up-policy-and-a-sign-in-policy"></a>Eu devo usar uma política de inscrição ou entrada ou uma política de inscrição e uma política de entrada?
Recomendamos que você use uma política de inscrição ou entrada em vez de usar uma política de inscrição e uma política de entrada.  

política de inscrever-se ou entrar Olá tem mais recursos do que a política de entrada hello. Também permite a personalização da interface do usuário toouse página e tem um melhor suporte para localização. 

Olá entrar diretiva é recomendada se você não precisa toolocalize suas políticas, só precisa de recursos de personalização secundárias para a identidade visual e deseja senha redefinição embutida.

## <a name="next-steps"></a>Próximas etapas
* [Configuração de token, de sessão e de logon único](active-directory-b2c-token-session-sso.md)
* [Desabilitar a verificação de email durante a inscrição do consumidor](active-directory-b2c-reference-disable-ev.md)

