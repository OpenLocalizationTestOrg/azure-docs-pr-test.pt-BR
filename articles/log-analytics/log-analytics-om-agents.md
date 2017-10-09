---
title: "aaaConnect do Operations Manager tooLog análise | Microsoft Docs"
description: "toomaintain estendido de seu investimento no System Center Operations Manager e usar recursos de análise de Log, você pode integrar o Operations Manager com o seu espaço de trabalho do OMS."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 245ef71e-15a2-4be8-81a1-60101ee2f6e6
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: magoedte
ms.openlocfilehash: b2841c7aa209fec7357dc4c8b1ff4325fdaa37ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-operations-manager-toolog-analytics"></a>Conectar o Operations Manager tooLog análise
toomaintain estendido de seu investimento no System Center Operations Manager e usar recursos de análise de Log, você pode integrar o Operations Manager com o seu espaço de trabalho do OMS.  Isso permite que você aproveitar as oportunidades de saudação do OMS enquanto continua toouse do Operations Manager para:

* Continuar o monitoramento de integridade de saudação de seus serviços de TI com o Operations Manager
* Manter a integração com suas soluções de ITSM com suporte ao gerenciamento de incidentes e problemas
* Gerenciar o ciclo de vida de saudação dos agentes implantados tooon local e nuvem pública máquinas virtuais que você monitorar com o Operations Manager

Integração com o System Center Operations Manager adiciona estratégia de operações de serviço do valor tooyour usando a velocidade de saudação e a eficiência do OMS de coletar, armazenar e analisar dados do Operations Manager.  OMS ajuda a correlacionar e trabalho com relação a identificação de falhas de saudação de problemas e identificar recorrências para oferecer suporte a seu processo de gerenciamento existente do problema.   Olá flexibilidade de saudação pesquisa mecanismo tooexamine desempenho, eventos e alerta de dados, com painéis avançados e reporting recursos tooexpose esses dados de maneiras significativas, demonstra força Olá OMS coloca em como complemento do Operations Manager.

agentes de saudação reporting grupo de gerenciamento do Operations Manager toohello coletam dados de seus servidores com base em fontes de dados de análise de Log hello e soluções habilitadas em sua assinatura do OMS.  Dependendo da solução Olá que você habilitou, dados, essas soluções são enviadas diretamente de um servidor de gerenciamento do Operations Manager toohello OMS o serviço da web, ou devido a saudação volume de dados coletados no sistema gerenciado por agente hello, são enviados diretamente do serviço web do hello agente tooOMS. servidor de gerenciamento Olá encaminha os dados do OMS Olá diretamente toohello OMS web serviço; banco de dados OperationsManager ou OperationsManagerDW toohello nunca será gravada.  Quando um servidor de gerenciamento perde a conectividade com o serviço de web do OMS hello, ele armazena em cache dados saudação localmente até que a comunicação é restabelecida com o OMS.  Se o servidor de gerenciamento Olá estiver offline devido tooplanned manutenção ou paralisação, outro servidor de gerenciamento no grupo de gerenciamento Olá retoma a conectividade com o OMS.  

Olá diagrama a seguir ilustra conexão Olá entre servidores de gerenciamento hello e os agentes em um grupo de gerenciamento do System Center Operations Manager e o OMS, incluindo portas e direção hello.   

![oms-operations-manager-integration-diagram](./media/log-analytics-om-agents/oms-operations-manager-connection.png)

Se suas políticas de segurança de TI não permitir que os computadores em sua toohello tooconnect de rede da Internet, servidores de gerenciamento podem ser configurado tooconnect toohello OMS Gateway tooreceive configuração informações e enviar os dados coletados dependendo na solução Olá ter habilitado.  Para obter mais informações e etapas sobre como tooconfigure seu toocommunicate de grupo de gerenciamento do Operations Manager por meio de um serviço OMS do Gateway do OMS toohello, consulte [conectar computadores tooOMS usando Olá OMS Gateway](log-analytics-oms-gateway.md).  

## <a name="system-requirements"></a>Requisitos do sistema
Antes de começar, examine Olá tooverify detalhes que você atenda aos pré-requisitos a seguir.

* O OMS dá suporte apenas ao Operations Manager 2016, Operations Manager 2012 SP1 UR6 e superior e ao Operations Manager 2012 R2 UR2 e superior.  Foi adicionado suporte a proxy ao Operations Manager 2012 SP1 UR7 e Operations Manager 2012 R2 UR3.
* Todos os agentes do Operations Manager devem atender aos requisitos de suporte mínimos. Certifique-se de que agentes estão no atualização mínima hello, caso contrário, o tráfego de agente do Windows pode falhar e muitos erros podem preencher o log de eventos do Operations Manager de saudação.
* Uma assinatura do OMS.  Para obter informações adicionais, leia a [Introdução ao Log Analytics](log-analytics-get-started.md).

### <a name="network"></a>Rede
informações de saudação abaixo lista Olá proxy e firewall informações de configuração necessárias para o agente do Operations Manager hello, servidores de gerenciamento e toocommunicate do console de operações com o OMS.  Tráfego de cada componente é de saída do seu serviço OMS do toohello de rede.     

|Recurso | Número da porta| Ignorar a Inspeção de HTTP|  
|---------|------|-----------------------|  
|**Agente**|||  
|\*.ods.opinsights.azure.com| 443 |Sim|  
|\*.oms.opinsights.azure.com| 443|Sim|  
|\*.blob.core.windows.net| 443|Sim|  
|\*.azure-automation.net| 443|Sim|  
|**Servidor de gerenciamento**|||  
|\*.service.opinsights.azure.com| 443||  
|\*.blob.core.windows.net| 443| Sim|  
|\*.ods.opinsights.azure.com| 443| Sim|  
|*.azure-automation.net | 443| Sim|  
|**TooOMS de console do Operations Manager**|||  
|service.systemcenteradvisor.com| 443||  
|\*.service.opinsights.azure.com| 443||  
|\*.live.com| 80 e 443||  
|\*.microsoft.com| 80 e 443||  
|\*.microsoftonline.com| 80 e 443||  
|\*.mms.microsoft.com| 80 e 443||  
|login.windows.net| 80 e 443||  


## <a name="connecting-operations-manager-toooms"></a>Conectando o Operations Manager tooOMS
Execute Olá seguinte série de etapas tooconfigure seu tooone de tooconnect do grupo de gerenciamento do Operations Manager dos espaços de trabalho do OMS.

1. No console do Operations Manager hello, selecione Olá **administração** espaço de trabalho.
2. Expanda o nó do hello Operations Management Suite e clique em **Conexão**.
3. Clique em Olá **registrar tooOperations Management Suite** link.
4. Em Olá **operações Assistente integrado do consultor: autenticação** página, insira o endereço de email de saudação ou o número de telefone e a senha da conta de administrador de saudação que é associada à sua assinatura do OMS e clique em  **Entrar no**.
5. Depois que você está autenticado com êxito, no hello **Assistente para integração do Operations Management Suite: selecionar espaço de trabalho** página, são solicitadas tooselect seu espaço de trabalho do OMS.  Se você tiver mais de um espaço de trabalho, selecione Olá espaço de trabalho, você deseja tooregister com grupo de gerenciamento do Operations Manager Olá da lista suspensa de saudação e, em seguida, clique em **próximo**.
   
   > [!NOTE]
   > O Operations Manager dá suporte a apenas um espaço de trabalho do OMS por vez. conexão Olá Olá computadores e que foram registrados tooOMS com espaço de trabalho anterior de saudação são removidos do OMS.
   > 
   > 
6. Em Olá **operações Assistente integrado do consultor: resumo** página, confirme suas configurações e se estiverem corretas, clique em **criar**.
7. Em Olá **operações Assistente integrado do consultor: Concluir** , clique em **fechar**.

### <a name="add-agent-managed-computers"></a>Adicionar computadores gerenciados por agente
Depois de configurar a integração com o seu espaço de trabalho do OMS, isso só estabelece uma conexão com o OMS, sem dados são coletados dos agentes Olá tooyour grupo de gerenciamento de relatórios. Isso só acontecerá depois de configurar quais computadores gerenciados por agente específicos coletam dados para o Log Analytics. Você pode selecionar objetos de computador Olá individualmente ou você pode selecionar um grupo que contenha objetos de computador do Windows. Não é possível selecionar um grupo que contém instâncias de outra classe, como discos lógicos ou Bancos de Dados SQL.

1. Console do Operations Manager abertos hello e selecione Olá **administração** espaço de trabalho.
2. Expanda o nó do hello Operations Management Suite e clique em **Conexão**.
3. Clique em hello **adicionar um grupo decomputadores/** link em ações de saudação título no lado direito de saudação do painel de saudação.
4. Em Olá **pesquisa de computador** caixa de diálogo, você pode pesquisar computadores ou grupos monitorados pelo Operations Manager. Selecione tooOMS tooonboard de computadores ou grupos, clique em **adicionar**e, em seguida, clique em **Okey**.

Você pode exibir os computadores e grupos configurados toocollect dados do nó de computadores gerenciados de saudação sob Operations Management Suite em Olá **administração** espaço de trabalho do console de operações de saudação.  Aqui, é possível adicionar ou remover computadores e grupos conforme necessário.

### <a name="configure-oms-proxy-settings-in-hello-operations-console"></a>Definir configurações de proxy OMS no console de operações de saudação
Execute Olá etapas a seguir se for um servidor proxy interno entre o grupo de gerenciamento hello e o serviço web do OMS.  Essas configurações são gerenciadas centralmente em grupo de gerenciamento de saudação e sistemas distribuídos tooagent gerenciados que estão incluídos nos dados de toocollect escopo Olá para OMS.  Isso é útil para quando determinadas soluções bypass Olá gerenciamento servidor e enviar dados diretamente tooOMS de serviço da web.

1. Console do Operations Manager abertos hello e selecione Olá **administração** espaço de trabalho.
2. Expanda Operations Management Suite e clique em **Conexões**.
3. No hello exibição Conexão do OMS, clique em **configurar servidor Proxy**.
4. Em **Assistente do consultor: servidor Proxy** página, selecione **usar uma tooaccess saudação do servidor proxy Operations Management Suite**, e, em seguida, digite a URL de saudação com número de porta hello, por exemplo, http:// corpproxy:80 e clique **concluir**.

Se o servidor proxy requer autenticação, execute as etapas a seguir de saudação tooconfigure credenciais e configurações que precisam toopropagate toomanaged computadores que relata tooOMS no grupo de gerenciamento de saudação.

1. Console do Operations Manager abertos hello e selecione Olá **administração** espaço de trabalho.
2. Em **Configuração RunAs**, selecione **Perfis**.
3. Olá abrir **Proxy System Center Advisor executado como perfil** perfil.
4. No hello Assistente executar como perfil, clique em Adicionar toouse uma conta executar como. Você pode criar uma conta [Executar Como](https://technet.microsoft.com/library/hh321655.aspx) ou usar uma conta existente. Essa conta precisa toohave suficientes permissões toopass por meio do servidor de proxy de saudação.
5. tooset Olá conta toomanage, escolha **uma classe selecionada, grupo ou objeto**, clique em **selecione...** e, em seguida, clique em **Grupo...** Olá tooopen **grupo pesquisa** caixa.
6. Procure e selecione o **Grupo de Servidores de Monitoramento do Microsoft System Center Advisor**.  Clique em **Okey** depois de selecionar saudação do hello grupo tooclose **grupo pesquisa** caixa.
7. Clique em **Okey** tooclose Olá **adicionar uma conta executar como** caixa.
8. Clique em **salvar** toocomplete Olá assistente e salve as alterações.

Depois de criar conexão hello e configurar quais agentes irá coletar e relatar dados tooOMS, hello configuração a seguir é aplicada no grupo de gerenciamento hello, não necessariamente nesta ordem:

* Olá conta executar como **Microsoft.SystemCenter.Advisor.RunAsAccount.Certificate** é criado.  Ele está associado ao perfil executar como da saudação **System Center Advisor executado como perfil de BLOBs do Microsoft** e o direcionamento de duas classes - **servidor coleta** e **grupo de gerenciamento do Operations Manager** .
* Dois conectores são criados.  Olá primeiro chamado **Microsoft.SystemCenter.Advisor.DataConnector** e é automaticamente configurado com uma assinatura que encaminha todos os alertas gerados a partir de instâncias de todas as classes tooOMS de grupo de gerenciamento Olá Log Análise. conector segundo Olá **Advisor Connector**, que é responsável pela comunicação com o serviço web do OMS e compartilhamento de dados.
* Agentes e grupos que você selecionou toocollect dados no grupo de gerenciamento de saudação é adicionado toohello **grupo de servidor de monitoramento do Microsoft System Center Advisor**.

## <a name="management-pack-updates"></a>Atualizações do pacote de gerenciamento
Após a configuração, o grupo de gerenciamento do Operations Manager Olá estabelece uma conexão com hello serviço OMS.  servidor de gerenciamento de saudação sincroniza com o serviço web de saudação e receber informações de configuração atualizada na forma de saudação de pacotes de gerenciamento para soluções de saudação habilitadas que se integram com o Operations Manager.   O Operations Manager verifica atualizações para esses pacotes de gerenciamento, baixando-as e importando-as imediatamente quando elas estão disponíveis.  Há duas regras específicas que controlam esse comportamento:

* **Microsoft.SystemCenter.Advisor.MPUpdate** -atualizações de pacotes de gerenciamento de OMS base hello. Executada a cada 12 horas por padrão.
* **Microsoft.SystemCenter.Advisor.Core.GetIntelligencePacksRule** - Atualiza os pacotes de gerenciamento de solução habilitados no seu espaço de trabalho. Executada a cada cinco (5) minutos por padrão.

Você pode substituir essas duas regras tooeither impedir download automático, desativando-os ou modificar a frequência de saudação de frequência hello servidor de gerenciamento sincroniza com o OMS toodetermine se um novo pacote de gerenciamento estiver disponível e deve ser baixado.  Siga as etapas de saudação [como tooOverride uma regra ou Monitor](https://technet.microsoft.com/library/hh212869.aspx) toomodify Olá **frequência** parâmetro com um valor em segundos toochange Olá agenda de sincronização ou modificar Olá **habilitado**  regras de saudação do parâmetro toodisable.  Saudação de destino substitui tooall objetos da classe grupo de gerenciamento do Operations Manager.

Se você quiser toocontinue seguindo o processo de controle de alterações existente para controlar versões do pacote de gerenciamento no grupo de gerenciamento de produção, pode desabilitar regras hello e habilitá-los durante horários específicos quando as atualizações são permitidas. Se você tiver um desenvolvimento ou o grupo de gerenciamento de controle de qualidade em seu ambiente e tem toohello de conectividade da Internet, você pode configurar esse grupo de gerenciamento com uma toosupport de espaço de trabalho do OMS neste cenário.  Isso permite que você tooreview e avaliar a versões iterativo Olá Olá OMS de pacotes de gerenciamento antes de liberá-los em seu grupo de gerenciamento de produção.

## <a name="switch-an-operations-manager-group-tooa-new-oms-workspace"></a>Alternar um tooa de grupo do Operations Manager novo espaço de trabalho do OMS
1. Faça logon na assinatura do OMS tooyour e crie um espaço de trabalho em [Microsoft Operations Management Suite](http://oms.microsoft.com/).
2. Console do Operations Manager Olá aberto com uma conta que seja membro da função de administradores do Operations Manager de saudação e selecione Olá **administração** espaço de trabalho.
3. Expanda o Operations Management Suite e selecione **Conexões**.
4. Selecione Olá **configurar novamente a operação Management Suite** link no lado intermediária saudação do painel de saudação.
5. Siga Olá **Assistente para integração do Operations Management Suite** e digite Olá email endereço ou número de telefone e a senha da conta de administrador de saudação que está associada com seu novo espaço de trabalho do OMS.
   
   > [!NOTE]
   > Olá **Assistente para integração do Operations Management Suite: selecionar espaço de trabalho** página apresenta o espaço de trabalho existente do hello que está em uso.
   > 
   > 

## <a name="validate-operations-manager-integration-with-oms"></a>Validar a Integração do Operations Manager com o OMS
Há algumas maneiras diferentes, você pode verificar se seu tooOperations OMS integração Manager foi bem-sucedida.

### <a name="tooconfirm-integration-from-hello-oms-portal"></a>integração de tooconfirm do portal do OMS Olá
1. No portal do OMS hello, clique em Olá **configurações** lado a lado
2. Selecione **Fontes Conectadas**.
3. Na tabela de saudação em Olá seção do System Center Operations Manager, você deve ver o nome de Olá Olá do grupo de gerenciamento listado com número de saudação de agentes e o status ao último recebimento de dados.
   
   ![oms-settings-connectedsources](./media/log-analytics-om-agents/oms-settings-connectedsources.png)
4. Saudação de Observação **ID do espaço de trabalho** valor saudação do lado esquerdo da página de configurações de saudação.  Você a valida junto ao seu grupo de gerenciamento do Operations Manager, abaixo.  

### <a name="tooconfirm-integration-from-hello-operations-console"></a>integração tooconfirm Olá no console de operações
1. Console do Operations Manager abertos hello e selecione Olá **administração** espaço de trabalho.
2. Selecione **pacotes de gerenciamento** e em Olá **procure:** tipo de caixa de texto **Advisor** ou **Intelligence**.
3. Dependendo de você habilitou as soluções hello, verá um pacote de gerenciamento correspondente listado nos resultados da pesquisa de saudação.  Por exemplo, se você tiver habilitado o hello solução de gerenciamento de alertas, o pacote de gerenciamento de saudação gerenciamento de alertas do Microsoft System Center Advisor está na lista de saudação.
4. De saudação **monitoramento** exibir, navegar toohello **Operations Management Suite\Health estado** exibição.  Selecione um servidor de gerenciamento em Olá **estado do servidor de gerenciamento** painel e em Olá **exibição de detalhes** painel Confirmar valor Olá propriedade **URI do serviço de autenticação** coincide com a ID do espaço de trabalho do OMS Olá
   
   ![oms-opsmgr-mg-authsvcuri-property-ms](./media/log-analytics-om-agents/oms-opsmgr-mg-authsvcuri-property-ms.png)

## <a name="remove-integration-with-oms"></a>Remover a Integração com o OMS
Quando você não precisa mais integração entre o grupo de gerenciamento do Operations Manager e o espaço de trabalho do OMS, há várias etapas necessárias tooproperly remover Olá conexão e a configuração no grupo de gerenciamento de saudação. Olá procedimento a seguir tem você atualizar seu espaço de trabalho do OMS, excluindo a referência de saudação do seu grupo de gerenciamento, exclua Olá OMS conectores e, em seguida, excluir pacotes de gerenciamento com suporte do OMS.   

Pacotes de gerenciamento para soluções de saudação habilitadas que se integram com o Operations Manager e integração de toosupport necessária de pacotes de gerenciamento de Olá com hello serviço OMS não pode ser excluída facilmente saudação do grupo de gerenciamento.  Isso ocorre porque alguns dos pacotes de gerenciamento do OMS Olá tem dependências em outros pacotes de gerenciamento relacionados.  toodelete pacotes de gerenciamento com uma dependência em outros pacotes de gerenciamento, baixe o script hello [remover um pacote de gerenciamento com dependências](https://gallery.technet.microsoft.com/scriptcenter/Script-to-remove-a-84f6873e) do TechNet Script Center.  

1. Abra Olá Shell de comando do Operations Manager com uma conta que seja membro da função de administradores do Operations Manager hello.
   
    > [!WARNING]
    > Verifique se você não tiver pacotes de gerenciamento personalizados com palavra hello Supervisor ou IntelligencePack em nome de saudação antes de prosseguir, caso contrário, Olá etapas excluí-los a saudação do grupo de gerenciamento.
    > 

2. No prompt de shell de comando hello, digite`Get-SCOMManagementPack -name "*Advisor*" | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`
3. Em seguida, digite `Get-SCOMManagementPack -name “*IntelligencePack*” | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`
4. pacotes de pacotes de gerenciamento restantes que possuem uma dependência em outro gerenciamento do System Center Advisor tooremove, use o script hello *RecursiveRemove.ps1* baixado do hello TechNet Script Center anteriormente.  
 
    > [!NOTE]
    > Não exclua os pacotes de gerenciamento do Microsoft System Center Advisor ou o Microsoft System Center Advisor interno hello.  
    >  

5. Abra o console de operações do Operations Manager Olá com uma conta que seja membro da função de administradores do Operations Manager hello.
6. Em **administração**, selecione Olá **pacotes de gerenciamento** nó e em Olá **procure:** , digite **Advisor** e verifique se Olá ainda, os seguintes pacotes de gerenciamento são importados no grupo de gerenciamento:
   
   * Microsoft System Center Advisor
   * Microsoft System Center Advisor Interno
7. No portal do OMS hello, clique em Olá **configurações** lado a lado.
8. Selecione **Fontes Conectadas**.
9. Na tabela de saudação em Olá seção do System Center Operations Manager, você deve ver o nome de Olá Olá do grupo de gerenciamento que você deseja tooremove do espaço de trabalho de saudação.  Na coluna Olá **últimos dados**, clique em **remover**.  
   
    > [!NOTE]
    > Olá **remover** link não estará disponível até depois de 14 dias se não houver nenhuma atividade detectada a partir do grupo de gerenciamento conectado hello.  
    > 

10. Uma janela será exibida solicitando que você tooconfirm que você deseja tooproceed com a remoção de saudação.  Clique em **Sim** tooproceed. 

toodelete Olá dois conectores - Microsoft.SystemCenter.Advisor.DataConnector e o conector do Advisor, salve o script do PowerShell Olá abaixo tooyour computador e executar usando Olá exemplos a seguir:

```
    .\OM2012_DeleteConnector.ps1 “Advisor Connector” <ManagementServerName>
    .\OM2012_DeleteConnectors.ps1 “Microsoft.SytemCenter.Advisor.DataConnector” <ManagementServerName>
```

> [!NOTE]
> computador Olá de que executar este script, se não for um servidor de gerenciamento deve ter o shell de comando do Operations Manager Olá instalado dependendo da versão de saudação do seu grupo de gerenciamento.
> 
> 

```
    `param(
    [String] $connectorName,
    [String] $msName="localhost"
    )
    $mg = new-object Microsoft.EnterpriseManagement.ManagementGroup $msName
    $admin = $mg.GetConnectorFrameworkAdministration()
    ##########################################################################################
    # Configures a connector with hello specified name.
    ##########################################################################################
    function New-Connector([String] $name)
    {
         $connectorForTest = $null;
         foreach($connector in $admin.GetMonitoringConnectors())
    {
    if($connectorName.Name -eq ${name})
    {
         $connectorForTest = Get-SCOMConnector -id $connector.id
    }
    }
    if ($connectorForTest -eq $null)
    {
         $testConnector = New-Object Microsoft.EnterpriseManagement.ConnectorFramework.ConnectorInfo
         $testConnector.Name = $name
         $testConnector.Description = "${name} Description"
         $testConnector.DiscoveryDataIsManaged = $false
         $connectorForTest = $admin.Setup($testConnector)
         $connectorForTest.Initialize();
    }
    return $connectorForTest
    }
    ##########################################################################################
    # Removes a connector with hello specified name.
    ##########################################################################################
    function Remove-Connector([String] $name)
    {
        $testConnector = $null
        foreach($connector in $admin.GetMonitoringConnectors())
       {
        if($connector.Name -eq ${name})
       {
         $testConnector = Get-SCOMConnector -id $connector.id
       }
      }
     if ($testConnector -ne $null)
     {
        if($testConnector.Initialized)
     {
     foreach($alert in $testConnector.GetMonitoringAlerts())
     {
       $alert.ConnectorId = $null;
       $alert.Update("Delete Connector");
     }
     $testConnector.Uninitialize()
     }
     $connectorIdForTest = $admin.Cleanup($testConnector)
     }
    }
    ##########################################################################################
    # Delete a connector's Subscription
    ##########################################################################################
    function Delete-Subscription([String] $name)
    {
      foreach($testconnector in $admin.GetMonitoringConnectors())
      {
      if($testconnector.Name -eq $name)
      {
        $connector = Get-SCOMConnector -id $testconnector.id
      }
    }
    $subs = $admin.GetConnectorSubscriptions()
    foreach($sub in $subs)
    {
      if($sub.MonitoringConnectorId -eq $connector.id)
      {
        $admin.DeleteConnectorSubscription($admin.GetConnectorSubscription($sub.Id))
      }
     }
    }
    #New-Connector $connectorName
    write-host "Delete-Subscription"
    Delete-Subscription $connectorName
    write-host "Remove-Connector"
    Remove-Connector $connectorName
```

Na Olá futuras se você planeja reconectar seu gerenciamento grupo tooan OMS espaço de trabalho, você precisa importar toore Olá `Microsoft.SystemCenter.Advisor.Resources.\<Language>\.mpb` arquivo de pacote de gerenciamento do pacote cumulativo de atualização mais recente da saudação aplicado tooyour grupo de gerenciamento.  Você pode encontrar esse arquivo na Olá `%ProgramFiles%\Microsoft System Center 2012` ou hello `System Center 2012 R2\Operations Manager\Server\Management Packs for Update Rollups` pasta.

## <a name="next-steps"></a>Próximas etapas
funcionalidade de tooadd e coletar dados, consulte [soluções de análise de Log adicionar da Galeria de soluções de saudação](log-analytics-add-solutions.md).


