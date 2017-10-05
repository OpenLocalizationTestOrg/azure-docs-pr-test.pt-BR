---
title: "Exemplo do Azure IoT do MyDriving: Início rápido | Microsoft Docs"
description: "Introdução a um aplicativo que apresenta uma demonstração abrangente de como projetar um sistema de IoT usando o Microsoft Azure, incluindo o Stream Analytics, o Machine Learning e os Hubs de Eventos."
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
ms.openlocfilehash: 031b492df1f186087e7b91102cbb44f552999293
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="mydriving-iot-system-quick-start"></a><span data-ttu-id="9f1e7-103">Sistema de IoT MyDriving: início rápido</span><span class="sxs-lookup"><span data-stu-id="9f1e7-103">MyDriving IoT system: Quick start</span></span>
<span data-ttu-id="9f1e7-104">O MyDriving é um sistema que demonstra o design e a implementação de uma solução típica de [IoT](iot-suite-overview.md) (Internet das Coisas), que coleta a telemetria dos dispositivos, processa esses dados na nuvem e aplica o aprendizado de máquina para fornecer uma resposta adaptável.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-104">MyDriving is a system that demonstrates the design and implementation of a typical [Internet of Things](iot-suite-overview.md) (IoT) solution that gathers telemetry from devices, processes that data in the cloud, and applies machine learning to provide an adaptive response.</span></span> <span data-ttu-id="9f1e7-105">A demonstração registra os dados das suas viagens de carro, usando os dados tanto de seu telefone celular quanto de um adaptador que coleta informações do sistema de controle do carro.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-105">The demonstration logs data about your car trips, by using data from both your mobile phone and an adapter that collects information from your car’s control system.</span></span> <span data-ttu-id="9f1e7-106">Ele usa esses dados para fornecer comentários sobre o seu estilo de conduzir em comparação com outros usuários.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-106">It uses this data to provide feedback on your driving style in comparison to other users.</span></span>

<span data-ttu-id="9f1e7-107">A finalidade real do MyDriving é ensiná-lo a criar sua própria solução de IoT.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-107">The real purpose of MyDriving is to get you started in creating your own IoT solution.</span></span> <span data-ttu-id="9f1e7-108">Mas antes disso, vamos apresentá-lo ao uso do aplicativo MyDriving – como membro de nossa equipe de usuário de teste.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-108">But before that, let’s get you going with the MyDriving app itself--as a member of our test user team.</span></span> <span data-ttu-id="9f1e7-109">Isso proporciona a você uma experiência do aplicativo e do sistema por trás dele como um consumidor, antes de se aprofundar na arquitetura.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-109">This gives you an experience of the app and the system behind it as a consumer, before you delve into the architecture.</span></span> <span data-ttu-id="9f1e7-110">Ele também apresenta o HockeyApp – uma maneira interessante de gerenciar as distribuições de alfa e beta de seus aplicativos para usuários de teste.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-110">It also introduces you to HockeyApp, a cool way of managing the alpha and beta distributions of your apps to test users.</span></span>

## <a name="use-the-mobile-experience"></a><span data-ttu-id="9f1e7-111">Usar a experiência móvel</span><span class="sxs-lookup"><span data-stu-id="9f1e7-111">Use the mobile experience</span></span>
<span data-ttu-id="9f1e7-112">Você poderá usar o aplicativo MyDriving se tiver um dispositivo Android, iOS ou Windows 10.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-112">You can use the MyDriving app if you have an Android, iOS, or Windows 10 device.</span></span>

### <a name="android-and-windows-10-mobile-installation"></a><span data-ttu-id="9f1e7-113">Instalação do Android e do Windows Mobile 10</span><span class="sxs-lookup"><span data-stu-id="9f1e7-113">Android and Windows 10 Mobile installation</span></span>
<span data-ttu-id="9f1e7-114">Em seu dispositivo:</span><span class="sxs-lookup"><span data-stu-id="9f1e7-114">On your device:</span></span>

1. <span data-ttu-id="9f1e7-115">Permitir aplicativos de desenvolvimento:</span><span class="sxs-lookup"><span data-stu-id="9f1e7-115">Allow development apps:</span></span>
   
   * <span data-ttu-id="9f1e7-116">Android: em **Configurações** > **Segurança**, permita aplicativos de **Fontes desconhecidas**.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-116">Android: In **Settings** > **Security**, allow apps from **Unknown sources**.</span></span>
   * <span data-ttu-id="9f1e7-117">Windows 10: em **Configurações** > **Atualizações** > **Para Desenvolvedores**, defina o **Modo de desenvolvedor**.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-117">Windows 10: In **Settings** > **Updates** > **For Developers**, set **Developer mode**.</span></span>
2. <span data-ttu-id="9f1e7-118">Junte-se à nossa equipe de teste beta inscrevendo-se ou entrando no [HockeyApp](https://rink.hockeyapp.net).</span><span class="sxs-lookup"><span data-stu-id="9f1e7-118">Join our beta test team by signing up with, or signing in to, [HockeyApp](https://rink.hockeyapp.net).</span></span> <span data-ttu-id="9f1e7-119">O HockeyApp facilita a distribuição das primeiras versões do seu aplicativo para os usuários de teste.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-119">HockeyApp makes it easy to distribute early releases of your app to test users.</span></span>
   
   <span data-ttu-id="9f1e7-120">Se estiver usando o Windows 10, use o navegador Edge.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-120">If you’re using Windows 10, use the Edge browser.</span></span>
   
   <span data-ttu-id="9f1e7-121">Se você foi um participante do Build 2016, entre com o mesmo email da conta da Microsoft registrada para a conferência, usando um dos botões da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-121">If you were a Build 2016 attendee, sign in with the same Microsoft account email that you registered for the conference, by using one of the Microsoft buttons.</span></span> <span data-ttu-id="9f1e7-122">Você já se inscreveu no HockeyApp.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-122">You’re already signed up with HockeyApp.</span></span>
   
   ![Tela de entrada do HockeyApp](./media/iot-solution-get-started/image1.png)
3. <span data-ttu-id="9f1e7-124">Baixe e instale o aplicativo aqui:</span><span class="sxs-lookup"><span data-stu-id="9f1e7-124">Download and install the app from here:</span></span>
   
   * [<span data-ttu-id="9f1e7-125">Android</span><span class="sxs-lookup"><span data-stu-id="9f1e7-125">Android</span></span>](http://rink.io/spMyDrivingAndroid)
   * [<span data-ttu-id="9f1e7-126">Windows 10</span><span class="sxs-lookup"><span data-stu-id="9f1e7-126">Windows 10</span></span>](http://rink.io/spMyDrivingUWP)
   
   <span data-ttu-id="9f1e7-127">Há dois itens.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-127">There are two items.</span></span> <span data-ttu-id="9f1e7-128">Instale o certificado em **Pessoas Confiáveis**.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-128">Install the certificate in **Trusted People**.</span></span> <span data-ttu-id="9f1e7-129">Em seguida, instale o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-129">Then install the app.</span></span>

<span data-ttu-id="9f1e7-130">*Problemas ao iniciar o aplicativo no Windows Mobile 10?*</span><span class="sxs-lookup"><span data-stu-id="9f1e7-130">*Any issues starting the app on Windows 10 Mobile?*</span></span> <span data-ttu-id="9f1e7-131">Talvez seu telefone esteja com uma ou duas atualizações atrasadas.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-131">Your phone might be an update or two behind.</span></span> <span data-ttu-id="9f1e7-132">Verifique se você tem as atualizações mais recentes, ou instale:</span><span class="sxs-lookup"><span data-stu-id="9f1e7-132">Make sure you've got the latest updates, or install:</span></span>

* [<span data-ttu-id="9f1e7-133">Microsoft.NET.Native.Framework.1.2.appx</span><span class="sxs-lookup"><span data-stu-id="9f1e7-133">Microsoft.NET.Native.Framework.1.2.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Framework.1.2.appx) 
* [<span data-ttu-id="9f1e7-134">Microsoft.NET.Native.Runtime.1.1.appx</span><span class="sxs-lookup"><span data-stu-id="9f1e7-134">Microsoft.NET.Native.Runtime.1.1.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Runtime.1.1.appx) 
* [<span data-ttu-id="9f1e7-135">Microsoft.VCLibs.ARM.14.00.appx</span><span class="sxs-lookup"><span data-stu-id="9f1e7-135">Microsoft.VCLibs.ARM.14.00.appx</span></span>](https://download.hockeyapp.net/packages/win10/Microsoft.VCLibs.ARM.14.00.appx)

### <a name="ios-installation"></a><span data-ttu-id="9f1e7-136">Instalação do iOS</span><span class="sxs-lookup"><span data-stu-id="9f1e7-136">iOS installation</span></span>
<span data-ttu-id="9f1e7-137">Se você participou no Build 2016, baixe o aplicativo como membro de nossa equipe de teste no HockeyApp:</span><span class="sxs-lookup"><span data-stu-id="9f1e7-137">If you attended Build 2016, download the app as a member of our test team on HockeyApp:</span></span>

1. <span data-ttu-id="9f1e7-138">Em seu dispositivo iOS, entre no [HockeyApp](https://rink.hockeyapp.net).</span><span class="sxs-lookup"><span data-stu-id="9f1e7-138">On your iOS device, sign in to [HockeyApp](https://rink.hockeyapp.net).</span></span>
   <span data-ttu-id="9f1e7-139">Use um dos botões de entrada da Microsoft e entre com o mesmo email da conta da Microsoft registrado para a conferência.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-139">Use one of the Microsoft sign-in buttons, and sign in with the same Microsoft account email that you registered with the conference.</span></span> <span data-ttu-id="9f1e7-140">(Não use os campos de email e senha).</span><span class="sxs-lookup"><span data-stu-id="9f1e7-140">(Don’t use the email and password fields.)</span></span>
   
   ![Tela de entrada do HockeyApp](./media/iot-solution-get-started/image1.png)
2. <span data-ttu-id="9f1e7-142">No painel do HockeyApp, selecione MyDriving e baixe-o.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-142">In the HockeyApp dashboard, select MyDriving and download it.</span></span>
3. <span data-ttu-id="9f1e7-143">Autorize a versão beta do HockeyApp:</span><span class="sxs-lookup"><span data-stu-id="9f1e7-143">Authorize the beta release from HockeyApp:</span></span>
   
   <span data-ttu-id="9f1e7-144">a.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-144">a.</span></span> <span data-ttu-id="9f1e7-145">Acesse **Configurações** > **Geral** > **Gerenciamento de Perfis e Dispositivos**</span><span class="sxs-lookup"><span data-stu-id="9f1e7-145">Go to **Settings** > **General** > **Profiles and Device Management.**</span></span>
   
   <span data-ttu-id="9f1e7-146">b.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-146">b.</span></span> <span data-ttu-id="9f1e7-147">Confie no certificado **Bit Stadium GmbH** .</span><span class="sxs-lookup"><span data-stu-id="9f1e7-147">Trust the **Bit Stadium GmbH** certificate.</span></span>

<span data-ttu-id="9f1e7-148">Se você não participou no Build 2016, é possível criar e implantar o aplicativo por conta própria:</span><span class="sxs-lookup"><span data-stu-id="9f1e7-148">If you didn’t attend Build 2016, you can build and deploy the app yourself:</span></span>

1. <span data-ttu-id="9f1e7-149">Baixe o código [no GitHub].</span><span class="sxs-lookup"><span data-stu-id="9f1e7-149">Download the code [from GitHub].</span></span>
2. <span data-ttu-id="9f1e7-150">Crie e implante [usando o Xamarin].</span><span class="sxs-lookup"><span data-stu-id="9f1e7-150">Build and deploy by [using Xamarin].</span></span>

<span data-ttu-id="9f1e7-151">Encontre mais detalhes no [Guia de Referência do MyDriving](http://aka.ms/mydrivingdocs).</span><span class="sxs-lookup"><span data-stu-id="9f1e7-151">Find more details in the [MyDriving Reference Guide](http://aka.ms/mydrivingdocs).</span></span>

## <a name="get-an-obd-adapter-optional"></a><span data-ttu-id="9f1e7-152">Obter um adaptador OBD (opcional)</span><span class="sxs-lookup"><span data-stu-id="9f1e7-152">Get an OBD adapter (optional)</span></span>
<span data-ttu-id="9f1e7-153">Essa é a parte que faz deste um sistema de Internet das Coisas real!</span><span class="sxs-lookup"><span data-stu-id="9f1e7-153">This is the part that makes this a real Internet of Things system!</span></span> <span data-ttu-id="9f1e7-154">Você pode usar o aplicativo sem um sistema, mas é mais divertido com o sistema real, e ele não é caro.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-154">You can use the app without one, but it’s more fun with the real thing, and they aren’t expensive.</span></span>

<span data-ttu-id="9f1e7-155">O OBD (Diagnóstico interno) é o recurso do seu carro utilizado pela garagem para ajustá-lo e diagnosticar ruídos estranhos e lâmpadas de aviso.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-155">On-board diagnostics (OBD) is the feature of your car that the garage uses to tune up your car and diagnose odd noises and warning lamps.</span></span> <span data-ttu-id="9f1e7-156">A menos que seu carro seja uma verdadeira antiguidade, você encontrará um soquete em algum lugar na cabine, normalmente, atrás de uma aba sob o painel.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-156">Unless your car is of great antiquity, you’ll find a socket somewhere in the cabin, typically behind a flap under the dashboard.</span></span> <span data-ttu-id="9f1e7-157">Com o conector à direita, você pode obter a métrica de desempenho do mecanismo e fazer alguns ajustes.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-157">With the right connector, you can get metrics of the engine’s performance and make certain adjustments.</span></span> <span data-ttu-id="9f1e7-158">Um conector OBD pode ser adquirido por um valor barato em locais comuns.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-158">An OBD connector can be purchased cheaply from the usual places.</span></span> <span data-ttu-id="9f1e7-159">Ele se conecta usando Bluetooth ou Wi-Fi a um aplicativo em seu telefone.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-159">It connects by using Bluetooth or Wi-Fi to an app on your phone.</span></span>

<span data-ttu-id="9f1e7-160">Nesse caso, vamos conectar seu carro na nuvem.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-160">In this case, we’re going to connect your car to the cloud.</span></span> <span data-ttu-id="9f1e7-161">A conexão direta do OBD é feita com seu telefone, mas nosso aplicativo funciona como uma retransmissão.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-161">The direct connection from the OBD is to your phone, but our app works as a relay.</span></span> <span data-ttu-id="9f1e7-162">A telemetria do seu carro é enviada diretamente para o hub IoT do MyDriving, no qual é processada para registrar suas viagens e avaliar seu estilo de conduzir.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-162">Your car's telemetry is sent straight to the MyDriving IoT hub, where it's processed to log your road trips and assess your driving style.</span></span>

<span data-ttu-id="9f1e7-163">Para conectar um dispositivo OBD:</span><span class="sxs-lookup"><span data-stu-id="9f1e7-163">To connect an OBD device:</span></span>

1. <span data-ttu-id="9f1e7-164">Verifique se seu carro tem um soquete OBD.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-164">Check that your car has an OBD socket.</span></span>
2. <span data-ttu-id="9f1e7-165">Obtenha um adaptador OBD:</span><span class="sxs-lookup"><span data-stu-id="9f1e7-165">Obtain an OBD adapter:</span></span>
   
   * <span data-ttu-id="9f1e7-166">Se estiver usando um telefone Android ou Windows, você precisará de um adaptador OBD II habilitado para Bluetooth.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-166">If you're using an Android or Windows phone, you need a Bluetooth-enabled OBD II adapter.</span></span> <span data-ttu-id="9f1e7-167">Usamos a [Ferramenta de Digitalização BAFX Products 34t5 Bluetooth OBDII].</span><span class="sxs-lookup"><span data-stu-id="9f1e7-167">We used [BAFX Products 34t5 Bluetooth OBDII Scan Tool].</span></span>
   * <span data-ttu-id="9f1e7-168">Se estiver usando um telefone iOS, você precisará de um adaptador OBD habilitado para Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-168">If you're using an iOS phone, you need a Wi-Fi-enabled OBD adapter.</span></span> <span data-ttu-id="9f1e7-169">Usamos a [Ferramenta de Digitalização OBDLink MX Wi-Fi: scanner de adaptador/diagnóstico OBD].</span><span class="sxs-lookup"><span data-stu-id="9f1e7-169">We used [ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner].</span></span>
3. <span data-ttu-id="9f1e7-170">Siga as instruções que acompanham o adaptador OBD para conectá-lo ao seu telefone.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-170">Follow the instructions that come with your OBD adapter to connect it to your phone.</span></span> <span data-ttu-id="9f1e7-171">Lembre-se:</span><span class="sxs-lookup"><span data-stu-id="9f1e7-171">Keep the following in mind:</span></span>
   
   * <span data-ttu-id="9f1e7-172">Um adaptador Bluetooth deve ser emparelhado com o telefone, na página **Configurações** .</span><span class="sxs-lookup"><span data-stu-id="9f1e7-172">A Bluetooth adapter must be paired with the phone, on the **Settings** page.</span></span>
   * <span data-ttu-id="9f1e7-173">Um adaptador Wi-Fi deve ter um endereço no intervalo 192.168.xxx.xxx.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-173">A Wi-Fi adapter must have an address in the range 192.168.xxx.xxx.</span></span>
4. <span data-ttu-id="9f1e7-174">Se tiver vários carros, você poderá obter um adaptador separado para cada (no máximo três).</span><span class="sxs-lookup"><span data-stu-id="9f1e7-174">If you have several cars, you can get a separate adapter for each (maximum of three).</span></span>

<span data-ttu-id="9f1e7-175">Se não tiver um adaptador OBD, o aplicativo ainda enviará os dados de localização e velocidade do receptor GPS do telefone para o back-end e perguntará se você deseja simular um OBD.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-175">If you don’t have an OBD adapter, the app will still send location and speed data from the phone's GPS receiver to the back end and will ask if you want to simulate an OBD.</span></span>

<span data-ttu-id="9f1e7-176">É possível saber mais sobre como o aplicativo usa os dados do adaptador OBD e as opções para criar seu próprio dispositivo OBD na seção 2.1 “Dispositivos IoT” no [Guia de Referência do MyDriving](http://aka.ms/mydrivingdocs).</span><span class="sxs-lookup"><span data-stu-id="9f1e7-176">You can find out more about how the app uses data from the OBD adapter and about options for creating your own OBD device in section 2.1, "IoT Devices," in the [MyDriving Reference Guide](http://aka.ms/mydrivingdocs).</span></span>

## <a name="use-the-app"></a><span data-ttu-id="9f1e7-177">Usar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="9f1e7-177">Use the app</span></span>
<span data-ttu-id="9f1e7-178">Inicie o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-178">Start the app.</span></span> <span data-ttu-id="9f1e7-179">Há um guia de Início Rápido para orientar você sobre como ele funciona.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-179">There’s an initial Quickstart to walk you through how it works.</span></span>

### <a name="track-your-trips"></a><span data-ttu-id="9f1e7-180">Acompanhar suas viagens</span><span class="sxs-lookup"><span data-stu-id="9f1e7-180">Track your trips</span></span>
<span data-ttu-id="9f1e7-181">Toque no botão Gravar (círculo vermelho grande na parte inferior da tela) para iniciar uma viagem e toque novamente para encerrá-la.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-181">Tap the record button (big red circle at the bottom of the screen) to start a trip, and tap again to end.</span></span>

![Ilustração do botão Gravar para o acompanhamento da viagem](./media/iot-solution-get-started/image2.png)

<span data-ttu-id="9f1e7-183">Toda vez que iniciar uma viagem e, se não houver nenhum dispositivo OBD, será perguntado se você deseja usar o simulador.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-183">Each time you start a trip, if there’s no OBD device, you’ll be asked if you want to use the simulator.</span></span>

<span data-ttu-id="9f1e7-184">Ao final de uma viagem, clique no botão Parar, e você obterá um resumo.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-184">At the end of a trip, tap the stop button, and you get a summary.</span></span>

![Exemplo de um resumo de viagem](./media/iot-solution-get-started/image3.png)

### <a name="review-your-trips"></a><span data-ttu-id="9f1e7-186">Examinar suas viagens</span><span class="sxs-lookup"><span data-stu-id="9f1e7-186">Review your trips</span></span>
![Exemplo de uma viagem anterior](./media/iot-solution-get-started/image4.png)

### <a name="review-your-profile"></a><span data-ttu-id="9f1e7-188">Examinar seu perfil</span><span class="sxs-lookup"><span data-stu-id="9f1e7-188">Review your profile</span></span>
![Exemplo de um perfil de estilo de conduzir](./media/iot-solution-get-started/image5.png)

## <a name="send-us-your-test-feedback"></a><span data-ttu-id="9f1e7-190">Envie-nos seus comentários sobre o teste</span><span class="sxs-lookup"><span data-stu-id="9f1e7-190">Send us your test feedback</span></span>
<span data-ttu-id="9f1e7-191">Uma vez que criamos o MyDriving para ajudar a iniciar rapidamente seus próprios sistemas de IoT, certamente desejamos saber de você como ele funciona.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-191">Because we created MyDriving to help jumpstart your own IoT systems, we certainly want to hear from you about how well it works.</span></span> <span data-ttu-id="9f1e7-192">Fale conosco se:</span><span class="sxs-lookup"><span data-stu-id="9f1e7-192">Let us know if:</span></span>

* <span data-ttu-id="9f1e7-193">Você encontra dificuldades ou desafios.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-193">You run into difficulties or challenges.</span></span>
* <span data-ttu-id="9f1e7-194">Há um ponto de extensão que tornaria isso mais adequado ao seu cenário.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-194">There is an extension point that would make it more suitable to your scenario.</span></span>
* <span data-ttu-id="9f1e7-195">Você encontra uma maneira mais eficiente de atender a determinadas necessidades.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-195">You find a more efficient way to accomplish certain needs.</span></span>
* <span data-ttu-id="9f1e7-196">Você tem outras sugestões para melhorar o MyDriving ou essa documentação.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-196">You have any other suggestions for improving MyDriving or this documentation.</span></span>

<span data-ttu-id="9f1e7-197">No próprio aplicativo MyDriving, é possível usar o mecanismo interno de comentários do HockeyApp: no iOS e Android, basta balançar seu telefone ou usar o comando de menu **Comentários** .</span><span class="sxs-lookup"><span data-stu-id="9f1e7-197">Within the MyDriving app itself, you can use the built-in HockeyApp feedback mechanism: on iOS and Android, just give your phone a shake, or use the **Feedback** menu command.</span></span> <span data-ttu-id="9f1e7-198">Isso automaticamente anexa uma captura de tela para que saibamos sobre o que você está falando.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-198">This will automatically attach a screenshot, so that we’ll know what you’re talking about.</span></span> <span data-ttu-id="9f1e7-199">E, no caso de eventuais falhas, o HockeyApp coletará os logs delas para nos informar sobre o ocorrido.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-199">And if there are any unfortunate crashes, HockeyApp collects the crash logs to tell us about them.</span></span> <span data-ttu-id="9f1e7-200">Também é possível fornecer comentários por meio do [portal do HockeyApp].</span><span class="sxs-lookup"><span data-stu-id="9f1e7-200">You can also give feedback through the [HockeyApp portal].</span></span>

<span data-ttu-id="9f1e7-201">Também é possível arquivar um [problema no GitHub], ou deixar um comentário abaixo (edição en-us).</span><span class="sxs-lookup"><span data-stu-id="9f1e7-201">You can also file an [issue on GitHub], or leave a comment below (en-us edition).</span></span>

<span data-ttu-id="9f1e7-202">Aguardamos seu contato!</span><span class="sxs-lookup"><span data-stu-id="9f1e7-202">We look forward to hearing from you!</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f1e7-203">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9f1e7-203">Next steps</span></span>
* <span data-ttu-id="9f1e7-204">Explore o [Guia de Referência do MyDriving](http://aka.ms/mydrivingdocs) para entender como projetamos e criamos todo o sistema do MyDriving.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-204">Explore the [MyDriving Reference Guide](http://aka.ms/mydrivingdocs) to understand how we’ve designed and built the entire MyDriving system.</span></span>
* <span data-ttu-id="9f1e7-205">[Crie e implante um sistema por conta própria](iot-solution-build-system.md) usando nossos scripts do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-205">[Create and deploy a system of your own](iot-solution-build-system.md) by using our Azure Resource Manager scripts.</span></span> <span data-ttu-id="9f1e7-206">O [Guia de Referência do MyDriving](http://aka.ms/mydrivingdocs) também o orienta pelas áreas nas quais fará a maioria das personalizações.</span><span class="sxs-lookup"><span data-stu-id="9f1e7-206">The [MyDriving Reference Guide](http://aka.ms/mydrivingdocs) also guides you through areas where you’ll make the most customizations.</span></span>

<span data-ttu-id="9f1e7-207">[no GitHub]: https://github.com/Azure-Samples/MyDriving</span><span class="sxs-lookup"><span data-stu-id="9f1e7-207">[from GitHub]: https://github.com/Azure-Samples/MyDriving</span></span>
<span data-ttu-id="9f1e7-208">[usando o Xamarin]: https://developer.xamarin.com/guides/ios/getting_started/installation/</span><span class="sxs-lookup"><span data-stu-id="9f1e7-208">[using Xamarin]: https://developer.xamarin.com/guides/ios/getting_started/installation/</span></span>
<span data-ttu-id="9f1e7-209">[Ferramenta de Digitalização BAFX Products 34t5 Bluetooth OBDII]: http://www.amazon.com/gp/product/B005NLQAHS</span><span class="sxs-lookup"><span data-stu-id="9f1e7-209">[BAFX Products 34t5 Bluetooth OBDII Scan Tool]: http://www.amazon.com/gp/product/B005NLQAHS</span></span>
<span data-ttu-id="9f1e7-210">[Ferramenta de Digitalização OBDLink MX Wi-Fi: scanner de adaptador/diagnóstico OBD]: http://www.amazon.com/gp/product/B00OCYXTYY/ref=s9_simh_gw_g263_i1_r?pf_rd_m=ATVPDKIKX0DER&pf_rd_s=desktop-2&pf_rd_r=1MWRMKXK4KK9VYMJ44MP</span><span class="sxs-lookup"><span data-stu-id="9f1e7-210">[ScanTool OBDLink MX Wi-Fi: OBD Adapter/Diagnostic Scanner]: http://www.amazon.com/gp/product/B00OCYXTYY/ref=s9_simh_gw_g263_i1_r?pf_rd_m=ATVPDKIKX0DER&pf_rd_s=desktop-2&pf_rd_r=1MWRMKXK4KK9VYMJ44MP</span></span>
<span data-ttu-id="9f1e7-211">[portal do HockeyApp]: https://rink.hockeyapp.org</span><span class="sxs-lookup"><span data-stu-id="9f1e7-211">[HockeyApp portal]: https://rink.hockeyapp.org</span></span>
<span data-ttu-id="9f1e7-212">[problema no GitHub]: https://github.com/Azure-Samples/MyDriving/issues</span><span class="sxs-lookup"><span data-stu-id="9f1e7-212">[issue on GitHub]: https://github.com/Azure-Samples/MyDriving/issues</span></span>
