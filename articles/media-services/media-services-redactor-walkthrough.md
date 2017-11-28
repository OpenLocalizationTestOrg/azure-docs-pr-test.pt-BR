---
title: "Passo a passo de edição facial com o Azure Media Analytics | Microsoft Docs"
description: "Este tópico mostra instruções passo a passo sobre como executar um fluxo de trabalho de edição completo usando o AMSE (Explorador dos Serviços de Mídia do Azure) e o Azure Media Redactor Visualizer (ferramenta de código-fonte aberto)."
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
ms.openlocfilehash: c0c622237f8cdca65fb6933f14cc21e9eb9ac036
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="redact-faces-with-azure-media-analytics-walkthrough"></a><span data-ttu-id="7b3d8-103">Passo a passo de edição facial com o Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="7b3d8-103">Redact faces with Azure Media Analytics walkthrough</span></span>

## <a name="overview"></a><span data-ttu-id="7b3d8-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="7b3d8-104">Overview</span></span>

<span data-ttu-id="7b3d8-105">**Azure Media Redactor** é um MP (processador de mídia) do [Azure Media Analytics](media-services-analytics-overview.md) que oferece edição facial escalonável na nuvem.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-105">**Azure Media Redactor** is an [Azure Media Analytics](media-services-analytics-overview.md) media processor (MP) that offers scalable face redaction in the cloud.</span></span> <span data-ttu-id="7b3d8-106">A edição facial permite que você modifique seu vídeo para desfocar rostos de pessoas selecionadas.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-106">Face redaction enables you to modify your video in order to blur faces of selected individuals.</span></span> <span data-ttu-id="7b3d8-107">Você pode querer usar o serviço de edição facial em cenários de segurança pública e de notícias veiculadas.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-107">You may want to use the face redaction service in public safety and news media scenarios.</span></span> <span data-ttu-id="7b3d8-108">Alguns minutos de vídeo com vários rostos podem levar horas para serem editados manualmente, mas, com esse serviço, o processo de edição facial exigirá apenas algumas etapas simples.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-108">A few minutes of footage that contains multiple faces can take hours to redact manually, but with this service the face redaction process will require just a few simple steps.</span></span> <span data-ttu-id="7b3d8-109">Para saber mais, confira [este](https://azure.microsoft.com/blog/azure-media-redactor/)blog.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-109">For  more information, see [this](https://azure.microsoft.com/blog/azure-media-redactor/) blog.</span></span>

<span data-ttu-id="7b3d8-110">Para obter detalhes sobre o **Azure Media Redactor**, veja o tópico [Visão geral da edição de face](media-services-face-redaction.md).</span><span class="sxs-lookup"><span data-stu-id="7b3d8-110">For details about  **Azure Media Redactor**, see the [Face redaction overview](media-services-face-redaction.md) topic.</span></span>

<span data-ttu-id="7b3d8-111">Este tópico mostra instruções passo a passo sobre como executar um fluxo de trabalho de edição completo usando o AMSE (Explorador dos Serviços de Mídia do Azure) e o Azure Media Redactor Visualizer (ferramenta de código-fonte aberto).</span><span class="sxs-lookup"><span data-stu-id="7b3d8-111">This topic shows step by step instructions on how to run a full redaction workflow using Azure Media Services Explorer (AMSE) and Azure Media Redactor Visualizer (open source tool).</span></span>

<span data-ttu-id="7b3d8-112">No momento, o MP do **Azure Media Redactor** está em versão de Visualização.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-112">The **Azure Media Redactor** MP is currently in Preview.</span></span> <span data-ttu-id="7b3d8-113">Ele está disponível em todas as regiões públicas do Azure, bem como em data centers do Governo dos EUA e da China.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-113">It is available in all public Azure regions as well as US Government and China data centers.</span></span> <span data-ttu-id="7b3d8-114">Esta visualização está disponível gratuitamente no momento.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-114">This preview is currently free of charge.</span></span> <span data-ttu-id="7b3d8-115">Na versão atual, há um limite de 10 minutos de duração do vídeo processado.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-115">In the current release, there is a 10 minute limit on processed video length.</span></span>

<span data-ttu-id="7b3d8-116">Para saber mais, confira [este](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) blog.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-116">For more information, see [this](https://azure.microsoft.com/en-us/blog/redaction-preview-available-globally) blog.</span></span>

## <a name="azure-media-services-explorer-workflow"></a><span data-ttu-id="7b3d8-117">Fluxo de trabalho do Explorador dos Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="7b3d8-117">Azure Media Services Explorer workflow</span></span>

<span data-ttu-id="7b3d8-118">A maneira mais fácil de começar a usar o Redactor é com a ferramenta de código-fonte aberto AMSE no github.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-118">The easiest way to get started with Redactor is to use the open source AMSE tool on github.</span></span> <span data-ttu-id="7b3d8-119">Você pode executar um fluxo de trabalho simplificado no modo **combinado** se não precisar de acesso ao json de anotação ou às imagens jpg da face.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-119">You can run a simplified workflow via **combined** mode if you don’t need access to the annotation json or the face jpg images.</span></span>

### <a name="download-and-setup"></a><span data-ttu-id="7b3d8-120">Download e configuração</span><span class="sxs-lookup"><span data-stu-id="7b3d8-120">Download and setup</span></span>

1. <span data-ttu-id="7b3d8-121">Baixe a ferramenta AMSE [aqui](https://github.com/Azure/Azure-Media-Services-Explorer).</span><span class="sxs-lookup"><span data-stu-id="7b3d8-121">Download the AMSE tool from [here](https://github.com/Azure/Azure-Media-Services-Explorer).</span></span>
1. <span data-ttu-id="7b3d8-122">Faça logon em sua conta dos Serviços de Mídia usando sua chave de serviço.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-122">Log in to your Media Services account using your service key.</span></span>

    <span data-ttu-id="7b3d8-123">Para obter as informações de chave e nome da conta, vá para o [Portal do Azure](https://portal.azure.com/) e selecione sua conta do AMS.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-123">To obtain the account name and key information, go to the [Azure portal](https://portal.azure.com/) and select your AMS account.</span></span> <span data-ttu-id="7b3d8-124">Em seguida, selecione Configurações > Chaves.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-124">Then, select Settings > Keys.</span></span> <span data-ttu-id="7b3d8-125">A janela Gerenciar chaves mostra o nome da conta e as chaves primária e secundária são exibidas.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-125">The Manage keys windows shows the account name and the primary and secondary keys is displayed.</span></span> <span data-ttu-id="7b3d8-126">Copie os valores do nome da conta e a chave primária.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-126">Copy values of the account name and the primary key.</span></span>

![Redação de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough001.png)

### <a name="first-pass--analyze-mode"></a><span data-ttu-id="7b3d8-128">Primeira aprovação – modo de análise</span><span class="sxs-lookup"><span data-stu-id="7b3d8-128">First pass – analyze mode</span></span>

1. <span data-ttu-id="7b3d8-129">Carregue seu arquivo de mídia em Ativo –> Carregar, ou arrastando e soltando.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-129">Upload your media file through Asset –> Upload, or via drag and drop.</span></span> 
1. <span data-ttu-id="7b3d8-130">Clique com botão direito e processe o arquivo de mídia usando a Análise de Mídia –> Azure Media Redactor –> Modo de Análise.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-130">Right click and process your media file using Media Analytics –> Azure Media Redactor –> Analyze mode.</span></span> 


![Redação de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough002.png)

![Redação de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough003.png)

<span data-ttu-id="7b3d8-133">A saída incluirá um arquivo json de anotações com dados de localização de face, bem como um jpg de cada face detectada.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-133">The output will include an annotations json file with face location data, as well as a jpg of each detected face.</span></span> 

![Redação de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough004.png)

###<a name="second-pass--redact-mode"></a><span data-ttu-id="7b3d8-135">Segunda aprovação – modo de edição</span><span class="sxs-lookup"><span data-stu-id="7b3d8-135">Second pass – redact mode</span></span>

1. <span data-ttu-id="7b3d8-136">Carregue seu ativo de vídeo original na saída da primeira aprovação e o defina como um ativo primário.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-136">Upload your original video asset to the output from the first pass and set as a primary asset.</span></span> 

    ![Redação de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough005.png)

2. <span data-ttu-id="7b3d8-138">(Opcional) Carregue um arquivo “Dance_idlist.txt”, que inclui uma lista delimitada por nova linha das IDs que você deseja editar.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-138">(Optional) Upload a 'Dance_idlist.txt' file which includes a newline delimited list of the IDs you wish to redact.</span></span> 

    ![Redação de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough006.png)

3. <span data-ttu-id="7b3d8-140">(Opcional) Faça as edições no arquivo annotations.json, por exemplo, aumentar os limites da caixa delimitadora.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-140">(Optional) Make any edits to the annotations.json file such as increasing the bounding box boundaries.</span></span> 
4. <span data-ttu-id="7b3d8-141">Clique com botão direito no ativo de saída da primeira aprovação, selecione o Redactor e execute com o modo **Editar**.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-141">Right click the output asset from the first pass, select the Redactor, and run with the **Redact** mode.</span></span> 

    ![Redação de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough007.png)

5. <span data-ttu-id="7b3d8-143">Baixe ou compartilhe o ativo de saída editado final.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-143">Download or share the final redacted output asset.</span></span> 

    ![Redação de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough008.png)

##<a name="azure-media-redactor-visualizer-open-source-tool"></a><span data-ttu-id="7b3d8-145">Ferramenta de código-fonte aberto Azure Media Redactor Visualizador</span><span class="sxs-lookup"><span data-stu-id="7b3d8-145">Azure Media Redactor Visualizer open source tool</span></span>

<span data-ttu-id="7b3d8-146">Uma [ferramenta visualizadora](https://github.com/Microsoft/azure-media-redactor-visualizer) de código-fonte aberto que foi projetada para ajudar os desenvolvedores novatos no formato de anotações com análise e uso da saída.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-146">An open source [visualizer tool](https://github.com/Microsoft/azure-media-redactor-visualizer) is designed to help developers just starting with the annotations format with parsing and using the output.</span></span>

<span data-ttu-id="7b3d8-147">Após a clonagem do repositório, para executar o projeto, você precisará baixar o FFMPEG no [site oficial](https://ffmpeg.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="7b3d8-147">After you clone the repo, in order to run the project, you will need to download FFMPEG from their [official site](https://ffmpeg.org/download.html).</span></span>

<span data-ttu-id="7b3d8-148">Se você for um desenvolvedor que está tentando analisar os dados de anotação de JSON, examine Models.MetaData para obter exemplos de código.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-148">If you are a developer trying to parse the JSON annotation data, look inside Models.MetaData for sample code examples.</span></span>

### <a name="set-up-the-tool"></a><span data-ttu-id="7b3d8-149">Configurar a ferramenta</span><span class="sxs-lookup"><span data-stu-id="7b3d8-149">Set up the tool</span></span>

1.  <span data-ttu-id="7b3d8-150">Baixe e compile toda a solução.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-150">Download and build the entire solution.</span></span> 

    ![Redação de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough009.png)

2.  <span data-ttu-id="7b3d8-152">Baixe FFMPEG [aqui](https://ffmpeg.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="7b3d8-152">Download FFMPEG from [here](https://ffmpeg.org/download.html).</span></span> <span data-ttu-id="7b3d8-153">Este projeto foi desenvolvido originalmente com a versão be1d324 (2016-10-04) e com vinculação estática.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-153">This project was originally developed with version be1d324 (2016-10-04) with static linking.</span></span> 
3.  <span data-ttu-id="7b3d8-154">Copie ffmpeg.exe e ffprobe.exe na mesma pasta de saída que AzureMediaRedactor.exe.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-154">Copy ffmpeg.exe and ffprobe.exe to the same output folder as AzureMediaRedactor.exe.</span></span> 

    ![Redação de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough010.png)

4. <span data-ttu-id="7b3d8-156">Execute AzureMediaRedactor.exe.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-156">Run AzureMediaRedactor.exe.</span></span> 

### <a name="use-the-tool"></a><span data-ttu-id="7b3d8-157">Usar a ferramenta</span><span class="sxs-lookup"><span data-stu-id="7b3d8-157">Use the tool</span></span>

1. <span data-ttu-id="7b3d8-158">Processe o vídeo em sua conta dos Serviços de Mídia do Azure com o MP do Redactor no modo Análise.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-158">Process your video in your Azure Media Services account with the Redactor MP on Analyze mode.</span></span> 
2. <span data-ttu-id="7b3d8-159">Baixe o arquivo de vídeo original e a saída do trabalho Edição - Análise.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-159">Download both the original video file and the output of the Redaction - Analyze job.</span></span> 
3. <span data-ttu-id="7b3d8-160">Execute o aplicativo visualizador e escolha os arquivos acima.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-160">Run the visualizer application and choose the files above.</span></span> 

    ![Redação de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough011.png)

4. <span data-ttu-id="7b3d8-162">Visualize o arquivo.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-162">Preview your file.</span></span> <span data-ttu-id="7b3d8-163">Selecione quais faces você gostaria de desfocar na barra lateral à direita.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-163">Select which faces you'd like to blur via the sidebar on the right.</span></span> 
    
    ![Redação de face](./media/media-services-redactor-walkthrough/media-services-redactor-walkthrough012.png)

5.  <span data-ttu-id="7b3d8-165">O campo de texto inferior será atualizado com as IDs de face.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-165">The bottom text field will update with the face IDs.</span></span> <span data-ttu-id="7b3d8-166">Crie um arquivo chamado "idlist.txt" com essas IDs como uma lista delimitada por nova linha.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-166">Create a file called "idlist.txt" with these IDs as a newline delimited list.</span></span> 

    >[!NOTE]
    > <span data-ttu-id="7b3d8-167">O idlist.txt deve ser salvo em ANSI.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-167">The idlist.txt should be saved in ANSI.</span></span> <span data-ttu-id="7b3d8-168">É possível usar o bloco de notas para salvar em ANSI.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-168">You can use notepad to save in ANSI.</span></span>
    
6.  <span data-ttu-id="7b3d8-169">Carregue esse arquivo no ativo de saída da etapa 1.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-169">Upload this file to the output asset from step 1.</span></span> <span data-ttu-id="7b3d8-170">Carregue o vídeo original também nesse ativo e defina-o como ativo primário.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-170">Upload the original video to this asset as well and set as primary asset.</span></span> 
7.  <span data-ttu-id="7b3d8-171">Execute o trabalho de Edição nesse ativo com o modo de "Edição" para obter o último vídeo editado.</span><span class="sxs-lookup"><span data-stu-id="7b3d8-171">Run Redaction job on this asset with "Redact" mode to get the final redacted video.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="7b3d8-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7b3d8-172">Next steps</span></span> 

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="7b3d8-173">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="7b3d8-173">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-links"></a><span data-ttu-id="7b3d8-174">Links relacionados</span><span class="sxs-lookup"><span data-stu-id="7b3d8-174">Related links</span></span>
[<span data-ttu-id="7b3d8-175">Visão geral do Azure Media Services Analytics</span><span class="sxs-lookup"><span data-stu-id="7b3d8-175">Azure Media Services Analytics Overview</span></span>](media-services-analytics-overview.md)

[<span data-ttu-id="7b3d8-176">Demonstrações do Azure Media Analytics</span><span class="sxs-lookup"><span data-stu-id="7b3d8-176">Azure Media Analytics demos</span></span>](http://azuremedialabs.azurewebsites.net/demos/Analytics.html)

[<span data-ttu-id="7b3d8-177">Anunciando a redação da face da Análise de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="7b3d8-177">Announcing Face Redaction for Azure Media Analytics</span></span>](https://azure.microsoft.com/blog/azure-media-redactor/)
