---
title: "instalação do agente de integridade de conexão aaaAzure AD | Microsoft Docs"
description: "Esta é hello Azure AD Connect Health página que descreve a instalação do agente de saudação do AD FS e sincronização."
services: active-directory
documentationcenter: 
author: karavar
manager: samueld
editor: curtand
ms.assetid: 1cc8ae90-607d-4925-9c30-6770a4bd1b4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 9019628ec1d4c477496e08910cfd668ed1933a62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-health-agent-installation"></a>Instalação do Agente do Azure AD Connect Health
Este documento orienta você por instalando e Configurando agentes de integridade de conectar-se de saudação do AD do Azure. Você pode baixar os agentes de saudação do [aqui](active-directory-aadconnect-health.md#download-and-install-azure-ad-connect-health-agent).

## <a name="requirements"></a>Requisitos
Olá, a tabela a seguir é uma lista de requisitos para usar o Azure AD Connect Health.

| Requisito | Descrição |
| --- | --- |
| AD Premium do Azure |O Azure AD Connect Health é um recurso do Azure AD Premium e requer o Azure AD Premium. </br></br>Para saber mais, consulte [Introdução ao AD Premium do Azure](../active-directory-get-started-premium.md) </br>toostart uma avaliação gratuita de 30 dias, consulte [iniciar uma avaliação.](https://azure.microsoft.com/trial/get-started-active-directory/) |
| Você deve ser um global administrador do seu AD do Azure tooget Introdução ao Azure AD Connect Health |Por padrão, somente os administradores globais do hello podem instalar e configurar Olá integridade tooget da agentes iniciado, portal de saudação de acesso e realizar operações no Azure AD Connect Health. Para saber mais, consulte [Administrar seu diretório do Azure AD](../active-directory-administer.md). <br><br> Usando o controle de acesso baseado em função você pode permitir acesso aos usuários do tooAzure AD Connect Health tooother em sua organização. Para saber mais, confira [Controle de Acesso com Base em Função para o Azure AD Connect Health.](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control) </br></br>**Importante:** Olá conta usada durante a instalação de agentes Olá deve ser uma conta corporativa ou de estudante. Não pode ser uma conta da Microsoft. Para saber mais, confira [Inscrever-se no Azure como uma organização](../sign-up-organization.md) |
| O Agente do Azure AD Connect Health é instalado em cada servidor de destino | Azure AD Connect Health requer Olá agentes de integridade toobe instalado e configurado em dados de saudação do tooreceive de servidores de destino e fornece recursos de monitoramento e análise de saudação </br></br>Por exemplo, dados tooget da infraestrutura do AD FS, o agente de saudação devem ser instalados em saudação do AD FS e servidores de Proxy de aplicativo Web. Da mesma forma, os dados tooget em suas instalações infraestrutura do AD DS, Olá agente deve ser instalado em controladores de domínio de saudação. </br></br> |
| Pontos de extremidade de serviço do Azure de toohello conectividade de saída | Durante a instalação e o tempo de execução, o agente de saudação requer conectividade tooAzure AD Connect Health pontos de extremidade. Se a conectividade de saída está bloqueada usando Firewalls, certifique-se de que Olá pontos de extremidade a seguir são adicionadas toohello lista de permissões: </br></br><li>&#42;.blob.core.windows.net </li><li>&#42;.servicebus.windows.net - Port: 5671 </li><li>&#42;.adhybridhealth.azure.com/</li><li>https://management.azure.com </li><li>https://policykeyservice.dc.ad.msft.net/</li><li>https://login.windows.net</li><li>https://login.microsoftonline.com</li><li>https://secure.aadcdn.microsoftonline-p.com</li> |
|Conectividade de saída com base em endereços IP | Para IP com base em endereços filtragem nos firewalls, consulte toohello [intervalos de IP Azure](https://www.microsoft.com/en-us/download/details.aspx?id=41653).|
| A inspeção de SSL para tráfego de saída está filtrada ou desabilitada | Olá agente registro etapa ou dados carregamento operações poderão falhar se houver inspeção SSL ou término para o tráfego de saída na camada de rede hello. |
| Portas de firewall no servidor de saudação executando o agente de saudação. |Agente de saudação requer Olá toobe abrir por Olá agente toocommunicate com pontos de extremidade de serviço de integridade do AD do Azure Olá as portas de firewall a seguir.</br></br><li>Porta TCP 443</li><li>Porta TCP 5671</li> |
| Permitir Olá sites a seguir se segurança reforçada do IE estiver habilitada |Se segurança reforçada do IE estiver habilitada, em seguida, hello sites a seguir devem ser permitidas no servidor de saudação que vai toohave Olá agente instalado.</br></br><li>https://login.microsoftonline.com</li><li>https://secure.aadcdn.microsoftonline-p.com</li><li>https://login.windows.net</li><li>servidor de Federação Olá para sua organização confiada pelo Active Directory do Azure. Por exemplo: https://sts.contoso.com</li> |
|Desabilitar FIPS|Não há suporte para FIPS nos agentes do Azure AD Connect Health.|

## <a name="installing-hello-azure-ad-connect-health-agent-for-ad-fs"></a>Instalando Olá agente do Azure AD Connect Health para AD FS
toostart Olá instalação do agente, clique duas vezes no arquivo .exe Olá baixado. Na primeira tela de saudação, clique em instalar.

![Verifique o Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install1.png)

Depois de saudação instalação for concluída, clique em configurar agora.

![Verifique o Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install2.png)

Isso inicia um processo de registro do PowerShell janela tooinitiate Olá agente. Quando solicitado, entre com uma conta do AD do Azure que tem acesso tooperform agente registro. Por padrão, Olá conta de Administrador Global tem acesso.

![Verifique o Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install3.png)

Depois de entrar, o PowerShell continuará. Quando for concluída, você pode fechar o PowerShell e Olá configuração foi concluída.

Neste ponto, hello agente de serviços devem ser automaticamente permitindo Olá agente carregamento Olá necessário dados toohello serviço de nuvem iniciado de forma segura.

Se você não atendidos todos os Olá pré-requisitos descritos nas seções anteriores hello, serão exibidos avisos na janela do PowerShell hello. Ser Olá-se de toocomplete [requisitos](active-directory-aadconnect-health-agent-install.md#requirements) antes de instalar o agente de saudação. Olá captura de tela a seguir é um exemplo desses erros.

![Verifique o Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install4.png)

tooverify Olá agente foi instalado, procure Olá serviços no servidor de saudação a seguir. Se você concluiu a configuração de hello, eles já devem estar executando. Caso contrário, eles estão interrompidos até Olá configuração foi concluída.

* Serviço de diagnóstico do AD FS do Azure AD Connect Health
* Serviço do Insights do AD FS do Azure AD Connect Health
* Serviço de Monitoramento do AD FS do Azure AD Connect Health

![Verifique o Azure AD Connect Health](./media/active-directory-aadconnect-health-requirements/install5.png)

### <a name="agent-installation-on-windows-server-2008-r2-servers"></a>Instalação do agente em servidores do Windows Server 2008 R2
Etapas para servidores Windows Server 2008 R2:

1. Certifique-se de que esse servidor de saudação está em execução no Service Pack 1 ou superior.
2. Desative a ESC do IE para instalação do agente:
3. Instale o Windows PowerShell 4.0 em cada um dos servidores de saudação à frente instalando Olá agente de integridade do AD. tooinstall Windows PowerShell 4.0:
   * Instalar [Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=40779) usando Olá instalador offline do link toodownload Olá a seguir.
   * Instale o PowerShell ISE (de recursos do Windows)
   * Instalar Olá [Windows Management Framework 4.0.](https://www.microsoft.com/download/details.aspx?id=40855)
   * Instale o Internet Explorer versão 10 ou superior no servidor de saudação. (Requerida pela tooauthenticate do serviço de integridade hello, usando suas credenciais de administrador do Azure).
4. Para obter mais informações sobre como instalar o Windows PowerShell 4.0 no Windows Server 2008 R2, consulte o artigo do wiki Olá [aqui](http://social.technet.microsoft.com/wiki/contents/articles/20623.step-by-step-upgrading-the-powershell-version-4-on-2008-r2.aspx).

### <a name="enable-auditing-for-ad-fs"></a>Habilitar a auditoria do AD FS
> [!NOTE]
> Esta seção se aplica somente a servidores tooAD FS. Você não tem toofollow essas etapas em servidores de Proxy de aplicativo Web hello.
>

Para que Olá toogather de recursos de análise de uso e analisar dados, Olá agente do Azure AD Connect Health precisam Olá informações nos Logs de auditoria Olá AD FS. Esses logs não estão habilitados por padrão. Saudação de uso seguindo os procedimentos tooenable AD FS auditoria e toolocate saudação do AD FS auditoria logs, nos servidores do AD FS.

#### <a name="tooenable-auditing-for-ad-fs-on-windows-server-2008-r2"></a>tooenable auditoria do AD FS no Windows Server 2008 R2
1. Clique em **iniciar**, ponto muito**programas**, ponto muito**ferramentas administrativas**e, em seguida, clique em **política de segurança Local**.
2. Navegue toohello **gerenciamento de direitos de políticas de configurações de segurança** pasta e, em seguida, clique duas vezes em Gerar auditorias de segurança.
3. Em Olá **configuração de segurança Local** guia, verifique se a conta de serviço do hello AD FS 2.0 está listada. Se não estiver presente, clique em **adicionar usuário ou grupo** e adicioná-lo toohello lista e, em seguida, clique em **Okey**.
4. auditoria tooenable, abra um prompt de comando com privilégios elevados e execute Olá comando a seguir:<code>auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable</code>
5. Feche a política de segurança Local e, em seguida, abra o snap-in de gerenciamento de saudação. Olá tooopen snap-in de gerenciamento, clique em **iniciar**, ponto muito**programas**, ponto muito**ferramentas administrativas**e, em seguida, clique em AD FS 2.0 Management.
6. No painel de ações de saudação, clique em Editar propriedades do serviço de Federação.
7. Em Olá **propriedades do serviço de Federação** caixa de diálogo, clique em Olá **eventos** guia.
8. Selecione Olá **auditorias com êxito** e **auditorias com falha** caixas de seleção.
9. Clique em **OK**.

#### <a name="tooenable-auditing-for-ad-fs-on-windows-server-2012-r2"></a>tooenable auditoria do AD FS no Windows Server 2012 R2
1. Abra **política de segurança Local** abrindo **Gerenciador do servidor** na tela de início do hello, ou Gerenciador do servidor na barra de tarefas de saudação na área de trabalho hello, em seguida, clique em **política de segurança Local/ferramentas**.
2. Navegue toohello **atribuição de direitos de políticas de configurações de segurança** pasta e, em seguida, clique duas vezes em **gerar auditorias de segurança**.
3. Em Olá **configuração de segurança Local** guia, verifique se a conta de serviço do hello AD FS está listada. Se não estiver presente, clique em **adicionar usuário ou grupo** e adicioná-lo toohello lista e, em seguida, clique em **Okey**.
4. auditoria tooenable, abra um prompt de comando com privilégios elevados e execute Olá comando a seguir: ```auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable```.
5. Fechar **política de segurança Local**e, em seguida, abra Olá **gerenciamento do AD FS** snap-in (no Gerenciador do servidor, clique em ferramentas e, em seguida, selecione Gerenciamento do AD FS).
6. No painel de ações de saudação, clique em **editar propriedades do serviço de Federação**.
7. Na caixa de diálogo de propriedades do serviço de Federação hello, clique em Olá **eventos** guia.
8. Selecione Olá **auditorias com êxito e falha de auditorias** caixas de seleção e, em seguida, clique em **Okey**.

#### <a name="tooenable-auditing-for-ad-fs-on-windows-server-2016"></a>tooenable auditoria do AD FS no Windows Server 2016
1. Abra **política de segurança Local** abrindo **Gerenciador do servidor** na tela de início do hello, ou Gerenciador do servidor na barra de tarefas de saudação na área de trabalho hello, em seguida, clique em **política de segurança Local/ferramentas**.
2. Navegue toohello **atribuição de direitos de políticas de configurações de segurança** pasta e, em seguida, clique duas vezes em **gerar auditorias de segurança**.
3. Em Olá **configuração de segurança Local** guia, verifique se a conta de serviço do hello AD FS está listada. Se não estiver presente, clique em **adicionar usuário ou grupo** Adicionar lista de toohello de conta de serviço do hello AD FS e, em seguida, clique em **Okey**.
4. auditoria tooenable, abra um prompt de comando com privilégios elevados e execute Olá comando a seguir:<code>auditpol.exe /set /subcategory:"Application Generated" /failure:enable /success:enable.</code>
5. Fechar **política de segurança Local**e, em seguida, abra Olá **gerenciamento do AD FS** snap-in (no Gerenciador do servidor, clique em ferramentas e, em seguida, selecione Gerenciamento do AD FS).
6. No painel de ações de saudação, clique em **editar propriedades do serviço de Federação**.
7. Na caixa de diálogo de propriedades do serviço de Federação hello, clique em Olá **eventos** guia.
8. Selecione Olá **auditorias com êxito e falha de auditorias** caixas de seleção e, em seguida, clique em **Okey**. Isso deve ser habilitado por padrão.
9. Abra uma janela do PowerShell e execute Olá comando a seguir: ```Set-AdfsProperties -AuditLevel Verbose```.

Observe que o nível de auditoria "básico" é habilitado por padrão. Leia mais sobre Olá [aprimoramento de auditoria do AD FS no Windows Server 2016](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-fs/operations/auditing-enhancements-to-ad-fs-in-windows-server-2016)


#### <a name="toolocate-hello-ad-fs-audit-logs"></a>logs de auditoria toolocate saudação do AD FS
1. Abra o **Visualizador de Eventos**.
2. Vá tooWindows Logs e selecione **segurança**.
3. Na saudação à direita, clique em **filtrar Logs atuais**.
4. Em Origem do Evento, selecione **Auditoria do AD FS**.

![Logs de auditoria do AD FS](./media/active-directory-aadconnect-health-requirements/adfsaudit.png)

> [!WARNING]
> Uma política de grupo pode desabilitar a auditoria do AD FS. Se a auditoria do AD FS for desabilitada, a análise de uso sobre as atividades de logon não estará disponível. Verifique se você não tem uma política de grupo que desabilite a auditoria do AD FS.>
>


## <a name="installing-hello-azure-ad-connect-health-agent-for-sync"></a>Instalando o agente do hello Azure AD Connect Health para sincronização
Agente de integridade de conexão de saudação do AD do Azure para sincronização é instalado automaticamente na versão mais recente de saudação do Azure AD Connect. toouse do Azure AD Connect para sincronização, você precisa toodownload hello mais recente versão do Azure AD Connect e instalá-lo. Você pode baixar a versão mais recente do hello [aqui](http://www.microsoft.com/download/details.aspx?id=47594).

tooverify Olá agente foi instalado, procure Olá serviços no servidor de saudação a seguir. Se você concluiu a configuração de hello, eles já devem estar executando. Caso contrário, eles estão interrompidos até Olá configuração foi concluída.

* Serviço de Informações do Azure AD Connect Health para Sincronização
* Serviço de Monitoramento do Azure AD Connect Health para Sincronização

![Verificar sincronização do Azure AD Connect Health](./media/active-directory-aadconnect-health-sync/services.png)

> [!NOTE]
> Lembre-se de que usar o Azure AD Connect Health requer o Azure AD Premium. Se você não tiver o Azure AD Premium, você está toocomplete não é possível configuração Olá Olá portal do Azure. Para obter mais informações, consulte Olá [página requisitos](active-directory-aadconnect-health-agent-install.md#requirements).
>
>

## <a name="manual-azure-ad-connect-health-for-sync-registration"></a>Registro manual do Azure AD Connect Health para Sincronização
Se hello Azure AD Connect Health para registro de agente de sincronização falhar após a instalação bem-sucedida do Azure AD Connect, você pode usar o hello toomanually registrar o agente de saudação de comando do PowerShell a seguir.

> [!IMPORTANT]
> Usar esse comando do PowerShell só é necessário se o registro de agente Olá falha após a instalação do Azure AD Connect.
>
>

Olá PowerShell a seguir comando é necessário somente ao registro de agente de integridade de saudação falha mesmo após uma instalação bem-sucedida e a configuração do Azure AD Connect. serviços do Azure AD Connect Health Olá serão iniciada depois que o agente de saudação foi registrado com êxito.

Você pode registrar manualmente o agente de integridade de conexão de saudação do AD do Azure para sincronização usando Olá comando PowerShell a seguir:

`Register-AzureADConnectHealthSyncAgent -AttributeFiltering $false -StagingMode $false`

comando Olá usa parâmetros a seguir:

* AttributeFiltering: $true (padrão) - se do Azure AD Connect não está sincronizando o conjunto de atributos padrão hello e tem sido um atributo filtrado de toouse personalizado definido. Caso contrário, o valor será $false.
* StagingMode: $false (padrão) - se o servidor do Azure AD Connect Olá não está no modo, $true de preparo se o servidor de saudação configurado toobe no modo de preparo.

Quando solicitado a fornecer autenticação usar Olá a mesma conta de administrador global (como admin@domain.onmicrosoft.com) que foi usado para configurar a conexão do AD do Azure.

## <a name="installing-hello-azure-ad-connect-health-agent-for-ad-ds"></a>Instalando Olá agente do Azure AD Connect Health para AD DS
toostart Olá instalação do agente, clique duas vezes no arquivo .exe Olá baixado. Na primeira tela de saudação, clique em instalar.

![Verifique o Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install1.png)

Depois de saudação instalação for concluída, clique em configurar agora.

![Verifique o Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install2.png)

Um prompt de comando será iniciado, seguido pelo PowerShell, que executará Register-AzureADConnectHealthADDSAgent. Quando solicitada toosign em tooAzure, vá em frente e entre.

![Verifique o Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install3.png)

Depois de entrar, o PowerShell continuará. Quando for concluída, você pode fechar o PowerShell e Olá configuração foi concluída.

Neste ponto, os serviços de Olá devem ser iniciados automaticamente permitindo Olá agente toomonitor e coletam dados. Se você não atendidos todos os Olá pré-requisitos descritos nas seções anteriores hello, serão exibidos avisos na janela do PowerShell hello. Ser Olá-se de toocomplete [requisitos](active-directory-aadconnect-health-agent-install.md#requirements) antes de instalar o agente de saudação. Olá captura de tela a seguir é um exemplo desses erros.

![Verificar o Azure AD Connect Health para AD DS](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install4.png)

tooverify Olá agente foi instalado, procure Olá serviços no controlador de domínio Olá a seguir.

* Serviço do Insights do AD DS do Azure AD Connect Health
* Serviço de Monitoramento do AD DS do Azure AD Connect Health

Se você concluiu a configuração de hello, esses serviços já devem estar executando. Caso contrário, eles estão interrompidos até Olá configuração foi concluída.

![Verifique o Azure AD Connect Health](./media/active-directory-aadconnect-health/aadconnect-health-adds-agent-install5.png)


### <a name="agent-registration-using-powershell"></a>Registro de agente usando o PowerShell
Depois de instalar Olá agente apropriado setup.exe, você pode executar a etapa de registro de agente hello usando Olá comandos do PowerShell dependendo da função hello a seguir. Abra uma janela do PowerShell e execute o comando apropriado hello:

```
    Register-AzureADConnectHealthADFSAgent
    Register-AzureADConnectHealthADDSAgent
    Register-AzureADConnectHealthSyncAgent

```

Esses comandos aceitam "Credential" como um registro de saudação do parâmetro toocomplete de modo não interativo ou em um computador Server Core.
* Olá credencial pode ser capturado em uma variável do PowerShell que é passada como um parâmetro.
* Você pode fornecer qualquer identidade de AD do Azure que tenha acesso tooregister Olá agentes e não tem MFA habilitado.
* Por padrão, os administradores globais têm acesso tooperform registro de agente. Você também pode permitir que outros menos tooperform de identidades com privilégios nesta etapa. Leia mais sobre [Controle de acesso com base em função](active-directory-aadconnect-health-operations.md#manage-access-with-role-based-access-control).

```
    $cred = Get-Credential
    Register-AzureADConnectHealthADFSAgent -Credential $cred

```

## <a name="configure-azure-ad-connect-health-agents-toouse-http-proxy"></a>Configurar agentes de integridade de conexão de AD do Azure toouse HTTP Proxy
Você pode configurar os agentes de integridade de conexão de AD do Azure toowork com um HTTP Proxy.

> [!NOTE]
> * Usar "ProxyServerAddress de configuração Netsh WinHttp" não é suportado como agente Olá usa System.Net solicitações de web de toomake em vez de Microsoft Windows HTTP Services.
> * Olá, endereço de Http Proxy configurado é usado por meio do toopass Https mensagens criptografadas.
> * Não há suporte para proxies autenticados (usando HTTPBasic).
>
>

### <a name="change-health-agent-proxy-configuration"></a>Alterar a configuração de proxy do agente de integridade
Você tem Olá opções tooconfigure AD do Azure agente de integridade de conexão toouse um HTTP Proxy a seguir.

> [!NOTE]
> Todos os serviços do agente de integridade do Azure do AD Connect devem ser reiniciados para que Olá toobe de configurações de proxy atualizada. Execute Olá comando a seguir:<br>
> Restart-Service AdHealth*
>
>

#### <a name="import-existing-proxy-settings"></a>Importar configurações de proxy existentes
##### <a name="import-from-internet-explorer"></a>Importar do Internet Explorer
Configurações de proxy do Internet Explorer HTTP podem ser importadas, toobe usados pelo Olá agentes de integridade de conexão de AD do Azure. Em cada um dos servidores de Olá executando o agente de integridade de saudação, execute Olá comando PowerShell a seguir:

    Set-AzureAdConnectHealthProxySettings -ImportFromInternetSettings

##### <a name="import-from-winhttp"></a>Importar do WinHTTP
Configurações de proxy WinHTTP podem ser importadas, toobe usados pelo Olá agentes de integridade de conexão de AD do Azure. Em cada um dos servidores de Olá executando o agente de integridade de saudação, execute Olá comando PowerShell a seguir:

    Set-AzureAdConnectHealthProxySettings -ImportFromWinHttp

#### <a name="specify-proxy-addresses-manually"></a>Especificar endereços de Proxy manualmente
Você pode especificar manualmente um servidor proxy em cada servidor de saudação executando Olá agente de integridade, executando Olá comando PowerShell a seguir:

    Set-AzureAdConnectHealthProxySettings -HttpsProxyAddress address:port

Exemplo: *Set-AzureAdConnectHealthProxySettings -HttpsProxyAddress myproxyserver:443*

* "address" pode ser um nome do servidor DNS que pode ser resolvido ou um endereço IPv4
* "port" pode ser omitida. Se omitida, 443 é escolhida como a porta padrão.

#### <a name="clear-existing-proxy-configuration"></a>Limpar a configuração de proxy existente
Você pode desmarcar a configuração de proxy existente Olá executando Olá comando a seguir:

    Set-AzureAdConnectHealthProxySettings -NoProxy


### <a name="read-current-proxy-settings"></a>Ler configurações de proxy atuais
Você pode ler as configurações de proxy de saudação configurada atualmente executando Olá comando a seguir:

    Get-AzureAdConnectHealthProxySettings


## <a name="test-connectivity-tooazure-ad-connect-health-service"></a>Testar conectividade tooAzure AD conectar-se o serviço de integridade
É possível que problemas podem surgir que causam o agente do Azure AD Connect Health Olá toolose conectividade com o serviço de integridade de conexão de saudação do AD do Azure. Isso inclui problemas de rede, problemas de permissão, entre vários outros.

Se o agente de saudação toosend não é possível data toohello do Azure AD Connect Health service para mais de duas horas, ele é indicado com hello alerta no portal de saudação a seguir: "dados de serviço de integridade não são a toodate." Você pode confirmar se Olá afetado do Azure AD Connect Health agent é serviço de integridade de conexão tooupload capaz de dados toohello AD do Azure executando Olá comando PowerShell a seguir:

    Test-AzureADConnectHealthConnectivity -Role ADFS

parâmetro de função Hello usa Olá valores a seguir:

* ADFS
* Sincronizar
* ADICIONA

Você pode usar o sinalizador de ShowResults - Olá em Olá comando tooview logs detalhados. Use Olá exemplo a seguir:

    Test-AzureADConnectHealthConnectivity -Role Sync -ShowResult

> [!NOTE]
> toouse ferramenta de conectividade hello, você deve primeiro registro de agente Olá concluída. Se você não estiver toocomplete capaz de registro de agente de Olá, certifique-se de que atenda a todos os Olá [requisitos](active-directory-aadconnect-health-agent-install.md#requirements) do Azure AD Connect Health. Esse teste de conectividade é executado por padrão durante o registro do agente.
>
>

## <a name="related-links"></a>Links relacionados
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Operações de Azure AD Connect Health](active-directory-aadconnect-health-operations.md)
* [Usando o Azure AD Connect Health com o AD FS](active-directory-aadconnect-health-adfs.md)
* [Usando o Azure AD Connect Health para sincronização](active-directory-aadconnect-health-sync.md)
* [Usar o Azure AD Connect Health com o AD DS](active-directory-aadconnect-health-adds.md)
* [Perguntas frequentes do Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Histórico de versão do Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)
