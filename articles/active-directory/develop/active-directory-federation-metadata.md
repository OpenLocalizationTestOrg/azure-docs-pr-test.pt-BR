---
title: "aaaAzure AD metadados de Federação | Microsoft Docs"
description: "Este artigo descreve o documento de metadados de Federação Olá que publica do Active Directory do Azure para serviços que aceitam tokens do Active Directory do Azure."
services: active-directory
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: c2d5f80b-aa74-452c-955b-d8eb3ed62652
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 23535bcd5eeb3e9b2e17d89a9b0420fc98bd3895
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="federation-metadata"></a>Metadados de federação
Azure Active Directory (AD do Azure) publica um documento de metadados de federação para serviços que é configurado tooaccept tokens de segurança de saudação que emitem o AD do Azure. Olá formato de documento de metadados de Federação é descrito em Olá [Web Services Federation Language (WS-Federation) versão 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), que estende [metadados para OASIS SAML Security Assertion Markup Language () do hello v 2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).

## <a name="tenant-specific-and-tenant-independent-metadata-endpoints"></a>Pontos de extremidade de metadados específicos de locatário e independentes de locatário
O AD do Azure publica pontos de extremidade específicos de locatário e independentes de locatário.

Pontos de extremidade específicos de locatário destinam-se a um locatário específico. metadados de Federação específicos de locatário de saudação incluem informações sobre o locatário hello, incluindo informações de ponto de extremidade e emissor específico de locatário. Aplicativos que restringem o locatário do acesso tooa único usam pontos de extremidade específicos de locatário.

Pontos de extremidade independentes de locatário fornecem informações que é comum tooall locatários do AD Azure. Essas informações se aplicam a tootenants hospedado em *login.microsoftonline.com* e são compartilhadas por locatários. Os pontos de extremidade independentes de locatário são recomendados para aplicativos com vários locatários, pois eles não estão associados a qualquer locatário específico.

## <a name="federation-metadata-endpoints"></a>Pontos de extremidade de metadados de federação
O Azure AD publica metadados de federação em `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.

Para **pontos de extremidade específicos de locatário**, Olá `TenantDomainName` pode ser um dos seguintes tipos de saudação:

* Um nome de domínio registrado de um locatário do Azure AD, como: `contoso.onmicrosoft.com`.
* Olá imutável locatário ID de domínio hello, como `72f988bf-86f1-41af-91ab-2d7cd011db45`.

Para **pontos de extremidade independentes de locatário**, Olá `TenantDomainName` é `common`. Este documento lista apenas elementos de metadados de Federação Olá que são comuns tooall de locatários do AD do Azure que são hospedados em login.microsoftonline.com.

Por exemplo, um ponto de extremidade específico de locatário pode ser `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`. o ponto de extremidade do Hello independente de locatário é [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml). Você pode exibir o documento de metadados de Federação Olá digitando essa URL em um navegador.

## <a name="contents-of-federation-metadata"></a>Conteúdo de metadados de federação
Olá, seção a seguir fornece as informações necessárias para serviços que consomem Olá tokens emitidos pelo AD do Azure.

### <a name="entity-id"></a>ID da Entidade
Olá `EntityDescriptor` elemento contém um `EntityID` atributo. Olá valor Olá `EntityID` atributo representa o emissor hello, ou seja, segurança Olá serviço de token (STS) esse token emitido hello. É importante toovalidate emissor de hello quando você receber um token.

Olá metadados a seguir mostram um exemplo específico de locatário `EntityDescriptor` elemento com um `EntityID` elemento.

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="_b827a749-cfcb-46b3-ab8b-9f6d14a1294b"
entityID="https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db45/">
```
Você pode substituir Olá ID de locatário no ponto de extremidade do hello independente de locatário com seu toocreate de ID de locatário um locatário específico `EntityID` valor. valor resultante Hello serão Olá mesmo Olá emissor do token. Olá estratégia permite um emissor de saudação do aplicativo multilocatário toovalidate determinado locatário.

Olá metadados a seguir mostram um exemplo independente de locatário `EntityID` elemento. Observe que Olá `{tenant}` é um literal, não um espaço reservado.

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="="_0e5bd9d0-49ef-4258-bc15-21ce143b61bd"
entityID="https://sts.windows.net/{tenant}/">
```

### <a name="token-signing-certificates"></a>Certificados de autenticação de tokens
Quando um serviço recebe um token emitido por um locatário do AD do Azure, hello assinatura de token Olá deve ser validada com uma chave de assinatura que é publicada no documento de metadados de Federação hello. metadados de Federação Olá incluem parte pública de saudação dos certificados de saudação que locatários Olá usam para autenticação de tokens. bytes brutos do certificado Olá aparecem no hello `KeyDescriptor` elemento. certificado de assinatura de token de saudação é válido para assinatura somente quando Olá valor Olá `use` atributo é `signing`.

Um documento de metadados de Federação publicado pelo AD do Azure pode ter várias chaves de assinatura, como quando o AD do Azure está preparando Olá tooupdate certificado de assinatura. Quando um documento de metadados de Federação inclui mais de um certificado, um serviço que valida os tokens de saudação deve dar suporte todos os certificados no documento de saudação.

Olá, metadados a seguir mostram um exemplo `KeyDescriptor` elemento com uma chave de assinatura.

```
<KeyDescriptor use="signing">
<KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
<X509Data>
<X509Certificate>
MIIDPjCCAiqgAwIBAgIQVWmXY/+9RqFA/OG9kFulHDAJBgUrDgMCHQUAMC0xKzApBgNVBAMTImFjY291bnRzLmFjY2Vzc2NvbnRyb2wud2luZG93cy5uZXQwHhcNMTIwNjA3MDcwMDAwWhcNMTQwNjA3MDcwMDAwWjAtMSswKQYDVQQDEyJhY2NvdW50cy5hY2Nlc3Njb250cm9sLndpbmRvd3MubmV0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEArCz8Sn3GGXmikH2MdTeGY1D711EORX/lVXpr+ecGgqfUWF8MPB07XkYuJ54DAuYT318+2XrzMjOtqkT94VkXmxv6dFGhG8YZ8vNMPd4tdj9c0lpvWQdqXtL1TlFRpD/P6UMEigfN0c9oWDg9U7Ilymgei0UXtf1gtcQbc5sSQU0S4vr9YJp2gLFIGK11Iqg4XSGdcI0QWLLkkC6cBukhVnd6BCYbLjTYy3fNs4DzNdemJlxGl8sLexFytBF6YApvSdus3nFXaMCtBGx16HzkK9ne3lobAwL2o79bP4imEGqg+ibvyNmbrwFGnQrBc1jTF9LyQX9q+louxVfHs6ZiVwIDAQABo2IwYDBeBgNVHQEEVzBVgBCxDDsLd8xkfOLKm4Q/SzjtoS8wLTErMCkGA1UEAxMiYWNjb3VudHMuYWNjZXNzY29udHJvbC53aW5kb3dzLm5ldIIQVWmXY/+9RqFA/OG9kFulHDAJBgUrDgMCHQUAA4IBAQAkJtxxm/ErgySlNk69+1odTMP8Oy6L0H17z7XGG3w4TqvTUSWaxD4hSFJ0e7mHLQLQD7oV/erACXwSZn2pMoZ89MBDjOMQA+e6QzGB7jmSzPTNmQgMLA8fWCfqPrz6zgH+1F1gNp8hJY57kfeVPBiyjuBmlTEBsBlzolY9dd/55qqfQk6cgSeCbHCy/RU/iep0+UsRMlSgPNNmqhj5gmN2AFVCN96zF694LwuPae5CeR2ZcVknexOWHYjFM0MgUSw0ubnGl0h9AJgGyhvNGcjQqu9vd1xkupFgaN+f7P3p3EVN5csBg5H94jEcQZT7EKeTiZ6bTrpDAnrr8tDCy8ng
</X509Certificate>
</X509Data>
</KeyInfo>
</KeyDescriptor>
  ```

Olá `KeyDescriptor` elemento aparece em dois locais no documento de metadados de Federação Olá; na seção Olá específico do WS-Federation e Olá SAML específica. certificados de saudação publicados em ambas as seções serão Olá mesmo.

Na seção de saudação específico do WS-Federation, um leitor de metadados do WS-Federation lê os certificados de saudação de um `RoleDescriptor` elemento com hello `SecurityTokenServiceType` tipo.

Olá, metadados a seguir mostram um exemplo `RoleDescriptor` elemento.

```
<RoleDescriptor xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:fed="http://docs.oasis-open.org/wsfed/federation/200706" xsi:type="fed:SecurityTokenServiceType"protocolSupportEnumeration="http://docs.oasis-open.org/wsfed/federation/200706">
```

Na seção de saudação SAML específica, um leitor de metadados do WS-Federation lê os certificados de saudação de um `IDPSSODescriptor` elemento.

Olá, metadados a seguir mostram um exemplo `IDPSSODescriptor` elemento.

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
```
Não há nenhuma diferença no formato de saudação de certificados específicos do locatário e independentes de locatário.

### <a name="ws-federation-endpoint-url"></a>URL de ponto de extremidade de WS-Federation
metadados de Federação Olá incluem Olá URL é o Azure AD usa para logon único e saída no protocolo WS-Federation. Esse ponto de extremidade aparece no hello `PassiveRequestorEndpoint` elemento.

Olá, metadados a seguir mostram um exemplo `PassiveRequestorEndpoint` elemento para um ponto de extremidade específico de locatário.

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/72f988bf-86f1-41af-91ab-2d7cd011db45/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```
Ponto de extremidade Olá independente de locatário, Olá URL do WS-Federation aparece no ponto de extremidade Olá WS-Federation, como mostrado na saudação de exemplo a seguir.

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/common/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```

### <a name="saml-protocol-endpoint-url"></a>URL de ponto de extremidade do protocolo SAML
metadados de Federação Olá incluem Olá URL que usa o AD do Azure para logon único e saída no protocolo SAML 2.0. Esses pontos de extremidade aparecem no hello `IDPSSODescriptor` elemento.

Olá entrada e saída URLs aparecem na Olá `SingleSignOnService` e `SingleLogoutService` elementos.

Olá, metadados a seguir mostram um exemplo `PassiveResistorEndpoint` para um ponto de extremidade específico de locatário.

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com /saml2" />
  </IDPSSODescriptor>
```

Da mesma forma pontos de extremidade Olá para pontos de extremidade de protocolo SAML 2.0 comum Olá são publicados nos metadados de Federação independentes do locatário hello, conforme mostrado no hello exemplo a seguir.

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
  </IDPSSODescriptor>
```
