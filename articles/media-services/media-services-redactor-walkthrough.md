---
title: "as faces aaaRedact com instruções passo a passo de análise de mídia do Azure | Microsoft Docs"
description: "Este tópico mostra instruções passo a passo sobre como toorun um fluxo de trabalho de redação completo usando o Azure Media Services Explorer (AMSE) e o Azure Media Redactor visualizador (ferramenta de software livre)."
services: media-services
documentationcenter: 
author: Lichard
manager: cfowler
editor: 
ms.assetid: d6fa21b8-d80a-41b7-80c1-ff1761bc68f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/03/2017
ms.author: rli; juliako;
ms.openlocfilehash: ab28f4052b73fdb74fcd5766235eab35402a0c9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="redact-faces-with-azure-media-analytics-walkthrough"></a><span data-ttu-id="6e31a-103">Passo a passo de edição facial com o Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="6e31a-103">Redact faces with Azure Media Analytics walkthrough</span></span>

## <a name="overview"></a><span data-ttu-id="6e31a-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="6e31a-104">Overview</span></span>

<span data-ttu-id="6e31a-105">**Redactor de mídia do Azure** é um [análise de mídia do Azure](media-services-analytics-overview.md) processador de mídia (MP) que oferece redação face escalonável na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="6e31a-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in hello cloud.</span></span> <span data-ttu-id="6e31a-106">Redação da face permite que você toomodify o vídeo em faces de tooblur de ordem de pessoas selecionadas.</span><span class="sxs-lookup"><span data-stu-id="6e31a-106">Face redaction enables you toomodify your video in order tooblur faces of selected individuals.</span></span> <span data-ttu-id="6e31a-107">Talvez você queira serviço de redação de face toouse Olá em cenários de segurança e mídia públicos.</span><span class="sxs-lookup"><span data-stu-id="6e31a-107">You may want toouse hello face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="6e31a-108">Alguns minutos do que contém várias faces podem levar horas tooredact manualmente, mas com esta face de saudação do serviço redação processo requer apenas algumas etapas simples.</span><span class="sxs-lookup"><span data-stu-id="6e31a-108">A few minutes of footage that contains multiple faces can take hours tooredact manually, but with this service hello face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="6e31a-109">Para saber mais, confira [este](https://azure.microsoft.com/blog/azure-media-redactor/)blog.</span><span class="sxs-lookup"><span data-stu-id="6e31a-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="6e31a-110">Para obter detalhes sobre **Redactor de mídia do Azure**, consulte Olá [visão geral de redação de Face](media-services-face-redaction.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="6e31a-110">For details about  **Azure Media Redactor**, see hello [Face redaction overview](media-services-face-redaction.md) topic.</span></span>

<span data-ttu-id="6e31a-111">Este tópico mostra instruções passo a passo sobre como toorun um fluxo de trabalho de redação completo usando o Azure Media Services Explorer (AMSE) e o Azure Media Redactor visualizador (ferramenta de software livre).</span><span class="sxs-lookup"><span data-stu-id="6e31a-111">This topic shows step by step instructions on how toorun a full redaction workflow using Azure Media Services Explorer (AMSE) and Azure Media Redactor Visualizer (open source tool).</span></span>

<span data-ttu-id="6e31a-112">Olá **Redactor de mídia do Azure** MP está atualmente em visualização.</span><span class="sxs-lookup"><span data-stu-id="6e31a-112">hello **Azure Media Redactor** MP is currently in Preview.</span></span> <span data-ttu-id="6e31a-113">Ele está disponível em todas as regiões públicas do Azure, bem como em data centers do Governo dos EUA e da China.</span><span class="sxs-lookup"><span data-stu-id="6e31a-113">It is available in all public Azure regions as well as US Government and China data centers.</span></span> <span data-ttu-id="6e31a-114">Esta visualização está disponível gratuitamente no momento.</span><span class="sxs-lookup"><span data-stu-id="6e31a-114">This preview is currently free of charge.</span></span> <span data-ttu-id="6e31a-115">Na versão atual do hello, há um limite de 10 minutos no comprimento de vídeo processado.</span><span class="sxs-lookup"><span data-stu-id="6e31a-115">In hello current release, there is a 10 minute limit on processed video length.</span></span>

<span data-ttu-id="6e31a-116">Para saber mais, confira [este](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) blog.</span><span class="sxs-lookup"><span data-stu-id="6e31a-116">For more information, see [this](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) blog.</span></span>

## <a name="azure-media-services-explorer-workflow"></a><span data-ttu-id="6e31a-117">Fluxo de trabalho do Explorador dos Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="6e31a-117">Azure Media Services Explorer workflow</span></span>

<span data-ttu-id="6e31a-118">Olá tooget de maneira mais fácil de Introdução ao Redactor é a ferramenta AMSE de código aberto toouse Olá no github.</span><span class="sxs-lookup"><span data-stu-id="6e31a-118">hello easiest way tooget started with Redactor is toouse hello open source AMSE tool on github.</span></span> <span data-ttu-id="6e31a-119">Você pode executar um fluxo de trabalho simplificado por meio de **combinados** modo, se você não precisa acessar toohello anotação json ou hello face imagens jpg.</span><span class="sxs-lookup"><span data-stu-id="6e31a-119">You can run a simplified workflow via **combined** mode if you don’t need access toohello annotation json or hello face jpg images.</span></span>

### <a name="download-and-setup"></a><span data-ttu-id="6e31a-120">Download e configuração</span><span class="sxs-lookup"><span data-stu-id="6e31a-120">Download and setup</span></span>

1. <span data-ttu-id="6e31a-121">Baixar a ferramenta de AMSE de saudação do [aqui](https://github.com/Azure/Azure-Media-Services-Explorer).</span><span class="sxs-lookup"><span data-stu-id="6e31a-121">Download hello AMSE tool from [here](https://github.com/Azure/Azure-Media-Services-Explorer).</span></span>
1. <span data-ttu-id="6e31a-122">Faça logon na conta de serviços de mídia usando sua chave de serviço de tooyour.</span><span class="sxs-lookup"><span data-stu-id="6e31a-122">Log in tooyour Media Services account using your service key.</span></span>

    <span data-ttu-id="6e31a-123">tooobtain Olá nome da conta e informações de chave, vá toohello [portal do Azure](https://portal.azure.com/) e selecione sua conta AMS.</span><span class="sxs-lookup"><span data-stu-id="6e31a-123">tooobtain hello account name and key information, go toohello [Azure portal](https://portal.azure.com/) and select your AMS account.</span></span> <span data-ttu-id="6e31a-124">Em seguida, selecione Configurações > Chaves.</span><span class="sxs-lookup"><span data-stu-id="6e31a-124">Then, select Settings > Keys.</span></span> <span data-ttu-id="6e31a-125">windows do Hello gerenciar chaves mostra o nome da conta hello e as chaves primárias e secundárias Olá é exibida.</span><span class="sxs-lookup"><span data-stu-id="6e31a-125">hello Manage keys windows shows hello account name and hello primary and secondary keys is displayed.</span></span> <span data-ttu-id="6e31a-126">Copie os valores do nome da conta hello e Olá primary key.</span><span class="sxs-lookup"><span data-stu-id="6e31a-126">Copy values of hello account name and hello primary key.</span></span>

![Redação de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough001.png)

### <a name="first-pass--analyze-mode"></a><span data-ttu-id="6e31a-128">Primeira aprovação – modo de análise</span><span class="sxs-lookup"><span data-stu-id="6e31a-128">First pass – analyze mode</span></span>

1. <span data-ttu-id="6e31a-129">Carregue seu arquivo de mídia em Ativo –> Carregar, ou arrastando e soltando.</span><span class="sxs-lookup"><span data-stu-id="6e31a-129">Upload your media file through Asset –> Upload, or via drag and drop.</span></span> 
1. <span data-ttu-id="6e31a-130">Clique com botão direito e processe o arquivo de mídia usando a Análise de Mídia –> Azure Media Redactor –> Modo de Análise.</span><span class="sxs-lookup"><span data-stu-id="6e31a-130">Right click and process your media file using Media Analytics –> Azure Media Redactor –> Analyze mode.</span></span> 


![Redação de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough002.png)

![Redação de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough003.png)

<span data-ttu-id="6e31a-133">saída de Hello incluirá um arquivo json de anotações com dados de local de face, bem como jpg cada face detectado.</span><span class="sxs-lookup"><span data-stu-id="6e31a-133">hello output will include an annotations json file with face location data, as well as a jpg of each detected face.</span></span> 

![Redação de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough004.png)

###<a name="second-pass--redact-mode"></a><span data-ttu-id="6e31a-135">Segunda aprovação – modo de edição</span><span class="sxs-lookup"><span data-stu-id="6e31a-135">Second pass – redact mode</span></span>

1. <span data-ttu-id="6e31a-136">Carregue seu toohello ativo de vídeo original de saída da primeira passagem de saudação e definido como um ativo primário.</span><span class="sxs-lookup"><span data-stu-id="6e31a-136">Upload your original video asset toohello output from hello first pass and set as a primary asset.</span></span> 

    ![Redação de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough005.png)

2. <span data-ttu-id="6e31a-138">(Opcional) Carregar um arquivo de 'Dance_idlist.txt', que inclui uma lista delimitada de nova linha de saudação IDs que você deseja tooredact.</span><span class="sxs-lookup"><span data-stu-id="6e31a-138">(Optional) Upload a 'Dance_idlist.txt' file which includes a newline delimited list of hello IDs you wish tooredact.</span></span> 

    ![Redação de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough006.png)

3. <span data-ttu-id="6e31a-140">(Opcional) Fazer com que qualquer arquivo de annotations.json toohello edições como aumentar Olá limites da caixa delimitadora.</span><span class="sxs-lookup"><span data-stu-id="6e31a-140">(Optional) Make any edits toohello annotations.json file such as increasing hello bounding box boundaries.</span></span> 
4. <span data-ttu-id="6e31a-141">Olá ativo de saída da primeira passagem de saudação clique com botão direito, selecione Olá Redactor e executar com hello **Redact** modo.</span><span class="sxs-lookup"><span data-stu-id="6e31a-141">Right click hello output asset from hello first pass, select hello Redactor, and run with hello **Redact** mode.</span></span> 

    ![Redação de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough007.png)

5. <span data-ttu-id="6e31a-143">Baixar ou compartilhar Olá ativo de saída redigida final.</span><span class="sxs-lookup"><span data-stu-id="6e31a-143">Download or share hello final redacted output asset.</span></span> 

    ![Redação de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough008.png)

##<a name="azure-media-redactor-visualizer-open-source-tool"></a><span data-ttu-id="6e31a-145">Ferramenta de código-fonte aberto Azure Media Redactor Visualizador</span><span class="sxs-lookup"><span data-stu-id="6e31a-145">Azure Media Redactor Visualizer open source tool</span></span>

<span data-ttu-id="6e31a-146">Um código-fonte aberto [ferramenta Visualizador](https://github.com/Microsoft/azure-media-redactor-visualizer) é projetado toohelp desenvolvedores começando com o formato de anotações de saudação com análise e usando a saída de hello.</span><span class="sxs-lookup"><span data-stu-id="6e31a-146">An open source [visualizer tool](https://github.com/Microsoft/azure-media-redactor-visualizer) is designed toohelp developers just starting with hello annotations format with parsing and using hello output.</span></span>

<span data-ttu-id="6e31a-147">Após clonar o repositório de hello, no projeto de saudação do toorun ordem, você precisará toodownload FFMPEG de seus [site oficial do](https://ffmpeg.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="6e31a-147">After you clone hello repo, in order toorun hello project, you will need toodownload FFMPEG from their [official site](https://ffmpeg.org/download.html).</span></span>

<span data-ttu-id="6e31a-148">Se você for um desenvolvedor tentar tooparse Olá dados de anotação de JSON, examinar Models.MetaData para obter exemplos de código de exemplo.</span><span class="sxs-lookup"><span data-stu-id="6e31a-148">If you are a developer trying tooparse hello JSON annotation data, look inside Models.MetaData for sample code examples.</span></span>

### <a name="set-up-hello-tool"></a><span data-ttu-id="6e31a-149">Configurar a ferramenta de saudação</span><span class="sxs-lookup"><span data-stu-id="6e31a-149">Set up hello tool</span></span>

1.  <span data-ttu-id="6e31a-150">Baixar e compile a solução inteira hello.</span><span class="sxs-lookup"><span data-stu-id="6e31a-150">Download and build hello entire solution.</span></span> 

    ![Redação de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough009.png)

2.  <span data-ttu-id="6e31a-152">Baixe FFMPEG [aqui](https://ffmpeg.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="6e31a-152">Download FFMPEG from [here](https://ffmpeg.org/download.html).</span></span> <span data-ttu-id="6e31a-153">Este projeto foi desenvolvido originalmente com a versão be1d324 (2016-10-04) e com vinculação estática.</span><span class="sxs-lookup"><span data-stu-id="6e31a-153">This project was originally developed with version be1d324 (2016-10-04) with static linking.</span></span> 
3.  <span data-ttu-id="6e31a-154">Copiar toohello ffmpeg.exe e ffprobe.exe mesma pasta de saída como AzureMediaRedactor.exe.</span><span class="sxs-lookup"><span data-stu-id="6e31a-154">Copy ffmpeg.exe and ffprobe.exe toohello same output folder as AzureMediaRedactor.exe.</span></span> 

    ![Redação de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough010.png)

4. <span data-ttu-id="6e31a-156">Execute AzureMediaRedactor.exe.</span><span class="sxs-lookup"><span data-stu-id="6e31a-156">Run AzureMediaRedactor.exe.</span></span> 

### <a name="use-hello-tool"></a><span data-ttu-id="6e31a-157">Use a ferramenta Olá</span><span class="sxs-lookup"><span data-stu-id="6e31a-157">Use hello tool</span></span>

1. <span data-ttu-id="6e31a-158">Processe o vídeo em sua conta de serviços de mídia do Azure com hello Redactor MP no modo de analisar.</span><span class="sxs-lookup"><span data-stu-id="6e31a-158">Process your video in your Azure Media Services account with hello Redactor MP on Analyze mode.</span></span> 
2. <span data-ttu-id="6e31a-159">Baixar o arquivo de vídeo original hello e saída Olá Olá redação - analisar o trabalho.</span><span class="sxs-lookup"><span data-stu-id="6e31a-159">Download both hello original video file and hello output of hello Redaction - Analyze job.</span></span> 
3. <span data-ttu-id="6e31a-160">Execute o aplicativo de visualizador hello e escolher Olá arquivos acima.</span><span class="sxs-lookup"><span data-stu-id="6e31a-160">Run hello visualizer application and choose hello files above.</span></span> 

    ![Redação de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough011.png)

4. <span data-ttu-id="6e31a-162">Visualize o arquivo.</span><span class="sxs-lookup"><span data-stu-id="6e31a-162">Preview your file.</span></span> <span data-ttu-id="6e31a-163">Selecione qual faces você gostaria que tooblur por meio de barra lateral Olá Olá direita.</span><span class="sxs-lookup"><span data-stu-id="6e31a-163">Select which faces you'd like tooblur via hello sidebar on hello right.</span></span> 
    
    ![Redação de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough012.png)

5.  <span data-ttu-id="6e31a-165">campo de texto Olá inferior será atualizado com face Olá IDs.</span><span class="sxs-lookup"><span data-stu-id="6e31a-165">hello bottom text field will update with hello face IDs.</span></span> <span data-ttu-id="6e31a-166">Crie um arquivo chamado "idlist.txt" com essas IDs como uma lista delimitada por nova linha.</span><span class="sxs-lookup"><span data-stu-id="6e31a-166">Create a file called "idlist.txt" with these IDs as a newline delimited list.</span></span> 

    >[!NOTE]
    > <span data-ttu-id="6e31a-167">Olá idlist.txt devem ser salvos em ANSI.</span><span class="sxs-lookup"><span data-stu-id="6e31a-167">hello idlist.txt should be saved in ANSI.</span></span> <span data-ttu-id="6e31a-168">Você pode usar o bloco de notas toosave ANSI.</span><span class="sxs-lookup"><span data-stu-id="6e31a-168">You can use notepad toosave in ANSI.</span></span>
    
6.  <span data-ttu-id="6e31a-169">Carregar este ativo de saída do arquivo toohello da etapa 1.</span><span class="sxs-lookup"><span data-stu-id="6e31a-169">Upload this file toohello output asset from step 1.</span></span> <span data-ttu-id="6e31a-170">Carregar Olá toothis vídeo ativo original também e definido como ativo primário.</span><span class="sxs-lookup"><span data-stu-id="6e31a-170">Upload hello original video toothis asset as well and set as primary asset.</span></span> 
7.  <span data-ttu-id="6e31a-171">Execute trabalho de redação deste ativo com "Redact" modo tooget Olá final redigido vídeo.</span><span class="sxs-lookup"><span data-stu-id="6e31a-171">Run Redaction job on this asset with "Redact" mode tooget hello final redacted video.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6e31a-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6e31a-172">Next steps</span></span> 

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6e31a-173">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="6e31a-173">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="6e31a-174">Links relacionados</span><span class="sxs-lookup"><span data-stu-id="6e31a-174">Related links</span></span>
[<span data-ttu-id="6e31a-175">Visão geral do Azure Media Services Analytics</span><span class="sxs-lookup"><span data-stu-id="6e31a-175">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="6e31a-176">Demonstrações do Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="6e31a-176">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

[<span data-ttu-id="6e31a-177">Anunciando a redação da face da Análise de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="6e31a-177">Announcing Face Redaction for Azure Media Analytics</span></span>](https://azure.microsoft.com/blog/azure-media-redactor/)
