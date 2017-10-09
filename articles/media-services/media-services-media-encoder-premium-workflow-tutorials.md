---
title: "tutoriais de fluxo de trabalho Premium de codificador de mídia aaaAvanced"
description: "Este documento contém instruções passo a passo que mostram como tooperform avançado tarefas de fluxo de trabalho Premium de codificador de mídia e também como toocreate fluxos de trabalho complexos com o Designer de fluxo de trabalho."
services: media-services
documentationcenter: 
author: xstof
manager: cfowler
editor: 
ms.assetid: 1ba52865-b4a8-4ca0-ac96-920d55b9d15b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: christoc;xpouyat;juliako
ms.openlocfilehash: 641bd1be3bd795b5e138fa7ffdf299ff6710904e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-media-encoder-premium-workflow-tutorials"></a>Tutoriais avançados do fluxo de trabalho do Codificador de Mídia Premium
## <a name="overview"></a>Visão geral
Este documento contém instruções passo a passo que mostram como fluxos de trabalho toocustomize com **Designer de fluxo de trabalho**. Você pode encontrar os arquivos de fluxo de trabalho real Olá [aqui](https://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows/PremiumEncoderWorkflowSamples).  

## <a name="toc"></a>SUMÁRIO
Olá seguintes tópicos é abordado:

* [Codificando MXF em um MP4 de taxa de bits única](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)
  * [Iniciando um novo fluxo de trabalho](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_start_new)
  * [Usando Olá entrada de arquivo de mídia](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_file_input)
  * [Inspecionando fluxos de mídia](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_streams)
  * [Adicionando um codificador de vídeo para geração de arquivo .MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_file_generation)
  * [Fluxo de áudio Olá codificação](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio)
  * [Multiplexando fluxos de áudio e de vídeo em um contêiner MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_audio_and_fideo)
  * [Gravar o arquivo MP4 de saudação](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_writing_mp4)
  * [Criar um ativo de serviços de mídia do arquivo de saída Olá](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_asset_from_output)
  * [Saudação de teste terminar o fluxo de trabalho localmente](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_test)
* [Codificando MXF em MP4s com várias taxas bits - empacotamento dinâmico habilitado](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging)
  * [Adicionando uma ou mais saídas MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_more_outputs)
  * [Configurar nomes de saída do arquivo hello](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_conf_output_names)
  * [Adicionando uma Trilha de Áudio separada](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_audio_tracks)
  * [Adicionando hello. Arquivo SMIL ISM](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging_ism_file)
* [Codificando MXF em MP4 com várias taxas de bit - plano gráfico aprimorado](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4)
  * [Tooenhance de visão geral do fluxo de trabalho](#workflow-overview-to-enhance)
  * [Convenções de nomenclatura do arquivo](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_file_naming)
  * [Propriedades de componente na raiz de fluxo de trabalho de saudação de publicação](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_publishing)
  * [Faça com que os nomes de arquivo de saída gerados dependam dos valores de propriedade publicados](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to__multibitrate_MP4_output_files)
* [Adicionando a saída de MP4 toomultibitrate miniaturas](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4)
  * [Miniaturas de tooadd de visão geral do fluxo de trabalho para](#workflow-overview-to-add-thumbnails-to)
  * [Adicionando codificação JPG](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4__with_jpg)
  * [Lidando com a conversão de espaço de cor](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_color_space)
  * [Miniaturas de saudação de gravação](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_writing_thumbnails)
  * [Detectando erros em um fluxo de trabalho](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_errors)
  * [Fluxo de trabalho concluído](media-services-media-encoder-premium-workflow-tutorials.md#thumbnails_to__multibitrate_MP4_finish)
* [Corte baseado em tempo da saída MP4 com várias taxas de bits](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim)
  * [Toostart de visão geral do fluxo de trabalho adicionando restrições para](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_start)
  * [Usando Olá filtro de fluxo](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_use_stream_trimmer)
  * [Fluxo de trabalho concluído](media-services-media-encoder-premium-workflow-tutorials.md#time_based_trim_finish)
* [Apresentando o hello componente script](media-services-media-encoder-premium-workflow-tutorials.md#scripting)
  * [Criando scripts em um fluxo de trabalho: hello world](media-services-media-encoder-premium-workflow-tutorials.md#scripting_hello_world)
* [Corte baseado em quadro da saída MP4 com várias taxas de bits](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim)
  * [Plano gráfico toostart visão geral sobre a adição de corte para](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_start)
  * [Usando Olá Clip lista XML](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clip_list)
  * [Modificando a lista de saudação do clipe de um componente script](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_modify_clip_list)
  * [Adicionando uma propriedade de conveniência ClippingEnabled](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim_clippingenabled_prop)

## <a id="MXF_to_MP4"></a>Codificando MXF em um MP4 de taxa de bits única
Neste passo a passo, criaremos um arquivo MP4 de taxa de bits única com áudio codificado em AAC-HE a partir de um arquivo de entrada .MXF.

### <a id="MXF_to_MP4_start_new"></a>Iniciando um novo fluxo de trabalho
Abra o Designer de Fluxo de Trabalho e selecione "Arquivo" - "Novo Espaço de Trabalho" - "Transcodificar Esquema"

Olá novo fluxo de trabalho mostrará 3 elementos:

* Arquivo de Origem Principal
* XML da Lista de Clipes
* Arquivo/Ativo de Saída  

![Novo fluxo de trabalho de codificação](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-transcode-blueprint.png)

*Novo fluxo de trabalho de codificação*

### <a id="MXF_to_MP4_with_file_input"></a>Usando Olá entrada de arquivo de mídia
Em ordem tooaccept nosso arquivo de mídia de entrada, uma começa com a adição de um componente de entrada de arquivo de mídia. tooadd um fluxo de trabalho toohello de componente, procure-a na caixa de pesquisa de repositório hello e arrastar entrada hello desejado no painel de designer do hello. Faça isso para Olá entrada de arquivo de mídia e conecte Olá arquivo fonte primário componente toohello Filename pino de entrada de saudação entrada de arquivo de mídia.

![Entrada do Arquivo de Mídia conectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-input.png)

*Entrada do Arquivo de Mídia conectado*

Para que possa fazer muito mais do que, primeiro precisaremos designer de fluxo de trabalho toohello tooindicate o arquivo de exemplo gostaríamos toouse toodesign nosso fluxo de trabalho. toodo assim, clique em segundo plano do painel designer hello e procure a propriedade de arquivo de origem primário Olá no painel de propriedade direito hello. Clique no ícone de pasta hello e selecione Olá desejado arquivo tootest Olá fluxo de trabalho. Assim que isso for feito, o componente de entrada de arquivo de mídia Olá inspecionar o arquivo hello e preencher sua saída pins tooreflect Olá arquivo, que ele inspecionado.

![Entrada do Arquivo de Mídia preenchida](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-populated-media-file-input.png)

*Entrada do Arquivo de Mídia preenchida*

Enquanto isso Especifica com qual entrada que gostaríamos toowork com, ela não informa ainda em que a saída de hello codificado deve ir para. Semelhante Olá toohow principal arquivo de origem foi configurado, configure Olá propriedade da variável de pasta de saída, logo abaixo.

![Propriedades de Entrada e Saída configuradas](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configured-io-properties.png)

*Propriedades de Entrada e Saída configuradas*

### <a id="MXF_to_MP4_streams"></a>Inspecionando fluxos de mídia
Geralmente é preferível tooknow fluxo Olá aparência desse flui pelo fluxo de trabalho de saudação. tooinspect um fluxo em qualquer ponto no fluxo de trabalho hello, basta clicar uma saída ou entrada de pin em qualquer um dos componentes de saudação. Nesse caso, tente clicar em Olá pino de saída de vídeo descompactado da nossa entrada de arquivo de mídia. Uma caixa de diálogo será aberta que permite que o vídeo de saída de hello tooinspect.

![Inspecionando pino de saída de vídeo descompactado Olá](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-inspecting-uncompressed-video-output.png)

*Inspecionando pino de saída de vídeo descompactado Olá*

Em nosso caso, ele nos informa, por exemplo, que estamos lidando com uma entrada de 1920 x 1080 a 24 quadros por segundo em uma amostragem de 4:2:2 de um vídeo de quase 2 minutos.

### <a id="MXF_to_MP4_file_generation"></a>Adicionando um codificador de vídeo para geração de arquivo .MP4
Observe que, agora, um pino de saída Vídeo Descompactado e vários pinos de saída Áudio Descompactados estão disponíveis para uso em nossa Entrada do Arquivo de Mídia. Em ordem tooencode Olá vídeo de entrada, precisamos de um componente de codificação - nesse caso para gerar. Arquivos MP4.

tooencode Olá tooH.264 do fluxo de vídeo, adicione a superfície do designer de toohello Olá AVC codificador de vídeo componente. Esse componente recebe um fluxo de vídeo descompactado como entrada e fornece um fluxo de vídeo compactado AVC em seu pino de saída.

![Codificador AVC desconectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-avc-encoder.png)

*Codificador AVC desconectado*

Suas propriedades determinam como exatamente Olá codificação acontece. Vamos dar uma olhada em algumas Olá configurações mais importantes:

* Largura de saída e a altura de saída: esses determinam a resolução de saudação do vídeo Olá codificado. Em nosso caso, usaremos 640 x 360
* Taxa de quadros: quando toopassthrough conjunto será apenas adotar a taxa de quadros de origem Olá, é possível toooverride esta aqui. Observe que essa conversão de taxa de quadros não tem compensação de movimento.
* Nível e perfil: eles determinam perfil Olá AVC e nível. tooconveniently obter mais informações sobre Olá diferentes níveis e os perfis, clique em ícone de ponto de interrogação Olá no componente de codificador de vídeo AVC hello e página de ajuda de saudação mostrará mais detalhes sobre cada um dos níveis de saudação. Em nosso exemplo, vamos Escolher perfil principal no nível 3.2 (padrão de saudação).
* Modo de Controle de Taxa e Taxa de bits (kbps): em nosso cenário, optamos por uma saída de taxa de bits constante (CBR) de 1200 kbps
* Formato de vídeo: trata-se Olá VUI (informações de uso do vídeo) que é gravado no fluxo de h. 264 hello (informações sobre o que pode ser usado por uma exibição de saudação do decodificador tooenhance, mas não essencial toocorrectly decodificar):
* NTSC (normalmente para os Estados Unidos ou o Japão, usando 30 qps)
* PAL (normalmente para a Europa, usando 25 qps)
* Modo de Tamanho de GOP: configuraremos o Tamanho de GOP Fixo para nossos objetivos com um Intervalo de Chave de dois segundos com GOPs Fechados. Isso assegura a compatibilidade com hello que fornece serviços de mídia do empacotamento dinâmico do Azure.

toofeed nossa codificador AVC, conectar pino de saída de vídeo descompactado saudação do hello entrada de arquivo de mídia componente toohello vídeo descompactado pino de entrada do codificador Olá AVC.

![Codificador AVC conectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-avc-encoder.png)

*Codificador Principal de AVC conectado*

### <a id="MXF_to_MP4_audio"></a>Fluxo de áudio Olá codificação
Neste ponto, podemos ter codificado vídeo mas fluxo de áudio descompactados original Olá ainda precisa toobe compactado. Para isso vamos com AAC codificação por Olá componente AAC codificador (Dolby). Adicione-o fluxo de trabalho toohello.

![Codificador AVC desconectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-unconnected-aac-encoder.png)

*Codificador AAC desconectado*

Agora há uma incompatibilidade: há apenas um único descompactado áudio entrado pin de saudação AAC codificador enquanto mais do que provavelmente Olá entrada de arquivo de mídia terá dois descompactados disponíveis de fluxo de áudio: uma para Olá deixado canal de áudio e outro para Olá Certo. (Se você estiver lidando com som surround, serão seis canais). Portanto, não é possível toodirectly conecte áudio Olá da fonte de entrada de arquivo de mídia Olá codificador de áudio Olá AAC. componente AAC Hello espera um fluxo de áudio chamado "intercalado": um único fluxo que tem ambos Olá esquerda e hello canais corretos intercalados entre si. Já sabemos do nosso arquivo de mídia de origem que faixas de áudio em qual posição na origem hello, podemos gerar esse fluxo de áudio Intercalado com hello corretamente recebem posições locutor para a esquerda e direita.

Primeiro um desejará toogenerated um fluxo intercalado de canais de áudio de origem Olá necessário. componente de Interleaver de fluxo de áudio de saudação tratará isso para nós. Adicioná-lo toohello de fluxo de trabalho e se conectar a saídas de áudio de saudação do hello entrada de arquivo de mídia para ele.

![Intercalador do fluxo de áudio conectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-audio-stream-interleaver.png)

*Intercalador do fluxo de áudio conectado*

Agora que temos um fluxo de áudio intercalado, ainda não especificamos onde tooassign Olá esquerdo ou direito dos alto-falantes posições à. Em ordem toospecify isso, podemos aproveitar Olá locutor cedente de posição.

![Adicionando um Atribuidor de Posição do Alto-falante](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-speaker-position-assigner.png)

*Adicionando um Atribuidor de Posição do Alto-falante*

Configurar Olá locutor posição cedente para uso com um fluxo de entrada estéreo por meio de um filtro de predefinição de codificador de "Custom" e Olá canal predefinido chamado "2.0 (L, R)". (Isso atribuirá Olá locutor esquerdo posição toochannel 1 e Olá locutor certa posição toochannel 2.)

Conecte a saída de saudação do toohello entrada locutor posição cedente Olá Olá AAC codificador. Em seguida, conte-Olá AAC codificador toowork com um "2.0 (L, R)" canal predefinidos, para que ele saiba toodeal com áudio estéreo como entrada.

### <a id="MXF_to_MP4_audio_and_fideo"></a>Multiplexando fluxos de áudio e de vídeo em um contêiner MP4
Com base em nosso fluxo de vídeo codificado em AVC e em nosso fluxo de áudio codificado em AAC, podemos capturar ambos em um contêiner .MP4. processo de saudação de combinação de fluxos diferentes em uma única é chamado de "multiplexação" (ou "muxing"). Nesse caso, está intercalação hello e Olá vídeo fluxos de áudio em uma única coerente. Pacote de MP4. componente de saudação que coordena isso para um. Olá multiplexador ISO MPEG-4 é chamado de contêiner MP4. Adicione uma superfície de designer toohello e conecte Olá AVC codificador de vídeo e entradas de tooits AAC codificador hello.

![Multiplexador MPEG4 conectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-mpeg4-multiplexer.png)

*Multiplexador MPEG4 conectado*

### <a id="MXF_to_MP4_writing_mp4"></a>Gravar o arquivo MP4 de saudação
Ao gravar um arquivo de saída, o componente de saída de arquivo hello é usado. Podemos pode se conectar esta saída toohello de saudação multiplexador ISO MPEG-4 para que a saída é gravada toodisk. toodo, conectar Olá contêiner (MPEG-4) pin toohello gravação entrado pino de saída de hello arquivo de saída.

![Saída do arquivo conectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connected-file-output.png)

*Saída do arquivo conectado*

Olá nome do arquivo que será usado é determinado pelo Olá propriedade de arquivo. Enquanto essa propriedade pode ser codificado tooa valor, um provavelmente desejarão tooset-lo por meio de uma expressão em vez disso.

fluxo de trabalho toohave Olá determinar automaticamente a saída de hello arquivo de propriedade de nome de uma expressão, clique em Olá botão próximo toohello nome de arquivo (ícone de pasta próximo toohello). No hello menu suspenso e selecione "Expressão". Isso abrirá o editor de expressão hello. Limpe o conteúdo de saudação do editor de saudação primeiro.

![Editor de expressão vazio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-empty-expression-editor.png)

*Editor de expressão vazio*

editor de expressão Olá permite tooenter qualquer valor literal, combinado com uma ou mais variáveis. As variáveis começam com um sinal de cifrão. Conforme você pressionar a tecla de $ de hello, editor de saudação mostrará uma caixa suspensa com uma opção de variáveis disponíveis. Em nosso caso, usaremos uma combinação de variável de diretório de saída de hello e variável de nome de arquivo base de entrada hello:

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}.MP4

![Editor de expressão preenchido](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-expression-editor.png)

*Editor de expressão preenchido*

> [!NOTE]
> Em ordem toosee ver um arquivo de saída do seu trabalho de codificação no Azure, você deve fornecer um valor no editor de expressão hello.
>
>

Quando você confirmar expressão Olá atingindo okey, janela de propriedade Olá visualizará toowhat valor Olá arquivo propriedade resolve neste momento.

![Diretório de saída de resolução da Expressão do Arquivo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-file-expression-resolves-output-dir.png)

*Diretório de saída de resolução da Expressão do Arquivo*

### <a id="MXF_to_MP4_asset_from_output"></a>Criar um ativo de serviços de mídia do arquivo de saída Olá
Enquanto estamos foram gravadas, um arquivo de saída de MP4, ainda precisamos tooindicate este arquivo pertence toohello ativo quais serviços de mídia irá gerar como resultado da execução deste fluxo de trabalho de saída. toothis final, o nó de arquivo/ativo de saída Olá na tela de fluxo de trabalho de saudação é usado. Todos os arquivos de entrada para esse nó se tornará parte do hello resultante do Azure Media Services ativo.

Conecte-se Olá saída de arquivo componente toohello ativo/arquivo de saída componente toofinish Olá fluxo de trabalho.

![Fluxo de trabalho concluído](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow.png)

*Fluxo de trabalho concluído*

### <a id="MXF_to_MP4_test"></a>Saudação de teste terminar o fluxo de trabalho localmente
tootest Olá fluxo de trabalho localmente, pressione o botão de reprodução de Olá na barra de ferramentas de saudação na parte superior da saudação. Quando o fluxo de trabalho Olá terminar a execução, inspecione saída Olá gerada na pasta de saída de saudação configurada. Você verá Olá terminar o arquivo de saída de MP4 que foi codificado Olá MXF entrada do arquivo de origem.

## <a id="MXF_to_MP4_with_dyn_packaging"></a>Codificação do MXF em MP4 - empacotamento dinâmico com várias taxas bits habilitado
Neste passo a passo, criaremos um conjunto de arquivos MP4 com várias taxas de bits e áudio codificado em AAC a partir de um único arquivo de entrada .MXF.

Quando uma saída de ativo de múltiplas taxas de bits for desejada para uso em combinação com recursos de empacotamento dinâmico Olá oferecidos pelo Azure Media Services, vários arquivos MP4 com alinhamento GOP de cada uma taxa de bits diferente e a resolução precisará toobe gerado. Assim, Olá toodo [MXF codificação em uma taxa de bits única MP4](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4) passo a passo fornece um bom ponto de partida.

![Como iniciar o fluxo de trabalho](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow.png)

*Como iniciar o fluxo de trabalho*

### <a id="MXF_to_MP4_with_dyn_packaging_more_outputs"></a>Adicionando uma ou mais saídas MP4
Cada arquivo MP4 em nosso ativo resultante dos Serviços de Mídia do Azure oferecerá suporte a uma taxa de bits e resolução diferentes. Vamos adicionar um ou mais MP4 saída arquivos toohello fluxo de trabalho.

toomake-se de que temos todos os codificadores de vídeos criados com Olá mesmas configurações, é mais conveniente tooduplicate Olá codificador de vídeo AVC já existente e configure outra combinação de resolução e taxa de bits (vamos adicionar um 960 x 540 25 quadros por segundo 2,5 Mbps). codificador existente do tooduplicate hello, cópia colá-lo na superfície de designer hello.

Conecte-se Olá pino de saída de vídeo descompactado da saudação entrada de arquivo de mídia em nosso novo componente AVC.

![Segundo codificador AVC conectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-avc-encoder-connected.png)

*Segundo codificador AVC conectado*

Agora adapte configuração Olá para toooutput de codificador AVC nosso novo 960 x 540 a 2,5 Mbps. (Use as propriedades "Largura de saída", "Altura de saída" e "Taxa de bits (kbps)" para isso).

Considerando que desejamos toouse ativo resultante do hello junto com o empacotamento dinâmico do Azure Media Services, Olá ponto de extremidade de streaming necessidades toobe capaz de gerar desses arquivos MP4 fragmentos HLS/fragmentado MP4/DASH que são exatamente alinhado tooeach outro de forma que os clientes que estiver alternando entre diferentes taxas de bits obtém uma único smooth contínua áudio e vídeo experiência. toomake que acontecem, precisamos tooensure que, nas propriedades de saudação do codificadores AVC está definido Olá tamanho GOP ("grupo de imagens") para os dois arquivos MP4 too2 segundos, que podem ser feitos por:

* Definindo o tamanho de GOP Olá GOP tamanho modo tooFixed e
* segundos de tootwo de intervalo de quadro chave Hello.
* também definir Olá GOP IDR controle tooClosed GOP tooensure GOP todos está aguardando em seus próprios sem dependências

toomake nossa toounderstand conveniente de fluxo de trabalho, renomear o codificador de AVC primeiro Olá muito "codificador de vídeo AVC 640x360 1200kbps" e Olá codificador do segundo AVC "codificador de vídeo AVC 960 x 540 kbps 2500".

Agora, adicione um segundo Multiplexador ISO MPEG-4 e uma segunda Saída de arquivo. Conecte Olá multiplexador toohello novo AVC codificador e verifique se que a saída é direcionada para Olá saída de arquivo. Também se conectar Olá AAC codificador de áudio saída toohello nova entrada da multiplexador. Olá saída de arquivo por sua vez pode ser conectado toohello ativo/arquivo de saída nó tooadd-toohello ativo de serviços de mídia que será criado.

![Segundo Muxer e Saída do arquivo conectado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-second-muxer-file-output-connected.png)

*Segundo Muxer e Saída do arquivo conectado*

Para compatibilidade com o empacotamento dinâmico dos serviços de mídia do Azure, configure a contagem de tooGOP de modo de bloco de saudação do multiplexador ou duração e defina Olá GOPs por too1 parte. (Isso deve ser o padrão de hello.)

![Modos de parte do muxer](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-muxer-chunk-modes.png)

*Modos de parte do muxer*

Observação: talvez você queira toorepeat esse processo para qualquer taxa de bits e resolução de combinações de toohave adicionado toohello saída de ativo.

### <a id="MXF_to_MP4_with_dyn_packaging_conf_output_names"></a>Configurar nomes de saída do arquivo hello
Temos mais de um ativo de saída de arquivo único adicionado toohello. Isso fornece uma saudação-se de necessidade toomake nomes de arquivos para cada Olá saída arquivos são diferentes uns dos outros e talvez até mesmo se aplica uma convenção de nomenclatura de arquivo portanto fica claro saudação do nome de arquivo que você está lidando com.

Nomenclatura de arquivos de saída pode ser controlado por meio de expressões no designer de saudação. Abrir o painel de propriedade Olá para um dos componentes de saída de arquivo hello e abrir editor de expressão de saudação do hello propriedade de arquivo. Nosso primeiro arquivo de saída foi configurado por meio de saudação expressão a seguir (consulte o tutorial Olá para indo de [taxa de bits única saída MP4 do MXF tooa](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4)):

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}.MP4

Isso significa que nossa filename é determinada por duas variáveis: Olá saída toowrite directory no e hello nome base do arquivo de origem. antiga Olá é exposta como uma propriedade na raiz de fluxo de trabalho hello e Olá esta última é determinada pelo arquivo de entrada hello. Observe que esse diretório de saída Olá é usada para teste local. Essa propriedade será substituída pelo mecanismo de fluxo de trabalho hello quando o fluxo de trabalho de saudação é executado pelo processador de mídia com base em nuvem Olá nos serviços de mídia do Azure.
toogive ambos os arquivos de nossa saída uma saída consistente de nomenclatura, alteração Olá primeiro arquivo nomenclatura expressão para:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

e o segundo Olá para:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_960x540_2.MP4

Execução de um teste intermediário toomake-se de que ambos os arquivos de saída de MP4 gerados corretamente.

### <a id="MXF_to_MP4_with_dyn_packaging_audio_tracks"></a>Adicionando uma Trilha de Áudio separada
Como veremos mais tarde quando geramos uma toogo de arquivo. ISM com os arquivos de saída de MP4, nós também exigirá um arquivo MP4 somente de áudio como faixa de áudio Olá para nosso streaming adaptável. toocreate esse arquivo, adicione um fluxo de trabalho do muxer adicionais toohello (ISO-MPEG-4 multiplexador) e conecte-se o pino de saída do codificador do hello AAC com seu pin de entrada para acompanhar 1.

![Muxer de áudio adicionado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-added.png)

*Muxer de áudio adicionado*

Criar um fluxo de saída do arquivo de saída componente toooutput Olá terceiro de saudação muxer e configure a expressão de nomenclatura de arquivo hello como:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_128kbps_audio.MP4

![Criação de Saída do arquivo pelo muxer de áudio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-audio-muxer-creating-file-output.png)

*Criação de Saída do arquivo pelo muxer de áudio*

### <a id="MXF_to_MP4_with_dyn_packaging_ism_file"></a>Adicionando hello. Arquivo SMIL ISM
Para toowork de empacotamento dinâmico Olá em combinação com os dois MP4 arquivos (e Olá somente de áudio MP4) em nosso ativo do Media Services, também é necessário um arquivo de manifesto (também chamado de arquivo "SMIL": linguagem de integração de multimídia sincronizada). Esse arquivo indica tooAzure Media Services quais arquivos MP4 estão disponíveis para empacotamento dinâmico e que esses tooconsider para streaming de áudio hello. Um arquivo de manifesto típico para um conjunto de MP4s com um único fluxo de áudio tem a seguinte aparência:

    <?xml version="1.0" encoding="utf-8" standalone="yes"?>
    <smil xmlns="http://www.w3.org/2001/SMIL20/Language">
      <head>
        <meta name="formats" content="mp4" />
      </head>
      <body>
        <switch>
          <video src="H264_1900kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_1300kbps_AAC_und_ch2_96kbps.mp4" />
          <video src="H264_900kbps_AAC_und_ch2_96kbps.mp4" />
          <audio src="AAC_ch2_96kbps.mp4" title="AAC_und_ch2_96kbps" />
        </switch>
      </body>
    </smil>

arquivo. ISM de saudação contém dentro de uma instrução switch, tooeach uma referência de arquivos individuais de vídeo de MP4 hello e além de arquivo de áudio toothose também uma (ou mais) faz referência a tooan MP4 que contém apenas o áudio hello.

Gerar arquivo de manifesto de saudação para nosso conjunto de MP4 pode ser feito por meio de um componente chamado hello "AMS manifesto gravador". toouse, arraste-o para a superfície de saudação e conecte-se o hello "De gravação concluído" pinos de saída de hello três arquivos de saída componentes toohello AMS gravador de manifesto de entrada. Certifique-se de que tooconnect Olá saída Olá AMS manifesto gravador toohello ativo/arquivo de saída.

Assim como acontece com os outros componentes de saída de arquivo, configure o nome de saída de arquivo hello. ISM com uma expressão:

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_manifest.ism

Nosso fluxo de trabalho concluído é semelhante a saudação abaixo:

![Fluxo de trabalho MP4 toomultibitrate de terminar de MXF](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-mxf-to-multibitrate-mp4-workflow.png)

*Fluxo de trabalho MP4 toomultibitrate de terminar de MXF*

## <a id="MXF_to__multibitrate_MP4"></a>Codificando MXF em MP4 com várias taxas de bit - plano gráfico aprimorado
Em Olá [passo a passo de fluxo de trabalho anterior](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging) que vimos como um único ativo de entrada MXF pode ser convertido em um ativo de saída com arquivos MP4 com múltiplas taxas de bits, um arquivo MP4 somente de áudio e um arquivo de manifesto para uso em conjunto com a mídia do Azure Serviços de empacotamento dinâmico.

Este passo a passo mostrará como alguns aspectos de saudação podem ser aprimorados e torna mais conveniente.

### <a id="MXF_to_multibitrate_MP4_overview"></a>Tooenhance de visão geral do fluxo de trabalho
![Multibitrate MP4 tooenhance de fluxo de trabalho](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-enhance.png)

*Multibitrate MP4 tooenhance de fluxo de trabalho*

### <a id="MXF_to__multibitrate_MP4_file_naming"></a>Convenções de nomenclatura do arquivo
Fluxo de trabalho anterior Olá especificamos uma expressão simples como base Olá para gerar nomes de arquivo de saída. Temos alguns duplicação embora: todos os componentes de arquivo de saída individuais Olá Olá essa expressão especificada.

Por exemplo, nosso componente de saída de arquivo para o arquivo de vídeo primeiro Olá é configurado com esta expressão:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_640x360_1.MP4

Tempo para Olá segunda saída de vídeo, temos uma expressão como:

    ${ROOT_outputWriteDirectory}\\${ROOT_sourceFileBaseName}_960x540_2.MP4

Não seria mais claro, menos propenso a erros e mais conveniente se pudéssemos remover algumas essas duplicações e tornar as coisas mais configuráveis? Felizmente, podemos: recursos de expressão do designer de saudação em combinação com propriedades personalizadas da saudação capacidade toocreate em nosso raiz de fluxo de trabalho fornece uma camada adicional de conveniência.

Vamos supor que estamos será unidade de configuração de nome de arquivo do hello taxas de bits de arquivos MP4 individuais de saudação. Essas taxas de bits, irá visar tooconfigure em um centro colocar (em raiz de saudação do nosso gráfico), de onde eles serão acessada geração de nome de arquivo de tooconfigure e a unidade. toodo isso, vamos começar com a publicação de propriedade de taxa de bits Olá de ambos os raiz de toohello AVC codificadores de nosso fluxo de trabalho para que ele se tornará acessível de ambos os raiz hello, bem como codificadores Olá AVC. (Mesmo se for exibido em dois pontos diferentes, haverá apenas um valor subjacente).

### <a id="MXF_to__multibitrate_MP4_publishing"></a>Propriedades de componente na raiz de fluxo de trabalho de saudação de publicação
Abra o codificador de AVC primeiro hello, vá toohello propriedade de taxa de bits (kbps) e na lista suspensa de saudação selecione publicar.

![Propriedade de taxa de bits Olá publicação](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-bitrate-property.png)

*Propriedade de taxa de bits Olá publicação*

Configurar Olá publicar diálogo toopublish toohello raiz do nosso gráfico de fluxo de trabalho, com um nome publicado de "video1bitrate" e um nome de exibição legível de "Taxa de bits do vídeo 1". Configure um nome do grupo personalizado chamado "Taxas de Bits de Streaming" e toque em Publicar.

![Propriedade de taxa de bits Olá publicação](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-bitrate-property.png)

*Caixa de diálogo de publicação para a propriedade de taxa de bits*

Olá repetição mesmo para a propriedade de taxa de bits de saudação do hello segundo codificador AVC e nomeie-o "video2bitrate" com um nome de exibição de "Taxa de bits do vídeo 2", no hello mesma personalizado de grupo "Streaming taxas de bits".

Se nós agora inspecionar as propriedades de fluxo de trabalho raiz hello, veremos nosso grupo personalizado com hello aparecem duas propriedades publicadas. Ambos são refletir o valor de saudação de seu respectiva AVC codificador de taxa de bits.

![Propriedades de taxa de bits publicadas na raiz do fluxo de trabalho](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-bitrate-props-on-workflow-root.png)

Sempre que desejamos tooaccess essas propriedades de código ou de uma expressão, podemos fazer isso como este:

* no código embutido de um componente logo abaixo raiz Olá: node.getPropertyAsString('.. / video1bitrate', null)
* em uma expressão: ${ROOT_video1bitrate}

Vamos concluir o grupo de "Streaming taxas de bits" hello publicando nosso faixa de áudio de taxa de bits nele também. Em Propriedades Olá Olá AAC codificador, procure a configuração de taxa de bits de saudação e selecione publicar na Olá suspensa próxima tooit. Publicar toohello raiz do gráfico de saudação com nome "audio1bitrate" e exibir o nome "Taxa de bits de áudio 1" em nosso grupo personalizado "Streaming taxas de bits".

![Caixa de diálogo de publicação para a taxa de bits de áudio](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publishing-dialog-for-audio-bitrate.png)

*Caixa de diálogo de publicação para a taxa de bits de áudio*

![Propriedades de áudio e vídeos resultantes na raiz](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-resulting-video-and-audio-props-on-root.png)

*Propriedades de áudio e vídeos resultantes na raiz*

Observe que a alteração de qualquer um desses três valores também configura novamente e alterações Olá componentes do respectivos Olá são vinculados com valores (e, quando publicados do).

### <a id="MXF_to__multibitrate_MP4_output_files"></a>Faça com que os nomes de arquivo de saída gerados dependam dos valores de propriedade publicados
Em vez de codificar os nomes de arquivo gerado, podemos agora alterar nossa expressão de nome de arquivo em cada um dos toorely de componentes de saída de arquivo hello nas propriedades de taxa de bits Olá que acabou de ser publicados na raiz do gráfico de saudação. Começando com nossa primeira saída de arquivo, localizar a propriedade de arquivo hello e editar a expressão hello como este:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video1bitrate}kbps.MP4

parâmetros diferentes de saudação nesta expressão podem ser acessados e inseridos ao atingir o sinal de cifrão Olá teclado Olá enquanto estiver na janela de expressão de saudação. Um dos parâmetros disponíveis Olá é nossa propriedade video1bitrate que são publicados anteriormente.

![Acessando parâmetros dentro de uma expressão](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-accessing-parameters-within-an-expression.png)

*Acessando parâmetros dentro de uma expressão*

Olá mesmo para saída de arquivo hello para nosso vídeo segundo:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_video2bitrate}kbps.MP4

e para a saída de arquivo somente de áudio hello:

    ${ROOT_outputWriteDirectory}\${ROOT_sourceFileBaseName}_${ROOT_audio1bitrate}bps_audio.MP4

Se alterarmos agora Olá a taxa de bits para qualquer um dos arquivos de áudio ou vídeo hello, codificador do respectivos Olá será reconfigurado e convenção de nomes de arquivos com base em taxas de bits hello será cumprida automático.

## <a id="thumbnails_to__multibitrate_MP4"></a>Adicionando a saída de MP4 toomultibitrate miniaturas
A partir de um fluxo de trabalho que gera [uma saída como MP4 de uma entrada de MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), podemos agora verá em Adicionar saída de toohello de miniaturas.

### <a id="thumbnails_to__multibitrate_MP4_overview"></a>Miniaturas de tooadd de visão geral do fluxo de trabalho para
![Multibitrate MP4 toostart de fluxo de trabalho do](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-multibitrate-mp4-workflow-to-start-from.png)

*Multibitrate MP4 toostart de fluxo de trabalho do*

### <a id="thumbnails_to__multibitrate_MP4__with_jpg"></a>Adicionando codificação JPG
núcleo de saudação do nosso geração de miniaturas serão componente de codificador de JPG hello, toooutput capaz de arquivos. JPG.

![Codificador de JPG](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-jpg-encoder.png)

*Codificador de JPG*

No entanto diretamente não foi possível conectar nosso fluxo de vídeo descompactado da saudação entrada de arquivo de mídia no codificador JPG hello. Em vez disso, ele espera toobe entregue quadros individuais. Isso, podemos fazer através do componente de entrada do quadro de vídeo hello.

![Conectar-se um codificador JPG quadro portão toohello](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-frame-gate-to-jpg-encoder.png)

*Conectar-se um codificador JPG quadro portão toohello*

Portão de quadro Hello quando cada tantos segundos ou quadros permite toopass um quadro de vídeo. tempo de intervalo e hello de saudação deslocamento com que isso ocorre é configurável nas propriedades de saudação.

![Propriedades do Portão de Quadro do Vídeo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-video-frame-gate-properties.png)

*Propriedades do Portão de Quadro do Vídeo*

Vamos criar uma miniatura de cada minuto, definindo Olá modo tooTime (segundos) e Olá too60 de intervalo.

### <a id="thumbnails_to__multibitrate_MP4_color_space"></a>Lidando com a conversão de espaço de cor
Embora seria parecer lógico pins de vídeo descompactado do portão de quadro hello e hello entrada de arquivo de mídia agora podem ser conectados, obteremos um aviso se fazer isso.

![Erro no espaço de cor de entrada](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-input-color-space-error.png)

*Erro no espaço de cor de entrada*

Isso ocorre porque a forma Olá no qual cor informações são representadas em nosso original bruto descompactado fluxo de vídeo, provenientes de nosso MXF é diferente do que Olá codificador de JPG está esperando. Mais especificamente, uma chamada "espaço de cores" de "RGB" ou "Cinza" é esperado tooflow no. Isso significa que o fluxo de vídeo de entrada do que Olá vídeo quadro portão precisará toohave uma conversão aplicada primeiro sobre o seu espaço de cor.

Arraste a saudação de fluxo de trabalho Olá conversor de espaço de cor - Intel e conectá-lo tooour portão de quadro.

![Conexão de um Conversor de Espaço de Cor](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-connect-color-space-convertor.png)

*Conexão de um Conversor de Espaço de Cor*

Na janela de propriedades hello, escolha entrada hello BGR 24 Olá predefinição de lista.

### <a id="thumbnails_to__multibitrate_MP4_writing_thumbnails"></a>Miniaturas de saudação de gravação
Diferente do nosso vídeo de MP4, Olá codificador de JPG componente resultará em mais de um arquivo. Em ordem toodeal com isso, um componente de cena pesquisa JPG arquivo gravador pode ser usado: ele se miniaturas JPG entradas hello e gravar, cada nome de arquivo que está sendo o sufixo por um número diferente. (número de saudação normalmente indicando o número de saudação de segundos/unidades no fluxo de saudação que Olá miniatura foi obtido de.)

![Olá apresentando o gravador de arquivo JPG cena pesquisa](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer.png)

*Olá apresentando o gravador de arquivo JPG cena pesquisa*

Configurar a propriedade do caminho da pasta de saída de hello com expressão Olá: ${ROOT_outputWriteDirectory}

e Olá a propriedade com o prefixo de nome de arquivo:

    ${ROOT_sourceFileBaseName}_thumb_

prefixo de saudação determinará como arquivos em miniatura Olá estão sendo nomeados. Eles serão ser sufixo com um número indicando Olá posição da miniatura no fluxo de saudação.

![Propriedades do Gravador de arquivo JPG de Pesquisa de cena](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scene-search-jpg-file-writer-properties.png)

*Propriedades do Gravador de arquivo JPG de Pesquisa de cena*

Conecte-se nó do hello o gravador de arquivo JPG cena pesquisa toohello ativo/arquivo de saída.

### <a id="thumbnails_to__multibitrate_MP4_errors"></a>Detectando erros em um fluxo de trabalho
Conecte-se a entrada Olá Olá cor espaço conversor toohello bruto descompactados saída de vídeo. Agora, execute um teste local para o fluxo de trabalho de saudação. Há um fluxo de trabalho de Olá boas chances de repente parará a execução e indicar com um contorno vermelho no componente de saudação que encontrou um erro:

![Erro no Conversor de Espaço de Cor](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error.png)

*Erro no Conversor de Espaço de Cor*

Clique em ícone de "E" hello pouco vermelha no canto superior direito de saudação do hello conversor de espaço de cor componente toosee o que é o motivo de saudação Falha na tentativa de codificação de saudação.

![Caixa de diálogo do erro no Conversor de Espaço de Cor](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-color-space-converter-error-dialog.png)

*Caixa de diálogo do erro no Conversor de Espaço de Cor*

Na verdade, como você pode ver, Olá entrada espaço de cor padrão para o conversor de espaço de cor Olá tem rec601 toobe para nossa conversão solicitada de YUV tooRGB. Aparentemente, nosso fluxo não indica que é rec601. (Rec 601 é um padrão de codificação de sinais de vídeo analógicos entrelaçados no formato de vídeo digital. Ele especifica uma região ativa cobrindo 720 amostras de luminosidade e 360 exemplos de crominância por linha. cor Olá codificação sistema é conhecido como YCbCr 4:2:2.)

toofix isso, será indicamos nos metadados de saudação do nosso fluxo que estamos lidando com conteúdo rec601. toodo, então, vamos usar um componente do atualizador de tipo de dados de vídeo, colocaremos entre nossos bruto fonte e hello cor espaço componente de conversão. Esse atualizador de tipo de dados permite atualização manual de saudação de certos dados vídeos propriedades de tipo. Configurá-lo tooindicate um padrão de espaço de cor de "Rec 601". Isso fará com que fluxo de Olá Olá atualizador de tipo de dados de vídeo tootag com espaço de cor hello "Rec 601" se não houver nenhum espaço de cor foi definido. (Ela não substituirá todos os metadados existentes, a menos que a caixa de seleção de substituição de saudação foi verificada.)

![Atualizando o espaço de cor padrão em Olá atualizador de tipo de dados](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-update-color-space-standard-on-data-type.png)

*Atualizando o espaço de cor padrão em Olá atualizador de tipo de dados*

### <a id="thumbnails_to__multibitrate_MP4_finish"></a>Fluxo de trabalho concluído
Agora que nossa nosso fluxo de trabalho for concluído, faça outra toosee de execução de teste passar por ele.

![Fluxo de trabalho concluído para várias saídas mp4 com miniaturas](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-for-multi-mp4-thumbnails.png)

*Fluxo de trabalho concluído para várias saídas mp4 com miniaturas*

## <a id="time_based_trim"></a>Corte baseado em tempo da saída MP4 com várias taxas de bits
A partir de um fluxo de trabalho que gera [uma saída como MP4 de uma entrada de MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), podemos agora verá para cortar o vídeo de origem de saudação com base em carimbos de data / hora.

### <a id="time_based_trim_start"></a>Toostart de visão geral do fluxo de trabalho adicionando restrições para
![Iniciar a remoção de tooadd de fluxo de trabalho para](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-starting-workflow-to-add-trimming.png)

*Iniciar a remoção de tooadd de fluxo de trabalho para*

### <a id="time_based_trim_use_stream_trimmer"></a>Usando Olá filtro de fluxo
componente de filtro de fluxo Olá permite a partir de saudação tootrim e final de um fluxo de entrada se basear em informações de tempo (em segundos, minutos,...). filtro de saudação não oferece suporte a quadros de corte.

![Corte de fluxo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-stream-trimmer.png)

*Corte de fluxo*

Em vez de vincular codificadores Olá AVC e alto-falantes posição cedente toohello entrada do arquivo de mídia diretamente, colocaremos entre esses filtro de fluxo de saudação. (Uma para o sinal de vídeo hello e outro para o sinal de áudio intercaladas hello.)

![Como colocar o Corte de fluxo entre eles](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-put-stream-trimmer-in-between.png)

*Como colocar o Corte de fluxo entre eles*

Vamos configurar filtro de saudação para que somente Processaremos vídeo e áudio entre 15 e 60 segundos no vídeo de saudação.

Vá toohello propriedades de filtro de fluxo de vídeo de hello e configurar as propriedades de hora de término (60 s) e hora de início (15 anos). toomake se ambos os nossos filtro de áudio e vídeo está sempre toohello configurado mesmo começar e terminar valores, publicaremos esses raiz toohello de fluxo de trabalho de saudação.

![Publicar a propriedade de hora de início do Corte de Fluxo](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-start-time-from-stream-trimmer.png)

*Publicar a propriedade de hora de início do Corte de Fluxo*

![Publicar o diálogo da propriedade para a hora de início](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-start-time.png)

*Publicar o diálogo da propriedade para a hora de início*

![Publicar o diálogo da propriedade para a hora de término](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-publish-dialog-for-end-time.png)

*Publicar o diálogo da propriedade para a hora de término*

Se nós agora inspecionar raiz de saudação do nosso fluxo de trabalho, ambas as propriedades será claramente exibido e configuráveis a partir daí.

![Propriedades publicadas disponíveis na raiz](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-published-properties-available-on-root.png)

*Propriedades publicadas disponíveis na raiz*

Abrir as propriedades de corte de saudação do filtro de áudio Olá agora e configurar horários de início e de término com uma expressão que se refere a toohello publicado propriedades na raiz de saudação do nosso fluxo de trabalho.

Para a hora de início de corte de áudio hello:

    ${ROOT_TrimmingStartTime}

e para a hora de término:

    ${ROOT_TrimmingEndTime}

### <a id="time_based_trim_finish"></a>Fluxo de trabalho concluído
![Fluxo de trabalho concluído](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-finished-workflow-time-base-trimming.png)

*Fluxo de trabalho concluído*

## <a id="scripting"></a>Apresentando o hello componente script
Componentes de script podem executar scripts arbitrários durante as fases de execução de saudação do nosso fluxo de trabalho. Há quatro scripts diferentes que podem ser executados, cada um com características específicas e seu próprios lugar no ciclo de vida do fluxo de trabalho hello:

* **commandScript**
* **realizeScript**
* **processInputScript**
* **lifeCycleScript**

documentação de saudação do hello componente script vai em mais detalhes para cada Olá acima. Em [Olá seguinte seção](media-services-media-encoder-premium-workflow-tutorials.md#frame_based_trim), Olá **realizeScript** componente script é usado tooconstruct um xml cliplist imediatamente hello quando Olá será iniciado. Esse script é chamado durante a instalação do componente hello, que ocorre apenas uma vez no ciclo de vida.

### <a id="scripting_hello_world"></a>Criando scripts em um fluxo de trabalho: hello world
Arraste um componente script a superfície do designer hello e renomeá-lo (por exemplo, "SetClipListXML").

![Adicionando um Componente com Script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

*Adicionando um Componente com Script*

Quando você inspecionar as propriedades de saudação do hello componente script, Olá quatro tipos diferentes de script serão mostrados, cada script diferentes tooa configurável.

![Propriedades do Componente com Script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

*Propriedades do Componente com Script*

Limpe Olá processInputScript e abrir editor de saudação do hello realizeScript. Agora estão configurados e pronto toostart de script.

Os scripts são escritos em Groovy, uma linguagem de script compilada dinamicamente para plataforma Java Olá que mantém a compatibilidade com Java. Na verdade, grande parte do código Java é um código Groovy válido.

Vamos escrever um script groovy do simples hello world no contexto de saudação do nosso realizeScript. Insira o seguinte Olá no editor de saudação:

    node.log("hello world");

Agora, realize um teste local. Após essa execução inspecionar (por meio da guia sistema Olá Olá componente script) Olá propriedade Logs.

![Saída do log de Hello world](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output.png)

*Saída do log de Hello world*

objeto de nó de Hello, podemos chamar o método de log hello, refere-se tooour atual "nó" ou componente Olá nós estiver scrip em. Assim, cada componente tem Olá capacidade toooutput registrando dados, disponíveis por meio da guia de sistema de saudação. Nesse caso, estamos saída Olá literal de cadeia de caracteres "Olá, mundo". Toounderstand importante aqui é que isso pode ser toobe uma ferramenta de depuração inestimável, oferecendo informações sobre o script hello está realmente fazer.

De dentro de nosso ambiente de script, também temos acesso tooproperties em outros componentes. Tente o seguinte:

    //inspect current node:
    def nodepath = node.getNodePath();
    node.log("this node path: " + nodepath);

    //walking up tooother nodes:
    def parentnode = node.getParentNode();
    def parentnodepath = parentnode.getNodePath();
    node.log("parent node path: " + parentnodepath);

    //read properties from a node:
    def sourceFileExt = parentnode.getPropertyAsString( "sourceFileExtension", null );
    def sourceFileName = parentnode.getPropertyAsString("sourceFileBaseName", null);
    node.log("source file name with extension " + sourceFileExt + " is: " + sourceFileName);

Nossa janela de log nos mostrará Olá a seguir:

![Saída de log para acessar os caminhos do nó](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-output2.png)

*Saída de log para acessar os caminhos do nó*

## <a id="frame_based_trim"></a>Corte baseado em quadro da saída MP4 com várias taxas de bits
A partir de um fluxo de trabalho que gera [uma saída como MP4 de uma entrada de MXF](media-services-media-encoder-premium-workflow-tutorials.md#MXF_to_MP4_with_dyn_packaging), podemos agora verá para cortar o vídeo de origem de saudação com base na contagem de quadros.

### <a id="frame_based_trim_start"></a>Plano gráfico toostart visão geral sobre a adição de corte para
![Fluxo de trabalho toostart adicionando restrições para](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-workflow-start-adding-trimming-to.png)

*Fluxo de trabalho toostart adicionando restrições para*

### <a id="frame_based_trim_clip_list"></a>Usando Olá Clip lista XML
Todos os tutoriais de fluxo de trabalho anterior, usamos o componente de entrada de arquivo de mídia hello como nossa fonte de entrada de vídeo. Para este cenário específico, usaremos componente de origem da lista de clipe Olá em vez disso. Observe que isso não deve ser a forma preferida de saudação do trabalho; usar somente Olá Clip fonte da lista quando houver um motivo real toodo assim (como no hello abaixo caso, em que estamos fazendo uso dos recursos de fragmentação de lista de clipe Olá).

tooswitch do nosso toohello de entrada de arquivo de mídia Clip fonte da lista, arraste o componente de origem da lista de clipe Olá na superfície de design de saudação e conecte-se Olá Clip lista XML pin toohello Clip lista XML do designer de fluxo de trabalho de saudação. Isso deve preencher Olá Clip fonte da lista com os pins de saída, de acordo com o vídeo de entrada tooour. Agora conectar os pins não compactado de áudio e vídeo descompactado Olá de Olá Olá Clip lista origem toohello respectivos AVC codificadores e Interleaver de fluxo de áudio. Agora remova Olá entrada de arquivo de mídia.

![Substituído Olá entrada de arquivo de mídia com hello clipe de lista de origem](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-replaced-media-file-with-clip-source.png)

*Substituído Olá entrada de arquivo de mídia com hello clipe de lista de origem*

componente de origem da lista de clipe Olá toma como entrada um XML de lista"Clip". Ao selecionar Olá tootest de arquivo de origem com localmente, esse xml de lista de clipe é preenchido automaticamente para você.

![Propriedade XML de lista de clipes preenchida automaticamente](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-auto-populated-clip-list-xml-property.png)

*Propriedade XML de lista de clipes preenchida automaticamente*

Procurando mais detalhadamente xml de toohello, isso é como ele se parece com:

![Diálogo Editar lista de clipes](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-edit-clip-list-dialog.png)

*Diálogo Editar lista de clipes*

No entanto, isso não refletem recursos Olá Olá clip lista XML. Uma opção que temos é tooadd um elemento "Trim" em Olá vídeo e áudio fonte, como este:

![Adicionando uma lista de clipe toohello elemento trim](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-adding-trim-element-to-clip-list.png)

*Adicionando uma lista de clipe toohello elemento trim*

Se você modificar o xml de lista de clipe hello como acima e executar um teste local, você verá o vídeo Olá corretamente foi cortado entre 10 e 20 segundos no vídeo de saudação.

Toowhat contrary acontece quando você fizer uma execução local, embora, esse xml cliplist mesmo não teria Olá mesmo efeito quando aplicado a um fluxo de trabalho é executado no Azure Media Services. Quando é iniciado do codificador do Azure Premium, Olá cliplist xml é gerado sempre que novamente, com base em codificação de saudação de arquivo de entrada hello trabalho foi atribuído. Isso significa que qualquer alteração que fazemos no xml de saudação Infelizmente poderia ser substituída.

toocounter Olá cliplist xml ser apagado quando um trabalho de codificação é iniciado, podemos novamente gerar-Olá imediatamente após o início de saudação do nosso fluxo de trabalho. Essas ações personalizadas podem ser realizadas por meio do que é chamado de "Componente de script". Para obter mais informações, consulte [Introducing Olá componente script](media-services-media-encoder-premium-workflow-tutorials.md#scripting).

Arraste um componente script a superfície do designer hello e renomeá-lo muito "SetClipListXML".

![Adicionando um Componente com Script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-scripted-comp.png)

*Adicionando um Componente com Script*

Quando você inspecionar as propriedades de saudação do hello componente script, Olá quatro tipos diferentes de script serão mostrados, cada script diferentes tooa configurável.

![Propriedades do Componente com Script](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-scripted-comp-properties.png)

*Propriedades do Componente com Script*

### <a id="frame_based_trim_modify_clip_list"></a>Modificando a lista de saudação do clipe de um componente script
Antes de novamente, podemos gravar Olá cliplist xml que é gerado durante a inicialização do fluxo de trabalho, precisaremos conteúdo e a propriedade do toohave acesso toohello cliplist xml. Podemos fazer isso da seguinte forma:

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: " + clipListXML);

![Lista de clipes recebida registrada em log](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-incoming-clip-list-logged.png)

*Lista de clipes recebida registrada em log*

Primeiro, precisamos toodetermine uma maneira de qual ponto até o ponto em que desejamos tootrim Olá vídeo. toomake esse usuário de menos técnico toohello conveniente de fluxo de trabalho Olá publicar raiz de toohello duas propriedades do gráfico de saudação. toodo isso, clique com botão direito superfície do designer hello e selecione "Adicionar propriedade":

* Primeira propriedade: "ClippingTimeStart" do tipo: "TIMECODE"
* Segunda propriedade: "ClippingTimeEnd" do tipo: "TIMECODE"

![Adicionar o diálogo Propriedade à hora de início de corte](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-start-time.png)

*Adicionar o diálogo Propriedade à hora de início de corte*

![Propriedades da hora de corte publicadas na raiz do fluxo de trabalho](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-clip-time-props.png)

*Propriedades da hora de corte publicadas na raiz do fluxo de trabalho*

Configure ambos os valor adequado de tooa propriedades:

![Configurar Olá propriedades de início e término de recorte](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-configure-clip-start-end-prop.png)

*Configurar Olá propriedades de início e término de recorte*

Agora, em nosso script, podemos acessar as duas propriedades, da seguinte maneira:

    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    node.log("clipping start: " + clipstart);
    node.log("clipping end: " + clipend);

![Janela do log mostrando o início e o término do corte](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-show-start-end-clip.png)

*Janela do log mostrando o início e o término do corte*

Vamos analisar cadeias de caracteres de código de tempo de saudação em um formulário toouse mais conveniente, usando uma expressão regular simple:

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);
    node.log("framerate end is: " + endframerate);

![Janela do log com a saúda do código de tempo analisado](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-output-parsed-timecode.png)

*Janela do log com a saúda do código de tempo analisado*

Com essas informações à mão, agora podemos modificar início de Olá Olá cliplist xml tooreflect e horários de término para Olá desejado recorte precisas de quadro do filme hello.

![Elementos de corte script código tooadd](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-add-trim-elements.png)

*Elementos de corte script código tooadd*

Isso foi feito por meio de operações de manipulação de cadeia de caracteres normais. xml de lista de clipe modificado resultante Hello será gravado toohello clipListXML propriedade na raiz de fluxo de trabalho Olá por meio do método "setProperty" hello. janela de log Olá após a execução de outro teste nos mostrariam Olá a seguir:

![Lista de clipe resultante Olá registro](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-log-result-clip-list.png)

*Lista de clipe resultante Olá registro*

Faça um toosee de execução de teste como fluxos de áudio e vídeo de saudação tem sido cortados. Como você fará mais de uma execução de teste com valores diferentes para pontos de corte hello, você observará que aqueles serão não levadas em conta porém! motivo Olá é designer hello, ao contrário de saudação do Azure em tempo de execução, faz não substituição Olá cliplist xml cada execução. Isso significa que somente hello primeira vez que você definiu hello e pontos, fará com que Olá xml tootransform, todos Olá outras vezes, a cláusula de proteção (se (clipListXML.indexOf ("<trim>") = = -1)) impedirá o fluxo de trabalho de saudação de adicionar outro trim elemento quando já há uma presente.

toomake nosso fluxo de trabalho conveniente tootest localmente, é melhor adicionar algum código de manutenção de casa que verifica se um elemento de corte já estiver presente. Nesse caso, estamos pode removê-lo antes de continuar modificando Olá xml com os novos valores de saudação. Em vez de usar manipulações de cadeia de caracteres simples, é mais seguro provavelmente toodo isso por meio do objeto xml real do modelo de análise.

Antes que possamos adicionar esse código no entanto, vamos precisar tooadd que um número de instruções de importação no hello início do nosso script primeiro:

    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

Depois disso, podemos adicionar Olá necessário código de limpeza:

    //for local testing: delete any pre-existing trim elements from hello clip list xml by parsing hello xml into a DOM:
    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements,dom,XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
     //delete hello trim nodes:
    elementsToDelete.each{
        e -> e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

Esse código vai acima ponto Olá em que adicionamos Olá elementos trim toohello cliplist xml.

Neste ponto, podemos executar e modificar nosso fluxo de trabalho como tempo quanto queremos tendo alterações Olá aplicadas nunca.    

### <a id="frame_based_trim_clippingenabled_prop"></a>Adicionando uma propriedade de conveniência ClippingEnabled
Como você pode não querer sempre toohappen corte, vamos finalizar nosso fluxo de trabalho adicionando um conveniente sinalizador booliano que indica se deseja ou não podemos tooenable cortar / recorte.

Assim como antes, publicar uma nova raiz de toohello de propriedade de nosso fluxo de trabalho chamado "ClippingEnabled" do tipo "Booleano".

![Propriedade publicada para habilitar o recorte](./media/media-services-media-encoder-premium-workflow-tutorials/media-services-enable-clip.png)

*Propriedade publicada para habilitar o recorte*

Com hello abaixo cláusula de guarda simples, podemos verificar se a fragmentação é necessária e decidir se nossa lista de clipe como tal precisa toobe modificado ou não.

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }


### <a id="code"></a>Código completo
    import javax.xml.parsers.*;
    import org.xml.sax.*;
    import org.w3c.dom.*;
    import javax.xml.*;
    import javax.xml.xpath.*;
    import javax.xml.transform.*;
    import javax.xml.transform.stream.*;
    import javax.xml.transform.dom.*;

    // get cliplist xml:
    def clipListXML = node.getProperty("../clipListXml");
    node.log("clip list xml coming in: \n" + clipListXML);
    // get start and end of clipping:
    def clipstart = node.getProperty("../ClippingTimeStart").toString();
    def clipend = node.getProperty("../ClippingTimeEnd").toString();

    //parse hello start timing:
    def startregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipstart);
    startregresult.matches();
    def starttimecode = startregresult.group(1);
    node.log("timecode start is: " + starttimecode);
    def startframerate = startregresult.group(2);
    node.log("framerate start is: " + startframerate);

    //parse hello end timing:
    def endregresult = (~/(\d\d:\d\d:\d\d:\d\d)\/(\d\d)/).matcher(clipend);
    endregresult.matches();
    def endtimecode = endregresult.group(1);
    node.log("timecode end is: " + endtimecode);
    def endframerate = endregresult.group(2);

    node.log("framerate end is: " + endframerate);

    //for local testing: delete any pre-existing trim elements
    //from hello clip list xml by parsing hello xml into a DOM:

    DocumentBuilderFactory factory=DocumentBuilderFactory.newInstance();
    DocumentBuilder builder=factory.newDocumentBuilder();
    InputSource is=new InputSource(new StringReader(clipListXML));
    Document dom=builder.parse(is);

    //find hello trim element inside videoSource and audioSource and remove it if it exists already:
    XPath xpath = XPathFactory.newInstance().newXPath();
    String findAllTrimElements = "//trim";
    NodeList trimelems = xpath.evaluate(findAllTrimElements, dom, XPathConstants.NODESET);

    //copy trim nodes into a "to-be-deleted" collection
    Set<Element> elementsToDelete = new HashSet<Element>();
    for (int i = 0; i < trimelems.getLength(); i++) {
        Element e = (Element)trimelems.item(i);
        elementsToDelete.add(e);
    }

    node.log("about toodelete any existing trim nodes");
    //delete hello trim nodes:
    elementsToDelete.each{ e ->
        e.getParentNode().removeChild(e);
    };
    node.log("deleted any existing trim nodes");

    //serialize hello modified clip list xml dom into a string:
    def transformer = TransformerFactory.newInstance().newTransformer();
    StreamResult result = new StreamResult(new StringWriter());
    DOMSource source = new DOMSource(dom);
    transformer.transform(source, result);
    clipListXML = result.getWriter().toString();

    //check if clipping is required:
    def clippingrequired = node.getProperty("../ClippingEnabled");
    node.log("clipping required: " + clippingrequired.toString());
    if(clippingrequired == null || clippingrequired == false)
    {
        node.setProperty("../clipListXml",clipListXML);
        node.log("no clipping required");
        return;
    }

    //add trim elements toocliplist xml
    if ( clipListXML.indexOf("<trim>") == -1 )
    {
        //trim video
        clipListXML = clipListXML.replace("<videoSource>","<videoSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\"" + endframerate +"\"> " + endtimecode +
            " </outPoint>\n </trim> \n");
        //trim audio
        clipListXML = clipListXML.replace("<audioSource>","<audioSource>\n <trim>\n <inPoint fps=\""+
            startframerate +"\">" + starttimecode +
            "</inPoint>\n" + "<outPoint fps=\""+ endframerate +"\">" +
            endtimecode + "</outPoint>\n </trim>\n");
        node.log( "clip list going out: \n" +clipListXML );
        node.setProperty("../clipListXml",clipListXML);
    }


## <a name="also-see"></a>Consulte também
[Apresentando a codificação Premium nos Serviços de Mídia do Azure](http://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services)

[Como tooUse Premium de codificação no Azure Media Services](http://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services)

[Codificando conteúdo sob demanda com os Serviços de Mídia do Azure](media-services-encode-asset.md#media-encoder-premium-workflow)

[Codecs e formatos de fluxo de trabalho do Media Encoder Premium](media-services-premium-workflow-encoder-formats.md)

[Exemplos de arquivos de fluxo de trabalho](http://github.com/Azure/azure-media-services-samples/tree/master/Encoding%20Presets/VoD/MediaEncoderPremiumWorkfows)

[Ferramenta do Explorador dos Serviços de Mídia do Azure](http://aka.ms/amse)

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
