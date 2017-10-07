---
title: aaaAccess aplicativos de Proxy de aplicativo do Azure AD em equipes | Microsoft Docs
description: Use Proxy de aplicativo do Azure AD tooaccess seu aplicativo local por meio de Teams da Microsoft.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 13c36e43ae6349df09272e308ad4f40451cbbeb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="access-your-on-premises-applications-through-microsoft-teams"></a>Acessar seus aplicativos locais por meio do Microsoft Teams

Azure Active Directory Application Proxy fornece single sign-on tooon aplicativos locais, independentemente de onde você está e Teams Microsoft simplifica seus esforços de colaboração em um único local. Integrando Olá dois juntos significa que os usuários podem ser produtivos com seus colegas em qualquer situação. 

Os usuários poderão adicionar canais de equipes de tootheir de aplicativos de nuvem [usando guias](https://support.office.com/article/Video-Using-Tabs-7350a03e-017a-4a00-a6ae-1c9fe8c497b3?ui=en-US&rs=en-US&ad=US), mas o que acontece se esse site do SharePoint ou a ferramenta de planejamento, todos eles usarão é hospedado no local? Proxy de aplicativo é a solução de saudação. Eles podem adicionar aplicativos publicados pelo Proxy de aplicativo tootheir canais usando Olá URLs externas mesmo que eles sempre usam tooaccess seus aplicativos remotamente. E porque o Proxy de aplicativo autentica por meio do Active Directory do Azure, Olá ocorre mesmo única experiência de logon.


## <a name="install-hello-application-proxy-connector-and-publish-your-app"></a>Instalar o conector de Proxy de aplicativo hello e publicar seu aplicativo

Se você ainda não o fez, [configurar o Proxy de aplicativo para seu locatário e instalar o conector Olá](active-directory-application-proxy-enable.md). Em seguida, [publique seu aplicativo local](application-proxy-publish-azure-portal.md) para acesso remoto. Quando você estiver publicando um aplicativo hello, tome nota da URL externa Olá porque os usuários finais precisam essas informações quando adicionarem Olá tooTeams de aplicativo.

Se já tiver seus aplicativos publicados, mas não se lembra de suas URLs externas, consultá-los em Olá [portal do Azure](https://portal.azure.com). Entrar e navegue muito**Active Directory do Azure** > **aplicativos empresariais** > **todos os aplicativos** > Selecionar seu aplicativo > **Proxy de aplicativo**.

## <a name="add-your-app-tooteams"></a>Adicionar tooTeams seu aplicativo

Depois de publicar o aplicativo hello por meio do Proxy de aplicativo, informe aos usuários que eles podem adicioná-lo como uma guia diretamente em seus canais de equipes. Faça com que eles sigam estas três etapas:

1. Navegue toohello equipes de canal onde você deseja tooadd este aplicativo e selecionem  **+**  tooadd uma guia.

   ![Selecione Adicionar uma guia](./media/application-proxy-teams/add-tab.png)

2. Selecione **site** de opções da guia hello.

   ![Adicionar um site](./media/application-proxy-teams/website.png)

3. Dê um nome de guia hello e definir a URL externa do Proxy de aplicativo hello URL toohello. 

   ![Configurar a URL e o nome da guia](./media/application-proxy-teams/tab-name-url.png)

Depois que um membro de uma equipe adiciona guia hello, ele mostra todos no canal de saudação. Todos os usuários que têm acesso toohello aplicativo obtém acesso de logon único com credenciais Olá usam para Teams da Microsoft. Todos os usuários que não têm acesso toohello aplicativo verão a guia Olá em equipes, mas são bloqueados até que você conceder a eles permissões toohello local aplicativo e Olá versão publicada portal do Azure do aplicativo hello. 

## <a name="next-steps"></a>Próximas etapas

- Saiba como muito[publicar sites do SharePoint local](application-proxy-enable-remote-access-sharepoint.md) com Proxy de aplicativo.
- Configurar seu aplicativos toouse [domínios personalizados](active-directory-application-proxy-custom-domains.md) para sua URL externa. 
