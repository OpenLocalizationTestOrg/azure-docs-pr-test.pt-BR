---
title: aaaSingle logon com o Proxy de aplicativo | Microsoft Docs
description: "Aborda como tooprovide o logon único usando o Proxy de aplicativo do Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: ded0d9c9-45f6-47d7-bd0f-3f7fd99ab621
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: H1Hack27Feb2017, it-pro
ms.openlocfilehash: 0047e834cd42e057a75ebc0c5dcf860734464a05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="kerberos-constrained-delegation-for-single-sign-on-tooyour-apps-with-application-proxy"></a>Delegação restrita de Kerberos para aplicativos tooyour de logon único com o Proxy de aplicativo

Você pode fornecer o logon único para aplicativos locais, publicados por meio do Proxy do Aplicativo, que sejam protegidos com a Autenticação Integrada do Windows. Esses aplicativos exigem um tíquete Kerberos para acessar. Proxy de aplicativo usa a delegação restrita de Kerberos (KCD) toosupport esses aplicativos. 

Você pode habilitar aplicativos de tooyour de logon único usando a concessão de permissão de conectores de Proxy de aplicativo em usuários do Active Directory tooimpersonate Windows IWA (autenticação integrada). conectores de saudação usam toosend essa permissão e recebem tokens em seu nome.

## <a name="how-single-sign-on-with-kcd-works"></a>Como funciona o logon único com a KCD
Esse diagrama explica o fluxo de saudação quando um usuário tenta tooaccess um aplicativo local que usa a IWA.

![Diagrama de fluxo de autenticação do Microsoft AAD](./media/active-directory-application-proxy-sso-using-kcd/AuthDiagram.png)

1. usuário de saudação insere aplicativo hello URL tooaccess Olá local por meio do Proxy de aplicativo.
2. Proxy de aplicativo redireciona Olá solicitação tooAzure AD autenticação serviços toopreauthenticate. Neste ponto, o AD do Azure se aplica a qualquer política de autenticação e autorização aplicável, tal como autenticação multifator. Se Olá usuário for validado, o AD do Azure cria um token e envia toohello usuário.
3. usuário Olá passa Olá token tooApplication Proxy.
4. Proxy de aplicativo valida o token hello e recupera Olá Nome Principal do usuário (UPN) dele e, em seguida, envia Olá solicitação, Olá UPN e Olá toohello conector do nome Principal do serviço (SPN) por meio de um canal seguro duplamente autenticado.
5. Olá conector realiza a negociação de delegação restrita de Kerberos (KCD) com hello prem AD, representando Olá usuário tooget um aplicativo de toohello token Kerberos.
6. Do Active Directory envia o token Kerberos de saudação para Olá aplicativo toohello conector.
7. Olá conector envia Olá solicitação toohello aplicativo servidor original, usando o token do Kerberos Olá recebido do AD.
8. aplicativo Hello envia Olá resposta toohello conector, que é retornado toohello serviço de Proxy de aplicativo e, finalmente, o usuário toohello.

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar a usar o logon único para aplicativos de IWA, verifique se seu ambiente está preparado com hello definições e configurações a seguir:

* Seus aplicativos, como aplicativos Web do SharePoint, são definidos toouse autenticação integrada do Windows. Para sabe rmais, veja [Habilitar suporte para autenticação Kerberos](https://technet.microsoft.com/library/dd759186.aspx), ou para o SharePoint, consulte [Planejar a autenticação Kerberos no SharePoint 2013](https://technet.microsoft.com/library/ee806870.aspx).
* Todos os seus aplicativos têm [nome da entidade de serviço](https://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx).
* saudação em execução do servidor de saudação conector e o servidor de saudação executando o aplicativo hello estão associados ao domínio e a parte da saudação mesmo domínio ou em domínios confiáveis. Para obter mais informações sobre associação de domínio, consulte [ingressar em um domínio de tooa do computador](https://technet.microsoft.com/library/dd807102.aspx).
* servidor de saudação executando Olá conector tem atributo TokenGroupsGlobalAndUniversal do acesso tooread Olá para usuários. Essa configuração padrão pode foi afetada por ambiente Olá de proteção de segurança.

### <a name="configure-active-directory"></a>Configurar o Active Directory
configuração do Active Directory Olá varia, dependendo se o conector de Proxy de aplicativo e o servidor de aplicativo hello estão em Olá mesmo domínio ou não.

#### <a name="connector-and-application-server-in-hello-same-domain"></a>Conector e o servidor de aplicativos no hello mesmo domínio
1. No Active Directory, vá muito**ferramentas** > **usuários e computadores**.
2. Selecione o servidor de saudação executando o conector de saudação.
3. Clique com o botão direito do mouse e selecione **Propriedades** > **Delegação**.
4. Selecione **confiar no computador para delegação toospecified dos serviços somente**. 
5. Em **serviços toowhich esta conta pode apresentar credenciais delegadas** Adicionar valor Olá Olá identidade SPN saudação do servidor de aplicativos. Isso permite que os usuários tooimpersonate de conector de Proxy de aplicativo hello no AD contra aplicativos Olá definidos na lista de saudação.

   ![Captura de tela da janela Propriedades do Conector SVR](./media/active-directory-application-proxy-sso-using-kcd/Properties.jpg)

#### <a name="connector-and-application-server-in-different-domains"></a>O conector e o servidor de aplicativos estão em domínios diferentes
1. Para obter uma lista de pré-requisitos para trabalhar com o KCD entre domínios, consulte [Delegação restrita de Kerberos nos domínios](https://technet.microsoft.com/library/hh831477.aspx).
2. Saudação de uso `principalsallowedtodelegateto` propriedade Olá conector server tooenable Olá Proxy de aplicativo toodelegate para o servidor de conector hello. servidor de aplicativo Hello for `sharepointserviceaccount` e delegação de servidor de saudação é `connectormachineaccount`. Para o Windows 2012 R2, use esse código como um exemplo:

        $connector= Get-ADComputer -Identity connectormachineaccount -server dc.connectordomain.com

        Set-ADComputer -Identity sharepointserviceaccount -PrincipalsAllowedToDelegateToAccount $connector

        Get-ADComputer sharepointserviceaccount -Properties PrincipalsAllowedToDelegateToAccount

Sharepointserviceaccount pode ser a conta de máquina do SPS hello ou uma conta de serviço sob a qual Olá SPS pool de aplicativos está sendo executado.

## <a name="configure-single-sign-on"></a>Configurar o logon único 
1. Publicar seu aplicativo de acordo com as instruções de toohello descritas em [publicar aplicativos com Proxy de aplicativo](application-proxy-publish-azure-portal.md). Certifique-se de que tooselect **Active Directory do Azure** como Olá **método de pré-autenticação**.
2. Depois que o aplicativo aparece na lista de saudação de aplicativos corporativos, selecione-o e clique em **o logon único**.
3. Definir o modo de logon único Olá muito**autenticação integrada do Windows**.  
4. Digite hello **SPN do aplicativo interno** saudação do servidor de aplicativos. Neste exemplo, a saudação SPN para nosso aplicativo publicado é http/www.contoso.com. Este toobe de necessidades SPN na lista de saudação do conector de saudação do toowhich de serviços pode apresentar credenciais delegadas. 
5. Escolha Olá **identidade de logon recebido** para Olá conector toouse em nome de seus usuários. Para obter mais informações, consulte [Trabalhando com identidades diferentes de nuvem e local](#Working-with-different-on-premises-and-cloud-identities)

   ![Configuração de Aplicativo Avançada](./media/active-directory-application-proxy-sso-using-kcd/cwap_auth2.png)  


## <a name="sso-for-non-windows-apps"></a>SSO para aplicativos não Windows
Olá fluxo de delegação de Kerberos no Proxy de aplicativo do Azure AD inicia quando o AD do Azure autentica o usuário Olá na nuvem de saudação. Depois que a solicitação Olá chega no local, Olá Proxy de aplicativo do Azure AD conector emite um tíquete Kerberos em nome de usuário de saudação interagindo com hello Active Directory local. Esse processo é chamado tooas a delegação restrita de Kerberos (KCD). Olá próxima fase, uma solicitação é enviada toohello aplicativo de back-end com esse tíquete Kerberos. Há vários protocolos que definem como toosend tais solicitações. A maioria dos servidores não Windows espera Negotiate/SPNego, que agora tem suporte no Proxy de Aplicativo do AD do Azure.

Para obter mais informações sobre o Kerberos, consulte [tudo o que você deseja tooknow sobre delegação de restrita de Kerberos (KCD)](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/21/all-you-want-to-know-about-kerberos-constrained-delegation-kcd).

Os aplicativos que não são do Windows normalmente utilizam nomes de usuário ou nomes de conta SAM em vez de endereços de email de domínio. Se essa situação se aplica a aplicativos tooyour, será necessário tooconfigure Olá delegado logon identidade campo tooconnect suas identidades de aplicativo de tooyour de identidades de nuvem. 

## <a name="working-with-different-on-premises-and-cloud-identities"></a>Trabalhando com identidades diferentes de nuvem e local
Proxy de aplicativo pressupõe que os usuários tenham exatamente Olá a mesma identidade em nuvem hello e local. Se não for o caso de Olá, você pode ainda poderá usar KCD para logon único. Configurar um **delegada a identidade de logon** para cada toospecify aplicativo qual identidade deve ser usada ao executar o logon único.  

Esse recurso permite que muitas empresas que têm diferentes locais e na nuvem identidades toohave SSO de saudação nuvem local tooon aplicativos sem a necessidade de saudação usuários tooenter diferentes nomes de usuário e senhas. Isso inclui as organizações que:

* Têm vários domínios internamente (joe@us.contoso.com, joe@eu.contoso.com) e um domínio único na nuvem hello (joe@contoso.com).
* Tem o nome de domínio não roteáveis internamente (joe@contoso.usa) e um válido na nuvem hello.
* Não usem nomes de domínio internamente (joe)
* Use aliases diferentes locais e na nuvem hello. Por exemplo, joe-johns@contoso.com versus joej@contoso.com  

Com o Proxy de aplicativo, você pode selecionar quais Olá de tooobtain identidade toouse tíquete Kerberos. Essa configuração é por aplicativo. Algumas dessas opções são adequadas para sistemas que não aceitam o formato de endereço de email, e outras são desenvolvidas para logon alternativo.

![Captura de tela de parâmetro de identidade de logon delegada](./media/active-directory-application-proxy-sso-using-kcd/app_proxy_sso_diff_id_upn.png)

Se a identidade de logon delegado é usada, Olá valor pode não ser exclusivo em todos os domínios de saudação ou florestas em sua organização. Você pode evitar esse problema publicando esses aplicativos duas vezes com dois grupos diferentes de Conectores. Como cada aplicativo tem um público diferente, você pode adicionar seu domínio de diferentes tooa conectores.

### <a name="configure-sso-for-different-identities"></a>Configurar o SSO para diferentes identidades
1. Defina configurações de conexão do AD do Azure para a identidade principal Olá é o endereço de email de saudação (email). Isso é feito como parte da saudação personalizar o processo, alterando Olá **Nome Principal do usuário** campo nas configurações de sincronização de saudação. Essas configurações também determinam como os usuários fazem logon no tooOffice365 Windows10 dispositivos e outros aplicativos que usam o Azure AD como seu repositório de identidade.  
   ![Identificando a captura de tela de usuários - lista suspensa Nome UPN](./media/active-directory-application-proxy-sso-using-kcd/app_proxy_sso_diff_id_connect_settings.png)  
2. Em definições de configuração de aplicativo de Olá para o aplicativo hello você gostaria que toomodify, selecione Olá **identidade de logon recebido** toobe usado:

   * Nome UPN (por exemplo, joe@contoso.com)
   * Nome UPN alternativo (por exemplo, joed@contoso.local)
   * Nome de usuário que faz parte do nome UPN (por exemplo, joe)
   * Nome de usuário que faz parte do nome UPN alternativo (por exemplo, joed)
   * Nome de conta SAM local (depende da configuração do controlador de domínio Olá)

### <a name="troubleshooting-sso-for-different-identities"></a>Solucionando problemas de SSO para diferentes identidades
Se houver um erro no hello processo SSO, ele aparece no log de eventos de máquina Olá conector conforme explicado em [solução de problemas](application-proxy-back-end-kerberos-constrained-delegation-how-to.md).
Mas, em alguns casos, Olá solicitação é enviada com êxito aplicativo de back-end toohello enquanto este aplicativo respostas em várias outras respostas HTTP. Nesses casos de solução de problemas deve começar examinando o número de eventos 24029 na máquina de conector Olá no log de eventos de sessão de Proxy de aplicativo hello. identidade do usuário Olá que foi usada para delegação aparece no campo de "usuário" de saudação em detalhes do evento hello. Selecione tooturn no log de sessão, **Mostrar analítica e logs de depuração** no menu de exibição do Visualizador de eventos hello.

## <a name="next-steps"></a>Próximas etapas

* [Como tooconfigure um aplicativo de Proxy de aplicativo toouse delegação restrita de Kerberos](application-proxy-back-end-kerberos-constrained-delegation-how-to.md)
* [Solucionar problemas que surgirem com o Proxy de Aplicativo](active-directory-application-proxy-troubleshoot.md)


Para Olá últimas notícias e atualizações, confira Olá [blog de Proxy de aplicativo](http://blogs.technet.com/b/applicationproxyblog/)

