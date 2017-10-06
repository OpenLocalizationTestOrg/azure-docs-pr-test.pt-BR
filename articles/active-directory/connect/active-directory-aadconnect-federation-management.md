---
title: "aaaActive Directory Federation Services personalização com o Azure AD Connect e gerenciamento | Microsoft Docs"
description: "Gerenciamento do AD FS com o Azure AD Connect e personalização da experiência de entrada do AD FS do usuário com o Azure AD e o PowerShell."
keywords: "AD FS, ADFS, gerenciamento do AD FS, AAD Connect, Conectar, entrada, personalização do AD FS, reparar confiança, O365, federação, terceira parte confiável"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 2593b6c6-dc3f-46ef-8e02-a8e2dc4e9fb9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 361a2bfd6d7a6993dbe773d6ea039ad1afc6346a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-and-customize-active-directory-federation-services-by-using-azure-ad-connect"></a>Gerenciar e personalizar os Serviços de Federação do Active Directory usando o Azure AD Connect
Este artigo descreve como toomanage e personalizar os serviços de Federação do Active Directory (AD FS) usando o Connect do Azure Active Directory (AD do Azure). Ele também inclui outras tarefas comuns do AD FS que talvez você precise toodo para concluir a configuração de um farm do AD FS.

| Tópico | O que ele abrange |
|:--- |:--- |
| **Gerenciar o AD FS** | |
| [Reparar confiança Olá](#repairthetrust) |Como a federação de saudação toorepair confiança com o Office 365. |
| [Federar ao Azure AD usando uma ID de logon alternativa ](#alternateid) | Configurar a federação usando uma ID de logon alternativa  |
| [Adicionar um servidor do AD FS](#addadfsserver) |Como tooexpand um AD FS do farm com um servidor do AD FS adicional. |
| [Adicionar um Servidor Proxy de Aplicativo Web do AD FS](#addwapserver) |Como tooexpand um AD FS do farm com um servidor de Proxy de aplicativo da Web (WAP) adicional. |
| [Adicionar um domínio federado](#addfeddomain) |Como tooadd um domínio federado. |
| [Atualizar o certificado SSL de saudação](active-directory-aadconnectfed-ssl-update.md)| Como tooupdate Olá SSL de certificado para um farm do AD FS. |
| **Personalizar o AD FS** | |
| [Adicionar uma ilustração ou um logotipo da empresa personalizado](#customlogo) |Como toocustomize um AD FS sign-in de página com um logotipo da empresa e a ilustração. |
| [Adicionar uma descrição de entrada](#addsignindescription) |Como tooadd um entrada na página de descrição. |
| [Modificar regras de declaração do AD FS](#modclaims) |Como toomodify do AD FS declarações para vários cenários de Federação. |

## <a name="manage-ad-fs"></a>Gerenciar o AD FS
Você pode executar várias tarefas de AD FS relacionados no Azure AD Connect com mínima intervenção do usuário usando o Assistente do hello Azure AD Connect. Depois de instalar o Azure AD Connect pelo Assistente de saudação em execução, você pode executar o Assistente de saudação novamente tooperform tarefas adicionais.

## Reparar confiança Olá<a name=repairthetrust></a>
Você pode usar a integridade atual do Azure AD Connect toocheck Olá de saudação do AD FS e a confiança do AD do Azure e tomar as ações apropriadas toorepair Olá confiança. Siga estas etapas toorepair do Azure AD e o AD FS confiam.

1. Selecione **AAD reparo e a relação de confiança do ADFS** de lista de saudação de tarefas adicionais.
   ![Reparar a relação de confiança do AAD e do ADFS](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)

2. Em Olá **conectar tooAzure AD** , forneça suas credenciais de administrador global do AD do Azure e, em **próximo**.
   ![Conecte-se tooAzure AD](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)

3. Em Olá **credenciais de acesso remoto** insira credenciais Olá para o administrador de domínio hello.

   ![Credenciais de acesso remoto](media/active-directory-aadconnect-federation-management/RepairADTrust3.PNG)

    Depois que você clicar em **Avançar**, o Azure AD Connect verificará a integridade do certificado e mostrará eventuais problemas.

    ![Estado de certificados](media/active-directory-aadconnect-federation-management/RepairADTrust4.PNG)

    Olá **tooconfigure pronto** página Olá mostra a lista de ações que serão executadas toorepair confiança de saudação.

    ![Tooconfigure pronto](media/active-directory-aadconnect-federation-management/RepairADTrust5.PNG)

4. Clique em **instalar** toorepair confiança de saudação.

> [!NOTE]
> O Azure AD Connect só pode reparar ou agir em relação a certificados autoassinados. O Azure AD Connect não pode reparar certificados de terceiros.

## Federar ao Azure AD usando uma AlternateID <a name=alternateid></a>
É recomendável que Olá Principal do usuário Name(UPN) local e nuvem Olá Nome Principal do usuário são mantidos Olá mesmo. Se Olá UPN local usa um domínio não roteáveis (ex. Contoso. local) ou não pode ser alterado devido a dependências do aplicativo toolocal, é recomendável definir a ID de logon alternativo. ID de logon alternativo permite que você tooconfigure uma experiência de entrada no qual os usuários podem entrar com um atributo diferente de seu UPN, como email. opção de saudação para nome Principal do usuário no atributo do Azure AD Connect padrões toohello userPrincipalName no Active Directory. Se você escolher qualquer outro atributo para o nome UPN e estiver federando com o uso do AD FS, o Azure AD Connect configurará o AD FS para a ID de logon alternativa. Um exemplo de escolha de um atributo diferente para o nome UPN é mostrado abaixo:

![Seleção de atributo de ID alternativa](media/active-directory-aadconnect-federation-management/attributeselection.png)

A configuração da ID de logon alternativa do AD FS consiste em duas etapas principais:
1. **Configurar conjunto de declarações de emissão certo Olá**: regras de declaração de emissão de saudação na terceira parte confiável Olá AD do Azure de confiança são modificadas toouse Olá selecionado UserPrincipalName atributo como Olá ID alternativa do usuário hello.
2. **Habilitar identificação de logon alternativo na configuração de saudação do AD FS**: configuração do hello AD FS é atualizada para que o AD FS pode pesquisar usuários Olá florestas apropriado usando a ID alternativa Olá Há suporte para essa configuração no AD FS no Windows Server 2012 R2 (com KB2919355) ou posterior. Se Olá AD FS servidores 2012 R2, as verificações do Azure AD Connect presença Olá Olá necessário KB. Se hello KB não for detectado, um aviso aparecerá após a conclusão da configuração, conforme mostrado abaixo:

    ![Aviso de ausência de KB no 2012R2](media/active-directory-aadconnect-federation-management/kbwarning.png)

    configuração de saudação toorectify no caso de KB ausente, instale Olá necessário [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) e repare Olá confiança usando [reparar AAD e confiança do AD FS](#repairthetrust).

> [!NOTE]
> Para obter mais informações sobre toomanually alternateID e etapas de configurar, ler [Configurando ID de logon alternativo](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)

## Adicionar um servidor do AD FS <a name=addadfsserver></a>

> [!NOTE]
> servidor tooadd um AD FS, do Azure AD Connect exige o certificado de PFX hello. Portanto, você pode executar esta operação somente se você configurou o farm do hello AD FS usando o Azure AD Connect.

1. Selecione **Implantar um Servidor de Federação adicional** e clique em **Avançar**.

   ![Servidor de federação adicional](media/active-directory-aadconnect-federation-management/AddNewADFSServer1.PNG)

2. Em Olá **conectar tooAzure AD** , insira suas credenciais de administrador global do AD do Azure e, em **próximo**.

   ![Conecte-se tooAzure AD](media/active-directory-aadconnect-federation-management/AddNewADFSServer2.PNG)

3. Forneça credenciais de administrador de domínio de saudação.

   ![Credenciais de administrador de domínio](media/active-directory-aadconnect-federation-management/AddNewADFSServer3.PNG)

4. Azure AD Connect solicita uma senha de saudação do arquivo PFX Olá que você forneceu ao configurar seu novo farm do AD FS com o Azure AD Connect. Clique em **digitar senha** tooprovide senha Olá arquivo PFX de saudação.

   ![Senha de certificado](media/active-directory-aadconnect-federation-management/AddNewADFSServer4.PNG)

    ![Especificar certificado SSL](media/active-directory-aadconnect-federation-management/AddNewADFSServer5.PNG)

5. Em Olá **servidores do AD FS** , insira o nome do servidor de saudação ou toobe de endereço IP adicionado farm do toohello AD FS.

   ![Servidores do AD FS](media/active-directory-aadconnect-federation-management/AddNewADFSServer6.PNG)

6. Clique em **próximo**e percorrer Olá final **configurar** página. Depois que o Azure AD Connect concluiu a adição de farm do hello servidores toohello AD FS, você terá conectividade de Olá Olá opção tooverify.

   ![Tooconfigure pronto](media/active-directory-aadconnect-federation-management/AddNewADFSServer7.PNG)

    ![Instalação concluída](media/active-directory-aadconnect-federation-management/AddNewADFSServer8.PNG)

## Adicionar um servidor WAP do AD FS <a name=addwapserver></a>

> [!NOTE]
> tooadd um servidor WAP, Azure AD Connect exige o certificado de PFX hello. Portanto, você pode executar esta operação somente se você configurou o farm do hello AD FS usando o Azure AD Connect.

1. Selecione **implantar o Proxy de aplicativo Web** da lista de saudação de tarefas disponíveis.

   ![Implantar o proxy de aplicativo Web](media/active-directory-aadconnect-federation-management/WapServer1.PNG)

2. Forneça credenciais de administrador global do Azure hello.

   ![Conecte-se tooAzure AD](media/active-directory-aadconnect-federation-management/wapserver2.PNG)

3. Em Olá **certificado SSL especificar** , forneça a senha de saudação para arquivo PFX Olá fornecido quando você configurou o farm do hello AD FS com o Azure AD Connect.
   ![Senha de certificado](media/active-directory-aadconnect-federation-management/WapServer3.PNG)

    ![Especificar certificado SSL](media/active-directory-aadconnect-federation-management/WapServer4.PNG)

4. Adicione Olá server toobe adicionado como um servidor WAP. Como servidor WAP de saudação não pode ser toohello ingressado no domínio, o Assistente de saudação solicita servidor toohello de credenciais administrativas que está sendo adicionado.

   ![Credenciais administrativas de servidor](media/active-directory-aadconnect-federation-management/WapServer5.PNG)

5. Em Olá **credenciais de relação de confiança de Proxy** página, forneça proxy de saudação tooconfigure credenciais administrativas de confiança e acesso saudação do servidor primária no farm de saudação do AD FS.

   ![Credenciais de confiança de proxy](media/active-directory-aadconnect-federation-management/WapServer6.PNG)

6. Em Olá **tooconfigure pronto** página, o assistente Olá mostra lista Olá das ações que serão executadas.

   ![Tooconfigure pronto](media/active-directory-aadconnect-federation-management/WapServer7.PNG)

7. Clique em **instalar** toofinish configuração de saudação. Após a conclusão da configuração hello, fornece de assistente Olá Olá tooverify opção Olá servidores toohello de conectividade. Clique em **verificar** toocheck conectividade.

   ![Instalação concluída](media/active-directory-aadconnect-federation-management/WapServer8.PNG)

## Adicionar um domínio federado <a name=addfeddomain></a>

É fácil tooadd toobe um domínio federado com o Azure AD usando o Azure AD Connect. Azure AD Connect adiciona o domínio Olá para federação e modifica declaração Olá regras toocorrectly refletir emissor hello quando você tiver vários domínios federados com o Azure AD.

1. tooadd um domínio federado, tarefa Olá selecione **adicionar um domínio do AD do Azure**.

   ![Domínio do Azure AD adicional](media/active-directory-aadconnect-federation-management/AdditionalDomain1.PNG)

2. Na próxima página do Assistente de Olá Olá, forneça credenciais de administrador global de saudação do AD do Azure.

   ![Conecte-se tooAzure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain2.PNG)

3. Em Olá **credenciais de acesso remoto** , forneça credenciais de administrador de domínio hello.

   ![Credenciais de acesso remoto](media/active-directory-aadconnect-federation-management/additionaldomain3.PNG)

4. Na página seguinte do hello, o Assistente de saudação fornece uma lista de domínios do AD do Azure que você pode federar o seu diretório local com. Escolha domínio Olá Olá lista.

   ![Domínio do Azure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain4.PNG)

    Depois que você escolher o domínio Olá, Assistente Olá fornece informações adequadas sobre outras ações que Olá assistente será levar e Olá impacto da configuração de saudação. Em alguns casos, se você selecionar um domínio que ainda não é verificado no AD do Azure, Olá fornecerá informações toohelp verificar domínio hello. Consulte [adicionar seu nome de domínio personalizado tooAzure do Active Directory](../active-directory-add-domain.md) para obter mais detalhes.

5. Clique em **Avançar**. Olá **tooconfigure pronto** página mostra Olá lista de ações do Azure AD Connect realizada. Clique em **instalar** toofinish configuração de saudação.

   ![Tooconfigure pronto](media/active-directory-aadconnect-federation-management/AdditionalDomain5.PNG)

> [!NOTE]
> Os usuários de saudação adicionados domínio federado deve ser sincronizado antes que eles serão capazes de toologin tooAzure AD.

## <a name="ad-fs-customization"></a>Personalização do AD FS
Olá seções a seguir fornecem detalhes sobre algumas das tarefas comuns de saudação que você possa ter tooperform quando você personalizar sua página de entrada do AD FS.

## Adicionar uma ilustração ou um logotipo da empresa personalizado <a name=customlogo></a>
logotipo de saudação toochange da empresa de saudação que é exibido na Olá **entrar** página, use Olá seguindo a sintaxe e cmdlet do Windows PowerShell.

> [!NOTE]
> Olá recomendado dimensões para o logotipo de saudação são 260x35 96 dpi com um tamanho de arquivo maior do que 10 KB.

    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.PNG"}

> [!NOTE]
> Olá *TargetName* parâmetro é obrigatório. o tema padrão Olá liberado com o AD FS é denominado Default.

## Adicionar uma descrição de entrada <a name=addsignindescription></a>
tooadd um toohello de descrição de página de entrada **página de entrada**, use Olá seguindo a sintaxe e cmdlet do Windows PowerShell.

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in tooContoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>"

## Modificar regras de declaração do AD FS <a name=modclaims></a>
O AD FS oferece suporte a um idioma de declaração avançados que você pode usar regras de declaração toocreate personalizado. Para obter mais informações, consulte [Olá a função de linguagem da regra de declaração de saudação](https://technet.microsoft.com/library/dd807118.aspx).

Olá seções a seguir descrevem como você pode escrever regras personalizadas para alguns cenários que se relacionam tooAzure AD e Federação do AD FS.

### <a name="immutable-id-conditional-on-a-value-being-present-in-hello-attribute"></a>ID imutável condicional em um valor de estarem presentes no atributo Olá
Conexão do AD do Azure permite que você especifique um toobe atributo usado como uma âncora de origem quando objetos são sincronizados tooAzure AD. Se o valor de saudação no atributo personalizado Olá não está vazio, convém tooissue uma declaração de ID imutável.

Por exemplo, você pode selecionar **ms-ds-consistencyguid** como atributo de saudação de âncora de origem hello e problema **ImmutableID** como **ms-ds-consistencyguid** em maiusculas Olá o atributo tem um valor em relação a ela. Se não houver nenhum valor com atributo hello, emitir **objectGuid** como Olá ID imutável. Você pode construir o conjunto de saudação de regras de declaração personalizada conforme descrito em Olá seção a seguir.

**Regra 1: consultar atributos**

    c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]
    => add(store = "Active Directory", types = ("http://contoso.com/ws/2016/02/identity/claims/objectguid", "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"), query = "; objectGuid,ms-ds-consistencyguid;{0}", param = c.Value);

Essa regra, você está consultando valores hello **ms-ds-consistencyguid** e **objectGuid** para o usuário de saudação do Active Directory. Alterar nome de armazenamento apropriado de tooan Olá repositório de nome em sua implantação do AD FS. Também alterar Olá declarações tooa declarações adequadas tipo para a federação, conforme definido para **objectGuid** e **ms-ds-consistencyguid**.

Além disso, usando **adicionar** e não **problema**, evite a adição de um problema de saída para a entidade Olá e pode usar valores hello como valores intermediários. Você emitir Olá declaração em uma regra posteriormente depois de estabelecer quais toouse valor como Olá ID imutável.

**Regra 2: Verifique se o ms-ds-consistencyguid existe para o usuário Olá**

    NOT EXISTS([Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"])
    => add(Type = "urn:anandmsft:tmp/idflag", Value = "useguid");

Essa regra define um sinalizador temporário chamado **idflag** que está definido muito**useguid** se não houver nenhum **ms-ds-consistencyguid** preenchido para usuário hello. Olá lógica isso é o fato de saudação que o AD FS não permite declarações vazias. Portanto, quando você adicionar declarações http://contoso.com/ws/2016/02/identity/claims/objectguid e http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid na regra 1, você acabará com uma **msdsconsistencyguid** declaração somente se Olá valor é preenchido para usuário hello. Se ele não estiver populado, o AD FS verá que ele terá um valor vazio e o descartará imediatamente. Todos os objetos terão **objectGuid**. Portanto, essa declaração sempre estará presente após a Regra 1 ser executada.

**Regra 3: emitir ms-ds-consistencyguid como a ID imutável, se estiver presente**

    c:[Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c.Value);

Essa é uma verificação **Exist** implícita. Se valor Olá Olá declaração, em seguida, emita que como Olá imutável identificação. usa o exemplo anterior Olá Olá **nameidentifier** de declaração. Você terá toochange esse tipo de declaração adequado toohello de ID imutável Olá em seu ambiente.

**Regra 4: emitir o objectGuid como a ID imutável se ms-ds-consistencyGuid não estiver presente**

    c1:[Type == "urn:anandmsft:tmp/idflag", Value =~ "useguid"]
    && c2:[Type == "http://contoso.com/ws/2016/02/identity/claims/objectguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c2.Value);

Nessa regra, simplesmente você está verificando o sinalizador temporário Olá **idflag**. Você decide se tooissue Olá declaração com base em seu valor.

> [!NOTE]
> sequência de saudação dessas regras é importante.

### <a name="sso-with-a-subdomain-upn"></a>SSO com um subdomínio UPN
Você pode adicionar mais de um toobe domínio federado usando o Azure AD Connect, conforme descrito em [adicionar um novo domínio federado](active-directory-aadconnect-federation-management.md#addfeddomain). Você deve modificar Olá declaração de nome principal (UPN) do usuário para que hello emissor ID corresponde toohello domínio de raiz e não o subdomínio hello, porque o domínio de raiz federado Olá também aborda filhos hello.

Por padrão, Olá regra de declaração de emissor ID está definido como:

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

![Declaração de ID do emissor padrão](media/active-directory-aadconnect-federation-management/issuer_id_default.png)

regra de padrão de saudação simplesmente usa o sufixo UPN hello e usa-o na declaração de ID do emissor de saudação. Por exemplo, John é um usuário em sub.contoso.com e contoso.com é federado com o Azure AD. Insere John john@sub.contoso.com como Olá nome de usuário ao entrar tooAzure AD. regra de declaração de ID saudação padrão emissor no AD FS manipule em Olá maneira a seguir:

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(john@sub.contoso.com, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

**Valor de declaração:**  http://sub.contoso.com/adfs/services/trust/

toohave somente Olá domínio raiz emissor Olá valor de declaração, alterar Olá declaração regra toomatch Olá seguinte:

    c:[Type == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “^((.*)([.|@]))?(?<domain>[^.]*[.].*)$”, “http://${domain}/adfs/services/trust/“));

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre as [opções de entrada do usuário](active-directory-aadconnect-user-signin.md).
