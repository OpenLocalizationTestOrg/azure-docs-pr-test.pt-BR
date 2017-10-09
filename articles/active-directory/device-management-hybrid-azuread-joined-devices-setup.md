---
title: "dispositivos ingressados no aaaHow tooconfigure híbrida do Active Directory do Azure | Microsoft Docs"
description: "Saiba como tooconfigure híbrido do Azure Active Directory associados a dispositivos."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: f97ea436eca2833d8a9843acd19e5c633bc0fc07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-hybrid-azure-active-directory-joined-devices"></a>Como tooconfigure híbrido do Azure Active Directory associados a dispositivos

Com o gerenciamento de dispositivos no Azure AD (Azure Active Directory), você pode garantir que os usuários acessem recursos usando dispositivos que atendam aos padrões de segurança e conformidade. Para obter mais detalhes, consulte [gerenciamento de toodevice de Introdução no Active Directory do Azure](device-management-introduction.md).

Se você tiver um ambiente do Active Directory local e você desejar toojoin tooAzure seus dispositivos ingressados em domínio AD, você pode fazer isso configurando dispositivos do AD do Azure associado híbrida. Olá tópico fornece Olá relacionados etapas. 


## <a name="before-you-begin"></a>Antes de começar

Antes de começar a configurar dispositivos ingressados no híbrido do AD do Azure em seu ambiente, você deve estar familiarizado com cenários de saudação com suporte e as restrições de saudação.  

tooimprove legibilidade de saudação de descrições de hello, este tópico usa Olá termos a seguir: 

- **Dispositivos do Windows atuais** -este termo se refere a dispositivos que ingressaram no toodomain executando o Windows 10 ou Windows Server 2016.
- **Dispositivos de baixo nível do Windows** -este termo se refere a tooall **suporte** dispositivos Windows ingressados no domínio que estão executando o Windows 10 nem Windows Server 2016.  


### <a name="windows-current-devices"></a>Dispositivos atuais do Windows

- Para dispositivos que executam o sistema de operacional de desktop do Windows hello, é recomendável usar a atualização de aniversário do Windows 10 (versão 1607) ou posterior. 
- Olá registro atuais de dispositivos do Windows **é** suporte em ambientes de não-federado, como configurações de sincronização de hash de senha.  


### <a name="windows-down-level-devices"></a>Dispositivos de nível inferior do Windows

- Olá dispositivos de baixo nível do Windows a seguir têm suporte:
    - Windows 8.1
    - Windows 7
    - Windows Server 2012 R2
    - Windows Server 2012
    - Windows Server 2008 R2
- Olá registro de dispositivos de baixo nível do Windows **é** suporte em ambientes de não-federado por meio de perfeita Single Sign On [do Azure Active Directory perfeita Single Sign-On](https://aka.ms/hybrid/sso).
- Olá registro de dispositivos de baixo nível do Windows **não é** com suporte para dispositivos usando perfis de roaming. Se você depender da mobilidade de perfis ou configurações, use o Windows 10.



## <a name="prerequisites"></a>Pré-requisitos

Antes de iniciar a habilitação híbrido do Azure AD associado dispositivos na sua organização, você precisa toomake-se de que você está executando uma versão atualizada do AD do Azure se conectar.

Azure AD Connect:

- Mantém a associação de saudação entre a conta de computador de saudação de seu local no Active Directory (AD) e o objeto de dispositivo de saudação no AD do Azure. 
- Permite outros recursos relacionados ao dispositivo, como o Windows Hello for Business.



## <a name="configuration-steps"></a>Etapas da configuração

Você pode configurar dispositivos adicionados ao Azure AD híbrido para vários tipos de plataforma de dispositivo Windows. Este tópico inclui etapas Olá necessária para todos os cenários de configuração típica.  

Use Olá tabela tooget uma visão geral das etapas de saudação que são necessários para o cenário a seguir:  



| Etapas                                      | Sincronização de hash de senha e do Windows atual | Windows atual e a federação | Nível inferior do Windows |
| :--                                        | :-:                                    | :-:                            | :-:                |
| Etapa 1: configurar o ponto de conexão de serviço | ![Verificação][1]                            | ![Verificação][1]                    | ![Verificação][1]        |
| Etapa 2: configurar a emissão de declarações           |                                        | ![Verificação][1]                    | ![Verificação][1]        |
| Etapa 3: habilitar dispositivos não Windows 10      |                                        |                                | ![Verificação][1]        |
| Etapa 4: implantação de controle e distribuição     | ![Verificação][1]                            | ![Verificação][1]                    | ![Verificação][1]        |
| Etapa 5: Verificar os dispositivos adicionados          | ![Verificação][1]                            | ![Verificação][1]                    | ![Verificação][1]        |



## <a name="step-1-configure-service-connection-point"></a>Etapa 1: configurar o ponto de conexão de serviço

objeto de SCP (ponto) de conexão de serviço de saudação é usado por seus dispositivos durante saudação registro toodiscover informações de locatário do AD do Azure. Em seu local do Active Directory (AD), objeto Olá SCP para Olá híbrido do Azure AD associado dispositivos deve existir no hello nomenclatura contexto partição de configuração da floresta do computador hello. Há apenas um contexto de nomenclatura de configuração por floresta. Em uma configuração do Active Directory de várias floresta, o ponto de conexão de serviço Olá deve existir em todas as florestas de computadores que ingressaram no domínio.

Você pode usar o hello [ **Get-ADRootDSE** ](https://technet.microsoft.com/library/ee617246.aspx) cmdlet tooretrieve Olá contexto de nomenclatura configuração da floresta.  

Para uma floresta com o nome de domínio do Active Directory Olá *fabrikam.com*, Olá contexto de nomenclatura de configuração é:

`CN=Configuration,DC=fabrikam,DC=com`

Em sua floresta, o objeto Olá SCP para Olá o registro automático de dispositivos que ingressaram no domínio está localizado em:  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

Dependendo de como você implantou o Azure AD Connect, objeto de SCP Olá pode ter já foi configurado.
Você pode verificar a existência de saudação do objeto hello e recuperar valores de descoberta hello usando Olá script do Windows PowerShell a seguir: 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

Olá **$scp. Palavras-chave** saída mostra informações de locatário de saudação do AD do Azure, por exemplo:

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

Se o ponto de conexão de serviço Olá não existir, você pode criá-lo executando Olá `Initialize-ADSyncDomainJoinedComputerSync` cmdlet no seu servidor do Azure AD Connect. Credenciais de administrador corporativo é necessário toorun esse cmdlet.  
Olá cmdlet:

- Cria o ponto de conexão de serviço Olá na floresta do Active Directory de saudação do Azure AD Connect está conectado ao. 
- Exige que você Olá toospecify `AdConnectorAccount` parâmetro. Essa é a conta de saudação que é configurada como o Active Directory, conecte-se a conta de conector no AD do Azure. 


Olá, script a seguir mostra um exemplo para usar o cmdlet hello. Nesse script, `$aadAdminCred = Get-Credential` exige que você tootype um nome de usuário. Você precisa de nome de usuário Olá tooprovide no formato de nome principal (UPN) do usuário hello (`user@example.com`). 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

Olá `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:

- Usa o módulo do Active Directory PowerShell hello, que se baseia em serviços Web do Active Directory em execução em um controlador de domínio. Os Serviços Web do Active Directory têm suporte em controladores de domínio executando o Windows Server 2008 R2 e posterior.
- Só há suporte para Olá **MSOnline PowerShell versão do módulo 1.1.166.0**. toodownload neste módulo, use [link](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).   

Para controladores de domínio que executam o Windows Server 2008 ou versões anteriores, use script de saudação abaixo de ponto de conexão de serviço toocreate hello.

Em uma configuração de várias floresta, você deve usar o hello ponto de conexão de serviço do script toocreate Olá em cada floresta onde existem computadores a seguir:
 
    $verifiedDomain = "contoso.com"    # Replace this with any of your verified domain names in Azure AD
    $tenantID = "72f988bf-86f1-41af-91ab-2d7cd011db47"    # Replace this with you tenant ID
    $configNC = "CN=Configuration,DC=corp,DC=contoso,DC=com"    # Replace this with your AD configuration naming context

    $de = New-Object System.DirectoryServices.DirectoryEntry
    $de.Path = "LDAP://CN=Services," + $configNC

    $deDRC = $de.Children.Add("CN=Device Registration Configuration", "container")
    $deDRC.CommitChanges()

    $deSCP = $deDRC.Children.Add("CN=62a0ff2e-97b9-4513-943f-0d221bd30080", "serviceConnectionPoint")
    $deSCP.Properties["keywords"].Add("azureADName:" + $verifiedDomain)
    $deSCP.Properties["keywords"].Add("azureADId:" + $tenantID)

    $deSCP.CommitChanges()


## <a name="step-2-setup-issuance-of-claims"></a>Etapa 2: configurar a emissão de declarações

No Azure federado configuração do AD, dispositivos contam com os serviços de Federação do Active Directory (AD FS) ou uma parte 3 de tooAzure de tooauthenticate de serviço de Federação AD local. Dispositivos autenticam tooget um tooregister de token de acesso em relação a saudação do Azure Active Directory Device Registration Service (DRS do Azure).

Windows dispositivos atuais se autenticar usando a autenticação integrada do Windows tooan WS-Trust ponto de extremidade ativo (versões 1.3 ou 2005) hospedado pelo serviço de federação local hello.

> [!NOTE]
> Ao usar o AD FS, **adfs/services/trust/13/windowstransport** ou **adfs/services/trust/2005/windowstransport** devem ser habilitados. Se você estiver usando Olá Proxy de autenticação da Web, também Certifique-se de que esse ponto de extremidade é publicado por meio do proxy de saudação. Você pode ver quais pontos de extremidade são habilitados por meio do console de gerenciamento de saudação do AD FS em **Service > pontos de extremidade**.
>
>Se você não tiver o AD FS como seu serviço de federação local, siga as instruções de saudação do seu toomake fornecedor se que eles dão suporte a WS-Trust 1.3 ou pontos de extremidade de 2005 e que eles são publicados por meio de saudação (MEX) do arquivo de troca de metadados.

Olá seguintes declarações devem existir no token Olá recebida pelo Azure DRS para toocomplete de registro do dispositivo. DRS Azure criará um objeto de dispositivo no AD do Azure com algumas dessas informações que são usadas pelo objeto de dispositivo do Azure AD Connect tooassociate Olá recém-criado com hello computador conta local.

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

Se você tiver mais de um nome de domínio verificado, você precisa tooprovide Olá declaração para os computadores a seguir:

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

Se você já esteja emitindo uma declaração de ImmutableID (por exemplo, a ID de logon alternativo), será necessário tooprovide uma declaração correspondente para computadores:

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

Em Olá seções a seguir, você pode encontrar informações sobre:
 
- os valores Hello cada declaração deve ter
- Como uma definição se pareceria no AD FS

definição de saudação ajuda tooverify se houver valores hello, ou se você precisa toocreate-los.

> [!NOTE]
> Se você não usar o AD FS para o servidor de federação local, siga tooissue de configuração apropriada do fornecedor instruções toocreate Olá essas declarações.

### <a name="issue-account-type-claim"></a>Emitir declaração de tipo de conta

**`http://schemas.microsoft.com/ws/2012/01/accounttype`**-Esta declaração deve conter um valor de **DJ**, que identifica o dispositivo hello como um computador ingressado no domínio. No AD FS, você pode adicionar uma regra de transformação de emissão que se parece com o seguinte:

    @RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );

### <a name="issue-objectguid-of-hello-computer-account-on-premises"></a>Execute o objectGUID do hello computador conta local

**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`**-Esta declaração deve conter Olá **objectGUID** valor Olá conta de computador local. No AD FS, você pode adicionar uma regra de transformação de emissão que se parece com o seguinte:

    @RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );
 
### <a name="issue-objectsid-of-hello-computer-account-on-premises"></a>Problema objectSID Olá computador conta local

**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`**-Esta declaração deve conter Olá Olá **objectSid** valor Olá conta de computador local. No AD FS, você pode adicionar uma regra de transformação de emissão que se parece com o seguinte:

    @RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a>Emita o issuerID de computador quando houver vários nomes de domínio verificados no Azure AD

**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`**-Esta declaração deve conter Olá identificador URI (Uniform Resource) de qualquer um dos Olá verificar nomes de domínio que se conectam com hello token de emissão Olá federation service (AD FS ou 3ª parte) local. No AD FS, você pode adicionar regras de transformação de emissão que pareçam Olá aquelas abaixo em que ordem específica após Olá aquelas acima. Observe que essa regra de saudação do problema de tooexplicitly uma regra para os usuários é necessário. Em regras de saudação abaixo, uma regra primeiro identificar o usuário vs. autenticação de computador é adicionada.

    @RuleName = "Issue account type with hello value User when its not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://<verified-domain-name>/adfs/services/trust/"
    );


Declaração de saudação acima,

- `$<domain>`é a URL do serviço Olá AD FS
- `<verified-domain-name>`é um espaço reservado é necessário tooreplace com um de seus nomes de domínio verificado no AD do Azure



Para obter mais detalhes sobre nomes de domínio verificado, consulte [adicionar um nome de domínio personalizado tooAzure do Active Directory](active-directory-add-domain.md).  
tooget uma lista de seus domínios da empresa verificados, você pode usar o hello [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet. 

![Get-MsolDomain](./media/active-directory-conditional-access-automatic-device-registration-setup/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a>Emitir o ImmutableID de computador quando houver um para o usuário (por exemplo, a ID de login alternativa é definida)

**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - Essa declaração deve conter um valor válido para computadores. No AD FS, você pode criar uma regra de transformação de emissão da seguinte maneira:

    @RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );

### <a name="helper-script-toocreate-hello-ad-fs-issuance-transform-rules"></a>Regras de transformação de auxiliar script toocreate Olá AD FS emissão

Hello script a seguir ajudará com a criação de saudação de emissão de saudação transformar regras descritas acima.

    $multipleVerifiedDomainNames = $false
    $immutableIDAlreadyIssuedforUsers = $false
    $oneOfVerifiedDomainNames = 'example.com'   # Replace example.com with one of your verified domains
    
    $rule1 = '@RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );'

    $rule2 = '@RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'

    $rule3 = '@RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);'

    $rule4 = ''
    if ($multipleVerifiedDomainNames -eq $true) {
    $rule4 = '@RuleName = "Issue account type with hello value User when it is not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://' + $oneOfVerifiedDomainNames + '/adfs/services/trust/"
    );'
    }

    $rule5 = ''
    if ($immutableIDAlreadyIssuedforUsers -eq $true) {
    $rule5 = '@RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'
    }

    $existingRules = (Get-ADFSRelyingPartyTrust -Identifier urn:federation:MicrosoftOnline).IssuanceTransformRules 

    $updatedRules = $existingRules + $rule1 + $rule2 + $rule3 + $rule4 + $rule5

    $crSet = New-ADFSClaimRuleSet -ClaimRule $updatedRules 

    Set-AdfsRelyingPartyTrust -TargetIdentifier urn:federation:MicrosoftOnline -IssuanceTransformRules $crSet.ClaimRulesString 

### <a name="remarks"></a>Comentários 

- Esse script acrescenta Olá regras toohello existente regras. Script de saudação não são executadas duas vezes porque Olá conjuntos de regras será adicionado duas vezes. Certifique-se de que nenhuma regra correspondente existe para essas declarações (em condições de correspondente Olá) antes de executar o script hello novamente.

- Se você tiver vários nomes de domínio verificado (conforme mostrado no portal de saudação do AD do Azure ou por meio do cmdlet Get-MsolDomains de saudação), definir o valor de saudação do **$multipleVerifiedDomainNames** Olá script muito**$true**. Além disso, certifique-se de remover qualquer declaração de issuerid existente que possa ter sido criada pelo Azure AD Connect ou por outros meios. Aqui está um exemplo dessa regra:


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- Se você já tiver emitido um **ImmutableID** de declaração para contas de usuário, defina o valor de saudação do **$immutableIDAlreadyIssuedforUsers** Olá script muito**$true**.

## <a name="step-3-enable-windows-down-level-devices"></a>Etapa 3: habilitar dispositivos de nível inferior do Windows

Se alguns dos seus dispositivos associados ao domínio forem dispositivos de nível inferior do Windows, você precisa:

- Defina uma política no AD do Azure tooenable tooregister os dispositivos dos usuários.
 
- Configurar o local federação serviço tooissue declarações toosupport **Windows IWA (autenticação integrada)** para registro do dispositivo.
 
- Adicione Olá AD do Azure dispositivo autenticação ponto de extremidade toohello local Intranet zonas tooavoid certificado solicita ao autenticar o dispositivo hello.

### <a name="set-policy-in-azure-ad-tooenable-users-tooregister-devices"></a>Definir a diretiva no AD do Azure tooenable tooregister os dispositivos dos usuários

tooregister dispositivos de nível inferior do Windows, você precisa toomake-se de que Olá configuração tooallow usuários tooregister dispositivos no AD do Azure está definida. Olá portal do Azure, você encontrará essa configuração em:

`Azure Active Directory > Users and groups > Device settings`
    
Olá seguinte política deve ser definida muito**todos os**: **os usuários podem registrar seus dispositivos com o Azure AD**

![Registrar dispositivos](./media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a>Configurar o serviço de federação local 

Seu serviço de federação local deve oferecer suporte à emissão Olá **authenticationmehod** e **wiaormultiauthn** declarações durante o recebimento de uma autenticação solicitar a terceira parte confiável toohello AD do Azure mantém um resouce_params parâmetro com um valor codificado conforme mostrado abaixo:

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

Quando essa solicitação chega, serviço de federação local Olá deve autenticar o usuário hello usando a autenticação integrada do Windows e ao ser bem-sucedido, ele deverá emitir Olá duas declarações a seguir:

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

No AD FS, você deve adicionar esse método de autenticação Olá passa por uma regra de transformação de emissão.  

**tooadd essa regra:**

1. No console de gerenciamento do hello AD FS, vá muito`AD FS > Trust Relationships > Relying Party Trusts`.
2. Objeto de confiança de terceiros confiável Olá plataforma de identidade do Microsoft Office 365 e, em seguida, selecione **editar regras de declaração**.
3. Em Olá **regras de transformação de emissão** guia, selecione **Adicionar regra**.
4. Em Olá **regra de declaração** lista de modelo, selecione **enviar declarações usando uma regra personalizada**.
5. Selecione **Avançar**.
6. Em Olá **nome da regra de declaração** , digite **regra de declaração de método de autenticação**.
7. Em Olá **regra de declaração** caixa, Olá tipo regra a seguir:

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. No servidor de federação, digite o comando do PowerShell Olá abaixo depois de substituir  **\<RPObjectName\>**  com hello terceira parte confiável nome do objeto para o objeto de confiança de terceiros confiável do AD do Azure. Geralmente, este objeto é nomeado como **Plataforma de Identidade do Microsoft Office 365**.
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-hello-azure-ad-device-authentication-end-point-toohello-local-intranet-zones"></a>Adicionar zonas de Intranet Local Olá AD do Azure dispositivo autenticação ponto de extremidade toohello

certificado tooavoid avisa quando os usuários no registro de dispositivos autenticar tooAzure AD, você pode enviar uma saudação de tooadd política tooyour dispositivos que ingressaram no domínio seguindo a zona de Intranet Local toohello URL no Internet Explorer:

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a>Etapa 4: implantação de controle e distribuição

Quando você concluiu as etapas de saudação necessários, dispositivos que ingressaram no domínio são tooautomatically pronto junção do Azure AD:

- Todos os dispositivos associados ao domínio que executarem a Atualização de Aniversário do Windows 10 e o Windows Server 2016 serão registrados automaticamente no Azure AD na reinicialização do dispositivo ou no login. 

- Registrar novos dispositivos com o Azure AD quando o dispositivo Olá é reiniciado após a conclusão da operação de junção de domínio hello.

- Dispositivos que foram anteriormente do Azure AD registrados (por exemplo, para o Intune) transição muito "*ingressado no domínio, registrado no AAD*"; no entanto, levará algum tempo para esse processo toocomplete em todos os dispositivos de vencimento toohello o fluxo normal de atividade de usuário e domínio.

### <a name="remarks"></a>Comentários

- Você pode usar uma distribuição de saudação do toocontrol de objeto diretiva de grupo de registro automático do Windows 10 e computadores de domínio do Windows Server 2016.

- Windows 10 de novembro de 2015 atualização associa automaticamente com o Azure AD **somente** se o objeto de diretiva de grupo de distribuição de saudação é definido.

- toorollout de computadores de nível inferior do Windows, você pode implantar um [pacote do Windows Installer](#windows-installer-packages-for-non-windows-10-computers) toocomputers que você selecionar.

- Se você enviar por push a dispositivos que ingressaram no domínio tooWindows 8.1 objeto diretiva de grupo hello, uma junção é aplicada; No entanto, é recomendável que você use Olá [pacote do Windows Installer](#windows-installer-packages-for-non-windows-10-computers) toojoin todos os seus dispositivos de baixo nível do Windows. 

### <a name="create-a-group-policy-object"></a>Criar um objeto de Política de Grupo 

distribuição de saudação toocontrol de computadores atuais do Windows, você deve implantar Olá **registrar os computadores do domínio como dispositivos** dispositivos de toohello de objeto de diretiva de grupo que deseja tooregister. Por exemplo, você pode implantar o grupo de segurança de tooa ou unidade organizacional do hello política tooan.

**política de saudação tooset:**

1. Abra **Gerenciador do servidor**e, em seguida, ir muito`Tools > Group Policy Management`.
2. Vá toohello nó do domínio que corresponde a toohello domínio onde você deseja tooactivate o registro automático de computadores com Windows atuais.
3. Clique com o botão direito do mouse em **Objetos de Política de Grupo** e selecione **Novo**.
4. Insira um nome para o objeto de Política de Grupo. Por exemplo, *Ingresso no Azure AD híbrido. 
5. Clique em **OK**.
6. Clique com o botão direito do mouse em seu novo objeto de Política de Grupo e selecione **Editar**.
7. Vá muito**configuração do computador** > **políticas** > **modelos administrativos** > **Windows Componentes** > **registro de dispositivo**. 
8. Clique com o botão direito do mouse em **Registrar computadores associados ao domínio como dispositivos** e selecione **Editar**.
   
   > [!NOTE]
   > Este modelo de diretiva de grupo foi renomeado de versões anteriores do console de gerenciamento de política de grupo de saudação. Se você estiver usando uma versão anterior do console Olá, vá muito`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`. 

7. Selecione **Habilitado** e clique em **Aplicar**.
8. Clique em **OK**.
9. Saudação de link local de tooa de objeto de diretiva de grupo de sua escolha. Por exemplo, você pode vincular unidade organizacional específica de tooa. Você também pode vinculá-lo tooa o grupo de segurança específico de computadores que unir automaticamente com o Azure AD. tooset essa política para todos os computadores ingressados em domínio Windows 10 e Windows Server 2016 em sua organização, o domínio toohello de objeto de diretiva de grupo do link hello.

### <a name="windows-installer-packages-for-non-windows-10-computers"></a>Pacotes do Windows Installer para computadores que não são do Windows 10

computadores de nível inferior Windows toojoin ingressado no domínio em um ambiente federado, você pode baixar e instalar esses pacotes do Windows Installer (. msi) do Centro de Download em Olá [Microsoft ingresso no local para computadores sem Windows 10](https://www.microsoft.com/en-us/download/details.aspx?id=53554)página.

Você pode implantar o pacote de saudação usando um sistema de distribuição de software como o System Center Configuration Manager. Olá pacote dá suporte a opções de instalação silenciosa padrão Olá com hello *silencioso* parâmetro. Ramificação atual do System Center Configuration Manager oferece benefícios adicionais de versões anteriores, como registros do hello capacidade tootrack concluída. Para obter mais informações, consulte [System Center 2016](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).

instalador de saudação cria uma tarefa agendada no sistema de saudação que é executado no contexto de saudação do usuário. tarefa Olá é disparada quando o usuário Olá entra em tooWindows. tarefa Olá silenciosamente une dispositivo Olá com o Azure AD com as credenciais do usuário Olá depois de autenticar usando a autenticação integrada do Windows. tarefa agendada do toosee hello, no dispositivo hello, ir muito**Microsoft** > **ingresso**, e em seguida, acesse a biblioteca do Agendador de tarefas toohello.

## <a name="step-5-verify-joined-devices"></a>Etapa 5: Verificar os dispositivos adicionados

Você pode verificar dispositivos Unidos com êxito em sua organização usando Olá [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet Olá [módulo do Azure Active Directory PowerShell](/powershell/azure/install-msonlinev1?view=azureadps-2.0).

saída deste cmdlet Olá mostra os dispositivos registrados e associados ao Azure AD. tooget todos os dispositivos, use Olá **-todos os** parâmetro e, em seguida, filtrá-los usando Olá **deviceTrustType** propriedade. Dispositivos associados ao domínio possuem um valor de **Associado ao domínio**.

## <a name="next-steps"></a>Próximas etapas

* [Gerenciamento de toodevice de Introdução no Active Directory do Azure](device-management-introduction.md)



<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
