---
title: aaaHow toouse Blitline para processamento de imagem - guia de recursos do Azure
description: "Saiba como Olá toouse Blitline serviço tooprocess imagens dentro de um aplicativo do Azure."
services: 
documentationcenter: .net
author: blitline-dev
manager: jason@blitline.com
editor: jason@blitline.com
ms.assetid: 6c711248-0e52-4895-ba9e-8395628de924
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2014
ms.author: support@blitline.com
ms.openlocfilehash: 328fd177e25f45f29f8ad8e142d02b46017a858e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blitline-with-azure-and-azure-storage"></a><span data-ttu-id="e37c9-103">Como toouse Blitline com o Azure e armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="e37c9-103">How toouse Blitline with Azure and Azure Storage</span></span>
<span data-ttu-id="e37c9-104">Este guia explica como tooaccess Blitline como toosubmit trabalhos tooBlitline e serviços.</span><span class="sxs-lookup"><span data-stu-id="e37c9-104">This guide will explain how tooaccess Blitline services and how toosubmit jobs tooBlitline.</span></span>

## <a name="what-is-blitline"></a><span data-ttu-id="e37c9-105">O que é Blitline?</span><span class="sxs-lookup"><span data-stu-id="e37c9-105">What is Blitline?</span></span>
<span data-ttu-id="e37c9-106">Blitline é uma serviço que fornece processamento de imagem de nível empresarial em uma fração do preço de saudação que custaria toobuild de processamento de imagens baseado em nuvem-lo por conta própria.</span><span class="sxs-lookup"><span data-stu-id="e37c9-106">Blitline is a cloud-based image processing service that provides enterprise level image processing at a fraction of hello price that it would cost toobuild it yourself.</span></span>

<span data-ttu-id="e37c9-107">fato Olá é que o processamento de imagem foi feito repetidamente, geralmente recriado do início de saudação para cada site.</span><span class="sxs-lookup"><span data-stu-id="e37c9-107">hello fact is that image processing has been done over and over again, usually rebuilt from hello ground up for each and every website.</span></span> <span data-ttu-id="e37c9-108">Sabemos disso porque os compilamos milhões de vezes também.</span><span class="sxs-lookup"><span data-stu-id="e37c9-108">We realize this because we’ve built them a million times too.</span></span> <span data-ttu-id="e37c9-109">Um dia, decidimos que talvez fosse o momento de simplesmente fazê-lo para todas as pessoas.</span><span class="sxs-lookup"><span data-stu-id="e37c9-109">One day we decided that perhaps it‘s time we just do it for everyone.</span></span> <span data-ttu-id="e37c9-110">Sabemos como toodo-la, toodo-rápida e eficientemente e salve todos funcionam no hello enquanto isso.</span><span class="sxs-lookup"><span data-stu-id="e37c9-110">We know how toodo it, toodo it fast and efficiently, and save everyone work in hello meantime.</span></span>

<span data-ttu-id="e37c9-111">Para obter mais informações, consulte [http://www.blitline.com](http://www.blitline.com).</span><span class="sxs-lookup"><span data-stu-id="e37c9-111">For more information, see [http://www.blitline.com](http://www.blitline.com).</span></span>

## <a name="what-blitline-is-not"></a><span data-ttu-id="e37c9-112">O que o Blitline NÃO é...</span><span class="sxs-lookup"><span data-stu-id="e37c9-112">What Blitline is NOT...</span></span>
<span data-ttu-id="e37c9-113">tooclarify que Blitline é útil para, ele é geralmente mais fácil tooidentify que Blitline não antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="e37c9-113">tooclarify what Blitline is useful for, it is often easier tooidentify what Blitline does NOT do before moving forward.</span></span>

* <span data-ttu-id="e37c9-114">Blitline não tem imagens de tooupload de widgets HTML.</span><span class="sxs-lookup"><span data-stu-id="e37c9-114">Blitline does NOT have HTML widgets tooupload images.</span></span> <span data-ttu-id="e37c9-115">Você deve ter as imagens disponíveis publicamente ou com permissões restritas disponíveis para Blitline tooreach.</span><span class="sxs-lookup"><span data-stu-id="e37c9-115">You must have images available publicly or with restricted permissions available for Blitline tooreach.</span></span>
* <span data-ttu-id="e37c9-116">O Blitline NÃO faz o processamento de imagens ao vivo, como o Aviary.com.</span><span class="sxs-lookup"><span data-stu-id="e37c9-116">Blitline does NOT do live image processing, like Aviary.com</span></span>
* <span data-ttu-id="e37c9-117">Blitline não aceita carregamentos de imagem, não é possível enviar seu tooBlitline imagens diretamente.</span><span class="sxs-lookup"><span data-stu-id="e37c9-117">Blitline does NOT accept image uploads, you cannot push your images tooBlitline directly.</span></span> <span data-ttu-id="e37c9-118">Você deve enviá-las tooAzure armazenamento ou outros locais que blitline oferece suporte e, em seguida, conte-Blitline onde toogo obtê-los.</span><span class="sxs-lookup"><span data-stu-id="e37c9-118">You must push them tooAzure Storage or other places Blitline supports and then tell Blitline where toogo get them.</span></span>
* <span data-ttu-id="e37c9-119">O Blitline é massivamente paralelo e NÃO faz nenhum processamento síncrono.</span><span class="sxs-lookup"><span data-stu-id="e37c9-119">Blitline is massively parallel and does NOT do any synchronous processing.</span></span> <span data-ttu-id="e37c9-120">Ou seja, você deve nos fornecer um postback_url para que possamos informar a conclusão do processamento.</span><span class="sxs-lookup"><span data-stu-id="e37c9-120">Meaning you must give us a postback_url and we can tell you when we are done processing.</span></span>

## <a name="create-a-blitline-account"></a><span data-ttu-id="e37c9-121">Criar uma conta do Blitline</span><span class="sxs-lookup"><span data-stu-id="e37c9-121">Create a Blitline account</span></span>
[!INCLUDE [blitline-signup](../includes/blitline-signup.md)]

## <a name="how-toocreate-a-blitline-job"></a><span data-ttu-id="e37c9-122">Como toocreate um trabalho Blitline</span><span class="sxs-lookup"><span data-stu-id="e37c9-122">How toocreate a Blitline job</span></span>
<span data-ttu-id="e37c9-123">Blitline usa JSON toodefine Olá ações que você deseja tootake em uma imagem.</span><span class="sxs-lookup"><span data-stu-id="e37c9-123">Blitline uses JSON toodefine hello actions you want tootake on an image.</span></span> <span data-ttu-id="e37c9-124">Esse JSON é composto de alguns campos simples.</span><span class="sxs-lookup"><span data-stu-id="e37c9-124">This JSON is composed of a few simple fields.</span></span>

<span data-ttu-id="e37c9-125">exemplo de Hello mais simples é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="e37c9-125">hello simplest example is as follows:</span></span>

        json : '{
       "application_id": "MY_APP_ID",
       "src" : "http://cdn.blitline.com/filters/boys.jpeg",
       "functions" : [ {
           "name": "resize_to_fit",
           "params" : { "width": 240, "height": 140 },
           "save" : { "image_identifier" : "external_sample_1" }
       } ]
    }'

<span data-ttu-id="e37c9-126">Aqui temos JSON que levará a uma imagem de "src" "... boys.jpeg" e, em seguida, redimensione too240x140 essa imagem.</span><span class="sxs-lookup"><span data-stu-id="e37c9-126">Here we have JSON that will take a "src" image "...boys.jpeg" and then resize that image too240x140.</span></span>

<span data-ttu-id="e37c9-127">Olá ID do aplicativo é algo que você pode encontrar no seu **informações de conexão** ou **gerenciar** guia no Azure.</span><span class="sxs-lookup"><span data-stu-id="e37c9-127">hello Application ID is something you can find in your **CONNECTION INFO** or **MANAGE** tab on Azure.</span></span> <span data-ttu-id="e37c9-128">É o identificador secreto que permite que você toorun trabalhos em Blitline.</span><span class="sxs-lookup"><span data-stu-id="e37c9-128">It is your secret identifier that allows you toorun jobs on Blitline.</span></span>

<span data-ttu-id="e37c9-129">Olá "Salvar" parâmetro identifica as informações sobre onde você deseja a imagem de saudação do tooput depois de ter o processamos.</span><span class="sxs-lookup"><span data-stu-id="e37c9-129">hello "save" parameter identifies information about where you want tooput hello image once we have processed it.</span></span> <span data-ttu-id="e37c9-130">Neste caso trivial, não definimos um local.</span><span class="sxs-lookup"><span data-stu-id="e37c9-130">In this trivial case, we haven't defined one.</span></span> <span data-ttu-id="e37c9-131">Se nenhum local for definido, o Blitline irá armazená-la localmente (e temporariamente) em um local exclusivo na nuvem.</span><span class="sxs-lookup"><span data-stu-id="e37c9-131">If no location is defined Blitline will store it locally (and temporarily) at a unique cloud location.</span></span> <span data-ttu-id="e37c9-132">Você será capaz de tooget que local a partir do hello JSON retornado por Blitline quando você fizer Olá Blitline.</span><span class="sxs-lookup"><span data-stu-id="e37c9-132">You will be able tooget that location from hello JSON returned by Blitline when you make hello Blitline.</span></span> <span data-ttu-id="e37c9-133">Identificador da "imagem" Hello é necessária e será retornado tooyou quando tooidentify específico salva imagem.</span><span class="sxs-lookup"><span data-stu-id="e37c9-133">hello "image" identifier is required and is returned tooyou when tooidentify this particular saved image.</span></span>

<span data-ttu-id="e37c9-134">Você pode encontrar mais informações sobre Olá *funções* suportamos aqui: <http://www.blitline.com/docs/functions></span><span class="sxs-lookup"><span data-stu-id="e37c9-134">You can find more information about hello *functions* we support here: <http://www.blitline.com/docs/functions></span></span>

<span data-ttu-id="e37c9-135">Você também pode encontrar documentação sobre Olá opções de trabalho aqui: <http://www.blitline.com/docs/api></span><span class="sxs-lookup"><span data-stu-id="e37c9-135">You can also find documentation about hello job options here: <http://www.blitline.com/docs/api></span></span>

<span data-ttu-id="e37c9-136">Uma vez que o JSON tudo o que você precisa toodo é **POST** ele muito`http://api.blitline.com/job`</span><span class="sxs-lookup"><span data-stu-id="e37c9-136">Once you have your JSON all you need toodo is **POST** it too`http://api.blitline.com/job`</span></span>

<span data-ttu-id="e37c9-137">O JSON de volta será semelhante a isto:</span><span class="sxs-lookup"><span data-stu-id="e37c9-137">You will get JSON back that looks something like this:</span></span>

    {
     "results":
         {"images":
            [{
              "image_identifier":"external_sample_1",
              "s3_url":"https://s3.amazonaws.com/dev.blitline/2011110722/YOUR_APP_ID/CK3f0xBF_2bV6wf7gEZE8w.jpg"
            }],
          "job_id":"4eb8c9f72a50ee2a9900002f"
         }
    }


<span data-ttu-id="e37c9-138">Isso indica que Blitline recebeu a solicitação, ele tem colocá-la em uma fila de processamento e quando ele for concluído imagem Olá estarão disponível em: **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_aplicativo\_ID /CK3f0xBF_2bV6wf7gEZE8w.jpg**</span><span class="sxs-lookup"><span data-stu-id="e37c9-138">This tells you that Blitline has recieved your request, it has put it in a processing queue, and when it has completed hello image will be available at: **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_APP\_ID/CK3f0xBF_2bV6wf7gEZE8w.jpg**</span></span>

## <a name="how-toosave-an-image-tooyour-azure-storage-account"></a><span data-ttu-id="e37c9-139">Como toosave tooyour uma imagem conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="e37c9-139">How toosave an image tooyour Azure Storage account</span></span>
<span data-ttu-id="e37c9-140">Se você tiver uma conta de armazenamento do Azure, você pode apresentar imagens de saudação processada por push Blitline em seu contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="e37c9-140">If you have an Azure Storage account, you can easily have Blitline push hello processed images into your Azure container.</span></span> <span data-ttu-id="e37c9-141">Adicionando um "azure_destination" você definir local hello e permissões para toopush Blitline para.</span><span class="sxs-lookup"><span data-stu-id="e37c9-141">By adding an "azure_destination" you define hello location and permissions for Blitline toopush to.</span></span>

<span data-ttu-id="e37c9-142">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="e37c9-142">Here is an example:</span></span>

    job : '{
      "application_id": "YOUR_APP_ID",
      "src" : "http://www.google.com/logos/2011/houdini11-hp.jpg",
         "functions" : [{
         "name": "blur",
         "save" : {
             "image_identifier" : "YOUR_IMAGE_IDENTIFIER",
             "azure_destination" : {
                 "account_name" : "YOUR_AZURE_CONTAINER_NAME",
                 "shared_access_signature" : "SAS_THAT_GIVES_BLITLINE_PERMISSION_TO_WRITE_THIS_OBJECT_TO_CONTAINER",
               }
           }
         }]
       }'


<span data-ttu-id="e37c9-143">Preenchendo Olá CAPITALIZED valores pelos seus próprios, você pode enviar este toohttp://api.blitline.com/job JSON e hello "src" imagem será processada com um filtro de desfoque e, em seguida, enviada por push tooyou destino do Azure.</span><span class="sxs-lookup"><span data-stu-id="e37c9-143">By filling in hello CAPITALIZED values with your own, you can submit this JSON toohttp://api.blitline.com/job and hello "src" image will be processed with a blur filter and then pushed tooyou Azure destination.</span></span>

### <a name="please-note"></a><span data-ttu-id="e37c9-144">Observação:</span><span class="sxs-lookup"><span data-stu-id="e37c9-144">Please note:</span></span>
<span data-ttu-id="e37c9-145">Olá SAS deve conter Olá url SAS inteira, incluindo nome do arquivo do arquivo de destino Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="e37c9-145">hello SAS must contain hello entire SAS url, including hello filename of hello destination file.</span></span>

<span data-ttu-id="e37c9-146">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e37c9-146">Example:</span></span>

    http://blitline.blob.core.windows.net/sample/image.jpg?sr=b&sv=2012-02-12&st=2013-04-12T03%3A18%3A30Z&se=2013-04-12T04%3A18%3A30Z&sp=w&sig=Bte2hkkbwTT2sqlkkKLop2asByrE0sIfeesOwj7jNA5o%3D


<span data-ttu-id="e37c9-147">Você também pode ler a última edição Olá de documentos do armazenamento do Azure do Blitline [aqui](http://www.blitline.com/docs/azure_storage).</span><span class="sxs-lookup"><span data-stu-id="e37c9-147">You can also read hello latest edition of Blitline's Azure Storage docs [here](http://www.blitline.com/docs/azure_storage).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e37c9-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e37c9-148">Next Steps</span></span>
<span data-ttu-id="e37c9-149">Visite tooread blitline.com sobre todos os nossos recursos:</span><span class="sxs-lookup"><span data-stu-id="e37c9-149">Visit blitline.com tooread about all our other features:</span></span>

* <span data-ttu-id="e37c9-150">Documentos de ponto de extremidade de API do Blitline <http://www.blitline.com/docs/api></span><span class="sxs-lookup"><span data-stu-id="e37c9-150">Blitline API Endpoint Docs <http://www.blitline.com/docs/api></span></span>
* <span data-ttu-id="e37c9-151">Funções da API do Blitline <http://www.blitline.com/docs/functions></span><span class="sxs-lookup"><span data-stu-id="e37c9-151">Blitline API Functions <http://www.blitline.com/docs/functions></span></span>
* <span data-ttu-id="e37c9-152">Exemplos de API do Blitline <http://www.blitline.com/docs/examples></span><span class="sxs-lookup"><span data-stu-id="e37c9-152">Blitline API Examples <http://www.blitline.com/docs/examples></span></span>
* <span data-ttu-id="e37c9-153">Biblioteca de Nuget de terceiros <http://nuget.org/packages/Blitline.Net></span><span class="sxs-lookup"><span data-stu-id="e37c9-153">Third Part Nuget Library <http://nuget.org/packages/Blitline.Net></span></span>

