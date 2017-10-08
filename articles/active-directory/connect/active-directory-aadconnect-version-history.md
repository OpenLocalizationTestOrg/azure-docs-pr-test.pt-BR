---
title: "Azure AD Connect: histórico de liberação de versão | Microsoft Docs"
description: "Este artigo lista todas as versões do Azure AD Connect e do Azure AD Sync"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: ef2797d7-d440-4a9a-a648-db32ad137494
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b55e0f2d426e34ceef9869d5a6d1b0956d8bd076
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-version-release-history"></a>Azure AD Connect: histórico de lançamento de versão
equipe do Azure Active Directory (AD do Azure) Olá atualiza regularmente o Azure AD Connect com novos recursos e funcionalidade. Nem todas as adições são aplicáveis tooall públicos.

Este artigo é projetado toohelp você manter o controle de versões de saudação que foram lançadas e toounderstand se é necessário a versão mais recente do tooupdate toohello ou não.

Esta é uma lista de tópicos relacionados:


Tópico |  Detalhes
--------- | --------- |
Etapas tooupgrade do Azure AD Connect | Métodos diferentes muito[atualização do toohello versão anterior mais recente](active-directory-aadconnect-upgrade-previous-version.md) versão do Azure AD Connect.
Permissões necessárias | Para as permissões necessárias tooapply uma atualização, consulte [contas e permissões](./active-directory-aadconnect-accounts-permissions.md#upgrade).
Baixar| [Baixar o Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771).

## <a name="115610"></a>1.1.561.0
Status: 23 de julho de 2017

### <a name="azure-ad-connect"></a>Azure AD Connect

#### <a name="fixed-issue"></a>Problema corrigido

* Corrigido um problema que causou a regra de sincronização de fora da caixa de hello "Out tooAD - ImmutableId do usuário" toobe removido:

  * problema de saudação ocorre quando o Azure AD Connect é atualizado, ou hello quando a opção de tarefa *configuração de sincronização de atualização* hello Azure AD Connect assistente é usado tooupdate AD do Azure Connect configuração da sincronização.
  
  * Esta regra de sincronização é aplicável toocustomers que habilitaram Olá [msDS-ConsistencyGuid como recurso de âncora de origem](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor). Esse recurso foi introduzido na versão 1.1.524.0 e posteriores. Quando a regra de sincronização de saudação é removida, o Azure AD Connect não pode preencher local atributo do ms-DS-ConsistencyGuid AD com hello valor do atributo ObjectGuid. Isso não impede que novos usuários sejam provisionados no Azure AD.
  
  * correção de saudação garante que essa regra de sincronização de saudação não será removida durante a atualização, ou durante a alteração de configuração, como Olá está ativado. Para clientes existentes que foram afetados por esse problema, corrija Olá também garante que essa regra de sincronização Olá é adicionada novamente após a atualização de versão toothis do Azure AD Connect.

* Corrigido um problema que faz com que as regras de sincronização de fora da caixa valor de precedência de toohave é menor que 100:

  * Em geral, os valores de precedência de 0 a 99 são reservados para regras de sincronização personalizadas. Durante a atualização, os valores de precedência de Olá para regras de sincronização de fora da caixa são atualizados tooaccommodate alterações nas regras de sincronização. Devido a problema toothis, regras de sincronização de fora da caixa podem ser atribuídas o valor de precedência que for menor que 100.
  
  * correção de saudação impede que o problema de saudação que ocorrem durante a atualização. No entanto, ele não restaura os valores de precedência de saudação para clientes existentes que foram afetados pelo problema hello. Uma correção separada será fornecida em toohelp futura de saudação com restauração de saudação.

* Corrigido um problema em que hello [tela de domínio e a filtragem de unidade Organizacional](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) de saudação do Azure AD Connect assistente está mostrando *sincronizar todos os domínios e OUs* opção conforme selecionado, mesmo que a filtragem baseada em unidade Organizacional é habilitado.

*   Corrigido um problema que causou Olá [tela Configurar partições de diretório](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) em Olá Synchronization Service Manager tooreturn um erro se hello *atualização* botão é clicado. mensagem de erro Olá *"foi encontrado um erro ao atualizar domínios: não é possível toocast objeto do tipo 'System.Collections.ArrayList' tootype ' Microsoft.DirectoryServices.MetadirectoryServices.UI.PropertySheetBase.MaPropertyPages.PartitionObject."* Olá erro ocorre quando o novo domínio do AD foi adicionado tooan floresta existente do AD e você está tentando tooupdate do Azure AD Connect usando Olá botão Atualizar.

#### <a name="new-features-and-improvements"></a>Novos recursos e aprimoramentos

* [Recurso de atualização automática](active-directory-aadconnect-feature-automatic-upgrade.md) foi expandido toosupport clientes com hello configurações a seguir:
  * Você habilitou o recurso de write-back de dispositivo hello.
  * Você habilitou o recurso de write-back de grupo hello.
  * Olá instalação não é um configurações Express ou uma atualização do DirSync.
  * Você tem mais de 100.000 objetos no metaverso hello.
  * Você está se conectando toomore de uma floresta. A configuração expressa só se conecta a floresta tooone.
  * Olá conta de conector do AD não é saudação padrão MSOL_ conta mais.
  * servidor de saudação é definido toobe no modo de preparo.
  * Você habilitou o recurso de write-back de usuário hello.
  
  >[!NOTE]
  >expansão de escopo de saudação do recurso de atualização automática de saudação afeta os clientes com o Azure AD Connect compilação 1.1.105.0 e depois. Se você não quiser que seu toobe do servidor do Azure AD Connect atualizado automaticamente, você deve executar a seguinte cmdlet no seu servidor do Azure AD Connect: `Set-ADSyncAutoUpgrade -AutoUpgradeState disabled`. Para obter mais informações sobre habilitação/desabilitação da atualização automática, consulte tooarticle [do Azure AD Connect: a atualização automática](active-directory-aadconnect-feature-automatic-upgrade.md).

## <a name="115580"></a>1.1.558.0
Status: não será liberada. As alterações deste build estão incluídas na versão 1.1.561.0.

### <a name="azure-ad-connect"></a>Azure AD Connect

#### <a name="fixed-issue"></a>Problema corrigido

* Corrigido um problema que causou a saudação out-of-box sincronização regra "Out tooAD - ImmutableId do usuário" toobe removidos quando configuração filtragem baseada em unidade Organizacional é atualizada. Esta regra de sincronização é necessária para Olá [msDS-ConsistencyGuid como recurso de âncora de origem](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor).

* Corrigido um problema em que hello [tela de domínio e a filtragem de unidade Organizacional](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) de saudação do Azure AD Connect assistente está mostrando *sincronizar todos os domínios e OUs* opção conforme selecionado, mesmo que a filtragem baseada em unidade Organizacional é habilitado.

*   Corrigido um problema que causou Olá [tela Configurar partições de diretório](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) em Olá Synchronization Service Manager tooreturn um erro se hello *atualização* botão é clicado. mensagem de erro Olá *"foi encontrado um erro ao atualizar domínios: não é possível toocast objeto do tipo 'System.Collections.ArrayList' tootype ' Microsoft.DirectoryServices.MetadirectoryServices.UI.PropertySheetBase.MaPropertyPages.PartitionObject."* Olá erro ocorre quando o novo domínio do AD foi adicionado tooan floresta existente do AD e você está tentando tooupdate do Azure AD Connect usando Olá botão Atualizar.

#### <a name="new-features-and-improvements"></a>Novos recursos e aprimoramentos

* [Recurso de atualização automática](active-directory-aadconnect-feature-automatic-upgrade.md) foi expandido toosupport clientes com hello configurações a seguir:
  * Você habilitou o recurso de write-back de dispositivo hello.
  * Você habilitou o recurso de write-back de grupo hello.
  * Olá instalação não é um configurações Express ou uma atualização do DirSync.
  * Você tem mais de 100.000 objetos no metaverso hello.
  * Você está se conectando toomore de uma floresta. A configuração expressa só se conecta a floresta tooone.
  * Olá conta de conector do AD não é saudação padrão MSOL_ conta mais.
  * servidor de saudação é definido toobe no modo de preparo.
  * Você habilitou o recurso de write-back de usuário hello.
  
  >[!NOTE]
  >expansão de escopo de saudação do recurso de atualização automática de saudação afeta os clientes com o Azure AD Connect compilação 1.1.105.0 e depois. Se você não quiser que seu toobe do servidor do Azure AD Connect atualizado automaticamente, você deve executar a seguinte cmdlet no seu servidor do Azure AD Connect: `Set-ADSyncAutoUpgrade -AutoUpgradeState disabled`. Para obter mais informações sobre habilitação/desabilitação da atualização automática, consulte tooarticle [do Azure AD Connect: a atualização automática](active-directory-aadconnect-feature-automatic-upgrade.md).

## <a name="115570"></a>1.1.557.0
Status: julho de 2017

>[!NOTE]
>Esta compilação não está disponível toocustomers por meio do recurso de conectar-se a atualização automática de saudação do AD do Azure.

### <a name="azure-ad-connect"></a>Azure AD Connect

#### <a name="fixed-issue"></a>Problema corrigido
* Corrigido um problema com o cmdlet Olá Initialize-ADSyncDomainJoinedComputerSync que causou o domínio verificado do hello configurado no hello existente serviço conexão ponto objeto toobe alterado, mesmo que ele ainda é um domínio válido. Esse problema ocorre quando seu locatário do AD do Azure tem mais de um domínios verificados que podem ser usado para configurar o ponto de conexão de serviço de saudação.

#### <a name="new-features-and-improvements"></a>Novos recursos e aprimoramentos
* O Write-back de Senha já está disponível para versão prévia com a nuvem do Microsoft Azure Governamental e com o Microsoft Cloud Alemanha. Para obter mais informações sobre o suporte do Azure AD Connect Olá diferentes para instâncias de serviço, consulte tooarticle [do Azure AD Connect: considerações especiais para instâncias](active-directory-aadconnect-instances.md).

* Olá Initialize-ADSyncDomainJoinedComputerSync cmdlet agora tem um novo parâmetro opcional nomeado AzureADDomain. Esse parâmetro permite especificar qual verificado toobe de domínio usada para configurar o ponto de conexão de serviço de saudação.

### <a name="pass-through-authentication"></a>Autenticação de Passagem

#### <a name="new-features-and-improvements"></a>Novos recursos e aprimoramentos
* nome de saudação do agente de saudação necessário para autenticação de passagem foi alterada de *conector de Proxy de aplicativo do Microsoft Azure AD* muito*agente do Microsoft Azure AD Connect autenticação*.

* A habilitação da Autenticação de passagem não habilita a Sincronização de hash de senha por padrão.


## <a name="115530"></a>1.1.553.0
Status: junho de 2017

> [!IMPORTANT]
> Foram introduzidas alterações de regra de esquema e sincronização nesse build. O Serviço de Sincronização do Azure AD Connect disparará as etapas de Importação completa e Sincronização completa após a atualização. Detalhes das alterações de saudação são descritos abaixo. tootemporarily adiar etapas de importação completa e sincronização completa após a atualização, consulte tooarticle [como toodefer completo sincronização após a atualização](active-directory-aadconnect-upgrade-previous-version.md#how-to-defer-full-synchronization-after-upgrade).
>
>

### <a name="azure-ad-connect-sync"></a>Sincronização do Azure AD Connect

#### <a name="known-issue"></a>Problema conhecido
* Há um problema que afeta os clientes que estejam usando a [filtragem baseada em UO](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) com a sincronização do Azure AD Connect. Quando você navega toohello [página de domínio e a filtragem de UO](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) no Assistente para conectar-se de saudação do AD do Azure, é esperado Olá comportamento a seguir:
  * Se a filtragem baseada em unidade Organizacional é habilitado, Olá **de sincronização selecionados domínios e unidades organizacionais** opção é selecionada.
  * Caso contrário, Olá **sincronizar todos os domínios e OUs** opção é selecionada.

Olá, problema que surge é que hello **sincronizar todos os domínios e OUs opção** sempre é selecionado quando você executa o Assistente de saudação.  Isso ocorre mesmo se a filtragem baseada em UO tiver sido configurada anteriormente. Antes de salvar as alterações de configuração do AAD Connect, verifique se Olá **sincronizar selecionados domínios e OUs está selecionada** e verifique se todas as UOs necessário toosynchronize estão habilitadas novamente. Caso contrário, a filtragem baseada em UO será desabilitada.

#### <a name="fixed-issues"></a>Problemas corrigidos

* Corrigido um problema com write-back de senha que permite que um tooreset de administrador do AD do Azure senha Olá local AD conta de usuário privilegiado. problema de Olá ocorre quando o Azure AD Connect é concedido a permissão de redefinição de senha Olá conta Olá privilegiado. Olá problema é corrigido nesta versão do Azure AD Connect não permitindo que um tooreset de administrador do AD do Azure senha Olá local arbitrário AD conta de usuário privilegiado, a menos que o administrador Olá é proprietário de saudação dessa conta. Para obter mais informações, consulte muito[4033453 consultoria de segurança](https://technet.microsoft.com/library/security/4033453).

* Corrigido um problema relacionado toohello [msDS-ConsistencyGuid como âncora de origem](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#using-msds-consistencyguid-as-sourceanchor) recurso onde o Azure AD Connect não não write-back tooon locais de atributo msDS-ConsistencyGuid do AD. Olá problema ocorre quando há vários locais florestas do AD adicionado tooAzure AD Connect e hello *existem identidades de usuário em opção de vários diretórios* está selecionado. Quando essa configuração é usada, as regras de sincronização resultante de saudação não preenchem atributo sourceAnchorBinary Olá Olá metaverso. atributo de sourceAnchorBinary de saudação é usado como atributo de origem Olá para o atributo msDS-ConsistencyGuid. Como resultado, atributo do Write-back toohello ms-DSConsistencyGuid não ocorrerá. problema de saudação toofix, seguintes regras de sincronização foram tooensure atualizado que Olá sourceAnchorBinary atributo Olá que metaverso sempre é populado:
  * In from AD – InetOrgPerson AccountEnabled.xml
  * In from AD - InetOrgPerson Common.xml
  * In from AD - User AccountEnabled.xml
  * In from AD - User Common.xml
  * In from AD - User Join SOAInAAD.xml

* Anteriormente, até mesmo se hello [msDS-ConsistencyGuid como âncora de origem](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#using-msds-consistencyguid-as-sourceanchor) recurso não estiver habilitado, hello "Out tooAD – ImmutableId do usuário" regra de sincronização será adicionada tooAzure AD Connect. efeito de saudação é benigno e não faz com que o write-back de toooccur do atributo msDS-ConsistencyGuid. tooavoid confusão, foi adicionada lógica tooensure que Olá regra de sincronização é adicionado somente quando o recurso hello está habilitado.

* Corrigido um problema que causou toofail de sincronização de hash de senha com o evento de erro 611. Esse problema ocorria depois que um ou mais controladores de domínio eram removidos do AD local. No final da saudação de cada ciclo de sincronização de senha, Olá cookie de sincronização emitido por local AD contém IDs de invocação Olá removido dos controladores de domínio com valor de USN (número de sequência de atualização) de 0. Olá Gerenciador de sincronização de senha é toopersist não é possível sincronização cookie contendo USN valor de 0 e falhará com o evento de erro 611. Durante a próxima sincronização de saudação do ciclo, Olá Gerenciador de sincronização de senha reutiliza Olá última persistente cookie de sincronização que não contêm o valor de USN de 0. Isso faz com que Olá mesmas alterações de senha toobe ressincronizado. Com essa correção, Olá Gerenciador de sincronização de senha persiste o cookie de sincronização Olá corretamente.

* Anteriormente, mesmo se a atualização automática foi desativado usando o cmdlet Olá conjunto ADSyncAutoUpgrade, Olá atualização automática do processo continua toocheck para atualização periodicamente e se baseia em Olá baixado instalador toohonor desativação. Com essa correção, Olá o processo de atualização automática não verificará mais atualização periodicamente. correção de saudação é aplicada automaticamente quando o instalador de atualização para esta versão do Azure AD Connect é executada uma vez.

#### <a name="new-features-and-improvements"></a>Novos recursos e aprimoramentos

* Anteriormente, Olá [msDS-ConsistencyGuid como âncora de origem](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#using-msds-consistencyguid-as-sourceanchor) recurso estava disponível toonew implantações somente. Agora, ela é implantações tooexisting disponíveis. Mais especificamente:
  * tooaccess Olá recursos, Iniciar Assistente para conectar-se de saudação do AD do Azure e escolha Olá *âncora de origem de atualização* opção.
  * Essa opção é somente as implantações de tooexisting visível que estão usando o objectGuid como o atributo sourceAnchor.
  * Ao configurar a opção hello, o Assistente de saudação valida estado de saudação do atributo de msDS-ConsistencyGuid Olá no Active Directory local. Se o atributo de saudação não está configurado em qualquer objeto de usuário no diretório Olá, o Assistente de Olá usa Olá msDS-ConsistencyGuid como atributo de sourceAnchor hello. Se o atributo Olá estiver configurado em um ou mais objetos de usuário no diretório hello, Assistente de saudação conclui atributo hello está sendo usado por outros aplicativos e não é adequado como atributo sourceAnchor e não permite Olá tooproceed de alteração de âncora de origem. Se você tem certeza de que o atributo Olá não é usado por aplicativos existentes, será necessário toocontact suporte para obter informações sobre como toosuppress Olá erro.

* Específico muito**userCertificate** atributos nos objetos de dispositivo, o Azure AD Connect agora procura valores de certificados necessários para [tooAzure de dispositivos que ingressaram no domínio AD para Windows 10 experiência de conexão](https://docs.microsoft.com/azure/active-directory/active-directory-azureadjoin-devices-group-policy) e filtra os Olá restante antes de sincronizar tooAzure AD. tooenable esse comportamento, a regra de sincronização de out-of-box hello "Out tooAAD - dispositivo ingressar SOAInAD" foi atualizado.

* Azure AD Connect agora dá suporte a write-back do Exchange Online **cloudPublicDelegates** tooon local de atributo AD **publicDelegates** atributo. Isso permite que o cenário de saudação em que uma caixa de correio do Exchange Online pode ser concedida SendOnBehalfTo direitos toousers com caixa de correio do Exchange no local. toosupport esse recurso, uma nova regra de sincronização de fora da caixa "Out tooAD – usuário Exchange híbrido PublicDelegates write-back" foi adicionado. Essa regra de sincronização só é adicionada tooAzure AD se conectar ao recurso híbrida do Exchange está habilitado.

*   Azure AD Connect agora dá suporte a sincronização Olá **altRecipient** atributo do AD do Azure. toosupport essa alteração, regras de sincronização de fora da caixa a seguir foram atualizados tooinclude o fluxo de atributos Olá necessários:
  * Entrada do AD – usuário do Exchange
  * Limite tooAAD – ExchangeOnline do usuário
  
* Olá **cloudSOAExchMailbox** atributo Olá metaverso indica se um determinado usuário tem a caixa de correio do Exchange Online ou não. Sua definição foi atualizada tooinclude RecipientDisplayTypes Online adicionais do Exchange como essas caixas de correio de sala de conferência e equipamentos. tooenable essa alteração, a definição de saudação do atributo de cloudSOAExchMailbox hello, que se encontra na regra de sincronização de fora da caixa "do AAD – usuário Exchange híbrido", foi atualizada em:

```
CBool(IIF(IsNullOrEmpty([cloudMSExchRecipientDisplayType]),NULL,BitAnd([cloudMSExchRecipientDisplayType],&amp;HFF) = 0))
```

... toohello a seguir:

```
CBool(
  IIF(IsPresent([cloudMSExchRecipientDisplayType]),(
    IIF([cloudMSExchRecipientDisplayType]=0,True,(
      IIF([cloudMSExchRecipientDisplayType]=2,True,(
        IIF([cloudMSExchRecipientDisplayType]=7,True,(
          IIF([cloudMSExchRecipientDisplayType]=8,True,(
            IIF([cloudMSExchRecipientDisplayType]=10,True,(
              IIF([cloudMSExchRecipientDisplayType]=16,True,(
                IIF([cloudMSExchRecipientDisplayType]=17,True,(
                  IIF([cloudMSExchRecipientDisplayType]=18,True,(
                    IIF([cloudMSExchRecipientDisplayType]=1073741824,True,(
                       IF([cloudMSExchRecipientDisplayType]=1073741840,True,False)))))))))))))))))))),False))

```

* A seguir Olá adicionado conjunto de funções X509Certificate2 compatível para criar valores de certificado de toohandle de expressões de regra de sincronização no atributo de userCertificate Olá:

    ||||
    | --- | --- | --- |
    |CertSubject|CertIssuer|CertKeyAlgorithm|
    |CertSubjectNameDN|CertIssuerOid|CertNameInfo|
    |CertSubjectNameOid|CertIssuerDN|IsCert|
    |CertFriendlyName|CertThumbprint|CertExtensionOids|
    |CertFormat|CertNotAfter|CertPublicKeyOid|
    |CertSerialNumber|CertNotBefore|CertPublicKeyParametersOid|
    |CertVersion|CertSignatureAlgorithmOid|Selecionar|
    |CertKeyAlgorithmParams|CertHashString|Where|
    |||With|

* Alterações de esquema a seguir foram introduzidas tooallow clientes toocreate sincronização personalizadas regras tooflow sAMAccountName, domainNetBios e domainFQDN para objetos de grupo, bem como distinguishedName para objetos de usuário:

  * Atributos a seguir foram adicionados tooMV esquema:
    * Grupo: AccountName
    * Grupo: domainNetBios
    * Grupo: domainFQDN
    * Pessoa: distinguishedName

  * Atributos a seguir foram adicionados tooAzure esquema de conector AD:
    * Grupo: OnPremisesSamAccountName
    * Grupo: NetBiosName
    * Grupo: DnsDomainName
    * Usuário: OnPremisesDistinguishedName

* Olá ADSyncDomainJoinedComputerSync cmdlet script agora tem um novo parâmetro opcional nomeado AzureEnvironment. parâmetro Hello é usado toospecify Olá qual região correspondente locatário do Active Directory do Azure está hospedado no. Os valores válidos incluem:
  * AzureCloud (padrão)
  * AzureChinaCloud
  * AzureGermanyCloud
  * USGovernment
 
* Unir toouse atualizado do Editor de regra de sincronização (em vez de provisionar) como valor padrão de saudação do tipo de link durante a criação de regra de sincronização.

### <a name="ad-fs-management"></a>Gerenciamento dos AD FS

#### <a name="issues-fixed"></a>Problemas corrigidos

* URLs a seguir são novos pontos de extremidade do WS-Federation introduzidos por resiliência do AD do Azure tooimprove contra falha de autenticação e será adicionado tooon local responder a configuração de confiança de terceiros do AD FS:
  * https://ests.login.microsoftonline.com/login.srf
  * https://stamp2.login.microsoftonline.com/login.srf
  * https://ccs.login.microsoftonline.com/login.srf
  * https://ccs-sdf.login.microsoftonline.com/login.srf
  
* Corrigido um problema que causou o valor de declaração incorreta do AD FS toogenerate para IssuerID. problema de saudação ocorre se houver vários domínios verificados no locatário de saudação do AD do Azure e o sufixo do domínio de saudação do hello userPrincipalName atributo usado toogenerate Olá IssuerID declaração é pelo menos 3 níveis profunda (por exemplo, johndoe@us.contoso.com). Olá problema é resolvido atualizando regex Olá usado pelas regras de declaração de saudação.

#### <a name="new-features-and-improvements"></a>Novos recursos e aprimoramentos
* Anteriormente, o recurso de gerenciamento de certificados de ADFS de saudação fornecido pelo Azure AD Connect somente pode ser usado com ADFS farms de servidores gerenciados por meio do Azure AD Connect. Agora, você pode usar o recurso de saudação com farms de servidores do AD FS que não são gerenciados usando o Azure AD Connect.

## <a name="115240"></a>1.1.524.0
Lançamento: maio de 2017

> [!IMPORTANT]
> Foram introduzidas alterações de regra de esquema e sincronização nesse build. O Serviço de Sincronização do Azure AD Connect disparará as etapas de Importação Completa e Sincronização Completa após a atualização. Detalhes das alterações de saudação são descritos abaixo.
>
>

**Problemas corrigidos:**

Sincronização do Azure AD Connect

* Corrigido um problema que faz com que toooccur atualização automática no servidor do Azure AD Connect hello, mesmo se o cliente tiver desabilitado o recurso hello usando Olá conjunto ADSyncAutoUpgrade cmdlet. Com essa correção, Olá processo de atualização automática no servidor de saudação ainda verifica se há atualização periodicamente, mas instalador baixado hello respeita a configuração de atualização automática de saudação.
* Durante a atualização in-loco de DirSync, o Azure AD Connect cria um toobe de conta de serviço do AD do Azure usada pelo conector de saudação do AD do Azure para sincronizar com o AD do Azure. Após a criação de conta de Olá, Azure AD Connect autentica com o Azure AD usando a conta de saudação. Às vezes, a autenticação falha devido a problemas transitórios, que por sua vez, faz toofail atualização do DirSync no local com o erro *"Ocorreu um erro ao executar tarefa de configurar a sincronização do AAD: AADSTS50034: toosign nesse aplicativo, a conta de saudação deve ser adicionado toohello xxx.onmicrosoft.com directory."* tooimprove resiliência de saudação da atualização do DirSync, do Azure AD Connect agora tentará novamente a etapa de autenticação hello.
* Houve um problema com a compilação 443 que faz com que o DirSync in-loco atualização toosucceed mas necessários para a sincronização de diretório de perfis de execução não são criados. A lógica de reparo está incluída nesse build do Azure AD Connect. Quando o cliente atualiza toothis compilação, o Azure AD Connect detecta ausente perfis de execução e criá-los.
* Corrigido um problema que faz a sincronização de senha processo toofail toostart 6900 de ID de evento e o erro *"Um item com hello a mesma chave já foi adicionado"*. Esse problema ocorre se você atualizar OU partição de configuração de tooinclude AD de configuração de filtragem. toofix esse problema, a sincronização de senha agora processar sincroniza alterações de senha de partições de domínio do AD apenas. Partições não de domínio, como a partição de configuração, são ignoradas.
* Durante a instalação do Express, a conexão do AD do Azure cria um local toobe usado pelo Olá AD conector toocommunicate com o local de conta do AD DS AD. Anteriormente, Olá conta é criada com o sinalizador PASSWD_NOTREQD Olá definido no atributo de controle de conta de usuário hello e uma senha aleatória é definida na conta de saudação. Agora, Azure AD Connect explicitamente remove sinalizador PASSWD_NOTREQD Olá depois Olá senha é definida na conta de saudação.
* Corrigido um problema que faz com que o DirSync toofail de atualização com o erro *"Ocorreu um deadlock no sql server que tentar tooacquire um bloqueio de aplicativo"* quando o atributo de mailNickname hello está localizado no hello esquema do AD local, mas não é classe de objeto de usuário do AD de toohello limitada.
* Fixo de um problema que causa tooautomatically de recurso de write-back do dispositivo desativado quando um administrador está atualizando a configuração de sincronização do Azure AD Connect usando o Assistente de conexão do AD do Azure. Isso é causado pela verificação de pré-requisito executando Olá Assistente para write-back configuração de dispositivo existente Olá no AD local e Falha na verificação da saudação. correção de saudação é seleção de saudação tooskip se Write-back de dispositivo já está habilitado anteriormente.
* tooconfigure OU filtragem, você pode usar Assistente de conexão do AD do Azure hello ou Olá Synchronization Service Manager. Anteriormente, se você usar a filtragem de saudação do AD do Azure Connect Assistente tooconfigure unidade Organizacional, novas OUs criadas posteriormente são incluídas para sincronização de diretórios. Se você não quiser novo toobe UOs incluído, você deve configurar OU filtragem usando Olá Synchronization Service Manager. Agora, você pode obter Olá mesmo comportamento usando o Assistente de conexão do AD do Azure.
* Corrigido um problema que faz com que procedimentos armazenados exigidos pelo Azure AD Connect toobe criado no esquema de saudação do hello instalando admin, em vez de no esquema de dbo hello.
* Corrigido um problema que faz com que o atributo de TrackingId Olá retornado pelo AD do Azure toobe omitido na Olá AAD Logs de eventos de servidor se conectar. problema de Olá ocorre se o Azure AD Connect recebe uma mensagem de redirecionamento do AD do Azure e do Azure AD Connect é o ponto de extremidade de toohello de tooconnect fornecido. Olá TrackingId é usada pelo toocorrelate engenheiros de suporte com logs de lado do serviço durante a solução de problemas.
* Quando o Azure AD Connect recebe o erro LargeObject do AD do Azure, Azure AD Connect gera um evento com EventID 6941 e mensagem *"hello provisionado é muito grande. Número de saudação de valores de atributo nesse objeto trim."* A saudação mesmo momento, o Azure AD Connect também gera um evento enganoso com EventID 6900 e mensagem *"Microsoft.Online.Coexistence.ProvisionRetryException: não é possível toocommunicate com hello Windows serviço Active Directory do Azure."* toominimize confusão, Azure AD Connect não gera o evento com este último hello quando LargeObject erro é recebido.
* Corrigido um problema que faz com que o hello toobecome do Gerenciador de serviço de sincronização não responder durante a tentativa de configuração de saudação tooupdate para conector LDAP genérico.

**Novos recursos/melhorias:**

Sincronização do Azure AD Connect
* Sincronizar as alterações de regra – Olá regra de sincronização foram implementadas alterações a seguir:
  * Conjunto de regras de sincronização padrão atualizado toonot atributos de exportação **userCertificate** e **userSMIMECertificate** se atributos Olá tem mais de 15 valores.
  * Atributos do AD **employeeID** e **msExchBypassModerationLink** agora estão incluídas no conjunto de regras de sincronização saudação padrão.
  * O atributo **photo** do AD foi removido do conjunto de regras de sincronização padrão.
  * Adicionado **preferredDataLocation** toohello metaverso esquema e o esquema do conector AAD. Clientes que desejam tooupdate que podem implementar qualquer um dos atributos no AD do Azure personalizado toodo de regras de sincronização assim. toofind mais informações sobre o atributo Olá, consulte a seção tooarticle [sincronização do Azure AD Connect: como a toomake toohello uma alteração de configuração - Habilitar sincronização de PreferredDataLocation padrão](active-directory-aadconnectsync-change-the-configuration.md#enable-synchronization-of-preferreddatalocation).
  * Adicionado **userType** toohello metaverso esquema e o esquema do conector AAD. Clientes que desejam tooupdate que podem implementar qualquer um dos atributos no AD do Azure personalizado toodo de regras de sincronização assim.

* Conexão do AD do Azure agora automaticamente habilita Olá usar ConsistencyGuid atributo como atributo de âncora de origem Olá para local objetos do AD. Além disso, o Azure AD Connect preenche o atributo de ConsistencyGuid de saudação com valor de atributo objectGuid Olá se ela estiver vazia. Este recurso está apenas a implantação toonew aplicável. toofind mais informações sobre esse recurso, consulte a seção tooarticle [do Azure AD Connect: conceitos - usando msDS-ConsistencyGuid como sourceAnchor de projeto](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor).
* Nova solução de problemas cmdlet Invoke-ADSyncDiagnostics foi adicionado toohelp diagnosticar sincronização de Hash de senha problemas relacionados. Para obter informações sobre como usar o cmdlet hello, consulte tooarticle [solucionar problemas de sincronização de senha com a sincronização do Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-troubleshoot-password-synchronization).
* Conexão do AD do Azure agora oferece suporte a objetos de sincronizar Mail-Enabled de pasta pública do AD tooAzure AD no local. Você pode habilitar o recurso de saudação usando o Assistente de conexão do AD do Azure em recursos opcionais. toofind mais informações sobre esse recurso, consulte tooarticle [Office 365 diretório com base em borda bloqueando o suporte a locais Mail habilitado pública pastas](https://blogs.technet.microsoft.com/exchange/2017/05/19/office-365-directory-based-edge-blocking-support-for-on-premises-mail-enabled-public-folders).
* Um toosynchronize de conta do AD DS do local requer a conexão do AD do Azure AD. Anteriormente, se você instalou o Azure AD Connect usando o modo expresso hello, você pode fornecer credenciais de saudação de uma conta de administrador corporativo e do Azure AD Connect criaria conta Olá AD DS necessária. No entanto, para uma instalação personalizada e adicionar a implantação existente do tooan florestas, era necessário tooprovide Olá conta AD DS em vez disso. Agora, você também tem Olá opção tooprovide Olá credenciais de uma conta de administrador corporativo durante uma instalação personalizada e permitem que o Azure AD Connect criar hello AD DS conta necessária.
* O Azure AD Connect agora dá suporte a SQL AOA. Você deve habilitar o SQL AOA antes de instalar o Azure AD Connect. Durante a instalação, o Azure AD Connect detecta se a instância SQL Olá fornecida está habilitada para SQL AOA, ou não. Se SQL AOA estiver habilitado, o Azure AD Connect mais descobre se SQL AOA é replicação síncrona toouse configurado ou replicação assíncrona. Ao configurar o ouvinte do grupo de disponibilidade do hello, é recomendável que você defina Olá RegisterAllProvidersIP propriedade too0. Isso ocorre porque a conexão do AD do Azure atualmente usa o SQL Native Client tooconnect tooSQL e SQL Native Client não dá suporte para uso de saudação da propriedade MultiSubNetFailover.
* Se você estiver usando o LocalDB como banco de dados de saudação do servidor do Azure AD Connect e atingiu seu limite de tamanho de 10 GB, Olá serviço de sincronização não inicia. Anteriormente, você precisa tooperform operação ShrinkDatabase Olá LocalDB tooreclaim suficiente espaço de banco de dados para Olá toostart de serviço de sincronização. Depois que, você pode usar Olá toodelete Synchronization Service Manager executar tooreclaim histórico mais espaço de banco de dados. Agora, você pode usar Start-ADSyncPurgeRunHistory cmdlet toopurge executar dados de histórico do espaço de banco de dados de tooreclaim LocalDB. Além disso, esse cmdlet dá suporte ao modo offline (especificando Olá - parâmetro offline) que pode ser usado quando Olá serviço de sincronização não está em execução. Observação: Olá offline modo pode ser usado apenas se hello serviço de sincronização não está em execução e o banco de dados de saudação usado é LocalDB.
* tooreduce saudação do espaço de armazenamento necessário, o Azure AD Connect agora compacta os detalhes do erro de sincronização antes de armazená-los em bancos de dados LocalDB/SQL. Ao atualizar de uma versão anterior do Azure AD Connect toothis versão, do Azure AD Connect executa uma única compactação nos detalhes de erro de sincronização existente.
* Anteriormente, depois de atualizar OU configuração de filtragem, você deve executar manualmente a importação completa tooensure objetos existentes são corretamente incluído/excluído da sincronização de diretório. Agora, o Azure AD Connect aciona importação completa automaticamente durante a próxima sincronização de saudação do ciclo. Importação completa, mais só é ser aplicada toohello AD conectores afetados pela atualização de saudação. Observação: essa melhoria é aplicável tooOU filtragem atualizações feitas usando o assistente apenas do hello Azure AD Connect. Não é aplicável tooOU filtragem atualização feita usando Olá Synchronization Service Manager.
* Anteriormente, filtragem baseada em Grupo dava suporte apenas a objetos de Usuários, Grupos e Contato. Agora, a filtragem baseada em Grupo também dá suporte a objetos de Computador.
* Anteriormente, você podia excluir dados do Espaço Conector sem desabilitar o agendador de sincronização do Azure AD Connect. Agora, Olá Synchronization Service Manager exclusão de saudação de blocos de dados de espaço do conector se detectar que o Agendador hello está habilitado. Além disso, um aviso é retornado tooinform clientes sobre uma possível perda de dados se Olá dados de espaço do conector é excluído.
* Anteriormente, você deve desabilitar a transcrição do PowerShell para Azure AD Connect Assistente toorun corretamente. Esse problema foi parcialmente resolvido. Se você estiver usando a configuração de sincronização do toomanage do Assistente de conexão do AD do Azure, você pode habilitar transcrição do PowerShell. Se você estiver usando a configuração de toomanage do ADFS do Assistente de conexão do AD do Azure, você deve desabilitar a transcrição do PowerShell.



## <a name="114860"></a>1.1.486.0
Lançamento: abril de 2017

**Problemas corrigidos:**
* Correção do problema Olá onde do Azure AD Connect não será instalado com êxito em uma versão localizada do Windows Server.

## <a name="114840"></a>1.1.484.0
Lançamento: abril de 2017

**Problemas conhecidos:**

* Esta versão do Azure AD Connect não será instalado com êxito se Olá seguintes condições é verdadeira:
   1. Você está executando a atualização DirSync in-loco ou a nova instalação do Azure AD Connect.
   2. Você está usando uma versão localizada do Windows Server em que o nome de saudação do grupo de administradores interno no servidor de saudação não é "Administradores".
   3. Você está usando o padrão de saudação SQL Server 2012 Express LocalDB instalado com o Azure AD Connect em vez de fornecer seu próprio completa do SQL.

**Problemas corrigidos:**

Sincronização do Azure AD Connect
* Corrigido um problema onde Agendador de sincronização Olá ignora a etapa de sincronização inteiro Olá se o perfil de execução para essa etapa de sincronização não tiver um ou mais conectores. Por exemplo, você adicionou manualmente um conector usando Olá Synchronization Service Manager sem criar um perfil de execução para ele de importação de Delta. Essa correção garante que o Agendador de sincronização Olá continua toorun importação Delta para outros conectores.
* Corrigido um problema em que Olá serviço de sincronização imediatamente para o processamento um perfil de execução quando for encontra um problema com uma das etapas de saudação executar. Essa correção garante que Olá ignora o serviço de sincronização que execute a etapa e continua tooprocess Olá rest. Por exemplo, você tem um perfil de execução de Importação Delta para seu conector do AD com várias etapas de execução (uma para cada domínio do AD local). saudação de serviço de sincronização será executado importação Delta com hello outros domínios do AD mesmo se uma delas tiver problemas de conectividade de rede.
* Corrigido um problema que faz com que o toobe de atualização do conector AD do Azure Olá ignorado durante a atualização automática.
* Corrigido um problema tooincorrectly de conectar-se que faz com que o AD do Azure determinam se o servidor de saudação é um controlador de domínio durante a instalação, que por sua vez causas DirSync atualizar toofail.
* Fixo de um problema que faz com que o DirSync toonot atualização in-loco criar qualquer executar perfil Olá conector AD do Azure.
* Corrigido um problema em que interface de usuário do Gerenciador de serviço de sincronização Olá deixa de responder durante a tentativa de tooconfigure conector de LDAP genérico.

Gerenciamento dos AD FS
* Corrigido um problema onde o Assistente de conexão do AD do Azure Olá falha se o nó primário do hello AD FS tiver sido movido tooanother server.

SSO da Área de Trabalho
* Corrigido um problema no Assistente de conexão do AD do Azure Olá onde hello tela de entrada não permite que você habilitar o recurso de SSO de área de trabalho se você escolher a sincronização de senha como a opção de entrada durante a instalação de novo.

**Novos recursos/melhorias:**

Sincronização do Azure AD Connect
* AD conectar-se a sincronização do Azure agora dá suporte a uso de saudação de conta de serviço Virtual, a conta de serviço gerenciado e conta de serviço gerenciado do grupo como sua conta de serviço. Isso se aplica a instalação toonew do Azure AD Connect somente. Ao instalar o Azure AD Connect:
    * Por padrão, o assistente do Azure AD Connect criará uma Conta de Serviço Virtual e utilizará como sua conta de serviço.
    * Se você estiver instalando em um controlador de domínio, o Azure AD Connect reverterá ser tooprevious comportamento em que criará uma conta de usuário de domínio e o utiliza como sua conta de serviço em vez disso.
    * Você pode substituir o comportamento padrão de saudação fornecendo Olá seguinte:
      * Uma Conta de Serviço Gerenciado de Grupo
      * Uma Conta de Serviço Gerenciado
      * Uma conta de usuário do domínio
      * Uma conta de usuário local
* Anteriormente, se você atualizar tooa nova compilação do Azure AD Connect que contém atualizar conectores ou alterações nas regras de sincronização, o Azure AD Connect dispararão um ciclo de sincronização completa. Agora, o Azure AD Connect dispara seletivamente a etapa de Importação Completa somente para conectores com atualização e a etapa de Sincronização Completa somente para conectores com alterações de regra de sincronização.
* Anteriormente, Olá limite de exclusão de exportação só se aplica a tooexports que são disparadas por meio do Agendador de sincronização de saudação. Agora, o recurso de saudação é estendido tooinclude exportações manualmente disparadas por cliente hello usando Olá Synchronization Service Manager.
* No seu locatário do Azure AD, há uma configuração de serviço que indica se o recurso de Sincronização de Senha está habilitado para o seu locatário ou não. Anteriormente, é fácil para Olá toobe de configuração de serviço configurado incorretamente pelo Azure AD Connect quando você tem um ativo e um servidor de preparo. Agora, o Azure AD Connect tentará tookeep consistente com seu ativo de configuração de serviço de saudação apenas o servidor do Azure AD Connect.
* O assistente do Azure AD Connect agora detecta e retorna um aviso se o AD local não tiver Lixeira do AD ativada.
* Anteriormente, exportação tooAzure AD expira e falhará se Olá combinados tamanho dos objetos de saudação em lote Olá excede determinado limite. Agora, Olá serviço de sincronização tentará tooresend objetos de saudação em lotes menores se Olá problema for encontrado.
* saudação de aplicativo de gerenciamento de chaves do serviço de sincronização foi removida do Menu Iniciar do Windows. Gerenciamento de chave de criptografia continuará toobe têm suportada por meio da interface de linha de comando usando miiskmu.exe. Para obter informações sobre o gerenciamento de chave de criptografia, consulte tooarticle [chave de criptografia de sincronização se conectar de saudação do AD do Azure Abandoning](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-change-serviceacct-pass#abandoning-the-azure-ad-connect-sync-encryption-key).
* Anteriormente, se você alterar a senha da conta de serviço para o Azure AD Connect sincronização de hello, Olá serviço de sincronização não será capaz de iniciar corretamente até ter abandonado a chave de criptografia de saudação e reiniciadas a senha da conta de serviço para o Azure AD Connect sincronização de saudação. Agora, isso não é mais necessário.

SSO da Área de Trabalho

* Assistente de conexão do AD do Azure não requer mais porta 9090 toobe aberto na rede Olá ao configurar a autenticação de passagem e SSO de área de trabalho. Somente a porta 443 é exigida. 

## <a name="114430"></a>1.1.443.0
Lançamento: março de 2017

**Problemas corrigidos:**

Sincronização do Azure AD Connect
* Corrigido um problema que faz com que o Azure AD Connect Assistente toofail se o nome de exibição de saudação do hello conector AD do Azure não contém a saudação inicial onmicrosoft.com domínio atribuído toohello AD do Azure locatário.
* Corrigido um problema que faz com que o Azure AD Connect Assistente toofail ao fazer o banco de dados de tooSQL de conexão quando a senha Olá Olá conta de serviço de sincronização contém caracteres especiais, como o apóstrofo, dois-pontos e espaço.
* Corrigido um problema que causa o erro de saudação toooccur "hello dimage tem uma âncora que é diferente de imagem hello" em um servidor do Azure AD Connect em modo de preparo, após você temporariamente excluiu um local AD da sincronização do objeto e, em seguida, incluído-lo novamente para sincronizando.
* Corrigido um problema que causa o erro de saudação toooccur "objeto Olá localizado por DN é um fantasma" em um servidor do Azure AD Connect em modo de preparo, após você temporariamente excluiu um local AD da sincronização do objeto e incluído-o novamente para sincronizar.

Gerenciamento dos AD FS
* Corrigido um problema em que o Assistente do Azure AD Connect não atualizar a configuração do AD FS e definido Olá direita declarações em Olá terceira parte confiável após a configuração de ID de logon alternativo.
* Corrigido um problema em que o Assistente do Azure AD Connect é servidores de FS de identificador AD toocorrectly não é possível cujas contas de serviço são configuradas usando o formato userPrincipalName em vez do formato de sAMAccountName.

Autenticação de Passagem
* Corrigido um problema que faz com que o Azure AD Connect Assistente toofail se passar por meio de autenticação está selecionada, mas o registro do seu conector falhar.
* Corrigido um problema que faz com que o Azure AD Connect, verificações de validação de toobypass de assistente no método de entrada selecionado quando o recurso de SSO de área de trabalho está habilitado.

Redefinição de senha
* Corrigido um problema que pode causar hello Azure AAD Connect server toonot tentativa toore-conectar se a conexão de saudação foi interrompida por um firewall ou proxy.

**Novos recursos/melhorias:**

Sincronização do Azure AD Connect
* Agora, o cmdlet Get-ADSyncScheduler retorna uma nova propriedade booliana chamada SyncCycleInProgress. Se Olá retornou o valor for true, o que significa que há um ciclo de sincronização agendada em andamento.
* Pasta de destino para armazenar logs de instalação e de instalação do Azure AD Connect foi movida %localappdata%\AADConnect too%programdata%\AADConnect tooimprove acessibilidade toohello dos arquivos de log.

Gerenciamento dos AD FS
* Adição de suporte para atualização do Certificado SSL do Farm do AD FS.
* Adição de suporte para gerenciamento do AD FS 2016.
* Agora é possível especificar uma gMSA (Conta de Serviço Gerenciado de Grupo) existente durante a instalação do AD FS.
* Agora você pode configurar o SHA-256 como algoritmo de hash de assinatura de saudação da terceira parte confiável do AD do Azure.

Redefinição de senha
* Melhorias introduzidas tooallow Olá toofunction produto em ambientes com regras de firewall mais rigorosas.
* Conexão maior confiabilidade tooAzure barramento de serviço.

## <a name="113800"></a>1.1.380.0
Lançamento: dezembro de 2016

**Problema corrigido:**

* Problema de saudação fixa onde Olá issuerid regra de declaração para os serviços de Federação do Active Directory (AD FS) está faltando nesta compilação.

>[!NOTE]
>Esta compilação não está disponível toocustomers por meio do recurso de conectar-se a atualização automática de saudação do AD do Azure.

## <a name="113710"></a>1.1.371.0
Lançamento: dezembro de 2016

**Problema conhecido:**

* regra de declaração de issuerid Olá para o AD FS está ausente na compilação. regra de declaração de issuerid Olá será necessária se você está associando vários domínios com o Azure Active Directory (AD do Azure). Se você estiver usando seu local do Azure AD Connect toomanage implantação do AD FS, atualizando toothis build remove regra de declaração de issuerid existente Olá da configuração do AD FS. Você pode contornar o problema de saudação ao Adicionar regra de declaração de issuerid Olá após a atualização da instalação hello. Para obter detalhes sobre como adicionar Olá issuerid regra de declaração, consulte artigo toothis na [suporte para vários domínios para federação com o Azure AD](active-directory-aadconnect-multiple-domains.md).

**Problema corrigido:**

* Se 9090 de porta não está aberto para conexão de saída de hello, Olá do Azure AD Connect instalação ou atualização falhará.

>[!NOTE]
>Esta compilação não está disponível toocustomers por meio do recurso de conectar-se a atualização automática de saudação do AD do Azure.

## <a name="113700"></a>1.1.370.0
Lançamento: dezembro de 2016

**Problemas conhecidos:**

* regra de declaração de issuerid Olá para o AD FS está ausente na compilação. regra de declaração de issuerid Olá será necessária se você está associando vários domínios com o Azure AD. Se você estiver usando seu local do Azure AD Connect toomanage implantação do AD FS, atualizando toothis build remove regra de declaração de issuerid existente Olá da configuração do AD FS. Você pode contornar o problema de saudação ao Adicionar regra de declaração de issuerid Olá após a instalação/atualização. Para obter detalhes sobre como adicionar issuerid a regra de declaração, consulte o artigo toothis na [suporte para vários domínios para federação com o Azure AD](active-directory-aadconnect-multiple-domains.md).
* Porta 9090 deve ser aberto toocomplete de saída.

**Novos recursos:**

* Autenticação de Passagem (Visualização).

>[!NOTE]
>Esta compilação não está disponível toocustomers por meio do recurso de conectar-se a atualização automática de saudação do AD do Azure.

## <a name="113430"></a>1.1.343.0
Lançamento: novembro de 2016

**Problema conhecido:**

* regra de declaração de issuerid Olá para o AD FS está ausente na compilação. regra de declaração de issuerid Olá será necessária se você está associando vários domínios com o Azure AD. Se você estiver usando seu local do Azure AD Connect toomanage implantação do AD FS, atualizando toothis build remove regra de declaração de issuerid existente Olá da configuração do AD FS. Você pode contornar o problema de saudação ao Adicionar regra de declaração de issuerid Olá após a instalação/atualização. Para obter detalhes sobre como adicionar issuerid a regra de declaração, consulte o artigo toothis na [suporte para vários domínios para federação com o Azure AD](active-directory-aadconnect-multiple-domains.md).

**Problemas corrigidos:**

* Às vezes, a instalação do Azure AD Connect falha porque é uma conta de serviço local cuja senha atende o nível de saudação de complexidade especificada por política de senha da organização de saudação do toocreate não é possível.
* Corrigido um problema em que as regras de associação não são reavaliadas quando um objeto no espaço do conector Olá simultaneamente fica fora do escopo para uma junção regra e tornam-se em escopo para outro. Isso pode ocorrer se você tiver duas ou mais regras de junção cujas condições de junção são mutuamente exclusivas.
* Corrigido um problema em que regras de sincronização de entrada (do Azure AD) que não contêm regras de união não são processadas se elas tiverem valores de precedência inferiores daqueles que contém regras de associação.

**Aperfeiçoamentos:**

* Adicionado suporte para instalar o Azure AD Connect no Windows Server 2016 Standard ou posterior.
* Adicionado suporte para usar o SQL Server 2016 como banco de dados remoto Olá para o Azure AD Connect.

## <a name="112810"></a>1.1.281.0
Lançamento: agosto de 2016

**Problemas corrigidos:**

* Intervalo de toosync alterações não ocorrerá até que após Olá próximo ciclo de sincronização seja concluído.
* O assistente do Azure AD Connect não aceita uma conta do Azure AD cujo nome de usuário começa com um sublinhado (\_).
* Assistente de conexão do AD do Azure falha conta do tooauthenticate Olá AD do Azure se a senha da conta Olá contém muitos caracteres especial. Mensagem de erro "não é possível toovalidate credenciais. Ocorreu um erro inesperado.” é retornado.
* Desinstalando o servidor de preparo desabilita a sincronização de senha no locatário do AD do Azure e faz com que o toofail de sincronização de senha com o servidor ativo.
* Sincronização de senha falha em casos incomuns, quando não houver nenhum hash de senha armazenado em usuário hello.
* Quando o servidor do Azure AD Connect está habilitado para o modo de preparo, o write-back de senha não é temporariamente desabilitado.
* Assistente do Azure AD Connect não mostra a sincronização de senha real hello e configuração de write-back de senha quando o servidor está em modo de preparo. Ele sempre os mostra como desabilitados.
* Sincronização de toopassword de alterações de configuração e de write-back de senha não são mantidas pelo Assistente de conexão do AD do Azure, quando o servidor está em modo de preparo.

**Aperfeiçoamentos:**

* Atualizado saudação inicial ADSyncSyncCycle cmdlet tooindicate seja toosuccessfully capaz de iniciar um novo ciclo de sincronização ou não.
* Ciclo de sincronização de tooterminate de cmdlet adicionados Olá ADSyncSyncCycle parar e operação, que estão atualmente em andamento.
* Ciclo de sincronização atualizado Olá Stop-ADSyncScheduler cmdlet tooterminate e operação, que estão atualmente em andamento.
* Ao configurar [extensões de diretório](active-directory-aadconnectsync-feature-directory-extensions.md) no Assistente de conexão do AD do Azure, o atributo de saudação do AD do Azure do tipo "Cadeia de caracteres Teletex" agora pode ser selecionado.

## <a name="111890"></a>1.1.189.0
Lançamento: junho de 2016

**Problemas corrigidos e aperfeiçoamentos:**

* O Azure AD Connect agora pode ser instalado em um servidor compatível com FIPS.
  * Para sincronização de senha, confira [Sincronização de senha e FIPS](active-directory-aadconnectsync-implement-password-synchronization.md#password-synchronization-and-fips).
* Corrigido um problema em que um nome NetBIOS não pôde ser resolvido toohello FQDN no hello conector do Active Directory.

## <a name="111800"></a>1.1.180.0
Lançamento: maio de 2016

**Novos recursos:**

* Avisa e ajuda a verificar os domínios se você não fizer isso antes de executar o Azure AD Connect.
* Adicionado suporte ao [Microsoft Cloud Alemanha](active-directory-aadconnect-instances.md#microsoft-cloud-germany).
* Adicionado suporte para mais recente Olá [nuvem do Microsoft Azure Government](active-directory-aadconnect-instances.md#microsoft-azure-government-cloud) infraestrutura com novos requisitos de URL.

**Problemas corrigidos e aperfeiçoamentos:**

* Adicionado toohello filtragem toomake do Editor de regra de sincronização-toofind fácil regras de sincronização.
* Desempenho aprimorado ao excluir um espaço de conector.
* Corrigido um problema quando Olá mesmo objeto tanto foi excluído e adicionado em Olá mesmo executar (chamado excluir ou adicionar).
* Uma regra de sincronização desabilitada não pode mais reabilitar objetos e atributos incluídos na atualização ou na atualização de esquema de diretório.

## <a name="111300"></a>1.1.130.0
Lançamento: abril de 2016

**Novos recursos:**

* Adicionado suporte para atributos com valores múltiplos muito[extensões de diretório](active-directory-aadconnectsync-feature-directory-extensions.md).
* Adicionado suporte para mais variações de configuração para [atualização automática](active-directory-aadconnect-feature-automatic-upgrade.md) toobe considerado qualificado para atualização.
* Adicionados alguns cmdlets para o [agendador personalizado](active-directory-aadconnectsync-feature-scheduler.md#custom-scheduler).

## <a name="111190"></a>1.1.119.0
Lançamento: março de 2016

**Problemas corrigidos:**

* Foi garantido que a Instalação expressa não possa ser usada no Windows Server 2008 (pré-R2), já que a sincronização de senha não tem suporte neste sistema operacional.
* A atualização do DirSync com uma configuração de filtro personalizado não funcionou conforme o esperado.
* Ao atualizar a versão mais recente do tooa e não há nenhuma configuração de toohello alterações, uma sincronização/importação completa não deve ser agendada.

## <a name="111100"></a>1.1.110.0
Lançamento: fevereiro de 2016

**Problemas corrigidos:**

* Atualização de versões anteriores não funcionará se a instalação de saudação não está na pasta de C:\Program Files saudação padrão.
* Se você instalar e desmarque **iniciar o processo de sincronização Olá** final Olá Olá do Assistente de instalação, Assistente de instalação em execução Olá uma segunda vez não permitirão Agendador hello.
* Agendador Hello não funciona conforme o esperado em servidores onde hello formato de data/hora US-en não é usado. Ele também bloqueia `Get-ADSyncScheduler` vezes correto tooreturn.
* Se você instalou uma versão anterior do Azure AD Connect com o AD FS como Olá atualização e a opção de entrada, você não pode executar novamente o Assistente de instalação de saudação.

## <a name="111050"></a>1.1.105.0
Lançamento: fevereiro de 2016

**Novos recursos:**

* [Automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) para clientes de configurações Expressas.
* Suporte para Olá administrador global usando o Azure multi-Factor Authentication e Privileged Identity Management no Assistente de instalação de saudação.
  * Você precisa tooallow tooalso seu proxy para permitir tráfego toohttps://secure.aadcdn.microsoftonline-p.com se você usar a autenticação multifator.
  * Lista de sites confiáveis do tooadd https://secure.aadcdn.microsoftonline-p.com tooyour são necessários para o trabalho de tooproperly multi-Factor Authentication.
* Permite alterar o método de entrada do usuário Olá após a instalação inicial.
* Permitir [domínio e unidade Organizacional filtragem](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering) no Assistente de instalação de saudação. Isso também permite a conexão tooforests em que nem todos os domínios estão disponíveis.
* [Agendador](active-directory-aadconnectsync-feature-scheduler.md) baseia-se no mecanismo de sincronização de toohello.

**Recursos promovidos da visualização tooGA:**

* [Write-back de dispositivo](active-directory-aadconnect-feature-device-writeback.md).
* [Extensões de diretório](active-directory-aadconnectsync-feature-directory-extensions.md).

**Novos recursos de visualização:**

* Olá novo padrão ciclo de sincronização intervalo é de 30 minutos. Usado toobe três horas para todas as versões anteriores. Adiciona suporte toochange Olá [Agendador](active-directory-aadconnectsync-feature-scheduler.md) comportamento.

**Problemas corrigidos:**

* Olá Verifique se a página de domínios DNS não reconheceu sempre domínios hello.
* Solicita credenciais de administrador de domínio ao configurar o AD FS.
* Olá local contas do AD não são reconhecidas pelo Assistente de instalação de saudação se localizado em um domínio com uma árvore diferente de DNS de domínio raiz da saudação.

## <a name="1091310"></a>1.0.9131.0
Lançamento: dezembro de 2015

**Problemas corrigidos:**

* A sincronização de senha poderá não funcionar quando você alterar as senhas no AD DS (Active Directory Domain Services), mas funcionará quando você definir uma senha.
* Quando você tiver um servidor proxy, tooAzure autenticação AD pode falhar durante a instalação, ou se uma atualização for cancelada na página de configuração de saudação.
* A atualização de uma versão anterior do Azure AD Connect com uma instância completa do SQL Server falhará se você não for um SA (administrador do sistema) do SQL Server.
* Atualizando a partir de uma versão anterior do Azure AD Connect com um SQL Server remoto mostra o erro de "não é possível tooaccess Olá banco de dados SQL ADSync" hello.

## <a name="1091250"></a>1.0.9125.0
Lançamento: novembro de 2015

**Novos recursos:**

* Pode reconfigurar a confiança do AD FS tooAzure AD.
* Pode atualizar o esquema do Active Directory hello e regenerar as regras de sincronização.
* Pode desabilitar uma regra de sincronização.
* Pode definir "AuthoritativeNull" como um novo literal em uma regra de sincronização.

**Novos recursos de visualização:**

* [Azure AD Connect Health para sincronização](../connect-health/active-directory-aadconnect-health-sync.md).
* Suporte para sincronização de senha dos [Serviços de Domínio do AD do Azure](../active-directory-passwords-update-your-own-password.md) .

**Novo cenário com suporte:**

* Dá suporte a várias organizações local do Exchange. Para obter mais informações, confira [Implantações híbridas com várias florestas do Active Directory](https://technet.microsoft.com/library/jj873754.aspx).

**Problemas corrigidos:**

* Problemas de sincronização de senha:
  * Um objeto movido de escopo fora do escopo tooin não terão sua senha sincronizada. Isso inclui a UO e a filtragem de atributo.
  * Selecionar um novo tooinclude OU em sincronização não exige uma sincronização completa de senha.
  * Quando um usuário desabilitado é habilitado senha Olá não sincronizados.
  * fila de repetição de senha Olá é infinita e limite de saudação anterior de 5.000 toobe objetos obsoleto foi removido.
* Não é possível tooconnect tooActive diretório com o nível funcional de floresta do Windows Server 2016.
* Grupo de saudação toochange não é possível que é usado para filtragem de grupo após a instalação inicial do hello.
* Não cria um novo perfil de usuário no servidor do Azure AD Connect Olá para cada usuário fazer uma alteração de senha com write-back de senha habilitada.
* Não é possível toouse inteiro longo valores escopos de regras em sincronia.
* caixa de seleção Hello "write-back de dispositivo" permanecerá desabilitada se houver controladores de domínio inacessível.

## <a name="1086670"></a>1.0.8667.0
Lançamento: agosto de 2015

**Novos recursos:**

* saudação do Azure AD Connect, o Assistente de instalação está localizada tooall idiomas do Windows Server.
* Suporte adicionado para desbloqueio de contas ao usar o gerenciamento de senhas do AD do Azure.

**Problemas corrigidos:**

* Assistente de instalação do Azure AD Connect falha se outro usuário continuar a instalação, em vez de saudação pessoa iniciado pela primeira vez a instalação de saudação.
* Se uma desinstalação anterior do Azure AD Connect não toouninstall do Azure AD Connect sincronização corretamente, não é possível tooreinstall.
* Não é possível instalar o Azure AD Connect usando a instalação expressa se usuário Olá não está no domínio raiz da saudação da floresta de saudação ou se uma versão diferente do inglês do Active Directory é usada.
* Se Olá FQDN do hello conta de usuário do Active Directory não pode ser resolvido, é mostrada uma mensagem de erro enganoso ""falha toocommit hello esquema.
* Se conta Olá usada em Olá conector do Active Directory foi alterada fora Olá assistente, o Assistente de saudação falhará em execuções subsequentes.
* Às vezes, o Azure AD Connect não tooinstall em um controlador de domínio.
* Não é possível habilitar e desabilitar o "Modo de preparo" se os atributos de extensão forem adicionados.
* Write-back de senha falha em algumas configurações devido a uma senha incorreta no hello conector do Active Directory.
* DirSync não poderá ser atualizado se um DN (nome diferenciado) for usado na filtragem de atributos.
* Uso excessivo de CPU ao usar a redefinição de senha.

**Recursos de visualização removidos:**

* o recurso de visualização Olá [write-back de usuário](active-directory-aadconnect-feature-preview.md#user-writeback) temporariamente foi removida com base nos comentários de nossos clientes de visualização. Ele será adicionado novamente mais tarde depois abordamos Olá fornecido comentários.

## <a name="1086410"></a>1.0.8641.0
Lançamento: junho de 2015

**Versão inicial do Azure AD Connect.**

Nome alterado de tooAzure de sincronização do AD do Azure AD Connect.

**Novos recursos:**

* Instalação das [configurações expressas](active-directory-aadconnect-get-started-express.md)
* Pode [configurar o AD FS](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs)
* É possível [atualizar do DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md)
* [Impedir exclusões acidentais](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)
* Apresentação do [modo de preparo](active-directory-aadconnectsync-operations.md#staging-mode)

**Novos recursos de visualização:**

* [Write-back de usuário](active-directory-aadconnect-feature-preview.md#user-writeback)
* [Write-back de grupo](active-directory-aadconnect-feature-preview.md#group-writeback)
* [Write-back de dispositivo](active-directory-aadconnect-feature-device-writeback.md)
* [Extensões de diretório](active-directory-aadconnect-feature-preview.md)

## <a name="104940501"></a>1.0.494.0501
Lançamento: maio de 2015

**Novo Requisito:**

* Agora, o Azure AD Sync exige saudação do .NET Framework versão 4.5.1 toobe instalado.

**Problemas corrigidos:**

* O write-back de senha do Azure AD está falhando com um erro de conectividade do Barramento de Serviço do Azure.

## <a name="104910413"></a>1.0.491.0413
Lançamento: abril de 2015

**Problemas corrigidos e aperfeiçoamentos:**

* Olá conector do Active Directory não processa exclusões corretamente se Olá Lixeira estiver habilitada e existirem vários domínios na floresta de saudação.
* Olá desempenho das operações de importação foi aprimorado para hello Azure Active Directory Connector.
* Quando um grupo excedeu o limite de associação de saudação (por padrão, o limite de saudação é definido too50, 000 objetos), Olá grupo foi excluído no Active Directory do Azure. Com o novo comportamento de Olá, Olá grupo não será excluído, um erro será gerado e alteração de associação não é exportadas.
* Não é possível provisionar um novo objeto se uma exclusão de preparo com hello que mesmo DN já está presente no espaço do conector hello.
* Alguns objetos são marcados para sincronização durante uma sincronização delta, embora não exista nenhuma alteração preparada em objeto hello.
* Forçar uma sincronização de senha também remove Olá preferido DC.
* CSExportAnalyzer tem problemas com alguns estados de objetos.

**Novos recursos:**

* Uma junção agora pode se conectar muito "qualquer" tipo de objeto em Olá MV.

## <a name="104850222"></a>1.0.485.0222
Lançamento: fevereiro de 2015

**Aperfeiçoamentos:**

* Desempenho aprimorado de importação.

**Problemas corrigidos:**

* Sincronização de senhas respeita o atributo cloudFiltered Olá que é usado pela filtragem de atributos. Os objetos filtrados não estão mais no escopo de sincronização de senha.
* Em situações raras em que a topologia de saudação tinha muitos controladores de domínio, a sincronização de senha não funciona.
* "Servidor interrompido" durante a importação de saudação conector AD do Azure depois de gerenciamento de dispositivo foi habilitada no AD do Azure/Intune.
* Ingressar FSPs (Entidades de Segurança Externa) de vários domínios na mesma floresta causa um erro de ingresso ambíguo.

## <a name="104751202"></a>1.0.475.1202
Lançamento: dezembro de 2014

**Novos recursos:**

* Agora há suporte para a sincronização de senhas com filtragem baseada em atributo. Para obter mais informações, confira [Sincronização de senha com filtragem](active-directory-aadconnectsync-configure-filtering.md).
* atributo de msDS-ExternalDirectoryObjectID Hello será gravado tooActive Directory. Esse recurso adiciona suporte a aplicativos do Office 365. Ele usa OAuth2 tooaccess caixas de correio locais e Online em uma implantação híbrida do Exchange.

**Problemas de atualização corrigidos:**

* Uma versão mais recente do Assistente de entrada hello está disponível no servidor de saudação.
* Um caminho de instalação personalizado foi usado tooinstall sincronização do AD do Azure.
* Uma atualização de Olá de blocos de critério inválido de junção personalizada.

**Outras correções:**

* Modelos de Olá fixo para o Office Pro Plus.
* Foram corrigidos os problemas de instalação causados por nomes de usuário que começam com um traço.
* Fixa perdedora Olá sourceAnchor configuração ao executar o Assistente de instalação de saudação uma segunda vez.
* Rastreamento ETW fixo para a sincronização de senha corrigido.

## <a name="104701023"></a>1.0.470.1023
Lançamento: outubro de 2014

**Novos recursos:**

* A sincronização de senha de vários locais do Active Directory tooAzure AD.
* Instalação localizado da interface do usuário tooall idiomas do Windows Server.

**Atualizando do AADSync 1.0 GA**

Se você já tiver o Azure AD Sync instalado, há uma etapa adicional que você tenha tootake caso você tiver alterado as regras de sincronização de fora da caixa de saudação. Depois de ter atualizado versão toohello 1.0.470.1023, as regras de sincronização de saudação que você modificou são duplicadas. Para cada regra de sincronização modificada, Olá a seguir:

1.  Localize a regra de sincronização de saudação modificou e anote as alterações de saudação.
* Exclua regra de sincronização de saudação.
* Localize Olá nova regra de sincronização que é criada pelo Azure AD Sync e reaplique as alterações de saudação.

**Permissões para Olá conta do Active Directory**

Olá conta do Active Directory deve ser concedida hashes de senha permissões adicionais toobe tooread capaz de saudação do Active Directory. Olá permissões toogrant são chamados de "Replicar alterações de diretório" e "Directory replicando todas as alterações." As permissões são hashes de senha necessária toobe tooread capaz de saudação.

## <a name="104190911"></a>1.0.419.0911
Lançamento: setembro de 2014

**Versão inicial do Azure AD Sync.**

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre [Como integrar suas identidades locais ao Active Directory do Azure](active-directory-aadconnect.md).
