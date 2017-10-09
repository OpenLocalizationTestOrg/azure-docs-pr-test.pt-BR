---
title: aaaSmooth Streaming Windows Store App Tutorial | Microsoft Docs
description: "Saiba como toouse Azure Media Services toocreate um aplicativo c# da Windows Store com um MediaElement XML controlar o conteúdo de Smooth Stream tooplayback."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 0fa5d8c5-3d5f-4886-ae55-fb6de4f5256d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: juliako
ms.openlocfilehash: b02aa2c7f68fe22a23ea846d72fdd23bfba2b19c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobuild-a-smooth-streaming-windows-store-application"></a>Como tooBuild um aplicativo Smooth Streaming Windows Store

Olá Smooth Streaming Client SDK para Windows 8 permite que os aplicativos da Windows Store toobuild os desenvolvedores que podem reproduzir o conteúdo de Smooth Streaming ao vivo e sob demanda. Além disso, toohello de reprodução básicas de Smooth Streaming de conteúdo, Olá SDK também fornece recursos avançados, como proteção do Microsoft PlayReady, restrição de nível de qualidade, Live DVR, fluxo de áudio alternando, escutando para atualizações de status (tais como alterações de nível de qualidade ) e eventos de erro e assim por diante. Para obter mais informações de recursos de saudação com suporte, consulte Olá [notas de versão](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes). Para obter mais informações, consulte [Player Framework para Windows 8](http://playerframework.codeplex.com/). 

Este tutorial contém quatro lições:

1. Criar um aplicativo de armazenamento básico Smooth Streaming
2. Adicionar um controle deslizante barra tooControl Olá progresso de mídia
3. Selecionar fluxos do Smooth Streaming
4. Selecionar faixas do Smooth Streaming

## <a name="prerequisites"></a>Pré-requisitos
* Windows 8 32 bits ou 64 bits. Você pode obter o [Windows 8 Enterprise Evaluation (a página pode estar em inglês)](http://msdn.microsoft.com/evalcenter/jj554510.aspx) no MSDN.
* Visual Studio 2012 ou Visual Studio Express 2012 (ou versão posterior). Você pode obter a versão de avaliação de saudação do [aqui](http://www.microsoft.com/visualstudio/11/downloads).
* [SDK do Microsoft Smooth Streaming Client para Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home)

solução de saudação concluída para cada lição pode ser baixada de exemplos de código do MSDN Developer (Galeria de códigos): 

* [Lição 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) - Um Media Player simples de Smooth Streaming do Windows 8, 
* [Lição 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) - Um Media Player simples de Smooth Streaming do Windows 8 com um controle de barra deslizante, 
* [Lição 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) - Um Media Player simples de Smooth Streaming do Windows 8 com seleção de fluxo,  
* [Lição 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907) - um Media Player simples de Smooth Streaming do Windows 8 com seleção de faixa.

## <a name="lesson-1-create-a-basic-smooth-streaming-store-application"></a>Lição 1: Criar um aplicativo básico de Smooth Streaming para a Store

Nesta lição, você criará um aplicativo da Windows Store com um MediaElement controle tooplay Smooth Stream conteúdo.  aplicativo em execução Hello é semelhante a:

![Exemplo de aplicativo de Smooth Streaming da Windows Store][PlayerApplication]

Para obter mais informações sobre como desenvolver aplicativos da Windows Store, consulte [Desenvolver Ótimos Aplicativos para o Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx). Esta lição contém Olá procedimentos a seguir:

1. Criar um novo projeto da Windows Store
2. Interface de usuário do design hello (XAML)
3. Modificar Olá arquivo code-behind
4. Compilar e testar o aplicativo hello

**toocreate um projeto da Windows Store**

1. Execute o Visual Studio 2012 ou posterior.
2. De saudação **arquivo** menu, clique em **novo**e, em seguida, clique em **projeto**.
3. Caixa de diálogo do novo projeto hello, tipo ou hello select a seguir valores:

| Nome | Valor |
| --- | --- |
| Grupo de modelos |Instalado/Modelos/Visual C#/Windows Store |
| Modelo |Aplicativo em branco (XAML) |
| Nome |SSPlayer |
| Local |C:\SSTutorials |
| Nome da solução |SSPlayer |
| Criar diretório para a solução |(selecionado) |

1. Clique em **OK**.

**tooadd toohello uma referência SDK de cliente Smooth Streaming**

1. No Gerenciador de Soluções, clique com o botão direito do mouse em **SSPlayer** e, em seguida, clique em **Adicionar Referência**.
2. Digite ou selecione Olá valores a seguir:

| Nome | Valor |
| --- | --- |
| Grupo de referências |Windows/Extensions |
| Referência |Selecione SDK do Microsoft Smooth Streaming Client para Windows 8 e Pacote do Tempo de Execução do Microsoft Visual C++ |

1. Clique em **OK**. 

Depois de adicionar referências Olá, você deve selecionar a plataforma Olá direcionado (x64 ou x86), adição de referências não funcionará para configuração de plataforma de qualquer CPU.  No Gerenciador de Soluções, você verá a marca de aviso amarela para essas referências adicionadas.

**interface do usuário toodesign Olá player**

1. No Gerenciador de soluções, clique duas vezes em **MainPage. XAML** tooopen-lo no design Olá exibir.
2. Localizar Olá  **&lt;grade&gt;**  e  **&lt;/Grid&gt;**  marcas Olá arquivo XAML e código a seguir de saudação colar entre as marcas de saudação dois:

         <Grid.RowDefinitions>

            <RowDefinition Height="20"/>    <!-- spacer -->
            <RowDefinition Height="50"/>    <!-- media controls -->
            <RowDefinition Height="100*"/>  <!-- media element -->
            <RowDefinition Height="80*"/>   <!-- media stream and track selection -->
            <RowDefinition Height="50"/>    <!-- status bar -->
         </Grid.RowDefinitions>

         <StackPanel Name="spMediaControl" Grid.Row="1" Orientation="Horizontal">
            <TextBlock x:Name="tbSource" Text="Source :  " FontSize="16" FontWeight="Bold" VerticalAlignment="Center" />
            <TextBox x:Name="txtMediaSource" Text="http://ecn.channel9.msdn.com/o9/content/smf/smoothcontent/elephantsdream/Elephants_Dream_1024-h264-st-aac.ism/manifest" FontSize="10" Width="700" Margin="0,4,0,10" />
            <Button x:Name="btnSetSource" Content="Set Source" Width="111" Height="43" Click="btnSetSource_Click"/>
            <Button x:Name="btnPlay" Content="Play" Width="111" Height="43" Click="btnPlay_Click"/>
            <Button x:Name="btnPause" Content="Pause"  Width="111" Height="43" Click="btnPause_Click"/>
            <Button x:Name="btnStop" Content="Stop"  Width="111" Height="43" Click="btnStop_Click"/>
            <CheckBox x:Name="chkAutoPlay" Content="Auto Play" Height="55" Width="Auto" IsChecked="{Binding AutoPlay, ElementName=mediaElement, Mode=TwoWay}"/>
            <CheckBox x:Name="chkMute" Content="Mute" Height="55" Width="67" IsChecked="{Binding IsMuted, ElementName=mediaElement, Mode=TwoWay}"/>
         </StackPanel>

         <StackPanel Name="spMediaElement" Grid.Row="2" Height="435" Width="1072"
                    HorizontalAlignment="Center" VerticalAlignment="Center">
            <MediaElement x:Name="mediaElement" Height="356" Width="924" MinHeight="225"
                          HorizontalAlignment="Center" VerticalAlignment="Center" 
                          AudioCategory="BackgroundCapableMedia" />
            <StackPanel Orientation="Horizontal">
                <Slider x:Name="sliderProgress" Width="924" Height="44"
                        HorizontalAlignment="Center" VerticalAlignment="Center"
                        PointerPressed="sliderProgress_PointerPressed"/>
                <Slider x:Name="sliderVolume" 
                        HorizontalAlignment="Right" VerticalAlignment="Center" Orientation="Vertical" 
                        Height="79" Width="148" Minimum="0" Maximum="1" StepFrequency="0.1" 
                        Value="{Binding Volume, ElementName=mediaElement, Mode=TwoWay}" 
                        ToolTipService.ToolTip="{Binding Value, RelativeSource={RelativeSource Mode=Self}}"/>
            </StackPanel>
         </StackPanel>

         <StackPanel Name="spStatus" Grid.Row="4" Orientation="Horizontal">
            <TextBlock x:Name="tbStatus" Text="Status :  " 
               FontSize="16" FontWeight="Bold" VerticalAlignment="Center" HorizontalAlignment="Center" />
            <TextBox x:Name="txtStatus" FontSize="10" Width="700" VerticalAlignment="Center"/>
         </StackPanel>
   
   Olá controle MediaElement é uma mídia tooplayback usado. controle deslizante de saudação denominado sliderProgress será usado em andamento Olá próximo lição toocontrol Olá mídia.
3. Pressione **CTRL + S** toosave arquivo de saudação.

Olá controle MediaElement não oferece suporte a Streaming suave conteúda fora da caixa. suporte de Smooth Streaming de saudação de tooenable, você deve registrar o manipulador de Olá fluxo de bytes Smooth Streaming pela extensão de nome de arquivo e o tipo MIME.  tooregister, você usar o método MediaExtensionManager.RegisterByteStremHandler Olá Olá botão namespace.

Esse arquivo XAML, alguns manipuladores de eventos são associados com controles de saudação.  Você deve definir esses manipuladores de eventos.

**toomodify Olá arquivo code-behind**

1. No Gerenciador de Soluções, clique com o botão direito do mouse em **MainPage.xaml** e clique em **Exibir Código**.
2. Na parte superior de saudação do arquivo hello, adicione o seguinte de saudação usando a instrução:
   
        using Windows.Media;
3. Início de saudação do hello **MainPage** classe, adicione Olá membro de dados a seguir:
   
         private MediaExtensionManager extensions = new MediaExtensionManager();
4. No final de saudação do hello **MainPage** construtor, adicionar Olá duas linhas a seguir:
   
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "text/xml");
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "application/vnd.ms-sstr+xml");
5. No final de saudação do hello **MainPage** classe, cole Olá código a seguir:
   
         # region UI Button Click Events
         private void btnPlay_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Play();
         txtStatus.Text = "MediaElement is playing ...";
         }
         private void btnPause_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Pause();
         txtStatus.Text = "MediaElement is paused";
         }
         private void btnSetSource_Click(object sender, RoutedEventArgs e)
         {

         sliderProgress.Value = 0;
         mediaElement.Source = new Uri(txtMediaSource.Text);

         if (chkAutoPlay.IsChecked == true)
         {
             txtStatus.Text = "MediaElement is playing ...";
         }
         else
         {
             txtStatus.Text = "Click hello Play button tooplay hello media source.";
         }
         }
         private void btnStop_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Stop();
         txtStatus.Text = "MediaElement is stopped";
         }
         private void sliderProgress_PointerPressed(object sender, PointerRoutedEventArgs e)
         {

         txtStatus.Text = "Seek tooposition " + sliderProgress.Value;
         mediaElement.Position = new TimeSpan(0, 0, (int)(sliderProgress.Value));
         }
         # endregion

manipulador de eventos sliderProgress_PointerPressed Olá é definido aqui.  Há mais tooget de toodo funciona trabalhando, que será abordado na próxima lição Olá deste tutorial.
6. Pressione **CTRL + S** toosave arquivo de saudação.

Hello Olá terminar arquivo code-behind deve ser assim:

![Exibição do código no Visual Studio do aplicativo de Smooth Streaming da Windows Store][CodeViewPic]

**toocompile e testar o aplicativo hello**

1. De saudação **criar** menu, clique em **do Configuration Manager**.
2. Alterar **plataforma de solução ativa** toomatch sua plataforma de desenvolvimento.
3. Pressione **F6** toocompile projeto de saudação. 
4. Pressione **F5** aplicativo hello de toorun.
5. Na parte superior de saudação do aplicativo hello, você pode usar saudação padrão URL de Smooth Streaming ou insira outro. 
6. Clique em **Definir Origem**. Porque **reprodução automática** é habilitado por padrão, Olá reprodutor de mídia será automaticamente.  Você pode controlar a mídia de saudação usando Olá **reproduzir**, **pausar** e **parar** botões.  Você pode controlar o volume de mídia hello usando slider vertical hello.  No entanto, Olá horizontal controle deslizante para controlar Olá andamento da mídia ainda não está totalmente implementado. 

Você concluiu a Lição 1.  Nesta lição, você deve usar um controle de MediaElement tooplayback conteúdo de Smooth Streaming.  Próxima hello, você adicionará um progresso do controle deslizante toocontrol Olá de saudação conteúdo Smooth Streaming.

## <a name="lesson-2-add-a-slider-bar-toocontrol-hello-media-progress"></a>Lição 2: Adicionar um controle deslizante barra tooControl Olá progresso de mídia

Na lição 1, você criou um aplicativo da Windows Store com um controle de MediaElement XAML tooplayback conteúdo Smooth Streaming de mídia.  Ele vem com algumas funções básicas de mídia, como iniciar, parar e pausar.  Nesta lição, você adicionará um aplicativo toohello de controle de barra de controle deslizante.

Neste tutorial, usaremos uma posição de controle deslizante de saudação do timer tooupdate com base na posição atual de saudação do hello controle MediaElement.  controle deslizante de saudação início e hora de término também toobe necessidade atualizado em caso de conteúdo ao vivo.  Isso pode ser melhor tratado no evento de atualização de origem adaptável hello.

As origens de mídia são objetos que geram dados de mídia.  resolvedor de origem Olá leva um fluxo de bytes ou de URL e cria Olá mídia adequada fonte desse conteúdo.  resolvedor de origem Olá é forma padrão de saudação para fontes de mídia Olá aplicativos toocreate. 

Esta lição contém Olá procedimentos a seguir:

1. Registrar o manipulador de Smooth Streaming Olá 
2. Adicionar manipuladores de eventos de nível de Gerenciador de fonte adaptável de Olá
3. Adicionar manipuladores de eventos no nível de fonte adaptável Olá
4. Adicionar manipuladores de eventos de MediaElement
5. Adicionar o código relacionado à barra de controle deslizante
6. Compilar e testar o aplicativo hello

**tooregister Olá fluxo de bytes Smooth Streaming manipulador e passe Olá propertyset**

1. No Gerenciador de Soluções, clique com o botão direito do mouse em **MainPage.xaml** e clique em **Exibir Código**.
2. Início de saudação do arquivo hello, adicione o seguinte de saudação usando a instrução:

        using Microsoft.Media.AdaptiveStreaming;
3. Início de saudação do hello classe MainPage, adicione Olá membros de dados a seguir:

         private Windows.Foundation.Collections.PropertySet propertySet = new Windows.Foundation.Collections.PropertySet();             
         private IAdaptiveSourceManager adaptiveSourceManager;
4. Olá interna **MainPage** construtor, adicionar Olá código a seguir após Olá **isso. Inicializar Components();**  linha e linhas de código de registro Olá gravadas na lição anterior hello:

        // Gets hello default instance of AdaptiveSourceManager which manages Smooth 
        //Streaming media sources.
        adaptiveSourceManager = AdaptiveSourceManager.GetDefault();
        // Sets property key value tooAdaptiveSourceManager default instance.
        // {A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}" must be hardcoded.
        propertySet["{A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}"] = adaptiveSourceManager;
5. Olá interna **MainPage** construtor, modificar a saudação do hello dois RegisterByteStreamHandler métodos tooadd sucessivamente parâmetros:

         // Registers Smooth Streaming byte-stream handler for ".ism" extension and, 
         // "text/xml" and "application/vnd.ms-ss" mime-types and pass hello propertyset. 
         // http://*.ism/manifest URI resources will be resolved by Byte-stream handler.
         extensions.RegisterByteStreamHandler(

            "Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", 
            ".ism", 
            "text/xml", 
            propertySet );
         extensions.RegisterByteStreamHandler(

            "Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", 
            ".ism", 
            "application/vnd.ms-sstr+xml", 
         propertySet);
6. Pressione **CTRL + S** toosave arquivo de saudação.

**manipulador de eventos no nível do tooadd Olá fonte adaptável manager**

1. No Gerenciador de Soluções, clique com o botão direito do mouse em **MainPage.xaml** e clique em **Exibir Código**.
2. Olá interna **MainPage** classe, adicione Olá membro de dados a seguir:
   
     private AdaptiveSource adaptiveSource = null;
3. No final de saudação do hello **MainPage** classe, adicione Olá manipulador de eventos a seguir:
   
         # region Adaptive Source Manager Level Events
         private void mediaElement_AdaptiveSourceOpened(AdaptiveSource sender, AdaptiveSourceOpenedEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
         }

         # endregion Adaptive Source Manager Level Events
4. No final de saudação do hello **MainPage** construtor, adicionar Olá linha toosubscribe toohello adaptável fonte aberta de evento a seguir:
   
         adaptiveSourceManager.AdaptiveSourceOpenedEvent += 
           new AdaptiveSourceOpenedEventHandler(mediaElement_AdaptiveSourceOpened);
5. Pressione **CTRL + S** toosave arquivo de saudação.

**manipuladores de eventos no nível de fonte adaptável tooadd**

1. No Gerenciador de Soluções, clique com o botão direito do mouse em **MainPage.xaml** e clique em **Exibir Código**.
2. Olá interna **MainPage** classe, adicione Olá membro de dados a seguir:
   
     private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;
3. No final de saudação do hello **MainPage** classe, adicione Olá manipuladores de eventos a seguir:

         # region Adaptive Source Level Events
         private void mediaElement_ManifestReady(AdaptiveSource sender, ManifestReadyEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
            manifestObject = args.AdaptiveSource.Manifest;
         }

         private void mediaElement_AdaptiveSourceStatusUpdated(AdaptiveSource sender, AdaptiveSourceStatusUpdatedEventArgs args)
         {

            adaptiveSourceStatusUpdate = args;
         }

         private void mediaElement_AdaptiveSourceFailed(AdaptiveSource sender, AdaptiveSourceFailedEventArgs args)
         {

            txtStatus.Text = "Error: " + args.HttpResponse;
         }

         # endregion Adaptive Source Level Events
4. No final de saudação do hello **mediaElement AdaptiveSourceOpened** método, adicione Olá eventos de toohello de toosubscribe de código a seguir:
   
         adaptiveSource.ManifestReadyEvent +=

                    mediaElement_ManifestReady;
         adaptiveSource.AdaptiveSourceStatusUpdatedEvent += 

            mediaElement_AdaptiveSourceStatusUpdated;
         adaptiveSource.AdaptiveSourceFailedEvent += 

            mediaElement_AdaptiveSourceFailed;
5. Pressione **CTRL + S** toosave arquivo de saudação.

Olá mesmos eventos estão disponíveis na fonte adaptável Manager nível, que pode ser usado para tratar aos elementos de mídia comuns tooall de funcionalidade no aplicativo hello. Cada AdaptiveSource inclui seus próprios eventos e todos os eventos de AdaptiveSource serão colocados em cascata no AdaptiveSourceManager.

**manipuladores de eventos do elemento de mídia tooadd**

1. No Gerenciador de Soluções, clique com o botão direito do mouse em **MainPage.xaml** e clique em **Exibir Código**.
2. No final de saudação do hello **MainPage** classe, adicione Olá manipuladores de eventos a seguir:

         # region Media Element Event Handlers
         private void MediaOpened(object sender, RoutedEventArgs e)
         {

            txtStatus.Text = "MediaElement opened";
         }

         private void MediaFailed(object sender, ExceptionRoutedEventArgs e)
         {

            txtStatus.Text= "MediaElement failed: " + e.ErrorMessage;
         }

         private void MediaEnded(object sender, RoutedEventArgs e)
         {

            txtStatus.Text ="MediaElement ended.";
         }

         # endregion Media Element Event Handlers
3. No final de saudação do hello **MainPage** construtor, adicionar Olá eventos de toohello de toosubscript de código a seguir:

         mediaElement.MediaOpened += MediaOpened;
         mediaElement.MediaEnded += MediaEnded;
         mediaElement.MediaFailed += MediaFailed;
4. Pressione **CTRL + S** toosave arquivo de saudação.

**controle deslizante de tooadd relacionado código de barras**

1. No Gerenciador de Soluções, clique com o botão direito do mouse em **MainPage.xaml** e clique em **Exibir Código**.
2. Início de saudação do arquivo hello, adicione o seguinte de saudação usando a instrução:
      
        using Windows.UI.Core;
3. Olá interna **MainPage** classe, adicione Olá membros de dados a seguir:
   
         public static CoreDispatcher _dispatcher;
         private DispatcherTimer sliderPositionUpdateDispatcher;
4. No final de saudação do hello **MainPage** construtor, adicionar Olá código a seguir:
   
         _dispatcher = Window.Current.Dispatcher;
         PointerEventHandler pointerpressedhandler = new PointerEventHandler(sliderProgress_PointerPressed);
         sliderProgress.AddHandler(Control.PointerPressedEvent, pointerpressedhandler, true);    
5. No final de saudação do hello **MainPage** classe, adicione Olá código a seguir:

         # region sliderMediaPlayer
         private double SliderFrequency(TimeSpan timevalue)
         {

            long absvalue = 0;
            double stepfrequency = -1;

            if (manifestObject != null)
            {
                absvalue = manifestObject.Duration - (long)manifestObject.StartTime;
            }
            else
            {
                absvalue = mediaElement.NaturalDuration.TimeSpan.Ticks;
            }

            TimeSpan totalDVRDuration = new TimeSpan(absvalue);

            if (totalDVRDuration.TotalMinutes >= 10 && totalDVRDuration.TotalMinutes < 30)
            {
               stepfrequency = 10;
            }
            else if (totalDVRDuration.TotalMinutes >= 30 
                     && totalDVRDuration.TotalMinutes < 60)
            {
                stepfrequency = 30;
            }
            else if (totalDVRDuration.TotalHours >= 1)
            {
                stepfrequency = 60;
            }

            return stepfrequency;
         }

         void updateSliderPositionoNTicks(object sender, object e)
         {

            sliderProgress.Value = mediaElement.Position.TotalSeconds;
         }

         public void setupTimer()
         {

            sliderPositionUpdateDispatcher = new DispatcherTimer();
            sliderPositionUpdateDispatcher.Interval = new TimeSpan(0, 0, 0, 0, 300);
            startTimer();
         }

         public void startTimer()
         {

            sliderPositionUpdateDispatcher.Tick += updateSliderPositionoNTicks;
            sliderPositionUpdateDispatcher.Start();
         }

         // Slider start and end time must be updated in case of live content
         public async void setSliderStartTime(long startTime)
         {

            await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
            {
                TimeSpan timespan = new TimeSpan(adaptiveSourceStatusUpdate.StartTime);
                double absvalue = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero);
                sliderProgress.Minimum = absvalue;
            });
         }

         // Slider start and end time must be updated in case of live content
         public async void setSliderEndTime(long startTime)
         {

            await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
            {
                TimeSpan timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime);
                double absvalue = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero);
                sliderProgress.Maximum = absvalue;
            });
         }

         # endregion sliderMediaPlayer
      
>[!NOTE]
>CoreDispatcher é usado toomake alterações toohello da interface do usuário do thread de Thread de interface do usuário não. No caso de afunilamento no thread do distribuidor, o desenvolvedor pode escolher toouse dispatcher fornecido pelo elemento de interface do usuário que ele pretenda tooupdate.  Por exemplo:
   
         await sliderProgress.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () => { TimeSpan 

         timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime); 
         double absvalue  = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero); 

         sliderProgress.Maximum = absvalue; }); 
6. No final de saudação do hello **mediaElement_AdaptiveSourceStatusUpdated** método, adicione Olá código a seguir:

         setSliderStartTime(args.StartTime);
         setSliderEndTime(args.EndTime);
7. No final de saudação do hello **MediaOpened** método, adicione Olá código a seguir:

         sliderProgress.StepFrequency = SliderFrequency(mediaElement.NaturalDuration.TimeSpan);
         sliderProgress.Width = mediaElement.Width;
         setupTimer();
8. Pressione **CTRL + S** toosave arquivo de saudação.

**toocompile e testar o aplicativo hello**

1. Pressione **F6** toocompile projeto de saudação. 
2. Pressione **F5** aplicativo hello de toorun.
3. Na parte superior de saudação do aplicativo hello, você pode usar saudação padrão URL de Smooth Streaming ou insira outro. 
4. Clique em **Definir Origem**. 
5. Barra de controle deslizante de saudação do teste.

Você concluiu a lição 2.  Nesta lição, você adicionou um controle deslizante tooapplication. 

## <a name="lesson-3-select-smooth-streaming-streams"></a>Lição 3: Selecionar fluxos de Smooth Streaming
Smooth Streaming é toostream compatível com conteúdo com várias faixas de áudio de idioma que são selecionáveis visualizadores hello.  Nesta lição, você habilitará fluxos de tooselect visualizadores. Esta lição contém Olá procedimentos a seguir:

1. Modificar o arquivo XAML de saudação
2. Modificar o arquivo de behand código Olá
3. Compilar e testar o aplicativo hello

**arquivo do toomodify Olá XAML**

1. No Gerenciador de Soluções, clique com o botão direito do mouse em **MainPage.xaml**, e, em seguida, clique em **Designer de Modos de Exibição**.
2. Localize &lt;Grid.RowDefinitions&gt;e modificar Olá RowDefinitions para que eles se parece com:
   
         <Grid.RowDefinitions>            
            <RowDefinition Height="20"/>
            <RowDefinition Height="50"/>
            <RowDefinition Height="100"/>
            <RowDefinition Height="80"/>
            <RowDefinition Height="50"/>
         </Grid.RowDefinitions>
3. Olá interna &lt;grade&gt;&lt;/Grid&gt; marcas, adicione a saudação de código a seguir toodefine um controle listbox, para que os usuários podem ver Olá lista de fluxos disponíveis e selecione fluxos:

         <Grid Name="gridStreamAndBitrateSelection" Grid.Row="3">
            <Grid.RowDefinitions>
                <RowDefinition Height="300"/>
            </Grid.RowDefinitions>
            <Grid.ColumnDefinitions>
                <ColumnDefinition Width="250*"/>
                <ColumnDefinition Width="250*"/>
            </Grid.ColumnDefinitions>
            <StackPanel Name="spStreamSelection" Grid.Row="1" Grid.Column="0">
                <StackPanel Orientation="Horizontal">
                    <TextBlock Name="tbAvailableStreams" Text="Available Streams:" FontSize="16" VerticalAlignment="Center"></TextBlock>
                    <Button Name="btnChangeStreams" Content="Submit" Click="btnChangeStream_Click"/>
                </StackPanel>
                <ListBox x:Name="lbAvailableStreams" Height="200" Width="200" Background="Transparent" HorizontalAlignment="Left" 
                    ScrollViewer.VerticalScrollMode="Enabled" ScrollViewer.VerticalScrollBarVisibility="Visible">
                    <ListBox.ItemTemplate>
                        <DataTemplate>
                            <CheckBox Content="{Binding Name}" IsChecked="{Binding isChecked, Mode=TwoWay}" />
                        </DataTemplate>
                    </ListBox.ItemTemplate>
                </ListBox>
            </StackPanel>
         </Grid>
4. Pressione **CTRL + S** toosave alterações de saudação.

**toomodify Olá arquivo code-behind**

1. No Gerenciador de Soluções, clique com o botão direito do mouse em **MainPage.xaml** e clique em **Exibir Código**.
2. Olá SSPlayer namespace, adicione uma nova classe:
   
        #region class Stream
   
        public class Stream
        {
            private IManifestStream stream;
            public bool isCheckedValue;
            public string name;
   
            public string Name
            {
                get { return name; }
                set { name = value; }
            }
   
            public IManifestStream ManifestStream
            {
                get { return stream; }
                set { stream = value; }
            }
   
            public bool isChecked
            {
                get { return isCheckedValue; }
                set
                {
                    // mMke hello video stream always checked.
                    if (stream.Type == MediaStreamType.Video)
                    {
                        isCheckedValue = true;
                    }
                    else
                    {
                        isCheckedValue = value;
                    }
                }
            }
   
            public Stream(IManifestStream streamIn)
            {
                stream = streamIn;
                name = stream.Name;
            }
        }
        #endregion class Stream
3. Início de saudação do hello classe MainPage, adicione Olá definições de variáveis a seguir:
   
         private List<Stream> availableStreams;
         private List<Stream> availableAudioStreams;
         private List<Stream> availableTextStreams;
         private List<Stream> availableVideoStreams;
4. Em Olá classe MainPage, adicione Olá região a seguir:
   
        #region stream selection
        ///<summary>
        ///Functionality tooselect streams from IManifestStream available streams
        /// </summary>
   
        // This function is called from hello mediaElement_ManifestReady event handler 
        // tooretrieve hello streams and populate them toohello local data members.
        public void getStreams(Manifest manifestObject)
        {
            availableStreams = new List<Stream>();
            availableVideoStreams = new List<Stream>();
            availableAudioStreams = new List<Stream>();
            availableTextStreams = new List<Stream>();
   
            try
            {
                for (int i = 0; i<manifestObject.AvailableStreams.Count; i++)
                {
                    Stream newStream = new Stream(manifestObject.AvailableStreams[i]);
                    newStream.isChecked = false;
   
                    //populate hello stream lists based on hello types
                    availableStreams.Add(newStream);
   
                    switch (newStream.ManifestStream.Type)
                    {
                        case MediaStreamType.Video:
                            availableVideoStreams.Add(newStream);
                            break;
                        case MediaStreamType.Audio:
                            availableAudioStreams.Add(newStream);
                            break;
                        case MediaStreamType.Text:
                            availableTextStreams.Add(newStream);
                            break;
                    }
   
                    // Select hello default selected streams from hello manifest.
                    for (int j = 0; j<manifestObject.SelectedStreams.Count; j++)
                    {
                        string selectedStreamName = manifestObject.SelectedStreams[j].Name;
                        if (selectedStreamName.Equals(newStream.Name))
                        {
                            newStream.isChecked = true;
                            break;
                        }
                    }
                }
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }
        }
   
        // This function set hello list box ItemSource
        private async void refreshAvailableStreamsListBoxItemSource()
        {
            try
            {
                //update hello stream check box list on hello UI
                await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, ()
                    => { lbAvailableStreams.ItemsSource = availableStreams; });
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }
        }
   
        // This function creates a selected streams list
        private void createSelectedStreamsList(List<IManifestStream> selectedStreams)
        {
            bool isOneVideoSelected = false;
            bool isOneAudioSelected = false;
   
            // Only one video stream can be selected
            for (int j = 0; j<availableVideoStreams.Count; j++)
            {
                if (availableVideoStreams[j].isChecked && (!isOneVideoSelected))
                {
                    selectedStreams.Add(availableVideoStreams[j].ManifestStream);
                    isOneVideoSelected = true;
                }
            }
   
            // Select hello frist video stream from hello list if no video stream is selected
            if (!isOneVideoSelected)
            {
                availableVideoStreams[0].isChecked = true;
                selectedStreams.Add(availableVideoStreams[0].ManifestStream);
            }
   
            // Only one audio stream can be selected
            for (int j = 0; j<availableAudioStreams.Count; j++)
            {
                if (availableAudioStreams[j].isChecked && (!isOneAudioSelected))
                {
                    selectedStreams.Add(availableAudioStreams[j].ManifestStream);
                    isOneAudioSelected = true;
                    txtStatus.Text = "hello audio stream is changed too" + availableAudioStreams[j].ManifestStream.Name;
                }
            }
   
            // Select hello frist audio stream from hello list if no audio steam is selected.
            if (!isOneAudioSelected)
            {
                availableAudioStreams[0].isChecked = true;
                selectedStreams.Add(availableAudioStreams[0].ManifestStream);
            }
   
            // Multiple text streams are supported.
            for (int j = 0; j < availableTextStreams.Count; j++)
            {
                if (availableTextStreams[j].isChecked)
                {
                    selectedStreams.Add(availableTextStreams[j].ManifestStream);
                }
            }
        }
   
        // Change streams on a smooth streaming presentation with multiple video streams.
        private async void changeStreams(List<IManifestStream> selectStreams)
        {
            try
            {
                IReadOnlyList<IStreamChangedResult> returnArgs =
                    await manifestObject.SelectStreamsAsync(selectStreams);
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }
        }
        #endregion stream selection
5. Localize o método de mediaElement_ManifestReady hello, acrescentar Olá código final Olá função hello a seguir:
   
        getStreams(manifestObject);
        refreshAvailableStreamsListBoxItemSource();
   
    Portanto ao manifesto MediaElement estiver pronto, Olá código obtém uma lista de fluxos de saudação disponíveis e preenche a caixa de listagem de interface do usuário Olá com lista de saudação.
6. Dentro de Olá classe MainPage, localize Olá botões de interface do usuário clique em eventos de região e adicione Olá definição de função a seguir:
   
        private void btnChangeStream_Click(object sender, RoutedEventArgs e)
        {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();
   
            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);
   
            // Change streams on hello presentation
            changeStreams(selectedStreams);
        }

**toocompile e testar o aplicativo hello**

1. Pressione **F6** toocompile projeto de saudação. 
2. Pressione **F5** aplicativo hello de toorun.
3. Na parte superior de saudação do aplicativo hello, você pode usar saudação padrão URL de Smooth Streaming ou insira outro. 
4. Clique em **Definir Origem**. 
5. idioma padrão de saudação é audio_eng. Tente tooswitch entre audio_eng e audio_es. Toda vez que, você seleciona um novo fluxo, clique botão de envio de saudação.

Você concluiu a lição 3.  Nesta lição, você deve adicionar fluxos de toochoose funcionalidade hello.

## <a name="lesson-4-select-smooth-streaming-tracks"></a>Lição 4: Selecionar faixas de Smooth Streaming
Um apresentação de Smooth Streaming pode conter vários arquivos de vídeo codificados com diferentes níveis de qualidade (taxas de bits) e resoluções. Nesta lição, você permite que usuários tooselect faixas. Esta lição contém Olá procedimentos a seguir:

1. Modificar o arquivo XAML de saudação
2. Modificar o arquivo de behand código Olá
3. Compilar e testar o aplicativo hello

**arquivo do toomodify Olá XAML**

1. No Gerenciador de Soluções, clique com o botão direito do mouse em **MainPage.xaml**, e, em seguida, clique em **Designer de Modos de Exibição**.
2. Localizar Olá &lt;grade&gt; marca com o nome da saudação **gridStreamAndBitrateSelection**, acrescente Olá código final Olá marca Olá a seguir:
   
         <StackPanel Name="spBitRateSelection" Grid.Row="1" Grid.Column="1">
         <StackPanel Orientation="Horizontal">
             <TextBlock Name="tbBitRate" Text="Available Bitrates:" FontSize="16" VerticalAlignment="Center"/>
             <Button Name="btnChangeTracks" Content="Submit" Click="btnChangeTrack_Click" />
         </StackPanel>
         <ListBox x:Name="lbAvailableVideoTracks" Height="200" Width="200" Background="Transparent" HorizontalAlignment="Left" 
                  ScrollViewer.VerticalScrollMode="Enabled" ScrollViewer.VerticalScrollBarVisibility="Visible">
             <ListBox.ItemTemplate>
                 <DataTemplate>
                     <CheckBox Content="{Binding Bitrate}" IsChecked="{Binding isChecked, Mode=TwoWay}"/>
                 </DataTemplate>
             </ListBox.ItemTemplate>
         </ListBox>
         </StackPanel>
3. Pressione **CTRL + S** toosave ele altera

**toomodify Olá arquivo code-behind**

1. No Gerenciador de Soluções, clique com o botão direito do mouse em **MainPage.xaml** e clique em **Exibir Código**.
2. Olá SSPlayer namespace, adicione uma nova classe:
   
        #region class Track
        public class Track
        {
            private IManifestTrack trackInfo;
            public string _bitrate;
            public bool isCheckedValue;
   
            public IManifestTrack TrackInfo
            {
                get { return trackInfo; }
                set { trackInfo = value; }
            }
   
            public string Bitrate
            {
                get { return _bitrate; }
                set { _bitrate = value; }
            }
   
            public bool isChecked
            {
                get { return isCheckedValue; }
                set
                {
                    isCheckedValue = value;
                }
            }
   
            public Track(IManifestTrack trackInfoIn)
            {
                trackInfo = trackInfoIn;
                _bitrate = trackInfoIn.Bitrate.ToString();
            }
            //public Track() { }
        }
        #endregion class Track
3. Início de saudação do hello classe MainPage, adicione Olá definições de variáveis a seguir:
   
        private List<Track> availableTracks;
4. Em Olá classe MainPage, adicione Olá região a seguir:
   
        #region track selection
        /// <summary>
        /// Functionality tooselect video streams
        /// </summary>
   
        /// This Function gets hello tracks for hello selected video stream
        public void getTracks(Manifest manifestObject)
        {
            availableTracks = new List<Track>();
   
            IManifestStream videoStream = getVideoStream();
            IReadOnlyList<IManifestTrack> availableTracksLocal = videoStream.AvailableTracks;
            IReadOnlyList<IManifestTrack> selectedTracksLocal = videoStream.SelectedTracks;
   
            try
            {
                for (int i = 0; i < availableTracksLocal.Count; i++)
                {
                    Track thisTrack = new Track(availableTracksLocal[i]);
                    thisTrack.isChecked = true;
   
                    for (int j = 0; j < selectedTracksLocal.Count; j++)
                    {
                        string selectedTrackName = selectedTracksLocal[j].Bitrate.ToString();
                        if (selectedTrackName.Equals(thisTrack.Bitrate))
                        {
                            thisTrack.isChecked = true;
                            break;
                        }
                    }
                    availableTracks.Add(thisTrack);
                }
            }
            catch (Exception e)
            {
                txtStatus.Text = e.Message;
            }
        }
   
        // This function gets hello video stream that is playing
        private IManifestStream getVideoStream()
        {
            IManifestStream videoStream = null;
            for (int i = 0; i < manifestObject.SelectedStreams.Count; i++)
            {
                if (manifestObject.SelectedStreams[i].Type == MediaStreamType.Video)
                {
                    videoStream = manifestObject.SelectedStreams[i];
                    break;
                }
            }
            return videoStream;
        }
   
        // This function set hello UI list box control ItemSource
        private async void refreshAvailableTracksListBoxItemSource()
        {
            try
            {
                // Update hello track check box list on hello UI 
                await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, ()
                    => { lbAvailableVideoTracks.ItemsSource = availableTracks; });
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }        
        }
   
        // This function creates a list of hello selected tracks.
        private void createSelectedTracksList(List<IManifestTrack> selectedTracks)
        {
            // Create a list of selected tracks
            for (int j = 0; j < availableTracks.Count; j++)
            {
                if (availableTracks[j].isCheckedValue == true)
                {
                    selectedTracks.Add(availableTracks[j].TrackInfo);
                }
            }
        }
   
        // This function selects hello tracks based on user selection 
        private void changeTracks(List<IManifestTrack> selectedTracks)
        {
            IManifestStream videoStream = getVideoStream();
            try
            {
                videoStream.SelectTracks(selectedTracks);
            }
            catch (Exception ex)
            {
                txtStatus.Text = ex.Message;
            }
        }
        #endregion track selection
5. Localize o método de mediaElement_ManifestReady hello, acrescentar Olá código final Olá função hello a seguir:
   
         getTracks(manifestObject);
         refreshAvailableTracksListBoxItemSource();
6. Dentro de Olá classe MainPage, localize Olá botões de interface do usuário clique em eventos de região e adicione Olá definição de função a seguir:
   
         private void btnChangeStream_Click(object sender, RoutedEventArgs e)
         {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();

            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);

            // Change streams on hello presentation
            changeStreams(selectedStreams);
         }

**toocompile e testar o aplicativo hello**

1. Pressione **F6** toocompile projeto de saudação. 
2. Pressione **F5** aplicativo hello de toorun.
3. Na parte superior de saudação do aplicativo hello, você pode usar saudação padrão URL de Smooth Streaming ou insira outro. 
4. Clique em **Definir Origem**. 
5. Por padrão, todas as faixas de saudação do fluxo de vídeo Olá são selecionadas. alterações de taxa de bits de tooexperiment hello, você pode selecionar hello mais baixa taxa de bits disponível e, em seguida, selecione hello mais alta taxa de bits disponível. Você deve clicar em Enviar após cada alteração.  Você pode ver as alterações de qualidade de vídeo hello.

Você concluiu a lição 4.  Nesta lição, você deve adicionar Olá funcionalidade toochoose faixas.

## <a name="media-services-learning-paths"></a>Roteiros de aprendizagem dos Serviços de Mídia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fornecer comentários
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="other-resources"></a>Outros recursos:
* [Como toobuild um aplicativo Smooth Streaming Windows 8 JavaScript com recursos avançados](http://blogs.iis.net/cenkd/archive/2012/08/10/how-to-build-a-smooth-streaming-windows-8-javascript-application-with-advanced-features.aspx)
* [Visão Geral Técnica de Smooth Streaming](http://www.iis.net/learn/media/on-demand-smooth-streaming/smooth-streaming-technical-overview)

[PlayerApplication]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-1.png
[CodeViewPic]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-2.png

