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
# <a name="federation-metadata"></a><span data-ttu-id="11894-103">Metadados de federação</span><span class="sxs-lookup"><span data-stu-id="11894-103">Federation metadata</span></span>
<span data-ttu-id="11894-104">Azure Active Directory (AD do Azure) publica um documento de metadados de federação para serviços que é configurado tooaccept tokens de segurança de saudação que emitem o AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="11894-104">Azure Active Directory (Azure AD) publishes a federation metadata document for services that is configured tooaccept hello security tokens that Azure AD issues.</span></span> <span data-ttu-id="11894-105">Olá formato de documento de metadados de Federação é descrito em Olá [Web Services Federation Language (WS-Federation) versão 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), que estende [metadados para OASIS SAML Security Assertion Markup Language () do hello v 2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).</span><span class="sxs-lookup"><span data-stu-id="11894-105">hello federation metadata document format is described in hello [Web Services Federation Language (WS-Federation) Version 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), which extends [Metadata for hello OASIS Security Assertion Markup Language (SAML) v2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).</span></span>

## <a name="tenant-specific-and-tenant-independent-metadata-endpoints"></a><span data-ttu-id="11894-106">Pontos de extremidade de metadados específicos de locatário e independentes de locatário</span><span class="sxs-lookup"><span data-stu-id="11894-106">Tenant-specific and Tenant-independent metadata endpoints</span></span>
<span data-ttu-id="11894-107">O AD do Azure publica pontos de extremidade específicos de locatário e independentes de locatário.</span><span class="sxs-lookup"><span data-stu-id="11894-107">Azure AD publishes tenant-specific and tenant-independent endpoints.</span></span>

<span data-ttu-id="11894-108">Pontos de extremidade específicos de locatário destinam-se a um locatário específico.</span><span class="sxs-lookup"><span data-stu-id="11894-108">Tenant-specific endpoints are designed for a particular tenant.</span></span> <span data-ttu-id="11894-109">metadados de Federação específicos de locatário de saudação incluem informações sobre o locatário hello, incluindo informações de ponto de extremidade e emissor específico de locatário.</span><span class="sxs-lookup"><span data-stu-id="11894-109">hello tenant-specific federation metadata includes information about hello tenant, including tenant-specific issuer and endpoint information.</span></span> <span data-ttu-id="11894-110">Aplicativos que restringem o locatário do acesso tooa único usam pontos de extremidade específicos de locatário.</span><span class="sxs-lookup"><span data-stu-id="11894-110">Applications that restrict access tooa single tenant use tenant-specific endpoints.</span></span>

<span data-ttu-id="11894-111">Pontos de extremidade independentes de locatário fornecem informações que é comum tooall locatários do AD Azure.</span><span class="sxs-lookup"><span data-stu-id="11894-111">Tenant-independent endpoints provide information that is common tooall Azure AD tenants.</span></span> <span data-ttu-id="11894-112">Essas informações se aplicam a tootenants hospedado em *login.microsoftonline.com* e são compartilhadas por locatários.</span><span class="sxs-lookup"><span data-stu-id="11894-112">This information applies tootenants hosted at *login.microsoftonline.com* and is shared across tenants.</span></span> <span data-ttu-id="11894-113">Os pontos de extremidade independentes de locatário são recomendados para aplicativos com vários locatários, pois eles não estão associados a qualquer locatário específico.</span><span class="sxs-lookup"><span data-stu-id="11894-113">Tenant-independent endpoints are recommended for multi-tenant applications, since they are not associated with any particular tenant.</span></span>

## <a name="federation-metadata-endpoints"></a><span data-ttu-id="11894-114">Pontos de extremidade de metadados de federação</span><span class="sxs-lookup"><span data-stu-id="11894-114">Federation metadata endpoints</span></span>
<span data-ttu-id="11894-115">O Azure AD publica metadados de federação em `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span><span class="sxs-lookup"><span data-stu-id="11894-115">Azure AD publishes federation metadata at `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span>

<span data-ttu-id="11894-116">Para **pontos de extremidade específicos de locatário**, Olá `TenantDomainName` pode ser um dos seguintes tipos de saudação:</span><span class="sxs-lookup"><span data-stu-id="11894-116">For **tenant-specific endpoints**, hello `TenantDomainName` can be one of hello following types:</span></span>

* <span data-ttu-id="11894-117">Um nome de domínio registrado de um locatário do Azure AD, como: `contoso.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="11894-117">A registered domain name of an Azure AD tenant, such as: `contoso.onmicrosoft.com`.</span></span>
* <span data-ttu-id="11894-118">Olá imutável locatário ID de domínio hello, como `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span><span class="sxs-lookup"><span data-stu-id="11894-118">hello immutable tenant ID of hello domain, such as `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span></span>

<span data-ttu-id="11894-119">Para **pontos de extremidade independentes de locatário**, Olá `TenantDomainName` é `common`.</span><span class="sxs-lookup"><span data-stu-id="11894-119">For **tenant-independent endpoints**, hello `TenantDomainName` is `common`.</span></span> <span data-ttu-id="11894-120">Este documento lista apenas elementos de metadados de Federação Olá que são comuns tooall de locatários do AD do Azure que são hospedados em login.microsoftonline.com.</span><span class="sxs-lookup"><span data-stu-id="11894-120">This document lists only hello Federation Metadata elements that are common tooall Azure AD tenants that are hosted at login.microsoftonline.com.</span></span>

<span data-ttu-id="11894-121">Por exemplo, um ponto de extremidade específico de locatário pode ser `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span><span class="sxs-lookup"><span data-stu-id="11894-121">For example, a tenant-specific endpoint might be `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span> <span data-ttu-id="11894-122">o ponto de extremidade do Hello independente de locatário é [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span><span class="sxs-lookup"><span data-stu-id="11894-122">hello tenant-independent endpoint is [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span></span> <span data-ttu-id="11894-123">Você pode exibir o documento de metadados de Federação Olá digitando essa URL em um navegador.</span><span class="sxs-lookup"><span data-stu-id="11894-123">You can view hello federation metadata document by typing this URL in a browser.</span></span>

## <a name="contents-of-federation-metadata"></a><span data-ttu-id="11894-124">Conteúdo de metadados de federação</span><span class="sxs-lookup"><span data-stu-id="11894-124">Contents of federation Metadata</span></span>
<span data-ttu-id="11894-125">Olá, seção a seguir fornece as informações necessárias para serviços que consomem Olá tokens emitidos pelo AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="11894-125">hello following section provides information needed by services that consume hello tokens issued by Azure AD.</span></span>

### <a name="entity-id"></a><span data-ttu-id="11894-126">ID da Entidade</span><span class="sxs-lookup"><span data-stu-id="11894-126">Entity ID</span></span>
<span data-ttu-id="11894-127">Olá `EntityDescriptor` elemento contém um `EntityID` atributo.</span><span class="sxs-lookup"><span data-stu-id="11894-127">hello `EntityDescriptor` element contains an `EntityID` attribute.</span></span> <span data-ttu-id="11894-128">Olá valor Olá `EntityID` atributo representa o emissor hello, ou seja, segurança Olá serviço de token (STS) esse token emitido hello.</span><span class="sxs-lookup"><span data-stu-id="11894-128">hello value of hello `EntityID` attribute represents hello issuer, that is, hello security token service (STS) that issued hello token.</span></span> <span data-ttu-id="11894-129">É importante toovalidate emissor de hello quando você receber um token.</span><span class="sxs-lookup"><span data-stu-id="11894-129">It is important toovalidate hello issuer when you receive a token.</span></span>

<span data-ttu-id="11894-130">Olá metadados a seguir mostram um exemplo específico de locatário `EntityDescriptor` elemento com um `EntityID` elemento.</span><span class="sxs-lookup"><span data-stu-id="11894-130">hello following metadata shows a sample tenant-specific `EntityDescriptor` element with an `EntityID` element.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="_b827a749-cfcb-46b3-ab8b-9f6d14a1294b"
entityID="https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db45/">
```
<span data-ttu-id="11894-131">Você pode substituir Olá ID de locatário no ponto de extremidade do hello independente de locatário com seu toocreate de ID de locatário um locatário específico `EntityID` valor.</span><span class="sxs-lookup"><span data-stu-id="11894-131">You can replace hello tenant ID in hello tenant-independent endpoint with your tenant ID toocreate a tenant-specific `EntityID` value.</span></span> <span data-ttu-id="11894-132">valor resultante Hello serão Olá mesmo Olá emissor do token.</span><span class="sxs-lookup"><span data-stu-id="11894-132">hello resulting value will be hello same as hello token issuer.</span></span> <span data-ttu-id="11894-133">Olá estratégia permite um emissor de saudação do aplicativo multilocatário toovalidate determinado locatário.</span><span class="sxs-lookup"><span data-stu-id="11894-133">hello strategy allows a multi-tenant application toovalidate hello issuer for a given tenant.</span></span>

<span data-ttu-id="11894-134">Olá metadados a seguir mostram um exemplo independente de locatário `EntityID` elemento.</span><span class="sxs-lookup"><span data-stu-id="11894-134">hello following metadata shows a sample tenant-independent `EntityID` element.</span></span> <span data-ttu-id="11894-135">Observe que Olá `{tenant}` é um literal, não um espaço reservado.</span><span class="sxs-lookup"><span data-stu-id="11894-135">Please note, that hello `{tenant}` is a literal, not a placeholder.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="="_0e5bd9d0-49ef-4258-bc15-21ce143b61bd"
entityID="https://sts.windows.net/{tenant}/">
```

### <a name="token-signing-certificates"></a><span data-ttu-id="11894-136">Certificados de autenticação de tokens</span><span class="sxs-lookup"><span data-stu-id="11894-136">Token signing certificates</span></span>
<span data-ttu-id="11894-137">Quando um serviço recebe um token emitido por um locatário do AD do Azure, hello assinatura de token Olá deve ser validada com uma chave de assinatura que é publicada no documento de metadados de Federação hello.</span><span class="sxs-lookup"><span data-stu-id="11894-137">When a service receives a token that is issued by a Azure AD tenant, hello signature of hello token must be validated with a signing key that is published in hello federation metadata document.</span></span> <span data-ttu-id="11894-138">metadados de Federação Olá incluem parte pública de saudação dos certificados de saudação que locatários Olá usam para autenticação de tokens.</span><span class="sxs-lookup"><span data-stu-id="11894-138">hello federation metadata includes hello public portion of hello certificates that hello tenants use for token signing.</span></span> <span data-ttu-id="11894-139">bytes brutos do certificado Olá aparecem no hello `KeyDescriptor` elemento.</span><span class="sxs-lookup"><span data-stu-id="11894-139">hello certificate raw bytes appear in hello `KeyDescriptor` element.</span></span> <span data-ttu-id="11894-140">certificado de assinatura de token de saudação é válido para assinatura somente quando Olá valor Olá `use` atributo é `signing`.</span><span class="sxs-lookup"><span data-stu-id="11894-140">hello token signing certificate is valid for signing only when hello value of hello `use` attribute is `signing`.</span></span>

<span data-ttu-id="11894-141">Um documento de metadados de Federação publicado pelo AD do Azure pode ter várias chaves de assinatura, como quando o AD do Azure está preparando Olá tooupdate certificado de assinatura.</span><span class="sxs-lookup"><span data-stu-id="11894-141">A federation metadata document published by Azure AD can have multiple signing keys, such as when Azure AD is preparing tooupdate hello signing certificate.</span></span> <span data-ttu-id="11894-142">Quando um documento de metadados de Federação inclui mais de um certificado, um serviço que valida os tokens de saudação deve dar suporte todos os certificados no documento de saudação.</span><span class="sxs-lookup"><span data-stu-id="11894-142">When a federation metadata document includes more than one certificate, a service that is validating hello tokens should support all certificates in hello document.</span></span>

<span data-ttu-id="11894-143">Olá, metadados a seguir mostram um exemplo `KeyDescriptor` elemento com uma chave de assinatura.</span><span class="sxs-lookup"><span data-stu-id="11894-143">hello following metadata shows a sample `KeyDescriptor` element with a signing key.</span></span>

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

<span data-ttu-id="11894-144">Olá `KeyDescriptor` elemento aparece em dois locais no documento de metadados de Federação Olá; na seção Olá específico do WS-Federation e Olá SAML específica.</span><span class="sxs-lookup"><span data-stu-id="11894-144">hello `KeyDescriptor` element appears in two places in hello federation metadata document; in hello WS-Federation-specific section and hello SAML-specific section.</span></span> <span data-ttu-id="11894-145">certificados de saudação publicados em ambas as seções serão Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="11894-145">hello certificates published in both sections will be hello same.</span></span>

<span data-ttu-id="11894-146">Na seção de saudação específico do WS-Federation, um leitor de metadados do WS-Federation lê os certificados de saudação de um `RoleDescriptor` elemento com hello `SecurityTokenServiceType` tipo.</span><span class="sxs-lookup"><span data-stu-id="11894-146">In hello WS-Federation-specific section, a WS-Federation metadata reader would read hello certificates from a `RoleDescriptor` element with hello `SecurityTokenServiceType` type.</span></span>

<span data-ttu-id="11894-147">Olá, metadados a seguir mostram um exemplo `RoleDescriptor` elemento.</span><span class="sxs-lookup"><span data-stu-id="11894-147">hello following metadata shows a sample `RoleDescriptor` element.</span></span>

```
<RoleDescriptor xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:fed="http://docs.oasis-open.org/wsfed/federation/200706" xsi:type="fed:SecurityTokenServiceType"protocolSupportEnumeration="http://docs.oasis-open.org/wsfed/federation/200706">
```

<span data-ttu-id="11894-148">Na seção de saudação SAML específica, um leitor de metadados do WS-Federation lê os certificados de saudação de um `IDPSSODescriptor` elemento.</span><span class="sxs-lookup"><span data-stu-id="11894-148">In hello SAML-specific section, a WS-Federation metadata reader would read hello certificates from a `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="11894-149">Olá, metadados a seguir mostram um exemplo `IDPSSODescriptor` elemento.</span><span class="sxs-lookup"><span data-stu-id="11894-149">hello following metadata shows a sample `IDPSSODescriptor` element.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
```
<span data-ttu-id="11894-150">Não há nenhuma diferença no formato de saudação de certificados específicos do locatário e independentes de locatário.</span><span class="sxs-lookup"><span data-stu-id="11894-150">There are no differences in hello format of tenant-specific and tenant-independent certificates.</span></span>

### <a name="ws-federation-endpoint-url"></a><span data-ttu-id="11894-151">URL de ponto de extremidade de WS-Federation</span><span class="sxs-lookup"><span data-stu-id="11894-151">WS-Federation endpoint URL</span></span>
<span data-ttu-id="11894-152">metadados de Federação Olá incluem Olá URL é o Azure AD usa para logon único e saída no protocolo WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="11894-152">hello federation metadata includes hello URL that is Azure AD uses for single sign-in and single sign-out in WS-Federation protocol.</span></span> <span data-ttu-id="11894-153">Esse ponto de extremidade aparece no hello `PassiveRequestorEndpoint` elemento.</span><span class="sxs-lookup"><span data-stu-id="11894-153">This endpoint appears in hello `PassiveRequestorEndpoint` element.</span></span>

<span data-ttu-id="11894-154">Olá, metadados a seguir mostram um exemplo `PassiveRequestorEndpoint` elemento para um ponto de extremidade específico de locatário.</span><span class="sxs-lookup"><span data-stu-id="11894-154">hello following metadata shows a sample `PassiveRequestorEndpoint` element for a tenant-specific endpoint.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/72f988bf-86f1-41af-91ab-2d7cd011db45/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```
<span data-ttu-id="11894-155">Ponto de extremidade Olá independente de locatário, Olá URL do WS-Federation aparece no ponto de extremidade Olá WS-Federation, como mostrado na saudação de exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="11894-155">For hello tenant-independent endpoint, hello WS-Federation URL appears in hello WS-Federation endpoint, as shown in hello following sample.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/common/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```

### <a name="saml-protocol-endpoint-url"></a><span data-ttu-id="11894-156">URL de ponto de extremidade do protocolo SAML</span><span class="sxs-lookup"><span data-stu-id="11894-156">SAML protocol endpoint URL</span></span>
<span data-ttu-id="11894-157">metadados de Federação Olá incluem Olá URL que usa o AD do Azure para logon único e saída no protocolo SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="11894-157">hello federation metadata includes hello URL that Azure AD uses for single sign-in and single sign-out in SAML 2.0 protocol.</span></span> <span data-ttu-id="11894-158">Esses pontos de extremidade aparecem no hello `IDPSSODescriptor` elemento.</span><span class="sxs-lookup"><span data-stu-id="11894-158">These endpoints appear in hello `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="11894-159">Olá entrada e saída URLs aparecem na Olá `SingleSignOnService` e `SingleLogoutService` elementos.</span><span class="sxs-lookup"><span data-stu-id="11894-159">hello sign-in and sign-out URLs appear in hello `SingleSignOnService` and `SingleLogoutService` elements.</span></span>

<span data-ttu-id="11894-160">Olá, metadados a seguir mostram um exemplo `PassiveResistorEndpoint` para um ponto de extremidade específico de locatário.</span><span class="sxs-lookup"><span data-stu-id="11894-160">hello following metadata shows a sample `PassiveResistorEndpoint` for a tenant-specific endpoint.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com /saml2" />
  </IDPSSODescriptor>
```

<span data-ttu-id="11894-161">Da mesma forma pontos de extremidade Olá para pontos de extremidade de protocolo SAML 2.0 comum Olá são publicados nos metadados de Federação independentes do locatário hello, conforme mostrado no hello exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="11894-161">Similarly hello endpoints for hello common SAML 2.0 protocol endpoints are published in hello tenant-independent federation metadata, as shown in hello following sample.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
  </IDPSSODescriptor>
```
