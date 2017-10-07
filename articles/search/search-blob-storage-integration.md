---
title: aaaAdding tooBlob de pesquisa do Azure Storage | Microsoft Docs
description: "Crie um índice no código usando Olá API de REST de HTTP de pesquisa do Azure."
services: search
documentationcenter: 
author: ashmaka
manager: jhubbard
ms.service: search
ms.topic: article
ms.date: 05/04/2017
ms.author: ashmaka
ms.openlocfilehash: a3801790067bf169693b500e83799286b7387a77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="searching-blob-storage-with-azure-search"></a>Pesquisando no Armazenamento de Blobs com o Azure Search

Pesquisando em Olá diversos tipos de conteúdo armazenado no armazenamento de BLOBs do Azure pode ser um problema difícil toosolve. No entanto, você pode indexar e pesquisar Olá conteúdo de seus Blobs em apenas alguns cliques usando a pesquisa do Azure. Pesquisar no Armazenamento de Blobs requer o provisionamento de um serviço Azure Search. Olá vários limites de serviço e preços camadas da pesquisa do Azure podem ser encontradas no hello [página de preços](https://aka.ms/azspricing).

## <a name="what-is-azure-search"></a>O que é o Azure Search?
[A pesquisa do Azure](https://aka.ms/whatisazsearch) é uma solução de pesquisa que torna mais fácil para experiências de pesquisa de texto completo robusto desenvolvedores tooadd tooweb e aplicativos móveis. Como serviço, pesquisa do Azure remove Olá necessidade toomanage qualquer infraestrutura de pesquisa durante a oferta de uma [tempo de atividade de 99,9% SLA](https://aka.ms/azuresearchsla).

Com suporte avançado a 56 idiomas, o Azure Search pode analisar seu conteúdo e lidar de modo inteligente com as construções específicas a um idioma. A pesquisa do Azure também fornece Olá ferramentas toobuild uma experiência de usuário avançada de pesquisa. É simples tooadd recursos como ocorrências de interfaces toouser realce usando a pesquisa do Azure, typeahead sugestões de pesquisa e navegação facetada. toolearn sobre os recursos da pesquisa do Azure, você pode ler do serviço Olá [documentação](https://aka.ms/azsearchdocs).

## <a name="crack-open-and-search-through-hello-content-of-enterprise-document-formats"></a>Quebrar e pesquise o conteúdo de saudação de formatos de documentos da empresa
Com suporte para [documento extração](https://aka.ms/azsblobindexer) no armazenamento de BLOBs do Azure, pesquisa do Azure pode indexar o conteúdo de saudação de uma variedade de tipos de arquivos armazenados em blobs:
- PDF
- Microsoft Office: DOCX/DOC, XLSX/XLS, PPT/PPTX, MSG (emails do Outlook)
- HTML
- Arquivos de texto sem formatação

Extraindo os metadados desses tipos de arquivo e texto, é fácil toosearch em vários formatos de arquivo com uma única consulta toofind hello mais relevantes os documentos independentemente do tipo. Através da indexação de metadados de conteúdo e Olá Olá de documentos do Microsoft Office, PDFs e emails, é possível toobuild uma solução de gerenciamento de conteúdo corporativo usando o armazenamento de Blob e pesquisa do Azure.

## <a name="search-through-your-blob-metadata"></a>Pesquisar os metadados de blob
Um cenário comum que torna mais fácil toosort por meio de blobs de qualquer tipo de conteúdo é tooindex Olá blob personalizado definido pelo usuário, metadados, bem como Olá propriedades do sistema para cada um dos seus blobs. Dessa forma, informações para cada blob são indexadas independentemente do tipo de saudação do documento no blob Olá para que você pode facilmente a classificação e a faceta em todo o conteúdo do armazenamento de Blob.

[Saiba que mais sobre a indexação de metadados de blob.](https://aka.ms/azsblobmetadataindexing)

## <a name="image-search"></a>Pesquisa de imagem
Pesquisa de texto completo da pesquisa do Azure, a navegação facetada e recursos de classificação agora podem ser aplicadas toohello metadados de imagens armazenadas em blobs.

Se essas imagens são pré-processados usando Olá [API de visão do computador](https://www.microsoft.com/cognitive-services/computer-vision-api) serviços da Microsoft cognitivas, em seguida, é possível tooindex Olá visual conteúdo, encontrado em cada imagem inclusive OCR, reconhecimento de manuscrito. Estamos trabalhando na adição de recursos de processamento de imagem OCR e outros diretamente tooAzure pesquisa, se você estiver interessado nesses recursos envie uma solicitação em nosso [UserVoice](https://aka.ms/azsuv) ou [e-mail](mailto:azscustquestions@microsoft.com).

## <a name="index-and-search-through-json-blobs"></a>Indexar e pesquisar em blobs do JSON
A pesquisa do Azure pode ser configurado tooextract estruturado conteúdo encontrado em blobs que contêm JSON. A pesquisa do Azure pode ler blobs JSON e analisa Olá estruturado em campos apropriados de saudação de um documento de pesquisa do Azure. A pesquisa do Azure também pode levar a blobs que contêm uma matriz de objetos JSON e mapeiam cada documento de pesquisa do Azure separado do elemento tooa.

Observe que a análise JSON não é configurável no momento por meio do portal hello. [Saiba mais sobre análise de JSON no Azure Search.](https://aka.ms/azsjsonblobindexing)

## <a name="quick-start"></a>Início rápido
A pesquisa do Azure pode ser adicionada tooblobs diretamente da folha do portal de armazenamento do Blob hello.

![](./media/search-blob-storage-integration/blob-blade.png)

Clicar na opção "Adicionar pesquisa do Azure" de saudação inicia um fluxo de onde você pode selecionar um serviço de pesquisa do Azure existente ou criar um novo serviço. Se você criar um novo serviço, você será direcionado para fora da experiência de portal da conta de armazenamento. Você precisará toore-navegue folha portal do armazenamento toohello e selecione novamente a opção de "Adicionar pesquisa do Azure" Olá, onde você pode selecionar um serviço existente hello.

### <a name="next-steps"></a>Próximas etapas
Saiba mais sobre Olá indexador de Blob de pesquisa do Azure no hello completo [documentação](https://aka.ms/azsblobindexer).
