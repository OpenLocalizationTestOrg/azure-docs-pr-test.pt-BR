---
title: aaaEnable tooSharePoint de acesso remoto com o Proxy de aplicativo do Azure AD | Microsoft Docs
description: "Aborda os conceitos básicos de saudação sobre como toointegrate um servidor do SharePoint no local com o Proxy de aplicativo do Azure AD."
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
ms.date: 07/21/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 6ab413462fcaf387e150449df9c97505c4108bcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-access-toosharepoint-with-azure-ad-application-proxy"></a>Habilitar acesso remoto tooSharePoint com Proxy de aplicativo do Azure AD

Este artigo aborda como toointegrate um servidor do SharePoint no local com o Proxy de aplicativo do Azure Active Directory (AD do Azure).

tooenable tooSharePoint de acesso remoto com o Proxy de aplicativo do AD do Azure, siga as seções de saudação neste artigo passo a passo.

## <a name="prerequisites"></a>Pré-requisitos

Este artigo pressupõe que você já tenha o SharePoint 2013 ou mais recente no seu ambiente. Além disso, considere Olá pré-requisitos a seguir:

* O SharePoint inclui suporte nativo a Kerberos. Portanto, os usuários que estão acessando remotamente sites internos por meio do Proxy de aplicativo do Azure AD podem assumir toohave um único (SSO) experiência de logon.

* É necessário toomake alguns servidor SharePoint alterações tooyour de configuração. É recomendável usar um ambiente de preparo. Dessa forma, você pode fazer atualizações tooyour primeiro o servidor de preparo e, em seguida, facilitar um ciclo de teste antes de entrar em produção.

* Vamos supor que você já configurou o SSL para o SharePoint, porque não precisamos que SSL no hello publicado URL. Você precisa toohave que SSL habilitado em seu site interno, tooensure que links são enviadas/mapeada corretamente. Se você ainda não configurou o SSL, consulte [Configurar o SSL para o SharePoint 2013](https://blogs.msdn.microsoft.com/fabdulwahab/2013/01/20/configure-ssl-for-sharepoint-2013) para obter instruções. Além disso, certifique-se que Olá conector relações de confiança Olá certificado do computador que você execute. (certificado de saudação não precisa toobe emitido publicamente.)

## <a name="step-1-set-up-single-sign-on-toosharepoint"></a>Etapa 1: Configurar tooSharePoint de logon único

Os clientes desejam Olá SSO melhor experiência para seus aplicativos de back-end, o servidor do SharePoint nesse caso. Nesse cenário comum do AD do Azure, o usuário de saudação é autenticado apenas uma vez, porque eles não serão solicitados para a autenticação novamente.

Para aplicativos locais que exigem nem usam a autenticação do Windows, você pode obter o SSO, usando o protocolo de autenticação Kerberos hello e um recurso chamado delegação restringido de Kerberos (KCD). KCD, quando configurado, permite Olá tooobtain de conector de Proxy de aplicativo windows tíquete/token para um usuário, mesmo se o usuário Olá não conectado tooWindows diretamente. toolearn mais sobre o KCD, consulte [visão geral da delegação restrita de Kerberos](https://technet.microsoft.com/library/jj553400.aspx).

tooset o KCD para um servidor do SharePoint, use os procedimentos Olá Olá sequenciais seções a seguir:

### <a name="ensure-that-sharepoint-is-running-under-a-service-account"></a>Certificar-se de que SharePoint está em execução como uma conta de serviço

Primeiro, certifique-se de que o SharePoint está em execução em uma conta de serviço e não no sistema local, serviço local ou serviço de rede. Faça isso para que você pode anexar uma conta válida do serviço (SPNs) nomes de entidade tooa. Os SPNs são como Olá protocolo Kerberos identifica serviços diferentes. E você será necessário Olá conta posterior tooconfigure Olá KCD.

tooensure seus sites executados sob uma conta de serviço definido, execute Olá etapas a seguir:

1. Olá abrir **Administração Central do SharePoint 2013** site.
2. Vá muito**segurança** e selecione **configurar contas de serviço**.
3. Selecione **Pool de Aplicativos Web – SharePoint – 80**. Olá opções podem ser ligeiramente diferentes com base no nome de saudação do seu pool de web, ou se hello pool da web usa SSL por padrão.

  ![Opções para configurar uma conta de serviço](./media/application-proxy-remote-sharepoint/remote-sharepoint-service-web-application.png)

4. Se **selecionar uma conta para este componente** é **Serviço Local** ou **serviço de rede**, você precisa toocreate uma conta. Caso contrário, você tiver terminado e pode mover toohello próxima seção.
5. Escolha **Registrar uma nova conta gerenciada**. Depois que a conta é criada, você deve definir **Pool de aplicativos Web** antes que você pode usar a conta de saudação.

> [!NOTE]
É necessário toohave um previamente criado a conta do AD do Azure para o serviço de saudação. Sugerimos que você permita uma alteração automática de senha. Para obter mais informações sobre o conjunto completo de saudação de etapas e resolução de problemas, consulte [configurar alteração automática de senha no SharePoint 2013](https://technet.microsoft.com/library/ff724280.aspx).

### <a name="configure-sharepoint-for-kerberos"></a>Configurar o SharePoint para Kerberos

Usar KCD tooperform único logon toohello servidor do SharePoint, e isso só funciona com Kerberos.

tooconfigure do site do SharePoint para a autenticação Kerberos:

1. Olá abrir **Administração Central do SharePoint 2013** site.
2. Vá muito**gerenciamento de aplicativos**, selecione **gerenciar aplicativos web**e selecione o site do SharePoint. Neste exemplo, é **SharePoint - 80**.

  ![Selecionar site de SharePoint Olá](./media/application-proxy-remote-sharepoint/remote-sharepoint-manage-web-applications.png)

3. Clique em **provedores de autenticação** na barra de ferramentas de saudação.
4. Em Olá **provedores de autenticação** , clique em **zona padrão** tooview configurações de saudação.
5. Em Olá **Editar autenticação** caixa de diálogo caixa, role para baixo até ver **tipos de autenticação de declarações** e certifique-se de que ambos **habilitar autenticação do Windows** e  **Autenticação integrada do Windows** são selecionados.
6. Na caixa de lista suspensa de saudação, verifique se **negociação (Kerberos)** está selecionado.

  ![Caixa de diálogo Editar Autenticação](./media/application-proxy-remote-sharepoint/remote-sharepoint-service-edit-authentication.png)

7. Na parte inferior de saudação do hello **Editar autenticação** caixa de diálogo, clique em **salvar**.

### <a name="set-a-service-principal-name-for-hello-sharepoint-service-account"></a>Definir um nome de serviço principal para Olá conta de serviço do SharePoint

Antes de configurar Olá KCD, você precisa de serviço de SharePoint Olá de tooidentify em execução como conta de serviço de saudação que você configurou. Você pode fazer isso configurando um SPN. Para saber mais, confira [Service Principal Names](https://technet.microsoft.com/library/cc961723.aspx) (Nomes da entidade de serviço).

formato SPN Olá é:

```
<service class>/<host>:<port>
```

No formato SPN hello:

* _classe de serviço_ é um nome exclusivo para o serviço de saudação. Para o SharePoint, você usa **HTTP**.

* _host_ é de domínio totalmente qualificado da saudação ou nome NetBIOS do host Olá Olá serviço está em execução no. Para um site do SharePoint, esse texto talvez seja necessário toobe Olá URL do site hello, dependendo da versão de saudação do IIS que você está usando.

* _port_ é opcional.

Se for Olá FQDN do servidor do SharePoint hello:

```
sharepoint.demo.o365identity.us
```

Em seguida, Olá SPN é:

```
HTTP/ sharepoint.demo.o365identity.us demo
```

Talvez você também precise tooset SPNs para sites específicos em seu servidor. Para obter mais informações, confira [Configurar a autenticação Kerberos](https://technet.microsoft.com/library/cc263449(v=office.12).aspx). Preste muita atenção toohello seção "Criar nomes de entidade de serviço para seus aplicativos Web usando a autenticação Kerberos".

saudação de maneira mais fácil para você tooset SPNs é toofollow formatos de SPN de saudação que podem já estar presentes para seus sites. Copie esses tooregister SPNs na conta de serviço de saudação. toodo isso:

1. Navegue até site toohello com Olá SPN de outro computador.
 Quando você, Olá conjunto relevante de tíquetes Kerberos é armazenado em cache na máquina de saudação. Esses tíquetes contêm Olá SPN do local de destino de saudação navegou para.

2. Você pode extrair Olá SPN para o site usando uma ferramenta chamada [Klist](http://web.mit.edu/kerberos/krb5-devel/doc/user/user_commands/klist.html). Em uma janela de comando que está sendo executado no hello mesmo contexto de usuário Olá Olá acessados site no navegador hello, executar Olá comando a seguir:
```
Klist
```
Klist, em seguida, retorna o conjunto de saudação do destino SPNs. Neste exemplo, o valor de saudação realçada é Olá SPN é necessário:

  ![Resultados do Klist de exemplo](./media/application-proxy-remote-sharepoint/remote-sharepoint-target-service.png)

4. Agora que você tem Olá SPN, você precisa toomake-se de que ele está configurado corretamente na conta de serviço de saudação que você configurou para o aplicativo de web hello anteriormente. Execute Olá comando a seguir no prompt de comando hello como um administrador de domínio hello:

 ```
 setspn -S http/sharepoint.demo.o365identity.us demo\sp_svc
 ```

 Este comando define Olá SPN para o serviço do SharePoint Olá conta em execução como _demo\sp_svc_.

 Substituir _http/sharepoint.demo.o365identity.us_ com hello SPN para o servidor e _demo\sp_svc_ com conta de serviço de saudação em seu ambiente. Olá Setspn comando procura Olá SPN antes de adicionar a ele. Nesse caso, você poderá ver um erro **Valor de SPN duplicado**. Se você vir esse erro, certifique-se de que o valor de saudação é associado à conta de serviço de saudação.

Você pode verificar que Olá que SPN foi adicionado, executando o comando Setspn de saudação com hello -l opção. toolearn mais sobre esse comando, consulte [Setspn](https://technet.microsoft.com/library/cc731241.aspx).

### <a name="ensure-that-hello-connector-is-set-as-a-trusted-delegate-toosharepoint"></a>Certifique-se de que esse conector Olá é definido como um delegado confiável tooSharePoint

Configure Olá KCD para que o serviço de Proxy de aplicativo do Azure AD Olá pode delegar o serviço do usuário identidades toohello do SharePoint. Você fazer isso habilitando o conector de Proxy de aplicativo hello tooretrieve os tíquetes Kerberos para os usuários autenticados no AD do Azure. Esse servidor passa aplicativo de destino do hello contexto toohello ou SharePoint nesse caso.

Olá tooconfigure KCD, Olá Repita etapas para cada computador do conector:

1. Faça logon como um administrador de domínio tooa controlador de domínio e, em seguida, abra **computadores e usuários do Active Directory**.
2. Localize computador Olá Olá conector está em execução no. Neste exemplo, ele tem Olá mesmo servidor do SharePoint.
3. Clique duas vezes em computador Olá e clique em Olá **delegação** guia.
4. Verifique se as configurações de delegação de saudação são definidas muito**confiar no computador para delegação toohello especificado apenas serviços**e, em seguida, selecione **usar qualquer protocolo de autenticação**.

  ![Configurações de delegação](./media/application-proxy-remote-sharepoint/remote-sharepoint-delegation-box.png)

5. Clique em Olá **adicionar** , clique em **usuários ou computadores**e localize a conta de serviço de saudação.

  ![Adicionando Olá SPN para a conta de serviço Olá](./media/application-proxy-remote-sharepoint/remote-sharepoint-users-computers.png)

6. Na lista de saudação de SPNs, selecione Olá que você criou anteriormente para a conta de serviço de saudação.
7. Clique em **OK**. Clique em **Okey** toosave novamente as alterações de saudação.

## <a name="step-2-enable-remote-access-toosharepoint"></a>Etapa 2: Habilitar acesso remoto tooSharePoint

Agora que você tenha habilitado do SharePoint para Kerberos e configurou o KCD, você está pronto tooset backup tooSharePoint de logon único. Em seguida, do conector Olá, você pode publicar farm do SharePoint Olá para acesso remoto por meio do Proxy de aplicativo do Azure AD.

Olá tooperform seguintes etapas, você precisa toobe um membro de função de Administrador Global do hello na conta do Azure Active Directory da sua organização.

1. Entrar toohello [portal do Azure](https://manage.windowsazure.com) e localize seu locatário do AD do Azure.
2. Clique em **Aplicativos** e em **Adicionar**.
3. Selecione **Publicar um aplicativo que estará acessível fora de sua rede**. Se você não vir essa opção, certifique-se de que você tenha Azure AD Basic ou Premium configura locatário hello.
4. Execute cada uma das opções de saudação da seguinte maneira:
 * **Nome**: use qualquer valor que você queira, por exemplo, **SharePoint**.
 * **URL interna**: esta é a URL de saudação do site do SharePoint Olá internamente, como **https://SharePoint/**. Neste exemplo, verifique se toouse **https**.
 * **Método de Pré-autenticação**: selecione **Azure Active Directory**.

  ![Opções para adicionar um aplicativo](./media/application-proxy-remote-sharepoint/remote-sharepoint-add-application.png)

5. Depois que o aplicativo hello é publicado, clique em Olá **configurar** guia.
6. Role para baixo a opção toohello **traduzir URL nos cabeçalhos**. valor padrão de saudação é **Sim**. Alterá-la muito**não**.

 SharePoint usa Olá _cabeçalho de Host_ toolook valor site hello. Ele também gera links com base nesse valor. efeito de saudação é toomake-se de que qualquer link de SharePoint gera uma URL publicada que está configurada corretamente a URL externa do toouse hello. Definir o valor de saudação muito**Sim** também habilita Olá aplicativos de back-end do conector tooforward Olá solicitação toohello. No entanto, definir o valor de saudação muito**não** significa que Olá conector não enviará o nome de host interno hello. Em vez disso, o conector de Olá envia cabeçalho de host Olá Olá publicado aplicativos de back-end de toohello de URL.

 Além disso, tooensure que SharePoint aceita essa URL, você precisa toocomplete uma configuração mais no servidor do SharePoint hello. Você vai fazer isso na próxima seção, Olá.

7. Alterar **método de autenticação interna** muito**autenticação integrada do Windows**. Se o seu locatário do AD do Azure usa um UPN na nuvem de saudação que é diferente do hello UPN local, lembre-se tooupdate **identidade de logon recebido** também.
8. Definir **SPN do aplicativo interno** toohello valor que você definiu anteriormente. Por exemplo, **http/sharepoint.demo.o365identity.us**.
9. Atribua Olá aplicativo tooyour usuários de destino.

Seu aplicativo deve ter aparência semelhante toohello exemplo a seguir:

  ![Aplicativo concluído](./media/application-proxy-remote-sharepoint/remote-sharepoint-internal-application-spn.png)

## <a name="step-3-ensure-that-sharepoint-knows-about-hello-external-url"></a>Etapa 3: Certifique-se de que o SharePoint sabe sobre a URL externa de saudação

Sua última tooensure etapa SharePoint pode encontrar o site Olá com base na URL externa de hello, para que ele processará links de acordo com essa URL externa. Você pode fazer isso ao configurar mapeamentos alternativos de acesso para o site do SharePoint hello.

1. Olá abrir **Administração Central do SharePoint 2013** site.
2. Em **Configurações do Sistema**, selecione **Configurar Mapeamentos Alternativos de Acesso**.

 Isso abre o hello **mapeamentos alternativos de acesso** caixa.

  ![Caixa Mapeamentos Alternativos de Acesso](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access1.png)

3. Na lista suspensa de saudação ao lado **o conjunto de mapeamento de acesso alternativo**, selecione **coleção de mapeamento de acesso alternativo alteração**.
4. Selecione o seu site, por exemplo **SharePoint – 80**.

  ![Selecionar um site](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access2.png)

5. Você pode escolher tooadd Olá publicado URL como uma URL interna ou uma URL pública. Este exemplo usa uma URL pública como Olá extranet.
6. Clique em **editar URLs públicas** em Olá **Extranet** caminho e, em seguida, digite caminho Olá Olá publicou o aplicativo, como na etapa anterior hello. Por exemplo, **https://sharepoint-iddemo.msappproxy.net**.

  ![Inserir caminho Olá](./media/application-proxy-remote-sharepoint/remote-sharepoint-alternate-access3.png)

7. Clique em **Salvar**.

 Agora você pode acessar o site do SharePoint Olá externamente por meio do Proxy de aplicativo do Azure AD.

## <a name="next-steps"></a>Próximas etapas

- [Como tooprovide proteger o acesso remoto aplicativos tooon locais](active-directory-application-proxy-get-started.md)
- [Noções básicas sobre conectores de Proxy de Aplicativo do Azure AD](application-proxy-understand-connectors.md)
- [Publicando o SharePoint 2016 e o Servidor do Office Online com o Proxy de Aplicativo do Azure AD](https://blogs.technet.microsoft.com/dawiese/2016/06/09/publishing-sharepoint-2016-and-office-online-server-with-azure-ad-application-proxy/)
