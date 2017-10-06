---
title: "códigos de erro de serviços de mídia aaaAzure | Microsoft Docs"
description: "tópico de saudação fornece uma visão geral dos códigos de erro do Azure Media Services."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: d3a62a64-7608-4b17-8667-479b26ba0d6c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: de1ffd6dee8901a3051eb5032536c3669482d6b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-error-codes"></a>Códigos de erro dos Serviços de Mídia do Azure
Ao usar o Microsoft Azure Media Services, você pode receber códigos de erro HTTP de serviço Olá dependendo de problemas, como tokens de autenticação expirando tooactions que não têm suporte nos serviços de mídia. Olá, esta é uma lista de **códigos de erro HTTP** que podem ser retornados por serviços de mídia e Olá possível causa para eles.  

## <a name="400-bad-request"></a>400 Solicitação Inválida
contém informações inválidas de solicitação de saudação e é rejeitada devida tooone de saudação motivos a seguir:

* Uma versão de API incompatível foi especificada. Para a versão mais atual do hello, consulte [instalação para desenvolvimento de API de REST de serviços de mídia](media-services-rest-how-to-use.md).
* versão de API de saudação do Media Services não está especificado. Para obter informações sobre como toospecify Olá versão da API, consulte [referência de API REST do Media Services operações](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference).
  
  > [!NOTE]
  > Se você estiver usando tooMedia de tooconnect .NET ou Java SDKs Olá serviços, Olá versão da API é especificado para que você sempre que você tente e executa alguma ação em relação aos serviços de mídia.
  > 
  > 
* Uma propriedade indefinida foi especificada. é o nome da propriedade Olá na mensagem de erro de saudação. Somente as propriedades que são membros de uma determinada entidade podem ser especificadas. Confira [Azure Media Services REST API Reference](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference) (Referência da API REST dos Serviços de Mídia do Azure) para obter uma lista de entidades e suas propriedades.
* Um valor de propriedade inválido foi especificado. é o nome da propriedade Olá na mensagem de erro de saudação. Consulte o link anterior de saudação para tipos de propriedade válidos e seus valores.
* Um valor de propriedade está ausente e é obrigatório.
* Parte da URL de saudação especificado contém um valor incorreto.
* Uma tentativa foi feita tooupdate uma propriedade WriteOnce.
* Uma tentativa foi feita toocreate um trabalho que tem um ativo de entrada com um AssetFile primário que não foi especificado ou não pôde ser determinado.
* Uma tentativa foi feita tooupdate um localizador SAS. Localizadores SAS só podem ser criados ou excluídos. Os localizadores de streaming podem ser atualizados. Para saber mais, confira [Locators](https://docs.microsoft.com/rest/api/media/operations/locator) (Localizadores).
* Uma operação ou consulta sem suporte foi enviada.

## <a name="401-unauthorized"></a>401 Não Autorizado
solicitação de saudação não pôde ser autenticada (antes de poder ser autorizado) tooone vencimento de saudação motivos a seguir:

* Cabeçalho de autenticação ausente.
* Valor do cabeçalho de autenticação inválido.
  * Olá token tiver expirado. 
  * token de saudação contém uma assinatura inválida.

## <a name="403-forbidden"></a>403 Proibido
não é permitido devida Olá solicitação tooone de saudação motivos a seguir:

* Olá conta do Media Services não foi encontrado ou foi excluído.
* Olá conta do Media Services está desabilitado e o tipo de solicitação Olá não HTTP GET. As operações de serviço também retornarão uma resposta 403.
* Olá token de autenticação não contém informações de credenciais do usuário Olá: AccountName e/ou SubscriptionId. Você pode encontrar essas informações no hello extensão de interface de usuário de serviços de mídia para sua conta de serviços de mídia no hello Portal de gerenciamento.
* Olá recurso não pode ser acessado.
  
  * Uma tentativa foi feita toouse um MediaProcessor que não está disponível para sua conta de serviços de mídia.
  * Foi feita uma tentativa tooupdate um JobTemplate definido pelos serviços de mídia.
  * Uma tentativa foi feita toooverwrite localizador de alguns outros serviços de mídia da conta.
  * Uma tentativa foi feita toooverwrite ContentKey alguns outros serviços de mídia da conta.
* não foi possível criar o recurso Olá devido a cota de serviço tooa foi atingida para a conta de serviços de mídia hello. Para obter mais informações sobre cotas de serviço hello, consulte [cotas e limitações](media-services-quotas-and-limitations.md).

## <a name="404-not-found"></a>404 Não Encontrado
solicitação de saudação não é permitida em um recurso de vencimento tooone de saudação motivos a seguir:

* Uma tentativa foi feita tooupdate uma entidade que não existe.
* Uma tentativa foi feita toodelete uma entidade que não existe.
* Uma tentativa foi feita toocreate uma entidade que vincula tooan entidade que não existe.
* Uma tentativa foi feita tooGET uma entidade que não existe.
* Uma tentativa foi feita toospecify uma conta de armazenamento que não está associada a saudação conta do Media Services.  

## <a name="409-conflict"></a>409 Conflito
não é permitido devida Olá solicitação tooone de saudação motivos a seguir:

* Mais de um AssetFile tem nome de especificado hello dentro Olá ativo.
* Foi feita uma tentativa toocreate uma segunda primário AssetFile dentro Olá ativo.
* Foi feita uma tentativa toocreate um ContentKey com hello especificado Id já foi usado.
* Foi feita uma tentativa toocreate um localizador com hello especificado Id já foi usado.
* Mais de um IngestManifestFile com nome especificado de hello dentro Olá IngestManifest.
* Uma tentativa foi feita toolink um segundo toohello de ContentKey de criptografia de armazenamento ativos criptografados de armazenamento.
* Foi feita uma tentativa toolink Olá mesmo ContentKey toohello ativo.
* Uma tentativa foi feita toocreate tooan um localizador ativo cujo contêiner de armazenamento está ausente ou não está mais associado Olá ativo.
* Uma tentativa foi feita toocreate tooan um localizador ativo que já tem 5 localizadores em uso. (Armazenamento do azure impõe o limite de saudação de cinco políticas de acesso compartilhado em um contêiner de armazenamento.)
* Conta de armazenamento de um ativo de tooan IngestManifestAsset de vinculação não é Olá mesmo que a conta de armazenamento Olá usado pelo pai Olá IngestManifest.  

## <a name="500-internal-server-error"></a>500 Erro Interno do Servidor
Durante o processamento de saudação da solicitação hello, os serviços de mídia encontrar algum erro que impede o processamento de saudação de continuar. Isso pode ter ocorrido tooone de saudação motivos a seguir:

* Falha na criação de um trabalho ou ativo porque as informações de cota de serviço da conta de serviços de mídia hello estão temporariamente indisponíveis.
* Falha na criação de um contêiner de armazenamento de blob do ativo ou IngestManifest porque as informações de conta de armazenamento da conta hello estão temporariamente indisponíveis.
* Outro erro inesperado.

## <a name="503-service-unavailable"></a>503 Serviço Indisponível
servidor de saudação é solicitações tooreceive atualmente não é possível. Esse erro pode ser causado pelo serviço de toohello solicitações excessivas. Mecanismo de limitação de serviços de mídia restringe o uso de recursos de saudação para aplicativos que fazem o serviço de toohello solicitações excessivas.

> [!NOTE]
> Seleção Olá erro mensagem e erro código cadeia de caracteres tooget informações mais detalhadas sobre o motivo da saudação você obteve Olá erro 503. Esse erro nem sempre significa limitação.
> 
> 

As possíveis descrições de status são:

* "O servidor está ocupado. As execuções anteriores desse tipo de solicitação demoraram mais de {0} segundos."
* "O servidor está ocupado. Mais de {0} solicitações por segundo podem ser limitadas."
* "O servidor está ocupado. Mais de {0} solicitações em {1} segundos podem ser limitadas."

toohandle esse erro, é recomendável usar a lógica de repetição de retirada exponencial. Isso significa usar esperas mais longas progressivamente entre as repetições de respostas de erro consecutivas.  Para saber mais, confira [Transient Fault Handling Application Block](https://msdn.microsoft.com/library/hh680905.aspx) (Bloco de aplicativos para manipulação de falha transitória).

> [!NOTE]
> Se você estiver usando [SDK de serviços de mídia do Azure para .net](https://github.com/Azure/azure-sdk-for-media-services/tree/master), lógica de repetição Olá para erro Olá 503 foi implementada por Olá SDK.  
> 
> 

## <a name="see-also"></a>Consulte também
[Códigos de erro do gerenciamento dos Serviços de Mídia](http://msdn.microsoft.com/library/windowsazure/dn167016.aspx)

## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

