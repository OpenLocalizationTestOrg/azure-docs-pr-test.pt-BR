---
title: "uso de afinidade de sessão aaaEnable Olá Kit de ferramentas do Azure para Eclipse"
description: "Saiba como o uso de afinidade de sessão tooenable Olá Kit de ferramentas do Azure para Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 88c595ec-7d85-40bd-9078-8d6be7b3f0fa
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 523e728c58bda95e7af4b242e831694eb6d75cb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-session-affinity"></a>Habilitar a afinidade de sessão
Dentro de Olá Kit de ferramentas do Azure para Eclipse, você pode habilitar a afinidade de sessão HTTP ou "sessões Autoadesivas", para suas funções. Olá, imagem a seguir mostra Olá **balanceamento de carga** recurso de afinidade de sessão propriedades diálogo usado tooenable hello:

![][ic719492]

## <a name="tooenable-session-affinity-for-your-role"></a>afinidade de sessão tooenable para sua função
1. Função hello no Explorador de projeto do Eclipse, clique **Azure**e, em seguida, clique em **balanceamento de carga**.

2. Em Olá **propriedades de balanceamento de carga de WorkerRole1** caixa de diálogo:

   a. Verifique **Habilitar a afinidade de sessão HTTP (sessões autoadesivas) para esta função.**

   b. Para **toouse de ponto de extremidade de entrada**, selecione toouse um ponto de extremidade de entrada, por exemplo, **http (public: 80, private: 8080)**. Seu aplicativo deve usar esse ponto de extremidade como seu ponto de extremidade HTTP. Você pode habilitar vários pontos de extremidade para sua função, mas você pode selecionar apenas um deles toosupport sessões Autoadesivas.

   c. Recompile seu aplicativo.

Uma vez habilitada, se você tiver mais de uma instância de função, solicitações de HTTP vindo de um determinado cliente continuarão sendo manipuladas pelo Olá mesmo instância de função.

Olá Kit de ferramentas do Eclipse permite isso instalando um módulo IIS especial chamado roteamento ARR (Application Request) em cada uma de suas instâncias de função. O ARR redireciona as instância de função apropriada de toohello de solicitações HTTP. Olá Kit de ferramentas reconfigura automaticamente o ponto de extremidade de saudação selecionado para que o tráfego HTTP de entrada hello está primeiro roteado toohello ARR software. saudação de kit de ferramentas também cria um ponto de extremidade interno novo que o servidor de Java é configurado toolisten para. Que é o ponto de extremidade de saudação usado pela instância de função apropriada do ARR tooreroute Olá HTTP tráfego toohello. Dessa forma, cada instância de função em sua implantação de várias instâncias serve como um proxy reverso para todos os Olá outras instâncias, habilitando as sessões Autoadesivas.

## <a name="notes-about-session-affinity"></a>Observações sobre a afinidade de sessão
* Afinidade de sessão não funciona no emulador de computação hello. configurações Olá podem ser aplicadas no emulador de computação Olá sem interferir no processo de compilação ou execução do emulador de computação, mas o recurso Olá em si não funciona no emulador de computação hello.

* Habilitar a afinidade de sessão resultará em um aumento na quantidade de saudação do espaço em disco ocupada por sua implantação no Azure, como o software adicional será baixado e instalado em suas instâncias de função quando o serviço é iniciado no hello nuvem do Azure.

* Olá tempo tooinitialize cada função levará mais tempo.

* Ponto de extremidade interno, toofunction como um rerouter de tráfego, como mencionado acima, será adicionado.


## <a name="see-also"></a>Consulte também
[Kit de Ferramentas do Azure para Eclipse][Azure Toolkit for Eclipse]

[Criar um aplicativo Hello World para Azure no Eclipse][Creating a Hello World Application for Azure in Eclipse]

[Saudação de instalar o Kit de ferramentas do Azure para Eclipse][Installing hello Azure Toolkit for Eclipse] 

Para obter mais informações sobre como usar o Azure com Java, consulte Olá [Centro de desenvolvedores de Java do Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[How tooMaintain Session Data with Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699539
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719492]: ./media/azure-toolkit-for-eclipse-enable-session-affinity/ic719492.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690950.aspx -->
