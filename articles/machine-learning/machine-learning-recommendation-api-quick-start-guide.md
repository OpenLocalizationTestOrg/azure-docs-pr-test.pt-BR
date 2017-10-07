---
title: "Início Rápido: API de Recomendações do Azure Machine Learning (versão 1)| Microsoft Docs"
description: "Recomendações do Azure Machine Learning - guia de início rápido"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 5bce1a4a-1ad6-473f-812b-84f800fdc09a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: d8f98e85f723a1104cb169b26d797934140979f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="quick-start-guide-for-hello-machine-learning-recommendations-api-version-1"></a>Guia de início rápido para Olá API de recomendações de aprendizado de máquina (versão 1)

> [!NOTE]
> Você deve começar a usar o hello [recomendações API cognitivas serviço](https://www.microsoft.com/cognitive-services/recommendations-api) em vez de nesta versão. Olá serviço cognitivas recomendações será substituído por esse serviço e todos os novos recursos de saudação serão desenvolvidos existe. Ele possui novos recursos como suporte ao processamento em lotes, um Gerenciador de API aprimorado, uma superfície de API mais limpa, uma experiência de inscrição/cobrança mais consistente etc.
>
> Saiba mais sobre [toohello migrando novo serviço cognitivas](http://aka.ms/recomigrate).
> 
> 

Este documento descreve como tooonboard toouse seu serviço ou aplicativo recomendações de aprendizado de máquina do Microsoft Azure. Você pode encontrar mais detalhes no hello API recomendações em Olá [Cortana Intelligence galeria](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="general-overview"></a>Visão geral
toouse recomendações de aprendizado de máquina do Azure, você precisará Olá tootake etapas a seguir:

* Criar um modelo - um modelo é um contêiner de seus dados de uso, dados de catálogo e modelo de recomendação de saudação.
* Importar dados de catálogo - um catálogo contém informações de metadados sobre itens de saudação. 
* Importar dados de uso: os dados de uso podem ser carregados de uma entre duas maneiras (ou ambas):
  * Carregando um arquivo que contém dados de uso de saudação.
  * Enviando eventos de aquisição de dados.
    Geralmente você carregar um arquivo de uso na ordem de toobe capaz de toocreate um modelo de recomendação inicial (inicialização) e usá-lo até que o sistema Olá reúne dados suficientes usando o formato de aquisição de dados hello.
* Criar um modelo de recomendação - esta é uma operação assíncrona no qual Olá sistema de recomendação usa todos os dados de uso de saudação e cria um modelo de recomendação. Essa operação pode levar vários minutos ou várias horas, dependendo da saudação o tamanho dos dados de saudação e Olá criar parâmetros de configuração. Quando disparo compilação hello, você obterá uma ID de compilação. Use-toocheck quando o processo de compilação Olá terminou antes de iniciar tooconsume recomendações.
* Consumir recomendações - Obtenha recomendações para um item específico ou uma lista de itens.

Todas as etapas de saudação acima são feitas por meio de saudação API de recomendações de aprendizado de máquina do Azure.  Você pode baixar um aplicativo de exemplo que implementa a cada uma dessas etapas de saudação [Galeria também.](http://1drv.ms/1xeO2F3)

## <a name="limitations"></a>Limitações
* número máximo de saudação de modelos por assinatura é 10.
* número máximo de saudação de itens que pode conter um catálogo é 100.000.
* número máximo de saudação de pontos de uso que são mantidos é ~ 5.000.000. Olá mais antigo será excluído se novas serão carregadas ou relatadas.
* tamanho máximo de saudação de dados que podem ser enviados no POST (por exemplo, importar dados de catálogo, importar dados de uso) é de 200MB.
* Olá número de transações por segundo para uma compilação de modelo de recomendação não está ativo é ~ 2TPS. Uma compilação de modelo de recomendação está ativa pode conter backup too20TPS.

## <a name="integration"></a>Integração
### <a name="authentication"></a>Autenticação
Microsoft Azure Marketplace oferece suporte a um método de autenticação básica ou OAuth hello. Você pode localizar facilmente Olá chaves de conta navegando toohello chaves no marketplace de saudação em [as configurações de conta](https://datamarket.azure.com/account/keys). 

#### <a name="basic-authentication"></a>Autenticação básica
Adicione o cabeçalho de autorização hello:

    Authorization: Basic <creds>

    Where <creds> = ConvertToBase64("AccountKey:" + yourAccountKey);  

Converter tooBase64 (c#)

    var bytes = Encoding.UTF8.GetBytes("AccountKey:" + yourAccountKey);
    var creds = Convert.ToBase64String(bytes);

Converter tooBase64 (JavaScript)

    var creds = window.btoa("AccountKey" + ":" + yourAccountKey);




### <a name="service-uri"></a>URI de serviço
Olá URI raiz do serviço para Olá APIs de recomendações de aprendizado de máquina do Azure é [aqui.](https://api.datamarket.azure.com/amla/recommendations/v2/)

URI do serviço completo Olá é expressa usando elementos da especificação de OData hello.

### <a name="api-version"></a>Versão da API
Cada chamada de API terá, no final do hello, um parâmetro de consulta chamado apiVersion que deve ser definido muito "1.0".

### <a name="ids-are-case-sensitive"></a>IDs diferenciam minúsculas e maiúsculas
IDs, retornados por qualquer Olá APIs, diferenciam maiusculas de minúsculas e devem ser usadas como tal quando passados como parâmetros em chamadas API subsequentes. Por exemplo, IDS de modelo e de catálogo diferenciam maiúsculas de minúsculas.

### <a name="create-a-model"></a>Criar um modelo
Criando uma solicitação para "criar modelo":

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
  Observe que a ID do modelo Olá diferencia maiusculas de minúsculas.

XML de OData

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Create A New Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:35:21Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">CreateANewModelEntity2</title>
    <updated>2014-10-05T06:35:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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


### <a name="import-catalog-data"></a>Importar dados de catálogo
Se você carregar vários catálogo arquivos toohello mesmo modelo com várias chamadas, inserimos somente Olá novos itens de catálogo. Itens existentes permanecerão com seus valores originais hello.

| Método HTTP | URI |
|:--- |:--- |
| POST |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de saudação (diferencia maiusculas de minúsculas) |
| nome do arquivo |Identificador textual do catálogo de saudação.<br>São permitidos apenas letras (A-Z, a-z), números (0-9), hifens (-) e sublinhado (_).<br>Comprimento máximo: 50 |
| apiVersion |1.0 |
|  | |
| Corpo da solicitação |Dados de catálogo. Formato:<br>`<Item Id>,<Item Name>,<Item Category>[,<description>]`<br><br><table><tr><th>Nome</th><th>Obrigatório</th><th>Tipo</th><th>Descrição</th></tr><tr><td>Id do item</td><td>Sim</td><td>Alfanumérico, comprimento máximo 50</td><td>Identificador exclusivo de um item</td></tr><tr><td>Nome do Item</td><td>Sim</td><td>Alfanumérico, comprimento máximo 255</td><td>Nome do item</td></tr><tr><td>Categoria do Item</td><td>Sim</td><td>Alfanumérico, comprimento máximo 255</td><td>Categoria toowhich que este item pertence (por exemplo, livros de culinária Drama...)</td></tr><tr><td>Descrição</td><td>Não</td><td>Alfanumérico, comprimento máximo 4000</td><td>Descrição deste item</td></tr></table><br>O tamanho máximo do arquivo é de 200 MB.<br><br>Exemplo:<br><code>2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book<br>21bf8088-b6c0-4509-870c-e1c7ac78304a,hello Forgetting Room: A Fiction (Byzantium Book),Book<br>3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book<br>552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book</code> |

**Resposta**:

Código de status HTTP: 200

* `Feed\entry\content\properties\LineCount` – O número de linhas aceitas.
* `Feed\entry\content\properties\ErrorCount`-Número de linhas que não foram inseridas devido a erro tooan.

XML de OData

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
          <subtitle type="text">Import catalog file</subtitle>
          <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:58:04Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">ImportCatalogFileEntity2</title>
    <updated>2014-10-05T06:58:04Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">4</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
      </m:properties>
    </content>
      </entry>
    </feed>


### <a name="import-usage-data"></a>Importar dados de uso
#### <a name="uploading-a-file"></a>Carregar um arquivo
Esta seção mostra como os dados de uso tooupload usando um arquivo. Você pode chamar essa API várias vezes com dados de uso. Todos os dados de uso serão salvos para todas as chamadas.

| Método HTTP | URI |
|:--- |:--- |
| POST |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de saudação (diferencia maiusculas de minúsculas) |
| nome do arquivo |Identificador textual do catálogo de saudação.<br>São permitidos apenas letras (A-Z, a-z), números (0-9), hifens (-) e sublinhado (_).<br>Comprimento máximo: 50 |
| apiVersion |1.0 |
|  | |
| Corpo da solicitação |Dados de uso. Formato:<br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th>Nome</th><th>Obrigatório</th><th>Tipo</th><th>Descrição</th></tr><tr><td>Id de usuário</td><td>Sim</td><td>Alfanumérico</td><td>Identificador exclusivo de um usuário</td></tr><tr><td>Id do item</td><td>Sim</td><td>Alfanumérico, comprimento máximo 50</td><td>Identificador exclusivo de um item</td></tr><tr><td>Hora</td><td>Não</td><td>Data no formato: AAAA/MM/DDTHH:MM:SS (por exemplo, 2013/06/20T10:00:00)</td><td>Hora dos dados</td></tr><tr><td>Evento</td><td>Não, se fornecido, também deve colocar a data</td><td>Um dos seguintes hello:<br>• Clique<br>• RecommendationClick<br>•    AddShopCart<br>• RemoveShopCart<br>• Compra</td><td></td></tr></table><br>O tamanho máximo do arquivo é de 200 MB.<br><br>Exemplo:<br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

**Resposta**:

Código de status HTTP: 200

* `Feed\entry\content\properties\LineCount` – O número de linhas aceitas.
* `Feed\entry\content\properties\ErrorCount`-Número de linhas que não foram inseridas devido a erro tooan.
* `Feed\entry\content\properties\FileId` – Identificador do arquivo.

XML de OData

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Add bulk usage data (usage file)</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T07:21:44Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">AddBulkUsageDataUsageFileEntity2</title>
    <updated>2014-10-05T07:21:44Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">33</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
        <d:FileId m:type="Edm.String">fead7c1c-db01-46c0-872f-65bcda36025d</d:FileId>
      </m:properties>
    </content>
      </entry>
    </feed>


#### <a name="using-data-acquisition"></a>Usando a aquisição de dados
Esta seção mostra como eventos toosend real tempo recomendações tooAzure de aprendizado de máquina, normalmente a partir de seu site.

| Método HTTP | URI |
|:--- |:--- |
| POST |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| apiVersion |1.0 |
|  | |
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
            <PurchaseItems>
                <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
                <Count>3</Count>
            </PurchaseItems>
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

### <a name="build-a-recommendation-model"></a>Criar um modelo de recomendação
| Método HTTP | URI |
|:--- |:--- |
| POST |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de saudação (diferencia maiusculas de minúsculas) |
| userDescription |Identificador textual do catálogo de saudação. Observe que se você usar espaços você deve codificá-los com 20%. Consulte o exemplo acima.<br>Comprimento máximo: 50 |
| apiVersion |1.0 |
|  | |
| Corpo da solicitação |NENHUM |

**Resposta**:

Código de status HTTP: 200

Esta é uma API assíncrona. Você receberá uma ID de compilação como uma resposta. tooknow quando a compilação Olá terminou, você deve chamar hello "Obter compilações Status de um modelo de" API e localize essa compilação ID na resposta de saudação. Observe que uma compilação pode levar de toohours minutos dependendo do tamanho de saudação de dados de saudação.

Você não pode consumir recomendações até Olá compilar termina.

Status de compilação válidos:

* Criado – O modelo foi criado.
* Na fila – A compilação do modelo foi disparada e está na fila.
* Criando – O modelo está sendo criado.
* Sucesso – A compilação concluída com êxito.
* Erro – A compilação foi concluída com uma falha.
* Cancelado – A compilação foi cancelada.
* Cancelando – A compilação está sendo cancelada.

Observe que compilação Olá que ID pode ser encontrada em Olá que caminho a seguir:`Feed\entry\content\properties\Id`

XML de OData

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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

### <a name="get-build-status-of-a-model"></a>Obter status da compilação de um modelo
| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de saudação (diferencia maiusculas de minúsculas) |
| onlyLastBuild |Indica se tooreturn todos Olá criar histórico do modelo de saudação ou somente status de saudação da compilação mais recente do hello. |
| apiVersion |1.0 |

**Resposta**:

Código de status HTTP: 200

resposta de saudação inclui uma entrada por compilação. Cada entrada tem Olá seguintes dados:

* `feed/entry/content/properties/UserName`– Nome do usuário de saudação.
* `feed/entry/content/properties/ModelName`– Nome do modelo de saudação.
* `feed/entry/content/properties/ModelId` – Identificador exclusivo do modelo.
* `feed/entry/content/properties/IsDeployed`– Se o build Olá é implantado (também conhecido como compilação ativa).
* `feed/entry/content/properties/BuildId` – Identificador exclusivo da compilação.
* `feed/entry/content/properties/BuildType`-Tipo de compilação de saudação.
* `feed/entry/content/properties/Status` – Status da compilação. Pode ser uma das seguintes Olá: erro, construção, na fila, cancelar, cancelado, sucesso
* `feed/entry/content/properties/StatusMessage`– Mensagem de status detalhadas (aplica-se somente os estados de toospecific).
* `feed/entry/content/properties/Progress` – Andamento da compilação (%).
* `feed/entry/content/properties/StartTime` – Hora de início da compilação.
* `feed/entry/content/properties/EndTime` – Hora de término da compilação.
* `feed/entry/content/properties/ExecutionTime` – Duração da compilação.
* `feed/entry/content/properties/ProgressStep`– Os detalhes sobre o estágio atual de saudação que é uma compilação em andamento no.

Status de compilação válidos:

* Criada - a entrada da solicitação de compilação foi criada.
* Em fila – a solicitação de build foi disparada e está na fila.
* Compilando – a build está em andamento.
* Sucesso – A compilação concluída com êxito.
* Erro – A compilação foi concluída com uma falha.
* Cancelado – A compilação foi cancelada.
* Cancelando – A compilação está sendo cancelada.

Valores válidos para o tipo de compilação:

* Classificação - compilação de classificação. (Detalhes da compilação para classificação, consulte o documento de "Documentação de recomendação de aprendizado de máquina API" toohello).
* Recomendação - compilação de recomendação.
* Fbt - Build de frequentemente comprados juntos.

XML de OData

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get builds status of a model</subtitle>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T17:51:10Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'" />
    <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetBuildsStatusEntity</title>
    <updated>2014-11-05T17:51:10Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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


### <a name="get-recommendations"></a>Obter recomendações
| Método HTTP | URI |
|:--- |:--- |
| GET |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| modelId |Identificador exclusivo do modelo de saudação (diferencia maiusculas de minúsculas) |
| itemIds |Lista separada por vírgulas de saudação itens toorecommend para.<br>Comprimento máximo: 1024 |
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

XML de OData

resposta de exemplo Hello abaixo inclui 10 itens recomendados:

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
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

### <a name="update-model"></a>Atualizar modelo
Você pode atualizar a descrição do modelo hello ou Olá ID do ativo de compilação.
*ID de compilação ativa* – cada compilação para cada modelo tem uma ID de compilação. ID de compilação active Olá é Olá primeira compilação bem-sucedida cada novo modelo. Depois que você tiver uma ID de ativo de compilação e fazer compilações adicionais para Olá mesmo modelo, você precisa tooexplicitly defini-lo hello padrão criar ID se desejar. Quando você consome recomendações, se você não especificar a ID de compilação de saudação que você deseja toouse, padrão Olá um será usado automaticamente.

Esse mecanismo permite que você - depois de um modelo de recomendação em produção - toobuild novos modelos e testá-las antes de promovê-los tooproduction.

| Método HTTP | URI |
|:--- |:--- |
| PUT |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><br>Exemplo:<br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| Nome do Parâmetro | Valores Válidos |
|:--- |:--- |
| ID |Identificador exclusivo do modelo de saudação (diferencia maiusculas de minúsculas) |
| apiVersion |1.0 |
|  | |
| Corpo da solicitação |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`   <Description>New Description</Description>`<br>`          <ActiveBuildId>-1</ActiveBuildId>`<br>`</ModelUpdateParams>`<br><br>Observe que a descrição de marcas Olá XML e ActiveBuildId são opcionais. Se você não quiser tooset descrição ou ActiveBuildId, remova a marca de inteiro de hello. |

**Resposta**:

Código de status HTTP: 200

XML de OData

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Update an Existing Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T10:27:17Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'" />
    </feed>

## <a name="legal"></a>Legal
Este documento é fornecido "no estado em que se encontra". As informações e opiniões expressadas neste documento, incluindo URLs e outras referências a sites da Internet, podem ser alteradas sem aviso prévio. Alguns exemplos aqui representados são fornecidos somente para fins de ilustração e são fictícios. Nenhuma associação ou conexão real é intencional ou deve ser inferida. Este documento não dá nenhum direito legal tooany de propriedade intelectual de nenhum produto da Microsoft. Você pode copiar e usar este documento para fins de consulta interna. © 2014 Microsoft. Todos os direitos reservados. 

