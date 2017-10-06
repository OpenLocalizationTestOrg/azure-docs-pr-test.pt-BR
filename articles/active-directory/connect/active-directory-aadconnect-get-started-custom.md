---
title: "Instalação personalizada do Azure AD Connect | Microsoft Docs"
description: "Este documento fornece detalhes sobre as opções de instalação personalizada Olá para o Azure AD Connect. Use essas instruções tooinstall do Active Directory por meio do Azure AD Connect."
services: active-directory
keywords: "o que é o Azure AD Connect, instalar o Active Directory, componentes necessários do AD do Azure"
documentationcenter: 
author: billmath
manager: femila
ms.assetid: 6d42fb79-d9cf-48da-8445-f482c4c536af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: c49724fab78c5a1688662043f69506fff6f82104
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="custom-installation-of-azure-ad-connect"></a>Instalação personalizada do Azure AD Connect
Azure AD Connect **configurações personalizadas** é usado quando você quiser mais opções para instalação de saudação. Ele é usado se você tiver várias florestas ou se você quiser tooconfigure recursos opcionais que não são abordados instalação expressa hello. Ele é usado em todos os casos onde hello [ **instalação expressa** ](active-directory-aadconnect-get-started-express.md) opção não satisfaz a implantação ou a topologia.

Antes de iniciar a instalação do Azure AD Connect, certifique-se muito[download do Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771) e etapas de pré-requisito concluída Olá no [do Azure AD Connect: pré-requisitos de Hardware e](active-directory-aadconnect-prerequisites.md). Também verifique se você tem as contas necessárias disponíveis, conforme descrito em [Contas e permissões do Azure AD Connect](active-directory-aadconnect-accounts-permissions.md).

Se as configurações personalizadas não coincide com a topologia, por exemplo, tooupgrade DirSync, consulte [relacionada documentação](#related-documentation) para outros cenários.

## <a name="custom-settings-installation-of-azure-ad-connect"></a>Instalação de configurações personalizadas do Azure AD Connect
### <a name="express-settings"></a>Configurações Expressas
Nessa página, clique em **personalizar** toostart uma instalação de configurações personalizadas.

### <a name="install-required-components"></a>Instalar componentes necessários
Quando você instala os serviços de sincronização hello, você pode deixar a seção de configuração opcional Olá desmarcada e Azure AD Connect configura tudo automaticamente. Define uma instância do SQL Server 2012 Express LocalDB, criar grupos apropriados hello e atribuir permissões. Se você quiser toochange Olá padrões, você pode usar Olá tabela toounderstand Olá opções de configuração opcionais que estão disponíveis a seguir.

![Componentes necessários](./media/active-directory-aadconnect-get-started-custom/requiredcomponents.png)

| Configuração opcional | Descrição |
| --- | --- |
| Usar um SQL Server existente |Permite que você toospecify Olá nome e SQL Server nome da instância hello. Escolha esta opção se você já tiver um servidor de banco de dados que deseja toouse. Insira nome de instância Olá seguido por um vírgula e número da porta em **nome de instância** se o SQL Server não tem a navegação habilitada. |
| Usar uma conta de serviço existente |Por padrão o Azure AD Connect usa uma conta de serviço virtual para Olá toouse de serviços de sincronização. Se você usa um SQL server remoto ou usa um proxy que requer autenticação, você precisa toouse um **conta de serviço gerenciado** ou usar uma conta de serviço no domínio hello e saber a senha de saudação. Nesses casos, digite Olá conta toouse. Certifique-se de usuário Olá executando instalação Olá é um SA no SQL para que um logon para conta de serviço Olá pode ser criado. Veja [Contas e permissões do Azure AD Connect](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account) |
| Especificar grupos de sincronização personalizados |Por padrão do Azure AD Connect cria quatro servidores de local toohello grupos quando os serviços de sincronização de saudação são instalados. Esses grupos são: grupo Administradores, grupo de operadores, procurar grupo e Olá grupo de redefinição de senha. Você pode especificar seus próprios grupos aqui. os grupos de saudação devem ser locais no servidor de saudação e não podem ser localizados no domínio hello. |

### <a name="user-sign-in"></a>Entrada do usuário
Depois de instalar os componentes de saudação necessárias, você será solicitado a tooselect seus usuários único método de logon. Olá, a tabela a seguir fornece uma breve descrição das opções disponíveis de saudação. Para obter uma descrição completa de métodos de entrada hello, consulte [usuário entrar](active-directory-aadconnect-user-signin.md).

![Entrada do Usuário](./media/active-directory-aadconnect-get-started-custom/usersignin2.png)

| Opção de logon único | Descrição |
| --- | --- |
| Sincronização de senha |Os usuários são capaz toosign tooMicrosoft em serviços em nuvem, como o Office 365, usando Olá a mesma senha usada na sua rede local. as senhas dos usuários de saudação são sincronizado tooAzure AD como um hash de senha e a autenticação ocorre na nuvem de saudação. Veja [Sincronização de senha](active-directory-aadconnectsync-implement-password-synchronization.md) para obter mais informações. |
|Autenticação de Passagem (Visualização)|Os usuários são capaz toosign tooMicrosoft em serviços em nuvem, como o Office 365, usando Olá a mesma senha usada na sua rede local.  senha de usuários Olá é passada por toohello local do Active Directory controlador toobe validado.
| Federação com AD FS |Os usuários são capaz toosign tooMicrosoft em serviços em nuvem, como o Office 365, usando Olá a mesma senha usada na sua rede local.  Olá usuários são redirecionados tootheir toosign de instância do AD FS no local e a autenticação ocorre no local. |
| Não configurar |Nenhum dos recursos é instalado e configurado. Escolha essa opção se você já tiver um servidor de federação de terceiros ou outra solução existente em vigor. |
|Habilitar o Logon Único|Esta opção está disponível com a sincronização de senha e autenticação de passagem e fornece um logon único na experiência para usuários da área de trabalho na rede corporativa hello.  Para obter mais informações, veja [Logon único](active-directory-aadconnect-sso.md). </br>Observação para os clientes do AD FS essa opção não está disponível porque o AD FS já oferece Olá mesmo nível de logon único no.</br>(se PTA não for liberado no hello simultaneamente)
|Opção de Logon|Esta opção está disponível para clientes de sincronização de senha e fornece um logon único na experiência para usuários da área de trabalho na rede corporativa hello.  </br>Para obter mais informações, veja [Logon único](active-directory-aadconnect-sso.md). </br>Observação para os clientes do AD FS essa opção não está disponível porque o AD FS já oferece Olá mesmo nível de logon único no.


### <a name="connect-tooazure-ad"></a>Conecte-se tooAzure AD
Na tela de tooAzure AD conexão hello, insira uma conta de administrador global e a senha. Se você selecionou **federação com o AD FS** na página anterior do hello, não se conectar com uma conta em um domínio, você planejar tooenable para federação. Uma recomendação é uma conta no padrão de saudação do toouse **m** domínio, que acompanha o seu diretório do AD do Azure.

Essa conta é apenas utilizado toocreate uma conta de serviço no AD do Azure e não é usada após a conclusão do Assistente de saudação.  
![Entrada do Usuário](./media/active-directory-aadconnect-get-started-custom/connectaad.png)

Se sua conta de administrador global tem MFA habilitado, você precisa tooprovide Olá senha novamente Olá entrar popup e completa Olá desafio MFA. desafio Olá poderia ser um fornecendo um código de verificação ou uma chamada telefônica.  
![Entrada do usuário no MFA](./media/active-directory-aadconnect-get-started-custom/connectaadmfa.png)

conta de administrador global Olá também pode ter [Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md) habilitado.

Se você encontrar um erro e tiver problemas de conectividade, confira [Solucionar problemas de conectividade](active-directory-aadconnect-troubleshoot-connectivity.md).

## <a name="pages-under-hello-section-sync"></a>Páginas na seção Olá sincronização

### <a name="connect-your-directories"></a>Conecte seus diretórios
tooconnect tooyour o serviço de domínio do Active Directory, Azure AD Connect precisa de nome da floresta hello e credenciais de uma conta com permissões suficientes.

![Conectar-se ao Diretório](./media/active-directory-aadconnect-get-started-custom/connectdir01.png)

Depois de inserir o nome da floresta hello e clicando em **Adicionar diretório**, uma caixa de diálogo pop-up é exibida e solicita que você com hello as opções a seguir:

| Opção | Descrição |
| --- | --- |
| Usar conta existente | Selecione esta opção se você quiser tooprovide um existente do AD DS conta toobe usado do Azure AD Connect para conectar-se a floresta do AD de toohello durante a sincronização de diretório. Você pode inserir parte do domínio Olá no formato NetBios ou FQDN, ou seja, FABRIKAM\syncuser ou fabrikam.com\syncuser. Essa conta pode ser uma conta de usuário regular, porque ele só precisa de permissões de leitura saudação padrão. No entanto, dependendo do cenário, talvez você precise de mais permissões. Para saber mais, confira [Contas e permissões do Azure AD Connect](active-directory-aadconnect-accounts-permissions.md#create-the-ad-ds-account). |
| Criar nova conta | Selecione esta opção se você deseja que o Azure AD Connect Assistente toocreate Olá AD DS conta exigida pelo Azure AD Connect para conectar-se a floresta do AD de toohello durante a sincronização de diretório. Quando essa opção é selecionada, digite Olá username e password para uma conta de administrador corporativo. Olá conta de administrador corporativo fornecida será usada pelo Azure AD Connect saudação do assistente toocreate necessário conta AD DS. Você pode inserir parte do domínio Olá no formato NetBios ou FQDN, ou seja, FABRIKAM\administrator ou fabrikam.com\administrator. |

![Conectar-se ao Diretório](./media/active-directory-aadconnect-get-started-custom/connectdir02.png)


### <a name="azure-ad-sign-in-configuration"></a>Configuração de entrada do Azure AD
Esta página permite que você tooreview presente no local de domínios UPN de saudação AD DS e que foram verificado no AD do Azure. Esta página também permite tooconfigure Olá atributo toouse para userPrincipalName hello.

![Domínios não verificados](./media/active-directory-aadconnect-get-started-custom/aadsigninconfig.png)  
Examine cada domínio marcado como **Não Adicionado** e **Não Verificado**. Confira se os domínios que você usa foram verificados no Azure AD. Clique em símbolo de atualização hello quando você verificou se seus domínios. Para obter mais informações, consulte [adicionar e verificar o domínio Olá](../active-directory-add-domain.md)

**UserPrincipalName** -Olá atributo userPrincipalName é usuários do atributo Olá usam ao entrar no tooAzure AD e Office 365. domínios de saudação usada, também conhecido como Olá sufixo UPN, deve ser verificado no AD do Azure antes de saudação usuários estão sincronizados. A Microsoft recomenda tookeep saudação padrão atributo userPrincipalName. Se esse atributo não pode ser roteado e não pode ser verificado, é possível tooselect outro atributo. Por exemplo você pode selecionar email como atributo Olá mantendo Olá ID de entrada. O uso de um atributo diferente de userPrincipalName é conhecido como **ID Alternativa**. Olá valor do atributo ID alternativo deve seguir Olá RFC822 padrão. Uma ID Alternativa pode ser usada com a sincronização de senha e com a federação.

>[!NOTE]
> Quando você habilitar a autenticação de passagem, você deve ter pelo menos um domínio verificado na ordem toocontinue por meio do Assistente de saudação.

> [!WARNING]
> Usar uma ID alternativa não é compatível com todas as cargas de trabalho do Office 365. Para obter mais informações, consulte muito[Configurando ID de logon alternativo](https://technet.microsoft.com/library/dn659436.aspx).
>
>

### <a name="domain-and-ou-filtering"></a>Filtragem de domínio e UO
Por padrão, todos os domínios e UOs são sincronizados. Se houver alguns domínios ou unidades organizacionais que você deseja não toosynchronize tooAzure AD, você pode desmarcar esses domínios e unidades organizacionais.  
![Filtragem de DomainOU](./media/active-directory-aadconnect-get-started-custom/domainoufiltering.png)  
Esta página no Assistente de saudação é a configuração baseada em domínio e no OU filtragem. Se você planejar toomake alterações, consulte [filtragem baseada em domínio](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering) e [filtragem baseada em unidade organizacional](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) antes de fazer essas alterações. Algumas unidades organizacionais são essenciais para a funcionalidade de saudação e não devem ser desmarcadas.

Se você usar a filtragem baseada em Unidade Organizacional com versão do Azure AD Connect anterior a 1.1.524.0, as novas OUs adicionadas posteriormente serão sincronizadas por padrão. Se você deseja que o comportamento de saudação que a nova UOs não devem ser sincronizados, você pode configurá-lo após Olá assistente foi concluído com [filtragem baseada em unidade organizacional](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering). Para o Azure AD Connect versão 1.1.524.0 ou após, você pode indicar se deseja que o novo toobe UOs sincronizado ou não.

Se você planejar toouse [filtragem baseada em grupo](#sync-filtering-based-on-groups), verifique se hello OU com o grupo de saudação é incluído e não filtrado com a filtragem de UO. A filtragem de UO é avaliada antes da filtragem baseada em grupo.

Também é possível que alguns domínios não estão acessíveis devido a restrições de toofirewall. Esses domínios estão desmarcados por padrão e têm um aviso.  
![Domínios inacessíveis](./media/active-directory-aadconnect-get-started-custom/unreachable.png)  
Se você vir esse aviso, certifique-se de que esses domínios são realmente inacessíveis e aviso de saudação é esperado.

### <a name="uniquely-identifying-your-users"></a>Identificar com exclusividade seus usuários

#### <a name="select-how-users-should-be-identified-in-your-on-premises-directories"></a>Selecione como os usuários devem ser identificados em seus diretórios locais
Olá correspondência entre florestas recurso permite que você toodefine como os usuários de sua florestas do AD DS são representados no AD do Azure. Um usuário também pode ser representado somente uma vez em todas as florestas ou ter uma combinação de contas habilitadas e desabilitadas. usuário Olá também pode ser representado como um contato em algumas florestas.

![Exclusivo](./media/active-directory-aadconnect-get-started-custom/unique.png)

| Configuração | Descrição |
| --- | --- |
| [Os usuários são representados apenas uma vez em todas as florestas](active-directory-aadconnect-topologies.md#multiple-forests-single-azure-ad-tenant) |Todos os usuários são criados como objetos individuais no AD do Azure. Olá objetos não são ingressados no metaverso hello. |
| [Atributo de email](active-directory-aadconnect-topologies.md#multiple-forests-single-azure-ad-tenant) |Essa opção ingressa usuários e contatos, se o atributo de email Olá Olá mesmo valor em florestas diferentes. Será recomendável usar essa opção quando seus contatos tiverem sido criados com GALSync. Se esta opção for escolhida, os objetos de usuário cujo atributo de email não são preenchidos não será sincronizado tooAzure AD. |
| [ObjectSID e msExchangeMasterAccountSID/ msRTCSIP-OriginatorSid](active-directory-aadconnect-topologies.md#multiple-forests-single-azure-ad-tenant) |Essa opção associa um usuário habilitado em uma floresta de conta com um usuário desabilitado em uma floresta de recursos. No Exchange, essa configuração é conhecida como uma caixa de correio vinculada. Essa opção também pode ser usada se você usar somente o Lync e Exchange não está presente na floresta de recursos de saudação. |
| sAMAccountName e MailNickName |Essa opção ingressa em atributos em que é a ID de entrada hello esperado para usuário Olá pode ser encontrado. |
| Um atributo específico |Essa opção permite que você tooselect seu próprio atributo. Se esta opção for escolhida, os objetos de usuário cujo atributo (selecionado) não são preenchidos não será sincronizado tooAzure AD. **Limitação:** tornar toopick-se de que um atributo que já pode ser encontrado no metaverso hello. Se você escolher um atributo personalizado (não no metaverso Olá), não pode concluir o Assistente de saudação. |

#### <a name="select-how-users-should-be-identified-with-azure-ad---source-anchor"></a>Selecione como os usuários devem ser identificados no Azure AD - âncora de origem
Olá atributo sourceAnchor é um atributo que é imutável durante o tempo de vida de saudação de um objeto de usuário. É a chave primária de Olá vinculação de usuário local de saudação com usuário Olá no AD do Azure.

| Configuração | Descrição |
| --- | --- |
| Permitir que o Azure gerenciar âncora de origem Olá para mim | Selecione esta opção se você quiser o atributo do AD do Azure toopick Olá para você. Se você selecionar essa opção, o Assistente do Azure AD Connect se aplica a lógica de seleção Olá sourceAnchor atributo descrita na seção do artigo [do Azure AD Connect: conceitos - usando msDS-ConsistencyGuid como sourceAnchor de projeto](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor). Assistente de saudação informa qual atributo foi escolhido como atributo de âncora de origem Olá após a conclusão da instalação personalizada. |
| Um atributo específico | Selecione esta opção se desejar toospecify um atributo de AD existente como Olá sourceAnchor. |

Desde que o atributo de saudação não pode ser alterado, você deve planejar toouse um atributo válido. Um bom candidato é objectGUID. Esse atributo não for alterado, a menos que a conta de usuário de saudação é movida entre florestas/domínios. Em um ambiente de várias floresta em que você mover contas entre florestas, outro atributo deve ser usado, como um atributo com hello employeeID. Evite atributos que seriam alterados quando uma pessoa casasse ou mudasse de cargo. Você não pode usar atributos com um caractere @-sign, portanto, email e userPrincipalName não podem ser usados. atributo Olá também diferencia maiusculas de minúsculas então quando você move um objeto entre florestas, certifique-se de que toopreserve Olá maiusculas/minúsculas. Os atributos binários são codificados em base64, mas outros tipos de atributo permanecem no estado não codificado. Em cenários de federação e em algumas interfaces do AD do Azure, esse atributo também é conhecido como immutableID. Para obter mais informações sobre a âncora de origem Olá podem ser encontradas no hello [conceitos de projeto](active-directory-aadconnect-design-concepts.md#sourceanchor).

### <a name="sync-filtering-based-on-groups"></a>Filtragem de sincronização com base em grupos
Olá filtragem no recurso de grupos permite que você toosync apenas um pequeno subconjunto de objetos para um piloto. toouse esse recurso, criar um grupo para essa finalidade no Active Directory local. Em seguida, adicione usuários e grupos que devem ser sincronizado tooAzure AD como membros diretos. Posteriormente, você pode adicionar e remover usuários toothis grupo toomaintain Olá lista de objetos que devem estar presentes no AD do Azure. Todos os objetos que você deseja toosynchronize devem ser um membro direto do grupo de saudação. Isso incluirá os usuários, os grupos, os contatos e os computadores/dispositivos. A associação de grupos aninhados não é resolvida. Quando você adiciona um grupo como um membro, grupo Olá somente em si é adicionado e não a seus membros.

![Filtragem de sincronização](./media/active-directory-aadconnect-get-started-custom/filter2.png)

> [!WARNING]
> Este recurso está apenas pretendido toosupport uma implantação piloto. Não o utilize em uma implantação de produção completa.
>
>

Em uma implantação de produção completo, vai toobe rígido toomaintain um único grupo com todos os toosynchronize de objetos. Em vez disso, você deve usar um dos métodos de saudação em [configurar filtragem](active-directory-aadconnectsync-configure-filtering.md).

### <a name="optional-features"></a>Recursos opcionais
Esta tela permite recursos opcionais do tooselect Olá para seus cenários específicos.

![Recursos opcionais](./media/active-directory-aadconnect-get-started-custom/optional.png)

> [!WARNING]
> Se você tiver atualmente DirSync ou o Azure AD Sync active, não ative qualquer um dos recursos de write-back de saudação no Azure AD Connect.
>
>

| Recursos opcionais | Descrição |
| --- | --- |
| Implantação híbrida do Exchange  |Olá recurso de implantação híbrida do Exchange permite Olá coexistência de caixas de correio do Exchange no local e no Office 365. O Azure AD Connect está sincronizando um conjunto específico de [atributos](active-directory-aadconnectsync-attributes-synchronized.md#exchange-hybrid-writeback) do Azure AD em seu diretório local. |
| Pastas públicas do Exchange Mail | recurso de pastas públicas do Exchange Mail Olá permite que objetos de pasta pública toosynchronize habilitados para email de seu tooAzure do Active Directory local AD. |
| Aplicativo AD do Azure e filtragem de atributos |Habilitando o aplicativo do Azure AD e filtragem de atributo, hello conjunto de atributos sincronizados pode ser personalizado. Essa opção adiciona dois mais páginas toohello Assistente para configuração. Para saber mais, confira [Aplicativo e filtragem de atributos do Azure AD](#azure-ad-app-and-attribute-filtering). |
| Sincronização de senha |Se você selecionou federação como solução de entrada hello, você pode habilitar essa opção. Em seguida, a sincronização de senha pode ser usada como uma opção de backup. Para saber mais, confira [Sincronização de senha](active-directory-aadconnectsync-implement-password-synchronization.md). </br></br>Se você selecionou a autenticação de passagem essa opção é habilitada por padrão tooensure suporte para clientes herdados e como uma opção de backup. Para saber mais, confira [Sincronização de senha](active-directory-aadconnectsync-implement-password-synchronization.md).|
| Write-back de senha |Habilitando o write-back de senha, as alterações de senha originadas no Azure AD serão gravados tooyour diretório de local. Para saber mais, confira [Introdução ao gerenciamento de senhas](../active-directory-passwords-getting-started.md). |
| Write-back de grupo |Se você usar o hello **grupos do Office 365** de recursos, em seguida, você pode ter esses grupos representados no Active Directory local. Essa opção só estará disponível se você tiver o Exchange presente no seu Active Directory local. Para saber mais, confira [Write-back de grupo](active-directory-aadconnect-feature-preview.md#group-writeback). |
| Write-back de dispositivo |Permite que você toowriteback objetos de dispositivo no AD do Azure tooyour no local do Active Directory para cenários de acesso condicional. Para saber mais, confira [Habilitar o write-back de dispositivo no Azure AD Connect](active-directory-aadconnect-feature-device-writeback.md). |
| Sincronização de atributo de extensão de diretório |Habilitando a sincronização de atributos de extensões de diretório, atributos especificados são sincronizado tooAzure AD. Para saber mais, confira [Extensões de diretório](active-directory-aadconnectsync-feature-directory-extensions.md). |

### <a name="azure-ad-app-and-attribute-filtering"></a>Aplicativo AD do Azure e filtragem de atributos
Se você quiser toolimit tooAzure de toosynchronize quais atributos AD, iniciar, em seguida, selecionando os serviços que você está usando. Se você fizer alterações de configuração nesta página, um novo serviço tem toobe explicitamente selecionado por executar novamente o Assistente de instalação de saudação.

![Recursos opcionais - Aplicativos](./media/active-directory-aadconnect-get-started-custom/azureadapps2.png)

Com base nos serviços de saudação selecionados na etapa anterior Olá, esta página mostra todos os atributos que são sincronizados. Esta lista é uma combinação de todos os tipos de objeto que estão sendo sincronizado. Se houver alguns atributos específicos que você precisa toonot sincronizar, você pode cancelar a seleção desses atributos.

![Recursos opcionais - Atributos](./media/active-directory-aadconnect-get-started-custom/azureadattributes2.png)

> [!WARNING]
> A remoção de atributos pode afetar a funcionalidade. Para obter práticas recomendadas e recomendações, confira [atributos sincronizados](active-directory-aadconnectsync-attributes-synchronized.md#attributes-to-synchronize).
>
>

### <a name="directory-extension-attribute-sync"></a>Sincronização de atributo de extensão de diretório
Você pode estender o esquema de saudação no AD do Azure com os atributos personalizados adicionados por sua organização ou outros atributos no Active Directory. toouse esse recurso, selecione **sincronização do atributo de extensão de diretório** em Olá **recursos opcionais** página. Você pode selecionar mais toosync atributos nesta página.

![Extensões de diretório](./media/active-directory-aadconnect-get-started-custom/extension2.png)

Para saber mais, confira [Extensões de diretório](active-directory-aadconnectsync-feature-directory-extensions.md).

### <a name="enabling-single-sign-on-sso"></a>Habilitando o SSO (Logon Único)
Configurar o logon único para uso com a autenticação de passagem ou sincronização de senha é um processo simples que você só precisa toocomplete uma vez para cada floresta que está sendo sincronizado tooAzure AD. A configuração envolve duas etapas, da seguinte maneira:

1.  Crie conta de computador necessárias de saudação no Active Directory local.
2.  Configure a zona de intranet Olá das máquinas de clientes Olá toosupport único logon.

#### <a name="create-hello-computer-account-in-active-directory"></a>Criar conta de computador Olá no Active Directory
Para cada floresta que tenha sido adicionada no Azure AD Connect, você precisará toosupply credenciais de administrador de domínio para que a conta de computador Olá pode ser criada em cada floresta. credenciais de saudação são somente à conta de saudação toocreate usado e não são armazenadas ou usadas para qualquer outra operação. Basta adicionar credenciais Olá em Olá **logon único habilitar** página do Assistente de conexão Olá AD do Azure conforme mostrado:

![Habilitar o Logon Único](./media/active-directory-aadconnect-get-started-custom/enablesso.png)

>[!NOTE]
>Você pode ignorar uma floresta específica se não desejar toouse logon único nessa floresta.

#### <a name="configure-hello-intranet-zone-for-client-machines"></a>Configurar a zona de Intranet Olá para computadores cliente
tooensure que Olá cliente entradas automaticamente na intranet Olá zona é necessário tooensure duas URLs são parte da zona de intranet hello. Isso garante que o computador ingressado no domínio Olá envia automaticamente um tíquete de Kerberos tooAzure AD quando é rede corporativa toohello conectado.
Em um computador que tenha ferramentas de gerenciamento de diretiva de grupo hello.

1.  Abrir as ferramentas de gerenciamento de política de grupo Olá
2.  Edite diretiva de grupo Olá que serão aplicados tooall usuários. Por exemplo, hello diretiva de domínio padrão.
3.  Navegue muito**página do usuário \ Modelos Administrativos\Componentes do Windows\Internet Explorer controle Panel\Security** e selecione **tooZone lista de atribuição de Site** por imagem Olá abaixo.
4.  Habilitar a política de Olá e digite Olá dois itens na caixa de diálogo Olá a seguir.

        Value: `https://autologon.microsoftazuread-sso.com`  
        Data: 1  
        Value: `https://aadg.windows.net.nsatc.net`  
        Data: 1

5.  Ele deve ser a seguir toohello semelhante:  
![Zonas da Intranet](./media/active-directory-aadconnect-get-started-custom/sitezone.png)

6.  Clique em **Ok** duas vezes.

## <a name="configuring-federation-with-ad-fs"></a>Configurando a federação com o AD FS
Configurar o AD FS com o Azure AD Connect é simples, com apenas alguns cliques. a seguir Olá é necessária antes que a configuração de saudação.

* Um servidor do Windows Server 2012 R2 para o servidor de Federação Olá com gerenciamento remoto habilitado
* Um servidor do Windows Server 2012 R2 para o servidor de Proxy de aplicativo Web hello com gerenciamento remoto habilitado
* Você pretende toouse (por exemplo, sts.contoso.com) do nome do serviço de um certificado SSL para federação Olá

### <a name="ad-fs-configuration-pre-requisites"></a>Pré-requisitos de configuração do AD FS
tooconfigure do AD FS farm usando o Azure AD Connect, certifique-se de que o WinRM é habilitado em servidores remotos hello. Além disso, percorrer o requisito de portas Olá listado na [tabela 3 - Azure AD Connect e servidores de Federação/WAP](active-directory-aadconnect-ports.md#table-3---azure-ad-connect-and-ad-fs-federation-serverswap).

### <a name="create-a-new-ad-fs-farm-or-use-an-existing-ad-fs-farm"></a>Criar um novo farm do AD FS ou usar um farm do AD FS existente
Você pode usar um farm do AD FS existente, ou você pode escolher toocreate um novo farm do AD FS. Se você escolher uma nova toocreate, você é certificado SSL necessária tooprovide hello. Se o certificado SSL da saudação é protegido por senha, você será solicitado a senha hello.

![Farm do AD FS](./media/active-directory-aadconnect-get-started-custom/adfs1.png)

Se você escolher toouse um farm existente do AD FS, você será direcionado diretamente toohello Configurando a relação de confiança de saudação entre tela do AD FS e o Azure AD.

### <a name="specify-hello-ad-fs-servers"></a>Especificar servidores de saudação do AD FS
Digite hello servidores que você deseja tooinstall do AD FS no. Você pode adicionar um ou mais servidores com base em sua necessidades de planejamento de capacidade. Adicione todos os servidores tooActive diretório antes de executar essa configuração. A Microsoft recomenda instalar um único servidor do AD FS para implantações de teste e piloto. Adicionar e implantar suas necessidades de dimensionamento de mais toomeet de servidores executando o Azure AD Connect novamente após a configuração inicial.

> [!NOTE]
> Certifique-se de que todos os servidores são unidas tooan AD domínio antes de fazer essa configuração.
>
>

![Servidores do AD FS](./media/active-directory-aadconnect-get-started-custom/adfs2.png)

### <a name="specify-hello-web-application-proxy-servers"></a>Especificar servidores de Proxy de aplicativo Web Olá
Digite hello servidores que você deseja que seus servidores de proxy de aplicativo Web. servidor de proxy de aplicativo web Hello é implantado em sua rede de Perímetro (voltado para a extranet) e oferece suporte a solicitações de autenticação de extranet de saudação. Você pode adicionar um ou mais servidores com base em sua necessidades de planejamento de capacidade. A Microsoft recomenda instalar um único servidor proxy de aplicativo Web para implantações de teste e piloto. Adicionar e implantar suas necessidades de dimensionamento de mais toomeet de servidores executando o Azure AD Connect novamente após a configuração inicial. É recomendável ter um número equivalente de autenticação de toosatisfy servidores proxy da intranet hello.

> [!NOTE]
> <li> Se conta Olá usada não é um administrador local nos servidores de saudação do AD FS, em seguida, você será solicitado para credenciais de administrador.</li>
> <li> Certifique-se de que há conectividade HTTP/HTTPS entre Olá do Azure AD Connect e servidor de Proxy de aplicativo Web de saudação antes de executar essa etapa.</li>
> <li> Certifique-se de que há conectividade HTTP/HTTPS entre hello servidor de aplicativos Web e Olá AD FS server tooallow autenticação solicitações tooflow por meio de.</li>
>

![Aplicativo Web](./media/active-directory-aadconnect-get-started-custom/adfs3.png)

Você está tooenter solicitadas credenciais para que hello servidor de aplicativo web pode estabelecer um conexão segura toohello AD FS servidor. Essas credenciais necessário toobe um administrador local no saudação do servidor AD FS.

![Proxy](./media/active-directory-aadconnect-get-started-custom/adfs4.png)

### <a name="specify-hello-service-account-for-hello-ad-fs-service"></a>Especificar conta de serviço Olá para Olá serviço AD FS
o serviço de saudação AD FS requer um domínio de serviço tooauthenticate usuários da conta e informações de usuário de pesquisa do Active Directory. Ele pode dar suporte a dois tipos de contas de serviço:

* **Conta do Serviço Gerenciado de Grupo** ‒ introduzida nos Serviços de Domínio do Active Directory com o Windows Server 2012. Esse tipo de conta fornece serviços, como o AD FS, uma única conta sem a necessidade de senha da conta Olá tooupdate regularmente. Use esta opção se você já tiver controladores de domínio do Windows Server 2012 no domínio Olá que seus servidores do AD FS pertencem ao.
* **Conta de usuário de domínio** -este tipo de conta exige que você tooprovide uma senha e regularmente Olá atualização de senha quando a senha de saudação for alterada ou expira. Use essa opção apenas quando não há controladores de domínio do Windows Server 2012 no domínio Olá que seus servidores do AD FS pertencem a.

Se você tiver selecionado a Conta de Serviço Gerenciado de Grupo e se esse recurso nunca tiver sido usado no Active Directory, suas credenciais de Administrador Corporativo serão solicitadas. Essas credenciais são usadas tooinitiate repositório de chaves de saudação e habilitar o recurso de saudação no Active Directory.

> [!NOTE]
> Conexão do AD do Azure executa toodetect uma verificação se o serviço de saudação AD FS já está registrado como um SPN no domínio hello.  AD DS não permitirá toobe do SPN duplicado registrado uma vez.  Se um SPN duplicado for encontrado, não será capaz de tooproceed adicional até Olá SPN é removido.

![Conta de serviço do AD FS](./media/active-directory-aadconnect-get-started-custom/adfs5.png)

### <a name="select-hello-azure-ad-domain-that-you-wish-toofederate"></a>Selecionar domínio de saudação do AD do Azure que você deseja toofederate
Essa configuração é a relação de Federação Olá toosetup usado entre o AD FS e Azure AD. Ele configura tooAzure de tokens de segurança do AD FS tooissue AD e configura os tokens de saudação do AD do Azure tootrust dessa instância específica do AD FS. Esta página só permite tooconfigure um único domínio na instalação inicial do hello. Você pode configurar mais domínios mais tarde executando novamente o Azure AD Connect.

![Domínio do AD do Azure](./media/active-directory-aadconnect-get-started-custom/adfs6.png)

### <a name="verify-hello-azure-ad-domain-selected-for-federation"></a>Verificar o domínio de saudação do AD do Azure selecionado para federação
Quando você seleciona Olá toobe de domínio federado, Azure AD Connect fornece informações necessárias tooverify um domínio não verificado. Consulte [adicionar e verificar o domínio Olá](../active-directory-add-domain.md) como toouse essas informações.

![Domínio do AD do Azure](./media/active-directory-aadconnect-get-started-custom/verifyfeddomain.png)

> [!NOTE]
> Domínio do AD Connect tentativas tooverify Olá durante a saudação configurar estágio. Se você continuar tooconfigure sem adicionar os registros DNS necessários Olá, Assistente Olá não é capaz de toocomplete configuração de saudação.
>
>

## <a name="configure-and-verify-pages"></a>Configurar e verificar páginas
a configuração de saudação ocorre nesta página.

> [!NOTE]
> Antes de continuar a instalação e se você tiver configurado a federação, verifique se configurou a [Resolução de nomes para servidores de federação](active-directory-aadconnect-prerequisites.md#name-resolution-for-federation-servers).
>
>

![Tooconfigure pronto](./media/active-directory-aadconnect-get-started-custom/readytoconfigure2.png)

### <a name="staging-mode"></a>Modo de preparo
É possível toosetup um novo servidor de sincronização em paralelo com modo de preparo. É apenas toohave com suporte um servidor de sincronização exportando tooone diretório na nuvem hello. Mas se você quiser toomove em outro servidor, por exemplo um DirSync de execução, em seguida, você pode habilitar do Azure AD Connect em modo de preparo. Quando habilitada, sincronização de saudação do mecanismo de importação e sincronizar dados como normal, mas não exporta nada tooAzure anúncio ou. Olá recursos senha sincronização e a senha write-back são desabilitados no modo de preparo.

![Modo de preparo](./media/active-directory-aadconnect-get-started-custom/stagingmode.png)

No modo de preparo, ele é o mecanismo de sincronização de toohello toomake possíveis alterações necessárias e examinar quais são sobre toobe exportado. Quando a configuração de saudação correto, execute novamente o Assistente de instalação de saudação e desabilitar o modo de preparo. Dados agora são exportado tooAzure AD deste servidor. Verifique se toodisable Olá outro servidor no mesmo servidor de tempo de modo que apenas uma exportação de ativamente de saudação.

Para saber mais, confira [Modo de preparo](active-directory-aadconnectsync-operations.md#staging-mode).

### <a name="verify-your-federation-configuration"></a>Verificar a configuração de federação
Conexão do AD do Azure verifica as configurações de DNS Olá para você quando você clica Olá Verifique se o botão.

**Verificações de conectividade da intranet**

* Resolver o FQDN da federação: conexão do AD do Azure verifica se a federação Olá FQDN pode ser resolvida com a conectividade de tooensure DNS. Se o Azure AD Connect não pode resolver Olá FQDN, verificação de saudação falhará. Certifique-se de que um registro DNS está presente para o serviço de federação de saudação FQDN na verificação do pedido toosuccessfully Olá concluída.
* Registro DNS A: o Azure AD Connect verifica se há um registro A para seu serviço de Federação. Na ausência de saudação de um registro, a verificação da saudação falhará. Criar um um registro e não registro CNAME para o FQDN de Federação em ordem toosuccessfully concluir a verificação de saudação.

**Verificações de conectividade da extranet**

* Resolver o FQDN da federação: conexão do AD do Azure verifica se a federação Olá FQDN pode ser resolvida com a conectividade de tooensure DNS.

![Concluído](./media/active-directory-aadconnect-get-started-custom/completed.png)

![Verificar](./media/active-directory-aadconnect-get-started-custom/adfs7.png)

Além disso, execute Olá etapas de verificação a seguir:

* Validar que você pode entrar em um navegador de um computador ingressado no domínio na intranet Olá: conectar toohttps://myapps.microsoft.com e verificar Olá entrar com sua conta de login. conta de administrador Olá interna AD DS não está sincronizada e não pode ser usada para verificação.
* Valide que você pode entrar em um dispositivo de saudação à extranet. Em um computador doméstico ou um dispositivo móvel, conecte-se toohttps://myapps.microsoft.com e fornecer suas credenciais.
* Valide a entrada do cliente avançado. Conecte-se toohttps://testconnectivity.microsoft.com, escolha Olá **Office 365** Olá guia e escolha **Office 365 Single Sign-On teste**.

## <a name="next-steps"></a>Próximas etapas
Após a instalação de saudação, sair e entrar novamente tooWindows antes de usar o Gerenciador de serviço de sincronização ou Editor de regra de sincronização.

Agora que você tem o Azure AD Connect instalado, você pode [verificar a instalação do hello e atribuir licenças](active-directory-aadconnect-whats-next.md).

Saiba mais sobre esses recursos, que foram habilitados com instalação Olá: [impedir exclusões acidentais](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md) e [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md).

Saiba mais sobre esses tópicos comuns: [Agendador e como a sincronização tootrigger](active-directory-aadconnectsync-feature-scheduler.md).

Saiba mais sobre [Como integrar suas identidades locais ao Active Directory do Azure](active-directory-aadconnect.md).
