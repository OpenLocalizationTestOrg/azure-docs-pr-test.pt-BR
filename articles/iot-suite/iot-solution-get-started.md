---
title: "Exemplo do Azure IoT do MyDriving: Início rápido | Microsoft Docs"
description: "Começar com um aplicativo que é uma abrangente demonstração de como tooarchitect um sistema IoT usando o Microsoft Azure, incluindo análise de fluxo, aprendizado de máquina e Hubs de eventos."
services: 
documentationcenter: .net
suite: 
author: harikmenon
manager: douge
ms.assetid: f40ea71b-5721-4a6b-a886-53c2e9dffe8f
ms.service: multiple
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: dotnet
ms.topic: article
ms.date: 03/25/2016
ms.author: harikm
ms.openlocfilehash: 411b9a992deb22b915f8291d8559e2917d976b2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="mydriving-iot-system-quick-start"></a><span data-ttu-id="81381-103">Sistema de IoT MyDriving: início rápido</span><span class="sxs-lookup"><span data-stu-id="81381-103">MyDriving IoT system: Quick start</span></span>
<span data-ttu-id="81381-104">MyDriving é um sistema que demonstra o design de saudação e a implementação de um típico [Internet das coisas](iot-suite-overview.md) solução (IoT) que coleta a telemetria de dispositivos, processa esses dados na nuvem hello e aplica o aprendizado de máquina tooprovide uma resposta adaptável.</span><span class="sxs-lookup"><span data-stu-id="81381-104">MyDriving is a system that demonstrates hello design and implementation of a typical [Internet of Things](iot-suite-overview.md) (IoT) solution that gathers telemetry from devices, processes that data in hello cloud, and applies machine learning tooprovide an adaptive response.</span></span> <span data-ttu-id="81381-105">demonstração de Olá registra dados sobre viagens seu carro, usando dados de seu telefone celular e um adaptador que coleta informações do sistema de controle do carro.</span><span class="sxs-lookup"><span data-stu-id="81381-105">hello demonstration logs data about your car trips, by using data from both your mobile phone and an adapter that collects information from your car’s control system.</span></span> <span data-ttu-id="81381-106">Ele usa este comentário tooprovide de dados no seu estilo de como os usuários tooother de comparação.</span><span class="sxs-lookup"><span data-stu-id="81381-106">It uses this data tooprovide feedback on your driving style in comparison tooother users.</span></span>

<span data-ttu-id="81381-107">Olá finalidade real MyDriving é tooget iniciado na criação de sua própria solução de IoT.</span><span class="sxs-lookup"><span data-stu-id="81381-107">hello real purpose of MyDriving is tooget you started in creating your own IoT solution.</span></span> <span data-ttu-id="81381-108">Mas, antes disso, vamos sobre Olá MyDriving aplicativo em si – como um membro da nossa equipe de usuário de teste.</span><span class="sxs-lookup"><span data-stu-id="81381-108">But before that, let’s get you going with hello MyDriving app itself--as a member of our test user team.</span></span> <span data-ttu-id="81381-109">Isso fornece uma experiência de aplicativo hello e sistema de saudação por trás dela como um consumidor, antes de se a arquitetura de saudação.</span><span class="sxs-lookup"><span data-stu-id="81381-109">This gives you an experience of hello app and hello system behind it as a consumer, before you delve into hello architecture.</span></span> <span data-ttu-id="81381-110">Ele também apresenta tooHockeyApp, uma maneira interessante de distribuições de saudação alfa e beta dos usuários tootest aplicativos de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="81381-110">It also introduces you tooHockeyApp, a cool way of managing hello alpha and beta distributions of your apps tootest users.</span></span>

## <a name="use-hello-mobile-experience"></a><span data-ttu-id="81381-111">Use a experiência móvel Olá</span><span class="sxs-lookup"><span data-stu-id="81381-111">Use hello mobile experience</span></span>
<span data-ttu-id="81381-112">Você pode usar o hello MyDriving aplicativo se você tiver um dispositivo Android, iOS ou Windows 10.</span><span class="sxs-lookup"><span data-stu-id="81381-112">You can use hello MyDriving app if you have an Android, iOS, or Windows 10 device.</span></span>

### <a name="android-and-windows-10-mobile-installation"></a><span data-ttu-id="81381-113">Instalação do Android e do Windows Mobile 10</span><span class="sxs-lookup"><span data-stu-id="81381-113">Android and Windows 10 Mobile installation</span></span>
<span data-ttu-id="81381-114">Em seu dispositivo:</span><span class="sxs-lookup"><span data-stu-id="81381-114">On your device:</span></span>

1. <span data-ttu-id="81381-115">Permitir aplicativos de desenvolvimento:</span><span class="sxs-lookup"><span data-stu-id="81381-115">Allow development apps:</span></span>
   
   * <span data-ttu-id="81381-116">Android: em **Configurações** > **Segurança**, permita aplicativos de **Fontes desconhecidas**.</span><span class="sxs-lookup"><span data-stu-id="81381-116">Android: In **Settings** > **Security**, allow apps from **Unknown sources**.</span></span>
   * <span data-ttu-id="81381-117">Windows 10: em **Configurações** > **Atualizações** > **Para Desenvolvedores**, defina o **Modo de desenvolvedor**.</span><span class="sxs-lookup"><span data-stu-id="81381-117">Windows 10: In **Settings** > **Updates** > **For Developers**, set **Developer mode**.</span></span>
2. <span data-ttu-id="81381-118">Junte-se à nossa equipe de teste beta inscrevendo-se ou entrando no [HockeyApp](https://rink.hockeyapp.net).</span><span class="sxs-lookup"><span data-stu-id="81381-118">Join our beta test team by signing up with, or signing in to, [HockeyApp](https://rink.hockeyapp.net).</span></span> <span data-ttu-id="81381-119">HockeyApp torna fácil toodistribute primeiras versões dos seus usuários de tootest do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="81381-119">HockeyApp makes it easy toodistribute early releases of your app tootest users.</span></span>
   
   <span data-ttu-id="81381-120">Se você estiver usando o Windows 10, use o navegador de borda de saudação.</span><span class="sxs-lookup"><span data-stu-id="81381-120">If you’re using Windows 10, use hello Edge browser.</span></span>
   
   <span data-ttu-id="81381-121">Se você fosse um participante de compilação 2016, entrar com hello mesmo email de conta da Microsoft que você registrou para conferência hello, usando uma saudação botões da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="81381-121">If you were a Build 2016 attendee, sign in with hello same Microsoft account email that you registered for hello conference, by using one of hello Microsoft buttons.</span></span> <span data-ttu-id="81381-122">Você já se inscreveu no HockeyApp.</span><span class="sxs-lookup"><span data-stu-id="81381-122">You’re already signed up with HockeyApp.</span></span>
   
   ![Tela de entrada do HockeyApp](./media/iot-solution-get-started/image1.png)
3. <span data-ttu-id="81381-124">Baixe e instale o aplicativo hello aqui:</span><span class="sxs-lookup"><span data-stu-id="81381-124">Download and install hello app from here:</span></span>
   
   * [<span data-ttu-id="81381-125">Android</span><span class="sxs-lookup"><span data-stu-id="81381-125">Android</span></span>](http://rink.io/spMyDrivingAndroid)
   * [<span data-ttu-id="81381-126">Windows 10</span><span class="sxs-lookup"><span data-stu-id="81381-126">Windows 10</span></span>](http://rink.io/spMyDrivingUWP)
   
   <span data-ttu-id="81381-127">Há dois itens.</span><span class="sxs-lookup"><span data-stu-id="81381-127">There are two items.</span></span> <span data-ttu-id="81381-128">Instalar certificado Olá no **pessoas confiáveis**.</span><span class="sxs-lookup"><span data-stu-id="81381-128">Install hello certificate in **Trusted People**.</span></span> <span data-ttu-id="81381-129">Em seguida, instale o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="81381-129">Then install hello app.</span></span>

<span data-ttu-id="81381-130">*Problemas ao iniciar o aplicativo hello no Windows 10 Mobile?*</span><span class="sxs-lookup"><span data-stu-id="81381-130">*Any issues starting hello app on Windows 10 Mobile?*</span></span> <span data-ttu-id="81381-131">Talvez seu telefone esteja com uma ou duas atualizações atrasadas.</span><span class="sxs-lookup"><span data-stu-id="81381-131">Your phone might be an update or two behind.</span></span> <span data-ttu-id="81381-132">Verifique se você tem as atualizações mais recentes do hello, ou instala:</span><span class="sxs-lookup"><span data-stu-id="81381-132">Make sure you've got hello latest updates, or install:</span></span>

* [<span data-ttu-id="81381-133">Microsoft.NET.Native.Framework.1.2.appx</span><span class="sxs-lookup"><span data-stu-id="81381-133">Microsoft.NET.Native.Framework.1.2.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Framework.1.2.appx) 
* [<span data-ttu-id="81381-134">Microsoft.NET.Native.Runtime.1.1.appx</span><span class="sxs-lookup"><span data-stu-id="81381-134">Microsoft.NET.Native.Runtime.1.1.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Runtime.1.1.appx) 
* [<span data-ttu-id="81381-135">Microsoft.VCLibs.ARM.14.00.appx</span><span class="sxs-lookup"><span data-stu-id="81381-135">Microsoft.VCLibs.ARM.14.00.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.VCLibs.ARM.14.00.appx)

### <a name="ios-installation"></a><span data-ttu-id="81381-136">Instalação do iOS</span><span class="sxs-lookup"><span data-stu-id="81381-136">iOS installation</span></span>
<span data-ttu-id="81381-137">Se você participou 2016 de compilação, baixe o aplicativo de hello como um membro da nossa equipe de teste em HockeyApp:</span><span class="sxs-lookup"><span data-stu-id="81381-137">If you attended Build 2016, download hello app as a member of our test team on HockeyApp:</span></span>

1. <span data-ttu-id="81381-138">Em seu dispositivo iOS, entrar muito[HockeyApp](https://rink.hockeyapp.net).</span><span class="sxs-lookup"><span data-stu-id="81381-138">On your iOS device, sign in too[HockeyApp](https://rink.hockeyapp.net).</span></span>
   <span data-ttu-id="81381-139">Use uma saudação botões entrar Microsoft e entrar no hello email de conta Microsoft mesmo que você registrou com conferência hello.</span><span class="sxs-lookup"><span data-stu-id="81381-139">Use one of hello Microsoft sign-in buttons, and sign in with hello same Microsoft account email that you registered with hello conference.</span></span> <span data-ttu-id="81381-140">(Não use campos Olá de email e senha).</span><span class="sxs-lookup"><span data-stu-id="81381-140">(Don’t use hello email and password fields.)</span></span>
   
   ![Tela de entrada do HockeyApp](./media/iot-solution-get-started/image1.png)
2. <span data-ttu-id="81381-142">No painel do HockeyApp hello, selecione MyDriving e baixá-lo.</span><span class="sxs-lookup"><span data-stu-id="81381-142">In hello HockeyApp dashboard, select MyDriving and download it.</span></span>
3. <span data-ttu-id="81381-143">Autorize a versão beta de saudação do HockeyApp:</span><span class="sxs-lookup"><span data-stu-id="81381-143">Authorize hello beta release from HockeyApp:</span></span>
   
   <span data-ttu-id="81381-144">a.</span><span class="sxs-lookup"><span data-stu-id="81381-144">a.</span></span> <span data-ttu-id="81381-145">Vá muito**configurações** > **geral** > **perfis e gerenciamento de dispositivo.**</span><span class="sxs-lookup"><span data-stu-id="81381-145">Go too**Settings** > **General** > **Profiles and Device Management.**</span></span>
   
   <span data-ttu-id="81381-146">b.</span><span class="sxs-lookup"><span data-stu-id="81381-146">b.</span></span> <span data-ttu-id="81381-147">Saudação de confiança **Bit Estádio GmbH** certificado.</span><span class="sxs-lookup"><span data-stu-id="81381-147">Trust hello **Bit Stadium GmbH** certificate.</span></span>

<span data-ttu-id="81381-148">Se não frequentou 2016 de compilação, você pode criar e implantar o aplicativo hello por conta própria:</span><span class="sxs-lookup"><span data-stu-id="81381-148">If you didn’t attend Build 2016, you can build and deploy hello app yourself:</span></span>

1. <span data-ttu-id="81381-149">Baixar o código de saudação [do GitHub].</span><span class="sxs-lookup"><span data-stu-id="81381-149">Download hello code [from GitHub].</span></span>
2. <span data-ttu-id="81381-150">Crie e implante [usando o Xamarin].</span><span class="sxs-lookup"><span data-stu-id="81381-150">Build and deploy by [using Xamarin].</span></span>

<span data-ttu-id="81381-151">Encontrar mais detalhes no hello [guia de referência MyDriving](http://aka.ms/mydrivingdocs).</span><span class="sxs-lookup"><span data-stu-id="81381-151">Find more details in hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs).</span></span>

## <a name="get-an-obd-adapter-optional"></a><span data-ttu-id="81381-152">Obter um adaptador OBD (opcional)</span><span class="sxs-lookup"><span data-stu-id="81381-152">Get an OBD adapter (optional)</span></span>
<span data-ttu-id="81381-153">Isso faz parte de saudação que torna isso um sistema real de Internet das coisas!</span><span class="sxs-lookup"><span data-stu-id="81381-153">This is hello part that makes this a real Internet of Things system!</span></span> <span data-ttu-id="81381-154">Você pode usar o aplicativo hello sem uma, mas é divertido mais com algo real hello e não são caras.</span><span class="sxs-lookup"><span data-stu-id="81381-154">You can use hello app without one, but it’s more fun with hello real thing, and they aren’t expensive.</span></span>

<span data-ttu-id="81381-155">Diagnóstico integrado (OBD) é o recurso de saudação do seu carro Olá garagem usa tootune o carro e diagnosticar ruídos ímpares e lâmpadas de aviso.</span><span class="sxs-lookup"><span data-stu-id="81381-155">On-board diagnostics (OBD) is hello feature of your car that hello garage uses tootune up your car and diagnose odd noises and warning lamps.</span></span> <span data-ttu-id="81381-156">A menos que seu carro de época excelente, você encontrará um soquete em algum lugar na cabine hello, normalmente por trás flap no painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="81381-156">Unless your car is of great antiquity, you’ll find a socket somewhere in hello cabin, typically behind a flap under hello dashboard.</span></span> <span data-ttu-id="81381-157">Com o conector de direito hello, você pode obter métricas de desempenho do mecanismo de saudação e fazer alguns ajustes.</span><span class="sxs-lookup"><span data-stu-id="81381-157">With hello right connector, you can get metrics of hello engine’s performance and make certain adjustments.</span></span> <span data-ttu-id="81381-158">Um conector OBD pode ser adquirido barata de locais de saudação normal.</span><span class="sxs-lookup"><span data-stu-id="81381-158">An OBD connector can be purchased cheaply from hello usual places.</span></span> <span data-ttu-id="81381-159">Ele se conecta usando o aplicativo de tooan Bluetooth ou Wi-Fi em seu telefone.</span><span class="sxs-lookup"><span data-stu-id="81381-159">It connects by using Bluetooth or Wi-Fi tooan app on your phone.</span></span>

<span data-ttu-id="81381-160">Nesse caso, vamos tooconnect sua nuvem de toohello de carro.</span><span class="sxs-lookup"><span data-stu-id="81381-160">In this case, we’re going tooconnect your car toohello cloud.</span></span> <span data-ttu-id="81381-161">conexão direta de saudação do hello OBD é tooyour telefone, mas nosso aplicativo funciona como um retransmissor.</span><span class="sxs-lookup"><span data-stu-id="81381-161">hello direct connection from hello OBD is tooyour phone, but our app works as a relay.</span></span> <span data-ttu-id="81381-162">Telemetria do carro será enviada reta toohello MyDriving IoT hub, onde ela é processada toolog sua viagem e avaliar seu estilo de referências.</span><span class="sxs-lookup"><span data-stu-id="81381-162">Your car's telemetry is sent straight toohello MyDriving IoT hub, where it's processed toolog your road trips and assess your driving style.</span></span>

<span data-ttu-id="81381-163">tooconnect um dispositivo OBD:</span><span class="sxs-lookup"><span data-stu-id="81381-163">tooconnect an OBD device:</span></span>

1. <span data-ttu-id="81381-164">Verifique se seu carro tem um soquete OBD.</span><span class="sxs-lookup"><span data-stu-id="81381-164">Check that your car has an OBD socket.</span></span>
2. <span data-ttu-id="81381-165">Obtenha um adaptador OBD:</span><span class="sxs-lookup"><span data-stu-id="81381-165">Obtain an OBD adapter:</span></span>
   
   * <span data-ttu-id="81381-166">Se estiver usando um telefone Android ou Windows, você precisará de um adaptador OBD II habilitado para Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="81381-166">If you're using an Android or Windows phone, you need a Bluetooth-enabled OBD II adapter.</span></span> <span data-ttu-id="81381-167">Usamos a [Ferramenta de Digitalização BAFX Products 34t5 Bluetooth OBDII].</span><span class="sxs-lookup"><span data-stu-id="81381-167">We used [BAFX Products 34t5 Bluetooth OBDII Scan Tool].</span></span>
   * <span data-ttu-id="81381-168">Se estiver usando um telefone iOS, você precisará de um adaptador OBD habilitado para Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="81381-168">If you're using an iOS phone, you need a Wi-Fi-enabled OBD adapter.</span></span> <span data-ttu-id="81381-169">Usamos a [Ferramenta de Digitalização OBDLink MX Wi-Fi: scanner de adaptador/diagnóstico OBD].</span><span class="sxs-lookup"><span data-stu-id="81381-169">We used [ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner].</span></span>
3. <span data-ttu-id="81381-170">Siga as instruções de saudação que vêm com o tooconnect de adaptador OBD-tooyour telefone.</span><span class="sxs-lookup"><span data-stu-id="81381-170">Follow hello instructions that come with your OBD adapter tooconnect it tooyour phone.</span></span> <span data-ttu-id="81381-171">Lembre-Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="81381-171">Keep hello following in mind:</span></span>
   
   * <span data-ttu-id="81381-172">Um adaptador Bluetooth deve estar combinado com telefone hello, Olá **configurações** página.</span><span class="sxs-lookup"><span data-stu-id="81381-172">A Bluetooth adapter must be paired with hello phone, on hello **Settings** page.</span></span>
   * <span data-ttu-id="81381-173">Um adaptador de Wi-Fi deve ter um endereço no 192.168.xxx.xxx de intervalo de saudação.</span><span class="sxs-lookup"><span data-stu-id="81381-173">A Wi-Fi adapter must have an address in hello range 192.168.xxx.xxx.</span></span>
4. <span data-ttu-id="81381-174">Se tiver vários carros, você poderá obter um adaptador separado para cada (no máximo três).</span><span class="sxs-lookup"><span data-stu-id="81381-174">If you have several cars, you can get a separate adapter for each (maximum of three).</span></span>

<span data-ttu-id="81381-175">Se você não tiver um adaptador OBD, aplicativo hello ainda enviará local e dados de velocidade de toohello de receptor GPS do telefone Olá volta terminar e perguntará se você quiser toosimulate um OBD.</span><span class="sxs-lookup"><span data-stu-id="81381-175">If you don’t have an OBD adapter, hello app will still send location and speed data from hello phone's GPS receiver toohello back end and will ask if you want toosimulate an OBD.</span></span>

<span data-ttu-id="81381-176">Você pode encontrar mais informações sobre como o aplicativo hello usa dados de saudação OBD adaptador e sobre as opções para criar seu próprio dispositivo OBD na seção 2.1, "Dispositivos IoT", no hello [guia de referência MyDriving](http://aka.ms/mydrivingdocs).</span><span class="sxs-lookup"><span data-stu-id="81381-176">You can find out more about how hello app uses data from hello OBD adapter and about options for creating your own OBD device in section 2.1, "IoT Devices," in hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs).</span></span>

## <a name="use-hello-app"></a><span data-ttu-id="81381-177">Usar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="81381-177">Use hello app</span></span>
<span data-ttu-id="81381-178">Inicie aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="81381-178">Start hello app.</span></span> <span data-ttu-id="81381-179">Há um toowalk inicial de início rápido você por meio de como ele funciona.</span><span class="sxs-lookup"><span data-stu-id="81381-179">There’s an initial Quickstart toowalk you through how it works.</span></span>

### <a name="track-your-trips"></a><span data-ttu-id="81381-180">Acompanhar suas viagens</span><span class="sxs-lookup"><span data-stu-id="81381-180">Track your trips</span></span>
<span data-ttu-id="81381-181">Olá botão Registro (círculo vermelho grande na parte inferior da saudação da tela hello) toostart uma viagem de toque e toque novamente tooend.</span><span class="sxs-lookup"><span data-stu-id="81381-181">Tap hello record button (big red circle at hello bottom of hello screen) toostart a trip, and tap again tooend.</span></span>

![Ilustração do botão de registro Olá para viagem de controle](./media/iot-solution-get-started/image2.png)

<span data-ttu-id="81381-183">Cada vez que você iniciar uma viagem, se não houver nenhum dispositivo OBD, será perguntado se você quiser que o simulador de saudação toouse.</span><span class="sxs-lookup"><span data-stu-id="81381-183">Each time you start a trip, if there’s no OBD device, you’ll be asked if you want toouse hello simulator.</span></span>

<span data-ttu-id="81381-184">Final de saudação de uma viagem, toque Olá parar botão e, obter um resumo.</span><span class="sxs-lookup"><span data-stu-id="81381-184">At hello end of a trip, tap hello stop button, and you get a summary.</span></span>

![Exemplo de um resumo de viagem](./media/iot-solution-get-started/image3.png)

### <a name="review-your-trips"></a><span data-ttu-id="81381-186">Examinar suas viagens</span><span class="sxs-lookup"><span data-stu-id="81381-186">Review your trips</span></span>
![Exemplo de uma viagem anterior](./media/iot-solution-get-started/image4.png)

### <a name="review-your-profile"></a><span data-ttu-id="81381-188">Examinar seu perfil</span><span class="sxs-lookup"><span data-stu-id="81381-188">Review your profile</span></span>
![Exemplo de um perfil de estilo de conduzir](./media/iot-solution-get-started/image5.png)

## <a name="send-us-your-test-feedback"></a><span data-ttu-id="81381-190">Envie-nos seus comentários sobre o teste</span><span class="sxs-lookup"><span data-stu-id="81381-190">Send us your test feedback</span></span>
<span data-ttu-id="81381-191">Como criamos MyDriving toohelp iniciar seus próprios sistemas de IoT, queremos certamente toohear você sobre como ele funciona.</span><span class="sxs-lookup"><span data-stu-id="81381-191">Because we created MyDriving toohelp jumpstart your own IoT systems, we certainly want toohear from you about how well it works.</span></span> <span data-ttu-id="81381-192">Fale conosco se:</span><span class="sxs-lookup"><span data-stu-id="81381-192">Let us know if:</span></span>

* <span data-ttu-id="81381-193">Você encontra dificuldades ou desafios.</span><span class="sxs-lookup"><span data-stu-id="81381-193">You run into difficulties or challenges.</span></span>
* <span data-ttu-id="81381-194">Há um ponto de extensão para que seja mais adequada do cenário de tooyour.</span><span class="sxs-lookup"><span data-stu-id="81381-194">There is an extension point that would make it more suitable tooyour scenario.</span></span>
* <span data-ttu-id="81381-195">Você encontrar um tooaccomplish de maneira mais eficiente determinadas necessidades.</span><span class="sxs-lookup"><span data-stu-id="81381-195">You find a more efficient way tooaccomplish certain needs.</span></span>
* <span data-ttu-id="81381-196">Você tem outras sugestões para melhorar o MyDriving ou essa documentação.</span><span class="sxs-lookup"><span data-stu-id="81381-196">You have any other suggestions for improving MyDriving or this documentation.</span></span>

<span data-ttu-id="81381-197">No hello MyDriving o aplicativo em si, você pode usar o mecanismo de comentários do HockeyApp interno Olá: no iOS e Android, é só atribuir seu telefone uma agitação ou use Olá **comentários** comando de menu.</span><span class="sxs-lookup"><span data-stu-id="81381-197">Within hello MyDriving app itself, you can use hello built-in HockeyApp feedback mechanism: on iOS and Android, just give your phone a shake, or use hello **Feedback** menu command.</span></span> <span data-ttu-id="81381-198">Isso automaticamente anexa uma captura de tela para que saibamos sobre o que você está falando.</span><span class="sxs-lookup"><span data-stu-id="81381-198">This will automatically attach a screenshot, so that we’ll know what you’re talking about.</span></span> <span data-ttu-id="81381-199">E se houver quaisquer falhas ruim, HockeyApp coleta Olá falha logs tootell nos sobre eles.</span><span class="sxs-lookup"><span data-stu-id="81381-199">And if there are any unfortunate crashes, HockeyApp collects hello crash logs tootell us about them.</span></span> <span data-ttu-id="81381-200">Você também pode fornecer comentários por meio de saudação [HockeyApp portal].</span><span class="sxs-lookup"><span data-stu-id="81381-200">You can also give feedback through hello [HockeyApp portal].</span></span>

<span data-ttu-id="81381-201">Também é possível arquivar um [problema no GitHub], ou deixar um comentário abaixo (edição en-us).</span><span class="sxs-lookup"><span data-stu-id="81381-201">You can also file an [issue on GitHub], or leave a comment below (en-us edition).</span></span>

<span data-ttu-id="81381-202">Aguardamos toohearing você!</span><span class="sxs-lookup"><span data-stu-id="81381-202">We look forward toohearing from you!</span></span>

## <a name="next-steps"></a><span data-ttu-id="81381-203">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="81381-203">Next steps</span></span>
* <span data-ttu-id="81381-204">Explorar Olá [guia de referência de MyDriving](http://aka.ms/mydrivingdocs) toounderstand como é projetado e criado Olá MyDriving todo o sistema.</span><span class="sxs-lookup"><span data-stu-id="81381-204">Explore hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs) toounderstand how we’ve designed and built hello entire MyDriving system.</span></span>
* <span data-ttu-id="81381-205">[Crie e implante um sistema por conta própria](iot-solution-build-system.md) usando nossos scripts do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="81381-205">[Create and deploy a system of your own](iot-solution-build-system.md) by using our Azure Resource Manager scripts.</span></span> <span data-ttu-id="81381-206">Olá [guia de referência MyDriving](http://aka.ms/mydrivingdocs) também orienta você através das áreas onde você vai fazer Olá a maioria das personalizações.</span><span class="sxs-lookup"><span data-stu-id="81381-206">hello [MyDriving Reference Guide](http://aka.ms/mydrivingdocs) also guides you through areas where you’ll make hello most customizations.</span></span>

[do GitHub]: https://github.com/Azure-Samples/MyDriving
[usando o Xamarin]: https://developer.xamarin.com/guides/ios/getting_started/installation/
[Ferramenta de Digitalização BAFX Products 34t5 Bluetooth OBDII]: http://www.amazon.com/gp/product/B005NLQAHS
[Ferramenta de Digitalização OBDLink MX Wi-Fi: scanner de adaptador/diagnóstico OBD]: http://www.amazon.com/gp/product/B00OCYXTYY/ref=s9_simh_gw_g263_i1_r?pf_rd_m=ATVPDKIKX0DER&pf_rd_s=desktop-2&pf_rd_r=1MWRMKXK4KK9VYMJ44MP
[HockeyApp portal]: https://rink.hockeyapp.org
[problema no GitHub]: https://github.com/Azure-Samples/MyDriving/issues
