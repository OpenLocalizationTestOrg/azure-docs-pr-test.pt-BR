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
# <a name="azure-key-vault-net-20---release-notes-and-migration-guide"></a>.NET 2.0 para Cofre de Chaves do Azure - Notas de versão e guia de migração
Olá notas e diretrizes a seguir são para desenvolvedores que trabalham com Azure Key Vault .NET / biblioteca C#. Em transição de saudação do toohello 2.0 versão da saudação 1.0, um número de atualizações foram feito que exigem trabalho de migração em seu código para que você toobenefit das melhorias funcionais hello e adições de recursos, como **Cofre de chaves certificados** suporte.

## <a name="key-vault-certificates"></a>Certificados do Key Vault

Fornece suporte de certificados de Cofre de chaves para o gerenciamento de seu x509 certificados e hello comportamentos a seguir:  

* Um toocreate de proprietário do certificado permite que um certificado por meio de um processo de criação de Cofre de chaves ou importação de saudação de um certificado existente. Isso inclui certificados autoassinados e gerados por Autoridades de Certificação.
* Permite que um proprietário de certificados de Cofre de chaves tooimplement de armazenamento seguro e o gerenciamento de X509 certificados sem interação com o material da chave privada.  
* Permite um toocreate de proprietário do certificado em uma política que direciona o Cofre de chaves toomanage Olá ciclo de vida de um certificado.  
* Permite que os proprietários de certificado tooprovide informações de contato para a notificação sobre eventos de ciclo de vida de expiração e renovação de certificado.  
* Oferece suporte à renovação automática com emissores selecionados - provedores de certificado X509/autoridades de certificação parceiros do Cofre de Chaves.
  
  * Observação: provedores não têm parcerias/autoridades também são permitidas, mas, não dará suporte a recurso de renovação automática hello.

## <a name="net-support"></a>Suporte ao .NET

* **.NET 4.0** não tem suporte pela versão de hello 2.0 do hello Azure Key Vault .NET / biblioteca c#
* **.NET core** é compatível com a versão Olá 2.0 de hello Azure Key Vault .NET / biblioteca c#

## <a name="namespaces"></a>Namespaces

* Olá namespace **modelos** é alterado de **Microsoft.Azure.KeyVault** muito**Microsoft.Azure.KeyVault.Models**.
* Olá **Microsoft.Azure.KeyVault.Internal** namespace é descartado.
* namespace de dependências do SDK do Azure Olá são alterados de **Hyak.Common** e **Hyak.Common.Internals** muito**Microsoft.Rest** e  **Microsoft.Rest.Serialization**

## <a name="type-changes"></a>Alterações de tipo

* *Segredo* alterada muito*SecretBundle*
* *Dicionário* alterada muito*IDictionary*
* *Lista<T>, string []* alterada muito*IList<T>*
* *NextList* alterada muito *NextPageLink*

## <a name="return-types"></a>Tipos de retorno

* **KeyList** e **SecretList** retornarão *IPage<T>* em vez de *ListKeysResponseMessage*
* Olá gerado **BackupKeyAsync** retornará *BackupKeyResult* que contém *valor* (blob de backup). Antes de saudação método foi encapsulado e retornando valor Olá somente.

## <a name="exceptions"></a>Exceções

* *KeyVaultClientException* é alterada muito*KeyVaultErrorException*
* Erro do serviço de saudação é alterado de *exceção. Erro* muito*exceção. Body.Error.Message*.
* Removido informações adicionais da mensagem de erro Olá para **[JsonExtensionData]**.

## <a name="constructors"></a>Construtores

* Em vez de aceitar um *HttpClient* como um argumento de construtor, construtor de saudação aceita apenas *HttpClientHandler* ou *DelegatingHandler []*.

## <a name="downloaded-packages"></a>Pacotes baixados

Quando um cliente está processando uma dependência no seguinte de saudação do Cofre de chaves foram baixados

### <a name="previous-package-list"></a>Lista de pacotes anterior

* id do pacote="Hyak.Common" versão="1.0.2" targetFramework="net45"
* id do pacote="Microsoft.Azure.Common" versão="2.0.4" targetFramework="net45"
* id do pacote="Microsoft.Azure.Common.Dependencies" versão="1.0.0" targetFramework="net45"
* id do pacote="Microsoft.Azure.KeyVault" versão="1.0.0" targetFramework="net45"
* id do pacote="Microsoft.Bcl" versão="1.1.9" targetFramework="net45"
* id do pacote="Microsoft.Bcl.Async" versão="1.0.168" targetFramework="net45"
* id do pacote="Microsoft.Bcl.Build" version="1.0.14" targetFramework="net45"
* id do pacote="Microsoft.Net.Http" versão="2.2.22" targetFramework="net45"

### <a name="current-package-list"></a>Lista atual de pacotes

* id do pacote="Microsoft.Azure.KeyVault" versão="2.0.0-preview" targetFramework="net45"
* id do pacote="Microsoft.Rest.ClientRuntime" versão="2.2.0" targetFramework="net45"
* id do pacote="Microsoft.Rest.ClientRuntime.Azure" versão="3.2.0" targetFramework="net45"

## <a name="class-changes"></a>Alterações de classe

* A classe **UnixEpoch** foi removida
* **Base64UrlConverter** classe é renomeada muito**Base64UrlJsonConverter**

## <a name="other-changes"></a>Outras alterações

* Foi adicionado suporte para configuração de saudação da política de repetição de operação KV em falhas transitórias toothis versão da API de saudação.

## <a name="microsoftazuremanagementkeyvault-nuget"></a>Microsoft.Azure.Management.KeyVault NuGet

* Para operações de saudação que retornaram um *cofre*, tipo de retorno de saudação foi uma classe que continha uma propriedade de cofre. Olá tipo de retorno é agora *cofre*.
* *PermissionsToKeys* e *PermissionsToSecrets* agora são *Permissions.Keys* e *Permissions.Secrets*
* Alguns dos Olá retornam alterações de tipos de toohello plano de controle também se aplicam.

## <a name="microsoftazurekeyvaultextensions-nuget"></a>Microsoft.Azure.KeyVault.Extensions NuGet

* pacote de saudação é quebrada muito**Microsoft.Azure.KeyVault.Extensions** e **Microsoft.Azure.KeyVault.Cryptography** para operações de criptografia de saudação.

