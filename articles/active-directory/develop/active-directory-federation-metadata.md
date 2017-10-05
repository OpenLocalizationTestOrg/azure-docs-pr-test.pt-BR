---
title: "Metadados de Federação do Azure AD | Microsoft Docs"
description: "Este artigo descreve o documento de metadados de federação que o Azure Active Directory publica para serviços que aceitam tokens do Azure Active Directory."
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
ms.openlocfilehash: ecafb02a6ac13d1c3cd1fe77ef710cd8525e32b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="federation-metadata"></a><span data-ttu-id="c0de8-103">Metadados de federação</span><span class="sxs-lookup"><span data-stu-id="c0de8-103">Federation metadata</span></span>
<span data-ttu-id="c0de8-104">O Azure Active Directory (Azure AD) publica um documento de metadados federados para serviços que são configurados para aceitar os tokens de segurança que o Azure AD emite.</span><span class="sxs-lookup"><span data-stu-id="c0de8-104">Azure Active Directory (Azure AD) publishes a federation metadata document for services that is configured to accept the security tokens that Azure AD issues.</span></span> <span data-ttu-id="c0de8-105">O formato de documento de metadados federados é descrito no [Web Services Federation Language (WS-Federation) Version 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), que se estende para [Metadata for the OASIS Security Assertion Markup Language (SAML) v2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).</span><span class="sxs-lookup"><span data-stu-id="c0de8-105">The federation metadata document format is described in the [Web Services Federation Language (WS-Federation) Version 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html), which extends [Metadata for the OASIS Security Assertion Markup Language (SAML) v2.0](http://docs.oasis-open.org/security/saml/v2.0/saml-metadata-2.0-os.pdf).</span></span>

## <a name="tenant-specific-and-tenant-independent-metadata-endpoints"></a><span data-ttu-id="c0de8-106">Pontos de extremidade de metadados específicos de locatário e independentes de locatário</span><span class="sxs-lookup"><span data-stu-id="c0de8-106">Tenant-specific and Tenant-independent metadata endpoints</span></span>
<span data-ttu-id="c0de8-107">O AD do Azure publica pontos de extremidade específicos de locatário e independentes de locatário.</span><span class="sxs-lookup"><span data-stu-id="c0de8-107">Azure AD publishes tenant-specific and tenant-independent endpoints.</span></span>

<span data-ttu-id="c0de8-108">Pontos de extremidade específicos de locatário destinam-se a um locatário específico.</span><span class="sxs-lookup"><span data-stu-id="c0de8-108">Tenant-specific endpoints are designed for a particular tenant.</span></span> <span data-ttu-id="c0de8-109">Os metadados de federação específicos de locatário incluem informações sobre o locatário, incluindo informações de emissor e o ponto de extremidade específico de locatário.</span><span class="sxs-lookup"><span data-stu-id="c0de8-109">The tenant-specific federation metadata includes information about the tenant, including tenant-specific issuer and endpoint information.</span></span> <span data-ttu-id="c0de8-110">Os aplicativos que restringem o acesso a um único locatário usam pontos de extremidade específicos de locatário.</span><span class="sxs-lookup"><span data-stu-id="c0de8-110">Applications that restrict access to a single tenant use tenant-specific endpoints.</span></span>

<span data-ttu-id="c0de8-111">Os pontos de extremidade independentes de locatário fornecem informações que são comuns para todos os locatários do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c0de8-111">Tenant-independent endpoints provide information that is common to all Azure AD tenants.</span></span> <span data-ttu-id="c0de8-112">Essas informações se aplicam aos locatários hospedados em *login.microsoftonline.com* e são compartilhadas entre locatários.</span><span class="sxs-lookup"><span data-stu-id="c0de8-112">This information applies to tenants hosted at *login.microsoftonline.com* and is shared across tenants.</span></span> <span data-ttu-id="c0de8-113">Os pontos de extremidade independentes de locatário são recomendados para aplicativos com vários locatários, pois eles não estão associados a qualquer locatário específico.</span><span class="sxs-lookup"><span data-stu-id="c0de8-113">Tenant-independent endpoints are recommended for multi-tenant applications, since they are not associated with any particular tenant.</span></span>

## <a name="federation-metadata-endpoints"></a><span data-ttu-id="c0de8-114">Pontos de extremidade de metadados de federação</span><span class="sxs-lookup"><span data-stu-id="c0de8-114">Federation metadata endpoints</span></span>
<span data-ttu-id="c0de8-115">O Azure AD publica metadados de federação em `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span><span class="sxs-lookup"><span data-stu-id="c0de8-115">Azure AD publishes federation metadata at `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span>

<span data-ttu-id="c0de8-116">Para **pontos de extremidade específicos de locatário**, o `TenantDomainName` pode ser um dos seguintes tipos:</span><span class="sxs-lookup"><span data-stu-id="c0de8-116">For **tenant-specific endpoints**, the `TenantDomainName` can be one of the following types:</span></span>

* <span data-ttu-id="c0de8-117">Um nome de domínio registrado de um locatário do Azure AD, como: `contoso.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="c0de8-117">A registered domain name of an Azure AD tenant, such as: `contoso.onmicrosoft.com`.</span></span>
* <span data-ttu-id="c0de8-118">A ID de locatário imutável do domínio, como `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span><span class="sxs-lookup"><span data-stu-id="c0de8-118">The immutable tenant ID of the domain, such as `72f988bf-86f1-41af-91ab-2d7cd011db45`.</span></span>

<span data-ttu-id="c0de8-119">Para **pontos de extremidade independentes de locatário**, o `TenantDomainName` é `common`.</span><span class="sxs-lookup"><span data-stu-id="c0de8-119">For **tenant-independent endpoints**, the `TenantDomainName` is `common`.</span></span> <span data-ttu-id="c0de8-120">Este documento lista apenas os elementos de Metadados de Federação que são comuns a todos os locatários do Azure AD hospedados em login.microsoftonline.com.</span><span class="sxs-lookup"><span data-stu-id="c0de8-120">This document lists only the Federation Metadata elements that are common to all Azure AD tenants that are hosted at login.microsoftonline.com.</span></span>

<span data-ttu-id="c0de8-121">Por exemplo, um ponto de extremidade específico de locatário pode ser `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span><span class="sxs-lookup"><span data-stu-id="c0de8-121">For example, a tenant-specific endpoint might be `https://login.microsoftonline.com/contoso.onmicrosoft.com/FederationMetadata/2007-06/FederationMetadata.xml`.</span></span> <span data-ttu-id="c0de8-122">O ponto de extremidade independente de locatário é [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span><span class="sxs-lookup"><span data-stu-id="c0de8-122">The tenant-independent endpoint is [https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml](https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml).</span></span> <span data-ttu-id="c0de8-123">Você pode exibir o documento de metadados de federação digitando essa URL em um navegador.</span><span class="sxs-lookup"><span data-stu-id="c0de8-123">You can view the federation metadata document by typing this URL in a browser.</span></span>

## <a name="contents-of-federation-metadata"></a><span data-ttu-id="c0de8-124">Conteúdo de metadados de federação</span><span class="sxs-lookup"><span data-stu-id="c0de8-124">Contents of federation Metadata</span></span>
<span data-ttu-id="c0de8-125">A seção a seguir fornece as informações necessárias para serviços que consomem os tokens emitidos pelo AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c0de8-125">The following section provides information needed by services that consume the tokens issued by Azure AD.</span></span>

### <a name="entity-id"></a><span data-ttu-id="c0de8-126">ID da Entidade</span><span class="sxs-lookup"><span data-stu-id="c0de8-126">Entity ID</span></span>
<span data-ttu-id="c0de8-127">O elemento `EntityDescriptor` contém um atributo `EntityID`.</span><span class="sxs-lookup"><span data-stu-id="c0de8-127">The `EntityDescriptor` element contains an `EntityID` attribute.</span></span> <span data-ttu-id="c0de8-128">O valor do atributo `EntityID` representa o emissor, ou seja, o STS (serviço de token de segurança) que emitiu o token.</span><span class="sxs-lookup"><span data-stu-id="c0de8-128">The value of the `EntityID` attribute represents the issuer, that is, the security token service (STS) that issued the token.</span></span> <span data-ttu-id="c0de8-129">É importante validar o emissor ao receber um token.</span><span class="sxs-lookup"><span data-stu-id="c0de8-129">It is important to validate the issuer when you receive a token.</span></span>

<span data-ttu-id="c0de8-130">Os metadados a seguir mostram um exemplo de elemento `EntityDescriptor` específico de locatário com um elemento `EntityID`.</span><span class="sxs-lookup"><span data-stu-id="c0de8-130">The following metadata shows a sample tenant-specific `EntityDescriptor` element with an `EntityID` element.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="_b827a749-cfcb-46b3-ab8b-9f6d14a1294b"
entityID="https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db45/">
```
<span data-ttu-id="c0de8-131">Você pode substituir a ID de locatário no ponto de extremidade independente de locatário por sua ID de locatário para criar um valor `EntityID` específico de locatário.</span><span class="sxs-lookup"><span data-stu-id="c0de8-131">You can replace the tenant ID in the tenant-independent endpoint with your tenant ID to create a tenant-specific `EntityID` value.</span></span> <span data-ttu-id="c0de8-132">O valor resultante será igual ao emissor do token.</span><span class="sxs-lookup"><span data-stu-id="c0de8-132">The resulting value will be the same as the token issuer.</span></span> <span data-ttu-id="c0de8-133">Essa estratégia permite que um aplicativo multilocatário valide o emissor para determinado locatário.</span><span class="sxs-lookup"><span data-stu-id="c0de8-133">The strategy allows a multi-tenant application to validate the issuer for a given tenant.</span></span>

<span data-ttu-id="c0de8-134">Os metadados a seguir mostram um exemplo de elemento independente de locatário `EntityID` .</span><span class="sxs-lookup"><span data-stu-id="c0de8-134">The following metadata shows a sample tenant-independent `EntityID` element.</span></span> <span data-ttu-id="c0de8-135">Nesse elemento, observe que `{tenant}` é um literal, não um espaço reservado.</span><span class="sxs-lookup"><span data-stu-id="c0de8-135">Please note, that the `{tenant}` is a literal, not a placeholder.</span></span>

```
<EntityDescriptor
xmlns="urn:oasis:names:tc:SAML:2.0:metadata"
ID="="_0e5bd9d0-49ef-4258-bc15-21ce143b61bd"
entityID="https://sts.windows.net/{tenant}/">
```

### <a name="token-signing-certificates"></a><span data-ttu-id="c0de8-136">Certificados de autenticação de tokens</span><span class="sxs-lookup"><span data-stu-id="c0de8-136">Token signing certificates</span></span>
<span data-ttu-id="c0de8-137">Quando um serviço recebe um token emitido por um locatário do AD do Azure, a assinatura do token deve ser validada com uma chave de assinatura publicada no documento de metadados de federação.</span><span class="sxs-lookup"><span data-stu-id="c0de8-137">When a service receives a token that is issued by a Azure AD tenant, the signature of the token must be validated with a signing key that is published in the federation metadata document.</span></span> <span data-ttu-id="c0de8-138">Os metadados de federação incluem a parte pública dos certificados que os locatários usam para autenticação de tokens.</span><span class="sxs-lookup"><span data-stu-id="c0de8-138">The federation metadata includes the public portion of the certificates that the tenants use for token signing.</span></span> <span data-ttu-id="c0de8-139">Os bytes brutos do certificado aparecem no elemento `KeyDescriptor` .</span><span class="sxs-lookup"><span data-stu-id="c0de8-139">The certificate raw bytes appear in the `KeyDescriptor` element.</span></span> <span data-ttu-id="c0de8-140">O certificado de assinatura de token é válido para a assinatura somente quando o valor do atributo `use` é `signing`.</span><span class="sxs-lookup"><span data-stu-id="c0de8-140">The token signing certificate is valid for signing only when the value of the `use` attribute is `signing`.</span></span>

<span data-ttu-id="c0de8-141">Um documento de metadados de federação publicado pelo Azure AD pode ter várias chaves de assinatura, como quando o Azure AD está se preparando para atualizar o certificado de autenticação.</span><span class="sxs-lookup"><span data-stu-id="c0de8-141">A federation metadata document published by Azure AD can have multiple signing keys, such as when Azure AD is preparing to update the signing certificate.</span></span> <span data-ttu-id="c0de8-142">Quando um documento de metadados de federação inclui mais de um certificado, um serviço que valida os tokens deve dar suporte a todos os certificados no documento.</span><span class="sxs-lookup"><span data-stu-id="c0de8-142">When a federation metadata document includes more than one certificate, a service that is validating the tokens should support all certificates in the document.</span></span>

<span data-ttu-id="c0de8-143">Os metadados a seguir mostram um elemento de exemplo `KeyDescriptor` com uma chave de assinatura.</span><span class="sxs-lookup"><span data-stu-id="c0de8-143">The following metadata shows a sample `KeyDescriptor` element with a signing key.</span></span>

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

<span data-ttu-id="c0de8-144">O elemento `KeyDescriptor` aparece em dois lugares no documento de metadados federados na seção específica do WS-Federation e na seção específica de SAML.</span><span class="sxs-lookup"><span data-stu-id="c0de8-144">The `KeyDescriptor` element appears in two places in the federation metadata document; in the WS-Federation-specific section and the SAML-specific section.</span></span> <span data-ttu-id="c0de8-145">Os certificados publicados em ambas as seções serão os mesmos.</span><span class="sxs-lookup"><span data-stu-id="c0de8-145">The certificates published in both sections will be the same.</span></span>

<span data-ttu-id="c0de8-146">Na seção específica do WS-Federation, um leitor de metadados de WS-Federation leria os certificados de um elemento `RoleDescriptor` com o tipo `SecurityTokenServiceType`.</span><span class="sxs-lookup"><span data-stu-id="c0de8-146">In the WS-Federation-specific section, a WS-Federation metadata reader would read the certificates from a `RoleDescriptor` element with the `SecurityTokenServiceType` type.</span></span>

<span data-ttu-id="c0de8-147">Os metadados a seguir mostram um elemento `RoleDescriptor` de exemplo.</span><span class="sxs-lookup"><span data-stu-id="c0de8-147">The following metadata shows a sample `RoleDescriptor` element.</span></span>

```
<RoleDescriptor xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:fed="http://docs.oasis-open.org/wsfed/federation/200706" xsi:type="fed:SecurityTokenServiceType"protocolSupportEnumeration="http://docs.oasis-open.org/wsfed/federation/200706">
```

<span data-ttu-id="c0de8-148">Na seção específica de SAML, um leitor de metadados de WS-Federation leria os certificados de um `IDPSSODescriptor` elemento.</span><span class="sxs-lookup"><span data-stu-id="c0de8-148">In the SAML-specific section, a WS-Federation metadata reader would read the certificates from a `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="c0de8-149">Os metadados a seguir mostram um elemento `IDPSSODescriptor` de exemplo.</span><span class="sxs-lookup"><span data-stu-id="c0de8-149">The following metadata shows a sample `IDPSSODescriptor` element.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
```
<span data-ttu-id="c0de8-150">Não há diferenças no formato de certificados específicos de locatário e independentes de locatário.</span><span class="sxs-lookup"><span data-stu-id="c0de8-150">There are no differences in the format of tenant-specific and tenant-independent certificates.</span></span>

### <a name="ws-federation-endpoint-url"></a><span data-ttu-id="c0de8-151">URL de ponto de extremidade de WS-Federation</span><span class="sxs-lookup"><span data-stu-id="c0de8-151">WS-Federation endpoint URL</span></span>
<span data-ttu-id="c0de8-152">Os metadados de federação incluem a URL que usa o AD do Azure para logon único e saída única no protocolo WS-Federation.</span><span class="sxs-lookup"><span data-stu-id="c0de8-152">The federation metadata includes the URL that is Azure AD uses for single sign-in and single sign-out in WS-Federation protocol.</span></span> <span data-ttu-id="c0de8-153">Esse ponto de extremidade é mostrado no `PassiveRequestorEndpoint` elemento.</span><span class="sxs-lookup"><span data-stu-id="c0de8-153">This endpoint appears in the `PassiveRequestorEndpoint` element.</span></span>

<span data-ttu-id="c0de8-154">Os metadados a seguir mostram um elemento `PassiveRequestorEndpoint` de exemplo para um ponto de extremidade específico de locatário.</span><span class="sxs-lookup"><span data-stu-id="c0de8-154">The following metadata shows a sample `PassiveRequestorEndpoint` element for a tenant-specific endpoint.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/72f988bf-86f1-41af-91ab-2d7cd011db45/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```
<span data-ttu-id="c0de8-155">Para o ponto de extremidade independente de locatário, a URL de WS-Federation aparece no ponto de extremidade WS-Federation, conforme mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="c0de8-155">For the tenant-independent endpoint, the WS-Federation URL appears in the WS-Federation endpoint, as shown in the following sample.</span></span>

```
<fed:PassiveRequestorEndpoint>
<EndpointReference xmlns="http://www.w3.org/2005/08/addressing">
<Address>
https://login.microsoftonline.com/common/wsfed
</Address>
</EndpointReference>
</fed:PassiveRequestorEndpoint>
```

### <a name="saml-protocol-endpoint-url"></a><span data-ttu-id="c0de8-156">URL de ponto de extremidade do protocolo SAML</span><span class="sxs-lookup"><span data-stu-id="c0de8-156">SAML protocol endpoint URL</span></span>
<span data-ttu-id="c0de8-157">Os metadados de Federação incluem a URL que o AD do Azure usa para logon único e saída única no protocolo SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="c0de8-157">The federation metadata includes the URL that Azure AD uses for single sign-in and single sign-out in SAML 2.0 protocol.</span></span> <span data-ttu-id="c0de8-158">Esses pontos de extremidade aparecem no `IDPSSODescriptor` elemento.</span><span class="sxs-lookup"><span data-stu-id="c0de8-158">These endpoints appear in the `IDPSSODescriptor` element.</span></span>

<span data-ttu-id="c0de8-159">As URLs de entrada e saída aparecem nos elementos `SingleSignOnService` e `SingleLogoutService`.</span><span class="sxs-lookup"><span data-stu-id="c0de8-159">The sign-in and sign-out URLs appear in the `SingleSignOnService` and `SingleLogoutService` elements.</span></span>

<span data-ttu-id="c0de8-160">Os metadados a seguir mostram um `PassiveResistorEndpoint` de exemplo para um ponto de extremidade específico de locatário.</span><span class="sxs-lookup"><span data-stu-id="c0de8-160">The following metadata shows a sample `PassiveResistorEndpoint` for a tenant-specific endpoint.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/contoso.onmicrosoft.com /saml2" />
  </IDPSSODescriptor>
```

<span data-ttu-id="c0de8-161">Da mesma forma, os pontos de extremidade para os pontos de extremidade de protocolo SAML 2.0 comuns são publicados nos metadados de federação independentes de locatário, conforme mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="c0de8-161">Similarly the endpoints for the common SAML 2.0 protocol endpoints are published in the tenant-independent federation metadata, as shown in the following sample.</span></span>

```
<IDPSSODescriptor protocolSupportEnumeration="urn:oasis:names:tc:SAML:2.0:protocol">
…
    <SingleLogoutService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
    <SingleSignOnService Binding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect" Location="https://login.microsoftonline.com/common/saml2" />
  </IDPSSODescriptor>
```
