---
title: "a sincronização de senha aaaImplement com a sincronização do Azure AD Connect | Microsoft Docs"
description: "Fornece informações sobre como funciona a sincronização de senha e tooset backup."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 05f16c3e-9d23-45dc-afca-3d0fa9dbf501
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: billmath
ms.openlocfilehash: a0401640f2a4d914419ee4446f923bb3a972389d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-password-synchronization-with-azure-ad-connect-sync"></a>Implementar a sincronização de senha com o Azure AD Connect
Este artigo fornece informações que você precisa toosynchronize as senhas de usuário de uma instância no local do Active Directory instância tooa baseado em nuvem do Azure Active Directory (AD do Azure).

## <a name="what-is-password-synchronization"></a>O que é sincronização de senha
Olá a probabilidade de que você está impedido de realizar o seu trabalho devido tooa esquecido senha relacionado toohello número de senhas diferentes que você precisa tooremember. Olá senhas mais precisar tooremember, Olá superior Olá probabilidade tooforget um. Perguntas e chamadas sobre redefinições de senha e a demanda de outros problemas relacionados à senha Olá a maioria dos recursos de suporte técnico.

Sincronização de senha é que um recurso usado toosynchronize senhas de usuário de uma instância de tooa baseado em nuvem do Azure AD instância local do Active Directory.
Use esse recurso toosign em tooAzure AD serviços como o Office 365, Microsoft Intune, CRM Online e serviços de domínio de diretório ativo do Azure (Azure AD DS). Entrar no serviço toohello usando Olá mesma senha que você use toosign tooyour local instância do Active Directory.

![O que é o Azure AD Connect](./media/active-directory-aadconnectsync-implement-password-synchronization/arch1.png)

Reduzindo o número de saudação de senhas, os usuários precisam ter toojust toomaintain um. A sincronização de senha ajuda você a:

* Melhore a produtividade dos usuários hello.
* Reduzir os custos de assistência técnica.  

Além disso, se você decidir toouse [federação com os serviços de Federação do Active Directory (AD FS)](https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Configuring-AD-FS-for-user-sign-in-with-Azure-AD-Connect), você pode definir opcionalmente a sincronização de senha como um backup no caso de falha de infraestrutura do AD FS.

Sincronização de senha é um recurso de sincronização de diretório do extensão toohello implementado pela sincronização do Azure AD Connect. toouse a sincronização de senha em seu ambiente, você precisa:

* Instalar o Azure AD Connect.  
* Configurar a sincronização de diretórios entre sua instância do Active Directory local e a instância do Azure Active Directory.
* Habilitar a sincronização de senha.

Para saber mais, confira [Integrar suas identidades locais ao Azure Active Directory](active-directory-aadconnect.md).

> [!NOTE]
> Para obter mais detalhes sobre Azure Active Directory Domain Services, configurados para sincronização de senha e FIPS, veja “Sincronização de senha e FIPS” posteriormente neste artigo.
>
>

## <a name="how-password-synchronization-works"></a>Como a sincronização de senha funciona
Olá serviço de domínio do Active Directory armazena senhas na forma de saudação de uma representação do valor de hash de senha de usuário real hello. Um valor de hash é um resultado de uma função matemática unidirecional (Olá *algoritmo de hash*). Não há nenhum resultado do método toorevert saudação de uma versão de texto sem formatação toohello função unidirecional de uma senha. Você não pode usar um toosign de hash de senha na rede de local de tooyour.

toosynchronize sua senha, a sincronização do Azure AD Connect extrai o hash de senha de Olá instância do Active Directory local. O processamento de segurança adicional é aplicado toohello hash de senha antes que seja sincronizado toohello serviço de autenticação de Active Directory do Azure. As senhas são sincronizadas por usuário e em ordem cronológica.

fluxo de dados real de saudação do processo de sincronização de senha Olá é semelhante sincronização toohello de dados de usuário como DisplayName ou endereços de Email. No entanto, as senhas são sincronizadas mais frequentemente do que a janela de sincronização de diretório padrão Olá para outros atributos. o processo de sincronização de senha Olá é executado a cada 2 minutos. Não é possível modificar a frequência hello desse processo. Quando você sincronizar uma senha, substitua a senha de nuvem existente hello.

Olá primeiro que habilitar o recurso de sincronização de senha hello, ele executa uma sincronização inicial das senhas de saudação de todos os usuários em escopo. Você não pode definir explicitamente um subconjunto das senhas dos usuários que você deseja toosynchronize.

Quando você altera uma senha local, Olá atualizado senha é sincronizada, geralmente em questão de minutos.
o recurso de sincronização de senha Olá automaticamente repete as tentativas de sincronização com falha. Se ocorrer um erro durante uma tentativa de toosynchronize uma senha, um erro é registrado no seu visualizador de eventos.

sincronização de saudação de uma senha não tem impacto no usuário de saudação que está conectado no momento.
Sua sessão atual do serviço de nuvem imediatamente não é afetado por uma alteração de senha sincronizado que ocorre enquanto você está conectado no serviço de nuvem tooa. No entanto, quando o serviço de nuvem Olá exige que você tooauthenticate novamente, será necessário tooprovide sua nova senha.

Um usuário deve inserir suas credenciais corporativas tooAzure de tooauthenticate tempo um segundo AD, independentemente se ele estão conectados na rede corporativa tootheir. Esses padrão pode ser minimizado, no entanto, se o usuário Olá selecionará Olá Mantenha-me conectado na caixa de seleção (KMSI) na entrada. Essa seleção define um cookie de sessão que ignora a autenticação por um curto período. Comportamento KMSI pode ser habilitado ou desabilitado pelo administrador do AD do Azure hello.

> [!NOTE]
> Sincronização de senha só tem suporte para o usuário de tipo de objeto Olá no Active Directory. Não há suporte para o tipo de objeto iNetOrgPerson hello.

### <a name="detailed-description-of-how-password-synchronization-works"></a>Descrição detalhada de como funciona a sincronização de senha
a seguir Olá descreve detalhadamente como funciona a sincronização de senha entre o Active Directory e o AD do Azure.

![Fluxo da senha detalhado](./media/active-directory-aadconnectsync-implement-password-synchronization/arch3.png)


1. A cada dois minutos, agente de sincronização de senha Olá no servidor de conectar Olá AD solicitações hashes de senha armazenada (atributo unicodePwd de saudação) de um controlador de domínio por meio de saudação padrão [MS-DRSR](https://msdn.microsoft.com/library/cc228086.aspx) protocolo de replicação usado toosynchronize dados entre os controladores de domínio. conta de serviço Olá deve ter replicar alterações de diretório e permissões (por padrão na instalação) replicar Directory todas as alterações de AD Olá tooobtain hashes de senha.
2. Antes de enviar, Olá DC criptografa o hash de senha Olá MD4 usando uma chave que é um [MD5](http://www.rfc-editor.org/rfc/rfc1321.txt) hash da chave de sessão Olá RPC e um valor falso. Em seguida, envia o agente de sincronização de senha do hello resultado toohello via RPC. Olá DC também passa agente de sincronização de toohello salt hello usando o protocolo de replicação de saudação DC, para que agente Olá seja capaz de toodecrypt envelope de saudação.
3.  Depois que o agente de sincronização de senha Olá tem envelope criptografado Olá, ele usa [MD5CryptoServiceProvider](https://msdn.microsoft.com/library/System.Security.Cryptography.MD5CryptoServiceProvider.aspx) e Olá salt toogenerate um toodecrypt chave Olá recebida dados tooits back original MD4 formato. Em nenhum momento agente de sincronização de senha Olá ter senha de texto não criptografado de toohello de acesso. Olá uso do agente de sincronização de senha de MD5 é estritamente para compatibilidade de protocolo de replicação com hello controlador de domínio e é usado somente no local entre hello DC e o agente de sincronização de senha hello.
4.  Agente de sincronização de senha Olá expande bytes de too64 de hash de senha de binários de 16 bytes hello, primeiro converter Olá hash tooa 32 bytes cadeia de caracteres hexadecimal, e em seguida, converter essa cadeia de caracteres de volta para o binário com codificação UTF-16.
5.  Agente de sincronização de senha Olá adiciona um salt consiste em um salt 10 bytes, toohello 64 bytes binários toofurther proteger hash original hello.
6.  Agente de sincronização de senha Hello, em seguida, combina hash Olá MD4 mais salt e insere-o em Olá [PBKDF2](https://www.ietf.org/rfc/rfc2898.txt) função. 1000 iterações de saudação [HMAC-SHA256](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) algoritmo de hash com chave é usado. 
7.  Agente de sincronização de senha Olá leva o hash de 32 bytes resultante hello, concatena dois salt Olá Olá inúmeros SHA256 iterações tooit (para uso pelo AD do Azure) e transmite a cadeia de caracteres de saudação do Azure AD Connect tooAzure AD sobre SSL.</br> 
8.  Quando um usuário tenta toosign em tooAzure AD e insere sua senha, a senha de saudação é executado por meio de saudação MD4 mesmo + salt + PBKDF2 + HMAC-SHA256 processo. Se hash resultante Olá corresponder hash Olá armazenado no AD do Azure, o usuário de saudação inseriu a senha correta hello e é autenticado. 

>[!Note] 
>hash MD4 original de saudação não é transmitida tooAzure AD. Em vez disso, Olá hash SHA256 do hash MD4 original de saudação é transmitido. Como resultado, se o hash de saudação armazenado no AD do Azure é obtido, ele não pode ser usado em um ataque de passagem de hash local.

### <a name="how-password-synchronization-works-with-azure-active-directory-domain-services"></a>Como funciona a sincronização de senhas com o Azure Active Directory Domain Services
Você também pode usar toosynchronize de recurso de sincronização de senha Olá suas senhas locais muito[do Azure Active Directory Domain Services](../../active-directory-domain-services/active-directory-ds-overview.md). Nesse cenário, instância do Azure Active Directory Domain Services Olá autentica os usuários na nuvem Olá com todos os métodos de saudação disponíveis na sua instância do Active Directory local. experiência de Olá deste cenário é semelhante toousing Olá ferramenta de migração do Active Directory (ADMT) em um ambiente local.

### <a name="security-considerations"></a>Considerações de segurança
Durante a sincronização de senhas, versão de texto sem formatação Olá da sua senha não é exposto toohello recurso de sincronização de senha, tooAzure AD ou qualquer um dos serviços de saudação associado.

Autenticação de usuário ocorre no AD do Azure, em vez de em relação a instância do hello da organização do Active Directory. Se sua organização tiver preocupações sobre dados de senha de qualquer forma deixando Olá local, considere fatos Olá que Olá SHA256 dados de senha armazenados no AD do Azure – um hash de hash MD4 da original hello – é significativamente mais segura do que o que é armazenado no Active Directory. Além disso, porque esse hash SHA256 não puder ser descriptografada, ele não pode ser trazido de volta ambiente do Active Directory da organização toohello e apresentado como uma senha de usuário válido em um ataque de passagem de hash.





### <a name="password-policy-considerations"></a>Considerações sobre política de senha
Há dois tipos de políticas de senha que são afetadas ao habilitar a sincronização de senha:

* Política de complexidade de senha
* Política de expiração de senha

#### <a name="password-complexity-policy"></a>Política de complexidade de senha  
Quando a sincronização de senha está habilitada, políticas de complexidade de senha Olá na sua instância do Active Directory local substituem as políticas de complexidade na nuvem Olá para os usuários sincronizados. Você pode usar todas as senhas de saudação válido do seu tooaccess de instância local do Active Directory do Azure AD.

> [!NOTE]
> Senhas de usuários que são criados diretamente na nuvem Olá ainda são políticas de toopassword de assunto conforme definido na nuvem hello.

#### <a name="password-expiration-policy"></a>Política de expiração de senha  
Se um usuário estiver no escopo de saudação da sincronização de senha, a senha da conta de nuvem Olá é definida muito*nunca expirar*.

Você pode continuar toosign tooyour em serviços em nuvem usando uma senha sincronizada que expirou em seu ambiente local. Sua senha de nuvem é atualizada Olá da próxima vez que você alterar a senha Olá no ambiente de local de saudação.

#### <a name="account-expiration"></a>Expiração da conta
Se sua organização usa o atributo de accountExpires hello como parte do gerenciamento de contas de usuário, lembre-se de que esse atributo não é sincronizado tooAzure AD. Como resultado, uma conta expirada do Active Directory em um ambiente configurado para sincronização de senha ainda estará ativa no Azure AD. É recomendável que, se a conta de saudação expirou, uma ação de fluxo de trabalho deve disparar um script do PowerShell que desabilita a conta do AD do Azure do usuário hello. Por outro lado, quando a conta Olá estiver ativada, instância do AD do Azure Olá deve ser ativada.

### <a name="overwrite-synchronized-passwords"></a>Substituir senhas sincronizadas
Um administrador pode redefinir sua senha manualmente usando o Windows PowerShell.

Nesse caso, nova senha de saudação substitui sua senha sincronizada e todas as políticas de senha definidas na nuvem Olá são aplicadas toohello nova senha.

Se você alterar sua senha local novamente, Olá nova senha é sincronizada toohello nuvem, e ela substitui a senha Olá atualizado manualmente.

sincronização de saudação de uma senha não tem impacto sobre Olá usuário do Azure que está conectado. Sua sessão atual do serviço de nuvem imediatamente não é afetado por uma alteração de senha sincronizado que ocorre enquanto você está conectado no serviço de nuvem tooa. KMSI estende duração Olá dessa diferença. Quando o serviço de nuvem Olá exige que você tooauthenticate novamente, será necessário tooprovide sua nova senha.

### <a name="additional-advantages"></a>Vantagens adicionais

- Em geral, a sincronização de senha é mais simples tooimplement que um serviço de Federação. Ele não requer quaisquer servidores adicionais e elimina a dependência de um tooauthenticate usuários do serviço de Federação altamente disponível. 
- Sincronização de senha também pode ser habilitada no toofederation de adição. Ela pode ser usada como um fallback se seu serviço de federação sofrer uma interrupção.












## <a name="enable-password-synchronization"></a>Habilitar a sincronização de senha
Quando você instala o Azure AD Connect usando Olá **configurações expressas** opção, a sincronização de senha é habilitada automaticamente. Para obter mais detalhes, confira [Introdução ao Azure AD Connect usando configurações expressas](active-directory-aadconnect-get-started-express.md).

Se você usar configurações personalizadas ao instalar o Azure AD Connect, sincronização de senha está disponível na página de entrada do usuário de saudação. Para obter mais detalhes, confira [Instalação personalizada do Azure AD Connect](active-directory-aadconnect-get-started-custom.md).

![Habilitando a sincronização de senha](./media/active-directory-aadconnectsync-implement-password-synchronization/usersignin.png)

### <a name="password-synchronization-and-fips"></a>Sincronização de senha e FIPS
Se seu servidor foi bloqueado de acordo com o tooFederal Information Processing Standard (FIPS), em seguida, MD5 será desabilitada.

**tooenable MD5 para a sincronização de senha, execute Olá etapas a seguir:**

1. Vá too%programfiles%\Azure AD Sync\Bin.
2. Abra miiserver.exe.config.
3. Vá para toohello configuração/runtime nó final de saudação do arquivo hello.
4. Adicione Olá seguinte nó:`<enforceFIPSPolicy enabled="false"/>`
5. Salve suas alterações.

Para referência, essa captura mostra como deve ser a aparência:

```
    <configuration>
        <runtime>
            <enforceFIPSPolicy enabled="false"/>
        </runtime>
    </configuration>
```

Para saber mais sobre segurança e FIPS, veja [Sincronização de senha do AAD, criptografia e conformidade FIPS](https://blogs.technet.microsoft.com/enterprisemobility/2014/06/28/aad-password-sync-encryption-and-fips-compliance/).

## <a name="troubleshoot-password-synchronization"></a>Solucionar problemas de sincronização de senha
Caso tenha problemas com a sincronização de senha, veja [Solucionar problemas de sincronização de senha](active-directory-aadconnectsync-troubleshoot-password-synchronization.md).

## <a name="next-steps"></a>Próximas etapas
* [Sincronização do Azure AD Connect: personalizando opções de sincronização](active-directory-aadconnectsync-whatis.md)
* [Integração de suas identidades locais com o Active Directory do Azure](active-directory-aadconnect.md)
