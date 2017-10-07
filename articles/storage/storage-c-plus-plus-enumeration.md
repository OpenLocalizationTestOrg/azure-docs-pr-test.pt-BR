---
title: recursos de armazenamento do Azure aaaList com hello biblioteca de cliente de armazenamento para C++ | Microsoft Docs
description: "Saiba como Olá toouse listando APIs na biblioteca de cliente de armazenamento do Microsoft Azure para contêineres de tooenumerate do C++, blobs, filas, tabelas e entidades."
documentationcenter: .net
services: storage
author: dineshmurthy
manager: jahogg
editor: tysonn
ms.assetid: 33563639-2945-4567-9254-bc4a7e80698f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: dineshm
ms.openlocfilehash: d20a86688938704c24339aa9a1145786783fea5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="list-azure-storage-resources-in-c"></a>Listar recursos do Armazenamento do Azure no C++
Operações de lista são toomany principais cenários de desenvolvimento com o armazenamento do Azure. Este artigo descreve como toomost com eficiência enumerar objetos no armazenamento do Azure usando Olá listando as APIs fornecidas no hello biblioteca de cliente de armazenamento do Microsoft Azure para C++.

> [!NOTE]
> Este guia tem como alvo hello biblioteca de cliente de armazenamento do Azure para C++ versão 2. x, que está disponível por meio de [NuGet](http://www.nuget.org/packages/wastorage) ou [GitHub](https://github.com/Azure/azure-storage-cpp).
> 
> 

Olá biblioteca de cliente de armazenamento fornece uma variedade de toolist métodos ou objetos de consulta no armazenamento do Azure. Este artigo aborda Olá os seguintes cenários:

* Listar contêineres em uma conta
* Listar blobs em um contêiner ou diretório virtual de blob
* Listar filas em uma conta
* Lista de tabelas em uma conta
* Consultar entidades em uma tabela

Cada um desses métodos é mostrado usando sobrecargas diferentes para diferentes cenários.

## <a name="asynchronous-versus-synchronous"></a>Assíncrono versus síncrono
Porque Olá biblioteca de cliente de armazenamento para C++ é criada sobre Olá [biblioteca C++ REST](https://github.com/Microsoft/cpprestsdk), inerentemente oferecemos suporte a operações assíncronas usando [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html). Por exemplo:

```cpp
pplx::task<list_blob_item_segment> list_blobs_segmented_async(continuation_token& token) const;
```

Operações síncronas encapsular operações assíncronas correspondente de saudação:

```cpp
list_blob_item_segment list_blobs_segmented(const continuation_token& token) const
{
    return list_blobs_segmented_async(token).get();
}
```

Se você estiver trabalhando com vários aplicativos ou serviços de threading, recomendamos que você use Olá async APIs diretamente, em vez de criar uma sincronização de saudação do thread toocall APIs, que afeta significativamente o desempenho.

## <a name="segmented-listing"></a>Listagem segmentada
escala de saudação do armazenamento em nuvem requer listagem segmentada. Por exemplo, você pode ter em um milhão de blobs em um contêiner de blob do Azure ou mais de um bilhão de entidades em uma Tabela do Azure. Esses não são números teóricos, são casos reais de uso de clientes.

Portanto, é impraticável toolist todos os objetos em uma única resposta. Em vez disso, você pode listar objetos usando a paginação. Cada Olá listando APIs tem um *segmentada* sobrecarga.

a resposta para uma operação de listagem segmentado Olá inclui:

* <i>_segment</i>, que contenha Olá conjunto de resultados retornados para um toohello única chamada de API de listagem.
* *continuation_token*, que é passado toohello próxima chamada na ordem tooget Olá próxima página de resultados. Quando não houver nenhuma mais tooreturn de resultados, o token de continuação Olá é nulo.

Por exemplo, uma chamada típica toolist todos os blobs em um contêiner podem parecer Olá trecho de código a seguir. Olá código está disponível no nosso [exemplos](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):

```cpp
// List blobs in hello blob container
azure::storage::continuation_token token;
do
{
    azure::storage::list_blob_item_segment segment = container.list_blobs_segmented(token);
    for (auto it = segment.results().cbegin(); it != segment.results().cend(); ++it)
{
    if (it->is_blob())
    {
        process_blob(it->as_blob());
    }
    else
    {
        process_diretory(it->as_directory());
    }
}

    token = segment.continuation_token();
}
while (!token.empty());
```

Observe que o número de saudação de resultados retornados em uma página pode ser controlado pelo parâmetro hello *max_results* sobrecarga de saudação do cada API, por exemplo:

```cpp
list_blob_item_segment list_blobs_segmented(const utility::string_t& prefix, bool use_flat_blob_listing,
    blob_listing_details::values includes, int max_results, const continuation_token& token,
    const blob_request_options& options, operation_context context)
```

Se você não especificar Olá *max_results* parâmetro, o padrão de saudação valor máximo de resultados de too5000 é retornado em uma única página.

Observe também que uma consulta em relação ao armazenamento de tabela do Azure pode retornar nenhum registro ou menos registros que valor Olá Olá *max_results* parâmetro que você especificou, mesmo se o token de continuação Olá não está vazio. Uma razão pode ser que consulta Olá não foi possível concluir em cinco segundos. Desde que o token de continuação Olá não estiver vazio, consulta Olá deve continuar e seu código não deve presumir que o tamanho de saudação dos resultados de segmento.

Olá recomendado codificação padrão para a maioria dos cenários está segmentada listando, que fornece o progresso explícito de listagem ou a consulta e como o serviço de saudação responde tooeach solicitação. Principalmente para aplicativos C++ ou serviços, controle de nível inferior de saudação listando progresso pode ajudar a memória de controle e de desempenho.

## <a name="greedy-listing"></a>Listagem greedy
Versões anteriores do hello biblioteca de cliente de armazenamento para C++ (versões 0.5.0 visualizar e anterior) incluído não segmentado listagem APIs para tabelas e filas, como no exemplo a seguir de saudação:

```cpp
std::vector<cloud_table> list_tables(const utility::string_t& prefix) const;
std::vector<table_entity> execute_query(const table_query& query) const;
std::vector<cloud_queue> list_queues() const;
```

Esses métodos foram implementados como wrappers de APIs segmentadas. Para cada resposta de listagem segmentada, código Olá acrescentado vetor de tooa resultados hello e retornar todos os resultados depois contêineres completo Olá foram examinados.

Essa abordagem pode funcionar quando a conta de armazenamento de saudação ou tabela contém um pequeno número de objetos. No entanto, com um aumento no número de saudação de objetos, memória Olá necessária pode aumentar sem limite, porque todos os resultados permaneceram na memória. Uma operação de listagem pode levar muito tempo, durante o qual Olá chamador não tinha informações sobre seu progresso.

Eles greedy listando APIs no SDK de saudação não existe no c#, Java, ou Olá ambiente JavaScript Node. js. tooavoid Olá possíveis problemas de uso dessas APIs greedy, removemos-los na versão 0.6.0 visualização.

Se o seu código estiver chamando essas APIs greedy:

```cpp
std::vector<azure::storage::table_entity> entities = table.execute_query(query);
for (auto it = entities.cbegin(); it != entities.cend(); ++it)
{
    process_entity(*it);
}
```

Em seguida, você deve modificar seu código toouse Olá segmentada listando APIs:

```cpp
azure::storage::continuation_token token;
do
{
    azure::storage::table_query_segment segment = table.execute_query_segmented(query, token);
    for (auto it = segment.results().cbegin(); it != segment.results().cend(); ++it)
    {
        process_entity(*it);
    }

    token = segment.continuation_token();
} while (!token.empty());
```

Especificando Olá *max_results* parâmetro do segmento hello, você pode equilibrar entre os números de saudação de solicitações e considerações de desempenho de toomeet de uso de memória do seu aplicativo.

Além disso, se você estiver usando APIs de listagem segmentada mas armazenar dados saudação em uma coleção de local em um estilo de "greedy", também recomendamos que você refatorar o toohandle código armazenando dados em uma coleção de local com cuidado em escala.

## <a name="lazy-listing"></a>Listagem lenta
Embora a listagem greedy gerado possíveis problemas, é conveniente se não houver muitos objetos no contêiner de saudação.

Se você também estiver usando c# ou Oracle Java SDKs, você deve estar familiarizado com o modelo de programação enumerável hello, que oferece um listagem, onde hello dados em um determinado deslocamento são apenas buscados se for necessário lento estilo. Em C++, o modelo com base no iterador de saudação também fornece uma abordagem semelhante.

Uma API típica de listagem lenta, que usa **list_blobs** por exemplo é semelhante ao seguinte:

```cpp
list_blob_item_iterator list_blobs() const;
```

Um trecho de código típico que usa Olá lento listagem padrão pode ter esta aparência:

```cpp
// List blobs in hello blob container
azure::storage::list_blob_item_iterator end_of_results;
for (auto it = container.list_blobs(); it != end_of_results; ++it)
{
    if (it->is_blob())
    {
        process_blob(it->as_blob());
    }
    else
    {
        process_directory(it->as_directory());
    }
}
```

Observe que a listagem lenta só está disponível no modo síncrono.

A listagem lenta, em comparação com a listagem greedy, busca dados somente quando necessário. Sob Olá coberturas, que acessa dados do armazenamento do Azure somente quando o iterador Avançar Olá move para o próximo segmento. Portanto, o uso de memória é controlado com um tamanho limitado e Olá operação é rápida.

Listagem lenta APIs são incluídas no hello biblioteca de cliente de armazenamento para C++ versão 2.2.0.

## <a name="conclusion"></a>Conclusão
Neste artigo, discutimos diferentes sobrecargas para listar as APIs de vários objetos em Olá biblioteca de cliente de armazenamento para C++. toosummarize:

* As APIs assíncronas são altamente recomendadas em vários cenários de threads.
* A listagem segmentada é recomendada para a maioria dos cenários.
* Listagem lenta é fornecida na biblioteca hello como um wrapper conveniente em cenários síncronos.
* Listando greedy não é recomendado e foi removido da biblioteca de saudação.

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre a biblioteca de cliente e o armazenamento do Azure para C++, consulte Olá recursos a seguir.

* [Como toouse armazenamento de Blob de C++](storage-c-plus-plus-how-to-use-blobs.md)
* [Como toouse o armazenamento de tabela do C++](storage-c-plus-plus-how-to-use-tables.md)
* [Como toouse armazenamento de fila de C++](storage-c-plus-plus-how-to-use-queues.md)
* [Documentação Biblioteca de Cliente de Armazenamento do Azure para API do C++.](http://azure.github.io/azure-storage-cpp/)
* [Blog da equipe de Armazenamento do Azure](http://blogs.msdn.com/b/windowsazurestorage/)
* [Documentação do Armazenamento do Azure](https://azure.microsoft.com/documentation/services/storage/)

