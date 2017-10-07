---
title: 'Azure Active Directory B2C: solicitando tokens de acesso | Microsoft Docs'
description: Este artigo mostra como toosetup um aplicativo cliente e adquirir um token de acesso.
services: active-directory-b2c
documentationcenter: android
author: parakhj
manager: krassk
editor: 
ms.assetid: 1c75f17f-5ec5-493a-b906-f543b3b1ea66
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: parakhj
ms.openlocfilehash: 410639424fd4e5119a5d58751dfdb6e8957fd100
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-requesting-access-tokens"></a>Azure AD B2C: Solicitando tokens de acesso

Um token de acesso (denotado como **acesso\_token** nas respostas de saudação do Azure AD B2C) é uma forma de token de segurança que um cliente pode usar tooaccess recursos que é protegido por um [servidor de autorização](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-protocols#the-basics), como uma API da web. Tokens de acesso são representados como [JWTs](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-tokens#types-of-tokens) e contêm informações sobre servidor de saudação do recurso pretendido e o servidor de toohello de permissões concedidas hello. Ao chamar o servidor de saudação do recurso, token de acesso de saudação deve estar presente na solicitação HTTP hello.

Este artigo aborda como tooconfigure um aplicativo cliente e a API da web no pedido tooobtain um **acesso\_token**.

> [!NOTE]
> **Não há suporte a cadeias de API Web (em nome de) no Azure AD B2C.**
>
> Muitas arquiteturas incluem uma web API que precisa toocall outra API da web downstream, ambos protegido pelo Azure AD B2C. Este cenário é comum em clientes nativos que têm um API da web back-end, que por sua vez, chama um serviço online da Microsoft, como hello Azure AD Graph API.
>
> Neste cenário de API da web encadeadas pode ser suportado usando Olá grant de credencial de portador do OAuth 2.0 JWT, caso contrário, conhecido como fluxo de saudação em nome de. No entanto, a saudação em nome de fluxo não está implementada atualmente no Azure AD B2C.

## <a name="register-a-web-api-and-publish-permissions"></a>Registrar uma API Web e permissões de publicação

Antes de solicitar um token de acesso, você primeiro precisa tooregister uma API da web e publique permissões (escopos) que podem ser concedidas toohello aplicativo de cliente.

### <a name="register-a-web-api"></a>Registrar uma API Web

1. Na folha de recursos Olá B2C em Olá portal do Azure, clique em **aplicativos**.
1. Clique em **+ adicionar** na parte superior de saudação da folha de saudação.
1. Insira um **nome** para o aplicativo hello que descreve seu aplicativo tooconsumers. Por exemplo, você poderia digitar "API Contoso".
1. Saudação de alternância **incluem o aplicativo web / da web API** alternar muito**Sim**.
1. Insira um valor arbitrário para Olá **URLs de resposta**. Por exemplo, insira: `https://localhost:44316/`. valor de saudação não importa como uma API não deve receber o token de saudação diretamente no Azure AD B2C.
1. Insira um **URI da ID do aplicativo**. Este é o identificador de saudação usada para sua API da web. Por exemplo, digite 'Notas' na caixa de saudação. Olá **URI da ID do aplicativo** seriam `https://{tenantName}.onmicrosoft.com/notes`.
1. Clique em **criar** tooregister seu aplicativo.
1. Clique em aplicativo hello que você acabou de criar e copiar Olá globalmente exclusivo **ID do aplicativo cliente** que você usará posteriormente no seu código.

### <a name="publishing-permissions"></a>Permissões de publicação

Escopos, que são análogos toopermissions, são necessários quando seu aplicativo é chamar uma API. Alguns exemplos de escopos são "leitura" ou "gravação". Suponha que você deseja que seu web ou aplicativo nativo muito "leitura" de uma API. Seu aplicativo poderia chamar B2C do Azure AD e solicitação de token de acesso que oferece acesso toohello escopo "leitura". Para o Azure AD B2C tooemit tal um token de acesso, Olá aplicativo precisa toobe concedeu permissão muito "leitura" da API específica hello. toodo isso, sua API precisa primeiro toopublish hello "leitura" escopo.

1. Dentro de saudação do Azure AD B2C **aplicativos** folha, abra Olá web aplicativo de API ("API do Contoso").
1. Clique em **Escopos publicados**. Isso é onde você define permissões de saudação (escopos) que podem ser concedidas tooother aplicativos.
1. Adicionar **Valores do escopo** conforme necessário (por exemplo, "leitura"). Por padrão, o escopo de "user_impersonation" hello será definido. Você pode ignorar isso se desejar. Digite uma descrição do escopo de saudação em Olá **nome do escopo** coluna.
1. Clique em **Salvar**.

> [!IMPORTANT]
> Olá **nome do escopo** é descrição Olá Olá **o valor do escopo**. Ao usar escopo hello, verifique se Olá de toouse **o valor do escopo**.

## <a name="grant-a-native-or-web-app-permissions-tooa-web-api"></a>Conceder um nativo ou web API da web do aplicativo permissões tooa

Após uma API escopos toopublish configurado, o aplicativo de cliente de saudação precisa toobe concedida esses escopos via Olá portal do Azure.

1. Navegue toohello **aplicativos** menu na folha de recursos Olá B2C.
1. Registre um aplicativo cliente ([aplicativo Web](active-directory-b2c-app-registration.md#register-a-web-app) ou [cliente nativo](active-directory-b2c-app-registration.md#register-a-mobile-or-native-app)) se você ainda não tem um. Se você estiver seguindo este guia como ponto de partida, você precisará tooregister um aplicativo cliente.
1. Clique em **Acesso à API**.
1. Clique em **Adicionar**.
1. Selecione web API e hello escopos você gostaria que toogrant (permissões).
1. Clique em **OK**.

> [!NOTE]
> O Azure AD B2C não solicitará o consentimento dos usuários do aplicativo cliente. Em vez disso, todo o consentimento é fornecido pelo administrador hello, com base nas permissões de saudação configuradas entre aplicativos Olá descritos acima. Se uma concessão de permissão de um aplicativo for revogada, todos os usuários que foram anteriormente capaz tooacquire essa permissão não poderá mais ser capaz de toodo assim.

## <a name="requesting-a-token"></a>Solicitar um token

Ao solicitar um token de acesso, aplicativo de cliente hello precisa de permissões de saudação desejada de toospecify no hello **escopo** parâmetro de solicitação de saudação. Por exemplo, toospecify Olá **o valor do escopo** "leitura" hello API com hello **URI da ID do aplicativo** de `https://contoso.onmicrosoft.com/notes`, escopo Olá seria `https://contoso.onmicrosoft.com/notes/read`. Abaixo está um exemplo de um toohello de solicitação de código de autorização `/authorize` ponto de extremidade.

> [!NOTE]
> Atualmente, não há suporte para os domínios personalizados junto com os tokens de acesso. Você deve usar seu domínio tenantName.onmicrosoft.com na URL de solicitação de saudação.

```
https://login.microsoftonline.com/<tenantName>.onmicrosoft.com/oauth2/v2.0/authorize?p=<yourPolicyId>&client_id=<appID_of_your_client_application>&nonce=anyRandomValue&redirect_uri=<redirect_uri_of_your_client_application>&scope=https%3A%2F%2Fcontoso.onmicrosoft.com%2Fnotes%2Fread&response_type=code 
```

tooacquire várias permissões em Olá mesmo solicitar, você pode adicionar várias entradas de saudação único **escopo** parâmetro, separado por espaços. Por exemplo:

Decodificado em URL:

```
scope=https://contoso.onmicrosoft.com/notes/read openid offline_access
```

Codificado em URL:

```
scope=https%3A%2F%2Fcontoso.onmicrosoft.com%2Fnotes%2Fread%20openid%20offline_access
```

Você pode solicitar mais escopos (permissões) para um recurso do que aquelas concedidas para o seu aplicativo cliente. Quando esse for o caso de Olá, chamada de saudação será bem-sucedida se pelo menos uma permissão é concedida. Olá resultante **acesso\_token** terá sua declaração "scp" preenchida com somente permissões de saudação que foram concedidas com êxito.

> [!NOTE] 
> Não há suporte para solicitar permissões com base nos dois recursos de web diferente em Olá mesma solicitação. Esse tipo de solicitação falhará.

### <a name="special-cases"></a>Casos especiais

Olá OpenID Connect padrão especifica vários valores especiais "scope". Olá escopos especial representam Olá permissão a seguir muito "acessar o perfil do usuário hello":

* **openid**: isso solicita um token de ID
* **acesso\_offline**: Isso solicita um token de atualização (usando fluxos de [Código de Autenticação](active-directory-b2c-reference-oauth-code.md)).

Se hello `response_type` parâmetro em uma `/authorize` solicitação inclui `token`, Olá `scope` parâmetro deve incluir o escopo de pelo menos um recurso (diferente de `openid` e `offline_access`) que será concedido. Caso contrário, Olá `/authorize` solicitação terminará com falha.

## <a name="hello-returned-token"></a>Olá retornada um token

Em com êxito sem um uso **acesso\_token** (de qualquer Olá `/authorize` ou `/token` ponto de extremidade), seguir Olá declarações estarão presentes:

| Nome | Declaração | Descrição |
| --- | --- | --- |
|Público-alvo |`aud` |Olá **ID do aplicativo** de recurso único Olá esse token Olá concede acesso ao. |
|Escopo |`scp` |permissões de saudação concedidas toohello recursos. Várias permissões concedidas serão separadas por espaço. |
|Entidade Autorizada |`azp` |Olá **ID do aplicativo** de aplicativo cliente Olá que iniciou a solicitação de saudação. |

Quando sua API recebe Olá **acesso\_token**, ele deverá [validar token Olá](active-directory-b2c-reference-tokens.md) tooprove Olá token é autêntico e tem declarações de saudação correto.

Estamos sempre abrir toofeedback e sugestões! Se você tiver dificuldade com este tópico, poste no estouro de pilha usando Olá marca ['b2c de ad do azure'](https://stackoverflow.com/questions/tagged/azure-ad-b2c). Para solicitações de recurso, adicioná-los muito[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).

## <a name="next-steps"></a>Próximas etapas

* Criar uma API Web usando [.NET Core](https://github.com/Azure-Samples/active-directory-b2c-dotnetcore-webapi)
* Criar uma API Web usando [Node.JS](https://github.com/Azure-Samples/active-directory-b2c-javascript-nodejs-webapi)
