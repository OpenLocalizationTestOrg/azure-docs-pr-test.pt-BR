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
# <a name="using-multiple-input-files-and-component-properties-with-premium-encoder"></a>Usando vários arquivos de entrada e propriedades do componente com o Codificador Premium
## <a name="overview"></a>Visão geral
Há cenários nos quais propriedades do componente toocustomize, talvez seja necessário especificar o conteúdo XML de lista do clipe ou enviar vários arquivos de entrada quando você enviar uma tarefa com hello **o fluxo de trabalho do Media Encoder Premium** processador de mídia. Alguns exemplos incluem:

* Sobreposição de texto em vídeo e definir o valor de texto de saudação (por exemplo, a saudação data atual) em tempo de execução para cada vídeo de entrada.
* Personalizando Olá Clip lista XML (toospecify da fonte de um ou vários arquivos, com ou sem cortar, etc.).
* Sobreposição de uma imagem de logotipo no vídeo de entrada hello enquanto Olá vídeo é codificado.
* Vários idiomas de áudio codificação.

Olá toolet **o fluxo de trabalho do Media Encoder Premium** saber que você está alterando algumas propriedades no fluxo de trabalho hello quando você cria tarefa hello ou enviar vários arquivos de entrada, se você tiver toouse uma cadeia de caracteres de configuração que contém  **setRuntimeProperties** e/ou **transcodeSource**. Este tópico explica como toouse-los.

## <a name="configuration-string-syntax"></a>Sintaxe da cadeia de caracteres de configuração
Olá configuração cadeia de caracteres tooset em Olá codificação tarefa usa um documento XML que tem esta aparência:

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

a seguir Hello é código Olá c# que lê a configuração Olá XML de um arquivo, atualize-o com hello filename correto de vídeo e transmite toohello tarefas em um trabalho:

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

## <a name="customizing-component-properties"></a>Personalizando as propriedades do componente
### <a name="property-with-a-simple-value"></a>Propriedade com um valor simples
Em alguns casos, é útil toocustomize uma propriedade do componente junto com o arquivo de fluxo de trabalho de saudação que será toobe executada pelo fluxo de trabalho Premium de codificador de mídia.

Suponha que você criou um fluxo de trabalho texto sobreposições em seus vídeos e texto de saudação (por exemplo, a saudação data atual) deve toobe conjunto em tempo de execução. Você pode fazer isso enviando Olá texto toobe defina como o novo valor para a propriedade de texto de saudação do componente de sobreposição de saudação de saudação do hello tarefas de codificação. Você pode usar esse mecanismo toochange outras propriedades de um componente no fluxo de trabalho de saudação (como Olá posição ou cor da sobreposição de hello, taxa de bits de saudação do codificador Olá AVC, etc.).

**setRuntimeProperties** é uma propriedade em componentes de saudação do fluxo de trabalho de saudação de toooverride usado.

Exemplo:

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

### <a name="property-with-an-xml-value"></a>Propriedade com um valor XML
encapsular tooset uma propriedade que espera um valor XML, usando `<![CDATA[ and ]]>`.

Exemplo:

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
> Certifique-se de não tooput um carro logo após retornar `<![CDATA[`.

### <a name="propertypath-value"></a>Valor de propertyPath
Nos exemplos anteriores do hello, Olá propertyPath foi "/ arquivo de mídia de entrada/filename" ou "/ inactiveTimeout" ou "clipListXml".
Isso é, em geral, nome de saudação do componente de saudação e nome de saudação da propriedade hello. Olá caminho pode ter mais ou menos níveis, como "/ primarySourceFile" (porque é propriedade de saudação na raiz de saudação do fluxo de trabalho Olá) ou "/ vídeo/opacidade de sobreposição processamento/gráfico" (porque Olá sobreposição está em um grupo).    

toocheck Olá caminho e nome da propriedade, use Olá ação botão imediatamente ao lado de cada propriedade. Você pode clicar nesse botão de ação e escolher **Editar**. Isso mostrará você Olá real de nome da propriedade hello e imediatamente acima dela, Olá namespace.

![Ação/Editar](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture6_actionedit.png)

![Propriedade](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture7_viewproperty.png)

## <a name="multiple-input-files"></a>Vários arquivos de entrada
Cada tarefa que você enviar toohello **o fluxo de trabalho do Media Encoder Premium** requer dois ativos:

* Olá primeiro um é um *fluxo de trabalho ativo* que contém um arquivo de fluxo de trabalho. Você pode criar arquivos de fluxo de trabalho usando Olá [Designer de fluxo de trabalho](media-services-workflow-designer.md).
* Olá segundo é um *ativo de mídia* que contém Olá arquivos de mídia que você deseja tooencode.

Quando você estiver enviando várias toohello de arquivos de mídia **o fluxo de trabalho do Media Encoder Premium** aplica do codificador, Olá restrições a seguir:

* Olá de todas as mídias Olá arquivos devem estar no mesmo *ativo de mídia*. Não há suporte para o uso de vários Ativos de Mídia.
* Você deve definir o arquivo primário Olá nesse ativo de mídia (Idealmente, isso é hello principal arquivo de vídeo que Olá codificador é solicitado tooprocess).
* É necessário toopass dados de configuração que inclui a saudação **setRuntimeProperties** e/ou **transcodeSource** processador do elemento toohello.
  * **setRuntimeProperties** é propriedade de nome de arquivo hello toooverride usado ou outra propriedade em componentes de saudação do fluxo de trabalho de saudação.
  * **transcodeSource** é usado toospecify hello conteúdo XML de lista do clipe.

Conexões no fluxo de trabalho hello:

* Se você usar um ou vários componentes de entrada de arquivo de mídia e planejar toouse **setRuntimeProperties** toospecify Olá nome de arquivo, em seguida, não conecte Olá toothem de pin de componente de arquivo primário. Certifique-se de que não há nenhuma conexão entre o objeto de arquivo primário hello e hello entradas do arquivo de mídia.
* Se você preferir toouse Clip lista XML e um componente de origem de mídia, em seguida, você pode conectar os dois juntos.

![Nenhuma conexão de arquivo de origem primário tooMedia arquivo de entrada](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture0_nopin.png)

*Não há nenhuma conexão de arquivo primário de saudação tooMedia componente (s) de entrada do arquivo se você usar a propriedade de nome de arquivo setRuntimeProperties tooset hello.*

![Conexão do XML de lista de clipe tooClip fonte da lista](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture1_pincliplist.png)

*Você pode conectar-se o XML de lista de clipe tooMedia fonte e usar transcodeSource.*

### <a name="clip-list-xml-customization"></a>Personalização do XML da Lista de Clipes
Você pode especificar Olá Clip lista XML no fluxo de trabalho de saudação em tempo de execução usando **transcodeSource** na configuração de saudação de cadeia de caracteres XML. Isso requer Olá Clip lista XML pin toobe conectado toohello componente de origem de mídia no fluxo de trabalho de saudação.

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

Se você deseja toospecify /primarySourceFile toouse esta saída de hello propriedade tooname arquivos usando 'Expressões', é recomendável passar Olá Clip lista XML como uma propriedade *depois* propriedade /primarySourceFile a saudação, tooavoid Lista de clipe ter Olá ser substituído definindo /primarySourceFile hello.

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

Com outro corte preciso de quadro:

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

## <a name="example-1--overlay-an-image-on-top-of-hello-video"></a>Exemplo 1: Sobreposição de uma imagem na parte superior Olá vídeo

### <a name="presentation"></a>Apresentação
Considere um exemplo no qual você deseja toooverlay uma imagem de logotipo no vídeo de entrada hello enquanto Olá vídeo é codificado. Neste exemplo, o vídeo de entrada hello será denominado "Microsoft_HoloLens_Possibilities_816p24.mp4" e o logotipo de saudação é "logo.png". Você deve executar Olá etapas a seguir:

* Criar um ativo de fluxo de trabalho com o arquivo de fluxo de trabalho da saudação (consulte Olá exemplo a seguir).
* Criar um ativo de mídia, que contém dois arquivos: MyInputVideo.mp4 como Olá arquivo primário e MyLogo.png.
* Enviar um toohello tarefa mídia de fluxo de trabalho Premium de codificador de mídia ativos de entrada do processador com hello acima e especificar Olá cadeia de caracteres de configuração a seguir.

Configuração:

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

No exemplo hello acima, o nome de Olá Olá do arquivo de vídeo seja enviado toohello entrada do arquivo de mídia componente e Olá primarySourceFile propriedade. nome de Olá Olá do arquivo de logotipo é enviado tooanother entrada de arquivo de mídia que é conectado toohello sobreposição gráfico componente.

> [!NOTE]
> nome do arquivo de vídeo de saudação é enviada toohello primarySourceFile propriedade. Olá razão para isso é toouse essa propriedade no fluxo de trabalho Olá para a criação de nome de arquivo de saída correta hello usando expressões, por exemplo.

### <a name="step-by-step-workflow-creation"></a>Criação de fluxo de trabalho passo a passo
Aqui está Olá etapas toocreate um fluxo de trabalho que usa dois arquivos como entrada: um vídeo e uma imagem. Ele irá sobrepor imagem Olá sobre Olá vídeo.

Abra o **Designer de Fluxo de Trabalho** e selecione **Arquivo** > **Novo Espaço de Trabalho** > **Transcodificar Esquema**.

novo fluxo de trabalho de saudação mostra três elementos:

* Arquivo de Origem Principal
* XML da Lista de Clipes
* Arquivo/Ativo de Saída  

![Novo fluxo de trabalho de codificação](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture9_empty.png)

*Novo fluxo de trabalho de codificação*

No arquivo de mídia de entrada do pedido tooaccept hello, comece a adicionar um componente de entrada de arquivo de mídia. tooadd um fluxo de trabalho toohello de componente, procure-a na caixa de pesquisa de repositório hello e arrastar entrada hello desejado no painel de designer do hello.

Em seguida, adicione Olá toobe de arquivo de vídeo usada para criar o fluxo de trabalho. toodo assim, clique em Painel de plano de fundo Olá no Designer de fluxo de trabalho e procure a propriedade de arquivo de origem primário Olá no painel de propriedade direito hello. Clique Olá ícone da pasta e selecione o arquivo de vídeo apropriado hello.

![Fonte de Arquivo Primário](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture10_primaryfile.png)

*Fonte de Arquivo Primário*

Em seguida, especifique o arquivo de vídeo Olá no componente de entrada de arquivo de mídia hello.   

![Fonte de Entrada do Arquivo de Mídia](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture11_mediafileinput.png)

*Fonte de Entrada do Arquivo de Mídia*

Assim que isso for feito, o componente de entrada de arquivo de mídia Olá inspecionar o arquivo hello e preencher sua saída pins tooreflect Olá arquivo que ele inspecionado.

Olá próxima etapa é tooadd tooRec.709 de espaço de cor um "Atualizador de tipo de dados de vídeo" toospecify hello. Adicionar um "vídeo formato conversor" que é definir o tipo de Layout/Layout tooData = configurável Planar. Isso converterá o formato de tooa de fluxo de vídeo Olá que pode ser executado como uma origem de componente de sobreposição de saudação.

![Atualizador de tipo de dados e conversor de formato de vídeo](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter.png)

*Atualizador de tipo de dados e conversor de formato de vídeo*

![Tipo de layout = Planar Configurável](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture12_formatconverter2.png)

*O Tipo de layout é Planar Configurável*

Em seguida, adicione um componente de sobreposição de vídeo e conecte Olá pin de vídeo (descompactado) toohello (descompactado) vídeo pin de entrada de arquivo de mídia hello.

Adicionar outra entrada de arquivo de mídia (arquivo de logotipo do tooload Olá), clique neste componente e renomeá-lo muito "Logotipo de entrada de arquivo de mídia" e selecione uma imagem (um arquivo. png por exemplo) na propriedade do arquivo hello. Conecte-se Olá imagem descompactada pinos toohello imagem descompactada pinos da sobreposição de saudação.

![Fonte de arquivo de imagem e componente de sobreposição](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture13_overlay.png)

*Fonte de arquivo de imagem e componente de sobreposição*

Se você deseja toomodify Olá posição do logotipo Olá no vídeo de saudação (por exemplo, você talvez queira tooposition-lo em 10 por cento da parte superior da saudação canto esquerdo do vídeo Olá), desmarque caixa de seleção "Entrada Manual" hello. Você pode fazer isso porque você está usando um entrada de arquivo de mídia tooprovide Olá logotipo arquivo toohello sobreposição componente.

![Posição da sobreposição](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture14_overlay_position.png)

*Posição da sobreposição*

tooencode Olá tooH.264 do fluxo de vídeo, adicione hello AVC codificador de vídeo e a superfície do designer de toohello AAC codificador componentes. Conecte-se os pins hello.
Configure o codificador AAC hello e selecione conversão de formato de áudio/predefinição: 2.0 (L, R).

![Codificadores de Áudio e Vídeo](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture15_encoders.png)

*Codificadores de Áudio e Vídeo*

Agora adicione Olá **ISO Mpeg-4 multiplexador** e **arquivo de saída** componentes e conecte-se pins hello, conforme mostrado.

![Multiplexador MP4 e saída de arquivo](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture16_mp4output.png)

*Multiplexador MP4 e saída de arquivo*

Você precisará tooset Olá nome para o arquivo de saída hello. Clique em Olá **arquivo de saída** componente e Editar expressão Olá para o arquivo hello:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_withoverlay.mp4

![Nome de saída do arquivo](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture17_filenameoutput.png)

*Nome de saída do arquivo*

Você pode executar o fluxo de trabalho Olá localmente toocheck que está sendo executado corretamente.

Após a conclusão, você poderá executá-lo nos Serviços de Mídia do Azure.

Primeiro, preparar um ativo no Azure Media Services com dois arquivos: o arquivo de vídeo hello e logotipo hello. Você pode fazer isso usando a API Olá .NET ou REST. Você também pode fazer isso usando o portal do Azure de saudação ou [Gerenciador de serviços de mídia do Azure](https://github.com/Azure/Azure-Media-Services-Explorer) (AMSE).

Este tutorial mostra como ativos de toomanage com AMSE. Há dois ativo tooan tooadd arquivos de formas:

* Criar uma pasta local, copiar Olá dois arquivos e arrastar e soltar Olá pasta toohello **ativo** guia.
* Carregar o arquivo de vídeo hello como um ativo, exibir informações sobre os ativos hello, acesse a guia arquivos de toohello e carregar um arquivo adicional (logotipo).

> [!NOTE]
> Verifique se tooset um arquivo primário no ativo hello (Olá principal arquivo de vídeo).

![Arquivos de ativo no AMSE](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture18_assetinamse.png)

*Arquivos de ativo no AMSE*

Selecione Olá ativo e escolha tooencode com o codificador Premium. Carregar o fluxo de trabalho hello e selecioná-lo.

Clique em processador de toohello Olá botão toopass dados e, em seguida, adicione Olá propriedades de tempo de execução XML tooset Olá a seguir:

![Codificador Premium no AMSE](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture19_amsepremium.png)

*Codificador Premium no AMSE*

Em seguida, cole Olá dados XML a seguir. Você precisa toospecify nome de Olá Olá do arquivo de vídeo para Olá entrada de arquivo de mídia e primarySourceFile. Especifique o nome de saudação do nome de arquivo de saudação do logotipo Olá muito.

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

*setRuntimeProperties*

Se você usar Olá .NET SDK toocreate e executa tarefas de hello, esses dados XML tem toobe passado como cadeia de caracteres de configuração de saudação.

```c#
public ITask AddNew(string taskName, IMediaProcessor mediaProcessor, string configuration, TaskOptions options);
```

Após a conclusão do trabalho hello, arquivo hello MP4 Olá saída ativo exibe sobreposição Olá!

![Sobreposição de vídeo de saudação](./media/media-services-media-encoder-premium-workflow-multiplefilesinput/capture21_resultoverlay.png)

*Sobreposição de vídeo de saudação*

Você pode baixar o fluxo de trabalho de exemplo de saudação do [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/).

## <a name="example-2--multiple-audio-language-encoding"></a>Exemplo 2: Codificação de vários idiomas de áudio

Um exemplo de fluxo de trabalho de codificação de vários idiomas de áudio está disponível em [GitHub](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/MultilanguageAudioEncoding).

Esta pasta contém um fluxo de trabalho de exemplo que pode ser usado tooencode um ativo de arquivos MXF arquivos tooa várias MP4 com várias faixas de áudio.

Este fluxo de trabalho supõe que esse arquivo MXF Olá contém uma faixa de áudio; faixas de áudio adicionais Olá devem ser passadas como arquivos de áudio separados (WAV ou MP4...).

tooencode, siga estas etapas:

* Crie um ativo de serviços de mídia com hello e Olá MXF arquivos de áudio (0 too18 arquivos de áudio).
* Verifique se o que arquivo hello MXF é definido como um arquivo primário.
* Crie um trabalho e uma tarefa usando o processador de codificador de fluxo de trabalho Premium Olá. Use o fluxo de trabalho de saudação fornecido (MultiMP4-1080p-19audio-v1.workflow).
* Passe a tarefa de toohello Olá setruntime.xml dados (se você usar o Gerenciador de serviços de mídia do Azure, use hello "passar o fluxo de trabalho de toohello de dados xml" botão).
  * Atualize Olá dados toospecify Olá arquivo correto nomes e linguagens de marcas XML.
  * fluxo de trabalho Olá tem componentes de áudio denominados 1 áudio tooAudio 18.
  * RFC5646 há suporte para a marca de idioma hello.

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

* ativo Olá codificado conterá várias faixas de áudio de linguagem e essas faixas devem ser selecionáveis no Azure Media Player.

## <a name="see-also"></a>Consulte também
* [Apresentando a codificação Premium nos Serviços de Mídia do Azure](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)
* [Como toouse Premium de codificação no Azure Media Services](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)
* [Encoding on-demand content with Azure Media Services (Codificação do conteúdo sob demanda com os Serviços de Mídia do Azure)](media-services-encode-asset.md#media-encoder-premium-workflow)
* [Codecs e formatos de fluxo de trabalho do Media Encoder Premium](media-services-premium-workflow-encoder-formats.md)
* [Exemplos de arquivos de fluxo de trabalho](https://github.com/AzureMediaServicesSamples/Encoding-Presets/tree/master/VoD/MediaEncoderPremiumWorkfows)
* [Ferramenta do Explorador dos Serviços de Mídia do Azure](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
