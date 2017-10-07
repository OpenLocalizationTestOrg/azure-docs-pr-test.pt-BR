---
title: 'Azure Active Directory Domain Services: Implantar o Proxy de Aplicativo do Azure Active Directory | Microsoft Docs'
description: "Usar o Proxy de Aplicativo do Azure AD nos domínios gerenciados do Azure Active Directory Domain Services"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 4142111231d0256960d0c02d686d51533ba2171c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-ad-application-proxy-on-an-azure-ad-domain-services-managed-domain"></a>Implantar o Proxy de Aplicativo do Azure AD em um domínio gerenciado do Azure AD Domain Services
Proxy de aplicativo do Azure AD (Active Directory) ajuda você a dar suporte a funcionários remotos publicando local aplicativos toobe acessado por meio de saudação à internet. Com os serviços de domínio do AD do Azure, você pode agora levantar shift e executando serviços de infraestrutura local tooAzure os aplicativos herdados. Em seguida, você pode publicar esses aplicativos usando Olá Proxy de aplicativo do Azure AD, tooprovide toousers de acesso remoto seguro na sua organização.

Se você estiver toohello novo Proxy de aplicativo do Azure AD, saiba mais sobre esse recurso com hello artigo a seguir: [como tooprovide proteger o acesso remoto aplicativos locais tooon](../active-directory/active-directory-application-proxy-get-started.md).


## <a name="before-you-begin"></a>Antes de começar
tarefas de saudação tooperform listadas neste artigo, você precisa:

1. Uma **assinatura do Azure**válida.
2. Um **diretório do AD do Azure** - seja sincronizado com um diretório local ou com um diretório somente na nuvem.
3. Um **licença Premium ou Azure AD Basic** é necessário toouse Olá Proxy de aplicativo do Azure AD.
4. **Serviços de domínio do AD do Azure** devem estar habilitados para diretório de saudação do AD do Azure. Se você ainda não tiver feito isso, siga todas as tarefas de saudação descritas Olá [guia de Introdução](active-directory-ds-getting-started.md).

<br>

## <a name="task-1---enable-azure-ad-application-proxy-for-your-azure-ad-directory"></a>Tarefa 1: Habilitar o Proxy de Aplicativo do Azure AD para o diretório do Azure AD
Execute Olá seguindo as etapas tooenable Olá Proxy de aplicativo do Azure AD para seu diretório do AD do Azure.

1. Entrar como um administrador no hello [portal do Azure](http://portal.azure.com).

2. Clique em **Active Directory do Azure** toobring a visão geral do directory hello. Clique em **Aplicativos empresariais**.

    ![Selecionar um diretório do Azure AD](./media/app-proxy/app-proxy-enable-start.png)
3. Clique em **Proxy de aplicativo**. Se você não tiver uma assinatura do Azure AD Basic ou Azure AD Premium, verá uma opção tooenable uma versão de avaliação. Ativar/desativar **habilitar Proxy de aplicativo?** muito**habilitar** e clique em **salvar**.

    ![Habilitar Proxy de Aplicativo](./media/app-proxy/app-proxy-enable-proxy-blade.png)
4. toodownload Olá conector, clique em Olá **conector** botão.

    ![Baixe o conector](./media/app-proxy/app-proxy-enabled-download-connector.png)
5. Na página de download do hello, aceite os termos de licença hello e acordo de privacidade e clique em Olá **baixar** botão.

    ![Confirme o download](./media/app-proxy/app-proxy-enabled-confirm-download.png)


## <a name="task-2---provision-domain-joined-windows-servers-toodeploy-hello-azure-ad-application-proxy-connector"></a>Tarefa 2 - provisão domínio servidores toodeploy Olá AD do Azure Proxy de aplicativo conector do Windows
Você precisa máquinas de virtuais de Windows Server ingressado no domínio no qual você pode instalar o conector de Proxy de aplicativo do Azure AD hello. Dependendo dos aplicativos Olá sendo publicados, você poderá tooprovision vários servidores em que o conector hello está instalado. Essa opção de implantação fornece mais disponibilidade e ajuda a lidar com cargas mais pesadas de autenticação.

Provisionar servidores de conector Olá no hello mesma rede virtual (ou uma rede virtual conectado/emparelhadas), no qual você habilitou o domínio gerenciado do serviços de domínio do AD do Azure. Da mesma forma, os servidores de Olá hospedando aplicativos Olá publicar por meio do Proxy de aplicativo de saudação precisam toobe instalado Olá mesma rede virtual do Azure.

servidores de conector tooprovision, execute as tarefas de saudação descritas no artigo Olá intitulado [ingressar em um domínio gerenciado do Windows máquina virtual tooa](active-directory-ds-admin-guide-join-windows-vm.md).


## <a name="task-3---install-and-register-hello-azure-ad-application-proxy-connector"></a>Tarefa 3: instalar e registrar Olá conector de Proxy de aplicativo do AD do Azure
Anteriormente, você pode provisionar uma máquina de virtual do Windows Server e ingressados no domínio gerenciado toohello. Nesta tarefa, você instalará o conector de Proxy de aplicativo do Azure AD Olá nesta máquina virtual.

1. Copie Olá conector instalação pacote toohello VM no qual você instala o conector de Proxy de aplicativo Web do AD do Azure hello.

2. Executar **AADApplicationProxyConnectorInstaller.exe** na máquina virtual de saudação. Aceite os termos de licença de software de saudação.

    ![Aceite os termos de instalação](./media/app-proxy/app-proxy-install-connector-terms.png)
3. Durante a instalação, você está tooregister solicitadas Olá conector com hello Proxy de aplicativo do seu diretório do AD do Azure.
    * Forneça suas **credenciais de administrador global do Azure AD**. Seu locatário de administrador global pode ser diferente das suas credenciais do Microsoft Azure.
    * Olá administrador conta usada tooregister Olá conector deve pertencer toohello mesmo diretório onde você habilitou o serviço de Proxy de aplicativo hello. Por exemplo, se o domínio de locatário Olá for contoso.com, Olá administrador deve ser admin@contoso.com ou qualquer outro alias válido nesse domínio.
    * Se a configuração de segurança aprimorada do IE é ativada para o servidor de saudação onde você está instalando o conector hello, tela de saudação do registro pode estar bloqueada. acesso de tooallow, siga as instruções de saudação na mensagem de erro de saudação. Certifique-se de que a Segurança Melhorada do Internet Explorer está desativada.
    * Se o registro do conector não for bem-sucedido, confira [Solucionar problemas de Proxy de Aplicativo](../active-directory/active-directory-application-proxy-troubleshoot.md).

    ![Conector instalado](./media/app-proxy/app-proxy-connector-installed.png)
4. conector de saudação tooensure funciona corretamente, Olá execução do Azure AD aplicativo Proxy do conector de solução de problemas. Você deve ver um relatório com êxito após a solução de problemas de saudação em execução.

    ![Êxito da solução de problemas](./media/app-proxy/app-proxy-connector-troubleshooter.png)
5. Você deve ver o conector Olá recém-instalados listado na página de proxy de aplicativo hello no seu diretório do AD do Azure.

    ![](./media/app-proxy/app-proxy-connector-page.png)

> [!NOTE]
> Você pode escolher conectores tooinstall em vários servidores tooguarantee alta disponibilidade para a autenticação de aplicativos publicados pelo Olá Proxy de aplicativo do Azure AD. Execute as mesmas etapas listadas acima tooinstall conector de saudação em outros servidores tooyour ingressado no domínio do gerenciado de saudação.
>
>

## <a name="next-steps"></a>Próximas etapas
Você configurar Olá Proxy de aplicativo do Azure AD e integrado a seu domínio gerenciado do serviços de domínio do AD do Azure.

* **Migrar máquinas virtuais aplicativos tooAzure:** é possível comparação de precisão e shift seus aplicativos de locais servidores tooAzure máquinas virtuais tooyour ingressado no domínio gerenciado. Isso ajuda a eliminar os custos de infraestrutura de saudação da execução de servidores no local.

* **Publicar aplicativos usando o Proxy de aplicativo do Azure AD:** publicar aplicativos em execução em suas máquinas virtuais do Azure usando Olá Proxy de aplicativo do Azure AD. Para saber mais, confira [publicar aplicativos usando o Proxy de Aplicativo do Azure AD](../active-directory/application-proxy-publish-azure-portal.md)


## <a name="deployment-note---publish-iwa-integrated-windows-authentication-applications-using-azure-ad-application-proxy"></a>Nota sobre a implantação: publique aplicativos IWA (Autenticação Integrada do Windows) usando o Proxy de Aplicativo do Azure AD
Permitir que os aplicativos tooyour de logon único usando a autenticação do Windows integrada (IWA) concedendo permissão de conectores de Proxy de aplicativo tooimpersonate usuários e enviar e receber tokens em seu nome. Configure a delegação restringido de kerberos (KCD) para Olá conector toogrant Olá necessárias permissões tooaccess recursos no domínio gerenciado hello. Use o mecanismo de KCD de baseada em recursos de saudação em domínios gerenciados para aumentar a segurança.


### <a name="enable-resource-based-kerberos-constrained-delegation-for-hello-azure-ad-application-proxy-connector"></a>Habilitar a delegação restringido de kerberos com base em recursos para o conector de Proxy de aplicativo de saudação do AD do Azure
conector de Proxy de aplicativo do Azure Olá deve ser configurada para delegação restringido de kerberos (KCD), para que ele possa representar usuários no domínio gerenciado hello. Em um domínio gerenciado do Azure AD Domain Services, você não tem privilégios de administrador de domínio. Portanto, **não é possível configurar um KCD tradicional no nível da conta em um domínio gerenciado**.

Use o KCD baseado em recursos conforme descrito neste [artigo](active-directory-ds-enable-kcd.md).

> [!NOTE]
> Você precisa toobe membro Olá ' AAD DC' do grupo de administradores, Olá tooadminister gerenciadas usando cmdlets do PowerShell do AD de domínio.
>
>

Use configurações de saudação do hello PowerShell Get-ADComputer cmdlet tooretrieve para computador Olá no qual Olá Proxy de aplicativo do Azure AD connector está instalado.
```
$ConnectorComputerAccount = Get-ADComputer -Identity contoso100-proxy.contoso100.com
```

Depois disso, use Olá Set-ADComputer cmdlet tooset o KCD com base em recursos de servidor de saudação do recurso.
```
Set-ADComputer contoso100-resource.contoso100.com -PrincipalsAllowedToDelegateToAccount $ConnectorComputerAccount
```

Se você tiver implantado vários conectores de Proxy de aplicativo em seu domínio gerenciado, você precisa tooconfigure KCD com base em recursos para cada instância conector.


## <a name="related-content"></a>Conteúdo relacionado
* [Serviços de Domínio do Azure AD - guia de Introdução](active-directory-ds-getting-started.md)
* [Configurar a Delegação Restrita de Kerberos em um domínio gerenciado](active-directory-ds-enable-kcd.md)
* [Visão geral da Delegação Restrita de Kerberos](https://technet.microsoft.com/library/jj553400.aspx)
