---
title: "Vários arquivos de entrada e propriedades de componente com o Codificador Premium - Azure | Microsoft Docs"
description: "Este tópico explica como usar setRuntimeProperties para usar vários arquivos de entrada e transmitir dados personalizados para o processador de mídia do Fluxo de Trabalho Premium do Codificador de Mídia."
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
ms.openlocfilehash: df1ee5089a0af6ffce1431b658843fcb34a66ce5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="using-multiple-input-files-and-component-properties-with-premium-encoder"></a><span data-ttu-id="69e7b-103">Usando vários arquivos de entrada e propriedades do componente com o Codificador Premium</span><span class="sxs-lookup"><span data-stu-id="69e7b-103">Using multiple input files and component properties with Premium Encoder</span></span>
## <a name="overview"></a><span data-ttu-id="69e7b-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="69e7b-104">Overview</span></span>
<span data-ttu-id="69e7b-105">Há situações em que talvez você precise personalizar as propriedades do componente, especificar o conteúdo XML da Lista de Clipes ou enviar vários arquivos de entrada ao enviar uma tarefa com o processador de mídia **Fluxo de trabalho Premium de codificação de mídia** .</span><span class="sxs-lookup"><span data-stu-id="69e7b-105">There are scenarios in which you might need to customize component properties, specify Clip List XML content, or send multiple input files when you submit a task with the **Media Encoder Premium Workflow** media processor.</span></span> <span data-ttu-id="69e7b-106">Alguns exemplos incluem:</span><span class="sxs-lookup"><span data-stu-id="69e7b-106">Some examples are:</span></span>

* <span data-ttu-id="69e7b-107">Sobreposição de texto em vídeo e definição do valor do texto (por exemplo, a data atual) no tempo de execução de cada vídeo de entrada.</span><span class="sxs-lookup"><span data-stu-id="69e7b-107">Overlaying text on video and setting the text value (for example, the current date) at runtime for each input video.</span></span>
* <span data-ttu-id="69e7b-108">Personalização do XML da Lista de Clipes (para especificar um ou vários arquivos de origem, com ou sem corte etc.).</span><span class="sxs-lookup"><span data-stu-id="69e7b-108">Customizing the Clip List XML (to specify one or several source files, with or without trimming, etc.).</span></span>
* <span data-ttu-id="69e7b-109">Sobreposição de uma imagem de logotipo no vídeo de entrada durante a codificação do vídeo.</span><span class="sxs-lookup"><span data-stu-id="69e7b-109">Overlaying a logo image on the input video while the video is encoded.</span></span>
* <span data-ttu-id="69e7b-110">Vários idiomas de áudio codificação.</span><span class="sxs-lookup"><span data-stu-id="69e7b-110">Multiple audio language encoding.</span></span>

<span data-ttu-id="69e7b-111">Para permitir que o **Fluxo de Trabalho Premium do Codificador de Mídia** reconheça que você está alterando algumas propriedades no fluxo de trabalho ao criar a tarefa ou enviar vários arquivos de entrada, é necessário usar uma cadeia de caracteres de configuração que contenha **setRuntimeProperties** e/ou **transcodeSource**.</span><span class="sxs-lookup"><span data-stu-id="69e7b-111">To let the **Media Encoder Premium Workflow** know that you are changing some properties in the workflow when you create the task or send multiple input files, you have to use a configuration string that contains **setRuntimeProperties** and/or **transcodeSource**.</span></span> <span data-ttu-id="69e7b-112">Este tópico explica como usá-los.</span><span class="sxs-lookup"><span data-stu-id="69e7b-112">This topic explains how to use them.</span></span>

## <a name="configuration-string-syntax"></a><span data-ttu-id="69e7b-113">Sintaxe da cadeia de caracteres de configuração</span><span class="sxs-lookup"><span data-stu-id="69e7b-113">Configuration string syntax</span></span>
<span data-ttu-id="69e7b-114">A cadeia de caracteres de configuração a ser definida na tarefa de codificação usa um documento XML com esta aparência:</span><span class="sxs-lookup"><span data-stu-id="69e7b-114">The configuration string to set in the encoding task uses an XML document that looks like this:</span></span>

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

<span data-ttu-id="69e7b-115">Veja a seguir o código C# que lê a configuração XML em um arquivo, o atualiza com o nome de arquivo de vídeo correto e a transfere para a tarefa em um trabalho:</span><span class="sxs-lookup"><span data-stu-id="69e7b-115">The following is the C# code that reads the XML configuration from a file, update it with the right video filename and passes it to the task in a job:</span></span>

```c#
string premiumConfiguration = ReadAllText(@"D:\home\site\wwwroot\Presets\SetRuntime.xml").Replace("VideoFileName", myVideoFileName);

// Declare a new job.
IJob job = _context.Jobs.Create("Premium Workflow encoding job");

// Get a media processor reference, and pass to it the name of the 
// processor to use for the specific task.
IMediaProcessor processor = GetLatestMediaProcessorByName("Media Encoder Premium Workflow");

// Create a task with the encoding details, using a string preset.
ITask task = job.Tasks.AddNew("Premium Workflow encoding task",
                              processor,
                              premiumConfiguration,
                              TaskOptions.None);

// Specify the input assets
task.InputAssets.Add(workflow); // workflow asset
task.InputAssets.Add(video); // video asset with multiple files

// Add an output asset to contain the results of the job. 
// This output is specified as AssetCreationOptions.None, which 
// means the output asset is not encrypted. 
task.OutputAssets.AddNew("Output asset", AssetCreationOptions.None);
```

## <a name="customizing-component-properties"></a><span data-ttu-id="69e7b-116">Personalizando as propriedades do componente</span><span class="sxs-lookup"><span data-stu-id="69e7b-116">Customizing component properties</span></span>
### <a name="property-with-a-simple-value"></a><span data-ttu-id="69e7b-117">Propriedade com um valor simples</span><span class="sxs-lookup"><span data-stu-id="69e7b-117">Property with a simple value</span></span>
<span data-ttu-id="69e7b-118">Em alguns casos, é útil personalizar uma propriedade do componente junto com o arquivo de fluxo de trabalho que será executado pelo Fluxo de Trabalho Premium do Codificador de Mídia.</span><span class="sxs-lookup"><span data-stu-id="69e7b-118">In some cases, it is useful to customize a component property together with the workflow file that is going to be executed by Media Encoder Premium Workflow.</span></span>

<span data-ttu-id="69e7b-119">Suponha que você tenha criado um fluxo de trabalho que sobrepõe texto em vídeos, e que o texto (por exemplo, a data atual) deva ser definido em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="69e7b-119">Suppose you designed a workflow that overlays text on your videos, and the text (for example, the current date) is supposed to be set at runtime.</span></span> <span data-ttu-id="69e7b-120">É possível fazer isso enviando o texto a ser definido como o novo valor da propriedade de texto do componente de sobreposição por meio da tarefa de codificação.</span><span class="sxs-lookup"><span data-stu-id="69e7b-120">You can do this by sending the text to be set as the new value for the text property of the overlay component from the encoding task.</span></span> <span data-ttu-id="69e7b-121">Você pode usar esse mecanismo para alterar outras propriedades de um componente no fluxo de trabalho (por exemplo, a posição ou a cor da sobreposição, a taxa de bits do codificador AVC etc.).</span><span class="sxs-lookup"><span data-stu-id="69e7b-121">You can use this mechanism to change other properties of a component in the workflow (such as the position or color of the overlay, the bitrate of the AVC encoder, etc.).</span></span>

<span data-ttu-id="69e7b-122">**setRuntimeProperties** é usado para substituir uma propriedade nos componentes do fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="69e7b-122">**setRuntimeProperties** is used to override a property in the components of the workflow.</span></span>

<span data-ttu-id="69e7b-123">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="69e7b-123">Example:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
  <transcodeRequest>
    <setRuntimeProperties>
      <property propertyPath="Media File Input/filename" value="MyInputVideo.mp4" />
      <property propertyPath="/primarySourceFile" value="MyInputVideo.mp4" />
      <property propertyPath="Optional Text Overlay/Text To Image Converter/text" value="Today is Friday the 13th of May, 2016"/>
  </setRuntimeProperties>
</transcodeRequest>
```

### <a name="property-with-an-xml-value"></a><span data-ttu-id="69e7b-124">Propriedade com um valor XML</span><span class="sxs-lookup"><span data-stu-id="69e7b-124">Property with an XML value</span></span>
<span data-ttu-id="69e7b-125">Para definir uma propriedade que espere um valor XML, encapsule-a usando `<![CDATA[ and ]]>`.</span><span class="sxs-lookup"><span data-stu-id="69e7b-125">To set a property that expects an XML value, encapsulate by using `<![CDATA[ and ]]>`.</span></span>

<span data-ttu-id="69e7b-126">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="69e7b-126">Example:</span></span>

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
> <span data-ttu-id="69e7b-127">Lembre-se de não colocar um retorno de carro logo após `<![CDATA[`.</span><span class="sxs-lookup"><span data-stu-id="69e7b-127">Make sure not to put a carriage return just after `<![CDATA[`.</span></span>

### <a name="propertypath-value"></a><span data-ttu-id="69e7b-128">Valor de propertyPath</span><span class="sxs-lookup"><span data-stu-id="69e7b-128">propertyPath value</span></span>
<span data-ttu-id="69e7b-129">Nos exemplos anteriores, propertyPath era “/Entrada de Arquivo de Mídia/nomearquivo”, “/inactiveTimeout” ou “clipListXml”.</span><span class="sxs-lookup"><span data-stu-id="69e7b-129">In the previous examples, the propertyPath was "/Media File Input/filename" or "/inactiveTimeout" or "clipListXml".</span></span>
<span data-ttu-id="69e7b-130">Em geral, esse é o nome do componente que, por sua vez, é o nome da propriedade.</span><span class="sxs-lookup"><span data-stu-id="69e7b-130">This is, in general, the name of the component, then the name of the property.</span></span> <span data-ttu-id="69e7b-131">O caminho pode ter mais ou menos níveis, como "/primarySourceFile" (pois a propriedade está na raiz do fluxo de trabalho) ou "/Processamento de Vídeo/Sobreposição Gráfica/Opacidade" (pois a Sobreposição está em um grupo).</span><span class="sxs-lookup"><span data-stu-id="69e7b-131">The path can have more or fewer levels, like "/primarySourceFile" (because the property is at the root of the workflow) or "/Video Processing/Graphic Overlay/Opacity" (because the Overlay is in a group).</span></span>    

<span data-ttu-id="69e7b-132">Para verificar o caminho e o nome da propriedade, use o botão de ação ao lado de cada propriedade.</span><span class="sxs-lookup"><span data-stu-id="69e7b-132">To check the path and property name, use the action button that is immediately beside each property.</span></span> <span data-ttu-id="69e7b-133">Você pode clicar nesse botão de ação e escolher **Editar**.</span><span class="sxs-lookup"><span data-stu-id="69e7b-133">You can click this action button and select **Edit**.</span></span> <span data-ttu-id="69e7b-134">Isso mostrará o nome da propriedade e, logo acima dele, o namespace.</span><span class="sxs-lookup"><span data-stu-id="69e7b-134">This will show you the actual name of the property, and immediately above it, the namespace.</span></span>

![Ação/Editar](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture6_actionedit.png)

![Propriedade](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture7_viewproperty.png)

## <a name="multiple-input-files"></a><span data-ttu-id="69e7b-137">Vários arquivos de entrada</span><span class="sxs-lookup"><span data-stu-id="69e7b-137">Multiple input files</span></span>
<span data-ttu-id="69e7b-138">Cada tarefa enviada para o **Fluxo de Trabalho Premium do Codificador de Mídia** exige dois ativos:</span><span class="sxs-lookup"><span data-stu-id="69e7b-138">Each task that you submit to the **Media Encoder Premium Workflow** requires two assets:</span></span>

* <span data-ttu-id="69e7b-139">O primeiro é um *Ativo de Fluxo de Trabalho* que contém um arquivo de fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="69e7b-139">The first one is a *Workflow Asset* that contains a workflow file.</span></span> <span data-ttu-id="69e7b-140">Você pode criar arquivos de fluxo de trabalho usando o [Designer de Fluxo de Trabalho](media-services-workflow-designer.md).</span><span class="sxs-lookup"><span data-stu-id="69e7b-140">You can design workflow files by using the [Workflow Designer](media-services-workflow-designer.md).</span></span>
* <span data-ttu-id="69e7b-141">O segundo é um *Ativo de Mídia* que contém o(s) arquivo(s) de mídia que você deseja codificar.</span><span class="sxs-lookup"><span data-stu-id="69e7b-141">The second one is a *Media Asset* that contains the media file(s) that you want to encode.</span></span>

<span data-ttu-id="69e7b-142">Ao enviar vários arquivos de mídia para o codificador **Fluxo de Trabalho Premium do Codificador de Mídia** , as seguintes restrições se aplicam:</span><span class="sxs-lookup"><span data-stu-id="69e7b-142">When you're sending multiple media files to the **Media Encoder Premium Workflow** encoder, the following constraints apply:</span></span>

* <span data-ttu-id="69e7b-143">Todos os arquivos de mídia devem estar no mesmo *Ativo de Mídia*.</span><span class="sxs-lookup"><span data-stu-id="69e7b-143">All the media files must be in the same *Media Asset*.</span></span> <span data-ttu-id="69e7b-144">Não há suporte para o uso de vários Ativos de Mídia.</span><span class="sxs-lookup"><span data-stu-id="69e7b-144">Using multiple Media Assets is not supported.</span></span>
* <span data-ttu-id="69e7b-145">Você deve definir o arquivo primário neste Ativo de Mídia (de preferência, esse é o arquivo de vídeo principal que o codificador deverá processar).</span><span class="sxs-lookup"><span data-stu-id="69e7b-145">You must set the primary file in this Media Asset (ideally, this is the main video file that the encoder is asked to process).</span></span>
* <span data-ttu-id="69e7b-146">É necessário transmitir os dados de configuração que incluem o elemento **setRuntimeProperties** e/ou **transcodeSource** para o processador.</span><span class="sxs-lookup"><span data-stu-id="69e7b-146">It is necessary to pass configuration data that includes the **setRuntimeProperties** and/or **transcodeSource** element to the processor.</span></span>
  * <span data-ttu-id="69e7b-147">**setRuntimeProperties** é usado para substituir a propriedade de nome do arquivo ou outra propriedade nos componentes do fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="69e7b-147">**setRuntimeProperties** is used to override the filename property or another property in the components of the workflow.</span></span>
  * <span data-ttu-id="69e7b-148">**transcodeSource** é usado para especificar o conteúdo XML da Lista de Clipes.</span><span class="sxs-lookup"><span data-stu-id="69e7b-148">**transcodeSource** is used to specify the Clip List XML content.</span></span>

<span data-ttu-id="69e7b-149">Conexões no fluxo de trabalho:</span><span class="sxs-lookup"><span data-stu-id="69e7b-149">Connections in the workflow:</span></span>

* <span data-ttu-id="69e7b-150">Se você usar um ou vários componentes de Entrada do Arquivo de Mídia e pretende usar **setRuntimeProperties** para especificar o nome do arquivo, não conecte o pino do componente do arquivo primário a eles.</span><span class="sxs-lookup"><span data-stu-id="69e7b-150">If you use one or several Media File Input components and plan to use **setRuntimeProperties** to specify the file name, then do not connect the primary file component pin to them.</span></span> <span data-ttu-id="69e7b-151">Verifique se não há nenhuma conexão entre o objeto do arquivo primário e a(s) Entrada(s) do Arquivo de Mídia.</span><span class="sxs-lookup"><span data-stu-id="69e7b-151">Make sure that there is no connection between the primary file object and the Media File Input(s).</span></span>
* <span data-ttu-id="69e7b-152">Se você preferir usar o XML da Lista de Clipes e um componente da Fonte de Mídia, poderá conectar os dois juntos.</span><span class="sxs-lookup"><span data-stu-id="69e7b-152">If you prefer to use Clip List XML and one Media Source component, then you can connect both together.</span></span>

![Nenhuma conexão do Arquivo de Fonte Primária à Entrada do Arquivo de Mídia](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture0_nopin.png)

<span data-ttu-id="69e7b-154">*Não haverá conexão do arquivo primário com o(s) componente(s) de Entrada do Arquivo de Mídia se você usar setRuntimeProperties para definir a propriedade de nome do arquivo.*</span><span class="sxs-lookup"><span data-stu-id="69e7b-154">*There is no connection from the primary file to Media File Input component(s) if you use setRuntimeProperties to set the filename property.*</span></span>

![Conexão do XML da Lista de Clipes à Fonte da Lista de Clipes](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture1_pincliplist.png)

<span data-ttu-id="69e7b-156">*É possível conectar o XML da Lista de Clipes à Fonte de Mídia e usar transcodeSource.*</span><span class="sxs-lookup"><span data-stu-id="69e7b-156">*You can connect Clip List XML to Media Source and use transcodeSource.*</span></span>

### <a name="clip-list-xml-customization"></a><span data-ttu-id="69e7b-157">Personalização do XML da Lista de Clipes</span><span class="sxs-lookup"><span data-stu-id="69e7b-157">Clip List XML customization</span></span>
<span data-ttu-id="69e7b-158">É possível especificar o XML da Lista de Clipes no fluxo de trabalho, em tempo de execução, usando **transcodeSource** no XML da cadeia de caracteres de configuração.</span><span class="sxs-lookup"><span data-stu-id="69e7b-158">You can specify the Clip List XML in the workflow at runtime by using **transcodeSource** in the configuration string XML.</span></span> <span data-ttu-id="69e7b-159">Isso exige que o marcador do XML da Lista de Clipes esteja conectado ao componente de Fonte de Mídia no fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="69e7b-159">This requires the Clip List XML pin to be connected to the Media Source component in the workflow.</span></span>

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

<span data-ttu-id="69e7b-160">Se você deseja especificar /primarySourceFile para usar essa propriedade, para nomear os arquivos de saída usando 'Expressões', é recomendável transmitir o XML da Lista de Clipes como uma propriedade, *após* a propriedade /primarySourceFile, para evitar que a Lista de Clipes seja substituída pela configuração de /primarySourceFile.</span><span class="sxs-lookup"><span data-stu-id="69e7b-160">If you want to specify /primarySourceFile to use this property to name the output files by using 'Expressions', then we recommend passing the Clip List XML as a property *after* the /primarySourceFile property, to avoid having the Clip List be overridden by the /primarySourceFile setting.</span></span>

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

<span data-ttu-id="69e7b-161">Com outro corte preciso de quadro:</span><span class="sxs-lookup"><span data-stu-id="69e7b-161">With additional frame-accurate trimming:</span></span>

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

## <a name="example-1--overlay-an-image-on-top-of-the-video"></a><span data-ttu-id="69e7b-162">Exemplo 1: Sobrepor imagem sobre o vídeo</span><span class="sxs-lookup"><span data-stu-id="69e7b-162">Example 1 : Overlay an image on top of the video</span></span>

### <a name="presentation"></a><span data-ttu-id="69e7b-163">Apresentação</span><span class="sxs-lookup"><span data-stu-id="69e7b-163">Presentation</span></span>
<span data-ttu-id="69e7b-164">Considere um exemplo no qual você deseja sobrepor uma imagem de logotipo no vídeo de entrada durante a codificação do vídeo.</span><span class="sxs-lookup"><span data-stu-id="69e7b-164">Consider an example in which you want to overlay a logo image on the input video while the video is encoded.</span></span> <span data-ttu-id="69e7b-165">Neste exemplo, o vídeo de entrada chamado "Microsoft_HoloLens_Possibilities_816p24.mp4" e o logotipo é chamado "PNG".</span><span class="sxs-lookup"><span data-stu-id="69e7b-165">In this example, the input video is named "Microsoft_HoloLens_Possibilities_816p24.mp4" and the logo is named "logo.png".</span></span> <span data-ttu-id="69e7b-166">Você deve executar as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="69e7b-166">You should perform the following steps:</span></span>

* <span data-ttu-id="69e7b-167">Criar um Ativo de Fluxo de Trabalho com o arquivo de fluxo de trabalho (veja o exemplo a seguir).</span><span class="sxs-lookup"><span data-stu-id="69e7b-167">Create a Workflow Asset with the workflow file (see the following example).</span></span>
* <span data-ttu-id="69e7b-168">Criar um Ativo de Mídia, que contém dois arquivos: MyInputVideo.mp4 como o arquivo primário e MyLogo.png.</span><span class="sxs-lookup"><span data-stu-id="69e7b-168">Create a Media Asset, which contains two files: MyInputVideo.mp4 as the primary file and MyLogo.png.</span></span>
* <span data-ttu-id="69e7b-169">Enviar uma tarefa para o processador de mídia Fluxo de Trabalho Premium do Codificador de Mídia com os ativos de entrada indicados acima e especificar a cadeia de caracteres de configuração a seguir.</span><span class="sxs-lookup"><span data-stu-id="69e7b-169">Send a task to the Media Encoder Premium Workflow media processor with the above input assets and specify the following configuration string.</span></span>

<span data-ttu-id="69e7b-170">Configuração:</span><span class="sxs-lookup"><span data-stu-id="69e7b-170">Configuration:</span></span>

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

<span data-ttu-id="69e7b-171">No exemplo acima, o nome do arquivo de vídeo é enviado ao componente de Entrada do Arquivo de Mídia e à propriedade primarySourceFile.</span><span class="sxs-lookup"><span data-stu-id="69e7b-171">In the example above, the name of the video file is sent to the Media File Input component and the primarySourceFile property.</span></span> <span data-ttu-id="69e7b-172">O nome do arquivo de logotipo é enviado para outra Entrada do Arquivo de Mídia que está conectada ao componente de sobreposição de gráfico.</span><span class="sxs-lookup"><span data-stu-id="69e7b-172">The name of the logo file is sent to another Media File Input that is connected to the graphic overlay component.</span></span>

> [!NOTE]
> <span data-ttu-id="69e7b-173">O nome do arquivo de vídeo é enviado à propriedade primarySourceFile.</span><span class="sxs-lookup"><span data-stu-id="69e7b-173">The video file name is sent to the primarySourceFile property.</span></span> <span data-ttu-id="69e7b-174">A razão disso é para que essa propriedade seja usada no fluxo de trabalho na criação do nome do arquivo de saída correto usando Expressões, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="69e7b-174">The reason for this is to use this property in the workflow for building the correct output file name using Expressions, for example.</span></span>

### <a name="step-by-step-workflow-creation"></a><span data-ttu-id="69e7b-175">Criação de fluxo de trabalho passo a passo</span><span class="sxs-lookup"><span data-stu-id="69e7b-175">Step-by-step workflow creation</span></span>
<span data-ttu-id="69e7b-176">Estas são as etapas para criar um fluxo de trabalho que usa dois arquivos como entrada: um vídeo e uma imagem.</span><span class="sxs-lookup"><span data-stu-id="69e7b-176">Here are the steps to create a workflow that takes two files as input: a video and an image.</span></span> <span data-ttu-id="69e7b-177">Isto fará a sobreposição da imagem na parte superior do vídeo.</span><span class="sxs-lookup"><span data-stu-id="69e7b-177">It will overlay the image on top of the video.</span></span>

<span data-ttu-id="69e7b-178">Abra o **Designer de Fluxo de Trabalho** e selecione **Arquivo** > **Novo Espaço de Trabalho** > **Transcodificar Esquema**.</span><span class="sxs-lookup"><span data-stu-id="69e7b-178">Open **Workflow Designer** and select **File** > **New Workspace** > **Transcode Blueprint**.</span></span>

<span data-ttu-id="69e7b-179">O novo fluxo de trabalho mostra três elementos:</span><span class="sxs-lookup"><span data-stu-id="69e7b-179">The new workflow shows three elements:</span></span>

* <span data-ttu-id="69e7b-180">Arquivo de Origem Principal</span><span class="sxs-lookup"><span data-stu-id="69e7b-180">Primary Source File</span></span>
* <span data-ttu-id="69e7b-181">XML da Lista de Clipes</span><span class="sxs-lookup"><span data-stu-id="69e7b-181">Clip List XML</span></span>
* <span data-ttu-id="69e7b-182">Arquivo/Ativo de Saída</span><span class="sxs-lookup"><span data-stu-id="69e7b-182">Output File/Asset</span></span>  

![Novo fluxo de trabalho de codificação](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture9_empty.png)

<span data-ttu-id="69e7b-184">*Novo fluxo de trabalho de codificação*</span><span class="sxs-lookup"><span data-stu-id="69e7b-184">*New Encoding Workflow*</span></span>

<span data-ttu-id="69e7b-185">Para aceitar o arquivo de mídia de entrada, comece adicionando um componente de Entrada do Arquivo de Mídia.</span><span class="sxs-lookup"><span data-stu-id="69e7b-185">In order to accept the input media file, start with adding a Media File Input component.</span></span> <span data-ttu-id="69e7b-186">Para adicionar um componente ao fluxo de trabalho, procure-o na caixa de pesquisa do Repositório e arraste a entrada desejada até o painel do designer.</span><span class="sxs-lookup"><span data-stu-id="69e7b-186">To add a component to the workflow, look for it in the Repository search box and drag the desired entry onto the designer pane.</span></span>

<span data-ttu-id="69e7b-187">Em seguida, adicione o arquivo de vídeo que será usado para criar o fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="69e7b-187">Next, add the video file to be used for designing your workflow.</span></span> <span data-ttu-id="69e7b-188">Para fazer isso, clique no painel da tela de fundo do Designer de Fluxo de Trabalho e procure a propriedade do Arquivo de Origem Primário no painel de propriedades do lado direito.</span><span class="sxs-lookup"><span data-stu-id="69e7b-188">To do so, click the background pane in Workflow Designer and look for the Primary Source File property on the right-hand property pane.</span></span> <span data-ttu-id="69e7b-189">Clique no ícone de pasta e selecione o arquivo de vídeo apropriado.</span><span class="sxs-lookup"><span data-stu-id="69e7b-189">Click the folder icon and select the appropriate video file.</span></span>

![Fonte de Arquivo Primário](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture10_primaryfile.png)

<span data-ttu-id="69e7b-191">*Fonte de Arquivo Primário*</span><span class="sxs-lookup"><span data-stu-id="69e7b-191">*Primary File Source*</span></span>

<span data-ttu-id="69e7b-192">Em seguida, especifique o arquivo de vídeo no componente de Entrada do Arquivo de Mídia.</span><span class="sxs-lookup"><span data-stu-id="69e7b-192">Next, specify the video file in the Media File Input component.</span></span>   

![Fonte de Entrada do Arquivo de Mídia](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture11_mediafileinput.png)

<span data-ttu-id="69e7b-194">*Fonte de Entrada do Arquivo de Mídia*</span><span class="sxs-lookup"><span data-stu-id="69e7b-194">*Media File Input Source*</span></span>

<span data-ttu-id="69e7b-195">Assim que isso for feito, o componente Entrada do Arquivo de Mídia inspecionará o arquivo e preencherá seus pinos de saída para refletir o arquivo inspecionado por ele.</span><span class="sxs-lookup"><span data-stu-id="69e7b-195">As soon as this is done, the Media File Input component will inspect the file and populate its output pins to reflect the file that it inspected.</span></span>

<span data-ttu-id="69e7b-196">A próxima etapa é adicionar um “Atualizador de Tipo de Dados de Vídeo” para especificar o espaço de cores de Rec.709.</span><span class="sxs-lookup"><span data-stu-id="69e7b-196">The next step is to add a "Video Data Type Updater" to specify the color space to Rec.709.</span></span> <span data-ttu-id="69e7b-197">Adicione um "Conversor de Formato de Vídeo" definido como tipo de Layout de Dados/Layout = Planar Configurável.</span><span class="sxs-lookup"><span data-stu-id="69e7b-197">Add a "Video Format Converter" that is set to Data Layout/Layout type = Configurable Planar.</span></span> <span data-ttu-id="69e7b-198">Isso converterá a transmissão de vídeo em um formato que pode ser usado como uma fonte do componente de sobreposição.</span><span class="sxs-lookup"><span data-stu-id="69e7b-198">This will convert the video stream to a format that can be taken as a source of the overlay component.</span></span>

![Atualizador de tipo de dados e conversor de formato de vídeo](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter.png)

<span data-ttu-id="69e7b-200">*Atualizador de tipo de dados e conversor de formato de vídeo*</span><span class="sxs-lookup"><span data-stu-id="69e7b-200">*Video Data Type Updater and Format Converter*</span></span>

![Tipo de layout = Planar Configurável](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter2.png)

<span data-ttu-id="69e7b-202">*O Tipo de layout é Planar Configurável*</span><span class="sxs-lookup"><span data-stu-id="69e7b-202">*Layout type is Configurable Planar*</span></span>

<span data-ttu-id="69e7b-203">Em seguida, adicione um componente de Sobreposição de Vídeo e conecte o marcador de vídeo (descompactado) ao marcador de vídeo (descompactado) da entrada do arquivo de mídia.</span><span class="sxs-lookup"><span data-stu-id="69e7b-203">Next, add a Video Overlay component and connect the (uncompressed) video pin to the (uncompressed) video pin of the media file input.</span></span>

<span data-ttu-id="69e7b-204">Adicione outra Entrada do Arquivo de Mídia (para carregar o arquivo de logotipo), clique nesse componente e renomeie-o para "Logotipo de Entrada do Arquivo de Mídia" e escolha uma imagem (um arquivo .png, por exemplo) na propriedade do arquivo.</span><span class="sxs-lookup"><span data-stu-id="69e7b-204">Add another Media File Input (to load the logo file), click on this component and rename it to "Media File Input Logo", and select an image (a .png file for example) in the file property.</span></span> <span data-ttu-id="69e7b-205">Conecte o marcador da imagem Descompactada ao marcador da imagem Descompactada da sobreposição.</span><span class="sxs-lookup"><span data-stu-id="69e7b-205">Connect the Uncompressed image pin to the Uncompressed image pin of the overlay.</span></span>

![Fonte de arquivo de imagem e componente de sobreposição](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture13_overlay.png)

<span data-ttu-id="69e7b-207">*Fonte de arquivo de imagem e componente de sobreposição*</span><span class="sxs-lookup"><span data-stu-id="69e7b-207">*Overlay component and image file source*</span></span>

<span data-ttu-id="69e7b-208">Se quiser modificar a posição do logotipo no vídeo (por exemplo, talvez você queira posicioná-lo a 10% do canto superior esquerdo do vídeo), desmarque a caixa de seleção "Entrada Manual".</span><span class="sxs-lookup"><span data-stu-id="69e7b-208">If you want to modify the position of the logo on the video (for example, you might want to position it at 10 percent off of the top left corner of the video), clear the "Manual Input" check box.</span></span> <span data-ttu-id="69e7b-209">É possível fazer isso porque você está usando uma Entrada do Arquivo de Mídia para fornecer o arquivo de logotipo ao componente de sobreposição.</span><span class="sxs-lookup"><span data-stu-id="69e7b-209">You can do this because you are using a Media File Input to provide the logo file to the overlay component.</span></span>

![Posição da sobreposição](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture14_overlay_position.png)

<span data-ttu-id="69e7b-211">*Posição da sobreposição*</span><span class="sxs-lookup"><span data-stu-id="69e7b-211">*Overlay position*</span></span>

<span data-ttu-id="69e7b-212">Para codificar a transmissão de vídeo para H.264, adicione os componentes do Codificador de Vídeo AVC e do codificador AAC à superfície do designer.</span><span class="sxs-lookup"><span data-stu-id="69e7b-212">To encode the video stream to H.264, add the AVC Video Encoder and AAC encoder components to the designer surface.</span></span> <span data-ttu-id="69e7b-213">Conecte os marcadores.</span><span class="sxs-lookup"><span data-stu-id="69e7b-213">Connect the pins.</span></span>
<span data-ttu-id="69e7b-214">Configure o codificador AAC e escolha Conversão de Formato de Áudio/Predefinição: 2.0 (L, R).</span><span class="sxs-lookup"><span data-stu-id="69e7b-214">Set up the AAC encoder and select Audio Format Conversion/Preset : 2.0 (L, R).</span></span>

![Codificadores de Áudio e Vídeo](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture15_encoders.png)

<span data-ttu-id="69e7b-216">*Codificadores de Áudio e Vídeo*</span><span class="sxs-lookup"><span data-stu-id="69e7b-216">*Audio and Video Encoders*</span></span>

<span data-ttu-id="69e7b-217">Agora, adicione os componentes **Multiplexador ISO Mpeg-4** e **Saída de Arquivo** e conecte os pinos, conforme mostrado.</span><span class="sxs-lookup"><span data-stu-id="69e7b-217">Now add the **ISO Mpeg-4 Multiplexer** and **File Output** components and connect the pins as shown.</span></span>

![Multiplexador MP4 e saída de arquivo](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture16_mp4output.png)

<span data-ttu-id="69e7b-219">*Multiplexador MP4 e saída de arquivo*</span><span class="sxs-lookup"><span data-stu-id="69e7b-219">*MP4 multiplexer and file output*</span></span>

<span data-ttu-id="69e7b-220">É necessário definir o nome do arquivo de saída.</span><span class="sxs-lookup"><span data-stu-id="69e7b-220">You need to set the name for the output file.</span></span> <span data-ttu-id="69e7b-221">Clique no componente **Saída de Arquivo** e edite a expressão do arquivo:</span><span class="sxs-lookup"><span data-stu-id="69e7b-221">Click the **File Output** component and edit the expression for the file:</span></span>

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_withoverlay.mp4

![Nome de saída do arquivo](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture17_filenameoutput.png)

<span data-ttu-id="69e7b-223">*Nome de saída do arquivo*</span><span class="sxs-lookup"><span data-stu-id="69e7b-223">*File output name*</span></span>

<span data-ttu-id="69e7b-224">Você pode executar o fluxo de trabalho localmente para verificar se ele é executado corretamente.</span><span class="sxs-lookup"><span data-stu-id="69e7b-224">You can run the workflow locally to check that it is running correctly.</span></span>

<span data-ttu-id="69e7b-225">Após a conclusão, você poderá executá-lo nos Serviços de Mídia do Azure.</span><span class="sxs-lookup"><span data-stu-id="69e7b-225">After it finishes, you can run it in Azure Media Services.</span></span>

<span data-ttu-id="69e7b-226">Primeiro, prepare um ativo nos Serviços de Mídia do Azure com dois arquivos: o arquivo de vídeo e o logotipo.</span><span class="sxs-lookup"><span data-stu-id="69e7b-226">First, prepare an asset in Azure Media Services with two files in it: the video file and the logo.</span></span> <span data-ttu-id="69e7b-227">Você pode fazer isso usando a API REST ou o .NET.</span><span class="sxs-lookup"><span data-stu-id="69e7b-227">You can do this by using the .NET or REST API.</span></span> <span data-ttu-id="69e7b-228">Também é possível fazer isso usando o portal do Azure ou o AMSE ( [Gerenciador dos Serviços de Mídia do Azure](https://github.com/Azure/Azure-Media-Services-Explorer) ).</span><span class="sxs-lookup"><span data-stu-id="69e7b-228">You can also do this by using the Azure portal or [Azure Media Services Explorer](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).</span></span>

<span data-ttu-id="69e7b-229">Este tutorial mostra como gerenciar ativos com o AMSE.</span><span class="sxs-lookup"><span data-stu-id="69e7b-229">This tutorial shows you how to manage assets with AMSE.</span></span> <span data-ttu-id="69e7b-230">Há duas maneiras de adicionar arquivos a um ativo:</span><span class="sxs-lookup"><span data-stu-id="69e7b-230">There are two ways to add files to an asset:</span></span>

* <span data-ttu-id="69e7b-231">Crie uma pasta local, copie os dois arquivos nela e arraste e solte a pasta na guia **Ativo** .</span><span class="sxs-lookup"><span data-stu-id="69e7b-231">Create a local folder, copy the two files in it, and drag and drop the folder to the **Asset** tab.</span></span>
* <span data-ttu-id="69e7b-232">Carregue o arquivo de vídeo como um ativo, exiba as informações do ativo, vá para a guia Arquivos e carregue um arquivo adicional (logotipo).</span><span class="sxs-lookup"><span data-stu-id="69e7b-232">Upload the video file as an asset, display the asset information, go to the files tab, and upload an additional file (logo).</span></span>

> [!NOTE]
> <span data-ttu-id="69e7b-233">Lembre-se de definir um arquivo primário no ativo (o arquivo de vídeo principal).</span><span class="sxs-lookup"><span data-stu-id="69e7b-233">Make sure to set a primary file in the asset (the main video file).</span></span>

![Arquivos de ativo no AMSE](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture18_assetinamse.png)

<span data-ttu-id="69e7b-235">*Arquivos de ativo no AMSE*</span><span class="sxs-lookup"><span data-stu-id="69e7b-235">*Asset files in AMSE*</span></span>

<span data-ttu-id="69e7b-236">Selecione o ativo e escolha codificá-lo com o Codificador Premium.</span><span class="sxs-lookup"><span data-stu-id="69e7b-236">Select the asset and choose to encode it with Premium Encoder.</span></span> <span data-ttu-id="69e7b-237">Carregue o fluxo de trabalho e selecione-o.</span><span class="sxs-lookup"><span data-stu-id="69e7b-237">Upload the workflow and select it.</span></span>

<span data-ttu-id="69e7b-238">Clique no botão para transmitir dados ao processador e adicione o seguinte XML para definir as propriedades de tempo de execução:</span><span class="sxs-lookup"><span data-stu-id="69e7b-238">Click the button to pass data to the processor, and add the following XML to set the runtime properties:</span></span>

![Codificador Premium no AMSE](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture19_amsepremium.png)

<span data-ttu-id="69e7b-240">*Codificador Premium no AMSE*</span><span class="sxs-lookup"><span data-stu-id="69e7b-240">*Premium Encoder in AMSE*</span></span>

<span data-ttu-id="69e7b-241">Em seguida, cole os dados de XML a seguir.</span><span class="sxs-lookup"><span data-stu-id="69e7b-241">Then, paste the following XML data.</span></span> <span data-ttu-id="69e7b-242">Você precisa especificar o nome do arquivo de vídeo para a Entrada do Arquivo de Mídia e para primarySourceFile.</span><span class="sxs-lookup"><span data-stu-id="69e7b-242">You need to specify the name of the video file for both the Media File Input and primarySourceFile.</span></span> <span data-ttu-id="69e7b-243">Especifique o nome do arquivo para o logotipo também.</span><span class="sxs-lookup"><span data-stu-id="69e7b-243">Specify the name of the file name for the logo too.</span></span>

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

<span data-ttu-id="69e7b-245">*setRuntimeProperties*</span><span class="sxs-lookup"><span data-stu-id="69e7b-245">*setRuntimeProperties*</span></span>

<span data-ttu-id="69e7b-246">Se você usar o SDK do .NET para criar e executar a tarefa, esses dados XML deverão ser transmitidos como a cadeia de caracteres de configuração.</span><span class="sxs-lookup"><span data-stu-id="69e7b-246">If you use the .NET SDK to create and run the task, this XML data has to be passed as the configuration string.</span></span>

```c#
public ITask AddNew(string taskName, IMediaProcessor mediaProcessor, string configuration, TaskOptions options);
```

<span data-ttu-id="69e7b-247">Após a conclusão do trabalho, o arquivo MP4 no ativo de saída exibirá a sobreposição!</span><span class="sxs-lookup"><span data-stu-id="69e7b-247">After the job is complete, the MP4 file in the output asset displays the overlay!</span></span>

![Sobreposição no vídeo](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture21_resultoverlay.png)

<span data-ttu-id="69e7b-249">*Sobreposição no vídeo*</span><span class="sxs-lookup"><span data-stu-id="69e7b-249">*Overlay on the video*</span></span>

<span data-ttu-id="69e7b-250">Você pode baixar o fluxo de trabalho de exemplo no [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).</span><span class="sxs-lookup"><span data-stu-id="69e7b-250">You can download the sample workflow from [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).</span></span>

## <a name="example-2--multiple-audio-language-encoding"></a><span data-ttu-id="69e7b-251">Exemplo 2: Codificação de vários idiomas de áudio</span><span class="sxs-lookup"><span data-stu-id="69e7b-251">Example 2 : Multiple audio language encoding</span></span>

<span data-ttu-id="69e7b-252">Um exemplo de fluxo de trabalho de codificação de vários idiomas de áudio está disponível em [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding).</span><span class="sxs-lookup"><span data-stu-id="69e7b-252">An example of multiple audio language encoding workfkow is available in [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding).</span></span>

<span data-ttu-id="69e7b-253">Esta pasta contém um fluxo de trabalho de exemplo que pode ser usado para codificar um arquivo MXF para um ativo de arquivos MP4 múltiplas com várias faixas de áudio.</span><span class="sxs-lookup"><span data-stu-id="69e7b-253">This folder contains a sample workflow which can be used to encode a MXF file to a multi MP4 files asset with multiple audio tracks.</span></span>

<span data-ttu-id="69e7b-254">Esse fluxo de trabalho assume que o arquivo MXF contém uma faixa de áudio; as faixas de áudio adicionais devem ser passadas como arquivos separados de áudios (WAV ou... MP4).</span><span class="sxs-lookup"><span data-stu-id="69e7b-254">This workflow assumes that the MXF file contains one audio track ; the additional audio tracks should be passed as seperate audio files (WAV or MP4...).</span></span>

<span data-ttu-id="69e7b-255">Para codificar, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="69e7b-255">To encode, please follow these steps:</span></span>

* <span data-ttu-id="69e7b-256">Crie um ativo dos serviços de mídia com o arquivo MXF e os arquivos de áudio (arquivos de áudio de 0 a 18).</span><span class="sxs-lookup"><span data-stu-id="69e7b-256">Create a Media Services asset with the MXF file and the Audio files (0 to 18 audio files).</span></span>
* <span data-ttu-id="69e7b-257">Certifique-se de que o arquivo MXF é definido como um arquivo primário.</span><span class="sxs-lookup"><span data-stu-id="69e7b-257">Make sure that the MXF file is set as a primary file.</span></span>
* <span data-ttu-id="69e7b-258">Crie um trabalho e uma tarefa usando o processador do codificador de fluxo de trabalho Premium.</span><span class="sxs-lookup"><span data-stu-id="69e7b-258">Create a job and a task using the Premium Workflow Encoder processor.</span></span> <span data-ttu-id="69e7b-259">Use o fluxo de trabalho fornecido (MultiMP4-1080p-19audio-v1.workflow).</span><span class="sxs-lookup"><span data-stu-id="69e7b-259">Use the workflow provided (MultiMP4-1080p-19audio-v1.workflow).</span></span>
* <span data-ttu-id="69e7b-260">Passar os dados setruntime.xml para a tarefa (se você usar o Gerenciador de serviços de mídia do Azure, use o botão "passar dados xml para o fluxo de trabalho").</span><span class="sxs-lookup"><span data-stu-id="69e7b-260">Pass the setruntime.xml data to the task (if you use Azure Media Services Explorer, use the “pass xml data to the workflow” button).</span></span>
  * <span data-ttu-id="69e7b-261">Atualize os dados XML para especificar as marcas de idiomas e nomes de arquivo correto.</span><span class="sxs-lookup"><span data-stu-id="69e7b-261">Please update the XML data to specify the correct file names and languages tags.</span></span>
  * <span data-ttu-id="69e7b-262">O fluxo de trabalho tem componentes de áudio denominado 1 áudio para áudio 18.</span><span class="sxs-lookup"><span data-stu-id="69e7b-262">The workflow has audio components named Audio 1 to Audio 18.</span></span>
  * <span data-ttu-id="69e7b-263">RFC5646 há suporte para a marca de idioma.</span><span class="sxs-lookup"><span data-stu-id="69e7b-263">RFC5646 is supported for the language tag.</span></span>

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

* <span data-ttu-id="69e7b-264">O ativo codificado conterá várias faixas de áudio de idiomas e essas faixas devem ser selecionáveis no Azure Media Player.</span><span class="sxs-lookup"><span data-stu-id="69e7b-264">The encoded asset will contain multi language audio tracks and these tracks should be selectable in Azure Media Player.</span></span>

## <a name="see-also"></a><span data-ttu-id="69e7b-265">Consulte também</span><span class="sxs-lookup"><span data-stu-id="69e7b-265">See also</span></span>
* [<span data-ttu-id="69e7b-266">Apresentando a codificação Premium nos Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="69e7b-266">Introducing Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)
* [<span data-ttu-id="69e7b-267">How to use Premium Encoding in Azure Media Services (Como usar a codificação Premium nos Serviços de Mídia do Azure)</span><span class="sxs-lookup"><span data-stu-id="69e7b-267">How to use Premium Encoding in Azure Media Services</span></span>](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)
* [<span data-ttu-id="69e7b-268">Encoding on-demand content with Azure Media Services (Codificação do conteúdo sob demanda com os Serviços de Mídia do Azure)</span><span class="sxs-lookup"><span data-stu-id="69e7b-268">Encoding on-demand content with Azure Media Services</span></span>](media-services-encode-asset.md#media-encoder-premium-workflow)
* [<span data-ttu-id="69e7b-269">Codecs e formatos de fluxo de trabalho do Media Encoder Premium</span><span class="sxs-lookup"><span data-stu-id="69e7b-269">Media Encoder Premium Workflow formats and codecs</span></span>](media-services-premium-workflow-encoder-formats.md)
* [<span data-ttu-id="69e7b-270">Exemplos de arquivos de fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="69e7b-270">Sample workflow files</span></span>](https://github.com/AzureMediaServicesSamples/Encoding-Presets/tree/master/VoD/MediaEncoderPremiumWorkfows)
* [<span data-ttu-id="69e7b-271">Ferramenta do Explorador dos Serviços de Mídia do Azure</span><span class="sxs-lookup"><span data-stu-id="69e7b-271">Azure Media Services Explorer tool</span></span>](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a><span data-ttu-id="69e7b-272">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="69e7b-272">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="69e7b-273">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="69e7b-273">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
