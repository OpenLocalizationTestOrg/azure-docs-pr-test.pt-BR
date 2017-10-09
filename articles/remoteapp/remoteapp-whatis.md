---
title: "aaaWhat é o Azure RemoteApp? | Microsoft Docs"
description: Saiba como tooshare dispositivo tooany aplicativos e recursos por meio do Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: d7a8a311-e70a-4463-ac85-c7f62c500921
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: e13909f3a5698f58c7e4348f3ce53f43560f9b1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-remoteapp"></a>O que é o RemoteApp do Azure?
> [!IMPORTANT]
> O Azure RemoteApp será descontinuado até 31 de agosto de 2017. Saudação de leitura [comunicado](https://go.microsoft.com/fwlink/?linkid=821148) para obter detalhes.
> 
> 

O RemoteApp do Azure oferece funcionalidade de saudação do programa de Microsoft RemoteApp local hello, com o apoio de serviços de área de trabalho remota, tooAzure. O Azure RemoteApp o ajuda a fornecer acesso remoto seguro tooapplications de muitos dispositivos de usuário diferente. O Azure RemoteApp basicamente hospeda sessões do Terminal Server não persistente na nuvem hello e obter toouse-los e compartilhá-los com os usuários.

Com o Azure RemoteApp, você pode compartilhar aplicativos e recursos com usuários em praticamente qualquer dispositivo. Vamos hospedar seus aplicativos em nuvem Olá, significando que cuidar de hardware hello e dimensionamento toomeet demandas de usuário. Toodo se carregar o aplicativo hello desejado tooshare e, em seguida, obter seu usuários toouse esses aplicativos. [Os usuários obtêm tookeep seus próprios dispositivos](remoteapp-clients.md), enquanto você gerencia tudo por meio de saudação portal do Azure. Você ainda tem opção de saudação de usando suas credenciais corporativas, permitindo que você a garantir a segurança de saudação de aplicativos e dados.

Continue lendo para saber mais sobre o RemoteApp ou, se nós já convencemos você, [experimente-o agora](https://azure.microsoft.com/services/remoteapp/).

Tem dúvidas sobre o Azure RemoteApp? Confira nossas [Perguntas frequentes](remoteapp-faq.md).

O Azure RemoteApp faz parte da saudação [Microsoft Virtual Desktop Infrastructure](http://www.microsoft.com/server-cloud/products/virtual-desktop-infrastructure/explore.aspx).

**Novo!** Deseja toolearn mais sobre o Azure RemoteApp? Ou pronto toovalidate Azure RemoteApp em escala? Ingressar em nosso semanalmente [pedir a especialistas Olá webinar](https://azureinfo.microsoft.com/AzureRemoteAppAskTheExperts-Registration-Page.html?ls=Website).

## <a name="azure-remoteapp-collections"></a>Coleções do Azure RemoteApp
Há dois tipos de coleções do [Azure RemoteApp](remoteapp-collections.md):

* Um **coleção em nuvem** está hospedado no e armazena dados para os programas na nuvem hello. Os usuários podem acessar aplicativos ao efetuar logon com sua conta da Microsoft ou credenciais corporativas sincronizadas ou federadas com o Active Directory do Azure.
  
    Escolha uma coleção de nuvem quando o aplicativo hello deseja tooshare não precisar de um recurso de tooany de conexão da rede privada da empresa (por exemplo, por meio de um dispositivo VPN). Se o aplicativo hello usa recursos em Olá Internet, OneDrive, ou o Azure, uma coleção de nuvem irá funcionar para você. Também é toocreate mais rápida de saudação.
* Um **coleção híbrida** está hospedado no e armazena dados em Olá nuvem do Azure, mas também permite que usuários acessem dados e recursos armazenados em sua rede local. Os usuários podem acessar aplicativos ao efetuar logon com suas credenciais corporativas sincronizadas ou federadas com o Active Directory do Azure.
  
    Escolha uma coleção híbrida, se você precisar de um tooresources de conexão de rede privada da sua empresa. Por exemplo, se hello aplicativo precisa acessar tooone seguinte hello:
  
  * Servidores de arquivos localizados em sua intranet
  * Quicken
  * Bancos de dados por trás de um firewall
    
    Isso geralmente é mais útil para empresas de grandes porte com muitos recursos em redes privadas que não podem ser movido toohello nuvem.

Hello diferentes coleções tem opções diferentes, incluindo redes, portanto descobrir [qual coleção](remoteapp-collections.md) funciona melhor para você. 

### <a name="updating-your-collection"></a>Atualizando sua coleção
Uma das principais diferenças entre coleções de nuvem e híbridos Olá Olá é como as atualizações de software são tratadas. Com uma coleção de nuvem que usa a imagem pré-instalada Olá Office 365 ProPlus ou Office 2013, você não tem tooworry sobre as atualizações. serviço Olá mantém em si e distribui atualizações em uma base contínua, os aplicativos de tooboth e sistema operacional de saudação.

Para coleções de híbrida, bem como coleções de nuvem que usar uma imagem de modelo personalizado, você é responsável pela manutenção de aplicativos e a imagem de saudação. Para imagens de domínio, você pode controlar atualizações usando ferramentas como o Windows Update, a Diretiva de grupo ou o System Center.

Depois de atualizar a imagem de modelo personalizado, você carrega Olá de nova imagem toohello nuvem do Azure e atualize Olá coleção toouse Olá nova imagem. (Você pode fazer isso de saudação do Azure RemoteApp **início rápido** página ou Olá painel.)

Veja [Atualizar sua coleção](remoteapp-update.md) para obter mais informações.

## <a name="supported-remoteapp-clients"></a>Clientes com suporte do RemoteApp
Há suporte para o RemoteApp do Azure para Mac, iOS e Android em aplicativos de cliente de RemoteApp Olá para Windows e Windows RT, bem como aplicativos de área de trabalho remota Microsoft hello. Os usuários podem usar esses aplicativos no seu celular ou computação dispositivos tooaccess Olá novos programas RemoteApp do Azure.

Consulte [acessar seus aplicativos no Azure RemoteApp](remoteapp-clients.md) para obter mais informações sobre clientes hello.

## <a name="next-steps"></a>Próximas etapas
Vá! Experimente! Estes artigos ajudam a começar com o Azure RemoteApp:

* [Que tipo de coleção é necessária para o Azure RemoteApp?](remoteapp-collections.md)
* [Criar uma imagem de RemoteApp do Azure](remoteapp-imageoptions.md)
* [Como toocreate uma coleção de nuvem do Azure RemoteApp](remoteapp-create-cloud-deployment.md)
* [Como toocreate uma coleção híbrida do RemoteApp do Azure](remoteapp-create-hybrid-deployment.md)
* [Como o licenciamento funciona no RemoteApp do Azure?](remoteapp-licensing.md)
* [Práticas recomendadas para usar o RemoteApp do Azure](remoteapp-bestpractices.md)
* [Perguntas frequentes sobre o RemoteApp do Azure](remoteapp-faq.md)

### <a name="help-us-help-you"></a>Ajude-nos a ajudar você
Você sabia que na adição toorating neste artigo e fazer comentários para baixo abaixo, você pode fazer alterações toohello artigo? Falta alguma coisa? Há algo errado? Escrevi algo que não ficou muito claro? Role para cima e clique em **Editar no GitHub** ou **editar** toomake alterações - aqueles virão toous para revisão e, em seguida, uma vez que saia neles, você verá suas alterações e aprimoramentos aqui.

