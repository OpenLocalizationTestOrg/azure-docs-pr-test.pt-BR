---
title: "Azure AD Connect: contas e permissões | Microsoft Docs"
description: "Este tópico descreve as contas de saudação usada e criado e as permissões necessárias."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.reviewer: cychua
ms.assetid: b93e595b-354a-479d-85ec-a95553dd9cc2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: billmath
ms.openlocfilehash: 70a7013e0353d74714ec8a3ff54b3e811789a0b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-accounts-and-permissions"></a>Azure AD Connect: contas e permissões
Assistente de instalação de conectar-se de saudação do AD do Azure oferece dois caminhos diferentes:

* Em configurações do Express, o Assistente de saudação requer mais privilégios.  Isso é para que ele pode configurar a sua configuração facilmente, sem exigir que os usuários toocreate ou configurar permissões.
* Em configurações personalizadas, o Assistente de saudação oferece mais opções de. No entanto, há algumas situações em que é necessário tooensure você tem as permissões corretas Olá por conta própria.

## <a name="related-documentation"></a>documentação relacionada
Se você não leu documentação Olá em [integrando suas identidades locais ao Active Directory do Azure](../active-directory-aadconnect.md), hello tabela a seguir fornece links toorelated tópicos.

|Tópico |Link|  
| --- | --- |
|Baixar o Azure AD Connect | [Baixar o Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771)|
|Instalar usando as Configurações expressas | [Instalação expressa do Azure AD Connect](./active-directory-aadconnect-get-started-express.md)|
|Instalar usando Configurações personalizadas | [Instalação personalizada do Azure AD Connect](./active-directory-aadconnect-get-started-custom.md)|
|Atualização do DirSync | [Atualizar a partir da ferramenta de sincronização do AD do Azure (DirSync)](./active-directory-aadconnect-dirsync-upgrade-get-started.md)|
|Após a instalação | [Verificar a instalação do hello e atribuir licenças](active-directory-aadconnect-whats-next.md)|

## <a name="express-settings-installation"></a>Instalação das configurações expressas
Em configurações do Express, o Assistente de instalação Olá solicita credenciais de administrador de empresa do AD DS.  Isso é assim para que o Active Directory local possa ser configurado com as permissões necessárias para o Azure AD Connect. Se você estiver atualizando do DirSync, as credenciais do hello AD DS Enterprise Admins são tooreset usado por senha Olá Olá conta usada pelo DirSync. Você também precisa de credenciais de Administrador Global do Azure AD.

| Página do assistente | Credenciais coletadas | Permissões necessárias | Usadas para |
| --- | --- | --- | --- |
| N/D |Assistente de instalação do usuário em execução Olá |Administrador de servidor local Olá |<li>Cria Olá conta local que é usada como Olá [conta de serviço do mecanismo de sincronização](#azure-ad-connect-sync-service-account). |
| Conecte-se tooAzure AD |Credenciais de diretório do AD do Azure |Função de administrador global no AD do Azure |<li>Habilitando a sincronização no diretório do AD do Azure hello.</li>  <li>Criação de saudação [conta do Azure AD](#azure-ad-service-account) que é usada para operações de sincronização em andamento no AD do Azure.</li> |
| Conecte-se tooAD DS |Credenciais do Active Directory local |Membro do grupo de EA (administradores corporativos) Olá no Active Directory |<li>Cria um [conta](#active-directory-account) no Active Directory e concede permissões tooit. Isso conta criada é usadas informações do diretório tooread e gravação durante a sincronização.</li> |

### <a name="enterprise-admin-credentials"></a>Credenciais de administrador corporativo
Essas credenciais são usadas somente durante a instalação de saudação e não são usadas após a instalação de saudação. Olá administrador corporativo, Olá administrador de domínio deve se certificar de permissões de saudação no Active Directory podem ser definidas em todos os domínios.

### <a name="global-admin-credentials"></a>Credenciais de administrador global
Essas credenciais são usadas somente durante a instalação de saudação e não são usadas após a instalação de saudação. É usado toocreate Olá [conta do Azure AD](#azure-ad-service-account) usados para sincronizar alterações tooAzure AD. conta de saudação também permite sincronização como um recurso no AD do Azure.

### <a name="permissions-for-hello-created-ad-ds-account-for-express-settings"></a>Permissões para Olá AD DS conta criada para as configurações expressas
Olá [conta](#active-directory-account) criado para leitura e gravação tooAD DS tem Olá as seguintes permissões quando criada pelas configurações express:

| Permissão | Usado para |
| --- | --- |
| <li>Replicar alterações de diretório</li><li>Replicar todas as alterações de diretório |Sincronização de senha |
| Ler/Gravar todas as propriedades Usuário |Importação e Exchange híbrido |
| Ler/Gravar todas as propriedades iNetOrgPerson |Importação e Exchange híbrido |
| Ler/Gravar todas as propriedades Grupo |Importação e Exchange híbrido |
| Ler/Gravar todas as propriedades Contato |Importação e Exchange híbrido |
| Redefinir senha |Preparação para habilitar write-back de senha |

## <a name="custom-settings-installation"></a>Instalação de configurações personalizadas
Azure AD Connect versão 1.1.524.0 e posterior tem Assistente do hello opção toolet Olá AD do Azure Connect criar hello conta usada tooconnect tooActive Directory.  Versões anteriores exigem que a conta de saudação é criada antes da instalação de saudação. permissões de saudação deve conceder a essa conta podem ser encontradas na [criar hello AD DS conta](#create-the-ad-ds-account). 

| Página do assistente | Credenciais coletadas | Permissões necessárias | Usadas para |
| --- | --- | --- | --- |
| N/D |Assistente de instalação do usuário em execução Olá |<li>Administrador de servidor local Olá</li><li>Se usar um servidor SQL completo, o usuário de saudação deve ser administrador do sistema (SA) no SQL</li> |Por padrão, cria a conta de local de saudação que é usada como Olá [conta de serviço do mecanismo de sincronização](#azure-ad-connect-sync-service-account). conta Olá é criada somente quando Olá administrador não especifica uma conta específica. |
| Instalar serviços de sincronização, opção de conta de serviço |Credenciais de conta de usuário local ou AD |Usuário, as permissões são concedidas pelo Assistente de instalação de saudação |Se Olá administrador especifica uma conta, essa conta é usada como conta de serviço Olá para serviço de sincronização de saudação. |
| Conecte-se tooAzure AD |Credenciais de diretório do AD do Azure |Função de administrador global no AD do Azure |<li>Habilitando a sincronização no diretório do AD do Azure hello.</li>  <li>Criação de saudação [conta do Azure AD](#azure-ad-service-account) que é usada para operações de sincronização em andamento no AD do Azure.</li> |
| Conectar seus diretórios |Credenciais do Active Directory para cada floresta que é conectado tooAzure AD local |permissões de saudação dependem de quais recursos você habilita e pode ser encontradas no [criar conta Olá AD DS](#create-the-ad-ds-account) |Essa conta é usadas informações do diretório tooread e gravação durante a sincronização. |
| Servidores do AD FS |Para cada servidor na lista de hello, Assistente de saudação coleta credenciais quando Olá credenciais de logon do usuário Olá executando o Assistente de saudação tooconnect insuficiente |Administrador de domínio |Instalação e configuração da função de servidor Olá AD FS. |
| Servidores proxy de aplicativo Web |Para cada servidor na lista de hello, Assistente de saudação coleta credenciais quando Olá credenciais de logon do usuário Olá executando o Assistente de saudação tooconnect insuficiente |Administrador local no computador de destino Olá |Instalação e configuração da função de servidor WAP. |
| Credenciais de confiança de proxy |Credenciais de relação de confiança de serviço de Federação (Olá credenciais Olá proxy usa tooenroll para um certificado de confiança da saudação FS |Conta de domínio que seja um administrador local do servidor do hello AD FS |Registro inicial de certificado de confiança FS-WAP. |
| Página da conta de serviço do AD FS, "Usar uma opção de conta de usuário de domínio" |Credenciais de conta de usuário do AD |Usuário de domínio |conta de usuário de saudação AD cujas credenciais são fornecidas é usada como conta de logon de saudação do serviço de saudação do AD FS. |

### <a name="create-hello-ad-ds-account"></a>Criar conta Olá AD DS
Olá conta especificada na Olá **conectar seus diretórios** página deve estar presente no tooinstallation anterior do Active Directory.  Ele também deve ter permissões de saudação necessárias concedidas. Assistente de instalação de saudação não verifica permissões hello e quaisquer problemas são encontrados somente durante a sincronização.

Quais permissões você precisa depende de recursos opcionais de saudação habilitar. Se você tiver vários domínios, permissões de saudação devem ser concedidas para todos os domínios na floresta de saudação. Se você não habilitar esses recursos, Olá padrão **usuário de domínio** permissões são suficientes.

| Recurso | Permissões |
| --- | --- |
| Recurso msDS-ConsistencyGuid |Permissões de gravação toohello msDS-ConsistencyGuid atributo documentado em [conceitos de Design - usando msDS-ConsistencyGuid como sourceAnchor](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor). | 
| Sincronização de senha |<li>Replicar alterações de diretório</li>  <li>Replicar todas as alterações de diretório |
| Implantação híbrida do Exchange |Gravar permissões toohello atributos documentados em [write-back do Exchange híbrido](active-directory-aadconnectsync-attributes-synchronized.md#exchange-hybrid-writeback) para usuários, grupos e contatos. |
| Pasta pública do Exchange Mail |Atributos de toohello de permissões de leitura documentados em [pasta pública do Exchange Mail](active-directory-aadconnectsync-attributes-synchronized.md#exchange-mail-public-folder) para pastas públicas. | 
| Write-back de senha |Gravar permissões toohello atributos documentados em [guia de Introdução ao gerenciamento de senhas](../active-directory-passwords-writeback.md) para os usuários. |
| Write-back de dispositivo |Permissões concedidas com um script do PowerShell, conforme descrito em [Write-back do dispositivo](active-directory-aadconnect-feature-device-writeback.md). |
| Write-back de grupo |Ler, criar, atualizar e excluir objetos de grupo para **grupos do Office 365** sincronizados.  Para saber mais, confira [Write-back de grupo](active-directory-aadconnect-feature-preview.md#group-writeback).|

## <a name="upgrade"></a>Atualizar
Quando você atualiza de uma versão do Azure AD Connect tooa nova versão, você precisa Olá as seguintes permissões:

| Principal | Permissões necessárias | Usadas para |
| --- | --- | --- |
| Assistente de instalação do usuário em execução Olá |Administrador de servidor local Olá |Binários de atualização. |
| Assistente de instalação do usuário em execução Olá |Membro do ADSyncAdmins |Faça as alterações tooSync regras e outras configurações. |
| Assistente de instalação do usuário em execução Olá |Se você usar um servidor SQL completo: DBO (ou semelhante) do banco de dados de mecanismo de sincronização Olá |Fazer alterações no nível de banco de dados, como a atualização de tabelas com novas colunas. |

## <a name="more-about-hello-created-accounts"></a>Mais sobre Olá criada contas
### <a name="active-directory-account"></a>Conta do Active Directory
Se você usar configurações expressas, uma conta será criada no Active Directory e será usada para sincronização. Olá criado conta está localizada no domínio raiz da floresta Olá no contêiner de usuários hello e tem o nome prefixado com **MSOL_**. Olá conta é criada com uma senha longa complexa que não expire. Se você tiver uma política de senha em seu domínio, verifique se senhas longas e complexas são permitidas para esta conta.

![Conta do AD](./media/active-directory-aadconnect-accounts-permissions/adsyncserviceaccount.png)

Se você usar configurações personalizadas, são responsáveis por criar conta Olá antes de iniciar a instalação de saudação.

### <a name="azure-ad-connect-sync-service-account"></a>Conta de serviço de sincronização do Azure AD Connect
serviço de sincronização de saudação pode ser executado em contas diferentes. Ele pode ser executado em uma VSA (**conta de serviço virtual**), uma gMSA/sMSA (**conta de serviço gerenciado de grupo**) ou então uma conta de usuário regular. Opções de saudação com suporte foram alteradas com hello 2017 versão de abril de conectar-se ao fazer uma nova instalação. Se você atualizar de uma versão anterior do Azure AD Connect, essas opções adicionais não estarão disponíveis.

| Tipo de conta | Opção de instalação | Descrição |
| --- | --- | --- |
| [Conta de Serviço Virtual](#virtual-service-account) | Expressa e personalizada, abril de 2017 e posterior | Isso é usada para todas as instalações do express, exceto para instalações em um controlador de domínio de opção de saudação. Para personalizar, é saudação padrão opção, a menos que outra opção é usada. |
| [Conta de Serviço Gerenciado de Grupo](#group-managed-service-account) | Personalizada, abril de 2017 e posterior | Se você usar um SQL server remoto, é recomendável toouse um grupo de conta de serviço gerenciado. |
| [Conta de usuário](#user-account) | Expressa e personalizada, abril de 2017 e posterior | Uma conta de usuário prefixada com AAD_ só é criada durante a instalação quando instalada no Windows Server 2008 e quando instalada em um controlador de domínio. |
| [Conta de usuário](#user-account) | Expressa e personalizada, março de 2017 e versões anteriores | Uma conta local prefixada com AAD_ é criada durante a instalação. Ao usar a instalação personalizada, outra conta pode ser especificada. |

Se você usar conectar com uma compilação de março de 2017 ou anterior, em seguida, você não deve redefinir a senha de saudação na conta de serviço Olá desde o Windows destrói as chaves de criptografia Olá por motivos de segurança. Você não pode alterar Olá conta tooany outra conta sem reinstalar o Azure AD Connect. Se você atualizar tooa build de 2017 abril ou posteriormente, em seguida, é toochange com suporte Olá senha na conta de serviço de saudação, mas não conta Olá usada.

> [!Important]
> Você só pode definir a conta de serviço de saudação na primeira instalação. Não é suporte para a conta de serviço toochange Olá após a instalação de saudação.

Essa é uma tabela de padrão de saudação, recomendado, e opções com suporte para Olá sincronizar a conta de serviço.

Legenda:

- **Negrito** indica a opção padrão de saudação e na saudação de maioria dos casos a opção recomendada.
- *Itálico* indica Olá recomendado opção quando não é saudação padrão opção.
- 2008 – opção padrão quando instalado no Windows Server 2008
- Não negrito – opção com suporte
- Conta local - conta de usuário Local no servidor de saudação
- Conta do domínio – conta de usuário do domínio
- sMSA – [conta de serviço gerenciado autônomo](https://technet.microsoft.com/library/dd548356.aspx)
- gMSA – [conta de serviço gerenciado de grupo](https://technet.microsoft.com/library/hh831782.aspx)

| | LocalDB</br>Express | LocalDB/LocalSQL</br>Personalizado | SQL remoto</br>Personalizado |
| --- | --- | --- | --- |
| **computador autônomo/de grupo de trabalho** | Sem suporte | **VSA**</br>Conta local (2008)</br>Conta local |  Sem suporte |
| **computador associado ao domínio** | **VSA**</br>Conta local (2008) | **VSA**</br>Conta local (2008)</br>Conta local</br>Conta do domínio</br>sMSA, gMSA | **gMSA**</br>Conta do domínio |
| **Controlador de domínio** | **Conta do domínio** | *gMSA*</br>**Conta do domínio**</br>sMSA| *gMSA*</br>**Conta do domínio**|

#### <a name="virtual-service-account"></a>Conta de serviço virtual
Uma conta de serviço virtual é um tipo especial de conta que não tem uma senha e é gerenciada pelo Windows.

![VSA](./media/active-directory-aadconnect-accounts-permissions/aadsyncvsa.png)

Olá VSA é pretendido toobe usada com cenários em que o mecanismo de sincronização hello e SQL têm Olá mesmo servidor. Se você usar o SQL remoto, é recomendável toouse um [conta de serviço gerenciado do grupo](#managed-service-account) em vez disso.

Este recurso requer o Windows Server 2008 R2 ou posterior. Se você instala o Azure Connect AD no Windows Server 2008, instalação Olá reverterá toousing um [conta de usuário](#user-account) em vez disso.

#### <a name="group-managed-service-account"></a>Conta de serviço gerenciado de grupo
Se você usar um SQL server remoto, é recomendável toousing um **conta de serviço gerenciado de grupo**. Para obter mais informações sobre como tooprepare seu Active Directory para a conta de serviço gerenciado de grupo, consulte [grupo Managed Service Accounts Overview](https://technet.microsoft.com/library/hh831782.aspx).

toouse essa opção em Olá [instalar os componentes necessários](active-directory-aadconnect-get-started-custom.md#install-required-components) página, selecione **usar uma conta de serviço existente**e selecione **conta de serviço gerenciado**.  
![VSA](./media/active-directory-aadconnect-accounts-permissions/serviceaccount.png)  
Também é suportado toouse um [conta de serviço gerenciado de autônomo](https://technet.microsoft.com/library/dd548356.aspx). No entanto, eles podem ser usados somente no computador local hello e não há nenhum benefício toouse-los pela conta de serviço virtual saudação padrão.

Este recurso requer o Windows Server 2012 ou posterior. Se você precisar toouse um sistema operacional mais antigo e usa o SQL remoto, você deve usar um [conta de usuário](#user-account).

#### <a name="user-account"></a>Conta de usuário
Uma conta de serviço local é criada pelo Assistente de instalação da saudação (a menos que você especifique Olá conta toouse em configurações personalizadas). conta de saudação é prefixada **AAD_** e usado para toorun de serviço de sincronização real hello como. Se você instalar o Azure AD Connect em um controlador de domínio, conta de saudação é criada no domínio hello. Olá **AAD_** conta de serviço deve estar localizada em domínio Olá se:
   - você usa um servidor remoto executando o SQL Server
   - você usa um proxy que exija autenticação

![Conta de serviço de sincronização](./media/active-directory-aadconnect-accounts-permissions/syncserviceaccount.png)

Olá conta é criada com uma senha longa complexa que não expire.

Essa conta é usado toostore senhas Olá Olá outras contas de forma segura. Essas outras senhas de contas são armazenadas criptografadas no banco de dados de saudação. as chaves privadas de Olá Olá para chaves de criptografia são protegidas com criptografia de chave secreta de serviços criptográficos hello usando a API de proteção de dados do Windows (DPAPI).

Se você usar um servidor SQL completo, conta de serviço de saudação é Olá DBO do banco de dados de saudação criado para o mecanismo de sincronização de saudação. serviço de saudação não funcionará conforme o esperado com quaisquer outras permissões. Um logon do SQL também é criado.

Olá conta também recebe permissões toofiles, chaves do registro e outros toohello de objetos relacionados mecanismo de sincronização.

### <a name="azure-ad-service-account"></a>Conta de serviço do AD do Azure
Uma conta no AD do Azure é criada para uso do serviço de sincronização hello. Essa conta pode ser identificada com seu nome de exibição.

![Conta do AD](./media/active-directory-aadconnect-accounts-permissions/aadsyncserviceaccount.png)

saudação de nome da conta de saudação do servidor de saudação é usada no podem ser identificados na segunda parte Olá Olá do nome de usuário. Imagem de Olá, o nome do servidor de saudação é FABRIKAMCON. Se você tiver servidores de teste, cada servidor terá sua própria conta.

conta de serviço de saudação é criada com uma senha longa complexa que não expire. Ele recebe uma função especial **contas de sincronização de diretório** que tenha somente permissões tooperform directory tarefas de sincronização. Essa função interna especial não pode ser concedida fora do Assistente de conexão do AD do Azure hello. portal do Azure Hello mostra essa conta com função hello **usuário**.

Há um limite de 20 contas de serviço de sincronização no Azure AD. lista de saudação tooget existentes do AD do Azure de contas de serviço no AD do Azure, execute Olá seguinte cmdlet do PowerShell do Azure AD:`Get-AzureADDirectoryRole | where {$_.DisplayName -eq "Directory Synchronization Accounts"} | Get-AzureADDirectoryRoleMember`

tooremove não usada contas de serviço do AD do Azure, executadas Olá seguinte cmdlet do PowerShell do Azure AD:`Remove-AzureADUser -ObjectId <ObjectId-of-the-account-you-wish-to-remove>`

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre [Como integrar suas identidades locais ao Active Directory do Azure](../active-directory-aadconnect.md).
