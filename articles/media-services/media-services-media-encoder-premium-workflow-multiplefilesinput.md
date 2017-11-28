---
title: aaaMultiple entrada arquivos e propriedades do componente com o codificador Premium - Azure | Microsoft Docs
description: "Este tópico explica como a toouse setRuntimeProperties toouse entrada de vários arquivos e passar o processador de mídia de fluxo de trabalho Premium de codificador de mídia de toohello dados personalizados."
services: media-services
documentationcenter: 
author: xpouyat
manager: cfowler
editor: 
ms.assetid: 7fb35bdd-9891-4401-a65b-ef3cc8190e8a
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: xpouyat;anilmur;juliako
ms.openlocfilehash: e14d10fbf9669e0b88e5ba1c519f1ba5e0bafdd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-multiple-input-files-and-component-properties-with-premium-encoder"></a><span data-ttu-id="93774-103">Usando vários arquivos de entrada e propriedades do componente com o Codificador Premium</span><span class="sxs-lookup"><span data-stu-id="93774-103">Using multiple input files and component properties with Premium Encoder</span></span>
## <a name="overview"></a><span data-ttu-id="93774-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="93774-104">Overview</span></span>
<span data-ttu-id="93774-105">Há cenários nos quais propriedades do componente toocustomize, talvez seja necessário especificar o conteúdo XML de lista do clipe ou enviar vários arquivos de entrada quando você enviar uma tarefa com hello **o fluxo de trabalho do Media Encoder Premium** processador de mídia.</span><span class="sxs-lookup"><span data-stu-id="93774-105">There are scenarios in which you might need toocustomize component properties, specify Clip List XML content, or send multiple input files when you submit a task with hello **Media Encoder Premium Workflow** media processor.</span></span> <span data-ttu-id="93774-106">Alguns exemplos incluem:</span><span class="sxs-lookup"><span data-stu-id="93774-106">Some examples are:</span></span>

* <span data-ttu-id="93774-107">Sobreposição de texto em vídeo e definir o valor de texto de saudação (por exemplo, a saudação data atual) em tempo de execução para cada vídeo de entrada.</span><span class="sxs-lookup"><span data-stu-id="93774-107">Overlaying text on video and setting hello text value (for example, hello current date) at runtime for each input video.</span></span>
* <span data-ttu-id="93774-108">Personalizando Olá Clip lista XML (toospecify da fonte de um ou vários arquivos, com ou sem cortar, etc.).</span><span class="sxs-lookup"><span data-stu-id="93774-108">Customizing hello Clip List XML (toospecify one or several source files, with or without trimming, etc.).</span></span>
* <span data-ttu-id="93774-109">Sobreposição de uma imagem de logotipo no vídeo de entrada hello enquanto Olá vídeo é codificado.</span><span class="sxs-lookup"><span data-stu-id="93774-109">Overlaying a logo image on hello input video while hello video is encoded.</span></span>
* <span data-ttu-id="93774-110">Vários idiomas de áudio codificação.</span><span class="sxs-lookup"><span data-stu-id="93774-110">Multiple audio language encoding.</span></span>

<span data-ttu-id="93774-111">Olá toolet **o fluxo de trabalho do Media Encoder Premium** saber que você está alterando algumas propriedades no fluxo de trabalho hello quando você cria tarefa hello ou enviar vários arquivos de entrada, se você tiver toouse uma cadeia de caracteres de configuração que contém  **setRuntimeProperties** e/ou **transcodeSource**.</span><span class="sxs-lookup"><span data-stu-id="93774-111">toolet hello **Media Encoder Premium Workflow** know that you are changing some properties in hello workflow when you create hello task or send multiple input files, you have toouse a configuration string that contains **setRuntimeProperties** and/or **transcodeSource**.</span></span> <span data-ttu-id="93774-112">Este tópico explica como toouse-los.</span><span class="sxs-lookup"><span data-stu-id="93774-112">This topic explains how toouse them.</span></span>

## <a name="configuration-string-syntax"></a><span data-ttu-id="93774-113">Sintaxe da cadeia de caracteres de configuração</span><span class="sxs-lookup"><span data-stu-id="93774-113">Configuration string syntax</span></span>
<span data-ttu-id="93774-114">Olá configuração cadeia de caracteres tooset em Olá codificação tarefa usa um documento XML que tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="93774-114">hello configuration string tooset in hello encoding task uses an XML document that looks like this:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<transcodeRequest>
  <transcodeSource>
  </transcodeSource>
  <setRuntimeProperties>
    <property propertyPath="Media File Input/filename" value="VideoFileName.mp4" />
  </setRuntimeProperties>
</transcodeRequest>
```

<span data-ttu-id="93774-115">a seguir Hello é código Olá c# que lê a configuração Olá XML de um arquivo, atualize-o com hello filename correto de vídeo e transmite toohello tarefas em um trabalho:</span><span class="sxs-lookup"><span data-stu-id="93774-115">hello following is hello C# code that reads hello XML configuration from a file, update it with hello right video filename and passes it toohello task in a job:</span></span>

```c#
string premiumConfiguration = ReadAllText(@"D:\home\site\wwwroot\Presets\SetRuntime.xml").Replace("VideoFileName", myVideoFileName);

// Declare a new job.
IJob job = _context.Jobs.Create("Premium Workflow encoding job");

// Get a media processor reference, and pass tooit hello name of hello 
// processor toouse for hello specific task.
IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

// Create a task with hello encoding details, using a string preset.
ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                              processor,
                              premiumConfiguration,
                              TaskOptions.None);

// Specify hello input assets
task.InputAssets.Add(workflow); // workflow asset
task.InputAssets.Add(video); // video asset with multiple files

// Add an output asset toocontain hello results of hello job. 
// This output is specified as AssetCreationOptions.None, which 
// means hello output asset is not encrypted. 
task.OutputAssets.AddNew("Output asset", AssetCreationOptions.None);
```

## <a name="customizing-component-properties"></a><span data-ttu-id="93774-116">Personalizando as propriedades do componente</span><span class="sxs-lookup"><span data-stu-id="93774-116">Customizing component properties</span></span>
### <a name="property-with-a-simple-value"></a><span data-ttu-id="93774-117">Propriedade com um valor simples</span><span class="sxs-lookup"><span data-stu-id="93774-117">Property with a simple value</span></span>
<span data-ttu-id="93774-118">Em alguns casos, é útil toocustomize uma propriedade do componente junto com o arquivo de fluxo de trabalho de saudação que será toobe executada pelo fluxo de trabalho Premium de codificador de mídia.</span><span class="sxs-lookup"><span data-stu-id="93774-118">In some cases, it is useful toocustomize a component property together with hello workflow file that is going toobe executed by Media Encoder Premium Workflow.</span></span>

<span data-ttu-id="93774-119">Suponha que você criou um fluxo de trabalho texto sobreposições em seus vídeos e texto de saudação (por exemplo, a saudação data atual) deve toobe conjunto em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="93774-119">Suppose you designed a workflow that overlays text on your videos, and hello text (for example, hello current date) is supposed toobe set at runtime.</span></span> <span data-ttu-id="93774-120">Você pode fazer isso enviando Olá texto toobe defina como o novo valor para a propriedade de texto de saudação do componente de sobreposição de saudação de saudação do hello tarefas de codificação.</span><span class="sxs-lookup"><span data-stu-id="93774-120">You can do this by sending hello text toobe set as hello new value for hello text property of hello overlay component from hello encoding task.</span></span> <span data-ttu-id="93774-121">Você pode usar esse mecanismo toochange outras propriedades de um componente no fluxo de trabalho de saudação (como Olá posição ou cor da sobreposição de hello, taxa de bits de saudação do codificador Olá AVC, etc.).</span><span class="sxs-lookup"><span data-stu-id="93774-121">You can use this mechanism toochange other properties of a component in hello workflow (such as hello position or color of hello overlay, hello bitrate of hello AVC encoder, etc.).</span></span>

<span data-ttu-id="93774-122">**setRuntimeProperties** é uma propriedade em componentes de saudação do fluxo de trabalho de saudação de toooverride usado.</span><span class="sxs-lookup"><span data-stu-id="93774-122">**setRuntimeProperties** is used toooverride a property in hello components of hello workflow.</span></span>

<span data-ttu-id="93774-123">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="93774-123">Example:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="MyInputVideo.mp4" />
      <property propertyPath="/primarySourceFile" value="MyInputVideo.mp4" />
      <property propertyPath="Optional Text Overlay/Text tooImage Converter/text" value="Today is Friday hello 13th of May, 2016"/>
  </setRuntimeProperties>
</transcodeRequest>
```

### <a name="property-with-an-xml-value"></a><span data-ttu-id="93774-124">Propriedade com um valor XML</span><span class="sxs-lookup"><span data-stu-id="93774-124">Property with an XML value</span></span>
<span data-ttu-id="93774-125">encapsular tooset uma propriedade que espera um valor XML, usando `<![CDATA[ and ]]>`.</span><span class="sxs-lookup"><span data-stu-id="93774-125">tooset a property that expects an XML value, encapsulate by using `<![CDATA[ and ]]>`.</span></span>

<span data-ttu-id="93774-126">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="93774-126">Example:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

> [!NOTE]
> <span data-ttu-id="93774-127">Certifique-se de não tooput um carro logo após retornar `<![CDATA[`.</span><span class="sxs-lookup"><span data-stu-id="93774-127">Make sure not tooput a carriage return just after `<![CDATA[`.</span></span>

### <a name="propertypath-value"></a><span data-ttu-id="93774-128">Valor de propertyPath</span><span class="sxs-lookup"><span data-stu-id="93774-128">propertyPath value</span></span>
<span data-ttu-id="93774-129">Nos exemplos anteriores do hello, Olá propertyPath foi "/ arquivo de mídia de entrada/filename" ou "/ inactiveTimeout" ou "clipListXml".</span><span class="sxs-lookup"><span data-stu-id="93774-129">In hello previous examples, hello propertyPath was "/Media File Input/filename" or "/inactiveTimeout" or "clipListXml".</span></span>
<span data-ttu-id="93774-130">Isso é, em geral, nome de saudação do componente de saudação e nome de saudação da propriedade hello.</span><span class="sxs-lookup"><span data-stu-id="93774-130">This is, in general, hello name of hello component, then hello name of hello property.</span></span> <span data-ttu-id="93774-131">Olá caminho pode ter mais ou menos níveis, como "/ primarySourceFile" (porque é propriedade de saudação na raiz de saudação do fluxo de trabalho Olá) ou "/ vídeo/opacidade de sobreposição processamento/gráfico" (porque Olá sobreposição está em um grupo).</span><span class="sxs-lookup"><span data-stu-id="93774-131">hello path can have more or fewer levels, like "/primarySourceFile" (because hello property is at hello root of hello workflow) or "/Video Processing/Graphic Overlay/Opacity" (because hello Overlay is in a group).</span></span>    

<span data-ttu-id="93774-132">toocheck Olá caminho e nome da propriedade, use Olá ação botão imediatamente ao lado de cada propriedade.</span><span class="sxs-lookup"><span data-stu-id="93774-132">toocheck hello path and property name, use hello action button that is immediately beside each property.</span></span> <span data-ttu-id="93774-133">Você pode clicar nesse botão de ação e escolher **Editar**.</span><span class="sxs-lookup"><span data-stu-id="93774-133">You can click this action button and select **Edit**.</span></span> <span data-ttu-id="93774-134">Isso mostrará você Olá real de nome da propriedade hello e imediatamente acima dela, Olá namespace.</span><span class="sxs-lookup"><span data-stu-id="93774-134">This will show you hello actual name of hello property, and immediately above it, hello namespace.</span></span>

![Ação/Editar](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture6_actionedit.png)

![Propriedade](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture7_viewproperty.png)

## <a name="multiple-input-files"></a><span data-ttu-id="93774-137">Vários arquivos de entrada</span><span class="sxs-lookup"><span data-stu-id="93774-137">Multiple input files</span></span>
<span data-ttu-id="93774-138">Cada tarefa que você enviar toohello **o fluxo de trabalho do Media Encoder Premium** requer dois ativos:</span><span class="sxs-lookup"><span data-stu-id="93774-138">Each task that you submit toohello **Media Encoder Premium Workflow** requires two assets:</span></span>

* <span data-ttu-id="93774-139">Olá primeiro um é um *fluxo de trabalho ativo* que contém um arquivo de fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="93774-139">hello first one is a *Workflow Asset* that contains a workflow file.</span></span> <span data-ttu-id="93774-140">Você pode criar arquivos de fluxo de trabalho usando Olá [Designer de fluxo de trabalho](media-services-workflow-designer.md).</span><span class="sxs-lookup"><span data-stu-id="93774-140">You can design workflow files by using hello [Workflow Designer](media-services-workflow-designer.md).</span></span>
* <span data-ttu-id="93774-141">Olá segundo é um *ativo de mídia* que contém Olá arquivos de mídia que você deseja tooencode.</span><span class="sxs-lookup"><span data-stu-id="93774-141">hello second one is a *Media Asset* that contains hello media file(s) that you want tooencode.</span></span>

<span data-ttu-id="93774-142">Quando você estiver enviando várias toohello de arquivos de mídia **o fluxo de trabalho do Media Encoder Premium** aplica do codificador, Olá restrições a seguir:</span><span class="sxs-lookup"><span data-stu-id="93774-142">When you're sending multiple media files toohello **Media Encoder Premium Workflow** encoder, hello following constraints apply:</span></span>

* <span data-ttu-id="93774-143">Olá de todas as mídias Olá arquivos devem estar no mesmo *ativo de mídia*.</span><span class="sxs-lookup"><span data-stu-id="93774-143">All hello media files must be in hello same *Media Asset*.</span></span> <span data-ttu-id="93774-144">Não há suporte para o uso de vários Ativos de Mídia.</span><span class="sxs-lookup"><span data-stu-id="93774-144">Using multiple Media Assets is not supported.</span></span>
* <span data-ttu-id="93774-145">Você deve definir o arquivo primário Olá nesse ativo de mídia (Idealmente, isso é hello principal arquivo de vídeo que Olá codificador é solicitado tooprocess).</span><span class="sxs-lookup"><span data-stu-id="93774-145">You must set hello primary file in this Media Asset (ideally, this is hello main video file that hello encoder is asked tooprocess).</span></span>
* <span data-ttu-id="93774-146">É necessário toopass dados de configuração que inclui a saudação **setRuntimeProperties** e/ou **transcodeSource** processador do elemento toohello.</span><span class="sxs-lookup"><span data-stu-id="93774-146">It is necessary toopass configuration data that includes hello **setRuntimeProperties** and/or **transcodeSource** element toohello processor.</span></span>
  * <span data-ttu-id="93774-147">**setRuntimeProperties** é propriedade de nome de arquivo hello toooverride usado ou outra propriedade em componentes de saudação do fluxo de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="93774-147">**setRuntimeProperties** is used toooverride hello filename property or another property in hello components of hello workflow.</span></span>
  * <span data-ttu-id="93774-148">**transcodeSource** é usado toospecify hello conteúdo XML de lista do clipe.</span><span class="sxs-lookup"><span data-stu-id="93774-148">**transcodeSource** is used toospecify hello Clip List XML content.</span></span>

<span data-ttu-id="93774-149">Conexões no fluxo de trabalho hello:</span><span class="sxs-lookup"><span data-stu-id="93774-149">Connections in hello workflow:</span></span>

* <span data-ttu-id="93774-150">Se você usar um ou vários componentes de entrada de arquivo de mídia e planejar toouse **setRuntimeProperties** toospecify Olá nome de arquivo, em seguida, não conecte Olá toothem de pin de componente de arquivo primário.</span><span class="sxs-lookup"><span data-stu-id="93774-150">If you use one or several Media File Input components and plan toouse **setRuntimeProperties** toospecify hello file name, then do not connect hello primary file component pin toothem.</span></span> <span data-ttu-id="93774-151">Certifique-se de que não há nenhuma conexão entre o objeto de arquivo primário hello e hello entradas do arquivo de mídia.</span><span class="sxs-lookup"><span data-stu-id="93774-151">Make sure that there is no connection between hello primary file object and hello Media File Input(s).</span></span>
* <span data-ttu-id="93774-152">Se você preferir toouse Clip lista XML e um componente de origem de mídia, em seguida, você pode conectar os dois juntos.</span><span class="sxs-lookup"><span data-stu-id="93774-152">If you prefer toouse Clip List XML and one Media Source component, then you can connect both together.</span></span>

![Nenhuma conexão de arquivo de origem primário tooMedia arquivo de entrada](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture0_nopin.png)

<span data-ttu-id="93774-154">*Não há nenhuma conexão de arquivo primário de saudação tooMedia componente (s) de entrada do arquivo se você usar a propriedade de nome de arquivo setRuntimeProperties tooset hello.*</span><span class="sxs-lookup"><span data-stu-id="93774-154">*There is no connection from hello primary file tooMedia File Input component(s) if you use setRuntimeProperties tooset hello filename property.*</span></span>

![Conexão do XML de lista de clipe tooClip fonte da lista](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture1_pincliplist.png)

<span data-ttu-id="93774-156">*Você pode conectar-se o XML de lista de clipe tooMedia fonte e usar transcodeSource.*</span><span class="sxs-lookup"><span data-stu-id="93774-156">*You can connect Clip List XML tooMedia Source and use transcodeSource.*</span></span>

### <a name="clip-list-xml-customization"></a><span data-ttu-id="93774-157">Personalização do XML da Lista de Clipes</span><span class="sxs-lookup"><span data-stu-id="93774-157">Clip List XML customization</span></span>
<span data-ttu-id="93774-158">Você pode especificar Olá Clip lista XML no fluxo de trabalho de saudação em tempo de execução usando **transcodeSource** na configuração de saudação de cadeia de caracteres XML.</span><span class="sxs-lookup"><span data-stu-id="93774-158">You can specify hello Clip List XML in hello workflow at runtime by using **transcodeSource** in hello configuration string XML.</span></span> <span data-ttu-id="93774-159">Isso requer Olá Clip lista XML pin toobe conectado toohello componente de origem de mídia no fluxo de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="93774-159">This requires hello Clip List XML pin toobe connected toohello Media Source component in hello workflow.</span></span>

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <transcodeSource>
      <clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>video-part1.mp4</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>video-part1.mp4</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
      </clipList>
    </transcodeSource>
    <setRuntimeProperties>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

<span data-ttu-id="93774-160">Se você deseja toospecify /primarySourceFile toouse esta saída de hello propriedade tooname arquivos usando 'Expressões', é recomendável passar Olá Clip lista XML como uma propriedade *depois* propriedade /primarySourceFile a saudação, tooavoid Lista de clipe ter Olá ser substituído definindo /primarySourceFile hello.</span><span class="sxs-lookup"><span data-stu-id="93774-160">If you want toospecify /primarySourceFile toouse this property tooname hello output files by using 'Expressions', then we recommend passing hello Clip List XML as a property *after* hello /primarySourceFile property, tooavoid having hello Clip List be overridden by hello /primarySourceFile setting.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="c:\temp\start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <mediaFile>
              <file>c:\temp\start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <mediaFile>
              <file>c:\temp\start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

<span data-ttu-id="93774-161">Com outro corte preciso de quadro:</span><span class="sxs-lookup"><span data-stu-id="93774-161">With additional frame-accurate trimming:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="/primarySourceFile" value="start.mxf" />
      <property propertyPath="/inactiveTimeout" value="65" />
      <property propertyPath="clipListXml" value="xxx">
      <extendedValue><![CDATA[<clipList>
        <clip>
          <videoSource>
            <trim>
              <inPoint fps="25">00:00:05:24</inPoint>
              <outPoint fps="25">00:00:10:24</outPoint>
            </trim>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </videoSource>
          <audioSource>
            <trim>
              <inPoint fps="25">00:00:05:24</inPoint>
              <outPoint fps="25">00:00:10:24</outPoint>
            </trim>
            <mediaFile>
              <file>start.mxf</file>
            </mediaFile>
          </audioSource>
        </clip>
        <primaryClipIndex>0</primaryClipIndex>
        </clipList>]]>
      </extendedValue>
      </property>
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

## <a name="example-1--overlay-an-image-on-top-of-hello-video"></a><span data-ttu-id="93774-162">Exemplo 1: Sobreposição de uma imagem na parte superior Olá vídeo</span><span class="sxs-lookup"><span data-stu-id="93774-162">Example 1 : Overlay an image on top of hello video</span></span>

### <a name="presentation"></a><span data-ttu-id="93774-163">Apresentação</span><span class="sxs-lookup"><span data-stu-id="93774-163">Presentation</span></span>
<span data-ttu-id="93774-164">Considere um exemplo no qual você deseja toooverlay uma imagem de logotipo no vídeo de entrada hello enquanto Olá vídeo é codificado.</span><span class="sxs-lookup"><span data-stu-id="93774-164">Consider an example in which you want toooverlay a logo image on hello input video while hello video is encoded.</span></span> <span data-ttu-id="93774-165">Neste exemplo, o vídeo de entrada hello será denominado "Microsoft_HoloLens_Possibilities_816p24.mp4" e o logotipo de saudação é "logo.png".</span><span class="sxs-lookup"><span data-stu-id="93774-165">In this example, hello input video is named "Microsoft_HoloLens_Possibilities_816p24.mp4" and hello logo is named "logo.png".</span></span> <span data-ttu-id="93774-166">Você deve executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="93774-166">You should perform hello following steps:</span></span>

* <span data-ttu-id="93774-167">Criar um ativo de fluxo de trabalho com o arquivo de fluxo de trabalho da saudação (consulte Olá exemplo a seguir).</span><span class="sxs-lookup"><span data-stu-id="93774-167">Create a Workflow Asset with hello workflow file (see hello following example).</span></span>
* <span data-ttu-id="93774-168">Criar um ativo de mídia, que contém dois arquivos: MyInputVideo.mp4 como Olá arquivo primário e MyLogo.png.</span><span class="sxs-lookup"><span data-stu-id="93774-168">Create a Media Asset, which contains two files: MyInputVideo.mp4 as hello primary file and MyLogo.png.</span></span>
* <span data-ttu-id="93774-169">Enviar um toohello tarefa mídia de fluxo de trabalho Premium de codificador de mídia ativos de entrada do processador com hello acima e especificar Olá cadeia de caracteres de configuração a seguir.</span><span class="sxs-lookup"><span data-stu-id="93774-169">Send a task toohello Media Encoder Premium Workflow media processor with hello above input assets and specify hello following configuration string.</span></span>

<span data-ttu-id="93774-170">Configuração:</span><span class="sxs-lookup"><span data-stu-id="93774-170">Configuration:</span></span>

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="/primarySourceFile" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

<span data-ttu-id="93774-171">No exemplo hello acima, o nome de Olá Olá do arquivo de vídeo seja enviado toohello entrada do arquivo de mídia componente e Olá primarySourceFile propriedade.</span><span class="sxs-lookup"><span data-stu-id="93774-171">In hello example above, hello name of hello video file is sent toohello Media File Input component and hello primarySourceFile property.</span></span> <span data-ttu-id="93774-172">nome de Olá Olá do arquivo de logotipo é enviado tooanother entrada de arquivo de mídia que é conectado toohello sobreposição gráfico componente.</span><span class="sxs-lookup"><span data-stu-id="93774-172">hello name of hello logo file is sent tooanother Media File Input that is connected toohello graphic overlay component.</span></span>

> [!NOTE]
> <span data-ttu-id="93774-173">nome do arquivo de vídeo de saudação é enviada toohello primarySourceFile propriedade.</span><span class="sxs-lookup"><span data-stu-id="93774-173">hello video file name is sent toohello primarySourceFile property.</span></span> <span data-ttu-id="93774-174">Olá razão para isso é toouse essa propriedade no fluxo de trabalho Olá para a criação de nome de arquivo de saída correta hello usando expressões, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="93774-174">hello reason for this is toouse this property in hello workflow for building hello correct output file name using Expressions, for example.</span></span>

### <a name="step-by-step-workflow-creation"></a><span data-ttu-id="93774-175">Criação de fluxo de trabalho passo a passo</span><span class="sxs-lookup"><span data-stu-id="93774-175">Step-by-step workflow creation</span></span>
<span data-ttu-id="93774-176">Aqui está Olá etapas toocreate um fluxo de trabalho que usa dois arquivos como entrada: um vídeo e uma imagem.</span><span class="sxs-lookup"><span data-stu-id="93774-176">Here are hello steps toocreate a workflow that takes two files as input: a video and an image.</span></span> <span data-ttu-id="93774-177">Ele irá sobrepor imagem Olá sobre Olá vídeo.</span><span class="sxs-lookup"><span data-stu-id="93774-177">It will overlay hello image on top of hello video.</span></span>

<span data-ttu-id="93774-178">Abra o **Designer de Fluxo de Trabalho** e selecione **Arquivo** > **Novo Espaço de Trabalho** > **Transcodificar Esquema**.</span><span class="sxs-lookup"><span data-stu-id="93774-178">Open **Workflow Designer** and select **File** > **New Workspace** > **Transcode Blueprint**.</span></span>

<span data-ttu-id="93774-179">novo fluxo de trabalho de saudação mostra três elementos:</span><span class="sxs-lookup"><span data-stu-id="93774-179">hello new workflow shows three elements:</span></span>

* <span data-ttu-id="93774-180">Arquivo de Origem Principal</span><span class="sxs-lookup"><span data-stu-id="93774-180">Primary Source File</span></span>
* <span data-ttu-id="93774-181">XML da Lista de Clipes</span><span class="sxs-lookup"><span data-stu-id="93774-181">Clip List XML</span></span>
* <span data-ttu-id="93774-182">Arquivo/Ativo de Saída</span><span class="sxs-lookup"><span data-stu-id="93774-182">Output File/Asset</span></span>  

![Novo fluxo de trabalho de codificação](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture9_empty.png)

<span data-ttu-id="93774-184">*Novo fluxo de trabalho de codificação*</span><span class="sxs-lookup"><span data-stu-id="93774-184">*New Encoding Workflow*</span></span>

<span data-ttu-id="93774-185">No arquivo de mídia de entrada do pedido tooaccept hello, comece a adicionar um componente de entrada de arquivo de mídia.</span><span class="sxs-lookup"><span data-stu-id="93774-185">In order tooaccept hello input media file, start with adding a Media File Input component.</span></span> <span data-ttu-id="93774-186">tooadd um fluxo de trabalho toohello de componente, procure-a na caixa de pesquisa de repositório hello e arrastar entrada hello desejado no painel de designer do hello.</span><span class="sxs-lookup"><span data-stu-id="93774-186">tooadd a component toohello workflow, look for it in hello Repository search box and drag hello desired entry onto hello designer pane.</span></span>

<span data-ttu-id="93774-187">Em seguida, adicione Olá toobe de arquivo de vídeo usada para criar o fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="93774-187">Next, add hello video file toobe used for designing your workflow.</span></span> <span data-ttu-id="93774-188">toodo assim, clique em Painel de plano de fundo Olá no Designer de fluxo de trabalho e procure a propriedade de arquivo de origem primário Olá no painel de propriedade direito hello.</span><span class="sxs-lookup"><span data-stu-id="93774-188">toodo so, click hello background pane in Workflow Designer and look for hello Primary Source File property on hello right-hand property pane.</span></span> <span data-ttu-id="93774-189">Clique Olá ícone da pasta e selecione o arquivo de vídeo apropriado hello.</span><span class="sxs-lookup"><span data-stu-id="93774-189">Click hello folder icon and select hello appropriate video file.</span></span>

![Fonte de Arquivo Primário](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture10_primaryfile.png)

<span data-ttu-id="93774-191">*Fonte de Arquivo Primário*</span><span class="sxs-lookup"><span data-stu-id="93774-191">*Primary File Source*</span></span>

<span data-ttu-id="93774-192">Em seguida, especifique o arquivo de vídeo Olá no componente de entrada de arquivo de mídia hello.</span><span class="sxs-lookup"><span data-stu-id="93774-192">Next, specify hello video file in hello Media File Input component.</span></span>   

![Fonte de Entrada do Arquivo de Mídia](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture11_mediafileinput.png)

<span data-ttu-id="93774-194">*Fonte de Entrada do Arquivo de Mídia*</span><span class="sxs-lookup"><span data-stu-id="93774-194">*Media File Input Source*</span></span>

<span data-ttu-id="93774-195">Assim que isso for feito, o componente de entrada de arquivo de mídia Olá inspecionar o arquivo hello e preencher sua saída pins tooreflect Olá arquivo que ele inspecionado.</span><span class="sxs-lookup"><span data-stu-id="93774-195">As soon as this is done, hello Media File Input component will inspect hello file and populate its output pins tooreflect hello file that it inspected.</span></span>

<span data-ttu-id="93774-196">Olá próxima etapa é tooadd tooRec.709 de espaço de cor um "Atualizador de tipo de dados de vídeo" toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="93774-196">hello next step is tooadd a "Video Data Type Updater" toospecify hello color space tooRec.709.</span></span> <span data-ttu-id="93774-197">Adicionar um "vídeo formato conversor" que é definir o tipo de Layout/Layout tooData = configurável Planar.</span><span class="sxs-lookup"><span data-stu-id="93774-197">Add a "Video Format Converter" that is set tooData Layout/Layout type = Configurable Planar.</span></span> <span data-ttu-id="93774-198">Isso converterá o formato de tooa de fluxo de vídeo Olá que pode ser executado como uma origem de componente de sobreposição de saudação.</span><span class="sxs-lookup"><span data-stu-id="93774-198">This will convert hello video stream tooa format that can be taken as a source of hello overlay component.</span></span>

![Atualizador de tipo de dados e conversor de formato de vídeo](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter.png)

<span data-ttu-id="93774-200">*Atualizador de tipo de dados e conversor de formato de vídeo*</span><span class="sxs-lookup"><span data-stu-id="93774-200">*Video Data Type Updater and Format Converter*</span></span>

![Tipo de layout = Planar Configurável](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter2.png)

<span data-ttu-id="93774-202">*O Tipo de layout é Planar Configurável*</span><span class="sxs-lookup"><span data-stu-id="93774-202">*Layout type is Configurable Planar*</span></span>

<span data-ttu-id="93774-203">Em seguida, adicione um componente de sobreposição de vídeo e conecte Olá pin de vídeo (descompactado) toohello (descompactado) vídeo pin de entrada de arquivo de mídia hello.</span><span class="sxs-lookup"><span data-stu-id="93774-203">Next, add a Video Overlay component and connect hello (uncompressed) video pin toohello (uncompressed) video pin of hello media file input.</span></span>

<span data-ttu-id="93774-204">Adicionar outra entrada de arquivo de mídia (arquivo de logotipo do tooload Olá), clique neste componente e renomeá-lo muito "Logotipo de entrada de arquivo de mídia" e selecione uma imagem (um arquivo. png por exemplo) na propriedade do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="93774-204">Add another Media File Input (tooload hello logo file), click on this component and rename it too"Media File Input Logo", and select an image (a .png file for example) in hello file property.</span></span> <span data-ttu-id="93774-205">Conecte-se Olá imagem descompactada pinos toohello imagem descompactada pinos da sobreposição de saudação.</span><span class="sxs-lookup"><span data-stu-id="93774-205">Connect hello Uncompressed image pin toohello Uncompressed image pin of hello overlay.</span></span>

![Fonte de arquivo de imagem e componente de sobreposição](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture13_overlay.png)

<span data-ttu-id="93774-207">*Fonte de arquivo de imagem e componente de sobreposição*</span><span class="sxs-lookup"><span data-stu-id="93774-207">*Overlay component and image file source*</span></span>

<span data-ttu-id="93774-208">Se você deseja toomodify Olá posição do logotipo Olá no vídeo de saudação (por exemplo, você talvez queira tooposition-lo em 10 por cento da parte superior da saudação canto esquerdo do vídeo Olá), desmarque caixa de seleção "Entrada Manual" hello.</span><span class="sxs-lookup"><span data-stu-id="93774-208">If you want toomodify hello position of hello logo on hello video (for example, you might want tooposition it at 10 percent off of hello top left corner of hello video), clear hello "Manual Input" check box.</span></span> <span data-ttu-id="93774-209">Você pode fazer isso porque você está usando um entrada de arquivo de mídia tooprovide Olá logotipo arquivo toohello sobreposição componente.</span><span class="sxs-lookup"><span data-stu-id="93774-209">You can do this because you are using a Media File Input tooprovide hello logo file toohello overlay component.</span></span>

![Posição da sobreposição](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture14_overlay_position.png)

<span data-ttu-id="93774-211">*Posição da sobreposição*</span><span class="sxs-lookup"><span data-stu-id="93774-211">*Overlay position*</span></span>

<span data-ttu-id="93774-212">tooencode Olá tooH.264 do fluxo de vídeo, adicione hello AVC codificador de vídeo e a superfície do designer de toohello AAC codificador componentes.</span><span class="sxs-lookup"><span data-stu-id="93774-212">tooencode hello video stream tooH.264, add hello AVC Video Encoder and AAC encoder components toohello designer surface.</span></span> <span data-ttu-id="93774-213">Conecte-se os pins hello.</span><span class="sxs-lookup"><span data-stu-id="93774-213">Connect hello pins.</span></span>
<span data-ttu-id="93774-214">Configure o codificador AAC hello e selecione conversão de formato de áudio/predefinição: 2.0 (L, R).</span><span class="sxs-lookup"><span data-stu-id="93774-214">Set up hello AAC encoder and select Audio Format Conversion/Preset : 2.0 (L, R).</span></span>

![Codificadores de Áudio e Vídeo](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture15_encoders.png)

<span data-ttu-id="93774-216">*Codificadores de Áudio e Vídeo*</span><span class="sxs-lookup"><span data-stu-id="93774-216">*Audio and Video Encoders*</span></span>

<span data-ttu-id="93774-217">Agora adicione Olá **ISO Mpeg-4 multiplexador** e **arquivo de saída** componentes e conecte-se pins hello, conforme mostrado.</span><span class="sxs-lookup"><span data-stu-id="93774-217">Now add hello **ISO Mpeg-4 Multiplexer** and **File Output** components and connect hello pins as shown.</span></span>

![Multiplexador MP4 e saída de arquivo](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture16_mp4output.png)

<span data-ttu-id="93774-219">*Multiplexador MP4 e saída de arquivo*</span><span class="sxs-lookup"><span data-stu-id="93774-219">*MP4 multiplexer and file output*</span></span>

<span data-ttu-id="93774-220">Você precisará tooset Olá nome para o arquivo de saída hello.</span><span class="sxs-lookup"><span data-stu-id="93774-220">You need tooset hello name for hello output file.</span></span> <span data-ttu-id="93774-221">Clique em Olá **arquivo de saída** componente e Editar expressão Olá para o arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="93774-221">Click hello **File Output** component and edit hello expression for hello file:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_withoverlay.mp4

![Nome de saída do arquivo](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture17_filenameoutput.png)

<span data-ttu-id="93774-223">*Nome de saída do arquivo*</span><span class="sxs-lookup"><span data-stu-id="93774-223">*File output name*</span></span>

<span data-ttu-id="93774-224">Você pode executar o fluxo de trabalho Olá localmente toocheck que está sendo executado corretamente.</span><span class="sxs-lookup"><span data-stu-id="93774-224">You can run hello workflow locally toocheck that it is running correctly.</span></span>

<span data-ttu-id="93774-225">Após a conclusão, você poderá executá-lo nos Serviços de Mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="93774-225">After it finishes, you can run it in Azure Media Services.</span></span>

<span data-ttu-id="93774-226">Primeiro, preparar um ativo no Azure Media Services com dois arquivos: o arquivo de vídeo hello e logotipo hello.</span><span class="sxs-lookup"><span data-stu-id="93774-226">First, prepare an asset in Azure Media Services with two files in it: hello video file and hello logo.</span></span> <span data-ttu-id="93774-227">Você pode fazer isso usando a API Olá .NET ou REST.</span><span class="sxs-lookup"><span data-stu-id="93774-227">You can do this by using hello .NET or REST API.</span></span> <span data-ttu-id="93774-228">Você também pode fazer isso usando o portal do Azure de saudação ou [Gerenciador de serviços de mídia do Azure](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).</span><span class="sxs-lookup"><span data-stu-id="93774-228">You can also do this by using hello Azure portal or [Azure Media Services Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).</span></span>

<span data-ttu-id="93774-229">Este tutorial mostra como ativos de toomanage com AMSE.</span><span class="sxs-lookup"><span data-stu-id="93774-229">This tutorial shows you how toomanage assets with AMSE.</span></span> <span data-ttu-id="93774-230">Há dois ativo tooan tooadd arquivos de formas:</span><span class="sxs-lookup"><span data-stu-id="93774-230">There are two ways tooadd files tooan asset:</span></span>

* <span data-ttu-id="93774-231">Criar uma pasta local, copiar Olá dois arquivos e arrastar e soltar Olá pasta toohello **ativo** guia.</span><span class="sxs-lookup"><span data-stu-id="93774-231">Create a local folder, copy hello two files in it, and drag and drop hello folder toohello **Asset** tab.</span></span>
* <span data-ttu-id="93774-232">Carregar o arquivo de vídeo hello como um ativo, exibir informações sobre os ativos hello, acesse a guia arquivos de toohello e carregar um arquivo adicional (logotipo).</span><span class="sxs-lookup"><span data-stu-id="93774-232">Upload hello video file as an asset, display hello asset information, go toohello files tab, and upload an additional file (logo).</span></span>

> [!NOTE]
> <span data-ttu-id="93774-233">Verifique se tooset um arquivo primário no ativo hello (Olá principal arquivo de vídeo).</span><span class="sxs-lookup"><span data-stu-id="93774-233">Make sure tooset a primary file in hello asset (hello main video file).</span></span>

![Arquivos de ativo no AMSE](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture18_assetinamse.png)

<span data-ttu-id="93774-235">*Arquivos de ativo no AMSE*</span><span class="sxs-lookup"><span data-stu-id="93774-235">*Asset files in AMSE*</span></span>

<span data-ttu-id="93774-236">Selecione Olá ativo e escolha tooencode com o codificador Premium.</span><span class="sxs-lookup"><span data-stu-id="93774-236">Select hello asset and choose tooencode it with Premium Encoder.</span></span> <span data-ttu-id="93774-237">Carregar o fluxo de trabalho hello e selecioná-lo.</span><span class="sxs-lookup"><span data-stu-id="93774-237">Upload hello workflow and select it.</span></span>

<span data-ttu-id="93774-238">Clique em processador de toohello Olá botão toopass dados e, em seguida, adicione Olá propriedades de tempo de execução XML tooset Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="93774-238">Click hello button toopass data toohello processor, and add hello following XML tooset hello runtime properties:</span></span>

![Codificador Premium no AMSE](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture19_amsepremium.png)

<span data-ttu-id="93774-240">*Codificador Premium no AMSE*</span><span class="sxs-lookup"><span data-stu-id="93774-240">*Premium Encoder in AMSE*</span></span>

<span data-ttu-id="93774-241">Em seguida, cole Olá dados XML a seguir.</span><span class="sxs-lookup"><span data-stu-id="93774-241">Then, paste hello following XML data.</span></span> <span data-ttu-id="93774-242">Você precisa toospecify nome de Olá Olá do arquivo de vídeo para Olá entrada de arquivo de mídia e primarySourceFile.</span><span class="sxs-lookup"><span data-stu-id="93774-242">You need toospecify hello name of hello video file for both hello Media File Input and primarySourceFile.</span></span> <span data-ttu-id="93774-243">Especifique o nome de saudação do nome de arquivo de saudação do logotipo Olá muito.</span><span class="sxs-lookup"><span data-stu-id="93774-243">Specify hello name of hello file name for hello logo too.</span></span>

```xml
<?xml version="1.0" encoding="utf-16"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="/primarySourceFile" value="Microsoft_HoloLens_Possibilities_816p24.mp4" />
      <property propertyPath="Media File Input Logo/filename" value="logo.png" />
    </setRuntimeProperties>
  </transcodeRequest>
```

![setRuntimeProperties](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture20_amsexmldata.png)

<span data-ttu-id="93774-245">*setRuntimeProperties*</span><span class="sxs-lookup"><span data-stu-id="93774-245">*setRuntimeProperties*</span></span>

<span data-ttu-id="93774-246">Se você usar Olá .NET SDK toocreate e executa tarefas de hello, esses dados XML tem toobe passado como cadeia de caracteres de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="93774-246">If you use hello .NET SDK toocreate and run hello task, this XML data has toobe passed as hello configuration string.</span></span>

```c#
public ITask AddNew(string taskName, IMediaProcessor mediaProcessor, string configuration, TaskOptions options);
```

<span data-ttu-id="93774-247">Após a conclusão do trabalho hello, arquivo hello MP4 Olá saída ativo exibe sobreposição Olá!</span><span class="sxs-lookup"><span data-stu-id="93774-247">After hello job is complete, hello MP4 file in hello output asset displays hello overlay!</span></span>

![Sobreposição de vídeo de saudação](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture21_resultoverlay.png)

<span data-ttu-id="93774-249">*Sobreposição de vídeo de saudação*</span><span class="sxs-lookup"><span data-stu-id="93774-249">*Overlay on hello video*</span></span>

<span data-ttu-id="93774-250">Você pode baixar o fluxo de trabalho de exemplo de saudação do [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).</span><span class="sxs-lookup"><span data-stu-id="93774-250">You can download hello sample workflow from [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).</span></span>

## <a name="example-2--multiple-audio-language-encoding"></a><span data-ttu-id="93774-251">Exemplo 2: Codificação de vários idiomas de áudio</span><span class="sxs-lookup"><span data-stu-id="93774-251">Example 2 : Multiple audio language encoding</span></span>

<span data-ttu-id="93774-252">Um exemplo de fluxo de trabalho de codificação de vários idiomas de áudio está disponível em [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding).</span><span class="sxs-lookup"><span data-stu-id="93774-252">An example of multiple audio language encoding workfkow is available in [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding).</span></span>

<span data-ttu-id="93774-253">Esta pasta contém um fluxo de trabalho de exemplo que pode ser usado tooencode um ativo de arquivos MXF arquivos tooa várias MP4 com várias faixas de áudio.</span><span class="sxs-lookup"><span data-stu-id="93774-253">This folder contains a sample workflow which can be used tooencode a MXF file tooa multi MP4 files asset with multiple audio tracks.</span></span>

<span data-ttu-id="93774-254">Este fluxo de trabalho supõe que esse arquivo MXF Olá contém uma faixa de áudio; faixas de áudio adicionais Olá devem ser passadas como arquivos de áudio separados (WAV ou MP4...).</span><span class="sxs-lookup"><span data-stu-id="93774-254">This workflow assumes that hello MXF file contains one audio track ; hello additional audio tracks should be passed as seperate audio files (WAV or MP4...).</span></span>

<span data-ttu-id="93774-255">tooencode, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="93774-255">tooencode, please follow these steps:</span></span>

* <span data-ttu-id="93774-256">Crie um ativo de serviços de mídia com hello e Olá MXF arquivos de áudio (0 too18 arquivos de áudio).</span><span class="sxs-lookup"><span data-stu-id="93774-256">Create a Media Services asset with hello MXF file and hello Audio files (0 too18 audio files).</span></span>
* <span data-ttu-id="93774-257">Verifique se o que arquivo hello MXF é definido como um arquivo primário.</span><span class="sxs-lookup"><span data-stu-id="93774-257">Make sure that hello MXF file is set as a primary file.</span></span>
* <span data-ttu-id="93774-258">Crie um trabalho e uma tarefa usando o processador de codificador de fluxo de trabalho Premium Olá.</span><span class="sxs-lookup"><span data-stu-id="93774-258">Create a job and a task using hello Premium Workflow Encoder processor.</span></span> <span data-ttu-id="93774-259">Use o fluxo de trabalho de saudação fornecido (MultiMP4-1080p-19audio-v1.workflow).</span><span class="sxs-lookup"><span data-stu-id="93774-259">Use hello workflow provided (MultiMP4-1080p-19audio-v1.workflow).</span></span>
* <span data-ttu-id="93774-260">Passe a tarefa de toohello Olá setruntime.xml dados (se você usar o Gerenciador de serviços de mídia do Azure, use hello "passar o fluxo de trabalho de toohello de dados xml" botão).</span><span class="sxs-lookup"><span data-stu-id="93774-260">Pass hello setruntime.xml data toohello task (if you use Azure Media Services Explorer, use hello “pass xml data toohello workflow” button).</span></span>
  * <span data-ttu-id="93774-261">Atualize Olá dados toospecify Olá arquivo correto nomes e linguagens de marcas XML.</span><span class="sxs-lookup"><span data-stu-id="93774-261">Please update hello XML data toospecify hello correct file names and languages tags.</span></span>
  * <span data-ttu-id="93774-262">fluxo de trabalho Olá tem componentes de áudio denominados 1 áudio tooAudio 18.</span><span class="sxs-lookup"><span data-stu-id="93774-262">hello workflow has audio components named Audio 1 tooAudio 18.</span></span>
  * <span data-ttu-id="93774-263">RFC5646 há suporte para a marca de idioma hello.</span><span class="sxs-lookup"><span data-stu-id="93774-263">RFC5646 is supported for hello language tag.</span></span>

```xml
<?xml version="1.0" encoding="utf-16"?>
<transcodeRequest>
  <setRuntimeProperties>
    <property propertyPath="Media File Input Video/filename" value="MainVideo.mxf" />
    <property propertyPath="Language/language_code" value="en" />
    <property propertyPath="/primarySourceFile" value="MainVideo.mxf" />
    <property propertyPath="Audio 1/Media File Input/filename" value="french-audio.wav" />
    <property propertyPath="Audio 1/Language/language_code" value="fr" />
    <property propertyPath="Audio 2/Media File Input/filename" value="german-audio.wav" />
    <property propertyPath="Audio 2/Language/language_code" value="de" />
    <property propertyPath="Audio 3/Media File Input/filename" value="japanese-audio.wav" />
    <property propertyPath="Audio 3/Language/language_code" value="ja" />
  </setRuntimeProperties>
</transcodeRequest>
```

* <span data-ttu-id="93774-264">ativo Olá codificado conterá várias faixas de áudio de linguagem e essas faixas devem ser selecionáveis no Azure Media Player.</span><span class="sxs-lookup"><span data-stu-id="93774-264">hello encoded asset will contain multi language audio tracks and these tracks should be selectable in Azure Media Player.</span></span>

## <a name="see-also"></a><span data-ttu-id="93774-265">Consulte também</span><span class="sxs-lookup"><span data-stu-id="93774-265">See also</span></span>
* [<span data-ttu-id="93774-266">Apresentando a codificação Premium nos Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="93774-266">Introducing Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)
* [<span data-ttu-id="93774-267">Como toouse Premium de codificação no Azure Media Services</span><span class="sxs-lookup"><span data-stu-id="93774-267">How toouse Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)
* [<span data-ttu-id="93774-268">Encoding on-demand content with Azure Media Services (Codificação do conteúdo sob demanda com os Serviços de Mídia do Azure)</span><span class="sxs-lookup"><span data-stu-id="93774-268">Encoding on-demand content with Azure Media Services</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)
* [<span data-ttu-id="93774-269">Codecs e formatos de fluxo de trabalho do Media Encoder Premium</span><span class="sxs-lookup"><span data-stu-id="93774-269">Media Encoder Premium Workflow formats and codecs</span></span>](media-services-premium-workflow-encoder-formats.md)
* [<span data-ttu-id="93774-270">Exemplos de arquivos de fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="93774-270">Sample workflow files</span></span>](https://github.com/AzureMediaServicesSamples/Encoding-Presets/tree/master/VoD/MediaEncoderPremiumWorkfows)
* [<span data-ttu-id="93774-271">Ferramenta do Explorador dos Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="93774-271">Azure Media Services Explorer tool</span></span>](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a><span data-ttu-id="93774-272">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="93774-272">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="93774-273">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="93774-273">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
