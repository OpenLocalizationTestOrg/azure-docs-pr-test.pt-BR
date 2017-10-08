---
title: "Azure AD Connect: Logon Único Contínuo – Início Rápido| Microsoft Docs"
description: Este artigo descreve como tooget iniciada com o Azure Active Directory perfeita Single Sign-On.
services: active-directory
keywords: "o que é o Azure AD Connect, instalar o Active Directory, componentes necessários do Azure AD, SSO, Logon Único"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 97d40ed41b3bfad9ff7e11ddbdb8de594ee85de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-quick-start"></a>Logon Único Contínuo do Azure Active Directory: Início Rápido

## <a name="how-toodeploy-seamless-sso"></a>Como toodeploy SSO contínuo

Azure Active Directory perfeita SSO (Azure AD perfeita SSO) assina automaticamente os usuários quando eles estão na sua rede corporativa de tooyour conectado de áreas de trabalho corporativas. Ele fornece a seus usuários fácil acesso tooyour baseado em nuvem aplicativos sem a necessidade de todos os componentes locais adicionais.

>[!IMPORTANT]
>recurso de SSO contínuo Hello está atualmente em visualização.

toodeploy SSO contínuo, você precisa toofollow estas etapas:

## <a name="step-1-check-prerequisites"></a>Etapa 1: verificar pré-requisitos

Certifique-se de que Olá pré-requisitos a seguir foram atendidos:

1. Configurar seu servidor do Azure AD Connect: se você usa a [Autenticação de Passagem](active-directory-aadconnect-pass-through-authentication.md) como seu método de entrada, nenhuma ação adicional é necessária. Se você usa a [Sincronização de Hash de Senha](active-directory-aadconnectsync-implement-password-synchronization.md) como seu método de entrada e se há um firewall entre o Azure AD Connect e Azure AD, verifique se:
- Você está usando versões 1.1.484.0 ou posteriores do Azure AD Connect.
- O Azure AD Connect pode se comunicar com URLs `*.msappproxy.net` e sobre a porta 443. Esse pré-requisito é aplicável somente ao habilitar o recurso de hello, não para logons de usuário real.
- Conexão do AD do Azure pode tornar toohello de conexões IP direto [Datacenter do Azure intervalos IP](https://www.microsoft.com/download/details.aspx?id=41653). Novamente, esse pré-requisito é aplicável somente quando você habilitar o recurso de saudação.
2. Você precisa ter credenciais de administrador de domínio para cada floresta do AD que você sincronize tooAzure AD (usando o Azure AD Connect) e cujos usuários você deseja tooenable SSO contínuo.

## <a name="step-2-enable-hello-feature"></a>Etapa 2: Habilitar o recurso de saudação

O SSO Contínuo pode ser habilitado usando o [Azure AD Connect](active-directory-aadconnect.md).

Se você estiver fazendo uma instalação nova do Azure AD Connect, escolha Olá [caminho de instalação personalizado](active-directory-aadconnect-get-started-custom.md). Em hello "usuário" página de entrada, marque a opção de "Habilitar logon único" de saudação.

![Azure AD Connect – Entrada do usuário](./media/active-directory-aadconnect-sso/sso8.png)

Se você já tem uma instalação do Azure AD Connect, escolha "Alterar página de entrada do usuário" no Azure AD Connect e clique em "Avançar". Em seguida, marque a opção de "Habilitar logon único" de saudação.

![Azure AD Connect – Alterar entrada do usuário](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

Prossiga com o assistente Olá até chegar a página de "Habilitar logon único" toohello. Forneça credenciais de administrador de domínio para cada floresta do AD que você sincronize tooAzure AD (usando o Azure AD Connect) e cujos usuários você deseja tooenable SSO contínuo. 

Após a conclusão do Assistente de saudação, SSO contínua está habilitada em seu locatário.

>[!NOTE]
> credenciais de administrador de domínio Olá não são armazenadas no Azure AD Connect ou no AD do Azure, mas são somente o recurso de saudação tooenable usado.

Siga essas tooverify instruções que você tenha ativado SSO contínuo corretamente:

1. Entrar toohello [Centro de administração do Active Directory do Azure](https://aad.portal.azure.com) com credenciais de Administrador Global de saudação para seu locatário.
2. Selecione **Active Directory do Azure** na navegação esquerda hello.
3. Selecione **Azure AD Connect**.
4. Verifique se esse Olá **logon único perfeita** recurso mostra como **habilitado**.

![Portal do Azure – folha do Azure AD Connect](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="step-3-roll-out-hello-feature"></a>Etapa 3: Implantar o recurso de saudação

tooroll usuários de tooyour recurso hello, terá as configurações de zona de Intranet dos tooadd duas URLs do AD do Azure (https://autologon.microsoftazuread-sso.com e https://aadg.windows.net.nsatc.net) toousers por meio da política de grupo no Active Directory.

>[!NOTE]
> Olá seguindo as instruções só funciona para o Internet Explorer e Google Chrome no Windows (se ele compartilha o conjunto de URLs de sites confiáveis no Internet Explorer). Ler a próxima seção Olá para instruções tooset Mozilla Firefox e Google Chrome no Mac.

### <a name="why-do-you-need-toomodify-users-intranet-zone-settings"></a>Por que você precisa de configurações da zona de Intranet toomodify dos usuários?

Por padrão, o navegador Olá calcula automaticamente zona de saudação à direita (Internet ou Intranet) de uma URL. Por exemplo, http://contoso/ é mapeado toohello zona de Intranet, enquanto http://intranet.contoso.com/ é mapeada toohello da zona da Internet (como Olá URL contém um ponto). Navegadores não enviam o ponto de extremidade do Kerberos tíquetes tooa nuvem - como Olá duas do Azure AD URLs - a menos que sua URL explicitamente é adicionada a zona de Intranet toohello do navegador.

### <a name="detailed-steps"></a>Etapas detalhadas

1. Abra a ferramenta de gerenciamento de diretiva de grupo de saudação.
2. Edite saudação diretiva de grupo é aplicada toosome ou todos os seus usuários. Neste exemplo, usamos Olá **Default Domain Policy**.
3. Navegue muito**página do usuário \ Modelos Administrativos\Componentes do Windows\Internet Explorer controle Panel\Security** e selecione **tooZone lista de atribuição de Site**.
![Logon Único](./media/active-directory-aadconnect-sso/sso6.png)  
4. Habilitar a política de Olá e digite hello valores (URLs AD do Azure onde os tíquetes Kerberos são encaminhados) a seguir e dados (*1* indica a zona da Intranet) na caixa de diálogo de saudação.

        Value: https://autologon.microsoftazuread-sso.com
        Data: 1
        Value: https://aadg.windows.net.nsatc.net
        Data: 1
>[!NOTE]
> Se você quiser toodisallow alguns usuários usem SSO contínuo - por exemplo, se esses usuários estão entrando em quiosques compartilhados - defina Olá anterior valores muito*4*. Essa ação adiciona Olá URLs do AD do Azure toohello zona restrita e falha todo o tempo de saudação de SSO contínuo.

5. Clique em **OK** e em **OK** novamente.

![Logon único](./media/active-directory-aadconnect-sso/sso7.png)

### <a name="browser-considerations"></a>Considerações de navegador

#### <a name="mozilla-firefox"></a>Mozilla Firefox

O Mozilla Firefox não faz a autenticação Kerberos automaticamente. Cada usuário tem toomanually adicionar configurações de saudação do AD do Azure URLs tootheir Firefox usando Olá etapas a seguir:
1. Execute o Firefox e digite `about:config` na barra de endereços de saudação. Ignore as notificações que aparecerem.
2. Pesquise Olá **network.negotiate-auth.trusted-uris** preferência. Esta preferência lista os sites confiáveis do Firefox para a autenticação Kerberos.
3. Clique com o botão direito do mouse e selecione "Modificar".
4. Insira "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net" no campo de saudação.
5. Clique em "Okey" e reabra o navegador hello.

#### <a name="safari-on-mac-os"></a>Safari no Mac OS

Verifique essa máquina Olá executando o Mac OS tooAD unida. Consulte as instruções sobre como toodo que [aqui](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).

#### <a name="google-chrome-on-mac-os"></a>Google Chrome no Mac OS

Para o Google Chrome no Mac OS e outras plataformas não Windows, consulte muito[neste artigo](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) para obter informações sobre como toowhitelist Olá URLs do AD do Azure para a autenticação integrada.

Usando a diretiva de grupo de Active Directory de terceiros tooroll extensões Olá URLs do AD do Azure tooFirefox e Google Chrome em usuários do Mac está fora do escopo deste artigo.

#### <a name="known-limitations"></a>Limitações conhecidas

O SSO Contínuo não funciona no modo de navegação particular em navegadores Firefox e Edge. Também não funciona no Internet Explorer se Olá navegador é executado no modo de proteção aprimorada.

>[!IMPORTANT]
>Podemos recentemente revertida suporte para a borda tooinvestigate problemas reportados por clientes.

## <a name="step-4-test-hello-feature"></a>Etapa 4: Testar o recurso de saudação

recurso de saudação tootest para um usuário específico, certifique-se de que _todos os_ Olá condições a seguir foram atendidos:
  - usuário Hello está entrando em um dispositivo corporativo.
  - dispositivo de saudação foi tooyour anteriormente ingressado no domínio de AD (Active Directory).
  - dispositivo Olá tem uma conexão direta de tooyour Domain Controller (DC), na rede corporativa Olá com ou sem fio ou por uma conexão de acesso remoto, como uma conexão VPN.
  - Você tem [distribuiu recurso Olá](##step-3-roll-out-the-feature) toothis usuário usando a diretiva de grupo.

cenário de saudação tootest onde o usuário de Olá insere apenas Olá nome de usuário, mas a senha não é hello:
- Entre no *https://myapps.microsoft.com/* em uma nova sessão privativa do navegador.

cenário de saudação tootest onde o usuário Olá não tem senha de nome de usuário ou Olá Olá tooenter: 
- Entre no *https://myapps.microsoft.com/contoso.onmicrosoft.com* em uma nova sessão privativa do navegador. Substitua "*contoso*" pelo nome do seu locatário.
- Ou entre no *https://myapps.microsoft.com/contoso.com* em uma nova sessão privativa do navegador. Substitua "*contoso.com*" por um domínio verificado (não um domínio federado) em seu locatário.

## <a name="step-5-roll-over-keys"></a>Etapa 5: Sobrepor chaves

Na etapa 2, o Azure AD Connect cria contas de computador (representando o AD do Azure) em todas as florestas Olá AD no qual você habilitou o SSO contínuo. Saiba mais detalhes [aqui](active-directory-aadconnect-sso-how-it-works.md). Para maior segurança, é recomendável que você frequentemente mudarem chaves de descriptografia de Kerberos Olá dessas contas de computador.

>[!IMPORTANT]
>Você não precisará desta etapa toodo _imediatamente_ depois que você habilitou o recurso de saudação. Sobrepor chaves de descriptografia de Kerberos Olá pelo menos a cada 30 dias.

## <a name="next-steps"></a>Próximas etapas

- [**Aprofundamento técnico**](active-directory-aadconnect-sso-how-it-works.md) – entenda como esse recurso funciona.
- [**Perguntas frequentes sobre** ](active-directory-aadconnect-sso-faq.md) -respostas toofrequently perguntas frequentes.
- [**Solucionar problemas de** ](active-directory-aadconnect-troubleshoot-sso.md) -Saiba como tooresolve comum problemas com o recurso de saudação.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) – para registrar solicitações de novos recursos.
