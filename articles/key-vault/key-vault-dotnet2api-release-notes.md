---
title: "aaaKey notas de versão de API do cofre .NET 2. x | Microsoft Docs"
description: "Os desenvolvedores de .NET usará toocode essa API para o Cofre de chaves do Azure"
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
editor: bruceper
ms.assetid: 1cccf21b-5be9-4a49-8145-483b695124ba
ms.service: key-vault
ms.devlang: CSharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/02/2017
ms.author: bruceper
ms.openlocfilehash: d95b84cf73c155f117f37e93893f27b02a75855c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-net-20---release-notes-and-migration-guide"></a><span data-ttu-id="a0d20-103">.NET 2.0 para Cofre de Chaves do Azure - Notas de versão e guia de migração</span><span class="sxs-lookup"><span data-stu-id="a0d20-103">Azure Key Vault .NET 2.0 - Release Notes and Migration Guide</span></span>
<span data-ttu-id="a0d20-104">Olá notas e diretrizes a seguir são para desenvolvedores que trabalham com Azure Key Vault .NET / biblioteca C#.</span><span class="sxs-lookup"><span data-stu-id="a0d20-104">hello following notes and guidance are for developers working with Azure Key Vault .NET / C# library.</span></span> <span data-ttu-id="a0d20-105">Em transição de saudação do toohello 2.0 versão da saudação 1.0, um número de atualizações foram feito que exigem trabalho de migração em seu código para que você toobenefit das melhorias funcionais hello e adições de recursos, como **Cofre de chaves certificados** suporte.</span><span class="sxs-lookup"><span data-stu-id="a0d20-105">In hello transition from hello 1.0 version toohello 2.0 version, a number of updates have been made that will require migration work in your code in order for you toobenefit from hello functional improvements and feature additions such as **Key Vault certificates** support.</span></span>

## <a name="key-vault-certificates"></a><span data-ttu-id="a0d20-106">Certificados do Key Vault</span><span class="sxs-lookup"><span data-stu-id="a0d20-106">Key Vault certificates</span></span>

<span data-ttu-id="a0d20-107">Fornece suporte de certificados de Cofre de chaves para o gerenciamento de seu x509 certificados e hello comportamentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="a0d20-107">Key Vault certificates support provides for management of your x509 certificates and hello following behaviors:</span></span>  

* <span data-ttu-id="a0d20-108">Um toocreate de proprietário do certificado permite que um certificado por meio de um processo de criação de Cofre de chaves ou importação de saudação de um certificado existente.</span><span class="sxs-lookup"><span data-stu-id="a0d20-108">Allows a certificate owner toocreate a certificate through a Key Vault creation process or through hello import of an existing certificate.</span></span> <span data-ttu-id="a0d20-109">Isso inclui certificados autoassinados e gerados por Autoridades de Certificação.</span><span class="sxs-lookup"><span data-stu-id="a0d20-109">This includes both self-signed and Certificate Authority generated certificates.</span></span>
* <span data-ttu-id="a0d20-110">Permite que um proprietário de certificados de Cofre de chaves tooimplement de armazenamento seguro e o gerenciamento de X509 certificados sem interação com o material da chave privada.</span><span class="sxs-lookup"><span data-stu-id="a0d20-110">Allows a Key Vault certificate owner tooimplement secure storage and management of X509 certificates without interaction with private key material.</span></span>  
* <span data-ttu-id="a0d20-111">Permite um toocreate de proprietário do certificado em uma política que direciona o Cofre de chaves toomanage Olá ciclo de vida de um certificado.</span><span class="sxs-lookup"><span data-stu-id="a0d20-111">Allows a certificate owner toocreate a policy that directs Key Vault toomanage hello life-cycle of a certificate.</span></span>  
* <span data-ttu-id="a0d20-112">Permite que os proprietários de certificado tooprovide informações de contato para a notificação sobre eventos de ciclo de vida de expiração e renovação de certificado.</span><span class="sxs-lookup"><span data-stu-id="a0d20-112">Allows certificate owners tooprovide contact information for notification about life-cycle events of expiration and renewal of certificate.</span></span>  
* <span data-ttu-id="a0d20-113">Oferece suporte à renovação automática com emissores selecionados - provedores de certificado X509/autoridades de certificação parceiros do Cofre de Chaves.</span><span class="sxs-lookup"><span data-stu-id="a0d20-113">Supports automatic renewal with selected issuers - Key Vault partner X509 certificate providers / certificate authorities.</span></span>
  
  * <span data-ttu-id="a0d20-114">Observação: provedores não têm parcerias/autoridades também são permitidas, mas, não dará suporte a recurso de renovação automática hello.</span><span class="sxs-lookup"><span data-stu-id="a0d20-114">NOTE - Non-partnered providers/authorities are also allowed but, will not support hello auto renewal feature.</span></span>

## <a name="net-support"></a><span data-ttu-id="a0d20-115">Suporte ao .NET</span><span class="sxs-lookup"><span data-stu-id="a0d20-115">.NET support</span></span>

* <span data-ttu-id="a0d20-116">**.NET 4.0** não tem suporte pela versão de hello 2.0 do hello Azure Key Vault .NET / biblioteca c#</span><span class="sxs-lookup"><span data-stu-id="a0d20-116">**.NET 4.0** is not supported by hello 2.0 version of hello Azure Key Vault .NET/C# library</span></span>
* <span data-ttu-id="a0d20-117">**.NET core** é compatível com a versão Olá 2.0 de hello Azure Key Vault .NET / biblioteca c#</span><span class="sxs-lookup"><span data-stu-id="a0d20-117">**.NET Core** is supported by hello 2.0 version of hello Azure Key Vault .NET/C# library</span></span>

## <a name="namespaces"></a><span data-ttu-id="a0d20-118">Namespaces</span><span class="sxs-lookup"><span data-stu-id="a0d20-118">Namespaces</span></span>

* <span data-ttu-id="a0d20-119">Olá namespace **modelos** é alterado de **Microsoft.Azure.KeyVault** muito**Microsoft.Azure.KeyVault.Models**.</span><span class="sxs-lookup"><span data-stu-id="a0d20-119">hello namespace for **models** is changed from **Microsoft.Azure.KeyVault** too**Microsoft.Azure.KeyVault.Models**.</span></span>
* <span data-ttu-id="a0d20-120">Olá **Microsoft.Azure.KeyVault.Internal** namespace é descartado.</span><span class="sxs-lookup"><span data-stu-id="a0d20-120">hello **Microsoft.Azure.KeyVault.Internal** namespace is dropped.</span></span>
* <span data-ttu-id="a0d20-121">namespace de dependências do SDK do Azure Olá são alterados de **Hyak.Common** e **Hyak.Common.Internals** muito**Microsoft.Rest** e  **Microsoft.Rest.Serialization**</span><span class="sxs-lookup"><span data-stu-id="a0d20-121">hello Azure SDK dependencies namespace are changed from **Hyak.Common** and **Hyak.Common.Internals** too**Microsoft.Rest** and **Microsoft.Rest.Serialization**</span></span>

## <a name="type-changes"></a><span data-ttu-id="a0d20-122">Alterações de tipo</span><span class="sxs-lookup"><span data-stu-id="a0d20-122">Type changes</span></span>

* <span data-ttu-id="a0d20-123">*Segredo* alterada muito*SecretBundle*</span><span class="sxs-lookup"><span data-stu-id="a0d20-123">*Secret* changed too*SecretBundle*</span></span>
* <span data-ttu-id="a0d20-124">*Dicionário* alterada muito*IDictionary*</span><span class="sxs-lookup"><span data-stu-id="a0d20-124">*Dictionary* changed too*IDictionary*</span></span>
* <span data-ttu-id="a0d20-125">*Lista<T>, string []* alterada muito*IList<T>*</span><span class="sxs-lookup"><span data-stu-id="a0d20-125">*List<T>, string []* changed too*IList<T>*</span></span>
* <span data-ttu-id="a0d20-126">*NextList* alterada muito *NextPageLink*</span><span class="sxs-lookup"><span data-stu-id="a0d20-126">*NextList* changed too *NextPageLink*</span></span>

## <a name="return-types"></a><span data-ttu-id="a0d20-127">Tipos de retorno</span><span class="sxs-lookup"><span data-stu-id="a0d20-127">Return types</span></span>

* <span data-ttu-id="a0d20-128">**KeyList** e **SecretList** retornarão *IPage<T>* em vez de *ListKeysResponseMessage*</span><span class="sxs-lookup"><span data-stu-id="a0d20-128">**KeyList** and **SecretList** will return *IPage<T>* instead of *ListKeysResponseMessage*</span></span>
* <span data-ttu-id="a0d20-129">Olá gerado **BackupKeyAsync** retornará *BackupKeyResult* que contém *valor* (blob de backup).</span><span class="sxs-lookup"><span data-stu-id="a0d20-129">hello generated **BackupKeyAsync** will return *BackupKeyResult* which contains *Value* (back-up blob).</span></span> <span data-ttu-id="a0d20-130">Antes de saudação método foi encapsulado e retornando valor Olá somente.</span><span class="sxs-lookup"><span data-stu-id="a0d20-130">Before hello method was wrapped and returning only hello value.</span></span>

## <a name="exceptions"></a><span data-ttu-id="a0d20-131">Exceções</span><span class="sxs-lookup"><span data-stu-id="a0d20-131">Exceptions</span></span>

* <span data-ttu-id="a0d20-132">*KeyVaultClientException* é alterada muito*KeyVaultErrorException*</span><span class="sxs-lookup"><span data-stu-id="a0d20-132">*KeyVaultClientException* is changed too*KeyVaultErrorException*</span></span>
* <span data-ttu-id="a0d20-133">Erro do serviço de saudação é alterado de *exceção. Erro* muito*exceção. Body.Error.Message*.</span><span class="sxs-lookup"><span data-stu-id="a0d20-133">hello service error is changed from *exception.Error* too*exception.Body.Error.Message*.</span></span>
* <span data-ttu-id="a0d20-134">Removido informações adicionais da mensagem de erro Olá para **[JsonExtensionData]**.</span><span class="sxs-lookup"><span data-stu-id="a0d20-134">Removed additional info from hello error message for **[JsonExtensionData]**.</span></span>

## <a name="constructors"></a><span data-ttu-id="a0d20-135">Construtores</span><span class="sxs-lookup"><span data-stu-id="a0d20-135">Constructors</span></span>

* <span data-ttu-id="a0d20-136">Em vez de aceitar um *HttpClient* como um argumento de construtor, construtor de saudação aceita apenas *HttpClientHandler* ou *DelegatingHandler []*.</span><span class="sxs-lookup"><span data-stu-id="a0d20-136">Instead of accepting an *HttpClient* as a constructor argument, hello constructor only accepts *HttpClientHandler* or *DelegatingHandler[]*.</span></span>

## <a name="downloaded-packages"></a><span data-ttu-id="a0d20-137">Pacotes baixados</span><span class="sxs-lookup"><span data-stu-id="a0d20-137">Downloaded packages</span></span>

<span data-ttu-id="a0d20-138">Quando um cliente está processando uma dependência no seguinte de saudação do Cofre de chaves foram baixados</span><span class="sxs-lookup"><span data-stu-id="a0d20-138">When a client is processing a  dependency on Key Vault hello following were downloaded</span></span>

### <a name="previous-package-list"></a><span data-ttu-id="a0d20-139">Lista de pacotes anterior</span><span class="sxs-lookup"><span data-stu-id="a0d20-139">Previous package list</span></span>

* <span data-ttu-id="a0d20-140">id do pacote="Hyak.Common" versão="1.0.2" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="a0d20-140">package id="Hyak.Common" version="1.0.2" targetFramework="net45"</span></span>
* <span data-ttu-id="a0d20-141">id do pacote="Microsoft.Azure.Common" versão="2.0.4" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="a0d20-141">package id="Microsoft.Azure.Common" version="2.0.4" targetFramework="net45"</span></span>
* <span data-ttu-id="a0d20-142">id do pacote="Microsoft.Azure.Common.Dependencies" versão="1.0.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="a0d20-142">package id="Microsoft.Azure.Common.Dependencies" version="1.0.0" targetFramework="net45"</span></span>
* <span data-ttu-id="a0d20-143">id do pacote="Microsoft.Azure.KeyVault" versão="1.0.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="a0d20-143">package id="Microsoft.Azure.KeyVault" version="1.0.0" targetFramework="net45"</span></span>
* <span data-ttu-id="a0d20-144">id do pacote="Microsoft.Bcl" versão="1.1.9" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="a0d20-144">package id="Microsoft.Bcl" version="1.1.9" targetFramework="net45"</span></span>
* <span data-ttu-id="a0d20-145">id do pacote="Microsoft.Bcl.Async" versão="1.0.168" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="a0d20-145">package id="Microsoft.Bcl.Async" version="1.0.168" targetFramework="net45"</span></span>
* <span data-ttu-id="a0d20-146">id do pacote="Microsoft.Bcl.Build" version="1.0.14" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="a0d20-146">package id="Microsoft.Bcl.Build" version="1.0.14" targetFramework="net45"</span></span>
* <span data-ttu-id="a0d20-147">id do pacote="Microsoft.Net.Http" versão="2.2.22" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="a0d20-147">package id="Microsoft.Net.Http" version="2.2.22" targetFramework="net45"</span></span>

### <a name="current-package-list"></a><span data-ttu-id="a0d20-148">Lista atual de pacotes</span><span class="sxs-lookup"><span data-stu-id="a0d20-148">Current package list</span></span>

* <span data-ttu-id="a0d20-149">id do pacote="Microsoft.Azure.KeyVault" versão="2.0.0-preview" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="a0d20-149">package id="Microsoft.Azure.KeyVault" version="2.0.0-preview" targetFramework="net45"</span></span>
* <span data-ttu-id="a0d20-150">id do pacote="Microsoft.Rest.ClientRuntime" versão="2.2.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="a0d20-150">package id="Microsoft.Rest.ClientRuntime" version="2.2.0" targetFramework="net45"</span></span>
* <span data-ttu-id="a0d20-151">id do pacote="Microsoft.Rest.ClientRuntime.Azure" versão="3.2.0" targetFramework="net45"</span><span class="sxs-lookup"><span data-stu-id="a0d20-151">package id="Microsoft.Rest.ClientRuntime.Azure" version="3.2.0" targetFramework="net45"</span></span>

## <a name="class-changes"></a><span data-ttu-id="a0d20-152">Alterações de classe</span><span class="sxs-lookup"><span data-stu-id="a0d20-152">Class changes</span></span>

* <span data-ttu-id="a0d20-153">A classe **UnixEpoch** foi removida</span><span class="sxs-lookup"><span data-stu-id="a0d20-153">**UnixEpoch** class has been removed</span></span>
* <span data-ttu-id="a0d20-154">**Base64UrlConverter** classe é renomeada muito**Base64UrlJsonConverter**</span><span class="sxs-lookup"><span data-stu-id="a0d20-154">**Base64UrlConverter** class is renamed too**Base64UrlJsonConverter**</span></span>

## <a name="other-changes"></a><span data-ttu-id="a0d20-155">Outras alterações</span><span class="sxs-lookup"><span data-stu-id="a0d20-155">Other changes</span></span>

* <span data-ttu-id="a0d20-156">Foi adicionado suporte para configuração de saudação da política de repetição de operação KV em falhas transitórias toothis versão da API de saudação.</span><span class="sxs-lookup"><span data-stu-id="a0d20-156">Support for hello configuration of KV operation retry policy on transient failures has been added toothis version of hello API.</span></span>

## <a name="microsoftazuremanagementkeyvault-nuget"></a><span data-ttu-id="a0d20-157">Microsoft.Azure.Management.KeyVault NuGet</span><span class="sxs-lookup"><span data-stu-id="a0d20-157">Microsoft.Azure.Management.KeyVault NuGet</span></span>

* <span data-ttu-id="a0d20-158">Para operações de saudação que retornaram um *cofre*, tipo de retorno de saudação foi uma classe que continha uma propriedade de cofre.</span><span class="sxs-lookup"><span data-stu-id="a0d20-158">For hello operations that returned a *vault*, hello return type was a class that contained a Vault property.</span></span> <span data-ttu-id="a0d20-159">Olá tipo de retorno é agora *cofre*.</span><span class="sxs-lookup"><span data-stu-id="a0d20-159">hello return type is now *Vault*.</span></span>
* <span data-ttu-id="a0d20-160">*PermissionsToKeys* e *PermissionsToSecrets* agora são *Permissions.Keys* e *Permissions.Secrets*</span><span class="sxs-lookup"><span data-stu-id="a0d20-160">*PermissionsToKeys* and *PermissionsToSecrets* are now *Permissions.Keys* and *Permissions.Secrets*</span></span>
* <span data-ttu-id="a0d20-161">Alguns dos Olá retornam alterações de tipos de toohello plano de controle também se aplicam.</span><span class="sxs-lookup"><span data-stu-id="a0d20-161">Some of hello return types changes apply toohello control-plane as well.</span></span>

## <a name="microsoftazurekeyvaultextensions-nuget"></a><span data-ttu-id="a0d20-162">Microsoft.Azure.KeyVault.Extensions NuGet</span><span class="sxs-lookup"><span data-stu-id="a0d20-162">Microsoft.Azure.KeyVault.Extensions NuGet</span></span>

* <span data-ttu-id="a0d20-163">pacote de saudação é quebrada muito**Microsoft.Azure.KeyVault.Extensions** e **Microsoft.Azure.KeyVault.Cryptography** para operações de criptografia de saudação.</span><span class="sxs-lookup"><span data-stu-id="a0d20-163">hello package is broken up too**Microsoft.Azure.KeyVault.Extensions** and **Microsoft.Azure.KeyVault.Cryptography** for hello cryptography operations.</span></span>

