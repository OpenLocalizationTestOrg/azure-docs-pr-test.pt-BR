---
title: aplicativos com reconhecimento de aaaClaims - Proxy de aplicativo do Azure AD | Microsoft Docs
description: "Como toopublish local aplicativos ASP.NET que aceitam declarações do ADFS para acesso remoto seguro pelos usuários."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: harshja
ms.assetid: 91e6211b-fe6a-42c6-bdb3-1fff0312db15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 7be633225de700226c7c94815eb91b3de2b61cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-claims-aware-apps-in-application-proxy"></a>Trabalho com aplicativos com reconhecimento de declarações no Proxy de Aplicativo
[Aplicativos com reconhecimento de declarações](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) executar um serviço de Token de segurança (STS) de toohello de redirecionamento. Olá STS solicita as credenciais do usuário de saudação em troca de um token e, em seguida, redireciona o aplicativo de toohello usuário hello. Há algumas maneiras tooenable Proxy de aplicativo toowork com esses redirecionamentos. Use este artigo tooconfigure sua implantação para aplicativos com reconhecimento de declarações. 

## <a name="prerequisites"></a>Pré-requisitos
Certifique-se de que Olá STS que Olá aplicativo com reconhecimento de declarações redireciona toois disponível fora de sua rede local. Você pode disponibilizar Olá STS, expondo-lo por meio de um proxy ou permitindo fora de conexões. 

## <a name="publish-your-application"></a>Publicar seu aplicativo

1. Publicar seu aplicativo de acordo com as instruções de toohello descritas em [publicar aplicativos com Proxy de aplicativo](application-proxy-publish-azure-portal.md).
2. Navegue toohello página de aplicativo no hello portal e selecione **o logon único**.
3. Se você tiver escolhido **Azure Active Directory** como seu **Método de Pré-autenticação**, selecione **Logon único do Azure AD desabilitado** como seu **Método de Autenticação Interno**. Se você escolheu **passagem** como seu **método de pré-autenticação**, você não precisa toochange nada.

## <a name="configure-adfs"></a>Configurar o ADFS

Você pode configurar o ADFS para aplicativos com reconhecimento de declarações de uma de duas maneiras. Olá primeiro é usar domínios personalizados. Olá segundo é com o WS-Federation. 

### <a name="option-1-custom-domains"></a>Opção 1: Domínios personalizados

Se todos Olá URLs internas para seus aplicativos são totalmente qualificados (FQDNs) de nomes de domínio, você pode configurar [domínios personalizados](active-directory-application-proxy-custom-domains.md) para seus aplicativos. Use Olá domínios personalizados toocreate URLs externas que são Olá mesmo Olá URLs internas. Quando suas URLs externas correspondem as URLs internas, redirecionamentos de STS Olá funcionam se os usuários estão no local ou remoto. 

### <a name="option-2-ws-federation"></a>Opção 2: especificação Web Services Federation

1. Abra o Gerenciamento de ADFS.
2. Vá muito**terceira parte confiável**, clique no aplicativo hello está sendo publicado com Proxy de aplicativo e escolha **propriedades**.  

   ![Confianças em Terceiras Partes Confiáveis, clique com o botão direito do mouse no nome do aplicativo - captura de tela](./media/active-directory-application-proxy-claims-aware-apps/appproxyrelyingpartytrust.png)  

3. Em Olá **pontos de extremidade** guia em **tipo de ponto de extremidade**, selecione **WS-Federation**.
4. Em **confiável URL**, digite Olá URL inserida em Olá Proxy de aplicativo em **URL externa** e clique em **Okey**.  

   ![Adicionar um ponto de extremidade - definir valor de URL Confiável - captura de tela](./media/active-directory-application-proxy-claims-aware-apps/appproxyendpointtrustedurl.png)  

## <a name="next-steps"></a>Próximas etapas
* [Habilitar logon único](application-proxy-sso-overview.md) para aplicativos sem reconhecimento de declarações
* [Habilitar toointeract de aplicativos cliente nativo com aplicativos de proxy](active-directory-application-proxy-native-client.md)


