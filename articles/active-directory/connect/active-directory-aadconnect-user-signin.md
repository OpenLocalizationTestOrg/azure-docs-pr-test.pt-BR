---
title: "Azure AD Connect: Conexão do usuário | Microsoft Docs"
description: "Conexão do usuário do Azure AD Connect para configurações personalizadas."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 547b118e-7282-4c7f-be87-c035561001df
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 7848b419f3855b25cfa074a46779d258bd534bae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-user-sign-in-options"></a>Opções de entrada de usuário do Azure AD Connect
Conexão do Active Directory (AD do Azure) do Azure permite que seu toosign usuários na nuvem tooboth e recursos locais usando Olá mesmas senhas. Este artigo descreve os conceitos principais para cada toohelp de modelo de identidade que escolha identidade Olá que você deseja toouse para entrar no tooAzure AD.

Se você já estiver familiarizado com o modelo de identidade do AD do Azure hello e deseja toolearn mais informações sobre um método específico, consulte o link apropriado hello:

* [Sincronização de senha](#password-synchronization) com [SSO (logon único)](active-directory-aadconnect-sso.md)
* [Autenticação de passagem](active-directory-aadconnect-pass-through-authentication.md)
* [SSO federado (com o AD FS [Serviços de Federação do Active Directory])](#federation-that-uses-a-new-or-existing-farm-with-ad-fs-in-windows-server-2012-r2)

## <a name="choosing-hello-user-sign-in-method-for-your-organization"></a>Escolhendo Olá usuário método de entrada para a sua organização
Para a maioria das organizações que quiser apenas tooenable usuário entrar tooOffice 365 aplicativos SaaS e outros recursos de baseado no AD do Azure, recomendamos a opção de sincronização de senha saudação padrão. Algumas organizações, no entanto, tem um motivo específico que não são capaz toouse essa opção. Elas podem escolher uma opção de conexão federada, como o AD FS ou a autenticação de passagem. Você pode usar o hello toohelp tabela você fazer a escolha certa Olá a seguir.

Preciso muito| PS com SSO| PA com SSO| AD FS |
 --- | --- | --- | --- |
Sincronize o novo usuário, contato e contas de grupo em nuvem do local do Active Directory toohello automaticamente.|x|x|x|
Configurar meu locatário para cenários híbridos do Office 365.|x|x|x|
Habilite meus usuários toosign em e serviços de nuvem de acesso usando sua senha local.|x|x|x|
Implementar o logon único usando credenciais corporativas.|x|x|x|
Certifique-se de que nenhuma senha é armazenada na nuvem hello.||x*|x|
Habilitar soluções de autenticação multifator locais.|||x|

*Por meio de um conector leve.

>[!NOTE]
> A autenticação de passagem atualmente tem algumas limitações com clientes avançados. Consulte [Autenticação de passagem](active-directory-aadconnect-pass-through-authentication.md) para obter mais detalhes.

### <a name="password-synchronization"></a>Sincronização de senha
Com a sincronização de senha, hashes de senhas de usuário são sincronizados do local do Active Directory tooAzure AD. Quando as senhas são alteradas ou redefinir local, o hello novas senhas são sincronizado tooAzure AD imediatamente para que os usuários podem sempre usar Olá mesmo senha para recursos de nuvem e local. senhas de saudação nunca são enviadas tooAzure AD ou armazenadas no AD do Azure em texto não criptografado. Você pode usar a sincronização de senha junto com a senha tooenable de write-back de autoatendimento redefinição de senha no AD do Azure.

Além disso, você pode habilitar [SSO](active-directory-aadconnect-sso.md) para usuários em computadores que ingressaram no domínio que estão na rede corporativa hello. Com o logon único, ativado tooenter de necessidade somente usuários toohelp um nome de usuário que eles acessarem com segurança os recursos de nuvem.

![Sincronização de senha](./media/active-directory-aadconnect-user-signin/passwordhash.png)

Para obter mais informações, consulte Olá [a sincronização de senha](active-directory-aadconnectsync-implement-password-synchronization.md) artigo.

### <a name="pass-through-authentication"></a>Autenticação de passagem
Com a autenticação de passagem, Olá a senha de usuário é validado controlador do hello local do Active Directory. senha de saudação não precisa toobe presente no AD do Azure de qualquer forma. Isso permite políticas locais, como restrições de horário de logon toobe avaliada durante serviços toocloud de autenticação.

Autenticação de passagem usa um agente simple em um computador ingressado no domínio do Windows Server 2012 R2 no ambiente de local de saudação. Esse agente escuta as solicitações de validação de senha. Ele não requer qualquer toohello de abrir portas de entrada toobe da Internet.

Além disso, você também pode habilitar logon único para usuários em computadores que ingressaram no domínio que estão na rede corporativa hello. Com o logon único, ativado tooenter de necessidade somente usuários toohelp um nome de usuário que eles acessarem com segurança os recursos de nuvem.
![Autenticação de passagem](./media/active-directory-aadconnect-user-signin/pta.png)

Para obter mais informações, confira:
- [Autenticação de passagem](active-directory-aadconnect-pass-through-authentication.md)
- [Logon Único](active-directory-aadconnect-sso.md)

### <a name="federation-that-uses-a-new-or-existing-farm-with-ad-fs-in-windows-server-2012-r2"></a>Federação que usa um farm novo ou existente com o AD FS no Windows Server 2012 R2
Com a entrada federada, seus usuários possam entrar em tooAzure serviços baseados em AD com suas senhas no local. Enquanto eles estão na rede corporativa hello, eles não ainda tem tooenter suas senhas. Usando a opção de Federação Olá com o AD FS, você pode implantar um farm novo ou existente com o AD FS no Windows Server 2012 R2. Se você escolher toospecify um farm existente, do Azure AD Connect configura Olá confiança entre seu farm e o AD do Azure para que os usuários podem entrar.

<center>![Federação com o AD FS no Windows Server 2012 R2](./media/active-directory-aadconnect-user-signin/federatedsignin.png)</center>

#### <a name="deploy-federation-with-ad-fs-in-windows-server-2012-r2"></a>Implantar a federação com o AD FS no Windows Server 2012 R2

Se você estiver implantando um novo farm, será necessário:

* Um servidor do Windows Server 2012 R2 para o servidor de Federação hello.
* Um servidor do Windows Server 2012 R2 para Olá Proxy de aplicativo Web.
* Um arquivo .pfx com um certificado SSL para o nome do serviço de federação pretendido. Por exemplo: fs.contoso.com.

Se você estiver implantando um novo farm ou usando um farm existente, será necessário:

* Credenciais de administrador local nos servidores de federação.
* Credenciais de administrador local em qualquer servidor de grupo de trabalho (não ingressados no domínio) que você pretende toodeploy Olá função Proxy de aplicativo Web em.
* máquina de saudação executar Olá assistente em toobe tooconnect capaz de tooany outras máquinas que você deseja tooinstall AD FS ou o Proxy de aplicativo Web no usando o gerenciamento remoto do Windows.

Para obter mais informações, consulte [Configurando o SSO com o AD FS](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs).

#### <a name="sign-in-by-using-an-earlier-version-of-ad-fs-or-a-third-party-solution"></a>Conectar usando uma versão anterior do AD FS ou uma solução de terceiros
Se você já tiver configurado a nuvem entrar usando uma versão anterior do AD FS (como o AD FS 2.0) ou um provedor de federação de terceiros, você pode escolher tooskip entrar na configuração do usuário por meio do Azure AD Connect. Isso permite sincronização mais recente do tooget hello e outros recursos do Azure AD Connect enquanto estiver usando a solução existente para entrar.

Para obter mais informações, consulte Olá [lista de compatibilidade de federação de terceiros do AD do Azure](active-directory-aadconnect-federation-compatibility.md).


## <a name="user-sign-in-and-user-principal-name"></a>Conexão do usuário e nome UPN
### <a name="understanding-user-principal-name"></a>Entendendo o nome UPN
No Active Directory, sufixo de UPN (UPN) saudação padrão é o nome DNS de saudação do domínio Olá onde a conta de usuário de saudação foi criada. Na maioria dos casos, isso é o nome de domínio de saudação que é registrado como domínio de empresa Olá em Olá da Internet. No entanto, é possível adicionar mais sufixos UPN usando Domínios e Relações de Confiança do Active Directory.

Olá UPN do usuário Olá tem o formato de saudação username@domain. Por exemplo, para um domínio do Active Directory denominado "contoso.com", um usuário chamado João pode ter Olá UPN "john@contoso.com". Olá UPN do usuário Olá baseia-se na RFC 822. Embora hello UPN e compartilhamento de email hello mesmo formato, valor Olá Olá UPN para um usuário pode ou não ser Olá mesmo como o endereço de email de saudação do usuário hello.

### <a name="user-principal-name-in-azure-ad"></a>Nome UPN no Azure AD
Assistente de conexão do AD do Azure Olá usa o atributo userPrincipalName de saudação ou permite que você especifique Olá toobe de atributo (em uma instalação personalizada) usado do local como nome de usuário principal Olá no AD do Azure. Este é o valor de saudação que é usada para entrar no tooAzure AD. Se Olá valor do atributo de userPrincipalName Olá não corresponde tooa verificado domínio no AD do Azure, em seguida, o AD do Azure substitui-lo com um padrão. c o m valor.

Cada diretório no Active Directory do Azure vem com um nome de domínio interno com hello formato contoso.onmicrosoft.com, que permite que você começar a usar o Azure ou outros serviços da Microsoft. Você pode melhorar e simplificar a experiência de entrada hello usando domínios personalizados. Para obter informações sobre nomes de domínio personalizado no AD do Azure e como tooverify um domínio, consulte [adicionar seu nome de domínio personalizado tooAzure do Active Directory](../add-custom-domain.md#add-your-custom-domain).

## <a name="azure-ad-sign-in-configuration"></a>Configuração de entrada do Azure AD
### <a name="azure-ad-sign-in-configuration-with-azure-ad-connect"></a>Configuração de entrada do Azure AD entrar com o Azure AD Connect
experiência de entrada Hello AD do Azure depende se o AD do Azure pode corresponder a saudação sufixo UPN de um usuário que está sendo sincronizado tooone de domínios personalizados de saudação que são verificadas no diretório do AD do Azure hello. Conexão do AD do Azure fornece ajuda ao configurar o AD do Azure configurações de entrada, para que Olá entrar experiência do usuário na nuvem Olá é experiência de local toohello semelhante.

Listas do Azure AD Connect Olá sufixos UPN que são definidos para Olá toomatch de domínios e tentativas com um domínio personalizado no AD do Azure. Em seguida, ele ajuda com uma ação de apropriada de saudação que precisa toobe realizada.
página de entrada Hello AD do Azure lista sufixos UPN Olá definidos para o Active Directory no local e exibe o status de saudação correspondente em cada sufixo. valores de status Olá podem ser uma das seguintes hello:

| Estado | Descrição | Ação necessária |
|:--- |:--- |:--- |
| Verificado |O Azure AD Connect encontrou uma correspondência de domínio verificado no Azure AD. Todos os usuários deste domínio podem se conectar usando suas credenciais locais. |Nenhuma ação é necessária. |
| Não verificado |O Azure AD Connect encontrou uma correspondência de domínio personalizado, mas ele não é verificado. sufixo UPN Olá usuários Olá deste domínio será alterado toohello padrão. o sufixo onmicrosoft.com após a sincronização se Olá domínio não é verificado. | [Verifique se o domínio personalizado Olá no AD do Azure.](../add-custom-domain.md#verify-the-domain-name-with-azure-ad) |
| Não adicionado |Conexão do AD do Azure não encontrou um domínio personalizado sufixo UPN correspondia toohello. sufixo UPN Olá usuários Olá deste domínio será alterado toohello padrão. c o m sufixo se domínio Olá não é adicionado e verificado no Azure. | [Adicionar e verificar um domínio personalizado que corresponde a toohello sufixo UPN.](../add-custom-domain.md) |

página de entrada Hello AD do Azure lista sufixos UPN de saudação que são definidos para o Active Directory local e Olá correspondente domínio personalizado no AD do Azure com o status de verificação atual hello. Em uma instalação personalizada, agora você pode selecionar o atributo Olá Olá UPN no hello **entrar do AD do Azure** página.

![Página de entrada do Azure AD](./media/active-directory-aadconnect-user-signin/custom_azure_sign_in.png)

Você pode clicar em Olá atualização toore busca hello mais recente status de botão de domínios personalizados de saudação do AD do Azure.

### <a name="selecting-hello-attribute-for-hello-user-principal-name-in-azure-ad"></a>Selecionar atributo Olá Olá UPN no AD do Azure
Olá atributo userPrincipalName é atributo Olá usados pelos usuários quando eles entrarem tooAzure AD e Office 365. Você deve verificar domínios hello (também conhecido como sufixos UPN) que são usados no AD do Azure antes de saudação usuários estão sincronizados.

É altamente recomendável que você mantenha o saudação padrão atributo userPrincipalName. Se esse atributo for nonroutable e não pode ser verificado, e em seguida, é possível tooselect outro atributo (por exemplo, email) como Olá que mantém Olá ID de entrada. Isso é conhecido como Olá ID alternativo Olá valor do atributo ID alternativo deve seguir Olá RFC 822 padrão. Você pode usar uma ID alternativa com SSO de senha e federação SSO como solução de entrada hello.

> [!NOTE]
> O uso de uma ID Alternativa não é compatível com todas as cargas de trabalho do Office 365. Para obter mais informações, consulte [Configurando uma ID de logon alternativa](https://technet.microsoft.com/library/dn659436.aspx).
>
>

#### <a name="different-custom-domain-states-and-their-effect-on-hello-azure-sign-in-experience"></a>Estados de outro domínio personalizado e seu efeito na experiência de saudação entrada do Azure
É muito importante toounderstand Olá relação entre os estados de domínio personalizado de saudação em seu diretório do AD do Azure e hello, sufixos UPN que são definidos no local. Vamos percorrer Olá diferentes possíveis Azure entrar experiências quando você estiver configurando a sincronização com o uso do Azure AD Connect.

Para Olá informações a seguir, vamos supor que estamos preocupados com hello UPN sufixo contoso.com, que é usado no diretório local de saudação como parte do UPN – por exemplo user@contoso.com.

###### <a name="express-settingspassword-synchronization"></a>Configurações expressas/sincronização de senha
| Estado | Efeito sobre a experiência de entrada do usuário do Azure |
|:---:|:--- |
| Não adicionado |Nesse caso, nenhum domínio personalizado para contoso.com foi adicionado no diretório do AD do Azure hello. Os usuários que têm o UPN local com o sufixo Olá @contoso.com não será capaz de toouse seu toosign UPN local em tooAzure. Em vez disso, eles serão necessário toouse um UPN novo que forneceu toothem pelo AD do Azure adicionando o sufixo Olá Olá padrão diretório AD do Azure. Por exemplo, se você estiver sincronizando usuários toohello do Azure AD directory azurecontoso.onmicrosoft.com, em seguida, Olá usuário local user@contoso.com terá um UPN de user@azurecontoso.onmicrosoft.com. |
| Não verificado |Nesse caso, temos contoso.com um domínio personalizado que é adicionado no diretório de saudação do AD do Azure. No entanto, ele ainda não foi verificado. Se você prosseguir com a sincronizar os usuários sem verificar o domínio Olá, Olá os usuários receberão um UPN novo pelo AD do Azure, assim como em hello "Não adicionado" cenário. |
| Verificado |Nesse caso, temos um domínio personalizado contoso.com já adicionado e verificado no AD do Azure para Olá sufixo UPN. Os usuários serão capaz toouse local nome principal do usuário, por exemplo user@contoso.com, toosign em tooAzure depois que eles são sincronizados tooAzure AD. |

###### <a name="ad-fs-federation"></a>Federação do AD FS
Você não pode criar uma federação padrão hello. c o m domínio no AD do Azure ou um domínio personalizado não verificado no AD do Azure. Quando você estiver executando o Assistente para conectar de saudação do AD do Azure, se você selecionar um domínio não verificado toocreate uma federação com, em seguida, o Azure AD Connect solicita com hello necessário registra toobe criado onde o DNS está hospedado para o domínio de saudação. Para obter mais informações, consulte [verificar o domínio Olá AD do Azure selecionado para federação](active-directory-aadconnect-get-started-custom.md#verify-the-azure-ad-domain-selected-for-federation).

Se você selecionar a opção de entrada do usuário de saudação **federação com o AD FS**, em seguida, você deve ter uma toocontinue de domínio personalizado, criando uma federação no AD do Azure. Para nossa discussão, isso significa que podemos deve ter um domínio personalizado de contoso.com adicionado no diretório de saudação do AD do Azure.

| Estado | Efeito na experiência de entrada do usuário do Azure Olá |
|:---:|:--- |
| Não adicionado |Nesse caso, o Azure AD Connect não encontrou um domínio personalizado correspondente para Olá contoso.com de sufixo UPN no diretório do AD do Azure hello. Você precisa tooadd contoso.com um domínio personalizado se você precisar de usuários toosign no usando o AD FS com seu UPN local (como user@contoso.com). |
| Não verificado |Nesse caso, o Azure AD Connect solicitará os detalhes adequados sobre como é possível verificar o domínio em um estágio posterior. |
| Verificado |Nesse caso, você pode prosseguir com a configuração de saudação sem nenhuma ação adicional. |

## <a name="changing-hello-user-sign-in-method"></a>Alterar o método de entrada do usuário de saudação
Você pode alterar o método de entrada do usuário de saudação de federação, a sincronização de senha ou autenticação de passagem usando Olá as tarefas que estão disponíveis no Azure AD Connect após a configuração inicial de saudação do Azure AD Connect com o Assistente de saudação. Execute novamente o Assistente de conexão do AD do Azure Olá, e você verá uma lista de tarefas que você pode executar. Selecione **Alterar usuário entrar** da lista de saudação de tarefas.

![Alterar a entrada do usuário](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

Na página seguinte do hello, você será solicitado a tooprovide credenciais de saudação do AD do Azure.

![Conecte-se tooAzure AD](./media/active-directory-aadconnect-user-signin/changeusersignin2.png)

Em Olá **usuário entrar** , selecione Olá desejado usuário entrar.

![Conecte-se tooAzure AD](./media/active-directory-aadconnect-user-signin/changeusersignin2a.png)

> [!NOTE]
> Se você estiver apenas criando uma sincronização de toopassword switch temporário, em seguida, selecione Olá **não converte as contas de usuário** caixa de seleção. Não marcar a opção de saudação converterá toofederated cada usuário, e pode levar várias horas.
>
>

## <a name="next-steps"></a>Próximas etapas
- Saiba mais sobre [como integrar suas identidades locais ao Azure Active Directory](active-directory-aadconnect.md).
- Saiba mais sobre os [conceitos de design do Azure AD Connect](active-directory-aadconnect-design-concepts.md).
