---
title: "a sincronização de senha aaaTroubleshoot com a sincronização do Azure AD Connect | Microsoft Docs"
description: "Este artigo fornece informações sobre como tootroubleshoot problemas de sincronização de senha."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 390eafec792cb39251627c14cb754f8bb30035b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-password-synchronization-with-azure-ad-connect-sync"></a>Solução de problemas de sincronização de senha com a sincronização do Azure AD Connect
Este tópico fornece etapas para como tootroubleshoot problemas de sincronização de senha. Se as senhas não estiverem sincronizando conforme o esperado, isso poderá ocorrer para um subconjunto de usuários ou para todos os usuários. Para o Azure Active Directory (AD do Azure) conecte-se a implantação com a versão 1.1.524.0 ou posterior, agora há um cmdlet de diagnóstico que você pode usar tootroubleshoot problemas de sincronização de senha:

* Se você tiver um problema em que nenhum senhas são sincronizadas, consulte toohello [nenhum senhas são sincronizadas: solucionar problemas usando o cmdlet de diagnóstico Olá](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) seção.

* Se você tiver um problema com os objetos individuais, consulte toohello [um objeto não está sincronizando senhas: solucionar problemas usando o cmdlet de diagnóstico Olá](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) seção.

Para versões mais antigas de implantação do Azure AD Connect:

* Se você tiver um problema em que nenhum senhas são sincronizadas, consulte toohello [nenhum senhas são sincronizadas: manual, as etapas de solução de problemas](#no-passwords-are-synchronized-manual-troubleshooting-steps) seção.

* Se você tiver um problema com os objetos individuais, consulte toohello [um objeto não está sincronizando senhas: manual, as etapas de solução de problemas](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) seção.

## <a name="no-passwords-are-synchronized-troubleshoot-by-using-hello-diagnostic-cmdlet"></a>Sem as senhas são sincronizadas: solucionar problemas usando o cmdlet de diagnóstico Olá
Você pode usar o hello `Invoke-ADSyncDiagnostics` toofigure cmdlet out por que não há senhas são sincronizadas.

> [!NOTE]
> Olá `Invoke-ADSyncDiagnostics` cmdlet está disponível apenas para o Azure AD Connect versão 1.1.524.0 ou posterior.

### <a name="run-hello-diagnostics-cmdlet"></a>Execute o cmdlet de diagnóstico de saudação
problemas de tootroubleshoot onde nenhum senhas são sincronizadas:

1. Abra uma nova sessão do Windows PowerShell no seu servidor do Azure AD Connect com hello **executar como administrador** opção.

2. Execute `Set-ExecutionPolicy RemoteSigned` ou `Set-ExecutionPolicy Unrestricted`.

3. Execute `Import-Module ADSyncDiagnostics`.

4. Execute `Invoke-ADSyncDiagnostics -PasswordSync`.

### <a name="understand-hello-results-of-hello-cmdlet"></a>Entender os resultados de saudação do cmdlet Olá
Olá diagnóstico executa Olá verificações a seguir:

* Valida que Olá recurso de sincronização de senha está habilitado para seu locatário do AD do Azure.

* Valida que saudação do servidor não está em modo de preparo do Azure AD Connect.

* Para cada local existente conector do Active Directory (que corresponde a floresta do Active Directory existente de tooan):

   * Valida que Olá recurso de sincronização de senha está habilitado.
   
   * Logs de eventos de aplicativo do Windows procura eventos de pulsação de sincronização de senha em hello.

   * Para cada domínio do Active Directory em um conector para Active Directory local hello:

      * Valida que Olá domínio é acessível a partir do servidor de conectar-se de saudação do AD do Azure.

      * Valida que contas de serviços de domínio Active Directory (AD DS) Olá usadas pelo conector para Active Directory local Olá tem correto Olá de nome de usuário, senha e as permissões necessárias para a sincronização de senha.

Olá diagrama a seguir ilustra os resultados de saudação do cmdlet Olá para uma topologia do Active Directory local único domínio:

![Saída de diagnóstico da sincronização de senha](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalgeneral.png)

Olá restante desta seção descreve resultados específicos que são retornados pelo cmdlet hello e problemas correspondentes.

#### <a name="password-synchronization-feature-isnt-enabled"></a>O recurso de sincronização de senha não está habilitado
Se você não tiver habilitado a sincronização de senha usando o Assistente do hello Azure AD Connect, Olá erro a seguir será retornada:

![A sincronização de senha não está habilitada](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobaldisabled.png)

#### <a name="azure-ad-connect-server-is-in-staging-mode"></a>O servidor do Azure AD Connect está em modo de preparo
Se o servidor do Azure AD Connect hello está em modo de preparo, a sincronização de senha está temporariamente desabilitada e hello seguinte erro será retornado:

![O servidor do Azure AD Connect está em modo de preparo](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalstaging.png)

#### <a name="no-password-synchronization-heartbeat-events"></a>Nenhum evento de pulsação de sincronização de senha
Cada Active Directory Connector local tem seu próprio canal de sincronização de senha. Quando Olá canal de sincronização de senha é estabelecido e não existem quaisquer toobe de alterações de senha sincronizada, um evento de pulsação (EventId 654) é gerado uma vez a cada 30 minutos em Olá Log de eventos de aplicativo do Windows. Para cada conector do Active Directory local, Olá cmdlet procura por eventos de pulsação correspondentes no hello últimos três horas. Se nenhum evento de pulsação é encontrado, hello seguinte erro será retornado:

![Nenhum evento de pulsação de sincronização de senha](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalnoheartbeat.png)

#### <a name="ad-ds-account-does-not-have-correct-permissions"></a>A conta do AD DS não tem as permissões corretas
Se a conta de saudação AD DS que é usada pelo Olá local hashes de senha do Active Directory connector toosynchronize não tem as permissões apropriadas Olá, hello seguinte erro será retornado:

![Credenciais incorretas](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectpermission.png)

#### <a name="incorrect-ad-ds-account-username-or-password"></a>Nome de usuário ou senha incorreta da conta do AD DS
Se o hello AD DS conta usada pelo hello hashes de senha local do Active Directory connector toosynchronize tem um nome de usuário incorreto ou a senha, hello seguinte erro será retornado:

![Credenciais incorretas](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectcredential.png)

## <a name="one-object-is-not-synchronizing-passwords-troubleshoot-by-using-hello-diagnostic-cmdlet"></a>Um objeto não está sincronizando senhas: solucionar problemas usando o cmdlet de diagnóstico Olá
Você pode usar o hello `Invoke-ADSyncDiagnostics` toodetermine cmdlet por que um objeto não está sincronizando senhas.

> [!NOTE]
> Olá `Invoke-ADSyncDiagnostics` cmdlet está disponível apenas para o Azure AD Connect versão 1.1.524.0 ou posterior.

### <a name="run-hello-diagnostics-cmdlet"></a>Execute o cmdlet de diagnóstico de saudação
problemas de tootroubleshoot onde nenhum senhas são sincronizadas:

1. Abra uma nova sessão do Windows PowerShell no seu servidor do Azure AD Connect com hello **executar como administrador** opção.

2. Execute `Set-ExecutionPolicy RemoteSigned` ou `Set-ExecutionPolicy Unrestricted`.

3. Execute `Import-Module ADSyncDiagnostics`.

4. Execute Olá cmdlet a seguir:
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName <Name-of-AD-Connector> -DistinguishedName <DistinguishedName-of-AD-object>
   ```
   Por exemplo:
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName "contoso.com" -DistinguishedName "CN=TestUserCN=Users,DC=contoso,DC=com"
   ```

### <a name="understand-hello-results-of-hello-cmdlet"></a>Entender os resultados de saudação do cmdlet Olá
Olá diagnóstico executa Olá verificações a seguir:

* Examina o estado de saudação do objeto do Active Directory Olá no espaço do conector do Active Directory hello, o metaverso e o Azure espaço do conector AD.

* Valida que não existem regras de sincronização com a sincronização de senha habilitada e aplicada de objeto do Active Directory toohello.

* Tentativas de tooretrieve e exibir resultados de Olá Olá última tentativa toosynchronize Olá password para objeto hello.

Olá diagrama a seguir ilustra os resultados de Olá Olá cmdlet, ao solucionar problemas de sincronização de senha para um único objeto:

![Saída de diagnóstico da sincronização de senha – objeto único](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectgeneral.png)

Olá restante desta seção descreve resultados específicos retornados pelo cmdlet hello e problemas correspondentes.

#### <a name="hello-active-directory-object-isnt-exported-tooazure-ad"></a>saudação do Active Directory não está tooAzure exportado AD
Sincronização de senha para essa conta do Active Directory local falhará porque não há nenhum objeto correspondente no locatário do AD do Azure hello. saudação de erro a seguir será retornada:

![Objeto do Azure AD está ausente](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnotexported.png)

#### <a name="user-has-a-temporary-password"></a>O usuário tem uma senha temporária
Atualmente, o Azure AD Connect não dá suporte à sincronização de senhas temporárias com o Azure AD. Uma senha é considerada toobe temporário se hello **alterar a senha no próximo logon** opção é definida no usuário do hello local do Active Directory. saudação de erro a seguir será retornada:

![A senha temporária não é exportada](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjecttemporarypassword.png)

#### <a name="results-of-last-attempt-toosynchronize-password-arent-available"></a>Resultados da última tentativa de toosynchronize senha não estão disponíveis
Por padrão, o Azure AD Connect armazena resultados Olá de tentativas de sincronização de senha por sete dias. Se não houver nenhum resultado disponível para o objeto do Active Directory Olá selecionado, Olá aviso a seguir será retornada:

![Saída de diagnóstico de um único objeto – nenhum histórico de sincronização de senha](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnohistory.png)


## <a name="no-passwords-are-synchronized-manual-troubleshooting-steps"></a>Nenhuma senha é sincronizada: etapas manuais de solução de problemas
Siga essas toodetermine etapas porque não há senhas são sincronizadas:

1. É servidor conectar Olá [modo de preparo](active-directory-aadconnectsync-operations.md#staging-mode)? Um servidor no modo de preparo não sincroniza nenhuma senha.

2. Executar script Olá Olá [obter status de saudação de configurações de sincronização de senha](#get-the-status-of-password-sync-settings) seção. Ele fornece uma visão geral da configuração de sincronização de senha hello.  

    ![Saída de script do PowerShell das configurações de sincronização de senha](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/psverifyconfig.png)  

3. Se o recurso de saudação não está habilitado no AD do Azure ou se Olá status de canal de sincronização não está habilitado, execute o Assistente de instalação de conectar-se de saudação. Selecione **Personalizar opções de sincronização**e desmarque a sincronização de senha. Essa alteração desabilita temporariamente o recurso de saudação. Em seguida, execute novamente o Assistente de saudação e habilite novamente a sincronização de senha. Execute o script hello novamente tooverify que Olá configuração está correta.

4. Procure no log de eventos de saudação para erros. Procure Olá eventos, o que poderia indicar um problema a seguir:
    * Fonte: “Sincronização de diretório” ID: 0, 611, 652, 655 Se um desses eventos aparecer, há um problema de conectividade. mensagem de saudação do log de eventos contém informações sobre a floresta em que você tem um problema. Para obter mais informações, consulte [Problema de conectividade](#connectivity problem).

5. Se não aparecer nenhuma pulsação ou se nada mais funcionou, execute [Disparar uma sincronização completa de todas as senhas](#trigger-a-full-sync-of-all-passwords). Execute o script hello apenas uma vez.

6. Consulte Olá [solucionar problemas de um objeto que não está sincronizando senhas](#one-object-is-not-synchronizing-passwords) seção.

### <a name="connectivity-problems"></a>Problemas de conectividade

Você tem conectividade com o Azure AD?

Conta Olá exigi hashes de senha de saudação permissões tooread em todos os domínios? Se você instalou conectar usando as configurações Express, permissões de saudação já devem estar corretas. 

Se você usou a instalação personalizada, defina as permissões de saudação manualmente fazendo Olá seguinte:
    
1. conta de saudação toofind usada pelo conector do Active Directory hello, início **Synchronization Service Manager**. 
 
2. Vá muito**conectores**e em seguida, procure a floresta de Active Directory local Olá solução de problemas. 
 
3. Selecione o conector hello e, em seguida, clique em **propriedades**. 
 
4. Vá muito**conectar-se a floresta do diretório tooActive**.  
    
    ![Conta usada pelo Active Directory Connector](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/connectoraccount.png)  
    Observe Olá nome de usuário e domínio Olá onde Olá conta está localizada.
    
5. Iniciar **computadores e usuários do Active Directory**e, em seguida, verifique se que conta Olá você encontrou anteriormente tem permissões de acompanhamento de Olá definidas na raiz de saudação de todos os domínios na floresta:
    * Replicar alterações de diretório
    * Replicar todas as alterações de diretório

6. É Olá controladores de domínio pode ser acessados pelo Azure AD Connect? Se o servidor de conectar Olá não pode se conectar a controladores de domínio tooall, configurar **usar somente o controlador de domínio preferencial**.  
    
    ![Controlador de domínio usado pelo Active Directory Connector](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/preferreddc.png)  
    
7. Voltar muito**Synchronization Service Manager** e **configurar a partição de diretório**. 
 
8. Selecione o domínio no **selecionar partições de diretório**, selecione Olá **usam somente controladores de domínio preferencial** caixa de seleção e, em seguida, clique em **configurar**. 

9. Na lista de hello, insira os controladores de domínio Olá conectar deve usar para sincronização de senha. Olá mesma lista é usada para importar e exportar também. Siga estas etapas para todos os domínios.

10. Se o script hello mostra que não há nenhuma pulsação, execute o script de saudação [disparar uma sincronização completa de todas as senhas](#trigger-a-full-sync-of-all-passwords).

## <a name="one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps"></a>Um objeto não está sincronizando senhas: etapas manuais de solução de problemas
Facilmente, você pode solucionar problemas de sincronização de senha, revisando o status de saudação de um objeto.

1. Em **computadores e usuários do Active Directory**, pesquisar por usuário hello e, em seguida, verifique se esse Olá **usuário deve alterar a senha no próximo logon** caixa de seleção é desmarcada.  

    ![Senhas produtivas do Active Directory](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/adprodpassword.png)  

    Se Olá caixa é selecionada, peça Olá usuário toosign em e alterar a senha de saudação. As senhas temporárias não são sincronizadas com o Azure AD.

2. Se a senha Olá parece correta no Active Directory, execute usuário Olá no mecanismo de sincronização de saudação. Por usuário Olá seguinte do local do Active Directory tooAzure AD, você pode ver se há um erro descritivo no objeto de saudação.

    a. Iniciar Olá [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).

    b. Clique em **Conectores**.

    c. Selecione Olá **conector do Active Directory** onde Olá usuário está localizado.

    d. Selecione **Pesquisar Espaço do Conector**.

    e. Em Olá **escopo** selecione **DN ou âncora**e, em seguida, insira DN completo de saudação do usuário Olá solução de problemas.

    ![Pesquisar por usuário no espaço do conector com DN](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/searchcs.png)  

    f. Localizar usuário Olá você está procurando e, em seguida, clique em **propriedades** toosee Olá a todos os atributos. Se o usuário Olá não estiver no resultado da pesquisa Olá, verifique se o [regras de filtragem](active-directory-aadconnectsync-configure-filtering.md) e certifique-se de que você execute [aplicar e verifique se as alterações](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) para Olá usuário tooappear em conectar.

    g. detalhes de sincronização de senha toosee saudação do objeto Olá Olá semana passada, clique **Log**.  

    ![Detalhes do log do objeto](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/csobjectlog.png)  

    Se o log de objeto Olá estiver vazio, o Azure AD Connect foi hash de senha não é possível tooread Olá do Active Directory. Continue a solução de problemas com [Erros de conectividade](#connectivity-errors). Se você vir qualquer outro valor que **êxito**, consulte a tabela toohello [log de sincronização de senha](#password-sync-log).

    h. Selecione Olá **linhagem** guia e verifique se essa regra de pelo menos uma sincronização em Olá **PasswordSync** coluna é **True**. Configuração padrão de hello, Olá nome da regra de sincronização de saudação é **em do AD - Useraccountenabled**.  

    ![Informações de linhagem de um usuário](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync.png)  

    i. Clique em **propriedades de objeto do metaverso** toodisplay uma lista de atributos de usuário.  

    ![Informações de metaverso](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvpasswordsync.png)  

    Verifique se não há nenhum atributo **cloudFiltered** presente. Certifique-se de que os atributos de domínio de saudação (domainFQDN e domainNetBios) têm valores esperados de saudação.

    j. Clique em Olá **conectores** guia. Certifique-se de que você vê os conectores tooboth do Active Directory local e o Azure AD.

    ![Informações de metaverso](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvconnectors.png)  

    k. Linha de saudação Select que representa o AD do Azure, clique em **propriedades**e, em seguida, clique em Olá **linhagem** objeto de espaço do conector de saudação de guia deve ter uma regra de saída em Olá **PasswordSync** coluna definida muito**True**. Configuração padrão de hello, Olá nome da regra de sincronização de saudação é **Out tooAAD - ingresso de usuário**.  

    ![Caixa de diálogo Propriedades do objeto de espaço do conector](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync2.png)  

### <a name="password-sync-log"></a>Log de sincronização de senha
coluna de status de saudação pode ter Olá valores a seguir:

| Status | Descrição |
| --- | --- |
| Sucesso |A senha foi sincronizada com êxito. |
| FilteredByTarget |Senha está definida muito**usuário deve alterar a senha no próximo logon**. A senha não foi sincronizada. |
| NoTargetConnection |Nenhum objeto no metaverso hello, ou no espaço do conector de saudação do AD do Azure. |
| SourceConnectorNotPresent |Nenhum objeto encontrado no espaço do conector Olá local do Active Directory. |
| TargetNotExportedToDirectory |objeto Olá Olá espaço do conector AD do Azure ainda não foram exportado. |
| MigratedCheckDetailsForMoreInfo |A entrada de log foi criada antes da versão 1.0.9125.0 e é mostrada em seu estado herdado. |
| Erro |O serviço retornou um erro desconhecido. |
| Desconhecido |Ocorreu um erro durante a tentativa de tooprocess um lote de hashes de senha.  |
| MissingAttribute |Atributos específicos (por exemplo, o hash de Kerberos) exigidos pelos Azure AD Domain Services não estão disponíveis. |
| RetryRequestedByTarget |Atributos específicos (por exemplo, o hash de Kerberos) exigidos pelos Azure AD Domain Services não estavam disponíveis anteriormente. É feita uma tentativa de tooresynchronize saudação do hash de senha. |

## <a name="scripts-toohelp-troubleshooting"></a>Solução de problemas de toohelp de scripts

### <a name="get-hello-status-of-password-sync-settings"></a>Obter status de saudação de configurações de sincronização de senha
```
Import-Module ADSync
$connectors = Get-ADSyncConnector
$aadConnectors = $connectors | Where-Object {$_.SubType -eq "Windows Azure Active Directory (Microsoft)"}
$adConnectors = $connectors | Where-Object {$_.ConnectorTypeName -eq "AD"}
if ($aadConnectors -ne $null -and $adConnectors -ne $null)
{
    if ($aadConnectors.Count -eq 1)
    {
        $features = Get-ADSyncAADCompanyFeature -ConnectorName $aadConnectors[0].Name
        Write-Host
        Write-Host "Password sync feature enabled in your Azure AD directory: "  $features.PasswordHashSync
        foreach ($adConnector in $adConnectors)
        {
            Write-Host
            Write-Host "Password sync channel status BEGIN ------------------------------------------------------- "
            Write-Host
            Get-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector.Name
            Write-Host
            $pingEvents =
                Get-EventLog -LogName "Application" -Source "Directory Synchronization" -InstanceId 654  -After (Get-Date).AddHours(-3) |
                    Where-Object { $_.Message.ToUpperInvariant().Contains($adConnector.Identifier.ToString("D").ToUpperInvariant()) } |
                    Sort-Object { $_.Time } -Descending
            if ($pingEvents -ne $null)
            {
                Write-Host "Latest heart beat event (within last 3 hours). Time " $pingEvents[0].TimeWritten
            }
            else
            {
                Write-Warning "No ping event found within last 3 hours."
            }
            Write-Host
            Write-Host "Password sync channel status END ------------------------------------------------------- "
            Write-Host
        }
    }
    else
    {
        Write-Warning "More than one Azure AD Connectors found. Please update hello script toouse hello appropriate Connector."
    }
}
Write-Host
if ($aadConnectors -eq $null)
{
    Write-Warning "No Azure AD Connector was found."
}
if ($adConnectors -eq $null)
{
    Write-Warning "No AD DS Connector was found."
}
Write-Host
```

#### <a name="trigger-a-full-sync-of-all-passwords"></a>Disparar uma sincronização completa de todas as senhas
> [!NOTE]
> Execute este script apenas uma vez. Se você precisar toorun-mais de uma vez, algo é problema hello. tootroubleshoot Olá problema, contate o suporte da Microsoft.

Você pode disparar uma sincronização completa de todas as senhas usando Olá script a seguir:

```
$adConnector = "<CASE SENSITIVE AD CONNECTOR NAME>"
$aadConnector = "<CASE SENSITIVE AAD CONNECTOR NAME>"
Import-Module adsync
$c = Get-ADSyncConnector -Name $adConnector
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter "Microsoft.Synchronize.ForceFullPasswordSync", String, ConnectorGlobal, $null, $null, $null
$p.Value = 1
$c.GlobalParameters.Remove($p.Name)
$c.GlobalParameters.Add($p)
$c = Add-ADSyncConnector -Connector $c
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $false
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $true
```

## <a name="next-steps"></a>Próximas etapas
* [Implementação de sincronização de senha com a sincronização do Azure AD Connect](active-directory-aadconnectsync-implement-password-synchronization.md)
* [Sincronização do Azure AD Connect: personalizando as opções de sincronização](active-directory-aadconnectsync-whatis.md)
* [Integração de suas identidades locais com o Active Directory do Azure](active-directory-aadconnect.md)
