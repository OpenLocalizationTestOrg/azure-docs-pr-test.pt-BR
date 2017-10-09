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
ms.openlocfilehash: a76a5ce3cd690f32914f8f0c1f64273f13c5063e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="list-azure-storage-resources-in-c"></a><span data-ttu-id="11e17-103">Listar recursos do Armazenamento do Azure no C++</span><span class="sxs-lookup"><span data-stu-id="11e17-103">List Azure Storage resources in C++</span></span>
<span data-ttu-id="11e17-104">Operações de lista são toomany principais cenários de desenvolvimento com o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="11e17-104">Listing operations are key toomany development scenarios with Azure Storage.</span></span> <span data-ttu-id="11e17-105">Este artigo descreve como toomost com eficiência enumerar objetos no armazenamento do Azure usando Olá listando as APIs fornecidas no hello biblioteca de cliente de armazenamento do Microsoft Azure para C++.</span><span class="sxs-lookup"><span data-stu-id="11e17-105">This article describes how toomost efficiently enumerate objects in Azure Storage using hello listing APIs provided in hello Microsoft Azure Storage Client Library for C++.</span></span>

> [!NOTE]
> <span data-ttu-id="11e17-106">Este guia tem como alvo hello biblioteca de cliente de armazenamento do Azure para C++ versão 2. x, que está disponível por meio de [NuGet](http://www.nuget.org/packages/wastorage) ou [GitHub](https://github.com/Azure/azure-storage-cpp).</span><span class="sxs-lookup"><span data-stu-id="11e17-106">This guide targets hello Azure Storage Client Library for C++ version 2.x, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp).</span></span>
> 
> 

<span data-ttu-id="11e17-107">Olá biblioteca de cliente de armazenamento fornece uma variedade de toolist métodos ou objetos de consulta no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="11e17-107">hello Storage Client Library provides a variety of methods toolist or query objects in Azure Storage.</span></span> <span data-ttu-id="11e17-108">Este artigo aborda Olá os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="11e17-108">This article addresses hello following scenarios:</span></span>

* <span data-ttu-id="11e17-109">Listar contêineres em uma conta</span><span class="sxs-lookup"><span data-stu-id="11e17-109">List containers in an account</span></span>
* <span data-ttu-id="11e17-110">Listar blobs em um contêiner ou diretório virtual de blob</span><span class="sxs-lookup"><span data-stu-id="11e17-110">List blobs in a container or virtual blob directory</span></span>
* <span data-ttu-id="11e17-111">Listar filas em uma conta</span><span class="sxs-lookup"><span data-stu-id="11e17-111">List queues in an account</span></span>
* <span data-ttu-id="11e17-112">Lista de tabelas em uma conta</span><span class="sxs-lookup"><span data-stu-id="11e17-112">List tables in an account</span></span>
* <span data-ttu-id="11e17-113">Consultar entidades em uma tabela</span><span class="sxs-lookup"><span data-stu-id="11e17-113">Query entities in a table</span></span>

<span data-ttu-id="11e17-114">Cada um desses métodos é mostrado usando sobrecargas diferentes para diferentes cenários.</span><span class="sxs-lookup"><span data-stu-id="11e17-114">Each of these methods is shown using different overloads for different scenarios.</span></span>

## <a name="asynchronous-versus-synchronous"></a><span data-ttu-id="11e17-115">Assíncrono versus síncrono</span><span class="sxs-lookup"><span data-stu-id="11e17-115">Asynchronous versus synchronous</span></span>
<span data-ttu-id="11e17-116">Porque Olá biblioteca de cliente de armazenamento para C++ é criada sobre Olá [biblioteca C++ REST](https://github.com/Microsoft/cpprestsdk), inerentemente oferecemos suporte a operações assíncronas usando [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html).</span><span class="sxs-lookup"><span data-stu-id="11e17-116">Because hello Storage Client Library for C++ is built on top of hello [C++ REST library](https://github.com/Microsoft/cpprestsdk), we inherently support asynchronous operations by using [pplx::task](http://microsoft.github.io/cpprestsdk/classpplx_1_1task.html).</span></span> <span data-ttu-id="11e17-117">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="11e17-117">For example:</span></span>

```cpp
pplx::task<list_blob_item_segment> list_blobs_segmented_async(continuation_token& token) const;
```

<span data-ttu-id="11e17-118">Operações síncronas encapsular operações assíncronas correspondente de saudação:</span><span class="sxs-lookup"><span data-stu-id="11e17-118">Synchronous operations wrap hello corresponding asynchronous operations:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const continuation_token& token) const
{
    return list_blobs_segmented_async(token).get();
}
```

<span data-ttu-id="11e17-119">Se você estiver trabalhando com vários aplicativos ou serviços de threading, recomendamos que você use Olá async APIs diretamente, em vez de criar uma sincronização de saudação do thread toocall APIs, que afeta significativamente o desempenho.</span><span class="sxs-lookup"><span data-stu-id="11e17-119">If you are working with multiple threading applications or services, we recommend that you use hello async APIs directly instead of creating a thread toocall hello sync APIs, which significantly impacts your performance.</span></span>

## <a name="segmented-listing"></a><span data-ttu-id="11e17-120">Listagem segmentada</span><span class="sxs-lookup"><span data-stu-id="11e17-120">Segmented listing</span></span>
<span data-ttu-id="11e17-121">escala de saudação do armazenamento em nuvem requer listagem segmentada.</span><span class="sxs-lookup"><span data-stu-id="11e17-121">hello scale of cloud storage requires segmented listing.</span></span> <span data-ttu-id="11e17-122">Por exemplo, você pode ter em um milhão de blobs em um contêiner de blob do Azure ou mais de um bilhão de entidades em uma Tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="11e17-122">For example, you can have over a million blobs in an Azure blob container or over a billion entities in an Azure Table.</span></span> <span data-ttu-id="11e17-123">Esses não são números teóricos, são casos reais de uso de clientes.</span><span class="sxs-lookup"><span data-stu-id="11e17-123">These are not theoretical numbers, but real customer usage cases.</span></span>

<span data-ttu-id="11e17-124">Portanto, é impraticável toolist todos os objetos em uma única resposta.</span><span class="sxs-lookup"><span data-stu-id="11e17-124">It is therefore impractical toolist all objects in a single response.</span></span> <span data-ttu-id="11e17-125">Em vez disso, você pode listar objetos usando a paginação.</span><span class="sxs-lookup"><span data-stu-id="11e17-125">Instead, you can list objects using paging.</span></span> <span data-ttu-id="11e17-126">Cada Olá listando APIs tem um *segmentada* sobrecarga.</span><span class="sxs-lookup"><span data-stu-id="11e17-126">Each of hello listing APIs has a *segmented* overload.</span></span>

<span data-ttu-id="11e17-127">a resposta para uma operação de listagem segmentado Olá inclui:</span><span class="sxs-lookup"><span data-stu-id="11e17-127">hello response for a segmented listing operation includes:</span></span>

* <span data-ttu-id="11e17-128"><i>_segment</i>, que contenha Olá conjunto de resultados retornados para um toohello única chamada de API de listagem.</span><span class="sxs-lookup"><span data-stu-id="11e17-128"><i>_segment</i>, which contains hello set of results returned for a single call toohello listing API.</span></span>
* <span data-ttu-id="11e17-129">*continuation_token*, que é passado toohello próxima chamada na ordem tooget Olá próxima página de resultados.</span><span class="sxs-lookup"><span data-stu-id="11e17-129">*continuation_token*, which is passed toohello next call in order tooget hello next page of results.</span></span> <span data-ttu-id="11e17-130">Quando não houver nenhuma mais tooreturn de resultados, o token de continuação Olá é nulo.</span><span class="sxs-lookup"><span data-stu-id="11e17-130">When there are no more results tooreturn, hello continuation token is null.</span></span>

<span data-ttu-id="11e17-131">Por exemplo, uma chamada típica toolist todos os blobs em um contêiner podem parecer Olá trecho de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="11e17-131">For example, a typical call toolist all blobs in a container may look like hello following code snippet.</span></span> <span data-ttu-id="11e17-132">Olá código está disponível no nosso [exemplos](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):</span><span class="sxs-lookup"><span data-stu-id="11e17-132">hello code is available in our [samples](https://github.com/Azure/azure-storage-cpp/blob/master/Microsoft.WindowsAzure.Storage/samples/BlobsGettingStarted/Application.cpp):</span></span>

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

<span data-ttu-id="11e17-133">Observe que o número de saudação de resultados retornados em uma página pode ser controlado pelo parâmetro hello *max_results* sobrecarga de saudação do cada API, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="11e17-133">Note that hello number of results returned in a page can be controlled by hello parameter *max_results* in hello overload of each API, for example:</span></span>

```cpp
list_blob_item_segment list_blobs_segmented(const utility::string_t& prefix, bool use_flat_blob_listing,
    blob_listing_details::values includes, int max_results, const continuation_token& token,
    const blob_request_options& options, operation_context context)
```

<span data-ttu-id="11e17-134">Se você não especificar Olá *max_results* parâmetro, o padrão de saudação valor máximo de resultados de too5000 é retornado em uma única página.</span><span class="sxs-lookup"><span data-stu-id="11e17-134">If you do not specify hello *max_results* parameter, hello default maximum value of up too5000 results is returned in a single page.</span></span>

<span data-ttu-id="11e17-135">Observe também que uma consulta em relação ao armazenamento de tabela do Azure pode retornar nenhum registro ou menos registros que valor Olá Olá *max_results* parâmetro que você especificou, mesmo se o token de continuação Olá não está vazio.</span><span class="sxs-lookup"><span data-stu-id="11e17-135">Also note that a query against Azure Table storage may return no records, or fewer records than hello value of hello *max_results* parameter that you specified, even if hello continuation token is not empty.</span></span> <span data-ttu-id="11e17-136">Uma razão pode ser que consulta Olá não foi possível concluir em cinco segundos.</span><span class="sxs-lookup"><span data-stu-id="11e17-136">One reason might be that hello query could not complete in five seconds.</span></span> <span data-ttu-id="11e17-137">Desde que o token de continuação Olá não estiver vazio, consulta Olá deve continuar e seu código não deve presumir que o tamanho de saudação dos resultados de segmento.</span><span class="sxs-lookup"><span data-stu-id="11e17-137">As long as hello continuation token is not empty, hello query should continue, and your code should not assume hello size of segment results.</span></span>

<span data-ttu-id="11e17-138">Olá recomendado codificação padrão para a maioria dos cenários está segmentada listando, que fornece o progresso explícito de listagem ou a consulta e como o serviço de saudação responde tooeach solicitação.</span><span class="sxs-lookup"><span data-stu-id="11e17-138">hello recommended coding pattern for most scenarios is segmented listing, which provides explicit progress of listing or querying, and how hello service responds tooeach request.</span></span> <span data-ttu-id="11e17-139">Principalmente para aplicativos C++ ou serviços, controle de nível inferior de saudação listando progresso pode ajudar a memória de controle e de desempenho.</span><span class="sxs-lookup"><span data-stu-id="11e17-139">Particularly for C++ applications or services, lower-level control of hello listing progress may help control memory and performance.</span></span>

## <a name="greedy-listing"></a><span data-ttu-id="11e17-140">Listagem greedy</span><span class="sxs-lookup"><span data-stu-id="11e17-140">Greedy listing</span></span>
<span data-ttu-id="11e17-141">Versões anteriores do hello biblioteca de cliente de armazenamento para C++ (versões 0.5.0 visualizar e anterior) incluído não segmentado listagem APIs para tabelas e filas, como no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="11e17-141">Earlier versions of hello Storage Client Library for C++ (versions 0.5.0 Preview and earlier) included non-segmented listing APIs for tables and queues, as in hello following example:</span></span>

```cpp
std::vector<cloud_table> list_tables(const utility::string_t& prefix) const;
std::vector<table_entity> execute_query(const table_query& query) const;
std::vector<cloud_queue> list_queues() const;
```

<span data-ttu-id="11e17-142">Esses métodos foram implementados como wrappers de APIs segmentadas.</span><span class="sxs-lookup"><span data-stu-id="11e17-142">These methods were implemented as wrappers of segmented APIs.</span></span> <span data-ttu-id="11e17-143">Para cada resposta de listagem segmentada, código Olá acrescentado vetor de tooa resultados hello e retornar todos os resultados depois contêineres completo Olá foram examinados.</span><span class="sxs-lookup"><span data-stu-id="11e17-143">For each response of segmented listing, hello code appended hello results tooa vector and returned all results after hello full containers were scanned.</span></span>

<span data-ttu-id="11e17-144">Essa abordagem pode funcionar quando a conta de armazenamento de saudação ou tabela contém um pequeno número de objetos.</span><span class="sxs-lookup"><span data-stu-id="11e17-144">This approach might work when hello storage account or table contains a small number of objects.</span></span> <span data-ttu-id="11e17-145">No entanto, com um aumento no número de saudação de objetos, memória Olá necessária pode aumentar sem limite, porque todos os resultados permaneceram na memória.</span><span class="sxs-lookup"><span data-stu-id="11e17-145">However, with an increase in hello number of objects, hello memory required could increase without limit, because all results remained in memory.</span></span> <span data-ttu-id="11e17-146">Uma operação de listagem pode levar muito tempo, durante o qual Olá chamador não tinha informações sobre seu progresso.</span><span class="sxs-lookup"><span data-stu-id="11e17-146">One listing operation can take a very long time, during which hello caller had no information about its progress.</span></span>

<span data-ttu-id="11e17-147">Eles greedy listando APIs no SDK de saudação não existe no c#, Java, ou Olá ambiente JavaScript Node. js.</span><span class="sxs-lookup"><span data-stu-id="11e17-147">These greedy listing APIs in hello SDK do not exist in C#, Java, or hello JavaScript Node.js environment.</span></span> <span data-ttu-id="11e17-148">tooavoid Olá possíveis problemas de uso dessas APIs greedy, removemos-los na versão 0.6.0 visualização.</span><span class="sxs-lookup"><span data-stu-id="11e17-148">tooavoid hello potential issues of using these greedy APIs, we removed them in version 0.6.0 Preview.</span></span>

<span data-ttu-id="11e17-149">Se o seu código estiver chamando essas APIs greedy:</span><span class="sxs-lookup"><span data-stu-id="11e17-149">If your code is calling these greedy APIs:</span></span>

```cpp
std::vector<azure::storage::table_entity> entities = table.execute_query(query);
for (auto it = entities.cbegin(); it != entities.cend(); ++it)
{
    process_entity(*it);
}
```

<span data-ttu-id="11e17-150">Em seguida, você deve modificar seu código toouse Olá segmentada listando APIs:</span><span class="sxs-lookup"><span data-stu-id="11e17-150">Then you should modify your code toouse hello segmented listing APIs:</span></span>

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

<span data-ttu-id="11e17-151">Especificando Olá *max_results* parâmetro do segmento hello, você pode equilibrar entre os números de saudação de solicitações e considerações de desempenho de toomeet de uso de memória do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="11e17-151">By specifying hello *max_results* parameter of hello segment, you can balance between hello numbers of requests and memory usage toomeet performance considerations for your application.</span></span>

<span data-ttu-id="11e17-152">Além disso, se você estiver usando APIs de listagem segmentada mas armazenar dados saudação em uma coleção de local em um estilo de "greedy", também recomendamos que você refatorar o toohandle código armazenando dados em uma coleção de local com cuidado em escala.</span><span class="sxs-lookup"><span data-stu-id="11e17-152">Additionally, if you're using segmented listing APIs, but store hello data in a local collection in a "greedy" style, we also strongly recommend that you refactor your code toohandle storing data in a local collection carefully at scale.</span></span>

## <a name="lazy-listing"></a><span data-ttu-id="11e17-153">Listagem lenta</span><span class="sxs-lookup"><span data-stu-id="11e17-153">Lazy listing</span></span>
<span data-ttu-id="11e17-154">Embora a listagem greedy gerado possíveis problemas, é conveniente se não houver muitos objetos no contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="11e17-154">Although greedy listing raised potential issues, it is convenient if there are not too many objects in hello container.</span></span>

<span data-ttu-id="11e17-155">Se você também estiver usando c# ou Oracle Java SDKs, você deve estar familiarizado com o modelo de programação enumerável hello, que oferece um listagem, onde hello dados em um determinado deslocamento são apenas buscados se for necessário lento estilo.</span><span class="sxs-lookup"><span data-stu-id="11e17-155">If you're also using C# or Oracle Java SDKs, you should be familiar with hello Enumerable programming model, which offers a lazy-style listing, where hello data at a certain offset is only fetched if it is required.</span></span> <span data-ttu-id="11e17-156">Em C++, o modelo com base no iterador de saudação também fornece uma abordagem semelhante.</span><span class="sxs-lookup"><span data-stu-id="11e17-156">In C++, hello iterator-based template also provides a similar approach.</span></span>

<span data-ttu-id="11e17-157">Uma API típica de listagem lenta, que usa **list_blobs** por exemplo é semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="11e17-157">A typical lazy listing API, using **list_blobs** as an example, looks like this:</span></span>

```cpp
list_blob_item_iterator list_blobs() const;
```

<span data-ttu-id="11e17-158">Um trecho de código típico que usa Olá lento listagem padrão pode ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="11e17-158">A typical code snippet that uses hello lazy listing pattern might look like this:</span></span>

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

<span data-ttu-id="11e17-159">Observe que a listagem lenta só está disponível no modo síncrono.</span><span class="sxs-lookup"><span data-stu-id="11e17-159">Note that lazy listing is only available in synchronous mode.</span></span>

<span data-ttu-id="11e17-160">A listagem lenta, em comparação com a listagem greedy, busca dados somente quando necessário.</span><span class="sxs-lookup"><span data-stu-id="11e17-160">Compared with greedy listing, lazy listing fetches data only when necessary.</span></span> <span data-ttu-id="11e17-161">Sob Olá coberturas, que acessa dados do armazenamento do Azure somente quando o iterador Avançar Olá move para o próximo segmento.</span><span class="sxs-lookup"><span data-stu-id="11e17-161">Under hello covers, it fetches data from Azure Storage only when hello next iterator moves into next segment.</span></span> <span data-ttu-id="11e17-162">Portanto, o uso de memória é controlado com um tamanho limitado e Olá operação é rápida.</span><span class="sxs-lookup"><span data-stu-id="11e17-162">Therefore, memory usage is controlled with a bounded size, and hello operation is fast.</span></span>

<span data-ttu-id="11e17-163">Listagem lenta APIs são incluídas no hello biblioteca de cliente de armazenamento para C++ versão 2.2.0.</span><span class="sxs-lookup"><span data-stu-id="11e17-163">Lazy listing APIs are included in hello Storage Client Library for C++ in version 2.2.0.</span></span>

## <a name="conclusion"></a><span data-ttu-id="11e17-164">Conclusão</span><span class="sxs-lookup"><span data-stu-id="11e17-164">Conclusion</span></span>
<span data-ttu-id="11e17-165">Neste artigo, discutimos diferentes sobrecargas para listar as APIs de vários objetos em Olá biblioteca de cliente de armazenamento para C++.</span><span class="sxs-lookup"><span data-stu-id="11e17-165">In this article, we discussed different overloads for listing APIs for various objects in hello Storage Client Library for C++ .</span></span> <span data-ttu-id="11e17-166">toosummarize:</span><span class="sxs-lookup"><span data-stu-id="11e17-166">toosummarize:</span></span>

* <span data-ttu-id="11e17-167">As APIs assíncronas são altamente recomendadas em vários cenários de threads.</span><span class="sxs-lookup"><span data-stu-id="11e17-167">Async APIs are strongly recommended under multiple threading scenarios.</span></span>
* <span data-ttu-id="11e17-168">A listagem segmentada é recomendada para a maioria dos cenários.</span><span class="sxs-lookup"><span data-stu-id="11e17-168">Segmented listing is recommended for most scenarios.</span></span>
* <span data-ttu-id="11e17-169">Listagem lenta é fornecida na biblioteca hello como um wrapper conveniente em cenários síncronos.</span><span class="sxs-lookup"><span data-stu-id="11e17-169">Lazy listing is provided in hello library as a convenient wrapper in synchronous scenarios.</span></span>
* <span data-ttu-id="11e17-170">Listando greedy não é recomendado e foi removido da biblioteca de saudação.</span><span class="sxs-lookup"><span data-stu-id="11e17-170">Greedy listing is not recommended and has been removed from hello library.</span></span>

## <a name="next-steps"></a><span data-ttu-id="11e17-171">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="11e17-171">Next steps</span></span>
<span data-ttu-id="11e17-172">Para obter mais informações sobre a biblioteca de cliente e o armazenamento do Azure para C++, consulte Olá recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="11e17-172">For more information about Azure Storage and Client Library for C++, see hello following resources.</span></span>

* [<span data-ttu-id="11e17-173">Como toouse armazenamento de Blob de C++</span><span class="sxs-lookup"><span data-stu-id="11e17-173">How toouse Blob Storage from C++</span></span>](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="11e17-174">Como toouse o armazenamento de tabela do C++</span><span class="sxs-lookup"><span data-stu-id="11e17-174">How toouse Table Storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="11e17-175">Como toouse armazenamento de fila de C++</span><span class="sxs-lookup"><span data-stu-id="11e17-175">How toouse Queue Storage from C++</span></span>](../storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="11e17-176">Documentação Biblioteca de Cliente de Armazenamento do Azure para API do C++.</span><span class="sxs-lookup"><span data-stu-id="11e17-176">Azure Storage Client Library for C++ API documentation.</span></span>](http://azure.github.io/azure-storage-cpp/)
* [<span data-ttu-id="11e17-177">Blog da equipe de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="11e17-177">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* [<span data-ttu-id="11e17-178">Documentação do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="11e17-178">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)

