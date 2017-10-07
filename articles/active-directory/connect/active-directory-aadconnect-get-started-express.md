---
title: "Introdução ao Azure AD Connect usando configurações expressas | Microsoft Docs"
description: "Saiba como toodownload, instalar e executar o Assistente de instalação de saudação do Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: curtand
ms.assetid: b6ce45fd-554d-4f4d-95d1-47996d561c9f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 79f796fa7738b85e9236e856bddb529379f60390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-ad-connect-using-express-settings"></a>Introdução ao Azure AD Connect usando configurações expressas
As **configurações expressas** do Azure AD Connect são usadas quando você tem uma topologia de floresta única e a [sincronização de senha](active-directory-aadconnectsync-implement-password-synchronization.md) para autenticação. **Configurações expressas** é a opção padrão de saudação e é usada para o cenário de hello mais comumente implantado. Você está apenas alguns cliques curto ausente tooextend sua nuvem de toohello de diretório local.

Antes de iniciar a instalação do Azure AD Connect, certifique-se muito[download do Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771) e etapas de pré-requisito concluída Olá no [do Azure AD Connect: pré-requisitos de Hardware e](active-directory-aadconnect-prerequisites.md).

Se configurações expressas não corresponderem à sua topologia, confira a [documentação relacionada](#related-documentation) para outros cenários.

## <a name="express-installation-of-azure-ad-connect"></a>Instalação expressa do Azure AD Connect
Você pode ver essas etapas na ação Olá [vídeos](#videos) seção.

1. Entrar como um servidor de toohello de administrador local que desejar tooinstall do Azure AD Connect em. Você deve fazer isso no servidor de saudação desejar que o servidor de sincronização de saudação toobe.
2. Navegue tooand duas vezes em **AzureADConnect.msi**.
3. Na tela de boas-vindas hello, selecione Olá caixa comum acordo toohello, termos de licença e clique em **continuar**.  
4. Na tela de configurações do hello Express, clique em **usar configurações expressas**.  
   ![Bem-vindo tooAzure AD Connect](./media/active-directory-aadconnect-get-started-express/express.png)
5. Na tela de tooAzure AD conexão Olá, insira Olá nome de usuário e senha de um administrador global para AD do Azure. Clique em **Avançar**.  
   ![Conecte-se tooAzure AD](./media/active-directory-aadconnect-get-started-express/connectaad.png) se você recebe um erro e tiver problemas de conectividade, consulte [solucionar problemas de conectividade](active-directory-aadconnect-troubleshoot-connectivity.md).
6. Na tela de DS tooAD de conexão hello, digite Olá username e password para uma conta de administrador corporativo. Você pode inserir parte do domínio Olá no formato NetBios ou FQDN, ou seja, FABRIKAM\administrator ou fabrikam.com\administrator. Clique em **Avançar**.  
   ![Conecte-se tooAD DS](./media/active-directory-aadconnect-get-started-express/connectad.png)
7. Olá [ **configuração de entrada do AD do Azure** ](active-directory-aadconnect-user-signin.md#azure-ad-sign-in-configuration) página mostra somente se você não tiver concluído [verificar seus domínios](../active-directory-add-domain.md) em Olá [pré-requisitos](active-directory-aadconnect-prerequisites.md).
   ![Domínios não verificados](./media/active-directory-aadconnect-get-started-express/unverifieddomain.png)  
   Se essa página for mostrada, examine todos os domínios marcados como **Não Adicionado** e **Não Verificado**. Confira se os domínios que você usa foram verificados no Azure AD. Clique em símbolo de atualização hello quando você verificou se seus domínios.
8. Na tela de tooconfigure pronto do hello, clique em **instalar**.
   * Opcionalmente, na página de tooconfigure pronto do hello, você pode desmarcar Olá **iniciar o processo de sincronização de saudação assim que a configuração for concluída** caixa de seleção. Você deve desmarcar essa caixa de seleção se você quiser toodo uma configuração adicional, como [filtragem](active-directory-aadconnectsync-configure-filtering.md). Se você desmarcar essa opção, o Assistente de saudação configura a sincronização, mas deixa Agendador Olá desabilitado. Ele não será executado até você habilitá-la manualmente por [executar novamente o Assistente de instalação Olá](active-directory-aadconnectsync-installation-wizard.md).
   * Se você tiver o Exchange no Active Directory local, você também tem uma opção tooenable [ **implantação híbrida do Exchange**](https://technet.microsoft.com/library/jj200581.aspx). Habilite esta opção se você planejar toohave caixas de correio Exchange ambos na nuvem hello e local em Olá mesmo tempo.
     ![Tooconfigure pronto do Azure AD Connect](./media/active-directory-aadconnect-get-started-express/readytoconfigure.png)
9. Quando a saudação instalação for concluída, clique em **saída**.
10. Após a instalação Olá, saia e entre novamente antes de usar o Gerenciador de serviço de sincronização ou Editor de regra de sincronização.

## <a name="videos"></a>Vídeos
Para obter um vídeo sobre o uso de instalação expressa hello, consulte:

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Express-Settings/player]
> 
> 

## <a name="next-steps"></a>Próximas etapas
Agora que você tem o Azure AD Connect instalado, você pode [verificar a instalação do hello e atribuir licenças](active-directory-aadconnect-whats-next.md).

Saiba mais sobre esses recursos, que foram habilitados com instalação Olá: [atualização automática](active-directory-aadconnect-feature-automatic-upgrade.md), [impedir exclusões acidentais](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md), e [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md).

Saiba mais sobre esses tópicos comuns: [Agendador e como a sincronização tootrigger](active-directory-aadconnectsync-feature-scheduler.md).

Saiba mais sobre [Como integrar suas identidades locais ao Active Directory do Azure](active-directory-aadconnect.md).

## <a name="related-documentation"></a>documentação relacionada
| Tópico |
| --- | --- |
| Visão geral do Azure AD Connect |
| Instalar usando configurações personalizadas |
| Atualização do DirSync |
| Contas usadas para instalação |

