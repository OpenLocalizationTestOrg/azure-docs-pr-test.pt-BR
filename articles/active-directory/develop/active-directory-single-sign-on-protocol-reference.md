---
title: "Logon único no protocolo de SAML de aaaAzure | Microsoft Docs"
description: "Este artigo descreve o protocolo de logon único no SAML saudação no Active Directory do Azure"
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: ad8437f5-b887-41ff-bd77-779ddafc33fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: priyamo
ms.custom: aaddev
ms.openlocfilehash: 435cfe0e7be3f2defd34e8b6f6b0f08596ee1f48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# Protocolo SAML de Logon Único
Este artigo aborda as solicitações de autenticação de saudação SAML 2.0 e respostas do Azure Active Directory (AD do Azure) oferece suporte para logon único.

diagrama de protocolo Hello abaixo descreve a sequência de logon único hello. Olá, serviço de nuvem (provedor de serviços de saudação) usa um toopass de associação de redirecionamento de HTTP um `AuthnRequest` (solicitação de autenticação) elemento tooAzure AD (provedor de identidade Olá). AD do Azure, em seguida, usa um toopost de associação HTTP post um `Response` serviço de nuvem do elemento toohello.

![Fluxo de trabalho de Logon Único](media/active-directory-single-sign-on-protocol-reference/active-directory-saml-single-sign-on-workflow.png)

## AuthnRequest
toorequest uma autenticação de usuário, serviços de nuvem enviar um `AuthnRequest` tooAzure elemento AD. Um exemplo de SAML 2.0 `AuthnRequest` poderia ter esta aparência:

```
<samlp:AuthnRequest
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="id6c1c178c166d486687be4aaf5e482730"
Version="2.0" IssueInstant="2013-03-18T03:28:54.1839884Z"
xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
<Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://www.contoso.com</Issuer>
</samlp:AuthnRequest>
```


| Parâmetro |  | Descrição |
| --- | --- | --- |
| ID |obrigatório |Saudação de toopopulate esse atributo do AD do Azure usa `InResponseTo` atributo de saudação retornada uma resposta. ID não deve começar com um número, portanto, uma estratégia comum é tooprepend uma cadeia de caracteres como "id" toohello representação de cadeia de caracteres de um GUID. Por exemplo, `id6c1c178c166d486687be4aaf5e482730` é uma ID válida. |
| Versão |obrigatório |Ele deve ser **2.0**. |
| IssueInstant |obrigatório |Isso é uma cadeia de caracteres DateTime com um valor de UTC e [formato de ida e volta ("o")](https://msdn.microsoft.com/library/az4se3k1.aspx). AD do Azure espera um valor DateTime desse tipo, mas não avaliar ou usar o valor de saudação. |
| AssertionConsumerServiceUrl |opcional |Se fornecido, isso deve corresponder Olá `RedirectUri` saudação do serviço de nuvem no Azure AD. |
| ForceAuthn |opcional | Esse é um valor booliano. Se true, isso significa que o usuário Olá será forçado toore-autenticar, mesmo se tiverem uma sessão válida com o Azure AD. |
| IsPassive |opcional |Este é um valor booleano que especifica se o AD do Azure deve autenticar Olá usuário silenciosamente, sem interação do usuário, usando o cookie de sessão Olá se houver. Se for true, AD do Azure tentará usuário de saudação tooauthenticate usando o cookie de sessão hello. |

Todos os outros atributos `AuthnRequest` , como Consent, Destination, AssertionConsumerServiceIndex, AttributeConsumerServiceIndex e ProviderName são **ignorados**.

O AD do Azure também ignora Olá `Conditions` elemento `AuthnRequest`.

### Emissor
Olá `Issuer` elemento em um `AuthnRequest` devem corresponder exatamente a um Olá **ServicePrincipalNames** no serviço de nuvem Olá no AD do Azure. Normalmente, isso é definido toohello **URI da ID do aplicativo** que é especificado durante o registro do aplicativo.

Um trecho SAML de exemplo que contém a saudação `Issuer` elemento tem esta aparência:

```
<Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://www.contoso.com</Issuer>
```

### NameIDPolicy
Esse elemento solicita um formato de ID de nome específico em resposta hello e é opcional em `AuthnRequest` tooAzure elementos enviados AD.

Um elemento de exemplo `NameIdPolicy` tem esta aparência:

```
<NameIDPolicy Format="urn:oasis:names:tc:SAML:2.0:nameid-format:persistent"/>
```

Se `NameIDPolicy` for fornecido, você poderá incluir seu atributo `Format` opcional. Olá `Format` atributo pode ter apenas um dos Olá valores a seguir; qualquer outro valor resulta em erro.

* `urn:oasis:names:tc:SAML:2.0:nameid-format:persistent`: O azure Active Directory emite Olá NameID declaração como um identificador de par.
* `urn:oasis:names:tc:SAML:1.1:nameid-format:emailAddress`: O azure Active Directory emite Olá declaração de NameID no formato de endereço de email.
* `urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified`: Este valor permite que o formato de declaração do Active Directory do Azure tooselect hello. Active Directory do Azure emite Olá NameID como um identificador de par.
* `urn:oasis:names:tc:SAML:2.0:nameid-format:transient`: O azure Active Directory emite Olá NameID declaração como um valor gerado aleatoriamente que é a operação atual de SSO toohello exclusivo. Isso significa que o valor de saudação é temporária e não pode ser usado tooidentify Olá autenticação do usuário.

O AD do Azure ignora Olá `AllowCreate` atributo.

### RequestAuthnContext
Olá `RequestedAuthnContext` elemento Especifica os métodos de autenticação de saudação desejado. É opcional em `AuthnRequest` tooAzure elementos enviados AD. O Azure AD dá suporte a apenas um valor `AuthnContextClassRef`: `urn:oasis:names:tc:SAML:2.0:ac:classes:Password`.

### Scoping
Olá `Scoping` elemento, que inclui uma lista de provedores de identidade, é opcional em `AuthnRequest` tooAzure elementos enviados AD.

Se fornecido, não inclua Olá `ProxyCount` atributo, `IDPListOption` ou `RequesterID` elemento, pois eles não têm suporte.

### Signature
Não inclua um elemento `Signature` nos elementos `AuthnRequest`, pois o Azure AD não dá suporte a solicitações de autenticação assinadas.

### Assunto
O AD do Azure ignora Olá `Subject` elemento `AuthnRequest` elementos.

## Resposta
Quando um logon solicitado for concluído com êxito, o AD do Azure posta um serviço de nuvem toohello resposta. Uma exemplo resposta tooa tentativa bem-sucedida de logon tem esta aparência:

```
<samlp:Response ID="_a4958bfd-e107-4e67-b06d-0d85ade2e76a" Version="2.0" IssueInstant="2013-03-18T07:38:15.144Z" Destination="https://contoso.com/identity/inboundsso.aspx" InResponseTo="id758d0ef385634593a77bdf7e632984b6" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion"> https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
  <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
    ...
  </ds:Signature>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success" />
  </samlp:Status>
  <Assertion ID="_bf9c623d-cc20-407a-9a59-c2d0aee84d12" IssueInstant="2013-03-18T07:38:15.144Z" Version="2.0" xmlns="urn:oasis:names:tc:SAML:2.0:assertion">
    <Issuer>https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
    <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      ...
    </ds:Signature>
    <Subject>
      <NameID>Uz2Pqz1X7pxe4XLWxV9KJQ+n59d573SepSAkuYKSde8=</NameID>
      <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
        <SubjectConfirmationData InResponseTo="id758d0ef385634593a77bdf7e632984b6" NotOnOrAfter="2013-03-18T07:43:15.144Z" Recipient="https://contoso.com/identity/inboundsso.aspx" />
      </SubjectConfirmation>
    </Subject>
    <Conditions NotBefore="2013-03-18T07:38:15.128Z" NotOnOrAfter="2013-03-18T08:48:15.128Z">
      <AudienceRestriction>
        <Audience>https://www.contoso.com</Audience>
      </AudienceRestriction>
    </Conditions>
    <AttributeStatement>
      <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name">
        <AttributeValue>testuser@contoso.com</AttributeValue>
      </Attribute>
      <Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">
        <AttributeValue>3F2504E0-4F89-11D3-9A0C-0305E82C3301</AttributeValue>
      </Attribute>
      ...
    </AttributeStatement>
    <AuthnStatement AuthnInstant="2013-03-18T07:33:56.000Z" SessionIndex="_bf9c623d-cc20-407a-9a59-c2d0aee84d12">
      <AuthnContext>
        <AuthnContextClassRef> urn:oasis:names:tc:SAML:2.0:ac:classes:Password</AuthnContextClassRef>
      </AuthnContext>
    </AuthnStatement>
  </Assertion>
</samlp:Response>
```

### Resposta
Olá `Response` elemento inclui o resultado de saudação da solicitação de autorização de saudação. O AD do Azure define Olá `ID`, `Version` e `IssueInstant` valores hello `Response` elemento. Ele também define Olá seguintes atributos:

* `Destination`: Quando o logon for concluído com êxito, isso é definido toohello `RedirectUri` saudação do provedor de serviço (serviço de nuvem).
* `InResponseTo`: Isso é definido toohello `ID` atributo de saudação `AuthnRequest` elemento que iniciou a resposta de saudação.

### Emissor
O AD do Azure define Olá `Issuer` elemento muito`https://login.microsoftonline.com/<TenantIDGUID>/` onde <TenantIDGUID> é ID de locatário de saudação do locatário de saudação do AD do Azure.

Por exemplo, uma resposta de exemplo com o elemento Issuer poderia ser assim:

```
<Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion"> https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
```

### Status
Olá `Status` elemento transmite o êxito de saudação ou falha de logon. Ele inclui Olá `StatusCode` elemento, que contém um código ou um conjunto de códigos aninhados que representam Olá status da solicitação de saudação. Ele também inclui Olá `StatusMessage` elemento, que contém mensagens de erro personalizadas que são geradas durante o processo de logon do hello.

<!-- TODO: Add a authentication protocol error reference -->

a seguir Olá é uma SAML resposta tooan logon tentativa malsucedida.

```
<samlp:Response ID="_f0961a83-d071-4be5-a18c-9ae7b22987a4" Version="2.0" IssueInstant="2013-03-18T08:49:24.405Z" InResponseTo="iddce91f96e56747b5ace6d2e2aa9d4f8c" xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol">
  <Issuer xmlns="urn:oasis:names:tc:SAML:2.0:assertion">https://sts.windows.net/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Requester">
      <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:RequestUnsupported" />
    </samlp:StatusCode>
    <samlp:StatusMessage>AADSTS75006: An error occurred while processing a SAML2 Authentication request. AADSTS90011: hello SAML authentication request property 'NameIdentifierPolicy/SPNameQualifier' is not supported.
Trace ID: 66febed4-e737-49ff-ac23-464ba090d57c
Timestamp: 2013-03-18 08:49:24Z</samlp:StatusMessage>
  </samlp:Status>
```

### Asserção
Em adição toohello `ID`, `IssueInstant` e `Version`, o AD do Azure define Olá Olá elementos a seguir `Assertion` elemento da resposta de saudação.

#### Emissor
Isso é definido muito`https://sts.windows.net/<TenantIDGUID>/`onde <TenantIDGUID> é hello ID do locatário do locatário de saudação do AD do Azure.

```
<Issuer>https://login.microsoftonline.com/82869000-6ad1-48f0-8171-272ed18796e9/</Issuer>
```

#### Signature
AD do Azure assina a asserção Olá no logon bem-sucedido de tooa resposta. Olá `Signature` elemento contém uma assinatura digital que o serviço de nuvem Olá pode usar tooauthenticate Olá fonte tooverify Olá a integridade de asserção de saudação.

toogenerate essa assinatura digital, o AD do Azure usa Olá Olá da chave de assinatura `IDPSSODescriptor` elemento do documento de metadados.

```
<ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
      digital_signature_here
    </ds:Signature>
```

#### Assunto
Isso especifica a entidade de saudação que é Olá assunto das instruções de saudação em asserção hello. Ele contém um `NameID` elemento, que representa o usuário autenticado hello. Olá `NameID` valor é um identificador de destino que é o provedor de serviços de toohello somente direcionado é público-alvo Olá token hello. É persistente - pode ser revogado, mas nunca é reatribuído. Ele também é opaco, que não revela nada sobre o usuário hello e não pode ser usado como um identificador para consultas de atributo.

Olá `Method` atributo de saudação `SubjectConfirmation` é sempre definido muito`urn:oasis:names:tc:SAML:2.0:cm:bearer`.

```
<Subject>
      <NameID>Uz2Pqz1X7pxe4XLWxV9KJQ+n59d573SepSAkuYKSde8=</NameID>
      <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
        <SubjectConfirmationData InResponseTo="id758d0ef385634593a77bdf7e632984b6" NotOnOrAfter="2013-03-18T07:43:15.144Z" Recipient="https://contoso.com/identity/inboundsso.aspx" />
      </SubjectConfirmation>
</Subject>
```

#### Condições
Este elemento Especifica o usam de condições que definem Olá aceitável de asserções SAML.

```
<Conditions NotBefore="2013-03-18T07:38:15.128Z" NotOnOrAfter="2013-03-18T08:48:15.128Z">
      <AudienceRestriction>
        <Audience>https://www.contoso.com</Audience>
      </AudienceRestriction>
</Conditions>
```

Olá `NotBefore` e `NotOnOrAfter` atributos especificam o intervalo de saudação durante o qual Olá asserção é válida.

* Olá valor Olá `NotBefore` atributo é igual tooor ligeiramente (menos de um segundo) mais tarde do que o valor de saudação do `IssueInstant` atributo de saudação `Assertion` elemento. O AD do Azure não conta para qualquer diferença de tempo entre ele mesmo e hello (provedor de serviço) do serviço de nuvem e não adicionar o buffer toothis tempo.
* Olá valor Olá `NotOnOrAfter` atributo é 70 minutos mais tarde do que valor Olá Olá `NotBefore` atributo.

#### Público-alvo
Ele contém um URI que identifica um público-alvo. AD do Azure define o valor de saudação do valor de toohello elemento de `Issuer` elemento de saudação `AuthnRequest` que iniciou Olá logon. Olá tooevaluate `Audience` valor, use o valor Olá Olá `App ID URI` que foi especificada durante o registro do aplicativo.

```
<AudienceRestriction>
        <Audience>https://www.contoso.com</Audience>
</AudienceRestriction>
```

Como Olá `Issuer` valor, hello `Audience` valor deve corresponder exatamente a um de saudação nomes principais de serviço que representa o serviço de nuvem Olá no AD do Azure. No entanto, se hello valor de saudação `Issuer` elemento não é um valor de URI, hello `Audience` valor na resposta de saudação é hello `Issuer` valor prefixado com `spn:`.

#### AttributeStatement
Ele contém declarações sobre Olá assunto ou o usuário. Olá, trecho a seguir contém um exemplo `AttributeStatement` elemento. reticências Olá indicam que esse elemento Olá pode incluir vários atributos e valores de atributo.

```
<AttributeStatement>
      <Attribute Name="http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name">
        <AttributeValue>testuser@contoso.com</AttributeValue>
      </Attribute>
      <Attribute Name="http://schemas.microsoft.com/identity/claims/objectidentifier">
        <AttributeValue>3F2504E0-4F89-11D3-9A0C-0305E82C3301</AttributeValue>
      </Attribute>
      ...
</AttributeStatement>
```        

* **Nome de declaração** : Olá valor Olá `Name` atributo (`http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`) é Olá UPN do usuário Olá autenticado, como `testuser@managedtenant.com`.
* **Declaração de ObjectIdentifier** : Olá valor Olá `ObjectIdentifier` atributo (`http://schemas.microsoft.com/identity/claims/objectidentifier`) é hello `ObjectId` saudação do objeto de diretório representando Olá autenticou o usuário no AD do Azure. `ObjectId`é um imutável, globalmente exclusivo e reutilizar o identificador seguro do hello autenticou o usuário.

#### AuthnStatement
Esse elemento declara que assunto Olá asserção foi autenticado por um meio específico em um determinado momento.

* Olá `AuthnInstant` atributo especifica o tempo de saudação nos quais o usuário Olá autenticado com o Azure AD.
* Olá `AuthnContext` elemento Especifica o contexto de autenticação Olá usado tooauthenticate usuário de saudação.

```
<AuthnStatement AuthnInstant="2013-03-18T07:33:56.000Z" SessionIndex="_bf9c623d-cc20-407a-9a59-c2d0aee84d12">
      <AuthnContext>
        <AuthnContextClassRef> urn:oasis:names:tc:SAML:2.0:ac:classes:Password</AuthnContextClassRef>
      </AuthnContext>
</AuthnStatement>
```