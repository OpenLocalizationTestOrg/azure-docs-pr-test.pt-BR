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
# <a name="how-toouse-blitline-with-azure-and-azure-storage"></a>Como toouse Blitline com o Azure e armazenamento do Azure
Este guia explica como tooaccess Blitline como toosubmit trabalhos tooBlitline e serviços.

## <a name="what-is-blitline"></a>O que é Blitline?
Blitline é uma serviço que fornece processamento de imagem de nível empresarial em uma fração do preço de saudação que custaria toobuild de processamento de imagens baseado em nuvem-lo por conta própria.

fato Olá é que o processamento de imagem foi feito repetidamente, geralmente recriado do início de saudação para cada site. Sabemos disso porque os compilamos milhões de vezes também. Um dia, decidimos que talvez fosse o momento de simplesmente fazê-lo para todas as pessoas. Sabemos como toodo-la, toodo-rápida e eficientemente e salve todos funcionam no hello enquanto isso.

Para obter mais informações, consulte [http://www.blitline.com](http://www.blitline.com).

## <a name="what-blitline-is-not"></a>O que o Blitline NÃO é...
tooclarify que Blitline é útil para, ele é geralmente mais fácil tooidentify que Blitline não antes de continuar.

* Blitline não tem imagens de tooupload de widgets HTML. Você deve ter as imagens disponíveis publicamente ou com permissões restritas disponíveis para Blitline tooreach.
* O Blitline NÃO faz o processamento de imagens ao vivo, como o Aviary.com.
* Blitline não aceita carregamentos de imagem, não é possível enviar seu tooBlitline imagens diretamente. Você deve enviá-las tooAzure armazenamento ou outros locais que blitline oferece suporte e, em seguida, conte-Blitline onde toogo obtê-los.
* O Blitline é massivamente paralelo e NÃO faz nenhum processamento síncrono. Ou seja, você deve nos fornecer um postback_url para que possamos informar a conclusão do processamento.

## <a name="create-a-blitline-account"></a>Criar uma conta do Blitline
[!INCLUDE [blitline-signup](../includes/blitline-signup.md)]

## <a name="how-toocreate-a-blitline-job"></a>Como toocreate um trabalho Blitline
Blitline usa JSON toodefine Olá ações que você deseja tootake em uma imagem. Esse JSON é composto de alguns campos simples.

exemplo de Hello mais simples é o seguinte:

        json : '{
       "application_id": "MY_APP_ID",
       "src" : "http://cdn.blitline.com/filters/boys.jpeg",
       "functions" : [ {
           "name": "resize_to_fit",
           "params" : { "width": 240, "height": 140 },
           "save" : { "image_identifier" : "external_sample_1" }
       } ]
    }'

Aqui temos JSON que levará a uma imagem de "src" "... boys.jpeg" e, em seguida, redimensione too240x140 essa imagem.

Olá ID do aplicativo é algo que você pode encontrar no seu **informações de conexão** ou **gerenciar** guia no Azure. É o identificador secreto que permite que você toorun trabalhos em Blitline.

Olá "Salvar" parâmetro identifica as informações sobre onde você deseja a imagem de saudação do tooput depois de ter o processamos. Neste caso trivial, não definimos um local. Se nenhum local for definido, o Blitline irá armazená-la localmente (e temporariamente) em um local exclusivo na nuvem. Você será capaz de tooget que local a partir do hello JSON retornado por Blitline quando você fizer Olá Blitline. Identificador da "imagem" Hello é necessária e será retornado tooyou quando tooidentify específico salva imagem.

Você pode encontrar mais informações sobre Olá *funções* suportamos aqui: <http://www.blitline.com/docs/functions>

Você também pode encontrar documentação sobre Olá opções de trabalho aqui: <http://www.blitline.com/docs/api>

Uma vez que o JSON tudo o que você precisa toodo é **POST** ele muito`http://api.blitline.com/job`

O JSON de volta será semelhante a isto:

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


Isso indica que Blitline recebeu a solicitação, ele tem colocá-la em uma fila de processamento e quando ele for concluído imagem Olá estarão disponível em: **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_aplicativo\_ID /CK3f0xBF_2bV6wf7gEZE8w.jpg**

## <a name="how-toosave-an-image-tooyour-azure-storage-account"></a>Como toosave tooyour uma imagem conta de armazenamento do Azure
Se você tiver uma conta de armazenamento do Azure, você pode apresentar imagens de saudação processada por push Blitline em seu contêiner do Azure. Adicionando um "azure_destination" você definir local hello e permissões para toopush Blitline para.

Aqui está um exemplo:

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


Preenchendo Olá CAPITALIZED valores pelos seus próprios, você pode enviar este toohttp://api.blitline.com/job JSON e hello "src" imagem será processada com um filtro de desfoque e, em seguida, enviada por push tooyou destino do Azure.

### <a name="please-note"></a>Observação:
Olá SAS deve conter Olá url SAS inteira, incluindo nome do arquivo do arquivo de destino Olá Olá.

Exemplo:

    http://blitline.blob.core.windows.net/sample/image.jpg?sr=b&sv=2012-02-12&st=2013-04-12T03%3A18%3A30Z&se=2013-04-12T04%3A18%3A30Z&sp=w&sig=Bte2hkkbwTT2sqlkkKLop2asByrE0sIfeesOwj7jNA5o%3D


Você também pode ler a última edição Olá de documentos do armazenamento do Azure do Blitline [aqui](http://www.blitline.com/docs/azure_storage).

## <a name="next-steps"></a>Próximas etapas
Visite tooread blitline.com sobre todos os nossos recursos:

* Documentos de ponto de extremidade de API do Blitline <http://www.blitline.com/docs/api>
* Funções da API do Blitline <http://www.blitline.com/docs/functions>
* Exemplos de API do Blitline <http://www.blitline.com/docs/examples>
* Biblioteca de Nuget de terceiros <http://nuget.org/packages/Blitline.Net>

