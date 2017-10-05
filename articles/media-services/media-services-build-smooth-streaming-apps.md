---
title: Tutorial do Aplicativo Windows Store do Smooth Streaming | Microsoft Docs
description: "Saiba como usar os Serviços de Mídia do Azure para criar um aplicativo C# da Windows Store com um controle XML MediaElement para reprodução de conteúdo de Smooth Streaming."
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
ms.openlocfilehash: c9bb3b1915543fea3561cb309f55c4e8a74ded6d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-build-a-smooth-streaming-windows-store-application"></a><span data-ttu-id="6a89c-103">Como compilar um aplicativo Smooth Streaming da Windows Store</span><span class="sxs-lookup"><span data-stu-id="6a89c-103">How to Build a Smooth Streaming Windows Store Application</span></span>

<span data-ttu-id="6a89c-104">O SDK do Smooth Streaming Client para Windows 8 permite que os desenvolvedores criem aplicativos da Windows Store que podem reproduzir conteúdo de Smooth Streaming sob demanda e ao vivo.</span><span class="sxs-lookup"><span data-stu-id="6a89c-104">The Smooth Streaming Client SDK for Windows 8 enables developers to build Windows Store applications that can play on-demand and live Smooth Streaming content.</span></span> <span data-ttu-id="6a89c-105">Além da reprodução básica de conteúdo do Smooth Streaming, o SDK também fornece recursos avançados, como proteção do Microsoft PlayReady, restrição de nível de qualidade, Live DVR, alternância de fluxo de áudio, escuta de atualizações de status (como alterações no nível da qualidade), eventos de erros e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="6a89c-105">In addition to the basic playback of Smooth Streaming content, the SDK also provides rich features like Microsoft PlayReady protection, quality level restriction, Live DVR, audio stream switching, listening for status updates (such as quality level changes) and error events, and so on.</span></span> <span data-ttu-id="6a89c-106">Para obter mais informações sobre os recursos suportados, consulte as [notas da versão (a página pode estar em inglês)](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes).</span><span class="sxs-lookup"><span data-stu-id="6a89c-106">For more information of the supported features, see the [release notes](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes).</span></span> <span data-ttu-id="6a89c-107">Para obter mais informações, consulte [Player Framework para Windows 8](http://playerframework.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="6a89c-107">For more information, see [Player Framework for Windows 8](http://playerframework.codeplex.com/).</span></span> 

<span data-ttu-id="6a89c-108">Este tutorial contém quatro lições:</span><span class="sxs-lookup"><span data-stu-id="6a89c-108">This tutorial contains four lessons:</span></span>

1. <span data-ttu-id="6a89c-109">Criar um aplicativo de armazenamento básico Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="6a89c-109">Create a Basic Smooth Streaming Store Application</span></span>
2. <span data-ttu-id="6a89c-110">Adicionar um barra deslizante para controlar o andamento da mídia</span><span class="sxs-lookup"><span data-stu-id="6a89c-110">Add a Slider Bar to Control the Media Progress</span></span>
3. <span data-ttu-id="6a89c-111">Selecionar fluxos do Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="6a89c-111">Select Smooth Streaming Streams</span></span>
4. <span data-ttu-id="6a89c-112">Selecionar faixas do Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="6a89c-112">Select Smooth Streaming Tracks</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a89c-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6a89c-113">Prerequisites</span></span>
* <span data-ttu-id="6a89c-114">Windows 8 32 bits ou 64 bits.</span><span class="sxs-lookup"><span data-stu-id="6a89c-114">Windows 8 32-bit or 64-bit.</span></span> <span data-ttu-id="6a89c-115">Você pode obter o [Windows 8 Enterprise Evaluation (a página pode estar em inglês)](http://msdn.microsoft.com/evalcenter/jj554510.aspx) no MSDN.</span><span class="sxs-lookup"><span data-stu-id="6a89c-115">You can get [Windows 8 Enterprise Evaluation](http://msdn.microsoft.com/evalcenter/jj554510.aspx) from MSDN.</span></span>
* <span data-ttu-id="6a89c-116">Visual Studio 2012 ou Visual Studio Express 2012 (ou versão posterior).</span><span class="sxs-lookup"><span data-stu-id="6a89c-116">Visual Studio 2012 or Visual Studio Express 2012 (or a later version).</span></span> <span data-ttu-id="6a89c-117">Você pode obter a versão de avaliação [aqui](http://www.microsoft.com/visualstudio/11/downloads).</span><span class="sxs-lookup"><span data-stu-id="6a89c-117">You can get the trial version from [here](http://www.microsoft.com/visualstudio/11/downloads).</span></span>
* <span data-ttu-id="6a89c-118">[SDK do Microsoft Smooth Streaming Client para Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home)</span><span class="sxs-lookup"><span data-stu-id="6a89c-118">[Microsoft Smooth Streaming Client SDK for Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home).</span></span>

<span data-ttu-id="6a89c-119">A solução completa para cada lição pode ser baixada das Amostras de Código de Desenvolvedor do MSDN (Galeria de Códigos):</span><span class="sxs-lookup"><span data-stu-id="6a89c-119">The completed solution for each lesson can be downloaded from MSDN Developer Code Samples (Code Gallery):</span></span> 

* <span data-ttu-id="6a89c-120">[Lição 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) - Um Media Player simples de Smooth Streaming do Windows 8,</span><span class="sxs-lookup"><span data-stu-id="6a89c-120">[Lesson 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) - A Simple Windows 8 Smooth Streaming Media Player,</span></span> 
* <span data-ttu-id="6a89c-121">[Lição 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) - Um Media Player simples de Smooth Streaming do Windows 8 com um controle de barra deslizante,</span><span class="sxs-lookup"><span data-stu-id="6a89c-121">[Lesson 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) - A Simple Windows 8 Smooth Streaming Media Player with a Slider Bar Control,</span></span> 
* <span data-ttu-id="6a89c-122">[Lição 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) - Um Media Player simples de Smooth Streaming do Windows 8 com seleção de fluxo,</span><span class="sxs-lookup"><span data-stu-id="6a89c-122">[Lesson 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) - A Windows 8 Smooth Streaming Media Player with Stream Selection,</span></span>  
* <span data-ttu-id="6a89c-123">[Lição 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907) - um Media Player simples de Smooth Streaming do Windows 8 com seleção de faixa.</span><span class="sxs-lookup"><span data-stu-id="6a89c-123">[Lesson 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907)  - A Windows 8 Smooth Streaming Media Player with Track Selection.</span></span>

## <a name="lesson-1-create-a-basic-smooth-streaming-store-application"></a><span data-ttu-id="6a89c-124">Lição 1: Criar um aplicativo básico de Smooth Streaming para a Store</span><span class="sxs-lookup"><span data-stu-id="6a89c-124">Lesson 1: Create a Basic Smooth Streaming Store Application</span></span>

<span data-ttu-id="6a89c-125">Nesta lição, você criará um aplicativo da Windows Store com um controle MediaElement para reproduzir conteúdo de Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="6a89c-125">In this lesson, you will create a Windows Store application with a MediaElement control to play Smooth Stream content.</span></span>  <span data-ttu-id="6a89c-126">O aplicativo em execução é semelhante a:</span><span class="sxs-lookup"><span data-stu-id="6a89c-126">The running application looks like:</span></span>

![Exemplo de aplicativo de Smooth Streaming da Windows Store][PlayerApplication]

<span data-ttu-id="6a89c-128">Para obter mais informações sobre como desenvolver aplicativos da Windows Store, consulte [Desenvolver Ótimos Aplicativos para o Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx).</span><span class="sxs-lookup"><span data-stu-id="6a89c-128">For more information on developing Windows Store application, see [Develop Great Apps for Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx).</span></span> <span data-ttu-id="6a89c-129">Esta lição contém os seguintes procedimentos:</span><span class="sxs-lookup"><span data-stu-id="6a89c-129">This lesson contains the following procedures:</span></span>

1. <span data-ttu-id="6a89c-130">Criar um novo projeto da Windows Store</span><span class="sxs-lookup"><span data-stu-id="6a89c-130">Create a Windows Store project</span></span>
2. <span data-ttu-id="6a89c-131">Criar a interface do usuário (XAML)</span><span class="sxs-lookup"><span data-stu-id="6a89c-131">Design the user interface (XAML)</span></span>
3. <span data-ttu-id="6a89c-132">Modificar o arquivo code-behind</span><span class="sxs-lookup"><span data-stu-id="6a89c-132">Modify the code behind file</span></span>
4. <span data-ttu-id="6a89c-133">Compilar e testar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="6a89c-133">Compile and test the application</span></span>

<span data-ttu-id="6a89c-134">**Para criar um novo projeto da Windows Store**</span><span class="sxs-lookup"><span data-stu-id="6a89c-134">**To create a Windows Store project**</span></span>

1. <span data-ttu-id="6a89c-135">Execute o Visual Studio 2012 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="6a89c-135">Run Visual Studio 2012 or later.</span></span>
2. <span data-ttu-id="6a89c-136">No menu **ARQUIVO**, clique em **Novo** e em **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="6a89c-136">From the **FILE** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="6a89c-137">Na caixa de diálogo Novo Projeto, digite ou selecione os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="6a89c-137">From the New Project dialog, type or select  the following values:</span></span>

| <span data-ttu-id="6a89c-138">Nome</span><span class="sxs-lookup"><span data-stu-id="6a89c-138">Name</span></span> | <span data-ttu-id="6a89c-139">Valor</span><span class="sxs-lookup"><span data-stu-id="6a89c-139">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6a89c-140">Grupo de modelos</span><span class="sxs-lookup"><span data-stu-id="6a89c-140">Template group</span></span> |<span data-ttu-id="6a89c-141">Instalado/Modelos/Visual C#/Windows Store</span><span class="sxs-lookup"><span data-stu-id="6a89c-141">Installed/Templates/Visual C#/Windows Store</span></span> |
| <span data-ttu-id="6a89c-142">Modelo</span><span class="sxs-lookup"><span data-stu-id="6a89c-142">Template</span></span> |<span data-ttu-id="6a89c-143">Aplicativo em branco (XAML)</span><span class="sxs-lookup"><span data-stu-id="6a89c-143">Blank App (XAML)</span></span> |
| <span data-ttu-id="6a89c-144">Nome</span><span class="sxs-lookup"><span data-stu-id="6a89c-144">Name</span></span> |<span data-ttu-id="6a89c-145">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="6a89c-145">SSPlayer</span></span> |
| <span data-ttu-id="6a89c-146">Local</span><span class="sxs-lookup"><span data-stu-id="6a89c-146">Location</span></span> |<span data-ttu-id="6a89c-147">C:\SSTutorials</span><span class="sxs-lookup"><span data-stu-id="6a89c-147">C:\SSTutorials</span></span> |
| <span data-ttu-id="6a89c-148">Nome da solução</span><span class="sxs-lookup"><span data-stu-id="6a89c-148">Solution Name</span></span> |<span data-ttu-id="6a89c-149">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="6a89c-149">SSPlayer</span></span> |
| <span data-ttu-id="6a89c-150">Criar diretório para a solução</span><span class="sxs-lookup"><span data-stu-id="6a89c-150">Create directory for solution</span></span> |<span data-ttu-id="6a89c-151">(selecionado)</span><span class="sxs-lookup"><span data-stu-id="6a89c-151">(selected)</span></span> |

1. <span data-ttu-id="6a89c-152">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="6a89c-152">Click **OK**.</span></span>

<span data-ttu-id="6a89c-153">**Para adicionar uma referência ao SDK do Smooth Streaming Client**</span><span class="sxs-lookup"><span data-stu-id="6a89c-153">**To add a reference to the Smooth Streaming Client SDK**</span></span>

1. <span data-ttu-id="6a89c-154">No Gerenciador de Soluções, clique com o botão direito do mouse em **SSPlayer** e, em seguida, clique em **Adicionar Referência**.</span><span class="sxs-lookup"><span data-stu-id="6a89c-154">From Solution Explorer, right-click **SSPlayer**, and then click **Add Reference**.</span></span>
2. <span data-ttu-id="6a89c-155">Digite ou selecione os valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="6a89c-155">Type or select the following values:</span></span>

| <span data-ttu-id="6a89c-156">Nome</span><span class="sxs-lookup"><span data-stu-id="6a89c-156">Name</span></span> | <span data-ttu-id="6a89c-157">Valor</span><span class="sxs-lookup"><span data-stu-id="6a89c-157">Value</span></span> |
| --- | --- |
| <span data-ttu-id="6a89c-158">Grupo de referências</span><span class="sxs-lookup"><span data-stu-id="6a89c-158">Reference group</span></span> |<span data-ttu-id="6a89c-159">Windows/Extensions</span><span class="sxs-lookup"><span data-stu-id="6a89c-159">Windows/Extensions</span></span> |
| <span data-ttu-id="6a89c-160">Referência</span><span class="sxs-lookup"><span data-stu-id="6a89c-160">Reference</span></span> |<span data-ttu-id="6a89c-161">Selecione SDK do Microsoft Smooth Streaming Client para Windows 8 e Pacote do Tempo de Execução do Microsoft Visual C++</span><span class="sxs-lookup"><span data-stu-id="6a89c-161">Select Microsoft Smooth Streaming Client SDK for Windows 8 and Microsoft Visual C++ Runtime Package</span></span> |

1. <span data-ttu-id="6a89c-162">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="6a89c-162">Click **OK**.</span></span> 

<span data-ttu-id="6a89c-163">Depois de adicionar as referências, você deve selecionar a plataforma de destino (x64 ou x86). A adição de referências não funcionará para a configuração Qualquer plataforma de CPU.</span><span class="sxs-lookup"><span data-stu-id="6a89c-163">After adding the references, you must select the targeted platform (x64 or x86), adding references will not work for Any CPU platform configuration.</span></span>  <span data-ttu-id="6a89c-164">No Gerenciador de Soluções, você verá a marca de aviso amarela para essas referências adicionadas.</span><span class="sxs-lookup"><span data-stu-id="6a89c-164">In solution explorer, you will see yellow warning mark for these added references.</span></span>

<span data-ttu-id="6a89c-165">**Para criar a interface do usuário do player**</span><span class="sxs-lookup"><span data-stu-id="6a89c-165">**To design the player user interface**</span></span>

1. <span data-ttu-id="6a89c-166">No Gerenciador de Soluções, clique duas vezes em **MainPage.xaml** para abri-lo no modo de exibição de design.</span><span class="sxs-lookup"><span data-stu-id="6a89c-166">From Solution Explorer, double click **MainPage.xaml** to open it in the design view.</span></span>
2. <span data-ttu-id="6a89c-167">Localize as marcas **&lt;Grid&gt;** e **&lt;/Grid&gt;** no arquivo XAML e cole o seguinte código entre as duas marcas:</span><span class="sxs-lookup"><span data-stu-id="6a89c-167">Locate the **&lt;Grid&gt;** and **&lt;/Grid&gt;**  tags the XAML file, and paste the following code between the two tags:</span></span>

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
   
   <span data-ttu-id="6a89c-168">O controle MediaElement é usado para a reprodução de mídia.</span><span class="sxs-lookup"><span data-stu-id="6a89c-168">The MediaElement control is used to playback media.</span></span> <span data-ttu-id="6a89c-169">O controle deslizante denominado sliderProgress será usado na próxima lição para controlar o andamento da mídia.</span><span class="sxs-lookup"><span data-stu-id="6a89c-169">The slider control named sliderProgress will be used in the next lesson to control the media progress.</span></span>
3. <span data-ttu-id="6a89c-170">Pressione **CTRL+S** para salvar o arquivo.</span><span class="sxs-lookup"><span data-stu-id="6a89c-170">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="6a89c-171">O controle MediaElement não oferece suporte a conteúdo de Smooth Streaming pronto para uso.</span><span class="sxs-lookup"><span data-stu-id="6a89c-171">The MediaElement control does not support Smooth Streaming content out-of-box.</span></span> <span data-ttu-id="6a89c-172">Para habilitar o suporte do Smooth Streaming, você deve registrar o manipulador de fluxo de bytes do Smooth Streaming por extensão de nome de arquivo e tipo MIME.</span><span class="sxs-lookup"><span data-stu-id="6a89c-172">To enable the Smooth Streaming support, you must register the Smooth Streaming byte-stream handler by file name extension and MIME type.</span></span>  <span data-ttu-id="6a89c-173">Para se registrar, você deve usar o método MediaExtensionManager.RegisterByteStremHandler do namespace Windows.Media.</span><span class="sxs-lookup"><span data-stu-id="6a89c-173">To register, you use the MediaExtensionManager.RegisterByteStremHandler method of the Windows.Media namespace.</span></span>

<span data-ttu-id="6a89c-174">Nesse arquivo XAML, alguns manipuladores de eventos são associados aos controles.</span><span class="sxs-lookup"><span data-stu-id="6a89c-174">In this XAML file, some event handlers are associated with the controls.</span></span>  <span data-ttu-id="6a89c-175">Você deve definir esses manipuladores de eventos.</span><span class="sxs-lookup"><span data-stu-id="6a89c-175">You must define those event handlers.</span></span>

<span data-ttu-id="6a89c-176">**Para modificar o arquivo code-behind**</span><span class="sxs-lookup"><span data-stu-id="6a89c-176">**To modify the code behind file**</span></span>

1. <span data-ttu-id="6a89c-177">No Gerenciador de Soluções, clique com o botão direito do mouse em **MainPage.xaml** e clique em **Exibir Código**.</span><span class="sxs-lookup"><span data-stu-id="6a89c-177">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="6a89c-178">Na parte superior do arquivo, adicione a seguinte instrução using:</span><span class="sxs-lookup"><span data-stu-id="6a89c-178">At the top of the file, add the following using statement:</span></span>
   
        using Windows.Media;
3. <span data-ttu-id="6a89c-179">No início da classe **MainPage** adicione os membros de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="6a89c-179">At the beginning of the **MainPage** class, add the following data member:</span></span>
   
         private MediaExtensionManager extensions = new MediaExtensionManager();
4. <span data-ttu-id="6a89c-180">No final do construtor **MainPage** adicione as duas linhas a seguir:</span><span class="sxs-lookup"><span data-stu-id="6a89c-180">At the end of the **MainPage** constructor, add the following two lines:</span></span>
   
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "text/xml");
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "application/vnd.ms-sstr+xml");
5. <span data-ttu-id="6a89c-181">No final da classe **MainPage** cole o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="6a89c-181">At the end of the **MainPage** class, paste the following code:</span></span>
   
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
             txtStatus.Text = "Click the Play button to play the media source.";
         }
         }
         private void btnStop_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Stop();
         txtStatus.Text = "MediaElement is stopped";
         }
         private void sliderProgress_PointerPressed(object sender, PointerRoutedEventArgs e)
         {

         txtStatus.Text = "Seek to position " + sliderProgress.Value;
         mediaElement.Position = new TimeSpan(0, 0, (int)(sliderProgress.Value));
         }
         # endregion

<span data-ttu-id="6a89c-182">O manipulador de eventos sliderProgress_PointerPressed é definido aqui.</span><span class="sxs-lookup"><span data-stu-id="6a89c-182">The sliderProgress_PointerPressed event handler is defined here.</span></span>  <span data-ttu-id="6a89c-183">Para fazer isso funcionar há mais trabalhos a fazer que serão abordados na próxima lição deste tutorial.</span><span class="sxs-lookup"><span data-stu-id="6a89c-183">There are more works to do to get it working, which will be covered in the next lesson of this tutorial.</span></span>
6. <span data-ttu-id="6a89c-184">Pressione **CTRL+S** para salvar o arquivo.</span><span class="sxs-lookup"><span data-stu-id="6a89c-184">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="6a89c-185">O arquivo code-behind concluído deve ser semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="6a89c-185">The finished the code behind file shall look like this:</span></span>

![Exibição do código no Visual Studio do aplicativo de Smooth Streaming da Windows Store][CodeViewPic]

<span data-ttu-id="6a89c-187">**Para compilar e testar o aplicativo**</span><span class="sxs-lookup"><span data-stu-id="6a89c-187">**To compile and test the application**</span></span>

1. <span data-ttu-id="6a89c-188">No menu **COMPILAR** clique em **Gerenciador de Configurações**.</span><span class="sxs-lookup"><span data-stu-id="6a89c-188">From the **BUILD** menu, click **Configuration Manager**.</span></span>
2. <span data-ttu-id="6a89c-189">Altere **Plataforma da solução ativa** para que corresponda à sua plataforma de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="6a89c-189">Change **Active solution platform** to match your development platform.</span></span>
3. <span data-ttu-id="6a89c-190">Pressione **F6** para compilar o projeto.</span><span class="sxs-lookup"><span data-stu-id="6a89c-190">Press **F6** to compile the project.</span></span> 
4. <span data-ttu-id="6a89c-191">Pressione **F5** para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6a89c-191">Press **F5** to run the application.</span></span>
5. <span data-ttu-id="6a89c-192">Na parte superior do aplicativo, use a URL do Smooth Streaming padrão ou digite outra URL.</span><span class="sxs-lookup"><span data-stu-id="6a89c-192">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span></span> 
6. <span data-ttu-id="6a89c-193">Clique em **Definir Origem**.</span><span class="sxs-lookup"><span data-stu-id="6a89c-193">Click **Set Source**.</span></span> <span data-ttu-id="6a89c-194">Como, por padrão, **Executar Automaticamente** está habilitado, a mídia deverá ser reproduzida automaticamente.</span><span class="sxs-lookup"><span data-stu-id="6a89c-194">Because **Auto Play** is enabled by default, the media shall play automatically.</span></span>  <span data-ttu-id="6a89c-195">Você pode controlar a mídia usando os botões **Reproduzir**, **Pausar** e **Parar**.</span><span class="sxs-lookup"><span data-stu-id="6a89c-195">You can control the media using the **Play**, **Pause** and **Stop** buttons.</span></span>  <span data-ttu-id="6a89c-196">É possível controlar o volume da mídia usando o controle deslizante vertical.</span><span class="sxs-lookup"><span data-stu-id="6a89c-196">You can control the media volume using the vertical slider.</span></span>  <span data-ttu-id="6a89c-197">No entanto, a barra deslizante horizontal para controle do progresso da mídia ainda não está totalmente implementado.</span><span class="sxs-lookup"><span data-stu-id="6a89c-197">However the horizontal slider for controlling the media progress is not fully implemented yet.</span></span> 

<span data-ttu-id="6a89c-198">Você concluiu a Lição 1.</span><span class="sxs-lookup"><span data-stu-id="6a89c-198">You have completed lesson1.</span></span>  <span data-ttu-id="6a89c-199">Nesta lição, você usa um controle MediaElement para reproduzir conteúdo de Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="6a89c-199">In this lesson, you use a MediaElement control to playback Smooth Streaming content.</span></span>  <span data-ttu-id="6a89c-200">Na próxima lição, você irá adicionar um controle deslizante para controlar o andamento do conteúdo de Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="6a89c-200">In the next lesson, you will add a slider to control the progress of the Smooth Streaming content.</span></span>

## <a name="lesson-2-add-a-slider-bar-to-control-the-media-progress"></a><span data-ttu-id="6a89c-201">Lição 2: Adicionar um barra deslizante para controlar o andamento da mídia</span><span class="sxs-lookup"><span data-stu-id="6a89c-201">Lesson 2: Add a Slider Bar to Control the Media Progress</span></span>

<span data-ttu-id="6a89c-202">Na Lição 1, você criou um aplicativo da Windows Store com um controle XAML MediaElement para reproduzir conteúdo de mídia de Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="6a89c-202">In lesson 1, you created a Windows Store application with a MediaElement XAML control to playback Smooth Streaming media content.</span></span>  <span data-ttu-id="6a89c-203">Ele vem com algumas funções básicas de mídia, como iniciar, parar e pausar.</span><span class="sxs-lookup"><span data-stu-id="6a89c-203">It comes some basic media functions like start, stop and pause.</span></span>  <span data-ttu-id="6a89c-204">Nesta lição, você irá adicionar um controle de barra deslizante ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6a89c-204">In this lesson, you will add a slider bar control to the application.</span></span>

<span data-ttu-id="6a89c-205">Neste tutorial, usaremos um timer para atualizar a posição do controle deslizante com base na posição atual do controle MediaElement.</span><span class="sxs-lookup"><span data-stu-id="6a89c-205">In this tutorial, we will use a timer to update the slider position based on the current position of the MediaElement control.</span></span>  <span data-ttu-id="6a89c-206">A hora de início e de término do controle deslizante também precisam ser atualizadas no caso de conteúdo ao vivo.</span><span class="sxs-lookup"><span data-stu-id="6a89c-206">The slider start and end time also need to be updated in case of live content.</span></span>  <span data-ttu-id="6a89c-207">Isso pode ser manipulado melhor no evento de atualização de origem adaptável.</span><span class="sxs-lookup"><span data-stu-id="6a89c-207">This can be better handled in the adaptive source update event.</span></span>

<span data-ttu-id="6a89c-208">As origens de mídia são objetos que geram dados de mídia.</span><span class="sxs-lookup"><span data-stu-id="6a89c-208">Media sources are objects that generate media data.</span></span>  <span data-ttu-id="6a89c-209">O resolvedor de origem utiliza um fluxo de bytes ou uma URL e cria a origem de mídia adequada para esse conteúdo.</span><span class="sxs-lookup"><span data-stu-id="6a89c-209">The source resolver takes a URL or byte stream and creates the appropriate media source for that content.</span></span>  <span data-ttu-id="6a89c-210">O resolvedor de origem é o modo padrão para os aplicativos criarem origens de mídia.</span><span class="sxs-lookup"><span data-stu-id="6a89c-210">The source resolver is the standard way for the applications to create media sources.</span></span> 

<span data-ttu-id="6a89c-211">Esta lição contém os seguintes procedimentos:</span><span class="sxs-lookup"><span data-stu-id="6a89c-211">This lesson contains the following procedures:</span></span>

1. <span data-ttu-id="6a89c-212">Registrar o manipulador do Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="6a89c-212">Register the Smooth Streaming handler</span></span> 
2. <span data-ttu-id="6a89c-213">Adicionar manipuladores de eventos no nível do gerenciador de origem adaptável</span><span class="sxs-lookup"><span data-stu-id="6a89c-213">Add the adaptive source manager level event handlers</span></span>
3. <span data-ttu-id="6a89c-214">Adicionar os manipuladores de eventos de origem adaptável</span><span class="sxs-lookup"><span data-stu-id="6a89c-214">Add the adaptive source level event handlers</span></span>
4. <span data-ttu-id="6a89c-215">Adicionar manipuladores de eventos de MediaElement</span><span class="sxs-lookup"><span data-stu-id="6a89c-215">Add MediaElement event handlers</span></span>
5. <span data-ttu-id="6a89c-216">Adicionar o código relacionado à barra de controle deslizante</span><span class="sxs-lookup"><span data-stu-id="6a89c-216">Add slider bar related code</span></span>
6. <span data-ttu-id="6a89c-217">Compilar e testar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="6a89c-217">Compile and test the application</span></span>

<span data-ttu-id="6a89c-218">**Para registrar o manipulador de fluxo de bytes de Smooth Streaming e aprovar o propertyset**</span><span class="sxs-lookup"><span data-stu-id="6a89c-218">**To register the Smooth Streaming byte-stream handler and pass the propertyset**</span></span>

1. <span data-ttu-id="6a89c-219">No Gerenciador de Soluções, clique com o botão direito do mouse em **MainPage.xaml** e clique em **Exibir Código**.</span><span class="sxs-lookup"><span data-stu-id="6a89c-219">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="6a89c-220">No início do arquivo, adicione a seguinte instrução using:</span><span class="sxs-lookup"><span data-stu-id="6a89c-220">At the beginning of the file, add the following using statement:</span></span>

        using Microsoft.Media.AdaptiveStreaming;
3. <span data-ttu-id="6a89c-221">No início da classe MainPage adicione os membros de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="6a89c-221">At the beginning of the MainPage class, add the following data members:</span></span>

         private Windows.Foundation.Collections.PropertySet propertySet = new Windows.Foundation.Collections.PropertySet();             
         private IAdaptiveSourceManager adaptiveSourceManager;
4. <span data-ttu-id="6a89c-222">No construtor **MainPage**, adicione o seguinte código após a linha **this.Initialize Components();** e as linhas de código do registro escritas na lição anterior:</span><span class="sxs-lookup"><span data-stu-id="6a89c-222">Inside the **MainPage** constructor, add the following code after the **this.Initialize Components();** line and the registration code lines written in the previous lesson:</span></span>

        // Gets the default instance of AdaptiveSourceManager which manages Smooth 
        //Streaming media sources.
        adaptiveSourceManager = AdaptiveSourceManager.GetDefault();
        // Sets property key value to AdaptiveSourceManager default instance.
        // {A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}" must be hardcoded.
        propertySet["{A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}"] = adaptiveSourceManager;
5. <span data-ttu-id="6a89c-223">Dentro do construtor **MainPage** , modifique os dois métodos RegisterByteStreamHandler para adicionar os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="6a89c-223">Inside the **MainPage** constructor, modify the two RegisterByteStreamHandler methods to add the forth parameters:</span></span>

         // Registers Smooth Streaming byte-stream handler for ".ism" extension and, 
         // "text/xml" and "application/vnd.ms-ss" mime-types and pass the propertyset. 
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
6. <span data-ttu-id="6a89c-224">Pressione **CTRL+S** para salvar o arquivo.</span><span class="sxs-lookup"><span data-stu-id="6a89c-224">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="6a89c-225">**Para adicionar o manipulador de eventos no nível do gerenciador de origens adaptáveis**</span><span class="sxs-lookup"><span data-stu-id="6a89c-225">**To add the adaptive source manager level event handler**</span></span>

1. <span data-ttu-id="6a89c-226">No Gerenciador de Soluções, clique com o botão direito do mouse em **MainPage.xaml** e clique em **Exibir Código**.</span><span class="sxs-lookup"><span data-stu-id="6a89c-226">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="6a89c-227">No início da classe **MainPage** adicione os membros de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="6a89c-227">Inside the **MainPage** class, add the following data member:</span></span>
   
     <span data-ttu-id="6a89c-228">private AdaptiveSource adaptiveSource = null;</span><span class="sxs-lookup"><span data-stu-id="6a89c-228">private AdaptiveSource adaptiveSource = null;</span></span>
3. <span data-ttu-id="6a89c-229">No final da classe **MainPage** , adicione o manipulador de eventos a seguir:</span><span class="sxs-lookup"><span data-stu-id="6a89c-229">At the end of the **MainPage** class, add the following event handler:</span></span>
   
         # region Adaptive Source Manager Level Events
         private void mediaElement_AdaptiveSourceOpened(AdaptiveSource sender, AdaptiveSourceOpenedEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
         }

         # endregion Adaptive Source Manager Level Events
4. <span data-ttu-id="6a89c-230">No final do construtor **MainPage** , adicione a seguinte linha para inscrever-se para o evento de fonte aberta adaptável:</span><span class="sxs-lookup"><span data-stu-id="6a89c-230">At the end of the **MainPage** constructor, add the following line to subscribe to the adaptive source open event:</span></span>
   
         adaptiveSourceManager.AdaptiveSourceOpenedEvent += 
           new AdaptiveSourceOpenedEventHandler(mediaElement_AdaptiveSourceOpened);
5. <span data-ttu-id="6a89c-231">Pressione **CTRL+S** para salvar o arquivo.</span><span class="sxs-lookup"><span data-stu-id="6a89c-231">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="6a89c-232">**Para adicionar os manipuladores de eventos de origens adaptáveis**</span><span class="sxs-lookup"><span data-stu-id="6a89c-232">**To add adaptive source level event handlers**</span></span>

1. <span data-ttu-id="6a89c-233">No Gerenciador de Soluções, clique com o botão direito do mouse em **MainPage.xaml** e clique em **Exibir Código**.</span><span class="sxs-lookup"><span data-stu-id="6a89c-233">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="6a89c-234">No início da classe **MainPage** adicione os membros de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="6a89c-234">Inside the **MainPage** class, add the following data member:</span></span>
   
     <span data-ttu-id="6a89c-235">private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;</span><span class="sxs-lookup"><span data-stu-id="6a89c-235">private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;</span></span>
3. <span data-ttu-id="6a89c-236">No final da classe **MainPage** , adicione os manipuladores de eventos a seguir:</span><span class="sxs-lookup"><span data-stu-id="6a89c-236">At the end of the **MainPage** class, add the following event handlers:</span></span>

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
4. <span data-ttu-id="6a89c-237">No final do método **mediaElement AdaptiveSourceOpened** , adicione o seguinte código para se inscrever nos eventos:</span><span class="sxs-lookup"><span data-stu-id="6a89c-237">At the end of the **mediaElement AdaptiveSourceOpened** method, add the following code to subscribe to the events:</span></span>
   
         adaptiveSource.ManifestReadyEvent +=

                    mediaElement_ManifestReady;
         adaptiveSource.AdaptiveSourceStatusUpdatedEvent += 

            mediaElement_AdaptiveSourceStatusUpdated;
         adaptiveSource.AdaptiveSourceFailedEvent += 

            mediaElement_AdaptiveSourceFailed;
5. <span data-ttu-id="6a89c-238">Pressione **CTRL+S** para salvar o arquivo.</span><span class="sxs-lookup"><span data-stu-id="6a89c-238">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="6a89c-239">Os mesmos eventos também estão disponíveis no nível do gerenciador de origens adaptáveis, que pode ser usado para manipular a funcionalidade comum a todos os elementos de mídia do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6a89c-239">The same events are available on Adaptive Source manger level as well, which can be used for handling functionality common to all media elements in the app.</span></span> <span data-ttu-id="6a89c-240">Cada AdaptiveSource inclui seus próprios eventos e todos os eventos de AdaptiveSource serão colocados em cascata no AdaptiveSourceManager.</span><span class="sxs-lookup"><span data-stu-id="6a89c-240">Each AdaptiveSource includes its own events and all AdaptiveSource events will be cascaded under AdaptiveSourceManager.</span></span>

<span data-ttu-id="6a89c-241">**Para adicionar manipuladores de eventos de elementos de mídia**</span><span class="sxs-lookup"><span data-stu-id="6a89c-241">**To add Media Element event handlers**</span></span>

1. <span data-ttu-id="6a89c-242">No Gerenciador de Soluções, clique com o botão direito do mouse em **MainPage.xaml** e clique em **Exibir Código**.</span><span class="sxs-lookup"><span data-stu-id="6a89c-242">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="6a89c-243">No final da classe **MainPage** , adicione os manipuladores de eventos a seguir:</span><span class="sxs-lookup"><span data-stu-id="6a89c-243">At the end of the **MainPage** class, add the following event handlers:</span></span>

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
3. <span data-ttu-id="6a89c-244">No final do construtor **MainPage** , adicione o seguinte código para se inscrever nos eventos:</span><span class="sxs-lookup"><span data-stu-id="6a89c-244">At the end of the **MainPage** constructor, add the following code to subscript to the events:</span></span>

         mediaElement.MediaOpened += MediaOpened;
         mediaElement.MediaEnded += MediaEnded;
         mediaElement.MediaFailed += MediaFailed;
4. <span data-ttu-id="6a89c-245">Pressione **CTRL+S** para salvar o arquivo.</span><span class="sxs-lookup"><span data-stu-id="6a89c-245">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="6a89c-246">**Para adicionar o código relacionado à barra de controle deslizante**</span><span class="sxs-lookup"><span data-stu-id="6a89c-246">**To add slider bar related code**</span></span>

1. <span data-ttu-id="6a89c-247">No Gerenciador de Soluções, clique com o botão direito do mouse em **MainPage.xaml** e clique em **Exibir Código**.</span><span class="sxs-lookup"><span data-stu-id="6a89c-247">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="6a89c-248">No início do arquivo, adicione a seguinte instrução using:</span><span class="sxs-lookup"><span data-stu-id="6a89c-248">At the beginning of the file, add the following using statement:</span></span>
      
        using Windows.UI.Core;
3. <span data-ttu-id="6a89c-249">No início da classe **MainPage** adicione os membros de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="6a89c-249">Inside the **MainPage** class, add the following data members:</span></span>
   
         public static CoreDispatcher _dispatcher;
         private DispatcherTimer sliderPositionUpdateDispatcher;
4. <span data-ttu-id="6a89c-250">No final do construtor **MainPage** adicione o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="6a89c-250">At the end of the **MainPage** constructor, add the following code:</span></span>
   
         _dispatcher = Window.Current.Dispatcher;
         PointerEventHandler pointerpressedhandler = new PointerEventHandler(sliderProgress_PointerPressed);
         sliderProgress.AddHandler(Control.PointerPressedEvent, pointerpressedhandler, true);    
5. <span data-ttu-id="6a89c-251">No final da classe **MainPage** , adicione o código a seguir:</span><span class="sxs-lookup"><span data-stu-id="6a89c-251">At the end of the **MainPage** class, add the following code:</span></span>

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
><span data-ttu-id="6a89c-252">O CoreDispatcher é usado para fazer alterações no thread da interface do usuário no thread que não é da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="6a89c-252">CoreDispatcher is used to make changes to the UI thread from non UI Thread.</span></span> <span data-ttu-id="6a89c-253">No caso de afunilamento no dispatcher de threads, o desenvolvedor pode optar por usar o dispatcher fornecido pelo elemento da interface do usuário que pretende atualizar.</span><span class="sxs-lookup"><span data-stu-id="6a89c-253">In case of bottleneck on dispatcher thread, developer can choose to use dispatcher provided by UI-element he/she intends to update.</span></span>  <span data-ttu-id="6a89c-254">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="6a89c-254">For example:</span></span>
   
         await sliderProgress.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () => { TimeSpan 

         timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime); 
         double absvalue  = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero); 

         sliderProgress.Maximum = absvalue; }); 
6. <span data-ttu-id="6a89c-255">Ao final do método **mediaElement_AdaptiveSourceStatusUpdated**, adicione este código:</span><span class="sxs-lookup"><span data-stu-id="6a89c-255">At the end of the **mediaElement_AdaptiveSourceStatusUpdated** method, add the following code:</span></span>

         setSliderStartTime(args.StartTime);
         setSliderEndTime(args.EndTime);
7. <span data-ttu-id="6a89c-256">No final do método **MediaOpened** , adicione o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="6a89c-256">At the end of the **MediaOpened** method, add the following code:</span></span>

         sliderProgress.StepFrequency = SliderFrequency(mediaElement.NaturalDuration.TimeSpan);
         sliderProgress.Width = mediaElement.Width;
         setupTimer();
8. <span data-ttu-id="6a89c-257">Pressione **CTRL+S** para salvar o arquivo.</span><span class="sxs-lookup"><span data-stu-id="6a89c-257">Press **CTRL+S** to save the file.</span></span>

<span data-ttu-id="6a89c-258">**Para compilar e testar o aplicativo**</span><span class="sxs-lookup"><span data-stu-id="6a89c-258">**To compile and test the application**</span></span>

1. <span data-ttu-id="6a89c-259">Pressione **F6** para compilar o projeto.</span><span class="sxs-lookup"><span data-stu-id="6a89c-259">Press **F6** to compile the project.</span></span> 
2. <span data-ttu-id="6a89c-260">Pressione **F5** para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6a89c-260">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="6a89c-261">Na parte superior do aplicativo, use a URL do Smooth Streaming padrão ou digite outra URL.</span><span class="sxs-lookup"><span data-stu-id="6a89c-261">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="6a89c-262">Clique em **Definir Origem**.</span><span class="sxs-lookup"><span data-stu-id="6a89c-262">Click **Set Source**.</span></span> 
5. <span data-ttu-id="6a89c-263">Testar a barra de controle deslizante.</span><span class="sxs-lookup"><span data-stu-id="6a89c-263">Test the slider bar.</span></span>

<span data-ttu-id="6a89c-264">Você concluiu a lição 2.</span><span class="sxs-lookup"><span data-stu-id="6a89c-264">You have completed lesson 2.</span></span>  <span data-ttu-id="6a89c-265">Nesta lição, você adicionou um controle deslizante ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6a89c-265">In this lesson you added a slider to application.</span></span> 

## <a name="lesson-3-select-smooth-streaming-streams"></a><span data-ttu-id="6a89c-266">Lição 3: Selecionar fluxos de Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="6a89c-266">Lesson 3: Select Smooth Streaming Streams</span></span>
<span data-ttu-id="6a89c-267">O Smooth Streaming é capaz de transmitir conteúdo com faixas de áudio de vários idiomas que podem ser selecionadas pelos visualizadores.</span><span class="sxs-lookup"><span data-stu-id="6a89c-267">Smooth Streaming is capable to stream content with multiple language audio tracks that are selectable by the viewers.</span></span>  <span data-ttu-id="6a89c-268">Nesta lição, você habilitará a seleção dos fluxos pelos visualizadores.</span><span class="sxs-lookup"><span data-stu-id="6a89c-268">In this lesson, you will enable viewers to select streams.</span></span> <span data-ttu-id="6a89c-269">Esta lição contém os seguintes procedimentos:</span><span class="sxs-lookup"><span data-stu-id="6a89c-269">This lesson contains the following procedures:</span></span>

1. <span data-ttu-id="6a89c-270">Modificar o arquivo XAML</span><span class="sxs-lookup"><span data-stu-id="6a89c-270">Modify the XAML file</span></span>
2. <span data-ttu-id="6a89c-271">Modificar o arquivo code-behind</span><span class="sxs-lookup"><span data-stu-id="6a89c-271">Modify the code behand file</span></span>
3. <span data-ttu-id="6a89c-272">Compilar e testar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="6a89c-272">Compile and test the application</span></span>

<span data-ttu-id="6a89c-273">**Para modificar o arquivo XAML**</span><span class="sxs-lookup"><span data-stu-id="6a89c-273">**To modify the XAML file**</span></span>

1. <span data-ttu-id="6a89c-274">No Gerenciador de Soluções, clique com o botão direito do mouse em **MainPage.xaml**, e, em seguida, clique em **Designer de Modos de Exibição**.</span><span class="sxs-lookup"><span data-stu-id="6a89c-274">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="6a89c-275">Localize &lt;Grid.RowDefinitions&gt; e modifique as RowDefinitions para que elas fiquem assim:</span><span class="sxs-lookup"><span data-stu-id="6a89c-275">Locate &lt;Grid.RowDefinitions&gt;, and modify the RowDefinitions so they looks like:</span></span>
   
         <Grid.RowDefinitions>            
            <RowDefinition Height="20"/>
            <RowDefinition Height="50"/>
            <RowDefinition Height="100"/>
            <RowDefinition Height="80"/>
            <RowDefinition Height="50"/>
         </Grid.RowDefinitions>
3. <span data-ttu-id="6a89c-276">Nas marcas &lt;Grid&gt;&lt;/Grid&gt;, adicione o seguinte código para definir um controle de caixa de listagem, para que os usuários possam ver a lista de fluxos disponíveis e selecioná-los:</span><span class="sxs-lookup"><span data-stu-id="6a89c-276">Inside the &lt;Grid&gt;&lt;/Grid&gt; tags, add the following code to define a listbox control, so users can see the list of available streams, and select streams:</span></span>

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
4. <span data-ttu-id="6a89c-277">Pressione **CTRL+S** para salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="6a89c-277">Press **CTRL+S** to save the changes.</span></span>

<span data-ttu-id="6a89c-278">**Para modificar o arquivo code-behind**</span><span class="sxs-lookup"><span data-stu-id="6a89c-278">**To modify the code behind file**</span></span>

1. <span data-ttu-id="6a89c-279">No Gerenciador de Soluções, clique com o botão direito do mouse em **MainPage.xaml** e clique em **Exibir Código**.</span><span class="sxs-lookup"><span data-stu-id="6a89c-279">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="6a89c-280">Dentro do namespace SSPlayer, adicione uma nova classe:</span><span class="sxs-lookup"><span data-stu-id="6a89c-280">Inside the SSPlayer namespace, add a new class:</span></span>
   
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
                    // mMke the video stream always checked.
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
3. <span data-ttu-id="6a89c-281">No início da classe MainPage, adicione as seguintes definições de variáveis:</span><span class="sxs-lookup"><span data-stu-id="6a89c-281">At the beginning of the MainPage class, add the following variable definitions:</span></span>
   
         private List<Stream> availableStreams;
         private List<Stream> availableAudioStreams;
         private List<Stream> availableTextStreams;
         private List<Stream> availableVideoStreams;
4. <span data-ttu-id="6a89c-282">Dentro da classe MainPage, adicione a seguinte região:</span><span class="sxs-lookup"><span data-stu-id="6a89c-282">Inside the MainPage class, add the following region:</span></span>
   
        #region stream selection
        ///<summary>
        ///Functionality to select streams from IManifestStream available streams
        /// </summary>
   
        // This function is called from the mediaElement_ManifestReady event handler 
        // to retrieve the streams and populate them to the local data members.
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
   
                    //populate the stream lists based on the types
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
   
                    // Select the default selected streams from the manifest.
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
   
        // This function set the list box ItemSource
        private async void refreshAvailableStreamsListBoxItemSource()
        {
            try
            {
                //update the stream check box list on the UI
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
   
            // Select the frist video stream from the list if no video stream is selected
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
                    txtStatus.Text = "The audio stream is changed to " + availableAudioStreams[j].ManifestStream.Name;
                }
            }
   
            // Select the frist audio stream from the list if no audio steam is selected.
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
5. <span data-ttu-id="6a89c-283">Localize o método mediaElement_ManifestReady e acrescente o seguinte código no final da função:</span><span class="sxs-lookup"><span data-stu-id="6a89c-283">Locate the mediaElement_ManifestReady method, append the following code at the end of the function:</span></span>
   
        getStreams(manifestObject);
        refreshAvailableStreamsListBoxItemSource();
   
    <span data-ttu-id="6a89c-284">Quando o manifesto MediaElement estiver pronto, o código obterá uma lista dos fluxos disponíveis e populará a caixa de listagem da interface do usuário com a lista.</span><span class="sxs-lookup"><span data-stu-id="6a89c-284">So when MediaElement manifest is ready, the code gets a list of the available streams, and populates the UI list box with the list.</span></span>
6. <span data-ttu-id="6a89c-285">Na classe MainPage, localize a região de eventos de cliques de botões da interface do usuário e adicione a seguinte definição de função:</span><span class="sxs-lookup"><span data-stu-id="6a89c-285">Inside the MainPage class, locate the UI buttons click events region, and then add the following function definition:</span></span>
   
        private void btnChangeStream_Click(object sender, RoutedEventArgs e)
        {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();
   
            // Create a list of the selected streams
            createSelectedStreamsList(selectedStreams);
   
            // Change streams on the presentation
            changeStreams(selectedStreams);
        }

<span data-ttu-id="6a89c-286">**Para compilar e testar o aplicativo**</span><span class="sxs-lookup"><span data-stu-id="6a89c-286">**To compile and test the application**</span></span>

1. <span data-ttu-id="6a89c-287">Pressione **F6** para compilar o projeto.</span><span class="sxs-lookup"><span data-stu-id="6a89c-287">Press **F6** to compile the project.</span></span> 
2. <span data-ttu-id="6a89c-288">Pressione **F5** para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6a89c-288">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="6a89c-289">Na parte superior do aplicativo, use a URL do Smooth Streaming padrão ou digite outra URL.</span><span class="sxs-lookup"><span data-stu-id="6a89c-289">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="6a89c-290">Clique em **Definir Origem**.</span><span class="sxs-lookup"><span data-stu-id="6a89c-290">Click **Set Source**.</span></span> 
5. <span data-ttu-id="6a89c-291">O idioma padrão é audio_eng.</span><span class="sxs-lookup"><span data-stu-id="6a89c-291">The default language is audio_eng.</span></span> <span data-ttu-id="6a89c-292">Tente alternar entre audio_eng e audio_es.</span><span class="sxs-lookup"><span data-stu-id="6a89c-292">Try to switch between audio_eng and audio_es.</span></span> <span data-ttu-id="6a89c-293">Toda vez que selecionar um novo fluxo, você deverá clicar no botão Enviar.</span><span class="sxs-lookup"><span data-stu-id="6a89c-293">Everytime, you select a new stream, you must click the Submit button.</span></span>

<span data-ttu-id="6a89c-294">Você concluiu a lição 3.</span><span class="sxs-lookup"><span data-stu-id="6a89c-294">You have completed lesson 3.</span></span>  <span data-ttu-id="6a89c-295">Nesta lição, você adicionará a funcionalidade de escolher fluxos.</span><span class="sxs-lookup"><span data-stu-id="6a89c-295">In this lesson, you add the functionality to choose streams.</span></span>

## <a name="lesson-4-select-smooth-streaming-tracks"></a><span data-ttu-id="6a89c-296">Lição 4: Selecionar faixas de Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="6a89c-296">Lesson 4: Select Smooth Streaming Tracks</span></span>
<span data-ttu-id="6a89c-297">Um apresentação de Smooth Streaming pode conter vários arquivos de vídeo codificados com diferentes níveis de qualidade (taxas de bits) e resoluções.</span><span class="sxs-lookup"><span data-stu-id="6a89c-297">A Smooth Streaming presentation can contain multiple video files encoded with different quality levels (bit rates) and resolutions.</span></span> <span data-ttu-id="6a89c-298">Nesta lição, você habilitará a seleção de faixas pelos usuários.</span><span class="sxs-lookup"><span data-stu-id="6a89c-298">In this lesson, you will enable users to select tracks.</span></span> <span data-ttu-id="6a89c-299">Esta lição contém os seguintes procedimentos:</span><span class="sxs-lookup"><span data-stu-id="6a89c-299">This lesson contains the following procedures:</span></span>

1. <span data-ttu-id="6a89c-300">Modificar o arquivo XAML</span><span class="sxs-lookup"><span data-stu-id="6a89c-300">Modify the XAML file</span></span>
2. <span data-ttu-id="6a89c-301">Modificar o arquivo code-behind</span><span class="sxs-lookup"><span data-stu-id="6a89c-301">Modify the code behand file</span></span>
3. <span data-ttu-id="6a89c-302">Compilar e testar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="6a89c-302">Compile and test the application</span></span>

<span data-ttu-id="6a89c-303">**Para modificar o arquivo XAML**</span><span class="sxs-lookup"><span data-stu-id="6a89c-303">**To modify the XAML file**</span></span>

1. <span data-ttu-id="6a89c-304">No Gerenciador de Soluções, clique com o botão direito do mouse em **MainPage.xaml**, e, em seguida, clique em **Designer de Modos de Exibição**.</span><span class="sxs-lookup"><span data-stu-id="6a89c-304">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="6a89c-305">Localize a marca &lt;Grid&gt; com o nome **gridStreamAndBitrateSelection** e acrescente o seguinte código ao final da marca:</span><span class="sxs-lookup"><span data-stu-id="6a89c-305">Locate the &lt;Grid&gt; tag with the name **gridStreamAndBitrateSelection**, append the following code at the end of the tag:</span></span>
   
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
3. <span data-ttu-id="6a89c-306">Pressione **CTRL+S** para salvar as alterações</span><span class="sxs-lookup"><span data-stu-id="6a89c-306">Press **CTRL+S** to save he changes</span></span>

<span data-ttu-id="6a89c-307">**Para modificar o arquivo code-behind**</span><span class="sxs-lookup"><span data-stu-id="6a89c-307">**To modify the code behind file**</span></span>

1. <span data-ttu-id="6a89c-308">No Gerenciador de Soluções, clique com o botão direito do mouse em **MainPage.xaml** e clique em **Exibir Código**.</span><span class="sxs-lookup"><span data-stu-id="6a89c-308">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="6a89c-309">Dentro do namespace SSPlayer, adicione uma nova classe:</span><span class="sxs-lookup"><span data-stu-id="6a89c-309">Inside the SSPlayer namespace, add a new class:</span></span>
   
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
3. <span data-ttu-id="6a89c-310">No início da classe MainPage, adicione as seguintes definições de variáveis:</span><span class="sxs-lookup"><span data-stu-id="6a89c-310">At the beginning of the MainPage class, add the following variable definitions:</span></span>
   
        private List<Track> availableTracks;
4. <span data-ttu-id="6a89c-311">Dentro da classe MainPage, adicione a seguinte região:</span><span class="sxs-lookup"><span data-stu-id="6a89c-311">Inside the MainPage class, add the following region:</span></span>
   
        #region track selection
        /// <summary>
        /// Functionality to select video streams
        /// </summary>
   
        /// This Function gets the tracks for the selected video stream
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
   
        // This function gets the video stream that is playing
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
   
        // This function set the UI list box control ItemSource
        private async void refreshAvailableTracksListBoxItemSource()
        {
            try
            {
                // Update the track check box list on the UI 
                await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, ()
                    => { lbAvailableVideoTracks.ItemsSource = availableTracks; });
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }        
        }
   
        // This function creates a list of the selected tracks.
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
   
        // This function selects the tracks based on user selection 
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
5. <span data-ttu-id="6a89c-312">Localize o método mediaElement_ManifestReady e acrescente o seguinte código no final da função:</span><span class="sxs-lookup"><span data-stu-id="6a89c-312">Locate the mediaElement_ManifestReady method, append the following code at the end of the function:</span></span>
   
         getTracks(manifestObject);
         refreshAvailableTracksListBoxItemSource();
6. <span data-ttu-id="6a89c-313">Na classe MainPage, localize a região de eventos de cliques de botões da interface do usuário e adicione a seguinte definição de função:</span><span class="sxs-lookup"><span data-stu-id="6a89c-313">Inside the MainPage class, locate the UI buttons click events region, and then add the following function definition:</span></span>
   
         private void btnChangeStream_Click(object sender, RoutedEventArgs e)
         {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();

            // Create a list of the selected streams
            createSelectedStreamsList(selectedStreams);

            // Change streams on the presentation
            changeStreams(selectedStreams);
         }

<span data-ttu-id="6a89c-314">**Para compilar e testar o aplicativo**</span><span class="sxs-lookup"><span data-stu-id="6a89c-314">**To compile and test the application**</span></span>

1. <span data-ttu-id="6a89c-315">Pressione **F6** para compilar o projeto.</span><span class="sxs-lookup"><span data-stu-id="6a89c-315">Press **F6** to compile the project.</span></span> 
2. <span data-ttu-id="6a89c-316">Pressione **F5** para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6a89c-316">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="6a89c-317">Na parte superior do aplicativo, use a URL do Smooth Streaming padrão ou digite outra URL.</span><span class="sxs-lookup"><span data-stu-id="6a89c-317">At the top of the application, you can either use the default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="6a89c-318">Clique em **Definir Origem**.</span><span class="sxs-lookup"><span data-stu-id="6a89c-318">Click **Set Source**.</span></span> 
5. <span data-ttu-id="6a89c-319">Por padrão, todas as faixas do fluxo de vídeo são selecionadas.</span><span class="sxs-lookup"><span data-stu-id="6a89c-319">By default, all of the tracks of the video stream are selected.</span></span> <span data-ttu-id="6a89c-320">Para testar as alterações de taxa de bits, é possível selecionar a taxa de bits mais baixa disponível e, em seguida, selecionar a taxa de bits mais alta disponível.</span><span class="sxs-lookup"><span data-stu-id="6a89c-320">To experiment the bit rate changes, you can select the lowest bit rate available, and then select the highest bit rate available.</span></span> <span data-ttu-id="6a89c-321">Você deve clicar em Enviar após cada alteração.</span><span class="sxs-lookup"><span data-stu-id="6a89c-321">You must click Submit after each change.</span></span>  <span data-ttu-id="6a89c-322">Você pode ver as alterações na qualidade do vídeo.</span><span class="sxs-lookup"><span data-stu-id="6a89c-322">You can see the video quality changes.</span></span>

<span data-ttu-id="6a89c-323">Você concluiu a lição 4.</span><span class="sxs-lookup"><span data-stu-id="6a89c-323">You have completed lesson 4.</span></span>  <span data-ttu-id="6a89c-324">Nesta lição, você adicionará a funcionalidade de escolher faixas.</span><span class="sxs-lookup"><span data-stu-id="6a89c-324">In this lesson, you add the functionality to choose tracks.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="6a89c-325">Roteiros de aprendizagem dos Serviços de Mídia</span><span class="sxs-lookup"><span data-stu-id="6a89c-325">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="6a89c-326">Fornecer comentários</span><span class="sxs-lookup"><span data-stu-id="6a89c-326">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="other-resources"></a><span data-ttu-id="6a89c-327">Outros recursos:</span><span class="sxs-lookup"><span data-stu-id="6a89c-327">Other Resources:</span></span>
* [<span data-ttu-id="6a89c-328">Como criar um aplicativo JavaScript de Smooth Streaming do Windows 8 com recursos avançados</span><span class="sxs-lookup"><span data-stu-id="6a89c-328">How to build a Smooth Streaming Windows 8 JavaScript application with advanced features</span></span>](http://blogs.iis.net/cenkd/archive/2012/08/10/how-to-build-a-smooth-streaming-windows-8-javascript-application-with-advanced-features.aspx)
* [<span data-ttu-id="6a89c-329">Visão Geral Técnica de Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="6a89c-329">Smooth Streaming Technical Overview</span></span>](http://www.iis.net/learn/media/on-demand-smooth-streaming/smooth-streaming-technical-overview)

[PlayerApplication]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-1.png
[CodeViewPic]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-2.png

