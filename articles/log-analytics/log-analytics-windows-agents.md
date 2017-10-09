---
title: "aaaConnect Windows computadores tooAzure análise de Log | Microsoft Docs"
description: "Este artigo mostra computadores com Windows hello etapas tooconnect Olá no seu toohello de infraestrutura no local de serviço de análise de Log usando uma versão personalizada do hello agente de monitoramento da Microsoft (MMA)."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 932f7b8c-485c-40c1-98e3-7d4c560876d2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7e15f9eeb0440bd2f6557d7215df701526e4f9aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-windows-computers-toohello-log-analytics-service-in-azure"></a>Conecte-se o serviço de análise de logs do Windows computadores toohello no Azure

Este artigo mostra etapas Olá tooconnect computadores com Windows em seus espaços de trabalho de tooOMS de infraestrutura local usando uma versão personalizada do hello agente de monitoramento da Microsoft (MMA). Você precisa tooinstall e conectar agentes para todos os computadores de saudação que você deseja tooonboard para poderem serviço de análise de Log toosend dados toohello e tooview e agir sobre dados. Cada agente pode relatar toomultiple espaços de trabalho.

Você pode instalar agentes usando a Instalação, a linha de comando ou com o DSC (Configuração de Estado Desejado) na Automação do Azure.  

>[!NOTE]
Para máquinas virtuais em execução no Azure, você poderá simplificar a instalação usando Olá [extensão da máquina virtual](log-analytics-azure-vm-extension.md).

Em computadores com conectividade com a Internet, o agente de saudação usa Olá conexão toohello Internet toosend dados tooOMS. Para computadores que não tem conectividade com a Internet, você pode usar um proxy ou Olá [OMS Gateway](log-analytics-oms-gateway.md).

Conectar-se a sua tooOMS de computadores do Windows é simples em três etapas simples:

1. Baixar o arquivo de configuração do agente de saudação do portal do OMS Olá
2. Instalar o agente de saudação usando o método hello escolhido
3. Configurar o agente de saudação ou adicionar espaços de trabalho adicionais, se necessário

Hello diagrama a seguir mostra a relação Olá entre computadores com Windows e o OMS depois que você instalou e configurou os agentes.

![oms-direct-agent-diagram](./media/log-analytics-windows-agents/oms-direct-agent-diagram.png)

Se suas políticas de segurança de TI não permitir que os computadores em sua toohello tooconnect de rede da Internet, você pode configurar seu toohello de tooconnect computadores Gateway do OMS. Para obter mais informações e etapas sobre como tooconfigure toocommunicate seus servidores através de um serviço OMS do Gateway do OMS toohello, consulte [conectar computadores tooOMS usando Olá OMS Gateway](log-analytics-oms-gateway.md).

## <a name="system-requirements-and-required-configuration"></a>Requisitos do sistema e a configuração necessária
Antes de instalar ou implantar agentes, examine Olá tooensure detalhes que você atende aos requisitos de saudação a seguir.

- Você só pode instalar Olá OMS MMA em computadores que executam o Windows Server 2008 SP 1 ou posterior ou Windows 7 SP1 ou posterior.
- É necessária uma assinatura do Azure.  Para saber mais, confira [Introdução ao Log Analytics](log-analytics-get-started.md).
- Cada computador do Windows deve ser capaz de tooconnect toohello Internet usando HTTPS ou toohello Gateway do OMS. Essa conexão pode ser direta por meio de um proxy, ou Olá Gateway do OMS.
- Você pode instalar Olá OMS MMA em máquinas virtuais, servidores e computadores autônomos. Se você quiser tooconnect tooOMS de máquinas virtuais hospedadas pelo Azure, consulte [tooLog de máquinas virtuais do Azure conectar análise](log-analytics-azure-vm-extension.md).
- Agente de saudação precisa toouse a porta TCP 443 para vários recursos.

### <a name="network"></a>Rede

Para Windows agentes tooconnect tooand registrar no serviço do OMS hello, eles devem ter acesso de recursos toonetwork, incluindo URLs de domínio e os números de porta de saudação.

- Para servidores proxy, você precisa tooensure que Olá recursos configurados nas configurações do agente de servidor de proxy apropriados.
- Para firewalls que restringem o acesso toohello da Internet, você ou sua rede engenheiros necessário tooconfigure tooOMS de acesso de toopermit seu firewall. Nenhuma ação é necessária nas configurações do agente.

Olá, a tabela a seguir mostra os recursos necessários para comunicação.

>[!NOTE]
>Alguns dos Olá recursos a seguir mencionam Insights operacionais, que era o nome anterior para análise de Log.

| Recurso de agente | Portas | Ignorar a inspeção de HTTPS |
|---|---|---|
| *.ods.opinsights.azure.com | 443 | Sim |
| *.oms.opinsights.azure.com | 443 | Sim |
| *.blob.core.windows.net | 443 | Sim |
| *.azure-automation.net | 443 | Sim |



## <a name="download-hello-agent-setup-file-from-oms"></a>Baixar o arquivo de configuração do agente de saudação do OMS
1. No portal do OMS hello, em Olá **visão geral** , clique em Olá **configurações** lado a lado.  Clique em Olá **fontes conectadas** guia na parte superior da saudação.  
    ![Guia Fontes Conectadas](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)
2. Clique em **servidores Windows** e, em seguida, clique em **baixar o agente do Windows** arquivo de instalação aplicável tooyour computador processador tipo toodownload hello.
3. Em saudação à direita do **ID do espaço de trabalho**, clique Olá ícone para copiar e colar Olá ID no bloco de notas.
4. Em saudação à direita do **chave primária**, clique Olá ícone para copiar e colar chave Olá no bloco de notas.     

## <a name="install-hello-agent-using-setup"></a>Instalar agente hello usando a instalação
1. Execute o agente de saudação de tooinstall de instalação em um computador que você deseja toomanage.
2. Na página de boas-vindas hello, clique em **próximo**.
3. Na página de termos de licença hello, leia Olá da licença e, em seguida, clique em **concordo**.
4. Na página de pasta de destino hello, alterar ou mantenha a pasta de instalação padrão hello e, em seguida, clique em **próximo**.
5. Na página de opções de instalação do agente Olá, você pode escolher tooconnect Olá agente tooAzure análise de Log (OMS), Operations Manager, ou você pode deixar as escolhas de saudação em branco se desejar usar o agente de saudação tooconfigure mais tarde. Clique em **Avançar**.   
    - Se você escolheu tooconnect tooAzure Log Analytics (OMS), cole Olá **ID do espaço de trabalho** e **chave do espaço de trabalho (chave primária)** que você copiou no bloco de notas no procedimento anterior do hello e, em seguida, clique em  **Próxima**.  
        ![colar ID de Espaço de Trabalho e a Chave Primária](./media/log-analytics-windows-agents/connect-workspace.png)
    - Se você escolheu tooconnect tooOperations Manager, digite Olá **nome do grupo de gerenciamento**, **Management Server** nome, e **porta do servidor de gerenciamento**e, em seguida, clique em **Próxima**. Na página de conta de Ação agente hello, escolha a conta do sistema Local hello ou uma conta de domínio local e, em seguida, clique em **próximo**.  
        ![configuração do grupo de gerenciamento ](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![conta de ação de agente](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)

6. Na página de tooInstall pronto do hello, revise suas escolhas e clique em **instalar**.
7. Em Olá configuração concluída com êxito, clique em **concluir**.
8. Ao concluir, Olá **Microsoft Monitoring Agent** aparece na **painel de controle**. Você pode examinar sua configuração existe e verificar que o agente de saudação é conectado tooOperational Insights (OMS). Quando conectados tooOMS, Olá agent exibirá uma mensagem dizendo: **Olá Microsoft Monitoring Agent tiver conectado com êxito o serviço do Microsoft Operations Management Suite toohello.**

## <a name="configure-proxy-settings"></a>Definir configurações de proxy

Você pode usar o hello seguindo as configurações de proxy do procedimento tooconfigure para Olá Microsoft Monitoring Agent usando o painel de controle. Você precisa toouse este procedimento para cada servidor. Se você tiver vários servidores que você precisa tooconfigure, talvez seja mais fácil toouse tooautomate um script esse processo. Nesse caso, consulte o procedimento a seguir Olá [tooconfigure as configurações de proxy para Olá Microsoft Monitoring Agent usando um script](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).

### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-control-panel"></a>configurações de proxy de tooconfigure para Olá Microsoft Monitoring Agent usando o painel de controle
1. Abra o **Painel de controle**.
2. Abra o **Microsoft Monitoring Agent**.
3. Clique em Olá **as configurações de Proxy** guia.  
    ![guia Configurações de proxy](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)
4. Selecione **usar um servidor proxy** e digite a URL de saudação e número da porta, se necessário, semelhante toohello exemplo mostrado. Se o servidor proxy requer autenticação, digite Olá username e password tooaccess Olá servidor proxy.


### <a name="verify-agent-connectivity-toooms"></a>Verifique se tooOMS de conectividade do agente

Você pode facilmente verificar se os agentes estão se comunicando com o OMS usando Olá procedimento a seguir:

1.  No computador de saudação com o agente do Windows hello, abra o painel de controle.
2.  Abra o Microsoft Monitoring Agent.
3.  Clique em Guia do hello Azure Log Analytics (OMS).
4.  Na coluna de Status hello, você verá que o agente Olá conectado com êxito de serviço do Operations Management Suite toohello.

![agente conectado](./media/log-analytics-windows-agents/mma-connected.png)


### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-a-script"></a>configurações de proxy de tooconfigure para Olá Microsoft Monitoring Agent usando um script
Copie Olá seguinte exemplo, atualizá-lo com o ambiente de tooyour específicas de informações, salve-o com uma extensão de nome de arquivo PS1 e, em seguida, execute o script de saudação em cada computador que se conecta diretamente de serviço do OMS toohello.

    param($ProxyDomainName="http://proxy.contoso.com:80", $cred=(Get-Credential))

    # First we get hello Health Service configuration object.  We need toodetermine if we
    #have hello right update rollup with hello API we need.  If not, no need toorun hello rest of hello script.
    $healthServiceSettings = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'

    $proxyMethod = $healthServiceSettings | Get-Member -Name 'SetProxyInfo'

    if (!$proxyMethod)
    {
         Write-Output 'Health Service proxy API not present, will not update settings.'
         return
    }

    Write-Output "Clearing proxy settings."
    $healthServiceSettings.SetProxyInfo('', '', '')

    $ProxyUserName = $cred.username

    Write-Output "Setting proxy too$ProxyDomainName with proxy username $ProxyUserName."
    $healthServiceSettings.SetProxyInfo($ProxyDomainName, $ProxyUserName, $cred.GetNetworkCredential().password)



## <a name="install-hello-agent-using-hello-command-line"></a>Instalar o agente de Olá usando a linha de comando de saudação
- Modifique e, em seguida, use Olá após o agente de saudação tooinstall de exemplo usando a linha de comando de saudação. exemplo Hello executa uma instalação completamente silenciosa.

    >[!NOTE]
    Se você quiser tooupgrade um agente, você precisa toouse Olá análise de Log do API de script. Consulte Olá tooupgrade próximo da seção um agente.

    ```dos
    MMASetup-AMD64.exe /Q:A /R:N /C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1"
    ```

Agente de saudação usa IExpress como seu Self-extractor usando Olá `/c` comando. Você pode ver as opções de linha de comando de saudação em [de linha de comando para IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) e, em seguida, atualização Olá exemplo toosuit suas necessidades.

|Opções específicas do MMA                   |Observações         |
|---------------------------------------|--------------|
|ADD_OPINSIGHTS_WORKSPACE               | 1 = Configurar Olá agente tooreport tooa área de trabalho                |
|OPINSIGHTS_WORKSPACE_ID                | Id do espaço de trabalho (guid) para Olá tooadd de espaço de trabalho                    |
|OPINSIGHTS_WORKSPACE_KEY               | Tooinitially usado chave do espaço de trabalho autenticar com o espaço de trabalho de saudação |
|OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE  | Especifique o ambiente de nuvem Olá onde se encontra o espaço de trabalho de saudação <br> 0 = nuvem comercial do Azure (padrão) <br> 1 = Azure Governamental |
|OPINSIGHTS_PROXY_URL               | URI para Olá proxy toouse |
|OPINSIGHTS_PROXY_USERNAME               | Nome de usuário tooaccess um proxy autenticado |
|OPINSIGHTS_PROXY_PASSWORD               | Senha tooaccess um proxy autenticado |

>[!NOTE]
limite de tamanho de linha de comando de saudação de atingir do tooavoid de IExpress, instalar o agente de saudação com nenhum espaço de trabalho configurado e, em seguida, usar uma configuração de tooset de script para o espaço de trabalho de saudação.

>[!NOTE]
Se você receber um `Command line option syntax error.` ao usar o hello `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` parâmetro, você pode usar o hello solução alternativa a seguir:
```dos
MMASetup-AMD64.exe /C /T:.\MMAExtract
cd .\MMAExtract
setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1
```

## <a name="add-a-workspace-using-a-script"></a>Adicionar um espaço de trabalho usando um script
Adicione um espaço de trabalho com API de script do agente de análise de Log de Olá Olá exemplo a seguir:

```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey)
$mma.ReloadConfiguration()
```

tooadd um espaço de trabalho no Azure do governo dos EUA, use Olá exemplo de script a seguir:
```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey, 1)
$mma.ReloadConfiguration()
```

>[!NOTE]
Se você usou Olá linha de comando ou script anteriormente tooinstall ou configurar o agente Olá, `EnableAzureOperationalInsights` foi substituído pelo `AddCloudWorkspace`.

## <a name="install-hello-agent-using-dsc-in-azure-automation"></a>Instalar o agente de saudação usando DSC na automação do Azure

Você pode usar o hello após o agente de saudação do script exemplo tooinstall usando DSC na automação do Azure. exemplo Hello instala Olá agente de 64 bits, identificado por Olá `URI` valor. Você também pode usar a versão de 32 bits hello, substituindo o valor URI de saudação. Olá URIs para ambas as versões são:

- Agente do Windows de 64 bits – https://go.microsoft.com/fwlink/?LinkId=828603
- Agente do Windows de 32 bits – https://go.microsoft.com/fwlink/?LinkId=828604


>[!NOTE]
Este exemplo de procedimento e de script não atualizará um agente existente.

1. Importar Olá xPSDesiredStateConfiguration módulo de DSC de [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) na automação do Azure.  
2.  Crie ativos de variável da Automação do Azure para *OPSINSIGHTS_WS_ID* e *OPSINSIGHTS_WS_KEY*. Definir *OPSINSIGHTS_WS_ID* tooyour ID de espaço de trabalho de análise de logs do OMS e defina *OPSINSIGHTS_WS_KEY* toohello a chave primária de seu espaço de trabalho.
3.  Use Olá seguinte script e salve-o como MMAgent.ps1
4.  Modifique e, em seguida, use Olá após o agente de saudação tooinstall de exemplo usando a DSC na automação do Azure. Importe MMAgent.ps1 para automação do Azure usando a interface de automação do Azure hello ou cmdlet.
5.  Atribua uma configuração de toohello do nó. Dentro de 15 minutos, nó Olá verifica sua configuração e Olá MMA é enviada por push toohello nó.

```PowerShell
Configuration MMAgent
{
    $OIPackageLocalPath = "C:\MMASetup-AMD64.exe"
    $OPSINSIGHTS_WS_ID = Get-AutomationVariable -Name "OPSINSIGHTS_WS_ID"
    $OPSINSIGHTS_WS_KEY = Get-AutomationVariable -Name "OPSINSIGHTS_WS_KEY"


    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    Node OMSnode {
        Service OIService
        {
            Name = "HealthService"
            State = "Running"
            DependsOn = "[Package]OI"
        }

        xRemoteFile OIPackage {
            Uri = "https://go.microsoft.com/fwlink/?LinkId=828603"
            DestinationPath = $OIPackageLocalPath
        }

        Package OI {
            Ensure = "Present"
            Path  = $OIPackageLocalPath
            Name = "Microsoft Monitoring Agent"
            ProductId = "8A7F2C51-4C7D-4BFD-9014-91D11F24AAE2"
            Arguments = '/C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=' + $OPSINSIGHTS_WS_ID + ' OPINSIGHTS_WORKSPACE_KEY=' + $OPSINSIGHTS_WS_KEY + ' AcceptEndUserLicenseAgreement=1"'
            DependsOn = "[xRemoteFile]OIPackage"
        }
    }
}


```

### <a name="get-hello-latest-productid-value"></a>Obter o valor de ProductId mais recente Olá

Olá `ProductId value` Olá MMAgent.ps1 script é exclusivo tooeach versão do agente. Quando uma versão atualizada de cada agente é publicada, Olá ProductId valor é alterado. Portanto, quando Olá ProductId alterado de saudação futura, você pode descobrir a versão do agente de hello usando um script simples. Depois que você tiver Olá versão do agente mais recente instalado em um servidor de teste, você pode usar o hello seguinte valor de ProductId do script tooget Olá instalado. Usando o valor de ProductId hello mais recente, você pode atualizar o valor de saudação em Olá MMAgent.ps1 script.

```PowerShell
$InstalledApplications  = Get-ChildItem hklm:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall


foreach ($Application in $InstalledApplications)

{

     $Key = Get-ItemProperty $Application.PSPath

     if ($Key.DisplayName -eq "Microsoft Monitoring Agent")

     {

        $Key.DisplayName

        Write-Output ("Product ID is: " + $Key.PSChildName.Substring(1,$Key.PSChildName.Length -2))

     }

}  
```

## <a name="configure-an-agent-manually-or-add-additional-workspaces"></a>Configurar um agente manualmente ou adicionar outros espaços de trabalho
Se você instalou agentes, mas não os configurou ou se desejar que os espaços de trabalho do agente tooreport toomultiple hello, você pode usar o hello informações tooenable um agente a segui-lo ou reconfigurá-lo. Depois que você tiver configurado o agente de hello, ele registrará o serviço do agente hello e obterá informações de configuração necessárias e os pacotes de gerenciamento que contêm informações de solução.

1. Depois de instalar Olá Microsoft Monitoring Agent, abra **painel de controle**.
2. Abra **Microsoft Monitoring Agent** e, em seguida, clique em Olá **Azure Log Analytics (OMS)** guia.   
3. Clique em **adicionar** tooopen Olá **adicionar um espaço de trabalho de análise de Log** caixa.
4. Saudação de colar **ID do espaço de trabalho** e **chave do espaço de trabalho (chave primária)** que você copiou no bloco de notas no procedimento anterior para espaço de trabalho de saudação que você deseja tooadd e, em seguida, clique em **Okey**.  
    ![configurar o Azure Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)

Depois que dados são coletados de computadores monitorados por agente Olá, número de saudação dos computadores monitorados pelo OMS será exibido no portal do OMS Olá em Olá **fontes conectadas** guia **configurações** como  **Servidores conectados**.


## <a name="toodisable-an-agent"></a>toodisable um agente
1. Depois de instalar o agente hello, abra **painel de controle**.
2. Abra o Microsoft Monitoring Agent e clique em Olá **Azure Log Analytics (OMS)** guia.
3. Selecione um espaço de trabalho e clique em **Remover**. Repita essa etapa para todos os outros espaços de trabalho.


## <a name="optionally-configure-agents-tooreport-tooan-operations-manager-management-group"></a>Opcionalmente, configure o grupo de gerenciamento do agentes tooreport tooan do Operations Manager

Se você usar o Operations Manager em sua infraestrutura de TI, você também pode usar o agente MMA hello como um agente do Operations Manager.

### <a name="tooconfigure-mma-agents-tooreport-tooan-operations-manager-management-group"></a>grupo de gerenciamento tooconfigure MMA agentes tooreport tooan do Operations Manager
1.  No computador de saudação onde Olá é instalado, abra **painel de controle**.  
2.  Abra **Microsoft Monitoring Agent** e, em seguida, clique em Olá **Operations Manager** guia.  
    ![Guia Microsoft Monitoring Agent Operations Manager](./media/log-analytics-windows-agents/om-mg01.png)
3.  Se seus servidores do Operations Manager tiverem integração com o Active Directory, clique em **Atualizar automaticamente as atribuições de grupo de gerenciamento do AD DS**.
4.  Clique em **adicionar** tooopen Olá **adicionar um grupo de gerenciamento** caixa de diálogo.  
    ![Adicionar um Grupo de Gerenciamento do Microsoft Monitoring Agent](./media/log-analytics-windows-agents/oms-mma-om02.png)
5.  Em **nome do grupo de gerenciamento** caixa, digite o nome de saudação do seu grupo de gerenciamento.
6.  Em Olá **servidor de gerenciamento primário** caixa, digite o nome de computador de saudação do servidor de gerenciamento primário de saudação.
7.  Em Olá **porta do servidor de gerenciamento** caixa tipo hello número da porta TCP.
8.  Em **conta de Ação agente**, escolha a conta do sistema Local hello ou uma conta de domínio local.
9.  Clique em **Okey** tooclose Olá **adicionar um grupo de gerenciamento** caixa de diálogo e clique **Okey** tooclose Olá **propriedades do agente de monitoramento Microsoft**caixa de diálogo.


## <a name="next-steps"></a>Próximas etapas

- [Adicionar soluções de análise de Log de saudação Galeria de soluções](log-analytics-add-solutions.md) tooadd funcionalidade e reunir dados.
