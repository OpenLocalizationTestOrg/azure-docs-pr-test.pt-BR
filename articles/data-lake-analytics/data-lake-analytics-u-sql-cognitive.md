---
title: Usando recursos cognitivos do U-SQL no Azure Data Lake Analytics | Microsoft Docs
description: "Saiba como usar a inteligência de recursos Cognitivos no U-SQL"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: sukvg
editor: cgronlun
ms.assetid: 019c1d53-4e61-4cad-9b2c-7a60307cbe19
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: saveenr
ms.openlocfilehash: f77329f9838d6e824afa7234de90f62257a004de
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-get-started-with-the-cognitive-capabilities-of-u-sql"></a><span data-ttu-id="5e472-103">Tutorial: introdução aos recursos Cognitivos do U-SQL</span><span class="sxs-lookup"><span data-stu-id="5e472-103">Tutorial: Get started with the Cognitive capabilities of U-SQL</span></span>

<span data-ttu-id="5e472-104">Os recursos cognitivos para o U-SQL permitem aos desenvolvedores colocar inteligência em seus programas de Big Data.</span><span class="sxs-lookup"><span data-stu-id="5e472-104">Cognitive capabilities for U-SQL enable developers to use put intelligence in their big data programs.</span></span> <span data-ttu-id="5e472-105">O processo geral de maneira simples:</span><span class="sxs-lookup"><span data-stu-id="5e472-105">The overall process in simple:</span></span>

* <span data-ttu-id="5e472-106">Usar a instrução REFERENCE ASSEMBLY para habilitar os recursos cognitivos para o Script U-SQL</span><span class="sxs-lookup"><span data-stu-id="5e472-106">Use the REFERENCE ASSEMBLY statement to enable the cognitive features for the U-SQL Script</span></span>
* <span data-ttu-id="5e472-107">Chame a operação PROCESS para usar os recursos Cognitivos</span><span class="sxs-lookup"><span data-stu-id="5e472-107">Call the PROCESS operation to use the Cognitive capabilities</span></span> 

## <a name="imaging-scenarios"></a><span data-ttu-id="5e472-108">Imaginando cenários</span><span class="sxs-lookup"><span data-stu-id="5e472-108">Imaging scenarios</span></span>

### <a name="example-image-tagging"></a><span data-ttu-id="5e472-109">Exemplo: marcação de imagem</span><span class="sxs-lookup"><span data-stu-id="5e472-109">Example: Image tagging</span></span>

<span data-ttu-id="5e472-110">O exemplo a seguir mostra um uso de ponta a ponta dos recursos de geração de imagens para detectar objetos nas imagens.</span><span class="sxs-lookup"><span data-stu-id="5e472-110">The following example shows an end-to-end use of the imaging capabilities to detect objects in images.</span></span>

    REFERENCE ASSEMBLY ImageCommon;
    REFERENCE ASSEMBLY FaceSdk;
    REFERENCE ASSEMBLY ImageEmotion;
    REFERENCE ASSEMBLY ImageTagging;
    REFERENCE ASSEMBLY ImageOcr;

    @imgs =
        EXTRACT FileName string, ImgData byte[]
        FROM @"/images/{FileName:*}.jpg"
        USING new Cognition.Vision.ImageExtractor();

    // Extract the number of objects on each image and tag them 
    @objects =
        PROCESS @imgs 
        PRODUCE FileName,
                NumObjects int,
                Tags string
        READONLY FileName
        USING new Cognition.Vision.ImageTagger();


### <a name="extract-emotions-from-human-faces"></a><span data-ttu-id="5e472-111">Extrair emoções de faces humanas</span><span class="sxs-lookup"><span data-stu-id="5e472-111">Extract emotions from human faces</span></span> 

    @emotions =
        PROCESS @imgs
        PRODUCE FileName string,
                NumFaces int,
                Emotion string
        READONLY FileName
        USING new Cognition.Vision.EmotionAnalyzer();

### <a name="estimate-age-and-gender-for-human-faces"></a><span data-ttu-id="5e472-112">Estimar a idade e o sexo de faces humanas</span><span class="sxs-lookup"><span data-stu-id="5e472-112">Estimate age and gender for human faces</span></span>

    @faces = 
            PROCESS @imgs
            PRODUCE FileName,
                    NumFaces int,
                    FaceAge string,
                    FaceGender string
            READONLY FileName
            USING new Cognition.Vision.FaceDetector();

### <a name="detect-text-in-images-ocr"></a><span data-ttu-id="5e472-113">Detectar texto em imagens (OCR)</span><span class="sxs-lookup"><span data-stu-id="5e472-113">Detect text in Images (OCR)</span></span>

    @ocrs =
            PROCESS @imgs
            PRODUCE FileName,
                    Text string
            READONLY FileName
            USING new Cognition.Vision.OcrExtractor();

## <a name="text-scenarios"></a><span data-ttu-id="5e472-114">Cenários de texto</span><span class="sxs-lookup"><span data-stu-id="5e472-114">Text scenarios</span></span>

### <a name="input-data"></a><span data-ttu-id="5e472-115">Dados de entrada</span><span class="sxs-lookup"><span data-stu-id="5e472-115">Input data</span></span>

<span data-ttu-id="5e472-116">Suponha que temos uma entrada que consiste em "Guerra e Paz" de Leo Tolstóy.</span><span class="sxs-lookup"><span data-stu-id="5e472-116">Assume that we have an input that consists of “War and Peace” by Leo Tolstoy.</span></span>

    REFERENCE ASSEMBLY [TextCommon];
    REFERENCE ASSEMBLY [TextSentiment];
    REFERENCE ASSEMBLY [TextKeyPhrase];

    @WarAndPeace =
        EXTRACT No int,
                Year string,
                Book string,
                Chapter string,
                Text string
        FROM @"/usqlext/samples/cognition/war_and_peace.csv"
        USING Extractors.Csv();

### <a name="extract-key-phrases-for-each-paragraph"></a><span data-ttu-id="5e472-117">Extraia frases-chave de cada parágrafo</span><span class="sxs-lookup"><span data-stu-id="5e472-117">Extract key phrases for each paragraph</span></span>

    @keyphrase =
        PROCESS @WarAndPeace
        PRODUCE No,
                Year,
                Book,
                Chapter,
                Text,
                KeyPhrase string
        READONLY No,
                Year,
                Book,
                Chapter,
                Text
        USING new Cognition.Text.KeyPhraseExtractor();

    // Tokenize the key phrases.
    @kpsplits =
        SELECT No,
            Year,
            Book,
            Chapter,
            Text,
            T.KeyPhrase
        FROM @keyphrase
            CROSS APPLY
                new Cognition.Text.Splitter("KeyPhrase") AS T(KeyPhrase);
    
### <a name="perform-sentiment-analysis-on-each-paragraph"></a><span data-ttu-id="5e472-118">Executar análise de sentimento em cada parágrafo</span><span class="sxs-lookup"><span data-stu-id="5e472-118">Perform sentiment analysis on each paragraph</span></span>

    @sentiment =
        PROCESS @WarAndPeace
        PRODUCE No,
                Year,
                Book,
                Chapter,
                Text,
                Sentiment string,
                Conf double
        READONLY No,
                Year,
                Book,
                Chapter,
                Text
        USING new Cognition.Text.SentimentAnalyzer(true);

