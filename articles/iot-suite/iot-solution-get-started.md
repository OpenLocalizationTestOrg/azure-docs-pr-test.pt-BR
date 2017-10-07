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
# <a name="mydriving-iot-system-quick-start"></a>Sistema de IoT MyDriving: início rápido
MyDriving é um sistema que demonstra o design de saudação e a implementação de um típico [Internet das coisas](iot-suite-overview.md) solução (IoT) que coleta a telemetria de dispositivos, processa esses dados na nuvem hello e aplica o aprendizado de máquina tooprovide uma resposta adaptável. demonstração de Olá registra dados sobre viagens seu carro, usando dados de seu telefone celular e um adaptador que coleta informações do sistema de controle do carro. Ele usa este comentário tooprovide de dados no seu estilo de como os usuários tooother de comparação.

Olá finalidade real MyDriving é tooget iniciado na criação de sua própria solução de IoT. Mas, antes disso, vamos sobre Olá MyDriving aplicativo em si – como um membro da nossa equipe de usuário de teste. Isso fornece uma experiência de aplicativo hello e sistema de saudação por trás dela como um consumidor, antes de se a arquitetura de saudação. Ele também apresenta tooHockeyApp, uma maneira interessante de distribuições de saudação alfa e beta dos usuários tootest aplicativos de gerenciamento.

## <a name="use-hello-mobile-experience"></a>Use a experiência móvel Olá
Você pode usar o hello MyDriving aplicativo se você tiver um dispositivo Android, iOS ou Windows 10.

### <a name="android-and-windows-10-mobile-installation"></a>Instalação do Android e do Windows Mobile 10
Em seu dispositivo:

1. Permitir aplicativos de desenvolvimento:
   
   * Android: em **Configurações** > **Segurança**, permita aplicativos de **Fontes desconhecidas**.
   * Windows 10: em **Configurações** > **Atualizações** > **Para Desenvolvedores**, defina o **Modo de desenvolvedor**.
2. Junte-se à nossa equipe de teste beta inscrevendo-se ou entrando no [HockeyApp](https://rink.hockeyapp.net). HockeyApp torna fácil toodistribute primeiras versões dos seus usuários de tootest do aplicativo.
   
   Se você estiver usando o Windows 10, use o navegador de borda de saudação.
   
   Se você fosse um participante de compilação 2016, entrar com hello mesmo email de conta da Microsoft que você registrou para conferência hello, usando uma saudação botões da Microsoft. Você já se inscreveu no HockeyApp.
   
   ![Tela de entrada do HockeyApp](./media/iot-solution-get-started/image1.png)
3. Baixe e instale o aplicativo hello aqui:
   
   * [Android](http://rink.io/spMyDrivingAndroid)
   * [Windows 10](http://rink.io/spMyDrivingUWP)
   
   Há dois itens. Instalar certificado Olá no **pessoas confiáveis**. Em seguida, instale o aplicativo hello.

*Problemas ao iniciar o aplicativo hello no Windows 10 Mobile?* Talvez seu telefone esteja com uma ou duas atualizações atrasadas. Verifique se você tem as atualizações mais recentes do hello, ou instala:

* [Microsoft.NET.Native.Framework.1.2.appx](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Framework.1.2.appx) 
* [Microsoft.NET.Native.Runtime.1.1.appx](https://download.hockeyapp.net/packages/win10/Microsoft.NET.Native.Runtime.1.1.appx) 
* [Microsoft.VCLibs.ARM.14.00.appx](https://download.hockeyapp.net/packages/win10/Microsoft.VCLibs.ARM.14.00.appx)

### <a name="ios-installation"></a>Instalação do iOS
Se você participou 2016 de compilação, baixe o aplicativo de hello como um membro da nossa equipe de teste em HockeyApp:

1. Em seu dispositivo iOS, entrar muito[HockeyApp](https://rink.hockeyapp.net).
   Use uma saudação botões entrar Microsoft e entrar no hello email de conta Microsoft mesmo que você registrou com conferência hello. (Não use campos Olá de email e senha).
   
   ![Tela de entrada do HockeyApp](./media/iot-solution-get-started/image1.png)
2. No painel do HockeyApp hello, selecione MyDriving e baixá-lo.
3. Autorize a versão beta de saudação do HockeyApp:
   
   a. Vá muito**configurações** > **geral** > **perfis e gerenciamento de dispositivo.**
   
   b. Saudação de confiança **Bit Estádio GmbH** certificado.

Se não frequentou 2016 de compilação, você pode criar e implantar o aplicativo hello por conta própria:

1. Baixar o código de saudação [do GitHub].
2. Crie e implante [usando o Xamarin].

Encontrar mais detalhes no hello [guia de referência MyDriving](http://aka.ms/mydrivingdocs).

## <a name="get-an-obd-adapter-optional"></a>Obter um adaptador OBD (opcional)
Isso faz parte de saudação que torna isso um sistema real de Internet das coisas! Você pode usar o aplicativo hello sem uma, mas é divertido mais com algo real hello e não são caras.

Diagnóstico integrado (OBD) é o recurso de saudação do seu carro Olá garagem usa tootune o carro e diagnosticar ruídos ímpares e lâmpadas de aviso. A menos que seu carro de época excelente, você encontrará um soquete em algum lugar na cabine hello, normalmente por trás flap no painel de saudação. Com o conector de direito hello, você pode obter métricas de desempenho do mecanismo de saudação e fazer alguns ajustes. Um conector OBD pode ser adquirido barata de locais de saudação normal. Ele se conecta usando o aplicativo de tooan Bluetooth ou Wi-Fi em seu telefone.

Nesse caso, vamos tooconnect sua nuvem de toohello de carro. conexão direta de saudação do hello OBD é tooyour telefone, mas nosso aplicativo funciona como um retransmissor. Telemetria do carro será enviada reta toohello MyDriving IoT hub, onde ela é processada toolog sua viagem e avaliar seu estilo de referências.

tooconnect um dispositivo OBD:

1. Verifique se seu carro tem um soquete OBD.
2. Obtenha um adaptador OBD:
   
   * Se estiver usando um telefone Android ou Windows, você precisará de um adaptador OBD II habilitado para Bluetooth. Usamos a [Ferramenta de Digitalização BAFX Products 34t5 Bluetooth OBDII].
   * Se estiver usando um telefone iOS, você precisará de um adaptador OBD habilitado para Wi-Fi. Usamos a [Ferramenta de Digitalização OBDLink MX Wi-Fi: scanner de adaptador/diagnóstico OBD].
3. Siga as instruções de saudação que vêm com o tooconnect de adaptador OBD-tooyour telefone. Lembre-Olá seguinte:
   
   * Um adaptador Bluetooth deve estar combinado com telefone hello, Olá **configurações** página.
   * Um adaptador de Wi-Fi deve ter um endereço no 192.168.xxx.xxx de intervalo de saudação.
4. Se tiver vários carros, você poderá obter um adaptador separado para cada (no máximo três).

Se você não tiver um adaptador OBD, aplicativo hello ainda enviará local e dados de velocidade de toohello de receptor GPS do telefone Olá volta terminar e perguntará se você quiser toosimulate um OBD.

Você pode encontrar mais informações sobre como o aplicativo hello usa dados de saudação OBD adaptador e sobre as opções para criar seu próprio dispositivo OBD na seção 2.1, "Dispositivos IoT", no hello [guia de referência MyDriving](http://aka.ms/mydrivingdocs).

## <a name="use-hello-app"></a>Usar o aplicativo hello
Inicie aplicativo hello. Há um toowalk inicial de início rápido você por meio de como ele funciona.

### <a name="track-your-trips"></a>Acompanhar suas viagens
Olá botão Registro (círculo vermelho grande na parte inferior da saudação da tela hello) toostart uma viagem de toque e toque novamente tooend.

![Ilustração do botão de registro Olá para viagem de controle](./media/iot-solution-get-started/image2.png)

Cada vez que você iniciar uma viagem, se não houver nenhum dispositivo OBD, será perguntado se você quiser que o simulador de saudação toouse.

Final de saudação de uma viagem, toque Olá parar botão e, obter um resumo.

![Exemplo de um resumo de viagem](./media/iot-solution-get-started/image3.png)

### <a name="review-your-trips"></a>Examinar suas viagens
![Exemplo de uma viagem anterior](./media/iot-solution-get-started/image4.png)

### <a name="review-your-profile"></a>Examinar seu perfil
![Exemplo de um perfil de estilo de conduzir](./media/iot-solution-get-started/image5.png)

## <a name="send-us-your-test-feedback"></a>Envie-nos seus comentários sobre o teste
Como criamos MyDriving toohelp iniciar seus próprios sistemas de IoT, queremos certamente toohear você sobre como ele funciona. Fale conosco se:

* Você encontra dificuldades ou desafios.
* Há um ponto de extensão para que seja mais adequada do cenário de tooyour.
* Você encontrar um tooaccomplish de maneira mais eficiente determinadas necessidades.
* Você tem outras sugestões para melhorar o MyDriving ou essa documentação.

No hello MyDriving o aplicativo em si, você pode usar o mecanismo de comentários do HockeyApp interno Olá: no iOS e Android, é só atribuir seu telefone uma agitação ou use Olá **comentários** comando de menu. Isso automaticamente anexa uma captura de tela para que saibamos sobre o que você está falando. E se houver quaisquer falhas ruim, HockeyApp coleta Olá falha logs tootell nos sobre eles. Você também pode fornecer comentários por meio de saudação [HockeyApp portal].

Também é possível arquivar um [problema no GitHub], ou deixar um comentário abaixo (edição en-us).

Aguardamos toohearing você!

## <a name="next-steps"></a>Próximas etapas
* Explorar Olá [guia de referência de MyDriving](http://aka.ms/mydrivingdocs) toounderstand como é projetado e criado Olá MyDriving todo o sistema.
* [Crie e implante um sistema por conta própria](iot-solution-build-system.md) usando nossos scripts do Azure Resource Manager. Olá [guia de referência MyDriving](http://aka.ms/mydrivingdocs) também orienta você através das áreas onde você vai fazer Olá a maioria das personalizações.

[do GitHub]: https://github.com/Azure-Samples/MyDriving
[usando o Xamarin]: https://developer.xamarin.com/guides/ios/getting_started/installation/
[Ferramenta de Digitalização BAFX Products 34t5 Bluetooth OBDII]: http://www.amazon.com/gp/product/B005NLQAHS
[Ferramenta de Digitalização OBDLink MX Wi-Fi: scanner de adaptador/diagnóstico OBD]: http://www.amazon.com/gp/product/B00OCYXTYY/ref=s9_simh_gw_g263_i1_r?pf_rd_m=ATVPDKIKX0DER&pf_rd_s=desktop-2&pf_rd_r=1MWRMKXK4KK9VYMJ44MP
[HockeyApp portal]: https://rink.hockeyapp.org
[problema no GitHub]: https://github.com/Azure-Samples/MyDriving/issues
