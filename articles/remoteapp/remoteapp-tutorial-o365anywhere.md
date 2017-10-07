---
title: "aaaGet Olá a mesma experiência do Office 365 em qualquer dispositivo com o Azure RemoteApp | Microsoft Docs"
description: "Saiba como tooshare qualquer aplicativo do Office 365 com seus usuários usando o Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 0c971ce9-7d45-4cfb-9737-15b6706047e8
ms.service: remoteapp
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 11/23/2016
ms.author: guscatal;elizapo
ms.openlocfilehash: 140056c22c8c69b9ec605318e35a72b144da07eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-hello-same-office-365-experience-on-any-device-with-azure-remoteapp"></a>Get hello a mesma experiência do Office 365 em qualquer dispositivo com o Azure RemoteApp
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

Este artigo abordará como toodeploy Office 365 em qualquer dispositivo em sua empresa. Os usuários podem obter Olá mesmos recursos e experiência de interface do usuário no Android, Apple e no Windows.

Faremos isso usando o RemoteApp do Azure hospedando o Office 365 em máquinas virtuais com capacidade de dimensionamento no Azure, às quais os usuários possam se conectar. Chamamos esse conjunto de máquinas virtuais de uma “coleção nuvem”.

## <a name="create-a-cloud-collection"></a>Criar uma coleção na nuvem
Navega pela primeira vez depois de criar uma conta do Azure, muito**RemoteApp** clicando no link Olá no lado esquerdo de saudação.
![Mostrando o Azure RemoteApp em Olá Portal do Azure](./media/remoteapp-tutorial-o365anywhere/1-menu.png)

Continue clicando em **novo** inferior hello e "Criando rápida" uma coleção. Forneça um nome, região hello, assinatura hello, plano hello e imagem hello "Proffesional do Office 2013" que fornecemos.
![Caixa de diálogo Criar](./media/remoteapp-tutorial-o365anywhere/2-quickcreate.png)

Depois de concluir o processo de criação de coleção do hello formulário Olá deve começar. Isso pode levar horas tooan mais ou menos.

![Aguardando](./media/remoteapp-tutorial-o365anywhere/3-waiting.png)

Depois de processo hello, terá aparência semelhante a esta. Se clicarmos em **Publicação** , podemos ver que a maioria dos aplicativos do Office já foram publicados para nós.
![Coleção criada](./media/remoteapp-tutorial-o365anywhere/4-done.png)

![Aplicativos publicados](./media/remoteapp-tutorial-o365anywhere/5-publish.png)

Agora você também pode adicionar mais usuários que têm acesso toothis coleção clicando **acesso de usuário**.
![Configurar o acesso do usuário](./media/remoteapp-tutorial-o365anywhere/6-user.png)

Agora vamos testar conexão tooOffice 365!

## <a name="connect-toooffice-365"></a>Conecte-se tooOffice 365
Podemos entrará em muito[https://www.remoteapp.windowsazure.com/](https://www.remoteapp.windowsazure.com/), role para baixo e clique em **baixar clientes** tooinstall cliente de Azure RemoteApp Olá no dispositivo Olá que você está usando. Olá capturas de tela abaixo são para Windows.

Depois que o aplicativo hello inicia deverá toosign com sua conta da Microsoft (anteriormente chamada de "Live ID"), use Olá mesmo que sua conta do Azure agora. Quando você tiver feito logon, você deve receber uma notificação sobre novos convites, clique nos mesmos e você deve ver uma lista como a mostrada abaixo. Aceite o convite de saudação que corresponde a seu email do proprietário de conta do Azure.

![Novo convite](./media/remoteapp-tutorial-o365anywhere/7-araclient.png)

Abaixo, sua aparência quando há novos convites.

![Aceite um aplicativo](./media/remoteapp-tutorial-o365anywhere/8-invitation.png)

Depois de aceitar o convite hello, você deve ver todos os aplicativos do Office Olá no cliente do Azure RemoteApp hello.

![Lista de aplicativos](./media/remoteapp-tutorial-o365anywhere/9-work.png)

Quando você clicar em qualquer um desses aplicativos, Olá deve começar em Olá máquina virtual do Azure e devem ser definidos! Aproveite!

![iniciando](./media/remoteapp-tutorial-o365anywhere/10-arastart.png)

![powerpoint](./media/remoteapp-tutorial-o365anywhere/11-pp.png)

