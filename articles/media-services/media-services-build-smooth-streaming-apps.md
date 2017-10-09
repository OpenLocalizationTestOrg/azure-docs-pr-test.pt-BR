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
# <a name="how-toobuild-a-smooth-streaming-windows-store-application"></a><span data-ttu-id="68bed-103">Como tooBuild um aplicativo Smooth Streaming Windows Store</span><span class="sxs-lookup"><span data-stu-id="68bed-103">How tooBuild a Smooth Streaming Windows Store Application</span></span>

<span data-ttu-id="68bed-104">Olá Smooth Streaming Client SDK para Windows 8 permite que os aplicativos da Windows Store toobuild os desenvolvedores que podem reproduzir o conteúdo de Smooth Streaming ao vivo e sob demanda.</span><span class="sxs-lookup"><span data-stu-id="68bed-104">hello Smooth Streaming Client SDK for Windows 8 enables developers toobuild Windows Store applications that can play on-demand and live Smooth Streaming content.</span></span> <span data-ttu-id="68bed-105">Além disso, toohello de reprodução básicas de Smooth Streaming de conteúdo, Olá SDK também fornece recursos avançados, como proteção do Microsoft PlayReady, restrição de nível de qualidade, Live DVR, fluxo de áudio alternando, escutando para atualizações de status (tais como alterações de nível de qualidade ) e eventos de erro e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="68bed-105">In addition toohello basic playback of Smooth Streaming content, hello SDK also provides rich features like Microsoft PlayReady protection, quality level restriction, Live DVR, audio stream switching, listening for status updates (such as quality level changes) and error events, and so on.</span></span> <span data-ttu-id="68bed-106">Para obter mais informações de recursos de saudação com suporte, consulte Olá [notas de versão](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes).</span><span class="sxs-lookup"><span data-stu-id="68bed-106">For more information of hello supported features, see hello [release notes](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes).</span></span> <span data-ttu-id="68bed-107">Para obter mais informações, consulte [Player Framework para Windows 8](http://playerframework.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="68bed-107">For more information, see [Player Framework for Windows 8](http://playerframework.codeplex.com/).</span></span> 

<span data-ttu-id="68bed-108">Este tutorial contém quatro lições:</span><span class="sxs-lookup"><span data-stu-id="68bed-108">This tutorial contains four lessons:</span></span>

1. <span data-ttu-id="68bed-109">Criar um aplicativo de armazenamento básico Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="68bed-109">Create a Basic Smooth Streaming Store Application</span></span>
2. <span data-ttu-id="68bed-110">Adicionar um controle deslizante barra tooControl Olá progresso de mídia</span><span class="sxs-lookup"><span data-stu-id="68bed-110">Add a Slider Bar tooControl hello Media Progress</span></span>
3. <span data-ttu-id="68bed-111">Selecionar fluxos do Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="68bed-111">Select Smooth Streaming Streams</span></span>
4. <span data-ttu-id="68bed-112">Selecionar faixas do Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="68bed-112">Select Smooth Streaming Tracks</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68bed-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="68bed-113">Prerequisites</span></span>
* <span data-ttu-id="68bed-114">Windows 8 32 bits ou 64 bits.</span><span class="sxs-lookup"><span data-stu-id="68bed-114">Windows 8 32-bit or 64-bit.</span></span> <span data-ttu-id="68bed-115">Você pode obter o [Windows 8 Enterprise Evaluation (a página pode estar em inglês)](http://msdn.microsoft.com/evalcenter/jj554510.aspx) no MSDN.</span><span class="sxs-lookup"><span data-stu-id="68bed-115">You can get [Windows 8 Enterprise Evaluation](http://msdn.microsoft.com/evalcenter/jj554510.aspx) from MSDN.</span></span>
* <span data-ttu-id="68bed-116">Visual Studio 2012 ou Visual Studio Express 2012 (ou versão posterior).</span><span class="sxs-lookup"><span data-stu-id="68bed-116">Visual Studio 2012 or Visual Studio Express 2012 (or a later version).</span></span> <span data-ttu-id="68bed-117">Você pode obter a versão de avaliação de saudação do [aqui](http://www.microsoft.com/visualstudio/11/downloads).</span><span class="sxs-lookup"><span data-stu-id="68bed-117">You can get hello trial version from [here](http://www.microsoft.com/visualstudio/11/downloads).</span></span>
* <span data-ttu-id="68bed-118">[SDK do Microsoft Smooth Streaming Client para Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home)</span><span class="sxs-lookup"><span data-stu-id="68bed-118">[Microsoft Smooth Streaming Client SDK for Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home).</span></span>

<span data-ttu-id="68bed-119">solução de saudação concluída para cada lição pode ser baixada de exemplos de código do MSDN Developer (Galeria de códigos):</span><span class="sxs-lookup"><span data-stu-id="68bed-119">hello completed solution for each lesson can be downloaded from MSDN Developer Code Samples (Code Gallery):</span></span> 

* <span data-ttu-id="68bed-120">[Lição 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) - Um Media Player simples de Smooth Streaming do Windows 8,</span><span class="sxs-lookup"><span data-stu-id="68bed-120">[Lesson 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) - A Simple Windows 8 Smooth Streaming Media Player,</span></span> 
* <span data-ttu-id="68bed-121">[Lição 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) - Um Media Player simples de Smooth Streaming do Windows 8 com um controle de barra deslizante,</span><span class="sxs-lookup"><span data-stu-id="68bed-121">[Lesson 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) - A Simple Windows 8 Smooth Streaming Media Player with a Slider Bar Control,</span></span> 
* <span data-ttu-id="68bed-122">[Lição 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) - Um Media Player simples de Smooth Streaming do Windows 8 com seleção de fluxo,</span><span class="sxs-lookup"><span data-stu-id="68bed-122">[Lesson 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) - A Windows 8 Smooth Streaming Media Player with Stream Selection,</span></span>  
* <span data-ttu-id="68bed-123">[Lição 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907) - um Media Player simples de Smooth Streaming do Windows 8 com seleção de faixa.</span><span class="sxs-lookup"><span data-stu-id="68bed-123">[Lesson 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907)  - A Windows 8 Smooth Streaming Media Player with Track Selection.</span></span>

## <a name="lesson-1-create-a-basic-smooth-streaming-store-application"></a><span data-ttu-id="68bed-124">Lição 1: Criar um aplicativo básico de Smooth Streaming para a Store</span><span class="sxs-lookup"><span data-stu-id="68bed-124">Lesson 1: Create a Basic Smooth Streaming Store Application</span></span>

<span data-ttu-id="68bed-125">Nesta lição, você criará um aplicativo da Windows Store com um MediaElement controle tooplay Smooth Stream conteúdo.</span><span class="sxs-lookup"><span data-stu-id="68bed-125">In this lesson, you will create a Windows Store application with a MediaElement control tooplay Smooth Stream content.</span></span>  <span data-ttu-id="68bed-126">aplicativo em execução Hello é semelhante a:</span><span class="sxs-lookup"><span data-stu-id="68bed-126">hello running application looks like:</span></span>

![Exemplo de aplicativo de Smooth Streaming da Windows Store][PlayerApplication]

<span data-ttu-id="68bed-128">Para obter mais informações sobre como desenvolver aplicativos da Windows Store, consulte [Desenvolver Ótimos Aplicativos para o Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx).</span><span class="sxs-lookup"><span data-stu-id="68bed-128">For more information on developing Windows Store application, see [Develop Great Apps for Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx).</span></span> <span data-ttu-id="68bed-129">Esta lição contém Olá procedimentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="68bed-129">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="68bed-130">Criar um novo projeto da Windows Store</span><span class="sxs-lookup"><span data-stu-id="68bed-130">Create a Windows Store project</span></span>
2. <span data-ttu-id="68bed-131">Interface de usuário do design hello (XAML)</span><span class="sxs-lookup"><span data-stu-id="68bed-131">Design hello user interface (XAML)</span></span>
3. <span data-ttu-id="68bed-132">Modificar Olá arquivo code-behind</span><span class="sxs-lookup"><span data-stu-id="68bed-132">Modify hello code behind file</span></span>
4. <span data-ttu-id="68bed-133">Compilar e testar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="68bed-133">Compile and test hello application</span></span>

<span data-ttu-id="68bed-134">**toocreate um projeto da Windows Store**</span><span class="sxs-lookup"><span data-stu-id="68bed-134">**toocreate a Windows Store project**</span></span>

1. <span data-ttu-id="68bed-135">Execute o Visual Studio 2012 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="68bed-135">Run Visual Studio 2012 or later.</span></span>
2. <span data-ttu-id="68bed-136">De saudação **arquivo** menu, clique em **novo**e, em seguida, clique em **projeto**.</span><span class="sxs-lookup"><span data-stu-id="68bed-136">From hello **FILE** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="68bed-137">Caixa de diálogo do novo projeto hello, tipo ou hello select a seguir valores:</span><span class="sxs-lookup"><span data-stu-id="68bed-137">From hello New Project dialog, type or select  hello following values:</span></span>

| <span data-ttu-id="68bed-138">Nome</span><span class="sxs-lookup"><span data-stu-id="68bed-138">Name</span></span> | <span data-ttu-id="68bed-139">Valor</span><span class="sxs-lookup"><span data-stu-id="68bed-139">Value</span></span> |
| --- | --- |
| <span data-ttu-id="68bed-140">Grupo de modelos</span><span class="sxs-lookup"><span data-stu-id="68bed-140">Template group</span></span> |<span data-ttu-id="68bed-141">Instalado/Modelos/Visual C#/Windows Store</span><span class="sxs-lookup"><span data-stu-id="68bed-141">Installed/Templates/Visual C#/Windows Store</span></span> |
| <span data-ttu-id="68bed-142">Modelo</span><span class="sxs-lookup"><span data-stu-id="68bed-142">Template</span></span> |<span data-ttu-id="68bed-143">Aplicativo em branco (XAML)</span><span class="sxs-lookup"><span data-stu-id="68bed-143">Blank App (XAML)</span></span> |
| <span data-ttu-id="68bed-144">Nome</span><span class="sxs-lookup"><span data-stu-id="68bed-144">Name</span></span> |<span data-ttu-id="68bed-145">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="68bed-145">SSPlayer</span></span> |
| <span data-ttu-id="68bed-146">Local</span><span class="sxs-lookup"><span data-stu-id="68bed-146">Location</span></span> |<span data-ttu-id="68bed-147">C:\SSTutorials</span><span class="sxs-lookup"><span data-stu-id="68bed-147">C:\SSTutorials</span></span> |
| <span data-ttu-id="68bed-148">Nome da solução</span><span class="sxs-lookup"><span data-stu-id="68bed-148">Solution Name</span></span> |<span data-ttu-id="68bed-149">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="68bed-149">SSPlayer</span></span> |
| <span data-ttu-id="68bed-150">Criar diretório para a solução</span><span class="sxs-lookup"><span data-stu-id="68bed-150">Create directory for solution</span></span> |<span data-ttu-id="68bed-151">(selecionado)</span><span class="sxs-lookup"><span data-stu-id="68bed-151">(selected)</span></span> |

1. <span data-ttu-id="68bed-152">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="68bed-152">Click **OK**.</span></span>

<span data-ttu-id="68bed-153">**tooadd toohello uma referência SDK de cliente Smooth Streaming**</span><span class="sxs-lookup"><span data-stu-id="68bed-153">**tooadd a reference toohello Smooth Streaming Client SDK**</span></span>

1. <span data-ttu-id="68bed-154">No Gerenciador de Soluções, clique com o botão direito do mouse em **SSPlayer** e, em seguida, clique em **Adicionar Referência**.</span><span class="sxs-lookup"><span data-stu-id="68bed-154">From Solution Explorer, right-click **SSPlayer**, and then click **Add Reference**.</span></span>
2. <span data-ttu-id="68bed-155">Digite ou selecione Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="68bed-155">Type or select hello following values:</span></span>

| <span data-ttu-id="68bed-156">Nome</span><span class="sxs-lookup"><span data-stu-id="68bed-156">Name</span></span> | <span data-ttu-id="68bed-157">Valor</span><span class="sxs-lookup"><span data-stu-id="68bed-157">Value</span></span> |
| --- | --- |
| <span data-ttu-id="68bed-158">Grupo de referências</span><span class="sxs-lookup"><span data-stu-id="68bed-158">Reference group</span></span> |<span data-ttu-id="68bed-159">Windows/Extensions</span><span class="sxs-lookup"><span data-stu-id="68bed-159">Windows/Extensions</span></span> |
| <span data-ttu-id="68bed-160">Referência</span><span class="sxs-lookup"><span data-stu-id="68bed-160">Reference</span></span> |<span data-ttu-id="68bed-161">Selecione SDK do Microsoft Smooth Streaming Client para Windows 8 e Pacote do Tempo de Execução do Microsoft Visual C++</span><span class="sxs-lookup"><span data-stu-id="68bed-161">Select Microsoft Smooth Streaming Client SDK for Windows 8 and Microsoft Visual C++ Runtime Package</span></span> |

1. <span data-ttu-id="68bed-162">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="68bed-162">Click **OK**.</span></span> 

<span data-ttu-id="68bed-163">Depois de adicionar referências Olá, você deve selecionar a plataforma Olá direcionado (x64 ou x86), adição de referências não funcionará para configuração de plataforma de qualquer CPU.</span><span class="sxs-lookup"><span data-stu-id="68bed-163">After adding hello references, you must select hello targeted platform (x64 or x86), adding references will not work for Any CPU platform configuration.</span></span>  <span data-ttu-id="68bed-164">No Gerenciador de Soluções, você verá a marca de aviso amarela para essas referências adicionadas.</span><span class="sxs-lookup"><span data-stu-id="68bed-164">In solution explorer, you will see yellow warning mark for these added references.</span></span>

<span data-ttu-id="68bed-165">**interface do usuário toodesign Olá player**</span><span class="sxs-lookup"><span data-stu-id="68bed-165">**toodesign hello player user interface**</span></span>

1. <span data-ttu-id="68bed-166">No Gerenciador de soluções, clique duas vezes em **MainPage. XAML** tooopen-lo no design Olá exibir.</span><span class="sxs-lookup"><span data-stu-id="68bed-166">From Solution Explorer, double click **MainPage.xaml** tooopen it in hello design view.</span></span>
2. <span data-ttu-id="68bed-167">Localizar Olá  **&lt;grade&gt;**  e  **&lt;/Grid&gt;**  marcas Olá arquivo XAML e código a seguir de saudação colar entre as marcas de saudação dois:</span><span class="sxs-lookup"><span data-stu-id="68bed-167">Locate hello **&lt;Grid&gt;** and **&lt;/Grid&gt;**  tags hello XAML file, and paste hello following code between hello two tags:</span></span>

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
   
   <span data-ttu-id="68bed-168">Olá controle MediaElement é uma mídia tooplayback usado.</span><span class="sxs-lookup"><span data-stu-id="68bed-168">hello MediaElement control is used tooplayback media.</span></span> <span data-ttu-id="68bed-169">controle deslizante de saudação denominado sliderProgress será usado em andamento Olá próximo lição toocontrol Olá mídia.</span><span class="sxs-lookup"><span data-stu-id="68bed-169">hello slider control named sliderProgress will be used in hello next lesson toocontrol hello media progress.</span></span>
3. <span data-ttu-id="68bed-170">Pressione **CTRL + S** toosave arquivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="68bed-170">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="68bed-171">Olá controle MediaElement não oferece suporte a Streaming suave conteúda fora da caixa.</span><span class="sxs-lookup"><span data-stu-id="68bed-171">hello MediaElement control does not support Smooth Streaming content out-of-box.</span></span> <span data-ttu-id="68bed-172">suporte de Smooth Streaming de saudação de tooenable, você deve registrar o manipulador de Olá fluxo de bytes Smooth Streaming pela extensão de nome de arquivo e o tipo MIME.</span><span class="sxs-lookup"><span data-stu-id="68bed-172">tooenable hello Smooth Streaming support, you must register hello Smooth Streaming byte-stream handler by file name extension and MIME type.</span></span>  <span data-ttu-id="68bed-173">tooregister, você usar o método MediaExtensionManager.RegisterByteStremHandler Olá Olá botão namespace.</span><span class="sxs-lookup"><span data-stu-id="68bed-173">tooregister, you use hello MediaExtensionManager.RegisterByteStremHandler method of hello Windows.Media namespace.</span></span>

<span data-ttu-id="68bed-174">Esse arquivo XAML, alguns manipuladores de eventos são associados com controles de saudação.</span><span class="sxs-lookup"><span data-stu-id="68bed-174">In this XAML file, some event handlers are associated with hello controls.</span></span>  <span data-ttu-id="68bed-175">Você deve definir esses manipuladores de eventos.</span><span class="sxs-lookup"><span data-stu-id="68bed-175">You must define those event handlers.</span></span>

<span data-ttu-id="68bed-176">**toomodify Olá arquivo code-behind**</span><span class="sxs-lookup"><span data-stu-id="68bed-176">**toomodify hello code behind file**</span></span>

1. <span data-ttu-id="68bed-177">No Gerenciador de Soluções, clique com o botão direito do mouse em **MainPage.xaml** e clique em **Exibir Código**.</span><span class="sxs-lookup"><span data-stu-id="68bed-177">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="68bed-178">Na parte superior de saudação do arquivo hello, adicione o seguinte de saudação usando a instrução:</span><span class="sxs-lookup"><span data-stu-id="68bed-178">At hello top of hello file, add hello following using statement:</span></span>
   
        using Windows.Media;
3. <span data-ttu-id="68bed-179">Início de saudação do hello **MainPage** classe, adicione Olá membro de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="68bed-179">At hello beginning of hello **MainPage** class, add hello following data member:</span></span>
   
         private MediaExtensionManager extensions = new MediaExtensionManager();
4. <span data-ttu-id="68bed-180">No final de saudação do hello **MainPage** construtor, adicionar Olá duas linhas a seguir:</span><span class="sxs-lookup"><span data-stu-id="68bed-180">At hello end of hello **MainPage** constructor, add hello following two lines:</span></span>
   
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "text/xml");
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "application/vnd.ms-sstr+xml");
5. <span data-ttu-id="68bed-181">No final de saudação do hello **MainPage** classe, cole Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="68bed-181">At hello end of hello **MainPage** class, paste hello following code:</span></span>
   
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

<span data-ttu-id="68bed-182">manipulador de eventos sliderProgress_PointerPressed Olá é definido aqui.</span><span class="sxs-lookup"><span data-stu-id="68bed-182">hello sliderProgress_PointerPressed event handler is defined here.</span></span>  <span data-ttu-id="68bed-183">Há mais tooget de toodo funciona trabalhando, que será abordado na próxima lição Olá deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="68bed-183">There are more works toodo tooget it working, which will be covered in hello next lesson of this tutorial.</span></span>
6. <span data-ttu-id="68bed-184">Pressione **CTRL + S** toosave arquivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="68bed-184">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="68bed-185">Hello Olá terminar arquivo code-behind deve ser assim:</span><span class="sxs-lookup"><span data-stu-id="68bed-185">hello finished hello code behind file shall look like this:</span></span>

![Exibição do código no Visual Studio do aplicativo de Smooth Streaming da Windows Store][CodeViewPic]

<span data-ttu-id="68bed-187">**toocompile e testar o aplicativo hello**</span><span class="sxs-lookup"><span data-stu-id="68bed-187">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="68bed-188">De saudação **criar** menu, clique em **do Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="68bed-188">From hello **BUILD** menu, click **Configuration Manager**.</span></span>
2. <span data-ttu-id="68bed-189">Alterar **plataforma de solução ativa** toomatch sua plataforma de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="68bed-189">Change **Active solution platform** toomatch your development platform.</span></span>
3. <span data-ttu-id="68bed-190">Pressione **F6** toocompile projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="68bed-190">Press **F6** toocompile hello project.</span></span> 
4. <span data-ttu-id="68bed-191">Pressione **F5** aplicativo hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="68bed-191">Press **F5** toorun hello application.</span></span>
5. <span data-ttu-id="68bed-192">Na parte superior de saudação do aplicativo hello, você pode usar saudação padrão URL de Smooth Streaming ou insira outro.</span><span class="sxs-lookup"><span data-stu-id="68bed-192">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
6. <span data-ttu-id="68bed-193">Clique em **Definir Origem**.</span><span class="sxs-lookup"><span data-stu-id="68bed-193">Click **Set Source**.</span></span> <span data-ttu-id="68bed-194">Porque **reprodução automática** é habilitado por padrão, Olá reprodutor de mídia será automaticamente.</span><span class="sxs-lookup"><span data-stu-id="68bed-194">Because **Auto Play** is enabled by default, hello media shall play automatically.</span></span>  <span data-ttu-id="68bed-195">Você pode controlar a mídia de saudação usando Olá **reproduzir**, **pausar** e **parar** botões.</span><span class="sxs-lookup"><span data-stu-id="68bed-195">You can control hello media using hello **Play**, **Pause** and **Stop** buttons.</span></span>  <span data-ttu-id="68bed-196">Você pode controlar o volume de mídia hello usando slider vertical hello.</span><span class="sxs-lookup"><span data-stu-id="68bed-196">You can control hello media volume using hello vertical slider.</span></span>  <span data-ttu-id="68bed-197">No entanto, Olá horizontal controle deslizante para controlar Olá andamento da mídia ainda não está totalmente implementado.</span><span class="sxs-lookup"><span data-stu-id="68bed-197">However hello horizontal slider for controlling hello media progress is not fully implemented yet.</span></span> 

<span data-ttu-id="68bed-198">Você concluiu a Lição 1.</span><span class="sxs-lookup"><span data-stu-id="68bed-198">You have completed lesson1.</span></span>  <span data-ttu-id="68bed-199">Nesta lição, você deve usar um controle de MediaElement tooplayback conteúdo de Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="68bed-199">In this lesson, you use a MediaElement control tooplayback Smooth Streaming content.</span></span>  <span data-ttu-id="68bed-200">Próxima hello, você adicionará um progresso do controle deslizante toocontrol Olá de saudação conteúdo Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="68bed-200">In hello next lesson, you will add a slider toocontrol hello progress of hello Smooth Streaming content.</span></span>

## <a name="lesson-2-add-a-slider-bar-toocontrol-hello-media-progress"></a><span data-ttu-id="68bed-201">Lição 2: Adicionar um controle deslizante barra tooControl Olá progresso de mídia</span><span class="sxs-lookup"><span data-stu-id="68bed-201">Lesson 2: Add a Slider Bar tooControl hello Media Progress</span></span>

<span data-ttu-id="68bed-202">Na lição 1, você criou um aplicativo da Windows Store com um controle de MediaElement XAML tooplayback conteúdo Smooth Streaming de mídia.</span><span class="sxs-lookup"><span data-stu-id="68bed-202">In lesson 1, you created a Windows Store application with a MediaElement XAML control tooplayback Smooth Streaming media content.</span></span>  <span data-ttu-id="68bed-203">Ele vem com algumas funções básicas de mídia, como iniciar, parar e pausar.</span><span class="sxs-lookup"><span data-stu-id="68bed-203">It comes some basic media functions like start, stop and pause.</span></span>  <span data-ttu-id="68bed-204">Nesta lição, você adicionará um aplicativo toohello de controle de barra de controle deslizante.</span><span class="sxs-lookup"><span data-stu-id="68bed-204">In this lesson, you will add a slider bar control toohello application.</span></span>

<span data-ttu-id="68bed-205">Neste tutorial, usaremos uma posição de controle deslizante de saudação do timer tooupdate com base na posição atual de saudação do hello controle MediaElement.</span><span class="sxs-lookup"><span data-stu-id="68bed-205">In this tutorial, we will use a timer tooupdate hello slider position based on hello current position of hello MediaElement control.</span></span>  <span data-ttu-id="68bed-206">controle deslizante de saudação início e hora de término também toobe necessidade atualizado em caso de conteúdo ao vivo.</span><span class="sxs-lookup"><span data-stu-id="68bed-206">hello slider start and end time also need toobe updated in case of live content.</span></span>  <span data-ttu-id="68bed-207">Isso pode ser melhor tratado no evento de atualização de origem adaptável hello.</span><span class="sxs-lookup"><span data-stu-id="68bed-207">This can be better handled in hello adaptive source update event.</span></span>

<span data-ttu-id="68bed-208">As origens de mídia são objetos que geram dados de mídia.</span><span class="sxs-lookup"><span data-stu-id="68bed-208">Media sources are objects that generate media data.</span></span>  <span data-ttu-id="68bed-209">resolvedor de origem Olá leva um fluxo de bytes ou de URL e cria Olá mídia adequada fonte desse conteúdo.</span><span class="sxs-lookup"><span data-stu-id="68bed-209">hello source resolver takes a URL or byte stream and creates hello appropriate media source for that content.</span></span>  <span data-ttu-id="68bed-210">resolvedor de origem Olá é forma padrão de saudação para fontes de mídia Olá aplicativos toocreate.</span><span class="sxs-lookup"><span data-stu-id="68bed-210">hello source resolver is hello standard way for hello applications toocreate media sources.</span></span> 

<span data-ttu-id="68bed-211">Esta lição contém Olá procedimentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="68bed-211">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="68bed-212">Registrar o manipulador de Smooth Streaming Olá</span><span class="sxs-lookup"><span data-stu-id="68bed-212">Register hello Smooth Streaming handler</span></span> 
2. <span data-ttu-id="68bed-213">Adicionar manipuladores de eventos de nível de Gerenciador de fonte adaptável de Olá</span><span class="sxs-lookup"><span data-stu-id="68bed-213">Add hello adaptive source manager level event handlers</span></span>
3. <span data-ttu-id="68bed-214">Adicionar manipuladores de eventos no nível de fonte adaptável Olá</span><span class="sxs-lookup"><span data-stu-id="68bed-214">Add hello adaptive source level event handlers</span></span>
4. <span data-ttu-id="68bed-215">Adicionar manipuladores de eventos de MediaElement</span><span class="sxs-lookup"><span data-stu-id="68bed-215">Add MediaElement event handlers</span></span>
5. <span data-ttu-id="68bed-216">Adicionar o código relacionado à barra de controle deslizante</span><span class="sxs-lookup"><span data-stu-id="68bed-216">Add slider bar related code</span></span>
6. <span data-ttu-id="68bed-217">Compilar e testar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="68bed-217">Compile and test hello application</span></span>

<span data-ttu-id="68bed-218">**tooregister Olá fluxo de bytes Smooth Streaming manipulador e passe Olá propertyset**</span><span class="sxs-lookup"><span data-stu-id="68bed-218">**tooregister hello Smooth Streaming byte-stream handler and pass hello propertyset**</span></span>

1. <span data-ttu-id="68bed-219">No Gerenciador de Soluções, clique com o botão direito do mouse em **MainPage.xaml** e clique em **Exibir Código**.</span><span class="sxs-lookup"><span data-stu-id="68bed-219">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="68bed-220">Início de saudação do arquivo hello, adicione o seguinte de saudação usando a instrução:</span><span class="sxs-lookup"><span data-stu-id="68bed-220">At hello beginning of hello file, add hello following using statement:</span></span>

        using Microsoft.Media.AdaptiveStreaming;
3. <span data-ttu-id="68bed-221">Início de saudação do hello classe MainPage, adicione Olá membros de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="68bed-221">At hello beginning of hello MainPage class, add hello following data members:</span></span>

         private Windows.Foundation.Collections.PropertySet propertySet = new Windows.Foundation.Collections.PropertySet();             
         private IAdaptiveSourceManager adaptiveSourceManager;
4. <span data-ttu-id="68bed-222">Olá interna **MainPage** construtor, adicionar Olá código a seguir após Olá **isso. Inicializar Components();**  linha e linhas de código de registro Olá gravadas na lição anterior hello:</span><span class="sxs-lookup"><span data-stu-id="68bed-222">Inside hello **MainPage** constructor, add hello following code after hello **this.Initialize Components();** line and hello registration code lines written in hello previous lesson:</span></span>

        // Gets hello default instance of AdaptiveSourceManager which manages Smooth 
        //Streaming media sources.
        adaptiveSourceManager = AdaptiveSourceManager.GetDefault();
        // Sets property key value tooAdaptiveSourceManager default instance.
        // {A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}" must be hardcoded.
        propertySet["{A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}"] = adaptiveSourceManager;
5. <span data-ttu-id="68bed-223">Olá interna **MainPage** construtor, modificar a saudação do hello dois RegisterByteStreamHandler métodos tooadd sucessivamente parâmetros:</span><span class="sxs-lookup"><span data-stu-id="68bed-223">Inside hello **MainPage** constructor, modify hello two RegisterByteStreamHandler methods tooadd hello forth parameters:</span></span>

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
6. <span data-ttu-id="68bed-224">Pressione **CTRL + S** toosave arquivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="68bed-224">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="68bed-225">**manipulador de eventos no nível do tooadd Olá fonte adaptável manager**</span><span class="sxs-lookup"><span data-stu-id="68bed-225">**tooadd hello adaptive source manager level event handler**</span></span>

1. <span data-ttu-id="68bed-226">No Gerenciador de Soluções, clique com o botão direito do mouse em **MainPage.xaml** e clique em **Exibir Código**.</span><span class="sxs-lookup"><span data-stu-id="68bed-226">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="68bed-227">Olá interna **MainPage** classe, adicione Olá membro de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="68bed-227">Inside hello **MainPage** class, add hello following data member:</span></span>
   
     <span data-ttu-id="68bed-228">private AdaptiveSource adaptiveSource = null;</span><span class="sxs-lookup"><span data-stu-id="68bed-228">private AdaptiveSource adaptiveSource = null;</span></span>
3. <span data-ttu-id="68bed-229">No final de saudação do hello **MainPage** classe, adicione Olá manipulador de eventos a seguir:</span><span class="sxs-lookup"><span data-stu-id="68bed-229">At hello end of hello **MainPage** class, add hello following event handler:</span></span>
   
         # region Adaptive Source Manager Level Events
         private void mediaElement_AdaptiveSourceOpened(AdaptiveSource sender, AdaptiveSourceOpenedEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
         }

         # endregion Adaptive Source Manager Level Events
4. <span data-ttu-id="68bed-230">No final de saudação do hello **MainPage** construtor, adicionar Olá linha toosubscribe toohello adaptável fonte aberta de evento a seguir:</span><span class="sxs-lookup"><span data-stu-id="68bed-230">At hello end of hello **MainPage** constructor, add hello following line toosubscribe toohello adaptive source open event:</span></span>
   
         adaptiveSourceManager.AdaptiveSourceOpenedEvent += 
           new AdaptiveSourceOpenedEventHandler(mediaElement_AdaptiveSourceOpened);
5. <span data-ttu-id="68bed-231">Pressione **CTRL + S** toosave arquivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="68bed-231">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="68bed-232">**manipuladores de eventos no nível de fonte adaptável tooadd**</span><span class="sxs-lookup"><span data-stu-id="68bed-232">**tooadd adaptive source level event handlers**</span></span>

1. <span data-ttu-id="68bed-233">No Gerenciador de Soluções, clique com o botão direito do mouse em **MainPage.xaml** e clique em **Exibir Código**.</span><span class="sxs-lookup"><span data-stu-id="68bed-233">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="68bed-234">Olá interna **MainPage** classe, adicione Olá membro de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="68bed-234">Inside hello **MainPage** class, add hello following data member:</span></span>
   
     <span data-ttu-id="68bed-235">private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;</span><span class="sxs-lookup"><span data-stu-id="68bed-235">private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;</span></span>
3. <span data-ttu-id="68bed-236">No final de saudação do hello **MainPage** classe, adicione Olá manipuladores de eventos a seguir:</span><span class="sxs-lookup"><span data-stu-id="68bed-236">At hello end of hello **MainPage** class, add hello following event handlers:</span></span>

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
4. <span data-ttu-id="68bed-237">No final de saudação do hello **mediaElement AdaptiveSourceOpened** método, adicione Olá eventos de toohello de toosubscribe de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="68bed-237">At hello end of hello **mediaElement AdaptiveSourceOpened** method, add hello following code toosubscribe toohello events:</span></span>
   
         adaptiveSource.ManifestReadyEvent +=

                    mediaElement_ManifestReady;
         adaptiveSource.AdaptiveSourceStatusUpdatedEvent += 

            mediaElement_AdaptiveSourceStatusUpdated;
         adaptiveSource.AdaptiveSourceFailedEvent += 

            mediaElement_AdaptiveSourceFailed;
5. <span data-ttu-id="68bed-238">Pressione **CTRL + S** toosave arquivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="68bed-238">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="68bed-239">Olá mesmos eventos estão disponíveis na fonte adaptável Manager nível, que pode ser usado para tratar aos elementos de mídia comuns tooall de funcionalidade no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="68bed-239">hello same events are available on Adaptive Source manger level as well, which can be used for handling functionality common tooall media elements in hello app.</span></span> <span data-ttu-id="68bed-240">Cada AdaptiveSource inclui seus próprios eventos e todos os eventos de AdaptiveSource serão colocados em cascata no AdaptiveSourceManager.</span><span class="sxs-lookup"><span data-stu-id="68bed-240">Each AdaptiveSource includes its own events and all AdaptiveSource events will be cascaded under AdaptiveSourceManager.</span></span>

<span data-ttu-id="68bed-241">**manipuladores de eventos do elemento de mídia tooadd**</span><span class="sxs-lookup"><span data-stu-id="68bed-241">**tooadd Media Element event handlers**</span></span>

1. <span data-ttu-id="68bed-242">No Gerenciador de Soluções, clique com o botão direito do mouse em **MainPage.xaml** e clique em **Exibir Código**.</span><span class="sxs-lookup"><span data-stu-id="68bed-242">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="68bed-243">No final de saudação do hello **MainPage** classe, adicione Olá manipuladores de eventos a seguir:</span><span class="sxs-lookup"><span data-stu-id="68bed-243">At hello end of hello **MainPage** class, add hello following event handlers:</span></span>

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
3. <span data-ttu-id="68bed-244">No final de saudação do hello **MainPage** construtor, adicionar Olá eventos de toohello de toosubscript de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="68bed-244">At hello end of hello **MainPage** constructor, add hello following code toosubscript toohello events:</span></span>

         mediaElement.MediaOpened += MediaOpened;
         mediaElement.MediaEnded += MediaEnded;
         mediaElement.MediaFailed += MediaFailed;
4. <span data-ttu-id="68bed-245">Pressione **CTRL + S** toosave arquivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="68bed-245">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="68bed-246">**controle deslizante de tooadd relacionado código de barras**</span><span class="sxs-lookup"><span data-stu-id="68bed-246">**tooadd slider bar related code**</span></span>

1. <span data-ttu-id="68bed-247">No Gerenciador de Soluções, clique com o botão direito do mouse em **MainPage.xaml** e clique em **Exibir Código**.</span><span class="sxs-lookup"><span data-stu-id="68bed-247">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="68bed-248">Início de saudação do arquivo hello, adicione o seguinte de saudação usando a instrução:</span><span class="sxs-lookup"><span data-stu-id="68bed-248">At hello beginning of hello file, add hello following using statement:</span></span>
      
        using Windows.UI.Core;
3. <span data-ttu-id="68bed-249">Olá interna **MainPage** classe, adicione Olá membros de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="68bed-249">Inside hello **MainPage** class, add hello following data members:</span></span>
   
         public static CoreDispatcher _dispatcher;
         private DispatcherTimer sliderPositionUpdateDispatcher;
4. <span data-ttu-id="68bed-250">No final de saudação do hello **MainPage** construtor, adicionar Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="68bed-250">At hello end of hello **MainPage** constructor, add hello following code:</span></span>
   
         _dispatcher = Window.Current.Dispatcher;
         PointerEventHandler pointerpressedhandler = new PointerEventHandler(sliderProgress_PointerPressed);
         sliderProgress.AddHandler(Control.PointerPressedEvent, pointerpressedhandler, true);    
5. <span data-ttu-id="68bed-251">No final de saudação do hello **MainPage** classe, adicione Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="68bed-251">At hello end of hello **MainPage** class, add hello following code:</span></span>

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
><span data-ttu-id="68bed-252">CoreDispatcher é usado toomake alterações toohello da interface do usuário do thread de Thread de interface do usuário não.</span><span class="sxs-lookup"><span data-stu-id="68bed-252">CoreDispatcher is used toomake changes toohello UI thread from non UI Thread.</span></span> <span data-ttu-id="68bed-253">No caso de afunilamento no thread do distribuidor, o desenvolvedor pode escolher toouse dispatcher fornecido pelo elemento de interface do usuário que ele pretenda tooupdate.</span><span class="sxs-lookup"><span data-stu-id="68bed-253">In case of bottleneck on dispatcher thread, developer can choose toouse dispatcher provided by UI-element he/she intends tooupdate.</span></span>  <span data-ttu-id="68bed-254">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="68bed-254">For example:</span></span>
   
         await sliderProgress.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () => { TimeSpan 

         timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime); 
         double absvalue  = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero); 

         sliderProgress.Maximum = absvalue; }); 
6. <span data-ttu-id="68bed-255">No final de saudação do hello **mediaElement_AdaptiveSourceStatusUpdated** método, adicione Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="68bed-255">At hello end of hello **mediaElement_AdaptiveSourceStatusUpdated** method, add hello following code:</span></span>

         setSliderStartTime(args.StartTime);
         setSliderEndTime(args.EndTime);
7. <span data-ttu-id="68bed-256">No final de saudação do hello **MediaOpened** método, adicione Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="68bed-256">At hello end of hello **MediaOpened** method, add hello following code:</span></span>

         sliderProgress.StepFrequency = SliderFrequency(mediaElement.NaturalDuration.TimeSpan);
         sliderProgress.Width = mediaElement.Width;
         setupTimer();
8. <span data-ttu-id="68bed-257">Pressione **CTRL + S** toosave arquivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="68bed-257">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="68bed-258">**toocompile e testar o aplicativo hello**</span><span class="sxs-lookup"><span data-stu-id="68bed-258">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="68bed-259">Pressione **F6** toocompile projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="68bed-259">Press **F6** toocompile hello project.</span></span> 
2. <span data-ttu-id="68bed-260">Pressione **F5** aplicativo hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="68bed-260">Press **F5** toorun hello application.</span></span>
3. <span data-ttu-id="68bed-261">Na parte superior de saudação do aplicativo hello, você pode usar saudação padrão URL de Smooth Streaming ou insira outro.</span><span class="sxs-lookup"><span data-stu-id="68bed-261">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="68bed-262">Clique em **Definir Origem**.</span><span class="sxs-lookup"><span data-stu-id="68bed-262">Click **Set Source**.</span></span> 
5. <span data-ttu-id="68bed-263">Barra de controle deslizante de saudação do teste.</span><span class="sxs-lookup"><span data-stu-id="68bed-263">Test hello slider bar.</span></span>

<span data-ttu-id="68bed-264">Você concluiu a lição 2.</span><span class="sxs-lookup"><span data-stu-id="68bed-264">You have completed lesson 2.</span></span>  <span data-ttu-id="68bed-265">Nesta lição, você adicionou um controle deslizante tooapplication.</span><span class="sxs-lookup"><span data-stu-id="68bed-265">In this lesson you added a slider tooapplication.</span></span> 

## <a name="lesson-3-select-smooth-streaming-streams"></a><span data-ttu-id="68bed-266">Lição 3: Selecionar fluxos de Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="68bed-266">Lesson 3: Select Smooth Streaming Streams</span></span>
<span data-ttu-id="68bed-267">Smooth Streaming é toostream compatível com conteúdo com várias faixas de áudio de idioma que são selecionáveis visualizadores hello.</span><span class="sxs-lookup"><span data-stu-id="68bed-267">Smooth Streaming is capable toostream content with multiple language audio tracks that are selectable by hello viewers.</span></span>  <span data-ttu-id="68bed-268">Nesta lição, você habilitará fluxos de tooselect visualizadores.</span><span class="sxs-lookup"><span data-stu-id="68bed-268">In this lesson, you will enable viewers tooselect streams.</span></span> <span data-ttu-id="68bed-269">Esta lição contém Olá procedimentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="68bed-269">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="68bed-270">Modificar o arquivo XAML de saudação</span><span class="sxs-lookup"><span data-stu-id="68bed-270">Modify hello XAML file</span></span>
2. <span data-ttu-id="68bed-271">Modificar o arquivo de behand código Olá</span><span class="sxs-lookup"><span data-stu-id="68bed-271">Modify hello code behand file</span></span>
3. <span data-ttu-id="68bed-272">Compilar e testar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="68bed-272">Compile and test hello application</span></span>

<span data-ttu-id="68bed-273">**arquivo do toomodify Olá XAML**</span><span class="sxs-lookup"><span data-stu-id="68bed-273">**toomodify hello XAML file**</span></span>

1. <span data-ttu-id="68bed-274">No Gerenciador de Soluções, clique com o botão direito do mouse em **MainPage.xaml**, e, em seguida, clique em **Designer de Modos de Exibição**.</span><span class="sxs-lookup"><span data-stu-id="68bed-274">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="68bed-275">Localize &lt;Grid.RowDefinitions&gt;e modificar Olá RowDefinitions para que eles se parece com:</span><span class="sxs-lookup"><span data-stu-id="68bed-275">Locate &lt;Grid.RowDefinitions&gt;, and modify hello RowDefinitions so they looks like:</span></span>
   
         <Grid.RowDefinitions>            
            <RowDefinition Height="20"/>
            <RowDefinition Height="50"/>
            <RowDefinition Height="100"/>
            <RowDefinition Height="80"/>
            <RowDefinition Height="50"/>
         </Grid.RowDefinitions>
3. <span data-ttu-id="68bed-276">Olá interna &lt;grade&gt;&lt;/Grid&gt; marcas, adicione a saudação de código a seguir toodefine um controle listbox, para que os usuários podem ver Olá lista de fluxos disponíveis e selecione fluxos:</span><span class="sxs-lookup"><span data-stu-id="68bed-276">Inside hello &lt;Grid&gt;&lt;/Grid&gt; tags, add hello following code toodefine a listbox control, so users can see hello list of available streams, and select streams:</span></span>

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
4. <span data-ttu-id="68bed-277">Pressione **CTRL + S** toosave alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="68bed-277">Press **CTRL+S** toosave hello changes.</span></span>

<span data-ttu-id="68bed-278">**toomodify Olá arquivo code-behind**</span><span class="sxs-lookup"><span data-stu-id="68bed-278">**toomodify hello code behind file**</span></span>

1. <span data-ttu-id="68bed-279">No Gerenciador de Soluções, clique com o botão direito do mouse em **MainPage.xaml** e clique em **Exibir Código**.</span><span class="sxs-lookup"><span data-stu-id="68bed-279">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="68bed-280">Olá SSPlayer namespace, adicione uma nova classe:</span><span class="sxs-lookup"><span data-stu-id="68bed-280">Inside hello SSPlayer namespace, add a new class:</span></span>
   
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
3. <span data-ttu-id="68bed-281">Início de saudação do hello classe MainPage, adicione Olá definições de variáveis a seguir:</span><span class="sxs-lookup"><span data-stu-id="68bed-281">At hello beginning of hello MainPage class, add hello following variable definitions:</span></span>
   
         private List<Stream> availableStreams;
         private List<Stream> availableAudioStreams;
         private List<Stream> availableTextStreams;
         private List<Stream> availableVideoStreams;
4. <span data-ttu-id="68bed-282">Em Olá classe MainPage, adicione Olá região a seguir:</span><span class="sxs-lookup"><span data-stu-id="68bed-282">Inside hello MainPage class, add hello following region:</span></span>
   
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
5. <span data-ttu-id="68bed-283">Localize o método de mediaElement_ManifestReady hello, acrescentar Olá código final Olá função hello a seguir:</span><span class="sxs-lookup"><span data-stu-id="68bed-283">Locate hello mediaElement_ManifestReady method, append hello following code at hello end of hello function:</span></span>
   
        getStreams(manifestObject);
        refreshAvailableStreamsListBoxItemSource();
   
    <span data-ttu-id="68bed-284">Portanto ao manifesto MediaElement estiver pronto, Olá código obtém uma lista de fluxos de saudação disponíveis e preenche a caixa de listagem de interface do usuário Olá com lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="68bed-284">So when MediaElement manifest is ready, hello code gets a list of hello available streams, and populates hello UI list box with hello list.</span></span>
6. <span data-ttu-id="68bed-285">Dentro de Olá classe MainPage, localize Olá botões de interface do usuário clique em eventos de região e adicione Olá definição de função a seguir:</span><span class="sxs-lookup"><span data-stu-id="68bed-285">Inside hello MainPage class, locate hello UI buttons click events region, and then add hello following function definition:</span></span>
   
        private void btnChangeStream_Click(object sender, RoutedEventArgs e)
        {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();
   
            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);
   
            // Change streams on hello presentation
            changeStreams(selectedStreams);
        }

<span data-ttu-id="68bed-286">**toocompile e testar o aplicativo hello**</span><span class="sxs-lookup"><span data-stu-id="68bed-286">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="68bed-287">Pressione **F6** toocompile projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="68bed-287">Press **F6** toocompile hello project.</span></span> 
2. <span data-ttu-id="68bed-288">Pressione **F5** aplicativo hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="68bed-288">Press **F5** toorun hello application.</span></span>
3. <span data-ttu-id="68bed-289">Na parte superior de saudação do aplicativo hello, você pode usar saudação padrão URL de Smooth Streaming ou insira outro.</span><span class="sxs-lookup"><span data-stu-id="68bed-289">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="68bed-290">Clique em **Definir Origem**.</span><span class="sxs-lookup"><span data-stu-id="68bed-290">Click **Set Source**.</span></span> 
5. <span data-ttu-id="68bed-291">idioma padrão de saudação é audio_eng.</span><span class="sxs-lookup"><span data-stu-id="68bed-291">hello default language is audio_eng.</span></span> <span data-ttu-id="68bed-292">Tente tooswitch entre audio_eng e audio_es.</span><span class="sxs-lookup"><span data-stu-id="68bed-292">Try tooswitch between audio_eng and audio_es.</span></span> <span data-ttu-id="68bed-293">Toda vez que, você seleciona um novo fluxo, clique botão de envio de saudação.</span><span class="sxs-lookup"><span data-stu-id="68bed-293">Everytime, you select a new stream, you must click hello Submit button.</span></span>

<span data-ttu-id="68bed-294">Você concluiu a lição 3.</span><span class="sxs-lookup"><span data-stu-id="68bed-294">You have completed lesson 3.</span></span>  <span data-ttu-id="68bed-295">Nesta lição, você deve adicionar fluxos de toochoose funcionalidade hello.</span><span class="sxs-lookup"><span data-stu-id="68bed-295">In this lesson, you add hello functionality toochoose streams.</span></span>

## <a name="lesson-4-select-smooth-streaming-tracks"></a><span data-ttu-id="68bed-296">Lição 4: Selecionar faixas de Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="68bed-296">Lesson 4: Select Smooth Streaming Tracks</span></span>
<span data-ttu-id="68bed-297">Um apresentação de Smooth Streaming pode conter vários arquivos de vídeo codificados com diferentes níveis de qualidade (taxas de bits) e resoluções.</span><span class="sxs-lookup"><span data-stu-id="68bed-297">A Smooth Streaming presentation can contain multiple video files encoded with different quality levels (bit rates) and resolutions.</span></span> <span data-ttu-id="68bed-298">Nesta lição, você permite que usuários tooselect faixas.</span><span class="sxs-lookup"><span data-stu-id="68bed-298">In this lesson, you will enable users tooselect tracks.</span></span> <span data-ttu-id="68bed-299">Esta lição contém Olá procedimentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="68bed-299">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="68bed-300">Modificar o arquivo XAML de saudação</span><span class="sxs-lookup"><span data-stu-id="68bed-300">Modify hello XAML file</span></span>
2. <span data-ttu-id="68bed-301">Modificar o arquivo de behand código Olá</span><span class="sxs-lookup"><span data-stu-id="68bed-301">Modify hello code behand file</span></span>
3. <span data-ttu-id="68bed-302">Compilar e testar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="68bed-302">Compile and test hello application</span></span>

<span data-ttu-id="68bed-303">**arquivo do toomodify Olá XAML**</span><span class="sxs-lookup"><span data-stu-id="68bed-303">**toomodify hello XAML file**</span></span>

1. <span data-ttu-id="68bed-304">No Gerenciador de Soluções, clique com o botão direito do mouse em **MainPage.xaml**, e, em seguida, clique em **Designer de Modos de Exibição**.</span><span class="sxs-lookup"><span data-stu-id="68bed-304">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="68bed-305">Localizar Olá &lt;grade&gt; marca com o nome da saudação **gridStreamAndBitrateSelection**, acrescente Olá código final Olá marca Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="68bed-305">Locate hello &lt;Grid&gt; tag with hello name **gridStreamAndBitrateSelection**, append hello following code at hello end of hello tag:</span></span>
   
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
3. <span data-ttu-id="68bed-306">Pressione **CTRL + S** toosave ele altera</span><span class="sxs-lookup"><span data-stu-id="68bed-306">Press **CTRL+S** toosave he changes</span></span>

<span data-ttu-id="68bed-307">**toomodify Olá arquivo code-behind**</span><span class="sxs-lookup"><span data-stu-id="68bed-307">**toomodify hello code behind file**</span></span>

1. <span data-ttu-id="68bed-308">No Gerenciador de Soluções, clique com o botão direito do mouse em **MainPage.xaml** e clique em **Exibir Código**.</span><span class="sxs-lookup"><span data-stu-id="68bed-308">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="68bed-309">Olá SSPlayer namespace, adicione uma nova classe:</span><span class="sxs-lookup"><span data-stu-id="68bed-309">Inside hello SSPlayer namespace, add a new class:</span></span>
   
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
3. <span data-ttu-id="68bed-310">Início de saudação do hello classe MainPage, adicione Olá definições de variáveis a seguir:</span><span class="sxs-lookup"><span data-stu-id="68bed-310">At hello beginning of hello MainPage class, add hello following variable definitions:</span></span>
   
        private List<Track> availableTracks;
4. <span data-ttu-id="68bed-311">Em Olá classe MainPage, adicione Olá região a seguir:</span><span class="sxs-lookup"><span data-stu-id="68bed-311">Inside hello MainPage class, add hello following region:</span></span>
   
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
5. <span data-ttu-id="68bed-312">Localize o método de mediaElement_ManifestReady hello, acrescentar Olá código final Olá função hello a seguir:</span><span class="sxs-lookup"><span data-stu-id="68bed-312">Locate hello mediaElement_ManifestReady method, append hello following code at hello end of hello function:</span></span>
   
         getTracks(manifestObject);
         refreshAvailableTracksListBoxItemSource();
6. <span data-ttu-id="68bed-313">Dentro de Olá classe MainPage, localize Olá botões de interface do usuário clique em eventos de região e adicione Olá definição de função a seguir:</span><span class="sxs-lookup"><span data-stu-id="68bed-313">Inside hello MainPage class, locate hello UI buttons click events region, and then add hello following function definition:</span></span>
   
         private void btnChangeStream_Click(object sender, RoutedEventArgs e)
         {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();

            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);

            // Change streams on hello presentation
            changeStreams(selectedStreams);
         }

<span data-ttu-id="68bed-314">**toocompile e testar o aplicativo hello**</span><span class="sxs-lookup"><span data-stu-id="68bed-314">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="68bed-315">Pressione **F6** toocompile projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="68bed-315">Press **F6** toocompile hello project.</span></span> 
2. <span data-ttu-id="68bed-316">Pressione **F5** aplicativo hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="68bed-316">Press **F5** toorun hello application.</span></span>
3. <span data-ttu-id="68bed-317">Na parte superior de saudação do aplicativo hello, você pode usar saudação padrão URL de Smooth Streaming ou insira outro.</span><span class="sxs-lookup"><span data-stu-id="68bed-317">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="68bed-318">Clique em **Definir Origem**.</span><span class="sxs-lookup"><span data-stu-id="68bed-318">Click **Set Source**.</span></span> 
5. <span data-ttu-id="68bed-319">Por padrão, todas as faixas de saudação do fluxo de vídeo Olá são selecionadas.</span><span class="sxs-lookup"><span data-stu-id="68bed-319">By default, all of hello tracks of hello video stream are selected.</span></span> <span data-ttu-id="68bed-320">alterações de taxa de bits de tooexperiment hello, você pode selecionar hello mais baixa taxa de bits disponível e, em seguida, selecione hello mais alta taxa de bits disponível.</span><span class="sxs-lookup"><span data-stu-id="68bed-320">tooexperiment hello bit rate changes, you can select hello lowest bit rate available, and then select hello highest bit rate available.</span></span> <span data-ttu-id="68bed-321">Você deve clicar em Enviar após cada alteração.</span><span class="sxs-lookup"><span data-stu-id="68bed-321">You must click Submit after each change.</span></span>  <span data-ttu-id="68bed-322">Você pode ver as alterações de qualidade de vídeo hello.</span><span class="sxs-lookup"><span data-stu-id="68bed-322">You can see hello video quality changes.</span></span>

<span data-ttu-id="68bed-323">Você concluiu a lição 4.</span><span class="sxs-lookup"><span data-stu-id="68bed-323">You have completed lesson 4.</span></span>  <span data-ttu-id="68bed-324">Nesta lição, você deve adicionar Olá funcionalidade toochoose faixas.</span><span class="sxs-lookup"><span data-stu-id="68bed-324">In this lesson, you add hello functionality toochoose tracks.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="68bed-325">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="68bed-325">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="68bed-326">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="68bed-326">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="other-resources"></a><span data-ttu-id="68bed-327">Outros recursos:</span><span class="sxs-lookup"><span data-stu-id="68bed-327">Other Resources:</span></span>
* [<span data-ttu-id="68bed-328">Como toobuild um aplicativo Smooth Streaming Windows 8 JavaScript com recursos avançados</span><span class="sxs-lookup"><span data-stu-id="68bed-328">How toobuild a Smooth Streaming Windows 8 JavaScript application with advanced features</span></span>](http://blogs.iis.net/cenkd/archive/2012/08/10/how-to-build-a-smooth-streaming-windows-8-javascript-application-with-advanced-features.aspx)
* [<span data-ttu-id="68bed-329">Visão Geral Técnica de Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="68bed-329">Smooth Streaming Technical Overview</span></span>](http://www.iis.net/learn/media/on-demand-smooth-streaming/smooth-streaming-technical-overview)

[PlayerApplication]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-1.png
[CodeViewPic]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-2.png

