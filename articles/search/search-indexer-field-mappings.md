---
title: mapeamentos de aaaField em indexadores de pesquisa do Azure
description: "Configurar tooaccount de mapeamentos de campo de indexador de pesquisa do Azure diferenças em representações de dados e nomes de campo"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 0325a4de-0190-4dd5-a64d-4e56601d973b
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: eugenesh
ms.openlocfilehash: 009d5dbc12cb9e8d9cfd3e8042e907ca88399ad7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="field-mappings-in-azure-search-indexers"></a>Mapeamentos de campo em indexadores do Azure Search
Ao usar indexadores de pesquisa do Azure, você pode encontrar por conta própria, ocasionalmente, em situações em que seus dados de entrada não correspondem bastante esquema de saudação do índice de destino. Nesses casos, você pode usar **mapeamentos de campo** tootransform forma desejada do hello seus dados.

Algumas situações em que os mapeamentos de campo são úteis:

* A fonte de dados tem um campo `_id`, mas a Pesquisa do Azure não permite nomes de campo iniciados com um sublinhado. Um mapeamento de campo permite que você muito "Renomear" um campo.
* Você deseja toopopulate Olá vários campos de índice com hello dados, por exemplo, de fonte de dados mesmo porque deseja tooapply analisadores diferentes toothose campos. Mapeamentos de campo permitem a “bifurcação” de um campo de fonte de dados.
* Você precisa tooBase64 codificar ou decodificar dados. Mapeamentos de campo dão suporte a diversas **funções de mapeamento**, incluindo funções para codificação e decodificação Base64.   

## <a name="setting-up-field-mappings"></a>Configurar mapeamentos de campo
Você pode adicionar mapeamentos de campo ao criar um novo indexador usando Olá [criar indexador](https://msdn.microsoft.com/library/azure/dn946899.aspx) API. Você pode gerenciar mapeamentos de campo em um indexador de indexação usando Olá [atualização indexador](https://msdn.microsoft.com/library/azure/dn946892.aspx) API.

Um mapeamento de campo consiste em 3 partes:

1. Um `sourceFieldName`, que representa um campo na fonte de dados. Essa propriedade é obrigatória.
2. Um `targetFieldName`opcional, que representa um campo em seu índice de pesquisa. Se omitido, Olá o mesmo nome no hello fonte de dados é usada.
3. Um `mappingFunction`opcional, que pode transformar seus dados usando uma das várias funções predefinidas. Olá a lista completa de funções [abaixo](#mappingFunctions).

Mapeamentos de campos são adicionados toohello `fieldMappings` matriz na definição do indexador hello.

Por exemplo, veja como você pode acomodar as diferenças nos nomes de campo:

```JSON

PUT https://[service name].search.windows.net/indexers/myindexer?api-version=[api-version]
Content-Type: application/json
api-key: [admin key]
{
    "dataSourceName" : "mydatasource",
    "targetIndexName" : "myindex",
    "fieldMappings" : [ { "sourceFieldName" : "_id", "targetFieldName" : "id" } ]
}
```

Um indexador pode ter vários mapeamentos de campo. Por exemplo, aqui está como você pode "bifurcar" um campo:

```JSON

"fieldMappings" : [
    { "sourceFieldName" : "text", "targetFieldName" : "textStandardEnglishAnalyzer" },
    { "sourceFieldName" : "text", "targetFieldName" : "textSoundexAnalyzer" },
]
```

> [!NOTE]
> Pesquisa do Azure usa a comparação diferencia maiusculas de minúsculas tooresolve Olá função nomes do campo e os mapeamentos de campo. Isso é prático (você não tem tooget todas as caixas de saudação à direita), mas isso significa que a fonte de dados ou índice não pode ter campos que diferenciam somente maiusculas e minúsculas.  
>
>

<a name="mappingFunctions"></a>

## <a name="field-mapping-functions"></a>Funções de mapeamento de campo
Essas funções atualmente têm suporte:

* [base64Encode](#base64EncodeFunction)
* [base64Decode](#base64DecodeFunction)
* [extractTokenAtPosition](#extractTokenAtPositionFunction)
* [jsonArrayToStringCollection](#jsonArrayToStringCollectionFunction)

<a name="base64EncodeFunction"></a>

### <a name="base64encode"></a>base64Encode
Executa *URL segura* codificação Base64 de saudação de cadeia de caracteres de entrada. Pressupõe que a entrada hello está codificado com UTF-8.

#### <a name="sample-use-case"></a>Casos de uso de exemplo
Somente caracteres de URL seguro podem aparecer em uma chave de documento da pesquisa do Azure (como os clientes devem ser capaz de tooaddress documento de hello usando Olá API de pesquisa, por exemplo). Se seus dados contiverem caracteres não seguros URL e você quiser toouse-toopopulate um campo de chave em seu índice de pesquisa, usar essa função.   

#### <a name="example"></a>Exemplo
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "Path",
    "targetFieldName" : "UrlSafePath",
    "mappingFunction" : { "name" : "base64Encode" }
  }]
```

<a name="base64DecodeFunction"></a>

### <a name="base64decode"></a>base64Decode
Executa a decodificação de Base64 da cadeia de caracteres de entrada hello. Olá entrada será considerada tooa *URL segura* cadeia de caracteres codificada em Base64.

#### <a name="sample-use-case"></a>Casos de uso de exemplo
Valores de metadados personalizados de blob devem ser codificados em ASCII. Você pode usar Base64 codificação toorepresent arbitrárias cadeias de caracteres Unicode nos metadados de blob personalizado. No entanto, pesquisa toomake significativa, você pode usar essas função tooturn Olá codificado dados novamente em cadeias de caracteres "normais" ao popular o índice de pesquisa.  

#### <a name="example"></a>Exemplo
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "Base64EncodedMetadata",
    "targetFieldName" : "SearchableMetadata",
    "mappingFunction" : { "name" : "base64Decode" }
  }]
```

<a name="extractTokenAtPositionFunction"></a>

### <a name="extracttokenatposition"></a>extractTokenAtPosition
Divisões de um campo de cadeia de caracteres usando Olá especificado delimitador e escolhe Olá token no hello posição especificada na divisão resultante hello.

Por exemplo, se hello entrada é `Jane Doe`, Olá `delimiter` é `" "`(espaço) e hello `position` é 0, o resultado de saudação é `Jane`; se hello `position` é 1, Olá resultado é `Doe`. Se a posição Olá refere-se o token tooa que não existe, um erro será retornado.

#### <a name="sample-use-case"></a>Casos de uso de exemplo
A fonte de dados contiver uma `PersonName` campo e você quiser tooindex como dois separado `FirstName` e `LastName` campos. Você pode usar este Olá toosplit de função usando o caractere de espaço Olá Olá delimitador de entrada.

#### <a name="parameters"></a>parâmetros
* `delimiter`: toouse uma cadeia de caracteres como separador de saudação ao dividir Olá a cadeia de caracteres de entrada.
* `position`: uma posição de base zero de inteiro de saudação toopick de token após a cadeia de caracteres de entrada hello está dividida.    

#### <a name="example"></a>Exemplo
```JSON

"fieldMappings" : [
  {
    "sourceFieldName" : "PersonName",
    "targetFieldName" : "FirstName",
    "mappingFunction" : { "name" : "extractTokenAtPosition", "parameters" : { "delimiter" : " ", "position" : 0 } }
  },
  {
    "sourceFieldName" : "PersonName",
    "targetFieldName" : "LastName",
    "mappingFunction" : { "name" : "extractTokenAtPosition", "parameters" : { "delimiter" : " ", "position" : 1 } }
  }]
```

<a name="jsonArrayToStringCollectionFunction"></a>

### <a name="jsonarraytostringcollection"></a>jsonArrayToStringCollection
Transformações de uma cadeia de caracteres formatada como uma matriz JSON de cadeias de caracteres em uma matriz de cadeia de caracteres que pode ser usado toopopulate um `Collection(Edm.String)` campo no índice de saudação.

Por exemplo, se a cadeia de caracteres de entrada hello está `["red", "white", "blue"]`, e o campo de destino de saudação do tipo `Collection(Edm.String)` será preenchida com valores hello três `red`, `white` e `blue`. Para valores de entrada que não podem ser analisados como matrizes de cadeia de caracteres JSON, um erro será retornado.

#### <a name="sample-use-case"></a>Casos de uso de exemplo
Banco de dados SQL do Azure não tem um tipo de dados interno que naturalmente mapeia muito`Collection(Edm.String)` campos na pesquisa do Azure. toopopulate campos da coleção de cadeia de caracteres, formate sua fonte de dados como uma matriz de cadeia de caracteres JSON e usar essa função.

#### <a name="example"></a>Exemplo
```JSON

"fieldMappings" : [
  { "sourceFieldName" : "tags", "mappingFunction" : { "name" : "jsonArrayToStringCollection" } }
]
```

## <a name="help-us-make-azure-search-better"></a>Ajude-nos a aprimorar o Azure Search
Se você tiver solicitações de recursos ou ideias para melhorias, entre em contato toous em nosso [site UserVoice](https://feedback.azure.com/forums/263029-azure-search/).
