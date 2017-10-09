---
title: "aplicativo de demonstração do Mobile Engagement aaaAzure | Microsoft Docs"
description: "Descreve onde toodownload, como toouse e benefícios de saudação do uso do Azure Mobile Engagement demonstrar o aplicativo"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: f624d5aa-254b-4ad0-96a3-f00e6c3a2c97
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2016
ms.author: piyushjo
ms.openlocfilehash: 9ff0df0d21e1bad6aff573db49304a55593df1c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-demo-app"></a>Aplicativo de demonstração do Azure Mobile Engagement
Publicamos um aplicativo de demonstração do Azure Mobile Engagement para **iOS**, **Android**, e **Windows** plataformas toohelp você recursos úteis toofind e saber mais sobre o Mobile Contrato.

Olá aplicativo ajuda a:

* Localizar facilmente links úteis tooMobile recursos de contrato como vídeos, documentação, fóruns de suporte Olá, e onde o recurso de tooraise toogo solicitações.
* Experiência de notificações de exemplo que são suportadas pelo ideias do Mobile Engagement tooget para seus próprios aplicativos móveis.
* Usar um toostudy de implementação de referência como tooimplement Mobile Engagement em seu próprio aplicativo. Você pode aprender a:
  
  * Coletar dados de análise.
  * Implementar cenários de notificação avançada de tipos, como *Tela inteira intersticial* ou *Pop-up*.
  * Implementar pesquisas e sondagens.
  * Implementar cenários de push e dados por push silencioso.   

## <a name="app-installation"></a>Instalação do aplicativo
Este aplicativo está disponível em Olá lojas de aplicativos a seguir:

* **Aplicativo de demonstração Universal do Windows**:
  
  * Baixar o aplicativo hello em Olá [loja de aplicativos Windows](https://www.microsoft.com/en-us/store/apps/azure-mobile-engagement/9nblggh4qmh2).
  * Olá aplicativo foi desenvolvido como um aplicativo Universal do Windows 10. Olá código-fonte está disponível em [GitHub](https://github.com/Azure/azure-mobile-engagement-app-windows).
* **Aplicativo de demonstração do iOS**:
  
  * Baixar o aplicativo hello em Olá [da Apple store](https://itunes.apple.com/us/app/azure%20mobile%20engagement/id1105090090).
  * Olá aplicativo foi desenvolvido em iOS Swift. Olá código-fonte está disponível em [GitHub](https://github.com/Azure/azure-mobile-engagement-app-ios).
* **Aplicativo de demonstração do Android**:
  
  * Baixar o aplicativo hello em Olá [loja Google Play](https://play.google.com/store/apps/details?id=com.microsoft.azure.engagement).
  * Olá código-fonte está disponível em [GitHub](https://github.com/Azure/azure-mobile-engagement-app-android).

![Aplicativo de demonstração Universal do Windows][1]

![Aplicativo de demonstração do iOS][2]
![Aplicativo de demonstração Android][3]

## <a name="usage"></a>Uso
Você pode usar este aplicativo no hello maneiras a seguir:

**Baixe o aplicativo de saudação em seu dispositivo de links de repositório de aplicativo hello (fornecido anteriormente):**

> [!IMPORTANT]
> Você não precisa de uma conta do Azure ou precisa tooconnect Olá aplicativo tooa back-end. aplicativo Hello funciona de forma independente.
> 
> 

* Depois que você tiver um aplicativo hello em seu dispositivo, você pode ir por meio de links de saudação em Olá esquerda menu toofind Olá recursos úteis sobre o compromisso de mobilidade.
* Adicionamos Olá [feed RSS do serviço](https://aka.ms/azmerssfeed) no aplicativo para que você está sempre atualizado sobre atualizações de produto mais recentes hello.
* Você também pode usar Olá exemplo cenários tooexperience Olá tipo de notificação de notificações que são suportados pelo Mobile Engagement para cada plataforma. Essas notificações podem ser experiente localmente – ou seja, você pode clicar em botões Olá Olá telas tooshow você Olá experiência de notificações, toosending idênticos Olá notificações de plataforma do Mobile Engagement hello.

![Menu do aplicativo para Windows][4]

![Menu de aplicativo para iOS][5]
![Menu de aplicativo para Android][6]

**Baixe o código-fonte Olá da saudação GitHub links (fornecido anteriormente):**

* Depois de baixar o código-fonte hello, abri-lo no ambiente de desenvolvimento respectivos de hello – XCode para iOS, Android Studio para Visual Studio para Windows e Android.
* Em seguida, você deve seguir nosso [etapas básicas de integração SDK](mobile-engagement-windows-store-dotnet-get-started.md) para que você pode tooconnect tooits este aplicativo possui instância de back-end do Mobile Engagement.
  * É necessário tooconfigure uma cadeia de caracteres de conexão no aplicativo hello.
  * Você também precisa tooconfigure plataforma de notificação de envio de saudação para seu aplicativo.
* Você observará que o aplicativo hello em si é instrumentado com o Mobile Engagement. Portanto, que você abra o aplicativo hello depois de se conectar toohello back-end, você será toosee capaz de sessão de usuário de hello, atividades, eventos e assim por diante, Olá **Monitor** guia.
* Você também será capaz de toosend notificações toothis aplicativo de sua própria instância do Mobile Engagement, em vez de usar notificações de locais.
  
  * Aqui você pode adicionar seu dispositivo como um dispositivo de teste usando Olá **Get hello ID do dispositivo** item de menu no aplicativo hello. Isso fornece uma identificação do dispositivo que você registra em seguida como um dispositivo de teste com sua instância de back-end da plataforma.
    
    ![Identificação do dispositivo no Windows][7]
    
    ![ID do dispositivo no iOS][8]
    ![ID do dispositivo no Android][9]

## <a name="key-features-of-hello-demo-app"></a>Os principais recursos do aplicativo de demonstração de Olá
* Como mencionado anteriormente, com este aplicativo, você tem todos os recursos principais de saudação para compromisso de mobilidade em sua mão. Você pode usar links Olá no menu esquerdo hello.
* Você pode experimentar as notificações fora do aplicativo de cada plataforma. Essas notificações podem ser entregues como **somente notificação**, onde simplesmente clicar notificação Olá abre uma tela nativo do aplicativo hello (usando **vinculação profunda**) – ou como um **Web anúncio**, onde você pode entregar o conteúdo HTML adicional de saudação do Mobile Engagement volta terminar toobe exibido quando a notificação de saudação é clicada.
  
    ![Notificações fora do aplicativo][29]
* No iOS, você tem tooclose Olá aplicativo toosee Olá fora do aplicativo ou sistema notificações por push. Você pode examinar a implementação de saudação aqui para adicionar **botões de ação**, como Olá aqueles que são adicionados toothis notificação fora do aplicativo para *comentários* e *compartilhamento* (de forma que usuário Olá pode levar à direita de ação de notificação de saudação em si).
  
    ![Notificações fora do aplicativo no iOS][11] ![Tela de notificação fora do aplicativo no iOS][14]
* No Android, opções de saudação com suporte são adicionando texto de várias linhas (**texto grande**) ou uma imagem de notificação (**panorama**) notificação toohello, juntamente com hello **debotõesdeação** (como suporte para iOS).
  
    ![Notificações fora do aplicativo no Android][12] ![Tela de notificação fora do aplicativo no Android][15]
* No Windows 10, você pode ver a aparecem das notificações de saudação em Olá PC. Essa notificação também aparece na Olá Windows 10 **Central de notificações**. Não há suporte para a adição de **botões de ação** no momento Olá Olá SDK do Windows.
  
    ![Notificações fora do aplicativo no Windows][10] ![Tela fora do aplicativo no Windows][13]
* Você pode experimentar as notificações padrão “no aplicativo” de cada plataforma. Essa é uma experiência de duas etapas em que uma janela **Notificação** é exibida primeiro. Quando você clicar nele, ele abre a tela inteira **comunicado**, conforme exibido no hello captura de tela a seguir. Olá conteúdo este anúncio vem da sua instância de back-end do compromisso de mobilidade. Olá SDK tem modelos Olá para notificações e anúncios. Você pode facilmente personalizá-los, conforme mostrado neste aplicativo de demonstração com inclusão de saudação do nosso logotipo e cores.  
  
    ![Notificações no aplicativo no Windows][16]
  
    ![Notificações no aplicativo no iOS][17]  ![Notificações no aplicativo no Android][18]
  
    **iOS**, **Android**
* Você também pode usar o hello **categoria** recurso do Mobile Engagement toocustomize essa experiência padrão. Aplicativo de demonstração de Olá já demonstramos duas maneiras toochange Olá experiência comum de notificações de saudação. Observe que esse recurso de categoria Olá ainda não é suportado em Olá SDK do Windows.
  
    **Tela inteira intersticial:**
  
    ![Notificação no aplicativo - Categoria intersticial][30]
  
    ![Categoria intersticial no iOS][21]     ![Categoria intersticial no Android][22]
  
    **Notificação de pop-up:**
  
    ![Notificação no aplicativo - Categoria pop-up][31]
  
    ![Notificação de pop-up no iOS][19]    ![Notificação de pop-up no Android][20]

**iOS**, **Android**

* O Mobile Engagement também dá suporte a um tipo especializado de notificação no aplicativo chamado **Sondagens**. Isso permite que você toosend os usuários com aplicativo tooyour segmentada pesquisas rápidas. Você pode adicionar perguntas e opções para cada pergunta como Olá captura de tela a seguir. Isso, em seguida, será exibido como um usuário de aplicativo toohello notificação no aplicativo.   
  
    ![Notificações de sondagem][32]
  
    ![Pesquisa no Windows][26]
  
    ![Pesquisa no iOS][27]   ![Pesquisa no Android][28]

**iOS**, **Android**

* O Mobile Engagement também dá suporte à notificações de **Push de Dados** silenciosas. Com essas notificações, você pode enviar dados de seu serviço (como Olá dados JSON no exemplo a seguir de saudação), que você pode manipular no seu aplicativo e executar alguma ação. Um exemplo é como podemos alterar Olá preço de um item seletivamente usando notificações de envio de dados.
  
    ![Notificação por push de dados][33]
  
    ![Notificação por push de dados no Windows][23]
  
    ![Notificação por push de dados no iOS][24]  ![Notificação por push de dados no Android][25]

**iOS**, **Android**

> [!NOTE]
> Você pode exibir as instruções passo a passo detalhadas para qualquer uma dessas notificações, clicando em **clique aqui para obter instruções sobre como toosend essas notificações de plataforma do Mobile Engagement** em qualquer tela de notificação de exemplo.
> 
> 

[1]: ./media/mobile-engagement-demo-apps/home-windows.png
[2]: ./media/mobile-engagement-demo-apps/home-ios.png
[3]: ./media/mobile-engagement-demo-apps/home-android.png
[4]: ./media/mobile-engagement-demo-apps/menu-windows.png
[5]: ./media/mobile-engagement-demo-apps/menu-ios.png
[6]: ./media/mobile-engagement-demo-apps/menu-android.png
[7]: ./media/mobile-engagement-demo-apps/device-id-windows.png
[8]: ./media/mobile-engagement-demo-apps/device-id-ios.png
[9]: ./media/mobile-engagement-demo-apps/device-id-android.png
[10]: ./media/mobile-engagement-demo-apps/out-of-app-windows.png
[11]: ./media/mobile-engagement-demo-apps/out-of-app-ios.png
[12]: ./media/mobile-engagement-demo-apps/out-of-app-android.png
[13]: ./media/mobile-engagement-demo-apps/out-of-app-display-windows.png
[14]: ./media/mobile-engagement-demo-apps/out-of-app-display-ios.png
[15]: ./media/mobile-engagement-demo-apps/out-of-app-display-android.png
[16]: ./media/mobile-engagement-demo-apps/in-app-windows.png
[17]: ./media/mobile-engagement-demo-apps/in-app-ios.png
[18]: ./media/mobile-engagement-demo-apps/in-app-android.png
[19]: ./media/mobile-engagement-demo-apps/pop-up-ios.png
[20]: ./media/mobile-engagement-demo-apps/pop-up-android.png
[21]: ./media/mobile-engagement-demo-apps/interstitial-ios.png
[22]: ./media/mobile-engagement-demo-apps/interstitial-android.png
[23]: ./media/mobile-engagement-demo-apps/data-push-windows.png
[24]: ./media/mobile-engagement-demo-apps/data-push-ios.png
[25]: ./media/mobile-engagement-demo-apps/data-push-android.png
[26]: ./media/mobile-engagement-demo-apps/survey-windows.png
[27]: ./media/mobile-engagement-demo-apps/survey-ios.png
[28]: ./media/mobile-engagement-demo-apps/survey-android.png
[29]: ./media/mobile-engagement-demo-apps/out-of-app.png
[30]: ./media/mobile-engagement-demo-apps/in-app-interstitial.png
[31]: ./media/mobile-engagement-demo-apps/in-app-pop-up.png
[32]: ./media/mobile-engagement-demo-apps/notification-poll.png
[33]: ./media/mobile-engagement-demo-apps/notification-data-push.png
