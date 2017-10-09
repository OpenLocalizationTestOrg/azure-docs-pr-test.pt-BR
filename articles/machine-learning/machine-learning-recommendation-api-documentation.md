---
title: "aaaMachine documentação da API do aprendizado recomendações | Microsoft Docs"
description: "Documentação da API de recomendações de aprendizado de máquina do Azure para um mecanismo de recomendações disponível no Microsoft Azure Marketplace de saudação."
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 32c3ab2f-fdd7-48cc-b501-ad55c79b87dc
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: LuisCa
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: d1cec228bf23870c05c8ab8df2779b0c3c65b06d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations-api-documentation"></a>Documentação da API de Recomendações do Azure Machine Learning
> [!NOTE]
> Deve começar a usar o hello recomendações API cognitivas serviço em vez de nesta versão. Olá serviço cognitivas recomendações será substituído por esse serviço e todos os novos recursos de saudação serão desenvolvidos existe. Ele possui novos recursos como suporte ao processamento em lotes, um Gerenciador de API aprimorado, uma superfície de API mais limpa, uma experiência de inscrição/cobrança mais consistente etc.
> Saiba mais sobre [toohello migrando novo serviço cognitivas](http://aka.ms/recomigrate)
> 
> 

Este documento descreve as APIs de Recomendações do Microsoft Azure Machine Learning.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a>1. Visão geral
Este documento é uma referência para a API. Você deve começar com o documento de "Azure Machine Learning recomendação – início rápido" hello.

Olá API de recomendações de aprendizado de máquina do Azure pode ser dividido em Olá seguintes grupos lógicos:

* <ins>Limitações</ins> - limitações da API de recomendações.
* <ins>Informações gerais</ins> -informações sobre autenticação, controle de versão e URI de serviço.
* <ins>Modelo Basic</ins> -APIs que permitem operações básicas do toodo Olá no modelo (por exemplo, criar, atualizar e excluir um modelo).
* <ins>Modelo avançado</ins> -APIs que permitem que você tooget avançado análises de dados no modelo de saudação.
* <ins>Modelo de regras de negócio</ins> -APIs que permitem a você as regras de negócio toomanage nos resultados de recomendação de modelo hello.
* <ins>Catálogo</ins> -APIs que permitem operações básicas de toodo em um catálogo de modelo. Um catálogo contém informações de metadados sobre itens Olá Olá de dados de uso.
* <ins>Recurso</ins> -APIs que permitem insights tooget no item no catálogo hello e como toouse esse melhores recomendações toobuild informações.
* <ins>Dados de uso</ins> -APIs que permitem operações básicas de toodo nos dados de uso do modelo de saudação. Dados de uso no formato básico Olá consistem em linhas que incluem pares de &#60; userId &#62; &#60; itemId &#62;.
* <ins>Criar</ins> - criar APIs que permitem que você tootrigger um modelo e façam operações básicas que são relacionadas toothis compilar. Você pode iniciar uma compilação de modelo uma vez que você tenha dados de uso valiosos.
* <ins>Recomendação</ins> -APIs que permitem a você recomendações tooconsume depois que termina de compilação de saudação de um modelo.
* <ins>Dados de usuário</ins> -APIs que permitem a você informações toofetch nos dados de uso do usuário hello.
* <ins>Notificações</ins> -APIs que permitem que você tooreceive notificações sobre problemas relacionados a operações tooyour API. (Por exemplo, você estiver relatando dados de uso por meio de aquisição de dados e a maioria dos eventos de saudação processamento estão falhando. Uma notificação de erro será gerada.)

## <a name="2-limitations"></a>2. Limitações
* número máximo de saudação de modelos por assinatura é 10.
* Olá o número máximo de compilações por modelo é 20.
* número máximo de saudação de itens que pode conter um catálogo é 100.000.
* número máximo de saudação de pontos de uso que são mantidos é ~ 5.000.000. Olá mais antigo será excluído se novas serão carregadas ou relatadas.
* tamanho máximo de saudação de dados que podem ser enviados no POST (por exemplo, importar dados de catálogo, importar dados de uso) é de 200MB.
* número máximo de saudação de itens que podem ser feitas para a obtenção de recomendações é 150.

## <a name="3-apis---general-information"></a>3. APIs – Informações Gerais
### <a name="31-authentication"></a>3.1. Autenticação
Siga as diretrizes do Microsoft Azure Marketplace Olá sobre a autenticação. marketplace Olá dá suporte a um método de autenticação de Basic ou OAuth do hello.

### <a name="32-service-uri"></a>3.2. URI de serviço
Olá URI raiz do serviço para Olá APIs de recomendações de aprendizado de máquina do Azure é [aqui.](https://api.datamarket.azure.com/amla/recommendations/v3/)

URI do serviço completo Olá é expressa usando elementos da especificação de OData hello.  

### <a name="33-api-version"></a>3.3. Versão da API
Cada chamada de API terá, no final do hello, um parâmetro de consulta chamado apiVersion too1.0 deve ser definido.

### <a name="34-ids-are-case-sensitive"></a>3.4. IDs diferenciam minúsculas e maiúsculas
IDs, retornados por qualquer Olá APIs, diferenciam maiusculas de minúsculas e devem ser usadas como tal quando passados como parâmetros em chamadas API subsequentes. Por exemplo, IDS d modelo e de catálogo diferenciam maiúsculas de minúsculas.

## <a name="4-recommendations-quality-and-cold-items"></a>4. Qualidade das recomendações e itens frios
### <a name="41-recommendation-quality"></a>4.1. Qualidade da recomendação
Criar um modelo de recomendação é geralmente suficiente recomendações de tooprovide tooallow Olá sistema. No entanto, qualidade da recomendação varia com base no uso de saudação processado e Olá cobertura do catálogo de saudação. Por exemplo se você tiver muitos itens frios (sem uso significativo de itens), o sistema de saudação terão dificuldade para fornecer uma recomendação de tal um item ou usando um item tal como recomendado. No item frios problema na ordem tooovercome hello, sistema Olá permite o uso de saudação de metadados de recomendações de Olá Olá itens tooenhance. Esses metadados são chamados tooas recursos. Os recursos mais comuns são o autor de um livro ou um ator de um filme. Recursos são fornecidos por meio do catálogo de saudação na forma de saudação de cadeias de caracteres de chave/valor. Para o formato completo Olá Olá do arquivo de catálogo, consulte toohello [importar seção catálogo](#81-import-catalog-data). 

### <a name="42-rank-build"></a>4.2. Compilação de classificação
Recursos podem aprimorar o modelo de recomendação hello, mas toodo assim requer o uso de saudação do recursos significativos. Uma nova compilação foi apresentada para essa finalidade: uma compilação de classificação. Esta compilação será a classificação da utilidade de saudação de recursos. Um recurso significativo é um recurso com uma pontuação de classificação 2 ou maior.
Depois de entender quais recursos de saudação são significativos, disparar um build de recomendação com lista hello (ou sublista) dos recursos significativos. É possível toouse que esses recursos para o aprimoramento de saudação do passivos itens e itens frios. Em ordem toouse-los para itens passivos, Olá `UseFeatureInModel` parâmetro de compilação deve ser configurado. Em ordem toouse de recursos para itens frios, Olá `AllowColdItemPlacement` parâmetro de compilação deve ser habilitado.
Observação: Não é possível tooenable `AllowColdItemPlacement` sem habilitar `UseFeatureInModel`.

### <a name="43-recommendation-reasoning"></a>4.3. Raciocínio de recomendação
O raciocínio de recomendação é outro aspecto do uso de recursos. Na verdade, o mecanismo de recomendações de aprendizado de máquina do Azure de saudação pode usar explicações de recomendação de tooprovide de recursos (também conhecido como raciocínio), à esquerda toomore confiança no hello recomendado item do consumidor de recomendação de saudação.
tooenable raciocínio, hello `AllowFeatureCorrelation` e `ReasoningFeatureList` parâmetros devem ser toorequesting antes da instalação uma compilação de recomendação.

## <a name="5-model-basic"></a>5. Modelo Básico
### <a name="51-create-model"></a>5.1. Criar modelo
Cria uma solicitação "criar modelo".

| Método HTTP | URI |
|:--- |:--- |
| POST |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| modelName |São permitidos apenas letras (A-Z, a-z), números (0-9), hifens (-) e sublinhado (_).<br>Comprimento máximo: 20 |
| apiVersion |1.0 |
|  | |
| Corpo da solicitação |NENHUM |

**Resposta**:

Código de status HTTP: 200

* `feed/entry/content/properties/id`-Contém a ID do modelo hello.
  **Observação**: a ID do modelo diferencia maiúsculas de minúsculas.

XML de OData

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Create A New Model</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:35:21Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">CreateANewModelEntity2</title>
    <updated>2014-10-05T06:35:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">a658c626-2baa-43a7-ac98-f6ee26120a12</d:Id>
        <d:Name m:type="Edm.String">MyFirstModel</d:Name>
        <d:Date m:type="Edm.String">10/5/2014 6:35:19 AM</d:Date>
        <d:Status m:type="Edm.String">Created</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:UserName>
        <d:Description m:type="Edm.String"></d:Description>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="52-get-model"></a>5.2. Obter modelo
Criar uma solicitação “obter modelo".

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br>Exemplo:<br>`<rootURI>/GetModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| ID |Identificador exclusivo do modelo de saudação (com distinção entre maiusculas e minúsculas) |
| apiVersion |1.0 |
|  | |
| Corpo da solicitação |NENHUM |

**Resposta**:

Código de status HTTP: 200

dados de modelo de saudação podem ser encontrados em Olá elementos a seguir:

* `feed/entry/content/properties/Id` - ID exclusivo do modelo.
* `feed/entry/content/properties/Name` - Nome do modelo.
* `feed/entry/content/properties/Date` - Data de criação do modelo.
* `feed/entry/content/properties/Status` - Status do modelo. Um dos seguintes hello:
  * Criado - O modelo é criado e não contém Catálogo e Uso.
  * ReadyForBuild - O modelo é criado e contém Catálogo e Uso.
* `feed/entry/content/properties/HasActiveBuild`-Indica se o modelo de saudação foi criado com êxito.
* `feed/entry/content/properties/BuildId` - ID da compilação ativa do modelo.
* `feed/entry/content/properties/Mpr` - Classificação porcentual média do modelo (MPR - consulte ModelInsight para obter mais informações).
* `feed/entry/content/properties/UserName` - Nome do usuário interno do modelo.

XML de OData

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get A List Of All Models</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T14:35:51Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
        <d:Name m:type="Edm.String">vah-11111</d:Name>
        <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
        <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
        <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
        <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
        <d:Description m:type="Edm.String">short description</d:Description>
        <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="53----get-all-models"></a>5.3.    Obter todos os modelos
Recupera todos os modelos do usuário atual hello.

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetAllModels?apiVersion=%271.0%27`<br>Exemplo:<br>`<rootURI>/GetAllModels?apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| apiVersion |1.0 |
|  | |
| Corpo da solicitação |NENHUM |

**Resposta**:

Código de status HTTP: 200

* `feed/entry/content/properties/Id` - ID exclusivo do modelo.
* `feed/entry/content/properties/Name` - Nome do modelo.
* `feed/entry/content/properties/Date` - Data de criação do modelo.
* `feed/entry/content/properties/Status` - Status do modelo. Um dos seguintes hello:
  * Criado - O modelo é criado e não contém Catálogo e Uso.
  * ReadyForBuild - O modelo é criado e contém Catálogo e Uso.
* `feed/entry/content/properties/HasActiveBuild`-Indica se o modelo de saudação foi criado com êxito.
* `feed/entry/content/properties/BuildId` - ID da compilação ativa do modelo.
* `feed/entry/content/properties/Mpr` - MPR do modelo MPR (consulte o ModelInsight para obter mais informações).
* `feed/entry/content/properties/UserName` - Nome do usuário interno do modelo.
* `feed/entry/content/properties/UsageFileNames` - Lista de arquivos de uso do modelo separados por vírgula.
* `feed/entry/content/properties/CatalogId` - ID do catálogo do modelo.
* `feed/entry/content/properties/Description` - Descrição do modelo.
* `feed/entry/content/properties/CatalogFileName` - Nome do arquivo do catálogo do modelo.

XML de OData

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get A List Of All Models</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-28T14:35:51Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
                    <d:Name m:type="Edm.String">vah-11111</d:Name>
                    <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
                    <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
                    <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
                    <d:BuildId m:type="Edm.String">-1</d:BuildId>
                    <d:Mpr m:type="Edm.String">0</d:Mpr>
                    <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
                    <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
                    <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
                    <d:Description m:type="Edm.String">short description</d:Description>
                    <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="54----update-model"></a>5.4.    Atualizar modelo
Você pode atualizar a descrição do modelo hello ou Olá ID do ativo de compilação.<br>
<ins>ID de compilação ativa</ins> – cada compilação para cada modelo tem uma ID de compilação. ID de compilação active Olá é Olá primeira compilação bem-sucedida cada novo modelo. Depois que você tiver uma ID de ativo de compilação e fazer compilações adicionais para Olá mesmo modelo, você precisa tooexplicitly defini-lo hello padrão criar ID se desejar. Quando você consome recomendações, se você não especificar a ID de compilação de saudação que você deseja toouse, padrão Olá um será usado automaticamente.<br>
Esse mecanismo permite que você - depois de um modelo de recomendação em produção - toobuild novos modelos e testá-las antes de promovê-los tooproduction.

| Método HTTP | URI |
|:--- |:--- |
| PUT |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br>Exemplo:<br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| ID |Identificador exclusivo do modelo de saudação (com distinção entre maiusculas e minúsculas) |
| apiVersion |1.0 |
|  | |
| Corpo da solicitação |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`<Description>New Description</Description>`<br>`<ActiveBuildId>-1</ActiveBuildId>`<br>` </ModelUpdateParams>`<br><br>Observe que a descrição de marcas Olá XML e ActiveBuildId são opcionais. Se você não quiser tooset descrição ou ActiveBuildId, remova a marca de inteiro de hello. |

**Resposta**:

Código de status HTTP: 200

### <a name="55----delete-model"></a>5.5.    Excluir modelo
Exclui um modelo existente por ID.

| Método HTTP | URI |
|:--- |:--- |
| EXCLUIR |`<rootURI>/DeleteModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br>Exemplo:<br>`<rootURI>/DeleteModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| ID |Identificador exclusivo do modelo de saudação (com distinção entre maiusculas e minúsculas) |
| apiVersion |1.0 |
|  | |
| Corpo da solicitação |NENHUM |

**Resposta**:

Código de status HTTP: 200

XML de OData

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Delete Model by Id</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T10:39:33Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">DeleteModelByIdEntity</title>
    <updated>2014-10-28T10:39:33Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:string m:type="Edm.String"></d:string>
      </m:properties>
    </content>
      </entry>
    </feed>

## <a name="6-model-advanced"></a>6. Modelo Avançado
### <a name="61----model-data-insight"></a>6.1.    Visão de modelo de dados
Retorna dados estatísticos sobre os dados de uso Olá este modelo foi criado com.

Disponível somente para compilação de Recomendação.

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetDataInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br>Exemplo:<br>`<rootURI>/GetDataInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de saudação |
| apiVersion |1.0 |
|  | |
| Corpo da solicitação |NENHUM |

**Resposta**:

Código de status HTTP: 200

Olá dados são retornados como uma coleção de propriedades.

* `feed/entry/id/content/properties/key`-Contém o nome da propriedade hello.
* `feed/entry/id/content/properties/value`-Contém o valor da propriedade hello.

Olá tabela a seguir mostra o valor de saudação que representa cada chave.

| Chave | Descrição |
|:--- |:--- |
| AvgItemLength |Média de usuários distintos por item. |
| AvgUserLength |Média de itens distintos por usuários. |
| DensificationNumberOfItems |Número de itens após a remoção dos itens que não podem ser modelados. |
| DensificationNumberOfUsers |Número de pontos de uso após a remoção de usuários e itens que não podem ser modelados. |
| DensificationNumberOfRecords |Número de pontos de uso após a remoção de usuários e itens que não podem ser modelados. |
| MaxItemLength |Número de usuários distintos para o item mais popular hello. |
| MaxUserLength |Número máximo de itens distintos para um usuário. |
| MinItemLength |Número máximo de usuários distintos para um item. |
| MinUserLength |Número mínimo de itens distintos para um usuário. |
| RawNumberOfItems |Número de itens em arquivos de uso de saudação. |
| RawNumberOfUsers |Número de pontos de uso antes de qualquer remoção. |
| RawNumberOfRecords |Número de pontos de uso antes de qualquer remoção. |
| SamplingNumberOfItems |N/D |
| SamplingNumberOfRecords |N/D |
| SamplingNumberOfUsers |N/D |

XML de OData

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get data insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgItemLength</d:Key>
        <d:Value m:type="Edm.String">18.936</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgUserLength</d:Key>
        <d:Value m:type="Edm.String">51.879</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfItems</d:Key>
        <d:Value m:type="Edm.String">2,000</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfRecords</d:Key>
        <d:Value m:type="Edm.String">37,872</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
        <m:properties>
            <d:Key m:type="Edm.String">DensificationNumberOfUsers</d:Key>
            <d:Value m:type="Edm.String">730</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxItemLength</d:Key>
                <d:Value m:type="Edm.String">4,704</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxUserLength</d:Key>
                <d:Value m:type="Edm.String">190</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinItemLength</d:Key>
                <d:Value m:type="Edm.String">8</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinUserLength</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="62----model-insight"></a>6.2.    Percepção de modelo
Retorna informações de modelo na compilação active hello ou (se fornecida) em uma versão específica.

Disponível somente para compilação de Recomendação.

| Método HTTP | URI |
|:--- |:--- |
| GET |Com a ID de compilação ativa:<br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/GetModelInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br>Com a ID de compilação específica:<br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de saudação |
| buildId |Opcional - número que identifica uma compilação bem-sucedida. |
| apiVersion |1.0 |
|  | |
| Corpo da solicitação |NENHUM |

**Resposta**:

Código de status HTTP: 200

Olá dados são retornados como uma coleção de propriedades.

* `feed/entry/id/content/properties/key`
* `feed/entry/id/content/properties/value`

Olá tabela a seguir mostra o valor de saudação que representa cada chave.

| Chave | Descrição |
|:--- |:--- |
| CatalogCoverage |Parte do catálogo de saudação pode ser modelado com padrões de uso. rest Olá itens Olá precisará de recursos com base no conteúdo. |
| Mpr |Classificação de percentual médio de modelo de saudação. Menor é melhor. |
| NumberOfDimensions |Número de dimensões usado pelo algoritmo de fatoração Olá matriz. |

XML de OData

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get model insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">CatalogCoverage</d:Key>
                <d:Value m:type="Edm.String">1.000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">Mpr</d:Key>
                <d:Value m:type="Edm.String">0.367</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">NumberOfDimensions</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="63----get-model-sample"></a>6.3.    Obter um exemplo de modelo
Obtém uma amostra de modelo de recomendação de saudação.

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetModelSample?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br>Exemplo:<br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br>Com a ID de compilação específica:<br>`<rootURI>/GetModelSample?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27`<br>Exemplo:<br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&buildId=%271500068%27&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de saudação |
| apiVersion |1.0 |
|  | |
| Corpo da solicitação |NENHUM |

**Resposta**:

Código de status HTTP: 200

XML de OData

A resposta é retornada no formato de texto sem formatação:

<pre>
Level 1
---------------
655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel
    655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel Rating: 0.5215
    3f471802-f84f-44a0-99c8-6d2e7418eec1, Black Hawk Down: A Story of Modern War Rating: 0.5151
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5148
    6afc18e4-8c2a-43d1-9021-57543d6b11d8, Imajica Rating: 0.5146
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.514
56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai
    56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai Rating: 0.5218
    53156702-cc0c-443d-b718-6fb74b2491d3, Son of \ Rating: 0.5212
    fb8cf7a6-8719-46ee-97d4-92f931d77a3a, Smoke and Mirrors: Short Fictions and Illusions Rating: 0.5188
    8f5fe006-79e4-4679-816b-950989d1db4b, A Place I've Never Been (Contemporary American Fiction) Rating: 0.5156
    d8db4583-cc0f-49ce-bc95-b7fa3491623f, Happiness: A Novel Rating: 0.5156
50471eec-9aeb-4900-84d7-21567ab18546, If hello Buddha Dated: A Handbook for Finding Love on a Spiritual Path
    cfe922a1-7ca0-4f8d-ad9d-b7cc87bfe0ef, Divine Secrets of hello Ya-Ya Sisterhood: A Novel Rating: 0.5266
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5252
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5244
    e2cbf7ad-0636-4117-8b30-298da6df7077, Animal Dreams Rating: 0.5227
    6c818fd3-5a09-417d-9ab4-7ffe090f0fef, Confessions of an Ugly Stepsister: A Novel Rating: 0.5222
5e97148f-defb-4d74-af2d-80f4763bf531, hello Deep End of hello Ocean (Oprah's Book Club)
    5e97148f-defb-4d74-af2d-80f4763bf531, hello Deep End of hello Ocean (Oprah's Book Club) Rating: 0.537
    5dcbac37-2946-4f2a-a0b3-bbe710f9409a, Up Island: A Novel Rating: 0.5277
    bc5b69db-733b-4346-adde-3927544258f7, Downtown Rating: 0.5275
    31fe5c63-3e5a-48d0-802b-d3b0f989a634, Have a Nice Day: A Tale of Blood and Sweatsocks Rating: 0.5252
    0adf981a-b65b-4c11-b36b-78aca2f948a2, hello Perfect Storm: A True Story of Men Against hello Sea Rating: 0.5238
68f97068-ae1a-4163-9e94-396b800b743d, Modoc: hello True Story of hello Greatest Elephant That Ever Lived
    68f97068-ae1a-4163-9e94-396b800b743d, Modoc: hello True Story of hello Greatest Elephant That Ever Lived Rating: 0.5379
    6724862e-e4e7-4022-9614-1468d8b902ff, Little House on hello Prairie Rating: 0.5345
    cdedb837-1620-496d-94c4-6ccfed888320, Little House in hello Big Woods Rating: 0.5325
    382164ba-406b-4187-b726-d7a54b9d790d, hello Tao of Pooh Rating: 0.5309
    6a068d6a-bb74-4ba3-b3f2-a956c4f9d1b5, On hello Banks of Plum Creek Rating: 0.5285
37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships
    37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars, Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships Rating: 0.5397
    f2be16d4-5faf-4d32-ab83-7ba74d29261e, Politically Correct Bedtime Stories: Modern Tales for Our Life and Times Rating: 0.5207
    ef732c5c-334b-4d6b-ab82-7255eb7286d0, Honor Among Thieves Rating: 0.5195
    0b209b8c-7cdd-47fd-b940-05c7ff7c60fc, hello Giving Tree Rating: 0.5194
    883b360f-8b42-407f-b977-2f44ad840877, Scary Stories tooTell in hello Dark: Collected from American Folklore (Scary Stories) Rating: 0.5184
ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: hello Craft of Baseball
    d008dae9-c73a-40a1-9a9b-96d5cf546f36, hello Gulag Archipelago 1918-1956: An Experiment in Literary Investigation I-II Rating: 0.5416
    ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: hello Craft of Baseball Rating: 0.5403
    49dec30e-0adb-411a-b186-48eaabf6f8bc, Fatherland Rating: 0.5394
    cc7964fd-d30f-478e-a425-93ddbdf094ed, Magic hello Gathering: Arena Vol. 1 Rating: 0.5379
    8a1e9f36-97af-4614-bed9-24e3940a05f3, More Sniglets: Any Word That Doesn't Appear in hello Dictionary but Should Rating: 0.5377
12a6d988-be21-4a09-8143-9d5f4261ba16, A Dream of Eagles
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5417
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.5416
    1f1a34c4-9781-49f5-a3cc-acec3ae3c71d, hello Family Rating: 0.5371
    56daeffe-7d48-43cd-8ef8-7dffd0c103d3, Kilo Class Rating: 0.5366
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5366
df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish
    56d33036-dfda-46b9-8e2a-76cb03921bb0, hello X-Files: Ground Zero Rating: 0.5417
    0780cde8-6529-4e1d-b6c6-082c1b80e596, Twelve Red Herrings Rating: 0.5416
    df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish Rating: 0.5408
    400fe331-2c35-490c-adbc-b28b4b73d56c, Shall We Tell hello President? Rating: 0.5383
    f86ad7d0-5c03-42b3-aebf-13d44aec8b30, Shades of Grace Rating: 0.5358
de1f62a4-89e6-44d2-aaee-992a4bf093f1, hello Map That Changed hello World: William Smith and hello Birth of Modern Geology
    de1f62a4-89e6-44d2-aaee-992a4bf093f1, hello Map That Changed hello World: William Smith and hello Birth of Modern Geology Rating: 0.5422
    b303538f-e2c6-4a2c-b425-8d21e684fc3e, My Uncle Oswald Rating: 0.5385
    34b84627-48af-4a4c-96c4-b26fb3863f56, Midnight In hello Garden of Good and Evil Rating: 0.5379
    306cbaa7-b1a8-4142-9d55-e11b5018a7a8, hello Street Lawyer Rating: 0.5376
    e53b4baa-8c09-45c4-95c0-b6a26b98770b, Miss Smillas Feeling for Snow Rating: 0.5367

Level 2
---------------
352aaea1-6b12-454d-a3d5-46379d9e4eb2, hello Sinister Pig (Hillerman Tony)
    352aaea1-6b12-454d-a3d5-46379d9e4eb2, hello Sinister Pig (Hillerman Tony) Rating: 0.5425
    74c49398-bc10-4af5-a658-a996a1201254, Children of hello Storm (Peters Elizabeth) Rating: 0.5387
    9ba80080-196e-43fd-8025-391d963f77e7, hello Floating Girl Rating: 0.5372
    e68f81d5-7745-4cc7-b943-fedb8fcc2ced, Killer Smile (Scottoline Lisa) Rating: 0.5353
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5332
c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days
    0adf981a-b65b-4c11-b36b-78aca2f948a2, hello Perfect Storm: A True Story of Men Against hello Sea Rating: 0.5433
    c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days Rating: 0.543
    a00ae6ad-4a7f-4211-9836-75ce8834eb11, Sniglets (Snig'lit: Any Word That Doesn't Appear in hello Dictionary But Should) Rating: 0.5327
    6f6e192e-0d64-49ca-9b63-f09413ea1ee6, Politically Correct Holiday Stories: For an Enlightened Yuletide Season Rating: 0.5307
    798051a8-147d-4d46-b0dc-e836325029e6, AGE OF INNOCENCE (MOVIE TIE-IN) Rating: 0.5301
73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics)
    cba8163f-6536-436b-8130-47b4a43c827f, Trust No One (hello Official Guide toohello X-Files Vol. 2) Rating: 0.5434
    5708e4cb-2492-49c0-94a8-cc413eec5d89, Small Gods (Discworld Novels (Paperback)) Rating: 0.5406
    73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics) Rating: 0.5403
    d885b0bd-ae4b-452d-bdf2-faa90197dbc9, hello Color of Magic Rating: 0.539
    b133a9c4-4784-4db3-b100-d0d6dffb94d2, hello Truth Is Out There (hello Official Guide toohello X-Files Vol. 1) Rating: 0.5367
271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why hello Winged Whale Sings
    271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why hello Winged Whale Sings Rating: 0.5445
    2de1c354-90ff-47c5-a0db-1bad7d88ef94, hello Salaryman's Wife (Children of Violence Series) Rating: 0.5329
    d279416e-19c0-43f8-9ec9-a585947879ca, Zen Attitude Rating: 0.5316
    c8f854d7-3de3-4b23-8217-f4f851670fd4, Revenge of hello Cootie Girls: A Robin Hudson Mystery (Robin Hudson Mysteries (Paperback)) Rating: 0.5305
    8ef4751c-7074-409e-a3ac-d49b222fc864, Where hello Wild Things Are Rating: 0.5289
9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God
    9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God Rating: 0.5446
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, hello Bean Trees Rating: 0.5389
    65ecbdd1-131c-40c3-a3d6-d86ca281377a, hello God of Small Things Rating: 0.5387
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, hello Stone Diaries Rating: 0.5355
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5344
5f17d90a-2604-4fe8-8977-1a280b9098b1, One for hello Money (Stephanie Plum Novels (Paperback))
    5f17d90a-2604-4fe8-8977-1a280b9098b1, One for hello Money (Stephanie Plum Novels (Paperback)) Rating: 0.5446
    57169b2b-9a8a-486b-9aac-1ed98ce57168, Final Appeal Rating: 0.5332
    efcb1bc4-7278-4a8f-b491-befde02070d6, Moment of Truth Rating: 0.5329
    1efa91a2-993b-4c43-9f5c-3454fc12612d, Burn Factor Rating: 0.5309
    24c59962-458a-4ec8-b95d-d694e861919c, At Home in Mitford (hello Mitford Years) Rating: 0.5303
4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: hello Boy Who Was Raised As a Girl
    4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: hello Boy Who Was Raised As a Girl Rating: 0.5449
    cd5f2c03-20cb-43be-a1fb-3b4233e63222, Pigs in Heaven Rating: 0.5329
    19985fdb-d07a-4a25-ae4a-97b9cb61e5d1, Love in hello Time of Cholera (Penguin Great Books of hello 20th Century) Rating: 0.5267
    15689d09-c711-4844-84d8-130a90237b26, Bel Canto Rating: 0.5245
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5235
98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories
    f874b5a3-5d40-4436-94ff-0fa1c090ddf5, hello Sun Also Rises (A Scribner classic) Rating: 0.5451
    98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories Rating: 0.5442
    0ce0014a-9a48-4013-a08a-7f2c11877930, H.M.S. Unseen Rating: 0.5421
    15316ca6-1e38-425f-893d-691944a47000, More Scary Stories tooTell In hello Dark Rating: 0.5409
    329d5682-3dc3-4206-8aa2-eef4b1032258, Letters from hello Earth Rating: 0.54
5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover))
    5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover)) Rating: 0.5462
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5372
    604eb3bd-6026-4f51-bffd-9fb54f180400, Family Pictures: A Novel Rating: 0.5341
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5334
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, hello Bean Trees Rating: 0.5319
d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven
    d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven Rating: 0.5491
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5401
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, hello Stone Diaries Rating: 0.5393
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5382
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5367

</pre>


## <a name="7-model-business-rules"></a>7. Regras de negócio do modelo
Estes são os tipos de saudação de regras de suporte:

* <strong>Lista de bloqueios</strong> -lista de bloqueios permite que você tooprovide uma lista de itens que você não quer tooreturn nos resultados de recomendação de saudação. 
* <strong>FeatureBlockList</strong> -lista de bloqueios do recurso permite que você tooblock itens com base nos valores de saudação de seus recursos.

*Não envie mais de 1.000 itens em uma única regra de lista de bloqueios ou sua chamada poderá expirar. Se você precisar de mais de 1.000 itens tooblock, você pode fazer várias chamadas de lista de bloqueios.*

* <strong>Upsale</strong> -Upsale permite que você tooenforce itens tooreturn nos resultados de recomendação de saudação.
* <strong>Lista branca</strong> -lista branca permite você tooonly sugerir recomendações de uma lista de itens.
* <strong>FeatureWhiteList</strong> -lista de permissões de recurso permite que você tooonly recomendável itens que têm valores de recurso específico.
* <strong>PerSeedBlockList</strong> - por habilita semente de bloco que você tooprovide por uma lista de itens que não pode ser retornado como resultados de recomendação de item.

### <a name="71----get-model-rules"></a>7.1.    Obter regras de modelo
| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetModelRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br>Exemplo:<br>`<rootURI>/GetModelRules?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de saudação |
| apiVersion |1.0 |
|  | |
| Corpo da solicitação |NENHUM |

**Resposta**:

Código de status HTTP: 200

* `feed/entry/content/properties/Id` - Identificador exclusivo desta regra.
* `feed/entry/content/properties/Type`-Tipo de regra de saudação.
* `feed/entry/content/properties/Parameter` - O parâmetro da regra.

XML de OData

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get a list of rules for a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T12:58:57Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000043</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1000"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000044</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1001"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="72----add-rule"></a>7.2.    Adicionar regra
| Método HTTP | URI |
|:--- |:--- |
| POST |`<rootURI>/AddRule?apiVersion=%271.0%27` |
| HEADER |`"Content-Type", "text/xml"` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| apiVersion |1.0 |
|  | |
| Corpo da solicitação | |

<ins>Sempre que fornecer Ids de Item para regras de negócios, verifique se toouse Olá externo Id do item de hello (Olá a mesma Id que você usou no arquivo de catálogo Olá)</ins><br>
<ins>tooadd uma regra de lista de bloqueios:</ins><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>BlockList</Type><Value>{"ItemsToExclude":["2406E770-769C-4189-89DE-1C9283F93A96","3906E110-769C-4189-89DE-1C9283F98888"]}</Value></ApiFilter>`<br><br><ins>
<ins>tooadd uma regra de FeatureBlockList:</ins><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureBlockList</Type><Value>{"Name":"Movie_category","Values":["Adult","Drama"]}</Value></ApiFilter>`<br><br><ins>tooadd uma regra de Upsale:</ins><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>Upsale</Type><Value>{"ItemsToUpsale":["2406E770-769C-4189-89DE-1C9283F93A96"],"NumberOfItemsToUpsale":5}</Value></ApiFilter>`<br><br>
<ins>tooadd uma regra de lista de permissões:</ins><br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>WhiteList</Type><Value>{"ItemsToInclude":["2406E770-769C-4189-89DE-1C9283F93A96","1116E770-769C-4189-89DE-1C9283F88888"]}</Value></ApiFilter>`<br><br><ins>
<ins>tooadd uma regra de FeatureWhiteList:</ins><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureWhiteList</Type><Value>{"Name":"Movie_rating","Values":["PG13"]}</Value></ApiFilter>`<br><br><ins>tooadd uma regra de PerSeedBlockList:</ins><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>PerSeedBlockList</Type><Value>{"SeedItems":["9949"],"ItemsToExclude":["9862","8158","8244"]}</Value></ApiFilter>`|

**Resposta**:

Código de status HTTP: 200

Olá API retorna Olá recém-criado regra com seus detalhes. propriedade de regras Olá pode ser recuperada da saudação caminhos a seguir:

* `feed/entry/content/properties/Id` - Identificador exclusivo desta regra.
* `feed/entry/content/properties/Type`-Tipo de regra de saudação: lista de bloqueios ou Upsale.
* `feed/entry/content/properties/Parameter` - O parâmetro da regra.

XML de OData

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Add A Rule</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T11:13:28Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AddARuleEntity</title>
        <updated>2014-11-05T11:13:28Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000041</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1002"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="73----delete-rule"></a>7.3.    Excluir regra
| Método HTTP | URI |
|:--- |:--- |
| EXCLUIR |`<rootURI>/DeleteRule?modelId=%27<model_id>%27&filterId=%27<filter_Id>%27&apiVersion=%271.0%27`<br><br>Exemplo:<br>`DeleteRule?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&filterId=%271000011%27&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de saudação |
| filterId |Identificador exclusivo do filtro de saudação |
| apiVersion |1.0 |
|  | |
| Corpo da solicitação |NENHUM |

**Resposta**:

Código de status HTTP: 200

### <a name="74----delete-all-rules"></a>7.4.    Excluir todas as regras
| Método HTTP | URI |
|:--- |:--- |
| EXCLUIR |`<rootURI>/DeleteAllRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>Exemplo:<br>`DeleteAllRules?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de saudação |
| apiVersion |1.0 |
|  | |
| Corpo da solicitação |NENHUM |

**Resposta**:

Código de status HTTP: 200

## <a name="8-catalog"></a>8. Catálogo
### <a name="81----import-catalog-data"></a>8.1.    Importar Dados de Catálogo
Se você carregar vários catálogo arquivos toohello mesmo modelo com várias chamadas, inserimos somente Olá novos itens de catálogo. Itens existentes permanecerão com seus valores originais hello. Você não pode atualizar os dados do catálogo usando este método.

dados de catálogo de saudação devem seguir Olá formato a seguir:

* Sem recursos – `<Item Id>,<Item Name>,<Item Category>[,<Description>]`
* Com recursos – `<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`

Observação: o tamanho máximo do arquivo de saudação é 200MB.

** Detalhes do formato **

| Nome | Obrigatório | Tipo | Descrição |
|:--- |:--- |:--- |:--- |
| Id do item |Sim |[A-z], [a-z], [0-9], [_] &#40;Sublinhado&#41;, [-] &#40;Traço&#41;<br> Comprimento máximo: 50 |Identificador exclusivo de um item |
| Nome do Item |Sim |Qualquer caractere alfanumérico<br> Comprimento máximo: 255 |Nome do item. |
| Categoria do Item |Sim |Qualquer caractere alfanumérico <br> Comprimento máximo: 255 |Categoria toowhich este item pertence (por exemplo, culinária manuais, Drama...); pode ser vazio. |
| Descrição |Não, a menos que os recursos estejam presentes (mas pode estar vazia) |Qualquer caractere alfanumérico <br> Comprimento máximo: 4000 |Descrição deste item. |
| Lista de recursos |Não |Qualquer caractere alfanumérico <br> Comprimento máximo: 4.000; Número máximo de recursos: 20 |Lista separada por vírgulas de nome do recurso = valor de recurso que pode ser usado tooenhance recomendação do modelo; consulte [tópicos avançados](#2-advanced-topics) seção. |

| Método HTTP | URI |
|:--- |:--- |
| POST |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |
| HEADER |`"Content-Type", "text/xml"` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de saudação |
| nome do arquivo |Identificador textual do catálogo de saudação.<br>São permitidos apenas letras (A-Z, a-z), números (0-9), hifens (-) e sublinhado (_).<br>Comprimento máximo: 50 |
| apiVersion |1.0 |
|  | |
| Corpo da solicitação |Exemplo (com recursos):<br/>2406e770-769c-4189-89de-1c9283f93a96, Clara Callan, catálogo, descrição de catálogo hello, criar = Richard Wright, publicador = Harper Flamingo Canadá, ano = 2001<br>Olá 21bf8088-b6c0-4509-870c-e1c7ac78304a, sala Forgetting: criar um ficção (Byzantium catálogo), catálogo, = Nick Bantock, publicador = Harpercollins, ano = 1997<br>3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book,,author=Timothy Findley, publisher=HarperFlamingo Canada, year=2001<br>552a1940-21e4-4399-82bb-594b46d7ed54, moderação de feras, livro, descrição de catálogo hello, criar = Magnus Mills, publicador = publicação de Arcade ano = 1998</pre> |

**Resposta**:

Código de status HTTP: 200

Olá API retorna um relatório de importação de saudação.

* `feed\entry\content\properties\LineCount` – O número de linhas aceitas.
* `feed\entry\content\properties\ErrorCount`-Número de linhas que não foram inseridas devido a erro tooan.

XML de OData

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Import catalog file</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-05T06:58:04Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'" />
    <entry>
       <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ImportCatalogFileEntity2</title>
        <updated>2014-10-05T06:58:04Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:LineCount m:type="Edm.String">4</d:LineCount>
                <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="82----get-catalog"></a>8.2.    Obter catálogo
Recupera todos os itens de catálogo.
Olá catálogo será recuperado de uma página por vez. Se você quiser tooget itens em um índice específico, você pode usar o parâmetro de odata Olá $skip. Por exemplo se você quiser itens tooget começando na posição 100, Adicionar parâmetro hello $skip = solicitação de toohello 100.

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetCatalog?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>Exemplo:<br>`GetCatalog?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de saudação |
| apiVersion |1.0 |
|  | |
| Corpo da solicitação |NENHUM |

**Resposta**:

Código de status HTTP: 200

resposta de saudação inclui uma entrada por item de catálogo. Cada entrada tem Olá seguintes dados:

* `feed/entry/content/properties/ExternalId`-ID externa do item de catálogo, Olá fornecido pelo cliente hello.
* `feed/entry/content/properties/InternalId`-ID interna do item, Olá que gerou recomendações de aprendizado de máquina do Azure do catálogo.
* `feed/entry/content/properties/Name` - Nome do item do catálogo.
* `feed/entry/content/properties/Category` - Categoria do item do catálogo.
* `feed/entry/content/properties/Description` - Descrição do item do catálogo.
* `feed/entry/content/properties/Metadata` - Metadados do item do catálogo.

XML de OData

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get All Catalog Items</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">552A1940-21E4-4399-82BB-594B46D7ED54</d:ExternalId>
                <d:InternalId m:type="Edm.String">060db26a-e6a6-464e-bb52-436d2da82a50</d:InternalId>
                <d:Name m:type="Edm.String">Restraint of Beasts</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:ExternalId>
                <d:InternalId m:type="Edm.String">209d7bfe-2eb9-4455-92a3-7c867a41a74a</d:InternalId>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">3BB5CB44-D143-4BDD-A55C-443964BF4B23</d:ExternalId>
                <d:InternalId m:type="Edm.String">913ff79b-059b-4d4d-8042-6fa4cc1391dd</d:InternalId>
                <d:Name m:type="Edm.String">Spadework</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">21BF8088-B6C0-4509-870C-E1C7AC78304A</d:ExternalId>
                <d:InternalId m:type="Edm.String">ea65e4fa-768c-40b4-92c3-69d3e8178691</d:InternalId>
                <d:Name m:type="Edm.String">hello Forgetting Room: A Fiction (Byzantium Book)</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="83----get-catalog-items-by-token"></a>8.3.    Obter itens de catálogo por Token
| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetCatalogItemsByToken?modelId=%27<modelId>%27&token=%27<token>%27&apiVersion=%271.0%27`<br><br>Exemplo:<br>`GetCatalogItemsByToken?modelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&token=%27Cla%27&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de saudação |
| token |Token de nome do item de catálogo hello. Deve conter pelo menos três caracteres. |
| apiVersion |1.0 |
|  | |
| Corpo da solicitação |NENHUM |

**Resposta**:

Código de status HTTP: 200

resposta de saudação inclui uma entrada por item de catálogo. Cada entrada tem Olá seguintes dados:

* `feed/entry/content/properties/InternalId`-ID interna do item, Olá que gerou recomendações de aprendizado de máquina do Azure do catálogo.
* `feed/entry/content/properties/Name` - Nome do item do catálogo.
* `feed/entry/content/properties/Rating` - (para uso futuro)
* `feed/entry/content/properties/Reasoning` - (para uso futuro)
* `feed/entry/content/properties/Metadata` - (para uso futuro)
* `feed/entry/content/properties/FormattedRating` - (para uso futuro)

XML de OData

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get Catalog items that contain a token</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:48:19Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">CatalogItemsThatContainATokenEntity</title>
            <updated>2014-10-29T11:48:19Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                  <m:properties>
                    <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                    <d:Name m:type="Edm.String">Clara Callan</d:Name>
                    <d:Rating m:type="Edm.Double">0</d:Rating>
                    <d:Reasoning m:type="Edm.String"></d:Reasoning>
                    <d:Metadata m:type="Edm.String"></d:Metadata>
                    <d:FormattedRating m:type="Edm.Double" m:null="true"></d:FormattedRating>
                  </m:properties>
            </content>
        </entry>
    </feed>

## <a name="9-usage-data"></a>9. Dados de uso
### <a name="91----import-usage-data"></a>9.1.    Importar Dados de Uso
#### <a name="911-uploading-file"></a>9.1.1. Carregamento de Arquivo
Esta seção mostra como os dados de uso tooupload usando um arquivo. Você pode chamar essa API várias vezes com dados de uso. Todos os dados de uso serão salvos para todas as chamadas.

| Método HTTP | URI |
|:--- |:--- |
| POST |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de saudação |
| nome do arquivo |Identificador textual do catálogo de saudação.<br>São permitidos apenas letras (A-Z, a-z), números (0-9), hifens (-) e sublinhado (_).<br>Comprimento máximo: 50 |
| apiVersion |1.0 |
|  | |
| Corpo da solicitação |Dados de uso. Formato:<br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th>Nome</th><th>Obrigatório</th><th>Tipo</th><th>Descrição</th></tr><tr><td>Id de usuário</td><td>Sim</td><td>[A-z], [a-z], [0-9], [_] &#40;Sublinhado&#41;, [-] &#40;Traço&#41;<br> Comprimento máximo: 255 </td><td>Identificador exclusivo de um usuário.</td></tr><tr><td>Id do item</td><td>Sim</td><td>[A-z], [a-z], [0-9], [&#95;] &#40;Underscore&#41;, [-] &#40;Dash&#41;<br> Comprimento máximo: 50</td><td>Identificador exclusivo de um item</td></tr><tr><td>Hora</td><td>Não</td><td>Data no formato: AAAA/MM/DDTHH:MM:SS (por exemplo, 2013/06/20T10:00:00)</td><td>Hora dos dados.</td></tr><tr><td>Evento</td><td>Não; se fornecido, também deve colocar a data</td><td>Um dos seguintes hello:<br>• Clique<br>• RecommendationClick<br>•    AddShopCart<br>• RemoveShopCart<br>• Compra</td><td></td></tr></table><br>Tamanho máximo do arquivo: 200 MB<br><br>Exemplo:<br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

**Resposta**:

Código de status HTTP: 200

* `Feed\entry\content\properties\LineCount` – O número de linhas aceitas.
* `Feed\entry\content\properties\ErrorCount`-Número de linhas que não foram inseridas devido a erro tooan.
* `Feed\entry\content\properties\FileId` – Identificador do arquivo.

XML de OData

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Add bulk usage data (usage file)</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T07:21:44Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">AddBulkUsageDataUsageFileEntity2</title>
    <updated>2014-10-05T07:21:44Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">33</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
        <d:FileId m:type="Edm.String">fead7c1c-db01-46c0-872f-65bcda36025d</d:FileId>
      </m:properties>
    </content>
      </entry>
    </feed>


#### <a name="912-using-data-acquisition"></a>9.1.2. Usar a Aquisição de Dados
Esta seção mostra como eventos toosend real tempo recomendações tooAzure de aprendizado de máquina, normalmente a partir de seu site.

| Método HTTP | URI |
|:--- |:--- |
| POST |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27` |
| HEADER |`"Content-Type", "text/xml"` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| apiVersion |1.0 |
| Corpo da solicitação |Entrada de dados de evento para cada evento que você deseja toosend. Você deve enviar para a mesma sessão de usuário ou navegador Olá Olá mesmo ID nesse campo de SessionId hello. (Consulte o exemplo de corpo de evento abaixo.) |

* Exemplo de evento “Click”:
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
        <Name>Click</Name>
        <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
        </EventData>
        </Event>
* Exemplo de evento “RecommendationClick”:
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>RecommendationClick</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* Exemplo de evento “AddShopCart”:
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* Exemplo de evento “RemoveShopCart”:
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
              <EventData>
                      <Name>RemoveShopCart</Name>
                      <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
                </EventData>
          </EventData>
        </Event>
* Exemplo de evento “Purchase”:
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
            <EventData>
                <Name>Purchase</Name>
                <PurchaseItems>
                    <PurchaseItem>
                        <ItemId>ABBF8081-C5C0-4F09-9701-E1C7AC78304A</ItemId>
                        <Count>1</Count>
                    </PurchaseItem>
                    <PurchaseItem>
                        <ItemId>21BF8088-B6C0-4509-870C-11C0AC7F304B</ItemId>
                        <Count>3</Count>
                    </PurchaseItem>
                </PurchaseItems>
            </EventData>
        </EventData>
        </Event>
* Exemplo de envio de dois eventos “Click” e “AddShopCart”:
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>Click</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
          <ItemName>itemName</ItemName>
          <ItemDescription>item description</ItemDescription>
          <ItemCategory>category</ItemCategory>
        </EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>552A1940-21E4-4399-82BB-594B46D7ED54</ItemId>
        </EventData>
          </EventData>
        </Event>

**Response**: código de status HTTP: 200

### <a name="92----list-model-usage-files"></a>9.2.    Lista dos arquivos de modelo de uso
Recupera os metadados de todos os arquivos de uso do modelo.
Olá uso arquivos poderão ser recuperados uma página por vez. Cada página contém 100 itens. Se você quiser tooget itens em um índice específico, você pode usar o parâmetro de odata Olá $skip. Por exemplo se você quiser itens tooget começando na posição 100, Adicionar parâmetro hello $skip = solicitação de toohello 100.

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/ListModelUsageFiles?forModelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/ListModelUsageFiles?forModelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| forModelId |Identificador exclusivo do modelo de saudação |
| apiVersion |1.0 |
|  | |
| Corpo da solicitação |NENHUM |

**Resposta**:

Código de status HTTP: 200

resposta de saudação inclui uma entrada por arquivo de uso. Cada entrada tem Olá seguintes dados:

* `feed\entry\content\properties\Id` - ID do arquivo de uso.
* `feed\entry\content\properties\Length` - Comprimento de arquivo de uso em MB.
* `feed\entry\content\properties\DateModified`-Data em que o arquivo de uso de saudação foi criado.
* `feed\entry\content\properties\UseInModel`-Se o arquivo de uso de saudação é usado no modelo de saudação.

XML de OData

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of model's usage files info</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
            <updated>2014-10-30T09:40:25Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">4c067b42-e975-4cb2-8c98-a6ab80ed6d63</d:Id>
                    <d:Length m:type="Edm.Double">0</d:Length>
                    <d:DateModified m:type="Edm.String">10/30/2014 9:19:57 AM</d:DateModified>
                    <d:UseInModel m:type="Edm.String">true</d:UseInModel>
                </m:properties>
            </content>
        </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">3126d816-4e80-4248-8339-1ebbdb9d544d</d:Id>
                <d:Length m:type="Edm.Double">0.001</d:Length>
                <d:DateModified m:type="Edm.String">10/30/2014 9:21:44 AM</d:DateModified>
                <d:UseInModel m:type="Edm.String">true</d:UseInModel>
              </m:properties>
        </content>
    </entry>
</feed>

### <a name="93----get-usage-statistics"></a>9.3.    Obter estatísticas de uso
Obter estatísticas de uso

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetUsageStatistics?modelId=%27<modelId>%27& startDate=%27<date>%27&endDate=%27<date>%27&eventTypes=%27<types>%27&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/GetUsageStatistics?modelId=%271d20c34f-dca1-4eac-8e5d-f299e4e4ad66%27&startDate=%272014%2F10%2F17T00%3A00%3A00%27&endDate=%272014%2F11%2F16T00%3A00%3A00%27&eventTypes=%271%2C2%2C3%2C4%2C5%27&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de saudação |
| startDate |Data de início. Formato: aaaa/MM/ddTHH:mm:ss |
| endDate |Data de término. Formato: aaaa/MM/ddTHH:mm:ss |
| eventTypes |Tipos de cadeia de caracteres separada por vírgulas de evento ou null tooget todos os eventos |
| apiVersion |1.0 |
|  | |
| Corpo da solicitação |NENHUM |

**Resposta**:

Código de status HTTP: 200

Uma coleção de elementos de chave/valor. Cada uma contém a soma de saudação de eventos para um tipo de evento específico, agrupados por hora.

* `feed\entry[i]\content\properties\Key`-Contém o tempo de saudação (agrupado por hora) e o tipo de evento de saudação.
* `feed\entry[i]\content\properties\Value` - Contagem de eventos total.

XML de OData

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get usage statistics</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-18T11:39:16Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;Click</d:Event>
                <d:Value m:type="Edm.String">5</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;RecommendationClick</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
              </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/1/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/5/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="94----get-usage-file-sample"></a>9.4.    Obter um exemplo de arquivo de uso
Recupera Olá primeiro 2KB de conteúdo do arquivo de uso.

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetUsageFileSample?modelId=%27<modelId>%27& fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/GetUsageFileSample?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fileId=%274c067b42-e975-4cb2-8c98-a6ab80ed6d63%27&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de saudação |
| fileId |Identificador exclusivo do arquivo de modelo de uso de saudação |
| apiVersion |1.0 |
|  | |
| Corpo da solicitação |NENHUM |

**Resposta**:

Código de status HTTP: 200

A resposta é retornada no formato de texto sem formatação:

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
</pre>


### <a name="95----get-model-usage-file"></a>9.5.    Obtenha o modelo do arquivo de uso
Recupera todo o conteúdo do arquivo de uso Olá Olá.

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetModelUsageFile?mid=%27<modelId>%27& fid=%27<fileId>%27&download=%27<download_value>%27&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/GetModelUsageFile?mid=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fid=%273126d816-4e80-4248-8339-1ebbdb9d544d%27&download=%271%27&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| mid |Identificador exclusivo do modelo de saudação |
| fid |Identificador exclusivo do arquivo de modelo de uso de saudação |
| baixar |1 |
| apiVersion |1.0 |
|  | |
| Corpo da solicitação |NENHUM |

**Resposta**:

Código de status HTTP: 200

A resposta é retornada no formato de texto sem formatação:

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
244881,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
50547,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
213090,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
260655,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
72214,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
36326,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189336,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260655,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
162100,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
54946,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260965,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
102758,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
112602,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
163925,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
262998,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
144717,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
</pre>

### <a name="96----delete-usage-file"></a>9.6.    Excluir o arquivo de uso
Exclui o arquivo de uso do modelo especificado hello.

| Método HTTP | URI |
|:--- |:--- |
| EXCLUIR |`<rootURI>/DeleteUsageFile?modelId=%27<modelId>%27&fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/DeleteUsageFile?modelId=%270f86d698-d0f4-4406-a684-d13d22c47a73%27&fileId=%27f2e0b09d-be5c-46b2-9ac2-c7f622e5e1a5%27&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de saudação |
| fileId |Identificador exclusivo da saudação toobe de arquivo excluído |
| apiVersion |1.0 |
|  | |
| Corpo da solicitação |NENHUM |

**Resposta**:

Código de status HTTP: 200

### <a name="97----delete-all-usage-files"></a>9.7.    Excluir todos os arquivos de uso
Exclui todos os arquivos de uso do modelo.

| Método HTTP | URI |
|:--- |:--- |
| EXCLUIR |`<rootURI>/DeleteAllUsageFiles?modelId=%27<modelId>%27&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/DeleteAllUsageFiles?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de saudação |
| apiVersion |1.0 |
|  | |
| Corpo da solicitação |NENHUM |

**Resposta**:

Código de status HTTP: 200

## <a name="10-features"></a>10. Recursos
Esta seção mostra como tooretrieve recurso informações, como recursos de saudação importado e seus valores, sua classificação, e quando esta classificação foi alocada. Recursos são importados como parte dos dados de catálogo Olá, e, em seguida, sua classificação associada quando é feita uma compilação de classificação.
Classificação de recurso pode alterar o acordo padrão de toohello de dados de uso e tipo de itens. Mas para uso consistentes/itens, classificação de saudação deve ter apenas pequenas flutuações.
classificação de saudação de recursos é um número negativo. Olá número 0 significa que não foi classificado com o recurso hello (acontece se você invocar essa conclusão de toohello anterior de API da compilação de classificação primeiro Olá). Data de saudação em que a classificação Olá foi atribuída é chamada de atualização de pontuação hello.

### <a name="101-get-features-info-for-last-rank-build"></a>10.1. Obter informações de recursos (para a última compilação de classificação)
Recupera as informações de recurso hello, incluindo classificação, para a última compilação classificação bem-sucedida hello.

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de saudação |
| samplingSize |Número de valores tooinclude para cada recurso de acordo com dados de toohello presentes no catálogo de saudação. <br/>Os valores possíveis são:<br> - 1 - Todas as amostras. <br>0 - Sem amostragem. <br>N - Retornar N amostras para cada nome de recurso. |
| apiVersion |1.0 |
|  | |
| Corpo da solicitação |NENHUM |

**Resposta**:

Código de status HTTP: 200

resposta de saudação contém uma lista de entradas de informações de recurso. Cada entrada contém:

* `feed/entry/content/m:properties/d:Name` - Nome do recurso.
* `feed/entry/content/m:properties/d:RankUpdateDate`-Data em que Olá classificação foi alocado toothis recurso, também conhecido como recurso de atualização de pontuação. Uma data do histórico (“0001-01-01T00:00:00”) significa que nenhuma compilação de classificação foi executada.
* `feed/entry/content/m:properties/d:Rank` - Classificação de recurso (float). Uma classificação de 2.0 e superior é considerada um bom recurso.
* `feed/entry/content/m:properties/d:SampleValues`-Lista separada por vírgulas dos valores de tamanho de amostragem toohello solicitado.

XML de OData

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get hello features of a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-01-08T13:15:02Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Author</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Publisher</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1"/>
        <contenttype="application/xml">
        <m:properties>
            <d:Name m:type="Edm.String">Year</d:Name>
            <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
            <d:Rank m:type="Edm.String">0</d:Rank>
            <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
        </m:properties>
        </content>
    </entry>
</feed>

### <a name="102-get-features-info-for-specific-rank-build"></a>10.2. Obter informações de recursos (para uma compilação de classificação específica)
Recupera as informações de recurso hello, incluindo Olá de classificação para uma determinada compilação de classificação.

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&rankBuildId=<rankBuildId>&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&rankBuildId=1000551&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de saudação |
| samplingSize |Número de valores tooinclude para cada recurso de acordo com dados de toohello presentes no catálogo de saudação.<br/> Os valores possíveis são:<br> - 1 - Todas as amostras. <br>0 - Sem amostragem. <br>N - Retornar N amostras para cada nome de recurso. |
| rankBuildId |Identificador exclusivo da compilação classificação hello ou -1 para a última compilação de classificação Olá |
| apiVersion |1.0 |
|  | |
| Corpo da solicitação |NENHUM |

**Resposta**:

Código de status HTTP: 200

resposta de saudação contém uma lista de entradas de informações de recurso. Cada entrada contém:

* `feed/entry/content/m:properties/d:Name` - Nome do recurso.
* `feed/entry/content/m:properties/d:RankUpdateDate`-Data em que Olá classificação foi alocado toothis recurso, também conhecido como recurso de atualização de pontuação. Uma data do histórico (“0001-01-01T00:00:00”) significa que nenhuma compilação de classificação foi executada.
* `feed/entry/content/m:properties/d:Rank` - Classificação de recurso (float). Uma classificação de 2.0 e superior é considerada um bom recurso.
* `feed/entry/content/m:properties/d:SampleValues`-Lista separada por vírgulas dos valores de tamanho de amostragem toohello solicitado.

OData

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get hello features of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:54:22Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Author</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">3.38867426</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Publisher</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.67839336</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Year</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.12352145</d:Rank>
                    <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
                </m:properties>
            </content>
        </entry>
    </feed>


## <a name="11-build"></a>11. Compilação
  Esta seção explica Olá diferentes APIs relacionadas toobuilds. Existem 3 tipos de compilações: uma compilação de recomendação, uma compilação de classificação e uma compilação FBT (frequentemente comprada junto).

finalidade da compilação do Hello recomendação é toogenerate um modelo de recomendação é usado para previsões. As previsões (para esse tipo de compilação) vêm em duas versões:

* I2I - também conhecido como Item recomendações tooItem - receber um item ou uma lista de itens, essa opção poderá prever uma lista de itens que são provavelmente toobe altamente interessante.
* U2I - também conhecido como Recomendações de tooItem usuário - recebe uma id de usuário (e, opcionalmente, uma lista de itens) essa opção poderá prever uma lista de itens que são provavelmente toobe altamente interessante para Olá dado usuário (e suas opções adicionais de itens). recomendações de U2I Olá baseiam-se no histórico de saudação de itens que foram de interesse do usuário Olá tempo toohello Olá modelo foi criado.

Uma compilação de classificação é uma compilação técnica que permite que você toolearn sobre a utilidade de saudação de seus recursos. Geralmente, em ordem tooget Olá melhores resultados para um modelo de recomendação que envolvem recursos, você deve levar Olá etapas a seguir:

* Disparar um build de classificação (a menos que a pontuação Olá dos recursos de estável) e aguarde até que você obtém a pontuação de recurso de saudação.
* Recuperar classificação Olá os recursos por chamada hello [obter informações de recursos](#101-get-features-info-for-last-rank-build) API.
* Configure uma compilação de recomendação com hello parâmetros a seguir:
  * `useFeatureInModel`-Definir tooTrue.
  * `ModelingFeatureList`-Lista de separada por vírgulas de tooa conjunto de recursos com uma pontuação de 2.0 ou mais (de acordo com classificações toohello recuperado na etapa anterior Olá).
  * `AllowColdItemPlacement`-Definir tooTrue.
  * Opcionalmente, você pode definir `EnableFeatureCorrelation` tooTrue e `ReasoningFeatureList` toohello lista de recursos que você deseja toouse para obter explicações (geralmente Olá mesma lista de recursos usada na modelagem ou uma sublista).
* Disparar Olá recomendação compilação com parâmetros de saudação configurado.

Observação: Se você não configurar os parâmetros (por exemplo, invocar a compilação de recomendação de saudação sem parâmetros) ou você não desabilitar explicitamente uso Olá de recursos (por exemplo, `UseFeatureInModel` definir tooFalse), sistema Olá definirá os parâmetros relacionados ao recurso de saudação toohello explicado acima de valores, caso exista uma compilação de classificação.

Não há nenhuma restrição sobre como executar uma compilação de classificação e uma recomendação de compilação simultaneamente para Olá mesmo modelo. No entanto, você não pode executar duas versões do mesmo tipo no mesmo modelo em paralelo de saudação do hello.

Uma compilação FBT (Frequentemente Comprado Juntos) é outro algoritmo de recomendações chamado por vezes de recomendador "conservador", o que é bom para os catálogos não homogêneos por natureza (homogêneas: livros, filmes, alguns alimentos, moda; não homogêneo: computadores e dispositivos, entre domínios, altamente diversificados).

Observação: se os arquivos de uso que você carregou hello contêm campo opcional de hello "tipo de evento", em seguida, para FBT modelagem somente eventos de "Comprar" será usado. Se nenhum tipo de evento for fornecido, todos os eventos serão considerados como compra.

#### <a name="111-build-parameters"></a>11.1 Parâmetros de compilação
Cada tipo de compilação pode ser configurado por meio de um conjunto de parâmetros (descritos abaixo). Se você não configurar parâmetros de saudação, o sistema Olá automaticamente atributo valores de parâmetros toohello toohello informações presentes no tempo de saudação disparar um build de acordo com.

##### <a name="1111-usage-condenser"></a>11.1.1. Condensador de uso
Os usuários ou itens com poucos pontos de uso podem conter mais ruído que informações. sistema de saudação tentativas toopredict Olá o número mínimo de pontos de uso por usuário/item toobe usada em um modelo. Esse número será dentro do intervalo de saudação definido pelo hello ItemCutoffLowerBound e parâmetros de ItemCutoffUpperBound itens e o intervalo de saudação definido pelo hello UserCutOffLowerBound e UserCutoffUpperBound parâmetros para os usuários. efeito de condensador Olá itens ou usuários pode ser minimizado definindo pelo menos uma das Olá correspondente toozero de limites.

##### <a name="1112-rank-build-parameters"></a>11.1.2. Parâmetros de compilação de classificação
Olá a tabela abaixo descreve os parâmetros de construção Olá para um build de classificação.

| Chave | Descrição | Tipo | Valor Válido |
|:--- |:--- |:--- |:--- |
| NumberOfModelIterations |número de saudação de iterações modelo Olá executa é refletido pela Olá tempo e hello precisão do modelo de computação geral. número mais alto de Olá Olá, você terá maior precisão do hello, mas Olá computação tempo irá demorar mais. |Número inteiro |10-50 |
| NumberOfModelDimensions |número de saudação de dimensões se relaciona toohello número do modelo de saudação 'recursos' tentará toofind dentro de seus dados. Aumentar o número de saudação de dimensões permitirá ajustar melhor os resultados de saudação em clusters menores. No entanto, muitas dimensões impedirá modelo Olá localização de correlações entre itens. |Número inteiro |10-40 |
| ItemCutOffLowerBound |Define Olá item inferior para condensador hello. Consulte o condensador de uso acima. |Número inteiro |2 ou mais (0 desabilita o condensador) |
| ItemCutOffUpperBound |Define Olá item limite superior condensador hello. Consulte o condensador de uso acima. |Número inteiro |2 ou mais (0 desabilita o condensador) |
| UserCutOffLowerBound |Define Olá usuário inferior para condensador hello. Consulte o condensador de uso acima. |Número inteiro |2 ou mais (0 desabilita o condensador) |
| UserCutOffUpperBound |Define Olá usuário limite superior condensador hello. Consulte o condensador de uso acima. |Número inteiro |2 ou mais (0 desabilita o condensador) |

##### <a name="1113-recommendation-build-parameters"></a>11.1.3. Parâmetros de compilação de recomendação
Olá a tabela abaixo descreve os parâmetros de construção Olá para compilação de recomendação.

| Chave | Descrição | Tipo | Valor Válido |
|:--- |:--- |:--- |:--- |
| NumberOfModelIterations |número de saudação de iterações modelo Olá executa é refletido pela Olá tempo e hello precisão do modelo de computação geral. número mais alto de Olá Olá, você terá maior precisão do hello, mas Olá computação tempo irá demorar mais. |Número inteiro |10-50 |
| NumberOfModelDimensions |número de saudação de dimensões se relaciona toohello número do modelo de saudação 'recursos' tentará toofind dentro de seus dados. Aumentar o número de saudação de dimensões permitirá ajustar melhor os resultados de saudação em clusters menores. No entanto, muitas dimensões impedirá modelo Olá localização de correlações entre itens. |Número inteiro |10-40 |
| ItemCutOffLowerBound |Define Olá item inferior para condensador hello. Consulte o condensador de uso acima. |Número inteiro |2 ou mais (0 desabilita o condensador) |
| ItemCutOffUpperBound |Define Olá item limite superior condensador hello. Consulte o condensador de uso acima. |Número inteiro |2 ou mais (0 desabilita o condensador) |
| UserCutOffLowerBound |Define Olá usuário inferior para condensador hello. Consulte o condensador de uso acima. |Número inteiro |2 ou mais (0 desabilita o condensador) |
| UserCutOffUpperBound |Define Olá usuário limite superior condensador hello. Consulte o condensador de uso acima. |Número inteiro |2 ou mais (0 desabilita o condensador) |
| Descrição |Descrição da compilação. |Cadeia de caracteres |Qualquer texto, máximo de 512 caracteres |
| EnableModelingInsights |Permite que você toocompute métricas no modelo de recomendação de saudação. |Booliano |Verdadeiro/Falso |
| UseFeaturesInModel |Indica se os recursos podem ser usados no modelo de recomendação de saudação do pedido tooenhance. |Booliano |Verdadeiro/Falso |
| ModelingFeatureList |Lista separada por vírgulas de toobe de nomes de recurso usado na compilação de recomendação hello, na recomendação de saudação do tooenhance de ordem. |Cadeia de caracteres |Nomes de recurso, o too512 caracteres |
| AllowColdItemPlacement |Indica se a recomendação de saudação também enviar por push itens frios por meio de similaridade de recurso. |Booliano |Verdadeiro/Falso |
| EnableFeatureCorrelation |Indica se os recursos podem ser usados no raciocínio. |Booliano |Verdadeiro/Falso |
| ReasoningFeatureList |Lista separada por vírgulas de toobe de nomes de recurso usado para raciocínio sentenças (por exemplo, explicações de recomendação). |Cadeia de caracteres |Nomes de recurso, o too512 caracteres |
| EnableU2I |Permitir recomendação Olá personalizado conhecido como U2I (recomendações de tooitem do usuário). |Booliano |True/False (verdadeiro por padrão) |

##### <a name="1114-fbt-build-parameters"></a>11.1.4. Parâmetros de compilação FBT
Olá a tabela abaixo descreve os parâmetros de construção Olá para compilação de recomendação.

| Chave | Descrição | Tipo | Valor Válido (Padrão) |
|:--- |:--- |:--- |:--- |
| FbtSupportThreshold |Como o modelo Olá conservadora é. Número de ocorrências colegas de itens toobe considerados para modelagem. |Número inteiro |3-50 (6) |
| FbtMaxItemSetSize |Limites Olá número de itens em um conjunto frequente. |Número inteiro |2-3 (2) |
| FbtMinimalScore |Pontuação mínima que um conjunto frequente deve ter em ordem toobe incluído no hello retornados resultados. Olá superior hello melhor. |Duplo |0 e acima (0) |
| FbtSimilarityFunction |Define Olá toobe de função de similaridade usado pela compilação hello. Comparação de precisão favorece serendipity, ocorrência colegas favorece previsibilidade e Jaccard é um bom meio-termo entre Olá dois. |Cadeia de caracteres |cooccurrence, lift, jaccard (lift) |

### <a name="112-trigger-a-recommendation-build"></a>11.2. Disparar uma Compilação de Recomendação
  Por padrão, essa API vai disparar uma compilação de modelo de recomendação. tootrigger uma classificação de compilação (em ordem tooscore de recursos), variante de API de compilação Olá com parâmetro de tipo de compilação deve ser usado.

| Método HTTP | URI |
|:--- |:--- |
| POST |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |
| HEADER |`"Content-Type", "text/xml"` (Se estiver enviando o Corpo da solicitação) |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de saudação |
| userDescription |Identificador textual do catálogo de saudação. Observe que se você usar espaços você deve codificá-los com 20%. Consulte o exemplo acima.<br>Comprimento máximo: 50 |
| apiVersion |1.0 |
|  | |
| Corpo da solicitação |Se deixado em branco compilação Olá será executada com parâmetros de compilação saudação padrão.<br><br>Se você quiser parâmetros de compilação tooset hello, envie parâmetros de saudação como XML no corpo de saudação como Olá exemplo a seguir. (Consulte a seção de hello "parâmetros de compilação" para obter uma explicação dos parâmetros de saudação).`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>` |

**Resposta**:

Código de status HTTP: 200

Esta é uma API assíncrona. Você receberá uma ID de compilação como uma resposta. tooknow quando a compilação Olá terminou, você deve chamar hello "Obter compilações Status de um modelo de" API e localize essa compilação ID na resposta de saudação. Observe que uma compilação pode levar de toohours minutos dependendo do tamanho de saudação de dados de saudação.

Você não pode consumir recomendações até Olá compilar termina.

Status de compilação válidos:

* Criar - A solicitação de compilação foi criada.
* Em fila - A solicitação de compilação foi enviada e será enfileirada.
* Compilando - A compilação está em andamento.
* Sucesso - A compilação concluída com êxito.
* Erro - A compilação foi concluída com uma falha.
* Cancelado - A compilação foi cancelada.
* Cancelando - foi enviada uma solicitação de cancelamento para compilação de saudação.

Observe que compilação Olá que ID pode ser encontrada em Olá que caminho a seguir:`Feed\entry\content\properties\Id`

XML de OData

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">1000272</d:Id>
        <d:UserName m:type="Edm.String"></d:UserName>
        <d:ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:ModelId>
        <d:ModelName m:type="Edm.String">docTest</d:ModelName>
        <d:Type m:type="Edm.String">Recommendation</d:Type>
        <d:CreationTime m:type="Edm.String">2014-10-05T08:56:31.893</d:CreationTime>
        <d:Progress_BuildId m:type="Edm.String">1000272</d:Progress_BuildId>
        <d:Progress_ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:Progress_ModelId>
        <d:Progress_UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:Progress_UserName>
        <d:Progress_IsExecutionStarted m:type="Edm.String">false</d:Progress_IsExecutionStarted>
        <d:Progress_IsExecutionEnded m:type="Edm.String">false</d:Progress_IsExecutionEnded>
        <d:Progress_Percent m:type="Edm.String">0</d:Progress_Percent>
        <d:Progress_StartTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_StartTime>
        <d:Progress_EndTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_EndTime>
        <d:Progress_UpdateDateUTC m:type="Edm.String"></d:Progress_UpdateDateUTC>
        <d:Status m:type="Edm.String">Queued</d:Status>
        <d:Key1 m:type="Edm.String">UseFeaturesInModel</d:Key1>
        <d:Value1 m:type="Edm.String">False</d:Value1>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="113-trigger-build-recommendation-rank-or-fbt"></a>11.3. Disparar Compilação (Recomendação, Classificação ou FBT)
| Método HTTP | URI |
|:--- |:--- |
| POST |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&buildType=%27<buildType>%27&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&buildType=%27Ranking%27&apiVersion=%271.0%27` |
| HEADER |`"Content-Type", "text/xml"` (Se estiver enviando o Corpo da solicitação) |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de saudação |
| userDescription |Identificador textual do catálogo de saudação. Observe que se você usar espaços você deve codificá-los com 20%. Consulte o exemplo acima.<br>Comprimento máximo: 50 |
| buildType |Tipo de saudação compilação tooinvoke: <br/> -.'Recomendação' compilação de recomendação <br> - 'Classificação' para compilação de classificação <br/> - “Fbt” para compilação FBT |
| apiVersion |1.0 |
|  | |
| Corpo da solicitação |Se deixado em branco compilação Olá será executada com parâmetros de compilação saudação padrão.<br><br>Se você quiser tooset parâmetros de compilação, enviá-los como XML no corpo de saudação como em Olá exemplo a seguir. (Consulte a seção de hello "parâmetros de compilação" para uma explicação e uma lista completa de parâmetros de saudação).`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>` |

**Resposta**:

Código de status HTTP: 200

Esta é uma API assíncrona. Você receberá uma ID de compilação como uma resposta. tooknow quando a compilação Olá terminou, você deve chamar hello "Obter compilações Status de um modelo de" API e localize essa compilação ID na resposta de saudação. Observe que uma compilação pode levar de toohours minutos dependendo do tamanho de saudação de dados de saudação.

Você não pode consumir recomendações até Olá compilar termina.

Status de compilação válidos:

* Criado - O modelo foi criado.
* Na fila - A compilação do modelo foi disparada e está na fila.
* Criando - O modelo está sendo criado.
* Sucesso - A compilação concluída com êxito.
* Erro - A compilação foi concluída com uma falha.
* Cancelado - A compilação foi cancelada.
* Cancelando - A compilação está sendo cancelada.

Observe que compilação Olá que ID pode ser encontrada em Olá que caminho a seguir:`Feed\entry\content\properties\Id`

XML de OData

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">1000272</d:Id>
        <d:UserName m:type="Edm.String"></d:UserName>
        <d:ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:ModelId>
        <d:ModelName m:type="Edm.String">docTest</d:ModelName>
        <d:Type m:type="Edm.String">Recommendation</d:Type>
        <d:CreationTime m:type="Edm.String">2014-10-05T08:56:31.893</d:CreationTime>
        <d:Progress_BuildId m:type="Edm.String">1000272</d:Progress_BuildId>
        <d:Progress_ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:Progress_ModelId>
        <d:Progress_UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:Progress_UserName>
        <d:Progress_IsExecutionStarted m:type="Edm.String">false</d:Progress_IsExecutionStarted>
        <d:Progress_IsExecutionEnded m:type="Edm.String">false</d:Progress_IsExecutionEnded>
        <d:Progress_Percent m:type="Edm.String">0</d:Progress_Percent>
        <d:Progress_StartTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_StartTime>
        <d:Progress_EndTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_EndTime>
        <d:Progress_UpdateDateUTC m:type="Edm.String"></d:Progress_UpdateDateUTC>
        <d:Status m:type="Edm.String">Queued</d:Status>
        <d:Key1 m:type="Edm.String">UseFeaturesInModel</d:Key1>
        <d:Value1 m:type="Edm.String">False</d:Value1>
      </m:properties>
    </content>
      </entry>
    </feed>




### <a name="114-get-builds-status-of-a-model"></a>11.4. Obter status da compilação de um modelo
Recupera compilações e seus status para um modelo específico.

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de saudação |
| onlyLastBuild |Indica se tooreturn todos Olá criar histórico do modelo de saudação ou somente status de saudação da compilação mais recente do hello |
| apiVersion |1.0 |

**Resposta**:

Código de status HTTP: 200

resposta de saudação inclui uma entrada por compilação. Cada entrada tem Olá seguintes dados:

* `feed/entry/content/properties/UserName`-Nome de usuário de saudação.
* `feed/entry/content/properties/ModelName`-Nome do modelo de saudação.
* `feed/entry/content/properties/ModelId` - Identificador exclusivo do modelo.
* `feed/entry/content/properties/IsDeployed`-Se a compilação Olá é implantada (também conhecido como compilação ativa).
* `feed/entry/content/properties/BuildId` - Identificador exclusivo da compilação.
* `feed/entry/content/properties/BuildType`-Tipo de compilação de saudação.
* `feed/entry/content/properties/Status` - Status da compilação. Pode ser uma das seguintes Olá: erro, construção, na fila, cancelando, cancelado, êxito.
* `feed/entry/content/properties/StatusMessage`-Mensagem de status detalhadas (aplica-se somente os estados de toospecific).
* `feed/entry/content/properties/Progress` - Andamento da compilação (%).
* `feed/entry/content/properties/StartTime` - Hora de início da compilação.
* `feed/entry/content/properties/EndTime` - Hora de término da compilação.
* `feed/entry/content/properties/ExecutionTime` - Duração da compilação.
* `feed/entry/content/properties/ProgressStep`-Os detalhes sobre o estágio atual de saudação de uma compilação em andamento.

Status de compilação válidos:

* Criada - a entrada da solicitação de compilação foi criada.
* Em fila - a solicitação de build foi disparada e está na fila.
* Compilando - a build está em andamento.
* Sucesso - A compilação concluída com êxito.
* Erro - A compilação foi concluída com uma falha.
* Cancelado - A compilação foi cancelada.
* Cancelando - A compilação está sendo cancelada.

Valores válidos para o tipo de compilação:

* Classificação - compilação de classificação.
* Recomendação - compilação de recomendação.

XML de OData

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T17:51:10Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T17:51:10Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:UserName m:type="Edm.String">b-434e-b2c9-84935664ff20@dm.com</d:UserName>
                    <d:ModelName m:type="Edm.String">ModelName</d:ModelName>
                    <d:ModelId m:type="Edm.String">1d20c34f-dca1-4eac-8e5d-f299e4e4ad66</d:ModelId>
                    <d:IsDeployed m:type="Edm.String">true</d:IsDeployed>
                    <d:BuildId m:type="Edm.String">1000272</d:BuildId>
                    <d:BuildType m:type="Edm.String">Recommendation</d:BuildType>
                    <d:Status m:type="Edm.String">Success</d:Status>
                    <d:StatusMessage m:type="Edm.String"></d:StatusMessage>
                    <d:Progress m:type="Edm.String">0</d:Progress>
                    <d:StartTime m:type="Edm.String">2014-11-02T13:43:51</d:StartTime>
                    <d:EndTime m:type="Edm.String">2014-11-02T13:45:10</d:EndTime>
                    <d:ExecutionTime m:type="Edm.String">00:01:19</d:ExecutionTime>
                    <d:IsExecutionStarted m:type="Edm.String">false</d:IsExecutionStarted>
                    <d:ProgressStep m:type="Edm.String"></d:ProgressStep>
                </m:properties>
            </content>
        </entry>
    </feed>


### <a name="115-get-builds-status"></a>11.5. Obter Status da Compilação
Recupera os status da compilação de todos os modelos de um usuário

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=<bool>&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=true&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| onlyLastBuild |Indica se tooreturn todos Olá criar histórico do modelo de saudação ou somente status de saudação da compilação mais recente do hello. |
| apiVersion |1.0 |

**Resposta**:

Código de status HTTP: 200

resposta de saudação inclui uma entrada por compilação. Cada entrada tem Olá seguintes dados:

* `feed/entry/content/properties/UserName`-Nome de usuário de saudação.
* `feed/entry/content/properties/ModelName`-Nome do modelo de saudação.
* `feed/entry/content/properties/ModelId` - Identificador exclusivo do modelo.
* `feed/entry/content/properties/IsDeployed`-Se a compilação de saudação é implantada.
* `feed/entry/content/properties/BuildId` - Identificador exclusivo da compilação.
* `feed/entry/content/properties/BuildType`-Tipo de compilação de saudação.
* `feed/entry/content/properties/Status` - Status da compilação. Pode ser uma das seguintes Olá: erro, construção, na fila, cancelado, cancelando, êxito.
* `feed/entry/content/properties/StatusMessage`-Mensagem de status detalhadas (aplica-se somente os estados de toospecific).
* `feed/entry/content/properties/Progress` - Andamento da compilação (%).
* `feed/entry/content/properties/StartTime` - Hora de início da compilação.
* `feed/entry/content/properties/EndTime` - Hora de término da compilação.
* `feed/entry/content/properties/ExecutionTime` - Duração da compilação.
* `feed/entry/content/properties/ProgressStep`-Os detalhes sobre o estágio atual de saudação de uma compilação em andamento.

Status de compilação válidos:

* Criada - a entrada da solicitação de compilação foi criada.
* Em fila - a solicitação de build foi disparada e está na fila.
* Compilando - a build está em andamento.
* Sucesso - A compilação concluída com êxito.
* Erro - A compilação foi concluída com uma falha.
* Cancelado - A compilação foi cancelada.
* Cancelando - A compilação está sendo cancelada.

Valores válidos para o tipo de compilação:

* Classificação - compilação de classificação.
* Recomendação - compilação de recomendação.

XML de OData

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T18:41:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T18:41:21Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:UserName m:type="Edm.String">b-434e-b2c9-84935664ff20@dm.com</d:UserName>
                    <d:ModelName m:type="Edm.String">ModelName</d:ModelName>
                    <d:ModelId m:type="Edm.String">1d20c34f-dca1-4eac-8e5d-f299e4e4ad66</d:ModelId>
                    <d:IsDeployed m:type="Edm.String">true</d:IsDeployed>
                    <d:BuildId m:type="Edm.String">1000272</d:BuildId>
                    <d:BuildType m:type="Edm.String">Recommendation</d:BuildType>
                    <d:Status m:type="Edm.String">Success</d:Status>
                    <d:StatusMessage m:type="Edm.String"></d:StatusMessage>
                    <d:Progress m:type="Edm.String">0</d:Progress>
                    <d:StartTime m:type="Edm.String">2014-11-02T13:43:51</d:StartTime>
                    <d:EndTime m:type="Edm.String">2014-11-02T13:45:10</d:EndTime>
                    <d:ExecutionTime m:type="Edm.String">00:01:19</d:ExecutionTime>
                    <d:IsExecutionStarted m:type="Edm.String">false</d:IsExecutionStarted>
                    <d:ProgressStep m:type="Edm.String"></d:ProgressStep>
                </m:properties>
            </content>
        </entry>
    </feed>


### <a name="116-delete-build"></a>11.6. Excluir compilação
Exclui uma compilação.

OBSERVAÇÃO:  <br>Não é possível excluir uma compilação ativa. Olá modelo deve ser atualizada tooa compilação diferente de ativo antes de excluí-lo.<br>Não é possível excluir um build em andamento. Você deve cancelar a compilação Olá primeiro chamar <strong>cancelar a compilação</strong>.

| Método HTTP | URI |
|:--- |:--- |
| EXCLUIR |`<rootURI>/DeleteBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/DeleteBuild?buildId=%271500068%27&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| buildId |Identificador exclusivo da compilação de saudação. |
| apiVersion |1.0 |

**Resposta:**

Código de status HTTP: 200

### <a name="117-cancel-build"></a>11.7. Cancelar compilação
Cancela uma compilação que está no status de compilação.

| Método HTTP | URI |
|:--- |:--- |
| PUT |`<rootURI>/CancelBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/CancelBuild?buildId=%271500076%27&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| buildId |Identificador exclusivo da compilação de saudação. |
| apiVersion |1.0 |

**Resposta:**

Código de status HTTP: 200

### <a name="118-get-build-parameters"></a>11.8. Obter parâmetros de compilação
Recupera parâmetros de compilação.

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetBuildParameters?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/GetBuildParameters?buildId=%271000653%27&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| buildId |Identificador exclusivo da compilação de saudação. |
| apiVersion |1.0 |

**Resposta:**

Código de status HTTP: 200

Essa API retorna uma coleção de elementos de chave/valor. Cada elemento representa um parâmetro e seu valor:

* `feed/entry/content/properties/Key` - nome do parâmetro de build.
* `feed/entry/content/properties/Value` - valor do parâmetro de build.

Olá tabela a seguir mostra o valor de saudação que representa cada chave.

| Chave | Descrição | Tipo | Valor Válido |
|:--- |:--- |:--- |:--- |
| NumberOfModelIterations |número de saudação de iterações modelo Olá executa é refletido pela Olá tempo e hello precisão do modelo de computação geral. número mais alto de Olá Olá, você terá maior precisão do hello, mas Olá computação tempo irá demorar mais. |Número inteiro |10-50 |
| NumberOfModelDimensions |número de saudação de dimensões se relaciona toohello número do modelo de saudação 'recursos' tentará toofind dentro de seus dados. Aumentar o número de saudação de dimensões permitirá ajustar melhor os resultados de saudação em clusters menores. No entanto, muitas dimensões impedirá modelo Olá localização de correlações entre itens. |Número inteiro |10-40 |
| ItemCutOffLowerBound |Define Olá item inferior para condensador hello. Consulte o condensador de uso acima. |Número inteiro |2 ou mais (0 desabilita o condensador) |
| ItemCutOffUpperBound |Define Olá item limite superior condensador hello. Consulte o condensador de uso acima. |Número inteiro |2 ou mais (0 desabilita o condensador) |
| UserCutOffLowerBound |Define Olá usuário inferior para condensador hello. Consulte o condensador de uso acima. |Número inteiro |2 ou mais (0 desabilita o condensador) |
| UserCutOffUpperBound |Define Olá usuário limite superior condensador hello. Consulte o condensador de uso acima. |Número inteiro |2 ou mais (0 desabilita o condensador) |
| Descrição |Descrição da compilação. |Cadeia de caracteres |Qualquer texto, máximo de 512 caracteres |
| EnableModelingInsights |Permite que você toocompute métricas no modelo de recomendação de saudação. |Booliano |Verdadeiro/Falso |
| UseFeaturesInModel |Indica se os recursos podem ser usados no modelo de recomendação de saudação do pedido tooenhance. |Booliano |Verdadeiro/Falso |
| ModelingFeatureList |Lista separada por vírgulas de toobe de nomes de recurso usado na compilação de recomendação hello, na recomendação de saudação do tooenhance de ordem. |Cadeia de caracteres |Nomes de recurso, o too512 caracteres |
| AllowColdItemPlacement |Indica se a recomendação de saudação também enviar por push itens frios por meio de similaridade de recurso. |Booliano |Verdadeiro/Falso |
| EnableFeatureCorrelation |Indica se os recursos podem ser usados no raciocínio. |Booliano |Verdadeiro/Falso |
| ReasoningFeatureList |Lista separada por vírgulas de toobe de nomes de recurso usado para raciocínio sentenças (por exemplo, explicações de recomendação). |Cadeia de caracteres |Nomes de recurso, o too512 caracteres |

XML de OData

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get build parameters</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:50:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UseFeaturesInModel</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">AllowColdItemPlacement</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableFeatureCorrelation</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableModelingInsights</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelIterations</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
            <titletype="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelDimensions</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <linkrel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ModelingFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ReasoningFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">Description</d:Key>
                    <d:Value m:type="Edm.String">rankBuild</d:Value>
                </m:properties>
            </content>
        </entry>
    </feed>

## <a name="12-recommendation"></a>12. Recomendações
### <a name="121-get-item-recommendations-for-active-build"></a>12.1. Obter Recomendações de Item (para compilação ativa)
Obter recomendações de compilação de saudação ativo do tipo "Recomendação" ou "Fbt" com base em uma lista de itens de sementes (entrada).

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de saudação |
| itemIds |Lista separada por vírgulas de saudação itens toorecommend para. <br>Se compilação active Olá é do tipo FBT, em seguida, você pode enviar somente um item. <br>Comprimento máximo: 1024 |
| numberOfResults |Número de resultados necessários  <br> Máx.: 150 |
| includeMetatadata |Uso futuro, sempre falso |
| apiVersion |1.0 |

**Resposta:**

Código de status HTTP: 200

resposta de saudação inclui uma entrada por itens recomendados. Cada entrada tem Olá seguintes dados:

* `Feed\entry\content\properties\Id` - ID do item recomendado.
* `Feed\entry\content\properties\Name`-Nome do item de saudação.
* `Feed\entry\content\properties\Rating`-Classificação de recomendação de saudação; número mais alto significa maior confiança.
* `Feed\entry\content\properties\Reasoning` - Raciocínio da recomendação (por exemplo, explicações de recomendação).

resposta de exemplo Hello abaixo inclui 10 itens recomendados.

XML de OData

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">159</d:Id>
        <d:Name m:type="Edm.String">159</d:Name>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">52</d:Id>
        <d:Name m:type="Edm.String">52</d:Name>
        <d:Rating m:type="Edm.Double">0.539588900748721</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">35</d:Id>
        <d:Name m:type="Edm.String">35</d:Name>
        <d:Rating m:type="Edm.Double">0.53842946443853</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '35'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">124</d:Id>
        <d:Name m:type="Edm.String">124</d:Name>
        <d:Rating m:type="Edm.Double">0.536712832792886</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '124'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">120</d:Id>
        <d:Name m:type="Edm.String">120</d:Name>
        <d:Rating m:type="Edm.Double">0.533673023762878</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '120'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">96</d:Id>
        <d:Name m:type="Edm.String">96</d:Name>
        <d:Rating m:type="Edm.Double">0.532544826370521</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '96'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">69</d:Id>
        <d:Name m:type="Edm.String">69</d:Name>
        <d:Rating m:type="Edm.Double">0.531678607847759</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '69'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">172</d:Id>
        <d:Name m:type="Edm.String">172</d:Name>
        <d:Rating m:type="Edm.Double">0.530957821375951</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '172'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">155</d:Id>
        <d:Name m:type="Edm.String">155</d:Name>
        <d:Rating m:type="Edm.Double">0.529093541481333</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '155'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">32</d:Id>
        <d:Name m:type="Edm.String">32</d:Name>
        <d:Rating m:type="Edm.Double">0.528917978168322</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '32'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="122-get-item-recommendations-of-a-specific-build"></a>12.2. Obter Recomendações de Item (de uma compilação específica)
Obtenha recomendações de uma compilação específica do tipo “Recomendação” ou “Fbt”.

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de saudação |
| itemIds |Lista separada por vírgulas de saudação itens toorecommend para. <br>Se compilação active Olá é do tipo FBT, em seguida, você pode enviar somente um item. <br>Comprimento máximo: 1024 |
| numberOfResults |Número de resultados necessários  <br> Máx.: 150 |
| includeMetatadata |Uso futuro, sempre falso |
| buildId |Olá toouse id para esta solicitação de recomendação de compilação |
| apiVersion |1.0 |

**Resposta:**

Código de status HTTP: 200

resposta de saudação inclui uma entrada por itens recomendados. Cada entrada tem Olá seguintes dados:

* `Feed\entry\content\properties\Id` - ID do item recomendado.
* `Feed\entry\content\properties\Name`-Nome do item de saudação.
* `Feed\entry\content\properties\Rating`-Classificação de recomendação de saudação; número mais alto significa maior confiança.
* `Feed\entry\content\properties\Reasoning` - Raciocínio da recomendação (por exemplo, explicações de recomendação).

Veja um exemplo de resposta no 12.1

### <a name="123-get-fbt-recommendations-for-active-build"></a>12.3. Obter Recomendações de FBT (para compilação ativa)
Obter recomendações de compilação de ativo de saudação do tipo "Fbt" com base em um item de semente (entrada).

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=<double>&includeMetadata=false&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de saudação |
| itemId |Item toorecommend para. <br>Comprimento máximo: 1024 |
| numberOfResults |Número de resultados necessários  <br>Máx.: 150 |
| minimalScore |Pontuação mínima que um conjunto frequente deve ter em ordem toobe incluído no hello retornados resultados |
| includeMetatadata |Uso futuro, sempre falso |
| apiVersion |1.0 |

**Resposta:**

Código de status HTTP: 200

resposta de saudação inclui uma entrada por conjunto de itens Recomendados (um conjunto de itens que são geralmente comprados junto com o item de semente/entrada hello). Cada entrada tem Olá seguintes dados:

* `Feed\entry\content\properties\Id1` - ID do item recomendado.
* `Feed\entry\content\properties\Name1`-Nome do item de saudação.
* `Feed\entry\content\properties\Id2` - ID do segundo item recomendado (opcional).
* `Feed\entry\content\properties\Name2`-Nome do item 2 da saudação (opcional).
* `Feed\entry\content\properties\Rating`-Classificação de recomendação de saudação; número mais alto significa maior confiança.
* `Feed\entry\content\properties\Reasoning` - Raciocínio da recomendação (por exemplo, explicações de recomendação).

resposta de exemplo Hello abaixo inclui 3 conjuntos de itens recomendados.

XML de OData

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemId='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">159</d:Id1>
        <d:Name1 m:type="Edm.String">159</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">52</d:Id1>
        <d:Name1 m:type="Edm.String">52</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.533343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">35</d:Id1>
        <d:Name1 m:type="Edm.String">35</d:Name1>
        <d:Id2 m:type="Edm.String">102</d:Id2>
        <d:Name2 m:type="Edm.String">102</d:Name2>
        <d:Rating m:type="Edm.Double">0.523343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '35' and '102'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="124-get-fbt-recommendations-of-a-specific-build"></a>12.4. Obter Recomendações FBT (de uma compilação específica)
Obtenha recomendações de uma compilação específica do tipo "Fbt".

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=0.1&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de saudação |
| itemId |Item toorecommend para. <br>Comprimento máximo: 1024 |
| numberOfResults |Número de resultados necessários  <br>Máx.: 150 |
| minimalScore |Pontuação mínima que um conjunto frequente deve ter em ordem toobe incluído no hello retornados resultados |
| includeMetatadata |Uso futuro, sempre falso |
| buildId |Olá toouse id para esta solicitação de recomendação de compilação |
| apiVersion |1.0 |

**Resposta:**

Código de status HTTP: 200

resposta de saudação inclui uma entrada por conjunto de itens Recomendados (um conjunto de itens que são geralmente comprados junto com o item de semente/entrada hello). Cada entrada tem Olá seguintes dados:

* `Feed\entry\content\properties\Id1` - ID do item recomendado.
* `Feed\entry\content\properties\Name1`-Nome do item de saudação.
* `Feed\entry\content\properties\Id2` - ID do segundo item recomendado (opcional).
* `Feed\entry\content\properties\Name2`-Nome do item 2 da saudação (opcional).
* `Feed\entry\content\properties\Rating`-Classificação de recomendação de saudação; número mais alto significa maior confiança.
* `Feed\entry\content\properties\Reasoning` - Raciocínio da recomendação (por exemplo, explicações de recomendação).

Veja um exemplo de resposta no 12.3

### <a name="125-get-user-recommendations-for-active-build"></a>12.5. Obter Recomendações do Usuário (para compilação ativa)
Obtenha recomendações de usuário de uma compilação do tipo "Recomendação" marcada como compilação ativa.

Olá API retornará uma lista de item previsto de acordo com o toohello histórico de uso do usuário hello.

Observações: 

1. Não há nenhuma recomendação de usuário para a compilação FBT.
2. Se criar hello ativo é FBT esse método será retornará um erro.

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de saudação |
| userId |Identificador exclusivo do usuário Olá |
| numberOfResults |Número de resultados necessários  |
| includeMetatadata |Uso futuro, sempre falso |
| apiVersion |1.0 |

**Resposta:**

Código de status HTTP: 200

resposta de saudação inclui uma entrada por itens recomendados. Cada entrada tem Olá seguintes dados:

* `Feed\entry\content\properties\Id` - ID do item recomendado.
* `Feed\entry\content\properties\Name`-Nome do item de saudação.
* `Feed\entry\content\properties\Rating`-Classificação de recomendação de saudação; número mais alto significa maior confiança.
* `Feed\entry\content\properties\Reasoning` - Raciocínio da recomendação (por exemplo, explicações de recomendação).

Veja um exemplo de resposta no 12.1

### <a name="126-get-user-recommendations-with-item-list-for-active-build"></a>12.6. Obter recomendações de usuário com a lista de itens (para compilação ativa)
Obtenha recomendações de usuário de uma compilação do tipo "Recomendação" marcada como compilação ativa com uma lista de itens adicionais

Olá API retornará uma lista de item previsto de acordo com o toohello histórico de uso do usuário de saudação e itens fornecidos adicionais de saudação.

Observações: 

1. Não há nenhuma recomendação de usuário para a compilação FBT.
2. Se criar hello ativo é FBT esse método será retornará um erro.

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%2C1000%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de saudação |
| userId |Identificador exclusivo do usuário Olá |
| itemsIds |Lista separada por vírgulas de saudação itens toorecommend para. Comprimento máximo: 1024 |
| numberOfResults |Número de resultados necessários  |
| includeMetatadata |Uso futuro, sempre falso |
| apiVersion |1.0 |

**Resposta:**

Código de status HTTP: 200

resposta de saudação inclui uma entrada por itens recomendados. Cada entrada tem Olá seguintes dados:

* `Feed\entry\content\properties\Id` - ID do item recomendado.
* `Feed\entry\content\properties\Name`-Nome do item de saudação.
* `Feed\entry\content\properties\Rating`-Classificação de recomendação de saudação; número mais alto significa maior confiança.
* `Feed\entry\content\properties\Reasoning` - Raciocínio da recomendação (por exemplo, explicações de recomendação).

Veja um exemplo de resposta no 12.1

### <a name="127-get-user-recommendations--of-a-specific-build"></a>12.7. Obter Recomendações de Usuário (de uma compilação específica)
Obtenha recomendações de usuário de uma compilação específica do tipo "Recomendação".

Olá API retornará uma lista de item previsto, de acordo com o histórico de utilização de toohello de usuário de hello (utilizado na compilação específico Olá).

Observação: Não há nenhuma recomendação de usuário para a compilação FBT.

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de saudação |
| userId |Identificador exclusivo do usuário Olá |
| numberOfResults |Número de resultados necessários  |
| includeMetatadata |Uso futuro, sempre falso |
| buildId |Olá toouse id para esta solicitação de recomendação de compilação |
| apiVersion |1.0 |

**Resposta:**

Código de status HTTP: 200

resposta de saudação inclui uma entrada por itens recomendados. Cada entrada tem Olá seguintes dados:

* `Feed\entry\content\properties\Id` - ID do item recomendado.
* `Feed\entry\content\properties\Name`-Nome do item de saudação.
* `Feed\entry\content\properties\Rating`-Classificação de recomendação de saudação; número mais alto significa maior confiança.
* `Feed\entry\content\properties\Reasoning` - Raciocínio da recomendação (por exemplo, explicações de recomendação).

Veja um exemplo de resposta no 12.1

### <a name="128-get-user-recommendations-with-item-list-of-a-specific-build"></a>12.8. Obtenha Recomendações de Usuário com a lista de itens (de uma compilação específica)
Obter recomendações de usuário de uma versão específica do tipo "Recomendação" e a lista de saudação de itens adicionais.

Retorna uma lista de item previsto, de acordo com toohello histórico de uso do usuário hello e uma lista de itens adicional Olá Olá API.

Observação: Não há nenhuma recomendação de usuário para a compilação FBT.

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de saudação |
| userId |Identificador exclusivo do usuário Olá |
| itemIds |Lista separada por vírgulas de saudação itens toorecommend para. Comprimento máximo: 1024 |
| numberOfResults |Número de resultados necessários  |
| includeMetatadata |Uso futuro, sempre falso |
| buildId |Olá toouse id para esta solicitação de recomendação de compilação |
| apiVersion |1.0 |

**Resposta:**

Código de status HTTP: 200

resposta de saudação inclui uma entrada por itens recomendados. Cada entrada tem Olá seguintes dados:

* `Feed\entry\content\properties\Id` - ID do item recomendado.
* `Feed\entry\content\properties\Name`-Nome do item de saudação.
* `Feed\entry\content\properties\Rating`-Classificação de recomendação de saudação; número mais alto significa maior confiança.
* `Feed\entry\content\properties\Reasoning` - Raciocínio da recomendação (por exemplo, explicações de recomendação).

Veja um exemplo de resposta no 12.1

## <a name="13-user-usage-history"></a>13. Histórico de uso do usuário
Após a criação de um modelo de recomendação foi sistema Olá permitirá tooretrieve Olá histórico do usuário (usuário específico de itens tooa associado) usado para compilação de saudação.
Essa API permite histórico do usuário Olá tooretrieve

Observação: histórico de saudação do usuário está atualmente disponível apenas para compilações de recomendação.

### <a name="131-retrieve-user-history"></a>13.1 Recuperar o histórico do usuário
Recuperar Olá lista de item usado na Olá active compilar ou no hello especificado compilar para Olá id de usuário fornecida.

| Método HTTP | URI |
|:--- |:--- |
| GET |Obter o histórico de saudação do usuário para compilação active hello.<br/>`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&apiVersion=%271.0%27`<br/><br/>Obter o histórico de saudação do usuário para Olá fornecido compilação`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`<br/><br/>Exemplo:`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| modelId |Olá identificador exclusivo do modelo de saudação. |
| userId |Identificador exclusivo de saudação do usuário hello. |
| buildId |parâmetro opcional, permitir tooindicate de qual compilação histórico de saudação do usuário deve ser busca |
| apiVersion |1.0 |

**Resposta:**

Código de status HTTP: 200

resposta de saudação inclui uma entrada por itens recomendados. Cada entrada tem Olá seguintes dados:

* `Feed\entry\content\properties\Id` - ID do item recomendado.
* `Feed\entry\content\properties\Name`-Nome do item de saudação.
* `Feed\entry\content\properties\Rating` - N/A.
* `Feed\entry\content\properties\Reasoning` - N/A.

XML de OData

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get User History</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-05-26T15:32:47Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">CatalogItemsThatContainATokenEntity</title>
        <updated>2015-05-26T15:32:47Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Rating m:type="Edm.Double">0</d:Rating>
                <d:Reasoning m:type="Edm.String"/>
                <d:Metadata m:type="Edm.String"/>
                <d:FormattedRating m:type="Edm.Double" m:null="true"/>
            </m:properties>
        </content>
    </entry>
</feed>

## <a name="14-notifications"></a>14. Notificações
Recomendações de aprendizado de máquina do Azure cria notificações quando ocorrem erros persistentes no sistema de saudação. Há três tipos de notificações:

1. Falha na compilação – Essa notificação é disparada para cada falha de compilação.
2. Falha - esta notificação de processamento de aquisição de dados é disparada quando temos mais de 100 erros em Olá últimos 5 minutos no processamento de saudação de eventos de uso por modelo.
3. Falha de consumo de recomendação - essa notificação é disparada quando temos mais de 100 erros em Olá últimos 5 minutos no processamento de saudação de solicitações de recomendação por modelo.

### <a name="141-get-notifications"></a>14.1. Obter notificações
Recupera todas as notificações de Olá para todos os modelos ou para um único modelo.

| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetNotifications?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br>Obter todas as notificações para todos os modelos:<br>`<rootURI>/GetNotifications?apiVersion=%271.0%27`<br><br>Exemplo para obter notificações para um modelo específico:<br>`<rootURI>/GetNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%277` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| modelId |Parâmetro opcional. Quando omitido, você receberá todas as notificações para todos os modelos. <br>Valor válido: o identificador exclusivo do modelo de saudação. |
| apiVersion |1.0 |
|  | |
| Corpo da solicitação |NENHUM |

**Resposta:**

Código de status HTTP: 200

XML de OData

    hello response includes one entry per notification. Each entry has hello following data:
        * feed\entry\content\properties\UserName - Internal user name identification.
        * feed\entry\content\properties\ModelId - Model ID.
        * feed\entry\content\properties\Message - Notification message.
        * feed\entry\content\properties\DateCreated - Date that this notification was created in UTC format.
        * feed\entry\content\properties\NotificationType - Notification types. Values are BuildFailure, RecommendationFailure, and DataAquisitionFailure.

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of Notifications for a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-04T13:24:23Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'" />
        <entry>
                <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfNotificationsForAUserEntity</title>
            <updated>2014-11-04T13:24:23Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:UserName m:type="Edm.String">515506bc-3693-4dce-a5e2-81cb3e8efb56@dm.com</d:UserName>
                    <d:ModelId m:type="Edm.String">967136e8-f868-4258-9331-10d567f87fae</d:ModelId>
                    <d:Message m:type="Edm.String">Build failed for user</d:Message>
                    <d:DateCreated m:type="Edm.String">2014-11-04T13:23:14.383</d:DateCreated>
                    <d:NotificationType m:type="Edm.String">BuildFailure</d:NotificationType>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="142-delete-model-notifications"></a>14.2. Excluir as notificações de modelo
Exclui todas notificações de leitura de um modelo.

| Método HTTP | URI |
|:--- |:--- |
| EXCLUIR |`<rootURI>/DeleteModelNotifications?modelId=%<model_id>%27&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/DeleteModelNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de saudação |
| apiVersion |1.0 |
|  | |
| Corpo da solicitação |NENHUM |

**Resposta**:

Código de status HTTP: 200

### <a name="143-delete-user-notifications"></a>14.3. Excluir as notificações do usuário
Exclui todas as notificações de todos os modelos

| Método HTTP | URI |
|:--- |:--- |
| EXCLUIR |`<rootURI>/DeleteUserNotifications?apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| apiVersion |1.0 |
|  | |
| Corpo da solicitação |NENHUM |

**Resposta**:

Código de status HTTP: 200

## <a name="15-legal"></a>15. Legal
Este documento é fornecido "no estado em que se encontra". Informações e opiniões expressadas neste documento, incluindo URLs e outras referências a sites da Internet, podem ser alteradas sem aviso prévio.<br><br>
Alguns exemplos aqui representados são fornecidos somente para fins de ilustração e são fictícios. Nenhuma associação ou conexão real é intencional ou deve ser inferida.<br><br>
Este documento não dá nenhum direito legal tooany de propriedade intelectual de nenhum produto da Microsoft. Você pode copiar e usar este documento para fins de consulta interna.<br><br>
© 2015 Microsoft. Todos os direitos reservados.

